---
title: "Übersicht über SharePoint-Webhooks"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: fa9edc4423c4e6ab7e1f3ff97dab8be10ff6d7f0
ms.sourcegitcommit: 0d04831f6f30e5fbcf38d6509d602628552d0b28
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="overview-of-sharepoint-webhooks"></a><span data-ttu-id="19b0c-102">Übersicht über SharePoint-Webhooks</span><span class="sxs-lookup"><span data-stu-id="19b0c-102">Overview of SharePoint webhooks</span></span>

<span data-ttu-id="19b0c-103">SharePoint-[Webhooks](http://en.wikipedia.org/wiki/Webhook) ermöglichen Entwicklern das Erstellen von Anwendungen, die den Empfang von Benachrichtigungen für bestimmte Ereignisse, die in SharePoint auftreten, abonnieren.</span><span class="sxs-lookup"><span data-stu-id="19b0c-103">SharePoint [webhooks](http://en.wikipedia.org/wiki/Webhook) enable developers to build applications that subscribe to receive notifications on specific events that occur in SharePoint.</span></span> <span data-ttu-id="19b0c-104">Wenn ein Ereignis ausgelöst wird, sendet SharePoint ein HTTP POST-Payload an den Abonnenten.</span><span class="sxs-lookup"><span data-stu-id="19b0c-104">When an event is triggered, SharePoint sends an HTTP POST payload to the subscriber.</span></span> <span data-ttu-id="19b0c-105">Webhooks sind leichter zu entwickeln und zu verwenden als Windows Communication Foundation-Dienste (WCF), die von SharePoint-Add-In-Remote-Ereignisempfängern verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="19b0c-105">Webhooks are easier to develop and consume than Windows Communication Foundation (WCF) services used by SharePoint add-in remote event receivers.</span></span> <span data-ttu-id="19b0c-106">Dies liegt daran, dass Webhooks reguläre HTTP-Dienste sind (Web-API).</span><span class="sxs-lookup"><span data-stu-id="19b0c-106">This is because webhooks are regular HTTP services (web API).</span></span>

<span data-ttu-id="19b0c-107">Webhooks sind derzeit nur für SharePoint-Listenelemente aktiviert.</span><span class="sxs-lookup"><span data-stu-id="19b0c-107">Currently webhooks are only enabled for SharePoint list items.</span></span> <span data-ttu-id="19b0c-108">SharePoint-Listenelement-Webhooks umfassen die Ereignisse, die Listenelementänderungen für eine angegeben SharePoint-Liste oder Dokumentbibliothek entspricht.</span><span class="sxs-lookup"><span data-stu-id="19b0c-108">SharePoint list item webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library.</span></span> <span data-ttu-id="19b0c-109">SharePoint-Webhooks bieten eine einfache Benachrichtigungspipeline, damit Ihre Anwendung Änderungen an einer SharePoint-Liste erkennen kann, ohne den Dienst abzurufen.</span><span class="sxs-lookup"><span data-stu-id="19b0c-109">SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span> <span data-ttu-id="19b0c-110">Weitere Informationen finden Sie unter [SharePoint-Listen-Webhooks](./lists/overview-sharepoint-list-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="19b0c-110">For more information see [SharePoint list webhooks](./lists/overview-sharepoint-list-webhooks.md).</span></span> 

## <a name="creating-webhooks"></a><span data-ttu-id="19b0c-111">Erstellen von Webhooks</span><span class="sxs-lookup"><span data-stu-id="19b0c-111">Creating webhooks</span></span>
<span data-ttu-id="19b0c-112">Um einen neuen SharePoint-Webhook zu erstellen, fügen Sie ein neues Abonnement zur entsprechenden SharePoint-Ressource hinzu, z. B. zu einer SharePoint-Liste.</span><span class="sxs-lookup"><span data-stu-id="19b0c-112">To create a new SharePoint webhook, you add a new subscription to the specific SharePoint resource, such as a SharePoint list.</span></span> 

<span data-ttu-id="19b0c-113">Die folgenden Informationen sind für das Erstellen eines neuen Abonnements erforderlich:</span><span class="sxs-lookup"><span data-stu-id="19b0c-113">The following information is required for creating a new subscription:</span></span>

- <span data-ttu-id="19b0c-p103">Ressource – Die Ressourcenendpunkt-URL, für die Sie das Abonnement erstellen. Zum Beispiel eine SharePoint-Listen-API-URL.</span><span class="sxs-lookup"><span data-stu-id="19b0c-p103">Resource - The resource endpoint URL you are creating the subscription for. For example a SharePoint List API URL.</span></span>
- <span data-ttu-id="19b0c-p104">Serverbenachrichtigungs-URL – Ihre Dienstendpunkt-URL. SharePoint sendet eine HTTP-POST an diesen Endpunkt, wenn Ereignisse in der angegebenen Ressource auftreten.</span><span class="sxs-lookup"><span data-stu-id="19b0c-p104">Server notification URL - Your service endpoint URL. SharePoint will send an HTTP POST to this endpoint when events occur in the specified resource.</span></span>
- <span data-ttu-id="19b0c-p105">Ablaufdatum – das Ablaufdatum für Ihr Abonnement. Das Ablaufdatum darf nicht länger als 6 Monate sein. Standardmäßig wird der Ablauf von Abonnements auf 6 Monate nach dem Erstellungsdatum festgelegt.</span><span class="sxs-lookup"><span data-stu-id="19b0c-p105">Expiration date - The expiration date for your subscription. The expiration date should not be more than 6 months. By default, subscriptions are set to expire 6 months from when they are created.</span></span> 

<span data-ttu-id="19b0c-121">Die folgenden zusätzlichen Informationen können Sie ebenfalls einschließen:</span><span class="sxs-lookup"><span data-stu-id="19b0c-121">You can also include the following additional information if needed:</span></span>

- <span data-ttu-id="19b0c-p106">Clientzustand – eine verschlüsselte Zeichenfolge, die zurück an den Client bei allen Benachrichtigungen übergeben wird. Dies können Sie zum Überprüfen von Benachrichtigungen, zum Kategorisieren unterschiedlicher Abonnements oder aus anderen Gründen verwenden.</span><span class="sxs-lookup"><span data-stu-id="19b0c-p106">Client State - An opaque string passed back to the client on all notifications. You can use this for validating notifications, tagging different subscriptions, or other reasons.</span></span>

## <a name="handling-webhook-validation-requests"></a><span data-ttu-id="19b0c-124">Behandeln von Webhook-Überprüfungsanfragen</span><span class="sxs-lookup"><span data-stu-id="19b0c-124">Handling webhook validation requests</span></span>

<span data-ttu-id="19b0c-p107">Wenn ein neues Abonnement erstellt wird, überprüft SharePoint, ob die URL für die Benachrichtigung den Empfang von Webhook-Benachrichtigungen unterstützt. Diese Überprüfung erfolgt während der Anforderung zum Erstellen des Abonnements. Das Abonnement wird nur erstellt, wenn der Dienst in einer bestimmten Frist mit dem Überprüfungstoken antwortet.</span><span class="sxs-lookup"><span data-stu-id="19b0c-p107">When a new subscription is created, SharePoint will validate whether the notification URL supports receiving webhook notifications. This validation is performed during the subscription creation request. The subscription will only be created if your service responds in a timely manner back with the validation token.</span></span>

### <a name="example-validation-request"></a><span data-ttu-id="19b0c-128">Beispiel für Überprüfungsanforderung</span><span class="sxs-lookup"><span data-stu-id="19b0c-128">Example validation request</span></span>

<span data-ttu-id="19b0c-129">Wenn ein neues Abonnement erstellt wird, sendet SharePoint eine HTTP POST-Anforderung an die eingetragene URL in einem Format ähnlich dem folgenden Beispiel:</span><span class="sxs-lookup"><span data-stu-id="19b0c-129">When a new subscription is created, SharePoint will send an HTTP POST request to the registered URL in a format similar to the following example:</span></span>


```http
POST https://contoso.azurewebsites.net/your/webhook/service?validationToken={randomString}
Content-Length: 0
```

### <a name="response"></a><span data-ttu-id="19b0c-130">Antwort</span><span class="sxs-lookup"><span data-stu-id="19b0c-130">Response</span></span>

<span data-ttu-id="19b0c-131">Damit das Abonnement erfolgreich erstellt wird, muss Ihr Dienst der Anforderung durch Zurückgeben des **ValidationToken**-Abfragezeichenfolgenparameters als Nur-Text-Antwort antworten.</span><span class="sxs-lookup"><span data-stu-id="19b0c-131">For the subscription to be created successfully, your service must respond to the request by returning the value of the **validationToken** query string parameter as a plain-text response.</span></span>

```http
HTTP/1.1 200 OK
Content-Type: text/plain

{randomString}
```

<span data-ttu-id="19b0c-132">Wenn Ihre Anwendung einen anderen Statuscode als `200` zurückgibt oder nicht mit dem Wert des **ValidationToken**-Parameters antwortet, schlägt die Anforderung zum Erstellen eines neuen Abonnements fehl.</span><span class="sxs-lookup"><span data-stu-id="19b0c-132">If your application returns a status code other than `200` or fails to respond with the value of the **validationToken** parameter, the request to create a new subscription will fail.</span></span>

## <a name="receiving-notifications"></a><span data-ttu-id="19b0c-133">Empfangen von Benachrichtigungen</span><span class="sxs-lookup"><span data-stu-id="19b0c-133">Receiving notifications</span></span>
<span data-ttu-id="19b0c-p108">Die Benachrichtigungsnutzlast informiert die Anwendung darüber, dass in einer bestimmten Ressource für ein bestimmtes Abonnement ein Ereignis aufgetreten ist. Mehrere Benachrichtigungen an Ihre Anwendung können in eine einzige Anforderung zusammengefasst werden, wenn mehrere Änderungen in der Ressource innerhalb des gleichen Zeitraums aufgetreten sind.</span><span class="sxs-lookup"><span data-stu-id="19b0c-p108">The notification payload will inform your application that an event occurred in a given resource for a given subscription. Multiple notifications to your application may be batched together into a single request, if multiple changes occurred in the resource within the same time period.</span></span>

<span data-ttu-id="19b0c-136">Die Benachrichtigungsnutzlast enthält im Textteil außerdem den Clientzustand, sofern Sie ihn beim Erstellen des Abonnements verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="19b0c-136">The notification payload body will also contain your client state if you used it when creating the subscription.</span></span>

### <a name="webhook-notification-resource"></a><span data-ttu-id="19b0c-137">Webhook-Benachrichtigungsressource</span><span class="sxs-lookup"><span data-stu-id="19b0c-137">Webhook notification resource</span></span>

<span data-ttu-id="19b0c-138">Die Benachrichtigungsressource definiert die Form der Daten, die Ihrem Dienst bereitgestellt werden, wenn eine SharePoint-Webhook-Benachrichtigungsanforderung an die registrierte Benachrichtigungs-URL gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="19b0c-138">The notification resource defines the shape of the data provided to your service when a SharePoint webhook notification request is submitted to your registered notification URL.</span></span>

#### <a name="json-representation"></a><span data-ttu-id="19b0c-139">JSON-Darstellung</span><span class="sxs-lookup"><span data-stu-id="19b0c-139">JSON representation</span></span>

<span data-ttu-id="19b0c-140">Jede vom Dienst generierte Benachrichtigung wird in eine**WebhookNotification**-Instanz serialisiert:</span><span class="sxs-lookup"><span data-stu-id="19b0c-140">Each notification generated by the service is serialized into a **webhookNotifiation** instance:</span></span>

```json
{
    "subscriptionId":"91779246-afe9-4525-b122-6c199ae89211",
    "clientState":"00000000-0000-0000-0000-000000000000",
    "expirationDateTime":"2016-04-30T17:27:00.0000000Z",
    "resource":"b9f6f714-9df8-470b-b22e-653855e1c181",
    "tenantId":"00000000-0000-0000-0000-000000000000",
    "siteUrl":"/",
    "webId":"dbc5a806-e4d4-46e5-951c-6344d70b62fa"
}
```

<span data-ttu-id="19b0c-141">Da in einer einzigen Anforderung mehrere Benachrichtigungen an den Dienst gesendet werden können, werden diese in einem Objekt mit einem einzigen Array-**Wert** zusammengefasst:</span><span class="sxs-lookup"><span data-stu-id="19b0c-141">Since multiple notifications may be submitted to your service in a single request, these are combined together in an object with a single array **value**:</span></span>

```json
{
   "value":[
      {
         "subscriptionId":"91779246-afe9-4525-b122-6c199ae89211",
         "clientState":"00000000-0000-0000-0000-000000000000",
         "expirationDateTime":"2016-04-30T17:27:00.0000000Z",
         "resource":"b9f6f714-9df8-470b-b22e-653855e1c181",
         "tenantId":"00000000-0000-0000-0000-000000000000",
         "siteUrl":"/",
         "webId":"dbc5a806-e4d4-46e5-951c-6344d70b62fa"
      }
   ]
}
```

#### <a name="properties"></a><span data-ttu-id="19b0c-142">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="19b0c-142">Properties</span></span>

| <span data-ttu-id="19b0c-143">Eigenschaftenname</span><span class="sxs-lookup"><span data-stu-id="19b0c-143">Property Name</span></span>          | <span data-ttu-id="19b0c-144">Typ</span><span class="sxs-lookup"><span data-stu-id="19b0c-144">Type</span></span>              | <span data-ttu-id="19b0c-145">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="19b0c-145">description</span></span>                                                                                                                         |
|:-----------------------|:------------------|:------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="19b0c-146">**resource**</span><span class="sxs-lookup"><span data-stu-id="19b0c-146">**resource**</span></span>           | <span data-ttu-id="19b0c-147">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="19b0c-147">String</span></span>            | <span data-ttu-id="19b0c-148">Eindeutige ID der Liste, in der das Abonnement registriert ist.</span><span class="sxs-lookup"><span data-stu-id="19b0c-148">Unique identifier of the list where the subscription is registered.</span></span>                                                                 |
| <span data-ttu-id="19b0c-149">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="19b0c-149">**subscriptionId**</span></span>     | <span data-ttu-id="19b0c-150">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="19b0c-150">String</span></span>            | <span data-ttu-id="19b0c-151">Die eindeutige ID für die Abonnementressource.</span><span class="sxs-lookup"><span data-stu-id="19b0c-151">The unique identifier for the subscription resource</span></span>                                                                                 |
| <span data-ttu-id="19b0c-152">**clientState**</span><span class="sxs-lookup"><span data-stu-id="19b0c-152">**clientState**</span></span>        | <span data-ttu-id="19b0c-153">Zeichenfolge – optional</span><span class="sxs-lookup"><span data-stu-id="19b0c-153">String - optional</span></span> | <span data-ttu-id="19b0c-154">Ein optionaler Zeichenfolgenwert, der in der Benachrichtigungsmitteilung für Ihr Abonnement zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="19b0c-154">An optional string value that is passed back in the notification message for this subscription.</span></span>                                     |
| <span data-ttu-id="19b0c-155">**expirationDateTime**</span><span class="sxs-lookup"><span data-stu-id="19b0c-155">**expirationDateTime**</span></span> | <span data-ttu-id="19b0c-156">DateTime</span><span class="sxs-lookup"><span data-stu-id="19b0c-156">DateTime</span></span>          | <span data-ttu-id="19b0c-157">Datum und Uhrzeit des Ablaufs des Abonnements, wenn dies nicht aktualisiert oder erneuert wird.</span><span class="sxs-lookup"><span data-stu-id="19b0c-157">The date and time when the subscription will expire if not updated or renewed.</span></span>                                                      |
| <span data-ttu-id="19b0c-158">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="19b0c-158">**tenantId**</span></span>           | <span data-ttu-id="19b0c-159">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="19b0c-159">String</span></span>            | <span data-ttu-id="19b0c-160">Eindeutige ID für den Mandanten, der diese Benachrichtigung generiert hat.</span><span class="sxs-lookup"><span data-stu-id="19b0c-160">Unique identifier for the tenant which generated this notification.</span></span>                                                                 |
| <span data-ttu-id="19b0c-161">**siteUrl**</span><span class="sxs-lookup"><span data-stu-id="19b0c-161">**siteUrl**</span></span>            | <span data-ttu-id="19b0c-162">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="19b0c-162">String</span></span>            | <span data-ttu-id="19b0c-163">Server-relative URL der Website, auf der das Abonnement registriert wurde.</span><span class="sxs-lookup"><span data-stu-id="19b0c-163">Server relative URL of the site where the subscription is registered.</span></span>                                                               |
| <span data-ttu-id="19b0c-164">**webId**</span><span class="sxs-lookup"><span data-stu-id="19b0c-164">**webId**</span></span>              | <span data-ttu-id="19b0c-165">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="19b0c-165">String</span></span>            | <span data-ttu-id="19b0c-166">Eindeutige ID des Webs, in dem das Abonnement registriert wurde.</span><span class="sxs-lookup"><span data-stu-id="19b0c-166">Unique identifier of the web where the subscription is registered.</span></span>                                                                  |

#### <a name="example-notification"></a><span data-ttu-id="19b0c-167">Beispielbenachrichtigung</span><span class="sxs-lookup"><span data-stu-id="19b0c-167">Example notification</span></span>
<span data-ttu-id="19b0c-p109">Der Hauptteil der HTTP-Anforderung an die Dienstbenachrichtigungs-URL enthält eine Webhook-Benachrichtigung. Das folgende Beispiel zeigt eine Nutzlast mit einer Benachrichtigung:</span><span class="sxs-lookup"><span data-stu-id="19b0c-p109">The body of the HTTP request to your service notification URL will contain a webhook notification. The following example shows a payload with one notification:</span></span>

```json
{
   "value":[
      {
         "subscriptionId":"91779246-afe9-4525-b122-6c199ae89211",
         "clientState":"00000000-0000-0000-0000-000000000000",
         "expirationDateTime":"2016-04-30T17:27:00.0000000Z",
         "resource":"b9f6f714-9df8-470b-b22e-653855e1c181",
         "tenantId":"00000000-0000-0000-0000-000000000000",
         "siteUrl":"/",
         "webId":"dbc5a806-e4d4-46e5-951c-6344d70b62fa"
      }
   ]
}
```

<span data-ttu-id="19b0c-170">Die Benachrichtigung umfasst keine Informationen zu den Änderungen, durch die sie ausgelöst wurde.</span><span class="sxs-lookup"><span data-stu-id="19b0c-170">The notification doesn't include any information about the changes that triggered it.</span></span> <span data-ttu-id="19b0c-171">Ihre Anwendung verwendet die [GetChanges-API](https://msdn.microsoft.com/de-DE/library/office/dn531433.aspx#bk_ListGetChanges) in der Liste, um die Sammlung von Änderungen aus dem Änderungsprotokoll abzufragen und den Änderungstokenwert für alle nachfolgenden Aufrufe zu speichern, wenn die Anwendung benachrichtigt wird.</span><span class="sxs-lookup"><span data-stu-id="19b0c-171">Your application is expected to use the [GetChanges API](https://msdn.microsoft.com/de-DE/library/office/dn531433.aspx#bk_ListGetChanges) on the list to query the collection of changes from the change log and store the change token value for any subsequent calls when the application is notified.</span></span>

## <a name="event-types"></a><span data-ttu-id="19b0c-172">Ereignistypen</span><span class="sxs-lookup"><span data-stu-id="19b0c-172">Event types</span></span>
<span data-ttu-id="19b0c-173">SharePoint-Webhooks unterstützen nur asynchrone Ereignisse.</span><span class="sxs-lookup"><span data-stu-id="19b0c-173">SharePoint webhooks only support asynchronous events.</span></span> <span data-ttu-id="19b0c-174">Das bedeutet, dass Webhooks nur nach einer Änderung ausgelöst werden (ähnlich wie **-ed**-Ereignisse). Somit sind synchrone Ereignisse (**-ing**-Ereignisse) nicht möglich.</span><span class="sxs-lookup"><span data-stu-id="19b0c-174">This means that webhooks are only fired after a change happened (similar to **-ed** events), and thus synchronous (**-ing** events) are not possible.</span></span>

## <a name="error-handling"></a><span data-ttu-id="19b0c-175">Fehlerbehandlung</span><span class="sxs-lookup"><span data-stu-id="19b0c-175">Error handling</span></span>
<span data-ttu-id="19b0c-176">Wenn beim Senden der Benachrichtigung an Ihre Anwendung ein Fehler auftritt, versucht SharePoint bis zu 5 Mal, die Benachrichtigung zuzustellen.</span><span class="sxs-lookup"><span data-stu-id="19b0c-176">If an error occurs while sending the notification to your application, SharePoint will retry up to 5 times to deliver the notification.</span></span> <span data-ttu-id="19b0c-177">Jede Antwort, die einen HTTP-Statuscode außerhalb des Bereichs 200-299 aufweist oder die abläuft, wird in 5 Minuten erneut versucht.</span><span class="sxs-lookup"><span data-stu-id="19b0c-177">Any response with an HTTP status code outside of the 200-299 range, or that times out, will be attempted again 5 minute later.</span></span> <span data-ttu-id="19b0c-178">Wenn die Anforderung nach 5 Versuchen nicht erfolgreich ist, wird die Benachrichtigung gelöscht.</span><span class="sxs-lookup"><span data-stu-id="19b0c-178">If the request is not successful after 5 attempts, the notification is dropped.</span></span> <span data-ttu-id="19b0c-179">Weitere Benachrichtigungen an Ihre Anwendung werden weiterhin ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="19b0c-179">Future notifications will still be attempted to your application.</span></span>

## <a name="expiration"></a><span data-ttu-id="19b0c-180">Ablauf</span><span class="sxs-lookup"><span data-stu-id="19b0c-180">Expiration</span></span>
<span data-ttu-id="19b0c-181">Webhook-Abonnements laufen standardmäßig nach 6 Monaten ab, wenn kein **ExpirationDateTime**-Wert angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="19b0c-181">Webhook subscriptions are set to expire after 6 months by default if an **expirationDateTime** value is not specified.</span></span> 

<span data-ttu-id="19b0c-p113">Sie müssen beim Erstellen des Abonnements ein Ablaufdatum festlegen. Das Ablaufdatum sollte nicht länger als 6 Monate sein. Die Anwendung sollte das Ablaufdatum entsprechend den Anforderungen Ihrer Anwendung behandeln, indem das Abonnement regelmäßig aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="19b0c-p113">You need to set an expiration date when creating the subscription. The expiration date should be less than 6 months. Your application is expected to handle the expiration date according to your application's needs by updating the subscription periodically.</span></span> 

## <a name="retry-mechanism"></a><span data-ttu-id="19b0c-185">Wiederholungsmechanismus</span><span class="sxs-lookup"><span data-stu-id="19b0c-185">Retry mechanism</span></span>

<span data-ttu-id="19b0c-186">Wenn ein Ereignis in SharePoint auftritt und Ihr Dienstendpunkt nicht erreichbar ist (z. B. aufgrund von Wartungen), wiederholt SharePoint das Senden der Benachrichtigung.</span><span class="sxs-lookup"><span data-stu-id="19b0c-186">If an event occurs in SharePoint and your service endpoint is not reachable (e.g., due to maintenance) SharePoint will retry sending the notification.</span></span> <span data-ttu-id="19b0c-187">SharePoint führt **5 Wiederholungen mit 5 Minuten Wartezeit** zwischen den Versuchen durch.</span><span class="sxs-lookup"><span data-stu-id="19b0c-187">SharePoint performs a retry of **5 times with a 5 minute wait time** between the attempts.</span></span> <span data-ttu-id="19b0c-188">Wenn aus irgendeinem Grund Ihr Dienst länger ausfällt, stellt der Aufruf an `GetChanges()` beim nächsten Aufruf durch SharePoint die Änderungen, die verpasst wurden, als der Dienst nicht verfügbar war, wieder her.</span><span class="sxs-lookup"><span data-stu-id="19b0c-188">If for some reason your service is down for a longer time, the next time when it's up and gets called by SharePoint, the call to the `GetChanges()` will recover the changes that were missed when your service was not available.</span></span>
