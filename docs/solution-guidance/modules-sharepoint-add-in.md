---
title: Module in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: c985fed4a6cb047efc81d5b7cf5d11bb17601a84
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="modules-in-the-sharepoint-add-in-model"></a>Module in der SharePoint-add-in-Objektmodell
======================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Bereitstellen von Artefakten in einer SharePoint-Umgebung unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war. In einer typischen vollständige vertrauen Code (FTC) / Farmlösung Szenario Module definiert in deklarativen Code (Feature Framework XML-Dateien) in SharePoint-Features hinzugefügt wurden. Die Module enthalten die Liste der Artefakte auf dem SharePoint-Server bereitstellen. Die Module wurden zu SharePoint-Features hinzugefügt und über die SharePoint-Lösungen bereitgestellt. Bei Aktivierung des Features wurden die Artefakte in den Modulen definiert in der SharePoint-Umgebung bereitgestellt.

In einem Szenario mit SharePoint-Add-Ins Modell wird das remote provisioning Muster Artefakte für SharePoint-Umgebungen bereit.

<a name="terminology"></a>Terminologie
-----------

In diesem Artikel werden der Begriff *Artefakte* bezeichnet. Artefakte bezieht sich auf Elemente, die in der Regel in einer SharePoint-Umgebung bereitgestellt werden. Artefakte in der Regel umfassen:

- JavaScript-Dateien
- CSS-Dateien
- Bilddateien (JPG, GIF, PNG, usw.).
- Gestaltungsvorlagen
- Seitenlayouts
- Listenelemente

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien zum Bereitstellen von Artefakten auf SharePoint-Umgebungen bereitstellen.

- Verwenden Sie das remote provisioning Muster (SharePoint-Client-Side Object Model und SharePoint-REST-API) zum Bereitstellen von Artefakten in SharePoint-Umgebungen.
- Verwenden Sie deklarative Codemodule oder Feature Framework XML-Dateien nicht zum Bereitstellen von Artefakten in SharePoint-Umgebungen.

**Debuggen**

Ein große Vorteil der Verwendung von Code zum Bereitstellen von Artefakten ist, dass Sie den Bereitstellungsprozess Debuggen, wenn Sie Code verwenden können. Es ist nicht möglich, den Bereitstellungsprozess Debuggen bei Verwendung von deklarativen Codemodule oder Feature Framework XML-Dateien zum Bereitstellen von Artefakten in SharePoint-Umgebungen.

**Erste Schritte**

Die folgenden O365 Plug & Play-Codebeispiele veranschaulichen zum Erstellen einer SharePoint-Add-ins, die das remote provisioning Muster zum Bereitstellen von Artefakten in einer SharePoint-Umgebung verwenden.

  Dieses Beispiel veranschaulicht das Erstellen einer neuen Ordner in der Formatbibliothek und Hinzufügen von JavaScript-Dateien und Bildern auf die neuen Dateien.

