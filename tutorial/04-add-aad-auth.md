<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="fd897-101">В этом упражнении вы будете расширяем приложение из предыдущего упражнения для поддержки проверки подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd897-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="fd897-102">Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="fd897-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="fd897-103">На этом этапе выполняется интеграция элемента управления **логинбуттон** из [элементов управления Windows Graph](https://github.com/windows-toolkit/Graph-Controls) в приложение.</span><span class="sxs-lookup"><span data-stu-id="fd897-103">In this step you will integrate the **LoginButton** control from the [Windows Graph Controls](https://github.com/windows-toolkit/Graph-Controls) into the application.</span></span>

1. <span data-ttu-id="fd897-104">Щелкните правой кнопкой мыши проект **графтуториал** в обозревателе решений и выберите команду **Добавить > новый элемент..**.. Выберите **файл Resources (. РеСВ)**, назовите файл `OAuth.resw` и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="fd897-104">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Resources File (.resw)**, name the file `OAuth.resw` and select **Add**.</span></span> <span data-ttu-id="fd897-105">Когда новый файл откроется в Visual Studio, создайте два ресурса, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fd897-105">When the new file opens in Visual Studio, create two resources as follows.</span></span>

    - <span data-ttu-id="fd897-106">**Name:** `AppId`, **value:** идентификатор приложения, созданный на портале регистрации приложений</span><span class="sxs-lookup"><span data-stu-id="fd897-106">**Name:** `AppId`, **Value:** the app ID you generated in Application Registration Portal</span></span>
    - <span data-ttu-id="fd897-107">**Name:** `Scopes`, **значение:**`User.Read Calendars.Read`</span><span class="sxs-lookup"><span data-stu-id="fd897-107">**Name:** `Scopes`, **Value:** `User.Read Calendars.Read`</span></span>

    ![Снимок экрана: файл OAuth. РеСВ в редакторе Visual Studio](./images/edit-resources-01.png)

    > [!IMPORTANT]
    > <span data-ttu-id="fd897-109">Если вы используете систему управления версиями (например, Git), то теперь мы бы не могли исключить `OAuth.resw` файл из системы управления версиями, чтобы избежать случайной утечки идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="fd897-109">If you're using source control such as git, now would be a good time to exclude the `OAuth.resw` file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="configure-the-loginbutton-control"></a><span data-ttu-id="fd897-110">Настройка элемента управления Логинбуттон</span><span class="sxs-lookup"><span data-stu-id="fd897-110">Configure the LoginButton control</span></span>

1. <span data-ttu-id="fd897-111">Откройте `MainPage.xaml.cs` и добавьте приведенный `using` ниже оператор в начало файла.</span><span class="sxs-lookup"><span data-stu-id="fd897-111">Open `MainPage.xaml.cs` and add the following `using` statement to the top of the file.</span></span>

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    ```

1. <span data-ttu-id="fd897-112">Замените существующий конструктор приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="fd897-112">Replace the existing constructor with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ConstructorSnippet":::

    <span data-ttu-id="fd897-113">Этот код загружает параметры из `OAuth.resw` и Инициализирует поставщик MSAL с этими значениями.</span><span class="sxs-lookup"><span data-stu-id="fd897-113">This code loads the settings from `OAuth.resw` and initializes the MSAL provider with those values.</span></span>

1. <span data-ttu-id="fd897-114">Теперь добавьте обработчик события для `ProviderUpdated` события. `ProviderManager`</span><span class="sxs-lookup"><span data-stu-id="fd897-114">Now add an event handler for the `ProviderUpdated` event on the `ProviderManager`.</span></span> <span data-ttu-id="fd897-115">Добавьте к классу `MainPage` следующую функцию:</span><span class="sxs-lookup"><span data-stu-id="fd897-115">Add the following function to the `MainPage` class.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ProviderUpdatedSnippet":::

    <span data-ttu-id="fd897-116">Это событие инициируется при изменении поставщика или при изменении состояния поставщика.</span><span class="sxs-lookup"><span data-stu-id="fd897-116">This event triggers when the provider changes, or when the provider state changes.</span></span>

1. <span data-ttu-id="fd897-117">В обозревателе решений разверните узел **Homepage. XAML** и откройте `HomePage.xaml.cs`его.</span><span class="sxs-lookup"><span data-stu-id="fd897-117">In Solution Explorer, expand **HomePage.xaml** and open `HomePage.xaml.cs`.</span></span> <span data-ttu-id="fd897-118">Замените существующий конструктор приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="fd897-118">Replace the existing constructor with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/HomePage.xaml.cs" id="ConstructorSnippet":::

1. <span data-ttu-id="fd897-119">Перезапустите приложение и щелкните элемент управления **входом** в верхней части приложения.</span><span class="sxs-lookup"><span data-stu-id="fd897-119">Restart the app and click the **Sign In** control at the top of the app.</span></span> <span data-ttu-id="fd897-120">Когда вы вошли в систему, Пользовательский интерфейс должен измениться, чтобы показать, что вы успешно выполнили вход.</span><span class="sxs-lookup"><span data-stu-id="fd897-120">Once you've signed in, the UI should change to indicate that you've successfully signed-in.</span></span>

    ![Снимок экрана приложения после входа](./images/add-aad-auth-01.png)

    > [!NOTE]
    > <span data-ttu-id="fd897-122">`ButtonLogin` Элемент управления реализует логику сохранения и обновления маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="fd897-122">The `ButtonLogin` control implements the logic of storing and refreshing the access token for you.</span></span> <span data-ttu-id="fd897-123">Маркеры хранятся в безопасном хранилище и обновляются по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="fd897-123">The tokens are stored in secure storage and refreshed as needed.</span></span>
