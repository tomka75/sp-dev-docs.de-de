---
title: "Ressourcen-URI für Excel Services-REST-API"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 79f95305-ec9e-4842-b937-85f66ced98e4
ms.openlocfilehash: 01b264b2e668e3779df8fcc08c70142241f7f8db
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="resources-uri-for-excel-services-rest-api"></a>Ressourcen-URI für Excel Services-REST-API

Mit der REST-API in Excel Services können Sie eine direkte Verknüpfung zu Entitäten herstellen.
  
    
    


> **Hinweis:** Die Excel Services-REST-API bezieht sich auf SharePoint und SharePoint 2016 (lokal). Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
> )-Endpunkts sind.
  
    
    


## <a name="base-rest-url"></a>Basis-REST-URL

Es folgt ein Beispiel für eine REST-URL zu einem bestimmten Element in einer Arbeitsmappe.
  
    
    

```

http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/<ResourceLocation>
```

Deaktiviert die Basis-REST-URL ist eine relative URL der REST basiert. Es folgt ein Beispiel für ein Basis-REST-URL zu einer bestimmten Arbeitsmappe.
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>
```

Angenommen, Sie verfügen über eine Arbeitsmappe mit dem Namen „sampleWorkbook.xlsx“ in der folgenden Dokumentbibliothek:  
  
    
    



```
http://<ServerName>/Docs/Documents/sampleWorkbook.xlsx
```

Die Basis-REST-URL zur Arbeitsmappe lautet wie folgt:
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx
```


## <a name="resources-uri"></a>Ressourcen-URI

In Tabelle 1 sind alle Ressourcen in der REST-API in Excel Services aufgeführt, auf die zugegriffen werden kann. Für den Zugriff auf eine bestimmte Ressource fügen Sie den Ressourcenspeicherort an die Basis-REST-URL zu einer Arbeitsmappe an.
  
    
    

**Tabelle 1. Ressourcen, auf die in der Excel Services-REST-API zugegriffen werden kann**


|**Speicherort der Ressource**|**Format**|**Beispiel**|**Hinweise**|
|:-----|:-----|:-----|:-----|
|/model  <br/> |Atom (Standard)  <br/> |/model  <br/> |Gibt einen ATOM-Feed mit den von der REST-API in Excel Services unterstützten Ressourcen zurück. Zu den unterstützten Ressourcen zählen Bereiche, Diagramme, Tabellen und PivotTables.  <br/> |
|/model  <br/> |Arbeitsmappe  <br/> |/model?$format=workbook  <br/> |Dies ist die Arbeitsmappe. Unterstützte Arbeitsmappenformate sind XLSX, XLSB und XLSM.  <br/> |
|/model/Ranges  <br/> |Atom (Standard)  <br/> |/model/Ranges?$format=atom  <br/> |Ein ATOM-Feed, der alle benannten Bereiche in der Arbeitsmappe auflistet.  <br/> |
|/model/Ranges('[Name]')  <br/> |HTML (Standard)  <br/> |/model/Ranges('MyRange')?$format=html  <br/> |Ein HTML-Fragment für den angeforderten Bereich.  <br/> |
|/model/Ranges('[Name]')  <br/> |Atom  <br/> |/model/Ranges('MyRange')?$format=atom  <br/> |Ein ATOM-Eintrag, der eine XML-Darstellung der Daten in diesem Bereich enthält.  <br/> |
|/model/Charts  <br/> |Atom (Standard)  <br/> |/model/Charts?$format=atom  <br/> |Ein ATOM-Feed, der alle Diagramme in der Arbeitsmappe auflistet.  <br/> |
|/model/Charts('[Name]')  <br/> |Bild (Standard)  <br/> |/model/Charts('MyChart')?$format=image  <br/> |Ein Bild des Diagramms. Das Bild hat das PNG-Format (Portable Network Graphics).  <br/> |
|/model/Tables  <br/> |Atom (Standard)  <br/> |/model/Tables?$format=atom  <br/> |Ein ATOM-Feed, der alle verfügbaren Tabellen in der Arbeitsmappe auflistet.  <br/> |
|/model/Tables('[Name]')  <br/> |HTML (Standard)  <br/> |/model/Tables('MyTable')?$format=html  <br/> |Ein HTML-Fragment für die angeforderte Tabelle.  <br/> |
|/model/Tables('[Name]')  <br/> |Atom  <br/> |/model/Tables('MyTable')?$format=atom  <br/> |Ein ATOM-Eintrag, der eine XML-Darstellung der Daten in dieser Tabelle enthält.  <br/> |
|/model/PivotTables  <br/> |Atom (Standard)  <br/> |/model/PivotTables?$format=atom  <br/> |Ein ATOM-Feed, der alle verfügbaren PivotTables in der Arbeitsmappe auflistet.  <br/> |
|/model/PivotTables('[Name]')  <br/> |HTML (Standard)  <br/> |/model/PivotTables('MyPivotTable)?$format=html  <br/> |Ein HTML-Fragment für die angeforderte PivotTable.  <br/> |
|/model/PivotTables('[Name]')  <br/> |Atom  <br/> |/model/PivotTables('MyPivotTable')?$format=atom  <br/> |Ein Atom-Eintrag, der eine XML-Darstellung der Daten aus den PivotTables enthält.  <br/> |
   

> **Hinweis:** Excel Services begrenzt die Anzahl der Bereiche, die Sie in eine URL einfügen können auf 10. Wenn Sie mehr als 10 Bereiche in eine URL einfügen, erhalten Sie eine Fehlermeldung, die darauf hinweist, dass der Dienst nicht verfügbar ist. 
  
    
    


## <a name="see-also"></a>Siehe auch


#### <a name="concepts"></a>Konzepte


  
    
    
 [Grundlegende URI-Struktur und Pfad](basic-uri-structure-and-path.md)
