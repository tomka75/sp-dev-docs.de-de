# <a name="isvalidguid"></a>isValid(guid)




Gibt an, ob eine GUID gültig ist, d. h., ob sie von Guid.tryParse() erfolgreich analysiert werden würde. Diese Funktion ist günstiger als Guid.tryParse(), weil kein GUID-Objekt erstellt wird.

**Signatur:** _public static isValid(guid: string): boolean;_

**Gibt Folgendes zurück**: `boolean`



„True“, wenn die GUID gültig ist.

#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `guid`    | `string` | Die eingegebene Zeichenfolge. |


