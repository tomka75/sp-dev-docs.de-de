---
title: Step 4 Building and Testing the Application
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f2feeecb-1b4c-4049-be4e-11d414f13d9f
ms.openlocfilehash: 344c1fff77662184f13d9f4397b1c7e1f6b065e1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="step-4-building-and-testing-the-application"></a><span data-ttu-id="c9feb-102">Step 4: Building and Testing the Application</span><span class="sxs-lookup"><span data-stu-id="c9feb-102">Step 4: Building and Testing the Application</span></span>

<span data-ttu-id="c9feb-p101">In diesem Schritt erstellen und testen Sie die Anwendung. In Visual Studio stehen mehrere Methoden zum Erstellen und Ausführen einer Konsolenanwendung in der IDE zur Verfügung. Dazu gehören:</span><span class="sxs-lookup"><span data-stu-id="c9feb-p101">In this step, you will build and test your application. Visual Studio offers several methods to build and run a console application from the IDE, such as:</span></span>
  
    
    


- <span data-ttu-id="c9feb-105">Starten ohne Debuggen (STRG+F5)</span><span class="sxs-lookup"><span data-stu-id="c9feb-105">Start Without Debugging ( **CTRL + F5**)</span></span>
    
  
- <span data-ttu-id="c9feb-106">Starten (F5)</span><span class="sxs-lookup"><span data-stu-id="c9feb-106">Start ( **F5**)</span></span>
    
  

## <a name="build-run-and-debug-the-application"></a><span data-ttu-id="c9feb-107">Erstellen, Ausführen und Debuggen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c9feb-107">Build, Run, and Debug the Application</span></span>


### <a name="to-build-and-run-the-application"></a><span data-ttu-id="c9feb-108">Erstellen und Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c9feb-108">To build and run the application</span></span>


1. <span data-ttu-id="c9feb-109">Klicken Sie im Menü **Debuggen** auf **Starten ohne Debuggen** oder drücken Sie **STRG + F5**.</span><span class="sxs-lookup"><span data-stu-id="c9feb-109">On the **Debug** menu, click **Start Without Debugging** or press **CTRL + F5**.</span></span> <span data-ttu-id="c9feb-110">Dadurch wird sichergestellt, dass das Konsolenfenster geöffnet bleibt, nachdem das Programm ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="c9feb-110">On the Debug menu, click Start Without Debugging or press CTRL + F5. This ensures that the console window remains open after the program has finished executing.</span></span> 
    
  
2. <span data-ttu-id="c9feb-111">Die Anwendung druckt die folgende Ausgabe in der Konsole.</span><span class="sxs-lookup"><span data-stu-id="c9feb-111">The application prints the following output to the console.</span></span>
    
    > <span data-ttu-id="c9feb-112">**Hinweis:** Die angezeigten Werte hängen von den Werten ab, die Sie in der Arbeitsmappe, der Sitzungs-ID usw. verwenden.</span><span class="sxs-lookup"><span data-stu-id="c9feb-112">**Note** These values vary depending on the values you have in your workbook, session ID, and so on.</span></span> 

```
  
The Credential is: System.Net.SystemNetworkCredential
Total rows in range: 18
Value in range is: 4245.955129
```

3. <span data-ttu-id="c9feb-113">Drücken Sie eine beliebige Taste, um SampleApplication.exe zu schließen.</span><span class="sxs-lookup"><span data-stu-id="c9feb-113">Press any key to close SampleApplication.exe.</span></span>
    
  

### <a name="file-not-found-exception"></a><span data-ttu-id="c9feb-114">Ausnahme "Datei nicht gefunden"</span><span class="sxs-lookup"><span data-stu-id="c9feb-114">File Not Found Exception</span></span>


1. <span data-ttu-id="c9feb-115">Wenn der bereitgestellte Pfad zu der Arbeitsmappe falsch ist, wird die Ausnahme "Datei nicht gefunden" ausgelöst, die durch folgenden Code abgefangen wird:</span><span class="sxs-lookup"><span data-stu-id="c9feb-115">If the path to the workbook you provided is wrong, you will get a "file not found" exception, which is caught by the following code:</span></span>
    
```cs
  
catch (SoapException e)
{
    Console.WriteLine("SOAP Exception Message: {0}", e.Message);
}
```


```VB.net
  
Catch e As SoapException
Console.WriteLine("SOAP Exception Message: {0}", e.Message)
End Try
```

2. <span data-ttu-id="c9feb-116">Die folgende Ausgabe wird für die SOAP-Ausnahme in der Konsole angezeigt:</span><span class="sxs-lookup"><span data-stu-id="c9feb-116">The application prints the following SOAP exception output to the console:</span></span>
    
```
  
SOAP Exception Message: The file you selected could not be found. Check the spelling of the file name and verify that the location is correct.

```


