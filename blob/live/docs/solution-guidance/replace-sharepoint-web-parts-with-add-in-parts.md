---
title: Ersetzen Sie SharePoint-Webparts mit Add-in-Webparts
ms.date: 11/03/2017
ms.openlocfilehash: 3c65234be92b9757f3ed0894e0e8e7d11b6a2187
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="replace-sharepoint-web-parts-with-add-in-parts"></a><span data-ttu-id="bf741-102">Ersetzen Sie SharePoint-Webparts mit Add-in-Webparts</span><span class="sxs-lookup"><span data-stu-id="bf741-102">Replace SharePoint Web Parts with add-in parts</span></span>

<span data-ttu-id="bf741-103">Verwenden des Transformationsprozess Webparts mithilfe des SharePoint-Clientobjektmodells (CSOM) mit Add-in-Webparts zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="bf741-103">Use the transformation process to replace Web Parts with add-in parts by using the SharePoint client object model (CSOM).</span></span>

<span data-ttu-id="bf741-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="bf741-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="bf741-105">Den Transformationsprozess können SharePoint-Webparts mit Add-in-Webparts auf Seiten durch das Verwenden von CSOM zum Suchen und Entfernen von bestimmten Webparts, und fügen Sie dann das neue Add-in-Teile ersetzt.</span><span class="sxs-lookup"><span data-stu-id="bf741-105">You can use the transformation process to replace SharePoint Web Parts with add-in parts on pages by using CSOM to find and remove specific Web Parts, and then adding the new add-in parts.</span></span>

