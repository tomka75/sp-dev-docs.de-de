# <a name="sharepoint-list-webhooks"></a>SharePoint-Listen-Webhooks

SharePoint-Listen-Webhooks umfassen die Ereignisse, die Listenelementänderungen für eine angegeben SharePoint-Liste oder Dokumentbibliothek entspricht. SharePoint-Webhooks bieten eine einfache Benachrichtigungspipeline, damit Ihre Anwendung Änderungen an einer SharePoint-Liste erkennen kann, ohne den Dienst abzurufen.

## <a name="tasks"></a>Aufgaben
| Aufgabe                                                | HTTP-Methode                                                  |
|-----------------------------------------------------|--------------------------------------------------------------|
| [Erstellen eines neuen Abonnements](./create-subscription) | `POST    /_api/web/lists('list-guid')/subscriptions`         |
| [Abrufen von Abonnements](./get-subscription)          | `GET     /_api/web/lists('list-guid')/subscriptions`         |
| [Löschen eines Abonnements](./delete-subscription)       | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`   |
| [Aktualisieren eines Abonnements](./update-subscription)     | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`   |

## <a name="list-event-types"></a>Listenereignistypen
Benachrichtigungen werden an Ihre Anwendung für die folgenden asynchronen Listenelementereignisse in SharePoint gesendet:

* ItemAdded
* ItemUpdated
* ItemDeleted
* ItemCheckedOut
* ItemCheckedIn
* ItemUncheckedOut
* ItemAttachmentAdded
* ItemAttachmentDeleted
* ItemFileMoved
* ItemVersionDeleted
* ItemFileConverted

Synchrone Ereignisse werden in Webhooks nicht unterstützt.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Übersicht über SharePoint-Webhooks](../overview-sharepoint-webhooks)
