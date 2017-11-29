---
title: "Ersetzen Sie Dateien bereitgestellt, Verwendung von Modulen in SharePoint-farmlösungen"
ms.date: 11/03/2017
ms.openlocfilehash: 3ea55aa39c86acc513ce65954e9ed5cf2195902b
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="replace-files-deployed-using-modules-in-sharepoint-farm-solutions"></a><span data-ttu-id="81577-102">Ersetzen Sie Dateien bereitgestellt, Verwendung von Modulen in SharePoint-farmlösungen</span><span class="sxs-lookup"><span data-stu-id="81577-102">Replace files deployed using modules in SharePoint farm solutions</span></span>

<span data-ttu-id="81577-103">Ersetzen Sie Dateien wie Masterseiten und Seitenlayouts in SharePoint, die Verwendung von Modulen in farmlösungen durch Hochladen und Aktualisieren der Verweise von neuen Dateien bereitgestellt wurden.</span><span class="sxs-lookup"><span data-stu-id="81577-103">Replace files, like master pages and page layouts in SharePoint, that were deployed using modules in farm solutions by uploading and updating references to use new files.</span></span>

<span data-ttu-id="81577-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="81577-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="81577-105">Wenn Sie Dateien mithilfe von Modulen deklarativ in farmlösungen bereitgestellt, erfahren Sie, wie sie in neue Lösungen umgewandelt, die Verweise auf Dateien aktualisiert und bieten eine ähnliche Funktionalität mithilfe des Clientobjektmodells (CSOM).</span><span class="sxs-lookup"><span data-stu-id="81577-105">If you deployed files declaratively using modules in farm solutions, learn how to transform them into new solutions that update references to files and provide similar functionality using the client object model (CSOM).</span></span> <span data-ttu-id="81577-106">In der Vergangenheit wurden Module zur Bereitstellung von Dateien wie etwa Gestaltungsvorlagen und Seitenlayouts verwendet.</span><span class="sxs-lookup"><span data-stu-id="81577-106">In the past, modules were used to deploy files such as master pages and page layouts.</span></span> <span data-ttu-id="81577-107">In diesem Artikel wird beschrieben, wie die Transformation zu verwenden:</span><span class="sxs-lookup"><span data-stu-id="81577-107">This article describes how to use the transformation process to:</span></span>

1. <span data-ttu-id="81577-108">Hochladen von neuen Gestaltungsvorlagen und Seitenlayouts.</span><span class="sxs-lookup"><span data-stu-id="81577-108">Upload new master pages and page layouts.</span></span>
    
2. <span data-ttu-id="81577-109">Aktualisieren der Verweise, um die neue Masterseiten und Seitenlayoutdateien verwenden.</span><span class="sxs-lookup"><span data-stu-id="81577-109">Update references to use the new master pages and page layout files.</span></span>
    
<span data-ttu-id="81577-110">Verwenden Sie diese Transformation verarbeiten, wenn:</span><span class="sxs-lookup"><span data-stu-id="81577-110">Use this transformation process when:</span></span>

- <span data-ttu-id="81577-111">Ihrer vorhandenen farmlösungen verwendet Module zum Bereitstellen von Dateien.</span><span class="sxs-lookup"><span data-stu-id="81577-111">Your existing farm solutions used modules to deploy files.</span></span>
    
-  <span data-ttu-id="81577-112">Sie möchten Gestaltungsvorlagen und Seitenlayouts in farmlösungen mit neuen Gestaltungsvorlagen und Seitenlayouts zu ersetzen, sodass sie mit SharePoint Online migriert werden können.</span><span class="sxs-lookup"><span data-stu-id="81577-112">You want to replace master pages and page layouts in farm solutions with new master pages and page layouts so that they can be migrated to SharePoint Online.</span></span>
    
- <span data-ttu-id="81577-113">Sie haben Dokumentinhaltstypen auf Gestaltungsvorlagen oder in Seitenlayouts in Ihrer farmlösung deklarativ festgelegt.</span><span class="sxs-lookup"><span data-stu-id="81577-113">You have set document content types on master pages or page layouts in your farm solution declaratively.</span></span>

