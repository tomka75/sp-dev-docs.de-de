---
title: SharePoint-Websites "modernen" Klassifizierung
description: "Konfigurieren von außerhalb der im Feld Website-Klassifizierung für moderne SharePoint-Websites."
ms.date: 12/19/2017
ms.openlocfilehash: 8dbff0c128f96120a693a9341604b00616700e64
ms.sourcegitcommit: bf4bc1e80c6ef1a0ff479039ef9ae0ee84d5f6b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2017
---
# <a name="sharepoint-modern-sites-classification"></a><span data-ttu-id="5257a-103">SharePoint-Websites "modernen" Klassifizierung</span><span class="sxs-lookup"><span data-stu-id="5257a-103">SharePoint "modern" sites classification</span></span>
<span data-ttu-id="5257a-104">Wenn Sie in SharePoint Online "modernen" Websites erstellen, können Sie optional 'Website Klassifikation' definieren die Vertraulichkeit Ihrer Daten Website auswählen.</span><span class="sxs-lookup"><span data-stu-id="5257a-104">When you create "modern" sites in SharePoint Online, you can optionally select a 'Site Classification' to define the sensitivity of your site data.</span></span> <span data-ttu-id="5257a-105">Das Ziel der Website Klassifizierung ist mit ermöglichen, Verwalten von Clustern von Websites basierend auf ihrer Klassifizierung Unternehmensleitung und Compliance im Hinblick auf sowie, basierte auf der Website Klassifizierung Governance-Prozessen zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="5257a-105">The goal of site classification is to allow managing clusters of sites based on their classification from a governance and compliance perspective, as well as to automate governance processes based on site classification.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5257a-106">Die Option 'Website-Klassifizierung' ist nicht standardmäßig aktiviert, und müssen Sie es auf der Ebene der Azure AD konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="5257a-106">The 'Site Classification' option is not enabled by default, and you need to configure it at the Azure AD level.</span></span>

## <a name="enabling-site-classification-in-your-tenant"></a><span data-ttu-id="5257a-107">Aktivieren in Ihrem Mandanten 'Website-Klassifizierung'</span><span class="sxs-lookup"><span data-stu-id="5257a-107">Enabling 'Site Classification' in your tenant</span></span>

<span data-ttu-id="5257a-108">Um der 'Website Klassifikation' profitieren müssen Sie diese Funktion auf Ebene der Azure AD in Ihrem Ziel-Mandanten zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="5257a-108">In order to benefit of 'Site Classification' you need to enable this capability at the Azure AD level, in your target tenant.</span></span> <span data-ttu-id="5257a-109">Nachdem Sie diese Funktion aktiviert haben, sehen Sie ein weiteres Feld "Wie Sensititive Ihre Daten ist?"</span><span class="sxs-lookup"><span data-stu-id="5257a-109">Once you have enabled this capability, you will see an additional field 'How sensititive is your data?'</span></span> <span data-ttu-id="5257a-110">Beim Erstellen neuer Websites "modernen".</span><span class="sxs-lookup"><span data-stu-id="5257a-110">while creating new "modern" sites.</span></span> <span data-ttu-id="5257a-111">In der folgenden Abbildung sehen Sie, wie das Feld 'Website Klassifikation' aussieht.</span><span class="sxs-lookup"><span data-stu-id="5257a-111">In the following figure you can see how the 'Site Classification' field looks like.</span></span>

![Die Option "Website-Klassifizierung" beim Erstellen einer "modernen" Website in SharePoint Online](media/modern-experiences/site-classification-ui.png)

<span data-ttu-id="5257a-113">Klicken Sie in der folgenden Abbildung sehen Sie die Klassifizierung nutzen, die in der Kopfzeile einer "modernen" Website.</span><span class="sxs-lookup"><span data-stu-id="5257a-113">While in the following figure, you can see the classification highlighted in the header of a "modern" site.</span></span>

![Die Klassifizierung"Website" hervorgehoben in der Kopfzeile einer "modernen" Website](media/modern-experiences/site-classification-ui-output.png)

