---
title: Durchsuchen von neuen Inhalten mit der SharePoint-Suche
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2a3a7d23-775a-4d95-9066-ebbd18c92ad4
ms.openlocfilehash: b8798b513c8db47c66c6754f72edb805fc724ce0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="searching-new-content-with-sharepoint-search"></a>Durchsuchen von neuen Inhalten mit der SharePoint-Suche
Erfahren Sie, wie Sie Inhalte für Benutzer für die Suche in SharePoint verfügbar machen.
## <a name="making-content-available-for-search-in-sharepoint"></a>Verfügbarmachen von Inhalt für die Suche in SharePoint

Suche in SharePoint stellt zwei Ansätze für die Verarbeitung von Abfragen zum Zurückgeben von Suchergebnissen bereit: die Sammelsuche und das Durchforsten von Inhalten.
  
    
    
 **Sammelsuche** Bei diesem Ansatz werden Suchergebnisse für Inhalte zurückgegeben, die nicht von Ihrem Suchserver durchforstet werden. Die Abfrage wird an ein externes Inhaltsrepository weitergeleitet, in dem sie von der Suchmaschine dieses Repositorys verarbeitet wird. Die Suchmaschine des Repositorys gibt dann die Ergebnisse an den Suchserver zurück. Der Suchserver formatiert und rendert die Ergebnisse aus dem externen Repository für die Anzeige auf der Suchergebnisseite. Dieser Ansatz bietet folgende Vorteile:
  
    
    

- Sie benötigen keine zusätzlichen kapazitätsanforderungen für den Inhaltsindex, wie der Inhalt von Suche in SharePoint nicht durchforstet wird.
    
  
- Sie können die vorhandene Suchmaschine eines Repositorys nutzen. Sie können z. B. einen Verbund mit einer Internetsuchmaschine herstellen, um das Internet zu durchsuchen.
    
  
- Sie können die Suchmaschine des Inhaltsrepositorys für die spezielle Inhaltsgruppe des Repositorys optimieren, was möglicherweise eine bessere Suchleistung für die Inhaltsgruppe bereitstellt.
    
  
- Sie können auf Repositorys zugreifen, die gegen Durchforstungen abgesichert sind, auf die aber mit Suchabfragen zugegriffen werden kann.
    
  
 **Durchforsten von Inhalten** Bei diesem Ansatz werden Ergebnisse vom Inhaltsindex der Suchdienstanwendung basierend auf der Abfrage des Benutzers zurückgegeben. Der Inhaltsindex enthält Inhalte, die von der Suchdienstanwendung durchforstet werden, und umfasst Textinhalte und Metadaten für jedes Inhaltselement. Dieser Ansatz ermöglicht Folgendes:
  
    
    

- Sie können Suchergebnisse nach Relevanz sortieren.
    
  
- Sie können steuern, wie häufig der Inhaltsindex aktualisiert wird.
    
  
- Sie können angeben, welche Metadaten durchforstet werden.
    
  
- Sie können einen einzelnen Sicherungsvorgang für durchforstete Inhalte durchführen.
    
  

## <a name="in-this-section"></a>Inhalt dieses Abschnitts


-  [Connector Framework für die Suche in SharePoint](search-connector-framework-in-sharepoint.md)
    
  -  [Optimieren der BDC-Modelldatei für die Suche in SharePoint](enhancing-the-bdc-model-file-for-search-in-sharepoint.md)
    
  
  -  [Vorgehensweise: durchforsten zugeordneter externe Inhaltstypen in SharePoint](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
  -  [Vorgehensweise: durchforsten binary large Objects () in SharePoint](how-to-crawl-binary-large-objects-blobs-in-sharepoint.md)
    
  
  -  [Vorgehensweise: durchforsten zugeordneter externe Inhaltstypen in SharePoint](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
  -  [Vorgehensweise: Konfigurieren der Sicherheit auf Elementebene in SharePoint](how-to-configure-item-level-security-in-sharepoint.md)
    
  

