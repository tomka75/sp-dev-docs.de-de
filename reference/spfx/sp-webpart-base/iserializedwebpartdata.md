# <a name="iserializedwebpartdata-interface"></a>ISerializedWebPartData-Schnittstelle







Diese Struktur stellt den Teil des serialisierten Zustands eines Webparts dar, der vom Webpart gesteuert wird. Diese wird durch IWebPartData erweitert. Darin sind zusätzliche Daten enthalten, die vom Framework zu serialisierten Daten hinzugefügt werden.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`dataVersion`      | [`Version`](../sp-core-library/version.md) | Definition: Webpart-Datenversion. Beachten Sie, dass sich die Datenversion vom Versionsfeld im Manifest unterscheidet. Die Manifestversion wird zum Steuern der Versionsverwaltung des Webpartcodes verwendet, die Datenversion wird hingegen zum Steuern der Versionsverwaltung der serialisierten Daten des Webparts verwendet. Weitere Informationen finden Sie im dataVersion-Feld Ihres Webparts. Verwendung: Versionsverwaltung und Weiterentwicklung der serialisierten Daten des Webparts. Erforderlich: ja Typ: Version Unterstützte Werte: MAJOR.MINOR Beispiel: "1.0" |
|`properties`      | `any` | Definition: Webpartspezifische Eigenschaften. Jedes einzelne Webpart besitzt die Definition dieser Eigenschaften. Verwendung: Wird vom Webpart zum Verwalten seiner internen Metadaten und Konfigurationsdaten verwendet. Der Frameworkcode kommt nie in Kontakt mit diesen Eigenschaften. Erforderlich: ja Typ: beliebig Unterstützte Werte: beliebige, in einer Zeichenfolge darstellbare JSON-Objekthierarchie. Beispiel: { 'value': 'text value' } |
|`serverProcessedContent`      | [`ISerializedServerProcessedData`](../sp-webpart-base/iserializedserverprocesseddata.md) | Definition: Die Datensammlungen, die von serverseitigen Diensten wie Suchindex und Linkkorrektur verarbeitet werden können. |






