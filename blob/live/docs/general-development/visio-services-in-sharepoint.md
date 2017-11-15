---
title: Visio Services in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ed8c5d12-e17d-4ceb-b195-601c26824370
ms.openlocfilehash: d59e3c6d447327e9ad9444f889f38c24ca21120f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="visio-services-in-sharepoint"></a><span data-ttu-id="9346d-102">Visio Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9346d-102">Visio Services in SharePoint</span></span>
<span data-ttu-id="9346d-103">Mit Visio Services in Microsoft SharePoint können Sie programmgesteuert Visio-Dateien in den Formaten VSDX, VSDM und VDW (Visio-Webzeichnungen) in Microsoft SharePoint und Microsoft SharePoint Online laden, anzeigen und damit interagieren.</span><span class="sxs-lookup"><span data-stu-id="9346d-103">Visio Services in Microsoft SharePoint Server 2013 enables you to load, display, and interact programmatically with Visio .vsdx, .vsdm files and Visio Web Drawings (.vdw) on Microsoft SharePoint Server 2013 and Microsoft SharePoint Online.</span></span>
## <a name="whats-new-in-visio-services-in-sharepoint"></a><span data-ttu-id="9346d-104">Neuigkeiten in Visio Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9346d-104">What's new in Visio Services in SharePoint Server 2013</span></span>
<span data-ttu-id="9346d-105"><a name="visserv15_WhatsNew"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-105"></span></span>

<span data-ttu-id="9346d-106">Visio Services in Microsoft SharePoint und in Microsoft SharePoint Online enthält einige neue Features. Dazu zählen die Unterstützung des neuen Dateiformats für Microsoft Visio 2013, Unterstützung von Microsoft Business Connectivity Services (BCS)-Datenquellen und der programmgesteuerte Zugriff auf Kommentare.</span><span class="sxs-lookup"><span data-stu-id="9346d-106">Visio Services in Microsoft SharePoint Server 2013 and in Microsoft SharePoint Online includes several new features, including support for the new Microsoft Visio 2013 file format, support for Microsoft Business Connectivity Services (BCS) data sources, and programmatic access to comments.</span></span>
  
    
    

