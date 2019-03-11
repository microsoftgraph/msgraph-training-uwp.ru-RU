# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="d8f2d-101">Выполнение завершенного проекта</span><span class="sxs-lookup"><span data-stu-id="d8f2d-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8f2d-102">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="d8f2d-102">Prerequisites</span></span>

<span data-ttu-id="d8f2d-103">Чтобы запустить завершенный проект в этой папке, вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="d8f2d-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="d8f2d-104">[Visual Studio](https://visualstudio.microsoft.com/vs/) , установленный на компьютере для разработки.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-104">[Visual Studio](https://visualstudio.microsoft.com/vs/) installed on your development machine.</span></span> <span data-ttu-id="d8f2d-105">Если у вас нет Visual Studio, посетите предыдущую ссылку для получения вариантов загрузки.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-105">If you do not have Visual Studio, visit the previous link for download options.</span></span> <span data-ttu-id="d8f2d-106">(**Примечание:** это руководство написано в Visual Studio 2017 версии 15,81.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-106">(**Note:** This tutorial was written with Visual Studio 2017 version 15.81.</span></span> <span data-ttu-id="d8f2d-107">Действия, описанные в этом руководстве, могут работать с другими версиями, но не тестировались.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="d8f2d-108">Личная учетная запись Майкрософт с почтовым ящиком на Outlook.com или рабочей или учебной учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="d8f2d-109">Если у вас нет учетной записи Майкрософт, у вас есть несколько вариантов для получения бесплатной учетной записи:</span><span class="sxs-lookup"><span data-stu-id="d8f2d-109">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="d8f2d-110">Вы можете [зарегистрироваться для создания новой личной учетной записи Майкрософт](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="d8f2d-110">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="d8f2d-111">Вы можете [зарегистрироваться в программе для разработчиков office 365](https://developer.microsoft.com/office/dev-program) , чтобы получить бесплатную подписку на Office 365.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-111">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-native-application-with-the-application-registration-portal"></a><span data-ttu-id="d8f2d-112">Регистрация собственного приложения с помощью портала регистрации приложений</span><span class="sxs-lookup"><span data-stu-id="d8f2d-112">Register a native application with the Application Registration Portal</span></span>

1. <span data-ttu-id="d8f2d-113">Откройте браузер и перейдите на [портал регистрации приложений](https://apps.dev.microsoft.com) и войдите в систему, используя **личную учетную запись** (с учетной записью Майкрософт) или **рабочую или учебную учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-113">Open a browser and navigate to the [Application Registration Portal](https://apps.dev.microsoft.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="d8f2d-114">В верхней части страницы выберите **Добавить приложение** .</span><span class="sxs-lookup"><span data-stu-id="d8f2d-114">Select **Add an app** at the top of the page.</span></span>

    > <span data-ttu-id="d8f2d-115">**Примечание:** Если на странице отображается несколько кнопок **Добавить приложение** , выберите ту, которая соответствует списку **приложений** для конвергенции.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-115">**Note:** If you see more than one **Add an app** button on the page, select the one that corresponds to the **Converged apps** list.</span></span>

1. <span data-ttu-id="d8f2d-116">На странице **Регистрация приложения** присвойте параметру **имя приложения** учебнику **Диаграмма UWP** и выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-116">On the **Register your application** page, set the **Application Name** to **UWP Graph Tutorial** and select **Create**.</span></span>

    ![Снимок экрана: создание нового приложения на веб-сайте портала регистрации приложений](../../../Images/arp-create-app-01.png)

1. <span data-ttu-id="d8f2d-118">На странице **Регистрация руководства диаграммы UWP** в разделе **свойства** скопируйте **идентификатор приложения** так, как он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-118">On the **UWP Graph Tutorial Registration** page, under the **Properties** section, copy the **Application Id** as you will need it later.</span></span>

    ![Снимок экрана с ИДЕНТИФИКАТОРом только что созданного приложения](../../../Images/arp-create-app-02.png)

1. <span data-ttu-id="d8f2d-120">ПроКрутите окно вниз до раздела **платформы** .</span><span class="sxs-lookup"><span data-stu-id="d8f2d-120">Scroll down to the **Platforms** section.</span></span>

    1. <span data-ttu-id="d8f2d-121">Нажмите кнопку **Добавить платформу**.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-121">Select **Add Platform**.</span></span>
    1. <span data-ttu-id="d8f2d-122">В диалоговом окне **Добавление платформы** выберите **собственное приложение**.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-122">In the **Add Platform** dialog, select **Native Application**.</span></span>

        ![Снимок экрана: создание платформы для приложения](../../../Images/arp-create-app-03.png)

1. <span data-ttu-id="d8f2d-124">ПроКрутите страницу вниз и выберите команду **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-124">Scroll to the bottom of the page and select **Save**.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="d8f2d-125">Настройка примера</span><span class="sxs-lookup"><span data-stu-id="d8f2d-125">Configure the sample</span></span>

1. <span data-ttu-id="d8f2d-126">Переименуйте `OAuth.resw.example` файл в `OAuth.resw`.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-126">Rename the `OAuth.resw.example` file to `OAuth.resw`.</span></span>
1. <span data-ttu-id="d8f2d-127">Откройте `graph-tutorial.sln` в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-127">Open `graph-tutorial.sln` in Visual Studio.</span></span>
1. <span data-ttu-id="d8f2d-128">Измените `OAuth.resw` файл в Visual Studio. Замените `YOUR_APP_ID_HERE` идентификатором **приложения** , полученНым на портале регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-128">Edit the `OAuth.resw` file in visual studio.Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="d8f2d-129">В обозревателе решений щелкните правой кнопкой мыши решение **Graph – Tutorial** и выберите пункт **восстановление пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-129">In Solution Explorer, right-click the **graph-tutorial** solution and choose **Restore NuGet Packages**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="d8f2d-130">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="d8f2d-130">Run the sample</span></span>

<span data-ttu-id="d8f2d-131">В Visual Studio нажмите клавишу **F5** или выберите **Отладка _гт_ начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="d8f2d-131">In Visual Studio, press **F5** or choose **Debug > Start Debugging**.</span></span>