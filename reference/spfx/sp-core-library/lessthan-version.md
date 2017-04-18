# <a name="lessthancomparewith"></a>lessThan(compareWith)




Überprüft, ob diese Version niedriger (d. h. älter) als der Eingabeparameter ist. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 0.9.9 lessThan 1.0.0 -> true 2.0 lessThan 2.0.0 -> false 3.0 lessThan 3.0.1 -> true 04.01 lessThan 4.1 -> false

**Signatur:** _public lessThan(compareWith: [Version](../sp-core-library/version.md)): boolean;_

**Gibt Folgendes zurück**: `boolean`



einen booleschen Wert, der angibt, ob diese Version niedriger als der Eingabeparameter ist.

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `compareWith`    | [`Version`](../sp-core-library/version.md) | Die Version, mit der verglichen werden soll |


