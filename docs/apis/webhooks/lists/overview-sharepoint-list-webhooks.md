---
title: SharePoint-Listen-Webhooks
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 2b3543885de7fcce75694d368667f17dd690592f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-list-webhooks"></a>SharePoint-Listen-Webhooks

SharePoint-Listen-Webhooks umfassen die Ereignisse, die Listenelementänderungen für eine angegeben SharePoint-Liste oder Dokumentbibliothek entspricht. SharePoint-Webhooks bieten eine einfache Benachrichtigungspipeline, damit Ihre Anwendung Änderungen an einer SharePoint-Liste erkennen kann, ohne den Dienst abzurufen.

## <a name="tasks"></a>Aufgaben
| Aufgabe                                                | HTTP-Methode                                                  |
|-----------------------------------------------------|--------------------------------------------------------------|
| [Erstellen eines neuen Abonnements](./create-subscription.md) | `POST    /_api/web/lists('list-guid')/subscriptions`         |
| [Abrufen von Abonnements](./get-subscription.md)          | `GET     /_api/web/lists('list-guid')/subscriptions`         |
| [Löschen eines Abonnements](./delete-subscription.md)       | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`   |
| [Aktualisieren eines Abonnements](./update-subscription.md)     | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`   |

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

## <a name="see-also"></a>Siehe auch

* [Übersicht über SharePoint-Webhooks](../overview-sharepoint-webhooks.md)
