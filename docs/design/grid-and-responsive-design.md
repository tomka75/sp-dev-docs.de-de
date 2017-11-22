---
title: Rasterdesigns und dynamische Designs in SharePoint
ms.date: 9/25/2017
ms.openlocfilehash: 1025e1863d03bad9056d74c87307a7a1e4c8f103
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-grid-and-responsive-design"></a>Rasterdesigns und dynamische Designs in SharePoint
 
Dynamische Benutzeroberflächen skalieren nahtlos für verschiedene Geräte, sodass Ihre Inhalte passend für die jeweilige Bildschirmgröße dargestellt werden. Dank dynamischer Designs entfällt zudem die Notwendigkeit, für unterschiedliche Geräte jeweils eigene Versionen der Seiten auf Ihrer Website zu erstellen.  

Die Designrichtlinien für dynamische Seiten in der SharePoint-Erstellungsumgebung beinhalten ein dynamisches Rastersystem, das auf [Office UI Fabric](https://dev.office.com/fabric) basiert. In diesem Artikel werden das zugrunde liegende Seitenrastersystem und die Haltepunkte beschrieben, d. h. die Bildschirmgrößen, bei denen das Seitenlayout angepasst wird. 


![SharePoint-Seite auf verschiedenen Geräten](../images/design-grid-responsive-overview.png)



## <a name="page-type-grids"></a>Seitentypraster 

Für jeden Seitentyp in der SharePoint-Erstellungsumgebung lassen sich eigene Regeln für die Anwendung des dynamischen Fabric-Rasters festlegen. Dadurch wird sichergestellt, dass jede Seite optimal dargestellt wird, unabhängig davon, für welches Gerät sie entworfen ist, und dass die Oberfläche für das jeweilige Gerät optimiert ist. Das grundlegende Raster für SharePoint-Desktopoberflächen ist eine Struktur mit 12 Spalten. Die Anzahl der Spalten und die Bundstegbreite werden basierend auf der Breite des Bildschirms angepasst. 

In den folgenden Abschnitt zeigen wir Ihnen, wie die grundlegende Rasterstruktur auf verschiedene Typen von SharePoint-Seiten angewendet wird. So können Sie sich einen Überblick darüber verschaffen, wie sich das Raster an die jeweiligen Oberflächen- und Geräteanforderungen anpasst.


![Abbildung eines Rasters mit 12 Spalten](../images/design-grid_diagram.png)



### <a name="team-sites"></a>Teamwebsites

Der Inhaltsbereich einer Teamwebsite ist linksbündig fixiert. Der Navigationsbereich befindet sich auf Teamwebsites links. Die Bereichswebparts belegen daher das Raster, und beim dynamischen Umbruch wird der für die Navigation reservierte Bereich berücksichtigt. Die maximale Breite des Inhaltsbereichs einer Teamwebsite beträgt 1.204 Pixel, die minimale Größe 320 Pixel für eine optimale Darstellung auf Mobilgeräten.

![Teamwebsite](../images/design-grid-team-site.png)

Die folgenden Beispiele demonstrieren, wie das Raster an den jeweiligen Haupthaltepunkten auf einer Teamwebsite angepasst wird.

#### <a name="small-320-x-568"></a>Klein (320 × 568)
Das kleine Raster besteht aus einem einzelnen zentrierten Spaltenbereich mit einem Rand von 20 Pixel links und rechts.

![Teamwebsite (kleines Raster)](../images/design-grid-Team-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a>Mittel (480 × 854)
Das mittelgroße Raster besteht aus 12 Spalten mit Bundstegen von je 16 Pixel.

![Teamwebsite (mittelgroßes Raster)](../images/design-grid-Team-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a>Groß (640 × 1.024)
Das große Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.

![Teamwebsite (großes Raster)](../images/design-grid-Team-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a>XL (1.024 × 768)
Das XL-Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.

![Teamwebsite (XL-Raster)](../images/design-grid-Team-site-XL-Canvas-24px-gutters.png)

#### <a name="xxl-1366-x-768"></a>XXL (1.366 × 768)
Das XXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.

![Teamwebsite (XXL-Raster)](../images/design-grid-Team-site–XXL-Canvas-32px-gutters.png)

#### <a name="xxxl-1920-x-1080"></a>XXXL (1.920 × 1.080)
Das XXXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.

![Teamwebsite (XXXL-Raster)](../images/design-grid-Team-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="team-site-multicolumn-pages-and-web-parts"></a>Teamwebsite mit mehrspaltigen Seiten und Webparts
Webparts werden je nach Seitenlayout horizontal skaliert. Das folgende Beispiel veranschaulicht, wie die Größe eines Webparts an die Größe des linken Navigationsbereichs angepasst wird.

![Teamwebsite mit mehrspaltiger Seite und Webparts](../images/design-grid-Team-site-web-parts.png)


### <a name="communication-sites"></a>Kommunikationswebsites

Kommunikationswebsites verfügen über eine Navigationsleiste oben auf der Seite sowie einen zentrierten Inhaltsbereich. Die maximale Breite des Inhaltsbereichs einer Kommunikationswebsite beträgt 1.204 Pixel, die Mindestgröße 320 Pixel für eine optimale Darstellung auf Mobilgeräten.

![Kommunikationswebsite](../images/design-grid-communication_site.png)

Die folgenden Beispiele zeigen, wie das Raster an den jeweiligen Haupthaltepunkten auf einer Kommunikationswebsite angepasst wird.

#### <a name="small-320-x-568"></a>Klein (320 × 568)
Das kleine Raster besteht aus einem einzelnen zentrierten Spaltenbereich mit einem Rand von 20 Pixel links und rechts.

![Kommunikationswebsite (kleines Raster)](../images/design-grid-Communication-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a>Mittel (480 × 854)
Das mittelgroße Raster besteht aus 12 Spalten mit Bundstegen von je 16 Pixel.

![Kommunikationswebsite (mittelgroßes Raster)](../images/design-grid-Communication-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a>Groß (640 × 1.024)
Das große Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.

![Kommunikationswebsite (großes Raster)](../images/design-grid-Communication-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a>XL (1.024 × 768)
Das XL-Raster besteht aus 12 Spalten mit Bundstegen von je 24 Pixel.

![Kommunikationswebsite (XL-Raster)](../images/design-grid-Communication-site-XL-Canvas-24px-gutters.png)


#### <a name="xxl-1366-x-768"></a>XXL (1.366 × 768)
Das XXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.

![Kommunikationswebsite (XXL-Raster)](../images/design-grid-Communication-site-XXL-Canvas-32px-gutters-maxwidth-1204.png)


#### <a name="xxxl-1920-x-1080"></a>XXXL (1.920 × 1.080)
Das XXXL-Raster besteht aus 12 Spalten mit Bundstegen von je 32 Pixel.

![Kommunikationswebsite (XXXL-Raster)](../images/design-grid-Communication-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="communication-site-multicolumn-pages-and-web-parts"></a>Kommunikationswebsite mit mehrspaltigen Seiten und Webparts
Webparts werden je nach Seitenlayout horizontal skaliert. Das Beispiel unten veranschaulicht eine Kommunikationswebsite und Webparts in einem Layout mit einer bis drei Spalten.

![Kommunikationswebsite mit mehreren Spalten und Webparts](../images/design-grid-Communciation-site-web-parts.png)



## <a name="breakpoints"></a>Haltepunkte 

Damit die Oberfläche sich nahtlos an unterschiedliche Bildschirmgrößen anpasst, sollte die SharePoint-UI das Layout an den folgenden Haltepunktbreiten anpassen: 

- 320
- 1.024
- 1.366
- 1.920
 
Dabei sollten Sie bedenken, wie Ihre Inhalte sich zwischen diesen Haltepunkten verändern, wenn die Größe des Darstellungsbereichs an den nächstgelegenen Haltepunkt angepasst wird. Die Abbildung unten dient lediglich der Veranschaulichung und ist nicht pixelgenau.


![SharePoint-Diagramm mit Haltepunkten](../images/design-grid-breakpoints.png)


Das dynamische Raster für Teamwebsites und Kommunikationswebsites passt sich bei der Umstellung von einem der großen Haltepunkte an einen Mobilgeräte-Haltepunkt an. Dadurch wird die Website optimal an das jeweilige Geräte und die jeweilige Bildschirmgröße angepasst. In der folgenden Tabelle finden Sie einen Überblick über die Rastergrößen an verschiedenen Haltepunkten, basierend auf den Bildschirmgrößen gängiger Geräte.



| Fensterbreite | Gerät                  | Haltepunkt | Spalten | Bundsteg | Maximale Anzahl von Spalten pro Abschnitt |
|--------------|-------------------------|------------|---------|--------|-------------------------|
| 320          | iPhone 5/SE (320 ×568)     | Small      | 1       | -    | 1                       |
| 480          | 6-Zoll-Gerät               | Medium     | 1       | -    | 1                       |
| 640          | 8-Zoll-Gerät               | Large      | 12      | 16     | 2                       |
| 768          | iPad im Hochformat (768 × 1.024)  | Large      | 12      | 24     | 2                       |
| 1.024         | iPad im Querformat (1.024 ×768) | X-Large    | 12      | 24     | 3                       |
| 1.368         | Surface Pro 3 (1.368 × 912)  | XX-Large   | 12      | 32     | 3                       |
| 1.440         | Surface Pro 4 (1.440 × 960)  | XX-Large   | 12      | 32     | 3                       |
| 1.600         | Web (1.600 × 900)            | XX-Large   | 12      | 32     | 3                       |
| 1.920         | Web (1.920 x 1.080)           | XXX-Large  | 12      | 32     | 3                       |

## <a name="see-also"></a>Weitere Artikel

- [Design Toolkit & Assets](https://developer.microsoft.com/de-DE/fabric#/resources)


