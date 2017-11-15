---
title: Vorgehensweise Konvertieren ein Add-in-bezogenen externes Inhaltstyps in mandantenbereichsbezogenen
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 35c5d670-e402-4641-b3c5-6f61ae1ec69b
ms.openlocfilehash: 2e52c54b30f2e22017682edb01d1d00fefd90359
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-convert-an-add-in-scoped-external-content-type-to-tenant-scoped"></a><span data-ttu-id="da262-102">Vorgehensweise: Konvertieren ein Add-in-bezogenen externes Inhaltstyps in mandantenbereichsbezogenen</span><span class="sxs-lookup"><span data-stu-id="da262-102">How to: Convert an add-in-scoped external content type to tenant-scoped</span></span>
<span data-ttu-id="da262-p101">Informationen Sie zum Erstellen eines OData-basierten externen Inhaltstyps mithilfe von Visual Studio 2012 automatische Generierung Tools und importieren es in die Business Connectivity Services (BCS)-Metadaten gespeichert, damit sie über eine gesamte Mandanten Workspace verwendet werden kann. BDC-Modelle werden komplexe XML-Definitionen von einer externen Datenquelle. Sie werden beim Definieren der externer Inhaltstypen für BCS verwendet. Sie sind sehr schwer zu manuell erstellen, damit Tools erstellt wurden, wenn die Dateien mit Visual Studio 2012 und Office Developer Tools für Visual Studio 2012 automatisch generiert werden soll. Verwendung dieser Tools, können Sie ein App-Paket mit Visual Studio-Veröffentlichung erstellen, und öffnen Sie das Paket zum Extrahieren der Modelldatei.</span><span class="sxs-lookup"><span data-stu-id="da262-p101">Learn how to create an OData-based external content type using Visual Studio 2012 auto-generation tools and import it into the Business Connectivity Services (BCS) metadata store so that it can be used across an entire tenant workspace. BDC models are complex XML definitions of an external data source. They are used when defining external content types for BCS. They are very difficult to build manually, so tools have been built to automatically generate the files using Visual Studio 2012 and Office Developer Tools for Visual Studio 2012. Using these tools, you can create an .app package using Visual Studio publishing, and then open that package to extract the model file.</span></span>
  
    
    


## <a name="extract-the-bdc-model-file-from-a-visual-studio-add-in-package"></a><span data-ttu-id="da262-108">Extrahieren Sie die BDC-Modelldatei aus einem Visual Studio-add-in-Paket</span><span class="sxs-lookup"><span data-stu-id="da262-108">Extract the BDC model file from a Visual Studio add-in package</span></span>

<span data-ttu-id="da262-109">Die folgenden Schritte zeigen, wie den OData-basierten externen Inhaltstyp erstellen und dann in den BCS-Metadatenspeicher importieren, so, dass sie über eine gesamte Mandanten Arbeitsbereich verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="da262-109">The following steps show you how to create the OData-based external content type and then import it into the BCS metadata store so that it can be used across an entire tenant workspace.</span></span>
  
    
    

### <a name="to-create-a-bdc-model-file-from-an-odata-source"></a><span data-ttu-id="da262-110">Erstellen Sie eine BDC-Modelldatei aus einer OData-Quelle</span><span class="sxs-lookup"><span data-stu-id="da262-110">To create a BDC model file from an OData source</span></span>


