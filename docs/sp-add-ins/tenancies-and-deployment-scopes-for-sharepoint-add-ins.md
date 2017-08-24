
# <a name="tenancies-and-deployment-scopes-for-sharepoint-add-ins"></a><span data-ttu-id="0f083-101">Mandantschaften und Bereitstellungsbereiche von Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="0f083-101">Tenancies and deployment scopes for SharePoint Add-ins</span></span>
 <span data-ttu-id="0f083-102">Lernen Sie das Konzept von Mandantschaften und die Unterschiede zwischen der Bereitstellung von SharePoint-Add-Ins im Mandantenbereich und im Webbereich kennen.</span><span class="sxs-lookup"><span data-stu-id="0f083-102">Learn about the concept of tenancies and the differences between deploying SharePoint Add-ins at tenant scope and web scope.</span></span>
 

 <span data-ttu-id="0f083-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="0f083-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="tenancies-and-add-in-scope"></a><span data-ttu-id="0f083-106">Mandantschaften und Add-In-Bereich</span><span class="sxs-lookup"><span data-stu-id="0f083-106">Tenancies and add-in scope</span></span>
<span data-ttu-id="0f083-107"><a name="AppScope"> </a></span><span class="sxs-lookup"><span data-stu-id="0f083-107"></span></span>

