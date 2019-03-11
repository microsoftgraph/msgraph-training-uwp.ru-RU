<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9bf55-101">В этом упражнении вы создадите новое собственное приложение Azure AD с помощью портала реестра приложений (ARP).</span><span class="sxs-lookup"><span data-stu-id="9bf55-101">In this exercise you will create a new Azure AD native application using the Application Registry Portal (ARP).</span></span>

1. <span data-ttu-id="9bf55-102">Откройте браузер и перейдите на [портал регистрации приложений](https://apps.dev.microsoft.com) и войдите в систему, используя **личную учетную запись** (с учетной записью Майкрософт) или **рабочую или учебную учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="9bf55-102">Open a browser and navigate to the [Application Registration Portal](https://apps.dev.microsoft.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="9bf55-103">В верхней части страницы выберите **Добавить приложение** .</span><span class="sxs-lookup"><span data-stu-id="9bf55-103">Select **Add an app** at the top of the page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9bf55-104">Если на странице отображается несколько кнопок **Добавить приложение** , выберите ту, которая соответствует списку **приложений** для конвергенции.</span><span class="sxs-lookup"><span data-stu-id="9bf55-104">If you see more than one **Add an app** button on the page, select the one that corresponds to the **Converged apps** list.</span></span>

1. <span data-ttu-id="9bf55-105">На странице **Регистрация приложения** присвойте параметру **имя приложения** учебнику **Диаграмма UWP** и выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="9bf55-105">On the **Register your application** page, set the **Application Name** to **UWP Graph Tutorial** and select **Create**.</span></span>

    ![Снимок экрана: создание нового приложения на веб-сайте портала регистрации приложений](./images/arp-create-app-01.png)

1. <span data-ttu-id="9bf55-107">На странице **Регистрация руководства диаграммы UWP** в разделе **свойства** скопируйте **идентификатор приложения** так, как он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="9bf55-107">On the **UWP Graph Tutorial Registration** page, under the **Properties** section, copy the **Application Id** as you will need it later.</span></span>

    ![Снимок экрана с ИДЕНТИФИКАТОРом только что созданного приложения](./images/arp-create-app-02.png)

1. <span data-ttu-id="9bf55-109">ПроКрутите окно вниз до раздела **платформы** .</span><span class="sxs-lookup"><span data-stu-id="9bf55-109">Scroll down to the **Platforms** section.</span></span>

    1. <span data-ttu-id="9bf55-110">Нажмите кнопку **Добавить платформу**.</span><span class="sxs-lookup"><span data-stu-id="9bf55-110">Select **Add Platform**.</span></span>
    1. <span data-ttu-id="9bf55-111">В диалоговом окне **Добавление платформы** выберите **собственное приложение**.</span><span class="sxs-lookup"><span data-stu-id="9bf55-111">In the **Add Platform** dialog, select **Native Application**.</span></span>

        ![Снимок экрана: создание платформы для приложения](./images/arp-create-app-03.png)

1. <span data-ttu-id="9bf55-113">ПроКрутите страницу вниз и выберите команду **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9bf55-113">Scroll to the bottom of the page and select **Save**.</span></span>