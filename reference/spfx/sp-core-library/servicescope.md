# <a name="servicescope-class"></a>ServiceScope-Klasse







ServiceScope bietet eine formalisierte Möglichkeit für Komponenten zum Registrieren und Nutzen von Abhängigkeiten („Diensten“) sowie die Möglichkeit, dass unterschiedliche Implementierungen in unterschiedlichen Bereichen registriert werden. Dadurch wird die Modularität durch Entkopplung von Komponenten von ihren Abhängigkeiten wesentlich verbessert. Angenommen, verschiedene Komponenten müssen auf eine IPageManager-Instanz zugreifen. Wir könnten den PageManager einfach als Singleton (d. h. als globale Variable) erstellen, dies funktioniert aber nicht, wenn wir beispielsweise ein Popupfenster erstellen müssen, für das eine zweite PageManager-Instanz erforderlich ist. Eine bessere Lösung wäre, PageManager als Konstruktorparameter für die einzelnen Komponenten hinzufügen, für die er erforderlich ist. Dann sehen wir uns jedoch unmittelbar mit dem Problem konfrontiert, dass der Code, der diese Konstruktoren aufruft, auch einen PageManager-Parameter benötigt. In einer Anwendung mit vielen solchen Abhängigkeiten würde die Geschäftslogik, die viele Teilsysteme miteinander verbindet, schließlich einen Konstruktorparameter für jede möglichen Abhängigkeit aufnehmen, was sehr unübersichtlich ist. Eine natürliche Lösung wäre es, alle Abhängigkeiten in eine Klasse mit einem Namen wie „"ApplicationContext“ zu verschieben und dann diese als Konstruktorparameter zu übergeben. Dadurch kann PageManager an Klassen übergeben werden, die diesen benötigen, ohne die Zwischenklassen zu beeinträchtigen, die ihn nicht benötigen. Es ist jedoch immer noch ein Entwurfsproblem, dass „ApplicationContext“ hartcodierte Abhängigkeiten bei vielen nicht miteinander verknüpften Aktionen aufweist. Ein flexiblerer Ansatz besteht darin, ein Wörterbuch daraus zu erstellen, das Elemente für Verbraucher/Anbieter nachschlagen kann, die den korrekten Nachschlageschlüssel (d. h. ServiceKey) kennen. Dies ist das beliebte „service locator“-Entwurfsmuster, das wir aus der SPContext-API im klassischen SharePoint kennen. Bei ServiceScope wird diese Idee auf zweierlei Arten einen Schritt weiter geführt: Zunächst stellt es einen Mechanismus für die Bereichsdefinition bereit, sodass zwei unterschiedliche Seiten jeweils eine eindeutige PageManager-Instanz verwenden könnten, während weiterhin andere gemeinsame Abhängigkeiten gemeinsam verwendet werden. Außerdem kann ein ServiceKey eine Standardimplementierung der Abhängigkeit bereitstellen. Dies ist für die API-Stabilität in unserer modularen clientseitigen Umgebung wichtig: Angenommen, in Version 2.0 unserer Anwendung würde eine neue IDiagnosticTracing-Schnittstelle eingeführt, die von einer Komponente der Version 2.0 verwendet wird. Wenn die Version 2.0-Komponente von einer älteren 1.0-Anwendung geladen wird, würde ein Fehler auftreten. Dieser Fehler könnte behoben werden, indem jeder Verbraucher nach fehlenden Abhängigkeiten suchen und diesen Fall lösen muss, hierfür wären aber viele Überprüfungen erforderlich. Eine bessere Lösung besteht darin, sicherzustellen, dass immer eine Standardimplementierung vorhanden ist, vielleicht nur ein Testverhalten, damit Komponenten sich nicht darum kümmern müssen. Verwendung: ServiceScope-Instanzen werden durch Aufrufen von ServiceScope.startNewRoot() oder ServiceScope.startNewChild() erstellt. Sie befinden sich zunächst in einem „nicht abgeschlossenen“ Zustand, in dem provide() aufgerufen werden kann, um Dienstschlüssel zu registrieren, consume() ist jedoch verboten. Nachdem ServiceScope.finish() aufgerufen wurde, ist consume() zulässig, und provide() ist nun verboten. Durch diese Semantik wird sichergestellt, dass ServiceScope.consume() immer dasselbe Ergebnis für denselben Schlüssel zurückgibt und nicht von der Reihenfolge der Initialisierung abhängig ist. Außerdem können wir Ringabhängigkeiten unterstützen, ohne dass wir uns um unendliche Schleifen Gedanken machen müssen, wenn wir mit externen Komponenten arbeiten, die von Drittanbietern implementiert wurden. Um Fehler zu vermeiden, empfiehlt es sich immer, consume() innerhalb eines Rückrufs vom serviceScope.whenFinished() aufzurufen.


