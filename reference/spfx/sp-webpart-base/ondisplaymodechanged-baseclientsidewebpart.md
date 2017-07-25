<span data-ttu-id="0316f-p101">Diese API wird aufgerufen, wenn der Anzeigemodus eines Webparts geändert wird. Die standardmäßige Implementierung dieser API ruft die Webpart-Rendermethode auf, um das Webpart mit dem neuen Anzeigemodus erneut zu rendern. Wenn ein Webpartentwickler nicht möchte, dass bei einer Änderung des Anzeigemodus ein erneutes Rendern auftritt, kann er diese API überschreiben und bestimmte Updates für das Webpart-DOM ausführen, um den Anzeigemodus zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="0316f-p101">This API is called when the display mode of a web part is changed. The default implementation of this API calls the web part render method to re-render the web part with the new display mode. If a web part developer does not want a full re-render to happen on display mode change, they can override this API and perform specific updates to the web part DOM to switch its display mode.</span></span>




Diese API wird aufgerufen, wenn der Anzeigemodus eines Webparts geändert wird. Die standardmäßige Implementierung dieser API ruft die Webpart-Rendermethode auf, um das Webpart mit dem neuen Anzeigemodus erneut zu rendern. Wenn ein Webpartentwickler nicht möchte, dass bei einer Änderung des Anzeigemodus ein erneutes Rendern auftritt, kann er diese API überschreiben und bestimmte Updates für das Webpart-DOM ausführen, um den Anzeigemodus zu wechseln.

<span data-ttu-id="0316f-105">**Signatur:** _@virtual protected on[DisplayMode](../sp-core-library/displaymode.md)Changed(oldDisplayMode: DisplayMode): void;_</span><span class="sxs-lookup"><span data-stu-id="0316f-105">**Signature:** _@virtual protected on[DisplayMode](../sp-core-library/displaymode.md)Changed(oldDisplayMode: DisplayMode): void;_</span></span>

<span data-ttu-id="0316f-106">**Gibt Folgendes zurück**: `void`</span><span class="sxs-lookup"><span data-stu-id="0316f-106">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="0316f-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="0316f-107">Parameters</span></span>


| <span data-ttu-id="0316f-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="0316f-108">Parameter</span></span>    | <span data-ttu-id="0316f-109">Typ</span><span class="sxs-lookup"><span data-stu-id="0316f-109">Type</span></span>    | <span data-ttu-id="0316f-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="0316f-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `oldDisplayMode`    | [`DisplayMode`](../sp-core-library/displaymode.md) | <span data-ttu-id="0316f-111">Der alte Anzeigemodus.</span><span class="sxs-lookup"><span data-stu-id="0316f-111">The old display mode.</span></span> |


