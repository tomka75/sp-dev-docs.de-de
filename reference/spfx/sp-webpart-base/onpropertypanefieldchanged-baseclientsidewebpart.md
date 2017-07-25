<span data-ttu-id="fe892-p101">Diese API wird nach dem Aktualisieren des neuen Werts der Eigenschaft im Eigenschaftenbehälter aufgerufen, wenn der PropertyPane im reaktiven Modus verwendet wird. Die grundlegende Implementierung dieser API rendert das Webpart erneut.</span><span class="sxs-lookup"><span data-stu-id="fe892-p101">This API is invoked after updating the new value of the property in the property bag when the PropertyPane is being used in Reactive mode. The base implementation of this API re-renders the web part.</span></span>




Diese API wird nach dem Aktualisieren des neuen Werts der Eigenschaft im Eigenschaftenbehälter aufgerufen, wenn der PropertyPane im reaktiven Modus verwendet wird. Die grundlegende Implementierung dieser API rendert das Webpart erneut.

<span data-ttu-id="fe892-104">**Signatur:** _@virtual protected onPropertyPaneFieldChanged(propertyPath: string, oldValue: any, newValue: any): void;_</span><span class="sxs-lookup"><span data-stu-id="fe892-104">**Signature:** _@virtual protected onPropertyPaneFieldChanged(propertyPath: string, oldValue: any, newValue: any): void;_</span></span>

<span data-ttu-id="fe892-105">**Gibt Folgendes zurück**: `void`</span><span class="sxs-lookup"><span data-stu-id="fe892-105">**Returns**: `void`</span></span>





#### <a name="parameters"></a><span data-ttu-id="fe892-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="fe892-106">Parameters</span></span>


| <span data-ttu-id="fe892-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="fe892-107">Parameter</span></span>    | <span data-ttu-id="fe892-108">Typ</span><span class="sxs-lookup"><span data-stu-id="fe892-108">Type</span></span>    | <span data-ttu-id="fe892-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="fe892-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `propertyPath`    | `string` | <span data-ttu-id="fe892-110">JSON-Pfad der Eigenschaft im Eigenschaftenbehälter.</span><span class="sxs-lookup"><span data-stu-id="fe892-110">JSON path of the property in the property bag.</span></span> |
| `oldValue`    | `any` | <span data-ttu-id="fe892-111">Der alte Wert der Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="fe892-111">Old value of the property.</span></span> |
| `newValue`    | `any` | <span data-ttu-id="fe892-112">Der neue Wert der Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="fe892-112">New value of the property.</span></span> |


