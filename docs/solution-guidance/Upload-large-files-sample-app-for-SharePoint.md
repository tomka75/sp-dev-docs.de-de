---
title: "Beispiel-Add-In zum Hochladen großer Dateien für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 1d9df7d05d92e79b89dd4d552522eeb3447b2d56
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="upload-large-files-sample-add-in-for-sharepoint"></a>Beispiel-Add-In zum Hochladen großer Dateien für SharePoint

Hochladen von Dateien, die größer als 2 MB sind, in SharePoint und SharePoint Online mit SaveBinaryDirect, ContentStream, StartUpload, ContinueUpload und FinishUpload.  

_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_

In dem [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)-Beispiel wird gezeigt, wie Sie mit einem vom Anbieter gehosteten Add-In große Dateien in SharePoint hochladen und die maximale Dateigröße von 2 MB beim Hochladen umgehen können. Verwenden Sie diese Lösung, wenn Sie Dateien, die größer als 2 MB sind, in SharePoint hochladen möchten. In diesem Beispiel wird eine Konsolenanwendung ausgeführt, mit der große Dateien mithilfe einer der folgenden Methoden in einer Dokumentbibliothek hochgeladen werden:

- Die  ** [SaveBinaryDirect](https://msdn.microsoft.com/library/office/ee538285.aspx)**-Methode der **Microsoft.SharePoint.Client.File **-Klasse.
    
- Die  ** [ContentStream](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.contentstream.aspx)**-Eigenschaft der **FileCreationInformation**-Klasse.
    
- Die  ** [StartUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.startupload.aspx)**-,  ** [ContinueUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.continueupload.aspx)**- und ** [FinishUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.finishupload.aspx)**-Methoden in der **File**-Klasse.
    
In der folgenden Tabelle werden die Methoden zum Hochladen von Dateien und deren Verwendung erläutert.

**Optionen für das Hochladen von Dateien**

|**Option für das Hochladen der Datei**|**Überlegungen**|**Wann sollte sie verwendet werden**|**Unterstützte Plattformen**|
|:-----|:-----|:-----|:-----|
| Die [Content](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.content.aspx)-Eigenschaft der **FileCreationInformation**-Klasse.|Maximale Dateigröße, die hochgeladen werden kann, beträgt 2 MB. Zeitüberschreitung nach 30 Minuten.|Verwenden Sie diese Methode, wenn Sie Dateien hochladen, die kleiner als 2 MB sind. |SharePoint Server 2013, SharePoint Online|
| **SaveBinaryDirect**-Methode der **File**-Klasse.|Keine Dateigrößenbeschränkungen. Zeitüberschreitung nach 30 Minuten.|Verwenden Sie diese Methode nur, wenn Sie eine Richtlinie zu Benutzerauthentifzierungen verwenden. Eine Richtlinie zu Benutzerauthentifizierungen ist nicht in einem Add-In für SharePoint verfügbar, sie kann jedoch in systemeigenen Geräte-Add-Ins, in Windows PowerShell- und Windows-Konsolenanwendungen verwendet werden.|SharePoint Server 2013, SharePoint Online|
| Die **ContentStream**-Eigenschaft der **FileCreationInformation**-Klasse.|Keine Dateigrößenbeschränkungen. Zeitüberschreitung nach 30 Minuten.|Empfohlen für:<br/>- SharePoint Server 2013.<br/>- SharePoint Online, wenn die Datei kleiner als 10 MB ist.|SharePoint Server 2013, SharePoint Online|
|Hochladen einer einzelnen Datei als Satz von Datenblöcken mithilfe der  **StartUpload**-,  **ContinueUpload**- und  **FinishUpload**-Methoden der **File**-Klasse.|Keine Dateigrößenbeschränkungen. Zeitüberschreitung nach 30 Minuten. Jeder Datenblock muss innerhalb von 30 Minuten nach Fertigstellung des vorherigen Blocks hochgeladen werden, um eine Zeitüberschreitung zu vermeiden. |Empfohlen für SharePoint Online, wenn die Datei größer als 10 MB ist.|SharePoint Online|

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie zunächst das [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)-Beispiel-Add-In aus dem Projekt [Office 365-Entwicklermuster und -vorgehensweisen](https://github.com/SharePoint/PnP/tree/dev) auf GitHub herunter.

## <a name="using-the-corelargefileupload-sample-app"></a>Verwenden der Core.LargeFileUpload Beispiel-App
<a name="sectionSection1"> </a>

Beim Starten dieses Codebeispiels wird eine Konsolenanwendung geöffnet. Sie müssen eine SharePoint Online-Websitesammlungs-URL und Ihre Anmeldeinformationen für Office 365 angeben. Nach der Authentifizierung zeigt die Konsolenanwendung eine Ausnahme an. Die Ausnahme tritt auf, wenn die **UploadDocumentContent**-Methode in FileUploadService.cs versucht, die **FileCreationInformation.Content**-Eigenschaft zum Hochladen einer Datei zu verwenden, die größer als 2 MB ist. **UploadDocumentContent** erstellt außerdem eine Dokumentbibliothek **Dokumente**, wenn diese noch nicht vorhanden ist. Die Dokumentbibliothek **Dokumente** wird weiter unten in diesem Codebeispiel verwendet.

**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.

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

Dieses Codebeispiel bietet in FileUploadService.cs drei Optionen, mit denen Sie große Dateien in einer Dokumentbibliothek hochladen können:

- Die **File.SaveBinaryDirect**-Methode.
    
- Die **FileCreationInformation.ContentStream**-Eigenschaft.
    
- Die **StartUpload**-, **ContinueUpload**- und **FinishUpload**-Methoden der **File**-Klasse.
    
**SaveBinaryDirect** verwendet in FileUploadService.cs die **Microsoft.SharePoint.Client.File.SaveBinaryDirect**-Methode mit einem **FileStream**-Objekt zum Hochladen von Dateien in einer Dokumentbibliothek. 

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

**UploadDocumentContentStream** verwendet in FileUploadService.cs die **FileCreationInformation.ContentStream**-Eigenschaft mit dem **FileStream**-Objekt zum Hochladen einer Datei in einer Dokumentbibliothek .

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

**UploadFileSlicePerSlice** lädt in FileUploadService.cs eine große Datei in einer Dokumentbibliothek als ein Satz von Datenblöcken oder Abschnitten hoch. **UploadFileSlicePerSlice** führt die folgenden Aufgaben durch:

1. Ruft eine neue GUID ab. Um eine Datei in Datenblöcken hochzuladen, müssen Sie eine eindeutige GUID verwenden. 
    
2. Berechnet die Blockgröße eines Abschnitts in Byte. Zum Berechnen der Blockgröße in Bytes verwendet **UploadFileSlicePerSlice** das **FileChunkSizeInMB**-Objekt, das die Größe der einzelnen Datenblöcke in MB angibt. 
    
3. Überprüft, ob die Größe der hochzuladenden Datei (**fileSize**) kleiner als oder gleich der Blockgröße (**blockSize**) ist.
    
    1. Wenn **fileSize** kleiner als oder gleich der Blockgröße ist, wird in dem Beispiel sichergestellt, dass die Datei mithilfe der **FileCreationInformation.ContentStream**-Eigenschaft hochgeladen wird. Denken Sie daran, dass die empfohlene Blockgröße bei 10 MB und größer liegt.
      
    2. Wenn **fileSize** größer als die Blockgröße ist, trifft Folgendes zu:
    
        1. Ein Datenblock der Datei wird in einem **Puffer** gelesen.
    
        2. Wenn die Blockgröße gleich der Dateigröße ist, wird die gesamte Datei gelesen. Der Datenblock wird in **lastBuffer** kopiert.  **lastBuffer** verwendet dann **File.FinishUpload**, um den Block hochzuladen.
    
    3. Ist die Blockgröße nicht gleich der Dateigröße, gibt es mehr als einen Datenblock, der aus der Datei zu lesen ist.  **File.StartUpload** wird aufgerufen, um den ersten Abschnitt hochladen. Das **fileoffset**-Objekt, das als Anfang des nächsten Datenblocks verwendet wird, wird dann auf die Anzahl der aus dem ersten Datenblock hochgeladenen Bytes festgelegt. Beim Lesen des nächsten Datenblocks wird, falls der letzte Block noch nicht erreicht wurde, **File.ContinueUpload** aufgerufen, um den nächsten Datenblock der Datei hochzuladen. Der Vorgang wird wiederholt, bis der letzte Block gelesen wurde. Beim Lesen des letzten Datenblocks lädt **File.FinishUpload** den letzten Block hoch und übergibt die Datei. Der Dateiinhalt wird dann geändert, wenn diese Methode ausgeführt wurde.

**Hinweis:** Berücksichtigen die folgenden bewährten Methoden:
- Verwenden Sie einen Wiederholungsmechanismus für den Fall, dass der Upload unterbrochen wird. Wenn das Hochladen einer Datei unterbrochen wird, wird die Datei „nicht fertig gestellte Datei“ genannt. Möglicherweise möchten Sie mit dem Hochladen einer nicht fertig gestellten Datei unmittelbar nach der Unterbrechung des Uploads erneut beginnen. Nicht fertig gestellte Dateien werden in dem Zeitraum zwischen 6 Stunden und 24 Stunden, nachdem das Hochladen der Datei unterbrochen wurde, auf dem Server entfernt. Dieser Zeitraum kann sich ohne vorherige Ankündigung ändern.
- Beim Hochladen einer Datei in Datenblöcken in SharePoint Online, wird die Datei in SharePoint Online gesperrt. Wenn eine Unterbrechung auftritt, bleibt die Datei 15 Minuten gesperrt. Wird der nächste Datenblock der Datei nicht innerhalb von 15 Minuten in SharePoint Online hochgeladen, wird die Datei freigegeben. Nach der Freigabe können Sie mit dem Hochladen der Datei fortfahren, oder ein anderer Benutzer kann mit dem Hochladen der Datei beginnen. Beginnt ein anderer Benutzer mit dem Hochladen der Datei, wird die noch nicht fertig gestellte Datei aus SharePoint Online entfernt. Die Dauer, für die eine Datei gesperrt ist, nachdem das Hochladen unterbrochen wurde, kann sich ohne vorherige Ankündigung ändern.
- Sie möchten die Blockgröße ggf. ändern. Es wird empfohlen, eine Blockgröße von 10 MB zu verwenden.
- Verfolgen Sie beim Fortsetzen des Hochladens eines unterbrochenen Datenblocks nach, welche Datenblöcke bereits erfolgreich hochgeladen wurden.

Datenblöcke müssen in einer sequenziellen Reihenfolge hochgeladen werden. Mehrere Datenblöcke können nicht gleichzeitig hochgeladen werden (z. B. unter Verwendung eines Multithread-Ansatzes).

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

Navigieren Sie nach Abschluss des Codebeispiels auf Ihrer Office 365-Website zu der Dokumentbibliothek **Dokumente**, indem Sie **Zuletzt verwendet** >  > **Dokumente** wählen. Überprüfen Sie, ob die Dokumentbibliothek **Dokumente** drei große Dateien enthält. 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [Core.BulkDocumentUploader-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader)
