---
title: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bc60ea49-c44e-4531-af62-06b8cf77d35d
ms.openlocfilehash: 9ddf00811e05fcca25b4c4f406ac22ce5de9aca0
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="create-an-external-content-type-from-an-odata-source-in-sharepoint"></a><span data-ttu-id="6d06a-102">Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d06a-102">How to: Create an external content type from an OData source in SharePoint</span></span>

<span data-ttu-id="6d06a-103">In diesem Artikel erfahren Sie, wie Sie Visual Studio 2012 verwenden, um eine veröffentlichte OData-Quelle zu erkennen und einen wieder verwendbaren externen Inhaltstyp für die Verwendung in Business Connectivity Services (BCS) in SharePoint zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6d06a-103">Learn how to use Visual Studio 2012 to discover a published OData source and create a reusable external content type for use in Business Connectivity Services (BCS) in SharePoint.</span></span>

## <a name="prerequisites-for-creating-odata-based-external-content-types"></a><span data-ttu-id="6d06a-104">Voraussetzungen für das Erstellen von OData-basierten externen Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="6d06a-104">Prerequisites for creating OData-based external content types</span></span>
<span data-ttu-id="6d06a-105"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="6d06a-105"><a name="bkmk_Prerequisites"> </a></span></span>

<span data-ttu-id="6d06a-106">Zum Erstellen eines externen Inhaltstyps aus einer Open Data-Protokollquelle (OData) benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6d06a-106">To create an external content type from an Open Data protocol (OData) source, you will need the following:</span></span>
  
    
    

- <span data-ttu-id="6d06a-107">Eine Instanz von SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d06a-107">An instance of SharePoint</span></span>
    
  
- <span data-ttu-id="6d06a-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="6d06a-108">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="6d06a-109">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="6d06a-109">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="6d06a-110">Einen veröffentlichten OData-Dienst, der über das Internet verfügbar ist</span><span class="sxs-lookup"><span data-stu-id="6d06a-110">A published OData service available through the Internet</span></span>
    
  
<span data-ttu-id="6d06a-111">Informationen zum Einrichten Ihrer SharePoint-Entwicklungsumgebung finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6d06a-111">For information about how to set up your SharePoint development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

> <span data-ttu-id="6d06a-112">**Hinweis:** SharePoint Designer 2013kann nicht für die automatische Generierung von BDC-Modellen aus einer OData-Quelle verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="6d06a-112">**Note:** SharePoint Designer 2013 can't be used to autogenerate BDC models from an OData source.</span></span> <span data-ttu-id="6d06a-113">Sie können stattdessen Visual Studio 2012 verwenden.</span><span class="sxs-lookup"><span data-stu-id="6d06a-113">You can use Visual Studio 2012 instead.</span></span> 
  
    
    


### <a name="core-concepts-for-working-with-odata-external-content-types"></a><span data-ttu-id="6d06a-114">Kernkonzepte für das Arbeiten mit externen OData-Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="6d06a-114">Core concepts for working with OData external content types</span></span>

<span data-ttu-id="6d06a-115">Die folgenden Artikel enthalten Informationen zu OData und dem OData-Connector in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6d06a-115">The following articles provide background information about OData and the OData connector in SharePoint.</span></span>
  
    
    

<span data-ttu-id="6d06a-116">**Tabelle 1: Kernkonzeüte für externe OData-Inhaltstypen**</span><span class="sxs-lookup"><span data-stu-id="6d06a-116">**Table 1. Core concepts for OData external content types**</span></span>


