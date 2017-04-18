# <a name="iwebpartcontext-interface"></a>IWebPartContext-Schnittstelle







Die grundlegende Kontextschnittstelle für clientseitige Webparts.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`domElement`      | `HTMLElement` | Verweis auf das DOM-Element, das diese clientseitige Komponente hostet. |
|`httpClient`      | [`HttpClient`](../sp-http/httpclient.md) | HttpClient-Instanz bezogen auf dieses Webpart. |
|`instanceId`      | `string` | Webpart-Instanz-ID. Dies ist ein global eindeutiger Wert. |
|`manifest`      | `IClientSideWebPartManifestInstance<any>` | Manifest für das clientseitige Webpart. |
|`pageContext`      | [`PageContext`](../sp-page-context/pagecontext.md) | SharePoint-Seitenkontext. |
|`propertyPane`      | `IPropertyPaneAccessor` | Accessor für allgemeine Vorgänge des Webpart-Eigenschaftenbereichs. |
|`spHttpClient`      | [`SPHttpClient`](../sp-http/sphttpclient.md) | SPHttpClient-Instanz bezogen auf dieses Webpart. |
|`statusRenderer`      | [`IClientSideWebPartStatusRenderer`](../sp-webpart-base/iclientsidewebpartstatusrenderer.md) | Statuswiedergabe des Webparts. |
|`webPartTag`      | `string` | Webpart-Tag, das für die Protokollierung und Telemetrie verwendet werden soll. |






### <a name="remarks"></a>Bemerkungen

Ein „Kontextobjekt“ ist eine Sammlung von bekannten Dienste und anderen Objekten, die wahrscheinlich von Geschäftslogik benötigt werden, die mit einer Komponente arbeitet. Jeder Komponententyp verfügt über eine eigene spezielle Erweiterung dieser Schnittstelle, z. B. IWebPartContext für Webparts, ICodePartContext für Codeparts usw.

