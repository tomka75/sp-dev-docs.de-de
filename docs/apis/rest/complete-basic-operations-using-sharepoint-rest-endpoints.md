# <a name="complete-basic-operations-using-sharepoint-rest-endpoints"></a>Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten
In diesem Artikel erfahren Sie, wie Sie grundlegende Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen, auch als CRUD-Operationen (Create, Read, Update, Delete) bezeichnet, mit der SharePoint-REST-Schnittstelle durchführen.

## <a name="developing-with-the-sharepoint-client-apis-and-rest"></a>Entwickeln mit SharePoint-Client-APIs und REST
<a name="ClientAPIs"> </a> Sie können grundlegende CRUD-Vorgänge (Erstellen, Lesen, Aktualisieren und Löschen) mithilfe der Representational State Transfer (REST)-Schnittstelle ausführen, die von SharePoint bereitgestellt wird. Die REST-Schnittstelle macht alle SharePoint-Entitäten und -Vorgänge verfügbar, die in den anderen SharePoint-Client APIs zur Verfügung stehen. Ein Vorteil der Verwendung von REST besteht darin, dass Sie keine Verweise auf SharePoint-Bibliotheken oder Clientassemblys hinzufügen müssen. Stattdessen sorgen Sie dafür, dass HTTP-Anforderungen an die entsprechenden Endpunkte SharePoint-Entitäten abrufen oder aktualisieren, z. B. Webs, Listen und Listenelemente. Unter [Einführung in den SharePoint-REST-Dienst](get-to-know-the-sharepoint-rest-service.md)  erhalten Sie eine umfassende Einführung in die SharePoint-REST-Schnittstelle und ihre Architektur.
 
Unter [Arbeiten mit Listen und Listenelementen unter Verwendung von REST](working-with-lists-and-list-items-with-rest.md) und [Arbeiten mit Ordnern und Dateien unter Verwendung von REST](working-with-folders-and-files-with-rest.md) wird ausführlich erläutert, wie mit den wichtigsten SharePoint-Entitäten gearbeitet wird. Unter [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations) finden Sie ein Beispiel, in dem gezeigt wird, wie viele dieser Vorgänge im Kontext einer in C# geschriebenen ASP.NET-Webanwendung ausgeführt werden.
 
