---
title: Externe Inhaltstypen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 11d7adb5-5388-4517-ae03-beb7be1c6981
ms.openlocfilehash: beac2fcaea11c5998a2b8a96291e45dc1ae5313e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="external-content-types-in-sharepoint"></a>Externe Inhaltstypen in SharePoint
Erfahren Sie, welche Möglichkeiten Ihnen externe Inhaltstypen bieten, und was Sie benötigen, um mit deren Erstellung in SharePoint zu beginnen.
## <a name="what-is-an-external-content-type"></a>Was ist ein externer Inhaltstyp?
<a name="SP15ectoverview_what"> </a>

Der externe Inhaltstyp ist ein zentrales Konzept von Business Connectivity Services (BCS). Externe Inhaltstypen werden für sämtliche Funktionen und Dienste verwendet, die von BCS geboten werden, und stellen wiederverwendbare Metadatenbeschreibungen von Konnektivitätsinformationen und Datendefinitionen sowie deren Verhalten dar, die Sie auf eine bestimmte Kategorie externer Daten anwenden möchten.
  
    
    
Mit externen Inhaltstypen können Sie die Metadaten und Verhaltensweisen einer Geschäftsentität (etwa eines Kunden oder einer Bestellung) an einem zentralen Ort verwalten und wiederverwenden, und Benutzer können mit diesen externen Daten und Prozessen auf sinnvollere Weise interagieren.
  
    
    
Hier einige der Vorteile der Verwendung externer Inhaltstypen:
  
    
    

- **Wiederverwendbarkeit:** Ein externer Inhaltstyp ist eine wiederverwendbare Datendefinition einer Geschäftsentität. Nachdem Sie sie erstellt haben, können Sie sie mit jeder der Präsentationsfeatures in BCS verwenden, um die Interaktion mit externen Daten benutzerfreundlich zu gestalten.
    
  
- **Kapseln von Komplexitäten externer Systeme:** Externe Inhaltstypen ermöglichen Information Workern, Geschäftslösungen zusammenzustellen, ohne die Komplexitäten der externen Systeme, wie Konnektivitätsinformationen und Codeschnittstellen, berücksichtigen zu müssen. Sobald ein Benutzer einen externen Inhaltstyp erstellt hat, steht dieser allen Benutzern zur beliebigen Verwendung zur Verfügung (solange sie die Berechtigungen zum Durchführen dieses Vorgangs sowie Zugriff auf die externen Daten besitzen). Der Benutzer muss allerdings nichts über den Speicherort der externen Daten oder die Verbindung zu diesen wissen.
    
  
- **Bereitstellen von integriertem Office- und SharePoint-Verhalten:** Externe Inhaltstypen stellen für externe Daten und Services Office-elementartige Verhaltensweisen (wie Kontakte, Aufgaben, Kalender Outlook, Dokumente in Word und Listen in SharePoint Workspace), SharePoint-Verhaltensweisen (wie Listen, Webparts und Profilseiten) und Funktionen (wie die Fähigkeit zur Offlinesuche oder -arbeit) bereit. Dadurch können Benutzer in ihren vertrauten Arbeitsumgebungen arbeiten, ohne nach Daten suchen oder andere (und proprietäre) Benutzeroberflächen verwenden zu müssen.
    
  
- **Unterstützung bei der Bereitstellung von sichererem Zugriff:** Externe Inhaltstypen halten die vom externen System und SharePoint verwendeten Sicherheitsmechanismen ein. Durch die Konfiguration von Sicherheitseinstellungen in SharePoint können Sie genau steuern, wer auf welche Daten zugreift.
    
  
- **Vereinfachen der Verwaltung:** Da externe Inhaltstypen einmal erstellt und von mehreren Lösungen in verschiedenen Szenarios verwendet werden können, können Sie sie leicht verwalten. So können Sie z. B. deren Zugriffsberechtigungen sowie deren Verbindungs- und Datendefinitionen an einem zentralen Ort verwalten.
    
  
- **Ermöglichen einer externen Datensuche:** Sie können von einem Intranetportal aus SharePoint Server-Suchdienst verwenden, um Informationen über einen bestimmten externen Inhaltstyp wie einen Kunden nachzuschlagen. SharePoint Server-Suchdienst ruft die Daten direkt aus dem externen System ab. Daher können Benutzer die Informationen erhalten, die sie benötigen, ohne eine Genehmigung einzuholen oder eine separate Anwendung zu installieren.
    
  
- **Ermöglichen von Offlinearbeit:** Sie können externe Inhaltstypen in Outlook 2013 offline verwenden. Business Connectivity Services (BCS) bietet umfangreiche Features für Caching und die Offlinearbeit und unterstützt cachebasierte Vorgänge. Benutzer können externe Daten nahtlos und effizient bearbeiten, auch wenn sie offline sind oder die Serverbindung langsam, unterbrochen oder nicht verfügbar ist. Die Lese-/Schreibvorgänge, die an zwischengespeicherten Geschäftsentitäten durchgeführt werden, werden synchronisiert, sobald eine Verbindung zum Server verfügbar ist.
    
  

## <a name="prerequisites-for-working-with-bcs-external-content-types"></a>Voraussetzungen für das Arbeiten mit externen BCS-Inhaltstypen
<a name="SP15ectoverview_prereq"> </a>

Um mit der Erstellung externer Inhaltstypen beginnen zu können, benötigen Sie Folgendes:
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
- Office Developer Tools für Visual Studio 2012
    
    oder
    
  
