---
title: "Unterstützung von % und # in Dateien und Ordner mit der API http://"
ms.date: 11/03/2017
ms.openlocfilehash: 4667020c2387650d8ad84dc000afa785f7b07016
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="supporting--and--in-file-and-folder-with-the-resourcepath-api"></a><span data-ttu-id="72800-102">Unterstützung von % und # in Dateien und Ordner mit der API http://</span><span class="sxs-lookup"><span data-stu-id="72800-102">Supporting % and # in file and folder with the ResourcePath API</span></span>

<span data-ttu-id="72800-103">Unterstützung für % und # dürfen in Dateien und Ordner wird in SharePoint Online bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="72800-103">Support for % and # in file and folder is being deployed within SharePoint Online.</span></span>  <span data-ttu-id="72800-104">Leider kann aufgrund einer vorhandenen API Strukturen und Muster aufrufen, arbeiten mit diesen Dateinamen manchmal mehrdeutig wird.</span><span class="sxs-lookup"><span data-stu-id="72800-104">Unfortunately, due to existing API structures and calling patterns, working with these file names can sometimes become ambiguous.</span></span>  <span data-ttu-id="72800-105">Sie können [Weitere Hintergrund dies in unserem Entwicklerblog](https://dev.office.com/blogs/upcoming-changes-to-sharepoint-and-onedrive-for-business-apis-to-support-and-in-file-names)suchen.</span><span class="sxs-lookup"><span data-stu-id="72800-105">You can find [more background behind this on our developer blog](https://dev.office.com/blogs/upcoming-changes-to-sharepoint-and-onedrive-for-business-apis-to-support-and-in-file-names).</span></span>  <span data-ttu-id="72800-106">Neue APIs wurden in lässt sich sagen auf die SharePoint Online-Client-Objekt Objektmodell (CSOM)-Oberfläche # und % Zeichen unterstützen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="72800-106">In summary, new APIs have been added to the SharePoint Online client object model (CSOM) surface to provide support for # and % characters.</span></span>

## <a name="resourcepath"></a><span data-ttu-id="72800-107">Http://</span><span class="sxs-lookup"><span data-stu-id="72800-107">ResourcePath</span></span>
 
<span data-ttu-id="72800-108">Beachten Sie als eine Zusammenfassung vorhandenen SharePoint-APIs (beispielsweise SPFileCollection.GetByUrl) Zeichenfolge-basierte Handles beide codiert und decodiert automatisch von URLs, unter der Annahme, dass % und #-Zeichen in einem Pfad impliziert, dass die URL codiert wurde.</span><span class="sxs-lookup"><span data-stu-id="72800-108">As a recap, note that existing String-based SharePoint APIs (such as SPFileCollection.GetByUrl) handle both encoded and decoded URLs by automatically assuming that % and # characters in a path imply that the URL has been encoded.</span></span>  <span data-ttu-id="72800-109">Durch die neue Unterstützung ist % und # dürfen in der Datei und der Ordner, der diese automatische Behandlung jetzt problematisch, weil es downstream Code ignorieren oder Dateinamen mit % und # dürfen in diese mishandle führen kann.</span><span class="sxs-lookup"><span data-stu-id="72800-109">With new support % and # in file and folder, this automatic treatment is now problematic because it may cause downstream code to ignore or mishandle filenames with % and # in them.</span></span>
 
