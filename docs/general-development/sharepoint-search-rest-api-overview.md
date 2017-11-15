---
title: "Übersicht über die REST-API der SharePoint-Suche"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d0684be67a04f79cea059564390918be084d9eaf
ms.sourcegitcommit: d68d6cf927d69696a3561f7d8ffe9a3ed9dbd03c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="sharepoint-search-rest-api-overview"></a>Übersicht über die REST-API der SharePoint-Suche
Fügen Sie Suchfunktionen zu Client- und mobilen Anwendungen hinzu, mit dem Search-REST-Dienst in SharePoint und jeder Technologie, die REST-Webanforderungen unterstützt.
## <a name="querying-with-the-search-rest-service"></a>Erstellen von Abfragen mit dem Search-REST-Dienst
<a name="bk_queryrest"> </a>

Suche in SharePoint enthält einen Search-REST-Dienst, mit dem Sie Suchfunktionen zu Ihren Client- und mobilen Anwendungen hinzufügen können. Verwenden sie dazu eine beliebige Technologie, die REST-Webanforderungen unterstützt. Mit dem Search-REST-Dienst können Sie Keyword Query Language (KQL)- oder FAST Query Language (FQL)-Abfragen in Ihren SharePoint-Add-Ins, Remoteclient-Anwendungen, mobilen Anwendungen und anderen Anwendungen senden.
  
    
    
Der Search-REST-Dienst unterstützt **POST**- und **GET**-HTTP-Anforderungen.
  
    
    

### <a name="get-requests"></a>GET-Anforderungen

Erstellen Sie den URI für **GET**Abfrageanforderungen hinsichtlich des Search-REST-Diensts wie folgt:
  
    
    
 `/_api/search/query`
  
    
    
Für **GET**-Anforderungen geben Sie die Abfrageparameter in der URL an. Sie können die **GET**-Anforderungs-URL auf zwei Arten erstellen:
  
    
    


  
    
    
>  `http://server/_api/search/query?query_parameter=value&amp;query_parameter=value`
    
  

  
    
    
>  `http://server/_api/search/query(query_parameter=value&amp;query_parameter=<value>)`
    
  

### <a name="post-requests"></a>POST-Anforderungen

Sie erstellen den URI für **POST**-Abfrageanforderungen hinsichtlich des Search-REST-Diensts wie folgt:
  
    
    
 `/_api/search/postquery`
  
    
    
Für **POST**-Anforderungen geben Sie die Abfrageparameter in der Anforderung im JavaScript Object Notation (JSON)-Format weiter.
  
    
    
Die **POST**-HTTP-Version des Search-REST-Diensts unterstützt alle Parameter, die von der **GET**-HTTP-Version unterstützt werden. Einige der Parameter weisen jedoch unterschiedliche Datentypen auf, wie in Tabelle 1 beschrieben.
  
    
    

**Tabelle 1. Abfrageparameter mit unterschiedlichen Datentypen für POST-Anforderungen**


