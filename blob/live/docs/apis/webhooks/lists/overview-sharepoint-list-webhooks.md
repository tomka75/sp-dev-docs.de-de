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
# <a name="sharepoint-list-webhooks"></a><span data-ttu-id="afa43-102">SharePoint-Listen-Webhooks</span><span class="sxs-lookup"><span data-stu-id="afa43-102">SharePoint list webhooks</span></span>

<span data-ttu-id="afa43-p101">SharePoint-Listen-Webhooks umfassen die Ereignisse, die Listenelementänderungen für eine angegeben SharePoint-Liste oder Dokumentbibliothek entspricht. SharePoint-Webhooks bieten eine einfache Benachrichtigungspipeline, damit Ihre Anwendung Änderungen an einer SharePoint-Liste erkennen kann, ohne den Dienst abzurufen.</span><span class="sxs-lookup"><span data-stu-id="afa43-p101">The SharePoint list webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library. SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span>

## <a name="tasks"></a><span data-ttu-id="afa43-105">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="afa43-105">Tasks</span></span>
| <span data-ttu-id="afa43-106">Aufgabe</span><span class="sxs-lookup"><span data-stu-id="afa43-106">Task</span></span>                                                | <span data-ttu-id="afa43-107">HTTP-Methode</span><span class="sxs-lookup"><span data-stu-id="afa43-107">HTTP method</span></span>                                                  |
|-----------------------------------------------------|--------------------------------------------------------------|
| [<span data-ttu-id="afa43-108">Erstellen eines neuen Abonnements</span><span class="sxs-lookup"><span data-stu-id="afa43-108">Create a new subscription</span></span>](./create-subscription.md) | `POST    /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="afa43-109">Abrufen von Abonnements</span><span class="sxs-lookup"><span data-stu-id="afa43-109">Get subscriptions</span></span>](./get-subscription.md)          | `GET     /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="afa43-110">Löschen eines Abonnements</span><span class="sxs-lookup"><span data-stu-id="afa43-110">Delete a subscription.</span></span>](./delete-subscription.md)       | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`   |
| [<span data-ttu-id="afa43-111">Aktualisieren eines Abonnements</span><span class="sxs-lookup"><span data-stu-id="afa43-111">Update a subscription</span></span>](./update-subscription.md)     | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`   |

## <a name="list-event-types"></a><span data-ttu-id="afa43-112">Listenereignistypen</span><span class="sxs-lookup"><span data-stu-id="afa43-112">List event types</span></span>
<span data-ttu-id="afa43-113">Benachrichtigungen werden an Ihre Anwendung für die folgenden asynchronen Listenelementereignisse in SharePoint gesendet:</span><span class="sxs-lookup"><span data-stu-id="afa43-113">Notifications will be sent to your application for the following asynchronous list item events in SharePoint:</span></span>

* <span data-ttu-id="afa43-114">ItemAdded</span><span class="sxs-lookup"><span data-stu-id="afa43-114">ItemAdded</span></span>
* <span data-ttu-id="afa43-115">ItemUpdated</span><span class="sxs-lookup"><span data-stu-id="afa43-115">ItemUpdated</span></span>
* <span data-ttu-id="afa43-116">ItemDeleted</span><span class="sxs-lookup"><span data-stu-id="afa43-116">ItemDeleted</span></span>
* <span data-ttu-id="afa43-117">ItemCheckedOut</span><span class="sxs-lookup"><span data-stu-id="afa43-117">ItemCheckedOut</span></span>
* <span data-ttu-id="afa43-118">ItemCheckedIn</span><span class="sxs-lookup"><span data-stu-id="afa43-118">ItemCheckedIn</span></span>
* <span data-ttu-id="afa43-119">ItemUncheckedOut</span><span class="sxs-lookup"><span data-stu-id="afa43-119">ItemUncheckedOut</span></span>
* <span data-ttu-id="afa43-120">ItemAttachmentAdded</span><span class="sxs-lookup"><span data-stu-id="afa43-120">ItemAttachmentAdded</span></span>
* <span data-ttu-id="afa43-121">ItemAttachmentDeleted</span><span class="sxs-lookup"><span data-stu-id="afa43-121">ItemAttachmentDeleted</span></span>
* <span data-ttu-id="afa43-122">ItemFileMoved</span><span class="sxs-lookup"><span data-stu-id="afa43-122">ItemFileMoved</span></span>
* <span data-ttu-id="afa43-123">ItemVersionDeleted</span><span class="sxs-lookup"><span data-stu-id="afa43-123">ItemVersionDeleted</span></span>
* <span data-ttu-id="afa43-124">ItemFileConverted</span><span class="sxs-lookup"><span data-stu-id="afa43-124">ItemFileConverted</span></span>

<span data-ttu-id="afa43-125">Synchrone Ereignisse werden in Webhooks nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="afa43-125">Synchronous events are not supported in webhooks.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="afa43-126">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="afa43-126">Additional resources</span></span>

* [<span data-ttu-id="afa43-127">Übersicht über SharePoint-Webhooks</span><span class="sxs-lookup"><span data-stu-id="afa43-127">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks.md)
