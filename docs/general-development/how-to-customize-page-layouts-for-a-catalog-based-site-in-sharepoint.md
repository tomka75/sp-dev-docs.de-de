---
title: "Anpassen der Seitenlayouts für eine katalogbasierte Website in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 21d8db99-73b3-4429-b6cb-04e375af9f55
ms.openlocfilehash: d5606b864544072f0cde253363144f400d98414d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="customize-page-layouts-for-a-catalog-based-site-in-sharepoint"></a>Anpassen der Seitenlayouts für eine katalogbasierte Website in SharePoint

Hier erfahren Sie, wie Sie Layouts für Kategorieseiten und Katalogelementseiten für eine websiteübergreifende SharePoint-Veröffentlichungswebsite erstellen und anpassen können.

## <a name="prerequisites-for-creating-and-customizing-page-layouts-for-a-catalog-based-site"></a>Voraussetzungen für die Erstellung und Anpassung von Seitenlayouts für eine katalogbasierte Website
<a name="bk_prereqs"> </a>

Um die Schritte in diesem Beispiel ausführen zu können, benötigen Sie Folgendes:
  
    
    

- Einen HTML-Editor
    
  
- Eine websiteübergreifende SharePoint-Veröffentlichungsumgebung
    
  
Informationen zur Konfiguration einer websiteübergreifenden SharePoint-Veröffentlichungsumgebung finden Sie unter  [Konfigurieren der websiteübergreifenden Veröffentlichung in SharePoint](http://technet.microsoft.com/de-DE/library/jj656774.aspx).
  
    
    

### <a name="core-concepts-to-know-for-creating-and-customizing-page-layouts-for-a-catalog-based-site"></a>Kernkonzepte zur Erstellung und Anpassung von Seitenlayouts für eine katalogbasierte Website

In Tabelle 1 sind nützliche Artikel aufgeführt, die Ihnen die Konzepte und Arbeitsschritte zur Erstellung und Anpassung von Seitenlayouts für eine katalogbasierte Website näher bringen.
  
    
    

**Tabelle 1. Kernkonzepte für die Erstellung und Anpassung von Seitenlayouts für eine katalogbasierte Website**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [Übersicht über die websiteübergreifende Veröffentlichung in SharePoint](http://technet.microsoft.com/de-DE/library/jj635883.aspx) <br/> |Erfahren Sie, wie Sie mit der websiteübergreifenden Veröffentlichung und Such-Webparts anpassungsfähige SharePoint-Websites für das Internet, Intranet und Extranet erstellen können.  <br/> |
| [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md) <br/> |Erfahren Sie, wie Sie Seitenlayouts in SharePoint Server erstellen können.  <br/> |
| [Vorgehensweise: Beheben von Fehlern und Warnungen bei der Vorschau einer Seite in SharePoint](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md) <br/> |Erfahren Sie, wie Sie Probleme beheben, die verhindern, dass die serverseitige Vorschau Ihre Seite rendert.  <br/> |
| [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md) <br/> |Erfahren Sie, wie Sie mit Codeausschnitten der HTML-Masterseite oder dem Seitenlayout SharePoint-Funktionen hinzufügen.  <br/> |
   

## <a name="introduction-to-category-page-layouts-and-catalog-item-page-layouts"></a>Einführung in Layouts für Kategorieseiten und Katalogelementseiten
<a name="bk_introduction"> </a>

Kategorieseiten und Katalogobjektseiten sind Seitenlayouts, die Sie zum konsistenten Anzeigen von strukturiertem Kataloginhalt auf einer Website verwenden können. SharePoint kann standardmäßig ein Kategorieseitenlayout und ein Katalogobjektseiten-Layout pro Katalogverbindung erstellen. Seiten, die auf diesen Layouts basieren, werden in der Seitenbibliothek einer Veröffentlichungswebsite erstellt, wenn Sie die Website mit einem Katalog verbinden. Weitere Informationen zu Seitenlayouts finden Sie unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md). Weitere Informationen zu Features, die für kategoie-Seitenlayouts und Katalogelement-Seitenlayouts spezifisch sind, finden Sie unter[Übersicht über websiteübergreifende Veröffentlichung in SharePoint](http://technet.microsoft.com/de-DE/library/jj635883.aspx).
  
    
    
Standardmäßig werden Layouts für Kategorieseiten und Katalogelementseiten automatisch erstellt, wenn Sie eine Veröffentlichungswebsite mit einem Katalog verbinden. Sie können diese Layouts jedoch auch mit dem Entwurfs-Manager erstellen und sie bei der Verbindung der Veröffentlichungswebsite mit einem Katalog oder der Konfiguration eines Navigationsausdruckssatzes auf einer Veröffentlichungswebsite auswählen.
  
    
    

## <a name="create-a-category-page-layout"></a>Erstellen eines Layouts für eine Kategorieseite
<a name="bk_createCategoryPage"> </a>

Vor dem Erstellen oder Anpassen eines Layouts für Kategorieseiten empfehlen wir Ihnen, ein zugeordnetes Netzlaufwerk zu erstellen, das auf den **Gestaltungsvorlagenkatalog** verweist. Weitere Informationen finden Sie unter [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
  
    
    
Die einfachste Methode besteht darin, ein Layout für eine Kategorieseite automatisch bei der Verbindung einer Veröffentlichungswebsite mit einem Katalog von SharePoint erstellen zu lassen und anschließend das Markup des bestehenden Kategorieseitenlayouts an den Seitenentwurf anzupassen. Alternativ können Sie mit dem Entwurfs-Manager ein vollständig neues Layout erstellen.
  
    
    

### <a name="to-customize-an-existing-category-page-layout-that-was-created-automatically-by-sharepoint"></a>So passen Sie ein automatisch von SharePoint erstelltes Layout für eine Kategorieseite an


1. Öffnen Sie im Windows-Explorer das zugeordnete Netzlaufwerk, das auf den Gestaltungsvorlagenkatalog verweist.
    
  
2. Um das Layout für die Kategorieseite anzupassen, bearbeiten Sie die HTML-Datei auf dem Server mit einem HTML-Editor. Öffnen Sie dazu die HTML-Datei mit einem HTML-Editor im zugeordneten Netzlaufwerk, und bearbeiten Sie sie. Nach jedem Speichervorgang werden die Änderungen mit der entsprechenden ASPX-Datei synchronisiert.
    
  
3. Ersetzen Sie das Markup innerhalb des Inhaltsplatzhalters, der **id="PlaceHolderMain"** beinhaltet, durch das Markup, das Sie im Seitenlayout verwenden möchten.
    
    > **Wichtig:** Der Markupcodeausschnitt für die Inhaltssuche muss erhalten bleiben, damit auf der Kategorieseite Suchergebnisse angezeigt werden können. 
4. Um den HTML-Code für alle Codeausschnitte, die Sie der Seite hinzufügen möchten, zu konfigurieren und zu kopieren, befolgen Sie die Schritte 1 bis 11 im Abschnitt „Einfügen eines Codeausschnitts aus dem Codeausschnittkatalog" unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).
    
  
5. Nehmen Sie alle weiteren gewünschten Änderungen am Markup vor, und speichern Sie die Datei.
    
  
6. Befolgen Sie die Schritte 9 bis 11 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md), um den Dateistatus zu prüfen, eine Vorschau des Seitenlayouts zur erstellen und mögliche Fehler zu beheben.
    
  

### <a name="to-create-a-category-page-layout-by-using-design-manager"></a>So erstellen Sie ein Kategorieseitenlayout mit dem Entwurfs-Manager


1. Befolgen Sie die Schritte 1 bis 6 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).
    
  
2. Wählen Sie bei Schritt 7 den Inhaltstyp **Artikelseite**.
    
  
3. Wählen Sie **OK** aus.
    
    SharePoint erstellt jetzt eine HTML-Datei und eine ASPX-Datei mit dem gleichen Namen.
    
    Im Entwurfs-Manager wird die HTML-Datei nun mit der Spalte **Status** angezeigt, die einen der beiden folgenden Status hat:
    
  - Fehler
    
  
  - **Konvertierung erfolgreich**
    
  
4. Öffnen Sie im Windows-Explorer das Netzlaufwerk, das auf den Gestaltungsvorlagenkatalog verweist.
    
  
5. Um das Layout für die Kategorieseite anzupassen, bearbeiten Sie die HTML-Datei, die sich auf dem Server befindet, mit einem HTML-Editor. Nach jedem Speichervorgang werden die Änderungen mit der entsprechenden ASPX-Datei synchronisiert.
    
  
6. Ersetzen Sie im Tag **\<head\>** den Inhaltsplatzhalter **id="PlaceHolderPageTitle"** durch:
    
```HTML
  
<!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
<!--CS: Start Taxonomy TermProperty Snippet-->
<!--SPM:<%@Register Tagprefix="Taxonomy"  Namespace="Microsoft.SharePoint.Taxonomy" Assembly="Microsoft.SharePoint.Taxonomy, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>-->
<!--MS:<Taxonomy:TermProperty Property="Name" runat="server">-->
<!--ME:</Taxonomy:TermProperty>-->
<!--ME:</asp:ContentPlaceHolder>-->
```

7. Suchen Sie nach dem Inhaltsplatzhalter mit **id="PlaceHolderPageTitleInTitleArea"**, und ersetzen Sie ihn durch:
    
```HTML
  
<!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitleInTitleArea" runat="server">-->
<!--SPM:<asp:SiteMapPath runat="server" ParentLevelsDisplayed="1" SiteMapProvider="CurrentNavigationSwitchableProvider"/>-->
<!--ME:</asp:ContentPlaceHolder>-->
```

8. Ersetzen Sie das Markup innerhalb des Inhaltsplatzhalters, der **id="PlaceHolderMain"** beinhaltet, durch das Markup, das Sie im Seitenlayout verwenden möchten.
    
  
9. Um den HTML-Code für den Inhaltssuche-Codeausschnitt und alle weiteren Codeausschnitte, die Sie der Seite hinzufügen möchten, zu konfigurieren und zu kopieren, befolgen Sie die Schritte 1 bis 11 im Abschnitt „Einfügen eines Codeausschnitts aus dem Codeausschnittkatalog" unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).
    
    > [!NOTE]
    > Wenn Sie den Inhaltssuche-Codeausschnitt zum Seitenlayout hinzufügen, ändern Sie die Abfrage so, dass die Ergebnisquelle verwendet wird, die erstellt wurde, als Sie die Veröffentlichungswebsite mit einem Katalog verbunden haben. Weitere Informationen finden Sie unter [Konfigurieren von Ergebnisquellen für Web Content Management in SharePoint](http://technet.microsoft.com/de-DE/library/jj715262.aspx). 

10. Nehmen Sie alle weiteren gewünschten Änderungen am Markup vor, und speichern Sie die Datei.
    
  
11. Befolgen Sie die Schritte 9 bis 11 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md), um den Dateistatus zu prüfen, eine Vorschau des Seitenlayouts zur erstellen und mögliche Fehler zu beheben.
    
  

## <a name="understanding-the-markup-in-the-html-category-page-layout"></a>Grundlegendes zum Markup im HTML-Layout der Kategorieseite
<a name="bk_CategoryPageMarkup"> </a>

Wenn Sie ein Seitenlayout erstellen, wird eine ASPX-Datei zur Verwendung durch SharePoint erstellt, und der HTML-Datei für das Seitenlayout wird HTML-Code hinzugefügt. Layouts für Kategorieseiten umfassen Markupkomponenten, die dem Seitenlayout basierend auf der Funktion zur websiteübergreifenden Veröffentlichung von Sammlungen hinzugefügt werden und die speziell für Kategorieseitenlayouts gelten. Möglicherweise fällt Ihnen die Bearbeitung des HTML-Kategorieseitenlayouts leichter, wenn Sie sich im Folgenden näher mit dem Markup vertraut machen.
  
    
    

### <a name="browser-window-page-title"></a>Seitentitel im Browserfenster

Die Komponente im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderPageTitle"** enthält Markup, mit dem SharePoint angewiesen wird, eine Begriffseigenschaft als Seitentitel im Browserfenster zu verwenden, anstelle des Standardseiten-Feldwerts. Dieses Markup wird im folgenden Codebeispiel dargestellt.
  
    
    

```HTML

<!--CS: Start Taxonomy TermProperty Snippet-->
<!--SPM:<%@Register Tagprefix="Taxonomy"  Namespace="Microsoft.SharePoint.Taxonomy" Assembly="Microsoft.SharePoint.Taxonomy, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c" %>-->
<!--MS:<Taxonomy:TermProperty Property="Name" runat="server">-->
<!--ME:</Taxonomy:TermProperty>-->
```


### <a name="page-title"></a>Seitentitel

Die Komponente im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderPageTitleInTitleArea"** enthält Markup, mit dem SharePoint angewiesen wird, eine Begriffseigenschaft als Seitentitel auf der Seite zu verwenden, anstelle des Codeausschnitts **SPTitleBreadcrumb** und des Standardseiten-Feldwerts. Dieses Markup wird im folgenden Codebeispiel dargestellt.
  
    
    

```HTML

<!--SPM:<asp:SiteMapPath runat="server" ParentLevelsDisplayed="1" SiteMapProvider="CurrentNavigationSwitchableProvider"/>-->"
```


### <a name="content-search-snippet"></a>Inhaltssuche-Codeausschnitt

Die Komponente, die auf den Seiteninhalts-Codeausschnitt im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderMain"** folgt, enthält Markup für einen Webpart-Zonencodeausschnitt mit vier Webpartzonen. Die erste Webpartzone enthält einen Inhaltssuche-Codeausschnitt, mit dem ein Inhaltssuche-Webpart auf der Seite angezeigt wird. Dieser Codeausschnitt enthält des Weiteren Informationen, die zur Abfrage der Ergebnisquelle und Anzeige der Ergebnisse auf der Seite benötigt werden. Die weiteren drei Webpartzonen sind leer. Möchten Sie ein benutzerdefiniertes Layout für Kategorieseiten erstellen, muss das Markup für den Inhaltssuche-Codeausschnitt in der HTML-Datei des Seitenlayouts eingefügt werden. Das folgende Codebeispiel zeigt das Markup für den Inhaltssuche-Codeausschnitt. Ersetzen Sie _ResultSourceID_ durch die GUID der Ergebnisquelle und _CatalogURL_ durch die URL des Katalogs.
  
> [!NOTE]
> Die GUIDS für **ID** und **\_\_WebPartId** werden von SharePoint nach dem Zufallsprinzip generiert, wenn dem Seitenlayout Codeausschnitte hinzugefügt werden.
  
    
    


```HTML
<!--
CS: Start Content Search Snippet-->
<!--SPM:<%@Register Tagprefix="a781102493" Namespace="Microsoft.Office.Server.Search.WebControls" Assembly="Microsoft.Office.Server.Search, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<a781102493:ContentBySearchWebPart runat="server" DataProviderJSON="{&amp;#34;QueryTemplate&amp;#34;:&amp;#34;&amp;#34;,&amp;#34;SourceID&amp;#34;
:&amp;#34;ResultSourceID&amp;#34;,&amp;#34;PropertiesJson&amp;#34;:&amp;#34;
{'Tag':'{Term.IDWithChildren}','Scope':'CatalogURL'}&amp;#34;}" ResultsPerPage="3" RenderTemplateId="~sitecollection/_catalogs/masterpage/Display Templates/Content Web Parts/Control_ListWithPaging.js" 
ItemTemplateId="~sitecollection/_catalogs/masterpage/Display Templates/Content Web Parts/Item_PictureOnTop.js" SelectedPropertiesJson="[&amp;#34;WorkId&amp;#34;,&amp;#34;Rank&amp;#34;,&amp;#34;Title&amp;#34;,&amp;#34;Author&amp;#34;,&amp;#34;
Size&amp;#34;,&amp;#34;Path&amp;#34;,&amp;#34;Description&amp;#34;,&amp;#34;Write&amp;#34;,&amp;#34;CollapsingStatus&amp;#34;,&amp;#34;
HitHighlightedSummary&amp;#34;,&amp;#34;HitHighlightedProperties&amp;#34;,&amp;#34;ContentClass&amp;#34;,&amp;#34;
PictureThumbnailURL&amp;#34;,&amp;#34;ServerRedirectedURL&amp;#34;,&amp;#34;ServerRedirectedEmbedURL&amp;#34;,&amp;#34;
ServerRedirectedPreviewURL&amp;#34;,&amp;#34;FileExtension&amp;#34;,&amp;#34;ContentTypeId&amp;#34;,&amp;#34;ParentLink&amp;#34;,&amp;#34;
ViewsLifeTime&amp;#34;,&amp;#34;ViewsRecent&amp;#34;,&amp;#34;SectionNames&amp;#34;,&amp;#34;SectionIndexes&amp;#34;,&amp;#34;
SiteLogo&amp;#34;,&amp;#34;SiteDescription&amp;#34;,&amp;#34;deeplinks&amp;#34;,&amp;#34;importance&amp;#34;]" ShouldHideControlWhenEmpty="True" FrameType="None" SuppressWebPartChrome="False" Description="$Resources:Microsoft.Office.Server.Search,CBS_Description;" IsIncluded="True" 
ZoneID="" PartOrder="0" FrameState="Normal" AllowRemove="True" AllowZoneChange="True" 
AllowMinimize="True" AllowConnect="True" AllowEdit="True" AllowHide="True" IsVisible="True" 
DetailLink="" HelpLink="" HelpMode="Modeless" Dir="Default" PartImageSmall="" IsIncludedFilter="" ExportControlledProperties="True" ConnectionID="00000000-0000-0000-0000-000000000000" ID="g_54e35103_6f29_4dd9_b93b_8d4c863834af" ChromeType="None" ExportMode="All" __MarkupType="vsattributemarkup" __WebPartId="54e35103-6f29-4dd9-b93b-8d4c863834af" 
WebPart="true" Height="" Width="" Title="$Resources:cms,WebPartZoneTitle_Dynamic;">-->
<!--ME:</a781102493:ContentBySearchWebPart>-->
<!--CE: End Content Search Snippet-->

```


## <a name="create-a-catalog-item-page-layout"></a>Erstellen eines Seitenlayouts für ein Katalogelement
<a name="bk_createCatItemPage"> </a>

Vor dem Erstellen oder Anpassen eines Layouts für Kategorieelemente empfehlen wir Ihnen, ein zugeordnetes Netzlaufwerk zu erstellen, das auf den Gestaltungsvorlagenkatalog verweist. Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
  
    
    
Ähnlich wie beim Kategorieseitenlayout ist auch beim Erstellen eines Katalogelement-Seitenlayouts die einfachste Methode, das Seitenlayout von SharePoint automatisch erstellen zu lassen, wenn Sie die Veröffentlichungswebsite mit einem Katalog verbinden. Anschließend passen Sie das vorhandenen Katalogelement-Seitenlayout an, um von Seitenentwurf zusätzlich erfordertes Markup hinzuzufügen. Alternativ können Sie mithilfe des Entwurfs-Managers ein Katalogelement-Seitenlayout von Grund auf neu erstellen.
  
    
    

### <a name="to-customize-an-existing-catalog-item-page-layout-that-was-created-automatically-by-sharepoint"></a>So bearbeiten Sie ein bestehendes Layout für ein Kategorieelement, das automatisch von SharePoint erstellt wurde


1. Öffnen Sie im Windows-Explorer das Netzlaufwerk, das auf den Gestaltungsvorlagenkatalog verweist.
    
  
2. Um das Layout für die Katalogelementseite anzupassen, bearbeiten Sie die HTML-Datei, die sich auf dem Server befindet, mit einem HTML-Editor. Nach jedem Speichervorgang werden die Änderungen mit der entsprechenden ASPX-Datei synchronisiert.
    
  
3. Fügen Sie das Markup, das Sie im Seitenlayout verwenden möchten, im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderMain"** hinzu.
    
  
4. Löschen Sie alle Codeausschnitte, die Sie nicht im Seitenlayout verwenden möchten, und verschieben Sie die verbleibenden Codeausschnitte an die Stellen, an denen die Werte der Eigenschaften angezeigt sollen.
    
    > **Achtung:** Standardmäßig wird dem Seitenlayout ein Webpartzone-Codeausschnitt hinzugefügt, der einen Codeausschnitt zur Wiederverwendung von Katalogobjekten enthält. Dieser Codeausschnitt enthält den Datenanbieter, der Abfrageergebnisse zurückgibt, die von allen anderen Codeausschnitten auf der Seite verwendet werden. Es wird empfohlen, dass Sie den Codeausschnitt zur Wiederverwendung von Katalogobjekten in diesem standardmäßigen Webpartzone-Codeausschnitt belassen. (Sie können den Codeausschnitt zur Wiederverwendung von Katalogobjekten außerhalb der Webpartzone verschieben und die angezeigte Eigenschaft ändern. Aber Sie müssen den Codeausschnitt zur Wiederverwendung von Katalogobjekten im Seitenlayout belassen.) Weitere Informationen finden Sie unter [Seitenfelder](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields)weiter unten in diesem Artikel. 
5. Um den HTML-Code für alle Codeausschnitte, die Sie auf der Seite verwenden möchten, zu konfigurieren und zu kopieren, befolgen Sie die Schritte 1 bis 11 im Abschnitt „Einfügen eines Codeausschnitts aus dem Codeausschnittkatalog" unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).
    
  
6. Nehmen Sie alle weiteren gewünschten Änderungen am Markup vor, und speichern Sie die Datei.
    
  
7. Befolgen Sie die Schritte 9 bis 11 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md), um den Dateistatus zu prüfen, eine Vorschau des Seitenlayouts zur erstellen und mögliche Fehler zu beheben.
    
  

