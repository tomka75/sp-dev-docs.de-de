---
title: Branding von Codeausschnitten mithilfe von CSS in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d18d07b6-1a6b-4589-a65c-932b67cef595
ms.openlocfilehash: 4ed891c06956c4d2ff79cd681b81a3869a03cc3c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="brand-snippets-by-using-css-in-sharepoint"></a>Branding von Codeausschnitten mithilfe von CSS in SharePoint

Um einen Codeausschnitt zu formatieren, überschreiben Sie die Standardformatvorlagen mit benutzerdefiniertem CSS. Sie können CSS-IDs und Elementselektoren verwenden, um alle auf Elemente angewendeten Standardformatvorlagen zu überschreiben, oder Sie können einen HTML-Editor oder ein Tool wie die F12-Entwicklertools in Internet Explorer verwenden, um bestimmte Standardformatvorlagen zu identifizieren und zu überschreiben.

## <a name="introduction-to-styling-snippets-with-css"></a>Einführung in die Formatierung von Codeausschnitten mit CSS
<a name="Introduction"> </a>

Nachdem Sie eine HTML-Masterseite konvertiert oder ein HTML-Seitenlayout erstellt haben, können Sie diese Seite in der serverseitigen Vorschau des Entwurfs-Managers anzeigen. Von der Vorschauseite aus können Sie zum Codeausschnittkatalog navigieren und dann Codeausschnitte in die HTML-Datei kopieren. Ein Ausschnitt ist eine HTML-Darstellung eines SharePoint-Steuerelements, z. B. ein Steuerelement der oberen Navigationsleiste oder ein Suchfeld.
  
    
    
Nachdem Sie einen Codeausschnitt in die HTML-Datei auf dem zugeordneten Laufwerk kopiert und dann die Änderungen gespeichert haben, können Sie die serverseitige Vorschau der HTML-Datei aktualisieren, um zu sehen, wie das Steuerelement gerendert wird. Codeausschnitte enthalten Markup, das eine Entwurfszeitvorschau in Ihrem gewünschten HTML-Editor bereitstellt, Sie sollten dieses Markup jedoch nicht bearbeiten, da es schreibgeschützt ist und Auswirkungen darauf hat, wie das Steuerelement auf dem Server gerendert wird. Die serverseitige Vorschau hingegen ist eine Vorschau in voller Genauigkeit mit Live-Daten, falls verfügbar, ein Navigationssteuerelement zeigt z. B. die aktuelle Navigationsstruktur der Website mit Live-Daten aus Ihrer Datenquelle, z. B.ein SharePoint-Terminologiespeicher für die verwaltete Navigation.
  
> [!NOTE]
> Weitere Informationen zum Zuordnen eines Netzlaufwerks finden Sie unter [Vorgehensweise: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md). 
  
    
    

Codeausschnitte erben ihre Formatvorlagen standardmäßig von SharePoint-Formatvorlagen, z. B. „corev15.css“. Um einen Codeausschnitt zu formatieren, müssen Sie diese Formatvorlagen mit Ihrem benutzerdefiniertem CSS überschreiben. Zu diesem Zweck können Sie folgende Aktionen ausführen:
  
    
    

- Verwenden Sie CSS-IDs und Elementselektoren, um die auf die ausgewählten Elemente angewendeten Formatvorlagen vollständig zu überschreiben.
    
  
- Verwenden Sie browserbasierte Tools wie die F12-Entwicklertools in Internet Explorer, um die standardmäßigen Formatvorlagen in der serverseitigen Vorschau im Entwurfs-Manager zu prüfen, und identifizieren Sie dann bestimmte Formatvorlagen, die überschrieben werden sollen.
    
  
- Verwenden Sie die Funktionen Ihres HTML-Editors, um die Standardformatvorlagen in der schreibgeschützten Vorschau eines Codeausschnitts zu prüfen, und identifizieren Sie dann bestimmte Formatvorlagen zum Überschreiben. 
    
  
Um die Standardformatvorlagen mithilfe der Entwicklertools in Internet Explorer zu identifizieren, sollten Sie die serverseitige Vorschau im Entwurfs-Manager verwenden, um Ihre HTML-Masterseite oder das Seitenlayout anzuzeigen. Drücken Sie **F12**, um die Entwicklertools zu starten, wählen Sie das Menü **Suchen** aus, und wählen Sie dann **Element durch Klicken auswählen** aus. Dadurch können Sie auf Element auf der Seite klicken und genau sehen, welche Formatvorlagen überschrieben werden sollen, indem Sie CSS zu der benutzerdefinierten Formatvorlage hinzufügen, mit der Ihre HTML-Masterseite oder das Seitenlayout verknüpft ist.
  
    
    
