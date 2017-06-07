# <a name="sppermission-class"></a>SPPermission-Klasse







Diese Klasse kann verwendet werden, um festzustellen, ob der aktuelle Benutzer über einen angeforderten Satz von Berechtigungen verfügt. Gibt die integrierten Berechtigungen an, die in SharePoint Foundation verfügbar sind. Abgeleitet von OneDriveWeb/ODBNext/odsp-shared https://msdn.microsoft.com/de-de/library/microsoft.sharepoint.spbasepermissions.aspx


## <a name="constructor"></a>Konstruktor


**Signatur:** _constructor(value: [IODataBasePermission](../sp-odata-types/iodatabasepermission.md));_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine


## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`addAndCustomizePages`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | HTML-Seiten oder Webpartseiten hinzufügen, ändern oder löschen und die Website mithilfe eines Editors bearbeiten, der mit SharePoint Foundation kompatibel ist. |
|`addDelPrivateWebParts`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Persönliche Webparts auf einer Webpartseite hinzufügen oder entfernen. |
|`addListItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Listen Elemente hinzufügen, Dokumentbibliotheken Dokumente hinzufügen und Webdiskussionskommentare hinzufügen. |
|`applyStyleSheets`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Ein Stylesheet (CSS-Datei) auf die Website anwenden. |
|`applyThemeAndBorder`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Ein Design oder Rahmen auf die ganze Website anwenden. |
|`approveItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Eine Nebenversion eines Listenelements oder Dokuments genehmigen. |
|`browseDirectories`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Dateien und Ordner in einer Website mithilfe von Microsoft Office SharePoint Designer 2007 und WebDAV-Schnittstellen aufzählen. |
|`browserUserInfo`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Informationen über Websitebenutzer anzeigen. |
|`cancelCheckout`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Ein Dokument, das für einen anderen Benutzer ausgecheckt ist, verwerfen oder einchecken. |
|`createAlerts`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | E-Mail-Warnungen erstellen. |
|`createGroups`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Eine Gruppe von Benutzern erstellen, die überall in der Websitesammlung verwendet werden kann. |
|`createSSCSite`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Eine Website mit Self-Service Site Creation erstellen. |
|`deleteListItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Elemente aus einer Liste, Dokumente aus einer Dokumentbibliothek und Webdiskussionskommentare in Dokumenten löschen. |
|`deleteVersions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Ältere Versionen eines Listenelements oder Dokuments löschen. |
|`editListItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Elemente in Listen, Dokumente in Dokumentbibliotheken und Webdiskussionskommentare in Dokumenten bearbeiten sowie Webpartseiten in Dokumentbibliotheken anpassen. |
|`editMyUserInfo`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Ermöglicht Benutzern das Ändern ihrer eigenen Benutzerinformationen, z. B. Hinzufügen eines Bildes. |
|`emptyMask`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Verfügt über keine Berechtigungen für die Website. Nicht über die Benutzeroberfläche verfügbar. |
|`enumeratePermissions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Berechtigungen für die Website, die Liste, den Ordner, das Dokument oder das Listenelement auflisten. |
|`fullMask`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Verfügt über alle Berechtigungen für die Website. Nicht über die Benutzeroberfläche verfügbar. |
|`layoutsPage`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Sie möchten die Layoutseite anzeigen? |
|`manageAlerts`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Benachrichtigungen für alle Benutzer der Website verwalten. |
|`manageLists`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Listen erstellen oder löschen, Spalten einer Liste erstellen oder löschen und öffentliche Ansichten einer Liste hinzufügen oder löschen. |
|`managePermissions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Berechtigungsstufen für die Website erstellen und ändern, und Benutzern und Gruppen Berechtigungen zuweisen. |
|`managePersonalViews`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Persönliche Ansichten von Listen erstellen, ändern und löschen. |
|`manageSubwebs`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Unterwebsites wie Teamwebsites, Besprechungsarbeitsbereich-Websites und Dokumentarbeitsbereich-Websites erstellen. |
|`manageWeb`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Ermöglicht das Ausführen aller Verwaltungsaufgaben für die Website sowie die Verwaltung des Inhalts. Eigenschaften von Features im Bereich der Website über das Objektmodell oder die Benutzeroberfläche (UI) aktivieren, deaktivieren oder bearbeiten. Wenn diese für die Stammwebsite einer Websitesammlung gewährt werden, aktivieren, deaktivieren oder bearbeiten Sie die Eigenschaften der Features im Bereich der Website über das Objektmodell. Um zu der Seite mit den Features der Websitesammlung zu navigieren und die Features im Bereich der Websitesammlung über die Benutzeroberfläche zu aktivieren oder zu deaktivieren, müssen Sie ein Websitesammlungsadministrator sein. |
|`open`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Ermöglicht Benutzern das Öffnen einer Website, einer Liste oder eines Ordners für den Zugriff auf im Container enthaltene Elemente. |
|`openItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Die Quelle von Dokumenten mit serverseitigem Dateihandler anzeigen. |
|`updatePersonalWebParts`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Webparts aktualisieren, um personalisierte Informationen anzuzeigen. |
|`useClientIntegration`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Features zum Starten von Clientanwendungen verwenden. Andernfalls müssen Benutzer lokal an Dokumenten arbeiten und die Änderungen hochladen. |
|`useRemoteAPIs`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | SOAP-, WebDAV- oder Microsoft Office SharePoint Designer 2007-Schnittstellen verwenden, um auf die Website zuzugreifen. |
|`value`     | `public` | [`IODataBasePermission`](../sp-odata-types/iodatabasepermission.md) | _Schreibgeschützt._ Gibt den Wert des SPPermission-Objekts zurück. |
|`viewFormPages`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Formulare, Ansichten und Anwendungsseiten anzeigen und Listen auflisten. |
|`viewListItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Elemente in Listen, Dokumente in Dokumentbibliotheken und Webdiskussionskommentare anzeigen. |
|`viewPages`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Seiten einer Website anzeigen. |
|`viewUsageData`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Berichte über Websiteverwendung anzeigen. |
|`viewVersions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Ältere Versionen eines Listenelements oder Dokuments anzeigen. |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`hasAllPermissions(...requestedPerms)`](hasallpermissions-sppermission.md)     | `public` | `boolean` | Funktion zum Bestimmen, ob eine bestimmte Berechtigungsmaske über alle der angeforderten Berechtigungen verfügt. |
|[`hasAnyPermissions(...requestedPerms)`](hasanypermissions-sppermission.md)     | `public` | `boolean` | Funktion zum Bestimmen, ob eine bestimmte Berechtigungsmaske über eine der angeforderten Berechtigungen verfügt. |
|[`hasPermission(requestedPerm)`](haspermission-sppermission.md)     | `public` | `boolean` | Funktion zum Überprüfen, ob eine bestimmte Berechtigungsmaske über die entsprechende Berechtigung verfügt. |