### <a name="to-create-a-catalog-item-page-layout-by-using-design-manager"></a>So erstellen Sie mit dem Entwurfs-Manager ein Layout für eine Katalogelementseite


1. Befolgen Sie die Schritte 1 bis 6 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).
    
  
2. Wählen Sie in Schritt 7 **Remotekatalog**, und wählen Sie dann den Katalog mit den Daten, die auf der Seite angezeigt werden sollen.
    
  
3. Wählen Sie **OK** aus.
    
    SharePoint erstellt jetzt eine HTML-Datei und eine ASPX-Datei mit dem gleichen Namen.
    
    Im Entwurfs-Manager wird die HTML-Datei nun mit der Spalte **Status** angezeigt, die einen der beiden folgenden Status hat:
    
  - Fehler
    
  
  - **Konvertierung erfolgreich**
    
  
4. Öffnen Sie im Windows-Explorer das Netzlaufwerk, das auf den Gestaltungsvorlagenkatalog verweist.
    
  
5. Um das Layout für die Katalogelementseite anzupassen, bearbeiten Sie HTML-Datei, die sich auf dem Server befindet, mit einem HTML-Editor. Nach jedem Speichervorgang werden die Änderungen mit der entsprechenden ASPX-Datei synchronisiert.
    
  
6. Fügen Sie das Markup, das Sie im Seitenlayout verwenden möchten, im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderMain"** hinzu.
    
  
7. Löschen Sie alle Codeausschnitte, die Sie nicht im Seitenlayout verwenden möchten, und verschieben Sie die verbleibenden Codeausschnitte an die Stellen, an denen die Werte der Eigenschaften angezeigt sollen.
    
    > **Achtung:** Standardmäßig wird dem Seitenlayout ein Webpartzone-Codeausschnitt hinzugefügt, der einen Codeausschnitt zur Wiederverwendung von Katalogobjekten enthält. Dieser Codeausschnitt enthält den Datenanbieter, der Abfrageergebnisse zurückgibt, die von allen anderen Codeausschnitten auf der Seite verwendet werden. Es wird empfohlen, dass Sie den Codeausschnitt zur Wiederverwendung von Katalogobjekten in diesem standardmäßigen Webpartzone-Codeausschnitt belassen. (Sie können den Codeausschnitt zur Wiederverwendung von Katalogobjekten außerhalb der Webpartzone verschieben und die angezeigte Eigenschaft ändern. Aber Sie müssen den Codeausschnitt zur Wiederverwendung von Katalogobjekten im Seitenlayout belassen.) Weitere Informationen finden Sie unter [Seitenfelder](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields)weiter unten in diesem Artikel. 
