---
title: Lokalisierung in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 33a39ac3c656c9de086432da14ce6fa6cac34870
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="localization-in-the-sharepoint-add-in-model"></a><span data-ttu-id="5268f-102">Lokalisierung in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="5268f-102">Localization in the SharePoint add-in model</span></span>
===========================================

<a name="summary"></a><span data-ttu-id="5268f-103">Summary</span><span class="sxs-lookup"><span data-stu-id="5268f-103">Summary</span></span>
-------

<span data-ttu-id="5268f-104">Ansatz verwenden Sie zum Implementieren der Lokalisierung für Add-ins unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="5268f-104">The approach you take to implement localization for Add-ins is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="5268f-105">In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario, Lokalisierung für benutzerdefinierte Komponenten wie Webparts, Benutzersteuerelemente und Websteuerelemente mit einer Kombination von Ressourcendateien, verwalteter Code, Eigenschaften und deklarativen Code implementiert wurde.</span><span class="sxs-lookup"><span data-stu-id="5268f-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, localization for custom components such as Web Parts, User Controls, and Web Controls was implemented with a combination of resource files, .Net managed code, properties, and declarative code.</span></span>  <span data-ttu-id="5268f-106">In Features, die über den SharePoint-Lösungen bereitgestellt wurden alle Artefakte gepackt.</span><span class="sxs-lookup"><span data-stu-id="5268f-106">All the artifacts were packaged in features deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="5268f-107">In einem Modell Szenario SharePoint-Add-in verwenden Sie JavaScript oder der Lokalisierung Funktionen der Web-Technologie, wenn, der Sie die Add-ins mit Lokalisierung implementieren erstellen, zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="5268f-107">In an SharePoint Add-in model scenario, you use JavaScript or the localization capabilities associated with the web technology you build your Add-ins with to implement localization.</span></span> <span data-ttu-id="5268f-108">Je nach den lokalisierten Ressource können Sie auch klassische Ressourcendateien verwenden, beispielsweise wenn müssen Sie Lozalize-Elemente mithilfe von featureelementen Framework in der Definition-Add-in-Add-in-Web bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="5268f-108">Depending on the localized resource, you might also use classic resources files, for example when you need to lozalize elements deployed to add-in web using feature framework elements in the add-in definition.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="5268f-109">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="5268f-109">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="5268f-110">In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für die Implementierung der Lokalisierung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="5268f-110">As a rule of a thumb, we would like to provide the following high-level guidelines for implementing localization.</span></span>

- <span data-ttu-id="5268f-111">Sie müssen die entsprechenden Language Packs in Ihre lokale SharePoint- und Office 365-Umgebungen ermöglichen Benutzern das Erstellen von Websites in eine bestimmte Kultur und Sprache installieren.</span><span class="sxs-lookup"><span data-stu-id="5268f-111">You must install the appropriate Language Packs in your SharePoint on-premises and Office 365 environments to enable users to create websites in a specific language and culture.</span></span>
- <span data-ttu-id="5268f-112">Verwenden von JavaScript Lokalisierung in SharePoint-Add-ins implementiert ist auch ein Ansatz, mit denen Sie Inhalte im Skript-Editor-Add-in Webparts lokalisieren können.</span><span class="sxs-lookup"><span data-stu-id="5268f-112">Using JavaScript to implement localization in SharePoint Add-ins is also an approach you may use to localize content in Script Editor Add-in Parts.</span></span> 

<a name="localization-scenarios"></a><span data-ttu-id="5268f-113">Lokalisierung Szenarien</span><span class="sxs-lookup"><span data-stu-id="5268f-113">Localization scenarios</span></span>
----------------------

<span data-ttu-id="5268f-114">Es gibt zwei verschiedene Szenarien, in dem Sie Lokalisierung für ein Add-In implementieren müssen.</span><span class="sxs-lookup"><span data-stu-id="5268f-114">There are two distinct scenarios where you may need to implement localization for an Add-in.</span></span>

- <span data-ttu-id="5268f-115">SharePoint-Hosting-Add-ins</span><span class="sxs-lookup"><span data-stu-id="5268f-115">SharePoint-hosted Add-ins</span></span>
- <span data-ttu-id="5268f-116">Vom Anbieter gehosteten-Add-ins</span><span class="sxs-lookup"><span data-stu-id="5268f-116">Provider-hosted Add-ins</span></span>

