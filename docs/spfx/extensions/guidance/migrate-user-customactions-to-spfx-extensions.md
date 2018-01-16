---
title: "Migrieren von UserCustomAction-/ECB-Menüelementen zu SharePoint-Framework-Erweiterungen"
ms.date: 12/19/2017
ms.prod: sharepoint
ms.openlocfilehash: 50540de75666a8a43697d1f31259713edc06108c
ms.sourcegitcommit: bf4bc1e80c6ef1a0ff479039ef9ae0ee84d5f6b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2017
---
# <a name="migrating-user-customaction--ecb-menu-items-to-sharepoint-framework-extensions"></a>Migrieren von UserCustomAction-/ECB-Menüelementen zu SharePoint-Framework-Erweiterungen

SharePoint-Framework ist ein neues Modell zur Erstellung von SharePoint-Anpassungen. Wenn Sie SharePoint mit benutzerdefinierten Benutzeraktionen und benutzerdefinierten ECB-Menüelementen (Edit Control Block) unter Verwendung von SharePoint-Featureframework angepasst haben, fragen Sie sich möglicherweise, welche Vorteile die Migration von diesen zu dem neuen SharePoint-Framework bietet.

Bei der Entwicklung von SharePoint-Framework-Erweiterungen sind folgende Optionen verfügbar:

* **Application Customizer**: Erweiterung der nativen modernen Benutzeroberfläche von SharePoint Online, indem benutzerdefinierte Elemente und clientseitiger Code den vordefinierten Platzhaltern der modernen Seiten hinzugefügt werden. Zu der Zeit, zu der dieser Artikel verfasst wurde, waren die verfügbaren Platzhalter die Kopf- und Fußzeile jeder modernen Seite.
* **Command Set**: Benutzerdefinierte ECB-Menüelemente oder benutzerdefinierte Schaltflächen können der Befehlsleiste einer Listenansicht für eine Liste oder Bibliothek hinzugefügt werden. Sie können diesen Befehlen eine JavaScript (TypeScript)-Aktion zuordnen.
* **Field Customizer**: Anpassung der Darstellung eines Felds in einer Listenansicht mit benutzerdefinierten HTML-Elementen und clientseitigem Code.

Je nach Ziel der Anpassung können Sie eine der oben genannten Konfigurationen nutzen.
**Application Customizer** sind zum Beispiel ein hervorragender Ersatz für benutzerdefinierte Benutzeraktionen.
**Befehlssätze** sind dagegen ein entsprechender Ersatz für die ECB-Menüelemente.

## <a name="benefit-of-migrating-existing-sharepoint-feature-framework-customizations-to-the-sharepoint-framework"></a>Vorteile einer Migration vorhandener SharePoint-Framework-Anpassungen zu SharePoint-Framework

SharePoint-Framework wurde für die neue „moderne“ SharePoint-Oberfläche konzipiert, welche auf modernen Teamwebsites und modernen Kommunikationswebsites für alle Geräte und Plattformen verfügbar sind.

### <a name="the-only-supported-way-of-customizing-no-script-modern-sites"></a>Die einzige unterstützte Möglichkeit zum Anpassen von modernen No-Script-Websites 

Einer der Hauptvorteile der Migration bisheriger SharePoint-Featureframework-Anpassungen zu SharePoint-Framework ist, dass dies die einzige unterstützte Methode zum Anpassen der Benutzeroberfläche auf modernen Websites ist.
Bei modernen Websites ist die Kennzeichnung „Kein Skript“ aktiviert, wodurch in die Seite integrierte Skripts nicht ausgeführt werden, sowie benutzerdefinierte Benutzeraktionen, die sich auf externen JavaScript- oder integrierten JavaScript-Code beziehen.
Bisherige benutzerdefinierte Benutzeraktionen funktionieren nicht in der modernen Benutzeroberfläche. Darüber hinaus sind die ECB-Anpassungen, die bei Verwendung des Featureframework integriert sind, sehr eingeschränkt. Sie können zum Beispiel nur ECB-Elemente definieren, die sich nicht auf die externe JavaScript-Datei beziehen oder keine integrierten JavaScript-Aufrufe verwenden. Daher müssen Sie, wenn Sie die moderne Benutzeroberfläche erweitern möchten, auf SharePoint-Framework aktualisieren.

