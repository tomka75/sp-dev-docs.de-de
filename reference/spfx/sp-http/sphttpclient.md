# <a name="sphttpclient-class"></a>SPHttpClient-Klasse







SPHttpClient wird zum Durchführen von REST-Aufrufen für SharePoint verwendet. Es fügt Standardkopfzeilen hinzu, verwaltet den für Schreibvorgänge erforderlichen Digest und sammelt Telemetrie, die dem Dienst hilft, die Leistung einer Anwendung zu überwachen. Verwenden Sie für die Kommunikation mit Nicht-SharePoint-Diensten stattdessen die HttpClient-Klasse.


## <a name="constructor"></a>Konstruktor


**Signatur:** _constructor(serviceScope: [ServiceScope](../sp-core-library/servicescope.md));_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine


## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`serviceKey`     | `public` | [`ServiceKey`](../sp-core-library/servicekey.md)<[`SPHttpClient`](../sp-http/sphttpclient.md)> | Der Diensschlüssel für SPHttpClient. |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`beginBatch()`](beginbatch-sphttpclient.md)     | `public` | `SPHttpClientBatch` | Beginnt einen ODATA-Batch, der mehrere REST-Abfragen in einer einzigen Web-Anforderung gebündelt zulässt. |
|[`fetch(url,configuration,options)`](fetch-sphttpclient.md)     | `public` | `Promise<SPHttpClientResponse>` | Im Allgemeinen sind die Parameter und die Semantik für SPHttpClient.fetch() im Wesentlichen identisch mit dem WHATWG-API-Standard, der hier dokumentiert wird: https://fetch.spec.whatwg.org/. Die SPHttpClient-Unterklasse fügt einige zusätzliche Verhaltensweisen hinzu, beim Arbeiten mit SharePoint-OData-APIs nützlich sind (die auch durch Verwenden von HttpClient vermieden werden können): – Standardmäßige "Accept"- und "Content-Type"-Kopfzeilen werden hinzugefügt, sofern kein Wert explizit angegeben wird. – Für Schreibvorgänge wird eine "X-RequestDigest"-Kopfzeile automatisch hinzugefügt. –Das Anforderungs-Digest-Token wird automatisch abgerufen und in einem Cache mit Unterstützung für das Vorabladen gespeichert. Für einen Schreibvorgang, fügt SPHttpClient automatisch die "X-RequestDigest"-hinzu, die möglicherweise durch Ausgabe einer separaten Anforderung wie "https://example.com/sites/sample/_api/contextinfo" abgerufen werden muss. Normalerweise kann die entsprechende SPWeb-URL erraten werden, indem nach einem reservierten URL-Segment gesucht wird, z. B. "_api" in der ursprünglichen URL, die an fetch() übergeben wird. Verwenden Sie andernfalls ISPHttpClientOptions.webUrl, um die URL explizit anzugeben. |
|[`get(url,configuration,options)`](get-sphttpclient.md)     | `public` | `Promise<SPHttpClientResponse>` | Ruft fetch() auf, legt die Methode aber auf 'GET' fest. |
|[`getWebUrlFromRequestUrl(requestUrl)`](getweburlfromrequesturl-sphttpclient.md)     | `public, static` | `string` | Dies verwendet eine Heuristik, um die zur bereitgestellten REST-URL gehörende SPWeb-URL zu erraten. Das ist für Vorgänge wie z. B. X-RequestDigest- und ODATA-Batchverarbeitung notwendig, die das Veröffentlichen in einem getrennten REST-Endpunkt erfordern, um eine Anforderung abzuschließen. Wenn zum Beispiel requestUrl "/sites/site/web/_api/service" ist, ist die zurückgegebene URL "/sites/site/web". Wenn requestUrl "http://example.com/_layouts/service" ist, ist die zurückgegebene URL "http://example.com". |
|[`post(url,configuration,options)`](post-sphttpclient.md)     | `public` | `Promise<SPHttpClientResponse>` | Ruft fetch() auf, legt die Methode aber auf ‚POST‘ fest. |





