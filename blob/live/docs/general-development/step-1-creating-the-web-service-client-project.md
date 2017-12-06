---
title: Step 1 Creating the Web Service Client Project
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1f0fc9fc-0db4-47bb-8204-a06777b84e76
ms.openlocfilehash: 4224c42b2ffbb1cf037e59fac927811510441970
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="step-1-creating-the-web-service-client-project"></a><span data-ttu-id="03af7-102">Step 1: Creating the Web Service Client Project</span><span class="sxs-lookup"><span data-stu-id="03af7-102">Step 1: Creating the Web Service Client Project</span></span>

<span data-ttu-id="03af7-p101">Im Rahmen dieser exemplarischen Vorgehensweise erstellen Sie ein neues Projekt und eine einfache Konsolenanwendung, die auf die Excel Web Services zugreift. Es wird davon ausgegangen, dass die Entwicklung in Visual Studio erfolgt.</span><span class="sxs-lookup"><span data-stu-id="03af7-p101">For this walkthrough, you will create a new project and a simple console application that accesses Excel Web Services. This walkthrough assumes you are developing in Visual Studio.</span></span> 
  
    
    


## <a name="creating-the-project"></a><span data-ttu-id="03af7-105">Erstellen des Projekts</span><span class="sxs-lookup"><span data-stu-id="03af7-105">Creating the Project</span></span>

<span data-ttu-id="03af7-106">Im folgenden Projekt wird Microsoft Visual Studio 2003 verwendet.</span><span class="sxs-lookup"><span data-stu-id="03af7-106">The following project uses Microsoft Visual Studio 2003.</span></span>
  
    
    

> <span data-ttu-id="03af7-107">**Hinweis:** Wenn Sie Microsoft Visual Studio 2005 oder Microsoft Visual Studio 2008 verwenden, variiert das Verfahren zum Erstellen eines neuen Projekts geringfügig in Abhängigkeit von den Einstellungen, die Sie in der integrierten Entwicklungsumgebung von Visual Studio verwenden.</span><span class="sxs-lookup"><span data-stu-id="03af7-107">**Note** If you are using Microsoft Visual Studio 2005 or Microsoft Visual Studio 2008, the process to create a new project is slightly different depending on which settings you use in the Visual Studio integrated development environment (IDE).</span></span>
  
    
    


### <a name="to-create-a-new-project"></a><span data-ttu-id="03af7-108">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="03af7-108">To create a new project</span></span>


1. <span data-ttu-id="03af7-109">Starten Sie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03af7-109">Start Visual Studio.</span></span>
    
  
2. <span data-ttu-id="03af7-p102">Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie dann auf **Projekt**. Das Dialogfeld **Neues Projekt** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="03af7-p102">On the **File** menu, point to **New**, and then click **Project**. The **New Project** dialog box appears.</span></span>
    
  
3. <span data-ttu-id="03af7-112">Wählen Sie im Bereich **Projekttyp** die Option **Visual C#-Projekte** aus.</span><span class="sxs-lookup"><span data-stu-id="03af7-112">In the **Project Type** pane, select **Visual C# Projects**.</span></span>
    
  
4. <span data-ttu-id="03af7-113">Klicken Sie im Bereich **Vorlagen** auf **Konsolenanwendung**.</span><span class="sxs-lookup"><span data-stu-id="03af7-113">In the **Templates** pane, click **Console Application**.</span></span>
    
  
5. <span data-ttu-id="03af7-114">Geben Sie im Feld **Name** den Namen **SampleApplication** ein.</span><span class="sxs-lookup"><span data-stu-id="03af7-114">In the **Name** box, type **SampleApplication**.</span></span>
    
  
6. <span data-ttu-id="03af7-115">Geben Sie im Feld **Speicherort** den Pfad ein, in dem Sie Ihr Projekt speichern möchten, oder klicken Sie auf **Durchsuchen**, um zu dem Ordner zu navigieren.</span><span class="sxs-lookup"><span data-stu-id="03af7-115">In the **Location** box, enter the path where you want to save your project, or click **Browse** to navigate to the folder.</span></span>
    
  
7. <span data-ttu-id="03af7-116">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="03af7-116">Click **OK**.</span></span> <span data-ttu-id="03af7-117">Das neu erstellte Projekt wird im **Projektmappen-Explorer** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="03af7-117">Your newly created project appears in **Solution Explorer**.</span></span> 
  
    
    
<span data-ttu-id="03af7-118">Im **Projektmappen-Explorer** wurde eine Datei mit dem Standardnamen Class1.cs zu Ihrem Projekt hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="03af7-118">In **Solution Explorer**, a file with the default name of Class1.cs has been added to your project.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="03af7-119">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="03af7-119">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="03af7-120">Konzepte</span><span class="sxs-lookup"><span data-stu-id="03af7-120">Concepts</span></span>


  
    
    
 [<span data-ttu-id="03af7-121">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="03af7-121">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="03af7-122">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="03af7-122">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="03af7-123">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="03af7-123">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
#### <a name="other-resources"></a><span data-ttu-id="03af7-124">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="03af7-124">Other resources</span></span>


  
    
    
 [<span data-ttu-id="03af7-125">Step 2: Adding a Web Reference</span><span class="sxs-lookup"><span data-stu-id="03af7-125">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="03af7-126">Step 3: Accessing the Web Service</span><span class="sxs-lookup"><span data-stu-id="03af7-126">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="03af7-127">Step 4: Building and Testing the Application</span><span class="sxs-lookup"><span data-stu-id="03af7-127">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
  
    
    
 [<span data-ttu-id="03af7-128">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="03af7-128">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)