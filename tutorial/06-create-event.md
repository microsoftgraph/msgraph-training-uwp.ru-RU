<!-- markdownlint-disable MD002 MD041 -->

В этом разделе вы добавим возможность создания событий в календаре пользователя.

1. Добавьте новую страницу для нового представления событий. Щелкните правой кнопкой мыши проект **GraphTutorial** в обозревателе решений и **выберите "Добавить > Новый элемент...".** Выберите **пустую страницу,** `NewEventPage.xaml` введите в поле **"Имя"** и выберите **"Добавить".**

1. Откройте **NewEventPage.xaml** и замените его содержимое на следующее.

    :::code language="xaml" source="../demo/GraphTutorial/NewEventPage.xaml" id="NewEventPageXamlSnippet":::

1. Откройте **NewEventPage.xaml.cs** и добавьте следующие утверждения в `using` верхнюю часть файла.

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="UsingStatementsSnippet":::

1. Добавьте интерфейс **INotifyPropertyChange** в **класс NewEventPage.** Замените существующее объявление класса на следующее.

    ```csharp
    public sealed partial class NewEventPage : Page, INotifyPropertyChanged
    {
        public NewEventPage()
        {
            this.InitializeComponent();
            DataContext = this;
        }
    }
    ```

1. Добавьте следующие свойства в **класс NewEventPage.**

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="PropertiesSnippet":::

1. Добавьте следующий код, чтобы получить часовой пояс пользователя из Microsoft Graph при загрузке страницы.

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="LoadTimeZoneSnippet":::

1. Добавьте следующий код для создания события.

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="CreateEventSnippet":::

1. Измените `NavView_ItemInvoked` метод в файле **MainPage.xaml.cs,** чтобы заменить существующий `switch` выписку на следующий.

    ```csharp
    switch (invokedItem.ToLower())
    {
        case "new event":
            RootFrame.Navigate(typeof(NewEventPage));
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

1. Сохраните изменения и запустите приложение. Во sign in, select the **New event** menu item, fill in the form, and select **Create** to add an event to the user's calendar.

    ![Снимок экрана со страницей нового события](images/create-event-01.png)
