<span data-ttu-id="d0c65-p101">Diese API sollte überschrieben werden, um zeitintensive Operationen, z. B. das Abrufen von Daten von einem Remotedienst, vor dem ersten Rendern des Webparts durchzuführen. Die Ladeanzeige wird während der Lebensdauer dieser Methode angezeigt. Diese API wird nur einmal während des Lebenszyklus eines Webparts aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="d0c65-p101">This API should be overridden to perform long running operations e.g. data fetching from a remote service before the initial rendering of the web part. The loading indicator is displayed during the lifetime of this method. This API is called only once during the lifecycle of a web part.</span></span>




Diese API sollte überschrieben werden, um zeitintensive Operationen, z. B. das Abrufen von Daten von einem Remotedienst, vor dem ersten Rendern des Webparts durchzuführen. Die Ladeanzeige wird während der Lebensdauer dieser Methode angezeigt. Diese API wird nur einmal während des Lebenszyklus eines Webparts aufgerufen.

<span data-ttu-id="d0c65-105">**Signatur:** _@virtual protected onInit(): Zusage<void>;_</span><span class="sxs-lookup"><span data-stu-id="d0c65-105">**Signature:** _@virtual protected onInit(): Promise<void>;_</span></span>

<span data-ttu-id="d0c65-106">**Gibt Folgendes zurück**: `Promise<void>`</span><span class="sxs-lookup"><span data-stu-id="d0c65-106">**Returns**: `Promise<void>`</span></span>





#### <a name="parameters"></a><span data-ttu-id="d0c65-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="d0c65-107">Parameters</span></span>
<span data-ttu-id="d0c65-108">Keine</span><span class="sxs-lookup"><span data-stu-id="d0c65-108">None</span></span>


