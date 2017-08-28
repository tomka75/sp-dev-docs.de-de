# <a name="working-with-the-original-requestdigest"></a>Arbeiten mit dem ursprünglichen __RequestDigest

Ein Großteil des Codes für die klassischen SharePoint-Seiten lässt sich auch mit SharePoint Framework verwenden. Manchmal jedoch fehlen einzelne Komponenten oder Variablen. Ein Beispiel ist das Formularfeld `__REQUESTDIGEST`. Im Idealfall würden Sie für den Zugriff auf den Digest keine globale Variable verwenden, sondern einfach das aktualisierte `HttpRequest`-Objekt für Ihren SharePoint-Aufruf nutzen. Dieses Objekt würde sich dann um die Digest-/Authentifizierungslogik kümmern (inklusive beispielsweise auch abgelaufener Token). Wie das funktioniert, ist im Artikel [Connect your client-side web part to SharePoint (Hello world part 2)](https://dev.office.com/sharepoint/docs/spfx/web-parts/get-started/connect-to-sharepoint) beschrieben.

Verwendet Ihr vorhandener Code jedoch einige ältere Konstrukte, können Sie mithilfe von clientseitigem Code und DOM-Manipulation diese Konstrukte ganz einfach wieder zur Seite hinzufügen. Dazu erstellen Sie einerseits einen Hook in der Methode `onInit` in der Webpart-Grundklasse und andererseits das DOM-Element, das dort eigentlich erwartet wird. Hier ein Codebeispiel, mit dem Sie das Formularelement `__REQUESTDIGEST` erstellen können:

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

>**Hinweis:** Es gibt eine bessere Methode für den Abruf des aktuellen Digestwerts, die sich um sämtliche Aspekte kümmert, einschließlich Zwischenspeicherung, abgelaufener Token und erneutem Fetchen (hierzu müssen Sie `digestCacheServiceKey` und `IDigestCache` aus **sp-client-base** importieren):

```JavaScript
    var digestCache:IDigestCache = this.context.serviceScope.consume(digestCacheServiceKey);
    digestCache.fetchDigest(this.context.pageContext.web.serverRelativeUrl).then((digest: string) => {
      // Do Something with the digest
      console.log(digest);
    });
```
