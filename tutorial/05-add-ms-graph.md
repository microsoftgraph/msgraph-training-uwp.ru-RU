<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="66720-101">В этом упражнении вы включаете Microsoft Graph в приложение.</span><span class="sxs-lookup"><span data-stu-id="66720-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="66720-102">Для этого приложения вы будете использовать клиентскую библиотеку Microsoft Graph для [.NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) для вызова Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="66720-102">For this application, you will use the [Microsoft Graph Client Library for .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="66720-103">Получить события календаря из Outlook</span><span class="sxs-lookup"><span data-stu-id="66720-103">Get calendar events from Outlook</span></span>

1. <span data-ttu-id="66720-104">Добавьте новую страницу для представления календаря.</span><span class="sxs-lookup"><span data-stu-id="66720-104">Add a new page for the calendar view.</span></span> <span data-ttu-id="66720-105">Щелкните правой кнопкой мыши проект **GraphTutorial** в обозревателе решений и **выберите "Добавить > новый элемент...".** Выберите **пустую страницу,** `CalendarPage.xaml` введите в поле **"Имя"** и выберите **"Добавить".**</span><span class="sxs-lookup"><span data-stu-id="66720-105">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `CalendarPage.xaml` in the **Name** field, and select **Add**.</span></span>

1. <span data-ttu-id="66720-106">Откройте `CalendarPage.xaml` и добавьте следующую строку в существующий `<Grid>` элемент.</span><span class="sxs-lookup"><span data-stu-id="66720-106">Open `CalendarPage.xaml` and add the following line inside the existing `<Grid>` element.</span></span>

    ```xaml
    <TextBlock x:Name="Events" TextWrapping="Wrap"/>
    ```

