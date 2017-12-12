---
title: Migrieren vorhandener Skript-Editor-Webpart-Anpassungen zu SharePoint-Framework
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 89a8252798287bf0e668d5f8a9538d1c28381eb6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="migrate-existing-script-editor-web-part-customizations-to-the-sharepoint-framework"></a>Migrieren vorhandener Skript-Editor-Webpart-Anpassungen zu SharePoint-Framework

SharePoint Framework ist ein neues Modell zur Erstellung von SharePoint-Anpassungen. Falls Sie Ihre clientseitigen SharePoint-Lösungen bisher mithilfe des Skript-Editor-Webparts erstellt haben, fragen Sie sich möglicherweise, welche Vorteile eine Migration zu unserem neuen Entwicklungsmodell SharePoint Framework hat. In diesem Artikel werden die verschiedenen Vorteile einer Migration vorhandener clientseitiger Anpassungen zum neuen Entwicklungsmodell SharePoint Framework beschrieben. Darüber hinaus stellen wir Ihnen verschiedene Aspekte vor, die Sie bei der Migrationsplanung berücksichtigen sollten.

> Hinweis: Die Informationen in diesem Artikel gelten für Anpassungen, die mithilfe des Skript-Editor-Webparts erstellt wurden, sowie für Anpassungen, die mithilfe des Inhalts-Editor-Webparts erstellt wurden. Wann immer in diesem Artikel auf das Skript-Editor-Webpart Bezug genommen wird, sind _sowohl das Inhalts-Editor-Webpart als auch das Skript-Editor-Webpart_ gemeint.

## <a name="benefit-of-migrating-existing-client-side-customizations-to-the-sharepoint-framework"></a>Vorteile einer Migration vorhandener clientseitiger Anpassungen zu SharePoint-Framework

SharePoint Framework wurde von Grund auf als ein SharePoint-Entwicklungsmodell konzipiert, das den Schwerpunkt auf die clientseitige Entwicklung legt. Während es in erster Linie Erweiterungsfunktionen für moderne Teamwebsites bietet, funktionieren SharePoint Framework-basierte Anpassungen auch in der klassischen SharePoint-Oberfläche. Wenn Sie Ihre Anpassungen mit SharePoint Framework erstellen, hat das eine Reihe von Vorteilen gegenüber der Verwendung der übrigen aktuell verfügbaren SharePoint-Entwicklungsmodelle.

### <a name="build-once-reuse-across-all-devices"></a>Einmal erstellen, geräteunabhängig wiederverwenden

Die moderne SharePoint-Benutzeroberfläche bietet native Unterstützung für den Zugriff auf in SharePoint gespeicherte Informationen, über jedes Gerät. Darüber hinaus unterstützt die moderne Oberfläche auch die mobile SharePoint-App. Lösungen auf SharePoint Framework-Basis integrieren sich nahtlos in die moderne SharePoint-Oberfläche und lassen sich nicht nur auf unterschiedlichsten Geräten, sondern auch in der mobilen SharePoint-App nutzen. Da SharePoint Framework-Lösungen außerdem in der klassischen SharePoint-Oberfläche funktionieren, können sie auch von Organisationen genutzt werden, die noch nicht zur modernen Oberfläche migriert sind.

### <a name="more-robust-and-future-proof"></a>Stabiler und zukunftssicher

In der Vergangenheit haben Entwickler SharePoint angepasst, indem sie Komponenten an spezifische DOM-Elemente in der Benutzeroberfläche angefügt haben. Mit dieser Methode konnten sie die Standardbenutzeroberfläche ändern oder Endbenutzern zusätzliche Funktionen bereitstellen. Lösungen dieser Art waren jedoch fehleranfällig. Denn: Das DOM von SharePoint-Seiten war nie als Erweiterungsoberfläche gedacht. Wann immer es geändert wurde, funktionierten von ihm abhängige Lösungen anschließend nicht mehr.

