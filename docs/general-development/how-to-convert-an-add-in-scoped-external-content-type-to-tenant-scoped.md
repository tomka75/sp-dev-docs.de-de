---
title: Konvertieren eines externen Inhaltstyps auf Add-In-Ebene auf Mandantenbereich
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 35c5d670-e402-4641-b3c5-6f61ae1ec69b
ms.openlocfilehash: a6790c1f756ab06cb9e00efe7eeac2675eb5bc85
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="convert-an-add-in-scoped-external-content-type-to-tenant-scoped"></a>Konvertieren eines externen Inhaltstyps auf Add-In-Ebene auf Mandantenbereich

Informationen Sie zum Erstellen eines OData-basierten externen Inhaltstyps mithilfe von Visual Studio 2012 automatische Generierung Tools und importieren es in die Business Connectivity Services (BCS)-Metadaten gespeichert, damit sie über eine gesamte Mandanten Workspace verwendet werden kann. BDC-Modelle werden komplexe XML-Definitionen von einer externen Datenquelle. Sie werden beim Definieren der externer Inhaltstypen für BCS verwendet. Sie sind sehr schwer zu manuell erstellen, damit Tools erstellt wurden, wenn die Dateien mit Visual Studio 2012 und Office Developer Tools für Visual Studio 2012 automatisch generiert werden soll. Verwendung dieser Tools, können Sie ein App-Paket mit Visual Studio-Veröffentlichung erstellen, und öffnen Sie das Paket zum Extrahieren der Modelldatei.
  
    
    


## <a name="extract-the-bdc-model-file-from-a-visual-studio-add-in-package"></a>Extrahieren Sie die BDC-Modelldatei aus einem Visual Studio-add-in-Paket

Die folgenden Schritte zeigen, wie den OData-basierten externen Inhaltstyp erstellen und dann in den BCS-Metadatenspeicher importieren, so, dass sie über eine gesamte Mandanten Arbeitsbereich verwendet werden kann.
  
    
    

### <a name="to-create-a-bdc-model-file-from-an-odata-source"></a>Erstellen Sie eine BDC-Modelldatei aus einer OData-Quelle


1. Erstellen Sie in Visual Studio 2012 ein Projekt **-Add-in für SharePoint**.
    
  
2. Geben Sie die Add-in-Einstellungen, einschließlich der Add-in-Name die URL der Website für das Debuggen des Add-Ins und wie Sie das Add-in ( **automatisch gehostete**, **vom Anbieter gehostete** oder **SharePoint-Hosting** ) hosten möchten. Weitere Informationen finden Sie unter [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).
    
  
3. Wählen Sie auf **Fertig stellen**, um die app zu erstellen.
    
  
4. Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.
    
    Einen Assistenten, der können Sie die ausgewählten Datenquelle suchen und erstellen Sie das BDC-Modell, wird gestartet.
    
  
5. Geben Sie auf der Seite **Set OData Source** die URL des OData-Diensts, die Sie mit verbinden möchten. Die URL sollte etwa wie folgt aussehen: `http://services.odata.org/Northwind/Northwind.svc/`.
    
    Geben Sie einen Namen für die OData-Quelle an.
    
    > **Hinweis:** In diesem Beispiel verwenden Sie den Northwind-Dienst, der in der Hersteller-Liste auf der  [OpenData Protocol-Website](http://www.odata.org) befindet. 
6. Eine Liste wird angezeigt, mit Datenentitäten, die vom OData Service verfügbar gemacht werden. Wählen Sie eine oder mehrere Entitäten, und wählen Sie **Fertig stellen**.
    
  

### <a name="to-deploy-the-add-in-scoped-external-content-type-as-an-add-in-package"></a>Den Add-in-bezogenen externen Inhaltstyp als ein Add-in-Paket bereitgestellt


1. Wählen Sie im Visual Studio, klicken Sie im Menü **Erstellen** auf **Veröffentlichen**.
    
  
2. Nennen Sie das Paket, geben Sie den Speichervorgang Speicherort auf Ihrem lokalen Festplatte Laufwerk, und wählen Sie **Fertig stellen**.
    
  

### <a name="to-extract-the-model-file-from-the-app-package"></a>Extrahiert die Modelldatei aus dem App-Paket


1. Öffnen Sie den Ordner, in dem das App-Paket erstellt wird.
    
  
2.  Ändern Sie die Erweiterung von App inZIP.
    
  
3. Extrahieren Sie das ZIP-Paket in einen lokalen Ordner.
    
  
4. Öffnen Sie den extrahierten Ordner aus, um die WSP-Datei zu suchen.
    
  
5. Verschieben Sie die WSP-Datei an einen anderen Speicherort.
    
  
6. Ändern Sie die WSP-Dateinamenerweiterung für diese Datei in CAB.
    
  
7. Öffnen Sie die CAB-Datei, und finden Sie die Datei Bdcmodel.bdcm.
    
  
8. Speichern Sie die Bdcmodel.bdcm-Datei an einen anderen Speicherort.
    
  

### <a name="to-import-the-model-file-using-sharepoint-central-administration-pages"></a>So importieren Sie die Modelldatei mithilfe der SharePoint-Zentraladministrationsseiten


1. Öffnen Sie SharePoint Online oder SharePoint lokalen Zentraladministrationsseiten.
    
  
2. Wählen Sie **Verwalten Applications dienen**.
    
  
3. Wählen Sie die **Business Data Connectivity-Dienst**.
    
  
4. Wählen Sie den **Import**-Link auf der Serverkomponente.
    
  
5. Wählen Sie die Schaltfläche **Durchsuchen**, um den Speicherort angeben, in dem Sie die bdcm-Datei extrahiert haben.
    
  
6. Lassen Sie die Standardeinstellungen, und wählen Sie dann auf **Importieren**.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Vorgehensweise: erstellen ein Add-in-bezogenen externes Inhaltstyps in SharePoint](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [Erste Schritte mit den Business Connectivity Services in SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Open Data Protocol](http://www.odata.org)
    
  

  
    
    