### <a name="easier-access-to-information-in-sharepoint-and-office-365"></a>Einfacherer Zugriff auf Informationen in SharePoint und Office 365

Ein weiterer, zu berücksichtigender Aspekt ist, dass in dem bisherigen Modell von benutzerdefinierten Benutzeraktionen und ECB-Anpassungen SharePoint-Inhalte und -Daten nicht problemlos genutzt werden konnten. Die einzige Möglichkeit bestand in der Verwendung von JSOM (clientseitiges JavaScript-Objektmodell von SharePoint) oder Low-Level-REST-APIs. Darüber hinaus war es fast unmöglich, alle Dienste von Office 365 zu nutzen, es sei denn, Sie haben ADAL.JS (Azure Active Directory Authentication Library für JavaScript) und benutzerdefinierten JavaScript-Code eigenständig verwendet.
Heutzutage kann mit SharePoint-Framework und den SharePoint-Framework-Erweiterungen problemlos sowohl die SharePoint-REST-API als auch Microsoft Graph verwendet werden.
Daher können Sie nun leistungsstarke Lösungen erstellen, die alle von Microsoft Office 365 bereitgestellten Dienst verwenden und mit diesen interagieren können.

## <a name="similarities-between-sharepoint-framework-solutions-and-sharepoint-feature-framework-customizations"></a>Ähnlichkeiten zwischen SharePoint-Framework-Lösungen und SharePoint-Featureframework-Anpassungen

Benutzerdefinierte Benutzeraktionen und ECB-Elemente von SharePoint-Featureframework und SharePoint-Featureframework-Anpassungen weisen einige Ähnlichkeiten auf. 

### <a name="provisioning-model"></a>Bereitstellungsmodell

Sowohl SharePoint-Framework-Erweiterungen als auch Lösungen für benutzerdefinierte Aktionen oder ECB-Menüelemente verwenden eine XML-Manifestdatei, die nahezu die SharePoint-Featureframework-Syntax aufweist. Daher basiert die Bereitstellung auf der gleichen Methode.

### <a name="run-as-a-part-of-the-page"></a>Ausführung als Teil der Seite

Ähnlich wie benutzerdefinierte Aktionen und ECB von SharePoint-Featureframework sind SharePoint-Erweiterungen Teil der Seite. Damit haben diese Lösungen Zugriff auf das DOM der Seite und können mit anderen Komponenten auf der Seite kommunizieren. Zusätzlich macht diese Tatsache es Entwicklern leichter, ihre Lösungen dynamisch zu gestalten, sodass sie sich an die verschiedenen Formfaktoren anpassen können, in denen eine SharePoint-Seite angezeigt werden kann. Unter anderem wird auch die mobile SharePoint-App unterstützt.
Basierend auf der Tatsache, dass SharePoint-Framework-Erweiterungen als Teil der Seite ausgeführt haben, können unabhängig davon, auf welche Ressourcen die jeweilige Anpassung Zugriff hat, auch andere Elemente auf der Seite auf diese zugreifen. Das ist ein wichtiger Aspekt bei der Erstellung von Lösungen, die den impliziten OAuth-Fluss mit Bearerzugriffstoken nutzen oder vertrauliche Informationen in Cookies oder im Browserspeicher speichern. Da SharePoint-Framework-Erweiterungen als Teil der Seite ausgeführt werden, können andere Elemente auf der Seite ebenfalls auf alle diese Ressourcen zugreifen.

### <a name="use-any-library-to-build-your-extensions"></a>Bibliotheksunabhängige Erweiterungserstellung

