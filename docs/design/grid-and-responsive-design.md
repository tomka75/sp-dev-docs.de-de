---
title: SharePoint-Raster und reaktionsschnelles Design
ms.date: 9/25/2017
ms.openlocfilehash: 1025e1863d03bad9056d74c87307a7a1e4c8f103
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-grid-and-responsive-design"></a>SharePoint-Raster und reaktionsschnelles Design
 
Reaktionsschnelle Umgebungen werden nahtlos geräteübergreifend skaliert, damit Sie Ihre Inhalte auf einer Vielzahl an verschiedenen Bildschirmgrößen besser anzeigen können. Das reaktionsschnelle Design macht auch das Erstellen mehrerer Versionen Ihrer Websiteseiten überflüssig, um verschiedene Geräte zu unterstützen.  

Der Designleitfaden für reaktionsschnelle Seiten in der SharePoint-Erstellungsumgebung beinhaltet ein reaktionsschnelles Rastersystem, das auf [Office UI Fabric](https://dev.office.com/fabric) basiert. In diesem Artikel werden das zugrunde liegende Seitenrastersystem und die Haltepunkte oder die wichtigsten Bildschirmgrößen beschrieben, bei denen sich das Layout der Seiten ändert. 


![SharePoint-Seite auf mehreren Geräten](../images/design-grid-responsive-overview.png)



## <a name="page-type-grids"></a>Seitentypraster 

Jeder Seitentyp in der SharePoint-Erstellungsumgebung kann eigene Regeln für das Anwenden des reaktionsschnellen Fabric-Rasters haben. Dadurch wird sichergestellt, dass jede Seite gut aussieht, unabhängig davon, für welches Gerät sie entworfen ist, und dass die Umgebung für dieses Gerät optimiert ist. Das grundlegende Raster in der SharePoint-Desktopumgebung ist eine Struktur mit 12 Spalten. Die Anzahl der Spalten und die Bundstegbreite werden basierend auf der Breite des Bildschirms angepasst. 

Die folgenden Abschnitte zeigen die grundlegende Rasterstruktur für verschiedene Arten von SharePoint-Seiten, damit Sie besser verstehen können, wie das Raster zur Unterstützung der Umgebung und Geräteanforderungen angepasst wird.


![Raster mit 12 Spalten – Diagramm](../images/design-grid_diagram.png)



### <a name="team-sites"></a>Teamwebsites

Der Inhaltsbereich für eine Teamwebsite ist auf der linken Seite gesperrt. Teamwebsites weisen einen linken Navigationsbereich auf. Daher respektieren Webparts im Raster und das Reflow-Verhalten den Bereich für die Navigation. Die maximale Breite des Inhaltsbereichs einer Teamwebsite beträgt 1204px und die minimale Größe 320px für Mobilgeräte.

![Teamwebsite](../images/design-grid-team-site.png)

Die folgenden Beispiele zeigen, wie das Raster zwischen den Haupthaltepunkten auf einer Teamwebsite angepasst wird.

#### <a name="small-320-x-568"></a>Klein 320 x 568
Die kleine Größe umfasst einen einzelnen Spaltenbereich in der Mitte, mit Rändern von 20px links und rechts.

![Teamwebsite (kleines Raster)](../images/design-grid-Team-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a>Mittel 480 x 854
Die mittlere Größe umfasst 12 Spalten mit 16px-Bundstegen.

![Teamwebsite (mittleres Raster)](../images/design-grid-Team-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a>Groß 640 x 1024
Die große Größe umfasst 12 Spalten mit  24px-Bundstegen.

![Teamwebsite (großes Raster)](../images/design-grid-Team-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a>XL 1024 x 768
Die XL-Größe umfasst 12 Spalten mit 24px-Bundstegen.

![Teamwebsite (XL-Raster)](../images/design-grid-Team-site-XL-Canvas-24px-gutters.png)

#### <a name="xxl-1366-x-768"></a>XXL 1366 x 768
Die XXL-Größe umfasst 12 Spalten mit 32px-Bundstegen.

![Teamwebsite (XXL-Raster)](../images/design-grid-Team-site–XXL-Canvas-32px-gutters.png)

#### <a name="xxxl-1920-x-1080"></a>XXXL 1920 x 1080
Die XXXL-Größe umfasst 12 Spalten mit 32px-Bundstegen.

![Teamwebsite (XXXL-Raster)](../images/design-grid-Team-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="team-site-multicolumn-pages-and-web-parts"></a>Mehrsprachige Seiten und Webparts auf Teamwebsites
Webparts werden je nach Seitenlayout horizontal skaliert. Das folgende Beispiel zeigt, wie die Größe eines Webparts an den linken Navigationsbereich angepasst wird.

![Mehrsprachige Teamwebsiteseite mit Webparts](../images/design-grid-Team-site-web-parts.png)


### <a name="communication-sites"></a>Kommunikationswebsites

Kommunikationswebsites haben eine obere Navigationsleiste und einen Inhaltsbereich in der Mitte. Die maximale Breite des Inhaltsbereichs einer Kommunikationswebsite beträgt 1204px und die minimale Größe 320px für Mobilgeräte.

![Kommunikationswebsite](../images/design-grid-communication_site.png)

Die folgenden Beispiele zeigen, wie das Raster zwischen den Haupthaltepunkten auf einer Kommunikationswebsite angepasst wird.

#### <a name="small-320-x-568"></a>Klein 320 x 568
Die kleine Größe umfasst einen einzelnen Spaltenbereich in der Mitte, mit Rändern von 20px links und rechts.

![Kommunikationswebsite (kleines Raster)](../images/design-grid-Communication-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a>Mittel 480 x 854
Die mittlere Größe umfasst 12 Spalten mit 16px-Bundstegen.

![Kommunikationswebsite (mittleres Raster)](../images/design-grid-Communication-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a>Groß 640 x 1024
Die große Größe umfasst 12 Spalten mit  24px-Bundstegen.

![Kommunikationswebsite (großes Raster)](../images/design-grid-Communication-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a>XL 1024 x 768
Die XL-Größe umfasst 12 Spalten mit 24px-Bundstegen.

![Kommunikationswebsite (XL-Raster)](../images/design-grid-Communication-site-XL-Canvas-24px-gutters.png)


#### <a name="xxl-1366-x-768"></a>XXL 1366 x 768
Die XXL-Größe umfasst 12 Spalten mit 32px-Bundstegen.

![Kommunikationswebsite (XXL-Raster)](../images/design-grid-Communication-site-XXL-Canvas-32px-gutters-maxwidth-1204.png)


#### <a name="xxxl-1920-x-1080"></a>XXXL 1920 x 1080
Die XXXL-Größe umfasst 12 Spalten mit 32px-Bundstegen.

![Kommunikationswebsite (XXXL-Raster)](../images/design-grid-Communication-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="communication-site-multicolumn-pages-and-web-parts"></a>Mehrsprachige Seiten und Webparts auf Kommunikationswebsite
Webparts werden je nach Seitenlayout horizontal skaliert. Dieses Beispiel zeigt eine Kommunikationswebsite und Webparts für Layouts mit einer, zwei oder drei Spalten.

![Kommunikationswebsite mit mehreren Spalten und Webparts](../images/design-grid-Communciation-site-web-parts.png)



## <a name="breakpoints"></a>Haltepunkte 

Um eine nahtlose Erfahrung zwischen Bildschirmgrößen sicherzustellen, sollte die SharePoint-Benutzeroberfläche Layouts für die folgenden Haltepunktbreiten anpassen: 

- 320
- 1024
- 1366
- 1920
 
Innerhalb dieser Haltepunkte sollten Sie berücksichtigen, wie Ihre Inhalte verschoben werden, wenn die Viewport-Größe für den nächsten Haltepunkt optimiert wird. Beachten Sie, dass dieses Diagramm nur zur Veranschaulichung dient und die Pixel nicht präzise zeigt.


![SharePoint-Diagramm mit Haltepunkten](../images/design-grid-breakpoints.png)


Das reaktionsschnelle Raster für Teamwebsites und Kommunikationswebsites wird beim Wechsel von großen Haltepunkten zu mobilen Haltepunkten angepasst. Hierdurch wird die Website für das Gerät und die Bildschirmgröße optimiert. Die folgende Tabelle beschreibt die Rastergrößen an verschiedenen Haltepunkten basierend auf gängigen Gerätegrößen.



| Fensterbreite | Gerät                  | Haltepunkt | Spalten | Bundsteg | Maximale Anzahl von Spalten pro Bereich |
|--------------|-------------------------|------------|---------|--------|-------------------------|
| 320          | iPhone 5/SE, 320 x 568     | Klein      | 1       | Nicht zutreffend    | 1                       |
| 480          | 6-Zoll-Gerät               | Mittel     | 1       | Nicht zutreffend    | 1                       |
| 640          | 8-Zoll-Gerät               | Groß      | 12      | 16     | 2                       |
| 768          | iPad Hochformat 768x1024  | Groß      | 12      | 24     | 2                       |
| 1024         | iPad Querformat 1024x768 | X-Large    | 12      | 24     | 3                       |
| 1368         | Surface Pro 3 1368x912  | XX-Large   | 12      | 32     | 3                       |
| 1440         | Surface Pro 4 1440x960  | XX-Large   | 12      | 32     | 3                       |
| 1600         | Web 1600x900            | XX-Large   | 12      | 32     | 3                       |
| 1920         | Web 1920x1080           | XXX-Large  | 12      | 32     | 3                       |

## <a name="see-also"></a>Siehe auch

- [Design – Toolkit und Ressourcen](https://developer.microsoft.com/en-us/fabric#/resources)


