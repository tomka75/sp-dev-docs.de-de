# <a name="sp-webpart-base-module"></a>sp-webpart-base-Modul



## <a name="classes"></a>Klassen

| Klasse    |  Beschreibung |
|:-------------|:---------------|
| [`BaseClientSideWebPart`](./sp-webpart-base/baseclientsidewebpart.md)     | Diese abstrakte Klasse implementiert die Basisfunktionen für ein clientseitiges Webpart. Jedes clientseitige Webpart muss von dieser Klasse erben. Zusammen mit der Basisfunktionalität stellt diese Klasse einige APIs bereit, die vom Webpart verwendet werden können. Diese APIs werden in zwei Kategorien unterteilt. Die erste Kategorie dieser APIs stellt Daten und Funktionen bereit. Beispiel: der Wepartkontext (d. h. this.context). Diese API sollte verwendet werden, um auf kontextbezogene Daten zuzugreifen, die für diese Webpartinstanz relevant sind. Die zweite Kategorie dieser APIs stellt eine Basisimplementierung für den Webpart-Lebenszyklus bereit und kann für eine aktualisierte Implementierung überschrieben werden. Die render()-API ist die einzige API, die zwingend von einem Webpart implementiert/überschrieben werden muss. Alle anderen Lebenszyklus-APIs verfügen über eine Basisimplementierung und können basierend auf den Anforderungen des Webparts überschrieben werden. Informationen zum Treffen der richtigen Entscheidung finden Sie in der Dokumentation der einzelnen APIs. |



## <a name="interfaces"></a>Schnittstellen