1. <span data-ttu-id="66720-107">Откройте `CalendarPage.xaml.cs` и добавьте следующие утверждения в `using` верхней части файла.</span><span class="sxs-lookup"><span data-stu-id="66720-107">Open `CalendarPage.xaml.cs` and add the following `using` statements at the top of the file.</span></span>

    ```csharp
    using Microsoft.Graph;
    using Microsoft.Toolkit.Graph.Providers;
    using Microsoft.Toolkit.Uwp.UI.Controls;
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="66720-108">Добавьте в класс следующие `CalendarPage` функции.</span><span class="sxs-lookup"><span data-stu-id="66720-108">Add the following functions to the `CalendarPage` class.</span></span>

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

    <span data-ttu-id="66720-109">Рассмотрим, что делает `OnNavigatedTo` код.</span><span class="sxs-lookup"><span data-stu-id="66720-109">Consider with the code in `OnNavigatedTo` is doing.</span></span>

    - <span data-ttu-id="66720-110">Будет вызван URL-адрес `/me/calendarview` .</span><span class="sxs-lookup"><span data-stu-id="66720-110">The URL that will be called is `/me/calendarview`.</span></span>
        - <span data-ttu-id="66720-111">Параметры `startDateTime` `endDateTime` и параметров определяют начало и конец представления календаря.</span><span class="sxs-lookup"><span data-stu-id="66720-111">The `startDateTime` and `endDateTime` parameters define the start and end of the calendar view.</span></span>
        - <span data-ttu-id="66720-112">Заглавная часть приводит к возвращению событий в часовом поясе `Prefer: outlook.timezone` `start` `end` пользователя.</span><span class="sxs-lookup"><span data-stu-id="66720-112">The `Prefer: outlook.timezone` header causes the `start` and `end` of the events to be returned in the user's time zone.</span></span>
        - <span data-ttu-id="66720-113">Функция `Select` ограничивает поля, возвращаемые для каждого события, только теми, которые будут фактически использовать приложение.</span><span class="sxs-lookup"><span data-stu-id="66720-113">The `Select` function limits the fields returned for each event to just those the app will actually use.</span></span>
        - <span data-ttu-id="66720-114">Функция `OrderBy` сортировать результаты по дате и времени начала.</span><span class="sxs-lookup"><span data-stu-id="66720-114">The `OrderBy` function sorts the results by the start date and time.</span></span>
        - <span data-ttu-id="66720-115">Функция `Top` запрашивает не более 50 событий.</span><span class="sxs-lookup"><span data-stu-id="66720-115">The `Top` function requests at most 50 events.</span></span>

1. <span data-ttu-id="66720-116">Измените `NavView_ItemInvoked` метод в `MainPage.xaml.cs` файле, чтобы заменить существующий `switch` параметр на следующий.</span><span class="sxs-lookup"><span data-stu-id="66720-116">Modify the `NavView_ItemInvoked` method in the `MainPage.xaml.cs` file to replace the existing `switch` statement with the following.</span></span>

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

<span data-ttu-id="66720-117">Теперь вы можете запустить приложение, войти  в систему и щелкнуть элемент навигации "Календарь" в левом меню.</span><span class="sxs-lookup"><span data-stu-id="66720-117">You can now run the app, sign in, and click the **Calendar** navigation item in the left-hand menu.</span></span> <span data-ttu-id="66720-118">Вы увидите дамп событий в JSON в календаре пользователя.</span><span class="sxs-lookup"><span data-stu-id="66720-118">You should see a JSON dump of the events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="66720-119">Отображение результатов</span><span class="sxs-lookup"><span data-stu-id="66720-119">Display the results</span></span>

1. <span data-ttu-id="66720-120">Замените все содержимое на `CalendarPage.xaml` следующее:</span><span class="sxs-lookup"><span data-stu-id="66720-120">Replace the entire contents of `CalendarPage.xaml` with the following.</span></span>

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

1. <span data-ttu-id="66720-121">Откройте `CalendarPage.xaml.cs` и замените `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` строку на следующую.</span><span class="sxs-lookup"><span data-stu-id="66720-121">Open `CalendarPage.xaml.cs` and replace the `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` line with the following.</span></span>

    ```csharp
    EventList.ItemsSource = events.CurrentPage.ToList();
    ```

    <span data-ttu-id="66720-122">Если запустить приложение сейчас и выбрать календарь, вы получите список событий в сетке данных.</span><span class="sxs-lookup"><span data-stu-id="66720-122">If you run the app now and select the calendar, you should get a list of events in a data grid.</span></span> <span data-ttu-id="66720-123">Однако значения **start** и **End** отображаются не для пользователей.</span><span class="sxs-lookup"><span data-stu-id="66720-123">However, the **Start** and **End** values are displayed in a non-user-friendly manner.</span></span> <span data-ttu-id="66720-124">Вы можете управлять отображением этих значений с помощью [преобразоващика значений.](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter)</span><span class="sxs-lookup"><span data-stu-id="66720-124">You can control how those values are displayed by using a [value converter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span></span>

1. <span data-ttu-id="66720-125">Щелкните правой кнопкой мыши проект **GraphTutorial** в обозревателе решений и **выберите add > Class...**. Назовем класс `GraphDateTimeTimeZoneConverter.cs` и выберите **"Добавить".**</span><span class="sxs-lookup"><span data-stu-id="66720-125">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > Class...**. Name the class `GraphDateTimeTimeZoneConverter.cs` and select **Add**.</span></span> <span data-ttu-id="66720-126">Замените все содержимое файла на следующее:</span><span class="sxs-lookup"><span data-stu-id="66720-126">Replace the entire contents of the file with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/GraphDateTimeTimeZoneConverter.cs" id="ConverterSnippet":::

    <span data-ttu-id="66720-127">Этот код принимает [структуру dateTimeTimeZone,](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) возвращаемую Microsoft Graph, и разбирает ее в `DateTimeOffset` объект.</span><span class="sxs-lookup"><span data-stu-id="66720-127">This code takes the [dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) structure returned by Microsoft Graph and parses it into a `DateTimeOffset` object.</span></span> <span data-ttu-id="66720-128">Затем он преобразует значение в часовой пояс пользователя и возвращает отформатированные значения.</span><span class="sxs-lookup"><span data-stu-id="66720-128">It then converts the value into the user's time zone and returns the formatted value.</span></span>

1. <span data-ttu-id="66720-129">Откройте `CalendarPage.xaml` и добавьте следующее **перед** `<Grid>` элементом.</span><span class="sxs-lookup"><span data-stu-id="66720-129">Open `CalendarPage.xaml` and add the following **before** the `<Grid>` element.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="ResourcesSnippet":::

1. <span data-ttu-id="66720-130">Замените два `DataGridTextColumn` последних элемента на следующие.</span><span class="sxs-lookup"><span data-stu-id="66720-130">Replace the last two `DataGridTextColumn` elements with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="BindingSnippet" highlight="4,9":::

1. <span data-ttu-id="66720-131">Запустите приложение, войдите в систему и щелкните элемент **навигации календаря.**</span><span class="sxs-lookup"><span data-stu-id="66720-131">Run the app, sign in, and click the **Calendar** navigation item.</span></span> <span data-ttu-id="66720-132">Должен отформатирован список событий со значениями **start** и **End.**</span><span class="sxs-lookup"><span data-stu-id="66720-132">You should see the list of events with the **Start** and **End** values formatted.</span></span>

    ![Снимок экрана с таблицей событий](./images/add-msgraph-01.png)
