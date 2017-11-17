---
title: Speichern, Herunter- und Hochladen einer SharePoint-Website als Vorlage
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2e637172-ddac-4a70-bd77-55a1645a3db1
ms.openlocfilehash: f018af03acc5536b9abc4abe244664f9d9bed4ab
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="save-download-and-upload-a-sharepoint-site-as-a-template"></a><span data-ttu-id="6f717-102">Speichern, Herunter- und Hochladen einer SharePoint-Website als Vorlage</span><span class="sxs-lookup"><span data-stu-id="6f717-102">Save, download, and upload a SharePoint site as a template</span></span>
<span data-ttu-id="6f717-p101">Hier erfahren Sie, wie Sie mithilfe von SharePoint-Websitevorlagen stabile Anwendungen entwerfen und erstellen. Sie können zuverlässige SharePoint-Anwendungen entwerfen und erstellen, die mehrere Datenquellen, benutzerorientierte Ansichten und Formulare, hochgradig angepasste Workflows u. v. a. m. beinhalten. Sobald Sie eine Geschäftslösungs-Website erstellt haben, können Sie diese direkt in der SharePoint-Umgebung verwenden. Sie können die Lösung aber auch in eine Vorlage umwandeln und in einer anderen Umgebung bereitstellen und für andere Benutzer verfügbar machen, sodass sie als Vorlage zum Erstellen neuer Websites verwendet oder zur weiteren Entwicklung in Visual Studio weitergegeben werden kann.</span><span class="sxs-lookup"><span data-stu-id="6f717-p101">Learn how to design and build robust applications by using SharePoint site templates. You can design and build robust SharePoint applications that include a rich set of data sources, customer-facing views and forms, highly customized workflows, and more. Once you've built your business solution site, you can start to use it immediately in your SharePoint environment. Or, you can turn your solution into a template and deploy it in another environment, make it available to users so they can create new sites from it, or hand it off for additional development in Visual Studio.</span></span>
  
    
    


## <a name="what-is-a-sharepoint-site-template"></a><span data-ttu-id="6f717-107">Was ist eine SharePoint-Websitevorlage?</span><span class="sxs-lookup"><span data-stu-id="6f717-107">What is a SharePoint site template?</span></span>
<span data-ttu-id="6f717-108"><a name="bkmk_WhatIsTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="6f717-108"></span></span>

<span data-ttu-id="6f717-p102">SharePoint-Websitevorlagen sind vorkonfigurierte Definitionen, die einem bestimmten Geschäftszweck dienen. Sie können auf Grundlage dieser Vorlagen Ihre eigene SharePoint-Website erstellen und die Website dann beliebig anpassen. Wahrscheinlich sind Sie mit den Standardwebsitevorlagen wie Teamwebsite, Projektwebsite und Communitywebsite vertraut.</span><span class="sxs-lookup"><span data-stu-id="6f717-p102">SharePoint site templates are prebuilt definitions designed around a particular business need. You can use these templates as they are to create your own SharePoint site, and then customize the site as much as you want. You're probably familiar with the default site templates, such as Team Site, Project Site, and Communities Site.</span></span>
  
    
    
<span data-ttu-id="6f717-p103">Zusätzlich zu den Standardvorlagen können Sie auf Basis einer Website, die Sie erstellt und angepasst haben, Ihre eigene Websitevorlage erstellen. Dies ist ein nützliches Feature, mit dem Sie eine benutzerdefinierte Lösung erstellen und diese dann für Ihre Kollegen, das gesamte Unternehmen oder andere Unternehmen freigeben können. Sie können die Website auch verpacken und in einer anderen Umgebung oder Anwendung wie Visual Studio öffnen und sie auch dort anpassen.</span><span class="sxs-lookup"><span data-stu-id="6f717-p103">In addition to the default templates, you can create your own site template based on a site you've created and customized. This is a powerful feature that allows you to create a custom solution and then share that solution with your peers, the broader organization, or outside organizations. You can also package the site and open it in another environment or application such as Visual Studio and also customize it there.</span></span>
  
    
    
