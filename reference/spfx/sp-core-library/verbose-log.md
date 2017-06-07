# <a name="verbosesourcemessagescope"></a>verbose(source,message,scope)




Protokolliert eine ausführliche Meldung.

**Signatur:** _public static verbose(source: string, message: string, scope?: [ServiceScope](../sp-core-library/servicescope.md)): void;_

**Gibt Folgendes zurück**: `void`





#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `source`    | `string` | Die Quelle, aus der die Meldung protokolliert wird, z. B. der Klassenname. Die Quelle bietet Kontextinformationen für die protokollierte Meldung. Wenn die Quelle länger als 20 Zeichen ist, werden nur die ersten 20 Zeichen behalten. |
| `message`    | `string` | Die zu protokollierende Meldung. Wenn die Meldung länger als 100 Zeichen ist, werden nur die ersten 100 Zeichen behalten. |
| `scope`    | [`ServiceScope`](../sp-core-library/servicescope.md) | __Optional.__ Der Dienstbereich, den die Quelle verwendet. Ein Dienstbereich kann weitere Kontextinformationen (z. B. Webpartinformationen) zur protokollierten Meldung bereitstellen. |