Weitere Informationen zu den Gruppen von APIs, die auf der SharePoint-Plattform verfügbar sind, finden Sie unter [Auswählen des richtigen API-Satzes in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx). Informationen dazu, wie Sie andere Client-APIs verwenden, finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](https://msdn.microsoft.com/en-us/library/office/jj163201.aspx), [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint 2013-Clientbibliothekscode](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx) und [Erstellen von Windows Phone-Apps, die auf SharePoint 2013 zugreifen](https://msdn.microsoft.com/en-us/library/office/jj163228.aspx).
 

## <a name="http-operations-in-sharepoint-rest-services"></a>HTTP-Operationen in SharePoint-REST-Diensten
<a name="HTTPOps"> </a> Die Endpunkte im SharePoint-REST-Dienst entsprechen den Typen und Mitgliedern in den SharePoint-Clientobjektmodellen. Mithilfe von HTTP-Anfragen, können Sie diese REST-Endpunkte verwenden, um typische CRUD-Vorgänge (**Create**, **Read**, **Update** und **Delete**, Erstellen, Lesen, Aktualisieren und Löschen) in SharePoint-Entitäten, z. B. Listen und Websites auszuführen. 
 
In der Regel entsprechen Endpunkte, die **Read**-Operationen darstellen, HTTP-**GET**-Befehlen.  Endpunkte, die Aktualisierungsoperationen darstellen, entsprechen HTTP-**POST**-Befehlen, und Endpunkte, die Aktualisierungs- oder Einfügeoperationen darstellen, entsprechen HTTP-**PUT**-Befehlen.
 
Verwenden Sie in SharePoint **POST**, um Entitäten wie Listen und Websites zu erstellen. Der SharePoint-REST-Dienst unterstützt das Senden von **POST**-Befehlen, die Objektdefinitionen enthalten, an Endpunkte, die Sammlungen darstellen. Sie könnten z. B. einen **POST**-Befehl, der eine neue Listenobjektdefinition in ATOM enthält, an die folgende URL senden, um eine SharePoint-Liste zu erstellen.
 
 ```
 http://<site url>/_api/web/lists
 ```

Bei **POST**-Vorgängen werden alle Eigenschaften, die nicht erforderlich sind, auf ihre Standardwerte festgelegt. Wenn Sie versuchen, eine schreibgeschützte Eigenschaft als Teil des **POST**-Vorgangs festzulegen, gibt der Dienst eine Ausnahme zurück.
  
Verwenden Sie **PUT**- und **MERGE**-Vorgänge, um vorhandene SharePoint-Objekte zu aktualisieren. Jeder Dienstendpunkt, der einen **SET**-Vorgang einer Objekteigenschaft dargestellt, unterstützt sowohl **PUT**- als auch **MERGE**-Anforderungen. Bei **MERGE**-Vorgängen ist das Festlegen von Eigenschaften optional; Eigenschaften, die Sie nicht explizit festlegen, behalten ihre aktuelle Eigenschaft. Bei **PUT**-Befehlen werden jedoch alle nicht explizit festgelegten Eigenschaften auf ihre Standardeigenschaften festgelegt. Wenn Sie darüber hinaus bei Verwendung von HTTP-**PUT**-Befehlen nicht alle erforderlichen Eigenschaften in Objektaktualisierungen angeben, gibt der REST-Dienst eine Ausnahme zurück.
  
Verwenden Sie den HTTP-**DELETE**-Befehl für die spezifische Endpunk-URL, um das von diesem Endpunkt dargestellte SharePoint-Objekt zu löschen. Bei wiederverwendbaren Objekten, z. B. Listen, Dateien und Listenelementen, führt dies zu einer **Recycle**-Operation.
 
## <a name="reading-data-with-the-sharepoint-rest-interface"></a>Lesen von Daten mit der SharePoint-REST-Schnittstelle
<a name="ReadingData"> </a>  Um die in SharePoint integrierten REST-Funktionen zu verwenden, erstellen Sie mithilfe des OData-Standards eine RESTful-HTTP-Anforderung, die der Clientobjektmodell-API entspricht, die Sie verwenden möchten.  Jede SharePoint-Entität wird an einem Endpunkt auf der SharePoint-Website verfügbar gemacht, auf die Sie abzielen, und ihre Metadaten werden entweder im XML- oder im JSON-Format dargestellt. Sie können die HTTP-Anforderung in einer beliebigen Sprache erstellen, einschließlich, aber nicht beschränkt auf JavaScript und C#.
 
Um Informationen von einem REST-Endpunkt zu lesen, müssen Sie sowohl die URL des Endpunkts als auch die OData-Darstellung der SharePoint-Entität kennen, die an diesem Endpunkt verfügbar gemacht wird. Um beispielsweise alle Listen in einer bestimmten SharePoint-Website abzurufen, würen Sie eine **GET**-Anforderung an `http://<site url>/_api/web/lists` erstellen. Sie können in Ihrem Browser zu dieser URL navigieren und sich den XML-Code ansehen, der zurückgegeben wird. Wenn Sie die Anforderung in Code erstellen, können Sie angeben, ob die OData-Darstellung der Listen in XML oder JSON abgerufen werden soll.
 
Der folgende C#-Code zeigt, wie diese **GET**-Anforderung erstellt wird, die eine JSON-Darstellung aller Listen einer Website mithilfe von JQuery zurückgibt. Außerdem wird angenommen, dass Sie über gültiges OAuth-Zugriffstoken verfügen, das in der **AccessToken**-Variablen gespeichert ist. Sie benötigen das Zugriffstoken nicht, wenn Sie diesen Aufruf von innerhalb eines Add-In-Webs vornehmen, wie dies beispielsweise in einem in SharePoint gehosteten Add-In der Fall ist. Beachten Sie, dass Sie ein Zugriffstoken nicht aus Code abrufen können, der in einem Browserclient ausgeführt wird. Sie müssen das Zugriffstoken aus Code abrufen, der auf einem Server ausgeführt wird. Unter [OAuth-Ablauf mit Kontexttoken für Add-Ins in SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) und [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx) wird erläutert, wie Sie ein Zugriffstoken abrufen können.

```
HttpWebRequest endpointRequest =
  (HttpWebRequest)HttpWebRequest.Create(
  "http://<site url>/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", 
  "Bearer " + accessToken);
HttpWebResponse endpointResponse =
  (HttpWebResponse)endpointRequest.GetResponse();

```

Diese Anforderung würde ein wenig anders aussehen, wenn Sie das Add-In in JavaScript schreiben, aber die domänenübergreifende SharePoint-Bibliothek verwenden. In diesem Fall müssen Sie kein Zugriffstoken bereitstellen. Im folgenden Code wird veranschaulicht, wie diese Anforderung aussähe, wenn Sie die domänenübergreifende Bibliothek verwenden und die OData-Darstellung der Listen als XML und nicht als JSON abrufen möchten. (Da Atom das Standardformat für die Antwort ist, müssen Sie keinen **Accept**-Header einschließen.) Weitere Informationen zur Verwendung der domänenübergreifenden Bibliothek finden Sie unter [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx).
 
```javascript
var executor = new SP.RequestExecutor(appweburl);
executor.executeAsync(
    {
        url:
            appweburl +
            "/_api/SP.AppContextSite(@target)/web/lists?@target='" +
            hostweburl + "'",
        method: "GET",
        success: successHandler,
        error: errorHandler
    }
);
```

Der Code im folgenden Beispiel gezeigt, wie eine JSON-Darstellung aller Listen in einer Website mithilfe von C# angefordert wird. Es wird davon ausgegangen, dass Sie über ein OAuth-Zugriffstoken verfügen, das Sie in der `accessToken`-Variable speichern.

```
HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + "/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse endpointResponse = (HttpWebResponse)endpointRequest.GetResponse();

```

### <a name="getting-properties-that-arent-returned-with-the-resource"></a>Abrufen von Eigenschaften, die nicht mit der Ressource zurückgegeben werden
<a name="NavigationProperties"> </a>Viele Eigenschaftswerte werden zurückgegeben, wenn Sie eine Ressource abrufen. Bei einigen Eigenschaften müssen Sie allerdings eine **GET**-Anforderung direkt an den Eigenschaftsendpunkt senden. Dies gilt i. d. R. für Eigenschaften, die SharePoint-Entitäten darstellen.
 
Das folgende Beispiel zeigt, wie Sie eine Eigenschaft abrufen, indem Sie den Namen der Eigenschaft an den Ressourcenendpunkt anhängen. Im Beispiel wird der Wert der **Author**-Eigenschaft von einer **File**-Ressource abgerufen.
 
 ```
 http:// _<site url>_/_api/web/getfilebyserverrelativeurl('/ _<folder name>_/ _<file name>_')/author
 ```

Um die Ergebnisse im JSON-Format zu erhalten, fügen Sie einen **Accept**-Header zu `"application/json;odata=verbose"` hinzu.

## <a name="writing-data-by-using-the-rest-interface"></a>Schreiben von Daten unter Verwendung der REST-Schnittstelle
<a name="WritingData"> </a>

Sie können SharePoint-Entitäten erstellen und aktualisieren, indem Sie RESTful HTTP-Anforderungen für die entsprechenden Endpunkte, so wie Sie es beim Lesen von Daten tun. Ein wichtiger Unterschied besteht jedoch darin, dass Sie eine **POST**-Anforderung verwenden. Wenn Sie Entitäten aktualisieren, übergeben Sie auch eine **PUT**- oder **MERGE**-HTTP-Anforderungsmethode, indem Sie einen der diese Ausdrücke als Wert des der **X-HTTP-Method**-Schlüssels zu den Headern Ihrer Anforderung hinzufügen. Die **MERGE**-Methode aktualisiert nur die Eigenschaften der Entität, die Sie angeben, während die **PUT**-Methode die vorhandene Entität durch eine neue ersetzt, die Sie im Textkörper von **POST** angeben. Verwenden sie die **DELETE**-Methode, um die Entität zu löschen. Beim Erstellen oder Aktualisieren einer Entität aktualisieren, müssen Sie eine OData-Darstellung der Entität angeben, die Sie im Textkörper der HTTP-Anforderung erstellen oder ändern möchten.
 
Ein weiterer wichtiger Aspekt beim Erstellen, Aktualisieren und Löschen von SharePoint-Entitäten ist, dass diese Operationen den Formulardigestwert der Serveranforderung als Wert des **X-RequestDigest**-Headers benötigen, wenn Sie OAuth nicht zum Autorisieren Ihrer Anforderungen verwenden. Sie können diesen Wert abrufen, indem Sie eine **POST**-Anforderung mit einem leeren Textkörper erstellen und den Wert des `http://<site url>/_api/contextinfo`-Knotens im XML-Code extrahieren, den der `d:FormDigestValue`**contextInfo**-Endpunkt zurückgibt. Das folgende Beispiel zeigt eine HTTP-Anforderung für den **contextInfo**-Endpunkt in C#.
 
```
HttpWebRequest endpointRequest =
  (HttpWebRequest)HttpWebRequest.Create(
  "http://<site url>/_api/contextinfo");
endpointRequest.Method = "POST";
endpointRequest.Accept = "application/json;odata=verbose";
HttpWebResponse endpointResponse =
  (HttpWebResponse)endpointRequest.GetResponse();
  
```

Wenn Sie den unter [Autorisierung und Authentifizierung für Add-Ins in SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142384.aspx) beschriebenen Authentifizierungs- und Autorisierungsablauf verwenden, müssen Sie den Anforderungsdigest nicht in Ihre Anforderungen einschließen.
 
Wenn Sie die domänenübergreifende JavaScript-Bibliothek verwenden, übernimmt SP.RequestExecutor das Abrufen und Senden des Formulardigestwerts für Sie.
 
Wenn Sie ein in SharePoint gehostetes Add-In erstellen, müssen Sie keine separate HTTP-Anforderung zum Abrufen des Formulardigestwerts erstellen. Sie können stattdessen den Wert im JavaScript-Code von der SharePoint-Seite abrufen (wenn die Seite die Standardmasterseite verwendet), wie im folgenden Beispiel dargestellt, in dem JQuery verwendet und eine Liste erstellt wird.
 
```javascript
jQuery.ajax({
        url: "http://<site url>/_api/web/lists",
        type: "POST",
        data:  JSON.stringify({ '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true,
 'BaseTemplate': 100, 'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test' }
),
        headers: { 
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "content-length": <length of post body>,
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: doSuccess,
        error: doError
});
```

Im folgenden Beispiel wird gezeigt, wie Sie die Liste aktualisieren, die im vorherigen Beispiel erstellt wird. In dem Beispiel wird der Titel der Liste geändert, JQuery verwendet und angenommen, dass Sie diesen Vorgang in einem in SharePoint gehosteten Add-In ausführen.

```javascript
jQuery.ajax({
        url: "http://<site url>/_api/web/lists/GetByTitle('Test')",
        type: "POST",
        data: JSON.stringify({ '__metadata': { 'type': 'SP.List' }, 'Title': 'New title' }),
        headers: { 
            "X-HTTP-Method":"MERGE",
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "content-length": <length of post body>,
            "X-RequestDigest": $("#__REQUESTDIGEST").val(),
            "IF-MATCH": "*"
        },
        success: doSuccess,
        error: doError
});

```

Für den Wert des **IF-MATCH**-Schlüssels in den Anforderungsheadern geben Sie den **etag**-Wert einer Liste oder eines Listenelements an. Dieser bestimmte Wert gilt nur für Listen und Listenelemente und soll Ihnen helfen, Konkurrenzprobleme beim Aktualisieren dieser Entitäten zu vermeiden. Im vorherigen Beispiel wird ein Sternchen (*) für diesen Wert verwendet, und Sie können diesen Wert immer dann verwenden, wenn keine Konkurrenzprobleme auftreten können. Andernfalls sollten Sie den * *etag* *-Wert oder eine Liste bzw. ein Listenelement abrufen, indem Sie eine * *GET* *-Anforderung ausführen, die die Entität abruft. Die Antwortheader der resultierenden HTTP-Antwort übergeben das etag als den Wert des **ETag**-Schlüssels. Dieser Wert ist auch in den Entitätsmetadaten enthalten. Das folgende Beispiel zeigt das öffnende `<entry>`-Tag für den XML-Knoten, der die Listeninformationen enthält. Die **m:etag**-Eigenschaft enthält den * *etag**-Wert.

```XML
<entry xml:base="http://site url/_api/" xmlns=http://www.w3.org/2005/Atom 
xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" 
xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"
xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml" m:etag=""1"">
```

## <a name="creating-a-site-with-rest"></a>Erstellen einer Website mit REST
<a name="bk_CreateSite"> </a>

Das folgende Beispiel zeigt, wie Sie eine Website in JavaScript erstellen können.

```javascript
jQuery.ajax({
    url: "http://<site url>/_api/web/webinfos/add",
    type: "POST",
    data: JSON.stringify(
        {'parameters': {
            '__metadata':  {'type': 'SP.WebInfoCreationInformation' },
            'Url': 'RestSubWeb',
            'Title': 'RestSubWeb',
            'Description': 'REST created web',
            'Language':1033,
            'WebTemplate':'sts',
            'UseUniquePermissions':false}
        }
    ),
    headers: { 
        "accept": "application/json; odata=verbose", 
        "content-type":"application/json;odata=verbose",
        "content-length": <length of post body>,
        "X-RequestDigest": $("#__REQUESTDIGEST").val() 
    },
    success: doSuccess,
    error: doError
});
```

## <a name="how-rest-requests-differ-by-environment"></a>So unterscheiden sich REST-Anforderungen je nach Umgebung
<a name="bk_HowRequestsDiffer"> </a>

Das Erstellen und Senden einer HTTP-Anforderung kann je nach Sprache, Bibliothek und Add-In-Typ unterschiedlich, Sie müssen daher häufig eine oder mehrere Anforderungskomponenten ändern, wenn Sie eine Anforderung von einer Umgebung in eine andere übersetzen. AJAX-Anforderungen von JQuery  verwenden z. B. die Parameter **data** und **type**, um den Anforderungstext und -typ anzugeben, daten Anforderungen verwenden jedoch **body**- und **method**- Parameter, um diese Wert anzugeben.
 
In den folgenden Abschnitten werden weitere allgemeine Unterschiede zwischen Umgebungen beschrieben.

### <a name="the-way-you-get-and-send-the-form-digest-value-depends-on-the-add-in"></a>Wie Sie den Formulardigestwert abrufen und senden, hängt von dem Add-In ab
<a name="FormDigest"> </a>

Wenn Sie eine POST-Anforderung senden, muss die Anforderung den Formulardigestwert im **X-RequestDigest**-Header enthalten. Die Art und Weise, wie Sie den Wert abrufen und senden, hängt jedoch vom Add-In ab:
 
- In in SharePoint gehosteten Add-Ins können Sie einfach den folgenden Header übergeben: 
 
 `X-RequestDigest": $("#__REQUESTDIGEST").val()`
    
- Rufen Sie in Cloud-gehosteten Add-Ins, die OAuth verwenden, zuerst den Formulardigestwert ab, indem sie eine Anforderung an den **contextinfo**-Endpunkt senden, und dann der Anforderung den Wert hinzufügen, wie unter [Schreiben von Daten unter Verwendung der REST-Schnittstelle](complete-basic-operations-using-sharepoint-rest-endpoints.md#WritingData) gezeigt.
    
- In in der Cloud gehosteten Add-Ins, die die domänenübergreifende JavaScript-Bibliothek verwenden, müssen Sie den Formulardigestwert nicht angeben. Standardmäßig übernimmt SP. RequestExecutor dies automatisch für Sie. (Der content-length-Wert wird auch behandelt.)

### <a name="add-ins-that-use-oauth-must-pass-access-tokens-in-requests"></a>Add-Ins, die OAuth verwenden, müssen Zugriffstoken in Anforderungen übergeben
<a name="OAuthTokens"> </a>

In der Cloud gehostete Add-Ins verwenden entweder OAuth oder die domänenübergreifende Bibliothek, um Zugriff auf SharePoint-Daten zu autorisieren. Add-In-Komponenten mit Code, der auf einem Remotewebserver ausgeführt wird, muss OAuth zum Autorisieren des Zugriffs auf SharePoint-Daten verwenden. In diesem Fall müssen Sie einen **Authorization**-Header zum Senden des Zugriffstokens einschließen. Unter [Lesen von Daten mit der SharePoint-REST-Schnittstelle](complete-basic-operations-using-sharepoint-rest-endpoints.md#ReadingData) finden Sie ein Beispiel, in dem ein Autorisierungsheader zu einem **HTTPWebRequest**-Objekt hinzugefügt wird.
 
 **Hinweis** In der Cloud gehostete Add-In-Komponenten, die in JavaScript geschrieben werden, müssen das **SP. RequestExecutor**-Objekt domänenübergreifenden Bibliothek verwenden, um auf SharePoint-Daten zuzugreifen. Für Anforderungen der domänenübergreifenden Bibliothek ist kein Zugriffstoken erforderlich.
 
Weitere Informationen zu OAuth-Zugriffstoken und wie diese abgerufen werden, finden Sie unter [OAuth-Ablauf mit Kontexttoken für Add-Ins in SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) und [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx).
 
### <a name="endpoint-uris-in-cross-domain-requests-use-spappcontextsite-to-change-the-context"></a>Endpunkt-URIs in domänenübergreifenden Bibliotheksanforderungen verwenden "SP.AppContextSite", um den Kontext zu ändern
<a name="AppContextSite"> </a>

Die Anforderungen werden an den in der **url**-Eigenschaft der Anforderung angegebenen Ressourcenendpunkt gesendet. Endpunkt-URIs verwenden das folgende Format:
 
 `_<site url>_/_api/ _<context>_/ _<resource>_ (example, https://contoso.com/_api/web/lists)`
 
Anforderungen der domänenübergreifenden Bibliothek verwenden dieses Format, wenn auf Daten im Add-In-Web zugegriffen wird. Dabei handelt es sich um den Standardkontext für Anforderungen von domänenübergreifenden Bibliotheken. Um aber auf Daten im Hostweb oder in einer anderen Websitesammlung zuzugreifen, müssen die Anforderungen das Hostweb oder die andere Websitesammlung als Kontext initialisieren. Zu diesem Zweck verwenden sie den **SP. AppContextSite**-Endpunkt im URI, wie in Tabelle 1 dargestellt. In den Beispiel-URIs in Tabelle 1 wird der **@target**-Alias zum Senden der Ziel-URL in der Abfragezeichenfolge verwendet, da die URL ein Sonderzeichen (‚:‘) enthält.

 **Hinweis** Damit ein in der Cloud gehostetes Add-In beim Verwenden der domänenübergreifenden Bibliothek auf SharePoint-Daten zugreifen kann, ist eine Add-In-Webinstanz erforderlich.

**Tabelle 1. Verwenden des SP.AppContextSite-Endpunkts zum Ändern des Kontexts der Anforderung**


|**Add-In-Typ**|**Szenario für den domänenübergreifenden Datenzugriff**|**Beispiel-Endpunkt-URI**|
|:-----|:-----|:-----|
|In der Cloud gehostet|JavaScript-Add-In-Komponente, die mithilfe der domänenübergreifenden Bibliothek auf Hostwebdaten zugreift| _<app web url>_/_api/SP.AppContextSite(@target)/web/lists?@target=' _<host web url>_'|
|In der Cloud gehostet|JavaScript-Add-In-Komponente, die mithilfe der domänenübergreifenden Bibliothek auf Daten zugreift, die sich in einer anderen Websitesammlung als dem Hostweb befinden (gilt nur für Add-Ins mit Mandantenbereich)| _<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'|
|Auf SharePoint gehostet|Add-In-Webkomponente, die auf Daten einer anderen Websitesammlung zugreift (gilt nur für Add-Ins mit Mandantenbereich)| _<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'|

 
  **Hinweis** Für Szenarien für den domänenübergreifenden Datenzugriff sind auch entsprechende Add-In-Berechtigungen erforderlich. Weitere Informationen finden Sie unter [Zugreifen auf Daten in einem Hostweb](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_Hostweb) und [Zugreifen auf Daten in allen Websitesammlungen](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_TenantScope).

SharePoint-Add-Ins können die Add-In-Web-URL und die Hostweb-URL aus der Abfragezeichenfolge der Add-In-Seite abrufen, wie im folgenden Codebeispiel dargestellt. In dem Beispiel wird auch gezeigt, wie auf die domänenübergreifende Bibliothek verwiesen wird, die in der Datei „SP.RequestExecutor.js“ im Hostweb definiert ist. In dem Beispiel wird davon ausgegangen, dass das Add-In von SharePoint aus wird gestartet. Anweisungen zum korrekten Festlegen des SharePoint-Kontexts, wenn das Add-In nicht aus SharePoint gestartet wird, finden Sie unter [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx).

```javascript
var hostweburl;
var appweburl;

// Get the URLs for the add-in web the host web URL from the query string.
$(document).ready(function () {
  //Get the URI decoded URLs.
  hostweburl = decodeURIComponent(getQueryStringParameter("SPHostUrl"));
  appweburl = decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));

  // Load the SP.RequestExecutor.js file.
  $.getScript(hostweburl + "/_layouts/15/SP.RequestExecutor.js", runCrossDomainRequest);
});

// Build and send the HTTP request.
function runCrossDomainRequest() {
  var executor = new SP.RequestExecutor(appweburl); 
  executor.executeAsync({
      url: appweburl + "/_api/SP.AppContextSite(@target)/web/lists?@target='" + hostweburl + "'",
      method: "GET", 
      headers: { "Accept": "application/json; odata=verbose" }, 
      success: successHandler, 
      error: errorHandler 
  });
}

// Get a query string value.
// For production add-ins, you may want to use a library to handle the query string.
function getQueryStringParameter(paramToRetrieve) {
  var params = document.URL.split("?")[1].split("&amp;");
  var strParams = "";
  for (var i = 0; i < params.length; i = i + 1) {
    var singleParam = params[i].split("=");
    if (singleParam[0] == paramToRetrieve) return singleParam[1];
  }
}
… // success and error callback functions
```

## <a name="properties-used-in-rest-requests"></a>In REST-Anforderungen verwendete Eigenschaften
<a name="bk_requestElements"> </a>

In Tabelle 2 sind häufig in HTTP-Anforderungen für den SharePoint-REST-Dienst verwendete Eigenschaften aufgeführt.
 
**Tabelle 2. Verwendung von REST-Anforderungseigenschaften in HTTP-Anforderungen**

|**Eigenschaften**|**Wann erforderlich**|**Beschreibung**|
|:-----|:-----|:-----|
|**url**|Alle Anforderungen|Die URL eines REST-Ressourcenendpunkts. Beispiel:  `http://<site url>/_api/web/lists`|
|**method** (oder **type**)|Alle Anforderungen|Die HTTP-Anforderungsmethode:  **GET** für Lesevorgänge und **POST** für Schreibvorgänge. **POST**-Anforderungen können Operationen aktualisieren oder löschen, indem ein **DELETE**-, **MERGE**- oder **PUT**-Verb im **X-HTTP-Method**-Header angegeben wird.|
|**body** (oder **data**)|**POST**-Anforderungen, die Daten im Anforderungstextkörper senden|Der Textkörper der POST-Anforderung. Sendet Daten (z. B. komplexe Typen), die nicht im Endpunkt-URI gesendet werden können. Wird zusammen mit dem **content-length**-Header verwendet.|
|**Authentication**-Header|Remote-Add-Ins, die OAuth zum Authentifizieren von Benutzern verwenden. Trifft nicht zu, wenn JavaScript oder die domänenübergreifende Bibliothek verwendet wird.|Sendet das OAuth-Zugriffstoken (das von einem sicheren Microsoft ACS-Tokenserver, Microsoft Access Control Service, abgerufen wird), das zum Authentifizieren des Benutzers für die Anforderung verwendet wird. Beispiel: `"Authorization": "Bearer " + accessToken`, wobei `accessToken` die Variable darstellt, die das Token speichert. Token müssen mit serverseitigem Code abgerufen werden.|
|**X-RequestDigest**-Header|**POST**-Anforderungen (außer SP.RequestExecutor-Anforderungen)|Remote-Add-Ins, die OAuth verwenden, können den Formulardigestwert von dem `http://<site url>/_api/contextinfo`-Endpunkt abrufen. In SharePoint gehostete Add-Ins können rufen Sie den Wert aus dem **#__REQUESTDIGEST**-Seitensteuerelement abrufen, wenn dieses auf der SharePoint-Seite verfügbar ist. Weitere Informationen finden Sie unter [Schreiben von Daten unter Verwendung der REST-Schnittstelle](#WritingData).|
|**accept**-Header|Anforderungen, die SharePoint-Metadaten zurückgeben|Gibt das Format für Antwortdaten vom Server an. Das Standardformat ist `application/atom+xml`. Beispiel:  `"accept":"application/json;odata=verbose"`|
|**content-type**-Header|**POST**-Anforderungen, die Daten im Anforderungstextkörper senden|Gibt das Format der Daten an, die der Client an den Server sendet. Das Standardformat ist `application/atom+xml`. Beispiel:  `"content-type":"application/json;odata=verbose"`|
|**content-length**-Header|**POST**-Anforderungen, die Daten im Anforderungstextkörper senden (außer SP.RequestExecutor-Anforderungen)|Gibt die Länge des Inhalts an. Beispiel:  `"content-length":requestBody.length`|
|**IF-MATCH**-Header|**POST**-Anforderungen für **DELETE**-, **MERGE**- oder **PUT**-Vorgänge, in erster Linie, um Listen und Bibliotheken zu ändern.|Bietet eine Möglichkeit, um sicherzustellen, dass das zu ändernde Objekt nicht geändert wurde, seit es zuletzt abgerufen wurde. Alternativ können Sie angeben, dass Änderungen überschrieben werden sollen, wie im folgenden Beispiel dargestellt: `"IF-MATCH":"*"`|
|**X-HTTP-Method**-Header|**POST**-Anforderungen für **DELETE**-, **MERGE**- oder **PUT**-Vorgänge|Wird verwendet, um festzulegen, dass die Anforderung einen Aktualisierungs- oder Löschvorgang durchführt. Beispiel: `"X-HTTP-Method":"PUT"`|
|**binaryStringRequestBody**|SP.RequestExecutor-**POST**-Anforderungen, die binäre Daten im Anforderungstextkörper senden|Gibt an, ob der Anforderungstextkörper eine binäre Zeichenfolge ist.  **Boolescher Wert**.|
|**binaryStringResponseBody**|SP.RequestExecutor-Anforderungen, die binäre Daten zurückgeben|Gibt an, ob die Antwort eine binäre Zeichenfolge ist.  **Boolescher Wert**.|

## <a name="batch-job-support"></a>Unterstützung für Batchaufträge
<a name="batch"> </a> Der SharePoint Online-REST-Dienst (und der Dienst von SharePoint 2016 (lokal) und höher) unterstützt die Kombination mehrerer Anforderungen in einem einzelnen Dienstaufruf mithilfe der OData-Abfrageoption `$batch`. Einzelheiten und Links zu Codebeispielen finden Sie unter [Erstellen von Batchanforderungen mit den REST-APIs](make-batch-requests-with-the-rest-apis.md).

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Arbeiten mit Listen und Listenelementen unter Verwendung von REST](working-with-lists-and-list-items-with-rest.md)
-  [Arbeiten mit Ordner und Dateien unter Verwendung von REST](working-with-folders-and-files-with-rest.md) 
-  [REST-API-Referenz und Beispiele](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
-  [SharePoint 2013: Ausführen grundlegender Datenzugriffsvorgänge für Dateien und Ordner mithilfe von REST](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint 2013-Clientbibliothekscode](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx)
-  [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/jj163201.aspx)
-  [Entwickeln von SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/jj163794.aspx)
-  [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/fp179897.aspx)
-  [Arbeiten mit externen Daten in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179893.aspx)
-  [OData (Open Data Protocol)](http://www.odata.org/)
-  [OData: JSON (JavaScript Object Notation)-Format](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
-  [Festlegen von benutzerdefinierten Berechtigungen in einer Liste mit der REST-Schnittstelle](set-custom-permissions-on-a-list-by-using-the-rest-interface.md)