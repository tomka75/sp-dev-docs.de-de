<span data-ttu-id="38302-p101">Die Log-Klasse stellt statische Methoden zum Protokollieren von Meldungen auf unterschiedlichen Ebenen (ausführliche, Information, Warnung, Fehler) und mit Kontextinformationen bereit. Kontextinformationen helfen bei der Identifizierung, welche Komponente die Meldungen generiert hat, und gestalten die Meldung hilfreich und filterbar.</span><span class="sxs-lookup"><span data-stu-id="38302-p101">The Log class provides static methods for logging messages at different levels (verbose, info, warning, error) and with context information. Context information helps identify which component generated the messages and makes the messages useful and filterable.</span></span>







Die Log-Klasse stellt statische Methoden zum Protokollieren von Meldungen auf unterschiedlichen Ebenen (ausführliche, Information, Warnung, Fehler) und mit Kontextinformationen bereit. Kontextinformationen helfen bei der Identifizierung, welche Komponente die Meldungen generiert hat, und gestalten die Meldung hilfreich und filterbar.






## <a name="methods"></a><span data-ttu-id="38302-104">Methoden</span><span class="sxs-lookup"><span data-stu-id="38302-104">Methods</span></span>

| <span data-ttu-id="38302-105">Methode</span><span class="sxs-lookup"><span data-stu-id="38302-105">Method</span></span>       | <span data-ttu-id="38302-106">Zugriffsmodifizierer</span><span class="sxs-lookup"><span data-stu-id="38302-106">Access Modifier</span></span> | <span data-ttu-id="38302-107">Rückgabewerte</span><span class="sxs-lookup"><span data-stu-id="38302-107">Returns</span></span>  | <span data-ttu-id="38302-108">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="38302-108">Description</span></span>|
|:-------------|:----|:-------|:-----------|
|[`error(source,error,scope)`](error-log.md)     | `public, static` | `void` | <span data-ttu-id="38302-109">Protokolliert einen Fehler</span><span class="sxs-lookup"><span data-stu-id="38302-109">Logs an error</span></span> |
|[`info(source,message,scope)`](info-log.md)     | `public, static` | `void` | <span data-ttu-id="38302-110">Protokolliert eine Meldung nur zu Informationszwecken.</span><span class="sxs-lookup"><span data-stu-id="38302-110">Logs an informational message</span></span> |
|[`verbose(source,message,scope)`](verbose-log.md)     | `public, static` | `void` | <span data-ttu-id="38302-111">Protokolliert eine ausführliche Meldung.</span><span class="sxs-lookup"><span data-stu-id="38302-111">Logs a verbose message</span></span> |
|[`warn(source,message,scope)`](warn-log.md)     | `public, static` | `void` | <span data-ttu-id="38302-112">Protokolliert eine Warnung.</span><span class="sxs-lookup"><span data-stu-id="38302-112">Logs a warning</span></span> |

## <a name="sample"></a><span data-ttu-id="38302-113">Beispiel</span><span class="sxs-lookup"><span data-stu-id="38302-113">Sample</span></span>
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
