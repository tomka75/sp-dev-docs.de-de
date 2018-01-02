---
title: "Nicht unterstützte Features in Excel Services-REST-API"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4139901f-255b-4556-b8c8-3d986a07c587
ms.openlocfilehash: 1e8bf0ba8947391e0479aded0086a8c836ce38bb
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="unsupported-features-in-excel-services-rest-api"></a>Nicht unterstützte Features in Excel Services-REST-API

Die erste Version der Excel Services-REST-API unterstützt nicht alle Excel-Features. 
  
> [!NOTE] 
> Die Excel Services-REST-API kann in lokalen Bereitstellungen von SharePoint und SharePoint 2016 verwendet werden. Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
)-Endpunkts sind.
  
    
    


Es folgt eine partielle Liste einiger wichtiger Features, die derzeit nicht unterstützt werden oder in der REST-API Excel Services arbeiten:
  
    
    


- **Keine unverankerten Diagramme.** Wenn ein Bereich ein Diagramm enthält und Sie den Bereich über REST anfordern, erhalten Sie nur den Bereich.
    
  
- **Keine Sparklines, keine bedingte Formatierung für Symbole.** Derzeit nicht unterstützt.
    
  
- **Keine Pixelperfektion mit EWA.** Das von REST produzierte HTML ist dem von Excel Web Access produzierten HTML sehr ähnlich. Mit der REST-API in Excel Services kann jedoch nicht auf alle CSS-Elemente (Cascading Stylesheets) zugegriffen werden, auf die Excel Web Access Zugriff hat. Die REST-API in Excel Services gibt ein HTML-Fragment zurück. Das HTML-Fragment muss eigenständig sein.
    
  
- **Keine Unterscheidung in Tabellen.** Wenn eine Tabelle als ATOM angefordert wird, kann nicht festgestellt werden, ob es sich bei der Zelle oder den Daten um eine Spaltenüberschrift, eine Summe oder allgemeine Daten handelt. In der Tabelle wird diesbezüglich nämlich keine Unterscheidung gemacht. Alle Tabellenzeilen in der gesamten Tabelle werden gleich behandelt.
    
  
- **URL-Größenbeschränkungen.** Die URL-Größe ist auf etwa 2000 Zeichen begrenzt. Das heißt, wenn in einer Arbeitsmappe sehr viele Parameter vorhanden sind, können Sie möglicherweise nicht alle Parameter festlegen. Dies gilt insbesondere, wenn die Arbeitsmappe tief in der Hierarchie einer Ordnerstruktur angeordnet ist.
    
  
- **Sonderzeichen.** Zeichen wie "?" und "#" werden nicht unterstützt. Um ordnungsgemäß auf Blattnamen zu verweisen, die Sonderzeichen enthalten, gilt die Grundregel "Feststellen, was der Excel-Client macht", wenn Sie in einer Formel auf ein Blatt mit Sonderzeichen verweisen, und diesem Beispiel folgen.
    
  

