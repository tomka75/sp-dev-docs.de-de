---
title: Erstellen externer Inhaltstypen auf Add-In-Ebene in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: de4b50a3-84da-48ce-9ba0-fe06571e52a8
ms.openlocfilehash: 3a89995c1362d50b65b7277416ff165cd4d3db47
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-an-add-in-scoped-external-content-type-in-sharepoint"></a><span data-ttu-id="45bdb-102">Erstellen externer Inhaltstypen auf Add-In-Ebene in SharePoint</span><span class="sxs-lookup"><span data-stu-id="45bdb-102">How to: Create an add-in-scoped external content type in SharePoint</span></span>

<span data-ttu-id="45bdb-103">In diesem Artikel erfahren Sie, wie Sie externe Inhaltstypen erstellen, die in einer SharePoint-Add-In installiert, gesichert und verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="45bdb-103">Learn how to create external content types that can be installed, secured, and used in an SharePoint Add-in.</span></span>

## <a name="prerequisites-for-developing-add-in-scoped-external-content-types"></a><span data-ttu-id="45bdb-104">Erforderliche Komponenten für die Entwicklung von add-in-bezogenen externen Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="45bdb-104">Prerequisites for developing add-in-scoped external content types</span></span>
<span data-ttu-id="45bdb-105"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="45bdb-105"><a name="bkmk_Prerequisites"> </a></span></span>

<span data-ttu-id="45bdb-106">Wenn Sie die ersten Schritte beim Entwickeln von add-in-bezogenen externen Inhaltstypen, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="45bdb-106">To get started developing add-in-scoped external content types, you need the following:</span></span>
  
    
    

- <span data-ttu-id="45bdb-107">SharePoint</span><span class="sxs-lookup"><span data-stu-id="45bdb-107">SharePoint</span></span>
    
  
- <span data-ttu-id="45bdb-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="45bdb-108">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="45bdb-109">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="45bdb-109">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="45bdb-110">Einen veröffentlichten OData-Dienst, der über das Internet verfügbar ist</span><span class="sxs-lookup"><span data-stu-id="45bdb-110">A published OData service available through the Internet</span></span>
    
  
<span data-ttu-id="45bdb-111">Informationen zum Einrichten einer SharePoint-Entwicklungsumgebung finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="45bdb-111">For information about setting up a SharePoint development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="create-an-add-in-scoped-external-content-type"></a><span data-ttu-id="45bdb-112">Erstellen externer Inhaltstypen auf Add-In-Ebene</span><span class="sxs-lookup"><span data-stu-id="45bdb-112">Create an add-in-scoped external content type</span></span>
<span data-ttu-id="45bdb-113"><a name="bkmk_CreateECT"> </a></span><span class="sxs-lookup"><span data-stu-id="45bdb-113"><a name="bkmk_CreateECT"> </a></span></span>

<span data-ttu-id="45bdb-114">Die folgenden Schritte zeigen zum Erstellen eines externen Inhaltstyps basierend auf einer Open Data Protocol (OData) Datenquelle, und ändern sie Ihre SharePoint-Add-In zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="45bdb-114">The following steps show how to create an external content type based on an Open Data protocol (OData) source, and how to modify it to be scoped to your SharePoint Add-in.</span></span>
  
    
    

### <a name="to-create-a-new-sharepoint-add-in"></a><span data-ttu-id="45bdb-115">So erstellen Sie ein neues SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="45bdb-115">To create a new SharePoint Add-in</span></span>


1. <span data-ttu-id="45bdb-116">Öffnen Sie Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="45bdb-116">Open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="45bdb-117">Erstellen Sie ein Projekt **-Add-in für SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="45bdb-117">Create an **Add-in for SharePoint** project.</span></span>
    
  
3. <span data-ttu-id="45bdb-p101">Geben Sie die Add-in-Einstellungen, einschließlich der Add-in-Name die URL der Website für das Debuggen des Add-Ins und wie Sie das Add-in (automatisch gehostet, vom Anbieter gehostete oder SharePoint-Hosting) hosten möchten. Weitere Informationen finden Sie unter  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="45bdb-p101">Specify the add-in settings, including add-in name, the site URL for debugging the add-in, and how you would like to host the add-in (Autohosted, Provider-hosted, or SharePoint-hosted). For more information, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span></span>
    
  
4. <span data-ttu-id="45bdb-120">Wählen Sie auf **Fertig stellen**, um die app zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="45bdb-120">Choose **Finish** to create the app.</span></span>
    
  
<span data-ttu-id="45bdb-121">Führen Sie die Schritte zum Erstellen von SharePoint-Add-Ins finden Sie in der folgenden:</span><span class="sxs-lookup"><span data-stu-id="45bdb-121">For complete steps for creating SharePoint Add-ins, see the following:</span></span>
  
    
    

