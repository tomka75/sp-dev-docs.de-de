
# <a name="create-an-office-add-in-using-any-editor"></a>Erstellen eines Office-Add-Ins mit einem beliebigen Editor

Sie können den Yeoman-Generator zum Erstellen Ihrer Office-Add-Ins verwenden. Der Yeoman-Generator stellt das Projektgerüst und die Buildverwaltung bereit. Die Datei `manifest.xml` teilt der Office-Anwendung mit, wo Ihr Add-In gespeichert ist und wie es angezeigt werden soll. Die Office-Anwendung übernimmt das Hosten des Add-Ins in Office.

 >**Hinweis:** Diese Anweisungen gehen von der Verwendung eines Mac-Terminals aus. Sie können jedoch auch andere Shellumgebungen verwenden. 


## <a name="prerequisites-for-the-yeoman-generator"></a>Erforderliche Komponenten für den Yeoman-Generator

Vor der Installation des Yeoman-Office-Generators müssen [git](https://git-scm.com/downloads) und node.js auf Ihrem Computer installiert sein. Mac-Benutzern empfehlen wir [Node Version Manager](https://github.com/creationix/nvm) zur Installation von node.js mit den korrekten Berechtigungen. Windows-Benutzer können node.js über [nodejs.org](https://nodejs.org/en/) installieren.

>**Hinweis:** Installieren Sie git unter Windows mit den Standardwerten. Ausnahmen:

>- Verwenden von git über die Windows-Eingabeaufforderung
>- Verwenden des Standardkonsolenfensters von Windows

Öffnen Sie nach der Installation von node.js ein Terminal, und installieren Sie den Generator global.

```
npm install -g yo generator-office
```


## <a name="create-the-default-files-for-your-add-in"></a>Erstellen der Standarddateien für Ihr Add-In

Der Yeoman-Generator wird in dem Verzeichnis ausgeführt, in dem Sie das Gerüst für das Projekt erstellen möchten. Bevor Sie ein Office-Add-In entwickeln, müssen Sie zunächst einen Ordner für Ihr Projekt erstellen.

Wechseln Sie im Terminal in den übergeordneten Ordner, in dem Sie Ihr Projekt erstellen möchten. Erstellen Sie anschließend mit den folgenden Befehlen einen neuen Ordner mit dem Namen _myHelloWorldaddin_, und wechseln Sie in diesen Ordner:




```
mkdir myHelloWorldaddin
cd myHelloWorldaddin
```

Verwenden Sie den Yeoman-Generator, um das Add-In des gewünschten Typs zu erstellen: Mit den Schritten in diesem Artikel erstellen Sie ein einfaches Aufgabenbereich-Add-In. Geben Sie zur Ausführung des Generators den folgenden Befehl ein:




```
yo office
```

**Yeoman-Generator-Eingabe für ein Add-In**

Sie werden von dem Generator aufgefordert, Folgendes anzugeben: 


- Neuer Unterordner: Verwenden Sie _N_.
- Name des Add-Ins: Verwenden Sie _myHelloWorldaddin_. 
- Die unterstützte Office-Anwendung: Sie können eine beliebige Anwendung auswählen.
- Neues Add-In erstellen: Verwenden Sie _Yes, I want a new add-in._
- [TypeScript](https://www.typescriptlang.org/) hinzufügen: Verwenden Sie _N_.
- Framework auswählen: Verwenden Sie _Jquery_.

>**Hinweis:** Wenn Sie ein Office-Add-In erstellen möchten, das Office UI Fabric React verwendet, geben Sie Folgendes ein:
>- [TypeScript](https://www.typescriptlang.org/) hinzufügen: Verwenden Sie _Y_.
>- Framework auswählen: Verwenden Sie _React_.

![GIF von Yeoman-Generator mit einer Aufforderung zur Projekteingabe](../../images/gettingstarted-fast.gif)

Dadurch werden die Struktur und die grundlegenden Dateien für Ihr Add-In erstellt.


## <a name="hosting-your-office-add-in"></a>Hosten Ihres Office-Add-Ins

Office-Add-Ins müssen per HTTPS gehostet werden, auch während der Entwicklung. Yo Office erstellt die Datei „bsconfig.json“, die wiederum Browsersync verwendet. Dieses Modul synchronisiert Dateiänderungen über mehrere Geräte hinweg und macht es Ihnen damit einfacher, Ihr Add-In anzupassen und zu testen. 

Geben Sie den folgenden Befehl in die Konsole ein, um die lokale HTTPS-Website unter „https://localhost:3000“ zu öffnen:


```
npm start
```

Browsersync startet nun einen HTTPS-Server und öffnet die Datei „index.html“ aus Ihrem Projekt. Es wird ein Fehler angezeigt, der ein Problem mit dem Sicherheitszertifikat der Website meldet.


![GIF mit der Umgehung des Fehlers zum Anzeigen der Standarddatei „index.html“](../../images/ssl-chrome-bypass.gif)

Dieser Fehler tritt auf, weil Browsersync ein selbstsigniertes SSL-Zertifikat enthält, dem Ihre Entwicklungsumgebung vertrauen muss. Informationen zur Behebung dieses Fehlers finden Sie in diesem Artikel zum Thema [Hinzufügen von selbstsignierten Zertifikaten](https://github.com/OfficeDev/generator-office/blob/master/src/docs/ssl.md).

## <a name="sideload-the-add-in-into-office"></a>Querladen des Add-Ins in Office

Sie können das Add-In mittels Querladen zu Testzwecken auf den Office-Clients installieren:

- [Querladen von Office-Add-Ins zu Testzwecken](../testing/create-a-network-shared-folder-catalog-for-task-pane-and-content-add-ins.md)
- [Querladen von Office-Add-Ins auf dem iPad und Mac zu Testzwecken](../testing/sideload-an-office-add-in-on-ipad-and-mac.md)   
- [Querladen von Outlook-Add-Ins zu Testzwecken](../outlook/testing-and-tips.md)

## <a name="develop-your-office-add-in"></a>Entwickeln Ihres Office-Add-Ins

Zur Entwicklung der Dateien für Ihr benutzerdefiniertes Office-Add-In können Sie einen beliebigen Text-Editor verwenden.

> **Wichtig:** In der Datei„manifest-myHelloWorldaddin.xml“ ist definiert, wie die Office-Clientanwendungen mit dem Add-In interagieren sollen. Der Wert im Tag `<id>` ist eine GUID, die Yo Office bei der Erstellung des Projekts generiert. Ändern Sie die GUID Ihres Add-Ins nicht. Wenn der Host Azure ist, ist der `SourceLocation`-Wert eine URL, die _https://[Name-Ihrer-Web-App].azurewebsites.net/[Pfad-zum-Add-In]_ ähnelt. Wenn Sie Ihr Add-In wie in diesem Beispiel selbst hosten, lautet die URL _https://localhost:3000/[Pfad-zum-Add-In]_.


## <a name="debug-your-office-add-in"></a>Debuggen Ihres Office-Add-Ins

Sie können Ihr Add-In auf verschiedene Arten debuggen:

- Fügen Sie einen Debugger aus dem Aufgabenbereich (Office 2016 für Windows) an.
- Verwenden Sie die Entwicklertools Ihres Browsers.
- Verwenden Sie die F12-Entwicklertools unter Windows 10

### <a name="attach-debugger-from-the-task-pane"></a>Anfügen eines Debuggers aus dem Aufgabenbereich

In Office 2016 für Windows, Build 77xx.xxxx oder höher, können Sie den Debugger aus dem Aufgabenbereich anfügen. 

Um das Tool **Debugger anfügen**, und klicken Sie auf die obere rechte Ecke des Aufgabenbereichs, um das Menü **Persönlichkeit** (wie in dem roten Kreis in der folgenden Abbildung dargestellt) zu aktivieren.   

![Screenshot des Menüs „Debugger anfügen“](../../images/attach-debugger.png)

Wählen Sie **Debugger anfügen** aus. Dadurch wird das Dialogfeld **Just-In-Time-Debugger von Visual Studio**, wie in der folgenden Abbildung dargestellt, angezeigt. 

![Screenshot des Dialogfelds des JIT-Debuggers von Visual Studio](../../images/visual-studio-debugger.png)

Sie können den Debugger dann anfügen und das Debuggen in Visual Studio ausführen.   

  >**Hinweis**:  Derzeit ist [Visual Studio 2015](https://www.visualstudio.com/downloads/) mit [Update 3](https://msdn.microsoft.com/en-us/library/mt752379.aspx) das einzige unterstützte Debugger-Tool. Wenn Sie Visual Studio nicht installiert haben, hat das Auswählen der Option **Debugger anfügen** keine Auswirkung.  
  
Weitere Informationen hierzu finden Sie unter folgenden Themen:

-    Zum Starten und Verwenden des DOM-Explorers in Visual Studio lesen Sie Tipp 4 im Abschnitt [Tips and Tricks](https://blogs.msdn.microsoft.com/officeapps/2013/04/16/building-great-looking-apps-for-office-using-the-new-project-templates/#tips_tricks) des Blogbeitrags [Building great-looking apps for Office using the new project templates (Erstellen ansprechender Apps für Office mithilfe der neuen Projektvorlagen)](https://blogs.msdn.microsoft.com/officeapps/2013/04/16/building-great-looking-apps-for-office-using-the-new-project-templates).
-    Informationen zum Festlegen von Haltepunkten finden Sie unter [Verwenden von Haltepunkten](https://msdn.microsoft.com/en-US/library/5557y8b4.aspx).
-    Informationen zur Verwendung von F12 finden Sie unter [Verwenden der F12-Entwicklertools](https://msdn.microsoft.com/en-us/library/bg182326(v=vs.85).aspx).

### <a name="browser-developer-tools"></a>Entwicklertools des Browsers 

Sie können die Office-Webclients verwenden und die Entwicklertools des Browsers öffnen, um das Add-In so wie jede andere clientseitige JavaScript-Anwendung auch zu debuggen. 

### <a name="f12-developer-tools-on-windows-10"></a>F12-Entwicklertools unter Windows 10

Wenn Sie den Office-Desktopclient unter Windows 10 verwenden, können Sie [Add-Ins mithilfe von F12-Entwicklertools unter Windows 10 debuggen](../testing/debug-add-ins-using-f12-developer-tools-on-windows-10.md).
    
## <a name="additional-resources"></a>Zusätzliche Ressourcen


- [Erstellen und Debuggen von Office-Add-Ins in Visual Studio](../../docs/get-started/create-and-debug-office-add-ins-in-visual-studio.md)
    