SharePoint Framework bietet Entwicklern standardisierte API- und Erweiterungspunkte, mit deren Hilfe sie clientseitige Lösungen erstellen und Endbenutzern zusätzliche Funktionen bereitstellen können. Mit SharePoint Framework haben Entwickler ein Modell zur Erstellung unterstützter und zukunftssicherer Lösungen an der Hand und müssen sich keine Sorgen darüber machen, wie zukünftige Änderungen an der SharePoint-Benutzeroberfläche sich auf ihre Lösung auswirken könnten.

### <a name="easier-access-to-information-in-sharepoint-and-office-365"></a>Einfacherer Zugriff auf Informationen in SharePoint und Office 365

Microsoft erweitert den Funktionsumfang von SharePoint und Office 365 kontinuierlich. Da immer mehr Organisationen beide Plattformen nutzen, wird der Zugriff auf in Office 365 gespeicherte Informationen und Erkenntnisse für Entwickler zunehmend wichtig, um funktionsreiche Lösungen erstellen zu können. Eines der Ziele von SharePoint Framework ist es, Entwicklern die Anbindung an verschiedenste SharePoint- und Office 365-APIs einfach zu machen.

### <a name="enable-users-to-configure-solutions-to-their-needs"></a>Anforderungsbasierte Lösungskonfiguration auf Benutzerseite

Clientseitige Lösungen auf Basis eingebetteter Skripts ließen sich von Endbenutzern oft nur schwer für ihr individuelles Anforderungsprofil konfigurieren. Eine Konfiguration solcher Lösungen war nur durch die Anpassung ihres Codes oder über eine speziell für diesen Zweck erstellte individuelle Benutzeroberfläche möglich.

Clientseitige SharePoint Framework-Webparts bieten ein Standardverfahren zur Webpartkonfiguration in Gestalt eines Eigenschaftenbereichs: eine vertraute Funktion für Benutzer, die in der Vergangenheit mit klassischen Webparts gearbeitet haben. Entwickler clientseitiger Webparts können entscheiden, ob ihr Webpart einen dynamischen Eigenschaftenbereich haben soll (Standard), sodass jede Änderung an einer Webparteigenschaft direkt im Webpartkörper sichtbar wird, oder einen nicht dynamischen Eigenschaftenbereich, bei dem Webparteigenschaften explizit angewendet werden müssen.

### <a name="work-on-no-script-sites"></a>Unterstützung von No-Script-Websites

Mit der No-Script-Funktion in SharePoint Online möchte Microsoft Organisationen bei der Anpassungsgovernance helfen. Ist für einen Mandanten oder eine bestimmte Websitesammlung das No-Script-Flag gesetzt, werden auf Skriptinjektion und Einbettung basierende Anpassungen deaktiviert.

Da clientseitige SharePoint Framework-Webparts über den App-Katalog bereitgestellt und vorab genehmigt werden, dürfen sie auf No-Script-Websites ausgeführt werden. Auf modernen Teamwebsites ist die No-Script-Einstellung standardmäßig aktiviert, sodass eine Einbettung von Skripts auf diesen Websites nicht möglich ist. Damit ist SharePoint Framework aktuell das einzige unterstützte Modell zur Erstellung clientseitiger Anpassungen für moderne Teamwebsites.

## <a name="similarities-between-sharepoint-framework-solutions-and-script-editor-web-part-customizations"></a>Ähnlichkeiten zwischen SharePoint Framework-Lösungen und Skript-Editor-Webpart-Anpassungen

SharePoint Framework-Lösungen basieren zwar auf einem neuen Entwicklungsmodell, das eine neue Toolkette verwendet; sie haben aber dennoch Ähnlichkeit mit den Skript-Editor-Webpart-Anpassungen, die Sie bisher erstellt haben. Die Tatsache, dass beide Anpassungstypen auf dieselben Konzepte setzen, macht eine Migration zum neuen Entwicklungsmodell SharePoint Framework einfacher.

### <a name="run-as-a-part-of-the-page"></a>Ausführung als Teil der Seite

Ähnlich wie eingebettete Anpassungen und Skript-Editor-Webparts sind SharePoint Framework-Lösungen Teil der Seite. Damit haben diese Lösungen Zugriff auf das DOM der Seite und können mit anderen Komponenten auf der Seite kommunizieren. Zusätzlich macht diese Tatsache es Entwicklern leichter, ihre Lösungen dynamisch zu gestalten, sodass sie sich an die verschiedenen Formfaktoren anpassen können, in denen eine SharePoint-Seite angezeigt werden kann. Unter anderem wird auch die mobile SharePoint-App unterstützt.