Die standardmäßigen SharePoint-Formatvorlagen enthalten viele Formatvorlagen, aufgrund derer es schwierig ist, bestimmte Formate zu identifizieren. Als Alternative zu browserbasierten Tools und in Abhängigkeit von Ihrem HTML-Editor ist es vielleicht einfacher, den Codeausschnitt aus dem Codeausschnittkatalog in Ihre HTML-Datei zu kopieren und dann den HTML-Editor zum Identifizieren von Formatvorlagen zu verwenden. Wenn Sie im Codeausschnittkatalog **Aktualisieren** und dann **In Zwischenablage kopieren** auswählen, enthält der Codeausschnitt eine HTML-Vorschau dieses Codeausschnitts. Nachdem Sie den Codeausschnitt in Ihre HTML-Datei kopiert haben, können Sie die in der schreibgeschützten Vorschau verwendeten Formatvorlagen überprüfen, die im Codeausschnitt enthalten sind. Auf diese Weise analysieren Sie eine kleinere Teilmenge der Standardformatvorlagen.
  
    
    
In Abhängigkeit von dem Codeausschnitt und dem Umfang Ihrer Anpassung, möchten Sie vielleicht CSS-IDs und Elementselektoren verwenden, um alle Standardformatvorlagen vollständig zu überschreiben anstatt bestimmte Formatvorlagen für das Überschreiben auszuwählen. Im folgenden Beispiel wird veranschaulicht, wie diese Methode verwendet wird, um benutzerdefinierte Formatvorlagen auf den Codeausschnitt für die obere Navigationsleiste anzuwenden.
  
    
    

## <a name="example-style-the-top-navigation-snippet"></a>Beispiel: Codeausschnitt zum Formatieren der oberen Navigationsleiste
<a name="Example"> </a>

Der Codeausschnitt für die obere Nagivationsleiste ist einer der am häufigsten verwendeten Codeausschnitte, er ist daher auch einer der häufigsten Branding-Codeausschnitte. Auf einer SharePoint-Website können Sie eine Option zum Verwenden der verwalteten Navigation auswählen, sodass ein Terminologiespeicher die Datenquelle für den Codeausschnitt der oberen Navigationsleiste wird. Auf diese Weise können Sie das Terminologiespeicher-Verwaltungstool unter **Websiteeinstellungen** verwenden, um Navigationsausdrücke hinzuzufügen oder zu löschen und die Navigationstaxonomie zu verwalten, die vom Codeausschnitt für die obere Navigationsleite angezeigt wird.
  
    
    
In diesem Beispiel verwendet die Website die verwaltete Navigation, die obere Navigationsleiste ruft ihre Einträge also von einem Terminologiespeicher ab. Es gibt eine Ebene von Flyouts, die angezeigt werden, wenn Sie den Mauszeiger über einen Navigationsausdruck der obersten Ebene bewegen, z. B. **Computer**. In diesem Abschnitt wird veranschaulicht, wie diese benutzerdefinierten Formatvorlagen die SharePoint-Standardformatvorlagen überschreiben.
  
    
    

### <a name="sample-1-navigation-div-from-the-html-mockup-file"></a>Beispiel 1: Navigation \<div\> aus der HTML-Modelldatei

Bevor Sie beim Entwerfen des HTML-Modells für Ihre Masterseite den Entwurfs-Manager verwenden, werden Sie wahrscheinlich HTML und CSS zum Entwerfen eines funktionalen Elements der oberen Navigationsleiste verwenden. In diesem HTML-Beispiel wird eine grundlegende Struktur für die obere Navigationsleiste verwendet: ein **\<div\>**-Element mit einer ID und einem Klassennamen, eine Liste für die Einträge der oberen Navigationsleiste und eine verschachtelte Liste für jedes Flyout-Untermenü.
  
    
    

