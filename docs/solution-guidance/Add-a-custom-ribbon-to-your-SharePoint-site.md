---
title: "Hinzufügen eines benutzerdefinierten Menüband zu Ihrer SharePoint-Website"
ms.date: 11/03/2017
ms.openlocfilehash: 371711f55879477a62cd891c04e86e8aa2101db0
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="add-a-custom-ribbon-to-your-sharepoint-site"></a><span data-ttu-id="fc97c-102">Hinzufügen eines benutzerdefinierten Menübands zu Ihrer SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="fc97c-102">Add a custom ribbon to your SharePoint site</span></span>

<span data-ttu-id="fc97c-103">Hinzufügen oder Entfernen eines benutzerdefinierten Menübands zu bzw. von Ihrer SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="fc97c-103">Add or remove a custom ribbon on your SharePoint site.</span></span> <span data-ttu-id="fc97c-104">Fügen Sie JavaScript-Ereignishandler mithilfe der eingebetteten JavaScript-Technik hinzu, um die Ereignisse Ihres benutzerdefinierten Menübands zu behandeln.</span><span class="sxs-lookup"><span data-stu-id="fc97c-104">Add JavaScript event handlers using the embed JavaScript technique to handle your custom ribbon's events.</span></span>

<span data-ttu-id="fc97c-105">_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="fc97c-105">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="fc97c-106">Das [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands)-Codebeispiel zeigt, wie Sie ein benutzerdefiniertes Menüband zu Ihrer SharePoint-Website hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fc97c-106">The  [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands) code sample shows you how to add a custom ribbon to a SharePoint site.</span></span> <span data-ttu-id="fc97c-107">Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:</span><span class="sxs-lookup"><span data-stu-id="fc97c-107">Use this solution if you want to:</span></span>

- <span data-ttu-id="fc97c-108">Sie möchten ein benutzerdefiniertes Menüband, eine Gruppe oder eine Schaltfläche zu Ihrer SharePoint-Website oder -Liste hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fc97c-108">Add a custom ribbon, group, or button to your SharePoint site or list.</span></span>
    
- <span data-ttu-id="fc97c-109">Sie möchten ein benutzerdefiniertes Menüband für bestimmte Inhaltstypen, Websites oder Listen anzeigen.</span><span class="sxs-lookup"><span data-stu-id="fc97c-109">Display a custom ribbon for specific content types, sites, or lists.</span></span>

