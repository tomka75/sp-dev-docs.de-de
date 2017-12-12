---
title: "Massenupload Dokumente Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 3dce2044fa25e5ec1f231c6511b2186f6c9191d8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="bulk-upload-documents-sample-add-in-for-sharepoint"></a><span data-ttu-id="c10fb-102">Massenupload Dokumente Beispiel-add-in für SharePoint</span><span class="sxs-lookup"><span data-stu-id="c10fb-102">Bulk upload documents sample add-in for SharePoint</span></span>

<span data-ttu-id="c10fb-103">Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie per Massenimport Hochladen von Dokumenten in Dokumentbibliotheken, einschließlich OneDrive für Unternehmen.</span><span class="sxs-lookup"><span data-stu-id="c10fb-103">As part of your Enterprise Content Management (ECM) strategy, you can bulk upload documents to document libraries, including OneDrive for Business.</span></span>
    
<span data-ttu-id="c10fb-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="c10fb-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

> [!NOTE] 
> <span data-ttu-id="c10fb-105">Im Beispiel lädt eine Datei in eine Dokumentbibliothek hoch.</span><span class="sxs-lookup"><span data-stu-id="c10fb-105">The sample uploads one file to a document library.</span></span> <span data-ttu-id="c10fb-106">Zum Hochladen mehrerer Dateien müssen Sie das Beispiel zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="c10fb-106">To upload multiple files, you'll need to extend the sample.</span></span>

<span data-ttu-id="c10fb-107">Dieses Add-In wird verwendet eine Konsolenanwendung zum Hochladen von Dateien mithilfe von REST-API-aufrufen.</span><span class="sxs-lookup"><span data-stu-id="c10fb-107">This add-in uses a console application to upload files by using REST API calls.</span></span> <span data-ttu-id="c10fb-108">Konfigurationseinstellungen werden in einem XML-Element und eine CSV-Datei angegeben.</span><span class="sxs-lookup"><span data-stu-id="c10fb-108">Configuration settings are specified in an XML and a CSV file.</span></span> <span data-ttu-id="c10fb-109">Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:</span><span class="sxs-lookup"><span data-stu-id="c10fb-109">Use this solution if you want to:</span></span>

- <span data-ttu-id="c10fb-110">Hochladen von Dateien in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="c10fb-110">Upload files to SharePoint Online.</span></span>
    
- <span data-ttu-id="c10fb-111">Migrieren zu Office 365 und Verwenden einer benutzerdefinierten Migrationstool, um Ihre Dateien zu verschieben.</span><span class="sxs-lookup"><span data-stu-id="c10fb-111">Migrate to Office 365 and use a custom migration tool to move your files.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c10fb-112">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="c10fb-112">Before you begin</span></span>
<span data-ttu-id="c10fb-113"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="c10fb-113"></span></span>

