---
title: "PowerShell-Cmdlets für SharePoint-Websitedesigns und -Websiteskripts"
description: Verwenden Sie PowerShell-Cmdlets zum Erstellen, Abrufen und Entfernen von Websitedesigns und Websiteskripts.
ms.date: 12/14/2017
ms.openlocfilehash: d28a487c20970973cd11a26532068b54c095d939
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-cmdlets-for-sharepoint-site-designs-and-site-scripts"></a><span data-ttu-id="93eac-103">PowerShell-Cmdlets für SharePoint-Websitedesigns und -Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="93eac-103">PowerShell cmdlets for SharePoint site designs and site scripts</span></span>

> [!NOTE]
> <span data-ttu-id="93eac-104">Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="93eac-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="93eac-105">Sie werden in Produktionsumgebungen derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="93eac-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="93eac-106">Verwenden Sie PowerShell-Cmdlets zum Erstellen, Abrufen und Entfernen von Websitedesigns und Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="93eac-106">Use PowerShell cmdlets to create, retrieve, and remove site designs and site scripts.</span></span>

## <a name="getting-started"></a><span data-ttu-id="93eac-107">Erste Schritte</span><span class="sxs-lookup"><span data-stu-id="93eac-107">Getting started</span></span>

<span data-ttu-id="93eac-108">Bevor Sie die PowerShell-Cmdlets ausführen können, müssen Sie Folgendes tun:</span><span class="sxs-lookup"><span data-stu-id="93eac-108">To run the PowerShell cmdlets for theme management, you'll need to do the following:</span></span>

1. <span data-ttu-id="93eac-109">Sie müssen die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunterladen und installieren.</span><span class="sxs-lookup"><span data-stu-id="93eac-109">Download and install the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span> <span data-ttu-id="93eac-110">Ist auf Ihrem System bereits eine frühere Version der Shell installiert, müssen Sie diese Version deinstallieren und anschließend die neueste Version installieren.</span><span class="sxs-lookup"><span data-stu-id="93eac-110">If you already have a previous version of the shell installed, uninstall it first and then install the latest version.</span></span>
1. <span data-ttu-id="93eac-111">Sie müssen eine Verbindung zu Ihrem SharePoint-Mandanten einrichten. Eine Anleitung finden Sie unter [Herstellen einer Verbindung mit SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx).</span><span class="sxs-lookup"><span data-stu-id="93eac-111">Follow the instructions at [Connect to SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx) to connect to your SharePoint tenant.</span></span>

<span data-ttu-id="93eac-112">Um die Einrichtung zu überprüfen, verwenden Sie das **Get-SPOSiteScript** zum Lesen der aktuellen Liste von Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="93eac-112">To verify your setup, try using the **Get-SPOSiteScript** cmdlet to read the current list of site scripts.</span></span> <span data-ttu-id="93eac-113">Wenn das Cmdlet ausgeführt und ohne Fehler zurückgegeben wird, können Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="93eac-113">If the cmdlet runs and returns False with no errors, as shown in the following example, you're ready to proceed.</span></span>

## <a name="site-design-cmdlets"></a><span data-ttu-id="93eac-114">Websitedesign-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="93eac-114">Site design cmdlets</span></span>

<span data-ttu-id="93eac-115">Zur Verwaltung von Websitedesigns und Websiteskripts über die PowerShell stehen Ihnen die folgenden Cmdlets zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="93eac-115">The following cmdlets are available for managing site themes from PowerShell:</span></span>

