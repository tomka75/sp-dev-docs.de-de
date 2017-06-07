# <a name="iclientsidecomponentcontext-interface"></a>IClientSideComponentContext-Schnittstelle





Diese befindet sich im Betamodus

Die grundlegende Kontextschnittstelle für clientseitige Komponenten.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`manifest`      | `IClientSideComponentManifest` | Manifest für die clientseitige Komponente. |
|`serviceScope`      | [`ServiceScope`](../sp-core-library/servicescope.md) | Dienstumfangsinstanz, die auf diesen Webpart beschränkt ist. |






### <a name="remarks"></a>HinwBemerkungeneise

Ein „Kontextobjekt“ ist eine Sammlung von bekannten Dienste und anderen Objekten, die wahrscheinlich von Geschäftslogik benötigt werden, die mit einer Komponente arbeitet. Jeder Komponententyp verfügt über eine eigene spezielle Erweiterung dieser Schnittstelle, z. B. IWebPartContext für Webparts, ICodePartContext für Codeparts usw.

