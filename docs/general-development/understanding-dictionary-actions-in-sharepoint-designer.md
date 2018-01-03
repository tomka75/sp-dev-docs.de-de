---
title: "Verstehen von Wörterbuchaktionen in SharePoint Designer 2013"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 73df233e-bad8-4ea1-b05d-61ecab597924
ms.openlocfilehash: 521a83199046ba17636ae41fc8834989d2a7cb91
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="understanding-dictionary-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="d7f1f-102">Verstehen von Wörterbuchaktionen in SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="d7f1f-102">Understanding Dictionary actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="d7f1f-103">Der Variablentyp "Wörterbuch" ist ein neuer Variablentyp in der Workflowplattform von SharePoint, die Sie mit SharePoint Designer 2013 verwenden können.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-103">The Dictionary variable type is a new variable type in the SharePoint Workflow platform that you can use with SharePoint Designer 2013.</span></span> 

   

## <a name="understanding-the-dictionary-variable-type"></a><span data-ttu-id="d7f1f-104">Grundlegendes zum Variablentyp "Wörterbuch"</span><span class="sxs-lookup"><span data-stu-id="d7f1f-104">Understanding the Dictionary variable type</span></span>
<span data-ttu-id="d7f1f-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="d7f1f-105"><a name="section1"> </a></span></span>

<span data-ttu-id="d7f1f-p101">Ein Workflow ist eine Folge von Aktionen, die zu einem gewünschten Ergebnis führen. Beim Erstellen eines Workflows müssen Sie häufig Werte für die Verwendung in anderen Teilen des Workflows in einer Variablen (Speichercontainer) speichern.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p101">A workflow is a series of actions that perform a desired outcome. As you build a workflow you often need to save values in a variable (storage container) to use in other parts of the workflow.</span></span>
  
    
    
<span data-ttu-id="d7f1f-p102">Wenn Sie eine Variable erstellen, müssen Sie dem Workflowmodul mitteilen, welche Art von Daten in der Variablen enthalten sind. Beispiel: Sie möchten den Namen eines Mitarbeiters in einer Variablen speichern. Der Name eines Mitarbeiters ist eine Zeichenfolge. Somit würden Sie eine Variable vom Typ **String** erstellen. Der Workflow könnte dann den Namen des Mitarbeiters, z. B. "John Doe", in der Variablen speichern.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p102">When you create a variable you need to tell the workflow engine what type of data will be contained in the variable. For example, you might want to save the name of an employee in a variable. The name of an employee is a string of characters so you would create a variable of type **String**. The workflow could then store the name of the employee, such as "John Doe," in the variable.</span></span> 
  
    
    

<span data-ttu-id="d7f1f-112">**Abbildung: Eine Zeichenfolgenvariable**</span><span class="sxs-lookup"><span data-stu-id="d7f1f-112">**Figure: A String variable**</span></span>

  
    
    

  
    
    
![Eine Zeichenfolgenvariable](../images/SPD-Dictionary-1a.png)
  
    
    
<span data-ttu-id="d7f1f-p103">SharePoint Designer 2013 verfügt über einen neuen Variablentyp **Wörterbuch**. Der Variablentyp **Wörterbuch** ist ein Container, der eine Auflistung von anderen Variablen enthalten soll. In Ihrem Workflow muss möglicherweise mehr als nur der Name des Mitarbeiters gespeichert werden. Sie müssen möglicherweise auch seine Adresse und sein Geburtsdatum speichern. Wenn Sie keine **Wörterbuch**-Variable verwenden, müssen Sie mehrere eigenständige Variablen erstellen. Dies kann schnell zu Schwierigkeiten in der Organisation und bei der Verwendung in der Workflowlogik führen. Eine **Wörterbuch**-Variable ermöglicht es, mehrere Datenpunkte in einer Variablen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p103">SharePoint Designer 2013 has a new variable type called **Dictionary**. The **Dictionary** variable type is a container designed to hold a collection of other variables. For example, your workflow might need to store more than just the name of the employee. It might also need to store his address and birth date. If you do not use the **Dictionary** variable you will have to create multiple stand-alone variables. This can quickly become difficult to organize and difficult to work with in the logic of the workflow. A **Dictionary** variable allows you to store multiple data points in a single variable.</span></span>
  
    
    
<span data-ttu-id="d7f1f-121">Die Abbildung veranschaulicht das Konzept.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-121">The figure illustrates the concept.</span></span>
  
    
    

<span data-ttu-id="d7f1f-122">**Abbildung: Eine Wörterbuchvariable**</span><span class="sxs-lookup"><span data-stu-id="d7f1f-122">**Figure: A Dictionary variable**</span></span>

  
    
    

  
    
    
![Eine Wörterbuchvariable](../images/SPD15-Dictionary-1b.png)
  
    
    

  
    
    

  
    
    