8. Um den HTML-Code für alle Codeausschnitte, die Sie auf der Seite verwenden möchten, zu konfigurieren und zu kopieren, befolgen Sie die Schritte 1 bis 11 im Abschnitt „Einfügen eines Codeausschnitts aus dem Codeausschnittkatalog" unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).
    
  
9. Nehmen Sie alle weiteren gewünschten Änderungen am Markup vor, und speichern Sie die Datei.
    
  
10. Befolgen Sie die Schritte 9 bis 11 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md), um den Dateistatus zu prüfen, eine Vorschau des Seitenlayouts zur erstellen und mögliche Fehler zu beheben.
    
  

## <a name="understanding-the-markup-in-the-html-catalog-item-page-layout"></a>Grundlegendes zum Markup im HTML-Layout für Katalogelementseiten
<a name="bk_CatItemMarkup"> </a>

Wenn Sie ein Seitenlayout erstellen, wird eine ASPX-Datei zur Verwendung durch SharePoint erstellt, und der HTML-Datei für das Seitenlayout wird HTML-Code hinzugefügt. Layouts für Katalogelementseiten umfassen Markupkomponenten, die dem Seitenlayout basierend auf der Funktion zur websiteübergreifenden Veröffentlichung von Sammlungen hinzugefügt werden und die speziell für Katalogelement-Seitenlayouts gelten. Möglicherweise fällt Ihnen die Bearbeitung des HTML-Katalogelement-Seitenlayouts leichter, wenn Sie sich im Folgenden näher mit dem Markup vertraut machen.
  
    
    

