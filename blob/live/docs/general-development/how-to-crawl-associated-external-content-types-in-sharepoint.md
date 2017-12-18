---
title: Durchforsten zugeordneter externer Inhaltstypen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 187ec42e-f749-4e22-abef-1df604143063
ms.openlocfilehash: c6aaedd3271255c03840d8fd7c26abe689286f2b
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="crawl-associated-external-content-types-in-sharepoint"></a><span data-ttu-id="6f912-102">Durchforsten zugeordneter externer Inhaltstypen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6f912-102">How to: Crawl associated external content types in SharePoint</span></span>

<span data-ttu-id="6f912-103">In diesem Artikel erfahren Sie, wie Sie die suchspezifischen Eigenschaften im Business Data Connectivity (BDC)-Dienst-Metadatenmodell zum Durchforsten von Zuordnungen und für die verschiedenen Benutzeroberflächen, die Sie aktivieren können, verwenden können.</span><span class="sxs-lookup"><span data-stu-id="6f912-103">Learn how to use the search specific properties in the Business Data Connectivity (BDC) service metadata model for crawling associations, and the different user experiences that you can enable.</span></span>

## <a name="crawling-the-associated-external-content-type"></a><span data-ttu-id="6f912-104">Durchforsten des zugeordneten externen Inhaltstyps</span><span class="sxs-lookup"><span data-stu-id="6f912-104">Crawling the associated external content type</span></span>
<span data-ttu-id="6f912-105"><a name="HowToCrawlAssociations_CrawlingAssociatedExternalTypes"> </a></span><span class="sxs-lookup"><span data-stu-id="6f912-105"><a name="HowToCrawlAssociations_CrawlingAssociatedExternalTypes"> </a></span></span>