## <a name="workflow-actions-that-use-the-dictionary-variable-type"></a><span data-ttu-id="d7f1f-124">Workflowaktionen für den Variablentyp "Wörterbuch"</span><span class="sxs-lookup"><span data-stu-id="d7f1f-124">Workflow actions that use the Dictionary variable type</span></span>
<span data-ttu-id="d7f1f-125"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="d7f1f-125"><a name="section2"> </a></span></span>

<span data-ttu-id="d7f1f-p104">Ein Workflow besteht aus mehreren Aktionen, die während der Verarbeitung des Workflows ausgeführt werden. SharePoint Designer 2013 enthält viele verschiedene Aktionen. Beispielsweise gibt es eine Aktion zum Senden einer E-Mail, zum Erstellen eines Listenelements und zum Protokollieren von Nachrichten im Workflowverlauf.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p104">A workflow consists of multiple actions that are executed as the workflow is processed. SharePoint Designer 2013 contains many different actions. For example, there is an action to send an email message, create a list item, and log messages to workflow history.</span></span>
  
    
    
<span data-ttu-id="d7f1f-129">Im Folgenden sind die drei Aktionen aufgeführt, die speziell für den Variablentyp **Wörterbuch** entwickelt wurden.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-129">The following are the three actions specifically designed for the **Dictionary** variable type.</span></span>
  
    
    

- <span data-ttu-id="d7f1f-130">**Wörterbuch erstellen**</span><span class="sxs-lookup"><span data-stu-id="d7f1f-130">**Build Dictionary**</span></span>
    
  
- <span data-ttu-id="d7f1f-131">**Elemente in einem Wörterbuch zählen**</span><span class="sxs-lookup"><span data-stu-id="d7f1f-131">**Count Items in a Dictionary**</span></span>
    
  
- <span data-ttu-id="d7f1f-132">**Ein Element aus einem Wörterbuch abrufen**</span><span class="sxs-lookup"><span data-stu-id="d7f1f-132">**Get an Item from a Dictionary**</span></span>
    
  
<span data-ttu-id="d7f1f-133">Die Workflowaktionen für den Variablentyp Wörterbuch finden Sie in der Dropdownliste **Aktion**, wie in der Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-133">The workflow actions for the Dictionary variable type can be found on the **Action** drop-down list, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="d7f1f-134">**Abbildung: Wörterbuchaktionen**</span><span class="sxs-lookup"><span data-stu-id="d7f1f-134">**Figure: Dictionary actions**</span></span>

  
    
    

  
    
    
![Wörterbuchaktionen](../images/SPD15-Dictionary-2.png)
  
    
    

### <a name="create-variables-with-the-build-dictionary-action"></a><span data-ttu-id="d7f1f-136">Erstellen von Variablen mit der Aktion "Wörterbuch erstellen"</span><span class="sxs-lookup"><span data-stu-id="d7f1f-136">Create variables with the "Build Dictionary" action</span></span>

<span data-ttu-id="d7f1f-p105">Sie verwenden die Aktion **Wörterbuch erstellen**, um eine Variable vom Typ **Wörterbuch** zu erstellen. Sie geben den Inhalt des Wörterbuchs ein und geben dann den Namen des Wörterbuchs in der Variablenliste an.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p105">You use the **Build Dictionary** action to create a variable of type **Dictionary**. You enter the contents of the dictionary and then specify the name of the dictionary in the variable list.</span></span>
  
    
    
<span data-ttu-id="d7f1f-p106">Die Abbildung zeigt das Dialogfeld **Wörterbuch erstellen**. Beachten Sie, dass dem Wörterbuch drei Variablen hinzugefügt wurden: eine Zeichenfolge, eine ganze Zahl und eine Datum/Uhrzeit-Variable.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p106">The figure shows the **Build a Dictionary** dialog box. Notice that three variables have been added to the dictionary: a string, an integer, and a date/time.</span></span>
  
    
    

<span data-ttu-id="d7f1f-141">**Abbildung: Das Dialogfeld "Wörterbuch erstellen"**</span><span class="sxs-lookup"><span data-stu-id="d7f1f-141">**Figure: The "Build a Dictionary" dialog box**</span></span>

  
    
    

  
    
    
![Dialogfeld zum Erstellen eines Wörterbuchs](../images/SPD15-BuildADictionaryDialog.png)
  
    
    
<span data-ttu-id="d7f1f-p107">Ein **Wörterbuch** kann jeden Typ von Variable enthalten, der in der SharePoint-Workflowplattform verfügbar ist. In der folgenden Liste werden die verfügbaren Variablentypen definiert:</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p107">A **Dictionary** can contain any type of variable available in the SharePoint Workflow platform. The following list defines the variable types available:</span></span>
  
    
    

