# <a name="ispcomponentloader-interface"></a>ISPComponentLoader-Schnittstelle







Schnittstelle für das Modulladeprogramm. Es können Module und Skripts (über SystemJS) und CSS auf der Seite geladen werden. Außerdem wird der Zugriff auf die Manifeste ermöglicht, die auf der Seite vorhanden sind.







## <a name="methods"></a>Methoden

| Methode       |  Rückgabewerte   | Beschreibung|
|:-------------|:-------|:-----------|
|[`loadComponent(manifest)`](loadcomponent-ispcomponentloader.md)      | `Promise<TComponent>` | Lädt eine Komponente aus einem Manifest. |
|[`loadCss(url)`](loadcss-ispcomponentloader.md)      | `void` | Fügt ein <link ... />-Tag für ein Stylesheet hinzu. |
|[`loadScript(url,options)`](loadscript-ispcomponentloader.md)      | `Promise<TModule>` | Wenn eine URL vorhanden ist, wird ein Skript geladen. |




