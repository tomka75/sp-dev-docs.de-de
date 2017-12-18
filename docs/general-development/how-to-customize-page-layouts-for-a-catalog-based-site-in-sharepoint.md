---
title: "Anpassen der Seitenlayouts für eine katalogbasierte Website in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 21d8db99-73b3-4429-b6cb-04e375af9f55
ms.openlocfilehash: 9e7c7811531f4dd01f890eddd705fcb882f90128
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="customize-page-layouts-for-a-catalog-based-site-in-sharepoint"></a><span data-ttu-id="1d0af-102">Anpassen der Seitenlayouts für eine katalogbasierte Website in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d0af-102">How to: Customize page layouts for a catalog-based site in SharePoint</span></span>

<span data-ttu-id="1d0af-103">Hier erfahren Sie, wie Sie Layouts für Kategorieseiten und Katalogelementseiten für eine websiteübergreifende SharePoint-Veröffentlichungswebsite erstellen und anpassen können.</span><span class="sxs-lookup"><span data-stu-id="1d0af-103">Learn how to create and customize category page and catalog-item page layouts for a SharePoint cross-site publishing site.</span></span>

## <a name="prerequisites-for-creating-and-customizing-page-layouts-for-a-catalog-based-site"></a><span data-ttu-id="1d0af-104">Voraussetzungen für die Erstellung und Anpassung von Seitenlayouts für eine katalogbasierte Website</span><span class="sxs-lookup"><span data-stu-id="1d0af-104">Prerequisites for creating and customizing page layouts for a catalog-based site</span></span>
<span data-ttu-id="1d0af-105"><a name="bk_prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="1d0af-105"><a name="bk_prereqs"> </a></span></span>

<span data-ttu-id="1d0af-106">Um die Schritte in diesem Beispiel ausführen zu können, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="1d0af-106">To follow the steps in this example, you must have the following:</span></span>
  
    
    

