# <a name="servicekey-t-class"></a>ServiceKey <T>-Klasse



_Typparameter: `<T>`_



Der SericeKey ist ein Suchschlüssel, der beim Aufrufen von ServiceScope.consume() zum Abrufen einer Abhängigkeit verwendet wird. Der Schlüssel definiert auch eine Standardimplementierung der Abhängigkeit, die vom Stammbereich automatisch erstellt wird, wenn die Abhängigkeit nicht gefunden wird. Durch Bereitstellen einer Standardimplementierung wird sichergestellt, dass neue Abhängigkeiten bedenkenlos eingeführt werden können, ohne versehentlich Komponenten zu zerstören, die von einem älteren Host geladen werden (der nicht die neue Abhängigkeit bereitstellt).


## <a name="constructor"></a>Konstruktor
PRIVAT - Rufen Sie dies nicht aus Ihrem eigenen Code auf.

**Signatur:** _constructor(id: string, name: string, defaultCreator: ServiceCreator<T>);_

**Gibt Folgendes zurück**: 



#### <a name="parameters"></a>Parameter
Keine


## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`defaultCreator`     | `public` | `ServiceCreator<T>` |  |
|`id`     | `public` | `string` |  |
|`name`     | `public` | `string` |  |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`create(name,serviceClass)`](create-servicekey.md)     | `public, static` | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | Erstellt einen neue ServiceKey, dessen Implementierung standardmäßig eine neue Instanz einer TypeScript-Klasse ist, die den standardmäßigen Konstruktorparameter akzeptiert. Wenn Sie benutzerdefinierte Konstruktorparameter angeben möchten, verwenden Sie stattdessen createCustom(). |
|[`createCustom(name,defaultCreator)`](createcustom-servicekey.md)     | `public, static` | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | Erstellt einen neuen ServiceKey, dessen standardmäßige Implementierung durch Aufruf des angegebenen Rückrufs abgerufen wird. |





