# <a name="converttoodatastringliteral"></a>convertToODataStringLiteral()




Konvertiert eine Variable in ein OData-Zeichenfolgenliteral, das für die Verwendung in einer REST-URL geeignet ist. Die zurückgegebene Zeichenfolge wird in einfache Anführungszeichen eingeschlossen, und alle einfachen Anführungszeichen werden mit Escapezeichen versehen. Beispiel für die Verwendung: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produziert diese URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files"

**Signatur:** _public static convertToODataStringLiteral(value: string): string;_

**Gibt Folgendes zurück**: `string`





#### <a name="parameters"></a>Parameter
Keine


