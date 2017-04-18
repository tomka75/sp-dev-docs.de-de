# <a name="sphttpclientconfigurations-class"></a>SPHttpClientConfigurations-Klasse







Diese Klasse bietet standardmäßige vordefinierte SPHTTPClientConfiguration-Objekte zur Verwendung mit der SPHttpClient-Klasse. Allgemein sollten Clients die neueste verfügbare Versionsnummer auswählen, wodurch alle Optionen, die für typische Szenarios empfohlen werden, aktiviert werden. (Wenn in Zukunft neue Optionen eingeführt werden, wird auch eine neue Versionsnummer eingeführt, um sicherzustellen, dass vorhandener Code weiterhin so funktioniert wie zum Zeitpunkt des Testens.)



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`none`     | `public` | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | Diese Konfiguration deaktiviert alle Funktionsoptionen für HttpClient. Das fetch()-Verhalten ist im Prinzip mit dem der WHATWG-Standard-API identisch, die hier dokumentiert wird: https://fetch.spec.whatwg.org/ |
|`v1`     | `public` | [`SPHttpClientConfiguration`](../sp-http/sphttpclientconfiguration.md) | Version 1 ermöglicht diese Optionen: ConsoleLogging = WAHR; JsonRequest = WAHR; JsonResponse = WAHR; DefaultSameOriginCredentials = WAHR; DefaultODataVersion = ODataVersion.v4; RequestDigest = True |







