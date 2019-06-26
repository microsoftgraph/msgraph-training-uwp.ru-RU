<!-- markdownlint-disable MD002 MD041 -->

В этом упражнении вы добавите Microsoft Graph в приложение. Для этого приложения вы будете использовать клиентскую [библиотеку Microsoft Graph для .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) , чтобы совершать вызовы в Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Получение событий календаря из Outlook

Для начала добавьте новую страницу для представления календаря. Щелкните правой кнопкой мыши проект **Graph – Tutorial** в обозревателе решений и выберите команду **Добавить > новый элемент..**.. Выберите **пустая страница**, `CalendarPage.xaml` введите в поле **имя** и нажмите кнопку **Добавить**.

Откройте `CalendarPage.xaml` и добавьте указанную ниже строку в существующий `<Grid>` элемент.

```xml
<TextBlock x:Name="Events" TextWrapping="Wrap"/>
```

Откройте `CalendarPage.xaml.cs` и добавьте приведенные `using` ниже операторы в начало файла.

```cs
using Microsoft.Toolkit.Services.MicrosoftGraph;
using Microsoft.Toolkit.Uwp.UI.Controls;
using Newtonsoft.Json;
```

Затем добавьте в `CalendarPage` класс следующие функции:

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

Рассмотрим выполнение кода `OnNavigatedTo` .

- URL-адрес, который будет вызываться — это `/v1.0/me/events`.
- `Select` Функция ограничит поля, возвращаемые для каждого события, только теми, которые будут реально использоваться в представлении.
- `OrderBy` Функция сортирует результаты по дате и времени создания, начиная с самого последнего элемента.

Прежде чем запускать приложение, чтобы перейти к этой странице календаря, измените `NavView_ItemInvoked` метод в `MainPage.xaml.cs` файле, указав следующую `throw new NotImplementedException();` строку.

```cs
case "calendar":
    RootFrame.Navigate(typeof(CalendarPage));
    break;
```

Теперь можно запустить приложение, войти и щелкнуть элемент Навигация в календаре **** в меню слева. Вы должны увидеть дамп событий в календаре пользователя.

## <a name="display-the-results"></a>Отображение результатов

Теперь вы можете заменить дамп JSON на какой-то способ отобразить результаты в удобном для пользователя виде. Замените все содержимое `CalendarPage.xaml` следующим.

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

Вместо него `TextBlock` заменяется `DataGrid`. Теперь откройте `CalendarPage.xaml.cs` и замените `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` строку приведенным ниже.

```cs
EventList.ItemsSource = events.CurrentPage.ToList();
```

Если вы запустите приложение сейчас и выбираете календарь, вам следует получить список событий в сетке данных. Тем не менее **** , начальное и **Конечное** значения отображаются непонятным способом. Способ отображения этих значений можно контролировать с помощью [конвертера значений](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).

Щелкните правой кнопкой мыши проект **Graph – Tutorial** в обозревателе решений и выберите команду **Добавить класс >..**.. Назовите класс `GraphDateTimeTimeZoneConverter.cs` и нажмите кнопку **Добавить**. Замените все содержимое файла на приведенный ниже код.

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

Этот код получает структуру [dateTimeTimeZone](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/datetimetimezone) , возвращенную Microsoft Graph, и анализирует ее в `DateTimeOffset` объект. Затем значение преобразуется в часовой пояс пользователя и возвращает форматированное значение.

Откройте `CalendarPage.xaml` и добавьте следующий `<Grid>` элемент **перед** элементом.

```xml
<Page.Resources>
    <local:GraphDateTimeTimeZoneConverter x:Key="DateTimeTimeZoneValueConverter" />
</Page.Resources>
```

Затем замените `Binding="{Binding Start.DateTime}"` строку на следующий.

```xml
Binding="{Binding Start, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

Замените `Binding="{Binding End.DateTime}"` строку на приведенную ниже строку.

```xml
Binding="{Binding End, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

Запустите приложение и войдите в систему, а затем щелкните **** элемент навигации по календарю. Вы должны увидеть список событий с отформатированными **начальным** и **конечным** значениями.

![Снимок экрана с таблицей событий](./images/add-msgraph-01.png)
