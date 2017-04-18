# <a name="sp-http-module"></a>sp-http-Modul



## <a name="classes"></a>Klassen

| Klasse    |  Beschreibung |
|:-------------|:---------------|
| [`HttpClient`](./sp-http/httpclient.md)     | HttpClient implementiert einen grundlegenden Satz von Funktionen für REST-Vorgänge. Die Unterklasse SPHttpClient erweitert diese grundlegenden Funktionen mit SharePoint-spezifischen Verbesserungen. |
| [`HttpClientConfiguration`](./sp-http/httpclientconfiguration.md)     | Das HttpClientConfiguration-Objekt bietet eine Reihe von Optionen für das Aktivieren/Deaktivieren verschiedener Funktionen der HttpClient-Klasse. Normalerweise werden diese Optionen festgelegt (z. B. beim Aufruf von HttpClient.fetch()), indem einer der vordefinierten Standardwerte aus HttpClientConfigurations bereitgestellt wird, jedoch können Schalter auch über die HttpClientConfiguration.overrideWith()-Methode geändert werden. |
| [`HttpClientConfigurations`](./sp-http/httpclientconfigurations.md)     | Diese Klasse bietet standardmäßige vordefinierte HTTPClientConfiguration-Objekte zur Verwendung mit der HttpClient-Klasse. Allgemein sollten Clients die neueste verfügbare Versionsnummer auswählen, wodurch alle Optionen, die für typische Szenarios empfohlen werden, aktiviert werden. (Wenn in Zukunft neue Optionen eingeführt werden, wird auch eine neue Versionsnummer eingeführt, um sicherzustellen, dass vorhandener Code weiterhin so funktioniert wie zum Zeitpunkt des Testens.) |
| [`HttpClientResponse`](./sp-http/httpclientresponse.md)     | Die Response-Unterklasse, die von Methoden wie HttpClient.fetch() zurückgegeben wird. |
| [`ODataVersion`](./sp-http/odataversion.md)     | Stellt die unterstützte Version der „OData-Version“-Kopfzeile dar, die Teil des Open Data Protocol-Standards ist. |
| [`SPHttpClient`](./sp-http/sphttpclient.md)     | SPHttpClient wird zum Durchführen von REST-Aufrufen für SharePoint verwendet. Es fügt Standardkopfzeilen hinzu, verwaltet den für Schreibvorgänge erforderlichen Digest und sammelt Telemetrie, die dem Dienst hilft, die Leistung einer Anwendung zu überwachen. Verwenden Sie für die Kommunikation mit Nicht-SharePoint-Diensten stattdessen die HttpClient-Klasse. |
| [`SPHttpClientCommonConfiguration`](./sp-http/sphttpclientcommonconfiguration.md)     | Allgemeine Basisklasse für SPHttpClientConfiguration und SPHttpClientBatchConfiguration. |
| [`SPHttpClientConfiguration`](./sp-http/sphttpclientconfiguration.md)     | Das SPHttpClientConfiguration-Objekt bietet eine Reihe von Optionen für das Aktivieren/Deaktivieren verschiedener Funktionen der SPHttpClient-Klasse. Normalerweise werden diese Optionen festgelegt (z. B. beim Aufruf von SPHttpClient.fetch()), indem einer der vordefinierten Standardwerte aus SPHttpClientConfigurations bereitgestellt wird, jedoch können Schalter auch über die SPHttpClientConfiguration.overrideWith()-Methode geändert werden. |
| [`SPHttpClientConfigurations`](./sp-http/sphttpclientconfigurations.md)     | Diese Klasse bietet standardmäßige vordefinierte SPHTTPClientConfiguration-Objekte zur Verwendung mit der SPHttpClient-Klasse. Allgemein sollten Clients die neueste verfügbare Versionsnummer auswählen, wodurch alle Optionen, die für typische Szenarios empfohlen werden, aktiviert werden. (Wenn in Zukunft neue Optionen eingeführt werden, wird auch eine neue Versionsnummer eingeführt, um sicherzustellen, dass vorhandener Code weiterhin so funktioniert wie zum Zeitpunkt des Testens.) |
| [`SPHttpClientResponse`](./sp-http/sphttpclientresponse.md)     | Die Response-Unterklasse, die von Methoden, wie z. B. SPHttpClient.fetch(), zurückgegeben wird. |



## <a name="interfaces"></a>Schnittstellen

| Schnittstelle    |  Beschreibung |
|:-------------|:---------------|
| [`IHttpClientConfiguration`](./sp-http/ihttpclientconfiguration.md)   | Flags-Schnittstelle für HttpClientConfiguration.  |
| [`IHttpClientOptions`](./sp-http/ihttpclientoptions.md)   | Diese Schnittstelle definiert die Optionen für die HttpClient-Vorgänge, z. B. get(), post(), fetch() usw. Sie basiert auf den WHATWG-API-Standardparametern, die hier beschriebenen werden: https://fetch.spec.whatwg.org/  |
| [`ISPHttpClientCommonConfiguration`](./sp-http/isphttpclientcommonconfiguration.md)   | Flags-Schnittstelle für SPHttpClientCommonConfiguration.  |
| [`ISPHttpClientConfiguration`](./sp-http/isphttpclientconfiguration.md)   | Flags-Schnittstelle für SPHttpClientConfiguration.  |
| [`ISPHttpClientOptions`](./sp-http/isphttpclientoptions.md)   | Diese Schnittstelle definiert die Optionen für die SPHttpClient-Vorgänge, z. B. get(), post(), fetch() usw. Sie basiert auf den WHATWG-API-Standardparametern, die hier beschriebenen werden: https://fetch.spec.whatwg.org/  |






