# <a name="tryparseguid"></a>tryParse(guid)




Versucht, die Eingabezeichenfolge zum Erstellen eines neuen GUID-Objekts zu analysieren. Wenn die Zeichenfolge nicht analysiert werden kann, wird undefiniert zurückgegeben.

**Signatur:** _public static tryParse(guid: string): [Guid](../sp-core-library/guid.md);_

**Gibt Folgendes zurück**: [`Guid`](../sp-core-library/guid.md)



Das GUID-Objekt oder undefiniert wenn die Zeichenfolge nicht analysiert werden konnte.

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `guid`    | `string` | Die eingegebene Zeichenfolge. |


### <a name="remarks"></a>Bemerkungen

Beispiele für die von dieser Funktion akzeptierte Syntax: 'd5369f3b-bd7a-412a-9c0f-7f0650bb5489' '{d5369f3b-bd7a-412a-9c0f-7f0650bb5489}' '/Guid(d5369f3b-bd7a-412a-9c0f-7f0650bb5489)'

