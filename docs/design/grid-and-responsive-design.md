---
title: Rasterdesigns und dynamische Designs in SharePoint
ms.date: 9/25/2017
ms.openlocfilehash: cb3fc7476188614e5cc49cd560ab4aeb86e813ca
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/24/2017
---
# <a name="sharepoint-grid-and-responsive-design"></a><span data-ttu-id="d7989-102">Rasterdesigns und dynamische Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d7989-102">SharePoint grid and responsive design</span></span>
 
<span data-ttu-id="d7989-103">Dynamische Benutzeroberflächen skalieren nahtlos für verschiedene Geräte, sodass Ihre Inhalte passend für die jeweilige Bildschirmgröße dargestellt werden.</span><span class="sxs-lookup"><span data-stu-id="d7989-103">Responsive experiences seamlessly scale across devices, to better display your content on a range of different screen sizes.</span></span> <span data-ttu-id="d7989-104">Dank dynamischer Designs entfällt zudem die Notwendigkeit, für unterschiedliche Geräte jeweils eigene Versionen der Seiten auf Ihrer Website zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d7989-104">Responsive design also eliminates the need to build multiple versions of your site pages to support different devices.</span></span>  

<span data-ttu-id="d7989-105">Die Designrichtlinien für dynamische Seiten in der SharePoint-Erstellungsumgebung beinhalten ein dynamisches Rastersystem, das auf [Office UI Fabric](https://dev.office.com/fabric) basiert.</span><span class="sxs-lookup"><span data-stu-id="d7989-105">The design guidance for responsive pages in the SharePoint authoring environment incorporates a responsive grid system that is based on [Office UI Fabric](https://dev.office.com/fabric).</span></span> <span data-ttu-id="d7989-106">In diesem Artikel werden das zugrunde liegende Seitenrastersystem und die Haltepunkte beschrieben, d. h. die Bildschirmgrößen, bei denen das Seitenlayout angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="d7989-106">This article describes the underlying page grid system and the breakpoints, or key screen sizes where the layout of the pages will change.</span></span> 


![SharePoint-Seite auf verschiedenen Geräten](../images/design-grid-responsive-overview.png)



## <a name="page-type-grids"></a><span data-ttu-id="d7989-108">Seitentypraster</span><span class="sxs-lookup"><span data-stu-id="d7989-108">Page type grids</span></span> 

<span data-ttu-id="d7989-109">Für jeden Seitentyp in der SharePoint-Erstellungsumgebung lassen sich eigene Regeln für die Anwendung des dynamischen Fabric-Rasters festlegen.</span><span class="sxs-lookup"><span data-stu-id="d7989-109">Each page type in the SharePoint authoring experience can have its own rules for how it applies the Fabric responsive grid.</span></span> <span data-ttu-id="d7989-110">Dadurch wird sichergestellt, dass jede Seite optimal dargestellt wird, unabhängig davon, für welches Gerät sie entworfen ist, und dass die Oberfläche für das jeweilige Gerät optimiert ist.</span><span class="sxs-lookup"><span data-stu-id="d7989-110">This is to ensure that each page looks great, regardless of what device it's designed for, and that the experience is optimized for that environment.</span></span> <span data-ttu-id="d7989-111">Das grundlegende Raster für SharePoint-Desktopoberflächen ist eine Struktur mit 12 Spalten.</span><span class="sxs-lookup"><span data-stu-id="d7989-111">The basic grid in the SharePoint desktop experiences is a 12 column structure.</span></span> <span data-ttu-id="d7989-112">Die Anzahl der Spalten und die Bundstegbreite werden basierend auf der Breite des Bildschirms angepasst.</span><span class="sxs-lookup"><span data-stu-id="d7989-112">The number of columns and gutter width will adjust based on the screen width.</span></span> 

<span data-ttu-id="d7989-113">In den folgenden Abschnitt zeigen wir Ihnen, wie die grundlegende Rasterstruktur auf verschiedene Typen von SharePoint-Seiten angewendet wird. So können Sie sich einen Überblick darüber verschaffen, wie sich das Raster an die jeweiligen Oberflächen- und Geräteanforderungen anpasst.</span><span class="sxs-lookup"><span data-stu-id="d7989-113">The following sections show the basic grid structure applied across different types of SharePoint pages, to help you better understand how the grid adjusts to support the experience and device needs.</span></span>


![Abbildung eines Rasters mit 12 Spalten](../images/design-grid_diagram.png)



### <a name="team-sites"></a><span data-ttu-id="d7989-115">Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="d7989-115">Team sites</span></span>

<span data-ttu-id="d7989-116">Der Inhaltsbereich einer Teamwebsite ist linksbündig fixiert.</span><span class="sxs-lookup"><span data-stu-id="d7989-116">The content area for a team site is locked to the left.</span></span> <span data-ttu-id="d7989-117">Der Navigationsbereich befindet sich auf Teamwebsites links. Die Bereichswebparts belegen daher das Raster, und beim dynamischen Umbruch wird der für die Navigation reservierte Bereich berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="d7989-117">Team sites have a left navigation, therefore the space web parts occupy on the gird and the reflow behavior respects the space given to the navigation.</span></span> <span data-ttu-id="d7989-118">Die maximale Breite des Inhaltsbereichs einer Teamwebsite beträgt 1.204 Pixel, die minimale Größe 320 Pixel für eine optimale Darstellung auf Mobilgeräten.</span><span class="sxs-lookup"><span data-stu-id="d7989-118">The max width of the content area of a Team site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Teamwebsite](../images/design-grid-team-site.png)

