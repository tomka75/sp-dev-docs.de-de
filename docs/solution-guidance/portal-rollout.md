---
title: "Bewährte Methoden für die Einführung von SharePoint Online-Portale"
ms.date: 11/03/2017
ms.openlocfilehash: 996ab833afffc5849bb70e99b624c13842cbfca9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="best-practices-for-rolling-out-sharepoint-online-portals"></a>Bewährte Methoden für die Einführung von SharePoint Online-Portale

Nach Sie widmen live Ihre Zeit und weniger Energie in Gebäude, die neue SharePoint Portal basieren darauf zuzugreifen soll... so bald wie möglich, aber was wäre eine gute Modell dafür? In diesem Artikel wird erläutert, das empfohlene Modell für die Bereitstellung von Ihrem Portal für die Endbenutzer.

> [!NOTE] 
> Obwohl dieser Anleitung SharePoint Online Zielgruppenadressierung ist die meisten davon gilt auch für Portale in einer lokalen SharePoint-Umgebung gehostet wird.


_**Gilt für:** SharePoint Online_

## <a name="anti-patterns-in-other-words-dont-do-these-things"></a>Anti-Muster (also nicht sollten Sie folgende Aktionen)
<a name="sectionSectionAntiPatterns"></a> Unterhalb der Liste enthält die wichtigsten Punkte **nicht** zu tun, wenn es darum geht, Rollout auf Ihrem Portal:
- Stress Testen Ihres Portals anhand Ihrer SharePoint Online-Mandanten
- Führen Sie einer Big Warnsymbol Version im Wesentlichen Freigeben Ihrer neue Portal für **Alle** Ihre Benutzer zum gleichen Zeitpunkt
- Freigeben von Ihrem Portal, wenn eine große Anzahl von Sicherheitsgruppen als Mitglieder der Gruppe kann zu Problemen führen. Dies kann mit einer großen Anzahl vorkommen, jeweils mit einer einzelnen Websitegruppenmitgliedschaft (30-40 KB) Sicherheitsgruppen oder einer kleineren Anzahl von Sicherheitsgruppen, die Mitglieder der viele Websitegruppen sind möglich.


## <a name="how-did-you-do-this-in-the-past"></a>Wie haben Sie dies in der Vergangenheit?
<a name="sectionSection0"></a> Oft Kunden wurde umfangreiche Belastungstests auf ihre lokalen-Portale SharePoint ausgeführt, wie sie ermitteln, ob die Infrastruktur die Last zu bewältigen würde und trotzdem ordentliche Seitenladezeiten wollten. Mit SharePoint Online jedoch nicht mehr **Ausführen eines klassischen Leistungstests ist nicht zulässig** , da:
- SharePoint Online wird die Last als ein Denial-of-Service-Angriffs testen finden Sie unter und einfach wird der Benutzer oder sogar schlechter vollständige Mandanten blockieren
- Wenn der Test wird nicht blockiert es wird schwerer Testergebnisse interpretiert werden im resultierenden gedrosselt werden
- SharePoint Online wird dynamisch die zugrunde liegende Infrastruktur skaliert, die hervorragend, funktioniert aber nicht Wenn Sie plötzlich eine umfassende Load Erhöhung. Das Skalierung Back-End-Modell benötigt Zeit zum kompensieren erhöhte Last
- Solche ein Leistungstest ist nur eine einmalige Überprüfung, während Sie Portal auf weiterentwickelt beibehalten werden, die besser auf verlassen im Portal Telemetrie integriert, sodass Sie fortlaufend Nachsorge auf die Leistung Ihres Portals können. Es ist außerdem schwer zu einen Auslastungstest erstellen, der eine echte Verwendungsmuster darstellt.

Der empfohlene Ansatz für die Einführung des neuen Portals ist mit einer phasenweisen Einführung Plan in Kombination mit integriert Portal Telemetrie Portal Leistung gemessen, während weiterer Benutzer hinzugefügt werden. Das nächste Kapitel bieten weitere Details, um diese Vorgehensweise.

## <a name="recommendation-use-a-phased-portal-roll-out-strategy-combined-with-portal-telemetry"></a>Empfehlung: Verwenden einer phasenweisen Portal Bereitstellungsstrategie in Kombination mit Portal Telemetrie
Ein häufig verwendetes Modell für die Einführung neuen Funktionen wird phasenweise mithilfe der in der Regel besteht:
- Ein **Pilotprojekt** Wave: Hierbei handelt es sich beim ersten das Portal für eine Gruppe von ausgewählten Benutzern geöffnet ist. Es ist wichtig, um eine Gruppe von Benutzern repräsentative, critical, Key abzurufen, die das erste Feedback geben können
- Eine oder mehrere **Endbenutzer** hochrangige: die Anzahl der Ihnen hochrangige abhängt für wie viele Benutzer Sie werden müssen in Kombination mit Details des Modells Sie einhalten. Wir sehen, dass Unternehmen ihre einführen hochrangige mit ihrer Organisationsstruktur ausrichten, andere Unternehmen werden durch country/region...in das, was entscheidend ist die Tatsache, dass Sie neue Benutzer schrittweise Portal hinzufügen am Ende ausrichten

Unter Bild zeigt eine gute schrittweisen einführen. Beachten Sie, dass dies auch im Konto verwendet, die in der Regel Endbenutzer hochrangige weniger tatsächlichen Benutzern stehen eingeladen anschließend Benutzer.

![phasenweise Portal einführen-Modell](https://support.content.office.net/en-us/media/0bc14a20-9420-4986-b9b9-fbcd2c6e0fb9.png)

Die oben genannten Phasen erhalten Sie Zeit zum kompensieren Feedback und ändern Sie Ihr Portal, falls erforderlich, aber wie messen und phasenweise Nachsorge auf die Leistung während dieser Einführung? Der empfohlene Ansatz zum auf diese Weise ist in der Implementierung Portal Telemetrie einbetten, wie [im Artikel Leistung Telemetrie](https://msdn.microsoft.com/en-us/pnp_articles/portal-performance#telemetry)Abschnitt erläutert. Mit einer fortlaufenden Datenfluss Portal Leistung helfen Ihnen beim verstehen, wenn die Portal Leistung geändert wird, wenn die Anzahl der Benutzer, sondern auch wächst Wenn Sie in der zukünftigen stellen Portal ändert.

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Capacity planning and load testing SharePoint Online](https://support.office.com/en-us/article/Capacity-planning-and-load-testing-SharePoint-Online-c932bd9b-fb9a-47ab-a330-6979d03688c0?ui=en-US&rs=en-US&ad=US)
