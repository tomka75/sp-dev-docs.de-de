---
title: Walkthrough Developing a Custom Application Using Excel Web Services
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2f9bf243-281a-4d70-917e-9eaf0b867631
ms.openlocfilehash: 96cbe71ced7143b9888645b3b455c3738f0030a6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="walkthrough-developing-a-custom-application-using-excel-web-services"></a><span data-ttu-id="61e19-102">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="61e19-102">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>

<span data-ttu-id="61e19-103">Die exemplarische Vorgehensweise in diesem Abschnitt beschreibt das Verfahren für den Zugriff auf die Excel Web Services von einer mit Microsoft Visual C# erstellten Anwendung.</span><span class="sxs-lookup"><span data-stu-id="61e19-103">The walkthrough in this section describes the process for accessing Excel Web Services from an application created with Microsoft Visual C#.</span></span>
  
    
    

<span data-ttu-id="61e19-104">Diese exemplarische Vorgehensweise vermittelt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="61e19-104">During this walkthrough, you will learn how to:</span></span>
- <span data-ttu-id="61e19-105">Erstellen einer Clientanwendung mithilfe der Visual Studio-Projektvorlage für Konsolenanwendungen.</span><span class="sxs-lookup"><span data-stu-id="61e19-105">Create a client application using the Visual Studio Console Application project template.</span></span>
    
  
- <span data-ttu-id="61e19-106">Hinzufügen eines Webverweises für die Excel Web Services.</span><span class="sxs-lookup"><span data-stu-id="61e19-106">Add a Web reference for Excel Web Services.</span></span>
    
  
- <span data-ttu-id="61e19-p101">Schreiben von Code für den Zugriff auf den Webdienst. Sie erfahren, wie eine Arbeitsmappe geöffnet wird, die Sitzungs-ID abgerufen wird, die Standardanmeldeinformationen übergeben werden, Webdienst-Versionsinformationen abgerufen werden, das Bereichskoordinatenobjekt definiert wird, der Bereich, der das Bereichskoordinatenobjekt verwendet, abgerufen wird, die Arbeitsmappe geschlossen wird und die SOAP-Ausnahme aufgefangen wird.</span><span class="sxs-lookup"><span data-stu-id="61e19-p101">Write code to access the Web service. You will learn how to open a workbook, get the session ID, pass in the default credentials, get Web service version information, define the range coordinate object, get the range that uses the range coordinate object, close the workbook, and catch the SOAP exception.</span></span>
    
  
- <span data-ttu-id="61e19-109">Testen und Ausführen der Konsolenanwendung im Debugmodus.</span><span class="sxs-lookup"><span data-stu-id="61e19-109">Test and run the console application in debug mode.</span></span>
    
  
<span data-ttu-id="61e19-p102">Eine Clientkonsolenanwendung ist nur eine Möglichkeit, um auf den Webdienst zuzugreifen. Ein gängigeres Verfahren ist die Verwendung von Serveranwendungen wie Microsoft ASP.NET-Anwendungen. Im Rahmen dieser exemplarischen Vorgehensweise wird der Einfachheit halber eine Konsolenanwendung als Beispiel verwendet, um die Aspekte der Excel Web Services-API zu beleuchten.</span><span class="sxs-lookup"><span data-stu-id="61e19-p102">A client console application is just one way to access the Web service. A more common way would be to use server applications, such as Microsoft ASP.NET applications. This walkthrough uses a console application example for simplicity, to focus on the Excel Web Services API aspects.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="61e19-113">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="61e19-113">Prerequisites</span></span>

<span data-ttu-id="61e19-114">In order to complete this walkthrough, you will need:</span><span class="sxs-lookup"><span data-stu-id="61e19-114">In order to complete this walkthrough, you will need:</span></span> 
  
    
    

- <span data-ttu-id="61e19-115">Microsoft SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="61e19-115">Microsoft SharePoint Server 2010.</span></span>
    
  
- <span data-ttu-id="61e19-116">Visual Studio oder ein vergleichbares mit Microsoft .NET Framework kompatibles Entwicklungstool.</span><span class="sxs-lookup"><span data-stu-id="61e19-116">Visual Studio or a similar Microsoft .NET Framework-compatible development tool.</span></span>
    
  
- <span data-ttu-id="61e19-117">Ausreichende Berechtigungen (mindestens die Berechtigung "Anzeigen"), um auf die Excel Web Services auf dem Computer zugreifen zu können, auf dem sich SharePoint Server 2010 befindet.</span><span class="sxs-lookup"><span data-stu-id="61e19-117">Sufficient permissions (at the very least, "view" permissions) to be able to access Excel Web Services on the computer where SharePoint Server 2010 is located.</span></span> 
    
    > <span data-ttu-id="61e19-118">**Hinweis:** Weitere Informationen zu Arbeitsmappenberechtigungen finden Sie weiter unten im Abschnitt "Arbeitsmappenberechtigungen".</span><span class="sxs-lookup"><span data-stu-id="61e19-118">**Note** For more information about workbook permissions, see the following section, "Workbook Permissions."</span></span> 
