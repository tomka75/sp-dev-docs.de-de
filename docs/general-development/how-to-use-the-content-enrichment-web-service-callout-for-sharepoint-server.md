---
title: "Vorgehensweise verwenden die Anreicherung Web Service als Legende für SharePoint Server"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d4e44498-9a3d-4f2f-b5ba-6ebef9971dcb
ms.openlocfilehash: cd0c56acb2b806bcaf2718f0702729d005711f78
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server"></a><span data-ttu-id="d3915-102">Anleitung: Aufrufen des Inhaltserweiterungs-Webdiensts in SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="d3915-102">How to: Use the Content Enrichment web service callout for SharePoint Server</span></span>
<span data-ttu-id="d3915-103">In diesem Artikel erfahren Sie, wie Sie den Inhaltserweiterungs-Webdienst in SharePoint implementieren, um verwaltete Eigenschaften von durchforsteten Elementen zu ändern, noch bevor die Elemente indiziert werden.</span><span class="sxs-lookup"><span data-stu-id="d3915-103">Learn how to implement the Content Enrichment web service in SharePoint Server 2013 to modify the managed properties of crawled items before they are indexed.</span></span>
<span data-ttu-id="d3915-104">Entwickler können die Inhaltsverarbeitung in der SharePoint-Suche um einen benutzerdefinierten Schritt ergänzen, in dem die verwalteten Eigenschaften von durchforsteten Elementen noch vor der Indizierung der Elemente verändert werden.</span><span class="sxs-lookup"><span data-stu-id="d3915-104">Search in SharePoint enables developers to add a custom step to content processing to modify the managed properties of crawled items before they are indexed.</span></span> <span data-ttu-id="d3915-105">Für diesen benutzerdefinierten Schritt muss ein externer Webdienst implementiert werden, der die verwalteten Eigenschaften von Elementen noch während der Elementverarbeitung erweitern kann: der Inhaltserweiterungs-Webdienst. Anschließend muss das System so konfiguriert werden, dass dieser externe Webdienst aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="d3915-105">This custom step requires the implementation of an external web service--the Content Enrichment web service--that can enrich managed properties of items being processed; and then configuring the system to call this external web service.</span></span>
  
    
    

<span data-ttu-id="d3915-106">Zur Implementierung des externen Inhaltserweiterungs-Webdiensts werden die Schnittstellen im Namespace [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) verwendet.</span><span class="sxs-lookup"><span data-stu-id="d3915-106">Implementation of the external content enrichment web service relies on interfaces under the  [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) namespace.</span></span>
## <a name="windows-powershell-cmdlets-to-use-with-the-content-enrichment-web-service"></a><span data-ttu-id="d3915-107">Windows PowerShell-Cmdlets zur Verwendung mit dem Inhaltserweiterung-Webdienst</span><span class="sxs-lookup"><span data-stu-id="d3915-107">Windows PowerShell Cmdlets to use with the Content Enrichment web service</span></span>
<span data-ttu-id="d3915-108"><a name="SP15_PowerShell_Cmdlets_Content_Enrichment"> </a></span><span class="sxs-lookup"><span data-stu-id="d3915-108"></span></span>

<span data-ttu-id="d3915-109">Die Funktionalität Inhaltserweiterung, konfiguriert und mit den folgenden Cmdlets Windows PowerShell aktiviert:</span><span class="sxs-lookup"><span data-stu-id="d3915-109">The Content Enrichment functionality is configured and enabled with the following Windows PowerShell cmdlets:</span></span>
  
    
    

