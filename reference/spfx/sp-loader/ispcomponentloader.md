<span data-ttu-id="9b65b-p101">Schnittstelle für das Modulladeprogramm. Es können Module und Skripts (über SystemJS) und CSS auf der Seite geladen werden. Außerdem wird der Zugriff auf die Manifeste ermöglicht, die auf der Seite vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="9b65b-p101">Interface for the module loader. It allows to load modules and scripts (through SystemJS) and CSS on the page. Also allows access to the manifests that exist in the page.</span></span>







Schnittstelle für das Modulladeprogramm. Es können Module und Skripts (über SystemJS) und CSS auf der Seite geladen werden. Außerdem wird der Zugriff auf die Manifeste ermöglicht, die auf der Seite vorhanden sind.







## <a name="methods"></a><span data-ttu-id="9b65b-105">Methoden</span><span class="sxs-lookup"><span data-stu-id="9b65b-105">Methods</span></span>

| <span data-ttu-id="9b65b-106">Methode</span><span class="sxs-lookup"><span data-stu-id="9b65b-106">Method</span></span>       |  <span data-ttu-id="9b65b-107">Rückgabewerte</span><span class="sxs-lookup"><span data-stu-id="9b65b-107">Returns</span></span>   | <span data-ttu-id="9b65b-108">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="9b65b-108">Description</span></span>|
|:-------------|:-------|:-----------|
|[`loadComponent(manifest)`](loadcomponent-ispcomponentloader.md)      | `Promise<TComponent>` | <span data-ttu-id="9b65b-109">Lädt eine Komponente aus einem Manifest.</span><span class="sxs-lookup"><span data-stu-id="9b65b-109">Loads a component from a manifest.</span></span> |
|[`loadCss(url)`](loadcss-ispcomponentloader.md)      | `void` | <span data-ttu-id="9b65b-110">Fügt ein <link ... />-Tag für ein Stylesheet hinzu.</span><span class="sxs-lookup"><span data-stu-id="9b65b-110">Inserts a <link ... /> tag for a stylesheet.</span></span> |
|[`loadScript(url,options)`](loadscript-ispcomponentloader.md)      | `Promise<TModule>` | <span data-ttu-id="9b65b-111">Wenn eine URL vorhanden ist, wird ein Skript geladen.</span><span class="sxs-lookup"><span data-stu-id="9b65b-111">Given a URL, load a script.</span></span> |




