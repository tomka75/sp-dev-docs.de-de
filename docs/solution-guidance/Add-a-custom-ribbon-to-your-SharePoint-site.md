---
title: "Hinzufügen eines benutzerdefinierten Menüband zu Ihrer SharePoint-Website"
ms.date: 11/03/2017
ms.openlocfilehash: 3f7d212ca1b263d61f17e26092618753c9daa70e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-custom-ribbon-to-your-sharepoint-site"></a>Hinzufügen eines benutzerdefinierten Menübands zu Ihrer SharePoint-Website

Hinzufügen oder Entfernen eines benutzerdefinierten Menübands zu bzw. von Ihrer SharePoint-Website. Fügen Sie JavaScript-Ereignishandler mithilfe der eingebetteten JavaScript-Technik hinzu, um die Ereignisse Ihres benutzerdefinierten Menübands zu behandeln.

_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_

Das [Core.RibbonCommands]((https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands))-Codebeispiel zeigt, wie Sie ein benutzerdefiniertes Menüband zu Ihrer SharePoint-Website hinzufügen. Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:

- Sie möchten ein benutzerdefiniertes Menüband, eine Gruppe oder eine Schaltfläche zu Ihrer SharePoint-Website oder -Liste hinzufügen.
    
- Sie möchten ein benutzerdefiniertes Menüband für bestimmte Inhaltstypen, Websites oder Listen anzeigen.

> [!NOTE] 
> In diesem Codebeispiel wird gezeigt, wie Sie die JavaScript-Funktionen aufrufen, die Ereignisse behandeln, die von den Schaltflächen des Menübands ausgelöst wurden. Dieses Codebeispiel stellt nicht die Implementierung der JavaScript-Ereignishandlerfunktionen für die Schaltflächen des Menübands bereit. Um die JavaScript-Ereignishandlerfunktionen zu implementieren, verwenden Sie die eingebettete JavaScript-Technik zum Einbetten der JavaScript-Ereignishandlerfunktionen auf allen Seiten, auf denen das benutzerdefinierte Menüband angezeigt wird. Weitere Informationen zum Einbetten von JavaScript finden Sie unter [Anpassen der Benutzeroberfläche Ihrer SharePoint-Website mithilfe von JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie zunächst das [Core.RibbonCommands]((https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands))-Beispiel-Add-In aus dem Projekt [Office 365-Entwicklermuster und -vorgehensweisen]((https://github.com/SharePoint/PnP/tree/dev)) auf GitHub herunter.

## <a name="using-the-coreribboncommands-app"></a>Verwenden der Core.RibbonCommands-App
<a name="sectionSection1"> </a>

Wählen Sie beim Ausführen dieses Codebeispiels auf der Startseite unter **Menüband registrieren** die Option **Menüband hinzufügen** aus. Zeigen Sie beim Aktualisieren der Seite das benutzerdefinierte Menüband an, indem Sie **Dokumente** > **Benutzerdefinierte Registerkarte** auswählen.

In diesem Codebeispiel wird ein benutzerdefiniertes Menüband mithilfe von „Models\RibbonCommands.xml“ definiert. „RibbonCommands.xml“ definiert benutzerdefinierte Menübandgruppen, Schaltflächen und Benutzeroberflächen-Ereignishandler für das Menüband. Weitere Informationen finden Sie unter [Anpassen und Erweitern des SharePoint Server 2010-Menübands](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx) und [Server-Menüband-XML](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx).

Das benutzerdefinierte Menüband wird aufgrund von **RegistrationId="0x01"** und **RegistrationType="ContentType"** auf allen Websites und Listen im Hostweb angezeigt.  **RegistrationId="0x01"** und **RegistrationType="ContentType"** geben an, dass das Menüband für alle Inhaltstypen angezeigt wird, die vom Typ **"0x01"** erben, bei denen es sich um Inhaltstypen handelt, die von der  **Item**-Klasse erben. Um Ihr Menüband auf einen benutzerdefinierten Inhaltstyp anzuwenden, ersetzen Sie "0x01" durch die ID Ihres benutzerdefinierten Inhaltstyps. Um das Menüband auf eine Liste anzuwenden, ändern Sie den Wert von RegistrationType in **List**. 

> [!NOTE] 
> Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.

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

> [!NOTE] 
> Wenn Sie die eingebettete JavaScript-Methode verwenden, um die Ereignisbehandlung für die Schaltflächen Ihrer Menübänder zu implementieren, muss die JavaScript-Datei die in den **CommandUIHandler**-Elementen definierten Methoden definieren. Die eingebettete JavaScript-Datei sollte beispielsweise Funktionen wie **GetCurrentItem** und **AddNewCustom** implementieren.

**InitializeButton_Click** in Default.aspx führt die folgenden Aufgaben aus:

1. Aufruf von **GetCustomActionXmlNode** zum Lesen der XML-Datei und zum Zurückgeben des **CustomAction**-Objekts in RibbonCommands.xml. Das **CustomAction**-Objekt enthält das Markup für die Anpassung des Menübands.
    
2. Lesen mehrerer Elemente und Attributwerte aus dem **CustomAction**-Objekt.
    
3. Konvertieren des **CommandUIExtension**-Elements (das die Menübandgruppen, Schaltflächen und Ereignishandler der Benutzeroberfläche definiert) in eine Zeichenfolge mit dem Namen **xmlContent**.
    
4.  Erstellen einer neuen benutzerdefinierten Aktion mithilfe von **clientContext.Web.UserCustomActions.Add**.
    
5. Hinzufügen des Markups für die Menübandanpassung (in **xmlContent**) zur SharePoint-Website mit der **CustomAction.CommandUIExtension**.
    
6. Registrieren des benutzerdefinierten Menübands durch Festlegen von **CustomAction.RegistrationId** und **CustomAction.RegistrationType** auf die Attributwerte des **CustomAction**-Objekts, das in Schritt 2 gelesen wurde.

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

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Anpassen der Benutzeroberfläche der SharePoint-Benutzeroberfläche mithilfe von JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md)
    
-  [Anpassen und Erweitern des SharePoint Server 2010-Menübands](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx)
    
-  [Server-Menüband-XML](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx)
    