- SharePoint Designer 2013
    
  
Informationen zur Einrichtung einer Entwicklungsumgebung zur Erstellung externer Inhaltstypen finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

## <a name="what-can-you-do-with-external-content-types"></a>Welche Möglichkeiten bieten externe Inhaltstypen?
<a name="SP15ectoverview_whattodo"> </a>

Wenn SharePoint so konfiguriert ist, dass es mit dem externen System kommuniziert, können Sie mithilfe der externen Inhaltstypen die folgenden Objekte erstellen, um die zugrunde liegenden Daten darzustellen:
  
    
    

- **Externe Listen**
    
    Eine externe Liste ermöglicht auf die gleiche Weise, wie auf SharePoint-Listendaten zugegriffen wird, Zugriff auf Daten in externen Systemen. Externe Listen verwenden externe Inhaltstypen als ihre Datenquellen. Mithilfe externer Listen können Sie die Metadaten verwenden, die bereits über einen externen Inhaltstyp definiert sind, um eine SharePoint-Liste zu erstellen, die externe Daten enthält und das gleiche Aussehen und Verhalten wie jede andere SharePoint-Liste aufweist.
    
    Sie können externe Listen auch offline nehmen, um sie in Outlook 2013 zu verwenden. So können Sie mit externen Daten wie mit systemeigenen Outlook-Elementtypen wie Kontakten, Aufgaben und Beiträgen arbeiten, und die externen Daten in Office-Clientanwendungen verwenden.
    
    Bei externen Listen können Sie in das externe System zurückschreiben, wenn dies vom externen System erlaubt wird und es vom externen Inhaltstyp entsprechend modelliert wurde. Dies impliziert, dass Benutzer externe Daten direkt in der Liste bearbeiten können. Alle Änderungen, die an den Elementen in der Liste vorgenommen wurden, werden automatisch mit dem externen System synchronisiert. Außerdem können Sie mithilfe der Schaltfläche **Daten aktualisieren** in der Liste Daten synchronisieren und aktualisierte Daten vom externen System automatisch erhalten.
    
  
- **Externe Datenspalten**
    
    Mithilfe der externen Datenspalte können Benutzer Daten aus externen Inhaltstypen zu standardmäßigen SharePoint-Listen hinzufügen. Wie eine externe Liste können externe Datenspalten Daten von jedem externen Inhaltstyp anzeigen, der in Business Connectivity Services (BCS) modelliert wurde.
    
  
- **Geschäftsdaten-Webparts**
    
    SharePoint bietet für die Arbeit mit externen Daten fünf verschiedene Webparts: Geschäftsdatenliste, Geschäftsdatenelement, Generator für Geschäftsdatenelemente, Geschäftsdaten-Beziehungsliste und Geschäftsdatenaktionen.
    
  
- **Auswahltool für externe Inhaltstypen**
    
    Ein Auswahltool für externe Inhaltstypen stellt dem Benutzer Funktionen zur Auswahl und Auflösung bereit. Sie können ein Auswahltool in ein Formular oder eine Seite einbetten, wenn ein Benutzer aus einer Liste verfügbarer externer Inhaltstypen einen externen Inhaltstyp auswählen können soll. 
    
  
- **Auswahltool für externe Elemente**
    
    Ein Auswahltool für externe Elemente stellt für externe Elemente auf dem Server und in Rich-Client-Office-Anwendungen Funktionen zur Auswahl und Auflösung bereit. Sie können ein Auswahltool in ein Formular oder eine Seite einbetten, wenn ein Benutzer aus einer Liste mit Kunden ein externes Element wie einen Kunden auswählen können soll. 
    
  
- **Profilseiten**
    
    Profilseiten sind SharePoint-Seiten in SharePoint, auf denen die Details zu einem externen Element angezeigt werden. Wie jedes andere SharePoint-Webparts-Seite können Sie diese Seite so anpassen, dass Details eines externen Elements angezeigt werden.
    
  
- **Benutzerdefinierte Seiten und Anwendungen**
    
    Sie können die Programmierbarkeitsoptionen von SharePoint verwenden, wie das SharePoint-Objektmodell, das SharePoint-Clientobjektmodell und REST-URLs (Representational State Transfer).
    
  
Tabelle 1 enthält Beispielaufgaben, mit denen das Arbeiten mit externen Inhaltstypen veranschaulicht wird.
  
    
    

**Tabelle 1. Einfache Aufgaben für das Arbeiten mit externen Inhaltstypen**


|**Aufgabe**|**Beschreibung**|
|:-----|:-----|
| [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |Erfahren Sie, wie Sie mithilfe von Visual Studio 2012 eine veröffentlichte OData-Quelle ermitteln und einen wiederverwendbaren externen Inhaltstyp zur Verwendung in SharePoint Business Connectivity Services (BCS) erstellen.  <br/> |
| [Vorgehensweise: Erstellen externer Inhaltstypen für SQL Server in SharePoint](how-to-create-external-content-types-for-sql-server-in-sharepoint.md) <br/> |Erfahren Sie, wie Sie einen externen Inhaltstyp erstellen, der auf einer SQL Server-Datenbank basiert.  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="SP15ectoverview_addres"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Vorgehensweise: erstellen ein Add-in-bezogenen externes Inhaltstyps in SharePoint](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen externer Inhaltstypen für SQL Server in SharePoint](how-to-create-external-content-types-for-sql-server-in-sharepoint.md)
    
  
-  [Erste Schritte mit den Business Connectivity Services in SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  

