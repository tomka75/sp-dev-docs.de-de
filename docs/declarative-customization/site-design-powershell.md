---
title: "PowerShell-Cmdlets für SharePoint-Websitedesigns und -Websiteskripts"
description: Verwenden Sie PowerShell-Cmdlets zum Erstellen, Abrufen und Entfernen von Websitedesigns und Websiteskripts.
ms.date: 01/08/2018
ms.openlocfilehash: 24c49a9b7e6ae19cd6118573d11720803adc4c94
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="powershell-cmdlets-for-sharepoint-site-designs-and-site-scripts"></a><span data-ttu-id="d6d20-103">PowerShell-Cmdlets für SharePoint-Websitedesigns und -Websiteskripts</span><span class="sxs-lookup"><span data-stu-id="d6d20-103">PowerShell cmdlets for SharePoint site designs and site scripts</span></span>

> [!NOTE]
> <span data-ttu-id="d6d20-104">Websitedesigns und Websiteskripts befinden sich in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="d6d20-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="d6d20-105">Sie werden derzeit nur für Produktionsumgebungen im Zielrelease unterstützt.Sie werden derzeit nur für Produktionsumgebungen im Zielrelease unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-105">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="d6d20-106">Verwenden Sie PowerShell-Cmdlets zum Erstellen, Abrufen, Aktualisieren und Entfernen von Websitedesigns und Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="d6d20-106">Use PowerShell cmdlets to create, retrieve, and remove site designs and site scripts.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d6d20-107">Erste Schritte</span><span class="sxs-lookup"><span data-stu-id="d6d20-107">Getting started</span></span>

<span data-ttu-id="d6d20-108">Bevor Sie die PowerShell-Cmdlets ausführen können, müssen Sie Folgendes tun:</span><span class="sxs-lookup"><span data-stu-id="d6d20-108">To run the PowerShell cmdlets, you'll need to do the following:</span></span>

