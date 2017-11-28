---
title: Listeninstanz in SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 5bfe9697dfbd75b389f974801add3ed399507ed4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="list-instance-in-the-sharepoint-add-in-model"></a><span data-ttu-id="d0aec-102">Listeninstanz in SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="d0aec-102">List instance in the SharePoint add-in model</span></span>
============================================

<a name="summary"></a><span data-ttu-id="d0aec-103">Summary</span><span class="sxs-lookup"><span data-stu-id="d0aec-103">Summary</span></span>
-------

<span data-ttu-id="d0aec-104">Ansatz verwenden Sie zum Erstellen von Listeninstanzen unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="d0aec-104">The approach you take to create list instances is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="d0aec-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario Listeninstanzen wurden mit deklarativem Code erstellt und über den SharePoint-Lösungen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="d0aec-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, list instances were created with declarative code and deployed via SharePoint Solutions.</span></span> 

<span data-ttu-id="d0aec-106">In einem Szenario mit SharePoint-Add-Ins Modell wird das remote provisioning Muster Listeninstanzen erstellen.</span><span class="sxs-lookup"><span data-stu-id="d0aec-106">In a SharePoint Add-in model scenario, the remote provisioning pattern is used to create list instances.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="d0aec-107">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="d0aec-107">High-level guidelines</span></span>
---------------------

<span data-ttu-id="d0aec-108">In der Regel von einer Ziehpunkt möchten wir bieten die folgenden allgemeinen Richtlinien Listeninstanzen erstellen.</span><span class="sxs-lookup"><span data-stu-id="d0aec-108">As a rule of a thumb, we would like to provide the following high-level guidelines to create list instances.</span></span>

- <span data-ttu-id="d0aec-109">Verwenden Sie das remote provisioning Muster, um Listeninstanzen erstellen.</span><span class="sxs-lookup"><span data-stu-id="d0aec-109">Use the remote provisioning pattern to create list instances.</span></span>
- <span data-ttu-id="d0aec-110">Verwenden Sie keinen deklarativen Code (elements.xml) Listeninstanzen erstellen.</span><span class="sxs-lookup"><span data-stu-id="d0aec-110">Do not use declarative code (elements.xml) to create list instances.</span></span>

<span data-ttu-id="d0aec-111">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="d0aec-111">**Getting started**</span></span>

<span data-ttu-id="d0aec-112">Die folgenden O365 Plug & Play-Codebeispiel und Video wird gezeigt, wie ein SharePoint-Add-in zu erstellen, die eine Benutzeroberfläche bereitstellt, mit die Endbenutzer neue Dokumentbibliotheken erstellen können.</span><span class="sxs-lookup"><span data-stu-id="d0aec-112">The following O365 PnP code sample and video demonstrates how to create a SharePoint Add-in that provides a user interface that allows end users to create new document libraries.</span></span> <span data-ttu-id="d0aec-113">Darüber hinaus wird das Erstellen einer Dokumentbibliothek mit spezifischen Konfigurationen, die gemeinsam eine Vorlage darstellen veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="d0aec-113">It also demonstrates how to create a document library with specific configurations that collectively represent a template.</span></span> <span data-ttu-id="d0aec-114">In diesem Beispiel finden Sie den Code, mit der eine Listeninstanz erstellt.</span><span class="sxs-lookup"><span data-stu-id="d0aec-114">In this sample you will find the code that creates a list instance.</span></span>