- <span data-ttu-id="1d0af-107">Einen HTML-Editor</span><span class="sxs-lookup"><span data-stu-id="1d0af-107">An HTML editor</span></span>
    
  
- <span data-ttu-id="1d0af-108">Eine websiteübergreifende SharePoint-Veröffentlichungsumgebung</span><span class="sxs-lookup"><span data-stu-id="1d0af-108">A SharePoint cross-site publishing environment</span></span>
    
  
<span data-ttu-id="1d0af-109">Informationen zur Konfiguration einer websiteübergreifenden SharePoint-Veröffentlichungsumgebung finden Sie unter  [Konfigurieren der websiteübergreifenden Veröffentlichung in SharePoint](http://technet.microsoft.com/de-DE/library/jj656774.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d0af-109">For information about how to set up a SharePoint cross-site publishing environment, see  [Configure cross-site publishing in SharePoint](http://technet.microsoft.com/de-DE/library/jj656774.aspx).</span></span>
  
    
    

### <a name="core-concepts-to-know-for-creating-and-customizing-page-layouts-for-a-catalog-based-site"></a><span data-ttu-id="1d0af-110">Kernkonzepte zur Erstellung und Anpassung von Seitenlayouts für eine katalogbasierte Website</span><span class="sxs-lookup"><span data-stu-id="1d0af-110">Core concepts to know for creating and customizing page layouts for a catalog-based site</span></span>

<span data-ttu-id="1d0af-111">In Tabelle 1 sind nützliche Artikel aufgeführt, die Ihnen die Konzepte und Arbeitsschritte zur Erstellung und Anpassung von Seitenlayouts für eine katalogbasierte Website näher bringen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-111">Table 1 lists useful articles that can help you understand the concepts and steps that are involved in creating and customizing page layouts for a catalog-based site.</span></span>
  
    
    

<span data-ttu-id="1d0af-112">**Tabelle 1. Kernkonzepte für die Erstellung und Anpassung von Seitenlayouts für eine katalogbasierte Website**</span><span class="sxs-lookup"><span data-stu-id="1d0af-112">**Table 1. Core concepts for creating and customizing page layouts for a catalog-based site**</span></span>


|<span data-ttu-id="1d0af-113">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="1d0af-113">**Article title**</span></span>|<span data-ttu-id="1d0af-114">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="1d0af-114">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="1d0af-115">Übersicht über die websiteübergreifende Veröffentlichung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d0af-115">Overview of cross-site publishing in SharePoint</span></span>](http://technet.microsoft.com/de-DE/library/jj635883.aspx) <br/> |<span data-ttu-id="1d0af-116">Erfahren Sie, wie Sie mit der websiteübergreifenden Veröffentlichung und Such-Webparts anpassungsfähige SharePoint-Websites für das Internet, Intranet und Extranet erstellen können.</span><span class="sxs-lookup"><span data-stu-id="1d0af-116">Learn about how to use cross-site publishing and Search Web Parts to create adaptive SharePoint Internet, intranet, and extranet sites.</span></span>  <br/> |
| [<span data-ttu-id="1d0af-117">Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d0af-117">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md) <br/> |<span data-ttu-id="1d0af-118">Erfahren Sie, wie Sie Seitenlayouts in SharePoint Server erstellen können.</span><span class="sxs-lookup"><span data-stu-id="1d0af-118">Learn about how to create page layouts in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="1d0af-119">Vorgehensweise: Beheben von Fehlern und Warnungen bei der Vorschau einer Seite in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d0af-119">How to: Resolve errors and warnings when previewing a page in SharePoint</span></span>](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md) <br/> |<span data-ttu-id="1d0af-120">Erfahren Sie, wie Sie Probleme beheben, die verhindern, dass die serverseitige Vorschau Ihre Seite rendert.</span><span class="sxs-lookup"><span data-stu-id="1d0af-120">Learn about how to resolve any issues that prevent the server-side preview from rendering your page.</span></span>  <br/> |
| [<span data-ttu-id="1d0af-121">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="1d0af-121">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md) <br/> |<span data-ttu-id="1d0af-122">Erfahren Sie, wie Sie mit Codeausschnitten der HTML-Masterseite oder dem Seitenlayout SharePoint-Funktionen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-122">Learn about how to use snippets to add SharePoint functionality to your HTML master page or page layout.</span></span>  <br/> |
   

## <a name="introduction-to-category-page-layouts-and-catalog-item-page-layouts"></a><span data-ttu-id="1d0af-123">Einführung in Layouts für Kategorieseiten und Katalogelementseiten</span><span class="sxs-lookup"><span data-stu-id="1d0af-123">Introduction to category page layouts and catalog item page layouts</span></span>
<span data-ttu-id="1d0af-124"><a name="bk_introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="1d0af-124"><a name="bk_introduction"> </a></span></span>

<span data-ttu-id="1d0af-125">Kategorieseiten und Katalogobjektseiten sind Seitenlayouts, die Sie zum konsistenten Anzeigen von strukturiertem Kataloginhalt auf einer Website verwenden können.</span><span class="sxs-lookup"><span data-stu-id="1d0af-125">Category pages and catalog item pages are page layouts that you can use to show structured catalog content consistently across a site.</span></span> <span data-ttu-id="1d0af-126">SharePoint kann standardmäßig ein Kategorieseitenlayout und ein Katalogobjektseiten-Layout pro Katalogverbindung erstellen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-126">By default, SharePoint can automatically create one category page layout and one catalog item page layout per catalog connection.</span></span> <span data-ttu-id="1d0af-127">Seiten, die auf diesen Layouts basieren, werden in der Seitenbibliothek einer Veröffentlichungswebsite erstellt, wenn Sie die Website mit einem Katalog verbinden.</span><span class="sxs-lookup"><span data-stu-id="1d0af-127">Pages based on these layouts are created in the Pages library of a publishing site when you connect the site to a catalog.</span></span> <span data-ttu-id="1d0af-128">Weitere Informationen zu Seitenlayouts finden Sie unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="1d0af-128">For more information about page layouts, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span> <span data-ttu-id="1d0af-129">Weitere Informationen zu Features, die für kategoie-Seitenlayouts und Katalogelement-Seitenlayouts spezifisch sind, finden Sie unter[Übersicht über websiteübergreifende Veröffentlichung in SharePoint](http://technet.microsoft.com/de-DE/library/jj635883.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d0af-129">For more information about features that are specific to category page layouts and catalog item page layouts, see  [Overview of cross-site publishing in SharePoint](http://technet.microsoft.com/de-DE/library/jj635883.aspx).</span></span>
  
    
    
<span data-ttu-id="1d0af-p102">Standardmäßig werden Layouts für Kategorieseiten und Katalogelementseiten automatisch erstellt, wenn Sie eine Veröffentlichungswebsite mit einem Katalog verbinden. Sie können diese Layouts jedoch auch mit dem Entwurfs-Manager erstellen und sie bei der Verbindung der Veröffentlichungswebsite mit einem Katalog oder der Konfiguration eines Navigationsausdruckssatzes auf einer Veröffentlichungswebsite auswählen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p102">By default, category page layouts and catalog item page layouts are created automatically when you connect a publishing site to a catalog. You can also use Design Manager to create category page layouts and catalog item page layouts that you can select when you connect a publishing site to a catalog, or when you configure the navigation term set on a publishing site.</span></span>
  
    
    

## <a name="create-a-category-page-layout"></a><span data-ttu-id="1d0af-132">Erstellen eines Layouts für eine Kategorieseite</span><span class="sxs-lookup"><span data-stu-id="1d0af-132">Create a category page layout</span></span>
<span data-ttu-id="1d0af-133"><a name="bk_createCategoryPage"> </a></span><span class="sxs-lookup"><span data-stu-id="1d0af-133"><a name="bk_createCategoryPage"> </a></span></span>

<span data-ttu-id="1d0af-p103">Vor dem Erstellen oder Anpassen eines Layouts für Kategorieseiten empfehlen wir Ihnen, ein zugeordnetes Netzlaufwerk zu erstellen, das auf den **Gestaltungsvorlagenkatalog** verweist. Weitere Informationen finden Sie unter [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="1d0af-p103">Before you can create or customize a category page layout, we recommend that you create a mapped network drive that points to the **Master Page Gallery**. For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
  
    
    
<span data-ttu-id="1d0af-p104">Die einfachste Methode besteht darin, ein Layout für eine Kategorieseite automatisch bei der Verbindung einer Veröffentlichungswebsite mit einem Katalog von SharePoint erstellen zu lassen und anschließend das Markup des bestehenden Kategorieseitenlayouts an den Seitenentwurf anzupassen. Alternativ können Sie mit dem Entwurfs-Manager ein vollständig neues Layout erstellen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p104">The simplest way to create a category page layout is to let SharePoint create the page layout automatically when you connect the publishing site to a catalog, and then customize the existing category page layout to change the markup as required by the page design. Alternatively, you can create a new category page layout from scratch by using Design Manager.</span></span>
  
    
    

### <a name="to-customize-an-existing-category-page-layout-that-was-created-automatically-by-sharepoint"></a><span data-ttu-id="1d0af-138">So passen Sie ein automatisch von SharePoint erstelltes Layout für eine Kategorieseite an</span><span class="sxs-lookup"><span data-stu-id="1d0af-138">To customize an existing category page layout that was created automatically by SharePoint</span></span>


1. <span data-ttu-id="1d0af-139">Öffnen Sie im Windows-Explorer das zugeordnete Netzlaufwerk, das auf den Gestaltungsvorlagenkatalog verweist.</span><span class="sxs-lookup"><span data-stu-id="1d0af-139">Using Windows Explorer, open the mapped network drive to the Master Page Gallery.</span></span>
    
  
2. <span data-ttu-id="1d0af-p105">Um das Layout für die Kategorieseite anzupassen, bearbeiten Sie die HTML-Datei auf dem Server mit einem HTML-Editor. Öffnen Sie dazu die HTML-Datei mit einem HTML-Editor im zugeordneten Netzlaufwerk, und bearbeiten Sie sie. Nach jedem Speichervorgang werden die Änderungen mit der entsprechenden ASPX-Datei synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p105">To customize a category page layout, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time that you save the HTML file, any changes are synched to the associated .aspx file.</span></span>
    
  
3. <span data-ttu-id="1d0af-142">Ersetzen Sie das Markup innerhalb des Inhaltsplatzhalters, der **id="PlaceHolderMain"** beinhaltet, durch das Markup, das Sie im Seitenlayout verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="1d0af-142">Replace the markup inside the content placeholder that has **id="PlaceHolderMain"** with the markup that you want to use in the page layout.</span></span>
    
    > <span data-ttu-id="1d0af-143">**Wichtig:** Der Markupcodeausschnitt für die Inhaltssuche muss erhalten bleiben, damit auf der Kategorieseite Suchergebnisse angezeigt werden können.</span><span class="sxs-lookup"><span data-stu-id="1d0af-143">**Important:** You must keep the Content Search Snippet markup so that the category page can display search results.</span></span> 
4. <span data-ttu-id="1d0af-144">Um den HTML-Code für alle Codeausschnitte, die Sie der Seite hinzufügen möchten, zu konfigurieren und zu kopieren, befolgen Sie die Schritte 1 bis 11 im Abschnitt „Einfügen eines Codeausschnitts aus dem Codeausschnittkatalog" unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="1d0af-144">To configure and copy the HTML for any snippets you want to add to the page, follow step 1 through step 11 in the "Insert a snippet from the Snippet Gallery" section of  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  
5. <span data-ttu-id="1d0af-145">Nehmen Sie alle weiteren gewünschten Änderungen am Markup vor, und speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="1d0af-145">Make any other required changes to the markup, and then save the file.</span></span>
    
  
6. <span data-ttu-id="1d0af-146">Befolgen Sie die Schritte 9 bis 11 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md), um den Dateistatus zu prüfen, eine Vorschau des Seitenlayouts zur erstellen und mögliche Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="1d0af-146">Follow step 9 through step 11 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md) to check the status of the file, preview the page layout, and fix any errors.</span></span>
    
  

### <a name="to-create-a-category-page-layout-by-using-design-manager"></a><span data-ttu-id="1d0af-147">So erstellen Sie ein Kategorieseitenlayout mit dem Entwurfs-Manager</span><span class="sxs-lookup"><span data-stu-id="1d0af-147">To create a category page layout by using Design Manager</span></span>


1. <span data-ttu-id="1d0af-148">Befolgen Sie die Schritte 1 bis 6 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="1d0af-148">Follow step 1 through step 6 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
    
  
2. <span data-ttu-id="1d0af-149">Wählen Sie bei Schritt 7 den Inhaltstyp **Artikelseite**.</span><span class="sxs-lookup"><span data-stu-id="1d0af-149">In step 7, choose the **Article Page** content type.</span></span>
    
  
3. <span data-ttu-id="1d0af-150">Wählen Sie **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="1d0af-150">Choose **OK**.</span></span>
    
    <span data-ttu-id="1d0af-151">SharePoint erstellt jetzt eine HTML-Datei und eine ASPX-Datei mit dem gleichen Namen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-151">At this point, SharePoint creates an HTML file and an .aspx file that has the same name.</span></span>
    
    <span data-ttu-id="1d0af-152">Im Entwurfs-Manager wird die HTML-Datei nun mit der Spalte **Status** angezeigt, die einen der beiden folgenden Status hat:</span><span class="sxs-lookup"><span data-stu-id="1d0af-152">In Design Manager, your HTML file now appears with a **Status** column that shows one of two statuses:</span></span>
    
  - <span data-ttu-id="1d0af-153">Fehler</span><span class="sxs-lookup"><span data-stu-id="1d0af-153">**Warnings and Errors**</span></span>
    
  
  - <span data-ttu-id="1d0af-154">**Konvertierung erfolgreich**</span><span class="sxs-lookup"><span data-stu-id="1d0af-154">**Conversion successful**</span></span>
    
  
4. <span data-ttu-id="1d0af-155">Öffnen Sie im Windows-Explorer das Netzlaufwerk, das auf den Gestaltungsvorlagenkatalog verweist.</span><span class="sxs-lookup"><span data-stu-id="1d0af-155">Using Windows Explorer, open the mapped network drive to the Master Page Gallery.</span></span>
    
  
5. <span data-ttu-id="1d0af-p106">Um das Layout für die Kategorieseite anzupassen, bearbeiten Sie die HTML-Datei, die sich auf dem Server befindet, mit einem HTML-Editor. Nach jedem Speichervorgang werden die Änderungen mit der entsprechenden ASPX-Datei synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p106">To customize the category page layout, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time that you save the HTML file, any changes are synched to the associated .aspx file.</span></span>
    
  
6. <span data-ttu-id="1d0af-158">Ersetzen Sie im Tag **\<head\>** den Inhaltsplatzhalter **id="PlaceHolderPageTitle"** durch:</span><span class="sxs-lookup"><span data-stu-id="1d0af-158">In the **\<head\>** tag, replace the content placeholder that has **id="PlaceHolderPageTitle"** with:</span></span>
    
```HTML
  
<!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
<!--CS: Start Taxonomy TermProperty Snippet-->
<!--SPM:<%@Register Tagprefix="Taxonomy"  Namespace="Microsoft.SharePoint.Taxonomy" Assembly="Microsoft.SharePoint.Taxonomy, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>-->
<!--MS:<Taxonomy:TermProperty Property="Name" runat="server">-->
<!--ME:</Taxonomy:TermProperty>-->
<!--ME:</asp:ContentPlaceHolder>-->
```

7. <span data-ttu-id="1d0af-159">Suchen Sie nach dem Inhaltsplatzhalter mit **id="PlaceHolderPageTitleInTitleArea"**, und ersetzen Sie ihn durch:</span><span class="sxs-lookup"><span data-stu-id="1d0af-159">Find the content placeholder that has the **id="PlaceHolderPageTitleInTitleArea"** and replace it with:</span></span>
    
```HTML
  
<!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitleInTitleArea" runat="server">-->
<!--SPM:<asp:SiteMapPath runat="server" ParentLevelsDisplayed="1" SiteMapProvider="CurrentNavigationSwitchableProvider"/>-->
<!--ME:</asp:ContentPlaceHolder>-->
```

8. <span data-ttu-id="1d0af-160">Ersetzen Sie das Markup innerhalb des Inhaltsplatzhalters, der **id="PlaceHolderMain"** beinhaltet, durch das Markup, das Sie im Seitenlayout verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="1d0af-160">Replace the markup inside the content placeholder that has **id="PlaceHolderMain"** with the markup that you want to use in the page layout.</span></span>
    
  
9. <span data-ttu-id="1d0af-161">Um den HTML-Code für den Inhaltssuche-Codeausschnitt und alle weiteren Codeausschnitte, die Sie der Seite hinzufügen möchten, zu konfigurieren und zu kopieren, befolgen Sie die Schritte 1 bis 11 im Abschnitt „Einfügen eines Codeausschnitts aus dem Codeausschnittkatalog" unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="1d0af-161">To configure and copy the HTML for the Content Search Snippet and any other snippets you want to add to the page, follow step 1 through step 11 in the "Insert a snippet from the Snippet Gallery" section of  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
    > <span data-ttu-id="1d0af-162">**Hinweis:** Wenn Sie den Inhaltssuche-Codeausschnitt zum Seitenlayout hinzufügen, ändern Sie die Abfrage so, dass die Ergebnisquelle verwendet wird, die erstellt wurde, als Sie die Veröffentlichungswebsite mit einem Katalog verbunden haben.</span><span class="sxs-lookup"><span data-stu-id="1d0af-162">**Note:** When you add the Content Search Snippet to the page layout, be sure to change the query to use the result source that was created when you connected the publishing site to a catalog.</span></span> <span data-ttu-id="1d0af-163">Weitere Informationen finden Sie unter [Konfigurieren von Ergebnisquellen für Web Content Management in SharePoint](http://technet.microsoft.com/de-DE/library/jj715262.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d0af-163">For more information, see  [Configure result sources for web content management in SharePoint](http://technet.microsoft.com/de-DE/library/jj715262.aspx).</span></span> 
10. <span data-ttu-id="1d0af-164">Nehmen Sie alle weiteren gewünschten Änderungen am Markup vor, und speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="1d0af-164">Make any other required changes to the markup, and then save the file.</span></span>
    
  
11. <span data-ttu-id="1d0af-165">Befolgen Sie die Schritte 9 bis 11 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md), um den Dateistatus zu prüfen, eine Vorschau des Seitenlayouts zur erstellen und mögliche Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="1d0af-165">Follow step 9 through step 11 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md) to check the status of the file, preview the page layout, and fix any errors.</span></span>
    
  

