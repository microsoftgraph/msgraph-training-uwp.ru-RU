<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9e2ba-101">В этом разделе вы создадите новое приложение UWP.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-101">In this section you'll create a new UWP app.</span></span>

1. <span data-ttu-id="9e2ba-102">Откройте Visual Studio и выберите **создать новый проект**.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-102">Open Visual Studio, and select **Create a new project**.</span></span> <span data-ttu-id="9e2ba-103">Выберите параметр **пустое приложение (универсальные окна)** , в котором используется C#, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-103">Choose the **Blank App (Universal Windows)** option that uses C#, then select **Next**.</span></span>

    ![Visual Studio 2019 диалоговое окно создания нового проекта](./images/vs-create-new-project.png)

1. <span data-ttu-id="9e2ba-105">В диалоговом окне **Настройка нового проекта** введите `GraphTutorial` в поле **Название проекта** и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-105">In the **Configure your new project** dialog, enter `GraphTutorial` in the **Project name** field and select **Create**.</span></span>

    ![Visual Studio 2019 Настройка диалогового окна "создать проект"](./images/vs-configure-new-project.png)

    > [!IMPORTANT]
    > <span data-ttu-id="9e2ba-107">Убедитесь, что вы вводите точно такое же имя для проекта Visual Studio, которое указано в этих инструкциях лаборатории.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-107">Ensure that you enter the exact same name for the Visual Studio Project that is specified in these lab instructions.</span></span> <span data-ttu-id="9e2ba-108">Имя проекта Visual Studio становится частью пространства имен в коде.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-108">The Visual Studio Project name becomes part of the namespace in the code.</span></span> <span data-ttu-id="9e2ba-109">Код в этих инструкциях зависит от пространства имен, которое соответствует имени проекта Visual Studio, указанного в данных инструкциях.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-109">The code inside these instructions depends on the namespace matching the Visual Studio Project name specified in these instructions.</span></span> <span data-ttu-id="9e2ba-110">Если вы используете другое имя проекта, код не будет компилироваться, если не настроить все пространства имен в качестве имени проекта Visual Studio, вводимого при создании проекта.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-110">If you use a different project name the code will not compile unless you adjust all the namespaces to match the Visual Studio Project name you enter when you create the project.</span></span>

1. <span data-ttu-id="9e2ba-111">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-111">Select **OK**.</span></span> <span data-ttu-id="9e2ba-112">В диалоговом окне **новый универсальный проект платформы Windows** убедитесь, что для `Windows 10, Version 1809 (10.0; Build 17763)` **минимальной версии** задано значение, или более поздней, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-112">In the **New Universal Windows Platform Project** dialog, ensure that the **Minimum version** is set to `Windows 10, Version 1809 (10.0; Build 17763)` or later and select **OK**.</span></span>

## <a name="install-nuget-packages"></a><span data-ttu-id="9e2ba-113">Установка пакетов Nuget</span><span class="sxs-lookup"><span data-stu-id="9e2ba-113">Install NuGet packages</span></span>

<span data-ttu-id="9e2ba-114">Прежде чем переходить, установите некоторые дополнительные пакеты NuGet, которые будут использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-114">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="9e2ba-115">[Microsoft. Toolkit. UWP. UI. Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/) для добавления элементов управления пользовательского интерфейса для уведомлений в приложении и загрузки индикаторов.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-115">[Microsoft.Toolkit.Uwp.Ui.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/) to add some UI controls for in-app notifications and loading indicators.</span></span>
- <span data-ttu-id="9e2ba-116">[Microsoft. Toolkit. UWP. UI. Controls. DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) для отображения сведений, возвращенных Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-116">[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) to display the information returned by Microsoft Graph.</span></span>
- <span data-ttu-id="9e2ba-117">[Microsoft. Toolkit. Graph. Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) для обработки извлечения маркера входа и доступа.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-117">[Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) to handle login and access token retrieval.</span></span>

1. <span data-ttu-id="9e2ba-118">Выберите **инструменты > диспетчер пакетов NuGet > консоли диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-118">Select **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="9e2ba-119">В консоли диспетчера пакетов введите указанные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-119">In the Package Manager Console, enter the following commands.</span></span>

    ```powershell
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls -Version 6.0.0
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid -Version 6.0.0
    Install-Package Microsoft.Toolkit.Graph.Controls -IncludePrerelease
    ```

## <a name="design-the-app"></a><span data-ttu-id="9e2ba-120">Проектирование приложения</span><span class="sxs-lookup"><span data-stu-id="9e2ba-120">Design the app</span></span>

<span data-ttu-id="9e2ba-121">В этом разделе описывается создание пользовательского интерфейса для приложения.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-121">In this section you'll create the UI for the app.</span></span>

