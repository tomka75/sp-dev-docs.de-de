---
title: Erstellen von Suchabfragen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c4372fcc-4574-4c81-a345-a1bb282ca8f7
ms.openlocfilehash: d2dfcbbe782057d012f72ca05328316638db635f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="building-search-queries-in-sharepoint"></a>Erstellen von Suchabfragen in SharePoint
Hier erhalten Sie Informationen zur Suchsyntax, die in SharePoint zum Erstellen von Abfrageregeln und Suchabfragen unterstützt wird.
## <a name="supported-search-syntax-in-sharepoint-for-building-search-queries"></a>Unterstützte Suchsyntax in SharePoint zum Erstellen von Suchabfragen
<a name="SP15Buildquery_support"> </a>

Die SharePoint-Suche unterstützt die KQL- (Keyword Query Language) und FQL-Suchsyntax (FAST Query Language) zum Erstellen von Suchabfragen.
  
    
    
 **Keyword Query Language (KQL)**
  
    
    
KQL ist die Standardabfragesprache für die Erstellung von Suchabfragen. Mithilfe von KQL geben Sie die Suchbegriffe oder die Eigenschaftseinschränkungen an, die an den SharePoint-Suchdienst übergeben werden.
  
    
    
 **FAST Query Language (FQL)**
  
    
    
Bei FQL handelt es sich um eine strukturierte Abfragesprache, die erweiterte Abfrageoperatoren unterstützt. Mithilfe von FQL können Sie komplexe Abfragen erstellen, die dem SharePoint-Suchdienst programmgesteuert übergeben werden sollen. FQL ist nicht für Endbenutzer vorgesehen und wird standardmäßig deaktiviert. 
  
    
    
Verwenden Sie zur Aktivierung von FQL die **EnableFQL**-Eigenschaft. Kopieren Sie dann die Standardergebnisquelle, und ändern Sie die Zeichenfolge für die  `{?{searchTerms} -ContentClass=urn:content-class:SPSPeople}` auf einer der folgenden Ebenen - Suchdienstanwendung (SSA), Websitesammlung oder Website. Dazu müssen Sie eine der folgenden Methoden verwenden:
  
    
    

- Entfernen Sie den KQL-Filter,  `-ContentClass:urn:content-class:SPSPeople`, aus der Abfragetransformation. Die sich ergebende Zeichenfolge für die Abfragetransformation lautet:  `{?{searchTerms}}`
    
  
- Ersetzen Sie die Zeichenfolge für die Abfragetransformation durch ein FQL-Äquivalent wie z. B. `{?andnot({searchTerms},filter(contentclass:"urn:content-class:SPSPeople*"))}`.
    
  
Weitere Informationen zu Ergebnisquellen und deren Funktionsweise finden Sie unter:  [Informationen zu Ergebnisquellen](http://office.microsoft.com/de-DE/support/sharepoint/sharepointsearch/understanding-result-sources-HA102848849.aspx) und [Konfigurieren der Ergebnisquellen für die Suche in SharePoint](http://technet.microsoft.com/de-DE/library/jj683115%28v=office.15%29.aspx).
  
    
    

## <a name="in-this-section"></a>Inhalt dieses Abschnitts
<a name="SP15Buildquery_support"> </a>


-  [Syntaxreferenz für die Keyword Query Language (KQL)](keyword-query-language-kql-syntax-reference.md)
    
  
-  [Syntaxreferenz für FQL (FAST Query Language)](fast-query-language-fql-syntax-reference.md)
    
  
-  [Verwenden der SharePoint-Suchabfrage-APIs](using-the-sharepoint-search-query-apis.md)
    
  

## <a name="see-also"></a>Siehe auch
<a name="SP15Buildquery_addlresources"> </a>


-  [Suche in SharePoint](search-in-sharepoint.md)
    
  
-  [Übersicht über Abfrageverarbeitung in SharePoint](http://technet.microsoft.com/de-DE/library/jj219620%28v=office.15%29.aspx)
    
  
-  [Abfragevariablen in SharePoint](http://technet.microsoft.com/de-DE/library/jj683123.aspx)
    
  