<span data-ttu-id="0f083-p102">Einem SharePoint-Mandanten ist ein Satz von Websitesammlungen in einer SharePoint-Farm oder in SharePoint Online zugeordnet. In SharePoint Online gehören die Websitesammlungen zu einem einzelnen Kundenkonto. In einer SharePoint-Farm kann es sich um alle Websitesammlungen in einer SharePoint-Webanwendung bzw. eine Teilmenge davon oder auch um einen Satz von Websitesammlungen aus mehreren Webanwendungen in der Farm handeln. Ein Mandant kann genau wie eine SharePoint-Webanwendung über einen SharePoint-Add-In-Add-In-Katalog verfügen.</span><span class="sxs-lookup"><span data-stu-id="0f083-p102">A SharePoint tenancy is a set of site collections in either a SharePoint farm or in SharePoint Online. In SharePoint Online, the site collections belong to a single customer account. In a SharePoint farm, the site collections can be all the site collections in a SharePoint web application or a subset of them, or it can be a set of site collections from across multiple web applications in the farm. A tenancy can have a SharePoint Add-in add-in catalog just as a SharePoint web application can.</span></span>
 

 
<span data-ttu-id="0f083-p103">Einem SharePoint-Add-In ist ein Add-In-Bereich zugewiesen. Die beiden möglichen Add-In-Bereiche sindWebbereich oderMandantenbereich. Der Unterschied stellt keine interne Eigenschaft des Add-Ins dar, und Sie als Entwickler können den Bereich Ihres Add-Ins nicht festlegen. Die Entscheidung wird von Mandantenadministratoren als Nebeneffekt der Installationsart des Add-Ins getroffen. Nachdem ein Add-In in den Add-In-Katalog eines Mandanten hochgeladen wurde, steht sie sofort zur Installation auf einzelnen Websites innerhalb des Mandanten zur Verfügung. Auf diese Weise installierte Add-Ins gelten im Webbereich. Mandantenadministratoren haben jedoch auch eine andere Möglichkeit. Sie können eine Batchinstallation des Add-Ins auf einer Untermenge von Websites des Mandanten vornehmen. Auf diese Weise installierte Add-Ins gelten im Mandantenbereich. Der Mandantenadministrator kann mithilfe einer Liste von verwalteten Pfaden, Websitevorlagen oder Websitesammlungen angeben, auf welchen Websites das Add-In installiert wird. Ein per Batch installiertes Add-In kann nur von einem Mandantenadministrator deinstalliert werden. Wenn der Mandantenadministrator das Add-In deinstalliert, wird es von allen Websites des Mandanten deinstalliert. Benutzer können ein per Batch installiertes Add-In nicht auf einzelnen Websites deinstallieren. Dasselbe gilt für die Aktualisierung von per Batch installierten Add-Ins: nur ein Mandantenadministrator kann dies tun, und das Add-In wird per Batchupdate auf allen Websites des Mandanten aktualisiert, auf denen es installiert ist.</span><span class="sxs-lookup"><span data-stu-id="0f083-p103">A SharePoint Add-in has an add-in scope. The two possible add-in scopes are web scope ortenant scope. The difference is not an intrinsic property of the add-in, and you, the developer, do not decide what the scope of your add-in is. The decision is made by tenant administrators as a side effect of how the add-in is installed. After an add-in is uploaded to the add-in catalog of a tenancy, it is immediately available to be installed on websites within the tenancy on a website-by-website basis. Add-ins that are installed this way have web scope. Tenant administrators have another option, however. They can choose to batch install the add-in to a subset of websites within the tenancy. Add-ins that are installed in this way have tenant scope. The tenant admin can specify which websites the add-in is installed to by means of a list of managed paths, a list of site templates, or a list of site collections. An add-in that has been batch-installed can only be uninstalled by a tenant administrator. When the tenant admin uninstalls the add-in, it is uninstalled from every website in the tenancy. Users can't uninstall a batch-installed add-in on a website-by-website basis. The same principle applies to updating a batch-installed add-in: only a tenant administrator can do it, and it is batch-updated on every website in the tenancy where it is installed.</span></span>
 

 
<span data-ttu-id="0f083-p104">Bei der Batchinstallation eines Add-Ins, das ein Add-In-Web enthält, wird nur ein einzelnes Add-In-Web erstellt und von allen Hostwebsites verwendet, auf denen das Add-In installiert wird. Das Add-In-Web befindet sich in der Websitesammlung des Unternehmenskatalogs.</span><span class="sxs-lookup"><span data-stu-id="0f083-p104">If an add-in that includes an add-in web is batch-installed, only one add-in web is created and it is shared by all the host websites on which the add-in is installed. The add-in web is located in the site collection of the organization's add-in catalog.</span></span>
 

 
<span data-ttu-id="0f083-128">Wenn neue Websitesammlungen in der Mandantschaft erstellt werden, werden Add-Ins, die zuvor im Batch installiert wurden, automatisch in der neuen Websitesammlung installiert.</span><span class="sxs-lookup"><span data-stu-id="0f083-128">When new site collections are created in the tenancy, add-ins that were previously batch-installed are automatically installed on the new site collection.</span></span>
 

 

 <span data-ttu-id="0f083-p105">**Hinweis** Der Add-In-Bereich sollte nicht mit dem Featurebereich verwechselt werden. Der Featurebereich bestimmt, wo die Elemente in einem Feature bereitgestellt werden. Mögliche Werte sind z. B. **Farm**, **WebApplication**, **Website** (d. h. Websitesammlung) und **Web**. Nur **Web** ist für Features in SharePoint-Add-Ins zulässig (sowohl Hostweb-Features als auch Features in einer WSP-Datei in einem Add-In-Paket). Der Add-In-Bereich sollte ebenfalls nicht mit den Add-In-Berechtigungsstufen verwechselt werden. SharePoint-Add-Ins können Berechtigungen für alle oder ausgewählte Teile von SharePoint-Inhalten auf der Listen-, Web-, Websitesammlungs- und Mandantenebene anfordern. Durch das Installieren eines Add-Ins mit Mandantenbereich erhält das Add-In weder zusätzliche Berechtigungen noch werden wesentliche Bedingungen des SharePoint-Sicherheitsmodells außer Kraft gesetzt. Weitere Informationen zu Add-In-Berechtigungen finden Sie unter [Add-In Berechtigungen in SharePoint](add-in-permissions-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="0f083-p105">**Note**  Add-in scope should not be confused with Feature scope. Feature scope determines where the elements in a Feature are deployed. The possibilities include  **Farm**,  **WebApplication**,  **Site** (that is, site collection), and **Web**. Only  **Web** is permitted for Features in SharePoint Add-ins (both host web Features and Features inside a .wsp in an add-in package).Add-in scope should also not be confused with add-in permission levels. SharePoint Add-ins can request permissions to all or selected parts of SharePoint content at the levels of list, web, site collection, and tenancy. Installing an add-in with tenant scope does not give it permissions that it would not otherwise have, nor does it cancel key provisions of the SharePoint security model. For more information about add-in permissions, see  [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint-2013).</span></span>
 


## <a name="limitations-of-tenant-scoped-add-ins"></a><span data-ttu-id="0f083-136">Einschränkungen für Add-Ins mit Mandantenbereich</span><span class="sxs-lookup"><span data-stu-id="0f083-136">Limitations of tenant-scoped add-ins</span></span>
<span data-ttu-id="0f083-137"><a name="Tenant"> </a></span><span class="sxs-lookup"><span data-stu-id="0f083-137"></span></span>

<span data-ttu-id="0f083-138">Die folgenden Arten von Add-Ins können nicht per Batch installiert werden:</span><span class="sxs-lookup"><span data-stu-id="0f083-138">The following kinds of add-ins cannot be batch-installed:</span></span>
 

 

- <span data-ttu-id="0f083-p106">Add-Ins, die eine benutzerdefinierte Aktion für das Menüband enthalten. (Als Menüelemente bereitgestellte benutzerdefinierte Aktionen sind zulässig.)</span><span class="sxs-lookup"><span data-stu-id="0f083-p106">Add-ins that contain a custom action for the ribbon. (Custom actions that are deployed as menu items are allowed.)</span></span>
    
 
- <span data-ttu-id="0f083-141">Add-Ins, die ein Add-In-Webpart enthalten.</span><span class="sxs-lookup"><span data-stu-id="0f083-141">Add-ins that contain an add-in part.</span></span> 
    
 
<span data-ttu-id="0f083-142">Denken Sie außerdem daran, dass die Installation mit Mandantenbereich in der Office 365 Small Business Premium-Version von SharePoint Online nicht möglich ist.</span><span class="sxs-lookup"><span data-stu-id="0f083-142">In addition, note again that installation with tenant scope is not possible in the Office 365 Small Business Premium version of SharePoint Online.</span></span>
 

 

## <a name="how-to-install-uninstall-and-update-an-add-in-on-multiple-websites-in-a-tenancy"></a><span data-ttu-id="0f083-143">Installieren, Deinstallieren und Aktualisieren eines Add-Ins auf mehreren Websites eines Mandanten</span><span class="sxs-lookup"><span data-stu-id="0f083-143">How to install, uninstall, and update an add-in on multiple websites in a tenancy</span></span>
<span data-ttu-id="0f083-144"><a name="Web"> </a></span><span class="sxs-lookup"><span data-stu-id="0f083-144"></span></span>

<span data-ttu-id="0f083-145">Add-Ins aus dem Office Store oder aus einem Add-In-Katalog können von Mandantenadministratoren mit dem folgenden Verfahren auf mehreren Websites eines Mandanten installiert, deinstalliert und aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="0f083-145">Regardless of whether an add-in is installed from the Office Store or from an add-in catalog, tenant admins can install it to multiple websites in a tenancy, uninstall it, and update it by using the following procedures.</span></span>
 

 

### <a name="to-install-a-sharepoint-add-in-to-multiple-websites"></a><span data-ttu-id="0f083-146">So installieren Sie ein SharePoint-Add-In auf mehreren Websites</span><span class="sxs-lookup"><span data-stu-id="0f083-146">To install a SharePoint Add-in to multiple websites</span></span>


1. <span data-ttu-id="0f083-147">Navigieren Sie zur Seite **Websiteinhalte** der Website für den Unternehmenskatalog.</span><span class="sxs-lookup"><span data-stu-id="0f083-147">Navigate to the **Site Contents** page of the corporate catalog website.</span></span>
    
 
2. <span data-ttu-id="0f083-148">Wählen Sie **Add-In hinzufügen** aus, und installieren Sie das Add-In so, wie Sie bei jeder anderen SharePoint-Website vorgehen würden.</span><span class="sxs-lookup"><span data-stu-id="0f083-148">Select **Add an add-in** and install the add-in just as you would on any other SharePoint website.</span></span>
    
 
3. <span data-ttu-id="0f083-p107">Nachdem das Add-In installiert wurde, zeigen Sie auf der Seite **Websiteinhalte** auf den Link zu dem Add-In. Ein „**...**“-Link wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0f083-p107">After the add-in is installed, hover over the link to the add-in in the **Site Contents** page. A " **...**" link appears.</span></span>
    
 
4. <span data-ttu-id="0f083-151">Wählen Sie den Link aus. Ein Popup wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0f083-151">Select the link, and a callout appears.</span></span>
    
 
5. <span data-ttu-id="0f083-152">Wählen Sie im Menü den Befehl **Bereitstellung** aus.</span><span class="sxs-lookup"><span data-stu-id="0f083-152">Select **Deployment** on the menu.</span></span>
    
 
6. <span data-ttu-id="0f083-p108">Geben Sie auf der Benutzeroberfläche für die Bereitstellung die Websitesammlungen an, in denen das Add-In installiert werden soll. Sie können nach verwalteten Pfaden, Websitevorlagen oder URLs filtern.</span><span class="sxs-lookup"><span data-stu-id="0f083-p108">Use the deployment UI that opens to specify the site collections to which you want the add-in installed. You can filter by managed paths, site templates, or URLs. The filters have a logical "OR" relationship: the add-in is installed to the union of all the site collections that pass any one or more of the filters.</span></span>
    
 
7. <span data-ttu-id="0f083-156">Wählen Sie **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="0f083-156">Select **OK**.</span></span>
    
 

### <a name="to-uninstall-a-batch-installed-sharepoint-add-in"></a><span data-ttu-id="0f083-157">So deinstallieren Sie ein per Batch installiertes SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="0f083-157">To uninstall a batch-installed SharePoint Add-in</span></span>


1. <span data-ttu-id="0f083-158">Navigieren Sie zur Seite **Websiteinhalte** der Website für den Unternehmenskatalog.</span><span class="sxs-lookup"><span data-stu-id="0f083-158">Navigate to the **Site Contents** page of the corporate catalog website.</span></span>
    
 
2. <span data-ttu-id="0f083-p109">Zeigen Sie auf der Seite **Websiteinhalte** auf den Link zu dem Add-In. Ein „**...**“-Link wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0f083-p109">Hover over the link to the add-in in the **Site Contents** page. A " **...**" link appears.</span></span>
    
 
3. <span data-ttu-id="0f083-161">Wählen Sie den Link aus. Ein Popup wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0f083-161">Select the link, and a callout appears.</span></span>
    
 
4. <span data-ttu-id="0f083-162">Wählen Sie im Popup **Entfernen** aus.</span><span class="sxs-lookup"><span data-stu-id="0f083-162">Select **Remove** on the callout.</span></span>
    
 

### <a name="to-update-a-batch-installed-sharepoint-add-in"></a><span data-ttu-id="0f083-163">So aktualisieren Sie ein per Batch installiertes SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="0f083-163">To update a batch-installed SharePoint Add-in</span></span>


1. <span data-ttu-id="0f083-p110">Navigieren Sie zur Seite **Websiteinhalte** der Website für den Unternehmenskatalog. Wenn für ein Add-In ein Update verfügbar ist, wird neben dem Add-In eine Meldung angezeigt. Es wird ein Link angezeigt, um das Add-In zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="0f083-p110">Navigate to the **Site Contents** page of the corporate catalog website. If there is an update available for an add-in, a message appears beside the add-in. There will be a link to update the add-in.</span></span>
    
 
2. <span data-ttu-id="0f083-167">Klicken Sie auf den Link, um das Add-In zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="0f083-167">Click the link to update the add-in.</span></span>
    
 
3. <span data-ttu-id="0f083-168">Wenn Sie zur Genehmigung der Berechtigungsanforderungen des Add-Ins aufgefordert werden, wählen Sie **Vertrauen** aus.</span><span class="sxs-lookup"><span data-stu-id="0f083-168">When you are prompted to approve the permission requests of the add-in, choose **Trust It**.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="0f083-169">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="0f083-169">Additional resources</span></span>
<span data-ttu-id="0f083-170"><a name="SP15tenancies_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0f083-170"></span></span>


-  [<span data-ttu-id="0f083-171">Veröffentlichen von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0f083-171">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="0f083-172">Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0f083-172">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 
-  [<span data-ttu-id="0f083-173">Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen</span><span class="sxs-lookup"><span data-stu-id="0f083-173">Deploying and installing SharePoint Add-ins: methods and options</span></span>](deploying-and-installing-sharepoint-add-ins-methods-and-options)
    
 
-  [<span data-ttu-id="0f083-174">Aktualisierungsverfahren für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0f083-174">SharePoint Add-ins update process</span></span>](sharepoint-add-ins-update-process)
    
 

