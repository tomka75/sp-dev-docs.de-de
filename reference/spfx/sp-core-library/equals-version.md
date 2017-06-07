# <a name="equalscomparewith"></a>equals(compareWith)




Überprüft, ob diese Version dem Eingabeparameter entspricht. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 1.0.0 equals 1.0.0 -> true 2.0.1 equals 2.0.0 -> false 3.0 equals 3.0.0 -> true 04.01 equals 4.1 -> true

**Signatur:** _public equals(compareWith: [Version](../sp-core-library/version.md)): boolean;_

**Gibt Folgendes zurück**: `boolean`



einen booleschen Wert, der angibt, ob diese Version dem Eingabeparameter entspricht.

#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | Die Version, mit der verglichen werden soll |


