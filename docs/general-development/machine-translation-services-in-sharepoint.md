---
title: "Dienste für maschinelle Übersetzung in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 15a81428-da94-40b8-8ed4-6a12f05661e2
ms.openlocfilehash: b6ca7d803db3befe35d49836d441ea5eeee450b5
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="machine-translation-services-in-sharepoint"></a><span data-ttu-id="5a78d-102">Dienste für maschinelle Übersetzung in SharePoint</span><span class="sxs-lookup"><span data-stu-id="5a78d-102">Machine Translation Services in SharePoint</span></span>
<span data-ttu-id="5a78d-103">Erfahren Sie mehr über Dienst für maschinelle Übersetzung, eine neue Dienstanwendung in SharePoint , die eine automatische maschinelle Übersetzung von Dateien und Websites bietet.</span><span class="sxs-lookup"><span data-stu-id="5a78d-103">Learn about the Machine Translation Service, which is a new service application in SharePoint that provides automatic machine translation of files and sites.</span></span>
## <a name="machine-translation-service-overview"></a><span data-ttu-id="5a78d-104">Dienst für maschinelle Übersetzung-Übersicht</span><span class="sxs-lookup"><span data-stu-id="5a78d-104">Machine Translation Service overview</span></span>
<span data-ttu-id="5a78d-105"><a name="TranslationSvc_Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-105"><a name="TranslationSvc_Overview"> </a></span></span>

> [!NOTE]
> <span data-ttu-id="5a78d-106">Wenn Sie die Funktion für maschinelle Übersetzung verwenden, können Benutzer Ihre Inhalte zwecks Übersetzung an Microsoft senden.</span><span class="sxs-lookup"><span data-stu-id="5a78d-106">Note: Using machine translation will allow users to send content to Microsoft for translation.</span></span> <span data-ttu-id="5a78d-107">Möglicherweise verwendet Microsoft von Benutzern gesendete Inhalte, um die Qualität der Übersetzungen zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="5a78d-107">Microsoft may use content users send us to improve the quality of translations.</span></span> <span data-ttu-id="5a78d-108">Wenn Sie den Dienst für maschinelle Übersetzung in Ihrer Anwendung verwenden, obliegt es Ihnen, die Benutzer darüber zu informieren, dass sie Inhalte zwecks Übersetzung an Microsoft senden können und dass Microsoft von Benutzern gesendete Inhalte möglicherweise zur Verbesserung der Qualität der Übersetzungen nutzt.</span><span class="sxs-lookup"><span data-stu-id="5a78d-108">If you use the Machine Translation Service in your application, you are responsible for informing users that this application will allow users to send content to Microsoft for translation and that Microsoft may use content users send us to improve the quality of translations.</span></span> <span data-ttu-id="5a78d-109">Weitere Informationen finden Sie in den Datenschutzbestimmungen von Microsoft Translator.</span><span class="sxs-lookup"><span data-stu-id="5a78d-109">See Microsoft Translator Privacy for more information.</span></span> 
  
    
    