| Schnittstelle    |  Beschreibung |
|:-------------|:---------------|
| [`IClientSideWebPartStatusRenderer`](./sp-webpart-base/iclientsidewebpartstatusrenderer.md)   | Die Schnittstelle, die von einer Komponente implementiert wird, die den Ladeindikator und Fehlermeldungen für ein Webpart anzeigen soll.  |
| [`IPlaceholderProps`](./sp-webpart-base/iplaceholderprops.md)   | Zum Anzeigen eines Platzhalters bei keinem oder temporärem Inhalt verwendet. Schaltfläche ist optional.  |
| [`IPlaceholderSpinnerProps`](./sp-webpart-base/iplaceholderspinnerprops.md)   | Schnittstelle für Eigenschaften zum Anzeigen des Ladedrehfelds im Webpart-Anzeigebereich.  |
| [`IPropertyPaneButtonProps`](./sp-webpart-base/ipropertypanebuttonprops.md)   | Eigenschaften der PropertyPane-Schaltfläche.  |
| [`IPropertyPaneCheckboxProps`](./sp-webpart-base/ipropertypanecheckboxprops.md)   | PropertyPane-CheckBox-Komponenteneigenschaften.  |
| [`IPropertyPaneChoiceGroupOption`](./sp-webpart-base/ipropertypanechoicegroupoption.md)   | PropertyPane-ChoiceGroup-Optionseigenschaften.  |
| [`IPropertyPaneChoiceGroupProps`](./sp-webpart-base/ipropertypanechoicegroupprops.md)   | PropertyPane-ChoiceGroup-Eigenschaften.  |
| [`IPropertyPaneConfiguration`](./sp-webpart-base/ipropertypaneconfiguration.md)   | Webpart-Konfigurationseinstellungen  |
| [`IPropertyPaneCustomFieldProps`](./sp-webpart-base/ipropertypanecustomfieldprops.md)   | PropertyPane CustomPropertyField-Eigenschaften  |
| [`IPropertyPaneDropdownOption`](./sp-webpart-base/ipropertypanedropdownoption.md)   | PropertyPane-Dropdown-Optionen.  |
| [`IPropertyPaneDropdownProps`](./sp-webpart-base/ipropertypanedropdownprops.md)   | PropertyPane-Dropdown-Komponenteneigenschaften.  |
| [`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)   | PropertyPane-Feld.  |
| [`IPropertyPaneGroup`](./sp-webpart-base/ipropertypanegroup.md)   | PropertyPane-Gruppe. Gruppe ist Teil der PropertyPanePage.  |
| [`IPropertyPaneLabelProps`](./sp-webpart-base/ipropertypanelabelprops.md)   | PropertyPaneLabel-Komponenteneigenschaften.  |
| [`IPropertyPaneLinkProps`](./sp-webpart-base/ipropertypanelinkprops.md)   | PropertyPaneLink-Komponenteneigenschaften.  |
| [`IPropertyPanePage`](./sp-webpart-base/ipropertypanepage.md)   | PropertyPanePage-Schnittstelle.  |
| [`IPropertyPanePageHeader`](./sp-webpart-base/ipropertypanepageheader.md)   | PropertyPane-Kopfzeile. Diese Kopfzeile ist für alle Seiten identisch.  |
| [`IPropertyPaneSliderProps`](./sp-webpart-base/ipropertypanesliderprops.md)   | PropertyPaneSliderProps-Komponenteneigenschaften.  |
| [`IPropertyPaneTextFieldProps`](./sp-webpart-base/ipropertypanetextfieldprops.md)   | PropertyPaneTextField-Komponenteneigenschaften.  |
| [`IPropertyPaneToggleProps`](./sp-webpart-base/ipropertypanetoggleprops.md)   | PropertyPaneToggle-Komponenteneigenschaften.  |
| [`ISerializedServerProcessedData`](./sp-webpart-base/iserializedserverprocesseddata.md)   | Enthält Datensammlungen, die von serverseitigen Diensten wie Suchindex und Linkkorrektur verarbeitet werden können.  |
| [`ISerializedWebPartData`](./sp-webpart-base/iserializedwebpartdata.md)   | Diese Struktur stellt den Teil des serialisierten Zustands eines Webparts dar, der vom Webpart gesteuert wird. Diese wird durch IWebPartData erweitert. Darin sind zusätzliche Daten enthalten, die vom Framework zu serialisierten Daten hinzugefügt werden.  |
| [`IWebPartContext`](./sp-webpart-base/iwebpartcontext.md)   | Die grundlegende Kontextschnittstelle für clientseitige Webparts.  |
| [`IWebPartData`](./sp-webpart-base/iwebpartdata.md)   | Diese Struktur stellt den serialisierten Zustand eines Webparts dar. Wenn die serialize()-API für ein Webpart aufgerufen wird, sollte die Ausgabe diese Struktur sein. Die Struktur des „properties“-Felds gehört dem Webpart und bezieht sich nur auf das Webpart. Jedes Webpart kann den Satz von Eigenschaften auswählen, der serialisiert werden soll.  |
| [`IWebPartPropertiesMetadata`](./sp-webpart-base/iwebpartpropertiesmetadata.md)   | Diese Struktur wird verwendet, um Metadaten für Webparteigenschaften als Zeichenfolgenzuordnung zu IWebPartPropertyMetadata zu definieren. Der Schlüssel sollte ein JSON-Pfad zu der Eigenschaft in Webparteigenschaften sein. Der JSON-Pfad unterstützt die folgenden Operatoren: - Punkt . zum Auswählen von Objektelementen, z. B. person.name - Klammern [] für die Auswahl von Arrayelementen, z. B. person.photoURLs[0] - Sternchen in Klammern [*] für Arrayelementplatzhalter, z. B. person.websites[*]. Sie können Kombinationen aus diesen Operatoren erstellen, z. B. person.websites[*]url Wichtiger Hinweis: Es wird jeweils nur einen Platzhalter pro Pfad unterstützt. Beispiel: Angenommen, wir haben ein Webpart mit Eigenschaften vorliegen, die das folgende Schema aufweisen: { title: string; person: { name: string; bio: string; photoURLs: string[]; websites: { title: string; url: string; }[] } } Wir können die Metadaten für die gewünschten Eigenschaften wie folgt definieren: { 'person.bio': { isRichContent: true }, 'person.photoURLs[*]': { isImageSource: true }, 'person.websites[*].url': { isLink: true } } So werden die SharePoint-Server auf den Inhalt Ihrer Eigenschaften aufmerksam und führen Dienste wie z. B. Suchindizierung, Korrektur von Links usw. für die Daten aus. Für den Fall, dass einer der Werte von diesen Diensten aktualisiert werden muss, z. B. Linkkorrektur, wird der Eigenschaftenbehälter des Webparts automatisch aktualisiert.  |



## <a name="functions"></a>Funktionen

| Funktion     | Rückgabewerte | Beschreibung |
|:-------------|:------|:---------------|
| [`PropertyPaneButton(targetProperty,properties)`](./sp-webpart-base/propertypanebutton.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneButtonProps`](./sp-webpart-base/ipropertypanebuttonprops.md)>  | Hilfsmethode zum Erstellen einer Schaltfläche im PropertyPane.  |
| [`PropertyPaneCheckbox(targetProperty,properties)`](./sp-webpart-base/propertypanecheckbox.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneCheckboxProps`](./sp-webpart-base/ipropertypanecheckboxprops.md)>  | Hilfsmethode zum Erstellen eines Kontrollkästchens im PropertyPane.  |
| [`PropertyPaneChoiceGroup(targetProperty,properties)`](./sp-webpart-base/propertypanechoicegroup.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneChoiceGroupProps`](./sp-webpart-base/ipropertypanechoicegroupprops.md)>  | Hilfsmethode zum Erstellen einer Auswahlgruppe im PropertyPane.  |
| [`PropertyPaneDropdown(targetProperty,properties)`](./sp-webpart-base/propertypanedropdown.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneDropdownProps`](./sp-webpart-base/ipropertypanedropdownprops.md)>  | Hilfsmethode zum Erstellen eines Dropdowns im PropertyPane.  |
| [`PropertyPaneHorizontalRule(properties)`](./sp-webpart-base/propertypanehorizontalrule.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<void>  | Hilfsmethode zum Erstellen einer horizontalen Regel im PropertyPane.  |
| [`PropertyPaneLabel(targetProperty,properties)`](./sp-webpart-base/propertypanelabel.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneLabelProps`](./sp-webpart-base/ipropertypanelabelprops.md)>  | Hilfsmethode zum Erstellen einer Beschriftung im PropertyPane.  |
| [`PropertyPaneLink(targetProperty,properties)`](./sp-webpart-base/propertypanelink.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneLinkProps`](./sp-webpart-base/ipropertypanelinkprops.md)>  | Hilfsmethode zum Erstellen eines Links im PropertyPane.  |
| [`PropertyPaneSlider(targetProperty,properties)`](./sp-webpart-base/propertypaneslider.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneSliderProps`](./sp-webpart-base/ipropertypanesliderprops.md)>  | Hilfsmethode zum Erstellen eines Schiebereglers im PropertyPane.  |
| [`PropertyPaneTextField(targetProperty,properties)`](./sp-webpart-base/propertypanetextfield.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneTextFieldProps`](./sp-webpart-base/ipropertypanetextfieldprops.md)>  | Hilfsmethode zum Erstellen eines TextField im PropertyPane.  |
| [`PropertyPaneToggle(targetProperty,properties)`](./sp-webpart-base/propertypanetoggle.md) |[`IPropertyPaneField`](./sp-webpart-base/ipropertypanefield.md)<[`IPropertyPaneToggleProps`](./sp-webpart-base/ipropertypanetoggleprops.md)>  | Hilfsmethode zum Erstellen einer Umschaltfläche im PropertyPane.  |


## <a name="enumerations"></a>Enumerationen

| Enumeration      | Beschreibung|
|:-----------|:------------|
|[`PropertyPaneButtonType`](./sp-webpart-base/propertypanebuttontype.md)    | Aufzählung für alle unterstützten Schaltflächentypen. |
|[`PropertyPaneFieldType`](./sp-webpart-base/propertypanefieldtype.md)    | Aufzählung für alle unterstützten PropertyPane-Feldtypen. Namen sollten mit denen in  office-ui-fabric-react konsistent sein, achten Sie darauf, dass Sie die Groß-und Kleinschreibung ordnungsgemäß verwenden. |




