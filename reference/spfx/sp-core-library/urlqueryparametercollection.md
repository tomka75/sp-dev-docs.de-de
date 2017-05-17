# <a name="urlqueryparametercollection-class"></a>UrlQueryParameterCollection-Klasse







Klasse für das Speichern und Abrufen von Abfrageparametern. Die URL kann serverbezogen sein und analysiert leere/NULL-Zeichenfolgen. Die Abfrageparameter müssen mit „?“ beginnen, um den ersten Abfrageparameter anzuzeigen, und „&“ für alle nachfolgenden Parameter verwenden. Die Klasse unterstützt auch Fragmente. Verhalten von Edge-Fällen: Leerer Wert (www.example.com/?test=) speichert Schlüssel und leeren Wert Keine Gleichheitszeichen in queryParam (www.example.com/?test) speichert Schlüssel und undefinierten Wert Leerer queryParam (www.example.com/?&debug=on) speichert undefinierten Schlüssel und Wert und Wert Abfrageparameter nur mit Gleichheitszeichen (www.example.com/?=&debug=on) speichert leeren Zeichenfolgenschlüssel und -wert


## <a name="constructor"></a>Konstruktor


**Signatur:** _constructor(url: string);_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine





## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte    | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`getValue(param)`](getvalue-urlqueryparametercollection.md)     | `public` | `string` | Gibt den Wert für den ersten übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValue('TEST') ---> 'done' getValue('debug') ---> 'false' getValue('lost') ---> undefined |
|[`getValues(param)`](getvalues-urlqueryparametercollection.md)     | `public` | `string[]` | Gibt die Werte für alle übereinstimmenden Abfrageparameter oder undefiniert zurück, wenn der Schlüssel nicht vorhanden ist. Beispiele: this._queryParameterList = [ {key: TEST, value: done}, {key: DEBUG, value: false}, {key: TEST, value: notdone}] getValues('TEST') ---> ['done', 'notdone'] getValues('debug') ---> ['false'] getValues('lost') ---> undefined |

## <a name="sample"></a>Beispiel

```ts
import {
  UrlQueryParameterCollection
} from '@microsoft/sp-core-library';

// ...
let queryParameterCollection = new UrlQueryParameterCollection(document.URL);
let idValue = queryParameterCollection.getValue("id");
// ...
```



