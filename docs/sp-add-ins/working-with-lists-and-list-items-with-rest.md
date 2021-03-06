


# <a name="working-with-lists-and-list-items-with-rest"></a>Arbeiten mit Listen und Listenelementen unter Verwendung von REST
In diesem Artikel erfahren Sie, wie Sie grundlegende Erstell-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, für Listen und Listenelemente mit der SharePoint REST-Schnittstelle durchführen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 


 **Tipp**  Der SharePoint Online-REST-Dienst (und der Dienst von SharePoint 2016 (lokal) und höher) unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption `$batch`. Einzelheiten und Links zu Codebeispielen finden Sie unter [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis) (Erstellen von Batchanforderungen mit den REST-APIs).
 


## <a name="prerequisites"></a>Voraussetzungen

In diesem Artikel setzen wir voraus, dass Sie bereits den Artikel zum Thema [Einführung in den SharePoint-REST-Dienst](get-to-know-the-sharepoint-2013-rest-service) sowie den Artikel zum Thema [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](complete-basic-operations-using-sharepoint-2013-rest-endpoints) gelesen haben. Es werden keine Codeausschnitte bereitgestellt.
 

 

## <a name="retrieving-lists-and-list-properties-with-rest"></a>Abrufen von Listen und Listeneigenschaften mit REST
<a name="RetrieveLists"> </a>

Das folgende Beispiel zeigt, wie Sie eine bestimmte Liste **abrufen**, wenn ihre GUID bekannt ist.
 

 

```
url: http://site url/_api/web/lists(guid'list GUID'),
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```


 **Hinweis**  Verwenden Sie  `application/json;odata=verbose` in der Kopfzeile `accept`, wenn Sie die Antwort in JSON wünschen. Verwenden Sie `application/atom+xml` in der Kopfzeile `accept`, wenn Sie die Antwort im Format Atom wünschen.
 

Das folgende Beispiel zeigt, wie Sie eine bestimmte Liste **abrufen**, wenn ihr Titel bekannt ist.
 

 



```
url: http://site url/_api/web/lists/GetByTitle('Test')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Der folgende XML-Code zeigt ein Beispiel für die Listeneigenschaften, die beim Anfordern des XML-Inhaltstyps zurückgegeben werden.
 

 



```XML
  <content type="application/xml">
  <m:properties>
  <d:AllowContentTypes m:type="Edm.Boolean">true</d:AllowContentTypes> 
  <d:BaseTemplate m:type="Edm.Int32">100</d:BaseTemplate> 
  <d:BaseType m:type="Edm.Int32">0</d:BaseType> 
  <d:ContentTypesEnabled m:type="Edm.Boolean">false</d:ContentTypesEnabled> 
  <d:Created m:type="Edm.DateTime">2012-06-26T23:15:58Z</d:Created> 
  <d:DefaultContentApprovalWorkflowId m:type="Edm.Guid">00000000-0000-0000-0000-000000000000</d:DefaultContentApprovalWorkflowId> 
  <d:Description>A list created by Project Based Retention used to store Project Policy Items.</d:Description> 
  <d:Direction>none</d:Direction> 
  <d:DocumentTemplateUrl m:null="true" /> 
  <d:DraftVersionVisibility m:type="Edm.Int32">0</d:DraftVersionVisibility> 
  <d:EnableAttachments m:type="Edm.Boolean">true</d:EnableAttachments> 
  <d:EnableFolderCreation m:type="Edm.Boolean">false</d:EnableFolderCreation> 
  <d:EnableMinorVersions m:type="Edm.Boolean">false</d:EnableMinorVersions> 
  <d:EnableModeration m:type="Edm.Boolean">false</d:EnableModeration> 
  <d:EnableVersioning m:type="Edm.Boolean">false</d:EnableVersioning> 
  <d:EntityTypeName>ProjectPolicyItemList</d:EntityTypeName> 
  <d:ForceCheckout m:type="Edm.Boolean">false</d:ForceCheckout> 
  <d:HasExternalDataSource m:type="Edm.Boolean">false</d:HasExternalDataSource> 
  <d:Hidden m:type="Edm.Boolean">true</d:Hidden> 
  <d:Id m:type="Edm.Guid">74de3ff3-029c-42f9-bd2a-1e9463def69d</d:Id> 
  <d:ImageUrl>/_layouts/15/images/itgen.gif</d:ImageUrl> 
  <d:IrmEnabled m:type="Edm.Boolean">false</d:IrmEnabled> 
  <d:IrmExpire m:type="Edm.Boolean">false</d:IrmExpire> 
  <d:IrmReject m:type="Edm.Boolean">false</d:IrmReject> 
  <d:IsApplicationList m:type="Edm.Boolean">false</d:IsApplicationList> 
  <d:IsCatalog m:type="Edm.Boolean">false</d:IsCatalog> 
  <d:IsPrivate m:type="Edm.Boolean">false</d:IsPrivate> 
  <d:ItemCount m:type="Edm.Int32">0</d:ItemCount> 
  <d:LastItemDeletedDate m:type="Edm.DateTime">2012-06-26T23:15:58Z</d:LastItemDeletedDate> 
  <d:LastItemModifiedDate m:type="Edm.DateTime">2012-06-26T23:15:59Z</d:LastItemModifiedDate> 
  <d:ListItemEntityTypeFullName>SP.Data.ProjectPolicyItemListItem</d:ListItemEntityTypeFullName> 
  <d:MultipleDataList m:type="Edm.Boolean">false</d:MultipleDataList> 
  <d:NoCrawl m:type="Edm.Boolean">true</d:NoCrawl> 
  <d:ParentWebUrl>/</d:ParentWebUrl> 
  <d:ServerTemplateCanCreateFolders m:type="Edm.Boolean">true</d:ServerTemplateCanCreateFolders> 
  <d:TemplateFeatureId m:type="Edm.Guid">00bfea71-de22-43b2-a848-c05709900100</d:TemplateFeatureId> 
  <d:Title>Project Policy Item List</d:Title> 
  </m:properties>
  </content>