## <a name="constructor"></a>Konstruktor
PRIVAT - RUFEN SIE DIES NICHT AUS IHREM EIGENEN CODE AUF.

**Signatur:** _constructor(parent: [ServiceScope](../sp-core-library/servicescope.md));_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine





## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`consume(serviceKey)`](consume-servicescope.md)     | `public` | `T` | Komponenten sollten diese Funktion aufrufen, um eine Abhängigkeit zu nutzen, d. h. den Dienstschlüssel nachschlagen und die registrierte Dienstinstanz zurückgeben. Wenn die Instanz nicht gefunden werden kann, wird automatisch eine Standardinstanz erstellt und beim Stammdienstbereich registriert. |
|[`createAndProvide(serviceKey,simpleServiceClass)`](createandprovide-servicescope.md)     | `public` | `T` | Dies ist eine Abkürzungsfunktion, die dem Erstellen einer neuen Instanz von SimpleServiceClass entspricht und dann durch Aufruf von ServiceScope.provide() registriert wird. |
|[`createDefaultAndProvide(serviceKey)`](createdefaultandprovide-servicescope.md)     | `public` | `T` | Dies ist eine Abkürzungsfunktion, die die Standardimplementierung des angegebenen ServiceKey erstellt und ihn dann durch Aufrufen von ServiceScope.provide() registriert. |
|[`finish()`](finish-servicescope.md)     | `public` | `void` | Wenn ein ServiceScope zum ersten Mal gestartet wird, ist er ein "nicht beendeter" Zustand, in dem provide() zulässig ist, consume() aber nicht zulässig ist. Nach dem Aufrufen von finish() gefolgt von consume() ist consume() zulässig, provide() aber nicht. Dieser Formalismus beseitigt vollständig eine Anzahl von schwierigen Fehlern, z. B.: Scope2 ist ein untergeordnetes Element von Scope1 und Scope1 stellt Instanz A1 von Schnittstelle A bereit; Wenn jemand A1 aus Scope2 (über die Vererbung) nutzt, bevor Scope2.provide() mit A2 aufgerufen wird, gibt ein nachfolgender Aufruf von Scope2.consume() möglicherweise ein anderes Ergebnis als der vorherige Aufruf zurück, was für Entwickler sehr verwirrend wäre. |
|[`getParent()`](getparent-servicescope.md)     | `public` | [`ServiceScope`](../sp-core-library/servicescope.md) | Gibt das übergeordnete Element des aktuellen ServiceScope oder undefiniert zurück, wenn dies ein Stammbereich ist. |
|[`provide(serviceKey,service)`](provide-servicescope.md)     | `public` | `T` | ServiceScope.provide() wird zum Registrieren einer Implementierung der angegebenen serviceKey für den aktuellen Bereich verwendet. Dies kann nur verwendet werden, wenn der ServiceScope sich in einem „nicht abgeschlossenen“ Zustand befindet, d. h., bevor finish() aufgerufen wurde. |
|[`startNewChild()`](startnewchild-servicescope.md)     | `public` | [`ServiceScope`](../sp-core-library/servicescope.md) | Erstellt einen neuen ServiceScope, der ein untergeordnetes Element des aktuellen Bereichs ist. Für alle Schlüssel, die nicht explizit vom untergeordneten Bereich bereitgestellt werden, wird die übergeordnete Hierarchie berücksichtigt. |
|[`startNewRoot()`](startnewroot-servicescope.md)     | `public, static` | [`ServiceScope`](../sp-core-library/servicescope.md) | Erstellt einen neuen ServiceScope auf Stammebene. Nur Bereiche auf Stammebene können standardmäßige Implementierungen von ServiceKeys automatisch erstellen. |
|[`whenFinished(callback)`](whenfinished-servicescope.md)     | `public` | `void` | Das Aufrufen von ServiceScope.consume() vor dem Aufrufen von finish() ist ein Fehler. Die zuverlässigste Möglichkeit zum Schutz Ihrer Komponente vor diesem Fehler besteht darin, die consume()-Aufrufe innerhalb eines whenFinished()-Rückrufs auszuführen. Wenn der Dienstbereich bereits abgeschlossen ist, wird der Rückruf sofort ausgeführt; andernfalls wird er später nach Abschluss des Bereichs ausgeführt. |





