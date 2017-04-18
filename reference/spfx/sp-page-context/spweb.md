# <a name="spweb-class"></a>SPWeb-Klasse







Diese Klasse wird in erster Linie mit der PageContext-Klasse verwendet. Sie bietet kontextbezogene Informationen für die SharePoint-Website („Web), die die Seite hostet.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`absoluteUrl`     | `public` | `string` | _Schreibgeschützt._ Gibt die absolute URL für dieses SPWeb zurück. Beispiel: „https://example.com/sites/PubSite/SubWeb“ |
|`id`     | `public` | [`Guid`](../sp-core-library/guid.md) | _Schreibgeschützt._ Die GUID, die das SPWeb auf dem Server identifiziert. |
|`isAppWeb`     | `public` | `boolean` | _Schreibgeschützt._ Gibt „true“ zurück, wenn dieses SPWeb der Webcontainer für eine SPApp ist. |
|`language`     | `public` | `number` | _Schreibgeschützt._ Gibt den Gebietsschemabezeichner (Local Identifier, LCID) für die Standardsprache der Website zurück. Beispiel: 1033 steht für den Gebietsschemabzeichner für en-US. |
|`logoUrl`     | `public` | `string` | _Schreibgeschützt._ Gibt die absolute URL des websitelogos zurück. Beispiel: https://example.com/sites/PubSite/SubWeb/logo.jpg |
|`permissions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | _Schreibgeschützt._ Gibt das SPPermission-Objekt zurück, das den Satz von Berechtigungen darstellt, den der aktuelle Benutzer für die Interaktion mit dem Web hat. |
|`serverRelativeUrl`     | `public` | `string` | _Schreibgeschützt._ Gibt die serverbezogene URL für dieses SPWeb zurück. Beispiel: „/sites/PubSite/SubWeb“ |
|`templateName`     | `public` | `string` | _Schreibgeschützt._ Gibt den Namen der Websitedefinition oder der Websitevorlage zurück, die zum Erstellen der Website verwendet wurde. Beispiel: Beim Erstellen einer neuen Website auf SharePoint stellt „BLOG“ die Blogvorlage dar. |
|`title`     | `public` | `string` | _Schreibgeschützt._ Gibt den Titel des aktuellen SPWeb zurück. |







