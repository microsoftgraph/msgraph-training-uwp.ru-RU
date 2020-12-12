<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="74e51-101">В этом разделе вы создадим новое приложение UWP.</span><span class="sxs-lookup"><span data-stu-id="74e51-101">In this section you'll create a new UWP app.</span></span>

1. <span data-ttu-id="74e51-102">Откройте Visual Studio и выберите **"Создать новый проект".**</span><span class="sxs-lookup"><span data-stu-id="74e51-102">Open Visual Studio, and select **Create a new project**.</span></span> <span data-ttu-id="74e51-103">Выберите параметр **"Пустое приложение (универсальные приложения для** Windows)", использующий C#, а затем выберите **"Далее".**</span><span class="sxs-lookup"><span data-stu-id="74e51-103">Choose the **Blank App (Universal Windows)** option that uses C#, then select **Next**.</span></span>

    ![Visual Studio 2019 г. диалоговое окно создания проекта](./images/vs-create-new-project.png)

1. <span data-ttu-id="74e51-105">В **диалоговом окке** "Настройка нового проекта" введите в поле "Имя проекта" `GraphTutorial` и выберите **"Создать".** </span><span class="sxs-lookup"><span data-stu-id="74e51-105">In the **Configure your new project** dialog, enter `GraphTutorial` in the **Project name** field and select **Create**.</span></span>

    ![Visual Studio 2019 г. диалоговое окно "Настройка нового проекта"](./images/vs-configure-new-project.png)

    > [!IMPORTANT]
    > <span data-ttu-id="74e51-107">Убедитесь, что введите точно такое же имя для Visual Studio Project, которое указано в этих лабораторных инструкциях.</span><span class="sxs-lookup"><span data-stu-id="74e51-107">Ensure that you enter the exact same name for the Visual Studio Project that is specified in these lab instructions.</span></span> <span data-ttu-id="74e51-108">Имя Visual Studio проекта становится частью пространства имен в коде.</span><span class="sxs-lookup"><span data-stu-id="74e51-108">The Visual Studio Project name becomes part of the namespace in the code.</span></span> <span data-ttu-id="74e51-109">Код в этих инструкциях зависит от пространства имен, совпадающих Visual Studio имени проекта, указанного в этих инструкциях.</span><span class="sxs-lookup"><span data-stu-id="74e51-109">The code inside these instructions depends on the namespace matching the Visual Studio Project name specified in these instructions.</span></span> <span data-ttu-id="74e51-110">Если используется другое имя проекта, код не будет компилироваться, если не настроить все пространства имен в соответствие с именем Visual Studio проекта, которое вы вводите при создании проекта.</span><span class="sxs-lookup"><span data-stu-id="74e51-110">If you use a different project name the code will not compile unless you adjust all the namespaces to match the Visual Studio Project name you enter when you create the project.</span></span>

1. <span data-ttu-id="74e51-111">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="74e51-111">Select **OK**.</span></span> <span data-ttu-id="74e51-112">В **диалоговом** окте "Новый  проект универсальной платформы Windows" убедитесь, что минимальная версия установлена или более `Windows 10, Version 1809 (10.0; Build 17763)` поздней, и выберите **"ОК".**</span><span class="sxs-lookup"><span data-stu-id="74e51-112">In the **New Universal Windows Platform Project** dialog, ensure that the **Minimum version** is set to `Windows 10, Version 1809 (10.0; Build 17763)` or later and select **OK**.</span></span>

## <a name="install-nuget-packages"></a><span data-ttu-id="74e51-113">Установка пакетов Nuget</span><span class="sxs-lookup"><span data-stu-id="74e51-113">Install NuGet packages</span></span>

<span data-ttu-id="74e51-114">Прежде чем двигаться дальше, установите некоторые дополнительные пакеты NuGet, которые вы будете использовать позже.</span><span class="sxs-lookup"><span data-stu-id="74e51-114">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="74e51-115">[Microsoft.набор средств.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) для отображения информации, возвращаемой Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="74e51-115">[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) to display the information returned by Microsoft Graph.</span></span>
- <span data-ttu-id="74e51-116">[Microsoft.набор средств.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) для обработки и получения маркеров входа и доступа.</span><span class="sxs-lookup"><span data-stu-id="74e51-116">[Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) to handle login and access token retrieval.</span></span>

1. <span data-ttu-id="74e51-117">Select **Tools > NuGet диспетчер пакетов > диспетчер пакетов Console**.</span><span class="sxs-lookup"><span data-stu-id="74e51-117">Select **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="74e51-118">В консоли диспетчер пакетов введите следующие команды.</span><span class="sxs-lookup"><span data-stu-id="74e51-118">In the Package Manager Console, enter the following commands.</span></span>

    ```powershell
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid -IncludePrerelease
    Install-Package Microsoft.Toolkit.Graph.Controls -IncludePrerelease
    ```

## <a name="design-the-app"></a><span data-ttu-id="74e51-119">Проектирование приложения</span><span class="sxs-lookup"><span data-stu-id="74e51-119">Design the app</span></span>

<span data-ttu-id="74e51-120">В этом разделе вы создадим пользовательский интерфейс для приложения.</span><span class="sxs-lookup"><span data-stu-id="74e51-120">In this section you'll create the UI for the app.</span></span>

