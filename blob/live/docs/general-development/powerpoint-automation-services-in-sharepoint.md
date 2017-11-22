---
title: PowerPoint-Automatisierungsdienste in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 168c7dc0-fbdc-41a2-84db-65d211d3d673
ms.openlocfilehash: 38aaa276eb79da8e7ad6a63e4b043c762535923a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="powerpoint-automation-services-in-sharepoint"></a><span data-ttu-id="d8e68-102">PowerPoint-Automatisierungsdienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8e68-102">PowerPoint Automation Services in SharePoint</span></span>
<span data-ttu-id="d8e68-103">In diesem Artikel erfahren Sie, wie Sie mithilfe von Microsoft PowerPoint Automation Services Präsentationen serverseitig in verschiedene Dateiformate bzw. aus verschiedenen Dateiformaten konvertieren können.</span><span class="sxs-lookup"><span data-stu-id="d8e68-103">Learn to use Microsoft PowerPoint Automation Services to do server-side presentation conversions to and from a variety of file formats.</span></span> 

## <a name="introduction"></a><span data-ttu-id="d8e68-104">Einführung</span><span class="sxs-lookup"><span data-stu-id="d8e68-104">Introduction</span></span>
<span data-ttu-id="d8e68-105"><a name="PAS_Intro"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-105"></span></span>

<span data-ttu-id="d8e68-106">Viele Unternehmen unterschiedlichster Größe verwenden ihre Microsoft SharePoint Server-Bibliotheken als Repository für Microsoft PowerPoint-Präsentationen.</span><span class="sxs-lookup"><span data-stu-id="d8e68-106">Many businesses, large and small, use their Microsoft SharePoint Server libraries as a repository for Microsoft PowerPoint presentations.</span></span> <span data-ttu-id="d8e68-107">Dabei stellen sie alle jeweils eigene Anforderungen an die Speicherung, Verteilung und Aktualisierung der Präsentationen.</span><span class="sxs-lookup"><span data-stu-id="d8e68-107">These businesses all have their own particular needs for storing, distributing, and updating their presentations.</span></span> <span data-ttu-id="d8e68-108">Microsoft PowerPoint Automation Services ist ein neues Feature von Microsoft SharePoint, mit dem Unternehmen ihre Präsentationen verwalten können.</span><span class="sxs-lookup"><span data-stu-id="d8e68-108">Microsoft PowerPoint Automation Services is a new feature of Microsoft SharePoint that can help enterprises to manage their presentations.</span></span> <span data-ttu-id="d8e68-109">Es handelt sich um einen freigegebenen Dienst, der eine unbeaufsichtigte, serverseitige Konvertierung von Präsentationen in andere Formate ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="d8e68-109">It is a shared service that provides unattended, server-side conversion of presentations into other formats.</span></span> <span data-ttu-id="d8e68-110">Er wurde speziell für die Ausführung auf Servern entwickelt und kann auch eine große Anzahl von Präsentationsdateien zuverlässig und vorhersehbar verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="d8e68-110">It was designed from the outset to work on servers and can process many presentation files in a reliable and predictable manner.</span></span>
  
    
    
<span data-ttu-id="d8e68-p102">Mit PowerPoint Automation Services können Sie das PowerPoint-Binärdateiformat (.ppt) und das PowerPoint-Open XML-Dateiformat (.pptx) in andere Formate konvertieren. Sie können beispielsweise mehrere PowerPoint 97-2003-Dateien in Open XML-Präsentationsdateien konvertieren. Sie können auch eine benutzerdefinierte Aktion im Menü **Bearbeiten** erstellen, damit Benutzer bei Bedarf eine PDF-Version ihrer Präsentationen erstellen können.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p102">Using PowerPoint Automation Services, you can convert from the PowerPoint binary file format (.ppt) and the PowerPoint Open XML file format (.pptx) to other formats. For example, you may want to upgrade a batch of PowerPoint 97-2003 files to Open XML presentation files. You could also create a custom action in the **Edit** menu to allow users to create a PDF version of presentations on demand.</span></span>
  
    
    

> <span data-ttu-id="d8e68-114">**Hinweis:** PowerPoint Automation Services nutzt Funktionen von SharePoint und ist selbst ein Feature von SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d8e68-114">**Note:** PowerPoint Automation Services takes advantage of facilities of SharePoint and is a feature of it.</span></span> <span data-ttu-id="d8e68-115">Sie können PowerPoint Automation Services nur verwenden, wenn SharePoint installiert ist.</span><span class="sxs-lookup"><span data-stu-id="d8e68-115">You must have SharePoint installed to use PowerPoint Automation Services.</span></span> <span data-ttu-id="d8e68-116">Wenn Sie SharePoint in einer Serverfarm verwenden, müssen Sie PowerPoint Automation Services explizit aktivieren.</span><span class="sxs-lookup"><span data-stu-id="d8e68-116">If you are using SharePoint in a server farm, you must explicitly enable PowerPoint Automation Services.</span></span> 
  
    
    


## <a name="powerpoint-automation-services-scenarios"></a><span data-ttu-id="d8e68-117">Anwendungsszenarien für PowerPoint Automation Services</span><span class="sxs-lookup"><span data-stu-id="d8e68-117">PowerPoint Automation Services scenarios</span></span>
<span data-ttu-id="d8e68-118"><a name="PAS_Scenarios"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-118"></span></span>

<span data-ttu-id="d8e68-119">Die folgenden Szenarien beschreiben einige Möglichkeiten der Verwendung von PowerPoint Automation Services zum Automatisieren der Präsentationsverarbeitung auf einem Server:</span><span class="sxs-lookup"><span data-stu-id="d8e68-119">The following scenarios describe a couple of ways that you can use PowerPoint Automation Services to automate processing presentations on a server:</span></span>
  
    
    

