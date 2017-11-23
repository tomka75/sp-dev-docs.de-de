---
title: SharePoint-Raster und reaktionsschnelles Design
ms.date: 9/25/2017
ms.openlocfilehash: 1025e1863d03bad9056d74c87307a7a1e4c8f103
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-grid-and-responsive-design"></a><span data-ttu-id="a33b1-102">SharePoint-Raster und reaktionsschnelles Design</span><span class="sxs-lookup"><span data-stu-id="a33b1-102">SharePoint grid and responsive design</span></span>
 
<span data-ttu-id="a33b1-103">Reaktionsschnelle Umgebungen werden nahtlos geräteübergreifend skaliert, damit Sie Ihre Inhalte auf einer Vielzahl an verschiedenen Bildschirmgrößen besser anzeigen können.</span><span class="sxs-lookup"><span data-stu-id="a33b1-103">Responsive experiences seamlessly scale across devices, to better display your content on a range of different screen sizes.</span></span> <span data-ttu-id="a33b1-104">Das reaktionsschnelle Design macht auch das Erstellen mehrerer Versionen Ihrer Websiteseiten überflüssig, um verschiedene Geräte zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-104">Responsive design also eliminates the need to build multiple versions of your site pages to support different devices.</span></span>  

<span data-ttu-id="a33b1-105">Der Designleitfaden für reaktionsschnelle Seiten in der SharePoint-Erstellungsumgebung beinhaltet ein reaktionsschnelles Rastersystem, das auf [Office UI Fabric](https://dev.office.com/fabric) basiert.</span><span class="sxs-lookup"><span data-stu-id="a33b1-105">The design guidance for responsive pages in the SharePoint authoring environment incorporates a responsive grid system that is based on [Office UI Fabric](https://dev.office.com/fabric).</span></span> <span data-ttu-id="a33b1-106">In diesem Artikel werden das zugrunde liegende Seitenrastersystem und die Haltepunkte oder die wichtigsten Bildschirmgrößen beschrieben, bei denen sich das Layout der Seiten ändert.</span><span class="sxs-lookup"><span data-stu-id="a33b1-106">This article describes the underlying page grid system and the breakpoints, or key screen sizes where the layout of the pages will change.</span></span> 


![SharePoint-Seite auf mehreren Geräten](../images/design-grid-responsive-overview.png)



## <a name="page-type-grids"></a><span data-ttu-id="a33b1-108">Seitentypraster</span><span class="sxs-lookup"><span data-stu-id="a33b1-108">Page type grids</span></span> 

<span data-ttu-id="a33b1-109">Jeder Seitentyp in der SharePoint-Erstellungsumgebung kann eigene Regeln für das Anwenden des reaktionsschnellen Fabric-Rasters haben.</span><span class="sxs-lookup"><span data-stu-id="a33b1-109">Each page type in the SharePoint authoring experience can have its own rules for how it applies the Fabric responsive grid.</span></span> <span data-ttu-id="a33b1-110">Dadurch wird sichergestellt, dass jede Seite gut aussieht, unabhängig davon, für welches Gerät sie entworfen ist, und dass die Umgebung für dieses Gerät optimiert ist.</span><span class="sxs-lookup"><span data-stu-id="a33b1-110">This is to ensure that each page looks great, regardless of what device it's designed for, and that the experience is optimized for that environment.</span></span> <span data-ttu-id="a33b1-111">Das grundlegende Raster in der SharePoint-Desktopumgebung ist eine Struktur mit 12 Spalten.</span><span class="sxs-lookup"><span data-stu-id="a33b1-111">The basic grid in the SharePoint desktop experiences is a 12 column structure.</span></span> <span data-ttu-id="a33b1-112">Die Anzahl der Spalten und die Bundstegbreite werden basierend auf der Breite des Bildschirms angepasst.</span><span class="sxs-lookup"><span data-stu-id="a33b1-112">The number of columns and gutter width will adjust based on the screen width.</span></span> 

<span data-ttu-id="a33b1-113">Die folgenden Abschnitte zeigen die grundlegende Rasterstruktur für verschiedene Arten von SharePoint-Seiten, damit Sie besser verstehen können, wie das Raster zur Unterstützung der Umgebung und Geräteanforderungen angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="a33b1-113">The following sections show the basic grid structure applied across different types of SharePoint pages, to help you better understand how the grid adjusts to support the experience and device needs.</span></span>


![Raster mit 12 Spalten – Diagramm](../images/design-grid_diagram.png)



### <a name="team-sites"></a><span data-ttu-id="a33b1-115">Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="a33b1-115">Team sites</span></span>

<span data-ttu-id="a33b1-116">Der Inhaltsbereich für eine Teamwebsite ist auf der linken Seite gesperrt.</span><span class="sxs-lookup"><span data-stu-id="a33b1-116">The content area for a team site is locked to the left.</span></span> <span data-ttu-id="a33b1-117">Teamwebsites weisen einen linken Navigationsbereich auf. Daher respektieren Webparts im Raster und das Reflow-Verhalten den Bereich für die Navigation.</span><span class="sxs-lookup"><span data-stu-id="a33b1-117">Team sites have a left navigation, therefore the space web parts occupy on the gird and the reflow behavior respects the space given to the navigation.</span></span> <span data-ttu-id="a33b1-118">Die maximale Breite des Inhaltsbereichs einer Teamwebsite beträgt 1204px und die minimale Größe 320px für Mobilgeräte.</span><span class="sxs-lookup"><span data-stu-id="a33b1-118">The max width of the content area of a Team site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Teamwebsite](../images/design-grid-team-site.png)

