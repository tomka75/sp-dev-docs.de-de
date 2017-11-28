---
title: Typ des benutzerdefinierten Felds in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 550669c2e1cb7e766f93ed1ae00fc0962421bace
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="custom-field-type-in-the-sharepoint-add-in-model"></a><span data-ttu-id="e9070-102">Typ des benutzerdefinierten Felds in der SharePoint-add-in-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="e9070-102">Custom field type in the SharePoint add-in model</span></span>
================================================

<a name="summary"></a><span data-ttu-id="e9070-103">Summary</span><span class="sxs-lookup"><span data-stu-id="e9070-103">Summary</span></span>
-------

<span data-ttu-id="e9070-104">Ansatz verwenden Sie angepasste Endbenutzer Erfahrungen anzugebende unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.</span><span class="sxs-lookup"><span data-stu-id="e9070-104">The approach you take to provide customized end user experiences is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="e9070-105">In einer typischen vollständige vertrauen Code (FTC) / Szenario Farmlösung, benutzerdefinierte Feldtypen mit SharePoint Server-Side-Objektmodellcode erstellt wurden, durch Vererbung von einer der integrierten feldtypklassen und durch Erstellen einer Feldtyp-Bereitstellungsdatei (XML).</span><span class="sxs-lookup"><span data-stu-id="e9070-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, custom field types were created with the SharePoint server-side object model code by inheriting from one of the built-in field type classes and creating a field type deployment file (XML).</span></span> <span data-ttu-id="e9070-106">Diese Komponenten wurden über die SharePoint-Lösungen bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="e9070-106">These components were deployed via SharePoint solutions.</span></span> 

<span data-ttu-id="e9070-107">In einem Szenario mit SharePoint-Add-ins Modell werden angepasste Endbenutzer Erfahrungen über clientseitiges Rendering implementiert.</span><span class="sxs-lookup"><span data-stu-id="e9070-107">In a SharePoint Add-ins model scenario, customized end user experiences are implemented via client-side rendering.</span></span> <span data-ttu-id="e9070-108">Bei diesem Ansatz werden JavaScript-Dateien zum Implementieren von angepassten Endbenutzer Erfahrungen verwendet.</span><span class="sxs-lookup"><span data-stu-id="e9070-108">In this approach, JavaScript files are used to implement customized end user experiences.</span></span> <span data-ttu-id="e9070-109">Das remote provisioning Muster stellt die JavaScript-Dateien und registriert diese mit SharePoint-Felder über die JSLink-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="e9070-109">The remote provisioning pattern deploys the JavaScript files and registers them with SharePoint fields via the JSLink property.</span></span>

<span data-ttu-id="e9070-110">Aus Sicht des Endbenutzers sieht das Funktion/Ergebnis gleich aus.</span><span class="sxs-lookup"><span data-stu-id="e9070-110">From an end user's perspective the capability/result looks the same.</span></span>

<span data-ttu-id="e9070-111">Es folgen einige Beispiele der Typ des benutzerdefinierten Felds, die eine Zuordnung Google implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="e9070-111">Here are some examples of custom field type that implements a Google map.</span></span> <span data-ttu-id="e9070-112">Diese ergeben sich aus dem [Branding.JSLink](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink) Office 365 Plug & Play-Beispiel.</span><span class="sxs-lookup"><span data-stu-id="e9070-112">These come from the [Branding.JSLink](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink) Office 365 PnP Sample.</span></span>

<span data-ttu-id="e9070-113">**Google-Zuordnung Miniaturansichten in einer Listenansicht angezeigt:**</span><span class="sxs-lookup"><span data-stu-id="e9070-113">**Thumbnail Google map images displayed in a list view:**</span></span>

![Zwei Google Kartenansichten Microsoft Campus Location Point und Bereich angezeigt.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps.png)

<span data-ttu-id="e9070-115">**Inlinebearbeitung eine größere Google Map Miniaturansicht angezeigt:**
![zwei Google zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="e9070-115">**Inline editing showing a larger Google map thumbnail:**
![Two Google maps.</span></span> <span data-ttu-id="e9070-116">Eine Ansicht mit dem Microsoft Campus Location Point mit einem Link, wählen Sie den Speicherort, der anderen Ansicht darstellen Microsoft Campus Speicherort mit einem Link zum-Shape bearbeiten.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Edit.png)</span><span class="sxs-lookup"><span data-stu-id="e9070-116">One view showing the Microsoft Campus Location Point with a link to Select Location, the other view showing the Microsoft Campus Location Area with a link to Edit Shape.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Edit.png)</span></span>

