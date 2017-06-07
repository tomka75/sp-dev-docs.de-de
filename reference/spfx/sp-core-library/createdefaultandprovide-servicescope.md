# <a name="createdefaultandprovideservicekey"></a>createDefaultAndProvide(serviceKey)




Dies ist eine Abkürzungsfunktion, die die Standardimplementierung des angegebenen ServiceKey erstellt und ihn dann durch Aufrufen von ServiceScope.provide() registriert.

**Signatur:** _public createDefaultAndProvide < T >(serviceKey: [ServiceKey](../sp-core-library/servicekey.md)<T>): T;_

**Gibt Folgendes zurück**: `T`



- eine Dienstinstanz, die mit ServiceKey.defaultCreator erstellt wurde

#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `serviceKey`    | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | der Schlüssel, der später verwendet werden kann, um den Dienst nutzen |


