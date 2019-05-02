<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="dc764-101">В этом упражнении вы будете расширяем приложение из предыдущего упражнения для поддержки проверки подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc764-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="dc764-102">Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="dc764-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="dc764-103">На этом этапе вы интегрируете элемент управления [аадлогин](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable) из [набора инструментов сообщества Windows](https://github.com/Microsoft/WindowsCommunityToolkit) в приложение.</span><span class="sxs-lookup"><span data-stu-id="dc764-103">In this step you will integrate the [AadLogin](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable) control from the [Windows Community Toolkit](https://github.com/Microsoft/WindowsCommunityToolkit) into the application.</span></span>

<span data-ttu-id="dc764-104">Щелкните правой кнопкой мыши проект **Graph – Tutorial** в обозревателе решений и выберите команду **Добавить _гт_ новый элемент..**.. Выберите **файл Resources (. РеСВ)**, назовите файл `OAuth.resw` и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="dc764-104">Right-click the **graph-tutorial** project in Solution Explorer and choose **Add > New Item...**. Choose **Resources File (.resw)**, name the file `OAuth.resw` and choose **Add**.</span></span> <span data-ttu-id="dc764-105">Когда новый файл откроется в Visual Studio, создайте два ресурса, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="dc764-105">When the new file opens in Visual Studio, create two resources as follows.</span></span>

- <span data-ttu-id="dc764-106">**Имя:** `AppId`, **Value:** идентификатор приложения, созданный на портале регистрации приложений</span><span class="sxs-lookup"><span data-stu-id="dc764-106">**Name:** `AppId`, **Value:** the app ID you generated in Application Registration Portal</span></span>
- <span data-ttu-id="dc764-107">**Имя:** `Scopes`, **Значение:**`User.Read Calendars.Read`</span><span class="sxs-lookup"><span data-stu-id="dc764-107">**Name:** `Scopes`, **Value:** `User.Read Calendars.Read`</span></span>

![Снимок экрана: файл OAuth. РеСВ в редакторе Visual Studio](./images/edit-resources-01.png)

> [!IMPORTANT]
> <span data-ttu-id="dc764-109">Если вы используете систему управления версиями (например, Git), то теперь мы бы не могли исключить `OAuth.resw` файл из системы управления версиями, чтобы избежать случайной утечки идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="dc764-109">If you're using source control such as git, now would be a good time to exclude the `OAuth.resw` file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="configure-the-aadlogin-control"></a><span data-ttu-id="dc764-110">Настройка элемента управления Аадлогин</span><span class="sxs-lookup"><span data-stu-id="dc764-110">Configure the AadLogin control</span></span>

<span data-ttu-id="dc764-111">Начните с добавления кода для считывания значений из файла ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dc764-111">Start by adding code to read the values out of the resources file.</span></span> <span data-ttu-id="dc764-112">Откройте `MainPage.xaml.cs` и добавьте приведенный `using` ниже оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="dc764-112">Open `MainPage.xaml.cs` and add the following `using` statement to the top of the file.</span></span>

```cs
using Microsoft.Toolkit.Services.MicrosoftGraph;
```

<span data-ttu-id="dc764-113">Замените строку `RootFrame.Navigate(typeof(HomePage));` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="dc764-113">Replace the `RootFrame.Navigate(typeof(HomePage));` line with the following code.</span></span>

```cs
// Load OAuth settings
var oauthSettings = Windows.ApplicationModel.Resources.ResourceLoader.GetForCurrentView("OAuth");
var appId = oauthSettings.GetString("AppId");
var scopes = oauthSettings.GetString("Scopes");

if (string.IsNullOrEmpty(appId) || string.IsNullOrEmpty(scopes))
{
    Notification.Show("Could not load OAuth Settings from resource file.");
}
else
{
    // Initialize Graph
    MicrosoftGraphService.Instance.AuthenticationModel = MicrosoftGraphEnums.AuthenticationModel.V2;
    MicrosoftGraphService.Instance.Initialize(appId,
        MicrosoftGraphEnums.ServicesToInitialize.UserProfile,
        scopes.Split(' '));

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
}
```