<a name="add-in-web-components-or-assets"></a><span data-ttu-id="5268f-117">Add-Ins Web Components oder Objekte</span><span class="sxs-lookup"><span data-stu-id="5268f-117">Add-in web components or assets</span></span>
-------------------------
<span data-ttu-id="5268f-118">In diesem Szenario wird die Lokalisierung auf das Add-in über JavaScript angewendet.</span><span class="sxs-lookup"><span data-stu-id="5268f-118">In this scenario localization is applied to the Add-in via JavaScript.</span></span>

- <span data-ttu-id="5268f-119">SharePoint-Hosting-Add-ins haben keinen Zugriff auf Server-basierte Ressourcendateien in den SharePoint-Servern, aber Sie haben Zugriff auf die Feature-Element Resx-Dateien</span><span class="sxs-lookup"><span data-stu-id="5268f-119">SharePoint-hosted Add-ins do not have access to server-based resource files in the SharePoint servers, but you have access on the feature element resx files</span></span> 
- <span data-ttu-id="5268f-120">Die Vorgehensweise zum Lokalisieren eines SharePoint-Hosting-Add-Ins und ein Office-Add-in sind sehr ähnlich, da beide JavaScript verwenden.</span><span class="sxs-lookup"><span data-stu-id="5268f-120">The approach to localize a SharePoint-hosted Add-in and an Office Add-in are very similar because they both use JavaScript.</span></span>

<span data-ttu-id="5268f-121">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="5268f-121">**When is it a good fit?**</span></span>

<span data-ttu-id="5268f-122">Beim Erstellen eines SharePoint-Hosting-Add-Ins wird mithilfe von JavaScript Ihre optimale Breite, da Sie JavaScript-Lokalisierung implementieren und alle erforderlichen zur Unterstützung der Lokalisierung mit dem SharePoint-Hosting-Add-in JavaScript-Dateien bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="5268f-122">When you are creating a SharePoint-hosted Add-in, using JavaScript is your best fit because you can implement localization with JavaScript and deploy all of the JavaScript files necessary to support localization with the SharePoint-hosted Add-in.</span></span> <span data-ttu-id="5268f-123">Sie können auch diesem Ansatz nutzen, wenn das vom Anbieter gehosteten-add-in auch bestimmte-add-ins Web enthält.</span><span class="sxs-lookup"><span data-stu-id="5268f-123">You can also take advantage of this approach if your provider hosted add-in contains also specific add-in web.</span></span>

<span data-ttu-id="5268f-124">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="5268f-124">**Getting Started**</span></span>

<span data-ttu-id="5268f-125">Szenario 2 in der [Core.JavaScriptCustomization (O365 Plug & Play-Beispiel))](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) wird gezeigt, wie JavaScript verwenden, um den Text in ein Add-in als auch die HTML-Elemente in das Add-in zugeordneten Attribute lokalisieren.</span><span class="sxs-lookup"><span data-stu-id="5268f-125">Scenario 2 in the [Core.JavaScriptCustomization (O365 PnP Sample))](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) demonstrates how to use JavaScript to localize the text in an Add-in as well as attributes associated with the HTML elements in the Add-in.</span></span>

<span data-ttu-id="5268f-126">Die [Lokalisieren von SharePoint-Add-ins](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx) wird veranschaulicht, wie JavaScript für die Lokalisierung von Ressourcen im Web-Add-in verwenden.</span><span class="sxs-lookup"><span data-stu-id="5268f-126">The [Localize SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx) also demonstrates how to use JavaScript to localize assets in the add-in web.</span></span>

<a name="remote-components"></a><span data-ttu-id="5268f-127">Remotekomponenten</span><span class="sxs-lookup"><span data-stu-id="5268f-127">Remote components</span></span>
-------------------------
<span data-ttu-id="5268f-128">In diesem Szenario gilt Lokalisierung für das Add-in über die Lokalisierung Technologien mit der Web-Technologie hosten das Add-in verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="5268f-128">In this scenario localization is applied to the Add-in via the localization technologies associated with the web technology hosting the Add-in.</span></span>

