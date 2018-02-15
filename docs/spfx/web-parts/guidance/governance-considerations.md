---
title: "Sharepoint Framework-Lösungen – Überlegungen zum Thema Governance"
description: "Um die Vorteile von SharePoint-Framework-Lösungen optimal nutzen zu können, sollte Ihr Unternehmen über einen umsetzbaren Governanceplan verfügen, der die wichtigsten Überlegungen zur Projektverwaltung abdeckt."
ms.date: 01/26/2018
ms.prod: sharepoint
ms.openlocfilehash: 7e00979261ba23a58352d6f963e8cddd6dfc1357
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-framework-solutions-governance-considerations"></a>Sharepoint Framework-Lösungen – Überlegungen zum Thema Governance

Mithilfe des SharePoint-Frameworks können Organisationen problemlos Lösungen erstellen, die die in SharePoint und Office 365 verfügbaren Funktionen besser nutzen. SharePoint Framework-Lösungen funktionieren mit modernen Webtechnologien sowie verschiedenen mobilen Geräten, sodass Sie produktive Benutzerumgebungen und Apps bereitstellen können, die vom ersten Tag an schnell reagieren und für Mobilgeräte geeignet sind. Um die Vorteile von SharePoint-Framework-Lösungen optimal nutzen zu können, sollte Ihr Unternehmen über einen umsetzbaren Governanceplan verfügen, der die wichtigsten Überlegungen zur Projektverwaltung abdeckt.

## <a name="anatomy-of-sharepoint-framework-solutions"></a>Anatomie von SharePoint Framework-Lösungen

![Diagramm zum Aufbau von SharePoint Framework-Lösungen](../../../images/guidance-governance-spfx-structure-schema.png)