### <a name="enabling-site-classification-with-powershell"></a><span data-ttu-id="5257a-115">Aktivieren "Website-Klassifizierung' mit PowerShell</span><span class="sxs-lookup"><span data-stu-id="5257a-115">Enabling 'Site Classification' with PowerShell</span></span>
<span data-ttu-id="5257a-116">Führen Sie zum Aktivieren der Funktion "Website-Klassifizierung" eine Reihe von PowerShell-Code, wie unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5257a-116">To enable the 'Site Classification' capability you can execute a bunch of PowerShell code, like the one illustrated below.</span></span>

```ps
# Install the AzureAD Preview Module for PowerShell
Install-Module AzureADPreview

# Connect to Azure AD
Connect-AzureAD

# Create new directory setting and set initial values
$template = Get-AzureADDirectorySettingTemplate | where { $_.DisplayName -eq "Group.Unified" }

$setting = $template.CreateDirectorySetting()
$setting["UsageGuidelinesUrl"] = "https://aka.ms/sppnp"
$setting["ClassificationList"] = "HBI, MBI, LBI, GDPR"
$setting["DefaultClassification"] = "MBI"
New-AzureADDirectorySetting -DirectorySetting $setting

```

> [!NOTE]
> <span data-ttu-id="5257a-117">Erwägen Sie, dass eine While (ungefähr 1 Stunde oder mehr) benötigt wird, um die Einstellungen in der Benutzeroberfläche von Office 365 verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="5257a-117">Please, consider that it takes a while (about 1 hour or more) to have the settings available in the UI of Office 365.</span></span>

<span data-ttu-id="5257a-118">Über den Codeausschnitt befindlichen Anwendung lohnt zu sagen, dass die RTM-Version verwenden können ziemlich bald werden jedoch zum Zeitpunkt der Erstellung dieses Dokuments Sie die Vorabversion von AzureAD-Cmdlets verwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="5257a-118">About the code snippet above, it worth it to say that at the time of this writing you have to use the preview version of the AzureAD cmdlets, but pretty soon you will be able to use the RTM version.</span></span>
<span data-ttu-id="5257a-119">Nachdem Sie die Cmdlets AzureAD installiert haben, müssen Sie einfach mit dem Ziel Azure AD-Mandanten herzustellen, die Ihre Ziel-SharePoint Online-Mandanten sichern wird.</span><span class="sxs-lookup"><span data-stu-id="5257a-119">Once you have installed the AzureAD cmdlets, you simply need to connect to the target Azure AD tenant, which is backing your target SharePoint Online tenant.</span></span>
<span data-ttu-id="5257a-120">Mit dem Cmdlet _Get-AzureADDirectorySettingTemplate_ erhalten Sie einen Verweis auf die Vorlage"Einstellung" für die "Unified Gruppen', also einen mit _DisplayName_ der 'Group.Unified'.</span><span class="sxs-lookup"><span data-stu-id="5257a-120">Using the _Get-AzureADDirectorySettingTemplate_ cmdlet you get a reference to the 'Setting Template' for the 'Unified Groups', which is the one with _DisplayName_ of 'Group.Unified'.</span></span>
<span data-ttu-id="5257a-121">Nachdem Sie die Vorlage verfügen, können Sie die Einstellungen dieser Vorlage durch Erstellen einer neuen _Verzeichnisberechtigungen_ und Bereitstellen der Einstellungswerte über ein Wörterbuch konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="5257a-121">Once you have the template, you can configure the settings of that template by creating a new _DirectorySetting_ and providing the setting values through a dictionary.</span></span>

<span data-ttu-id="5257a-122">Die wichtigsten Einstellungen, aus der Sicht "Website Klassifizierung" lauten:</span><span class="sxs-lookup"><span data-stu-id="5257a-122">The main settings, from a 'Site Classification' perspective are:</span></span>
* <span data-ttu-id="5257a-123">**UsageGuidelinesUrl**: die URL einer Seite, auf dem Sie erklären können, was die unterschiedlichen Optionen sind.</span><span class="sxs-lookup"><span data-stu-id="5257a-123">**UsageGuidelinesUrl**: the URL of a page where you can explain what are the different classification options.</span></span> <span data-ttu-id="5257a-124">Ein Link zu dieser Seite werden im Formular Site Creation und in der Kopfzeile jeder geschützten Website angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5257a-124">A link to that page will show up in the site creation form and in the header of every classified site.</span></span>
* <span data-ttu-id="5257a-125">**ClassificationList**: eine durch Trennzeichen getrennte Liste mit Werten für die Liste der 'Website-Klassifizierung' Optionen.</span><span class="sxs-lookup"><span data-stu-id="5257a-125">**ClassificationList**: a comma separated list of values for the 'Site Classification' options list.</span></span>
* <span data-ttu-id="5257a-126">**DefaultClassification**: der Standardwert für die Klassifizierung"Website".</span><span class="sxs-lookup"><span data-stu-id="5257a-126">**DefaultClassification**: the default value for the 'Site Classification'.</span></span>

