<span data-ttu-id="fa793-p101">Komponenten sollten diese Funktion aufrufen, um eine Abhängigkeit zu nutzen, d. h. den Dienstschlüssel nachschlagen und die registrierte Dienstinstanz zurückgeben. Wenn die Instanz nicht gefunden werden kann, wird automatisch eine Standardinstanz erstellt und beim Stammdienstbereich registriert.</span><span class="sxs-lookup"><span data-stu-id="fa793-p101">Components should call this function to "consume" a dependency, i.e. look up the serviceKey and return the registered service instance. If the instance cannot be found, then a default instance will be autocreated and registered with the root ServiceScope.</span></span>




Komponenten sollten diese Funktion aufrufen, um eine Abhängigkeit zu nutzen, d. h. den Dienstschlüssel nachschlagen und die registrierte Dienstinstanz zurückgeben. Wenn die Instanz nicht gefunden werden kann, wird automatisch eine Standardinstanz erstellt und beim Stammdienstbereich registriert.

<span data-ttu-id="fa793-104">**Signatur:** _public consume < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_</span><span class="sxs-lookup"><span data-stu-id="fa793-104">**Signature:** _public consume < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_</span></span>

<span data-ttu-id="fa793-105">**Gibt Folgendes zurück**: `T`</span><span class="sxs-lookup"><span data-stu-id="fa793-105">**Returns**: `T`</span></span>



- <span data-ttu-id="fa793-106">die Dienstinstanz</span><span class="sxs-lookup"><span data-stu-id="fa793-106">the service instance</span></span>

#### <a name="parameters"></a><span data-ttu-id="fa793-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="fa793-107">Parameters</span></span>


| <span data-ttu-id="fa793-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="fa793-108">Parameter</span></span>    | <span data-ttu-id="fa793-109">Typ</span><span class="sxs-lookup"><span data-stu-id="fa793-109">Type</span></span>    | <span data-ttu-id="fa793-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="fa793-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | <span data-ttu-id="fa793-111">Der Schlüssel, der verwendet wurde, als provide() aufgerufen wurde, um den Dienst zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="fa793-111">the key that was used when provide() was called to register the service</span></span> |


