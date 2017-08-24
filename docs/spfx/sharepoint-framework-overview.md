# <a name="overview-of-the-sharepoint-framework"></a>Übersicht über das SharePoint Framework

Das SharePoint Framework (SPFx) ist ein Seiten- und Webpart-Modell, das vollständige Unterstützung für die clientseitige SharePoint-Entwicklung, einfache Integration in SharePoint-Daten und Unterstützung für Open-Source-Tools bietet. Mit dem SharePoint Framework können Sie moderne Webtechnologien und -tools in Ihrer bevorzugten Entwicklungsumgebung verwenden, um produktive Erfahrungen zu ermöglichen und Apps zu erstellen, die vom ersten Tag an schnell reagieren und für Mobilgeräte geeignet sind. Das SharePoint Framework funktioniert für das lokale SharePoint und SharePoint Online.
 
Zu den wichtigsten Features von SharePoint Framework zählen:

* Es wird im Kontext des aktuellen Benutzers und der aktuellen Verbindung im Browser ausgeführt. Die Anpassung läuft nicht über iFrames (JavaScript wird direkt in die Seite eingebettet).
* Die Steuerelemente werden im normalen Seiten-DOM gerendert.
* Die Steuerelemente reagieren von sich aus, und der Zugriff ist sofort möglich.
* Ermöglicht dem Entwickler den Zugriff auf den Lebenszyklus – einschließlich, zusätzlich zu **Rendern** -  **Laden**, **Serialisieren** und **Deserialisieren**, **Konfigurationsänderungen** und vieles mehr.
* Es ist vom Framework unabhängig. Sie können ein beliebiges Browser-Framework verwenden: React, Handlebars, Knockout, Angular und weitere.
* Die Toolchain basiert auf allgemeinen Open-Source-Cliententwicklungstools wie npm, TypeScript, Yeoman, Webpack und Gulp.
* Die Leistung ist zuverlässig.
* Endbenutzer können clientseitige SPFx-Lösungen verwenden, die von den Mandantenadministratoren (oder deren Stellvertretern) auf allen Websites genehmigt sind, einschließlich Self-Service-Team-, Gruppen- oder persönliche Websites. 
* Lösungen können auf klassischen Webpart- und Veröffentlichungsseiten sowie auf modernen Seiten bereitgestellt werden.
 
Im Skript-Editor-Webpart wird das Laufzeitmodell verbessert. Es enthält einer stabile Client-API, ein HttpClient-Objekt, das die Authentifizierung bei SharePoint und Office 365 verarbeitet, Kontextinformationen, einfache Eigenschaftsdefinition und -konfiguration und mehr. 

Wenn Sie mit C# und Visual Studio oder JavaScript arbeiten, müssen Sie ggf. etwas über clientseitige JavaScript-Entwicklung lernen. Die meisten Ihre Kenntnisse sind vollständig übertragbar. Sie verwenden die gleichen [REST-Dienste](https://msdn.microsoft.com/de-de/library/office/jj860569.aspx) oder [JavaScript Object Model (JSOM)](https://msdn.microsoft.com/de-de/library/office/jj193034.aspx) – je nach Ihren Anforderungen. Das Datenmodell wurde nicht geändert. Und wenn Sie ein C#-Entwickler sind, bietet TypeScript einen guten Übergang in die JavaScript-Welt. Die Wahl der IDE bleibt Ihnen überlassen. Viele Entwickler verwenden die plattformübergreifende IDE Visual Studio Code. Viele Entwickler verwenden auch Produkte wie Sublime und ATOM. Verwenden Sie, was für Sie am besten geeignet ist.

## <a name="why-the-sharepoint-framework"></a>Warum SharePoint Framework?

SharePoint wurde im Jahr 2001 als lokales Produkt gestartet. Im Laufe der Zeit hat eine große Entwicklercommunity es auf viele verschiedene Arten erweitert und gestaltet. In den meisten Fällen ist die Entwicklercommunity denselben Mustern und Methoden gefolgt, die das SharePoint-Produktentwicklungsteam verwendet hat, einschließlich Webparts, SharePoint-Feature-XML und mehr. Viele Funktionen wurden in C# entwickelt, zu DLLs kompiliert und auf den Servern bereitgestellt.
 
Diese Lösung funktionierte gut in Umgebungen mit nur einem Unternehmen, konnte aber nicht für die Cloud skaliert werden, in der mehrere Mandanten nebeneinander ausgeführt werden. Dementsprechend haben wir zwei alternative Modelle eingeführt: clientseitige JavaScript-Einfügung und SharePoint-Add-Ins. Beide Lösungen haben Vor- und Nachteile. 

### <a name="javascript-injection"></a>JavaScript-Einfügung

Einer der beliebtesten Webparts in SharePoint Online ist der Skript-Editor. Sie können den Skript-Editor verwenden, um JavaScript in das Webpart einzufügen, und dieses JavaScript dann beim Rendern der Seite ausführen. Das ist einfach und rudimentär, aber effektiv. Die Ausführung erfolgt im gleichen Browserkontext wie die Seite und befindet sich in der gleichen DOM, damit eine Interaktion mit anderen Steuerelementen auf der Seite möglich ist.  Er ist auch relativ leistungsfähig und einfach zu verwenden. 

