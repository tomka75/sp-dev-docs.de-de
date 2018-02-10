---
title: Barrierefreiheit im SharePoint-Webpartdesign
description: "Richtlinien für Barrierefreiheit in Webparts"
ms.date: 01/23/2018
ms.openlocfilehash: 0a1b4aa88771b07b9f4060906ddf4062d2281dcd
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
<!--Based on how rough this content is in its current state, i'm going to pull it from this initial release so we can edit and better prepare. -->

# <a name="accessibility-in-sharepoint-web-part-design"></a><span data-ttu-id="90e67-103">Barrierefreiheit im SharePoint-Webpartdesign</span><span class="sxs-lookup"><span data-stu-id="90e67-103">Accessibility in SharePoint web part design</span></span>

<span data-ttu-id="90e67-104">Die Entwicklung eines gleichbleibenden Erlebnisses, bei dem die visuellen, auditiven, körperlichen, kognitiven und sprachlichen Bedürfnisse aller Benutzer erfüllt werden, ist eine wichtige Komponente des SharePoint-Webpartdesigns.</span><span class="sxs-lookup"><span data-stu-id="90e67-104">Developing an equal experience that meets all users' unique visual, hearing, dexterity, cognitive, and speech needs is an important component of SharePoint web part design.</span></span> <span data-ttu-id="90e67-105">Ein barrierefreies Design bezieht sich nicht nur auf Menschen mit körperlichen Einschränkungen, sondern möglicherweise auch auf situationsbedingte Einschränkungen.</span><span class="sxs-lookup"><span data-stu-id="90e67-105">Accessible design applies not only to people with disabilities, but also to potential situational impairments.</span></span> <span data-ttu-id="90e67-106">Ein barrierefreies Design ist ein gutes Design.</span><span class="sxs-lookup"><span data-stu-id="90e67-106">Accessible design is good design.</span></span>

## <a name="accessibility-guidelines"></a><span data-ttu-id="90e67-107">Richtlinien für Eingabehilfen</span><span class="sxs-lookup"><span data-stu-id="90e67-107">Accessibility guidelines</span></span>

<!-- Make sure that this is an external resource that folks can access. Original link was to a OneNote file. -->
<span data-ttu-id="90e67-108">Alle Microsoft-Produkte müssen die [Microsoft-Eingabehilfenstandards](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Link zu den Microsoft-Eingabehilfenstandards") erfüllen.</span><span class="sxs-lookup"><span data-stu-id="90e67-108">All Microsoft products must meet the requirements listed in the [Microsoft Accessibility Standards](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Link to Microsoft Accesssibility Standards").</span></span>  

<!-- Fabric components are not designed to be accessible already? And, shouldn't components that aren't based on Fabric also be accessible? -->

