# <a name="ipropertypanecustomfieldprops-interface"></a>IPropertyPaneCustomFieldProps-Schnittstelle







PropertyPane CustomPropertyField-Eigenschaften




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`context`      | `any` | Instanz-spezifischer Kontext. Dieser Kontext wird wieder an das Webpart in den onRender- und onDispose-APIs übergeben. Das Webpart kann diesen Kontext zum Verwalten von Zustandsinformationen verwenden. |
|`key`      | `string` | Ein EINDEUTIGER Schlüssel gibt die Identität dieses Steuerelements an. Der PropertyPane verwendet ReactJS zum Rendern der Komponenten. ReactJS verwendet Schlüssel, um eine Komponente zu identifizieren und um zu ermitteln, ob sie erneut gerendert werden soll. Dies ist ein Leistungsfeature in ReactJS. Lesen Sie den folgenden Link, um zu verstehen, wie Sie den Wert für den Schlüssel auswählen. |
|`onDispose`      | `(domElement: HTMLElement, context?: any) => void` | Diese API wird aufgerufen, wenn die Komponente vom Hostelement getrennt wird. |
|`onRender`      | `(domElement: HTMLElement, context?: any) => void` | Diese API wird aufgerufen, wenn das benutzerdefinierte Feld im Hostelement bereitgestellt wird. |






