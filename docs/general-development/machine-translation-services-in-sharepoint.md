---
title: "Dienste für maschinelle Übersetzung in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 15a81428-da94-40b8-8ed4-6a12f05661e2
ms.openlocfilehash: e8a47de97c63f8c438d19e07a549a939cce30357
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="machine-translation-services-in-sharepoint"></a>Dienste für maschinelle Übersetzung in SharePoint
Erfahren Sie mehr über Dienst für maschinelle Übersetzung, eine neue Dienstanwendung in SharePoint , die eine automatische maschinelle Übersetzung von Dateien und Websites bietet.
## <a name="machine-translation-service-overview"></a>Dienst für maschinelle Übersetzung-Übersicht
<a name="TranslationSvc_Overview"> </a>


> **Hinweis:** Wenn Sie die Funktion für maschinelle Übersetzung verwenden, können Benutzer Ihre Inhalte zwecks Übersetzung an Microsoft senden. Möglicherweise verwendet Microsoft von Benutzern gesendete Inhalte, um die Qualität der Übersetzungen zu verbessern. Wenn Sie den Dienst für maschinelle Übersetzung in Ihrer Anwendung verwenden, obliegt es Ihnen, die Benutzer darüber zu informieren, dass sie Inhalte zwecks Übersetzung an Microsoft senden können und dass Microsoft von Benutzern gesendete Inhalte möglicherweise zur Verbesserung der Qualität der Übersetzungen nutzt. Weitere Informationen finden Sie in den Datenschutzbestimmungen von Microsoft Translator. 
  
    
    