### <a name="enabling-site-classification-with-pnp-core-library"></a><span data-ttu-id="5257a-127">Aktivieren "Website-Klassifizierung' mit Plug & Play-Core-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="5257a-127">Enabling 'Site Classification' with PnP Core Library</span></span>

<span data-ttu-id="5257a-128">Eine weitere Möglichkeit, die Sie zum Aktivieren der Funktion "Website-Klassifizierung" ist der Plug & Play-Hauptbibliothek einsetzen, mit dem einige Erweiterungsmethoden zum Verwalten von Klassifizierung in C#-Code enthält.</span><span class="sxs-lookup"><span data-stu-id="5257a-128">Another option that you have to enable the 'Site Classification' capability is to leverage the PnP Core Library, which provides few extension methods to manage classification in C# code.</span></span>
<span data-ttu-id="5257a-129">Beispielsweise können Sie C#-Code wie unten dargestellt, um die Klassifizierung' Website' aktivieren schreiben.</span><span class="sxs-lookup"><span data-stu-id="5257a-129">For example, to enable the 'Site Classification' you can write C# code like the one illustrated below.</span></span>

```C#
// Connect to the admin central of your tenant
using (var adminContext = new ClientContext("https://[tenant]-admin.sharepoint.com/"))
{
    // Provide a valid set of credentials
    adminContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Create a new instance of the Tenant class of CSOM
    var tenant = new Tenant(adminContext);

    // Get an Azure AD Access Token using ADAL, MSAL, or whatever else you like
    var accessToken = getAzureADAccessToken();

    // Define the list of classifications
    var newClassificationList = new List<String>();
    newClassificationList.Add("HBI");
    newClassificationList.Add("MBI");
    newClassificationList.Add("LBI");
    newClassificationList.Add("GDPR");

    // Use the PnP extension method to enable 'Site Classification'
    // Including a default classification value and a the URL to an informative page
    tenant.EnableSiteClassifications(accessToken, newClassificationList, "MBI", "http://aka.ms/OfficeDevPnP");
}

```

## <a name="updating-or-removing-site-classification-in-your-tenant"></a><span data-ttu-id="5257a-130">Aktualisieren oder Entfernen von "Website-Klassifizierung" in Ihrem Mandanten</span><span class="sxs-lookup"><span data-stu-id="5257a-130">Updating or Removing 'Site Classification' in your tenant</span></span>

<span data-ttu-id="5257a-131">Wie für die Aktivierung der 'Website Klassifikation', aktualisieren oder entfernen die Einstellung erfolgen kann entweder mithilfe von PowerShell oder PnP Core-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="5257a-131">As like as for enabling the 'Site Classification', updating or removing the setting can be done either using PowerShell or PnP Core Library.</span></span>

### <a name="updating-or-removing-site-classification-with-powershell"></a><span data-ttu-id="5257a-132">Aktualisieren oder Entfernen von 'Site Klassifizierung' mit PowerShell</span><span class="sxs-lookup"><span data-stu-id="5257a-132">Updating or Removing 'Site Classification' with PowerShell</span></span>

<span data-ttu-id="5257a-133">Wenn Sie anschließend die Einstellungen 'Website Klassifizierung' aktualisieren müssen, können Sie den folgenden PowerShell-Codeausschnitt.</span><span class="sxs-lookup"><span data-stu-id="5257a-133">If you need to update the 'Site Classification' settings afterwards, you can use the following PowerShell snippet.</span></span>

