# <a name="validate-class"></a>Validate-Klasse







Diese Klasse implementiert ein Standardverfahren zum Überprüfen von Eigenschaften und Funktionsparametern. Im Gegensatz zu Debugassertionen werden Validate-Überprüfungen immer durchgeführt und lösen immer einen Fehler aus, auch in einer Produktionsversion. Achten Sie daher darauf, diese Überprüfungen nicht zu häufig zu verwenden, damit die Leistung nicht beeinträchtigt wird.






## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte    | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`isNonemptyString(value,variableName)`](isnonemptystring-validate.md)     | `public, static` | `void` | Löst eine Ausnahme aus, wenn die angegebene Zeichenfolge NULL, nicht definiert oder eine leere Zeichenfolge ist. |
|[`isNotNullOrUndefined(value,variableName)`](isnotnullorundefined-validate.md)     | `public, static` | `void` | Löst eine Ausnahme aus, wenn der angegebene Wert NULL oder nicht definiert ist. |
|[`isTrue(value,variableName)`](istrue-validate.md)     | `public, static` | `void` | Löst eine Ausnahme aus, wenn der angegebene Wert nicht „true“ ist. |

## <a name="sample"></a>Beispiel
```ts
import {
  Validate
} from '@microsoft/sp-core-library';

Validate.isNonemptyString(idValue, "idValue");
Validate.isNotNullOrUndefined(idValue, "idValue");
Validate.isTrue((idValue !== undefined), "idValue");
```
