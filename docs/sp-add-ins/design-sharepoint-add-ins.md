---
title: Entwerfen von SharePoint-Add-Ins
description: "In diesem Artikel finden Sie einen Überblick über die in SharePoint-Add-Ins verfügbaren Entwurfs- und Architekturoptionen. Außerdem erfahren Sie, wie Sie die richtigen Entscheidungen treffen können, um sich die Entwicklung Ihres SharePoint-Add-Ins einfacher zu machen."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: e33f97d9d19d277020094c739ada08133b53d297
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="design-sharepoint-add-ins"></a>Entwerfen von SharePoint-Add-Ins

Angenommen, Sie haben eine großartige Idee für ein Add-In. In diesem Abschnitt führen wir Sie durch die erforderlichen Entwurfsentscheidungen und stellen bewährte Methoden für die Erstellung Ihres Add-Ins bereit. Was macht zum Beispiel eine gute Benutzeroberfläche aus? Welche Add-In-"Formen" sind verfügbar? Nach welchen Kriterien sollten diese ausgewählt werden? Welche Optionen stehen für den Datenzugriff zur Verfügung? 

<a name="SP15Design_Startdesigning"> </a>
## <a name="start-designing-sharepoint-add-ins"></a>Erste Schritte beim Entwerfen von SharePoint-Add-Ins

Da das Cloud-Add-In-Modell in SharePoint so viele Designoptionen ermöglicht, können SharePoint-Add-Ins die unterschiedlichsten Formen und Größen haben. Dieser Abschnitt liefert nützliche Tipps für einige der wichtigsten Entscheidungen, die Sie bei der Planung und beim Entwurf der Architektur und der Benutzerfreundlichkeit Ihres Add-Ins treffen müssen. Dazu zählen das Hosting Ihres Add-Ins, der effiziente und sichere Zugriff auf Daten und die Benutzung.

- [Drei Methoden für Entwurfsoptionen für SharePoint-Add-Ins](three-ways-to-think-about-design-options-for-sharepoint-add-ins.md): In diesem Artikel finden Sie eine Übersicht über die verfügbaren Entwurfs- und Architekturoptionen für SharePoint-Add-Ins.  
- [SharePoint-Add-Ins](sharepoint-add-ins.md): In diesem Artikel erfahren Sie, was genau SharePoint-Add-Ins sind.

<a name="SP15Design_Hostingmodel"> </a>
## <a name="choose-the-right-hosting-model-for-your-add-in"></a>Auswählen des richtigen Hostingmodells für Ihr Add-In

SharePoint-Add-Ins unterstützen mehrere Hostingoptionen. Sie können einen eigenen Webstack verwenden, die von Microsoft bereitgestellten Dienste Microsoft Azure oder SQL Azure nutzen oder das Add-In in SharePoint hosten. Der unten aufgeführte Artikel enthält Ressourcen und Richtlinien, die Ihnen bei der Auswahl des richtigen Hostingmodells für Ihr Add-In helfen:

- [Choose patterns for developing and hosting your SharePoint Add-in](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md): Hier erfahren Sie, welche Möglichkeiten es gibt, die Komponenten eines SharePoint-Add-Ins zu hosten.

<a name="SP15Design_Dataaccess"> </a>
## <a name="choose-the-right-data-access-technologies-for-your-add-in"></a>Auswählen der richtigen Datenzugriffstechnologien für Ihr Add-In

Sie müssen sicherstellen, dass Ihr Add-In effizient und sicher auf Daten zugreifen kann. Für den Zugriff auf SharePoint und die Arbeit mit Daten in Ihrem Add-In stehen verschiedene Datenzugriffstechnologien zur Verfügung. In dem unten aufgeführten Artikel finden Sie einen Überblick über die verschiedenen Optionen und erfahren, wie Sie die für Ihr Add-In richtige Option auswählen können: 

- [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md): In diesem Artikel erfahren Sie, welche Datenzugriffsoptionen Ihnen bei der Erstellung von SharePoint-Add-Ins zur Verfügung stehen, welche Datenkonnektivitätsoptionen für eingehende und ausgehende Daten es gibt und über welche APIs Add-Ins auf SharePoint-Daten zugreifen können.

<a name="SP15Design_UX"> </a>
## <a name="design-the-ux-for-your-add-in"></a>Entwerfen der Benutzeroberfläche Ihres Add-Ins

Beim Entwerfen eines Add-Ins sollte Ihr oberstes Ziel die Bereitstellung einer Benutzeroberfläche sein, mit der Ihre Benutzer die intendierten Szenarien unkompliziert umsetzen können. In dem unten aufgeführten Artikel finden Sie alle nötigen Ressourcen und Designrichtlinien für die Erstellung effektiver Add-Ins, die Best Practices für Benutzeroberflächen einhalten und das vertraute Aussehen und Verhalten von SharePoint bieten.

- [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins.md): Hier erfahren Sie mehr über die UX (User Experience)-Optionen, die Ihnen beim Erstellen von SharePoint-Add-Ins zur Verfügung stehen.

<a name="Upgrade"> </a>
## <a name="design-with-update-in-mind"></a>Einplanen von Updateprozessen in der Entwurfsphase

Möglicherweise möchten Sie irgendwann einmal ein Update für Ihr Add-In erstellen und in den Office Store oder den Add-In-Katalog einer Organisation hochladen. Das wird sehr viel einfacher sein, wenn Sie sich bereits beim Entwurf der ersten Version Gedanken darüber machen, wie Sie Ihr Add-In in Zukunft aktualisieren möchten. Wir empfehlen Ihnen, bereits frühzeitig während der Entwurfsphase die folgenden Artikel zu lesen: 

- [Aktualisierungsprozess von Add-Ins für SharePoint](sharepoint-add-ins-update-process.md)
- [Aktualisieren von Add-Ins für SharePoint](update-sharepoint-add-ins.md)

## <a name="next-steps-develop-and-publish-your-add-in"></a>Nächste Schritte: Entwickeln und Veröffentlichen Ihres Add-Ins
<a name="SP15Design_Next"> </a>

Sie haben einen soliden Entwurf für Ihr Add-In erarbeitet? Dann können Sie das Add-In erstellen und veröffentlichen. In den nachfolgenden Artikeln erfahren Sie, wie Sie dazu vorgehen müssen:

- [Entwickeln von SharePoint-Add-Ins](develop-sharepoint-add-ins.md): In diesem Artikel stellen wir Ihnen weiterführende Konzepte und Funktionen des Add-In-Modells vor.
- [Veröffentlichen von SharePoint-Add-Ins](publish-sharepoint-add-ins.md): In diesem Artikel erfahren Sie, wie Sie SharePoint-Add-Ins veröffentlichen können und welche Voraussetzungen hierfür zu erfüllen sind.

## <a name="additional-resources"></a>Weitere Ressourcen
<a name="SP15Design_AddRes"> </a>

-  [Beispielpaket für SharePoint-Add-Ins](http://code.msdn.microsoft.com/office/Apps-for-SharePoint-sample-64c80184)
-  [Reimagine SharePoint development](http://msdn.microsoft.com/de-DE/office/apps/dn133840)
-  [SharePoint-Add-Ins](sharepoint-add-ins.md)
-  [Entwickeln von SharePoint-Add-ins](develop-sharepoint-add-ins.md)
-  [Blog für Add-Ins](http://blogs.msdn.com/b/spoffapps)
    
 

