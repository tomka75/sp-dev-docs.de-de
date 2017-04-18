# <a name="baseclientsidewebpart-tproperties-class"></a>BaseClientSideWebPart <TProperties>-Klasse



_Typparameter: `<TProperties>`_



Diese abstrakte Klasse implementiert die Basisfunktionen für ein clientseitigen Webpart. Jedes clientseitige Webpart muss von dieser Klasse erben. Zusammen mit der Basisfunktionalität stellt diese Klasse einige APIs bereit, die vom Webpart verwendet werden können. Diese APIs werden in zwei Kategorien unterteilt. Die erste Kategorie dieser APIs stellt Daten und Funktionen bereit. Beispiel: der Wepartkontext (d. h. this.context). Diese API sollte verwendet werden, um auf kontextbezogene Daten zuzugreifen, die für diese Webpartinstanz relevant sind. Die zweite Kategorie dieser APIs stellt eine Basisimplementierung für den Webpart-Lebenszyklus bereit und kann für eine aktualisierte Implementierung überschrieben werden. Die render()-API ist die einzige API, die zwingend von einem Webpart implementiert/überschrieben werden muss. Alle anderen Lebenszyklus-APIs verfügen über eine Basisimplementierung und können basierend auf den Anforderungen des Webparts überschrieben werden. Informationen zum Treffen der richtigen Entscheidung finden Sie in der Dokumentation der einzelnen APIs.


## <a name="constructor"></a>Konstruktor
Konstruktor für die BaseClientSideWebPart-Klasse. Wenn eine Unterklasse den Konstruktor überschreibt, muss er super() als erste Zeile des zugehörigen Konstruktors aufrufen. Es wird dringend empfohlen, dass das Webpart die OnInit-API verwendet, um alle Webpart-spezifischen Initialisierungen auszuführen. Die meisten Webpartfunktionen wie "this.context" und "this.properties" können nicht vor dem onInit-Teil des Webpart-Ladelebenszyklus verwendet werden. Beispiel: constructor() { super(); . . klassenspezifischer Konstruktorcode .. }

**Signatur:** _constructor();_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine


## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`accessibleTitle`     | `public` | `string` | Diese Eigenschaft verweist auf den Titel des Webparts, auf den zugegriffen werden kann und der für Bildschirmsprachausgaben zur Verfügung steht. Die Basisimplementierung gibt diesen Standardtitel im Manifest zurück. Webparts, die beschreibende Titel mit mehr Kontextinformationen bereitstellen möchten, müssen diese API außer Kraft setzen. |
|`canOpenPopupOnRender`     | `public` | `boolean` | _Schreibgeschützt._ Diese Eigenschaft gibt an, ob ein Webpart ein Popup beim anfänglichen Rendern öffnen kann. In einigen Umgebungen rendert der Host die Webparts häufig neu, sodass durch das Öffnen von Popups während des Renderns Popups wiederholt geöffnet werden und somit sehr benutzerunfreundlich sind. Beispiel: Die klassischen SharePoint-Seiten führen Postbacks aus, sodass eine Seite bei dem jedem Klick auf eine Schaltfläche erneut gerendert wird. Wenn ein Webpart ein Popup beim Rendern öffnen muss, sollte es diese API vor dem Öffnen des Popups verwenden. Wenn diese API "false" zurückgibt, darf das Webpart beim anfänglichen Rendern kein Popup öffnen. Einige der Webparts, die beim Rendern Popups öffnen, sind das Webpart zum Einbetten vom Dokumenten, das beim anfänglichen Rendern in der Dateiauswahl eingeblendet wird, und das Webpart zum Einbetten von Videos, dass beim anfänglichen Rendern den Eigenschaftenbereich (PropertyPane ) einblendet. |
|`context`     | `public` | [`IWebPartContext`](../sp-webpart-base/iwebpartcontext.md) | _Schreibgeschützt._ Diese Eigenschaft ist ein Zeiger auf den Webpartkontext. |
|`dataVersion`     | `public` | [`Version`](../sp-core-library/version.md) | _Schreibgeschützt._ Der Wert dieser Eigenschaft wird in den serialisierten Daten des Webparts gespeichert, um Entwicklern das Verwalten von Versionen des Webparts zu ermöglichen. Die Standardversion ist 1.0. |
|`description`     | `public` | `string` | _Schreibgeschützt._ Beschreibung des Webparts. |
|`disableReactivePropertyChanges`     | `public` | `boolean` | _Schreibgeschützt._ Diese Eigenschaft wird verwendet, um die PropertyPane-Interaktion des Webparts von "Reactive" auf "NonReactive" zu ändern. Das Standardverhalten ist "Reactive". "Reactive" impliziert, dass Änderungen am PropertyPane sofort an das Webpart übertragen werden und dass dem Benutzer Aktualisierungen sofort angezeigt werden. Dadurch erhält der Seitenersteller sofortiges Feedback und kann entscheiden, ob die neuen Konfigurationsänderungen beibehalten werden sollen. "NonReactive" impliziert, dass die Konfigurationsänderungen nur nach dem Klicken auf die PropertyPane-Schaltfläche "Übernehmen" an das Webpart übertragen werden. |
|`displayMode`     | `public` | [`DisplayMode`](../sp-core-library/displaymode.md) | _Schreibgeschützt._ Diese Eigenschaft ist der aktuelle Anzeigemodus des Webparts. |
|`domElement`     | `public` | `HTMLElement` | _Schreibgeschützt._ Diese Eigenschaft ist ein Zeiger auf das DOM-Stammelement des Webparts. Dies ist ein DIV-Element und enthält die gesamte DOM-Unterstruktur des Webparts. |
|`isRenderAsync`     | `public` | `boolean` | _Schreibgeschützt._ Gibt an, ob das Webpart im asynchronen Modus gerendert wird. Standardwert ist "false". Wenn das Webpart dieses Feld außer Kraft setzt, um "true" zurückzugeben, muss es die RenderCompleted-API aufrufen, nachdem das Rendern des Webparts abgeschlossen ist. |
|`previewImageUrl`     | `public` | `string` | Diese Eigenschaft zaigt auf das Vorschaubild für das Webpart. Die Basisimplementierung gibt nicht definiert zurück. Webparts, die eine gültige Vorschaubild-URL bereitstellen möchten, müssen diese API außer Kraft setzen. Die Vorschaubild-URL kann verwendet werden, um eine Vorschau des Webparts oder der Seite zu erstellen, auf der das Webpart vorhanden ist. |
|`properties`     | `public` | `TProperties` | _Schreibgeschützt._ Diese Eigenschaft ist der Zeiger auf den benutzerdefinierten Eigenschaftenbehälter des Webparts. |
|`propertiesMetadata`     | `public` | [`IWebPartPropertiesMetadata`](../sp-webpart-base/iwebpartpropertiesmetadata.md) | _Schreibgeschützt._ Diese Eigenschaft definiert Metadaten für den Webpart-Eigenschaftenbehälter. Die Metadaten können SharePoint dabei helfen, den Inhalt der Eigenschaften besser zu verstehen und relevante Dienste für die Daten auszuführen. |
|`renderedFromPersistedData`     | `public` | `boolean` | _Schreibgeschützt._ Diese Eigenschaft gibt an, ob das Webpart aus den gespeicherten Daten (serialisierter Zustand seit dem letzten Speichern des Webparts) gerendert wurde. Beispiel: Wenn das Webpart zum ersten Mal mithilfe der Toolbox hinzugefügt wird, ist der Wert "false". |
|`renderedOnce`     | `public` | `boolean` | _Schreibgeschützt._ Diese Eigenschaft gibt an, ob das Webpart einmal gerendert wurde. Nach dem erstmaligen Rendern ist der Wert dieser Eigenschaft immer "true". Bis ein erneutes vollständiges Rendern des Webparts erfolgt. |
|`title`     | `public` | `string` | _Schreibgeschützt._ Der Titel des Webparts |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`clearError()`](clearerror-baseclientsidewebpart.md)     | `protected` | `void` | Diese API sollte zum Löschen der Fehlermeldung im Anzeigebereich des Webparts verwendet werden. |
|[`getPropertyPaneConfiguration()`](getpropertypaneconfiguration-baseclientsidewebpart.md)     | `protected` | [`IPropertyPaneConfiguration`](../sp-webpart-base/ipropertypaneconfiguration.md) | Diese API wird verwendet, um die Konfiguration zum Erstellen des Eigenschaftenbereich für das Webpart zu erstellen. Wenn das Webpart PropertyPane für die Konfiguration verwenden möchte, muss diese API außer Kraft gesetzt werden, und das Webpart muss die Konfiguration für PropertyPane zurückgeben. |
|[`onAfterDeserialize(deserializedObject,dataVersion)`](onafterdeserialize-baseclientsidewebpart.md)     | `protected` | `TProperties` | Diese API wird aufgerufen, nachdem das Webpart für ein Objekt deserialisiert wurde – kurz vor dem Auffüllen des Eigenschaftenbehälters. Für die Standardimplementierung ist keine Aktion erforderlich. Ein Webpartentwickler kann diese API außer Kraft setzen, wenn das deserialisierte Objekt den Anfangszustand des Eigenschaftenbehälters nicht vollständig wiedergibt. So hat der Webpartentwickler die Möglichkeit, den Eigenschaftenbehälter direkt nach dem Deserialisieren der Daten für ein Obekt aufzufüllen. |
|[`onAfterPropertyPaneChangesApplied()`](onafterpropertypanechangesapplied-baseclientsidewebpart.md)     | `protected` | `void` | Diese API wird aufgerufen, nachdem die am PropertyPane vorgenommenen Änderungen angewendet werden, wenn der PropertyPane im nicht reaktiven Modus verwendet wird. Diese API wird nicht aufgerufen, wenn der PropertyPane im reaktiven Modus verwendet wird. |
|[`onBeforeSerialize()`](onbeforeserialize-baseclientsidewebpart.md)     | `protected` | `void` | Diese API wird aufgerufen, bevor das Webpart serialisiert wird. Für die Standardimplementierung ist keine Aktion erforderlich. Ein Webpartentwickler kann diese API überschreiben, wenn der Status des Webparts nicht vollständig im Eigenschaftenbehälter (d. h. this.properties) nicht vollständig wiedergegeben wird. Auf diese Weise können Webentwickler den Eigenschaftenbehälter direkt vor der Serialisierung aktualisieren. |
|[`onDisplayModeChanged(oldDisplayMode)`](ondisplaymodechanged-baseclientsidewebpart.md)     | `protected` | `void` | Diese API wird aufgerufen, wenn der Anzeigemodus eines Webparts geändert wird. Die standardmäßige Implementierung dieser API ruft die Webpart-Rendermethode auf, um das Webpart mit dem neuen Anzeigemodus erneut zu rendern. Wenn ein Webpartentwickler nicht möchte, dass bei einer Änderung des Anzeigemodus ein erneutes Rendern auftritt, kann er diese API überschreiben und bestimmte Updates für das Webpart-DOM ausführen, um den Anzeigemodus zu wechseln. |
|[`onDispose()`](ondispose-baseclientsidewebpart.md)     | `protected` | `void` | Diese API sollte zum Aktualisieren des Inhalts des PropertyPane verwendet werden. Diese API wird am Ende des Lebenszyklus des Webparts auf einer Seite aufgerufen. Sie sollte zum Entfernen lokaler Ressourcen (d. h. DOM-Elemente) verwendet werden, die das Webpart speichert. Diese API wird in Szenarien wie z. B. die Seitennavigation aufgerufen, der Host geht daher von einer Seite auf eine andere über und entfernt die Seite, die er verlässt. |
|[`onInit()`](oninit-baseclientsidewebpart.md)     | `protected` | `Promise<void>` | Diese API sollte überschrieben werden, um zeitintensive Operationen, z. B. das Abrufen von Daten von einem Remotedienst, vor dem ersten Rendern des Webparts durchzuführen. Die Ladeanzeige wird während der Lebensdauer dieser Methode angezeigt. Diese API wird nur einmal während des Lebenszyklus eines Webparts aufgerufen. |
|[`onPropertyPaneConfigurationComplete()`](onpropertypaneconfigurationcomplete-baseclientsidewebpart.md)     | `protected` | `void` | Diese API wird aufgerufen, wenn die Konfiguration im PropertyPane abgeschlossen ist. Sie wird in den folgenden Fällen aufgerufen: – Wenn CONFIGURATION_COMPLETE_TIMEOUT (der aktuelle Wert beträgt 5 Sekunden) nach der letzten Änderung abläuft. – Wenn der Benutzer auf die Schaltfläche 'x' (Schließen) klickt, bevor CONFIGURATION_COMPLETE_TIMEOUT abläuft. – Wenn der Benutzer auf „Anwenden“ klickt, bevor CONFIGURATION_COMPLETE_TIMEOUT abläuft. – Wenn der Benutzer Webparts wechselt, erhält das aktuelle Webpart dieses Ereignis. |
|[`onPropertyPaneConfigurationStart()`](onpropertypaneconfigurationstart-baseclientsidewebpart.md)     | `protected` | `void` | Diese API wird aufgerufen, wenn die Konfiguration im PropertyPane beginnt. Sie wird in den folgenden Fällen aufgerufen: – Wenn der PropertyPane geöffnet wird. – Wenn der Benutzer Webparts wechselt, ruft das neue Webpart dieses Ereignis ab. |
|[`onPropertyPaneFieldChanged(propertyPath,oldValue,newValue)`](onpropertypanefieldchanged-baseclientsidewebpart.md)     | `protected` | `void` | Diese API wird nach dem Aktualisieren des neuen Werts der Eigenschaft im Eigenschaftenbehälter aufgerufen, wenn der PropertyPane im reaktiven Modus verwendet wird. Die grundlegende Implementierung dieser API rendert das Webpart erneut. |
|[`onPropertyPaneRendered()`](onpropertypanerendered-baseclientsidewebpart.md)     | `protected` | `void` | Diese API wird aufgerufen, wenn der PropertyPane gerendert wird. Aus der Perspektive des Frameworks sollte dieser Ereignishandler nicht übergeben und ausgelöst werden. Diese API sollte als veraltet markiert und dann im Rahmen einer Umgestaltung entfernt werden. |
|[`render()`](render-baseclientsidewebpart.md)     | `protected` | `void` | Diese API wird aufgerufen, um das Webpart zu rendern. Es gibt keine grundlegende Implementierung dieser API, und das Webpart muss diese API überschreiben. |
|[`renderCompleted()`](rendercompleted-baseclientsidewebpart.md)     | `protected` | `void` | Diese API sollte von Webparts aufgerufen werden, die ein asynchrones Rendering durchführen. Diese Webparts müssen die IsRenderAsync-API überschreiben und „true“ zurückgeben. Ein Beispiel hierfür sind Webparts, die Inhalte in einem IFrame rendern. Das Webpart initiiert die IFrame-Darstellung in der render()-API, aber das tatsächliche Rendern wird erst abgeschlossen, nachdem der Ladevorgang des IFrame abgeschlossen ist. |
|[`renderError(error)`](rendererror-baseclientsidewebpart.md)     | `protected` | `void` | Diese API sollte zum Rendern einer Fehlermeldung im Anzeigebereich des Webparts verwendet werden. Protokolliert auch die Fehlermeldung mithilfe der Ablaufverfolgungsprotokollierung. |





