---
title: "SharePoint-Framework – Bekannte Probleme und häufig gestellte Fragen"
description: "Lösungen für Probleme und Antworten auf häufig gestellte Fragen zum SharePoint-Framework."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 79b580fd263636ccab392f99f11983c24ac08e8b
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-framework-known-issues-and-frequently-asked-questions"></a>SharePoint-Framework – Bekannte Probleme und häufig gestellte Fragen

Auf dieser Seite finden Sie eine Liste bekannter Probleme mit SharePoint-Framework sowie Antworten auf häufig gestellte Fragen. 

## <a name="known-issues"></a>Bekannte Probleme

### <a name="dev-certificate-issue-with-chrome-v58-"></a>Problem mit dem Entwicklerzertifikat unter Chrome (ab v58)

- *Datum: 28. April 2017*
- *Aktualisiert: 2. Mai 2017*

Wenn Sie Chrome als Entwicklungsbrowser verwenden, treten möglicherweise Probleme mit dem Entwicklerzertifikat auf, unabhängig davon, ob Sie den Befehl `gulp trust-dev-cert` ausführen. Chrome hat sein Modell für die Überprüfung von Zertifikaten ab Version 58 geändert. Beim Zugriff auf die lokale Workbench wird Ihnen daher möglicherweise die Warnmeldung „Ihre Verbindung ist nicht privat“ angezeigt.

Sie sollten Ihre Yeoman-Vorlagenpakete aktualisieren. Wir haben die Zertifizierungserstellungslogik im Paket [*@microsoft/gulp-core-build-serve* aktualisiert](https://www.npmjs.com/package/@microsoft/gulp-core-build-serve). 

In vorhandenen Lösungen können Sie einfach diesen Ordner löschen und `npm install` ausführen, um das aktualisierte Paket abzurufen. Darüber hinaus müssen Sie die Befehle `untrust-dev-cert` und `trust-dev-cert` auf Ihrem Computer ausführen, um das Problem der Zertifizierungserstellungslogik zu behoben. 

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="when-will-custom-actions-and-jslink-be-available-in-the-sharepoint-framework"></a>Ab wann werden benutzerdefinierte Aktionen und JSLink im SharePoint-Framework verfügbar sein?

- *Datum: 6. Juni 2017*

SharePoint-Framework-Erweiterungen mit zusätzlichen Anpassungsmöglichkeiten sind jetzt in SharePoint Online verfügbar. Weitere Informationen zu den SharePoint-Framework-Erweiterungen finden Sie in unserer Dokumentation:

- [Übersicht über SharePoint-Framework-Erweiterungen](./extensions/overview-extensions.md)
- [Lernprogramme zu SharePoint-Framework-Erweiterungen](./extensions/get-started/build-a-hello-world-extension.md)

### <a name="will-sharepoint-framework-be-available-in-on-premises"></a>Wird SharePoint-Framework auch in lokalen Bereitstellungen verfügbar sein?

- *Datum: 6. Juni 2017*

Die clientseitigen Webparts von SharePoint-Framework auf klassischen Seiten werden im Rahmen des Feature Pack 2 (FP2) mit SharePoint 2016 veröffentlicht. Es gibt derzeit keine Pläne, SharePoint-Framework-Funktionen für SharePoint 2013 bereitzustellen. Es gibt keine bestimmte Liste der SharePoint-Framework-Funktionen, die in der SharePoint 2019-Version enthalten sein werden.

## <a name="see-also"></a>Siehe auch

Verwenden Sie die folgenden Ressourcen, um den SharePoint-Entwicklern Feedback, Kommentare und Fragen zukommen zu lassen. 

- [SharePoint-Entwicklungsdokumente auf GitHub zu Problemen](https://github.com/SharePoint/sp-dev-docs/issues)
- [Microsoft Tech Community-Bereich für SharePoint-Entwickler](https://aka.ms/sppnp-community)

