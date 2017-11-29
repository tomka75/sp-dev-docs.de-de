---
title: "Konfigurieren von SharePoint gehostet durch Drittanbieter-Add-ins für die Verteilung"
ms.date: 11/03/2017
ms.openlocfilehash: 82a1c046063dda3a612f96f70e5583d58ca9a505
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="configure-sharepoint-provider-hosted-add-ins-for-distribution"></a><span data-ttu-id="0da56-102">Konfigurieren von SharePoint gehostet durch Drittanbieter-Add-ins für die Verteilung</span><span class="sxs-lookup"><span data-stu-id="0da56-102">Configure SharePoint Provider-Hosted Add-ins for Distribution</span></span>

### <a name="summary"></a><span data-ttu-id="0da56-103">Summary</span><span class="sxs-lookup"><span data-stu-id="0da56-103">Summary</span></span> ###

<span data-ttu-id="0da56-104">Auf dieser Seite erläutert die Probleme, die bei der Freigabe eines SharePoint-Anwendung mit anderen Entwicklern vom Anbieter gehostete oder beim Abrufen einer Kopie aus einem Quellcodeverwaltungssystem wie Team Foundation Server, Git oder Visual Studio Online auftreten können.</span><span class="sxs-lookup"><span data-stu-id="0da56-104">This page explains issues that may arise when sharing a SharePoint Provider-Hosted application with other developers or when obtaining a copy from a source control system such as Team Foundation Server, Git or Visual Studio Online.</span></span>

# <a name="configure-sharepoint-provider-hosted-add-ins-for-distribution"></a><span data-ttu-id="0da56-105">Konfigurieren von SharePoint gehostet durch Drittanbieter-Add-ins für die Verteilung</span><span class="sxs-lookup"><span data-stu-id="0da56-105">Configure SharePoint Provider-Hosted Add-ins for Distribution</span></span>

<span data-ttu-id="0da56-106">Alle SharePoint gehostet durch Drittanbieter-add-ins mit Visual Studio 2013 erstellt enthalten ein NuGet-Paket, das SharePoint-spezifische Code hinzugefügt und verweist auf die Webanwendung, die als das RemoteWeb für die SharePoint-add-in fungiert.</span><span class="sxs-lookup"><span data-stu-id="0da56-106">All SharePoint Provider-Hosted add-ins created using Visual Studio 2013 include a NuGet package that adds SharePoint-specific code and references to the web application that serves as the RemoteWeb for the SharePoint add-in.</span></span> 

<span data-ttu-id="0da56-107">Durch die Office-Entwicklertools in Visual Studio das Webanwendungsprojekt hinzugefügt NuGet-Paket ist nicht in der Registrierung des NuGet-Paket vorhanden, und daher Versuche zum Erstellen einer NuGet-Paket-Wiederherstellung schlägt fehl, da ein passendes Paket gefunden werden kann.</span><span class="sxs-lookup"><span data-stu-id="0da56-107">The NuGet package added to the web application project by the Office Developer Tools in Visual Studio is not present in the NuGet package registry and therefore attempts to perform a NuGet package restore will fail because it cannot find a matching package.</span></span>

## <a name="understanding-the-problem"></a><span data-ttu-id="0da56-108">Beschreibung des Problems</span><span class="sxs-lookup"><span data-stu-id="0da56-108">Understanding the Problem</span></span> ##

<span data-ttu-id="0da56-109">Die im **Office Developer Tools für Visual Studio 2013**Version 12.0.31105, fügt ein NuGet-Paket für Webanwendungen als die RemoteWeb für SharePoint gehostet durch Drittanbieter-add-ins erstellt. Dieses Paket, die **App für SharePoint Web Toolkit**hinzugefügt Webprojekt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="0da56-109">The **Office Developer Tools for Visual Studio 2013**, version 12.0.31105, adds a NuGet package to web applications created as the RemoteWeb for SharePoint Provider-Hosted add-ins. This package, the **App for SharePoint Web Toolkit**, adds the following things to the web project:</span></span>

- <span data-ttu-id="0da56-110">Assemblys & Verweise auf die Assemblys SharePoint Client-Side Object Model (CSOM)</span><span class="sxs-lookup"><span data-stu-id="0da56-110">Assemblies & references to the SharePoint Client-Side Object Model (CSOM) assemblies</span></span>
- <span data-ttu-id="0da56-111">Eine Codedatei `TokenHelper.cs` , die bei der Authentifizierung für add-ins unterstützt.</span><span class="sxs-lookup"><span data-stu-id="0da56-111">A code file `TokenHelper.cs` that assists in the authentication process for add-ins.</span></span>
- <span data-ttu-id="0da56-112">Eine Codedatei `SharePointContext.cs` Ihnen dabei hilft, erstellen und Verwalten von einem SharePoint-Kontext innerhalb der Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="0da56-112">A code file `SharePointContext.cs` that helps in creating and maintaining a SharePoint context within the web application.</span></span>

