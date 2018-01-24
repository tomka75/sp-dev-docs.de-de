---
title: Arbeiten mit __REQUESTDIGEST
description: "Fügen Sie einen gültigen Anforderungsdigest zu Ihrer Anforderung hinzu, wenn Sie Nicht-GET-REST-Anforderung auf der SharePoint-API ausführen."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: 8a357c2a199566dbbf24f209c18b5f4673bd8b1a
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="work-with-requestdigest"></a>Arbeiten mit __REQUESTDIGEST

Bei der Ausführung von Nicht-GET-REST-Anforderungen auf der SharePoint-API müssen Sie einen gültigen Anforderungsdigest zu Ihrer Anforderung hinzufügen. Dieser Digest beweist SharePoint die Gültigkeit Ihrer Anforderung. Da dieses Token nur für einen begrenzten Zeitraum gültig ist, müssen Sie sicherstellen, dass das vorhandene Token gültig ist, bevor Sie es zu Ihrer Anforderung hinzufügen, da die Anforderung ansonsten fehlschlägt. 

Auf klassischen Seiten enthält SharePoint ein Anforderungsdigesttoken auf der Seite in einem verborgenen Feld namens **__REQUESTDIGEST**. Eine der am häufigsten verwendeten Arbeitsmethoden für den Anforderungsdigest ist, ihn aus diesem Feld abzurufen und zu der Anforderung hinzuzufügen, wie z. B.:

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

Eine solche Anforderung würde zunächst funktionieren, aber wenn der Benutzer die Seite für einen längeren Zeitraum geöffnet hat, läuft der Anforderungsdigest auf der Seite ab und die Anforderung schlägt mit dem Ergebnis **403 VERBOTEN** fehl. Standardmäßig ist ein Anforderungsdigesttoken 30 Minuten gültig. Vor der Verwendung sollten Sie daher überprüfen, ob es noch gültig ist. In der Vergangenheit musste dies manuell durch den Vergleich des Zeitstempels aus dem Anforderungsdigest mit der aktuellen Zeit erfolgen. 

SharePoint-Framework vereinfacht diesen Prozess durch zwei Möglichkeiten, mit denen Sie sicherstellen können, dass Ihre Anforderung ein gültiges Anforderungsdigesttoken enthält.

## <a name="use-the-sphttpclient-to-communicate-with-the-sharepoint-rest-api"></a>Verwenden von SPHttpClient zum Kommunizieren mit der SharePoint-REST-API

Die empfohlene Vorgehensweise für die Kommunikation mit der SharePoint-REST-API besteht in der Verwendung des im Lieferumfang des SharePoint-Frameworks enthaltenen SPHttpClient. Diese Klasse umfasst die Ausgabe von REST-Anforderungen an die SharePoint-REST-API mit geeigneter Logik, die Ihren Code vereinfacht. 

Wenn Sie z. B. eine Nicht-GET-Anforderung mithilfe eines SPHttpClient ausgeben, erhält dieser automatisch einen gültigen Anforderungsdigest und fügt diesen der Anforderung hinzu. Dies vereinfacht Ihre Lösung erheblich, da Sie keinen Code programmieren müssen, um Anforderungsdigesttoken zu verwalten und deren Gültigkeit sicherzustellen.

Wenn Sie eine neue Anpassungen auf dem SharePoint-Framework erstellen, sollten Sie für die Kommunikation mit der SharePoint-REST-API immer den SPHttpClient verwenden. 

In manchen Fällen können Sie den SPHttpClient möglicherweise nicht verwenden. Dies kann z. B. der Fall sein, wenn Sie eine vorhandene Anpassung auf die SharePoint-Framework migrieren und so viel wie möglich von dem ursprünglichen Code beibehalten möchten oder wenn Sie eine Anpassung mithilfe einer Bibliothek, wie z. B. Angular(JS) erstellen möchten, die über einen eigenen Service für die Ausgabe von Webanfragen verfügt. In solchen Fällen erhalten Sie ein gültiges Anforderungsdigesttoken aus dem **DigestCache**.

## <a name="retrieve-a-valid-request-digest-by-using-the-digestcache-service"></a>Abrufen eines gültigen Anforderungsdigest mithilfe des DigestCache-Diensts

Wenn Sie den SPHttpClient nicht für die Kommunikation mit der SharePoint-REST-API verwenden können, können Sie ein gültiges Anforderungsdigesttoken erhalten, indem Sie den mit der SharePoint-Framework bereitgestellten **DigestCache**-Dienst verwenden. 

Der Vorteil der Verwendung des DigestCache-Dienstes gegenüber der manuellen Anforderung eines gültigen Anforderungsdigesttoken ist, dass der DigestCache automatisch überprüft, ob der zuvor abgerufene Anforderungsdigest noch gültig ist. Falls er abgelaufen ist, fordert der DigestCache-Dienst automatisch ein neues Anforderungsdigesttoken bei SharePoint an und speichert es für nachfolgende Anforderungen. DigestCache vereinfacht die Programmierung und macht Ihre Lösung robuster.

### <a name="to-use-the-digestcache-service-in-your-code"></a>Verwenden des DigestCache-Dienstes im Code

1. Importieren Sie die Typen **DigestCache** und **IDigestCache** aus dem Paket **@microsoft/sp-http**:

  ```ts
  // ...
  import { IDigestCache, DigestCache } from '@microsoft/sp-http';

  export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
    // ...
  }
  ```

2. Wenn Sie ein gültiges Anforderungsdigesttoken benötigen, rufen Sie einen Verweis auf den DigestCache-Dienst ab und rufen Sie dann seine **fetchDigest**-Methode auf:

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