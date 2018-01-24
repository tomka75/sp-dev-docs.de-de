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
# <a name="work-with-requestdigest"></a><span data-ttu-id="02213-103">Arbeiten mit __REQUESTDIGEST</span><span class="sxs-lookup"><span data-stu-id="02213-103">Work with __REQUESTDIGEST</span></span>

<span data-ttu-id="02213-104">Bei der Ausführung von Nicht-GET-REST-Anforderungen auf der SharePoint-API müssen Sie einen gültigen Anforderungsdigest zu Ihrer Anforderung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="02213-104">When executing non-GET REST requests to the SharePoint API, you must add a valid request digest to your request.</span></span> <span data-ttu-id="02213-105">Dieser Digest beweist SharePoint die Gültigkeit Ihrer Anforderung.</span><span class="sxs-lookup"><span data-stu-id="02213-105">This digest proves validity of your request to SharePoint.</span></span> <span data-ttu-id="02213-106">Da dieses Token nur für einen begrenzten Zeitraum gültig ist, müssen Sie sicherstellen, dass das vorhandene Token gültig ist, bevor Sie es zu Ihrer Anforderung hinzufügen, da die Anforderung ansonsten fehlschlägt.</span><span class="sxs-lookup"><span data-stu-id="02213-106">Because this token is valid only for a limited period of time, you have to ensure that the token you have is valid before adding it to your request or the request fails.</span></span> 

<span data-ttu-id="02213-107">Auf klassischen Seiten enthält SharePoint ein Anforderungsdigesttoken auf der Seite in einem verborgenen Feld namens **__REQUESTDIGEST**.</span><span class="sxs-lookup"><span data-stu-id="02213-107">In classic pages, SharePoint includes a request digest token on the page in a hidden field named **__REQUESTDIGEST**.</span></span> <span data-ttu-id="02213-108">Eine der am häufigsten verwendeten Arbeitsmethoden für den Anforderungsdigest ist, ihn aus diesem Feld abzurufen und zu der Anforderung hinzuzufügen, wie z. B.:</span><span class="sxs-lookup"><span data-stu-id="02213-108">In classic pages, SharePoint includes a request digest token on the page in a hidden field named __REQUESTDIGEST. One of the most common approaches to work with the request digest, is to obtain it from that field and add it to the request, for example:</span></span>

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

<span data-ttu-id="02213-109">Eine solche Anforderung würde zunächst funktionieren, aber wenn der Benutzer die Seite für einen längeren Zeitraum geöffnet hat, läuft der Anforderungsdigest auf der Seite ab und die Anforderung schlägt mit dem Ergebnis **403 VERBOTEN** fehl.</span><span class="sxs-lookup"><span data-stu-id="02213-109">Such a request would work initially, but if the user has the page open for a longer period of time, the request digest on the page expires and the request fails with a **403 FORBIDDEN** result.</span></span> <span data-ttu-id="02213-110">Standardmäßig ist ein Anforderungsdigesttoken 30 Minuten gültig. Vor der Verwendung sollten Sie daher überprüfen, ob es noch gültig ist.</span><span class="sxs-lookup"><span data-stu-id="02213-110">By default, a request digest token is valid for 30 minutes, so before using it, you have to ensure that it's still valid.</span></span> <span data-ttu-id="02213-111">In der Vergangenheit musste dies manuell durch den Vergleich des Zeitstempels aus dem Anforderungsdigest mit der aktuellen Zeit erfolgen.</span><span class="sxs-lookup"><span data-stu-id="02213-111">In the past you had to do this manually, by comparing the timestamp from the request digest with the current time.</span></span> 

<span data-ttu-id="02213-112">SharePoint-Framework vereinfacht diesen Prozess durch zwei Möglichkeiten, mit denen Sie sicherstellen können, dass Ihre Anforderung ein gültiges Anforderungsdigesttoken enthält.</span><span class="sxs-lookup"><span data-stu-id="02213-112">SharePoint Framework simplifies this process by offering you two ways of ensuring that your request has a valid request digest token.</span></span>

## <a name="use-the-sphttpclient-to-communicate-with-the-sharepoint-rest-api"></a><span data-ttu-id="02213-113">Verwenden von SPHttpClient zum Kommunizieren mit der SharePoint-REST-API</span><span class="sxs-lookup"><span data-stu-id="02213-113">Use the SPHttpClient to communicate with the SharePoint REST API</span></span>

<span data-ttu-id="02213-114">Die empfohlene Vorgehensweise für die Kommunikation mit der SharePoint-REST-API besteht in der Verwendung des im Lieferumfang des SharePoint-Frameworks enthaltenen SPHttpClient.</span><span class="sxs-lookup"><span data-stu-id="02213-114">The recommended way to communicate with the SharePoint REST API is to use the SPHttpClient provided with the SharePoint Framework.</span></span> <span data-ttu-id="02213-115">Diese Klasse umfasst die Ausgabe von REST-Anforderungen an die SharePoint-REST-API mit geeigneter Logik, die Ihren Code vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="02213-115">This class wraps issuing REST requests to the SharePoint REST API with convenient logic that simplifies your code.</span></span> 

<span data-ttu-id="02213-116">Wenn Sie z. B. eine Nicht-GET-Anforderung mithilfe eines SPHttpClient ausgeben, erhält dieser automatisch einen gültigen Anforderungsdigest und fügt diesen der Anforderung hinzu.</span><span class="sxs-lookup"><span data-stu-id="02213-116">For example, whenever you issue a non-GET request using the SPHttpClient, it automatically obtains a valid request digest and adds it to the request.</span></span> <span data-ttu-id="02213-117">Dies vereinfacht Ihre Lösung erheblich, da Sie keinen Code programmieren müssen, um Anforderungsdigesttoken zu verwalten und deren Gültigkeit sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="02213-117">This significantly simplifies your solution because you don't need to build code to manage request digest tokens and ensure their validity.</span></span>

