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
# <a name="how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server"></a>Anleitung: Aufrufen des Inhaltserweiterungs-Webdiensts in SharePoint Server
In diesem Artikel erfahren Sie, wie Sie den Inhaltserweiterungs-Webdienst in SharePoint implementieren, um verwaltete Eigenschaften von durchforsteten Elementen zu ändern, noch bevor die Elemente indiziert werden.
Entwickler können die Inhaltsverarbeitung in der SharePoint-Suche um einen benutzerdefinierten Schritt ergänzen, in dem die verwalteten Eigenschaften von durchforsteten Elementen noch vor der Indizierung der Elemente verändert werden. Für diesen benutzerdefinierten Schritt muss ein externer Webdienst implementiert werden, der die verwalteten Eigenschaften von Elementen noch während der Elementverarbeitung erweitern kann: der Inhaltserweiterungs-Webdienst. Anschließend muss das System so konfiguriert werden, dass dieser externe Webdienst aufgerufen wird.
  
    
    

Zur Implementierung des externen Inhaltserweiterungs-Webdiensts werden die Schnittstellen im Namespace [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) verwendet.
## <a name="windows-powershell-cmdlets-to-use-with-the-content-enrichment-web-service"></a>Windows PowerShell-Cmdlets zur Verwendung mit dem Inhaltserweiterung-Webdienst
<a name="SP15_PowerShell_Cmdlets_Content_Enrichment"> </a>

Die Funktionalität Inhaltserweiterung, konfiguriert und mit den folgenden Cmdlets Windows PowerShell aktiviert:
  
    
    

-  [Get-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219783%28office.15%29.aspx)
    
  
-  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219659%28office.15%29.aspx)
    
  
-  [Remove-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219742%28office.15%29.aspx)
    
  
-  [New-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219502%28office.15%29.aspx)
    
  
Diese Windows PowerShell-Cmdlets können Administratoren Folgendes konfigurieren:
  
    
    

- Eine benutzerdefinierte Gruppe von verwalteten Eigenschaften mit dem externen Webdienst gesendet werden.
    
  
- Eine benutzerdefinierte Gruppe von verwalteten Eigenschaften, die vom externen Webdienst zurückgegeben werden soll.
    
  
- Eine Bedingung Trigger darstellt, die ein Prädikat für jedes Element verarbeiteten ausführen. Wenn eine Bedingung für den Auslöser verwendet wird, wird der externen Webdienst aufgerufen, nur, wenn der Trigger **true**ausgewertet wird. Wenn die Bedingung keine Trigger verwendet wird, werden alle Elemente auf den externen Webdienst gesendet.
    
  
- Ein **FailureMode**, mit dem den Webdienst entweder können fehlschlagen Elemente, die können nicht verarbeitet werden, während der inhaltserweiterung Schritt oder übergeben Sie diese Elemente über ohne Änderung. Wenn die Elemente durchgeführt wurde, werden nicht indiziert und eine Warnung ausgegeben wird in den ULS-Protokolldateien geschrieben.
    
  
- Ein **DebugMode**, der eine schnelle Prototypen des externen Webdiensts ermöglicht. Bei Aktivierung erhält der externen Webdienst aller verfügbare verwaltete Eigenschaften. In **DebugMode**die Trigger-Bedingung wird ignoriert, und keine verwalteten Eigenschaften Ausgaben vom Webdienst werden ebenfalls ignoriert.
    
  
- Ein Schalter, **SendRawData**, die die Rohdaten eines Elements im Binärformat sendet. Dies ist nützlich, wenn mehr Metadaten erforderlich ist, als was aus der analysierten Version des Elements abgerufen werden kann.
    
  
Darüber hinaus stehen die Optionen zur Angabe der größenbeschränkungen für Nachrichten und Timeouts. Finden Sie unter  [Benutzerdefinierte Inhaltsverarbeitung mit dem Webdienstpopup zur Inhaltsanreicherung](custom-content-processing-with-the-content-enrichment-web-service-callout.md) für eine vollständige Liste der konfigurierbaren Eigenschaften.
  
    
    

