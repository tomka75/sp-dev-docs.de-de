# <a name="iwebpartdata-interface"></a>IWebPartData-Schnittstelle







Diese Struktur stellt den serialisierten Zustand eines Webparts dar. Wenn die serialize()-API für ein Webpart aufgerufen wird, sollte die Ausgabe diese Struktur sein. Die Struktur des „properties“-Felds gehört dem Webpart und bezieht sich nur auf das Webpart. Jedes Webpart kann den Satz von Eigenschaften auswählen, der serialisiert werden soll.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`description`      | `string` | Definition: Webpartbeschreibung. Verwendung: Anzeigen der Beschreibung des Webparts. Erforderlich: nein Typ: Zeichenfolge Unterstützte Werte: Zeichenfolge mit der Beschreibung. Beispiel: „Text“ |
|`id`      | `string` | Definition: eindeutige Webpart-Typ-ID. Verwendung: Eindeutige Identifizierung eines Webparts. Erforderlich: Ja Typ: GUID Unterstützte Werte: beliebige GUID Beispiel: „dbef608d-3ad5-4f8f-b139-d916f2f0a294“ |
|`instanceId`      | `string` | Definition: eindeutige Instanz-ID des Webparts. Ein Webpart kann auf einer Seite mehrere Instanzen aufweisen. Diese ID muss über Zeit- und Seitengrenzen hinweg eindeutig sein. Verwendung: Wird vom Framework verwendet, um eine Instanz eines Webparts eindeutig zu identifizieren. Obligatorisch: ja Typ: Zeichenfolge Unterstützte Werte: eine eindeutige Zeichenfolge. Kann eine GUID oder ein anderes eindeutig identifizierbares Format sein. Beispiel: ["dbef608d-3ad5-4f8f-b139-d916f2f0a294"] Experimentell: Ja |
|`title`      | `string` | Definition: Webparttitel. Verwendung: Anzeigen des Namens des Webparts in der Toolbox, im Webpartkatalog und auf der Seite. Erforderlich: ja Typ: Zeichenfolge Unterstützte Werte: Zeichenfolge mit weniger als 100 Zeichen Beispiel: „Text“ |