### <a name="browser-window-page-title"></a>Seitentitel im Browserfenster

Die Komponente im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderPageTitle"** enthält einen Codeausschnitt zur Wiederverwendung von Katalogelementen, mit dem SharePoint angewiesen wird, den Namen des Katalogelements als Seitentitel im Browserfenster zu verwenden, anstelle des Standardseiten-Feldwerts. Dieses Markup wird im folgenden Codebeispiel dargestellt.
  
> [!NOTE]
> Die GUIDS für **ID** und **__WebPartId** werden von SharePoint nach dem Zufallsprinzip generiert, wenn dem Seitenlayout Codeausschnitte hinzugefügt werden.
  
    
    


```HTML

<!--CS: [Title] Start Catalog-Item Reuse Snippet-->
<!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;Title&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_863912c1_c849_46dc_8781_2920ee2bc83f" __WebPartId="{863912c1-c849-46dc-8781-2920ee2bc83f}">-->
<!--SPM:<RenderFormat>-->
<!--DC:Renders value from search without any additional formatting.-->
<!--SPM:</RenderFormat>-->
<!--SPM:</cc1:CatalogItemReuseWebPart>-->
<!--CE:End Catalog-Item Reuse Snippet-->

```


### <a name="page-fields"></a>Seitenfelder
<a name="bk_pagefields"> </a>