- <span data-ttu-id="93eac-116">**Add-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="93eac-116">**Add-SPOSiteDesign**</span></span>
- <span data-ttu-id="93eac-117">**Add-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="93eac-117">**Add-SPOSiteScript**</span></span>
- <span data-ttu-id="93eac-118">**Get-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="93eac-118">**Get-SPOSiteDesign**</span></span>
- <span data-ttu-id="93eac-119">**Get-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="93eac-119">**Get-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="93eac-120">**Get-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="93eac-120">**Get-SPOSiteScript**</span></span>
- <span data-ttu-id="93eac-121">**Grant-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="93eac-121">**Grant-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="93eac-122">**Remove-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="93eac-122">**Remove-SPOSiteDesign**</span></span>
- <span data-ttu-id="93eac-123">**Remove-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="93eac-123">**Remove-SPOSiteScript**</span></span>
- <span data-ttu-id="93eac-124">**Revoke-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="93eac-124">**Revoke-SPOSiteDesignRights**</span></span>

<!--
- **Set-SPOSiteDesign**
- **Set-SPOSiteScript**
-->

<!-- TBD document pipe bind parameters -->

## <a name="add-spositedesign"></a><span data-ttu-id="93eac-125">Add-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="93eac-125">Add-SPOSiteDesign</span></span>

<span data-ttu-id="93eac-126">Erstellen eines neues Websitedesigns, das für Benutzer beim Erstellen einer neuen Website von der SharePoint-Startseite verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="93eac-126">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

```powershell
Add-SPOSiteDesign
  -Title <string>
  -WebTemplate <string>
  -SiteScripts <SPOSiteScriptPipeBind[]>
  [-Description <string>]
  [-PreviewImageUrl <string>]
  [-PreviewImageAltText <string>]
  [-IsDefault]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="93eac-127">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-127">Parameters</span></span>

|<span data-ttu-id="93eac-128">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-128">Parameter</span></span>  | <span data-ttu-id="93eac-129">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93eac-129">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="93eac-130">-Title</span><span class="sxs-lookup"><span data-stu-id="93eac-130">title</span></span>                 | <span data-ttu-id="93eac-131">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="93eac-131">The display name of the web site.</span></span> |
|<span data-ttu-id="93eac-132">-WebTemplate</span><span class="sxs-lookup"><span data-stu-id="93eac-132">WebTemplate</span></span>           | <span data-ttu-id="93eac-133">Identifiziert, zu welcher Basisvorlage das Design hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="93eac-133">Identifies which base template to add the design to.</span></span> <span data-ttu-id="93eac-134">Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage.</span><span class="sxs-lookup"><span data-stu-id="93eac-134">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="93eac-135">-SiteScripts</span><span class="sxs-lookup"><span data-stu-id="93eac-135">-SiteScripts</span></span>           | <span data-ttu-id="93eac-136">Ein Array von einem oder mehreren Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="93eac-136">An array of one or more site scripts.</span></span> <span data-ttu-id="93eac-137">Jedes wird durch eine ID identifziert.</span><span class="sxs-lookup"><span data-stu-id="93eac-137">Each is identified by an ID.</span></span> <span data-ttu-id="93eac-138">Die Skripts werden in der aufgeführten Reihenfolge ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="93eac-138">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="93eac-139">[-Description]</span><span class="sxs-lookup"><span data-stu-id="93eac-139">Description</span></span>         | <span data-ttu-id="93eac-140">Die Anzeigebeschreibung des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="93eac-140">The display description of site design.</span></span> |
|<span data-ttu-id="93eac-141">[-PreviewImageUrl]</span><span class="sxs-lookup"><span data-stu-id="93eac-141">PreviewImageUrl</span></span>     | <span data-ttu-id="93eac-142">Die URL eines Vorschaubilds.</span><span class="sxs-lookup"><span data-stu-id="93eac-142">The URL of a preview image.</span></span> <span data-ttu-id="93eac-143">Wenn keine angegeben ist, verwendet SharePoint ein allgemeines Bild.</span><span class="sxs-lookup"><span data-stu-id="93eac-143">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="93eac-144">[-PreviewImageAltText]</span><span class="sxs-lookup"><span data-stu-id="93eac-144">[-PreviewImageAltText]</span></span> | <span data-ttu-id="93eac-145">Die Alternativtextbeschreibung des Bilds für Barrierefreiheit.</span><span class="sxs-lookup"><span data-stu-id="93eac-145">The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="93eac-146">[-IsDefault]</span><span class="sxs-lookup"><span data-stu-id="93eac-146">isDefault</span></span>           | <span data-ttu-id="93eac-147">Eine Option, die das Websitedesign auf die Standardwebsitevorlage anwendet.</span><span class="sxs-lookup"><span data-stu-id="93eac-147">A switch that if provided, applies the site design to the default site template.</span></span> <!-- For more information see [Applying a site design to a default SharePoint template](site-design-apply-default-template.md) --> |

<span data-ttu-id="93eac-148">Nachfolgend finden Sie ein Beispiel für das Erstellen eines neues Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="93eac-148">Here's an example of creating a new site design.</span></span>

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "<ID>" `
  -Description "Tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview" `
  -IsDefault $false
```

