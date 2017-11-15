---
title: Vorgehensweise Erstellen eine externe Liste mithilfe einer in SharePoint OData-Datenquelle
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 601fbfce-a0c6-43dd-8398-540d094c083c
ms.openlocfilehash: c0fe48ca9061d22f5aade9b3afbf15ba306f0ae0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint"></a><span data-ttu-id="a5cff-102">Vorgehensweise: Erstellen eine externe Liste mithilfe einer in SharePoint OData-Datenquelle</span><span class="sxs-lookup"><span data-stu-id="a5cff-102">How to: Create an external list using an OData data source in SharePoint</span></span>
<span data-ttu-id="a5cff-p101">In diesem Artikel erfahren Sie, wie Sie externe Listen programmgesteuert erstellen und an OData-basierte externe Inhaltstypen in SharePoint binden. Obwohl Hauptbenutzer oder SharePoint-Administrator eine externe Liste mithilfe von SharePoint Designer 2013 wahrscheinlich erstellen, wird ein Entwickler die Möglichkeit zum Erstellen von externer Listen mithilfe der Tools von deren Handel, Visual Studio 2012 und die Office Developer Tools für Visual Studio 2012 interessiert sein. Wird dadurch mehr Flexibilität zu Funktionen hinzuzufügen und um eine Lösung zu packen, die umfasst Features zur späteren Bereitstellung in eine Business Connectivity Services (BCS) oder viele Umgebungen hosten.</span><span class="sxs-lookup"><span data-stu-id="a5cff-p101">Learn how to create an external list programmatically and bind it to an OData-based external content type in SharePoint. Although a power user or SharePoint administrator will likely create an external list using SharePoint Designer 2013, a developer will be interested in the ability to create external lists using the tools of their trade, Visual Studio 2012 and the Office Developer Tools for Visual Studio 2012. This gives them more flexibility to add functionality and to package a solution that includes Business Connectivity Services (BCS) features for later deployment into one or many host environments.</span></span>
  
    
    


## <a name="prerequisites-for-creating-an-external-list"></a><span data-ttu-id="a5cff-106">Voraussetzungen für die Erstellung einer externen Liste</span><span class="sxs-lookup"><span data-stu-id="a5cff-106">Prerequisites for creating an external list</span></span>
<span data-ttu-id="a5cff-107"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="a5cff-107"></span></span>

<span data-ttu-id="a5cff-108">Die folgenden Komponenten sind erforderlich, damit eine externe Liste aus einer OData-Quelle zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="a5cff-108">The following components are needed to create an external list from an OData source:</span></span>
  
    
    

- <span data-ttu-id="a5cff-109">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a5cff-109">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="a5cff-110">SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5cff-110">SharePoint</span></span>
    
  
- <span data-ttu-id="a5cff-111">Office Developer Tools für Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a5cff-111">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="a5cff-112">Ein externen Inhaltstyp basierend auf einer OData-Quelle veröffentlicht: Anweisungen finden Sie unter  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a5cff-112">A published external content type based on an OData source: For instructions, see  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span>
    
  
<span data-ttu-id="a5cff-113">Informationen zum Einrichten einer SharePoint-Entwicklungsumgebung finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a5cff-113">For information about setting up a SharePoint development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

### <a name="core-concepts-for-creating-external-lists"></a><span data-ttu-id="a5cff-114">Zentrale Konzepte zum Erstellen von externer Listen</span><span class="sxs-lookup"><span data-stu-id="a5cff-114">Core concepts for creating external lists</span></span>

<span data-ttu-id="a5cff-115">Die folgenden Artikel enthalten Informationen zu SharePoint-Add-Ins und andere Hintergrundinformationen zum Erstellen von externer Listen.</span><span class="sxs-lookup"><span data-stu-id="a5cff-115">The following articles provide information about SharePoint Add-ins and other background information for creating external lists.</span></span>
  
    
    

<span data-ttu-id="a5cff-116">**In Tabelle 1. Kernkonzepte für externe Listen**</span><span class="sxs-lookup"><span data-stu-id="a5cff-116">**Table 1. Core concepts for external lists**</span></span>


