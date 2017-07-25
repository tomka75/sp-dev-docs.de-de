<span data-ttu-id="1a562-p101">Überprüft, ob diese Version dem Eingabeparameter entspricht. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 1.0.0 equals 1.0.0 -> true 2.0.1 equals 2.0.0 -> false 3.0 equals 3.0.0 -> true 04.01 equals 4.1 -> true</span><span class="sxs-lookup"><span data-stu-id="1a562-p101">Checks if this version is equal to the input parameter. Missing patch number is treated as zero. Examples: 1.0.0 equals 1.0.0 -> true 2.0.1 equals 2.0.0 -> false 3.0 equals 3.0.0 -> true 04.01 equals 4.1 -> true</span></span>




Überprüft, ob diese Version dem Eingabeparameter entspricht. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 1.0.0 equals 1.0.0 -> true 2.0.1 equals 2.0.0 -> false 3.0 equals 3.0.0 -> true 04.01 equals 4.1 -> true

<span data-ttu-id="1a562-105">**Signatur:** _public equals(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span><span class="sxs-lookup"><span data-stu-id="1a562-105">**Signature:** _public equals(compareWith: [Version](../sp-core-library/version.md)): boolean;_</span></span>

<span data-ttu-id="1a562-106">**Gibt Folgendes zurück**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="1a562-106">**Returns**: `boolean`</span></span>



<span data-ttu-id="1a562-107">einen booleschen Wert, der angibt, ob diese Version dem Eingabeparameter entspricht.</span><span class="sxs-lookup"><span data-stu-id="1a562-107">A boolean indicating if this version is equal to the input parameter</span></span>

#### <a name="parameters"></a><span data-ttu-id="1a562-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="1a562-108">Parameters</span></span>


| <span data-ttu-id="1a562-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="1a562-109">Parameter</span></span>    | <span data-ttu-id="1a562-110">Typ</span><span class="sxs-lookup"><span data-stu-id="1a562-110">Type</span></span>    | <span data-ttu-id="1a562-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1a562-111">Description</span></span> |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | <span data-ttu-id="1a562-112">Die Version, mit der verglichen werden soll</span><span class="sxs-lookup"><span data-stu-id="1a562-112">The version to compare with</span></span> |


