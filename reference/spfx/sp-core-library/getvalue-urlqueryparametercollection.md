<span data-ttu-id="044cb-p101">Gibt den Wert für den ersten übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> undefined</span><span class="sxs-lookup"><span data-stu-id="044cb-p101">Returns the value of the first matching query parameter or undefined if the key doesn't exist. Examples: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> undefined</span></span>




Gibt den Wert für den ersten übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> undefined

<span data-ttu-id="044cb-104">**Signatur:** _public getValue(param: string): string;_</span><span class="sxs-lookup"><span data-stu-id="044cb-104">**Signature:** _public getValue(param: string): string;_</span></span>

<span data-ttu-id="044cb-105">**Gibt Folgendes zurück**: `string`</span><span class="sxs-lookup"><span data-stu-id="044cb-105">**Returns**: `string`</span></span>





#### <a name="parameters"></a><span data-ttu-id="044cb-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="044cb-106">Parameters</span></span>


| <span data-ttu-id="044cb-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="044cb-107">Parameter</span></span>    | <span data-ttu-id="044cb-108">Typ</span><span class="sxs-lookup"><span data-stu-id="044cb-108">Type</span></span>    | <span data-ttu-id="044cb-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="044cb-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `param`    | `string` | <span data-ttu-id="044cb-110">der nicht nach Groß-/Kleinschreibung unterscheidende Schlüssel für den gewünschten Abfrageparameterwert.</span><span class="sxs-lookup"><span data-stu-id="044cb-110">the case insensitive key for the desired query parameter value.</span></span> |


