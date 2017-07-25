<span data-ttu-id="a03dd-p101">Überprüft, ob diese Version größer (d. h. neuer) als der Eingabeparameter ist. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 1.0.0 greaterThan 0.0.9 -> true 2.0 greaterThan 2.0.0 -> false 3.0.1 greaterThan 3.0 -> true</span><span class="sxs-lookup"><span data-stu-id="a03dd-p101">Checks if this version is greater (i.e. newer) than the input parameter. Missing patch number is treated as zero Examples: 1.0.0 greaterThan 0.0.9 -> true 2.0 greaterThan 2.0.0 -> false 3.0.1 greaterThan 3.0 -> true</span></span>




Überprüft, ob diese Version größer (d. h. neuer) als der Eingabeparameter ist. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 1.0.0 greaterThan 0.0.9 -> true 2.0 greaterThan 2.0.0 -> false 3.0.1 greaterThan 3.0 -> true

<span data-ttu-id="a03dd-104">**Signatur:** _public greaterThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span><span class="sxs-lookup"><span data-stu-id="a03dd-104">**Signature:** _public greaterThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span></span>

<span data-ttu-id="a03dd-105">**Gibt Folgendes zurück**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="a03dd-105">**Returns**: `boolean`</span></span>



<span data-ttu-id="a03dd-106">einen booleschen Wert, der angibt, ob diese Version größer als der Eingabeparameter ist.</span><span class="sxs-lookup"><span data-stu-id="a03dd-106">A boolean indicating if this version is greater than the input parameter</span></span>

#### <a name="parameters"></a><span data-ttu-id="a03dd-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="a03dd-107">Parameters</span></span>


| <span data-ttu-id="a03dd-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="a03dd-108">Parameter</span></span>    | <span data-ttu-id="a03dd-109">Typ</span><span class="sxs-lookup"><span data-stu-id="a03dd-109">Type</span></span>    | <span data-ttu-id="a03dd-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a03dd-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | <span data-ttu-id="a03dd-111">Die Version, mit der verglichen werden soll</span><span class="sxs-lookup"><span data-stu-id="a03dd-111">The version to compare with</span></span> |