- [Branding.ClientSideRendering (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
    + Finden Sie unter der ***UploadJSFiles*** und die ***UploadFileToFolder*** -Methoden in der [Klasse "default.aspx.cs"](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.ClientSideRendering/Branding.ClientSideRenderingWeb/Pages/Default.aspx.cs) Weitere Details.
    + Diese Methoden werden auch eine Kurzübersicht unten angezeigt.
    
        **Erstellen Sie einen Ordner, und Laden Sie JavaScript-Dateien in den Ordner:**

        ```
        void UploadJSFiles(Web web)
        {
            //Delete the folder if it exists
            Microsoft.SharePoint.Client.List list = web.Lists.GetByTitle("Style Library");
            IEnumerable<Folder> results = web.Context.LoadQuery<Folder>(list.RootFolder.Folders.Where(folder => folder.Name == "JSLink-Samples"));
            web.Context.ExecuteQuery();
            Folder samplesJSfolder = results.FirstOrDefault();
        
            if (samplesJSfolder != null)
            {
                samplesJSfolder.DeleteObject();
                web.Context.ExecuteQuery();
            }
        
            //Create new folder
            samplesJSfolder = list.RootFolder.Folders.Add("JSLink-Samples");
            web.Context.Load(samplesJSfolder);
            web.Context.ExecuteQuery();
        
            //Upload JavaScript files to folder
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/Accordion.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/ConfidentialDocuments.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/DisableInput.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/HiddenField.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/PercentComplete.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/PriorityColor.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/ReadOnlySPControls.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/RegexValidator.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/SubstringLongText.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/DependentFields.js"), samplesJSfolder);
        
            //Create another folder inside the folder that was just created
            Folder imgsFolder = samplesJSfolder.Folders.Add("imgs");
            web.Context.Load(imgsFolder);
            web.Context.ExecuteQuery();
        
            //Upload image files to folder
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/imgs/Confidential.png"), imgsFolder);
        }
        ```
        **Erstellen Sie einen Ordner aus, und Laden Sie Bilddateien in den Ordner:**
        ```
        public static void UploadFileToFolder(Web web, string filePath, Folder folder)
            {
            //Create a FileStream to the file to upload
                using (FileStream fs = new FileStream(filePath, FileMode.Open))
                {
                //Create FileCreationInformation object to set file metadata
                    FileCreationInformation flciNewFile = new FileCreationInformation();
    
                    flciNewFile.ContentStream = fs;
                    flciNewFile.Url = System.IO.Path.GetFileName(filePath);
                    flciNewFile.Overwrite = true;
    
                //Upload file to SharePoint
                        Microsoft.SharePoint.Client.File uploadFile = folder.Files.Add(flciNewFile);
    
                //Check in the file
                    uploadFile.CheckIn("CSR sample js file", CheckinType.MajorCheckIn);
    
                    folder.Context.Load(uploadFile);
                    folder.Context.ExecuteQuery();
                }
        }
        ```

Dieses Beispiel zeigt, wie Gestaltungsvorlagen hochladen, Festlegen der Gestaltungsvorlage Metadaten und Anwenden der Gestaltungsvorlage auf der Website durch Festlegen der CustomMasterUrl-Eigenschaft für das Web-Objekt.

- [Branding.ApplyBranding (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ApplyBranding)
    + Siehe die ***UploadPageLayout***, ***CreatePublishingPage***und ***SetSupportCaseContent*** Methoden in der [BrandingHelper.cs-Klasse](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.ApplyBranding/Branding.ApplyBranding.Console/BrandingHelper.cs) für weitere Details.
    + Zusätzlich zum Erstellen neuer Elemente in SharePoint, wird in diesem Beispiel gezeigt, wie Elemente zu entfernen.  Die Methoden, die Elemente entfernen sind als Referenz unten aufgeführt.  
        **Löschen einer Datei:**
    
        ```
        private static void DeleteFile(Web web, string fileName, string serverPath, string serverFolder)
        {
            var fileUrl = string.Concat(serverPath, serverFolder, (string.IsNullOrEmpty(serverFolder) ? string.Empty : "/"), fileName);
            var fileToDelete = web.GetFileByServerRelativeUrl(fileUrl);
            fileToDelete.DeleteObject();
            web.Context.ExecuteQuery();
        }
    
        ```
        **Löschen eines Ordners:**
        ```
        public static void RemoveFolder(ClientContext clientContext, string folder, string path)
            {
                var web = clientContext.Web;
                var filePath = web.ServerRelativeUrl.TrimEnd(Program.trimChars) + "/" + path + "/";
                var folderToDelete = web.GetFolderByServerRelativeUrl(string.Concat(filePath, folder));
                Console.WriteLine("Removing folder {0} from {1}", folder, path);
                folderToDelete.DeleteObject();
                clientContext.ExecuteQuery();
            }
        ```
        **Zuweisung einer Gestaltungsvorlage und Löschen der Gestaltungsvorlage**
        ```
        public static void RemoveMasterPage(ClientContext clientContext, string name, string folder)
            {
                var web = clientContext.Web;
                clientContext.Load(web, w => w.AllProperties);
                clientContext.ExecuteQuery();
    
                Console.WriteLine("Deactivating and removing {0} from {1}", name, web.ServerRelativeUrl);            
            
                //set master pages back to the defaults that were being used
                if (web.AllProperties.FieldValues.ContainsKey("OriginalMasterUrl"))
                {
                    web.MasterUrl = (string)web.AllProperties["OriginalMasterUrl"];
                }
                if (web.AllProperties.FieldValues.ContainsKey("CustomMasterUrl"))
                {
                    web.CustomMasterUrl = (string)web.AllProperties["CustomMasterUrl"];
                }
                web.Update();
                clientContext.ExecuteQuery();
    
                //now that the master page is set back to its default, re-reference the web from context and delete the custom master pages
                web = clientContext.Web;
                var lists = web.Lists;
                var gallery = web.GetCatalog(116);
                clientContext.Load(lists, l => l.Include(ll => ll.DefaultViewUrl));
                clientContext.Load(gallery, g => g.RootFolder.ServerRelativeUrl);
                clientContext.ExecuteQuery();
                var masterPath = gallery.RootFolder.ServerRelativeUrl.TrimEnd(new char[] { '/' }) + "/";
                DeleteFile(web, name, masterPath, folder);
            }
        ```
        **Löschen eines Seitenlayouts**
        ```
        public static void RemovePageLayout(ClientContext clientContext, string name, string folder)
        {
            var web = clientContext.Web;
                var lists = web.Lists;
                var gallery = web.GetCatalog(116);
                clientContext.Load(lists, l => l.Include(ll => ll.DefaultViewUrl));
                clientContext.Load(gallery, g => g.RootFolder.ServerRelativeUrl);
                clientContext.ExecuteQuery();
    
                Console.WriteLine("Removing page layout {0} from {1}", name, clientContext.Web.ServerRelativeUrl);
    
                var masterPath = gallery.RootFolder.ServerRelativeUrl.TrimEnd(Program.trimChars) + "/";
            
                DeleteFile(web, name, masterPath, folder);
        }
        ```

    + Sehen Sie sich das [Anwenden von Branding zu SharePoint-Websites mit einer Add-in für SharePoint (Office 365 Plug & Play-Video)](https://channel9.msdn.com/Blogs/Office-365-Dev/Applying-Branding-to-SharePoint-Sites-with-an-App-for-SharePoint-Office-365-Developer-Patterns-and-P) für einen Durchlauf über dieses Beispiels.

In diesem Beispiel wurde ein wenig der Everythign darin.  Es veranschaulicht, wie die Veröffentlichungsfeatures aktivieren, Seitenlayouts hochladen, Veröffentlichungsseiten erstellen, Listen, Inhaltstypen und Listenelemente und Pblishing Seiten erstellen und Hinzufügen von Webparts und Add-in-Webparts zu den Seiten zu erstellen.  Darüber hinaus veranschaulicht Listenelemente auf der Hostwebsite und das Web-Add-in bereitstellen.

- [Branding.ClientSideRendering (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
    + Siehe Beispiele für diese Vorgänge die Methoden in der [Utils.cs-Klasse](https://github.com/SharePoint/PnP/blob/master/Samples/Core.DataStorageModels/Core.DataStorageModelsWeb/Util/Util.cs) .
    + Diese Methoden werden als Referenz unten aufgeführt.  
        **Websitesammlung und Veröffentlichung Features auf Websiteebene zu aktivieren:**
        ```
        public static void ActivePublishingFeature(ClientContext ctx)
        {
            Guid publishingSiteFeatureId = new Guid("f6924d36-2fa8-4f0b-b16d-06b7250180fa");
            Guid publishingWebFeatureId = new Guid("94c94ca6-b32f-4da9-a9e3-1f3d343d7ecb");
    
            Site clientSite = ctx.Site;
            ctx.Load(clientSite);
    
            FeatureCollection clientSiteFeatures = clientSite.Features;
            ctx.Load(clientSiteFeatures);
    
            //Activate the site feature
            clientSiteFeatures.Add(publishingSiteFeatureId, true, FeatureDefinitionScope.Farm);
            ctx.ExecuteQuery();
    
            FeatureCollection clientWebFeatures = ctx.Web.Features;
            ctx.Load(clientWebFeatures);
    
            //Activate the web feature
            clientWebFeatures.Add(publishingWebFeatureId, true, FeatureDefinitionScope.Farm);
            ctx.ExecuteQuery();
        }
        ```
        **Erstellen Sie eine Liste:**
        ```
        public static List CreateList(ClientContext ctx, int templateType,
                                           string title, string url, QuickLaunchOptions quickLaunchOptions)
        {
            ListCreationInformation listCreationInfo = new ListCreationInformation
            {
                TemplateType = templateType,
                Title = title,
                Url = url,
                QuickLaunchOption = quickLaunchOptions
            };
            List spList = ctx.Web.Lists.Add(listCreationInfo);
            ctx.Load(spList);
            ctx.ExecuteQuery();
    
            return spList;
        }
    
        ```
        **Erstellen eines Inhaltstyps**
        ```
        public static ContentType CreateContentType(ClientContext ctx, string ctyName, string group, string ctyId)
        {
            ContentTypeCreationInformation contentTypeCreation = new ContentTypeCreationInformation();
            contentTypeCreation.Name = ctyName;
            contentTypeCreation.Description = "Custom Content Type";
            contentTypeCreation.Group = group;
            contentTypeCreation.Id = ctyId;
    
            //Add the new content type to the collection
            ContentType ct = ctx.Web.ContentTypes.Add(contentTypeCreation);
            ctx.Load(ct);
            ctx.ExecuteQuery();
    
            return ct;
        }
    
        ```
        **Hochladen eines Seitenlayouts**
        ```
        public static void UploadPageLayout(ClientContext ctx, string sourcePath, string targetListTitle, string targetUrl)
            {
            using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
            {
                byte[] data = new byte[fs.Length];
                fs.Read(data, 0, data.Length);
                using (MemoryStream ms = new MemoryStream())
                {
                    ms.Write(data, 0, data.Length);
                    var newfile = new FileCreationInformation();
                    newfile.Content = ms.ToArray();
                    newfile.Url = targetUrl;
                    newfile.Overwrite = true;
    
                    List docs = ctx.Web.Lists.GetByTitle(targetListTitle);
                    Microsoft.SharePoint.Client.File uploadedFile = docs.RootFolder.Files.Add(newfile);
                    uploadedFile.CheckOut();
                    uploadedFile.CheckIn("Data storage model", CheckinType.MajorCheckIn);
                    uploadedFile.Publish("Data storage model layout.");
    
                    ctx.Load(uploadedFile);
                    ctx.ExecuteQuery();
                }
            }
        }
    
        ```
        **Erstellen einer Veröffentlichungsseite, und legen Sie ihr Seitenlayout:**
        ```
        public static void CreatePublishingPage(ClientContext clientContext, string pageName, string pagelayoutname, string url, string queryurl)
            {
                var publishingPageName = pageName + ".aspx";
    
                Web web = clientContext.Web;
                clientContext.Load(web);
    
                List pages = web.Lists.GetByTitle("Pages");
                clientContext.Load(pages.RootFolder, f => f.ServerRelativeUrl);
                clientContext.ExecuteQuery();
    
                Microsoft.SharePoint.Client.File file =
                    web.GetFileByServerRelativeUrl(pages.RootFolder.ServerRelativeUrl + "/" + pageName + ".aspx");
                clientContext.Load(file, f => f.Exists);
                clientContext.ExecuteQuery();
                if(file.Exists)
                {
                    file.DeleteObject();
                    clientContext.ExecuteQuery();
                }
                PublishingWeb publishingWeb = PublishingWeb.GetPublishingWeb(clientContext, web);
                clientContext.Load(publishingWeb);
    
                if (publishingWeb != null)
                {
                    List publishingLayouts = clientContext.Site.RootWeb.Lists.GetByTitle("Master Page Gallery");
    
                    ListItemCollection allItems = publishingLayouts.GetItems(CamlQuery.CreateAllItemsQuery());
                    clientContext.Load(allItems, items => items.Include(item => item.DisplayName).Where(obj => obj.DisplayName == pagelayoutname));
                    clientContext.ExecuteQuery();
    
                    ListItem layout = allItems.Where(x => x.DisplayName == pagelayoutname).FirstOrDefault();
                    clientContext.Load(layout);
    
                    PublishingPageInformation publishingpageInfo = new PublishingPageInformation()
                    {
                        Name = publishingPageName,
                        PageLayoutListItem = layout,
                    };
    
                    PublishingPage publishingPage = publishingWeb.AddPublishingPage(publishingpageInfo);
                    publishingPage.ListItem.File.CheckIn(string.Empty, CheckinType.MajorCheckIn);
                    publishingPage.ListItem.File.Publish(string.Empty);
                    clientContext.ExecuteQuery();
                }
                SetSupportCaseContent(clientContext, "SupportCasesPage", url, queryurl);
            }
        ```
        **Erstellen von Listenelementen**
        ```
        public static void AddDemoDataToSupportCasesList(ClientContext ctx, List list, string title,
                                                           string status, string csr, string customerID)
        {
            ListItemCreationInformation itemCreateInfo = new ListItemCreationInformation();
            ListItem newItem = list.AddItem(itemCreateInfo);
            newItem["Title"] = title;
            newItem["FTCAM_Status"] = status;
            newItem["FTCAM_CSR"] = csr;
            newItem["FTCAM_CustomerID"] = customerID;
            newItem.Update();
            ctx.ExecuteQuery();
        }
        ```
        **Bereitstellen von Inhalten in einer Veröffentlichungsseite (Inhalt von Suchwebparts, Skript-Editor-Webpart-Add-in Teil), und veröffentlichen Sie die Seite:**
        ```
        public static void SetSupportCaseContent(ClientContext ctx, string pageName, string url, string queryurl)
        {
            List pages = ctx.Web.Lists.GetByTitle("Pages");
            ctx.Load(pages.RootFolder, f => f.ServerRelativeUrl);
            ctx.ExecuteQuery();
    
            Microsoft.SharePoint.Client.File file =
                ctx.Web.GetFileByServerRelativeUrl(pages.RootFolder.ServerRelativeUrl + "/" + pageName + ".aspx");
            ctx.Load(file);
            ctx.ExecuteQuery();
    
            file.CheckOut();
    
            LimitedWebPartManager limitedWebPartManager = file.GetLimitedWebPartManager(PersonalizationScope.Shared);
    
            string quicklaunchmenuFormat =
                @"<div><a href='{0}/{1}'>Sample Home Page</a></div>
                <br />
                <div style='font-weight:bold'>CSR Dashboard</div>
                <div class='cdsm_mainmenu'>
                    <ul>
                        <li><a href='{0}/CSRInfo/{1}'>My CSR Info</a></li>
                        <li><a href='{0}/CallQueue/{1}'>Call Queue</a></li>
                        <li>
                            <span class='collapse_arrow'></span>
                            <span><a href='{0}/CustomerDashboard/{1}'>Customer Dashboard</a></span>
                            <ul>
                                <li><a href='{0}/CustomerDashboard/Orders{1}'>Recent Orders</a></li>
                                <li><a class='current' href='#'>Support Cases</a></li>
                                <li><a href='{0}/CustomerDashboard/Notes{1}'>Notes</a></li>
                            </ul>
                        </li>
                    </ul>
                </div>
                <div class='cdsm_submenu'>
                </div>";
    
            string quicklaunchmenu = string.Format(quicklaunchmenuFormat, url, queryurl);
    
            string qlwebPartXml = "<?xml version=\"1.0\" encoding=\"utf-8\"?><webParts><webPart xmlns=\"http://schemas.microsoft.com/WebPart/v3\"><metaData><type name=\"Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c\" /><importErrorMessage>Cannot import this Web Part.</importErrorMessage></metaData><data><properties><property name=\"Content\" type=\"string\"><![CDATA[" + quicklaunchmenu + "]]></property><property name=\"ChromeType\" type=\"chrometype\">None</property></properties></data></webPart></webParts>";
            WebPartDefinition qlWpd = limitedWebPartManager.ImportWebPart(qlwebPartXml);
            WebPartDefinition qlWpdNew = limitedWebPartManager.AddWebPart(qlWpd.WebPart, "SupportCasesZoneLeft", 0);
            ctx.Load(qlWpdNew);
    
            //Customer Dropdown List Script Web Part
            string dpwebPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/CustomerDropDownlist.webpart");
            WebPartDefinition dpWpd = limitedWebPartManager.ImportWebPart(dpwebPartXml);
            WebPartDefinition dpWpdNew = limitedWebPartManager.AddWebPart(dpWpd.WebPart, "SupportCasesZoneTop", 0);
            ctx.Load(dpWpdNew);
    
            //Support Case CBS Info Web Part
            string cbsInfoWebPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/SupportCaseCBSWebPartInfo.webpart");
            WebPartDefinition cbsInfoWpd = limitedWebPartManager.ImportWebPart(cbsInfoWebPartXml);
            WebPartDefinition cbsInfoWpdNew = limitedWebPartManager.AddWebPart(cbsInfoWpd.WebPart, "SupportCasesZoneMiddle", 0);
            ctx.Load(cbsInfoWpdNew);
    
            //Support Case Content By Search Web Part
            string cbswebPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/SupportCase CBS Webpart/SupportCaseCBS.webpart");
            WebPartDefinition cbsWpd = limitedWebPartManager.ImportWebPart(cbswebPartXml);
            WebPartDefinition cbsWpdNew = limitedWebPartManager.AddWebPart(cbsWpd.WebPart, "SupportCasesZoneMiddle", 1);
            ctx.Load(cbsWpdNew);
    
            //Support Cases App Part
            string appPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/SupportCaseAppPart.webpart");
            WebPartDefinition appPartWpd = limitedWebPartManager.ImportWebPart(appPartXml);
            WebPartDefinition appPartdNew = limitedWebPartManager.AddWebPart(appPartWpd.WebPart, "SupportCasesZoneBottom", 0);
            ctx.Load(appPartdNew);
    
            //Get Host Web Query String and show support case list web part
            string querywebPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/GetHostWebQueryStringAndShowList.webpart");
            WebPartDefinition queryWpd = limitedWebPartManager.ImportWebPart(querywebPartXml);
            WebPartDefinition queryWpdNew = limitedWebPartManager.AddWebPart(queryWpd.WebPart, "SupportCasesZoneBottom", 1);
            ctx.Load(queryWpdNew);
    
    
            file.CheckIn("Data storage model", CheckinType.MajorCheckIn);
            file.Publish("Data storage model");
            ctx.Load(file);
            ctx.ExecuteQuery();
        }
    ```

    + Finden Sie unter der ***FillHostWebSupportCasesToThreshold*** und die ***FillAppWebNotesListToThreshold*** -Methoden in der [Klasse SharePointService.cs](https://github.com/SharePoint/PnP/blob/master/Samples/Core.DataStorageModels/Core.DataStorageModelsWeb/Services/SharePointService.cs) ausführliche Informationen zum Bereitstellen von Listenelementen in der Hostwebsite und das Web-Add-in.  
    + ***Wichtiger Hinweis:*** Die gleichen hostweb und Add-Ins Web Ansätze in diesem Beispiel veranschaulicht können für jede Art von Artifact deren an die entsprechende Position Bereitstellung angewendet werden.

        **Listenelemente zu einer Liste im hostweb hinzuzufügen:**
        ```
        public string FillHostWebSupportCasesToThreshold()
            {
                using (var clientContext = SharePointContext.CreateUserClientContextForSPHost())
                {
                    List supportCasesList = clientContext.Web.Lists.GetByTitle("Support Cases");
                    ListItemCreationInformation itemCreateInfo = new ListItemCreationInformation();
                    for (int i = 0; i < 500; i++)
                    {
                        ListItem newItem = supportCasesList.AddItem(itemCreateInfo);
                        newItem["Title"] = "Wrong product received." + i.ToString();
                        newItem["FTCAM_Status"] = "Open";
                        newItem["FTCAM_CSR"] = "bjones";
                        newItem["FTCAM_CustomerID"] = "thresholds test";
                        newItem.Update();
                        if (i % 100 == 0)
                            clientContext.ExecuteQuery();
                    }
                    clientContext.ExecuteQuery();
    
               
                    clientContext.Load(supportCasesList, l => l.ItemCount);
                    clientContext.ExecuteQuery();
    
                    if(supportCasesList.ItemCount>=5000)
                        return "The Host Web Support Cases List has " + supportCasesList.ItemCount + " items, and exceeds the threshold.";
                    else
                        return 500 + " items have been added to the Host Web Support Cases List. " +
                         "There are " + (5000 - supportCasesList.ItemCount) + " items left to add.";    
            }
        }
        ```
    
        **Hinzufügen von Listenelementen zu einer Liste im Web-Add-in:**
        ```
        public string FillAppWebNotesListToThreshold()
            {
                using (var clientContext = SharePointContext.CreateUserClientContextForSPAppWeb())
                {
                    List notesList = clientContext.Web.Lists.GetByTitle("Notes");
    
                    var itemCreateInfo = new ListItemCreationInformation();
                    for (int i = 0; i < 500; i++)
                    {
                        ListItem newItem = notesList.AddItem(itemCreateInfo);
                        newItem["Title"] = "Notes Title." + i.ToString();
                        newItem["FTCAM_Description"] = "Notes description";
                        newItem.Update();
                        if (i % 100 == 0)
                            clientContext.ExecuteQuery();
                    }
                    clientContext.ExecuteQuery();
    
                    clientContext.Load(notesList, l => l.ItemCount);
                    clientContext.ExecuteQuery();
    
                    if (notesList.ItemCount >= 5000)
                        return "The Add-in Web Notes List has " + notesList.ItemCount + " items, and exceeds the threshold.";
                    else
                        return 500 + " items have been added to the Add-in Web Notes List. " +
                                       "There are " + (5000-notesList.ItemCount) + " items left to add.";          
                }
            }
        ```
    
<a name="related-links"></a>Verwandte links
=============

- [Masterseiten (Anleitung SharePoint-Add-Ins)](master-pages-sharepoint-add-in.md)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Branding.ClientSideRendering (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
- [Branding.ApplyBranding (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ApplyBranding)
- [Branding.ClientSideRendering (O365 Plug & Play-Codebeispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
- Beispiele und Inhalte am [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