Bei diesem Ansatz gibt es jedoch auch einige Nachteile. Während Sie Ihre Lösung packen können, damit Endbenutzer das Steuerelement auf der Seite ablegen können, können Sie Konfigurationsoptionen nur schwer bereitstellen. Außerdem kann der Endbenutzer die Seite bearbeiten und das Skript ändern, sodass das Webpart beschädigt werden kann. Ein weiteres großes Problem besteht darin, dass der Skript-Editor-Webpart nicht als **„Safe For Scripting“**  gekennzeichnet ist.  Die meisten Self-Service-Websitesammlungen (eigene Websites, Teamwebsites, Gruppenwebsites) haben ein Feature namens **„NoScript“** aktiviert. Technisch gesehen ist dies das Entfernen der Berechtigung „Add/Customize Pages“ (Hinzufügen/Anpassen von Seiten, ACP) in SharePoint. Dies bedeutet, dass der Skript-Editor-Webpart auf diesen Websites blockiert wird.  

### <a name="sharepoint-add-in-model"></a>SharePoint-Add-In-Modell

Die aktuelle Option für Lösungen, die auf NoScript-Websites ausgeführt werden, ist das Add-In-/App-Part-Modell. Diese Implementierung erstellt einen **iFrame**, wo sich das eigentliche Objekt befindet und ausgeführt wird. Der Vorteil besteht darin, dass es für Information Worker einfacher ist, zu vertrauen und bereitzustellen, da der iFrame für das System extern ist und keinen Zugriff auf den aktuellen DOM/die aktuelle Verbindung hat. Endbenutzer können Add-Ins auf NoScript-Websites installieren. 

Auch bei diesem Ansatz gibt es einige Nachteile. Die Add-Ins werden in einem **iFrame** ausgeführt. iFrames sind langsamer als der Skript-Editor-Webpart, da er eine neue Anforderung für eine andere Seite erfordert. Die Seite muss Authentifizierung und Autorisierung durchlaufen, über eigene Aufrufe SharePoint-Daten abrufen, verschiedene JavaScript-Bibliotheken laden und vieles mehr. Ein Skript-Editor braucht in der Regel z. B. 100 Millisekunden zum Laden und Rendern, während ein App-Part u. U. 2 Sekunden oder länger benötigt. Darüber hinaus wird es durch die **iFrame**-Grenze schwieriger, reaktive Designs zu erstellen und CSS- sowie Designinformationen zu vererben. iFrames besitzen eine erhöhte Sicherheit, was für Sie (der Zugriff auf Ihre Seite ist durch andere Steuerelemente auf der Seite nicht möglich) und den Endbenutzer (das Steuerelement hat keinen Zugriff auf die Verbindung mit Office 365) hilfreich sein kann.


### <a name="sharepoint-framework"></a>SharePoint Framework 

In der Vergangenheit haben wir Webparts als voll vertrauenswürdige C#-Assemblys erstellt, die auf die Cloud-Servern installiert wurden. Aktuelle Entwicklungsmodelle umfassen jedoch in den meisten Fällen JavaScript, das in einem Browser ausgeführt wird und REST-API-Aufrufe an die SharePoint- und Office 365-Back-End-Arbeitslasten vornimmt. C#-Assemblys funktionieren in dieser Umgebung nicht. Wir brauchten ein neues Entwicklungsmodell. Das SharePoint Framework ist die nächste Stufe der SharePoint-Entwicklung.

## <a name="whats-next"></a>Nächste Schritte

Dies ist die erste Vorschauversion. Wir stellen nach und nach Updates und Optimierungen basierend auf Ihrem Feedback und Ihren Erfahrungen bereit. Während sich das SharePoint Framework in der Vorschau befindet, können gelegentlich grundlegende Änderungen an API-Namen, Abläufen und mehr auftreten. Zukünftige Updates für das SharePoint Framework werden abwärtskompatibel sein, damit Ihre Lösungen weiterhin funktionieren.

## <a name="sharepoint-framework-license"></a>SharePoint Framework-Lizenz

Die SharePoint Framework-Komponenten werden unter dieser [Microsoft EULA](https://github.com/SharePoint/sp-dev-docs/blob/master/Microsoft%20Sharepoint%20Framework%20Preview%20EULA.DOCX) lizenziert.

## <a name="questions"></a>Fragen?

Wenn Sie noch Fragen haben, stellen Sie diese auf [SharePoint StackExchange](http://sharepoint.stackexchange.com/). Kennzeichnen Sie Ihre Fragen und Kommentare mit [#spfx](http://sharepoint.stackexchange.com/tags/spfx/), [#spfx-webparts](http://sharepoint.stackexchange.com/tags/spfx-webparts/) und [#spfx-tooling](http://sharepoint.stackexchange.com/tags/spfx-tooling/). 

Sie können auch Probleme, Fragen oder Feedback zu den Dokumenten oder dem SharePoint Framework in unserem [GitHub-Repository](https://github.com/SharePoint/sp-dev-docs/issues) veröffentlichen.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Übersicht über clientseitige SharePoint-Webparts](./web-parts/overview-client-side-web-parts)