|<span data-ttu-id="a5cff-117">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="a5cff-117">**Article title**</span></span>|<span data-ttu-id="a5cff-118">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="a5cff-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="a5cff-119">Erste Schritte mit den Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5cff-119">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md) <br/> |<span data-ttu-id="a5cff-120">Informationen Sie zu Business Connectivity Services und wie Sie externe Daten in SharePoint verfügbar machen können.</span><span class="sxs-lookup"><span data-stu-id="a5cff-120">Learn about Business Connectivity Services and how you can expose external data in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="a5cff-121">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="a5cff-121">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |<span data-ttu-id="a5cff-122">Erfahren Sie mehr über das neue App-Modell in SharePoint, mit dem Sie Apps, d. h. kleine, einfach zu verwendende Lösungen für Endbenutzer, erstellen können.</span><span class="sxs-lookup"><span data-stu-id="a5cff-122">Learn about the new app model in SharePoint that enables you to create apps, which are small, easy-to-use solutions for end users.</span></span>  <br/> |
| [<span data-ttu-id="a5cff-123">Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5cff-123">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx) <br/> |<span data-ttu-id="a5cff-124">In diesem Artikel erfahren Sie mehr über die verschiedenen Verfahren zum Hosten von SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="a5cff-124">Learn about the different ways that you can host SharePoint Add-ins.</span></span>  <br/> |
   

## <a name="create-a-new-external-list"></a><span data-ttu-id="a5cff-125">Erstellen Sie eine neue externe Liste</span><span class="sxs-lookup"><span data-stu-id="a5cff-125">Create a new external list</span></span>
<span data-ttu-id="a5cff-126"><a name="bkmk_CreateNewVList"> </a></span><span class="sxs-lookup"><span data-stu-id="a5cff-126"></span></span>

<span data-ttu-id="a5cff-127">Die folgenden Verfahren werden gezeigt, wie eine neue externe Liste erstellen, OData-basierten externen Inhaltstyp zu binden und Veröffentlichen in SharePointVisual Studio 2012 verwenden.</span><span class="sxs-lookup"><span data-stu-id="a5cff-127">The following procedures will show you how to create a new external list, bind it to OData-based external content type, and publish to SharePoint using Visual Studio 2012.</span></span>
  
    
    

> <span data-ttu-id="a5cff-128">**Hinweis:** Im ersten Schritt wird davon ausgegangen, dass Sie erfolgreich einen externen Inhaltstyp erstellt haben, wie unter  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="a5cff-128">**Note** The first step assumes that you have successfully created an external content type, as described in  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span> 
  
    
    


### <a name="to-add-an-external-list-automatically"></a><span data-ttu-id="a5cff-129">So fügen Sie eine externe Liste automatisch hinzu</span><span class="sxs-lookup"><span data-stu-id="a5cff-129">To add an external list automatically</span></span>


1. <span data-ttu-id="a5cff-p102">Wenn Sie eine einfache Liste, die angibt, was in Ihren externen Inhaltstyp ist dem Projekt hinzufügen möchten, können Sie die Visual Studio 2012 automatische Generierung von Tools verwenden. Die Liste wird erstellt, wenn der externe Inhaltstyp erstellt wird. Wenn Sie das Kontrollkästchen **Erstellen Listeninstanzen für die ausgewählten Datenentitäten (mit Ausnahme von Dienstvorgänge)** gefunden auswählen im zweite Schritt des automatische Generierung von Prozess (Wählen Sie im Schritt Datenentitäten), den Assistenten die XML-Deklaration erstellt und hinzufügen neue externe Inhaltstypen für jede Entität, die Sie ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="a5cff-p102">If you just want to add a simple list to your project that reflects what is in your external content type, you can use the Visual Studio 2012 autogeneration tools. The list is created when the external content type is created. When you select the **Create list instances for the selected data entities (except Service Operations)** check box found in the second step of the autogeneration process (Select the Data Entities step), the wizard creates the XML declarations and add new external content types for each entity you selected.</span></span>
    
  
2. <span data-ttu-id="a5cff-133">Drücken Sie F5 zum Bereitstellen des Projekts und die neue Liste wird auch bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="a5cff-133">Press F5 to deploy the project, and the new list is also deployed.</span></span>
    
  
<span data-ttu-id="a5cff-134">Zu Testzwecken sollten Sie die Datei AppManifest.xml ändern, sodass die Startseite der app die Liste ist, den, die Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="a5cff-134">For testing purposes, you may want to modify the AppManifest.xml file so that the starting page of the app is the list you just created.</span></span> 
  
    
    

### <a name="to-modify-the-appmanifestxml-file"></a><span data-ttu-id="a5cff-135">So ändern Sie die Datei AppManifest.xml</span><span class="sxs-lookup"><span data-stu-id="a5cff-135">To modify the AppManifest.xml file</span></span>


1. <span data-ttu-id="a5cff-136">Öffnen Sie die Datei „Appmanifest.xml“ im XML-Editor.</span><span class="sxs-lookup"><span data-stu-id="a5cff-136">Open the AppManifest.xml file using an XML editor.</span></span>
    
  
2. <span data-ttu-id="a5cff-137">Suchen Sie das \<StartPage\>-Tag.</span><span class="sxs-lookup"><span data-stu-id="a5cff-137">Find the \< tag.</span></span>
    
  
3. <span data-ttu-id="a5cff-138">Ändern Sie den Wert zu `~appWebUrl/Lists/Employees`.</span><span class="sxs-lookup"><span data-stu-id="a5cff-138">Change the value to  `~appWebUrl/Lists/Employees`.</span></span>
    
  
4. <span data-ttu-id="a5cff-139">Speichern Sie Ihre Änderungen.</span><span class="sxs-lookup"><span data-stu-id="a5cff-139">Save your changes.</span></span>
    
  

### <a name="to-publish-the-project"></a><span data-ttu-id="a5cff-140">Um das Projekt zu veröffentlichen</span><span class="sxs-lookup"><span data-stu-id="a5cff-140">To publish the project</span></span>


- <span data-ttu-id="a5cff-141">Drücken Sie F5, um das Projekt und die externe Liste bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a5cff-141">Press F5 to deploy your project and external list.</span></span> 
    
    <span data-ttu-id="a5cff-142">Öffnen Sie einen Webbrowser, und navigieren Sie zu der neuen Liste, die Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="a5cff-142">Open a web browser, and navigate to the new list you created.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="a5cff-143">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a5cff-143">Additional resources</span></span>
<span data-ttu-id="a5cff-144"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="a5cff-144"></span></span>


-  [<span data-ttu-id="a5cff-145">Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5cff-145">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a5cff-146">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5cff-146">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a5cff-147">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5cff-147">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a5cff-148">So geht's: Erstellen einer einfachen automatisch gehosteten App für SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5cff-148">How to: Create a basic autohosted app for SharePoint</span></span>](http://msdn.microsoft.com/library/0572894d-c437-4b7d-8ac6-8405496e2145%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="a5cff-149">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5cff-149">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  