- <span data-ttu-id="5268f-129">Wenn ASP.NET verwendet wird, um das Add-in zu implementieren, werden Ressourcendateien und JavaScript-Dateien für die Lokalisierung von es verwendet.</span><span class="sxs-lookup"><span data-stu-id="5268f-129">When ASP.NET is used to implement the Add-in, resource files and JavaScript files are used to localize it.</span></span>
- <span data-ttu-id="5268f-130">Wenn eine andere Technologie wie PHP, Python oder Ruby werden verwendet, um das Add-in zu implementieren die Lokalisierung-Funktionen, die diesen Plattformen zugeordnet verwendet.</span><span class="sxs-lookup"><span data-stu-id="5268f-130">When another technology such as PHP, Python, or Ruby are used to implement the Add-in the localization capabilities associated with those platforms is used.</span></span>

<span data-ttu-id="5268f-131">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="5268f-131">**When is it a good fit?**</span></span>

<span data-ttu-id="5268f-132">Wenn Sie ein vom Anbieter gehosteten-Add-in erstellen, ist mithilfe der Lokalisierung-Technologie, die mit dem Web Hostingplattform kommt die am besten passt, da Sie das Add-in auf eine Weise erstellen, die kein benutzerdefinierten Code oder zusätzliche Komplexität einleitet.</span><span class="sxs-lookup"><span data-stu-id="5268f-132">When you are creating a Provider-hosted Add-in, using the localization technology that comes with the web hosting platform is the best fit because you are building the Add-in in a way that does not introduce custom code or additional complexity.</span></span>

<span data-ttu-id="5268f-133">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="5268f-133">**Getting Started**</span></span>

<span data-ttu-id="5268f-134">In den folgenden Artikeln wird beschrieben, wie vom Anbieter gehosteten-Add-ins mit Ressourcendateien und JavaScript lokalisieren.</span><span class="sxs-lookup"><span data-stu-id="5268f-134">The following articles describes how to localize Provider-hosted Add-ins with resource files and JavaScript.</span></span>

- <span data-ttu-id="5268f-135">[Lokalisieren von SharePoint-Add-ins (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)</span><span class="sxs-lookup"><span data-stu-id="5268f-135">[Localize SharePoint Add-ins (MSDN Article)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)</span></span>
- [<span data-ttu-id="5268f-136">Lokalisieren Sie die Add-ins Web, Hostwebsite und Remotekomponenten ein Add-in (MSDN Code Sample)</span><span class="sxs-lookup"><span data-stu-id="5268f-136">Localize the add-in web, host web, and remote components of an add-in  (MSDN Code Sample)</span></span>](https://code.msdn.microsoft.com/office/SharePoint-2013-Bookstore-328060fc)

<a name="related-links"></a><span data-ttu-id="5268f-137">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="5268f-137">Related links</span></span>
=============

- <span data-ttu-id="5268f-138">[Lokalisieren von SharePoint-Add-ins (MSDN-Artikel)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)</span><span class="sxs-lookup"><span data-stu-id="5268f-138">[Localize SharePoint Add-ins (MSDN Article)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)</span></span>
- [<span data-ttu-id="5268f-139">Lokalisieren Sie die Web-Add-in, Host-Web und Remotekomponenten ein Add-in (Office Dev GitHub-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="5268f-139">Localize the add-in web, host web, and remote components of an add-in  (Office Dev GitHub sample)</span></span>](https://github.com/SharePoint/SharePoint-Add-in-Localization)
- <span data-ttu-id="5268f-140">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="5268f-140">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="5268f-141">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="5268f-141">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="5268f-142">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="5268f-142">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="5268f-143">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="5268f-143">Related PnP samples</span></span>
===================

- [<span data-ttu-id="5268f-144">VariationsExtensions.cs-Klasse (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="5268f-144">VariationsExtensions.cs class (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core/AppModelExtensions/VariationExtensions.cs)
- <span data-ttu-id="5268f-145">Beispiele und Inhalte am [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="5268f-145">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="5268f-146">Gilt für</span><span class="sxs-lookup"><span data-stu-id="5268f-146">Applies to</span></span>
==========
- <span data-ttu-id="5268f-147">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="5268f-147">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="5268f-148">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="5268f-148">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="5268f-149">SharePoint 2013 lokal</span><span class="sxs-lookup"><span data-stu-id="5268f-149">SharePoint 2013 on-premises</span></span>