<span data-ttu-id="e9070-117">**Ein Dialogfeld mit dem Aktivieren der Inlinebearbeitung:**
![eine Google Wegweiser für die Microsoft Campus Form angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e9070-117">**A dialog enabling inline editing:**
![A Google Map showing the Microsoft Campus Shape.</span></span> <span data-ttu-id="e9070-118">Text auf das Bild liest, klicken Sie auf der Karte Markierungen platzieren und erstellen Ihre Form.</span><span class="sxs-lookup"><span data-stu-id="e9070-118">Text on the image reads, Click on the map to place markers and create your shape.</span></span> <span data-ttu-id="e9070-119">Fertig stellen Sie, indem Sie auf der ersten Marker.</span><span class="sxs-lookup"><span data-stu-id="e9070-119">Finish by clicking on the first marker.</span></span> <span data-ttu-id="e9070-120">Sie können ziehen Sie jede der Markierungen um, oder klicken Sie auf klicken sie auf Weitere Optionen.</span><span class="sxs-lookup"><span data-stu-id="e9070-120">You can drag each of the markers around, or click on them for more options.</span></span> <span data-ttu-id="e9070-121">Oben auf die Schaltfläche Zuordnung löschen können Sie um alle Marken zu entfernen.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Shape_Edit.png)</span><span class="sxs-lookup"><span data-stu-id="e9070-121">You can use the Clear Map button above to remove all markers.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Shape_Edit.png)</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="e9070-122">Allgemeine Richtlinien</span><span class="sxs-lookup"><span data-stu-id="e9070-122">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="e9070-123">In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für die Implementierung clientseitiges Rendering bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="e9070-123">As a rule of a thumb, we would like to provide the following high-level guidelines for implementing client-side rendering.</span></span>

- <span data-ttu-id="e9070-124">Verwenden Sie die JavaScript-Dateien und clientseitiges Rendering benutzerdefinierte Feldtypen implementieren.</span><span class="sxs-lookup"><span data-stu-id="e9070-124">Use JavaScript files and client-side rendering to implement custom field types.</span></span>
- <span data-ttu-id="e9070-125">Verwenden Sie das remote provisioning Muster JavaScript-Dateien bereitstellen und registrieren mit SharePoint-Felder oder -Listenansicht-Webparts.</span><span class="sxs-lookup"><span data-stu-id="e9070-125">Use the remote provisioning pattern to deploy JavaScript files and register them with SharePoint fields or List View Web Parts.</span></span>
- <span data-ttu-id="e9070-126">Registrieren Sie das Modul minimale herunterladen Strategie (MDS), um sicherzustellen, dass das Modul MDS sollten Sie die benutzerdefinierte Rendering JavaScript-Dateien ist die JavaScript-Dateien.</span><span class="sxs-lookup"><span data-stu-id="e9070-126">Register the JavaScript files with the Minimal Download Strategy (MDS) engine to ensure the MDS engine is aware of the custom rendering JavaScript files.</span></span>
- <span data-ttu-id="e9070-127">Festlegen des JSLink-Eigenschaft mit Hostwebsite mindestens Vollzugriff auf Webebene erfordert, daher wird diese Vorgehensweise nicht geeignet für add-ins auf der SharePoint Store ist</span><span class="sxs-lookup"><span data-stu-id="e9070-127">Setting JSLink property to host web requires at least full permission at web level, so this approach is not suitable for add-ins at the SharePoint store</span></span>

<a name="options-to-implement-client-side-rendering-with-javascript-files-via-the-jslink-property"></a><span data-ttu-id="e9070-128">Optionen für die Implementierung von clientseitiges Rendering mit JavaScript-Dateien über die JSLink-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="e9070-128">Options to implement client-side rendering with JavaScript files via the JSLink property</span></span>
----------------------------------------------------------------------------------------

<span data-ttu-id="e9070-129">Sie haben eine Reihe von Optionen für die Implementierung von clientseitiges Rendering mit JavaScript-Dateien über die JSLink-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="e9070-129">You have a couple of options to implement client-side rendering with JavaScript files via the JSLink property.</span></span>

