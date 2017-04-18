# <a name="iodatauser-interface"></a>IODataUser-Schnittstelle







Stellt ein OData-SP.User-Objekt dar. Weitere Informationen zu diesem Objekt finden Sie in der MSDN-Dokumentation: https://msdn.microsoft.com/de-de/library/office/jj860569.aspx




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`Email`      | `string` | Beispiel: "jemand@example.com" |
|`Id`      | `number` |  |
|`IsSiteAdmin`      | `boolean` | Boolescher Wert, der angibt, ob der Benutzer ein Websitesammlungsadministrator ist. |
|`LoginName`      | `string` | Beispiel: "i:0#.w|domain\user" |
|`PrincipalType`      | `number` | Diese Aufzählung verfügt über ein FlagsAttribute-Attribut, das eine bitweise Kombination der Memberwerte zulässt. Keine: 0 User: 1 DistributionList: 2 SecurityGroup: 4 SharePointGroup: 8 All: 15 |
|`Title`      | `string` | Beispiel: "DOMAIN\user" |
|`UserId`      | `IODataUserId` | Ruft die Informationen des Benutzers einschließlich Bezeichner des Benutzernamens und Aussteller des Bezeichners des Benutzernamens ab. |






