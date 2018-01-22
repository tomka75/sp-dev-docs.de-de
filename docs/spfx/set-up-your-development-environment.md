---
title: Einrichten Ihrer SharePoint Framework-Entwicklungsumgebung
description: "Verwenden Sie Visual Studio oder Ihre eigene benutzerdefinierte Entwicklungsumgebung, um SharePoint Framework-Lösungen zu erstellen. Sie können einen Mac, PC oder Linux verwenden."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 0c849ef4ad13962ecb4e3cfd8dc34aec0baab523
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="set-up-your-sharepoint-framework-development-environment"></a><span data-ttu-id="9a37c-104">Einrichten Ihrer SharePoint Framework-Entwicklungsumgebung</span><span class="sxs-lookup"><span data-stu-id="9a37c-104">Set up your SharePoint Framework development environment</span></span>

<span data-ttu-id="9a37c-105">Sie können Visual Studio oder Ihre eigene benutzerdefinierte Entwicklungsumgebung verwenden, um SharePoint Framework-Lösungen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="9a37c-105">You can use Visual Studio, or your own custom development environment to build SharePoint Framework solutions. You can use a Mac, PC, or Linux.</span></span> <span data-ttu-id="9a37c-106">Sie können einen Mac, PC oder Linux verwenden.</span><span class="sxs-lookup"><span data-stu-id="9a37c-106">You can use a Mac, PC, or Linux.</span></span>

> [!NOTE] 
> <span data-ttu-id="9a37c-107">Bevor Sie die Schritte in diesem Artikel durchführen, müssen Sie [Ihren Office 365-Mandanten einrichten](./set-up-your-developer-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="9a37c-107">Note: Before following the steps in this article, be sure to [Set up your Office 365 Tenant](./set-up-your-developer-tenant.md).</span></span>

<span data-ttu-id="9a37c-108">Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq) nachvollziehen.</span><span class="sxs-lookup"><span data-stu-id="9a37c-108">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span>

<span data-ttu-id="9a37c-109"><a href="https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a></span><span class="sxs-lookup"><span data-stu-id="9a37c-109"></span></span>

## <a name="install-developer-tools"></a><span data-ttu-id="9a37c-110">Installieren von Entwicklertools</span><span class="sxs-lookup"><span data-stu-id="9a37c-110">Install developer tools</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="9a37c-111">Installieren von NodeJS</span><span class="sxs-lookup"><span data-stu-id="9a37c-111">Install Node.js.</span></span>