- <span data-ttu-id="e9070-130">Legen Sie die JSLink-Eigenschaft auf eine Listenansicht-Webpart, das eine Ansicht einer SharePoint-Liste rendert.</span><span class="sxs-lookup"><span data-stu-id="e9070-130">Set the JSLink property on a List View Web Part that renders a view of a SharePoint list.</span></span> 
- <span data-ttu-id="e9070-131">Legen Sie die JSLink-Eigenschaft für ein SharePoint-Feld.</span><span class="sxs-lookup"><span data-stu-id="e9070-131">Set the JSLink property for a SharePoint field.</span></span> 
- <span data-ttu-id="e9070-132">Legen Sie die JSLink-Eigenschaft für ein SharePoint-Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="e9070-132">Set the JSLink property for a SharePoint content type.</span></span> 
    

<a name="set-the-jslink-property-on-a-list-view-web-part-that-renders-a-view-of-a-sharepoint-list"></a><span data-ttu-id="e9070-133">Legen Sie die JSLink-Eigenschaft auf eine Listenansicht-Webpart, das eine Ansicht einer SharePoint-Liste rendert</span><span class="sxs-lookup"><span data-stu-id="e9070-133">Set the JSLink property on a List View Web Part that renders a view of a SharePoint list</span></span>
-----------------------------------------------------------------------------------------
<span data-ttu-id="e9070-134">Bei dieser Option legen Sie die JSLink-Eigenschaft auf eine WebPartDefinition.</span><span class="sxs-lookup"><span data-stu-id="e9070-134">In this option you set the JSLink property on a WebPartDefinition.</span></span>
    
- <span data-ttu-id="e9070-135">**Dieser Ansatz erstellen ein benutzerdefinierten Feldtyps nicht speziell auf der Ebene der SPField.**</span><span class="sxs-lookup"><span data-stu-id="e9070-135">**This approach does not specifically create a custom field type at the SPField level.**</span></span>
    + <span data-ttu-id="e9070-136">Aus diesem Grund *das benutzerdefinierte Rendering gilt nur in der Listenansicht-Webpart, in dem Sie die JSLink-Eigenschaft festlegen*.</span><span class="sxs-lookup"><span data-stu-id="e9070-136">Therefore, *the custom rendering only applies in the List View Web Part where you set the JSLink property*.</span></span>
- <span data-ttu-id="e9070-137">Dieser Ansatz ermöglicht es das Rendering für eine oder mehrere SharePoint-Felder gleichzeitig zu ändern.</span><span class="sxs-lookup"><span data-stu-id="e9070-137">This approach allows you to change the rendering for one or more SharePoint fields at once.</span></span>
- <span data-ttu-id="e9070-138">Dieser Ansatz kann mit deklarativem Code, mit dem SharePoint Server-Side-Objektmodell, mit dem SharePoint mithilfe der clientseitigen Objektmodell (CSOM) oder über PowerShell erfolgen.</span><span class="sxs-lookup"><span data-stu-id="e9070-138">This approach may be done with declarative code, with the SharePoint server-side object model, with the SharePoint client-side object model (CSOM), or via PowerShell.</span></span>
    + <span data-ttu-id="e9070-139">Es wird empfohlen, dass Sie das SharePoint Server-Side-Objektmodell, den SharePoint-Client-seitigen Objektmodell oder die PowerShell verwenden, um die JSLink-Eigenschaft über die remote provisioning Muster festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e9070-139">We recommend you use the SharePoint server-side object model, the SharePoint client-side object model, or PowerShell to set the JSLink property via the remote provisioning pattern.</span></span>

<span data-ttu-id="e9070-140">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="e9070-140">**When is it a good fit?**</span></span>

<span data-ttu-id="e9070-141">Wenn Sie bestimmte Ansichten für SharePoint-Listendaten definieren, und ändern das Rendering für mehr als ein SharePoint-Feld müssen, ist dies eine gute Wahl.</span><span class="sxs-lookup"><span data-stu-id="e9070-141">When you need to define specific views for SharePoint list data and modify the rendering for more than one SharePoint field, this is a good option.</span></span>

<span data-ttu-id="e9070-142">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="e9070-142">**Getting started**</span></span>

