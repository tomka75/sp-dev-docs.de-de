<span data-ttu-id="3ebb4-p103">Gibt die Werte für alle übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined</span><span class="sxs-lookup"><span data-stu-id="3ebb4-p103">Returns the values of all of the matching query parameters or undefined if the key doesn't exist. Examples: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined</span></span> |
|[`getValues(param)`](getvalues-urlqueryparametercollection.md)     | `public` | `string[]` | Gibt die Werte für alle übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined |

## <a name="sample"></a><span data-ttu-id="3ebb4-122">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3ebb4-122">Sample</span></span>

```ts
import {
  UrlQueryParameterCollection
} from '@microsoft/sp-core-library';

// ...
let queryParameterCollection = new UrlQueryParameterCollection(document.URL);
let idValue = queryParameterCollection.getValue("id");
// ...
```



