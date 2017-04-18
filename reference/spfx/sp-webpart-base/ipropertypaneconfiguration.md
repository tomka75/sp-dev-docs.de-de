# <a name="ipropertypaneconfiguration-interface"></a>IPropertyPaneConfiguration-Schnittstelle







Webpart-Konfigurationseinstellungen




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`currentPage`      | `number` | Im PropertyPane anzuzeigende Seite. |
|`loadingIndicatorDelayTime`      | `number` | Anzahl von Millisekunden für die Verzögerung vor dem Einblenden der Ladeanzeige im Eigenschaftenbereich. Standardwert ist 500. |
|`pages`      | [`IPropertyPanePage`](../sp-webpart-base/ipropertypanepage.md)[] | Die Gesamtzahl der Seiten im PropertyPane. |
|`showLoadingIndicator`      | `boolean` | Gibt an, ob die Ladeanzeige oben im Eigenschaftenbereich angezeigt werden soll. Dieses Feature soll verwendet werden, wenn der Benutzer auf eine Zusageauflösung wartet. Wenn auf true festgelegt, wird das Overlay der Ladeanzeige nach 500 ms eingeblendet (Webpart-Autor kann dieses Verhalten mithilfe der OverlayLoadingIndicator-Eigenschaft überschreiben). Der Grund, warum sie nicht sofort angezeigt wird, besteht darin, dass wir die Ladeanzeige nie einblenden möchten. Aber in der Praxis können asynchrone Anfragen lange dauern, sodass die Anzeige einer Ladeanzeige für den Endbenutzer erforderlich wird. |