- <span data-ttu-id="61e19-119">Eine auf einem lokalen Laufwerk oder in einer lokalen SharePoint-Dokumentbibliothek installierte Beispiel-Arbeitsmappe.</span><span class="sxs-lookup"><span data-stu-id="61e19-119">A sample workbook installed on a local drive or local SharePoint document library.</span></span> 
    
  
- <span data-ttu-id="61e19-p103">Einen vertrauenswürdigen Speicherort zum Speichern von Arbeitsmappen, auf die Sie mithilfe der Excel Web Services zugreifen möchten. Wenn die Arbeitsmappen nicht an einem vertrauenswürdigen Speicherort gespeichert sind, führen die Excel Web Services-Aufrufe zum Öffnen der Arbeitsmappe zu einem Fehler. Bei dieser exemplarischen Vorgehensweise wird davon ausgegangen, dass sich die Arbeitsmappe auf dem lokalen Computer befindet.</span><span class="sxs-lookup"><span data-stu-id="61e19-p103">A trusted location to store the workbooks that you want to access using Excel Web Services. If the workbooks are not stored in a trusted location, the Excel Web Services calls to open the workbook will fail. This walkthrough assumes the workbook is present on the local computer.</span></span> 
    
    > <span data-ttu-id="61e19-123">**Hinweis:** Informationen zum Festlegen eines vertrauenswürdigen Speicherorts finden Sie unter  [Vorgehensweise: Aufbauen einer Vertrauensstellung zu einem Speicherort](how-to-trust-a-location.md) und [Vorgehensweise: Aufbauen einer Vertrauensstellung zu Arbeitsmappen mit Skript](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="61e19-123">**Note** For information about how to trust a location, see  [How to: Trust a Location](how-to-trust-a-location.md) and [How to: Trust Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx).</span></span> 
- <span data-ttu-id="61e19-124">Erstellen der Arbeitsmappe mithilfe von Excel.</span><span class="sxs-lookup"><span data-stu-id="61e19-124">To create the workbook using Excel.</span></span>
    
  
- <span data-ttu-id="61e19-125">Sie müssen die Arbeitsmappe als XLSX- oder XLSB-Datei speichern.</span><span class="sxs-lookup"><span data-stu-id="61e19-125">To save the workbook as .xlsx or .xlsb files.</span></span>
    
  
<span data-ttu-id="61e19-p104">Die Arbeitsmappe, die in diesem Beispiel verwendet wird, trägt den Namen "Sheet1". Das Arbeitsblatt enthält 11 Spalten und 19 Zeilen. Jede Zelle von A1 bis K19 enthält einen numerischen Wert, z. B. 4245,955, 6960,673 usw.</span><span class="sxs-lookup"><span data-stu-id="61e19-p104">The workbook used in this example has a worksheet named "Sheet1". The worksheet has 11 columns and 19 rows. Each cell from A1 to K19 contains a numeric value—for example, 4245.955, 6960.673, and so on.</span></span>
  
    
    

## <a name="workbook-permissions"></a><span data-ttu-id="61e19-129">Arbeitsmappenberechtigungen</span><span class="sxs-lookup"><span data-stu-id="61e19-129">Workbook Permissions</span></span>


- <span data-ttu-id="61e19-130">Zum Abrufen der gesamten Arbeitsmappe (z. B. durch Aufrufen der **GetWorkbook**-Methode) benötigt der Aufrufer die Berechtigung "Öffnen" für die Arbeitsmappe.</span><span class="sxs-lookup"><span data-stu-id="61e19-130">To get the entire workbook (for example, by calling the **GetWorkbook** method), the caller needs "open" permission fr the workbook.</span></span>
    
  
- <span data-ttu-id="61e19-131">Zum Aufrufen der **GetApiVersion**-Methode sind keine Berechtigungen erforderlich.</span><span class="sxs-lookup"><span data-stu-id="61e19-131">To call the **GetApiVersion** method, no permission is necessary.</span></span>
    
  
- <span data-ttu-id="61e19-132">Für die übrigen Excel Web Services-Methoden benötigt der Aufrufer die Berechtigung "Anzeigen" (in Microsoft SharePoint Foundation) oder "Lesen" (auf einer Dateifreigabe ) für die Arbeitsmappe.</span><span class="sxs-lookup"><span data-stu-id="61e19-132">For the rest of the Excel Web Services methods, the caller needs "view" permission (in Microsoft SharePoint Foundation) or "read" permission (on a file share) for the workbook.</span></span>
    
    > <span data-ttu-id="61e19-133">**Hinweis:** Weitere Informationen zum Festlegen von Berechtigungen finden Sie in der Dokumentation zu SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="61e19-133">**Note** For more information about setting permissions, see the SharePoint Foundation documentation.</span></span> 

## <a name="see-also"></a><span data-ttu-id="61e19-134">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="61e19-134">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="61e19-135">Konzepte</span><span class="sxs-lookup"><span data-stu-id="61e19-135">Concepts</span></span>


  
    
    
 [<span data-ttu-id="61e19-136">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="61e19-136">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="61e19-137">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="61e19-137">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="61e19-138">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="61e19-138">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="61e19-139">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="61e19-139">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a><span data-ttu-id="61e19-140">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="61e19-140">Other resources</span></span>


  
    
    
 [<span data-ttu-id="61e19-141">Step 1: Creating the Web Service Client Project</span><span class="sxs-lookup"><span data-stu-id="61e19-141">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="61e19-142">Step 2: Adding a Web Reference</span><span class="sxs-lookup"><span data-stu-id="61e19-142">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="61e19-143">Step 3: Accessing the Web Service</span><span class="sxs-lookup"><span data-stu-id="61e19-143">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="61e19-144">Step 4: Building and Testing the Application</span><span class="sxs-lookup"><span data-stu-id="61e19-144">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
