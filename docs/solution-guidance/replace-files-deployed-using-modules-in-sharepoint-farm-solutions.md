---
title: "Ersetzen Sie Dateien bereitgestellt, Verwendung von Modulen in SharePoint-farmlösungen"
ms.date: 11/03/2017
ms.openlocfilehash: 3ea55aa39c86acc513ce65954e9ed5cf2195902b
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="replace-files-deployed-using-modules-in-sharepoint-farm-solutions"></a>Ersetzen Sie Dateien bereitgestellt, Verwendung von Modulen in SharePoint-farmlösungen

Ersetzen Sie Dateien wie Masterseiten und Seitenlayouts in SharePoint, die Verwendung von Modulen in farmlösungen durch Hochladen und Aktualisieren der Verweise von neuen Dateien bereitgestellt wurden.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Wenn Sie Dateien mithilfe von Modulen deklarativ in farmlösungen bereitgestellt, erfahren Sie, wie sie in neue Lösungen umgewandelt, die Verweise auf Dateien aktualisiert und bieten eine ähnliche Funktionalität mithilfe des Clientobjektmodells (CSOM). In der Vergangenheit wurden Module zur Bereitstellung von Dateien wie etwa Gestaltungsvorlagen und Seitenlayouts verwendet. In diesem Artikel wird beschrieben, wie die Transformation zu verwenden:

1. Hochladen von neuen Gestaltungsvorlagen und Seitenlayouts.
    
2. Aktualisieren der Verweise, um die neue Masterseiten und Seitenlayoutdateien verwenden.
    
Verwenden Sie diese Transformation verarbeiten, wenn:

- Ihrer vorhandenen farmlösungen verwendet Module zum Bereitstellen von Dateien.
    
-  Sie möchten Gestaltungsvorlagen und Seitenlayouts in farmlösungen mit neuen Gestaltungsvorlagen und Seitenlayouts zu ersetzen, sodass sie mit SharePoint Online migriert werden können.
    
- Sie haben Dokumentinhaltstypen auf Gestaltungsvorlagen oder in Seitenlayouts in Ihrer farmlösung deklarativ festgelegt.

