# <a name="fetchurlconfigurationoptions"></a>fetch(url,configuration,options)


 Hinweis: Dies steht im **Betamodus** zur Verfügung. Für die Verwendung in der Produktion ist dies nicht empfohlen.

Führt einen REST-Dienstanruf aus. Obwohl die SPHttpClient-Unterklasse Verbesserungen hinzufügt, sind die Parameter und die Semantik für HttpClient.fetch() im Wesentlichen identisch mit dem WHATWG-API-Standard, der hier dokumentiert wird: https://fetch.spec.whatwg.org/

**Signatur:** _@virtual public fetch(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), Optionen: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_

**Gibt Folgendes zurück**: `Promise<HttpClientResponse>`



Eine Zusage, die das Ergebnis zurückgibt.

#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `url`    | `string` | Die abzurufende URL |
| `configuration`    | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | Bestimmt das Standardverhalten von HttpClient; dies sollte normalerweise die neueste Versionsnummer von HttpClientConfigurations sein. |
| `options`    | [`IHttpClientOptions`](../sp-http/ihttpclientoptions.md) | Zusätzliche Optionen, die Auswirkungen auf die Anforderung haben. |