- <span data-ttu-id="d8e68-p104">Ein Großunternehmen speichert alle Präsentationen zum Gewinn in einer einzelnen Dokumentbibliothek auf einer Unternehmens-Intranetwebsite. Die Bibliothek enthält zahlreiche Präsentationen, die sich über die Jahre angesammelt haben. Die IT-Abteilung möchte alle Präsentationsdateien im PowerPoint 97-2003-Binärdateiformat (.ppt) in das Open XML-Präsentationsdateiformat (.pptx) umwandeln. Die diese Konvertierung durchführenden Entwickler möchten eine Lösung auf dem Server bereitstellen, die alle Dateien in der Bibliothek durchläuft, prüft, ob die Datei das PPT-Format aufweist, und anschließend eine solche Datei in das PPTX-Dateiformat umwandelt.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p104">A large enterprise stores all of their yearly earnings presentations in a single document library on a corporate intranet site. The library contains a large number of presentations that have accumulated over the years. The IT department wants to upgrade all of the presentation files in the PowerPoint 97-2003 binary file format (.ppt) to the Open XML presentation file format (.pptx). The developer who is performing the conversion decides to deploy a solution to the server that will iterate through each of the files in the library, check to see whether the file is in the .ppt format, and convert each .ppt file to the .pptx file format.</span></span>
    
  
- <span data-ttu-id="d8e68-p105">Eine regionale Vertriebsabteilung bietet maßgeschneiderte Kundendienstangebote für jeden einzelnen Kunden. Jeder Verkäufer überprüft zusammen mit dem Kunden seine Angebote in einem Meeting, entweder persönlich oder online. Nach dem Meeting stellt der Verkäufer eine Kopie des Angebots für den Kunden in Form einer PDF zur Verfügung. Die Abteilung beauftragt einen Anbieter damit, ein benutzerdefiniertes Verb im Menü **Bearbeiten** für die in einer Dokumentbibliothek in ihrem Extranet gespeicherten PowerPoint-Dateien zu erstellen. Durch Klicken auf das Verb führt der Server ein Programm aus, das die PowerPoint-Datei in eine in der gleichen Bibliothek gespeicherte PDF umwandelt.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p105">A regional sales department provides custom service estimates to each of their clients. Each salesperson reviews their quotes with clients in a meeting, either in-person or online. After the meeting, the salesperson provides a copy of the quote to the customer in the form of a PDF. The department hires a vendor to create a custom verb in the **Edit** menu for PowerPoint files stored in a document library in their extranet. When the verb is clicked, the server runs a program that converts the PowerPoint file to a PDF located in the same library.</span></span>
    
  

### <a name="supported-source-presentation-formats"></a><span data-ttu-id="d8e68-129">Unterstützte Formate der Quellpräsentation</span><span class="sxs-lookup"><span data-stu-id="d8e68-129">Supported source presentation formats</span></span>

<span data-ttu-id="d8e68-130">Die folgenden Formate der Quellpräsentation werden bei der Konvertierung unterstützt:</span><span class="sxs-lookup"><span data-stu-id="d8e68-130">The supported source presentation formats for conversion are as follows:</span></span>
  
    
    

- <span data-ttu-id="d8e68-131">Open XML-Präsentationsformat (.pptx)</span><span class="sxs-lookup"><span data-stu-id="d8e68-131">Open XML File Format presentation format (.pptx)</span></span>
    
  
- <span data-ttu-id="d8e68-132">PowerPoint 97-2003-Präsentation (.ppt)</span><span class="sxs-lookup"><span data-stu-id="d8e68-132">PowerPoint 97-2003 presentation (.ppt)</span></span>
    
  

### <a name="supported-destination-document-formats"></a><span data-ttu-id="d8e68-133">Unterstützte Formate des Zieldokuments</span><span class="sxs-lookup"><span data-stu-id="d8e68-133">Supported destination document formats</span></span>

<span data-ttu-id="d8e68-134">Die unterstützten Formate der Zieldokumente umfassen alle unterstützten Formate der Quelldokumente und die folgenden Formate:</span><span class="sxs-lookup"><span data-stu-id="d8e68-134">The supported destination document formats include all of the supported source document formats and the following:</span></span>
  
    
    

- <span data-ttu-id="d8e68-135">.pptx (Open XML-Präsentationsformat)</span><span class="sxs-lookup"><span data-stu-id="d8e68-135">.pptx (Open XML File Format presentation format)</span></span>
    
  
- <span data-ttu-id="d8e68-136">.pdf</span><span class="sxs-lookup"><span data-stu-id="d8e68-136">Pdf</span></span>
    
  
- <span data-ttu-id="d8e68-137">.xps (Open XML Paper Specification)</span><span class="sxs-lookup"><span data-stu-id="d8e68-137">.xps (Open XML Paper Specification)</span></span>
    
  
- <span data-ttu-id="d8e68-138">.jpg</span><span class="sxs-lookup"><span data-stu-id="d8e68-138">JPG</span></span>
    
  
- <span data-ttu-id="d8e68-139">.png (Portable Network Graphics Format)</span><span class="sxs-lookup"><span data-stu-id="d8e68-139">.png (Portable Network Graphics Format)</span></span>
    
  

### <a name="limitations-of-powerpoint-automation-services"></a><span data-ttu-id="d8e68-140">Einschränkungen von PowerPoint Automation Services</span><span class="sxs-lookup"><span data-stu-id="d8e68-140">Limitations of PowerPoint Automation Services</span></span>

<span data-ttu-id="d8e68-p106">PowerPoint Automation Services umfasst keine Funktionen zum Ausdrucken von Dokumenten. Es ist jedoch einfach, PowerPoint-Präsentationsdateien (.ppt und .pptx) in PDF- oder XPS-Dateien zu konvertieren, und sie an einen Drucker zu senden.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p106">PowerPoint Automation Services does not include capabilities for printing documents. However, it is straightforward to convert PowerPoint presentation files (.ppt and .pptx) to PDF or XPS and spool them to a printer.</span></span>
  
    
    

## <a name="powerpoint-automation-services-api"></a><span data-ttu-id="d8e68-143">PowerPoint Automation Services-API</span><span class="sxs-lookup"><span data-stu-id="d8e68-143">PowerPoint Automation Services API</span></span>
<span data-ttu-id="d8e68-144"><a name="PAS_APIs"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-144"></span></span>