-  <span data-ttu-id="45bdb-122">[Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](http://msdn.microsoft.com/library/3038dd73-41ee-436f-8c78-ef8e6869bf7b%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="45bdb-122">[Get started creating provider-hosted SharePoint Add-ins](http://msdn.microsoft.com/library/3038dd73-41ee-436f-8c78-ef8e6869bf7b%28Office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="45bdb-123">[So geht's: Erstellen einer einfachen automatisch gehosteten App für SharePoint](http://msdn.microsoft.com/library/0572894d-c437-4b7d-8ac6-8405496e2145%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="45bdb-123">[How to: Create a basic autohosted app for SharePoint](http://msdn.microsoft.com/library/0572894d-c437-4b7d-8ac6-8405496e2145%28Office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="45bdb-124">[Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](http://msdn.microsoft.com/library/1b992485-6efe-4ea4-a18c-221689b0b66f%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="45bdb-124">[Get started creating SharePoint-hosted SharePoint Add-ins](http://msdn.microsoft.com/library/1b992485-6efe-4ea4-a18c-221689b0b66f%28Office.15%29.aspx)</span></span>
    
  

### <a name="to-generate-the-external-content-type"></a><span data-ttu-id="45bdb-125">Um den externen Inhaltstyp zu generieren.</span><span class="sxs-lookup"><span data-stu-id="45bdb-125">To generate the external content type</span></span>


1. <span data-ttu-id="45bdb-126">Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.</span><span class="sxs-lookup"><span data-stu-id="45bdb-126">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
    <span data-ttu-id="45bdb-127">Einen Assistenten, der können Sie die ausgewählten Datenquelle suchen und erstellen Sie das BDC-Modell, wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="45bdb-127">This starts a wizard that helps you find the selected data source and create the BDC model.</span></span>
    
  
2. <span data-ttu-id="45bdb-p102">Geben Sie auf der Seite **Set OData Source** die URL des OData-Diensts, die Sie mit verbinden möchten. Die URL sollte etwa wie folgt aussehen: `http://services.odata.org/Northwind/Northwind.svc/`.</span><span class="sxs-lookup"><span data-stu-id="45bdb-p102">On the **Set OData Source** page, enter the URL of the OData service that you want to connect to. The URL should look something like this: `http://services.odata.org/Northwind/Northwind.svc/`.</span></span>
    
    <span data-ttu-id="45bdb-130">Geben Sie einen Namen für die OData-Quelle an.</span><span class="sxs-lookup"><span data-stu-id="45bdb-130">Specify a name for your OData source.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="45bdb-131">In diesem Beispiel verwenden Sie den Northwind-Dienst, der sich in der Hersteller-Liste auf der [OpenData Protocol-Website](http://www.odata.org) befindet.</span><span class="sxs-lookup"><span data-stu-id="45bdb-131">[Note:](http://www.odata.org) For this example, you will use the Northwind service that is available from the producers list located on the  Open Data Protocol website.</span></span> 

3. <span data-ttu-id="45bdb-p103">Eine Liste wird angezeigt, mit Datenentitäten, die vom OData Service verfügbar gemacht werden. Wählen Sie eine oder mehrere Entitäten, und wählen Sie **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="45bdb-p103">A list appears showing data entities that are being exposed by the OData Service. Select one or more of the entities, and choose **Finish**.</span></span>
    
  

### <a name="to-deploy-the-add-in-scoped-external-content-type"></a><span data-ttu-id="45bdb-134">Zum Bereitstellen von des Add-in-bezogenen externen Inhaltstyps</span><span class="sxs-lookup"><span data-stu-id="45bdb-134">To deploy the add-in-scoped external content type</span></span>


- <span data-ttu-id="45bdb-135">Drücken Sie F5, um kompilieren Sie das Projekt, und laden die Projektdateien in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="45bdb-135">Press F5 to compile the project and upload the project files to SharePoint.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="45bdb-136">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="45bdb-136">See also</span></span>
<span data-ttu-id="45bdb-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="45bdb-137"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="45bdb-138">Add-in-bezogenen externen Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="45bdb-138">Add-in-scoped external content types in SharePoint</span></span>](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  <span data-ttu-id="45bdb-139">[Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="45bdb-139">[Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="45bdb-140">[SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="45bdb-140">[SharePoint Add-ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)</span></span>
    
  
-  [<span data-ttu-id="45bdb-141">Externe Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="45bdb-141">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="45bdb-142">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="45bdb-142">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="45bdb-143">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="45bdb-143">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  

