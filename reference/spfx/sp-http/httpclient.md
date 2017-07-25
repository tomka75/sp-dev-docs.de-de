<span data-ttu-id="adff2-p104">Führt einen REST-Dienstanruf aus. Obwohl die SPHttpClient-Unterklasse Verbesserungen hinzufügt, sind die Parameter und die Semantik für HttpClient.fetch() im Wesentlichen identisch mit dem WHATWG-API-Standard, der hier dokumentiert wird: https://fetch.spec.whatwg.org/</span><span class="sxs-lookup"><span data-stu-id="adff2-p104">Performs a REST service call. Although the SPHttpClient subclass adds additional enhancements, the parameters and semantics for HttpClient.fetch() are essentially the same as the WHATWG API standard that is documented here: https://fetch.spec.whatwg.org/</span></span>|
|:-------------|:----|:-------|:-----------|
|[`fetch(url,configuration,options)`](fetch-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | Führt einen REST-Dienstanruf aus. Obwohl die SPHttpClient-Unterklasse Verbesserungen hinzufügt, sind die Parameter und die Semantik für HttpClient.fetch() im Wesentlichen identisch mit dem WHATWG-API-Standard, der hier dokumentiert wird: https://fetch.spec.whatwg.org/ |
|[`fetchCore()`](fetchcore-httpclient.md)     | `protected` | `Promise<Response>` | <span data-ttu-id="adff2-126">Mit dieser Methode, die das zugrunde liegende IFetchProvider.fetch() aufruft, werden alle Netzwerkanfragen weitergeleitet.</span><span class="sxs-lookup"><span data-stu-id="adff2-126">All network requests are routed through this method, which calls the underlying IFetchProvider.fetch().</span></span> |
|[`get(url,configuration,options)`](get-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | <span data-ttu-id="adff2-127">Ruft fetch() auf, legt die Methode aber auf 'GET' fest.</span><span class="sxs-lookup"><span data-stu-id="adff2-127">Calls fetch(), but sets the method to 'GET'.</span></span> |
|[`post(url,configuration,options)`](post-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | <span data-ttu-id="adff2-128">Ruft fetch() auf, legt die Methode aber auf 'POST' fest.</span><span class="sxs-lookup"><span data-stu-id="adff2-128">Calls fetch(), but sets the method to 'POST'.</span></span> |