```


 **Hinweis**  Die Eigenschaft  **ListItemEntityTypeFullName** ( **SP.Data.ProjectPolicyItemListItem** im vorhergehenden Beispiel) ist wichtig, wenn Sie Listenelemente erstellen und aktualisieren möchten. Dieser Wert muss als **type**-Eigenschaft in den Metadaten übergeben werden, die Sie im Textkörper der HTTP-Anforderung übergeben, wenn Sie Listenelemente erstellen und aktualisieren.
 


## <a name="working-with-lists-by-using-rest"></a>Arbeiten mit Listen unter Verwendung von REST
<a name="WorkLists"> </a>

Das folgende Beispiel zeigt, wie Sie eine Liste **erstellen**.
 

 

```
url: http://site url/_api/web/lists
method: POST
body: { '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true, 'BaseTemplate': 100,
 'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test' }
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

Das folgende Beispiel zeigt, wie Sie eine Liste **aktualisieren** und dazu die **MERGE**-Methode verwenden.
 

 



```
url: http://site url/_api/web/lists(guid'list GUID')
method: POST
body: { '__metadata': { 'type': 'SP.List' }, 'Title': 'New title' }
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    IF-MATCH": etag or "*"
    X-HTTP-Method: MERGE,
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

Das folgende Beispiel zeigt, wie Sie ein **benutzerdefiniertes Feld** für eine Liste **erstellen**.
 

 



```
Url: url: http://site url/_api/web/lists(guid'list GUID')/Fields
Method:POST
Body: { '__metadata': { 'type': 'SP.Field' }, 'Title': 'field title', 'FieldTypeKind': FieldType value,'Required': 'true/false', 'EnforceUniqueValues': 'true/false','StaticName': 'field name'}
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

Das folgende Beispiel zeigt, wie Sie eine Liste **löschen**.
 

 



```
url: http://site url/_api/web/lists(guid'list GUID')
method: POST
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method: DELETE

```


## <a name="working-with-list-items-by-using-rest"></a>Arbeiten mit Listenelementen unter Verwendung von REST
<a name="ListItems"> </a>

Das folgende Beispiel zeigt, wie Sie alle Elemente einer Liste **abrufen**.
 

 

 **Hinweis** Die OData-Abfrageoption „$skip“ funktioniert nicht für das Abfragen von Listenelementen. In vielen Fällen können Sie stattdessen die Option [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx) verwenden.
 


