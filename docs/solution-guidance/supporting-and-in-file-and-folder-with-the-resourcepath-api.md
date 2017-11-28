---
title: "Unterstützung von % und # in Dateien und Ordner mit der API http://"
ms.date: 11/03/2017
ms.openlocfilehash: 4667020c2387650d8ad84dc000afa785f7b07016
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="supporting--and--in-file-and-folder-with-the-resourcepath-api"></a>Unterstützung von % und # in Dateien und Ordner mit der API http://

Unterstützung für % und # dürfen in Dateien und Ordner wird in SharePoint Online bereitgestellt wird.  Leider kann aufgrund einer vorhandenen API Strukturen und Muster aufrufen, arbeiten mit diesen Dateinamen manchmal mehrdeutig wird.  Sie können [Weitere Hintergrund dies in unserem Entwicklerblog](https://dev.office.com/blogs/upcoming-changes-to-sharepoint-and-onedrive-for-business-apis-to-support-and-in-file-names)suchen.  Neue APIs wurden in lässt sich sagen auf die SharePoint Online-Client-Objekt Objektmodell (CSOM)-Oberfläche # und % Zeichen unterstützen hinzugefügt.

## <a name="resourcepath"></a>Http://
 
Beachten Sie als eine Zusammenfassung vorhandenen SharePoint-APIs (beispielsweise SPFileCollection.GetByUrl) Zeichenfolge-basierte Handles beide codiert und decodiert automatisch von URLs, unter der Annahme, dass % und #-Zeichen in einem Pfad impliziert, dass die URL codiert wurde.  Durch die neue Unterstützung ist % und # dürfen in der Datei und der Ordner, der diese automatische Behandlung jetzt problematisch, weil es downstream Code ignorieren oder Dateinamen mit % und # dürfen in diese mishandle führen kann.
 
Eine neue Klasse-- `Microsoft.SharePoint.Client.ResourcePath` --APIs hinzugefügt wurde.  Die Klasse http:// ist unerlässlich für die Unterstützung der folgenden neuen Zeichen.  Es bietet die Möglichkeit neue, eindeutige ein Element in SharePoint und OneDrive für Unternehmen, da es geht davon aus, und nur mit decodierten URLs funktioniert behandeln. String-basierte Pfade zur Darstellung einer vollständig (absolut) oder teilweise (relativ) URL für eine Websitesammlung, Website, Dateien, Ordner oder andere Artifact und OneDrive für Unternehmen ersetzt. Um ordnungsgemäß % und # innerhalb von URLs zu unterstützen, müssen Sie die http://-basierten APIs zusammen mit decodiert URLs verwenden.
 
Http:// kann einfach erstellt werden, indem Sie eine statische Funktion aufrufen `ResourcePath.FromDecodedUrl(string)`. Der übergebene Wert kann durch Aufrufen der Eigenschaft DecodedUrl aus dem http://-Objekt zugegriffen werden. 
 
