# <a name="introduction"></a><span data-ttu-id="a50f5-101">Einführung</span><span class="sxs-lookup"><span data-stu-id="a50f5-101">Introduction</span></span>
<span data-ttu-id="a50f5-102">Die meisten SharePoint Online Mandanten behandelt die Datei open Erfahrung mit dem **strict** Objektmodell.</span><span class="sxs-lookup"><span data-stu-id="a50f5-102">Most of the SharePoint Online tenants handles the file open experience using the **strict** model.</span></span> <span data-ttu-id="a50f5-103">Daher alle Dateien, die potenziell Schaden (z. B. eine HTML-Datei mit dem Skript eingebettet) führen können nicht im Browser ausgeführt, aber heruntergeladen oder als unformatierten Inhalt (html Preview die moderne Benutzeroberfläche) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="a50f5-103">As a result, all files which can potentially cause harm (e.g. a html file having embedded script) are not executed in the browser but downloaded or shown as raw content (html preview in the modern user experience).</span></span> <span data-ttu-id="a50f5-104">Wenn Ihre Mandanten mit konfiguriert wurde die **permissive** modellieren, und klicken Sie dann die Datei öffnen Erfahrung führen Sie die Datei wird, beispielsweise eine HTML-Datei in einer Dokumentbibliothek ausgeführt und Seite im Browser angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="a50f5-104">If your tenant is configured using the **permissive** model then the file open experience will execute the file, for example a html file in a document library does get executed and page is shown in the browser.</span></span> <span data-ttu-id="a50f5-105">Würde strict dieser Datei heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="a50f5-105">In strict this file would be downloaded.</span></span>

<span data-ttu-id="a50f5-106">Die Standardeinstellung ist heute strict, und Sie können nicht bereits auf das Objektmodell permissive wechseln Ihres Mandanten.</span><span class="sxs-lookup"><span data-stu-id="a50f5-106">Today the default setting is strict, and you already cannot switch your tenant to the permissive model.</span></span> <span data-ttu-id="a50f5-107">Für Mandanten, die die letzten Schritte zu permissive gewechselt geändert werden: permissive Mandanten Modell wird als veraltet markiert, an dieser Stelle alle Mandanten werden umgestellt werden strikte.</span><span class="sxs-lookup"><span data-stu-id="a50f5-107">For tenants that switched to permissive in the past things will change: the tenant permissive model will be deprecated, at that point all tenants will be switched to strict.</span></span>