|**Parameter**|**Datentyp**|
|:-----|:-----|
| [SelectProperties](#bk_SelectProperties) <br/> |string[]  <br/> |
| [RefinementFilters](#bk_RefinementFilters) <br/> |string[]  <br/> |
| [SortList](#bk_SortList) <br/> | [Sort](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.Sort.aspx) <br/> |
| [HithighlightedProperties](#bk_HithighlightedProperties) <br/> |string[]  <br/> |
| [Properties](#bk_Properties) <br/> | [Microsoft.SharePoint.Client.Search.Query.KeywordQueryProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.KeywordQueryProperties.aspx) <br/> |
   
Verwenden Sie **POST**-Anforderungen in den folgenden Szenarios:
  
    
    

- Bei Überschreitung der URL-Längenbeschränkung für eine **GET**-Anforderung
    
  
- Wenn Sie die Abfrageparameter nicht in einer einfachen URL angeben können. Wenn Sie beispielsweise Parameterwerte weitergeben müssen, die ein Array eines komplexen Typs oder durch Kommas getrennte Zeichenfolgen enthalten, sind Sie bei der Erstellung der **POST**-Anforderung flexibler.
    
  
- Bei Verwendung des  [ReorderingRules](#bk_ReorderingRules)-Parameters, da er nur für **POST**-Anforderungen unterstützt wird
    
  

## <a name="using-query-parameters-with-the-search-rest-service"></a>Verwenden von Abfrageparametern für den Search-REST-Dienst
<a name="bk_UsingQueryParams"> </a>

Wenn Sie den Search-REST-Dienst aufrufen, geben Sie Abfrageparameter für die Anforderung an. Suche in SharePoint verwendet diese Abfrageparameter, um die Suchabfrage zu erstellen. Für eine **GET**-Anforderung geben Sie die Abfrageparameter in der URL an. Für **POST**-Anforderungen geben Sie die Abfrageparameter im Textkörper im JavaScript Object Notation (JSON)-Format weiter.
  
    
    
In den folgenden Abschnitten werden die Abfrageparameter beschrieben, mit denen Sie Suchabfragen mit dem Search-REST-Dienst senden können.
  
    
    

### <a name="querytext-parameter"></a>QueryText-Parameter

Eine Zeichenfolge, die den Text für die Suchabfrage enthält
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'
  
    
    
 **Beispiel für POST-Anforderung**

```JSON
{
    'request': {
         'Querytext': 'sharepoint',
         'RowLimit':20, 
         'ClientType':'ContentSearchRegular'
         }
}
```


### <a name="querytemplate"></a>QueryTemplate
<a name="bk_QueryTemplate"> </a>

Eine Zeichenfolge, die den Text enthält, der den Abfragetext ersetzt (als Teil einer Abfragetransformation)
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http://server/_api/search/query?querytext='sharepoint'&amp;querytemplate='{searchterms} author:johndoe'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'Querytemplate' : '{searchterms} Author:johndoe'
}
```


### <a name="enableinterleaving"></a>EnableInterleaving
<a name="bk_EnableInterleaving"> </a>

Ein boolescher Wert, der angibt, ob die für den Ergebnisblock zurückgegebenen Ergebnistabellen mit den für die ursprüngliche Abfrage zurückgegebenen Ergebnistabellen kombiniert werden 
  
    
    
 **true** zum Kombinieren der Ergebnistabellen; andernfalls **false**. Der Standardwert ist **true**. 
  
    
    
Ändern Sie diesen Wert nur, wenn Sie Ihre eigene überlappende Implementierung bereitstellen möchten.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableinterleaving=true
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableInterleaving' : 'True'
}
```


### <a name="sourceid"></a>SourceId
<a name="bk_SourceId"> </a>

Ergebnis-Quell-ID für Ausführung der Suchabfrage
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;sourceid='8413cd39-2156-4e00-b54d-11efd9abdb89'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'SourceId' : '8413cd39-2156-4e00-b54d-11efd9abdb89'
}
```


### <a name="rankingmodelid"></a>RankingModelId
<a name="bk_RankingModelId"> </a>

ID des Rangfolgemodells für die Abfrage
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;rankingmodelid= _CustomRankingModelID_
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RankingModelId' : 'CustomRankingModelID '
}
```


### <a name="startrow"></a>StartRow
<a name="bk_StartRow"> </a>

Erste Zeile, die in den Suchergebnissen enthalten ist, die zurückgegeben werden. Verwenden Sie diesen Parameter, wenn Sie die Seitenverwaltung für Suchergebnisse implementieren möchten.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;startrow=10
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'StartRow' : '10'
}
```


### <a name="rowlimit"></a>RowLimit
<a name="bk_RowLimit"> </a>

Maximale Anzahl von Zeilen, die in den Suchergebnissen zurückgegeben werden. Verglichen mit  _RowsPerPage_ ist _RowLimit_ die maximale Anzahl zurückgegebener Zeilen.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowlimit=30
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RowLimit' : '30'
}
```


### <a name="rowsperpage"></a>RowsPerPage
<a name="bk_RowsPerPage"> </a>

Maximale Anzahl von Zeilen, die pro Seite zurückgegeben werden. Verglichen mit  _RowLimit_ bezieht sich _RowsPerPage_ auf die maximale Anzahl von Zeilen, die pro Seite zurückgegeben werden. "RowsPerPage" wird hauptsächlich verwendet, wenn Sie die Seitenverwaltung für Suchergebnisse implementieren möchten.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowsperpage=10
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RowsPerPage' : '10'
}
```


### <a name="selectproperties"></a>SelectProperties
<a name="bk_SelectProperties"> </a>

Verwaltete Eigenschaften, die in den Suchergebnissen zurückgegeben werden. Um eine verwaltete Eigenschaft zurückzugeben, stellen Sie das abrufbare Flag der Eigenschaft im Suchschema auf **true** ein.
  
    
    
Für **GET**-Anforderungen können Sie den  _SelectProperties_-Parameter in einer Zeichenfolge mit einer durch Kommas getrennten Liste von Eigenschaften angeben. Für **POST**-Anforderungen geben Sie den  _SelectProperties_-Parameter als Zeichenfolgenarray an.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;selectproperties='Title,Author'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'SelectProperties' : {
    'results' : [
          'Title,
          Author'
          ]
}
}
```


### <a name="culture"></a>Culture
<a name="bk_Culture"> </a>

Gebietsschema-ID (LCID) für die Abfrage (siehe  [Von Microsoft zugewiesene Gebietsschema-IDs](http://msdn.microsoft.com/en-us/goglobal/bb964664.aspx)).
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;culture=1044
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'Culture' : '1044'
}
```


### <a name="refinementfilters"></a>RefinementFilters
<a name="bk_RefinementFilters"> </a>

Satz an Verfeinerungsfiltern für das Senden einer Verfeinerungsabfrage. Für **GET**-Anforderungen wird der  _RefinementFilters_-Parameter als FQL-Filter angegeben. Für **POST**-Anforderungen wird der  _RefinementFilters_-Parameter als Array von FQL-Filtern angegeben.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;refinementfilters='fileExtension:equals("docx")'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RefinementFilters' : {
'results' : ['fileExtension:equals("docx")']
}
}
```


### <a name="refiners"></a>Einschränkungen
<a name="bk_Refiners"> </a>

Satz an Einschränkungen, die in einem Suchergebnis zurückgegeben werden
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;refiners='author,size'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'Refiners': {
'results' : ['author,size']
}
}
```


### <a name="hiddenconstraints"></a>HiddenConstraints
<a name="bk_HiddenConstraints"> </a>

Zusätzliche Abfrageausdrücke zum Anhängen an die Abfrage
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;hiddenconstraints='developer'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'HiddenConstraints':'developer'
}
```


### <a name="sortlist"></a>SortList
<a name="bk_SortList"> </a>

Liste der Eigenschaften, nach der die Suchergebnisse sortiert sind
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;sortlist='rank:descending,modifiedby:ascending'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'SortList' : 
{
    'results' : [
        {
                'Property':'Created',
                'Direction': '0'
        },
        {
                'Property':'FileExtension',
                'Direction': '1'
        }
    ]
}
}
```


### <a name="enablestemming"></a>EnableStemming
<a name="bk_EnableStemming"> </a>

Ein boolescher Wert, der angibt, ob Wortstammerkennung aktiviert ist 
  
    
    
 **true**, wenn Wortstammerkennung aktiviert ist; andernfalls **false**. Der Standardwert ist **true**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablestemming=false
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableStemming : 'False'
}
```


### <a name="trimduplicates"></a>TrimDuplicates
<a name="bk_TrimDuplicates"> </a>

Ein boolescher Wert, der angibt, ob doppelte Elemente aus den Ergebnissen entfernt werden 
  
    
    
 **true**, um doppelte Elemente zu entfernen; andernfalls **false**. Der Standardwert ist **true**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;trimduplicates=false
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'TrimDuplicates':'False'
}
```


### <a name="timeout"></a>Timeout
<a name="bk_Timeout"> </a>

Zeit in Millisekunden bis zum Timeout der Abfrageanforderung. Der Standardwert ist 30000.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;timeout=60000
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'Timeout':'60000'
}
```


