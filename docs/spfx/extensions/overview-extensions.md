---
title: "Übersicht über SharePoint-Framework (SPFx)-Erweiterungen"
description: "Verwenden Sie SPFx-Erweiterungen, um weitere Aspekte der SharePoint-Benutzeroberfläche anzupassen, wie beispielsweise Benachrichtigungsbereiche, Symbolleisten und Listendatenansichten."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: a39bfdc82e3557fb791c43db21e889448f75b785
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="overview-of-sharepoint-framework-extensions"></a>Übersicht über SharePoint-Framework-Erweiterungen

Mit SharePoint-Framework (SPFx)-Erweiterungen können Sie die SharePoint-Benutzeroberfläche erweitern. Mit SharePoint-Framework-Erweiterungen können Sie weitere Aspekte der SharePoint-Benutzeroberfläche anpassen, u. a. Benachrichtigungsbereiche, Symbolleisten und Listenansichten. SharePoint-Framework-Erweiterungen sind in allen Office 365-Mandanten für die Produktion verfügbar. 

> [!NOTE] 
> Sie erhalten einen kostenlosen Office 365-Entwicklermandanten, wenn Sie sich für das [Office 365 Developer Program](http://dev.office.com/devprogram) registrieren.

Mithilfe von SharePoint Framework-Erweiterungen können Sie die SharePoint-Benutzeroberfläche auf modernen Seiten und in Dokumentbibliotheken erweitern. Dabei können Sie für die clientseitige Entwicklung die vertrauten SharePoint Framework-Tools und -Bibliotheken nutzen. Im Besonderen bietet SharePoint Framework drei neue Erweiterungstypen:

- **Application Customizers**. Erweiterungen dieses Typs fügen einer Seite Skripts hinzu. Außerdem greifen sie auf bekannte HTML-Element-Platzhalter zu und erweitern sie um benutzerdefinierte Renderings.
- **Field Customizers**. Über Erweiterungen dieses Typs können sie modifizierte Datenansichten für Felder in einer Liste bereitstellen.
- **Command Sets**. Erweiterungen dieses Typs erweitern die SharePoint-Befehlsoberfläche um neue Aktionen und stellen clientseitigen Code bereit, mit dessen Hilfe Sie bestimmte Verhaltensweisen implementieren können.

Zusätzlich zu einfachen JavaScript-Projekten können Sie auch gängige Skripterstellungsframeworks wie AngularJS und React zur Erstellung Ihrer Erweiterungen nutzen. So können Sie beispielsweise React mit Komponenten aus Office UI Fabric React kombinieren und Oberflächen erstellen, die dieselben Komponenten verwenden wie Office 365.

> [!NOTE]
> Es gibt ein bekanntes Problem mit der Unterstützung für die Erweiterung von Listen und Bibliotheken in klassischen Benutzeroberflächen. Diese funktionieren derzeit nur im Kontext moderner Teamwebsites, die auch als Gruppen zugeordnete Teamwebsites bezeichnet werden. Wir arbeiten an der Lösung dieses Problems. 

## <a name="get-started"></a>Erste Schritte

1. Falls Sie SharePoint Framework noch nicht installiert haben, müssen Sie die Schritt-für-Schritt-Anleitung im Artikel zum Thema [Einrichten Ihrer Entwicklungsumgebung](../set-up-your-development-environment.md) befolgen.

2. Führen Sie nach der Installation von SharePoint Framework den folgenden Befehl aus, um Ihre Yeoman-Vorlagen auf die neueste Version zu aktualisieren:

    ```
    npm install -g @microsoft/generator-sharepoint
    ```

3. Anschließend erstellen Sie Ihre erste SharePoint Framework-Erweiterung mithilfe der Anleitung im Artikel [Build your first SharePoint Framework Extension (Hello World part 1)](get-started/build-a-hello-world-extension.md).

## <a name="stay-up-to-date"></a>Immer auf dem neuen Stand
Die neuesten Informationen zu SharePoint Framework-Verbesserungen, einschließlich Erweiterungsaktualisierungen, finden Sie hier:

* [@SharePoint](https://twitter.com/sharepoint) und [@OfficeDev](https://twitter.com/officedev) auf Twitter
* [Office-Entwicklerblog](http://dev.office.com/blogs)

## <a name="provide-feedback"></a>Übermitteln von Feedback 
Übermitteln Sie gerne Ihr Feedback zum allgemein verfügbaren SharePoint-Framework. Über die folgenden Ressourcen können Sie Ihr Feedback direkt an das Entwicklungsteam von SharePoint übermitteln:

- [Problemliste im Repository „sp-dev-docs“](https://github.com/SharePoint/sp-dev-docs/issues): Fragen, Probleme und Kommentare
* [SharePoint StackExchange](http://sharepoint.stackexchange.com/): Verwenden Sie die Tags [#spfx](http://sharepoint.stackexchange.com/tags/spfx/), [#spfx-extensions](http://sharepoint.stackexchange.com/tags/spfx-extensions/) und [#spfx-tooling](http://sharepoint.stackexchange.com/tags/spfx-tooling/).
* [SharePoint Developer](https://techcommunity.microsoft.com/t5/SharePoint-Developer/bd-p/SharePointDev): Gruppe in der Microsoft Tech Community
* [SharePoint Developer UserVoice](https://sharepoint.uservoice.com/forums/329220-sharepoint-dev-platform): Plattform zur Anforderung neuer Funktionen und Features


## <a name="see-also"></a>Siehe auch

- [Übersicht über das SharePoint Framework](../sharepoint-framework-overview.md)
- [Entwicklungstools und -bibliotheken für das SharePoint Framework](../tools-and-libraries.md)