<span data-ttu-id="fc97c-110">**Hinweis**: In diesem Codebeispiel wird gezeigt, wie Sie die JavaScript-Funktionen aufrufen, die Ereignisse behandeln, die von den Schaltflächen des Menübands ausgelöst wurden.</span><span class="sxs-lookup"><span data-stu-id="fc97c-110">**Note**  This code sample shows how to call the JavaScript functions that handle events raised by the ribbon's buttons.</span></span> <span data-ttu-id="fc97c-111">Dieses Codebeispiel stellt nicht die Implementierung der JavaScript-Ereignishandlerfunktionen für die Schaltflächen des Menübands bereit.</span><span class="sxs-lookup"><span data-stu-id="fc97c-111">This code sample does not provide the implementation of the JavaScript event handler functions for the ribbon's buttons.</span></span> <span data-ttu-id="fc97c-112">Um die JavaScript-Ereignishandlerfunktionen zu implementieren, verwenden Sie die eingebettete JavaScript-Technik zum Einbetten der JavaScript-Ereignishandlerfunktionen auf allen Seiten, auf denen das benutzerdefinierte Menüband angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="fc97c-112">To implement the JavaScript event handler functions, use the embed JavaScript technique to embed the JavaScript event handler functions on all pages where your custom ribbon appears.</span></span> <span data-ttu-id="fc97c-113">Weitere Informationen zum Einbetten von JavaScript finden Sie unter [Anpassen der Benutzeroberfläche Ihrer SharePoint-Website mithilfe von JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).</span><span class="sxs-lookup"><span data-stu-id="fc97c-113">For more information about embedding JavaScript, see  [Customize your SharePoint site UI by using JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fc97c-114">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="fc97c-114">Before you begin</span></span>
<span data-ttu-id="fc97c-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="fc97c-115"></span></span>

<span data-ttu-id="fc97c-116">Laden Sie zunächst das [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands)-Beispiel-Add-In aus dem Projekt [Office 365-Entwicklermuster und -vorgehensweisen](https://github.com/SharePoint/PnP/tree/dev) auf GitHub herunter.</span><span class="sxs-lookup"><span data-stu-id="fc97c-116">To get started, download the  [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-coreribboncommands-app"></a><span data-ttu-id="fc97c-117">Verwenden der Core.RibbonCommands-App</span><span class="sxs-lookup"><span data-stu-id="fc97c-117">Using the Core.RibbonCommands app</span></span>
<span data-ttu-id="fc97c-118"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="fc97c-118"></span></span>

<span data-ttu-id="fc97c-119">Wählen Sie beim Ausführen dieses Codebeispiels auf der Startseite unter **Menüband registrieren** die Option **Menüband hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="fc97c-119">When you run this code sample, on the start page in  **Register the ribbon**, choose  **Add Ribbon**.</span></span> <span data-ttu-id="fc97c-120">Zeigen Sie beim Aktualisieren der Seite das benutzerdefinierte Menüband an, indem Sie **Dokumente** > **Benutzerdefinierte Registerkarte** auswählen.</span><span class="sxs-lookup"><span data-stu-id="fc97c-120">When the page refreshes, view the custom ribbon by choosing  **Documents** > **Custom Tab**.</span></span>

<span data-ttu-id="fc97c-121">In diesem Codebeispiel wird ein benutzerdefiniertes Menüband mithilfe von „Models\RibbonCommands.xml“ definiert.</span><span class="sxs-lookup"><span data-stu-id="fc97c-121">This code sample defines a custom ribbon by using Models\RibbonCommands.xml.</span></span> <span data-ttu-id="fc97c-122">„RibbonCommands.xml“ definiert benutzerdefinierte Menübandgruppen, Schaltflächen und Benutzeroberflächen-Ereignishandler für das Menüband.</span><span class="sxs-lookup"><span data-stu-id="fc97c-122">RibbonCommands.xml defines custom ribbon groups, buttons, and UI event handlers for the ribbon.</span></span> <span data-ttu-id="fc97c-123">Weitere Informationen finden Sie unter [Anpassen und Erweitern des SharePoint Server 2010-Menübands](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx) und [Server-Menüband-XML](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc97c-123">For more information, see [Customizing and Extending the SharePoint 2010 Server Ribbon](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx) and [Server Ribbon XML](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx).</span></span>

<span data-ttu-id="fc97c-124">Das benutzerdefinierte Menüband wird aufgrund von **RegistrationId="0x01"** und **RegistrationType="ContentType"** auf allen Websites und Listen im Hostweb angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fc97c-124">The custom ribbon displays on all sites and lists on the host web because  **RegistrationId="0x01"** and **RegistrationType="ContentType"**.</span></span>  <span data-ttu-id="fc97c-125">**RegistrationId="0x01"** und **RegistrationType="ContentType"** geben an, dass das Menüband für alle Inhaltstypen angezeigt wird, die vom Typ **"0x01"** erben, bei denen es sich um Inhaltstypen handelt, die von der  **Item**-Klasse erben.</span><span class="sxs-lookup"><span data-stu-id="fc97c-125">**RegistrationId="0x01"** and **RegistrationType="ContentType"** specify that the ribbon will appear for all content types that inherit from type **"0x01"**, which are content types that inherit from the  **Item** class.</span></span> <span data-ttu-id="fc97c-126">Um Ihr Menüband auf einen benutzerdefinierten Inhaltstyp anzuwenden, ersetzen Sie "0x01" durch die ID Ihres benutzerdefinierten Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="fc97c-126">To apply your ribbon to a custom content type, replace "0x01" with your custom content type's ID.</span></span> <span data-ttu-id="fc97c-127">Um das Menüband auf eine Liste anzuwenden, ändern Sie den Wert von RegistrationType in **List**.</span><span class="sxs-lookup"><span data-stu-id="fc97c-127">To apply your ribbon to a list, change the value of RegistrationType to **List**.</span></span> 

<span data-ttu-id="fc97c-128">**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="fc97c-128">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```XML
<?xml version="1.0" encoding="utf-8" ?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction
    Id="CustomCustomRibbonTab"
    Location="CommandUI.Ribbon.ListView"
    RegistrationId="0x01"
    RegistrationType="ContentType"
    Sequence="100"
    >
    <CommandUIExtension>
      <CommandUIDefinitions>
        <CommandUIDefinition
          Location="Ribbon.Tabs._children">
          <Tab
            Id="Ribbon.CustomRibbonTab"
            Title="Custom Tab"
            Description="Custom Tab Description"
            Sequence="501">
            <Scaling
              Id="Ribbon.CustomRibbonTab.Scaling">
              <MaxSize
                Id="Ribbon.CustomRibbonTab.MaxSize"
                GroupId="Ribbon.CustomRibbonTab.ManageCustomGroup"
                Size="OneLargeTwoMedium"/>
              <MaxSize
                Id="Ribbon.CustomRibbonTab.TabTwoMaxSize"
                GroupId="Ribbon.CustomRibbonTab.NewOpenCustomGroup"
                Size="TwoLarge" />
              <Scale
                Id="Ribbon.CustomRibbonTab.Scaling.CustomTabScaling"
                GroupId="Ribbon.CustomRibbonTab.ManageCustomGroup"
                Size="OneLargeTwoMedium" />
              <Scale
                Id="Ribbon.CustomRibbonTab.Scaling.CustomSecondTabScaling"
                GroupId="Ribbon.CustomRibbonTab.NewOpenCustomGroup"
                Size="TwoLarge" />
            </Scaling>
            <Groups Id="Ribbon.CustomRibbonTab.Groups">
              <Group
                Id="Ribbon.CustomRibbonTab.ManageCustomGroup"
                Description="Group to Custom Functions"
                Title="Manage Item"
                Sequence="52"
                Template="Ribbon.Templates.CustomTemplate">
                <Controls Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Controls">
                  <Button
                    Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Accept"
                    Command="CustomRibbonTab.AcceptCustomCommand"
                    Sequence="15"
                    Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                    Image32by32Top="-68"
                    Image32by32Left="-272"
                    Description="Accept Item"
                    LabelText="Accept"
                    TemplateAlias="AWR" />
                  <Button
                    Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Reject"
                    Command="CustomRibbonTab.RejectCustomCommand"
                    Sequence="17"
                    Image16by16="{SiteUrl}/_layouts/15/1033/Images/formatmap16x16.png?rev=23"
                    Image16by16Top="-216"
                    Image16by16Left="-290"
                    Description="Reject Item"
                    LabelText="Reject"
                    TemplateAlias="RWR"/>
                  <Button
                    Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Verify"
                    Command="CustomRibbonTab.VerifyCustomCommand"
                    Sequence="19"
                    Image16by16="{SiteUrl}/_layouts/15/1033/Images/formatmap16x16.png?rev=23"
                    Image16by16Top="-126"
                    Image16by16Left="-144"
                    Description="Verify Item"
                    LabelText="Verify"
                    TemplateAlias="ACWR"/>
                  <Button
                   Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Close"
                   Command="CustomRibbonTab.CloseCustomCommand"
                   Sequence="19"
                   Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                   Image32by32Top="-0"
                   Image32by32Left="-34"
                   Description="Close Item"
                   LabelText="Close"
                   TemplateAlias="CWR"/>
                  <Button
                   Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Copy"
                   Command="CustomRibbonTab.CopyCustomCommand"
                   Sequence="19"
                   Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                   Image32by32Top="-442"
                   Image32by32Left="-67"
                   Description="Copy Item"
                   LabelText="Copy"
                   TemplateAlias="CPWR"/>
                </Controls>
              </Group>
              <Group
                Id="Ribbon.CustomRibbonTab.NewOpenCustomGroup"
                Description="Group to manage item"
                Title="New &amp;amp; Open"
                Sequence="53"
                Template="Ribbon.Templates.CustomTemplate">
                <Controls Id="Ribbon.CustomRibbonTab.NewOpenCustomGroup.Controls">
                  <Button
                    Id="Ribbon.CustomRibbonTab.NewOpenCustomGroup.New"
                    Command="CustomRibbonTab.NewCustomCommand"
                    Sequence="15"
                    Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                    Image32by32Top="-33"
                    Image32by32Left="-66"
                    Description="New Item"
                    LabelText="New"
                    TemplateAlias="LOR"/>
                  <Button
                   Id="Ribbon.CustomRibbonTab.NewOpenCustomGroup.Open"
                   Command="CustomRibbonTab.OpenCustomCommand"
                   Sequence="15"
                   Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                   Image32by32Top="-170"
                   Image32by32Left="-138"
                   Description="Open Item"
                   LabelText="Open"
                   TemplateAlias="LORS"/>
                </Controls>
              </Group>
            </Groups>
          </Tab>
        </CommandUIDefinition>
        <CommandUIDefinition Location="Ribbon.Templates._children">
          <GroupTemplate Id="Ribbon.Templates.CustomTemplate">
            <Layout
              Title="OneLargeTwoMedium"
              LayoutTitle="OneLargeTwoMedium">
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="AWR" />
                </Row>
              </Section>
              <Section Alignment="Top" Type="TwoRow">
                <Row>
                  <ControlRef DisplayMode="Medium" TemplateAlias="RWR" />
                </Row>
                <Row>
                  <ControlRef DisplayMode="Medium" TemplateAlias="ACWR" />
                </Row>
              </Section>
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="CWR" />
                </Row>
              </Section>
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="CPWR" />
                </Row>
              </Section>
            </Layout>
            <Layout
             Title="TwoLarge"
             LayoutTitle="TwoLarge">
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="LOR" />
                </Row>
              </Section>
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="LORS" />
                </Row>
              </Section>
            </Layout>
          </GroupTemplate>
        </CommandUIDefinition>
      </CommandUIDefinitions>
      <CommandUIHandlers>
        <CommandUIHandler
          Command="CustomRibbonTab.AcceptCustomCommand"
          CommandAction="javascript:GetCurrentItem('AP');"/>
        <CommandUIHandler
          Command="CustomRibbonTab.RejectCustomCommand"
          CommandAction="javascript:GetCurrentItem('RJ');"/>
        <CommandUIHandler
          Command="CustomRibbonTab.VerifyCustomCommand"
          CommandAction="javascript:GetCurrentItem('AK');"/>
        <CommandUIHandler
          Command="CustomRibbonTab.NewCustomCommand"
          CommandAction="javascript:AddNewCustom();"/>
        <CommandUIHandler
          Command="CustomRibbonTab.OpenCustomCommand"
          CommandAction="javascript:OpenExistingCustom();"/>
        <CommandUIHandler
          Command="CustomRibbonTab.CloseCustomCommand"
          CommandAction="javascript:CloseExistingCustom();"/>
        <CommandUIHandler
          Command ="CustomRibbonTab.CopyCustomCommand"
          CommandAction="Javascript:CopyCustom();"/>
      </CommandUIHandlers>
    </CommandUIExtension>
  </CustomAction>
</Elements>
```

<span data-ttu-id="fc97c-129">**Hinweis** Wenn Sie die eingebettete JavaScript-Methode verwenden, um die Ereignisbehandlung für die Schaltflächen Ihrer Menübänder zu implementieren, muss die JavaScript-Datei die in den **CommandUIHandler**-Elementen definierten Methoden definieren.</span><span class="sxs-lookup"><span data-stu-id="fc97c-129">**Note**  If you use the embed JavaScript technique to implement event handling for your ribbons' buttons, your JavaScript file must implement the methods defined in the  **CommandUIHandler** elements.</span></span> <span data-ttu-id="fc97c-130">Die eingebettete JavaScript-Datei sollte beispielsweise Funktionen wie **GetCurrentItem** und **AddNewCustom** implementieren.</span><span class="sxs-lookup"><span data-stu-id="fc97c-130">For example, your embedded JavaScript file should implement functions like **GetCurrentItem** and **AddNewCustom**.</span></span>

<span data-ttu-id="fc97c-131">**InitializeButton_Click** in Default.aspx führt die folgenden Aufgaben aus:</span><span class="sxs-lookup"><span data-stu-id="fc97c-131">**InitializeButton_Click** in Default.aspx performs the following tasks:</span></span>

1. <span data-ttu-id="fc97c-132">Aufruf von **GetCustomActionXmlNode** zum Lesen der XML-Datei und zum Zurückgeben des **CustomAction**-Objekts in RibbonCommands.xml.</span><span class="sxs-lookup"><span data-stu-id="fc97c-132">Calls  **GetCustomActionXmlNode** to read the XML file and return the **CustomAction** object defined in RibbonCommands.xml.</span></span> <span data-ttu-id="fc97c-133">Das **CustomAction**-Objekt enthält das Markup für die Anpassung des Menübands.</span><span class="sxs-lookup"><span data-stu-id="fc97c-133">The **CustomAction** object contains the ribbon customization markup.</span></span>
    
2. <span data-ttu-id="fc97c-134">Lesen mehrerer Elemente und Attributwerte aus dem **CustomAction**-Objekt.</span><span class="sxs-lookup"><span data-stu-id="fc97c-134">Reads several elements and attribute values from the  **CustomAction** object.</span></span>
    
3. <span data-ttu-id="fc97c-135">Konvertieren des **CommandUIExtension**-Elements (das die Menübandgruppen, Schaltflächen und Ereignishandler der Benutzeroberfläche definiert) in eine Zeichenfolge mit dem Namen **xmlContent**.</span><span class="sxs-lookup"><span data-stu-id="fc97c-135">Converts the  **CommandUIExtension** element (which defines the ribbon groups, buttons, and UI event handlers) to a string called **xmlContent**.</span></span>
    
4.  <span data-ttu-id="fc97c-136">Erstellen einer neuen benutzerdefinierten Aktion mithilfe von **clientContext.Web.UserCustomActions.Add**.</span><span class="sxs-lookup"><span data-stu-id="fc97c-136">Creates a new custom action by using **clientContext.Web.UserCustomActions.Add**.</span></span>
    
5. <span data-ttu-id="fc97c-137">Hinzufügen des Markups für die Menübandanpassung (in **xmlContent**) zur SharePoint-Website mit der **CustomAction.CommandUIExtension**.</span><span class="sxs-lookup"><span data-stu-id="fc97c-137">Adds the ribbon customization markup (in  **xmlContent**) to the SharePoint site using the  **CustomAction.CommandUIExtension**.</span></span>
    
6. <span data-ttu-id="fc97c-138">Registrieren des benutzerdefinierten Menübands durch Festlegen von **CustomAction.RegistrationId** und **CustomAction.RegistrationType** auf die Attributwerte des **CustomAction**-Objekts, das in Schritt 2 gelesen wurde.</span><span class="sxs-lookup"><span data-stu-id="fc97c-138">Registers the custom ribbon by setting the  **CustomAction.RegistrationId** and **CustomAction.RegistrationType** to the attribute values of the **CustomAction** object read in step 2.</span></span>

```C#
 protected void InitializeButton_Click(object sender, EventArgs e) {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost()) {
                clientContext.Load(clientContext.Web, web => web.UserCustomActions);
                clientContext.ExecuteQuery();

                // Get the XML elements file and get the CommandUIExtension node.
                var customActionNode = GetCustomActionXmlNode();
                var customActionName = customActionNode.Attribute("Id").Value;
                var commandUIExtensionNode = customActionNode.Element(ns + "CommandUIExtension");
                var xmlContent = commandUIExtensionNode.ToString();
                var location = customActionNode.Attribute("Location").Value;
                var registrationId = customActionNode.Attribute("RegistrationId").Value;
                var registrationTypeString = customActionNode.Attribute("RegistrationType").Value;
                var registrationType = (UserCustomActionRegistrationType)Enum.Parse(typeof(UserCustomActionRegistrationType), registrationTypeString);

                var sequence = 1000;
                if (customActionNode.Attribute(ns + "Sequence") != null) {
                    sequence = Convert.ToInt32(customActionNode.Attribute(ns + "Sequence").Value);
                }

                // Determine if the custom action exists already.
                var customAction = clientContext.Web.UserCustomActions.FirstOrDefault(uca => uca.Name == customActionName);

                // If the custom action does not exist, create it.
                if (customAction == null) {
                    // create the ribbon.
                    customAction = clientContext.Web.UserCustomActions.Add();
                    customAction.Name = customActionName;
                }

                // Set custom action properties.
                customAction.Location = location;
                customAction.CommandUIExtension = xmlContent; // CommandUIExtension xml
                customAction.RegistrationId = registrationId;
                customAction.RegistrationType = registrationType;
                customAction.Sequence = sequence;

                customAction.Update();
                clientContext.Load(customAction);
                clientContext.ExecuteQuery();
            }
        }
```

## <a name="additional-resources"></a><span data-ttu-id="fc97c-139">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="fc97c-139">Additional resources</span></span>
<span data-ttu-id="fc97c-140"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="fc97c-140"></span></span>

-  [<span data-ttu-id="fc97c-141">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="fc97c-141">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="fc97c-142">Anpassen der Benutzeroberfläche der SharePoint-Benutzeroberfläche mithilfe von JavaScript</span><span class="sxs-lookup"><span data-stu-id="fc97c-142">Customize your SharePoint site UI by using JavaScript</span></span>](Customize-your-SharePoint-site-UI-by-using-JavaScript.md)
    
-  [<span data-ttu-id="fc97c-143">Anpassen und Erweitern des SharePoint Server 2010-Menübands</span><span class="sxs-lookup"><span data-stu-id="fc97c-143">Customizing and Extending the SharePoint 2010 Server Ribbon</span></span>](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx)
    
-  [<span data-ttu-id="fc97c-144">Server-Menüband-XML</span><span class="sxs-lookup"><span data-stu-id="fc97c-144">Server Ribbon XML</span></span>](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx)
    
