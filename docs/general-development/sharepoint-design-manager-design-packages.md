---
title: Designpakete des SharePoint-Entwurfs-Managers
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 85ad1993-4d75-4806-9097-b934865a899a
ms.openlocfilehash: 7fd5fa67e4e93d3f3110d53ece58fd1ad5f668e3
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-design-manager-design-packages"></a><span data-ttu-id="2d46d-102">Designpakete des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="2d46d-102">SharePoint Design Manager design packages</span></span>
<span data-ttu-id="2d46d-103">Informationen zum Erstellen und Exportieren des visuellen Designs einer SharePoint-Websitesammlung als Paket</span><span class="sxs-lookup"><span data-stu-id="2d46d-103">Learn how to build and export the visual design of a SharePoint site collection as a package.</span></span>
## <a name="overview-of-design-packages"></a><span data-ttu-id="2d46d-104">Übersicht über Designpakete</span><span class="sxs-lookup"><span data-stu-id="2d46d-104">Overview of Design Packages</span></span>
<span data-ttu-id="2d46d-105"><a name="int"> </a></span><span class="sxs-lookup"><span data-stu-id="2d46d-105"><a name="int"> </a></span></span>

<span data-ttu-id="2d46d-106">Mithilfe des Entwurfs-Managers in SharePoint können Webentwickler und Webdesigner visuelle Designs für SharePoint-Websitesammlungen erstellen und anschließend als Paket exportieren.</span><span class="sxs-lookup"><span data-stu-id="2d46d-106">In SharePoint, Design Manager can help web developers and designers build and export the visual design of a SharePoint site collection as a package.</span></span> <span data-ttu-id="2d46d-107">Ein solches Paket lässt sich unkompliziert an Kunden oder andere involvierte Gruppen übermitteln, die es in ihren Websitesammlungen installieren können.</span><span class="sxs-lookup"><span data-stu-id="2d46d-107">This package can easily be distributed to customers, or other designated groups, for installation on their site collections.</span></span> <span data-ttu-id="2d46d-108">Dieses neue Feature vereinfacht die Übermittlung von Designs und macht es Kunden einfacher, die Entwicklung visueller Designs für ihre Websites auszulagern.</span><span class="sxs-lookup"><span data-stu-id="2d46d-108">This new feature reduces the complexity of transporting designs, and makes it easier for customers to outsource the visual design of their sites.</span></span> <span data-ttu-id="2d46d-109">Möglich sind beispielsweise folgende Verwendungsszenarien:</span><span class="sxs-lookup"><span data-stu-id="2d46d-109">For example, some usage scenarios can include the following:</span></span>
  
    
    

- <span data-ttu-id="2d46d-p102">**Neues Design**: Ein Unternehmen mit eingeschränkten Fähigkeiten im Bereich Webdesign schließt möglicherweise einen Vertrag mit einer Agentur ab, die die aktuelle SharePoint-Website des Unternehmens aktualisiert und moderner gestaltet. Die Agentur kann die Website erstellen und die Inhalte problemlos packen, um sie in die SharePoint-Farm des Unternehmens zurück zu importieren.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p102">**New Design** —A company with limited web design capabilities might contract a vendor agency to refresh their current SharePoint site with a more modern interpretation. The agency can create the site and easily package the contents for importing back into the company SharePoint farm.</span></span>
    
  
- <span data-ttu-id="2d46d-p103">**Websiteübergreifende Veröffentlichung**: Die IT-Abteilung eines Unternehmens, das die websiteübergreifende Veröffentlichung in SharePoint nutzt, muss ggf. ein visuelles Design über mehrere Websitesammlungen hinweg freigeben. Das Unternehmen erstellt die Website intern und sucht nach einer einfachen Möglichkeit, das Design über mehrere SharePoint-Websites hinweg zu transportieren. Die Designpaketfunktion des Entwurfs-Managers bietet dem Unternehmen die Möglichkeit, die Daten mit geringerem Verwaltungsaufwand und reduzierter Komplexität zu exportieren und zu importieren.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p103">**Cross-Site Publishing** —An enterprise IT department using cross-site publishing in SharePoint might have to share a visual design across multiple site collections. They create the site in-house and want a simple way to transport the design across several SharePoint websites. The design package functionality through Device Manager enables them to export and import with reduced administrative support and complexity.</span></span>
    
  
<span data-ttu-id="2d46d-p104">Dieser Artikel kann Ihnen dabei helfen, zu verstehen, wie Designpakete in SharePoint erstellt und verwendet werden. Sie erhalten einen Überblick über die Paketerstellung und Anleitungen zum Workflow beim Exportieren und Importieren von Paketen. Außerdem werden erforderliche Berechtigungen für bestimmte Vorgänge sowie die Architektur von Designpaketen erörtert.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p104">This article can help you understand design packaging in SharePoint by providing an overview of package creation, and offers workflow guidance for package exporting and importing. It also discusses required permissions for specific operations, and design package architecture.</span></span>
  
    
    