- <span data-ttu-id="d7f1f-145">**Boolean**: Ein Ja/Nein-Wert Wert</span><span class="sxs-lookup"><span data-stu-id="d7f1f-145">**Boolean**: A Yes or No value</span></span>
    
  
- <span data-ttu-id="d7f1f-146">**Date/Time**: Datum und Uhrzeit</span><span class="sxs-lookup"><span data-stu-id="d7f1f-146">**Date/Time**: A date and time</span></span>
    
  
- <span data-ttu-id="d7f1f-147">**Dictionary**: Eine Auflistung von Variablen</span><span class="sxs-lookup"><span data-stu-id="d7f1f-147">**Dictionary**: A collection of variables</span></span>
    
  
- <span data-ttu-id="d7f1f-148">**Guid**: Eine GUID (Globally Unique Identifier)</span><span class="sxs-lookup"><span data-stu-id="d7f1f-148">**Guid**: A Globally Unique Identifier (GUID)</span></span>
    
  
- <span data-ttu-id="d7f1f-149">**Integer**: Eine ganze Zahl ohne Dezimalstellen</span><span class="sxs-lookup"><span data-stu-id="d7f1f-149">**Integer**: A whole number without decimals</span></span>
    
  
- <span data-ttu-id="d7f1f-150">**Number**: Eine Zahl, die Dezimalstellen enthalten kann</span><span class="sxs-lookup"><span data-stu-id="d7f1f-150">**Number**: A number that can contain decimals</span></span>
    
  
- <span data-ttu-id="d7f1f-151">**Zeichenfolge**: Eine Folge aus Zeichen</span><span class="sxs-lookup"><span data-stu-id="d7f1f-151">**String**: A string of characters</span></span>
    
  

    
> <span data-ttu-id="d7f1f-152">**Wichtig:** Der Variablentyp **Wörterbuch** ist wichtig bei der Verwendung der Aktion **HTTP-Webdienst aufrufen**.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-152">**Important:** The **Dictionary** variable type is critical when you are using the **Call HTTP Web Service** action.</span></span>
  
    
    


    
> <span data-ttu-id="d7f1f-153">**Vorsicht:** Sie können das Feld **Name** nur für die Suche verwenden, wenn Sie einen Wert in einem Wörterbuch festlegen.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-153">**Caution:** Using the **Name** field as a lookup is only supported when you are setting a value in a dictionary.</span></span> <span data-ttu-id="d7f1f-154">Wenn Sie ein Wörterbuch aufbauen, wird das Feld **Name** nicht für die Suche unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-154">Using the **Name** field as a lookup is not supported when you are building a dictionary.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="d7f1f-155">Eine **Dictionary**-Variable kann eine Variable vom Typ **Wörterbuch** enthalten.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-155">Note: A **Dictionary** variable can contain a variable of type **Dictionary**.</span></span> <span data-ttu-id="d7f1f-156">Die Möglichkeit, **Dictionary**-Variablen in einem **Wörterbuch** zu speichern, bietet eine Reihe von Vorteilen.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-156">The ability to store **Dictionary** variables within a **Dictionary** provides a number of benefits.</span></span> <span data-ttu-id="d7f1f-157">Sie können z. B. ein **Wörterbuch** erstellen, um Informationen über Mitarbeiter zu speichern.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-157">For example, you might create a **Dictionary** to store information about employees.</span></span> <span data-ttu-id="d7f1f-158">Innerhalb des **Wörterbuchs** können Sie einen weiteren **Wörterbuch**-Eintrag für jeden Mitarbeiter erstellen.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-158">Within the **Dictionary** you might create another **Dictionary** entry for each employee.</span></span> <span data-ttu-id="d7f1f-159">Wenn Sie den Workflow erstellen, können Sie die **Wörterbuch**-Variable verwenden, anstatt ständig neue eigenständige Variablen für jede Information zu jedem Mitarbeiter zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-159">As you build the workflow you can use the **Dictionary** variable instead of constantly creating new stand-alone variables for each piece of information about each employee.</span></span> <span data-ttu-id="d7f1f-160">Wie in diesem Beispiel gezeigt, kann ein **Wörterbuch** verwendet werden, um komplexe Informationen im Workflow zu organisieren.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-160">As this example shows, a **Dictionary** can be used to organize complex information within the workflow.</span></span>
  
    
    


