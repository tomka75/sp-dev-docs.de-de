# <a name="working-with-requestdigest"></a><span data-ttu-id="b89c1-101">Arbeiten mit __REQUESTDIGEST</span><span class="sxs-lookup"><span data-stu-id="b89c1-101">Working with __REQUESTDIGEST</span></span>

<span data-ttu-id="b89c1-p101">Beim Ausführen von Nicht-GET-REST-Anforderungen an die SharePoint-API müssen Sie einen gültigen Anforderungsdigest zu Ihrer Anforderung hinzufügen. Dieser Digest belegt die Gültigkeit Ihrer Anforderung für SharePoint. Da dieses Token nur eine begrenzte Zeit gültig ist, müssen Sie sicherstellen, dass das Token gültig ist, bevor Sie es zu der Anforderung hinzufügen. Andernfalls schlägt die Anforderung fehl. In diesem Artikel werden die unterschiedlichen Ansätze beschrieben, wie Sie einen gültigen Anforderungsdigest erhalten, sowie Tücken bei einigen häufig verwendeten Ansätzen.</span><span class="sxs-lookup"><span data-stu-id="b89c1-p101">When executing non-GET REST requests to the SharePoint API, you must add a valid request digest to your request. This digest proves validity of your request to SharePoint. Because this token is valid only for a limited period of time, you have to ensure that the token you have is valid, before adding it to your request or the request will fail. This article describes the different approaches to obtain a valid request digest and pitfalls of some commonly used approaches.</span></span>

## <a name="considerations-when-using-request-digest-from-the-hidden-requestdigest-field"></a><span data-ttu-id="b89c1-106">Aspekte bei Verwendung des Anforderungsdigest aus dem ausgeblendeten __REQUESTDIGEST-Feld</span><span class="sxs-lookup"><span data-stu-id="b89c1-106">Considerations when using request digest from the hidden __REQUESTDIGEST field</span></span>

<span data-ttu-id="b89c1-p102">In klassischen Seiten schließt SharePoint ein Anforderungsdigesttoken auf der Seite in einem ausgeblendetes Feld mit dem Namen **__REQUESTDIGEST** ein. Eine der am häufigsten verwendeten Methoden zum Arbeiten mit dem Anforderungsdigest besteht darin, diesen über dieses Feld abzurufen und ihn dann zu der Anforderung hinzuzufügen. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b89c1-p102">In classic pages, SharePoint includes a request digest token on the page in a hidden field named **__REQUESTDIGEST**. One of the most common approaches to work with the request digest, is to obtain it from that field and add it to the request, for example:</span></span>

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

<span data-ttu-id="b89c1-p103">Eine solche Anforderung würde anfänglich funktionieren, wenn der Benutzer aber die Seite über einen längeren Zeitraum geöffnet lässt, würde der Anforderungsdigest auf der Seite ablaufen, und die Anforderung würde mit dem Ergebnis **403 FORBIDDEN** fehlschlagen. Standardmäßig ist ein Anforderungsdigesttoken 30 Minuten lang gültig, bevor Sie es verwenden, müssen Sie daher sicherstellen, dass es immer noch gültig ist. Bisher musste dies manuell durch Vergleichen des Zeitstempels des Anforderungsdigest mit der aktuellen Uhrzeit ausgeführt werden. In SharePoint Framework wird dieser Vorgang vereinfacht, indem Ihnen zwei Möglichkeiten bereitgestellt werden, um sicherzustellen, dass Ihre Anforderungen ein gültiges Anforderungsdigesttoken aufweist.</span><span class="sxs-lookup"><span data-stu-id="b89c1-p103">Such request would work initially, but if the user would have the page open for a longer period of time, the request digest on the page would expire and the request would fail with a **403 FORBIDDEN** result. By default, a request digest token is valid for 30 minutes, so before using it, you have to ensure that it's still valid. In the past you had to do this manually, by comparing the timestamp from the request digest with the current time. SharePoint Framework simplifies this process by offering you two ways of ensuring that your request has a valid request digest token.</span></span>

## <a name="use-the-sphttpclient-to-communicate-with-the-sharepoint-rest-api"></a><span data-ttu-id="b89c1-113">Verwenden von SPHttpClient zum Kommunizieren mit der SharePoint-REST-API</span><span class="sxs-lookup"><span data-stu-id="b89c1-113">Use the SPHttpClient to communicate with the SharePoint REST API</span></span>