<span data-ttu-id="bf741-106">**Wichtig:**  Farmlösungen können nicht mit SharePoint Online migriert werden.</span><span class="sxs-lookup"><span data-stu-id="bf741-106">**Important:**  Farm solutions cannot be migrated to SharePoint Online.</span></span> <span data-ttu-id="bf741-107">Durch die Techniken und den Code in diesem Artikel beschriebenen anwenden, können Sie einer neuen Lösung mit ähnlicher Funktionalität erstellen, dass Ihre farmlösungen zu ermöglichen, können in SharePoint Online bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="bf741-107">By applying the techniques and code described in this article, you can build a new solution with similar functionality that your farm solutions provide, which can then be deployed to SharePoint Online.</span></span> <span data-ttu-id="bf741-108">Nachdem Sie diese Verfahren anwenden, werden Ihre Seiten-add-in Webparts verwenden, klicken Sie dann auf SharePoint Online migriert werden können aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="bf741-108">After you apply these techniques, your pages will be updated to use add-in parts, which can then be migrated to SharePoint Online.</span></span> <span data-ttu-id="bf741-109">Der Code in diesem Artikel erfordert zusätzlichen Code, um eine voll funktionsfähige Lösung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="bf741-109">The code in this article requires additional code to provide a fully working solution.</span></span> <span data-ttu-id="bf741-110">In diesem Artikel erläutern beispielsweise nicht Anleitung zu Office 365, authentifizieren Implementierung Ausnahmebehandlung erforderlich, und so weiter.</span><span class="sxs-lookup"><span data-stu-id="bf741-110">For example, this article does not discuss how to authenticate to Office 365, how to implement required exception handling, and so on.</span></span> <span data-ttu-id="bf741-111">Zusätzliche Codebeispiele finden Sie unter [Office 365 Developer Mustern und Methoden Projekt](https://github.com/SharePoint/PnP).</span><span class="sxs-lookup"><span data-stu-id="bf741-111">For additional code samples, see the [Office 365 Developer Patterns and Practices project](https://github.com/SharePoint/PnP).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bf741-112">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="bf741-112">Before you begin</span></span>

<span data-ttu-id="bf741-113">Stellen Sie vor dem Ausführen der Schritte in diesem Artikel, um Ihre Webparts mit Add-in-Teile ersetzen sicher, dass Sie:</span><span class="sxs-lookup"><span data-stu-id="bf741-113">Before performing the steps in this article to replace your Web Parts with add-in parts, make sure that you:</span></span>

- <span data-ttu-id="bf741-114">Verwenden eine SharePoint-Umgebung, die so konfiguriert ist, zur Unterstützung von add-ins SharePoint Online ist so konfiguriert, dass-add-ins zu unterstützen. Wenn Sie SharePoint Server 2013 lokal verwenden, finden Sie unter [Konfigurieren einer Umgebung für SharePoint-Add-ins (SharePoint 2013)](https://technet.microsoft.com/library/fp161236%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="bf741-114">Are using a SharePoint environment that is configured to support add-ins. SharePoint Online is configured to support add-ins. If you are using SharePoint Server 2013 on-premises, see [Configure an environment for SharePoint Add-ins (SharePoint 2013)](https://technet.microsoft.com/library/fp161236%28v=office.15%29).</span></span>
    
- <span data-ttu-id="bf741-115">Das neue Add-in-Teil haben in SharePoint bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="bf741-115">Have deployed your new add-in part to SharePoint.</span></span>
    
- <span data-ttu-id="bf741-116">Haben Ihre-add-ins **Vollzugriff** -Berechtigungen auf dem **Web**zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="bf741-116">Have assigned your add-ins  **FullControl** permissions on the **Web**.</span></span> <span data-ttu-id="bf741-117">Weitere Informationen finden Sie unter [Add-in-Berechtigungen in SharePoint 2013](https://msdn.microsoft.com/library/office/fp142383.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf741-117">For more information, see [Add-in permissions in SharePoint 2013](https://msdn.microsoft.com/library/office/fp142383.aspx).</span></span>

## <a name="replace-web-parts-with-add-in-parts"></a><span data-ttu-id="bf741-118">Ersetzen Sie die Webparts durch Add-in-Webparts</span><span class="sxs-lookup"><span data-stu-id="bf741-118">Replace Web Parts with add-in parts</span></span>

<span data-ttu-id="bf741-119">So ersetzen die Webparts durch neue Add-in-Teile:</span><span class="sxs-lookup"><span data-stu-id="bf741-119">To replace Web Parts with new add-in parts:</span></span>

1. <span data-ttu-id="bf741-120">Exportieren Sie das neue Add-in-Teil.</span><span class="sxs-lookup"><span data-stu-id="bf741-120">Export the new add-in part.</span></span> <span data-ttu-id="bf741-121">Verwenden Sie das exportierte Webpart-Add-in, um die Webpart-Add-in-Definition abzurufen.</span><span class="sxs-lookup"><span data-stu-id="bf741-121">Use the exported add-in part to get the add-in part definition.</span></span> 
    
2. <span data-ttu-id="bf741-122">Suchen Sie nach allen Seiten mit Webparts ausgetauscht werden, und entfernen Sie die Webparts.</span><span class="sxs-lookup"><span data-stu-id="bf741-122">Find all pages with Web Parts to be replaced, and then remove the Web Parts.</span></span> 
    
3. <span data-ttu-id="bf741-123">Erstellen des neuen Teils-Add-in auf der Seite mithilfe der Webpart-Add-in-Definition.</span><span class="sxs-lookup"><span data-stu-id="bf741-123">Create the new add-in part on the page by using the add-in part definition.</span></span> 
    
<span data-ttu-id="bf741-124">CSOM mithilfe um eines Webparts mit einem Webpart-Add-in zu ersetzen, müssen Sie die Webpart-Add-in-Definition durch Exportieren das Webpart-Add-Ins erhalten möchten.</span><span class="sxs-lookup"><span data-stu-id="bf741-124">To use CSOM to replace a Web Part with an add-in part, you need to get the add-in part definition by exporting the add-in part.</span></span> <span data-ttu-id="bf741-125">So exportieren Sie das Webpart-Add-in, um das Add-in-Webpart Definition abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="bf741-125">To export the add-in part to get the add-in part's definition:</span></span>

1. <span data-ttu-id="bf741-126">Öffnen Sie der SharePoint-Website und wählen Sie **Einstellungen**oder das Zahnradsymbol, und wählen Sie dann auf **Seite bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="bf741-126">Open your SharePoint site and choose  **Settings**, or the gear icon, and then choose  **Edit page**.</span></span>
    
2. <span data-ttu-id="bf741-127">Wählen Sie auf dem Menüband **Einfügen** > **Webpart-Add-in**.</span><span class="sxs-lookup"><span data-stu-id="bf741-127">On the ribbon, choose  **INSERT** > **Add-in Part**.</span></span>
    
3. <span data-ttu-id="bf741-128">Wählen Sie den Webpart-add-in, und wählen Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="bf741-128">Choose your add-in part, and then choose  **Add**.</span></span>
    
4. <span data-ttu-id="bf741-129">Wenn das Webpart-Add-in auf der Seite hinzugefügt wird, wählen Sie den Pfeil nach unten in der oberen rechten Ecke des Webparts-Add-in, und wählen Sie dann auf **Webpart bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="bf741-129">When the add-in part is added to your page, choose the down arrow in the top-right corner of the add-in part, and then choose  **Edit Web Part**.</span></span>
    
5. <span data-ttu-id="bf741-130">Im Dialogfeld **Erweitert**im **Modus exportieren** wählen Sie **alle Daten exportieren**, und wählen Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf741-130">In  **Advanced**, in  **Export Mode** choose **Export all data**, and then choose  **OK**.</span></span>
    
6. <span data-ttu-id="bf741-131">Wenn Sie die Seite bearbeiten mit der Webpart-Add-in angezeigt zurückkehren, wählen Sie den Pfeil nach unten in der oberen rechten Ecke des Webparts-Add-in, und wählen Sie dann auf **Exportieren**.</span><span class="sxs-lookup"><span data-stu-id="bf741-131">When you return to the edit page with your add-in part displayed, choose the down arrow in the top-right corner of the add-in part, and then choose  **Export**.</span></span>
    
7. <span data-ttu-id="bf741-132">Wählen Sie **Speichern**aus.</span><span class="sxs-lookup"><span data-stu-id="bf741-132">Choose  **Save**.</span></span>
    
8. <span data-ttu-id="bf741-133">Nachdem der Download abgeschlossen ist, wählen Sie **Ordner öffnen**.</span><span class="sxs-lookup"><span data-stu-id="bf741-133">After the download completes, choose  **Open folder**.</span></span>
    
9. <span data-ttu-id="bf741-134">Öffnen Sie **Editor**, und wählen Sie **Datei** > **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="bf741-134">Open  **Notepad**, then choose  **File** > **Open**.</span></span>
    
10. <span data-ttu-id="bf741-135">Wählen Sie die Add-in-Webpart-Datei, die Sie heruntergeladen haben, und wählen Sie dann die Webpart-Add-in-Definition anzeigen **Öffnen** .</span><span class="sxs-lookup"><span data-stu-id="bf741-135">Choose the add-in part file that you downloaded, and then choose  **Open** to view the add-in part definition.</span></span>
    
<span data-ttu-id="bf741-136">**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="bf741-136">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="bf741-137">So verwenden Sie die Webpart-Add-in-Definition in Ihrem Code CSOM</span><span class="sxs-lookup"><span data-stu-id="bf741-137">To use the add-in part definition in your CSOM code:</span></span>

- <span data-ttu-id="bf741-138">Ersetzen Sie alle doppelte Anführungszeichen (") mit zwei doppelte Anführungszeichen (" ") in der Definition der Webpart-Add-in.</span><span class="sxs-lookup"><span data-stu-id="bf741-138">Replace all double quotes (") with a pair of double quotes ("") in the add-in part definition.</span></span>
    
- <span data-ttu-id="bf741-139">Weisen Sie die Definition der Webpart-Add-in eine Zeichenfolge, die in Ihrem CSOM-Code verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="bf741-139">Assign the add-in part definition to a string that will be used in your CSOM code.</span></span>

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

<span data-ttu-id="bf741-140">**ReplaceWebPartsWithAppParts** startet das Suchen von Webparts zu ersetzen durch:</span><span class="sxs-lookup"><span data-stu-id="bf741-140">**ReplaceWebPartsWithAppParts** starts the process of finding the Web Parts to be replaced by:</span></span>

1. <span data-ttu-id="bf741-141">Abrufen von einige Eigenschaften aus dem [Web](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.aspx) , die Bibliothek für **Seiten** auf der Website zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="bf741-141">Getting some properties from the [Web](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.aspx) to find the **Pages** library on the site.</span></span>
    
2. <span data-ttu-id="bf741-142">Abrufen von in der Bibliothek für **Seiten** Listenelemente und die Datei, die dem Listenelement zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="bf741-142">In the  **Pages** library, getting the list items and the file associated with the list item.</span></span>
    
3. <span data-ttu-id="bf741-143">Aufrufen von **FindWebPartToReplace**für jedes Listenelement aus der Bibliothek für **Seiten** zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="bf741-143">For each list item returned from the  **Pages** library, calling **FindWebPartToReplace**.</span></span>

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

<span data-ttu-id="bf741-144">**FindWebPartToReplace** sucht nach Webparts, die durch das neue Add-in-Teil von ersetzt werden soll:</span><span class="sxs-lookup"><span data-stu-id="bf741-144">**FindWebPartToReplace** finds Web Parts that should be replaced with the new add-in part by:</span></span>

1. <span data-ttu-id="bf741-145">Festlegen von **Seite** auf die Datei mit dem Listenelement aus der Bibliothek für **Seiten** zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="bf741-145">Setting  **page** to the file associated with the list item returned from the **Pages** library.</span></span>
    
2. <span data-ttu-id="bf741-146">Verwenden von [LimitedWebPartManager](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.aspx) , um alle Webparts auf einer bestimmten Seite zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="bf741-146">Using [LimitedWebPartManager](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.aspx) to find all Web Parts on a specific page.</span></span> <span data-ttu-id="bf741-147">Der Titel der einzelnen Webparts wird auch im Lambda-Ausdruck zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="bf741-147">The title of each Web Part is also returned in the lambda expression.</span></span>
    
3. <span data-ttu-id="bf741-148">Für jeden Webpart in der Webpart-Manager- [WebParts](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.webparts.aspx) sind Eigentum, bestimmen, ob das Webpart-Titel und die **OldWebPartTitle** -Variable, die auf den Titel des Webparts Sie festgelegt ist ersetzen, gleich.</span><span class="sxs-lookup"><span data-stu-id="bf741-148">For each Web Part in the Web Part manager's [WebParts](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.webparts.aspx) property, determining whether the Web Part's title and the **oldWebPartTitle** variable, which is set to the title of the Web Part you are replacing, are equal.</span></span> <span data-ttu-id="bf741-149">Wenn der Titel des Webparts und **OldWebPartTitle** gleich sind, rufen Sie **ReplaceWebPart**. Anderenfalls fahren Sie mit der nächsten Iteration der **Foreach** -Schleife.</span><span class="sxs-lookup"><span data-stu-id="bf741-149">If the Web Part title and **oldWebPartTitle** are equal, call **ReplaceWebPart**; otherwise continue with the next iteration of the **foreach** loop.</span></span>

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

<span data-ttu-id="bf741-150">**ReplaceWebPart** ersetzt das neue Webpart durch:</span><span class="sxs-lookup"><span data-stu-id="bf741-150">**ReplaceWebPart** replaces the new Web Part by:</span></span>

1. <span data-ttu-id="bf741-151">Verwenden von [LimitedWebPartManager.ImportWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.importwebpart.aspx) , um die XML-Zeichenfolge in **AppPartXml** in einer [WebPartDefinition](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.aspx)zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="bf741-151">Using [LimitedWebPartManager.ImportWebPart ](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.importwebpart.aspx) to convert the XML string in **appPartXml** into a [WebPartDefinition](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.aspx).</span></span>
    
2. <span data-ttu-id="bf741-152">Verwenden von [LimitedWebPartManager.AddWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.addwebpart.aspx) zum Hinzufügen eines Webparts zu einer Seite in einer bestimmten WebPartZone.</span><span class="sxs-lookup"><span data-stu-id="bf741-152">Using [LimitedWebPartManager.AddWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.addwebpart.aspx) to add a Web Part to a page in a specific Web Part zone.</span></span> <span data-ttu-id="bf741-153">Stellen Sie sicher, übergeben Sie die **Zonen-ID** an **AddWebPart**, die andernfalls eine Ausnahme wird ausgelöst, wenn **"ExecuteQuery"** ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="bf741-153">Ensure you pass the **zoneId** to **AddWebPart**, otherwise an exception will be thrown when  **ExecuteQuery** runs.</span></span>
    
3. <span data-ttu-id="bf741-154">Verwenden Sie [WebPartDefinition.DeleteWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.deletewebpart.aspx) , um das alte-Webpart auf der Seite löschen.</span><span class="sxs-lookup"><span data-stu-id="bf741-154">Using [WebPartDefinition.DeleteWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.deletewebpart.aspx) to delete the old Web Part from the page.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="bf741-155">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="bf741-155">Additional resources</span></span>
<span data-ttu-id="bf741-156"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bf741-156"></span></span>

- [<span data-ttu-id="bf741-157">Transformieren von Farmlösungen in das SharePoint-Add-In-Modell</span><span class="sxs-lookup"><span data-stu-id="bf741-157">Transform farm solutions to the SharePoint add-in model</span></span>](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [<span data-ttu-id="bf741-158">Provisioning.Pages</span><span class="sxs-lookup"><span data-stu-id="bf741-158">Provisioning.Pages</span></span>](https://github.com/SharePoint/PnP/tree/master/Scenarios/Provisioning.Pages)