## <a name="understanding-the-markup-in-the-html-category-page-layout"></a><span data-ttu-id="1d0af-166">Grundlegendes zum Markup im HTML-Layout der Kategorieseite</span><span class="sxs-lookup"><span data-stu-id="1d0af-166">Understanding the markup in the HTML category page layout</span></span>
<span data-ttu-id="1d0af-167"><a name="bk_CategoryPageMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="1d0af-167"><a name="bk_CategoryPageMarkup"> </a></span></span>

<span data-ttu-id="1d0af-p108">Wenn Sie ein Seitenlayout erstellen, wird eine ASPX-Datei zur Verwendung durch SharePoint erstellt, und der HTML-Datei für das Seitenlayout wird HTML-Code hinzugefügt. Layouts für Kategorieseiten umfassen Markupkomponenten, die dem Seitenlayout basierend auf der Funktion zur websiteübergreifenden Veröffentlichung von Sammlungen hinzugefügt werden und die speziell für Kategorieseitenlayouts gelten. Möglicherweise fällt Ihnen die Bearbeitung des HTML-Kategorieseitenlayouts leichter, wenn Sie sich im Folgenden näher mit dem Markup vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p108">When you create a page layout, an .aspx file is created that SharePoint uses, and some HTML markup is added to the HTML version of the page layout. Category page layouts have markup components that are added to the page layout based on the Cross-Site Collection Publishing feature, and that are unique to category page layouts. When you edit the HTML category page layout in your HTML editor, it might be helpful to understand some of this markup.</span></span>
  
    
    

### <a name="browser-window-page-title"></a><span data-ttu-id="1d0af-171">Seitentitel im Browserfenster</span><span class="sxs-lookup"><span data-stu-id="1d0af-171">Browser window page title</span></span>

<span data-ttu-id="1d0af-p109">Die Komponente im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderPageTitle"** enthält Markup, mit dem SharePoint angewiesen wird, eine Begriffseigenschaft als Seitentitel im Browserfenster zu verwenden, anstelle des Standardseiten-Feldwerts. Dieses Markup wird im folgenden Codebeispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p109">The component that appears inside the content placeholder with **id="PlaceHolderPageTitle"** contains markup that tells SharePoint to use a term property as the page title in the browser window, instead of using the standard page field value. The following code shows the markup for the browser window page title.</span></span>
  
    
    

```HTML

<!--CS: Start Taxonomy TermProperty Snippet-->
<!--SPM:<%@Register Tagprefix="Taxonomy"  Namespace="Microsoft.SharePoint.Taxonomy" Assembly="Microsoft.SharePoint.Taxonomy, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c" %>-->
<!--MS:<Taxonomy:TermProperty Property="Name" runat="server">-->
<!--ME:</Taxonomy:TermProperty>-->
```


