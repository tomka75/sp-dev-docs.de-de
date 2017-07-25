<span data-ttu-id="14e97-p101">Diese Struktur wird verwendet, um Metadaten für Webparteigenschaften als Zeichenfolgenzuordnung zu IWebPartPropertyMetadata zu definieren. Der Schlüssel sollte ein JSON-Pfad zu der Eigenschaft in Webparteigenschaften sein. Der JSON-Pfad unterstützt die folgenden Operatoren: - Punkt . zum Auswählen von Objektelementen, z. B. person.name - Klammern [] für die Auswahl von Arrayelementen, z. B. person.photoURLs[0] - Sternchen in Klammern [*] für Arrayelementplatzhalter, z. B. person.websites[*]. Sie können Kombinationen aus diesen Operatoren erstellen, z. B. person.websites[*]url Wichtiger Hinweis: Es wird jeweils nur einen Platzhalter pro Pfad unterstützt. Beispiel: Angenommen, wir haben ein Webpart mit Eigenschaften vorliegen, die das folgende Schema aufweisen: { title: string; person: { name: string; bio: string; photoURLs: string[]; websites: { title: string; url: string; }[] } } Wir können die Metadaten für die gewünschten Eigenschaften wie folgt definieren: { 'person.bio': { isRichContent: true }, 'person.photoURLs[*]': { isImageSource: true }, 'person.websites[*].url': { isLink: true } } So werden die SharePoint-Server auf den Inhalt Ihrer Eigenschaften aufmerksam und führen Dienste wie z. B. Suchindizierung, Korrektur von Links usw. für die Daten aus. Für den Fall, dass einer der Werte von diesen Diensten aktualisiert werden muss, z. B. Linkkorrektur, wird der Eigenschaftenbehälter des Webparts automatisch aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="14e97-p101">This structure is used to define metadata for web part propeties as a map of string to IWebPartPropertyMetadata The key should be a json path to the property in web part propeties. The json path supports the following operators: - Dot . for selecting object members e.g. person.name - Brackets [] for selecting array items e.g. person.photoURLs[0] - Bracketed asterisk [*] for array elements wildcard e.g. person.websites[*]. You can make combinations of these operators e.g. person.websites[*].url Important Note: Only one wildcard per path is supported. Example: Let's assume we have a web part with properties that have the following schema: { title: string; person: { name: string; bio: string; photoURLs: string[]; websites: { title: string; url: string; }[] } } We can define the metadata for the desired properties as following: { 'person.bio': { isRichContent: true }, 'person.photoURLs[*]': { isImageSource: true }, 'person.websites[*].url': { isLink: true } } This will make SharePoint servers aware of the content of your properties and run services such as search indexing, link fix-up, etc on the data. In case any of the values needs to update by these services, e.g link fix-up, the web part property bag is automatically updated.</span></span>







Diese Struktur wird verwendet, um Metadaten für Webparteigenschaften als Zeichenfolgenzuordnung zu IWebPartPropertyMetadata zu definieren. Der Schlüssel sollte ein JSON-Pfad zu der Eigenschaft in Webparteigenschaften sein. Der JSON-Pfad unterstützt die folgenden Operatoren: - Punkt . zum Auswählen von Objektelementen, z. B. person.name - Klammern [] für die Auswahl von Arrayelementen, z. B. person.photoURLs[0] - Sternchen in Klammern [*] für Arrayelementplatzhalter, z. B. person.websites[*]. Sie können Kombinationen aus diesen Operatoren erstellen, z. B. person.websites[*]url Wichtiger Hinweis: Es wird jeweils nur einen Platzhalter pro Pfad unterstützt. Beispiel: Angenommen, wir haben ein Webpart mit Eigenschaften vorliegen, die das folgende Schema aufweisen: { title: string; person: { name: string; bio: string; photoURLs: string[]; websites: { title: string; url: string; }[] } } Wir können die Metadaten für die gewünschten Eigenschaften wie folgt definieren: { 'person.bio': { isRichContent: true }, 'person.photoURLs[*]': { isImageSource: true }, 'person.websites[*].url': { isLink: true } } So werden die SharePoint-Server auf den Inhalt Ihrer Eigenschaften aufmerksam und führen Dienste wie z. B. Suchindizierung, Korrektur von Links usw. für die Daten aus. Für den Fall, dass einer der Werte von diesen Diensten aktualisiert werden muss, z. B. Linkkorrektur, wird der Eigenschaftenbehälter des Webparts automatisch aktualisiert.







## <a name="methods"></a><span data-ttu-id="14e97-107">Methoden</span><span class="sxs-lookup"><span data-stu-id="14e97-107">Methods</span></span>

| <span data-ttu-id="14e97-108">Methode</span><span class="sxs-lookup"><span data-stu-id="14e97-108">Method</span></span>       |  <span data-ttu-id="14e97-109">Rückgabewerte</span><span class="sxs-lookup"><span data-stu-id="14e97-109">Returns</span></span>   | <span data-ttu-id="14e97-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="14e97-110">Description</span></span>|
|:-------------|:-------|:-----------|
|[`index()`](__index-iwebpartpropertiesmetadata.md)      | `IWebPartPropertyMetadata` |  |