<span data-ttu-id="c10fb-114">Laden Sie Sie zuerst [Core.BulkDocumentUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="c10fb-114">To get started, download the  [Core.BulkDocumentUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="c10fb-115">Bevor Sie das Codebeispiel ausführen, folgendermaßen Sie vor:</span><span class="sxs-lookup"><span data-stu-id="c10fb-115">Before you run the code sample, do the following:</span></span>


1. <span data-ttu-id="c10fb-116">Bearbeiten Sie die Datei OneDriveUploader.xml mit den folgenden Informationen:</span><span class="sxs-lookup"><span data-stu-id="c10fb-116">Edit the OneDriveUploader.xml file with the following information:</span></span>
    
    - <span data-ttu-id="c10fb-117">Protokolldateien für der Speicherort, in dem Sie Text und CSV speichern möchten.</span><span class="sxs-lookup"><span data-stu-id="c10fb-117">The location where you want to save your text and CSV log files.</span></span>
    
    - <span data-ttu-id="c10fb-118">Der Pfad zu der CSV-Datei zur Zuordnung (beispielsweise C:\PnP\Samples\Core.BulkDocumentUploader\Input\SharePointSites.csv).</span><span class="sxs-lookup"><span data-stu-id="c10fb-118">The file path to your CSV mapping file (for example, C:\PnP\Samples\Core.BulkDocumentUploader\Input\SharePointSites.csv).</span></span>
    
    - <span data-ttu-id="c10fb-119">Die Position des Unternehmens-Richtliniendateien hochzuladenden (beispielsweise C:\PnP\Samples\Core.BulkDocumentUploader\Input\OneDriveFiles).</span><span class="sxs-lookup"><span data-stu-id="c10fb-119">The location of the company policy files to upload (for example, C:\PnP\Samples\Core.BulkDocumentUploader\Input\OneDriveFiles).</span></span>
    
    - <span data-ttu-id="c10fb-120">SharePoint Online-Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="c10fb-120">Your SharePoint Online credentials.</span></span>
    
    - <span data-ttu-id="c10fb-121">Die Aktion im Dokument (hochladen oder löschen) ausführen.</span><span class="sxs-lookup"><span data-stu-id="c10fb-121">The document action to perform (either upload or delete).</span></span>
    
    - <span data-ttu-id="c10fb-122">Der neue Dateiname auf die Datei angewendet wird, nachdem die Datei, in die Dokumentbibliothek (beispielsweise Unternehmen Richtlinie DOCUMENT.xlsx hochgeladen wurde).</span><span class="sxs-lookup"><span data-stu-id="c10fb-122">The new file name to apply to the file after the file is uploaded to the document library (for example, COMPANY POLICY DOCUMENT.xlsx).</span></span>
    
2. <span data-ttu-id="c10fb-123">In der Zuordnungsdatei SharePointSites.csv zum Hochladen von Dateien an die URL der Dokumentbibliothek und den Namen der hochzuladenden Datei Richtlinie Unternehmen aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="c10fb-123">In the SharePointSites.csv mapping file, list the document library URL to upload files to, and the name of the company policy file to upload.</span></span> 
    
3. <span data-ttu-id="c10fb-124">Fügen Sie den Dateipfad der OneDriveUploader.xml-Datei als Befehlszeilenargument.</span><span class="sxs-lookup"><span data-stu-id="c10fb-124">Add the file path of the OneDriveUploader.xml file as a command-line argument.</span></span> <span data-ttu-id="c10fb-125">Zu diesem Zweck öffnen Sie die Projekteigenschaften Core.BulkDocumentUploader im Projektmappen-Explorer, und wählen Sie dann **Eigenschaften** > **Debuggen**, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="c10fb-125">To do this, open the Core.BulkDocumentUploader project properties in Solution Explorer, and then choose  **Properties** > **Debug**, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="c10fb-126">**Abbildung 1. OneDriveUploader.xml festlegen als Befehlszeilenargument in den Projekteigenschaften**</span><span class="sxs-lookup"><span data-stu-id="c10fb-126">**Figure 1. Setting OneDriveUploader.xml as a command-line argument in the project properties**</span></span>

    ![Screenshot der Eigenschaftenbereich Core.BulkDocumentUploader mit "Debug" hervorgehoben.](media/f1d950b4-82be-4800-9ccc-07fa2c739fad.png)


## <a name="using-the-corebulkdocumentuploader-sample-app"></a><span data-ttu-id="c10fb-128">Verwenden die Core.BulkDocumentUploader Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="c10fb-128">Using the Core.BulkDocumentUploader sample app</span></span>
<span data-ttu-id="c10fb-129"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="c10fb-129"></span></span>

<span data-ttu-id="c10fb-130">Aus der **Main** -Methode in Program.cs Ruft die **RecurseActions** -Methode die **Run** -Methode in OneDriveMapper.cs.</span><span class="sxs-lookup"><span data-stu-id="c10fb-130">From the  **Main** method in Program.cs, the **RecurseActions** method calls the **Run** method in OneDriveMapper.cs.</span></span> <span data-ttu-id="c10fb-131">Die **Run** -Methode ruft den Speicherort der Datei zum Hochladen von SharePointSites.csv ab und ruft dann die **IterateCollection** -Methode.</span><span class="sxs-lookup"><span data-stu-id="c10fb-131">The **Run** method gets the location of the file to upload from SharePointSites.csv, and then calls the **IterateCollection** method.</span></span>

> [!NOTE] 
> <span data-ttu-id="c10fb-132">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="c10fb-132">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
public override void Run(BaseAction parentAction, DateTime CurrentTime, LogHelper logger)
        {
            CsvProcessor csvProcessor = new CsvProcessor();

            logger.LogVerbose(string.Format("Attempting to read mapping CSV file '{0}'", this.UserMappingCSVFile));

            using (StreamReader reader = new StreamReader(this.UserMappingCSVFile))
            {
                csvProcessor.Execute(reader, (entries, y) => { IterateCollection(entries, logger); }, logger);
            }
        }

```

<span data-ttu-id="c10fb-133">Die Datei SharePointSite.csv enthält eine Datei zum Hochladen und der Dokumentbibliothek, um diese Datei zum Hochladen.</span><span class="sxs-lookup"><span data-stu-id="c10fb-133">The SharePointSite.csv file lists a file to upload and the document library to upload that file to.</span></span> <span data-ttu-id="c10fb-134">Die **IterateCollection** -Methode führt dann Folgendes ein, um die Datei in die Dokumentbibliothek hoch:</span><span class="sxs-lookup"><span data-stu-id="c10fb-134">The  **IterateCollection** method then does the following to upload the file to the document library:</span></span>

1. <span data-ttu-id="c10fb-135">Ruft die hochzuladende Datei ab.</span><span class="sxs-lookup"><span data-stu-id="c10fb-135">Gets the file to upload.</span></span> 
    
2. <span data-ttu-id="c10fb-136">Stellt sicher, dass der Benutzer über Berechtigungen zum Hinzufügen von Elementen verfügt.</span><span class="sxs-lookup"><span data-stu-id="c10fb-136">Ensures that the user has permissions to add items.</span></span>
    
3. <span data-ttu-id="c10fb-137">Das **HttpWebRequest** -Objekt erstellt mit den Authentifizierungscookie, die REST-Zeichenfolge-Anforderung zum Hochladen des Dokuments und die HTTP-Anforderung Aktion-Methode.</span><span class="sxs-lookup"><span data-stu-id="c10fb-137">Creates the  **HttpWebRequest** object with the authentication cookie, the REST string request to upload the document, and the HTTP request action method.</span></span>
    
4. <span data-ttu-id="c10fb-138">Führt die Dateien hochladen.</span><span class="sxs-lookup"><span data-stu-id="c10fb-138">Performs the file upload.</span></span>

> [!NOTE] 
> <span data-ttu-id="c10fb-139">Der Dateiname wird mit dem Wert des **FileUploadName** in OneDriveUploader.xml angegebenen überschrieben.</span><span class="sxs-lookup"><span data-stu-id="c10fb-139">The file name is overwritten with the value of  **FileUploadName** specified in OneDriveUploader.xml.</span></span>

```C#
public override void IterateCollection(Collection<string> entries, LogHelper logger)
        {
            Stopwatch IterationSW = new Stopwatch();
            IterationSW.Start();

            logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "Establishing context object to: '{0}'", entries[this.SiteIndex]));

            try
            {
                // Use the context of the current iteration URL for current user item.
                using (ClientContext context = new ClientContext(entries[this.SiteIndex]))
                {
                    using (SecureString password = new SecureString())
                    {
                        foreach (char c in this.Password.ToCharArray())
                        {
                            password.AppendChar(c);
                        }

                        context.Credentials = new SharePointOnlineCredentials(this.UserName, password);

                        // Get the file to upload from the directory.
                        FileInfo theFileToUpload = new FileInfo(Path.Combine(this.DirectoryLocation + "\\", entries[this.FileIndex] + ".xlsx"));

                        logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "Attempting to {0} file {1}", this.DocumentAction, theFileToUpload));

                        // Ensure that the account has permissions to access.
                        BasePermissions perm = new BasePermissions();
                        perm.Set(PermissionKind.AddListItems);

                        ConditionalScope scope = new ConditionalScope(context, () => context.Web.DoesUserHavePermissions(perm).Value);

                        using(scope.StartScope())
                        {
                            Stopwatch tempSW = new Stopwatch();
                            tempSW.Start();

                            int success = 0;

                            while(tempSW.Elapsed.TotalSeconds < 20)
                            {
                                var digest = context.GetFormDigestDirect();

                                string cookie = ((SharePointOnlineCredentials)context.Credentials).GetAuthenticationCookie(new Uri(entries[this.SiteIndex])).TrimStart("SPOIDCRL=".ToCharArray());

                                using (Stream s = theFileToUpload.OpenRead())
                                {
                                    // Define REST string request to upload document to context. This string specifies the Documents folder, but you can specify another document library.
                                    string theTargetUri = string.Format(CultureInfo.CurrentCulture, "{0}/_api/web/lists/getByTitle('Documents')/RootFolder/Files/add(url='{1}',overwrite='true')?", entries[this.SiteIndex], this.FileUploadName);

                                    // Define REST HTTP request object.
                                    HttpWebRequest SPORequest = (HttpWebRequest)HttpWebRequest.Create(theTargetUri);

                                    // Define HTTP request action method.
                                    if (this.DocumentAction == "Upload")
                                    {
                                        SPORequest.Method = "POST";
                                    }
                                    else if (this.DocumentAction == "Delete")
                                    {
                                        SPORequest.Method = "DELETE";
                                    }
                                    else
                                    {
                                        logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "There was a problem with the HTTP request in DocumentAction attribute of XML file"));
                                        throw new Exception("The HTTP Request operation is not supported, please check the value of DocumentAction in the XML file");
                                    }

                                    // Build out additional HTTP request details.
                                    SPORequest.Accept = "application/json;odata=verbose";
                                    SPORequest.Headers.Add("X-RequestDigest", digest.DigestValue);
                                    SPORequest.ContentLength = s.Length;
                                    SPORequest.ContentType = "application/octet-stream";

                                    // Handle authentication to context through cookie.
                                    SPORequest.CookieContainer = new CookieContainer();
                                    SPORequest.CookieContainer.Add(new Cookie("SPOIDCRL", cookie, string.Empty, new Uri(entries[this.SiteIndex]).Authority));

                                    // Perform file upload/deletion.
                                    using (Stream requestStream = SPORequest.GetRequestStream())
                                    {
                                        s.CopyTo(requestStream);
                                    }

                                    // Get HTTP response to determine success of operation.
                                    HttpWebResponse SPOResponse = (HttpWebResponse)SPORequest.GetResponse();

                                    logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "Successfully '{0}' file {1}", this.DocumentAction, theFileToUpload));
                                    logger.LogOutcome(entries[this.SiteIndex], "SUCCCESS");

                                    success = 1;

                                    // Dispose of the HTTP response.
                                    SPOResponse.Close();

                                    break;
                                }
                                                       
                            }

                            tempSW.Stop();

                            if (success != 1)
                            {
                                throw new Exception("The HTTP Request operation exceeded the timeout of 20 seconds");
                            }

                        }
                    }
                }

            }
            catch(Exception ex)
            {
                logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "There was an issue performing '{0}' on to the URL '{1}' with exception: {2}", this.DocumentAction, entries[this.SiteIndex], ex.Message));
                logger.LogOutcome(entries[this.SiteIndex], "FAILURE");
            }
            finally
            {
                IterationSW.Stop();
                logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "Completed processing URL:'{0}' in {1} seconds", entries[this.SiteIndex], IterationSW.ElapsedMilliseconds/1000));
            }
        }

```

## <a name="see-also"></a><span data-ttu-id="c10fb-140">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c10fb-140">See also</span></span>
<span data-ttu-id="c10fb-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c10fb-141"></span></span>

-  [<span data-ttu-id="c10fb-142">Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="c10fb-142">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)   
-  [<span data-ttu-id="c10fb-143">Core.LargeFileUpload-Beispiel</span><span class="sxs-lookup"><span data-stu-id="c10fb-143">Core.LargeFileUpload sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)
    
