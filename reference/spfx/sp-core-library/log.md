# <a name="log-class"></a>Log-Klasse







Die Log-Klasse stellt statische Methoden zum Protokollieren von Meldungen auf unterschiedlichen Ebenen (ausführliche, Information, Warnung, Fehler) und mit Kontextinformationen bereit. Kontextinformationen helfen bei der Identifizierung, welche Komponente die Meldungen generiert hat, und gestalten die Meldung hilfreich und filterbar.






## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`error(source,error,scope)`](error-log.md)     | `public, static` | `void` | Protokolliert einen Fehler |
|[`info(source,message,scope)`](info-log.md)     | `public, static` | `void` | Protokolliert eine Meldung nur zu Informationszwecken. |
|[`verbose(source,message,scope)`](verbose-log.md)     | `public, static` | `void` | Protokolliert eine ausführliche Meldung. |
|[`warn(source,message,scope)`](warn-log.md)     | `public, static` | `void` | Protokolliert eine Warnung. |

## <a name="sample"></a>Beispiel
```ts
import {
  Log
} from '@microsoft/sp-core-library';

// ...
Log.error("sample", new Error("error message"));
Log.info("sample", "informational message");
Log.warn("sample", "warning message");
Log.verbose("sample", "verbose message");
// ...
```