<span data-ttu-id="81577-114">**Wichtig:**  Farmlösungen können nicht mit SharePoint Online migriert werden.</span><span class="sxs-lookup"><span data-stu-id="81577-114">**Important:**  Farm solutions cannot be migrated to SharePoint Online.</span></span> <span data-ttu-id="81577-115">Durch die Techniken und den Code in diesem Artikel beschriebenen anwenden, können Sie eine neue Lösung mit ähnlicher Funktionalität, den Ihre farmlösungen bereitstellen, Update Verweise auf Dateien, erstellen, und klicken Sie dann die neue Lösung mit SharePoint Online bereitgestellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="81577-115">By applying the techniques and code described in this article, you can build a new solution with similar functionality that your farm solutions provide, update references to files, and then the new solution can be deployed to SharePoint Online.</span></span> <span data-ttu-id="81577-116">Klicken Sie dann können Sie das Feature deaktivieren und die vorherige farmlösung zurückgezogen.</span><span class="sxs-lookup"><span data-stu-id="81577-116">You can then disable the feature and retract the previous farm solution.</span></span> <span data-ttu-id="81577-117">Der Code in diesem Artikel erfordert zusätzlichen Code, um eine voll funktionsfähige Lösung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="81577-117">The code in this article requires additional code to provide a fully working solution.</span></span> <span data-ttu-id="81577-118">In diesem Artikel erläutern beispielsweise nicht wie Authentifizierung mit Office 365, Implementierung Ausnahmebehandlung erforderlich, und so weiter.</span><span class="sxs-lookup"><span data-stu-id="81577-118">For example, this article does not discuss how to authenticate with Office 365, how to implement required exception handling, and so on.</span></span> <span data-ttu-id="81577-119">Zusätzliche Codebeispiele finden Sie unter [Office 365 Developer Mustern und Methoden Projekt](https://github.com/SharePoint/PnP).</span><span class="sxs-lookup"><span data-stu-id="81577-119">For additional code samples, see the [Office 365 Developer Patterns and Practices project](https://github.com/SharePoint/PnP).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="81577-120">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="81577-120">Before you begin</span></span>

<span data-ttu-id="81577-121">Idealerweise sollten Sie überprüfen Ihrer vorhandenen farmlösungen, erfahren Sie mehr über die in diesem Artikel beschriebenen Verfahren und dann planen, wie diese Techniken für Ihre Szenarien gelten.</span><span class="sxs-lookup"><span data-stu-id="81577-121">Ideally, you should review your existing farm solutions, learn about the techniques described in this article, and then plan how to apply these techniques to your scenarios.</span></span> <span data-ttu-id="81577-122">Wenn Sie mit farmlösungen vertraut sind, oder nicht über eine vorhandene farmlösung verfügen entwickelt, kann es für Sie hilfreich sein:</span><span class="sxs-lookup"><span data-stu-id="81577-122">If you are unfamiliar with farm solutions or do not have an existing farm solution to work with, it might be helpful for you to:</span></span>

- <span data-ttu-id="81577-123">Laden Sie die [Projektmappe Contoso.Intranet](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet).</span><span class="sxs-lookup"><span data-stu-id="81577-123">Download the [Contoso.Intranet solution](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet).</span></span> <span data-ttu-id="81577-124">Überprüfen Sie Übung 1 [Ersetzung von Dateien über Modulen in voll vertrauenswürdig Lösungen bereitgestellt](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-1%20Replacement%20of%20files%20deployed%20via%20Modules/Lab.md) , um eine schnelle Grundlegendes zur Seite wie master Pages und Layouts in der Vergangenheit erstellt wurden möglicherweise erhalten möchten.</span><span class="sxs-lookup"><span data-stu-id="81577-124">Review exercise 1 in [Replacement of files provisioned via Modules in Full Trust Solutions](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-1%20Replacement%20of%20files%20deployed%20via%20Modules/Lab.md) to get a quick understanding of how master pages and page layouts might have been built in the past.</span></span>
    
- <span data-ttu-id="81577-125">Informationen Sie zu farmlösungen.</span><span class="sxs-lookup"><span data-stu-id="81577-125">Learn about farm solutions.</span></span> <span data-ttu-id="81577-126">Weitere Informationen finden Sie unter [Übersicht über SharePoint 2010-Architekturen](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) und[Farmlösungen in SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).</span><span class="sxs-lookup"><span data-stu-id="81577-126">For more information, see [SharePoint 2010 Architectures Overview](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) and[Build farm solutions in SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).</span></span>
    
<span data-ttu-id="81577-127">Aktivieren Sie Sie vor dem Ausführen Ihrer Codebeispiel die Veröffentlichungsfeatures für die Websitesammlung und Website mit den folgenden Verfahren.</span><span class="sxs-lookup"><span data-stu-id="81577-127">Before running your code sample, enable the publishing features on the site collection and site with the following procedures.</span></span>

1. <span data-ttu-id="81577-128">So aktivieren Sie das Feature **SharePoint Server-Veröffentlichungsinfrastruktur** für die Websitesammlung:</span><span class="sxs-lookup"><span data-stu-id="81577-128">To enable the  **SharePoint Server Publishing Infrastructure** feature on the site collection:</span></span>
    
    1. <span data-ttu-id="81577-129">Öffnen Sie die SharePoint-Website, und navigieren Sie zu **Einstellungen** > **Websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="81577-129">Open your SharePoint site and go to  **Settings** > **Site Settings**.</span></span>
    
    2. <span data-ttu-id="81577-130">Wählen Sie in der **Verwaltung der Websitesammlung** **Websitesammlungs-Features**.</span><span class="sxs-lookup"><span data-stu-id="81577-130">In  **Site Collection Administration**, choose  **Site collection features**.</span></span>
    
    3. <span data-ttu-id="81577-131">Wählen Sie auf **SharePoint Server-Veröffentlichungsinfrastruktur** **Aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="81577-131">On  **SharePoint Server Publishing Infrastructure**, choose  **Activate**.</span></span>
    
2. <span data-ttu-id="81577-132">So aktivieren Sie das Feature **SharePoint Server-Veröffentlichung** auf der Website:</span><span class="sxs-lookup"><span data-stu-id="81577-132">To enable the  **SharePoint Server Publishing** feature on the site:</span></span>
    
    1. <span data-ttu-id="81577-133">Öffnen Sie die SharePoint-Website, und navigieren Sie zu **Einstellungen** > **Websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="81577-133">Open your SharePoint site and go to  **Settings** > **Site Settings**.</span></span>
    
    2. <span data-ttu-id="81577-134">Wählen Sie in der Liste **Websiteaktionen** **Websitefeatures verwalten**.</span><span class="sxs-lookup"><span data-stu-id="81577-134">In  **Site Actions**, choose  **Manage site features**.</span></span>
    
    3. <span data-ttu-id="81577-135">Wählen Sie auf **SharePoint Server-Veröffentlichung** **Aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="81577-135">On  **SharePoint Server Publishing**, choose  **Activate**.</span></span>
    
<span data-ttu-id="81577-136">So richten Visual Studio-Projekt</span><span class="sxs-lookup"><span data-stu-id="81577-136">To set up your Visual Studio project:</span></span>

1. <span data-ttu-id="81577-137">Laden Sie das [Beispielprojekt](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/Student.zip).</span><span class="sxs-lookup"><span data-stu-id="81577-137">Download the [sample project](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/Student.zip).</span></span> <span data-ttu-id="81577-138">Wählen Sie **Ansicht unformatierte** Downloadvorgang das Beispielprojekt, extrahieren Sie die Dateien aus der Zipdatei, und navigieren Sie zu dem Ordner Module9/ModuleReplacement.</span><span class="sxs-lookup"><span data-stu-id="81577-138">Choose  **View Raw** to start downloading the sample project, extract the files from the zip file, and then navigate to the Module9/ModuleReplacement folder.</span></span>
    
2. <span data-ttu-id="81577-139">Öffnen Sie ModuleReplacement.sln.</span><span class="sxs-lookup"><span data-stu-id="81577-139">Open ModuleReplacement.sln.</span></span>
    
3. <span data-ttu-id="81577-140">Öffnen Sie settings.xml.</span><span class="sxs-lookup"><span data-stu-id="81577-140">Open settings.xml.</span></span> <span data-ttu-id="81577-141">Überprüfen Sie und aktualisieren Sie die folgenden Attribute, um Ihre Anforderungen erfüllen:</span><span class="sxs-lookup"><span data-stu-id="81577-141">Review and update the following attributes to meet your requirements:</span></span>
    
    1.  <span data-ttu-id="81577-142">**Masterpage** Element - verwendet das Attribut **File** an die neue Masterseite für die Bereitstellung auf den Gestaltungsvorlagenkatalog und das Attribut **ersetzt** die vorhandene Gestaltungsvorlage im Gestaltungsvorlagenkatalog gibt.</span><span class="sxs-lookup"><span data-stu-id="81577-142">**masterpage** element - Uses the **file** attribute to specify the new master page to deploy to the master page gallery, and the **replaces** attribute specifies the existing master page in the master page gallery.</span></span>
    
    2.  <span data-ttu-id="81577-143">**PageLayout** -Element - verwendet das Attribut **File** , um die neue Seite Layout-Datei anzugeben, das Attribut **ersetzt** die vorhandene Seite Layout-Datei an und mehrere andere Attribute, um zusätzliche Seite Layoutinformationen anzugeben.</span><span class="sxs-lookup"><span data-stu-id="81577-143">**pagelayout** element - Uses the **file** attribute to specify the new page layout file, the **replaces** attribute to specify the existing page layout file, and several other attributes to specify additional page layout information.</span></span>

    <span data-ttu-id="81577-144">**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="81577-144">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

4. <span data-ttu-id="81577-145">In MasterPageGalleryFiles.cs definieren die Klassen **MasterPageGalleryFile** und **LayoutFile** -Geschäftsobjekte, in denen Informationen zu den neuen Gestaltungsvorlagen und Seitenlayouts in SharePoint hochgeladen werden gespeichert.</span><span class="sxs-lookup"><span data-stu-id="81577-145">In MasterPageGalleryFiles.cs, the  **MasterPageGalleryFile** and **LayoutFile** classes define business objects that store information about the new master pages and page layouts to be uploaded to SharePoint.</span></span>

## <a name="upload-and-update-references-to-master-pages"></a><span data-ttu-id="81577-146">Hochladen Sie und aktualisieren Sie der Verweise auf Gestaltungsvorlagen</span><span class="sxs-lookup"><span data-stu-id="81577-146">Upload and update references to master pages</span></span>

<span data-ttu-id="81577-147">Hochladen und Aktualisieren der Verweise auf die neuen Masterseiten auf Ihrer SharePoint-Website:</span><span class="sxs-lookup"><span data-stu-id="81577-147">To upload and update references to the new master pages on your SharePoint site:</span></span>

1. <span data-ttu-id="81577-148">Fügen Sie in der Datei Program.cs die folgenden **using** -Anweisung hinzu.</span><span class="sxs-lookup"><span data-stu-id="81577-148">In Program.cs, add the following  **using** statement.</span></span>
    
    ```C#
        using System.Security;
    ```

2. <span data-ttu-id="81577-149">Fügen Sie in der Datei Program.cs die folgenden Methoden zum Ausführen der Authentifizierung zu Office 365.</span><span class="sxs-lookup"><span data-stu-id="81577-149">In Program.cs, add the following methods to perform authentication to Office 365.</span></span>
    
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

3. <span data-ttu-id="81577-150">Fügen Sie den folgenden Code in Program.cs der **Main** -Methode, die die folgenden Aufgaben ausführt:</span><span class="sxs-lookup"><span data-stu-id="81577-150">In Program.cs, add the following code to the  **Main** method, which performs the following tasks:</span></span>
    
    1. <span data-ttu-id="81577-151">Lädt die Datei settings.xml.</span><span class="sxs-lookup"><span data-stu-id="81577-151">Loads the settings.xml file.</span></span>
    
    2. <span data-ttu-id="81577-152">Ruft einen Verweis auf den Gestaltungsvorlagenkatalog mithilfe von [GetCatalog](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.getcatalog.aspx)(116).</span><span class="sxs-lookup"><span data-stu-id="81577-152">Gets a reference to the master page gallery by using [GetCatalog](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.getcatalog.aspx)(116).</span></span> <span data-ttu-id="81577-153">Masterseiten werden in den Gestaltungsvorlagenkatalog hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="81577-153">Master pages are uploaded to the master page gallery.</span></span> <span data-ttu-id="81577-154">Der Bezeichner der Listenvorlage der Gestaltungsvorlagenkatalog ist 116.</span><span class="sxs-lookup"><span data-stu-id="81577-154">The identifier of the list template of the master page gallery is 116.</span></span> <span data-ttu-id="81577-155">Weitere Informationen finden Sie unter [ListTemplate-Element (Website)](https://msdn.microsoft.com/library/ms439434.aspx).</span><span class="sxs-lookup"><span data-stu-id="81577-155">For more information, see [ListTemplate Element (Site)](https://msdn.microsoft.com/library/ms439434.aspx).</span></span> <span data-ttu-id="81577-156">Weitere Informationen über den Gestaltungsvorlagenkatalog werden geladen, einschließlich der Verwendung von [List.ContentTypes](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.contenttypes.aspx) zum Abrufen der Inhaltstypen Gestaltungsvorlagenkatalog zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="81577-156">Other details about the master page gallery are loaded, including using [List.ContentTypes](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.contenttypes.aspx) to get the content types associated with the master page gallery.</span></span>
    
    3. <span data-ttu-id="81577-157">Lädt die Eigenschaften des einschließlich Web.ContentTypes, Web.MasterUrl und Web.CustomMasterUrl Web-Objekts.</span><span class="sxs-lookup"><span data-stu-id="81577-157">Loads properties of the Web object including Web.ContentTypes, Web.MasterUrl, and Web.CustomMasterUrl.</span></span>
    
    4. <span data-ttu-id="81577-158">**ParentMasterPageContentTypeId** festgelegt auf den Inhaltstyp-ID von Masterseiten.</span><span class="sxs-lookup"><span data-stu-id="81577-158">Sets  **parentMasterPageContentTypeId** to the content type ID of master pages.</span></span> <span data-ttu-id="81577-159">Weitere Informationen finden Sie unter[Base Content Type Hierarchy](https://msdn.microsoft.com/library/ms452896%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="81577-159">For more information, see[Base Content Type Hierarchy](https://msdn.microsoft.com/library/ms452896%28v=office.14%29.aspx).</span></span>
    
    5. <span data-ttu-id="81577-160">Ruft den Inhaltstyp der Gestaltungsvorlagen aus den Gestaltungsvorlagenkatalog ab.</span><span class="sxs-lookup"><span data-stu-id="81577-160">Gets the content type of master pages from the master page gallery.</span></span> <span data-ttu-id="81577-161">Dieser Inhaltstyp wird verwendet, um den Inhaltstyp der neuen Gestaltungsvorlage weiter unten in diesem Artikel festlegen.</span><span class="sxs-lookup"><span data-stu-id="81577-161">This content type is used to set the content type of the new master page later in this article.</span></span> 
    
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

4. <span data-ttu-id="81577-162">Fügen Sie in Program.cs die **UploadAndSetMasterPages** -Methode, die eine Liste von Geschäftsobjekten durch **MasterPageGalleryFile** erstellt:</span><span class="sxs-lookup"><span data-stu-id="81577-162">In Program.cs, add the  **UploadAndSetMasterPages** method, which creates a list of **MasterPageGalleryFile** business objects by:</span></span>
    
    1. <span data-ttu-id="81577-163">Alle im settings.xml definierten **MasterPage** Elemente lesen.</span><span class="sxs-lookup"><span data-stu-id="81577-163">Reading all the  **masterPage** elements defined in settings.xml.</span></span>
    
    2. <span data-ttu-id="81577-164">Laden für jedes **MasterPage** -Element, das eine Gestaltungsvorlage für SharePoint hochladen angibt, die Attributwerte in einem Geschäftsobjekt **MasterPageGalleryFile** .</span><span class="sxs-lookup"><span data-stu-id="81577-164">For each  **masterPage** element, which specifies a master page to upload to SharePoint, loading the attribute values into a **MasterPageGalleryFile** business object.</span></span>
    
    3. <span data-ttu-id="81577-165">Für jedes **MasterPageGalleryFile** Business-Objekt in der Liste **UploadAndSetMasterPage**anrufen.</span><span class="sxs-lookup"><span data-stu-id="81577-165">For each  **MasterPageGalleryFile** business object in the list, making a call to **UploadAndSetMasterPage**.</span></span>
    
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

5. <span data-ttu-id="81577-166">Fügen Sie in Program.cs die **UploadAndSetMasterPage** -Methode, die folgenden Aufgaben ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="81577-166">In Program.cs, add the  **UploadAndSetMasterPage** method, which performs the following tasks:</span></span>
    
    1. <span data-ttu-id="81577-167">Checkt die Gestaltungsvorlage.</span><span class="sxs-lookup"><span data-stu-id="81577-167">Checks out the master page.</span></span>
    
    2. <span data-ttu-id="81577-168">Lädt die neue Datei mit [komplexer FileCreationInformation](https://msdn.microsoft.com/library/microsoft.sharepoint.client.filecreationinformation.aspx)hoch.</span><span class="sxs-lookup"><span data-stu-id="81577-168">Uploads the new file by using [FileCreationInformation](https://msdn.microsoft.com/library/microsoft.sharepoint.client.filecreationinformation.aspx).</span></span>
    
    3. <span data-ttu-id="81577-169">Ruft das Listenelement mit der neu hochgeladene Datei verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="81577-169">Gets the list item associated with the newly uploaded file.</span></span>
    
    4. <span data-ttu-id="81577-170">Verschiedene Eigenschaften festgelegt für das Listenelement, einschließlich Festlegen der Inhaltstyp-ID des Listenelements auf den Inhaltstyp-ID der Masterseite.</span><span class="sxs-lookup"><span data-stu-id="81577-170">Sets various properties on the list item, including setting the content type ID of the list item to the content type ID of the master page.</span></span>
    
    5. <span data-ttu-id="81577-171">Überprüft und genehmigt die neue Masterseite veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="81577-171">Checks in, publishes, and approves the new master page.</span></span> 
    
    6. <span data-ttu-id="81577-172">Wenn die Masterseite für die aktuelle Website oder benutzerdefinierte Gestaltungsvorlage URL auf die alte Gestaltungsvorlage festgelegt ist, aktualisiert [Web.MasterUrl](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.masterurl.aspx) oder[Web.CustomMasterUrl](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.custommasterurl.aspx) , um die URL der neu hochgeladene Masterseite verwenden.</span><span class="sxs-lookup"><span data-stu-id="81577-172">If the current site's master page or custom master page URL is set to the old master page, updates [Web.MasterUrl](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.masterurl.aspx) or[Web.CustomMasterUrl](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.custommasterurl.aspx) to use the newly uploaded master page URL.</span></span>
    
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

## <a name="upload-and-update-references-to-page-layouts"></a><span data-ttu-id="81577-173">Hochladen Sie und aktualisieren Sie der Verweise auf Seitenlayouts</span><span class="sxs-lookup"><span data-stu-id="81577-173">Upload and update references to page layouts</span></span>

<span data-ttu-id="81577-174">**Hinweis:**  Die Codebeispiele in diesem Abschnitt erstellen Sie auf die Codebeispiele im vorherigen Abschnitt dieses Artikels.</span><span class="sxs-lookup"><span data-stu-id="81577-174">**Note:**  The code examples in this section build on the code examples in the previous section of this article.</span></span> 

<span data-ttu-id="81577-175">Um Seitenlayouts zu ersetzen, die Verwendung von Modulen in farmlösungen bereitgestellt wurden, Hochladen Sie und aktualisieren Sie der Verweise auf die neue Seitenlayoutdateien durch verwenden:</span><span class="sxs-lookup"><span data-stu-id="81577-175">To replace page layouts that were deployed using modules in farm solutions, upload and update references to use the new page layout files by:</span></span>


1. <span data-ttu-id="81577-176">Aktualisieren der **Main** -Methode durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="81577-176">Updating the  **Main** method with the following code.</span></span> <span data-ttu-id="81577-177">Dieser Code enthält zusätzliche Schritte zum Hochladen und Aktualisieren der Verweise auf Seitenlayoutdateien, einschließlich:</span><span class="sxs-lookup"><span data-stu-id="81577-177">This code contains additional steps for uploading and updating references to page layout files, including:</span></span>
    
    1. <span data-ttu-id="81577-178">Wenn Sie auf das Seitenlayout Inhaltstyp-ID **ParentPageLayoutContentTypeId** festlegen</span><span class="sxs-lookup"><span data-stu-id="81577-178">Setting  **parentPageLayoutContentTypeId** to the page layout's content type ID.</span></span>
    
    2.  <span data-ttu-id="81577-179">Abrufen eines Inhaltstyps, der mit **ParentPageLayoutContentTypeId** aus den Gestaltungsvorlagenkatalog übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="81577-179">Getting a content type that matches **parentPageLayoutContentTypeId** from the master page gallery.</span></span>
    
    3. <span data-ttu-id="81577-180">**UploadPageLayoutsAndUpdateReferences**aufrufen.</span><span class="sxs-lookup"><span data-stu-id="81577-180">Calling  **UploadPageLayoutsAndUpdateReferences**.</span></span>
    
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

2. <span data-ttu-id="81577-181">Fügen Sie in Program.cs die **UploadPageLayoutsAndUpdateReferences** -Methode, die folgenden Schritte ausführt:</span><span class="sxs-lookup"><span data-stu-id="81577-181">In Program.cs, add the  **UploadPageLayoutsAndUpdateReferences** method, which performs the following steps:</span></span>
    
    1. <span data-ttu-id="81577-182">Liest die Seite Ersatz Layoutinformationen settings.xml **Pagelayout** Elemente lesen und speichern die Seite Ersatz Layoutinformationen im **LayoutFile** von Geschäftsobjekten zu einer Liste aller Business-Objekte hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="81577-182">Reads the page layout replacement information by reading the  **pagelayout** elements from settings.xml, storing the page layout replacement information in **LayoutFile** business objects, and adding all the business objects to a list.</span></span>
    
    2. <span data-ttu-id="81577-183">Für jede Seitenlayout ersetzen:</span><span class="sxs-lookup"><span data-stu-id="81577-183">For each page layout to replace:</span></span>
    
        1. <span data-ttu-id="81577-184">Abfragen geben die Websiteinhaltstypen mithilfe von [Web.ContentTypes](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.contenttypes.aspx) finden Sie eine entsprechende Ressourcen, in dem der Name des Inhaltstyps für die Website der **AssociatedContentTypeName** in settings.xml für das neue Seitenlayout angegebenen gleich ist.</span><span class="sxs-lookup"><span data-stu-id="81577-184">Queries the site's content types by using [Web.ContentTypes](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.contenttypes.aspx) to find a matching content type where the name of the site's content type is equal to the **associatedContentTypeName** specified in settings.xml for the new page layout.</span></span>
    
        2. <span data-ttu-id="81577-185">Ruft die **UploadPageLayout**.</span><span class="sxs-lookup"><span data-stu-id="81577-185">Calls  **UploadPageLayout**.</span></span>
    
        3. <span data-ttu-id="81577-186">Ruft die **UpdatePages** zum Aktualisieren vorhandener Seiten, um die neuen Seitenlayouts zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="81577-186">Calls  **UpdatePages** to update existing pages to use the new page layouts.</span></span>

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

3.  <span data-ttu-id="81577-187">Fügen Sie in Program.cs die **UploadPageLayout** -Methode, die folgenden Aufgaben ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="81577-187">In Program.cs, add the **UploadPageLayout** method, which performs the following tasks:</span></span>
    
    1. <span data-ttu-id="81577-188">Checkt die seitenlayoutdatei.</span><span class="sxs-lookup"><span data-stu-id="81577-188">Checks out the page layout file.</span></span>
    
    2. <span data-ttu-id="81577-189">Lädt die neue Datei mit [komplexer FileCreationInformation](https://msdn.microsoft.com/library/microsoft.sharepoint.client.filecreationinformation.aspx)hoch.</span><span class="sxs-lookup"><span data-stu-id="81577-189">Uploads the new file by using [FileCreationInformation](https://msdn.microsoft.com/library/microsoft.sharepoint.client.filecreationinformation.aspx).</span></span>
    
    3. <span data-ttu-id="81577-190">Ruft das Listenelement mit der neu hochgeladene Datei verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="81577-190">Gets the list item associated with the newly uploaded file.</span></span>
    
    4. <span data-ttu-id="81577-191">Verschiedene Eigenschaften festgelegt für das Listenelement, einschließlich **ContentTypeId** und **PublishingAssociatedContentType**.</span><span class="sxs-lookup"><span data-stu-id="81577-191">Sets various properties on the list item, including  **ContentTypeId** and **PublishingAssociatedContentType**.</span></span>
    
    5. <span data-ttu-id="81577-192">Checkt, veröffentlicht, und die neue seitenlayoutdatei genehmigt.</span><span class="sxs-lookup"><span data-stu-id="81577-192">Checks in, publishes, and approves the new page layout file.</span></span>
    
    6.  <span data-ttu-id="81577-193">Um Verweise auf die alte Seite Layout-Datei zu entfernen, gespeichert Anrufe **PublishingHelper.UpdateAvailablePageLayouts** so aktualisieren Sie den XML-Code in der **PageLayouts** -Eigenschaft auf der aktuellen Website.</span><span class="sxs-lookup"><span data-stu-id="81577-193">To remove references to the old page layout file, calls **PublishingHelper.UpdateAvailablePageLayouts** to update the XML stored in the **PageLayouts** property on the current site.</span></span>
    
    7. <span data-ttu-id="81577-194">Wenn die neu hochgeladene seitenlayoutdatei des **DefaultLayout** Attributwert aus settings.xml auf **true** festgelegt ist, verwendet **PublishingHelper.SetDefaultPageLayout** so aktualisieren Sie den XML-Code in die **DefaultPageLayout** -Eigenschaft auf gespeichert, die aktuelle Website.</span><span class="sxs-lookup"><span data-stu-id="81577-194">If the newly uploaded page layout file's  **defaultLayout** attribute value from settings.xml is set to **true** , uses **PublishingHelper.SetDefaultPageLayout** to update the XML stored in the **DefaultPageLayout** property on the current site.</span></span>
    

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

4. <span data-ttu-id="81577-195">Fügen Sie in Program.cs die **UpdatePages** -Methode, die folgenden Aufgaben ausgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="81577-195">In Program.cs, add the  **UpdatePages** method, which performs the following tasks:</span></span>
    
    1. <span data-ttu-id="81577-196">Dient zum Abrufen der Bibliothek für **Seiten** , und klicken Sie dann in der Bibliothek für **Seiten** Ruft alle Listenelemente.</span><span class="sxs-lookup"><span data-stu-id="81577-196">Gets the  **Pages** library, and then gets all the list items in the **Pages** library.</span></span>
    
    2. <span data-ttu-id="81577-197">Für jedes Listenelement verwendet das Listenelement **PublishingPageLayout** Feld, um ein passendes Seitenlayout zu aktualisieren, finden die in settings.xml angegeben wurde und jetzt in **Pagelayouts** gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="81577-197">For each list item, uses the list item's  **PublishingPageLayout** field to find a matching page layout to update, which was specified in settings.xml and is now stored in **pagelayouts** .</span></span> <span data-ttu-id="81577-198">Wenn das Listenelement **PublishingPageLayout** Feld werden, um auf das neue Seitenlayout zu verweisen aktualisiert muss:</span><span class="sxs-lookup"><span data-stu-id="81577-198">If the list item's **PublishingPageLayout** field needs to be updated to refer to the new page layout:</span></span>
    
        1. <span data-ttu-id="81577-199">Checkt das Listenelement-Datei mithilfe von **PublishingHelper.CheckOutFile**.</span><span class="sxs-lookup"><span data-stu-id="81577-199">Checks out the list item's file by using  **PublishingHelper.CheckOutFile**.</span></span>
    
        2. <span data-ttu-id="81577-200">Die URL des Seitenlayouts verweisen auf die neue Seite Layout-Datei aktualisiert, und aktualisiert anschließend das **PublishingPageLayout** Feld des Listenelements.</span><span class="sxs-lookup"><span data-stu-id="81577-200">Updates the URL of the page layout to refer to the new page layout file, and then updates the  **PublishingPageLayout** field of the list item.</span></span>
    
        3. <span data-ttu-id="81577-201">Checkt, veröffentlicht, und die Datei, die durch das Listenelement genehmigt.</span><span class="sxs-lookup"><span data-stu-id="81577-201">Checks in, publishes, and approves the file referenced by the list item.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="81577-202">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="81577-202">Additional resources</span></span>
<span data-ttu-id="81577-203"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="81577-203"></span></span>

- [<span data-ttu-id="81577-204">Transformieren von Farmlösungen in das SharePoint-Add-In-Modell</span><span class="sxs-lookup"><span data-stu-id="81577-204">Transform farm solutions to the SharePoint add-in model</span></span>](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [<span data-ttu-id="81577-205">SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="81577-205">SharePoint 2013</span></span>](https://msdn.microsoft.com/library/office/jj162979.aspx)
