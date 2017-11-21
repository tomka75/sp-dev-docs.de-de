---
title: Vorgehensweise Anwenden einer Gestaltungsvorlage auf eine Website in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 04861390-84d5-40ea-b0db-6c0748eff196
ms.openlocfilehash: a015d4d276933219a548693e11e6e67671cef983
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-apply-a-master-page-to-a-site-in-sharepoint"></a>Vorgehensweise: Anwenden einer Gestaltungsvorlage auf eine Website in SharePoint
Erfahren Sie, wie Sie eine Gestaltungsvorlage zu einer SharePoint-Website zuordnen.
## <a name="mapping-a-master-page-to-a-site"></a>Zuordnen einer Gestaltungsvorlage zu einer Website

In SharePoint definiert eine Gestaltungsvorlage die gemeinsam genutzten Rahmenelemente, z. B. den Chrom, für alle Seiten Ihrer Website. Nach der Erstellung der Gestaltungsvorlage kann diese einer Website zugeordnet werden. Dies kann für alle Veröffentlichungsseiten erfolgen, die für alle Benutzer vorgesehen sind, aber auch für die administrativen Seiten, die zur Verwaltung der Website verwendet werden. Wenn Sie die untergeordnete Website einer übergeordneten Website konfigurieren, können Sie alternativ die Gestaltungsvorlage der übergeordneten Website übernehmen. In diesem Artikel sind die Schritte zum Zuordnen einer erstellten Gestaltungsvorlage zu einer Website, zum Übernehmen der Gestaltungsvorlage von einer übergeordneten Website, oder zum Zuordnen einer Gestaltungsseite zu einem bestimmten Gerätekanal enthalten.
  
    
    

> **Hinweis:** Weitere Informationen zum Entwurfs-Manager und zu Gestaltungsvorlagen finden Sie unter [Übersicht über den Entwurfs-Manager in SharePoint](overview-of-design-manager-in-sharepoint.md). Weitere Informationen zum Erstellen von Gerätekanälen finden Sie unter [SharePoint-Entwurfs-Manager-Gerätekanäle](sharepoint-design-manager-device-channels.md). 
  
    
    


### <a name="to-map-a-master-page-to-a-sharepoint-site"></a>So ordnen Sie eine Gestaltungsvorlage einer SharePoint-Website zu


1.  Klicken Sie in den **Websiteeinstellungen** für die vorgesehene Website im Abschnitt **Aussehen und Verhalten** auf **Gestaltungsvorlage**.
    
    > **Hinweis:** Wenn der Link **Gestaltungsvorlage** nicht vorhanden ist, müssen Sie das Veröffentlichungsfeature mit den folgenden Schritten aktivieren. Navigieren Sie zu **Websiteeinstellungen | Websitesammlungsverwaltung | Websitesammlungsfeatures**. Scrollen Sie nach unten zum Feature **SharePoint Server-Veröffentlichungsinfrastruktur**, und klicken Sie auf **Aktivieren**. 
2. Wählen Sie in den **Einstellungen für die Gestaltungsvorlage der Website** eine der beiden Optionen für die Abschnitte **Gestaltungsvorlage der Website** oder **Systemgestaltungsvorlage** aus:
    
  - **Gestaltungsvorlage für die Website von der übergeordneten Website erben**: Wählen Sie diese Option aus, wenn Sie eine untergeordnete SharePoint-Website konfigurieren und die Gestaltungsvorlage der übergeordneten Website verwenden möchten.
    
    > **Hinweis: ** Diese Option ist nicht verfügbar, wenn Sie auf der übergeordneten Website der obersten Ebene arbeiten. 
  - **Eine Gestaltungsvorlage für die Website und alle erbenden Websites angeben**: Wählen Sie diese Option, wenn Sie eine bestimmte Gestaltungsvorlage zur Website oder eine bestimmte Gestaltungsvorlage für administrative Seiten zuordnen möchten. Es ist das Dropdownfeld **Standard** oder **Alle Kanäle** in Abhängigkeit von Ihrer Website oder Systemkonfiguration verfügbar, daher können Sie eine bestimmte Gestaltungsvorlage auswählen, die im Gestaltungsvorlagenkatalog enthalten ist. Wählen Sie die gewünschte Gestaltungsvorlage aus dem Dropdownfeld aus.
    
    > **Hinweis:** Wenn Gerätekanäle konfiguriert sind, stehen weitere Dropdownfelder für zusätzliche Zuordnungsoptionen für Gestaltungsvorlagen zur Verfügung. 
3. Wählen Sie **OK** aus.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
    
  
-  [Übersicht über den Entwurfs-Manager in SharePoint](overview-of-design-manager-in-sharepoint.md)
    
  
-  [Neuerung bei SharePoint-Websiteentwicklung](what-s-new-with-sharepoint-site-development.md)
    
  
