# <a name="posturlconfigurationoptions"></a><span data-ttu-id="ac734-101">post(url,configuration,options)</span><span class="sxs-lookup"><span data-stu-id="ac734-101">post(url,configuration,options)</span></span>




<span data-ttu-id="ac734-102">Ruft fetch() auf, legt die Methode aber auf ‚POST‘ fest.</span><span class="sxs-lookup"><span data-stu-id="ac734-102">Calls fetch(), but sets the method to 'POST'.</span></span>

<span data-ttu-id="ac734-103">**Signatur:** _@override public post(url: string, configuration: [SPHttpClientConfiguration](../sp-http/sphttpclientconfiguration.md), Optionen: [ISPHttpClientOptions](../sp-http/isphttpclientoptions.md)): Promise<[SPHttpClientResponse](../sp-http/sphttpclientresponse.md)>;_</span><span class="sxs-lookup"><span data-stu-id="ac734-103">**Signature:** _@override public post(url: string, configuration: [SPHttpClientConfiguration](../sp-http/sphttpclientconfiguration.md), options: [ISPHttpClientOptions](../sp-http/isphttpclientoptions.md)): Promise<[SPHttpClientResponse](../sp-http/sphttpclientresponse.md)>;_</span></span>

<span data-ttu-id="ac734-104">**Gibt Folgendes zurück**: `Promise<SPHttpClientResponse>`</span><span class="sxs-lookup"><span data-stu-id="ac734-104">**Returns**: `Promise<SPHttpClientResponse>`</span></span>



<span data-ttu-id="ac734-105">Eine Zusage, die das Ergebnis zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="ac734-105">a promise that will return the result</span></span>

#### <a name="parameters"></a><span data-ttu-id="ac734-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="ac734-106">Parameters</span></span>


| <span data-ttu-id="ac734-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="ac734-107">Parameter</span></span>    | <span data-ttu-id="ac734-108">Typ</span><span class="sxs-lookup"><span data-stu-id="ac734-108">Type</span></span>    | <span data-ttu-id="ac734-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ac734-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `url`    | `string` | <span data-ttu-id="ac734-110">Die abzurufende URL</span><span class="sxs-lookup"><span data-stu-id="ac734-110">the URL to fetch</span></span> |
| `configuration`    | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | <span data-ttu-id="ac734-111">Bestimmt das Standardverhalten von SPHttpClient; dies sollte normalerweise die neueste Versionsnummer von SPHttpClientConfigurations sein.</span><span class="sxs-lookup"><span data-stu-id="ac734-111">determines the default behavior of SPHttpClient; normally this should be the latest version number from SPHttpClientConfigurations</span></span> |
| `options`    | [`ISPHttpClientOptions`](../sp-http/isphttpclientoptions.md) | <span data-ttu-id="ac734-112">Zusätzliche Optionen, die Auswirkungen auf die Anforderung haben.</span><span class="sxs-lookup"><span data-stu-id="ac734-112">additional options that affect the request</span></span> |