1. <span data-ttu-id="74e51-121">Для начала добавьте переменную уровня приложения для отслеживания состояния проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="74e51-121">Start by adding an application-level variable to track authentication state.</span></span> <span data-ttu-id="74e51-122">В обозревателе решений **разкрой app.xaml** и откройте **App.xaml.cs.**</span><span class="sxs-lookup"><span data-stu-id="74e51-122">In Solution Explorer, expand **App.xaml** and open **App.xaml.cs**.</span></span> <span data-ttu-id="74e51-123">Добавьте в класс следующее `App` свойство.</span><span class="sxs-lookup"><span data-stu-id="74e51-123">Add the following property to the `App` class.</span></span>

    ```csharp
    public bool IsAuthenticated { get; set; }
    ```

1. <span data-ttu-id="74e51-124">Определите макет главной страницы.</span><span class="sxs-lookup"><span data-stu-id="74e51-124">Define the layout for the main page.</span></span> <span data-ttu-id="74e51-125">Откройте `MainPage.xaml` и замените все его содержимое на следующее.</span><span class="sxs-lookup"><span data-stu-id="74e51-125">Open `MainPage.xaml` and replace its entire contents with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/MainPage.xaml" id="MainPageXamlSnippet":::

    <span data-ttu-id="74e51-126">Это определяет базовый [NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview) с навигационными ссылками **"Главная",**"Календарь" и "Новое событие", которые будут выступать в качестве основного представления приложения.  </span><span class="sxs-lookup"><span data-stu-id="74e51-126">This defines a basic [NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview) with **Home**, **Calendar**, and **New event** navigation links to act as the main view of the app.</span></span> <span data-ttu-id="74e51-127">Он также добавляет в загон представления контроль [LoginButton.](https://github.com/windows-toolkit/Graph-Controls)</span><span class="sxs-lookup"><span data-stu-id="74e51-127">It also adds a [LoginButton](https://github.com/windows-toolkit/Graph-Controls) control in the header of the view.</span></span> <span data-ttu-id="74e51-128">Этот контроль позволит пользователю войти и выйти. The control isn't fully enabled yet, you will configure it in a later exercise.</span><span class="sxs-lookup"><span data-stu-id="74e51-128">That control will allow the user to sign in and out. The control isn't fully enabled yet, you will configure it in a later exercise.</span></span>

1. <span data-ttu-id="74e51-129">Щелкните правой кнопкой мыши проект **учебника** по графику в обозревателе решений **и выберите "Добавить > Новый элемент...".** Выберите **пустую страницу,** `HomePage.xaml` введите в поле **"Имя"** и выберите **"Добавить".**</span><span class="sxs-lookup"><span data-stu-id="74e51-129">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `HomePage.xaml` in the **Name** field, and select **Add**.</span></span> <span data-ttu-id="74e51-130">Замените `<Grid>` существующий элемент в файле следующим:</span><span class="sxs-lookup"><span data-stu-id="74e51-130">Replace the existing `<Grid>` element in the file with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/HomePage.xaml" id="HomePageGridSnippet" highlight="2-5":::

1. <span data-ttu-id="74e51-131">**Разкрой mainPage.xaml** в обозревателе решений и `MainPage.xaml.cs` откройте.</span><span class="sxs-lookup"><span data-stu-id="74e51-131">Expand **MainPage.xaml** in Solution Explorer and open `MainPage.xaml.cs`.</span></span> <span data-ttu-id="74e51-132">Добавьте в класс следующую `MainPage` функцию для управления состоянием проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="74e51-132">Add the following function to the `MainPage` class to manage authentication state.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SetAuthStateSnippet":::

1. <span data-ttu-id="74e51-133">Добавьте следующий код в `MainPage()` конструктор **после** `this.InitializeComponent();` строки.</span><span class="sxs-lookup"><span data-stu-id="74e51-133">Add the following code to the `MainPage()` constructor **after** the `this.InitializeComponent();` line.</span></span>

    ```csharp
    // Initialize auth state to false
    SetAuthState(false);

    // Configure MSAL provider
    // TEMPORARY
    MsalProvider.ClientId = "11111111-1111-1111-1111-111111111111";

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
    ```

    <span data-ttu-id="74e51-134">При первом начале приложения оно инициализирует состояние проверки подлинности и `false` переходит на начальную страницу.</span><span class="sxs-lookup"><span data-stu-id="74e51-134">When the app first starts, it will initialize the authentication state to `false` and navigate to the home page.</span></span>

1. <span data-ttu-id="74e51-135">Добавьте следующий обработчик событий, чтобы загрузить запрашиваемую страницу, когда пользователь выбирает элемент в представлении навигации.</span><span class="sxs-lookup"><span data-stu-id="74e51-135">Add the following event handler to load the requested page when the user selects an item from the navigation view.</span></span>

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

1. <span data-ttu-id="74e51-136">Сохраните все изменения, нажмите **F5** или выберите "Отладка> **начать** отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74e51-136">Save all of your changes, then press **F5** or select **Debug > Start Debugging** in Visual Studio.</span></span>

    > [!NOTE]
    > <span data-ttu-id="74e51-137">Убедитесь, что выбрана соответствующая конфигурация компьютера (ARM, x64, x86).</span><span class="sxs-lookup"><span data-stu-id="74e51-137">Make sure you select the appropriate configuration for your machine (ARM, x64, x86).</span></span>

    ![Снимок экрана с домашней страницей](./images/create-app-01.png)
