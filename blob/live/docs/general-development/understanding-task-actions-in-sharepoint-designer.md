---
title: Verstehen von Aufgabenaktionen in SharePoint Designer 2013
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 6fd69e94-ebe1-4d5d-98db-b2f3ce16f098
ms.openlocfilehash: ea78cffb454521f88e01fede693a4659594b7e42
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="understanding-task-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="ea7fc-102">Verstehen von Aufgabenaktionen in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="ea7fc-102">Understanding Task Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="ea7fc-103">Hier lernen, mit Aufgabenaktionen in SharePoint Designer 2013 zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-103">Learn to use Task Actions in SharePoint Designer 2013.</span></span>
||
|:-----|
||
   

## <a name="overview-of-task-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="ea7fc-104">Übersicht über Aufgabenaktionen in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="ea7fc-104">Overview of Task Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="ea7fc-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="ea7fc-105"><a name="section1"> </a></span></span>

<span data-ttu-id="ea7fc-106">In SharePoint werden Aufgaben dazu verwendet, Personen oder Gruppen Arbeiten zuzuweisen und den Arbeitsfortschritt nachzuverfolgen.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-106">A task in SharePoint is used to assign work to a person or group and then track the progress of that work over time.</span></span> <span data-ttu-id="ea7fc-107">In SharePoint Designer 2013 gibt es zwei Workflowaktionen für die Arbeit mit Aufgaben.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-107">There are two workflow actions in SharePoint Designer 2013 designed for working with tasks.</span></span>
  
    
    
<span data-ttu-id="ea7fc-108">Konkret sind das die folgenden Aktionen:</span><span class="sxs-lookup"><span data-stu-id="ea7fc-108">These actions are:</span></span>
  
    
    

- <span data-ttu-id="ea7fc-109">**Aufgabe zuweisen** wird verwendet, um eine SharePoint-Aufgabe zu erstellen und einem einzelnen Teilnehmer zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-109">**Assign a task** is used to create a SharePoint task and assign it to a single participant.</span></span>
    
  
- <span data-ttu-id="ea7fc-110">**Vorgangsprozess starten** wird verwendet, um eine Aufgabe mehreren Teilnehmern zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-110">**Start a task process** is used to assign a task to multiple participants.</span></span>
    
  
<span data-ttu-id="ea7fc-111">Sie finden die Aufgabenaktionen im Dropdown-Menü **Aktion** im Menüband von SharePoint Designer 2013, wie in der Abbildung unten zu sehen ist.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-111">The Task Actions are accessed in the **Action** drop-down menu of the SharePoint Designer 2013 ribbon, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="ea7fc-112">**Abbildung: Aufgabenaktionen in SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="ea7fc-112">**Figure: Task Actions in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Aufgabenaktionen sind im Dropdown-Menü "Aktion" des Menübands von SharePoint Designer 2013 Preview verfügbar](../images/spd15-TaskActions1.png)
  
    
    

  
    
    

  
    
    

## <a name="using-task-actions-in-sharepoint"></a><span data-ttu-id="ea7fc-114">Verwenden von Aufgabenaktionen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ea7fc-114">Using Task Actions in SharePoint</span></span>
<span data-ttu-id="ea7fc-115"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="ea7fc-115"><a name="section2"> </a></span></span>

<span data-ttu-id="ea7fc-p102">Ein Geschäftsprozess besteht häufig aus Aufgaben, die von Personen ausgeführt werden müssen. Ein Workflow koordiniert die einzelnen Prozesschritte. Ein Workflow verwendet Aufgabenaktionen, um Personen Aufgaben zuzuweisen. Beispielsweise müssen verschiedenen Aufgaben durchgeführt werden, wenn ein Unternehmen einen neuen Mitarbeiter anstellt. Eine dieser Aufgaben könnte die Mitarbeitereinführung sein. Für diese Aufgabe könnte dann ein Mitarbeiter der Personalabteilung verantwortlich sein.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-p102">A business process often consists of tasks that must be performed by people. A workflow orchestrates the steps of a process. A workflow uses Task Actions to assign tasks to people. For example, when a new employee is hired a number of tasks need to be performed. One such task might be a new employee orientation. The task might need to be performed by a member of the Human Resources department.</span></span>
  
    
    