<span data-ttu-id="6f717-p104">Das Umwandeln einer angepassten Website bzw. einer Geschäftslösung in eine Vorlage stellt eine äußerst hilfreiche und leistungsstarke Funktion dar. Sobald Sie Ihre Lösung als Vorlage verpacken, werden Sie erkennen, welches Potenzial SharePoint als Plattform für Geschäftsanwendungen bietet. Die Option zur Erstellung einer Websitevorlage macht all dies möglich.</span><span class="sxs-lookup"><span data-stu-id="6f717-p104">Turning your customized site or business solution into a template is an extremely useful and very powerful capability. Once you start to package your solution as a template, you begin to realize the potential of SharePoint as a platform for business applications. The site template option makes all of this possible.</span></span>
  
    
    
<span data-ttu-id="6f717-p105">Beim Speichern der Website als Vorlage wird eine WSP-Datei (Web Solution Package) erstellt. Dabei handelt es sich um eine CAB-Datei mit dem Lösungsmanifest. Die erstellte Lösung wird im Lösungskatalog für die SharePoint-Websitesammlung gespeichert. Sobald Sie die Vorlage speichern, wird eine Lösungsdatei (WSP-Datei) erstellt und im Lösungskatalog gespeichert. Dort können Sie die Lösung herunterladen oder aktivieren.</span><span class="sxs-lookup"><span data-stu-id="6f717-p105">When you save your site as a template, you create a Web Solution Package, or WSP. A WSP is a CAB file that uses the solution manifest. The solution that you create is stored in the solutions gallery for the SharePoint site collection. Once you save the template, a solution file (.wsp) is created and stored in the solutions gallery where you can download or activate the solution.</span></span>
  
    
    

> <span data-ttu-id="6f717-122">**Hinweis:** Die erstelle WSP-Datei ist eine teilweise vertrauenswürdige Benutzerlösung, die über das gleiche deklarative Format wie eine voll vertrauenswürdige SharePoint-Lösung verfügt.</span><span class="sxs-lookup"><span data-stu-id="6f717-122">**Note** The WSP you create is a partial trust user solution that has the same declarative format as a full trust SharePoint solution. However, it does not support the full extent of feature element types that are supported by full trust solutions.</span></span> <span data-ttu-id="6f717-123">Er werden jedoch nicht alle Feature-Elementtypen von vollständig vertrauenswürdigen Lösungen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="6f717-123">The WSP you create is a partial trust user solution that has the same declarative format as a full trust SharePoint solution. However, it does not support the full extent of feature element types that are supported by full trust solutions.</span></span> 
  
    
    


### <a name="what-gets-saved-in-a-template"></a><span data-ttu-id="6f717-124">Was wird in einer Vorlage gespeichert?</span><span class="sxs-lookup"><span data-stu-id="6f717-124">What gets saved in a template?</span></span>

<span data-ttu-id="6f717-p107">Wenn Sie eine SharePoint-Website als Vorlage speichern, speichern Sie das gesamte Framework der Website: die Listen und Bibliotheken, Ansichten und Formulare sowie die Workflows. Zusätzlich zu diesen Komponenten können Sie die Inhalte der Website in die Vorlage einschließen, z. B. die in den Dokumentbibliotheken gespeicherten Dokumente. Dies könnte nützlich sein, um Benutzern zum Einstieg Beispielinhalte zur Verfügung zu stellen. Beachten Sie, dass dies auch die Größe Ihrer Vorlage über die 50 MB Standardgrenze für Websitevorlagen hinaus erhöhen könnte.</span><span class="sxs-lookup"><span data-stu-id="6f717-p107">When you save a SharePoint site as a template, you're saving the overall framework of the site — its lists and libraries, views and forms, and workflows. In addition to these components, you can include the contents of the site in the template; for example, the documents stored in the document libraries. This could be useful to provide sample content for users to get started with. Consider that this could also increase the size of your template beyond the default 50-MB site template limit.</span></span>
  
    
    
