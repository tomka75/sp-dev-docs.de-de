---
title: "Debuggen von SharePoint-Framework-Lösungen in Visual Studio Code"
description: "Erforderliche Komponenten und Schritte zum Konfigurieren von Visual Studio Code für das Debuggen von SharePoint Framework-Lösungen."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 3e5687a6fe0a617d5eeb999ff00e376f948cb177
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="debug-sharepoint-framework-solutions-in-visual-studio-code"></a>Debuggen von SharePoint-Framework-Lösungen in Visual Studio Code

Visual Studio Code ist eine beliebter Code-Editor, der häufig zur Erstellung von SharePoint Framework-Lösungen verwendet wird. Wenn Sie Ihre SharePoint Framework-Lösung in Visual Studio Code debuggen, können Sie Ihren Code effizienter durcharbeiten und Fehler beheben. 

In einem Video in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=oNChcluMrm8&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG) werden auch die erforderlichen Schritte zum Aktivieren von Debugging in Visual Studio Code erläutert. 

<a href="https://www.youtube.com/watch?v=oNChcluMrm8&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../images/spfx-debug-youtube.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="prerequisites"></a>Voraussetzungen

Am einfachsten lässt sich Visual Studio Code mit Google Chrome und der Visual Studio Code-Extension „Debugger for Chrome“ für das Debuggen von SharePoint Framework-Lösungen konfigurieren. Ab SharePoint-Framework-Yeoman-Generator Version 1.3.4 werden Standardprojektvorlagen (Webparts und Erweiterungen) mit zugehörigen Voraussetzungen geliefert und fordern zur Installation der erforderlichen Visual Studio Code-Erweiterungen auf. In diesem Fall werden Sie aufgefordert, die Chrome-Debugger-Erweiterung für Visual Studio Code zu installieren.

