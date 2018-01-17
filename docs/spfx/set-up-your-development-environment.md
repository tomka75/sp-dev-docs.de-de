---
title: Einrichten Ihrer SharePoint Framework-Entwicklungsumgebung
ms.date: 12/11/2017
ms.prod: sharepoint
ms.openlocfilehash: 1259ceae3b13efdd0d359734fef6d080696a2c6a
ms.sourcegitcommit: 6018dbb696faef5f60ebf0f79f830385fab2a4d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/11/2017
---
# <a name="set-up-your-sharepoint-framework-development-environment"></a><span data-ttu-id="e76de-102">Einrichten Ihrer SharePoint Framework-Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="e76de-102">Set up your SharePoint client-side web part development environment</span></span>

<span data-ttu-id="e76de-p101">Sie können Visual Studio oder Ihre eigene benutzerdefinierte Entwicklungsumgebung verwenden, um SharePoint Framework-Lösungen zu erstellen. Sie können einen Mac, PC oder Linux verwenden.</span><span class="sxs-lookup"><span data-stu-id="e76de-p101">You can use Visual Studio, or your own custom development environment to build SharePoint client-side web parts. You can use a Mac, PC, or Linux.</span></span>

><span data-ttu-id="e76de-105">**Hinweis:** Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [Ihren Office 365-Mandanten einrichten](./set-up-your-developer-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e76de-105">**Note:** Before following the steps in this article, be sure to [Set up your Office 365 Tenant](./set-up-your-developer-tenant.md).</span></span>

<span data-ttu-id="e76de-106">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq) nachvollziehen:</span><span class="sxs-lookup"><span data-stu-id="e76de-106">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span>

<span data-ttu-id="e76de-107"><a href="https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a></span><span class="sxs-lookup"><span data-stu-id="e76de-107"><a href="https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a></span></span>

## <a name="install-developer-tools"></a><span data-ttu-id="e76de-108">Installieren von Entwicklertools</span><span class="sxs-lookup"><span data-stu-id="e76de-108">Install developer tools</span></span>

### <a name="nodejs"></a><span data-ttu-id="e76de-109">NodeJS</span><span class="sxs-lookup"><span data-stu-id="e76de-109">NodeJS</span></span>

