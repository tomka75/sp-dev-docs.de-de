<span data-ttu-id="dd34b-p101">Dies verwendet eine Heuristik, um die zur bereitgestellten REST-URL gehörende SPWeb-URL zu erraten. Das ist für Vorgänge wie z. B. X-RequestDigest- und ODATA-Batchverarbeitung notwendig, die das Veröffentlichen in einem getrennten REST-Endpunkt erfordern, um eine Anforderung abzuschließen. Wenn zum Beispiel requestUrl "/sites/site/web/_api/service" ist, ist die zurückgegebene URL "/sites/site/web". Wenn requestUrl "http://example.com/_layouts/service" ist, ist die zurückgegebene URL "http://example.com".</span><span class="sxs-lookup"><span data-stu-id="dd34b-p101">This uses a heuristic to guess the SPWeb URL associated with the provided REST URL. This is necessary for operations such as the X-RequestDigest and ODATA batching, which require POSTing to a separate REST endpoint in order to complete a request. For excample, if the requestUrl is "/sites/site/web/_api/service", the returned URL would be "/sites/site/web". Or if the requestUrl is "http://example.com/_layouts/service", the returned URL would be "http://example.com".</span></span>




Dies verwendet eine Heuristik, um die zur bereitgestellten REST-URL gehörende SPWeb-URL zu erraten. Das ist für Vorgänge wie z. B. X-RequestDigest- und ODATA-Batchverarbeitung notwendig, die das Veröffentlichen in einem getrennten REST-Endpunkt erfordern, um eine Anforderung abzuschließen. Wenn zum Beispiel requestUrl "/sites/site/web/_api/service" ist, ist die zurückgegebene URL "/sites/site/web". Wenn requestUrl "http://example.com/_layouts/service" ist, ist die zurückgegebene URL "http://example.com".

<span data-ttu-id="dd34b-106">**Signatur:** _public static getWebUrlFromRequestUrl(requestUrl: string): string;_</span><span class="sxs-lookup"><span data-stu-id="dd34b-106">**Signature:** _public static getWebUrlFromRequestUrl(requestUrl: string): string;_</span></span>

<span data-ttu-id="dd34b-107">**Gibt Folgendes zurück**: `string`</span><span class="sxs-lookup"><span data-stu-id="dd34b-107">**Returns**: `string`</span></span>



<span data-ttu-id="dd34b-108">die abgeleitete SPWeb-URL</span><span class="sxs-lookup"><span data-stu-id="dd34b-108">the inferred SPWeb URL</span></span>

#### <a name="parameters"></a><span data-ttu-id="dd34b-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="dd34b-109">Parameters</span></span>


| <span data-ttu-id="dd34b-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="dd34b-110">Parameter</span></span>    | <span data-ttu-id="dd34b-111">Typ</span><span class="sxs-lookup"><span data-stu-id="dd34b-111">Type</span></span>    | <span data-ttu-id="dd34b-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dd34b-112">Description</span></span> |
|:-------------|:---------------|:------------|
| `requestUrl`    | `string` | <span data-ttu-id="dd34b-113">Die URL für einen SharePoint REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="dd34b-113">The URL for a SharePoint REST service</span></span> |


