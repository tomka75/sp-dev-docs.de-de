# <a name="urlutilities-class"></a>UrlUtilities-Klasse







Häufig verwendete Hilfsfunktionen für das Arbeiten mit URLs. Diese Dienstprogramme sollen einfach, klein und vielfältig anwendbar sein.






## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`convertToODataStringLiteral()`](converttoodatastringliteral-urlutilities.md)     | `public, static` | `string` | Konvertiert eine Variable in ein OData-Zeichenfolgenliteral, das für die Verwendung in einer REST-URL geeignet ist. Die zurückgegebene Zeichenfolge wird in einfache Anführungszeichen eingeschlossen, und alle einfachen Anführungszeichen werden mit Escapezeichen versehen. Beispiel für die Verwendung: const url = "/_api/web/GetFolderByServerRelativeUrl(" + UrlUtilities.convertToODataStringLiteral("/SitePages/Alice's%20Page") + ")/Files"; // Produziert diese URL: // "/_api/web/GetFolderByServerRelativeUrl('/SitePages/Alice''s%20Page')/Files" |
|[`removeEndSlash(url)`](removeendslash-urlutilities.md)     | `public, static` | `string` | Entfernt Schrägstriche vom Ende der URL. Bei dieser Funktion wird angenommen, dass die Eingabe bereits eine gültige absolute oder serverbezogene URL ist. Beispiele: removeEndSlash('http://example.com/') ---> 'http://example.com' removeEndSlash('/example') ---> '/example' removeEndSlash('/') ---> '' |





