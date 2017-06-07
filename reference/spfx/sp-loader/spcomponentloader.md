# <a name="spcomponentloader-class"></a>SPComponentLoader-Klasse







Komponentenladeprogramm. Muss mit einem implementierten ISPComponentLoader initialisiert werden.






## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`initialize()`](initialize-spcomponentloader.md)     | `public, static` | `void` | Initialisiert das Komponentenladeprogramm mit einer Implementierung. Muss einmal aufgerufen werden, bevor es verwendet werden kann. |
|[`loadComponent()`](loadcomponent-spcomponentloader.md)     | `public, static` | `Promise<TComponent>` | {@inheritdoc ISPComponentLoader.loadComponent} |
|[`loadCss()`](loadcss-spcomponentloader.md)     | `public, static` | `void` | {@inheritdoc ISPComponentLoader.loadCss} |
|[`loadScript()`](loadscript-spcomponentloader.md)     | `public, static` | `Promise<TModule>` | {@inheritdoc ISPComponentLoader.loadScript} |





