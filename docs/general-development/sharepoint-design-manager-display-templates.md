---
title: Anzeigevorlagen im SharePoint-Entwurfs-Manager
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1a782bac-48ee-4baf-8751-0f943a306e0f
ms.openlocfilehash: 337336c6d40db8db4cab7b73f070cf2a6ab59e08
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-design-manager-display-templates"></a>Anzeigevorlagen im SharePoint-Entwurfs-Manager
Hier finden Sie Informationen zu Anzeigevorlagen. Es wird erläutert, in welchem Zusammenhang diese mit Suche-Webparts stehen, wie die Vorlagen strukturiert sind, wie Eigenschaften zugeordnet und Variablen und jQuery verwendet werden und wie eine benutzerdefinierte Anzeigevorlage in SharePoint erstellt wird.
## <a name="introduction-to-display-templates"></a>Einführung in Anzeigevorlagen
<a name="bk_introduction"> </a>

Anzeigevorlagen in SharePoint sind Vorlagen in Webparts, die Suchtechnologie verwenden (in diesem Artikel als Suche-Webparts bezeichnet), um die Ergebnisse einer Abfrage des Suchindex anzuzeigen. Anzeigevorlagen steuern, welche verwalteten Eigenschaften in den Suchergebnissen angezeigt werden und wie diese im Webpart angezeigt werden. Jede Anzeigevorlage besteht aus zwei Dateien: einer HTML-Version der Anzeigevorlage, die Sie im HTML-Editor bearbeiten können, und einer .js-Datei, die SharePoint verwendet.
  
> [!NOTE]
> Nur Such-Webparts können Anzeigevorlagen verwenden. Das Inhaltsabfrage-Webpart ist nicht suchgesteuert und verwendet daher keine Anzeigevorlagen. 
  
    
    

Sie können vorhandene Anzeigevorlagen im Entwurfs-Manager anzeigen. Sie können sie aber nicht auf die gleiche Weise im Entwurfs-Manager erstellen, wie Sie Gestaltungsvorlagen und Seitenlayouts erstellen. Stattdessen gehen Sie folgendermaßen vor:
  
    
    

