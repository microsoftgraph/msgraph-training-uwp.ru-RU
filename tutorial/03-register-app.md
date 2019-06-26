<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="30df9-101">В этом упражнении вы создадите новое собственное приложение Azure AD с помощью центра администрирования Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30df9-101">In this exercise you will create a new Azure AD native application using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="30df9-102">Откройте браузер и перейдите в [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) и войдите с помощью **личной учетной записи** (т.е. учетной записи Майкрософт) или **рабочей или учебной учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="30df9-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="30df9-103">Выберите **Azure Active Directory** в левой панели навигации, а затем выберите **Регистрация приложений** в разделе **Управление**.</span><span class="sxs-lookup"><span data-stu-id="30df9-103">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="30df9-104">Снимок экрана с регистрациями приложений</span><span class="sxs-lookup"><span data-stu-id="30df9-104">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="30df9-105">Выберите **Новая регистрация**.</span><span class="sxs-lookup"><span data-stu-id="30df9-105">Select **New registration**.</span></span> <span data-ttu-id="30df9-106">На странице**Зарегистрировать приложение** задайте необходимые значения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="30df9-106">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="30df9-107">Введите **имя** `UWP Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="30df9-107">Set **Name** to `UWP Graph Tutorial`.</span></span>
    - <span data-ttu-id="30df9-108">Введите **поддерживаемые типы учетных записей** для **учетных записей в любом каталоге организаций и личных учетных записей Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="30df9-108">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="30df9-109">В разделе **URI перенаправления**измените раскрывающийся список на общедоступный **клиент (мобильный & Настольный)** и `urn:ietf:wg:oauth:2.0:oob`задайте значение.</span><span class="sxs-lookup"><span data-stu-id="30df9-109">Under **Redirect URI**, change the dropdown to **Public client (mobile & desktop)**, and set the value to `urn:ietf:wg:oauth:2.0:oob`.</span></span>

    ![Снимок страницы "регистрация приложения"](./images/aad-register-app.png)

1. <span data-ttu-id="30df9-111">Выберите **регистр**.</span><span class="sxs-lookup"><span data-stu-id="30df9-111">Select **Register**.</span></span> <span data-ttu-id="30df9-112">На странице **учебника UWP Graph** СКОПИРУЙТЕ значение **идентификатора Application (Client)** и сохраните его, он понадобится на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="30df9-112">On the **UWP Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Снимок экрана с ИДЕНТИФИКАТОРом приложения для новой регистрации приложения](./images/aad-application-id.png)
