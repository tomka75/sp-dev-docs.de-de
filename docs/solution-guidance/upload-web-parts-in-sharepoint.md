---
title: Hochladen von Webparts in SharePoint
ms.date: 11/03/2017
ms.openlocfilehash: c7e6e7a4bc6d843661ecd7c27d71381f47254ca9
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="upload-web-parts-in-sharepoint"></a><span data-ttu-id="afda8-102">Hochladen von Webparts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="afda8-102">Upload Web Parts in SharePoint</span></span>

<span data-ttu-id="afda8-103">Bereitstellen Sie vorkonfigurierte, standardmäßigen SharePoint-Webparts für die Benutzer.</span><span class="sxs-lookup"><span data-stu-id="afda8-103">Deploy pre-configured, standard SharePoint Web Parts for your users.</span></span>

<span data-ttu-id="afda8-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="afda8-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="afda8-105">Sie können die vorkonfigurierte, standardmäßigen SharePoint-Webparts für Benutzer hinzufügen zu ihrer SharePoint-Websites hochladen.</span><span class="sxs-lookup"><span data-stu-id="afda8-105">You can upload pre-configured, standard SharePoint Web Parts for users to add to their SharePoint sites.</span></span> <span data-ttu-id="afda8-106">Beispielsweise können Sie eine vorkonfigurierte hochladen:</span><span class="sxs-lookup"><span data-stu-id="afda8-106">For example, you can upload a pre-configured:</span></span>

- <span data-ttu-id="afda8-107">Skript-Editor-Webpart, das JavaScript-Dateien auf der Remotewebsite verwendet.</span><span class="sxs-lookup"><span data-stu-id="afda8-107">Script Editor Web Part that uses JavaScript files on the remote web.</span></span>
    
- <span data-ttu-id="afda8-108">Inhaltssuche-Webpart.</span><span class="sxs-lookup"><span data-stu-id="afda8-108">Content Search Web Part.</span></span>
    
<span data-ttu-id="afda8-109">In diesem Artikel wird das vor dem konfigurieren den Skript-Editor-Webpart JavaScript-Dateien auf der Remotewebsite verwenden, um Anpassung der Benutzeroberfläche auszuführen.</span><span class="sxs-lookup"><span data-stu-id="afda8-109">This article discusses pre-configuring the Script Editor Web Part to use JavaScript files on the remote web to perform UI customization.</span></span> <span data-ttu-id="afda8-110">Mit dieser Lösung können:</span><span class="sxs-lookup"><span data-stu-id="afda8-110">Use this solution to:</span></span>

- <span data-ttu-id="afda8-111">Verwenden Sie die Skriptdateien aus dem remote Web in Webparts und nicht verweisenden Skripts aus der Liste **Websiteobjekte** auf dem hostweb.</span><span class="sxs-lookup"><span data-stu-id="afda8-111">Use script files from the remote web in your Web Parts rather than referencing scripts from the **Site Assets** list on the host web.</span></span>
    
- <span data-ttu-id="afda8-112">Bereitstellen von vorkonfigurierten Webparts in Ihrer benutzerdefinierten Site Bereitstellungsprozesses.</span><span class="sxs-lookup"><span data-stu-id="afda8-112">Deploy pre-configured Web Parts in your custom site provisioning process.</span></span> <span data-ttu-id="afda8-113">Möglicherweise möchten Sie beispielsweise als Teil Ihrer benutzerdefinierten Site Bereitstellungsprozesses, Website Nutzungsinformationen Richtlinie für den Benutzer angezeigt wird, wenn eine neue Website erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="afda8-113">For example, as part of your custom site provisioning process, you might want to display site usage policy information to the user when a new site is created.</span></span> 
    
- <span data-ttu-id="afda8-114">Geladen Sie gefilterte Inhalte in Webparts für Ihre Benutzer automatisch.</span><span class="sxs-lookup"><span data-stu-id="afda8-114">Automatically load filtered content in your Web Parts for your users.</span></span> <span data-ttu-id="afda8-115">Beispielsweise kann Skriptdatei Lesen von einem externen System lokale Nachrichten Informationen anzeigen.</span><span class="sxs-lookup"><span data-stu-id="afda8-115">For example, your script file can display local news information read from an external system.</span></span>
    
- <span data-ttu-id="afda8-116">Ermöglicht es Benutzern ihrer Website mithilfe von Webparts aus dem **Webpartkatalog**zusätzliche Funktionen hinzu.</span><span class="sxs-lookup"><span data-stu-id="afda8-116">Allow users to add additional functionality to their site by using Web Parts from the **Web Part Gallery**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="afda8-117">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="afda8-117">Before you begin</span></span>