## <a name="prerequisites-for-using-the-content-enrichment-web-service-callout-for-sharepoint"></a>Voraussetzungen für das Aufrufen des Inhaltserweiterungs-Webdiensts in SharePoint
<a name="SP15ContentEnrich_prereq"> </a>

Um diese Vorgehensweise ausführen zu können, müssen Sie Folgendes in Ihrer Entwicklungsumgebung installiert sein:
  
    
    

- Suche in SharePoint
    
  
- Visual Studio 2010 oder ein vergleichbares Entwicklungstool, das mit .NET Framework kompatibel ist
    
  
- Administratorrechte in der SharePoint-Installation
    
  
- Ein Server, auf dem der Dienst mit IIS gehostet werden kann
    
  
Sie müssen außerdem wissen, wie zum Erstellen einer Website in IIS, und stellen Sie einen Dienst hinzu
  
    
    

## <a name="set-up-a-content-enrichment-service-project"></a>Einrichten eines inhaltserweiterung Service-Projekts
<a name="SP15ContentEnrich_setup"> </a>

In diesem Schritt werden Sie das Dienstprojekt Implementierung erstellen und fügen Sie die erforderlichen Verweise auf das Projekt.
  
    
    

### <a name="to-create-the-project-for-a-content-enrichment-service"></a>So erstellen Sie das Projekt für einen Dienst inhaltserweiterung


1. Wählen Sie in Visual Studio auf der Menüleiste **Datei**, **neu**, **Projekt**.
    
  
2. Wählen Sie in **Projekttypen** unter Visual C#- **WCF**.
    
  
3. Wählen Sie unter **Vorlagen** **WCF Service-Anwendung**. Klicken Sie im Feld **Name** Geben Sie **ContentProcessingEnrichmentService**, und wählen Sie dann auf die Schaltfläche **OK**.
    
  
4. Löschen Sie die automatisch generierte **Service1** -Klasse und **Service1** -Schnittstelle.
    
  

### <a name="to-add-references-to-the-content-enrichment-service-project"></a>So fügen Sie Verweise auf das Projekt inhaltserweiterung-Dienst hinzu


1. Wählen Sie im Menü **Projekt** **Verweis hinzufügen** aus.
    
  
2. Wählen Sie **Durchsuchen** aus, und suchen Sie die **Microsoft.Office.Server.Search.ContentProcessingEnrichment** -Assembly im Installationsordner von SharePoint unter _Installation Path_\\Microsoft Office Servers\\15.0\\Search\\Applications\\External. 
    
    > **Hinweis:** Falls SharePoint auf einem anderen Computer als dem Entwicklungscomputer installiert ist, müssen Sie die Assembly auf den Entwicklungscomputer kopieren und von dort referenzieren. 

## <a name="create-a-content-enrichment-service"></a>Erstellen eines Inhaltserweiterungsdiensts
<a name="SP15ContentEnrich_createservice"> </a>

Ihre Inhalte Verarbeitung Anreicherung Dienst muss die **IContentProcessingEnrichmentService** -Schnittstelle aus dem [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) -Namespace implementieren. Das Codebeispiel in diesem Abschnitt wird eine einfache Implementierung dieser Schnittstelle.
  
    
    
Die Implementierung erfordert zwei verwaltete Eigenschaften für jedes Element, das über den externen Webdienst empfangen: **Author** und **Filename**. Die **Author** ist eine Liste von **String** -Objekten und der **Filename** ist ein **String** -Objekt.
  
    
    
Die Implementierung **IContentProcessingEnrichmentService** schreibt die binären Daten an einen temporären Speicherort auf einem Datenträger mit **Filename** als den Namen der Datei. Klicken Sie dann ein neuer Namen in die Liste der Autoren hinzugefügt und an die inhaltsverarbeitungskomponente zurückgegeben.
  
    
    

### <a name="to-create-the-class-file-for-the-content-enrichment-service"></a>Erstellen Sie die Klassendatei für den Dienst inhaltserweiterung


1. Wählen Sie im Menü **PROJEKT** die Option **Neues Element hinzufügen** aus.
    
  
2. Klicken Sie unter **Visual C#-** unter **Installierte Vorlagen** wählen Sie **Web**, und wählen Sie dann auf **WCF-Dienst**.
    
  
3. Geben Sie **ContentProcessingEnrichmentService.svc**, und wählen Sie dann auf **Hinzufügen**.
    
  
4. Löschen Sie die **IContentProcessingEnrichmentService.cs**-Schnittstelle, die erstellt wird.
    
  