<span data-ttu-id="a33b1-120">Die folgenden Beispiele zeigen, wie das Raster zwischen den Haupthaltepunkten auf einer Teamwebsite angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="a33b1-120">The following examples show how the grid adjusts between key breakpoints on a team site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="a33b1-121">Klein 320 x 568</span><span class="sxs-lookup"><span data-stu-id="a33b1-121">Small 320 x 568</span></span>
<span data-ttu-id="a33b1-122">Die kleine Größe umfasst einen einzelnen Spaltenbereich in der Mitte, mit Rändern von 20px links und rechts.</span><span class="sxs-lookup"><span data-stu-id="a33b1-122">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Teamwebsite (kleines Raster)](../images/design-grid-Team-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a><span data-ttu-id="a33b1-124">Mittel 480 x 854</span><span class="sxs-lookup"><span data-stu-id="a33b1-124">Medium 480 x 854</span></span>
<span data-ttu-id="a33b1-125">Die mittlere Größe umfasst 12 Spalten mit 16px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-125">The medium size has 12 columns, with 16px gutters.</span></span>

![Teamwebsite (mittleres Raster)](../images/design-grid-Team-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a><span data-ttu-id="a33b1-127">Groß 640 x 1024</span><span class="sxs-lookup"><span data-stu-id="a33b1-127">Large 640 x 1024</span></span>
<span data-ttu-id="a33b1-128">Die große Größe umfasst 12 Spalten mit  24px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-128">The large size has 12 columns, with 24px gutters.</span></span>

![Teamwebsite (großes Raster)](../images/design-grid-Team-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a><span data-ttu-id="a33b1-130">XL 1024 x 768</span><span class="sxs-lookup"><span data-stu-id="a33b1-130">XL 1024 x 768</span></span>
<span data-ttu-id="a33b1-131">Die XL-Größe umfasst 12 Spalten mit 24px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-131">The XL size has a twelve columns, with 24px gutters.</span></span>

![Teamwebsite (XL-Raster)](../images/design-grid-Team-site-XL-Canvas-24px-gutters.png)

#### <a name="xxl-1366-x-768"></a><span data-ttu-id="a33b1-133">XXL 1366 x 768</span><span class="sxs-lookup"><span data-stu-id="a33b1-133">XXL 1366 x 768</span></span>
<span data-ttu-id="a33b1-134">Die XXL-Größe umfasst 12 Spalten mit 32px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-134">The XXL size has a twelve columns, with 32px gutters.</span></span>

![Teamwebsite (XXL-Raster)](../images/design-grid-Team-site–XXL-Canvas-32px-gutters.png)

#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="a33b1-136">XXXL 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="a33b1-136">XXXL 1920 x 1080</span></span>
<span data-ttu-id="a33b1-137">Die XXXL-Größe umfasst 12 Spalten mit 32px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-137">The XXXL size has a twelve columns, with 32px gutters.</span></span>

![Teamwebsite (XXXL-Raster)](../images/design-grid-Team-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="team-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="a33b1-139">Mehrsprachige Seiten und Webparts auf Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="a33b1-139">Team site multicolumn pages and web parts</span></span>
<span data-ttu-id="a33b1-140">Webparts werden je nach Seitenlayout horizontal skaliert.</span><span class="sxs-lookup"><span data-stu-id="a33b1-140">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="a33b1-141">Das folgende Beispiel zeigt, wie die Größe eines Webparts an den linken Navigationsbereich angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="a33b1-141">The following example shows how the size of a web part adjusts to accommodate the left navigation.</span></span>

![Mehrsprachige Teamwebsiteseite mit Webparts](../images/design-grid-Team-site-web-parts.png)


### <a name="communication-sites"></a><span data-ttu-id="a33b1-143">Kommunikationswebsites</span><span class="sxs-lookup"><span data-stu-id="a33b1-143">Communication sites</span></span>

<span data-ttu-id="a33b1-144">Kommunikationswebsites haben eine obere Navigationsleiste und einen Inhaltsbereich in der Mitte.</span><span class="sxs-lookup"><span data-stu-id="a33b1-144">Communication sites have a top navigation and a centered content area.</span></span> <span data-ttu-id="a33b1-145">Die maximale Breite des Inhaltsbereichs einer Kommunikationswebsite beträgt 1204px und die minimale Größe 320px für Mobilgeräte.</span><span class="sxs-lookup"><span data-stu-id="a33b1-145">The maximum width of the content area of a communication site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Kommunikationswebsite](../images/design-grid-communication_site.png)

<span data-ttu-id="a33b1-147">Die folgenden Beispiele zeigen, wie das Raster zwischen den Haupthaltepunkten auf einer Kommunikationswebsite angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="a33b1-147">The following examples show how the grid adjusts between key breakpoints on a communication site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="a33b1-148">Klein 320 x 568</span><span class="sxs-lookup"><span data-stu-id="a33b1-148">Small 320 x 568</span></span>
<span data-ttu-id="a33b1-149">Die kleine Größe umfasst einen einzelnen Spaltenbereich in der Mitte, mit Rändern von 20px links und rechts.</span><span class="sxs-lookup"><span data-stu-id="a33b1-149">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Kommunikationswebsite (kleines Raster)](../images/design-grid-Communication-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a><span data-ttu-id="a33b1-151">Mittel 480 x 854</span><span class="sxs-lookup"><span data-stu-id="a33b1-151">Medium 480 x 854</span></span>
<span data-ttu-id="a33b1-152">Die mittlere Größe umfasst 12 Spalten mit 16px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-152">The medium size has 12 columns, with 16px gutters.</span></span>

![Kommunikationswebsite (mittleres Raster)](../images/design-grid-Communication-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a><span data-ttu-id="a33b1-154">Groß 640 x 1024</span><span class="sxs-lookup"><span data-stu-id="a33b1-154">Large 640 x 1024</span></span>
<span data-ttu-id="a33b1-155">Die große Größe umfasst 12 Spalten mit  24px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-155">The large size has 12 columns, with 24px gutters.</span></span>

![Kommunikationswebsite (großes Raster)](../images/design-grid-Communication-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a><span data-ttu-id="a33b1-157">XL 1024 x 768</span><span class="sxs-lookup"><span data-stu-id="a33b1-157">XL 1024 x 768</span></span>
<span data-ttu-id="a33b1-158">Die XL-Größe umfasst 12 Spalten mit 24px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-158">The XL size has a twelve columns, with 24px gutters.</span></span>

![Kommunikationswebsite (XL-Raster)](../images/design-grid-Communication-site-XL-Canvas-24px-gutters.png)


#### <a name="xxl-1366-x-768"></a><span data-ttu-id="a33b1-160">XXL 1366 x 768</span><span class="sxs-lookup"><span data-stu-id="a33b1-160">XXL 1366 x 768</span></span>
<span data-ttu-id="a33b1-161">Die XXL-Größe umfasst 12 Spalten mit 32px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-161">The XXL size has a twelve columns, with 32px gutters.</span></span>

![Kommunikationswebsite (XXL-Raster)](../images/design-grid-Communication-site-XXL-Canvas-32px-gutters-maxwidth-1204.png)


#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="a33b1-163">XXXL 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="a33b1-163">XXXL 1920 x 1080</span></span>
<span data-ttu-id="a33b1-164">Die XXXL-Größe umfasst 12 Spalten mit 32px-Bundstegen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-164">The XXXL size has a twelve columns, with 32px gutters.</span></span>

![Kommunikationswebsite (XXXL-Raster)](../images/design-grid-Communication-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="communication-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="a33b1-166">Mehrsprachige Seiten und Webparts auf Kommunikationswebsite</span><span class="sxs-lookup"><span data-stu-id="a33b1-166">Communication site multicolumn pages and web parts</span></span>
<span data-ttu-id="a33b1-167">Webparts werden je nach Seitenlayout horizontal skaliert.</span><span class="sxs-lookup"><span data-stu-id="a33b1-167">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="a33b1-168">Dieses Beispiel zeigt eine Kommunikationswebsite und Webparts für Layouts mit einer, zwei oder drei Spalten.</span><span class="sxs-lookup"><span data-stu-id="a33b1-168">This example shows a communcation site and web parts for single to three column layouts.</span></span>

![Kommunikationswebsite mit mehreren Spalten und Webparts](../images/design-grid-Communciation-site-web-parts.png)



## <a name="breakpoints"></a><span data-ttu-id="a33b1-170">Haltepunkte</span><span class="sxs-lookup"><span data-stu-id="a33b1-170">Breakpoints</span></span> 

<span data-ttu-id="a33b1-171">Um eine nahtlose Erfahrung zwischen Bildschirmgrößen sicherzustellen, sollte die SharePoint-Benutzeroberfläche Layouts für die folgenden Haltepunktbreiten anpassen:</span><span class="sxs-lookup"><span data-stu-id="a33b1-171">To create a smooth flowing experience between screen sizes, the SharePoint UI should adapt layouts for the following breakpoint widths:</span></span> 

- <span data-ttu-id="a33b1-172">320</span><span class="sxs-lookup"><span data-stu-id="a33b1-172">320</span></span>
- <span data-ttu-id="a33b1-173">1024</span><span class="sxs-lookup"><span data-stu-id="a33b1-173">1024
(&H400)</span></span>
- <span data-ttu-id="a33b1-174">1366</span><span class="sxs-lookup"><span data-stu-id="a33b1-174">1366</span></span>
- <span data-ttu-id="a33b1-175">1920</span><span class="sxs-lookup"><span data-stu-id="a33b1-175">1920</span></span>
 
<span data-ttu-id="a33b1-176">Innerhalb dieser Haltepunkte sollten Sie berücksichtigen, wie Ihre Inhalte verschoben werden, wenn die Viewport-Größe für den nächsten Haltepunkt optimiert wird.</span><span class="sxs-lookup"><span data-stu-id="a33b1-176">Within these breakpoints, you should take into consideration how your content will shift when the viewport size becomes optimized for the nearest breakpoint.</span></span> <span data-ttu-id="a33b1-177">Beachten Sie, dass dieses Diagramm nur zur Veranschaulichung dient und die Pixel nicht präzise zeigt.</span><span class="sxs-lookup"><span data-stu-id="a33b1-177">Note that this diagram is for illustration only and is not pixel accurate.</span></span>


![SharePoint-Diagramm mit Haltepunkten](../images/design-grid-breakpoints.png)


<span data-ttu-id="a33b1-179">Das reaktionsschnelle Raster für Teamwebsites und Kommunikationswebsites wird beim Wechsel von großen Haltepunkten zu mobilen Haltepunkten angepasst.</span><span class="sxs-lookup"><span data-stu-id="a33b1-179">The responsive grid for both team sites and communication sites adjusts when going from large breakpoints to mobile breakpoints.</span></span> <span data-ttu-id="a33b1-180">Hierdurch wird die Website für das Gerät und die Bildschirmgröße optimiert.</span><span class="sxs-lookup"><span data-stu-id="a33b1-180">This optimizes the site for the device and screen size.</span></span> <span data-ttu-id="a33b1-181">Die folgende Tabelle beschreibt die Rastergrößen an verschiedenen Haltepunkten basierend auf gängigen Gerätegrößen.</span><span class="sxs-lookup"><span data-stu-id="a33b1-181">The following table describes the grid sizes at various breakpoints based on popular device sizes.</span></span>



| <span data-ttu-id="a33b1-182">Fensterbreite</span><span class="sxs-lookup"><span data-stu-id="a33b1-182">Window width</span></span> | <span data-ttu-id="a33b1-183">Gerät</span><span class="sxs-lookup"><span data-stu-id="a33b1-183">Device</span></span>                  | <span data-ttu-id="a33b1-184">Haltepunkt</span><span class="sxs-lookup"><span data-stu-id="a33b1-184">Breakpoint</span></span> | <span data-ttu-id="a33b1-185">Spalten</span><span class="sxs-lookup"><span data-stu-id="a33b1-185">Columns</span></span> | <span data-ttu-id="a33b1-186">Bundsteg</span><span class="sxs-lookup"><span data-stu-id="a33b1-186">Gutter</span></span> | <span data-ttu-id="a33b1-187">Maximale Anzahl von Spalten pro Bereich</span><span class="sxs-lookup"><span data-stu-id="a33b1-187">Max columns per section</span></span> |
|--------------|-------------------------|------------|---------|--------|-------------------------|
| <span data-ttu-id="a33b1-188">320</span><span class="sxs-lookup"><span data-stu-id="a33b1-188">320</span></span>          | <span data-ttu-id="a33b1-189">iPhone 5/SE, 320 x 568</span><span class="sxs-lookup"><span data-stu-id="a33b1-189">iPhone 5/SE,320x568</span></span>     | <span data-ttu-id="a33b1-190">Klein</span><span class="sxs-lookup"><span data-stu-id="a33b1-190">Small</span></span>      | <span data-ttu-id="a33b1-191">1</span><span class="sxs-lookup"><span data-stu-id="a33b1-191">1</span></span>       | <span data-ttu-id="a33b1-192">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="a33b1-192">N/A</span></span>    | <span data-ttu-id="a33b1-193">1</span><span class="sxs-lookup"><span data-stu-id="a33b1-193">1</span></span>                       |
| <span data-ttu-id="a33b1-194">480</span><span class="sxs-lookup"><span data-stu-id="a33b1-194">480</span></span>          | <span data-ttu-id="a33b1-195">6-Zoll-Gerät</span><span class="sxs-lookup"><span data-stu-id="a33b1-195">6" device</span></span>               | <span data-ttu-id="a33b1-196">Mittel</span><span class="sxs-lookup"><span data-stu-id="a33b1-196">Medium</span></span>     | <span data-ttu-id="a33b1-197">1</span><span class="sxs-lookup"><span data-stu-id="a33b1-197">1</span></span>       | <span data-ttu-id="a33b1-198">Nicht zutreffend</span><span class="sxs-lookup"><span data-stu-id="a33b1-198">N/A</span></span>    | <span data-ttu-id="a33b1-199">1</span><span class="sxs-lookup"><span data-stu-id="a33b1-199">1</span></span>                       |
| <span data-ttu-id="a33b1-200">640</span><span class="sxs-lookup"><span data-stu-id="a33b1-200">640</span></span>          | <span data-ttu-id="a33b1-201">8-Zoll-Gerät</span><span class="sxs-lookup"><span data-stu-id="a33b1-201">8" device</span></span>               | <span data-ttu-id="a33b1-202">Groß</span><span class="sxs-lookup"><span data-stu-id="a33b1-202">Large</span></span>      | <span data-ttu-id="a33b1-203">12</span><span class="sxs-lookup"><span data-stu-id="a33b1-203">1.2</span></span>      | <span data-ttu-id="a33b1-204">16</span><span class="sxs-lookup"><span data-stu-id="a33b1-204">16**</span></span>     | <span data-ttu-id="a33b1-205">2</span><span class="sxs-lookup"><span data-stu-id="a33b1-205">2</span></span>                       |
| <span data-ttu-id="a33b1-206">768</span><span class="sxs-lookup"><span data-stu-id="a33b1-206">768</span></span>          | <span data-ttu-id="a33b1-207">iPad Hochformat 768x1024</span><span class="sxs-lookup"><span data-stu-id="a33b1-207">iPad portrait 768x1024</span></span>  | <span data-ttu-id="a33b1-208">Groß</span><span class="sxs-lookup"><span data-stu-id="a33b1-208">Large</span></span>      | <span data-ttu-id="a33b1-209">12</span><span class="sxs-lookup"><span data-stu-id="a33b1-209">1.2</span></span>      | <span data-ttu-id="a33b1-210">24</span><span class="sxs-lookup"><span data-stu-id="a33b1-210">2.4</span></span>     | <span data-ttu-id="a33b1-211">2</span><span class="sxs-lookup"><span data-stu-id="a33b1-211">2</span></span>                       |
| <span data-ttu-id="a33b1-212">1024</span><span class="sxs-lookup"><span data-stu-id="a33b1-212">1024
(&H400)</span></span>         | <span data-ttu-id="a33b1-213">iPad Querformat 1024x768</span><span class="sxs-lookup"><span data-stu-id="a33b1-213">iPad landscape 1024x768</span></span> | <span data-ttu-id="a33b1-214">X-Large</span><span class="sxs-lookup"><span data-stu-id="a33b1-214">X-Large</span></span>    | <span data-ttu-id="a33b1-215">12</span><span class="sxs-lookup"><span data-stu-id="a33b1-215">1.2</span></span>      | <span data-ttu-id="a33b1-216">24</span><span class="sxs-lookup"><span data-stu-id="a33b1-216">2.4</span></span>     | <span data-ttu-id="a33b1-217">3</span><span class="sxs-lookup"><span data-stu-id="a33b1-217">3</span></span>                       |
| <span data-ttu-id="a33b1-218">1368</span><span class="sxs-lookup"><span data-stu-id="a33b1-218">1368</span></span>         | <span data-ttu-id="a33b1-219">Surface Pro 3 1368x912</span><span class="sxs-lookup"><span data-stu-id="a33b1-219">Surface Pro 3 1368x912</span></span>  | <span data-ttu-id="a33b1-220">XX-Large</span><span class="sxs-lookup"><span data-stu-id="a33b1-220">XX-Large</span></span>   | <span data-ttu-id="a33b1-221">12</span><span class="sxs-lookup"><span data-stu-id="a33b1-221">1.2</span></span>      | <span data-ttu-id="a33b1-222">32</span><span class="sxs-lookup"><span data-stu-id="a33b1-222">3.2</span></span>     | <span data-ttu-id="a33b1-223">3</span><span class="sxs-lookup"><span data-stu-id="a33b1-223">3</span></span>                       |
| <span data-ttu-id="a33b1-224">1440</span><span class="sxs-lookup"><span data-stu-id="a33b1-224">1440</span></span>         | <span data-ttu-id="a33b1-225">Surface Pro 4 1440x960</span><span class="sxs-lookup"><span data-stu-id="a33b1-225">Surface Pro 4 1440x960</span></span>  | <span data-ttu-id="a33b1-226">XX-Large</span><span class="sxs-lookup"><span data-stu-id="a33b1-226">XX-Large</span></span>   | <span data-ttu-id="a33b1-227">12</span><span class="sxs-lookup"><span data-stu-id="a33b1-227">1.2</span></span>      | <span data-ttu-id="a33b1-228">32</span><span class="sxs-lookup"><span data-stu-id="a33b1-228">3.2</span></span>     | <span data-ttu-id="a33b1-229">3</span><span class="sxs-lookup"><span data-stu-id="a33b1-229">3</span></span>                       |
| <span data-ttu-id="a33b1-230">1600</span><span class="sxs-lookup"><span data-stu-id="a33b1-230">1600</span></span>         | <span data-ttu-id="a33b1-231">Web 1600x900</span><span class="sxs-lookup"><span data-stu-id="a33b1-231">Web 1600x900</span></span>            | <span data-ttu-id="a33b1-232">XX-Large</span><span class="sxs-lookup"><span data-stu-id="a33b1-232">XX-Large</span></span>   | <span data-ttu-id="a33b1-233">12</span><span class="sxs-lookup"><span data-stu-id="a33b1-233">1.2</span></span>      | <span data-ttu-id="a33b1-234">32</span><span class="sxs-lookup"><span data-stu-id="a33b1-234">3.2</span></span>     | <span data-ttu-id="a33b1-235">3</span><span class="sxs-lookup"><span data-stu-id="a33b1-235">3</span></span>                       |
| <span data-ttu-id="a33b1-236">1920</span><span class="sxs-lookup"><span data-stu-id="a33b1-236">1920</span></span>         | <span data-ttu-id="a33b1-237">Web 1920x1080</span><span class="sxs-lookup"><span data-stu-id="a33b1-237">Web 1920x1080</span></span>           | <span data-ttu-id="a33b1-238">XXX-Large</span><span class="sxs-lookup"><span data-stu-id="a33b1-238">XXX-Large</span></span>  | <span data-ttu-id="a33b1-239">12</span><span class="sxs-lookup"><span data-stu-id="a33b1-239">1.2</span></span>      | <span data-ttu-id="a33b1-240">32</span><span class="sxs-lookup"><span data-stu-id="a33b1-240">3.2</span></span>     | <span data-ttu-id="a33b1-241">3</span><span class="sxs-lookup"><span data-stu-id="a33b1-241">3</span></span>                       |

## <a name="see-also"></a><span data-ttu-id="a33b1-242">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="a33b1-242">See also</span></span>

- [<span data-ttu-id="a33b1-243">Design – Toolkit und Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a33b1-243">Design toolkit and assets</span></span>](https://developer.microsoft.com/de-de/fabric#/resources)


