# <a name="geturlconfigurationoptions"></a>get(url,configuration,options)




Ruft fetch() auf, legt die Methode aber auf 'GET' fest.

**Signatur:** _@override public get(url: string, configuration: [SPHttpClientConfiguration](../sp-http/sphttpclientconfiguration.md), options?: [ISPHttpClientOptions](../sp-http/isphttpclientoptions.md)): Promise<[SPHttpClientResponse](../sp-http/sphttpclientresponse.md)>;_

**Gibt Folgendes zurück**: `Promise<SPHttpClientResponse>`



Eine Zusage, die das Ergebnis zurückgibt.

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `url`    | `string` | Die abzurufende URL |
| `configuration`    | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | Bestimmt das Standardverhalten von SPHttpClient; dies sollte normalerweise die neueste Versionsnummer von SPHttpClientConfigurations sein. |
| `options`    | [`ISPHttpClientOptions`](../sp-http/isphttpclientoptions.md) | __Optional.__ Zusätzliche Optionen, die Auswirkungen auf die Anforderung haben. |