### <a name="index-out-of-range-exception"></a><span data-ttu-id="c9feb-117">Ausnahme "Der Index liegt außerhalb des gültigen Bereichs"</span><span class="sxs-lookup"><span data-stu-id="c9feb-117">Index Out Of Range Exception</span></span>


1. <span data-ttu-id="c9feb-p103">Wenn Sie versuchen, einen Wert außerhalb des Bereichs abzurufen, erhalten Sie eine **System.IndexOutOfRangeException**-Ausnahme. Die folgende Ausgabe wird in der Konsole angezeigt:</span><span class="sxs-lookup"><span data-stu-id="c9feb-p103">If you try to get a value from outside the range, you will get a **System.IndexOutOfRangeException** exception. The application prints the following output to the console:</span></span>
    
```
  
The Credential is: System.Net.SystemNetworkCredential
The sessionID is : 64.28e58e90-b757-4658-b1c4-890ad68ef6cbRmqR4IINXfkMeOJRG8Iq0Y
27tVk=110.33d3R6fqv7tr2jPyYiPwRu|!@en-US|en-US|+0480#0000-10-00-05T02:00:00:0000
#+0000#0000-04-00-01T02:00:00:0000#-0060
Total rows in range: 18
```

2. <span data-ttu-id="c9feb-120">Anschließend erhalten Sie eine unbehandelte Ausnahme mit folgender Meldung:</span><span class="sxs-lookup"><span data-stu-id="c9feb-120">Then you will get an unhandled exception that says:</span></span>
    
```
  
An unhandled exception of type 'System.IndexOutOfRangeException' occurred in SampleApplication.exe
Additional information: Index was outside the bounds of the array.
```

3. <span data-ttu-id="c9feb-121">Sie können die obige unbehandelte Ausnahme behandeln, indem Sie nach dem **catch**-Block für die SOAP-Ausnahme einen weiteren **catch**-Block zum Abfangen der Ausnahme hinzufügen, wie im Folgenden gezeigt:</span><span class="sxs-lookup"><span data-stu-id="c9feb-121">You can handle the above unhandled exception by adding another **catch** block to catch the exception after the SOAP exception **catch** block as shown here:</span></span>
    
```cs
  
catch (Exception e)
{
    Console.WriteLine("Exception Message: {0}", e.Message);
}
```


```VB.net
  
Catch e As Exception
Console.WriteLine("Exception Message: {0}", e.Message)
End Try
```


### <a name="to-run-the-application-using-f5"></a><span data-ttu-id="c9feb-122">Ausführen der Anwendung mit F5</span><span class="sxs-lookup"><span data-stu-id="c9feb-122">To run the application using F5</span></span>


1. <span data-ttu-id="c9feb-123">Sie können Ihre Anwendung ausführen, indem Sie im Menü **Debuggen** auf **Start** klicken oder **F5** drücken.</span><span class="sxs-lookup"><span data-stu-id="c9feb-123">You can run your application by clicking **Start** on the **Debug** menu, or by pressing **F5**.</span></span> <span data-ttu-id="c9feb-124">Damit sichergestellt ist, dass das Konsolenfenster nach Ausführung des Programms geöffnet bleibt, können Sie am Ende des Codes (nach dem **catch**-Block) die folgende Codezeile hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="c9feb-124">You can run your application by clicking Start on the Debug menu, or by pressing F5. To ensure that the console window remains open after the program has finished executing, you could add the following line of code at the end of your code (after the **catch** block):</span></span>
    
```cs
  
Console.ReadLine();
```


```VB.net
  Console.ReadLine()
```

2. <span data-ttu-id="c9feb-125">Drücken Sie eine beliebige Taste, um SampleApplication.exe zu schließen.</span><span class="sxs-lookup"><span data-stu-id="c9feb-125">Press any key to close SampleApplication.exe.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="c9feb-126">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c9feb-126">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="c9feb-127">Konzepte</span><span class="sxs-lookup"><span data-stu-id="c9feb-127">Concepts</span></span>


  
    
    
 [<span data-ttu-id="c9feb-128">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="c9feb-128">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
#### <a name="other-resources"></a><span data-ttu-id="c9feb-129">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c9feb-129">Other resources</span></span>


  
    
    
 [<span data-ttu-id="c9feb-130">Step 1: Creating the Web Service Client Project</span><span class="sxs-lookup"><span data-stu-id="c9feb-130">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="c9feb-131">Step 2: Adding a Web Reference</span><span class="sxs-lookup"><span data-stu-id="c9feb-131">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="c9feb-132">Step 3: Accessing the Web Service</span><span class="sxs-lookup"><span data-stu-id="c9feb-132">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="c9feb-133">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="c9feb-133">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
  
    
    
 [<span data-ttu-id="c9feb-134">How to: Trust Workbook Locations Using Script</span><span class="sxs-lookup"><span data-stu-id="c9feb-134">How to: Trust Workbook Locations Using Script</span></span>](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx)