<span data-ttu-id="02213-118">Wenn Sie eine neue Anpassungen auf dem SharePoint-Framework erstellen, sollten Sie für die Kommunikation mit der SharePoint-REST-API immer den SPHttpClient verwenden.</span><span class="sxs-lookup"><span data-stu-id="02213-118">If you're building new customizations on the SharePoint Framework, you should always use the SPHttpClient to communicate with the SharePoint REST API.</span></span> 

<span data-ttu-id="02213-119">In manchen Fällen können Sie den SPHttpClient möglicherweise nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="02213-119">Sometimes, however, you might not be able to use the SPHttpClient.</span></span> <span data-ttu-id="02213-120">Dies kann z. B. der Fall sein, wenn Sie eine vorhandene Anpassung auf die SharePoint-Framework migrieren und so viel wie möglich von dem ursprünglichen Code beibehalten möchten oder wenn Sie eine Anpassung mithilfe einer Bibliothek, wie z. B. Angular(JS) erstellen möchten, die über einen eigenen Service für die Ausgabe von Webanfragen verfügt.</span><span class="sxs-lookup"><span data-stu-id="02213-120">If you're building new customizations on the SharePoint Framework, you should always use the SPHttpClient to communicate with the SharePoint REST API. Sometimes however, you might not be able to use the SPHttpClient. This can be the case for example when you're migrating an existing customization to the SharePoint Framework and want to keep as much of the original code as possible, or you're building a customization using a library such as Angular(JS), that has its own services for issuing web requests. In such cases you can obtain a valid request digest token from the DigestCache.</span></span> <span data-ttu-id="02213-121">In solchen Fällen erhalten Sie ein gültiges Anforderungsdigesttoken aus dem **DigestCache**.</span><span class="sxs-lookup"><span data-stu-id="02213-121">In such cases you can obtain a valid request digest token from the **DigestCache**.</span></span>

## <a name="retrieve-a-valid-request-digest-by-using-the-digestcache-service"></a><span data-ttu-id="02213-122">Abrufen eines gültigen Anforderungsdigest mithilfe des DigestCache-Diensts</span><span class="sxs-lookup"><span data-stu-id="02213-122">Retrieve valid request digest using the DigestCache service</span></span>

<span data-ttu-id="02213-123">Wenn Sie den SPHttpClient nicht für die Kommunikation mit der SharePoint-REST-API verwenden können, können Sie ein gültiges Anforderungsdigesttoken erhalten, indem Sie den mit der SharePoint-Framework bereitgestellten **DigestCache**-Dienst verwenden.</span><span class="sxs-lookup"><span data-stu-id="02213-123">If you can't use the SPHttpClient for communicating with the SharePoint REST API, you can obtain a valid request digest token by using the **DigestCache** service provided with the SharePoint Framework.</span></span> 

<span data-ttu-id="02213-124">Der Vorteil der Verwendung des DigestCache-Dienstes gegenüber der manuellen Anforderung eines gültigen Anforderungsdigesttoken ist, dass der DigestCache automatisch überprüft, ob der zuvor abgerufene Anforderungsdigest noch gültig ist.</span><span class="sxs-lookup"><span data-stu-id="02213-124">The benefit of using the DigestCache service over manually obtaining a valid request digest token is that the DigestCache automatically checks if the previously retrieved request digest is still valid.</span></span> <span data-ttu-id="02213-125">Falls er abgelaufen ist, fordert der DigestCache-Dienst automatisch ein neues Anforderungsdigesttoken bei SharePoint an und speichert es für nachfolgende Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="02213-125">If it's expired, the DigestCache service automatically requests a new request digest token from SharePoint and stores it from subsequent requests.</span></span> <span data-ttu-id="02213-126">DigestCache vereinfacht die Programmierung und macht Ihre Lösung robuster.</span><span class="sxs-lookup"><span data-stu-id="02213-126">Using the DigestCache simplifies your code and makes your solution more robust.</span></span>

### <a name="to-use-the-digestcache-service-in-your-code"></a><span data-ttu-id="02213-127">Verwenden des DigestCache-Dienstes im Code</span><span class="sxs-lookup"><span data-stu-id="02213-127">To use the DigestCache service in your code, first import the DigestCache and IDigestCache types from the @microsoft/sp-http package:</span></span>

1. <span data-ttu-id="02213-128">Importieren Sie die Typen **DigestCache** und **IDigestCache** aus dem Paket **@microsoft/sp-http**:</span><span class="sxs-lookup"><span data-stu-id="02213-128">Import the **DigestCache** and **IDigestCache** types from the **@microsoft/sp-http** package:</span></span>

  ```ts
  // ...
  import { IDigestCache, DigestCache } from '@microsoft/sp-http';

  export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
    // ...
  }
  ```

2. <span data-ttu-id="02213-129">Wenn Sie ein gültiges Anforderungsdigesttoken benötigen, rufen Sie einen Verweis auf den DigestCache-Dienst ab und rufen Sie dann seine **fetchDigest**-Methode auf:</span><span class="sxs-lookup"><span data-stu-id="02213-129">Next, whenever you need a valid request digest token, retrieve a reference to the DigestCache service and call its **fetchDigest** method:</span></span>

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