<span data-ttu-id="72800-110">Eine neue Klasse-- `Microsoft.SharePoint.Client.ResourcePath` --APIs hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="72800-110">A new class -- `Microsoft.SharePoint.Client.ResourcePath` -- has been added to APIs.</span></span>  <span data-ttu-id="72800-111">Die Klasse http:// ist unerlässlich für die Unterstützung der folgenden neuen Zeichen.</span><span class="sxs-lookup"><span data-stu-id="72800-111">The ResourcePath class is fundamental to the support of these new characters.</span></span>  <span data-ttu-id="72800-112">Es bietet die Möglichkeit neue, eindeutige ein Element in SharePoint und OneDrive für Unternehmen, da es geht davon aus, und nur mit decodierten URLs funktioniert behandeln.</span><span class="sxs-lookup"><span data-stu-id="72800-112">It provides a new, unambiguous way to address an item within SharePoint and OneDrive for Business, because it assumes and only works with decoded URLs.</span></span> <span data-ttu-id="72800-113">String-basierte Pfade zur Darstellung einer vollständig (absolut) oder teilweise (relativ) URL für eine Websitesammlung, Website, Dateien, Ordner oder andere Artifact und OneDrive für Unternehmen ersetzt.</span><span class="sxs-lookup"><span data-stu-id="72800-113">It replaces String-based paths to represent a full (absolute) or partial (relative) URL for a site collection, site, file, folder or other artifact and OneDrive for Business.</span></span> <span data-ttu-id="72800-114">Um ordnungsgemäß % und # innerhalb von URLs zu unterstützen, müssen Sie die http://-basierten APIs zusammen mit decodiert URLs verwenden.</span><span class="sxs-lookup"><span data-stu-id="72800-114">To properly support % and # within URLs, you will need to use the ResourcePath-based APIs along with Decoded URLs.</span></span>
 
<span data-ttu-id="72800-115">Http:// kann einfach erstellt werden, indem Sie eine statische Funktion aufrufen `ResourcePath.FromDecodedUrl(string)`.</span><span class="sxs-lookup"><span data-stu-id="72800-115">ResourcePath can be simply constructed by calling a static function `ResourcePath.FromDecodedUrl(string)`.</span></span> <span data-ttu-id="72800-116">Der übergebene Wert kann durch Aufrufen der Eigenschaft DecodedUrl aus dem http://-Objekt zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="72800-116">The passed in input value can be accessed from the ResourcePath object by calling the property DecodedUrl.</span></span> 
 