Im Gegensatz zu SharePoint-Add-Ins werden clientseitige SharePoint Framework-Webparts nicht in einem iFrame isoliert. Ganz gleich also, auf welche Ressourcen ein clientseitiges Webpart zugreifen kann: Die anderen Elemente auf der Seite haben auf diese Ressourcen ebenfalls Zugriff. Das ist ein wichtiger Aspekt bei der Erstellung von Lösungen, die den impliziten OAuth-Fluss mit Bearerzugriffstoken nutzen oder vertrauliche Informationen in Cookies oder im Browserspeicher speichern. Da clientseitige Webparts als Teil der Seite ausgeführt werden, können andere Elemente auf der Seite ebenfalls auf alle diese Ressourcen zugreifen.

### <a name="use-any-library-to-build-your-web-part"></a>Bibliotheksunabhängige Webparterstellung

Bei der Erstellung von Anpassungen mithilfe des Skript-Editor-Webparts haben Sie möglicherweise Bibliotheken wie jQuery und Knockout verwendet, um Ihre Anpassung dynamisch zu machen und sie besser auf Benutzerinteraktionen reagieren zu lassen. Wenn Sie clientseitige SharePoint Framework-Webparts erstellen, können Sie ganz wie bisher auch jede beliebige clientseitige Bibliothek verwenden, um den Funktionsumfang Ihrer Lösung zu erweitern. Ein weiterer Vorteil von SharePoint Framework ist die Isolierung Ihres Skripts. Obwohl das Webpart als Teil der Seite ausgeführt wird, ist das Skript als Modul verpackt. So können beispielsweise mehrere verschiedene Webparts auf ein und derselben Seite jeweils eine andere jQuery-Version verwenden, ohne dass es zu Konflikten kommt. Das ist ein leistungsfähiges Feature, das es Ihnen ermöglicht, sich auf die Schaffung von konkretem geschäftlichem Mehrwert zu konzentrieren; technische Migrationen und Funktionskompromisse sind nicht mehr nötig.

### <a name="run-as-the-current-user"></a>Ausführung als aktueller Benutzer

Bei Skript-Editor-Webpart-Anpassungen war zur Kommunikation mit SharePoint lediglich ein Aufruf der entsprechenden API notwendig. Die clientseitige Lösung wurde im Browser im Kontext des aktuellen Benutzers ausgeführt; da der Authentifizierungscookie automatisch zusammen mit der Anforderung gesendet wurde, konnte die Lösung eine direkte Verbindung zu SharePoint aufbauen. Zur Kommunikation mit SharePoint war also anders als bei der Verwendung von SharePoint-Add-Ins keine zusätzliche Authentifizierung erforderlich. Der gleiche Mechanismus wird auch bei SharePoint Framework-basierten Anpassungen angewendet. Auch sie werden im Kontext des aktuell authentifizierten Benutzers ausgeführt und erfordern keine zusätzlichen Authentifizierungsschritte zur Kommunikation mit SharePoint.

### <a name="use-only-client-side-code"></a>Beschränkung auf clientseitigen Code

Sowohl SharePoint Framework-Lösungen als auch Skript-Editor-Webpart-Lösungen werden im Browser ausgeführt und dürfen ausschließlich clientseitigen JavaScript-Code enthalten. Dabei gelten für clientseitige Lösungen eine Reihe von Einschränkungen: Sie unterstützen beispielsweise keine Rechteerweiterungen in SharePoint und können auch keine Verbindung zu externen APIs aufbauen, die CORS (Cross-Origin Resource Sharing) oder die Authentifizierung per implizitem OAuth-Fluss nicht unterstützen. In solchen Fällen kann die clientseitige Lösung eine serverseitige Remote-API nutzen, die den erforderlichen Vorgang ausführt und die Ergebnisse an den Client zurückgibt.

### <a name="host-solution-in-sharepoint"></a>Lösungshosting in SharePoint

