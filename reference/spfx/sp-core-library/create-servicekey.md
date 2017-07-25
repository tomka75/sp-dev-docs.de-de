<span data-ttu-id="b5690-p101">Erstellt einen neue ServiceKey, dessen Implementierung standardmäßig eine neue Instanz einer TypeScript-Klasse ist, die den standardmäßigen Konstruktorparameter akzeptiert. Wenn Sie benutzerdefinierte Konstruktorparameter angeben möchten, verwenden Sie stattdessen createCustom().</span><span class="sxs-lookup"><span data-stu-id="b5690-p101">Constructs a new ServiceKey whose default implementation will be a new instance of a TypeScript class that accepts the standard constructor parameter. If you want to specify custom constructor parameters, use createCustom() instead.</span></span>




Erstellt einen neue ServiceKey, dessen Implementierung standardmäßig eine neue Instanz einer TypeScript-Klasse ist, die den standardmäßigen Konstruktorparameter akzeptiert. Wenn Sie benutzerdefinierte Konstruktorparameter angeben möchten, verwenden Sie stattdessen createCustom().

<span data-ttu-id="b5690-104">**Signatur:** _public static create < T >(name: string, serviceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): [ServiceKey](../sp-core-library/servicekey.md)<T>;_</span><span class="sxs-lookup"><span data-stu-id="b5690-104">**Signature:** _public static create < T >(name: string, serviceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): [ServiceKey](../sp-core-library/servicekey.md)<T>;_</span></span>

<span data-ttu-id="b5690-105">**Gibt Folgendes zurück**: [`ServiceKey`](../sp-core-library/servicekey.md)<T></span><span class="sxs-lookup"><span data-stu-id="b5690-105">**Returns**: [`ServiceKey`](../sp-core-library/servicekey.md)<T></span></span>



- <span data-ttu-id="b5690-106">den neu erstellten ServiceKey</span><span class="sxs-lookup"><span data-stu-id="b5690-106">the newly created ServiceKey</span></span>

#### <a name="parameters"></a><span data-ttu-id="b5690-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="b5690-107">Parameters</span></span>


| <span data-ttu-id="b5690-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="b5690-108">Parameter</span></span>    | <span data-ttu-id="b5690-109">Typ</span><span class="sxs-lookup"><span data-stu-id="b5690-109">Type</span></span>    | <span data-ttu-id="b5690-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b5690-110">Description</span></span> |
|:-------------|:---------------|:------------|
| `name`    | `string` | <span data-ttu-id="b5690-111">Ein Name wie z. B. "MyApplication.IMyService", der innerhalb der Anwendung eindeutig sein muss.</span><span class="sxs-lookup"><span data-stu-id="b5690-111">A name such as "MyApplication.IMyService" which should be unique within your application.</span></span> |
| `serviceClass`    | `{ new (serviceScope: ServiceScope); }` | <span data-ttu-id="b5690-112">die TypeScript-Klasse, die den Dienst implementiert.</span><span class="sxs-lookup"><span data-stu-id="b5690-112">the TypeScript class that implements the service.</span></span> |


