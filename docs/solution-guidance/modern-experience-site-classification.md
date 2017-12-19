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
# <a name="sharepoint-modern-sites-classification"></a>SharePoint-Websites "modernen" Klassifizierung
Wenn Sie in SharePoint Online "modernen" Websites erstellen, können Sie optional 'Website Klassifikation' definieren die Vertraulichkeit Ihrer Daten Website auswählen. Das Ziel der Website Klassifizierung ist mit ermöglichen, Verwalten von Clustern von Websites basierend auf ihrer Klassifizierung Unternehmensleitung und Compliance im Hinblick auf sowie, basierte auf der Website Klassifizierung Governance-Prozessen zu automatisieren.

> [!IMPORTANT]
> Die Option 'Website-Klassifizierung' ist nicht standardmäßig aktiviert, und müssen Sie es auf der Ebene der Azure AD konfigurieren.

## <a name="enabling-site-classification-in-your-tenant"></a>Aktivieren in Ihrem Mandanten 'Website-Klassifizierung'

Um der 'Website Klassifikation' profitieren müssen Sie diese Funktion auf Ebene der Azure AD in Ihrem Ziel-Mandanten zu aktivieren. Nachdem Sie diese Funktion aktiviert haben, sehen Sie ein weiteres Feld "Wie Sensititive Ihre Daten ist?" Beim Erstellen neuer Websites "modernen". In der folgenden Abbildung sehen Sie, wie das Feld 'Website Klassifikation' aussieht.

![Die Option "Website-Klassifizierung" beim Erstellen einer "modernen" Website in SharePoint Online](media/modern-experiences/site-classification-ui.png)

Klicken Sie in der folgenden Abbildung sehen Sie die Klassifizierung nutzen, die in der Kopfzeile einer "modernen" Website.

![Die Klassifizierung"Website" hervorgehoben in der Kopfzeile einer "modernen" Website](media/modern-experiences/site-classification-ui-output.png)

### <a name="enabling-site-classification-with-powershell"></a>Aktivieren "Website-Klassifizierung' mit PowerShell
Führen Sie zum Aktivieren der Funktion "Website-Klassifizierung" eine Reihe von PowerShell-Code, wie unten dargestellt.

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
> Erwägen Sie, dass eine While (ungefähr 1 Stunde oder mehr) benötigt wird, um die Einstellungen in der Benutzeroberfläche von Office 365 verfügbar sind.

Über den Codeausschnitt befindlichen Anwendung lohnt zu sagen, dass die RTM-Version verwenden können ziemlich bald werden jedoch zum Zeitpunkt der Erstellung dieses Dokuments Sie die Vorabversion von AzureAD-Cmdlets verwenden müssen.
Nachdem Sie die Cmdlets AzureAD installiert haben, müssen Sie einfach mit dem Ziel Azure AD-Mandanten herzustellen, die Ihre Ziel-SharePoint Online-Mandanten sichern wird.
Mit dem Cmdlet _Get-AzureADDirectorySettingTemplate_ erhalten Sie einen Verweis auf die Vorlage"Einstellung" für die "Unified Gruppen', also einen mit _DisplayName_ der 'Group.Unified'.
Nachdem Sie die Vorlage verfügen, können Sie die Einstellungen dieser Vorlage durch Erstellen einer neuen _Verzeichnisberechtigungen_ und Bereitstellen der Einstellungswerte über ein Wörterbuch konfigurieren.

Die wichtigsten Einstellungen, aus der Sicht "Website Klassifizierung" lauten:
* **UsageGuidelinesUrl**: die URL einer Seite, auf dem Sie erklären können, was die unterschiedlichen Optionen sind. Ein Link zu dieser Seite werden im Formular Site Creation und in der Kopfzeile jeder geschützten Website angezeigt.
* **ClassificationList**: eine durch Trennzeichen getrennte Liste mit Werten für die Liste der 'Website-Klassifizierung' Optionen.
* **DefaultClassification**: der Standardwert für die Klassifizierung"Website".

### <a name="enabling-site-classification-with-pnp-core-library"></a>Aktivieren "Website-Klassifizierung' mit Plug & Play-Core-Bibliothek

Eine weitere Möglichkeit, die Sie zum Aktivieren der Funktion "Website-Klassifizierung" ist der Plug & Play-Hauptbibliothek einsetzen, mit dem einige Erweiterungsmethoden zum Verwalten von Klassifizierung in C#-Code enthält.
Beispielsweise können Sie C#-Code wie unten dargestellt, um die Klassifizierung' Website' aktivieren schreiben.

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

## <a name="updating-or-removing-site-classification-in-your-tenant"></a>Aktualisieren oder Entfernen von "Website-Klassifizierung" in Ihrem Mandanten

Wie für die Aktivierung der 'Website Klassifikation', aktualisieren oder entfernen die Einstellung erfolgen kann entweder mithilfe von PowerShell oder PnP Core-Bibliothek.

### <a name="updating-or-removing-site-classification-with-powershell"></a>Aktualisieren oder Entfernen von 'Site Klassifizierung' mit PowerShell

