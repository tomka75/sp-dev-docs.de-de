# <a name="createandprovideservicekeysimpleserviceclass"></a>createAndProvide(serviceKey,simpleServiceClass)




Dies ist eine Abkürzungsfunktion, die dem Erstellen einer neuen Instanz von SimpleServiceClass entspricht und dann durch Aufruf von ServiceScope.provide() registriert wird.

**Signatur:** _public createAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>, simpleServiceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): T;_

**Gibt Folgendes zurück**: `T`



- eine neu erstellte Instanz von simpleServiceClass

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | der Schlüssel, der später verwendet werden kann, um den Dienst nutzen |
| `simpleServiceClass`    | `{ new (serviceScope: ServiceScope); }` | die zu erstellende TypeScript-Klasse |


