# <a name="createcustomnamedefaultcreator"></a>createCustom(name,defaultCreator)




Erstellt einen neuen ServiceKey, dessen standardmäßige Implementierung durch Aufruf des angegebenen Rückrufs abgerufen wird.

**Signatur:** _public static createCustom < T >(name: string, defaultCreator: ServiceCreator<T>): [ServiceKey](../sp-core-library/servicekey.md)<T>;_

**Gibt Folgendes zurück**: [`ServiceKey`](../sp-core-library/servicekey.md)<T>



- den neu erstellten ServiceKey

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `name`    | `string` | Ein Name wie z. B. "MyApplication.IMyService", der innerhalb der Anwendung eindeutig sein muss. |
| `defaultCreator`    | `ServiceCreator<T>` | Ein Rückruf, der ein Objekt zurückgibt, das die T-Schnittstelle implementiert. |