### <a name="to-modify-the-default-code-in-the-contentprocessingenrichmentservice-class"></a>So ändern Sie den Standardcode in der ContentProcessingEnrichmentService-Klasse


1. Ersetzen Sie die vorhandenen Direktiven **using** durch die folgenden **using** Direktiven am Anfang der Klasse.
    
```cs
  
using System;
using System.Collections.Generic;
using System.IO;
using Microsoft.Office.Server.Search.ContentProcessingEnrichment;
using Microsoft.Office.Server.Search.ContentProcessingEnrichment.PropertyTypes;

```

2. Löschen Sie die **DoWork** -Methode.
    
  

### <a name="to-implement-the-icontentprocessingenrichmentservice-interface-method"></a>Implementieren die IContentProcessingEnrichmentService Schnittstelle-Methode


1. Fügen Sie den folgenden Code innerhalb der Klasse, um die erforderlichen Konstanten und Elemente des Objekts definiert.
    
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

2. Fügen Sie den folgenden Code für die **ProcessItem** -Methode.
    
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

3. Ändern **web.config** akzeptieren von Nachrichten bis zu 8 MB, und konfigurieren Sie **readerQuotas**, um eine ausreichend große Zahl sein.
    
  
4. Fügen Sie die folgenden innerhalb **<system.serviceModel>**.
    
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

Erstellen Sie das Projekt, und stellen Sie es auf Ihrer IIS-Website bereit.
  
    
    

## <a name="configure-sharepoint"></a>Konfigurieren von SharePoint
<a name="SP15ContentEnrich_configure"> </a>

Öffnen Sie die SharePoint-Verwaltungsshell, und geben Sie die folgende Sequenz von Windows PowerShell-Cmdlets.
  
    
    

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

Die Abfolge der Windows PowerShell-Cmdlets können Sie zunächst ein Konfigurationsobjekt erstellen, mit dem Cmdlet  [New-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219502%28office.15%29.aspx) . Configuration-Objekts wird anschließend in Richtung der Service-Implementierung verwiesen; als bewährte Methode verwenden Sie `http://localhost:808` für _Site_URL_.
  
    
    
Die verwalteten Eigenschaften **Author** und **Filename** werden an den Dienst für jedes Element gesendet, die verarbeitet wird. Darüber hinaus haben Sie die Webdienstclients darüber informiert, dass der Dienst eine einzelne verwaltete Eigenschaft **Author**ausgegeben wird. In ist zusätzlich zu verwalteten Eigenschaften WebClient-Dienst konfiguriert die Rohdaten des Elements mit einer Einschränkung auf die Größe der Daten senden. Schließlich wird das Cmdlet  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/de-DE/library/jj219659%28office.15%29.aspx)verwendet, um die gesamte Konfiguration zu speichern. Nachdem dieses Cmdlet zurückgibt, wird die Konfiguration aktiv ist, und die Durchforstungskomponente verwendet diese Konfiguration für den nächsten Durchforstungsvorgang.
  
    
    
Nachdem dieser Schritt abgeschlossen ist, können Sie eine vollständige Durchforstung der Website beginnen. Wenn der Dienst ordnungsgemäß funktioniert, sollten Sie überwachen Sie den temporären Ordner auf dem Server mit der Website für die Dokumente geschrieben werden auf dem Datenträger.
  
    
    
Sie können die Konfiguration später mit dem folgenden Cmdlet Windows PowerShell entfernen.
  
    
    



```

Remove-SPEnterpriseSearchContentEnrichmentConfiguration -SearchApplication $ssa
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15ContentEnrich_addresources"> </a>


-  [Starten, anhalten, fortsetzen oder Beenden einer Durchforstung](http://technet.microsoft.com/de-DE/library/jj219814%28office.15%29.aspx)
    
  
-  [Konfigurieren der Suche in SharePoint](configure-search-in-sharepoint.md)
    
  
-  [Benutzerdefinierte Inhaltsverarbeitung mit dem Webdienstpopup zur Inhaltsanreicherung](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  

