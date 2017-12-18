---
title: Erstellen einer externen Liste mithilfe einer OData-Datenquelle in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 601fbfce-a0c6-43dd-8398-540d094c083c
ms.openlocfilehash: a926f2a85678a35e41cb590da67eae1724cdd29c
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="create-an-external-list-using-an-odata-data-source-in-sharepoint"></a>Erstellen einer externen Liste mithilfe einer OData-Datenquelle in SharePoint

In diesem Artikel erfahren Sie, wie Sie externe Listen programmgesteuert erstellen und an OData-basierte externe Inhaltstypen in SharePoint binden. Obwohl Hauptbenutzer oder SharePoint-Administrator eine externe Liste mithilfe von SharePoint Designer 2013 wahrscheinlich erstellen, wird ein Entwickler die Möglichkeit zum Erstellen von externer Listen mithilfe der Tools von deren Handel, Visual Studio 2012 und die Office Developer Tools für Visual Studio 2012 interessiert sein. Wird dadurch mehr Flexibilität zu Funktionen hinzuzufügen und um eine Lösung zu packen, die umfasst Features zur späteren Bereitstellung in eine Business Connectivity Services (BCS) oder viele Umgebungen hosten.
  
    
    


## <a name="prerequisites-for-creating-an-external-list"></a>Voraussetzungen für die Erstellung einer externen Liste
<a name="bkmk_Prereqs"> </a>

Die folgenden Komponenten sind erforderlich, damit eine externe Liste aus einer OData-Quelle zu erstellen:
  
    
    

- Visual Studio 2012
    
  
- SharePoint
    
  
- Office Developer Tools für Visual Studio 2012
    
  
- Ein externen Inhaltstyp basierend auf einer OData-Quelle veröffentlicht: Anweisungen finden Sie unter  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).
    
  
Informationen zum Einrichten einer SharePoint-Entwicklungsumgebung finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

### <a name="core-concepts-for-creating-external-lists"></a>Zentrale Konzepte zum Erstellen von externer Listen

Die folgenden Artikel enthalten Informationen zu SharePoint-Add-Ins und andere Hintergrundinformationen zum Erstellen von externer Listen.
  
    
    

**In Tabelle 1. Kernkonzepte für externe Listen**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [Erste Schritte mit den Business Connectivity Services in SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md) <br/> |Informationen Sie zu Business Connectivity Services und wie Sie externe Daten in SharePoint verfügbar machen können.  <br/> |
| [SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |Erfahren Sie mehr über das neue App-Modell in SharePoint, mit dem Sie Apps, d. h. kleine, einfach zu verwendende Lösungen für Endbenutzer, erstellen können.  <br/> |
| [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx) <br/> |In diesem Artikel erfahren Sie mehr über die verschiedenen Verfahren zum Hosten von SharePoint-Add-Ins.  <br/> |
   

## <a name="create-a-new-external-list"></a>Erstellen Sie eine neue externe Liste
<a name="bkmk_CreateNewVList"> </a>

Die folgenden Verfahren werden gezeigt, wie eine neue externe Liste erstellen, OData-basierten externen Inhaltstyp zu binden und Veröffentlichen in SharePointVisual Studio 2012 verwenden.
  
    
    

> **Hinweis:** Im ersten Schritt wird davon ausgegangen, dass Sie erfolgreich einen externen Inhaltstyp erstellt haben, wie unter  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) beschrieben. 
  
    
    


### <a name="to-add-an-external-list-automatically"></a>So fügen Sie eine externe Liste automatisch hinzu


1. Wenn Sie eine einfache Liste, die angibt, was in Ihren externen Inhaltstyp ist dem Projekt hinzufügen möchten, können Sie die Visual Studio 2012 automatische Generierung von Tools verwenden. Die Liste wird erstellt, wenn der externe Inhaltstyp erstellt wird. Wenn Sie das Kontrollkästchen **Erstellen Listeninstanzen für die ausgewählten Datenentitäten (mit Ausnahme von Dienstvorgänge)** gefunden auswählen im zweite Schritt des automatische Generierung von Prozess (Wählen Sie im Schritt Datenentitäten), den Assistenten die XML-Deklaration erstellt und hinzufügen neue externe Inhaltstypen für jede Entität, die Sie ausgewählt haben.
    
  
2. Drücken Sie F5 zum Bereitstellen des Projekts und die neue Liste wird auch bereitgestellt.
    
  
Zu Testzwecken sollten Sie die Datei AppManifest.xml ändern, sodass die Startseite der app die Liste ist, den, die Sie gerade erstellt haben. 
  
    
    

### <a name="to-modify-the-appmanifestxml-file"></a>So ändern Sie die Datei AppManifest.xml


1. Öffnen Sie die Datei „Appmanifest.xml“ im XML-Editor.
    
  
2. Suchen Sie das \<StartPage\>-Tag.
    
  
3. Ändern Sie den Wert zu `~appWebUrl/Lists/Employees`.
    
  
4. Speichern Sie Ihre Änderungen.
    
  

### <a name="to-publish-the-project"></a>Um das Projekt zu veröffentlichen


- Drücken Sie F5, um das Projekt und die externe Liste bereitstellen. 
    
    Öffnen Sie einen Webbrowser, und navigieren Sie zu der neuen Liste, die Sie erstellt haben.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bkmk_AdditionalResources"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [So geht's: Erstellen einer einfachen automatisch gehosteten App für SharePoint](http://msdn.microsoft.com/library/0572894d-c437-4b7d-8ac6-8405496e2145%28Office.15%29.aspx)
    
  
-  [Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  

