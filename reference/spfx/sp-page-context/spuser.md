# <a name="spuser-class"></a>SPUser-Klasse







Diese Klasse wird in erster Linie mit der PageContext-Klasse verwendet. Sie bietet kontextbezogene Informationen für den SharePoint-Benutzer, der auf die Seite zugreift.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`displayName`     | `public` | `string` | _Schreibgeschützt._ Der Anzeigename für den aktuellen Benutzer. Beispiel: „John Doe“ |
|`email`     | `public` | `string` | _Schreibgeschützt._ Die E-Mail-Adresse des aktuellen Benutzers. Beispiel: „example@contoso.com“ |
|`isAnonymousGuestUser`     | `public` | `boolean` | _Schreibgeschützt._ Wird zurückgegeben, wenn der aktuelle Benutzer ein anonymer Gast ist. |
|`isExternalGuestUser`     | `public` | `boolean` | _Schreibgeschützt._ Gibt „true“ zurück, wenn der aktuelle Benutzer ein externer Gast ist. |
|`loginName`     | `public` | `string` | _Schreibgeschützt._ Der Anmeldename für den aktuellen Benutzer. Beispiel: „i:0#.w|domain\user“ |







