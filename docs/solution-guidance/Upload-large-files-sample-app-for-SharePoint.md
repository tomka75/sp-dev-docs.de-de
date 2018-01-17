---
title: "Beispiel-Add-In zum Hochladen großer Dateien für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a6c04ffcdf8d6714250dee1ba0709c869c338b9f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="upload-large-files-sample-add-in-for-sharepoint"></a><span data-ttu-id="be2e5-102">Beispiel-Add-In zum Hochladen großer Dateien für SharePoint</span><span class="sxs-lookup"><span data-stu-id="be2e5-102">Upload large files sample add-in for SharePoint</span></span>

<span data-ttu-id="be2e5-103">Hochladen von Dateien, die größer als 2 MB sind, in SharePoint und SharePoint Online mit SaveBinaryDirect, ContentStream, StartUpload, ContinueUpload und FinishUpload. </span><span class="sxs-lookup"><span data-stu-id="be2e5-103">Upload files larger than 2MB to SharePoint and SharePoint Online using SaveBinaryDirect, ContentStream, StartUpload, ContinueUpload and FinishUpload.</span></span> 

<span data-ttu-id="be2e5-104">_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="be2e5-104">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="be2e5-105">In dem [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)-Beispiel wird gezeigt, wie Sie mit einem vom Anbieter gehosteten Add-In große Dateien in SharePoint hochladen und die maximale Dateigröße von 2 MB beim Hochladen umgehen können.</span><span class="sxs-lookup"><span data-stu-id="be2e5-105">The  [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload) sample shows you how to use a provider-hosted add-in to upload large files to SharePoint, and how to bypass the 2 MB file upload limit.</span></span> <span data-ttu-id="be2e5-106">Verwenden Sie diese Lösung, wenn Sie Dateien, die größer als 2 MB sind, in SharePoint hochladen möchten.</span><span class="sxs-lookup"><span data-stu-id="be2e5-106">Use this solution if you want to upload files that are larger than 2 MB to SharePoint.</span></span> <span data-ttu-id="be2e5-107">In diesem Beispiel wird eine Konsolenanwendung ausgeführt, mit der große Dateien mithilfe einer der folgenden Methoden in einer Dokumentbibliothek hochgeladen werden:</span><span class="sxs-lookup"><span data-stu-id="be2e5-107">This sample runs as a console application that uploads large files to a document library by using one of the following methods:</span></span>

