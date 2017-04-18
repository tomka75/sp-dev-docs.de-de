# <a name="spsite-class"></a>SPSite-Klasse







Diese Klasse wird in erster Linie mit der PageContext-Klasse verwendet. Sie bietet kontextbezogene Informationen für die SharePoint-Websitesammlung („Website“), die die Seite hostet.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`absoluteUrl`     | `public` | `string` | _Schreibgeschützt._ Gibt die absolute URL für diese SPSite zurück. Beispiel: „https://example.com/sites/PubSite“ |
|`cdnPrefix`     | `public` | `string` | _Schreibgeschützt._ Gibt das Präfix des angegebenen CDN der Anwendung oder NULL zurück, wenn keines vorhanden ist. |
|`classification`     | `public` | `string` | _Schreibgeschützt._ Gibt die Klassifizierung der Website zurück. |
|`correlationId`     | `public` | [`Guid`](../sp-core-library/guid.md) | _Schreibgeschützt._ Gibt die Korrelations-ID zurück an die aktuelle Serveranforderung zurück. |
|`id`     | `public` | [`Guid`](../sp-core-library/guid.md) | _Schreibgeschützt._ Die GUID, die die SPSite auf dem Server identifiziert. |
|`isNoScriptEnabled`     | `public` | `boolean` | _Schreibgeschützt._ Gibt „true“ zurück, wenn für die SPSite isNoScript aktiviert wurde. |
|`recycleBinItemCount`     | `public` | `number` | _Schreibgeschützt._ Die Anzahl der Elemente im Papierkorb. |
|`serverRelativeUrl`     | `public` | `string` | _Schreibgeschützt._ Gibt die serverbezogene URL für diese SPSite an. Beispiel: „/sites/PubSite“ |
|`serverRequestPath`     | `public` | `string` | _Schreibgeschützt._ Gibt die serverRelativeUrl der ursprünglichen Anforderung zurück. Beispiel: „/teams/SPClientTest/SitePages/Home.aspx“ |
|`sitePagesEnabled`     | `public` | `boolean` | _Schreibgeschützt._ Gibt „true“ zurück, wenn für diese SPSite SitePages aktiviert sind. |







