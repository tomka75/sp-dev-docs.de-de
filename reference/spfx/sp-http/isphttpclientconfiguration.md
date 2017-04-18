# <a name="isphttpclientconfiguration-interface"></a>ISPHttpClientConfiguration-Schnittstelle







Flags-Schnittstelle für SPHttpClientConfiguration.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`defaultODataVersion`      | [`ODataVersion`](../sp-http/odataversion.md) | Wenn dieser Schalter angegeben (d. h. definiert) ist: Wenn die „OData-Version“-Kopfzeile nicht explizit für die Anforderung hinzugefügt wurde, wird die Kopfzeile von SPHttpClient hinzugefügt, um die von defaultODataVersion angegebene Version anzugeben. HINWEIS: Ohne eine „OData-Version“-Kopfzeile wird für SharePoint-Server derzeit standardmäßig in den meisten Fällen Version 3.0 verwendet. Die empfohlene Version ist 4.0. |
|`defaultSameOriginCredentials`      | `boolean` | Wenn dieser Schalter „true“ ist: Wenn RequestInit.credentials nicht explizit für die Anforderung angegeben wird, wird dieser Wert von SPHttpClient auf „same-origin“ festgelegt. Ohne diesen Schalter können unterschiedliche Webbrowser unterschiedliche Standardwerte anwenden. Weitere Informationen finden Sie in der Spezifikation: https://fetch.spec.whatwg.org/#cors-protocol-and-credentials |
|`requestDigest`      | `boolean` | Wenn dieser Schalter „true“ ist: Wenn die „X-RequestDigest“-Kopfzeile nicht explizit für die Anforderung hinzugefügt wurde, so wird diese von SPHttpClient hinzugefügt, wenn die Anforderung ein Schreibvorgang ist (d. h. eine andere HTTP-Methode als „GET“, „HEAD“ oder „OPTIONS“) ist. Der Anforderungsdigest wird vom DigestCache-Dienst verwaltet. Im Falle eines Cachefehlers kann eine zusätzliche Netzwerkanforderung ausgeführt werden. |