### <a name="new-file-format"></a><span data-ttu-id="9346d-107">Neues Dateiformat</span><span class="sxs-lookup"><span data-stu-id="9346d-107">New file format</span></span>
<span data-ttu-id="9346d-108"><a name="vis15_WhatsNew_NewFF"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-108"></span></span>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|<span data-ttu-id="9346d-p101">Mit Visio 2013 wird ein neues Dateiformat eingefügt (VSDX), das auf dem Standard Open Packaging Conventions (OPC, ISO 29500, Teil 2) und den XML-Elementen aus dem vorherigen Visio-Dateiformat (VDX) basiert. Es handelt sich um ein komprimiertes, XML-basiertes Dateiformat, ähnlich wie bei anderen -Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="9346d-p101">Visio 2013 introduces a new file format (.vsdx), based on the Open Packaging Conventions (OPC) standard (ISO 29500, Part 2) and the XML elements from the previous Visio XML file format (.vdx). It is a zipped, XML-based file format similar to the file formats used in other applications.  </span></span><br/> <span data-ttu-id="9346d-p102">Mit dem neuen Dateiformat können Sie Visio 2013-Zeichnungen direkt in einer SharePoint Server- oder SharePoint Online-Bibliothek speichern, ohne die Datei als Visio-Webzeichnung (VDW) veröffentlichen zu müssen. Dennoch kann Visio Services Visio-Webzeichnungen weiterhin lesen und anzeigen.</span><span class="sxs-lookup"><span data-stu-id="9346d-p102">With the new file format, you can save a Visio 2013 drawing directly to a SharePoint Server or SharePoint Online library, without having to publish the file as a Visio Web Drawing (.vdw). Even so, Visio Services can still read and display Visio Web Drawing files.  </span></span><br/> <span data-ttu-id="9346d-p103">Mit Visio Services können Visio-Webzeichnungen im Format VDW weiterhin im Browser angezeigt werden. Es können außerdem die neuen Formate Visio-Zeichnung (VSDX) und Visio-Zeichnung mit Makros (VSDM) gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="9346d-p103">Visio Services retains the ability to display the Visio Web Drawing (.vdw) format in the browser. It now also renders the new Visio drawing (.vsdx) and Visio macro-enabled drawing (.vsdm) formats.  </span></span><br/> <span data-ttu-id="9346d-p104"> Das Visio ServicesECMAScript (JavaScript, JScript)-Objektmodell enthält eine neue API zur Unterstützung der neuen Dateiformate:  [Vwa.VwaControl.getDiagramFileType Method](http://msdn.microsoft.com/library/fd8ca95f-a3be-4000-bce8-3aaf1f48148c%28Office.15%29.aspx). Die Methoden geben einen Wert von  [Vwa.DiagramFileType Enumeration](http://msdn.microsoft.com/library/dd2f8a5d-a54b-44bd-a458-02efdcba0201%28Office.15%29.aspx) zurück, der angibt ob eine im Visio Web Access-Webpart angezeigte Datei eine Visio-Zeichnung (VSDX) oder eine Visio-Webzeichnung (VDW) ist. </span><span class="sxs-lookup"><span data-stu-id="9346d-p104">The Visio ServicesECMAScript (JavaScript, JScript) object model contains a new API to support the new file format: the  [Vwa.VwaControl.getDiagramFileType Method](http://msdn.microsoft.com/library/fd8ca95f-a3be-4000-bce8-3aaf1f48148c%28Office.15%29.aspx). The methods returns a value from the  [Vwa.DiagramFileType Enumeration](http://msdn.microsoft.com/library/dd2f8a5d-a54b-44bd-a458-02efdcba0201%28Office.15%29.aspx) that indicates whether the file displayed in the Visio Web Access Web Part is a Visio drawing (.vsdx) or a Visio Web Drawing (.vdw). </span></span><br/> <span data-ttu-id="9346d-119">Weitere Informationen über das neue Dateiformat in Visio 2013 finden Sie unter [Einführung in das Visio-Dateiformat (.vsdx)](http://msdn.microsoft.com/library/69736f40-8f67-46c2-abf6-82dffecb2274%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9346d-119">For more information about the new file format in Visio 2013, see  [Introduction to the Visio file format (.vsdx)](http://msdn.microsoft.com/library/69736f40-8f67-46c2-abf6-82dffecb2274%28Office.15%29.aspx).</span></span>  <br/> <span data-ttu-id="9346d-120">**Hinweis:** Die neuen Visio-Dateien (.vsdx und .vsdm) werden nur im Rasterformat in Visio Services angezeigt.</span><span class="sxs-lookup"><span data-stu-id="9346d-120">The new Visio files (.vsdx and .vsdm) are only displayed in raster format on Visio Services. Visio Web Drawings (.vdw) can still be displayed using Silverlight.</span></span> <span data-ttu-id="9346d-121">Visio-Webzeichnungen (.vdw) können weiterhin mit Silverlight angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="9346d-121">Visio Web Drawings (.vdw) can still be displayed using Silverlight.</span></span>           |
   

### <a name="support-for-business-connectivity-services-bcs-data"></a><span data-ttu-id="9346d-122">Unterstützung für Business Connectivity Services (BCS)-Daten</span><span class="sxs-lookup"><span data-stu-id="9346d-122">Support for Business Connectivity Services (BCS) data</span></span>
<span data-ttu-id="9346d-123"><a name="vis15_WhatsNew_BCS"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-123"></span></span>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|<span data-ttu-id="9346d-126">Visio 2013-Diagramme können nun mit externen Listen verbunden werden, die mit Microsoft Business Connectivity Services (BCS) auf SharePoint-Servern und in SharePoint Online erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="9346d-126">Visio 2013 diagrams can now be connected to external lists created using Microsoft Business Connectivity Services (BCS) on SharePoint Server 2013 servers and in SharePoint Online. Visio Services supports the ability to refresh the Visio diagrams as the data updates.</span></span> <span data-ttu-id="9346d-127">Visio Services unterstützt das Aktualisieren der Visio-Diagramme beim Aktualisieren von Daten.</span><span class="sxs-lookup"><span data-stu-id="9346d-127">Visio Services supports the ability to refresh the Visio diagrams as the data updates.</span></span>  <br/> <span data-ttu-id="9346d-128">**Hinweis:** Visio Services bietet keine Unterstützung für SQL, SQL Azure, OLEDC, ODBC und benutzerdefinierte Datenanbieter als Datenquellen in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="9346d-128">Visio Services does not support SQL, SQL Azure, OLEDC, ODBC, and custom data providers as data sources in SharePoint Online.</span></span>           |
   

### <a name="commenting"></a><span data-ttu-id="9346d-129">Kommentare</span><span class="sxs-lookup"><span data-stu-id="9346d-129">Commenting</span></span>
<span data-ttu-id="9346d-130"><a name="vis15_WhatsNew_Commenting"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-130"></span></span>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|<span data-ttu-id="9346d-p107">Visio 2013 enthält ein neues Framework für Kommentare. Kommentare können nun mit einer bestimmten Form oder Seite verknüpft werden. Visio Services enthält JavaScript-APIs zum Abrufen der Kommentare aus einem Diagramm.</span><span class="sxs-lookup"><span data-stu-id="9346d-p107">Visio 2013 includes a new commenting framework. Comments can now be associated with a particular shape or page. Visio Services includes JavaScript APIs to retrieve the comments from a diagram.  </span></span><br/> <span data-ttu-id="9346d-136">Weitere Information zu den APIs für Kommentare im Visio ServicesJavaScript-Objektmodell finden Sie unter den Themen  [VwaPage.getPageComments Method](http://msdn.microsoft.com/library/d1e7740c-e0fa-4823-b2b6-14551bb84c36%28Office.15%29.aspx) und [VwaShape.getComments Method](http://msdn.microsoft.com/library/fcdec9c2-a503-4315-b048-033cd5ac09dd%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9346d-136">For more information about the commenting APIs in the Visio ServicesJavaScript object model, see the topics  [VwaPage.getPageComments Method](http://msdn.microsoft.com/library/d1e7740c-e0fa-4823-b2b6-14551bb84c36%28Office.15%29.aspx) and [VwaShape.getComments Method](http://msdn.microsoft.com/library/fcdec9c2-a503-4315-b048-033cd5ac09dd%28Office.15%29.aspx).</span></span>  <br/> |
   

### <a name="expanded-recalculation"></a><span data-ttu-id="9346d-137">Erweiterte Neuberechnung</span><span class="sxs-lookup"><span data-stu-id="9346d-137">Expanded recalculation</span></span>
<span data-ttu-id="9346d-138"><a name="vis15_WhatsNew_Commenting"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-138"></span></span>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|<span data-ttu-id="9346d-p108">Visio Services kann Formeln im ShapeSheet neu berechnen. Zusätzlich zum Aktualisieren von Datengrafiken kann Visio Services alle Formen aktualisieren, die Daten und Diagramme enthalten, die von Daten abhängig sind. Bei der Neuberechnung werden die meisten ShapeSheet-Funktionen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="9346d-p108">Visio Services can now recalculate formulas in the ShapeSheet. In addition to refreshing Data Graphics, Visio Services can refresh all shapes with data and visuals that depend upon data. Most ShapeSheet functions are supported for recalculation.</span></span>  <br/> |
   

### <a name="improved-error-handling"></a><span data-ttu-id="9346d-144">Verbesserte Fehlerbehandlung</span><span class="sxs-lookup"><span data-stu-id="9346d-144">Improved error handling</span></span>
<span data-ttu-id="9346d-145"><a name="vis15_WhatsNew_Commenting"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-145"></span></span>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|<span data-ttu-id="9346d-p109">Bei einem Fehler bei der Aktualisierung der Daten in einer angezeigten Visio-Zeichnung in Visio Services wird nun ein statisches Bild des Diagramms angezeigt. Außerdem gibt Visio Services hilfreichere Informationen in Fehlermeldungen aus.</span><span class="sxs-lookup"><span data-stu-id="9346d-p109">When a data refresh error occurs in a Visio drawing displayed in Visio Services, the display now falls back to a static image of the diagram. Visio Services also provides more actionable information in error messages.</span></span>  <br/> |
   

### <a name="secure-store-authentication"></a><span data-ttu-id="9346d-150">Sichere Authentifizierung im Store</span><span class="sxs-lookup"><span data-stu-id="9346d-150">Secure Store Authentication</span></span>
<span data-ttu-id="9346d-151"><a name="vis15_WhatsNew_Commenting"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-151"></span></span>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|<span data-ttu-id="9346d-p110">Bisher mussten Authentifizierungseinstellungen für externe Datenquellen (wie z. B. eine SQL-Datenbank) in einem Dienstprogramm in Microsoft Excel konfiguriert werden. Mit Visio 2013 können Benutzer Ihre mit Diagrammen verbundenen Daten direkt in der Visio-Clientanwendung konfigurieren, wodurch Datenquellen in Visio Services aktualisiert werden können.</span><span class="sxs-lookup"><span data-stu-id="9346d-p110">Previously, Authentication Settings for external data sources (a SQL database, for example) could only be configured through a utility in Microsoft Excel. With Visio 2013, users can now configure their data connected diagrams directly from the Visio client, which allows data sources to be refreshed in Visio Services.</span></span>  <br/> |
   

## <a name="visio-services-javascript-object-model"></a><span data-ttu-id="9346d-156">Visio Services-JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="9346d-156">Visio Services JavaScript Object Model</span></span>
<span data-ttu-id="9346d-157"><a name="visserv15_JSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-157"></span></span>


|||
|:-----|:-----|
|![Notiz zum Verhalten in der Cloud](../images/mod_icon_incloud.gif)           <br/> ![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|<span data-ttu-id="9346d-p111">Der  [Vwa-Namespace](http://msdn.microsoft.com/library/b67939fa-d3db-41ff-8864-eabd318ba7c4%28Office.15%29.aspx) im JavaScript-Objektmodell in Visio Services ermöglicht Ihnen den programmatischen Zugriff auf Visio-Zeichnungen, die im Visio Web Access-Webpart angezeigt werden. Mit dem JavaScript-Objektmodell können Sie auf Daten zu Diagrammen, Seiten, Formen, Formhyperlinks und umgebenden Felder von Formen zugreifen. Dadurch können Sie die Informationen neu anordnen und bspw. bestimmte Formen hervorheben, Überlagerungen auf Diagrammen platzieren, auf Diagramm- und Mausereignisse reagieren und die Schwenk- und Zoom-Eigenschaften des Viewports ändern.</span><span class="sxs-lookup"><span data-stu-id="9346d-p111">The  [Vwa namespace](http://msdn.microsoft.com/library/b67939fa-d3db-41ff-8864-eabd318ba7c4%28Office.15%29.aspx) in the JavaScript object model in Visio Services gives you programmatic access to Visio drawings displayed in the Visio Web Access Web Part. Using the JavaScript object model, you can access data about diagrams, pages, and shapes; shape hyperlinks; and shape bounding box properties. With this access, you can create mashups that highlight shapes, place overlays on the diagram, respond to diagram and mouse events, and change the panning and zooming properties of the viewport. </span></span><br/> <span data-ttu-id="9346d-163">Weitere Informationen zum Hinzufügen eines Visio Web Access-Webparts zu einer SharePoint-Seite und zum Programmieren dieser Seite mit den JavaScript-APIs in Visio 2013 finden Sie unter  [Anpassen von Visio-Webzeichnungen im Visio Web Access-Webpart](http://msdn.microsoft.com/en-us/library/ff394649.aspx).</span><span class="sxs-lookup"><span data-stu-id="9346d-163">For information about adding a Visio Web Access Web Part to a SharePoint page and programming that page by using the JavaScript APIs in Visio 2013, see  [Customizing Visio Web Drawings in the Visio Web Access Web Part](http://msdn.microsoft.com/en-us/library/ff394649.aspx).</span></span>  <br/> |
   

## <a name="visio-services-class-library"></a><span data-ttu-id="9346d-164">Visio Services-Klassenbibliothek</span><span class="sxs-lookup"><span data-stu-id="9346d-164">Visio Services Class Library</span></span>
<span data-ttu-id="9346d-165"><a name="visserv15_Mref"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-165"></span></span>


|||
|:-----|:-----|
|![Hinweis zum lokalen Verhalten](../images/mod_icon_onpremises.gif)|<span data-ttu-id="9346d-167">Sie können die Visio Services-Klassenbibliothek im Namespace [Microsoft.Office.Visio.Server](https://msdn.microsoft.com/library/Microsoft.Office.Visio.Server.aspx) verwenden, um benutzerdefinierte Visio Services-Datenanbieter zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="9346d-167">You can use the Visio Services class library, in the  [Microsoft.Office.Visio.Server](https://msdn.microsoft.com/library/Microsoft.Office.Visio.Server.aspx) namespace, to build custom Visio Services data providers. These data providers permit you to programmatically refresh data derived from custom data sources in Visio 2013 diagrams hosted on a SharePoint Server 2013 site.</span></span> <span data-ttu-id="9346d-168">Diese Datenanbieter ermöglichen Ihnen die programmgesteuerte Aktualisierung von Daten, die aus benutzerdefinierten Datenquellen in Visio 2013-Diagrammen abgeleitet werden, die auf einer SharePoint-Website gehostet sind.</span><span class="sxs-lookup"><span data-stu-id="9346d-168">You can use the Visio Services class library, in the  Microsoft.Office.Visio.Server namespace, to build custom Visio Services data providers. These data providers permit you to programmatically refresh data derived from custom data sources in Visio 2013 diagrams hosted on a SharePoint Server 2013 site.</span></span> <br/> <span data-ttu-id="9346d-169">Weitere Informationen zum Erstellen benutzerdefinierter Datenanbieter und zu einer vollständige End-to-End-Lösung finden Sie unter  [Erstellen einen benutzerdefinierten Datenanbieters mit Visio Services](http://msdn.microsoft.com/en-us/library/ff394595.aspx).</span><span class="sxs-lookup"><span data-stu-id="9346d-169">For more information about creating a custom data provider and to work through a complete end-to-end solution, see  [Creating a Custom Data Provider with Visio Services](http://msdn.microsoft.com/en-us/library/ff394595.aspx).</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="9346d-170">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9346d-170">Additional Resources</span></span>
<span data-ttu-id="9346d-171"><a name="visserv15_Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="9346d-171"></span></span>


-  [<span data-ttu-id="9346d-172">Microsoft.Office.Visio.Server</span><span class="sxs-lookup"><span data-stu-id="9346d-172">Microsoft.Office.Visio.Server</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Visio.Server.aspx)
    
  
-  [<span data-ttu-id="9346d-173">Vwa-Namespace</span><span class="sxs-lookup"><span data-stu-id="9346d-173">Vwa namespace</span></span>](http://msdn.microsoft.com/library/b67939fa-d3db-41ff-8864-eabd318ba7c4%28Office.15%29.aspx)
    
  
-  <span data-ttu-id="9346d-174">
  [Erstellen einen benutzerdefinierten Datenanbieters mit Visio Services](http://msdn.microsoft.com/en-us/library/ff394595.aspx)</span><span class="sxs-lookup"><span data-stu-id="9346d-174">[Creating a Custom Data Provider with Visio Services](http://msdn.microsoft.com/en-us/library/ff394595.aspx)</span></span>
    
  
-  <span data-ttu-id="9346d-175">
  [Anpassen von Visio-Webzeichnungen im Visio Web Access-Webpart](http://msdn.microsoft.com/en-us/library/ff394649.aspx)</span><span class="sxs-lookup"><span data-stu-id="9346d-175">[Customizing Visio Web Drawings in the Visio Web Access Web Part](http://msdn.microsoft.com/en-us/library/ff394649.aspx)</span></span>
    
  
-  [<span data-ttu-id="9346d-176">New in Visio for developers</span><span class="sxs-lookup"><span data-stu-id="9346d-176">New in Visio for developers</span></span>](http://msdn.microsoft.com/library/7e3fb858-0ab8-bd2e-217c-c85b10d79785%28Office.15%29.aspx)
    
  
- <span data-ttu-id="9346d-177">Eine Liste der neuen Features in vis15short für Endbenutzer finden Sie unter  [Neuerungen in Visio](http://office.com/redir/HA102749364.aspx).</span><span class="sxs-lookup"><span data-stu-id="9346d-177">For a list of new features in vis15short for end users, see  [What's new in Visio](http://office.com/redir/HA102749364.aspx).</span></span>
    
  
