# <a name="createcustomnamedefaultcreator"></a><span data-ttu-id="27440-101">createCustom(name,defaultCreator)</span><span class="sxs-lookup"><span data-stu-id="27440-101">createCustom(name,defaultCreator)</span></span>




<span data-ttu-id="27440-102">Erstellt einen neuen ServiceKey, dessen standardmäßige Implementierung durch Aufruf des angegebenen Rückrufs abgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="27440-102">Constructs a new ServiceKey whose default implementation will be obtained by invoking the specified callback.</span></span>

<span data-ttu-id="27440-103">**Signatur:** _public static createCustom < T >(name: string, defaultCreator: ServiceCreator<T>): [ServiceKey](../sp-core-library/servicekey.md)<T>;_</span><span class="sxs-lookup"><span data-stu-id="27440-103">**Signature:** _public static createCustom < T >(name: string, defaultCreator: ServiceCreator<T>): [ServiceKey](../sp-core-library/servicekey.md)<T>;_</span></span>

<span data-ttu-id="27440-104">**Gibt Folgendes zurück**: [`ServiceKey`](../sp-core-library/servicekey.md)<T></span><span class="sxs-lookup"><span data-stu-id="27440-104">**Returns**: [`ServiceKey`](../sp-core-library/servicekey.md)<T></span></span>



- <span data-ttu-id="27440-105">den neu erstellten ServiceKey</span><span class="sxs-lookup"><span data-stu-id="27440-105">the newly created ServiceKey</span></span>

#### <a name="parameters"></a><span data-ttu-id="27440-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="27440-106">Parameters</span></span>


| <span data-ttu-id="27440-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="27440-107">Parameter</span></span>    | <span data-ttu-id="27440-108">Typ</span><span class="sxs-lookup"><span data-stu-id="27440-108">Type</span></span>    | <span data-ttu-id="27440-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="27440-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `name`    | `string` | <span data-ttu-id="27440-110">Ein Name wie z. B. "MyApplication.IMyService", der innerhalb der Anwendung eindeutig sein muss.</span><span class="sxs-lookup"><span data-stu-id="27440-110">A name such as "MyApplication.IMyService" which should be unique within your application.</span></span> |
| `defaultCreator`    | `ServiceCreator<T>` | <span data-ttu-id="27440-111">Ein Rückruf, der ein Objekt zurückgibt, das die T-Schnittstelle implementiert.</span><span class="sxs-lookup"><span data-stu-id="27440-111">A callback that returns an object that implements the T interface</span></span> |


