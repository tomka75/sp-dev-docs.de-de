---
title: Barrierefreiheit im SharePoint-Webpartdesign
ms.date: 11/21/2017
ms.openlocfilehash: f308f8d1cbe1fabc274e8c83af9cf1b6e8d43177
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
<!--Based on how rough this content is in it's current state, i'm going to pull it from this initial release so we can edit and better prepare. -->

# <a name="accessibility-in-sharepoint-web-part-design"></a><span data-ttu-id="7be21-102">Barrierefreiheit im SharePoint-Webpartdesign</span><span class="sxs-lookup"><span data-stu-id="7be21-102">Accessibility in SharePoint web part design</span></span>

<span data-ttu-id="7be21-103">Die Entwicklung eines gleichbleibenden Erlebnisses, bei dem die visuellen, auditiven, körperlichen, kognitiven und sprachlichen Bedürfnisse aller Benutzer erfüllt werden, ist eine wichtige Komponente des SharePoint-Webpartdesigns.</span><span class="sxs-lookup"><span data-stu-id="7be21-103">Developing an equal experience that meets all users' unique visual, hearing, dexterity, cognitive, and speech needs is an important component of SharePoint web part design.</span></span> <span data-ttu-id="7be21-104">Ein barrierefreies Design bezieht sich nicht nur auf Menschen mit körperlichen Einschränkungen, sondern möglicherweise auch auf situationsbedingte Einschränkungen.</span><span class="sxs-lookup"><span data-stu-id="7be21-104">Accessible design applies not only to people with disabilities, but also to potential situational impairments.</span></span> <span data-ttu-id="7be21-105">Ein barrierefreies Design ist ein gutes Design.</span><span class="sxs-lookup"><span data-stu-id="7be21-105">Accessible design is good design.</span></span>

## <a name="accessibility-guidelines"></a><span data-ttu-id="7be21-106">Richtlinien für Eingabehilfen</span><span class="sxs-lookup"><span data-stu-id="7be21-106">Accessibility guidelines</span></span>

<!-- Make sure that this is an external resource that folks can access. Original link was to a OneNote file. -->
<span data-ttu-id="7be21-107">Alle Microsoft-Produkte müssen die [Microsoft-Eingabehilfenstandards](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Link zu den Microsoft-Eingabehilfenstandards") erfüllen.</span><span class="sxs-lookup"><span data-stu-id="7be21-107">All Microsoft products must meet the requirements listed in the [Microsoft Accessibility Standards](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Link to Microsoft Accesssibility Standards").</span></span>  

<!-- Fabric components are not designed to be accessible already? And, shouldn't components that aren't based on Fabric also be accessible? -->

