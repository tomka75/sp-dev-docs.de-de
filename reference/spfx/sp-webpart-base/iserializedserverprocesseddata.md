# <a name="iserializedserverprocesseddata-interface"></a>ISerializedServerProcessedData-Schnittstelle







Enthält Datensammlungen, die von serverseitigen Diensten wie Suchindex und Linkkorrektur verarbeitet werden können.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`htmlStrings`      | `{ [key: string]: string }` | Eine Schlüssel-/Wertzuordnung, bei der Schlüssel Zeichenfolgenbezeichner und Werte Rich-Text mit HTML sind. SharePoint-Server behandeln die Werte als HTML-Inhalt und führen Dienste wie Sicherheitsüberprüfungen, Suchindex und Linkkorrektur dafür aus. Beispiel: {'MyRichDescription': '<div>Einige Standard<b>HTML-Inhalte</b><a href='http://somelink'>Link</a></div>' 'anotherRichText': <div class='aClass'><span style='color:red'>Text in rot</div> } |
|`imageSources`      | `{ [key: string]: string }` | Eine Schlüssel-/Wertzuordnung, bei der Schlüssel Zeichenfolgenbezeichner und Werte Bildquellen sind. SharePoint-Server behandeln Sie die Werte als Bildquellen und führen Dienste wie Suchindex und Linkkorrektur dafür aus. Beispiel: {'myImage1': 'http://res.contoso.com/path/to/file' 'myImage2': 'https://res.contoso.com/someName.jpg'} |
|`links`      | `{ [key: string]: string }` | Eine Schlüssel-/Wertzuordnung, bei der Schlüssel Zeichenfolgenbezeichner und Werte Links sind. SharePoint-Server behandeln die Werte als Links und führen Sie Dienste wie Linkkorrektur dafür aus. Beispiel: { 'myWebURL': 'http://contoso.com' 'myFileLink': 'https://res.contoso.com/file.docx' } |






