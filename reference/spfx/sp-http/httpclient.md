# <a name="httpclient-class"></a>HttpClient-Klasse







HttpClient implementiert einen grundlegenden Satz von Funktionen für REST-Vorgänge. Die Unterklasse SPHttpClient erweitert diese grundlegenden Funktionen mit SharePoint-spezifischen Verbesserungen.


## <a name="constructor"></a>Konstruktor


**Signature** _constructor(serviceScope: [ServiceScope](../sp-core-library/servicescope.md));_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine


## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`serviceKey`     | `public` | [`ServiceKey`](../sp-core-library/servicekey.md)<[`HttpClient`](../sp-http/httpclient.md)> | Der Diensschlüssel für HttpClient. Hinweis: Dies steht im **Betamodus** zur Verfügung. Für die Verwendung in der Produktion ist dies nicht empfohlen. |
|`serviceScope`     | `public` | [`ServiceScope`](../sp-core-library/servicescope.md) | _Schreibgeschützt._ Der an den Konstruktor übergebene ServiceScope. |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`fetch(url,configuration,options)`](fetch-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | Führt einen REST-Dienstaufruf aus. Obwohl die SPHttpClient-Unterklasse Verbesserungen hinzufügt, sind die Parameter und die Semantik für HttpClient.fetch() im Wesentlichen identisch mit dem WHATWG-API-Standard, der hier dokumentiert wird: https://fetch.spec.whatwg.org/ |
|[`fetchCore()`](fetchcore-httpclient.md)     | `protected` | `Promise<Response>` | Mit dieser Methode, die das zugrunde liegende IFetchProvider.fetch() aufruft, werden alle Netzwerkanfragen weitergeleitet. |
|[`get(url,configuration,options)`](get-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | Ruft fetch() auf, legt die Methode aber auf 'GET' fest. |
|[`post(url,configuration,options)`](post-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | Ruft fetch() auf, legt die Methode aber auf 'POST' fest. |





