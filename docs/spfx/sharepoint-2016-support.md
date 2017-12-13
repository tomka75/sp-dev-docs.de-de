---
title: SharePoint-Framework-Entwicklung mit SharePoint 2016 Feature Pack 2
ms.date: 09/25/2017
ms.openlocfilehash: 6841d1a2df002bdf7c7a280c76bb0f21bc7a1d26
ms.sourcegitcommit: d68d6cf927d69696a3561f7d8ffe9a3ed9dbd03c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="sharepoint-framework-development-with-sharepoint-2016-feature-pack-2"></a>SharePoint-Framework-Entwicklung mit SharePoint 2016 Feature Pack 2

SharePoint 2016 Feature Pack 2 unterstützt clientseitige Webparts des SharePoint-Frameworks, die auf klassischen SharePoint-Seiten gehostet werden.

Eine Einführung in die SharePoint-Framework-Entwicklung in SharePoint 2016 mit dem Feature Pack 2 finden Sie auch im folgenden Video im [YouTube-Kanal „SharePoint Patterns and Practices“](https://www.youtube.com/watch?v=LGLMxnmHk6U&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG).

> [!VIDEO https://www.youtube.com/embed/LGLMxnmHk6U?list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG]

## <a name="which-version-of-the-sharepoint-framework-to-use"></a>Zu verwendende Version von SharePoint-Framework

Da SharePoint Online und SharePoint 2016 unterschiedliche Versionszyklen für neue Funktionen haben, verfügen sie auch über verschiedene Funktionen im Hinblick auf SharePoint-Framework. SharePoint Online verwendet immer die neueste Version von SharePoint-Framework, SharePoint 2016 unterstützt jedoch nur die Version, die mit den serverseitigen Abhängigkeiten der bereitgestellten Pakete übereinstimmt.

SharePoint 2016 Feature Pack 2 unterstützt clientseitige Webparts des SharePoint-Frameworks, die auf klassischen, mit SharePoint-Framework v1.1.0 erstellten SharePoint-Seiten gehostet wurden. Dies bedeutet, dass Sie bei der Entwicklung für die SharePoint 2016-Plattform aufgrund der serverseitigen Versionsabhängigkeiten SharePoint-Framework v1.1.0 verwenden müssen.

Wenn Sie die gleichen clientseitigen Webparts in SharePoint 2016 und in SharePoint Online verwenden möchten, müssen Sie SharePoint-Framework v1.1.0 als Basisversion verwenden, um sicherzustellen, dass das Webpart in beiden Umgebungen funktioniert.

Ab Version 1.3 bietet der SharePoint-Framework-Yeoman-Generator Unterstützung für die Erstellung von Lösungsgerüsten, die die neueste Version von SharePoint-Framework sowohl für die Verwendung mit SharePoint Online als auch mit lokalen SharePoint-Bereitstellungen auf der Grundlage von SharePoint-Framework v1.1.0 verwenden. Sie müssen keine separate Version des SharePoint-Framework-Yeoman-Generators für die Erstellung von Lösungsgerüsten für die Verwendung mit lokalen SharePoint-Bereitstellungen installieren.

## <a name="hosting-your-sharepoint-framework-solution-for-on-premises-deployment"></a>Hosten der SharePoint-Framework-Lösung für die lokale Bereitstellung

Für die Bereitstellung von clientseitiger SharePoint-Framework-Weboarts sind zwei unterschiedliche Aktionen erforderlich:

- Bereitstellung des Lösungspakets im SharePoint-App-Katalog
- Hosten der JavaScript-Dateien an einem zentralen Speicherort

Sie können die JavaScript-Dateien an einem Speicherort hosten, der für Ihre Umgebung am besten geeignet ist. Diese Dateien können zum Beispiel an den folgenden Speicherorten gehostet werden:

- **Azure CDN** – Einrichtung ähnlich wie bei SharePoint Online. Endbenutzer benötigen eine Internetverbindung.
- **Lokaler Server in Ihrem Netzwerk** – Ein Server, auf dem die JavaScript-Dateien für Ihr Unternehmensnetzwerk gehostet werden. Dies ist mit einer beliebigen Technologie möglich, solange auf die Dateien über HTTP-Anforderungen zugegriffen werden kann.
- **SharePoint-2016** – Sie können auch Ihre Dateien in der lokalen SharePoint-Farm hosten. Sie können zum Beispiel eine standardisierte Website in der Farm definieren, in der alle SharePoint-Framework-Ressourcen gehostet werden. Beachten Sie jedoch, dass JSON-Dateien standardmäßig nicht in SharePoint 2016-Bibliotheken hochgeladen werden können. Aus diesem Grund müssen die Einstellungen der Farmebene für diese Option angepasst werden.

> Weitere Informationen zu den gesperrten Dateitypen in SharePoint 2016 finden Sie im folgenden Support-Artikel: [Dateitypen, die einer Liste oder Bibliothek nicht hinzugefügt werden können](https://support.office.com/de-DE/article/Types-of-files-that-cannot-be-added-to-a-list-or-library-30be234d-e551-4c2a-8de8-f8546ffbf5b3#ID0EAADAAA=2016)

## <a name="development-environment-considerations"></a>Überlegungen zur Entwicklungsumgebung

Wenn Sie clientseitige SharePoint-Framework-Webparts entwickeln, ist für den Zugriff auf npm-Pakete eine Internetverbindung erforderlich. Dies ist erforderlich, wenn das Lösungsgerüst mithilfe der Vorlagen von SharePoint-Framework-Yeoman erstellt wird.

Wenn die Entwicklungscomputer über keinen Internetzugang verfügen, können Sie eine lokale Registrierung für die erforderlichen npm-Pakete einrichten. Allerdings ist dies mit zusätzlicher Software und einem deutlichen Mehraufwand im Hinblick auf die Einrichtung und Verwaltung lokaler Paketversionen mit Paketen in dem tatsächlichen npm-Katalog verbunden.

> Das Dokument [Team-basierte Entwicklung im SharePoint-Framework](team-based-development-on-sharepoint-framework.md) enthält verschiedene Optionen für die Einrichtung der Entwicklungsumgebung, zum Beispiel, wenn mehrere SharePoint-Framework-Versionen unterstützt werden müssen.

## <a name="how-to-determine-which-sharepoint-framework-version-was-used-for-a-solution"></a>Ermitteln der für die Lösung verwendeten SharePoint-Framework-Version

Wenn Sie über vorhandene SharePoint-Framework-Lösungen verfügen und herausfinden möchten, welche Version von SharePoint-Framework für sie verwendet wurde, müssen Sie die folgenden Dateien prüfen:

- **.yo-rc.json** – Datei im Stammordner der Lösung, in der die bei der Erstellung der Lösung verwendete SharePoint-Framework-Yeoman-Vorlagenversion gespeichert ist.
- **package.JSON** – Datei im Stammordner der Lösung, die Verweise auf die in der Lösung verwendeten Paketversionen enthält.
- **npm-shrinkwrap.json** – Datei im Stammordner der Lösung, die Informationen zu den verwendeten genauen Versionen enthält (bei Verwendung des `npm shrinkwrap`-Befehls zum Sperren der genauen Versionen der Lösung).
- **package.json** – Datei im Ordner *node_modules/@microsoft/sp-webpart-base*, die ein *version*-Attribut enthält, das der verwendeten SharePoint-Framework-Version entspricht, wenn Sie Pakete in Ihrer Lösung installiert haben.