Für vorhandene Anrufe, die in einer URL-Zeichenfolge basierende dauern, Sie müssen ermitteln, ob der Pfad für den führende zu Zeichenfolge-basierte URL Anrufe wurden mit ver- oder entschlüsselte URLs bereitgestellt, und gibt an, ob die Pfade auch code Anker Hyperlinks zulässig (d. h.: #bookmark Ergänzungen auf oberen Rand der Datei-URL).

> Hinweis: Nicht einfach suchen und Ersetzen der vorhandene Verwendungen des String-basierte URL APIs mit `ResourcePath.FromDecodedUrl`.  Sie müssen URL ordnungsgemäß bestimmt und potenziell decodieren URLs vor zuerst mit der `ResourcePath.FromDecodedUrl(string)` API.

In Fällen, in dem eine Codepath führt zu einer Zeichenfolge-basierte SharePoint API-Aufruf verwendet **Decodiert URLs (z. B. "FY17 Report.docx")**, dann können Sie diesen anrufen mit einfach ersetzen `ResourcePath.FromDecodedUrl(string)` und die entsprechenden unten aufgeführten http://-Methoden.
 
Beachten Sie, dass in vielen Fällen, in dem Sie die URL aus SharePoint über APIs gelesen, der http:// auch angegeben wird, dieser Codemuster konsistenter, vornehmen, damit Sie die http:// anstelle der URL verwenden können.
 
Beachten Sie außerdem, dass diese Änderung auch für die SharePoint-REST-basierte von Anrufen sowie gilt.  Überprüfen Sie die unten, um diese neue APIs in REST-Beispiele finden Sie unter Szenarien.

## <a name="new-apis-that-are-based-on-resourcepath-and-supports--and-"></a>Neue APIs, die auf http:// basieren und unterstützt # und %
 
Im folgenden sind die neuen APIs, die wir eingeführt, um die vorhandenen APIs zur Unterstützung der # und % zu ersetzen. Wir die alte API und der neuen API nebeneinander für den Vergleich aufgelistet. Die Kernfunktionen dieser APIs nicht geändert, wie Sie die Position des Elements wurde geändert.
 
Die Dokumentation der neuen APIs kann unter https://msdn.microsoft.com/en-us/library/jj193041.aspx bezeichnet werden.  Haben wir die .net CSOM APIs unten aufgeführt, aber die neuen Methoden sind auch im entsprechenden Format in unseren CSOM JavaScript-Bibliotheken verfügbar.
 
**Assembly-Microsoft.SharePoint.Client.dll**

| Typ | Alte-Methode | New-Methode | 
|----------|-------------|------|
| Microsoft.SharePoint.SPList | AddItem(Microsoft.SharePoint.SPListItemCreationInformation) | AddItemUsingPath (SPListItemCreationInformationUsingPath-Parameter) | 
| Microsoft.SharePoint.SPFile | MoveTo (System.String, Microsoft.SharePoint.SPMoveOperations) | MoveToUsingPath (SPResourcePath NewPath, SPMoveOperations MoveOperations) | 
| Microsoft.SharePoint.SPFile | CopyTo (System.String, Boolean) | CopyToUsingPath (SPResourcePath NewPath, Bool Overwrite) | 
| Microsoft.SharePoint.SPFileCollection | GetByUrl(System.String) | GetByPath(SPResourcePath) | 
| Microsoft.SharePoint.SPFileCollection | Fügen Sie hinzu (System.String, Microsoft.SharePoint.SPTemplateFileType) | AddUsingPath (SPResourcePath, SPFileCollectionAddWithTemplateParameters) | 
| Microsoft.SharePoint.SPFolder | MoveTo(System.String) | MoveToUsingPath (SPResourcePath NewPath) | 
| Microsoft.SharePoint.SPFolder | AddSubFolder(System.String) | AddSubFolderUsingPath (SPResourcePath LeafPath) | 
| Microsoft.SharePoint.SPFolderCollection | GetByUrl(System.String) | GetByPath (SPResourcePath Pfad) | 
| Microsoft.SharePoint.SPFolderCollection | Add(System.String) | AddUsingPath (SPResourcePath Pfad, SPFolderCreationInformation-Parameter) | 
|  | AddWithOverwrite (String Url, Bool Overwrite) |  | 
| Microsoft.SharePoint.SPRemoteWeb | GetFileByServerRelativeUrl(System.String) | GetFileByServerRelativePath (SPResourcePath Pfad) | 
| Microsoft.SharePoint.SPWeb | GetList(System.String) | GetListUsingPath(SPResourcePath) | 
| Microsoft.SharePoint.SPWeb | GetListItem(System.String) | GetListItemUsingPath(SPResourcePath) | 


Die folgenden CSOM-Objekte zurückgeben http://-Eigenschaften, die in über APIs verwendet werden können. Obwohl die alte-Eigenschaft auch decodierten URLs zurückgegeben wird, wird die neue http://-Eigenschaft für Komfort, Einfachheit und Klarheit in Anrufe über APIs bereitgestellt.  Die einzige Ausnahme ist die SPFolder.WelcomePage-Eigenschaft, die früher codierten und uncodierten URLs zurückgegeben. Dies ist eindeutig jetzt über die WelcomePagePath-Eigenschaft zurückgegeben.

| Typ | Alte-Eigenschaft | New-Eigenschaft | 
|----------|-------------|------|
| Microsoft.SharePoint.SPList | DefaultViewUrl | DefaultViewPath | 
| Microsoft.SharePoint.SPList | DefaultEditFormUrl | DefaultEditFormPath | 
| Microsoft.SharePoint.SPList | DefaultNewFormUrl | DefaultNewFormPath | 
| Microsoft.SharePoint.SPList | DefaultDisplayFormUrl | DefaultDisplayFormPath | 
| Microsoft.SharePoint.SPAttachment | ServerRelativeUrl | ServerRelativePath | 
| Microsoft.SharePoint.SPFile | ServerRelativeUrl | ServerRelativePath | 
| Microsoft.SharePoint.SPFolder | ServerRelativeUrl | ServerRelativePath | 
| Microsoft.SharePoint.SPFolder | WelcomePage | WelcomePagePath / WelcomePageParameters | 
| Microsoft.SharePoint.SPView | ServerRelativeUrl | ServerRelativePath | 
| Microsoft.SharePoint.SPDocumentLibraryInformation | ServerRelativeUrl | ServerRelativePath | 


## <a name="existing-apis-that-are-not-ambiguous-about-the-url-formant-and-can-supports--and-"></a>Vorhandene APIs, die nicht über die URL-Tabelle mehrdeutige und kann unterstützt # und %
 
Die folgenden APIs akzeptieren nur ordnungsgemäß codierten URLs als Eingabe. Sie unterstützen auch unter-codierten URLs, solange die URL ohne jede Mehrdeutigkeit genutzt werden kann. In der Reihenfolge Wörter mindestens # oder % Zeichen im Pfad der URL % codiert werden soll. Diese APIs werden weiterhin die vorhandene Weise arbeiten. in der URL "#" wird als ein Fragmenttrennzeichen, aber nicht Teil der URL-Pfad behandelt.

| Typ | Alte-Eigenschaft | 
|----------|-------------|
| Microsoft.SharePoint.SPWeb |  GetFileByUrl(System.String) |
| Microsoft.SharePoint.SPWeb |  GetFileByWOPIFrameUrl(System.String) |
| Microsoft.SharePoint.SPWeb |  GetFileByLinkingUrl(System.String) |

Die folgenden C#-Eigenschaften werden zurückzugebenden System.Uri mit eindeutige Codierung für die Verwendung mit den oben genannten APIs hinzugefügt. Die ältere Variant-Wert mit der unter APIs zurückgegebenen decodiert URLs und inzwischen sie nie # enthalten oder Zeichen, die URL wurde nicht mehrdeutige. Vorwärts, wir nicht das decodierte Verhalten der älteren Varianten zum Codieren % und #-Zeichen im Pfad aufteilen möchten. Aus diesem Grund wurden neue APIs erstellt.
 
| Typ   |      Alte-Eigenschaft      |  New-Eigenschaft |
|----------|-------------|------|
| Microsoft.SharePoint.SPFile |  LinkingUrl | LinkingUri |
| Microsoft.SharePoint.SPFile |  ServerRedirectedEmbedUrl | ServerRedirectedEmbedUri |


## <a name="sample-code"></a>Beispielcode (engl.)

Es folgen einige Beispielcode für grundlegende Szenarios in CSOM:
 
- Hinzufügen einer Datei in einen Ordner (.net)

```C#
  ClientContext context = new ClientContext("http://site");
  Web web = context.Web;
  // Get the parent folder
  ResourcePath folderPath = ResourcePath.FromDecodedUrl("/Shared Documents");
  Folder parentFolder = web.GetFolderByServerRelativePath(folderPath);
 
  // Create the parameters used to add a file
  ResourcePath filePath = ResourcePath.FromDecodedUrl("/Shared Documents/hello world.txt");
  byte[] fileContent = System.Text.Encoding.UTF8.GetBytes("sample file content");
  FileCollectionAddParameters fileAddParameters = new FileCollectionAddParameters();
  fileAddParameters.Overwrite = true;
  using (MemoryStream contentStream = new MemoryStream(fileContent))
  {
    // Add a file
    Microsoft.SharePoint.Client.File addedFile = parentFolder.Files.AddUsingPath(filePath, fileAddParameters, contentStream);
 
    // Select properties of added file to inspect
    context.Load(addedFile, f => f.UniqueId, f1 => f1.ServerRelativePath);
 
    // Perform the actual operation
    context.ExecuteQuery();
 
    // Print the results
    Console.WriteLine(
      "Added File [UniqueId:{0}] [ServerRelativePath:{1}]",
      addedFile.UniqueId,
      addedFile.ServerRelativePath.DecodedUrl);
  }

```

- Fügen Sie einen untergeordneten Ordner in einen Ordner (.net)

```C#
    ClientContext context = new ClientContext("http://site");
    Web web = context.Web;
    // Get the parent folder
    ResourcePath folderPath = ResourcePath.FromDecodedUrl("/Shared Documents");
    Folder parentFolder = web.GetFolderByServerRelativePath(folderPath);
 
    // Create the parameters used to add a folder
    ResourcePath subFolderPath = ResourcePath.FromDecodedUrl("/Shared Documents/sub folder");
    FolderCollectionAddParameters folderAddParameters = new FolderCollectionAddParameters();
    folderAddParameters.Overwrite = true;
 
    // Add a sub folder
    Folder addedFolder = parentFolder.Folders.AddUsingPath(subFolderPath, folderAddParameters);
 
    // Select properties of added file to inspect
    context.Load(addedFolder, f => f.UniqueId, f1 => f1.ServerRelativePath);
 
    // Perform the actual operation
    context.ExecuteQuery();
 
    // Print the results
    Console.WriteLine(
        "Added Folder [UniqueId:{0}] [ServerRelativePath:{1}]",
        addedFolder.UniqueId,
        addedFolder.ServerRelativePath.DecodedUrl);
```

- Rufen Sie eine Datei im Web (.net)

```C#
    ClientContext context = new ClientContext("http://site");
    Web web = context.Web;
    // Get the file
    ResourcePath filePath = ResourcePath.FromDecodedUrl("/Shared Documents/hello world.txt");
    File file = web.GetFileByServerRelativePath(filePath);
 
    // Select properties of the file
    context.Load(file, f => f.UniqueId, f1 => f1.ServerRelativePath);
 
    // Perform the actual operation
    context.ExecuteQuery();
 
    // Print the results
    Console.WriteLine(
        "File Properties [UniqueId:{0}] [ServerRelativePath:{1}]",
        file.UniqueId,
        file.ServerRelativePath.DecodedUrl);
```

Es folgen einige Beispielcode für grundlegende Szenarios in REST:

- Abrufen von Ordnern

```
url: http://site url/_api/web/GetFolderByServerRelativePath(decodedUrl='folder name')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

- Ordner erstellen
 
```
url: http://site url/_api/web/Folders/AddUsingPath(decodedurl='/document library relative url/folder name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
 
```
 
- Abrufen von Dateien
 
```
url: http://site url/_api/web/GetFileByServerRelativePath(decodedUrl='folder name/file name')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
 
- Hinzufügen von Dateien
 
```
url: http://site url/_api/web/GetFolderByServerRelativePath(decodedUrl='folder name')/Files/AddStubUsingPath(decodedurl='testfile.txt')
methods: POST
Headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    Content-Length: length
 
```
