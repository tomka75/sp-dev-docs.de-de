# <a name="getvalueparam"></a>getValue(param)




Gibt den Wert für den ersten übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> undefined

**Signatur:** _public getValue(param: string): string;_

**Gibt Folgendes zurück**: `string`





#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `param`    | `string` | der nicht nach Groß-/Kleinschreibung unterscheidende Schlüssel für den gewünschten Abfrageparameterwert. |


