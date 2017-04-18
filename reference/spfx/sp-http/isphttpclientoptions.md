# <a name="isphttpclientoptions-interface"></a>ISPHttpClientOptions-Schnittstelle







Diese Schnittstelle definiert die Optionen für die SPHttpClient-Vorgänge, z. B. get(), post(), fetch() usw. Sie basiert auf den WHATWG-API-Standardparametern, die hier beschriebenen werden: https://fetch.spec.whatwg.org/




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`webUrl`      | `string` | Für einen Schreibvorgang fügt SPHttpClient automatisch die Kopfzeile „X-RequestDigest“ hinzu, die möglicherweise mithilfe einer separaten Anforderung wie z. B. „https://example.com/sites/sample/_api/contextinfo“ abgerufen werden muss. In der Regel kann die SPWeb-URL (in diesem Beispiel „https://example.com/sites/sample“) erraten werden, indem in der ursprünglichen REST-Abfrage nach einem reservierten URL-Segment gesucht wird, z. B. „_api“. Bestimmte REST-Endpunkte enthalten jedoch kein reserviertes URL-Segment; in diesem Fall kann die webUrl explizit von dieser Option angegeben werden. |