## <a name="creating-a-design-package"></a><span data-ttu-id="2d46d-117">Erstellen von Designpaketen</span><span class="sxs-lookup"><span data-stu-id="2d46d-117">Creating a design package</span></span>
<span data-ttu-id="2d46d-118"><a name="package"> </a></span><span class="sxs-lookup"><span data-stu-id="2d46d-118"><a name="package"> </a></span></span>

<span data-ttu-id="2d46d-p105">Benutzer erstellen als SharePoint-Lösungspakete (WSP-Datei) bezeichnete Designpakete auf ihrer SharePoint-Website über den Entwurfs-Manager in **Websiteeinstellungen**. Der Schritt zum Erstellen des Pakets folgt auf andere Entwurfs-Manager-Schritte für das Branding und die Veröffentlichung einer SharePoint-Website. Hierzu zählen das Hochladen der Designdateien, das Erstellen einer Gestaltungsvorlage und das Bearbeiten von Seitenlayouts. Nachdem die Website veröffentlicht wurde, ist das Erstellen der WSP-Datei für den Export ein relativ einfacher Vorgang.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p105">A user creates a design package, called a SharePoint solution package (.wsp file) on their SharePoint site, through Design Manager in **Site Settings**. The step for creating the package follows other Design Manager steps for branding and publishing a SharePoint site, including uploading design files, creating a master page, and editing page layouts. After the site is published, it is a relatively simple process to create the .wsp file for export.</span></span>
  
    
    
<span data-ttu-id="2d46d-122">In Abbildung 1 wird die Option im Entwurfs-Manager gezeigt, mit der das Designpaket benannt und erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="2d46d-122">Figure 1 shows the option in Design Manager for naming and creating the design package.</span></span>
  
    
    

<span data-ttu-id="2d46d-123">**Abbildung 1: Exportieren eines Designpakets**</span><span class="sxs-lookup"><span data-stu-id="2d46d-123">**Figure 1. Exporting a design package**</span></span>

  
    
    

  
    
    
![Exportieren eines Entwurfspakets](../images/sp15Con_DesignPackageExp_Figure1.png)
  
    
    
