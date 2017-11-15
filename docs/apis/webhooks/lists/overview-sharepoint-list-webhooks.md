---
title: SharePoint-Listen-Webhooks
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 81657f3bcaf45eeea4e0999d3c6eb6dfad0407b1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
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

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Übersicht über SharePoint-Webhooks](../overview-sharepoint-webhooks.md)