Die Komponenten im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderMain"** enthalten Codeausschnitte für die Felder **Title**, **Page Content** und **Catalog-Item URL**. Sie können diese Codeausschnitte auf Wunsch aus dem Seitenlayout löschen. Das folgende Codebeispiel zeigt das Markup für diese Seitenfelder.
  
    
    

```HTML

<div>
    <!--CS: Start Page Field: Title Snippet-->
    <!--SPM:<%@Register Tagprefix="PageFieldTextField" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, 
Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" CssClass="edit-mode-panel">-->
        <!--MS:<PageFieldTextField:TextField FieldName="fa564e0f-0c70-4ab9-b863-0177e6ddd247" 
runat="server">-->
        <!--ME:</PageFieldTextField:TextField>-->
    <!--ME:</Publishing:EditModePanel>-->
    <!--CE: End Page Field: Title Snippet-->
</div>
<div>
    <!--CS: Start Page Field: Page Content Snippet-->
    <!--SPM:<%@Register Tagprefix="PageFieldRichHtmlField" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<PageFieldRichHtmlField:RichHtmlField FieldName="f55c4d88-1f2e-4ad9-aaa8-819af4ee7ee8" runat="server">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
            <div id="ctl02_label" style="display:none">Page Content</div>
            <div id="ctl02__ControlWrapper_RichHtmlField" class="ms-rtestate-field" style="display:inline" aria-labelledby="ctl02_label">
                <div align="left" class="ms-formfieldcontainer">
                    <div class="ms-formfieldlabelcontainer" nowrap="nowrap">
                        <span class="ms-formfieldlabel" nowrap="nowrap">Page Content</span>
                    </div>
                    <div class="ms-formfieldvaluecontainer">
                        <div class="ms-rtestate-field">Page Content field value. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</div>
                    </div>
                </div>
            </div>
        <!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</PageFieldRichHtmlField:RichHtmlField>-->
    <!--CE: End Page Field: Page Content Snippet-->
</div>
<div>
    <!--CS: Start Page Field: Catalog-Item URL Snippet-->
    <!--SPM:<%@Register Tagprefix="PageFieldCatalogSourceFieldControl" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<PageFieldCatalogSourceFieldControl:CatalogSourceFieldControl FieldName="75772bbf-0c25-4710-b52c-7b78344ad136" runat="server">-->
    <!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
        <div align="left" class="ms-formfieldcontainer">
            <div class="ms-formfieldlabelcontainer" nowrap="nowrap">
                <span class="ms-formfieldlabel" nowrap="nowrap">Catalog-Item URL</span>
            </div>
            <div class="ms-formfieldvaluecontainer">
                <a href="http://www.example.com">Link to sample web site.</a>
            </div>
        </div>
    <!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</PageFieldCatalogSourceFieldControl:CatalogSourceFieldControl>-->
    <!--CE: End Page Field: Catalog-Item URL Snippet-->
</div>

```

