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
# <a name="crawl-associated-external-content-types-in-sharepoint"></a>Durchforsten zugeordneter externer Inhaltstypen in SharePoint

In diesem Artikel erfahren Sie, wie Sie die suchspezifischen Eigenschaften im Business Data Connectivity (BDC)-Dienst-Metadatenmodell zum Durchforsten von Zuordnungen und für die verschiedenen Benutzeroberflächen, die Sie aktivieren können, verwenden können.

## <a name="crawling-the-associated-external-content-type"></a>Durchforsten des zugeordneten externen Inhaltstyps
<a name="HowToCrawlAssociations_CrawlingAssociatedExternalTypes"> </a>

Microsoft Business Connectivity Services (BCS) können Sie zwei verwandte externe Inhaltstypen, verknüpfen, der dann Sie verwandten externen Inhalte abgerufen werden sollen können. Beispielsweise können Sie externen Inhalte von zwei SQL Server Datenbank Datenbanktabellen basierenden externen Inhaltstypen abgerufen werden, die auf Fremdschlüsseln basieren. Dieses Konzept der Verknüpfung von zwei verwandte externer Inhaltstypen wird als eine  *Zuordnung*  bezeichnet. Weitere Informationen zu Zuordnungen finden Sie unter [Hinzufügen von Zuordnungen zwischen externen Inhaltstypen](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx). 
  
    
    
Im Kontext von Suche Connector Framework wird der externe quellinhaltstyp eines Association-Elements als den externen Inhaltstyp für das übergeordnete bezeichnet. Der Crawler Suche kann durchforstet werden externe Inhaltstypen, die das übergeordnete Element auf zwei Arten zugeordnet sind: als Anlagen oder als untergeordnete Elemente. Diese Zuordnungen externer Inhaltstypen wirken sich auf Folgendes:
  
    
    

- Verwendung durch den Benutzer
    
  
- Inkrementelle Durchforstungen
    
  
- Verarbeitung des Löschens von Durchforstungen
    
  

### <a name="user-experience-effects-from-external-content-type-associations"></a>Auswirkungen auf die Benutzerumgebung durch Zuordnungen externer Inhaltstypen

Ein untergeordneter Inhaltstyp hat ein eigene Suchergebnis-URL und Profilseite, nachdem die Profilseite erstellt wurde. Die Suchergebnis-URL ist die URL, die angezeigt wird, wenn der Benutzer in den Daten des untergeordneten externen Inhaltstyps einen Begriff sucht. 
  
    
    
Der externe Inhaltstyp für eine Anlage hat keine eigene Suchergebnis-URL. Wenn der Benutzer im externen Anlagenelement nach einem Begriff sucht, wird daher stattdessen die URL für den übergeordneten externen Inhaltstyp angezeigt. Sie können diese URL auf die Profilseiten-URL des übergeordneten Inhaltstyps festlegen. Die Profilseite für den übergeordneten externen Inhaltstyp enthält alle Felder des externen Inhaltstyps der Anlage, die vom Zuordnungsnavigator zur Verfügung gestellt werden.
  
    
    

### <a name="incremental-crawl-effects-from-external-content-type-associations"></a>Effekte der inkrementellen Durchforstung aus externem Inhaltstypzuordnungen

Untergeordnete externe Elemente werden erneut durchforstet und für zeitstempelbasierte inkrementelle Durchforstungen aktualisiert werden, wenn der Zeitstempel des untergeordneten externen Elements ändert. 
  
    
    
Für externe Inhaltstypen vom Typ Anlage wird der Zeitstempel des übergeordneten externen Elements als Zeitstempel des externen Elements Anlage interpretiert. Änderungen am externen Element Anlage werden bei einer inkrementellen Durchforstung nur berücksichtigt, wenn sich der Zeitstempel des übergeordneten externen Elements ändert.
  
    
    

### <a name="processing-crawl-deletions-effects-from-external-content-type-associations"></a>Auswirkungen auf die Verarbeitung des Löschens von Durchforstungen durch Zuordnungen externer Inhaltstypen

Bei der Verarbeitung des Löschens Wenn des übergeordneten externen Inhaltstyps aus dem Index gelöscht wird, löscht der Crawler Suche die zugeordnete Anlage externe Inhaltstypen und untergeordnete externe Inhaltstypen aus dem Index.
  
    
    

## <a name="crawling-associated-external-content-type-attachments"></a>Durchforsten des zugeordneten externen Inhaltstyps "Anlagen"
<a name="HowToCrawlAssociations_CrawlingAttachments"> </a>

Wenn Sie eine Zuordnung so markieren möchten, dass sie als Anlage durchforstet wird, fügen Sie die Eigenschaft **AttachmentAccessor** wie folgt zur Instanz der **Association**-Methode hinzu.
  
    
    

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


> **Hinweis:** Sie können einen beliebigen Wert für die Eigenschaft **AttachmentAccessor** angeben. Dieser Wert wird von der Suche nicht überprüft.
  
    
    


## <a name="crawling-associated-external-content-types-as-child-external-content-types"></a>Durchforsten zugeordneter externer Inhaltstypen als untergeordnete externe Inhaltstypen
<a name="HowToCrawlAssociations_CrawlingChildExternalTypes"> </a>

Fügen Sie zum Markieren einer Zuordnung, dass sie als untergeordneter Inhaltstyp durchforstet wird, die **DirectoryLink**-Eigenschaft wie folgt der Instanz der **Association**-Methode hinzu.
  
    
    

```XML

<Association Name="ChildrenNavigator Association" Type="AssociationNavigator" ...>
    <Properties>
        <Property Name="DirectoryLink" Type="System.String">x</Property>
    </Properties>
    <SourceEntity Namespace="ParentExternalContentType" Name="Parent" />
    <DestinationEntity Namespace="ChildExternalContentType" Name="Child External Content Type" />
</Association>
```


> **Hinweis:** Sie können einen beliebigen Wert für die Eigenschaft **DirectoryLink** angeben. Dieser Wert wird von der Suche nicht überprüft.
  
    
    


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15crawlects_addlresources"> </a>


-  [Connector Framework für die Suche in SharePoint](search-connector-framework-in-sharepoint.md)
    
  
-  [Hinzufügen von Zuordnungen zwischen externen Inhaltstypen](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx)
    
  
-  [Association-Element in MethodInstances (BDCMetadata-Schema)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx)
    
  
-  [Step 4 (Optional): Define Associations](http://msdn.microsoft.com/library/6bc55f46-459a-4986-8744-8c6c5f45097b%28Office.15%29.aspx)
    
  

