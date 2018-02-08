---
title: Rasterdesigns und dynamische Designs in SharePoint
description: "Das zugrunde liegende Seitenrastersystem und die Haltepunkte, d. h. die Bildschirmgrößen, bei denen das Seitenlayout angepasst wird."
ms.date: 01/23/2018
ms.openlocfilehash: b94980b57682e519091272bcf3801fcffcf854ff
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-grid-and-responsive-design"></a><span data-ttu-id="b1cbf-103">Rasterdesigns und dynamische Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1cbf-103">SharePoint grid and responsive design</span></span>
 
<span data-ttu-id="b1cbf-104">Dynamische Benutzeroberflächen skalieren nahtlos für verschiedene Geräte, sodass Ihre Inhalte passend für die jeweilige Bildschirmgröße dargestellt werden.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-104">Responsive experiences seamlessly scale across devices, to better display your content on a range of different screen sizes.</span></span> <span data-ttu-id="b1cbf-105">Dank dynamischer Designs entfällt zudem die Notwendigkeit, für unterschiedliche Geräte jeweils eigene Versionen der Seiten auf Ihrer Website zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-105">Responsive design also eliminates the need to build multiple versions of your site pages to support different devices.</span></span>  

<span data-ttu-id="b1cbf-106">Die Designrichtlinien für dynamische Seiten in der SharePoint-Erstellungsumgebung beinhalten ein dynamisches Rastersystem, das auf [Office UI Fabric](https://developer.microsoft.com/de-DE/fabric) basiert.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-106">The design guidance for responsive pages in the SharePoint authoring environment incorporates a responsive grid system that is based on [Office UI Fabric](https://developer.microsoft.com/de-DE/fabric).</span></span> <span data-ttu-id="b1cbf-107">In diesem Artikel werden das zugrunde liegende Seitenrastersystem und die Haltepunkte beschrieben, d. h. die Bildschirmgrößen, bei denen das Seitenlayout angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-107">This article describes the underlying page grid system and the breakpoints, or key screen sizes where the layout of the pages will change.</span></span> 


![SharePoint-Seite auf verschiedenen Geräten](../images/design-grid-responsive-overview.png)



## <a name="page-type-grids"></a><span data-ttu-id="b1cbf-109">Seitentypraster</span><span class="sxs-lookup"><span data-stu-id="b1cbf-109">Page type grids</span></span> 

<span data-ttu-id="b1cbf-110">Für jeden Seitentyp in der SharePoint-Erstellungsumgebung lassen sich eigene Regeln für die Anwendung des dynamischen Fabric-Rasters festlegen.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-110">Each page type in the SharePoint authoring experience can have its own rules for how it applies the Fabric responsive grid.</span></span> <span data-ttu-id="b1cbf-111">Dadurch wird sichergestellt, dass jede Seite optimal dargestellt wird, unabhängig davon, für welches Gerät sie entworfen ist, und dass die Oberfläche für das jeweilige Gerät optimiert ist.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-111">This is to ensure that each page looks great, regardless of what device it's designed for, and that the experience is optimized for that environment.</span></span> <span data-ttu-id="b1cbf-112">Das grundlegende Raster für SharePoint-Desktopoberflächen ist eine Struktur mit 12 Spalten.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-112">The basic grid in the SharePoint desktop experiences is a 12 column structure.</span></span> <span data-ttu-id="b1cbf-113">Die Anzahl der Spalten und die Bundstegbreite werden basierend auf der Breite des Bildschirms angepasst.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-113">The number of columns and gutter width will adjust based on the screen width.</span></span> 

<span data-ttu-id="b1cbf-114">In den folgenden Abschnitt zeigen wir Ihnen, wie die grundlegende Rasterstruktur auf verschiedene Typen von SharePoint-Seiten angewendet wird. So können Sie sich einen Überblick darüber verschaffen, wie sich das Raster an die jeweiligen Oberflächen- und Geräteanforderungen anpasst.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-114">The following sections show the basic grid structure applied across different types of SharePoint pages, to help you better understand how the grid adjusts to support the experience and device needs.</span></span>


![Abbildung eines Rasters mit 12 Spalten](../images/design-grid_diagram.png)

<br/>

### <a name="team-sites"></a><span data-ttu-id="b1cbf-116">Teamwebsites</span><span class="sxs-lookup"><span data-stu-id="b1cbf-116">Team sites</span></span>

<span data-ttu-id="b1cbf-117">Der Inhaltsbereich einer Teamwebsite ist linksbündig fixiert.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-117">The content area for a team site is locked to the left.</span></span> <span data-ttu-id="b1cbf-118">Der Navigationsbereich befindet sich auf Teamwebsites links. Die Bereichswebparts belegen daher das Raster, und beim dynamischen Umbruch wird der für die Navigation reservierte Bereich berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-118">Team sites have a left navigation, therefore the space web parts occupy on the gird and the reflow behavior respects the space given to the navigation.</span></span> <span data-ttu-id="b1cbf-119">Die maximale Breite des Inhaltsbereichs einer Teamwebsite beträgt 1.204 Pixel, die minimale Größe 320 Pixel für eine optimale Darstellung auf Mobilgeräten.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-119">The max width of the content area of a Team site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Teamwebsite](../images/design-grid-team-site.png)

<br/>

<span data-ttu-id="b1cbf-121">Die folgenden Beispiele demonstrieren, wie das Raster an den jeweiligen Haupthaltepunkten auf einer Teamwebsite angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-121">The following examples show how the grid adjusts between key breakpoints on a team site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="b1cbf-122">Klein (320 × 568)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-122">Small 320 x 568</span></span>
<span data-ttu-id="b1cbf-123">Das kleine Raster besteht aus einem einzelnen zentrierten Spaltenbereich mit einem Rand von 20 Pixel links und rechts.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-123">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Teamwebsite (kleines Raster)](../images/design-grid-Team-site-S-Canvas-no-column.png)

<br/>

#### <a name="medium-480-x-854"></a><span data-ttu-id="b1cbf-125">Mittel (480 × 854)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-125">Medium 480 x 854</span></span>
<span data-ttu-id="b1cbf-126">Das mittelgroße Raster besteht aus 12 Spalten mit Bundstegen von je 16 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-126">The medium size has 12 columns, with 16px gutters.</span></span>

![Teamwebsite (mittelgroßes Raster)](../images/design-grid-Team-site-M-Canvas-16px-gutters.png)

<br/>

#### <a name="large-640-x-1024"></a><span data-ttu-id="b1cbf-128">Groß (640 × 1.024)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-128">Large 640 x 1024</span></span>
<span data-ttu-id="b1cbf-129">Das große Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-129">The large size has 12 columns, with 24px gutters.</span></span>

![Teamwebsite (großes Raster)](../images/design-grid-Team-site-L-Canvas-24px-gutters.png)

<br/>

#### <a name="xl-1024-x-768"></a><span data-ttu-id="b1cbf-131">XL (1.024 × 768)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-131">XL 1024 x 768</span></span>
<span data-ttu-id="b1cbf-132">Das XL-Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-132">The XL size has 12 columns, with 24px gutters.</span></span>

![Teamwebsite (XL-Raster)](../images/design-grid-Team-site-XL-Canvas-24px-gutters.png)

<br/>

#### <a name="xxl-1366-x-768"></a><span data-ttu-id="b1cbf-134">XXL (1.366 × 768)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-134">XXL 1366 x 768</span></span>
<span data-ttu-id="b1cbf-135">Das XXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-135">The XXL size has 12 columns, with 32px gutters.</span></span>

![Teamwebsite (XXL-Raster)](../images/design-grid-Team-site-XXL-Canvas-32px-gutters.png)

<br/>

#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="b1cbf-137">XXXL (1.920 × 1.080)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-137">XXXL 1920 x 1080</span></span>
<span data-ttu-id="b1cbf-138">Das XXXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-138">The XXXL size has 12 columns, with 32px gutters.</span></span>

![Teamwebsite (XXXL-Raster)](../images/design-grid-Team-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

<br/>

#### <a name="team-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="b1cbf-140">Teamwebsite mit mehrspaltigen Seiten und Webparts</span><span class="sxs-lookup"><span data-stu-id="b1cbf-140">Team site multicolumn pages and web parts</span></span>
<span data-ttu-id="b1cbf-141">Webparts werden je nach Seitenlayout horizontal skaliert.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-141">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="b1cbf-142">Das folgende Beispiel veranschaulicht, wie die Größe eines Webparts an die Größe des linken Navigationsbereichs angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-142">The following example shows how the size of a web part adjusts to accommodate the left navigation.</span></span>

![Teamwebsite mit mehrspaltiger Seite und Webparts](../images/design-grid-Team-site-web-parts.png)


### <a name="communication-sites"></a><span data-ttu-id="b1cbf-144">Kommunikationswebsites</span><span class="sxs-lookup"><span data-stu-id="b1cbf-144">Communication sites</span></span>

<span data-ttu-id="b1cbf-145">Kommunikationswebsites verfügen über eine Navigationsleiste oben auf der Seite sowie einen zentrierten Inhaltsbereich.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-145">Communication sites have a top navigation and a centered content area.</span></span> <span data-ttu-id="b1cbf-146">Die maximale Breite des Inhaltsbereichs einer Kommunikationswebsite beträgt 1.204 Pixel, die Mindestgröße 320 Pixel für eine optimale Darstellung auf Mobilgeräten.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-146">The maximum width of the content area of a communication site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Kommunikationswebsite](../images/design-grid-communication_site.png)

<br/>

<span data-ttu-id="b1cbf-148">Die folgenden Beispiele zeigen, wie das Raster an den jeweiligen Haupthaltepunkten auf einer Kommunikationswebsite angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-148">The following examples show how the grid adjusts between key breakpoints on a communication site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="b1cbf-149">Klein (320 × 568)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-149">Small 320 x 568</span></span>
<span data-ttu-id="b1cbf-150">Das kleine Raster besteht aus einem einzelnen zentrierten Spaltenbereich mit einem Rand von 20 Pixel links und rechts.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-150">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Kommunikationswebsite (kleines Raster)](../images/design-grid-Communication-site-S-Canvas-no-column.png)

<br/>

#### <a name="medium-480-x-854"></a><span data-ttu-id="b1cbf-152">Mittel (480 × 854)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-152">Medium 480 x 854</span></span>
<span data-ttu-id="b1cbf-153">Das mittelgroße Raster besteht aus 12 Spalten mit Bundstegen von je 16 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-153">The medium size has 12 columns, with 16px gutters.</span></span>

![Kommunikationswebsite (mittelgroßes Raster)](../images/design-grid-Communication-site-M-Canvas-16px-gutters.png)

<br/>

#### <a name="large-640-x-1024"></a><span data-ttu-id="b1cbf-155">Groß (640 × 1.024)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-155">Large 640 x 1024</span></span>
<span data-ttu-id="b1cbf-156">Das große Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-156">The large size has 12 columns, with 24px gutters.</span></span>

![Kommunikationswebsite (großes Raster)](../images/design-grid-Communication-site-L-Canvas-24px-gutters.png)

<br/>

#### <a name="xl-1024-x-768"></a><span data-ttu-id="b1cbf-158">XL (1.024 × 768)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-158">XL 1024 x 768</span></span>
<span data-ttu-id="b1cbf-159">Das XL-Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-159">The XL size has 12 columns, with 24px gutters.</span></span>

![Kommunikationswebsite (XL-Raster)](../images/design-grid-Communication-site-XL-Canvas-24px-gutters.png)

<br/>

#### <a name="xxl-1366-x-768"></a><span data-ttu-id="b1cbf-161">XXL (1.366 × 768)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-161">XXL 1366 x 768</span></span>
<span data-ttu-id="b1cbf-162">Das XXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-162">The XXL size has 12 columns, with 32px gutters.</span></span>

![Kommunikationswebsite (XXL-Raster)](../images/design-grid-Communication-site-XXL-Canvas-32px-gutters-maxwidth-1204.png)

<br/>

#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="b1cbf-164">XXXL (1.920 × 1.080)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-164">XXXL 1920 x 1080</span></span>
<span data-ttu-id="b1cbf-165">Das XXXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-165">The XXXL size has 12 columns, with 32px gutters.</span></span>

![Kommunikationswebsite (XXXL-Raster)](../images/design-grid-Communication-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

<br/>

#### <a name="communication-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="b1cbf-167">Kommunikationswebsite mit mehrspaltigen Seiten und Webparts</span><span class="sxs-lookup"><span data-stu-id="b1cbf-167">Communication site multicolumn pages and web parts</span></span>
<span data-ttu-id="b1cbf-168">Webparts werden je nach Seitenlayout horizontal skaliert.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-168">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="b1cbf-169">Das Beispiel unten veranschaulicht eine Kommunikationswebsite und Webparts in einem Layout mit einer bis drei Spalten.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-169">This example shows a communcation site and web parts for single to three column layouts.</span></span>

![Kommunikationswebsite mit mehreren Spalten und Webparts](../images/design-grid-Communciation-site-web-parts.png)



## <a name="breakpoints"></a><span data-ttu-id="b1cbf-171">Haltepunkte</span><span class="sxs-lookup"><span data-stu-id="b1cbf-171">Breakpoints</span></span> 

<span data-ttu-id="b1cbf-172">Damit die Oberfläche sich nahtlos an unterschiedliche Bildschirmgrößen anpasst, sollte die SharePoint-UI das Layout an den folgenden Haltepunktbreiten anpassen:</span><span class="sxs-lookup"><span data-stu-id="b1cbf-172">To create a smooth flowing experience between screen sizes, the SharePoint UI should adapt layouts for the following breakpoint widths:</span></span> 

- <span data-ttu-id="b1cbf-173">320 px</span><span class="sxs-lookup"><span data-stu-id="b1cbf-173">320 px</span></span>
- <span data-ttu-id="b1cbf-174">1024 px</span><span class="sxs-lookup"><span data-stu-id="b1cbf-174">1024 px</span></span>
- <span data-ttu-id="b1cbf-175">1366 px</span><span class="sxs-lookup"><span data-stu-id="b1cbf-175">1366 px</span></span>
- <span data-ttu-id="b1cbf-176">1920 px</span><span class="sxs-lookup"><span data-stu-id="b1cbf-176">1920 px</span></span>
 
<span data-ttu-id="b1cbf-177">Dabei sollten Sie bedenken, wie Ihre Inhalte sich zwischen diesen Haltepunkten verändern, wenn die Größe des Darstellungsbereichs an den nächstgelegenen Haltepunkt angepasst wird.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-177">Within these breakpoints, you should take into consideration how your content will shift when the viewport size becomes optimized for the nearest breakpoint.</span></span> <span data-ttu-id="b1cbf-178">Die Abbildung unten dient lediglich der Veranschaulichung und ist nicht pixelgenau.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-178">Note that this diagram is for illustration only and is not pixel accurate.</span></span>


![SharePoint-Diagramm mit Haltepunkten](../images/design-grid-breakpoints.png)

<br/>

<span data-ttu-id="b1cbf-180">Das dynamische Raster für Teamwebsites und Kommunikationswebsites passt sich bei der Umstellung von einem der großen Haltepunkte an einen Mobilgeräte-Haltepunkt an.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-180">The responsive grid for both team sites and communication sites adjusts when going from large breakpoints to mobile breakpoints.</span></span> <span data-ttu-id="b1cbf-181">Dadurch wird die Website optimal an das jeweilige Geräte und die jeweilige Bildschirmgröße angepasst.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-181">This optimizes the site for the device and screen size.</span></span> <span data-ttu-id="b1cbf-182">In der folgenden Tabelle finden Sie einen Überblick über die Rastergrößen an verschiedenen Haltepunkten, basierend auf den Bildschirmgrößen gängiger Geräte.</span><span class="sxs-lookup"><span data-stu-id="b1cbf-182">The following table describes the grid sizes at various breakpoints based on popular device sizes.</span></span>



| <span data-ttu-id="b1cbf-183">Fensterbreite</span><span class="sxs-lookup"><span data-stu-id="b1cbf-183">Window width</span></span> | <span data-ttu-id="b1cbf-184">Gerät</span><span class="sxs-lookup"><span data-stu-id="b1cbf-184">Device</span></span>                  | <span data-ttu-id="b1cbf-185">Haltepunkt</span><span class="sxs-lookup"><span data-stu-id="b1cbf-185">Breakpoint</span></span> | <span data-ttu-id="b1cbf-186">Spalten</span><span class="sxs-lookup"><span data-stu-id="b1cbf-186">Columns</span></span> | <span data-ttu-id="b1cbf-187">Bundsteg</span><span class="sxs-lookup"><span data-stu-id="b1cbf-187">Gutter</span></span> | <span data-ttu-id="b1cbf-188">Maximale Anzahl von Spalten pro Abschnitt</span><span class="sxs-lookup"><span data-stu-id="b1cbf-188">Max columns per section</span></span> |
|:-------------|:------------------------|:-----------|:-------:|:------:|:-----------------------:|
| <span data-ttu-id="b1cbf-189">320</span><span class="sxs-lookup"><span data-stu-id="b1cbf-189">320</span></span>          | <span data-ttu-id="b1cbf-190">iPhone 5/SE (320 ×568)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-190">iPhone 5/SE,320x568</span></span>     | <span data-ttu-id="b1cbf-191">Small</span><span class="sxs-lookup"><span data-stu-id="b1cbf-191">Small</span></span>      | <span data-ttu-id="b1cbf-192">1</span><span class="sxs-lookup"><span data-stu-id="b1cbf-192">1</span></span>       | <span data-ttu-id="b1cbf-193">-</span><span class="sxs-lookup"><span data-stu-id="b1cbf-193">N/A</span></span>    | <span data-ttu-id="b1cbf-194">1</span><span class="sxs-lookup"><span data-stu-id="b1cbf-194">1</span></span>                       |
| <span data-ttu-id="b1cbf-195">480</span><span class="sxs-lookup"><span data-stu-id="b1cbf-195">480</span></span>          | <span data-ttu-id="b1cbf-196">6-Zoll-Gerät</span><span class="sxs-lookup"><span data-stu-id="b1cbf-196">6" device</span></span>               | <span data-ttu-id="b1cbf-197">Medium</span><span class="sxs-lookup"><span data-stu-id="b1cbf-197">Medium</span></span>     | <span data-ttu-id="b1cbf-198">1</span><span class="sxs-lookup"><span data-stu-id="b1cbf-198">1</span></span>       | <span data-ttu-id="b1cbf-199">-</span><span class="sxs-lookup"><span data-stu-id="b1cbf-199">N/A</span></span>    | <span data-ttu-id="b1cbf-200">1</span><span class="sxs-lookup"><span data-stu-id="b1cbf-200">1</span></span>                       |
| <span data-ttu-id="b1cbf-201">640</span><span class="sxs-lookup"><span data-stu-id="b1cbf-201">640</span></span>          | <span data-ttu-id="b1cbf-202">8-Zoll-Gerät</span><span class="sxs-lookup"><span data-stu-id="b1cbf-202">8" device</span></span>               | <span data-ttu-id="b1cbf-203">Large</span><span class="sxs-lookup"><span data-stu-id="b1cbf-203">Large</span></span>      | <span data-ttu-id="b1cbf-204">12</span><span class="sxs-lookup"><span data-stu-id="b1cbf-204">1.2</span></span>      | <span data-ttu-id="b1cbf-205">16</span><span class="sxs-lookup"><span data-stu-id="b1cbf-205">1.6</span></span>     | <span data-ttu-id="b1cbf-206">2</span><span class="sxs-lookup"><span data-stu-id="b1cbf-206">2</span></span>                       |
| <span data-ttu-id="b1cbf-207">768</span><span class="sxs-lookup"><span data-stu-id="b1cbf-207">768</span></span>          | <span data-ttu-id="b1cbf-208">iPad im Hochformat (768 × 1.024)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-208">iPad portrait 768x1024</span></span>  | <span data-ttu-id="b1cbf-209">Large</span><span class="sxs-lookup"><span data-stu-id="b1cbf-209">Large</span></span>      | <span data-ttu-id="b1cbf-210">12</span><span class="sxs-lookup"><span data-stu-id="b1cbf-210">1.2</span></span>      | <span data-ttu-id="b1cbf-211">24</span><span class="sxs-lookup"><span data-stu-id="b1cbf-211">2.4</span></span>     | <span data-ttu-id="b1cbf-212">2</span><span class="sxs-lookup"><span data-stu-id="b1cbf-212">2</span></span>                       |
| <span data-ttu-id="b1cbf-213">1.024</span><span class="sxs-lookup"><span data-stu-id="b1cbf-213">1024
(&H400)</span></span>         | <span data-ttu-id="b1cbf-214">iPad im Querformat (1.024 ×768)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-214">iPad landscape 1024x768</span></span> | <span data-ttu-id="b1cbf-215">X-Large</span><span class="sxs-lookup"><span data-stu-id="b1cbf-215">X-Large</span></span>    | <span data-ttu-id="b1cbf-216">12</span><span class="sxs-lookup"><span data-stu-id="b1cbf-216">1.2</span></span>      | <span data-ttu-id="b1cbf-217">24</span><span class="sxs-lookup"><span data-stu-id="b1cbf-217">2.4</span></span>     | <span data-ttu-id="b1cbf-218">3</span><span class="sxs-lookup"><span data-stu-id="b1cbf-218">3</span></span>                       |
| <span data-ttu-id="b1cbf-219">1.368</span><span class="sxs-lookup"><span data-stu-id="b1cbf-219">1368</span></span>         | <span data-ttu-id="b1cbf-220">Surface Pro 3 (1.368 × 912)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-220">Surface Pro 3 1368x912</span></span>  | <span data-ttu-id="b1cbf-221">XX-Large</span><span class="sxs-lookup"><span data-stu-id="b1cbf-221">XX-Large</span></span>   | <span data-ttu-id="b1cbf-222">12</span><span class="sxs-lookup"><span data-stu-id="b1cbf-222">1.2</span></span>      | <span data-ttu-id="b1cbf-223">32</span><span class="sxs-lookup"><span data-stu-id="b1cbf-223">3.2</span></span>     | <span data-ttu-id="b1cbf-224">3</span><span class="sxs-lookup"><span data-stu-id="b1cbf-224">3</span></span>                       |
| <span data-ttu-id="b1cbf-225">1.440</span><span class="sxs-lookup"><span data-stu-id="b1cbf-225">1440</span></span>         | <span data-ttu-id="b1cbf-226">Surface Pro 4 (1.440 × 960)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-226">Surface Pro 4 1440x960</span></span>  | <span data-ttu-id="b1cbf-227">XX-Large</span><span class="sxs-lookup"><span data-stu-id="b1cbf-227">XX-Large</span></span>   | <span data-ttu-id="b1cbf-228">12</span><span class="sxs-lookup"><span data-stu-id="b1cbf-228">1.2</span></span>      | <span data-ttu-id="b1cbf-229">32</span><span class="sxs-lookup"><span data-stu-id="b1cbf-229">3.2</span></span>     | <span data-ttu-id="b1cbf-230">3</span><span class="sxs-lookup"><span data-stu-id="b1cbf-230">3</span></span>                       |
| <span data-ttu-id="b1cbf-231">1.600</span><span class="sxs-lookup"><span data-stu-id="b1cbf-231">1600</span></span>         | <span data-ttu-id="b1cbf-232">Web (1.600 × 900)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-232">Web 1600x900</span></span>            | <span data-ttu-id="b1cbf-233">XX-Large</span><span class="sxs-lookup"><span data-stu-id="b1cbf-233">XX-Large</span></span>   | <span data-ttu-id="b1cbf-234">12</span><span class="sxs-lookup"><span data-stu-id="b1cbf-234">1.2</span></span>      | <span data-ttu-id="b1cbf-235">32</span><span class="sxs-lookup"><span data-stu-id="b1cbf-235">3.2</span></span>     | <span data-ttu-id="b1cbf-236">3</span><span class="sxs-lookup"><span data-stu-id="b1cbf-236">3</span></span>                       |
| <span data-ttu-id="b1cbf-237">1.920</span><span class="sxs-lookup"><span data-stu-id="b1cbf-237">1920</span></span>         | <span data-ttu-id="b1cbf-238">Web (1.920 x 1.080)</span><span class="sxs-lookup"><span data-stu-id="b1cbf-238">Web 1920x1080</span></span>           | <span data-ttu-id="b1cbf-239">XXX-Large</span><span class="sxs-lookup"><span data-stu-id="b1cbf-239">XXX-Large</span></span>  | <span data-ttu-id="b1cbf-240">12</span><span class="sxs-lookup"><span data-stu-id="b1cbf-240">1.2</span></span>      | <span data-ttu-id="b1cbf-241">32</span><span class="sxs-lookup"><span data-stu-id="b1cbf-241">3.2</span></span>     | <span data-ttu-id="b1cbf-242">3</span><span class="sxs-lookup"><span data-stu-id="b1cbf-242">3</span></span>                       |

<br/>

## <a name="see-also"></a><span data-ttu-id="b1cbf-243">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="b1cbf-243">See also</span></span>

- [<span data-ttu-id="b1cbf-244">Design Toolkit & Assets</span><span class="sxs-lookup"><span data-stu-id="b1cbf-244">Design toolkit and assets</span></span>](https://developer.microsoft.com/de-DE/fabric#/resources)
- [<span data-ttu-id="b1cbf-245">Entwerfen von benutzerfreundlichen SharePoint-Umgebungen</span><span class="sxs-lookup"><span data-stu-id="b1cbf-245">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)