1. <span data-ttu-id="9e2ba-122">Для начала добавьте переменную уровня приложения для отслеживания состояния проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-122">Start by adding an application-level variable to track authentication state.</span></span> <span data-ttu-id="9e2ba-123">В обозревателе решений разверните узел **app. XAML** и откройте **app.XAML.CS**.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-123">In Solution Explorer, expand **App.xaml** and open **App.xaml.cs**.</span></span> <span data-ttu-id="9e2ba-124">Добавьте в `App` класс следующее свойство.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-124">Add the following property to the `App` class.</span></span>

    ```csharp
    public bool IsAuthenticated { get; set; }
    ```

1. <span data-ttu-id="9e2ba-125">Определите макет главной страницы.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-125">Define the layout for the main page.</span></span> <span data-ttu-id="9e2ba-126">Откройте `MainPage.xaml` и замените все содержимое приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-126">Open `MainPage.xaml` and replace its entire contents with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/MainPage.xaml" id="MainPageXamlSnippet":::

    <span data-ttu-id="9e2ba-127">Этот параметр определяет базовую [навигатионвиев](/uwp/api/windows.ui.xaml.controls.navigationview) с **домашними** и **календарными** ссылками навигации, которые действуют в качестве основного представления приложения.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-127">This defines a basic [NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview) with **Home** and **Calendar** navigation links to act as the main view of the app.</span></span> <span data-ttu-id="9e2ba-128">Кроме того, в заголовок представления добавляется элемент управления [логинбуттон](https://github.com/windows-toolkit/Graph-Controls) .</span><span class="sxs-lookup"><span data-stu-id="9e2ba-128">It also adds a [LoginButton](https://github.com/windows-toolkit/Graph-Controls) control in the header of the view.</span></span> <span data-ttu-id="9e2ba-129">Этот элемент управления позволит пользователю выполнить вход и выход. Элемент управления еще не полностью включен, его можно настроить в ходе следующего упражнения.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-129">That control will allow the user to sign in and out. The control isn't fully enabled yet, you will configure it in a later exercise.</span></span>

1. <span data-ttu-id="9e2ba-130">Щелкните правой кнопкой мыши проект **Graph – Tutorial** в обозревателе решений и выберите команду **Добавить > новый элемент..**.. Выберите **пустая страница**, `HomePage.xaml` введите в поле **имя** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-130">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `HomePage.xaml` in the **Name** field, and select **Add**.</span></span> <span data-ttu-id="9e2ba-131">Замените существующий `<Grid>` элемент в файле на следующий.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-131">Replace the existing `<Grid>` element in the file with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/HomePage.xaml" id="HomePageGridSnippet" highlight="2-5":::

1. <span data-ttu-id="9e2ba-132">Разверните узел **MainPage. XAML** в обозревателе решений и `MainPage.xaml.cs`откройте его.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-132">Expand **MainPage.xaml** in Solution Explorer and open `MainPage.xaml.cs`.</span></span> <span data-ttu-id="9e2ba-133">Добавьте указанную ниже функцию в `MainPage` класс для управления состоянием проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-133">Add the following function to the `MainPage` class to manage authentication state.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SetAuthStateSnippet":::

1. <span data-ttu-id="9e2ba-134">Добавьте следующий код в `MainPage()` конструктор **после** `this.InitializeComponent();` строки.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-134">Add the following code to the `MainPage()` constructor **after** the `this.InitializeComponent();` line.</span></span>

    ```csharp
    // Initialize auth state to false
    SetAuthState(false);

    // Configure MSAL provider
    // TEMPORARY
    MsalProvider.ClientId = "11111111-1111-1111-1111-111111111111";

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
    ```

    <span data-ttu-id="9e2ba-135">При первом запуске приложения выполняется инициализация состояния проверки подлинности на `false` домашнюю страницу и переход на нее.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-135">When the app first starts, it will initialize the authentication state to `false` and navigate to the home page.</span></span>

1. <span data-ttu-id="9e2ba-136">Добавьте следующий обработчик событий для загрузки запрашиваемой страницы, когда пользователь выбирает элемент в представлении навигации.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-136">Add the following event handler to load the requested page when the user selects an item from the navigation view.</span></span>

    ```csharp
    private void NavView_ItemInvoked(NavigationView sender, NavigationViewItemInvokedEventArgs args)
    {
        var invokedItem = args.InvokedItem as string;

        switch (invokedItem.ToLower())
        {
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

1. <span data-ttu-id="9e2ba-137">Сохраните все изменения, нажмите клавишу **F5** или выберите **Отладка > начать отладку** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e2ba-137">Save all of your changes, then press **F5** or select **Debug > Start Debugging** in Visual Studio.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9e2ba-138">Убедитесь, что выбрана соответствующая конфигурация для вашего компьютера (ARM, x64, x86).</span><span class="sxs-lookup"><span data-stu-id="9e2ba-138">Make sure you select the appropriate configuration for your machine (ARM, x64, x86).</span></span>

    ![Снимок экрана с домашней страницей](./images/create-app-01.png)
