# <a name="guid-class"></a>GUID-Klasse







Diese Klasse stellt einen Globally Unique Identifier (Global eindeutiger Bezeichner) dar, wie von IETF RFC 4122 beschrieben. Die Eingabezeichenfolge ist normalisiert und überprüft, was wichtige Garantien bereitstellt, die anderen Code vereinfachen, der mit der GUID funktioniert. Diese Klasse stellt außerdem grundlegende Unterstützung für das Generieren einer pseudozufälligen GUID bereit. Beachten Sie jedoch, dass die Eindeutigkeit von der Math.random()-Funktion des Browsers abhängt und möglicherweise für einige Anwendungen nicht geeignet ist.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`empty`     | `public` | [`Guid`](../sp-core-library/guid.md) | Gibt eine neue leere GUID-Instanz zurück. |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`equals()`](equals-guid.md)     | `public` | `boolean` | Vergleicht diese Instanz mit einer anderen GUID-Instanz |
|[`isValid(guid)`](isvalid-guid.md)     | `public, static` | `boolean` | Gibt an, ob eine GUID gültig ist, d. h., ob sie von Guid.tryParse() erfolgreich analysiert werden würde. Diese Funktion ist günstiger als Guid.tryParse(), weil kein GUID-Objekt erstellt wird. |
|[`newGuid()`](newguid-guid.md)     | `public, static` | [`Guid`](../sp-core-library/guid.md) | Gibt eine neue GUID-Instanz mit einer pseudozufällig erstellten GUID entsprechend des UUID-Algorithmus, Version 4, von RFC 4122 zurück. |
|[`parse(guid)`](parse-guid.md)     | `public, static` | [`Guid`](../sp-core-library/guid.md) | Analysiert die Eingabezeichenfolge zum Erstellen eines neuen GUID-Objekts. Wenn die Zeichenfolge nicht analysiert werden kann, wird ein Fehler ausgelöst. |
|[`toString()`](tostring-guid.md)     | `public` | `string` | Object.prototype.toString-Außerkraftsetzung |
|[`tryParse(guid)`](tryparse-guid.md)     | `public, static` | [`Guid`](../sp-core-library/guid.md) | Versucht, die Eingabezeichenfolge zum Erstellen eines neuen GUID-Objekts zu analysieren. Wenn die Zeichenfolge nicht analysiert werden kann, wird undefiniert zurückgegeben. |





