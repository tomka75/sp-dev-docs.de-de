# <a name="environment-class"></a>Umgebungsklasse







Diese Klasse enthält kontextbezogene Informationen zur Umgebung, die das Framework und die zugehörigen Komponenten hostet.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`applicationSessionId`     | `public` | [`Guid`](../sp-core-library/guid.md) | _Schreibgeschützt._ Ein eindeutiger Bezeichner, der zum Korrelieren der Protokollierung und anderer Diagnoseinformationen verwendet wird. Er besteht für die Dauer der Clientanwendungsinstanz, d. h. er beginnt mit der Serveranforderung, die die Seite rendert, und endet z. B., wenn die Browserregisterkarte geschlossen wird oder F5 gedrückt wird, um die Seite erneut zu laden. Beachten Sie, dass, wenn der Router der Anwendung Router In-Place-Navigation (über die history.pushState()-API) unterstützt, die Anwendungssitzung während dieser Übergänge bestehen bleibt. |
|`pageSessionId`     | `public` | [`Guid`](../sp-core-library/guid.md) | _Schreibgeschützt._ Ein eindeutiger Bezeichner, der zum Korrelieren der Protokollierung und anderer Diagnoseinformationen verwendet wird. Während die gesamte Lebensdauer der Clientanwendungsinstanz von der applicationSessionId nachverfolgt wird, verfolgt pageSessionId eine einzelne "Seite" nach, die gerendert wird. Nehmen Sie beispielsweise an, dass die Anwendung ursprünglich PageA lädt und dass der Benutzer dann eine In-Place-Navigation (über die history.pushState()-API) zu PageB durchführt und dann zurück zu PageA navigiert, bevor er schließlich die Browserregisterkarte schließt. Während dieser Sequenz bleibt die applicationSessionId unverändert, jedoch wird die pageSessionId bei jeder Navigation geändert. Die 3 verschiedenen pageSessionId-Werte werden von der Diagnose verwendet, z. B. um Erfolg-/Fehlschlagsstatistiken für PageA unabhängig von PageB nachzuverfolgen. Das Konzept einer "Seite" wird von der Anwendung definiert. |
|`type`     | `public` | [`EnvironmentType`](../sp-core-library/environmenttype.md) | _Schreibgeschützt._ Eine Aufzählung, die beschreibt, in welcher Art von Umgebung das Framework ausgeführt wird. |