1. <span data-ttu-id="d6d20-109">Sie müssen die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunterladen und installieren.</span><span class="sxs-lookup"><span data-stu-id="d6d20-109">Download and install the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span> <span data-ttu-id="d6d20-110">Ist auf Ihrem System bereits eine frühere Version der Shell installiert, müssen Sie diese Version deinstallieren und anschließend die neueste Version installieren.</span><span class="sxs-lookup"><span data-stu-id="d6d20-110">If you already have a previous version of the shell installed, uninstall it first and then install the latest version.</span></span>
1. <span data-ttu-id="d6d20-111">Sie müssen eine Verbindung zu Ihrem SharePoint-Mandanten einrichten. Eine Anleitung finden Sie unter [Herstellen einer Verbindung mit SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6d20-111">Follow the instructions at [Connect to SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx) to connect to your SharePoint tenant.</span></span>

<span data-ttu-id="d6d20-112">Um die Einrichtung zu überprüfen, verwenden Sie das **Get-SPOSiteScript** zum Lesen der aktuellen Liste von Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="d6d20-112">To verify your setup, try using the **Get-SPOSiteScript** cmdlet to read the current list of site scripts.</span></span> <span data-ttu-id="d6d20-113">Wenn das Cmdlet ausgeführt und ohne Fehler zurückgegeben wird, können Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="d6d20-113">If the cmdlet runs and returns with no errors, you're ready to proceed.</span></span>

## <a name="site-design-cmdlets"></a><span data-ttu-id="d6d20-114">Websitedesign-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="d6d20-114">Site design cmdlets</span></span>

<span data-ttu-id="d6d20-115">Zur Verwaltung von Websitedesigns und Websiteskripts über die PowerShell stehen Ihnen die folgenden Cmdlets zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="d6d20-115">The following cmdlets are available for managing site designs and site scripts from PowerShell:</span></span>

- <span data-ttu-id="d6d20-116">**Add-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="d6d20-116">**Add-SPOSiteDesign**</span></span>
- <span data-ttu-id="d6d20-117">**Add-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="d6d20-117">**Add-SPOSiteScript**</span></span>
- <span data-ttu-id="d6d20-118">**Get-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="d6d20-118">**Get-SPOSiteDesign**</span></span>
- <span data-ttu-id="d6d20-119">**Get-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="d6d20-119">**Get-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="d6d20-120">**Get-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="d6d20-120">**Get-SPOSiteScript**</span></span>
- <span data-ttu-id="d6d20-121">**Grant-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="d6d20-121">**Grant-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="d6d20-122">**Remove-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="d6d20-122">**Remove-SPOSiteDesign**</span></span>
- <span data-ttu-id="d6d20-123">**Remove-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="d6d20-123">**Remove-SPOSiteScript**</span></span>
- <span data-ttu-id="d6d20-124">**Revoke-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="d6d20-124">**Revoke-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="d6d20-125">**Set-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="d6d20-125">**Set-SPOSiteDesign**</span></span>
- <span data-ttu-id="d6d20-126">**Set-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="d6d20-126">**Set-SPOSiteScript**</span></span>

<!-- TBD document pipe bind parameters -->

## <a name="add-spositedesign"></a><span data-ttu-id="d6d20-127">Add-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="d6d20-127">Add-SPOSiteDesign</span></span>

<span data-ttu-id="d6d20-128">Erstellen eines neues Websitedesigns, das für Benutzer beim Erstellen einer neuen Website von der SharePoint-Startseite verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="d6d20-128">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

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

### <a name="parameters"></a><span data-ttu-id="d6d20-129">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-129">Parameters</span></span>

|<span data-ttu-id="d6d20-130">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-130">Parameter</span></span>  | <span data-ttu-id="d6d20-131">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-131">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="d6d20-132">-Title</span><span class="sxs-lookup"><span data-stu-id="d6d20-132">-Title</span></span>                 | <span data-ttu-id="d6d20-133">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="d6d20-133">The display name of the site design.</span></span> |
|<span data-ttu-id="d6d20-134">-WebTemplate</span><span class="sxs-lookup"><span data-stu-id="d6d20-134">-WebTemplate</span></span>           | <span data-ttu-id="d6d20-135">Identifiziert, zu welcher Basisvorlage das Design hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="d6d20-135">Identifies which base template to add the design to.</span></span> <span data-ttu-id="d6d20-136">Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage.</span><span class="sxs-lookup"><span data-stu-id="d6d20-136">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="d6d20-137">-SiteScripts</span><span class="sxs-lookup"><span data-stu-id="d6d20-137">-SiteScripts</span></span>           | <span data-ttu-id="d6d20-138">Ein Array von einem oder mehreren Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="d6d20-138">An array of one or more site scripts.</span></span> <span data-ttu-id="d6d20-139">Jedes wird durch eine ID identifziert.</span><span class="sxs-lookup"><span data-stu-id="d6d20-139">Each is identified by an ID.</span></span> <span data-ttu-id="d6d20-140">Die Skripts werden in der aufgeführten Reihenfolge ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-140">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="d6d20-141">[-Description]</span><span class="sxs-lookup"><span data-stu-id="d6d20-141">[-Description]</span></span>         | <span data-ttu-id="d6d20-142">Die Anzeigebeschreibung des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="d6d20-142">The display description of site design.</span></span> |
|<span data-ttu-id="d6d20-143">[-PreviewImageUrl]</span><span class="sxs-lookup"><span data-stu-id="d6d20-143">[-PreviewImageUrl]</span></span>     | <span data-ttu-id="d6d20-144">Die URL eines Vorschaubilds.</span><span class="sxs-lookup"><span data-stu-id="d6d20-144">The URL of a preview image.</span></span> <span data-ttu-id="d6d20-145">Wenn keine angegeben ist, verwendet SharePoint ein allgemeines Bild.</span><span class="sxs-lookup"><span data-stu-id="d6d20-145">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="d6d20-146">[-PreviewImageAltText]</span><span class="sxs-lookup"><span data-stu-id="d6d20-146">[-PreviewImageAltText]</span></span> | <span data-ttu-id="d6d20-147">Die Alternativtextbeschreibung des Bilds für Barrierefreiheit.</span><span class="sxs-lookup"><span data-stu-id="d6d20-147">The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="d6d20-148">[-IsDefault]</span><span class="sxs-lookup"><span data-stu-id="d6d20-148">[-IsDefault]</span></span>           | <span data-ttu-id="d6d20-149">Eine Option, die das Websitedesign auf die Standardwebsitevorlage anwendet.</span><span class="sxs-lookup"><span data-stu-id="d6d20-149">A switch that if provided, applies the site design to the default site template.</span></span> <span data-ttu-id="d6d20-150">Weitere Informationen finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="d6d20-150">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="d6d20-151">Im folgenden Beispiel wird ein neues Websitedesign erstellt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-151">The following example creates a new site design.</span></span>

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "<ID>" `
  -Description "Tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview"
```

## <a name="add-spositescript"></a><span data-ttu-id="d6d20-152">Add-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="d6d20-152">Add-SPOSiteScript</span></span>

<span data-ttu-id="d6d20-153">Lädt ein neues Websiteskript hoch, das entweder direkt oder in einem Websitedesign verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="d6d20-153">Uploads a new site script for use either directly or in a site design.</span></span>

```powershell
Add-SPOSiteScript
  -Title <string>
  -Content <string>
  [-Description <string>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-154">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-154">Parameters</span></span>

|<span data-ttu-id="d6d20-155">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-155">Parameter</span></span>     | <span data-ttu-id="d6d20-156">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-156">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="d6d20-157">-Title</span><span class="sxs-lookup"><span data-stu-id="d6d20-157">-Title</span></span>       | <span data-ttu-id="d6d20-158">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="d6d20-158">The display name of the site design.</span></span> |
| <span data-ttu-id="d6d20-159">-Content</span><span class="sxs-lookup"><span data-stu-id="d6d20-159">-Content</span></span>     | <span data-ttu-id="d6d20-160">JSON-Wert, der das Skript beschreibt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-160">JSON value that describes the script.</span></span> <span data-ttu-id="d6d20-161">Weitere Informationen finden Sie unter [JSON-Referenz](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d6d20-161">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|
| <span data-ttu-id="d6d20-162">-Description</span><span class="sxs-lookup"><span data-stu-id="d6d20-162">-Description</span></span> | <span data-ttu-id="d6d20-163">Eine Beschreibung des Skripts.</span><span class="sxs-lookup"><span data-stu-id="d6d20-163">A description of the script.</span></span> |

<span data-ttu-id="d6d20-164">Im folgenden Beispiel wird eine neue Website aus dem folgenden Skript in einer Datei hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-164">The following example adds a new site from the following script in a file.</span></span>

```json
{
  "verb": "setSiteLogo",
  "url": "https://contoso.sharepoint.com/SiteAssets/company-logo.png"
},
```

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' -Raw | Add-SPOSiteScript -Title "Customer logo" -Description "Applies customer logo for customer sites"
```

## <a name="get-spositedesign"></a><span data-ttu-id="d6d20-165">Get-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="d6d20-165">Get-SPOSiteDesign</span></span>

<span data-ttu-id="d6d20-166">Ruft Details zu Websitedesigns ab, die sich im SharePoint-Mandanten befinden.</span><span class="sxs-lookup"><span data-stu-id="d6d20-166">Gets details about site designs that are on the SharePoint tenant.</span></span> <span data-ttu-id="d6d20-167">Sie können eine ID eines bestimmten Websitedesigns angeben, das abgerufen werden soll.</span><span class="sxs-lookup"><span data-stu-id="d6d20-167">You can specify an ID of a specific site design to retrieve.</span></span> <span data-ttu-id="d6d20-168">Wenn keine Parameter aufgeführt werden, werden Details zu allen Websitedesigns aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-168">If there are no parameters listed, then details about all site designs are listed.</span></span>

```powershell
Get-SPOSiteDesign
  [[-Identity] <SPOSiteDesignPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-169">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-169">Parameters</span></span>

|<span data-ttu-id="d6d20-170">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-170">Parameter</span></span>     | <span data-ttu-id="d6d20-171">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-171">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="d6d20-172">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="d6d20-172">[-Identity]</span></span>  | <span data-ttu-id="d6d20-173">Die ID des abzurufenden Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="d6d20-173">The ID of the site design to retrieve.</span></span> |

<span data-ttu-id="d6d20-174">Das folgende Beispiel und die Beispielantwort zeigen, wie Sie Details zum Design der Website erhalten.</span><span class="sxs-lookup"><span data-stu-id="d6d20-174">The following example and sample response shows how to get site design details.</span></span>

```powershell
PS C:\> Get-SPOSiteDesign 44252d09-62c4-4913-9eb0-a2a8b8d7f863

Id                  : 44252d09-62c4-4913-9eb0-a2a8b8d7f863
Title               : Contoso - Team Project
WebTemplate         : 64
SiteScriptIds       : {1306913c-8463-42ca-bd63-efad0fcdbba4}
Description         : Use this design to apply Contoso theme and create
                      custom lists and add to nav
```

## <a name="get-spositedesignrights"></a><span data-ttu-id="d6d20-175">Get-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="d6d20-175">Get-SPOSiteDesignRights</span></span>

<span data-ttu-id="d6d20-176">Zeigt eine Liste von Prinzipalen und deren Berechtigungen zur Verwendung des Websitedesigns an.</span><span class="sxs-lookup"><span data-stu-id="d6d20-176">Displays a list of principals and their rights for usage of the site design.</span></span> <span data-ttu-id="d6d20-177">Dies kann verwendet werden, um den Bereich zu ermitteln, den Ihr Websitedesign mit Benutzern in dem Mandanten aufweist.</span><span class="sxs-lookup"><span data-stu-id="d6d20-177">This can be used to determine the scope that your site design has with users on the tenant.</span></span>

```powershell
Get-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-178">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-178">Parameters</span></span>

|<span data-ttu-id="d6d20-179">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-179">Parameter</span></span>     | <span data-ttu-id="d6d20-180">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-180">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="d6d20-181">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="d6d20-181">[-Identity]</span></span>  | <span data-ttu-id="d6d20-182">Die ID des Websitedesigns zum Abrufen von Bereichsinformationen.</span><span class="sxs-lookup"><span data-stu-id="d6d20-182">The ID of the site design to get scoping information.</span></span> |

<span data-ttu-id="d6d20-183">Im folgenden Beispiel werden die Rechte für ein Websitedesign abgerufen.</span><span class="sxs-lookup"><span data-stu-id="d6d20-183">The following example gets the rights for a site design.</span></span>

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1

DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.onmicrosoft.com   View
```

## <a name="get-spositescript"></a><span data-ttu-id="d6d20-184">Get-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="d6d20-184">Get-SPOSiteScript</span></span>

<span data-ttu-id="d6d20-185">Zeigt Informationen zu vorhandenen Websiteskripts an.</span><span class="sxs-lookup"><span data-stu-id="d6d20-185">Displays information about existing site scripts.</span></span> <span data-ttu-id="d6d20-186">Wenn kein Parameter bereitgestellt wird, gibt dieses Cmdlet **Id**, **Title**, **Description** und **Version** jedes Websiteskripts an.</span><span class="sxs-lookup"><span data-stu-id="d6d20-186">When no parameter is provided, this cmdlet returns the **Id**, **Title**, **Description**, and **Version** of each site script.</span></span> <span data-ttu-id="d6d20-187">Wenn eine Websiteskript-ID bereitgestellt wird, gibt dieses Cmdlet auch **Content** an, wobei es sich um den JSON-Code des Websiteskripts handelt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-187">When a site script ID is provided, this cmdlet also returns the **Content**, which is the JSON of the site script.</span></span>

```powershell
Get-SPOSiteScript
  [[-Identity] <SPOSiteScriptPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-188">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-188">Parameters</span></span>

|<span data-ttu-id="d6d20-189">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-189">Parameter</span></span>     | <span data-ttu-id="d6d20-190">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-190">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="d6d20-191">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="d6d20-191">[-Identity]</span></span>  | <span data-ttu-id="d6d20-192">Die ID des Websiteskripts, über das Informationen abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="d6d20-192">The ID of the site script to get information about.</span></span> |

<span data-ttu-id="d6d20-193">Das folgende Beispiel zeigt, wie Skriptinformationen für eine bestimmte Skript-ID abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="d6d20-193">The following example shows how to get script information for a specific script ID.</span></span>

```powershell
PS C:\scripts> Get-SPOSiteScript 07702c07-0485-426f-b710-4704241caad9

Id          : 07702c07-0485-426f-b710-4704241caad9
Title       : Contoso theme
Description :
Content     : {
                  "$schema": "schema.json",
                      "actions": [
                          {
                             "verb": "applyTheme",
                             "themeName": "Custom Cyan"
                          }
                      ],
                          "bindata": { },
                  "version": 1
              }
Version     : 1
```

## <a name="grant-spositedesignrights"></a><span data-ttu-id="d6d20-194">Grant-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="d6d20-194">Grant-SPOSiteDesignRights</span></span>

<span data-ttu-id="d6d20-195">Wird zum Anwenden von Berechtigungen auf einen Satz von Benutzern oder eine Sicherheitsgruppe verwendet, wodurch die Sichtbarkeit des Websitedesigns in der UX effektiv festgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="d6d20-195">Used to apply permissions to set of users or security group, effectively scoping visibility of site design in UX.</span></span> <span data-ttu-id="d6d20-196">Diese beginnen öffentlich.</span><span class="sxs-lookup"><span data-stu-id="d6d20-196">They start off public.</span></span> <span data-ttu-id="d6d20-197">Nachdem Sie jedoch Berechtigungen festgelegt haben, können nur diese Gruppen oder Benutzer auf das Websitedesign zugreifen.</span><span class="sxs-lookup"><span data-stu-id="d6d20-197">But once you set permissions, only those groups or users with permissions can access the site design.</span></span>

```powershell
Grant-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  -Rights {View}
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-198">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-198">Parameters</span></span>

|<span data-ttu-id="d6d20-199">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-199">Parameter</span></span>     | <span data-ttu-id="d6d20-200">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-200">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="d6d20-201">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="d6d20-201">[-Identity]</span></span>  | <span data-ttu-id="d6d20-202">Die ID des Websitedesigns zum Abrufen von Bereichsinformationen.</span><span class="sxs-lookup"><span data-stu-id="d6d20-202">The ID of the site design to get scoping information.</span></span> |
| <span data-ttu-id="d6d20-203">-Principals</span><span class="sxs-lookup"><span data-stu-id="d6d20-203">-Principals</span></span>  | <span data-ttu-id="d6d20-204">Eine oder mehrere Prinzipale, für die Berechtigungen hinzugefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="d6d20-204">One or more principles to add permissions for.</span></span> |
| <span data-ttu-id="d6d20-205">-Rights</span><span class="sxs-lookup"><span data-stu-id="d6d20-205">-Rights</span></span>      | <span data-ttu-id="d6d20-206">Ist immer auf den Wert **View** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-206">Always set to the value **View**.</span></span> <span data-ttu-id="d6d20-207">Alle Benutzer oder Gruppen mit Anzeigeberechtigungen können das Websitedesign anzeigen und verwenden.</span><span class="sxs-lookup"><span data-stu-id="d6d20-207">Any user or group with view permissions can view and use the site design.</span></span> |

<span data-ttu-id="d6d20-208">Im folgenden Beispiel wird gezeigt, wie Sie einem Benutzer (Nestor) auf der fiktiven Contoso-Website Anzeigeberechtigungen für ein Websitedesign erteilen können.</span><span class="sxs-lookup"><span data-stu-id="d6d20-208">The following example shows how to grant view rights on a site design to Nestor (a user at the fictional Contoso site).</span></span>

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.onmicrosoft.com" `
         -Rights View
```

## <a name="remove-spositedesign"></a><span data-ttu-id="d6d20-209">Remove-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="d6d20-209">Remove-SPOSiteDesign</span></span>

<span data-ttu-id="d6d20-210">Entfernt ein Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="d6d20-210">Removes a site design.</span></span> <span data-ttu-id="d6d20-211">Dieses wird nicht mehr in der Benutzeroberfläche zum Erstellen einer neuen Website angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-211">It will no longer appear in the UI for creating a new site.</span></span>

```powershell
  Remove-SPOSiteDesign
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-212">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-212">Parameters</span></span>

|<span data-ttu-id="d6d20-213">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-213">Parameter</span></span>     | <span data-ttu-id="d6d20-214">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-214">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="d6d20-215">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="d6d20-215">[-Identity]</span></span>  | <span data-ttu-id="d6d20-216">Die ID des zu entfernenden Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="d6d20-216">The ID of the site design to remove.</span></span> |

<span data-ttu-id="d6d20-217">Das folgende Beispiel zeigt, wie Sie ein Websitedesign entfernen.</span><span class="sxs-lookup"><span data-stu-id="d6d20-217">The following example shows how to remove a site design.</span></span>

```powershell

```

## <a name="remove-spositescript"></a><span data-ttu-id="d6d20-218">Remove-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="d6d20-218">Remove-SPOSiteScript</span></span>

<span data-ttu-id="d6d20-219">Entfernt ein Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="d6d20-219">Removes a site script.</span></span> <!-- TBD how is dependency problem handled so you don't delete a script that a design depends on. this currently creates an error when running the design.) -->

```powershell
Remove-SPOSiteScript
  [-Identity] <SPOSiteScriptPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-220">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-220">Parameters</span></span>

|<span data-ttu-id="d6d20-221">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-221">Parameter</span></span>     | <span data-ttu-id="d6d20-222">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-222">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="d6d20-223">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="d6d20-223">[-Identity]</span></span>  | <span data-ttu-id="d6d20-224">Die ID des zu entfernenden Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="d6d20-224">The ID of the site script to remove.</span></span> |

```powershell
C:\> Remove-SPOSiteDesign 21209d88-38de-4844-9823-f1f600a1179a
```

## <a name="revoke-spositedesignrights"></a><span data-ttu-id="d6d20-225">Revoke-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="d6d20-225">Revoke-SPOSiteDesignRights</span></span>

<span data-ttu-id="d6d20-226">Widerruft Berechtigungen für angegebene Prinzipale aus einem Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="d6d20-226">Revokes rights for specified principals from a site design.</span></span>

```powershell
Revoke-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-227">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-227">Parameters</span></span>

|<span data-ttu-id="d6d20-228">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-228">Parameter</span></span>     | <span data-ttu-id="d6d20-229">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-229">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="d6d20-230">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="d6d20-230">[-Identity]</span></span>  | <span data-ttu-id="d6d20-231">Die ID des Websitedesigns, aus dem Berechtigungen widerrufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="d6d20-231">The ID of the site design from which to revoke rights.</span></span> |
| <span data-ttu-id="d6d20-232">-Principals</span><span class="sxs-lookup"><span data-stu-id="d6d20-232">-Principals</span></span>  | <span data-ttu-id="d6d20-233">Mindestens ein Prinzipal zum Widerrufen von Berechtigungen im angegebenen Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="d6d20-233">One or more principals to revoke rights on the specified site design.</span></span> |

<span data-ttu-id="d6d20-234">Das folgende Beispiel zeigt, wie Sie Berechtigungen für ein Websitedesign für Nestor widerrufen.</span><span class="sxs-lookup"><span data-stu-id="d6d20-234">The following example shows how to revoke rights to a site design for Nestor.</span></span>

```powershell
PS C:\> Revoke-SPOSiteDesignRights 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
   -Principals "nestorw@contoso.onmicrosoft.com"
```

<!--
## Set-SPOSiteDesign (TBD)
Updates a previously uploaded site design.
## Set-SPOSiteScript (TBD)
Updates a previously uploaded site script.
-->

## <a name="set-spositedesign"></a><span data-ttu-id="d6d20-235">Set-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="d6d20-235">Set-SPOSiteDesign</span></span>

<span data-ttu-id="d6d20-236">Ein zuvor hochgeladenes Websitedesign wird aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="d6d20-236">Updates a previously uploaded site design.</span></span> 

```powershell
Set-SPOSiteDesign
  -Identity <SPOSiteDesignPipeBind[]>
  [-Title <string>]
  [-WebTemplate <string>]
  [-SiteScripts <SPOSiteScriptPipeBind[]>]
  [-Description <string>]
  [-PreviewImageUrl <string>]
  [-PreviewImageAltText <string>]
  [-IsDefault]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-237">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-237">Parameters</span></span>

|<span data-ttu-id="d6d20-238">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-238">Parameter</span></span>  | <span data-ttu-id="d6d20-239">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-239">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="d6d20-240">-Title</span><span class="sxs-lookup"><span data-stu-id="d6d20-240">-Title</span></span>                 | <span data-ttu-id="d6d20-241">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="d6d20-241">The display name of the site design.</span></span> |
|<span data-ttu-id="d6d20-242">-WebTemplate</span><span class="sxs-lookup"><span data-stu-id="d6d20-242">-WebTemplate</span></span>           | <span data-ttu-id="d6d20-243">Identifiziert, zu welcher Basisvorlage das Design hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="d6d20-243">Identifies which base template to add the design to.</span></span> <span data-ttu-id="d6d20-244">Verwenden Sie den Wert **64** für die Teamwebsite-Vorlage und den Wert **68** für die Kommunikationswebsitevorlage.</span><span class="sxs-lookup"><span data-stu-id="d6d20-244">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="d6d20-245">-SiteScripts</span><span class="sxs-lookup"><span data-stu-id="d6d20-245">-SiteScripts</span></span>           | <span data-ttu-id="d6d20-246">Ein Array von einem oder mehreren Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="d6d20-246">An array of one or more site scripts.</span></span> <span data-ttu-id="d6d20-247">Jedes wird durch eine ID identifziert.</span><span class="sxs-lookup"><span data-stu-id="d6d20-247">Each is identified by an ID.</span></span> <span data-ttu-id="d6d20-248">Die Skripts werden in der aufgeführten Reihenfolge ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-248">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="d6d20-249">[-Description]</span><span class="sxs-lookup"><span data-stu-id="d6d20-249">[-Description]</span></span>         | <span data-ttu-id="d6d20-250">Die Anzeigebeschreibung des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="d6d20-250">The display description of site design.</span></span> |
|<span data-ttu-id="d6d20-251">[-PreviewImageUrl]</span><span class="sxs-lookup"><span data-stu-id="d6d20-251">[-PreviewImageUrl]</span></span>     | <span data-ttu-id="d6d20-252">Die URL eines Vorschaubilds.</span><span class="sxs-lookup"><span data-stu-id="d6d20-252">The URL of a preview image.</span></span> <span data-ttu-id="d6d20-253">Wenn keine angegeben ist, verwendet SharePoint ein allgemeines Bild.</span><span class="sxs-lookup"><span data-stu-id="d6d20-253">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="d6d20-254">[-PreviewImageAltText]</span><span class="sxs-lookup"><span data-stu-id="d6d20-254">[-PreviewImageAltText]</span></span> | <span data-ttu-id="d6d20-255">Die Alternativtextbeschreibung des Bilds für Barrierefreiheit.</span><span class="sxs-lookup"><span data-stu-id="d6d20-255">The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="d6d20-256">[-IsDefault]</span><span class="sxs-lookup"><span data-stu-id="d6d20-256">[-IsDefault]</span></span>           | <span data-ttu-id="d6d20-257">Eine Option, die das Websitedesign auf die Standardwebsitevorlage anwendet.</span><span class="sxs-lookup"><span data-stu-id="d6d20-257">A switch that if provided, applies the site design to the default site template.</span></span> <span data-ttu-id="d6d20-258">Weitere Informationen finden Sie unter [Anpassen eines standardmäßigen Websitedesigns](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="d6d20-258">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="d6d20-259">Im folgende Beispiel wird ein zuvor erstelltes Websitedesign aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="d6d20-259">The following example updates a previously created site design.</span></span>

```powershell
C:\> Set-SPOSiteDesign `
  -Title "Contoso customer tracking - version 2" `
  -WebTemplate "68" `
  -Description "Updated site design for list schema that tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview - version 2"
```
## <a name="set-spositescript"></a><span data-ttu-id="d6d20-260">Set-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="d6d20-260">Set-SPOSiteScript</span></span>

<span data-ttu-id="d6d20-261">Ein zuvor hochgeladenes Websiteskript wird aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="d6d20-261">Updates a previously uploaded site script.</span></span>

```powershell
Set-SPOSiteScript
  -Title <string>
  -Content <string>
  [-Description <string>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="d6d20-262">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-262">Parameters</span></span>

|<span data-ttu-id="d6d20-263">Parameter</span><span class="sxs-lookup"><span data-stu-id="d6d20-263">Parameter</span></span>     | <span data-ttu-id="d6d20-264">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d6d20-264">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="d6d20-265">-Title</span><span class="sxs-lookup"><span data-stu-id="d6d20-265">-Title</span></span>       | <span data-ttu-id="d6d20-266">Der Anzeigename des Websitedesigns.</span><span class="sxs-lookup"><span data-stu-id="d6d20-266">The display name of the site design.</span></span> |
| <span data-ttu-id="d6d20-267">-Content</span><span class="sxs-lookup"><span data-stu-id="d6d20-267">-Content</span></span>     | <span data-ttu-id="d6d20-268">JSON-Wert, der das Skript beschreibt.</span><span class="sxs-lookup"><span data-stu-id="d6d20-268">JSON value that describes the script.</span></span> <span data-ttu-id="d6d20-269">Weitere Informationen finden Sie unter [JSON-Referenz](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d6d20-269">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|
| <span data-ttu-id="d6d20-270">-Description</span><span class="sxs-lookup"><span data-stu-id="d6d20-270">-Description</span></span> | <span data-ttu-id="d6d20-271">Eine Beschreibung des Skripts.</span><span class="sxs-lookup"><span data-stu-id="d6d20-271">A description of the script.</span></span> |

<span data-ttu-id="d6d20-272">Im folgenden Beispiel wird ein zuvor erstelltes Websiteskript aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="d6d20-272">The following example updates a previously created site script.</span></span> <span data-ttu-id="d6d20-273">Alle Websitedesigns, die darauf verweisen, führen das aktualisierte Skript aus.</span><span class="sxs-lookup"><span data-stu-id="d6d20-273">Any site designs referencing it will executed the updated script.</span></span> 

```json
{
    "$schema": "schema.json",
        "actions": [
            {
                "verb": "addNavLink",
                "url": "/Custom Library",
                "displayName": "Custom Library Updated",
                "isWebRelative": true
            },
            {
                "verb": "addNavLink",
                "url": "/Lists/Custom List",
                "displayName": "Custom List Updated",
                "isWebRelative": true
            },
            {
                "verb": "applyTheme",
                themeName: "Contoso Explorers"
            }
        ],
            "bindata": { },
    "version": 2
}
```
<span data-ttu-id="d6d20-274">In Zwischenablage kopieren</span><span class="sxs-lookup"><span data-stu-id="d6d20-274">Copy to clipboard</span></span>

```powershell
C:\> $script = Get-Clipboard -Raw
C:\> Set-SPOSiteScript -Identity 7647d3d6-1046-41fe-a798-4ff66b099d12 -Content $script -Description "Update site script to change links and apply Contoso Explorers theme"
```

## <a name="see-also"></a><span data-ttu-id="d6d20-275">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="d6d20-275">See also</span></span>

- [<span data-ttu-id="d6d20-276">JSON-Schemareferenz</span><span class="sxs-lookup"><span data-stu-id="d6d20-276">JSON schema reference</span></span>](site-design-json-schema.md)
- [<span data-ttu-id="d6d20-277">REST API</span><span class="sxs-lookup"><span data-stu-id="d6d20-277">REST API</span></span>](site-design-rest-api.md)
- [<span data-ttu-id="d6d20-278">Anwenden eines Bereichs auf Ihr Websitedesign</span><span class="sxs-lookup"><span data-stu-id="d6d20-278">Apply a scope to your site design</span></span>](site-design-scoping.md)
