---
title: Aktualisieren von SharePoint-Framework-Paketen
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: b8d542ac73d1739faff65f4636cffdef062a3c00
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="update-sharepoint-framework-packages"></a>Aktualisieren von SharePoint-Framework-Paketen 

Die SharePoint-Tools für die clientseitige Entwicklung verwenden den [npm](https://www.npmjs.com/)-Paket-Manager, um Abhängigkeiten und andere erforderliche JavaScript-Hilfsprogramme zu verwalten. npm ist in der Regel als Teil des Node.js-Setups enthalten.

Beim Erstellen einer neuen clientseitigen Lösung ruft der Yeoman-Generator für SharePoint die neuesten SharePoint-Framework-Pakete ab, die für Ihr clientseitiges Projekt erforderlich sind. Ihre vorhandenen Pakete sind ggf. veraltet und möglicherweise stehen zum Erstellen Ihres Projekts neue Versionen der Pakete zur Verfügung. Entsprechend den [Versionshinweisen](https://aka.ms/spfx-release-notes) für eine bestimmte Version oder das neueste Paket können Sie die in Ihrem Projekt verwendeten SharePoint-Framework-Pakete aktualisieren. SharePoint Framework-Pakete enthalten die npm-Pakete, die Sie in Ihrem Projekt installiert haben (Beispiel: [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library)), sowie die global installierten npm-Pakete (Beispiel: [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint)). 

Obwohl nicht erforderlich, empfiehlt es sich, die SharePoint Framework-Pakete regelmäßig zu aktualisieren, um alle neuesten Änderungen und Updates zu erhalten. 

## <a name="find-outdated-packages-in-your-project"></a>Suche nach veralteten Paketen im Projekt
Führen Sie in einer Konsole im selben Verzeichnis wie das Projekt den folgenden Befehl aus, um nach veralteten Paketen in Ihrem clientseitigen Projekt zu suchen, einschließlich SharePoint Framework-Paketen und anderen, von denen Ihr Projekt abhängt. 

```
npm outdated
```

Der Befehl listet die folgenden Informationen zu den Paketen auf, von denen Ihr Projekt abhängt. Diese Informationen werden der Datei `package.json` im Stammverzeichnis des Projekts und der npm-Registry entnommen.

* Aktuelle, in Ihrem Projekt installierte Version
* Von Ihrem Projekt angeforderte Version (verfügbar in `package.json`)
* Neueste verfügbare Version

![Veraltete NPM-Pakete](../../images/npm-outdated-packages-list.png)

Um die SharePoint Framework Pakete zu identifizieren, suchen Sie nach den Paketnamen, die mit dem folgenden npm-Bereich und -Präfix beginnen:

```
@microsoft/sp-
```
Zusammen mit den Framework-Paketen müssen Sie ggf. auch die Pakete `react` und `office-ui-fabric-react` aktualisieren. Lesen Sie unbedingt die [Versionshinweise](https://aka.ms/spfx-release-notes) für die jeweilige Version, um zu erfahren, welche Pakete eine Aktualisierung erfordern, und entsprechend planen zu können.

### <a name="update-packages"></a>Aktualisieren der Pakete
Um ein oder mehrere Pakete auf die neueste Version zu aktualisieren, müssen Sie die Paketinformationen in der Datei `package.json` bearbeiten und dann die neuesten Pakete abrufen.

#### <a name="update-package-versions"></a>Aktualisieren der Paketversionen
Öffnen Sie das Projekt in Ihrem bevorzugten Codeeditor, und suchen Sie im Stammverzeichnis des Projekts nach der Datei `package.json`.

Suchen Sie in der Datei `package.json` im Abschnitt `dependencies` und `devDependencies` nach den Paketen und aktualisieren Sie diese auf die neueste, im Befehl `npm outdated` aufgeführte Version. Beispiel: Im nachfolgenden Bild sind die Versionsaktualisierungen der SharePoint Framework-Pakete hervorgehoben. Links befinden sich die alten und rechts die neuen Versionen.

![Bearbeiten der Paketversionen in der Datei „package.json“](../../images/npm-update-packagejson-versions.png)

Nachdem Sie die Paketversionen aktualisiert haben, speichern Sie die Datei `package.json`.

#### <a name="update-packages"></a>Aktualisieren der Pakete
Öffnen Sie Ihre bevorzugte Konsole und navigieren Sie zum Stammverzeichnis des Projekts. Führen Sie zum Aktualisieren der Pakete die nachstehenden Anweisungen aus:

Löschen Sie den Ordner `node_modules`. Dies ist der Ordner, in dem npm die Pakete für Ihr Projekt lokal installiert. Durch Löschen dieses Ordners wird npm gezwungen, die neuesten Pakete abzurufen, anstatt die vorhandenen zu duplizieren.

Wenn Sie eine Mac- oder Linux-Umgebung verwenden, führen Sie den folgenden Befehl aus:

```
rm -rf node_modules/
```

Wenn Sie eine Windows-Umgebung verwenden, führen Sie den folgenden Befehl aus:

```
 rd /s /q node_modules/
```

Führen Sie nun zum Abrufen der neuesten Pakete aus der npm-Registry den folgenden Befehl aus:

```
npm install
```

Mit diesem Befehl wird der Ordner `node_modules` erstellt und es werden auf Grundlage der Informationen aus der Datei `package.json` alle Pakete und Abhängigkeiten installiert, die für Ihr Projekt erforderlich sind. Nach dem Aktualisieren der Datei mit den neuesten Versionen sind nun die neuesten Pakete und Abhängigkeiten installiert. 

Führen Sie danach den folgenden Befehl aus, um alte Buildartefakte zu entfernen:

```
gulp clean
```

### <a name="update-your-code"></a>Aktualisieren des Codes
Bei wichtigen API-Änderungen müssen Sie ggf. den vorhandenen Projektcode und die Konfigurationsdateien aktualisieren. In jeder Version werden wichtige Änderungen sowie die an Ihrem Code erforderlichen Änderungen in den [Versionshinweisen](https://aka.ms/spfx-release-notes) hervorgehoben. Sie müssen den Code mit diesen Fehlerbehebungen aktualisieren.

Sie können das Projekt jederzeit erstellen, um zu erfahren, ob Fehler und Warnungen vorliegen. Führen Sie dazu den Befehl in einer Konsole im Projektverzeichnis aus:

```
gulp build
```

## <a name="update-yeoman-generator-for-sharepoint"></a>Aktualisieren des Yeoman-Generators für SharePoint
Im Gegensatz zu den npm-Paketen, die für ein bestimmtes clientseitiges Projekt installiert werden, wird der Yeoman-Generator für SharePoint global auf Ihrem Computer installiert.

Um herauszufinden, ob der Yeoman-Generator für SharePoint aktuell ist, führen Sie den folgenden Befehl in einem Konsolenfenster aus. 

```
npm outdated -g
```

Der Befehl listet die folgenden Informationen zu den Paketen auf, die global auf Ihrem Computer installiert sind. Diese Informationen stammen aus den auf Ihrem Computer und in der npm-Registry installierten Versionen.

* Aktuelle, global auf Ihrem Computer installierte Version
* Von Ihnen bei der Installation angeforderte Version
* Neueste verfügbare Version

![Veraltete globale npm-Pakete](../../images/npm-outdated-global-packages-list.png)

Um das Generator-Paket zu ermitteln, suchen Sie nach folgendem Paketnamen:

```
@microsoft/generator-sharepoint
```

### <a name="update-generator-package"></a>Aktualisieren des Generator-Pakets
Öffnen Sie Ihre bevorzugte Konsole und führen Sie den folgenden Befehl aus, um den Generator auf die neueste veröffentlichte Version zu aktualisieren:

```
npm install @microsoft/generator-sharepoint@latest -g
```

Mit dem Befehl wird der Yeoman-Generator für SharePoint zusammen mit allen Abhängigkeiten auf die neueste veröffentlichte Version aktualisiert. Sie können dies überprüfen, indem Sie den folgenden Befehl in der Verwaltungskonsole ausführen:

```
npm ls @microsoft/generator-sharepoint -g --depth=0
```






 