Dienst für maschinelle Übersetzung ist eine neue Dienstanwendung in SharePoint, die eine automatische maschinelle Übersetzung von Dateien und Websites bietet. Wenn die Dienst für maschinelle Übersetzung-Anwendung eine Übersetzungsanforderung verarbeitet, wird die Anforderung an den in der Cloud gehosteten maschinellen Übersetzungsdienst  [Microsoft Translator](http://www.microsoft.com/de-DE/translator/) weitergeleitet, wo die tatsächliche Übersetzungsarbeit durchgeführt wird. Dieser Clouddienst betreibt auch die Microsoft Office-, Lync-, Yammer und Bing-Übersetzungsfeatures.
  
    
    
The Dienst für maschinelle Übersetzung-Anwendung verarbeitet Übersetzungsanforderungen asynchron und synchron. Asynchrone Übersetzungsanforderungen werden verarbeitet, wenn der Zeitgeberauftrag der Übersetzung ausgeführt wird. Das Standardintervall des Übersetzungszeitgeberauftrags ist 15 Minuten. Sie können diese Einstellung in der Zentraladministration oder mithilfe von Windows PowerShell verwalten. Mithilfe des folgenden Befehls können Sie den Zeitgeber auch so festlegen, dass er sofort ausgeführt wird:
  
    
    



```

$tj = get-sptimerjob "Sharepoint Translation Services"
$tj.Runnow()
```

Synchrone Übersetzungsanforderungen werden verarbeitet, sobald sie gesendet werden.
  
    
    

### <a name="shared-components-with-word-automation-services"></a>Gemeinsam genutzte Komponenten mit Word Automation Services
<a name="TranslationSvc_SharedWAS"> </a>

Die Dienst für maschinelle Übersetzung-Architektur verwendet mehrere Komponenten der Microsoft Word Automation Services-Architektur. Weitere Informationen zur Word Automation Services-Architektur finden Sie unter  [Architektur von Word Automation Services](http://msdn.microsoft.com/library/567bf68d-46bb-4ee8-981d-186549b9e5b8%28Office.15%29.aspx).
  
    
    
Das Dienst für maschinelle Übersetzung-Objektmodell ist dem Word Automation Services-Objektmodell nachgebildet, wenn Sie also mit der Word Automation Services-Programmierung vertraut sind, werden Sie Ähnlichkeiten mit der Programmierung mit dem Dienst für maschinelle Übersetzung-Objektmodell feststellen.
  
    
    

## <a name="using-the-machine-translation-service-server-object-model"></a>Verwenden des Dienst für maschinelle Übersetzung-Serverobjektmodells
<a name="TranslationSvc_ServerOM"> </a>

Anwendungen, die das Serverobjektmodell verwenden, müssen direkt auf einem Server ausgeführt werden, auf dem SharePoint ausgeführt wird. Weitere Informationen zum Erstellen von Anwendungen, die remote gehostet werden können, finden Sie unter  [Verwenden des Dienst für maschinelle Übersetzung-Clientobjektmodells](#TranslationSvc_UsingCSOM) weiter unten in diesem Thema. Das Dienst für maschinelle Übersetzung-Serverobjektmodell befindet sich im **Microsoft.Office.TranslationServices**-Namespace, der sich in "Microsoft.Office.TranslationServices.dll" befindet.
  
    
    
Mithilfe des Serverobjektmodells können Sie Anforderungen an die Dienst für maschinelle Übersetzung-Anwendung asynchron oder synchron (für sofortige Übersetzung) übermitteln. Die Dienst für maschinelle Übersetzung-Anwendung weist zwei Arbeitswarteschlangen für das Speichern von Übersetzungsanforderungen auf: die asynchrone Warteschlange und die synchrone Warteschlange. Anfoderungen in der synchronen Warteschlange werden mit höherer Priorität behandelt und vor Anforderungen in der asynchronen Warteschlange übersetzt. Die Anforderungen werden basierend auf der von Ihnen verwendeten Klasse an eine der beiden Warteschlangen weitergeleitet.
  
    
    

  
    
    
![Verwandte Codeausschnitte und Beispiel-Apps](../images/mod_icon_links_samples.png)
  
    
    
Beispielcode, in dem die Verwendung des Serverobjektmodells aus einer Konsolenanwendung veranschaulicht wird, finden Sie unter  [SharePoint: Zugreifen auf den maschinellen Übersetzungsdienst mithilfe des Serverobjektmodells](http://code.msdn.microsoft.com/SharePoint-Access-86639c3d ).
  
    
    

### <a name="asynchronous-translation-using-the-server-object-model"></a>Asynchrone Übersetzung mithilfe des Serverobjektmodells

Die **TranslationJob**-Klasse definiert einen Satz von zu übersetzenden Elementen. Dies kann eine einzelne Datei oder jede Datei in einem Ordner oder eine Dokumentbibliothek sein. Übersetzungsaufträge, die auf diese Weise übermittelt werden, werden in der Übersetzungsdatenbank gespeichert. Bei jeder Ausführung des Übersetzungszeitgeberauftrags werden einige Aufträge aus der Übersetzungsdatenbank genommen und für die Übersetzung zu der asynchronen Warteschlange hinzugefügt. Das Standardinterall des Übersetzungszeitgeberauftrags beträgt 15 Minuten.
  
    
    
Der folgende Code zeigt, wie eine einzelne Datei asynchron übersetzt wird.
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
TranslationJob job = new TranslationJob(sc, CultureInfo.GetCultureInfo(culture)); 
job.AddFile(input, output);
job.Start(); 

```

Der folgende Code zeigt, wie jede Datei in einem Ordner asynchron übersetzt wird.
  
    
    



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

Der folgende Code zeigt, wie jede Datei in einer Dokumentbibliothek asynchron übersetzt wird.
  
    
    



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


### <a name="synchronous-translation-using-the-server-object-model"></a>Synchrone Übersetzung mithilfe des Serverobjektmodells

Sie verwenden die **SyncTranslator**-Klasse, um eine sofortige Übersetzung für Dateien und Streams anzufordern. Übersetzungsanforderungen, die mithilfe dieser Klasse erfolgen, werden nicht auf die gleiche Art und Weise weitergeleitet wie Anforderungen mithilfe der **TranslationJob**-Klasse. Sie werden unmittelbar der synchronen Warteschlange für die Bearbeitung hinzugefügt. Die **TranslationItemInfo**-Klasse enthält die Details für eine einzelne Datei, die von Dienst für maschinelle Übersetzung übersetzt wird. Die **SyncTranslator.Translate**-Methode gibt eine Instanz dieser Klasse in synchronen Übersetzungsaufträgen zurück.
  
    
    
Der folgende Code zeigt, wie eine einzelne Datei synchron übersetzt wird.
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
SyncTranslator job = new SyncTranslator(sc, CultureInfo.GetCultureInfo(jobCulture));
TranslationItemInfo itemInfo = job.Translate(input, output);

```

Der folgende Code zeigt, wie ein Stream synchron übersetzt wird.
  
    
    



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

Der folgende Code zeigt, wie eine Bytesequenz synchron übersetzt wird.
  
    
    



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


### <a name="permissions"></a>Berechtigungen
<a name="TranslationSvc_Permissions"> </a>

Wenn der Benutzer, für den die Übersetzungsanforderung ausgeführt wird, auf die zu übersetzende Datei zugreifen kann, und dieser Benutzer auf den Ausgabeort der Datei zugreifen kann, so führt der Benutzer die Sicherheitsüberprüfung durch, und die Datei wird übersetzt.
  
    
    

## <a name="using-the-machine-translation-services-client-object-model"></a>Verwenden des Dienst für maschinelle Übersetzung-Clientobjektmodells
<a name="TranslationSvc_UsingCSOM"> </a>

Dienst für maschinelle Übersetzung umfasst auch ein Clientobjektmodell (CSOM), das Zugriff auf die Dienst für maschinelle Übersetzung-API für Online-, lokale und mobile Entwicklung ermöglicht. Clientanwedungen können das CSOM verwenden, um auf Serverinhalte und -funktionen zuzugreifen. Das CSOM implementiert einen Großteil der Übersetzungsfunktionalität des Servers, das CSOM und das serverseitige Objektmodell verfügen jedoch nicht über eine 1:1-Parität. Die asynchrone Übersetzung einzelner Dateien sowie von Dateien in einer Dokumentbibliothek oder in einem Ordner wird unterstützt. Die synchrone Übersetzung von Dateien wird unterstützt, Dateistreams werden jedoch nicht unterstützt.
  
    
    
Das Dienst für maschinelle Übersetzung-CSOM umfasst ein .NET-verwaltetes clientseitiges Objektmodell sowie Microsoft Silverlight- und JavaScript-Objektmodelle. Es basiert auf dem SharePoint-CSOM. Deshalb greift Clientcode zuerst auf das SharePoint-CSOM und dann auf das Dienst für maschinelle Übersetzung-CSOM zu. 
  
    
    
Weitere Informationen zum SharePoint-CSOM finden Sie unter  [SharePoint 2010-Clientobjektmodell](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). Weitere Informaitonen zum **ClientContext**-Objekt, das der Einstiegspunkt für das CSOM ist, finden Sie unter  [Clientkontext als zentrales Objekt](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).
  
    
    
In Tabelle 1 sind die äquivalenten Objekte dargestellt, die die CSOM-APIs für die Dienst für maschinelle Übersetzung-Serverobjekte bereitstellen. 
  
    
    

**Tabelle 1. Serverobjektmodell-APIs und die entsprechenden CSOMs**


|**Server**|**.NET-verwaltet und Silverlight**|**JavaScript**|
|:-----|:-----|:-----|
|Microsoft.Office.TranslationServices.TranslationJob  <br/> |Microsoft.Office.TranslationServices.Client.TranslationJob  <br/> |SP.Translation.TranslationJob  <br/> |
|Microsoft.Office.TranslationServices.TranslationJobInfo  <br/> |Microsoft.Office.TranslationServices.Client.TranslationJobInfo  <br/> |SP.Translation.TranslationJobInfo  <br/> |
|Microsoft.Office.TranslationServices.TranslationItemInfo  <br/> |Microsoft.Office.TranslationServices.Client.TranslationItemInfo  <br/> |SP.Translation.TranslationItemInfo  <br/> |
|Microsoft.Office.TranslationServices.TranslationJobStatus  <br/> |Microsoft.Office.TranslationServices.Client.TranslationJobStatus  <br/> |SP.Translation.TranslationJobStatus  <br/> |
|Microsoft.Office.TranslationServices.SyncTranslator  <br/> |Microsoft.Office.TranslationServices.Client.SyncTranslator  <br/> |SP.Translation.SyncTranslator  <br/> |
   

### <a name="machine-translation-service-net-managed-csom-and-silverlight-csom"></a>Dienst für maschinelle Übersetzung .NET-verwaltetes CSOM und Silverlight-CSOM
<a name="TranslationSvc_ManagedCSOM"> </a>

Rufen Sie für das .NET-verwaltete CSOM eine **ClientContext**-Instanz ab (diese befindet sich im **Microsoft.SharePoint.Client**-Namespace in der Microsoft.SharePoint.Client.dll). Verwenden Sie dann das Objektmodell im **Microsoft.Office.TranslationServices.Client**-Namespace in der "Microsoft.Office.TranslationServices.Client.dll".
  
    
    

  
    
    
![Verwandte Codeausschnitte und Beispiel-Apps](../images/mod_icon_links_samples.png)
  
    
    
Beispielcode, in dem die Verwendung des .NET-verwalteten CSOMs veranschaulicht wird, finden Sie unter  [SharePoint: Zugreifen auf den maschinellen Übersetzungsdienst mithilfe des Clientobjektmodells](http://code.msdn.microsoft.com/SharePoint-Perform-a-8e53b06a).
  
    
    
Rufen Sie für das Silverlight-CSOM eine **ClientContext**-Instanz ab (diese befindet sich im **Microsoft.SharePoint.Client**-Namespace in der "Microsoft.SharePoint.Client.Silverlight.dll"). Verwenden Sie dann das Objektmodell im **Microsoft.Office.TranslationServices.Client**-Namespace in der "Microsoft.Office.TranslationServices.Silverlight.dll".
  
    
    

  
    
    
![Verwandte Codeausschnitte und Beispiel-Apps](../images/mod_icon_links_samples.png)
  
    
    
Beispielcode, in dem die Verwendung des Silverlight-CSOM veranschaulicht wird, finden Sie unter  [SharePoint: Zugreifen auf den maschinellen Übersetzungsdienst von der Silverlight-Anwendung aus](http://code.msdn.microsoft.com/SharePoint-Access-cdaff6b2).
  
    
    
So übersetzen Sie eine einzige Datei asynchron
  
    
    



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

So übersetzen Sie einen Ordner asynchron
  
    
    



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

So übersetzen Sie eine Bibliothek asynchron
  
    
    



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

So übersetzen Sie eine einzige Datei synchron
  
    
    



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

So rufen Sie alle Sprachen ab, die von Dienst für maschinelle Übersetzung unterstützt werden:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
IEnumerable<string> supportedLanguages = TranslationJob.EnumerateSupportedLanguages(clientContext);
clientContext.ExecuteQuery();
foreach (string item in supportedLanguages)
{
    Console.Write(item + ", ");
}
```

So überprüfen Sie, ob eine bestimmte Sprache unterstützt wird
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<bool> isSupported;
isSupported = TranslationJob.IsLanguageSupported(clientContext, "language");
clientContext.ExecuteQuery();
```

So rufen Sie alle Dateinamenerweiterungen ab, die von Dienst für maschinelle Übersetzung unterstützt werden:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
IEnumerable<string> fileExt = TranslationJob.EnumerateSupportedFileExtensions(clientContext);
clientContext.ExecuteQuery();
foreach (string item in fileExt)
{
    Console.Write(item + ", ");
}
```

So überprüfen Sie, ob eine bestimmte Dateinamenerweiterung unterstützt wird
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<bool> isSupported;
isSupported = TranslationJob.IsFileExtensionSupported(clientContext, "fileExtension");
clientContext.ExecuteQuery();

```

So überprüfen Sie die maximale Dateigröße für eine bestimmte Dateinamenerweiterung
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<int> maxSize;
maxSize = TranslationJob.GetMaximumFileSize(clientContext, "fileExtension");
clientContext.ExecuteQuery();
```


### <a name="machine-translation-service-javascript-csom"></a>Dienst für maschinelle Übersetzung JavaScript-CSOM
<a name="TranslationSvc_JavaScriptCSOM"> </a>

Rufen Sie für das JavaScript-CSOM eine **SP.ClientContext**-Instanz ab, und verwenden Sie dann das Objektmodell in der Datei "SP.Translation.js".
  
    
    

  
    
    
![Verwandte Codeausschnitte und Beispiel-Apps](../images/mod_icon_links_samples.png)
  
    
    
Beispielcode, in dem die Verwendung des JavaScript-CSOM veranschaulicht wird, finden Sie unter  [SharePoint: Zugreifen auf den maschinellen Übersetzungsdienst mit JavaScript](http://code.msdn.microsoft.com/SharePoint-Accessing-647f6dd9).
  
    
    
So übersetzen Sie eine einzige Datei asynchron
  
    
    



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

So übersetzen Sie einen Ordner asynchron
  
    
    



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

So übersetzen Sie eine Bibliothek asynchron
  
    
    



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

So übersetzen Sie eine einzige Datei synchron
  
    
    



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

So rufen Sie alle Sprachen ab, die von Dienst für maschinelle Übersetzung unterstützt werden:
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.enumerateSupportedLanguages(clientContext);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededListAllLang),Function.createDelegate(this, this.onQueryFailed));
```

So überprüfen Sie, ob eine bestimmte Sprache unterstützt wird
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.isLanguageSupported(clientContext," language");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededTestLang),Function.createDelegate(this, this.onQueryFailed));
```

So rufen Sie alle Dateinamenerweiterungen ab, die von Dienst für maschinelle Übersetzung unterstützt werden:
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.enumerateSupportedFileExtensions(clientContext);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededListAllFileExt),Function.createDelegate(this, this.onQueryFailed));
```

So überprüfen Sie, ob eine bestimmte Dateinamenerweiterung unterstützt wird
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.isFileExtensionSupported(clientContext," fileExtension");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededTestFileExt),Function.createDelegate(this, this.onQueryFailed));
```


## <a name="machine-translation-service-rest-service"></a>Dienst für maschinelle Übersetzung-REST-Dienst
<a name="TranslationSvc_REST"> </a>

SharePoint umfasst einen REST-Dienst (Representational State Transfer), mit dem Sie remote mit der Dienst für maschinelle Übersetzung-Anwendung unter Verwendung einer Technologie interagieren können, die REST-Webanforderungen unterstützt. Allgemeine Informationen zu REST in SharePoint finden Sie unter  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).
  
    
    

### <a name="ansynchronous-translation-rest-api"></a>Asynchrone Übersetzungs-REST-API

Die REST-API für die asynchrone Übersetzung ist wie folgt: 
  
    
    
 `http://serverName/_api/TranslationJob('language')`
  
    
    
So übersetzen Sie eine einzige Datei asynchron 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateFile(inputFile='/path/intput file', outputFile='/path/output file')`
  
    
    
So übersetzen Sie einen Ordner asynchron 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateFolder(inputFolder='/path/in', outputFolder='/path/out')`
  
    
    
So übersetzen Sie eine Bibliothek asynchron 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateLibrary(inputLibrary='/LibraryName', outputLibrary='/LibraryName'')`
  
    
    

### <a name="synchronous-translation-rest-api"></a>Synchrone Übersetzungs-REST-API

Der Dienst für maschinelle Übersetzung-REST-Dienst unterstützt nur die synchrone Übersetzung von Dateien. Die API hierfür ist wie folgt: 
  
    
    
 `http://serverName/_api/SyncTranslator('language')/Translate(outputFile='/path/output file', inputFile='/path/input file')`
  
    
    

### <a name="additional-machine-translation-service-rest-apis"></a>Zusätzliche Dienst für maschinelle ÜbersetzungREST-APIs

Der Dienst für maschinelle Übersetzung-REST-Dienst umfasst zusätzliche APIs, die Sie zum Abrufen von Informationen zu den Dienst für maschinelle Übersetzung-Anwendungsfunktionen und zum Status des Übersetzungsauftrags verwenden können.
  
    
    
So rufen Sie alle Sprachen ab, die von Dienst für maschinelle Übersetzung unterstützt werden 
  
    
    
 `http://serverName/_api/TranslationJob.EnumerateSupportedLanguages`
  
    
    
So überprüfen Sie, ob eine bestimmte Sprache unterstützt wird 
  
    
    
 `http://serverName/_api/TranslationJob.IsLanguageSupported('language')`
  
    
    
So rufen Sie alle Dateinamenerweiterungen ab, die von Dienst für maschinelle Übersetzung unterstützt werden 
  
    
    
 `http://serverName/_api/TranslationJob.EnumerateSupportedFileEXtensions`
  
    
    
So überprüfen Sie, ob eine bestimmte Dateinamenerweiterung unterstützt wird 
  
    
    
 `http://serverName/_api/TranslationJob.IsFileExtensionSupported('extension')`
  
    
    
So überprüfen Sie die maximale Dateigröße für eine bestimmte Dateinamenerweiterung 
  
    
    
 `http://serverName/_api/TranslationJob.GetMaximumFileSize('extension')`
  
    
    
So rufen Sie eine Liste aller asynchronen Übersetzungsaufträge ab 
  
    
    
 `http://serverName/_api/TranslationJobStatus.GetAllJobs`
  
    
    
So rufen Sie eine Liste aller aktiven asynchronen Übersetzungsaufträge ab 
  
    
    
 `http://serverName/_api/TranslationJobStatus.GetAllActiveJobs`
  
    
    
So rufen Sie die Dokumentinformationen für einen bestimmten asynchronen Übersetzungsauftrag ab 
  
    
    
 `http://serverName/_api/TranslationJobStatus('jobid')/GetAllItems`
  
    
    
So rufen Sie einen asynchronen Übersetzungsauftrag ab 
  
    
    
 `http://serverName/_api/TranslationJob.CancelJob('jobid')`
  
    
    

## <a name="requirements-for-microsoft-word-documents"></a>Anforderungen für Microsoft Word-Dokumente
<a name="TranslationSvc_REST"> </a>

Der SharePoint-Dienst für maschinelle Übersetzungen verwendet beim Übersetzen von Microsoft Word-Dokumenten die Sprache des Absatzes als Ausgangssprache. Wenn der Absatz beispielsweise in Spanisch geschrieben wurde, die Sprache für den Absatz jedoch auf Englisch festgelegt ist, übersetzt der Übersetzungsdienst den Absatz nicht ins Englische. Dies kommt daher, dass der Absatz bereits auf Englisch festgelegt ist.
  
    
    

### <a name="to-set-the-paragraph-language-follow-these-steps"></a>Gehen Sie wie folgt vor, um die Sprache des Absatzes festzulegen:


1. Markieren Sie den Absatz.
    
  
2.  Klicken Sie im Menüband auf die Registerkarte „Überprüfen“.
    
  
3.  Klicken Sie im Dropdownmenü auf „Sprache“, und wählen Sie „Sprache für die Korrekturhilfen festlegen“.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="TranslationSvc_AR"> </a>


-  [Office 2013- und SharePoint-Anwendungsdienste](office-and-sharepoint-application-services.md)
    
  