```PowerShell
# Connect to Azure AD
Connect-AzureAD

# Read current settings
(Get-AzureADDirectorySetting | where { $_.DisplayName -eq "Group.Unified" }).Values

# Update settings
$currentSettings = Get-AzureADDirectorySetting | where { $_.DisplayName -eq "Group.Unified" }
$currentSettings["UsageGuidelinesUrl"] = "https://aka.ms/sppnp"
$currentSettings["ClassificationList"] = "HBI, MBI, LBI, GDPR"
$currentSettings["DefaultClassification"] = "MBI"
Set-AzureADDirectorySetting -Id $currentSettings.Id -DirectorySetting $currentSettings
```

> [!NOTE]
> <span data-ttu-id="5257a-134">Erwägen Sie, dass eine While (ungefähr 1 Stunde oder mehr) benötigt wird, um die Einstellungen in der Benutzeroberfläche von Office 365 aktualisiert haben.</span><span class="sxs-lookup"><span data-stu-id="5257a-134">Please, consider that it takes a while (about 1 hour or more) to have the settings updated in the UI of Office 365.</span></span> <span data-ttu-id="5257a-135">Großes Problem sollte sie jedoch nicht, da Sie die Einstellungen für "Website-Klassifizierung" sehr häufig aktualisieren sollte nicht.</span><span class="sxs-lookup"><span data-stu-id="5257a-135">However, it shouldn't be a big issue, because you shouldn't update the 'Site Classification' settings very often.</span></span>

<span data-ttu-id="5257a-136">Wie Sie sehen können, müssen Sie lediglich die Directory-Einstellung mit dem Wert _DisplayName_ 'Group.Unified' Suchen und dann aktualisieren Sie die Einstellungswerte und übernehmen Sie die mit dem Cmdlet _Set-AzureADDirectorySetting_ .</span><span class="sxs-lookup"><span data-stu-id="5257a-136">As you can see, you simply need to search for the Directory Setting with a _DisplayName_ value of 'Group.Unified' and then you can update its setting values and apply the changes by using the _Set-AzureADDirectorySetting_ cmdlet.</span></span>

<span data-ttu-id="5257a-137">Zum Entfernen der Klassifikation"Website" können Sie das Cmdlet _Remove-AzureADDirectorySetting_ wie im folgenden Codeausschnitt verwenden.</span><span class="sxs-lookup"><span data-stu-id="5257a-137">To remove a 'Site Classification' you can use the _Remove-AzureADDirectorySetting_ cmdlet, like in the following code snippet.</span></span>

```ps
# Delete settings
$currentSettings = Get-AzureADDirectorySetting | where { $_.DisplayName -eq "Group.Unified" }
Remove-AzureADDirectorySetting -Id $currentSettings.Id
```

### <a name="updating-or-removing-site-classification-with-pnp-core-library"></a><span data-ttu-id="5257a-138">Aktualisieren oder Entfernen von 'Site Klassifizierung' mit Plug & Play-Core-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="5257a-138">Updating or Removing 'Site Classification' with PnP Core Library</span></span>

<span data-ttu-id="5257a-139">Eine weitere Option, die Ihnen ist die Plug & Play-Kern-Bibliothek verwenden.</span><span class="sxs-lookup"><span data-stu-id="5257a-139">Another option that you have is to use the PnP Core Library.</span></span>
<span data-ttu-id="5257a-140">Beispielsweise können Sie zum Aktualisieren der Klassifikation"Website" C#-Code wie unten dargestellt schreiben.</span><span class="sxs-lookup"><span data-stu-id="5257a-140">For example, to update the 'Site Classification' you can write C# code like the one illustrated below.</span></span>

```C#
// Connect to the admin central of your tenant
using (var adminContext = new ClientContext("https://[tenant]-admin.sharepoint.com/"))
{
    // Provide a valid set of credentials
    adminContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Create a new instance of the Tenant class of CSOM
    var tenant = new Tenant(adminContext);

    // Get an Azure AD Access Token using ADAL, MSAL, or whatever else you like
    var accessToken = getAzureADAccessToken();

    // Retrieve the current set of values for 'Site Classification'
    var classificationList = tenant.GetSiteClassificationList(accessToken);
    
    // And update it by adding a new value
    var updatedClassificationList = new List<String>(classificationList);
    updatedClassificationList.Add("TopSecret");

    // Update the 'Site Classification' settings accordingly
    tenant.UpdateSiteClassificationSettings(accessToken, updatedClassificationList, "MBI", "http://aka.ms/SharePointPnP");
}
```

