---
title: Branding von SharePoint-Websites in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 114b4b241e4fbf54cf49dc5b9ebc32d7c357d2a6
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="branding-sharepoint-sites-in-the-sharepoint-add-in-model"></a>Branding von SharePoint-Websites in der SharePoint-add-in-Objektmodell
========================================================

<a name="summary"></a>Summary
-------

Der Ansatz, die Sie, um Marke SharePoint-Websites durchführen in unterscheidet das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war / Farmlösungen.  In einer typischen vollständige vertrauen Code (FTC) / branding Szenario Farmlösung, benutzerdefinierte Masterseiten, Webvorlagen, JavaScript, CSS-Dateien und Bildern zum Implementieren einer benutzerdefinierten Marke erstellt werden.  Darüber hinaus können SharePoint-Designs und zusammengesetzten zum Implementieren einer benutzerdefinierten Marke erstellt werden.  Diese Artefakte sind in der Regel in einer Funktion, die deklarativen Code und FTC verwendet gepackt / Farmlösung Bereitstellen der Objekte und mit der SharePoint-Website zu registrieren.

In einer SharePoint-Add-Ins Modell branding Szenario zugeordneten aller Optionen FTC / Farmlösung branding Szenarien sind verfügbar.  Unabhängig davon, welche Option Sie wählen, können Sie bereitstellen und registrieren Ihre branding Anlagen auf SharePoint-Websites über die Bereitstellung von Remote Muster.

<a name="terminology"></a>Terminologie
-----------

In diesem Artikel wird den Begriff **SharePoint Design**, d. h. Bedeutungen in anderen Artikeln auf MSDN, MS-Blogs und alle über das Internet überlastet ist.  In der MSDN-Terminologie **SharePoint Design** speziell bezieht sich auf die Farbpalette / Farbschema (.spcolor-Datei) angewendet, auf einer SharePoint-Website.  Plug & Play-Terminologie sind die Begriffe, die **SharePoint-Designs** und **durchkomponierten Look** identisch.