<span data-ttu-id="d8e68-145">Wenn Sie PowerPoint Automation Services verwenden möchten, senden Sie über die Programmierschnittstelle des Features eine Konvertierungsanforderung an den SharePoint-Server.</span><span class="sxs-lookup"><span data-stu-id="d8e68-145">To use PowerPoint Automation Services, you use its programming interface to send a conversion request to the SharePoint server.</span></span> <span data-ttu-id="d8e68-146">In jeder Konvertierungsanforderung geben Sie an, welche Dateien konvertiert werden sollen und welches Ausgabeformat für den Konvertierungsauftrag gewünscht ist.</span><span class="sxs-lookup"><span data-stu-id="d8e68-146">For each conversion request, you specify which files you want to convert and the output format of the conversion job.</span></span> <span data-ttu-id="d8e68-147">In einigen Konvertierungsanforderungen können Sie zusätzlich angeben, welche Inhaltstypen konvertiert werden sollen, beispielsweise Kommentare, ausgeblendete Folien oder Dokumenteigenschaften.</span><span class="sxs-lookup"><span data-stu-id="d8e68-147">For some conversion requests, you can also specify what types of content is converted, including comments, hidden slides, or document properties.</span></span>
  
    
    
<span data-ttu-id="d8e68-p108">PowerPoint Automation Services verwendet die asynchrone Mustermethode zum Senden und Empfangen von Konvertierungsanforderungen. Sie können somit einen Code schreiben, mit dem mit der Ausführung fortgefahren wird, nachdem eine Konvertierungsanforderung gesendet wurde. Wenn Sie die Benutzer über den Abschluss einer Konvertierungsanforderung benachrichtigen möchten, können Sie eine Stellvertretung angeben, die auf eine auszuführende Rückrufmethode verweist, sobald der Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p108">PowerPoint Automation Services uses the asynchronous pattern method for sending and receiving conversion requests. Thus, you can write code that continues to execute after a conversion request has been sent. If you need to provide notification to users after a conversion request has been completed, you can specify a delegate that references a callback method to execute when the operation completes.</span></span> 
  
    
    

