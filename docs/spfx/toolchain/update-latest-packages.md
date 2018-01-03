---
title: Aktualisieren von SharePoint-Framework-Paketen
ms.date: 11/29/2017
ms.prod: sharepoint
ms.openlocfilehash: 665c22ffea27a8b62d433cfb4932625664638e0a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="update-sharepoint-framework-packages"></a>Aktualisieren von SharePoint-Framework-Paketen

Die SharePoint-Tools für die clientseitige Entwicklung verwenden den [npm]((https://www.npmjs.com/))-Paket-Manager, um Abhängigkeiten und andere erforderliche JavaScript-Hilfsprogramme zu verwalten. npm ist in der Regel als Teil des Node.js-Setups enthalten.

Beim Erstellen einer neuen clientseitigen Lösung ruft der Yeoman-Generator für SharePoint die neuesten SharePoint-Framework-Pakete ab, die für Ihr clientseitiges Projekt erforderlich sind. Ihre vorhandenen Pakete sind ggf. veraltet und möglicherweise stehen zum Erstellen Ihres Projekts neue Versionen der Pakete zur Verfügung. Entsprechend den [Versionshinweisen]((https://aka.ms/spfx-release-notes)) für eine bestimmte Version oder das neueste Paket können Sie die in Ihrem Projekt verwendeten SharePoint-Framework-Pakete aktualisieren. SharePoint Framework-Pakete enthalten die npm-Pakete, die Sie in Ihrem Projekt installiert haben (Beispiel: [@microsoft/sp-core-library]((https://www.npmjs.com/)package/@microsoft/sp-core-library)), sowie die global installierten npm-Pakete (Beispiel: [@microsoft/generator-sharepoint]((https://www.npmjs.com/)package/@microsoft/generator-sharepoint)). 

> [!TIP]
> Obwohl nicht erforderlich, empfiehlt es sich, die SharePoint Framework-Pakete regelmäßig zu aktualisieren, um alle neuesten Änderungen und Updates zu erhalten.

## <a name="find-outdated-packages-in-your-project"></a>Suche nach veralteten Paketen im Projekt

Führen Sie in einer Konsole im selben Verzeichnis wie das Projekt den folgenden Befehl aus, um nach veralteten Paketen in Ihrem clientseitigen Projekt zu suchen, einschließlich SharePoint Framework-Paketen und anderen, von denen Ihr Projekt abhängt. 

```sh
npm outdated
```

Der Befehl listet die folgenden Informationen zu den Paketen auf, von denen Ihr Projekt abhängt. Diese Informationen werden der Datei `package.json` im Stammverzeichnis des Projekts und der npm-Registry entnommen.

* Aktuelle, in Ihrem Projekt installierte Version
* Von Ihrem Projekt angeforderte Version (verfügbar in `package.json`)
* Neueste verfügbare Version

![Veraltete NPM-Pakete](../../images/npm-outdated-packages-list.png)

Um die SharePoint Framework Pakete zu identifizieren, suchen Sie nach den Paketnamen, die mit dem folgenden npm-Bereich und -Präfix beginnen:

```text
@microsoft/sp-
```

Zusammen mit den Framework-Paketen müssen Sie ggf. auch die Pakete `react` und `office-ui-fabric-react` aktualisieren. Lesen Sie unbedingt die [Versionshinweise]((https://aka.ms/spfx-release-notes)) für die jeweilige Version, um zu erfahren, welche Pakete eine Aktualisierung erfordern, und entsprechend planen zu können.

### <a name="using-npm-outdated-with-project-targeting-sharepoint-2016"></a>Verwenden veralteter npm-Pakete mit Projekten für SharePoint 2016

Ab Feature Pack 2 werden SharePoint-Framework-Lösungen in SharePoint 2016 unterstützt. SharePoint 2016 verwendet eine ältere Version von SharePoint-Framework als die Version, die in SharePoint Online verfügbar ist. Beim Erstellen des Gerüsts für neue Projekte müssen Sie im SharePoint-Framework-Yeoman-Generator angeben, ob Ihre Lösung die aktuelle Version von SharePoint-Framework verwenden und nur mit SharePoint Online verwendet werden kann oder eine ältere Version von SharePoint-Framework verwenden und sowohl mit SharePoint 2016 als auch mit SharePoint Online verwende werden kann.

Beim Ausführen des `npm outdated`-Befehls in einem Projekt, das sowohl für SharePoint Online als auch für SharePoint 2016 entwickelt wurde, werden die aktuellen Versionen der SharePoint-Framework-Pakete angezeigt. Diese Versionen funktionieren jedoch nur mit SharePoint Online. Wenn Sie Ihre Lösung für die Verwendung mit den aktuellen Paketen aktualisieren, funktioniert diese nicht länger mit SharePoint 2016.

Beim Arbeiten mit SharePoint-Framework-Lösungen, die mit lokalen SharePoint-Bereitstellungen kompatibel sind, sollten Sie immer prüfen, welche Patchebene die SharePoint-Zielfarm aufweist und welche Version von SharePoint-Framework unterstützt wird.

### <a name="update-packages"></a>Aktualisieren der Pakete

Beim Aktualisieren von Paketen auf neuere Versionen sollten Sie immer Ihren Paket-Manager (npm oder Yarn) verwenden. Bearbeiten Sie die Datei `package.json` nicht manuell. Wenn Sie, wie empfohlen, eine Sperrdatei verwenden, werden die Änderungen ignoriert, die Sie an der Datei `package.json` vornehmen.

Beginnen Sie damit, zu ermitteln, welche Pakete aktualisiert werden sollen und welche neuere Version verwendet werden soll. Beachten Sie, dass es ggf. nicht möglich ist, die neueste Version des angegebenen Pakets zu verwenden, da sie möglicherweise nicht mit anderen SharePoint-Framework-Abhängigkeiten wie TypeScript kompatibel ist.

Führen Sie für jedes Paket, das Sie aktualisieren möchten, den folgenden Befehl aus:

```sh
npm install mypackage@newversion --save
```

Wenn Sie zum Beispiel bisher AngularJS Version v1.5.9 verwendet haben und auf Version 1.6.5 aktualisieren möchten, müssen Sie den folgenden Befehl ausführen:

```sh
npm install angular@1.6.5 --save
```

Beim Aktualisieren des Pakets mit npm werden die angegebene Version des Pakets in Ihrem Projekt installiert sowie die Versionsnummer in den Abhängigkeiten der Datei „package.json“ und der im Projekt verwendeten Sperrdatei aktualisiert.

Führen Sie danach den folgenden Befehl aus, um alte Buildartefakte zu entfernen:

```sh
gulp clean
```

### <a name="update-your-code"></a>Aktualisieren des Codes

Bei wichtigen API-Änderungen müssen Sie ggf. den vorhandenen Projektcode und die Konfigurationsdateien aktualisieren. In jeder Version werden wichtige Änderungen sowie die an Ihrem Code erforderlichen Änderungen in den [Versionshinweisen]((https://aka.ms/spfx-release-notes)) hervorgehoben. Sie müssen den Code mit diesen Fehlerbehebungen aktualisieren.

Sie können das Projekt jederzeit erstellen, um zu erfahren, ob Fehler und Warnungen vorliegen. Führen Sie dazu den Befehl in einer Konsole im Projektverzeichnis aus:

```sh
gulp build
```

## <a name="update-yeoman-generator-for-sharepoint"></a>Aktualisieren des Yeoman-Generators für SharePoint

Wenn Sie den SharePoint-Framework-Yeoman-Generator global installiert haben, können Sie mit dem folgenden Befehl ermitteln, ob eine Aktualisierung erforderlich ist:

```sh
npm outdated -g
```

Der Befehl listet die folgenden Informationen zu den Paketen auf, die global auf Ihrem Computer installiert sind. Diese Informationen stammen aus den auf Ihrem Computer und in der npm-Registry installierten Versionen.

* Aktuelle, global auf Ihrem Computer installierte Version
* Von Ihnen bei der Installation angeforderte Version
* Neueste verfügbare Version

![Veraltete globale npm-Pakete](../../images/npm-outdated-global-packages-list.png)

Um das Generator-Paket zu ermitteln, suchen Sie nach folgendem Paketnamen:

```sh
@microsoft/generator-sharepoint
```

### <a name="update-generator-package"></a>Aktualisieren des Generator-Pakets

Öffnen Sie Ihre bevorzugte Konsole und führen Sie den folgenden Befehl aus, um den Generator auf die neueste veröffentlichte Version zu aktualisieren:

```sh
npm install @microsoft/generator-sharepoint@latest -g
```

Mit dem Befehl wird der Yeoman-Generator für SharePoint zusammen mit allen Abhängigkeiten auf die neueste veröffentlichte Version aktualisiert. Sie können dies überprüfen, indem Sie den folgenden Befehl in der Verwaltungskonsole ausführen:

```sh
npm ls @microsoft/generator-sharepoint -g --depth=0
```

## <a name="see-also"></a>Siehe auch

* [Aktualisieren von SharePoint-Framework-Projekten (Anleitung für Team-basierte Entwicklung)](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/team-based-development-on-sharepoint-framework#upgrading-sharepoint-framework-projects)
* [Aktualisieren von SharePoint-Elementen (Bereitstellen von SharePoint-Objekten)](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/toolchain/provision-sharepoint-assets#upgrade-sharepoint-items)