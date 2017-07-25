# <a name="posturlconfigurationoptions"></a><span data-ttu-id="3292c-101">post(url,configuration,options)</span><span class="sxs-lookup"><span data-stu-id="3292c-101">post(url,configuration,options)</span></span>




<span data-ttu-id="3292c-102">Ruft fetch() auf, legt die Methode aber auf ‚POST‘ fest.</span><span class="sxs-lookup"><span data-stu-id="3292c-102">Calls fetch(), but sets the method to 'POST'.</span></span>

<span data-ttu-id="3292c-103">**Signatur:** _@virtual public post(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), Optionen: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_</span><span class="sxs-lookup"><span data-stu-id="3292c-103">**Signature:** _@virtual public post(url: string, configuration: [HttpClientConfiguration](../sp-http/httpclientconfiguration.md), options: [IHttpClientOptions](../sp-http/ihttpclientoptions.md)): Promise<[HttpClientResponse](../sp-http/httpclientresponse.md)>;_</span></span>

<span data-ttu-id="3292c-104">**Gibt Folgendes zurück**: `Promise<HttpClientResponse>`</span><span class="sxs-lookup"><span data-stu-id="3292c-104">**Returns**: `Promise<HttpClientResponse>`</span></span>



<span data-ttu-id="3292c-105">Eine Zusage, die das Ergebnis zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="3292c-105">a promise that will return the result</span></span>

#### <a name="parameters"></a><span data-ttu-id="3292c-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="3292c-106">Parameters</span></span>


| <span data-ttu-id="3292c-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="3292c-107">Parameter</span></span>    | <span data-ttu-id="3292c-108">Typ</span><span class="sxs-lookup"><span data-stu-id="3292c-108">Type</span></span>    | <span data-ttu-id="3292c-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3292c-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `url`    | `string` | <span data-ttu-id="3292c-110">Die abzurufende URL</span><span class="sxs-lookup"><span data-stu-id="3292c-110">the URL to fetch</span></span> |
| `configuration`    | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | <span data-ttu-id="3292c-111">Bestimmt das Standardverhalten von HttpClient; dies sollte normalerweise die neueste Versionsnummer von HttpClientConfigurations sein.</span><span class="sxs-lookup"><span data-stu-id="3292c-111">determines the default behavior of HttpClient; normally this should be the latest version number from HttpClientConfigurations</span></span> |
| `options`    | [`IHttpClientOptions`](../sp-http/ihttpclientoptions.md) | <span data-ttu-id="3292c-112">Zusätzliche Optionen, die Auswirkungen auf die Anforderung haben.</span><span class="sxs-lookup"><span data-stu-id="3292c-112">additional options that affect the request</span></span> |


