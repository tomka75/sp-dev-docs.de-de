# <a name="iwebpartpropertiesmetadata-interface"></a>IWebPartPropertiesMetadata-Schnittstelle







Diese Struktur wird verwendet, um Metadaten für Webparteigenschaften als Zeichenfolgenzuordnung zu IWebPartPropertyMetadata zu definieren. Der Schlüssel sollte ein JSON-Pfad zu der Eigenschaft in Webparteigenschaften sein. Der JSON-Pfad unterstützt die folgenden Operatoren: - Punkt . zum Auswählen von Objektelementen, z. B. person.name - Klammern [] für die Auswahl von Arrayelementen, z. B. person.photoURLs[0] - Sternchen in Klammern [*] für Arrayelementplatzhalter, z. B. person.websites[*]. Sie können Kombinationen aus diesen Operatoren erstellen, z. B. person.websites[*]url Wichtiger Hinweis: Es wird jeweils nur einen Platzhalter pro Pfad unterstützt. Beispiel: Angenommen, wir haben ein Webpart mit Eigenschaften vorliegen, die das folgende Schema aufweisen: { title: string; person: { name: string; bio: string; photoURLs: string[]; websites: { title: string; url: string; }[] } } Wir können die Metadaten für die gewünschten Eigenschaften wie folgt definieren: { 'person.bio': { isRichContent: true }, 'person.photoURLs[*]': { isImageSource: true }, 'person.websites[*].url': { isLink: true } } So werden die SharePoint-Server auf den Inhalt Ihrer Eigenschaften aufmerksam und führen Dienste wie z. B. Suchindizierung, Korrektur von Links usw. für die Daten aus. Für den Fall, dass einer der Werte von diesen Diensten aktualisiert werden muss, z. B. Linkkorrektur, wird der Eigenschaftenbehälter des Webparts automatisch aktualisiert.







## <a name="methods"></a>Methoden

| Methode       |  Rückgabewerte   | Beschreibung|
|:-------------|:-------|:-----------|
|[`index()`](__index-iwebpartpropertiesmetadata.md)      | `IWebPartPropertyMetadata` |  |




