# <a name="set-up-your-sharepoint-client-side-web-part-development-environment"></a>Einrichten Ihrer SharePoint-Entwicklungsumgebung für clientseitige Webparts

Sie können Visual Studio oder Ihre eigene benutzerdefinierte Entwicklungsumgebung verwenden, um clientseitige SharePoint-Webparts zu erstellen. Sie können einen Mac, PC oder Linux verwenden.

>**Hinweis:** Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [Ihren Office 365-Mandanten einrichten](./set-up-your-developer-tenant).

Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=1) nachvollziehen: 

<a href="https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
    <img src="../../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="install-developer-tools"></a>Installieren von Entwicklertools

### <a name="nodejs"></a>NodeJS
Installieren Sie [NodeJS](https://nodejs.org/en/) Long Term Support (LTS).

* Wenn Sie NodeJS bereits installiert haben, überprüfen Sie mit `node -v`, ob Sie die neueste Version verwenden. Es sollte die aktuelle [LTS-Version](https://nodejs.org/en/download/) zurückgegeben werden. 
* Wenn Sie mit einem Mac arbeiten, empfehlen wir [Homebrew](http://brew.sh/) zur Installation und Verwaltung von NodeJS. 

> Beachten Sie: Die SPFx-Buildpipeline unterstützt npm v5.x derzeit **NICHT**. Sie müssen daher entweder v3 oder v4 verwenden. Als dieser Artikel verfasst wurde, installierte die LTS-Version von NodeJS (v6.11.0) die Version 3.10.10 von npm. Wir werden diesen Abschnitt aktualisieren, sobald sich Änderungen bei der Unterstützung ergeben. Ein Downgrade auf eine ältere npm-Version können Sie über den Befehl `npm install -g npm@3` durchführen.

### <a name="code-editors"></a>Code-Editoren
Installieren Sie einen Code-Editor. Sie können einen beliebigen Code-Editor oder eine beliebige IDE verwenden, der bzw. die die clientseitige Entwicklung unterstützt, um Ihren Webpart zu erstellen, z. B.:

* [Visual Studio Code](https://code.visualstudio.com/)
* [Atom](https://atom.io)
* [WebStorm](https://www.jetbrains.com/webstorm) 

Die Schritte und Beispiele in dieser Dokumentation verwenden [Visual Studio Code](https://code.visualstudio.com/), aber Sie können einen beliebigen Editor verwenden. 

### <a name="if-you-are-using-ubuntu"></a>Wenn Sie Ubuntu verwenden, gilt Folgendes:

Sie müssen mit dem folgenden Befehl Compilertools installieren:
    
```
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a>Wenn Sie Fedora verwenden

Sie müssen mit dem folgenden Befehl Compilertools installieren:
    
```
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a>Installieren von Yeoman und Gulp

[Yeoman](http://yeoman.io/) hilft Ihnen bei den ersten Schritten mit neuen Projekten und stellt bewährte Methoden und Tools bereit, mit denen Sie produktiv arbeiten können. Clientseitige SharePoint-Entwicklungstools umfassen einen Yeoman-Generator zum Erstellen neuer Webparts. Der Generator stellt allgemeine Buildtools, häufig verwendeten Boilerplate-Code und eine allgemeine Umgebungswebsite zum Hosten von Webparts für Tests bereit.

Geben Sie den folgenden Befehl ein, um Yeoman und Gulp zu installieren:
    
```
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a>Installieren des Yeoman SharePoint-Generators

Der Yeoman SharePoint-Webpart-Generator hilft Ihnen beim schnellen Erstellen eines clientseitigen SharePoint-Lösungsprojekts mit den richtigen Tools und der richtigen Projektstruktur.

Geben Sie den folgenden Befehl ein, um den Yeoman SharePoint-Generator zu installieren:
    
```
npm install -g @microsoft/generator-sharepoint 
```
>**Hinweis:** Der Yeoman-Generator für SharePoint ist für die globale Bereitstellung mit der Erstversion General Availability (GA) vorgesehen. Bei lokaler Installation im Projekt treten bekannte Probleme auf, die nach der GA-Version behoben werden.


## <a name="optional-tools"></a>Optionale Tools

Hier sind einige Tools, die auch nützlich sein können:

* [Fiddler](http://www.telerik.com/fiddler)
* [Postman-Plug-In für Chrome](https://www.getpostman.com/docs/introduction)
* [Cmder für Windows](http://cmder.net/)
* [Oh My Zsh für Mac](http://ohmyz.sh/)
* [Git Source Control Tools](https://git-scm.com/)

## <a name="next-steps"></a>Nächste Schritte

Sie können jetzt [Ihren ersten clientseitigen Webpart erstellen](web-parts/get-started/build-a-hello-world-web-part)!
