---
title: Listeninstanz in SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 5bfe9697dfbd75b389f974801add3ed399507ed4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="list-instance-in-the-sharepoint-add-in-model"></a>Listeninstanz in SharePoint-add-in-Objektmodell
============================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Erstellen von Listeninstanzen unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario Listeninstanzen wurden mit deklarativem Code erstellt und über den SharePoint-Lösungen bereitgestellt. 

In einem Szenario mit SharePoint-Add-Ins Modell wird das remote provisioning Muster Listeninstanzen erstellen.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir bieten die folgenden allgemeinen Richtlinien Listeninstanzen erstellen.

- Verwenden Sie das remote provisioning Muster, um Listeninstanzen erstellen.
- Verwenden Sie keinen deklarativen Code (elements.xml) Listeninstanzen erstellen.

**Erste Schritte**

Die folgenden O365 Plug & Play-Codebeispiel und Video wird gezeigt, wie ein SharePoint-Add-in zu erstellen, die eine Benutzeroberfläche bereitstellt, mit die Endbenutzer neue Dokumentbibliotheken erstellen können. Darüber hinaus wird das Erstellen einer Dokumentbibliothek mit spezifischen Konfigurationen, die gemeinsam eine Vorlage darstellen veranschaulicht. In diesem Beispiel finden Sie den Code, mit der eine Listeninstanz erstellt.

- [ECM. DocumentLibraries (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)

Im folgende Video durchlaufen im Codebeispiel.

- [Dokument- und Vorlagen mit app-Modell (O365 Plug & Play-Video)](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)

Verwenden Sie die AddList-Methode in der SharePoint-CSOM, um eine Listeninstanz über die remote provisioning Muster zu erstellen. Der folgende Code die [ECM entnommen. DocumentLibraries (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) veranschaulicht, wie Sie ihn.

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

Das folgende Codebeispiel veranschaulicht, wie eine Listeninstanz mit der SharePoint-REST-API zu erstellen.  In diesem Beispiel stammen von [Listen und der Liste Elemente REST-API-Referenz (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)

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

<a name="related-links"></a>Verwandte links
=============
- [Listen und Liste Elemente REST-API-Referenz (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)
- [Listendefinitionen / Listenvorlagen (SharePoint-Add-Ins Modell Anleitung)](list-definition-template-sharepoint-add-in.md)
- [Dokument- und Vorlagen mit app-Modell (O365 Plug & Play-Video)](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [ECM. DocumentLibraries (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
- Beispiele und Inhalte am [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
