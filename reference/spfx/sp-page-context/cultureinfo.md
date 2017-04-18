# <a name="cultureinfo-class"></a>CultureInfo-Klasse







Diese Klasse wird in erster Linie mit der PageContext-Klasse verwendet. Sie stellt Gebietsschemainformationen für den aktuellen Benutzer der Anwendung bereit.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`currentCultureName`     | `public` | `string` | _Schreibgeschützt._ Diese Zeichenfolge bestimmt das Sprachenstandardformat für Datum, Uhrzeit, Zahlen, Währungswerte, die Sortierreihenfolge von Text, Groß-/Kleinschreibungskonventionen und Zeichenfolgenvergleiche. Diese Eigenschaft hat eventuell eine leere Zeichenfolge, ist aber nie undefiniert. Beispiel: Ist der currentCultureName "en-AU", kann die Anwendung diese Informationen verwenden, um das Datum als 1/8 anstelle von 8/1 anzuzeigen. |
|`currentUICultureName`     | `public` | `string` | _Schreibgeschützt._ Diese Zeichenfolge bestimmt die Standardsprache der Benutzeroberfläche. Dies wird für die Lokalisierung und Übersetzung von Text verwendet. Diese Eigenschaft hat eventuell eine leere Zeichenfolge, ist aber nie undefiniert. Beispiel: Ist currentUICultureName "es-MX", könnte die Anwendung diese Informationen verwenden, um das Wort "hello" als "hola" zu übersetzen. |
|`isRightToLeft`     | `public` | `boolean` | _Schreibgeschützt._ Dieser Wert stellt die dominante Richtung des geschriebenen Text für die Standardsprache der Benutzeroberfläche dar. |







