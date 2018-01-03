---
title: "Erstellen von wiederverwendbaren Komponenten für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bb4467e2-57f0-4cf1-91b8-4d3d8d2358cb
ms.openlocfilehash: 997f882794dfef4ef9fa3173ee61fd76c6c84d3e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="build-reusable-components-for-sharepoint"></a>Erstellen von wiederverwendbaren Komponenten für SharePoint
Hier lernen Sie einige der wichtigsten wiederverwendbaren Komponenten, die in SharePoint, einschließlich der Webparts, Workflows, benutzerdefinierte Listen und erstellt werden können.
## <a name="reusable-components-in-sharepoint"></a>Wiederverwendbare Komponenten in SharePoint
<a name="SP15Reusecomp_Reusable"> </a>

SharePoint verwenden, können Sie eine Vielzahl von Komponenten, beispielsweise Listen, Webparts und Inhaltstypen, die Sie in verschiedenen apps, Websites und Lösungen wiederverwenden können erstellen. In diesem Abschnitt werden einige der am häufigsten verwendeten wiederverwendbaren Komponenten, die Sie in SharePoint erstellen können. Zukünftige Updates auf diese Dokumentation enthält Informationen zu weiteren Komponenten, die Sie erstellen können.
  
    
> [!NOTE]
> Es gibt einige Beschränkungen, welche Komponenten Sie in SharePoint-Add-Ins verwenden können. Weitere Informationen finden Sie unter [Hostwebsites, Add-In-Websites und SharePoint-Komponenten in SharePoint]((http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx)). 
  
    
    


- **Webparts** sind die am häufigsten verwendeten Möglichkeit zum Erweitern von SharePoint. Informationen zum Erstellen von Webparts ist eine hervorragende Möglichkeit zum Starten des SharePoint-Entwicklung. Weitere Informationen finden Sie unter [SharePoint Developer Building Blocks: Technologies for Creating SharePoint Applications]((http://msdn.microsoft.com/library/138422cf-c140-466a-bcd8-cacba51ef886%28Office.15%29.aspx)#bb2_WebParts).
    
  
- **Benutzerdefinierte Listen** in SharePoint-Websites bieten Speicherorte zum Speichern von Daten. Bearbeiten von Daten in SharePoint-Listen ist eine häufig verwendete Methode. Listen können Sie Daten enthalten, die die programmgesteuert zugegriffen werden. Weitere Informationen finden Sie unter [Baustein: Listen und Dokumentbibliotheken]((http://msdn.microsoft.com/library/16da8f64-f53b-4490-8636-db0e4d7a6912%28Office.15%29.aspx)).
    
  
- **Workflows** können Sie kodifiziert und Standardisieren von Geschäftsprozessen und sind die wesentlichen Tools für die Implementierung von bestimmten Szenarien. Weitere Informationen finden Sie unter [Workflows in SharePoint](workflows-in-sharepoint.md).
    
  
- **Externe Inhaltstypen** stellen Daten außerhalb der SharePoint-Bereitstellung der SharePoint-Anwendung zur Verfügung. Weitere Informationen finden Sie unter [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md).
    
  
- Sie können einen **Inhaltstyp** definieren, die einen Prototyp eines Listenelements ist. Wenn Sie eine Liste von Inhaltstypen verwenden, können Sie die Liste definieren, damit sie nur Elemente mit einem Inhaltstyp enthält, oder Sie können angeben, dass es Elemente eines mehrere Inhaltstypen enthalten kann. Weitere Informationen finden Sie unter [Einführung in Inhaltstypen]((http://msdn.microsoft.com/library/a345a6c5-7031-46ab-a2c2-37bedc3012f4%28Office.15%29.aspx)).
    
  
- **Spaltentypen** und **Feldtypen** können Sie rich-Metadaten von standardisierten Feldern und Spalten in SharePoint-Listen zu definieren. Sie können eine Websitespalte (in einer Websitespaltenkatalog) für einen bestimmten Datentyp definieren, die Sie innerhalb der gesamten Website verwenden können. Diese gleicht definierende Domänen in Datenbankentwurf Schema. Hiermit können Sie sicherstellen, dass Spalten in mehreren Listen auf den gleichen Wert Speicherplatz verwenden. Weitere Informationen finden Sie unter [Custom Field Types]((http://msdn.microsoft.com/library/1345b345-226d-443a-918f-af123a3c7b13%28Office.15%29.aspx)).
    
  
- **Ereignisempfänger** können Sie Ereignishandler schreiben, die aufgerufen werden, wenn beispielsweise Benutzer hinzufügen, löschen oder Ändern von Elementen in Listen oder SharePoint-Dokumentbibliotheken. Weitere Informationen finden Sie unter [Baustein: Ereignisbehandlung]((http://msdn.microsoft.com/library/212cf488-43cb-4250-82d5-3b962b6e56e6%28Office.15%29.aspx)).
    
  
- **Remote-Ereignisempfänger** bieten eine Möglichkeit, externe Systeme der SharePoint-Ereignisse zu benachrichtigen. Sie können angeben, dass die Eigenschaften Endpunkt und Ereignis aufrufen, wenn ein Ereignis eintritt. Weitere Informationen finden Sie unter [Erstellen eines Remoteereignisempfängers in Add-Ins für SharePoint]((http://msdn.microsoft.com/library/628c6103-52f9-4d85-9464-4a6862b36640%28Office.15%29.aspx)).
    
  

## <a name="see-also"></a>Siehe auch
<a name="SP15Reusecomp_AddRes"> </a>


-  [Programmiermodelle in SharePoint](programming-models-in-sharepoint.md)
    
  
-  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md)
    
  
-  [Übersicht über die SharePoint-Entwicklung](sharepoint-development-overview.md)
    
  
-  [Hostwebsites, Add-In-Websites und SharePoint-Komponenten in SharePoint]((http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx))
    
  
-  [Bausteine von SharePoint Foundation 2010]((http://msdn.microsoft.com/library/0d7f5106-dcbd-442e-9907-d28a323bbe11%28Office.15%29.aspx))
    
  
-  [SharePoint-Entwicklerbausteine: Technologien zum Erstellen von SharePoint-Anwendungen (Teil 1 von 2)]((http://msdn.microsoft.com/library/7ef04158-d149-4301-ab91-4617677eefc4%28Office.15%29.aspx))
    
  
-  [SharePoint-Entwicklerbausteine: Technologien zum Erstellen von SharePoint-Anwendungen (Teil 2 von 2)]((http://msdn.microsoft.com/library/138422cf-c140-466a-bcd8-cacba51ef886%28Office.15%29.aspx))
    
  