<span data-ttu-id="9a37c-112">Installieren Sie die [NodeJS-Version 6.x](https://nodejs.org/download/release/latest-v6.x/).</span><span class="sxs-lookup"><span data-stu-id="9a37c-112">Install [NodeJS version 6.x](https://nodejs.org/download/release/latest-v6.x/).</span></span> 

- <span data-ttu-id="9a37c-113">Wenn Sie Windows verwenden, können Sie die MSI-Installationsprogramme in diesem Link verwenden, um NodeJS auf einfache Weise einzurichten.</span><span class="sxs-lookup"><span data-stu-id="9a37c-113">If you are in Windows, you can use the msi installers in the above link for easiest way to setup NodeJS</span></span>
- <span data-ttu-id="9a37c-114">Wenn Sie NodeJS bereits installiert haben, überprüfen Sie mit `node -v`, ob Sie die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="9a37c-114">If you have NodeJS already installed please check you have the latest version using `node -v`. It should return the current LTS version.</span></span> <span data-ttu-id="9a37c-115">Es sollte die aktuelle [LTS-Version](https://nodejs.org/en/download/) zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="9a37c-115">It should return the current [LTS version](https://nodejs.org/en/download/).</span></span> 
- <span data-ttu-id="9a37c-116">Wenn Sie mit einem Mac arbeiten, empfehlen wir [Homebrew](http://brew.sh/) zur Installation und Verwaltung von NodeJS.</span><span class="sxs-lookup"><span data-stu-id="9a37c-116">If you are using a Mac, it is recommended you use [homebrew](http://brew.sh/) to install and manage NodeJS.</span></span> 

> [!NOTE] 
> <span data-ttu-id="9a37c-117">Die SharePoint-Framework-Buildpipeline unterstützt derzeit nicht die LTS-Version von Node.js.</span><span class="sxs-lookup"><span data-stu-id="9a37c-117">Note: The SharePoint Framework build pipeline doesn't currently support the LTS version of Node.js.</span></span> <span data-ttu-id="9a37c-118">Laden Sie stattdessen die [Node.js-Version 6.11.5](https://nodejs.org/download/release/latest-v6.x/) herunter.</span><span class="sxs-lookup"><span data-stu-id="9a37c-118">Instead, download [Node.js version 6.11.5](https://nodejs.org/download/release/latest-v6.x/).</span></span> <span data-ttu-id="9a37c-119">So wird npm 3.10.10 installiert.</span><span class="sxs-lookup"><span data-stu-id="9a37c-119">This installs npm 3.10.10.</span></span> <span data-ttu-id="9a37c-120">Wenn Sie die Version v5.x von npm verwenden, müssen Sie zunächst ein Downgrade auf eine ältere Version von npm durchführen, indem Sie den folgenden Befehl ausführen: `npm install -g npm@3`.</span><span class="sxs-lookup"><span data-stu-id="9a37c-120">Note that if you have a v5.x version of npm, you will need to downgrade to an older npm version by using the following command: `npm install -g npm@3`.</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="9a37c-121">Installieren eines Code-Editors</span><span class="sxs-lookup"><span data-stu-id="9a37c-121">Install a code editor</span></span>

<span data-ttu-id="9a37c-122">Sie können einen beliebigen Code-Editor oder eine beliebige IDE verwenden, der bzw. die die clientseitige Entwicklung unterstützt, um Ihren Webpart zu erstellen, z. B.:</span><span class="sxs-lookup"><span data-stu-id="9a37c-122">Install a code editor. You can use any code editor or IDE that supports client-side development to build your web part, such as:</span></span>

- [<span data-ttu-id="9a37c-123">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9a37c-123">Visual Studio Code</span></span>](https://code.visualstudio.com/)
- [<span data-ttu-id="9a37c-124">Atom</span><span class="sxs-lookup"><span data-stu-id="9a37c-124">Atom</span></span>](https://atom.io)
- [<span data-ttu-id="9a37c-125">WebStorm</span><span class="sxs-lookup"><span data-stu-id="9a37c-125">Webstorm</span></span>](https://www.jetbrains.com/webstorm)

<span data-ttu-id="9a37c-126">Die Schritte und Beispiele in dieser Dokumentation verwenden [Visual Studio Code](https://code.visualstudio.com/), aber Sie können einen beliebigen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="9a37c-126">The steps and examples in this documentation use [Visual Studio Code](https://code.visualstudio.com/), but you can use any editor of your choice.</span></span>

### <a name="if-you-are-using-ubuntu"></a><span data-ttu-id="9a37c-127">Wenn Sie Ubuntu verwenden, gilt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="9a37c-127">If you are using Ubuntu</span></span>

<span data-ttu-id="9a37c-128">Sie müssen mit dem folgenden Befehl Compilertools installieren:</span><span class="sxs-lookup"><span data-stu-id="9a37c-128">You need to install compiler tools using the following command:</span></span>

```sh
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a><span data-ttu-id="9a37c-129">Wenn Sie Fedora verwenden</span><span class="sxs-lookup"><span data-stu-id="9a37c-129">If you are using fedora</span></span>

<span data-ttu-id="9a37c-130">Sie müssen mit dem folgenden Befehl Compilertools installieren:</span><span class="sxs-lookup"><span data-stu-id="9a37c-130">You need to install compiler tools using the following command:</span></span>

```sh
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a><span data-ttu-id="9a37c-131">Installieren von Yeoman und Gulp</span><span class="sxs-lookup"><span data-stu-id="9a37c-131">Install Yeoman and gulp</span></span>

<span data-ttu-id="9a37c-132">[Yeoman](http://yeoman.io/) hilft Ihnen bei den ersten Schritten mit neuen Projekten und stellt bewährte Methoden und Tools bereit, mit denen Sie produktiv arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="9a37c-132">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive.</span></span> <span data-ttu-id="9a37c-133">Clientseitige SharePoint-Entwicklungstools umfassen einen Yeoman-Generator zum Erstellen neuer Webparts.</span><span class="sxs-lookup"><span data-stu-id="9a37c-133">SharePoint client-side development tools include a Yeoman generator for creating new web parts.</span></span> <span data-ttu-id="9a37c-134">Der Generator stellt allgemeine Buildtools, häufig verwendeten Boilerplate-Code und eine allgemeine Umgebungswebsite zum Hosten von Webparts für Tests bereit.</span><span class="sxs-lookup"><span data-stu-id="9a37c-134">The generator provides common build tools, common boilerplate code, and a common playground website to host web parts for testing.</span></span>

<span data-ttu-id="9a37c-135">Geben Sie den folgenden Befehl ein, um Yeoman und Gulp zu installieren:</span><span class="sxs-lookup"><span data-stu-id="9a37c-135">Enter the following command to install Yeoman and gulp:</span></span>

```sh
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a><span data-ttu-id="9a37c-136">Installieren des Yeoman SharePoint-Generators</span><span class="sxs-lookup"><span data-stu-id="9a37c-136">Install Yeoman SharePoint generator</span></span>

<span data-ttu-id="9a37c-137">Der Yeoman SharePoint-Webpart-Generator hilft Ihnen beim schnellen Erstellen eines clientseitigen SharePoint-Lösungsprojekts mit den richtigen Tools und der richtigen Projektstruktur.</span><span class="sxs-lookup"><span data-stu-id="9a37c-137">The Yeoman SharePoint web part generator helps you quickly create a SharePoint client-side solution project with the right toolchain and project structure.</span></span>

<span data-ttu-id="9a37c-138">Geben Sie den folgenden Befehl ein, um den SharePoint-Framework-Yeoman-Generator global zu installieren:</span><span class="sxs-lookup"><span data-stu-id="9a37c-138">To install the SharePoint Framework Yeoman generator globally, enter the following command:</span></span>

```sh
npm install -g @microsoft/generator-sharepoint
```

<span data-ttu-id="9a37c-139">Wenn Sie zwischen den verschiedenen Projekten mit unterschiedlichen Versionen des SharePoint-Framework-Yeoman-Generators wechseln müssen, können Sie den Generator lokal als eine Entwicklungsabhängigkeit im Projektordner installieren, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="9a37c-139">If you need to switch between the different projects created using different versions of the SharePoint Framework Yeoman generator, you can install the generator locally as a development dependency in the project folder by executing the following command:</span></span>

```sh
npm install @microsoft/generator-sharepoint --save-dev
```

## <a name="optional-tools"></a><span data-ttu-id="9a37c-140">Optionale Tools</span><span class="sxs-lookup"><span data-stu-id="9a37c-140">Optional tools</span></span>

<span data-ttu-id="9a37c-141">Hier sind einige Tools, die auch nützlich sein können:</span><span class="sxs-lookup"><span data-stu-id="9a37c-141">Here are some tools that might come in handy as well:</span></span>

* [<span data-ttu-id="9a37c-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="9a37c-142">Fiddler</span></span>](https://www.telerik.com/fiddler)
* [<span data-ttu-id="9a37c-143">Postman-Plug-In für Chrome</span><span class="sxs-lookup"><span data-stu-id="9a37c-143">Postman plugin for Chrome</span></span>](https://www.getpostman.com/docs/postman/launching_postman/navigating_postman)
* [<span data-ttu-id="9a37c-144">Cmder für Windows</span><span class="sxs-lookup"><span data-stu-id="9a37c-144">Cmder for Windows</span></span>](http://cmder.net/)
* [<span data-ttu-id="9a37c-145">Oh My Zsh für Mac</span><span class="sxs-lookup"><span data-stu-id="9a37c-145">Oh My Zsh for Mac</span></span>](http://ohmyz.sh/)
* [<span data-ttu-id="9a37c-146">Git Source Control Tools</span><span class="sxs-lookup"><span data-stu-id="9a37c-146">Git source control tools</span></span>](https://git-scm.com/)

## <a name="next-steps"></a><span data-ttu-id="9a37c-147">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="9a37c-147">Next steps</span></span>

<span data-ttu-id="9a37c-148">Sie können jetzt [Ihr erstes clientseitiges Webpart erstellen](web-parts/get-started/build-a-hello-world-web-part.md)!</span><span class="sxs-lookup"><span data-stu-id="9a37c-148">You are now ready to [build your first client-side web part](web-parts/get-started/build-a-hello-world-web-part.md)!</span></span>

> [!NOTE]
> <span data-ttu-id="9a37c-149">Wenn Sie einen Fehler in der Dokumentation oder im SharePoint Framework finden, melden Sie ihn an das SharePoint Engineering unter Verwendung der [Fehlerliste im sp-dev-docs-Repository](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="9a37c-149">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="9a37c-150">Vielen Dank im Voraus für Ihr Feedback.</span><span class="sxs-lookup"><span data-stu-id="9a37c-150">Thanks for your input advance.</span></span>