> <span data-ttu-id="d8e68-151">**Hinweis:** Weitere Informationen zur Arbeit mit dem asynchronen Entwurfsmuster finden Sie in unserem [Übersichtsartikel zum asynchronen Programmiermodell](http://msdn.microsoft.com/de-DE/library/ms228963.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8e68-151">**Note** For more information about how to work with the asynchronous design pattern, see the  [Asynchronous Programming Overview](http://msdn.microsoft.com/de-DE/library/ms228963.aspx).</span></span> 
  
    
    

<span data-ttu-id="d8e68-p109">Die folgenden Abschnitte beinhalten eine eingeschränkte Liste von Klassen, die zum Senden und Empfangen von Konvertierungsanforderungen erforderlich sind. All diese Klassen sind im **Microsoft.Office.Server.PowerPoint.Conversion**-Namespace enthalten.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p109">The sections below contain a limited list of the classes that are necessary for sending and receiving a conversion requests. All of these classes are contained in the **Microsoft.Office.Server.PowerPoint.Conversion** namespace.</span></span>
  
    
    

### <a name="request-base-class"></a><span data-ttu-id="d8e68-154">Request-Basisklasse</span><span class="sxs-lookup"><span data-stu-id="d8e68-154">Request Base Class</span></span>

<span data-ttu-id="d8e68-p110">Die **Request**-Klasse ist die grundlegendste Klasse im **Microsoft.Office.Server.PowerPoint.Conversion**-Namespace. Alle anderen request-Typen - **PresentationRequest**, **PictureRequest**, **PdfRequest** und **XpsRequest** - erben von dieser.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p110">The **Request** class is the most fundamental class within the **Microsoft.Office.Server.PowerPoint.Conversion** namespace. All of the otherrequest types— **PresentationRequest**, **PictureRequest**, **PdfRequest**, and **XpsRequest**—inherit from it.</span></span> 
  
    
    

<span data-ttu-id="d8e68-157">**Tabelle 1. Request-Basisklassenelemente**</span><span class="sxs-lookup"><span data-stu-id="d8e68-157">**Table 1. Request base class members**</span></span>


|<span data-ttu-id="d8e68-158">**Elementname**</span><span class="sxs-lookup"><span data-stu-id="d8e68-158">**Member name**</span></span>|<span data-ttu-id="d8e68-159">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="d8e68-159">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d8e68-160">**BeginConvert(Microsoft.SharePoint.SPServiceContext, System.AsyncCallback, System.Object)**-Methode</span><span class="sxs-lookup"><span data-stu-id="d8e68-160">**BeginConvert(Microsoft.SharePoint.SPServiceContext, System.AsyncCallback, System.Object)** method</span></span> <br/> |<span data-ttu-id="d8e68-p111">Startet den Konvertierungsvorgang. Der erste Parameter,  _serviceContext_, gibt den Kontext der SharePoint-Website an, auf der sich die zu konvertierende Datei befindet. Mit dem  _callback_-Parameter können Sie einen Delegaten festlegen, der auf eine Methode verweist, die nach Abschluss des Vorgangs auszuführen ist. Verwenden Sie den  _state_-Parameter, wenn weitere Informationen aus dem aufrufenden Code an die Rückrufmethode übergeben werden müssen.  </span><span class="sxs-lookup"><span data-stu-id="d8e68-p111">Begins the conversion operation. The first parameter,  _serviceContext_, specifies the context of the SharePoint site where the file to be converted is located. Use the  _callback_ parameter to specify a delegate that references a method to execute once the operation has completed. Use the _state_ parameter if you need to pass any additional information from the calling code to the callback method. </span></span><br/> <span data-ttu-id="d8e68-165">Gibt ein  [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) -Objekt zurück.</span><span class="sxs-lookup"><span data-stu-id="d8e68-165">Returns an  [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) object.</span></span> <br/> |
|<span data-ttu-id="d8e68-166">**EndConvert(IAsyncResult)**-Methode</span><span class="sxs-lookup"><span data-stu-id="d8e68-166">**EndConvert(IAsyncResult)** method</span></span> <br/> |<span data-ttu-id="d8e68-p112">Beendet den Konvertierungsvorgang. Der  _result_-Parameter erwartet das resultierende  [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) -Objekt, das von der entsprechenden **BeginConvert**-Konvertierungsanforderung zurückgegeben wird. Wenn diese Anforderung zum Zeitpunkt des Aufrufs von **EndConvert**noch nicht abgeschlossen wurde, wird der aufrufende Thread blockiert, bis der Konvertierungsvorgang abgeschlossen ist.  </span><span class="sxs-lookup"><span data-stu-id="d8e68-p112">Ends the conversion operation. The  _result_ parameter expects the resulting [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) object that the corresponding **BeginConvert** conversion request returns. If that request has not been completed when **EndConvert** is called, the calling thread is blocked until the conversion operation is complete. </span></span><br/> <span data-ttu-id="d8e68-170">Gibt keinen Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="d8e68-170">Does not return a value.</span></span>  <br/> |
   

### <a name="presentationrequest-class"></a><span data-ttu-id="d8e68-171">PresentationRequest-Klasse</span><span class="sxs-lookup"><span data-stu-id="d8e68-171">PresentationRequest class</span></span>

<span data-ttu-id="d8e68-p113">Die **PresentationRequest**-Klasse, die von der **Request**-Klasse erbt, wandelt eine PowerPoint 97-2003-Datei (.ppt) oder Open XML-Präsentationsdatei (.pptx) in ein anderes Dateiformat um. Im ersten oben erwähnten Szenario wird diese Klasse zum Konvertieren älterer Präsentationsdateien in einer Dokumentbibliothek in das Open XML-Präsentationsdateiformat verwendet.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p113">The **PresentationRequest** class, which inherits from the **Request** class, converts a PowerPoint 97-2003 file (.ppt) or Open XML File Format presentation (.pptx) to another presentation file format. In the first scenario mentioned above, you use this class to convert older presentation files in a document library to the Open XML File Format presentation format.</span></span>
  
    
    
<span data-ttu-id="d8e68-174">Die Konstruktormethode für die **PresentationRequest**-klasse verfügt über drei erforderliche Parameter:</span><span class="sxs-lookup"><span data-stu-id="d8e68-174">The constructor method for the **PresentationRequest** class has three required parameters:</span></span>
  
    
    

-  <span data-ttu-id="d8e68-175">_input_ Wählt die Datei, die Sie in ein [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) -Objekt konvertiert möchten.</span><span class="sxs-lookup"><span data-stu-id="d8e68-175">_input_—Takes the file that you want to convert as a  [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) object.</span></span>
    
  
-  <span data-ttu-id="d8e68-176">_extension_ Eine Zeichenfolge, die die Dateierweiterung der zu konvertierenden Datei angibt.</span><span class="sxs-lookup"><span data-stu-id="d8e68-176">_extension_—A string that specifies the file extension of the file being converted.</span></span>
    
  
-  <span data-ttu-id="d8e68-177">_output_ Ein [SPFileStream](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfilestream.aspx)-Objekt, das den Speicherort für die Ausgabe festlegt.</span><span class="sxs-lookup"><span data-stu-id="d8e68-177">_output_—An  [SPFileStream](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfilestream.aspx) object that specifies where the output will be stored.</span></span>
    
  
<span data-ttu-id="d8e68-p114">Die **PresentationRequest**-Klasse verfügt über eine Überladung für die Konstruktormethode, die einen  _settings_-Parameter hinzufügt. Der  _settings_-Parameter lässt ein **PresentationSettings**-Objekt als Argument zu.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p114">The **PresentationRequest** class has a single overload for its constructor method that adds a _settings_ parameter. The _settings_ parameter accepts a **PresentationSettings** object as an argument.</span></span>
  
    
    

> <span data-ttu-id="d8e68-180">**Tipp:** Vergewissern Sie sich bei der Rückkonvertierung des Ausgabeobjekts des Typs [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) in ein Objekt des Typs [SPFile](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfile.aspx), dass die Dateiendung der ausgegebenen Datei der Dateiendung des gewünschten Dateityps entspricht (.ppt oder .pptx).</span><span class="sxs-lookup"><span data-stu-id="d8e68-180">**TIP** When converting the output  [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) object back to an [SPFile](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfile.aspx) object, check that the extension given to the resulting file matches the extension of the file type that you want (.ppt or .pptx).</span></span>
  
    
    


### <a name="pdfrequest-class"></a><span data-ttu-id="d8e68-181">PdfRequest-Klasse</span><span class="sxs-lookup"><span data-stu-id="d8e68-181">PdfRequest class</span></span>

<span data-ttu-id="d8e68-p115">Die **PdfRequest**-Klasse, die auch von der **Request**-Klasse erbt, konvertiert eine PowerPoint 97-2003-Datei (.ppt) oder Open XML-Präsentationsdatei (.pptx.) in eine PDF-Datei. Im zweiten oben erwähnten Szenario wird diese Klasse zum Konvertieren von Präsentationen in PDF-Dateien verwendet.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p115">The **PdfRequest** class, which also inherits from the **Request** class, converts a PowerPoint 97-2003 file (.ppt) or Open XML File Format presentation (.pptx) to a.pdf file. In the second scenario mentioned above, you use this class to convert presentations to PDF files.</span></span>
  
    
    
<span data-ttu-id="d8e68-184">Die Konstruktormethode für die **PdfRequest**-Klasse verfügt, ähnlich wie die **PresentationRequest**-Klasse, ebenfalls über drei erforderliche Parameter:  _input_,  _extension_ und _output_.</span><span class="sxs-lookup"><span data-stu-id="d8e68-184">The constructor method for the **PdfRequest** class also has three required parameters— _input_,  _extension_, and  _output_—similar to the **PresentationRequest** class.</span></span>
  
    
    
<span data-ttu-id="d8e68-p116">Die **PdfRequest**-Klasse verfügt auch über eine Überladung für die Konstruktormethode, die einen  _settings_-Parameter hinzufügt. Der  _settings_-Parameter lässt ein **FixedFormatSettings**-Objekt als Argument zu.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p116">The **PdfRequest** class also has a single overload for its constructor method that adds a _settings_ parameter. The _settings_ parameter accepts a **FixedFormatSettings** object as an argument.</span></span>
  
    
    

> <span data-ttu-id="d8e68-187">**Tipp:** Vergewissern Sie sich bei der Rückkonvertierung des Ausgabeobjekts des Typs [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) in ein Objekt des Typs [SPFile](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfile.aspx), dass die Dateiendung der ausgegebenen Datei der Dateiendung des gewünschten Dateityps entspricht (.pdf).</span><span class="sxs-lookup"><span data-stu-id="d8e68-187">**TIP** When converting the output  [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) object back to an [SPFile](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfile.aspx) object, check that the extension given to the resulting file matches the extension of the file type that you want (.pdf).</span></span>
  
    
    


### <a name="picturerequest-class"></a><span data-ttu-id="d8e68-188">PictureRequest-Klasse</span><span class="sxs-lookup"><span data-stu-id="d8e68-188">PictureRequest class</span></span>

<span data-ttu-id="d8e68-189">Die **PictureRequest**-Klasse, die auch von der **Request**-Klasse erbt, wandelt eine PowerPoint 97-2003-Datei (.ppt) oder Open XML-Präsentationsdatei File (.pptx) in eine Auflistung von Bilddateien im JPG- oder PNG-Format um.</span><span class="sxs-lookup"><span data-stu-id="d8e68-189">The **PictureRequest** class, which also inherits from the **Request** class, converts a PowerPoint 97-2003 file (.ppt) or Open XML File Format presentation (.pptx) to a collection of image files in either the.jpg or .png format.</span></span>
  
    
    
<span data-ttu-id="d8e68-p117">Die Konstruktormethode für die **PictureRequest**-Klasse verfügt ebenfalls über vier erforderliche Parameter. Die  _input_-,  _extension_- und _output_-Parameter ähneln den Parametern für den **PresentationRequest**-Klassenkonstruktor. Die Konstruktormethode für die **PictureRequest**-Klasse verfügt auch über einen erforderlichen  _format_-Parameter, der eine Konstante aus der **PictureFormat**-Enumeration sein muss.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p117">The constructor method for the **PictureRequest** class also has four required parameters. The _input_,  _extension_, and  _output_ parameters are similar to the parameters for the **PresentationRequest** class constructor. The constructor method for the **PictureRequest** class also has a required _format_ parameter, which must be a constant from the **PictureFormat** enumeration.</span></span>
  
    
    
<span data-ttu-id="d8e68-193">Die Klasse **PictureRequest** hat keine Überladungen für ihre Konstruktormethode.</span><span class="sxs-lookup"><span data-stu-id="d8e68-193">The **PictureRequest** class does not have any overloads for its constructor method.</span></span>
  
    
    

> <span data-ttu-id="d8e68-194">**Tipp:** Die Klasse **PictureRequest** gibt einen Datenstrom mit einem Paket von Bilddateien zurück.</span><span class="sxs-lookup"><span data-stu-id="d8e68-194">**Tip:** The **PictureRequest** class returns a stream that contains a package of image files.</span></span> <span data-ttu-id="d8e68-195">Vergewissern Sie sich bei der Rückkonvertierung des Ausgabeobjekts des Typs [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) in ein Objekt des Typs [SPFile](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfile.aspx), dass die ausgegebene Datei die Dateiendung „.zip“ hat.</span><span class="sxs-lookup"><span data-stu-id="d8e68-195">TIP The PictureRequest class returns a stream that contains a package of image files. When converting the output [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) object back to an [SPFile](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfile.aspx) object, check that the extension given to the resulting file is .zip.</span></span>
  
    
    


## <a name="building-a-powerpoint-automation-services-application"></a><span data-ttu-id="d8e68-196">Erstellen einer PowerPoint Automation Services-Anwendung</span><span class="sxs-lookup"><span data-stu-id="d8e68-196">Building a PowerPoint Automation Services application</span></span>
<span data-ttu-id="d8e68-197"><a name="PAS_Build"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-197"></span></span>

<span data-ttu-id="d8e68-p119">Am einfachsten kann das Schreiben von Code, der PowerPoint Automation Services verwendet, anhand der Erstellung einer Konsolenanwendung veranschaulicht werden. Sie müssen die Konsolenanwendung auf dem SharePoint Server, und nicht auf einem Clientcomputer erstellen und ausführen. Der Code zum Starten von Konvertierungsanforderung weicht, abhängig davon, ob der Konvertierungsanforderungscode in einem Webpart, einem Workflow oder einem Ereignishandler integriert ist, nur gering ab. In der folgenden Vorgehensweise wird dargestellt, wie eine API bei der Verwendung von PowerPoint Automation Services aus einer Konsolenanwendung ohne zusätzliche Komplexität eines Webparts, eines Ereignishandlers oder eines Workflows verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p119">The easiest way to show how to write code that uses PowerPoint Automation Services is to build a console application. You must build and run the console application on the SharePoint Server, not on a client computer. The code to start conversion requests is similar whether the conversion request code is incorporated into a Web Part, a workflow, or an event handler. By using PowerPoint Automation Services from a console application, the following procedure shows how to use the API without adding the complexities of a Web Part, an event handler, or a workflow.</span></span>
  
    
    

> <span data-ttu-id="d8e68-202">**Hinweis:** Da PowerPoint Automation Services ein SharePoint-Dienst ist, können Sie das Feature nur in Anwendungen verwenden, die direkt unter SharePoint Server ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="d8e68-202">**Note** Because PowerPoint Automation Services is a service of SharePoint Server 2013, you can use it only in an application that runs directly on a SharePoint Server. You must build the application as a farm solution. You cannot use PowerPoint Automation Services from a sandboxed solution.</span></span> <span data-ttu-id="d8e68-203">Die Anwendung muss als Farmlösung erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="d8e68-203">You must build the application as a farm solution.</span></span> <span data-ttu-id="d8e68-204">PowerPoint Automation Services lässt sich nicht in Sandkastenlösungen einsetzen.</span><span class="sxs-lookup"><span data-stu-id="d8e68-204">You cannot use PowerPoint Automation Services from a sandboxed solution.</span></span> 
  
    
    


### <a name="to-build-the-application"></a><span data-ttu-id="d8e68-205">So erstellen Sie die Anwendung</span><span class="sxs-lookup"><span data-stu-id="d8e68-205">To build the application</span></span>


1. <span data-ttu-id="d8e68-206">Starten Sie Microsoft Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="d8e68-206">Start Microsoft Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="d8e68-207">Zeigen Sie im Menü **Datei** auf **Neu**, und wählen Sie dann **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-207">On the **File** menu, point to **New**, and then choose **Project**.</span></span> 
    
  
3. <span data-ttu-id="d8e68-208">Erweitern Sie im Dialogfenster **Neues Projekt** unter **Installiert** **Vorlagen**, erweitern Sie **Visual C#**, und wählen Sie dann **Windows**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-208">In the **New Project** dialog box, under **Installed**, expand **Templates**, expand **Visual C#**, and then chose **Windows**.</span></span>
    
  
4. <span data-ttu-id="d8e68-209">Wählen Sie in der Liste der Projektvorlagen **Konsolenanwendung**</span><span class="sxs-lookup"><span data-stu-id="d8e68-209">In the list of project templates, choose **Console Application**.</span></span>
    
  
5. <span data-ttu-id="d8e68-210">Vergewissern Sie sich, dass das Visual Studio-Projekt auf .NET Framework 4 verweist.</span><span class="sxs-lookup"><span data-stu-id="d8e68-210">Be sure that the project in Visual Studio targets .NET Framework 4.</span></span>
    
    > <span data-ttu-id="d8e68-211">**Hinweis:** Beim Einsatz früherer SharePoint Server-Versionen musste auf .NET Framework 3.5 verwiesen werden.</span><span class="sxs-lookup"><span data-stu-id="d8e68-211">**Note:** Previous versions of SharePoint Server required that you target .NET Framework 3.5.</span></span> <span data-ttu-id="d8e68-212">Jetzt verweisen die Microsoft.SharePoint-Bibliotheken auf Assemblys in .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="d8e68-212">The Microsoft.SharePoint libraries now reference assemblies in .NET Framework 4.</span></span> <span data-ttu-id="d8e68-213">Stellen Sie außerdem sicher, dass das Projekt auf die Vollversion von .NET Framework 4 verweist, nicht auf das .NET Framework 4 Client Profile.</span><span class="sxs-lookup"><span data-stu-id="d8e68-213">Note Previous versions of SharePoint Server required that you target .NET Framework 3.5. The Microsoft.SharePoint libraries now reference assemblies in .NET Framework 4. Also make sure that your project targets the full .NET Framework 4 and not the .NET Framework 4 Client Profile.</span></span> 
6. <span data-ttu-id="d8e68-214">Geben Sie in das Feld **Name** den gewünschten Namen für das Projekt ein, zum Beispiel „PAS_Sample“.</span><span class="sxs-lookup"><span data-stu-id="d8e68-214">In the **Name** box, type the name that you want to use for your project, such as PAS_Sample.</span></span>
    
  
7. <span data-ttu-id="d8e68-215">Geben Sie im Feld **Speicherort** den Speicherort ein, an dem das Projekt abgelegt werden soll.</span><span class="sxs-lookup"><span data-stu-id="d8e68-215">In the **Location** box, type the location where you want to place the project.</span></span>
    
  
8. <span data-ttu-id="d8e68-216">Klicken Sie zum Erstellen der Projektmappe auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-216">Click **OK** to create the solution.</span></span>
    
  
9. <span data-ttu-id="d8e68-217">Standardmäßig erstellt Visual Studio 2012 Projekte, die auf x86-CPUs abzielen, zum Erstellen von SharePoint Server-Anwendungen muss jedoch auf alle CPUs abgezielt werden.</span><span class="sxs-lookup"><span data-stu-id="d8e68-217">By default, Visual Studio 2012 creates projects that target x86 CPUs, but to build SharePoint Server applications, you must target any CPU.</span></span>
    
    <span data-ttu-id="d8e68-218">Klicken Sie beim Erstellen einer Microsoft Visual C#-Anwendung im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und klicken Sie dann auf **Eigenschaften**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-218">If you are building a Microsoft Visual C# application, in **Solution Explorer**, right-click the project, and then click **Properties**.</span></span>
    
  - <span data-ttu-id="d8e68-219">Klicken Sie im Projektfenster **Eigenschaften** auf **Build**</span><span class="sxs-lookup"><span data-stu-id="d8e68-219">In the project **Properties** window, click **Build**.</span></span>
    
  
  - <span data-ttu-id="d8e68-220">Zeigen Sie auf die Liste **Konfiguration**, und wählen Sie **Alle Konfigurationen**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-220">Point to the **Configuration** list, and select **All Configurations**.</span></span>
    
  
  - <span data-ttu-id="d8e68-221">Zeigen Sie auf die Liste **Zielplattform**, und wählen Sie **Alle CPUs**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-221">Point to the **Platform Target** list, and select **Any CPU**.</span></span>
    
  

    
    
    <span data-ttu-id="d8e68-222">Klicken Sie beim Erstellen einer Microsoft Visual Basic .NET Framework-Anwendung im Fenster **Eigenschaften** auf **Kompilieren**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-222">If you are building a Microsoft Visual Basic .NET Framework application, in the **Properties** window, click **Compile**.</span></span>
    
  - <span data-ttu-id="d8e68-223">Klicken Sie auf **Erweiterte Kompilierungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-223">Click **Advanced Compile Options**.</span></span>
    
  
  - <span data-ttu-id="d8e68-224">Zeigen Sie auf die Liste **Konfiguration**, und wählen Sie **Alle Konfigurationen**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-224">Point to the **Configuration** list, and then select **All Configurations**.</span></span>
    
  
  - <span data-ttu-id="d8e68-225">Zeigen Sie auf die Liste **Zielplattform**, und klicken Sie dann auf **Alle CPUs**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-225">Point to the **Platform Target** list, and then click **Any CPU**.</span></span>
    
  

    
    
  
10. <span data-ttu-id="d8e68-226">Klicken Sie im Menü **Projekt** auf **Verweis hinzufügen**, um das Dialogfeld **Verweis hinzufügen** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="d8e68-226">On the **Project** menu, click **Add Reference** to open the **Add Reference** dialog box.</span></span>
    
  
11. <span data-ttu-id="d8e68-227">Erweitern Sie **Assemblys**, und führen Sie die folgenden Aktionen durch:</span><span class="sxs-lookup"><span data-stu-id="d8e68-227">Expand **Assemblies**, and then do the following:</span></span>
    
  - <span data-ttu-id="d8e68-228">Erweitern Sie **Framework**, und fügen Sie dann einen Verweis auf System.Web hinzu.</span><span class="sxs-lookup"><span data-stu-id="d8e68-228">Expand **Framework**, and then add a reference to System.Web.</span></span>
    
  
  - <span data-ttu-id="d8e68-229">Erweitern Sie **Erweiterungen**, und fügen Sie dann einen Verweis auf Microsoft.SharePoint hinzu.</span><span class="sxs-lookup"><span data-stu-id="d8e68-229">Expand **Extensions**, and then add a reference to Microsoft.SharePoint.</span></span>
    
  
12. <span data-ttu-id="d8e68-230">Wählen Sie im Dialogfenster **Verweis hinzufügen** **Durchsuchen**, navigieren Sie zum Speicherort für die Datei „Microsoft.Office.Server.PowerPoint.dl" (standardmäßig ist dies C:\\Windows\\Microsoft.NET\\assembly\\GAC_MSIL\\Microsoft.Office.Server.PowerPoint\\v4.0_15.0.0.0__71e9bce111e9429c), wählen Sie die Assembly aus, und wählen Sie dann **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="d8e68-230">Also in the **Add Reference** dialog box, choose **Browse**, navigate to the location for the Microsoft.Office.Server.PowerPoint.dll (default location is C:\\Windows\\Microsoft.NET\\assembly\\GAC_MSIL\\Microsoft.Office.Server.PowerPoint\\v4.0_15.0.0.0__71e9bce111e9429c), select the assembly, and then choose **Add**.</span></span> 
    
  
<span data-ttu-id="d8e68-231">Die folgenden C#- und Visual Basic-Beispiele zeigen eine einfache PowerPoint Automation Services-Anwendung, die eine PowerPoint 97-2003-Datei (.ppt) im Ordner „Freigegebene Dokumente" einer SharePoint-Website in eine PowerPoint Open XML-Datei (.pptx) im gleichen Ordner konvertiert.</span><span class="sxs-lookup"><span data-stu-id="d8e68-231">The following C# and Visual Basic examples show a simple PowerPoint Automation Services application that converts a PowerPoint 97-2003 file (.ppt) in the Shared Documents folder of a SharePoint site to a PowerPoint Open XML file (.pptx) in the same folder.</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Web;
using Microsoft.SharePoint;
using Microsoft.Office.Server.PowerPoint.Conversion;

namespace PAS_Sample
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                string siteURL = "http://localhost";
                using (SPSite site = new SPSite(siteURL))
                {
                    using (SPWeb web = site.OpenWeb())
                    {
                        Console.WriteLine("Begin conversion");

                        // Get a reference to the "Shared Documents" library 
                        // and the presentation file to be converted.
                        SPFolder docs = web.Folders[siteURL + 
                            "/Shared Documents"];
                        SPFile file = docs.Files[siteURL + 
                            "/Shared Documents/Pres1.ppt"];

                        // Convert the file to a stream and create an
                        // SPFileStream object for the conversion output.
                        Stream fStream = file.OpenBinaryStream();
                        SPFileStream stream = new SPFileStream(web, 0x1000);

                        // Create the presentation conversion request.
                        PresentationRequest request = new PresentationRequest(
                            fStream,
                            ".ppt",
                            stream);

                        // Send the request synchronously, passing
                        // in a 'null' value for the callback parameter, 
                        // and capturing the response in the result object.
                        IAsyncResult result = request.BeginConvert(
                            SPServiceContext.GetContext(site),
                            null,
                            null);

                        // Use the EndConvert method to get the result. 
                        request.EndConvert(result);

                        // Add the converted file to the document library.
                        SPFile newFile = docs.Files.Add(
                            "newPres1.pptx", 
                            stream, 
                            true);
                        Console.WriteLine("Output: {0}", newFile.Url);

                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error: " + ex.Message);
            }
            finally
            {
                Console.WriteLine("Complete");
                Console.ReadKey();
            }
        }
    }
}
```




```VB.net

