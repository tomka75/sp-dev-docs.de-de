---
title: Barrierefreiheit im SharePoint-Webpartdesign
ms.date: 9/25/2017
ms.openlocfilehash: 55dcf68b350ca7ae004a1caad958f623394551be
ms.sourcegitcommit: b05e9f1edb1a23b07b7986655fac92c24dd62f5a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
<!--Based on how rough this content is in it's current state, i'm going to pull it from this initial release so we can edit and better prepare. -->




# <a name="accessibility-in-sharepoint-web-part-design"></a><span data-ttu-id="23449-102">Barrierefreiheit im SharePoint-Webpartdesign</span><span class="sxs-lookup"><span data-stu-id="23449-102">Accessibility in SharePoint web part design</span></span>

<span data-ttu-id="23449-103">Die Entwicklung eines gleichbleibenden Erlebnisses, bei dem die visuellen, auditiven, körperlichen, kognitiven und sprachlichen Bedürfnisse aller Benutzer erfüllt werden, ist eine wichtige Komponente des SharePoint-Webpartdesigns.</span><span class="sxs-lookup"><span data-stu-id="23449-103">Developing an equal experience that meets all users' unique visual, hearing, dexterity, cognitive, and speech needs is an important component of SharePoint web part design.</span></span> <span data-ttu-id="23449-104">Ein barrierefreies Design bezieht sich nicht nur auf Menschen mit körperlichen Einschränkungen, sondern möglicherweise auch auf situationsbedingte Einschränkungen.</span><span class="sxs-lookup"><span data-stu-id="23449-104">Accessible design applies not only to people with disabilities, but also to potential situational impairments.</span></span> <span data-ttu-id="23449-105">Ein barrierefreies Design ist ein gutes Design.</span><span class="sxs-lookup"><span data-stu-id="23449-105">Accessible design is good design.</span></span>

## <a name="accessibility-guidelines"></a><span data-ttu-id="23449-106">Richtlinien für Eingabehilfen</span><span class="sxs-lookup"><span data-stu-id="23449-106">Accessibility guidelines</span></span>

<!-- Make sure that this is an external resource that folks can access. Original link was to a OneNote file. -->
<span data-ttu-id="23449-107">Alle Microsoft-Produkte müssen die [Microsoft-Eingabehilfenstandards](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Link zu den Microsoft-Eingabehilfenstandards") erfüllen.</span><span class="sxs-lookup"><span data-stu-id="23449-107">All Microsoft products must meet the requirements listed in the [Microsoft Accessibility Standards](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Link to Microsoft Accesssibility Standards").</span></span>  

<!-- Fabric components are not designed to be accessible already? And, shouldn't components that aren't based on Fabric also be accessible? -->