<span data-ttu-id="d7989-120">Die folgenden Beispiele demonstrieren, wie das Raster an den jeweiligen Haupthaltepunkten auf einer Teamwebsite angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="d7989-120">The following examples show how the grid adjusts between key breakpoints on a team site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="d7989-121">Klein (320 × 568)</span><span class="sxs-lookup"><span data-stu-id="d7989-121">Small 320 x 568</span></span>
<span data-ttu-id="d7989-122">Das kleine Raster besteht aus einem einzelnen zentrierten Spaltenbereich mit einem Rand von 20 Pixel links und rechts.</span><span class="sxs-lookup"><span data-stu-id="d7989-122">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Teamwebsite (kleines Raster)](../images/design-grid-Team-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a><span data-ttu-id="d7989-124">Mittel (480 × 854)</span><span class="sxs-lookup"><span data-stu-id="d7989-124">Medium 480 x 854</span></span>
<span data-ttu-id="d7989-125">Das mittelgroße Raster besteht aus 12 Spalten mit Bundstegen von je 16 Pixel.</span><span class="sxs-lookup"><span data-stu-id="d7989-125">The medium size has 12 columns, with 16px gutters.</span></span>

![Teamwebsite (mittelgroßes Raster)](../images/design-grid-Team-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a><span data-ttu-id="d7989-127">Groß (640 × 1.024)</span><span class="sxs-lookup"><span data-stu-id="d7989-127">Large 640 x 1024</span></span>
<span data-ttu-id="d7989-128">Das große Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.</span><span class="sxs-lookup"><span data-stu-id="d7989-128">The large size has 12 columns, with 24px gutters.</span></span>

![Teamwebsite (großes Raster)](../images/design-grid-Team-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a><span data-ttu-id="d7989-130">XL (1.024 × 768)</span><span class="sxs-lookup"><span data-stu-id="d7989-130">XL 1024 x 768</span></span>
<span data-ttu-id="d7989-131">Das XL-Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.</span><span class="sxs-lookup"><span data-stu-id="d7989-131">The large size has 12 columns, with 24px gutters.</span></span>

![Teamwebsite (XL-Raster)](../images/design-grid-Team-site-XL-Canvas-24px-gutters.png)

#### <a name="xxl-1366-x-768"></a><span data-ttu-id="d7989-133">XXL (1.366 × 768)</span><span class="sxs-lookup"><span data-stu-id="d7989-133">XXL 1366 x 768</span></span>
<span data-ttu-id="d7989-134">Das XXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.</span><span class="sxs-lookup"><span data-stu-id="d7989-134">The XXL size has a twelve columns, with 32px gutters.</span></span>

![Teamwebsite (XXL-Raster)](../images/design-grid-Team-site-XXL-Canvas-32px-gutters.png)


#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="d7989-136">XXXL (1.920 × 1.080)</span><span class="sxs-lookup"><span data-stu-id="d7989-136">XXXL 1920 x 1080</span></span>
<span data-ttu-id="d7989-137">Das XXXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32.</span><span class="sxs-lookup"><span data-stu-id="d7989-137">The XXXL size has a twelve columns, with 32px gutters.</span></span>

![Teamwebsite (XXXL-Raster)](../images/design-grid-Team-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="team-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="d7989-139">Teamwebsite mit mehrspaltigen Seiten und Webparts</span><span class="sxs-lookup"><span data-stu-id="d7989-139">Team site multicolumn pages and web parts</span></span>
<span data-ttu-id="d7989-140">Webparts werden je nach Seitenlayout horizontal skaliert.</span><span class="sxs-lookup"><span data-stu-id="d7989-140">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="d7989-141">Das folgende Beispiel veranschaulicht, wie die Größe eines Webparts an die Größe des linken Navigationsbereichs angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="d7989-141">The following example shows how the size of a web part adjusts to accommodate the left navigation.</span></span>

![Teamwebsite mit mehrspaltiger Seite und Webparts](../images/design-grid-Team-site-web-parts.png)


### <a name="communication-sites"></a><span data-ttu-id="d7989-143">Kommunikationswebsites</span><span class="sxs-lookup"><span data-stu-id="d7989-143">Communication sites</span></span>

<span data-ttu-id="d7989-144">Kommunikationswebsites verfügen über eine Navigationsleiste oben auf der Seite sowie einen zentrierten Inhaltsbereich.</span><span class="sxs-lookup"><span data-stu-id="d7989-144">Communication sites have a top navigation and a centered content area.</span></span> <span data-ttu-id="d7989-145">Die maximale Breite des Inhaltsbereichs einer Kommunikationswebsite beträgt 1.204 Pixel, die Mindestgröße 320 Pixel für eine optimale Darstellung auf Mobilgeräten.</span><span class="sxs-lookup"><span data-stu-id="d7989-145">The maximum width of the content area of a communication site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Kommunikationswebsite](../images/design-grid-communication_site.png)

<span data-ttu-id="d7989-147">Die folgenden Beispiele zeigen, wie das Raster an den jeweiligen Haupthaltepunkten auf einer Kommunikationswebsite angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="d7989-147">The following examples show how the grid adjusts between key breakpoints on a communication site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="d7989-148">Klein (320 × 568)</span><span class="sxs-lookup"><span data-stu-id="d7989-148">Small 320 x 568</span></span>
<span data-ttu-id="d7989-149">Das kleine Raster besteht aus einem einzelnen zentrierten Spaltenbereich mit einem Rand von 20 Pixel links und rechts.</span><span class="sxs-lookup"><span data-stu-id="d7989-149">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Kommunikationswebsite (kleines Raster)](../images/design-grid-Communication-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a><span data-ttu-id="d7989-151">Mittel (480 × 854)</span><span class="sxs-lookup"><span data-stu-id="d7989-151">Medium 480 x 854</span></span>
<span data-ttu-id="d7989-152">Das mittelgroße Raster besteht aus 12 Spalten mit Bundstegen von je 16 Pixel.</span><span class="sxs-lookup"><span data-stu-id="d7989-152">The medium size has 12 columns, with 16px gutters.</span></span>

![Kommunikationswebsite (mittelgroßes Raster)](../images/design-grid-Communication-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a><span data-ttu-id="d7989-154">Groß (640 × 1.024)</span><span class="sxs-lookup"><span data-stu-id="d7989-154">Large 640 x 1024</span></span>
<span data-ttu-id="d7989-155">Das große Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.</span><span class="sxs-lookup"><span data-stu-id="d7989-155">The large size has 12 columns, with 24px gutters.</span></span>

![Kommunikationswebsite (großes Raster)](../images/design-grid-Communication-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a><span data-ttu-id="d7989-157">XL (1.024 × 768)</span><span class="sxs-lookup"><span data-stu-id="d7989-157">XL 1024 x 768</span></span>
<span data-ttu-id="d7989-158">Das XL-Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.</span><span class="sxs-lookup"><span data-stu-id="d7989-158">The XL size has a twelve columns, with 24px gutters.</span></span>

![Kommunikationswebsite (XL-Raster)](../images/design-grid-Communication-site-XL-Canvas-24px-gutters.png)


#### <a name="xxl-1366-x-768"></a><span data-ttu-id="d7989-160">XXL (1.366 × 768)</span><span class="sxs-lookup"><span data-stu-id="d7989-160">XXL 1366 x 768</span></span>
<span data-ttu-id="d7989-161">Das XXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.</span><span class="sxs-lookup"><span data-stu-id="d7989-161">The XXL size has a twelve columns, with 32px gutters.</span></span>

![Kommunikationswebsite (XXL-Raster)](../images/design-grid-Communication-site-XXL-Canvas-32px-gutters-maxwidth-1204.png)


#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="d7989-163">XXXL (1.920 × 1.080)</span><span class="sxs-lookup"><span data-stu-id="d7989-163">XXXL 1920 x 1080</span></span>
<span data-ttu-id="d7989-164">Das XXXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.</span><span class="sxs-lookup"><span data-stu-id="d7989-164">The XXXL size has a twelve columns, with 32px gutters.</span></span>

![Kommunikationswebsite (XXXL-Raster)](../images/design-grid-Communication-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="communication-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="d7989-166">Kommunikationswebsite mit mehrspaltigen Seiten und Webparts</span><span class="sxs-lookup"><span data-stu-id="d7989-166">Communication site multicolumn pages and web parts</span></span>
<span data-ttu-id="d7989-167">Webparts werden je nach Seitenlayout horizontal skaliert.</span><span class="sxs-lookup"><span data-stu-id="d7989-167">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="d7989-168">Das Beispiel unten veranschaulicht eine Kommunikationswebsite und Webparts in einem Layout mit einer bis drei Spalten.</span><span class="sxs-lookup"><span data-stu-id="d7989-168">This example shows a communcation site and web parts for single to three column layouts.</span></span>

![Kommunikationswebsite mit mehreren Spalten und Webparts](../images/design-grid-Communciation-site-web-parts.png)



## <a name="breakpoints"></a><span data-ttu-id="d7989-170">Haltepunkte</span><span class="sxs-lookup"><span data-stu-id="d7989-170">Breakpoints</span></span> 

<span data-ttu-id="d7989-171">Damit die Oberfläche sich nahtlos an unterschiedliche Bildschirmgrößen anpasst, sollte die SharePoint-UI das Layout an den folgenden Haltepunktbreiten anpassen:</span><span class="sxs-lookup"><span data-stu-id="d7989-171">To create a smooth flowing experience between screen sizes, the SharePoint UI should adapt layouts for the following breakpoint widths:</span></span> 

- <span data-ttu-id="d7989-172">320</span><span class="sxs-lookup"><span data-stu-id="d7989-172">320</span></span>
- <span data-ttu-id="d7989-173">1.024</span><span class="sxs-lookup"><span data-stu-id="d7989-173">1024</span></span>
- <span data-ttu-id="d7989-174">1.366</span><span class="sxs-lookup"><span data-stu-id="d7989-174">1366</span></span>
- <span data-ttu-id="d7989-175">1.920</span><span class="sxs-lookup"><span data-stu-id="d7989-175">1920</span></span>
 
<span data-ttu-id="d7989-176">Dabei sollten Sie bedenken, wie Ihre Inhalte sich zwischen diesen Haltepunkten verändern, wenn die Größe des Darstellungsbereichs an den nächstgelegenen Haltepunkt angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="d7989-176">Within these breakpoints, you should take into consideration how your content will shift when the viewport size becomes optimized for the nearest breakpoint.</span></span> <span data-ttu-id="d7989-177">Die Abbildung unten dient lediglich der Veranschaulichung und ist nicht pixelgenau.</span><span class="sxs-lookup"><span data-stu-id="d7989-177">Note that this diagram is for illustration only and is not pixel accurate.</span></span>


![SharePoint-Diagramm mit Haltepunkten](../images/design-grid-breakpoints.png)


<span data-ttu-id="d7989-179">Das dynamische Raster für Teamwebsites und Kommunikationswebsites passt sich bei der Umstellung von einem der großen Haltepunkte an einen Mobilgeräte-Haltepunkt an.</span><span class="sxs-lookup"><span data-stu-id="d7989-179">The responsive grid for both team sites and communication sites adjusts when going from large breakpoints to mobile breakpoints.</span></span> <span data-ttu-id="d7989-180">Dadurch wird die Website optimal an das jeweilige Geräte und die jeweilige Bildschirmgröße angepasst.</span><span class="sxs-lookup"><span data-stu-id="d7989-180">This optimizes the site for the device and screen size.</span></span> <span data-ttu-id="d7989-181">In der folgenden Tabelle finden Sie einen Überblick über die Rastergrößen an verschiedenen Haltepunkten, basierend auf den Bildschirmgrößen gängiger Geräte.</span><span class="sxs-lookup"><span data-stu-id="d7989-181">The following table describes the grid sizes at various breakpoints based on popular device sizes.</span></span>



| <span data-ttu-id="d7989-182">Fensterbreite</span><span class="sxs-lookup"><span data-stu-id="d7989-182">Window width</span></span> | <span data-ttu-id="d7989-183">Gerät</span><span class="sxs-lookup"><span data-stu-id="d7989-183">Device</span></span>                  | <span data-ttu-id="d7989-184">Haltepunkt</span><span class="sxs-lookup"><span data-stu-id="d7989-184">Breakpoint</span></span> | <span data-ttu-id="d7989-185">Spalten</span><span class="sxs-lookup"><span data-stu-id="d7989-185">Columns</span></span> | <span data-ttu-id="d7989-186">Bundsteg</span><span class="sxs-lookup"><span data-stu-id="d7989-186">Gutter</span></span> | <span data-ttu-id="d7989-187">Maximale Anzahl von Spalten pro Abschnitt</span><span class="sxs-lookup"><span data-stu-id="d7989-187">Max columns per section</span></span> |
|--------------|-------------------------|------------|---------|--------|-------------------------|
| <span data-ttu-id="d7989-188">320</span><span class="sxs-lookup"><span data-stu-id="d7989-188">320</span></span>          | <span data-ttu-id="d7989-189">iPhone 5/SE (320 ×568)</span><span class="sxs-lookup"><span data-stu-id="d7989-189">iPhone 5/SE,320x568</span></span>     | <span data-ttu-id="d7989-190">Small</span><span class="sxs-lookup"><span data-stu-id="d7989-190">Small</span></span>      | <span data-ttu-id="d7989-191">1</span><span class="sxs-lookup"><span data-stu-id="d7989-191">1</span></span>       | <span data-ttu-id="d7989-192">-</span><span class="sxs-lookup"><span data-stu-id="d7989-192">N/A</span></span>    | <span data-ttu-id="d7989-193">1</span><span class="sxs-lookup"><span data-stu-id="d7989-193">1</span></span>                       |
| <span data-ttu-id="d7989-194">480</span><span class="sxs-lookup"><span data-stu-id="d7989-194">480</span></span>          | <span data-ttu-id="d7989-195">6-Zoll-Gerät</span><span class="sxs-lookup"><span data-stu-id="d7989-195">6" device</span></span>               | <span data-ttu-id="d7989-196">Medium</span><span class="sxs-lookup"><span data-stu-id="d7989-196">Medium</span></span>     | <span data-ttu-id="d7989-197">1</span><span class="sxs-lookup"><span data-stu-id="d7989-197">1</span></span>       | <span data-ttu-id="d7989-198">-</span><span class="sxs-lookup"><span data-stu-id="d7989-198">N/A</span></span>    | <span data-ttu-id="d7989-199">1</span><span class="sxs-lookup"><span data-stu-id="d7989-199">1</span></span>                       |
| <span data-ttu-id="d7989-200">640</span><span class="sxs-lookup"><span data-stu-id="d7989-200">640</span></span>          | <span data-ttu-id="d7989-201">8-Zoll-Gerät</span><span class="sxs-lookup"><span data-stu-id="d7989-201">8" device</span></span>               | <span data-ttu-id="d7989-202">Large</span><span class="sxs-lookup"><span data-stu-id="d7989-202">Large</span></span>      | <span data-ttu-id="d7989-203">12</span><span class="sxs-lookup"><span data-stu-id="d7989-203">12</span></span>      | <span data-ttu-id="d7989-204">16</span><span class="sxs-lookup"><span data-stu-id="d7989-204">16</span></span>     | <span data-ttu-id="d7989-205">2</span><span class="sxs-lookup"><span data-stu-id="d7989-205">2</span></span>                       |
| <span data-ttu-id="d7989-206">768</span><span class="sxs-lookup"><span data-stu-id="d7989-206">768</span></span>          | <span data-ttu-id="d7989-207">iPad im Hochformat (768 × 1.024)</span><span class="sxs-lookup"><span data-stu-id="d7989-207">iPad portrait 768x1024</span></span>  | <span data-ttu-id="d7989-208">Large</span><span class="sxs-lookup"><span data-stu-id="d7989-208">Large</span></span>      | <span data-ttu-id="d7989-209">12</span><span class="sxs-lookup"><span data-stu-id="d7989-209">12</span></span>      | <span data-ttu-id="d7989-210">24</span><span class="sxs-lookup"><span data-stu-id="d7989-210">24</span></span>     | <span data-ttu-id="d7989-211">2</span><span class="sxs-lookup"><span data-stu-id="d7989-211">2</span></span>                       |
| <span data-ttu-id="d7989-212">1.024</span><span class="sxs-lookup"><span data-stu-id="d7989-212">1024</span></span>         | <span data-ttu-id="d7989-213">iPad im Querformat (1.024 ×768)</span><span class="sxs-lookup"><span data-stu-id="d7989-213">iPad landscape 1024x768</span></span> | <span data-ttu-id="d7989-214">X-Large</span><span class="sxs-lookup"><span data-stu-id="d7989-214">X-Large</span></span>    | <span data-ttu-id="d7989-215">12</span><span class="sxs-lookup"><span data-stu-id="d7989-215">12</span></span>      | <span data-ttu-id="d7989-216">24</span><span class="sxs-lookup"><span data-stu-id="d7989-216">24</span></span>     | <span data-ttu-id="d7989-217">3</span><span class="sxs-lookup"><span data-stu-id="d7989-217">3</span></span>                       |
| <span data-ttu-id="d7989-218">1.368</span><span class="sxs-lookup"><span data-stu-id="d7989-218">1368</span></span>         | <span data-ttu-id="d7989-219">Surface Pro 3 (1.368 × 912)</span><span class="sxs-lookup"><span data-stu-id="d7989-219">Surface Pro 3 1368x912</span></span>  | <span data-ttu-id="d7989-220">XX-Large</span><span class="sxs-lookup"><span data-stu-id="d7989-220">XX-Large</span></span>   | <span data-ttu-id="d7989-221">12</span><span class="sxs-lookup"><span data-stu-id="d7989-221">12</span></span>      | <span data-ttu-id="d7989-222">32</span><span class="sxs-lookup"><span data-stu-id="d7989-222">32</span></span>     | <span data-ttu-id="d7989-223">3</span><span class="sxs-lookup"><span data-stu-id="d7989-223">3</span></span>                       |
| <span data-ttu-id="d7989-224">1.440</span><span class="sxs-lookup"><span data-stu-id="d7989-224">1440</span></span>         | <span data-ttu-id="d7989-225">Surface Pro 4 (1.440 × 960)</span><span class="sxs-lookup"><span data-stu-id="d7989-225">Surface Pro 4 1440x960</span></span>  | <span data-ttu-id="d7989-226">XX-Large</span><span class="sxs-lookup"><span data-stu-id="d7989-226">XX-Large</span></span>   | <span data-ttu-id="d7989-227">12</span><span class="sxs-lookup"><span data-stu-id="d7989-227">12</span></span>      | <span data-ttu-id="d7989-228">32</span><span class="sxs-lookup"><span data-stu-id="d7989-228">32</span></span>     | <span data-ttu-id="d7989-229">3</span><span class="sxs-lookup"><span data-stu-id="d7989-229">3</span></span>                       |
| <span data-ttu-id="d7989-230">1.600</span><span class="sxs-lookup"><span data-stu-id="d7989-230">1600</span></span>         | <span data-ttu-id="d7989-231">Web (1.600 × 900)</span><span class="sxs-lookup"><span data-stu-id="d7989-231">Web 1600x900</span></span>            | <span data-ttu-id="d7989-232">XX-Large</span><span class="sxs-lookup"><span data-stu-id="d7989-232">XX-Large</span></span>   | <span data-ttu-id="d7989-233">12</span><span class="sxs-lookup"><span data-stu-id="d7989-233">12</span></span>      | <span data-ttu-id="d7989-234">32</span><span class="sxs-lookup"><span data-stu-id="d7989-234">32</span></span>     | <span data-ttu-id="d7989-235">3</span><span class="sxs-lookup"><span data-stu-id="d7989-235">3</span></span>                       |
| <span data-ttu-id="d7989-236">1.920</span><span class="sxs-lookup"><span data-stu-id="d7989-236">1920</span></span>         | <span data-ttu-id="d7989-237">Web (1.920 x 1.080)</span><span class="sxs-lookup"><span data-stu-id="d7989-237">Web 1920x1080</span></span>           | <span data-ttu-id="d7989-238">XXX-Large</span><span class="sxs-lookup"><span data-stu-id="d7989-238">XXX-Large</span></span>  | <span data-ttu-id="d7989-239">12</span><span class="sxs-lookup"><span data-stu-id="d7989-239">12</span></span>      | <span data-ttu-id="d7989-240">32</span><span class="sxs-lookup"><span data-stu-id="d7989-240">32</span></span>     | <span data-ttu-id="d7989-241">3</span><span class="sxs-lookup"><span data-stu-id="d7989-241">3</span></span>                       |

## <a name="see-also"></a><span data-ttu-id="d7989-242">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="d7989-242">See also</span></span>

- [<span data-ttu-id="d7989-243">Design Toolkit & Assets</span><span class="sxs-lookup"><span data-stu-id="d7989-243">Design toolkit and assets</span></span>](https://developer.microsoft.com/de-DE/fabric#/resources)


