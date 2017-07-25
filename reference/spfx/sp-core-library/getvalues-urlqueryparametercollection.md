<span data-ttu-id="dabf3-p101">Gibt die Werte für alle übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined</span><span class="sxs-lookup"><span data-stu-id="dabf3-p101">Returns the values of all of the matching query parameters or undefined if the key doesn't exist. Examples: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined</span></span>




Gibt die Werte für alle übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined

<span data-ttu-id="dabf3-104">**Signatur:** _public getValues(param: string): string[];_</span><span class="sxs-lookup"><span data-stu-id="dabf3-104">**Signature:** _public getValues(param: string): string[];_</span></span>

<span data-ttu-id="dabf3-105">**Gibt Folgendes zurück**: `string[]`</span><span class="sxs-lookup"><span data-stu-id="dabf3-105">**Returns**: `string[]`</span></span>





#### <a name="parameters"></a><span data-ttu-id="dabf3-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="dabf3-106">Parameters</span></span>


| <span data-ttu-id="dabf3-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="dabf3-107">Parameter</span></span>    | <span data-ttu-id="dabf3-108">Typ</span><span class="sxs-lookup"><span data-stu-id="dabf3-108">Type</span></span>    | <span data-ttu-id="dabf3-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dabf3-109">Description</span></span> |
|:-------------|:---------------|:------------|
| `param`    | `string` | <span data-ttu-id="dabf3-110">der nicht nach Groß-/Kleinschreibung unterscheidende Schlüssel für den gewünschten Abfrageparameterwert.</span><span class="sxs-lookup"><span data-stu-id="dabf3-110">the case insensitive key for the desired query parameter value.</span></span> |