- <span data-ttu-id="be2e5-108">Die  ** [SaveBinaryDirect](https://msdn.microsoft.com/library/office/ee538285.aspx)**-Methode der **Microsoft.SharePoint.Client.File **-Klasse.</span><span class="sxs-lookup"><span data-stu-id="be2e5-108">The  ** [SaveBinaryDirect](https://msdn.microsoft.com/library/office/ee538285.aspx)** method on the **Microsoft.SharePoint.Client.File** class.</span></span>
    
- <span data-ttu-id="be2e5-109">Die  ** [ContentStream](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.contentstream.aspx)**-Eigenschaft der **FileCreationInformation**-Klasse.</span><span class="sxs-lookup"><span data-stu-id="be2e5-109">The  ** [ContentStream](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.contentstream.aspx)** property on the **FileCreationInformation** class.</span></span>
    
- <span data-ttu-id="be2e5-110">Die  ** [StartUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.startupload.aspx)**-,  ** [ContinueUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.continueupload.aspx)**- und ** [FinishUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.finishupload.aspx)**-Methoden in der **File**-Klasse.</span><span class="sxs-lookup"><span data-stu-id="be2e5-110">The  ** [StartUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.startupload.aspx)**,  ** [ContinueUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.continueupload.aspx)** and ** [FinishUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.finishupload.aspx)** methods on the **File** class.</span></span>
    
<span data-ttu-id="be2e5-111">In der folgenden Tabelle werden die Methoden zum Hochladen von Dateien und deren Verwendung erläutert.</span><span class="sxs-lookup"><span data-stu-id="be2e5-111">The following table lists the file upload methods that are available and describes when to use each method.</span></span>

<span data-ttu-id="be2e5-112">**Optionen für das Hochladen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="be2e5-112">**Options for uploading files**</span></span>

|<span data-ttu-id="be2e5-113">**Option für das Hochladen der Datei**</span><span class="sxs-lookup"><span data-stu-id="be2e5-113">**File upload option**</span></span>|<span data-ttu-id="be2e5-114">**Überlegungen**</span><span class="sxs-lookup"><span data-stu-id="be2e5-114">**Considerations**</span></span>|<span data-ttu-id="be2e5-115">**Wann sollte sie verwendet werden**</span><span class="sxs-lookup"><span data-stu-id="be2e5-115">**When should you use this?**</span></span>|<span data-ttu-id="be2e5-116">**Unterstützte Plattformen**</span><span class="sxs-lookup"><span data-stu-id="be2e5-116">**Supported platforms**</span></span>|
|:-----|:-----|:-----|:-----|
| <span data-ttu-id="be2e5-117">Die [Content](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.content.aspx)-Eigenschaft der **FileCreationInformation**-Klasse.</span><span class="sxs-lookup"><span data-stu-id="be2e5-117">[Content](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.content.aspx) property on the **FileCreationInformation** class.</span></span>|<span data-ttu-id="be2e5-118">Maximale Dateigröße, die hochgeladen werden kann, beträgt 2 MB.</span><span class="sxs-lookup"><span data-stu-id="be2e5-118">Maximum file size that can be uploaded is 2 MB.</span></span> <span data-ttu-id="be2e5-119">Zeitüberschreitung nach 30 Minuten.</span><span class="sxs-lookup"><span data-stu-id="be2e5-119">Time-out occurs after 30 minutes.</span></span>|<span data-ttu-id="be2e5-120">Verwenden Sie diese Methode, wenn Sie Dateien hochladen, die kleiner als 2 MB sind.</span><span class="sxs-lookup"><span data-stu-id="be2e5-120">Use to upload files that are less than 2 MB only.</span></span> |<span data-ttu-id="be2e5-121">SharePoint Server 2013, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="be2e5-121">SharePoint Server 2013, SharePoint Online</span></span>|
| <span data-ttu-id="be2e5-122">**SaveBinaryDirect**-Methode der **File**-Klasse.</span><span class="sxs-lookup"><span data-stu-id="be2e5-122">**SaveBinaryDirect** method on the **File** class.</span></span>|<span data-ttu-id="be2e5-123">Keine Dateigrößenbeschränkungen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-123">No file size limits.</span></span> <span data-ttu-id="be2e5-124">Zeitüberschreitung nach 30 Minuten.</span><span class="sxs-lookup"><span data-stu-id="be2e5-124">Time-out occurs after 30 minutes.</span></span>|<span data-ttu-id="be2e5-125">Verwenden Sie diese Methode nur, wenn Sie eine Richtlinie zu Benutzerauthentifzierungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="be2e5-125">Only use this method if you're using a user-only authentication policy.</span></span> <span data-ttu-id="be2e5-126">Eine Richtlinie zu Benutzerauthentifizierungen ist nicht in einem Add-In für SharePoint verfügbar, sie kann jedoch in systemeigenen Geräte-Add-Ins, in Windows PowerShell- und Windows-Konsolenanwendungen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="be2e5-126">User-only authentication policy is not available in an add-in for SharePoint, but can be used in native device apps, Windows PowerShell, and Windows console applications.</span></span>|<span data-ttu-id="be2e5-127">SharePoint Server 2013, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="be2e5-127">SharePoint Server 2013, SharePoint Online</span></span>|
| <span data-ttu-id="be2e5-128">Die **ContentStream**-Eigenschaft der **FileCreationInformation**-Klasse.</span><span class="sxs-lookup"><span data-stu-id="be2e5-128">**ContentStream** property on the **FileCreationInformation** class.</span></span>|<span data-ttu-id="be2e5-129">Keine Dateigrößenbeschränkungen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-129">No file size limits.</span></span> <span data-ttu-id="be2e5-130">Zeitüberschreitung nach 30 Minuten.</span><span class="sxs-lookup"><span data-stu-id="be2e5-130">Time-out occurs after 30 minutes.</span></span>|<span data-ttu-id="be2e5-131">Empfohlen für:</span><span class="sxs-lookup"><span data-stu-id="be2e5-131">Recommended for:</span></span><br/><span data-ttu-id="be2e5-132">- SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="be2e5-132">- SharePoint Server 2013.</span></span><br/><span data-ttu-id="be2e5-133">- SharePoint Online, wenn die Datei kleiner als 10 MB ist.</span><span class="sxs-lookup"><span data-stu-id="be2e5-133">- SharePoint Online when the file is smaller than 10 MB.</span></span>|<span data-ttu-id="be2e5-134">SharePoint Server 2013, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="be2e5-134">SharePoint Server 2013, SharePoint Online</span></span>|
|<span data-ttu-id="be2e5-135">Hochladen einer einzelnen Datei als Satz von Datenblöcken mithilfe der  **StartUpload**-,  **ContinueUpload**- und  **FinishUpload**-Methoden der **File**-Klasse.</span><span class="sxs-lookup"><span data-stu-id="be2e5-135">Upload a single file as a set of chunks using the  **StartUpload**,  **ContinueUpload**, and  **FinishUpload** methods on the **File** class.</span></span>|<span data-ttu-id="be2e5-136">Keine Dateigrößenbeschränkungen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-136">No file size limits.</span></span> <span data-ttu-id="be2e5-137">Zeitüberschreitung nach 30 Minuten.</span><span class="sxs-lookup"><span data-stu-id="be2e5-137">Time-out occurs after 30 minutes.</span></span> <span data-ttu-id="be2e5-138">Jeder Datenblock muss innerhalb von 30 Minuten nach Fertigstellung des vorherigen Blocks hochgeladen werden, um eine Zeitüberschreitung zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="be2e5-138">Each chunk of the file must upload within 30 minutes of completion of the previous chunk to avoid the time-out.</span></span> |<span data-ttu-id="be2e5-139">Empfohlen für SharePoint Online, wenn die Datei größer als 10 MB ist.</span><span class="sxs-lookup"><span data-stu-id="be2e5-139">Recommended for SharePoint Online when the file is larger than 10 MB.</span></span>|<span data-ttu-id="be2e5-140">SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="be2e5-140">SharePoint Online</span></span>|

## <a name="before-you-begin"></a><span data-ttu-id="be2e5-141">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="be2e5-141">Before you begin</span></span>
<span data-ttu-id="be2e5-142"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="be2e5-142"></span></span>

<span data-ttu-id="be2e5-143">Laden Sie zunächst das [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)-Beispiel-Add-In aus dem Projekt [Office 365-Entwicklermuster und -vorgehensweisen](https://github.com/SharePoint/PnP/tree/dev) auf GitHub herunter.</span><span class="sxs-lookup"><span data-stu-id="be2e5-143">To get started, download the  [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-corelargefileupload-sample-app"></a><span data-ttu-id="be2e5-144">Verwenden der Core.LargeFileUpload Beispiel-App</span><span class="sxs-lookup"><span data-stu-id="be2e5-144">Using the Core.LargeFileUpload sample app</span></span>
<span data-ttu-id="be2e5-145"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="be2e5-145"></span></span>

<span data-ttu-id="be2e5-146">Beim Starten dieses Codebeispiels wird eine Konsolenanwendung geöffnet.</span><span class="sxs-lookup"><span data-stu-id="be2e5-146">When you start this code sample, a console application appears.</span></span> <span data-ttu-id="be2e5-147">Sie müssen eine SharePoint Online-Websitesammlungs-URL und Ihre Anmeldeinformationen für Office 365 angeben.</span><span class="sxs-lookup"><span data-stu-id="be2e5-147">You must supply a SharePoint Online site collection URL and your logon credentials for Office 365.</span></span> <span data-ttu-id="be2e5-148">Nach der Authentifizierung zeigt die Konsolenanwendung eine Ausnahme an.</span><span class="sxs-lookup"><span data-stu-id="be2e5-148">After authentication, the console application displays an exception.</span></span> <span data-ttu-id="be2e5-149">Die Ausnahme tritt auf, wenn die **UploadDocumentContent**-Methode in FileUploadService.cs versucht, die **FileCreationInformation.Content**-Eigenschaft zum Hochladen einer Datei zu verwenden, die größer als 2 MB ist.</span><span class="sxs-lookup"><span data-stu-id="be2e5-149">The exception occurs when the  **UploadDocumentContent** method in FileUploadService.cs tries to use the **FileCreationInformation.Content** property to upload a file that is larger than 2 MB.</span></span> <span data-ttu-id="be2e5-150">**UploadDocumentContent** erstellt außerdem eine Dokumentbibliothek **Dokumente**, wenn diese noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="be2e5-150">**UploadDocumentContent** also creates a document library called **Docs** if it does not already exist.</span></span> <span data-ttu-id="be2e5-151">Die Dokumentbibliothek **Dokumente** wird weiter unten in diesem Codebeispiel verwendet.</span><span class="sxs-lookup"><span data-stu-id="be2e5-151">The **Docs** document library is used later in this code sample.</span></span>

> [!NOTE] 
> <span data-ttu-id="be2e5-152">Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="be2e5-152">Note  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
public void UploadDocumentContent(ClientContext ctx, string libraryName, string filePath)
        {
            Web web = ctx.Web;

            // Ensure that target library exists. Create if it is missing.
            if (!LibraryExists(ctx, web, libraryName))
            {
                CreateLibrary(ctx, web, libraryName);
            }

            FileCreationInformation newFile = new FileCreationInformation();

         // The next line of code causes an exception to be thrown for files larger than 2 MB.
            newFile.Content = System.IO.File.ReadAllBytes(filePath);
            newFile.Url = System.IO.Path.GetFileName(filePath);

            // Get instances to the given library.
            List docs = web.Lists.GetByTitle(libraryName);
            
 // Add file to the library.
            Microsoft.SharePoint.Client.File uploadFile = docs.RootFolder.Files.Add(newFile);
            ctx.Load(uploadFile);
            ctx.ExecuteQuery();
        } 

```

<span data-ttu-id="be2e5-153">Dieses Codebeispiel bietet in FileUploadService.cs drei Optionen, mit denen Sie große Dateien in einer Dokumentbibliothek hochladen können:</span><span class="sxs-lookup"><span data-stu-id="be2e5-153">In FileUploadService.cs, this code sample provides three options that you can use to upload large files to a document library:</span></span>

- <span data-ttu-id="be2e5-154">Die **File.SaveBinaryDirect**-Methode.</span><span class="sxs-lookup"><span data-stu-id="be2e5-154">The  **File.SaveBinaryDirect** method.</span></span>
    
- <span data-ttu-id="be2e5-155">Die **FileCreationInformation.ContentStream**-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="be2e5-155">The  **FileCreationInformation.ContentStream** property.</span></span>
    
- <span data-ttu-id="be2e5-156">Die **StartUpload**-, **ContinueUpload**- und **FinishUpload**-Methoden der **File**-Klasse.</span><span class="sxs-lookup"><span data-stu-id="be2e5-156">The  **StartUpload**,  **ContinueUpload**, and  **FinishUpload** methods on the **File** class.</span></span>
    
<span data-ttu-id="be2e5-157">**SaveBinaryDirect** verwendet in FileUploadService.cs die **Microsoft.SharePoint.Client.File.SaveBinaryDirect**-Methode mit einem **FileStream**-Objekt zum Hochladen von Dateien in einer Dokumentbibliothek. </span><span class="sxs-lookup"><span data-stu-id="be2e5-157">In FileUploadService.cs,  **SaveBinaryDirect** uses the **Microsoft.SharePoint.Client.File.SaveBinaryDirect** method with a **FileStream** object to upload files to a document library.</span></span>

```C#
public void SaveBinaryDirect(ClientContext ctx, string libraryName, string filePath)
        {
            Web web = ctx.Web;
            // Ensure that the target library exists. Create it if it is missing.
            if (!LibraryExists(ctx, web, libraryName))
            {
                CreateLibrary(ctx, web, libraryName);
            }

            using (FileStream fs = new FileStream(filePath, FileMode.Open))
            {
                Microsoft.SharePoint.Client.File.SaveBinaryDirect(ctx, string.Format("/{0}/{1}", libraryName, System.IO.Path.GetFileName(filePath)), fs, true);
            }

        } 

```

<span data-ttu-id="be2e5-158">**UploadDocumentContentStream** verwendet in FileUploadService.cs die **FileCreationInformation.ContentStream**-Eigenschaft mit dem **FileStream**-Objekt zum Hochladen einer Datei in einer Dokumentbibliothek .</span><span class="sxs-lookup"><span data-stu-id="be2e5-158">In FileUploadService.cs,  **UploadDocumentContentStream** uses the **FileCreationInformation.ContentStream** property with the **FileStream** object to upload a file to a document library.</span></span>

```C#
public void UploadDocumentContentStream(ClientContext ctx, string libraryName, string filePath)
        {

            Web web = ctx.Web;
            // Ensure that the target library exists. Create it if it is missing.
            if (!LibraryExists(ctx, web, libraryName))
            {
                CreateLibrary(ctx, web, libraryName);
            }

            using (FileStream fs = new FileStream(filePath, FileMode.Open))
            {
                FileCreationInformation flciNewFile = new FileCreationInformation();

                // This is the key difference for the first case - using ContentStream property
                flciNewFile.ContentStream = fs;
                flciNewFile.Url = System.IO.Path.GetFileName(filePath);
                flciNewFile.Overwrite = true;

                List docs = web.Lists.GetByTitle(libraryName);
                Microsoft.SharePoint.Client.File uploadFile = docs.RootFolder.Files.Add(flciNewFile);

                ctx.Load(uploadFile);
                ctx.ExecuteQuery();
            }
        }

```

<span data-ttu-id="be2e5-159">**UploadFileSlicePerSlice** lädt in FileUploadService.cs eine große Datei in einer Dokumentbibliothek als ein Satz von Datenblöcken oder Abschnitten hoch.</span><span class="sxs-lookup"><span data-stu-id="be2e5-159">In FileUploadService.cs,  **UploadFileSlicePerSlice** uploads a large file to a document library as a set of chunks or fragments.</span></span> <span data-ttu-id="be2e5-160">**UploadFileSlicePerSlice** führt die folgenden Aufgaben durch:</span><span class="sxs-lookup"><span data-stu-id="be2e5-160">**UploadFileSlicePerSlice** performs the following tasks:</span></span>

1. <span data-ttu-id="be2e5-161">Ruft eine neue GUID ab.</span><span class="sxs-lookup"><span data-stu-id="be2e5-161">Gets a new GUID.</span></span> <span data-ttu-id="be2e5-162">Um eine Datei in Datenblöcken hochzuladen, müssen Sie eine eindeutige GUID verwenden.</span><span class="sxs-lookup"><span data-stu-id="be2e5-162">To upload a file in chunks, you must use a unique GUID.</span></span> 
    
2. <span data-ttu-id="be2e5-163">Berechnet die Blockgröße eines Abschnitts in Byte.</span><span class="sxs-lookup"><span data-stu-id="be2e5-163">Calculates the block size of the chunk in bytes.</span></span> <span data-ttu-id="be2e5-164">Zum Berechnen der Blockgröße in Bytes verwendet **UploadFileSlicePerSlice** das **FileChunkSizeInMB**-Objekt, das die Größe der einzelnen Datenblöcke in MB angibt.</span><span class="sxs-lookup"><span data-stu-id="be2e5-164">To calculate the block size in bytes,  **UploadFileSlicePerSlice** uses **fileChunkSizeInMB**, which specifies the size of the individual chunks in MB.</span></span> 
    
3. <span data-ttu-id="be2e5-165">Überprüft, ob die Größe der hochzuladenden Datei (**fileSize**) kleiner als oder gleich der Blockgröße (**blockSize**) ist.</span><span class="sxs-lookup"><span data-stu-id="be2e5-165">Tests if the size of the file to upload ( **fileSize**) is less than or equal to the chunk size ( **blockSize**).</span></span>
    
    1. <span data-ttu-id="be2e5-166">Wenn **fileSize** kleiner als oder gleich der Blockgröße ist, wird in dem Beispiel sichergestellt, dass die Datei mithilfe der **FileCreationInformation.ContentStream**-Eigenschaft hochgeladen wird.</span><span class="sxs-lookup"><span data-stu-id="be2e5-166">If  **fileSize** is less than or equal to the chunk size, the sample ensures that the file is still uploaded by using the **FileCreationInformation.ContentStream** property.</span></span> <span data-ttu-id="be2e5-167">Denken Sie daran, dass die empfohlene Blockgröße bei 10 MB und größer liegt.</span><span class="sxs-lookup"><span data-stu-id="be2e5-167">Remember that the recommended chunk size is 10 MB or larger.</span></span>
      
    2. <span data-ttu-id="be2e5-168">Wenn **fileSize** größer als die Blockgröße ist, trifft Folgendes zu:</span><span class="sxs-lookup"><span data-stu-id="be2e5-168">If  **fileSize** is larger than the chunk size:</span></span>
    
        1. <span data-ttu-id="be2e5-169">Ein Datenblock der Datei wird in einem **Puffer** gelesen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-169">A chunk of the file is read into  **buffer**.</span></span>
    
        2. <span data-ttu-id="be2e5-170">Wenn die Blockgröße gleich der Dateigröße ist, wird die gesamte Datei gelesen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-170">If the chunk size is equal to the file size, the entire file was read.</span></span> <span data-ttu-id="be2e5-171">Der Datenblock wird in **lastBuffer** kopiert.</span><span class="sxs-lookup"><span data-stu-id="be2e5-171">The chunk is copied to  **lastBuffer**.</span></span>  <span data-ttu-id="be2e5-172">**lastBuffer** verwendet dann **File.FinishUpload**, um den Block hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-172">**lastBuffer** then uses **File.FinishUpload** to upload the chunk.</span></span>
    
    3. <span data-ttu-id="be2e5-173">Ist die Blockgröße nicht gleich der Dateigröße, gibt es mehr als einen Datenblock, der aus der Datei zu lesen ist.</span><span class="sxs-lookup"><span data-stu-id="be2e5-173">If the chunk size is not equal to the file size, there is more than one chunk to read from the file.</span></span>  <span data-ttu-id="be2e5-174">**File.StartUpload** wird aufgerufen, um den ersten Abschnitt hochladen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-174">**File.StartUpload** is called to upload the first chunk.</span></span> <span data-ttu-id="be2e5-175">Das **fileoffset**-Objekt, das als Anfang des nächsten Datenblocks verwendet wird, wird dann auf die Anzahl der aus dem ersten Datenblock hochgeladenen Bytes festgelegt.</span><span class="sxs-lookup"><span data-stu-id="be2e5-175">**fileoffset**, which is used as the starting point of the next chunk, is then set to the amount of bytes uploaded from the first chunk.</span></span> <span data-ttu-id="be2e5-176">Beim Lesen des nächsten Datenblocks wird, falls der letzte Block noch nicht erreicht wurde, **File.ContinueUpload** aufgerufen, um den nächsten Datenblock der Datei hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-176">When the next chunk is read, if the last chunk has not been reached,  **File.ContinueUpload** is called to upload the next chunk of the file.</span></span> <span data-ttu-id="be2e5-177">Der Vorgang wird wiederholt, bis der letzte Block gelesen wurde.</span><span class="sxs-lookup"><span data-stu-id="be2e5-177">The process repeats until the last chunk is read.</span></span> <span data-ttu-id="be2e5-178">Beim Lesen des letzten Datenblocks lädt **File.FinishUpload** den letzten Block hoch und übergibt die Datei.</span><span class="sxs-lookup"><span data-stu-id="be2e5-178">When the last chunk is read, **File.FinishUpload** uploads the last chunk and commits the file.</span></span> <span data-ttu-id="be2e5-179">Der Dateiinhalt wird dann geändert, wenn diese Methode ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="be2e5-179">The file content is then changed when this method is finished.</span></span>

> [!NOTE] 
> <span data-ttu-id="be2e5-180">Berücksichtigen die folgenden bewährten Methoden:</span><span class="sxs-lookup"><span data-stu-id="be2e5-180">Note  Consider the following best practices:</span></span>
- <span data-ttu-id="be2e5-181">Verwenden Sie einen Wiederholungsmechanismus für den Fall, dass der Upload unterbrochen wird.</span><span class="sxs-lookup"><span data-stu-id="be2e5-181">Use a retry mechanism in case your upload is interrupted.</span></span> <span data-ttu-id="be2e5-182">Wenn das Hochladen einer Datei unterbrochen wird, wird die Datei „nicht fertig gestellte Datei“ genannt.</span><span class="sxs-lookup"><span data-stu-id="be2e5-182">When an uploaded file is interrupted, the file is called an unfinished file.</span></span> <span data-ttu-id="be2e5-183">Möglicherweise möchten Sie mit dem Hochladen einer nicht fertig gestellten Datei unmittelbar nach der Unterbrechung des Uploads erneut beginnen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-183">You may restart uploading an unfinished file soon after the upload was interrupted.</span></span> <span data-ttu-id="be2e5-184">Nicht fertig gestellte Dateien werden in dem Zeitraum zwischen 6 Stunden und 24 Stunden, nachdem das Hochladen der Datei unterbrochen wurde, auf dem Server entfernt.</span><span class="sxs-lookup"><span data-stu-id="be2e5-184">Unfinished files are removed from the server between 6 hours to 24 hours after the unfinished file was interrupted.</span></span> <span data-ttu-id="be2e5-185">Dieser Zeitraum kann sich ohne vorherige Ankündigung ändern.</span><span class="sxs-lookup"><span data-stu-id="be2e5-185">This removal period might change without notice.</span></span>
- <span data-ttu-id="be2e5-186">Beim Hochladen einer Datei in Datenblöcken in SharePoint Online, wird die Datei in SharePoint Online gesperrt.</span><span class="sxs-lookup"><span data-stu-id="be2e5-186">When uploading a file in chunks to SharePoint Online, a lock is placed on the file in SharePoint Online.</span></span> <span data-ttu-id="be2e5-187">Wenn eine Unterbrechung auftritt, bleibt die Datei 15 Minuten gesperrt.</span><span class="sxs-lookup"><span data-stu-id="be2e5-187">When an interruption occurs, the file remains locked for 15 minutes.</span></span> <span data-ttu-id="be2e5-188">Wird der nächste Datenblock der Datei nicht innerhalb von 15 Minuten in SharePoint Online hochgeladen, wird die Datei freigegeben.</span><span class="sxs-lookup"><span data-stu-id="be2e5-188">If the next chunk of the file is not uploaded to SharePoint Online within 15 minutes, the lock is removed.</span></span> <span data-ttu-id="be2e5-189">Nach der Freigabe können Sie mit dem Hochladen der Datei fortfahren, oder ein anderer Benutzer kann mit dem Hochladen der Datei beginnen.</span><span class="sxs-lookup"><span data-stu-id="be2e5-189">After the lock is removed, you can resume uploading, or another user can start uploading the file.</span></span> <span data-ttu-id="be2e5-190">Beginnt ein anderer Benutzer mit dem Hochladen der Datei, wird die noch nicht fertig gestellte Datei aus SharePoint Online entfernt.</span><span class="sxs-lookup"><span data-stu-id="be2e5-190">If another user starts uploading the file, your unfinished file is removed from SharePoint Online.</span></span> <span data-ttu-id="be2e5-191">Die Dauer, für die eine Datei gesperrt ist, nachdem das Hochladen unterbrochen wurde, kann sich ohne vorherige Ankündigung ändern.</span><span class="sxs-lookup"><span data-stu-id="be2e5-191">The period of time the lock remains on a file after an upload is interrupted can change without notice.</span></span>
- <span data-ttu-id="be2e5-192">Sie möchten die Blockgröße ggf. ändern.</span><span class="sxs-lookup"><span data-stu-id="be2e5-192">You might change the chunk size.</span></span> <span data-ttu-id="be2e5-193">Es wird empfohlen, eine Blockgröße von 10 MB zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="be2e5-193">We recommend using a chunk size of 10 MB.</span></span>
- <span data-ttu-id="be2e5-194">Verfolgen Sie beim Fortsetzen des Hochladens eines unterbrochenen Datenblocks nach, welche Datenblöcke bereits erfolgreich hochgeladen wurden.</span><span class="sxs-lookup"><span data-stu-id="be2e5-194">Resume an interrupted chunk by tracking which chunks uploaded successfully.</span></span>

<span data-ttu-id="be2e5-195">Datenblöcke müssen in einer sequenziellen Reihenfolge hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="be2e5-195">Chunks must be uploaded in sequential order.</span></span> <span data-ttu-id="be2e5-196">Mehrere Datenblöcke können nicht gleichzeitig hochgeladen werden (z. B. unter Verwendung eines Multithread-Ansatzes).</span><span class="sxs-lookup"><span data-stu-id="be2e5-196">You cannot upload slices concurrently (for example, by using a multithreaded approach).</span></span>

```
 public Microsoft.SharePoint.Client.File UploadFileSlicePerSlice(ClientContext ctx, string libraryName, string fileName, int fileChunkSizeInMB = 3)
        {
            // Each sliced upload requires a unique ID.
            Guid uploadId = Guid.NewGuid();

            // Get the name of the file.
            string uniqueFileName = Path.GetFileName(fileName);

            // Ensure that target library exists, and create it if it is missing.
            if (!LibraryExists(ctx, ctx.Web, libraryName))
            {
                CreateLibrary(ctx, ctx.Web, libraryName);
            }
            // Get the folder to upload into. 
            List docs = ctx.Web.Lists.GetByTitle(libraryName);
            ctx.Load(docs, l => l.RootFolder);
            // Get the information about the folder that will hold the file.
            ctx.Load(docs.RootFolder, f => f.ServerRelativeUrl);
            ctx.ExecuteQuery();

            // File object.
            Microsoft.SharePoint.Client.File uploadFile;

            // Calculate block size in bytes.
            int blockSize = fileChunkSizeInMB * 1024 * 1024;

            // Get the information about the folder that will hold the file.
            ctx.Load(docs.RootFolder, f => f.ServerRelativeUrl);
            ctx.ExecuteQuery();


            // Get the size of the file.
            long fileSize = new FileInfo(fileName).Length;

            if (fileSize <= blockSize)
            {
                // Use regular approach.
                using (FileStream fs = new FileStream(fileName, FileMode.Open))
                {
                    FileCreationInformation fileInfo = new FileCreationInformation();
                    fileInfo.ContentStream = fs;
                    fileInfo.Url = uniqueFileName;
                    fileInfo.Overwrite = true;
                    uploadFile = docs.RootFolder.Files.Add(fileInfo);
                    ctx.Load(uploadFile);
                    ctx.ExecuteQuery();
                    // Return the file object for the uploaded file.
                    return uploadFile;
                }
            }
            else
            {
                // Use large file upload approach.
                ClientResult<long> bytesUploaded = null;

                FileStream fs = null;
                try
                {
                    fs = System.IO.File.Open(fileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
                    using (BinaryReader br = new BinaryReader(fs))
                    {
                        byte[] buffer = new byte[blockSize];
                        Byte[] lastBuffer = null;
                        long fileoffset = 0;
                        long totalBytesRead = 0;
                        int bytesRead;
                        bool first = true;
                        bool last = false;

                        // Read data from file system in blocks. 
                        while ((bytesRead = br.Read(buffer, 0, buffer.Length)) > 0)
                        {
                            totalBytesRead = totalBytesRead + bytesRead;

                            // You've reached the end of the file.
                            if (totalBytesRead == fileSize)
                            {
                                last = true;
                                // Copy to a new buffer that has the correct size.
                                lastBuffer = new byte[bytesRead];
                                Array.Copy(buffer, 0, lastBuffer, 0, bytesRead);
                            }

                            if (first)
                            {
                                using (MemoryStream contentStream = new MemoryStream())
                                {
                                    // Add an empty file.
                                    FileCreationInformation fileInfo = new FileCreationInformation();
                                    fileInfo.ContentStream = contentStream;
                                    fileInfo.Url = uniqueFileName;
                                    fileInfo.Overwrite = true;
                                    uploadFile = docs.RootFolder.Files.Add(fileInfo);

                                    // Start upload by uploading the first slice. 
                                    using (MemoryStream s = new MemoryStream(buffer))
                                    {
                                        // Call the start upload method on the first slice.
                                        bytesUploaded = uploadFile.StartUpload(uploadId, s);
                                        ctx.ExecuteQuery();
                                        // fileoffset is the pointer where the next slice will be added.
                                        fileoffset = bytesUploaded.Value;
                                    }

                                    // You can only start the upload once.
                                    first = false;
                                }
                            }
                            else
                            {
                                // Get a reference to your file.
                                uploadFile = ctx.Web.GetFileByServerRelativeUrl(docs.RootFolder.ServerRelativeUrl + System.IO.Path.AltDirectorySeparatorChar + uniqueFileName);

                                if (last)
                                {
                                    // Is this the last slice of data?
                                    using (MemoryStream s = new MemoryStream(lastBuffer))
                                    {
                                        // End sliced upload by calling FinishUpload.
                                        uploadFile = uploadFile.FinishUpload(uploadId, fileoffset, s);
                                        ctx.ExecuteQuery();

                                        // Return the file object for the uploaded file.
                                        return uploadFile;
                                    }
                                }
                                else
                                {
                                    using (MemoryStream s = new MemoryStream(buffer))
                                    {
                                        // Continue sliced upload.
                                        bytesUploaded = uploadFile.ContinueUpload(uploadId, fileoffset, s);
                                        ctx.ExecuteQuery();
                                        // Update fileoffset for the next slice.
                                        fileoffset = bytesUploaded.Value;
                                    }
                                }
                            }

                        } // while ((bytesRead = br.Read(buffer, 0, buffer.Length)) > 0)
                    }
                }
                finally
                {
                    if (fs != null)
                    {
                        fs.Dispose();
                    }
                }
            }

            return null;
        }
```

<span data-ttu-id="be2e5-197">Navigieren Sie nach Abschluss des Codebeispiels auf Ihrer Office 365-Website zu der Dokumentbibliothek **Dokumente**, indem Sie **Zuletzt verwendet** >  > **Dokumente** wählen. Überprüfen Sie, ob die Dokumentbibliothek **Dokumente** drei große Dateien enthält. </span><span class="sxs-lookup"><span data-stu-id="be2e5-197">After the code sample is finished, in your Office 365 site, you can go to the  **Docs** document library by choosing **Recent** > **Docs**. Verify that the  **Docs** document library contains three large files.</span></span>

## <a name="see-also"></a><span data-ttu-id="be2e5-198">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="be2e5-198">See also</span></span>
<span data-ttu-id="be2e5-199"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="be2e5-199"></span></span>

-  [<span data-ttu-id="be2e5-200">Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="be2e5-200">Enterprise content management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  <span data-ttu-id="be2e5-201">[Core.BulkDocumentUploader-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader)</span><span class="sxs-lookup"><span data-stu-id="be2e5-201">[Core.BulkDocumentUploader sample](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader)</span></span>
