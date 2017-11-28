---
title: JavaScript-Muster und Leistung
ms.date: 11/03/2017
ms.openlocfilehash: d9f125657f65da7da770e36e7c1c314759a05c29
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="javascript-patterns-and-performance"></a><span data-ttu-id="8bc06-102">JavaScript-Muster und Leistung</span><span class="sxs-lookup"><span data-stu-id="8bc06-102">JavaScript Patterns and Performance</span></span>

<span data-ttu-id="8bc06-103">Vor Jahren ASP.NET erhielten wir die serverseitige UI-Steuerelement rendern, und es wurde eine gute.</span><span class="sxs-lookup"><span data-stu-id="8bc06-103">Years ago, ASP.NET gave us server-side UI control rendering, and it was good.</span></span> <span data-ttu-id="8bc06-104">Diese serverseitige rendern, erfordert jedoch voll vertrauenswürdiger Code.</span><span class="sxs-lookup"><span data-stu-id="8bc06-104">That server-side rendering, however, requires full-trust code.</span></span> <span data-ttu-id="8bc06-105">Nun, da wir auf SharePoint und Office 365 gewechselt haben, ist voll vertrauenswürdiger Code nicht mehr eine Option.</span><span class="sxs-lookup"><span data-stu-id="8bc06-105">Now that we have transitioned to SharePoint and Office 365, full-trust code is no longer an option.</span></span> <span data-ttu-id="8bc06-106">Dies bedeutet, dass mehr nicht serverseitige Benutzeroberfläche Steuerelementwiedergabe für uns funktionieren.</span><span class="sxs-lookup"><span data-stu-id="8bc06-106">That means server-side UI control rendering won't work for us any more.</span></span>

<span data-ttu-id="8bc06-107">Noch, benötigen Unternehmen noch benutzerdefinierten UI-Funktionalität für ihre Websites und apps.</span><span class="sxs-lookup"><span data-stu-id="8bc06-107">Yet, businesses still need custom UI functionality for their websites and apps.</span></span> <span data-ttu-id="8bc06-108">Dies bedeutet, dass benutzerdefinierte Funktionen der Benutzeroberfläche von der Serverseite in die clientseitige verschoben werden muss.</span><span class="sxs-lookup"><span data-stu-id="8bc06-108">That means custom UI functionality must be moved from the server-side to the client-side.</span></span> 

<span data-ttu-id="8bc06-109">Clientseitige JavaScript ist nun die bessere Wahl für das Rendern der UI-Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="8bc06-109">Client-side JavaScript is now the way to go for UI control rendering.</span></span>

## <span data-ttu-id="8bc06-110"><a name="JavaScriptPatterns"></a>JavaScript-Muster</span><span class="sxs-lookup"><span data-stu-id="8bc06-110"><a name="JavaScriptPatterns"></a> JavaScript Patterns</span></span>

<span data-ttu-id="8bc06-111">Da clientseitige JavaScript der Pfad ist, was die besten Möglichkeiten zum Implementieren des clientseitigen JavaScript sind?</span><span class="sxs-lookup"><span data-stu-id="8bc06-111">Since client-side JavaScript is the path, what are the best ways to implement client-side JavaScript?</span></span> <span data-ttu-id="8bc06-112">Wie Einstieg eine?</span><span class="sxs-lookup"><span data-stu-id="8bc06-112">How does one get started?</span></span>

<span data-ttu-id="8bc06-113">Es gibt mehrere Optionen aus:</span><span class="sxs-lookup"><span data-stu-id="8bc06-113">There are several options:</span></span>