<span data-ttu-id="e9070-143">Im folgende Beispiel wird die JSLink-Eigenschaft auf eine SharePoint Listenansicht-Webpart.</span><span class="sxs-lookup"><span data-stu-id="e9070-143">The following sample sets the JSLink property on a SharePoint List View Web Part.</span></span>

- [<span data-ttu-id="e9070-144">Branding.ClientSideRendering (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="e9070-144">Branding.ClientSideRendering (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
    + <span data-ttu-id="e9070-145">Enthält 9 Beispiele, in denen die JSLink-Eigenschaft für ein SharePoint Listenansicht-Webpart und eine Erläuterung der Implementierung der jedes Beispiel festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e9070-145">Includes 9 samples that set the JSLink property on a SharePoint List View Web Part and an explanation of how each sample was implemented.</span></span>
    + <span data-ttu-id="e9070-146">Die RegisterJStoWebPart-Methode wird die Listenansicht-Webpart des JSLink-Eigenschaft festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e9070-146">The RegisterJStoWebPart method sets the List View Web Part's JSLink property.</span></span> 

<a name="set-the-jslink-property-for-a-sharepoint-field"></a><span data-ttu-id="e9070-147">Legen Sie die JSLink-Eigenschaft für ein SharePoint-Feld</span><span class="sxs-lookup"><span data-stu-id="e9070-147">Set the JSLink property for a SharePoint field</span></span>
----------------------------------------------

<span data-ttu-id="e9070-148">Bei dieser Option legen Sie die JSLink-Eigenschaft für ein SPField.</span><span class="sxs-lookup"><span data-stu-id="e9070-148">In this option you set the JSLink property on an SPField.</span></span>
    
- <span data-ttu-id="e9070-149">**Dieser Ansatz registriert insbesondere die JSLink-Eigenschaft auf der Ebene der SPField.**</span><span class="sxs-lookup"><span data-stu-id="e9070-149">**This approach specifically registers the JSLink property at the SPField level.**</span></span>
    + <span data-ttu-id="e9070-150">Aus diesem Grund *gilt das benutzerdefinierte Rendering überall der SPField gerendert wird*.</span><span class="sxs-lookup"><span data-stu-id="e9070-150">Therefore, *the custom rendering will apply everywhere the SPField is rendered*.</span></span>
- <span data-ttu-id="e9070-151">Dieser Ansatz ermöglicht Ihnen, das Rendering für ein SharePoint-Feld zu ändern.</span><span class="sxs-lookup"><span data-stu-id="e9070-151">This approach allows you to change the rendering for one SharePoint field.</span></span>
- <span data-ttu-id="e9070-152">Dieser Ansatz kann mit deklarativem Code, mit dem SharePoint Server-Side-Objektmodell, mit dem SharePoint-Objektmodell mithilfe der clientseitigen oder über PowerShell erfolgen.</span><span class="sxs-lookup"><span data-stu-id="e9070-152">This approach may be done with declarative code, with the SharePoint server-side object model, with the SharePoint client-side object model, or via PowerShell.</span></span>
    + <span data-ttu-id="e9070-153">Es wird empfohlen, dass Sie das SharePoint Server-Side-Objektmodell, den SharePoint-Client-seitigen Objektmodell oder die PowerShell verwenden, um die JSLink-Eigenschaft über die remote provisioning Muster festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e9070-153">We recommend you use the SharePoint server-side object model, the SharePoint client-side object model, or PowerShell to set the JSLink property via the remote provisioning pattern.</span></span>

<span data-ttu-id="e9070-154">**Wenn sie geeignet ist?**</span><span class="sxs-lookup"><span data-stu-id="e9070-154">**When is it a good fit?**</span></span>

<span data-ttu-id="e9070-155">Wenn Sie zum Definieren einer bestimmten Ansicht für ein bestimmtes Feld SharePoint, und stellen Sie sicher, dass die Ansicht immer verwendet wird benötigen, wenn das Feld gerendert wird, ist dies eine gute Wahl.</span><span class="sxs-lookup"><span data-stu-id="e9070-155">When you need to define a specific view for a given SharePoint field and ensure the view is always used when the field is rendered, this is a good option.</span></span>

<span data-ttu-id="e9070-156">**Erste Schritte**</span><span class="sxs-lookup"><span data-stu-id="e9070-156">**Getting started**</span></span>

<span data-ttu-id="e9070-157">In den folgenden Artikeln wird gezeigt, wie die JSLink-Eigenschaft auf eine SPField festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e9070-157">The following articles demonstrate how to set the JSLink property on a SPField.</span></span>

- [<span data-ttu-id="e9070-158">Verwenden die JSLink-Eigenschaft die Art zu ändern, die Ihre Feld oder Ansichten in SharePoint 2013 (Tobias Zimmergren) gerendert werden</span><span class="sxs-lookup"><span data-stu-id="e9070-158">Using the JSLink property to change the way your field or views are rendered in SharePoint 2013 (Tobias Zimmergren)</span></span>](http://zimmergren.net/technical/sp-2013-using-the-spfield-jslink-property-to-change-the-way-your-field-is-rendered-in-sharepoint-2013)
- [<span data-ttu-id="e9070-159">Verwenden von JSLink mit SharePoint 2013 (MSDN Magazine)</span><span class="sxs-lookup"><span data-stu-id="e9070-159">Using JSLink with SharePoint 2013 (MSDN Magazine)</span></span>](https://msdn.microsoft.com/en-us/magazine/dn745867.aspx)

<a name="challenges-with-implementing-client-side-rendering-with-javascript-files-via-the-jslink-property"></a><span data-ttu-id="e9070-160">Probleme bei der Implementierung von clientseitiges Rendering mit JavaScript-Dateien über die JSLink-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="e9070-160">Challenges with implementing client-side rendering with JavaScript files via the JSLink property</span></span>
------------------------------------------------------------------------------------------------

<span data-ttu-id="e9070-161">Benutzerdefiniertes clientseitiges Rendering Komponenten bei der Entwicklung, behalten Sie im Hinterkopf Folgendes.</span><span class="sxs-lookup"><span data-stu-id="e9070-161">As you develop custom client-side rendering components, keep in mind the following things.</span></span>

- <span data-ttu-id="e9070-162">Nicht alle SharePoint-Felder können mit der JSLink-Eigenschaft außer Kraft gesetzt werden.</span><span class="sxs-lookup"><span data-stu-id="e9070-162">Not all SharePoint fields may be overridden with the JSLink property.</span></span>
    + <span data-ttu-id="e9070-163">Die TaxonomyField ist ein gutes Beispiel.</span><span class="sxs-lookup"><span data-stu-id="e9070-163">The TaxonomyField is a good example.</span></span>
- <span data-ttu-id="e9070-164">JSLink unterstützt mehrere Token.</span><span class="sxs-lookup"><span data-stu-id="e9070-164">JSLink supports several tokens.</span></span>
    + <span data-ttu-id="e9070-165">_layouts</span><span class="sxs-lookup"><span data-stu-id="e9070-165">_layouts</span></span>
    + <span data-ttu-id="e9070-166">_SITE</span><span class="sxs-lookup"><span data-stu-id="e9070-166">_site</span></span>
    + <span data-ttu-id="e9070-167">_siteCollection</span><span class="sxs-lookup"><span data-stu-id="e9070-167">_siteCollection</span></span>
    + <span data-ttu-id="e9070-168">_siteCollectionLayouts</span><span class="sxs-lookup"><span data-stu-id="e9070-168">_siteCollectionLayouts</span></span>
    + <span data-ttu-id="e9070-169">_siteLayouts</span><span class="sxs-lookup"><span data-stu-id="e9070-169">_siteLayouts</span></span>
- <span data-ttu-id="e9070-170">Sie können die JSLink JavaScript-Dateien mit SharePoint Skript auf Anforderung (SOD) Framework verzögerte Laden der Datei registrieren.</span><span class="sxs-lookup"><span data-stu-id="e9070-170">You can register the JSLink JavaScript files with the SharePoint Script On Demand (SOD) framework to lazy load the file.</span></span>
    - <span data-ttu-id="e9070-171">Verwenden Sie das Tag (d) am Ende der URL JSLink die Datei mit der SOD registrieren.</span><span class="sxs-lookup"><span data-stu-id="e9070-171">Use the (d) tag at the end of the JSLink URL to register the file with the SOD.</span></span>
 
    ```
    ~sitecollection/Style Library/JSLink-Samples/DependentFields.js(d)
    ```
- <span data-ttu-id="e9070-172">Sie können mehrere JavaScript-Dateien über die JSLink-Eigenschaft laden.</span><span class="sxs-lookup"><span data-stu-id="e9070-172">You can load multiple JavaScript files via the JSLink property.</span></span>
    + <span data-ttu-id="e9070-173">Dies ist insbesondere dann hilfreich, wenn eine Bibliothek der JavaScript-Dateien, die Ihre clientseitiges Rendering implementieren.</span><span class="sxs-lookup"><span data-stu-id="e9070-173">This is especially helpful if you have a library of JavaScript files that implement your client-side rendering.</span></span>
    + <span data-ttu-id="e9070-174">Erwägen Sie diese Vorgehensweise bei mobile Geräten Zielgruppenadressierung, da Sie nur das JavaScript übermitteln, Sie ein bestimmtes SharePoint-Feld clientseitiges Rendering implementieren müssen, können.</span><span class="sxs-lookup"><span data-stu-id="e9070-174">Consider using this approach when targeting mobile devices because it allows you to deliver just the JavaScript you need to implement a given SharePoint field's client-side rendering.</span></span>
    + <span data-ttu-id="e9070-175">Verwendung der | Zeichen, trennen Sie die JavaScript-Dateien, die Sie laden möchten.</span><span class="sxs-lookup"><span data-stu-id="e9070-175">Use the | character to separate the JavaScript files you wish to load.</span></span> 
    
    ```
    ~sitecollection/Style Library/JSLink-Samples/MainLibrary.js|~sitecollection/Style Library/JSLink-Samples/SpecificField.js**(d)**
    ```

<a name="related-links"></a><span data-ttu-id="e9070-176">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="e9070-176">Related links</span></span>
=============
- [<span data-ttu-id="e9070-177">SPField.JSLink-Eigenschaft (MSDN-API-Dokumente)</span><span class="sxs-lookup"><span data-stu-id="e9070-177">SPField.JSLink property (MSDN API Docs)</span></span>](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfield.jslink.aspx)
- [<span data-ttu-id="e9070-178">Verwenden die JSLink-Eigenschaft die Art zu ändern, die Ihre Feld oder Ansichten in SharePoint 2013 (Tobias Zimmergren) gerendert werden</span><span class="sxs-lookup"><span data-stu-id="e9070-178">Using the JSLink property to change the way your field or views are rendered in SharePoint 2013 (Tobias Zimmergren)</span></span>](http://zimmergren.net/technical/sp-2013-using-the-spfield-jslink-property-to-change-the-way-your-field-is-rendered-in-sharepoint-2013)
- [<span data-ttu-id="e9070-179">Verwenden von JSLink mit SharePoint 2013 (MSDN Magazine)</span><span class="sxs-lookup"><span data-stu-id="e9070-179">Using JSLink with SharePoint 2013 (MSDN Magazine)</span></span>](https://msdn.microsoft.com/en-us/magazine/dn745867.aspx)
- <span data-ttu-id="e9070-180">Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")</span><span class="sxs-lookup"><span data-stu-id="e9070-180">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="e9070-181">Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")</span><span class="sxs-lookup"><span data-stu-id="e9070-181">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="e9070-182">Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span><span class="sxs-lookup"><span data-stu-id="e9070-182">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="e9070-183">Verwandte Plug & Play-Beispiele</span><span class="sxs-lookup"><span data-stu-id="e9070-183">Related PnP samples</span></span>
===================

- [<span data-ttu-id="e9070-184">Branding.ClientSideRendering (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="e9070-184">Branding.ClientSideRendering (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
- [<span data-ttu-id="e9070-185">Branding.JSLink (O365 Plug & Play-Beispiel)</span><span class="sxs-lookup"><span data-stu-id="e9070-185">Branding.JSLink (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink)
- <span data-ttu-id="e9070-186">Beispiele und Inhalte am https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="e9070-186">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="e9070-187">Gilt für</span><span class="sxs-lookup"><span data-stu-id="e9070-187">Applies to</span></span>
==========
- <span data-ttu-id="e9070-188">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="e9070-188">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="e9070-189">Office 365 dedizierte (D) *teilweise*</span><span class="sxs-lookup"><span data-stu-id="e9070-189">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="e9070-190">SharePoint 2013 lokal – *teilweise*</span><span class="sxs-lookup"><span data-stu-id="e9070-190">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="e9070-191">*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*</span><span class="sxs-lookup"><span data-stu-id="e9070-191">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
