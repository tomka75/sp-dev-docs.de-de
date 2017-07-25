<span data-ttu-id="dc55b-p103">Wenn dieser Schalter „true“ ist: Wenn die „X-RequestDigest“-Kopfzeile nicht explizit für die Anforderung hinzugefügt wurde, so wird diese von SPHttpClient hinzugefügt, wenn die Anforderung ein Schreibvorgang ist (d. h. eine andere HTTP-Methode als „GET“, „HEAD“ oder „OPTIONS“) ist. Der Anforderungsdigest wird vom DigestCache-Dienst verwaltet. Im Falle eines Cachefehlers kann eine zusätzliche Netzwerkanforderung ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="dc55b-p103">When this switch is true: If the 'X-RequestDigest' header was not explicitly added for the request, then SPHttpClient will add it if the request is a write operation (i.e. an HTTP method other than 'GET', 'HEAD', or 'OPTIONS'). The request digest is managed by the DigestCache service. In the case of a cache miss, an additional network request may be performed.</span></span> |
|`requestDigest`      | `boolean` | Wenn dieser Schalter „true“ ist: Wenn die „X-RequestDigest“-Kopfzeile nicht explizit für die Anforderung hinzugefügt wurde, so wird diese von SPHttpClient hinzugefügt, wenn die Anforderung ein Schreibvorgang ist (d. h. eine andere HTTP-Methode als „GET“, „HEAD“ oder „OPTIONS“) ist. Der Anforderungsdigest wird vom DigestCache-Dienst verwaltet. Im Falle eines Cachefehlers kann eine zusätzliche Netzwerkanforderung ausgeführt werden. |






