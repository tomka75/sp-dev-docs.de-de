---
title: "Einrichten Ihrer SharePoint-Entwicklungsumgebung für clientseitige Webparts"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: c7e48ed9dfc32d4e7aa04502507d0df532e8ed50
ms.sourcegitcommit: 53385f08de7c705ba76c6e4985c33d27ee76307e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/08/2017
---
# <a name="set-up-your-sharepoint-client-side-web-part-development-environment"></a>Einrichten Ihrer SharePoint-Entwicklungsumgebung für clientseitige Webparts

Sie können Visual Studio oder Ihre eigene benutzerdefinierte Entwicklungsumgebung verwenden, um clientseitige SharePoint-Webparts zu erstellen. Sie können einen Mac, PC oder Linux verwenden.

>**Hinweis:** Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [Ihren Office 365-Mandanten einrichten](./set-up-your-developer-tenant.md).

Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=1) nachvollziehen:

<a href="https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="install-developer-tools"></a>Installieren von Entwicklertools

### <a name="nodejs"></a>NodeJS

Installieren Sie die [NodeJS-Version 6.x](https://nodejs.org/download/release/latest-v6.x/). 

* Wenn Sie Windows verwenden, können Sie die MSI-Installationsprogramme in dem oben genannten Link verwenden, um NodeJS auf einfache Weise einzurichten.
* Wenn Sie NodeJS bereits installiert haben, überprüfen Sie mit `node -v`, ob Sie die neueste Version verwenden. Es sollte die aktuelle [LTS-Version](https://nodejs.org/en/download/) zurückgegeben werden. 
* Wenn Sie mit einem Mac arbeiten, empfehlen wir [Homebrew](http://brew.sh/) zur Installation und Verwaltung von NodeJS. 

>**Hinweis:** Die SharePoint-Framework-Buildpipeline unterstützt derzeit nicht die LTS-Version von Node.js. Laden Sie stattdessen die [Node.js-Version 6.11.5](https://nodejs.org/download/release/latest-v6.x/) herunter. So wird npm 3.10.10 installiert. Wenn Sie die Version v5.x von npm verwenden, müssen Sie zunächst ein Downgrade auf eine ältere Version von npm durchführen, indem Sie den folgenden Befehl ausführen: `npm install -g npm@3`.

### <a name="code-editors"></a>Code-Editoren

Installieren Sie einen Code-Editor. Sie können einen beliebigen Code-Editor oder eine beliebige IDE verwenden, der bzw. die die clientseitige Entwicklung unterstützt, um Ihren Webpart zu erstellen, z. B.:

* [Visual Studio Code](https://code.visualstudio.com/)
* [Atom](https://atom.io)
* [WebStorm](https://www.jetbrains.com/webstorm)

Die Schritte und Beispiele in dieser Dokumentation verwenden [Visual Studio Code](https://code.visualstudio.com/), aber Sie können einen beliebigen Editor verwenden.

### <a name="if-you-are-using-ubuntu"></a>Wenn Sie Ubuntu verwenden, gilt Folgendes:

Sie müssen mit dem folgenden Befehl Compilertools installieren:

```sh
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a>Wenn Sie Fedora verwenden

Sie müssen mit dem folgenden Befehl Compilertools installieren:

```sh
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a>Installieren von Yeoman und Gulp

[Yeoman](http://yeoman.io/) hilft Ihnen bei den ersten Schritten mit neuen Projekten und stellt bewährte Methoden und Tools bereit, mit denen Sie produktiv arbeiten können. Clientseitige SharePoint-Entwicklungstools umfassen einen Yeoman-Generator zum Erstellen neuer Webparts. Der Generator stellt allgemeine Buildtools, häufig verwendeten Boilerplate-Code und eine allgemeine Umgebungswebsite zum Hosten von Webparts für Tests bereit.

Geben Sie den folgenden Befehl ein, um Yeoman und Gulp zu installieren:

```sh
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a>Installieren des Yeoman SharePoint-Generators

Der Yeoman SharePoint-Webpart-Generator hilft Ihnen beim schnellen Erstellen eines clientseitigen SharePoint-Lösungsprojekts mit den richtigen Tools und der richtigen Projektstruktur.

Geben Sie den folgenden Befehl ein, um den SharePoint-Framework-Yeoman-Generator global zu installieren:

```sh
npm install -g @microsoft/generator-sharepoint
```

Wenn Sie zwischen den verschiedenen Projekten mit unterschiedlichen Versionen des SharePoint-Framework-Yeoman-Generators wechseln müssen, können Sie den Generator lokal als eine Entwicklungsabhängigkeit im Projektordner installieren, indem Sie den folgenden Befehl ausführen:

```sh
npm install @microsoft/generator-sharepoint --save-dev
```

## <a name="optional-tools"></a>Optionale Tools

Hier sind einige Tools, die auch nützlich sein können:

* [Fiddler](http://www.telerik.com/fiddler)
* [Postman-Plug-In für Chrome](https://www.getpostman.com/docs/introduction)
* [Cmder für Windows](http://cmder.net/)
* [Oh My Zsh für Mac](http://ohmyz.sh/)
* [Git Source Control Tools](https://git-scm.com/)

## <a name="next-steps"></a>Nächste Schritte

Sie können jetzt [Ihren ersten clientseitigen Webpart erstellen](web-parts/get-started/build-a-hello-world-web-part.md)!