Bei der Erstellung von Seitenanpassungen mithilfe von benutzerdefinierten Aktionen haben Sie möglicherweise Bibliotheken wie jQuery und Knockout verwendet, um Ihre Anpassung dynamisch zu machen und sie besser auf Benutzerinteraktionen reagieren zu lassen. Wenn Sie SharePoint-Framework-Erweiterungen erstellen, können Sie ganz wie bisher auch jede beliebige clientseitige Bibliothek verwenden, um den Funktionsumfang Ihrer Lösung zu erweitern. Ein weiterer Vorteil von SharePoint-Framework ist die Isolierung Ihres Skripts. Obwohl das Webpart als Teil der Seite ausgeführt wird, ist das Skript als Modul verpackt. So können beispielsweise mehrere verschiedene Erweiterungen auf ein und derselben Seite jeweils eine andere jQuery-Version verwenden, ohne dass es zu Konflikten kommt. Das ist ein leistungsfähiges Feature, das es Ihnen ermöglicht, sich auf die Schaffung von konkretem geschäftlichem Mehrwert zu konzentrieren; technische Migrationen und Funktionskompromisse sind nicht mehr nötig.

### <a name="run-as-the-current-user"></a>Ausführung als aktueller Benutzer

Bei Anpassungen mithilfe von benutzerdefinierten Benutzeraktionen und ECB-Menüelementen war zur Kommunikation mit SharePoint lediglich ein Aufruf der entsprechenden API notwendig. Die clientseitige Lösung wurde im Browser im Kontext des aktuellen Benutzers ausgeführt; da der Authentifizierungscookie automatisch zusammen mit der Anforderung gesendet wurde, konnte die Lösung eine direkte Verbindung zu SharePoint aufbauen. Zur Kommunikation mit SharePoint war also anders als bei der Verwendung von SharePoint-Add-Ins keine zusätzliche Authentifizierung erforderlich. Der gleiche Mechanismus wird auch bei SharePoint Framework-basierten Anpassungen angewendet. Auch sie werden im Kontext des aktuell authentifizierten Benutzers ausgeführt und erfordern keine zusätzlichen Authentifizierungsschritte zur Kommunikation mit SharePoint.

Natürlich bezieht sich der Sicherheitskontext auf den aktuell verbundenen Benutzer. Das bedeutet, dass Sie unter dem Aspekt der Sicherheit, beim Installieren von SharePoint-Framework-Erweiterungen in einer beliebigen Zielwebsitesammlung sorgfältig vorgehen müssen.

### <a name="use-only-client-side-code"></a>Beschränkung auf clientseitigen Code

Sowohl SharePoint-Framework-Erweiterungen als auch Lösungen für benutzerdefinierte Benutzeraktionen oder ECB-Menüelemente werden im Browser ausgeführt und dürfen ausschließlich clientseitigen JavaScript-Code enthalten. Dabei gelten für clientseitige Lösungen eine Reihe von Einschränkungen: Sie unterstützen beispielsweise keine Rechteerweiterungen in SharePoint und können auch keine Verbindung zu externen APIs aufbauen, die CORS (Cross-Origin Resource Sharing) oder die Authentifizierung per implizitem OAuth-Fluss nicht unterstützen. In solchen Fällen kann die clientseitige Lösung eine serverseitige Remote-API nutzen, die den erforderlichen Vorgang ausführt und die Ergebnisse an den Client zurückgibt.

### <a name="hosting-model-self-consistent-and-based-on-office-365"></a>In sich stimmiges und auf Office 365 basierendes Hostingmodell

Sowohl SharePoint-Framework-Erweiterungen als auch Lösungen für benutzerdefinierte Benutzeraktionen oder ECB-Menüelemente können in SharePoint Online und schließlich im Office 365-CDN-Dienst gehostet werden, ohne dass externe Dienste oder Hostingumgebungen erforderlich sind.

Während das Hosting von SharePoint Framework-Lösungen in einem CDN eine Reihe von Vorteilen hat, ist es nicht zwingend erforderlich. Sie könnten den Lösungscode auch in einer normalen SharePoint-Dokumentbibliothek hosten. Im App-Katalog bereitgestellte SharePoint-Framework-Pakete (.sppkg-Dateien) geben die URL an, unter der SharePoint-Framework den Code der Lösung finden kann. Es gibt keine Einschränkungen hinsichtlich des Ziels dieser URL, solange der Benutzer der Seite mit der Erweiterung das Skript von dem angegebenen Speicherort herunterladen kann.
Office 365 bietet ein öffentliches CDN, über das Sie Dateien aus einer spezifischen SharePoint-Dokumentbibliothek in einem CDN veröffentlichen können. Das öffentliche CDN von Office 365 ist ein guter Kompromiss zwischen den Vorteilen eines CDN und der Einfachheit des Hostings von Codedateien in einer SharePoint-Dokumentbibliothek. Wenn Ihre Organisation kein Problem darin sieht, Codedateien öffentlich verfügbar zu machen, ist das öffentliche CDN von Office 365 eine interessante Option.