<span data-ttu-id="90e67-109">Wenn Sie ein Dialogfeld, eine Dateiauswahl oder eine beliebige andere [Office-UI-Fabric](https://developer.microsoft.com/de-DE/fabric#/components)-Komponente erstellen, befolgen Sie die Anleitungen in diesem Artikel, um sicherzustellen, dass Ihre Inhalte barrierefrei sind.</span><span class="sxs-lookup"><span data-stu-id="90e67-109">If you're building a dialog box, file picker, or any other [Office UI Fabric](https://developer.microsoft.com/de-DE/fabric#/components) component, follow the guidance in this article to ensure that your content is accessible.</span></span> 

<!-- Not sure why we have that link? It currently goes to the OneNote file. Where is the Common UI Controls content? Is that related to accessibility? [v-licapu] - I agree; we shouldn't be linking to this unless it's live to external audiences; even I can't access it. I moved it to within the comment: 
[Common UI Controls](https://microsoft.sharepoint.com/teams/STS/_layouts/OneNote.aspx?id=%2Fteams%2FSTS%2FShared%20Documents%2FSP%20Accessibility%2FAccessibility%20Guidance&wd=target%28Accessibility%20101.one%7C0005C142-938C-4411-B543-B9F4199E19B3%2FEverything%20you%20need%20to%20know%20about%20Accessibility%7CE099AFE3-8804-4E1F-BA50-99493AB8A3D0%2F%29 "Link to Common UI Controls") -->

## <a name="accessibility-testing"></a><span data-ttu-id="90e67-110">Barrierefreiheitsprüfung</span><span class="sxs-lookup"><span data-stu-id="90e67-110">Accessibility testing</span></span>

<!-- FYI, I added links. Can we assume that our target audience uses the Edge browser? -->

<span data-ttu-id="90e67-111">Testen Sie Ihr Webpart zunächst mit [Narrator](https://support.microsoft.com/de-DE/help/22798/windows-10-narrator-get-started) und Microsoft Edge, und überprüfen Sie dann das barrierefreie Erlebnis mit [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).</span><span class="sxs-lookup"><span data-stu-id="90e67-111">Test your web part first with [Narrator](https://support.microsoft.com/de-DE/help/22798/windows-10-narrator-get-started) and Microsoft Edge, and then verify the accessibility experience with [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).</span></span>

<span data-ttu-id="90e67-112">Narrator und Microsoft Edge entsprechen den Standards.</span><span class="sxs-lookup"><span data-stu-id="90e67-112">Narrator and Microsoft Edge are standards compliant.</span></span> <span data-ttu-id="90e67-113">Wenn Sie die Überprüfung auf diese Weise vornehmen, können Sie Probleme leichter aufdecken und feststellen, ob Ihre Seite die Eingabehilfenstandards erfüllt.</span><span class="sxs-lookup"><span data-stu-id="90e67-113">When you test with that combination, you are more likely to find issues, and you can validate that your site meets accessibility standards.</span></span> 

<span data-ttu-id="90e67-114">JAWS ist Marktführer auf dem Gebiet der Sprachausgabe.</span><span class="sxs-lookup"><span data-stu-id="90e67-114">JAWS is the market leader in screen readers.</span></span> <span data-ttu-id="90e67-115">JAWS enthält Features, mit denen Sie die Barrierefreiheit einiger Websites verbessern können, die bei anderen Sprachausgaben nicht so leicht zugänglich sind.</span><span class="sxs-lookup"><span data-stu-id="90e67-115">JAWS includes features that can improve the accessibility of some websites that aren't as accessible in other screen readers.</span></span> <span data-ttu-id="90e67-116">Daher garantiert ein Test in JAWS möglicherweise nicht, dass Ihre Website alle Barrierefreiheitsanforderungen erfüllt.</span><span class="sxs-lookup"><span data-stu-id="90e67-116">Therefore testing in JAWS might not ensure that your site meets all accessibility requirements.</span></span> 
 
<span data-ttu-id="90e67-117">Möglicherweise möchten Sie auch testen, welche Kombination von Browser und Sprachausgabe den größten Marktanteil für Ihre Website aufweist.</span><span class="sxs-lookup"><span data-stu-id="90e67-117">You might also want to test for whatever combination of browser and screen reader has the greatest market share for your website.</span></span>

<!-- Delete? This doesn't seem like text that should be in externally published docs? 
When suppliers test with JAWS, we ask them to repro identified bugs with Narrator and Edge. In the case a bug does not repro with Narrator/Edge it is sent to Mary Smith who works with VFO for a Jaws specific fix. 
-->

## <a name="keyboard-navigation"></a><span data-ttu-id="90e67-118">Tastaturnavigation</span><span class="sxs-lookup"><span data-stu-id="90e67-118">Keyboard navigation</span></span>

<!-- Is this section telling people how to navigate via a keyboard, or how to design to optimize for keyboard navigation? If the former, . -->

<span data-ttu-id="90e67-119">Für manche Benutzer ist die Navigation einer Website über die Tastatur leichter.</span><span class="sxs-lookup"><span data-stu-id="90e67-119">For some users, navigating a site via keyboard is more accessible.</span></span> <span data-ttu-id="90e67-120">Erfahrene Benutzer verwenden häufig die Tastaturnavigation.</span><span class="sxs-lookup"><span data-stu-id="90e67-120">Power users also often rely on keyboard navigation.</span></span> <span data-ttu-id="90e67-121">Verwenden Sie Tastaturkurzbefehle wie Tabs, um zu Steuerelementen der Seite zu wechseln, und verwenden Sie die Pfeiltasten zum Navigieren innerhalb der Steuerelemente.</span><span class="sxs-lookup"><span data-stu-id="90e67-121">Use keyboard shortcuts such as tabs to go controls on the page, and use arrow keys to navigate inside controls.</span></span>

### <a name="navigation-between-controls"></a><span data-ttu-id="90e67-122">Navigation zwischen Steuerelementen</span><span class="sxs-lookup"><span data-stu-id="90e67-122">Navigation between controls</span></span>

<span data-ttu-id="90e67-123">Jedes Steuerelement ist ein Tabstopp.</span><span class="sxs-lookup"><span data-stu-id="90e67-123">Each control is a tab stop.</span></span> <span data-ttu-id="90e67-124">Innerhalb eines Steuerelements gelten die folgenden Regeln:</span><span class="sxs-lookup"><span data-stu-id="90e67-124">Within a control, the following rules apply:</span></span>

- <span data-ttu-id="90e67-125">Im Allgemeinen ist der erste Tabstopp der obere linke Bereich des Steuerelements.</span><span class="sxs-lookup"><span data-stu-id="90e67-125">In general, the first tab stop is the top left area of the control.</span></span> <span data-ttu-id="90e67-126">Der letzte Tabstopp ist das untere rechte Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="90e67-126">The last tab stop is the bottom right control.</span></span>
- <span data-ttu-id="90e67-127">Bei modalen Oberflächen sollte der letzte Tabstopp die Commit-Aktionen umfassen.</span><span class="sxs-lookup"><span data-stu-id="90e67-127">For modal surfaces, the last tab stop should be the commit actions.</span></span>
- <span data-ttu-id="90e67-128">Bei Listen sollte der erste Tabstopp das erste Element in der Liste, der nächste Tabstopp die Befehle, der nächste die Navigation, der nächste die Einstellungen usw. umfassen.</span><span class="sxs-lookup"><span data-stu-id="90e67-128">For lists, the first tab stop should be the first item in the list, the next should be the commands, and then the navigation, settings, and so on.</span></span>

<!-- We should make sure the content in the accessibility topic is accessibible. ;) Please describe the information that the image conveys; something like this (also consider making the image an actual screen shot, that might be more clear):

In the following image:
The first tab is the list item.
The second tab is the command.
The third tab is the navigation.
-->


![Darstellung der Tabstopps einer SharePoint-Seite](https://i.imgur.com/Vn3VosN.png)

<br/>

### <a name="navigation-within-a-control"></a><span data-ttu-id="90e67-130">Navigation innerhalb eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="90e67-130">Navigation within a control</span></span>

<span data-ttu-id="90e67-131">Sie können die Pfeiltasten verwenden, um zu Objekten eines Steuerelements, z. B. den Optionen in einem Menü, Befehlen in einer Befehlsleiste oder Elementen in einer Liste zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="90e67-131">You can use arrow keys to move to items in a control, such as choices in a menu, commands in a command bar, or items in a list.</span></span>

<!-- This image is not very clear. Do you need to have the "blank" list box on the left? -->

![Verwenden der Pfeiltasten zum Navigieren innerhalb eines Steuerelements](https://i.imgur.com/vF0Nk73.png)

<br/>

### <a name="selecting-the-current-item"></a><span data-ttu-id="90e67-133">Auswählen des aktuellen Elements</span><span class="sxs-lookup"><span data-stu-id="90e67-133">Selecting the current item</span></span>

<span data-ttu-id="90e67-134">Verwenden Sie die Leertaste oder deaktivieren Sie das derzeit gewählte Element in einem Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="90e67-134">Use the space bar to select or deselect the item currently in focus in a control.</span></span>

![Verwenden der Leertaste zum Auswählen eines Elements in einer Liste](https://i.imgur.com/j3fBKPl.png)

<br/>

### <a name="run-a-control"></a><span data-ttu-id="90e67-136">Ausführen eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="90e67-136">Run a control</span></span>

<span data-ttu-id="90e67-137">Drücken Sie die EINGABETASTE, um ein Steuerelement auszuführen.</span><span class="sxs-lookup"><span data-stu-id="90e67-137">Select Enter or the return key to run a control.</span></span>

![Drücken der EINGABTASTE zum Ausführen eines Steuerelements](https://i.imgur.com/s0nMPdT.png)

<br/>

### <a name="leave-a-control"></a><span data-ttu-id="90e67-139">Verlassen eines Steuerelements</span><span class="sxs-lookup"><span data-stu-id="90e67-139">Leave a control</span></span>

<span data-ttu-id="90e67-140">Drücken Sie die **ESC-Taste**, um ein Steuerelement zu verlassen und zum Container zurückkehren.</span><span class="sxs-lookup"><span data-stu-id="90e67-140">Select **Escape** to exit a control and return to the container.</span></span>

![Drücken der ESC-Taste zum Verlassen eines Steuerelements und zum Zurückkehren zum Container](https://i.imgur.com/uD99zIX.png)

<br/>

### <a name="go-to-the-first-or-last-item"></a><span data-ttu-id="90e67-142">Wechseln zum ersten bzw. letzten Element</span><span class="sxs-lookup"><span data-stu-id="90e67-142">Go to the first or last item</span></span>

<span data-ttu-id="90e67-143">Drücken Sie **POS1** oder **Ende**, um direkt zum ersten oder letzten Element einer Liste, eines Menüs usw. zu springen.</span><span class="sxs-lookup"><span data-stu-id="90e67-143">Select **Home** or **End** to go directly to the first or last item in a list, menu, and so on.</span></span>

![Drücken von POS1 oder Ende, um zum ersten oder letzten Element einer Liste zu springen](https://i.imgur.com/gGKsh74.png)

<br/>

## <a name="screen-reader-navigation"></a><span data-ttu-id="90e67-145">Navigation per Sprachausgabe</span><span class="sxs-lookup"><span data-stu-id="90e67-145">Screen reader navigation</span></span>

<span data-ttu-id="90e67-146">Benutzer mit Sehschwächen navigieren die Benutzeroberfläche der Website per Sprachausgabe</span><span class="sxs-lookup"><span data-stu-id="90e67-146">Users who have vision impairments rely on screen readers to navigate the site UI.</span></span> 

<!-- Narrator isn't a third-party product. This image needs more text/explanation; please also clarify the alt text. Is this section important, or can it be removed, given the previous mention of testing with Narrator and JAWS? Again, the intent/target audience for this information isn't clear - is it for the user, or the designer? Can you explain why this information is important from the designer's POV? -->

![Navigation per Sprachausgabe einer SharePoint-Website](https://i.imgur.com/ar23o3X.png)

## <a name="alt-text-and-transcripts"></a><span data-ttu-id="90e67-148">Alternativtext und Transkriptionen</span><span class="sxs-lookup"><span data-stu-id="90e67-148">Alt text and transcripts</span></span>

<span data-ttu-id="90e67-149">Verwenden Sie Beschreibungen von Bildern, die von der Sprachausgabe verarbeitet werden können.</span><span class="sxs-lookup"><span data-stu-id="90e67-149">Use alt text to provide descriptions of images that can be consumed by screen readers.</span></span> <span data-ttu-id="90e67-150">Dies ist nützlich Benutzer mit Sehschwächen, die Informationen visuell nicht erfassen können.</span><span class="sxs-lookup"><span data-stu-id="90e67-150">This is useful for vision-impaired users who cannot consume information visually.</span></span> <span data-ttu-id="90e67-151">Stellen Sie sicher, dass Ihr Alternativtext eine ausführliche Beschreibung enthält, da einige Benutzer eine Sprachausgabe verwenden, um Zugriff auf die Informationen des Bildes zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="90e67-151">Make sure that your alt text is descriptive, keeping in mind that some readers are relying on a screen reader to access the information conveyed in the image.</span></span> 

<span data-ttu-id="90e67-152">Verwenden Sie nicht nur Farben, um eine Bedeutung zu erklären, sondern auch Formen.</span><span class="sxs-lookup"><span data-stu-id="90e67-152">Don't rely only on color to convey meaning; rely on both color and shape.</span></span>

<span data-ttu-id="90e67-153">Um eine vollständige Konformität mit den Eingabehilfenstandards zu erreichen, beziehen Sie Alternativtext und eine vollständige Transkription der Audio- und Videoinhalte Ihrer Website mit ein.</span><span class="sxs-lookup"><span data-stu-id="90e67-153">To be fully compliant with accessibility standards, include alt text and a complete transcript of audio and video content on your site.</span></span>

## <a name="minimum-readable-contrast"></a><span data-ttu-id="90e67-154">Lesbarkeit durch Kontrast</span><span class="sxs-lookup"><span data-stu-id="90e67-154">Minimum readable contrast</span></span>

<span data-ttu-id="90e67-155">Ein minimaler Kontrast ist dringend erforderlich, damit Benutzer mit Sehschwächen die Inhalte der Seite erfassen können.</span><span class="sxs-lookup"><span data-stu-id="90e67-155">A minimum level of contrast is essential to help users with vision impairments consume the content on the page.</span></span> <span data-ttu-id="90e67-156">Dies ist ebenfalls wichtig, um eine Lesbarkeit bei schwacher Beleuchtung oder störenden Effekten wie Blendung zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="90e67-156">It is also important to aid readability in low light and glare situations.</span></span> 

<!--Original image ![Neutral, Theme, and Alert colors for minimum readable contrast](https://i.imgur.com/L7pSF1w.png)-->

![Farben für Lesbarkeit durch Kontrast](../images/wcag-2aa-compliance-colors.png)

### <a name="theme-colors-blue-with-neutral-colors-followed-by-alert-colors"></a><span data-ttu-id="90e67-158">Designfarben (Blau) mit neutralen Farben gefolgt von Warnfarben</span><span class="sxs-lookup"><span data-stu-id="90e67-158">Theme colors (blue) with neutral colors, followed by alert colors</span></span>

![Designfarben (Blau) mit neutralen Farben und Warnfarben](../images/accessibility-blue-theme-and-alert-colors.png)

<br/>

<table>
<tr>
<td style="color:white; background-color:#004578"><span data-ttu-id="90e67-160">themeDarker: #004578</span><span class="sxs-lookup"><span data-stu-id="90e67-160">themeDarker: #004578</span></span></td>
<td style="color:white; background-color:#000000"><span data-ttu-id="90e67-161">black: #000000</span><span class="sxs-lookup"><span data-stu-id="90e67-161">black: #000000</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#005a9e"><span data-ttu-id="90e67-162">themeDark: #005a9e</span><span class="sxs-lookup"><span data-stu-id="90e67-162">themeDark: #005a9e</span></span></td>
<td style="color:white; background-color:#212121"><span data-ttu-id="90e67-163">neutralDark: #212121</span><span class="sxs-lookup"><span data-stu-id="90e67-163">neutralDark: #212121</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#106ebe"><span data-ttu-id="90e67-164">themeDarkAlt: #106ebe</span><span class="sxs-lookup"><span data-stu-id="90e67-164">themeDarkAlt: #106ebe</span></span></td>
<td style="color:white; background-color:#333"><span data-ttu-id="90e67-165">neutralPrimary: #333</span><span class="sxs-lookup"><span data-stu-id="90e67-165">neutralPrimary: #333</span></span></td>
</tr>
<tr>
<td rowspan="3" style="font-weight:bold; vertical-align:middle; color:white; background-color:#0078d7"><span data-ttu-id="90e67-166">themePrimary: #0078d7</span><span class="sxs-lookup"><span data-stu-id="90e67-166">themePrimary: #0078d7</span></span></td>
<td style="color:white; background-color:#3c3c3c"><span data-ttu-id="90e67-167">neutralPrimaryAlt: #3c3c3c</span><span class="sxs-lookup"><span data-stu-id="90e67-167">neutralPrimaryAlt: #3c3c3c</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#666666"><span data-ttu-id="90e67-168">neutralSecondary: #666666</span><span class="sxs-lookup"><span data-stu-id="90e67-168">neutralSecondary: #666666</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#a6a6a6"><span data-ttu-id="90e67-169">neutralTertiary: #a6a6a6</span><span class="sxs-lookup"><span data-stu-id="90e67-169">neutralTertiary: #a6a6a6</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#2b88d8"><span data-ttu-id="90e67-170">themeSecondary: #2b88d8</span><span class="sxs-lookup"><span data-stu-id="90e67-170">themeSecondary: #2b88d8</span></span></td>
<td style="color:black; background-color:#c8c8c8"><span data-ttu-id="90e67-171">neutralTertiaryAlt: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="90e67-171">neutralTertiaryAlt: #c8c8c8</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#71afe5"><span data-ttu-id="90e67-172">themeTertiary: #71afe5</span><span class="sxs-lookup"><span data-stu-id="90e67-172">themeTertiary: #71afe5</span></span></td>
<td style="color:black; background-color:#eaeaea"><span data-ttu-id="90e67-173">neutralLight: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="90e67-173">neutralLight: #eaeaea</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#c7e0f4"><span data-ttu-id="90e67-174">themeLight: #c7e0f4</span><span class="sxs-lookup"><span data-stu-id="90e67-174">themeLight: #c7e0f4</span></span></td>
<td style="color:black; background-color:#f4f4f4"><span data-ttu-id="90e67-175">neutralLighter: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="90e67-175">neutralLighter: #f4f4f4</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#deecf9"><span data-ttu-id="90e67-176">themeLighter: #deecf9</span><span class="sxs-lookup"><span data-stu-id="90e67-176">themeLighter: #deecf9</span></span></td>
<td style="color:black; background-color:#f8f8f8"><span data-ttu-id="90e67-177">neutralLighterAlt: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="90e67-177">neutralLighterAlt: #f8f8f8</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#eff6fc"><span data-ttu-id="90e67-178">themeLighterAlt: #eff6fc</span><span class="sxs-lookup"><span data-stu-id="90e67-178">themeLighterAlt: #eff6fc</span></span></td>
<td style="color:black; background-color:#fff"><span data-ttu-id="90e67-179">white: #fff</span><span class="sxs-lookup"><span data-stu-id="90e67-179">white: #fff</span></span></td>
</tr>
</table>

<br/>

<table>
<tr>
<td style="color:white; background-color:#952226"><span data-ttu-id="90e67-180">themeDark: #952226</span><span class="sxs-lookup"><span data-stu-id="90e67-180">themeDark: #952226</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#f6d6d8"><span data-ttu-id="90e67-181">themeLight: #f6d6d8</span><span class="sxs-lookup"><span data-stu-id="90e67-181">themeLight: #f6d6d8</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#e55c12"><span data-ttu-id="90e67-182">themeSecondary: #e55c12</span><span class="sxs-lookup"><span data-stu-id="90e67-182">themeSecondary: #e55c12</span></span></td>
</tr>
</table>

<br/>

<table>
<tr>
<td style="color:white; background-color:#0f7c39"><span data-ttu-id="90e67-183">themeDarkAlt: #0f7c39</span><span class="sxs-lookup"><span data-stu-id="90e67-183">themeDarkAlt: #0f7c39</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#bff7d5"><span data-ttu-id="90e67-184">themeLight: #bff7d5</span><span class="sxs-lookup"><span data-stu-id="90e67-184">themeLight: #bff7d5</span></span></td>
</tr>
</table>


## <a name="high-contrast"></a><span data-ttu-id="90e67-185">Hoher Kontrast</span><span class="sxs-lookup"><span data-stu-id="90e67-185">High contrast</span></span>

<span data-ttu-id="90e67-186">Verwenden Sie Farben mit hohem Kontrast für die Auswahl von Komponenten und Merkmalen im Internet.</span><span class="sxs-lookup"><span data-stu-id="90e67-186">Use high contrast colors as a guide for color choices for components and states on the web.</span></span> <span data-ttu-id="90e67-187">Windows-Computer können nur erkennen, ob ein PC mit der Einstellung „Hoher Kontrast“ oder „Hoher Kontrast Weiß“ ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="90e67-187">Windows computers only have the ability to detect whether a PC is running high contrast, or high contrast white.</span></span> <span data-ttu-id="90e67-188">Verwenden Sie aus diesem Grund die standardmäßige Einstellung „Hoher Kontrast Schwarz“ für alle kontrastreichen, nicht weißen Designs.</span><span class="sxs-lookup"><span data-stu-id="90e67-188">For this reason, use the default high contrast black setting for any high contrast, non-white theme.</span></span>

<!-- In the left part of the image, I think the title should be "High Contrast Black". -->

![Einstellungen „Hoher Kontrast Schwarz“ und „Hoher Kontrast Weiß“](https://i.imgur.com/qvTFzd4.png)

<br/>

## <a name="see-also"></a><span data-ttu-id="90e67-190">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="90e67-190">See also</span></span>

- [<span data-ttu-id="90e67-191">Designs und Farben in SharePoint</span><span class="sxs-lookup"><span data-stu-id="90e67-191">SharePoint themes and colors</span></span>](themes-colors.md)
- [<span data-ttu-id="90e67-192">Entwerfen von benutzerfreundlichen SharePoint-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="90e67-192">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)