# <a name="is-my-tenant-impacted"></a><span data-ttu-id="a50f5-108">Betroffen Meine Mandanten ist davon?</span><span class="sxs-lookup"><span data-stu-id="a50f5-108">Is my tenant impacted?</span></span>
<span data-ttu-id="a50f5-109">Es wird empfohlen, Sie können diese durch die Einstellung der PermissiveBrowserFileHandlingOverride von [Office 365 PowerShell für SharePoint Online](https://technet.microsoft.com/en-us/library/fp161362.aspx)überprüfen:</span><span class="sxs-lookup"><span data-stu-id="a50f5-109">The recommended approach to check this is by checking the PermissiveBrowserFileHandlingOverride setting using [Office 365 PowerShell for SharePoint Online](https://technet.microsoft.com/en-us/library/fp161362.aspx):</span></span>

```PowerShell
Connect-SPOService -url https://contoso-admin.sharepoint.com
$tenant = get-spotenant
$tenant.PermissiveBrowserFileHandlingOverride
```

<span data-ttu-id="a50f5-110">Wenn dies **False** führt ist dann Ihres Mandanten nicht betroffen sind, wenn dies auf **True** festgelegt ist, und klicken Sie dann die bevorstehende das Verwerfen der Vorbereitung müssen.</span><span class="sxs-lookup"><span data-stu-id="a50f5-110">If this results in **False** then your tenant is not impacted, if this is set to **True** then you need prepare for the upcoming deprecation.</span></span> 

# <a name="how-can-i-prepare-for-changing-permissive-into-strict"></a><span data-ttu-id="a50f5-111">Wie kann ich Vorbereiten für permissive in strict ändern?</span><span class="sxs-lookup"><span data-stu-id="a50f5-111">How can I prepare for changing permissive into strict?</span></span>

![Zeigt permissive strict Modell](media/permissivetostrictmodel.png)

## <a name="step-1-assess-the-impact"></a><span data-ttu-id="a50f5-113">Schritt 1: Bewerten der Auswirkungen</span><span class="sxs-lookup"><span data-stu-id="a50f5-113">Step 1: Assess the impact</span></span>
<span data-ttu-id="a50f5-114">Grundlegendes zu viele Dateien betroffen sind, ist ein erster Schritt und Sie können, die über den Dateiscanner permissive.</span><span class="sxs-lookup"><span data-stu-id="a50f5-114">Understanding which files are impacted is a first step and you can do that via the permissive file scanner.</span></span> <span data-ttu-id="a50f5-115">Finden Sie in der [SharePoint-Permissive Scanner](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.PermissiveFile.Scanner) erfahren Sie mehr über den Scanner und Verwendungsweise.</span><span class="sxs-lookup"><span data-stu-id="a50f5-115">See the [SharePoint Permissive Scanner](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.PermissiveFile.Scanner) to learn more about the scanner and how to use it.</span></span> <span data-ttu-id="a50f5-116">In der Standardkonfiguration dieser Scanner sucht nach html/html-Dateien, aber Sie können mithilfe der Befehlszeilenoptionen den Scanner zu suchenden zusätzliche Filetypes anfordern.</span><span class="sxs-lookup"><span data-stu-id="a50f5-116">In the default configuration this scanner searches for html/html files, but using the command line options you can request the scanner to search for additional filetypes.</span></span>

<span data-ttu-id="a50f5-117">Das Ergebnis der Scanner mit allen CSV-Datei ist die betroffener (html/Htm + optional andere Dateitypen) Dateien, einschließlich Informationen zu den html/Htm-Dateien (Anzahl von Verknüpfungen und Skripts, die verwendet werden, letzten Änderungsdaten Ansichten).</span><span class="sxs-lookup"><span data-stu-id="a50f5-117">The result of the scanner is CSV file listing all the impacted (html/htm + optional other file types) files, including information about the html/htm files (number of links and scripts that are used, last change data, number of views).</span></span>

## <a name="step-2-analyze-the-scan-results"></a><span data-ttu-id="a50f5-118">Schritt 2: Analysieren der Überprüfungsergebnisse</span><span class="sxs-lookup"><span data-stu-id="a50f5-118">Step 2: Analyze the scan results</span></span>
<span data-ttu-id="a50f5-119">Nachdem Sie die Liste der betroffenen Dateien haben müssen Sie die bewerten, wenn diese Dateien und die Websites, halten diese Dateien weiterhin Business relevant sind.</span><span class="sxs-lookup"><span data-stu-id="a50f5-119">Once you’ve the list of impacted files you need to assess which if these files and the sites holding these files are still business relevant.</span></span> <span data-ttu-id="a50f5-120">Die Datei und/oder Website möglicherweise veraltet und, wenn also Remediation dieser Dateien/Sites übersprungen werden kann.</span><span class="sxs-lookup"><span data-stu-id="a50f5-120">The file and/or site might be stale and if so remediation of those files/sites might be skipped.</span></span> <span data-ttu-id="a50f5-121">Unterstützen Sie beim Verständnis der geschäftlicher Bedarf der Bericht enthält die Website-Auflistung Administratoren und Websitebesitzer, bietet Ihnen die benötigte Informationen, um sie zu kontaktieren.</span><span class="sxs-lookup"><span data-stu-id="a50f5-121">To help you with understanding the business need the report contains the site collection admins and site owners, providing you the needed information to contact them.</span></span>

## <a name="step-3-remediate-the-files"></a><span data-ttu-id="a50f5-122">Schritt 3: Warten von Dateien</span><span class="sxs-lookup"><span data-stu-id="a50f5-122">Step 3: Remediate the files</span></span>
<span data-ttu-id="a50f5-123">Wenn die Dateien wichtig sind, und werden weiterhin die Dateien nach der Mandanten, um die Einstellung strict verschoben wurde ausgeführt werden soll, müssen Sie die Dateien zu warten, wie in den nächsten Kapiteln erläutert.</span><span class="sxs-lookup"><span data-stu-id="a50f5-123">If the files are still important and you’ll want to continue to be able to execute the files once the tenant has moved to the strict setting, then you’ll need to remediate the files as explained in the next chapters.</span></span> 

# <a name="remediation-process-for-htmlhtm-files"></a><span data-ttu-id="a50f5-124">Remediation-Prozess für html/Htm-Dateien</span><span class="sxs-lookup"><span data-stu-id="a50f5-124">Remediation process for html/htm files</span></span>
<span data-ttu-id="a50f5-125">Der Hauptgrund für Kunden permissive Modus wann immer möglich ist, da sie HTML-Dateien aus innerhalb einer Dokumentbibliothek verwenden können möchten.</span><span class="sxs-lookup"><span data-stu-id="a50f5-125">The main reason for customers sticking with permissive mode is because they want to be able to use html files from inside a document library.</span></span> <span data-ttu-id="a50f5-126">Wie bereits erwähnt, sobald auf strict verschoben diese Dateien einfach herunterladen und mehr nicht automatisch geöffnet werden.</span><span class="sxs-lookup"><span data-stu-id="a50f5-126">As mentioned before once moved to strict these files will simply download and not automatically open anymore.</span></span>
<span data-ttu-id="a50f5-127">Für diese html/HTML-Dateien der Wartung ist einfach: Wenn eine Benutzer /-app mit Websitebesitzer oder Berechtigungen der Websitesammlung Admin die html/Htm-Dateien in ASPX-Dateien benennt, und klicken Sie dann diese Dateien erneut geöffnet.</span><span class="sxs-lookup"><span data-stu-id="a50f5-127">For these html/html files the remediation is simple: if a user/app with site owner or site collection admin permissions renames the html/htm files to ASPX files then these files do open again.</span></span> <span data-ttu-id="a50f5-128">[Plug & Play-PowerShell für SharePoint](https://aka.ms/sppnp-powershell) -zeigt ein wie dies möglich.</span><span class="sxs-lookup"><span data-stu-id="a50f5-128">Below [SharePoint PnP PowerShell](https://aka.ms/sppnp-powershell) shows a how this can be done.</span></span> <span data-ttu-id="a50f5-129">Angenommen, Sie haben eine HTML-Datei mit der folgenden Url: https://contoso.sharepoint.com/sites/permissive/html/newfile.html.</span><span class="sxs-lookup"><span data-stu-id="a50f5-129">Assume you’ve a html file with following url: https://contoso.sharepoint.com/sites/permissive/html/newfile.html.</span></span> 

```PowerShell
Connect-PnPOnline -Url https://contoso.sharepoint.com/sites/permissive -Verbose
Rename-PnPFile -ServerRelativeUrl /sites/permissive/html/newfile.html -TargetFileName newfile.aspx -OverwriteIfAlreadyExists
```

<span data-ttu-id="a50f5-130">Später wird in diesem Artikel ein Skript angezeigt werden, dass, eine vollständige "Beseitigung" von einer kompletten Websitesammlung ausführen können.</span><span class="sxs-lookup"><span data-stu-id="a50f5-130">Later on this article a script will be shown that can perform a full "remediation" of a complete site collection.</span></span>

## <a name="who-can-perform-this-rename"></a><span data-ttu-id="a50f5-131">Wer umbenennen ausführen können?</span><span class="sxs-lookup"><span data-stu-id="a50f5-131">Who can perform this rename?</span></span>
<span data-ttu-id="a50f5-132">Die Rename muss ausgeführt werden, von Benutzern mit der Berechtigung AddAndCustomizePages (ACP), die standardmäßig Websitesammlungs-Administratoren oder Websitebesitzer erteilt wird.</span><span class="sxs-lookup"><span data-stu-id="a50f5-132">The rename must be performed by users having the AddAndCustomizePages (ACP) permission, which by default is granted to site collection administrators or site owners.</span></span> <span data-ttu-id="a50f5-133">Bearbeiten Sie das Umbenennen von einem Benutzer mit erfolgt die Berechtigungsstufe (in diesem Fall Websitemitglieder) und klicken Sie dann die Rename erfolgt, aber die resultierende ASPX-Datei ist nicht für die Ausführung markiert und als solche werden heruntergeladen und nicht ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="a50f5-133">If the rename is done by a user with Edit the permission level (so site members) then the rename is done, but the resulting .aspx file is not marked for execution and as such will be downloaded and not executed.</span></span> 

<span data-ttu-id="a50f5-134">Bei einer Sammeloperation umbenannt werden soll Sie wahrscheinlich einen app-Prinzipal anstelle eines Benutzerkontos und es gilt: app-Prinzipals benötigt eine Berechtigung für die ACP (z. B. Vollzugriff Berechtigungsstufe) für diesen Vorgang.</span><span class="sxs-lookup"><span data-stu-id="a50f5-134">When you want to do a bulk rename you most likely will use an app principal instead of a user account and there the same applies: the app principal needs the ACP permission (e.g. Full Control permission level) to make this work.</span></span>

## <a name="what-about-embedded-links-to-other-htmlhtm-files"></a><span data-ttu-id="a50f5-135">Was geschieht mit eingebetteten Links zu anderen html/Htm-Dateien?</span><span class="sxs-lookup"><span data-stu-id="a50f5-135">What about embedded links to other html/htm files?</span></span>
<span data-ttu-id="a50f5-136">Mein html/Htm-Dateilink zu anderen html/Htm-Dateien im selben Ordner oder in einem Unterordner... wird diese Links Unterbrechung, wenn die Dateien auf Aspx umbenannt werden?</span><span class="sxs-lookup"><span data-stu-id="a50f5-136">My html/htm files link to other html/htm files in the same folder or in a subfolder…will these links break if the files are renamed to aspx?</span></span> <span data-ttu-id="a50f5-137">Die zugrunde liegende Rename erfolgt den MoveTo-API-Aufruf verwenden, und klicken Sie dann die meisten der relativen Links in der HTML-Datei automatisch aktualisiert werden, um Links zu... Aspx-Dateien werden Umbenennen im Wesentlichen eine Struktur der geschachtelten html/Htm-Dateien, die miteinander verknüpft nur möglich durch die tatsächlichen Dateien umbenennen, werden alle Links in die Dokumente durch die Rename behandelt.</span><span class="sxs-lookup"><span data-stu-id="a50f5-137">If the underlying rename is done using the MoveTo API call then most of the relative links inside the html file are automatically fixed to be links to aspx files…essentially renaming a structure of nested html/htm files which link to each other can be done by only renaming the actual files, all the links inside the documents will be handled by the rename.</span></span>

> [!NOTE]
> <span data-ttu-id="a50f5-138">Die automatische Umbenennung funktioniert nicht, wenn das html-Dokument Links, die in einer anderen Websitesammlung oder enthält Wenn die Links dynamisch generiert werden mithilfe von JavaScript-Dateien zeigen.</span><span class="sxs-lookup"><span data-stu-id="a50f5-138">The automatic renaming will not work when the html document has links pointing to files in another site collection or when the links are dynamically generated using JavaScript.</span></span> <span data-ttu-id="a50f5-139">In diesen Fällen müssen manuelle Aktionen Fixup die Links.</span><span class="sxs-lookup"><span data-stu-id="a50f5-139">In those cases, manual actions are required to fixup the links.</span></span>

## <a name="what-about-htmlhtml-files-referenced-in-a-content-editor-web-part"></a><span data-ttu-id="a50f5-140">Was geschieht mit html/HTML-Dateien in einem Inhalts-Editor-Webpart?</span><span class="sxs-lookup"><span data-stu-id="a50f5-140">What about html/html files referenced in a content editor web part?</span></span>
<span data-ttu-id="a50f5-141">Ein allgemeines Muster beim Arbeiten mit dem Inhalts-Editor-Webpart verweist auf eine html/Htm-Datei.</span><span class="sxs-lookup"><span data-stu-id="a50f5-141">A common pattern when working with the content editor web part is referencing a html/htm file.</span></span> <span data-ttu-id="a50f5-142">Wenn die referenzierten html/Htm-Datei in einer ASPX-Datei umbenannt wird, und klicken Sie dann SharePoint automatisch werden auch aktualisieren Sie den Verweis im Inhalts-Editor-Webpart, d. h. ab diesem Zeitpunkt, dass das Inhalts-Editor-Webpart auf die ASPX-Datei, anstatt die html/Htm-Datei geladen wird.</span><span class="sxs-lookup"><span data-stu-id="a50f5-142">When the referenced html/htm file is renamed to a .aspx file then SharePoint will automatically also update the reference in the content editor web part, meaning as of that moment the content editor web part will load the .aspx file instead of the html/htm file.</span></span> <span data-ttu-id="a50f5-143">So können Dateien vom Inhalts-Editor-Webpart zusammen mit allen anderen html/Htm-Dateien umbenannt werden.</span><span class="sxs-lookup"><span data-stu-id="a50f5-143">So files used by the content editor web part can be renamed together with all the other html/htm files.</span></span>

## <a name="what-about-sites-having-the-noscript-feature-enabled"></a><span data-ttu-id="a50f5-144">Was geschieht mit Websites mit der Funktion "Noscript" aktiviert</span><span class="sxs-lookup"><span data-stu-id="a50f5-144">What about sites having the “noscript” feature enabled</span></span>
<span data-ttu-id="a50f5-145">Alle "modernen" Websites (moderne Teamwebsite, Kommunikation Site) haben das "Noscript" Feature standardmäßig aktiviert.</span><span class="sxs-lookup"><span data-stu-id="a50f5-145">All “modern” sites (modern team site, communication site) have the “noscript” feature turned on by default.</span></span> <span data-ttu-id="a50f5-146">Das Ergebnis dieses ist, niemand, der die Berechtigung AddAndCustomizePages (ACP) verwendet werden, damit niemand eine erfolgreiche Umbenennen von html/Htm auf Aspx durchführen können.</span><span class="sxs-lookup"><span data-stu-id="a50f5-146">The result of this is that no one will have the AddAndCustomizePages (ACP) permission, so no one can perform a successful rename from html/htm to aspx.</span></span> <span data-ttu-id="a50f5-147">In der Regel live die html/Htm-Dateien in (migrierten) klassische Teamwebsites, damit dieses Problem nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="a50f5-147">Typically, the html/htm files live in (migrated) classic team sites so this problem is not there.</span></span> <span data-ttu-id="a50f5-148">In der Groß-/Kleinschreibung, den, die Sie in einer Website "Noscript" arbeiten, müssen Sie erste Deaktivieren des Features "Noscript" führen Sie die benennt und klicken Sie dann auf "Noscript" erneut aktivieren.</span><span class="sxs-lookup"><span data-stu-id="a50f5-148">In the case you are working in a “noscript” site you’ll need to first turn off the “noscript” feature, perform the renames and then turn on “noscript” again.</span></span> <span data-ttu-id="a50f5-149">Dementsprechend die html/Htm-Dateien erneut ausgeführt werden können, aber führen Sie beachten Sie, dass jede Änderung für diese Dateien werden als nicht ausführbar erneut markieren, wird.</span><span class="sxs-lookup"><span data-stu-id="a50f5-149">As a result the html/htm files can be executed again, but do note that each change on these files will mark them as non-executable again.</span></span> <span data-ttu-id="a50f5-150">Deaktivieren "Noscript" erneut aus, und Aktualisieren der Datei werden dies behandelt.</span><span class="sxs-lookup"><span data-stu-id="a50f5-150">Turning off “noscript” again and updating the file will handle this.</span></span>

## <a name="in-the-modern-document-library-experience-the-aspx-file-initially-do-not-seem-to-open"></a><span data-ttu-id="a50f5-151">Moderne Document Library Oberfläche die Aspx-Datei zunächst nicht scheinen öffnen?</span><span class="sxs-lookup"><span data-stu-id="a50f5-151">In the modern document library experience the aspx file initially do not seem to open?</span></span>
<span data-ttu-id="a50f5-152">Die moderne Document Library Erfahrung "wird davon ausgegangen" ein bestimmten Dateityps, wenn die Datei wurde hinzugefügt, und beim Zugriff auf die Datei zum ersten Mal sehen Sie, dass fälschlicherweise Aspx-Dateien geöffnet werden.</span><span class="sxs-lookup"><span data-stu-id="a50f5-152">The modern document library experience “assumes” a certain file type when the file was added and when accessing the file for the first time you’ll see that aspx files are opened wrongly.</span></span> <span data-ttu-id="a50f5-153">Zweiter Versuch führt jedoch die Datei aus.</span><span class="sxs-lookup"><span data-stu-id="a50f5-153">Second attempt however does execute the file.</span></span> <span data-ttu-id="a50f5-154">Geben Sie die vermeiden dieses Problems, die zum programmgesteuerten Pull nach unten einmal für jede umbenannte Datei empfohlen wird die SharePoint die Möglichkeit, die Datei richtig festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="a50f5-154">The avoid this problem it’s recommended to programmatically pull down each renamed file once, which gives SharePoint the opportunity to correctly set the file type.</span></span> <span data-ttu-id="a50f5-155">Zeigt eine wie [SharePoint Plug & Play-PowerShell](https://aka.ms/sppnp-powershell) kann dies erfolgen:</span><span class="sxs-lookup"><span data-stu-id="a50f5-155">Below [SharePoint PnP PowerShell](https://aka.ms/sppnp-powershell) shows a how this can be done:</span></span>

```PowerShell
Connect-PnPOnline -Url https://contoso.sharepoint.com/sites/permissive -Verbose
Get-PnPFile -Url /sites/permissive/html/newfile.aspx -Path c:\temp -Filename newfile.aspx -AsFile
```

> [!NOTE]
> <span data-ttu-id="a50f5-156">Dieser Schritt "herunterladen" ist im Skript enthalten, die eine vollständige "Beseitigung" von einer kompletten Websitesammlung ausführen können.</span><span class="sxs-lookup"><span data-stu-id="a50f5-156">This "download" step is included in the script that can perform a full "remediation" of a complete site collection.</span></span>

# <a name="remediation-of-other-file-types"></a><span data-ttu-id="a50f5-157">Behebung von anderen Dateitypen</span><span class="sxs-lookup"><span data-stu-id="a50f5-157">Remediation of other file types</span></span>
<span data-ttu-id="a50f5-158">HTML/Htm-Dateien sind als Hauptgrund für Kunden, die permissive Modus, aber was zu anderen Dateitypen verwenden?</span><span class="sxs-lookup"><span data-stu-id="a50f5-158">Html/htm files are the major reason for customers to use the permissive mode but what about other file types?</span></span> <span data-ttu-id="a50f5-159">Für viele Dateiformate bietet SharePoint Online eine einer Vorschaufunktion wie in diesem [Blog](https://techcommunity.microsoft.com/t5/OneDrive-for-Business/Announcing-New-File-Viewers-Available-for-OneDrive-For-Business/td-p/60040)erläutert.</span><span class="sxs-lookup"><span data-stu-id="a50f5-159">For the many common file formats SharePoint Online does offer a preview capability as explained in this [blog](https://techcommunity.microsoft.com/t5/OneDrive-for-Business/Announcing-New-File-Viewers-Available-for-OneDrive-For-Business/td-p/60040).</span></span> <span data-ttu-id="a50f5-160">SharePoint Online können die folgenden Formate eine Vorschau anzeigen:</span><span class="sxs-lookup"><span data-stu-id="a50f5-160">SharePoint Online can preview the following formats:</span></span>

## <a name="documents"></a><span data-ttu-id="a50f5-161">Dokumente</span><span class="sxs-lookup"><span data-stu-id="a50f5-161">Documents</span></span>
<span data-ttu-id="a50f5-162">CSV, Doc, Docm, DOCX-, DOTX-, Eml, msg, Odp, ods Odt, Pdf, POT-, potm-, Potx, Pps, Ppsx, ppt, Pptm, Pptx, Rtf, Vsd, Vsdx, Xls, Xlsb, Xlsm, Xlsx</span><span class="sxs-lookup"><span data-stu-id="a50f5-162">csv, doc, docm, docx, dotx, eml, msg, odp, ods, odt, pdf, pot, potm, potx, pps, ppsx, ppt, pptm, pptx, rtf, vsd, vsdx, xls, xlsb, xlsm, xlsx</span></span>

## <a name="images"></a><span data-ttu-id="a50f5-163">Bilder</span><span class="sxs-lookup"><span data-stu-id="a50f5-163">Images</span></span>
<span data-ttu-id="a50f5-164">AI, Arw, Bmp, cr2, Eps, gibt Erf, Gif, Ico, Symbol, Jpeg, Jpg, Mrw, Nef, Orf, Pict, Png, Psd, Tif, tiff</span><span class="sxs-lookup"><span data-stu-id="a50f5-164">ai, arw, bmp, cr2, eps, erf, gif, ico, icon, jpeg, jpg, mrw, nef, orf, pict, png, psd, tif, tiff</span></span>

## <a name="video"></a><span data-ttu-id="a50f5-165">Video</span><span class="sxs-lookup"><span data-stu-id="a50f5-165">Video</span></span>
<span data-ttu-id="a50f5-166">3GP, m4v, Mov, MP4 (engl.), WMV (engl.)</span><span class="sxs-lookup"><span data-stu-id="a50f5-166">3gp, m4v, mov, mp4, wmv</span></span>

## <a name="3d"></a><span data-ttu-id="a50f5-167">3D</span><span class="sxs-lookup"><span data-stu-id="a50f5-167">3D</span></span>
<span data-ttu-id="a50f5-168">3mf, Fbx, Obj, Blatt, stl</span><span class="sxs-lookup"><span data-stu-id="a50f5-168">3mf, fbx, obj, ply, stl</span></span>

## <a name="medical"></a><span data-ttu-id="a50f5-169">Medizinische</span><span class="sxs-lookup"><span data-stu-id="a50f5-169">Medical</span></span>
<span data-ttu-id="a50f5-170">DCM, dcm30, Dic, Dicm, dicom</span><span class="sxs-lookup"><span data-stu-id="a50f5-170">dcm, dcm30, dic, dicm, dicom</span></span>

## <a name="text-and-code"></a><span data-ttu-id="a50f5-171">Text und code</span><span class="sxs-lookup"><span data-stu-id="a50f5-171">Text and code</span></span>
<span data-ttu-id="a50f5-172">ABAP, Ada, adp, Ahk, als, as3, Asc, ASCX-Datei, Asm, Asp, Awk, Bash, Bash_login, Bash_logout, Bash_profile, Bashrc, Bat, Literaturverzeichnis, Bsh, Build, Generator, C, C ++ Capfile, cc, cfc, cfm, Cfml, cl, Clj, Cls, Cmake, Cmd, Kaffee, Cpp, cpt, Cpy, Cs, Cshtml, Cson, Csproj, Css, CTP-Version , cxx aufweisen, d, Ddl, di, Dif, Diff, Disco, Dml, Dtd, Dtml, el, Emakefile, Erb, Erl, f, f90, f95, fs, Fsi, Fsscript, Fsx, Gemfile, Gemspec, Gitconfig, wechseln Sie, einzigartige, Gvy, h, h-, Haml, Lenkern, HB, Hcp, Hh, Hpp, Hrl, hs, Htc, Hxx, Idl, Iim, inc, inf, Ini, Inl, Ipp , Irbrc, Jade, Jav, Java, Js, Jsp, Jsx, l, weniger Lhs, Lisp, melden Sie sich, Lst, Ltx, Lua, m, stellen, Markdn, Abzugsverteilung(en), Md, Mdown, Mkdn, ml, Mli, Mll, Mly, mm, weitere, Nfo, Opml, Osascript, auszuchecken, p, Pas, Patch, Php, php2, php3, php4, php5, Phtml, pl, Plist, pm, Pod, pp , profile, Eigenschaften, ps1, pt, hierhin, Pyw, R, Kielfall, Rb, Rbx, rc, re Infodatei, Reg, Rest, Resw, Resx, Rhtml, Rjs, Rprofile, Rpy, Rss, Rst, Rxml, s, Sass, Scala, Scm, Sconscript, Sconstruct, Skripts, Scss, sgml, sh Shtml, Sml, Sql, Sty, Tcl, tex, Text, mit, Tld, Tli, Aktivitätenvorlagenstatistik, Tpl, Txt, Vb, vi, Vim, Wsdl, Xhtml, Xml, Xoml, Xsd, Xsl, Xslt, Yaml, Yaws, Yml, Zip, zsh</span><span class="sxs-lookup"><span data-stu-id="a50f5-172">abap, ada, adp, ahk, as, as3, asc, ascx, asm, asp, awk, bash, bash_login, bash_logout, bash_profile, bashrc, bat, bib, bsh, build, builder, c, c++, capfile, cc, cfc, cfm, cfml, cl, clj, cls, cmake, cmd, coffee, cpp, cpt, cpy, cs, cshtml, cson, csproj, css, ctp, cxx, d, ddl, di, dif, diff, disco, dml, dtd, dtml, el, emakefile, erb, erl, f, f90, f95, fs, fsi, fsscript, fsx, gemfile, gemspec, gitconfig, go, groovy, gvy, h, h++, haml, handlebars, hbs, hcp, hh, hpp, hrl, hs, htc, hxx, idl, iim, inc, inf, ini, inl, ipp, irbrc, jade, jav, java, js, jsp, jsx, l, less, lhs, lisp, log, lst, ltx, lua, m, make, markdn, markdown, md, mdown, mkdn, ml, mli, mll, mly, mm, mud, nfo, opml, osascript, out, p, pas, patch, php, php2, php3, php4, php5, phtml, pl, plist, pm, pod, pp, profile, properties, ps1, pt, py, pyw, r, rake, rb, rbx, rc, re, readme, reg, rest, resw, resx, rhtml, rjs, rprofile, rpy, rss, rst, rxml, s, sass, scala, scm, sconscript, sconstruct, script, scss, sgml, sh, shtml, sml, sql, sty, tcl, tex, text, textile, tld, tli, tmpl, tpl, txt, vb, vi, vim, wsdl, xhtml, xml, xoml, xsd, xsl, xslt, yaml, yaws, yml, zip, zsh</span></span>

# <a name="sample-script-that-can-remediate-a-complete-site-collection"></a><span data-ttu-id="a50f5-173">Beispielskript, das eine kompletten Websitesammlung beheben können</span><span class="sxs-lookup"><span data-stu-id="a50f5-173">Sample script that can remediate a complete site collection</span></span>
<span data-ttu-id="a50f5-174">Dieses Skript kann als Start-Basis für eine Website bezogenen Auflistung Remediation verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a50f5-174">This script can be used as a starting basis for a site collection scoped remediation.</span></span> <span data-ttu-id="a50f5-175">Das Skript wird Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a50f5-175">The script will do the following:</span></span>
- <span data-ttu-id="a50f5-176">PnP PowerShell installieren Sie, sofern noch nicht installiert</span><span class="sxs-lookup"><span data-stu-id="a50f5-176">Install PnP-PowerShell if not yet installed</span></span>
- <span data-ttu-id="a50f5-177">Verwenden der Suche alle html/Htm-Dateien in der Websitesammlung zu finden sind</span><span class="sxs-lookup"><span data-stu-id="a50f5-177">Use search to find all the html/htm files in the site collection</span></span>
- <span data-ttu-id="a50f5-178">Benennen Sie die Dateien in .aspx</span><span class="sxs-lookup"><span data-stu-id="a50f5-178">Rename those files to .aspx</span></span>
- <span data-ttu-id="a50f5-179">Laden Sie die umbenannte Datei um beim ersten Zugriff in der Benutzeroberfläche der modernen Dokumentbibliothek Arbeiten ermöglichen</span><span class="sxs-lookup"><span data-stu-id="a50f5-179">Download the renamed file to enable it to work on first access in the modern document library user interface</span></span>


```PowerShell
# This script does rename .htm and .html files to .aspx files. Doing so enables these files to be "executed" in SharePoint Online 
# which has it's file handling configured to be strict. See https://docs.microsoft.com/en-us/sharepoint/dev/solution-guidance/security-permissivesetting 
# for more details

function PermissiveRemediateASiteCollection
{
    param([string] $siteCollectionUrl, [string] $winCredentialsManagerLabel)
    
    $siteCollectionUrl = $siteCollectionUrl.TrimEnd("/");

    # Gets or Sets the tenant admin credentials.
    $credentials = $null

    if(![String]::IsNullOrEmpty($winCredentialsManagerLabel) -and (Get-PnPStoredCredential -Name $winCredentialsManagerLabel) -ne $null)
    {
        $credentials = $winCredentialsManagerLabel
    }
    else
    {
        # Prompts for credentials, if not found in the Windows Credential Manager.
        $email = Read-Host -Prompt "Please enter admin email"
        $pass = Read-host -AsSecureString "Please enter admin password"
        $credentials = New-Object –TypeName "System.Management.Automation.PSCredential" –ArgumentList $email, $pass
    }

    if($credentials -eq $null) 
    {
        Write-Host "Error: No credentials supplied." -ForegroundColor Red
        exit 1
    }

    Connect-PnPOnline -Url $siteCollectionUrl -Credentials $credentials -Verbose

    Write-Host "Using search to obtain a list of files to remediate..."
    Try
    {
        $searchQuery = "((fileextension=htm OR fileextension=html) AND contentclass=STS_ListItem_DocumentLibrary AND Path:$siteCollectionUrl/*)"
        $htmlFiles = Submit-PnPSearchQuery -Query $searchQuery -TrimDuplicates:$false -All
    }
    Catch [Exception]
    {
       $ErrorMessage = $_.Exception.Message
       Write-Host "Error: Search query to find the files to remediate failed...exiting the script" -ForegroundColor Red 
       Write-Host "Error: $ErrorMessage" -ForegroundColor Red 
       exit 1
    }

    # if no files were found then bail out
    if ($htmlFiles.RowCount -eq 0)
    {
        Write-Host "No files found to remediate...exiting the script" -ForegroundColor Green
        exit 0
    }
    else
    {
        Write-Host "Found" $htmlFiles.RowCount "files to remediate" -ForegroundColor Green
    }

    # Create temp folder if not yet existing
    $path = "$env:TEMP\permissivefix"
    If(!(test-path $path))
    {
          New-Item -ItemType Directory -Force -Path $path
    }

    # iterate over the found files and rename them
    foreach($htmlFile in $htmlFiles.ResultRows)
    {
        Try
        {
            $web = $htmlFile.SPWebUrl
            Write-Host "Connected to $web..."
            Connect-PnPOnline -Url $web -Credentials $credentials

            $fileToRename = $htmlFile.OriginalPath
            Write-Host "Renaming $fileToRename..."

            # Get the server relative path
            $serverRelativePath = $fileToRename.Replace("https://", "")
            $serverRelativePath = $serverRelativePath.Substring($serverRelativePath.IndexOf("/"))
            #Write-Host $serverRelativePath

            # Get new file name and server relative path
            $newFileName = $serverRelativePath.Substring($serverRelativePath.LastIndexOf("/") + 1).ToLower()
            $serverRelativePathNew = $serverRelativePath
            if ($newFileName.EndsWith(".html"))
            {
                $newFileName = $newFileName.Replace(".html", ".aspx")
                $serverRelativePathNew = $serverRelativePathNew.Replace(".html", ".aspx")
            } 
            elseif($newFileName.EndsWith(".htm"))
            {
                $newFileName = $newFileName.Replace(".htm", ".aspx")
                $serverRelativePathNew = $serverRelativePathNew.Replace(".html", ".aspx")
            }
        
            # Perform the file rename
            Rename-PnPFile -ServerRelativeUrl $serverRelativePath -TargetFileName $newFileName -OverwriteIfAlreadyExists -Force
        
            # Download the file once to ensure it works correctly in modern UI
            Get-PnPFile -Url $serverRelativePathNew -Path $path -Filename $newFileName -AsFile -Force
        }
        Catch [Exception]
        {
           $ErrorMessage = $_.Exception.Message
           Write-Host "Error: Rename of file $serverRelativePath failed" -ForegroundColor Red 
           Write-Host "Error: $ErrorMessage" -ForegroundColor Red 
        }
    }

    # Cleanup the temp folder
    Write-Host "Cleaning up the temp folder $path"
    Remove-Item $path -Recurse -ErrorAction Ignore

    Write-Host "Remediation done for site collection $siteCollectionUrl" -BackgroundColor DarkGreen -ForegroundColor White
}

#######################################################
# MAIN section                                        #
#######################################################

# Url of the site collection to remediate
$siteCollectionUrlToRemediate = "https://contoso.sharepoint.com/sites/testsite"
# If you use credential manager then specify the used credential manager entry, if left blank you'll be asked for a user/pwd
$credentialManagerCredentialToUse = "credmandreference"

# Ensure PnP PowerShell is loaded
if (-not (Get-Module -ListAvailable -Name SharePointPnPPowerShellOnline)) 
{
    Install-Module SharePointPnPPowerShellOnline
}

Import-Module SharePointPnPPowerShellOnline

# Remediate the given site collection
PermissiveRemediateASiteCollection $siteCollectionUrlToRemediate $credentialManagerCredentialToUse

```

<span data-ttu-id="a50f5-180">Die Beispielausgabe des erfolgreicher Skript ausgeführt werden, sieht folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="a50f5-180">The sample output of succesful script run looks like this:</span></span>

```Txt
WARNING: The names of some imported commands from the module 'SharePointPnPPowerShellOnline' include unapproved verbs that might make them less discoverable. To find the commands with unapproved ver
bs, run the Import-Module command again with the Verbose parameter. For a list of approved verbs, type Get-Verb.
VERBOSE: PnP PowerShell Cmdlets (2.22.1801.0): Connected to https://contoso.sharepoint.com/sites/testsite
Using search to obtain a list of files to remediate...
Found 15 files to remediate


    Directory: C:\Users\demouser\AppData\Local\Temp


Mode                LastWriteTime         Length Name                                                                                                                                                
----                -------------         ------ ----                                                                                                                                                
d-----        7/02/2018     19:48                permissivefix                                                                                                                                       
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/About.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/brol.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/imagetarget.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/sample_html_afternoscript9.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/bla.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/sample_html.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/home2.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/howtouse.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/home.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/team_home.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/imagesource.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/bla2.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/wikipage.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/newfile_html.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/Home3.html...
Cleaning up the temp folder C:\Users\demouser\AppData\Local\Temp\permissivefix
Remediation done for site collection https://contoso.sharepoint.com/sites/testsite

```

