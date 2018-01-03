---
title: Suche in Excel Services-REST-API
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e3a8e057-f803-446d-81c9-4eb8ef3691e1
ms.openlocfilehash: 3b89c557207195b675224b7be525c5fe670c20a9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="discovery-in-excel-services-rest-api"></a>Suche in Excel Services-REST-API

Dieses Thema behandelt die Ermittlungsmechanismen, die in der Excel Services-REST-API integriert sind.
  
> [!NOTE]
> Die Excel Services-REST-API kann in lokalen Bereitstellungen von SharePoint und SharePoint 2016 verwendet werden. Für Office 365 Education-, Business- und Enterprise-Konten verwenden Sie die Excel-REST-APIs, die Bestandteil des [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
)-Endpunkts sind.
  
    
    


## <a name="discovery-base-url-and-discovery-example"></a>Beispiel für Ermittlung der Basis-URL und Ermittlung

Mithilfe der Ermittlung können Entwickler und Benutzer Informationen über und den Inhalt einer Arbeitsmappe manuell oder programmgesteuert ermitteln. Der Ermittlungsmechanismus stellt den  [Atom]((http://tools.ietf.org/html/rfc4287))-Feed bereit, der Informationen über die Ressourcen in einer Arbeitsmappe enthält. Sie können mithilfe der Ermittlung die Ressourcen in der Arbeitsmappe erkunden und anzeigen. Hierzu gehören Bereiche, Diagramme, Tabellen und PivotTables.
  
    
    
Im Folgenden das Konstrukt der REST-URL zu einem einzelnen Element in einer Arbeitsmappe:
  
    
    



```

http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/<ResourceLocation>
```

Wie im Thema  [Grundlegende URI-Struktur und Pfad](basic-uri-structure-and-path.md) beschrieben, sehen Sie im Folgenden die REST-URL für den Zugriff auf die Arbeitsmappe **sampleWorkbook.xlsx** und die Anzeige des Diagramms **SampleChart**: 
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('SampleChart')
```

Zum Starten und Erkunden der Ressourcen in der Arbeitsmappe und zum Anzeigen der Ressourcen mithilfe der Ermittlung navigieren Sie mithilfe einer URL, die folgendem Beispiel entspricht, zur Modellseite:
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/<DocumentLibrary>/<FileName>/model
```

Wird die Beispielarbeitsmappe sampleWorkbook.xlsx verwendet, lautet der URI wie folgt:
  
    
    



```
http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model
```

Im Folgenden ein Screenshot der Modellseite.
  
    
    

**Excel Services REST-Modell-URL**

  
    
    

  
    
    
![Excel Services REST-Modell-URL](../images/SharePointServer14Con_XLSvcs_RESTModel.gif)
  
    
    
Die URL zur Modellseite ist der Ausgangspunkt der Ermittlung. Auf der Modellseite werden vier Ressourcenauflistungen angezeigt, die derzeit von der Excel Services-REST-API unterstützt werden. Die Ressourcenauflistungen sind Bereiche, Diagramme, Tabellen oder PivotTables. Sie können diese Ressourcen in einer bestimmten Arbeitsmappe erkunden, indem Sie auf der Modellseite auf **Bereiche**, **Diagramme**, **Tabellen** oder **PivotTables** klicken.
  
    
    
Führen Sie für den Zugriff auf das Diagramm in der Arbeitsmappe mithilfe von Ermittlung z. B. die folgenden Schritte durch: 
  
    
    

  
    
    

1. Klicken Sie auf der Modellseite auf **Diagramme**. Beim Klicken auf den Link **Diagramme** wird ein weiteres Atom-Feed geöffnet. Dieses Feed enthält alle Diagramme, die in der Beispielarbeitsmappe sampleWorkbook.xlsx verfügbar sind. Die Beispielarbeitsmappe sampleWorkbook.xlsx enthält drei Diagramme: **Diagramm 1**, **Diagramm 3** und **SampleChart**. Aus diesem Grund werden drei Diagrammnamen aufgelistet, wie im folgenden Screenshot dargestellt.
    
   **Diagrammliste der Excel Services REST-Ermittlung**

  

  ![Diagrammliste der Excel Services REST-Ermittlung](../images/19126dce-b896-4623-8686-92f2fa807283.gif)
  

  

  
2. Klicken Sie auf der Modellseite auf **SampleChart**. Dadurch wird das Diagramm namens **SampleChart** angezeigt, das sich in der Arbeitsmappe **sampleWorkbook.xlsx** befindet, wie im folgenden Screenshot gezeigt. 
    
   **Anzeigen von Diagrammen mit REST**

  

  ![Anzeigen des Diagramms über REST](../images/11734dcf-1b57-40cc-b1e8-8b10b7e5d5cb.gif)
  

  

  
3. Auf gleiche Weise wird durch Klicken auf **Chart 1** oder **Chart 3** das entsprechende Diagramm angezeigt. Wenn Sie auf **SampleChart** klicken, wird zur tatsächlichen URL des Diagramms navigiert. Im Folgenden die URL zum **SampleChart**-Bild (wie im folgenden Screenshot gezeigt):
    
```
  http://<ServerName>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('SampleChart%20')?$format=image
```


## <a name="atom-feed"></a>Atom-Feed

Mithilfe des von der REST-API bereitgestellten  [Atom]((http://tools.ietf.org/html/rfc4287))-Feeds können Sie einfacher auf die Daten zugreifen ,die für Sie von Interesse sind. Wenn Sie die Quelle der Webseite anzeigen, erhalten Sie den XML-Code. Ein Beispiel aus den Diagrammen in **sampleWorkbook.xlsx** sehen Sie unten.
  
    
    
Wie aus dem XML-Code ersichtlich ist, enthält der Feed überquerbare Elemente, anhand derer der Code ermitteln kann, welche Elemente in der Arbeitsmappe vorhanden sind. Jeder Atom-Eintrag entspricht einem Diagramm, auf das Sie zugreifen können. Dieser Mechanismus gilt in gleicher Weise für die Ermittlung von Bereichen, Tabellen und PivotTables.
  
    
    



```XML
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<feed xmlns="http://www.w3.org/2005/Atom" xmlns:x="http://schemas.microsoft.com/office/2008/07/excelservices/rest" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservice" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <title type="text">Charts</title>
  <id>http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts</id>
  <updated>2010-01-19T19:32:53Z</updated>
  <author>
    <name />
  </author>
  <link rel="self" href="http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts?$format=atom" title="Charts" />
  <entry>
    <category term="ExcelServices.Chart" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
    <title>Chart 1</title>
    <id>http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%201')</id>
    <updated>2010-01-19T19:32:53Z</updated>
    <author>
      <name />
    </author>
    <link rel="alternate" title="Chart 1" href="http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%201')?$format=image" />
    <content type="image/png" src="http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%201')?$format=image" />
  </entry>
  <entry>
    <category term="ExcelServices.Chart" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
    <title>Chart 3</title>
    <id>http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%203')</id>
    <updated>2010-01-19T19:32:53Z</updated>
    <author>
      <name />
    </author>
    <link rel="alternate" title="Chart 3" href="http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%203')?$format=image" />
    <content type="image/png" src="http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('Chart%203')?$format=image" />
  </entry>
  <entry>
    <category term="ExcelServices.Chart" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
    <title>SampleChart </title>
    <id>http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('SampleChart%20')</id>
    <updated>2010-01-19T19:32:53Z</updated>
    <author>
      <name />
    </author>
    <link rel="alternate" title="SampleChart" href="http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('SampleChart%20')?$format=image" />
    <content type="image/png" src="http://ServerName/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/model/Charts('SampleChart%20')?$format=image" />
  </entry>
</feed>
```


## <a name="see-also"></a>Siehe auch


#### <a name="concepts"></a>Konzepte


  
    
    
 [Ressourcen-URI für die REST API in Excel Services](resources-uri-for-excel-services-rest-api.md)
