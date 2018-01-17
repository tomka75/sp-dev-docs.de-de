---
title: Verstehen von Ereignisaktionen in SharePoint Designer 2013
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fe4ad8cf-2c6f-488d-8b33-6bf4357018ac
ms.openlocfilehash: 07ec3fe8c0a131b9f5a87df55e5745a664aba825
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="understanding-eventing-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="7acc5-102">Verstehen von Ereignisaktionen in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="7acc5-102">Understanding Eventing Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="7acc5-103">Informationen zur Verwendung von Ereignisaktionen in SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="7acc5-103">Learn to use Eventing Actions in SharePoint Designer 2013.</span></span>
## <a name="overview-of-eventing-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="7acc5-104">Übersicht über Ereignisaktionen in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="7acc5-104">Overview of Eventing Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="7acc5-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="7acc5-105"><a name="section1"> </a></span></span>

<span data-ttu-id="7acc5-p101">Ein SharePoint-Workflow kann eine Benachrichtigung beim Hinzufügen oder Ändern eines Elements abonnieren. Wenn ein Element hinzugefügt oder geändert wird, wird ein Ereignis aufgerufen. Ein Workflow kann auf diese Ereignisse warten, bevor mit dem Workflow fortgefahren wird. Die Ereignisaktionen in SharePoint Designer 2013 sind die folgenden:</span><span class="sxs-lookup"><span data-stu-id="7acc5-p101">A SharePoint workflow can subscribe to be notified when an item is added or changed. When an item is added or changed, it is called an event. A workflow can wait for these events to happen before proceeding with the workflow. The Eventing actions in SharePoint Designer 2013 are:</span></span> 
  
    
    

- <span data-ttu-id="7acc5-110">**Auf Ereignis in Listenelement warten:** Wird verwendet, damit gewartet wird, bis ein neues Element erstellt oder ein Element geändert wird.</span><span class="sxs-lookup"><span data-stu-id="7acc5-110">**Wait for Event in List Item:** Used to wait for a new item to be created or an item to be changed.</span></span>
    
  
- <span data-ttu-id="7acc5-111">**Auf Projektereignis warten:** Wird verwendet, damit gewartet wird, bis ein Projekt eingecheckt, zugesichert oder eingereicht wird.</span><span class="sxs-lookup"><span data-stu-id="7acc5-111">**Wait for Project Event:** Used to wait for a project to be checked in, committed, or submitted.</span></span>
    
  
- <span data-ttu-id="7acc5-112">**Auf Feldänderung im aktuellen Element warten:** Wird verwendet, damit gewartet wird, bis ein Feld im aktuellen Element geändert wird.</span><span class="sxs-lookup"><span data-stu-id="7acc5-112">**Wait for Field Change in Current Item:** Used to wait for a field to be changed in the current item.</span></span>
    
  
<span data-ttu-id="7acc5-113">Sie finden die Ereignisaktionen im Dropdownmenü **Aktion** im Menüband von SharePoint Designer 2013 (siehe Abbildungen unten).</span><span class="sxs-lookup"><span data-stu-id="7acc5-113">The Eventing actions are accessed in the **Action** drop-down menu of the SharePoint Designer 2013 ribbon as shown in the figures.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="7acc5-114">Die **Project Web App-Aktionen** sind nur verfügbar, wenn Sie mit einer Project Web App-Website arbeiten.</span><span class="sxs-lookup"><span data-stu-id="7acc5-114">The **Project Web App Actions** are only available when working with a Project Web App site.</span></span>
  
    
    


<span data-ttu-id="7acc5-115">**Ereignisaktion in SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="7acc5-115">**Eventing Action in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Ereignisaktionen in SharePoint Designer 2013](../images/SPD15-EventingActions1.png)
  
    
    

<span data-ttu-id="7acc5-117">**Project Web App-Ereignisaktion in SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="7acc5-117">**Project Web App Eventing Action in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Aktion zum Warten auf ein Projektereignis](../images/SPD15-EventingActions4.png)
  
    
    

<span data-ttu-id="7acc5-119">**Auf Feldänderung im aktuellen Element warten in SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="7acc5-119">**Wait for Field Change in Current Item event in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Auswählen von "Auf Feldänderung im aktuellen Element warten".](../images/wf15-eventingactions3.png)
  
    
    

  
    
    

  
    
    

## <a name="using-eventing-actions-in-sharepoint"></a><span data-ttu-id="7acc5-121">Verwenden von Ereignisaktionen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7acc5-121">Using Eventing Actions in SharePoint</span></span>
<span data-ttu-id="7acc5-122"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="7acc5-122"><a name="section2"> </a></span></span>

<span data-ttu-id="7acc5-p102">Ein Workflow sorgt für die Abstimmung von Geschäftsprozessen. In einem Geschäftsprozess ist es häufig wichtig zu warten, bis ein Element hinzugefügt oder in einer SharePoint-Liste aktualisiert wird. Das Verwenden der Ereignisaktionen ermöglicht es, auf ein Ereignis zu warten und dann eine Workflowaktion auszuführen.</span><span class="sxs-lookup"><span data-stu-id="7acc5-p102">A workflow orchestrates business processes. In a business process it is often important to wait for an item to be added or updated in a SharePoint list. Using the Eventing actions you can wait for an event to happen and then perform a workflow action.</span></span>
  
    
    