Imports System
Imports System.Collections.Generic
Imports System.IO
Imports System.Linq
Imports System.Text
Imports System.Web
Imports Microsoft.SharePoint
Imports Microsoft.Office.Server.PowerPoint.Conversion

Namespace PAS_Sample
    Class Program
        Private Shared Sub Main(args As String())
            Try
                Dim siteURL As String = "http://localhost"
                Using site As New SPSite(siteURL)
                    Using web As SPWeb = site.OpenWeb()
                        Console.WriteLine("Begin conversion")

                        ' Get a reference to the "Shared Documents" library 
                        ' and the presentation file to be converted.
                        Dim docs As SPFolder = web.Folders(siteURL + _
                            "/Shared Documents")
                        Dim file As SPFile = docs.Files(siteURL + _
                            "/Shared Documents/Pres1.ppt")

                        ' Convert the file to a stream and create an
                        ' SPFileStream object for the conversion output.
                        Dim fStream As Stream = file.OpenBinaryStream()
                        Dim stream As New SPFileStream(web, &amp;H1000)

                        ' Create the presentation conversion request.
                        Dim request As New PresentationRequest(fStream, _
                            ".ppt", 
                            stream)

                        ' Send the request synchronously, passing
                        ' in a Nothing value for the callback parameter, 
                        ' and capturing the response in the result object.
                        Dim result As IAsyncResult = request.BeginConvert(_
                            SPServiceContext.GetContext(site), _
                            Nothing, _
                            Nothing)

                        ' Use the EndConvert method to get the result. 
                        request.EndConvert(result)

                        ' Add the converted file to the document library.
                        Dim newFile As SPFile = docs.Files.Add(_
                            "newPres1.pptx", _
                            stream, _
                            True)

                        Console.WriteLine("Output: {0}", newFile.Url)
                    End Using
                End Using
            Catch ex As Exception
                Console.WriteLine("Error: " + ex.Message)
            Finally
                Console.WriteLine("Complete")
                Console.ReadKey()
            End Try
        End Sub
    End Class