### <a name="enablenicknames"></a>EnableNicknames
<a name="bk_EnableNicknames"> </a>

Ein boolescher Wert, der angibt, ob die genauen Ausdrücke in der Suchabfrage verwendet werden, um Übereinstimmungen zu finden, oder ob auch Spitznamen verwendet werden 
  
    
    
 **true**, wenn Spitznamen verwendet werden; andernfalls **false**. Der Standardwert ist **false**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablenicknames=true
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'EnableNicknames':'True'
}
```


### <a name="enablephonetic"></a>EnablePhonetic
<a name="bk_EnablePhonetic"> </a>

Ein boolescher Wert, der angibt, ob die phonetische Form der Abfrageausdrücke verwendet wird, um Übereinstimmungen zu finden 
  
    
    
 **true**, wenn die phonetische Form verwendet wird; andernfalls **false**. Der Standardwert ist **false**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablephonetic=true
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'EnablePhonetic':'True'
}
```


### <a name="enablefql"></a>EnableFql
<a name="bk_EnableFql"> </a>

Ein boolescher Wert, der angibt, ob die Abfrage die FAST Query Language (FQL) verwendet 
  
    
    
 **true**, wenn die Abfrage eine FQL-Abfrage ist; andernfalls **false**. Der Standardwert ist **false**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablefql=true
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'EnableFQL':'True'
}
```


### <a name="hithighlightedproperties"></a>HithighlightedProperties
<a name="bk_HithighlightedProperties"> </a>

Eigenschaften zur Hervorhebung in der Suchergebnisübersicht, wenn der Eigenschaftenwert den vom Benutzer eingegebenen Suchbegriffen entspricht. Für **GET**-Anforderungen geben Sie eine Zeichenfolge mit einer durch Kommas getrennten Liste von Eigenschaften an. Für **POST**-Anforderungen geben Sie ein Array von Zeichenfolgen an.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedproperties='Title'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'HitHighlightedProperties' :  {
    'results' : [
         'Title'   
    ]
}
}
```


