---
title: Erstellen von SharePoint-Add-Ins in Visual Studio
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ef06e1e32cbdafb36b2ff074dacd0d528f6a656f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="create-sharepoint-add-ins-in-visual-studio"></a><span data-ttu-id="231e0-102">Erstellen von SharePoint-Add-Ins in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="231e0-102">Create SharePoint Add-ins in Visual Studio</span></span>
<span data-ttu-id="231e0-103">Erfahren Sie, wie Sie SharePoint-Add-Ins mithilfe von Vorlagen für Projekte und Projektelemente in Visual Studio entwickeln.</span><span class="sxs-lookup"><span data-stu-id="231e0-103">Learn to develop SharePoint Add-ins by using templates for projects and project items in Visual Studio.</span></span>
 

 <span data-ttu-id="231e0-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="231e0-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="231e0-107">Sie können SharePoint Add-Ins mithilfe neuer Vorlagen für Projekte und Projektelemente in **vsnv** erstellen.</span><span class="sxs-lookup"><span data-stu-id="231e0-107">You can develop SharePoint Add-ins by using new templates for projects and project items in  **vsnv**.</span></span> 
 

## <a name="project-templates"></a><span data-ttu-id="231e0-108">Projektvorlagen</span><span class="sxs-lookup"><span data-stu-id="231e0-108">Project templates</span></span>
<span data-ttu-id="231e0-109"><a name="SP15Projecttemplates_templates"> </a></span><span class="sxs-lookup"><span data-stu-id="231e0-109"></span></span>

