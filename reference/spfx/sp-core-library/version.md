# <a name="version-class"></a>Version-Klasse







Diese Klasse stellt Versionen dar, die das Zeichenfolgenformat MAJOR.MINOR[.PATCH[.REVISION]] aufweisen, wobei MAJOR, MINOR, PATCH und REVISION ganze Zahlen sind. PATCH und REVISION sind optional. Vorangestellte Nullen sind zulässig, haben aber bei Vergleichen keine Bedeutung. Beispiele: 1.0, 1.0.0, 1.0.0.0, 1.01, 01.02.03, 001.002.003.004



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`major`     | `public` | `number` | _Schreibgeschützt._ Die erste Zahl in der Versionszeichenfolge, die die Hauptversion angibt. |
|`minor`     | `public` | `number` | _Schreibgeschützt._ Die zweite Zahl in der Versionszeichenfolge, die die Nebenversion angibt. |
|`patch`     | `public` | `number` | _Schreibgeschützt._ Die dritte Zahl in der Versionszeichenfolge, die die Patchnummer in einer semantischen Version oder die Buildnummer in einer .NET System.Version-Klasse angibt. Ist auf undefiniert festgelegt, wenn die dritte Zahl nicht vorhanden ist. |
|`revision`     | `public` | `number` | _Schreibgeschützt._ Die vierte Zahl in der Versionszeichenfolge, die die Überarbeitungsnummer angibt. Ist auf undefiniert festgelegt, wenn die vierte Zahl nicht vorhanden ist. |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`equals(compareWith)`](equals-version.md)     | `public` | `boolean` | Überprüft, ob diese Version dem Eingabeparameter entspricht. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 1.0.0 equals 1.0.0 -> true 2.0.1 equals 2.0.0 -> false 3.0 equals 3.0.0 -> true 04.01 equals 4.1 -> true |
|[`greaterThan(compareWith)`](greaterthan-version.md)     | `public` | `boolean` | Überprüft, ob diese Version größer (d. h. neuer) als der Eingabeparameter ist. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 1.0.0 greaterThan 0.0.9 -> true 2.0 greaterThan 2.0.0 -> false 3.0.1 greaterThan 3.0 -> true |
|[`isValid(versionString)`](isvalid-version.md)     | `public, static` | `boolean` | Gibt an, ob eine Versionszeichenfolge gültig ist. |
|[`lessThan(compareWith)`](lessthan-version.md)     | `public` | `boolean` | Überprüft, ob diese Version niedriger (d. h. älter) als der Eingabeparameter ist. Fehlende Patchnummer wird als 0 (null) angenommen. Beispiele: 0.9.9 lessThan 1.0.0 -> true 2.0 lessThan 2.0.0 -> false 3.0 lessThan 3.0.1 -> true 04.01 lessThan 4.1 -> false |
|[`parse(versionString)`](parse-version.md)     | `public, static` | [`Version`](../sp-core-library/version.md) | Erstellt eine neue Versionsinstanz unter Verwendung der Versionszeichenfolge. tryParse überprüft die eingegebene Versionszeichenfolge und löst einen Fehler aus, wenn sie ungültig ist. |
|[`toString()`](tostring-version.md)     | `public` | `string` | Object.prototype.toString-Außerkraftsetzung Die Versionszeichenfolge in MAJOR.MINOR[.PATCH[.REVISION]] |
|[`tryParse(versionString)`](tryparse-version.md)     | `public, static` | [`Version`](../sp-core-library/version.md) | Versucht, eine neue Versionsinstanz mithilfe der Versionszeichenfolge zu erstellen. Gibt „nicht definiert“ zurück, wenn dieser Vorgang nicht erfolgreich war. |





