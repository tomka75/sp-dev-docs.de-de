# <a name="iplaceholderprops-interface"></a>IPlaceholderProps-Schnittstelle







Zum Anzeigen eines Platzhalters bei keinem oder temporärem Inhalt verwendet. Schaltfläche ist optional.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`buttonLabel`      | `string` | Beschriftung, die auf der Schaltfläche unterhalb der Beschreibung angezeigt wird. Optional: Wie die Schaltfläche optional. |
|`contentClassName`      | `string` | Dieser className wird auf das Stammelement des Inhalts angewendet. Verwenden Sie dies, um benutzerdefinierte Formatvorlagen auf den Platzhalter anzuwenden. |
|`description`      | `string` | Textbeschreibung für den Platzhalter. Wird unterhalb des Symbols und des Symboltexts angezeigt. |
|`icon`      | `string` | Symbolklassenname aus der MDL2-Gruppe. Beispiel: 'ms-Icon--Add'. |
|`iconText`      | `string` | Für das Symbol angezeigte Überschrift. |
|`onAdd`      | `() => void` | onClick-Handler für die Schaltfläche. Optional: Wie die Schaltfläche optional. |






