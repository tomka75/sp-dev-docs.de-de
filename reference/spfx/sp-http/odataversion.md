# <a name="odataversion-class"></a>ODataVersion-Klasse







Stellt die unterstützte Version der „OData-Version“-Kopfzeile dar, die Teil des Open Data Protocol-Standards ist.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`v3`     | `public` | [`ODataVersion`](../sp-http/odataversion.md) | Stellt Version 3.0 für die „OData-Version“-Kopfzeile dar |
|`v4`     | `public` | [`ODataVersion`](../sp-http/odataversion.md) | Stellt Version 4.0 für die „OData-Version“-Kopfzeile dar |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Gibt Folgendes zurück:  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`toString()`](tostring-odataversion.md)     | `public` | `string` | Gibt den Wert „OData-Version“ zurück, z. B. „4.0“. |
|[`tryParseFromHeaders()`](tryparsefromheaders-odataversion.md)     | `public, static` | [`ODataVersion`](../sp-http/odataversion.md) | Wenn die Kopfzeile „OData-Version“ vorhanden ist, gibt dies die entsprechende OData-Version-Konstante zurück. Ein Fehler wird ausgelöst, wenn die Versionsnummer nicht unterstützt wird. Wenn die Kopfzeile nicht vorhanden ist, wird „nicht definiert“ zurückgegeben. |





