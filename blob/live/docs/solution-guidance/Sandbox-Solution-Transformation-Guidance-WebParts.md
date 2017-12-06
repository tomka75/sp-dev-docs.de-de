---
title: Sandkasten-Transformation ausgesprochen - Webparts
ms.date: 11/03/2017
ms.openlocfilehash: 3c93765118827db986e0830dba870aee6002eeb1
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="sandbox-solution-transformation-guidance---web-parts"></a><span data-ttu-id="41c21-102">Sandkasten-Transformation ausgesprochen - Webparts</span><span class="sxs-lookup"><span data-stu-id="41c21-102">Sandbox solution transformation guidance - Web Parts</span></span>
<span data-ttu-id="41c21-103">Transformieren oder Konvertieren von codebasierte sandkastenlösungen in der SharePoint-add-in-Objektmodell.</span><span class="sxs-lookup"><span data-stu-id="41c21-103">Transform or convert your code-based sandbox solutions to the SharePoint add-in model.</span></span> <span data-ttu-id="41c21-104">Hier erfahren Sie, über die Optionen und Strategien für die vorhandenen Funktionalität in SharePoint-add-in-Modell oder alternative Lösungen zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="41c21-104">Learn about the options and strategies of converting existing functionality to SharePoint add-in model or alternative solutions.</span></span>

<span data-ttu-id="41c21-105">_**Gilt für:** Add-ins für SharePoint | SharePoint 2013 | SharePoint-2016 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="41c21-105">_**Applies to:** Add-ins for SharePoint | SharePoint 2013 | SharePoint 2016 | SharePoint Online_</span></span>


## <a name="summary"></a><span data-ttu-id="41c21-106">Summary</span><span class="sxs-lookup"><span data-stu-id="41c21-106">Summary</span></span>

<span data-ttu-id="41c21-107">Einer der Gründe, dass viele Entwickler codebasierte sandkastenlösungen genutzt haben ist Wunsch visuelle Webparts nutzen.</span><span class="sxs-lookup"><span data-stu-id="41c21-107">One of the reasons many developers have leveraged code-based sandbox solutions is a desire to utilize visual web parts.</span></span> <span data-ttu-id="41c21-108">Dies bietet eine hervorragende Möglichkeit zum Trennen von Code aus Layout als auch ASP.net-Steuerelemente verwenden.</span><span class="sxs-lookup"><span data-stu-id="41c21-108">This provides a great way to separate code from layout as well as utilize the ASP.net controls.</span></span> <span data-ttu-id="41c21-109">Sie können natürlich auch weiterhin mithilfe visuelle Webparts in einer vom Anbieter gehosteten-add-in über die Client-WebParts.</span><span class="sxs-lookup"><span data-stu-id="41c21-109">You can of course continue to use visual web parts in a provider hosted add-in via client web parts.</span></span> <span data-ttu-id="41c21-110">Dies ist ein hervorragendes Ansatz und bietet einen direkte Migrationspfad für viele Clientanwendungen.</span><span class="sxs-lookup"><span data-stu-id="41c21-110">This is a great approach and provides a direct migration path for many applications.</span></span>

<span data-ttu-id="41c21-111">Eine andere Methode ist das Webpart als Client Side Lösung neu zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="41c21-111">Another method is to re-write the web part as a client side solution.</span></span> <span data-ttu-id="41c21-112">Dies planungslösung Neuentwurf der Lösung, um JavaScript, HTML-Fragmente verwenden und eine oder mehrere Frameworks unterstützen.</span><span class="sxs-lookup"><span data-stu-id="41c21-112">This will involve redesigning the solution to use JavaScript, HTML fragments, and one or more supporting frameworks.</span></span> <span data-ttu-id="41c21-113">Obwohl dies Net neue Arbeit ist, hat sie den Vorteil Einrichten Ihrer Lösung, die einfache Integration in die in Kürze verfügbare SharePoint-Framework.</span><span class="sxs-lookup"><span data-stu-id="41c21-113">While this is net-new work, it has the added benefit of setting up your solution to easily integrate into the upcoming SharePoint Framework.</span></span> <span data-ttu-id="41c21-114">Dies ist eine gute Wahl für einfache Anzeige- oder Daten Eintrag Webparts und Clientanwendungen ganze Seite skalieren kann.</span><span class="sxs-lookup"><span data-stu-id="41c21-114">This is a great choice for simple display or data entry web parts and can scale up to full page client applications.</span></span>