<span data-ttu-id="5257a-141">Darüber hinaus können Sie zum Deaktivieren und entfernen die Einstellungen 'Website Klassifizierung', wie im folgenden Codeausschnitt verwenden.</span><span class="sxs-lookup"><span data-stu-id="5257a-141">Moreover, in order to disable and remove the 'Site Classification' settings, you can use a code snippet like the following one.</span></span>

```C#
// Connect to the admin central of your tenant
using (var adminContext = new ClientContext("https://[tenant]-admin.sharepoint.com/"))
{
    // Provide a valid set of credentials
    adminContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Create a new instance of the Tenant class of CSOM
    var tenant = new Tenant(adminContext);

    // Get an Azure AD Access Token using ADAL, MSAL, or whatever else you like
    var accessToken = getAzureADAccessToken();

    // Disable the 'Site Classification' settings
    tenant.DisableSiteClassifications(accessToken);
}
```

## <a name="managing-the-classification-of-a-site"></a><span data-ttu-id="5257a-142">Verwalten von der Klassifikation einer Website</span><span class="sxs-lookup"><span data-stu-id="5257a-142">Managing the classification of a site</span></span>

<span data-ttu-id="5257a-143">Der Wert der Klassifizierung für eine Website gelesen werden kann, oder aktualisiert, später mithilfe der Benutzeroberfläche von SharePoint Online, wie Sie sehen in der folgenden Abbildung, durch die Einstellungen 'Standortinformationen' bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="5257a-143">The value of classification for a site can be read, or updated, later on using the UI of SharePoint Online, as you can see in the following figure, by editing the 'Site Information' settings.</span></span>

![Die Option 'Website-Klassifizierung' während der Bearbeitung der Einstellungen 'Standortinformationen' einer "modernen" Website in SharePoint Online](media/modern-experiences/site-classification-update-ui.png)

### <a name="programmatically-reading-the-classification-of-a-site"></a><span data-ttu-id="5257a-145">Programmgesteuertes Lesen der Klassifikation einer Website</span><span class="sxs-lookup"><span data-stu-id="5257a-145">Programmatically reading the classification of a site</span></span>

<span data-ttu-id="5257a-146">Aus der Perspektive eines Entwicklers können Sie CSOM und der REST-API von SharePoint Online zum Lesen und schreiben den Wert der Klassifikation für einen bestimmten Standort.</span><span class="sxs-lookup"><span data-stu-id="5257a-146">From a developer's perspective, you can use CSOM and the REST API of SharePoint Online to read and write the value of classification for a specific site.</span></span> <span data-ttu-id="5257a-147">Tatsächlich hat jeder SharePoint Online-Websitesammlung die _Klassifizierung_ -Eigenschaft, die Sie verwenden können, lesen Sie die Website-Klassifizierung.</span><span class="sxs-lookup"><span data-stu-id="5257a-147">In fact, every SharePoint Online site collection has the _Classification_ property that you can use to read the site classification.</span></span> 

<span data-ttu-id="5257a-148">Hier sehen Sie einen PowerShell Ausschnitt dafür.</span><span class="sxs-lookup"><span data-stu-id="5257a-148">Here you can see a PowerShell snippet to do that.</span></span>

```ps
# Delete settings
Connect-PnPOnline "https://[tenant].sharepoint.com/sites/[modernsite]" -Credentials [credentials]

$site = Get-PnPSite
$classificationValue = Get-PnPProperty -ClientObject $site -Property Classification
Write-Host $classificationValue
```

<span data-ttu-id="5257a-149">Wenn Sie den Wert für "Website-Klassifizierung" mit REST lesen möchten, können beispielsweise in einem SharePoint-Framework-Client-Side-Webpart den folgenden REST-Endpunkt verwenden:</span><span class="sxs-lookup"><span data-stu-id="5257a-149">If you like to read the 'Site Classification' value using REST, for example within a SharePoint Framework client-side web part, you can use the following REST endpoint:</span></span>

```TEXT
https://[tenant].sharepoint.com/sites/[modernsite]/_api/site/Classification
```