<span data-ttu-id="231e0-p102">Wenn Sie eine Projektvorlage in Visual Studio verwenden, erstellt diese eine Projektmappe mit den Projektelementen und -dateien, die für den Projekttyp erforderlich sind. Die folgenden Projektvorlagen werden im Dialogfeld **Neues Projekt** angezeigt, wenn Sie den Knoten **Office/SharePoint** und dann den Knoten **Add-Ins** auswählen. Informationen über die Projektvorlagen unter dem Knoten **SharePoint-Lösungen** finden Sie im Artikel über [SharePoint-Projekt- und -Projektelementvorlagen](http://go.microsoft.com/fwlink/?LinkId=255306).</span><span class="sxs-lookup"><span data-stu-id="231e0-p102">When you use a project template in Visual Studio, it creates a solution that contains the project items and files that the project type requires. The following project templates appear in the  **New Project** dialog box if you expand the **Office/SharePoint** node and then you choose the **Add-ins** node. For information about the project templates under the **SharePoint Solutions** node, see [SharePoint Project and Project Item Templates](http://go.microsoft.com/fwlink/?LinkId=255306).</span></span> 
 

 

### <a name="office-add-in"></a><span data-ttu-id="231e0-113">Office-Add-In</span><span class="sxs-lookup"><span data-stu-id="231e0-113">Office Add-in</span></span>

<span data-ttu-id="231e0-p103">Erstellt eine Webseite, die in einer Office-Anwendung wie Excel oder Outlook gehostet wird. Eine Office-Add-In liefert zusätzliche Inhalte und Funktionen in einem Dokument oder Outlook-Element. Weitere Informationen finden Sie unter  [Office-Add-Ins-Plattformübersicht](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="231e0-p103">Creates a webpage that's hosted inside an Office application, such as Excel or Outlook. An Office Add-in provides additional content and functionality in a document or Outlook item. For more information, see  [Office Add-ins platform overview](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).</span></span>
 

 

### <a name="sharepoint-add-in"></a><span data-ttu-id="231e0-117">SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="231e0-117">SharePoint Add-in</span></span>

<span data-ttu-id="231e0-p104">Erstellt ein SharePoint-Add-In basierend auf den Informationen, die Sie in einem Assistenten eingeben. Zu diesen Informationen gehören folgende Angaben.</span><span class="sxs-lookup"><span data-stu-id="231e0-p104">Creates a SharePoint Add-in based on the information that you specify in a wizard. This information includes the following data.</span></span>
 

 

- <span data-ttu-id="231e0-120">Der Name des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="231e0-120">The name of the add-in.</span></span>
    
 
- <span data-ttu-id="231e0-121">Die lokale SharePoint-Website oder die SharePoint-Remotewebsite für das Debugging Ihres Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="231e0-121">The local or remote SharePoint site to use for debugging your add-in.</span></span>
    
 
- <span data-ttu-id="231e0-122">Der Typ des Add-Ins, das Sie erstellen möchten: von einem Provider gehostet oder von SharePoint gehostet.</span><span class="sxs-lookup"><span data-stu-id="231e0-122">The type of add-in that you want to create: provider-hosted or SharePoint-hosted.</span></span> 
    
 
<span data-ttu-id="231e0-123">Weitere Informationen finden Sie unter [SharePoint-Add-Ins](sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="231e0-123">For more information, see  [SharePoint Add-ins](sharepoint-add-ins.md).</span></span>
 

 

### <a name="cloud-business-add-in"></a><span data-ttu-id="231e0-124">Cloud-Business-Add-In</span><span class="sxs-lookup"><span data-stu-id="231e0-124">Cloud Business Add-in</span></span>

<span data-ttu-id="231e0-p105">Mithilfe der Vorlage **Cloud-Business-Add-In** in Visual Studio können Sie ein in SharePoint gehostetes Add-In erstellen, in dem mobile Benutzer an einem Remotestandort mithilfe moderner Geräte wie Smartphones und Tablet-PCs mit Toucheingabe Daten anzeigen, hinzufügen und aktualisieren können. Weitere Informationen finden Sie unter [Erstellen von Cloud-Geschäfts-Add-Ins](create-cloud-business-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="231e0-p105">By using the  **Cloud Business Add-in** template in Visual Studio, you can create a SharePoint-hosted add-in in which mobile users can view, add, and update data from remote locations by using modern, touch-oriented devices such as phones and tablets. For more information, see [Create cloud business add-ins](create-cloud-business-add-ins.md).</span></span>
 

 

## <a name="project-item-templates"></a><span data-ttu-id="231e0-127">Projektelementvorlagen</span><span class="sxs-lookup"><span data-stu-id="231e0-127">Project item templates</span></span>
<span data-ttu-id="231e0-128"><a name="SP15Projecttemplates_items"> </a></span><span class="sxs-lookup"><span data-stu-id="231e0-128"></span></span>

<span data-ttu-id="231e0-129">Nach Erstellung einer SharePoint-Lösung können Sie Projektelemente anhand der folgenden Vorlagen hinzufügen, die im Dialogfeld **Neues Element hinzufügen** unter dem Knoten **Office/SharePoint** angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="231e0-129">After you create a SharePoint solution, you can add project items to it by using the following templates, which appear in the  **Add New Item** dialog box under the **Office/SharePoint** node.</span></span>
 

 

### <a name="office-add-in"></a><span data-ttu-id="231e0-130">Office-Add-In</span><span class="sxs-lookup"><span data-stu-id="231e0-130">Office Add-in</span></span>

<span data-ttu-id="231e0-p106">Fügt Ihrem SharePoint-Add-In ein Office-Add-In hinzu. Sie können ein Aufgabenbereichs-, ein Inhalts- oder ein Mail-Add-In erstellen. Weitere Informationen finden Sie unter  [Office-Add-Ins-Plattformübersicht](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="231e0-p106">Adds an Office Add-in to your SharePoint Add-in. You can add a task pane add-in, a content add-in, or a mail add-in. For more information, see  [Office Add-ins platform overview](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).</span></span>
 

 

### <a name="client-web-part-host-web"></a><span data-ttu-id="231e0-134">Clientwebpart (Hostweb)</span><span class="sxs-lookup"><span data-stu-id="231e0-134">Client Web Part (Host Web)</span></span>

<span data-ttu-id="231e0-p107">Fügt Ihrem SharePoint-Add-In ein Clientwebpart hinzu. Durch Hinzufügen eines Clientwebparts können Sie Add-Ins auf den Seiten einer Hostwebsite anzeigen. Diese Vorlage enthält eine einzelne Datei vom Typ "Elements.xml", deren Eigenschaften die folgenden Elemente des Clientwebparts definieren:</span><span class="sxs-lookup"><span data-stu-id="231e0-p107">Adds a client web part to your SharePoint Add-in. By adding a client web part, you can display add-ins on the pages of a host site. This template contains a single Elements.xml file, whose properties define the following elements of the client web part.</span></span>
 

 


|<span data-ttu-id="231e0-138">**Eigenschaftenname**</span><span class="sxs-lookup"><span data-stu-id="231e0-138">**Property Name**</span></span>|<span data-ttu-id="231e0-139">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="231e0-139">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="231e0-140">ClientWebPart</span><span class="sxs-lookup"><span data-stu-id="231e0-140">ClientWebPart</span></span>|<span data-ttu-id="231e0-141">Gibt den Namen, den Titel, die Beschreibung und die Dimensionen des Clientwebparts an.</span><span class="sxs-lookup"><span data-stu-id="231e0-141">Specifies the name, the title, the description, and the dimensions of the client web part.</span></span>|
|<span data-ttu-id="231e0-142">Content</span><span class="sxs-lookup"><span data-stu-id="231e0-142">Content</span></span>|<span data-ttu-id="231e0-p108">Definiert den Speicherort der Seite, die innerhalb des Clientwebparts gerendert wird. Das Element verfügt über zwei Eigenschaften: `Type` und `Src`. `Type` gibt den Typ des Webparts an, das Sie erstellen, beispielsweise HTML. `Src` definiert den Speicherort der Seite, die innerhalb des Clientwebparts gerendert wird. Die Vorlage verweist unter Verwendung des Schemas _ _Eigenschaftsname__ auf Eigenschaften in der Abfragezeichenfolge. Beispiel: `Src="~addinWebUrl/Pages/ClientWebPart1.aspx?Property1=_property1_"`Weitere Informationen finden Sie unter [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="231e0-p108">Defines the location of the page that renders inside the client web part. This element has two properties:  `Type` and `Src`.  `Type` specifies the type of web part that you're creating, such as HTML. `Src` defines the location of the page that will render inside the client web part. The template references properties on the query string by using the pattern _ _PropertyName__, such as  `Src="~addinWebUrl/Pages/ClientWebPart1.aspx?Property1=_property1_"`For more information, see  [Create add-in parts to install with your SharePoint Add-in](create-add-in-parts-to-install-with-your-sharepoint-add-in.md).</span></span>|

### <a name="content-type"></a><span data-ttu-id="231e0-148">Inhaltstyp</span><span class="sxs-lookup"><span data-stu-id="231e0-148">Content Type</span></span>

<span data-ttu-id="231e0-p109">Fügt Ihrem SharePoint-Add-In einen Inhaltstyp hinzu, ähnlich wie bei Inhaltstypen, die in früheren Version von SharePoint verwendet wurden. Ein Inhaltstyp ist ein Satz von Metadaten, Workflows und Verhaltensweisen für eine Kategorie von Elementen in einer SharePoint-Liste oder -Bibliothek. Beispielsweise ist ein Element ein Listeninhaltstyp. Andere Listeninhaltstypen sind z. B. Ankündigungen, Kontakte und Aufgaben, und sie erben vom Inhaltstyp Element. Der Inhaltstyp Kontakt enthält Spalten wie **Vorname**, **Nachname** und **Position**.</span><span class="sxs-lookup"><span data-stu-id="231e0-p109">Adds a content type to your SharePoint Add-in, similar to content types that were used in previous versions of SharePoint. A content type is a set of metadata, workflows, and behavior for a category of items in a SharePoint list or library. For example, an item is one type of list content. Other types of list content include announcements, contacts, and tasks, and they inherit from the item content type. The contact content type contains columns such as  **First Name**,  **Last Name**, and  **Job Title**.</span></span>
 

 
<span data-ttu-id="231e0-p110">Wenn Sie Ihrem SharePoint-Add-In einen Inhaltstyp hinzufügen, geben Sie den Basisinhaltstyp an, von dem der neue Inhaltstyp erben soll. Eine Vererbung ist beispielsweise von einer Ankündigung, einem Kontakt, einem Dokument oder von einem Element möglich. Danach konfigurieren Sie mit dem **Inhaltstyp**-Designer die Spalten für den Inhaltstyp und dessen Eigenschaften (wie Name und Beschreibung). Die von Ihnen gewählten Werte werden den Elementen `ContentType` und `FieldRef` in der Datei „Elements.xml“ hinzugefügt. Weitere Informationen finden Sie unter [Baustein: Inhaltstypen](http://msdn.microsoft.com/library/277dfc42-d9a8-4fae-9ae1-0d202b14674f%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="231e0-p110">When you add a content type to your SharePoint Add-in, you specify the base content type from which the new content type inherits. For example, it can inherit from an announcement, a contact, a document, or an item content type. You then use the  **Content Type** designer to configure the columns for the content type and its other properties, such as its name and its description. The values that you choose are added to the `ContentType` and `FieldRef` elements in the Elements.xml file. For more information, see [Building Block: SharePoint 2010 Content Types](http://msdn.microsoft.com/library/277dfc42-d9a8-4fae-9ae1-0d202b14674f%28Office.15%29.aspx).</span></span>
 

 

### <a name="empty-element"></a><span data-ttu-id="231e0-159">Leeres Element</span><span class="sxs-lookup"><span data-stu-id="231e0-159">Empty Element</span></span>

<span data-ttu-id="231e0-p111">Fügt Ihrer SharePoint-Add-In ein Projektelement für ein leeres Element hinzu. Dieses Projektelement enthält eine einzelne Datei (ELEMENTS.XML), in der Sie die Eigenschaften des Elements festlegen. Ein leeres Element wird in der Regel zur Definition eines Elements verwendet, für das Visual Studio keine Vorlage bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="231e0-p111">Adds a project item for an empty element to your SharePoint Add-in. This project item contains a single file, Elements.xml, where you define the properties of the element. You typically use an empty element to define an item for which Visual Studio doesn't provide a template.</span></span>
 

 

### <a name="list"></a><span data-ttu-id="231e0-163">Liste</span><span class="sxs-lookup"><span data-stu-id="231e0-163">List</span></span>

<span data-ttu-id="231e0-p112">Fügt Ihrem SharePoint-Add-In zwei Projektelemente hinzu: eine Listendefinition und eine Instanz der Liste. Wenn Sie Ihrem Add-In eine Liste hinzufügen, geben Sie an, wie die Liste genannt werden soll und ob eine leere Liste oder eine auf einem bestehenden Listentyp basierende Liste erstellt werden soll. Zudem geben Sie an, ob die Liste angepasst werden kann. Danach konfigurieren Sie mit dem **Listendesigner** die Spalten und Ansichten für die Liste sowie weitere Eigenschaften, wie den Namen und die Beschreibung der Liste. Weitere Informationen über Listeneigenschaften finden Sie unter [ListTemplate-Element (Listenvorlage)](http://msdn.microsoft.com/library/e565ead9-adcb-4a90-97e3-04850719420a%28Office.15%29.aspx) und [ListInstance-Element (Listeninstanz)](http://msdn.microsoft.com/library/cfefe8e5-2656-4d71-bb4e-5f991a800598%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="231e0-p112">Adds two project items to your SharePoint Add-in: a list definition and an instance of the list. When you add a list to your add-in, you specify what to name the list and whether to create either a blank list or a list that's based on an existing list type. You also specify whether the list can be customized. Then you use the  **List Designer** to configure the columns and views for the list and other properties, such as the list's name and description. For more information about list properties, see [ListTemplate Element (List Template)](http://msdn.microsoft.com/library/e565ead9-adcb-4a90-97e3-04850719420a%28Office.15%29.aspx) and [ListInstance Element (List Instance)](http://msdn.microsoft.com/library/cfefe8e5-2656-4d71-bb4e-5f991a800598%28Office.15%29.aspx).</span></span>
 

 

### <a name="menu-item-custom-action"></a><span data-ttu-id="231e0-169">Benutzerdefinierte Aktion für Menüelement</span><span class="sxs-lookup"><span data-stu-id="231e0-169">Menu Item Custom Action</span></span>

<span data-ttu-id="231e0-p113">Fügt ein Projektelement hinzu, das die Benutzeroberfläche der entsprechenden Hostwebsite erweitert, indem einem Listenmenü eine Aktion hinzugefügt wird. Die benutzerdefinierte Menüaktion umfasst eine Datei vom Typ "Elements.xml", in der die Eigenschaften der Aktion definiert werden. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit Add-Ins für SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="231e0-p113">Adds a project item that extends the UI of its host site by adding an action to a list menu. The menu custom action contains an Elements.xml file, which you use to define the properties of the action. For more information, see  [Create custom actions to deploy with SharePoint Add-ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span></span>
 

 

### <a name="module"></a><span data-ttu-id="231e0-173">Modul</span><span class="sxs-lookup"><span data-stu-id="231e0-173">Module</span></span>

<span data-ttu-id="231e0-p114">Fügt Ihrem SharePoint-Add-In ein Modul-Projektelement hinzu. Module sind einfach ausgedrückt Behälter, mit denen Sie bei der Bereitstellung Ihres SharePoint-Add-Ins weitere Dateien einschließen können. Um eine Datei hinzuzufügen, kopieren Sie sie unter dem Modul im **Projektmappen-Explorer** in das Projekt. Ein Verweis auf die Datei wird der Datei ELEMENTS. XML für das Modul automatisch hinzugefügt. Der Verweis enthält den Pfad und die URL der neuen Datei. Die Datei SAMPLE.TXT für das Modul können Sie löschen, da sie lediglich als Beispiel dient.</span><span class="sxs-lookup"><span data-stu-id="231e0-p114">Adds a module project item to your SharePoint Add-in. Modules are basically containers that you can use to include other files when you deploy your SharePoint Add-in. To add a file, you copy it into the project under the module in  **Solution Explorer**. A reference to the file is automatically added to the Elements.xml file for the module, and the reference specifies the path and URL of the new file. You can delete the Sample.txt file that's included with the module because it's included only for example purposes.</span></span>
 

 

### <a name="remote-event-receiver"></a><span data-ttu-id="231e0-179">Remoteereignisempfänger</span><span class="sxs-lookup"><span data-stu-id="231e0-179">Remote Event Receiver</span></span>

<span data-ttu-id="231e0-p115">Fügt Ihrer SharePoint-Add-In ein Projektelement für einen Remoteereignisempfänger und Ihrer Lösung ein Webanwendungsprojekt hinzu, sofern noch kein solches Projekt vorhanden ist. Die Webanwendung enthält einen Webdienst, der dem Remoteereignisempfänger in Ihrer SharePoint-Add-In zugeordnet ist. Der Webdienst enthält eine Visual Basic- oder Visual C#-Codedatei, deren Code ausgeführt wird, wenn in der SharePoint-Add-In ein Listen-, ein Listenelement- oder ein Webelementereignis auftritt. Wenn eine Webanwendung vorhanden ist, wird sie der SharePoint-Add-In zugeordnet, und der Webdienst wird der Anwendung hinzugefügt. Weitere Informationen finden Sie unter  [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="231e0-p115">Adds a project item for a remote event receiver to your SharePoint Add-in and a web application project to your solution, if such a project isn't already present. The web application contains a web service that's associated with the remote event receiver in your SharePoint Add-in. The web service contains a Visual Basic or Visual C# code file whose code executes when a list, a list item, or a web item event occurs in the SharePoint Add-in. If a web application is present, it's associated with the SharePoint Add-in, and the web service is added to that application. For more information, see  [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins.md).</span></span>
 

 

### <a name="ribbon-custom-action"></a><span data-ttu-id="231e0-185">Benutzerdefinierte Menübandaktion</span><span class="sxs-lookup"><span data-stu-id="231e0-185">Ribbon Custom Action</span></span>

<span data-ttu-id="231e0-p116">Fügt ein Projektelement hinzu, das die Benutzeroberfläche der entsprechenden Hostwebsite erweitert, indem einem Menüband eine Aktion hinzugefügt wird. Die benutzerdefinierte Menübandaktion umfasst eine Datei vom Typ "Elements.xml", in der die Eigenschaften der Aktion definiert werden. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit Add-Ins für SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="231e0-p116">Adds a project item that extends the UI of its host site by adding an action to a ribbon. The ribbon custom action contains an Elements.xml file, which defines the properties of the action. For more information, see  [Create custom actions to deploy with SharePoint Add-ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span></span>
 

 

### <a name="search-configuration"></a><span data-ttu-id="231e0-189">Suchkonfiguration</span><span class="sxs-lookup"><span data-stu-id="231e0-189">Search Configuration</span></span>

<span data-ttu-id="231e0-190">Fügt ein Projektelement hinzu, das Ihnen das Importieren benutzerdefinierter Suchkonfigurationseinstellungen ermöglicht, die von einer SharePoint-Website exportiert wurden.</span><span class="sxs-lookup"><span data-stu-id="231e0-190">Adds a project item that enables you to import custom search configuration settings that have been exported from a SharePoint site.</span></span>
 

 

### <a name="site-column"></a><span data-ttu-id="231e0-191">Websitespalte</span><span class="sxs-lookup"><span data-stu-id="231e0-191">Site Column</span></span>

<span data-ttu-id="231e0-p117">Fügt Ihrer SharePoint-Add-In ein Projektelement für eine Websitespalte hinzu. Die Websitespalte enthält eine Datei ELEMENTS.XML, die die  `Field`-Eigenschaften der Websitespalte definiert, einschließlich der folgenden Daten.</span><span class="sxs-lookup"><span data-stu-id="231e0-p117">Adds a project item for a site column to your SharePoint Add-in. The site column contains an Elements.xml file that defines the  `Field` properties of the site column, including the following data.</span></span>
 

 


|<span data-ttu-id="231e0-194">**Eigenschaftenname**</span><span class="sxs-lookup"><span data-stu-id="231e0-194">**Property Name**</span></span>|<span data-ttu-id="231e0-195">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="231e0-195">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="231e0-196">ID</span><span class="sxs-lookup"><span data-stu-id="231e0-196">ID</span></span>|<span data-ttu-id="231e0-197">Ein eindeutiger GUID-Wert für die Websitespalte.</span><span class="sxs-lookup"><span data-stu-id="231e0-197">A unique GUID value for the site column.</span></span>|
|<span data-ttu-id="231e0-198">Name</span><span class="sxs-lookup"><span data-stu-id="231e0-198">Name</span></span>|<span data-ttu-id="231e0-199">Ein eindeutiger Name, der als Verweis auf die Websitespalte dient.</span><span class="sxs-lookup"><span data-stu-id="231e0-199">A unique name that's used to reference the site column.</span></span>|
|<span data-ttu-id="231e0-200">DisplayName</span><span class="sxs-lookup"><span data-stu-id="231e0-200">DisplayName</span></span>|<span data-ttu-id="231e0-201">Ein auf der Benutzeroberfläche angezeigter Anzeigename.</span><span class="sxs-lookup"><span data-stu-id="231e0-201">A friendly name that appears in the UI.</span></span>|
|<span data-ttu-id="231e0-202">Type</span><span class="sxs-lookup"><span data-stu-id="231e0-202">Type</span></span>|<span data-ttu-id="231e0-203">Der Datentyp der Websitespalte, der auf **SPFieldType** basiert, z. B. Boolesch, Nachschlagedaten oder Text.</span><span class="sxs-lookup"><span data-stu-id="231e0-203">The data type of the site column based on  **SPFieldType**, such as Boolean, lookup, or text.</span></span>|
|<span data-ttu-id="231e0-204">Required</span><span class="sxs-lookup"><span data-stu-id="231e0-204">Required</span></span>|<span data-ttu-id="231e0-205">Wenn die Spalte erforderlich ist, wird die Eigenschaft auf **True** festgelegt; anderenfalls wird die Eigenschaft auf **False** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="231e0-205">If the column is required, the property is set to  **True**; otherwise, the property is set to  **False**.</span></span>|
|<span data-ttu-id="231e0-206">Group</span><span class="sxs-lookup"><span data-stu-id="231e0-206">Group</span></span>|<span data-ttu-id="231e0-p118">Gibt den Namen der Gruppe an, der die Websitespalte zugeordnet ist. Der Standardwert für diese Eigenschaft lautet **Spalten benutzerdef. Website**.</span><span class="sxs-lookup"><span data-stu-id="231e0-p118">Specifies the name of the group to which the site column is assigned. The default value for this property is  **Custom Site Columns**.</span></span>|
<span data-ttu-id="231e0-209">Weitere Informationen finden Sie unter [Baustein: Spalten und Feldtypen](http://msdn.microsoft.com/library/58548ade-e439-4931-82a2-fa29bd5afdb7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="231e0-209">For more information, see  [Building Block: Columns and Field Types](http://msdn.microsoft.com/library/58548ade-e439-4931-82a2-fa29bd5afdb7%28Office.15%29.aspx).</span></span>
 

 

### <a name="workflow"></a><span data-ttu-id="231e0-210">Workflow</span><span class="sxs-lookup"><span data-stu-id="231e0-210">Workflow</span></span>

<span data-ttu-id="231e0-p119">Fügt Ihrer SharePoint-Add-In ein Projektelement für einen Microsoft Azure-Workflow hinzu. Weitere Informationen finden Sie unter  [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx). Wenn Sie diese Art von Element hinzufügen, geben Sie einen Namen für den Workflow an und definieren ihn als Listen- oder Website-Workflow. Ein Listenworkflow funktioniert nur mit einer Liste und ein Website-Workflow nur mit der SharePoint-Website. Bei der Erstellung des Workflows legen Sie zudem fest, ob dem Workflow automatisch Listen und Bibliotheken zugeordnet werden sollen, und wenn ja, welche. Für jede Zuordnung, die Sie hinzufügen, wird dem Workflowprojekt eine Datei hinzugefügt. Ein Workflow enthält die folgenden Dateien.</span><span class="sxs-lookup"><span data-stu-id="231e0-p119">Adds a project item for a Microsoft Azure workflow to your SharePoint Add-in. For more information, see  [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx). When you add this type of item, you specify a name for the workflow and whether it's a list or site workflow. As the names suggest, a list workflow works only with a list, and a site workflow works only with the SharePoint site. When you're creating the workflow, you also specify whether to automatically associate the workflow with lists and libraries, and if so, which ones. For every association that you add, a file for it is added to the workflow project. A workflow contains the following files.</span></span>
 

 


|<span data-ttu-id="231e0-218">**Dateiname**</span><span class="sxs-lookup"><span data-stu-id="231e0-218">**File Name**</span></span>|<span data-ttu-id="231e0-219">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="231e0-219">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="231e0-220">Elements.xml</span><span class="sxs-lookup"><span data-stu-id="231e0-220">Elements.xml</span></span>|<span data-ttu-id="231e0-p120">Gibt die Konfiguration des Workflows und die darin enthaltenen Dateien an, wie die Datei WORKFLOW.XAML und Zuordnungsdateien, sowie die Eigenschaften jeder Datei, wie URL, Typ und Pfad. Für jede Datei, die dem Workflowprojekt hinzugefügt wird, wird in der Datei ELEMENTS.XML für den Workflow ein entsprechender Bereich erstellt. Zuordnungsdateien in Listenworkflows erfordern eine Liste, damit sie über einen Verweis auf das Listentoken verfügen. In einem Website-Workflow wird eine GUID für die Website hinzugefügt. **Vorsicht** Da Visual Studio die Elemente in der Datei ELEMENTS.XML beibehält, raten wir von einer Änderung der Datei ab, es sei denn, Sie kennen die Auswirkungen der Änderungen genau.</span><span class="sxs-lookup"><span data-stu-id="231e0-p120">Specifies the configuration of the workflow and the files that it contains, such as the workflow.xaml file and association files, and the properties of each file, such as its URL, its type, and its path. For each file that's added to the workflow project, a corresponding section is added to the Elements.xml file for the workflow. Association files in list workflows require a list, so they have a reference to the list token. In a site workflow, a GUID is added for the site. **Caution**  Because Visual Studio maintains the items in the Elements.xml file, we recommend against changing it unless you're familiar with the impact of the changes.</span></span> |
|<span data-ttu-id="231e0-226">Workflow.xaml</span><span class="sxs-lookup"><span data-stu-id="231e0-226">Workflow.xaml</span></span>|<span data-ttu-id="231e0-p121">Der Designer für den Workflow. In dieser Datei können Sie dem Workflow Aktionen hinzufügen und deren Code und Eigenschaften festlegen.</span><span class="sxs-lookup"><span data-stu-id="231e0-p121">Represents the designer for the workflow. In this file, you add actions to the workflow and set their code and properties.</span></span>|
|<span data-ttu-id="231e0-229">WorkflowStartAssociation</span><span class="sxs-lookup"><span data-stu-id="231e0-229">WorkflowStartAssociation</span></span>|<span data-ttu-id="231e0-p122">Startet den Workflow manuell in SharePoint. Diese Datei wird dem Workflowprojekt hinzugefügt, wenn Sie das Kontrollkästchen **Benutzer startet den Workflow manuell** im Workflow-Assistenten aktivieren.</span><span class="sxs-lookup"><span data-stu-id="231e0-p122">Manually starts the workflow on SharePoint. This file is added to the workflow project if you select the  **A user manually starts the workflow** check box in the workflow wizard.</span></span>|
|<span data-ttu-id="231e0-232">ItemAddedAssociation</span><span class="sxs-lookup"><span data-stu-id="231e0-232">ItemAddedAssociation</span></span>|<span data-ttu-id="231e0-p123">Startet den Workflow manuell, sofern einer vorhanden ist, wenn ein Benutzer ein Element auf der Website oder in der Liste erstellt (je nach Workflowtyp). Diese Datei wird dem Workflowprojekt hinzugefügt, wenn Sie das Kontrollkästchen **Der Workflow wird automatisch gestartet, wenn ein Element hinzugefügt wird** im Workflow-Assistenten aktivieren.</span><span class="sxs-lookup"><span data-stu-id="231e0-p123">Starts the workflow automatically if one is present when a user creates an item in the site or list (depending on the workflow type). This file is added to the workflow project if you select the  **The workflow starts automatically when an item is added** check box in the workflow wizard.</span></span>|
|<span data-ttu-id="231e0-235">ItemUpdatedAssociation</span><span class="sxs-lookup"><span data-stu-id="231e0-235">ItemUpdatedAssociation</span></span>|<span data-ttu-id="231e0-p124">Startet den Workflow automatisch, sofern einer vorhanden ist, wenn ein Benutzer ein Element auf der Website oder in der Liste ändert (je nach Workflowtyp). Diese Datei wird dem Workflowprojekt hinzugefügt, wenn Sie das Kontrollkästchen **Der Workflow wird automatisch gestartet, wenn ein Element geändert wird** im Workflow-Assistenten aktivieren.</span><span class="sxs-lookup"><span data-stu-id="231e0-p124">Starts the workflow automatically, if one is present when a user changes an item in the site or list (depending on the workflow type). This file is added to the workflow project if you select the  **The workflow starts automatically when an item is changed** check box in the workflow wizard.</span></span>|
|<span data-ttu-id="231e0-238">WorkflowHistoryList</span><span class="sxs-lookup"><span data-stu-id="231e0-238">WorkflowHistoryList</span></span>|<span data-ttu-id="231e0-239">Die Datei, die dem Workflowprojekt hinzugefügt wird, wenn eine Verlaufsliste für den Workflow im Workflow-Assistenten erstellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="231e0-239">Represents the file that's added to the workflow project if you create a history list for the workflow in the workflow wizard.</span></span>|
|<span data-ttu-id="231e0-240">WorkflowTaskList</span><span class="sxs-lookup"><span data-stu-id="231e0-240">WorkflowTaskList</span></span>|<span data-ttu-id="231e0-241">Die Datei, die dem Workflowprojekt hinzugefügt wird, wenn eine Aufgabenliste für den Workflow im Workflow-Assistenten erstellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="231e0-241">Represents the file that's added to the workflow project if you create a task list for the workflow in the workflow wizard.</span></span>|

### <a name="workflow-custom-activity"></a><span data-ttu-id="231e0-242">Benutzerdefinierte Workflowaktivität</span><span class="sxs-lookup"><span data-stu-id="231e0-242">Workflow Custom Activity</span></span>

<span data-ttu-id="231e0-p125">Fügt Ihrer SharePoint-Add-In ein Projektelement für eine benutzerdefinierte Workflowaktivität hinzu. Durch Hinzufügen einer benutzerdefinierten Workflowaktivität können Sie zusätzliche Workflowaktionen erstellen, die dann als benutzerdefinierte Aktionen in SharePoint Designer 2013 importiert werden können. Die benutzerdefinierte Workflowaktivität umfasst eine Datei vom Typ "Elements.xml", in der die Eigenschaften der Aktion definiert werden, sowie eine XAML-Datei für den Workflow-Designer. Weitere Informationen finden Sie unter  [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="231e0-p125">Adds a project item for a workflow custom activity to your SharePoint Add-in. By adding a workflow custom activity, you can create additional workflow actions that you can then import as custom actions in SharePoint Designer 2013. The workflow custom activity contains an Elements.xml file, which defines the properties of the action, and a .xaml file for the workflow designer. For more information, see  [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="231e0-247">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="231e0-247">Additional resources</span></span>
<span data-ttu-id="231e0-248"><a name="SP15Projecttemplates_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="231e0-248"></span></span>


-  [<span data-ttu-id="231e0-249">Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="231e0-249">Tools and environments for developing SharePoint Add-ins</span></span>](tools-and-environments-for-developing-sharepoint-add-ins.md)
    
 
