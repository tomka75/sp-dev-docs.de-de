# <a name="httpclientconfiguration-class"></a>HttpClientConfiguration-Klasse

_Implementiert:[`IHttpClientConfiguration`](../sp-http/ihttpclientconfiguration.md)_



Diese befindet sich im Betamodus

Das HttpClientConfiguration-Objekt bietet eine Reihe von Optionen für das Aktivieren/Deaktivieren verschiedener Funktionen der HttpClient-Klasse. Normalerweise werden diese Optionen festgelegt (z. B. beim Aufruf von HttpClient.fetch()), indem einer der vordefinierten Standardwerte aus HttpClientConfigurations bereitgestellt wird, jedoch können Schalter auch über die HttpClientConfiguration.overrideWith()-Methode geändert werden.


## <a name="constructor"></a>Konstruktor
Erstellt eine neue Instanz von HttpClientConfiguration mit den angegebenen Flags. Die Standardwerte werden für alle Flags verwendet, die fehlen oder nicht definiert sind. Wenn overrideFlags angegeben wird, hat dies Vorrang vor Flags. *

**Signatur:** _constructor(flags: [IHttpClientConfiguration](../sp-http/ihttpclientconfiguration.md), overrideFlags?: IHttpClientConfiguration);_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine


## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`consoleLogging`     | `public` | `boolean` | _Schreibgeschützt._ {@inheritdoc IHttpClientConfiguration.consoleLogging} |
|`flags`     | `public` | [`IHttpClientConfiguration`](../sp-http/ihttpclientconfiguration.md) |  |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`initializeFlags()`](initializeflags-httpclientconfiguration.md)     | `protected` | `void` | Untergeordnete Klassen sollten diese Methode überschreiben, um das Flags-Objekt zu initialisieren. |
|[`overrideWith()`](overridewith-httpclientconfiguration.md)     | `public` | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | Untergeordnete Klassen sollten diese Methode überschreiben, um den untergeordneten Klassentyp anstelle des grundlegenden Klassentyps zu erstellen. |