Wenn Sie anschließend die Einstellungen 'Website Klassifizierung' aktualisieren müssen, können Sie den folgenden PowerShell-Codeausschnitt.

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
> Erwägen Sie, dass eine While (ungefähr 1 Stunde oder mehr) benötigt wird, um die Einstellungen in der Benutzeroberfläche von Office 365 aktualisiert haben. Großes Problem sollte sie jedoch nicht, da Sie die Einstellungen für "Website-Klassifizierung" sehr häufig aktualisieren sollte nicht.

Wie Sie sehen können, müssen Sie lediglich die Directory-Einstellung mit dem Wert _DisplayName_ 'Group.Unified' Suchen und dann aktualisieren Sie die Einstellungswerte und übernehmen Sie die mit dem Cmdlet _Set-AzureADDirectorySetting_ .

Zum Entfernen der Klassifikation"Website" können Sie das Cmdlet _Remove-AzureADDirectorySetting_ wie im folgenden Codeausschnitt verwenden.

```ps
# Delete settings
$currentSettings = Get-AzureADDirectorySetting | where { $_.DisplayName -eq "Group.Unified" }
Remove-AzureADDirectorySetting -Id $currentSettings.Id
```

### <a name="updating-or-removing-site-classification-with-pnp-core-library"></a>Aktualisieren oder Entfernen von 'Site Klassifizierung' mit Plug & Play-Core-Bibliothek

Eine weitere Option, die Ihnen ist die Plug & Play-Kern-Bibliothek verwenden.
Beispielsweise können Sie zum Aktualisieren der Klassifikation"Website" C#-Code wie unten dargestellt schreiben.

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

Darüber hinaus können Sie zum Deaktivieren und entfernen die Einstellungen 'Website Klassifizierung', wie im folgenden Codeausschnitt verwenden.

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

## <a name="managing-the-classification-of-a-site"></a>Verwalten von der Klassifikation einer Website

Der Wert der Klassifizierung für eine Website gelesen werden kann, oder aktualisiert, später mithilfe der Benutzeroberfläche von SharePoint Online, wie Sie sehen in der folgenden Abbildung, durch die Einstellungen 'Standortinformationen' bearbeiten.

![Die Option 'Website-Klassifizierung' während der Bearbeitung der Einstellungen 'Standortinformationen' einer "modernen" Website in SharePoint Online](media/modern-experiences/site-classification-update-ui.png)

### <a name="programmatically-reading-the-classification-of-a-site"></a>Programmgesteuertes Lesen der Klassifikation einer Website

Aus der Perspektive eines Entwicklers können Sie CSOM und der REST-API von SharePoint Online zum Lesen und schreiben den Wert der Klassifikation für einen bestimmten Standort. Tatsächlich hat jeder SharePoint Online-Websitesammlung die _Klassifizierung_ -Eigenschaft, die Sie verwenden können, lesen Sie die Website-Klassifizierung. 

Hier sehen Sie einen PowerShell Ausschnitt dafür.

```ps
# Delete settings
Connect-PnPOnline "https://[tenant].sharepoint.com/sites/[modernsite]" -Credentials [credentials]

$site = Get-PnPSite
$classificationValue = Get-PnPProperty -ClientObject $site -Property Classification
Write-Host $classificationValue
```

Wenn Sie den Wert für "Website-Klassifizierung" mit REST lesen möchten, können beispielsweise in einem SharePoint-Framework-Client-Side-Webpart den folgenden REST-Endpunkt verwenden:

```TEXT
https://[tenant].sharepoint.com/sites/[modernsite]/_api/site/Classification
```

Basierend auf der Klassifizierungswert einer Website, können Sie die Automatisierung und benutzerdefinierten Richtlinien definieren.

In der Hauptbibliothek Plug & Play-ist es eine Erweiterungsmethode für die Website der CSOM, dem Sie auf einfache Weise den Klassifizierungswert einer Website gelesen werden kann. Im folgenden Codeausschnitt sehen Sie, wie Sie diese Erweiterungsmethode verwenden können.

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

### <a name="programmatically-updating-the-classification-of-a-site"></a>Programmgesteuerte Aktualisierung der Klassifikation einer Website

Wenn Ihr Ziel einer Website "modernen" Kommunikation ist, können Sie die _Klassifizierung_ -Eigenschaft des CSOM verwenden, um den Wert zu aktualisieren.

Ihr Ziel einer Teamwebsite "modernen" und den Klassifizierungswert aktualisieren möchten, sollten Sie das Microsoft Graph verwenden, da die _Klassifizierung_ -Eigenschaft des CSOM einfach den Wert der Eigenschaft _Klassifizierung_ der Office 365 repliziert Mitglied der Gruppe.

> [!NOTE]
> Weitere finden Sie ausführliche Informationen zum Aktualisieren einer Office 365-Gruppe mithilfe der Microsoft Graph im Dokument [Gruppe aktualisieren](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_update).

Um Sie so aktualisieren Sie die Klassifizierung einer Website, in der Plug & Play-Hauptbibliothek erleichtern ist eine Erweiterungsmethode, die für Sie das rechte-Verhalten, abhängig vom Websitetyp "modernen" angewendet wird. In der folgende Codeauszug sehen Sie, wie Sie es.

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