<span data-ttu-id="ea7fc-p103">Die Aktionen **Aufgabe zuweisen** und **Vorgangsprozess starten** befinden sich im Dropdown-Menü **Aktionen** auf dem Menüband in SharePoint Designer 2013. Sie können einem Workflow Aktionen hinzufügen und Sie an Ihre Bedürfnisse anpassen. Die Aktion **Aufgabe zuweisen** wird verwendet, um eine Aufgabe einem einzelnem Teilnehmer zuzuweisen. Die Aktion **Vorgangsprozess starten** wird verwendet, um eine Aufgabe mehreren Teilnehmern zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-p103">The **Assign a task** and **Start a task process** actions are located on the **Actions** drop-down menu in the SharePoint Designer 2013 ribbon. You can add the actions to your workflow and then customize them for your particular circumstance. The **Assign a task** action is used to assign a task to a single participant. The **Start a task process** action is used to assign a task to multiple participants.</span></span>
  
    
    

### <a name="assign-a-task"></a><span data-ttu-id="ea7fc-126">Zuweisen einer Aufgabe</span><span class="sxs-lookup"><span data-stu-id="ea7fc-126">Assign a task</span></span>

<span data-ttu-id="ea7fc-127">Die untenstehende Abbildung zeigt die Aktion **Aufgabe zuweisen**.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-127">The **Assign a task** action is shown in the figure.</span></span>
  
    
    

