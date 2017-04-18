# <a name="ipropertypanetextfieldprops-interface"></a>IPropertyPaneTextFieldProps-Schnittstelle







PropertyPaneTextField-Komponenteneigenschaften.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`ariaLabel`      | `string` | Aria-Beschriftung für das Textfeld, sofern vorhanden. |
|`deferredValidationTime`      | `number` | Die Validierung des Textfelds beginnt, wenn die Benutzer `deferredValidationTime` Millisekunden lang keine Eingabe vornehmen. Der Standardwert ist 200. |
|`description`      | `string` | Die Beschreibung der Eingabe in da Textfeld. |
|`disabled`      | `boolean` | Gibt an, ob das Textfeld des Eigenschaftenbereichs aktiviert ist. |
|`errorMessage`      | `string` | Der Standardwert des Textfelds, sofern vorhanden. |
|`label`      | `string` | Beschriftung für das Textfeld. |
|`multiline`      | `boolean` | Gibt an, ob das Textfeld ein mehrzeiliges Textfeld ist. Der Standardwert ist "false". |
|`onGetErrorMessage`      | `(value: string) => string `,` Promise<string>` | Die Methode wird verwendet, um die Validierungsfehlermeldung zu erhalten und zu ermitteln, ob der Eingabewert gültig ist oder nicht. Wenn eine Zeichenfolge zurückgegeben wird: - Es wird eine leere Zeichenfolge zurückgegeben, wenn diese gültig ist. - Fall diese nicht gültig ist, wird die Zeichenfolge der Fehlermeldung zurückgegeben, und im Textfeld wird ein roter Rahmen sowie eine Fehlermeldung unter dem Textfeld angezeigt. Wenn Zusage<string> zurückgegeben wird: - Der aufgelöste Wert wird als Fehlermeldung angezeigt. - Der abgelehnte Wert wird verworfen. |
|`placeholder`      | `string` | Platzhaltertext, der im Textfeld angezeigt werden soll. |
|`resizable`      | `boolean` | Gibt an, ob die Größe des mehrzeiligen Textfelds geändert werden kann. Der Standardwert ist „true“. |
|`underlined`      | `boolean` | Gibt an, ob das Textfeld unterstrichen angezeigt wird. Der Standardwert ist "false". |
|`value`      | `string` | Der aktuelle Wert des Textfelds. Dieser wird nur bereitgestellt, wenn das Textfeld eine gesteuerte Komponente ist, bei der Sie den aktuellen Zustand verwalten. |