1. <span data-ttu-id="da262-111">Erstellen Sie in Visual Studio 2012 ein Projekt **-Add-in für SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="da262-111">In Visual Studio 2012, create an **Add-in for SharePoint** project.</span></span>
    
  
2. <span data-ttu-id="da262-p102">Geben Sie die Add-in-Einstellungen, einschließlich der Add-in-Name die URL der Website für das Debuggen des Add-Ins und wie Sie das Add-in ( **automatisch gehostete**, **vom Anbieter gehostete** oder **SharePoint-Hosting** ) hosten möchten. Weitere Informationen finden Sie unter [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="da262-p102">Specify the add-in settings, including add-in name, the site URL for debugging the add-in, and how you want to host the add-in ( **Autohosted**, **Provider-hosted**, or **SharePoint-hosted**). For more information, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span></span>
    
  
3. <span data-ttu-id="da262-114">Wählen Sie auf **Fertig stellen**, um die app zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="da262-114">Choose **Finish** to create the app.</span></span>
    
  
4. <span data-ttu-id="da262-115">Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.</span><span class="sxs-lookup"><span data-stu-id="da262-115">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
    <span data-ttu-id="da262-116">Einen Assistenten, der können Sie die ausgewählten Datenquelle suchen und erstellen Sie das BDC-Modell, wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="da262-116">This starts a wizard that helps you find the selected data source and create the BDC model.</span></span>
    
  
5. <span data-ttu-id="da262-p103">Geben Sie auf der Seite **Set OData Source** die URL des OData-Diensts, die Sie mit verbinden möchten. Die URL sollte etwa wie folgt aussehen: `http://services.odata.org/Northwind/Northwind.svc/`.</span><span class="sxs-lookup"><span data-stu-id="da262-p103">On the **Set OData Source** page, enter the URL of the OData service that you want to connect to. The URL should look something like this: `http://services.odata.org/Northwind/Northwind.svc/`.</span></span>
    
    <span data-ttu-id="da262-119">Geben Sie einen Namen für die OData-Quelle an.</span><span class="sxs-lookup"><span data-stu-id="da262-119">Specify a name for your OData source.</span></span>
    
    > <span data-ttu-id="da262-120">**Hinweis:** In diesem Beispiel verwenden Sie den Northwind-Dienst, der in der Hersteller-Liste auf der  [OpenData Protocol-Website](http://www.odata.org) befindet.</span><span class="sxs-lookup"><span data-stu-id="da262-120">**Note** For this example, you will use the Northwind service that is available from the producers list located on the  [Open Data Protocol website](http://www.odata.org).</span></span> 
6. <span data-ttu-id="da262-p104">Eine Liste wird angezeigt, mit Datenentitäten, die vom OData Service verfügbar gemacht werden. Wählen Sie eine oder mehrere Entitäten, und wählen Sie **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="da262-p104">A list appears showing data entities that are being exposed by the OData Service. Select one or more of the entities, and choose **Finish**.</span></span>
    
  

### <a name="to-deploy-the-add-in-scoped-external-content-type-as-an-add-in-package"></a><span data-ttu-id="da262-123">Den Add-in-bezogenen externen Inhaltstyp als ein Add-in-Paket bereitgestellt</span><span class="sxs-lookup"><span data-stu-id="da262-123">To deploy the add-in-scoped external content type as an add-in package</span></span>


1. <span data-ttu-id="da262-124">Wählen Sie im Visual Studio, klicken Sie im Menü **Erstellen** auf **Veröffentlichen**.</span><span class="sxs-lookup"><span data-stu-id="da262-124">In Visual Studio, on the **Build** menu, choose **Publish**.</span></span>
    
  
2. <span data-ttu-id="da262-125">Nennen Sie das Paket, geben Sie den Speichervorgang Speicherort auf Ihrem lokalen Festplatte Laufwerk, und wählen Sie **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="da262-125">Name the package, specify the save location on your local hard drive, and choose **Finish**.</span></span>
    
  

### <a name="to-extract-the-model-file-from-the-app-package"></a><span data-ttu-id="da262-126">Extrahiert die Modelldatei aus dem App-Paket</span><span class="sxs-lookup"><span data-stu-id="da262-126">To extract the model file from the .app package</span></span>


1. <span data-ttu-id="da262-127">Öffnen Sie den Ordner, in dem das App-Paket erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="da262-127">Open the folder where the .app package is created.</span></span>
    
  
2.  <span data-ttu-id="da262-128">Ändern Sie die Erweiterung von App inZIP.</span><span class="sxs-lookup"><span data-stu-id="da262-128">Change the file name extension from.app to.zip.</span></span>
    
  
3. <span data-ttu-id="da262-129">Extrahieren Sie das ZIP-Paket in einen lokalen Ordner.</span><span class="sxs-lookup"><span data-stu-id="da262-129">Extract the ZIP package to a local folder.</span></span>
    
  
4. <span data-ttu-id="da262-130">Öffnen Sie den extrahierten Ordner aus, um die WSP-Datei zu suchen.</span><span class="sxs-lookup"><span data-stu-id="da262-130">Open the extracted folder to find the WSP file.</span></span>
    
  
5. <span data-ttu-id="da262-131">Verschieben Sie die WSP-Datei an einen anderen Speicherort.</span><span class="sxs-lookup"><span data-stu-id="da262-131">Move the WSP file to another location.</span></span>
    
  
6. <span data-ttu-id="da262-132">Ändern Sie die WSP-Dateinamenerweiterung für diese Datei in CAB.</span><span class="sxs-lookup"><span data-stu-id="da262-132">Change the .wsp file name extension on this file to .cab.</span></span>
    
  
7. <span data-ttu-id="da262-133">Öffnen Sie die CAB-Datei, und finden Sie die Datei Bdcmodel.bdcm.</span><span class="sxs-lookup"><span data-stu-id="da262-133">Open the .cab file, and you will find the Bdcmodel.bdcm file.</span></span>
    
  
8. <span data-ttu-id="da262-134">Speichern Sie die Bdcmodel.bdcm-Datei an einen anderen Speicherort.</span><span class="sxs-lookup"><span data-stu-id="da262-134">Save the Bdcmodel.bdcm file to another location.</span></span>
    
  

### <a name="to-import-the-model-file-using-sharepoint-central-administration-pages"></a><span data-ttu-id="da262-135">So importieren Sie die Modelldatei mithilfe der SharePoint-Zentraladministrationsseiten</span><span class="sxs-lookup"><span data-stu-id="da262-135">To import the model file using SharePoint Central Administration pages</span></span>


1. <span data-ttu-id="da262-136">Öffnen Sie SharePoint Online oder SharePoint lokalen Zentraladministrationsseiten.</span><span class="sxs-lookup"><span data-stu-id="da262-136">Open SharePoint Online or SharePoint on-premises Central Administration pages.</span></span>
    
  
2. <span data-ttu-id="da262-137">Wählen Sie **Verwalten Applications dienen**.</span><span class="sxs-lookup"><span data-stu-id="da262-137">Choose **Manage serve applications**.</span></span>
    
  
3. <span data-ttu-id="da262-138">Wählen Sie die **Business Data Connectivity-Dienst**.</span><span class="sxs-lookup"><span data-stu-id="da262-138">Choose **Business Data Connectivity Service**.</span></span>
    
  
4. <span data-ttu-id="da262-139">Wählen Sie den **Import**-Link auf der Serverkomponente.</span><span class="sxs-lookup"><span data-stu-id="da262-139">Choose the **Import** link on the server ribbon.</span></span>
    
  
5. <span data-ttu-id="da262-140">Wählen Sie die Schaltfläche **Durchsuchen**, um den Speicherort angeben, in dem Sie die bdcm-Datei extrahiert haben.</span><span class="sxs-lookup"><span data-stu-id="da262-140">Choose the **Browse** button to specify the location where you extracted the .bdcm file.</span></span>
    
  
6. <span data-ttu-id="da262-141">Lassen Sie die Standardeinstellungen, und wählen Sie dann auf **Importieren**.</span><span class="sxs-lookup"><span data-stu-id="da262-141">Keep the default settings, and then choose **Import**.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="da262-142">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="da262-142">Additional resources</span></span>
<span data-ttu-id="da262-143"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="da262-143"></span></span>


-  [<span data-ttu-id="da262-144">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="da262-144">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="da262-145">Vorgehensweise: erstellen ein Add-in-bezogenen externes Inhaltstyps in SharePoint</span><span class="sxs-lookup"><span data-stu-id="da262-145">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [<span data-ttu-id="da262-146">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="da262-146">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="da262-147">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="da262-147">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="da262-148">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="da262-148">Open Data Protocol</span></span>](http://www.odata.org)
    
  

  
    
    