**Wichtig:**  Farmlösungen können nicht mit SharePoint Online migriert werden. Durch die Techniken und den Code in diesem Artikel beschriebenen anwenden, können Sie eine neue Lösung mit ähnlicher Funktionalität, den Ihre farmlösungen bereitstellen, Update Verweise auf Dateien, erstellen, und klicken Sie dann die neue Lösung mit SharePoint Online bereitgestellt werden kann. Klicken Sie dann können Sie das Feature deaktivieren und die vorherige farmlösung zurückgezogen. Der Code in diesem Artikel erfordert zusätzlichen Code, um eine voll funktionsfähige Lösung bereitzustellen. In diesem Artikel erläutern beispielsweise nicht wie Authentifizierung mit Office 365, Implementierung Ausnahmebehandlung erforderlich, und so weiter. Zusätzliche Codebeispiele finden Sie unter [Office 365 Developer Mustern und Methoden Projekt](https://github.com/SharePoint/PnP).

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Idealerweise sollten Sie überprüfen Ihrer vorhandenen farmlösungen, erfahren Sie mehr über die in diesem Artikel beschriebenen Verfahren und dann planen, wie diese Techniken für Ihre Szenarien gelten. Wenn Sie mit farmlösungen vertraut sind, oder nicht über eine vorhandene farmlösung verfügen entwickelt, kann es für Sie hilfreich sein:

- Laden Sie die [Projektmappe Contoso.Intranet](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet). Überprüfen Sie Übung 1 [Ersetzung von Dateien über Modulen in voll vertrauenswürdig Lösungen bereitgestellt](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-1%20Replacement%20of%20files%20deployed%20via%20Modules/Lab.md) , um eine schnelle Grundlegendes zur Seite wie master Pages und Layouts in der Vergangenheit erstellt wurden möglicherweise erhalten möchten.
    
- Informationen Sie zu farmlösungen. Weitere Informationen finden Sie unter [Übersicht über SharePoint 2010-Architekturen](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) und[Farmlösungen in SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).
    
Aktivieren Sie Sie vor dem Ausführen Ihrer Codebeispiel die Veröffentlichungsfeatures für die Websitesammlung und Website mit den folgenden Verfahren.

1. So aktivieren Sie das Feature **SharePoint Server-Veröffentlichungsinfrastruktur** für die Websitesammlung:
    
    1. Öffnen Sie die SharePoint-Website, und navigieren Sie zu **Einstellungen** > **Websiteeinstellungen**.
    
    2. Wählen Sie in der **Verwaltung der Websitesammlung** **Websitesammlungs-Features**.
    
    3. Wählen Sie auf **SharePoint Server-Veröffentlichungsinfrastruktur** **Aktivieren**.
    
2. So aktivieren Sie das Feature **SharePoint Server-Veröffentlichung** auf der Website:
    
    1. Öffnen Sie die SharePoint-Website, und navigieren Sie zu **Einstellungen** > **Websiteeinstellungen**.
    
    2. Wählen Sie in der Liste **Websiteaktionen** **Websitefeatures verwalten**.
    
    3. Wählen Sie auf **SharePoint Server-Veröffentlichung** **Aktivieren**.
    
So richten Visual Studio-Projekt

1. Laden Sie das [Beispielprojekt](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/Student.zip). Wählen Sie **Ansicht unformatierte** Downloadvorgang das Beispielprojekt, extrahieren Sie die Dateien aus der Zipdatei, und navigieren Sie zu dem Ordner Module9/ModuleReplacement.
    
2. Öffnen Sie ModuleReplacement.sln.
    
3. Öffnen Sie settings.xml. Überprüfen Sie und aktualisieren Sie die folgenden Attribute, um Ihre Anforderungen erfüllen:
    
    1.  **Masterpage** Element - verwendet das Attribut **File** an die neue Masterseite für die Bereitstellung auf den Gestaltungsvorlagenkatalog und das Attribut **ersetzt** die vorhandene Gestaltungsvorlage im Gestaltungsvorlagenkatalog gibt.
    
    2.  **PageLayout** -Element - verwendet das Attribut **File** , um die neue Seite Layout-Datei anzugeben, das Attribut **ersetzt** die vorhandene Seite Layout-Datei an und mehrere andere Attribute, um zusätzliche Seite Layoutinformationen anzugeben.

    **Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

    ```XML
        <?xml version="1.0" encoding="utf-8" ?>
        <branding>
          <masterPages>
               <masterPage file="contoso_app.master" replaces="contoso.master"/>
          </masterPages>
          <pageLayouts>
               <pageLayout file="ContosoWelcomeLinksApp.aspx" replaces="ContosoWelcomeLinks.aspx" title="Contoso Welcome Links add-in" associatedContentTypeName="Contoso Web Page" defaultLayout="true" />
          </pageLayouts>
        </branding>
    
    ```

4. In MasterPageGalleryFiles.cs definieren die Klassen **MasterPageGalleryFile** und **LayoutFile** -Geschäftsobjekte, in denen Informationen zu den neuen Gestaltungsvorlagen und Seitenlayouts in SharePoint hochgeladen werden gespeichert.

## <a name="upload-and-update-references-to-master-pages"></a>Hochladen Sie und aktualisieren Sie der Verweise auf Gestaltungsvorlagen

Hochladen und Aktualisieren der Verweise auf die neuen Masterseiten auf Ihrer SharePoint-Website:

1. Fügen Sie in der Datei Program.cs die folgenden **using** -Anweisung hinzu.
    
    ```C#
        using System.Security;
    ```

2. Fügen Sie in der Datei Program.cs die folgenden Methoden zum Ausführen der Authentifizierung zu Office 365.
    
  ```C#
  static SecureString GetPassword()
        {
            SecureString sStrPwd = new SecureString();
            try
            {
                Console.Write("Password: ");

                for (ConsoleKeyInfo keyInfo = Console.ReadKey(true); keyInfo.Key != ConsoleKey.Enter; keyInfo = Console.ReadKey(true))
                {
                    if (keyInfo.Key == ConsoleKey.Backspace)
                    {
                        if (sStrPwd.Length > 0)
                        {
                            sStrPwd.RemoveAt(sStrPwd.Length - 1);
                            Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                            Console.Write(" ");
                            Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                        }
                    }
                    else if (keyInfo.Key != ConsoleKey.Enter)
                    {
                        Console.Write("*");
                        sStrPwd.AppendChar(keyInfo.KeyChar);
                    }

                }
                Console.WriteLine("");
            }
            catch (Exception e)
            {
                sStrPwd = null;
                Console.WriteLine(e.Message);
            }

            return sStrPwd;
        }

        static string GetUserName()
        {
            string strUserName = string.Empty;
            try
            {
                Console.Write("Username: ");
                strUserName = Console.ReadLine();
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
                strUserName = string.Empty;
            }
            return strUserName;
        }
  ```

3. Fügen Sie den folgenden Code in Program.cs der **Main** -Methode, die die folgenden Aufgaben ausführt:
    
    1. Lädt die Datei settings.xml.
    
    2. Ruft einen Verweis auf den Gestaltungsvorlagenkatalog mithilfe von [GetCatalog](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.getcatalog.aspx)(116). Masterseiten werden in den Gestaltungsvorlagenkatalog hochgeladen. Der Bezeichner der Listenvorlage der Gestaltungsvorlagenkatalog ist 116. Weitere Informationen finden Sie unter [ListTemplate-Element (Website)](https://msdn.microsoft.com/library/ms439434.aspx). Weitere Informationen über den Gestaltungsvorlagenkatalog werden geladen, einschließlich der Verwendung von [List.ContentTypes](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.contenttypes.aspx) zum Abrufen der Inhaltstypen Gestaltungsvorlagenkatalog zugeordnet.
    
    3. Lädt die Eigenschaften des einschließlich Web.ContentTypes, Web.MasterUrl und Web.CustomMasterUrl Web-Objekts.
    
    4. **ParentMasterPageContentTypeId** festgelegt auf den Inhaltstyp-ID von Masterseiten. Weitere Informationen finden Sie unter[Base Content Type Hierarchy](https://msdn.microsoft.com/library/ms452896%28v=office.14%29.aspx).
    
    5. Ruft den Inhaltstyp der Gestaltungsvorlagen aus den Gestaltungsvorlagenkatalog ab. Dieser Inhaltstyp wird verwendet, um den Inhaltstyp der neuen Gestaltungsvorlage weiter unten in diesem Artikel festlegen. 
    
    ```C#
    static void Main(string[] args)
        { 
            string userName = GetUserName();
            SecureString pwd = GetPassword();
            
         // End program if no credentials were entered.
            if (string.IsNullOrEmpty(userName) || (pwd == null))
              return;
                                   
            using (var clientContext = new ClientContext("http://sharepoint.contoso.com"))
            {
                            
                clientContext.AuthenticationMode = ClientAuthenticationMode.Default;
                clientContext.Credentials = new SharePointOnlineCredentials(userName, pwd);
                    
                XDocument settings = XDocument.Load("settings.xml");
    
                // Get a reference to the master page gallery which will be used to upload new master pages. 
             
                Web web = clientContext.Web;
                List gallery = web.GetCatalog(116);
                Folder folder = gallery.RootFolder;
            
                 // Load additional master page gallery properties.
                clientContext.Load(folder);
                clientContext.Load(gallery,
                                    g => g.ContentTypes,
                                    g => g.RootFolder.ServerRelativeUrl);
        
                // Load the content types and master page information from the web.
                clientContext.Load(web,
                                    w => w.ContentTypes,
                                    w => w.MasterUrl,
                                    w => w.CustomMasterUrl);
                clientContext.ExecuteQuery();
    
                // Get the content type for the master page from the master page gallery using the content type ID for masterpages (0x010105).
                const string parentMasterPageContentTypeId = "0x010105";  
                ContentType masterPageContentType = gallery.ContentTypes.FirstOrDefault(ct => ct.StringId.StartsWith(parentMasterPageContentTypeId));
                UploadAndSetMasterPages(web, folder, clientContext, settings, masterPageContentType.StringId);
                             
            }
    
        }
    ```

4. Fügen Sie in Program.cs die **UploadAndSetMasterPages** -Methode, die eine Liste von Geschäftsobjekten durch **MasterPageGalleryFile** erstellt:
    
    1. Alle im settings.xml definierten **MasterPage** Elemente lesen.
    
    2. Laden für jedes **MasterPage** -Element, das eine Gestaltungsvorlage für SharePoint hochladen angibt, die Attributwerte in einem Geschäftsobjekt **MasterPageGalleryFile** .
    
    3. Für jedes **MasterPageGalleryFile** Business-Objekt in der Liste **UploadAndSetMasterPage**anrufen.
    
    ```C#
        
    private static void UploadAndSetMasterPages(Web web, Folder folder, ClientContext clientContext, XDocument settings, string contentTypeId)
    {
        IList<MasterPageGalleryFile> masterPages = (from m in settings.Descendants("masterPage")
                                                    select new MasterPageGalleryFile
                                                    {
                                                        File = (string)m.Attribute("file"),
                                                        Replaces = (string)m.Attribute("replaces"),
                                                        ContentTypeId = contentTypeId
                                                    }).ToList();
        foreach (MasterPageGalleryFile masterPage in masterPages)
        {
            UploadAndSetMasterPage(web, folder, clientContext, masterPage);
        }
    }
    ```

5. Fügen Sie in Program.cs die **UploadAndSetMasterPage** -Methode, die folgenden Aufgaben ausgeführt werden:
    
    1. Checkt die Gestaltungsvorlage.
    
    2. Lädt die neue Datei mit [komplexer FileCreationInformation](https://msdn.microsoft.com/library/microsoft.sharepoint.client.filecreationinformation.aspx)hoch.
    
    3. Ruft das Listenelement mit der neu hochgeladene Datei verknüpft ist.
    
    4. Verschiedene Eigenschaften festgelegt für das Listenelement, einschließlich Festlegen der Inhaltstyp-ID des Listenelements auf den Inhaltstyp-ID der Masterseite.
    
    5. Überprüft und genehmigt die neue Masterseite veröffentlicht. 
    
    6. Wenn die Masterseite für die aktuelle Website oder benutzerdefinierte Gestaltungsvorlage URL auf die alte Gestaltungsvorlage festgelegt ist, aktualisiert [Web.MasterUrl](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.masterurl.aspx) oder[Web.CustomMasterUrl](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.custommasterurl.aspx) , um die URL der neu hochgeladene Masterseite verwenden.
    
    ```C#
      private static void UploadAndSetMasterPage(Web web, Folder folder, ClientContext clientContext, MasterPageGalleryFile masterPage)
    {
        using (var fileReadingStream = System.IO.File.OpenRead(masterPage.File))
        {
            // If necessary, ensure that the master page is checked out.
            PublishingHelper.CheckOutFile(web, masterPage.File, folder.ServerRelativeUrl);
    
    // Use the FileCreationInformation class to upload the new file.
            var fileInfo = new FileCreationInformation();
            fileInfo.ContentStream = fileReadingStream;
            fileInfo.Overwrite = true;
            fileInfo.Url = masterPage.File;
            File file = folder.Files.Add(fileInfo);
    
    // Get the list item associated with the newly uploaded master page file.
            ListItem item = file.ListItemAllFields;
            clientContext.Load(file.ListItemAllFields);
            clientContext.Load(file,
                                f => f.CheckOutType,
                                f => f.Level,
                                f => f.ServerRelativeUrl);
            clientContext.ExecuteQuery();
    
    item["ContentTypeId"] = masterPage.ContentTypeId;
            item["UIVersion"] = Convert.ToString(15);
            item["MasterPageDescription"] = "Master Page Uploaded using CSOM";
            item.Update();
            clientContext.ExecuteQuery();
    
    // If necessary, check in, publish, and approve the new master page file. 
            PublishingHelper.CheckInPublishAndApproveFile(file);
    
    // On the current site, update the master page references to use the new master page. 
            if (web.MasterUrl.EndsWith("/" + masterPage.Replaces))
            {
                web.MasterUrl = file.ServerRelativeUrl;
            }
            if (web.CustomMasterUrl.EndsWith("/" + masterPage.Replaces))
            {
                web.CustomMasterUrl = file.ServerRelativeUrl;
            }
            web.Update();
            clientContext.ExecuteQuery();
        }
    }
    ```

## <a name="upload-and-update-references-to-page-layouts"></a>Hochladen Sie und aktualisieren Sie der Verweise auf Seitenlayouts

**Hinweis:**  Die Codebeispiele in diesem Abschnitt erstellen Sie auf die Codebeispiele im vorherigen Abschnitt dieses Artikels. 

Um Seitenlayouts zu ersetzen, die Verwendung von Modulen in farmlösungen bereitgestellt wurden, Hochladen Sie und aktualisieren Sie der Verweise auf die neue Seitenlayoutdateien durch verwenden:


1. Aktualisieren der **Main** -Methode durch den folgenden Code. Dieser Code enthält zusätzliche Schritte zum Hochladen und Aktualisieren der Verweise auf Seitenlayoutdateien, einschließlich:
    
    1. Wenn Sie auf das Seitenlayout Inhaltstyp-ID **ParentPageLayoutContentTypeId** festlegen
    
    2.  Abrufen eines Inhaltstyps, der mit **ParentPageLayoutContentTypeId** aus den Gestaltungsvorlagenkatalog übereinstimmt.
    
    3. **UploadPageLayoutsAndUpdateReferences**aufrufen.
    
    ```C#
                static void Main(string[] args)
        { 
            string userName = GetUserName();
            SecureString pwd = GetPassword();
            
         // End program if no credentials were entered.
            if (string.IsNullOrEmpty(userName) || (pwd == null))
              return;
                                   
            using (var clientContext = new ClientContext("http://sharepoint.contoso.com"))
            {
                            
                clientContext.AuthenticationMode = ClientAuthenticationMode.Default;
                clientContext.Credentials = new SharePointOnlineCredentials(userName, pwd);
                    
                XDocument settings = XDocument.Load("settings.xml");
    
                // Get a reference to the master page gallery, which will be used to upload new master pages. 
             
                Web web = clientContext.Web;
                List gallery = web.GetCatalog(116);
                Folder folder = gallery.RootFolder;
            
                 // Load additional master page gallery properties. 
                clientContext.Load(folder);
                clientContext.Load(gallery,
                                    g => g.ContentTypes,
                                    g => g.RootFolder.ServerRelativeUrl);
        
                // Load the content types and master page information from the web.
                clientContext.Load(web,
                                    w => w.ContentTypes,
                                    w => w.MasterUrl,
                                    w => w.CustomMasterUrl);
                clientContext.ExecuteQuery();
    
                // Get the content type for the master page from the master page gallery using the content type ID for masterpages (0x010105).
                const string parentMasterPageContentTypeId = "0x010105";  
                ContentType masterPageContentType = gallery.ContentTypes.FirstOrDefault(ct => ct.StringId.StartsWith(parentMasterPageContentTypeId));
                UploadAndSetMasterPages(web, folder, clientContext, settings, masterPageContentType.StringId);
                             
    
               // Get the content type ID for the page layout, and then update references to the page layouts.
               const string parentPageLayoutContentTypeId = "0x01010007FF3E057FA8AB4AA42FCB67B453FFC100E214EEE741181F4E9F7ACC43278EE811"; 
               ContentType pageLayoutContentType = gallery.ContentTypes.FirstOrDefault(ct => ct.StringId.StartsWith(parentPageLayoutContentTypeId));
               UploadPageLayoutsAndUpdateReferences(web, folder, clientContext, settings, pageLayoutContentType.StringId);
            }
    
        }
    ```

2. Fügen Sie in Program.cs die **UploadPageLayoutsAndUpdateReferences** -Methode, die folgenden Schritte ausführt:
    
    1. Liest die Seite Ersatz Layoutinformationen settings.xml **Pagelayout** Elemente lesen und speichern die Seite Ersatz Layoutinformationen im **LayoutFile** von Geschäftsobjekten zu einer Liste aller Business-Objekte hinzufügen.
    
    2. Für jede Seitenlayout ersetzen:
    
        1. Abfragen geben die Websiteinhaltstypen mithilfe von [Web.ContentTypes](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.contenttypes.aspx) finden Sie eine entsprechende Ressourcen, in dem der Name des Inhaltstyps für die Website der **AssociatedContentTypeName** in settings.xml für das neue Seitenlayout angegebenen gleich ist.
    
        2. Ruft die **UploadPageLayout**.
    
        3. Ruft die **UpdatePages** zum Aktualisieren vorhandener Seiten, um die neuen Seitenlayouts zu verwenden.

  ```C#
        private static void UploadPageLayoutsAndUpdateReferences(Web web, Folder folder, ClientContext clientContext, XDocument settings, string contentTypeId)
{
    // Read the replacement settings stored in pageLayout elements in settings.xml.
    IList<LayoutFile> pageLayouts = (from m in settings.Descendants("pageLayout")
                                 select new LayoutFile
                                 {
                                     File = (string)m.Attribute("file"),
                                     Replaces = (string)m.Attribute("replaces"),
                                     Title = (string)m.Attribute("title"),
                                     ContentTypeId = contentTypeId,
                                     AssociatedContentTypeName = (string)m.Attribute("associatedContentTypeName"),
                                     DefaultLayout = m.Attribute("defaultLayout") != null &amp;&amp; (bool)m.Attribute("defaultLayout")
                                 }).ToList();

// Update the content type association.
            foreach (LayoutFile pageLayout in pageLayouts)
    {
        ContentType associatedContentType =
            web.ContentTypes.FirstOrDefault(ct => ct.Name == pageLayout.AssociatedContentTypeName);
        pageLayout.AssociatedContentTypeId = associatedContentType.StringId;                
        UploadPageLayout(web, folder, clientContext, pageLayout);
    }
            
            UpdatePages(web, clientContext, pageLayouts);
        }

  ```

3.  Fügen Sie in Program.cs die **UploadPageLayout** -Methode, die folgenden Aufgaben ausgeführt werden:
    
    1. Checkt die seitenlayoutdatei.
    
    2. Lädt die neue Datei mit [komplexer FileCreationInformation](https://msdn.microsoft.com/library/microsoft.sharepoint.client.filecreationinformation.aspx)hoch.
    
    3. Ruft das Listenelement mit der neu hochgeladene Datei verknüpft ist.
    
    4. Verschiedene Eigenschaften festgelegt für das Listenelement, einschließlich **ContentTypeId** und **PublishingAssociatedContentType**.
    
    5. Checkt, veröffentlicht, und die neue seitenlayoutdatei genehmigt.
    
    6.  Um Verweise auf die alte Seite Layout-Datei zu entfernen, gespeichert Anrufe **PublishingHelper.UpdateAvailablePageLayouts** so aktualisieren Sie den XML-Code in der **PageLayouts** -Eigenschaft auf der aktuellen Website.
    
    7. Wenn die neu hochgeladene seitenlayoutdatei des **DefaultLayout** Attributwert aus settings.xml auf **true** festgelegt ist, verwendet **PublishingHelper.SetDefaultPageLayout** so aktualisieren Sie den XML-Code in die **DefaultPageLayout** -Eigenschaft auf gespeichert, die aktuelle Website.
    

    ```C#
    private static void UploadPageLayout(Web web, Folder folder, ClientContext clientContext, LayoutFile pageLayout)
    {
        using (var fileReadingStream = System.IO.File.OpenRead(pageLayout.File))
        {
            PublishingHelper.CheckOutFile(web, pageLayout.File, folder.ServerRelativeUrl);
            // Use FileCreationInformation to upload the new page layout file.
            var fileInfo = new FileCreationInformation();
            fileInfo.ContentStream = fileReadingStream;
            fileInfo.Overwrite = true;
            fileInfo.Url = pageLayout.File;
            File file = folder.Files.Add(fileInfo);
            // Get the list item associated with the newly uploaded file.
            ListItem item = file.ListItemAllFields;
            clientContext.Load(file.ListItemAllFields);
            clientContext.Load(file,
                                f => f.CheckOutType,
                                f => f.Level,
                                f => f.ServerRelativeUrl);
            clientContext.ExecuteQuery();
    
    item["ContentTypeId"] = pageLayout.ContentTypeId;
            item["Title"] = pageLayout.Title;
            item["PublishingAssociatedContentType"] = string.Format(";#{0};#{1};#", pageLayout.AssociatedContentTypeName, pageLayout.AssociatedContentTypeId);
            item.Update();
            clientContext.ExecuteQuery();
    
    PublishingHelper.CheckInPublishAndApproveFile(file);
    
    PublishingHelper.UpdateAvailablePageLayouts(web, clientContext, pageLayout, file);
    
    if (pageLayout.DefaultLayout)
            {
                PublishingHelper.SetDefaultPageLayout(web, clientContext, file);
            }
        }
    }
    ```

4. Fügen Sie in Program.cs die **UpdatePages** -Methode, die folgenden Aufgaben ausgeführt werden:
    
    1. Dient zum Abrufen der Bibliothek für **Seiten** , und klicken Sie dann in der Bibliothek für **Seiten** Ruft alle Listenelemente.
    
    2. Für jedes Listenelement verwendet das Listenelement **PublishingPageLayout** Feld, um ein passendes Seitenlayout zu aktualisieren, finden die in settings.xml angegeben wurde und jetzt in **Pagelayouts** gespeichert ist. Wenn das Listenelement **PublishingPageLayout** Feld werden, um auf das neue Seitenlayout zu verweisen aktualisiert muss:
    
        1. Checkt das Listenelement-Datei mithilfe von **PublishingHelper.CheckOutFile**.
    
        2. Die URL des Seitenlayouts verweisen auf die neue Seite Layout-Datei aktualisiert, und aktualisiert anschließend das **PublishingPageLayout** Feld des Listenelements.
    
        3. Checkt, veröffentlicht, und die Datei, die durch das Listenelement genehmigt.

    ```C#
    private static void UpdatePages(Web web, ClientContext clientContext, IList<LayoutFile> pageLayouts)
    {
        // Get the Pages Library, and then get all the list items in it.
        List pagesList = web.Lists.GetByTitle("Pages");
        var allItemsQuery = CamlQuery.CreateAllItemsQuery();
        ListItemCollection items = pagesList.GetItems(allItemsQuery);
        clientContext.Load(items);
        clientContext.ExecuteQuery();
        foreach (ListItem item in items)
        {
            // Only update those pages that are using a page layout which is being replaced.
            var pageLayout = item["PublishingPageLayout"] as FieldUrlValue;
            if (pageLayout != null)
            {
                LayoutFile matchingLayout = pageLayouts.FirstOrDefault(p => pageLayout.Url.EndsWith("/" + p.Replaces));
                if (matchingLayout != null)
                {
                    // Check out the page so that we can update the page layout. 
                    PublishingHelper.CheckOutFile(web, item);
    
    // Update the pageLayout reference.
                    pageLayout.Url = pageLayout.Url.Replace(matchingLayout.Replaces, matchingLayout.File);
                    item["PublishingPageLayout"] = pageLayout;
                    item.Update();
                    File file = item.File;
    
    // Get the file and other attributes so that you can check in the file.
                    clientContext.Load(file,
                        f => f.Level,
                        f => f.CheckOutType);
                    clientContext.ExecuteQuery();
    
    
                    PublishingHelper.CheckInPublishAndApproveFile(file);
                }
            }
        }
    }
    ```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Transformieren von Farmlösungen in das SharePoint-Add-In-Modell](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [SharePoint 2013](https://msdn.microsoft.com/library/office/jj162979.aspx)
