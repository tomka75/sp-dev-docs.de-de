---
title: "Änderungen im BDC-Modellschema für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 882ea867-9acb-4313-99c9-865a523b72fd
ms.openlocfilehash: c95208da93af349ae768df7069c425eb088b8b30
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="changes-in-the-bdc-model-schema-for-sharepoint"></a>Änderungen im BDC-Modellschema für SharePoint
Hier erfahren Sie, was in SharePoint für das BDC-Modellschema geändert hat. Die Anzahl der Änderungen im Schema (BDCMetadata.xsd) für das Erstellen von BDC-Modelle auf SharePoint ist relativ gering. Aber diese Änderungen erhebliche Auswirkungen auf das Feature Angebote von Business Connectivity Services (BCS) festgelegt haben.
  
    
    

Weitere Informationen zum BDCMetadata-Schema finden Sie unter  [BDC-Modell-Schemareferenz für SharePoint](bdc-model-schema-reference-for-sharepoint.md).
## <a name="changes-to-complex-type-elements-in-bdcmetadataxsd"></a>Änderungen an den komplexen Typelemente in BDCMetadata.xsd
<a name="bkmk_ChangesToElements"> </a>

In der folgenden Tabelle zeigt, welche Änderungen an den Elemente der obersten Ebene im BDCMetadata-Schema vorgenommen wurden.
  
    
    

**In Tabelle 1. Neue komplexe Typen**


|**Element**|**Beschreibung**|
|:-----|:-----|
|IndividuallySecurableMetadataObject  <br/> |Verwendet, um festzulegen, dass die angegebenen **MetadataObject** explizit gesichert werden kann und nicht über seine Zuordnung zu seinem übergeordneten Element. <br/> |
|MetadataObject  <br/> |Zum Speichern der zusätzlichen Metadaten für die Verbindung mit der externen Datenquelle verwendet.  <br/> |
   

## <a name="changes-to-simple-type-elements-in-bdcmetadataxsd"></a>Änderungen an den einfachen Typ der Elemente in BDCMetadata.xsd
<a name="bkmk_ChangesToSimpleTypes"> </a>

Die folgende Tabelle enthält die Änderungen, die an die Attribute der einzelnen Elemente vorgenommen wurden.
  
    
    

**In Tabelle 2. Änderungen an einfache Typen**


|**Element**|**Beschreibung**|
|:-----|:-----|
|Keine Änderungen  <br/> ||
   

## <a name="changes-to-attributes-in-bdcmetadataxsd"></a>Ändern von Attributen in BDCMetadata.xsd
<a name="bkmk_ChangesToAttributes"> </a>

Die folgende Tabelle enthält die Änderungen an der Attribute der einzelnen Elemente.
  
    
    

**Tabelle 3. Ändern von Attributen**


|**Attribut**|**Übergeordneter Schlüssel**|**Beschreibung**|
|:-----|:-----|:-----|
|Keine Änderungen  <br/> |||
   

## <a name="see-also"></a>Siehe auch
<a name="bkmk_AdditionalResources"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Erste Schritte mit den Business Connectivity Services in SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Business Connectivity Services-Programmierreferenz für SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [BDC-Modell-Schemareferenz für SharePoint](bdc-model-schema-reference-for-sharepoint.md)
    
  