### <a name="bypassresulttypes"></a>BypassResultTypes
<a name="bk_BypassResultTypes"> </a>

Ein boolescher Wert, der angibt, ob eine Ergebnistypverarbeitung für die Abfrage durchgeführt werden soll 
  
    
    
 **true**, um eine Ereignistypverarbeitung durchzuführen; andernfalls **false**. Der Standardwert ist **false**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;bypassresulttypes=true
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'BypassResultTypes' : 'true'
}
```


### <a name="processbestbets"></a>ProcessBestBets
<a name="bk_ProcessBestBets"> </a>

Ein boolescher Wert, der angibt, ob die besten Suchergebnisse für die Abfrage zurückgegeben werden sollen 
  
    
    
 **true**, um die besten Suchergebnisse zurückzugeben; andernfalls **false**. Dieser Parameter wird nur verwendet, wenn **EnableQueryRules** auf **true** festgelegt ist. Andernfalls wird er ignoriert. Der Standardwert ist **false**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;processbestbets=true&amp;enablequeryrules=true
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'ProcessBestBets' : 'true',
'EnableQueryRules' : 'true'
}
```


### <a name="clienttype"></a>ClientType
<a name="bk_ClientType"> </a>

Typ des Clients, der die Abfrage gesendet hat
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;clienttype='custom'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'ClientType':'custom'
}
```


### <a name="personalizationdata"></a>PersonalizationData
<a name="bk_PersonalizationData"> </a>

GUID für den Benutzer, der die Suchabfrage gesendet hat
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _\<server\>_/_api/search/query?querytext='sharepoint'&amp;personalizationdata=' _\<GUID\>_'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'PersonalizationData' : ' <GUID> '
}
```