## <a name="options-for-replacing-web-parts"></a><span data-ttu-id="41c21-115">Optionen für den Austausch von Webparts</span><span class="sxs-lookup"><span data-stu-id="41c21-115">Options for replacing Web Parts</span></span>
<span data-ttu-id="41c21-116"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="41c21-116"></span></span>

|<span data-ttu-id="41c21-117">**Ansatz**</span><span class="sxs-lookup"><span data-stu-id="41c21-117">**Approach**</span></span>|<span data-ttu-id="41c21-118">**Weitere Informationen**</span><span class="sxs-lookup"><span data-stu-id="41c21-118">**Additional Information**</span></span>|
|:-----|:-----|
|<span data-ttu-id="41c21-119">Vom Anbieter gehosteten Add-in-Client-Webpart</span><span class="sxs-lookup"><span data-stu-id="41c21-119">Provider Hosted Add-In Client Webpart</span></span>|<ul><li>[<span data-ttu-id="41c21-120">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="41c21-120">Get started creating provider-hosted SharePoint Add-ins</span></span>](https://msdn.microsoft.com/en-us/library/office/fp142381.aspx)</li><li>[<span data-ttu-id="41c21-121">Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="41c21-121">Create add-in parts to install with your SharePoint Add-in</span></span>](https://msdn.microsoft.com/en-us/library/a2664289-6c56-4cb1-987a-22367fad55eb)</li><li>[<span data-ttu-id="41c21-122">Client Webpart-Definitionsschema</span><span class="sxs-lookup"><span data-stu-id="41c21-122">Client Web Part Definition Schema</span></span>](https://msdn.microsoft.com/en-us/library/office/dn481208.aspx)</li><li>[<span data-ttu-id="41c21-123">Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="41c21-123">Set up an on-premises development environment for SharePoint Add-ins</span></span>](https://msdn.microsoft.com/en-us/library/office/fp179923.aspx)</li></ul>|
|<span data-ttu-id="41c21-124">Client-Side-Lösung</span><span class="sxs-lookup"><span data-stu-id="41c21-124">Client Side Solution</span></span>|<ul><li>[<span data-ttu-id="41c21-125">Beispiel für einfache reagieren Formular</span><span class="sxs-lookup"><span data-stu-id="41c21-125">Simple React Form Sample</span></span>](https://github.com/SharePoint/PnP/tree/dev/Samples/SharePoint.React.SupportTicket)</li><li><span data-ttu-id="41c21-126">[Einbetten von Beispiele JavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScript)[*](#actionsupportnote)</span><span class="sxs-lookup"><span data-stu-id="41c21-126">[JavaScript Embedding Samples](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScript) [*](#actionsupportnote)</span></span></li><li>[<span data-ttu-id="41c21-127">Muster und Methoden JS-Core</span><span class="sxs-lookup"><span data-stu-id="41c21-127">Patterns and Practices JS Core</span></span>](https://github.com/SharePoint/PnP-JS-Core/)</li></ul>|


## <a name="design-considerations"></a><span data-ttu-id="41c21-128">Entwurfsaspekte</span><span class="sxs-lookup"><span data-stu-id="41c21-128">Design Considerations</span></span>

### <a name="provider-hosted-add-in"></a><span data-ttu-id="41c21-129">Vom Anbieter gehosteten-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="41c21-129">Provider Hosted Add-In</span></span>

<ul>
<li><span data-ttu-id="41c21-130">Erfordert Hostinginfrastruktur ab</span><span class="sxs-lookup"><span data-stu-id="41c21-130">Requires hosting infrastructure</span></span></li>
<li><span data-ttu-id="41c21-131">Hosting-Infrastruktur muss hoch verfügbar sein.</span><span class="sxs-lookup"><span data-stu-id="41c21-131">Hosting infrastructure must be highly available</span></span></li>
<li><span data-ttu-id="41c21-132">Client-Webpart wird in einem Iframe Beschränken der Kommunikation mit dem Rest der Seite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="41c21-132">Client part is displayed in an iframe limiting communication with the rest of the page</span></span></li>
<li><span data-ttu-id="41c21-133">Remote-APIs entweder über CSOM oder REST muss verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="41c21-133">Must use remote APIs either via CSOM or REST</span></span></li>
</ul>

### <a name="client-side-solution"></a><span data-ttu-id="41c21-134">Client-Side-Lösung</span><span class="sxs-lookup"><span data-stu-id="41c21-134">Client Side Solution</span></span>

<ul>
<li><span data-ttu-id="41c21-135">
<a name="actionsupportnote"></a>Bitte beachten Sie, dass die Möglichkeit zum Einbetten von JavaScript in der vorgeschriebenen Weise (über eine UserCustomAction) derzeit nicht außerhalb der klassische Erfahrung funktioniert.</span><span class="sxs-lookup"><span data-stu-id="41c21-135">
<a name="actionsupportnote"></a> Please note that the ability to embed JavaScript in the prescribed way (through a UserCustomAction) does not work currently outside of the classic experience.</span></span> <span data-ttu-id="41c21-136">In diesen Fällen können Sie die Dateien mit einem Skript-Editor-Webpart Verknüpfung herstellen.</span><span class="sxs-lookup"><span data-stu-id="41c21-136">For these cases you can link to the files using a script editor web part.</span></span></li>
<li><span data-ttu-id="41c21-137">Berechtigungen zu erhöhen, verwenden Sie einen Micro-Dienst stattdessen Add-in-Berechtigungen ist nicht möglich</span><span class="sxs-lookup"><span data-stu-id="41c21-137">Cannot elevate permissions, instead use a micro-service with add-in only permissions</span></span></li>
<li><span data-ttu-id="41c21-138">Abhängig von der Berechtigungen des aktuellen Benutzers</span><span class="sxs-lookup"><span data-stu-id="41c21-138">Limited by permissions of current user</span></span></li>
</ul>


## <a name="removing-your-sandbox-code-from-your-site"></a><span data-ttu-id="41c21-139">Entfernen des Sandkasten-Codes aus Ihrer Website</span><span class="sxs-lookup"><span data-stu-id="41c21-139">Removing your sandbox code from your site</span></span>
<span data-ttu-id="41c21-140"><a name="sectionSection3"></a> Wenn Sie Ihre vorhandenen Sandkasten-Lösung aus Ihrer Websites deaktivieren, alle Elemente oder Dateien, die mithilfe von deklarativer Optionen bereitgestellt werden nicht jedoch entfernt werden, die Features in der Sandkasten-Projektmappe werden automatisch deaktiviert und der Ereignisempfänger werden entfernt.</span><span class="sxs-lookup"><span data-stu-id="41c21-140"><a name="sectionSection3"> </a> When you deactivate your existing sandbox solution from your sites, any assets or files deployed using declarative options will not be removed however, the features in the sandbox solution will automatically be deactivated and the event receiver will be removed.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="41c21-141">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="41c21-141">Additional Resources</span></span>
<span data-ttu-id="41c21-142"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="41c21-142"></span></span>
-  [<span data-ttu-id="41c21-143">Entfernen codebasierte Sandkastenlösungen in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="41c21-143">Removing Code-Based Sandbox Solutions in SharePoint Online</span></span>](http://dev.office.com/blogs/removing-code-based-sandbox-solutions-in-sharepoint-online)
-  [<span data-ttu-id="41c21-144">Hilfestellung zur Transformation von Sandkastenlösungen</span><span class="sxs-lookup"><span data-stu-id="41c21-144">Sandbox solution transformation guidance</span></span>](https://msdn.microsoft.com/en-us/pnp_articles/sandbox-solution-transformation-guidance)
-  [<span data-ttu-id="41c21-145">Entfernen Sie Assemblyverweis aus der Sandkasten-Lösung in Visual Studio erstellten</span><span class="sxs-lookup"><span data-stu-id="41c21-145">Remove assembly reference from your Sandbox solution created in Visual Studio</span></span>](https://support.microsoft.com/en-us/kb/3183084)
-  [<span data-ttu-id="41c21-146">Erstellen von Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="41c21-146">Build add-ins for SharePoint</span></span>](https://msdn.microsoft.com/library/office/fp179930.aspx)
-  [<span data-ttu-id="41c21-147">Office 365-Entwicklung und SharePoint Mustern und Methoden ausgesprochen</span><span class="sxs-lookup"><span data-stu-id="41c21-147">Office 365 development and SharePoint patterns and practices solution guidance</span></span>](https://msdn.microsoft.com/en-us/pnp_articles/office-365-development-patterns-and-practices-solution-guidance)