Wenn das Katalogelement-Seitenlayout automatisch bei der Verbindung der Veröffentlichungswebsite mit dem Katalog erstellt wurde oder indem ein Remotekatalog bei der Erstellung des Seitenlayouts ausgewählt wurde, enthält das Seitenlayout außerdem einen Webpartzonen-Codeausschnitt mit einem Codeausschnitt zur Wiederverwendung von Katalogelementen, in dem der Datenanbieter für die Seite registriert ist. Der Codeausschnitt zur Wiederverwendung von Katalogelementen enthält die Eigenschaft **UseSharedDataProvider**, deren Wert auf **False** gesetzt ist. Der Webpartzonen-Codeausschnitt kann aus dem Seitenlayout gelöscht werden. Damit die Seite weiterhin Katalogelemente anzeigen kann, muss der Codeausschnitt zur Wiederverwendung von Katalogelementen allerdings im Seitenlayout verbleiben. Wenn Sie eine Seite mit diesem Seitenlayout erstellen, können Sie den Webpart so einstellen, dass er beim Aufrufen der Seite ausgeblendet wird.
  
    
    

> **Wichtig:** Wenn Sie ein neues Katalogelement-Seitenlayout erstellen und einen Inhaltstyp anstelle eines Remotekatalogs auswählen, müssen Sie einen Codeausschnitt zur Wiederverwendung von Katalogobjekten in das Seitenlayout einschließen. Der folgende Code zeigt das Markup für den Codeausschnitt zur Wiederverwendung von Katalogobjekten, wie er innerhalb des Webpartzone-Codeausschnitts angezeigt wird. Ersetzen Sie _ManagedPropertyName_ durch den Namen der verwalteten Eigenschaft, die angezeigt werden soll, ersetzen Sie _ResultSourceID_ durch die GUID der Ergebnisquelle, und ersetzen Sie _CatalogURL_ durch die URL des Katalogs.
  
    
    