Sie benötigen auch Google Chrome. [Laden Sie die aktuelle Version von Google Chrome herunter, und installieren Sie sie](https://www.google.com/chrome/browser/desktop/index.html).

Wenn Sie eine ältere Version des SharePoint-Framework-Yeoman-Generators als 1.3.4 verwenden, können Sie [die Chrome-Debugger-Erweiterung für Visual Studio Code aus dem Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) installieren.

## <a name="debug-configurations"></a>Debugkonfigurationen

Die Debugkonfigurationen sind in der Datei „launch.json“ im folgenden Visual Studio Code-Arbeitsbereichordner enthalten:

```
project-name\.vscode
```

Die Datei „launch.json“ enthält zwei Debugkonfigurationen:
* Konfiguration für die lokale Workbench
* Konfiguration für die gehostete Workbench

## <a name="debug-solution-using-local-workbench"></a>Debuggen der Lösung mithilfe der lokalen Workbench

Während der Erstellung von SharePoint Framework-Lösungen können Sie mithilfe der lokalen Workbench überprüfen, ob Ihr Webpart einwandfrei funktioniert. Über die lokale Workbench lassen sich komfortabel alle Szenarien testen, die keine Kommunikation mit SharePoint erfordern. Sie eignet sich zudem für die Offline-Entwicklung.

Sobald Sie Visual Studio Code für das Debuggen von SharePoint Framework-Lösungen mit Google Chrome und der lokalen Workbench konfiguriert haben, können Sie überprüfen, ob alles wie erwartet funktioniert.

### <a name="configure-a-breakpoint"></a>Konfigurieren eines Haltepunkts

1. Öffnen Sie in Visual Studio Code die Quelldatei des Hauptwebparts, und fügen Sie in der ersten Zeile der Methode **render** einen Haltepunkt hinzu. Klicken Sie dazu entweder links neben die Zeilennummer, oder markieren Sie die Codezeile im Editor, und drücken Sie die Taste F9.

    ![Haltepunkt, konfiguriert in einem clientseitigen SharePoint-Framework-Webpart in Visual Studio Code](../images/vscode-debugging-breakpoint-configured.png)

2. Wählen Sie in Visual Studio Code im Menü **Anzeigen** die Option **Integriertes Terminal** aus, oder drücken Sie **STRG+`** auf der Tastatur. 

3. Führen Sie im Terminal den folgenden Befehl aus:

    ```sh
    gulp serve --nobrowser
    ```

    Dieser Befehl erstellt Ihre SharePoint Framework-Lösung und startet den lokalen Webserver, der dann die Ausgabedateien ausliefert. Da der Debugger eine eigene Instanz des Browsers startet, verwenden Sie das Argument **--nobrowser**. Es verhindert, dass der Task **serve** ein Browserfenster öffnet.

    ![Befehl „gulp serve“ im integrierten Terminal in Visual Studio Code](../images/vscode-debugging-gulp-serve.png)

### <a name="start-debugging-in-visual-studio-code"></a>Starten des Debuggens in Visual Studio Code

Wechseln Sie nach Abschluss des gulp-Tasks in den Codebereich von Visual Studio Code, und drücken Sie F5. (Alternativ können Sie aus dem Menü **Debuggen** die Option **Debugging starten** auswählen.) 

Der Debugmodus in Visual Studio Code startet, und die Statusleiste wird orange. Außerdem wird ein neues Google Chrome-Fenster mit der lokalen Version der SharePoint-Workbench geöffnet.

> [!NOTE] 
> Zu diesem Zeitpunkt ist der Haltepunkt deaktiviert, da der Code des Webparts noch nicht geladen wurde. SharePoint Framework kann Webparts erst bei Bedarf laden, wenn sie der Seite hinzugefügt wurden.

![Visual Studio Code im Debugmodus neben Google Chrome mit der lokalen Version der SharePoint-Workbench](../images/vscode-debugging-chrome-started.png)


### <a name="add-a-web-part-to-the-canvas"></a>Hinzufügen eines Webparts zum Zeichenbereich

Um zu überprüfen, ob das Debuggen funktioniert, fügen Sie Ihr Webpart in der Workbench nun dem Zeichenbereich hinzu.

![Geöffnete Webpart-Toolbox in der SharePoint-Workbench](../images/vscode-debugging-adding-web-part-to-canvas.png)

<br/>

Sie sehen: Jetzt da der Code auf der Seite geladen wurde, ist der Haltepunktindikator aktiviert.

![Aktivierter Haltepunkt nach Hinzufügen des Webparts zum Zeichenbereich](../images/vscode-debugging-breakpoint-active.png)

<br/>

Wenn Sie die Seite nun neu laden, greift der Haltepunkt in Visual Studio Code, und Sie können alle Eigenschaften prüfen und den Code Schritt für Schritt durcharbeiten.

![Greifen des Haltepunkts in Visual Studio Code](../images/vscode-debugging-breakpoint-hit.png)

## <a name="debug-solution-using-hosted-workbench"></a>Debuggen der Lösung mithilfe der gehosteten Workbench

Wenn Sie SharePoint Framework-Lösungen erstellen, die mit SharePoint kommunizieren, möchten Sie möglicherweise überprüfen, ob die Interaktion zwischen Ihrer Lösung und SharePoint funktioniert. Das geht ganz einfach mit der gehosteten Version der SharePoint-Workbench. Sie ist auf jedem Office 365-Mandanten verfügbar, unter der Adresse `https://yourtenant.sharepoint.com/_layouts/workbench.aspx`. 

Da solche Tests während der Erstellung von SharePoint-Framework-Lösungen regelmäßig durchgeführt werden, ist es empfehlenswert, eine separate Debugkonfiguration für die gehostete Version der SharePoint-Workbench zu erstellen.

### <a name="debug-solution-using-hosted-workbench"></a>Debuggen der Lösung mithilfe der gehosteten Workbench

1. Öffnen Sie die Datei „launch.json“ und ersetzen Sie die `url`-Eigenschaft in der Konfiguration für die *gehostete Workbench* durch die URL Ihrer SharePoint-Website.

    ```json
    "url": "https://enter-your-SharePoint-site/_layouts/workbench.aspx",
    ```

2. Öffnen Sie in Visual Studio Code den Bereich **Debuggen**, und wählen Sie aus der Liste **Konfigurationen** die gerade erstellte Konfiguration für die **gehostete Workbench** aus.

    ![Ausgewählte Konfiguration „Hosted workbench“ im Dropdownmenü mit den Debugkonfigurationen in Visual Studio Code](../images/vscode-debugging-debugging-hosted-workbench.png)

3. Starten Sie das Debuggen. Drücken Sie dazu entweder die Taste F5, oder wählen Sie aus dem Menü **Debuggen** die Option **Debugging starten** aus. Visual Studio Code wechselt in den Debugmodus, und die Statusleiste wird orange. Außerdem öffnet die Extension „Debugger for Chrome“ eine neue Instanz von Google Chrome mit der Office 365-Anmeldeseite.

    ![Office 365-Anmeldeseite in Google Chrome nach dem Start des Debuggens in der gehosteten Workbench](../images/vscode-debugging-o365-login.png)

4. Fügen Sie nach der Anmeldung das Webpart zum Zeichenbereich hinzu, und aktualisieren Sie die Workbench, so wie dies mit der lokalen Workbench getan haben. Sie werden sehen, wie der Haltepunkt in Visual Studio Code gegriffen wird. Außerdem können Sie Variablen überprüfen und den Code durchlaufen.

    ![Greifen des Haltepunkts in Visual Studio Code beim Debuggen eines clientseitigen SharePoint-Framework-Webparts in der gehosteten Workbench](../images/vscode-debugging-breakpoint-hit-o365.png)

## <a name="for-older-projects"></a>Für ältere Projekte

Wenn Sie eine ältere Version des SharePoint-Framework-Yeoman-Generators verwenden, führen Sie die folgenden Schritte aus, um die Datei „launch.json“ manuell zu erstellen.

### <a name="create-debug-configuration-for-local-workbench"></a>Erstellen einer Debugkonfiguration für die lokale Workbench

1. Öffnen Sie in Visual Studio Code den Bereich **Debuggen**.

    ![Geöffneter Bereich „Debuggen“ in Visual Studio Code](../images/vscode-debugging-vscode-debug.png)

2. Öffnen Sie im oberen Abschnitt des Bereichs die Liste **Konfigurationen**, und wählen Sie die Option **Konfiguration hinzufügen...** aus.

    ![Hervorgehobene Option „Konfiguration hinzufügen...“ im Dropdownmenü mit den Debugkonfigurationen](../images/vscode-debugging-add-debug-configuration.png)

3. Wählen Sie aus der Liste der Debugumgebungen **Chrome** aus.

    ![Chrome hervorgehoben als Debugumgebung für die neue Konfiguration](../images/vscode-debugging-chrome-debug-environment.png)

4. Ersetzen Sie den Inhalt der generierten Datei **launch.json** durch:

    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "Local workbench",
                "type": "chrome",
                "request": "launch",
                "url": "https://localhost:4321/temp/workbench.html",
                "webRoot": "${workspaceRoot}",
                "sourceMaps": true,
                "sourceMapPathOverrides": {
                    "webpack:///../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../../src/*": "${webRoot}/src/*"
                },
                "runtimeArgs": [
                    "--remote-debugging-port=9222"
                ]
            }
        ]
    }
    ```

    Diese Konfiguration verwendet den Debugger **chrome**, der in der Extension **Debugger for Chrome** enthalten ist. Sie verweist auf die URL der lokalen Workbench als Ausgangspunkt. Essenziell beim Debuggen von TypeScript-Code ist die Konfiguration von Quellzuordnungen, die der Debugger nutzt, um im Browser ausgeführtes JavaScript dem ursprünglichen TypeScript-Code zuzuordnen.

### <a name="create-debug-configuration-for-hosted-workbench"></a>Erstellen einer Debugkonfiguration für die gehostete Workbench

1. Öffnen Sie in Visual Studio Code die Datei **./.vscode/launch.json**. 

2. Kopieren Sie die vorhandene Debugkonfiguration, und verwenden Sie die URL der gehosteten Workbench:

    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "Local workbench",
                "type": "chrome",
                "request": "launch",
                "url": "https://localhost:4321/temp/workbench.html",
                "webRoot": "${workspaceRoot}",
                "sourceMaps": true,
                "sourceMapPathOverrides": {
                    "webpack:///../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../../src/*": "${webRoot}/src/*"
                },
                "runtimeArgs": [
                    "--remote-debugging-port=9222"
                ]
            },
            {
                "name": "Hosted workbench",
                "type": "chrome",
                "request": "launch",
                "url": "https://contoso.sharepoint.com/_layouts/workbench.aspx",
                "webRoot": "${workspaceRoot}",
                "sourceMaps": true,
                "sourceMapPathOverrides": {
                    "webpack:///../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../../src/*": "${webRoot}/src/*"
                },
                "runtimeArgs": [
                    "--remote-debugging-port=9222"
                ]
            }
        ]
    }
    ```

## <a name="see-also"></a>Weitere Artikel

- [How to debug your SharePoint Framework web part (Elio Struyf)](https://www.eliostruyf.com/how-to-debug-your-sharepoint-framework-web-part/)
- [Debug SPFx React webpart with Visual Studio Code (Velin Georgiev)](https://blog.velingeorgiev.com/how-debug-sharepoint-framework-webpart-visual-studio-code)
- [Erstellen von Gerüsten für Projekte unter Verwendung des Yeoman-Generators von SharePoint](toolchain/scaffolding-projects-using-yeoman-sharepoint-generator.md)
- [SharePoint Framework-Übersicht](sharepoint-framework-overview.md)
