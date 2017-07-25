<span data-ttu-id="8a0b3-p101">Überprüft, ob diese Version niedriger (d. h. älter) als der Eingabeparameter ist. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 0.9.9 lessThan 1.0.0 -> true 2.0 lessThan 2.0.0 -> false 3.0 lessThan 3.0.1 -> true 04.01 lessThan 4.1 -> false</span><span class="sxs-lookup"><span data-stu-id="8a0b3-p101">Checks if this version is less (i.e. older) than the input parameter. Missing patch number is treated as zero Examples: 0.9.9 lessThan 1.0.0 -> true 2.0 lessThan 2.0.0 -> false 3.0 lessThan 3.0.1 -> true 04.01 lessThan 4.1 -> false</span></span>




Überprüft, ob diese Version niedriger (d. h. älter) als der Eingabeparameter ist. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 0.9.9 lessThan 1.0.0 -> true 2.0 lessThan 2.0.0 -> false 3.0 lessThan 3.0.1 -> true 04.01 lessThan 4.1 -> false

<span data-ttu-id="8a0b3-104">**Signatur:** _public lessThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span><span class="sxs-lookup"><span data-stu-id="8a0b3-104">**Signature:** _public lessThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span></span>

<span data-ttu-id="8a0b3-105">**Gibt Folgendes zurück**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="8a0b3-105">**Returns**: `boolean`</span></span>



<span data-ttu-id="8a0b3-106">einen booleschen Wert, der angibt, ob diese Version niedriger als der Eingabeparameter ist.</span><span class="sxs-lookup"><span data-stu-id="8a0b3-106">A boolean indicating if this version is less than the input parameter</span></span>

#### <a name="parameters"></a><span data-ttu-id="8a0b3-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="8a0b3-107">Parameters</span></span>


| <span data-ttu-id="8a0b3-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="8a0b3-108">Parameter</span></span>    | <span data-ttu-id="8a0b3-109">Typ</span><span class="sxs-lookup"><span data-stu-id="8a0b3-109">Type</span></span>    | <span data-ttu-id="8a0b3-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8a0b3-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | <span data-ttu-id="8a0b3-111">Die Version, mit der verglichen werden soll</span><span class="sxs-lookup"><span data-stu-id="8a0b3-111">The version to compare with</span></span> |