- Öffnen Sie Ihr  [dem Gestaltungsvorlagenkatalog zugeordnetes Netzwerklaufwerk](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
    
  
- Öffnen Sie einen der vier Ordner im Ordner **Anzeigevorlagen** .
    
    > [!NOTE]
    > Der Ordner Ihrer Wahl hängt vom Typ der zu verwendenden Anzeigevorlage ab. Wenn Ihre Website beispielsweise websiteübergreifende Veröffentlichung verwendet, kopieren Sie eine Anzeigevorlage aus dem Ordner **Inhalt-WebParts**. Weitere Informationen finden Sie unter [Anzeigen der Vorlagenreferenz in SharePoint Server](http://technet.microsoft.com/de-DE/library/jj944947.aspx). 

- Kopieren Sie die HTML-Datei für eine vorhandene Anzeigevorlage, die derjenigen ähnelt, die Sie erstellen möchten. Der genaue Speicherort, an den Sie die Datei kopieren, ist nicht wichtig, solange sich dieser im **Gestaltungsvorlagenkatalog** befindet.
    
  
- Öffnen und ändern Sie Ihre Kopie in einem HTML-Editor.
    
  
Wenn Sie eine vorhandene Anzeigevorlage als Ausgangspunkt für eine neue Anzeigevorlage verwenden, können Sie von den hilfreichen Informationen zum Anpassungsprozess in den Kommentaren der Standardanzeigevorlagen profitieren, und Sie verfügen über einen Rahmen für einfache Aufgaben wie das Zuordnen von Eingabefeldern. Außerdem ist durch diese Vorgehensweise sichergestellt, dass Ihre Vorlagen die richtige grundlegende Seitenstruktur verwenden.
  
    
    
Wenn Sie durch Kopieren der HTML-Datei für eine vorhandene Anzeigevorlage im Ordner **Anzeigevorlagen** im **Gestaltungsvorlagenkatalog** eine Anzeigevorlage erstellen, gilt Folgendes:
  
    
    

- Eine .js-Datei mit demselben Namen wird  an dem Ort erstellt, an den Sie die HTML-Datei kopiert haben.
    
  
- Sämtliches Markup, das SharePoint benötigt, wird der.js-Datei hinzugefügt, sodass die Anzeigevorlage korrekt angezeigt wird.
    
  
- Die HTML-Datei und die JS-Datei werden verknüpft, sodass spätere Änderungen an der HTML-Datei mit der JS-Datei synchronisiert werden, wenn die HTML-Datei gespeichert wird.
    
> [!NOTE]
> Die Synchronisierung erfolgt nur in eine Richtung. Änderungen an der HTML-Anzeigevorlage werden mit der verknüpften JS-Datei synchronisiert. Anders als bei Gestaltungsvorlagen und Seitenlayouts können Sie beim Arbeiten mit Anzeigevorlagen nicht nur mit der JS-Datei arbeiten, indem Sie die Verknüpfung zwischen den Dateien aufheben. Sie müssen sämtliches HTML und JavaScript in die HTML-Datei eingeben. 
  
    
    


## <a name="understanding-the-relationship-between-display-templates-and-search-web-parts"></a>Grundlegendes zur Beziehung zwischen Anzeigevorlagen und Suche-Webparts
<a name="bk_DTandSWP"> </a>

Es gibt grundsätzlich zwei Arten von Anzeigevorlagen:
  
    
    

- **Steuerelementvorlagen** bestimmen die allgemeine Struktur der Präsentation der Ergebnisse. Sie umfassen Listen, Listen mit Paging und Diaschauen.
    
  
- **Elementvorlagen** bestimmen, wie jedes Ergebnis im Satz angezeigt wird. Beinhaltet Bilder, Text, Video und andere Elemente.
    
  
Weitere Informationen zu diesen und anderen Anzeigevorlagen finden Sie unter  [Referenz der Anzeigevorlagen in SharePoint](http://technet.microsoft.com/de-DE/library/jj944947.aspx).
  
    
    
Nachdem Sie einer Seite ein Such-Webpart (wie z. B. das Inhaltssuche-Webpart) hinzugefügt haben, wählen Sie zum Konfigurieren des Webparts sowohl eine Steuerelementvorlage als auch eine Elementanzeigevorlage aus (siehe Abbildung 1).
  
    
    

**Abbildung 1. Toolbereich des Inhaltssuche-Webparts**

  
    
    

  
    
    
![Toolbereich des Inhaltssuche-Webparts](../images/115_content_search_web_part_tool_pane.gif)
  
    
    
Die Steuerelementvorlage stellt HTML bereit, um das allgemeine Layout so zu strukturieren, wie die Suchergebnisse präsentiert werden sollen. So stellt die Steuerelementvorlage möglicherweise das HTML für eine Kopfzeile und Beginn und Ende einer Liste bereit. Die Steuerelementvorlage wird im Webpart nur einmal gerendert.
  
    
    
Die Elementanzeigevorlage stellt HTML bereit, das die Anzeige jedes Elements im Ergebnissatz bestimmt. So stellt die Elementanzeigevorlage möglicherweise das HTML für ein Listenelement bereit, das ein Bild und drei Zeilen Text enthält, die unterschiedlichen verwalteten Eigenschaften zugeordnet sind, die mit dem Element verknüpft sind. Die Elementanzeigevorlage wird für jedes Element im Ergebnissatz einmal gerendert. Wenn der Ergebnissatz zehn Elemente enthält, erstellt die Anzeigevorlage daher ihren HMTL-Abschnitt zehnmal.
  
    
    
Wenn die Steuerelement- und die Elementanzeigevorlage auf diese Art und Weise zusammen verwendet werden, wird ein zusammenhängender HTML-Block erstellt, der im Webpart gerendert wird (siehe Abbildung 2).
  
    
    

**Abbildung 2. Kombinierte HTML-Ausgabe einer Steuerelementanzeigevorlage und einer Elementanzeigevorlage**

  
    
    

  
    
    
![Kombinierte HTML-Ausgabe einer Steuerelementanzeigevorlage und einer Elementanzeigevorlage](../images/sp15Con_CreateDisplayTemplateSP2013_Figure02.png)
  
    
    
Weitere Informationen zu Anzeigevorlagen finden Sie in Artikel  [Übersicht über das SharePoint-Seitenmodell](overview-of-the-sharepoint-page-model.md) im Abschnitt "Suchgesteuerte Webparts und Anzeigevorlagen".
  
    
    

## <a name="understanding-the-display-template-structure"></a>Grundlegendes zur Anzeigevorlagenstruktur
<a name="bk_DTstructure"> </a>

Die HTML-Datei, die für eine Anzeigevorlage verwendet wird, ist ein vollständiges HTML-Dokument, stellt aber keine vollständige HTML-Webseite dar. SharePoint wandelt die Teile der HTML-Anzeigevorlagendatei in JavaScript um. In diesem Abschnitt werden die vier wichtigsten Abschnitte einer Anzeigevorlage beschrieben.
  
    
    

### <a name="title-tag"></a>Tag „title“

Der Text im Tag **\<title\>** in einer Anzeigevorlagendatei wird als der Anzeigename im Abschnitt **Anzeigevorlagen** des Webpart-Bearbeitungsbereichs verwendet, wenn sich das Suche-Webpart im Bearbeitungsmodus befindet.  Das folgende Beispiel bezieht sich auf die Elementanzeigevorlage mit dem Namen „Item_Picture3Lines.html“":
  
    

```HTML

<title>Picture on left, 3 lines on right</title>
```


### <a name="header-properties"></a>Eigenschaften der Kopfzeile

Direkt nach dem Tag **\<title\>** findet sich ein Satz benutzerdefinierter Elemente, die mit folgendem Markup versehen sind:
  
    
    

```HTML
<!--[if gte mso 9]><xml>
<mso:CustomDocumentProperties>
…
</mso:CustomDocumentProperties>
</xml><![endif]-->

```

Diese Elemente und deren Eigenschaften liefern der SharePoint-Umgebung wichtige Informationen zur Anzeigevorlage. Tabelle 1 beschreibt die benutzerdefinierten Eigenschaften, die in Anzeigevorlagen verwendet werden.
  
> [!NOTE]
> Nicht alle benutzerdefinierten Eigenschaften werden in jeder Anzeigevorlage verwendet. Außerdem können einige Eigenschaften geändert werden, indem die Eigenschaften der Anzeigevorlagendatei im Entwurfs-Manager bearbeitet werden. 
  
    
    


**Tabelle 1. Liste der CustomDocumentProperties-Einträge**


|**Eigenschaft**|**Beschreibung**|
|:-----|:-----|
|**TemplateHidden** <br/> |Boolescher Wert, der angibt, ob die Anzeigevorlage in der Liste verfügbarer Vorlagen im Webpart ausgeblendet werden soll. Dieser Wert kann in den Eigenschaften der Anzeigevorlagendatei geändert werden.  <br/> |
|**ManagedPropertyMapping** <br/> |Ordnet Felder, die von Suchergebniselemente verfügbar gemacht werden, für JavaScript verfügbaren Eigenschaften zu. Wird nur in Elementvorlagen verwendet.  <br/> |
|**MasterPageDescription** <br/> |Liefert eine benutzerfreundliche Beschreibung der Anzeigevorlage. Diese wird Benutzern in der SharePoint-Bearbeitungsumgebung angezeigt. Dieser Wert kann in den Eigenschaften der Anzeigevorlagendatei geändert werden.  <br/> |
|**ContentTypeId** <br/> |Die ID des mit der Anzeigevorlage verknüpften Inhaltstyps.  <br/> |
|**TargetControlType** <br/> |Gibt den Kontext an, in dem die Anzeigevorlage verwendet wird. Dieser Wert kann in den Eigenschaften der Anzeigevorlagendatei geändert werden.  <br/> |
|**HtmlDesignAssociated** <br/> |Boolesche Wert, der angibt, ob mit einer HTML-Anzeigevorlagendatei eine JS-Datei verknüpft ist.  <br/> |
|**HtmlDesignConversionSucceeded** <br/> |Gibt an, ob der Konvertierungsprozess erfolgreich war. Dieser Wert wird der Datei von SharePoint automatisch hinzugefügt und wird nur in benutzerdefinierten Anzeigevorlagen verwendet.  <br/> |
|**HtmlDesignStatusAndPreview** <br/> |Enthält die URL zur HTML-Datei und den Text für die Spalte **Status** (entweder **Konvertierung erfolgreich** oder **Warnungen und Fehler**). Dieser Wert wird der Datei von SharePoint automatisch hinzugefügt und wird nur in benutzerdefinierten Anzeigevorlagen verwendet.  <br/> |
   

### <a name="script-block"></a>Skriptblock
<a name="bk_scriptblock"> </a>

Im Tag **\<body\>** sehen Sie das folgende **\<script\>**-Tag:
  
    
    

```HTML

<script>
     $includeLanguageScript(this.url, "~sitecollection/_catalogs/masterpage/Display Templates/Language Files/{Locale}/CustomStrings.js");
</script>
```

Standardmäßig ist diese Zeile in allen Anzeigevorlagen enthalten. Sie können weitere Codezeilen im Tag ** \<script\> ** hinzufügen, um CSS-Dateien oder andere JavaScript-Dateien außerhalb Ihrer HTML-Datei für die Hauptanzeigevorlage zu referenzieren. Tabelle 2 zeigt Beispiele, wie Sie andere Ressourcen einschließen.
  
    
    

**Tabelle 2. Beispiele für das Einschließen externer Ressourcen in das Tag \<script\>**


|**Wenn Sie Folgendes einschließen möchten:**|**Verwenden Sie den folgenden Code:**|
|:-----|:-----|
|Eine JavaScript-Datei, die Teil der aktuellen Websitesammlung ist  <br/> | `$includeScript(this.url, "~sitecollection/_catalogs/masterpage/Display Templates/Content Web Parts/MyScripts.js");` <br/> |
|Eine externe JavaScript-Datei  <br/> | `$includeScript(this.url, "http://www.contoso.com/ExternalScript.js");` <br/> |
|Eine CSS-Datei, die Teil der aktuellen Websitesammlung ist  <br/> | `$includeCSS(this.url, "~sitecollection/_catalogs/masterpage/Display Templates/Content Web Parts/MyCSS.css");` <br/> |
|Eine CSS-Datei, die sich an einem Speicherort relativ zur aktuellen Anzeigevorlage befindet  <br/> | `$includeCSS(this.url,"../../MyStyles/MyCSS.css");` <br/> |
   
> [!NOTE]
> Wenn für Elemente im Gestaltungsvorlagenkatalog eine **Inhaltsgenehmigung** erforderlich ist, müssen alle Ressourcendateien (einschließlich CSS- und .js-Dateien) veröffentlicht werden, bevor sie für Gestaltungsvorlagen und Seitenlayouts verfügbar sind. Weitere Informationen finden Sie unter [Festlegen einer Genehmigungsanforderung für Elemente in einer Websiteliste oder -bibliothek](http://office.microsoft.com/en-us/sharepoint-help/require-approval-of-items-in-a-site-list-or-library-HA102853936.aspx?CTT=1). 
  
    
    


### <a name="div-block"></a>DIV-Block
<a name="bk_scriptblock"> </a>

Dem Tag **\<script\>** folgt das Tag **\<div\>** mit einer ID. Standardmäßig entspricht die ID für das Tag ** \<div\> ** dem Namen der HTML-Datei. HTML oder Code, die/den die Anzeigevorlage bereitstellen soll, muss im Tag **\<div\>** enthalten sein. Aber das Tag selbst ist nicht im Markup enthalten, das auf der Webseite zur Laufzeit wiedergegeben wird.
  
> [!NOTE]
> Wenn Sie eine CSS-Formatvorlage oder eine ID zum HTML-Block zuweisen, der auf der Seite zur Laufzeit zurückgegeben wird, können Sie ein neues Tag im ersten **\<div\>**-Tag hinzufügen. Sie können eine CSS-Formatvorlage oder ID auch zum HTML-Code zuweisen, der die Variable `_#= ctx.RenderGroups(ctx) =#_` in der Steuerelementvorlage umgibt. Die Variable `_#= ctx.RenderGroups(ctx) =#_` wird verwendet, um den HTML-Code wiederzugeben, der die Abfrageergebnisse umgibt, die von der Elementvorlage wiedergegeben werden.
  
    
    

Im ersten ** \<div\> **-Tag sehen Sie Code in Kommentarblöcken, der mit ** \<!-- #\_ ** beginnt und mit ** \_#--\>** endet. Sie verwenden JavaScript-Code in diesen Blöcken und HTML außerhalb der Blöcke. Sie können mit diesen Blöcken auch den HTML-Code mit bedingten Anweisungen steuern. Verwenden Sie dazu einen Kommentarblock mit der bedingten Anweisung und einer öffnenden Klammer, gefolgt vom HTML-Code, gefolgt von einem weiteren Kommentarblock mit einer schließenden Klammer. Im folgenden Beispiel wird das Anker-Tag nur auf der Seite wiedergegeben, wenn den Wert für das Objekt **linkURL** nicht leer ist.
  
    
    



```HTML

<!--#_
if(!linkURL.isEmpty)
{
_#-->
     <a class="cbs-pictureImgLink" href="_#= linkURL =#_" title="_#= $htmlEncode(line1.defaultValueRenderer(line1)) =#_" id="_#= pictureLinkId =#_">
<!--#_
}
_#-->

```


## <a name="mapping-input-properties-and-getting-their-values"></a>Zuordnen von Eingabeeigenschaften und Abrufen ihrer Werte
<a name="bk_mapproperties"> </a>

Der Kopfzeilenbereich einer Elementanzeigevorlage weist eine benutzerdefinierte Dokumenteigenschaft namens **ManagedPropertyMapping** auf. Diese Eigenschaft ordnet die verwalteten Eigenschaften, die von der Suche verwendet werden, Werten zu, die von der Anzeigevorlage verwendet werden können. Die Eigenschaft ist eine durch Kommas getrennte Werteliste im folgenden Format: ' _Anzeigename der Eigenschaft_'{ _Eigenschaftsname_}:' _verwaltete Eigenschaft_'. Beispiel:  `'Picture URL'{Picture URL}:'PublishingImage;PictureURL;PictureThumbnailURL'`.
  
    
    
Im Folgenden wird das Format näher erläutert:
  
    
    

-  _Anzeigename der Eigenschaft_ ist der Eigenschaftsname, der im Bearbeitungsbereich des Webparts angezeigt wird, wenn die Anzeigevorlage ausgewählt wird.
    
  
-  _Eigenschaftsname_ ist ein Bezeichner, der lokalisierte Zeichenfolgeressourcen verwendet, um den Namen der verwalteten Eigenschaft nachzuschlagen. Er verwendet auch den Wert, der im Menü mit den Webparteinstellungen im Abschnitt **Eigenschaftszuordnungen** angezeigt wird. Wenn Sie die Einstellungen für ein Webpart bearbeiten, können Sie diesen Wert ändern, um zu ändern, welche verwaltete Eigenschaft mit dem im Webpart angezeigten Feld verknüpft wird.
    
  
-  _verwaltete Eigenschaft_ ist eine Zeichenfolge einer oder mehrerer verwalteter Eigenschaften, die durch Strichpunkte getrennt sind. Zur Laufzeit wird diese Liste von links nach rechts gelesen, und der erste Wert, der mit dem Namen einer verwalteten Eigenschaft des aktuellen Suchelements übereinstimmt, wird diesem Slot zugeordnet. Dadurch können Sie einen Anzeigenamen schreiben, der mit mehreren Elementtypen verwendet werden kann, und der bei Vorhandensein kompatibler Eigenschaften konsistentes Rendering verwenden kann.
    
  
Nachdem Sie eine Eigenschaft zugeordnet haben, können Sie mit folgendem Code deren Wert in Skript abrufen:  `var pictureURL = $getItemValue(ctx, "Picture URL");`
  
    
    
Der zweite Parameter, der an **$getItemValue()** übergeben wird, muss dem Anzeigenamen der Eigenschaft in einfachen Anführungszeichen entsprechen, der im **ManagedPropertyMapping**-Element verwendet wird. In diesem Beispiel ist **Picture URL** der Eigenschaftsname, der an **$getItemValue()** übergeben wird.
  
    
    
Dieser Code gibt ein Wertinformationsobjekt zurück ( **valueInfoObj**). Dieses Objekt enthält eine Rohdarstellung des Eingabewerts, zusammen mit dem Wert, auf den eine Standardcodierung angewendet wurde.
  
    
    
Sie können Variablen innerhalb der Abschnitte von JavaScript verwenden, wie Sie das normalerweise tun würden, um Variablen zu bearbeiten und HTML-Zeichenfolgen zu erstellen, die zur Laufzeit auf der Seite gerendert werden. Um Variablen zu referenzieren, die im Skript direkt im HTML deklariert wurden, müssen Sie allerdings das folgende Format verwenden: _#=  _variableName_ =#_. Um z. B. die Variable **pictureURL** als den Wert für ein Bild zu verwenden, müssen Sie den folgenden HTML-Code verwenden: `<img src="_#= pictureURL =#_" />`
  
    
    

## <a name="using-jquery-with-display-templates"></a>Verwenden von jQuery mit Anzeigevorlagen
<a name="bk_jQuery"> </a>

Sie können für Ihre Anzeigevorlagen jQuery verwenden. Beachten Sie dabei allerdings folgende zwei Punkte:
  
    
    

- Um die jQuery-Bibliotheken in Ihre Anzeigevorlage einzuschließen, befolgen Sie die im Abschnitt  [Skriptblock](#bk_scriptblock) weiter oben in diesem Artikel beschriebenen Anweisungen.
    
  
- Wenn Sie ID-Auswahlen in jQuery verwenden, erstellen Sie eine Variable für die ID mit dem folgenden Code:  `var containerQueryId = '#' + '_#= containerId =#_';`
    
    Verwenden Sie den folgenden Code, um die Auswahl in jQuery zu referenzieren:  `$('_#= containerQueryId =#_')`
    
  

## <a name="create-a-display-template"></a>Erstellen einer Anzeigevorlage
<a name="bk_createDT"> </a>

Bevor Sie mithilfe des folgenden Verfahrens eine Anzeigevorlage erstellen können, müssen Sie ein zugeordnetes Netzwerklaufwerk haben, das auf den **Gestaltungsvorlagenkatalog** verweist. Weitere Informationen finden Sie unter [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
  
    
    

### <a name="to-create-a-display-template"></a>So erstellen Sie eine Anzeigevorlage


1. Öffnen Sie mithilfe von Windows Explorer das auf den **Gestaltungsvorlagenkatalog** verweisende zugeordnete Netzwerklaufwerk.
    
  
2. Öffnen Sie den Ordner **Anzeigevorlagen** und dann den Ordner **Inhalt-Webparts**.
    
  
3. Kopieren Sie die HTML-Datei für eine Anzeigevorlage, die dem ähnelt, was Sie erstellen möchten. Eine Liste der Standardanzeigevorlagen und ihre Beschreibungen finden Sie unter  [Anzeigen der Vorlagenreferenz in SharePoint Server](http://technet.microsoft.com/de-DE/library/jj944947.aspx).
    
    SharePoint kopiert jetzt die HTML-Datei in eine .js-Datei mit demselben Namen. Wenn die kopierte HTML-Datei beispielsweise „Item_Picture3Line_copy.html“ heißt, wird auch eine entsprechende .js-Datei mit dem Namen „Item_Picture3Lines_copy.js“ erstellt. Wenn Sie die Datei umbenennen, ändert sich auch der Name der entsprechenden .js-Datei.
    
  
4. Um die Anzeigevorlage anzupassen, bearbeiten Sie die HTML-Datei auf dem Server. Verwenden Sie zum Öffnen und Bearbeiten der HTML-Datei auf dem zugeordneten Laufwerk einen HTML-Editor. Immer wenn Sie die HTML-Datei speichern, werden die Änderungen mit der entsprechenden JS-Datei synchronisiert.
    
  
5. Wechseln Sie zu Ihrer Veröffentlichungswebsite.
    
  
6. Wählen Sie in der rechten oberen Ecke der Seite **Einstellungen** und dann **Entwurfs-Manager**.
    
  
7. Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Anzeigevorlagen bearbeiten** aus. Ihre HTML-Datei wird nun mit der Spalte **Status** angezeigt, die einen der zwei Status aufweist:
    
  - Fehler
    
  
  - **Konvertierung erfolgreich**

    > [!NOTE]
    > Sie können nicht wie bei Gestaltungsvorlagen und Seitenlayouts die Vorschauseite verwenden, um eine serverseitige Livevorschau Ihrer Anzeigevorlage anzuzeigen. Um eine Vorschau der Anzeigevorlage anzuzeigen, müssen Sie einer Seite ein Inhaltssuche-Webpart hinzufügen und dann die Anzeigevorlage im Bearbeitungsbereich des Inhaltssuche-Webparts anwenden. Weist die Anzeigevorlage Fehler auf, zeigt das Inhaltssuche-Webpart eine Fehlermeldung an. Fehler müssen behoben werden, bevor die Anzeigevorlage korrekt angezeigt werden kann. 

8. Bearbeiten Sie zur Behebung von Fehlern die HTML-Datei auf dem Server. Verwenden Sie zum Öffnen und Bearbeiten der HTML-Datei auf dem zugeordneten Laufwerk einen HTML-Editor. Speichern Sie die Anzeigevorlage, und laden Sie dann die Seite mit dem Inhaltssuche-Webpart, welche die Anzeigevorlage verwendet, neu.
    
  

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Übersicht über den Entwurfs-Manager in SharePoint](overview-of-design-manager-in-sharepoint.md)
-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
-  [Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
-  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
-  [SharePoint Design Manager - Branding- und Designfunktionen](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

