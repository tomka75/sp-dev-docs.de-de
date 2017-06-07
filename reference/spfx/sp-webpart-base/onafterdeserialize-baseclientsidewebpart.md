# <a name="onafterdeserializedeserializedobjectdataversion"></a>onAfterDeserialize(deserializedObject,dataVersion)




Diese API wird aufgerufen, nachdem das Webpart für ein Objekt deserialisiert wurde – kurz vor dem Auffüllen des Eigenschaftenbehälters. Für die Standardimplementierung ist keine Aktion erforderlich. Ein Webpartentwickler kann diese API außer Kraft setzen, wenn das deserialisierte Objekt den Anfangszustand des Eigenschaftenbehälters nicht vollständig wiedergibt. So hat der Webpartentwickler die Möglichkeit, den Eigenschaftenbehälter direkt nach dem Deserialisieren der Daten für ein Obekt aufzufüllen.

**Signatur:** _@virtual protected onAfterDeserialize(deserializedObject: any, data[Version](../sp-core-library/version.md): Version): TProperties;_

**Gibt Folgendes zurück**: `TProperties`



Den Eigenschaftenbehälter des Webparts.

#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `deserializedObject`    | `any` | Das aus den gespeicherten Daten deserialisierte Objekt. Beachten Sie, dass das Schema dieses Objekt nicht unbedingt mit dem aktuellen Eigenschaftenbehälter konsistent ist, da die Serialisierung mit einer älteren Version des Webparts durchgeführt worden sein könnte. |
| `dataVersion`    | [`Version`](../sp-core-library/version.md) | Die Datenversion der gespeicherten Daten, die deserialisiert werden. Sie können diesen Wert verwenden, um zu bestimmen, ob die Daten von einem älteren Webpart serialisiert wurden. Webparts können ihre Datenversion durch Überschreiben der dataVersion-Eigenschaft definieren. |


### <a name="remarks"></a>HinwBemerkungeneise

Ein wichtiges Szenario für die Deserialisierung ist das Upgraden. Eine aktualisiertes Webpart kann die Daten laden, die von einer älteren Version des Webparts serialisiert wurden, das ein anderes Schema des Eigenschaftenbehälters unterstützt hat. Deshalb ist das deserialisierte Objekt nicht mit dem aktuellen Schema des Eigenschaftenbehälters konsistent. Der Entwickler kann onAfterDeserialize verwenden, um die dataVersion zu überprüfen und den Eigenschaftenbehälter zu korrigieren.

