# <a name="httpclientconfigurations-class"></a>HttpClientConfigurations-Klasse







Diese Klasse bietet standardmäßige vordefinierte HTTPClientConfiguration-Objekte zur Verwendung mit der HttpClient-Klasse. Allgemein sollten Clients die neueste verfügbare Versionsnummer auswählen, wodurch alle Optionen, die für typische Szenarios empfohlen werden, aktiviert werden. (Wenn in Zukunft neue Optionen eingeführt werden, wird auch eine neue Versionsnummer eingeführt, um sicherzustellen, dass vorhandener Code weiterhin so funktioniert wie zum Zeitpunkt des Testens.)



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`none`     | `public` | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | Diese Konfiguration deaktiviert alle Funktionsoptionen für HttpClient. Das fetch()-Verhalten ist im Prinzip mit dem der WHATWG-Standard-API identisch, die hier dokumentiert wird: https://fetch.spec.whatwg.org/ |
|`v1`     | `public` | [`HttpClientConfiguration`](../sp-http/httpclientconfiguration.md) | Version 1 aktiviert diese Optionen: consoleLogging=true |