### <a name="count-and-store-variables-with-the-count-items-in-a-dictionary-action"></a><span data-ttu-id="d7f1f-161">Ermitteln und Speichern von Variablen mit der Aktion „Elemente in einem Wörterbuch zählen“</span><span class="sxs-lookup"><span data-stu-id="d7f1f-161">Count and store variables with the "Count Items in a Dictionary" action</span></span>

<span data-ttu-id="d7f1f-p110">Mit der Aktion **Elemente in einem Wörterbuch zählen** zählen Sie die Variablen, die ein **Wörterbuch** enthält, und speichern diese Zahl dann in einer ganzzahligen Variablen. Anschließend können Sie die Anzahl von Elementen zum Durchlaufen des **Wörterbuchs** verwenden.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p110">You use the **Count Items in a Dictionary** action to count the variables that a **Dictionary** contains and then store that number in an Integer variable. You can then use the item count to loop through the **Dictionary**.</span></span>
  
    
    
<span data-ttu-id="d7f1f-164">Die Abbildung zeigt die Workflowaktion **Elemente in einem Wörterbuch zählen**.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-164">The figure shows the **Count Items in a Dictionary** workflow action.</span></span>
  
    
    

<span data-ttu-id="d7f1f-165">**Abbildung: Elemente in einem Wörterbuch zählen**</span><span class="sxs-lookup"><span data-stu-id="d7f1f-165">**Figure: Count items in a Dictionary**</span></span>

  
    
    

  
    
    
![Zählen von Elementen in einem Wörterbuch.](../images/SPD15-CountItemsInDictionary.png)
  
    
    

  
    
    

  
    
    

### <a name="retrieve-variables-with-the-get-an-item-from-a-dictionary-action"></a><span data-ttu-id="d7f1f-167">Abrufen von Variablen mit der Aktion "Ein Element aus einem Wörterbuch abrufen"</span><span class="sxs-lookup"><span data-stu-id="d7f1f-167">Retrieve variables with the "Get an Item from a Dictionary" action</span></span>

<span data-ttu-id="d7f1f-p111">Mit der Aktion **Ein Element aus einem Wörterbuch abrufen** rufen Sie eine im **Wörterbuch** gespeicherte Variable ab und platzieren sie in einer Variablen. Dies ist hilfreich, wenn Sie einen Wert aus dem Wörterbuch in einer eigenständigen Variablen gespeichert benötigen. Sie können einen Wert durch Eingeben des Namens der Variablen abrufen.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p111">You use the **Get an Item from a Dictionary** action to retrieve a variable stored in the **Dictionary** and place it in a variable. This is valuable when you need a value in the dictionary stored in a stand-alone variable. You can retrieve a value by entering the name of the variable.</span></span>
  
    
    
<span data-ttu-id="d7f1f-p112">Die Abbildung zeigt die Workflowaktion **Ein Element aus einem Wörterbuch abrufen**. Beachten Sie, dass **Age** der Name der Variablen im **Wörterbuch** ist, die in eine neue **Integer**-Variable ausgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="d7f1f-p112">The figure shows the **Get an Item from a Dictionary** workflow action. Notice that **Age** is the name of the variable in the **Dictionary** and it is being output to a new **Integer** variable.</span></span>
  
    
    

<span data-ttu-id="d7f1f-173">**Abbildung: Ein Element aus einem Wörterbuch abrufen**</span><span class="sxs-lookup"><span data-stu-id="d7f1f-173">**Figure: Get an item from a Dictionary**</span></span>

  
    
    

  
    
    
![Ein Element aus einem Wörterbuch abrufen.](../images/SPD15-GetAnItemFromDictionary.png)
  
    
    

  
    
    

  
    
    

## <a name="see-also"></a><span data-ttu-id="d7f1f-175">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d7f1f-175">See also</span></span>
<span data-ttu-id="d7f1f-176"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d7f1f-176"><a name="bk_addresources"> </a></span></span>


-  <span data-ttu-id="d7f1f-177">[Workflow in SharePoint]((http://technet.microsoft.com/de-DE/sharepoint/jj556245.aspx))</span><span class="sxs-lookup"><span data-stu-id="d7f1f-177">[Workflow in SharePoint]((http://technet.microsoft.com/de-DE/sharepoint/jj556245.aspx))</span></span>
    
  
-  <span data-ttu-id="d7f1f-178">[Neu in SharePoint-Workflows]((http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx))</span><span class="sxs-lookup"><span data-stu-id="d7f1f-178">[What's new in workflow in SharePoint]((http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx))</span></span>
    
  
-  <span data-ttu-id="d7f1f-179">[Erste Schritte mit SharePoint-Workflows]((http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx))</span><span class="sxs-lookup"><span data-stu-id="d7f1f-179">[Getting started with SharePoint workflow]((http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx))</span></span>
    
  

  
    
    

