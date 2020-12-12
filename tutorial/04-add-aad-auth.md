<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="07d48-101">В этом упражнении вы расширим приложение из предыдущего упражнения, чтобы поддерживать проверку подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07d48-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="07d48-102">Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="07d48-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="07d48-103">На этом этапе вы интегрируете элемент **управления LoginButton** из элементов управления [Windows Graph](https://github.com/windows-toolkit/Graph-Controls) в приложение.</span><span class="sxs-lookup"><span data-stu-id="07d48-103">In this step you will integrate the **LoginButton** control from the [Windows Graph Controls](https://github.com/windows-toolkit/Graph-Controls) into the application.</span></span>

1. <span data-ttu-id="07d48-104">Щелкните правой кнопкой мыши проект **GraphTutorial** в обозревателе решений и **выберите "Добавить > новый элемент...".** Choose **Resources File (.resw)**, name the file `OAuth.resw` and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="07d48-104">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Resources File (.resw)**, name the file `OAuth.resw` and select **Add**.</span></span> <span data-ttu-id="07d48-105">Когда новый файл откроется в Visual Studio, создайте два ресурса следующим образом.</span><span class="sxs-lookup"><span data-stu-id="07d48-105">When the new file opens in Visual Studio, create two resources as follows.</span></span>

    - <span data-ttu-id="07d48-106">**Имя:** `AppId` , **Значение:** ИД приложения, созданный на портале регистрации приложений</span><span class="sxs-lookup"><span data-stu-id="07d48-106">**Name:** `AppId`, **Value:** the app ID you generated in Application Registration Portal</span></span>
    - <span data-ttu-id="07d48-107">**Имя:** `Scopes` , **Значение:**`User.Read User.ReadBasic.All People.Read MailboxSettings.Read Calendars.ReadWrite`</span><span class="sxs-lookup"><span data-stu-id="07d48-107">**Name:** `Scopes`, **Value:** `User.Read User.ReadBasic.All People.Read MailboxSettings.Read Calendars.ReadWrite`</span></span>

    ![Снимок экрана: файл OAuth.resw в Visual Studio редакторе](./images/edit-resources-01.png)

    > [!IMPORTANT]
    > <span data-ttu-id="07d48-109">Если вы используете управление исходным кодом, например git, пришло бы время исключить файл из системы управления источником, чтобы не допустить случайной утечки вашего `OAuth.resw` ИД приложения.</span><span class="sxs-lookup"><span data-stu-id="07d48-109">If you're using source control such as git, now would be a good time to exclude the `OAuth.resw` file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="configure-the-loginbutton-control"></a><span data-ttu-id="07d48-110">Настройка управления LoginButton</span><span class="sxs-lookup"><span data-stu-id="07d48-110">Configure the LoginButton control</span></span>

1. <span data-ttu-id="07d48-111">Откройте `MainPage.xaml.cs` и добавьте следующий `using` выписку в верхнюю часть файла.</span><span class="sxs-lookup"><span data-stu-id="07d48-111">Open `MainPage.xaml.cs` and add the following `using` statement to the top of the file.</span></span>

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    ```

1. <span data-ttu-id="07d48-112">Замените существующий конструктор следующим:</span><span class="sxs-lookup"><span data-stu-id="07d48-112">Replace the existing constructor with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ConstructorSnippet":::

    <span data-ttu-id="07d48-113">Этот код загружает параметры и инициализирует поставщика `OAuth.resw` MSAL с этими значениями.</span><span class="sxs-lookup"><span data-stu-id="07d48-113">This code loads the settings from `OAuth.resw` and initializes the MSAL provider with those values.</span></span>

1. <span data-ttu-id="07d48-114">Теперь добавьте обработок события `ProviderUpdated` в `ProviderManager` .</span><span class="sxs-lookup"><span data-stu-id="07d48-114">Now add an event handler for the `ProviderUpdated` event on the `ProviderManager`.</span></span> <span data-ttu-id="07d48-115">Добавьте к классу `MainPage` следующую функцию:</span><span class="sxs-lookup"><span data-stu-id="07d48-115">Add the following function to the `MainPage` class.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ProviderUpdatedSnippet":::

    <span data-ttu-id="07d48-116">Это событие инициирует изменение поставщика или изменение состояния поставщика.</span><span class="sxs-lookup"><span data-stu-id="07d48-116">This event triggers when the provider changes, or when the provider state changes.</span></span>

1. <span data-ttu-id="07d48-117">В обозревателе решений **разкроем homePage.xaml** и откройте `HomePage.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="07d48-117">In Solution Explorer, expand **HomePage.xaml** and open `HomePage.xaml.cs`.</span></span> <span data-ttu-id="07d48-118">Замените существующий конструктор на следующий.</span><span class="sxs-lookup"><span data-stu-id="07d48-118">Replace the existing constructor with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/HomePage.xaml.cs" id="ConstructorSnippet":::

1. <span data-ttu-id="07d48-119">Перезапустите приложение и **щелкните в верхней** части приложения кнопку "Вход".</span><span class="sxs-lookup"><span data-stu-id="07d48-119">Restart the app and click the **Sign In** control at the top of the app.</span></span> <span data-ttu-id="07d48-120">После того как вы выполнили вставку, пользовательский интерфейс должен измениться, чтобы указать, что вы успешно выполнили вставку.</span><span class="sxs-lookup"><span data-stu-id="07d48-120">Once you've signed in, the UI should change to indicate that you've successfully signed-in.</span></span>

    ![Снимок экрана: приложение после регистрации](./images/add-aad-auth-01.png)

    > [!NOTE]
    > <span data-ttu-id="07d48-122">Этот контроль реализует логику хранения и `ButtonLogin` обновления маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="07d48-122">The `ButtonLogin` control implements the logic of storing and refreshing the access token for you.</span></span> <span data-ttu-id="07d48-123">Маркеры хранятся в безопасном хранилище и обновляются по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="07d48-123">The tokens are stored in secure storage and refreshed as needed.</span></span>
