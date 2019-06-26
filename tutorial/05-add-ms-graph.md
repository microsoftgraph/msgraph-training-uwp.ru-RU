<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="afeec-101">В этом упражнении вы добавите Microsoft Graph в приложение.</span><span class="sxs-lookup"><span data-stu-id="afeec-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="afeec-102">Для этого приложения вы будете использовать клиентскую [библиотеку Microsoft Graph для .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) , чтобы совершать вызовы в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="afeec-102">For this application, you will use the [Microsoft Graph Client Library for .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="afeec-103">Получение событий календаря из Outlook</span><span class="sxs-lookup"><span data-stu-id="afeec-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="afeec-104">Для начала добавьте новую страницу для представления календаря.</span><span class="sxs-lookup"><span data-stu-id="afeec-104">Start by adding a new page for the calendar view.</span></span> <span data-ttu-id="afeec-105">Щелкните правой кнопкой мыши проект **Graph – Tutorial** в обозревателе решений и выберите команду **Добавить > новый элемент..**.. Выберите **пустая страница**, `CalendarPage.xaml` введите в поле **имя** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="afeec-105">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `CalendarPage.xaml` in the **Name** field, and select **Add**.</span></span>

<span data-ttu-id="afeec-106">Откройте `CalendarPage.xaml` и добавьте указанную ниже строку в существующий `<Grid>` элемент.</span><span class="sxs-lookup"><span data-stu-id="afeec-106">Open `CalendarPage.xaml` and add the following line inside the existing `<Grid>` element.</span></span>

```xml
<TextBlock x:Name="Events" TextWrapping="Wrap"/>
```

<span data-ttu-id="afeec-107">Откройте `CalendarPage.xaml.cs` и добавьте приведенные `using` ниже операторы в начало файла.</span><span class="sxs-lookup"><span data-stu-id="afeec-107">Open `CalendarPage.xaml.cs` and add the following `using` statements at the top of the file.</span></span>

```cs
using Microsoft.Toolkit.Services.MicrosoftGraph;
using Microsoft.Toolkit.Uwp.UI.Controls;
using Newtonsoft.Json;
```

<span data-ttu-id="afeec-108">Затем добавьте в `CalendarPage` класс следующие функции:</span><span class="sxs-lookup"><span data-stu-id="afeec-108">Then add the following functions to the `CalendarPage` class.</span></span>

```cs
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
    // Get the Graph client from the service
    var graphClient = MicrosoftGraphService.Instance.GraphProvider;

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

<span data-ttu-id="afeec-109">Рассмотрим выполнение кода `OnNavigatedTo` .</span><span class="sxs-lookup"><span data-stu-id="afeec-109">Consider with the code in `OnNavigatedTo` is doing.</span></span>

- <span data-ttu-id="afeec-110">URL-адрес, который будет вызываться — это `/v1.0/me/events`.</span><span class="sxs-lookup"><span data-stu-id="afeec-110">The URL that will be called is `/v1.0/me/events`.</span></span>
- <span data-ttu-id="afeec-111">`Select` Функция ограничит поля, возвращаемые для каждого события, только теми, которые будут реально использоваться в представлении.</span><span class="sxs-lookup"><span data-stu-id="afeec-111">The `Select` function limits the fields returned for each events to just those the view will actually use.</span></span>
- <span data-ttu-id="afeec-112">`OrderBy` Функция сортирует результаты по дате и времени создания, начиная с самого последнего элемента.</span><span class="sxs-lookup"><span data-stu-id="afeec-112">The `OrderBy` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

<span data-ttu-id="afeec-113">Прежде чем запускать приложение, чтобы перейти к этой странице календаря, измените `NavView_ItemInvoked` метод в `MainPage.xaml.cs` файле, указав следующую `throw new NotImplementedException();` строку.</span><span class="sxs-lookup"><span data-stu-id="afeec-113">Just before running the app, in order to be able to navigate to this calendar page, modify the `NavView_ItemInvoked` method in the `MainPage.xaml.cs` file to replace the `throw new NotImplementedException();` line with as follows.</span></span>

```cs
case "calendar":
    RootFrame.Navigate(typeof(CalendarPage));
    break;
```

<span data-ttu-id="afeec-114">Теперь можно запустить приложение, войти и щелкнуть элемент Навигация в календаре \*\*\*\* в меню слева.</span><span class="sxs-lookup"><span data-stu-id="afeec-114">You can now run the app, sign in, and click the **Calendar** navigation item in the left-hand menu.</span></span> <span data-ttu-id="afeec-115">Вы должны увидеть дамп событий в календаре пользователя.</span><span class="sxs-lookup"><span data-stu-id="afeec-115">You should see a JSON dump of the events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="afeec-116">Отображение результатов</span><span class="sxs-lookup"><span data-stu-id="afeec-116">Display the results</span></span>

<span data-ttu-id="afeec-117">Теперь вы можете заменить дамп JSON на какой-то способ отобразить результаты в удобном для пользователя виде.</span><span class="sxs-lookup"><span data-stu-id="afeec-117">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="afeec-118">Замените все содержимое `CalendarPage.xaml` следующим.</span><span class="sxs-lookup"><span data-stu-id="afeec-118">Replace the entire contents of `CalendarPage.xaml` with the following.</span></span>

```xml
<Page
    x:Class="graph_tutorial.CalendarPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:graph_tutorial"
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

