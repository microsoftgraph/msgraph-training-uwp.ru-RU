<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="95a20-101">Откройте Visual Studio и выберите **создать новый проект**.</span><span class="sxs-lookup"><span data-stu-id="95a20-101">Open Visual Studio, and select **Create a new project**.</span></span> <span data-ttu-id="95a20-102">Выберите параметр **пустое приложение (универсальные окна)** , в котором используется C#, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="95a20-102">Choose the **Blank App (Universal Windows)** option that uses C#, then select **Next**.</span></span>

![Visual Studio 2019 диалоговое окно создания нового проекта](./images/vs-create-new-project.png)

<span data-ttu-id="95a20-104">В диалоговом окне **Настройка нового проекта** введите `graph-tutorial` в поле **Название проекта** и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="95a20-104">In the **Configure your new project** dialog, enter `graph-tutorial` in the **Project name** field and select **Create**.</span></span>

![Visual Studio 2019 Настройка диалогового окна "создать проект"](./images/vs-configure-new-project.png)

> [!IMPORTANT]
> <span data-ttu-id="95a20-106">Убедитесь, что вы вводите точно такое же имя для проекта Visual Studio, которое указано в этих инструкциях лаборатории.</span><span class="sxs-lookup"><span data-stu-id="95a20-106">Ensure that you enter the exact same name for the Visual Studio Project that is specified in these lab instructions.</span></span> <span data-ttu-id="95a20-107">Имя проекта Visual Studio становится частью пространства имен в коде.</span><span class="sxs-lookup"><span data-stu-id="95a20-107">The Visual Studio Project name becomes part of the namespace in the code.</span></span> <span data-ttu-id="95a20-108">Код в этих инструкциях зависит от пространства имен, которое соответствует имени проекта Visual Studio, указанного в данных инструкциях.</span><span class="sxs-lookup"><span data-stu-id="95a20-108">The code inside these instructions depends on the namespace matching the Visual Studio Project name specified in these instructions.</span></span> <span data-ttu-id="95a20-109">Если вы используете другое имя проекта, код не будет компилироваться, если не настроить все пространства имен в качестве имени проекта Visual Studio, вводимого при создании проекта.</span><span class="sxs-lookup"><span data-stu-id="95a20-109">If you use a different project name the code will not compile unless you adjust all the namespaces to match the Visual Studio Project name you enter when you create the project.</span></span>

<span data-ttu-id="95a20-110">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="95a20-110">Select **OK**.</span></span> <span data-ttu-id="95a20-111">В диалоговом окне **новый универсальный проект платформы Windows** убедитесь, что для `Windows 10 Fall Creators Update (10.0; Build 16299)` **минимальной версии** задано значение, или более поздней, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="95a20-111">In the **New Universal Windows Platform Project** dialog, ensure that the **Minimum version** is set to `Windows 10 Fall Creators Update (10.0; Build 16299)` or later and select **OK**.</span></span>