<span data-ttu-id="2d46d-125">Alternativ können Sie ein Designpaket aus einer anderen SharePoint-Websitesammlung über den Entwurfs-Manager auf der Homepage importieren, oder indem Sie **Designpaket importieren** unter **Websiteeinstellungen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="2d46d-125">Alternatively, you can import a design package from another SharePoint site collection through Design Manager on the Welcome page, or by choosing **Import design package** in **Site Settings**.</span></span>
  
    
> [!NOTE]
> <span data-ttu-id="2d46d-126">Weitere Informationen zum Entwurfs-Manager und zum Veröffentlichungsvorgang finden Sie unter [Übersicht über den Entwurfs-Manager in SharePoint](overview-of-design-manager-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="2d46d-126">[Note:](overview-of-design-manager-in-sharepoint.md) For more information about Design Manager and the publishing process, see  Overview of Design Manager in SharePoint.</span></span> 
  
    
    

<span data-ttu-id="2d46d-p106">Es ist ein Kontrollkästchen vorhanden, über das die Suchkonfiguration in das Designpaket aufgenommen wird. Diese Option wählen Sie, wenn Sie eine Website entwerfen und bedingte Suchergebnisse erstellen oder die Suchumgebung steuern. Diese Konfiguration enthält Objekte wie Abfrageregeln, Ergebnisquellen, Ergebnistypen sowie jegliche Schema- und Bewertungsmodelle. Damit sichergestellt wird, dass der Import der Suchkonfiguration nicht fehlschlägt, dürfen bei Elementen der Suchkonfiguration keine doppelten Namen vorhanden sein. Wenn Sie beispielsweise in einer Websitesammlung über eine Abfrageregel namens **SampleQueryRule** verfügen und diese in eine andere Websitesammlung mit einer bestehenden Regeln namens **SampleQueryRule** importieren, schlägt der Import der Suchkonfiguration fehl. Um dies zu verhindern, können Sie die Abfrageregel in der Quelle oder dem Ziel umbenennen oder löschen. Ergebnisquellen sowie das Schema müssen ebenfalls eindeutige Namen aufweisen. Wenn Sie eine Suchkonfiguration in Ihr Designpaket aufnehmen möchten, müssen Sie die folgenden Features auf Websiteebene unter **Websitefeatures verwalten** aktivieren, bevor Sie das Designpaket exportieren:</span><span class="sxs-lookup"><span data-stu-id="2d46d-p106">There is a check box for including the search configuration in the design package. You would choose this option if you are designing a site and creating conditional search results, or controlling the search experience. This configuration contains assets like query rules, result sources, result types, and any schema and ranking models. To ensure that the import of the search configuration does not fail, there must not be duplicate names for any elements of the search configuration. For example, if you have a query rule in a site collection named **SampleQueryRule**, and you import it into another site collection with an existing rule named **SampleQueryRule**, importing the search configuration fails. To prevent this, you can rename or delete the query rule on the source or on the target. Result sources, and the schema, also have to be uniquely named. If you want to include a search configuration in your design package, you must activate the following features at the site level under **Manage Site Features** before you export the design package:</span></span>
  
    
    

- <span data-ttu-id="2d46d-135">Suchkonfigurationsdaten-Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="2d46d-135">Search Config Data Content Types</span></span>
    
  
- <span data-ttu-id="2d46d-136">Suchkonfigurationsdaten-Websitespalten</span><span class="sxs-lookup"><span data-stu-id="2d46d-136">Search Config Data Site Columns</span></span>
    
  
- <span data-ttu-id="2d46d-137">Suchkonfigurationslisten-Instanzfeature</span><span class="sxs-lookup"><span data-stu-id="2d46d-137">Search Config List Instance Feature</span></span>
    
  
- <span data-ttu-id="2d46d-138">Suchkonfigurationsvorlagen-Feature</span><span class="sxs-lookup"><span data-stu-id="2d46d-138">Search Config Template Feature</span></span>
    
  
<span data-ttu-id="2d46d-p107">Wenn Sie möchten, dass Ihr Design im Ziel des Imports veröffentlicht wird, sollten Sie alle Designobjekte veröffentlichen oder die Hauptversionsverwaltung in designbezogenen Bibliotheken in der Quelle des Exports deaktivieren. Der Entwurfs-Manager exportiert nur die neueste Version jedes Objekts aus der Quelle. Wenn Sie beispielsweise über die Version 1.1 einer Gestaltungsvorlage in der Quelle verfügen, wird diese als Entwurf in das Ziel kopiert. Version 1.0 wird jedoch nicht kopiert. Außerdem werden alle Dateien, die ausgecheckt sind, nicht exportiert.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p107">If you want your design to be published on the target of import, you should publish all design assets or disable major versioning in design-related libraries on the source of export. Design Manager exports only the most recent version of each asset from the source. For example, if you have version 1.1 of a master page on the source it will be copied to the target as a draft. But, version 1.0 is not copied. Also, files that are checked out are not exported.</span></span>
  
    
    

## <a name="exporting-and-importing-a-design-package"></a><span data-ttu-id="2d46d-144">Exportieren und Importieren von Designpaketen</span><span class="sxs-lookup"><span data-stu-id="2d46d-144">Exporting and importing a design package</span></span>
<span data-ttu-id="2d46d-145"><a name="work"> </a></span><span class="sxs-lookup"><span data-stu-id="2d46d-145"><a name="work"> </a></span></span>

<span data-ttu-id="2d46d-p108">Sie können auf verschiedene Weise an einen End-to-End-Paketworkflow herangehen, wobei der Ansatz größtenteils von Ihren Zielsetzungen und den verfügbaren Designressourcen abhängig ist. Möglicherweise entscheiden Sie sich dafür, die Arbeit an eine Agentur auszulagern, oder Sie arbeiten intern, wenn Sie über die geeigneten internen Ressourcen verfügen. In Tabelle 1 wird ein Beispielworkflow erläutert. Dies umfasst den Austausch von Daten für das Design zwischen einem Kunden und einer Agentur sowie den Export und Import des Designpakets. Außerdem werden die benötigten Berechtigungen für designbezogene Vorgänge sowie Verpackungsvorgänge erläutert.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p108">You can approach an end-to-end packaging workflow several ways, with much of the approach depending on your objectives and available design resources. You may decide to outsource to a vendor agency, or do the work in-house if you have internal resourcing. Table 1 provides a sample workflow and exchange between a client and a vendor agency over the design, exporting, and importing of the design package. It also provides the required permissions for design-related operations, and packaging operations.</span></span>
  
    
    

<span data-ttu-id="2d46d-150">**Tabelle 1: Beispielworkflow für ein Designpaket**</span><span class="sxs-lookup"><span data-stu-id="2d46d-150">**Table 1. Sample design package workflow**</span></span>


|<span data-ttu-id="2d46d-151">**Schritt**</span><span class="sxs-lookup"><span data-stu-id="2d46d-151">**Step**</span></span>|<span data-ttu-id="2d46d-152">**Aktion**</span><span class="sxs-lookup"><span data-stu-id="2d46d-152">**Action**</span></span>|<span data-ttu-id="2d46d-153">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="2d46d-153">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="2d46d-154">1</span><span class="sxs-lookup"><span data-stu-id="2d46d-154">1</span></span>  <br/> |<span data-ttu-id="2d46d-155">Ein Kunde beauftragt eine Agentur mit der Erstellung eines visuellen Designs.</span><span class="sxs-lookup"><span data-stu-id="2d46d-155">Customer contracts vendor agency to create visual design.</span></span>  <br/> | <span data-ttu-id="2d46d-156">Der Designer erstellt die Website basierend auf den Anforderungen des Unternehmens.</span><span class="sxs-lookup"><span data-stu-id="2d46d-156">The vendor designer creates site, based on company requirements.</span></span> <br/> <span data-ttu-id="2d46d-157">**Hinweis:** Der Designer benötigt die Berechtigungsstufe **Designer**, um mit dem Entwurfs-Manager arbeiten und Pakete exportieren zu können.</span><span class="sxs-lookup"><span data-stu-id="2d46d-157">**Note:**  The vendor designer must have the **Designers** permission level to use Design Manager and create and export packages.</span></span> <span data-ttu-id="2d46d-158">Genauer gesagt benötigt er die Berechtigung **Design** zum Aufrufen, Hinzufügen, Aktualisieren, Löschen, Genehmigen und Anpassen von visuellen Designs.</span><span class="sxs-lookup"><span data-stu-id="2d46d-158">More specifically, the **Design** permission that allows viewing, adding, updating, deleting, approving, and customizing visual designs.</span></span>          |
|<span data-ttu-id="2d46d-159">2</span><span class="sxs-lookup"><span data-stu-id="2d46d-159">2</span></span>  <br/> |<span data-ttu-id="2d46d-160">Der Designer exportiert das visuelle Design in ein Designpaket.</span><span class="sxs-lookup"><span data-stu-id="2d46d-160">Vendor designer exports visual design into a design package.</span></span>  <br/> | <span data-ttu-id="2d46d-161">Der Designer exportiert das SharePoint-Lösungspaket (WSP-Datei), nachdem er die übrigen erforderlichen Branding- und Veröffentlichungsschritte abgeschlossen hat.</span><span class="sxs-lookup"><span data-stu-id="2d46d-161">The vendor designer exports the SharePoint solution package (.wsp file) after completing the other required branding and publishing steps.</span></span> <br/>  <span data-ttu-id="2d46d-162">Das Designpaket wird über einen sicheren Kanal an den Kunden geliefert.</span><span class="sxs-lookup"><span data-stu-id="2d46d-162">The design package is delivered to the customer via a secure channel.</span></span> <br/> |
|<span data-ttu-id="2d46d-163">3</span><span class="sxs-lookup"><span data-stu-id="2d46d-163">3</span></span>  <br/> |<span data-ttu-id="2d46d-164">Der Kunde importiert das visuelle Design in die angegebene SharePoint-Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="2d46d-164">Customer imports visual design into their specified SharePoint site collection.</span></span>  <br/> | <span data-ttu-id="2d46d-165">Der Kunde erhält das Designpaket über einen sicheren Kanal.</span><span class="sxs-lookup"><span data-stu-id="2d46d-165">The customer receives the design package via a secure channel.</span></span> <br/>  <span data-ttu-id="2d46d-166">Über die Homepage im Entwurfs-Manager oder durch Auswahl von **Designpaket importieren** unter **Websiteeinstellungen** importiert der Kunde die WSP-Datei und wendet das Designpaket auf die angegebene Websitesammlung an.</span><span class="sxs-lookup"><span data-stu-id="2d46d-166">Through the Welcome page in Design Manager or by choosing **Import design package** in **Site Settings**, the customer imports the .wsp file and applies the design package to the specified site collection.</span></span>  <br/> <span data-ttu-id="2d46d-167">**Hinweis:** Der Kunde benötigt die Berechtigungsstufe **Designer**, um mit dem Entwurfs-Manager arbeiten und Designpakete importieren zu können.</span><span class="sxs-lookup"><span data-stu-id="2d46d-167">**Note:**  The customer must have the **Designers** permission level to use Design Manager and import design packages.</span></span>          |
   

## <a name="understanding-design-package-contents"></a><span data-ttu-id="2d46d-168">Übersicht über den Inhalt von Designpaketen</span><span class="sxs-lookup"><span data-stu-id="2d46d-168">Understanding design package contents</span></span>
<span data-ttu-id="2d46d-169"><a name="packcont"> </a></span><span class="sxs-lookup"><span data-stu-id="2d46d-169"><a name="packcont"> </a></span></span>

<span data-ttu-id="2d46d-p110">Das Designpaket (WSP-Datei) enthält verschiedene Dateien, wenn es über den Entwurfs-Manager erstellt wird. Bei dem Verfahren werden Dateien aus verschiedenen Listen und Bibliotheken exportiert und bilden auf diese Weise das Gesamtpaket. Beim Import in eine Websitesammlung werden diese Dateien basierend auf dem Dateityp an verschiedene Speicherorte verteilt. Tabelle 2 enthält nähere Informationen zum Speicherort der Dateien und dem Typ der während des Zusammenstellungsvorgangs exportierten Dateien.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p110">Several files are included in the design package .wsp file when it is created through Design Manager. The process exports files from various lists and libraries to form the overall package. While importing to a site collection, these files are distributed to different locations based on file type. Table 2 details the location and type of files exported during the assembly process.</span></span>
  
    
    

<span data-ttu-id="2d46d-174">**Tabelle 2: Übersicht über den Inhalt eines Designpakets und Speicherorte für exportierte Dateien**</span><span class="sxs-lookup"><span data-stu-id="2d46d-174">**Table 2. Summary of design package contents and file exportation locations**</span></span>


|<span data-ttu-id="2d46d-175">**Exportspeicherort**</span><span class="sxs-lookup"><span data-stu-id="2d46d-175">**Export Location**</span></span>|<span data-ttu-id="2d46d-176">**Exportierte Objekte**</span><span class="sxs-lookup"><span data-stu-id="2d46d-176">**Exported Assets**</span></span>|
|:-----|:-----|
|<span data-ttu-id="2d46d-177">Dokumentbibliotheken</span><span class="sxs-lookup"><span data-stu-id="2d46d-177">Document libraries</span></span>  <br/> | <span data-ttu-id="2d46d-178">Gestaltungsvorlagenkatalog</span><span class="sxs-lookup"><span data-stu-id="2d46d-178">Master Pages Gallery</span></span> <br/>  <span data-ttu-id="2d46d-179">Designkatalog</span><span class="sxs-lookup"><span data-stu-id="2d46d-179">Themes Gallery</span></span> <br/>  <span data-ttu-id="2d46d-180">Formatbibliothek</span><span class="sxs-lookup"><span data-stu-id="2d46d-180">Style Library</span></span> <br/>  <span data-ttu-id="2d46d-181">Websiteobjektbibliothek</span><span class="sxs-lookup"><span data-stu-id="2d46d-181">Site Assets Library</span></span> <br/> |
|<span data-ttu-id="2d46d-182">Inhaltstypen, Felder</span><span class="sxs-lookup"><span data-stu-id="2d46d-182">Content types, fields</span></span>  <br/> | <span data-ttu-id="2d46d-183">Inhaltstypen, die vom Inhaltstyp "Seite" erben</span><span class="sxs-lookup"><span data-stu-id="2d46d-183">Content types that inherit from the Page content type</span></span> <br/> |
|<span data-ttu-id="2d46d-184">Listen</span><span class="sxs-lookup"><span data-stu-id="2d46d-184">Lists</span></span>  <br/> | <span data-ttu-id="2d46d-185">Design Gallery</span><span class="sxs-lookup"><span data-stu-id="2d46d-185">Design Gallery</span></span> <br/>  <span data-ttu-id="2d46d-186">Durchkomponierte Looks</span><span class="sxs-lookup"><span data-stu-id="2d46d-186">Composed looks</span></span> <br/>  <span data-ttu-id="2d46d-187">Gerätekanäle</span><span class="sxs-lookup"><span data-stu-id="2d46d-187">Device channels</span></span> <br/> |
   
> [!NOTE]
> <span data-ttu-id="2d46d-188">In SharePoint werden ausschließlich angepasste Dateien in Designpakete aufgenommen.</span><span class="sxs-lookup"><span data-stu-id="2d46d-188">Note: In SharePoint, only customized files are included in design packages.</span></span> <span data-ttu-id="2d46d-189">Die meisten standardmäßigen, nicht angepassten Systemdateien werden vom Packprozess nicht exportiert.</span><span class="sxs-lookup"><span data-stu-id="2d46d-189">The packaging process will not export most of the default non-customized system files.</span></span> 
  
    
    

<span data-ttu-id="2d46d-p112">In SharePoint können Sie ein importiertes Designpaket nicht deinstallieren, und Sie sollten niemals versuchen, ein Designpaket über den Lösungskatalog zu deaktivieren. Falls Sie dies versuchen, werden die Inhaltstypen des Seitenlayouts entfernt, und Benutzer können möglicherweise keine Unterwebsites mehr erstellen. Um diesen Zustand zu beheben, sollten Sie die folgenden Schritte durchführen, bei denen Folgendes gilt: Website A ist die ursprüngliche Websitesammlung, Website B ist die Websitesammlung mit dem deaktivierten Designpaket (ungültiger Zustand), und Website C ist eine von Ihnen erstellte neue leere Website.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p112">In SharePoint you cannot uninstall an imported design package, and you should never attempt to deactivate a design package through the solution gallery. If you do, page layout content types are removed and users may not be able to create subsites. To recover from this state, you should perform the following steps where site A= the original site collection, site B = the site collection with the deactivated design package (bad state), and site C = a new, blank site collection that you have created:</span></span>
  
    
    

1. <span data-ttu-id="2d46d-193">Exportieren Sie ein Designpaket von Website A</span><span class="sxs-lookup"><span data-stu-id="2d46d-193">Export a design package from site A</span></span>
    
  
2. <span data-ttu-id="2d46d-194">Importieren Sie das Designpaket in Website C</span><span class="sxs-lookup"><span data-stu-id="2d46d-194">Import the design package to site C</span></span>
    
  
3. <span data-ttu-id="2d46d-195">Exportieren Sie ein Designpaket von Website B</span><span class="sxs-lookup"><span data-stu-id="2d46d-195">Export a design package from site B</span></span>
    
  
4. <span data-ttu-id="2d46d-196">Importieren Sie das Designpaket in Website C</span><span class="sxs-lookup"><span data-stu-id="2d46d-196">Import the design package to site C</span></span>
    
  
5. <span data-ttu-id="2d46d-197">Exportieren Sie das Designpaket von Website C</span><span class="sxs-lookup"><span data-stu-id="2d46d-197">Export the design package from site C</span></span>
    
  
6. <span data-ttu-id="2d46d-198">Importieren Sie das Designpaket in Website B</span><span class="sxs-lookup"><span data-stu-id="2d46d-198">Import the design package to site B</span></span>
    
  
<span data-ttu-id="2d46d-p113">Alle erstellen Gerätekanäle und ihre Konfigurationen werden ebenfalls importiert, wenn das Designpaket entladen wird. Sie müssen jedoch Gestaltungsvorlagen angegebenen Gerätekanälen neu zuordnen, da diese Zuordnungen nicht konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p113">Any created device channels, and their configurations, are also imported when the design package is unloaded. But, you have to re-associate master pages to specified device channels because these mappings will not be configured.</span></span>
  
    
    
<span data-ttu-id="2d46d-p114">Beim Importieren eines Designpakets wird keine alternative CSS-URL festgelegt, selbst wenn eine solche in der Quelle des Exports konfiguriert war. CSS-Klassen sollten nicht in einer externen Datei im Gestaltungsvorlagenkatalog und auch nicht in der Gestaltungsvorlagendatei selbst gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="2d46d-p114">When importing a design package, an alternate CSS URL is not set, even if one was configured on the source of export. CSS classes should be stored in an external file in the Master Page Gallery and not in the master page file itself.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="2d46d-203">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2d46d-203">See also</span></span>
<span data-ttu-id="2d46d-204"><a name="addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2d46d-204"><a name="addresources"> </a></span></span>


-  [<span data-ttu-id="2d46d-205">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2d46d-205">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2d46d-206">Übersicht über den Entwurfs-Manager in SharePoint</span><span class="sxs-lookup"><span data-stu-id="2d46d-206">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2d46d-207">Neuerung bei SharePoint-Websiteentwicklung</span><span class="sxs-lookup"><span data-stu-id="2d46d-207">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development.md)
    
  
