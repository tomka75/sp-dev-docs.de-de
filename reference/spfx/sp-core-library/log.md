# <a name="log-class"></a>Log-Klasse







Die Log-Klasse stellt statische Methoden zum Protokollieren von Meldungen auf unterschiedlichen Ebenen (ausführliche, Information, Warnung, Fehler) und mit Kontextinformationen bereit. Kontextinformationen helfen bei der Identifizierung, welche Komponente die Meldungen generiert hat, und gestalten die Meldung hilfreich und filterbar.






## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Gibt Folgendes zurück:  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`error(source,error,scope)`](error-log.md)     | `public, static` | `void` | Protokolliert einen Fehler |
|[`info(source,message,scope)`](info-log.md)     | `public, static` | `void` | Protokolliert eine Meldung nur zu Informationszwecken. |
|[`verbose(source,message,scope)`](verbose-log.md)     | `public, static` | `void` | Protokolliert eine ausführliche Meldung. |
|[`warn(source,message,scope)`](warn-log.md)     | `public, static` | `void` | Protokolliert eine Warnung. |





