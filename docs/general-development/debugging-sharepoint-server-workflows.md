---
title: Debuggen von SharePoint-Workflows
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a5adf39b-8640-4871-be60-b786dcf9fafc
ms.openlocfilehash: 49dd0e9ee38d6c1211af4dd813d1e932f480e830
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="debugging-sharepoint-workflows"></a><span data-ttu-id="a8f84-102">Debuggen von SharePoint-Workflows</span><span class="sxs-lookup"><span data-stu-id="a8f84-102">Debugging SharePoint workflows</span></span>
<span data-ttu-id="a8f84-103">Hier finden Sie Erläuterungen dazu, wie SharePoint jetzt Workflow-Manager 1.0 für die Workflowverarbeitung und -verwaltung nutzt. Außerdem werden die Debugoptionen vorgestellt.</span><span class="sxs-lookup"><span data-stu-id="a8f84-103">Demonstrates how SharePoint now relies on Workflow Manager 1.0 for all workflow processing and management, and demonstrates debugging options.</span></span>
 <span data-ttu-id="a8f84-104">**Bereitgestellt von:** [Andrew Connell](http://social.msdn.microsoft.com/profile/andrew%20connell%20%5bmvp%5d/), [www.AndrewConnell.com](http://www.andrewconnell.com)</span><span class="sxs-lookup"><span data-stu-id="a8f84-104">**Provided by:** [Andrew Connell](http://social.msdn.microsoft.com/profile/andrew%20connell%20%5bmvp%5d/),  [www.AndrewConnell.com](http://www.andrewconnell.com)</span></span>
  
    

<span data-ttu-id="a8f84-105">Microsoft setzt in SharePoint auf einen anderen Ansatz als in früheren Versionen von SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a8f84-105">Microsoft has taken a different approach to workflows in SharePoint than in previous versions of SharePoint.</span></span> <span data-ttu-id="a8f84-106">Das Workflow-Team hat mit dem Azure-Team gearbeitet, um ein neues Produkt namens „Workflow-Manager“ zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-106">The workflow team worked with the Azure team to create a new product called Workflow Manager.</span></span> <span data-ttu-id="a8f84-107">Workflow-Manager hostet die neueste Version der Windows Workflow Foundation-Laufzeit und alle erforderlichen Dienste auf verfügbare und skalierbare Weise.</span><span class="sxs-lookup"><span data-stu-id="a8f84-107">Workflow Manager hosts the latest version of the Windows Workflow Foundation runtime and all the necessary services in an available and scalable way.</span></span> <span data-ttu-id="a8f84-108">Er nutzt die den Microsoft Azure Service Bus für Leistung und Skalierbarkeit und führt bei Bereitstellung genau die gleiche lokale Bereitstellung wie in der Cloud aus, ähnlich wie Office 365.</span><span class="sxs-lookup"><span data-stu-id="a8f84-108">It takes advantage of the Microsoft Azure Service Bus for performance and scalability, and when deployed, it runs exactly the same in an on-premises deployment as in the cloud, similar to Office 365.</span></span> <span data-ttu-id="a8f84-109">SharePoint wird dann verbunden und so konfiguriert, dass die gesamte Workflowausführung sowie zugehörige Aufgaben an die Workflow-Manager-Farm übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="a8f84-109">SharePoint is then connected and configured to hand off all workflow execution and related tasks to the Workflow Manager farm.</span></span>
  
    
    
<span data-ttu-id="a8f84-110">Diese Änderung in der Architektur erfordert einige Änderungen an den beiden primären Workflow-Erstellungstools (SharePoint Designer 2013 und Visual Studio 2012), mit denen Kunden benutzerdefinierte Workflows erstellten.</span><span class="sxs-lookup"><span data-stu-id="a8f84-110">This change in the architecture required some changes to the two primary workflow authoring tools (SharePoint Designer 2013 and Visual Studio 2012) customers used to create custom workflows.</span></span> <span data-ttu-id="a8f84-111">Die von Entwicklern in SharePoint 2007 und SharePoint 2010 verwendeten Debugging-Techniken gelten jedoch weiterhin.</span><span class="sxs-lookup"><span data-stu-id="a8f84-111">However, the debugging techniques employed by developers in SharePoint 2007 and SharePoint 2010 still apply.</span></span> <span data-ttu-id="a8f84-112">Die neue Architektur ermöglicht eine neue Option für Workflows, die mithilfe von SharePoint Designer 2013 oder Visual Studio 2012 erstellt wurden, dahingehend, dass Fiddler zum Überwachen des Verkehrs zwischen SharePoint und Workflow-Manager verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="a8f84-112">The new architecture allows for a new option for workflows created using either SharePoint Designer 2013 or Visual Studio 2012 in that Fiddler can be used to monitor traffic between SharePoint and Workflow Manager.</span></span>
  
    
    

## <a name="sharepoint-workflow-debugging-overview"></a><span data-ttu-id="a8f84-113">Überblick über das Workflowdebugging in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8f84-113">SharePoint workflow debugging overview</span></span>

<span data-ttu-id="a8f84-114">Das Debuggen benutzerdefinierter Workflows, die für SharePoint erstellt wurden, funktioniert auf die gleiche Weise wie in früheren Versionen, einschließlich SharePoint 2010 und SharePoint 2007. </span><span class="sxs-lookup"><span data-stu-id="a8f84-114">Debugging custom workflows created for SharePoint resembles previous versions, including SharePoint 2010 and SharePoint 2007.</span></span> <span data-ttu-id="a8f84-115">Welche Debuggingoptionen verfügbar sind, hängt von dem Tool ab, das zum Erstellen des Workflows verwendet wird (SharePoint Designer 2013 oder Visual Studio 2012), sowie von der Art der SharePoint-Bereitstellung, ob lokal oder Office 365 (gehostet).</span><span class="sxs-lookup"><span data-stu-id="a8f84-115">Some debugging options available will depend on the tool that is used to create the workflow (SharePoint Designer 2013 or Visual Studio 2012) and the kind of SharePoint deployment, such as on-premises or Office 365 (hosted).</span></span>
  
    
    
<span data-ttu-id="a8f84-116">Es gibt vier Verfahren zum Debuggen von Workflows, die Workflowautoren nutzen können:</span><span class="sxs-lookup"><span data-stu-id="a8f84-116">There are four workflow debugging techniques that can be leveraged by workflow authors:</span></span>
  
    
    

- <span data-ttu-id="a8f84-117">Protokollieren in der Workflowverlaufsliste</span><span class="sxs-lookup"><span data-stu-id="a8f84-117">Logging to the workflow history list</span></span>
    
  
- <span data-ttu-id="a8f84-118">Setzen von Haltepunkten</span><span class="sxs-lookup"><span data-stu-id="a8f84-118">Setting breakpoints</span></span>
    
  
- <span data-ttu-id="a8f84-119">Senden von Debugmeldungen an die Konsole</span><span class="sxs-lookup"><span data-stu-id="a8f84-119">Sending debug messages to the console</span></span>
    
  
- <span data-ttu-id="a8f84-120">Überwachen des Verkehrs zwischen SharePoint und Workflow-Manager mit Fiddler</span><span class="sxs-lookup"><span data-stu-id="a8f84-120">Monitoring traffic between SharePoint and Workflow Manager with Fiddler</span></span>
    
  
<span data-ttu-id="a8f84-p105">Jede Option hat ihre Vor- und Nachteile. Es ist hilfreich, wenn Sie wissen, was jeweils mit den beiden Workflowerstellungstools (SharePoint Designer 2013 oder Visual Studio 2012) sowie mit dem Typ der Workflowbereitstellung (lokal oder Office 365) möglich ist. Die folgende Tabelle zeigt eine Matrix der Erstellungstools, Bereitstellungsziele und der für die das jeweilige Szenario verfügbaren Optionen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p105">Each option has advantages and disadvantages. It helps to have an understanding of what is possible when using the two workflow authoring tools (SharePoint Designer 2013 or Visual Studio 2012), as well as the type of workflow deployment (on-premises or Office 365). The following table contains a matrix of authoring tools, deployment targets, and the options available in each scenario.</span></span>
  
    
    


||<span data-ttu-id="a8f84-124">**SharePoint lokal**</span><span class="sxs-lookup"><span data-stu-id="a8f84-124">**SharePoint On-Premises**</span></span>|<span data-ttu-id="a8f84-125">**Office 365 SharePoint Online**</span><span class="sxs-lookup"><span data-stu-id="a8f84-125">**Office 365 SharePoint Online**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a8f84-126">SharePoint Designer 2013, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a8f84-126">SharePoint Designer 2013, SharePoint Online</span></span>  <br/> | <span data-ttu-id="a8f84-127">Protokollieren In Verlaufsliste</span><span class="sxs-lookup"><span data-stu-id="a8f84-127">Log to history list</span></span> <br/>  <span data-ttu-id="a8f84-128">Fiddler</span><span class="sxs-lookup"><span data-stu-id="a8f84-128">Fiddler</span></span> <br/> | <span data-ttu-id="a8f84-129">Protokollieren In Verlaufsliste</span><span class="sxs-lookup"><span data-stu-id="a8f84-129">Log to history list</span></span> <br/> |
|<span data-ttu-id="a8f84-130">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a8f84-130">Visual Studio 2012</span></span>  <br/> | <span data-ttu-id="a8f84-131">Protokollieren In Verlaufsliste</span><span class="sxs-lookup"><span data-stu-id="a8f84-131">Log to history list</span></span> <br/>  <span data-ttu-id="a8f84-132">Haltepunkte</span><span class="sxs-lookup"><span data-stu-id="a8f84-132">Breakpoints</span></span> <br/>  <span data-ttu-id="a8f84-133">Debugmeldungen in Konsole</span><span class="sxs-lookup"><span data-stu-id="a8f84-133">Console debug messages</span></span> <br/>  <span data-ttu-id="a8f84-134">Fiddler</span><span class="sxs-lookup"><span data-stu-id="a8f84-134">Fiddler</span></span> <br/> | <span data-ttu-id="a8f84-135">Protokollieren in Verlaufsliste</span><span class="sxs-lookup"><span data-stu-id="a8f84-135">Log to history list</span></span> <br/>  <span data-ttu-id="a8f84-136">Haltepunkte</span><span class="sxs-lookup"><span data-stu-id="a8f84-136">Breakpoints</span></span> <br/> |
   

## <a name="debugging-with-the-workflow-history-list"></a><span data-ttu-id="a8f84-137">Debuggen mit der Workflowverlaufsliste</span><span class="sxs-lookup"><span data-stu-id="a8f84-137">Debugging with the workflow history list</span></span>

<span data-ttu-id="a8f84-p106">Die einzige Debugoption, die in jeder SharePoint-Bereitstellung verfügbar ist, ist das Schreiben von Protokollmeldungen in die Workflowverlaufsliste. Mit dieser Methode können Sie entweder die Aktion **In Verlaufsliste protokollieren** in SharePoint Designer 2013 oder die Aktivität **WriteToHistory** in Visual Studio 2012 verwenden, um eine Zeichenfolgenmeldung als neues Element zur Liste hinzuzufügen, die in der Workflowzuordnung angegeben ist. Hierbei handelt es sich um den Container für alle Verlaufsprotokollmeldungen. Es kann sich um einfache Zeichenfolgen oder eine Zusammensetzung aus dem Variableninhalt im Workflow handeln.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p106">The only debugging option that is available in every type of SharePoint deployment is writing log messages to the workflow history list. By using this method, you can use either the **Log to History List** action in SharePoint Designer 2013 or the **WriteToHistory** activity in Visual Studio 2012 to write a string message as a new item to the list, specified in the workflow association, which is the container for all history logging messages. These can be simple strings or constructed by concatenating the contents of variables within the workflow.</span></span>
  
    
    
<span data-ttu-id="a8f84-p107">Es ist nicht ideal, die Verlaufsliste als Debugtool zu verwenden, da die Benutzer die Meldungen sehen können. Daher muss der Workflowentwickler nach Abschluss der Debugsitzung und Freigabe des Workflows für die Produktion diese Meldungen entfernen, sodass zwischen dem Debuggen und der Bereitstellung ein weiterer Arbeitsschritt anfällt. Dies bleibt jedoch weiterhin die einzige Option, die für jedes Szenario verfügbar ist, unabhägig von dem Tool, das zum Erstellen des Workflows verwendet wurde oder um welchen Typ von SharePoint-Bereitstellung es sich handelt.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p107">Using the history list as a debugging tool is not ideal because users can see the messages. Therefore, when the debugging session is complete and the workflow is used in production, the workflow developer will want to remove these messages, creating an additional step between debugging and deployment. Nonetheless, this is the only option available in any scenario, regardless of which tool is used to create the workflow or which type of SharePoint deployment.</span></span>
  
    
    

## <a name="debugging-using-visual-studio-2012-breakpoints"></a><span data-ttu-id="a8f84-144">Debuggen mit Visual Studio 2012-Haltepunkten</span><span class="sxs-lookup"><span data-stu-id="a8f84-144">Debugging using Visual Studio 2012 breakpoints</span></span>

<span data-ttu-id="a8f84-p108">Eine weitere Debugoption ist die Nutzung von Haltepunkten. Haltepunkte sind nur für Workflows verfügbar, die mit Visual Studio 2012 erstellt wurden, da in SharePoint Designer 2013 keine Möglichkeit zum Setzen von Haltepunkten oder zum Anfügen eines Debuggers an den laufenden Prozess verfügbar ist. Diese Möglichkeiten sind sowohl in lokalen SharePoint- als auch in gehosteten Bereitstellungen wie Office 365 verfügbar. In diesem Szenario setzen Sie einen Haltepunkt für eine Aktivität im Workflow und starten den Workflow dann im Debugmodus.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p108">Another debugging option is to take advantage of breakpoints. Breakpoints are available only for workflows created using Visual Studio 2012, since SharePoint Designer 2013 has no capability to set breakpoints or to attach a debugger to the running process. These are available in both SharePoint on-premises and hosted deployments such as Office 365. In this scenario, you would set a breakpoint on an activity within the workflow and then start the workflow in debug mode.</span></span>
  
    
    

<span data-ttu-id="a8f84-149">**Abbildung 1: Starten des Workflows**</span><span class="sxs-lookup"><span data-stu-id="a8f84-149">**Figure 1. Start the workflow**</span></span>

  
    
    

  
    
    
![Abbildung 1: Workflow wird gestartet](../images/ngDebuggingSP2013Workflows01.png)
  
    
    
<span data-ttu-id="a8f84-p109">Visual Studio stellt den Workflow in der SharePoint-Zielumgebung bereit und fügt einen Debugger an. Wenn der Workflowprozess die Aktivität mit dem Haltepunkt erreicht, wird Visual Studio wieder aufgerufen, sodass Sie die Werte der Workflowvariablen überprüfen und die einzelnen Aktivitäten über Visual Studio 2012 durchgehen können, wie in der folgenden Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p109">Visual Studio will deploy the workflow to the target SharePoint environment and attach a debugger. When the workflow process reaches the activity the breakpoint is set on, Visual Studio regains focus and lets you examine the values of workflow variables and step through each activity from Visual Studio 2012, as shown in the following figure.</span></span>
  
    
    

<span data-ttu-id="a8f84-153">**Abbildung 2: Workflow-Haltepunkt**</span><span class="sxs-lookup"><span data-stu-id="a8f84-153">**Figure 2. Workflow breakpoint**</span></span>

  
    
    

  
    
    
![Abbildung 2: Workflow-Haltepunkt](../images/ngDebuggingSP2013Workflows02.png)
  
    
    

  
    
    

  
    
    

## <a name="debugging-workflows-using-debug-messages-and-the-test-service-host"></a><span data-ttu-id="a8f84-156">Debuggen von Workflows mithilfe von Debugmeldungen und des Testdiensthosts</span><span class="sxs-lookup"><span data-stu-id="a8f84-156">Debugging workflows using debug messages and the test service host</span></span>

<span data-ttu-id="a8f84-p111">Mit der Einführung von Workflow-Manager in SharePoint-Workflows stehen nun zwei neue Debugoptionen zur Verfügung, wenn Sie benutzerdefinierte Workflows mit Visual Studio 2012 erstellen und sie in einer lokalen Bereitstellung testen. Visual Studio 2012 umfasst eine **WriteLine** -Aktivität, die eine einzelne, zeichenfolgenbasierte Meldung als Eingabe akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p111">The introduction of Workflow Manager to the SharePoint workflow story introduces two new debugging opportunities available when you are creating custom workflows using Visual Studio 2012 and testing them in an on-premises deployment. Visual Studio 2012 includes a **WriteLine** activity that accepts a single string-based message as an input.</span></span>
  
    
    

<span data-ttu-id="a8f84-159">**Abbildung 3: WriteLine-Aktivität**</span><span class="sxs-lookup"><span data-stu-id="a8f84-159">**Figure 3. WriteLine activity**</span></span>

  
    
    

  
    
    
![Abbildung 3: WriteLine-Aktivität](../images/ngDebuggingSP2013Workflows.png)
  
    
    
<span data-ttu-id="a8f84-p113">Diese Aktivität schreibt die Meldung, die die **System.Diagnostics.Debug.WriteLine()**-Methode darstellt, in eine standardmäßige .NET-Windows-Konsolenanwendung. Das Workflow-Manager 1.0-Entwicklungstool beinhaltet das Konsolendienstprogramm **Test Service Host**, das von Visual Studio 2012 beim Starten einer neuen Debugsitzung und beim Testen mit einer lokalen SharePoint-Bereitstellung geöffnet wird. Dieses Konsolendienstprogramm, **Microsoft.Workflow.TestServiceHost.exe** in **C:\\Program Files (x86)\\Workflow Manager Tools\\1.0**, wird an die registrierte Workflow-Manager-Instanz angefügt und überwacht Meldungen, die von der **WriteLine**-Aktivität ausgegeben werden, wie in der folgenden Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p113">This activity will write the message that resembles the **System.Diagnostics.Debug.WriteLine()** method in a standard .NET Windows Console Application. The Workflow Manager 1.0 development tool includes a console utility that is named the **Test Service Host** that Visual Studio 2012 will open when a new debugging session is started and when testing with an on-premises SharePoint deployment. This console utility, **Microsoft.Workflow.TestServiceHost.exe** found in **C:\\Program Files (x86)\\Workflow Manager Tools\\1.0**, attaches to the registered Workflow Manager instance and listens for messages written using the **WriteLine** activity, as shown in the following figure.</span></span>
  
    
    

<span data-ttu-id="a8f84-165">**Abbildung 4: Meldungen für WriteLine-Aktivität**</span><span class="sxs-lookup"><span data-stu-id="a8f84-165">**Figure 4. Messages for WriteLine activity**</span></span>

  
    
    

  
    
    
![Abbildung 4: Nachrichten für WriteLine-Aktivität](../images/ngDebuggingSP2013Workflows04.png)
  
    
    
<span data-ttu-id="a8f84-p115">Diese Meldungen sehen aus wie Codekommentare oder Debugmeldungen in einer Konsolenanwendung. Im Gegensatz zum Schreiben in die Workflowverlaufsliste müssen Sie diese nicht entfernen, bevor Sie den Workflow in der Produktionsumgebung bereitstellen. Solange das **Test Service Host**-Dienstprogramm nicht mit Workflow-Manager verbunden ist, sind die Meldungen nicht von Bedeutung.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p115">These messages resemble code comments or debug messages in a console application. Unlike writing to the workflow history list, you don't need to remove these before deploying the workflow to production. Unless the **Test Service Host** utility is connected to Workflow Manager, the messages are harmless.</span></span>
  
    
    
<span data-ttu-id="a8f84-p116">Diese Debugoption ist nicht für Workflows verfügbar, die mit SharePoint Designer 2013 erstellt wurden, da keine Aktion vorhanden ist, die der **WriteLine**-Aktivität zugeordnet ist. Diese Debugoption steht leider nur für lokale SharePoint-Installationen zur Verfügung, da auf den vom Test Service Host-Dienstprogramm verwendeten Port normalerweise nicht von außerhalb des lokalen Netzwerks öffentlich zugegriffen werden kann. Dies gilt auch für Office 365. Die Ports, die SharePoint für die Verbindung mit Workflow-Manager verwendet, sind die gleichen, die der Test Service Host verwendet. Auf sie kann nur innerhalb des vertrauenswürdigen Netzwerks zugegriffen werden. Dies bedeutet jedoch nicht, dass Sie die Workflows ändern müssen, um **WriteLine**-Aktivitäten vor der Bereitstellung in Office 365 zu entfernen. Diese Aktivitäten können im Workflow verbleiben, da sie nicht sichtbar sind, solange der **Test Service Host** nicht mit Workflow-Manager verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p116">This debugging option is not available for workflows created using SharePoint Designer 2013, because there is no action that maps to the **WriteLine** activity. Unfortunately, this debugging option is available only to SharePoint on-premises installations, since the port used by the Test Service Host utility is typically not publically accessible outside an on-premises network. This is also true for Office 365. The ports SharePoint uses to connect to Workflow Manager are the same ones used by the Test Service Host, and those are only accessible within the trusted network. However, this does not mean that you need to change their workflows to remove any **WriteLine** activities before deployment to Office 365. These activities can be left in the workflow as they are not seen unless the **Test Service Host** is connected to Workflow Manager.</span></span>
  
    
    

## <a name="debugging-using-fiddler-to-monitor-http-traffic"></a><span data-ttu-id="a8f84-177">Debuggen mit Fiddler zum Überwachen des HTTP-Datenverkehrs</span><span class="sxs-lookup"><span data-stu-id="a8f84-177">Debugging using Fiddler to monitor HTTP traffic</span></span>

<span data-ttu-id="a8f84-178">Die letzte Option zum Debuggen von SharePoint-Workflows ist eine neue Ergänzung für Workflowentwickler aufgrund der Änderung bei der Verarbeitung von Workflows in der aktuellen Plattform.</span><span class="sxs-lookup"><span data-stu-id="a8f84-178">The last debugging option for SharePoint workflows is a new addition for workflow developers due to the change in how workflows are handled in the current platform.</span></span> <span data-ttu-id="a8f84-179">Bedenken Sie, dass in SharePoint der gesamte Workflowprozess an ein externes Produkt übergeben wird, und zwar Workflow Manager 1.0</span><span class="sxs-lookup"><span data-stu-id="a8f84-179">Recall that in SharePoint, all workflow processing is handed off to an external product, Workflow Manager 1.0.</span></span> <span data-ttu-id="a8f84-180">Wenn ein Workflow mit SharePoint kommunizieren muss, z. B. beim Aktualisieren des aktuellen Status des Workflows, beim Sammeln von Daten aus Elementen oder Benutzern oder beim Arbeiten mit Aufgaben, nutzen Aktivitäten von Workflow-Manager die SharePoint-REST-API für diese Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="a8f84-180">When a workflow has to communicate with SharePoint, such as updating the current state of the workflow, collecting data from items or users in a SharePoint site, or when working with tasks, Workflow Manager's activities leverage the SharePoint REST API to perform these operations.</span></span> <span data-ttu-id="a8f84-181">SharePoint kommuniziert mit Workflow-Manager über eine Clientbibliothek, die als Proxy für REST-Dienste dient, die von Workflow-Manager verfügbar gemacht werden.</span><span class="sxs-lookup"><span data-stu-id="a8f84-181">SharePoint communicates with Workflow Manager using a client library that serves as a proxy to REST services exposed by Workflow Manager.</span></span> <span data-ttu-id="a8f84-182">Sowohl SharePoint als auch Workflow-Manager kommunizieren über die Standard-HTTP- und -HTTPS-Protokolle miteinander.</span><span class="sxs-lookup"><span data-stu-id="a8f84-182">Both SharePoint and Workflow Manager communicate with one another using the standard HTTP and HTTPS protocols.</span></span>
  
    
    
<span data-ttu-id="a8f84-p118">Diese Architektur bietet Workflowerstellern eine neue Debugoption. Mithilfe des HTTP-Debugproxytools Fiddler können Sie alle Anforderungen und die entsprechenden Antworten zwischen den beiden Produkten überwachen. Darüber hinaus können auch alle benutzerdefinierten Dienste, die von den benutzerdefinierten Workflows mit der **HttpSend**-Aktivität in Visual Studio 2012 oder der entsprechenden **Call HTTP Web Service**-Aktion in SharePoint Designer 2013 aufgerufen werden, ebenso mit Fiddler überwacht und geprüft werden. Dieses Debugmodell ist unabhängig von dem Tool verfügbar, das Sie zum Erstellen von benutzerdefinierten Workflows verwenden (SharePoint Designer 2013 oder Visual Studio 2012).</span><span class="sxs-lookup"><span data-stu-id="a8f84-p118">This architecture yields a new debugging option for workflow authors. By using the HTTP debugging proxy tool Fiddler, you can monitor every request and corresponding response between the two products. In addition, any custom services called by the custom workflows using the **HttpSend** activity in Visual Studio 2012 or corresponding **Call HTTP Web Service** action in SharePoint Designer 2013 can also be monitored and inspected by Fiddler. This debugging model is also available, regardless of the tool that you use to create custom workflows (SharePoint Designer 2013 or Visual Studio 2012).</span></span>
  
    
    
<span data-ttu-id="a8f84-187">Diese Option ist nur dann nicht verfügbar, wenn Sie Workflows mithilfe einer Office 365-Bereitstellung von SharePoint testen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-187">The only time this option is not available is when you are testing workflows using an Office 365 deployment of SharePoint.</span></span> <span data-ttu-id="a8f84-188">Da der gesamte Datenverkehr zwischen SharePoint und Workflow-Manager serverseitig auftritt, ist es nicht möglich, eine Verbindung mit einem der Server in Office 365 herzustellen und Fiddler über die Konsole zu starten.</span><span class="sxs-lookup"><span data-stu-id="a8f84-188">Since all traffic between SharePoint and Workflow Manager occurs server-side, it is not possible to connect to one of the servers in Office 365 and start Fiddler from the console.</span></span>
  
    
    
<span data-ttu-id="a8f84-189">Diese Option bietet eine Transparenz und Einblicke in das Workflowmodul, die beim Entwickeln von Workflows in SharePoint-Versionen vor SharePoint nicht möglich waren.</span><span class="sxs-lookup"><span data-stu-id="a8f84-189">This new option gives you transparency and insight into the workflow engine that was not possible when developing workflows in previous versions of SharePoint before SharePoint.</span></span> 
  
    
    
<span data-ttu-id="a8f84-190">Sie können beispielsweise die unformatierten Antworten sehen, die von Workflow-Manager oder SharePoint in einem Webdienstaufruf zurückkommen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-190">For example, you can see the raw responses coming back from Workflow Manager or SharePoint in a web service call.</span></span> <span data-ttu-id="a8f84-191">Manchmal antwortet Workflow-Manager mit einer bestimmten Fehlermeldung.</span><span class="sxs-lookup"><span data-stu-id="a8f84-191">At times Workflow Manager may respond with a specific error message.</span></span> <span data-ttu-id="a8f84-192">SharePoint umfasst benutzerfreundliche Fehlermeldungen, diese sind aber möglicherweise nicht ausreichend spezifisch.</span><span class="sxs-lookup"><span data-stu-id="a8f84-192">SharePoint includes user-friendly error messages but these may not be sufficiently specific.</span></span> <span data-ttu-id="a8f84-193">Mithilfe von Fiddler können Sie die genaue Fehlermeldung sehen, die zur Problembehandlung zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="a8f84-193">Using Fiddler, you can see the exact error message returned to help troubleshoot the issue.</span></span> 
  
    
    
<span data-ttu-id="a8f84-p121">Ein anderer Anwendungsfall ist das Untersuchen der Antwort eines erfolgreichen Webdienstaufrufs. Wenn Sie Webdienste in Workflows verwenden, müssen Sie unabhängig vom Erstellungstool den genauen Eigenschaftennamen (und den Pfad, wenn es sich um eine komplexe Antwort handelt) für einen in einer Antwort enthaltenen Wert kennen. Mit Fiddler werden Ihnen die gesamten Antwortdaten angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p121">Another use case is examining the response from a successful web service call. When working with web services in workflows, regardless of the authoring tool, that you need to know the exact property name (and path if it is a complex response) for a value that is contained in a response. By using Fiddler, you can see the complete response data.</span></span>
  
    
    

### <a name="understanding-sharepoint-and-workflow-manager-for-debugging-with-fiddler"></a><span data-ttu-id="a8f84-197">Grundlegendes zu SharePoint und Workflow Manager für das Debuggen mit Fiddler</span><span class="sxs-lookup"><span data-stu-id="a8f84-197">Understanding SharePoint and Workflow Manager for debugging with Fiddler</span></span>

<span data-ttu-id="a8f84-p122">Um Workflows in SharePoint und Workflow-Manager 1.0 mit Fiddler debuggen zu können, müssen Sie vor dem Debuggen in einer Entwicklungsumgebung einige Konfigurations- und Einrichtungsschritte durchführen. Bevor Sie diese Schritte durchführen, ist es nützlich, die Funktionsweise von Fiddler sowie die Funktionsweise von Workflows in SharePoint zu kennen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p122">To debug workflows in SharePoint and Workflow Manager 1.0 with Fiddler, some configuration and setup steps must be performed in a developer environment before debugging. Before completing the steps, it helps to have an understanding of how Fiddler works and how workflows work in SharePoint.</span></span>
  
    
    

#### <a name="fiddler-can-only-inspect-traffic-from-the-local-server"></a><span data-ttu-id="a8f84-200">Fiddler kann nur Datenverkehr vom lokalen Server überprüfen</span><span class="sxs-lookup"><span data-stu-id="a8f84-200">Fiddler can only inspect traffic from the local server</span></span>

<span data-ttu-id="a8f84-201">Der einzige Datenverkehr, den Fiddler abfangen und überprüfen kann, sind Anforderungen, die vom lokalen Server stammen, auf dem Fiddler gestartet wurde.</span><span class="sxs-lookup"><span data-stu-id="a8f84-201">The only traffic Fiddler can intercept and inspect are requests originating from the local server where Fiddler was started.</span></span> <span data-ttu-id="a8f84-202">Dies kann eine Herausforderung darstellen, wenn Fiddler als Debugging-Tool für SharePoint-Workflows verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a8f84-202">This can present a challenge when Fiddler is used as a debugging tool for SharePoint workflows.</span></span> 
  
    
    
<span data-ttu-id="a8f84-203">Wenn SharePoint und Workflow Manager 1.0 auf unterschiedlichen Servern installiert sind und Fiddler von SharePoint Server gestartet wird, zeigt Fiddler nur den Datenverkehr an, wenn die Anforderung von SharePoint ausging.</span><span class="sxs-lookup"><span data-stu-id="a8f84-203">If SharePoint and Workflow Manager 1.0 are installed on different servers and if Fiddler is started from SharePoint Server, the only traffic that Fiddler will display is the traffic where the request originated from SharePoint.</span></span> <span data-ttu-id="a8f84-204">Der Datenverkehr, der von Workflow Manager 1.0 ausgeht, wird nicht abgefangen, selbst wenn sein Ziel SharePoint Server ist.</span><span class="sxs-lookup"><span data-stu-id="a8f84-204">None of the traffic originating from Workflow Manager 1.0, even if it is targeted to the SharePoint Server, will be intercepted.</span></span>
  
    
    
<span data-ttu-id="a8f84-205">Daher ist es beim Entwickeln von Workflows einfacher, sie zu debuggen, wenn sowohl SharePoint als auch Workflow Manager 1.0 auf demselben Server installiert sind. </span><span class="sxs-lookup"><span data-stu-id="a8f84-205">Therefore, when developing workflows, it is easier to debug them if both SharePoint and Workflow Manager 1.0 are installed on the same server.</span></span> <span data-ttu-id="a8f84-206">Beachten Sie, dass dies keine Voraussetzung ist. Sie können Fiddler sowohl auf SharePoint Server- als auch Workflow Manager-Servern starten, wobei es jedoch komplizierter ist, zwei Instanzen auf zwei Servern für den gleichen Workflowprozess zu überwachen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-206">Note that this is not a requirement; you can start Fiddler on both the SharePoint Server and Workflow Manager servers, although it is more complex to monitor two instances on two servers for the same workflow process.</span></span>
  
    
    

#### <a name="fiddler-can-only-inspect-traffic-from-the-current-logged-on-user"></a><span data-ttu-id="a8f84-207">Fiddler kann nur Datenverkehr des aktuell angemeldeten Benutzers überprüfen</span><span class="sxs-lookup"><span data-stu-id="a8f84-207">Fiddler can only inspect traffic from the current logged-on user</span></span>

 <span data-ttu-id="a8f84-p126">Fiddler kann nur den Datenverkehr des aktuell angemeldeten Benutzers abfangen und den Datenverkehr dieses Benutzers überprüfen. Um von SharePoint ausgehenden Datenverkehr anzuzeigen, müssen Sie sich bei SharePoint Server mit dem Windows-Konto anmelden, das als Identität für den Anwendungspool konfiguriert ist, der die Webanwendung für die SharePoint-Website hostet, von der der Workflow ausgeht.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p126">Fiddler can only intercept and inspect traffic from the current logged-on user. To view traffic that originated from SharePoint, you must log on to SharePoint Server using the Windows account that is configured as the identity of the application pool that hosts the web application for the SharePoint site initiating the workflow.</span></span>
  
    
    
<span data-ttu-id="a8f84-p127">Dies gilt auch für Workflow-Manager. Um von Workflow-Manager ausgehenden Datenverkehr abfangen und überprüfen zu können, müssen Sie sich mit der Windows-Identität anmelden, die bei der Bereitstellung der Workflow-Manager-Farm als Dienstkonto für Workflow-Manager konfiguriert wurde.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p127">The same is true with Workflow Manager. To intercept and inspect traffic that originates from Workflow Manager, you must log on to the server using the Windows identity configured during the provisioning of the Workflow Manager farm as the service account for Workflow Manager.</span></span>
  
    
    
<span data-ttu-id="a8f84-212">Bei der Verwendung von Fiddler zum Debuggen von Workflows ist das Debuggen nicht nur dann einfacher, wenn Workflow-Manager und SharePoint auf demselben Server installiert und konfiguriert sind, sondern wenn sie auch die gleiche Windows-Identität wie das Dienstkonto verwenden.</span><span class="sxs-lookup"><span data-stu-id="a8f84-212">When using Fiddler to debug workflows, it is easier to debug them if not only both Workflow Manager and SharePoint are installed and configured on the same server, but they also use the same Windows identity as the service account.</span></span> <span data-ttu-id="a8f84-213">Der gesamte Datenverkehr von Workflow-Manager und SharePoint kann von Fiddler abgefangen und überprüft werden.</span><span class="sxs-lookup"><span data-stu-id="a8f84-213">All traffic from both Workflow Manager and SharePoint can then be intercepted and inspected by Fiddler.</span></span>
  
    
    

#### <a name="sharepoint-must-trust-fiddlers-certificate"></a><span data-ttu-id="a8f84-214">SharePoint muss dem Fiddler-Zertifikat vertrauen</span><span class="sxs-lookup"><span data-stu-id="a8f84-214">SharePoint must trust Fiddler's certificate</span></span>

<span data-ttu-id="a8f84-215">Bevor Sie Fiddler zum Debuggen von SharePoint-Workflows verwenden, müssen Sie verstehen, wie verschlüsselter Datenverkehr behandelt wird.</span><span class="sxs-lookup"><span data-stu-id="a8f84-215">Before using Fiddler for debugging SharePoint workflows, you need to understand how encrypted traffic is handled.</span></span> <span data-ttu-id="a8f84-216">Verschlüsselter Datenverkehr über HTTP, der als HTTPS bezeichnet wird, wird mithilfe eines privaten Schlüssels eines Zertifikats implementiert, um einige Daten zu verschlüsseln und diese dann an einen anderen Empfänger zu senden.</span><span class="sxs-lookup"><span data-stu-id="a8f84-216">Encrypted traffic over HTTP, known as HTTPS, is implemented by using a certificate's private key to encrypt some data and then send it to another recipient.</span></span> <span data-ttu-id="a8f84-217">Der Empfänger hat den öffentlichen Schlüssel des Zertifikats, das mit dem privaten Schlüssel verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="a8f84-217">The recipient has the certificate's public key that is paired with the private key.</span></span> <span data-ttu-id="a8f84-218">Wenn eine Anforderung vom Empfänger empfangen wird, kann der Empfänger überprüfen, dass die Anforderung vom Absender stammte, da die Signatur des verschlüsselten Inhalts mit dem öffentlichen Schlüssel übereinstimmt, was nur dann der Fall sein kann, wenn dieser mit dem privaten Schlüssel des Zertifikats verschlüsselt wurde.</span><span class="sxs-lookup"><span data-stu-id="a8f84-218">When a request is received by the recipient, the recipient can validate that the request came from the sender because the encrypted content's signature matches the public key, which can only be true if it was encrypted with the certificate's private key.</span></span>
  
    
    
<span data-ttu-id="a8f84-219">Fiddler kann HTTPS-Verkehr abfangen und zum Entschlüsseln dieses Verkehrs konfiguriert werden, sodass ein lesbares Format zur Überprüfung im Tool entsteht.</span><span class="sxs-lookup"><span data-stu-id="a8f84-219">Fiddler can intercept HTTPS traffic and be configured to decrypt it so it is in a human-readable format for inspection in the tool.</span></span> <span data-ttu-id="a8f84-220">Nach der Anzeige der Anforderung verwendet Fiddler dann sein eigenes Zertifikat, um den Verkehr wieder zu verschlüsseln und ihn an den gewünschten Empfänger zu senden.</span><span class="sxs-lookup"><span data-stu-id="a8f84-220">After displaying the request, Fiddler then uses its own certificate to re-encrypt the traffic and send it to the intended recipient.</span></span> <span data-ttu-id="a8f84-221">Dies kann zu einem Problem führen, da der Empfänger jetzt die ursprüngliche Antwort erhalten hat, diese jedoch nicht mithilfe des Zertifikats vom ursprünglichen Absender gesichert wurde.</span><span class="sxs-lookup"><span data-stu-id="a8f84-221">This can cause an issue, though, because now the recipient received the original response but it is not secured using the certificate from the original sender.</span></span> <span data-ttu-id="a8f84-222">Dies kann beim Debuggen von SharePoint-Workflows ein Problem sein, da SharePoint dem Zertifikat von Fiddler nicht vertraut.</span><span class="sxs-lookup"><span data-stu-id="a8f84-222">This can be an issue when debugging SharePoint workflows because Fiddler's certificate is not trusted by SharePoint.</span></span> <span data-ttu-id="a8f84-223">Um Fiddler zum Abfangen und Überprüfen von HTTPS-Verkehr zwischen SharePoint und Workflow-Manager zu verwenden, muss das Fiddler-Zertifikat für SharePoint vertrauenswürdig sein.</span><span class="sxs-lookup"><span data-stu-id="a8f84-223">Therefore, in order to use Fiddler to intercept and inspect HTTPS traffic between SharePoint and Workflow Manager, the Fiddler certificate must be trusted by SharePoint.</span></span>
  
    
    

### <a name="configure-sharepoint-and-workflow-manager-10-for-workflow-debugging-with-fiddler"></a><span data-ttu-id="a8f84-224">Konfigurieren von SharePoint und Workflow-Manager 1.0 für das Workflowdebugging mit Fiddler</span><span class="sxs-lookup"><span data-stu-id="a8f84-224">Configure SharePoint and Workflow Manager 1.0 for workflow debugging with Fiddler</span></span>

<span data-ttu-id="a8f84-225">In den folgenden Abschnitten wird erläutert, wie Sie Fiddler und SharePoint für das Workflowdebugging konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="a8f84-225">The following sections explain how to configure Fiddler and SharePoint for workflow debugging.</span></span>
  
    
    

#### <a name="configure-the-net-framework-default-proxy-configuration"></a><span data-ttu-id="a8f84-226">.NET Framework-Standardproxykonfiguration konfigurieren</span><span class="sxs-lookup"><span data-stu-id="a8f84-226">Configure the .NET Framework default proxy configuration</span></span>

<span data-ttu-id="a8f84-227">Der erste Schritt besteht darin, die Standardproxykonfiguration für .NET Framework zu definieren.</span><span class="sxs-lookup"><span data-stu-id="a8f84-227">The first step is to first define the default proxy configuration for .NET Framework.</span></span> <span data-ttu-id="a8f84-228">Aufgrund dieser Änderungen kann Fiddler den Datenverkehr sowohl von SharePoint als auch von Workflow-Manager abfangen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-228">These changes will allow Fiddler to intercept the traffic coming from both SharePoint and the Workflow Manager.</span></span> <span data-ttu-id="a8f84-229">Öffnen Sie die Datei **machine.config** an den folgenden beiden Speicherorten:</span><span class="sxs-lookup"><span data-stu-id="a8f84-229">Open the **machine.config** file in both of the following locations:</span></span>
  
    
    

-  `%systemdrive%\\Windows\\Microsoft.NET\\Framework\\v4.0.30319\\Config\\machine.config`
    
  
-  `%systemdrive%\\Windows\\Microsoft.NET\\Framework64\\v4.0.30319\\Config\\machine.config`
    
  
<span data-ttu-id="a8f84-230">Fügen Sie als Nächstes das folgende Markup unten in jeder Datei hinzu, bevor Sie das **<configuration>**-Element schließen:</span><span class="sxs-lookup"><span data-stu-id="a8f84-230">Next, add the following markup to the bottom of each file, just before the closing **<configuration>** element:</span></span>
  
    
    



```xml

<system.net>
  <defaultProxy enabled="true">
    <proxy bypassonlocal="false" usesystemdefault="true" />
  </defaultProxy>
</system.net>
```

<span data-ttu-id="a8f84-231">Speichern Sie die Änderungen, und schließen Sie die Dateien.</span><span class="sxs-lookup"><span data-stu-id="a8f84-231">Save the changes and close the files.</span></span>
  
    
    

#### <a name="configure-fiddler-to-intercept-and-inspect-https-traffic"></a><span data-ttu-id="a8f84-232">Fiddler zum Abfangen und Überprüfen von HTTPS-Datenverkehr konfigurieren</span><span class="sxs-lookup"><span data-stu-id="a8f84-232">Configure Fiddler to intercept and inspect HTTPS traffic</span></span>

<span data-ttu-id="a8f84-233">Als Nächstes müssen Sie Fiddler zum Abfangen von verschlüsseltem Datenverkehr und zum Entschlüsseln konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="a8f84-233">The next step is to configure Fiddler to intercept encrypted traffic and decrypt it for configuration.</span></span>
  
    
    

1. <span data-ttu-id="a8f84-234">Starten Sie Fiddler.</span><span class="sxs-lookup"><span data-stu-id="a8f84-234">Start Fiddler.</span></span>
    
  
2. <span data-ttu-id="a8f84-235">Wenn Sie die lokale HOSTS-Datei verwenden, stellen Sie sicher, dass die Einträge in Fiddler enthalten sind. Wählen Sie hierzu die Menüoption **Tools -> HOSTS**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-235">If you are using the local HOSTS file, ensure that the entries are included in Fiddler by selecting the **Tools -> HOSTS** menu option.</span></span>
    
  
3. <span data-ttu-id="a8f84-236">Aktivieren Sie die Option **Enable remapping of requests for one host to a different host or IP, overriding DNS**,</span><span class="sxs-lookup"><span data-stu-id="a8f84-236">Check the **Enable remapping of requests for one host to a different host or IP, overriding DNS**,</span></span>
    
  
4. <span data-ttu-id="a8f84-237">Klicken Sie auf **Import Windows Hosts File**, und klicken Sie dann auf **Save**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-237">Click the **Import Windows Hosts File**, and then click the **Save** button.</span></span>
    
  

<span data-ttu-id="a8f84-238">**Abbildung 5: Hostneuzuordnung**</span><span class="sxs-lookup"><span data-stu-id="a8f84-238">**Figure 5. Host Remapping**</span></span>

  
    
    

  
    
    
![Abbildung 5: UI zur Nutzung der lokalen HOSTS-Datei](../images/ngDebuggingSP2013Workflows05.png)
  
    
    
<span data-ttu-id="a8f84-241">Als Nächstes konfigurieren Sie die Verbindungsoptionen von Fiddler.</span><span class="sxs-lookup"><span data-stu-id="a8f84-241">Next, configure Fiddler's connection options.</span></span> 
  
    
    

  
    
    

1. <span data-ttu-id="a8f84-242">Wählen Sie die Menüoption **Tools -> Fiddler Options**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-242">Select the **Tools -> Fiddler Options** menu option.</span></span>
    
  
2. <span data-ttu-id="a8f84-243">Klicken Sie auf die Registerkarte **Verbindungen**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-243">Click the **Connections** tab.</span></span>
    
  
3. <span data-ttu-id="a8f84-244">Heben Sie die Auswahl von **Chain to upstream gateway proxy** auf.</span><span class="sxs-lookup"><span data-stu-id="a8f84-244">Clear the **Chain to upstream gateway proxy** selection.</span></span>
    
  
4. <span data-ttu-id="a8f84-245">Wählen Sie die Optionen **Act as system proxy on startup** und **Monitor all connections** aus, wie in der folgenden Abbildung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="a8f84-245">Select the **Act as system proxy on startup** and **Monitor all connections** options, as shown in the following figure.</span></span>
    
   <span data-ttu-id="a8f84-246">**Abbildung 6: Fiddler-Verbindungsoptionen**</span><span class="sxs-lookup"><span data-stu-id="a8f84-246">**Figure 6. Fiddler connection options.**</span></span>

  

  ![Abbildung 6: Fiddler-Verbindungsoptionen](../images/ngDebuggingSP2013Workflows06.png)
  

  

  
5. <span data-ttu-id="a8f84-249">Wählen Sie die Registerkarte **HTTPS** im Dialogfeld **Fiddler Options**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-249">Select the **HTTPS** tab in the **Fiddler Options** dialog.</span></span>
    
  
6. <span data-ttu-id="a8f84-250">Aktivieren Sie das Kontrollkästchen **Capture HTTPS CONNECTs**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-250">Check the **Capture HTTPS CONNECTs**.</span></span>
    
  
7. <span data-ttu-id="a8f84-251">Wählen Sie **Decrypt HTTPS Traffic** aus.</span><span class="sxs-lookup"><span data-stu-id="a8f84-251">Select **Decrypt HTTPS Traffic**.</span></span>
    
  
8. <span data-ttu-id="a8f84-252">Wählen Sie **… from all processes** aus.</span><span class="sxs-lookup"><span data-stu-id="a8f84-252">Select **??? from all processes**.</span></span>
    
  
9. <span data-ttu-id="a8f84-253">Aktivieren Sie das Kontrollkästchen **Ignore server certificate errors**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-253">Check **Ignore server certificate errors**.</span></span>
    
  
10. <span data-ttu-id="a8f84-254">Klicken Sie auf **Export Root Certificate to Desktop**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-254">Click the **Export Root Certificate to Desktop** button.</span></span>
    
  
11. <span data-ttu-id="a8f84-255">Wenn eine Warnmeldung angezeigt wird, klicken Sie auf **Yes**, um **Trust the Fiddler Root certificate** zu bestätigen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-255">When prompted with a warning, click **Yes** to **Trust the Fiddler Root certificate**.</span></span>
    
  
<span data-ttu-id="a8f84-256">Hierdurch wird das Zertifikat in Windows als vertrauenswürdig konfiguriert, obwohl es in SharePoint noch nicht als vertrauenswürdig eingestuft wird.</span><span class="sxs-lookup"><span data-stu-id="a8f84-256">This process will configure Windows to trust the certificate, although SharePoint does not trust it yet.</span></span>
  
    
    

<span data-ttu-id="a8f84-257">**Abbildung 7: HTTPS-Registerkarte**</span><span class="sxs-lookup"><span data-stu-id="a8f84-257">**Figure 7. HTTPS tab**</span></span>

  
    
    

  
    
    
![Abbildung 7: Registerkarte „HTTPS“](../images/ngDebuggingSP2013Workflows07.png)
  
> [!NOTE]
> <span data-ttu-id="a8f84-260">Wenn eine Sicherheitswarnung angezeigt wird, dass dem Fiddler-Zertifikat nicht vertraut werden sollte, klicken Sie auf **Ja**, um mit der Installation des Zertifikats fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="a8f84-260">**Note:** If a security WRning appears with a message instructing not to trust the Fiddler certificate, click Yes to continue installing the certificate.</span></span>
  
    
    

#### <a name="configure-sharepoint-to-trust-the-certificate"></a><span data-ttu-id="a8f84-261">SharePoint konfigurieren, das Zertifikat als vertrauenswürdig einzustufen</span><span class="sxs-lookup"><span data-stu-id="a8f84-261">Configure SharePoint to trust the certificate</span></span>

<span data-ttu-id="a8f84-262">Als letzten Schritt müssen Sie SharePoint so konfigurieren, dass das im vorherigen Schritt exportierte Fiddler-Zertifikat als vertrauenswürdig eingestuft wird.</span><span class="sxs-lookup"><span data-stu-id="a8f84-262">The last step is to configure SharePoint to trust the Fiddler certificate that was exported in the previous step.</span></span> 
  
    
    

1. <span data-ttu-id="a8f84-263">Melden Sie sich als Farmadministrator bei SharePoint an.</span><span class="sxs-lookup"><span data-stu-id="a8f84-263">Log on as a SharePoint farm administrator.</span></span>
    
  
2. <span data-ttu-id="a8f84-264">Starten Sie die SharePoint-Verwaltungsshell.</span><span class="sxs-lookup"><span data-stu-id="a8f84-264">Start the SharePoint Management Shell.</span></span>
    
  
3. <span data-ttu-id="a8f84-265">Ladne Sie das SharePoint-Snap-In.</span><span class="sxs-lookup"><span data-stu-id="a8f84-265">Load the SharePoint Snap-In.</span></span>
    
```powershell
  
PS C:\\> Add-PSSnapIn Microsoft.SharePoint.PowerShell
```

4. <span data-ttu-id="a8f84-266">Installieren Sie mithilfe des Zertifikatdienstprogramms das Fiddler-Zertifikat.</span><span class="sxs-lookup"><span data-stu-id="a8f84-266">Use the certificate utility to install the Fiddler certificate.</span></span>
    
```powershell
  PS C:\\> $fidderCertificatePath = [full path to exported FiddlerRoot.cer certificate file]
PS C:\\> certutil.exe -addstore -enterprise -f -v root $fidderCertificatePath
PS C:\\> $fiddlerCertificate = Get-PfxCertificate -FilePath $fidderCertificatePath
PS C:\\> New-SPTrustedRootAuthority -Name "Fiddler" -Certificate $fiddlerCertificate

```

5. <span data-ttu-id="a8f84-267">Führen Sie IISRESET aus, um sicherzusstellen, dass SharePoint die Änderung hinsichtlich der Vertrauenswürdigkeit des Zertifikats übernommen hat.</span><span class="sxs-lookup"><span data-stu-id="a8f84-267">Run IISRESET to make sure that SharePoint picks up the certificate trust change.</span></span>
    
  

### <a name="walkthrough-debugging-a-sharepoint-workflow-with-fiddler"></a><span data-ttu-id="a8f84-268">Exemplarische Vorgehensweise: Debuggen eines SharePoint-Workflows mit Fiddler</span><span class="sxs-lookup"><span data-stu-id="a8f84-268">Walkthrough: Debugging a SharePoint workflow with Fiddler</span></span>

<span data-ttu-id="a8f84-269">In dieser einfachen exemplarischen Vorgehensweise wird die Verwendung von Fiddler zum Debuggen eines SharePoint-Workflows mithilfe von Visual Studio 2012 veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="a8f84-269">This simple walkthrough demonstrates using Fiddler to debug a SharePoint workflow authored using Visual Studio 2012.</span></span> <span data-ttu-id="a8f84-270">Wenn der Workflow gestartet wird, wird eine Kunden-ID aus einem Feld in einer benutzerdefinierten Liste abgerufen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-270">When the workflow starts, it retrieves a customer ID from a field in a custom list.</span></span> <span data-ttu-id="a8f84-271">Diese Kunden-ID dient zum Abfragen eines öffentlich zugänglich Diensts, um weitere Details über den Kunden abzurufen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-271">This customer ID is used to query a publically accessible service to retrieve additional details about the customer.</span></span> <span data-ttu-id="a8f84-272">Dann werden diese Werte zum Aktualisieren des ursprünglichen Listenelements verwendet.</span><span class="sxs-lookup"><span data-stu-id="a8f84-272">It then uses these values to update the original list item.</span></span> <span data-ttu-id="a8f84-273">Der Workflow ist im folgenden MSDN-Codebeispiel zu finden: [SharePoint-Workflow: Aufrufen eines externen Webdiensts](http://code.msdn.microsoft.com/officeapps/SharePoint-workflow-48ea87d4.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8f84-273">The workflow can be found in the following MSDN code sample:  [SharePoint Workflow: Call an External Web Service](http://code.msdn.microsoft.com/officeapps/SharePoint-workflow-48ea87d4.aspx).</span></span>
  
    
    
<span data-ttu-id="a8f84-274">Für diese exemplarische Vorgehensweise gelten die folgenden Voraussetzungen:</span><span class="sxs-lookup"><span data-stu-id="a8f84-274">This walkthrough has the following prerequisites:</span></span>
  
    
    

- <span data-ttu-id="a8f84-275">SharePoint und Workflow-Manager 1.0 müssen auf dem gleichen Server installiert sein.</span><span class="sxs-lookup"><span data-stu-id="a8f84-275">SharePoint and Workflow Manager 1.0 are installed on the same server.</span></span>
    
  
- <span data-ttu-id="a8f84-276">Die Windows-Identität **CONTOSO\\SP_Content** ist für die Anwendungspoolidentität konfiguriert, die die Webanwendung für die SharePoint-Website hostet, von der der Workflow gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="a8f84-276">The Windows identity **CONTOSO\\SP_Content** is configured for the application pool identity that hosts the web application serving the SharePoint site that starts the workflow.</span></span>
    
  
- <span data-ttu-id="a8f84-277">Die SharePoint-Website, von der der Workflow gestartet wird, ist **http://intranet.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-277">The SharePoint site used to start the workflow is **http://intranet.contoso.com**</span></span>
    
  
- <span data-ttu-id="a8f84-278">Der Workflow Manager 1.0-Farmendpunkt ist **w15sp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a8f84-278">The Workflow Manager 1.0 farm endpoint is **w15sp.contoso.com**.</span></span>
    
  
- <span data-ttu-id="a8f84-279">SharePoint und Workflow-Manager 1.0 sind so konfiguriert, dass sie OAuth über HTTP zulassen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-279">SharePoint and Workflow Manager 1.0 are configured to allow OAuth over HTTP.</span></span>
    
    > <span data-ttu-id="a8f84-280">**Vorsicht:** Die sollte nie auf einem Produktionsserver durchgeführt werden, sondern nur zum Testen und Debuggen.</span><span class="sxs-lookup"><span data-stu-id="a8f84-280">**Caution:** This should never be done on the production server, but only for testing and debugging.</span></span> 

1. <span data-ttu-id="a8f84-281">Melden Sie sich bei dem Server an, auf dem Workflow Manager und SharePoint installiert sind, wobei die Windows-Identität als Workflow-Manager 1.0-Farmkonto und SharePoint-Anwendungspoolidentität konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="a8f84-281">Log on to the server where Workflow Manager and SharePoint are installed with the Windows identity configured as the Workflow Manager 1.0 farm account and SharePoint application pool identity.</span></span>
    
  
2. <span data-ttu-id="a8f84-p136">Starten Sie Fiddler. Fiddler fängt nun den Datenverkehr vom aktuellen Benutzer ab. Wenn bereits Verbindungen vorhanden sind oder Prozesse ausgeführt werden, werden diese möglicherweise nicht von Fiddler abgefangen, da Fiddler beim Herstellen der Verbindungen noch nicht ausgeführt wurde. Um sowohl Workflow Manager als auch den SharePoint-Server zurückzusetzen und zu veranlassen, dass ihr Datenverkehr von Fiddler abgefangen wird, setzen Sie SharePoint mit IISRESET zurück, und setzen Sie Workflow Manager zurück, indem Sie den Windows-Dienst **Workflow Manager Backend** anhalten und neu starten. Verwenden Sie hierzu die folgenden beiden Befehle an einer administrativen Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p136">Start Fiddler. While Fiddler will now intercept traffic from the current user, if there are any existing connections or processes running, Fiddler may miss those as it was not running when the connections were initially established. To force both Workflow Manager and SharePoint Server to recycle and have their traffic to each other get intercepted by Fiddler, recycle SharePoint by running an IISRESET and recycle Workflow Manager by stopping and starting the Windows service **Workflow Manager Backend**. This can be done with the following two commands at an administrative command prompt.</span></span>
    
```powershell  
PS C:\\> IISRESET
PS C:\\> net stop WorkflowServiceBackend
PS C:\\> net start WorkflowServiceBackend
```

3. <span data-ttu-id="a8f84-286">Starten Sie den Workflow.</span><span class="sxs-lookup"><span data-stu-id="a8f84-286">Start the workflow.</span></span>
    
  
<span data-ttu-id="a8f84-287">Beachten Sie in der Abbildung unten, dass die Sitzungen 18-36 von SharePoint stammen und die Sitzungen 37-43 von Workflow-Manager.</span><span class="sxs-lookup"><span data-stu-id="a8f84-287">In the figure below, notice that sessions #18-36 originated from SharePoint and sessions #37-43 originated from Workflow Manager.</span></span>
  
    
    

<span data-ttu-id="a8f84-288">**Abbildung 8: Starten des Workflows**</span><span class="sxs-lookup"><span data-stu-id="a8f84-288">**Figure 8. Starting the workflow**</span></span>

  
    
    

  
    
    
![Abbildung 8: Workflow wird gestartet](../images/ngDebuggingSP2013Workflows08.png)
  
    
    
<span data-ttu-id="a8f84-291">Beachten Sie in Sitzung 36, dass SharePoint eine Anforderung an Workflow-Manager zum Starten eines Workflows richtet (in der Abbildung durch [A] gekennzeichnet). Workflow-Manager antwortet mit einer Erfolgsmeldung (in der Abbildung durch [B] gekennzeichnet):</span><span class="sxs-lookup"><span data-stu-id="a8f84-291">Notice that in session #36, SharePoint is requesting that Workflow Manager start a workflow (indicated as [A] in the figure) and Workflow Manager responds (indicated as [B] in the figure) with a "Success" message:</span></span>
  
    
    

<span data-ttu-id="a8f84-292">**Abbildung 9: Erfolgsmeldung**</span><span class="sxs-lookup"><span data-stu-id="a8f84-292">**Figure 9. "Success" message response**</span></span>

  
    
    

  
    
    
![Abbildung 10: Erfolgsmeldung](../images/ngDebuggingSP2013Workflows10.png)
  
    
    
<span data-ttu-id="a8f84-295">In Sitzung 40 ruft Workflow-Manager die Listenelement-ID und -GUID von SharePoint ab.</span><span class="sxs-lookup"><span data-stu-id="a8f84-295">Session #40 is where Workflow Manager is retrieving the list item ID and GUID from SharePoint.</span></span>
  
    
    

<span data-ttu-id="a8f84-296">**Abbildung 11: Abrufen der ID und GUID des Elements**</span><span class="sxs-lookup"><span data-stu-id="a8f84-296">**Figure 10. Retrieving item ID and GUID**</span></span>

  
    
    

  
    
    
![Abbildung 11: Abrufen der ID und GUID des Listenelements](../images/ngDebuggingSP2013Workflows11.png)
  
    
    
<span data-ttu-id="a8f84-p140">In Sitzung 43 aktualisiert Workflow-Manager das Listenelement in SharePoint mit einem neuen Wert für das Feld **Body** des Ankündigungselements, indem er ein JavaScript Object Notation (JSON)-Objekt (in der Abbildung durch [A] gekennzeichnet) als Nutzlast weitergibt. SharePoint antwortet mit dem HTTP-Status 204, der darauf hinweist, dass die Anforderung erfolgreich verarbeitet wurde. Die Antwort enthält jedoch keine Meldung.</span><span class="sxs-lookup"><span data-stu-id="a8f84-p140">Session #43 is where Workflow Manager is updating the list item in SharePoint with a new value for the announcement item's **Body** field by passing a JavaScript Object Notation (JSON) object (indicated as [A] in the figure) along as the payload. SharePoint responds with an HTTP status of 204, which indicates that it successfully processed the request, but there is no message in the response.</span></span>
  
    
    

<span data-ttu-id="a8f84-301">**Abbildung 11: Aktualisieren des Listenelements**</span><span class="sxs-lookup"><span data-stu-id="a8f84-301">**Figure 11. Updating the list item**</span></span>

  
    
    

  
    
    
![Abbildung 12: Aktualisieren des Listenelements in SharePoint](../images/ngDebuggingSP2013Workflows12.png)
  
    
    

  
    
    

  
    
    

## <a name="conclusion"></a><span data-ttu-id="a8f84-304">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="a8f84-304">Conclusion</span></span>

<span data-ttu-id="a8f84-305">Durch den Workflow-Textabschnitt in der SharePoint-Version wurde eine neue Abstraktionsebene eingeführt: Workflow-Manager 1.0.</span><span class="sxs-lookup"><span data-stu-id="a8f84-305">The workflow story in the SharePoint release introduced a new layer of abstraction, Workflow Manager 1.0.</span></span> <span data-ttu-id="a8f84-306">Durch diese neue Architektur wurde geändert, wie Workflows verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="a8f84-306">This new architecture changed how workflows are processed.</span></span> <span data-ttu-id="a8f84-307">SharePoint nutzt jetzt Workflow-Manager 1.0 für die gesamte Workflowverarbeitung und -verwaltung.</span><span class="sxs-lookup"><span data-stu-id="a8f84-307">SharePoint now relies on Workflow Manager 1.0 for all workflow processing and management.</span></span>
  
    
    
<span data-ttu-id="a8f84-308">Eine Aufgabe, die Sie beim Erstellen von benutzerdefinierten Anwendungen und Geschäftsprozessen in Workflows ausführen müssen, ist das Debuggen Ihrer Arbeit.</span><span class="sxs-lookup"><span data-stu-id="a8f84-308">One task you need to perform when creating custom applications and business processes in workflows is debugging your work.</span></span> <span data-ttu-id="a8f84-309">Die neue Workflowarchitektur von SharePoint bietet dieselben Optionen zum Debuggen, die in früheren Versionen von SharePoint vorhanden waren.</span><span class="sxs-lookup"><span data-stu-id="a8f84-309">The new workflow architecture of SharePoint offers the same debugging options that existed in previous versions of SharePoint.</span></span> <span data-ttu-id="a8f84-310">Die neue Architektur bietet jedoch zwei neue Optionen beim Erstellen von benutzerdefinierten Workflows mithilfe der neuen Architektur.</span><span class="sxs-lookup"><span data-stu-id="a8f84-310">However, the new architecture offers two new options when creating custom workflows using the new architecture.</span></span> <span data-ttu-id="a8f84-311">In diesem Artikel werden die älteren Debugging-Optionen sowie die neuen Optionen mithilfe der **WriteLine**-Aktivität und die Verwendung von Fiddler zum Abfangen und Überprüfen von Datenverkehr zwischen SharePoint und Workflow-Manager 1.0 erläutert.</span><span class="sxs-lookup"><span data-stu-id="a8f84-311">This article explained the legacy debugging options as well as the new options using the **WriteLine** activity and using Fiddler for intercepting and inspecting traffic between SharePoint and Workflow Manager 1.0.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="a8f84-312">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="a8f84-312">See also</span></span>
<span data-ttu-id="a8f84-313"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a8f84-313"><a name="bk_addresources"> </a></span></span>


-  <span data-ttu-id="a8f84-314">[Fiddler](http://fiddler2.com/home)</span><span class="sxs-lookup"><span data-stu-id="a8f84-314">[Fiddler](http://fiddler2.com/home)</span></span>
    
  

  
    
    