```HTML

<div id="navigation" class="msax-Navigation">
   <ul>
      <li><a href="#">Cameras</a>
         <ul>
            <li><a href="#">Camcorders</a></li>
            <li><a href="#">Digital cameras</a></li>
            <li><a href="#">Disposable cameras</a></li>
            <li><a href="#">Film cameras</a></li>
         </ul>
      </li>
      <li><a href="#">Computers</a>
         <ul>
            <li><a href="#">Desktops</a></li>
            <li><a href="#">Laptops</a></li>
            <li><a href="#">Netbooks</a></li>
            <li><a href="#">Tablets</a></li>
         </ul>
      </li>
      <li><a href="#">Media</a>
         <ul>
            <li><a href="#">Movies</a></li>
            <li><a href="#">Music</a></li>
            <li><a href="#">TV shows </a></li>
            <li><a href="#">Video games </a></li>
         </ul>
      </li>
      <li></li>
   </ul>
</div>

```


### <a name="sample-2-navigation-div-styled-with-custom-css"></a>Beispiel 2: Navigation \<div\> formatiert mit benutzerdefiniertem CSS

Um die SharePoint-Standardformatvorlagen zu überschreiben, fügen Sie in die HTML-Modelldatei einen Standardlink zu Ihrer CSS-Datei `(<link rel="stylesheet" type="text/css" href="URLtoYourCustomCSSFile"/>` ein, unmittelbar vor dem schließenden **\</head\>**-Tag.
  
    
    
Beachten Sie in diesen HTML-und CSS-Beispielen Folgendes:
  
    
    

- Navigationseinträge werden mithilfe des Formats `.msax-Navigation ul li` formatiert, anstatt Klassen direkt auf die ** \<uI\>**- oder **\<li\>**-Tags anzuwenden.
    
  
- Formatvorlagen verwenden die Syntax `.msax-Navigation ul li` anstelle von `.msax-Navigation ul>li`, da das Codeausschnitt-Markup möglicherweise intervenierende **\<div\>**-Tags zwischen den ausgewählten Elementen enthält.
    
  
- Der HTML-Modell enthält ein leeres **\<li\>\</li\>**- Element als letzten Eintrag von **\<ul\>** auf oberster Ebene. Dies liegt daran, dass SharePoint bei aktivierter verwalteter Navigation den Befehl **Links bearbeiten** als letzten Eintrag für die obere Navigationsleiste hinzufügt, und die finale Website muss diese Option in der Regel nicht anzeigen. Das CSS-Beispiel verwendet `.msax-Navigation ul li:last-child`, um diesen Eintrag auszuwählen und den Anzeigewert auf `none` festzulegen. Das leere **\<li\>\</li\>**-Element in der HTML-Datei ist ein temporärer Ersatz für den standardmäßigen Eintrag **Links bearbeiten**. Beachten Sie dieses finale **\<li\>**-Element, wenn Ihre Website die verwaltete Navigation und CSS `li:last-child`-Selektoren verwendet.
    
  



```HTML

.msax-Navigation {
margin: 10px 0px; top: 0px; position: relative;
z-index:200;
}
.msax-Navigation a {
margin: 0px; padding: 0px; border: 0px currentColor;
}
.msax-Navigation ul {
list-style: none; margin: 0px; padding: 0px; font-size: 16px; z-index:200;
}
.msax-Navigation ul li {
padding: 10px; display: inline-block; position: relative; z-index:200;
}
.msax-Navigation ul li:first-child {
margin: 0px;
}
.msax-Navigation ul li:last-child {
margin: 0px; padding: 0px; display: none;
}
.msax-Navigation ul li a.selected, .msax-Navigation ul li.selected {
background-color: rgb(58,60,62) !important;
color:rgb(255,255,255) !important;
}
.msax-Navigation ul li a {
width: 100%; color: rgb(58,60,62); font-size: 16px;
}
.msax-Navigation ul li:hover {
background-color: rgb(58,60,62);
color:rgb(255,255,255) !important;
}
.msax-Navigation ul li a:hover {
text-decoration: none;
color:rgb(255,255,255) !important;
}
.msax-Navigation li ul {
left: 0px; top: 35px; display: none; position: absolute; min-width: 100px; box-shadow: 5px 5px 10px 0px rgb(0,0,0); background-color: rgb(58,60,62);
}
.msax-Navigation li:hover ul {
display: block; z-index: 150;
}
.msax-Navigation li li {
margin: 0px; padding: 5px 10px 5px 0px; border-top-width: 0px; display: block; min-width: 100px;
}
.msax-Navigation li li:last-child {
margin: 0px; padding: 5px 10px 5px 0px; border-top-width: 0px; display: block; min-width: 100px;
}
.msax-Navigation li li a {
width: 100%; padding-left: 10px; display: block; color:rgb(255,255,255) !important;
}
.msax-Navigation li li:hover {
background-color: rgb(120, 120, 120);
}

```


