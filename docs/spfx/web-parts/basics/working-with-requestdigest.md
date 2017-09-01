# <a name="working-with-requestdigest"></a>Arbeiten mit __REQUESTDIGEST

Beim Ausführen von Nicht-GET-REST-Anforderungen an die SharePoint-API müssen Sie einen gültigen Anforderungsdigest zu Ihrer Anforderung hinzufügen. Dieser Digest belegt die Gültigkeit Ihrer Anforderung für SharePoint. Da dieses Token nur eine begrenzte Zeit gültig ist, müssen Sie sicherstellen, dass das Token gültig ist, bevor Sie es zu der Anforderung hinzufügen. Andernfalls schlägt die Anforderung fehl. In diesem Artikel werden die unterschiedlichen Ansätze beschrieben, wie Sie einen gültigen Anforderungsdigest erhalten, sowie Tücken bei einigen häufig verwendeten Ansätzen.

## <a name="considerations-when-using-request-digest-from-the-hidden-requestdigest-field"></a>Aspekte bei Verwendung des Anforderungsdigest aus dem ausgeblendeten __REQUESTDIGEST-Feld

In klassischen Seiten schließt SharePoint ein Anforderungsdigesttoken auf der Seite in einem ausgeblendetes Feld mit dem Namen **__REQUESTDIGEST** ein. Eine der am häufigsten verwendeten Methoden zum Arbeiten mit dem Anforderungsdigest besteht darin, diesen über dieses Feld abzurufen und ihn dann zu der Anforderung hinzuzufügen. Beispiel:

```js
var digest = $('#__REQUESTDIGEST').val();
$.ajax({
    url: '/_api/web/...'
    method: "POST",
    headers: {
        "Accept": "application/json; odata=nometadata",
        "X-RequestDigest": digest
    },
    success: function (data) {
      // ...
    },
    error: function (data, errorCode, errorMessage) {
      // ...
    }
});
```

Eine solche Anforderung würde anfänglich funktionieren, wenn der Benutzer aber die Seite über einen längeren Zeitraum geöffnet lässt, würde der Anforderungsdigest auf der Seite ablaufen, und die Anforderung würde mit dem Ergebnis **403 FORBIDDEN** fehlschlagen. Standardmäßig ist ein Anforderungsdigesttoken 30 Minuten lang gültig, bevor Sie es verwenden, müssen Sie daher sicherstellen, dass es immer noch gültig ist. Bisher musste dies manuell durch Vergleichen des Zeitstempels des Anforderungsdigest mit der aktuellen Uhrzeit ausgeführt werden. In SharePoint Framework wird dieser Vorgang vereinfacht, indem Ihnen zwei Möglichkeiten bereitgestellt werden, um sicherzustellen, dass Ihre Anforderungen ein gültiges Anforderungsdigesttoken aufweist.

## <a name="use-the-sphttpclient-to-communicate-with-the-sharepoint-rest-api"></a>Verwenden von SPHttpClient zum Kommunizieren mit der SharePoint-REST-API

Die empfohlene Methode zum Kommunizieren mit der SharePoint-REST-API besteht in der Verwendung des SPHttpClient, der mit SharePoint Framework bereitgestellt wird. Diese Klasse verpackt ausstellende REST-Anforderungen an die SharePoint-REST-API in eine praktische Logik, die Ihren Code vereinfacht. Jedes Mal, wenn Sie beispielsweise eine Nicht-GET-Anforderung mithilfe von SPHttpClient ausstellen, wird automatisch ein gültiger Anforderungsdigest abgerufen und zur Anforderung hinzugefügt. Dadurch wird Ihre Lösung wesentlich vereinfacht, da Sie keinen Code erstellen müssen, um Anforderungsdigesttoken zu verwalten und deren Gültigkeit sicherzustellen.

Wenn Sie neue Anpassungen im SharePoint Framework erstellen, sollten Sie immer den SPHttpClient zum Kommunizieren mit der SharePoint-REST-API verwenden. Manchmal ist es jedoch vielleicht nicht möglich, den SPHttpClient zu verwenden. Dies ist beispielsweise der Fall, wenn Sie eine vorhanden Anpassung in das SharePoint Framework migrieren und so viel ursprünglichen Code wie möglich beibehalten möchten, oder wenn Sie eine Anpassung mithilfe einer Bibliothek wie Angular(JS) erstellen, die ihre eigenen Dienste zum Ausstellen von Webanforderungen aufweist. In diesen Fällen können Sie ein gültiges Anforderungsdigesttoken aus dem **DigestCache** abrufen.

## <a name="retrieve-valid-request-digest-using-the-digestcache-service"></a>Abrufen eines gültigen Anforderungsdigest mithilfe des DigestCache-Diensts

Wenn Sie den SPHttpClient nicht für die Kommunikation mit der SharePoint-REST-API verwenden können, können Sie mithilfe des **DigestCache**-Dienst, der mit dem SharePoint Framework bereitgestellt wird, ein gültiges Anforderungsdigesttoken abrufen. Der Vorteil der Verwendung des DigestCache-Diensts verglichen mit dem manuellen Abrufen eines gültigen Anforderungsdigesttoken besteht darin, dass DigestCache automatisch prüft, ob der zuvor abgerufene Anforderungsdigest immer noch gültig ist oder nicht. Wenn er abgelaufen ist, fordert der DigestCache-Dienst automatisch ein neues Anforderungsdigesttoken von SharePoint an und speichert es für nachfolgende Anforderungen. Die Verwendung von DigestCache vereinfacht Ihren Code und macht Ihre Lösung stabiler.

Um den DigestCache-Dienst in Ihrem Code zu verwenden, importieren Sie die Typen **DigestCache** und **IDigestCache** aus dem Paket **@microsoft/sp-http**:

```ts
// ...
import { IDigestCache, DigestCache } from '@microsoft/sp-http';

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  // ...
}
```

Als nächstes rufen Sie jedes Mal, wenn Sie ein gültiges Anforderungsdigesttoken benötigen, einen Verweis auf den DigestCache-Dienst ab und rufen seine **fetchDigest**-Methode auf:

```ts
// ...
import { IDigestCache, DigestCache } from '@microsoft/sp-http';

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  protected onInit(): Promise<void> {
    return new Promise<void>((resolve: () => void, reject: (error: any) => void): void => {
      const digestCache: IDigestCache = this.context.serviceScope.consume(DigestCache.serviceKey);
      digestCache.fetchDigest(this.context.pageContext.web.serverRelativeUrl).then((digest: string): void => {
        // use the digest here
        resolve();
      });
    });
  }

  // ...
}
```