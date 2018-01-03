---
title: "Abrufen von Abfragevorschläge mithilfe des Such-REST-Diensts"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a64c5bec-64a8-4752-9c72-433d1c864aed
ms.openlocfilehash: 64f07696df6df14756303a53dd75f41de9ccbdbf
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="retrieving-query-suggestions-using-the-search-rest-service"></a>Abrufen von Abfragevorschläge mithilfe des Search-REST-Diensts
Erfahren Sie, wie Sie den Search-REST-Dienst aus Ihren Client- und mobilen Anwendungen verwenden können, um Abfragevorschläge aus der Suche in SharePoint abzurufen.
Abfragevorschläge, auch Suchvorschläge genannt, sind Ausdrücke, nach denen Benutzer bereits gesucht haben und die beim Eingeben einer Abfrage angezeigt oder "vorgeschlagen" werden. Über die Suche in SharePoint können Sie die Vorschläge nach und vor der Abfrage aktivieren. Die Vorschläge werden in einer Liste unter dem Suchfeld angezeigt, während der Benutzer eine Abfrage eingibt. Weitere Informationen zu Abfragevorschlägen und deren Aktivierung finden Sie unter [Verwalten von Abfragevorschlägen in SharePoint]((http://technet.microsoft.com/de-DE/library/jj721441.aspx)).
  
    
    


## <a name="suggest-endpoint-in-the-search-rest-service"></a>Vorschlagen eines Endpunkts im Search-REST-Dienst
<a name="bk_SuggestEndpoint"> </a>

Der Search-REST-Dienst enthält einen **Suggest** -Endpunkt, den Sie verwenden können, in jeder Technologie, die unterstützt der REST-Webanfragen Abfragevorschläge abgerufen, die das Suchsystem für eine Abfrage von Client oder mobilen Anwendungen generiert.
  
    
    
Der URI für **GET** Anforderungen an die Search-REST-Dienst **Suggest** Endpunkt ist:
  
    
    
 `/_api/search/suggest`
  
    
    
Die Parameter für die Abfragevorschläge werden in der URL angegeben. Sie können die Anforderungs-URL auf zwei Arten erstellen:
  
    
    


  
    
    
>  `http://server/_api/search/suggest?parameter=value&amp;parameter=value`
    
  

  
    
    
>  `http://server/_api/search/suggest(parameter=value&amp;parameter=value)`
    
  
> [!NOTE]
> Der Search-REST-Dienst unterstützt keine anonyme Anfragen an den Endpunkt **Suggest**.
  
    
    


## <a name="query-suggestion-parameters"></a>Parameter für die Abfragevorschläge
<a name="bk_SuggestParameters"> </a>

Den folgenden Abschnitten werden die Parameter, die Sie für den Endpunkt **Suggest** verwenden können.
  
    
    

### <a name="querytext"></a>Abfragetext

Eine Zeichenfolge, die den Text für die Suchabfrage enthält
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint"
  
    
    

### <a name="inumberofquerysuggestions"></a>iNumberOfQuerySuggestions

Die Anzahl der Abfragevorschläge abgerufen. Muss größer als 0 (null) sein. Der Standardwert ist 5.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Inumberofquerysuggestions = 3
  
    
    

### <a name="inumberofresultsuggestions"></a>iNumberOfResultSuggestions

Die Anzahl der persönlichen Ergebnisse abgerufen. Muss größer als 0 (null) sein. Der Standardwert ist 5.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Inumberofresultsuggestions = 4
  
    
    

### <a name="fprequerysuggestions"></a>fPreQuerySuggestions

Ein boolescher Wert, der angibt, ob Vorschläge vor der Abfrage oder nach der Abfrage abgerufen. **true** Vorschläge vor der Abfrage zurückzugebenden; andernfalls **false**. Der Standardwert ist **false**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Fprequerysuggestions = True
  
    
    

### <a name="fhithighlighting"></a>fHitHighlighting

Ein boolescher Wert, der angibt, ob Treffer hervorheben oder Abfragevorschläge fett formatiert. **true** fett formatiert die Ausdrücke in den zurückgegebenen Abfragevorschläge, die Ausdrücke in der angegebenen Abfrage übereinstimmen; andernfalls **false**. Der Standardwert ist **true**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Fhithighlighting = False
  
    
    

### <a name="fcapitalizefirstletters"></a>fCapitalizeFirstLetters

Ein boolescher Wert, der angibt, ob für die Großschreibung des ersten Buchstabens in jeden Ausdruck in der zurückgegebenen Abfragevorschläge. **true** für die Großschreibung des ersten Buchstabens in jeden Ausdruck; andernfalls **false**. Der Standardwert ist **false**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Fcapitalizefirstletters = False
  
    
    

### <a name="culture"></a>Culture

Gebietsschema-ID (LCID) für die Abfrage (siehe  [Von Microsoft zugewiesene Gebietsschema-IDs]((http://msdn.microsoft.com/de-DE/goglobal/bb964664.aspx))).
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Culture = 1044
  
    
    

### <a name="enablestemming"></a>EnableStemming

Ein boolescher Wert, der angibt, ob die wortstammerkennung aktiviert ist. **true** zum Aktivieren der wortstammerkennung; andernfalls **false**. Der Standardwert ist **true**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Enablestemming = False
  
    
    

### <a name="showpeoplenamesuggestions"></a>ShowPeopleNameSuggestions

Ein boolescher Wert, der angibt, ob in der zurückgegebenen Abfragevorschläge Personennamen eingeschlossen. **true** Personennamen in der zurückgegebenen Abfragevorschläge enthalten; andernfalls **false**. Der Standardwert ist **true**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Showpeoplenamesuggestions = False
  
    
    

### <a name="enablequeryrules"></a>EnableQueryRules

Ein boolescher Wert, der angibt, ob Abfrageregeln für diese Abfrage zu aktivieren. **true** um Abfrageregeln zu aktivieren; andernfalls **false**. Der Standardwert ist **true**.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Enablequeryrules = False
  
    
    

### <a name="fprefixmatchallterms"></a>fPrefixMatchAllTerms

Ein boolescher Wert, der angibt, ob Abfragevorschläge zurückgegeben für Präfix übereinstimmt. **true** zurückzugebenden Abfragevorschläge basierend auf Präfix entspricht, andernfalls **false** beim Abfragevorschläge das vollständige Abfragewort übereinstimmen soll.
  
    
    
 **Beispiel für GET-Anforderung**
  
    
    
http:// _server_/_api/search/suggest?querytext = "Sharepoint" &amp; Fprefixmatchallterms = False
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Übersicht über die REST-API der SharePoint-Suche](sharepoint-search-rest-api-overview.md)
    
  
-  [Suche in SharePoint](search-in-sharepoint.md)
    
  
-  [SharePoint: Verwenden des Search-REST-Diensts über eine App für SharePoint]((http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d))
    
  
-  [What's new in SharePoint-Suche für Entwickler](what-s-new-in-sharepoint-search-for-developers.md)
    
  
-  [Programmieren mit dem SharePoint REST-Dienst]((http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx))
    
  

  
    
    

