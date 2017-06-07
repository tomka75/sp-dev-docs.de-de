# <a name="getvaluesparam"></a>getValues(param)




Gibt die Werte für alle übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined

**Signatur:** _public getValues(param: string): string[];_

**Gibt Folgendes zurück**: `string[]`





#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `param`    | `string` | der nicht nach Groß-/Kleinschreibung unterscheidende Schlüssel für den gewünschten Abfrageparameterwert. |