### <a name="page-title"></a><span data-ttu-id="1d0af-174">Seitentitel</span><span class="sxs-lookup"><span data-stu-id="1d0af-174">Page title</span></span>

<span data-ttu-id="1d0af-p110">Die Komponente im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderPageTitleInTitleArea"** enthält Markup, mit dem SharePoint angewiesen wird, eine Begriffseigenschaft als Seitentitel auf der Seite zu verwenden, anstelle des Codeausschnitts **SPTitleBreadcrumb** und des Standardseiten-Feldwerts. Dieses Markup wird im folgenden Codebeispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p110">The component that appears inside the content placeholder with **id="PlaceHolderPageTitleInTitleArea"** contains markup that tells SharePoint to use a term property as the page title on the page, instead of using the **SPTitleBreadcrumb** snippet and the standard page title field value. The following code shows the markup for the page title.</span></span>
  
    
    

```HTML

<!--SPM:<asp:SiteMapPath runat="server" ParentLevelsDisplayed="1" SiteMapProvider="CurrentNavigationSwitchableProvider"/>-->"
```


### <a name="content-search-snippet"></a><span data-ttu-id="1d0af-177">Inhaltssuche-Codeausschnitt</span><span class="sxs-lookup"><span data-stu-id="1d0af-177">Content Search Snippet</span></span>

<span data-ttu-id="1d0af-p111">Die Komponente, die auf den Seiteninhalts-Codeausschnitt im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderMain"** folgt, enthält Markup für einen Webpart-Zonencodeausschnitt mit vier Webpartzonen. Die erste Webpartzone enthält einen Inhaltssuche-Codeausschnitt, mit dem ein Inhaltssuche-Webpart auf der Seite angezeigt wird. Dieser Codeausschnitt enthält des Weiteren Informationen, die zur Abfrage der Ergebnisquelle und Anzeige der Ergebnisse auf der Seite benötigt werden. Die weiteren drei Webpartzonen sind leer. Möchten Sie ein benutzerdefiniertes Layout für Kategorieseiten erstellen, muss das Markup für den Inhaltssuche-Codeausschnitt in der HTML-Datei des Seitenlayouts eingefügt werden. Das folgende Codebeispiel zeigt das Markup für den Inhaltssuche-Codeausschnitt. Ersetzen Sie _ResultSourceID_ durch die GUID der Ergebnisquelle und _CatalogURL_ durch die URL des Katalogs.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p111">The components that appear after the page content snippet, inside the content placeholder with **id="PlaceHolderMain"**, contain markup for a Web Part Zone Snippet that contains four Web Part zones. The first Web Part zone contains a Content Search Snippet that displays a Content Search Web Part on the page. This snippet also contains information that helps the Content Search Web Part query a result source and show the results on the page. The last three Web Part zones are empty. If you choose to create your own category page layout, you must include the markup for the Content Search Snippet in the HTML file for your page layout. The following code shows the markup for the Content Search snippet. Replace  _ResultSourceID_ with the GUID of the result source, and replace _CatalogURL_ with the URL of the catalog.</span></span>
  
    
    

> <span data-ttu-id="1d0af-185">**Hinweis:** Die GUIDS für **ID** und **\_\_WebPartId** werden von SharePoint nach dem Zufallsprinzip generiert, wenn dem Seitenlayout Codeausschnitte hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="1d0af-185">**Note:** The GUIDs for **ID** and **\_\_WebPartId** are randomly generated by SharePoint when the snippets are added to the page layout.</span></span>
  
    
    


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


## <a name="create-a-catalog-item-page-layout"></a><span data-ttu-id="1d0af-186">Erstellen eines Seitenlayouts für ein Katalogelement</span><span class="sxs-lookup"><span data-stu-id="1d0af-186">Create a catalog item page layout</span></span>
<span data-ttu-id="1d0af-187"><a name="bk_createCatItemPage"> </a></span><span class="sxs-lookup"><span data-stu-id="1d0af-187"><a name="bk_createCatItemPage"> </a></span></span>

<span data-ttu-id="1d0af-p112">Vor dem Erstellen oder Anpassen eines Layouts für Kategorieelemente empfehlen wir Ihnen, ein zugeordnetes Netzlaufwerk zu erstellen, das auf den Gestaltungsvorlagenkatalog verweist. Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="1d0af-p112">Before you can create or customize a catalog item page layout, we recommend that you create a mapped network drive that points to the Master Page Gallery. For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
  
    
    
<span data-ttu-id="1d0af-p113">Ähnlich wie beim Kategorieseitenlayout ist auch beim Erstellen eines Katalogelement-Seitenlayouts die einfachste Methode, das Seitenlayout von SharePoint automatisch erstellen zu lassen, wenn Sie die Veröffentlichungswebsite mit einem Katalog verbinden. Anschließend passen Sie das vorhandenen Katalogelement-Seitenlayout an, um von Seitenentwurf zusätzlich erfordertes Markup hinzuzufügen. Alternativ können Sie mithilfe des Entwurfs-Managers ein Katalogelement-Seitenlayout von Grund auf neu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p113">As with the category page layout, the simplest way to create a catalog item page layout is to let SharePoint create the page layout automatically when you connect the publishing site to a catalog, and then customize the existing catalog item page layout to add any additional markup required by the page design. Alternatively, you can create a catalog item page layout from scratch by using Design Manager.</span></span>
  
    
    

### <a name="to-customize-an-existing-catalog-item-page-layout-that-was-created-automatically-by-sharepoint"></a><span data-ttu-id="1d0af-192">So bearbeiten Sie ein bestehendes Layout für ein Kategorieelement, das automatisch von SharePoint erstellt wurde</span><span class="sxs-lookup"><span data-stu-id="1d0af-192">To customize an existing catalog item page layout that was created automatically by SharePoint</span></span>


1. <span data-ttu-id="1d0af-193">Öffnen Sie im Windows-Explorer das Netzlaufwerk, das auf den Gestaltungsvorlagenkatalog verweist.</span><span class="sxs-lookup"><span data-stu-id="1d0af-193">Using Windows Explorer, open the mapped network drive to the Master Page Gallery.</span></span>
    
  
2. <span data-ttu-id="1d0af-p114">Um das Layout für die Katalogelementseite anzupassen, bearbeiten Sie die HTML-Datei, die sich auf dem Server befindet, mit einem HTML-Editor. Nach jedem Speichervorgang werden die Änderungen mit der entsprechenden ASPX-Datei synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p114">To customize a catalog item page layout, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time that you save the HTML file, any changes are synched to the associated .aspx file.</span></span>
    
  
3. <span data-ttu-id="1d0af-196">Fügen Sie das Markup, das Sie im Seitenlayout verwenden möchten, im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderMain"** hinzu.</span><span class="sxs-lookup"><span data-stu-id="1d0af-196">Inside the content placeholder that has **id="PlaceHolderMain"**, add the markup that you want to use in the page layout.</span></span>
    
  
4. <span data-ttu-id="1d0af-197">Löschen Sie alle Codeausschnitte, die Sie nicht im Seitenlayout verwenden möchten, und verschieben Sie die verbleibenden Codeausschnitte an die Stellen, an denen die Werte der Eigenschaften angezeigt sollen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-197">Delete any snippets that you do not want to use in the page layout, and move the remaining snippets to places in the markup where you want the property values to appear.</span></span>
    
    > <span data-ttu-id="1d0af-198">**Achtung:** Standardmäßig wird dem Seitenlayout ein Webpartzone-Codeausschnitt hinzugefügt, der einen Codeausschnitt zur Wiederverwendung von Katalogobjekten enthält.</span><span class="sxs-lookup"><span data-stu-id="1d0af-198">**Caution:** By default, a Web Part Zone Snippet that contains a Catalog-Item Reuse Snippet is added to the page layout.</span></span> <span data-ttu-id="1d0af-199">Dieser Codeausschnitt enthält den Datenanbieter, der Abfrageergebnisse zurückgibt, die von allen anderen Codeausschnitten auf der Seite verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1d0af-199">This snippet contains the data provider that returns query results that are used by all other snippets on the page.</span></span> <span data-ttu-id="1d0af-200">Es wird empfohlen, dass Sie den Codeausschnitt zur Wiederverwendung von Katalogobjekten in diesem standardmäßigen Webpartzone-Codeausschnitt belassen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-200">We recommend that you keep the Catalog-Item Reuse Snippet in this default Web Part Zone Snippet.</span></span> <span data-ttu-id="1d0af-201">(Sie können den Codeausschnitt zur Wiederverwendung von Katalogobjekten außerhalb der Webpartzone verschieben und die angezeigte Eigenschaft ändern.</span><span class="sxs-lookup"><span data-stu-id="1d0af-201">(You can move the Catalog-Item Reuse Snippet outside the Web Part Zone, and you can change the property that it displays.</span></span> <span data-ttu-id="1d0af-202">Aber Sie müssen den Codeausschnitt zur Wiederverwendung von Katalogobjekten im Seitenlayout belassen.) Weitere Informationen finden Sie unter [Seitenfelder](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields)weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="1d0af-202">But, you must keep the Catalog-Item Reuse Snippet in the page layout.) For more information, see  [Page fields](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields), later in this article.</span></span> 