<span data-ttu-id="0da56-113">Die Arbeitsweise von Visual Studio ist, dass oder Addins, enthalten eine lokale Kopie der NuGet-Paket in der Regel damit Entwickler nicht immer mit dem Internet NuGet-Pakete herunterladen verbunden sein.</span><span class="sxs-lookup"><span data-stu-id="0da56-113">The way Visual Studio works is that it, or addins, typically contain a local copy of the NuGet package so developers do not always have to be connected to the internet to download the NuGet packages.</span></span> <span data-ttu-id="0da56-114">Das Paket, das die Tools enthalten hat eine ID von **AppForSharePoint16WebToolkit**.</span><span class="sxs-lookup"><span data-stu-id="0da56-114">The package that the tools include has an ID of **AppForSharePoint16WebToolkit**.</span></span>

<span data-ttu-id="0da56-115">Wenn Projekte in Datenquellen-Steuerelement übernommen werden, sind in der Regel die Pakete nicht eingeschlossen als Teil des Commit, da sie viel extra Speicher Speicherplatz Bedarfs und unnötig hinzufügen können erhöhen Sie die Größe eines Pakets, wenn es gemeinsam mit anderen Entwicklern.</span><span class="sxs-lookup"><span data-stu-id="0da56-115">When projects are committed to source control, typically the packages are not included as part of the commit because they can add a lot of extra storage space demands and unnecessarily increase the size of a package when sharing it with other developers.</span></span> <span data-ttu-id="0da56-116">Aus diesem Grund einer der ersten Aufgaben Entwickler Schritt nach Abrufen einer Kopie des Projekts aus der quellcodeverwaltung [Wiederherstellen NuGet-Paket](http://docs.nuget.org/docs/reference/package-restore)ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="0da56-116">Therefore one of the first tasks developers do after getting a copy of the project from source control is to run [NuGet package restore](http://docs.nuget.org/docs/reference/package-restore).</span></span>

<span data-ttu-id="0da56-117">Die Herausforderung besteht darin, dass ein Paket mit der gleichen ID nicht in der Registrierung des NuGet-Paket vorhanden ist; Es ist kein Paket mit der ID **AppForSharePoint16WebToolkit**.</span><span class="sxs-lookup"><span data-stu-id="0da56-117">The challenge is that a package with the same ID does not exist in the NuGet package registry; there is no package with an ID of **AppForSharePoint16WebToolkit**.</span></span> <span data-ttu-id="0da56-118">Stattdessen genauen gleiche Paket wurde hinzugefügt, um die Registrierung des NuGet-Paket als **AppForSharePointWebToolkit** ([http://www.nuget.org/packages/AppForSharePointWebToolkit](http://www.nuget.org/packages/AppForSharePointWebToolkit)) ** (*Beachten Sie die mangelnde die 16 im Feld-ID*).</span><span class="sxs-lookup"><span data-stu-id="0da56-118">Instead the exact same package was added to the NuGet package registry as **AppForSharePointWebToolkit** ([http://www.nuget.org/packages/AppForSharePointWebToolkit](http://www.nuget.org/packages/AppForSharePointWebToolkit))** (*notice the lack of the '16' in the ID*).</span></span>

## <a name="preparing-a-sharepoint-provider-hosted-add-in-project-for-source-control--distribution"></a><span data-ttu-id="0da56-119">Vorbereiten eines SharePoint gehostet durch Drittanbieter-Add-in-Projekts zur Quellcodeverwaltung / Verteilung</span><span class="sxs-lookup"><span data-stu-id="0da56-119">Preparing a SharePoint Provider-Hosted Add-in Project for Source Control / Distribution</span></span> ##

<span data-ttu-id="0da56-120">Bis die Office Developer Tools für Visual Studio 2013 aktualisiert werden, um dieses Problem zu beheben, empfiehlt es sich um das Projekt vor dem Ausführen eines Commits zu Ihrem Quellcodeverwaltungssystem, unabhängig davon ändern, wenn mithilfe von Team Foundation Server, Visual Studio Online, Git oder andere Lösung.</span><span class="sxs-lookup"><span data-stu-id="0da56-120">Until the Office Developer Tools for Visual Studio 2013 are updated to fix this issue, it is recommended to alter the project prior to committing to your source control system, regardless if you are using Team Foundation Server, Visual Studio Online, Git or any other solution.</span></span>

<span data-ttu-id="0da56-121">Suchen Sie nach dem Erstellen des Projekts innerhalb des Projekts `packages.config` -Datei, und suchen Sie für ein Paket mit der ID **AppForSharePoint16WebToolkit**.</span><span class="sxs-lookup"><span data-stu-id="0da56-121">After creating the project, look within the project's `packages.config` file and search for a package with an ID of **AppForSharePoint16WebToolkit**.</span></span> <span data-ttu-id="0da56-122">Die sicherste Methode zum Aktualisieren des Projekts ist zum Deinstallieren und Neuinstallieren von des Pakets.</span><span class="sxs-lookup"><span data-stu-id="0da56-122">The safest way to update the project is to uninstall & then reinstall the package.</span></span>

<span data-ttu-id="0da56-123">Öffnen Sie die **Paket-Manager-Konsole** in Visual Studio, und geben Sie Folgendes ein, um das Paket zu deinstallieren:</span><span class="sxs-lookup"><span data-stu-id="0da56-123">Open the **Package Manager Console** in Visual Studio and enter the following to uninstall the package:</span></span>

  ````powershell
  PM> Uninstall-Package -Id AppForSharePoint16WebToolkit
  ````

  > <span data-ttu-id="0da56-124">Wenn die Deinstallation einen Fehler zum Suchen nach nicht das Paket auslöst, entfernen Sie einfach den Paket-Verweis aus der `packages.config` Datei manuell & Ihre Änderungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="0da56-124">If the uninstall throws an error about not finding the package, simply remove the package reference from the `packages.config` file manually & save your changes.</span></span>

<span data-ttu-id="0da56-125">Installieren Sie nun die öffentliche Version der gleichen NuGet-Paket aus der öffentlichen Registrierung:</span><span class="sxs-lookup"><span data-stu-id="0da56-125">Now, install the public version of the same NuGet package from the public registry:</span></span>

  ````powershell
  PM> Install-Package -Id AppForSharePointWebToolkit
  ````

----------

### <a name="related-links"></a><span data-ttu-id="0da56-126">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="0da56-126">Related links</span></span> ###
- [<span data-ttu-id="0da56-127">NuGet: App für SharePoint-Web-Toolkit</span><span class="sxs-lookup"><span data-stu-id="0da56-127">NuGet: App for SharePoint Web Toolkit</span></span>](http://www.nuget.org/packages/AppForSharePointWebToolkit)
- [<span data-ttu-id="0da56-128">NuGet: Paket wiederherstellen</span><span class="sxs-lookup"><span data-stu-id="0da56-128">NuGet: Package Restore</span></span>](http://docs.nuget.org/docs/reference/package-restore)

### <a name="applies-to"></a><span data-ttu-id="0da56-129">Gilt für</span><span class="sxs-lookup"><span data-stu-id="0da56-129">Applies to</span></span> ###
-  <span data-ttu-id="0da56-130">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="0da56-130">Office 365 Multi Tenant (MT)</span></span>
-  <span data-ttu-id="0da56-131">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="0da56-131">Office 365 Dedicated (D)</span></span>
-  <span data-ttu-id="0da56-132">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="0da56-132">SharePoint 2013 on-premises</span></span>

### <a name="author"></a><span data-ttu-id="0da56-133">Autor</span><span class="sxs-lookup"><span data-stu-id="0da56-133">Author</span></span>
<span data-ttu-id="0da56-134">Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)</span><span class="sxs-lookup"><span data-stu-id="0da56-134">Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)</span></span>

### <a name="version-history"></a><span data-ttu-id="0da56-135">Versionsverlauf</span><span class="sxs-lookup"><span data-stu-id="0da56-135">Version history</span></span> ###
<span data-ttu-id="0da56-136">Version</span><span class="sxs-lookup"><span data-stu-id="0da56-136">Version</span></span>  | <span data-ttu-id="0da56-137">Datum</span><span class="sxs-lookup"><span data-stu-id="0da56-137">Date</span></span> | <span data-ttu-id="0da56-138">Kommentare</span><span class="sxs-lookup"><span data-stu-id="0da56-138">Comments</span></span>
---------| -----| --------
<span data-ttu-id="0da56-139">0,1</span><span class="sxs-lookup"><span data-stu-id="0da56-139">0.1</span></span>  | <span data-ttu-id="0da56-140">31 Dezember 2014</span><span class="sxs-lookup"><span data-stu-id="0da56-140">December 31, 2014</span></span> | <span data-ttu-id="0da56-141">Erster Entwurf</span><span class="sxs-lookup"><span data-stu-id="0da56-141">First draft</span></span>
