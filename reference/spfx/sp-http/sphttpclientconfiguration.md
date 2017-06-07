# <a name="sphttpclientconfiguration-class"></a>SPHttpClientConfiguration-Klasse

_Implementiert:[`ISPHttpClientConfiguration`](../sp-http/isphttpclientconfiguration.md)_





Das SPHttpClientConfiguration-Objekt bietet eine Reihe von Optionen für das Aktivieren/Deaktivieren verschiedener Funktionen der SPHttpClient-Klasse. Normalerweise werden diese Optionen festgelegt (z. B. beim Aufruf von SPHttpClient.fetch()), indem einer der vordefinierten Standardwerte aus SPHttpClientConfigurations bereitgestellt wird, jedoch können Schalter auch über die SPHttpClientConfiguration.overrideWith()-Methode geändert werden.


## <a name="constructor"></a>Konstruktor
Erstellt eine neue Instanz von SPHttpClientConfiguration mit den angegebenen Flags. Die Standardwerte werden für alle Flags verwendet, die fehlen oder nicht definiert sind. Wenn overrideFlags angegeben wird, hat dies Vorrang vor Flags.

**Signatur:** _constructor(flags: [ISPHttpClientConfiguration](../sp-http/isphttpclientconfiguration.md), overrideFlags?: ISPHttpClientConfiguration);_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine


## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`defaultODataVersion`     | `public` | [`ODataVersion`](../sp-http/odataversion.md) | _Schreibgeschützt._ {@inheritdoc IHttpClientConfiguration.defaultODataVersion} |
|`defaultSameOriginCredentials`     | `public` | `boolean` | _Schreibgeschützt._ {@inheritdoc IHttpClientConfiguration.defaultSameOriginCredentials} |
|`flags`     | `public` | [`ISPHttpClientConfiguration`](../sp-http/isphttpclientconfiguration.md) |  |
|`requestDigest`     | `public` | `boolean` | _Schreibgeschützt._ {@inheritdoc IHttpClientConfiguration.requestDigest} |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`initializeFlags()`](initializeflags-sphttpclientconfiguration.md)     | `protected` | `void` |  |
|[`overrideWith()`](overridewith-sphttpclientconfiguration.md)     | `public` | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) |  |