<span data-ttu-id="72800-117">Für vorhandene Anrufe, die in einer URL-Zeichenfolge basierende dauern, Sie müssen ermitteln, ob der Pfad für den führende zu Zeichenfolge-basierte URL Anrufe wurden mit ver- oder entschlüsselte URLs bereitgestellt, und gibt an, ob die Pfade auch code Anker Hyperlinks zulässig (d. h.: #bookmark Ergänzungen auf oberen Rand der Datei-URL).</span><span class="sxs-lookup"><span data-stu-id="72800-117">For existing calls that take in a String-based URL, you will need to determine whether the code path leading to String-based URL calls were provided with encoded or decoded URLs, and whether those code paths also permitted Anchor links (that is: #bookmark additions on top of the file URL.)</span></span>

> <span data-ttu-id="72800-118">Hinweis: Nicht einfach suchen und Ersetzen der vorhandene Verwendungen des String-basierte URL APIs mit `ResourcePath.FromDecodedUrl`.</span><span class="sxs-lookup"><span data-stu-id="72800-118">Note: Do not simply find and replace existing usages of String-based URL APIs with `ResourcePath.FromDecodedUrl`.</span></span>  <span data-ttu-id="72800-119">Sie müssen URL ordnungsgemäß bestimmt und potenziell decodieren URLs vor zuerst mit der `ResourcePath.FromDecodedUrl(string)` API.</span><span class="sxs-lookup"><span data-stu-id="72800-119">You will need to properly determine URL and potentially decode URLs first before using the `ResourcePath.FromDecodedUrl(string)` API.</span></span>

<span data-ttu-id="72800-120">In Fällen, in dem eine Codepath führt zu einer Zeichenfolge-basierte SharePoint API-Aufruf verwendet **Decodiert URLs (z. B. "FY17 Report.docx")**, dann können Sie diesen anrufen mit einfach ersetzen `ResourcePath.FromDecodedUrl(string)` und die entsprechenden unten aufgeführten http://-Methoden.</span><span class="sxs-lookup"><span data-stu-id="72800-120">In cases where a codepath leading to a String-based SharePoint API call used **Decoded URLs (e.g., 'FY17 Report.docx')**, then you can simply replace these calls with `ResourcePath.FromDecodedUrl(string)` and equivalent ResourcePath methods listed below.</span></span>
 
<span data-ttu-id="72800-121">Beachten Sie, dass in vielen Fällen, in dem Sie die URL aus SharePoint über APIs gelesen, der http:// auch angegeben wird, dieser Codemuster konsistenter, vornehmen, damit Sie die http:// anstelle der URL verwenden können.</span><span class="sxs-lookup"><span data-stu-id="72800-121">Note that in many cases where you read the URL from SharePoint via APIs, the ResourcePath is also provided to make these code patterns more consistent, so you can use the ResourcePath instead of URL.</span></span>
 
<span data-ttu-id="72800-122">Beachten Sie außerdem, dass diese Änderung auch für die SharePoint-REST-basierte von Anrufen sowie gilt.</span><span class="sxs-lookup"><span data-stu-id="72800-122">Also note that this change also applies to SharePoint REST-based calls, as well.</span></span>  <span data-ttu-id="72800-123">Überprüfen Sie die unten, um diese neue APIs in REST-Beispiele finden Sie unter Szenarien.</span><span class="sxs-lookup"><span data-stu-id="72800-123">Please review the scenarios below to see examples of these new APIs in REST.</span></span>

## <a name="new-apis-that-are-based-on-resourcepath-and-supports--and-"></a><span data-ttu-id="72800-124">Neue APIs, die auf http:// basieren und unterstützt # und %</span><span class="sxs-lookup"><span data-stu-id="72800-124">New APIs that are based on ResourcePath and supports # and %</span></span>
 
<span data-ttu-id="72800-125">Im folgenden sind die neuen APIs, die wir eingeführt, um die vorhandenen APIs zur Unterstützung der # und % zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="72800-125">Below are the new APIs that we introduced to replace the existing APIs in order to support # and %.</span></span> <span data-ttu-id="72800-126">Wir die alte API und der neuen API nebeneinander für den Vergleich aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="72800-126">We listed the old API and the new API side by side for your comparison.</span></span> <span data-ttu-id="72800-127">Die Kernfunktionen dieser APIs nicht geändert, wie Sie die Position des Elements wurde geändert.</span><span class="sxs-lookup"><span data-stu-id="72800-127">The core functionality of these APIs does not change, but how to represent the location of the item is changed.</span></span>
 
<span data-ttu-id="72800-128">Die Dokumentation der neuen APIs kann unter https://msdn.microsoft.com/en-us/library/jj193041.aspx bezeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="72800-128">The documentation of new APIs can be referred at https://msdn.microsoft.com/en-us/library/jj193041.aspx.</span></span>  <span data-ttu-id="72800-129">Haben wir die .net CSOM APIs unten aufgeführt, aber die neuen Methoden sind auch im entsprechenden Format in unseren CSOM JavaScript-Bibliotheken verfügbar.</span><span class="sxs-lookup"><span data-stu-id="72800-129">We have listed the .net CSOM APIs below, but the new methods are also available in equivalent form in our JavaScript CSOM libraries.</span></span>
 
<span data-ttu-id="72800-130">**Assembly-Microsoft.SharePoint.Client.dll**</span><span class="sxs-lookup"><span data-stu-id="72800-130">**Assembly Microsoft.SharePoint.Client.dll**</span></span>

| <span data-ttu-id="72800-131">Typ</span><span class="sxs-lookup"><span data-stu-id="72800-131">Type</span></span> | <span data-ttu-id="72800-132">Alte-Methode</span><span class="sxs-lookup"><span data-stu-id="72800-132">Old Method</span></span> | <span data-ttu-id="72800-133">New-Methode</span><span class="sxs-lookup"><span data-stu-id="72800-133">New Method</span></span> | 
|----------|-------------|------|
| <span data-ttu-id="72800-134">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="72800-134">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="72800-135">AddItem(Microsoft.SharePoint.SPListItemCreationInformation)</span><span class="sxs-lookup"><span data-stu-id="72800-135">AddItem(Microsoft.SharePoint.SPListItemCreationInformation)</span></span> | <span data-ttu-id="72800-136">AddItemUsingPath (SPListItemCreationInformationUsingPath-Parameter)</span><span class="sxs-lookup"><span data-stu-id="72800-136">AddItemUsingPath(SPListItemCreationInformationUsingPath parameters)</span></span> | 
| <span data-ttu-id="72800-137">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="72800-137">Microsoft.SharePoint.SPFile</span></span> | <span data-ttu-id="72800-138">MoveTo (System.String, Microsoft.SharePoint.SPMoveOperations)</span><span class="sxs-lookup"><span data-stu-id="72800-138">MoveTo(System.String, Microsoft.SharePoint.SPMoveOperations)</span></span> | <span data-ttu-id="72800-139">MoveToUsingPath (SPResourcePath NewPath, SPMoveOperations MoveOperations)</span><span class="sxs-lookup"><span data-stu-id="72800-139">MoveToUsingPath(SPResourcePath newPath, SPMoveOperations moveOperations)</span></span> | 
| <span data-ttu-id="72800-140">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="72800-140">Microsoft.SharePoint.SPFile</span></span> | <span data-ttu-id="72800-141">CopyTo (System.String, Boolean)</span><span class="sxs-lookup"><span data-stu-id="72800-141">CopyTo(System.String, Boolean)</span></span> | <span data-ttu-id="72800-142">CopyToUsingPath (SPResourcePath NewPath, Bool Overwrite)</span><span class="sxs-lookup"><span data-stu-id="72800-142">CopyToUsingPath(SPResourcePath newPath, bool overwrite)</span></span> | 
| <span data-ttu-id="72800-143">Microsoft.SharePoint.SPFileCollection</span><span class="sxs-lookup"><span data-stu-id="72800-143">Microsoft.SharePoint.SPFileCollection</span></span> | <span data-ttu-id="72800-144">GetByUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-144">GetByUrl(System.String)</span></span> | <span data-ttu-id="72800-145">GetByPath(SPResourcePath)</span><span class="sxs-lookup"><span data-stu-id="72800-145">GetByPath(SPResourcePath)</span></span> | 
| <span data-ttu-id="72800-146">Microsoft.SharePoint.SPFileCollection</span><span class="sxs-lookup"><span data-stu-id="72800-146">Microsoft.SharePoint.SPFileCollection</span></span> | <span data-ttu-id="72800-147">Fügen Sie hinzu (System.String, Microsoft.SharePoint.SPTemplateFileType)</span><span class="sxs-lookup"><span data-stu-id="72800-147">Add(System.String, Microsoft.SharePoint.SPTemplateFileType)</span></span> | <span data-ttu-id="72800-148">AddUsingPath (SPResourcePath, SPFileCollectionAddWithTemplateParameters)</span><span class="sxs-lookup"><span data-stu-id="72800-148">AddUsingPath(SPResourcePath, SPFileCollectionAddWithTemplateParameters)</span></span> | 
| <span data-ttu-id="72800-149">Microsoft.SharePoint.SPFolder</span><span class="sxs-lookup"><span data-stu-id="72800-149">Microsoft.SharePoint.SPFolder</span></span> | <span data-ttu-id="72800-150">MoveTo(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-150">MoveTo(System.String)</span></span> | <span data-ttu-id="72800-151">MoveToUsingPath (SPResourcePath NewPath)</span><span class="sxs-lookup"><span data-stu-id="72800-151">MoveToUsingPath(SPResourcePath newPath)</span></span> | 
| <span data-ttu-id="72800-152">Microsoft.SharePoint.SPFolder</span><span class="sxs-lookup"><span data-stu-id="72800-152">Microsoft.SharePoint.SPFolder</span></span> | <span data-ttu-id="72800-153">AddSubFolder(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-153">AddSubFolder(System.String)</span></span> | <span data-ttu-id="72800-154">AddSubFolderUsingPath (SPResourcePath LeafPath)</span><span class="sxs-lookup"><span data-stu-id="72800-154">AddSubFolderUsingPath(SPResourcePath leafPath)</span></span> | 
| <span data-ttu-id="72800-155">Microsoft.SharePoint.SPFolderCollection</span><span class="sxs-lookup"><span data-stu-id="72800-155">Microsoft.SharePoint.SPFolderCollection</span></span> | <span data-ttu-id="72800-156">GetByUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-156">GetByUrl(System.String)</span></span> | <span data-ttu-id="72800-157">GetByPath (SPResourcePath Pfad)</span><span class="sxs-lookup"><span data-stu-id="72800-157">GetByPath(SPResourcePath path)</span></span> | 
| <span data-ttu-id="72800-158">Microsoft.SharePoint.SPFolderCollection</span><span class="sxs-lookup"><span data-stu-id="72800-158">Microsoft.SharePoint.SPFolderCollection</span></span> | <span data-ttu-id="72800-159">Add(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-159">Add(System.String)</span></span> | <span data-ttu-id="72800-160">AddUsingPath (SPResourcePath Pfad, SPFolderCreationInformation-Parameter)</span><span class="sxs-lookup"><span data-stu-id="72800-160">AddUsingPath(SPResourcePath path, SPFolderCreationInformation parameters)</span></span> | 
|  | <span data-ttu-id="72800-161">AddWithOverwrite (String Url, Bool Overwrite)</span><span class="sxs-lookup"><span data-stu-id="72800-161">AddWithOverwrite(string url, bool overwrite)</span></span> |  | 
| <span data-ttu-id="72800-162">Microsoft.SharePoint.SPRemoteWeb</span><span class="sxs-lookup"><span data-stu-id="72800-162">Microsoft.SharePoint.SPRemoteWeb</span></span> | <span data-ttu-id="72800-163">GetFileByServerRelativeUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-163">GetFileByServerRelativeUrl(System.String)</span></span> | <span data-ttu-id="72800-164">GetFileByServerRelativePath (SPResourcePath Pfad)</span><span class="sxs-lookup"><span data-stu-id="72800-164">GetFileByServerRelativePath(SPResourcePath path)</span></span> | 
| <span data-ttu-id="72800-165">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="72800-165">Microsoft.SharePoint.SPWeb</span></span> | <span data-ttu-id="72800-166">GetList(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-166">GetList(System.String)</span></span> | <span data-ttu-id="72800-167">GetListUsingPath(SPResourcePath)</span><span class="sxs-lookup"><span data-stu-id="72800-167">GetListUsingPath(SPResourcePath)</span></span> | 
| <span data-ttu-id="72800-168">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="72800-168">Microsoft.SharePoint.SPWeb</span></span> | <span data-ttu-id="72800-169">GetListItem(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-169">GetListItem(System.String)</span></span> | <span data-ttu-id="72800-170">GetListItemUsingPath(SPResourcePath)</span><span class="sxs-lookup"><span data-stu-id="72800-170">GetListItemUsingPath(SPResourcePath)</span></span> | 


<span data-ttu-id="72800-171">Die folgenden CSOM-Objekte zurückgeben http://-Eigenschaften, die in über APIs verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="72800-171">The following CSOM objects return ResourcePath properties that can be used in above APIs.</span></span> <span data-ttu-id="72800-172">Obwohl die alte-Eigenschaft auch decodierten URLs zurückgegeben wird, wird die neue http://-Eigenschaft für Komfort, Einfachheit und Klarheit in Anrufe über APIs bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="72800-172">Although the old property also returns decoded URLs, the new ResourcePath property is provided for convenience, simplicity and clarity in calling above APIs.</span></span>  <span data-ttu-id="72800-173">Die einzige Ausnahme ist die SPFolder.WelcomePage-Eigenschaft, die früher codierten und uncodierten URLs zurückgegeben. Dies ist eindeutig jetzt über die WelcomePagePath-Eigenschaft zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="72800-173">The one exception to this is the SPFolder.WelcomePage property, which formerly returned both encoded and unencoded URLs; this is now unambiguously returned via the WelcomePagePath property.</span></span>

| <span data-ttu-id="72800-174">Typ</span><span class="sxs-lookup"><span data-stu-id="72800-174">Type</span></span> | <span data-ttu-id="72800-175">Alte-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="72800-175">Old Property</span></span> | <span data-ttu-id="72800-176">New-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="72800-176">New Property</span></span> | 
|----------|-------------|------|
| <span data-ttu-id="72800-177">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="72800-177">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="72800-178">DefaultViewUrl</span><span class="sxs-lookup"><span data-stu-id="72800-178">DefaultViewUrl</span></span> | <span data-ttu-id="72800-179">DefaultViewPath</span><span class="sxs-lookup"><span data-stu-id="72800-179">DefaultViewPath</span></span> | 
| <span data-ttu-id="72800-180">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="72800-180">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="72800-181">DefaultEditFormUrl</span><span class="sxs-lookup"><span data-stu-id="72800-181">DefaultEditFormUrl</span></span> | <span data-ttu-id="72800-182">DefaultEditFormPath</span><span class="sxs-lookup"><span data-stu-id="72800-182">DefaultEditFormPath</span></span> | 
| <span data-ttu-id="72800-183">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="72800-183">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="72800-184">DefaultNewFormUrl</span><span class="sxs-lookup"><span data-stu-id="72800-184">DefaultNewFormUrl</span></span> | <span data-ttu-id="72800-185">DefaultNewFormPath</span><span class="sxs-lookup"><span data-stu-id="72800-185">DefaultNewFormPath</span></span> | 
| <span data-ttu-id="72800-186">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="72800-186">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="72800-187">DefaultDisplayFormUrl</span><span class="sxs-lookup"><span data-stu-id="72800-187">DefaultDisplayFormUrl</span></span> | <span data-ttu-id="72800-188">DefaultDisplayFormPath</span><span class="sxs-lookup"><span data-stu-id="72800-188">DefaultDisplayFormPath</span></span> | 
| <span data-ttu-id="72800-189">Microsoft.SharePoint.SPAttachment</span><span class="sxs-lookup"><span data-stu-id="72800-189">Microsoft.SharePoint.SPAttachment</span></span> | <span data-ttu-id="72800-190">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="72800-190">ServerRelativeUrl</span></span> | <span data-ttu-id="72800-191">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="72800-191">ServerRelativePath</span></span> | 
| <span data-ttu-id="72800-192">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="72800-192">Microsoft.SharePoint.SPFile</span></span> | <span data-ttu-id="72800-193">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="72800-193">ServerRelativeUrl</span></span> | <span data-ttu-id="72800-194">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="72800-194">ServerRelativePath</span></span> | 
| <span data-ttu-id="72800-195">Microsoft.SharePoint.SPFolder</span><span class="sxs-lookup"><span data-stu-id="72800-195">Microsoft.SharePoint.SPFolder</span></span> | <span data-ttu-id="72800-196">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="72800-196">ServerRelativeUrl</span></span> | <span data-ttu-id="72800-197">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="72800-197">ServerRelativePath</span></span> | 
| <span data-ttu-id="72800-198">Microsoft.SharePoint.SPFolder</span><span class="sxs-lookup"><span data-stu-id="72800-198">Microsoft.SharePoint.SPFolder</span></span> | <span data-ttu-id="72800-199">WelcomePage</span><span class="sxs-lookup"><span data-stu-id="72800-199">WelcomePage</span></span> | <span data-ttu-id="72800-200">WelcomePagePath / WelcomePageParameters</span><span class="sxs-lookup"><span data-stu-id="72800-200">WelcomePagePath/ WelcomePageParameters</span></span> | 
| <span data-ttu-id="72800-201">Microsoft.SharePoint.SPView</span><span class="sxs-lookup"><span data-stu-id="72800-201">Microsoft.SharePoint.SPView</span></span> | <span data-ttu-id="72800-202">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="72800-202">ServerRelativeUrl</span></span> | <span data-ttu-id="72800-203">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="72800-203">ServerRelativePath</span></span> | 
| <span data-ttu-id="72800-204">Microsoft.SharePoint.SPDocumentLibraryInformation</span><span class="sxs-lookup"><span data-stu-id="72800-204">Microsoft.SharePoint.SPDocumentLibraryInformation</span></span> | <span data-ttu-id="72800-205">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="72800-205">ServerRelativeUrl</span></span> | <span data-ttu-id="72800-206">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="72800-206">ServerRelativePath</span></span> | 


## <a name="existing-apis-that-are-not-ambiguous-about-the-url-formant-and-can-supports--and-"></a><span data-ttu-id="72800-207">Vorhandene APIs, die nicht über die URL-Tabelle mehrdeutige und kann unterstützt # und %</span><span class="sxs-lookup"><span data-stu-id="72800-207">Existing APIs that are not ambiguous about the URL formant and can supports # and %</span></span>
 
<span data-ttu-id="72800-208">Die folgenden APIs akzeptieren nur ordnungsgemäß codierten URLs als Eingabe.</span><span class="sxs-lookup"><span data-stu-id="72800-208">The following APIs only accept properly encoded URLs as input.</span></span> <span data-ttu-id="72800-209">Sie unterstützen auch unter-codierten URLs, solange die URL ohne jede Mehrdeutigkeit genutzt werden kann.</span><span class="sxs-lookup"><span data-stu-id="72800-209">They also support under-encoded URLs as long as the URL can be consumed without any ambiguity.</span></span> <span data-ttu-id="72800-210">In der Reihenfolge Wörter mindestens # oder % Zeichen im Pfad der URL % codiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="72800-210">In order words, at least # or % characters in the path of the URL should be % encoded.</span></span> <span data-ttu-id="72800-211">Diese APIs werden weiterhin die vorhandene Weise arbeiten.</span><span class="sxs-lookup"><span data-stu-id="72800-211">These APIs will continue to work in the existing way.</span></span> <span data-ttu-id="72800-212">in der URL "#" wird als ein Fragmenttrennzeichen, aber nicht Teil der URL-Pfad behandelt.</span><span class="sxs-lookup"><span data-stu-id="72800-212">'#' in the URL is treated as a fragment delimiter, but not part of URL path.</span></span>

| <span data-ttu-id="72800-213">Typ</span><span class="sxs-lookup"><span data-stu-id="72800-213">Type</span></span> | <span data-ttu-id="72800-214">Alte-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="72800-214">Old Property</span></span> | 
|----------|-------------|
| <span data-ttu-id="72800-215">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="72800-215">Microsoft.SharePoint.SPWeb</span></span> |  <span data-ttu-id="72800-216">GetFileByUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-216">GetFileByUrl(System.String)</span></span> |
| <span data-ttu-id="72800-217">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="72800-217">Microsoft.SharePoint.SPWeb</span></span> |  <span data-ttu-id="72800-218">GetFileByWOPIFrameUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-218">GetFileByWOPIFrameUrl(System.String)</span></span> |
| <span data-ttu-id="72800-219">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="72800-219">Microsoft.SharePoint.SPWeb</span></span> |  <span data-ttu-id="72800-220">GetFileByLinkingUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="72800-220">GetFileByLinkingUrl(System.String)</span></span> |

<span data-ttu-id="72800-221">Die folgenden C#-Eigenschaften werden zurückzugebenden System.Uri mit eindeutige Codierung für die Verwendung mit den oben genannten APIs hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="72800-221">The following C# properties are added to return System.Uri with unambiguous encoding for use with the above APIs.</span></span> <span data-ttu-id="72800-222">Die ältere Variant-Wert mit der unter APIs zurückgegebenen decodiert URLs und inzwischen sie nie # enthalten oder Zeichen, die URL wurde nicht mehrdeutige.</span><span class="sxs-lookup"><span data-stu-id="72800-222">The older variant of the below APIs returned decoded URLs and since they never contained # or % characters, the URL was not ambiguous.</span></span> <span data-ttu-id="72800-223">Vorwärts, wir nicht das decodierte Verhalten der älteren Varianten zum Codieren % und #-Zeichen im Pfad aufteilen möchten.</span><span class="sxs-lookup"><span data-stu-id="72800-223">Going forward, we did not want to break the decoded behavior of the older variants to encode % and # characters in path.</span></span> <span data-ttu-id="72800-224">Aus diesem Grund wurden neue APIs erstellt.</span><span class="sxs-lookup"><span data-stu-id="72800-224">Therefore, new APIs were created.</span></span>
 
| <span data-ttu-id="72800-225">Typ</span><span class="sxs-lookup"><span data-stu-id="72800-225">Type</span></span>   |      <span data-ttu-id="72800-226">Alte-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="72800-226">Old Property</span></span>      |  <span data-ttu-id="72800-227">New-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="72800-227">New Property</span></span> |
|----------|-------------|------|
| <span data-ttu-id="72800-228">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="72800-228">Microsoft.SharePoint.SPFile</span></span> |  <span data-ttu-id="72800-229">LinkingUrl</span><span class="sxs-lookup"><span data-stu-id="72800-229">LinkingUrl</span></span> | <span data-ttu-id="72800-230">LinkingUri</span><span class="sxs-lookup"><span data-stu-id="72800-230">LinkingUri</span></span> |
| <span data-ttu-id="72800-231">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="72800-231">Microsoft.SharePoint.SPFile</span></span> |  <span data-ttu-id="72800-232">ServerRedirectedEmbedUrl</span><span class="sxs-lookup"><span data-stu-id="72800-232">ServerRedirectedEmbedUrl</span></span> | <span data-ttu-id="72800-233">ServerRedirectedEmbedUri</span><span class="sxs-lookup"><span data-stu-id="72800-233">ServerRedirectedEmbedUri</span></span> |


## <a name="sample-code"></a><span data-ttu-id="72800-234">Beispielcode (engl.)</span><span class="sxs-lookup"><span data-stu-id="72800-234">Sample code</span></span>

<span data-ttu-id="72800-235">Es folgen einige Beispielcode für grundlegende Szenarios in CSOM:</span><span class="sxs-lookup"><span data-stu-id="72800-235">Here are some sample code for basic scenarios in CSOM:</span></span>
 
- <span data-ttu-id="72800-236">Hinzufügen einer Datei in einen Ordner (.net)</span><span class="sxs-lookup"><span data-stu-id="72800-236">Add a file to a folder (.net)</span></span>

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

- <span data-ttu-id="72800-237">Fügen Sie einen untergeordneten Ordner in einen Ordner (.net)</span><span class="sxs-lookup"><span data-stu-id="72800-237">Add a sub-folder to a folder  (.net)</span></span>

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

- <span data-ttu-id="72800-238">Rufen Sie eine Datei im Web (.net)</span><span class="sxs-lookup"><span data-stu-id="72800-238">Get a file in the web (.net)</span></span>

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

<span data-ttu-id="72800-239">Es folgen einige Beispielcode für grundlegende Szenarios in REST:</span><span class="sxs-lookup"><span data-stu-id="72800-239">Here are some sample code for basic scenarios in REST:</span></span>

- <span data-ttu-id="72800-240">Abrufen von Ordnern</span><span class="sxs-lookup"><span data-stu-id="72800-240">Get Folders</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativePath(decodedUrl='folder name')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

- <span data-ttu-id="72800-241">Ordner erstellen</span><span class="sxs-lookup"><span data-stu-id="72800-241">Create Folder</span></span>
 
```
url: http://site url/_api/web/Folders/AddUsingPath(decodedurl='/document library relative url/folder name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
 
```
 
- <span data-ttu-id="72800-242">Abrufen von Dateien</span><span class="sxs-lookup"><span data-stu-id="72800-242">Get Files</span></span>
 
```
url: http://site url/_api/web/GetFileByServerRelativePath(decodedUrl='folder name/file name')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
 
- <span data-ttu-id="72800-243">Hinzufügen von Dateien</span><span class="sxs-lookup"><span data-stu-id="72800-243">Add Files</span></span>
 
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
