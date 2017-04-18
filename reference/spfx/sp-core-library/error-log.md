# <a name="errorsourceerrorscope"></a>error(source,error,scope)




Protokolliert einen Fehler

**Signatur:** _public static error(source: string, error: Error, scope?: [ServiceScope](../sp-core-library/servicescope.md)): void;_

**Gibt Folgendes zurück**: `void`





#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `source`    | `string` | die Quelle aus der der Fehler protokolliert wird, z. B. der Klassenname. Die Quelle bietet Kontextinformationen für den protokollierten Fehler. Wenn die Quelle länger als 20 Zeichen ist, werden nur die ersten 20 Zeichen behalten. |
| `error`    | `Error` | der zu protokollierende Fehler |
| `scope`    | [`ServiceScope`](../sp-core-library/servicescope.md) | __Optional.__ Der Dienstbereich, den die Quelle verwendet. Ein Dienstumfang kann weitere Kontextinformationen (z. B. Webpartinformationen) zum protokollierten Fehler bereitstellen. |


