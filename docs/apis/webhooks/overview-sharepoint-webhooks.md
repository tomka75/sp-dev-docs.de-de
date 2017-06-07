# <a name="overview-of-sharepoint-webhooks"></a>Übersicht über SharePoint-Webhooks

SharePoint-[Webhooks](http://en.wikipedia.org/wiki/Webhook) ermöglichen Entwicklern das Erstellen von Anwendungen, die den Empfang von Benachrichtigungen für bestimmte Ereignisse, die in SharePoint auftreten, abonnieren. Wenn ein Ereignis ausgelöst wird, sendet SharePoint ein HTTP POST-Payload an den Abonnenten. Webhooks sind leichter zu entwickeln und zu verwenden als Windows Communication Foundation-Dienste (WCF), die von SharePoint-Add-In-Remote-Ereignisempfängern verwendet werden. Dies liegt daran, dass Webhooks reguläre HTTP-Dienste sind (Web-API).

Webhooks sind derzeit nur für SharePoint-Listenelemente aktiviert. SharePoint-Listenelement-Webhooks umfassen die Ereignisse, die Listenelementänderungen für eine angegeben SharePoint-Liste oder Dokumentbibliothek entspricht. SharePoint-Webhooks bieten eine einfache Benachrichtigungspipeline, damit Ihre Anwendung Änderungen an einer SharePoint-Liste erkennen kann, ohne den Dienst abzurufen. Weitere Informationen finden Sie unter [SharePoint-Listen-Webhooks](./lists/overview-sharepoint-list-webhooks): 

## <a name="creating-webhooks"></a>Erstellen von Webhooks
Um einen neuen SharePoint-Webhook zu erstellen, fügen Sie ein neues Abonnement zur entsprechenden SharePoint-Ressource hinzu, z. B. zu einer SharePoint-Liste. 

Die folgenden Informationen sind für das Erstellen eines neuen Abonnements erforderlich:

- Ressource – Die Ressourcenendpunkt-URL, für die Sie das Abonnement erstellen. Zum Beispiel eine SharePoint-Listen-API-URL.
- Serverbenachrichtigungs-URL – Ihre Dienstendpunkt-URL. SharePoint sendet eine HTTP-POST an diesen Endpunkt, wenn Ereignisse in der angegebenen Ressource auftreten.
- Ablaufdatum – das Ablaufdatum für Ihr Abonnement. Das Ablaufdatum darf nicht länger als 6 Monate sein. Standardmäßig wird der Ablauf von Abonnements auf 6 Monate nach dem Erstellungsdatum festgelegt. 

Die folgenden zusätzlichen Informationen können Sie ebenfalls einschließen:

- Clientzustand – eine verschlüsselte Zeichenfolge, die zurück an den Client bei allen Benachrichtigungen übergeben wird. Dies können Sie zum Überprüfen von Benachrichtigungen, zum Kategorisieren unterschiedlicher Abonnements oder aus anderen Gründen verwenden.

## <a name="handling-webhook-validation-requests"></a>Behandeln von Webhook-Überprüfungsanfragen

Wenn ein neues Abonnement erstellt wird, überprüft SharePoint, ob die URL für die Benachrichtigung den Empfang von Webhook-Benachrichtigungen unterstützt. Diese Überprüfung erfolgt während der Anforderung zum Erstellen des Abonnements. Das Abonnement wird nur erstellt, wenn der Dienst in einer bestimmten Frist mit dem Überprüfungstoken antwortet.

### <a name="example-validation-request"></a>Beispiel für Überprüfungsanforderung

Wenn ein neues Abonnement erstellt wird, sendet SharePoint eine HTTP POST-Anforderung an die eingetragene URL in einem Format ähnlich dem folgenden Beispiel:


```http
POST https://contoso.azurewebsites.net/your/webhook/service?validationToken={randomString}
Content-Length: 0
```

### <a name="response"></a>Antwort

Damit das Abonnement erfolgreich erstellt wird, muss Ihr Dienst der Anforderung durch Zurückgeben des **ValidationToken**-Abfragezeichenfolgenparameters als Nur-Text-Antwort antworten.

```http
HTTP/1.1 200 OK
Content-Type: text/plain

{randomString}
```

Wenn Ihre Anwendung einen anderen Statuscode als `200` zurückgibt oder nicht mit dem Wert des **ValidationToken**-Parameters antwortet, schlägt die Anforderung zum Erstellen eines neuen Abonnements fehl.

## <a name="receiving-notifications"></a>Empfangen von Benachrichtigungen
Die Benachrichtigungsnutzlast informiert die Anwendung darüber, dass in einer bestimmten Ressource für ein bestimmtes Abonnement ein Ereignis aufgetreten ist. Mehrere Benachrichtigungen an Ihre Anwendung können in eine einzige Anforderung zusammengefasst werden, wenn mehrere Änderungen in der Ressource innerhalb des gleichen Zeitraums aufgetreten sind.

Die Benachrichtigungsnutzlast enthält im Textteil außerdem den Clientzustand, sofern Sie ihn beim Erstellen des Abonnements verwendet haben.

### <a name="webhook-notification-resource"></a>Webhook-Benachrichtigungsressource

Die Benachrichtigungsressource definiert die Form der Daten, die Ihrem Dienst bereitgestellt werden, wenn eine SharePoint-Webhook-Benachrichtigungsanforderung an die registrierte Benachrichtigungs-URL gesendet wird.

#### <a name="json-representation"></a>JSON-Darstellung

Jede vom Dienst generierte Benachrichtigung wird in eine**WebhookNotification**-Instanz serialisiert:

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

Da in einer einzigen Anforderung mehrere Benachrichtigungen an den Dienst gesendet werden können, werden diese in einem Objekt mit einem einzigen Array-**Wert** zusammengefasst:

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

#### <a name="properties"></a>Eigenschaften

| Eigenschaftenname          | Typ              | Beschreibung                                                                                                                         |
|:-----------------------|:------------------|:------------------------------------------------------------------------------------------------------------------------------------|
| **resource**           | Zeichenfolge            | Eindeutige ID der Liste, in der das Abonnement registriert ist.                                                                 |
| **subscriptionId**     | Zeichenfolge            | Die eindeutige ID für die Abonnementressource.                                                                                 |
| **clientState**        | Zeichenfolge – optional | Ein optionaler Zeichenfolgenwert, der in der Benachrichtigungsmitteilung für Ihr Abonnement zurückgegeben wird.                                     |
| **expirationDateTime** | DateTime          | Datum und Uhrzeit des Ablaufs des Abonnements, wenn dies nicht aktualisiert oder erneuert wird.                                                      |
| **tenantId**           | Zeichenfolge            | Eindeutige ID für den Mandanten, der diese Benachrichtigung generiert hat.                                                                 |
| **siteUrl**            | Zeichenfolge            | Server-relative URL der Website, auf der das Abonnement registriert wurde.                                                               |
| **webId**              | Zeichenfolge            | Eindeutige ID des Webs, in dem das Abonnement registriert wurde.                                                                  |

#### <a name="example-notification"></a>Beispielbenachrichtigung
Der Hauptteil der HTTP-Anforderung an die Dienstbenachrichtigungs-URL enthält eine Webhook-Benachrichtigung. Das folgende Beispiel zeigt eine Nutzlast mit einer Benachrichtigung:

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

Die Benachrichtigung umfasst keine Informationen zu den Änderungen, durch die sie ausgelöst wurde. Ihre Anwendung verwendet die [GetChanges-API](https://msdn.microsoft.com/EN-US/library/office/dn531433.aspx#bk_ListGetChanges) in der Liste, um die Sammlung von Änderungen aus dem Änderungsprotokoll abzufragen und den Änderungstokenwert für alle nachfolgenden Aufrufe zu speichern, wenn die Anwendung benachrichtigt wird.

## <a name="event-types"></a>Ereignistypen
SharePoint-Webhooks unterstützen nur asynchrone Ereignisse. Das bedeutet, dass Webhooks nur nach einer Änderung ausgelöst werden (ähnlich wie **-ed**-Ereignisse). Somit sind synchrone Ereignisse (**-ing**-Ereignisse) nicht möglich.

## <a name="error-handling"></a>Fehlerbehandlung
Wenn beim Senden der Benachrichtigung an Ihre Anwendung ein Fehler auftritt, folgt SharePoint der exponentiellen Back-off-Logik. Jede Antwort, die einen HTTP-Statuscode außerhalb des Bereichs 200-299 aufweist oder abläuft, wird in den nächsten Minuten wiederholt. Wenn die Anforderung nach 15 Minuten nicht erfolgreich ist, wird die Benachrichtigung gelöscht.

Zukünftige Benachrichtigungen werden immer noch an Ihrer Anwendung gesendet, obwohl der Dienst möglicherweise das Abonnement entfernt, wenn eine ausreichende Anzahl fehlgeschlagener Versuche erkannt wird.

## <a name="expiration"></a>Ablauf
Webhook-Abonnements laufen standardmäßig nach 6 Monaten ab, wenn kein **ExpirationDateTime**-Wert angegeben wird. 

Sie müssen beim Erstellen des Abonnements ein Ablaufdatum festlegen. Das Ablaufdatum sollte nicht länger als 6 Monate sein. Die Anwendung sollte das Ablaufdatum entsprechend den Anforderungen Ihrer Anwendung behandeln, indem das Abonnement regelmäßig aktualisiert wird. 

## <a name="retry-mechanism"></a>Wiederholungsmechanismus

Wenn ein Ereignis in SharePoint auftritt und Ihr Dienstendpunkt nicht erreichbar ist (z. B. aufgrund von Wartungen), wiederholt SharePoint das Senden der Benachrichtigung. SharePoint führt **5 Wiederholungen mit 5 Minuten Wartezeit** zwischen den Versuchen durch. Wenn aus irgendeinem Grund Ihr Dienst länger ausfällt, stellt der Aufruf an `GetChanges()` beim nächsten Aufruf durch SharePoint die Änderungen, die verpasst wurden, als der Dienst nicht verfügbar war, wieder her.