<span data-ttu-id="6f717-p108">Der Großteil der Objekte in einer Website werden in die Vorlage eingeschlossen und von dieser unterstützt. Es gibt jedoch einige Objekte und Features, die nicht unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="6f717-p108">Most of the objects in a site are included and supported by the template. However, there are several objects and features that are not supported.</span></span> 
  
    
    

- <span data-ttu-id="6f717-131">**Unterstützt** Listen, Bibliotheken, externe Listen, Datenquellenverbindungen, Listenansichten und Datenansichten, benutzerdefinierte Formulare, Workflows, Inhaltstypen, benutzerdefinierte Aktionen, Navigation, Websiteseiten, Gestaltungsvorlagen, Module und Webvorlagen</span><span class="sxs-lookup"><span data-stu-id="6f717-131">**Supported** Lists, libraries, external lists, data source connections, list views and data views, custom forms, workflows, content types, custom actions, navigation, site pages, master pages, modules, and web templates.</span></span>
    
  
- <span data-ttu-id="6f717-132">**Nicht unterstützt** Angepasste Berechtigungen, ausgeführte Workflowinstanzen, Versionsverlauf von Listenelementen, mit ausgeführten Workflows verknüpfte Workflowaufgaben, Personen- oder Gruppenfeldwerte, Taxonomiefeldwerte, Veröffentlichungsseiten und Veröffentlichungswebsites, Meine Websites, Features zum Anheften, SharePoint-Add-Ins und Remoteereignisempfänger</span><span class="sxs-lookup"><span data-stu-id="6f717-132">**Unsupported** Customized permissions, running workflow instances, list item version history, workflow tasks associated with running workflows, people or group field values, taxonomy field values, publishing pages and publishing sites, My Sites, stapled features, SharePoint Add-ins, and remote event receivers.</span></span>
    
    > <span data-ttu-id="6f717-133">**Hinweis:** Für Veröffentlichungswebsites, können Sie die Websitevorlagen-Definition verwenden.</span><span class="sxs-lookup"><span data-stu-id="6f717-133">**Note** For publishing sites, you can use site definition templates. For more information, see  Additional resources at the end of this topic.</span></span> <span data-ttu-id="6f717-134">Weitere Informationen finden Sie in den am Ende dieses Themas unter [Zusätzliche Ressourcen](save-download-and-upload-a-sharepoint-site-as-a-template.md#bkmk_additionalresources).</span><span class="sxs-lookup"><span data-stu-id="6f717-134">For publishing sites, you can use site definition templates. For more information, see [Additional resources](save-download-and-upload-a-sharepoint-site-as-a-template.md#bkmk_additionalresources) at the end of this topic.</span></span>

### <a name="what-can-you-do-with-sharepoint-templates"></a><span data-ttu-id="6f717-135">Was können Sie mit SharePoint-Vorlagen tun?</span><span class="sxs-lookup"><span data-stu-id="6f717-135">What can you do with SharePoint templates?</span></span>

<span data-ttu-id="6f717-p110">Das Speichern einer Website als Vorlage stellt ein sehr nützliches Feature dar, da es so viele Verwendungsmöglichkeiten für benutzerdefinierte Websites eröffnet. Im Folgenden sind die unmittelbaren Vorteile der Speicherung einer Website als Vorlage aufgelistet:</span><span class="sxs-lookup"><span data-stu-id="6f717-p110">Saving a site as a template is a powerful feature because it offers so many uses of custom sites. Here are the immediate benefits you get from saving a site as a template:</span></span>
  
    
    

- <span data-ttu-id="6f717-p111">**Unmittelbare Lösungsbereitstellung** Speichern und aktivieren Sie die Vorlage im Lösungskatalog, und erlauben Sie anderen Mitarbeitern, auf Basis dieser Vorlage neue Websites zu erstellen. Sie können sie auswählen und dann auf dieser Grundlage eine neue Website erstellen, welche die Komponenten der Website, ihre Struktur, ihre Workflows und mehr erbt. Sie benötigen Visual Studio nicht zum Erstellen Ihrer Lösung, müssen nicht direkt auf den Server zugreifen und Serveradministratorbefehle ausführen. Speichern Sie die Website einfach als Vorlage, aktivieren Sie sie und los geht's.</span><span class="sxs-lookup"><span data-stu-id="6f717-p111">**Deploy solutions immediately** Save and activate the template in the solutions gallery and let other employees create new sites from this template. You can select it, and then create a new site from it, which will inherit the components of the site, its structure, workflows, and more. You don't need Visual Studio to create your solution, and you have to access the server directly and run server administrator commands. Just save the site as a template, activate it, and off you go.</span></span>
    
  
- <span data-ttu-id="6f717-p112">**Portabilität** Zusätzlich zur Bereitstellung einer benutzerdefinierten Lösung in Ihrer Umgebung können Sie die WSP-Datei herunterladen, sie unterwegs verwenden und in einer anderen SharePoint-Umgebung bereitstellen. Sämtliche Websiteanpassungen Ihrerseits werden bequem in einer Datei gespeichert.</span><span class="sxs-lookup"><span data-stu-id="6f717-p112">**Portability** In addition to deploying a custom solution in your environment, you can download the .wsp file, take it on the road, and deploy it in another SharePoint environment. All of your site customization is conveniently stored in one file.</span></span>
    
  
- <span data-ttu-id="6f717-p113">**Erweiterbarkeit** Sie können Ihre angepasste Website als Weblösungspaket in Visual Studio öffnen, zusätzliche Entwicklungsanpassungen an der Vorlage vornehmen und sie dann in SharePoint bereitstellen. SharePoint-Websiteentwicklung kann daher einen Lösungslebenszyklus (Entwicklung, Staging und Aufnahme in die Produktion) durchlaufen, der SharePoint Designer 2013, Visual Studio und den Browser umfasst.</span><span class="sxs-lookup"><span data-stu-id="6f717-p113">**Extensibility** As a Web Solution Package, you can open your customized site in Visual Studio, perform additional development customization to the template, and then deploy it to SharePoint. SharePoint site development, as a result, can go through a solution life cycle (develop, stage, and put into production) that includes SharePoint Designer 2013, Visual Studio, and the browser.</span></span>
    
  
<span data-ttu-id="6f717-p114">Wenn Sie mit der Erstellung benutzerdefinierter Websites in SharePoint beginnen, entdecken Sie noch mehr Vorteile der Umwandlung Ihrer Website in eine Lösung, die im gesamten Unternehmen verwendet werden kann. Die grundlegenden Schritte beim Arbeiten mit Websitevorlagen sind folgende:</span><span class="sxs-lookup"><span data-stu-id="6f717-p114">As you begin to create custom sites in SharePoint, you'll discover even more benefits to turning your site into a solution that can be made portable across the organization. The basic steps to working with site templates are as follows:</span></span>
  
    
    

- <span data-ttu-id="6f717-148">Speichern Sie eine Website als Vorlage im Lösungskatalog.</span><span class="sxs-lookup"><span data-stu-id="6f717-148">Save a site as a template to the solutions gallery.</span></span>
    
  
- <span data-ttu-id="6f717-149">Laden Sie die Websitevorlage aus dem Lösungskatalog in eine WSP-Datei herunter.</span><span class="sxs-lookup"><span data-stu-id="6f717-149">Download the site template from the solutions gallery to a .wsp file.</span></span>
    
  
- <span data-ttu-id="6f717-150">Laden Sie die WSP-Datei in den Lösungskatalog hoch.</span><span class="sxs-lookup"><span data-stu-id="6f717-150">Upload the .wsp file to the solutions gallery.</span></span>
    
  
<span data-ttu-id="6f717-151">Nachdem Sie eine Websitevorlage im Lösungskatalog hinzugefügt haben und die Vorlage aktiviert wurde, steht die Vorlage auf der Registerkarte **Benutzerdefiniert** im Abschnitt **Vorlagenauswahl** auf der Seite **Neue SharePoint-Website** zur Auswahl zur Verfügung, wenn Sie das nächste Mal eine Website oder Unterwebsite erstellen.</span><span class="sxs-lookup"><span data-stu-id="6f717-151">After you add a site template to the solutions gallery and the template is activated, the next time that you create a site or subsite, the template is available for selection in the **Custom** tab of the **Template Selection** section on the **New SharePoint Site** page.</span></span>
  
    
    

## <a name="save-a-site-as-a-template-to-the-solutions-gallery"></a><span data-ttu-id="6f717-152">Speichern einer Website als Vorlage im Lösungskatalog</span><span class="sxs-lookup"><span data-stu-id="6f717-152">Save a site as a template to the solutions gallery</span></span>
<span data-ttu-id="6f717-153"><a name="bkmk_SaveTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="6f717-153"></span></span>


1. <span data-ttu-id="6f717-154">Navigieren Sie zur Website auf oberster Ebene der Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="6f717-154">Navigate to the top-level site of your site collection.</span></span>
    
  
2. <span data-ttu-id="6f717-155">Klicken Sie auf **Einstellungen** und dann auf **Websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="6f717-155">Click **Settings**, and then click **Site Settings**.</span></span>
    
  
3. <span data-ttu-id="6f717-156">Klicken Sie im Bereich **Websiteaktionen** auf **Website als Vorlage speichern**.</span><span class="sxs-lookup"><span data-stu-id="6f717-156">In the **Site Actions** section, click **Save site as a template**.</span></span>
    
  
4. <span data-ttu-id="6f717-157">Geben Sie im Bild **Dateiname** einen Namen an, der für die Vorlage verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="6f717-157">Specify a name to use for the template file in the **File name** box.</span></span>
    
  
5. <span data-ttu-id="6f717-158">Geben Sie in den Feldern **Vorlagenname** und **Vorlagenbeschreibung** einen Namen und eine Beschreibung für die Vorlage an.</span><span class="sxs-lookup"><span data-stu-id="6f717-158">Specify a name and description for the template in the **Template name** and **Template description** boxes.</span></span>
    
  
6. <span data-ttu-id="6f717-159">Wenn Sie den Inhalt der Website in die Websitevorlage integrieren möchten, wählen Sie das Feld **Inhalte einschließen**.</span><span class="sxs-lookup"><span data-stu-id="6f717-159">To include the content of the site in the site template, select the **Include Content** box.</span></span>
    
    > <span data-ttu-id="6f717-160">**Hinweis:** Das Einbeziehen des Inhalts der Website kann die Größe die Vorlage erheblich erhöhen.</span><span class="sxs-lookup"><span data-stu-id="6f717-160">**Note:** Including the content of the site can increase the size of the template significantly.</span></span> <span data-ttu-id="6f717-161">Der Standardgrenzwert für eine Websitevorlage beträgt 50 MB, kann in Ihrer Organisation jedoch auch geringer sein.</span><span class="sxs-lookup"><span data-stu-id="6f717-161">The default size limit for a site template is 50 MB but might be less in your organization.</span></span> <span data-ttu-id="6f717-162">Sie können Inhalte immer ausschließen und dann später die benötigten Inhalte in die neue Website kopieren.</span><span class="sxs-lookup"><span data-stu-id="6f717-162">You can always exclude the content, and then copy what you need later into the new site.</span></span> <span data-ttu-id="6f717-163">Sie können auch den Grenzwert erhöhen.</span><span class="sxs-lookup"><span data-stu-id="6f717-163">Or, you can increase the size limit.</span></span> <span data-ttu-id="6f717-164">Wenn Sie den Grenzwert beispielsweise auf ein Maximum erhöhen möchten, verwenden Sie die folgende Stsadm-Befehlssyntax.</span><span class="sxs-lookup"><span data-stu-id="6f717-164">For example, to increase the limit to the maximum allowed, use the following Stsadm command syntax.</span></span> >  `stsadm -o setproperty -pn max-template-document-size -pv 524288000`
7. <span data-ttu-id="6f717-165">Klicken Sie auf **OK**, um die Vorlage zu speichern.</span><span class="sxs-lookup"><span data-stu-id="6f717-165">Click **OK** to save the template.</span></span>
    
    <span data-ttu-id="6f717-166">Wenn alle Komponenten auf der Website gültig sind, wird die Vorlage erstellt, und es wird die Meldung angezeigt, dass der Vorgang erfolgreich abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="6f717-166">If all of the components on the site are valid, the template is created, and you see a message that states "Operation Completed Successfully."</span></span>
    
  
8. <span data-ttu-id="6f717-167">Führen Sie einen der folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="6f717-167">Do one of the following:</span></span>
    
  - <span data-ttu-id="6f717-168">Klicken Sie auf **OK**, um zu Ihrer Website zurückzukehren.</span><span class="sxs-lookup"><span data-stu-id="6f717-168">To return to your site, click **OK**.</span></span>
    
  
  - <span data-ttu-id="6f717-169">Klicken Sie auf **Lösungskatalog**, um direkt zur Websitevorlage zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="6f717-169">To go directly to the site template, click **Solutions Gallery**.</span></span>
    
  

## <a name="download-the-site-template-from-the-solutions-gallery-to-a-file"></a><span data-ttu-id="6f717-170">Herunterladen der Websitevorlage aus dem Lösungskatalog in eine Datei</span><span class="sxs-lookup"><span data-stu-id="6f717-170">Download the site template from the solutions gallery to a file</span></span>
<span data-ttu-id="6f717-171"><a name="bkmk_DownloadTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="6f717-171"></span></span>


1. <span data-ttu-id="6f717-172">Navigieren Sie zur Website auf oberster Ebene der Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="6f717-172">Navigate to the top-level site of your site collection.</span></span>
    
  
2. <span data-ttu-id="6f717-173">Klicken Sie auf **Einstellungen** und dann auf **Websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="6f717-173">Click **Settings**, and then click **Site Settings**.</span></span>
    
  
3. <span data-ttu-id="6f717-174">Klicken Sie im Abschnitt **Web-Designer-Kataloge** auf **Lösungen**.</span><span class="sxs-lookup"><span data-stu-id="6f717-174">In the **Web Designer Galleries** section, click **Solutions**.</span></span>
    
  
4. <span data-ttu-id="6f717-175">Wenn es erforderlich ist, die Lösung zu aktivieren, markieren Sie sie und klicken Sie in der **Befehle**-Gruppe auf **Aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="6f717-175">If it's necessary to activate the solution, select it, and in the **Commands** group, click **Activate**. Then, on the Activate Solution Confirmation screen, in the Commands group, click Activate.</span></span> <span data-ttu-id="6f717-176">Klicken Sie dann im Bildschirm **Lösungsaktivierung bestätigen** der **Befehle**-Gruppe auf **Aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="6f717-176">If it's necessary to activate the solution, select it, and in the **Commands** group, click **Activate**. Then, on the **Activate Solution Confirmation** screen, in the Commands group, click Activate.</span></span>
    
  
5. <span data-ttu-id="6f717-p117">Klicken Sie zum Herunterladen der Lösung im Lösungskatalog auf deren Name, und klicken Sie auf **Speichern**. Navigieren Sie dann im Dialogfeld **Speichern unter** zum Speicherort, an dem Sie die Lösung speichern möchten, klicken Sie auf **Speichern**, und klicken Sie dann auf **Schließen**.</span><span class="sxs-lookup"><span data-stu-id="6f717-p117">To download the solution, click its name in the solutions gallery, and click **Save**. Then, in the **Save As** dialog box, browse to the location where you want to save the solution, click **Save**, and then click **Close**.</span></span>
    
  

## <a name="upload-the-site-template-file-to-a-solutions-gallery"></a><span data-ttu-id="6f717-179">Hochladen der Websitevorlagendatei in einen Lösungskatalog</span><span class="sxs-lookup"><span data-stu-id="6f717-179">Upload the site template file to a solutions gallery</span></span>
<span data-ttu-id="6f717-180"><a name="bkmk_UploadTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="6f717-180"></span></span>


1. <span data-ttu-id="6f717-181">Navigieren Sie zur Website auf oberster Ebene der Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="6f717-181">Navigate to the top-level site of your site collection.</span></span>
    
  
2. <span data-ttu-id="6f717-182">Klicken Sie auf **Einstellungen** und dann auf **Websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="6f717-182">Click **Settings**, and then click **Site Settings**.</span></span>
    
  
3. <span data-ttu-id="6f717-183">Klicken Sie im Abschnitt **Web-Designer-Kataloge** auf **Lösungen**.</span><span class="sxs-lookup"><span data-stu-id="6f717-183">In the **Web Designer Galleries** section, click **Solutions**.</span></span>
    
  
4. <span data-ttu-id="6f717-p118">Klicken Sie zum Hochladen der Lösung in der Gruppe **Befehle** auf **Hochladen**, und klicken Sie dann im Dialogfeld **Dokument hinzufügen** auf **Durchsuchen**. Suchen Sie dann im Dialogfeld **Datei zum Hochladen auswählen** die Datei, klicken Sie auf **Öffnen**, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f717-p118">To upload the solution, in the **Commands** group, click **Upload**, and then in the **Add a Document** dialog box, click **Browse**. Then, in the **Choose File to Upload** dialog box, locate the file, select it, click **Open**, and then click **OK**.</span></span>
    
  
5. <span data-ttu-id="6f717-186">Klicken Sie zum Aktivieren der Lösung auf dem Bildschirm zur Bestätigung der Lösungsaktivierung in der Gruppe **Befehle** auf **Aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="6f717-186">To activate the solution, on the activate solution confirmation screen, in the **Commands** group, click **Activate**.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="6f717-187">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6f717-187">Additional resources</span></span>
<span data-ttu-id="6f717-188"><a name="bkmk_additionalresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6f717-188"></span></span>


-  <span data-ttu-id="6f717-189">
  [Websitetypen: WebTemplates und Websitedefinitionen](http://msdn.microsoft.com/en-us/library/ms434313.aspx)</span><span class="sxs-lookup"><span data-stu-id="6f717-189">[Site Types: WebTemplates and Site Definitions](http://msdn.microsoft.com/en-us/library/ms434313.aspx)</span></span>
    
  
-  <span data-ttu-id="6f717-190">
  [Grundlegendes zu packen und POST von Workflows in SharePoint](http://msdn.microsoft.com/en-us/library/jj819316%28v=office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="6f717-190">[Understanding how to package and deploy workflow in SharePoint](http://msdn.microsoft.com/en-us/library/jj819316%28v=office.15%29.aspx)</span></span>
    
  
-  <span data-ttu-id="6f717-191">
  [Farmlösungen in SharePoint erstellen](http://msdn.microsoft.com/en-us/library/jj163902%28v=office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="6f717-191">[Build farm solutions in SharePoint](http://msdn.microsoft.com/en-us/library/jj163902%28v=office.15%29.aspx)</span></span>
    
  
-  [<span data-ttu-id="6f717-192">Kopieren oder Verschieben einer Liste mithilfe einer Listenvorlage</span><span class="sxs-lookup"><span data-stu-id="6f717-192">Copy or move lists by using list templates</span></span>](http://office.com/redir/HA101782479.aspx)
    
  
-  [<span data-ttu-id="6f717-193">Kopieren oder Verschieben einer Bibliothek mithilfe einer Bibliotheksvorlage</span><span class="sxs-lookup"><span data-stu-id="6f717-193">Copy or move a library by using a library template</span></span>](http://office.com/redir/HA101814157.aspx)
    
  
-  [<span data-ttu-id="6f717-194">Kopieren oder Verschieben von Bibliotheksdateien mit "Öffnen" im Windows-Explorer</span><span class="sxs-lookup"><span data-stu-id="6f717-194">Copy or move library files by using Windows Explorer</span></span>](http://office.com/redir/HA101811182.aspx)
    
  