<span data-ttu-id="dc764-114">Этот код загружает параметры из `OAuth.resw` и инициализирует глобальный экземпляр объекта `MicrosoftGraphService` с этими значениями.</span><span class="sxs-lookup"><span data-stu-id="dc764-114">This code loads the settings from `OAuth.resw` and initializes the global instance of the `MicrosoftGraphService` with those values.</span></span>

<span data-ttu-id="dc764-115">Теперь добавьте обработчик события для `SignInCompleted` события в `AadLogin` элементе управления.</span><span class="sxs-lookup"><span data-stu-id="dc764-115">Now add an event handler for the `SignInCompleted` event on the `AadLogin` control.</span></span> <span data-ttu-id="dc764-116">Откройте `MainPage.xaml` файл и замените существующий `<graphControls:AadLogin>` элемент приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="dc764-116">Open the `MainPage.xaml` file and replace the existing `<graphControls:AadLogin>` element with the following.</span></span>

```xml
<graphControls:AadLogin x:Name="Login"
    HorizontalAlignment="Left"
    View="SmallProfilePhotoLeft"
    AllowSignInAsDifferentUser="False"
    SignInCompleted="Login_SignInCompleted"
    SignOutCompleted="Login_SignOutCompleted"
    />
```

<span data-ttu-id="dc764-117">Затем добавьте указанные ниже функции в `MainPage` класс в `MainPage.xaml.cs`файле.</span><span class="sxs-lookup"><span data-stu-id="dc764-117">Then add the following functions to the `MainPage` class in `MainPage.xaml.cs`.</span></span>

```cs
private void Login_SignInCompleted(object sender, Microsoft.Toolkit.Uwp.UI.Controls.Graph.SignInEventArgs e)
{
    // Set the auth state
    SetAuthState(true);
    // Reload the home page
    RootFrame.Navigate(typeof(HomePage));
}

private void Login_SignOutCompleted(object sender, EventArgs e)
{
    // Set the auth state
    SetAuthState(false);
    // Reload the home page
    RootFrame.Navigate(typeof(HomePage));
}
```

<span data-ttu-id="dc764-118">Наконец, в обозревателе решений разверните узел **Homepage. XAML** и откройте `HomePage.xaml.cs`его.</span><span class="sxs-lookup"><span data-stu-id="dc764-118">Finally, in Solution Explorer, expand **HomePage.xaml** and open `HomePage.xaml.cs`.</span></span> <span data-ttu-id="dc764-119">Добавьте следующий код после `this.InitializeComponent();` строки.</span><span class="sxs-lookup"><span data-stu-id="dc764-119">Add the following code after the `this.InitializeComponent();` line.</span></span>

```cs
if ((App.Current as App).IsAuthenticated)
{
    HomePageMessage.Text = "Welcome! Please use the menu to the left to select a view.";
}
```

<span data-ttu-id="dc764-120">Перезапустите приложение и щелкните элемент \*\*\*\* управления входом в верхней части приложения.</span><span class="sxs-lookup"><span data-stu-id="dc764-120">Restart the app and click the **Sign In** control at the top of the app.</span></span> <span data-ttu-id="dc764-121">Когда вы вошли в систему, Пользовательский интерфейс должен измениться, чтобы показать, что вы успешно выполнили вход.</span><span class="sxs-lookup"><span data-stu-id="dc764-121">Once you've signed in, the UI should change to indicate that you've successfully signed-in.</span></span>

![Снимок экрана приложения после входа](./images/add-aad-auth-01.png)

> [!NOTE]
> <span data-ttu-id="dc764-123">`AadLogin` Элемент управления реализует логику сохранения и обновления маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="dc764-123">The `AadLogin` control implements the logic of storing and refreshing the access token for you.</span></span> <span data-ttu-id="dc764-124">Маркеры хранятся в безопасном хранилище и обновляются по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="dc764-124">The tokens are stored in secure storage and refreshed as needed.</span></span>