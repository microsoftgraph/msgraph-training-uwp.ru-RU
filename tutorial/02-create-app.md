<!-- markdownlint-disable MD002 MD041 -->

В этом разделе вы создадим новое приложение UWP.

1. Откройте Visual Studio и выберите **"Создать новый проект".** Выберите параметр **"Пустое приложение (универсальные приложения для** Windows)", использующий C#, а затем выберите **"Далее".**

    ![Visual Studio 2019 г. диалоговое окно создания проекта](./images/vs-create-new-project.png)

1. В **диалоговом окке** "Настройка нового проекта" введите в поле "Имя проекта" `GraphTutorial` и выберите **"Создать".** 

    ![Visual Studio 2019 г. диалоговое окно "Настройка нового проекта"](./images/vs-configure-new-project.png)

    > [!IMPORTANT]
    > Убедитесь, что введите точно такое же имя для Visual Studio Project, которое указано в этих лабораторных инструкциях. Имя Visual Studio проекта становится частью пространства имен в коде. Код в этих инструкциях зависит от пространства имен, совпадающих Visual Studio имени проекта, указанного в этих инструкциях. Если используется другое имя проекта, код не будет компилироваться, если не настроить все пространства имен в соответствие с именем Visual Studio проекта, которое вы вводите при создании проекта.

1. Нажмите кнопку **ОК**. В **диалоговом** окте "Новый  проект универсальной платформы Windows" убедитесь, что минимальная версия установлена или более `Windows 10, Version 1809 (10.0; Build 17763)` поздней, и выберите **"ОК".**

## <a name="install-nuget-packages"></a>Установка пакетов Nuget

Прежде чем двигаться дальше, установите некоторые дополнительные пакеты NuGet, которые вы будете использовать позже.

- [Microsoft.набор средств.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) для отображения информации, возвращаемой Microsoft Graph.
- [Microsoft.набор средств.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) для обработки и получения маркеров входа и доступа.

1. Select **Tools > NuGet диспетчер пакетов > диспетчер пакетов Console**. В консоли диспетчер пакетов введите следующие команды.

    ```powershell
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid -IncludePrerelease
    Install-Package Microsoft.Toolkit.Graph.Controls -IncludePrerelease
    ```

## <a name="design-the-app"></a>Проектирование приложения

В этом разделе вы создадим пользовательский интерфейс для приложения.

1. Для начала добавьте переменную уровня приложения для отслеживания состояния проверки подлинности. В обозревателе решений **разкрой app.xaml** и откройте **App.xaml.cs.** Добавьте в класс следующее `App` свойство.

    ```csharp
    public bool IsAuthenticated { get; set; }
    ```

1. Определите макет главной страницы. Откройте `MainPage.xaml` и замените все его содержимое на следующее.

    :::code language="xaml" source="../demo/GraphTutorial/MainPage.xaml" id="MainPageXamlSnippet":::

    Это определяет базовый [NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview) с навигационными ссылками **"Главная",**"Календарь" и "Новое событие", которые будут выступать в качестве основного представления приложения.   Он также добавляет в загон представления контроль [LoginButton.](https://github.com/windows-toolkit/Graph-Controls) Этот контроль позволит пользователю войти и выйти. The control isn't fully enabled yet, you will configure it in a later exercise.

1. Щелкните правой кнопкой мыши проект **учебника** по графику в обозревателе решений **и выберите "Добавить > Новый элемент...".** Выберите **пустую страницу,** `HomePage.xaml` введите в поле **"Имя"** и выберите **"Добавить".** Замените `<Grid>` существующий элемент в файле следующим:

    :::code language="xaml" source="../demo/GraphTutorial/HomePage.xaml" id="HomePageGridSnippet" highlight="2-5":::

1. **Разкрой mainPage.xaml** в обозревателе решений и `MainPage.xaml.cs` откройте. Добавьте в класс следующую `MainPage` функцию для управления состоянием проверки подлинности.

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SetAuthStateSnippet":::

1. Добавьте следующий код в `MainPage()` конструктор **после** `this.InitializeComponent();` строки.

    ```csharp
    // Initialize auth state to false
    SetAuthState(false);

    // Configure MSAL provider
    // TEMPORARY
    MsalProvider.ClientId = "11111111-1111-1111-1111-111111111111";

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
    ```

    При первом начале приложения оно инициализирует состояние проверки подлинности и `false` переходит на начальную страницу.

1. Добавьте следующий обработчик событий, чтобы загрузить запрашиваемую страницу, когда пользователь выбирает элемент в представлении навигации.

    ```csharp
    private void NavView_ItemInvoked(NavigationView sender, NavigationViewItemInvokedEventArgs args)
    {
        var invokedItem = args.InvokedItem as string;

        switch (invokedItem.ToLower())
        {
            case "new event":
                throw new NotImplementedException();
                break;
            case "calendar":
                throw new NotImplementedException();
                break;
            case "home":
            default:
                RootFrame.Navigate(typeof(HomePage));
                break;
        }
    }
    ```

1. Сохраните все изменения, нажмите **F5** или выберите "Отладка> **начать** отладку в Visual Studio.

    > [!NOTE]
    > Убедитесь, что выбрана соответствующая конфигурация компьютера (ARM, x64, x86).

    ![Снимок экрана с домашней страницей](./images/create-app-01.png)
