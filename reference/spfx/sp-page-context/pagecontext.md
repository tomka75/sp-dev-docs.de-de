# <a name="pagecontext-class"></a>PageContext-Klasse







Der Seitenkontext bietet Standarddefinitionen für allgemeine SharePoint-Objekte, die gemeinsam von der clientseitigen Anwendung, den Webparts und anderen Komponenten verwendet werden. In der Regel werden die Daten über REST-Abfragen beim Navigieren zu einer neuen Seite abgerufen, sie können jedoch auch vorab vom Webserver geladen werden oder aus einem benutzerdefinierten Anwendungscache aufgefüllt werden.


## <a name="constructor"></a>Konstruktor


**Signatur:** _constructor(serviceScope: [ServiceScope](../sp-core-library/servicescope.md));_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine


## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`cultureInfo`     | `public` | [`CultureInfo`](../sp-page-context/cultureinfo.md) | _Schreibgeschützt._ Sie stellt Gebietsschemainformationen für den aktuellen Benutzer der Anwendung bereit. Diese Klasse wird in erster Linie mit der PageContext-Klasse verwendet. |
|`isInitialized`     | `public` | `boolean` | _Schreibgeschützt._ Gibt zurück, ob der PageContext initialisiert wurde. |
|`legacyPageContext`     | `public` | `any` | _Schreibgeschützt._ Diese Eigenschaft wird zur Erleichterung der Migration von Legacycode bereitgestellt. Sie gibt ein JavaScript-Objekt zurück, dessen Inhalt der _spPageContextInfo-Fenstervariablen von klassischen Seiten ähnlich ist. Der Inhalt dieser Variablen kann sich in zukünftigen Versionen von SharePoint ändern. Für neue Projekte wird stattdessen die Verwendung der Framework-APIs empfohlen, da diese dokumentiert sind und eine zuverlässige Abwärtskompatibilität bieten. |
|`list`     | `public` | [`SPList`](../sp-page-context/splist.md) | _Schreibgeschützt._ Kontextbezogene Informationen für die SharePoint-Liste, die die Seite hostet. Wenn der aktuellen Seite keine Liste zugeordnet ist, ist diese Eigenschaft nicht definiert. |
|`listItem`     | `public` | [`SPListItem`](../sp-page-context/splistitem.md) | _Schreibgeschützt._ Kontextbezogene Informationen für das SharePoint-Listenelement, das die Seite hostet. Wenn der aktuellen Seite kein Listenelement zugeordnet ist, ist diese Eigenschaft nicht definiert. |
|`serviceKey`     | `public` | [`ServiceKey`](../sp-core-library/servicekey.md)<[`PageContext`](../sp-page-context/pagecontext.md)> | Der Diensschlüssel für PageContext. |
|`site`     | `public` | [`SPSite`](../sp-page-context/spsite.md) | _Schreibgeschützt._ Kontextbezogene Informationen für die SharePoint-Websitesammlung („Website“), die die Seite hostet. |
|`user`     | `public` | [`SPUser`](../sp-page-context/spuser.md) | _Schreibgeschützt._ Sie bietet kontextbezogene Informationen für den SharePoint-Benutzer, der auf die Seite zugreift. Diese Klasse wird in erster Linie mit der PageContext-Klasse verwendet. |
|`web`     | `public` | [`SPWeb`](../sp-page-context/spweb.md) | _Schreibgeschützt._ Kontextbezogene Informationen für die SharePoint-Website („Web“), die die Seite hostet. |







