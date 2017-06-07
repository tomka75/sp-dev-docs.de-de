# <a name="splist-class"></a>SPList-Klasse







Diese Klasse wird in erster Linie mit der PageContext-Klasse verwendet. Sie bietet kontextbezogene Informationen für die SharePoint-Liste, die die Seite hostet.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`id`     | `public` | [`Guid`](../sp-core-library/guid.md) | _Schreibgeschützt._ Die GUID, die die SPList auf dem Server identifiziert. Diese Eigenschaft ist möglicherweise nicht definiert, wenn die Informationen nicht verfügbar sind. |
|`permissions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | _Schreibgeschützt._ Gibt das SPPermission-Objekt zurück, das den Satz von Berechtigungen darstellt, den der aktuelle Benutzer für die Interaktion mit der Liste hat. |
|`serverRelativeUrl`     | `public` | `string` | _Schreibgeschützt._ Gibt die serverbezogene URL für diese SPList an. Beispiel: "/sites/PubSite" |
|`title`     | `public` | `string` | _Schreibgeschützt._ Gibt den Titel für diese SPList zurück. |







