# <a name="sharepoint-site-theming-powershell-cmdlets"></a><span data-ttu-id="141fe-101">SharePoint-Websitedesign: PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="141fe-101">SharePoint site theming: PowerShell cmdlets</span></span>

<span data-ttu-id="141fe-102">Mithilfe von PowerShell-Cmdlets können SharePoint-Mandantenadministratoren Websitedesigns erstellen, abrufen und entfernen.</span><span class="sxs-lookup"><span data-stu-id="141fe-102">SharePoint tenant administrators can use PowerShell cmdlets to create, retrieve, and remove site themes.</span></span> <span data-ttu-id="141fe-103">Entwickler können zur Verwaltung von Designs außerdem die [REST-API](sharepoint-site-theming-rest-api.md) verwenden.</span><span class="sxs-lookup"><span data-stu-id="141fe-103">Developers can also use the SharePoint [REST API](sharepoint-site-theming-rest-api.md) to handle theme management tasks.</span></span>

<span data-ttu-id="141fe-104">Informationen zur Definition und Speicherung von Designs finden Sie in der [JSON-Schemareferenz](sharepoint-site-theming-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="141fe-104">For information about how themes are defined and stored, see [JSON schema reference](sharepoint-site-theming-json-schema.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="141fe-105">Erste Schritte</span><span class="sxs-lookup"><span data-stu-id="141fe-105">Getting started</span></span>

<span data-ttu-id="141fe-106">Bevor Sie die PowerShell-Cmdlets zur Verwaltung von Designs nutzen können, müssen Sie Folgendes tun:</span><span class="sxs-lookup"><span data-stu-id="141fe-106">To run the PowerShell cmdlets for theme management, you'll need to do the following:</span></span>

1. <span data-ttu-id="141fe-107">Sie müssen die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunterladen und installieren.</span><span class="sxs-lookup"><span data-stu-id="141fe-107">Download and install the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span> <span data-ttu-id="141fe-108">Ist auf Ihrem System bereits eine frühere Version der Shell installiert, müssen Sie diese Version deinstallieren und anschließend die neueste Version installieren.</span><span class="sxs-lookup"><span data-stu-id="141fe-108">If you already have a previous version of the shell installed, uninstall it first and then install the latest version.</span></span>
2. <span data-ttu-id="141fe-109">Sie müssen eine Verbindung zu Ihrem SharePoint-Mandanten einrichten. Eine Anleitung finden Sie unter [Herstellen einer Verbindung mit SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx).</span><span class="sxs-lookup"><span data-stu-id="141fe-109">Follow the instructions at [Connect to SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx) to connect to your SharePoint tenant.</span></span>

<span data-ttu-id="141fe-110">Überprüfen Sie nun Ihr Setup. Rufen Sie dazu mithilfe des Cmdlets **Get-SPOHideDefaultThemes** den Wert für die Einstellung „SPOHideDefaultThemes“ ab.</span><span class="sxs-lookup"><span data-stu-id="141fe-110">To verify your setup, try using the **Get-HideDefaultThemes** cmdlet to read the HideDefaultThemes setting.</span></span> <span data-ttu-id="141fe-111">Wenn das Cmdlet fehlerfrei ausgeführt wird und den Wert „False“ zurückgibt (siehe Beispiel unten), können Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="141fe-111">If the cmdlet runs and returns False with no errors, as shown in the following example, you're ready to proceed.</span></span>

```powershell
c:\> Get-SPOHideDefaultThemes
False
```
## <a name="site-theme-cmdlets"></a><span data-ttu-id="141fe-112">Cmdlets für das Websitedesign</span><span class="sxs-lookup"><span data-stu-id="141fe-112">Site theme cmdlets</span></span>

<span data-ttu-id="141fe-113">Zur Verwaltung von Websitedesigns über die PowerShell stehen Ihnen die folgenden Cmdlets zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="141fe-113">The following cmdlets are available for managing site themes from PowerShell:</span></span>

* <span data-ttu-id="141fe-114">**Add-SPOTheme** &mdash; Erstellt ein neues benutzerdefiniertes Design oder überschreibt ein vorhandenes Design mit neuen Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="141fe-114">**Add-SPOTheme** &mdash; Creates a new custom theme, or overwrites an existing theme to modify its settings.</span></span>
* <span data-ttu-id="141fe-115">**Get-SPOTheme** &mdash; Ruft die Einstellungen eines vorhandenen Designs ab.</span><span class="sxs-lookup"><span data-stu-id="141fe-115">**Get-SPOTheme** &mdash; Retrieves settings for an existing theme.</span></span>
* <span data-ttu-id="141fe-116">**Remove-SPOTheme** &mdash; Entfernt ein Design aus dem Designkatalog.</span><span class="sxs-lookup"><span data-stu-id="141fe-116">**Remove-SPOTheme** &mdash; Removes a theme from the theme gallery.</span></span>
* <span data-ttu-id="141fe-117">**Set-SPOHideDefaultThemes** &mdash; Legt fest, ob die Standarddesigns verfügbar sein sollen.</span><span class="sxs-lookup"><span data-stu-id="141fe-117">**Set-HideDefaultThemes** &mdash; Specifies whether the default themes should be available.</span></span>
* <span data-ttu-id="141fe-118">**Get-SPOHideDefaultThemes** &mdash; Fragt den aktuellen Wert der Einstellung „SPOHideDefaultThemes“ ab.</span><span class="sxs-lookup"><span data-stu-id="141fe-118">**Get-SPOHideDefaultThemes** &mdash; Queries the current SPOHideDefaultThemes setting.</span></span>

## <a name="add-spotheme"></a><span data-ttu-id="141fe-119">Add-SPOTheme</span><span class="sxs-lookup"><span data-stu-id="141fe-119">Add-SPOTheme</span></span>

<span data-ttu-id="141fe-120">Das Cmdlet **Add-SPOTheme** erstellt ein neues Design oder aktualisiert ein vorhandenes Design.</span><span class="sxs-lookup"><span data-stu-id="141fe-120">The **Add-SPOTheme** cmdlet creates a new theme or updates an existing theme.</span></span> <span data-ttu-id="141fe-121">Die Einstellungen für die Farbpalette können entweder als Hashtabelle oder Wörterbuch übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="141fe-121">The color pallette settings can be passed as either a hash table or a dictionary.</span></span>

<span data-ttu-id="141fe-122">Im folgenden Beispiel wird ein neues Design namens „Custom Cyan“ erstellt, mit Farbpaletteneinstellungen, die verschiedene Zyanschattierungen definieren.</span><span class="sxs-lookup"><span data-stu-id="141fe-122">In the following example, a new theme named "Custom Cyan" is created, with color pallette settings that are various shades of cyan.</span></span> <span data-ttu-id="141fe-123">Beachten Sie, dass die Einstellungen als Hashtabelle übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="141fe-123">Note that the settings are passed as a hash table.</span></span>

```powershell
$themepallette = @{
  "themePrimary" = "#00ffff";
  "themeLighterAlt" = "#f3fcfc";
  "themeLighter" = "#daffff";
  "themeLight" = "#affefe";
  "themeTertiary" = "#76ffff";
  "themeSecondary" = "#39ffff";
  "themeDarkAlt" = "#00c4c4";
  "themeDark" = "#009090";
  "themeDarker" = "#005252";
  "neutralLighterAlt" = "#f8f8f8";
  "neutralLighter" = "#f4f4f4";
  "neutralLight" = "#eaeaea";
  "neutralQuaternaryAlt" = "#dadada";
  "neutralQuaternary" = "#d0d0d0";
  "neutralTertiaryAlt" = "#c8c8c8";
  "neutralTertiary" = "#a6a6a6";
  "neutralSecondaryAlt" = "#767676";
  "neutralSecondary" = "#666666";
  "neutralPrimary" = "#333";
  "neutralPrimaryAlt" = "#3c3c3c";
  "neutralDark" = "#212121";
  "black" = "#000000";
  "white" = "#fff";
  "primaryBackground" = "#fff";
  "primaryText" = "#333"
 }

Add-SPOTheme -Name "Custom Cyan" -Palette $themepallette -IsInverted $false
```

> [!NOTE]
> <span data-ttu-id="141fe-124">Bei den vor Dezember 2017 veröffentlichten Versionen der SPO-Verwaltungsshell erforderte das Cmdlet **Add-SPOTheme**, dass die Einstellungen für die Farbpalette als Wörterbuch übergeben wurden.</span><span class="sxs-lookup"><span data-stu-id="141fe-124">Prior to the December 2017 release of SPO Management Shell, the **Add-SPOTheme** cmdlet required that color pallette settings be passed as a dictionary.</span></span> <span data-ttu-id="141fe-125">Es wird empfohlen, die neueste Version der SPO-Verwaltungsshell zu verwenden. Die folgende ```HashToDictionary```-Funktion kann jedoch verwendet werden, um eine Hashtabelle bei Bedarf in ein Wörterbuch zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="141fe-125">We recommend that you use the latest version of the SPO Management Shell, however the following ```HashToDictionary``` function can be used to convert a hash table to a dictionary if needed.</span></span>

```powershell
function HashToDictionary {
  Param ([Hashtable]$ht)
  $dictionary = New-Object "System.Collections.Generic.Dictionary``2[System.String,System.String]"
  foreach ($entry in $ht.GetEnumerator()) {
    $dictionary.Add($entry.Name, $entry.Value)
  }
  return $dictionary
}
```
<span data-ttu-id="141fe-126">Wenn Sie ein vorhandenes Design aktualisieren möchten (beispielsweise mit neuen Farbeinstellungen), verwenden Sie dieselbe Syntax wie im vorherigen Beispiel, fügen jedoch das Flag *-Overwrite* zum Cmdlet **Add-SPOTheme** hinzu.</span><span class="sxs-lookup"><span data-stu-id="141fe-126">If you want to update an existing theme (to modify some of its color settings, for example), use the same syntax as shown previously but add the *-Overwrite* flag to the **Add-SPOTheme** cmdlet.</span></span>

```powershell
Add-SPOTheme -Name "Custom Cyan" -Palette $themepallette -IsInverted $false -Overwrite
```
<span data-ttu-id="141fe-127">Wenn Sie ein Design hinzufügen, wird es noch nicht auf Websites angewendet.</span><span class="sxs-lookup"><span data-stu-id="141fe-127">Adding a theme does not apply the theme to any sites.</span></span> <span data-ttu-id="141fe-128">Das Design wird lediglich zum Store Ihres Mandanten hinzugefügt und steht dann auf modernen Seiten in der Designliste unter **Change the look** zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="141fe-128">It adds the theme to your tenant store, and then the theme will be available in the list of themes under the **Change the look** option for modern pages.</span></span>

## <a name="get-spotheme"></a><span data-ttu-id="141fe-129">Get-SPOTheme</span><span class="sxs-lookup"><span data-stu-id="141fe-129">Get-SPOTheme</span></span>

<span data-ttu-id="141fe-130">Das Cmdlet **Get-SPOTheme** gibt die Einstellungen für ein vorhandenes angegebenes Design zurück oder für alle hochgeladenen Designs, wenn kein Designname angegeben wurde.</span><span class="sxs-lookup"><span data-stu-id="141fe-130">The **Get-SPOTheme** cmdlet returns the settings for a named existing theme, or for all uploaded themes if no name is provided.</span></span>

<span data-ttu-id="141fe-131">Mit dem folgenden Code können Sie über das Cmdlet **Get-SPOTheme** die Einstellungen des Designs „Custom Cyan“ abrufen, das Sie im vorherigen Beispiel erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="141fe-131">For example, here's how to use the **Get-SPOTheme** cmdlet to return the settings for the "Custom Cyan" theme created in the previous example.</span></span>

```powershell
C:\> Get-SPOTheme -Name "Custom Cyan" | ConvertTo-Json
```
```json
{
    "Name":  "Custom Cyan",
    "Palette":  {
                    "themeLight":  "#affefe",
                    "themeTertiary":  "#76ffff",
                    "black":  "#000000",
                    "neutralSecondary":  "#666666",
                    "neutralTertiaryAlt":  "#c8c8c8",
                    "themeSecondary":  "#39ffff",
                    "themeDarker":  "#005252",
                    "primaryBackground":  "#fff",
                    "neutralQuaternary":  "#d0d0d0",
                    "neutralPrimaryAlt":  "#3c3c3c",
                    "neutralPrimary":  "#333",
                    "themeDark":  "#009090",
                    "themeLighter":  "#daffff",
                    "neutralTertiary":  "#a6a6a6",
                    "neutralQuaternaryAlt":  "#dadada",
                    "themeLighterAlt":  "#f3fcfc",
                    "white":  "#fff",
                    "neutralSecondaryAlt":  "#767676",
                    "neutralLighter":  "#f4f4f4",
                    "neutralLight":  "#eaeaea",
                    "neutralDark":  "#212121",
                    "themeDarkAlt":  "#00c4c4",
                    "neutralLighterAlt":  "#f8f8f8",
                    "primaryText":  "#333",
                    "themePrimary":  "#00ffff"
                },
    "IsInverted":  false
}
```
<span data-ttu-id="141fe-132">Wie Sie sehen, verwenden wir in diesem Beispiel den PowerShell-Filter _ConvertTo-Json_, um das Design im JSON-Format abzurufen.</span><span class="sxs-lookup"><span data-stu-id="141fe-132">Note that this example uses the PowerShell _ConvertTo-Json_ filter to display the theme in JSON format.</span></span>

<span data-ttu-id="141fe-133">Um alle hochgeladenen Designs zurückzugeben, verwenden Sie den **Get-SPOTheme**-Befehl ohne Argumente:</span><span class="sxs-lookup"><span data-stu-id="141fe-133">To return all uploaded themes, use the **Get-SPOTheme** command with no arguments:</span></span>

```powershell
C:\> Get-SPOTheme
```

<span data-ttu-id="141fe-134">Im Folgenden ein Beispiel der Ausgabe dieses Befehls:</span><span class="sxs-lookup"><span data-stu-id="141fe-134">Here's an example of the output from this command:</span></span>

![Beispiel zu Get-SPOTheme](../../images/Get-SPOTheme-example.png)

## <a name="remove-spotheme"></a><span data-ttu-id="141fe-136">Remove-SPOTheme</span><span class="sxs-lookup"><span data-stu-id="141fe-136">Remove-SPOTheme</span></span>

<span data-ttu-id="141fe-137">Das Cmdlet **Remove-SPOTheme** entfernt ein Design aus dem Store Ihres Mandanten.</span><span class="sxs-lookup"><span data-stu-id="141fe-137">The **Remove-SPOTheme** cmdlet removes a theme from your tenant store.</span></span> <span data-ttu-id="141fe-138">Das Cmdlet unten beispielsweise entfernt das Design „Custom Cyan“, das wir in den vorherigen Beispielen verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="141fe-138">For example, this cmdlet removes the "Custom Cyan" theme that was used in the previous examples.</span></span>

```powershell
c:\> Remove-SPOTheme -Name "Custom Cyan"
```
## <a name="set-spohidedefaultthemes"></a><span data-ttu-id="141fe-139">Set-SPOHideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="141fe-139">Set-SPOHideDefaultThemes</span></span>

> [!NOTE]
> <span data-ttu-id="141fe-140">Dieses Cmdlet wurde vor der im Dezember 2017 veröffentlichen Version der SPO-Verwaltungsshell als ```Set-HideDefaultThemes``` bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="141fe-140">This cmdlet was named ```Set-HideDefaultThemes``` until the December 2017 release of SPO Management Shell.</span></span> <span data-ttu-id="141fe-141">Es wird empfohlen, die neueste Version der PowerShell-Cmdlets zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="141fe-141">We recommend that you use the latest version of the PowerShell cmdlets.</span></span>

<span data-ttu-id="141fe-142">Das Cmdlet **Set-SPOHideDefaultThemes** gibt an, ob die in SharePoint integrierten Standarddesigns in der Liste aufgeführt werden sollen, die Ihnen in der Designauswahl zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="141fe-142">The **Set-HideDefaultThemes** cmdlet is used to specify whether the default themes that come with SharePoint should be included in the theme picker list.</span></span> <span data-ttu-id="141fe-143">Beispiel: Sie möchten benutzerdefinierte Designs für Ihre Websites erstellen und anschließend die Standarddesigns entfernen, damit auf alle Seiten Ihre benutzerdefinierten Designs angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="141fe-143">For example, you might want to create custom themes for your sites and then remove the default themes, to ensure that all pages will use your custom themes.</span></span>

<span data-ttu-id="141fe-144">Wenn Sie die Einstellung auf _$true_ setzen, werden die Standarddesigns ausgeblendet, wenn Sie sie auf _$false_ setzen (Standardeinstellung) werden sie angezeigt.</span><span class="sxs-lookup"><span data-stu-id="141fe-144">Specify the setting as either _$true_ to hide the default themes, or _$false_ (the default setting) to allow use of the default themes.</span></span> <span data-ttu-id="141fe-145">Das Cmdlet unten blendet die Standarddesigns aus:</span><span class="sxs-lookup"><span data-stu-id="141fe-145">For example, this cmdlet hides the default themes.</span></span>

```powershell
Set-SPOHideDefaultThemes $true
```
<span data-ttu-id="141fe-146">Wenn Sie das Design „Custom Cyan“ erstellen und anschließend die Standarddesigns ausblenden, wird in der Designliste unter **Change the look** nur noch dieses eine benutzerdefinierte Design angezeigt.</span><span class="sxs-lookup"><span data-stu-id="141fe-146">After creating the "Custom Cyan" theme, hiding the default themes will leave only the one custom theme in the themes list under **Change the look**.</span></span>

<span data-ttu-id="141fe-147">Sollen die Standarddesigns wieder in der Designauswahl angezeigt werden, können Sie das folgende Cmdlet verwenden.</span><span class="sxs-lookup"><span data-stu-id="141fe-147">To restore the default themes to the theme picker list, use the following cmdlet.</span></span>
```powershell
Set-SPOHideDefaultThemes $false
```

## <a name="get-spohidedefaultthemes"></a><span data-ttu-id="141fe-148">Get-SPOHideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="141fe-148">Get-SPOHideDefaultThemes</span></span>

> [!NOTE]
> <span data-ttu-id="141fe-149">Dieses Cmdlet wurde vor der im Dezember 2017 veröffentlichen Version der SPO-Verwaltungsshell als ```Get-HideDefaultThemes``` bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="141fe-149">this cmdlet was named ```Get-HideDefaultThemes``` until the December 2017 release of SPO Management Shell.</span></span> <span data-ttu-id="141fe-150">Es wird empfohlen, die neueste Version der PowerShell-Cmdlets zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="141fe-150">We recommend that you use the latest version of the PowerShell cmdlets.</span></span>

<span data-ttu-id="141fe-151">Das Cmdlet **Get-SPOHideDefaultThemes** ruft den aktuellen Wert für die Einstellung **Set-SPOHideDefaultThemes** ab.</span><span class="sxs-lookup"><span data-stu-id="141fe-151">The **Get-HideDefaultThemes** cmdlet retrieves the currrent **Set-HideDefaultThemes** setting.</span></span> <span data-ttu-id="141fe-152">Sie können dieses Cmdlet in ein PowerShell-Skript aufnehmen, um diese Einstellung auszulesen und eine bestimmte Aktion einzuleiten, je nachdem, ob die Standarddesigns angezeigt werden oder nicht.</span><span class="sxs-lookup"><span data-stu-id="141fe-152">You might want to use this cmdlet in a PowerShell script to read the setting and then take different actions based on whether the default themes are hidden.</span></span> <span data-ttu-id="141fe-153">Dieses Cmdlet hat keine Parameter.</span><span class="sxs-lookup"><span data-stu-id="141fe-153">This cmdlet does not have any parameters.</span></span>

```powershell
c:\> Get-SPOHideDefaultThemes
False
```

## <a name="see-also"></a><span data-ttu-id="141fe-154">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="141fe-154">See also</span></span>

* [<span data-ttu-id="141fe-155">Überblick über SharePoint-Websitedesign</span><span class="sxs-lookup"><span data-stu-id="141fe-155">SharePoint site theming overview</span></span>](sharepoint-site-theming-overview.md)
* [<span data-ttu-id="141fe-156">SharePoint-Websitedesign: JSON-Schema</span><span class="sxs-lookup"><span data-stu-id="141fe-156">SharePoint site theming: JSON schema</span></span>](sharepoint-site-theming-json-schema.md)
* [<span data-ttu-id="141fe-157">SharePoint-Websitedesign: CSOM</span><span class="sxs-lookup"><span data-stu-id="141fe-157">SharePoint site theming: CSOM</span></span>](sharepoint-site-theming-csom.md)
* [<span data-ttu-id="141fe-158">SharePoint-Websitedesign: REST-API</span><span class="sxs-lookup"><span data-stu-id="141fe-158">SharePoint site theming: REST API</span></span>](sharepoint-site-theming-rest-api.md)
* [<span data-ttu-id="141fe-159">SharePoint Online-Verwaltungsshell</span><span class="sxs-lookup"><span data-stu-id="141fe-159">SharePoint Online Management Shell</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=35588)
* <span data-ttu-id="141fe-160">[Herstellen einer Verbindung mit SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx)</span><span class="sxs-lookup"><span data-stu-id="141fe-160">[Connect to SharePoint Online PowerShell](https://technet.microsoft.com/de-DE/library/fp161372.aspx)</span></span>