<span data-ttu-id="7acc5-p103">Die Ereignisaktionen befinden sich im Dropdown-Menü „Aktionen" im SharePoint Designer 2013-Menüband. Sie können die Aktion für den Workflow hinzufügen und sie dann entsprechend anpassen.</span><span class="sxs-lookup"><span data-stu-id="7acc5-p103">The Eventing actions are located on the Actions drop-down menu in the SharePoint Designer 2013 ribbon. You can add the action to your workflow and then customize it for your particular circumstance.</span></span>
  
    
    

### <a name="wait-for-event-in-list-item"></a><span data-ttu-id="7acc5-128">Auf Ereignis in Listenelement warten</span><span class="sxs-lookup"><span data-stu-id="7acc5-128">Wait for Event in List Item</span></span>

<span data-ttu-id="7acc5-129">Die Aktion **Auf Ereignis in Listenelement warten** enthält zwei Bereiche, die bearbeitet werden können, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7acc5-129">The **Wait for Event in List Item** action contains two editable regions, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="7acc5-130">**Auf Ereignis in Listenelement warten**</span><span class="sxs-lookup"><span data-stu-id="7acc5-130">**Wait for Event in List Item**</span></span>

  
    
    

  
    
    
![Aktion zum Warten auf ein Ereignis in SharePoint Designer 2013](../images/SPD15-EventingActions2.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="7acc5-132">Die zwei Bereiche, die bearbeitet werden können sind die folgenden:</span><span class="sxs-lookup"><span data-stu-id="7acc5-132">The two editable regions are:</span></span>
  
    
    

- <span data-ttu-id="7acc5-133">**Dieses Elementereignis:** Die Liste und das Ereignis, die überwacht werden.</span><span class="sxs-lookup"><span data-stu-id="7acc5-133">**This item event:** The list and event that will be monitored.</span></span>
    
  
- <span data-ttu-id="7acc5-p104">**Ausgabevariable:** Eine Variable, in der die GUID des Elements gespeichert wird, von dem das Ereignis stammt. Elemente müssen ein ID- und ein GUID-Feld aufweisen. Die ID ist in der Liste eindeutig, und eine GUID ist global eindeutig. Beispiel: die ID des ersten Elements in der Liste ist „1" und die ID des zweiten Elements ist „2". Die GUID ist global eindeutig und ist ein 128-Bit-Wert, der aus einer Gruppe von 8 Hexadezimalziffern, gefolgt von drei Gruppen von jeweils 4 Hexadezimalziffern besteht, auf die wiederum eine Gruppe von 12 Hexadezimalziffern folgt. Ein Beispiel für eine GUID ist: 6B29FC40-CA47-1067-B31D-00DD010662DA. Die Aktion **Auf Ereignis in Listenelement warten** ruft die GUID ab.</span><span class="sxs-lookup"><span data-stu-id="7acc5-p104">**Output variable:** A variable in which to save the GUID of the item from which the event originated. Items have both an ID and a GUID field. The ID is unique to the list and a GUID is globally unique. For example, the ID of the first item in the list will be the number 1 and the ID of the second item will be the number 2. The GUID is globally unique and in the format of a 128-bit value consisting of 8 hexadecimal digits, followed by three groups of 4 hexadecimal digits each, followed by one group of 12 hexadecimal digits. An example of a GUID is: 6B29FC40-CA47-1067-B31D-00DD010662DA. The **Wait for Event in List Item** action retrieves the GUID.</span></span>
    
  
<span data-ttu-id="7acc5-141">Durch Klicken auf den Link **Dieses Elementereignis** wird das Dialogfeld **Listeneintragsereignis auswählen** geöffnet, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7acc5-141">Clicking the **this item event** link opens the **Choose List Item Event** dialog box, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="7acc5-142">**Dialogfeld „Listeneintragsereignis auswählen"**</span><span class="sxs-lookup"><span data-stu-id="7acc5-142">**Choose List Item Event dialog box**</span></span>

  
    
    

  
    
    
![Dialog zum Auswählen eines Listenelementereignisses](../images/SPD15-EventingActions3.jpg)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="7acc5-p105">Die Dropdownliste **Ereignis** entspricht dem Ereignistyp. Es stehen die Optionen „Warten, bis ein Element zur Liste hinzugefügt wird" oder „Warten, bis ein Element in der Liste geändert wird" zur Verfügung. Die Dropdownliste **Liste** entspricht der Liste, die überwacht wird.</span><span class="sxs-lookup"><span data-stu-id="7acc5-p105">The **Event** drop-down list corresponds to the type of event. The options are to wait for an item to be added to a list or to wait for an item to be changed in a list. The **List** drop-down corresponds to the list that is monitored.</span></span>
  
    
    

### <a name="wait-for-project-event"></a><span data-ttu-id="7acc5-147">Auf Projektereignis warten</span><span class="sxs-lookup"><span data-stu-id="7acc5-147">Wait for Project Event</span></span>

<span data-ttu-id="7acc5-148">Die Aktion **Auf Projektereignis warten** enthält einen Bereich, der bearbeitet werden kann, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7acc5-148">The **Wait for Project Event** action contains one editable region, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="7acc5-149">**Auf Projektereignis warten**</span><span class="sxs-lookup"><span data-stu-id="7acc5-149">**Wait for Project Event**</span></span>

  
    
    

  
    
    
![Warten auf Projektereignis in Workflow](../images/SPD15-EventingActions5.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="7acc5-151">Der zu bearbeitende Bereich ist:</span><span class="sxs-lookup"><span data-stu-id="7acc5-151">The editable region is:</span></span>
  
    
    

- <span data-ttu-id="7acc5-152">**Dieses Projektereignis:** Das Projektereignis, auf das der Workflow warten soll.</span><span class="sxs-lookup"><span data-stu-id="7acc5-152">**This project event:** The project event that the workflow should wait for.</span></span>
    
  
<span data-ttu-id="7acc5-p106">In der Dropdownliste **Dieses Projektereignis** stehen drei Projektereignisse zur Auswahl. Diese umfassen das Warten, bis ein Projekt eingecheckt, zugesichert oder eingereicht wird.</span><span class="sxs-lookup"><span data-stu-id="7acc5-p106">The **This project event** drop-down includes three project events to choose from. These include waiting for the project to be checked in, committed, or submitted.</span></span>
  
    
    
<span data-ttu-id="7acc5-155">Sobald das Ereignis eingetreten ist, setzt der Workflow den Prozess fort.</span><span class="sxs-lookup"><span data-stu-id="7acc5-155">Once an event has occurred the workflow will continue to process.</span></span>
  
    
    

### <a name="wait-for-field-change-in-current-item"></a><span data-ttu-id="7acc5-156">Auf Feldänderung im aktuellen Element warten</span><span class="sxs-lookup"><span data-stu-id="7acc5-156">Wait for Field Change in Current Item</span></span>

<span data-ttu-id="7acc5-157">Die Aktion **Auf Feldänderung im aktuellen Listenelement warten** enthält zwei Bereiche, die bearbeitet werden können, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="7acc5-157">The **Wait for Field Change in Current Item** action contains two editable regions, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="7acc5-158">**Auf Feldänderung im aktuellen Element warten**</span><span class="sxs-lookup"><span data-stu-id="7acc5-158">**Wait for Field Change in Current Item**</span></span>

  
    
    

  
    
    
![Screenshot von Ereignisaktion.](../images/wf15-eventingactions4.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="7acc5-160">Die Bereiche, die bearbeitet werden können sind die folgenden:</span><span class="sxs-lookup"><span data-stu-id="7acc5-160">The editable regions are:</span></span>
  
    
    

- <span data-ttu-id="7acc5-161">**Feld:** Das Elementfeld, dessen Änderungen überwacht werden sollen.</span><span class="sxs-lookup"><span data-stu-id="7acc5-161">**Field:** The field in the item that should be monitored for change.</span></span>
    
  
- <span data-ttu-id="7acc5-162">**Wert:** Der Wert, den das Feld aufweisen muss, damit mit dem Workflow fortgefahren wird.</span><span class="sxs-lookup"><span data-stu-id="7acc5-162">**Value:** The value that the field should equal in order for the workflow to proceed.</span></span>
    
  
<span data-ttu-id="7acc5-163">Sobald ein Feld geändert hat, wird der Workflow fortgesetzt.</span><span class="sxs-lookup"><span data-stu-id="7acc5-163">Once a field has changed the workflow continues.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="7acc5-164">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="7acc5-164">See also</span></span>
<span data-ttu-id="7acc5-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7acc5-165"><a name="bk_addresources"> </a></span></span>


-  <span data-ttu-id="7acc5-166">[Workflows in SharePoint ](http://technet.microsoft.com/de-DE/sharepoint/jj556245.aspx)</span><span class="sxs-lookup"><span data-stu-id="7acc5-166">[Workflow in SharePoint ](http://technet.microsoft.com/de-DE/sharepoint/jj556245.aspx)</span></span>
    
  
-  <span data-ttu-id="7acc5-167">[Neuerungen bei SharePoint-Workflows](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)</span><span class="sxs-lookup"><span data-stu-id="7acc5-167">[What's new in workflow in SharePoint](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)</span></span>
    
  
-  <span data-ttu-id="7acc5-168">[Erste Schritte mit SharePoint-Workflows](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)</span><span class="sxs-lookup"><span data-stu-id="7acc5-168">[Getting started with SharePoint workflow](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)</span></span>
    
  
-  [<span data-ttu-id="7acc5-169">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="7acc5-169">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="7acc5-170">Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)</span><span class="sxs-lookup"><span data-stu-id="7acc5-170">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  

  
    
    