<span data-ttu-id="6f912-p101">Microsoft Business Connectivity Services (BCS) können Sie zwei verwandte externe Inhaltstypen, verknüpfen, der dann Sie verwandten externen Inhalte abgerufen werden sollen können. Beispielsweise können Sie externen Inhalte von zwei SQL Server Datenbank Datenbanktabellen basierenden externen Inhaltstypen abgerufen werden, die auf Fremdschlüsseln basieren. Dieses Konzept der Verknüpfung von zwei verwandte externer Inhaltstypen wird als eine  *Zuordnung*  bezeichnet. Weitere Informationen zu Zuordnungen finden Sie unter [Hinzufügen von Zuordnungen zwischen externen Inhaltstypen](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f912-p101">Microsoft Business Connectivity Services (BCS) enables you to link two related external content types, which then enables you to fetch related external content. For example, you can fetch external content from two SQL Server database table-based external content types that are based on foreign keys. This concept of linking two related external content types is known as an  *association*  . For more information about associations, see [Adding Associations Between External Content Types](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx).</span></span> 
  
    
    
<span data-ttu-id="6f912-p102">Im Kontext von Suche Connector Framework wird der externe quellinhaltstyp eines Association-Elements als den externen Inhaltstyp für das übergeordnete bezeichnet. Der Crawler Suche kann durchforstet werden externe Inhaltstypen, die das übergeordnete Element auf zwei Arten zugeordnet sind: als Anlagen oder als untergeordnete Elemente. Diese Zuordnungen externer Inhaltstypen wirken sich auf Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6f912-p102">In the context of the Search connector framework, the source external content type of an association is referred to as the parent external content type. The Search crawler can crawl external content types that are associated with the parent in two ways: as attachments or as children. These external content type associations affect the following:</span></span>
  
    
    

- <span data-ttu-id="6f912-113">Verwendung durch den Benutzer</span><span class="sxs-lookup"><span data-stu-id="6f912-113">User experience</span></span>
    
  
- <span data-ttu-id="6f912-114">Inkrementelle Durchforstungen</span><span class="sxs-lookup"><span data-stu-id="6f912-114">Incremental crawls</span></span>
    
  
- <span data-ttu-id="6f912-115">Verarbeitung des Löschens von Durchforstungen</span><span class="sxs-lookup"><span data-stu-id="6f912-115">Processing crawl deletions</span></span>
    
  

### <a name="user-experience-effects-from-external-content-type-associations"></a><span data-ttu-id="6f912-116">Auswirkungen auf die Benutzerumgebung durch Zuordnungen externer Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="6f912-116">User experience effects from external content type associations</span></span>

<span data-ttu-id="6f912-p103">Ein untergeordneter Inhaltstyp hat ein eigene Suchergebnis-URL und Profilseite, nachdem die Profilseite erstellt wurde. Die Suchergebnis-URL ist die URL, die angezeigt wird, wenn der Benutzer in den Daten des untergeordneten externen Inhaltstyps einen Begriff sucht.</span><span class="sxs-lookup"><span data-stu-id="6f912-p103">A child external content type has its own search result URL and profile page, if the profile page has been created. The search result URL is the URL that is displayed if the user searches for a term in the child external content type data.</span></span> 
  
    
    
<span data-ttu-id="6f912-119">Der externe Inhaltstyp für eine Anlage hat keine eigene Suchergebnis-URL.</span><span class="sxs-lookup"><span data-stu-id="6f912-119">The external content type for an attachment does not have its own search result URL.</span></span> <span data-ttu-id="6f912-120">Wenn der Benutzer im externen Anlagenelement nach einem Begriff sucht, wird daher stattdessen die URL für den übergeordneten externen Inhaltstyp angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6f912-120">So if the user searches for a term in the attachment external item, the URL for the parent external content type is displayed instead.</span></span> <span data-ttu-id="6f912-121">Sie können diese URL auf die Profilseiten-URL des übergeordneten Inhaltstyps festlegen.</span><span class="sxs-lookup"><span data-stu-id="6f912-121">You can set this URL to the profile page URL of the parent.</span></span> <span data-ttu-id="6f912-122">Die Profilseite für den übergeordneten externen Inhaltstyp enthält alle Felder des externen Inhaltstyps der Anlage, die vom Zuordnungsnavigator zur Verfügung gestellt werden.</span><span class="sxs-lookup"><span data-stu-id="6f912-122">The profile page for the parent external content type will display all the fields from the attachment external content type that are exposed by the association navigator.</span></span>
  
    
    

### <a name="incremental-crawl-effects-from-external-content-type-associations"></a><span data-ttu-id="6f912-123">Effekte der inkrementellen Durchforstung aus externem Inhaltstypzuordnungen</span><span class="sxs-lookup"><span data-stu-id="6f912-123">Incremental crawl effects from external content type associations</span></span>

<span data-ttu-id="6f912-124">Untergeordnete externe Elemente werden erneut durchforstet und für zeitstempelbasierte inkrementelle Durchforstungen aktualisiert werden, wenn der Zeitstempel des untergeordneten externen Elements ändert.</span><span class="sxs-lookup"><span data-stu-id="6f912-124">Child external items are re-crawled and updated for timestamp-based incremental crawls if the timestamp of the child external item changes.</span></span> 
  
    
    
<span data-ttu-id="6f912-p105">Für externe Inhaltstypen vom Typ Anlage wird der Zeitstempel des übergeordneten externen Elements als Zeitstempel des externen Elements Anlage interpretiert. Änderungen am externen Element Anlage werden bei einer inkrementellen Durchforstung nur berücksichtigt, wenn sich der Zeitstempel des übergeordneten externen Elements ändert.</span><span class="sxs-lookup"><span data-stu-id="6f912-p105">For attachment external content types, the timestamp of the parent external item is interpreted as the timestamp of the attachment external item. This means that any changes in the attachment external item are picked up by an incremental crawl only when the timestamp of the parent external item changes.</span></span>
  
    
    

### <a name="processing-crawl-deletions-effects-from-external-content-type-associations"></a><span data-ttu-id="6f912-127">Auswirkungen auf die Verarbeitung des Löschens von Durchforstungen durch Zuordnungen externer Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="6f912-127">Processing crawl deletions effects from external content type associations</span></span>

<span data-ttu-id="6f912-128">Bei der Verarbeitung des Löschens Wenn des übergeordneten externen Inhaltstyps aus dem Index gelöscht wird, löscht der Crawler Suche die zugeordnete Anlage externe Inhaltstypen und untergeordnete externe Inhaltstypen aus dem Index.</span><span class="sxs-lookup"><span data-stu-id="6f912-128">When processing crawl deletions, if the parent external content type is deleted from the index, the Search crawler deletes the associated attachment external content types and child external content types from the index.</span></span>
  
    
    

## <a name="crawling-associated-external-content-type-attachments"></a><span data-ttu-id="6f912-129">Durchforsten des zugeordneten externen Inhaltstyps "Anlagen"</span><span class="sxs-lookup"><span data-stu-id="6f912-129">Crawling associated external content type attachments</span></span>
<span data-ttu-id="6f912-130"><a name="HowToCrawlAssociations_CrawlingAttachments"> </a></span><span class="sxs-lookup"><span data-stu-id="6f912-130"><a name="HowToCrawlAssociations_CrawlingAttachments"> </a></span></span>

<span data-ttu-id="6f912-131">Wenn Sie eine Zuordnung so markieren möchten, dass sie als Anlage durchforstet wird, fügen Sie die Eigenschaft **AttachmentAccessor** wie folgt zur Instanz der **Association**-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="6f912-131">To mark an association so that it is crawled as an attachment, add the **AttachmentAccessor** property to the **Association** method instance, as follows.</span></span>
  
    
    

```XML

<Association Name="AttachmentsNavigate Association" Type="AssociationNavigator" ...>
    <Properties>
        <Property Name="ForeignFieldMappings" Type="System.String">....... </Property>
        <Property Name="AttachmentAccessor" Type="System.String">x</Property>
    </Properties>
    <SourceEntity Namespace="ParentExternalContentType" Name="Parent" />
    <DestinationEntity Namespace="AttachmentExternalContentType" Name="Attachment External Content Type" />
</Association>
```


> <span data-ttu-id="6f912-132">**Hinweis:** Sie können einen beliebigen Wert für die Eigenschaft **AttachmentAccessor** angeben. Dieser Wert wird von der Suche nicht überprüft.</span><span class="sxs-lookup"><span data-stu-id="6f912-132">**Note:** You can specify any value for the **AttachmentAccessor** property; Search does not examine this value.</span></span>
  
    
    


## <a name="crawling-associated-external-content-types-as-child-external-content-types"></a><span data-ttu-id="6f912-133">Durchforsten zugeordneter externer Inhaltstypen als untergeordnete externe Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="6f912-133">Crawling associated external content types as child external content types</span></span>
<span data-ttu-id="6f912-134"><a name="HowToCrawlAssociations_CrawlingChildExternalTypes"> </a></span><span class="sxs-lookup"><span data-stu-id="6f912-134"><a name="HowToCrawlAssociations_CrawlingChildExternalTypes"> </a></span></span>

<span data-ttu-id="6f912-135">Fügen Sie zum Markieren einer Zuordnung, dass sie als untergeordneter Inhaltstyp durchforstet wird, die **DirectoryLink**-Eigenschaft wie folgt der Instanz der **Association**-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="6f912-135">To mark an association so that it is crawled as a child external content type, add the **DirectoryLink** property to the **Association** method instance, as follows.</span></span>
  
    
    

```XML

<Association Name="ChildrenNavigator Association" Type="AssociationNavigator" ...>
    <Properties>
        <Property Name="DirectoryLink" Type="System.String">x</Property>
    </Properties>
    <SourceEntity Namespace="ParentExternalContentType" Name="Parent" />
    <DestinationEntity Namespace="ChildExternalContentType" Name="Child External Content Type" />
</Association>
```


> <span data-ttu-id="6f912-136">**Hinweis:** Sie können einen beliebigen Wert für die Eigenschaft **DirectoryLink** angeben.</span><span class="sxs-lookup"><span data-stu-id="6f912-136">**Note:** You can specify any value for the **DirectoryLink** property.</span></span> <span data-ttu-id="6f912-137">Dieser Wert wird von der Suche nicht überprüft.</span><span class="sxs-lookup"><span data-stu-id="6f912-137">Search does not examine this value.</span></span>
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="6f912-138">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6f912-138">Additional resources</span></span>
<span data-ttu-id="6f912-139"><a name="SP15crawlects_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6f912-139"><a name="SP15crawlects_addlresources"> </a></span></span>


-  [<span data-ttu-id="6f912-140">Connector Framework für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6f912-140">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6f912-141">Hinzufügen von Zuordnungen zwischen externen Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="6f912-141">Adding Associations Between External Content Types</span></span>](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="6f912-142">Association-Element in MethodInstances (BDCMetadata-Schema)</span><span class="sxs-lookup"><span data-stu-id="6f912-142">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="6f912-143">Step 4 (Optional): Define Associations</span><span class="sxs-lookup"><span data-stu-id="6f912-143">Step 4 (Optional): Define Associations</span></span>](http://msdn.microsoft.com/library/6bc55f46-459a-4986-8744-8c6c5f45097b%28Office.15%29.aspx)
    
  

