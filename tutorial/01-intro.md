<!-- markdownlint-disable MD002 MD041 -->

В этом руководстве рассказывается, как создать приложение для универсальной платформы Windows (UWP), которое использует API Microsoft Graph для получения сведений о календаре для пользователя.

> [!TIP]
> Если вы предпочитаете просто скачать заполненный учебник, вы можете скачать или клонировать [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-uwp).

## <a name="prerequisites"></a>Необходимые компоненты

Прежде чем приступить к работе с этим руководством, на компьютере под управлением Windows 10 с [включенным режимом разработчика](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)должен быть установлен [Visual Studio](https://visualstudio.microsoft.com/vs/) . Если у вас нет Visual Studio, посетите предыдущую ссылку для получения вариантов загрузки.

Кроме того, у вас также должна быть личная учетная запись Майкрософт с почтовым ящиком на Outlook.com или рабочей или учебной учетной записью Майкрософт. Если у вас нет учетной записи Майкрософт, у вас есть несколько вариантов для получения бесплатной учетной записи:

- Вы можете [зарегистрироваться для создания новой личной учетной записи Майкрософт](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Вы можете [зарегистрироваться в программе для разработчиков office 365](https://developer.microsoft.com/office/dev-program) , чтобы получить бесплатную подписку на Office 365.

> [!NOTE]
> Это руководство было написано с помощью Visual Studio 2019 версии 16.5.0. Действия, описанные в этом руководстве, могут работать с другими версиями, но не тестировались.

## <a name="watch-the-tutorial"></a>Просмотр руководства

Этот модуль записан и доступен в канале разработки Office на YouTube.

<!-- markdownlint-disable MD033 MD034 -->
<br/>

> [!VIDEO https://www.youtube-nocookie.com/embed/oBYCBxkWMRA]
<!-- markdownlint-enable MD033 MD034 -->

## <a name="feedback"></a>Отзывы

Сообщите о нем в [репозиторий GitHub](https://github.com/microsoftgraph/msgraph-training-uwp).
