# <a name="hasanypermissionsrequestedperms"></a><span data-ttu-id="045c2-101">hasAnyPermissions(...requestedPerms)</span><span class="sxs-lookup"><span data-stu-id="045c2-101">hasAnyPermissions(...requestedPerms)</span></span>




<span data-ttu-id="045c2-102">Funktion zum Bestimmen, ob eine bestimmte Berechtigungsmaske über eine der angeforderten Berechtigungen verfügt.</span><span class="sxs-lookup"><span data-stu-id="045c2-102">Function for determining if a given permission mask has any of the requested permissions.</span></span>

<span data-ttu-id="045c2-103">**Signatur:** _public hasAnyPermissions(...requestedPerms: [SPPermission](../sp-page-context/sppermission.md)[]): boolean;_</span><span class="sxs-lookup"><span data-stu-id="045c2-103">**Signature:** _public hasAnyPermissions(...requestedPerms: [SPPermission](../sp-page-context/sppermission.md)[]): boolean;_</span></span>

<span data-ttu-id="045c2-104">**Gibt Folgendes zurück**: `boolean`</span><span class="sxs-lookup"><span data-stu-id="045c2-104">**Returns**: `boolean`</span></span>





#### <a name="parameters"></a><span data-ttu-id="045c2-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="045c2-105">Parameters</span></span>


| <span data-ttu-id="045c2-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="045c2-106">Parameter</span></span>    | <span data-ttu-id="045c2-107">Typ</span><span class="sxs-lookup"><span data-stu-id="045c2-107">Type</span></span>    | <span data-ttu-id="045c2-108">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="045c2-108">Description</span></span> |
|:-------------|:---------------|:------------|
| `...requestedPerms`    | <span data-ttu-id="045c2-109">[`SPPermission`](../sp-page-context/sppermission.md)[]</span><span class="sxs-lookup"><span data-stu-id="045c2-109"></span></span> | <span data-ttu-id="045c2-110">Beliebige Anzahl von SPPermission-Objekten, die mit dem Original verglichen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="045c2-110">Any number of SPPermission objects to be compared against the original</span></span> |