<span data-ttu-id="e76de-110">Installieren Sie die [NodeJS-Version 6.x](https://nodejs.org/download/release/latest-v6.x/).</span><span class="sxs-lookup"><span data-stu-id="e76de-110">Install [NodeJS version 6.x](https://nodejs.org/download/release/latest-v6.x/).</span></span> 

* <span data-ttu-id="e76de-111">Wenn Sie Windows verwenden, können Sie die MSI-Installationsprogramme in dem oben genannten Link verwenden, um NodeJS auf einfache Weise einzurichten.</span><span class="sxs-lookup"><span data-stu-id="e76de-111">If you are in Windows, you can use the msi installers in the above link for easiest way to setup NodeJS</span></span>
* <span data-ttu-id="e76de-p102">Wenn Sie NodeJS bereits installiert haben, überprüfen Sie mit `node -v`, ob Sie die neueste Version verwenden. Es sollte die aktuelle [LTS-Version](https://nodejs.org/en/download/) zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="e76de-p102">If you have NodeJS already installed please check you have the latest version using `node -v`. It should return the current [LTS version](https://nodejs.org/en/download/).</span></span> 
* <span data-ttu-id="e76de-114">Wenn Sie mit einem Mac arbeiten, empfehlen wir [Homebrew](http://brew.sh/) zur Installation und Verwaltung von NodeJS.</span><span class="sxs-lookup"><span data-stu-id="e76de-114">If you are using a Mac, it is recommended you use [homebrew](http://brew.sh/) to install and manage NodeJS.</span></span> 

><span data-ttu-id="e76de-115">**Hinweis:** Die SharePoint-Framework-Buildpipeline unterstützt derzeit nicht die LTS-Version von Node.js.</span><span class="sxs-lookup"><span data-stu-id="e76de-115">**Note:** The SharePoint Framework build pipeline doesn't currently support the LTS version of Node.js.</span></span> <span data-ttu-id="e76de-116">Laden Sie stattdessen die [Node.js-Version 6.11.5](https://nodejs.org/download/release/latest-v6.x/) herunter.</span><span class="sxs-lookup"><span data-stu-id="e76de-116">Instead, download [Node.js version 6.11.5](https://nodejs.org/download/release/latest-v6.x/).</span></span> <span data-ttu-id="e76de-117">So wird npm 3.10.10 installiert.</span><span class="sxs-lookup"><span data-stu-id="e76de-117">This installs npm 3.10.10.</span></span> <span data-ttu-id="e76de-118">Wenn Sie die Version v5.x von npm verwenden, müssen Sie zunächst ein Downgrade auf eine ältere Version von npm durchführen, indem Sie den folgenden Befehl ausführen: `npm install -g npm@3`.</span><span class="sxs-lookup"><span data-stu-id="e76de-118">Note that if you have a v5.x version of npm, you will need to downgrade to an older npm version by using the following command: `npm install -g npm@3`.</span></span>

### <a name="code-editors"></a><span data-ttu-id="e76de-119">Code-Editoren</span><span class="sxs-lookup"><span data-stu-id="e76de-119">Code Editors</span></span>

<span data-ttu-id="e76de-p104">Installieren Sie einen Code-Editor. Sie können einen beliebigen Code-Editor oder eine beliebige IDE verwenden, der bzw. die die clientseitige Entwicklung unterstützt, um Ihren Webpart zu erstellen, z. B.:</span><span class="sxs-lookup"><span data-stu-id="e76de-p104">Install a code editor. You can use any code editor or IDE that supports client-side development to build your web part, such as:</span></span>

* <span data-ttu-id="e76de-122">[Visual Studio Code](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="e76de-122">[Visual Studio Code](https://code.visualstudio.com/)</span></span>
* <span data-ttu-id="e76de-123">[Atom](https://atom.io)</span><span class="sxs-lookup"><span data-stu-id="e76de-123">[Atom](https://atom.io)</span></span>
* <span data-ttu-id="e76de-124">[WebStorm](https://www.jetbrains.com/webstorm)</span><span class="sxs-lookup"><span data-stu-id="e76de-124">[Webstorm](https://www.jetbrains.com/webstorm)</span></span>

<span data-ttu-id="e76de-125">Die Schritte und Beispiele in dieser Dokumentation verwenden [Visual Studio Code](https://code.visualstudio.com/), aber Sie können einen beliebigen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="e76de-125">The steps and examples in this documentation use [Visual Studio Code](https://code.visualstudio.com/), but you can use any editor of your choice.</span></span>

### <a name="if-you-are-using-ubuntu"></a><span data-ttu-id="e76de-126">Wenn Sie Ubuntu verwenden, gilt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="e76de-126">If you are using Ubuntu</span></span>

<span data-ttu-id="e76de-127">Sie müssen mit dem folgenden Befehl Compilertools installieren:</span><span class="sxs-lookup"><span data-stu-id="e76de-127">You need to install compiler tools using the following command:</span></span>

```sh
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a><span data-ttu-id="e76de-128">Wenn Sie Fedora verwenden</span><span class="sxs-lookup"><span data-stu-id="e76de-128">If you are using fedora</span></span>

<span data-ttu-id="e76de-129">Sie müssen mit dem folgenden Befehl Compilertools installieren:</span><span class="sxs-lookup"><span data-stu-id="e76de-129">You need to install compiler tools using the following command:</span></span>

```sh
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a><span data-ttu-id="e76de-130">Installieren von Yeoman und Gulp</span><span class="sxs-lookup"><span data-stu-id="e76de-130">Install Yeoman and gulp</span></span>

<span data-ttu-id="e76de-p105">[Yeoman](http://yeoman.io/) hilft Ihnen bei den ersten Schritten mit neuen Projekten und stellt bewährte Methoden und Tools bereit, mit denen Sie produktiv arbeiten können. Clientseitige SharePoint-Entwicklungstools umfassen einen Yeoman-Generator zum Erstellen neuer Webparts. Der Generator stellt allgemeine Buildtools, häufig verwendeten Boilerplate-Code und eine allgemeine Umgebungswebsite zum Hosten von Webparts für Tests bereit.</span><span class="sxs-lookup"><span data-stu-id="e76de-p105">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive. SharePoint client-side development tools include a Yeoman generator for creating new web parts. The generator provides common build tools, common boilerplate code, and a common playground web site to host web parts for testing.</span></span>

<span data-ttu-id="e76de-134">Geben Sie den folgenden Befehl ein, um Yeoman und Gulp zu installieren:</span><span class="sxs-lookup"><span data-stu-id="e76de-134">Enter the following command to install Yeoman and gulp:</span></span>

```sh
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a><span data-ttu-id="e76de-135">Installieren des Yeoman SharePoint-Generators</span><span class="sxs-lookup"><span data-stu-id="e76de-135">Install Yeoman SharePoint generator</span></span>

<span data-ttu-id="e76de-136">Der Yeoman SharePoint-Webpart-Generator hilft Ihnen beim schnellen Erstellen eines clientseitigen SharePoint-Lösungsprojekts mit den richtigen Tools und der richtigen Projektstruktur.</span><span class="sxs-lookup"><span data-stu-id="e76de-136">The Yeoman SharePoint web part generator helps you quickly create a SharePoint client-side solution project with the right toolchain and project structure.</span></span>

<span data-ttu-id="e76de-137">Geben Sie den folgenden Befehl ein, um den SharePoint-Framework-Yeoman-Generator global zu installieren:</span><span class="sxs-lookup"><span data-stu-id="e76de-137">To install the SharePoint Framework Yeoman generator globally, enter the following command:</span></span>

```sh
npm install -g @microsoft/generator-sharepoint
```

<span data-ttu-id="e76de-138">Wenn Sie zwischen den verschiedenen Projekten mit unterschiedlichen Versionen des SharePoint-Framework-Yeoman-Generators wechseln müssen, können Sie den Generator lokal als eine Entwicklungsabhängigkeit im Projektordner installieren, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="e76de-138">If you need to switch between the different projects created using different versions of the SharePoint Framework Yeoman generator, you can install the generator locally as a development dependency in the project folder by executing the following command:</span></span>

```sh
npm install @microsoft/generator-sharepoint --save-dev
```

## <a name="optional-tools"></a><span data-ttu-id="e76de-139">Optionale Tools</span><span class="sxs-lookup"><span data-stu-id="e76de-139">Optional tools</span></span>

<span data-ttu-id="e76de-140">Hier sind einige Tools, die auch nützlich sein können:</span><span class="sxs-lookup"><span data-stu-id="e76de-140">Here are some tools that might come in handy as well:</span></span>

* <span data-ttu-id="e76de-141">[Fiddler](http://www.telerik.com/fiddler)</span><span class="sxs-lookup"><span data-stu-id="e76de-141">[Fiddler](http://www.telerik.com/fiddler)</span></span>
* <span data-ttu-id="e76de-142">[Postman-Plug-In für Chrome](https://www.getpostman.com/docs/introduction)</span><span class="sxs-lookup"><span data-stu-id="e76de-142">[Postman plugin for Chrome](https://www.getpostman.com/docs/introduction)</span></span>
* <span data-ttu-id="e76de-143">[Cmder für Windows](http://cmder.net/)</span><span class="sxs-lookup"><span data-stu-id="e76de-143">[Cmder for Windows](http://cmder.net/)</span></span>
* <span data-ttu-id="e76de-144">[Oh My Zsh für Mac](http://ohmyz.sh/)</span><span class="sxs-lookup"><span data-stu-id="e76de-144">[Oh My Zsh for Mac](http://ohmyz.sh/)</span></span>
* <span data-ttu-id="e76de-145">[Git Source Control Tools](https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="e76de-145">[Git source control tools](https://git-scm.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e76de-146">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="e76de-146">Next steps</span></span>

<span data-ttu-id="e76de-147">Sie können jetzt [Ihren ersten clientseitigen Webpart erstellen](web-parts/get-started/build-a-hello-world-web-part.md)!</span><span class="sxs-lookup"><span data-stu-id="e76de-147">You are now ready to [build your first client-side web part](web-parts/get-started/build-a-hello-world-web-part.md)!</span></span>

> [!NOTE]
> <span data-ttu-id="e76de-148">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint-Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="e76de-148">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="e76de-149">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="e76de-149">Thanks for your input advance.</span></span>