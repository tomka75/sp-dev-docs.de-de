---
title: "Bekannte Probleme und häufig gestellte Fragen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6fba3eac7cca5200b7593dd51243df41211f6bc1
ms.sourcegitcommit: 8384d549db4ff023aacac273d74786928ebdeece
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/11/2017
---
# <a name="known-issues-and-frequently-asked-questions"></a>Bekannte Probleme und häufig gestellte Fragen

Auf dieser Seite finden Sie eine Liste bekannter Probleme mit SharePoint Framework sowie Antworten auf häufig gestellte Fragen. 

## <a name="known-issues"></a>Bekannte Probleme

**Problem mit dem Entwicklerzertifikat unter Chrome (ab v58)**

- *Datum – 28. April*
- *Aktualisiert – 2. Mai*

Wenn Sie Chrome als Entwicklungsbrowser verwenden, treten möglicherweise Probleme mit dem Entwicklerzertifikat auf, unabhängig davon, ob Sie den Befehl `gulp trust-dev-cert` ausführen. Chrome hat sein Modell für die Überprüfung von Zertifikaten ab Version 58 geändert. Beim Zugriff auf die lokale Workbench wird Ihnen daher möglicherweise die Warnmeldung „Ihre Verbindung ist nicht privat“ angezeigt.

Sie sollten Ihre Yeoman-Vorlagenpakete aktualisieren. Wir haben die Zertifizierungserstellungslogik im Paket *@microsoft/gulp-core-build-serve* aktualisiert. In vorhandenen Lösungen können Sie einfach diesen Ordner löschen und `npm install` ausführen, um das aktualisierte Paket abzurufen. Darüber hinaus müssen Sie die Befehle `untrust-dev-cert` und `trust-dev-cert` auf Ihrem Computer ausführen, um das Problem mit der Zertifizierungserstellungslogik zu beheben. 

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

**Ab wann werden benutzerdefinierte Aktionen und JSLink im SharePoint Framework verfügbar sein?**

- *Datum - 6. Juni*

SharePoint-Framework-Erweiterungen mit zusätzlichen Anpassungsmöglichkeiten sind jetzt in SharePoint Online verfügbar. Weitere Informationen zu den SharePoint-Framework-Erweiterungen finden Sie in unserer Dokumentation.

- [Übersicht über SharePoint-Framework-Erweiterungen](./extensions/overview-extensions.md)
- [Lernprogramme zu SharePoint-Framework-Erweiterungen](./extensions/get-started/build-a-hello-world-extension.md)

**Wird SharePoint-Framework auch in lokalen Bereitstellungen verfügbar sein?**

- *Datum - 6. Juni*

Die clientseitigen Webparts von SharePoint-Framework auf klassischen Seiten werden im Rahmen des Feature Pack 2 (FP2) mit SharePoint 2016 veröffentlicht. Es gibt derzeit keine Pläne, SharePoint-Framework-Funktionen für SharePoint 2013 bereitzustellen. Es gibt keine bestimmte Liste der SharePoint-Framework-Funktionen, die in der SharePoint 2019-Version enthalten sein sollen.

## <a name="see-also"></a>Siehe auch
Verwenden Sie die folgenden Ressourcen, um den SharePoint-Entwicklern Feedback, Kommentare und Fragen zukommen zu lassen: 

* [Problemliste unter „sp-dev-docs“ in GitHub]((https://github.com/SharePoint/sp-dev-docs/issues))
* [SharePoint Developer-Bereich in der Microsoft Tech Community]((https://aka.ms/sppnp-community))