<span data-ttu-id="ea7fc-128">**Abbildung: Aktion "Aufgabe zuweisen" in SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="ea7fc-128">**Figure: The Assign a task action in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Aktion "Eine Aufgabe zuweisen" in SharePoint Designer 2013.](../images/SPD15-TaskActions2.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="ea7fc-130">Für die Aktion **Assign a task** werden drei Eingaben benötigt: der Benutzer, dem die Aufgabe zugeteilt werden soll, die Variable "Ergebnis" und die Variable "Aufgaben-ID.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-130">The **Assign a task** action takes three inputs: the user to assign a task, the outcome variable, and the task id variable.</span></span>
  
    
    

- <span data-ttu-id="ea7fc-p104">**this user**: Öffnet das Dialogfenster **Aufgabe zuweisen** (siehe Abbildung unten). In diesem Dialogfenster können Sie verschiedene Parameter festlegen: Teilnehmer, Aufgabentitel, Beschreibung, Fälligkeitsdatum, Aufgabenoptionen, E-Mail-Optionen und Ergebnisoptionen.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-p104">**this user**: Opens the **Assign a Task** dialog as shown in the figure. Use the dialog to set the participant, task title, description, due date, task options, email options, and outcome options.</span></span>
    
  
- <span data-ttu-id="ea7fc-133">**Variable: Outcome**: Hiermit wird die Variable zugewiesen, die das Ergebnis der Aufgabe enthält.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-133">**Variable: Outcome**: Assigns the variable that will hold the outcome of the task.</span></span>
    
  
- <span data-ttu-id="ea7fc-134">**Variable: TaskID**: Hiermit wird die Variable zugewiesen, die die Aufgaben-ID enthält.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-134">**Variable: TaskID**: Assigns the variable that will hold the id of the task.</span></span>
    
  

<span data-ttu-id="ea7fc-135">**Abbildung: Dialogfenster "Aufgabe zuweisen"**</span><span class="sxs-lookup"><span data-stu-id="ea7fc-135">**Figure: The Assign a Task dialog box**</span></span>

  
    
    

  
    
    
![Verwenden Sie das Dialogfeld "Eine Aufgaben zuweisen", um Teilnehmer, Aufgabentitel, Beschreibung, Fälligkeitsdatum, Aufgabenoptionen, E-Mail-Optionen und Ergebnisoptionen festzulegen.](../images/SPD15-TaskActions3.png)
  
    
    

  
    
    

  
    
    

### <a name="start-a-task-process"></a><span data-ttu-id="ea7fc-137">Aufgabenprozess starten</span><span class="sxs-lookup"><span data-stu-id="ea7fc-137">Start a task process</span></span>

<span data-ttu-id="ea7fc-138">Die untenstehende Abbildung zeigt die Aktion **Vorgangsprozess starten**.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-138">The **Start a task process** action is shown in the figure.</span></span>
  
    
    

<span data-ttu-id="ea7fc-139">**Abbildung: Die Aktion "Vorgangsprozess starten".**</span><span class="sxs-lookup"><span data-stu-id="ea7fc-139">**Figure: The "Start a task process" action.**</span></span>

  
    
    

  
    
    
![Die Aktion "Einen Aufgabenprozess starten" akzeptiert zwei Eingaben: "Benutzer" und eine "Ergebnis"-Variable](../images/SPD15-TaskActions4.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="ea7fc-141">Für die Aktion **Vorgangsprozess starten** werden zwei Eingaben benötigt: die Bentutzer, die an der Aufgabe teilnehmen werden und die Variable "Ergebnis".</span><span class="sxs-lookup"><span data-stu-id="ea7fc-141">The **Start a task process** action takes two inputs: the users that will participate in the task and the outcome variable.</span></span>
  
    
    

- <span data-ttu-id="ea7fc-p105">**these users**: Öffnet das Dialogfenster **Vorgangsprozess starten**, wie in der Abbildung unten zu sehen ist. In diesem Dialogfenster können Sie verschiedene Parameter festlegen: Teilnehmer, Aufgabentitel, Beschreibung, Fälligkeitsdatum, Aufgabenoptionen, E-Mail-Optionen und Ergebnisoptionen.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-p105">**these users**: Opens the **Start a Task Process** dialog box as shown in the figure. Use the dialog box to set the participants, task title, description, due date, task options, email options, and outcome options.</span></span>
    
  
- <span data-ttu-id="ea7fc-144">**Variable: Outcome**: Hiermit wird die Variable zugewiesen, die das Ergebnis des Vorgangsprozesses enthält.</span><span class="sxs-lookup"><span data-stu-id="ea7fc-144">**Variable: Outcome**: Assigns the variable that holds the outcome of the task process.</span></span>
    
  

<span data-ttu-id="ea7fc-145">**Abbildung: Dialogfenster "Vorgangsprozess starten"**</span><span class="sxs-lookup"><span data-stu-id="ea7fc-145">**Figure: The Start a Task Process dialog box**</span></span>

  
    
    

  
    
    
![Verwenden Sie das Dialogfeld "Einen Aufgabenprozess starten", um Teilnehmer, Aufgabentitel, Beschreibung, Fälligkeitsdatum, Aufgabenoptionen, E-Mail-Optionen und Ergebnisoptionen festzulegen.](../images/SPD15-TaskActions5.png)
  
    
    

  
    
    

  
    
    

## <a name="see-also"></a><span data-ttu-id="ea7fc-147">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ea7fc-147">See also</span></span>
<span data-ttu-id="ea7fc-148"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ea7fc-148"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="ea7fc-149">Neuerungen in SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="ea7fc-149">What's new in workflow in SharePoint</span></span>](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [<span data-ttu-id="ea7fc-150">Erste Schritte mit SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="ea7fc-150">Getting started with SharePoint workflow</span></span>](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [<span data-ttu-id="ea7fc-151">Workflowentwicklung in SharePoint Designer und Visio</span><span class="sxs-lookup"><span data-stu-id="ea7fc-151">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="ea7fc-152">Kurzübersicht zu Workflowaktionen (SharePoint-Workflowplattform)</span><span class="sxs-lookup"><span data-stu-id="ea7fc-152">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  

  
    
    

