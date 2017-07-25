# <a name="createandprovideservicekeysimpleserviceclass"></a><span data-ttu-id="5e382-101">createAndProvide(serviceKey,simpleServiceClass)</span><span class="sxs-lookup"><span data-stu-id="5e382-101">createAndProvide(serviceKey,simpleServiceClass)</span></span>




<span data-ttu-id="5e382-102">Dies ist eine Abkürzungsfunktion, die dem Erstellen einer neuen Instanz von SimpleServiceClass entspricht und dann durch Aufruf von ServiceScope.provide() registriert wird.</span><span class="sxs-lookup"><span data-stu-id="5e382-102">This is a shorthand function that its equivalent to constructing a new instance of the simpleServiceClass, then registering it by calling ServiceScope.provide().</span></span>

<span data-ttu-id="5e382-103">**Signatur:** _public createAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, simpleServiceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): T;_</span><span class="sxs-lookup"><span data-stu-id="5e382-103">**Signature:** _public createAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, simpleServiceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): T;_</span></span>

<span data-ttu-id="5e382-104">**Gibt Folgendes zurück**: `T`</span><span class="sxs-lookup"><span data-stu-id="5e382-104">**Returns**: `T`</span></span>



- <span data-ttu-id="5e382-105">eine neu erstellte Instanz von simpleServiceClass</span><span class="sxs-lookup"><span data-stu-id="5e382-105">a newly constructed instance of simpleServiceClass</span></span>

#### <a name="parameters"></a><span data-ttu-id="5e382-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="5e382-106">Parameters</span></span>


| <span data-ttu-id="5e382-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="5e382-107">Parameter</span></span>    | <span data-ttu-id="5e382-108">Typ</span><span class="sxs-lookup"><span data-stu-id="5e382-108">Type</span></span>    | <span data-ttu-id="5e382-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="5e382-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | <span data-ttu-id="5e382-110">der Schlüssel, der später verwendet werden kann, um den Dienst nutzen</span><span class="sxs-lookup"><span data-stu-id="5e382-110">the key that can be used later to consume the service</span></span> |
| `simpleServiceClass`    | `{ new (serviceScope: ServiceScope); }` | <span data-ttu-id="5e382-111">die zu erstellende TypeScript-Klasse</span><span class="sxs-lookup"><span data-stu-id="5e382-111">the TypeScript class to be constructed</span></span> |


