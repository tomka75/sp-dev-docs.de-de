<span data-ttu-id="3428b-p101">Konvertiert eine Variable in ein OData-Zeichenfolgenliteral, das für die Verwendung in einer REST-URL geeignet ist. Die zurückgegebene Zeichenfolge wird in einfache Anführungszeichen eingeschlossen, und alle einfachen Anführungszeichen werden mit Escapezeichen versehen. Beispiel für die Verwendung: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produziert diese URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files"</span><span class="sxs-lookup"><span data-stu-id="3428b-p101">Converts a variable to an OData string literal suitable for usage in a REST URL. The returned string will be enclosed in single quotes, and any single quotes will be escaped. Example usage: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produces this URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files"</span></span>




Konvertiert eine Variable in ein OData-Zeichenfolgenliteral, das für die Verwendung in einer REST-URL geeignet ist. Die zurückgegebene Zeichenfolge wird in einfache Anführungszeichen eingeschlossen, und alle einfachen Anführungszeichen werden mit Escapezeichen versehen. Beispiel für die Verwendung: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produziert diese URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files"

<span data-ttu-id="3428b-105">**Signatur:** _public static convertToODataStringLiteral(value: string): string;_</span><span class="sxs-lookup"><span data-stu-id="3428b-105">**Signature:** _public static convertToODataStringLiteral(value: string): string;_</span></span>

<span data-ttu-id="3428b-106">**Gibt Folgendes zurück**: `string`</span><span class="sxs-lookup"><span data-stu-id="3428b-106">**Returns**: `string`</span></span>





#### <a name="parameters"></a><span data-ttu-id="3428b-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="3428b-107">Parameters</span></span>
<span data-ttu-id="3428b-108">Keine</span><span class="sxs-lookup"><span data-stu-id="3428b-108">None</span></span>