5. <span data-ttu-id="1d0af-203">Um den HTML-Code für alle Codeausschnitte, die Sie auf der Seite verwenden möchten, zu konfigurieren und zu kopieren, befolgen Sie die Schritte 1 bis 11 im Abschnitt „Einfügen eines Codeausschnitts aus dem Codeausschnittkatalog" unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="1d0af-203">To configure and copy the HTML snippet for any snippets you want to use in the page, follow step 1 through step 11 in the "Insert a snippet from the Snippet Gallery" section of  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  
6. <span data-ttu-id="1d0af-204">Nehmen Sie alle weiteren gewünschten Änderungen am Markup vor, und speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="1d0af-204">Make any other required changes to the markup, and then save the file.</span></span>
    
  
7. <span data-ttu-id="1d0af-205">Befolgen Sie die Schritte 9 bis 11 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md), um den Dateistatus zu prüfen, eine Vorschau des Seitenlayouts zur erstellen und mögliche Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="1d0af-205">Follow step 9 through step 11 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md) to check the status of the file, preview the page layout, and fix any errors.</span></span>
    
  

### <a name="to-create-a-catalog-item-page-layout-by-using-design-manager"></a><span data-ttu-id="1d0af-206">So erstellen Sie mit dem Entwurfs-Manager ein Layout für eine Katalogelementseite</span><span class="sxs-lookup"><span data-stu-id="1d0af-206">To create a catalog item page layout by using Design Manager</span></span>


1. <span data-ttu-id="1d0af-207">Befolgen Sie die Schritte 1 bis 6 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="1d0af-207">Follow step 1 through step 6 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
    
  
2. <span data-ttu-id="1d0af-208">Wählen Sie in Schritt 7 **Remotekatalog**, und wählen Sie dann den Katalog mit den Daten, die auf der Seite angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-208">In step 7, choose **Remote Catalog**, and then choose the catalog that contains the data to appear on the page.</span></span>
    
  
3. <span data-ttu-id="1d0af-209">Wählen Sie **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="1d0af-209">Choose **OK**.</span></span>
    
    <span data-ttu-id="1d0af-210">SharePoint erstellt jetzt eine HTML-Datei und eine ASPX-Datei mit dem gleichen Namen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-210">At this point, SharePoint creates an HTML file and an .aspx file that has the same name.</span></span>
    
    <span data-ttu-id="1d0af-211">Im Entwurfs-Manager wird die HTML-Datei nun mit der Spalte **Status** angezeigt, die einen der beiden folgenden Status hat:</span><span class="sxs-lookup"><span data-stu-id="1d0af-211">In Design Manager, your HTML file now appears with a **Status** column that shows one of two statuses:</span></span>
    
  - <span data-ttu-id="1d0af-212">Fehler</span><span class="sxs-lookup"><span data-stu-id="1d0af-212">**Warnings and Errors**</span></span>
    
  
  - <span data-ttu-id="1d0af-213">**Konvertierung erfolgreich**</span><span class="sxs-lookup"><span data-stu-id="1d0af-213">**Conversion successful**</span></span>
    
  
4. <span data-ttu-id="1d0af-214">Öffnen Sie im Windows-Explorer das Netzlaufwerk, das auf den Gestaltungsvorlagenkatalog verweist.</span><span class="sxs-lookup"><span data-stu-id="1d0af-214">Using Windows Explorer, open the mapped network drive to the Master Page Gallery.</span></span>
    
  
5. <span data-ttu-id="1d0af-p116">Um das Layout für die Katalogelementseite anzupassen, bearbeiten Sie HTML-Datei, die sich auf dem Server befindet, mit einem HTML-Editor. Nach jedem Speichervorgang werden die Änderungen mit der entsprechenden ASPX-Datei synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p116">To customize the catalog item page layout, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time that you save the HTML file, any changes are synched to the associated .aspx file.</span></span>
    
  
6. <span data-ttu-id="1d0af-217">Fügen Sie das Markup, das Sie im Seitenlayout verwenden möchten, im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderMain"** hinzu.</span><span class="sxs-lookup"><span data-stu-id="1d0af-217">Inside the content placeholder that has **id="PlaceHolderMain"**, add the markup that you want to use in the page layout.</span></span>
    
  
7. <span data-ttu-id="1d0af-218">Löschen Sie alle Codeausschnitte, die Sie nicht im Seitenlayout verwenden möchten, und verschieben Sie die verbleibenden Codeausschnitte an die Stellen, an denen die Werte der Eigenschaften angezeigt sollen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-218">Delete any snippets that you do not want to use in the page layout, and move the remaining snippets to places in the markup where you want the property values to appear.</span></span>
    
    > <span data-ttu-id="1d0af-219">**Achtung:** Standardmäßig wird dem Seitenlayout ein Webpartzone-Codeausschnitt hinzugefügt, der einen Codeausschnitt zur Wiederverwendung von Katalogobjekten enthält.</span><span class="sxs-lookup"><span data-stu-id="1d0af-219">**Caution:** By default, a Web Part Zone Snippet that contains a Catalog-Item Reuse Snippet is added to the page layout.</span></span> <span data-ttu-id="1d0af-220">Dieser Codeausschnitt enthält den Datenanbieter, der Abfrageergebnisse zurückgibt, die von allen anderen Codeausschnitten auf der Seite verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1d0af-220">This snippet contains the data provider that returns query results that are used by all other snippets on the page.</span></span> <span data-ttu-id="1d0af-221">Es wird empfohlen, dass Sie den Codeausschnitt zur Wiederverwendung von Katalogobjekten in diesem standardmäßigen Webpartzone-Codeausschnitt belassen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-221">We recommend that you keep the Catalog-Item Reuse Snippet in this default Web Part Zone Snippet.</span></span> <span data-ttu-id="1d0af-222">(Sie können den Codeausschnitt zur Wiederverwendung von Katalogobjekten außerhalb der Webpartzone verschieben und die angezeigte Eigenschaft ändern.</span><span class="sxs-lookup"><span data-stu-id="1d0af-222">(You can move the Catalog-Item Reuse Snippet outside the Web Part Zone, and you can change the property that it displays.</span></span> <span data-ttu-id="1d0af-223">Aber Sie müssen den Codeausschnitt zur Wiederverwendung von Katalogobjekten im Seitenlayout belassen.) Weitere Informationen finden Sie unter [Seitenfelder](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields)weiter unten in diesem Artikel.</span><span class="sxs-lookup"><span data-stu-id="1d0af-223">But, you must keep the Catalog-Item Reuse Snippet in the page layout.) For more information, see  [Page fields](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields), later in this article.</span></span> 
