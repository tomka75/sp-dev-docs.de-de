---
title: Barrierefreiheit im SharePoint-Webpartdesign
ms.date: 11/21/2017
ms.openlocfilehash: b1c2e0819d15e470d1502deee79f8d6ab9254213
ms.sourcegitcommit: 068729a51c9e2c1a83e7e33d28149ab79bfbd06e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/29/2017
---
<!--Based on how rough this content is in it's current state, i'm going to pull it from this initial release so we can edit and better prepare. -->

# <a name="accessibility-in-sharepoint-web-part-design"></a>Barrierefreiheit im SharePoint-Webpartdesign

Die Entwicklung eines gleichbleibenden Erlebnisses, bei dem die visuellen, auditiven, körperlichen, kognitiven und sprachlichen Bedürfnisse aller Benutzer erfüllt werden, ist eine wichtige Komponente des SharePoint-Webpartdesigns. Ein barrierefreies Design bezieht sich nicht nur auf Menschen mit körperlichen Einschränkungen, sondern möglicherweise auch auf situationsbedingte Einschränkungen. Ein barrierefreies Design ist ein gutes Design.

## <a name="accessibility-guidelines"></a>Richtlinien für Eingabehilfen

<!-- Make sure that this is an external resource that folks can access. Original link was to a OneNote file. -->
Alle Microsoft-Produkte müssen die [Microsoft-Eingabehilfenstandards](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Link zu den Microsoft-Eingabehilfenstandards") erfüllen.  

<!-- Fabric components are not designed to be accessible already? And, shouldn't components that aren't based on Fabric also be accessible? -->

Wenn Sie ein Dialogfeld, eine Dateiauswahl oder eine beliebige andere [Office-UI-Fabric](https://dev.office.com/fabric#/components)-Komponente erstellen, befolgen Sie die Anleitungen in diesem Artikel, um sicherzustellen, dass Ihre Inhalte barrierefrei sind. 

<!-- Not sure why we have that link? It currently goes to the OneNote file. Where is the Common UI Controls content? Is that related to accessibility? [v-licapu] - I agree; we shouldn't be linking to this unless it's live to external audiences; even I can't access it. I moved it to within the comment: 
[Common UI Controls](https://microsoft.sharepoint.com/teams/STS/_layouts/OneNote.aspx?id=%2Fteams%2FSTS%2FShared%20Documents%2FSP%20Accessibility%2FAccessibility%20Guidance&wd=target%28Accessibility%20101.one%7C0005C142-938C-4411-B543-B9F4199E19B3%2FEverything%20you%20need%20to%20know%20about%20Accessibility%7CE099AFE3-8804-4E1F-BA50-99493AB8A3D0%2F%29 "Link to Common UI Controls") -->

## <a name="accessibility-testing"></a>Barrierefreiheitsprüfung

<!-- FYI, I added links. Can we assume that our target audience uses the Edge browser? -->

Testen Sie Ihr Webpart zunächst mit [Narrator](https://support.microsoft.com/de-DE/help/22798/windows-10-narrator-get-started) und Microsoft Edge, und überprüfen Sie dann das barrierefrei Erlebnis mit [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).

Narrator und Microsoft Edge entsprechen den Standards. Wenn Sie die Überprüfung auf diese Weise vornehmen, können Sie Probleme leichter aufdecken und feststellen, ob Ihre Seite die Eingabehilfenstandards erfüllt. 

JAWS ist Marktführer auf dem Gebiet der Sprachausgabe. JAWS enthält Features, mit denen Sie die Barrierefreiheit einiger Websites verbessern können, die bei anderen Sprachausgaben nicht so leicht zugänglich sind. Daher garantiert ein Test in JAWS möglicherweise nicht, dass Ihre Website alle Barrierefreiheitsanforderungen erfüllt. 
 
Möglicherweise möchten Sie auch testen, welche Kombination von Browser und Sprachausgabe den größten Marktanteil für Ihre Website aufweist.

<!-- Delete? This doesn't seem like text that should be in externally published docs? 
When suppliers test with JAWS, we ask them to repro identified bugs with Narrator and Edge. In the case a bug does not repro with Narrator/Edge it is sent to Mary Smith who works with VFO for a Jaws specific fix. 
-->

## <a name="keyboard-navigation"></a>Tastaturnavigation

<!-- Is this section telling people how to navigate via a keyboard, or how to design to optimize for keyboard navigation? If the former, . -->

Für manche Benutzer ist die Navigation einer Website über die Tastatur leichter. Erfahrene Benutzer verwenden häufig die Tastaturnavigation. Verwenden Sie Tastaturkurzbefehle wie Tabs, um zu Steuerelementen der Seite zu wechseln, und verwenden Sie die Pfeiltasten zum Navigieren innerhalb der Steuerelemente.

### <a name="navigation-between-controls"></a>Navigation zwischen Steuerelementen

Jedes Steuerelement ist ein Tabstopp. Innerhalb eines Steuerelements gelten die folgenden Regeln:

- Im Allgemeinen ist der erste Tabstopp der obere linke Bereich des Steuerelements. Der letzte Tabstopp ist das untere rechte Steuerelement.
- Bei modalen Oberflächen sollte der letzte Tabstopp die Commit-Aktionen umfassen.
- Bei Listen sollte der erste Tabstopp das erste Element in der Liste, der nächste Tabstopp die Befehle, der nächste die Navigation, der nächste die Einstellungen usw. umfassen.

<!-- We should make sure the content in the accessibility topic is accessibible. ;) Please describe the information that the image conveys; something like this (also consider making the image an actual screen shot, that might be more clear):

In the following image:
The first tab is the list item.
The second tab is the command.
The third tab is the navigation.
-->

*Abbildung 1: Tabstopps einer SharePoint-Seite*

![Darstellung der Tabstopps einer SharePoint-Seite](https://i.imgur.com/Vn3VosN.png)

### <a name="navigation-within-a-control"></a>Navigation innerhalb eines Steuerelements

Sie können die Pfeiltasten verwenden, um zu Objekten eines Steuerelements, z. B. den Optionen in einem Menü, Befehlen in einer Befehlsleiste oder Elementen in einer Liste zu wechseln.

<!-- This image is not very clear. Do you need to have the "blank" list box on the left? -->

*Abbildung 2: Verwenden der Pfeiltasten zum Navigieren innerhalb eines Steuerelements*

![Verwenden der Pfeiltasten zum Navigieren innerhalb eines Steuerelements](https://i.imgur.com/vF0Nk73.png)

### <a name="selecting-the-current-item"></a>Auswählen des aktuellen Elements

Verwenden Sie die Leertaste oder deaktivieren Sie das derzeit gewählte Element in einem Steuerelement.

*Abbildung 3: Verwenden der Leertaste zum Auswählen eines Elements in einer Liste*

![Verwenden der Leertaste zum Auswählen eines Elements in einer Liste](https://i.imgur.com/j3fBKPl.png)

### <a name="run-a-control"></a>Ausführen eines Steuerelements

Drücken Sie die **Eingabetaste**, um ein Steuerelement auszuführen.

*Abbildung 4: Drücken der EINGABETASTE zum Ausführen eines Steuerelements*

![Drücken der EINGABTASTE zum Ausführen eines Steuerelements](https://i.imgur.com/s0nMPdT.png)

### <a name="leave-a-control"></a>Verlassen eines Steuerelements

Drücken Sie die **ESC-Taste**, um ein Steuerelement zu verlassen und zum Container zurückkehren.

*Abbildung 5: Drücken der ESC-Taste zum Verlassen eines Steuerelements und zum Zurückkehren zum Container*

![Drücken der ESC-Taste zum Verlassen eines Steuerelements und zum Zurückkehren zum Container](https://i.imgur.com/uD99zIX.png)

### <a name="go-to-the-first-or-last-item"></a>Wechseln zum ersten bzw. letzten Element

Drücken Sie **POS1** oder **Ende**, um direkt zum ersten oder letzten Element einer Liste, eines Menüs usw. zu springen.

*Abbildung 6: Drücken von POS1 oder Ende, um zum ersten oder letzten Element einer Liste zu springen*

![Drücken von POS1 oder Ende, um zum ersten oder letzten Element einer Liste zu springen](https://i.imgur.com/gGKsh74.png)


## <a name="screen-reader-navigation"></a>Navigation per Sprachausgabe

Benutzer mit Sehschwächen navigieren die Benutzeroberfläche der Website per Sprachausgabe 

<!-- Narrator isn't a third-party product. This image needs more text/explanation; please also clarify the alt text. Is this section important, or can it be removed, given the previous mention of testing with Narrator and JAWS? Again, the intent/target audience for this information isn't clear - is it for the user, or the designer? Can you explain why this information is important from the designer's POV? -->

*Abbildung 7: Navigation per Sprachausgabe einer SharePoint-Website*

![Navigation per Sprachausgabe einer SharePoint-Website](https://i.imgur.com/ar23o3X.png)

## <a name="alt-text-and-transcripts"></a>Alternativtext und Transkriptionen

Verwenden Sie Beschreibungen von Bildern, die von der Sprachausgabe verarbeitet werden können. Dies ist nützlich Benutzer mit Sehschwächen, die Informationen visuell nicht erfassen können. Stellen Sie sicher, dass Ihr Alternativtext eine ausführliche Beschreibung enthält, da einige Benutzer eine Sprachausgabe verwenden, um Zugriff auf die Informationen des Bildes zu erhalten. 

Verwenden Sie nicht nur Farben, um eine Bedeutung zu erklären, sondern auch Formen.

Um eine vollständige Konformität mit den Eingabehilfenstandards zu erreichen, beziehen Sie Alternativtext und eine vollständige Transkription der Audio- und Videoinhalte Ihrer Website mit ein.

## <a name="minimum-readable-contrast"></a>Lesbarkeit durch Kontrast

Ein minimaler Kontrast ist dringend erforderlich, damit Benutzer mit Sehschwächen die Inhalte der Seite erfassen können. Dies ist ebenfalls wichtig, um eine Lesbarkeit bei schwacher Beleuchtung oder störenden Effekten wie Blendung zu gewährleisten. 

<!-- Convert this image into a table, for accessibility. ;) -->
<!-- ![Neutral, Theme, and Alert colors for minimum readable contrast](https://i.imgur.com/L7pSF1w.png)-->

![Farben für Lesbarkeit durch Kontrast](../images/wcag-2aa-compliance-colors.png)

### <a name="theme-colors-blue-and-neutral-colors"></a>Designfarben (Blau) und neutrale Farben

<table>
<tr>
<td style="color:white; background-color:#004578">themeDarker: #004578</td>
<td style="color:white; background-color:#000000">black: #000000</td>
</tr>
<tr>
<td style="color:white; background-color:#005a9e">themeDark: #005a9e</td>
<td style="color:white; background-color:#212121">neutralDark: #212121</td>
</tr>
<tr>
<td style="color:white; background-color:#106ebe">themeDarkAlt: #106ebe</td>
<td style="color:white; background-color:#333">neutralPrimary: #333</td>
</tr>
<tr>
<td rowspan="3" style="font-weight:bold; vertical-align:middle; color:white; background-color:#0078d7">themePrimary: #0078d7</td>
<td style="color:white; background-color:#3c3c3c">neutralPrimaryAlt: #3c3c3c</td>
</tr>
<tr>
<td style="color:white; background-color:#666666">neutralSecondary: #666666</td>
</tr>
<tr>
<td style="color:black; background-color:#a6a6a6">neutralTertiary: #a6a6a6</td>
</tr>
<tr>
<td style="color:white; background-color:#2b88d8">themeSecondary: #2b88d8</td>
<td style="color:black; background-color:#c8c8c8">neutralTertiaryAlt: #c8c8c8</td>
</tr>
<tr>
<td style="color:black; background-color:#71afe5">themeTertiary: #71afe5</td>
<td style="color:black; background-color:#eaeaea">neutralLight: #eaeaea</td>
</tr>
<tr>
<td style="color:black; background-color:#c7e0f4">themeLight: #c7e0f4</td>
<td style="color:black; background-color:#f4f4f4">neutralLighter: #f4f4f4</td>
</tr>
<tr>
<td style="color:black; background-color:#deecf9">themeLighter: #deecf9</td>
<td style="color:black; background-color:#f8f8f8">neutralLighterAlt: #f8f8f8</td>
</tr>
<tr>
<td style="color:black; background-color:#eff6fc">themeLighterAlt: #eff6fc</td>
<td style="color:black; background-color:#fff">white: #fff</td>
</tr>
</table>

### <a name="alert-colors"></a>Farben für Warnungen

<table>
<tr>
<td style="color:white; background-color:#952226">themeDark: #952226</td>
</tr>
<tr>
<td style="color:black; background-color:#f6d6d8">themeLight: #f6d6d8</td>
</tr>
<tr>
<td style="color:white; background-color:#e55c12">themeSecondary: #e55c12</td>
</tr>
</table>

<br/>

<table>
<tr>
<td style="color:white; background-color:#0f7c39">themeDarkAlt: #0f7c39</td>
</tr>
<tr>
<td style="color:black; background-color:#bff7d5">themeLight: #bff7d5</td>
</tr>
</table>

## <a name="high-contrast"></a>Hoher Kontrast

Verwenden Sie Farben mit hohem Kontrast für die Auswahl von Komponenten und Merkmalen im Internet. Windows-Computer können nur erkennen, ob ein PC mit der Einstellung „Hoher Kontrast“ oder „Hoher Kontrast Weiß“ ausgeführt wird. Verwenden Sie aus diesem Grund die standardmäßige Einstellung „Hoher Kontrast Schwarz“ für alle kontrastreichen, nicht weißen Designs.

<!-- In the left part of the image, I think the title should be "High Contrast Black". -->

*Abbildung 8: Einstellungen „Hoher Kontrast Schwarz“ und „Hoher Kontrast Weiß“*

![Einstellungen „Hoher Kontrast Schwarz“ und „Hoher Kontrast Weiß“](https://i.imgur.com/qvTFzd4.png)