|<span data-ttu-id="6d06a-117">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="6d06a-117">**Article title**</span></span>|<span data-ttu-id="6d06a-118">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6d06a-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="6d06a-119">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d06a-119">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |<span data-ttu-id="6d06a-120">Erfahren Sie mehr über die ersten Schritte beim Erstellen externer Inhaltstypen auf der Basis von OData-Quellen und wie Sie diese Daten in SharePoint oder Office-Komponenten verwenden.</span><span class="sxs-lookup"><span data-stu-id="6d06a-120">Get started with creating external content types based on OData sources, and learn how to use that data in SharePoint or Office components.</span></span>  <br/> |
| [<span data-ttu-id="6d06a-121">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d06a-121">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="6d06a-122">Erfahren Sie mehr über externe BCS-Inhaltstypen und Voraussetzungen für deren Erstellung in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6d06a-122">Learn about BCS external content types and what you need to start creating them in SharePoint.</span></span>  <br/> |
   

## <a name="create-an-odata-based-external-content-type"></a><span data-ttu-id="6d06a-123">Erstellen eines OData-basierten externen Inhaltstyp</span><span class="sxs-lookup"><span data-stu-id="6d06a-123">Create an OData-based external content type</span></span>
<span data-ttu-id="6d06a-124"><a name="bkmk_CreatingODataECT"> </a></span><span class="sxs-lookup"><span data-stu-id="6d06a-124"><a name="bkmk_CreatingODataECT"> </a></span></span>

<span data-ttu-id="6d06a-125">Die folgenden Schritte zeigen, wie Sie Visual Studio 2012 zum Erstellen eines externen Inhaltstyps auf der Basis einer OData-Quelle verwenden.</span><span class="sxs-lookup"><span data-stu-id="6d06a-125">The following steps show how to use Visual Studio 2012 to create an external content type based on an OData source.</span></span>
  
    
    

### <a name="to-create-a-new-sharepoint-add-in"></a><span data-ttu-id="6d06a-126">So erstellen Sie ein neues SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="6d06a-126">To create a new SharePoint Add-in</span></span>


1. <span data-ttu-id="6d06a-127">Erstellen Sie in Visual Studio 2012 ein neues **App für SharePoint**-Projekt, das sich unter dem Knoten **SharePoint-Vorlage** befindet.</span><span class="sxs-lookup"><span data-stu-id="6d06a-127">In Visual Studio 2012, create a new **App for SharePoint** project, which is located under the **SharePoint template** node.</span></span>
    
  
2. <span data-ttu-id="6d06a-128">Benennen Sie Ihr Projekt, und wählen Sie **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="6d06a-128">Name your project, and choose **OK**.</span></span>
    
  
3. <span data-ttu-id="6d06a-129">Geben Sie zum Angeben der Einstellungen für SharePoint einen Namen für Ihre App und die URL des SharePoint-Servers ein, den Sie für das Debuggen verwenden.</span><span class="sxs-lookup"><span data-stu-id="6d06a-129">To specify the SharePoint settings, enter a name for your app, and the URL of the SharePoint server you will be debugging against.</span></span>
    
  
4. <span data-ttu-id="6d06a-130">Wählen Sie **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="6d06a-130">Choose **Finish**.</span></span>
    
  
<span data-ttu-id="6d06a-131">Nachdem das Projekt erstellt wurde, verwenden Sie das neue Tool für die automatische Generierung für OData-Quellen, und fügen Sie Ihrer App ein BDC-Modell für die OData-Quelle hinzu.</span><span class="sxs-lookup"><span data-stu-id="6d06a-131">After the project is created, you use the new autogeneration tooling for OData sources and add a BDC model for the OData source to your app.</span></span>
  
    
    

### <a name="to-add-a-new-bdc-model"></a><span data-ttu-id="6d06a-132">So fügen Sie ein neues BDC-Modell hinzu</span><span class="sxs-lookup"><span data-stu-id="6d06a-132">To add a new BDC model</span></span>


1. <span data-ttu-id="6d06a-133">Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.</span><span class="sxs-lookup"><span data-stu-id="6d06a-133">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
    <span data-ttu-id="6d06a-134">Damit wird ein Assistent gestartet, der Ihnen hilft, die ausgewählte Datenquelle zu ermitteln und das BDC-Modell zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6d06a-134">This starts a wizard that will help you discover the selected data source and create the BDC model.</span></span>
    
  
2. <span data-ttu-id="6d06a-p102">Auf der ersten Seite des Assistenten wird die URL des Datendiensts ermittelt. Geben Sie auf der Seite **OData-Quelle angeben** die URL des OData-Diensts ein, mit dem Sie eine Verbindung herstellen möchten. Die URL sollte etwa folgendermaßen aussehen: `http://services.odata.org/Northwind/Northwind.svc/`.</span><span class="sxs-lookup"><span data-stu-id="6d06a-p102">The first page of the wizard is used to collect the URL of the data service. On the **Specify OData Source** page, enter the URL of the OData service that you want to connect to. The URL should resemble the following: `http://services.odata.org/Northwind/Northwind.svc/`.</span></span>
    
    > <span data-ttu-id="6d06a-138">**Hinweis:** Sie zeigen den Northwind-Dienst an, der in der Liste der Produzenten auf der  [Open Data Protocol-Website ](http://www.odata.org/ecosystem#liveservices) verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="6d06a-138">**Note:** You will show the Northwind service that is available from the producers list found on the  [Open Data Protocol website](http://www.odata.org/ecosystem#liveservices).</span></span> 
3. <span data-ttu-id="6d06a-139">Wählen Sie einen Namen für Ihre OData-Datenquelle, und wählen Sie dann **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6d06a-139">Choose a name for your OData source, and then choose **Next**.</span></span>
    
  
4. <span data-ttu-id="6d06a-p103">Eine Liste von Datenentitäten, die von dem OData-Dienst verfügbar gemacht werden, wird angezeigt. Wählen Sie eine oder mehrere der Entitäten und dann **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="6d06a-p103">A list of data entities that are being exposed by the OData Service appears. Select one or more of the entities, and choose **Finish**.</span></span>
    
  

### <a name="to-view-the-structure-of-the-entities"></a><span data-ttu-id="6d06a-142">So zeigen Sie die Struktur der Entitäten an</span><span class="sxs-lookup"><span data-stu-id="6d06a-142">To view the structure of the entities</span></span>


- <span data-ttu-id="6d06a-p104">Beachten Sie, dass Visual Studio einen neuen Ordner namens „Externe Inhaltstypen" erstellt hat. In diesem Ordner finden Sie einen Unterordner mit dem Namen der neuen Datenquelle. Wenn Sie diesen weiter erweitern, sehen Sie ein Element, das die von Ihnen ausgewählte Entität darstellt. Zum Anzeigen einer grafischen Übersicht über die Entitäten und deren Typen öffnen Sie die **ECT**-Datei, die Sie anzeigen möchten.</span><span class="sxs-lookup"><span data-stu-id="6d06a-p104">Notice that Visual Studio created a new folder named External Content Types. Inside that folder, you will find a subfolder with the name of your new data source. If you further expand this, you will see an item that represents the entity you selected. To view a graphical list of the entities and their types, open the **ect** file that you want to view.</span></span>
    
    <span data-ttu-id="6d06a-147">Sie können auch den XML-Code der Entitäten anzeigen, indem Sie die ECT-Dateien in einem XML-Editor öffnen.</span><span class="sxs-lookup"><span data-stu-id="6d06a-147">You can also view the XML of the entities by opening the ect files in an XML editor.</span></span>
    
  

## <a name="use-a-stream-accessor-for-the-odata-source"></a><span data-ttu-id="6d06a-148">Verwenden eines StreamAccessors für die OData-Quelle</span><span class="sxs-lookup"><span data-stu-id="6d06a-148">Use a stream accessor for the OData source</span></span>
<span data-ttu-id="6d06a-149"><a name="bkmk_UseStreamAccessor"> </a></span><span class="sxs-lookup"><span data-stu-id="6d06a-149"><a name="bkmk_UseStreamAccessor"> </a></span></span>

<span data-ttu-id="6d06a-150">Mit dem folgenden Code können Sie auf einen Datenstrom zugreifen, den der OData-Connector verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="6d06a-150">Using the following code, you can access a data stream that the OData connector can use.</span></span>
  
    
    

```cs

/*Invoke  Stream Accessor Method */
        internal void ExecuteStreamAccessorMethod(IEntityInstance entityInstance, string streamAccessorName)
        {
            this.Log.Comment("ExecuteStreamAccessorMethod enter");
            this.Log.Comment("streamAccesor method" + streamAccessorName);
            IStreamableField isf = entityInstance.GetStreamableField(streamAccessorName);
            Stream resStream = isf.GetData();
            using (BinaryReader reader = new BinaryReader(resStream))
            {
                using (FileStream fs = File.Create(@"C:\\" + entityInstance.GetIdentity().GetIdentifierValues()[0] + ".jpg"))
                {
                    int bytesRead = 0;
                    do
                    {
                        int nrBytes = 80 * 1000 * 1000;
                        byte[] streamData = new byte[nrBytes];
                        bytesRead = reader.Read(streamData, 0, nrBytes);
                        this.Log.Comment("Total Bytes Read - " + bytesRead);
                        if (bytesRead > 0)
                        {
                            fs.Write(streamData, 0, bytesRead);
                        }
                    } while (bytesRead > 0);
                }
            }
            isf.Dispose();
            this.Log.Comment("ExecuteStreamAccessorMethod Exit" );
        }
```


## <a name="next-steps"></a><span data-ttu-id="6d06a-151">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="6d06a-151">Next steps</span></span>
<span data-ttu-id="6d06a-152"><a name="bkmk_Next"> </a></span><span class="sxs-lookup"><span data-stu-id="6d06a-152"><a name="bkmk_Next"> </a></span></span>

<span data-ttu-id="6d06a-153">Nachdem Sie einen externen Inhaltstyp erstellt haben, können Sie diesen verwenden, um Daten in SharePoint mithilfe der integrierten Objekte (externe Listen, Geschäftsdaten-Webparts oder benutzerdefinierter Code) zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="6d06a-153">After you have built an external content type, you can then use it to present data inside SharePoint by using the built-in objects (external lists, Business Data Web Parts, or custom code).</span></span>
  
    
    
<span data-ttu-id="6d06a-154">Weitere Informationen finden Sie unter  [Vorgehensweise: Erstellen eine externe Liste mithilfe einer in SharePoint OData-Datenquelle](how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6d06a-154">For more information, see  [How to: Create an external list using an OData data source in SharePoint](how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="6d06a-155">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6d06a-155">Additional resources</span></span>
<span data-ttu-id="6d06a-156"><a name="bkmk_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="6d06a-156"><a name="bkmk_Addres"> </a></span></span>


-  [<span data-ttu-id="6d06a-157">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d06a-157">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6d06a-158">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d06a-158">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6d06a-159">Was ist neu in Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d06a-159">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6d06a-160">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6d06a-160">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  

