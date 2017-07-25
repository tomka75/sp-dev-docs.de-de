<span data-ttu-id="ddd2d-p101">Analysiert die Eingabezeichenfolge zum Erstellen eines neuen GUID-Objekts. Wenn die Zeichenfolge nicht analysiert werden kann, wird ein Fehler ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="ddd2d-p101">Parses the input string to construct a new Guid object. If the string cannot be parsed, then an error is thrown.</span></span>




Analysiert die Eingabezeichenfolge zum Erstellen eines neuen GUID-Objekts. Wenn die Zeichenfolge nicht analysiert werden kann, wird ein Fehler ausgelöst.

<span data-ttu-id="ddd2d-104">**Signatur:** _public static parse(guidString: string): [Guid](../sp-core-library/guid.md);_</span><span class="sxs-lookup"><span data-stu-id="ddd2d-104">**Signature:** _public static parse(guidString: string): [Guid](../sp-core-library/guid.md);_</span></span>

<span data-ttu-id="ddd2d-105">**Gibt Folgendes zurück**: [`Guid`](../sp-core-library/guid.md)</span><span class="sxs-lookup"><span data-stu-id="ddd2d-105">**Returns**: [`Guid`](../sp-core-library/guid.md)</span></span>



<span data-ttu-id="ddd2d-106">Ein gültiges GUID-Objekt.</span><span class="sxs-lookup"><span data-stu-id="ddd2d-106">A valid Guid object</span></span>

#### <a name="parameters"></a><span data-ttu-id="ddd2d-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="ddd2d-107">Parameters</span></span>


| <span data-ttu-id="ddd2d-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="ddd2d-108">Parameter</span></span>    | <span data-ttu-id="ddd2d-109">Typ</span><span class="sxs-lookup"><span data-stu-id="ddd2d-109">Type</span></span>    | <span data-ttu-id="ddd2d-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ddd2d-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `guid`    |  | <span data-ttu-id="ddd2d-111">Die eingegebene Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="ddd2d-111">The input string.</span></span> |


### <a name="remarks"></a><span data-ttu-id="ddd2d-112">Bemerkungen</span><span class="sxs-lookup"><span data-stu-id="ddd2d-112">Remarks</span></span>

<span data-ttu-id="ddd2d-113">Beispiele für die von dieser Funktion akzeptierte Syntax: 'd5369f3b-bd7a-412a-9c0f-7f0650bb5489' '{d5369f3b-bd7a-412a-9c0f-7f0650bb5489}' '/Guid(d5369f3b-bd7a-412a-9c0f-7f0650bb5489)'</span><span class="sxs-lookup"><span data-stu-id="ddd2d-113">Example syntaxes accepted by this function: 'd5369f3b-bd7a-412a-9c0f-7f0650bb5489' '{d5369f3b-bd7a-412a-9c0f-7f0650bb5489}' '/Guid(d5369f3b-bd7a-412a-9c0f-7f0650bb5489)'</span></span>

