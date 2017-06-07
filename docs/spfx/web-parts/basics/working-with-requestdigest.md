# <a name="working-with-the-original-requestdigest"></a>Arbeiten mit dem ursprünglichen __RequestDigest

Um mit den klassischen SharePoint-Seiten zu arbeiten, die Sie mit dem SharePoint Framework verwenden können, muss eine Menge Code geschrieben werden, aber manchmal gibt es bestimmte Komponenten oder Variablen nicht. Ein Beispiel ist das __REQUESTDIGEST-Formularfeld.  In einer idealen Welt würden Sie keine globale Variable verwenden, um auf den Digest zuzugreifen, Sie würden einfach das aktualisierte **HttpRequest**-Objekt verwenden, um den SharePoint-Aufruf durchzuführen, und dieser würde den gesamten Digest/die gesamte Authentifizierungslogik (einschließlich abgelaufener Token) für Sie verarbeiten.  Im Artikel [Verbinden Ihres clientseitigen Webparts mit SharePoint (Hallo Welt, Teil 2)](https://github.com/SharePoint/sp-dev-docs/wiki/HelloWorld,-Talking-to-SharePoint) erfahren Sie, wie dies funktioniert.

Wenn Ihr vorhandener Code jedoch dank clientseitigem Code und DOM-Manipulation einige ältere Konstrukte verwendet, können diese relativ einfach wieder zu einer Seite hinzugefügt werden.  Wichtig ist, dass eine Verknüpfung mit der**onInit**-Methode in der grundlegenden Webpartklasse hergestellt und das DOM-Element, das Sie dort erwarten, erstellt wird.  Nachfolgend finden Sie ein Beispiel, in dem das __REQESTDIGEST-Formularelement erstellt wird.

```JavaScript
    public onInit<T>(): Promise<T>
    {
    // does the digest exist?
    if ( !document.getElementById('__REQUESTDIGEST') )
    {
      // OK, the request digest does not exist.  Let's create it.
      // first, grab the digest value out of the contextWebInfo object (if it exists).
      var digestValue: string;
      try{
        digestValue = (window as any)._spClientSidePageContext.contextWebInfo.FormDigestValue;
      }
      catch (exception){
        // there is no digest on this page, so just return.  This can easily happen on the local workbench
        return Promise.resolve();
      }

      if (digestValue){
        // OK, now lets create the digest input form.  It looks like this -
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

>**Hinweis:** Es gibt eine bessere Methode, um den aktuellen Digestwert abzurufen, der den gesamten Cache, das Ablaufen, das erneute Abrufen usw. verarbeitet.  Probieren Sie es aus.  Sie müssen DigestCacheServiceKey und IDigestCache aus sp-client-case importieren.

```JavaScript
    var digestCache:IDigestCache = this.context.serviceScope.consume(digestCacheServiceKey);
    digestCache.fetchDigest(this.context.pageContext.web.serverRelativeUrl).then((digest: string) => {
      // Do Something with the digest
      console.log(digest);
    });
```