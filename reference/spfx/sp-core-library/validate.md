<span data-ttu-id="c4fe3-p101">Diese Klasse implementiert ein Standardverfahren zum Überprüfen von Eigenschaften und Funktionsparametern. Im Gegensatz zu Debugassertionen werden Validate-Überprüfungen immer durchgeführt und lösen immer einen Fehler aus, auch in einer Produktionsversion. Achten Sie daher darauf, diese Überprüfungen nicht zu häufig zu verwenden, damit die Leistung nicht beeinträchtigt wird.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-p101">This class implements provides a standard way to validate properties and function parameters. Unlike debug assertions, Validate checks are always performed and will always throw an error, even in a production release. As such, be careful not to overuse these checks in a way that might impact performance.</span></span>







Diese Klasse implementiert ein Standardverfahren zum Überprüfen von Eigenschaften und Funktionsparametern. Im Gegensatz zu Debugassertionen werden Validate-Überprüfungen immer durchgeführt und lösen immer einen Fehler aus, auch in einer Produktionsversion. Achten Sie daher darauf, diese Überprüfungen nicht zu häufig zu verwenden, damit die Leistung nicht beeinträchtigt wird.






## <a name="methods"></a><span data-ttu-id="c4fe3-105">Methoden</span><span class="sxs-lookup"><span data-stu-id="c4fe3-105">Methods</span></span>

| <span data-ttu-id="c4fe3-106">Methode</span><span class="sxs-lookup"><span data-stu-id="c4fe3-106">Method</span></span>       | <span data-ttu-id="c4fe3-107">Zugriffsmodifizierer</span><span class="sxs-lookup"><span data-stu-id="c4fe3-107">Access Modifier</span></span> | <span data-ttu-id="c4fe3-108">Rückgabewerte</span><span class="sxs-lookup"><span data-stu-id="c4fe3-108">Returns</span></span>  | <span data-ttu-id="c4fe3-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="c4fe3-109">Description</span></span>|
|:-------------|:----|:-------|:-----------|
|[`isNonemptyString(value,variableName)`](isnonemptystring-validate.md)     | `public, static` | `void` | <span data-ttu-id="c4fe3-110">Löst eine Ausnahme aus, wenn die angegebene Zeichenfolge NULL, nicht definiert oder eine leere Zeichenfolge ist.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-110">Throws an exception if the specified string is null, undefined, or an empty string.</span></span> |
|[`isNotNullOrUndefined(value,variableName)`](isnotnullorundefined-validate.md)     | `public, static` | `void` | <span data-ttu-id="c4fe3-111">Löst eine Ausnahme aus, wenn der angegebene Wert NULL oder nicht definiert ist.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-111">Throws an exception if the specified value is null or undefined.</span></span> |
|[`isTrue(value,variableName)`](istrue-validate.md)     | `public, static` | `void` | <span data-ttu-id="c4fe3-112">Löst eine Ausnahme aus, wenn der angegebene Wert nicht „true“ ist.</span><span class="sxs-lookup"><span data-stu-id="c4fe3-112">Throws an exception if the specified value is not true.</span></span> |

## <a name="sample"></a><span data-ttu-id="c4fe3-113">Beispiel</span><span class="sxs-lookup"><span data-stu-id="c4fe3-113">Sample</span></span>
```ts
import {
  Validate
} from '@microsoft/sp-core-library';

Validate.isNonemptyString(idValue, "idValue");
Validate.isNotNullOrUndefined(idValue, "idValue");
Validate.isTrue((idValue !== undefined), "idValue");
```
