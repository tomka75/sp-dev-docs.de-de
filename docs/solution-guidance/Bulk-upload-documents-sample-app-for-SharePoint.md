---
title: "Massenupload Dokumente Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 3dce2044fa25e5ec1f231c6511b2186f6c9191d8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="bulk-upload-documents-sample-add-in-for-sharepoint"></a>Massenupload Dokumente Beispiel-add-in für SharePoint

Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie per Massenimport Hochladen von Dokumenten in Dokumentbibliotheken, einschließlich OneDrive für Unternehmen.
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

> [!NOTE] 
> Im Beispiel lädt eine Datei in eine Dokumentbibliothek hoch. Zum Hochladen mehrerer Dateien müssen Sie das Beispiel zu erweitern.

Dieses Add-In wird verwendet eine Konsolenanwendung zum Hochladen von Dateien mithilfe von REST-API-aufrufen. Konfigurationseinstellungen werden in einem XML-Element und eine CSV-Datei angegeben. Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:

- Hochladen von Dateien in SharePoint Online.
    
- Migrieren zu Office 365 und Verwenden einer benutzerdefinierten Migrationstool, um Ihre Dateien zu verschieben.

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.BulkDocumentUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Bevor Sie das Codebeispiel ausführen, folgendermaßen Sie vor:


1. Bearbeiten Sie die Datei OneDriveUploader.xml mit den folgenden Informationen:
    
    - Protokolldateien für der Speicherort, in dem Sie Text und CSV speichern möchten.
    
    - Der Pfad zu der CSV-Datei zur Zuordnung (beispielsweise C:\PnP\Samples\Core.BulkDocumentUploader\Input\SharePointSites.csv).
    
    - Die Position des Unternehmens-Richtliniendateien hochzuladenden (beispielsweise C:\PnP\Samples\Core.BulkDocumentUploader\Input\OneDriveFiles).
    
    - SharePoint Online-Anmeldeinformationen.
    
    - Die Aktion im Dokument (hochladen oder löschen) ausführen.
    
    - Der neue Dateiname auf die Datei angewendet wird, nachdem die Datei, in die Dokumentbibliothek (beispielsweise Unternehmen Richtlinie DOCUMENT.xlsx hochgeladen wurde).
    
2. In der Zuordnungsdatei SharePointSites.csv zum Hochladen von Dateien an die URL der Dokumentbibliothek und den Namen der hochzuladenden Datei Richtlinie Unternehmen aufgelistet. 
    
3. Fügen Sie den Dateipfad der OneDriveUploader.xml-Datei als Befehlszeilenargument. Zu diesem Zweck öffnen Sie die Projekteigenschaften Core.BulkDocumentUploader im Projektmappen-Explorer, und wählen Sie dann **Eigenschaften** > **Debuggen**, wie in Abbildung 1 dargestellt.
    
    **Abbildung 1. OneDriveUploader.xml festlegen als Befehlszeilenargument in den Projekteigenschaften**

    ![Screenshot der Eigenschaftenbereich Core.BulkDocumentUploader mit "Debug" hervorgehoben.](media/f1d950b4-82be-4800-9ccc-07fa2c739fad.png)


## <a name="using-the-corebulkdocumentuploader-sample-app"></a>Verwenden die Core.BulkDocumentUploader Beispiel-app
<a name="sectionSection1"> </a>

Aus der **Main** -Methode in Program.cs Ruft die **RecurseActions** -Methode die **Run** -Methode in OneDriveMapper.cs. Die **Run** -Methode ruft den Speicherort der Datei zum Hochladen von SharePointSites.csv ab und ruft dann die **IterateCollection** -Methode.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

Die Datei SharePointSite.csv enthält eine Datei zum Hochladen und der Dokumentbibliothek, um diese Datei zum Hochladen. Die **IterateCollection** -Methode führt dann Folgendes ein, um die Datei in die Dokumentbibliothek hoch:

1. Ruft die hochzuladende Datei ab. 
    
2. Stellt sicher, dass der Benutzer über Berechtigungen zum Hinzufügen von Elementen verfügt.
    
3. Das **HttpWebRequest** -Objekt erstellt mit den Authentifizierungscookie, die REST-Zeichenfolge-Anforderung zum Hochladen des Dokuments und die HTTP-Anforderung Aktion-Methode.
    
4. Führt die Dateien hochladen.

> [!NOTE] 
> Der Dateiname wird mit dem Wert des **FileUploadName** in OneDriveUploader.xml angegebenen überschrieben.

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

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)   
-  [Core.LargeFileUpload-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)
    