```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Das folgende Beispiel zeigt, wie sie ein bestimmtes Listenelement **abrufen**.
 

 



```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Der folgende XML-Code zeigt ein Beispiel für die Listenelementeigenschaften, die beim Anfordern des XML-Inhaltstyps zurückgegeben werden.
 

 



```XML
<content type="application/xml">
<m:properties> 
<d:FileSystemObjectType m:type="Edm.Int32">0</d:FileSystemObjectType>
<d:Id m:type="Edm.Int32">1</d:Id>
<d:ID m:type="Edm.Int32">1</d:ID>
<d:ContentTypeId>0x010049564F321A0F0543BA8C6303316C8C0F</d:ContentTypeId>
<d:Title>an item</d:Title>
<d:Modified m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Modified>
<d:Created m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Created>
<d:AuthorId m:type="Edm.Int32">11</d:AuthorId>
<d:EditorId m:type="Edm.Int32">11</d:EditorId>
<d:OData__UIVersionString>1.0</d:OData__UIVersionString>
<d:Attachments m:type="Edm.Boolean">false</d:Attachments>
<d:GUID m:type="Edm.Guid">eb6850c5-9a30-4636-b282-234eda8b1057</d:GUID>
</m:properties>
</content>
```

Das folgende Beispiel zeigt, wie Sie ein Listenelement **erstellen**.
 

 

 **Hinweis**  Zum Ausführen dieses Vorgangs müssen Sie die Eigenschaft **ListItemEntityTypeFullName** der Liste kennen und sie als Wert von **type** im HTTP-Anforderungstext weitergeben.
 




```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'Test'}
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

Das folgende Beispiel zeigt, wie Sie ein Listenelement **aktualisieren**.
 

 

 **Hinweis**  Zum Ausführen dieses Vorgangs müssen Sie die Eigenschaft **ListItemEntityTypeFullName** der Liste kennen und sie als Wert von **type** im HTTP-Anforderungstext weitergeben.
 




```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'TestUpdated'}
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"MERGE",
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

Das folgende Beispiel zeigt, wie Sie ein Listenelement **löschen**.
 

 



```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```


## <a name="using-etag-values-to-determine-document-and-list-item-versioning"></a>Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen
<a name="Etag"> </a>

 Der SharePoint REST-Dienst, der sich nach dem  [OData-Standard](http://www.odata.org/developers/protocols/operations) richtet, verwendet  [HTML ETags für die Gleichzeitigkeitssteuerung](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) von SharePoint-Listen und -Listenelementen. Um die Version eines Elements beim Ausführen einer **PUT**-,  **MERGE**- oder  **DELETE**-Anforderung zu prüfen, geben Sie ein **ETag** im HTTP-Anforderungskopf **If-Match** an.
 

 
Wenn das in Ihrer Anforderung angegebene **ETag** nicht mit dem **ETag** des Dokument- oder Listenelements auf dem Server übereinstimmt, gibt der REST-Dienst gemäß der OData-Spezifikation eine 412-Ausnahme zurück.
 

 

- Wenn Sie ein Überschreiben des Elements unabhängig von der Version erzwingen möchten, legen Sie den **ETag**-Wert auf **"*"** fest.
    
 
- Wenn Sie kein **ETag** angeben, überschreibt SharePoint das Element unabhängig von der Version.
    
 
In SharePoint gelten ETags nur für SharePoint-Listen und Listenelemente.
 

 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [Arbeiten mit Ordnern und Dateien unter Verwendung von REST](working-with-folders-and-files-with-rest)
    
 
-  [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
    
 
-  [SharePoint: Ausführen grundlegender Datenzugriffsvorgänge für Dateien und Ordner mithilfe von REST](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
    
 
-  [Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
    
 
-  [Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint - Demo](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
    
 
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](complete-basic-operations-using-sharepoint-2013-client-library-code)
    
 
-  [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013)
    
 
-  [Entwickeln von SharePoint-Add-Ins](develop-sharepoint-add-ins)
    
 
-  [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins)
    
 
-  [Arbeiten mit externen Daten in SharePoint](work-with-external-data-in-sharepoint-2013)
    
 
-  [Open Data Protocol](http://www.odata.org/)
    
 
-  [OData: JSON(JavaScript Object Notation)-Format](http://www.odata.org/documentation/odata-version-2-0/json-format/)
    
 

 

 

