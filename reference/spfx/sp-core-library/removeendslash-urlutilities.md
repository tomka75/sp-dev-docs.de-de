# <a name="removeendslashurl"></a>removeEndSlash(url)




Entfernt Schrägstriche vom Ende der URL. Bei dieser Funktion wird angenommen, dass die Eingabe bereits eine gültige absolute oder serverbezogene URL ist. Beispiele: removeEndSlash('http://example.com/') ---> 'http://example.com' removeEndSlash('/example') ---> '/example' removeEndSlash('/') ---> ''

**Signatur:** _public static removeEndSlash(url: string): string;_

**Gibt Folgendes zurück**: `string`





#### <a name="parameters"></a>Parameter


| Parameter       | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `url`    | `string` | Die URL, die normalisiert werden soll. |


