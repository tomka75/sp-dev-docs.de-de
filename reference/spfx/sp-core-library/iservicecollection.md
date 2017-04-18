# <a name="iservicecollection-interface"></a>IServiceCollection-Schnittstelle







Ein Muster in Kurzschrift zum Extrahieren bekannter Dienste aus einem ServiceScope.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`serviceScope`      | [`ServiceScope`](../sp-core-library/servicescope.md) | Gibt den zugrunde liegenden ServiceScope zurück, zu dem die Mitglieder gehören. |






### <a name="remarks"></a>Bemerkungen

Wiederverwendbare Bibliothekskomponenten deklarieren ihre Dienstabhängigkeiten in der Regel durch Aufrufen von ServiceScope.consume() mithilfe des entsprechenden ServiceKey für jeden Dienst. Für die Geschäftslogik der Anwendung oder kleine Projekte ist dieser Formalismus möglicherweise nicht erforderlich und würde die Lernkurve für Entwickler erhöhen. Als einfache Alternative können mit dem IServiceCollection-Muster gemeinsame Dienste für ein bestimmtes Szenario als eine einfache und praktische Sammlung übergeben werden. Beispielsweise kann eine Widget-Funktion die folgende Schnittstelle einführen: interface IWidgetServiceCollection extends IServiceCollection { spHttpClient: SPHttpClient; widgetManager: IWidgetManager; } Die Widget-Klasse kann dann möglicherweise eine „services“-Eigenschaft initialisieren, z. B.: property, like this: class Widget { private _services: IWidgetServiceCollection; constructor(serviceScope: ServiceScope) { serviceScope.whenFinished(() => { this._services = { serviceScope, spHttpClient: serviceScope.consume(SPHttpClient.serviceKey), widgetManager: serviceScope.consume(WidgetManager.ServiceKey), }; }); } public get services(): IWidgetServiceCollection {return diese ._services;}} Für eine Gruppe von Komponenten, die alle diese Abhängigkeiten aufweisen, kann dieses „services“-Objekt anstelle des abstrakten ServiceScope übergeben werden. Dies ermöglicht direkte Verweise, z. B. services.widgetManager, services.spHttpClient usw. Für untypische Abhängigkeiten steht weiterhin der services.serviceScope zur Verfügung. WICHTIG: Um das Muster übersichtlich und verständlich zu halten, sollte IServiceCollection NICHT mit zusätzlichen Elementen erweitert werden, bei denen es sich nicht um ServiceScope-Dienste handelt.