### <a name="resultsurl"></a>ResultsURL
<a name="bk_ResultsURL"> </a>

URL für die Seite mit den Suchergebnissen
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;resultsurl='http://server/site/resultspage.aspx'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint'
'ResultURL' : 'http://server/site/resultspage.aspx'
}
```


### <a name="querytag"></a>QueryTag
<a name="bk_QueryTag"> </a>

Benutzerdefinierte Tags, die die Abfrage identifizieren. Sie können mehrere Abfrage-Tags angeben, getrennt durch Semikolons.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint'
}
```


### <a name="properties"></a>Eigenschaften
<a name="bk_Properties"> </a>

Zusätzliche Eigenschaften für die Abfrage. **GET**-Anforderungen unterstützen nur Zeichenfolgewerte. **POST**-Anforderungen unterstützen Werte jedes Typs.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;properties='termid:guid'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'Properties' : {
     'results' : [
          {
               'Name' : 'sampleBooleanProperty',
               'Value' :
               {
                    'BoolVal' : 'True',
                    'QueryPropertyValueTypeIndex' : 3
               }
          },
          {
               'Name' : 'sampleIntProperty',
               'Value' : 
               {
                    'IntVal' : '1234',
                    'QueryPropertyValueTypeIndex' : 2
               }
          }
     ]
}
}
```


> **Hinweis:** [QueryPropertyValueType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.QueryPropertyValueType.aspx) gibt den Typ der Eigenschaft an. Jeder Typ weist einen bestimmten Indexwert auf.
  
    
    


### <a name="enablequeryrules"></a>EnableQueryRules
<a name="bk_EnableQueryRules"> </a>

Ein boolescher Wert, der angibt, ob Abfrageregeln für die Abfrage aktiviert werden 
  
    
    
 **true**, um Abfrageregeln zu aktivieren; andernfalls **false**. Der Standardwert ist **true**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablequeryrules=false
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableQueryRules' : 'false' 
}
```


### <a name="reorderingrules"></a>ReorderingRules
<a name="bk_ReorderingRules"> </a>

Spezielle Regeln für die Neuanordnung der Suchergebnisse. Diese Regeln können angeben, dass Dokumente, die bestimmte Bedingungen erfüllen, weiter oben oder unten in den Ergebnissen platziert werden. Diese Eigenschaft wird nur angewendet, wenn die Suchergebnisse basierend auf dem Rang sortiert sind. Sie müssen eine **POST**-Anforderung für diese Eigenschaft verwenden; dies funktioniert nicht für eine **GET**-Anforderung.
  
    
    
Im folgenden Beispiel bezieht sich  _MatchType_ auf [ReorderingRuleMatchType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.aspx) . Im folgenden Beispiel spezifiziert `'MatchType' : '0'` Folgendes: [ResultContainsKeyword](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.ResultContainsKeyword.aspx) .
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'ReorderingRules' :  {
    'results' : [
         {
             'MatchValue' : '<someValue>',
             'Boost' : '10',
             'MatchType' : '0'
         }
    ]
}
}
```


### <a name="processpersonalfavorites"></a>ProcessPersonalFavorites
<a name="bk_ProcessPersonalFavorites"> </a>

Ein boolescher Wert, der angibt, ob persönliche Favoriten in den Suchergebnissen zurückgegeben werden 
  
    
    
 **true**, um persönliche Favoriten zurückzugeben; andernfalls **false**. 
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;processpersonalfavorites=true
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'ProcessPersonalFavorites' : 'false'
}
```


