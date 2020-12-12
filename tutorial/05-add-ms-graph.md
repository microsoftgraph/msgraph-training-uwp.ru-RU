<!-- markdownlint-disable MD002 MD041 -->

В этом упражнении вы включаете Microsoft Graph в приложение. Для этого приложения вы будете использовать клиентскую библиотеку Microsoft Graph для [.NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) для вызова Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Получить события календаря из Outlook

1. Добавьте новую страницу для представления календаря. Щелкните правой кнопкой мыши проект **GraphTutorial** в обозревателе решений и **выберите "Добавить > новый элемент...".** Выберите **пустую страницу,** `CalendarPage.xaml` введите в поле **"Имя"** и выберите **"Добавить".**

1. Откройте `CalendarPage.xaml` и добавьте следующую строку в существующий `<Grid>` элемент.

    ```xaml
    <TextBlock x:Name="Events" TextWrapping="Wrap"/>
    ```

1. Откройте `CalendarPage.xaml.cs` и добавьте следующие утверждения в `using` верхней части файла.

    ```csharp
    using Microsoft.Graph;
    using Microsoft.Toolkit.Graph.Providers;
    using Microsoft.Toolkit.Uwp.UI.Controls;
    using Newtonsoft.Json;
    ```

1. Добавьте в класс следующие `CalendarPage` функции.

    ```csharp
    private void ShowNotification(string message)
    {
        // Get the main page that contains the InAppNotification
        var mainPage = (Window.Current.Content as Frame).Content as MainPage;

        // Get the notification control
        var notification = mainPage.FindName("Notification") as InAppNotification;

        notification.Show(message);
    }

    protected override async void OnNavigatedTo(NavigationEventArgs e)
    {
        // Get the Graph client from the provider
        var graphClient = ProviderManager.Instance.GlobalProvider.Graph;

        try
        {
            // Get the user's mailbox settings to determine
            // their time zone
            var user = await graphClient.Me.Request()
                .Select(u => new { u.MailboxSettings })
                .GetAsync();

            var startOfWeek = GetUtcStartOfWeekInTimeZone(DateTime.Today, user.MailboxSettings.TimeZone);
            var endOfWeek = startOfWeek.AddDays(7);

            var queryOptions = new List<QueryOption>
            {
                new QueryOption("startDateTime", startOfWeek.ToString("o")),
                new QueryOption("endDateTime", endOfWeek.ToString("o"))
            };

            // Get the events
            var events = await graphClient.Me.CalendarView.Request(queryOptions)
                .Header("Prefer", $"outlook.timezone=\"{user.MailboxSettings.TimeZone}\"")
                .Select(ev => new
                {
                    ev.Subject,
                    ev.Organizer,
                    ev.Start,
                    ev.End
                })
                .OrderBy("start/dateTime")
                .Top(50)
                .GetAsync();

            // TEMPORARY: Show the results as JSON
            Events.Text = JsonConvert.SerializeObject(events.CurrentPage);
        }
        catch (ServiceException ex)
        {
            ShowNotification($"Exception getting events: {ex.Message}");
        }

        base.OnNavigatedTo(e);
    }

    private static DateTime GetUtcStartOfWeekInTimeZone(DateTime today, string timeZoneId)
    {
        TimeZoneInfo userTimeZone = TimeZoneInfo.FindSystemTimeZoneById(timeZoneId);

        // Assumes Sunday as first day of week
        int diff = System.DayOfWeek.Sunday - today.DayOfWeek;

        // create date as unspecified kind
        var unspecifiedStart = DateTime.SpecifyKind(today.AddDays(diff), DateTimeKind.Unspecified);

        // convert to UTC
        return TimeZoneInfo.ConvertTimeToUtc(unspecifiedStart, userTimeZone);
    }
    ```

    Рассмотрим, что делает `OnNavigatedTo` код.

    - Будет вызван URL-адрес `/me/calendarview` .
        - Параметры `startDateTime` `endDateTime` и параметров определяют начало и конец представления календаря.
        - Заглавная часть приводит к возвращению событий в часовом поясе `Prefer: outlook.timezone` `start` `end` пользователя.
        - Функция `Select` ограничивает поля, возвращаемые для каждого события, только теми, которые будут фактически использовать приложение.
        - Функция `OrderBy` сортировать результаты по дате и времени начала.
        - Функция `Top` запрашивает не более 50 событий.

