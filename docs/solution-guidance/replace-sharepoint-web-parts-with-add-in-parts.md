---
title: Ersetzen Sie SharePoint-Webparts mit Add-in-Webparts
ms.date: 11/03/2017
ms.openlocfilehash: af8c3eb1d5f314332542247f811b9a25daf0702a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="replace-sharepoint-web-parts-with-add-in-parts"></a>Ersetzen Sie SharePoint-Webparts mit Add-in-Webparts

Verwenden des Transformationsprozess Webparts mithilfe des SharePoint-Clientobjektmodells (CSOM) mit Add-in-Webparts zu ersetzen.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Den Transformationsprozess können SharePoint-Webparts mit Add-in-Webparts auf Seiten durch das Verwenden von CSOM zum Suchen und Entfernen von bestimmten Webparts, und fügen Sie dann das neue Add-in-Teile ersetzt.

**Wichtig:**  Farmlösungen können nicht mit SharePoint Online migriert werden. Durch die Techniken und den Code in diesem Artikel beschriebenen anwenden, können Sie einer neuen Lösung mit ähnlicher Funktionalität erstellen, dass Ihre farmlösungen zu ermöglichen, können in SharePoint Online bereitgestellt werden. Nachdem Sie diese Verfahren anwenden, werden Ihre Seiten-add-in Webparts verwenden, klicken Sie dann auf SharePoint Online migriert werden können aktualisiert werden. Der Code in diesem Artikel erfordert zusätzlichen Code, um eine voll funktionsfähige Lösung bereitzustellen. In diesem Artikel erläutern beispielsweise nicht Anleitung zu Office 365, authentifizieren Implementierung Ausnahmebehandlung erforderlich, und so weiter. Zusätzliche Codebeispiele finden Sie unter [Office 365 Developer Mustern und Methoden Projekt](https://github.com/SharePoint/PnP).

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Stellen Sie vor dem Ausführen der Schritte in diesem Artikel, um Ihre Webparts mit Add-in-Teile ersetzen sicher, dass Sie:

- Verwenden eine SharePoint-Umgebung, die so konfiguriert ist, zur Unterstützung von add-ins SharePoint Online ist so konfiguriert, dass-add-ins zu unterstützen. Wenn Sie SharePoint Server 2013 lokal verwenden, finden Sie unter [Konfigurieren einer Umgebung für SharePoint-Add-ins (SharePoint 2013)](https://technet.microsoft.com/library/fp161236%28v=office.15%29).
    
- Das neue Add-in-Teil haben in SharePoint bereitgestellt werden.
    
- Haben Ihre-add-ins **Vollzugriff** -Berechtigungen auf dem **Web**zugewiesen. Weitere Informationen finden Sie unter [Add-in-Berechtigungen in SharePoint 2013](https://msdn.microsoft.com/library/office/fp142383.aspx).

## <a name="replace-web-parts-with-add-in-parts"></a>Ersetzen Sie die Webparts durch Add-in-Webparts

So ersetzen die Webparts durch neue Add-in-Teile:

1. Exportieren Sie das neue Add-in-Teil. Verwenden Sie das exportierte Webpart-Add-in, um die Webpart-Add-in-Definition abzurufen. 
    
2. Suchen Sie nach allen Seiten mit Webparts ausgetauscht werden, und entfernen Sie die Webparts. 
    
3. Erstellen des neuen Teils-Add-in auf der Seite mithilfe der Webpart-Add-in-Definition. 
    
CSOM mithilfe um eines Webparts mit einem Webpart-Add-in zu ersetzen, müssen Sie die Webpart-Add-in-Definition durch Exportieren das Webpart-Add-Ins erhalten möchten. So exportieren Sie das Webpart-Add-in, um das Add-in-Webpart Definition abgerufen werden:

1. Öffnen Sie der SharePoint-Website und wählen Sie **Einstellungen**oder das Zahnradsymbol, und wählen Sie dann auf **Seite bearbeiten**.
    
2. Wählen Sie auf dem Menüband **Einfügen** > **Webpart-Add-in**.
    
3. Wählen Sie den Webpart-add-in, und wählen Sie dann auf **Hinzufügen**.
    
4. Wenn das Webpart-Add-in auf der Seite hinzugefügt wird, wählen Sie den Pfeil nach unten in der oberen rechten Ecke des Webparts-Add-in, und wählen Sie dann auf **Webpart bearbeiten**.
    
5. Im Dialogfeld **Erweitert**im **Modus exportieren** wählen Sie **alle Daten exportieren**, und wählen Sie dann auf **OK**.
    
6. Wenn Sie die Seite bearbeiten mit der Webpart-Add-in angezeigt zurückkehren, wählen Sie den Pfeil nach unten in der oberen rechten Ecke des Webparts-Add-in, und wählen Sie dann auf **Exportieren**.
    
7. Wählen Sie **Speichern**aus.
    
8. Nachdem der Download abgeschlossen ist, wählen Sie **Ordner öffnen**.
    
9. Öffnen Sie **Editor**, und wählen Sie **Datei** > **Öffnen**.
    
10. Wählen Sie die Add-in-Webpart-Datei, die Sie heruntergeladen haben, und wählen Sie dann die Webpart-Add-in-Definition anzeigen **Öffnen** .
    
> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```XML
<webParts>
  <webPart xmlns="http://schemas.microsoft.com/WebPart/v3">
    <metaData>
      <type name="Microsoft.SharePoint.WebPartPages.ClientWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" />
      <importErrorMessage>Cannot import this Web Part.</importErrorMessage>
    </metaData>
    <data>
      <properties>
        <property name="TitleIconImageUrl" type="string" />
        <property name="Direction" type="direction">NotSet</property>
        <property name="ExportMode" type="exportmode">All</property>
        <property name="HelpUrl" type="string" />
        <property name="Hidden" type="bool">False</property>
        <property name="Description" type="string">WelcomeAppPart Description</property>
        <property name="FeatureId" type="System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">0b846986-3474-4f1a-93cf-b7817ef057f9</property>
        <property name="CatalogIconImageUrl" type="string" />
        <property name="Title" type="string">WelcomeAppPart</property>
        <property name="AllowHide" type="bool">True</property>
        <property name="ProductWebId" type="System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">741c5404-f43e-4f01-acfb-fcd100fc7d24</property>
        <property name="AllowZoneChange" type="bool">True</property>
        <property name="TitleUrl" type="string" />
        <property name="ChromeType" type="chrometype">Default</property>
        <property name="AllowConnect" type="bool">True</property>
        <property name="Width" type="unit" />
        <property name="Height" type="unit" />
        <property name="WebPartName" type="string">WelcomeAppPart</property>
        <property name="HelpMode" type="helpmode">Navigate</property>
        <property name="AllowEdit" type="bool">True</property>
        <property name="AllowMinimize" type="bool">True</property>
        <property name="ProductId" type="System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">0b846986-3474-4f1a-93cf-b7817ef057f8</property>
        <property name="AllowClose" type="bool">True</property>
        <property name="ChromeState" type="chromestate">Normal</property>
      </properties>
    </data>
  </webPart>
</webParts>
```

So verwenden Sie die Webpart-Add-in-Definition in Ihrem Code CSOM

- Ersetzen Sie alle doppelte Anführungszeichen (") mit zwei doppelte Anführungszeichen (" ") in der Definition der Webpart-Add-in.
    
- Weisen Sie die Definition der Webpart-Add-in eine Zeichenfolge, die in Ihrem CSOM-Code verwendet werden.

```C#
private const string appPartXml = @"<webParts>
  <webPart xmlns=""http://schemas.microsoft.com/WebPart/v3"">
    <metaData>
      <type name=""Microsoft.SharePoint.WebPartPages.ClientWebPart, Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"" />
      <importErrorMessage>Cannot import this Web Part.</importErrorMessage>
    </metaData>
    <data>
      <properties>
        <property name=""TitleIconImageUrl"" type=""string"" />
        <property name=""Direction"" type=""direction"">NotSet</property>
        <property name=""ExportMode"" type=""exportmode"">All</property>
        <property name=""HelpUrl"" type=""string"" />
        <property name=""Hidden"" type=""bool"">False</property>
        <property name=""Description"" type=""string"">WelcomeAppPart Description</property>
        <property name=""FeatureId"" type=""System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"">0b846986-3474-4f1a-93cf-b7817ef057f9</property>
        <property name=""CatalogIconImageUrl"" type=""string"" />
        <property name=""Title"" type=""string"">WelcomeAppPart Title</property>
        <property name=""AllowHide"" type=""bool"">True</property>
        <property name=""ProductWebId"" type=""System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"">717c00a1-08ea-41a5-a2b7-4c8f9c1ce770</property>
        <property name=""AllowZoneChange"" type=""bool"">True</property>
        <property name=""TitleUrl"" type=""string"" />
        <property name=""ChromeType"" type=""chrometype"">Default</property>
        <property name=""AllowConnect"" type=""bool"">True</property>
        <property name=""Width"" type=""unit"" />
        <property name=""Height"" type=""unit"" />
        <property name=""WebPartName"" type=""string"">WelcomeAppPart</property>
        <property name=""HelpMode"" type=""helpmode"">Navigate</property>
        <property name=""AllowEdit"" type=""bool"">True</property>
        <property name=""AllowMinimize"" type=""bool"">True</property>
        <property name=""ProductId"" type=""System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"">0b846986-3474-4f1a-93cf-b7817ef057f8</property>
        <property name=""AllowClose"" type=""bool"">True</property>
        <property name=""ChromeState"" type=""chromestate"">Normal</property>
      </properties>
    </data>
  </webPart>
</webParts>";
```

**ReplaceWebPartsWithAppParts** startet das Suchen von Webparts zu ersetzen durch:

1. Abrufen von einige Eigenschaften aus dem [Web](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.aspx) , die Bibliothek für **Seiten** auf der Website zu erhalten.
    
2. Abrufen von in der Bibliothek für **Seiten** Listenelemente und die Datei, die dem Listenelement zugeordnet.
    
3. Aufrufen von **FindWebPartToReplace**für jedes Listenelement aus der Bibliothek für **Seiten** zurückgegeben.

```C#
protected void ReplaceWebPartsWithAppParts(object sender, EventArgs e)
{
    var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
    using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        Web web = clientContext.Web;
        // Get properties from the Web.
        clientContext.Load(web,
                            w => w.ServerRelativeUrl,
                            w => w.AllProperties);
        clientContext.ExecuteQuery();
        // Read the Pages library name from the Web properties.
        var pagesListName = web.AllProperties["__pageslistname"] as string;

        var list = web.Lists.GetByTitle(pagesListName);
        var items = list.GetItems(CamlQuery.CreateAllItemsQuery());
        // Get the file associated with each list item.
        clientContext.Load(items,
                            i => i.Include(
                                    item => item.File));
        clientContext.ExecuteQuery();

        // Iterate through all pages in the Pages list.
        foreach (var item in items)
        {
            FindWebPartForReplacement(item, clientContext, web);
        }
    }
}
```

**FindWebPartToReplace** sucht nach Webparts, die durch das neue Add-in-Teil von ersetzt werden soll:

1. Festlegen von **Seite** auf die Datei mit dem Listenelement aus der Bibliothek für **Seiten** zurückgegeben.
    
2. Verwenden von [LimitedWebPartManager](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.aspx) , um alle Webparts auf einer bestimmten Seite zu erhalten. Der Titel der einzelnen Webparts wird auch im Lambda-Ausdruck zurückgegeben.
    
3. Für jeden Webpart in der Webpart-Manager- [WebParts](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.webparts.aspx) sind Eigentum, bestimmen, ob das Webpart-Titel und die **OldWebPartTitle** -Variable, die auf den Titel des Webparts Sie festgelegt ist ersetzen, gleich. Wenn der Titel des Webparts und **OldWebPartTitle** gleich sind, rufen Sie **ReplaceWebPart**. Anderenfalls fahren Sie mit der nächsten Iteration der **Foreach** -Schleife.

```C#
private static void FindWebPartToReplace(ListItem item, ClientContext clientContext, Web web)
{
    File page = item.File;
    // Requires Full Control permissions on the Web.
    LimitedWebPartManager webPartManager = page.GetLimitedWebPartManager(PersonalizationScope.Shared);
    clientContext.Load(webPartManager,
                        wpm => wpm.WebParts,
                        wpm => wpm.WebParts.Include(
                                            wp => wp.WebPart.Title));
    clientContext.ExecuteQuery();

    foreach (var oldWebPartDefinition in webPartManager.WebParts)
    {
        var oldWebPart = oldWebPartDefinition.WebPart;
        // Modify the Web Part if we find an old Web Part with the same title.
        if (oldWebPart.Title != oldWebPartTitle) continue;

        ReplaceWebPart(web, item, webPartManager, oldWebPartDefinition, clientContext, page);
    }
}
```

**ReplaceWebPart** ersetzt das neue Webpart durch:

1. Verwenden von [LimitedWebPartManager.ImportWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.importwebpart.aspx) , um die XML-Zeichenfolge in **AppPartXml** in einer [WebPartDefinition](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.aspx)zu konvertieren.
    
2. Verwenden von [LimitedWebPartManager.AddWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.addwebpart.aspx) zum Hinzufügen eines Webparts zu einer Seite in einer bestimmten WebPartZone. Stellen Sie sicher, übergeben Sie die **Zonen-ID** an **AddWebPart**, die andernfalls eine Ausnahme wird ausgelöst, wenn **"ExecuteQuery"** ausgeführt wird.
    
3. Verwenden Sie [WebPartDefinition.DeleteWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.deletewebpart.aspx) , um das alte-Webpart auf der Seite löschen.

```C#
private static void ReplaceWebPart(Web web, ListItem item, LimitedWebPartManager webPartManager,
      WebPartDefinition oldWebPartDefinition, ClientContext clientContext, File page)
  {
     
      // Create a Web Part definition using the XML string.
      var definition = webPartManager.ImportWebPart(appPartXml);
      webPartManager.AddWebPart(definition.WebPart, "RightColumn", 0);

      // Delete the old Web Part from the page.
      oldWebPartDefinition.DeleteWebPart();
      clientContext.Load(page,
                          p => p.CheckOutType,
                          p => p.Level);

      clientContext.ExecuteQuery();
     
  }
```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Transformieren von Farmlösungen in das SharePoint-Add-In-Modell](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [Provisioning.Pages](https://github.com/SharePoint/PnP/tree/master/Scenarios/Provisioning.Pages)