8. <span data-ttu-id="1d0af-224">Um den HTML-Code für alle Codeausschnitte, die Sie auf der Seite verwenden möchten, zu konfigurieren und zu kopieren, befolgen Sie die Schritte 1 bis 11 im Abschnitt „Einfügen eines Codeausschnitts aus dem Codeausschnittkatalog" unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="1d0af-224">To configure and copy the HTML snippet for any snippets you want to use in the page, follow step 1 through step 11 in the "Insert a snippet from the Snippet Gallery" section of  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  
9. <span data-ttu-id="1d0af-225">Nehmen Sie alle weiteren gewünschten Änderungen am Markup vor, und speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="1d0af-225">Make any other required changes to the markup, and then save the file.</span></span>
    
  
10. <span data-ttu-id="1d0af-226">Befolgen Sie die Schritte 9 bis 11 im Abschnitt „Erstellen eines Seitenlayouts" unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md), um den Dateistatus zu prüfen, eine Vorschau des Seitenlayouts zur erstellen und mögliche Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="1d0af-226">Follow step 9 through step 11 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md) to check the status of the file, preview the page layout, and fix any errors.</span></span>
    
  

## <a name="understanding-the-markup-in-the-html-catalog-item-page-layout"></a><span data-ttu-id="1d0af-227">Grundlegendes zum Markup im HTML-Layout für Katalogelementseiten</span><span class="sxs-lookup"><span data-stu-id="1d0af-227">Understanding the markup in the HTML catalog item page layout</span></span>
<span data-ttu-id="1d0af-228"><a name="bk_CatItemMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="1d0af-228"><a name="bk_CatItemMarkup"> </a></span></span>

<span data-ttu-id="1d0af-p118">Wenn Sie ein Seitenlayout erstellen, wird eine ASPX-Datei zur Verwendung durch SharePoint erstellt, und der HTML-Datei für das Seitenlayout wird HTML-Code hinzugefügt. Layouts für Katalogelementseiten umfassen Markupkomponenten, die dem Seitenlayout basierend auf der Funktion zur websiteübergreifenden Veröffentlichung von Sammlungen hinzugefügt werden und die speziell für Katalogelement-Seitenlayouts gelten. Möglicherweise fällt Ihnen die Bearbeitung des HTML-Katalogelement-Seitenlayouts leichter, wenn Sie sich im Folgenden näher mit dem Markup vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p118">When you create a page layout, an .aspx file is created that SharePoint uses, and some HTML markup is added to the HTML version of the page layout. Catalog item page layouts have markup components that are added to the page layout based on the Cross-Site Collection Publishing feature, and that are unique to catalog item page layouts. When you edit the HTML catalog item page layout in your HTML editor, it might be helpful to understand some of this markup.</span></span>
  
    
    

### <a name="browser-window-page-title"></a><span data-ttu-id="1d0af-232">Seitentitel im Browserfenster</span><span class="sxs-lookup"><span data-stu-id="1d0af-232">Browser window page title</span></span>

<span data-ttu-id="1d0af-p119">Die Komponente im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderPageTitle"** enthält einen Codeausschnitt zur Wiederverwendung von Katalogelementen, mit dem SharePoint angewiesen wird, den Namen des Katalogelements als Seitentitel im Browserfenster zu verwenden, anstelle des Standardseiten-Feldwerts. Dieses Markup wird im folgenden Codebeispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p119">The component that appears inside the content placeholder with **id="PlaceHolderPageTitle"** contains a Catalog-Item Reuse Snippet that tells SharePoint to use the name of the catalog item as the page title in the browser window, instead of using the standard page title field value. The following code shows the markup for the browser window page title.</span></span>
  
    
    

> <span data-ttu-id="1d0af-235">**Hinweis:** Die GUIDS für **ID** und **__WebPartId** werden von SharePoint nach dem Zufallsprinzip generiert, wenn dem Seitenlayout Codeausschnitte hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="1d0af-235">**Note:** The GUIDs for **ID** and **__WebPartId** are randomly generated by SharePoint when the snippets are added to the page layout.</span></span>
  
    
    


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


### <a name="page-fields"></a><span data-ttu-id="1d0af-236">Seitenfelder</span><span class="sxs-lookup"><span data-stu-id="1d0af-236">Page fields</span></span>
<span data-ttu-id="1d0af-237"><a name="bk_pagefields"> </a></span><span class="sxs-lookup"><span data-stu-id="1d0af-237"><a name="bk_pagefields"> </a></span></span>

<span data-ttu-id="1d0af-p120">Die Komponenten im Inhaltsplatzhalter mit dem Attribut **id="PlaceHolderMain"** enthalten Codeausschnitte für die Felder **Title**, **Page Content** und **Catalog-Item URL**. Sie können diese Codeausschnitte auf Wunsch aus dem Seitenlayout löschen. Das folgende Codebeispiel zeigt das Markup für diese Seitenfelder.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p120">The components that appear inside the content placeholder with **id="PlaceHolderMain"** contain snippets for the **Title**, **Page Content**, and **Catalog-Item URL** fields. You may delete any of these snippets from the page layout. The following code shows the markup for these page fields.</span></span>
  
    
    

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

<span data-ttu-id="1d0af-p121">Wenn das Katalogelement-Seitenlayout automatisch bei der Verbindung der Veröffentlichungswebsite mit dem Katalog erstellt wurde oder indem ein Remotekatalog bei der Erstellung des Seitenlayouts ausgewählt wurde, enthält das Seitenlayout außerdem einen Webpartzonen-Codeausschnitt mit einem Codeausschnitt zur Wiederverwendung von Katalogelementen, in dem der Datenanbieter für die Seite registriert ist. Der Codeausschnitt zur Wiederverwendung von Katalogelementen enthält die Eigenschaft **UseSharedDataProvider**, deren Wert auf **False** gesetzt ist. Der Webpartzonen-Codeausschnitt kann aus dem Seitenlayout gelöscht werden. Damit die Seite weiterhin Katalogelemente anzeigen kann, muss der Codeausschnitt zur Wiederverwendung von Katalogelementen allerdings im Seitenlayout verbleiben. Wenn Sie eine Seite mit diesem Seitenlayout erstellen, können Sie den Webpart so einstellen, dass er beim Aufrufen der Seite ausgeblendet wird.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p121">If the catalog item page layout was created automatically when the publishing site was connected to a catalog, or was created by selecting a remote catalog during page layout creation, the page layout also contains a Web Part Zone Snippet that contains a Catalog-Item Reuse Snippet that registers a data provider for the page. The Catalog-Item Reuse Snippet contains a **UseSharedDataProvider** property, which is set to **False**. The Web Part Zone Snippet can be deleted from the page layout. But, the Catalog-Item Reuse Snippet must be kept in the page layout markup for the page to display catalog items. When you create a page that uses this page layout, you can configure the Web Part so that it is hidden when a user views the page.</span></span>
  
    
    

> <span data-ttu-id="1d0af-246">**Wichtig:** Wenn Sie ein neues Katalogelement-Seitenlayout erstellen und einen Inhaltstyp anstelle eines Remotekatalogs auswählen, müssen Sie einen Codeausschnitt zur Wiederverwendung von Katalogobjekten in das Seitenlayout einschließen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-246">**Important:** If you create a new catalog item page layout, and you choose a content type instead of a remote catalog, you must include a Catalog-Item Reuse Snippet in the page layout.</span></span> <span data-ttu-id="1d0af-247">Der folgende Code zeigt das Markup für den Codeausschnitt zur Wiederverwendung von Katalogobjekten, wie er innerhalb des Webpartzone-Codeausschnitts angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="1d0af-247">The following code shows the markup for the Catalog-Item Reuse Snippet as it appears inside the Web Part Zone Snippet.</span></span> <span data-ttu-id="1d0af-248">Ersetzen Sie _ManagedPropertyName_ durch den Namen der verwalteten Eigenschaft, die angezeigt werden soll, ersetzen Sie _ResultSourceID_ durch die GUID der Ergebnisquelle, und ersetzen Sie _CatalogURL_ durch die URL des Katalogs.</span><span class="sxs-lookup"><span data-stu-id="1d0af-248">Replace  _ManagedPropertyName_ with the name of the managed property to display, replace _ResultSourceID_ with the GUID of the result source, and replace _CatalogURL_ with the URL of the catalog.</span></span>
  
    
    




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