<span data-ttu-id="b89c1-p104">Die empfohlene Methode zum Kommunizieren mit der SharePoint-REST-API besteht in der Verwendung des SPHttpClient, der mit SharePoint Framework bereitgestellt wird. Diese Klasse verpackt ausstellende REST-Anforderungen an die SharePoint-REST-API in eine praktische Logik, die Ihren Code vereinfacht. Jedes Mal, wenn Sie beispielsweise eine Nicht-GET-Anforderung mithilfe von SPHttpClient ausstellen, wird automatisch ein gültiger Anforderungsdigest abgerufen und zur Anforderung hinzugefügt. Dadurch wird Ihre Lösung wesentlich vereinfacht, da Sie keinen Code erstellen müssen, um Anforderungsdigesttoken zu verwalten und deren Gültigkeit sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="b89c1-p104">The recommended way to communicate with the SharePoint REST API is using the SPHttpClient provided with the SharePoint Framework. This class wraps issuing REST requests to the SharePoint REST API with convenient logic that simplifies your code. For example, whenever you issue a non-GET request using the SPHttpClient, it will automatically obtain a valid request digest and add it to the request. This significantly simplifies your solution as you don't need to build code to manage request digest tokens and ensure their validity.</span></span>

<span data-ttu-id="b89c1-p105">Wenn Sie neue Anpassungen im SharePoint Framework erstellen, sollten Sie immer den SPHttpClient zum Kommunizieren mit der SharePoint-REST-API verwenden. Manchmal ist es jedoch vielleicht nicht möglich, den SPHttpClient zu verwenden. Dies ist beispielsweise der Fall, wenn Sie eine vorhanden Anpassung in das SharePoint Framework migrieren und so viel ursprünglichen Code wie möglich beibehalten möchten, oder wenn Sie eine Anpassung mithilfe einer Bibliothek wie Angular(JS) erstellen, die ihre eigenen Dienste zum Ausstellen von Webanforderungen aufweist. In diesen Fällen können Sie ein gültiges Anforderungsdigesttoken aus dem **DigestCache** abrufen.</span><span class="sxs-lookup"><span data-stu-id="b89c1-p105">If you're building new customizations on the SharePoint Framework, you should always use the SPHttpClient to communicate with the SharePoint REST API. Sometimes however, you might not be able to use the SPHttpClient. This can be the case for example when you're migrating an existing customization to the SharePoint Framework and want to keep as much of the original code as possible, or you're building a customization using a library such as Angular(JS), that has its own services for issuing web requests. In such cases you can obtain a valid request digest token from the **DigestCache**.</span></span>

## <a name="retrieve-valid-request-digest-using-the-digestcache-service"></a><span data-ttu-id="b89c1-122">Abrufen eines gültigen Anforderungsdigest mithilfe des DigestCache-Diensts</span><span class="sxs-lookup"><span data-stu-id="b89c1-122">Retrieve valid request digest using the DigestCache service</span></span>

<span data-ttu-id="b89c1-p106">Wenn Sie den SPHttpClient nicht für die Kommunikation mit der SharePoint-REST-API verwenden können, können Sie mithilfe des **DigestCache**-Dienst, der mit dem SharePoint Framework bereitgestellt wird, ein gültiges Anforderungsdigesttoken abrufen. Der Vorteil der Verwendung des DigestCache-Diensts verglichen mit dem manuellen Abrufen eines gültigen Anforderungsdigesttoken besteht darin, dass DigestCache automatisch prüft, ob der zuvor abgerufene Anforderungsdigest immer noch gültig ist oder nicht. Wenn er abgelaufen ist, fordert der DigestCache-Dienst automatisch ein neues Anforderungsdigesttoken von SharePoint an und speichert es für nachfolgende Anforderungen. Die Verwendung von DigestCache vereinfacht Ihren Code und macht Ihre Lösung stabiler.</span><span class="sxs-lookup"><span data-stu-id="b89c1-p106">If you can't use the SPHttpClient for communicating with the SharePoint REST API, you can obtain a valid request digest token using the **DigestCache** service provided with the SharePoint Framework. The benefit of using the DigestCache service over manually obtaining a valid request digest token is, that the DigestCache automatically checks if the previously retrieved request digest is still valid or not. If it's expired, the DigestCache service will automatically request a new request digest token from SharePoint and store it from subsequent requests. Using the DigestCache simplifies your code and makes your solution more robust.</span></span>

<span data-ttu-id="b89c1-127">Um den DigestCache-Dienst in Ihrem Code zu verwenden, importieren Sie die Typen **DigestCache** und **IDigestCache** aus dem Paket **@microsoft/sp-http**:</span><span class="sxs-lookup"><span data-stu-id="b89c1-127">To use the DigestCache service in your code, first import the **DigestCache** and **IDigestCache** types from the **@microsoft/sp-http** package:</span></span>

```ts
// ...
import { IDigestCache, DigestCache } from '@microsoft/sp-http';

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  // ...
}
```

<span data-ttu-id="b89c1-128">Als nächstes rufen Sie jedes Mal, wenn Sie ein gültiges Anforderungsdigesttoken benötigen, einen Verweis auf den DigestCache-Dienst ab und rufen seine **fetchDigest**-Methode auf:</span><span class="sxs-lookup"><span data-stu-id="b89c1-128">Next, whenever you need a valid request digest token, retrieve a reference to the DigestCache service and call its **fetchDigest** method:</span></span>

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