- [<span data-ttu-id="d0aec-115">ECM. DocumentLibraries (O365 Plug & Play-Codebeispiel)</span><span class="sxs-lookup"><span data-stu-id="d0aec-115">ECM.DocumentLibraries (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)

<span data-ttu-id="d0aec-116">Im folgende Video durchlaufen im Codebeispiel.</span><span class="sxs-lookup"><span data-stu-id="d0aec-116">The following video walks through the code sample.</span></span>

- [<span data-ttu-id="d0aec-117">Dokument- und Vorlagen mit app-Modell (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="d0aec-117">Document and list templates with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)

<span data-ttu-id="d0aec-118">Verwenden Sie die AddList-Methode in der SharePoint-CSOM, um eine Listeninstanz über die remote provisioning Muster zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d0aec-118">Use the AddList method in the SharePoint CSOM to create a list instance via the remote provisioning pattern.</span></span> <span data-ttu-id="d0aec-119">Der folgende Code die [ECM entnommen. DocumentLibraries (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) veranschaulicht, wie Sie ihn.</span><span class="sxs-lookup"><span data-stu-id="d0aec-119">The following code taken from the [ECM.DocumentLibraries (O365 PnP Code Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) illustrates how to do it.</span></span>

    private void CreateLibrary(ClientContext ctx, Library library, string associateContentTypeID) 
    {
        if (!ctx.Web.ListExists(library.Title))
        {
           // Create List Instance
           ctx.Web.AddList(ListTemplateType.DocumentLibrary, library.Title, false);
           List _list = ctx.Web.GetListByTitle(library.Title);
           
           //Set Description
           if(!string.IsNullOrEmpty(library.Description)) 
           {
            _list.Description = library.Description;
           }

           //Turn on versioning 
           if(library.VerisioningEnabled) {
              _list.EnableVersioning = true;
           }
           
            //Turn on Content Types
           _list.ContentTypesEnabled = true;
           _list.Update();

           //Add Content Type to List
           ctx.Web.AddContentTypeToListById(library.Title, associateContentTypeID, true);
    
           //Remove the default Document Content Type
           _list.RemoveContentTypeByName(ContentTypeManager.DEFAULT_DOCUMENT_CT_NAME);

           ctx.Web.Context.ExecuteQuery();
        }
    }

<span data-ttu-id="d0aec-120">Das folgende Codebeispiel veranschaulicht, wie eine Listeninstanz mit der SharePoint-REST-API zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d0aec-120">The following code sample illustrates how to create a list instance with the SharePoint REST API.</span></span>  <span data-ttu-id="d0aec-121">In diesem Beispiel stammen von [Listen und der Liste Elemente REST-API-Referenz (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)</span><span class="sxs-lookup"><span data-stu-id="d0aec-121">This sample comes from the [Lists and list items REST API reference (MSDN Article)](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)</span></span>

    executor.executeAsync({
      url: "<app web url>/_api/SP.AppContextSite(@target)/web/lists
        ?@target='<host web url>'",
      method: "POST",
      body: "{ '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true, 'BaseTemplate': 100,
        'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test title' }",
      headers: { "content-type": "application/json;odata=verbose" },
      success: successHandler,
      error: errorHandler
    });

<a name="related-links"></a><span data-ttu-id="d0aec-122">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="d0aec-122">Related links</span></span>
=============
- [<span data-ttu-id="d0aec-123">Listen und Liste Elemente REST-API-Referenz (MSDN-Artikel)</span><span class="sxs-lookup"><span data-stu-id="d0aec-123">Lists and list items REST API reference (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)
- [<span data-ttu-id="d0aec-124">Listendefinitionen / Listenvorlagen (SharePoint-Add-Ins Modell Anleitung)</span><span class="sxs-lookup"><span data-stu-id="d0aec-124">List Definitions / List Templates (SharePoint Add-in model recipe)</span></span>](list-definition-template-sharepoint-add-in.md)
- [<span data-ttu-id="d0aec-125">Dokument- und Vorlagen mit app-Modell (O365 Plug & Play-Video)</span><span class="sxs-lookup"><span data-stu-id="d0aec-125">Document and list templates with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)
- <span data-ttu-id="d0aec-126">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="d0aec-126">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="d0aec-127">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="d0aec-127">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="d0aec-128">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="d0aec-128">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="d0aec-129">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="d0aec-129">Related PnP samples</span></span>
===================

- [<span data-ttu-id="d0aec-130">ECM. DocumentLibraries (O365 Plug & Play-Codebeispiel)</span><span class="sxs-lookup"><span data-stu-id="d0aec-130">ECM.DocumentLibraries (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
- <span data-ttu-id="d0aec-131">Beispiele und Inhalte am [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span><span class="sxs-lookup"><span data-stu-id="d0aec-131">Samples and content at [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="d0aec-132">Gilt für</span><span class="sxs-lookup"><span data-stu-id="d0aec-132">Applies to</span></span>
==========
- <span data-ttu-id="d0aec-133">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="d0aec-133">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="d0aec-134">Office 365 dedizierte (D) *teilweise*</span><span class="sxs-lookup"><span data-stu-id="d0aec-134">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="d0aec-135">SharePoint 2013 lokal – *teilweise*</span><span class="sxs-lookup"><span data-stu-id="d0aec-135">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="d0aec-136">*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*</span><span class="sxs-lookup"><span data-stu-id="d0aec-136">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
