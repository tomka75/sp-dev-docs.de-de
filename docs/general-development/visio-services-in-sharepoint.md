---
title: Visio Services in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ed8c5d12-e17d-4ceb-b195-601c26824370
ms.openlocfilehash: ad71c9db6949c0011e8a1d0ff1e8c5580f23b43e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="visio-services-in-sharepoint"></a>Visio Services in SharePoint
Mit Visio Services in Microsoft SharePoint können Sie programmgesteuert Visio-Dateien in den Formaten VSDX, VSDM und VDW (Visio-Webzeichnungen) in Microsoft SharePoint und Microsoft SharePoint Online laden, anzeigen und damit interagieren.
## <a name="whats-new-in-visio-services-in-sharepoint"></a>Neuigkeiten in Visio Services in SharePoint
<a name="visserv15_WhatsNew"> </a>

Visio Services in Microsoft SharePoint und in Microsoft SharePoint Online enthält einige neue Features. Dazu zählen die Unterstützung des neuen Dateiformats für Microsoft Visio 2013, Unterstützung von Microsoft Business Connectivity Services (BCS)-Datenquellen und der programmgesteuerte Zugriff auf Kommentare.
  
    
    

### <a name="new-file-format"></a>Neues Dateiformat
<a name="vis15_WhatsNew_NewFF"> </a>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|Mit Visio 2013 wird ein neues Dateiformat eingefügt (VSDX), das auf dem Standard Open Packaging Conventions (OPC, ISO 29500, Teil 2) und den XML-Elementen aus dem vorherigen Visio-Dateiformat (VDX) basiert. Es handelt sich um ein komprimiertes, XML-basiertes Dateiformat, ähnlich wie bei anderen -Anwendungen.<br/> Mit dem neuen Dateiformat können Sie Visio 2013-Zeichnungen direkt in einer SharePoint Server- oder SharePoint Online-Bibliothek speichern, ohne die Datei als Visio-Webzeichnung (VDW) veröffentlichen zu müssen. Dennoch kann Visio Services Visio-Webzeichnungen weiterhin lesen und anzeigen.<br/> Mit Visio Services können Visio-Webzeichnungen im Format VDW weiterhin im Browser angezeigt werden. Es können außerdem die neuen Formate Visio-Zeichnung (VSDX) und Visio-Zeichnung mit Makros (VSDM) gerendert werden.<br/>  Das Visio ServicesECMAScript (JavaScript, JScript)-Objektmodell enthält eine neue API zur Unterstützung der neuen Dateiformate:  [Vwa.VwaControl.getDiagramFileType Method]((http://msdn.microsoft.com/library/fd8ca95f-a3be-4000-bce8-3aaf1f48148c%28Office.15%29.aspx)). Die Methoden geben einen Wert von  [Vwa.DiagramFileType Enumeration]((http://msdn.microsoft.com/library/dd2f8a5d-a54b-44bd-a458-02efdcba0201%28Office.15%29.aspx)) zurück, der angibt ob eine im Visio Web Access-Webpart angezeigte Datei eine Visio-Zeichnung (VSDX) oder eine Visio-Webzeichnung (VDW) ist. <br/> Weitere Informationen über das neue Dateiformat in Visio 2013 finden Sie unter [Einführung in das Visio-Dateiformat (.vsdx)]((http://msdn.microsoft.com/library/69736f40-8f67-46c2-abf6-82dffecb2274%28Office.15%29.aspx)).  <br/> **Hinweis:** Die neuen Visio-Dateien (.vsdx und .vsdm) werden nur im Rasterformat in Visio Services angezeigt. Visio-Webzeichnungen (.vdw) können weiterhin mit Silverlight angezeigt werden.           |
   

### <a name="support-for-business-connectivity-services-bcs-data"></a>Unterstützung für Business Connectivity Services (BCS)-Daten
<a name="vis15_WhatsNew_BCS"> </a>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|Visio 2013-Diagramme können nun mit externen Listen verbunden werden, die mit Microsoft Business Connectivity Services (BCS) auf SharePoint-Servern und in SharePoint Online erstellt wurden. Visio Services unterstützt das Aktualisieren der Visio-Diagramme beim Aktualisieren von Daten.  <br/> **Hinweis:** Visio Services bietet keine Unterstützung für SQL, SQL Azure, OLEDC, ODBC und benutzerdefinierte Datenanbieter als Datenquellen in SharePoint Online.           |
   

### <a name="commenting"></a>Kommentare
<a name="vis15_WhatsNew_Commenting"> </a>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|Visio 2013 enthält ein neues Framework für Kommentare. Kommentare können nun mit einer bestimmten Form oder Seite verknüpft werden. Visio Services enthält JavaScript-APIs zum Abrufen der Kommentare aus einem Diagramm.<br/> Weitere Information zu den APIs für Kommentare im Visio ServicesJavaScript-Objektmodell finden Sie unter den Themen  [VwaPage.getPageComments Method]((http://msdn.microsoft.com/library/d1e7740c-e0fa-4823-b2b6-14551bb84c36%28Office.15%29.aspx)) und [VwaShape.getComments Method]((http://msdn.microsoft.com/library/fcdec9c2-a503-4315-b048-033cd5ac09dd%28Office.15%29.aspx)).  <br/> |
   

### <a name="expanded-recalculation"></a>Erweiterte Neuberechnung
<a name="vis15_WhatsNew_Commenting"> </a>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|Visio Services kann Formeln im ShapeSheet neu berechnen. Zusätzlich zum Aktualisieren von Datengrafiken kann Visio Services alle Formen aktualisieren, die Daten und Diagramme enthalten, die von Daten abhängig sind. Bei der Neuberechnung werden die meisten ShapeSheet-Funktionen unterstützt.  <br/> |
   

### <a name="improved-error-handling"></a>Verbesserte Fehlerbehandlung
<a name="vis15_WhatsNew_Commenting"> </a>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|Bei einem Fehler bei der Aktualisierung der Daten in einer angezeigten Visio-Zeichnung in Visio Services wird nun ein statisches Bild des Diagramms angezeigt. Außerdem gibt Visio Services hilfreichere Informationen in Fehlermeldungen aus.  <br/> |
   

### <a name="secure-store-authentication"></a>Sichere Authentifizierung im Store
<a name="vis15_WhatsNew_Commenting"> </a>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|Bisher mussten Authentifizierungseinstellungen für externe Datenquellen (wie z. B. eine SQL-Datenbank) in einem Dienstprogramm in Microsoft Excel konfiguriert werden. Mit Visio 2013 können Benutzer Ihre mit Diagrammen verbundenen Daten direkt in der Visio-Clientanwendung konfigurieren, wodurch Datenquellen in Visio Services aktualisiert werden können.  <br/> |
   

## <a name="visio-services-javascript-object-model"></a>Visio Services-JavaScript-Objektmodell
<a name="visserv15_JSOM"> </a>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|Der  [Vwa-Namespace]((http://msdn.microsoft.com/library/b67939fa-d3db-41ff-8864-eabd318ba7c4%28Office.15%29.aspx)) im JavaScript-Objektmodell in Visio Services ermöglicht Ihnen den programmatischen Zugriff auf Visio-Zeichnungen, die im Visio Web Access-Webpart angezeigt werden. Mit dem JavaScript-Objektmodell können Sie auf Daten zu Diagrammen, Seiten, Formen, Formhyperlinks und umgebenden Felder von Formen zugreifen. Dadurch können Sie die Informationen neu anordnen und bspw. bestimmte Formen hervorheben, Überlagerungen auf Diagrammen platzieren, auf Diagramm- und Mausereignisse reagieren und die Schwenk- und Zoom-Eigenschaften des Viewports ändern.<br/> Weitere Informationen zum Hinzufügen eines Visio Web Access-Webparts zu einer SharePoint-Seite und zum Programmieren dieser Seite mit den JavaScript-APIs in Visio 2013 finden Sie unter  [Anpassen von Visio-Webzeichnungen im Visio Web Access-Webpart]((http://msdn.microsoft.com/de-DE/library/ff394649.aspx)).  <br/> |
   

## <a name="visio-services-class-library"></a>Visio Services-Klassenbibliothek
<a name="visserv15_Mref"> </a>


|||
|:-----|:-----|
|![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|Sie können die Visio Services-Klassenbibliothek im Namespace [Microsoft.Office.Visio.Server]((https://msdn.microsoft.com/library/Microsoft.Office.Visio.Server.aspx)) verwenden, um benutzerdefinierte Visio Services-Datenanbieter zu erstellen. Diese Datenanbieter ermöglichen Ihnen die programmgesteuerte Aktualisierung von Daten, die aus benutzerdefinierten Datenquellen in Visio 2013-Diagrammen abgeleitet werden, die auf einer SharePoint-Website gehostet sind. <br/> Weitere Informationen zum Erstellen benutzerdefinierter Datenanbieter und zu einer vollständige End-to-End-Lösung finden Sie unter  [Erstellen einen benutzerdefinierten Datenanbieters mit Visio Services]((http://msdn.microsoft.com/de-DE/library/ff394595.aspx)).  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="visserv15_Additional"> </a>


-  [Microsoft.Office.Visio.Server]((https://msdn.microsoft.com/library/Microsoft.Office.Visio.Server.aspx))
    
  
-  [Vwa-Namespace]((http://msdn.microsoft.com/library/b67939fa-d3db-41ff-8864-eabd318ba7c4%28Office.15%29.aspx))
    
  
-  [Erstellen einen benutzerdefinierten Datenanbieters mit Visio Services]((http://msdn.microsoft.com/de-DE/library/ff394595.aspx))
    
  
-  [Anpassen von Visio-Webzeichnungen im Visio Web Access-Webpart]((http://msdn.microsoft.com/de-DE/library/ff394649.aspx))
    
  
-  [New in Visio for developers]((http://msdn.microsoft.com/library/7e3fb858-0ab8-bd2e-217c-c85b10d79785%28Office.15%29.aspx))
    
  
- Eine Liste der neuen Features in vis15short für Endbenutzer finden Sie unter  [Neuerungen in Visio]((http://office.com/redir/HA102749364.aspx)).
    
  