```HTML

<div>
    <!--CS: Start Web Part Zone Snippet-->
    <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, 
Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--SPM:<%@Register Tagprefix="cc1"  Namespace="Microsoft.Office.Server.Search.WebControls" Assembly="Microsoft.Office.Server.Search, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c" %>-->
    <!--MS:<WebPartPages:WebPartZone runat="server" Title="&amp;#60;%$Resources:cms,WebPartZoneTitle_Body%&amp;#62;" AllowPersonalization="False" FrameType="TitleBarOnly" ID="Body" Orientation="Vertical">-->
        <!--MS:<ZoneTemplate>-->
            <!--CS: [ManagedPropertyName] Start Catalog-Item Reuse Snippet-->
            <!--DC:To render the search property using a rendering template, change the "UseServerSideRenderFormat" property to "False".-->
            <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" AddSEOPropertiesFromSearch="True" LogAnalyticsViewEvent="True" UseSharedDataProvider="False" OverwriteResultPath="False" DataProviderJSON="{&amp;#34;QueryTemplate&amp;#34;:&amp;#34;ListItemID:{URLTOKEN.1}&amp;#34;,&amp;#34;SourceID&amp;#34;:&amp;#34; ResultSourceID&amp;#34;,&amp;#34;PropertiesJson&amp;#34;:&amp;#34;{&amp;#39;Scope&amp;#39;:&amp;#39;  CatalogURL&amp;#39;,&amp;#39;Tag&amp;#39;:&amp;#39;{Term}&amp;#39;}&amp;#34;}" ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;ManagedPropertyName&amp;#34;]" Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" MissingAssembly="Cannot import this Web Part." ID="g_d63eebe7_207f_4e8c_9566_7381acc80cc7" __WebPartId="{d63eebe7-207f-4e8c-9566-7381acc80cc7}">-->
            <!--SPM:<RenderFormat>-->
            <!--DC:Renders value from search without any additional formatting.-->
            <!--SPM:</RenderFormat>-->
            <!--SPM:</cc1:CatalogItemReuseWebPart>-->
        <!--ME:</ZoneTemplate>-->
    <!--ME:</WebPartPages:WebPartZone>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>

```

Wenn das Katalogelement-Seitenlayout automatisch bei der Verbindung der Veröffentlichungswebsite mit dem Katalog erstellt wurde oder indem ein Remotekatalog bei der Erstellung des Seitenlayouts ausgewählt wurde, enthält die restliche Seite Codeausschnitte zur Wiederverwendung von Katalogelementen, die den verwalteten Eigenschaften des Katalogs auf der Erstellungsseite entsprechen. Über diese verwalteten Eigenschaften werden die Details zu einem bestimmten Katalogelement unter Verwendung des Seitenlayouts für Katalogelemente angezeigt. Diese Codesausschnitte zur Wiederverwendung von Katalogelementen erscheinen außerhalb der Webpartzone und werden direkt auf der Seite gerendert, wenn ein Element auf der Kategorieseite ausgewählt wird. In Tabelle 2 sind die verwalteten Eigenschaften aufgeführt, die automatisch im Katalogelement-Seitenlayout enthalten sind.
  
> [!NOTE]
> Einige verwaltete Eigenschaften sind nur enthalten, wenn der Katalog eine Bibliothek für Seiten ist. In Tabelle 2 wird in der Spalte **Verwendet von** angegeben, welche verwalteten Eigenschaften von Bibliotheken für Seiten und von Listen verwendet werden und welche ausschließlich von Bibliotheken für Seiten.
  
    
    


**Tabelle 2. Standardmäßige verwaltete Eigenschaften für Codeausschnitte zur Wiederverwendung von Katalogelementen**


|**Verwaltete Eigenschaft**|**Beschreibung**|**Verwendet von**|
|:-----|:-----|:-----|
|**AuthorOWSUSER** <br/> |Der Name des Benutzers, der die Seite erstellt hat.  <br/> |Nur Bibliothek für Seiten  <br/> |
|**CreatedOWSDATE** <br/> |Das Datum, an dem die Seite oder das Listenelement erstellt wurde.  <br/> |Bibliothek für Seiten und Liste  <br/> |
|**EditorOWSUSER** <br/> |Der Name des Benutzers, der die Seite oder das Listenelement zuletzt geändert hat.  <br/> |Bibliothek für Seiten und Liste  <br/> |
|**ListItemID** <br/> |Die ID der Seite oder des Listenelements.  <br/> |Bibliothek für Seiten und Liste  <br/> |
|**ModifiedOWSDATE** <br/> |Das Datum, an dem die Seite oder das Listenelement zuletzt geändert wurde.  <br/> |Bibliothek für Seiten und Liste  <br/> |
|**PublishingContactOWSUSER** <br/> |„Kontakt“ ist eine Websitespalte, die von der Veröffentlichungsfunktion erstellt wird. Sie wird für den Seiteninhaltstyp als Kontaktperson oder -organisation für die Website verwendet.  <br/> |Nur Bibliothek für Seiten  <br/> |
|**PublishingIsFurlPageOWSBOOL** <br/> |Ein boolescher Wert, der angibt, ob der Seite eine benutzerfreundliche URL zugeordnet ist.  <br/> |Nur Bibliothek für Seiten  <br/> |
|**PublishingPageContentOWSHTML** <br/> |Der HTML-Inhalt der Seite.  <br/> |Nur Bibliothek für Seiten  <br/> |
|**PublishingPageLayoutOWSURLH** <br/> |Die URL zum Seitenlayout, das zum Erstellen der Seite verwendet wurde.  <br/> |Nur Bibliothek für Seiten  <br/> |
|**Title** <br/> |Der Titel der Seite oder des Listenelements.  <br/> |Bibliothek für Seiten und Liste  <br/> |
   
