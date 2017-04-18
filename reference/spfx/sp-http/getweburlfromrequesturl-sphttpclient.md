# <a name="getweburlfromrequesturlrequesturl"></a>getWebUrlFromRequestUrl(requestUrl)




Dies verwendet eine Heuristik, um die zur bereitgestellten REST-URL gehörende SPWeb-URL zu erraten. Das ist für Vorgänge wie z. B. X-RequestDigest- und ODATA-Batchverarbeitung notwendig, die das Veröffentlichen in einem getrennten REST-Endpunkt erfordern, um eine Anforderung abzuschließen. Wenn zum Beispiel requestUrl "/sites/site/web/_api/service" ist, ist die zurückgegebene URL "/sites/site/web". Wenn requestUrl "http://example.com/_layouts/service" ist, ist die zurückgegebene URL "http://example.com".

**Signatur:** _public static getWebUrlFromRequestUrl(requestUrl: string): string;_

**Gibt Folgendes zurück**: `string`



die abgeleitete SPWeb-URL

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `requestUrl`    | `string` | Die URL für einen SharePoint REST-Dienst |


