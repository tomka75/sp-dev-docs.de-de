# <a name="iodataweb-interface"></a>IODataWeb-Schnittstelle







Stellt ein OData-SP.Web-Objekt dar. Weitere Informationen zu diesem Objekt finden Sie in der MSDN-Dokumentation: https://msdn.microsoft.com/de-de/library/office/jj860569.aspx




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`Created`      | `string` | Ruft einen Wert ab, der angibt, wann die Website erstellt wurde. Beispiel: "/Date(2016,0,20,12,58,7,0)/" |
|`CurrentChangeToken`      | [`IODataChangeToken`](../sp-odata-types/iodatachangetoken.md) | Steht für den eindeutigen sequenziellen Ort einer Änderung innerhalb des Änderungsprotokolls. |
|`CustomMasterUrl`      | `string` | Ruft die URL für eine benutzerdefinierte Gestaltungsvorlagendatei ab, die auf die Website anzuwenden ist, oder legt diese URL fest. Beispiel: "/sites/PubSite/_catalogs/masterpage/seattle.master" |
|`Description`      | `string` | Dient zum Abrufen oder Festlegen der Beschreibung der Website. |
|`Id`      | `string` | Ruft einen Wert ab, der den Websitebezeichner für die Website angibt. Beispiel: "/Guid(92ea328e-9f50-49a6-9da5-2f2dd5577041)/" |
|`IsMultilingual`      | `boolean` | Wert, der darstellt, ob das Web |
|`Language`      | `number` | Ruft einen Wert ab, der die LCID für die Sprache angibt, die auf der Website verwendet wird. Beispiel: 1033 |
|`LastItemModifiedDate`      | `string` | Ruft einen Wert ab, der angibt, wann ein Element in der Website zuletzt geändert wurde. Beispiel: "/Date(1453618828000)/" |
|`MasterUrl`      | `string` | Dient zum Abrufen oder Festlegen der URL der Gestaltungsvorlage, die für die Website verwendet wird. Beispiel: "/sites/PubSite/_catalogs/masterpage/seattle.master" |
|`NoCrawl`      | `boolean` | Bestimmt, ob ein bestimmtes Web per Suche durchforstet wird. |
|`QuickLaunchEnabled`      | `boolean` | Dient zum Festlegen oder Abrufen eines Werts, der angibt, ob der Schnellstartbereich auf der Website aktiviert ist. |
|`RecycleBinEnabled`      | `boolean` | Dient zum Festlegen oder Abrufen eines Werts, der bestimmt, ob der Papierkorb für die Website aktiviert ist. |
|`ServerRelativeUrl`      | `string` | Dient zum Festlegen oder Abrufen der Server-relativen URL für die Website. Beispiel: "/sites/PubSite" |
|`SiteLogoUrl`      | `string` | Ruft die URL für das Logo dieser bestimmten Website ab. |
|`Title`      | `string` | Der Titel des Webs. |
|`UIVersion`      | `number` | Dient zum Festlegen oder Abrufen der Benutzeroberflächenversion der Website. Beispiel: 15 |
|`Url`      | `string` | Ruft die absolute URL für die Website ab. Beispiel: "http://example.com/sites/PubSite" |
|`WebTemplate`      | `string` | Ruft den Namen der Websitedefinition oder Websitevorlage ab, die zum Erstellen der Website verwendet wurde. Beispiel: "BLANKINTERNET" |






