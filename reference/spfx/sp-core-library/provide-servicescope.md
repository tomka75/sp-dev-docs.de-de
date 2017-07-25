<span data-ttu-id="8ebce-p101">ServiceScope.provide() wird zum Registrieren einer Implementierung der angegebenen serviceKey für den aktuellen Bereich verwendet. Dies kann nur verwendet werden, wenn der ServiceScope sich in einem „nicht abgeschlossenen“ Zustand befindet, d. h., bevor finish() aufgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="8ebce-p101">ServiceScope.provide() is used to register an implemententation of the given serviceKey for the current scope. It may only be used when the ServiceScope is in an "unfinished" state, i.e. before finish() has been called.</span></span>




ServiceScope.provide() wird zum Registrieren einer Implementierung der angegebenen serviceKey für den aktuellen Bereich verwendet. Dies kann nur verwendet werden, wenn der ServiceScope sich in einem „nicht abgeschlossenen“ Zustand befindet, d. h., bevor finish() aufgerufen wurde.

<span data-ttu-id="8ebce-104">**Signatur:** _public provide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, service: T): T;_</span><span class="sxs-lookup"><span data-stu-id="8ebce-104">**Signature:** _public provide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, service: T): T;_</span></span>

<span data-ttu-id="8ebce-105">**Gibt Folgendes zurück**: `T`</span><span class="sxs-lookup"><span data-stu-id="8ebce-105">**Returns**: `T`</span></span>



- <span data-ttu-id="8ebce-106">Das gleiche Objekt, das Dienstparameter übergeben wurde</span><span class="sxs-lookup"><span data-stu-id="8ebce-106">the same object that was passed as the "service" parameter</span></span>

#### <a name="parameters"></a><span data-ttu-id="8ebce-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="8ebce-107">Parameters</span></span>


| <span data-ttu-id="8ebce-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="8ebce-108">Parameter</span></span>    | <span data-ttu-id="8ebce-109">Typ</span><span class="sxs-lookup"><span data-stu-id="8ebce-109">Type</span></span>    | <span data-ttu-id="8ebce-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8ebce-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | <span data-ttu-id="8ebce-111">Der Schlüssel, der später verwendet wird, um den Dienst zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="8ebce-111">the key that will later be used to consume the service</span></span> |
| `service`    | `T` | <span data-ttu-id="8ebce-112">Die Dienstinstanz, die registriert wird.</span><span class="sxs-lookup"><span data-stu-id="8ebce-112">the service instance that is being registered</span></span> |


