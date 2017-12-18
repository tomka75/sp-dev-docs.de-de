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




# <a name="accessibility-in-sharepoint-web-part-design"></a>Barrierefreiheit im SharePoint-Webpartdesign

Die Entwicklung eines gleichbleibenden Erlebnisses, bei dem die visuellen, auditiven, körperlichen, kognitiven und sprachlichen Bedürfnisse aller Benutzer erfüllt werden, ist eine wichtige Komponente des SharePoint-Webpartdesigns. Ein barrierefreies Design bezieht sich nicht nur auf Menschen mit körperlichen Einschränkungen, sondern möglicherweise auch auf situationsbedingte Einschränkungen. Ein barrierefreies Design ist ein gutes Design.

## <a name="accessibility-guidelines"></a>Richtlinien für Eingabehilfen

<!-- Make sure that this is an external resource that folks can access. Original link was to a OneNote file. -->
Alle Microsoft-Produkte müssen die [Microsoft-Eingabehilfenstandards](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Link zu den Microsoft-Eingabehilfenstandards") erfüllen.  

<!-- Fabric components are not designed to be accessible already? And, shouldn't components that aren't based on Fabric also be accessible? -->

Wenn Sie ein Dialogfeld, eine Dateiauswahl oder eine beliebige andere [Office-UI-Fabric](https://dev.office.com/fabric#/components)-Komponente erstellen, befolgen Sie die Anleitungen in diesem Artikel, um sicherzustellen, dass Ihre Inhalte barrierefrei sind. 

<!-- Not sure why we have that link? It currently goes to the OneNote file. Where is the Common UI Controls content? Is that related to accessibility? -->

[Allgemeine Benutzeroberflächensteuerelemente](https://microsoft.sharepoint.com/teams/STS/_layouts/OneNote.aspx?id=%2Fteams%2FSTS%2FShared%20Documents%2FSP%20Accessibility%2FAccessibility%20Guidance&wd=target%28Accessibility%20101.one%7C0005C142-938C-4411-B543-B9F4199E19B3%2FEverything%20you%20need%20to%20know%20about%20Accessibility%7CE099AFE3-8804-4E1F-BA50-99493AB8A3D0%2F%29 "Link zu allgemeinen Benutzeroberflächensteuerelementen")

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
![Darstellung der Tabstopps einer SharePoint-Seite](https://i.imgur.com/Vn3VosN.png)

### <a name="navigation-within-a-control"></a>Navigation innerhalb eines Steuerelements

Sie können die Pfeiltasten verwenden, um zu Objekten eines Steuerelements, z. B. den Optionen in einem Menü, Befehlen in einer Befehlsleiste oder Elementen in einer Liste zu wechseln.

<!-- This image is not very clear. Do you need to have the "blank" list box on the left? -->

![Verwenden der Pfeiltasten zum Navigieren innerhalb eines Steuerelements](https://i.imgur.com/vF0Nk73.png)

### <a name="selecting-the-current-item"></a>Auswählen des aktuellen Elements

Verwenden Sie die Leertaste oder deaktivieren Sie das derzeit gewählte Element in einem Steuerelement.

![Verwenden der Leertaste zum Auswählen eines Elements in einer Liste](https://i.imgur.com/j3fBKPl.png)

### <a name="run-a-control"></a>Ausführen eines Steuerelements

Drücken Sie **Enter** oder die Eingabetaste, um ein Steuerelement auszuführen.

![Drücken von Enter zum Ausführen eines Steuerelements](https://i.imgur.com/s0nMPdT.png)

### <a name="leave-a-control"></a>Verlassen eines Steuerelements

Drücken Sie **Escape**, um ein Steuerelement zu verlassen und zum Container zurückkehren.

![Drücken von Escape, um ein Steuerelement zu verlassen und zum Container zurückkehren](https://i.imgur.com/uD99zIX.png)

### <a name="go-to-the-first-or-last-item"></a>Zum ersten bzw. letzten Element wechseln

Drücken Sie **POS1** oder **Ende**, um direkt zum ersten oder letzten Element einer Liste, eines Menüs usw. zu springen.

![Drücken von  POS1 oder Ende, um zum ersten oder letzten Element einer Liste zu springen](https://i.imgur.com/gGKsh74.png)


## <a name="screen-reader-navigation"></a>Navigation per Sprachausgabe

Benutzer mit Sehschwächen navigieren die Benutzeroberfläche der Website per Sprachausgabe 

<!-- Narrator isn't a third-party product. This image needs more text/explanation; please also clarify the alt text. Is this section important, or can it be removed, given the previous mention of testing with Narrator and JAWS? Again, the intent/target audience for this information isn't clear - is it for the user, or the designer? Can you explain why this information is important from the designer's POV? -->

![Navigation per Sprachausgabe einer SharePoint-Website](https://i.imgur.com/ar23o3X.png)

## <a name="alt-text-and-transcripts"></a>Alternativtext und Transkriptionen

Verwenden Sie Beschreibungen von Bildern, die von der Sprachausgabe verarbeitet werden können. Dies ist nützlich Benutzer mit Sehschwächen, die Informationen visuell nicht erfassen können. Stellen Sie sicher, dass Ihr Alternativtext eine ausführliche Beschreibung enthält, da einige Benutzer eine Sprachausgabe verwenden, um Zugriff auf die Informationen des Bildes zu erhalten. 

Verwenden Sie nicht nur Farben, um eine Bedeutung zu erklären, sondern auch Formen.

Um eine vollständige Konformität mit den Eingabehilfenstandards zu erreichen, beziehen Sie Alternativtext und eine vollständige Transkription der Audio- und Videoinhalte Ihrer Website mit ein.

## <a name="minimum-readable-contrast"></a>Lesbarkeit durch Kontrast

Ein minimaler Kontrast ist dringend erforderlich, damit Benutzer mit Sehschwächen die Inhalte der Seite erfassen können. Dies ist ebenfalls wichtig, um eine Lesbarkeit bei schwacher Beleuchtung oder störenden Effekten wie Blendung zu gewährleisten. 

<!-- Convert this image into a table, for accessibility. ;) -->

![Lesbarkeit durch Kontrast: Neutrale, Theme- und Signalfarben](https://i.imgur.com/L7pSF1w.png)


## <a name="high-contrast"></a>Hoher Kontrast

Verwenden Sie Farben mit hohem Kontrast für die Auswahl von Komponenten und Merkmalen im Internet. Windows-Computer können nur erkennen, ob ein PC mit der Einstellung „Hoher Kontrast“ oder „Hoher Kontrast Weiß“ ausgeführt wird. Verwenden Sie aus diesem Grund die standardmäßige Einstellung „Hoher Kontrast Schwarz“ für alle kontrastreichen, nicht weißen Designs.

<!-- In the left part of the image, I think the title should be "High Contrast Black". -->

![Einstellungen „Hoher Kontrast Schwarz“ und „Hoher Kontrast Weiß“](https://i.imgur.com/qvTFzd4.png)