<span data-ttu-id="5a78d-p102">Dienst für maschinelle Übersetzung ist eine neue Dienstanwendung in SharePoint, die eine automatische maschinelle Übersetzung von Dateien und Websites bietet. Wenn die Dienst für maschinelle Übersetzung-Anwendung eine Übersetzungsanforderung verarbeitet, wird die Anforderung an den in der Cloud gehosteten maschinellen Übersetzungsdienst  [Microsoft Translator](http://www.microsoft.com/de-DE/translator/) weitergeleitet, wo die tatsächliche Übersetzungsarbeit durchgeführt wird. Dieser Clouddienst betreibt auch die Microsoft Office-, Lync-, Yammer und Bing-Übersetzungsfeatures.</span><span class="sxs-lookup"><span data-stu-id="5a78d-p102">Machine Translation Service is a new service application in SharePoint that provides automatic machine translation of files and sites. When the Machine Translation Service application processes a translation request, it forwards the request to the  [Microsoft Translator](http://www.microsoft.com/de-DE/translator/) cloud-hosted machine translation service, where the actual translation work is performed. This cloud-service also powers the Microsoft Office, Lync, Yammer and Bing translation features.</span></span>
  
    
    
<span data-ttu-id="5a78d-p103">The Dienst für maschinelle Übersetzung-Anwendung verarbeitet Übersetzungsanforderungen asynchron und synchron. Asynchrone Übersetzungsanforderungen werden verarbeitet, wenn der Zeitgeberauftrag der Übersetzung ausgeführt wird. Das Standardintervall des Übersetzungszeitgeberauftrags ist 15 Minuten. Sie können diese Einstellung in der Zentraladministration oder mithilfe von Windows PowerShell verwalten. Mithilfe des folgenden Befehls können Sie den Zeitgeber auch so festlegen, dass er sofort ausgeführt wird:</span><span class="sxs-lookup"><span data-stu-id="5a78d-p103">The Machine Translation Service application processes translation requests asynchronously and synchronously. Asynchronous translation requests are processed when the translation timer job executes. The default interval of the translation timer job is 15 minutes; you can manage this setting in Central Administration or by using Windows PowerShell. You can also set the timer to execute immediately using the following command:</span></span>
  
    
    



```

$tj = get-sptimerjob "Sharepoint Translation Services"
$tj.Runnow()
```

<span data-ttu-id="5a78d-117">Synchrone Übersetzungsanforderungen werden verarbeitet, sobald sie gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="5a78d-117">Synchronous translation requests are processed as soon as they are submitted.</span></span>
  
    
    

### <a name="shared-components-with-word-automation-services"></a><span data-ttu-id="5a78d-118">Gemeinsam genutzte Komponenten mit Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="5a78d-118">Shared components with Word Automation Services</span></span>
<span data-ttu-id="5a78d-119"><a name="TranslationSvc_SharedWAS"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-119"><a name="TranslationSvc_SharedWAS"> </a></span></span>

<span data-ttu-id="5a78d-p104">Die Dienst für maschinelle Übersetzung-Architektur verwendet mehrere Komponenten der Microsoft Word Automation Services-Architektur. Weitere Informationen zur Word Automation Services-Architektur finden Sie unter  [Architektur von Word Automation Services](http://msdn.microsoft.com/library/567bf68d-46bb-4ee8-981d-186549b9e5b8%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a78d-p104">The Machine Translation Service architecture shares several components from the Microsoft Word Automation Services architecture. For more information about the Word Automation Services architecture, see  [Word Automation Services Architecture](http://msdn.microsoft.com/library/567bf68d-46bb-4ee8-981d-186549b9e5b8%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="5a78d-122">Das Dienst für maschinelle Übersetzung-Objektmodell ist dem Word Automation Services-Objektmodell nachgebildet, wenn Sie also mit der Word Automation Services-Programmierung vertraut sind, werden Sie Ähnlichkeiten mit der Programmierung mit dem Dienst für maschinelle Übersetzung-Objektmodell feststellen.</span><span class="sxs-lookup"><span data-stu-id="5a78d-122">The Machine Translation Service object model is modeled after the Word Automation Services object model, so if you are familiar with Word Automation Services programming, you'll find similarities with programming against the Machine Translation Service object model.</span></span>
  
    
    

## <a name="using-the-machine-translation-service-server-object-model"></a><span data-ttu-id="5a78d-123">Verwenden des Dienst für maschinelle Übersetzung-Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="5a78d-123">Using the Machine Translation Service server object model</span></span>
<span data-ttu-id="5a78d-124"><a name="TranslationSvc_ServerOM"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-124"><a name="TranslationSvc_ServerOM"> </a></span></span>

<span data-ttu-id="5a78d-p105">Anwendungen, die das Serverobjektmodell verwenden, müssen direkt auf einem Server ausgeführt werden, auf dem SharePoint ausgeführt wird. Weitere Informationen zum Erstellen von Anwendungen, die remote gehostet werden können, finden Sie unter  [Verwenden des Dienst für maschinelle Übersetzung-Clientobjektmodells](#TranslationSvc_UsingCSOM) weiter unten in diesem Thema. Das Dienst für maschinelle Übersetzung-Serverobjektmodell befindet sich im **Microsoft.Office.TranslationServices**-Namespace, der sich in "Microsoft.Office.TranslationServices.dll" befindet.</span><span class="sxs-lookup"><span data-stu-id="5a78d-p105">Applications that use the server object model must run directly on a server that is running SharePoint. For information about creating applications that can be hosted remotely, see  [Using the Machine Translation Services client object model](#TranslationSvc_UsingCSOM) later in this topic. The Machine Translation Service server object model resides in the **Microsoft.Office.TranslationServices** namespace, which is located in Microsoft.Office.TranslationServices.dll.</span></span>
  
    
    
<span data-ttu-id="5a78d-p106">Mithilfe des Serverobjektmodells können Sie Anforderungen an die Dienst für maschinelle Übersetzung-Anwendung asynchron oder synchron (für sofortige Übersetzung) übermitteln. Die Dienst für maschinelle Übersetzung-Anwendung weist zwei Arbeitswarteschlangen für das Speichern von Übersetzungsanforderungen auf: die asynchrone Warteschlange und die synchrone Warteschlange. Anfoderungen in der synchronen Warteschlange werden mit höherer Priorität behandelt und vor Anforderungen in der asynchronen Warteschlange übersetzt. Die Anforderungen werden basierend auf der von Ihnen verwendeten Klasse an eine der beiden Warteschlangen weitergeleitet.</span><span class="sxs-lookup"><span data-stu-id="5a78d-p106">Using the server object model, you can submit requests to the Machine Translation Service application asynchronously or synchronously (for instant translation). The Machine Translation Service application has two working queues for storing translation requests: the asynchronous queue and the synchronous queue. Requests in the synchronous queue are treated as higher priority and are translated before requests in the asynchronous queue. The requests are routed to one of these queues based on the class that you use.</span></span>
  
    
    

  
    
    
![Verwandte Codeausschnitte und Beispiel-Apps](../images/mod_icon_links_samples.png)
  
    
    
<span data-ttu-id="5a78d-133">Beispielcode, in dem die Verwendung des Serverobjektmodells aus einer Konsolenanwendung veranschaulicht wird, finden Sie unter  [SharePoint: Zugreifen auf den maschinellen Übersetzungsdienst mithilfe des Serverobjektmodells](http://code.msdn.microsoft.com/SharePoint-Access-86639c3d ).</span><span class="sxs-lookup"><span data-stu-id="5a78d-133">For sample code demonstrating how to use the server object model from a console application, see  [SharePoint: Access Machine Translation Service using server object model](http://code.msdn.microsoft.com/SharePoint-Access-86639c3d ).</span></span>
  
    
    

### <a name="asynchronous-translation-using-the-server-object-model"></a><span data-ttu-id="5a78d-134">Asynchrone Übersetzung mithilfe des Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="5a78d-134">Asynchronous translation using the server object model</span></span>

<span data-ttu-id="5a78d-p107">Die **TranslationJob**-Klasse definiert einen Satz von zu übersetzenden Elementen. Dies kann eine einzelne Datei oder jede Datei in einem Ordner oder eine Dokumentbibliothek sein. Übersetzungsaufträge, die auf diese Weise übermittelt werden, werden in der Übersetzungsdatenbank gespeichert. Bei jeder Ausführung des Übersetzungszeitgeberauftrags werden einige Aufträge aus der Übersetzungsdatenbank genommen und für die Übersetzung zu der asynchronen Warteschlange hinzugefügt. Das Standardinterall des Übersetzungszeitgeberauftrags beträgt 15 Minuten.</span><span class="sxs-lookup"><span data-stu-id="5a78d-p107">The **TranslationJob** class defines a set of items to be translated. This can be a single file or every file within a folder or document library. Translation jobs that are submitted this way are stored in the translation database. Each time the translation timer job runs, it takes some of the jobs from the translation database and adds them to the asynchronous queue to be translated. The default interval of the translation timer job is 15 minutes.</span></span>
  
    
    
<span data-ttu-id="5a78d-140">Der folgende Code zeigt, wie eine einzelne Datei asynchron übersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="5a78d-140">The following code shows how to translate a single file asynchronously.</span></span>
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
TranslationJob job = new TranslationJob(sc, CultureInfo.GetCultureInfo(culture)); 
job.AddFile(input, output);
job.Start(); 

```

<span data-ttu-id="5a78d-141">Der folgende Code zeigt, wie jede Datei in einem Ordner asynchron übersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="5a78d-141">The following code shows how to translate every file within a folder asynchronously.</span></span>
  
    
    



```VB.net

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
TranslationJob job = new TranslationJob(sc, CultureInfo.GetCultureInfo(culture));
using (SPSite siteIn = new SPSite(inputFolder))
{
    using (SPWeb webIn = siteIn.OpenWeb())
    {
        using (SPWeb webOut = siteOut.OpenWeb())
        {
            SPFolder folderIn = webIn.GetFolder(inputFolder);
            SPFolder folderOut = webOut.GetFolder(outputFolder);                    
            job.AddFolder(folderIn, folderOut, true);
            job.Start();
        }
    }
}
```

<span data-ttu-id="5a78d-142">Der folgende Code zeigt, wie jede Datei in einer Dokumentbibliothek asynchron übersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="5a78d-142">The following code shows how to translate every file within a document library asynchronously.</span></span>
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
TranslationJob job = new TranslationJob(sc, CultureInfo.GetCultureInfo(culture));
using (SPSite siteIn = new SPSite(inputList))
{
    using (SPWeb webIn = siteIn.OpenWeb())
    {
        using (SPSite siteOut = new SPSite(outputList))
        {
            using (SPWeb webOut = siteOut.OpenWeb())
            {
                SPDocumentLibrary listIn = (SPDocumentLibrary)webIn.GetList(inputList);
                SPDocumentLibrary listOut = (SPDocumentLibrary)webOut.GetList(outputList);
                job.AddLibrary(listIn, listOut);
                job.Start();
            }
        }
    }
}
```


### <a name="synchronous-translation-using-the-server-object-model"></a><span data-ttu-id="5a78d-143">Synchrone Übersetzung mithilfe des Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="5a78d-143">Synchronous translation using the server object model</span></span>

<span data-ttu-id="5a78d-p108">Sie verwenden die **SyncTranslator**-Klasse, um eine sofortige Übersetzung für Dateien und Streams anzufordern. Übersetzungsanforderungen, die mithilfe dieser Klasse erfolgen, werden nicht auf die gleiche Art und Weise weitergeleitet wie Anforderungen mithilfe der **TranslationJob**-Klasse. Sie werden unmittelbar der synchronen Warteschlange für die Bearbeitung hinzugefügt. Die **TranslationItemInfo**-Klasse enthält die Details für eine einzelne Datei, die von Dienst für maschinelle Übersetzung übersetzt wird. Die **SyncTranslator.Translate**-Methode gibt eine Instanz dieser Klasse in synchronen Übersetzungsaufträgen zurück.</span><span class="sxs-lookup"><span data-stu-id="5a78d-p108">You use the **SyncTranslator** class to request instant translation for files and streams. Translation requests that are made by using this class are not routed the same way as requests that are made by using the **TranslationJob** class. They are immediately added to the synchronous queue to be processed. The **TranslationItemInfo** class contains the details for a single item that is translated by the Machine Translation Service. The **SyncTranslator.Translate** method returns an instance of this class in synchronous translation jobs.</span></span>
  
    
    
<span data-ttu-id="5a78d-149">Der folgende Code zeigt, wie eine einzelne Datei synchron übersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="5a78d-149">The following code shows how to translate a single file synchronously.</span></span>
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
SyncTranslator job = new SyncTranslator(sc, CultureInfo.GetCultureInfo(jobCulture));
TranslationItemInfo itemInfo = job.Translate(input, output);

```

<span data-ttu-id="5a78d-150">Der folgende Code zeigt, wie ein Stream synchron übersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="5a78d-150">The following code shows how to translate a stream synchronously.</span></span>
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
SyncTranslator job = new SyncTranslator(sc, CultureInfo.GetCultureInfo(jobCulture));
FileStream inputStream = new FileStream(input, FileMode.Open);
FileStream outputStream = new FileStream(output, FileMode.Create);     
TranslationItemInfo itemInfo = job.Translate(inputStream, outputStream, fileFormat);
inputStream.Close();
outputStream.Flush();
outputStream.Close();

```

<span data-ttu-id="5a78d-151">Der folgende Code zeigt, wie eine Bytesequenz synchron übersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="5a78d-151">The following code shows how to translate a sequence of bytes synchronously.</span></span>
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
SyncTranslator job = new SyncTranslator(sc, CultureInfo.GetCultureInfo(jobCulture));
Byte[] inputByte;
Byte[] outputByte;
inputByte = File.ReadAllBytes(input);
outputByte = null;
TranslationItemInfo itemInfo = job.Translate(inputByte, out outputByte, fileFormat);
FileStream outputStream = File.Open(output, FileMode.Create);
MemoryStream memoryStream = new MemoryStream(outputByte);
memoryStream.WriteTo(outputStream);
outputStream.Flush();
outputStream.Close();

```


### <a name="permissions"></a><span data-ttu-id="5a78d-152">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="5a78d-152">Permissions</span></span>
<span data-ttu-id="5a78d-153"><a name="TranslationSvc_Permissions"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-153"><a name="TranslationSvc_Permissions"> </a></span></span>

<span data-ttu-id="5a78d-154">Wenn der Benutzer, für den die Übersetzungsanforderung ausgeführt wird, auf die zu übersetzende Datei zugreifen kann, und dieser Benutzer auf den Ausgabeort der Datei zugreifen kann, so führt der Benutzer die Sicherheitsüberprüfung durch, und die Datei wird übersetzt.</span><span class="sxs-lookup"><span data-stu-id="5a78d-154">If the user who the translation request is running for can access the file to be translated, and that user can access the output location for the file, the user clears the security check and the file is translated.</span></span>
  
    
    

## <a name="using-the-machine-translation-services-client-object-model"></a><span data-ttu-id="5a78d-155">Verwenden des Dienst für maschinelle Übersetzung-Clientobjektmodells</span><span class="sxs-lookup"><span data-stu-id="5a78d-155">Using the Machine Translation Services client object model</span></span>
<span data-ttu-id="5a78d-156"><a name="TranslationSvc_UsingCSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-156"><a name="TranslationSvc_UsingCSOM"> </a></span></span>

<span data-ttu-id="5a78d-p109">Dienst für maschinelle Übersetzung umfasst auch ein Clientobjektmodell (CSOM), das Zugriff auf die Dienst für maschinelle Übersetzung-API für Online-, lokale und mobile Entwicklung ermöglicht. Clientanwedungen können das CSOM verwenden, um auf Serverinhalte und -funktionen zuzugreifen. Das CSOM implementiert einen Großteil der Übersetzungsfunktionalität des Servers, das CSOM und das serverseitige Objektmodell verfügen jedoch nicht über eine 1:1-Parität. Die asynchrone Übersetzung einzelner Dateien sowie von Dateien in einer Dokumentbibliothek oder in einem Ordner wird unterstützt. Die synchrone Übersetzung von Dateien wird unterstützt, Dateistreams werden jedoch nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="5a78d-p109">Machine Translation Service also includes a client object model (CSOM) that enables access to the Machine Translation Service API for online, on-premises, and mobile development. Client applications can use the CSOM to access server content and functionality. The CSOM implements most of the translation functionality of the server, but the CSOM and the server-side object model do not have one-to-one parity. Asynchronous translation of individual files, and files in a document library or folder are supported. Synchronous translation of files is supported, but file streams are not supported.</span></span>
  
    
    
<span data-ttu-id="5a78d-p110">Das Dienst für maschinelle Übersetzung-CSOM umfasst ein .NET-verwaltetes clientseitiges Objektmodell sowie Microsoft Silverlight- und JavaScript-Objektmodelle. Es basiert auf dem SharePoint-CSOM. Deshalb greift Clientcode zuerst auf das SharePoint-CSOM und dann auf das Dienst für maschinelle Übersetzung-CSOM zu.</span><span class="sxs-lookup"><span data-stu-id="5a78d-p110">The Machine Translation Service CSOM includes a .NET managed client-side object model and Microsoft Silverlight and JavaScript object models. It is built on the SharePoint CSOM. Therefore, client code first accesses the SharePoint CSOM and then accesses the Machine Translation Service CSOM.</span></span> 
  
    
    
<span data-ttu-id="5a78d-p111">Weitere Informationen zum SharePoint-CSOM finden Sie unter  [SharePoint 2010-Clientobjektmodell](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). Weitere Informaitonen zum **ClientContext**-Objekt, das der Einstiegspunkt für das CSOM ist, finden Sie unter  [Clientkontext als zentrales Objekt](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a78d-p111">For more information about the SharePoint CSOM, see  [SharePoint 2010 Client Object Model](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). For more information about the **ClientContext** object, which is the entry point to the CSOM, see [Client Context as Central Object](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="5a78d-167">In Tabelle 1 sind die äquivalenten Objekte dargestellt, die die CSOM-APIs für die Dienst für maschinelle Übersetzung-Serverobjekte bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="5a78d-167">Table 1 shows the equivalent objects that the CSOM APIs provide for the Machine Translation Service server objects.</span></span> 
  
    
    

<span data-ttu-id="5a78d-168">**Tabelle 1. Serverobjektmodell-APIs und die entsprechenden CSOMs**</span><span class="sxs-lookup"><span data-stu-id="5a78d-168">**Table 1. Server object model APIs and their CSOM equivalents**</span></span>


|<span data-ttu-id="5a78d-169">**Server**</span><span class="sxs-lookup"><span data-stu-id="5a78d-169">**Server**</span></span>|<span data-ttu-id="5a78d-170">**.NET-verwaltet und Silverlight**</span><span class="sxs-lookup"><span data-stu-id="5a78d-170">**.NET Managed and Silverlight**</span></span>|<span data-ttu-id="5a78d-171">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5a78d-171">**JavaScript**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5a78d-172">Microsoft.Office.TranslationServices.TranslationJob</span><span class="sxs-lookup"><span data-stu-id="5a78d-172">Microsoft.Office.TranslationServices.TranslationJob</span></span>  <br/> |<span data-ttu-id="5a78d-173">Microsoft.Office.TranslationServices.Client.TranslationJob</span><span class="sxs-lookup"><span data-stu-id="5a78d-173">Microsoft.Office.TranslationServices.Client.TranslationJob</span></span>  <br/> |<span data-ttu-id="5a78d-174">SP.Translation.TranslationJob</span><span class="sxs-lookup"><span data-stu-id="5a78d-174">SP.Translation.TranslationJob</span></span>  <br/> |
|<span data-ttu-id="5a78d-175">Microsoft.Office.TranslationServices.TranslationJobInfo</span><span class="sxs-lookup"><span data-stu-id="5a78d-175">Microsoft.Office.TranslationServices.TranslationJobInfo</span></span>  <br/> |<span data-ttu-id="5a78d-176">Microsoft.Office.TranslationServices.Client.TranslationJobInfo</span><span class="sxs-lookup"><span data-stu-id="5a78d-176">Microsoft.Office.TranslationServices.Client.TranslationJobInfo</span></span>  <br/> |<span data-ttu-id="5a78d-177">SP.Translation.TranslationJobInfo</span><span class="sxs-lookup"><span data-stu-id="5a78d-177">SP.Translation.TranslationJobInfo</span></span>  <br/> |
|<span data-ttu-id="5a78d-178">Microsoft.Office.TranslationServices.TranslationItemInfo</span><span class="sxs-lookup"><span data-stu-id="5a78d-178">Microsoft.Office.TranslationServices.TranslationItemInfo</span></span>  <br/> |<span data-ttu-id="5a78d-179">Microsoft.Office.TranslationServices.Client.TranslationItemInfo</span><span class="sxs-lookup"><span data-stu-id="5a78d-179">Microsoft.Office.TranslationServices.Client.TranslationItemInfo</span></span>  <br/> |<span data-ttu-id="5a78d-180">SP.Translation.TranslationItemInfo</span><span class="sxs-lookup"><span data-stu-id="5a78d-180">SP.Translation.TranslationItemInfo</span></span>  <br/> |
|<span data-ttu-id="5a78d-181">Microsoft.Office.TranslationServices.TranslationJobStatus</span><span class="sxs-lookup"><span data-stu-id="5a78d-181">Microsoft.Office.TranslationServices.TranslationJobStatus</span></span>  <br/> |<span data-ttu-id="5a78d-182">Microsoft.Office.TranslationServices.Client.TranslationJobStatus</span><span class="sxs-lookup"><span data-stu-id="5a78d-182">Microsoft.Office.TranslationServices.Client.TranslationJobStatus</span></span>  <br/> |<span data-ttu-id="5a78d-183">SP.Translation.TranslationJobStatus</span><span class="sxs-lookup"><span data-stu-id="5a78d-183">SP.Translation.TranslationJobStatus</span></span>  <br/> |
|<span data-ttu-id="5a78d-184">Microsoft.Office.TranslationServices.SyncTranslator</span><span class="sxs-lookup"><span data-stu-id="5a78d-184">Microsoft.Office.TranslationServices.SyncTranslator</span></span>  <br/> |<span data-ttu-id="5a78d-185">Microsoft.Office.TranslationServices.Client.SyncTranslator</span><span class="sxs-lookup"><span data-stu-id="5a78d-185">Microsoft.Office.TranslationServices.Client.SyncTranslator</span></span>  <br/> |<span data-ttu-id="5a78d-186">SP.Translation.SyncTranslator</span><span class="sxs-lookup"><span data-stu-id="5a78d-186">SP.Translation.SyncTranslator</span></span>  <br/> |
   

### <a name="machine-translation-service-net-managed-csom-and-silverlight-csom"></a><span data-ttu-id="5a78d-187">Dienst für maschinelle Übersetzung .NET-verwaltetes CSOM und Silverlight-CSOM</span><span class="sxs-lookup"><span data-stu-id="5a78d-187">Machine Translation Service .NET managed CSOM and Silverlight CSOM</span></span>
<span data-ttu-id="5a78d-188"><a name="TranslationSvc_ManagedCSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-188"><a name="TranslationSvc_ManagedCSOM"> </a></span></span>

<span data-ttu-id="5a78d-p112">Rufen Sie für das .NET-verwaltete CSOM eine **ClientContext**-Instanz ab (diese befindet sich im **Microsoft.SharePoint.Client**-Namespace in der Microsoft.SharePoint.Client.dll). Verwenden Sie dann das Objektmodell im **Microsoft.Office.TranslationServices.Client**-Namespace in der "Microsoft.Office.TranslationServices.Client.dll".</span><span class="sxs-lookup"><span data-stu-id="5a78d-p112">For the .NET managed CSOM, get a **ClientContext** instance (located in the **Microsoft.SharePoint.Client** namespace in the Microsoft.SharePoint.Client.dll). Then use the object model in the **Microsoft.Office.TranslationServices.Client** namespace in the Microsoft.Office.TranslationServices.Client.dll.</span></span>
  
    
    

  
    
    
![Verwandte Codeausschnitte und Beispiel-Apps](../images/mod_icon_links_samples.png)
  
    
    
<span data-ttu-id="5a78d-192">Beispielcode, in dem die Verwendung des .NET-verwalteten CSOMs veranschaulicht wird, finden Sie unter  [SharePoint: Zugreifen auf den maschinellen Übersetzungsdienst mithilfe des Clientobjektmodells](http://code.msdn.microsoft.com/SharePoint-Perform-a-8e53b06a).</span><span class="sxs-lookup"><span data-stu-id="5a78d-192">For sample code demonstrating how to use the .NET Managed CSOM, see  [SharePoint: Access Machine Translation Service using the client object model](http://code.msdn.microsoft.com/SharePoint-Perform-a-8e53b06a).</span></span>
  
    
    
<span data-ttu-id="5a78d-p113">Rufen Sie für das Silverlight-CSOM eine **ClientContext**-Instanz ab (diese befindet sich im **Microsoft.SharePoint.Client**-Namespace in der "Microsoft.SharePoint.Client.Silverlight.dll"). Verwenden Sie dann das Objektmodell im **Microsoft.Office.TranslationServices.Client**-Namespace in der "Microsoft.Office.TranslationServices.Silverlight.dll".</span><span class="sxs-lookup"><span data-stu-id="5a78d-p113">For the Silverlight CSOM, get a **ClientContext** instance (located in the **Microsoft.SharePoint.Client** namespace in the Microsoft.SharePoint.Client.Silverlight.dll). Then use the object model in the **Microsoft.Office.TranslationServices.Client** namespace in the Microsoft.Office.TranslationServices.Silverlight.dll.</span></span>
  
    
    

  
    
    
![Verwandte Codeausschnitte und Beispiel-Apps](../images/mod_icon_links_samples.png)
  
    
    
<span data-ttu-id="5a78d-196">Beispielcode, in dem die Verwendung des Silverlight-CSOM veranschaulicht wird, finden Sie unter  [SharePoint: Zugreifen auf den maschinellen Übersetzungsdienst von der Silverlight-Anwendung aus](http://code.msdn.microsoft.com/SharePoint-Access-cdaff6b2).</span><span class="sxs-lookup"><span data-stu-id="5a78d-196">For sample code demonstrating how to use the Silverlight CSOM, see  [SharePoint: Access Machine Translation Service from Silverlight application](http://code.msdn.microsoft.com/SharePoint-Access-cdaff6b2).</span></span>
  
    
    
<span data-ttu-id="5a78d-197">So übersetzen Sie eine einzige Datei asynchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-197">To translate a single file asynchronously:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
string culture  = "cultureID";
string name = "translationJobName";
string  inputFile =  "http://serverName/path/inputFileName";
string outputFile = "http://serverName/path/outputFileName";
TranslationJob job = new TranslationJob(clientContext , culture);
job.AddFile(inputFile , outputFile);
job.Name = name;
job.Start();
clientContext.Load(job);
clientContext.ExecuteQuery();
//To retrieve the translation job ID.
string jobID = job.JobId;
```

<span data-ttu-id="5a78d-198">So übersetzen Sie einen Ordner asynchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-198">To translate a folder asynchronously:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
string culture = "cultureID";
string name = "translationJobName";
string inputFolder = clientContext.Web.GetFolderByServerRelativeUrl("inFolderPath");
string outputFolder = clientContext.Web.GetFolderByServerRelativeUrl("outFolderPath");  
TranslationJob job = new TranslationJob(clientContext , culture);
job.AddFolder(inputFolder, outputFolder, true);
job.Name = name;
job.Start();            
clientContext.Load(job);
clientContext.ExecuteQuery();
//To retrieve the translation job ID.
string jobID = job.JobId;
```

<span data-ttu-id="5a78d-199">So übersetzen Sie eine Bibliothek asynchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-199">To translate a library asynchronously:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
string culture = "cultureID";
string name = "translationJobName";
string inputLibrary = clientContext.Web.Lists.GetByTitle("inputLibraryName");
string outputLibrary = clientContext.Web.Lists.GetByTitle("outputLibraryName");
TranslationJob job = new TranslationJob(clientContext , culture);
job.AddFolder(inputLibrary , outputLibrary , true);
job.Name = name;
job.Start();            
clientContext.Load(job);
clientContext.ExecuteQuery();
//To retrieve the translation job ID.
string jobID = job.JobId;
```

<span data-ttu-id="5a78d-200">So übersetzen Sie eine einzige Datei synchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-200">To translate a single file synchronously:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
string culture = "cultureID"
string inputFile = "http://serverName/path/inputFileName";
string outputFile = "http://serverName/path/outputFileName";
SyncTranslator job = new SyncTranslator(clientContext , culture);
job.OutputSaveBehavior = SaveBehavior.AlwaysOverwrite;
ClientResult<TranslationItemInfo> cr = job.Translate(inputFile, outputFile );
clientContext.ExecuteQuery(); 
//To retrieve additional information about the translation job.
string errorCode = clientContext.Value.ErrorCode;
string errorMessage = clientContext.Value.ErrorMessage;
string translateID = clientContext.Value.TranslationId;
string succeedResult  = clientContext.Value.Succeeded;
string failResult  = clientContext.Value.Failed;
string cancelStatus = clientContext.Value.Canceled;
string inProgressStatus = clientContext.Value.InProgress;
string notStartedStatus = clientContext.Value.NotStarted;
```

<span data-ttu-id="5a78d-201">So rufen Sie alle Sprachen ab, die von Dienst für maschinelle Übersetzung unterstützt werden:</span><span class="sxs-lookup"><span data-stu-id="5a78d-201">To retrieve all languages that are supported by the Machine Translation Service:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
IEnumerable<string> supportedLanguages = TranslationJob.EnumerateSupportedLanguages(clientContext);
clientContext.ExecuteQuery();
foreach (string item in supportedLanguages)
{
    Console.Write(item + ", ");
}
```

<span data-ttu-id="5a78d-202">So überprüfen Sie, ob eine bestimmte Sprache unterstützt wird</span><span class="sxs-lookup"><span data-stu-id="5a78d-202">To check whether a specific language is supported:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<bool> isSupported;
isSupported = TranslationJob.IsLanguageSupported(clientContext, "language");
clientContext.ExecuteQuery();
```

<span data-ttu-id="5a78d-203">So rufen Sie alle Dateinamenerweiterungen ab, die von Dienst für maschinelle Übersetzung unterstützt werden:</span><span class="sxs-lookup"><span data-stu-id="5a78d-203">To retrieve all the file name extensions that are supported by the Machine Translation Service:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
IEnumerable<string> fileExt = TranslationJob.EnumerateSupportedFileExtensions(clientContext);
clientContext.ExecuteQuery();
foreach (string item in fileExt)
{
    Console.Write(item + ", ");
}
```

<span data-ttu-id="5a78d-204">So überprüfen Sie, ob eine bestimmte Dateinamenerweiterung unterstützt wird</span><span class="sxs-lookup"><span data-stu-id="5a78d-204">To check whether a specific file name extension is supported:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<bool> isSupported;
isSupported = TranslationJob.IsFileExtensionSupported(clientContext, "fileExtension");
clientContext.ExecuteQuery();

```

<span data-ttu-id="5a78d-205">So überprüfen Sie die maximale Dateigröße für eine bestimmte Dateinamenerweiterung</span><span class="sxs-lookup"><span data-stu-id="5a78d-205">To check the file size limit for a specific file name extension:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<int> maxSize;
maxSize = TranslationJob.GetMaximumFileSize(clientContext, "fileExtension");
clientContext.ExecuteQuery();
```


### <a name="machine-translation-service-javascript-csom"></a><span data-ttu-id="5a78d-206">Dienst für maschinelle Übersetzung JavaScript-CSOM</span><span class="sxs-lookup"><span data-stu-id="5a78d-206">Machine Translation Service JavaScript CSOM</span></span>
<span data-ttu-id="5a78d-207"><a name="TranslationSvc_JavaScriptCSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-207"><a name="TranslationSvc_JavaScriptCSOM"> </a></span></span>

<span data-ttu-id="5a78d-208">Rufen Sie für das JavaScript-CSOM eine **SP.ClientContext**-Instanz ab, und verwenden Sie dann das Objektmodell in der Datei "SP.Translation.js".</span><span class="sxs-lookup"><span data-stu-id="5a78d-208">For the JavaScript CSOM, get an **SP.ClientContext** instance, and then use the object model in the SP.Translation.js file.</span></span>
  
    
    

  
    
    
![Verwandte Codeausschnitte und Beispiel-Apps](../images/mod_icon_links_samples.png)
  
    
    
<span data-ttu-id="5a78d-210">Beispielcode, in dem die Verwendung des JavaScript-CSOM veranschaulicht wird, finden Sie unter  [SharePoint: Zugreifen auf den maschinellen Übersetzungsdienst mit JavaScript](http://code.msdn.microsoft.com/SharePoint-Accessing-647f6dd9).</span><span class="sxs-lookup"><span data-stu-id="5a78d-210">For sample code demonstrating how to use the JavaScript CSOM, see  [SharePoint: Accessing the Machine Translation Service with JavaScript](http://code.msdn.microsoft.com/SharePoint-Accessing-647f6dd9).</span></span>
  
    
    
<span data-ttu-id="5a78d-211">So übersetzen Sie eine einzige Datei asynchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-211">To translate a single file asynchronously:</span></span>
  
    
    



```

var asyncJob;
var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
asyncJob = SP.Translation.TranslationJob.newObject(clientContext, "cultureID");
asyncJob.set_outputSaveBehavior(SP.Translation.SaveBehavior.alwaysOverwrite);
asyncJob.addFile("inputFilePath", "outputFilePath");
asyncJob.set_name("translationJobName");
asyncJob.start();
clientContext.load(asyncJob);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededASync),Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="5a78d-212">So übersetzen Sie einen Ordner asynchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-212">To translate a folder asynchronously:</span></span>
  
    
    



```

var asyncJob;
var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
asyncJob = SP.Translation.TranslationJob.newObject(clientContext, "cultureID");
asyncJob.set_outputSaveBehavior(SP.Translation.SaveBehavior.alwaysOverwrite);
var inputFolder = clientContext.get_web().getFolderByServerRelativeUrl("inputFilePath");
var outputFolder = clientContext.get_web().getFolderByServerRelativeUrl("outputFilePath");
asyncJob.addFolder(inputFolder, outputFolder, true);
asyncJob.set_name("translationJobName");
asyncJob.start();
clientContext.load(asyncJob);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededASync),Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="5a78d-213">So übersetzen Sie eine Bibliothek asynchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-213">To translate a library asynchronously:</span></span>
  
    
    



```

var asyncJob;
var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
asyncJob = SP.Translation.TranslationJob.newObject(clientContext, "cultureID");
asyncJob.set_outputSaveBehavior(SP.Translation.SaveBehavior.alwaysOverwrite);
var inputLibrary= clientContext.get_web().get_lists().getByTitle("inputFilePath");
var outputLibrary= clientContext.get_web().get_lists().getByTitle("outputFilePath");
asyncJob.addLibrary(inputLibrary, outputLibrary);
asyncJob.set_name("translationJobName");
asyncJob.start();
clientContext.load(asyncJob);
clientContext.executeQueryAsync(Function.createDelegate(this,this.onQuerySucceededASync),Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="5a78d-214">So übersetzen Sie eine einzige Datei synchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-214">To translate a single file synchronously:</span></span>
  
    
    



```

var result;
var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var job = SP.Translation.SyncTranslator.newObject(clientContext, "cultureID");
job.set_outputSaveBehavior(SP.Translation.SaveBehavior.alwaysOverwrite);
result = job.translate("inputFilePath", "outputFilePath");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededSync),
Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="5a78d-215">So rufen Sie alle Sprachen ab, die von Dienst für maschinelle Übersetzung unterstützt werden:</span><span class="sxs-lookup"><span data-stu-id="5a78d-215">To retrieve all languages that are supported by the Machine Translation Service:</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.enumerateSupportedLanguages(clientContext);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededListAllLang),Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="5a78d-216">So überprüfen Sie, ob eine bestimmte Sprache unterstützt wird</span><span class="sxs-lookup"><span data-stu-id="5a78d-216">To check whether a specific language is supported:</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.isLanguageSupported(clientContext," language");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededTestLang),Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="5a78d-217">So rufen Sie alle Dateinamenerweiterungen ab, die von Dienst für maschinelle Übersetzung unterstützt werden:</span><span class="sxs-lookup"><span data-stu-id="5a78d-217">To retrieve all the file name extensions that are supported by the Machine Translation Service:</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.enumerateSupportedFileExtensions(clientContext);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededListAllFileExt),Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="5a78d-218">So überprüfen Sie, ob eine bestimmte Dateinamenerweiterung unterstützt wird</span><span class="sxs-lookup"><span data-stu-id="5a78d-218">To check whether a specific file name extension is supported:</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.isFileExtensionSupported(clientContext," fileExtension");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededTestFileExt),Function.createDelegate(this, this.onQueryFailed));
```


## <a name="machine-translation-service-rest-service"></a><span data-ttu-id="5a78d-219">Dienst für maschinelle Übersetzung-REST-Dienst</span><span class="sxs-lookup"><span data-stu-id="5a78d-219">Machine Translation Service REST service</span></span>
<span data-ttu-id="5a78d-220"><a name="TranslationSvc_REST"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-220"><a name="TranslationSvc_REST"> </a></span></span>

<span data-ttu-id="5a78d-p114">SharePoint umfasst einen REST-Dienst (Representational State Transfer), mit dem Sie remote mit der Dienst für maschinelle Übersetzung-Anwendung unter Verwendung einer Technologie interagieren können, die REST-Webanforderungen unterstützt. Allgemeine Informationen zu REST in SharePoint finden Sie unter  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a78d-p114">SharePoint includes a Representational State Transfer (REST) service that enables you to remotely interact with the Machine Translation Service application by using any technology that supports REST web requests. For general information about REST in SharePoint, see  [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span></span>
  
    
    

### <a name="ansynchronous-translation-rest-api"></a><span data-ttu-id="5a78d-223">Asynchrone Übersetzungs-REST-API</span><span class="sxs-lookup"><span data-stu-id="5a78d-223">Ansynchronous Translation REST API</span></span>

<span data-ttu-id="5a78d-224">Die REST-API für die asynchrone Übersetzung ist wie folgt:</span><span class="sxs-lookup"><span data-stu-id="5a78d-224">The REST API for performing asynchronous translation is as follows:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob('language')`
  
    
    
