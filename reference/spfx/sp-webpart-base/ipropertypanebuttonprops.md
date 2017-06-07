# <a name="ipropertypanebuttonprops-interface"></a>IPropertyPaneButtonProps-Schnittstelle







Eigenschaften der PropertyPane-Schaltfläche.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`ariaDescription`      | `string` | Detaillierte Beschreibung der Schaltfläche für Bildschirmsprachausgaben. Neben der zusammengesetzten Schaltfläche benötigen andere Schaltflächentypen weitere Angaben für die Bildschirmsprachausgabe. |
|`ariaLabel`      | `string` | Die Bereichsbeschriftung der Schaltfläche für Bildschirmsprachausgaben. |
|`buttonType`      | [`PropertyPaneButtonType`](../sp-webpart-base/propertypanebuttontype.md) | Der Typ der zu rendernden Schaltfläche. Standardwert ist ButtonType.normal. |
|`description`      | `string` | Beschreibung der Aktion für diese Schaltfläche. Nur für zusammengesetzte Schaltflächen verwendet. |
|`disabled`      | `boolean` | Gibt an, ob die Schaltfläche deaktiviert ist. |
|`icon`      | `string` | Das im Befehls- oder Herotyp angezeigte Schaltflächensymbol. |
|`onClick`      | `(value: any) => any` | Ein Rückruf, der beim Klicken auf die Schaltfläche ausgelöst wird und den vorhandenen Wert für die gebundene Eigenschaft übernimmt und den neuen Wert zurückgibt, der dann verwendet wird, um die Eigenschaftensammlung zu aktualisieren. Diese Aktualisierung führt zum erneuten Rendern von PropertyPane mit den neuen Eigenschaften. |
|`text`      | `string` | Anzeigetext des Elements. |