## <a name="differences-between-sharepoint-framework-solutions-and-sharepoint-feature-framework-customizations"></a>Unterschiede zwischen SharePoint-Framework-Lösungen und SharePoint-Featureframework-Anpassungen

Zwischen den beiden Entwicklungsmodellen gibt es jedoch auch einige wesentliche Unterschiede, die Sie beim Entwerfen der Architektur Ihrer Lösungen berücksichtigen sollten.

### <a name="run-in-no-script-sites"></a>Ausführung auf No-Script-Websites

Da SharePoint-Framework-Lösungen einschließlich Erweiterungen über den App-Katalog bereitgestellt und vorab genehmigt werden, fallen sie nicht unter die No-Script-Einschränkungen und funktionieren auf allen modernen Websites.

### <a name="pre-defined-set-of-extensibility-points"></a>Vordefinierten Satz von Erweiterungspunkten

Während eine benutzerdefinierte Benutzeraktion JavaScript-Code einbetten kann, der das DOM eines beliebigen Teils der Seite aktualisieren oder tatsächlich ändern kann, kann eine SharePoint-Framework-Erweiterung wie Application Customizer am Ende dieses Schreibvorgangs nur die Kopf- und/oder die Fußzeile einer beliebigen modernen Seite anpassen.

Theoretisch könnten Sie mit DOM einen Application Customizer erstellen,der die Struktur einer Seite vollständig ändern kann, wie dies bei benutzerdefinierten Benutzeraktionen der Fall war. Trotzdem förder SharePoint-Framework eine strukturierte und zuverlässige Vorgehensweise bei der Anpassung von SharePoint. Statt der Verwendung bestimmter DOM-Elemente bietet SharePoint-Framework Entwicklern bestimmte Hooks und Platzhalter für Anpassungen. Nur diese sollten verwendet werden.

### <a name="use-typescript-for-building-more-robust-and-easier-to-maintain-solution"></a>Verwendung von TypeScript für stabilere und einfacher zu pflegende Lösungen

Bei der Erstellung von Anpassungen mithilfe von benutzerdefinierten Benutzeraktionen oder ECB-Menüelementen haben Entwickler oft reines JavaScript verwendet. Solche Lösungen enthielten häufig keinerlei automatisierte Tests, und die Codeumgestaltung war fehleranfällig.
Mit SharePoint Framework können Entwickler bei der Lösungserstellung das TypeScript-Typensystem verwenden. Dank dieses Typensystems fallen Fehler bereits während der Entwicklung auf, nicht erst zur Laufzeit. Auch die Codeumgestaltung ist einfacher, weil Änderungen am Code durch TypeScript gesichert werden. Da jeder JavaScript-Code gültiger TypeScript-Code ist, ist die Einstiegshürde niedrig, und Sie können Ihren reinen JavaScript-Code schrittweise zu TypeScript migrieren. Das macht die Lösungspflege einfacher.

### <a name="no-access-to-sharepoint-javascript-object-model-by-default"></a>Kein standardmäßiger Zugriff auf das SharePoint JavaScript-Objektmodell

Bei der Erstellung clientseitiger Anpassungen für die klassische SharePoint-Benutzeroberfläche verwendeten viele Entwickler das JavaScript-Objektmodell (JSOM) zur Kommunikation mit SharePoint. JSOM bot IntelliSense und einfachen Zugriff auf die SharePoint-API, ähnlich wie das clientseitige Objektmodell (CSOM). Auf klassischen SharePoint-Seiten war die Kernkomponente von JSOM standardmäßig implementiert, und Entwickler konnten zusätzliche Komponenten laden, beispielsweise zur Kommunikation mit der SharePoint-Suche.
In der modernen SharePoint-Benutzeroberfläche ist SharePoint JSOM nicht standardmäßig implementiert. Obwohl Entwickler es selbst laden können, wird empfohlen, stattdessen die REST-API oder SharePoint Patterns and Practices JavaScript Core Library (PnP JS Library) zu verwenden, die die SharePoint-REST-API intern verwendet. REST ist universeller und lässt sich mit unterschiedlichen clientseitigen Bibliotheken wie jQuery, Angular und React verwenden.
Microsoft investiert nicht mehr aktiv in JSOM. Wenn Sie die Arbeit mit einer API bevorzugen, können Sie alternativ die PnP JS Library verwenden, die eine Fluent-API sowie TypeScript-Typisierungen bietet.