<span data-ttu-id="23449-108">Wenn Sie ein Dialogfeld, eine Dateiauswahl oder eine beliebige andere [Office-UI-Fabric](https://dev.office.com/fabric#/components)-Komponente erstellen, befolgen Sie die Anleitungen in diesem Artikel, um sicherzustellen, dass Ihre Inhalte barrierefrei sind.</span><span class="sxs-lookup"><span data-stu-id="23449-108">If you're building a dialog box, file picker, or any other [Office UI Fabric](https://dev.office.com/fabric#/components) component, follow the guidance in this article to ensure that your content is accessible.</span></span> 

<!-- Not sure why we have that link? It currently goes to the OneNote file. Where is the Common UI Controls content? Is that related to accessibility? -->

[<span data-ttu-id="23449-109">Allgemeine Benutzeroberflächensteuerelemente</span><span class="sxs-lookup"><span data-stu-id="23449-109">Common UI Controls</span></span>](https://microsoft.sharepoint.com/teams/STS/_layouts/OneNote.aspx?id=%2Fteams%2FSTS%2FShared%20Documents%2FSP%20Accessibility%2FAccessibility%20Guidance&wd=target%28Accessibility%20101.one%7C0005C142-938C-4411-B543-B9F4199E19B3%2FEverything%20you%20need%20to%20know%20about%20Accessibility%7CE099AFE3-8804-4E1F-BA50-99493AB8A3D0%2F%29 "Link zu allgemeinen Benutzeroberflächensteuerelementen")

## <a name="accessibility-testing"></a><span data-ttu-id="23449-110">Barrierefreiheitsprüfung</span><span class="sxs-lookup"><span data-stu-id="23449-110">Accessibility testing</span></span>

<!-- FYI, I added links. Can we assume that our target audience uses the Edge browser? -->

<span data-ttu-id="23449-111">Testen Sie Ihr Webpart zunächst mit [Narrator](https://support.microsoft.com/de-DE/help/22798/windows-10-narrator-get-started) und Microsoft Edge, und überprüfen Sie dann das barrierefrei Erlebnis mit [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).</span><span class="sxs-lookup"><span data-stu-id="23449-111">Test your web part first with [Narrator](https://support.microsoft.com/de-DE/help/22798/windows-10-narrator-get-started) and Microsoft Edge, and then verify the accessibility experience with [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).</span></span>

<span data-ttu-id="23449-112">Narrator und Microsoft Edge entsprechen den Standards.</span><span class="sxs-lookup"><span data-stu-id="23449-112">Narrator and Microsoft Edge are standards compliant.</span></span> <span data-ttu-id="23449-113">Wenn Sie die Überprüfung auf diese Weise vornehmen, können Sie Probleme leichter aufdecken und feststellen, ob Ihre Seite die Eingabehilfenstandards erfüllt.</span><span class="sxs-lookup"><span data-stu-id="23449-113">When you test with that combination, you are more likely to find issues, and you can validate that your site meets accessibility standards.</span></span> 

<span data-ttu-id="23449-114">JAWS ist Marktführer auf dem Gebiet der Sprachausgabe.</span><span class="sxs-lookup"><span data-stu-id="23449-114">JAWS is the market leader in screen readers.</span></span> <span data-ttu-id="23449-115">JAWS enthält Features, mit denen Sie die Barrierefreiheit einiger Websites verbessern können, die bei anderen Sprachausgaben nicht so leicht zugänglich sind.</span><span class="sxs-lookup"><span data-stu-id="23449-115">JAWS includes features that can improve the accessibility of some websites that aren't as accessible in other screen readers.</span></span> <span data-ttu-id="23449-116">Daher garantiert ein Test in JAWS möglicherweise nicht, dass Ihre Website alle Barrierefreiheitsanforderungen erfüllt.</span><span class="sxs-lookup"><span data-stu-id="23449-116">Therefore testing in JAWS might not ensure that your site meets all accessibility requirements.</span></span> 
 
<span data-ttu-id="23449-117">Möglicherweise möchten Sie auch testen, welche Kombination von Browser und Sprachausgabe den größten Marktanteil für Ihre Website aufweist.</span><span class="sxs-lookup"><span data-stu-id="23449-117">You might also want to test for whatever combination of browser and screen reader has the greatest market share for your website.</span></span>

<!-- Delete? This doesn't seem like text that should be in externally published docs? 
When suppliers test with JAWS, we ask them to repro identified bugs with Narrator and Edge. In the case a bug does not repro with Narrator/Edge it is sent to Mary Smith who works with VFO for a Jaws specific fix. 
-->

## <a name="keyboard-navigation"></a><span data-ttu-id="23449-118">Tastaturnavigation</span><span class="sxs-lookup"><span data-stu-id="23449-118">Keyboard navigation</span></span>

<!-- Is this section telling people how to navigate via a keyboard, or how to design to optimize for keyboard navigation? If the former, . -->

<span data-ttu-id="23449-119">Für manche Benutzer ist die Navigation einer Website über die Tastatur leichter.</span><span class="sxs-lookup"><span data-stu-id="23449-119">For some users, navigating a site via keyboard is more accessible.</span></span> <span data-ttu-id="23449-120">Erfahrene Benutzer verwenden häufig die Tastaturnavigation.</span><span class="sxs-lookup"><span data-stu-id="23449-120">Power users also often rely on keyboard navigation.</span></span> <span data-ttu-id="23449-121">Verwenden Sie Tastaturkurzbefehle wie Tabs, um zu Steuerelementen der Seite zu wechseln, und verwenden Sie die Pfeiltasten zum Navigieren innerhalb der Steuerelemente.</span><span class="sxs-lookup"><span data-stu-id="23449-121">Use keyboard shortcuts such as tabs to go controls on the page, and use arrow keys to navigate inside controls.</span></span>

### <a name="navigation-between-controls"></a><span data-ttu-id="23449-122">Navigation zwischen Steuerelementen</span><span class="sxs-lookup"><span data-stu-id="23449-122">Navigation between controls</span></span>

<span data-ttu-id="23449-123">Jedes Steuerelement ist ein Tabstopp.</span><span class="sxs-lookup"><span data-stu-id="23449-123">Each control is a tab stop.</span></span> <span data-ttu-id="23449-124">Innerhalb eines Steuerelements gelten die folgenden Regeln:</span><span class="sxs-lookup"><span data-stu-id="23449-124">Within a control, the following rules apply:</span></span>

- <span data-ttu-id="23449-125">Im Allgemeinen ist der erste Tabstopp der obere linke Bereich des Steuerelements.</span><span class="sxs-lookup"><span data-stu-id="23449-125">In general, the first tab stop is the top left area of the control.</span></span> <span data-ttu-id="23449-126">Der letzte Tabstopp ist das untere rechte Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="23449-126">The last tab stop is the bottom right control.</span></span>
- <span data-ttu-id="23449-127">Bei modalen Oberflächen sollte der letzte Tabstopp die Commit-Aktionen umfassen.</span><span class="sxs-lookup"><span data-stu-id="23449-127">For modal surfaces, the last tab stop should be the commit actions.</span></span>
- <span data-ttu-id="23449-128">Bei Listen sollte der erste Tabstopp das erste Element in der Liste, der nächste Tabstopp die Befehle, der nächste die Navigation, der nächste die Einstellungen usw. umfassen.</span><span class="sxs-lookup"><span data-stu-id="23449-128">For lists, the first tab stop should be the first item in the list, the next should be the commands, and then the navigation, settings, and so on.</span></span>

<!-- We should make sure the content in the accessibility topic is accessibible. ;) Please describe the information that the image conveys; something like this (also consider making the image an actual screen shot, that might be more clear):

In the following image:
The first tab is the list item.
The second tab is the command.
The third tab is the navigation.
-->
![Darstellung der Tabstopps einer SharePoint-Seite](https://i.imgur.com/Vn3VosN.png)

### <a name="navigation-within-a-control"></a><span data-ttu-id="23449-130">Navigation innerhalb eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="23449-130">Navigation within a control</span></span>

<span data-ttu-id="23449-131">Sie können die Pfeiltasten verwenden, um zu Objekten eines Steuerelements, z. B. den Optionen in einem Menü, Befehlen in einer Befehlsleiste oder Elementen in einer Liste zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="23449-131">You can use arrow keys to move to items in a control, such as choices in a menu, commands in a command bar, or items in a list.</span></span>

<!-- This image is not very clear. Do you need to have the "blank" list box on the left? -->

![Verwenden der Pfeiltasten zum Navigieren innerhalb eines Steuerelements](https://i.imgur.com/vF0Nk73.png)

### <a name="selecting-the-current-item"></a><span data-ttu-id="23449-133">Auswählen des aktuellen Elements</span><span class="sxs-lookup"><span data-stu-id="23449-133">Deletes the current item.</span></span>

<span data-ttu-id="23449-134">Verwenden Sie die Leertaste oder deaktivieren Sie das derzeit gewählte Element in einem Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="23449-134">Use the space bar to select or deselect the item currently in focus in a control.</span></span>

![Verwenden der Leertaste zum Auswählen eines Elements in einer Liste](https://i.imgur.com/j3fBKPl.png)

### <a name="run-a-control"></a><span data-ttu-id="23449-136">Ausführen eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="23449-136">Run a control</span></span>

<span data-ttu-id="23449-137">Drücken Sie **Enter** oder die Eingabetaste, um ein Steuerelement auszuführen.</span><span class="sxs-lookup"><span data-stu-id="23449-137">Press **Enter** or the return key to run a control.</span></span>

![Drücken von Enter zum Ausführen eines Steuerelements](https://i.imgur.com/s0nMPdT.png)

### <a name="leave-a-control"></a><span data-ttu-id="23449-139">Verlassen eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="23449-139">Leave a control</span></span>

<span data-ttu-id="23449-140">Drücken Sie **Escape**, um ein Steuerelement zu verlassen und zum Container zurückkehren.</span><span class="sxs-lookup"><span data-stu-id="23449-140">Press **Escape** to exit a control and return to the container.</span></span>

![Drücken von Escape, um ein Steuerelement zu verlassen und zum Container zurückkehren](https://i.imgur.com/uD99zIX.png)

### <a name="go-to-the-first-or-last-item"></a><span data-ttu-id="23449-142">Zum ersten bzw. letzten Element wechseln</span><span class="sxs-lookup"><span data-stu-id="23449-142">Go to the first or last item</span></span>

<span data-ttu-id="23449-143">Drücken Sie **POS1** oder **Ende**, um direkt zum ersten oder letzten Element einer Liste, eines Menüs usw. zu springen.</span><span class="sxs-lookup"><span data-stu-id="23449-143">Press **Home** or **End** to go directly to the first or last item in a list, menu, and so on.</span></span>

![Drücken von  POS1 oder Ende, um zum ersten oder letzten Element einer Liste zu springen](https://i.imgur.com/gGKsh74.png)


## <a name="screen-reader-navigation"></a><span data-ttu-id="23449-145">Navigation per Sprachausgabe</span><span class="sxs-lookup"><span data-stu-id="23449-145">Screen reader navigation</span></span>

<span data-ttu-id="23449-146">Benutzer mit Sehschwächen navigieren die Benutzeroberfläche der Website per Sprachausgabe</span><span class="sxs-lookup"><span data-stu-id="23449-146">Users who have vision impairments rely on screen readers to navigate the site UI.</span></span> 

<!-- Narrator isn't a third-party product. This image needs more text/explanation; please also clarify the alt text. Is this section important, or can it be removed, given the previous mention of testing with Narrator and JAWS? Again, the intent/target audience for this information isn't clear - is it for the user, or the designer? Can you explain why this information is important from the designer's POV? -->

![Navigation per Sprachausgabe einer SharePoint-Website](https://i.imgur.com/ar23o3X.png)

## <a name="alt-text-and-transcripts"></a><span data-ttu-id="23449-148">Alternativtext und Transkriptionen</span><span class="sxs-lookup"><span data-stu-id="23449-148">Alt text and transcripts</span></span>

<span data-ttu-id="23449-149">Verwenden Sie Beschreibungen von Bildern, die von der Sprachausgabe verarbeitet werden können.</span><span class="sxs-lookup"><span data-stu-id="23449-149">Use alt text to provide descriptions of images that can be consumed by screen readers.</span></span> <span data-ttu-id="23449-150">Dies ist nützlich Benutzer mit Sehschwächen, die Informationen visuell nicht erfassen können.</span><span class="sxs-lookup"><span data-stu-id="23449-150">This is useful for vision-impaired users who cannot consume information visually.</span></span> <span data-ttu-id="23449-151">Stellen Sie sicher, dass Ihr Alternativtext eine ausführliche Beschreibung enthält, da einige Benutzer eine Sprachausgabe verwenden, um Zugriff auf die Informationen des Bildes zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="23449-151">Make sure that your alt text is descriptive, keeping in mind that some readers are relying on a screen reader to access the information conveyed in the image.</span></span> 

<span data-ttu-id="23449-152">Verwenden Sie nicht nur Farben, um eine Bedeutung zu erklären, sondern auch Formen.</span><span class="sxs-lookup"><span data-stu-id="23449-152">Don't rely only on color to convey meaning; rely on both color and shape.</span></span>

<span data-ttu-id="23449-153">Um eine vollständige Konformität mit den Eingabehilfenstandards zu erreichen, beziehen Sie Alternativtext und eine vollständige Transkription der Audio- und Videoinhalte Ihrer Website mit ein.</span><span class="sxs-lookup"><span data-stu-id="23449-153">To be fully compliant with accessibility standards, include alt text and a complete transcript of audio and video content on your site.</span></span>

## <a name="minimum-readable-contrast"></a><span data-ttu-id="23449-154">Lesbarkeit durch Kontrast</span><span class="sxs-lookup"><span data-stu-id="23449-154">Minimum readable contrast</span></span>

<span data-ttu-id="23449-155">Ein minimaler Kontrast ist dringend erforderlich, damit Benutzer mit Sehschwächen die Inhalte der Seite erfassen können.</span><span class="sxs-lookup"><span data-stu-id="23449-155">A minimum level of contrast is essential to help users with vision impairments consume the content on the page.</span></span> <span data-ttu-id="23449-156">Dies ist ebenfalls wichtig, um eine Lesbarkeit bei schwacher Beleuchtung oder störenden Effekten wie Blendung zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="23449-156">It is also important to aid readability in low light and glare situations.</span></span> 

<!-- Convert this image into a table, for accessibility. ;) -->

![Lesbarkeit durch Kontrast: Neutrale, Theme- und Signalfarben](https://i.imgur.com/L7pSF1w.png)


## <a name="high-contrast"></a><span data-ttu-id="23449-158">Hoher Kontrast</span><span class="sxs-lookup"><span data-stu-id="23449-158">High contrast</span></span>

<span data-ttu-id="23449-159">Verwenden Sie Farben mit hohem Kontrast für die Auswahl von Komponenten und Merkmalen im Internet.</span><span class="sxs-lookup"><span data-stu-id="23449-159">Use high contrast colors as a guide for color choices for components and states on the web.</span></span> <span data-ttu-id="23449-160">Windows-Computer können nur erkennen, ob ein PC mit der Einstellung „Hoher Kontrast“ oder „Hoher Kontrast Weiß“ ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="23449-160">Windows computers only have the ability to detect whether a PC is running high contrast, or high contrast white.</span></span> <span data-ttu-id="23449-161">Verwenden Sie aus diesem Grund die standardmäßige Einstellung „Hoher Kontrast Schwarz“ für alle kontrastreichen, nicht weißen Designs.</span><span class="sxs-lookup"><span data-stu-id="23449-161">For this reason, use the default high contrast black setting for any high contrast, non-white theme.</span></span>

<!-- In the left part of the image, I think the title should be "High Contrast Black". -->

![Einstellungen „Hoher Kontrast Schwarz“ und „Hoher Kontrast Weiß“](https://i.imgur.com/qvTFzd4.png)