### <a name="sample-3-read-only-preview-of-the-top-navigation-snippet"></a>Beispiel 3: Schreibgeschützte Vorschau des Codeausschnitts der oberen Navigationsleiste

Nachdem Ihre benutzerdefinierten Formatvorlagen im HTML-Modell implementiert wurden und Sie über ein funktionales Element der oberen Navigationsleiste verfügen, führen Sie die üblichen Schritte aus:
  
    
    

1. Ordnen Sie ein Netzlaufwerk zu.
    
  
2. Laden Sie Ihre Designdateien hoch.
    
  
3. Konvertieren Sie die HTML-Datei in eine Masterseite.
    
  
4. Zeigen Sie Probleme in der Vorschau an, und korrigieren Sie sie.
    
  
5. Fügen Sie den Codeausschnitt der oberen Navigationsleiste in die HTML-Masterseite mithilfe des Codeausschnittkatalog ein.
    
  
Beachten Sie im Codeausschnittkatalog Folgendes, wenn Sie die Eigenschaften des Codeausschnitts der oberen Navigationsleiste konfigurieren:
  
    
    

- Nehmen Sie im Bereich **Wichtig** am oberen Rand keine Änderungen an der **CssClass**-Eigenschaft vor.
    
  
- Nehmen Sie keine Änderungen an Eigenschaften unter der Überschrift **AjaxDelta** vor, da diese Eigenschaften im Zusammenhang mit den MDS-Eigenschaften stehen, die SharePoint verwendet, um den HTML-Codeausschnitt in den entsprechenden ASP.NET-Codeausschnitt zu konvertieren. Dies gilt für alle Codeausschnitte, nicht nur für den Codeausschnitt der oberen Navigationsleiste.
    
  
- Wenn Sie beabsichtigen, die SharePoint-Standardformatvorlagen zu überschreiben, legen Sie Codeausschnittkatalog im Abschnitt **Behavior** unter **AspMenu** (wenn der Codeausschnitt mehrere Steuerelemente enthält, z. B. ein delegate-Steuerelement, sind möglicherweise mehrere Abschnitte **Behavior** vorhanden) die Option **ClientIDMode** auf **Static**. Wenn Sie die Option **ClientIDMode** auf die Standardeinstellung **Inherit** festgelegt lassen, ändern sich die angewendeten CSS-Klassen des Codeausschnitts basierend auf der Sortierung der Codeausschnitte auf der Seite. Weitere Informationen zu **ClientIDMode** finden Sie unter [Control.ClientIDMode-Eigenschaft]((http://msdn.microsoft.com/de-DE/library/system.web.ui.control.clientidmode.aspx)).
    
    Standardmäßig verwendet das Steuerelement der oberen Navigationsleiste beispielsweise standardmäßige SharePoint-ID-Attribute wie **zz5_TopNavigationMenu** und **zz6_RootAspMenu**. Durch Ändern von **ClientIDMode** in **Static** ermöglichen Sie die Verwendung dieser Standard-IDs als Selektoren in Ihrer eigenen CSS, um die SharePoint-Standardformatvorlagen zu überschreiben.
    
  
- Einige Eigenschaften sind bereits so konfiguriert, dass das Branding des Codeausschnitts der oberen Navigationsleiste vereinfacht wird, indem die standardmäßigen Verhaltensweisen von dynamischem CSS und JavaScript eliminiert werden. **UseSimpleRendering** wird beispielsweise standardmäßig auf **True** festgelegt, und **MaximumDynamicDisplayLevels** wird auf **0** festgelegt. Weitere Informationen zu bestimmten Eigenschaften des Codeausschnitts der oberen Navigationsleiste finden Sie unter [AspMenu-Eigenschaften]((http://msdn.microsoft.com/de-DE/library/ms412476.aspx)) und [Menu-Eigenschaften]((http://msdn.microsoft.com/de-DE/library/282668a1.aspx)).
    
  
Nachdem Sie den Codeausschnitt der oberen Navigationsleiste im Codeausschnittkatalog konfiguriert haben, wählen Sie **Aktualisieren** und dann **In die Zwischenablage kopieren** aus. Löschen Sie auf der HTML-Masterseite den Inhalt der Navigation `<div id="navigation" class="msax-Navigation">`, die das Modellsteuerelement enthält (löschen Sie nur den Inhalt des **\<div\>**-Tags und nicht das **\<div\>**-Tag selbst), und kopieren Sie dann den Codeausschnitt in die Navigation **\<div\>**. Ändern Sie, falls erforderlich, die Position der **\<#div\>**-Navigation, in der Regel direkt nach Beginn des `<div id="s4-bodyContainer">`-Tags, jedoch vor dem **\<#div\>** mit `PlaceHolderMain`.
  
    
    
Für einen einfachen Vergleich mit dem HTML-Code der **\<#div\>**-Navigation oben, enthält das folgende Beispiel den **\<div\>**-Teil der Navigation des Codeausschnitts der oberen Navigationsleiste. Beachten Sie, dass dies nicht der gesamte Codeausschnitt ist.
  
    
    



```HTML

<div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox">
     <ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static">
          <li class="static">
          <a accesskey="1" class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Cameras</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/camcorders" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Camcorders</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/digital-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Digital cameras</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/disposable-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Disposable cameras</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/film-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Film cameras</span></span></a></li>
          </ul>
          </li>
          <li class="static">
          <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Computers</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/desktops" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Desktops</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/laptops" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Laptops</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/netbooks" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Netbooks</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/tablets" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Tablets</span></span></a></li>
          </ul>
          </li>
          <li class="static">
          <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Media</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/movies" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Movies</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/music" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Music</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/tv-shows" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">TV shows</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/video-games" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Video games</span></span></a></li>
          </ul>
          </li>
          <li class="static ms-verticalAlignTop ms-listMenu-editLink ms-navedit-editArea">
          <span id="zz7_TopNavigationMenu_NavMenu_Edit" class="ms-navedit-editSpan">
          <a id="zz7_TopNavigationMenu_NavMenu_EditLinks" class="ms-navedit-editLinksText" href="#" onclick="g_QuickLaunchMenu = null; EnsureScriptParams('quicklaunch.js', 'QuickLaunchInitEditMode', 'zz7_TopNavigationMenu', 2, 0, 0, ''); cancelDefault(event); return false;">
          <span class="ms-displayInlineBlock">
          <span class="ms-navedit-editLinksIconWrapper ms-verticalAlignMiddle">
          <img class="ms-navedit-editLinksIcon" src="/_layouts/15/images/spcommon.png?rev=23" /></span><span class="ms-metadata ms-verticalAlignMiddle">Edit Links</span></span></a><span id="zz7_TopNavigationMenu_NavMenu_Loading" class="ms-navedit-menuLoading ms-hide"><a id="zz7_TopNavigationMenu_NavMenu_GearsLink" href="#" onclick="HideGears(); return false;" title="This animation indicates the operation is in progress. Click to remove this animated image."><img id="zz7_TopNavigationMenu_NavMenu_GearsImage" src="/_layouts/15/images/loadingcirclests16.gif?rev=23" /></a></span><div id="zz7_TopNavigationMenu_NavMenu_ErrorMsg" class="ms-navedit-errorMsg">
          </div>
          </span></li>
     </ul>
</div>

```

Anstatt nur benutzerdefinierte Formatvorlagen zu verwenden, kann es möglicherweise ein Szenario geben, in dem Sie nur eine bestimmte Formatvorlage überschreiben möchten. Um beispielsweise den Knoten **Links bearbeiten** auszublenden, können Sie eine benutzerdefinierte Formatvorlage erstellen, die die Standard-ID **zz7_TopNavigationMenu_NavMenu_Edit** verwendet, um die Anzeigeeinstellung auf `none` festzulegen.
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="Additional"> </a>


-  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md)
    
  
-  [Übersicht über den Entwurfs-Manager in SharePoint](overview-of-design-manager-in-sharepoint.md)
    
  
-  [Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
    
  