## <a name="add-spositescript"></a><span data-ttu-id="93eac-149">**Add-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="93eac-149">**Add-SPOSiteScript**</span></span>

<span data-ttu-id="93eac-150">Lädt ein neues Websiteskript in den Katalog hoch, das entweder direkt oder in einem Websitedesign verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="93eac-150">Uploads a new site script to the gallery for use either directly or in a site design.</span></span> <span data-ttu-id="93eac-151">Dieses Cmdlet unterstützt die Inline-Skriptdatei.</span><span class="sxs-lookup"><span data-stu-id="93eac-151">This cmdlet will support inline script; file</span></span>

```powershell
Add-SPOSiteScript
  -Title <string>
  -Content <string>
  [-Description <string>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="93eac-152">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-152">Parameters</span></span>

|<span data-ttu-id="93eac-153">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-153">Parameter</span></span>     | <span data-ttu-id="93eac-154">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93eac-154">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="93eac-155">-Title</span><span class="sxs-lookup"><span data-stu-id="93eac-155">title</span></span>       | <span data-ttu-id="93eac-156">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="93eac-156">The display name of the web site.</span></span> |
| <span data-ttu-id="93eac-157">-Content</span><span class="sxs-lookup"><span data-stu-id="93eac-157">Content</span></span>     | <span data-ttu-id="93eac-158">JSON-Wert, der das Skript beschreibt.</span><span class="sxs-lookup"><span data-stu-id="93eac-158">JSON value that describes the script.</span></span> <span data-ttu-id="93eac-159">Weitere Informationen finden Sie unter [JSON-Referenz](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="93eac-159">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|
| <span data-ttu-id="93eac-160">-Description</span><span class="sxs-lookup"><span data-stu-id="93eac-160">Description</span></span> | <span data-ttu-id="93eac-161">Eine Beschreibung des Skripts.</span><span class="sxs-lookup"><span data-stu-id="93eac-161">A description of the error.</span></span> |

<span data-ttu-id="93eac-162">Nachfolgend finden Sie ein Beispiel für das Hinzufügen einer neuen Website aus dem folgenden Skript zu einer Datei.</span><span class="sxs-lookup"><span data-stu-id="93eac-162">Here's an example of adding a new site from the following script in a file.</span></span>

```json
{
  "verb": "setSiteLogo",
  "url": "https://contoso.sharepoint.com/SiteAssets/company-logo.png"
},
```

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' -Raw | Add-SPOSiteScript -Title "Customer logo" -Description "Applies customer logo for customer sites"
```

## <a name="get-spositedesign"></a><span data-ttu-id="93eac-163">Get-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="93eac-163">Get-SPOSiteDesign</span></span>

