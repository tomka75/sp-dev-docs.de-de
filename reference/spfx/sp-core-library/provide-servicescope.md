# <a name="provideservicekeyservice"></a>provide(serviceKey,service)




ServiceScope.provide() wird zum Registrieren einer Implementierung der angegebenen serviceKey für den aktuellen Bereich verwendet. Dies kann nur verwendet werden, wenn der ServiceScope sich in einem „nicht abgeschlossenen“ Zustand befindet, d. h., bevor finish() aufgerufen wurde.

**Signatur:** _public provide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, service: T): T;_

**Gibt Folgendes zurück**: `T`



- Das gleiche Objekt, das Dienstparameter übergeben wurde

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | Der Schlüssel, der später verwendet wird, um den Dienst zu nutzen. |
| `service`    | `T` | Die Dienstinstanz, die registriert wird. |