## <a name="migrate-existing-customization-to-the-sharepoint-framework-extensions"></a>Migrieren vorhandener Anpassungen zu SharePoint-Framework-Erweiterungen

Eine Migration vorhandener Anpassungen zu SharePoint-Framework-Erweiterungen hat sowohl für Endbenutzer als auch für Entwickler Vorteile. Wenn Sie sich für eine Migration vorhandener Anpassungen zu SharePoint-Framework entscheiden, können Sie entweder so viel ihrer vorhandenen JavaScript-Skripts wie möglich wiederverwenden oder die Anpassung mithilfe von TypeScript komplett neu schreiben.

### <a name="reuse-existing-scripts"></a>Wiederverwenden vorhandener Skripts

Wenn Sie vorhandene Anpassungen zu SharePoint-Framework-Erweiterungen migrieren, können Sie Ihre bereits vorhandenen Skripts wiederverwenden. Obwohl SharePoint Framework gezielt auf die Verwendung von TypeScript ausgelegt ist, können Sie problemlos reines JavaScript verwenden und Ihren Code schrittweise auf TypeScript umstellen. Falls Sie eine Lösung nur während eines bestimmten Zeitraums unterstützen müssen oder Ihr Budget begrenzt ist, ist diese Strategie vielleicht ausreichend.

Es ist nicht immer möglich, bereits vorhandene Skripts in einer SharePoint-Framework-Lösung wiederzuverwenden. In Anbetracht der Vielzahl von JavaScript-Bibliotheken lässt sich vorab kaum einschätzen, ob Ihre vorhandenen Skripts in einer gegebenen SharePoint-Framework-Lösung wiederverwendet werden können oder ob Sie die Anpassung doch neu schreiben müssen. Sie haben nur die Möglichkeit, die einzelnen Komponenten in eine SharePoint-Framework-Lösung zu überführen und zu testen, ob sie wie erwartet funktionieren.

### <a name="rewrite-the-customization"></a>Neuschreiben der Anpassung

Wenn Sie Ihre Lösung über einen längeren Zeitraum unterstützen müssen, Sie SharePoint Framework effektiver nutzen möchten oder Ihre vorhandenen Skripts sich nicht mit SharePoint Framework wiederverwenden lassen, müssen Sie Ihre Anpassung möglicherweise komplett neu schreiben. Das ist zwar teurer als die Wiederverwendung vorhandener Skripts, führt aber langfristig zu besseren Ergebnissen: einer leistungsfähigeren Lösung, die sich einfacher pflegen und nutzen lässt.

Bei der Umschreibung einer vorhandenen Anpassung in eine SharePoint-Framework-Lösung sollten Sie immer von der gewünschten Funktion ausgehen. Ziehen Sie zur Implementierung der Benutzeroberfläche Office UI Fabric in Betracht, damit Ihre Lösung wie ein integraler Bestandteil von SharePoint aussieht. 

## <a name="more-information"></a>Weitere Informationen

Weitere Informationen zur Migration von benutzerdefinierten Benutzeraktionen und benutzerdefinierten ECB-Menüelementen (Edit Control Block) zu SharePoint-Framework-Erweiterungen finden Sie in den folgenden Lernprogrammen:

* [Lernprogramm: Migrieren von UserCustomAction zu SharePoint-Framework-Erweiterungen](./migrate-from-usercustomactions-to-spfx-extensions.md)
* [Lernprogramm: Migrieren vom Edit Control Block-Menüelement (ECB) zu SharePoint-Framework-Erweiterungen](./migrate-from-ecb-to-spfx-extensions.md)