<span data-ttu-id="7be21-108">Wenn Sie ein Dialogfeld, eine Dateiauswahl oder eine beliebige andere [Office-UI-Fabric](https://dev.office.com/fabric#/components)-Komponente erstellen, befolgen Sie die Anleitungen in diesem Artikel, um sicherzustellen, dass Ihre Inhalte barrierefrei sind.</span><span class="sxs-lookup"><span data-stu-id="7be21-108">If you're building a dialog box, file picker, or any other [Office UI Fabric](https://dev.office.com/fabric#/components) component, follow the guidance in this article to ensure that your content is accessible.</span></span> 

<!-- Not sure why we have that link? It currently goes to the OneNote file. Where is the Common UI Controls content? Is that related to accessibility? [v-licapu] - I agree; we shouldn't be linking to this unless it's live to external audiences; even I can't access it. I moved it to within the comment: 
[Common UI Controls](https://microsoft.sharepoint.com/teams/STS/_layouts/OneNote.aspx?id=%2Fteams%2FSTS%2FShared%20Documents%2FSP%20Accessibility%2FAccessibility%20Guidance&wd=target%28Accessibility%20101.one%7C0005C142-938C-4411-B543-B9F4199E19B3%2FEverything%20you%20need%20to%20know%20about%20Accessibility%7CE099AFE3-8804-4E1F-BA50-99493AB8A3D0%2F%29 "Link to Common UI Controls") -->

## <a name="accessibility-testing"></a><span data-ttu-id="7be21-109">Barrierefreiheitsprüfung</span><span class="sxs-lookup"><span data-stu-id="7be21-109">Accessibility testing</span></span>

<!-- FYI, I added links. Can we assume that our target audience uses the Edge browser? -->

<span data-ttu-id="7be21-110">Testen Sie Ihr Webpart zunächst mit [Narrator](https://support.microsoft.com/de-DE/help/22798/windows-10-narrator-get-started) und Microsoft Edge, und überprüfen Sie dann das barrierefrei Erlebnis mit [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).</span><span class="sxs-lookup"><span data-stu-id="7be21-110">Test your web part first with [Narrator](https://support.microsoft.com/de-DE/help/22798/windows-10-narrator-get-started) and Microsoft Edge, and then verify the accessibility experience with [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).</span></span>

<span data-ttu-id="7be21-111">Narrator und Microsoft Edge entsprechen den Standards.</span><span class="sxs-lookup"><span data-stu-id="7be21-111">Narrator and Microsoft Edge are standards compliant.</span></span> <span data-ttu-id="7be21-112">Wenn Sie die Überprüfung auf diese Weise vornehmen, können Sie Probleme leichter aufdecken und feststellen, ob Ihre Seite die Eingabehilfenstandards erfüllt.</span><span class="sxs-lookup"><span data-stu-id="7be21-112">When you test with that combination, you are more likely to find issues, and you can validate that your site meets accessibility standards.</span></span> 

<span data-ttu-id="7be21-113">JAWS ist Marktführer auf dem Gebiet der Sprachausgabe.</span><span class="sxs-lookup"><span data-stu-id="7be21-113">JAWS is the market leader in screen readers.</span></span> <span data-ttu-id="7be21-114">JAWS enthält Features, mit denen Sie die Barrierefreiheit einiger Websites verbessern können, die bei anderen Sprachausgaben nicht so leicht zugänglich sind.</span><span class="sxs-lookup"><span data-stu-id="7be21-114">JAWS includes features that can improve the accessibility of some websites that aren't as accessible in other screen readers.</span></span> <span data-ttu-id="7be21-115">Daher garantiert ein Test in JAWS möglicherweise nicht, dass Ihre Website alle Barrierefreiheitsanforderungen erfüllt.</span><span class="sxs-lookup"><span data-stu-id="7be21-115">Therefore testing in JAWS might not ensure that your site meets all accessibility requirements.</span></span> 
 
<span data-ttu-id="7be21-116">Möglicherweise möchten Sie auch testen, welche Kombination von Browser und Sprachausgabe den größten Marktanteil für Ihre Website aufweist.</span><span class="sxs-lookup"><span data-stu-id="7be21-116">You might also want to test for whatever combination of browser and screen reader has the greatest market share for your website.</span></span>

<!-- Delete? This doesn't seem like text that should be in externally published docs? 
When suppliers test with JAWS, we ask them to repro identified bugs with Narrator and Edge. In the case a bug does not repro with Narrator/Edge it is sent to Mary Smith who works with VFO for a Jaws specific fix. 
-->

## <a name="keyboard-navigation"></a><span data-ttu-id="7be21-117">Tastaturnavigation</span><span class="sxs-lookup"><span data-stu-id="7be21-117">Keyboard navigation</span></span>

<!-- Is this section telling people how to navigate via a keyboard, or how to design to optimize for keyboard navigation? If the former, . -->

<span data-ttu-id="7be21-118">Für manche Benutzer ist die Navigation einer Website über die Tastatur leichter.</span><span class="sxs-lookup"><span data-stu-id="7be21-118">For some users, navigating a site via keyboard is more accessible.</span></span> <span data-ttu-id="7be21-119">Erfahrene Benutzer verwenden häufig die Tastaturnavigation.</span><span class="sxs-lookup"><span data-stu-id="7be21-119">Power users also often rely on keyboard navigation.</span></span> <span data-ttu-id="7be21-120">Verwenden Sie Tastaturkurzbefehle wie Tabs, um zu Steuerelementen der Seite zu wechseln, und verwenden Sie die Pfeiltasten zum Navigieren innerhalb der Steuerelemente.</span><span class="sxs-lookup"><span data-stu-id="7be21-120">Use keyboard shortcuts such as tabs to go controls on the page, and use arrow keys to navigate inside controls.</span></span>

### <a name="navigation-between-controls"></a><span data-ttu-id="7be21-121">Navigation zwischen Steuerelementen</span><span class="sxs-lookup"><span data-stu-id="7be21-121">Navigation between controls</span></span>

<span data-ttu-id="7be21-122">Jedes Steuerelement ist ein Tabstopp.</span><span class="sxs-lookup"><span data-stu-id="7be21-122">Each control is a tab stop.</span></span> <span data-ttu-id="7be21-123">Innerhalb eines Steuerelements gelten die folgenden Regeln:</span><span class="sxs-lookup"><span data-stu-id="7be21-123">Within a control, the following rules apply:</span></span>

- <span data-ttu-id="7be21-124">Im Allgemeinen ist der erste Tabstopp der obere linke Bereich des Steuerelements.</span><span class="sxs-lookup"><span data-stu-id="7be21-124">In general, the first tab stop is the top left area of the control.</span></span> <span data-ttu-id="7be21-125">Der letzte Tabstopp ist das untere rechte Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="7be21-125">The last tab stop is the bottom right control.</span></span>
- <span data-ttu-id="7be21-126">Bei modalen Oberflächen sollte der letzte Tabstopp die Commit-Aktionen umfassen.</span><span class="sxs-lookup"><span data-stu-id="7be21-126">For modal surfaces, the last tab stop should be the commit actions.</span></span>
- <span data-ttu-id="7be21-127">Bei Listen sollte der erste Tabstopp das erste Element in der Liste, der nächste Tabstopp die Befehle, der nächste die Navigation, der nächste die Einstellungen usw. umfassen.</span><span class="sxs-lookup"><span data-stu-id="7be21-127">For lists, the first tab stop should be the first item in the list, the next should be the commands, and then the navigation, settings, and so on.</span></span>

<!-- We should make sure the content in the accessibility topic is accessibible. ;) Please describe the information that the image conveys; something like this (also consider making the image an actual screen shot, that might be more clear):

In the following image:
The first tab is the list item.
The second tab is the command.
The third tab is the navigation.
-->

<span data-ttu-id="7be21-128">*Abbildung 1: Tabstopps einer SharePoint-Seite*</span><span class="sxs-lookup"><span data-stu-id="7be21-128">*Figure 1. The tab stops on a SharePoint page*</span></span>

![Darstellung der Tabstopps einer SharePoint-Seite](https://i.imgur.com/Vn3VosN.png)

### <a name="navigation-within-a-control"></a><span data-ttu-id="7be21-130">Navigation innerhalb eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="7be21-130">Navigation within a control</span></span>

<span data-ttu-id="7be21-131">Sie können die Pfeiltasten verwenden, um zu Objekten eines Steuerelements, z. B. den Optionen in einem Menü, Befehlen in einer Befehlsleiste oder Elementen in einer Liste zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="7be21-131">You can use arrow keys to move to items in a control, such as choices in a menu, commands in a command bar, or items in a list.</span></span>

<!-- This image is not very clear. Do you need to have the "blank" list box on the left? -->

<span data-ttu-id="7be21-132">*Abbildung 2: Verwenden der Pfeiltasten zum Navigieren innerhalb eines Steuerelements*</span><span class="sxs-lookup"><span data-stu-id="7be21-132">*Figure 2. Using arrow keys to navigate within a control*</span></span>

![Verwenden der Pfeiltasten zum Navigieren innerhalb eines Steuerelements](https://i.imgur.com/vF0Nk73.png)

### <a name="selecting-the-current-item"></a><span data-ttu-id="7be21-134">Auswählen des aktuellen Elements</span><span class="sxs-lookup"><span data-stu-id="7be21-134">Selecting the current item</span></span>

<span data-ttu-id="7be21-135">Verwenden Sie die Leertaste oder deaktivieren Sie das derzeit gewählte Element in einem Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="7be21-135">Use the space bar to select or deselect the item currently in focus in a control.</span></span>

<span data-ttu-id="7be21-136">*Abbildung 3: Verwenden der Leertaste zum Auswählen eines Elements in einer Liste*</span><span class="sxs-lookup"><span data-stu-id="7be21-136">*Figure 3. Using the space bar to select an item in a list*</span></span>

![Verwenden der Leertaste zum Auswählen eines Elements in einer Liste](https://i.imgur.com/j3fBKPl.png)

### <a name="run-a-control"></a><span data-ttu-id="7be21-138">Ausführen eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="7be21-138">Run a control</span></span>

<span data-ttu-id="7be21-139">Drücken Sie die EINGABETASTE, um ein Steuerelement auszuführen.</span><span class="sxs-lookup"><span data-stu-id="7be21-139">Select Enter or the return key to run a control.</span></span>

<span data-ttu-id="7be21-140">*Abbildung 4: Drücken der EINGABETASTE zum Ausführen eines Steuerelements*</span><span class="sxs-lookup"><span data-stu-id="7be21-140">*Figure 4. Selecting Enter to run a control*</span></span>

![Drücken der EINGABTASTE zum Ausführen eines Steuerelements](https://i.imgur.com/s0nMPdT.png)

### <a name="leave-a-control"></a><span data-ttu-id="7be21-142">Verlassen eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="7be21-142">Leave a control</span></span>

<span data-ttu-id="7be21-143">Drücken Sie die **ESC-Taste**, um ein Steuerelement zu verlassen und zum Container zurückkehren.</span><span class="sxs-lookup"><span data-stu-id="7be21-143">Select **Escape** to exit a control and return to the container.</span></span>

<span data-ttu-id="7be21-144">*Abbildung 5: Drücken der ESC-Taste zum Verlassen eines Steuerelements und zum Zurückkehren zum Container*</span><span class="sxs-lookup"><span data-stu-id="7be21-144">*Figure 5. Selecting Escape to leave a control and return to the container*</span></span>

![Drücken der ESC-Taste zum Verlassen eines Steuerelements und zum Zurückkehren zum Container](https://i.imgur.com/uD99zIX.png)

### <a name="go-to-the-first-or-last-item"></a><span data-ttu-id="7be21-146">Wechseln zum ersten bzw. letzten Element</span><span class="sxs-lookup"><span data-stu-id="7be21-146">Go to the first or last item</span></span>

<span data-ttu-id="7be21-147">Drücken Sie **POS1** oder **Ende**, um direkt zum ersten oder letzten Element einer Liste, eines Menüs usw. zu springen.</span><span class="sxs-lookup"><span data-stu-id="7be21-147">Select **Home** or **End** to go directly to the first or last item in a list, menu, and so on.</span></span>

<span data-ttu-id="7be21-148">*Abbildung 6: Drücken von POS1 oder Ende, um zum ersten oder letzten Element einer Liste zu springen*</span><span class="sxs-lookup"><span data-stu-id="7be21-148">*Figure 6. Selecting Home or End to go to the first or last item in a list*</span></span>

![Drücken von POS1 oder Ende, um zum ersten oder letzten Element einer Liste zu springen](https://i.imgur.com/gGKsh74.png)


## <a name="screen-reader-navigation"></a><span data-ttu-id="7be21-150">Navigation per Sprachausgabe</span><span class="sxs-lookup"><span data-stu-id="7be21-150">Screen reader navigation</span></span>

<span data-ttu-id="7be21-151">Benutzer mit Sehschwächen navigieren die Benutzeroberfläche der Website per Sprachausgabe</span><span class="sxs-lookup"><span data-stu-id="7be21-151">Users who have vision impairments rely on screen readers to navigate the site UI.</span></span> 

<!-- Narrator isn't a third-party product. This image needs more text/explanation; please also clarify the alt text. Is this section important, or can it be removed, given the previous mention of testing with Narrator and JAWS? Again, the intent/target audience for this information isn't clear - is it for the user, or the designer? Can you explain why this information is important from the designer's POV? -->

<span data-ttu-id="7be21-152">*Abbildung 7: Navigation per Sprachausgabe einer SharePoint-Website*</span><span class="sxs-lookup"><span data-stu-id="7be21-152">*Figure 7. Screen reader navigation of a SharePoint page*</span></span>

![Navigation per Sprachausgabe einer SharePoint-Website](https://i.imgur.com/ar23o3X.png)

## <a name="alt-text-and-transcripts"></a><span data-ttu-id="7be21-154">Alternativtext und Transkriptionen</span><span class="sxs-lookup"><span data-stu-id="7be21-154">Alt text and transcripts</span></span>

<span data-ttu-id="7be21-155">Verwenden Sie Beschreibungen von Bildern, die von der Sprachausgabe verarbeitet werden können.</span><span class="sxs-lookup"><span data-stu-id="7be21-155">Use alt text to provide descriptions of images that can be consumed by screen readers.</span></span> <span data-ttu-id="7be21-156">Dies ist nützlich Benutzer mit Sehschwächen, die Informationen visuell nicht erfassen können.</span><span class="sxs-lookup"><span data-stu-id="7be21-156">This is useful for vision-impaired users who cannot consume information visually.</span></span> <span data-ttu-id="7be21-157">Stellen Sie sicher, dass Ihr Alternativtext eine ausführliche Beschreibung enthält, da einige Benutzer eine Sprachausgabe verwenden, um Zugriff auf die Informationen des Bildes zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="7be21-157">Make sure that your alt text is descriptive, keeping in mind that some readers are relying on a screen reader to access the information conveyed in the image.</span></span> 

<span data-ttu-id="7be21-158">Verwenden Sie nicht nur Farben, um eine Bedeutung zu erklären, sondern auch Formen.</span><span class="sxs-lookup"><span data-stu-id="7be21-158">Don't rely only on color to convey meaning; rely on both color and shape.</span></span>

<span data-ttu-id="7be21-159">Um eine vollständige Konformität mit den Eingabehilfenstandards zu erreichen, beziehen Sie Alternativtext und eine vollständige Transkription der Audio- und Videoinhalte Ihrer Website mit ein.</span><span class="sxs-lookup"><span data-stu-id="7be21-159">To be fully compliant with accessibility standards, include alt text and a complete transcript of audio and video content on your site.</span></span>

## <a name="minimum-readable-contrast"></a><span data-ttu-id="7be21-160">Lesbarkeit durch Kontrast</span><span class="sxs-lookup"><span data-stu-id="7be21-160">Minimum readable contrast</span></span>

<span data-ttu-id="7be21-161">Ein minimaler Kontrast ist dringend erforderlich, damit Benutzer mit Sehschwächen die Inhalte der Seite erfassen können.</span><span class="sxs-lookup"><span data-stu-id="7be21-161">A minimum level of contrast is essential to help users with vision impairments consume the content on the page.</span></span> <span data-ttu-id="7be21-162">Dies ist ebenfalls wichtig, um eine Lesbarkeit bei schwacher Beleuchtung oder störenden Effekten wie Blendung zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="7be21-162">It is also important to aid readability in low light and glare situations.</span></span> 

<!-- Convert this image into a table, for accessibility. ;) -->
<!-- ![Neutral, Theme, and Alert colors for minimum readable contrast](https://i.imgur.com/L7pSF1w.png)-->

![Farben für Lesbarkeit durch Kontrast](../images/wcag-2aa-compliance-colors.png)

### <a name="theme-colors-blue-and-neutral-colors"></a><span data-ttu-id="7be21-164">Designfarben (Blau) und neutrale Farben</span><span class="sxs-lookup"><span data-stu-id="7be21-164">Theme colors (Blue) and neutral colors</span></span>

<table>
<tr>
<td style="color:white; background-color:#004578"><span data-ttu-id="7be21-165">themeDarker: #004578</span><span class="sxs-lookup"><span data-stu-id="7be21-165">themeDarker: #004578</span></span></td>
<td style="color:white; background-color:#000000"><span data-ttu-id="7be21-166">black: #000000</span><span class="sxs-lookup"><span data-stu-id="7be21-166">black: #000000</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#005a9e"><span data-ttu-id="7be21-167">themeDark: #005a9e</span><span class="sxs-lookup"><span data-stu-id="7be21-167">themeDark: #005a9e</span></span></td>
<td style="color:white; background-color:#212121"><span data-ttu-id="7be21-168">neutralDark: #212121</span><span class="sxs-lookup"><span data-stu-id="7be21-168">neutralDark: #212121</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#106ebe"><span data-ttu-id="7be21-169">themeDarkAlt: #106ebe</span><span class="sxs-lookup"><span data-stu-id="7be21-169">themeDarkAlt: #106ebe</span></span></td>
<td style="color:white; background-color:#333"><span data-ttu-id="7be21-170">neutralPrimary: #333</span><span class="sxs-lookup"><span data-stu-id="7be21-170">neutralPrimary: #333</span></span></td>
</tr>
<tr>
<td rowspan="3" style="font-weight:bold; vertical-align:middle; color:white; background-color:#0078d7"><span data-ttu-id="7be21-171">themePrimary: #0078d7</span><span class="sxs-lookup"><span data-stu-id="7be21-171">themePrimary: #0078d7</span></span></td>
<td style="color:white; background-color:#3c3c3c"><span data-ttu-id="7be21-172">neutralPrimaryAlt: #3c3c3c</span><span class="sxs-lookup"><span data-stu-id="7be21-172">neutralPrimaryAlt: #3c3c3c</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#666666"><span data-ttu-id="7be21-173">neutralSecondary: #666666</span><span class="sxs-lookup"><span data-stu-id="7be21-173">neutralSecondary: #666666</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#a6a6a6"><span data-ttu-id="7be21-174">neutralTertiary: #a6a6a6</span><span class="sxs-lookup"><span data-stu-id="7be21-174">neutralTertiary: #a6a6a6</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#2b88d8"><span data-ttu-id="7be21-175">themeSecondary: #2b88d8</span><span class="sxs-lookup"><span data-stu-id="7be21-175">themeSecondary: #2b88d8</span></span></td>
<td style="color:black; background-color:#c8c8c8"><span data-ttu-id="7be21-176">neutralTertiaryAlt: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="7be21-176">neutralTertiaryAlt: #c8c8c8</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#71afe5"><span data-ttu-id="7be21-177">themeTertiary: #71afe5</span><span class="sxs-lookup"><span data-stu-id="7be21-177">themeTertiary: #71afe5</span></span></td>
<td style="color:black; background-color:#eaeaea"><span data-ttu-id="7be21-178">neutralLight: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="7be21-178">neutralLight: #eaeaea</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#c7e0f4"><span data-ttu-id="7be21-179">themeLight: #c7e0f4</span><span class="sxs-lookup"><span data-stu-id="7be21-179">themeLight: #c7e0f4</span></span></td>
<td style="color:black; background-color:#f4f4f4"><span data-ttu-id="7be21-180">neutralLighter: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="7be21-180">neutralLighter: #f4f4f4</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#deecf9"><span data-ttu-id="7be21-181">themeLighter: #deecf9</span><span class="sxs-lookup"><span data-stu-id="7be21-181">themeLighter: #deecf9</span></span></td>
<td style="color:black; background-color:#f8f8f8"><span data-ttu-id="7be21-182">neutralLighterAlt: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="7be21-182">neutralLighterAlt: #f8f8f8</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#eff6fc"><span data-ttu-id="7be21-183">themeLighterAlt: #eff6fc</span><span class="sxs-lookup"><span data-stu-id="7be21-183">themeLighterAlt: #eff6fc</span></span></td>
<td style="color:black; background-color:#fff"><span data-ttu-id="7be21-184">white: #fff</span><span class="sxs-lookup"><span data-stu-id="7be21-184">white: #fff</span></span></td>
</tr>
</table>

### <a name="alert-colors"></a><span data-ttu-id="7be21-185">Farben für Warnungen</span><span class="sxs-lookup"><span data-stu-id="7be21-185">Alert colors</span></span>

<table>
<tr>
<td style="color:white; background-color:#952226"><span data-ttu-id="7be21-186">themeDark: #952226</span><span class="sxs-lookup"><span data-stu-id="7be21-186">themeDark: #952226</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#f6d6d8"><span data-ttu-id="7be21-187">themeLight: #f6d6d8</span><span class="sxs-lookup"><span data-stu-id="7be21-187">themeLight: #f6d6d8</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#e55c12"><span data-ttu-id="7be21-188">themeSecondary: #e55c12</span><span class="sxs-lookup"><span data-stu-id="7be21-188">themeSecondary: #e55c12</span></span></td>
</tr>
</table>

<br/>

<table>
<tr>
<td style="color:white; background-color:#0f7c39"><span data-ttu-id="7be21-189">themeDarkAlt: #0f7c39</span><span class="sxs-lookup"><span data-stu-id="7be21-189">themeDarkAlt: #0f7c39</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#bff7d5"><span data-ttu-id="7be21-190">themeLight: #bff7d5</span><span class="sxs-lookup"><span data-stu-id="7be21-190">themeLight: #bff7d5</span></span></td>
</tr>
</table>

## <a name="high-contrast"></a><span data-ttu-id="7be21-191">Hoher Kontrast</span><span class="sxs-lookup"><span data-stu-id="7be21-191">High contrast</span></span>

<span data-ttu-id="7be21-192">Verwenden Sie Farben mit hohem Kontrast für die Auswahl von Komponenten und Merkmalen im Internet.</span><span class="sxs-lookup"><span data-stu-id="7be21-192">Use high contrast colors as a guide for color choices for components and states on the web.</span></span> <span data-ttu-id="7be21-193">Windows-Computer können nur erkennen, ob ein PC mit der Einstellung „Hoher Kontrast“ oder „Hoher Kontrast Weiß“ ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="7be21-193">Windows computers only have the ability to detect whether a PC is running high contrast, or high contrast white.</span></span> <span data-ttu-id="7be21-194">Verwenden Sie aus diesem Grund die standardmäßige Einstellung „Hoher Kontrast Schwarz“ für alle kontrastreichen, nicht weißen Designs.</span><span class="sxs-lookup"><span data-stu-id="7be21-194">For this reason, use the default high contrast black setting for any high contrast, non-white theme.</span></span>

<!-- In the left part of the image, I think the title should be "High Contrast Black". -->

<span data-ttu-id="7be21-195">*Abbildung 8: Einstellungen „Hoher Kontrast Schwarz“ und „Hoher Kontrast Weiß“*</span><span class="sxs-lookup"><span data-stu-id="7be21-195">*Figure 8. High contrast black and high contrast white settings*</span></span>

![Einstellungen „Hoher Kontrast Schwarz“ und „Hoher Kontrast Weiß“](https://i.imgur.com/qvTFzd4.png)





