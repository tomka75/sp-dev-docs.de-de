<span data-ttu-id="cf393-p101">Gibt an, ob eine GUID gültig ist, d. h., ob sie von Guid.tryParse() erfolgreich analysiert werden würde. Diese Funktion ist günstiger als Guid.tryParse(), weil kein GUID-Objekt erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="cf393-p101">Indicates whether a guid is valid, i.e. whether it would be successfully parsed by Guid.tryParse(). This function is cheaper than Guid.tryParse() because it does not construct a Guid object.</span></span>




Gibt an, ob eine GUID gültig ist, d. h., ob sie von Guid.tryParse() erfolgreich analysiert werden würde. Diese Funktion ist günstiger als Guid.tryParse(), weil kein GUID-Objekt erstellt wird.

<span data-ttu-id="cf393-104">**Signatur:** _public static isValid(guid: string): boolean;_</span><span class="sxs-lookup"><span data-stu-id="cf393-104">**Signature:** _public static isValid(guid: string): boolean;_</span></span>

<span data-ttu-id="cf393-105">**Gibt Folgendes zurück**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="cf393-105">**Returns**: `boolean`</span></span>



<span data-ttu-id="cf393-106">„True“, wenn die GUID gültig ist.</span><span class="sxs-lookup"><span data-stu-id="cf393-106">true, if the Guid is valid.</span></span>

#### <a name="parameters"></a><span data-ttu-id="cf393-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="cf393-107">Parameters</span></span>


| <span data-ttu-id="cf393-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="cf393-108">Parameter</span></span>    | <span data-ttu-id="cf393-109">Typ</span><span class="sxs-lookup"><span data-stu-id="cf393-109">Type</span></span>    | <span data-ttu-id="cf393-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="cf393-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `guid`    | `string` | <span data-ttu-id="cf393-111">Die eingegebene Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="cf393-111">The input string.</span></span> |