Einer der Vorteile der Erstellung von SharePoint-Anpassungen mithilfe von Skript-Editor-Webparts war die Tatsache, dass der Code in einer normalen SharePoint-Dokumentbibliothek gehostet werden konnte. Verglichen mit SharePoint-Add-Ins war weniger Infrastruktur notwendig, und das Lösungshosting war einfacher. Darüber hinaus konnten Organisationen SharePoint-Berechtigungen verwenden, um den Zugriff auf die Lösungsdateien zu steuern.

Während das Hosting von SharePoint Framework-Lösungen in einem CDN eine Reihe von Vorteilen hat, ist es nicht zwingend erforderlich. Sie könnten den Lösungscode auch in einer normalen SharePoint-Dokumentbibliothek hosten. Im App-Katalog bereitgestellte SharePoint Framework-Pakete (.sppkg-Dateien) geben die URL an, unter der SharePoint Framework den Code der Lösung finden kann. Es gibt keine Einschränkungen hinsichtlich des Ziels dieser URL, solange der Benutzer der Seite mit dem Webpart das Skript von dem angegebenen Speicherort herunterladen kann.

[Office 365 bietet ein öffentliches CDN](https://dev.office.com/blogs/office-365-public-cdn-developer-preview-release), über das Sie Dateien aus einer spezifischen SharePoint-Dokumentbibliothek in einem CDN veröffentlichen können. Das öffentliche CDN von Office 365 ist ein guter Kompromiss zwischen den Vorteilen eines CDN und der Einfachheit des Hostings von Codedateien in einer SharePoint-Dokumentbibliothek. Wenn Ihre Organisation kein Problem darin sieht, Codedateien öffentlich verfügbar zu machen, ist das öffentliche CDN von Office 365 eine interessante Option.

## <a name="differences-between-sharepoint-framework-solutions-and-script-editor-web-part-customizations"></a>Unterschiede zwischen SharePoint-Framework-Lösungen und Skript-Editor-Webpart-Anpassungen

SharePoint-Anpassungen auf SharePoint Framework-Basis und SharePoint-Anpassungen auf Basis des Skript-Editor-Webparts sind einander sehr ähnlich. Beide Anpassungstypen werden als Teil der Seite im Kontext des aktuellen Benutzers ausgeführt und mit clientseitigem JavaScript programmiert. Es gibt aber auch einige wesentliche Unterschiede, die Ihre Architekturentscheidungen beeinflussen könnten und die Sie daher beim Lösungsentwurf berücksichtigen sollten.

### <a name="run-in-no-script-sites"></a>Ausführung auf No-Script-Websites

Bei der Erstellung von clientseitigen Anpassungen mithilfe des Skript-Editor-Webparts mussten sie berücksichtigen, ob die Website, auf der die Anpassung eingesetzt werden sollte, eine No-Script-Website war oder nicht. War die Website eine No-Script-Website, mussten Sie entweder den Administrator bitten, die No-Script-Einstellung zu deaktivieren, oder Ihre Lösung umgestalten, beispielsweise durch eine Umstellung auf das Add-In-Modell.

Da SharePoint Framework-Lösungen über den App-Katalog bereitgestellt und vorab genehmigt werden, fallen sie nicht unter die No-Script-Einschränkungen und funktionieren auf allen Websites.

### <a name="deployed-and-updated-through-it"></a>Bereitstellung und Aktualisierung durch die IT-Abteilung

Skript-Editor-Webparts werden vor allem von sogenannten Citizen Developers zur Erstellung von SharePoint-Anpassungen genutzt: Endbenutzern, die mit von der IT-Abteilung genehmigten Umgebungen und Tools selbstständig Anwendungen entwickeln. Auch wenn sie nur mit Websitebesitzerberechtigungen ausgestattet sind, können Citizen Developers attraktive SharePoint-Anpassungen erstellen, die konkreten geschäftlichen Mehrwert bieten. Muss die Anpassung aktualisiert werden, können Benutzer mit den erforderlichen Berechtigungen Updates auf die Skriptdateien der Lösung anwenden. Diese Änderungen sind dann sofort für alle Benutzer sichtbar.

Skript-Editor-Webpart-Lösungen haben jedoch für die IT-Abteilung einen Nachteil: Sie kann nur schwer nachverfolgen, welche Anpassungen verwendet werden und wo diese Anpassungen verwendet werden. Darüber hinaus hat sie keine Möglichkeit, festzustellen, welche externen Skripts in ihrem Intranet verwendet werden und Zugriff auf ihre Daten haben.

SharePoint Framework gibt der IT-Abteilung die Kontrolle zurück. Da SharePoint Framework-Lösungen zentral im App-Katalog bereitgestellt und verwaltet werden, kann sie jede Lösung vor der Bereitstellung prüfen. Darüber hinaus werden auch alle Updates über den App-Katalog bereitgestellt, sodass auch sie vor der Bereitstellung überprüft und genehmigt werden können.

### <a name="focus-more-on-uniform-user-experience"></a>Verstärkter Fokus auf einer einheitlichen Benutzeroberfläche

Bei der Erstellung von Anpassungen mithilfe des Skript-Editor-Webparts hatten Citizen Developers die Kontrolle über das gesamte DOM ihrer Anpassung. Es gab keine Richtlinien hinsichtlich der Benutzeroberfläche oder der Funktionsweise von Anpassungen. Im Ergebnis erstellte jeder Entwickler seine Anpassungen anders, und die Endbenutzer waren mit vielen unterschiedlichen Benutzeroberflächen konfrontiert.

Eines der Ziele von SharePoint-Framework ist die Standardisierung der Erstellung clientseitiger Anpassungen. Es soll Einheitlichkeit erreicht werden, von der Bereitstellung über die Pflege bis hin zur Benutzeroberfläche. Mithilfe von [Office UI Fabric](http://dev.office.com/fabric) können Entwickler ihre benutzerdefinierten Lösungen leichter so gestalten, dass sie im Hinblick auf visuelles Design und Verhalten wie ein integraler Bestandteil von SharePoint wirken. Das fördert die Akzeptanz auf Benutzerseite. Die SharePoint Framework-Toolkette generiert Paketdateien für die Lösungen, die im App-Katalog bereitgestellt werden, sowie Skriptbundles, die an einem frei wählbaren Hostingspeicherort bereitgestellt werden. Aufbau und Verwaltungsprozess sind bei jeder Lösung gleich.

### <a name="dont-modify-dom-outside-of-the-customization"></a>Keine DOM-Modifizierung außerhalb der Anpassung

In der Vergangenheit wurden Skript-Editor-Webparts häufig eingesetzt, um Teile einer Seite zu ändern, so beispielsweise um die Symbolleiste um zusätzliche Schaltflächen zu erweitern oder die Überschrift oder das Branding der Seite anzupassen. Solche Anpassungen waren von bestimmten DOM-Elementen abhängig; bei jeder Aktualisierung der SharePoint-Benutzeroberfläche bestand daher ein Risiko, das sie anschließend nicht mehr funktionierten.

SharePoint-Framework fördert eine strukturierte und zuverlässige Vorgehensweise bei der Anpassung von SharePoint. Statt spezifische DOM-Elemente zur Anpassung von SharePoint zu verwenden, gibt SharePoint Framework Entwicklern eine öffentliche API an die Hand, mit deren Hilfe sie SharePoint erweitern können. Aktuell unterstützt SharePoint Framework als Form ausschließlich clientseitige Webparts. Die zukünftige Implementierung von Unterstützung für weitere Formen wie beispielsweise JSLink-Äquivalenten und benutzerdefinierten Benutzeraktionen wird aktuell [geprüft](https://dev.office.com/sharepoint/docs/spfx/roadmap). Ziel ist es, dass Entwickler mit SharePoint Framework die gängigsten Anpassungsszenarien implementieren können.

### <a name="distributed-as-packages"></a>Verteilung im Paketformat

Clientseitige SharePoint-Anpassungen verwenden zur Speicherung ihrer Daten häufig SharePoint-Listen und -Bibliotheken. Bei Skript-Editor-Webpart-Anpassungen war eine automatische Bereitstellung der hierzu erforderlichen Komponenten schwierig. Sollte eine Anpassung auch auf einer anderen Website bereitgestellt werden, musste häufig nicht nur das Webpart kopiert, sondern auch der benötigte Datenspeicher korrekt neu erstellt und gepflegt werden.

SharePoint Framework-Lösungen werden als Pakete verteilt, die ihre erforderlichen Komponenten wie Felder, Inhaltstypen und Listen selbst automatisch bereitstellen können. Entwickler können bei der Erstellung des Pakets angeben, welche Artefakte die Lösung erfordert; wann immer die Lösung dann auf einer Website installiert wird, werden die betreffenden Artefakte erstellt. Dadurch wird es deutlich einfacher, die Lösung auf mehreren Websites bereitzustellen und zu verwalten.

### <a name="use-typescript-for-building-more-robust-and-easier-to-maintain-solution"></a>Verwendung von TypeScript für stabilere und einfacher zu pflegende Lösungen

Bei der Erstellung von Script-Editor-Webpart-Anpassungen haben Citizen Developers oft reines JavaScript verwendet. Solche Lösungen enthielten häufig keinerlei automatisierte Tests, und die Codeumgestaltung war fehleranfällig.

Mit SharePoint Framework können Entwickler bei der Lösungserstellung das TypeScript-Typensystem verwenden. Dank dieses Typensystems fallen Fehler bereits während der Entwicklung auf, nicht erst zur Laufzeit. Auch die Codeumgestaltung ist einfacher, weil Änderungen am Code durch TypeScript gesichert werden. Da jeder JavaScript-Code gültiger TypeScript-Code ist, ist die Einstiegshürde niedrig, und Sie können Ihren reinen JavaScript-Code schrittweise zu TypeScript migrieren. Das macht die Lösungspflege einfacher.

### <a name="cant-rely-on-the-sppagecontextinfo-object"></a>Keine Unterstützung für das spPageContextInfo-Objekt

In der Vergangenheit nutzten Entwickler bei der Erstellung wiederverwendbarer clientseitiger Anpassungen das JavaScript-Objekt **spPageContextInfo**, um Informationen über die aktuelle Seite, die aktuelle Website oder den aktuellen Benutzer abzurufen. Dieses Objekt bot eine einfache Möglichkeit, die Lösung auf mehreren SharePoint-Websites wiederzuverwenden und feste URLs zu vermeiden.

Doch obwohl das Objekt **spPageContextInfo** auf klassischen SharePoint-Seiten noch im Einsatz ist, lässt es sich mit modernen SharePoint-Seiten und -Bibliotheken nicht zuverlässig verwenden. Entwicklern von SharePoint Framework-Lösungen empfehlen wir stattdessen die Verwendung des Objekts **[IWebPartContext.pageContext](https://dev.office.com/sharepoint/reference/spfx/sp-webpart-base/iwebpartcontext)**, das die Kontextinformationen der jeweiligen Lösung enthält.

### <a name="no-access-to-sharepoint-javascript-object-model-by-default"></a>Kein standardmäßiger Zugriff auf das SharePoint JavaScript-Objektmodell

Bei der Erstellung clientseitiger Anpassungen für die klassische SharePoint-Benutzeroberfläche verwendeten viele Entwickler das JavaScript-Objektmodell (JSOM) zur Kommunikation mit SharePoint. JSOM bot IntelliSense und einfachen Zugriff auf die SharePoint-API, ähnlich wie das clientseitige Objektmodell (CSOM). Auf klassischen SharePoint-Seiten war die Kernkomponente von JSOM standardmäßig implementiert, und Entwickler konnten zusätzliche Komponenten laden, beispielsweise zur Kommunikation mit der SharePoint-Suche.

In der modernen SharePoint-Benutzeroberfläche ist SharePoint JSOM nicht standardmäßig implementiert. Zwar können Entwickler es selbst laden, doch empfehlen wir stattdessen die Verwendung der REST-API. REST ist universeller und lässt sich mit unterschiedlichen clientseitigen Bibliotheken wie jQuery, Angular und React verwenden.

Microsoft investiert nicht mehr aktiv in JSOM. Wenn Sie die Arbeit mit einer API bevorzugen, können Sie alternativ die [SharePoint Patterns and Practices JavaScript Core Library](https://github.com/SharePoint/PnP-JS-Core) verwenden, die eine Fluent-API sowie TypeScript-Typisierungen bietet.

## <a name="migrate-existing-customization-to-the-sharepoint-framework"></a>Migrieren vorhandener Anpassungen zu SharePoint-Framework

Eine Migration vorhandener Skript-Editor-Webpart-Anpassungen zu SharePoint Framework hat sowohl für Endbenutzer als auch für Entwickler Vorteile. Wenn Sie sich für eine Migration vorhandener Anpassungen zu SharePoint Framework entscheiden, können Sie entweder so viel ihrer vorhandenen Skripts wie möglich wiederverwenden oder die Anpassung komplett neu schreiben.

### <a name="reuse-existing-scripts"></a>Wiederverwenden vorhandener Skripts

Wenn Sie vorhandene Skript-Editor-Webpart-Anpassungen zu SharePoint Framework migrieren, können Sie Ihre bereits vorhandenen Skripts wiederverwenden. Obwohl SharePoint Framework gezielt auf die Verwendung von TypeScript ausgelegt ist, können Sie problemlos reines JavaScript verwenden und Ihren Code schrittweise auf TypeScript umstellen. Falls Sie eine Lösung nur während eines bestimmten Zeitraums unterstützen müssen oder Ihr Budget begrenzt ist, ist diese Strategie vielleicht ausreichend.

Es ist nicht immer möglich, bereits vorhandene Skripts in einer SharePoint-Framework-Lösung wiederzuverwenden. SharePoint Framework-Lösungen werden beispielsweise als JavaScript-Module verpackt und laden asynchron auf der Seite. Einige JavaScript-Bibliotheken funktionieren aber nicht einwandfrei, wenn sie in einem Modul referenziert werden, oder müssen auf eine bestimmte Art und Weise referenziert werden. Darüber hinaus können die Einbindung von Seitenereignissen wie `onload` oder der Einsatz der jQuery-Funktion `ready` zu unerwünschten Ergebnissen führen.

In Anbetracht der Vielzahl von JavaScript-Bibliotheken lässt sich vorab kaum einschätzen, ob Ihre vorhandenen Skripts in einer gegebenen SharePoint Framework-Lösung wiederverwendet werden können oder ob Sie die Anpassung doch neu schreiben müssen. Sie haben nur die Möglichkeit, die einzelnen Komponenten in eine SharePoint Framework-Lösung zu überführen und zu testen, ob sie wie erwartet funktionieren.

### <a name="rewrite-the-customization"></a>Neuschreiben der Anpassung

Wenn Sie Ihre Lösung über einen längeren Zeitraum unterstützen müssen, Sie SharePoint Framework effektiver nutzen möchten oder Ihre vorhandenen Skripts sich nicht mit SharePoint Framework wiederverwenden lassen, müssen Sie Ihre Anpassung möglicherweise komplett neu schreiben. Das ist zwar teurer als die Wiederverwendung vorhandener Skripts, führt aber langfristig zu besseren Ergebnissen: einer leistungsfähigeren Lösung, die sich einfacher pflegen und nutzen lässt.

Bei der Umschreibung einer vorhandenen Skript-Editor-Webpart-Anpassung in eine SharePoint Framework-Lösung sollten Sie immer von der gewünschten Funktion ausgehen. Ziehen Sie zur Implementierung der Benutzeroberfläche Office UI Fabric in Betracht, damit Ihre Lösung wie ein integraler Bestandteil von SharePoint aussieht. Für die Realisierung von spezifischen Komponenten wie Diagrammen oder Schiebereglern sollten Sie auf moderne Bibliotheken zurückgreifen, die als Modul verteilt werden und über TypeScript-Typisierungen verfügen. Das macht es einfacher, die Komponenten in die Lösung zu integrieren.

Es gibt zwar keine allgemeingültige Antwort auf die Frage, welche Komponente für welches Szenario am besten geeignet ist; SharePoint Framework ist jedoch flexibel genug, um die meisten gängigen Szenarien unterstützen zu können. Mithilfe dieses Modells sollte es Ihnen gelingen, Ihre vorhandenen clientseitigen Anpassungen in SharePoint Framework-Lösungen mit vollem Funktionsumfang zu überführen.

### <a name="migration-tips"></a>Tipps für die Migration

Bei der Umgestaltung vorhandener Skript-Editor-Webpart-Anpassungen in SharePoint Framework-Anpassungen gibt es einige häufige Muster.

#### <a name="move-existing-code-to-sharepoint-framework"></a>Überführen des vorhandenen Codes nach SharePoint Framework

SharePoint-Anpassungen auf Basis des Skript-Editor-Webparts bestehen oft aus in das Webpart integriertem HTML-Markup und einem oder mehreren Verweisen auf JavaScript-Dateien. Wenn Sie eine vorhandene Anpassung in eine SharePoint-Framework-Lösung überführen, müssen Sie das HTML-Markup aus dem Skript-Editor-Webpart höchstwahrscheinlich in die Methode **render** des clientseitigen SharePoint Framework-Webparts verschieben. Verweise auf externe Skripts müssen in Verweise in der Eigenschaft **externals** in der Datei **config.json** umgeändert werden. Interne Skripts müssen Sie in den Quellordner des Webparts kopieren und mithilfe von Anweisungen des Typs **require()** aus der Webpartklasse referenzieren.

#### <a name="reference-functions-from-script-files"></a>Referenzieren von Funktionen aus Skriptdateien

Zur Referenzierung von Funktionen aus Skriptdateien müssen Sie die Funktionen als Export definieren. Nehmen wir als Beispiel eine bereits vorhandene JavaScript-Datei, die Sie in einem clientseitigen SharePoint Framework-Webpart verwenden möchten:

```js
var greeting = function() {
  alert('How are you doing?');
  return false;
}
```

Um die Funktion **greeting** aus der Webpartklasse aufrufen zu können, müssen Sie die JavaScript-Datei wie folgt ändern:

```js
var greeting = function() {  
  alert('How are you doing?');
  return false;
}

module.exports = {  
  greeting: greeting
};
```

Anschließend können Sie in der Webpartklasse auf das Skript verweisen und die Funktion **greeting** aufrufen:

```ts
public render(): void {  
  this.domElement.innerHTML = `
    <input type="button" value="Click me"/>`;

  const myScript = require('./my-script.js');
  this.domElement.querySelector('input').addEventListener('click', myScript.greeting);
}
```

#### <a name="execute-ajax-calls"></a>Ausführen von AJAX-Aufrufen

Viele clientseitige Anpassungen verwenden jQuery zur Ausführung von AJAX-Anforderungen, aufgrund seiner Einfachheit und seiner browserübergreifenden Kompatibilität. Falls Sie jQuery nur dafür verwenden: Sie können AJAX-Aufrufe auch über den Standard-HTTP-Client von SharePoint Framework ausführen. SharePoint Framework bietet zwei Typen von HTTP-Clients: [SPHttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/sphttpclient) zur Ausführung von Anforderungen an die SharePoint-REST-API und [HttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/httpclient) zur Ausgabe von Webanforderungen an andere REST-APIs. Einen Aufruf mit SPHttpClient zum Abrufen des Titels der aktuellen SharePoint-Website würden Sie wie folgt ausführen:

```ts
this.context.spHttpClient.get(`${this.context.pageContext.web.absoluteUrl}/_api/web?$select=Title`,
SPHttpClient.configurations.v1,
{
  headers: {
    'Accept': 'application/json;odata=nometadata',
    'odata-version': ''
  }
})
.then((response: SPHttpClientResponse): Promise<{Title: string}> => {
  return response.json();
})
.then((web: {Title: string}): void => {
  // web.Title
}, (error: any): void => {
  // error
});
```

## <a name="more-information"></a>Weitere Informationen

- [Migrate SharePoint JavaScript customizations to SharePoint Framework - reference functions from script files](https://blog.mastykarz.nl/migrate-sharepoint-javascript-customizations-sharepoint-framework-reference-functions/)
- [Migrate SharePoint JavaScript customizations to SharePoint Framework – jQuery AJAX calls and showing data](https://rencore.com/blog/migrate-sharepoint-javascript-customizations-to-sharepoint-framework-jquery-ajax-calls-and-showing-data/)
