# <a name="sphttpclientcommonconfiguration-class"></a>SPHttpClientCommonConfiguration-Klasse

_Implementiert:[`ISPHttpClientCommonConfiguration`](../sp-http/isphttpclientcommonconfiguration.md)_





Allgemeine Basisklasse für SPHttpClientConfiguration und SPHttpClientBatchConfiguration.


## <a name="constructor"></a>Konstruktor
Erstellt eine neue Instanz von SPHttpClientCommonConfiguration mit den angegebenen Flags. Die Standardwerte werden für alle Flags verwendet, die fehlen oder nicht definiert sind. Wenn overrideFlags angegeben wird, hat dies Vorrang vor Flags.

**Signatur:** _constructor(flags: [ISPHttpClientCommonConfiguration](../sp-http/isphttpclientcommonconfiguration.md), overrideFlags?: ISPHttpClientCommonConfiguration);_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine


## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`flags`     | `public` | [`ISPHttpClientCommonConfiguration`](../sp-http/isphttpclientcommonconfiguration.md) |  |
|`jsonRequest`     | `public` | `boolean` | _Schreibgeschützt._ {@inheritdoc IHttpClientConfiguration.jsonRequest} |
|`jsonResponse`     | `public` | `boolean` | _Schreibgeschützt._ {@inheritdoc IHttpClientConfiguration.jsonResponse} |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Gibt Folgendes zurück:  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`initializeFlags()`](initializeflags-sphttpclientcommonconfiguration.md)     | `protected` | `void` |  |
|[`overrideWith()`](overridewith-sphttpclientcommonconfiguration.md)     | `public` | [`SPHttpClientCommonConfiguration`](../sp-http/sphttpclientcommonconfiguration.md) |  |





