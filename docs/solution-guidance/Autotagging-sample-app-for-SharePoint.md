---
title: "Autotagging Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 79be82cac67ad11921b4c4477e5773efc98396e7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="autotagging-sample-add-in-for-sharepoint"></a><span data-ttu-id="ffb63-102">Autotagging Beispiel-add-in für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ffb63-102">Autotagging sample add-in for SharePoint</span></span>

<span data-ttu-id="ffb63-103">Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie automatisch Markieren von Dokumenten mit Metadaten wenn sie erstellt oder in SharePoint hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="ffb63-103">As part of your Enterprise Content Management (ECM) strategy, you can automatically tag documents with metadata when they are created or uploaded to SharePoint.</span></span> 
    
<span data-ttu-id="ffb63-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="ffb63-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="ffb63-105">Die [ECM. AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) Beispiel zeigt, wie Sie eine vom Anbieter gehosteten add-in, automatisch Inhalt des Tags, einer SharePoint-Bibliothek mit Daten aus einer benutzerdefinierten Benutzerprofileigenschaft stammende hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="ffb63-105">The [ECM.AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) sample shows you how to use a provider-hosted add-in to automatically tag content added to a SharePoint library with data sourced from a custom user profile property.</span></span> <span data-ttu-id="ffb63-106">Dieses Add-in verwendet remote-Ereignisempfänger, gehostet auf einer Azure-Website an:</span><span class="sxs-lookup"><span data-stu-id="ffb63-106">This add-in uses remote event receivers, hosted on an Azure Web Site, to:</span></span>   

- <span data-ttu-id="ffb63-107">Felder, Inhaltstypen und Dokumentbibliotheken zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-107">Create fields, content types, and document libraries.</span></span>
    
- <span data-ttu-id="ffb63-108">Rufen Sie den Wert einer benutzerdefinierten Profileigenschaft.</span><span class="sxs-lookup"><span data-stu-id="ffb63-108">Retrieve the value of a custom user profile property.</span></span>
    
- <span data-ttu-id="ffb63-109">Festlegen Sie Taxonomie Felder.</span><span class="sxs-lookup"><span data-stu-id="ffb63-109">Set taxonomy fields.</span></span>
    
<span data-ttu-id="ffb63-110">Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:</span><span class="sxs-lookup"><span data-stu-id="ffb63-110">Use this solution if you want to:</span></span>

- <span data-ttu-id="ffb63-111">Implementieren von Ereignisempfängern in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="ffb63-111">Implement event receivers in SharePoint Online.</span></span> 
    
- <span data-ttu-id="ffb63-112">Verbessern der Suchergebnisse durch Anfügen von zusätzliche Metadaten zum Inhalt erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="ffb63-112">Improve search results by attaching additional metadata to content when it's created.</span></span>
    
- <span data-ttu-id="ffb63-113">Klassifizieren von Inhalten.</span><span class="sxs-lookup"><span data-stu-id="ffb63-113">Classify your content.</span></span>
    
- <span data-ttu-id="ffb63-114">Modernisieren Code vor der Migration zu einer neueren Version von SharePoint, und Sie in der Vergangenheit Ereignisempfänger verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="ffb63-114">Modernize your code before migrating to a newer version of SharePoint, and you've used event receivers in the past.</span></span>
    
## <a name="before-you-begin"></a><span data-ttu-id="ffb63-115">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="ffb63-115">Before you begin</span></span>
<span data-ttu-id="ffb63-116"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="ffb63-116"></span></span>

