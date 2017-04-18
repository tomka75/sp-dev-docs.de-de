# <a name="iodatanavigationnode-interface"></a>IODataNavigationNode-Schnittstelle







Stellt ein OData-SP.NavigationNode-Objekt dar. https://msdn.Microsoft.com/en-us/library/Office/jj246311.aspx




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`Children`      | [`IODataNavigationNode`](../sp-odata-types/iodatanavigationnode.md)[] | Ruft oder ein Array mit Navigationsknoten ab oder legt es fest, die untergeordnete Elemente des aktuellen Knotens sind. |
|`Id`      | `number` | Ruft einen Wert ab, der den Bezeichner für den Navigationsknoten angibt. |
|`IsDocLib`      | `boolean` |  |
|`IsExternal`      | `boolean` | Ruft einen Wert ab oder legt einen Wert fest, der angibt, ob die URL des Navigationsknotens potenziell Seiten außerhalb der Websitesammlung entspricht. |
|`IsVisible`      | `boolean` | Ruft einen Wert ab oder legt einen Wert fest, der angibt, wenn der Knotennavigationslink sichtbar sein soll. |
|`Title`      | `string` | Ruft einen Wert ab oder legt einen Wert fest, der den Ankertext für den Knotennavigationslink angibt. |
|`Url`      | `string` | Ruft einen Wert ab oder legt einen Wert fest, der die URL angibt, die mit dem Navigationsknoten gespeichert werden soll. Es muss sich um eine URL in der relativen Form handeln, wenn IsExternal "false" ist. Es muss sich um eine URL in der relativen oder absoluten Form handeln. |