<span data-ttu-id="5a78d-225">So übersetzen Sie eine einzige Datei asynchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-225">To translate a single file asynchronously:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateFile(inputFile='/path/intput file', outputFile='/path/output file')`
  
    
    
<span data-ttu-id="5a78d-226">So übersetzen Sie einen Ordner asynchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-226">To translate a folder asynchronously:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateFolder(inputFolder='/path/in', outputFolder='/path/out')`
  
    
    
<span data-ttu-id="5a78d-227">So übersetzen Sie eine Bibliothek asynchron</span><span class="sxs-lookup"><span data-stu-id="5a78d-227">To translate a library asynchronously:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateLibrary(inputLibrary='/LibraryName', outputLibrary='/LibraryName'')`
  
    
    

### <a name="synchronous-translation-rest-api"></a><span data-ttu-id="5a78d-228">Synchrone Übersetzungs-REST-API</span><span class="sxs-lookup"><span data-stu-id="5a78d-228">Synchronous Translation REST API</span></span>

<span data-ttu-id="5a78d-p115">Der Dienst für maschinelle Übersetzung-REST-Dienst unterstützt nur die synchrone Übersetzung von Dateien. Die API hierfür ist wie folgt:</span><span class="sxs-lookup"><span data-stu-id="5a78d-p115">The Machine Translation Service REST service supports only synchronous translation of files. The API for this is as follows:</span></span> 
  
    
    
 `http://serverName/_api/SyncTranslator('language')/Translate(outputFile='/path/output file', inputFile='/path/input file')`
  
    
    

### <a name="additional-machine-translation-service-rest-apis"></a><span data-ttu-id="5a78d-231">Zusätzliche Dienst für maschinelle ÜbersetzungREST-APIs</span><span class="sxs-lookup"><span data-stu-id="5a78d-231">Additional Machine Translation Service REST APIs</span></span>

<span data-ttu-id="5a78d-232">Der Dienst für maschinelle Übersetzung-REST-Dienst umfasst zusätzliche APIs, die Sie zum Abrufen von Informationen zu den Dienst für maschinelle Übersetzung-Anwendungsfunktionen und zum Status des Übersetzungsauftrags verwenden können.</span><span class="sxs-lookup"><span data-stu-id="5a78d-232">The Machine Translation Service REST service includes additional APIs that you can use to retrieve information about the Machine Translation Service application capabilities and translation job status.</span></span>
  
    
    
<span data-ttu-id="5a78d-233">So rufen Sie alle Sprachen ab, die von Dienst für maschinelle Übersetzung unterstützt werden</span><span class="sxs-lookup"><span data-stu-id="5a78d-233">To retrieve all languages supported by Machine Translation Service:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.EnumerateSupportedLanguages`
  
    
    
<span data-ttu-id="5a78d-234">So überprüfen Sie, ob eine bestimmte Sprache unterstützt wird</span><span class="sxs-lookup"><span data-stu-id="5a78d-234">To check whether a specific language is supported:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.IsLanguageSupported('language')`
  
    
    
<span data-ttu-id="5a78d-235">So rufen Sie alle Dateinamenerweiterungen ab, die von Dienst für maschinelle Übersetzung unterstützt werden</span><span class="sxs-lookup"><span data-stu-id="5a78d-235">To retrieve all the file name extensions that are supported by Machine Translation Service:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.EnumerateSupportedFileEXtensions`
  
    
    
<span data-ttu-id="5a78d-236">So überprüfen Sie, ob eine bestimmte Dateinamenerweiterung unterstützt wird</span><span class="sxs-lookup"><span data-stu-id="5a78d-236">To check whether a specific file name extension is supported:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.IsFileExtensionSupported('extension')`
  
    
    
<span data-ttu-id="5a78d-237">So überprüfen Sie die maximale Dateigröße für eine bestimmte Dateinamenerweiterung</span><span class="sxs-lookup"><span data-stu-id="5a78d-237">To check the file size limit for a specific file name extension:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.GetMaximumFileSize('extension')`
  
    
    
<span data-ttu-id="5a78d-238">So rufen Sie eine Liste aller asynchronen Übersetzungsaufträge ab</span><span class="sxs-lookup"><span data-stu-id="5a78d-238">To retrieve a list of all the asynchronous translation jobs:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJobStatus.GetAllJobs`
  
    
    
<span data-ttu-id="5a78d-239">So rufen Sie eine Liste aller aktiven asynchronen Übersetzungsaufträge ab</span><span class="sxs-lookup"><span data-stu-id="5a78d-239">To retrieve a list of all the active asynchronous translation jobs:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJobStatus.GetAllActiveJobs`
  
    
    
<span data-ttu-id="5a78d-240">So rufen Sie die Dokumentinformationen für einen bestimmten asynchronen Übersetzungsauftrag ab</span><span class="sxs-lookup"><span data-stu-id="5a78d-240">To retrieve the document information for a specific asynchronous translation job:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJobStatus('jobid')/GetAllItems`
  
    
    
<span data-ttu-id="5a78d-241">So rufen Sie einen asynchronen Übersetzungsauftrag ab</span><span class="sxs-lookup"><span data-stu-id="5a78d-241">To cancel an asynchronous translation job:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.CancelJob('jobid')`
  
    
    

## <a name="requirements-for-microsoft-word-documents"></a><span data-ttu-id="5a78d-242">Anforderungen für Microsoft Word-Dokumente</span><span class="sxs-lookup"><span data-stu-id="5a78d-242">Requirements for Microsoft Word Documents</span></span>
<span data-ttu-id="5a78d-243"><a name="TranslationSvc_REST"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-243"><a name="TranslationSvc_REST"> </a></span></span>

<span data-ttu-id="5a78d-p116">Der SharePoint-Dienst für maschinelle Übersetzungen verwendet beim Übersetzen von Microsoft Word-Dokumenten die Sprache des Absatzes als Ausgangssprache. Wenn der Absatz beispielsweise in Spanisch geschrieben wurde, die Sprache für den Absatz jedoch auf Englisch festgelegt ist, übersetzt der Übersetzungsdienst den Absatz nicht ins Englische. Dies kommt daher, dass der Absatz bereits auf Englisch festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="5a78d-p116">SharePoint Machine Translation Service uses the paragraph language as the Source Language when it translates Microsoft Word documents. For example, if the paragraph is written in Spanish but the language for the paragraph is set to English, the Translation Service will not translate it to English. This is because it is already set to English.</span></span>
  
    
    

### <a name="to-set-the-paragraph-language-follow-these-steps"></a><span data-ttu-id="5a78d-247">Gehen Sie wie folgt vor, um die Sprache des Absatzes festzulegen:</span><span class="sxs-lookup"><span data-stu-id="5a78d-247">To set the paragraph language, follow these steps:</span></span>


1. <span data-ttu-id="5a78d-248">Markieren Sie den Absatz.</span><span class="sxs-lookup"><span data-stu-id="5a78d-248">Select the paragraph.</span></span>
    
  
2.  <span data-ttu-id="5a78d-249">Klicken Sie im Menüband auf die Registerkarte „Überprüfen“.</span><span class="sxs-lookup"><span data-stu-id="5a78d-249">Click the Review Ribbon tab.</span></span>
    
  
3.  <span data-ttu-id="5a78d-250">Klicken Sie im Dropdownmenü auf „Sprache“, und wählen Sie „Sprache für die Korrekturhilfen festlegen“.</span><span class="sxs-lookup"><span data-stu-id="5a78d-250">Click Language from the drop-down menu, and choose Set Proofing Language.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="5a78d-251">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="5a78d-251">See also</span></span>
<span data-ttu-id="5a78d-252"><a name="TranslationSvc_AR"> </a></span><span class="sxs-lookup"><span data-stu-id="5a78d-252"><a name="TranslationSvc_AR"> </a></span></span>


-  [<span data-ttu-id="5a78d-253">Office 2013- und SharePoint-Anwendungsdienste</span><span class="sxs-lookup"><span data-stu-id="5a78d-253">Office 2013 and SharePoint application services</span></span>](office-and-sharepoint-application-services.md)
    
  