End Namespace

```


### <a name="to-build-and-run-the-example"></a><span data-ttu-id="d8e68-232">So erstellen Sie das Beispiel und führen es aus</span><span class="sxs-lookup"><span data-stu-id="d8e68-232">To build and run the example</span></span>


1. <span data-ttu-id="d8e68-233">Fügen Sie ein PowerPoint-Dokument mit dem Namen Pres1.ppt zum Ordner „Freigegebene Dokumente" auf der SharePoint-Website hinzu.</span><span class="sxs-lookup"><span data-stu-id="d8e68-233">Add a PowerPoint document named Pres1.ppt to the Shared Documents folder in the SharePoint site.</span></span>
    
  
2. <span data-ttu-id="d8e68-234">Erstellen Sie das Beispiel, und führen Sie es aus.</span><span class="sxs-lookup"><span data-stu-id="d8e68-234">Build and run the example.</span></span>
    
  
3. <span data-ttu-id="d8e68-p122">Warten Sie eine Minute ab, bis der Konvertierungsprozess ausgeführt wird, navigieren Sie zum Ordner „Freigegebene Dokumente" auf einer SharePoint-Website, und aktualisieren Sie die Seite. Die Dokumentbibliothek enthält nun ein neues PowerPoint-Dokument, Pres1.pptx.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p122">After waiting one minute for the conversion process to run, navigate to the Shared Documents folder in the SharePoint site, and refresh the page. The document library now contains a new PowerPoint document, Pres1.pptx.</span></span>
    
  
<span data-ttu-id="d8e68-237">Das SharePoint-Feature PowerPoint Automation Services gibt Unternehmen erweiterte Funktionen für die Verwaltung von Präsentationsdateien an die Hand.</span><span class="sxs-lookup"><span data-stu-id="d8e68-237">PowerPoint Automation Services on SharePoint Server 2013 provides businesses with advanced capabilities for managing their presentation files. This high-performance solution allows scalable, server-side presentation manipulation and generation, as a batch or on-demand.</span></span> <span data-ttu-id="d8e68-238">Die hochleistungsfähige Lösung ermöglicht eine skalierbare, serverseitige Verarbeitung oder Generierung von Präsentationsdateien, entweder batchbasiert oder bedarfsbasiert.</span><span class="sxs-lookup"><span data-stu-id="d8e68-238">ppsrvc15short on sps15short provides businesses with advanced capabilities for managing their presentation files. This high-performance solution allows scalable, server-side presentation manipulation and generation, as a batch or on-demand.</span></span> 
  
    
    

> <span data-ttu-id="d8e68-239">**Hinweis:** Stellen Sie vor der Ausführung des Beispielcodes sicher, dass PowerPoint Automation Services in der Konsole der SharePoint-Zentraladministration aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="d8e68-239">**Note** Before you run the example, make sure that PowerPoint Automation Services has been enabled in the SharePoint Central Administration console.</span></span><br/>  <span data-ttu-id="d8e68-240">Sie können wie folgt überprüfen, ob PowerPoint Automation Services aktiviert ist:</span><span class="sxs-lookup"><span data-stu-id="d8e68-240">To verify that PowerPoint Automation Services is enabled, do the following:</span></span> <ul><li><span data-ttu-id="d8e68-p124">Wählen Sie in der Zentraladministrationskonsole unter **Systemeinstellungen** **Dienste auf dem Server verwalten**, und vergewissern Sie sich dann, dass der **PowerPoint-Konvertierungsdienst** auf **Gestartet** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p124">In the Central Administration console, under **System Settings**, choose **Manage services on server**, and then make sure that the **PowerPoint Conversion Service** is set to **Started**. </span></span></li><li><span data-ttu-id="d8e68-242">Wählen Sie in der Zentraladministrationskonsole unter **Anwendungsverwaltung** **Dienstanwendungen verwalten**, und vergewissern Sie sich dann, dass die **PowerPoint-Konvertierungsdienstanwendung** und der **Proxy der PowerPoint-Konvertierungsdienstanwendung** auf „Gestartet" festgelegt sind.</span><span class="sxs-lookup"><span data-stu-id="d8e68-242">Also in the Central Administration console, under **Application Management**, choose **Manage service applications**, and then make sure that the **PowerPoint Conversion Service Application** and **PowerPoint Conversion Service Application Proxy** are set to Started.</span></span></li></ul>
  
    
    


## <a name="conclusion"></a><span data-ttu-id="d8e68-243">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="d8e68-243">Conclusion</span></span>
<span data-ttu-id="d8e68-244"><a name="PAS_Conclusion"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-244"></span></span>

<span data-ttu-id="d8e68-245">Das SharePoint-Feature PowerPoint Automation Services gibt Unternehmen erweiterte Funktionen für die Verwaltung von Präsentationsdateien an die Hand.</span><span class="sxs-lookup"><span data-stu-id="d8e68-245">PowerPoint Automation Services on SharePoint Server 2013 provides businesses with advanced capabilities for managing their presentation files. This high-performance solution allows scalable, server-side presentation manipulation and generation, as a batch or on-demand.</span></span> <span data-ttu-id="d8e68-246">Die hochleistungsfähige Lösung ermöglicht eine skalierbare, serverseitige Verarbeitung oder Generierung von Präsentationsdateien, entweder batchbasiert oder bedarfsbasiert.</span><span class="sxs-lookup"><span data-stu-id="d8e68-246">ppsrvc15short on sps15short provides businesses with advanced capabilities for managing their presentation files. This high-performance solution allows scalable, server-side presentation manipulation and generation, as a batch or on-demand.</span></span> 
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="d8e68-247">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d8e68-247">Additional Resources</span></span>
<span data-ttu-id="d8e68-248"><a name="PAS_Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-248"></span></span>


-  [<span data-ttu-id="d8e68-249">Entwickeln mit SharePoint 2010 Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="d8e68-249">Developing with SharePoint 2010 Word Automation Services</span></span>](http://msdn.microsoft.com/de-DE/library/ff742315.aspx)
    
  
-  [<span data-ttu-id="d8e68-250">PowerPoint Developer Center</span><span class="sxs-lookup"><span data-stu-id="d8e68-250">PowerPoint Developer Center</span></span>](http://msdn.microsoft.com/de-DE/office/aa905465)
    
  
-  [<span data-ttu-id="d8e68-251">SharePoint Developer Center</span><span class="sxs-lookup"><span data-stu-id="d8e68-251">SharePoint Developer Center</span></span>](http://msdn.microsoft.com/de-DE/sharepoint/default.aspx)
    
  