<span data-ttu-id="1d0af-p123">Wenn das Katalogelement-Seitenlayout automatisch bei der Verbindung der Veröffentlichungswebsite mit dem Katalog erstellt wurde oder indem ein Remotekatalog bei der Erstellung des Seitenlayouts ausgewählt wurde, enthält die restliche Seite Codeausschnitte zur Wiederverwendung von Katalogelementen, die den verwalteten Eigenschaften des Katalogs auf der Erstellungsseite entsprechen. Über diese verwalteten Eigenschaften werden die Details zu einem bestimmten Katalogelement unter Verwendung des Seitenlayouts für Katalogelemente angezeigt. Diese Codesausschnitte zur Wiederverwendung von Katalogelementen erscheinen außerhalb der Webpartzone und werden direkt auf der Seite gerendert, wenn ein Element auf der Kategorieseite ausgewählt wird. In Tabelle 2 sind die verwalteten Eigenschaften aufgeführt, die automatisch im Katalogelement-Seitenlayout enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p123">If the catalog item page layout was created automatically when the publishing site was connected to a catalog, or was created by selecting a remote catalog during page layout creation, the rest of the page contains Catalog-Item Reuse Snippets that correspond to managed properties from the catalog on the authoring site. These managed properties display the details for the specific catalog item that is displayed by using the catalog item page layout. These Catalog-Item Reuse Snippets appear outside the Web Part zone, and are rendered directly on the page when an item is chosen on a category page. Table 2 lists the managed properties that are automatically included in the catalog item page layout.</span></span>
  
    
    

> <span data-ttu-id="1d0af-253">**Hinweis:** Einige verwaltete Eigenschaften sind nur enthalten, wenn der Katalog eine Bibliothek für Seiten ist.</span><span class="sxs-lookup"><span data-stu-id="1d0af-253">**Note:** Some managed properties are included only if the catalog is a Pages library.</span></span> <span data-ttu-id="1d0af-254">In Tabelle 2 wird in der Spalte **Verwendet von** angegeben, welche verwalteten Eigenschaften von Bibliotheken für Seiten und von Listen verwendet werden und welche ausschließlich von Bibliotheken für Seiten.</span><span class="sxs-lookup"><span data-stu-id="1d0af-254">The **Used by** column in Table 2 indicates which managed properties are used by both a Pages library and a list, and which from a Pages library only.</span></span>
  
    
    


<span data-ttu-id="1d0af-255">**Tabelle 2. Standardmäßige verwaltete Eigenschaften für Codeausschnitte zur Wiederverwendung von Katalogelementen**</span><span class="sxs-lookup"><span data-stu-id="1d0af-255">**Table 2. Default managed properties Catalog-Item Reuse Snippets**</span></span>


|<span data-ttu-id="1d0af-256">**Verwaltete Eigenschaft**</span><span class="sxs-lookup"><span data-stu-id="1d0af-256">**Managed property**</span></span>|<span data-ttu-id="1d0af-257">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="1d0af-257">**Description**</span></span>|<span data-ttu-id="1d0af-258">**Verwendet von**</span><span class="sxs-lookup"><span data-stu-id="1d0af-258">**Used by**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="1d0af-259">**AuthorOWSUSER**</span><span class="sxs-lookup"><span data-stu-id="1d0af-259">**AuthorOWSUSER**</span></span> <br/> |<span data-ttu-id="1d0af-260">Der Name des Benutzers, der die Seite erstellt hat.</span><span class="sxs-lookup"><span data-stu-id="1d0af-260">The name of the user who created the page.</span></span>  <br/> |<span data-ttu-id="1d0af-261">Nur Bibliothek für Seiten</span><span class="sxs-lookup"><span data-stu-id="1d0af-261">Pages library only</span></span>  <br/> |
|<span data-ttu-id="1d0af-262">**CreatedOWSDATE**</span><span class="sxs-lookup"><span data-stu-id="1d0af-262">**CreatedOWSDATE**</span></span> <br/> |<span data-ttu-id="1d0af-263">Das Datum, an dem die Seite oder das Listenelement erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="1d0af-263">The date the page or list item was created.</span></span>  <br/> |<span data-ttu-id="1d0af-264">Bibliothek für Seiten und Liste</span><span class="sxs-lookup"><span data-stu-id="1d0af-264">Pages library and list</span></span>  <br/> |
|<span data-ttu-id="1d0af-265">**EditorOWSUSER**</span><span class="sxs-lookup"><span data-stu-id="1d0af-265">**EditorOWSUSER**</span></span> <br/> |<span data-ttu-id="1d0af-266">Der Name des Benutzers, der die Seite oder das Listenelement zuletzt geändert hat.</span><span class="sxs-lookup"><span data-stu-id="1d0af-266">The name of the user who last changed the page or list item.</span></span>  <br/> |<span data-ttu-id="1d0af-267">Bibliothek für Seiten und Liste</span><span class="sxs-lookup"><span data-stu-id="1d0af-267">Pages library and list</span></span>  <br/> |
|<span data-ttu-id="1d0af-268">**ListItemID**</span><span class="sxs-lookup"><span data-stu-id="1d0af-268">**ListItemID**</span></span> <br/> |<span data-ttu-id="1d0af-269">Die ID der Seite oder des Listenelements.</span><span class="sxs-lookup"><span data-stu-id="1d0af-269">The ID for the page or list item.</span></span>  <br/> |<span data-ttu-id="1d0af-270">Bibliothek für Seiten und Liste</span><span class="sxs-lookup"><span data-stu-id="1d0af-270">Pages library and list</span></span>  <br/> |
|<span data-ttu-id="1d0af-271">**ModifiedOWSDATE**</span><span class="sxs-lookup"><span data-stu-id="1d0af-271">**ModifiedOWSDATE**</span></span> <br/> |<span data-ttu-id="1d0af-272">Das Datum, an dem die Seite oder das Listenelement zuletzt geändert wurde.</span><span class="sxs-lookup"><span data-stu-id="1d0af-272">The date the page or list item was last changed.</span></span>  <br/> |<span data-ttu-id="1d0af-273">Bibliothek für Seiten und Liste</span><span class="sxs-lookup"><span data-stu-id="1d0af-273">Pages library and list</span></span>  <br/> |
|<span data-ttu-id="1d0af-274">**PublishingContactOWSUSER**</span><span class="sxs-lookup"><span data-stu-id="1d0af-274">**PublishingContactOWSUSER**</span></span> <br/> |<span data-ttu-id="1d0af-p125">„Kontakt“ ist eine Websitespalte, die von der Veröffentlichungsfunktion erstellt wird. Sie wird für den Seiteninhaltstyp als Kontaktperson oder -organisation für die Website verwendet.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p125">Contact is a site column created by the Publishing feature. It is used on the Page Content Type as the person or group who is the contact person for the page.</span></span>  <br/> |<span data-ttu-id="1d0af-277">Nur Bibliothek für Seiten</span><span class="sxs-lookup"><span data-stu-id="1d0af-277">Pages library only</span></span>  <br/> |
|<span data-ttu-id="1d0af-278">**PublishingIsFurlPageOWSBOOL**</span><span class="sxs-lookup"><span data-stu-id="1d0af-278">**PublishingIsFurlPageOWSBOOL**</span></span> <br/> |<span data-ttu-id="1d0af-279">Ein boolescher Wert, der angibt, ob der Seite eine benutzerfreundliche URL zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="1d0af-279">A Boolean value that indicates whether the page is associated with a friendly URL.</span></span>  <br/> |<span data-ttu-id="1d0af-280">Nur Bibliothek für Seiten</span><span class="sxs-lookup"><span data-stu-id="1d0af-280">Pages library only</span></span>  <br/> |
|<span data-ttu-id="1d0af-281">**PublishingPageContentOWSHTML**</span><span class="sxs-lookup"><span data-stu-id="1d0af-281">**PublishingPageContentOWSHTML**</span></span> <br/> |<span data-ttu-id="1d0af-282">Der HTML-Inhalt der Seite.</span><span class="sxs-lookup"><span data-stu-id="1d0af-282">The HTML content of the page.</span></span>  <br/> |<span data-ttu-id="1d0af-283">Nur Bibliothek für Seiten</span><span class="sxs-lookup"><span data-stu-id="1d0af-283">Pages library only</span></span>  <br/> |
|<span data-ttu-id="1d0af-284">**PublishingPageLayoutOWSURLH**</span><span class="sxs-lookup"><span data-stu-id="1d0af-284">**PublishingPageLayoutOWSURLH**</span></span> <br/> |<span data-ttu-id="1d0af-285">Die URL zum Seitenlayout, das zum Erstellen der Seite verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="1d0af-285">The URL to the page layout that was used to create the page.</span></span>  <br/> |<span data-ttu-id="1d0af-286">Nur Bibliothek für Seiten</span><span class="sxs-lookup"><span data-stu-id="1d0af-286">Pages library only</span></span>  <br/> |
|<span data-ttu-id="1d0af-287">**Title**</span><span class="sxs-lookup"><span data-stu-id="1d0af-287">**Title**</span></span> <br/> |<span data-ttu-id="1d0af-288">Der Titel der Seite oder des Listenelements.</span><span class="sxs-lookup"><span data-stu-id="1d0af-288">The title of the page or list item.</span></span>  <br/> |<span data-ttu-id="1d0af-289">Bibliothek für Seiten und Liste</span><span class="sxs-lookup"><span data-stu-id="1d0af-289">Pages library and list</span></span>  <br/> |
   