Die verwalteten Eigenschaften für benutzerdefinierte Spalten, die Sie der Bibliothek für Seiten oder der Liste hinzufügen, werden ebenfalls in Codeausschnitte zur Wiederverwendung von Katalogelementen eingeschlossen. Der Name der verwalteten Eigenschaft variiert je nach dem Typ der Website, die Sie beim Erstellen der Websitespalte verwenden. Weitere Informationen finden Sie unter [Automatisch erstellte verwaltete Eigenschaften in SharePoint](http://technet.microsoft.com/de-DE/library/jj613136.aspx) und [Übersicht über das Suchschema in SharePoint](http://technet.microsoft.com/de-DE/library/jj219669.aspx).
  
    
    

> **Wichtig:** Die Websitespalte **Seitenbild** Websitespalte in einer Bibliothek für Seiten wird der verwalteten Eigenschaft **PublishingImage** zugeordnet. Die verwaltete Eigenschaft **PublishingImage** wird aber nicht automatisch in das Kategorieelement-Seitenlayout eingeschlossen. Um das Bild in das Seitenlayout einzuschließen, müssen Sie einen Codeausschnitt zur Wiederverwendung von Katalogelementen für die verwaltete Eigenschaft **PublishingImage** hinzufügen. Verwenden Sie den folgenden HTML-Code, um einen Codeausschnitte zur Wiederverwendung von Katalogelementen hinzuzufügen, um den Wert der verwalteten Eigenschaft **PublishingImage** im Seitenlayout anzuzeigen. Ersetzen Sie _UniqueID_ durch eine GUID, die für jede Instanz des Codeausschnitts eindeutig ist.
  
    
    




```HTML

<div>
<!--CS: [PublishingImage] Start Catalog-Item Reuse Snippet-->
<!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;PublishingImage&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_UniqueID" __WebPartId="{UniqueID}">-->
<!--SPM:<RenderFormat>-->
<!--SPM:<Format Type="HTML"> -->
<!--SPM:<Picture>-->True<!--SPM:</Picture>-->
<!--SPM:</Format> -->
<!--SPM:</RenderFormat>-->
<!--SPM:</cc1:CatalogItemReuseWebPart>-->
<!--CE:End Catalog-Item Reuse Snippet-->
</div>

```

Wenn Sie mit dem Entwurfs-Manager ein neues Katalogelement-Seitenlayout erstellen und einen Inhaltstyp anstellen eines Remotekatalogs auswählen, können Sie Codeausschnitte zur Wiederverwendung von Katalogelementen im Codeausschnittkatalog auswählen. Das folgende Codebeispiel zeigt das Markup der Codeausschnitte zur Wiederverwendung von Katalogelementen für die verwalteten Eigenschaften **Title**, **PublishingPageContentOWSHTML**, **CreatedOWSDATE** und **owstaxIdPageCategory**.
  
> [!NOTE]
> Die GUIDS für **ID** und **__WebPartId** werden von SharePoint nach dem Zufallsprinzip generiert, wenn dem Seitenlayout Codeausschnitte hinzugefügt werden.
  
    
    




```HTML

<div>
    <!--CS: [Title] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;Title&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_0dc23bb8_8d34_4f9f_8085_5a6ac286cb9e" 
__WebPartId="{0dc23bb8-8d34-4f9f-8085-5a6ac286cb9e}">-->
    <!--SPM:<RenderFormat>-->
    <!--DC:Renders value from search without any additional formatting.-->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>
<div>
    <!--CS: [PublishingPageContentOWSHTML] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;PublishingPageContentOWSHTML&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_25253a49_a9a6_4277_bf9d_416961024cee" 
__WebPartId="{25253a49-a9a6-4277-bf9d-416961024cee}">-->
    <!--SPM:<RenderFormat>-->
    <!--DC:Renders value from search without any additional formatting.-->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>
<div>
    <!--CS: [CreatedOWSDATE] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;CreatedOWSDATE&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." 
ID="g_4e1f180b_12f8_4e50_84d7_c72b0ee3793f" 
__WebPartId="{4e1f180b-12f8-4e50-84d7-c72b0ee3793f}">-->
    <!--SPM:<RenderFormat>-->
    <!--SPM:<Format Type="DateTime"> -->
    <!--DC:To render Date and Time, change this value to False.-->
    <!--SPM:<DateOnly>-->True<!--SPM:</DateOnly>-->
    <!--SPM:</Format> -->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>
<div>
    <!--CS: [owstaxIdPageCategory] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;owstaxIdPageCategory&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_22e39e9d_1b25_42c7_bf2a_7ebca37616d4" 
__WebPartId="{22e39e9d-1b25-42c7-bf2a-7ebca37616d4}">-->
    <!--SPM:<RenderFormat>-->
    <!--DC:Renders value from search without any additional formatting.-->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>

```


## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
    
  
-  [Übersicht über den Entwurfs-Manager in SharePoint](overview-of-design-manager-in-sharepoint.md)
    
  
-  [Übersicht über das SharePoint-Seitenmodell](overview-of-the-sharepoint-page-model.md)
    
  
-  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [Anzeigevorlagen im SharePoint-Entwurfs-Manager](sharepoint-design-manager-display-templates.md)
    
  