Ein SharePoint-Design ist eine der viele [SharePoint-Designoberfläche Komponenten auftreten](https://msdn.microsoft.com/en-us/library/office/jj927174.aspx).

In diesem Artikel den Begriff **SharePoint-Designs** mit dem spezifischen technischen Artikel ausrichten gewählten bezieht sich diese auf, um alle branding Optionen kurz beschrieben. 

<a name="why-would-you-custom-brand-a-sharepoint-site"></a>Warum würden Sie benutzerdefinierte SharePoint-Website Bewerbung?
----------------------------------------------------

Es gibt viele verschiedene Gründe, warum Sie auf einer SharePoint-Website anwenden würde benutzerdefiniertes branding.  Aus diesem Grund können enthalten Unternehmensidentität, Verwendbarkeit, Marketing.  

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für benutzerdefiniertes branding SharePoint-Websites bereitstellen

- Mit Office 365 Designs, SharePoint-Website Designoberfläche erleben Sie die Komponenten und besteht aus einem Branding mit SharePoint-Websites nach Möglichkeit prüft.
- Sie können einige CSS-Einstellungen über die alternative CSS-Option, wenn die Erstellung der Designs Standarddateispeicherort nicht unterstützen anpassen.
- Sie können zum Ändern oder Ausblenden von Elementen in einer SharePoint-Website Einbetten von JavaScript verwenden.
- Sie können SharePoint-Websites mithilfe von benutzerdefinierten Gestaltungsvorlagen anpassen, aber Bedenken Sie dadurch werden Sie zusätzliche langfristige Kosten und Probleme mit zukünftige Updates.
    + In den meisten Fällen können Sie alle branding Standardszenarien mit Designs, zusammengesetzten und alternative CSS erzielen.
    + Wenn Sie benutzerdefinierte Masterseiten verwenden möchten, bereiten Sie Änderungen der benutzerdefinierten Gestaltungsvorlagen anwenden, wenn wichtige Updates funktionsfähig zu Office 365 angewendet werden.
- Verwenden Sie remote-Bereitstellung bereitstellen und registrieren Sie Designs, zusammengesetzten und alle Artefakte branding mit SharePoint-Websites.
- Verwenden Sie nicht deklarativen Code oder Sandkasten-Code zum Bereitstellen und Registrieren des Designs, Masterseiten und andere Artefakte branding mit SharePoint-Websites.  

Unterstützen Office 365 SharePoint-Websites in lässt sich sagen benutzerdefiniertes branding. In diesem Artikel helfen Ihnen die kurz- und langfristigen Anpassung über eine betriebsbereite und Sicht der Wartung berücksichtigen. Dies kann nicht wirklich nur für SharePoint. Vielmehr Daumenregel IT-Lösungen mit einer beliebigen Plattform erstellte ist jedoch.

Es folgt ein Beispiel einer Office 365 SharePoint-Website, die mit den oben genannten Richtlinien angepasst wurde. In diesem Fall wurde die benutzerdefiniertes branding mit einer Office 365-Design, bereitgestellt und mit einer SharePoint-Website über das remote provisioning Muster mit der SharePoint-CSOM-API registriert implementiert.

In diesem Beispiel wird stammen aus der [Design-Management mit CSOM (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.DeployCustomThemeWeb).

![Eine SharePoint-Website mit einer Office 365-Design.](media/Recipes/Themes/example-custom-theme.png)

<a name="challenges-applying-brand-customization-to-sharepoint-sites"></a>Herausforderungen Anwenden der Marke Anpassung auf SharePoint-Websites
-----------------------------------------------------------
**Office 365-Designs im Vergleich zu SharePoint-Designs**

Es ist wichtig zu verstehen, dass Office 365-Designs und SharePoint-Designs unterscheiden.  Es ist außerdem wichtig zu verstehen, SharePoint-Designs und zusammengesetzten werden verwendet, um SharePoint-Websites mit Branding versehen.  In dieser Liste werden die verschiedenen Elemente beschrieben.  

- **Office 365-Designs** werden verwendet, um der oberen Navigationsleiste ein Office 365-Mandanten mit Branding versehen.  Sie werden nur in Office 365 SharePoint-Websites nicht lokalen unterstützt.
- **SharePoint-Designs** gelten Farben für die SharePoint-Websites.
- **Looks sucht** überwachter Farben, Schriftarten, Masterseiten und Hintergrundbilder Ihrer SharePoint-Websites. 

**Office 365-Designs** enthalten die unten aufgeführten Komponenten.  

- benutzerdefiniertes logo
- URL für benutzerdefiniertes logo
- Hintergrundbild
- Basis Farbe
- Akzent
- Navigationsleisten Hintergrundfarbe
- Text-und Symbole
- App-Menü-Symbol

Finden Sie unter [Anpassen der Office 365-Design für Ihre Organisation](https://support.office.com/en-au/article/Customize-the-Office-365-theme-for-your-organization-8275da91-7a48-4591-94ab-3123a3f79530) Artikel erfahren Sie mehr über Office 365-Designs.

**SharePoint-Designs** umfassen die folgenden Komponenten.  

- Farb-Palette (.spcolor-Datei)

*Beachten Sie, dass eine Gestaltungsvorlage, Gestaltungsvorlage in der Vorschau oder zusammengesetztes Design ein SharePoint-Designs in einer Office 365 SharePoint-Website nicht enthalten ist.* Dadurch wird die nicht zu benutzerdefinierte Gestaltungsvorlagen implementieren branding auf SharePoint-Websites verwenden oben genannten Anweisungen ausgerichtet.

**Zusammengesetzte Designs für lokale SharePoint 2013/2016 Websites verwendet** werden eine oder mehrere der folgenden Komponenten enthalten.  

- Farb-Palette (.spcolor-Datei) – so genannte eines SharePoint-Designs
- Schriftartenschema (.spfont-Datei)
- Hintergrundbild
- Gestaltungsvorlage
- Vorschau der Gestaltungsvorlage

Finden Sie im Artikel [Designs (Übersicht) für SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/jj927174.aspx) erfahren Sie mehr über diese Komponenten.

**Für Office 365 SharePoint-Websites verwendet Looks aus** enthalten eine oder mehrere der folgenden Komponenten.  

- Farb-Palette (.spcolor-Datei) – so genannte eines SharePoint-Designs
- Schriftartenschema (.spfont-Datei)
- Hintergrundbild
- Gestaltungsvorlage

**Teamwebsites im Vergleich zu Veröffentlichungssites**

Beim Anwenden von benutzerdefiniertem branding auf SharePoint-Websites treten Sie Teamwebsites und Veröffentlichung von Websites mit Branding versehen werden müssen. Im Allgemeinen verwenden Intranets in lokalen und Office 365-Szenarien in SharePoint erstellt eine Kombination von Teamwebsites und Veröffentlichung von Websites.  

Benutzerdefiniertes branding Anforderungen erfordern oft bestimmtes Layout ändert, Designs und JavaScript Einbetten von Techniken kann nicht erreichen.

In diesem Fall benötigen Teamwebsites in der Regel nicht die Menge an benutzerdefiniertes branding, führen Sie Veröffentlichungswebsites und die Out-of-Box SharePoint moderne Ansicht für mobile Geräte in der Regel ausreichend ist, um die Unterstützung von mobilen Geräten für Teamwebsites.  Da dies der Fall ist, empfiehlt es sich nur benutzerdefinierte Masterseiten für die Veröffentlichung von Websites und zum Verwenden von benutzerdefinierten SharePoint-Designs (.spcolor-Dateien), Schriftartenschemas (.spfont-Dateien) und Hintergrundbilder als zusammengesetzten Marke Teamwebsites definiert zu verwenden.

**Bereitstellung**

Benutzerdefiniertes branding wird normalerweise angewendet, wenn eine Website bereitgestellt wird.  Der Bereitstellungsprozess remote passt sehr gut bei diesem Ansatz.  In der Regel ist nur dann mithilfe des Webbrowsers wird zum Anpassen von SharePoint-branding manuell anwenden Prototypen oder Ändern einer einzelnen SharePoint-Website, die nicht eingeschlossen andere Websitesammlungen oder Websites sub wachsen geplant ist. 

<a name="options-to-apply-brand-customization-to-sharepoint-sites"></a>Optionen zum Anwenden der Marke Anpassung auf SharePoint-Websites
--------------------------------------------------------

Sie können mehrere Optionen zum Anwenden der Marke Anpassung auf SharePoint-Websites mit dem neuen SharePoint-Add-in-Modell auswählen.

- Verwenden Sie ein Office 365-Design auf eine SharePoint-Website mit Branding versehen.
- Ändern Sie das zusammengesetzte Design für eine SharePoint-Website.
- Verwenden Sie das Tool SharePoint Farbe Farbpalette, um eine Farbpalette für ein SharePoint-Design zu erstellen.
- Verwenden Sie alternative CSS, um einer SharePoint-Website mit Branding versehen.
- Erstellen Sie manuell ein Farbschema für ein SharePoint-Design. 
- Erstellen Sie manuell ein Schriftartenschema für ein SharePoint-Design.
- Verwenden Sie zum ein- und Ausblenden von Komponenten auf einer SharePoint-Website Einbetten von JavaScript.
- Erstellen von benutzerdefinierten Gestaltungsvorlagen und Seitenlayouts für eine SharePoint-Website.
- Erstellen Sie ein zusammengesetztes Design für eine SharePoint-Website.

<a name="use-an-office-365-theme-to-brand-a-sharepoint-site"></a>Verwenden Sie ein Office 365-Design auf eine SharePoint-Website mit Branding versehen
--------------------------------------------------

Ändern einer O365-Instanz Office-Designs ist die einfachste Methode zum Anwenden von branding zu einer SharePoint-Website.

- Office 365-Designs können zentral steuern branding in allen Office 365-Diensten verwendet werden.
    + Derzeit ist die Anzahl der Einstellungen für ein Office 365-Design zugeordnet beschränkt.
- Office 365-Designs können auf der Ebene der SharePoint-Website außer Kraft gesetzt werden.
- Office 365-Designs sind nur in Office 365-Mandanten, nicht in der lokalen SharePoint vorhanden.
- Office 365-Designs bieten eine gewisse Flexibilität zu eine SharePoint-Website mit Branding versehen.
- Office 365-Designs sind sehr einfache und kostengünstige implementieren und verwalten Sie die kurz- und langfristigen.

**Wenn ein Office 365-Design auf eine SharePoint-Website eine gute anpassen verwendet werden?**

Diese Option funktioniert gut, wenn Ihre branding Anforderungen nicht sehr spezifisch sind, und Sie nur sich für ein neues Farbschema für den Office-Leiste Teil Ihrer SharePoint-Website, eines Logos und eines Hintergrundbilds interessieren.  ***Es ist wichtig, beachten Sie, dass die einzige Möglichkeit zum Ändern des Symbols App-Menü über das Office 365-Design ist.***

**Empfohlene bereitstellungsansätzen**

Sie können das Office 365-Design für ein Office 365-Instanz über den Webbrowser oder die remote provisioning Muster ändern.

<a name="change-the-composed-look-for-a-sharepoint-site"></a>Ändern Sie das zusammengesetzte Design für eine SharePoint-Website
----------------------------------------------
Ändern einer SharePoint-zusammengesetztes Design der Website ist eine weitere einfache Möglichkeit zum branding bis hin zu einer SharePoint-Website anwenden.  

- Zusammengesetzten erfolgt in der Seite Websiteeinstellungen.  
- SharePoint im Lieferumfang von mehreren zusammengesetzten zur Auswahl.
- Zusammengesetzten vorhanden in beiden Office 365-Mandanten und in lokalen SharePoint.
- Zusammengesetzten bieten eine gewisse Flexibilität zu eine SharePoint-Website mit Branding versehen.
    + Beachten Sie, dass zusammengesetzten Sammlungen von Farb- und Schriftartenschemas eines Hintergrundbilds und einer Gestaltungsvorlage sind.
- Zusammengesetzten sind sehr einfache und kostengünstige in die kurz- und langfristigen implementieren.
- Zusammengesetzten können Out-of-Box Gestaltungsvorlagen oder benutzerdefinierten Gestaltungsvorlagen enthalten.
- Sie können zusammengesetzten auf einer Ebene pro Website verwenden.
 
**Wenn ein zusammengesetztes Design für eine SharePoint-Website eine gute Übereinstimmung geändert werden?**

Diese Option funktioniert gut, wenn Ihre branding Anforderungen nicht sehr spezifisch sind, und Sie nur sich für ein neues Farbschema, Hintergrundbild und einer Gestaltungsvorlage für die Website interessieren.

**Empfohlene bereitstellungsansätzen**

Sie können das zusammengesetzte Design für eine SharePoint-Website über den Webbrowser oder die remote provisioning Muster ändern.

<a name="use-the-sharepoint-color-palette-tool-to-create-a-color-palette-for-a-sharepoint-theme"></a>Verwenden Sie das Tool SharePoint Farbe Palette zum Erstellen einer Farbpalette für ein SharePoint-Design
--------------------------------------------------------------------------------------
Das [Tool für SharePoint Farbe Palette](http://www.microsoft.com/en-gb/download/details.aspx?id=38182) (siehe Abbildung unten) ist einfach zu verwenden und ermöglicht das Farbschema für ein SharePoint-Design zu erstellen.  Dieses Tool bietet eine *Was finden Sie unter Get* bearbeiten Oberfläche.  Wenn Sie die Farbschemas speichern, die dieses Tool erstellt wird eine .spcolor-Datei generiert.

![Das SharePoint-Farbe Palette-Tool](media/Recipes/Themes/color-palette-tool.png)

- Erstellen von benutzerdefinierten Farbschemas für SharePoint-Websites ist sehr einfache und kostengünstige implementieren und verwalten Sie die kurz- und langfristigen.
    + Denken Sie daran, die ein benutzerdefiniertes Farbschema ist nur ein Teil einer zusammengesetztes Design.
- Benutzerdefinierte Farbschemas bieten eine gewisse Flexibilität zu eine SharePoint-Website mit Branding versehen.
- Sie können Farbschemas über zusammengesetzten unter Anwenden einer pro Websiteebene.

**Beim Erstellen von benutzerdefinierten ist Farbschema für SharePoint-Websites geeignet?**

Diese Option funktioniert gut, wenn Ihre Bedürfnisse branding ein neues Farbschema enthalten benötigen, jedoch keine Änderung des Layouts oder ein- und Ausblenden von verschiedenen Office 365 SharePoint-Komponenten.

**Empfohlene bereitstellungsansätzen**

Sie können verwenden Sie den Webbrowser oder die remote provisioning Muster Hochladen der .spcolor-Datei, die das Tool erstellt, in einer SharePoint-Website, erstellen Sie ein zusammengesetztes Design, das es enthält, und auf einer SharePoint-Website anwenden.

<a name="use-alternate-css-to-brand-a-sharepoint-site"></a>Verwenden Sie alternative CSS auf eine SharePoint-Website mit Branding versehen
--------------------------------------------
Sie können auch eine benutzerdefinierte Datei cascading Stylesheet (CSS) erstellen und legen Sie es als Alternative CSS-Datei für eine SharePoint-Website.  

- Alternative CSS kann die Out-of-Box-CSS-Einstellungen außer Kraft gesetzt, die im Lieferumfang von SharePoint verwendet werden.
- Sie können den alternativen CSS-Ansatz für Steuerelement Farbe, Schriftarten und sogar Layout Einstellungen verwenden. 
- Alternative CSS erfordert Investition zu implementieren und verwalten Sie die kurz- und langfristigen ein mittleres Maßes an.
- Alternative CSS bietet eine gute Maß an Flexibilität zu eine SharePoint-Website mit Branding versehen.
- Alternative CSS können auf einer Ebene pro Website.

**Wenn Sie alternative CSS mit eine SharePoint-Website mit Branding versehen geeignet?**

Diese Option funktioniert gut, wenn Ihren Anforderungen branding ein neues Farbschema Schriftarten, und minimale Layout Änderungen erfordert aber nicht ein- und Ausblenden von verschiedenen Office 365 SharePoint-Komponenten.

**Empfohlene Bereitstellungsmethode**

Können den Webbrowser oder die remote provisioning Muster zum Hochladen einer CSS-Datei zu einer SharePoint-Website und auf einer SharePoint-Website anwenden.

<a name="create-a-color-scheme-for-a-sharepoint-theme-manually"></a>Erstellen Sie manuell ein Farbschema für ein SharePoint-Design
------------------------------------------------------
Sie können eine Datei .spcolor auch manuell mit einem Text-Editor wie Editor oder in Visual Studio erstellen.  Sie können sehen, dass ein Beispiel Ausschnitt aus einer Datei .spcolor unten angezeigt wird.

```XML
<?xml version="1.0" encoding="utf-8"?>
<s:colorPalette isInverted="false" previewSlot1="BackgroundOverlay" previewSlot2="BodyText" previewSlot3="AccentText" xmlns:s="http://schemas.microsoft.com/sharepoint/">
<s:color name="BodyText" value="444444" />
<s:color name="SubtleBodyText" value="777777" />
<s:color name="StrongBodyText" value="262626" />
```

- Erstellen von benutzerdefinierten Farbschemas für SharePoint-Websites ist sehr einfache und kostengünstige implementieren und verwalten Sie die kurz- und langfristigen.
    + Denken Sie daran, die ein benutzerdefiniertes Farbschema ist nur ein Teil einer zusammengesetztes Design.
- Benutzerdefinierte Farbschemas bieten eine gewisse Flexibilität zu eine SharePoint-Website mit Branding versehen.
- Sie können Farbschemas über zusammengesetzten auf einer Ebene pro Website anwenden.
 
**Wann wird manuell erstellen ein Farbschema für ein SharePoint site geeignet?**

Diese Option funktioniert gut, wenn Ihre Bedürfnisse branding ein neues Farbschema enthalten benötigen, jedoch keine Änderung des Layouts oder ein- und Ausblenden von verschiedenen Office 365 SharePoint-Komponenten.

**Empfohlene bereitstellungsansätzen**

Sie können den Webbrowser verwenden oder das remote provisioning Muster zum Hochladen der Datei .spcolor das Tool auf einer SharePoint-Website erstellt.

<a name="create-a-font-scheme-for-a-sharepoint-theme-manually"></a>Erstellen Sie manuell ein Schriftartenschema für ein SharePoint-Design
----------------------------------------------------
Sie können auch die Schriftarten definieren, die Ihrer SharePoint-Website verwendet werden, indem Sie ein Schriftartenschema für Ihre SharePoint-Website machen.  Sie müssen die .spfont-Datei manuell mit einem Text-Editor wie Editor oder in Visual Studio erstellen.  Sie können einen Ausschnitt Beispiel aus einer .spfont-Datei weiter unten finden Sie unter.

```XML
<?xml version="1.0" encoding="utf-8"?>
<s:fontScheme name="Bodoni" previewSlot1="title" previewSlot2="body" xmlns:s="http://schemas.microsoft.com/sharepoint/">
    <s:fontSlots>
        <s:fontSlot name="title">
            <s:latin typeface="Bodoni Book" eotsrc="/_layouts/15/fonts/BodoniBook.eot" woffsrc="/_layouts/15/fonts/BodoniBook.woff" ttfsrc="/_layouts/15/fonts/BodoniBook.ttf" svgsrc="/_layouts/15/fonts/BodoniBook.svg" largeimgsrc="/_layouts/15/fonts/BodoniBookLarge.png" smallimgsrc="/_layouts/15/fonts/BodoniBookSmall.png" />
            <s:ea typeface="" />
            <s:cs typeface="Segoe UI Light" />
            <s:font script="Arab" typeface="Segoe UI Light" />
```

- Erstellen von benutzerdefinierten Schriftartenschemas für SharePoint-Websites ist sehr einfache und kostengünstige implementieren und verwalten Sie die kurz- und langfristigen.  
    + Denken Sie daran, ein benutzerdefiniertes Schriftartenschema ist nur ein Teil einer zusammengesetztes Design.
- Benutzerdefinierte Schriftartenschemas bieten eine gewisse Flexibilität zu eine SharePoint-Website mit Branding versehen.
- Können Sie Schriftartenschemas über zusammengesetzten unter Anwenden einer pro Websiteebene.

**Wenn ist Manuelles Erstellen eines benutzerdefinierten Schriftartenschemas für eine SharePoint site geeignet?**

Diese Option funktioniert gut, wenn Ihre Bedürfnisse branding ein neues Schriftartenschema enthalten benötigen, jedoch keine Änderung des Layouts oder ein- und Ausblenden von verschiedenen Office 365 SharePoint-Komponenten.

**Empfohlene bereitstellungsansätzen**

Webbrowser oder die remote provisioning Muster können Sie die .spfont-Datei in einer SharePoint-Website hoch.

<a name="use-javascript-embedding-to-show-and-hide-components-on-a-sharepoint-site"></a>Verwenden Sie zum ein- und Ausblenden von Komponenten auf einer SharePoint-Website Einbetten von JavaScript
-------------------------------------------------------------------------
Sie können zum Anwenden von benutzerdefiniertem branding auf SharePoint-Websites Einbetten von JavaScript verwenden.  Einbetten von JavaScript registriert JavaScript für alle Seiten auf einer SharePoint-Website ausgeführt.  Im Detail nutzt die JavaScript Einbetten von benutzerdefinierten Aktionen Script-Block Definitionen zugewiesen.  Diese benutzerdefinierten Aktionen zur SharePoint-Website hinzugefügt werden und bewirkt, dass der JavaScript-Code in das Skript blockiert ausführen.  Dieser Ansatz ermöglicht in lässt sich sagen JavaScript-Code ausführen.  In einem Szenario mit branding verwendet der JavaScript-Code in der Regel JQuery um das Modell DOM (Document Object) zu bearbeiten.

Finden Sie in diesem Artikel erfahren, wie [Anpassen der Benutzeroberfläche mithilfe von JavaScript für die SharePoint-Website](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).  

- Verwenden von JavaScript erfordert für SharePoint-Websites Einbetten von Zeit bis zur Implementierung und Wartung in die kurz- und langfristigen ein mittleres Maßes an.
- Verwenden von JavaScript bietet für SharePoint-Websites einbetten eine gute Maß an Flexibilität zu eine SharePoint-Website mit Branding versehen.
- Sie können die JavaScript Einbetten von auf einer Ebene pro Website anwenden.
- Wenn die minimale herunterladen /Strategy (MDS) für eine SharePoint-Website aktiviert ist, die Sie besonders sorgfältig vorgehen ergreifen müssen, um sicherzustellen, dass alle JavaScript einbetten, den Sie verwenden wird ordnungsgemäß ausgeführt.  Im oben genannten Artikel wird dies im Detail beschrieben.

**Verwendung von JavaScript passen Einbetten von zum ein- und Ausblenden von Komponenten auf einer SharePoint-Website eine gute?**

Diese Option funktioniert gut, wenn Sie anzeigen oder ausblenden oder Ändern von Elementen, die mit SharePoint stammen müssen.  Beispielsweise können Sie JavaScript zum Ersetzen von des oberen Navigationsleiste Out-of-Box-Steuerelements mit Ihrer eigenen benutzerdefinierten mithilfe der clientseitigen Navigations-Steuerelement einbetten.

**Empfohlene Bereitstellungsmethode**

Das remote provisioning Muster können Sie JavaScript eingebettet Änderungen an einer SharePoint-Website bereitstellen.

<a name="create-custom-master-pages-and-page-layouts-for-a-sharepoint-site"></a>Erstellen von benutzerdefinierten Gestaltungsvorlagen und Seitenlayouts für eine SharePoint-Website
-----------------------------------------------------------------
In Szenarien, in denen eine benutzerdefinierte Gestaltungsvorlage die einzige Möglichkeit zum Implementieren der benutzerdefinierten branding Anforderungen können Sie eine benutzerdefinierte Gestaltungsvorlage und Seitenlayouts erstellen.  Behalten Sie im Hinterkopf die Punkte am Anfang dieses Artikels in Bezug auf die langfristige Wartungskosten im Zusammenhang mit diesem Ansatz vorgenommen.

- Verwenden von benutzerdefinierten Gestaltungsvorlagen für SharePoint-Websites enthält die höchste Stufe der Anpassung (unbegrenzt).
- Verwenden von benutzerdefinierten Gestaltungsvorlagen für SharePoint-Websites erfordert die größte Zeitspanne zu implementieren und verwalten Sie die kurz- und langfristigen.
- Alle Änderungen an Out-of-Box-Masterseiten, die im Lieferumfang von Service-Updates werden nicht in benutzerdefinierten Gestaltungsvorlagen wiedergegeben werden.
- Sie können benutzerdefinierte Masterseiten auf einer Ebene pro Website anwenden.
- Wenn Sie eine benutzerdefinierte Gestaltungsvorlage verwenden wird empfohlen, die beginnen mit einem der Out-of Feld Masterseiten und entsprechend Ihren Anforderungen zu ändern.
    + Versuchen, den Umfang der Anpassung zu minimieren, die Sie mit benutzerdefinierten Gestaltungsvorlagen vornehmen, Dies erleichtert die aktualisieren, wenn Office 365-dienständerungen an, aus dem Feld Gestaltungsvorlagen in benutzerdefinierten Gestaltungsvorlagen repliziert werden müssen.  
- Befinden sich viele erforderlichen Inhaltsplatzhalter in SharePoint-Gestaltungsvorlagen, die nicht entfernt werden müssen, oder sie Seiten, Fehler verursacht.  Wenn Sie einen Platzhalter für den Inhalt erforderlichen, da die Minute es Bereitstellung und weisen Sie die Masterseite Ihrer Website, die Fehler angezeigt werden entfernt haben wissen Sie.

**Wann sind benutzerdefinierte Masterseiten und Seitenlayouts für eine SharePoint-Website geeignet?**
Diese Option funktioniert gut, wenn Ihre Bedürfnisse branding sehr spezifisch sind, oder Sie Veröffentlichungssites.

**Empfohlene bereitstellungsansätzen**

Benutzerdefinierte Masterseiten können manuell über den Webbrowser hochgeladen und zusammengesetzten manuell zugewiesen werden.

Benutzerdefinierte Masterseiten möglicherweise hochgeladen und einer SharePoint-Website über das remote provisioning Muster sowie zugewiesen werden.

<a name="create-a-composed-look-for-a-sharepoint-site"></a>Erstellen Sie ein zusammengesetztes Design für eine SharePoint-Website
----------------------------------------------
Ein zusammengesetztes Design enthält die oben beschriebenen .spcolor und .spfont-Dateien.  Es auch enthalten eine Gestaltungsvorlage und eines Hintergrundbilds.  Ein zusammengesetztes Design ist keine gepackte Anlage, die Sie für eine SharePoint-Website bereitstellen.  Vielmehr ist ein zusammengesetztes Design eines Listenelements in einer speziellen SharePoint-Liste, die URLs der Gestaltungsvorlage, .spcolor-Datei, .spfont-Datei und Hintergrundbild enthält.  Wenn Sie ein zusammengesetztes Design auf einer SharePoint-Website anwenden werden alle diese Elemente zur Implementierung der branding-Objekte, die das Erscheinungsbild des zum Verfassen definiert festgelegt.

Die folgende Abbildung zeigt ein zusammengesetztes Design für ein Office 365 SharePoint-Website über das Web-Browser erstellen. Prüfen Sie die Abschnitte in Orange hervorgehoben.  Diese Highlights Geben Sie die oben beschriebenen .spcolor und .spfont-Dateien an.  Es ist wichtig, beachten Sie, dass die Datei .spcolor als die Design-URL bezeichnet wird.  Dies gilt auch für die Beschreibung eines SharePoint-Designs für ein Office 365 SharePoint-Website.

![Die Felder zusammengesetztes Design: Titel enthält Meine Designs. Meine Themennamen enthält. Master-Seiten-URL enthält https://site.sharepoint.com/_catalogs/masterpage/seattle.master. Design-URL enthält https://site.sharepoint.com/_catalogs/theme/15/custom.spcolor mit .spcolor Orange hervorgehoben. Bild-URL enthält https://site.sharepoint.com/_catalogs/theme/15/custom-bg.jpg. Schriftart Schema URL enthält https://site.sharepoint.com/_catalogs/theme/15/custom.spfont mit .spfont Orange hervorgehoben. Anzeigereihenfolge enthält 100.](media/Recipes/Themes/new-theme-browser.png)

- Mithilfe von zusammengesetzten für SharePoint-Websites bietet eine gute Anpassung.
- Verwenden von zusammengesetzten für SharePoint-Websites erfordert wenig Zeit bis zur Implementierung und Wartung in die kurz- und langfristigen.
- Sie können zusammengesetzten auf einer Ebene pro Website anwenden.

**Beim Erstellen von eines zusammengesetzten Design für eine SharePoint-Website geeignet ist?**

Diese Option funktioniert gut, wenn Ihre branding Anforderungen nicht sehr spezifisch sind, und Sie nur sich für eine neue Farbschema Schriftartenschema und Hintergrundbild für Ihre Website interessieren.

Diese Option ist auch gut, wenn Sie eine benutzerdefinierte Gestaltungsvorlage zum Implementieren der Standarddateispeicherort branding einschließen müssen.

**Empfohlene bereitstellungsansätzen**

Können Sie die Ressourcen, die ein zusammengesetztes Design über den Webbrowser bilden, und klicken Sie dann das zusammengesetzte Design über den Webbrowser erstellen hochladen, oder Sie können das remote provisioning Muster verwenden, die Anlagen hochladen, die ein zusammengesetztes Design bilden, und erstellen sie in der SharePoint-Liste.

# <a name="specic-challenges-with-chosen-path"></a>Specic Probleme mit dem angegebenen Pfad #
In der folgenden Aufzählungszeichen sind, besondere Aspekte mit ausgewählten Muster verweisen, auch wenn der branding Ansatz für Ihre Bereitstellung entschieden werden berücksichtigt werden sollten.

- Office 365-Designs sind äußerst beschränkt und hauptsächlich Steuern der Seite Abschnitt Navigation suite
- SharePoint-Designs sind abhängig von der Zeit, die sie auf der Website angewendet werden. Wenn das ausgewählte Design auf SharePoint-Website angewendet wird erstellt dynamisch benötigte CSS-Dateien basierend auf den Spcolor und Spfont-Dateien. Dies kann Wartung Requirments führen, wenn neue CSS-Definitionen für die SharePoint-UI eingeführt werden.
- Alternative CSS-Ansatz basiert auf außerhalb der Knotenarten überschreiben. Als neue Oob CSS-Definitionen eingeführt werden, können sie Ihre Website beeinflussen, und Sie möglicherweise erforderlich sind, um Änderungen auf die betreffende benutzerdefinierte CSS-Datei zu übernehmen.
- Gestaltungsvorlagen werden immer basierend auf aus dem Feld Masterseiten erstellt. Wenn neue Steuerelemente oder Layout Strukturen auf der Feld Masterseiten out eingeführt werden, sind Sie möglicherweise gezwungen, firewallübergreifenden verwendeten Websites Ihrer sowie benutzerdefinierten Gestaltungsvorlagen zu aktualisieren.
 
<a name="summary"></a>Summary
-------
Im folgende Diagramm werden alle Optionen auf eine SharePoint-Website auf hoher Ebene mit Branding versehen zusammengefasst.

![Ein Balkendiagramm der Branding Optionen Funktion im Vergleich zu Kosten. Office 365-Designs haben sehr niedrige Kosten, Wartungskosten und Funktion Anpassung. Zusammengesetzten (Farbschemas, Schriftartenschemas) haben niedrig Anpassung Kosten und Wartungskosten mit wenig bis mittleren-Funktion. Farbschemas haben niedrig Anpassung Kosten-, Wartungskosten und Funktion. Schriftartenschemas haben niedrig Anpassung Kosten-, Wartungskosten und Funktion. Alternative CSS hat mittlere Anpassung Kosten-, Wartungskosten und Funktion. Einbetten von JavaScript/Einfügung hat mittlere Anpassung Kosten-, Wartungskosten und Funktion. Benutzerdefinierte Master-Shape Anpassung hohe Kosten, Wartungskosten und -Funktion verfügt.](media/Recipes/Themes/option-comparison-chart.png)

<a name="related-links"></a>Verwandte links
=============
- [Tool für SharePoint Farbe palette](http://www.microsoft.com/en-gb/download/details.aspx?id=38182)
- Hands-2015 - [ausführliche Behandlung von sicheren SharePoint-Branding in Office 365 mithilfe von wiederholbare Muster und Methoden](https://channel9.msdn.com/Events/Ignite/2015/BRK3164)
- [Anpassen der Benutzeroberfläche der SharePoint-Benutzeroberfläche mithilfe von JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Design Management mit CSOM (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.DeployCustomThemeWeb)
- [Set-Design auf Website (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.SetThemeToSite)
- [Beim Festlegen eines SharePoint-Designs in einer App für SharePoint (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.Themes)
- [Tätigen von sofort einsatzbereit Seattle master schnell (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.InjectResponsiveCSS)
- [AlternateCSSUrl und SiteLogoUrl-Eigenschaften in das Webobjekt (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)
- Beispiele und Inhalte am https://github.com/SharePoint/PnP

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013/2016 lokalen – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