<span data-ttu-id="5257a-150">Basierend auf der Klassifizierungswert einer Website, können Sie die Automatisierung und benutzerdefinierten Richtlinien definieren.</span><span class="sxs-lookup"><span data-stu-id="5257a-150">Based on the classification value of a site, you can define automation and custom policy rules.</span></span>

<span data-ttu-id="5257a-151">In der Hauptbibliothek Plug & Play-ist es eine Erweiterungsmethode für die Website der CSOM, dem Sie auf einfache Weise den Klassifizierungswert einer Website gelesen werden kann.</span><span class="sxs-lookup"><span data-stu-id="5257a-151">In the PnP Core Library there is an extension method for the Site object of CSOM, which allows you to easily read the classification value of a site.</span></span> <span data-ttu-id="5257a-152">Im folgenden Codeausschnitt sehen Sie, wie Sie diese Erweiterungsmethode verwenden können.</span><span class="sxs-lookup"><span data-stu-id="5257a-152">In the following code snippet you can see how to leverage this extension method.</span></span>

```C#
// Connect to the target site collectiion
using (var clientContext = new ClientContext("https://[tenant].sharepoint.com/sites/[modernsite]"))
{
    // Provide a valid set of credentials
    clientContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Read the current classification value
    var currentClassification = clientContext.Site.GetSiteClassification();
}
```

### <a name="programmatically-updating-the-classification-of-a-site"></a><span data-ttu-id="5257a-153">Programmgesteuerte Aktualisierung der Klassifikation einer Website</span><span class="sxs-lookup"><span data-stu-id="5257a-153">Programmatically updating the classification of a site</span></span>

<span data-ttu-id="5257a-154">Wenn Ihr Ziel einer Website "modernen" Kommunikation ist, können Sie die _Klassifizierung_ -Eigenschaft des CSOM verwenden, um den Wert zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="5257a-154">If your target is a  "modern" communication site, you can use the _Classification_ property of CSOM to update the value, too.</span></span>

<span data-ttu-id="5257a-155">Ihr Ziel einer Teamwebsite "modernen" und den Klassifizierungswert aktualisieren möchten, sollten Sie das Microsoft Graph verwenden, da die _Klassifizierung_ -Eigenschaft des CSOM einfach den Wert der Eigenschaft _Klassifizierung_ der Office 365 repliziert Mitglied der Gruppe.</span><span class="sxs-lookup"><span data-stu-id="5257a-155">If your target is a "modern" team site and you want to update the classification value, you should use the Microsoft Graph because the _Classification_ property of CSOM simply replicates the value of the _classification_ property of the Office 365 Group.</span></span>

> [!NOTE]
> <span data-ttu-id="5257a-156">Weitere finden Sie ausführliche Informationen zum Aktualisieren einer Office 365-Gruppe mithilfe der Microsoft Graph im Dokument [Gruppe aktualisieren](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_update).</span><span class="sxs-lookup"><span data-stu-id="5257a-156">You can find further details about how to update an Office 365 Group using the Microsoft Graph in the document [Update group](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_update).</span></span>

<span data-ttu-id="5257a-157">Um Sie so aktualisieren Sie die Klassifizierung einer Website, in der Plug & Play-Hauptbibliothek erleichtern ist eine Erweiterungsmethode, die für Sie das rechte-Verhalten, abhängig vom Websitetyp "modernen" angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="5257a-157">In order to make it easier for you to update the classification of a site, in the PnP Core Library there is an extension method that applies for you the right behavior, depending on the "modern" site type.</span></span> <span data-ttu-id="5257a-158">In der folgende Codeauszug sehen Sie, wie Sie es.</span><span class="sxs-lookup"><span data-stu-id="5257a-158">In the following code excerpt you can see how to use it.</span></span>

```C#
// Connect to the target site collectiion
using (var clientContext = new ClientContext("https://[tenant].sharepoint.com/sites/[modernsite]"))
{
    // Provide a valid set of credentials
    clientContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Get an Azure AD Access Token using ADAL, MSAL, or whatever else you like
    // This is needed only if your target is a "modern" team site
    var accessToken = getAzureADAccessToken();

    // Update the classification value, where the accessToken is an optional argument
    clientContext.Site.SetSiteClassification("MBI", accessToken);

    // Read back the new classification value (it can take a while to get back the new value)
    var currentClassification = clientContext.Site.GetSiteClassification();
}
```
