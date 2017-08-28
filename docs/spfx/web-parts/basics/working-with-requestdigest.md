# <a name="working-with-the-original-requestdigest"></a><span data-ttu-id="04c50-101">Arbeiten mit dem ursprünglichen __RequestDigest</span><span class="sxs-lookup"><span data-stu-id="04c50-101">Working with the original __RequestDigest</span></span>

<span data-ttu-id="04c50-p101">Ein Großteil des Codes für die klassischen SharePoint-Seiten lässt sich auch mit SharePoint Framework verwenden. Manchmal jedoch fehlen einzelne Komponenten oder Variablen. Ein Beispiel ist das Formularfeld `__REQUESTDIGEST`. Im Idealfall würden Sie für den Zugriff auf den Digest keine globale Variable verwenden, sondern einfach das aktualisierte `HttpRequest`-Objekt für Ihren SharePoint-Aufruf nutzen. Dieses Objekt würde sich dann um die Digest-/Authentifizierungslogik kümmern (inklusive beispielsweise auch abgelaufener Token). Wie das funktioniert, ist im Artikel [Connect your client-side web part to SharePoint (Hello world part 2)](https://dev.office.com/sharepoint/docs/spfx/web-parts/get-started/connect-to-sharepoint) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="04c50-p101">There is a lot of code written to work with the classic SharePoint pages that you can use with the SharePoint Framework, but sometimes certain components or variables aren't there. One example is the __REQUESTDIGEST form field.  In an ideal world, you wouldn't use a global variable to access the digest, you'd just use the updated HttpRequest object to make your SharePoint call, and it will handle all the digest / auth logic for you (including things like expired tokens).  The Connect your client-side web part to SharePoint (Hello world part 2) article shows you how to do this.</span></span>

<span data-ttu-id="04c50-p102">Verwendet Ihr vorhandener Code jedoch einige ältere Konstrukte, können Sie mithilfe von clientseitigem Code und DOM-Manipulation diese Konstrukte ganz einfach wieder zur Seite hinzufügen. Dazu erstellen Sie einerseits einen Hook in der Methode `onInit` in der Webpart-Grundklasse und andererseits das DOM-Element, das dort eigentlich erwartet wird. Hier ein Codebeispiel, mit dem Sie das Formularelement `__REQUESTDIGEST` erstellen können:</span><span class="sxs-lookup"><span data-stu-id="04c50-p102">However, if your existing code uses some older constructs, through the power of client side code and DOM manipulation, it's fairly easy to add these back to a page.  The key is to hook into the onInit method in the base web part class, and pull the create the DOM element that you expect to be there.  Here's an example that creates the __REQESTDIGEST form element.</span></span>

```JavaScript
    public onInit<T>(): Promise<T>
    {
    // does the digest exist?
    if ( !document.getElementById('__REQUESTDIGEST') )
    {
      // OK, the request digest does not exist. Let's create it.
      // first, grab the digest value out of the contextWebInfo object (if it exists).
      var digestValue: string;
      try{
        digestValue = (window as any)._spClientSidePageContext.contextWebInfo.FormDigestValue;
      }
      catch (exception){
        // there is no digest on this page, so just return. This can easily happen on the local workbench
        return Promise.resolve();
      }

      if (digestValue){
        // OK, now lets create the digest input form. It looks like this:
        // <input type="hidden" name="__REQUESTDIGEST" id="__REQUESTDIGEST" value="blahblahblahblahblahblah, July23 -0000 or something like that">
        const requestDigestInput: Element = document.createElement('input');
        requestDigestInput.setAttribute('type', 'hidden');
        requestDigestInput.setAttribute('name', '__REQUESTDIGEST');
        requestDigestInput.setAttribute('id', '__REQUESTDIGEST');
        requestDigestInput.setAttribute('value', digestValue);

        // lastly, add the digest to the page
        document.body.appendChild(requestDigestInput);
      }
    }

    // no promise to return
    return Promise.resolve();
    }
```

><span data-ttu-id="04c50-109">**Hinweis:** Es gibt eine bessere Methode für den Abruf des aktuellen Digestwerts, die sich um sämtliche Aspekte kümmert, einschließlich Zwischenspeicherung, abgelaufener Token und erneutem Fetchen (hierzu müssen Sie `digestCacheServiceKey` und `IDigestCache` aus **sp-client-base** importieren):</span><span class="sxs-lookup"><span data-stu-id="04c50-109">Note: There is a better way to get the current digest value that will handle all of the caching / expiring / refetching / etc.  Give this a try.  You'll need to import digestCacheServiceKey and IDigestCache from sp-client-base</span></span>

```JavaScript
    var digestCache:IDigestCache = this.context.serviceScope.consume(digestCacheServiceKey);
    digestCache.fetchDigest(this.context.pageContext.web.serverRelativeUrl).then((digest: string) => {
      // Do Something with the digest
      console.log(digest);
    });
```
