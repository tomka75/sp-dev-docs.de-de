
# <a name="synchronize-sharepoint-items-using-the-rest-service"></a>Synchronisieren von SharePoint-Elementen mithilfe des REST-Diensts
Erfahren Sie, wie Sie mit der Ressource **GetListItemChangesSinceToken**, die Teil des SharePoint REST-Diensts ist, Elemente zwischen SharePoint und Ihren Add-Ins oder Diensten synchronisieren.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 


## <a name="synchronizing-sharepoint-items-using-the-getlistitemchangessincetoken-resource"></a>Synchronisieren von SharePoint-Elementen mithilfe der Ressource GetListItemChangesSinceToken

Zum Synchronisieren von Elementen zwischen SharePoint und Ihren Add-ins oder Diensten können Sie die Ressource **GetListItemChangesSinceToken** verwenden. **GetListItemChangesSinceToken** ist Teil des SharePoint REST-Diensts und entspricht dem Webdienstaufruf **Lists.GetListItemChangesSinceToken**.
 

 
Führen Sie eine **POST**-Anforderung aus, die ein Objekt [SP.ChangeLogItemQuery object properties](#bk_props) im Hauptteil enthält.
 

 
Die Anforderung gibt ADO **rowset** XML mit den Zeilen zurück, die alle mit der Abfrage übereinstimmenden Änderungen an Listenelementen enthalten. Weitere Informationen zu diesen Eigenschaften, einschließlich Eigenschaftendatenstrukturen, CAML-Elementbeschreibungen und Rückgabewerten finden Sie unter **Lists.GetListItemChangesSinceToken**.
 

 

||
|:-----|
|**Beispielanforderung**|
| `POST http://server/site/_api/web/Lists/GetByTitle('Announcements')/GetListItemChangesSinceToken`|
|**Beispiel für POST-Text**|
|
```XML
{ 'd' : { 
  'query': { 
    '__metadata': { 'type': 'SP.ChangeLogItemQuery'}, 
    'ViewName': '', 
    'Query': '<Where>
      <Contains>
         <FieldRef Name="Title" />
         <Value Type='Text'>Te</Value>
      </Contains></Where>',
    'QueryOptions': '<QueryOptions>
      <IncludeMandatoryColumns>FALSE</IncludeMandatoryColumns>
      <DateInUtc>False</DateInUtc>
      <IncludePermissions>TRUE</IncludePermissions>
      <IncludeAttachmentUrls>FALSE</IncludeAttachmentUrls>
      <Folder>Shared Documents/Test1</Folder></QueryOptions>', 
    'ChangeToken':'1;3;eee4c6d5-f88a-42c4-8ce1-685122984870;634397182229400000;3710', 
    'Contains':'<Contains>
      <FieldRef Name="Title"/>
      <Value Type="Text">Testing</Value></Contains>' } 
  } 
}

```

|

## <a name="spchangelogitemquery-object-properties"></a>Objekteigenschaften SP.ChangeLogItemQuery
<a name="bk_props"> </a>


****


|**Property**|**Description**|
|:-----|:-----|
|**ListName**|Eine Zeichenfolge, die entweder Titel oder GUID der Liste enthält. Bei Abruf der Tabelle "UserInfo" enthält die Zeichenfolge UserInfo. Die Verwendung der GUID führt zu einer besseren Leistung.|
|**ViewName**|Eine Zeichenfolge mit der GUID für die Ansicht, die für die durch die Parameter _query_,  _viewFields_ und  _rowLimit_ dargestellten Standard-Ansichtattribute zu verwenden ist. Wird dieses Argument nicht angegeben, so wird die Standardansicht verwendet. Wird das Argument angegeben, so setzt der Wert der Parameter _query_,  _viewFields_ oder  _rowLimit_ die entsprechende Einstellung in der Ansicht außer Kraft. Weist z. B. die durch den Parameter _viewFields_ angegebene Ansicht ein Zeilenlimit von 100 auf, während der Parameter _rowLimit_ den Wert 1000 enthält, dann werden in der Antwort 1000 Zeilen zurückgegeben.|
|**Query**|Ein [Query](http://msdn.microsoft.com/en-us/library/ms471093.aspx)-Element mit der Abfrage, die festlegt, welche Datensätze in welcher Reihenfolge zurückgegeben werden.|
|**QueryOptions**|Ein XML-Fragment in der folgenden Form, das separate Knoten für die verschiedenen Eigenschaften des Objekts **SPQuery** enthält.|
|**ChangeToken**|Eine Zeichenfolge, die das Änderungstoken für die Anforderung enthält. Eine Beschreibung des Formats, das in dieser Zeichenfolge verwendet wird, finden Sie unter [Übersicht über das Änderungsprotokoll](http://msdn.microsoft.com/en-us/library/bb417456.aspx). Wenn Null übergeben wird, werden alle Elemente in der Liste zurückgegeben.|
|**Contains**|Ein [Contains](http://msdn.microsoft.com/en-us/library/ms196501.aspx)-Element, das das benutzerdefinierte Filtern für die Abfrage definiert.|

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Grundlegendes zum SharePoint REST-Dienst](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [Arbeiten mit Listen und Listenelementen unter Verwendung von REST](working-with-lists-and-list-items-with-rest)
    
 
-  [Arbeiten mit Ordnern und Dateien unter Verwendung von REST](working-with-folders-and-files-with-rest)
    
 
-  [Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
-  [Ermitteln von URIs von SharePoint REST-Dienstendpunkten](determine-sharepoint-rest-service-endpoint-uris)
    
 
-  [Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen](use-odata-query-operations-in-sharepoint-rest-requests)
    
 
-  [REST-API-Referenz und Beispiele](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)
    
 

 

 

