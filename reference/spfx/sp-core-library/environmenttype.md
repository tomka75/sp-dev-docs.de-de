# <a name="environmenttype-enumeration"></a>EnvironmentType-Aufzählung
Eine Aufzählung, die beschreibt, in welcher Art von Umgebung das Framework ausgeführt wird.

| Element	       | Beschreibung|
|:-------------|:-------|
|`ClassicSharePoint`       | Gibt an, dass das Framework von einer klassischen Server-gerenderten SharePoint-Seite geladen wurde. |
|`Local`       | Stellt das Szenario des Frameworks dar, das auf einem localhost-Server gehostet wird, der in der Regel nicht auf SharePoint-REST-APIs zugreifen kann. Beispiel: Ein Entwickler verwendet einen gulp serve-Befehl, um die Änderungen in einem Browser zu testen. |
|`SharePoint`       | Gibt an, dass das Framework von einer Client-gerenderten SharePoint-Seite geladen wurde. |
|`Test`       | Stellt das Szenario des Frameworks dar, das in einem Einheits-/Integrationstest gehostet wird. Beispiel: Ein Entwickler führt eine Testeinheit zum Überprüfen der Änderungen an seinem Webpart aus. |