<span data-ttu-id="1d0af-290">Die verwalteten Eigenschaften für benutzerdefinierte Spalten, die Sie der Bibliothek für Seiten oder der Liste hinzufügen, werden ebenfalls in Codeausschnitte zur Wiederverwendung von Katalogelementen eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-290">The managed properties for custom columns that you add to the Pages library or list are also included in Catalog-Item Reuse Snippets.</span></span> <span data-ttu-id="1d0af-291">Der Name der verwalteten Eigenschaft variiert je nach dem Typ der Website, die Sie beim Erstellen der Websitespalte verwenden.</span><span class="sxs-lookup"><span data-stu-id="1d0af-291">The managed property name will vary, based on the site column type that you use when you create the site column.</span></span> <span data-ttu-id="1d0af-292">Weitere Informationen finden Sie unter [Automatisch erstellte verwaltete Eigenschaften in SharePoint](http://technet.microsoft.com/de-DE/library/jj613136.aspx) und [Übersicht über das Suchschema in SharePoint](http://technet.microsoft.com/de-DE/library/jj219669.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d0af-292">For more information, see  [Automatically created managed properties in SharePoint](http://technet.microsoft.com/de-DE/library/jj613136.aspx), and  [Overview of the search schema in SharePoint](http://technet.microsoft.com/de-DE/library/jj219669.aspx).</span></span>
  
    
    

> <span data-ttu-id="1d0af-293">**Wichtig:** Die Websitespalte **Seitenbild** Websitespalte in einer Bibliothek für Seiten wird der verwalteten Eigenschaft **PublishingImage** zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="1d0af-293">**Important:** The **Page Image** site column in a Pages library is mapped to the **PublishingImage** managed property.</span></span> <span data-ttu-id="1d0af-294">Die verwaltete Eigenschaft **PublishingImage** wird aber nicht automatisch in das Kategorieelement-Seitenlayout eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-294">But, the **PublishingImage** managed property is not automatically included in the category-item page layout.</span></span> <span data-ttu-id="1d0af-295">Um das Bild in das Seitenlayout einzuschließen, müssen Sie einen Codeausschnitt zur Wiederverwendung von Katalogelementen für die verwaltete Eigenschaft **PublishingImage** hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-295">To include the image in your page layout, you must add a Catalog-Item Reuse Snippet for the **PublishingImage** managed property.</span></span> <span data-ttu-id="1d0af-296">Verwenden Sie den folgenden HTML-Code, um einen Codeausschnitte zur Wiederverwendung von Katalogelementen hinzuzufügen, um den Wert der verwalteten Eigenschaft **PublishingImage** im Seitenlayout anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="1d0af-296">Use the following HTML to add a Catalog-Item Reuse Snippet to display the value of the **PublishingImage** managed property in your page layout.</span></span> <span data-ttu-id="1d0af-297">Ersetzen Sie _UniqueID_ durch eine GUID, die für jede Instanz des Codeausschnitts eindeutig ist.</span><span class="sxs-lookup"><span data-stu-id="1d0af-297">Replace _UniqueID_ with a GUID that is unique to each instance of the snippet.</span></span>
  
    
    




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

<span data-ttu-id="1d0af-p128">Wenn Sie mit dem Entwurfs-Manager ein neues Katalogelement-Seitenlayout erstellen und einen Inhaltstyp anstellen eines Remotekatalogs auswählen, können Sie Codeausschnitte zur Wiederverwendung von Katalogelementen im Codeausschnittkatalog auswählen. Das folgende Codebeispiel zeigt das Markup der Codeausschnitte zur Wiederverwendung von Katalogelementen für die verwalteten Eigenschaften **Title**, **PublishingPageContentOWSHTML**, **CreatedOWSDATE** und **owstaxIdPageCategory**.</span><span class="sxs-lookup"><span data-stu-id="1d0af-p128">If you create a new catalog item page layout by using Design Manager, and you choose a content type instead of a remote catalog, you can add Catalog-Item Reuse Snippets to the page by using the Snippet Gallery. The following code shows the markup for the Catalog-Item Reuse Snippets for the **Title**, **PublishingPageContentOWSHTML**, **CreatedOWSDATE**, and **owstaxIdPageCategory** managed properties.</span></span>
  
    
    

> <span data-ttu-id="1d0af-300">**Hinweis:** Die GUIDS für **ID** und **__WebPartId** werden von SharePoint nach dem Zufallsprinzip generiert, wenn dem Seitenlayout Codeausschnitte hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="1d0af-300">**Note:** The GUIDs for **ID** and **__WebPartId** are randomly generated by SharePoint when the snippets are added to the page layout.</span></span>
  
    
    




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


## <a name="additional-resources"></a><span data-ttu-id="1d0af-301">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="1d0af-301">Additional resources</span></span>
<span data-ttu-id="1d0af-302"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="1d0af-302"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="1d0af-303">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d0af-303">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1d0af-304">Übersicht über den Entwurfs-Manager in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d0af-304">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1d0af-305">Übersicht über das SharePoint-Seitenmodell</span><span class="sxs-lookup"><span data-stu-id="1d0af-305">Overview of the SharePoint page model</span></span>](overview-of-the-sharepoint-page-model.md)
    
  
-  [<span data-ttu-id="1d0af-306">Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d0af-306">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1d0af-307">Anzeigevorlagen im SharePoint-Entwurfs-Manager</span><span class="sxs-lookup"><span data-stu-id="1d0af-307">SharePoint Design Manager display templates</span></span>](sharepoint-design-manager-display-templates.md)
    
  