### <a name="querytemplatepropertiesurl"></a>QueryTemplatePropertiesUrl
<a name="bk_ProcessPersonalFavorites"> </a>

Speicherort der Datei queryparametertemplate.xml. Diese Datei wird verwendet, um anonymen Benutzern das Senden von Search-REST-Abfragen zu ermöglichen.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;querytemplatepropertiesurl='spfile://webroot/queryparametertemplate.xml'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
QueryTemplatePropertiesUrl : 'spfile://webroot/queryparametertemplate.xml'
}
```


### <a name="hithighlightedmultivaluepropertylimit"></a>HitHighlightedMultivaluePropertyLimit
<a name="bk_ProcessPersonalFavorites"> </a>

Anzahl der Eigenschaften für die Anzeige der Treffermarkierung in den Suchergebnissen
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedmultivaluepropertylimit=2
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'HitHighlihtedMultivaluePropertyLimit' : '2'
}
```


### <a name="enableorderinghithighlightedproperty"></a>EnableOrderingHitHighlightedProperty
<a name="bk_ProcessPersonalFavorites"> </a>

Ein boolescher Wert, der angibt, ob die Eigenschaften für die Treffermarkierung sortiert werden können 
  
    
    
 **true**, um Sortierungsregeln zu aktivieren; andernfalls **false**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableorderinghithighlightedproperty=false
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableOrderingHitHighlightedProperty' : 'false'
}
```


### <a name="collapsespecification"></a>CollapseSpecification
<a name="bk_ProcessPersonalFavorites"> </a>

Verwaltete Eigenschaften zum Reduzieren einzelner Suchergebnisse. Ergebnisse werden auf ein Ergebnis oder eine angegebene Anzahl von Ergebnissen reduziert, wenn sie beliebigen individuellen Reduzierungsspezifikationen entsprechen. In einer einzelnen Reduzierungsspezifikation werden die Ergebnisse reduziert, wenn ihre Eigenschaften allen individuellen Eigenschaften in der Reduzierungsspezifikation entsprechen.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;collapsespecification='Author:1 ContentType:2'
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'CollapseSpecification' : 'Author:1 ContentType:2'
}
```


### <a name="enablesorting"></a>EnableSorting
<a name="bk_ProcessPersonalFavorites"> </a>

Ein boolescher Wert, der angibt, ob die Suchergebnisse sortiert werden 
  
    
    
I **true**, um die Suchergebnisse mit  _SortList_ oder nach Rang zu sortieren, wenn _SortList_ leer ist. **false**, um die Ergebnisse nicht zu sortieren.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablesorting=false
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableSorting' : 'false'
}
```


### <a name="generateblockranklog"></a>GenerateBlockRankLog
<a name="bk_ProcessPersonalFavorites"> </a>

Ein boolescher Wert, der angibt, ob Blockrang-Protokollinformationen in der Eigenschaft **BlockRankLog** der überlappenden Ergebnistabelle zurückgegeben werden. Ein Blockrang-Protokoll enthält die Textinformationen zur Blockbewertung und die Dokumente, die dedupliziert wurden.
  
    
    
 **true**, um Blockrang-Protokollinformationen zurückzugeben; andernfalls **false**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;generateblockranklog=true
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'GenerateBlockRankLog' : 'true'
}
```


### <a name="uilanguage"></a>UIlanguage
<a name="bk_ProcessPersonalFavorites"> </a>

