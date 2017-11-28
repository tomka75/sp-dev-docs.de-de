---
title: "Richtlinien für die Entwicklung von SharePoint Online-Portale gut"
ms.date: 11/03/2017
ms.openlocfilehash: 3ec4237011796d6257378204f9d5ee5cb13db372
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="guidelines-for-developing-well-performing-sharepoint-online-portals"></a>Richtlinien für die Entwicklung von SharePoint Online-Portale gut

Lokale SharePoint-wurde, und ist eine häufig verwendete Plattform zum Erstellen von Unternehmensportale (auch bekannt als Intranets). Sie können ähnliche Portale SharePoint Online sowie, da jedoch SharePoint Online von einer Infrastruktur Architektur Sicht unterscheidet, ist es wichtig, die in der SharePoint Online spezifische Leistungsaspekte Faktor bei der Entwicklung Ihrer neuen, erstellen Portal. Diese Gruppe von Artikeln erhalten Hinweise auf die wichtigsten Portal Design Bereiche Sie.

>**Hinweis**: Obwohl dieser Anleitung SharePoint Online gerichtet ist die meisten davon gilt auch für Portale in einer lokalen SharePoint-Umgebung gehostet wird.

_**Gilt für:** SharePoint Online_

## <a name="why-did-we-create-these-guidelines"></a>Warum haben wir diese Richtlinien erstellt?
<a name="sectionSection0"></a> Des Zuwachses von SharePoint Online sind bemerkenswert und daher sind immer mehr Kunden Portale mit SharePoint Online als Plattform erstellen. Während teams arbeiten mit SharePoint-Unterstützung und mehrere Großkunden wir festgestellt haben, wie viele Kunden ihre Portale erstellt sie erstellen werden würden ist diese für lokale SharePoint- und diesem Ansatz beeinträchtigt Portal Leistung. Häufig werden diese Leistungsprobleme aufgelöst nach Portal Go live, sich natürlich nicht ideal befindet. Wir hoffen, dass die folgenden Richtlinien halten Kunden besser vorbereitet werden zum Starten von gut Portale SharePoint Online.

## <a name="whats-included"></a>Was hat enthalten?
Die Anleitung konzentriert sich derzeit hauptsächlich auf Mustern und Methoden, die Ihnen helfen erstellen gut ausführen Portale SharePoint Online Konzentration auf die folgenden Themen: Leistung, Informationsarchitektur, Navigation, Datenaggregation, branding und Portal einführen. Jeder der Artikel weist das gleiche Layout:
- Wir beginnen mit Anti-Muster: im Wesentlichen informiert Sie sollten Sie **nicht** nicht mehr
- Wir werden best Practices und Muster klicken Sie dann auf, wie Sie Ihr Portal implementieren sollten stellen
- Wir werde Ihnen eine Reihe von Verknüpfungen auf interessante Ressourcen, in denen Sie mehr erfahren können
- Wir haben die bewährten Methoden mit Beispielen wie in unserem [Beispiel Client-Side Data Access Layer (DAL)](https://github.com/SharePoint/PnP/tree/master/Samples/Portal.DataAccessLayer) ergänzt.

## <a name="how-to-provide-feedback-around-provided-guidance"></a>Wie Feedbacks Anleitungen bereitgestellt?
Diese Anleitung ist vollständig open-Source, und wir empfehlen die Gemeinschaft um Feedback geben möchten. Oben rechts von jeder Seite klicken Sie auf "Mitwirken" auf dem Sie zum Hosten dieser Anleitung GitHub Repository übertragen wird. In GitHub können Sie einmal: 
- Wenn Sie eine Erläuterung des Inhalts starten möchten, erstellen Sie ein Problem in der Problemliste
- Verzweigen Sie das Repository, nehmen Sie Änderungen in den Artikeln und erstellen Sie eine Pull-Anforderung. Vielen Dank für Ihre Beiträge und unsere MSDN veröffentlichen System haben Sie darüber, wie die Seite Mitwirkender Freigabemodus Pull-Anforderung angenommen wurde

>**Hinweis**: Es werden werden weitere weiterentwickelt dieser Anleitung durch Hinzufügen, Beispiele, zusätzliche Insights, Integration von neuen Funktionen von SharePoint Online und wir freuen absolut Community Feedback und Beiträge.

## <a name="whats-the-audience-were-targeting-with-these-guidelines"></a>Was ist die Benutzergruppe, die wir mit diesen Richtlinien abzielen?
<a name="sectionSection1"></a> Den meisten Abschnitten verwenden Inhaltsadressierung Portal Entwickler für, jedoch wenn Sie nicht über ein Entwickler Hintergrund haben dann It des empfohlen, um über diese Richtlinien zu gelangen, wie es weitere allgemeine Bereiche wie die **Informationsarchitektur**, **Branding erörtert** und **Wechseln Sie Live**.

## <a name="portal-guidance-overview"></a>Übersicht über die Portal-Anweisungen
<a name="sectionSection2"></a> Unter Tabelle enthält eine Übersicht über die einzelnen Artikel, die Teil der SharePoint Online Portal Richtlinien sind.

|**Portal Entwurfsbereich**|**Einführung in die Optionen**|
|:-----|:-----|
|Leistung|<p>Leistung ist ein wichtiger Aspekt des alle Portal, und dieser Artikel enthält zahlreiche Entwurfsmuster, die beim Erstellen von gut ausführen Portale helfen.</p><p>[Leitfaden zur Portal Leistung](portal-performance.md)</p>|
|Informationsarchitektur|<p>Ein sound Informationsarchitektur ist eine wichtige Voraussetzung für die stellen eine gute Leistung Portal fest.</p><p>[Die Architektur Anleitungen Portal-Informationen](portal-information-architecture.md)</p>|
|Navigation|<p>Jedes Portal Projekt muss die Frage Navigation anzugehen und für SharePoint Online müssen Sie bestimmte Richtlinien Konto haben, die in diesem Artikel beschrieben werden.</p><p>[Portalnavigation-Anweisungen](portal-navigation.md)</p>|
|Datenaggregation|<p>Beispiel für das Aggregieren und Rollup von Daten aus unterschiedlichen Standorten, nutzen in Konto Benutzervoreinstellungen in etwas, die fast alle Portale benötigen. Sehen Sie sich in diesem Artikel erfahren Sie mehr über eine flexible bewährte Ansatz für das Aggregieren von Daten.</p><p>[Portal Daten Aggregation Anleitungen](portal-data-aggregation.md)</p>|
|Branding|<p>Die Fähigkeit zum Anwenden einer benutzerdefinierten Marke in einem Portal ist eine typische Voraussetzung und dieser Artikel bietet Ihnen einen Überblick über die Optionen branding und branding bewährte Methoden.</p><p>[Portal branding Anleitungen](portal-branding.md)</p>|
|Wechseln Sie Live|<p>Freigabemodus Portal wurde entwickelt und getestet wurde die Zeit, um aber welche Strategie für die Implementierung folgen live zu gehen? In diesem Artikel erhalten Sie die Microsoft empfohlene Vorgehensweise.</p><p>[Portal wechseln live Anleitungen](portal-rollout.md)</p>|

