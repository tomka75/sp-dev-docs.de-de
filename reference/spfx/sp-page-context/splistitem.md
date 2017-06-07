# <a name="splistitem-class"></a>SPListItem-Klasse







Diese Klasse wird in erster Linie mit der PageContext-Klasse verwendet. Sie bietet kontextbezogene Informationen für das SharePoint-Listenelement, das die Seite hostet.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`id`     | `public` | `number` | _Schreibgeschützt._ Die Zahl, die das SPListItem auf dem Server identifiziert. |
|`permissions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | _Schreibgeschützt._ Gibt das SPPermission-Objekt zurück, das den Satz von Berechtigungen darstellt, den der aktuelle Benutzer für die Interaktion mit dem Listenelement hat. |







