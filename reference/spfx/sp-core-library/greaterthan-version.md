# <a name="greaterthancomparewith"></a>greaterThan(compareWith)




Überprüft, ob diese Version größer (d. h. neuer) als der Eingabeparameter ist. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 1.0.0 greaterThan 0.0.9 -> true 2.0 greaterThan 2.0.0 -> false 3.0.1 greaterThan 3.0 -> true

**Signatur:** _public greaterThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_

**Gibt Folgendes zurück**: `boolean`



einen booleschen Wert, der angibt, ob diese Version größer als der Eingabeparameter ist.

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | Die Version, mit der verglichen werden soll |


