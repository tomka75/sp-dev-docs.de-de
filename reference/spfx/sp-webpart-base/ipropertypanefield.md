# <a name="ipropertypanefield-tproperties-interface"></a>IPropertyPaneField <TProperties>-Schnittstelle



_Typparameter: `<TProperties>`_



PropertyPane-Feld.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`properties`      | `TProperties` | Eigenschaftenobjekt mit starkem Typ. Speziell für jeden Feldtyp. Beispiel: Checkbox has ICheckboxProps, TextField has ITextField props. |
|`shouldFocus`      | `boolean` | Gibt an, ob sich dieses Steuerelement im Fokus befinden soll. Standardwert ist "false". |
|`targetProperty`      | `string` | Zieleigenschaft aus dem Eigenschaftenbehälter des Webparts. |
|`type`      | [`PropertyPaneFieldType`](../sp-webpart-base/propertypanefieldtype.md) | Typ des PropertyPane-Felds. |