-  [<span data-ttu-id="d3915-110">Get-SPEnterpriseSearchContentEnrichmentConfiguration</span><span class="sxs-lookup"><span data-stu-id="d3915-110">Get-SPEnterpriseSearchContentEnrichmentConfiguration</span></span>](http://technet.microsoft.com/de-DE/library/jj219783%28office.15%29.aspx)
    
  
-  [<span data-ttu-id="d3915-111">Set-SPEnterpriseSearchContentEnrichmentConfiguration</span><span class="sxs-lookup"><span data-stu-id="d3915-111">Set-SPEnterpriseSearchContentEnrichmentConfiguration</span></span>](http://technet.microsoft.com/de-DE/library/jj219659%28office.15%29.aspx)
    
  
-  [<span data-ttu-id="d3915-112">Remove-SPEnterpriseSearchContentEnrichmentConfiguration</span><span class="sxs-lookup"><span data-stu-id="d3915-112">Remove-SPEnterpriseSearchContentEnrichmentConfiguration</span></span>](http://technet.microsoft.com/de-DE/library/jj219742%28office.15%29.aspx)
    
  
-  [<span data-ttu-id="d3915-113">New-SPEnterpriseSearchContentEnrichmentConfiguration</span><span class="sxs-lookup"><span data-stu-id="d3915-113">New-SPEnterpriseSearchContentEnrichmentConfiguration</span></span>](http://technet.microsoft.com/de-DE/library/jj219502%28office.15%29.aspx)
    
  
<span data-ttu-id="d3915-114">Diese Windows PowerShell-Cmdlets können Administratoren Folgendes konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="d3915-114">These Windows PowerShell cmdlets enable an administrator to configure the following:</span></span>
  
    
    

- <span data-ttu-id="d3915-115">Eine benutzerdefinierte Gruppe von verwalteten Eigenschaften mit dem externen Webdienst gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="d3915-115">A custom set of managed properties to be sent to the external web service.</span></span>
    
  
- <span data-ttu-id="d3915-116">Eine benutzerdefinierte Gruppe von verwalteten Eigenschaften, die vom externen Webdienst zurückgegeben werden soll.</span><span class="sxs-lookup"><span data-stu-id="d3915-116">A custom set of managed properties to be returned by the external web service.</span></span>
    
  
- <span data-ttu-id="d3915-p102">Eine Bedingung Trigger darstellt, die ein Prädikat für jedes Element verarbeiteten ausführen. Wenn eine Bedingung für den Auslöser verwendet wird, wird der externen Webdienst aufgerufen, nur, wenn der Trigger **true**ausgewertet wird. Wenn die Bedingung keine Trigger verwendet wird, werden alle Elemente auf den externen Webdienst gesendet.</span><span class="sxs-lookup"><span data-stu-id="d3915-p102">A trigger condition, that represents a predicate to execute for every item being processed. If a trigger condition is used, the external web service is called only when the trigger evaluates to **true**. If no trigger condition is used, all items are sent to the external web service.</span></span>
    
  
- <span data-ttu-id="d3915-p103">Ein **FailureMode**, mit dem den Webdienst entweder können fehlschlagen Elemente, die können nicht verarbeitet werden, während der inhaltserweiterung Schritt oder übergeben Sie diese Elemente über ohne Änderung. Wenn die Elemente durchgeführt wurde, werden nicht indiziert und eine Warnung ausgegeben wird in den ULS-Protokolldateien geschrieben.</span><span class="sxs-lookup"><span data-stu-id="d3915-p103">A **FailureMode** that enables the web service to either fail items that cannot be processed during the content enrichment step or pass these items through without any modification. If the items are failed, they are not indexed and a warning is written to the ULS log.</span></span>
    
  
- <span data-ttu-id="d3915-p104">Ein **DebugMode**, der eine schnelle Prototypen des externen Webdiensts ermöglicht. Bei Aktivierung erhält der externen Webdienst aller verfügbare verwaltete Eigenschaften. In **DebugMode**die Trigger-Bedingung wird ignoriert, und keine verwalteten Eigenschaften Ausgaben vom Webdienst werden ebenfalls ignoriert.</span><span class="sxs-lookup"><span data-stu-id="d3915-p104">A **DebugMode**, that enables rapid prototyping of the external web service. When enabled, the external web service receives all available managed properties. In **DebugMode**, the trigger condition is ignored and any managed properties output by the web service are also ignored.</span></span>
    
  
- <span data-ttu-id="d3915-p105">Ein Schalter, **SendRawData**, die die Rohdaten eines Elements im Binärformat sendet. Dies ist nützlich, wenn mehr Metadaten erforderlich ist, als was aus der analysierten Version des Elements abgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="d3915-p105">A **SendRawData** switch that sends the raw data of an item in binary form. This is useful when more metadata is required than what can be retrieved from the parsed version of the item.</span></span>
    
  
<span data-ttu-id="d3915-p106">Darüber hinaus stehen die Optionen zur Angabe der größenbeschränkungen für Nachrichten und Timeouts. Finden Sie unter  [Benutzerdefinierte Inhaltsverarbeitung mit dem Webdienstpopup zur Inhaltsanreicherung](custom-content-processing-with-the-content-enrichment-web-service-callout.md) für eine vollständige Liste der konfigurierbaren Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="d3915-p106">In addition, there are options for specifying size limits and timeouts. See  [Custom content processing with the Content Enrichment web service callout](custom-content-processing-with-the-content-enrichment-web-service-callout.md) for a full list of configurable properties.</span></span>
  
    
    

## <a name="prerequisites-for-using-the-content-enrichment-web-service-callout-for-sharepoint"></a><span data-ttu-id="d3915-129">Voraussetzungen für das Aufrufen des Inhaltserweiterungs-Webdiensts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3915-129">Prerequisites for using the Content Enrichment web service callout for SharePoint Server 2013</span></span>
<span data-ttu-id="d3915-130"><a name="SP15ContentEnrich_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="d3915-130"></span></span>

<span data-ttu-id="d3915-131">Um diese Vorgehensweise ausführen zu können, müssen Sie Folgendes in Ihrer Entwicklungsumgebung installiert sein:</span><span class="sxs-lookup"><span data-stu-id="d3915-131">To complete this how-to, you must have the following installed in your development environment:</span></span>
  
    
    

- <span data-ttu-id="d3915-132">Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3915-132">Search in SharePoint</span></span>
    
  
- <span data-ttu-id="d3915-133">Visual Studio 2010 oder ein vergleichbares Entwicklungstool, das mit .NET Framework kompatibel ist</span><span class="sxs-lookup"><span data-stu-id="d3915-133">Visual Studio 2010 or similar .NET Framework-compatible development tool</span></span>
    
  
- <span data-ttu-id="d3915-134">Administratorrechte in der SharePoint-Installation</span><span class="sxs-lookup"><span data-stu-id="d3915-134">Administrator privileges on your SharePoint Server 2013 installation</span></span>
    
  
- <span data-ttu-id="d3915-135">Ein Server, auf dem der Dienst mit IIS gehostet werden kann</span><span class="sxs-lookup"><span data-stu-id="d3915-135">A server on which you can host the service with IIS</span></span>
    
  
<span data-ttu-id="d3915-136">Sie müssen außerdem wissen, wie zum Erstellen einer Website in IIS, und stellen Sie einen Dienst hinzu</span><span class="sxs-lookup"><span data-stu-id="d3915-136">You must also know how to create a site in IIS and deploy a service to it</span></span>
  
    
    

## <a name="set-up-a-content-enrichment-service-project"></a><span data-ttu-id="d3915-137">Einrichten eines inhaltserweiterung Service-Projekts</span><span class="sxs-lookup"><span data-stu-id="d3915-137">Set up a content enrichment service project</span></span>
<span data-ttu-id="d3915-138"><a name="SP15ContentEnrich_setup"> </a></span><span class="sxs-lookup"><span data-stu-id="d3915-138"></span></span>

<span data-ttu-id="d3915-139">In diesem Schritt werden Sie das Dienstprojekt Implementierung erstellen und fügen Sie die erforderlichen Verweise auf das Projekt.</span><span class="sxs-lookup"><span data-stu-id="d3915-139">In this step, you will create the service implementation project and then add the required references to the project.</span></span>
  
    
    

### <a name="to-create-the-project-for-a-content-enrichment-service"></a><span data-ttu-id="d3915-140">So erstellen Sie das Projekt für einen Dienst inhaltserweiterung</span><span class="sxs-lookup"><span data-stu-id="d3915-140">To create the project for a content enrichment service</span></span>


1. <span data-ttu-id="d3915-141">Wählen Sie in Visual Studio auf der Menüleiste **Datei**, **neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="d3915-141">In Visual Studio, on the menu bar choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="d3915-142">Wählen Sie in **Projekttypen** unter Visual C#- **WCF**.</span><span class="sxs-lookup"><span data-stu-id="d3915-142">In **Project types**, under Visual C#, choose **WCF**.</span></span>
    
  
3. <span data-ttu-id="d3915-p107">Wählen Sie unter **Vorlagen** **WCF Service-Anwendung**. Klicken Sie im Feld **Name** Geben Sie **ContentProcessingEnrichmentService**, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3915-p107">Under **Templates**, choose **WCF Service Application**. In the **Name** field, type **ContentProcessingEnrichmentService**, and then choose the **OK** button.</span></span>
    
  
4. <span data-ttu-id="d3915-145">Löschen Sie die automatisch generierte **Service1** -Klasse und **Service1** -Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="d3915-145">Delete the automatically generated **Service1** class and **Service1** interface.</span></span>
    
  

### <a name="to-add-references-to-the-content-enrichment-service-project"></a><span data-ttu-id="d3915-146">So fügen Sie Verweise auf das Projekt inhaltserweiterung-Dienst hinzu</span><span class="sxs-lookup"><span data-stu-id="d3915-146">To add references to the content enrichment service project</span></span>


1. <span data-ttu-id="d3915-147">Wählen Sie im Menü **Projekt** **Verweis hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="d3915-147">On the **Project** menu, choose **Add Reference**.</span></span>
    
  
2. <span data-ttu-id="d3915-148">Wählen Sie **Durchsuchen** aus, und suchen Sie die **Microsoft.Office.Server.Search.ContentProcessingEnrichment** -Assembly im Installationsordner von SharePoint unter _Installation Path_\\Microsoft Office Servers\\15.0\\Search\\Applications\\External.</span><span class="sxs-lookup"><span data-stu-id="d3915-148">Choose **Browse** and locate the **Microsoft.Office.Server.Search.ContentProcessingEnrichment** assembly in your SharePoint installation folder under _Installation Path_\\Microsoft Office Servers\\15.0\\Search\\Applications\\External.</span></span> 
    
    > <span data-ttu-id="d3915-149">**Hinweis:** Falls SharePoint auf einem anderen Computer als dem Entwicklungscomputer installiert ist, müssen Sie die Assembly auf den Entwicklungscomputer kopieren und von dort referenzieren.</span><span class="sxs-lookup"><span data-stu-id="d3915-149">**Note** If SharePoint is installed on a machine other than your development machine, copy the assembly over to your development machine and reference it from there.</span></span> 

## <a name="create-a-content-enrichment-service"></a><span data-ttu-id="d3915-150">Erstellen eines Inhaltserweiterungsdiensts</span><span class="sxs-lookup"><span data-stu-id="d3915-150">Create a content enrichment service</span></span>
<span data-ttu-id="d3915-151"><a name="SP15ContentEnrich_createservice"> </a></span><span class="sxs-lookup"><span data-stu-id="d3915-151"></span></span>

<span data-ttu-id="d3915-p108">Ihre Inhalte Verarbeitung Anreicherung Dienst muss die **IContentProcessingEnrichmentService** -Schnittstelle aus dem [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) -Namespace implementieren. Das Codebeispiel in diesem Abschnitt wird eine einfache Implementierung dieser Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="d3915-p108">Your content processing enrichment service must implement the **IContentProcessingEnrichmentService** interface from the [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) namespace. The code example in this section is a basic implementation of this interface.</span></span>
  
    
    
<span data-ttu-id="d3915-p109">Die Implementierung erfordert zwei verwaltete Eigenschaften für jedes Element, das über den externen Webdienst empfangen: **Author** und **Filename**. Die **Author** ist eine Liste von **String** -Objekten und der **Filename** ist ein **String** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="d3915-p109">The implementation requires two managed properties for each item received via the external web service: **Author** and **Filename**. The **Author** is a list of **String** objects and the **Filename** is a **String** object.</span></span>
  
    
    
<span data-ttu-id="d3915-p110">Die Implementierung **IContentProcessingEnrichmentService** schreibt die binären Daten an einen temporären Speicherort auf einem Datenträger mit **Filename** als den Namen der Datei. Klicken Sie dann ein neuer Namen in die Liste der Autoren hinzugefügt und an die inhaltsverarbeitungskomponente zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="d3915-p110">The **IContentProcessingEnrichmentService** implementation writes the raw binary data to a temporary location on disk, with **Filename** as the name of the file. Then, a new name is added to the list of authors and returned to the content processing component.</span></span>
  
    
    

### <a name="to-create-the-class-file-for-the-content-enrichment-service"></a><span data-ttu-id="d3915-158">Erstellen Sie die Klassendatei für den Dienst inhaltserweiterung</span><span class="sxs-lookup"><span data-stu-id="d3915-158">To create the class file for the content enrichment service</span></span>


1. <span data-ttu-id="d3915-159">Wählen Sie im Menü **PROJEKT** die Option **Neues Element hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="d3915-159">On the **Project** menu, choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="d3915-160">Klicken Sie unter **Visual C#-** unter **Installierte Vorlagen** wählen Sie **Web**, und wählen Sie dann auf **WCF-Dienst**.</span><span class="sxs-lookup"><span data-stu-id="d3915-160">Under **Visual C#** in **Installed Templates**, choose **Web**, and then choose **WCF Service**.</span></span>
    
  
3. <span data-ttu-id="d3915-161">Geben Sie **ContentProcessingEnrichmentService.svc**, und wählen Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="d3915-161">Type **ContentProcessingEnrichmentService.svc**, and then choose **Add**.</span></span>
    
  
4. <span data-ttu-id="d3915-162">Löschen Sie die **IContentProcessingEnrichmentService.cs**-Schnittstelle, die erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="d3915-162">Delete the **IContentProcessingEnrichmentService.cs** interface that is created.</span></span>
    
  

### <a name="to-modify-the-default-code-in-the-contentprocessingenrichmentservice-class"></a><span data-ttu-id="d3915-163">So ändern Sie den Standardcode in der ContentProcessingEnrichmentService-Klasse</span><span class="sxs-lookup"><span data-stu-id="d3915-163">To modify the default code in the ContentProcessingEnrichmentService class</span></span>


1. <span data-ttu-id="d3915-164">Ersetzen Sie die vorhandenen Direktiven **using** durch die folgenden **using** Direktiven am Anfang der Klasse.</span><span class="sxs-lookup"><span data-stu-id="d3915-164">Replace the existing **using** directives with the following **using** directives at the beginning of the class.</span></span>
    
```cs
  
using System;
using System.Collections.Generic;
using System.IO;
using Microsoft.Office.Server.Search.ContentProcessingEnrichment;
using Microsoft.Office.Server.Search.ContentProcessingEnrichment.PropertyTypes;

```

2. <span data-ttu-id="d3915-165">Löschen Sie die **DoWork** -Methode.</span><span class="sxs-lookup"><span data-stu-id="d3915-165">Delete the **DoWork** method.</span></span>
    
  

### <a name="to-implement-the-icontentprocessingenrichmentservice-interface-method"></a><span data-ttu-id="d3915-166">Implementieren die IContentProcessingEnrichmentService Schnittstelle-Methode</span><span class="sxs-lookup"><span data-stu-id="d3915-166">To implement the IContentProcessingEnrichmentService interface method</span></span>


1. <span data-ttu-id="d3915-167">Fügen Sie den folgenden Code innerhalb der Klasse, um die erforderlichen Konstanten und Elemente des Objekts definiert.</span><span class="sxs-lookup"><span data-stu-id="d3915-167">Add the following code inside the class to define the required constants and members.</span></span>
    
```cs
  
// Defines the name of the managed property 'Filename'.
private const string FileNameProperty = "Filename";

// Defines the name of the managed property 'Author'
private const string AuthorProperty = "Author";

// Defines the temporary directory where binary data will be stored.
private const string TempDirectory = @"C:\\Temp";

// Defines the error code for managed properties with an unexpected type.
private const int UnexpectedType = 1;

// Defines the error code for encountering unexpected exceptions.
private const int UnexpectedError = 2;

private readonly ProcessedItem processedItemHolder = new ProcessedItem
{ 
   ItemProperties = new List<AbstractProperty>()
};
```

2. <span data-ttu-id="d3915-168">Fügen Sie den folgenden Code für die **ProcessItem** -Methode.</span><span class="sxs-lookup"><span data-stu-id="d3915-168">Add the following code for the **ProcessItem** method.</span></span>
    
```cs
  
public ProcessedItem ProcessItem(Item item)
{
   processedItemHolder.ErrorCode = 0;
   processedItemHolder.ItemProperties.Clear();
   try
   {
      // Iterate over each property received and locate the two properties we
      // configured the system to send.
      foreach (var property in item.ItemProperties)
      {
         // Check if this is the author property.
         if (property.Name.Equals(AuthorProperty, StringComparison.Ordinal))
         {
            var author = property as Property<List<string>>;
            if (author == null)
            {
               // The author property was not of the expected type.
               // Update the error code and return. 
                  processedItemHolder.ErrorCode = UnexpectedType;
                  return processedItemHolder;
            }
               // Adding a new author to the list so it will become searchable.      
                  author.Value.Add("ExampleService");
                  processedItemHolder.ItemProperties.Add(author);
         }
         else if (property.Name.Equals(FileNameProperty, StringComparison.Ordinal))
         {
            var filename = property as Property<string>;
            if (filename == null)
            {
               // The file name property was not of the expected type.
               // Update error code and return.
                  processedItemHolder.ErrorCode = UnexpectedType;
                  return processedItemHolder;
            }
            if (!string.IsNullOrEmpty(filename.Value))
            {
               var fullFilePath = string.Join(char.ToString(Path.DirectorySeparatorChar), TempDirectory, filename.Value);
               if (item.RawData != null)
               {   
                  var outputFile = File.Create(fullFilePath);
                  using (var writer = new BinaryWriter(outputFile))
                  {
                     writer.Write(item.RawData);
                  }
               }
            }
         }
      }
   }
   catch (Exception)
   { 
      processedItemHolder.ErrorCode = UnexpectedError;
   } return processedItemHolder;
}
```

3. <span data-ttu-id="d3915-169">Ändern **web.config** akzeptieren von Nachrichten bis zu 8 MB, und konfigurieren Sie **readerQuotas**, um eine ausreichend große Zahl sein.</span><span class="sxs-lookup"><span data-stu-id="d3915-169">Modify **web.config** to accept messages up to 8 MB, and configure **readerQuotas** to be a sufficiently large value.</span></span>
    
  
4. <span data-ttu-id="d3915-170">Fügen Sie die folgenden innerhalb **<system.serviceModel>**.</span><span class="sxs-lookup"><span data-stu-id="d3915-170">Add the following inside **<system.serviceModel>**.</span></span>
    
```XML
  
<bindings>
   <basicHttpBinding>
   <!-- The service will accept a maximum blob of 8 MB. -->
      <binding maxReceivedMessageSize = "8388608">
         <readerQuotas maxDepth="32"
          maxStringContentLength="2147483647"
          maxArrayLength="2147483647"   
          maxBytesPerRead="2147483647"   
          maxNameTableCharCount="2147483647" />  
             <security mode="None" />
      </binding>
   </basicHttpBinding>
</bindings>
```

<span data-ttu-id="d3915-171">Erstellen Sie das Projekt, und stellen Sie es auf Ihrer IIS-Website bereit.</span><span class="sxs-lookup"><span data-stu-id="d3915-171">Build the project and deploy it to your IIS site.</span></span>
  
    
    

## <a name="configure-sharepoint"></a><span data-ttu-id="d3915-172">Konfigurieren von SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3915-172">Configure SharePoint Server 2013</span></span>
<span data-ttu-id="d3915-173"><a name="SP15ContentEnrich_configure"> </a></span><span class="sxs-lookup"><span data-stu-id="d3915-173"></span></span>

<span data-ttu-id="d3915-174">Öffnen Sie die SharePoint-Verwaltungsshell, und geben Sie die folgende Sequenz von Windows PowerShell-Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d3915-174">Open the SharePoint Management Shell, and enter the following sequence of Windows PowerShell cmdlets.</span></span>
  
    
    

```

$ssa = Get-SPEnterpriseSearchServiceApplication
$config = New-SPEnterpriseSearchContentEnrichmentConfiguration
$config.Endpoint = http://Site_URL/ContentEnrichmentService.svc
$config.InputProperties = "Author", "Filename"
$config.OutputProperties = "Author"
$config.SendRawData = $True
$config.MaxRawDataSize = 8192
Set-SPEnterpriseSearchContentEnrichmentConfiguration -SearchApplication
$ssa -ContentEnrichmentConfiguration $config
```

<span data-ttu-id="d3915-p111">Die Abfolge der Windows PowerShell-Cmdlets können Sie zunächst ein Konfigurationsobjekt erstellen, mit dem Cmdlet  [New-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219502%28office.15%29.aspx) . Configuration-Objekts wird anschließend in Richtung der Service-Implementierung verwiesen; als bewährte Methode verwenden Sie `http://localhost:808` für _Site_URL_.</span><span class="sxs-lookup"><span data-stu-id="d3915-p111">The sequence of Windows PowerShell cmdlets help you to first create a configuration object by using the  [New-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219502%28office.15%29.aspx) cmdlet. The configuration object is then pointed toward your service implementation; as a best practice, use `http://localhost:808` for _Site_URL_.</span></span>
  
    
    
<span data-ttu-id="d3915-p112">Die verwalteten Eigenschaften **Author** und **Filename** werden an den Dienst für jedes Element gesendet, die verarbeitet wird. Darüber hinaus haben Sie die Webdienstclients darüber informiert, dass der Dienst eine einzelne verwaltete Eigenschaft **Author**ausgegeben wird. In ist zusätzlich zu verwalteten Eigenschaften WebClient-Dienst konfiguriert die Rohdaten des Elements mit einer Einschränkung auf die Größe der Daten senden. Schließlich wird das Cmdlet  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219659%28office.15%29.aspx)verwendet, um die gesamte Konfiguration zu speichern. Nachdem dieses Cmdlet zurückgibt, wird die Konfiguration aktiv ist, und die Durchforstungskomponente verwendet diese Konfiguration für den nächsten Durchforstungsvorgang.</span><span class="sxs-lookup"><span data-stu-id="d3915-p112">The managed properties **Author** and **Filename** are sent to your service for every item that is being processed. In addition, you have informed the web service client that the service will output a single managed property, **Author**. In additional to managed properties, the web service client is configured to send the raw data of the item with a limitation on the size of the data. Finally, the  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219659%28office.15%29.aspx)cmdlet is used to store the entire configuration. After this cmdlet returns, the configuration is active and the crawl component uses this configuration for its next crawl process.</span></span>
  
    
    
<span data-ttu-id="d3915-p113">Nachdem dieser Schritt abgeschlossen ist, können Sie eine vollständige Durchforstung der Website beginnen. Wenn der Dienst ordnungsgemäß funktioniert, sollten Sie überwachen Sie den temporären Ordner auf dem Server mit der Website für die Dokumente geschrieben werden auf dem Datenträger.</span><span class="sxs-lookup"><span data-stu-id="d3915-p113">After this is finished, you can start a full crawl of your site. If the service is working correctly, you should be able to monitor the temporary folder on the server hosting your site for the documents written to disk.</span></span>
  
    
    
<span data-ttu-id="d3915-184">Sie können die Konfiguration später mit dem folgenden Cmdlet Windows PowerShell entfernen.</span><span class="sxs-lookup"><span data-stu-id="d3915-184">You can remove the configuration later by using the following Windows PowerShell cmdlet.</span></span>
  
    
    



```

Remove-SPEnterpriseSearchContentEnrichmentConfiguration -SearchApplication $ssa
```


## <a name="additional-resources"></a><span data-ttu-id="d3915-185">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d3915-185">Additional resources</span></span>
<span data-ttu-id="d3915-186"><a name="SP15ContentEnrich_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d3915-186"></span></span>


-  [<span data-ttu-id="d3915-187">Starten, anhalten, fortsetzen oder Beenden einer Durchforstung</span><span class="sxs-lookup"><span data-stu-id="d3915-187">Start, pause, resume, or stop a crawl</span></span>](http://technet.microsoft.com/de-DE/library/jj219814%28office.15%29.aspx)
    
  
-  [<span data-ttu-id="d3915-188">Konfigurieren der Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3915-188">Configure search in SharePoint</span></span>](configure-search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d3915-189">Benutzerdefinierte Inhaltsverarbeitung mit dem Webdienstpopup zur Inhaltsanreicherung</span><span class="sxs-lookup"><span data-stu-id="d3915-189">Custom content processing with the Content Enrichment web service callout</span></span>](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  

