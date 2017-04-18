# <a name="iodatalist-interface"></a>IODataList-Schnittstelle







Stellt ein OData-SP.List-Objekt dar. Weitere Informationen zu diesem Objekt finden Sie in der MSDN-Dokumentation: https://msdn.microsoft.com/de-de/library/office/jj860569.aspx




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`BaseTemplate`      | `number` | Der Listendefinitionstyp, auf dem die Liste basiert. |
|`Created`      | `string` | Beispiel: "/Date(1453294804000)/" |
|`CurrentChangeToken`      | [`IODataChangeToken`](../sp-odata-types/iodatachangetoken.md) | Das Änderungstoken, das bei der Protokollierung der nächsten Änderung an der Liste verwendet wird. |
|`Description`      | `string` | Eine Beschreibung der Liste. |
|`EntityTypeName`      | `string` | Beispiel: "MyListTitleList" |
|`Hidden`      | `boolean` | Eine ausgeblendete Liste wird nicht auf der Seite zu Dokumenten und Listen, in der Schnellstartleiste, auf der Seite zum Ändern von Websiteinhalten oder der Seite zum Hinzufügen von Spalten als Option für Nachschlagefelder angezeigt. |
|`Id`      | `string` | Beispiel: "/Guid(9fb9199b-65f2-4a4a-b597-11d1a44422c1)/" |
|`LastItemDeletedDate`      | `string` | Beispiel: "/Date(1453294809000)/" |
|`LastItemModifiedDate`      | `string` | Beispiel: "/Date(1453294809000)/" |
|`ListItemEntityTypeFullName`      | `string` | Beispiel: "SP.Data.MyListTitleListItem" |
|`ParentWebUrl`      | `string` | Beispiel: "/sites/PubSite" |
|`TemplateFeatureId`      | `string` | Beispiel: "/Guid(22a9ef51-737b-4ff2-9346-694633fe4416)/" |
|`Title`      | `string` | Beispiel: "Pages" |