<span data-ttu-id="95a20-112">Прежде чем переходить, установите некоторые дополнительные пакеты NuGet, которые будут использоваться позже.</span><span class="sxs-lookup"><span data-stu-id="95a20-112">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="95a20-113">[Microsoft. Toolkit. UWP. UI. Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/) для добавления элементов управления пользовательского интерфейса для уведомлений в приложении и загрузки индикаторов.</span><span class="sxs-lookup"><span data-stu-id="95a20-113">[Microsoft.Toolkit.Uwp.Ui.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/) to add some UI controls for in-app notifications and loading indicators.</span></span>
- <span data-ttu-id="95a20-114">[Microsoft. Toolkit. UWP. UI. Controls. DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) для отображения сведений, возвращенных Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="95a20-114">[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) to display the information returned by Microsoft Graph.</span></span>
- <span data-ttu-id="95a20-115">[Microsoft. Toolkit. UWP. UI. Controls. Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.Graph/) для обработки извлечения маркера входа и доступа.</span><span class="sxs-lookup"><span data-stu-id="95a20-115">[Microsoft.Toolkit.Uwp.Ui.Controls.Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.Graph/) to handle login and access token retrieval.</span></span>
- <span data-ttu-id="95a20-116">[Microsoft. Graph](https://www.nuget.org/packages/Microsoft.Graph/) для совершения вызовов в Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="95a20-116">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) for making calls to the Microsoft Graph.</span></span>

<span data-ttu-id="95a20-117">Выберите **инструменты > диспетчер пакетов NuGet > консоли диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="95a20-117">Select **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="95a20-118">В консоли диспетчера пакетов введите указанные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="95a20-118">In the Package Manager Console, enter the following commands.</span></span>

```Powershell
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls -Version 6.0.0
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid -Version 6.0.0
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.Graph -Version 6.0.0
Install-Package Microsoft.Graph -Version 1.20.0
```

## <a name="design-the-app"></a><span data-ttu-id="95a20-119">Проектирование приложения</span><span class="sxs-lookup"><span data-stu-id="95a20-119">Design the app</span></span>

<span data-ttu-id="95a20-120">Для начала добавьте переменную уровня приложения для отслеживания состояния проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="95a20-120">Start by adding an application-level variable to track authentication state.</span></span> <span data-ttu-id="95a20-121">В обозревателе решений разверните узел **app. XAML** и откройте **app.XAML.CS**.</span><span class="sxs-lookup"><span data-stu-id="95a20-121">In Solution Explorer, expand **App.xaml** and open **App.xaml.cs**.</span></span> <span data-ttu-id="95a20-122">Добавьте в `App` класс следующее свойство.</span><span class="sxs-lookup"><span data-stu-id="95a20-122">Add the following property to the `App` class.</span></span>

```cs
public bool IsAuthenticated { get; set; }
```

<span data-ttu-id="95a20-123">Затем определите макет главной страницы.</span><span class="sxs-lookup"><span data-stu-id="95a20-123">Next, define the layout for the main page.</span></span> <span data-ttu-id="95a20-124">Откройте `MainPage.xaml` и замените все содержимое приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="95a20-124">Open `MainPage.xaml` and replace its entire contents with the following.</span></span>

```xml
<Page
    x:Class="graph_tutorial.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:graph_tutorial"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    xmlns:graphControls="using:Microsoft.Toolkit.Uwp.UI.Controls.Graph"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <NavigationView x:Name="NavView"
            IsSettingsVisible="False"
            ItemInvoked="NavView_ItemInvoked">

            <NavigationView.Header>
                <graphControls:AadLogin x:Name="Login"
                    HorizontalAlignment="Left"
                    View="SmallProfilePhotoLeft"
                    AllowSignInAsDifferentUser="False"
                    />
            </NavigationView.Header>

            <NavigationView.MenuItems>
                <NavigationViewItem Content="Home" x:Name="Home" Tag="home">
                    <NavigationViewItem.Icon>
                        <FontIcon Glyph="&#xE10F;"/>
                    </NavigationViewItem.Icon>
                </NavigationViewItem>
                <NavigationViewItem Content="Calendar" x:Name="Calendar" Tag="calendar">
                    <NavigationViewItem.Icon>
                        <FontIcon Glyph="&#xE163;"/>
                    </NavigationViewItem.Icon>
                </NavigationViewItem>
            </NavigationView.MenuItems>

            <StackPanel>
                <controls:InAppNotification x:Name="Notification" ShowDismissButton="true" />
                <Frame x:Name="RootFrame" Margin="24, 0" />
            </StackPanel>
        </NavigationView>
    </Grid>
</Page>
```

<span data-ttu-id="95a20-125">Этот параметр определяет базовую [навигатионвиев](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview) с **домашними** и **календарными** ссылками навигации, которые действуют в качестве основного представления приложения.</span><span class="sxs-lookup"><span data-stu-id="95a20-125">This defines a basic [NavigationView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview) with **Home** and **Calendar** navigation links to act as the main view of the app.</span></span> <span data-ttu-id="95a20-126">Кроме того, в заголовке представления добавляется элемент управления [аадлогин](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable) .</span><span class="sxs-lookup"><span data-stu-id="95a20-126">It also adds an [AadLogin](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable) control in the header of the view.</span></span> <span data-ttu-id="95a20-127">Этот элемент управления позволит пользователю выполнить вход и выход. Элемент управления еще не полностью включен, его можно настроить в ходе следующего упражнения.</span><span class="sxs-lookup"><span data-stu-id="95a20-127">That control will allow the user to sign in and out. The control isn't fully enabled yet, you will configure it in a later exercise.</span></span>

<span data-ttu-id="95a20-128">Теперь добавьте еще одну страницу XAML для представления "Домашняя страница".</span><span class="sxs-lookup"><span data-stu-id="95a20-128">Now add another XAML page for the Home view.</span></span> <span data-ttu-id="95a20-129">Щелкните правой кнопкой мыши проект **Graph – Tutorial** в обозревателе решений и выберите команду **Добавить > новый элемент..**.. Выберите **пустая страница**, `HomePage.xaml` введите в поле **имя** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="95a20-129">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `HomePage.xaml` in the **Name** field, and select **Add**.</span></span> <span data-ttu-id="95a20-130">Добавьте следующий код внутри `<Grid>` элемента в файле.</span><span class="sxs-lookup"><span data-stu-id="95a20-130">Add the following code inside the `<Grid>` element in the file.</span></span>

```xml
<StackPanel>
    <TextBlock FontSize="44" FontWeight="Bold" Margin="0, 12">Microsoft Graph UWP Tutorial</TextBlock>
    <TextBlock x:Name="HomePageMessage">Please sign in to continue.</TextBlock>
</StackPanel>
```

<span data-ttu-id="95a20-131">Теперь разверните **MainPage. XAML** в обозревателе решений и откройте `MainPage.xaml.cs`его.</span><span class="sxs-lookup"><span data-stu-id="95a20-131">Now expand **MainPage.xaml** in Solution Explorer and open `MainPage.xaml.cs`.</span></span> <span data-ttu-id="95a20-132">Добавьте указанную ниже функцию в `MainPage` класс для управления состоянием проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="95a20-132">Add the following function to the `MainPage` class to manage authentication state.</span></span>

```cs
private void SetAuthState(bool isAuthenticated)
{
    (App.Current as App).IsAuthenticated = isAuthenticated;

    // Toggle controls that require auth
    Calendar.IsEnabled = isAuthenticated;
}
```

<span data-ttu-id="95a20-133">Добавьте следующий код в `MainPage()` конструктор **после** `this.InitializeComponent();` строки.</span><span class="sxs-lookup"><span data-stu-id="95a20-133">Add the following code to the `MainPage()` constructor **after** the `this.InitializeComponent();` line.</span></span>

```cs
// Initialize auth state to false
SetAuthState(false);

// Navigate to HomePage.xaml
RootFrame.Navigate(typeof(HomePage));
```

<span data-ttu-id="95a20-134">При первом запуске приложения выполняется инициализация состояния проверки подлинности на `false` домашнюю страницу и переход на нее.</span><span class="sxs-lookup"><span data-stu-id="95a20-134">When the app first starts, it will initialize the authentication state to `false` and navigate to the home page.</span></span>

<span data-ttu-id="95a20-135">Добавьте следующий обработчик событий для загрузки запрашиваемой страницы, когда пользователь выбирает элемент в представлении навигации.</span><span class="sxs-lookup"><span data-stu-id="95a20-135">Add the following event handler to load the requested page when the user selects an item from the navigation view.</span></span>

```cs
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

<span data-ttu-id="95a20-136">Сохраните все изменения, нажмите клавишу **F5** или выберите **Отладка > начать отладку** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95a20-136">Save all of your changes, then press **F5** or select **Debug > Start Debugging** in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="95a20-137">Убедитесь, что выбрана соответствующая конфигурация для вашего компьютера (ARM, x64, x86).</span><span class="sxs-lookup"><span data-stu-id="95a20-137">Make sure you select the appropriate configuration for your machine (ARM, x64, x86).</span></span>

![Снимок экрана с домашней страницей](./images/create-app-01.png)