<span data-ttu-id="afda8-118">Laden Sie Sie zuerst [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) -Beispiel-add-in des Projekts [Office365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="afda8-118">To get started, download the [Core.AppScriptPart ](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) sample add-in from the [Office365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-coreappscriptpart-add-in"></a><span data-ttu-id="afda8-119">Mithilfe des Core.AppScriptPart-add-Ins</span><span class="sxs-lookup"><span data-stu-id="afda8-119">Using the Core.AppScriptPart add-in</span></span>

<span data-ttu-id="afda8-120">Wenn Sie das Codebeispiel ausführen und **Szenario ausführen**wählen:</span><span class="sxs-lookup"><span data-stu-id="afda8-120">When you run the code sample and choose **Run Scenario**:</span></span>

1. <span data-ttu-id="afda8-121">Wählen Sie **zurück zur Website**.</span><span class="sxs-lookup"><span data-stu-id="afda8-121">Choose **Back to Site**.</span></span>
    
2. <span data-ttu-id="afda8-122">**Seite**zum Auswählen von > **Bearbeiten** > **Einfügen** > **-Webpart**.</span><span class="sxs-lookup"><span data-stu-id="afda8-122">Choose **PAGE** > **Edit** > **INSERT** > **Web Part**.</span></span>
    
3. <span data-ttu-id="afda8-123">Wählen Sie in **Kategorien**die **Add-in-Skript Teil**, und dann **von Benutzerprofilinformationen**.</span><span class="sxs-lookup"><span data-stu-id="afda8-123">In **Categories**, choose **Add-in Script Part**, and then choose **User profile information**.</span></span>
    
4. <span data-ttu-id="afda8-124">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="afda8-124">Choose **Add**.</span></span>
    
5. <span data-ttu-id="afda8-125">Wählen Sie in der Dropdown-Liste in der oberen rechten Ecke des Webparts **von Benutzerprofilinformationen** **Webpart bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="afda8-125">In the drop-down in the upper-right corner of the **User profile information** Web Part, choose **Edit Web Part**.</span></span>
    
6. <span data-ttu-id="afda8-126">Wählen Sie **AUSSCHNITT bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="afda8-126">Choose **EDIT SNIPPET**.</span></span>
    
7. <span data-ttu-id="afda8-127">Überprüfen der ** &lt;Skript&gt; ** Element.</span><span class="sxs-lookup"><span data-stu-id="afda8-127">Review the **&lt;SCRIPT&gt;** element.</span></span>
    
    <span data-ttu-id="afda8-128">Beachten Sie, dass das **Src** -Attribut Links zu einer JavaScript-auf die Remotewebsite Datei.</span><span class="sxs-lookup"><span data-stu-id="afda8-128">Notice that the  **src** attribute links to a JavaScript file on the remote web.</span></span> <span data-ttu-id="afda8-129">Die ** &lt;Skript&gt; ** Element wird von der **Content** -Eigenschaft in der Core.AppScriptPartWeb\userprofileinformation.webpart festgelegt, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="afda8-129">The **&lt;SCRIPT&gt;** element is set by the **Content** property in the Core.AppScriptPartWeb\userprofileinformation.webpart, as shown in the following example.</span></span> <span data-ttu-id="afda8-130">Die JavaScript-Datei mit verknüpften durch das **Src** -Attribut ist Core.AppScriptPartWeb\Scripts\userprofileinformation.js.</span><span class="sxs-lookup"><span data-stu-id="afda8-130">The JavaScript file linked to by the **src** attribute is Core.AppScriptPartWeb\Scripts\userprofileinformation.js.</span></span> <span data-ttu-id="afda8-131">Userprofileinformation.js liest Profilinformationen des aktuellen Benutzers aus der Benutzerprofildienst und dann diese Informationen im Webpart angezeigt.</span><span class="sxs-lookup"><span data-stu-id="afda8-131">Userprofileinformation.js reads the current user's profile information from the user profile service, and then displays this information in the Web Part.</span></span>
    
     <span data-ttu-id="afda8-132">**Hinweis:** Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="afda8-132">**Note:** The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

  ```XML
  <property name="Content" type="string">&amp;lt;script type="text/javascript" src="https://localhost:44361/scripts/userprofileinformation.js"&amp;gt;&amp;lt;/script&amp;gt;
&amp;lt;div id="UserProfileAboutMe"&amp;gt;&amp;lt;div&amp;gt;
  </property>
  ```

8. <span data-ttu-id="afda8-133">Wählen Sie **Abbrechen**.</span><span class="sxs-lookup"><span data-stu-id="afda8-133">Choose **Cancel**.</span></span>
    
9. <span data-ttu-id="afda8-134">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="afda8-134">Choose **Save**.</span></span>

<span data-ttu-id="afda8-135">**Hinweis:** Wenn Ihre Benutzerprofil Bild nicht angezeigt wird, öffnen Sie Ihrer OneDrive for Business-Website, und klicken Sie dann mit der Hostwebsite zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="afda8-135">**Note:** If your user profile image does not display, open your OneDrive for Business site, and then return to the host web.</span></span>

<span data-ttu-id="afda8-136">In Core.AppScriptPartWeb\Pages\Default.aspx führt **Szenario ausführen** **BtnScenario_Click**, die Folgendes ermöglicht:</span><span class="sxs-lookup"><span data-stu-id="afda8-136">In Core.AppScriptPartWeb\Pages\Default.aspx, **Run Scenario** runs **btnScenario_Click**, which does the following:</span></span>

1. <span data-ttu-id="afda8-137">Ruft einen Verweis auf den Ordner **Webpartkatalog** .</span><span class="sxs-lookup"><span data-stu-id="afda8-137">Gets a reference to the **Web Part Gallery** folder.</span></span>
    
2. <span data-ttu-id="afda8-138">Wird verwendet, [komplexer FileCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.aspx) zum Erstellen der Datei userprofileinformation.webpart so vom Anbieter gehostete-add-in in den **Webpartkatalog**hoch.</span><span class="sxs-lookup"><span data-stu-id="afda8-138">Uses [FileCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.aspx) to create the userprofileinformation.webpart file to upload from the provider-hosted add-in to the **Web Part Gallery**.</span></span> <span data-ttu-id="afda8-139">Der Ordner **. Files.Add** -Methode fügt die Datei dem **Webpartkatalog**hinzu.</span><span class="sxs-lookup"><span data-stu-id="afda8-139">The **folder.Files.Add** method adds the file to the **Web Part Gallery**.</span></span>
    
3. <span data-ttu-id="afda8-140">Ruft alle Listenelemente in der **Webpart-Katalog**, und klicken Sie dann userprofileinformation.webpart gesucht.</span><span class="sxs-lookup"><span data-stu-id="afda8-140">Retrieves all list items in the **Web Part Gallery**, and then searches for userprofileinformation.webpart.</span></span>
    
4. <span data-ttu-id="afda8-141">Wenn userprofileinformation.webpart gefunden wird, weist das Webpart zu einer benutzerdefinierten Gruppe mit dem Namen **Add-in-Skript Teil**.</span><span class="sxs-lookup"><span data-stu-id="afda8-141">When userprofileinformation.webpart is found, assigns the Web Part to a custom group named **Add-in Script Part**.</span></span>

```C#
protected void btnScenario_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                var folder = clientContext.Web.Lists.GetByTitle("Web Part Gallery").RootFolder;
                clientContext.Load(folder);
                clientContext.ExecuteQuery();

                // Upload the "userprofileinformation.webpart" file.
                using (var stream = System.IO.File.OpenRead(
                                Server.MapPath("~/userprofileinformation.webpart")))
                {
                    FileCreationInformation fileInfo = new FileCreationInformation();
                    fileInfo.ContentStream = stream;
                    fileInfo.Overwrite = true;
                    fileInfo.Url = "userprofileinformation.webpart";
                    File file = folder.Files.Add(fileInfo);
                    clientContext.ExecuteQuery();
                }

                // Update the group that the Web Part belongs to. Start by getting all list items in the Web Part Gallery, and then find the Web Part that was just uploaded.
                var list = clientContext.Web.Lists.GetByTitle("Web Part Gallery");
                CamlQuery camlQuery = CamlQuery.CreateAllItemsQuery(100);
                Microsoft.SharePoint.Client.ListItemCollection items = list.GetItems(camlQuery);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
                foreach (var item in items)
                {
                    // Create new group.
                    if (item["FileLeafRef"].ToString().ToLowerInvariant() == "userprofileinformation.webpart")
                    {
                        item["Group"] = "add-in Script Part";
                        item.Update();
                        clientContext.ExecuteQuery();
                    }
                }

                lblStatus.Text = string.Format("add-in script part has been added to Web Part Gallery. You can find 'User Profile Information' script part under 'App Script Part' group in the <a href='{0}'>host web</a>.", spContext.SPHostUrl.ToString());
            }
        }
```

## <a name="additional-resources"></a><span data-ttu-id="afda8-142">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="afda8-142">Additional resources</span></span>
<span data-ttu-id="afda8-143"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="afda8-143"></span></span>

- [<span data-ttu-id="afda8-144">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="afda8-144">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [<span data-ttu-id="afda8-145">Anpassen der Benutzeroberfläche der SharePoint-Benutzeroberfläche mithilfe von JavaScript</span><span class="sxs-lookup"><span data-stu-id="afda8-145">Customize your SharePoint site UI by using JavaScript</span></span>](Customize-your-SharePoint-site-UI-by-using-JavaScript.md)
