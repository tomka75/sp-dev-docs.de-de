<span data-ttu-id="eba22-p102">Führt einen REST-Dienstanruf aus. Obwohl die SPHttpClient-Unterklasse Verbesserungen hinzufügt, sind die Parameter und die Semantik für HttpClient.fetch() im Wesentlichen identisch mit dem WHATWG-API-Standard, der hier dokumentiert wird: https://fetch.spec.whatwg.org/</span><span class="sxs-lookup"><span data-stu-id="eba22-p102">Performs a REST service call. Although the SPHttpClient subclass adds additional enhancements, the parameters and semantics for HttpClient.fetch() are essentially the same as the WHATWG API standard that is documented here: https://fetch.spec.whatwg.org/</span></span>

Führt einen REST-Dienstanruf aus. Obwohl die SPHttpClient-Unterklasse Verbesserungen hinzufügt, sind die Parameter und die Semantik für HttpClient.fetch() im Wesentlichen identisch mit dem WHATWG-API-Standard, der hier dokumentiert wird: https://fetch.spec.whatwg.org/

<span data-ttu-id="eba22-106">**Signatur:** _@virtual public fetch(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), Optionen: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_</span><span class="sxs-lookup"><span data-stu-id="eba22-106">**Signature:** _@virtual public fetch(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), options: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_</span></span>

<span data-ttu-id="eba22-107">**Gibt Folgendes zurück**: `Promise<HttpClientResponse>`</span><span class="sxs-lookup"><span data-stu-id="eba22-107">**Returns**: `Promise<HttpClientResponse>`</span></span>



<span data-ttu-id="eba22-108">Eine Zusage, die das Ergebnis zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="eba22-108">a promise that will return the result</span></span>

#### <a name="parameters"></a><span data-ttu-id="eba22-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="eba22-109">Parameters</span></span>


| <span data-ttu-id="eba22-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="eba22-110">Parameter</span></span>    | <span data-ttu-id="eba22-111">Typ</span><span class="sxs-lookup"><span data-stu-id="eba22-111">Type</span></span>    | <span data-ttu-id="eba22-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="eba22-112">Description</span></span> |
|:-------------|:---------------|:------------|
| `url`    | `string` | <span data-ttu-id="eba22-113">Die abzurufende URL</span><span class="sxs-lookup"><span data-stu-id="eba22-113">the URL to fetch</span></span> |
| `configuration`    | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | <span data-ttu-id="eba22-114">Bestimmt das Standardverhalten von HttpClient; dies sollte normalerweise die neueste Versionsnummer von HttpClientConfigurations sein.</span><span class="sxs-lookup"><span data-stu-id="eba22-114">determines the default behavior of HttpClient; normally this should be the latest version number from HttpClientConfigurations</span></span> |
| `options`    | [`IHttpClientOptions`](../sp-http/ihttpclientoptions.md) | <span data-ttu-id="eba22-115">Zusätzliche Optionen, die Auswirkungen auf die Anforderung haben.</span><span class="sxs-lookup"><span data-stu-id="eba22-115">additional options that affect the request</span></span> |


