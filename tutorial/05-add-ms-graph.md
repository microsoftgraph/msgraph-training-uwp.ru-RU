<!-- markdownlint-disable MD002 MD041 -->

В этом упражнении вы добавите Microsoft Graph в приложение. Для этого приложения вы будете использовать [клиентскую библиотеку Microsoft Graph для .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) , чтобы совершать вызовы в Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Получение событий календаря из Outlook

1. Добавление новой страницы для представления календаря. Щелкните правой кнопкой мыши проект **графтуториал** в обозревателе решений и выберите команду **Добавить > новый элемент..**.. Выберите **пустая страница**, `CalendarPage.xaml` введите в поле **имя** и нажмите кнопку **Добавить**.

1. Откройте `CalendarPage.xaml` и добавьте указанную ниже строку в существующий `<Grid>` элемент.

    ```xaml
    <TextBlock x:Name="Events" TextWrapping="Wrap"/>
    ```

1. Откройте `CalendarPage.xaml.cs` и добавьте приведенные `using` ниже операторы в начало файла.

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    using Microsoft.Toolkit.Uwp.UI.Controls;
    using Newtonsoft.Json;
    ```

1. Добавьте в `CalendarPage` класс следующие функции.

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
            // Get the events
            var events = await graphClient.Me.Events.Request()
                .Select("subject,organizer,start,end")
                .OrderBy("createdDateTime DESC")
                .GetAsync();

            // TEMPORARY: Show the results as JSON
            Events.Text = JsonConvert.SerializeObject(events.CurrentPage);
        }
        catch(Microsoft.Graph.ServiceException ex)
        {
            ShowNotification($"Exception getting events: {ex.Message}");
        }

        base.OnNavigatedTo(e);
    }
    ```

    Рассмотрим выполнение кода `OnNavigatedTo` .

    - URL-адрес, который будет вызываться — это `/v1.0/me/events`.
    - `Select` Функция ограничит поля, возвращаемые для каждого события, только теми, которые будут реально использоваться в представлении.
    - `OrderBy` Функция сортирует результаты по дате и времени создания, начиная с самого последнего элемента.

1. Измените `NavView_ItemInvoked` метод в `MainPage.xaml.cs` файле, чтобы заменить существующий `switch` оператор на следующий.

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SwitchStatementSnippet" highlight="4":::

Теперь можно запустить приложение, войти и щелкнуть элемент Навигация в **календаре** в меню слева. Вы должны увидеть дамп событий в календаре пользователя.

## <a name="display-the-results"></a>Отображение результатов

1. Замените все содержимое `CalendarPage.xaml` следующим.

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

1. Откройте `CalendarPage.xaml.cs` и замените `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` строку следующим.

    ```csharp
    EventList.ItemsSource = events.CurrentPage.ToList();
    ```

    Если вы запустите приложение сейчас и выбираете календарь, вам следует получить список событий в сетке данных. Тем не менее, **Начальное** и **Конечное** значения отображаются непонятным способом. Способ отображения этих значений можно контролировать с помощью [конвертера значений](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).

1. Щелкните правой кнопкой мыши проект **графтуториал** в обозревателе решений и выберите команду **Добавить класс >..**.. Назовите класс `GraphDateTimeTimeZoneConverter.cs` и нажмите кнопку **Добавить**. Замените все содержимое файла на приведенный ниже код.

    :::code language="csharp" source="../demo/GraphTutorial/GraphDateTimeTimeZoneConverter.cs" id="ConverterSnippet":::

    Этот код получает структуру [dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) , возвращенную Microsoft Graph, и анализирует ее в `DateTimeOffset` объект. Затем значение преобразуется в часовой пояс пользователя и возвращает форматированное значение.

1. Откройте `CalendarPage.xaml` и добавьте следующий `<Grid>` элемент **перед** элементом.

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="ResourcesSnippet":::

1. Замените два `DataGridTextColumn` последних элемента приведенными ниже.

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="BindingSnippet" highlight="4,9":::

1. Запустите приложение и войдите в систему, а затем щелкните элемент навигации по **календарю** . Вы должны увидеть список событий с отформатированными **начальным** и **конечным** значениями.

    ![Снимок экрана с таблицей событий](./images/add-msgraph-01.png)
