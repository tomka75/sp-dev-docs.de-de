# <a name="createdefaultandprovideservicekey"></a><span data-ttu-id="df8b1-101">createDefaultAndProvide(serviceKey)</span><span class="sxs-lookup"><span data-stu-id="df8b1-101">createDefaultAndProvide(serviceKey)</span></span>




<span data-ttu-id="df8b1-102">Dies ist eine Abkürzungsfunktion, die die Standardimplementierung des angegebenen ServiceKey erstellt und ihn dann durch Aufrufen von ServiceScope.provide() registriert.</span><span class="sxs-lookup"><span data-stu-id="df8b1-102">This is a shorthand function that constructs the default implementation of the specified serviceKey, and then registers it by calling ServiceScope.provide().</span></span>

<span data-ttu-id="df8b1-103">**Signatur:** _public createDefaultAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_</span><span class="sxs-lookup"><span data-stu-id="df8b1-103">**Signature:** _public createDefaultAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_</span></span>

<span data-ttu-id="df8b1-104">**Gibt Folgendes zurück**: `T`</span><span class="sxs-lookup"><span data-stu-id="df8b1-104">**Returns**: `T`</span></span>



- <span data-ttu-id="df8b1-105">eine Dienstinstanz, die mit ServiceKey.defaultCreator erstellt wurde</span><span class="sxs-lookup"><span data-stu-id="df8b1-105">a service instance that was constructed using ServiceKey.defaultCreator</span></span>

#### <a name="parameters"></a><span data-ttu-id="df8b1-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="df8b1-106">Parameters</span></span>


| <span data-ttu-id="df8b1-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="df8b1-107">Parameter</span></span>    | <span data-ttu-id="df8b1-108">Typ</span><span class="sxs-lookup"><span data-stu-id="df8b1-108">Type</span></span>    | <span data-ttu-id="df8b1-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="df8b1-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | <span data-ttu-id="df8b1-110">der Schlüssel, der später verwendet werden kann, um den Dienst nutzen</span><span class="sxs-lookup"><span data-stu-id="df8b1-110">the key that can be used later to consume the service</span></span> |