<span data-ttu-id="ffb63-117">Laden Sie Sie zunächst die [ECM. AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="ffb63-117">To get started, download the  [ECM.AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="ffb63-118">Vor dem Ausführen dieses Add-in führen Sie die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="ffb63-118">Before you run this add-in , do the following:</span></span>

1. <span data-ttu-id="ffb63-119">Erstellen einer Azure-Website und die ECM bereitstellen. AutoTaggingWeb-Projekt hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffb63-119">Create an Azure Web Site and deploy the ECM.AutoTaggingWeb project to it.</span></span>
    
2. <span data-ttu-id="ffb63-120">Registrieren Sie Ihr Add-in über die Seite "appregnew.aspx" in Office 365.</span><span class="sxs-lookup"><span data-stu-id="ffb63-120">Register your add-in using the Appregnew.aspx page in Office 365.</span></span> 
    
3. <span data-ttu-id="ffb63-121">Dieses Add-In wird nur-app-Berechtigungen verwendet.</span><span class="sxs-lookup"><span data-stu-id="ffb63-121">This add-in uses app-only permissions.</span></span> <span data-ttu-id="ffb63-122">Sie müssen nur-app-Berechtigungen, die über die Seite "appinv.aspx" in Office 365 zuweisen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-122">You need to assign app-only permissions using the AppInv.aspx page in Office 365.</span></span> <span data-ttu-id="ffb63-123">Kopieren Sie den folgenden XML-Code aus der Datei AppManifest.XML in die Berechtigung anfordern XML TextBox-Steuerelement auf der Seite "appinv.aspx", wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="ffb63-123">Copy the following XML from the AppManifest.xml file to the Permission Request XML textbox on the AppInv.aspx page, as shown in Figure 1.</span></span> 

    ``` 
      <AppPermissionRequests AllowAppOnlyPolicy="true">
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
        <AppPermissionRequest Scope="http://sharepoint/taxonomy" Right="Read" />
        <AppPermissionRequest Scope="http://sharepoint/social/tenant" Right="Read" />
      </AppPermissionRequests>
    ```

    <span data-ttu-id="ffb63-124">**Abbildung 1. Zuweisen von nur-app-Berechtigungen mithilfe der Seite "appinv.aspx" in Office 365**</span><span class="sxs-lookup"><span data-stu-id="ffb63-124">**Figure 1. Assigning app-only permissions by using the AppInv.aspx page in Office 365**</span></span>

    ![Screenshot der Seite "appinv.aspx" mit den Feldern App-ID und die Berechtigung anfordern XML hervorgehoben](media/d733e2b0-55f3-4aee-872b-49e7e2baf470.png)

4. <span data-ttu-id="ffb63-126">In der ECM. AutoTaggingWeb-Projekt, in der Datei ReceiverHelper.cs, in der Methode **CreateEventReciever** aktualisieren die **ReceiverUrl** -Eigenschaft mit der URL von der Azure-Website.</span><span class="sxs-lookup"><span data-stu-id="ffb63-126">In the ECM.AutoTaggingWeb project, in the ReceiverHelper.cs file, in the  **CreateEventReciever** method, update the **ReceiverUrl** property with the URL of your Azure Web Site.</span></span>

    ```C#
        public static EventReceiverDefinitionCreationInformation CreateEventReciever(string receiverName, EventReceiverType type)
            {
    
                EventReceiverDefinitionCreationInformation _rer = new EventReceiverDefinitionCreationInformation();
                _rer.EventType = type;
                _rer.ReceiverName = receiverName;
                _rer.ReceiverClass = "ECM.AutoTaggingWeb.Services.AutoTaggingService";
                _rer.ReceiverUrl = "https://<Your domain>.azurewebsites.net/Services/AutoTaggingService.svc";
                _rer.Synchronization = EventReceiverSynchronization.Synchronous;
                return _rer;
            }
    
    ```
5. <span data-ttu-id="ffb63-127">Packen Sie und Bereitstellen Sie Ihrer add-Ins.</span><span class="sxs-lookup"><span data-stu-id="ffb63-127">Package and deploy your add-in .</span></span> 
    
<span data-ttu-id="ffb63-128">Beim Starten Sie das Add-in, die Startseite des Dokuments Autotagging vom Anbieter gehosteten-Add-in angezeigt, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="ffb63-128">When you start the add-in , the start page of the Document Autotagging provider-hosted add-in displays, as shown in Figure 2.</span></span> <span data-ttu-id="ffb63-129">Die Startseite zeigt zusätzliche Konfigurationsschritte, dass Sie vor dem zuweisen oder Entfernen von Ereignisempfängern ausgeführt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-129">The start page shows some additional configuration steps you need to perform before you assign or remove the event receivers.</span></span> 

<span data-ttu-id="ffb63-130">**Abbildung 2. Zusätzliche Konfigurationsschritte erforderlich, um auf der Startseite in SharePoint ausgeführt werden**</span><span class="sxs-lookup"><span data-stu-id="ffb63-130">**Figure 2. Additional configuration steps to be performed on the add-in start page in SharePoint**</span></span>

![Screenshot des Autotagging-add-Ins der Startseite mit drei Einrichtungsschritte hervorgehoben.](media/eb0521b2-11e2-4c57-8026-d7e838c21eae.png)

## <a name="using-the-ecmautotagging-sample-add-in"></a><span data-ttu-id="ffb63-132">Verwenden die ECM. Autotagging Beispiel-add-in</span><span class="sxs-lookup"><span data-stu-id="ffb63-132">Using the ECM.Autotagging sample add-in</span></span> 
<span data-ttu-id="ffb63-133"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="ffb63-133"></span></span>

<span data-ttu-id="ffb63-134">In diesem Beispiel wird einen remote-Ereignisempfänger automatisch Tag (Metadaten hinzufügen) Profileigenschaft Dokumente, die in einer Dokumentbibliothek, mit der Daten von einem benutzerdefinierten Benutzer hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="ffb63-134">This sample uses a remote event receiver to automatically tag (add metadata to) documents that are added to a document library, with data from a custom user profile property.</span></span> <span data-ttu-id="ffb63-135">Der Prozessfluss für Autotagging Dokumente mithilfe des remote-Ereignisempfängers wird in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="ffb63-135">The process flow for autotagging documents using the remote event receiver is shown in Figure 3.</span></span>

<span data-ttu-id="ffb63-136">**Abbildung 3. Prozessfluss zum Markieren von Dokumenten in einer Dokumentbibliothek mithilfe eines remoteereignisempfängers**</span><span class="sxs-lookup"><span data-stu-id="ffb63-136">**Figure 3. Process flow for tagging documents in a document library by using a remote event receiver**</span></span>

![Abbildung des Prozesses zum Markieren von einem Dokument in einer Bibliothek.](media/430eee99-5ab9-49d8-8021-71d7cee79a73.png)

<span data-ttu-id="ffb63-139">Zuweisen von Metadaten für das neu erstellte Dokument in der Dokumentbibliothek mithilfe eines remoteereignisempfängers</span><span class="sxs-lookup"><span data-stu-id="ffb63-139">To assign metadata to the newly created document in the document library by using a remote event receiver:</span></span>

1. <span data-ttu-id="ffb63-140">Ein Benutzer erstellt oder neuen Inhalte in einer Dokumentbibliothek hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-140">A user creates or uploads new content to a document library.</span></span> <span data-ttu-id="ffb63-141">Ein remote-Ereignisempfänger zugeordnet ist, **ItemAdding** oder **ItemAdded** Ereignisse in dieser Dokumentbibliothek behandelt.</span><span class="sxs-lookup"><span data-stu-id="ffb63-141">A remote event receiver is assigned to handle  **ItemAdding** or **ItemAdded** events on this document library.</span></span>
    
2. <span data-ttu-id="ffb63-142">Die **ItemAdding** oder **ItemAdded** -Methode führt einen Aufruf an den Ereignisempfänger entfernen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-142">The  **ItemAdding** or **ItemAdded** method makes a call to the remove event receiver.</span></span>
    
3. <span data-ttu-id="ffb63-143">Das Add-in vom Anbieter gehosteten Ruft den Wert einer benutzerdefinierten Profileigenschaft in der User Profile Service von SharePoint für diesen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="ffb63-143">The provider-hosted add-in fetches the value of a custom user profile property in the User Profile Service of SharePoint for that user.</span></span> <span data-ttu-id="ffb63-144">In diesem Beispiel-add-in wird die Klassifizierung benutzerdefinierte Benutzerprofileigenschaft, die zuvor hinzugefügten abgerufen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-144">In this sample add-in , the Classification custom user profile property that was added previously is retrieved.</span></span>
    
4. <span data-ttu-id="ffb63-145">Der remote-Ereignisempfänger aktualisiert die Metadaten für das neue Dokument mit dem Wert des benutzerdefinierten Benutzerprofileigenschaft für diesen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="ffb63-145">The remote event receiver updates the metadata on the new document with the value of the custom user profile property for that user.</span></span> 

### <a name="run-scenario-1"></a><span data-ttu-id="ffb63-146">Führen Sie Szenario 1</span><span class="sxs-lookup"><span data-stu-id="ffb63-146">Run Scenario 1</span></span>

<span data-ttu-id="ffb63-147">Wenn Sie die Schaltfläche **Führen Sie Szenario 1**geklickt haben, führt das Add-in Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="ffb63-147">When you choose the button  **Run Scenario 1**, the add-in does the following:</span></span>

1. <span data-ttu-id="ffb63-148">Erstellt eine Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="ffb63-148">Creates a document library.</span></span>
    
2. <span data-ttu-id="ffb63-149">Den remote-Ereignisempfänger für das ItemAdding-Ereignis erstellt.</span><span class="sxs-lookup"><span data-stu-id="ffb63-149">Creates the remote event receiver for the ItemAdding event.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ffb63-150">Dieser Artikel beschreibt den Ereignistyp Empfänger ItemAdding.</span><span class="sxs-lookup"><span data-stu-id="ffb63-150">This article discusses the ItemAdding event receiver type.</span></span> <span data-ttu-id="ffb63-151">Im Allgemeinen führt eine höhere Leistung als das ItemAdded-Ereignisempfängertyp der Ereignistyp Empfänger ItemAdding.</span><span class="sxs-lookup"><span data-stu-id="ffb63-151">Generally, the ItemAdding event receiver type performs better than the ItemAdded event receiver type.</span></span> <span data-ttu-id="ffb63-152">Die ECM. Autotagging Beispiel stellt Code für die ItemAdding und die ItemAdded-Ereignis Receiver Typen bereit.</span><span class="sxs-lookup"><span data-stu-id="ffb63-152">The ECM.Autotagging sample provides code for both the ItemAdding and ItemAdded event receiver types.</span></span>

3. <span data-ttu-id="ffb63-153">Fügt den remote-Ereignisempfänger in die Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="ffb63-153">Adds the remote event receiver to the document library.</span></span>
    
<span data-ttu-id="ffb63-154">Der folgende Code in die **btnScenario1_Click** -Methode der Seite "default.aspx.cs" in der ECM. AutoTaggingWeb-Projekt zeigt diese Schritte.</span><span class="sxs-lookup"><span data-stu-id="ffb63-154">The following code, in the  **btnScenario1_Click** method of the Default.aspx.cs page in the ECM.AutoTaggingWeb project, shows these steps.</span></span>

> [!NOTE] 
> <span data-ttu-id="ffb63-155">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="ffb63-155">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
protected void btnScenario1_Click(object sender, EventArgs e)
        {
            var _libraryToCreate = this.GetLibaryInformationItemAdding();
 
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var ctx = spContext.CreateUserClientContextForSPHost())
            {
                try 
                { 
                    if(!ctx.Web.ListExists(_libraryToCreate.Title))
                    {
                        ScenarioHandler _scenario = new ScenarioHandler();
                        _scenario.CreateContosoDocumentLibrary(ctx, _libraryToCreate);
                    }
                    List _list = ctx.Web.Lists.GetByTitle(_libraryToCreate.Title);
                    EventReceiverDefinitionCreationInformation _rec = ReceiverHelper.CreateEventReciever(ScenarioHandler.AUTOTAGGING_ITEM_ADDING_RERNAME, EventReceiverType.ItemAdding);
                    ReceiverHelper.AddEventReceiver(ctx, _list, _rec);
                }
                catch(Exception _ex)
                {

                }
            }
        }  
```

<span data-ttu-id="ffb63-156">Die **CreateContosoDocumentLibrary** -Methode ist aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-156">A call is made to the  **CreateContosoDocumentLibrary** method.</span></span> <span data-ttu-id="ffb63-157">Der folgende Code in der Datei ScenarioHandler.cs werden Methoden von OfficeDevPnP.Core zum Erstellen einer benutzerdefinierten Dokumentbibliothek mit einem benutzerdefinierten Inhaltstyp verwendet.</span><span class="sxs-lookup"><span data-stu-id="ffb63-157">The following code in the ScenarioHandler.cs file uses methods from OfficeDevPnP.Core to create a custom document library with a custom content type.</span></span> <span data-ttu-id="ffb63-158">Der Standard-Inhaltstyp in der Dokumentbibliothek wurde entfernt.</span><span class="sxs-lookup"><span data-stu-id="ffb63-158">The default content type in the document library is removed.</span></span>

```C#
public void CreateContosoDocumentLibrary(ClientContext ctx, Library library)
        {
            // Check the fields.
            if (!ctx.Web.FieldExistsById(FLD_CLASSIFICATION_ID))
            {
                ctx.Web.CreateTaxonomyField(FLD_CLASSIFICATION_ID,
                                            FLD_CLASSIFICATION_INTERNAL_NAME,
                                            FLD_CLASSIFICATION_DISPLAY_NAME,
                                            FIELDS_GROUP_NAME,
                                            TAXONOMY_GROUP,
                                            TAXONOMY_TERMSET_CLASSIFICATION_NAME);
            }

            // Check the content type.
            if (!ctx.Web.ContentTypeExistsById(CONTOSODOCUMENT_CT_ID))
            {
                ctx.Web.CreateContentType(CONTOSODOCUMENT_CT_NAME,
                                          CT_DESC, CONTOSODOCUMENT_CT_ID,
                                          CT_GROUP);
            }

            // Associate fields to content types.
            if (!ctx.Web.FieldExistsByNameInContentType(CONTOSODOCUMENT_CT_NAME, FLD_CLASSIFICATION_INTERNAL_NAME))
            {
                ctx.Web.AddFieldToContentTypeById(CONTOSODOCUMENT_CT_ID,
                                                  FLD_CLASSIFICATION_ID.ToString(),
                                                  false);
            }

            
            CreateLibrary(ctx, library, CONTOSODOCUMENT_CT_ID);
        }

private void CreateLibrary(ClientContext ctx, Library library, string associateContentTypeID)
        {
            if (!ctx.Web.ListExists(library.Title))
            {
                ctx.Web.AddList(ListTemplateType.DocumentLibrary, library.Title, false);
                List _list = ctx.Web.GetListByTitle(library.Title);
                if (!string.IsNullOrEmpty(library.Description))
                {
                    _list.Description = library.Description;
                }

                if (library.VerisioningEnabled)
                {
                    _list.EnableVersioning = true;
                }

                _list.ContentTypesEnabled = true;
                _list.RemoveContentTypeByName("Document");
                _list.Update();
                
     
                ctx.Web.AddContentTypeToListById(library.Title, associateContentTypeID, true);
                ctx.Web.Context.ExecuteQuery();
               
            }
            else
            {
                throw new Exception("A list, survey, discussion board, or document library with the specified title already exists in this Web site.  Please choose another title.");
            }
        }
```

<span data-ttu-id="ffb63-159">Nach Ausführung dieses Codes wird die Dokumentbibliothek AutoTaggingSampleItemAdding in Websiteinhalte, erstellt, wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="ffb63-159">After this code runs, the AutoTaggingSampleItemAdding document library is created in Site Contents, as shown in Figure 4.</span></span>

<span data-ttu-id="ffb63-160">**Abbildung 4. AutoTaggingSampleItemAdding-Dokumentbibliothek**</span><span class="sxs-lookup"><span data-stu-id="ffb63-160">**Figure 4. AutoTaggingSampleItemAdding document library**</span></span>

![Screenshot Shwoing der Seite Websiteinhalte mit der neuen AutoTaggingSampleItemAdd-Dokumentbibliothek.](media/8820a44f-8df8-4c80-aeaa-e50c37b8912c.png)

<span data-ttu-id="ffb63-162">In der ECM. AutoTaggingWeb-Projekt erstellt die ItemAdding-ereignisempfängerdefinition in der Datei ReceiverHelper.cs, die **CreateEventReciever** -Methode.</span><span class="sxs-lookup"><span data-stu-id="ffb63-162">In the ECM.AutoTaggingWeb project, in the ReceiverHelper.cs file, the  **CreateEventReciever** method creates the ItemAdding event receiver definition.</span></span> <span data-ttu-id="ffb63-163">In der ECM. AutoTaggingWeb-Projekt, der Ordner Services enthält einen Webdienst mit dem Namen AutoTaggingService.svc.</span><span class="sxs-lookup"><span data-stu-id="ffb63-163">In the ECM.AutoTaggingWeb project, the Services folder includes a web service called AutoTaggingService.svc.</span></span> <span data-ttu-id="ffb63-164">Wenn Sie die ECM veröffentlicht haben. AutoTaggingWeb Projekt zu Ihrer Azure-Website, diesen Webdienst wurde auch auf Ihrer Website bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="ffb63-164">When you published the ECM.AutoTaggingWeb project to your Azure Web Site, this web service was also deployed to your site.</span></span> <span data-ttu-id="ffb63-165">Die **CreateEventReciever** -Methode weist diesen Webdienst als der remote-Ereignisempfänger in der Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="ffb63-165">The **CreateEventReciever** method assigns this web service as the remote event receiver on the document library.</span></span> <span data-ttu-id="ffb63-166">Der folgende Code aus der **CreateEventReciever** -Methode veranschaulicht, wie der remote-Ereignisempfänger den Webdienst zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-166">The following code from the **CreateEventReciever** method shows how to assign the web service to the remote event receiver.</span></span>

```C#
public static EventReceiverDefinitionCreationInformation CreateEventReciever(string receiverName, EventReceiverType type)
        {

            EventReceiverDefinitionCreationInformation _rer = new EventReceiverDefinitionCreationInformation();
            _rer.EventType = type;
            _rer.ReceiverName = receiverName;
            _rer.ReceiverClass = "ECM.AutoTaggingWeb.Services.AutoTaggingService";
            _rer.ReceiverUrl = "https://<Your domain>.azurewebsites.net/Services/AutoTaggingService.svc";
            _rer.Synchronization = EventReceiverSynchronization.Synchronous;
            return _rer;
        }

```

<span data-ttu-id="ffb63-167">Der folgende Code aus der **AddEventReceiver** -Methode weist den remote-Ereignisempfänger zu der Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="ffb63-167">The following code from the  **AddEventReceiver** method assigns the remote event receiver to the document library.</span></span>

```C#
public static void AddEventReceiver(ClientContext ctx, List list, EventReceiverDefinitionCreationInformation eventReceiverInfo)
        {
            if (!DoesEventReceiverExistByName(ctx, list, eventReceiverInfo.ReceiverName))
            {
                list.EventReceivers.Add(eventReceiverInfo);
                ctx.ExecuteQuery();
            }
        }

```

<span data-ttu-id="ffb63-168">Der remote-Ereignisempfänger wird jetzt in die Dokumentbibliothek hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="ffb63-168">Now, the remote event receiver is added to the document library.</span></span> <span data-ttu-id="ffb63-169">Wenn Sie ein Dokument zur Dokumentbibliothek **AutoTaggingSampleItemAdding** hochladen, das Dokument mit dem Wert der Klassifizierung benutzerdefinierte Profileigenschaft für diesen Benutzer gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="ffb63-169">When you upload a document to the  **AutoTaggingSampleItemAdding** document library, the document will be tagged with the value of the Classification custom user profile property for that user.</span></span> <span data-ttu-id="ffb63-170">Abbildung 5 veranschaulicht, wie die Eigenschaften in einem Dokument anzeigen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-170">Figure 5 shows how to view the properties on a document.</span></span> <span data-ttu-id="ffb63-171">Abbildung 6 zeigt das Dokument Metadaten, bei denen das Feld Klassifikation.</span><span class="sxs-lookup"><span data-stu-id="ffb63-171">Figure 6 shows the document's metadata with the Classification field.</span></span>


<span data-ttu-id="ffb63-172">**Abbildung 5. Anzeigen von Dokumenteigenschaften**</span><span class="sxs-lookup"><span data-stu-id="ffb63-172">**Figure 5. Viewing document properties**</span></span>

<span data-ttu-id="ffb63-173">![Screenshot eines Dokuments in der Bibliothek mit den Eigenschaften Test erweitert. ](media/991dc064-1855-4897-a012-c56c0079131e.png)
 **Abbildung 6. Feld Klassifikation in die Dokumentmetadaten**</span><span class="sxs-lookup"><span data-stu-id="ffb63-173">![Screenshot of a test document in the library with the properties expanded.](media/991dc064-1855-4897-a012-c56c0079131e.png)
**Figure 6. Classification field in the document metadata**</span></span>

![Screenshot, der die Metadaten des Dokuments Test mit HBI in das Feld Klassifikation zeigt.](media/9dc5be77-70b3-400a-a636-f5fc2face335.png)

<span data-ttu-id="ffb63-175">Die **HandleAutoTaggingItemAdding** -Methode verwendet in der Datei AutoTaggingService.svc.cs die **GetProfilePropertyFor** -Methode zum Abrufen des Werts der Benutzerprofileigenschaft Klassifikation.</span><span class="sxs-lookup"><span data-stu-id="ffb63-175">The  **HandleAutoTaggingItemAdding** method, in the AutoTaggingService.svc.cs file, uses the **GetProfilePropertyFor** method to retrieve the value of the Classification user profile property.</span></span>

```C#
public void HandleAutoTaggingItemAdding(SPRemoteEventProperties properties,SPRemoteEventResult result)
        {
            using (ClientContext ctx = TokenHelper.CreateRemoteEventReceiverClientContext(properties))
            {
                if (ctx != null)
                {
                    var itemProperties = properties.ItemEventProperties;
                    var _userLoginName = properties.ItemEventProperties.UserLoginName;
                    var _afterProperites = itemProperties.AfterProperties;
                    if(!_afterProperites.ContainsKey(ScenarioHandler.FLD_CLASSIFICATION_INTERNAL_NAME))
                    {
                        string _classficationToSet = ProfileHelper.GetProfilePropertyFor(ctx, _userLoginName, Constants.UPA_CLASSIFICATION_PROPERTY);
                        if(!string.IsNullOrEmpty(_classficationToSet))
                        { 
                            var _formatTaxonomy = AutoTaggingHelper.GetTaxonomyFormat(ctx, _classficationToSet);
                            result.ChangedItemProperties.Add(ScenarioHandler.FLD_CLASSIFICATION_INTERNAL_NAME, _formatTaxonomy);
                        }
                    }
                }
            }
        }

```
    
<span data-ttu-id="ffb63-176">**Wichtige**  Nach dem Abrufen des **Klassifizierung** Werts aus der **GetProfilePropertyFor** -Methode, muss der **Klassifizierung** Wert auf eine bestimmte Weise formatiert werden, bevor sie als Metadaten für das Dokument gespeichert werden können.</span><span class="sxs-lookup"><span data-stu-id="ffb63-176">**Important**  After retrieving the  **Classification** value from the **GetProfilePropertyFor** method, the **Classification** value must be formatted in a certain way before it can be stored as metadata on the document.</span></span> <span data-ttu-id="ffb63-177">Die **GetTaxonomyFormat** -Methode in der Datei AutoTaggingHelper.cs zeigt, wie zum Formatieren des Werts **Klassifikation** .</span><span class="sxs-lookup"><span data-stu-id="ffb63-177">The **GetTaxonomyFormat** method in the AutoTaggingHelper.cs file shows how to format the **Classification** value.</span></span>

```C#
public static string GetTaxonomyFormat(ClientContext ctx, string term)
        { 
            if(string.IsNullOrEmpty(term))
            {
                throw new ArgumentException(string.Format(EXCEPTION_MSG_INVALID_ARG, "term"));
            }
            string _result = string.Empty;
            var _list = ctx.Web.Lists.GetByTitle(TAXONOMY_HIDDEN_LIST_NAME);
            CamlQuery _caml = new CamlQuery();

            _caml.ViewXml = string.Format(TAXONOMY_CAML_QRY, term);
            var _listItemCollection = _list.GetItems(_caml);

            ctx.Load(_listItemCollection,
                eachItem => eachItem.Include(
                    item => item,
                    item => item.Id,
                    item => item[TAXONOMY_FIELDS_IDFORTERM]));
            ctx.ExecuteQuery();

            if (_listItemCollection.Count > 0)
            {
                var _item = _listItemCollection.FirstOrDefault();
                var _wssId = _item.Id;
                var _termId = _item[TAXONOMY_FIELDS_IDFORTERM].ToString(); ;
                _result = string.Format(TAXONOMY_FORMATED_STRING, _wssId, term, _termId);
            }

            return _result;
        }

```

### <a name="remove-event-scenario-1"></a><span data-ttu-id="ffb63-178">Szenario 1 entfernen</span><span class="sxs-lookup"><span data-stu-id="ffb63-178">Remove Event Scenario 1</span></span>

<span data-ttu-id="ffb63-179">Wenn Sie die Schaltfläche **Entfernen Ereignis Szenario 1**geklickt haben, führt der folgende Code, um den Ereignisempfänger aus der Dokumentbibliothek zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="ffb63-179">When you choose the button  **Remove Event Scenario 1**, the following code runs to remove the event receiver from the document library.</span></span>

```C#
public static void RemoveEventReceiver(ClientContext ctx, List list, string receiverName)
        {
            ctx.Load(list, lib => lib.EventReceivers);
            ctx.ExecuteQuery();

            var _rer = list.EventReceivers.Where(e => e.ReceiverName == receiverName).FirstOrDefault();
            if(_rer != null)
            {
                _rer.DeleteObject();
                ctx.ExecuteQuery();
            }
        }

```

## <a name="see-also"></a><span data-ttu-id="ffb63-180">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ffb63-180">See also</span></span>
<span data-ttu-id="ffb63-181"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ffb63-181"></span></span>

-  [<span data-ttu-id="ffb63-182">Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="ffb63-182">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="ffb63-183">OfficeDevPnP.Core-Beispiel</span><span class="sxs-lookup"><span data-stu-id="ffb63-183">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
