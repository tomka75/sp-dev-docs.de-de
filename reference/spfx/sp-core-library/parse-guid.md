# <a name="parseguid"></a>parse(guid)




Analysiert die Eingabezeichenfolge zum Erstellen eines neuen GUID-Objekts. Wenn die Zeichenfolge nicht analysiert werden kann, wird ein Fehler ausgelöst.

**Signatur:** _public static parse(guidString: string): [Guid](../sp-core-library/guid.md);_

**Gibt Folgendes zurück**: [`Guid`](../sp-core-library/guid.md)



Ein gültiges GUID-Objekt.

#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `guid`    |  | Die eingegebene Zeichenfolge. |


### <a name="remarks"></a>Bemerkungen

Beispiele für die von dieser Funktion akzeptierte Syntax: 'd5369f3b-bd7a-412a-9c0f-7f0650bb5489' '{d5369f3b-bd7a-412a-9c0f-7f0650bb5489}' '/Guid(d5369f3b-bd7a-412a-9c0f-7f0650bb5489)'