<span data-ttu-id="afeec-119">Вместо него `TextBlock` заменяется `DataGrid`.</span><span class="sxs-lookup"><span data-stu-id="afeec-119">This replaces the `TextBlock` with a `DataGrid`.</span></span> <span data-ttu-id="afeec-120">Теперь откройте `CalendarPage.xaml.cs` и замените `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` строку приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="afeec-120">Now open `CalendarPage.xaml.cs` and replace the `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` line with the following.</span></span>

```cs
EventList.ItemsSource = events.CurrentPage.ToList();
```

<span data-ttu-id="afeec-121">Если вы запустите приложение сейчас и выбираете календарь, вам следует получить список событий в сетке данных.</span><span class="sxs-lookup"><span data-stu-id="afeec-121">If you run the app now and select the calendar, you should get a list of events in a data grid.</span></span> <span data-ttu-id="afeec-122">Тем не менее \*\*\*\* , начальное и **Конечное** значения отображаются непонятным способом.</span><span class="sxs-lookup"><span data-stu-id="afeec-122">However, the **Start** and **End** values are displayed in a non-user-friendly manner.</span></span> <span data-ttu-id="afeec-123">Способ отображения этих значений можно контролировать с помощью [конвертера значений](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span><span class="sxs-lookup"><span data-stu-id="afeec-123">You can control how those values are displayed by using a [value converter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span></span>

<span data-ttu-id="afeec-124">Щелкните правой кнопкой мыши проект **Graph – Tutorial** в обозревателе решений и выберите команду **Добавить класс >..**.. Назовите класс `GraphDateTimeTimeZoneConverter.cs` и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="afeec-124">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > Class...**. Name the class `GraphDateTimeTimeZoneConverter.cs` and select **Add**.</span></span> <span data-ttu-id="afeec-125">Замените все содержимое файла на приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="afeec-125">Replace the entire contents of the file with the following.</span></span>

```cs
using Microsoft.Graph;
using System;

namespace graph_tutorial
{
    class GraphDateTimeTimeZoneConverter : Windows.UI.Xaml.Data.IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, string language)
        {
            DateTimeTimeZone date = value as DateTimeTimeZone;

            if (date != null)
            {
                // Resolve the time zone
                var timezone = TimeZoneInfo.FindSystemTimeZoneById(date.TimeZone);
                // Parse method assumes local time, which may not be the case
                var parsedDateAsLocal = DateTimeOffset.Parse(date.DateTime);
                // Determine the offset from UTC time for the specific date
                // Making this call adjusts for DST as appropriate
                var tzOffset = timezone.GetUtcOffset(parsedDateAsLocal.DateTime);
                // Create a new DateTimeOffset with the specific offset from UTC
                var correctedDate = new DateTimeOffset(parsedDateAsLocal.DateTime, tzOffset);
                // Return the local date time string
                return correctedDate.LocalDateTime.ToString();
            }

            return string.Empty;
        }

        public object ConvertBack(object value, Type targetType, object parameter, string language)
        {
            throw new NotImplementedException();
        }
    }
}
```

<span data-ttu-id="afeec-126">Этот код получает структуру [dateTimeTimeZone](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/datetimetimezone) , возвращенную Microsoft Graph, и анализирует ее в `DateTimeOffset` объект.</span><span class="sxs-lookup"><span data-stu-id="afeec-126">This code takes the [dateTimeTimeZone](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/datetimetimezone) structure returned by Microsoft Graph and parses it into a `DateTimeOffset` object.</span></span> <span data-ttu-id="afeec-127">Затем значение преобразуется в часовой пояс пользователя и возвращает форматированное значение.</span><span class="sxs-lookup"><span data-stu-id="afeec-127">It then converts the value into the user's time zone and returns the formatted value.</span></span>

<span data-ttu-id="afeec-128">Откройте `CalendarPage.xaml` и добавьте следующий `<Grid>` элемент **перед** элементом.</span><span class="sxs-lookup"><span data-stu-id="afeec-128">Open `CalendarPage.xaml` and add the following **before** the `<Grid>` element.</span></span>

```xml
<Page.Resources>
    <local:GraphDateTimeTimeZoneConverter x:Key="DateTimeTimeZoneValueConverter" />
</Page.Resources>
```

<span data-ttu-id="afeec-129">Затем замените `Binding="{Binding Start.DateTime}"` строку на следующий.</span><span class="sxs-lookup"><span data-stu-id="afeec-129">Then, replace the `Binding="{Binding Start.DateTime}"` line with the following.</span></span>

```xml
Binding="{Binding Start, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

<span data-ttu-id="afeec-130">Замените `Binding="{Binding End.DateTime}"` строку на приведенную ниже строку.</span><span class="sxs-lookup"><span data-stu-id="afeec-130">Replace the `Binding="{Binding End.DateTime}"` line with the following.</span></span>

```xml
Binding="{Binding End, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

<span data-ttu-id="afeec-131">Запустите приложение и войдите в систему, а затем щелкните \*\*\*\* элемент навигации по календарю.</span><span class="sxs-lookup"><span data-stu-id="afeec-131">Run the app, sign in, and click the **Calendar** navigation item.</span></span> <span data-ttu-id="afeec-132">Вы должны увидеть список событий с отформатированными **начальным** и **конечным** значениями.</span><span class="sxs-lookup"><span data-stu-id="afeec-132">You should see the list of events with the **Start** and **End** values formatted.</span></span>

![Снимок экрана с таблицей событий](./images/add-msgraph-01.png)
