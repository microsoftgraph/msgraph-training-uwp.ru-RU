<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="8065b-101">В этом упражнении вы создадите новое собственное приложение Azure AD с помощью центра администрирования Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8065b-101">In this exercise you will create a new Azure AD native application using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="8065b-102">Откройте браузер и перейдите в [центр администрирования Azure Active Directory](https://aad.portal.azure.com) и войдите в систему, используя **личную учетную запись** (с учетной записью Майкрософт) или **рабочую или учебную учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="8065b-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="8065b-103">Выберите **Azure Active Directory** в левой панели навигации, а затем выберите **Регистрация приложений (Предварительная версия)** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="8065b-103">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations (Preview)** under **Manage**.</span></span>

    ![<span data-ttu-id="8065b-104">Снимок экрана с регистрациями приложений</span><span class="sxs-lookup"><span data-stu-id="8065b-104">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="8065b-105">Нажмите кнопку **создать регистрацию**.</span><span class="sxs-lookup"><span data-stu-id="8065b-105">Select **New registration**.</span></span> <span data-ttu-id="8065b-106">На странице **Регистрация приложения** задайте указанные ниже значения.</span><span class="sxs-lookup"><span data-stu-id="8065b-106">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="8065b-107">Задайте \*\*\*\* для `UWP Graph Tutorial`параметра Name значение.</span><span class="sxs-lookup"><span data-stu-id="8065b-107">Set **Name** to `UWP Graph Tutorial`.</span></span>
    - <span data-ttu-id="8065b-108">Установите **Поддерживаемые типы учетных** записей для **учетных записей в любом организационном каталоге и личных учетНых записях Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="8065b-108">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="8065b-109">Оставьте пустым **URI перенаправления** .</span><span class="sxs-lookup"><span data-stu-id="8065b-109">Leave **Redirect URI** empty.</span></span>

    ![Снимок страницы "регистрация приложения"](./images/aad-register-an-app.png)

1. <span data-ttu-id="8065b-111">Выберите **регистр**.</span><span class="sxs-lookup"><span data-stu-id="8065b-111">Choose **Register**.</span></span> <span data-ttu-id="8065b-112">На странице **учебника UWP Graph** СКОПИРУЙТЕ значение **идентификатора Application (Client)** и сохраните его, он понадобится на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="8065b-112">On the **UWP Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Снимок экрана с ИДЕНТИФИКАТОРом приложения для новой регистрации приложения](./images/aad-application-id.png)

1. <span data-ttu-id="8065b-114">Выберите ссылку **Добавить URI перенаправления** .</span><span class="sxs-lookup"><span data-stu-id="8065b-114">Select the **Add a Redirect URI** link.</span></span> <span data-ttu-id="8065b-115">На странице " **Перенаправление URI** " выберите раздел **Перенаправление URI для общедоступных клиентов (мобильный, Настольный)** .</span><span class="sxs-lookup"><span data-stu-id="8065b-115">On the **Redirect URIs** page, locate the **Suggested Redirect URIs for public clients (mobile, desktop)** section.</span></span> <span data-ttu-id="8065b-116">Выберите `urn:ietf:wg:oauth:2.0:oob` универсальный код ресурса (URI) и нажмите кнопку **Save (сохранить**).</span><span class="sxs-lookup"><span data-stu-id="8065b-116">Select the `urn:ietf:wg:oauth:2.0:oob` URI, then choose **Save**.</span></span>

    ![Снимок экрана со страницей URI переНаправления](./images/aad-redirect-uris.png)