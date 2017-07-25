<span data-ttu-id="c6102-p101">SharePoint-Listen-Webhooks umfassen die Ereignisse, die Listenelementänderungen für eine angegeben SharePoint-Liste oder Dokumentbibliothek entspricht. SharePoint-Webhooks bieten eine einfache Benachrichtigungspipeline, damit Ihre Anwendung Änderungen an einer SharePoint-Liste erkennen kann, ohne den Dienst abzurufen.</span><span class="sxs-lookup"><span data-stu-id="c6102-p101">The SharePoint list webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library. SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span>

SharePoint-Listen-Webhooks umfassen die Ereignisse, die Listenelementänderungen für eine angegeben SharePoint-Liste oder Dokumentbibliothek entspricht. SharePoint-Webhooks bieten eine einfache Benachrichtigungspipeline, damit Ihre Anwendung Änderungen an einer SharePoint-Liste erkennen kann, ohne den Dienst abzurufen.

## <a name="tasks"></a><span data-ttu-id="c6102-104">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="c6102-104">Tasks</span></span>
| <span data-ttu-id="c6102-105">Aufgabe</span><span class="sxs-lookup"><span data-stu-id="c6102-105">Task</span></span>                                                | <span data-ttu-id="c6102-106">HTTP-Methode</span><span class="sxs-lookup"><span data-stu-id="c6102-106">HTTP method</span></span>                                                  |
|-----------------------------------------------------|--------------------------------------------------------------|
| [<span data-ttu-id="c6102-107">Erstellen eines neuen Abonnements</span><span class="sxs-lookup"><span data-stu-id="c6102-107">Create a new subscription</span></span>](./create-subscription) | `POST    /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="c6102-108">Abrufen von Abonnements</span><span class="sxs-lookup"><span data-stu-id="c6102-108">Get subscriptions</span></span>](./get-subscription)          | `GET     /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="c6102-109">Löschen eines Abonnements</span><span class="sxs-lookup"><span data-stu-id="c6102-109">Delete a subscription</span></span>](./delete-subscription)       | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`   |
| [<span data-ttu-id="c6102-110">Aktualisieren eines Abonnements</span><span class="sxs-lookup"><span data-stu-id="c6102-110">Update a subscription</span></span>](./update-subscription)     | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`   |

## <a name="list-event-types"></a><span data-ttu-id="c6102-111">Listenereignistypen</span><span class="sxs-lookup"><span data-stu-id="c6102-111">List event types</span></span>
<span data-ttu-id="c6102-112">Benachrichtigungen werden an Ihre Anwendung für die folgenden asynchronen Listenelementereignisse in SharePoint gesendet:</span><span class="sxs-lookup"><span data-stu-id="c6102-112">Notifications will be sent to your application for the following asynchronous list item events in SharePoint:</span></span>

* <span data-ttu-id="c6102-113">ItemAdded</span><span class="sxs-lookup"><span data-stu-id="c6102-113">ItemAdded</span></span>
* <span data-ttu-id="c6102-114">ItemUpdated</span><span class="sxs-lookup"><span data-stu-id="c6102-114">ItemUpdated</span></span>
* <span data-ttu-id="c6102-115">ItemDeleted</span><span class="sxs-lookup"><span data-stu-id="c6102-115">ItemDeleted</span></span>
* <span data-ttu-id="c6102-116">ItemCheckedOut</span><span class="sxs-lookup"><span data-stu-id="c6102-116">ItemCheckedOut</span></span>
* <span data-ttu-id="c6102-117">ItemCheckedIn</span><span class="sxs-lookup"><span data-stu-id="c6102-117">ItemCheckedIn</span></span>
* <span data-ttu-id="c6102-118">ItemUncheckedOut</span><span class="sxs-lookup"><span data-stu-id="c6102-118">ItemUncheckedOut</span></span>
* <span data-ttu-id="c6102-119">ItemAttachmentAdded</span><span class="sxs-lookup"><span data-stu-id="c6102-119">ItemAttachmentAdded</span></span>
* <span data-ttu-id="c6102-120">ItemAttachmentDeleted</span><span class="sxs-lookup"><span data-stu-id="c6102-120">ItemAttachmentDeleted</span></span>
* <span data-ttu-id="c6102-121">ItemFileMoved</span><span class="sxs-lookup"><span data-stu-id="c6102-121">ItemFileMoved</span></span>
* <span data-ttu-id="c6102-122">ItemVersionDeleted</span><span class="sxs-lookup"><span data-stu-id="c6102-122">ItemVersionDeleted</span></span>
* <span data-ttu-id="c6102-123">ItemFileConverted</span><span class="sxs-lookup"><span data-stu-id="c6102-123">ItemFileConverted</span></span>

<span data-ttu-id="c6102-124">Synchrone Ereignisse werden in Webhooks nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c6102-124">Synchronous events are not supported in webhooks.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c6102-125">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c6102-125">Additional resources</span></span>

* [<span data-ttu-id="c6102-126">Übersicht über SharePoint-Webhooks</span><span class="sxs-lookup"><span data-stu-id="c6102-126">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks)
