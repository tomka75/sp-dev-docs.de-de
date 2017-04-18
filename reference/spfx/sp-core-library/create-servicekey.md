# <a name="createnameserviceclass"></a>create(name,serviceClass)




Erstellt einen neue ServiceKey, dessen Implementierung standardmäßig eine neue Instanz einer TypeScript-Klasse ist, die den standardmäßigen Konstruktorparameter akzeptiert. Wenn Sie benutzerdefinierte Konstruktorparameter angeben möchten, verwenden Sie stattdessen createCustom().

**Signatur:** _public static create < T >(name: string, serviceClass: { new (serviceScope: [ServiceScope](../sp-core-library/servicescope.md)); }): [ServiceKey](../sp-core-library/servicekey.md)<T>;_

**Gibt Folgendes zurück**: [`ServiceKey`](../sp-core-library/servicekey.md)<T>



- den neu erstellten ServiceKey

#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `name`    | `string` | Ein Name wie z. B. "MyApplication.IMyService", der innerhalb der Anwendung eindeutig sein muss. |
| `serviceClass`    | `{ new (serviceScope: ServiceScope); }` | die TypeScript-Klasse, die den Dienst implementiert. |