|<span data-ttu-id="8bc06-114">Option</span><span class="sxs-lookup"><span data-stu-id="8bc06-114">Option</span></span>|<span data-ttu-id="8bc06-115">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8bc06-115">Description</span></span>|
|:---|:---|
|<span data-ttu-id="8bc06-116">Einbetten von JavaScript</span><span class="sxs-lookup"><span data-stu-id="8bc06-116">JavaScript Embedding</span></span> | <span data-ttu-id="8bc06-117">[Site.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.site.usercustomactions.aspx) oder [Web.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.web.usercustomactions.aspx) für die Aufnahme Skript direkt in das Seitenmarkup zu erlauben.</span><span class="sxs-lookup"><span data-stu-id="8bc06-117">[Site.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.site.usercustomactions.aspx) or [Web.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.web.usercustomactions.aspx) allow for the inclusion of script directly into the page markup.</span></span> <span data-ttu-id="8bc06-118">Dies wird in dem [Startladeprogramm Muster](#LoaderPattern) erläutert verwendet.</span><span class="sxs-lookup"><span data-stu-id="8bc06-118">This is used in the [Loader Pattern](#LoaderPattern) discussed below</span></span>|
|<span data-ttu-id="8bc06-119">Anzeigevorlagen</span><span class="sxs-lookup"><span data-stu-id="8bc06-119">Display Templates</span></span> | <span data-ttu-id="8bc06-120">Gilt für Ansichten und Suche.</span><span class="sxs-lookup"><span data-stu-id="8bc06-120">Applies to Views and Search.</span></span> <span data-ttu-id="8bc06-121">Sie müssen keine Art von einer app oder Anbieter bereitstellen Code gehostet.</span><span class="sxs-lookup"><span data-stu-id="8bc06-121">You don't have to deploy any kind of an app or provider hosted code.</span></span> <span data-ttu-id="8bc06-122">Es ist einfach eine JavaScript-Datei, die in der Formatbibliothek (z. b) zum Anpassen von Ansichten hochgeladen werden kann.</span><span class="sxs-lookup"><span data-stu-id="8bc06-122">It's simply a JavaScript file that can be uploaded to (for example) the style library to customize views.</span></span> <span data-ttu-id="8bc06-123">Sie können eine beliebige Ansicht mithilfe von JavaScript erforderlich erstellen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-123">You can create any view required by using JavaScript</span></span>|
|<span data-ttu-id="8bc06-124">Gehostete SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8bc06-124">SharePoint Hosted Add-Ins</span></span> | <span data-ttu-id="8bc06-125">Verwendet JSOM für die Kommunikation mit der Hostwebsite oder über das Web-Add-in.</span><span class="sxs-lookup"><span data-stu-id="8bc06-125">Uses JSOM to communicate back to the host web or the add-in web.</span></span> <span data-ttu-id="8bc06-126">Es ermöglicht den Zugriff auf den Webproxy für cross-Domain-Aufrufe</span><span class="sxs-lookup"><span data-stu-id="8bc06-126">It gives access to the Web Proxy for cross domain calls</span></span>|
|<span data-ttu-id="8bc06-127">Vom Anbieter gehosteten-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="8bc06-127">Provider Hosted Add-Ins</span></span> | <span data-ttu-id="8bc06-128">Ermöglicht die Erstellung von komplexen Anwendungen für eine Vielzahl von Technologie-Stapel - Beibehaltung sichere Integration in SharePoint</span><span class="sxs-lookup"><span data-stu-id="8bc06-128">Enables the creation of complex applications across a variety of technology stacks - while maintaining secure integration with SharePoint</span></span>|
|<span data-ttu-id="8bc06-129">JSLink</span><span class="sxs-lookup"><span data-stu-id="8bc06-129">JSLink</span></span> | <span data-ttu-id="8bc06-130">Ermöglicht es Ihnen, laden eine oder mehrere JavaScript-Dateien in vielen OOTB-Webparts und Ansichten</span><span class="sxs-lookup"><span data-stu-id="8bc06-130">Allows you to load one or more JavaScript files in many OOTB web parts and views</span></span>|
|<span data-ttu-id="8bc06-131">ScriptEditor-Webpart</span><span class="sxs-lookup"><span data-stu-id="8bc06-131">ScriptEditor Webpart</span></span> | <span data-ttu-id="8bc06-132">Fügen Sie das Skript direkt oder über Script-Tags durch Markup zum Erstellen komplexer einseitige Applications vollständig in die SharePoint-Website gehostet geladen</span><span class="sxs-lookup"><span data-stu-id="8bc06-132">Include script directly or loaded through script tags with markup to create complex single page applications hosted entirely within the SharePoint site</span></span>|

<span data-ttu-id="8bc06-133">Sind nicht der Meinung, dass Sie in diese Auswahlmöglichkeiten gesperrt sind, wenn Sie glauben, dass eine andere Option für Ihre Situation besser wäre.</span><span class="sxs-lookup"><span data-stu-id="8bc06-133">Don't think you are locked into these choices if you feel a different option would be better for your situation.</span></span> 

## <span data-ttu-id="8bc06-134"><a name="JavaScriptPerformance"></a>JavaScript-Leistung</span><span class="sxs-lookup"><span data-stu-id="8bc06-134"><a name="JavaScriptPerformance"></a> JavaScript Performance</span></span>

<span data-ttu-id="8bc06-135">In jedem Schritt des Entwicklungsprozesses ist es wichtig, Leistung im Hinterkopf behalten.</span><span class="sxs-lookup"><span data-stu-id="8bc06-135">At each step of the development process, it's important to keep performance in mind.</span></span> <span data-ttu-id="8bc06-136">Hier sind einige Punkte, die einen großen Unterschied in JavaScript Leistung vornehmen:</span><span class="sxs-lookup"><span data-stu-id="8bc06-136">Here are a few things that make a big difference in JavaScript performance:</span></span>

|<span data-ttu-id="8bc06-137">Option</span><span class="sxs-lookup"><span data-stu-id="8bc06-137">Option</span></span>|<span data-ttu-id="8bc06-138">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8bc06-138">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="8bc06-139">Reduzieren Sie die Anzahl von Anforderungen</span><span class="sxs-lookup"><span data-stu-id="8bc06-139">Reduce the number of requests</span></span>](#ReduceTheNumberOfRequests) | <span data-ttu-id="8bc06-140">Weniger Anfragen bedeutet weniger Roundtrips zum Server reduziert die Latenz.</span><span class="sxs-lookup"><span data-stu-id="8bc06-140">Fewer requests means fewer round-trips to the server, reducing latency.</span></span>|
|[<span data-ttu-id="8bc06-141">Rufen Sie nur die benötigten Daten ab</span><span class="sxs-lookup"><span data-stu-id="8bc06-141">Retrieve only the data you need</span></span>](#RetrieveOnlyTheDataYouNeed) | <span data-ttu-id="8bc06-142">Reduzieren Sie die Menge der Daten, die über das Netzwerk gesendet.</span><span class="sxs-lookup"><span data-stu-id="8bc06-142">Reduce the amount of data sent over the wire.</span></span> <span data-ttu-id="8bc06-143">Außerdem wird die Serverlast reduziert.</span><span class="sxs-lookup"><span data-stu-id="8bc06-143">Also reduces server load.</span></span>|
|[<span data-ttu-id="8bc06-144">Eine gute Seite Load-Erfahrung bereitstellen</span><span class="sxs-lookup"><span data-stu-id="8bc06-144">Provide a good page load experience</span></span>](#ProvideAGoodUserExperience) | <span data-ttu-id="8bc06-145">Behalten Sie die Benutzeroberfläche für den Benutzer schnell.</span><span class="sxs-lookup"><span data-stu-id="8bc06-145">Keep your UI responsive to the user.</span></span> <span data-ttu-id="8bc06-146">Zum Beispiel aktualisiert die Menüs auf der Seite *vor dem* starten Sie des Herunterladens von 100 Einträge.</span><span class="sxs-lookup"><span data-stu-id="8bc06-146">For example, update the menus on the page *before* you start the download of 100+ records.</span></span>|
|[<span data-ttu-id="8bc06-147">Verwenden Sie asynchrone Aufrufe und Muster nach Möglichkeit</span><span class="sxs-lookup"><span data-stu-id="8bc06-147">Use asynchronous calls and patterns whenever possible</span></span>](#EverythingIsAsynchronous) | <span data-ttu-id="8bc06-148">Abruf ist eine schwerer Belastung auf die Leistung als die Verwendung eines asynchronen Aufrufs oder Rückruf.</span><span class="sxs-lookup"><span data-stu-id="8bc06-148">Polling is a heavier burden on performance than using an asynchronous call or callback.</span></span>| 
|[<span data-ttu-id="8bc06-149">Das Zwischenspeichern der ist Schlüssel</span><span class="sxs-lookup"><span data-stu-id="8bc06-149">Caching is key</span></span>](#ClientSideCaching) | <span data-ttu-id="8bc06-150">Zwischenspeichern verringert die Belastung der Server weiter und sofortige Leistungssteigerung.</span><span class="sxs-lookup"><span data-stu-id="8bc06-150">Caching further reduces the burden on the server while giving immediate performance improvement.</span></span>|
|[<span data-ttu-id="8bc06-151">Vorbereiten Sie für weitere Ansichten von Seiten als jemals gedacht.</span><span class="sxs-lookup"><span data-stu-id="8bc06-151">Prepare for more page views than you ever imagined</span></span>](#PriceOfPopularity) | <span data-ttu-id="8bc06-152">Eine Daten fett Angebotsseite ist Ordnung, wenn Sie nur ein paar Treffer verfügen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-152">A data-heavy landing page is okay when you only have a few hits.</span></span> <span data-ttu-id="8bc06-153">Aber wenn Sie Tausende von aufrufen möchten, können, die wirklich Leistung beeinflussen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-153">But if you get thousands of hits, that can really impact performance.</span></span>|

## <span data-ttu-id="8bc06-154"><a name="WhatIsMyCodeDoing"></a>Was ist mein Code tun</span><span class="sxs-lookup"><span data-stu-id="8bc06-154"><a name="WhatIsMyCodeDoing"></a> What is my code doing</span></span>

<span data-ttu-id="8bc06-155">Aus Leistungsgründen ist es wichtig, wissen ausgeführten Code zu einem beliebigen Zeitpunkt.</span><span class="sxs-lookup"><span data-stu-id="8bc06-155">For performance, it's important to know what your code is doing at any point.</span></span> <span data-ttu-id="8bc06-156">Auf diese Weise können Sie die Möglichkeiten zur Verbesserung der Effizienz zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="8bc06-156">This lets you identify ways to improve efficiency.</span></span> <span data-ttu-id="8bc06-157">Im folgenden sind einige Methoden genau das, was ein.</span><span class="sxs-lookup"><span data-stu-id="8bc06-157">Below are a few good ways to do just that.</span></span>

### <span data-ttu-id="8bc06-158"><a name="ReduceTheNumberOfRequests"></a>Reduzieren Sie die Anzahl von Anforderungen</span><span class="sxs-lookup"><span data-stu-id="8bc06-158"><a name="ReduceTheNumberOfRequests"></a> Reduce the number of requests</span></span>

<span data-ttu-id="8bc06-159">Stellen Sie die wenigsten und kleinsten Anfragen immer möglich.</span><span class="sxs-lookup"><span data-stu-id="8bc06-159">Always make the fewest and smallest requests possible.</span></span> <span data-ttu-id="8bc06-160">Jeder Anforderung, den Sie ausschließen reduziert die Leistung Last auf dem Server und auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="8bc06-160">Each request you eliminate reduces the performance burden on the server and on the client.</span></span> <span data-ttu-id="8bc06-161">Und die Belastung der Leistung durch Ausführen einer kleineren Anforderung weiter reduziert.</span><span class="sxs-lookup"><span data-stu-id="8bc06-161">And making smaller requests further reduces the performance burden.</span></span>

<span data-ttu-id="8bc06-162">Es gibt verschiedene Möglichkeiten, Anfragen und reduziert Anforderungsgröße.</span><span class="sxs-lookup"><span data-stu-id="8bc06-162">There are several ways to reduce requests and reduce request size.</span></span>

- <span data-ttu-id="8bc06-163">Die Anzahl der JavaScript-Dateien in der Produktion.</span><span class="sxs-lookup"><span data-stu-id="8bc06-163">Limit the number of JavaScript files in production.</span></span> <span data-ttu-id="8bc06-164">Trennen die JavaScript-Dateien funktioniert auch für die Entwicklung, jedoch nicht so gut für die Produktion.</span><span class="sxs-lookup"><span data-stu-id="8bc06-164">Separating your JavaScript files works well for development, but not so well for production.</span></span> <span data-ttu-id="8bc06-165">Kombinieren von JavaScript-Dateien in einer einzigen JavaScript-Datei oder als wenige JavaScript-Dateien wie möglich.</span><span class="sxs-lookup"><span data-stu-id="8bc06-165">Combine your JavaScript files into a single JavaScript file, or as few JavaScript files as you can.</span></span>
- <span data-ttu-id="8bc06-166">Dateigrößen zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="8bc06-166">Shrink file sizes.</span></span> <span data-ttu-id="8bc06-167">Minimieren Sie die Produktion JavaScript-Dateien durch Zeilenumbrüche, Leerzeichen und Kommentare entfernen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-167">Minimize your production JavaScript files by removing line breaks, white space, and comments.</span></span> <span data-ttu-id="8bc06-168">Es gibt verschiedene JavaScript minify Programme und Websites, die Sie verwenden können, um Ihre JavaScript Dateigrößen erheblich verringert.</span><span class="sxs-lookup"><span data-stu-id="8bc06-168">There are several JavaScript minify programs and websites that you can use to greatly reduce your JavaScript file sizes.</span></span>
- <span data-ttu-id="8bc06-169">Verwenden Sie die Browser Zwischenspeichern von Dateien, um Anfragen zu verringern.</span><span class="sxs-lookup"><span data-stu-id="8bc06-169">Use browser file caching to reduce requests.</span></span> <span data-ttu-id="8bc06-170">Die aktualisierte [Ladeprogramm Muster](#LoaderPattern) unten ist eine gute Möglichkeit, diese Idee erweitern.</span><span class="sxs-lookup"><span data-stu-id="8bc06-170">The updated [Loader Pattern](#LoaderPattern) below is a good way to expand upon this idea.</span></span>

### <span data-ttu-id="8bc06-171">< einen Namen "RetrieveOnlyTheDataYouNeed" ></a> nur die benötigten Daten abrufen</span><span class="sxs-lookup"><span data-stu-id="8bc06-171"><a name"RetrieveOnlyTheDataYouNeed"></a> Retrieve only the data you need</span></span>

<span data-ttu-id="8bc06-172">Wenn Sie Daten anfordern, denken Sie daran, konzentrieren Sie sich Ihre Anforderungen an, was Sie tatsächlich benötigen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-172">When requesting data, remember to focus your requests to what you actually need.</span></span> <span data-ttu-id="8bc06-173">Download einen gesamten Artikel zum Abrufen des Titels, beispielsweise verringert Leistung erheblich.</span><span class="sxs-lookup"><span data-stu-id="8bc06-173">Downloading an entire article to obtain the title, for example, will reduce performance quite a bit.</span></span>

- <span data-ttu-id="8bc06-174">Verwenden Sie Server zu filtern, wählen und Grenzwerte Datenverkehr über das Netzwerk zu minimieren.</span><span class="sxs-lookup"><span data-stu-id="8bc06-174">Use server filtering, select, and limits to minimize traffic over the wire.</span></span>
- <span data-ttu-id="8bc06-175">Anzufordern Sie nicht alle Artikel, wenn Sie nur die ersten fünf als weiteres Beispiel möchten.</span><span class="sxs-lookup"><span data-stu-id="8bc06-175">Don't request all articles when you want only the first five, as another example.</span></span>
- <span data-ttu-id="8bc06-176">Stellen Sie nicht für die gesamte Eigenschaftenbehälter, wenn Sie nur eine Eigenschaft möchten.</span><span class="sxs-lookup"><span data-stu-id="8bc06-176">Don't ask for the entire property bag if you want only one property.</span></span> <span data-ttu-id="8bc06-177">Ein Beispiel ein Skripts benötigt nur eine Eigenschaft, aber angefordert gesamte Eigenschaftensammlung der herausstellte 800 KB sein.</span><span class="sxs-lookup"><span data-stu-id="8bc06-177">In one example, a script needed only one property, but requested the entire property bag, which turned out to be 800 KB.</span></span> <span data-ttu-id="8bc06-178">Beachten Sie außerdem, dass die Größe eines Objekts kann jetzt Neuigkeiten nur ein paar Kilobyte Megabyte weiter unten in den Produktlebenszyklus werden im Laufe der Zeit ändern kann.</span><span class="sxs-lookup"><span data-stu-id="8bc06-178">Also remember that the size of an object can change over time, so what is only a few kilobytes now can become megabytes in size later in the product lifecycle.</span></span> 

### <span data-ttu-id="8bc06-179"><a name="DontRequestDataYouWillDiscard"></a>Keine Daten anfordern, dass Sie nicht verwendete verwerfen werden</span><span class="sxs-lookup"><span data-stu-id="8bc06-179"><a name="DontRequestDataYouWillDiscard"></a> Don't request data that you will discard unused</span></span>

<span data-ttu-id="8bc06-180">Wenn Sie mehr Daten abrufen, als Sie tatsächlich verwenden, betrachten Sie es als eine Möglichkeit zum verbessern die ursprüngliche Abfrage filtern.</span><span class="sxs-lookup"><span data-stu-id="8bc06-180">If you retrieve more data than you actually use, think of it as an opportunity to better filter your initial query.</span></span> 

- <span data-ttu-id="8bc06-181">Fordern Sie nur die Felder, die Sie benötigen, wie Namen und die Adresse, die nicht den gesamten Datensatz.</span><span class="sxs-lookup"><span data-stu-id="8bc06-181">Request only the fields you need, like Name and Address, not the entire record.</span></span>
- <span data-ttu-id="8bc06-182">Stellen Sie bestimmte, absichtliche Filter Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-182">Make specific, deliberate filter requests.</span></span> <span data-ttu-id="8bc06-183">Beispielsweise, wenn Sie die verfügbaren Artikel auflisten möchten, rufen Sie den Titel, PublishingDate und Autor.</span><span class="sxs-lookup"><span data-stu-id="8bc06-183">For example, if you want to list the available articles, get the Title, PublishingDate, and Author.</span></span> <span data-ttu-id="8bc06-184">Lassen Sie die restlichen Felder aus der Anforderung.</span><span class="sxs-lookup"><span data-stu-id="8bc06-184">Leave the rest of the fields out of the request.</span></span>

### <span data-ttu-id="8bc06-185"><a name="ProvideAGoodUserExperience"></a>Geben Sie eine gute benutzererfahrung</span><span class="sxs-lookup"><span data-stu-id="8bc06-185"><a name="ProvideAGoodUserExperience"></a> Provide a good user experience</span></span>

<span data-ttu-id="8bc06-186">Darstellung, inkonsistente Benutzeroberflächen beeinträchtigen nicht nur Leistung, sondern auch wahrgenommenen Leistung.</span><span class="sxs-lookup"><span data-stu-id="8bc06-186">Jerky, inconsistent user interfaces impact not just performance, but also perceived performance.</span></span> <span data-ttu-id="8bc06-187">Schreiben von Code in so, dass eine reibungslose Umgebung zu schaffen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-187">Write your code in such a way as to give a smooth experience.</span></span>

- <span data-ttu-id="8bc06-188">Verwenden Sie ein Drehfeld, um anzugeben, dass Dinge laden oder Zeit.</span><span class="sxs-lookup"><span data-stu-id="8bc06-188">Use a spinner to indicate that things are loading or taking time.</span></span>
- <span data-ttu-id="8bc06-189">Die Reihenfolge der Ausführung für den Code verstehen, und es für die beste benutzerumgebung Form.</span><span class="sxs-lookup"><span data-stu-id="8bc06-189">Understand the order of execution for your code, and shape it for the best user experience.</span></span> <span data-ttu-id="8bc06-190">Angenommen, wenn große Datenmengen vom Server abgerufen werden soll, und Sie die Benutzeroberfläche durch ein Menü Ausblenden von ändern möchten, blenden Sie aus, klicken Sie im Menü zuerst.</span><span class="sxs-lookup"><span data-stu-id="8bc06-190">For example, if you plan to retrieve a lot of data from the server, and you plan to change the user interface by hiding a menu, hide the menu first.</span></span> <span data-ttu-id="8bc06-191">Verhindert, die eine versetzte UI-Erfahrung für den Benutzer ein.</span><span class="sxs-lookup"><span data-stu-id="8bc06-191">That will prevent a staggered UI experience for the user.</span></span>

## <span data-ttu-id="8bc06-192"><a name="EverythingIsAsynchronous"></a>Alles wird asynchron</span><span class="sxs-lookup"><span data-stu-id="8bc06-192"><a name="EverythingIsAsynchronous"></a> Everything is Asynchronous</span></span>

<span data-ttu-id="8bc06-193">Jede Codeaktivität im Browser sollte asynchronen betrachtet werden.</span><span class="sxs-lookup"><span data-stu-id="8bc06-193">Every code activity in the browser should be considered asynchronous.</span></span> <span data-ttu-id="8bc06-194">Laden Ihre Dateien in einer Reihenfolge, müssen Sie warten, bis das DOM geladen und Ihre Anfragen an SharePoint werden mit verschiedenen Geschwindigkeit abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-194">Your files load in some order, you must wait for the DOM to load, and your requests back to SharePoint will complete at different speeds.</span></span> 

- <span data-ttu-id="8bc06-195">Verstehen der Funktionsweise des Codes in der Zeit.</span><span class="sxs-lookup"><span data-stu-id="8bc06-195">Understand how your code operates in time.</span></span>
- <span data-ttu-id="8bc06-196">Verwenden von Ereignissen und Rückrufen anstelle von Abfragen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-196">Use events and callbacks instead of polling.</span></span>
- <span data-ttu-id="8bc06-197">Versprechen verwenden.</span><span class="sxs-lookup"><span data-stu-id="8bc06-197">Use promises.</span></span> <span data-ttu-id="8bc06-198">In jQuery sind sie **Zurückgestellt** -Objekten aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-198">In jQuery they're called **Deferred** objects.</span></span> <span data-ttu-id="8bc06-199">Ähnliche Konzepte in Q, WinJS und ES6 sind vorhanden.</span><span class="sxs-lookup"><span data-stu-id="8bc06-199">There are similar concepts in Q, WinJS, and ES6.</span></span>
- <span data-ttu-id="8bc06-200">Verwenden des asynchronen Aufrufs wird nicht asynchronen Aufrufs an.</span><span class="sxs-lookup"><span data-stu-id="8bc06-200">Use the asynchronous call in favor of the non-asynchronous call.</span></span>
- <span data-ttu-id="8bc06-201">Verwenden Sie asynchrone jedes Mal, wenn eine Verzögerung könnte:</span><span class="sxs-lookup"><span data-stu-id="8bc06-201">Use asynchronous any time there could be a delay:</span></span>
    - <span data-ttu-id="8bc06-202">Während einer AJAX-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="8bc06-202">During an AJAX request.</span></span>
    - <span data-ttu-id="8bc06-203">Während eine erhebliche DOM-Bearbeitung.</span><span class="sxs-lookup"><span data-stu-id="8bc06-203">During any significant DOM manipulation.</span></span>

<span data-ttu-id="8bc06-204">Asynchrone Muster Verbesserung von Leistung und erhöhen die Reaktionsgeschwindigkeit und das effektive Verketten von abhängigen Aktionen ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-204">Asynchronous patterns improve performance and responsiveness and allow for the effective chaining of dependent actions.</span></span>

## <span data-ttu-id="8bc06-205"><a name="ClientSideCaching"></a>Das clientseitige Zwischenspeichern</span><span class="sxs-lookup"><span data-stu-id="8bc06-205"><a name="ClientSideCaching"></a> Client Side Caching</span></span>

<span data-ttu-id="8bc06-206">Das clientseitige Zwischenspeichern ist der meisten häufig verpassten Leistungssteigerungen, den, die Sie dem Code hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="8bc06-206">Client side caching is one of the most often missed performance enhancements you can add to your code.</span></span>

<span data-ttu-id="8bc06-207">Es gibt drei unterschiedliche Standorten Ihre Daten zwischengespeichert werden können:</span><span class="sxs-lookup"><span data-stu-id="8bc06-207">There are three different places you can cache your data:</span></span>

|<span data-ttu-id="8bc06-208">Option</span><span class="sxs-lookup"><span data-stu-id="8bc06-208">Option</span></span>|<span data-ttu-id="8bc06-209">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8bc06-209">Description</span></span>|
|:---|:---|
|<span data-ttu-id="8bc06-210">Sitzungsinformationen</span><span class="sxs-lookup"><span data-stu-id="8bc06-210">Session Storage</span></span>|<span data-ttu-id="8bc06-211">Speichert Daten als Schlüssel/Wert-Paar auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="8bc06-211">Stores data as a key/value pair on the client.</span></span> <span data-ttu-id="8bc06-212">Dies ist pro Sitzungsspeicher, die immer als Zeichenfolgen gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="8bc06-212">This is per session storage which is always stored as strings.</span></span> <br /> <span data-ttu-id="8bc06-213">JSON.stringify() konvertiert JavaScript-Objekte in Zeichenfolgen, das zum Speichern von Objekten unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8bc06-213">JSON.stringify() will convert your JavaScript objects to strings which helps to store objects.</span></span>
|<span data-ttu-id="8bc06-214">Lokaler Speicher</span><span class="sxs-lookup"><span data-stu-id="8bc06-214">Local Storage</span></span>|<p><span data-ttu-id="8bc06-215">Speichert Daten als Schlüssel/Wert-Paar auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="8bc06-215">Stores data as a key/value pair on the client.</span></span> <span data-ttu-id="8bc06-216">Dies ist dauerhaft in allen Sitzungen, die immer als Zeichenfolgen gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="8bc06-216">This is persistent across sessions which is always stored as strings.</span></span></p><p><span data-ttu-id="8bc06-217">JSON.stringify() konvertiert JavaScript-Objekte in Zeichenfolgen, das zum Speichern von Objekten unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8bc06-217">JSON.stringify() will convert your JavaScript objects to strings which helps to store objects.</span></span></p>|
|<span data-ttu-id="8bc06-218">Lokale Datenbank</span><span class="sxs-lookup"><span data-stu-id="8bc06-218">Local Database</span></span>|<span data-ttu-id="8bc06-219">Speichert relationale Daten auf dem Client.</span><span class="sxs-lookup"><span data-stu-id="8bc06-219">Stores relational data on the client.</span></span> <span data-ttu-id="8bc06-220">Als Datenbank-Engine wird häufig SQL-Lite verwendet.</span><span class="sxs-lookup"><span data-stu-id="8bc06-220">Frequently uses SQL-Lite as the database engine.</span></span><br><span data-ttu-id="8bc06-221">Lokale Datenbankspeicher ist nicht immer verfügbar auf allen Browsern&mdash;Ziel Browserunterstützung überprüfen</span><span class="sxs-lookup"><span data-stu-id="8bc06-221">Local Database storage is not always available on all browsers&mdash;Check target browser support</span></span>

<span data-ttu-id="8bc06-222">Zwischenspeichern, berücksichtigen Sie beim die Speichergrenzwerte für Sie verfügbar und Aktualität Ihrer Daten.</span><span class="sxs-lookup"><span data-stu-id="8bc06-222">When caching, keep in mind the storage limits available to you, and the freshness of your data.</span></span> 
- <span data-ttu-id="8bc06-223">Wenn Sie das Ende der Speichergrenzwerte erreicht, kann es ratsam, entfernen Sie die zwischengespeicherten Daten älteren oder weniger wichtigen sein.</span><span class="sxs-lookup"><span data-stu-id="8bc06-223">If you are reaching the end of your storage limits, it might be wise to remove the older or less important cached data.</span></span> 
- <span data-ttu-id="8bc06-224">Verschiedene Arten von Daten können schneller als andere veralten.</span><span class="sxs-lookup"><span data-stu-id="8bc06-224">Different kinds of data can become stale faster than others.</span></span> <span data-ttu-id="8bc06-225">Eine Liste mit Newsartikeln veraltete in fünf bis zehn Minuten werden kann, jedoch Profilname eines Benutzers kann für mindestens 24 Stunden häufig sicher zwischengespeichert.</span><span class="sxs-lookup"><span data-stu-id="8bc06-225">A list of news articles can be stale in five to ten minutes, but a user's profile name can often be safely cached for 24 hours or more.</span></span> 

<span data-ttu-id="8bc06-226">Lokale und Sitzung Speicher nicht integrierten Ablauf haben, aber führen Sie Cookies.</span><span class="sxs-lookup"><span data-stu-id="8bc06-226">Local and session storage doesn't have expiration built-in, but cookies do.</span></span> <span data-ttu-id="8bc06-227">Sie können Ihre Daten in ein Cookie Ablauf in Ihrer lokalen Kopie und Sitzung Speicher hinzufügen binden.</span><span class="sxs-lookup"><span data-stu-id="8bc06-227">You can tie your stored data to a cookie to add expiration to your local and session storage.</span></span> <span data-ttu-id="8bc06-228">Sie können einen Speicher-Wrapper, der ein Ablaufdatum umfasst auch aktivieren Sie dieses Kontrollkästchen in Ihrem Code.</span><span class="sxs-lookup"><span data-stu-id="8bc06-228">You can also create a storage wrapper that includes an expiration date and check this in your code.</span></span>

## <span data-ttu-id="8bc06-229"><a name="PriceOfPopularity"></a>Der Preis des Beliebtheit</span><span class="sxs-lookup"><span data-stu-id="8bc06-229"><a name="PriceOfPopularity"></a> The Price of Popularity</span></span>

<span data-ttu-id="8bc06-230">Wie oft werden Ihre Seite angezeigt?</span><span class="sxs-lookup"><span data-stu-id="8bc06-230">How often is your page viewed?</span></span> <span data-ttu-id="8bc06-231">In der klassischen Szenario wird auf der Homepage für des Unternehmens als Startseite für alle Browser in der gesamten Organisation festgelegt.</span><span class="sxs-lookup"><span data-stu-id="8bc06-231">In the classic scenario, the corporate home page is set as the launch page for all browsers across the organization.</span></span> <span data-ttu-id="8bc06-232">Klicken Sie dann erhalten Sie plötzlich weitaus größere Datenverkehr, als Sie schon einmal gedacht.</span><span class="sxs-lookup"><span data-stu-id="8bc06-232">Then you suddenly get far more traffic than you ever imagined.</span></span> <span data-ttu-id="8bc06-233">Jedes Byte des Inhalts wird plötzlich im Server-Leistung und Bandbreite, der Ihre Homepage vergrößert.</span><span class="sxs-lookup"><span data-stu-id="8bc06-233">Every byte of content is suddenly magnified in the server performance and bandwidth that your home page consumes.</span></span>

<span data-ttu-id="8bc06-234">Lösung: wechseln Licht auf der Homepage und ein Link zu den anderen Inhalt.</span><span class="sxs-lookup"><span data-stu-id="8bc06-234">The solution: Go light on the home page and link to the other content.</span></span>

<span data-ttu-id="8bc06-235">Daten fett Dashboards sind auch ein Kandidat für eine vom Anbieter gehosteten app die unabhängig voneinander zu skalieren kann.</span><span class="sxs-lookup"><span data-stu-id="8bc06-235">Data-heavy dashboards are also a candidate for a provider hosted app which can scale independently.</span></span>

## <span data-ttu-id="8bc06-236"><a name="LoaderPattern"></a>Das Muster Ladeprogramm</span><span class="sxs-lookup"><span data-stu-id="8bc06-236"><a name="LoaderPattern"></a> The Loader Pattern</span></span>

<span data-ttu-id="8bc06-237">Das Ziel des Musters Ladeprogramm ist, geben Sie eine Möglichkeit, eine unbekannte Anzahl von remote-Skripts in einer Website einbetten, ohne dass Sie die Website aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="8bc06-237">The goal of the loader pattern is to provide a way to embed an unknown number of remote scripts into a site without having to update the site.</span></span> <span data-ttu-id="8bc06-238">Die Updates auf dem CDN remote ausgeführt werden können und alle Websites aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="8bc06-238">The updates can be done on the remote CDN and will update all sites.</span></span>

<span data-ttu-id="8bc06-239">Das Muster Ladeprogramm erstellt eine URL mit Datums- und Zeitstempel am Ende, damit die Datei nicht zwischengespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="8bc06-239">The Loader Pattern constructs a URL with date and time stamp at the end so that the file will not be cached.</span></span> <span data-ttu-id="8bc06-240">Richtet jQuery als Abhängigkeit auf die Datei, und dann führt eine Funktion im Ladeprogramm aus.</span><span class="sxs-lookup"><span data-stu-id="8bc06-240">It sets up jQuery as a dependency on the loader file, then executes a function in the loader.</span></span> <span data-ttu-id="8bc06-241">Dadurch wird sichergestellt, dass Ihre benutzerdefinierte JavaScript geladen wird, nachdem jQuery geladen ist.</span><span class="sxs-lookup"><span data-stu-id="8bc06-241">This ensures your custom JavaScript will load after jQuery finishes loading.</span></span>

<span data-ttu-id="8bc06-242">PnP-dev\Samples\Core.JavaScript\Core.JavaScript.Embedder\Program.cs:</span><span class="sxs-lookup"><span data-stu-id="8bc06-242">PnP-dev\Samples\Core.JavaScript\Core.JavaScript.Embedder\Program.cs:</span></span>

```csharp
static void Main(string[] args)
{
    ContextManager.WithContext((context) =>
        // this is the script block that will be embedded into the page
        // in practice this can be done during provisioning of the site/web
        // make sure to include ';' at end to play nice with page embedding
        // using the script on demand feature built into SharePoint we load jQuery, then our remote loader(pnp-loader.js or pnp-loader-cached.js) file using a dependency
        var script = @"(function (loaderFile, nocache) {
                                var url = loaderFile + ((nocache) ? '?' + encodeURIComponent((new Date()).getTime()) : '');
                                SP.SOD.registerSod('pnp-jquery.js', 'https://localhost:44324/js/jquery.js');
                                SP.SOD.registerSod('pnp-loader.js', url);
                                SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');
                                SP.SOD.executeFunc('pnp-loader.js', null, function() {});
                        })('https://localhost:44324/pnp-loader.js', true);";


        // this version of the script along with pnp-loaderMDS.js (or pnp-loaderMDS-cached.js) handles pages where the minimum download strategy is active
        var script2 = @"ExecuteOrDelayUntilBodyLoaded(function () {
                            var url = 'https://localhost:44324/js/pnp-loaderMDS.js?' + encodeURIComponent((new Date()).getTime());
                            SP.SOD.registerSod('pnp-jquery.js', 'https://localhost:44324/js/jquery.js');
                            SP.SOD.registerSod('pnp-loader.js', url);
                            SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');
                            SP.SOD.executeFunc('pnp-loader.js', null, function () {
                                if (typeof pnpLoadFiles === 'undefined') {
                                    RegisterModuleInit('https://localhost:44324/js/pnp-loaderMDS.js', pnpLoadFiles);
                                } else {
                                    pnpLoadFiles();
                                }
                            });    
                        });";

        // load the collection of existing links
        var links = context.Site.RootWeb.UserCustomActions;
        context.Load(links, ls => ls.Include(l => l.Title));
        context.ExecuteQueryRetry();

        // this block handles deleting previous test custom actions
        var doDelete = false;

        foreach (var link in links.ToArray().Where(l => l.Title.Equals("MyTestCustomAction", StringComparison.OrdinalIgnoreCase)))
        {
            link.DeleteObject();
            doDelete = true;
        }

        if (doDelete)
        {
            context.ExecuteQueryRetry();
        }

        // now we embed our script into the user custom action
        var newLink = context.Site.RootWeb.UserCustomActions.Add();
        newLink.Title = "MyTestCustomAction";
        newLink.Description = "Doing some testing.";
        newLink.ScriptBlock = script2;
        newLink.Location = "ScriptLink";
        newLink.Update();
        context.ExecuteQueryRetry();
    });
}
```

<span data-ttu-id="8bc06-243">Die `SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');` richtet die Abhängigkeit und `SP.SOD.executeFunc('pnp-loader.js', null, function() {});` erzwingt jQuery vor dem Laden des benutzerdefinierten JavaScript vollständig geladen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-243">The `SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');` sets up the dependency, and `SP.SOD.executeFunc('pnp-loader.js', null, function() {});` forces jQuery to load completely before loading the custom JavaScript.</span></span>

<span data-ttu-id="8bc06-244">Die `newLink.ScriptBlock = script2;` und `newLink.Location = "ScriptLink";` sind die wichtigsten Punkte dies in die Aktion des Benutzers Kunden hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8bc06-244">The `newLink.ScriptBlock = script2;` and `newLink.Location = "ScriptLink";` are the key parts of adding this into the user customer action.</span></span>

<span data-ttu-id="8bc06-245">Die Datei pnp loader.js lädt dann eine Liste der JavaScript-Dateien mit eine Zusage, die ausgeführt werden kann, wenn jeder Datei geladen wird.</span><span class="sxs-lookup"><span data-stu-id="8bc06-245">The pnp-loader.js file then loads a list of JavaScript files, with a promise that can be run when each file loads.</span></span>

<span data-ttu-id="8bc06-246">PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js:</span><span class="sxs-lookup"><span data-stu-id="8bc06-246">PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js:</span></span>

```javascript
(function () {

    var urlbase = 'https://localhost:44324';
    var files = [
        '/js/pnp-settings.js',
        '/js/pnp-core.js',
        '/js/pnp-clientcache.js',
        '/js/pnp-config.js',
        '/js/pnp-logging.js',
        '/js/pnp-devdashboard.js',
        '/js/pnp-uimods.js'
    ];

    // create a promise
    var promise = $.Deferred();

    // this function will be used to recursively load all the files
    var engine = function () {

        // maintain context
        var self = this;

        // get the next file to load
        var file = self.files.shift();

        var fullPath = urlbase + file;

        // load the remote script file
        $.getScript(fullPath).done(function () {
            if (self.files.length > 0) {
                engine.call(self);
            }
            else {
                self.promise.resolve();
            }
        }).fail(self.promise.reject);
    };

    // create our "this" we will apply to the engine function
    var ctx = {
        files: files,
        promise: promise
    };

    // call the engine with our context
    engine.call(ctx);

    // give back the promise
    return promise.promise();

})().done(function () {
    /* all scripts are loaded and I could take actions here */
}).fail(function () {
    /* something failed, take some action here if needed */
});
```

<span data-ttu-id="8bc06-247">Die Datei pnp loader.js werden nicht zwischengespeichert und dem eignet sich gut für eine Entwicklungsumgebung.</span><span class="sxs-lookup"><span data-stu-id="8bc06-247">The pnp-loader.js file does not cache, which works well for a development environment.</span></span> <span data-ttu-id="8bc06-248">Die Datei pnp-Ladeprogramm-cached.js ersetzt die `$.getScript` -Funktion mit einer `$.ajax` -Funktion die ermöglicht die Browser Zwischenspeichern von Dateien und ist besser geeignet für die Produktion.</span><span class="sxs-lookup"><span data-stu-id="8bc06-248">The pnp-loader-cached.js file replaces the `$.getScript` function with an `$.ajax` function which allows for browser caching of the files and is better suited for production.</span></span>

<span data-ttu-id="8bc06-249">Aus PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js</span><span class="sxs-lookup"><span data-stu-id="8bc06-249">From PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js</span></span>

```javascript
    // load the remote script file
    $.ajax({
        type: 'GET',
        url: fullPath,
        cache: true,
        dataType: 'script'
    }).done(function () {
        if (self.files.length > 0) {
            engine.call(self);
        }
        else {
            self.promise.resolve();
        }
    }).fail(self.promise.reject);
```

<span data-ttu-id="8bc06-250">Dieses Muster vereinfacht die Bereitstellung und auf Websites aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="8bc06-250">This pattern eases deployment and updates to sites.</span></span> <span data-ttu-id="8bc06-251">Es ist besonders hilfreich beim Bereitstellen von oder in Tausenden von Websitesammlungen aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="8bc06-251">It is especially useful when deploying or updating across thousands of site collections.</span></span>

## <span data-ttu-id="8bc06-252"><a name="CachingCurrentUserInfo"></a>Den aktuellen Benutzer Zwischenspeichern</span><span class="sxs-lookup"><span data-stu-id="8bc06-252"><a name="CachingCurrentUserInfo"></a> Caching the current user</span></span>

<span data-ttu-id="8bc06-253">Wenn die Benutzerinformationen bereits zwischengespeichert wird, ruft diese Funktion die Daten aus dem Sitzungscache ab.</span><span class="sxs-lookup"><span data-stu-id="8bc06-253">If the user info is already cached, this function gets the data from the session cache.</span></span> <span data-ttu-id="8bc06-254">Wenn die Benutzerinformationen nicht im Cache gespeichert ist, ruft es die bestimmte Benutzerinformationen wir müssen und in den Cache gespeichert.</span><span class="sxs-lookup"><span data-stu-id="8bc06-254">If the user info is not stored in the cache, it gets the specific user info we need and stores it in the cache.</span></span>

<span data-ttu-id="8bc06-255">Es wird auch zurückgestellt (jQuery-Version des Zusage) verwendet.</span><span class="sxs-lookup"><span data-stu-id="8bc06-255">This also uses Deferred (jQuery version of promise).</span></span> <span data-ttu-id="8bc06-256">Wenn wir die Daten aus dem Cache oder vom Server erhalten möchten, ist die verzögerte behoben.</span><span class="sxs-lookup"><span data-stu-id="8bc06-256">If we get the data from the cache or from the server, the Deferred is resolved.</span></span> <span data-ttu-id="8bc06-257">Wenn ein Fehler vorliegt, wird die verzögerte abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="8bc06-257">If there is an error, the Deferred is rejected.</span></span>

<span data-ttu-id="8bc06-258">Aus PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-core.js:</span><span class="sxs-lookup"><span data-stu-id="8bc06-258">From PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-core.js:</span></span>

```javascript
    getCurrentUserInfo: function (ctx) {

        var self = this;

        if (self._currentUserInfoPromise == null) {

            self._currentUserInfoPromise = $.Deferred(function (def) {

                var cachingTest = $pnp.session !== 'undefined' && $pnp.session.enabled;

                // if we have the caching module loaded
                if (cachingTest) {
                    var userInfo = $pnp.session.get(self._currentUserInfoCacheKey);
                    if (userInfo !== null) {
                        self._currentUserInfo = userInfo;
                        def.resolveWith(ctx || self._currentUserInfo, [self._currentUserInfo]);
                        return;
                    }
                }

                // send the request and allow caching
                $.ajax({
                    method: 'GET',
                    url: '/_api/SP.UserProfiles.PeopleManager/GetMyProperties?$select=AccountName,DisplayName,Title',
                    headers: { "Accept": "application/json; odata=verbose" },
                    cache: true
                }).done(function (response) {

                    // we also parse and add some custom properties as an example
                    self._currentUserInfo = $.extend(response.d,
                        {
                            ParsedLoginName: $pnp.core.getUserIdFromLogin(response.d.AccountName)
                        });

                    if (cachingTest) {
                        $pnp.session.add(self._currentUserInfoCacheKey, self._currentUserInfo);
                    }

                    def.resolveWith(ctx || self._currentUserInfo, [self._currentUserInfo]);

                }).fail(function (jqXHR, textStatus, errorThrown) {

                    console.error('[PNP]=>[Fatal Error] Could not load current user data data from /_api/SP.UserProfiles.PeopleManager/GetMyProperties. status: ' + textStatus + ', error: ' + errorThrown);
                    def.rejectWith(ctx || null);
                });
            });
        }

        return this._currentUserInfoPromise.promise();
    }
}
```

## <span data-ttu-id="8bc06-259"><a name="CachingPatternUsingAsynchronousAndDeferred"></a>Zwischenspeichern von asynchronen und zurückgestellte Muster</span><span class="sxs-lookup"><span data-stu-id="8bc06-259"><a name="CachingPatternUsingAsynchronousAndDeferred"></a> Caching pattern using asynchronous and Deferred</span></span>

<span data-ttu-id="8bc06-260">Ein weiteres Zwischenspeicherns Muster pnp clientcache.js StorageTest, finden Sie in die die Modernizer StorageTest entnommen wird.</span><span class="sxs-lookup"><span data-stu-id="8bc06-260">Another caching pattern can be found in pnp-clientcache.js storageTest, which is taken from the modernizer storageTest.</span></span> <span data-ttu-id="8bc06-261">Es enthält Funktionen zum Hinzufügen, abrufen, entfernen und GetOrAdd der die zwischengespeicherten Daten zurückgegeben wird, wenn im Cache ist oder die Daten vom Server ab und dem Cache hinzufügen, wenn sie nicht im Cache ist dem Schreiben von sich wiederholendem Code in der aufrufenden Funktion gespeichert.</span><span class="sxs-lookup"><span data-stu-id="8bc06-261">It contains functions for add, get, remove, and getOrAdd which will return the cached data if it's in the cache, or retrieve the data from the server and add it to the cache if it is not in the cache which saves writing repetitive code in the calling function.</span></span> <span data-ttu-id="8bc06-262">Get wird JSON.parse zum Ablauf zu testen, da Ablaufdatum in lokaler Speicher nicht wird verwendet.</span><span class="sxs-lookup"><span data-stu-id="8bc06-262">get uses JSON.parse to test for expiration since expiration is not a feature in local storage.</span></span> <span data-ttu-id="8bc06-263">_createPersistable speichert das JavaScript-Objekt im Cache lokalen Speicher.</span><span class="sxs-lookup"><span data-stu-id="8bc06-263">_createPersistable stores the JavaScript object in the local storage cache.</span></span>

<span data-ttu-id="8bc06-264">Aus PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-clientcache.js:</span><span class="sxs-lookup"><span data-stu-id="8bc06-264">From PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-clientcache.js:</span></span>

```javascript
// adds the client cache capability
caching: {

    // determine if we have local storage once
    enabled: storageTest(),

    add: function (/*string*/ key, /*object*/ value, /*datetime*/ expiration) {

        if (this.enabled) {
            localStorage.setItem(key, this._createPersistable(value, expiration));
        }
    },

    // gets an item from the cache, checking the expiration and removing the object if it is expired
    get: function (/*string*/ key) {

        if (!this.enabled) {
            return null;
        }

        var o = localStorage.getItem(key);

        if (o == null) {
            return o;
        }

        var persistable = JSON.parse(o);

        if (new Date(persistable.expiration) <= new Date()) {

            this.remove(key);
            o = null;

        } else {

            o = persistable.value;
        }

        return o;
    },

    // removes an item from local storage by key
    remove: function (/*string*/ key) {

        if (this.enabled) {
            localStorage.removeItem(key);
        }
    },

    // gets an item from the cache or adds it using the supplied getter function
    getOrAdd: function (/*string*/ key, /*function*/ getter) {

        if (!this.enabled) {
            return getter();
        }

        if (!$.isFunction(getter)) {
            throw 'Function expected for parameter "getter".';
        }

        var o = this.get(key);

        if (o == null) {
            o = getter();
            this.add(key, o);
        }

        return o;
    },

    // creates the persisted object wrapper using the value and the expiration, setting the default expiration if none is applied
    _createPersistable: function (/*object*/ o, /*datetime*/ expiration) {

        if (typeof expiration === 'undefined') {
            expiration = $pnp.core.dateAdd(new Date(), 'minute', $pnp.settings.localStorageDefaultTimeoutMinutes);
        }

        return JSON.stringify({
            value: o,
            expiration: expiration
        });
    }
},
```

<span data-ttu-id="8bc06-265">Für eine komplexere Verwendung der asynchronen und zurückgestellt können Sie auf das Entwicklerdashboard in pnp clientcache.js verweisen</span><span class="sxs-lookup"><span data-stu-id="8bc06-265">For a more complex usage of asynchronous and Deferred, you can refer to the developer dashboard in pnp-clientcache.js</span></span>

## <span data-ttu-id="8bc06-266"><a name="Resources"></a>Ressourcen</span><span class="sxs-lookup"><span data-stu-id="8bc06-266"><a name="Resources"></a> Resources</span></span>

### <a name="see-also"></a><span data-ttu-id="8bc06-267">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="8bc06-267">See Also</span></span>
- [<span data-ttu-id="8bc06-268">JavaScript-Muster und Verwendungsanalyse</span><span class="sxs-lookup"><span data-stu-id="8bc06-268">JavaScript – Patterns and Usage</span></span>](http://dev.office.com/blogs/javascript-development-patterns-with-sharepoint)
- [<span data-ttu-id="8bc06-269">JavaScript – Leistungsaspekte</span><span class="sxs-lookup"><span data-stu-id="8bc06-269">JavaScript – Performance Considerations</span></span>](http://dev.office.com/blogs/javascript-performance-considerations-with-sharepoint)
- [<span data-ttu-id="8bc06-270">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8bc06-270">Complete basic operations using JavaScript library code in SharePoint 2013</span></span>](https://msdn.microsoft.com/EN-US/library/office/jj163201.aspx)
- [<span data-ttu-id="8bc06-271">Clientseitiges Rendering (JS-Verknüpfung)-Codebeispiele</span><span class="sxs-lookup"><span data-stu-id="8bc06-271">Client-side rendering (JS Link) code samples</span></span>](https://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a)
- [<span data-ttu-id="8bc06-272">JavaScript einbetten (Anpassen der Benutzeroberfläche für SharePoint-Website mithilfe von JavaScript)</span><span class="sxs-lookup"><span data-stu-id="8bc06-272">JavaScript Embedding (Customize your SharePoint site UI by using JavaScript)</span></span>](https://msdn.microsoft.com/EN-US/library/dn913116.aspx)
- [<span data-ttu-id="8bc06-273">Durchsuchen von Anpassungen für SharePoint</span><span class="sxs-lookup"><span data-stu-id="8bc06-273">Search customizations for SharePoint</span></span>](https://msdn.microsoft.com/EN-US/library/mt210901.aspx)
- [<span data-ttu-id="8bc06-274">SharePoint-Add-in-Anleitung – benutzerdefinierte Feldtyp (mithilfe von Client Side Rendering)</span><span class="sxs-lookup"><span data-stu-id="8bc06-274">SharePoint Add-in Recipe – Custom field type (by using Client Side Rendering)</span></span>](custom-field-type-sharepoint-add-in.md)

### <a name="samples"></a><span data-ttu-id="8bc06-275">Beispiele (engl.)</span><span class="sxs-lookup"><span data-stu-id="8bc06-275">Samples</span></span>

- [<span data-ttu-id="8bc06-276">Performance.Caching</span><span class="sxs-lookup"><span data-stu-id="8bc06-276">Performance.Caching</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching)
- [<span data-ttu-id="8bc06-277">Core.JavaScript</span><span class="sxs-lookup"><span data-stu-id="8bc06-277">Core.JavaScript</span></span>](https://github.com/SharePoint/Pnp/tree/master/Samples/Core.JavaScript)