<span data-ttu-id="93eac-164">Ruft Details zu Websitedesigns ab, die sich im SharePoint-Mandanten befinden.</span><span class="sxs-lookup"><span data-stu-id="93eac-164">Gets details about site designs that are on the SharePoint tenant.</span></span> <span data-ttu-id="93eac-165">Sie können eine ID eines bestimmten Websitedesigns angeben, das abgerufen werden soll.</span><span class="sxs-lookup"><span data-stu-id="93eac-165">You can specify an ID of a specific site design to retrieve.</span></span> <span data-ttu-id="93eac-166">Wenn keine Parameter aufgeführt werden, werden Details zu allen Websitedesigns aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="93eac-166">If there are no parameters listed, then details about all site designs are listed.</span></span>

```powershell
Get-SPOSiteDesign
  [[-Identity] <SPOSiteDesignPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="93eac-167">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-167">Parameters</span></span>

|<span data-ttu-id="93eac-168">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-168">Parameter</span></span>     | <span data-ttu-id="93eac-169">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93eac-169">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="93eac-170">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="93eac-170">Identity</span></span>  | <span data-ttu-id="93eac-171">Die ID des abzurufenden Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="93eac-171">The ID of the object to retrieve.</span></span> |

<span data-ttu-id="93eac-172">Nachfolgend finden Sie ein Beispiel und eine Beispielantwort für das Abrufen von Websitedesigndetails.</span><span class="sxs-lookup"><span data-stu-id="93eac-172">Here's an example and sample response of getting site design details.</span></span>

```powershell
PS C:\> Get-SPOSiteDesign 44252d09-62c4-4913-9eb0-a2a8b8d7f863
```

```
Id                  : 44252d09-62c4-4913-9eb0-a2a8b8d7f863
Title               : Contoso - Team Project
WebTemplate         : 64
SiteScriptIds       : {1306913c-8463-42ca-bd63-efad0fcdbba4}
Description         : Use this design to apply Contoso theme and create
                      custom lists and add to nav
```

## <a name="get-spositedesignrights"></a><span data-ttu-id="93eac-173">Get-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="93eac-173">Get-SPOSiteDesignRights</span></span>

<span data-ttu-id="93eac-174">Zeigt eine Liste von Prinzipalen und deren Berechtigungen zur Verwendung des Websitedesigns an.</span><span class="sxs-lookup"><span data-stu-id="93eac-174">Displays a list of principals and their rights for usage of the site design.</span></span> <span data-ttu-id="93eac-175">Dies kann verwendet werden, um den Bereich zu ermitteln, den Ihr Websitedesign mit Benutzern in dem Mandanten aufweist.</span><span class="sxs-lookup"><span data-stu-id="93eac-175">This can be used to determine the scope that your site design has with users on the tenant.</span></span>

```powershell
Get-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="93eac-176">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-176">Parameters</span></span>

|<span data-ttu-id="93eac-177">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-177">Parameter</span></span>     | <span data-ttu-id="93eac-178">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93eac-178">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="93eac-179">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="93eac-179">Identity</span></span>  | <span data-ttu-id="93eac-180">Die ID des Websitedesigns zum Abrufen von Bereichsinformationen.</span><span class="sxs-lookup"><span data-stu-id="93eac-180">The ID of the site design to get scoping information.</span></span> |