1. Измените `NavView_ItemInvoked` метод в `MainPage.xaml.cs` файле, чтобы заменить существующий `switch` параметр на следующий.

    ```csharp
    switch (invokedItem.ToLower())
    {
        case "new event":
            throw new NotImplementedException();
            break;
        case "calendar":
            RootFrame.Navigate(typeof(CalendarPage));
            break;
        case "home":
        default:
            RootFrame.Navigate(typeof(HomePage));
            break;
    }
    ```

Теперь вы можете запустить приложение, войти  в систему и щелкнуть элемент навигации "Календарь" в левом меню. Вы увидите дамп событий в JSON в календаре пользователя.

## <a name="display-the-results"></a>Отображение результатов

1. Замените все содержимое на `CalendarPage.xaml` следующее:

    ```xaml
    <Page
        x:Class="GraphTutorial.CalendarPage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:GraphTutorial"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
        mc:Ignorable="d"
        Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

        <Grid>
            <controls:DataGrid x:Name="EventList" Grid.Row="1"
                    AutoGenerateColumns="False">
                <controls:DataGrid.Columns>
                    <controls:DataGridTextColumn
                            Header="Organizer"
                            Width="SizeToCells"
                            Binding="{Binding Organizer.EmailAddress.Name}"
                            FontSize="20" />
                    <controls:DataGridTextColumn
                            Header="Subject"
                            Width="SizeToCells"
                            Binding="{Binding Subject}"
                            FontSize="20" />
                    <controls:DataGridTextColumn
                            Header="Start"
                            Width="SizeToCells"
                            Binding="{Binding Start.DateTime}"
                            FontSize="20" />
                    <controls:DataGridTextColumn
                            Header="End"
                            Width="SizeToCells"
                            Binding="{Binding End.DateTime}"
                            FontSize="20" />
                </controls:DataGrid.Columns>
            </controls:DataGrid>
        </Grid>
    </Page>
    ```

1. Откройте `CalendarPage.xaml.cs` и замените `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` строку на следующую.

    ```csharp
    EventList.ItemsSource = events.CurrentPage.ToList();
    ```

    Если запустить приложение сейчас и выбрать календарь, вы получите список событий в сетке данных. Однако значения **start** и **End** отображаются не для пользователей. Вы можете управлять отображением этих значений с помощью [преобразоващика значений.](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter)

1. Щелкните правой кнопкой мыши проект **GraphTutorial** в обозревателе решений и **выберите add > Class...**. Назовем класс `GraphDateTimeTimeZoneConverter.cs` и выберите **"Добавить".** Замените все содержимое файла на следующее:

    :::code language="csharp" source="../demo/GraphTutorial/GraphDateTimeTimeZoneConverter.cs" id="ConverterSnippet":::

    Этот код принимает [структуру dateTimeTimeZone,](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) возвращаемую Microsoft Graph, и разбирает ее в `DateTimeOffset` объект. Затем он преобразует значение в часовой пояс пользователя и возвращает отформатированные значения.

1. Откройте `CalendarPage.xaml` и добавьте следующее **перед** `<Grid>` элементом.

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="ResourcesSnippet":::

1. Замените два `DataGridTextColumn` последних элемента на следующие.

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="BindingSnippet" highlight="4,9":::

1. Запустите приложение, войдите в систему и щелкните элемент **навигации календаря.** Должен отформатирован список событий со значениями **start** и **End.**

    ![Снимок экрана с таблицей событий](./images/add-msgraph-01.png)