Gebietsschema-ID (LCID) der Benutzeroberfläche (siehe  [Von Microsoft zugewiesene Gebietsschema-IDs](http://msdn.microsoft.com/en-us/goglobal/bb964664)).
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;uilanguage=1044
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'UILanguage' : '1044'
}
```


### <a name="desiredsnippetlength"></a>DesiredSnippetLength
<a name="bk_ProcessPersonalFavorites"> </a>

Bevorzugte Anzahl von Zeichen in der Treffermarkierungsübersicht für ein Suchergebnis
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;desiredsnippetlength=80
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'DesiredSnippetLength' : '80'
}
```


### <a name="maxsnippetlength"></a>MaxSnippetLength
<a name="bk_ProcessPersonalFavorites"> </a>

Maximale Anzahl von Zeichen in der Treffermarkierungsübersicht für ein Suchergebnis
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;maxsnippetlength=100
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'MaxSnippetLength' : '100' 
}
```


### <a name="summarylength"></a>SummaryLength
<a name="bk_ProcessPersonalFavorites"> </a>

Anzahl der Zeichen in der Ergebnisübersicht für ein Suchergebnis
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/query?querytext='sharepoint'&amp;summarylength=150
  
    
    
 **Beispiel für POST-Anforderung**
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'Summarylength' : '150'
}
```


## <a name="enabling-anonymous-search-rest-queries"></a>Ermöglichen anonymer Search-REST-Abfragen
<a name="bk_AnonymousREST"> </a>

Sie können die Suche konfigurieren, um Search-REST-Abfragen von anonymen Benutzern zu unterstützen. Websiteadministratoren können entscheiden, welche Abfrageparameter unter Verwendung der Datei queryparametertemplate.xml anonymen Benutzern zur Verfügung gestellt werden. Dieser Abschnitt beschreibt die Konfiguration Ihrer Website, um anonymen Zugriff zu ermöglichen und die Datei queryparametertemplate.xml zu erstellen.
  
    
    

### <a name="to-enable-anonymous-search-rest-queries"></a>So ermöglichen Sie anonyme Search-REST-Abfragen


