---
title: Migrieren von InfoPath-Formularen in SharePoint 2013
ms.date: 11/03/2017
ms.openlocfilehash: f53ff1c78524e1a18e7082317dc9bc5c0aa56cdf
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="migrate-infopath-forms-to-sharepoint-2013"></a>Migrieren von InfoPath-Formularen in SharePoint 2013

Migrieren von InfoPath-Formularen in Ihrer SharePoint-Add-ins zu anderen unterstützten Lösungen, wie Access-Anwendungen, sandkastenlösungen oder das Add-In Modell.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Wenn Sie InfoPath als Grundlage zum Erstellen von Formularen in Ihrer-add-ins verwenden, ist nun die Zeit bis zur erwägen, zum Migrieren von Formularen zu anderen Lösungen. InfoPath derzeit wird zwar unterstützt, InfoPath 2013 ist die letzte Version des Desktops Client InfoPath und InfoPath Forms Services in SharePoint 2013 ist die letzte Version von InfoPath Forms Services. Der Client und der lokalen Version von InfoPath Forms Services in SharePoint 2013 werden bis 2023 vollständig unterstützt. Der Forms-Dienst wird in Office 365 bis mindestens die nächste Hauptversion von Office unterstützt werden.

Um von InfoPath-Formularen zu ersetzen, können Sie eine der folgenden alternativen auswählen:

- Verwenden von Access-Anwendungen.

- Verwenden Sie Microsoft Nachrichtenübermittlung und des Microsoft PowerApps.
    
- Verschieben Sie komplexe Verhaltensweisen in neue Add-In-Modell und Client Side Entwicklungen.
    
Die ersten beiden Lösungen, wird empfohlen, weil Information Worker, die nicht wissen, wie schreiben und Bereitstellen von alternativen codebasierte implementiert werden können. Die folgende Tabelle beschreibt die Szenarien für die einzelnen Alternative am besten geeignet ist.

**Alternativen zur InfoPath in SharePoint 2013**

|**Alternative**|**Szenario**|
|:-----|:-----|
|Access-Anwendungen|Diese Option unterstützt mehrere Formulare, die relationale Daten in mehrere Tabellen Access, Excel-Tabellen und/oder SharePoint-Listen behandelt.|
|Verwenden Sie Microsoft Nachrichtenübermittlung und des Microsoft PowerApps|Dies ist die unsere empfohlener Ansatz für die Erweiterung von Listen von SharePoint-Hauptbenutzer.|
|Neue Add-In-Modell und Client Side Entwicklungen |Sie können komplexe Formulare beschäftigte Mitarbeiter umfassende Code in vom Anbieter gehosteten-add-ins oder Client Side-Webparts zu konvertieren. Diese Option erfordert Ressourcen für Entwickler.|

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Muster und Methoden für InfoPath-Transformation Anleitungen](https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath) 

-  [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Office 365-Entwicklungsmuster und -übungen auf GitHub](https://github.com/SharePoint/PnP)