<span data-ttu-id="93eac-181">Nachfolgend finden Sie ein Beispiel zum Abrufen der Berechtigungen für ein Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="93eac-181">Here's an example of getting the rights for a site design.</span></span>

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1
```

```
DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.sharepoint.com   View
```

## <a name="get-spositescript"></a><span data-ttu-id="93eac-182">Get-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="93eac-182">Get-SPOSiteScript</span></span>

<span data-ttu-id="93eac-183">Zeigt Informationen zu vorhandenen Websiteskripts an.</span><span class="sxs-lookup"><span data-stu-id="93eac-183">Displays information about existing site scripts.</span></span> <span data-ttu-id="93eac-184">Wenn kein Parameter bereitgestellt wird, gibt dieses Cmdlet **Id**, **Title**, **Description** und **Version** jedes Websiteskripts an.</span><span class="sxs-lookup"><span data-stu-id="93eac-184">When no parameter is provided, this cmdlet returns the **Id**, **Title**, **Description**, and **Version** of each site script.</span></span> <span data-ttu-id="93eac-185">Wenn eine Websiteskript-ID bereitgestellt wird, gibt dieses Cmdlet auch **Content** an, wobei es sich um den JSON-Code des Websiteskripts handelt.</span><span class="sxs-lookup"><span data-stu-id="93eac-185">When a site script ID is provided, this cmdlet also returns the **Content**, which is the JSON of the site script.</span></span>

```powershell
Get-SPOSiteScript
  [[-Identity] <SPOSiteScriptPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="93eac-186">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-186">Parameters</span></span>

|<span data-ttu-id="93eac-187">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-187">Parameter</span></span>     | <span data-ttu-id="93eac-188">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93eac-188">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="93eac-189">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="93eac-189">Identity</span></span>  | <span data-ttu-id="93eac-190">Die ID des Websiteskripts, über das Informationen abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="93eac-190">The ID of the site script to get information about.</span></span> |

## <a name="grant-spositedesignrights"></a><span data-ttu-id="93eac-191">Grant-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="93eac-191">Grant-SPOSiteDesignRights</span></span>

<span data-ttu-id="93eac-192">Wird zum Anwenden von Berechtigungen auf einen Satz von Benutzern oder eine Sicherheitsgruppe verwendet, wodurch die Sichtbarkeit des Websitedesigns in der UX effektiv festgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="93eac-192">Used to apply permissions to set of users or security group, effectively scoping visibility of site design in UX.</span></span> <span data-ttu-id="93eac-193">Diese beginnen öffentlich.</span><span class="sxs-lookup"><span data-stu-id="93eac-193">They start off public.</span></span> <span data-ttu-id="93eac-194">Nachdem Sie jedoch Berechtigungen festgelegt haben, können nur diese Gruppen oder Benutzer auf das Websitedesign zugreifen.</span><span class="sxs-lookup"><span data-stu-id="93eac-194">But once you set permissions, only those groups or users with permissions can access the site design.</span></span>

```powershell
Grant-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  -Rights {View}
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="93eac-195">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-195">Parameters</span></span>

|<span data-ttu-id="93eac-196">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-196">Parameter</span></span>     | <span data-ttu-id="93eac-197">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93eac-197">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="93eac-198">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="93eac-198">Identity</span></span>  | <span data-ttu-id="93eac-199">Die ID des Websitedesigns zum Abrufen von Bereichsinformationen.</span><span class="sxs-lookup"><span data-stu-id="93eac-199">The ID of the site design to get scoping information.</span></span> |
| <span data-ttu-id="93eac-200">-Principals</span><span class="sxs-lookup"><span data-stu-id="93eac-200">-Principals</span></span>  | <span data-ttu-id="93eac-201">Eine oder mehrere Prinzipale, für die Berechtigungen hinzugefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="93eac-201">One or more principles to add permissions for.</span></span> |
| <span data-ttu-id="93eac-202">-Rights</span><span class="sxs-lookup"><span data-stu-id="93eac-202">Rights</span></span>      | <span data-ttu-id="93eac-203">Ist immer auf den Wert **View** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="93eac-203">Always set to the value **View**.</span></span> <span data-ttu-id="93eac-204">Alle Benutzer oder Gruppen mit Anzeigeberechtigungen können das Websitedesign anzeigen und verwenden.</span><span class="sxs-lookup"><span data-stu-id="93eac-204">Any user or group with view permissions can view and use the site design.</span></span> |

<span data-ttu-id="93eac-205">Nachfolgend finden Sie ein Beispiel, wie Anzeigeberechtigungen für ein Websitedesign für einen Nestor (ein Benutzer auf der fiktiven Contoso-Website) erteilt werden.</span><span class="sxs-lookup"><span data-stu-id="93eac-205">Here's an example of how to grant view rights on a site design to Nestor (a user at the fictional Contoso site).</span></span>

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.sharepoint.com" `
         -Rights View
```

## <a name="remove-spositedesign"></a><span data-ttu-id="93eac-206">Remove-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="93eac-206">Remove-SPOSiteDesign</span></span>

<span data-ttu-id="93eac-207">Entfernt ein Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="93eac-207">Removes a site design.</span></span> <span data-ttu-id="93eac-208">Dieses wird nicht mehr in der Benutzeroberfläche zum Erstellen einer neuen Website angezeigt.</span><span class="sxs-lookup"><span data-stu-id="93eac-208">It will no longer appear in the UI for creating a new site.</span></span>

```powershell
  Remove-SPOSiteDesign
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="93eac-209">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-209">Parameters</span></span>

|<span data-ttu-id="93eac-210">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-210">Parameter</span></span>     | <span data-ttu-id="93eac-211">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93eac-211">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="93eac-212">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="93eac-212">Identity</span></span>  | <span data-ttu-id="93eac-213">Die ID des zu entfernenden Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="93eac-213">The ID of the site design to remove.</span></span> |

## <a name="remove-spositescript"></a><span data-ttu-id="93eac-214">Remove-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="93eac-214">Remove-SPOSiteScript</span></span>

<span data-ttu-id="93eac-215">Entfernt ein Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="93eac-215">Removes a site script.</span></span> <!-- TBD how is dependency problem handled so you don't delete a script that a design depends on. this currently creates an error when running the design.) -->

```powershell
Remove-SPOSiteScript
  [-Identity] <SPOSiteScriptPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="93eac-216">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-216">Parameters</span></span>

|<span data-ttu-id="93eac-217">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-217">Parameter</span></span>     | <span data-ttu-id="93eac-218">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93eac-218">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="93eac-219">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="93eac-219">Identity</span></span>  | <span data-ttu-id="93eac-220">Die ID des zu entfernenden Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="93eac-220">The ID of the site script to remove.</span></span> |

## <a name="revoke-spositedesignrights"></a><span data-ttu-id="93eac-221">Revoke-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="93eac-221">Revoke-SPOSiteDesignRights</span></span>

<span data-ttu-id="93eac-222">Widerruft Berechtigungen für angegebene Prinzipale aus einem Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="93eac-222">Revokes rights for specified principals from a site design.</span></span>

```powershell
Revoke-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="93eac-223">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-223">Parameters</span></span>

|<span data-ttu-id="93eac-224">Parameter</span><span class="sxs-lookup"><span data-stu-id="93eac-224">Parameter</span></span>     | <span data-ttu-id="93eac-225">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93eac-225">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="93eac-226">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="93eac-226">Identity</span></span>  | <span data-ttu-id="93eac-227">Die ID des Websitedesigns, aus dem Berechtigungen widerrufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="93eac-227">The ID of the site design from which to revoke rights.</span></span> |
| <span data-ttu-id="93eac-228">-Principals</span><span class="sxs-lookup"><span data-stu-id="93eac-228">-Principals</span></span>  | <span data-ttu-id="93eac-229">Mindestens ein Prinzipal zum Widerrufen von Berechtigungen im angegebenen Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="93eac-229">One or more principals to revoke rights on the specified site design.</span></span> |

<!--
## Set-SPOSiteDesign (TBD)

## Set-SPOSiteScript (TBD)
-->

<span data-ttu-id="93eac-230">Entwickler können zur Verwaltung von Designs außerdem die [REST-API](site-design-rest-api.md) verwenden.</span><span class="sxs-lookup"><span data-stu-id="93eac-230">Developers can also use the SharePoint [REST API](site-design-rest-api.md) to handle theme management tasks.</span></span>

<span data-ttu-id="93eac-231">Informationen zur Definition und Speicherung von Designs finden Sie in der [JSON-Schemareferenz](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="93eac-231">For information about how themes are defined and stored, see [JSON schema reference](site-design-json-schema.md).</span></span>