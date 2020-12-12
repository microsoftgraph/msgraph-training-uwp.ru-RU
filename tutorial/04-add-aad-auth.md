<!-- markdownlint-disable MD002 MD041 -->

В этом упражнении вы расширим приложение из предыдущего упражнения, чтобы поддерживать проверку подлинности с помощью Azure AD. Это необходимо для получения необходимого маркера доступа OAuth для вызова Microsoft Graph. На этом этапе вы интегрируете элемент **управления LoginButton** из элементов управления [Windows Graph](https://github.com/windows-toolkit/Graph-Controls) в приложение.

1. Щелкните правой кнопкой мыши проект **GraphTutorial** в обозревателе решений и **выберите "Добавить > новый элемент...".** Choose **Resources File (.resw)**, name the file `OAuth.resw` and select **Add**. Когда новый файл откроется в Visual Studio, создайте два ресурса следующим образом.

    - **Имя:** `AppId` , **Значение:** ИД приложения, созданный на портале регистрации приложений
    - **Имя:** `Scopes` , **Значение:**`User.Read User.ReadBasic.All People.Read MailboxSettings.Read Calendars.ReadWrite`

    ![Снимок экрана: файл OAuth.resw в Visual Studio редакторе](./images/edit-resources-01.png)

    > [!IMPORTANT]
    > Если вы используете управление исходным кодом, например git, пришло бы время исключить файл из системы управления источником, чтобы не допустить случайной утечки вашего `OAuth.resw` ИД приложения.

## <a name="configure-the-loginbutton-control"></a>Настройка управления LoginButton

1. Откройте `MainPage.xaml.cs` и добавьте следующий `using` выписку в верхнюю часть файла.

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    ```

1. Замените существующий конструктор следующим:

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ConstructorSnippet":::

    Этот код загружает параметры и инициализирует поставщика `OAuth.resw` MSAL с этими значениями.

1. Теперь добавьте обработок события `ProviderUpdated` в `ProviderManager` . Добавьте к классу `MainPage` следующую функцию:

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ProviderUpdatedSnippet":::

    Это событие инициирует изменение поставщика или изменение состояния поставщика.

1. В обозревателе решений **разкроем homePage.xaml** и откройте `HomePage.xaml.cs` . Замените существующий конструктор на следующий.

    :::code language="csharp" source="../demo/GraphTutorial/HomePage.xaml.cs" id="ConstructorSnippet":::

1. Перезапустите приложение и **щелкните в верхней** части приложения кнопку "Вход". После того как вы выполнили вставку, пользовательский интерфейс должен измениться, чтобы указать, что вы успешно выполнили вставку.

    ![Снимок экрана: приложение после регистрации](./images/add-aad-auth-01.png)

    > [!NOTE]
    > Этот контроль реализует логику хранения и `ButtonLogin` обновления маркера доступа. Маркеры хранятся в безопасном хранилище и обновляются по мере необходимости.