SharePoint Framework-Lösungen bestehen aus zwei Teilen: Code (häufig als Webpart-Paket bezeichnet), der einer URL bereitgestellt wird, und einer SPPKG-Datei mit dem Webpart-Manifest und einer URL, die auf den Speicherort verweist, an dem der Code für das Webpart bereitgestellt wird. Es gibt keine spezifischen Einschränkungen im Hinblick auf den Bereitstellungsort des Codes, solange Benutzer, die mit dem Webpart arbeiten, auf den Webpart-Code zugreifen können. Organisationen können ihre Webparts z. B. im [öffentlichen Office 365-CDN](https://dev.office.com/blogs/office-365-public-cdn-developer-preview-release), in [Azure Storage](../get-started/deploy-web-part-to-cdn.md) oder auf einem privaten Webserver bereitstellen.

## <a name="web-part-code-hosting-location-considerations"></a>Überlegungen zum Hostingspeicherort von Webpart-Code

Das Wichtigste, was Organisationen vor der Bereitstellung von SharePoint Framework-Lösungen wissen müssen, ist der Ort, an dem der Code der Lösung bereitgestellt werden soll. SharePoint Framework-Lösungen werden als Teil der Seite im Kontext des aktuellen Benutzers ausgeführt. Dies bedeutet: Alles, was der Benutzer tun darf, darf auch der Webpart-Code tun. Im Gegensatz zu SharePoint-Add-Ins wird auf SharePoint Framework-Lösungen kein separater Berechtigungsbereich angewendet. Daher sollten SharePoint-Administratoren SharePoint-Framework-Lösungen als besonders vertrauenswürdige Lösungen behandeln – auf die gleiche Weise, wie sie lokale Farmlösungen behandeln. Der Ort, an dem der Webpart-Code bereitgestellt wird, ist aus einer Reihe von Gründen wichtig. 

Berücksichtigen Sie folgende Überlegungen zum Speicherort:

### <a name="is-the-code-hosting-location-supported-by-the-organization"></a>Wird der Hostingspeicherort des Codes von der Organisation unterstützt?

In SharePoint-Framework gibt es keine Einschränkungen bezüglich des Orts, an dem der Code der Lösung bereitgestellt wird. Daher können Entwickler und Anbieter den Code an mehreren Speicherorten innerhalb oder außerhalb der IT-Abteilung der Organisation bereitstellen. Verschiedene Organisationen haben möglicherweise unterschiedliche Serveranforderungen, angefangen bei Richtlinien bis hin zu SLAs. Vor der Bereitstellung eines SharePoint-Framework-Lösungspakets sollten Organisationen sicherstellen, dass der Server, der zum Hosten des Codes verwendet wird, ein bekannter und von der Organisation zugelassener Server ist.

### <a name="who-manages-the-code-hosting-location"></a>Wer verwaltet den Hostingspeicherort des Codes?

SharePoint-Framework-Lösungen werden als Teil der Seite im Kontext des aktuellen Benutzers ausgeführt. Zwar kann eine Organisation den Code vor der Bereitstellung des Lösungspakets überprüfen, um sicherzustellen, dass der Code vertrauenswürdig ist, sie muss jedoch auch die Integrität des Codes sicherstellen können, solange er auf dem Mandanten bereitgestellt wird. Organisationen sollten genau wissen, wer den Hostingspeicherort verwaltet, von wem und unter welchen Umständen die Dateien geändert werden können und wie das Verfahren zum Genehmigen von Updates aussieht. Die Vorabbeschaffung dieser Informationen hilft nicht nur Organisationen bei der Steuerung des Updatevorgangs, sondern senkt auch das Risiko, dass bösartiger Code bereitgestellt wird.

### <a name="what-is-the-sla-for-the-hosting-location"></a>Welche SLA gilt für den Hostingspeicherort?

Wenn Organisationen Office 365 und SharePoint Online verwenden, hängen sie von der von Microsoft bereitgestellten SLA ab. SharePoint-Framework-Lösungen, die die Standardfunktionen von SharePoint und Office 365 erweitern, sollten auf Servern bereitgestellt werden, die der von Microsoft bereitgestellten SLA entsprechen oder diese sogar übertreffen. Auf diese Weise können Organisationen sicherstellen, dass sie tatsächlich vom Mehrwert ihrer Anpassungen profitieren können.

### <a name="is-the-hosting-location-optimized-for-performance"></a>Ist der Hostingspeicherort für Leistung optimiert?

Externe Bibliotheken über eine URL zu laden, anstatt sie in das Webpart-Paket einzubetten, ist der erste Schritt zum Beschleunigen der Ladezeit von SharePoint-Framework-Lösungen. Zur optimalen Nutzung sollten Sie sicherstellen, dass der Server, der die verschiedene Skripts hostet, ordnungsgemäß für optimale Leistung konfiguriert ist. Er sollte alle Dateien komprimiert bereitstellen, und je länger Dateien auf Proxys oder Clients zwischengespeichert werden dürfen, desto länger können Benutzer diese Skripts aus ihrem lokalen Cache laden, wodurch das Laden von SharePoint-Seiten mit Webparts erheblich beschleunigt wird.

## <a name="tools-and-libraries"></a>Tools und Bibliotheken

Beim Erstellen von clientseitigen Lösungen können Entwickler aus einer Vielzahl von Bibliotheken wählen, z. B. React, Angular, jQuery oder Knockout. Die Verwendung einer vorhandenen JavaScript-Bibliothek erleichtert Entwicklern die Erstellung von Lösungen mit umfassendem Funktionsumfang. Es gibt große Unterschiede zwischen der Funktionsweise der verschiedenen Bibliotheken, und häufig sind spezifische Kenntnisse erforderlich, um in vollem Umfang zu verstehen, wie eine Lösung mit der jeweiligen  Bibliothek erstellt wird.

Nachdem die Lösung für den Produktionsmandanten freigegeben wurde, müssen Sie sicherstellen, dass Ihre Supportorganisation (entweder Ihre eigene IT-Abteilung oder ein vertraglich verpflichteter Drittanbieter) Support für die Lösung leisten kann. Um dies zu erreichen, muss die Supportorganisation mindestens über ein grundlegendes Verständnis der Bibliothek verfügen, die zum Erstellen der betreffenden Lösung verwendet wurde. Außerdem gilt: Je größer die Anzahl der bei Ihrem Mandanten verwendeten Bibliothekstypen ist, desto schwieriger wird es, Support für die verschiedenen Lösungen zu leisten. Wenn Sie lediglich eine oder zwei Bibliotheken für die Verwendung in Ihrer Organisation auswählen, trägt dies zur Senkung der Betriebskosten bei. Bevor Sie eine Lösung für Ihren Produktionsmandanten bereitstellen, sollten Sie sicherstellen, dass die Lösung nur Bibliotheken verwendet, die in Ihrer Organisation unterstützt werden.

## <a name="using-external-scripts"></a>Verwenden von externen Skripts

Bei Verwendung vorhandener JavaScript-Bibliotheken können Entwickler diese wahlweise in das Webpart-Codepaket einschließen oder über eine URL laden. Das Laden von Bibliotheken über URLs ermöglicht es Entwicklern, die Leistung von SharePoint Framework-Lösungen zu optimieren. Da Bibliotheken über eine URL geladen werden, müssen sie nicht im Webpart-Paket enthalten sein, wodurch sich dessen Größe verringert, sodass es schneller geladen werden kann. Darüber hinaus werden SharePoint-Framework-Lösungen, die im gesamten Mandanten auf die gleichen Bibliotheken verweisen, schneller geladen, da sie die zuvor heruntergeladenen Skripts aus dem lokalen Cache wiederverwenden.

Es gibt keine Einschränkungen im Hinblick darauf, von wo die vorhandenen Bibliotheken geladen werden können, und es ist wichtig für Sie zu wissen, von welchen Servern externe Skripts geladen werden. Zusammen mit dem Webpart-Code werden diese Skripts im Kontext des aktuellen Benutzers ausgeführt und dürfen tun, was der aktuelle Benutzer tun darf. Daher ist es wichtig, dass Sie diesen Skripts und ihrer Integrität vertrauen. In einigen Organisationen gelten strenge Richtlinien im Hinblick auf das Laden von Ressourcen aus öffentlichen CDNs, und Sie sollten sicherstellen, dass die Lösung und die zugehörigen Ressourcen die Organisationsrichtlinien erfüllen.

## <a name="approving-sharepoint-framework-solutions-for-deployment"></a>Genehmigen von SharePoint-Framework-Lösungen für die Bereitstellung

SharePoint Framework-Lösungen werden zentral über den App-Katalog an einen Mandanten bereitgestellt. Ihre Organisation sollte über einen Plan verfügen, in dem beschrieben wird, wer zum Bereitstellen und Genehmigen von SharePoint Framework-Paketen berechtigt ist. Dies ist wichtig, da dieser Plan auch angeben sollte, wer dafür zuständig ist zu überprüfen, ob die bereitgestellten Pakete sicher sind und den Organisationsrichtlinien entsprechen. SharePoint Framework-Lösungen werden im Browser im Kontext des aktuellen Benutzers ausgeführt und haben im Gegensatz zu SharePoint-Add-Ins stets die gleichen Berechtigungen wie der momentan angemeldete Benutzer. Bevor Sie eine SharePoint-Framework-Lösung für die Verwendung in Ihrer Organisation bereitstellen und genehmigen, müssen Sie ihren Ursprung und andere Kriterien, die weiter oben in diesem Artikel genannten werden, sorgfältig prüfen.

Um zu überprüfen, ob die jeweilige SharePoint-Framework-Lösung die Organisationsrichtlinien erfüllt, sollten Sie den Inhalt des SPPKG-Pakets überprüfen, das Sie bereitstellen möchten, und den Inhalt der referenzierten Skripts sowie den Speicherort, an dem sie gehostet werden, genau untersuchen. Dieser Schritt kann manuell ausgeführt oder teilweise automatisiert werden, z. B. mithilfe von Drittanbietertools. [SharePoint Customization Analysis Framework](https://rencore.com/products/#spcaf) (SPCAF) ist ein Beispiel für eine Drittanbieterlösung, die die Analyse des Inhalts von SharePoint Framework-Lösungen und die Überprüfung, ob sie die Sicherheits- und Governanceanforderungen der Organisation erfüllen, erheblich vereinfacht.

## <a name="sharepoint-framework-solutions-and-no-script-sites"></a>SharePoint Framework-Lösungen und Websites ohne Skripts

In Office 365 können Organisationen die Einstellung „Kein Skript“ verwenden, um skriptbasierte Anpassungen in SharePoint Online zu deaktivieren. Organisationen können die Einstellung „Kein Skript“ entweder für den gesamten Mandanten oder für eine bestimmte Websitesammlung konfigurieren. Basierend auf den Kriterien aus den Organisationsrichtlinien können Administratoren die Einstellung „Kein Skript“ verwenden, um Anpassungen zu deaktivieren, die z. B. mit dem Skript-Editor-Webpart oder einer benutzerdefinierten Aktion erstellt wurden.

Die Einstellung „Kein Skript“ ermöglicht es Organisationen, eine zusätzliche Kontroll- und Sicherheitsebene auf den gesamten Mandanten oder bestimmte Websitesammlungen anzuwenden. Das Anpassen von SharePoint durch Einbetten und Einfügen von Skripts ist nicht ohne Risiken und sollte insbesondere auf Websites mit vertraulichen Informationen sorgfältig überdacht werden.

In der Vergangenheit haben Entwickler mithilfe von Techniken zum Einbetten und Einfügen von Skripts leistungsfähige SharePoint-Anpassungen erstellt. In einigen Fällen basierten diese Anpassungen auf einer bestimmten Seitenstruktur, und wenn diese geändert wurde, funktionierte die jeweilige Anpassung nicht mehr ordnungsgemäß. Um Entwickler beim Erstellen robusterer Lösungen zu unterstützen, hat das SharePoint-Entwicklungsteam entschieden, dass in allen modernen Websites die Einstellung „Kein Skript“ aktiviert sein sollte. Dies bedeutet, dass das Einbetten und Einfügen von Skripts auf diesen Websites nicht möglich ist und dass die Verwendung von SharePoint Framework derzeit die einzige Möglichkeit zum Anpassen dieser Websites ist. Es wird erwartet, dass zukünftig alle modernen Websites die Einstellung „Kein Skript“ verwenden und Alternativen für das Einbetten und Einfügen von Skripts für Entwickler verfügbar gemacht werden, um die verschiedenen Szenarios zu unterstützen.
