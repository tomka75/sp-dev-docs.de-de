<span data-ttu-id="dec18-p101">Diese API sollte zum Rendern einer Fehlermeldung im Anzeigebereich des Webparts verwendet werden. Protokolliert auch die Fehlermeldung mithilfe der Ablaufverfolgungsprotokollierung.</span><span class="sxs-lookup"><span data-stu-id="dec18-p101">This API should be used to render an error message in the web part display area. Also logs the error message using the trace logger.</span></span>




Diese API sollte zum Rendern einer Fehlermeldung im Anzeigebereich des Webparts verwendet werden. Protokolliert auch die Fehlermeldung mithilfe der Ablaufverfolgungsprotokollierung.

<span data-ttu-id="dec18-104">**Signatur:** _protected renderError(error: Error): void;_</span><span class="sxs-lookup"><span data-stu-id="dec18-104">**Signature:** _protected renderError(error: Error): void;_</span></span>

<span data-ttu-id="dec18-105">**Gibt Folgendes zurück**: `void`</span><span class="sxs-lookup"><span data-stu-id="dec18-105">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="dec18-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="dec18-106">Parameters</span></span>


| <span data-ttu-id="dec18-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="dec18-107">Parameter</span></span>    | <span data-ttu-id="dec18-108">Typ</span><span class="sxs-lookup"><span data-stu-id="dec18-108">Type</span></span>    | <span data-ttu-id="dec18-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dec18-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `error`    | `Error` | <span data-ttu-id="dec18-110">Ein Fehlerobjekt das die zu rendernde Fehlermeldung enthält.</span><span class="sxs-lookup"><span data-stu-id="dec18-110">An error object containing the error message to render.</span></span> |


