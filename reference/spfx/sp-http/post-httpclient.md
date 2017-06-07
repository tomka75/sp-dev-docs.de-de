# <a name="posturlconfigurationoptions"></a>post(url,configuration,options)




Ruft fetch() auf, legt die Methode aber auf ‚POST‘ fest.

**Signatur:** _@virtual public post(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), Optionen: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_

**Gibt Folgendes zurück**: `Promise<HttpClientResponse>`



Eine Zusage, die das Ergebnis zurückgibt.

#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `url`    | `string` | Die abzurufende URL |
| `configuration`    | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | Bestimmt das Standardverhalten von HttpClient; dies sollte normalerweise die neueste Versionsnummer von HttpClientConfigurations sein. |
| `options`    | [`IHttpClientOptions`](../sp-http/ihttpclientoptions.md) | Zusätzliche Optionen, die Auswirkungen auf die Anforderung haben. |