1. Ermöglichen Sie den anonymen Zugriff auf die Webanwendung und Veröffentlichungswebsite. Weitere Informationen erhalten Sie unter  [Verwalten von Berechtigungsrichtlinien für eine Webanwendung in SharePoint](http://technet.microsoft.com/en-us/library/ff608071.aspx) und [Planen der Benutzerauthentifizierungsmethoden in SharePoint](http://technet.microsoft.com/en-us/library/cc262350.aspx) in [TechNet](http://technet.microsoft.com/en-US/).
    
  
2. Fügen Sie eine neue Dokumentbibliothek namens QueryPropertiesTemplate zur Veröffentlichungswebsite hinzu.
    
  
3. Erstellen Sie eine XML-Datei namens queryparametertemplate.xml, und kopieren Sie die folgende XML in die Datei.
    
```XML
  
<QueryPropertiesTemplate xmlns="http://www.microsoft.com/sharepoint/search/KnownTypes/2008/08" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <QueryProperties i:type="KeywordQueryProperties">
        <EnableStemming>true</EnableStemming>
        <FarmId>FarmID</FarmId>
        <IgnoreAllNoiseQuery>true</IgnoreAllNoiseQuery>
        <KeywordInclusion>AllKeywords</KeywordInclusion>
        <SiteId>SiteID</SiteId>
        <SummaryLength>180</SummaryLength>
        <TrimDuplicates>true</TrimDuplicates>
        <WcfTimeout>120000</WcfTimeout>
        <WebId>WebID</WebId>
        <Properties xmlns:a="http://schemas.microsoft.com/2003/10/Serialization/Arrays">
            <a:KeyValueOfstringanyType>
                <a:Key>_IsEntSearchLicensed</a:Key>
                <a:Value i:type="b:boolean" xmlns:b="http://www.w3.org/2001/XMLSchema">true</a:Value>
            </a:KeyValueOfstringanyType>
            <a:KeyValueOfstringanyType>
                <a:Key>EnableSorting</a:Key>
                <a:Value i:type="b:boolean" xmlns:b="http://www.w3.org/2001/XMLSchema">true</a:Value>
            </a:KeyValueOfstringanyType>
            <a:KeyValueOfstringanyType>
                <a:Key>MaxKeywordQueryTextLength</a:Key>
                <a:Value i:type="b:int" xmlns:b="http://www.w3.org/2001/XMLSchema">4096</a:Value>
            </a:KeyValueOfstringanyType>
            <a:KeyValueOfstringanyType>
                <a:Key>TryCache</a:Key>
                <a:Value i:type="b:boolean" xmlns:b="http://www.w3.org/2001/XMLSchema">true</a:Value>
            </a:KeyValueOfstringanyType>
        </Properties>
        <PropertiesContractVersion>15.0.0.0</PropertiesContractVersion>
        <EnableFQL>false</EnableFQL>
        <EnableSpellcheck>Suggest</EnableSpellcheck>
        <EnableUrlSmashing>true</EnableUrlSmashing>
        <IsCachable>false</IsCachable>
        <MaxShallowRefinementHits>100</MaxShallowRefinementHits>
        <MaxSummaryLength>185</MaxSummaryLength>
        <MaxUrlLength>2048</MaxUrlLength>
        <SimilarType>None</SimilarType>
        <SortSimilar>true</SortSimilar>
        <TrimDuplicatesIncludeId>0</TrimDuplicatesIncludeId>
        <TrimDuplicatesKeepCount>1</TrimDuplicatesKeepCount>
    </QueryProperties>
    <WhiteList xmlns:a="http://schemas.microsoft.com/2003/10/Serialization/Arrays">
        <a:string>RowLimit</a:string>
        <a:string>SortList</a:string>
        <a:string>StartRow</a:string>
        <a:string>RefinementFilters</a:string>
        <a:string>Culture</a:string>
        <a:string>RankingModelId</a:string>
        <a:string>TrimDuplicatesIncludeId</a:string>
        <a:string>ReorderingRules</a:string>
        <a:string>EnableQueryRules</a:string>
        <a:string>HiddenConstraints</a:string>
        <a:string>QueryText</a:string>
        <a:string>QueryTemplate</a:string>
    </WhiteList>
</QueryPropertiesTemplate>
```

4. Aktualisieren Sie die Elemente  _SiteId_,  _FarmId_ und _WebId_ mit den Werten für Ihre Farm-, Website- und Veröffentlichungswebsitesammlung.
    
  
5. Speichern Sie die queryparametertemplate.xml in der QueryPropertiesTemplate-Dokumentbibliothek.
    
  
6. Fügen Sie den  _QueryTemplatePropertiesUrl_-Parameter zu Ihrem Search-REST-Aufruf hinzu, und geben Sie spfile://webroot/queryparametertemplate.xml als Wert an.
    
  

### <a name="queryparametertemplatexml-file"></a>Datei "queryparametertemplate.xml"

Die wichtigsten Elemente in der Datei "queryparametertemplate.xml" sind:
  
    
    

- Element **QueryProperties**
  
    
    
Enthält ein serialisiertes  [QueryProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.QueryProperties.aspx) -Objekt.
    
  
- Element **WhiteList**
  
    
    
Enthält die Liste der Abfrageeigenschaften, die der anonyme Benutzer festlegen darf.
    
  
Wenn eine anonyme Search-REST-Abfrage gesendet wird, wird das Abfrageobjekt mit den Informationen im **QueryProperties**-Element erstellt. Dann werden alle Eigenschaften in der Positivliste aus der eingehenden Abfrage in das neu erstellte Abfrageobjekt kopiert.
  
    
    

## <a name="in-this-section"></a>Inhalt dieses Abschnitts
<a name="bk_AnonymousREST"> </a>

-  [Abrufen von Abfragevorschläge mithilfe des Suche REST-Diensts](retrieving-query-suggestions-using-the-search-rest-service.md)
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Suche in SharePoint](search-in-sharepoint.md)
    
  
-  [SharePoint: Verwenden des Search-REST-Diensts über eine App für SharePoint](http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d)
    
  
-  [What's new in SharePoint-Suche für Entwickler](what-s-new-in-sharepoint-search-for-developers.md)
    
  
-  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  

  
    
    

