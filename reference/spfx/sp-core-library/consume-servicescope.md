# <a name="consumeservicekey"></a>consume(serviceKey)




Komponenten sollten diese Funktion aufrufen, um eine Abhängigkeit zu nutzen, d. h. den Dienstschlüssel nachschlagen und die registrierte Dienstinstanz zurückgeben. Wenn die Instanz nicht gefunden werden kann, wird automatisch eine Standardinstanz erstellt und beim Stammdienstbereich registriert.

**Signatur:** _public consume < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_

**Gibt Folgendes zurück**: `T`



- die Dienstinstanz

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | Der Schlüssel, der verwendet wurde, als provide() aufgerufen wurde, um den Dienst zu registrieren. |


