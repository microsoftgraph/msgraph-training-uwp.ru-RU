<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="02fcb-101">В этом руководстве рассказывается, как создать приложение для универсальной платформы Windows (UWP), которое использует API Microsoft Graph для получения сведений о календаре для пользователя.</span><span class="sxs-lookup"><span data-stu-id="02fcb-101">This tutorial teaches you how to build a Universal Windows Platform (UWP) app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="02fcb-102">Если вы предпочитаете просто скачать заполненный учебник, вы можете скачать или клонировать [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-uwp).</span><span class="sxs-lookup"><span data-stu-id="02fcb-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-uwp).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02fcb-103">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="02fcb-103">Prerequisites</span></span>

<span data-ttu-id="02fcb-104">Прежде чем приступить к работе с этим руководством, на компьютере под управлением Windows 10 с включенным [режимом разработчика](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)должен быть установлен [Visual Studio](https://visualstudio.microsoft.com/vs/) .</span><span class="sxs-lookup"><span data-stu-id="02fcb-104">Before you start this tutorial, you should have [Visual Studio](https://visualstudio.microsoft.com/vs/) installed on a computer running Windows 10 with [Developer mode turned on](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development).</span></span> <span data-ttu-id="02fcb-105">Если у вас нет Visual Studio, посетите предыдущую ссылку для получения вариантов загрузки.</span><span class="sxs-lookup"><span data-stu-id="02fcb-105">If you do not have Visual Studio, visit the previous link for download options.</span></span>

> [!NOTE]
> <span data-ttu-id="02fcb-106">Это руководство было написано с помощью Visual Studio 2017 версии 15.8.1.</span><span class="sxs-lookup"><span data-stu-id="02fcb-106">This tutorial was written with Visual Studio 2017 version 15.8.1.</span></span> <span data-ttu-id="02fcb-107">Действия, описанные в этом руководстве, могут работать с другими версиями, но не тестировались.</span><span class="sxs-lookup"><span data-stu-id="02fcb-107">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="feedback"></a><span data-ttu-id="02fcb-108">Обратная связь</span><span class="sxs-lookup"><span data-stu-id="02fcb-108">Feedback</span></span>

<span data-ttu-id="02fcb-109">Сообщите о нем в [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-uwp).</span><span class="sxs-lookup"><span data-stu-id="02fcb-109">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-uwp).</span></span>