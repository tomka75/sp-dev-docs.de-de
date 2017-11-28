# <a name="granting-access-via-azure-ad-app-only"></a><span data-ttu-id="8464f-101">Gewähren des Zugriffs über App-Only Azure AD</span><span class="sxs-lookup"><span data-stu-id="8464f-101">Granting access via Azure AD App-Only</span></span>
<span data-ttu-id="8464f-102">Bei Verwendung von SharePoint Online können Sie Anwendungen in Azure AD definieren und diese Anwendungen können Berechtigungen für SharePoint, aber auch für alle anderen Dienste in Office 365 erteilt werden.</span><span class="sxs-lookup"><span data-stu-id="8464f-102">When using SharePoint Online you can define applications in Azure AD and these applications can be granted permissions to SharePoint, but also to all the other services in Office 365.</span></span> <span data-ttu-id="8464f-103">Dieses Modell ist das bevorzugte Modell für den Fall, dass Sie SharePoint Online nutzen, wenn Sie SharePoint nutzen Sie, verwenden Sie das Modell SharePoint nur über müssen lokale-basierend Azure ACS [hier](security-apponly-azureacs.md "Link zu Azure ACS app nur Artikel")beschrieben.</span><span class="sxs-lookup"><span data-stu-id="8464f-103">This model is the preferred model in case you’re using SharePoint Online, if you’re using SharePoint on-premises you have to use the SharePoint Only model via based Azure ACS as described in [here](security-apponly-azureacs.md "link to Azure ACS app only article").</span></span>

## <a name="setting-up-an-azure-ad-app-for-app-only-access"></a><span data-ttu-id="8464f-104">Einrichten einer Azure AD-Apps für nur-app-Zugriff</span><span class="sxs-lookup"><span data-stu-id="8464f-104">Setting up an Azure AD app for app-only access</span></span>
<span data-ttu-id="8464f-105">In Azure AD bei nur-app-sollten Sie in der Regel verwenden eines Zertifikats zum Zugriff anfordern: jedermann das Zertifikat und dessen privaten Schlüssel kann die app und die Berechtigungen für die app verwenden.</span><span class="sxs-lookup"><span data-stu-id="8464f-105">In Azure AD when doing app-only you typically use a certificate to request access: anyone having the certificate and its private key can use the app and the permissions granted to the app.</span></span> <span data-ttu-id="8464f-106">Unten beschriebenen Schritte führen Sie durch die Einrichtung von diesem Modell.</span><span class="sxs-lookup"><span data-stu-id="8464f-106">Below steps walk you through the setup of this model.</span></span>

<span data-ttu-id="8464f-107">Sie sind jetzt bereit, die Azure AD-Anwendung für den Aufruf von SharePoint Online mit einem Zugriffstoken App nur zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="8464f-107">You are now ready to configure the Azure AD Application for invoking SharePoint Online with an App Only access token.</span></span> <span data-ttu-id="8464f-108">Hierzu müssen Sie zum Erstellen und konfigurieren ein selbstsigniertes x. 509-Zertifikat, die verwendet wird, um Ihre Anwendung mit Azure AD, während das Zugriffstoken nur-App anfordern zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="8464f-108">To do that, you have to create and configure a self-signed X.509 certificate, which will be used to authenticate your Application against Azure AD, while requesting the App Only access token.</span></span> <span data-ttu-id="8464f-109">Zunächst müssen Sie das selbstsignierte x. 509-Zertifikat erstellen, die mit dem Tool makecert.exe steht im Windows SDK oder über ein bereitgestellten Powershellskript, das eine Abhängigkeit zu Makecert nicht vorhanden ist, die erstellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="8464f-109">First you must create the self-signed X.509 Certificate, which can be created using the makecert.exe tool that is available in the Windows SDK or through a provided PowerShell script which does not have a dependency to makecert.</span></span> <span data-ttu-id="8464f-110">Verwenden von PowerShell-Skript ist die bevorzugte Methode und wird in diesem Kapitel erläutert.</span><span class="sxs-lookup"><span data-stu-id="8464f-110">Using the PowerShell script is the preferred method and is explained in this chapter.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8464f-111">Es ist wichtig, dass die Ausführung der folgenden Skripts mit Administratorrechten.</span><span class="sxs-lookup"><span data-stu-id="8464f-111">It's important that you run the below scripts with Administrator privileges.</span></span>

<span data-ttu-id="8464f-112">So erstellen Sie eine selbst signierte Zertifikat mit diesem Skript:</span><span class="sxs-lookup"><span data-stu-id="8464f-112">To create a self signed certificate with this script:</span></span>

```powershell
.\Create-SelfSignedCertificate.ps1 -CommonName "MyCompanyName" -StartDate 2017-10-01 -EndDate 2019-10-01
```

> [!NOTE]
> <span data-ttu-id="8464f-113">Die Daten werden in US-Datumsformat bereitgestellt: JJJJ-MM-TT</span><span class="sxs-lookup"><span data-stu-id="8464f-113">The dates are provided in US date format: YYYY-MM-dd</span></span>

<span data-ttu-id="8464f-114">Von hier aus kann das eigentliche Skript kopiert werden:</span><span class="sxs-lookup"><span data-stu-id="8464f-114">The actual script can be copied from here:</span></span>

```powershell
<#
.SYNOPSIS
Creates a Self Signed Certificate for use in server to server authentication
.DESCRIPTION
.EXAMPLE
PS C:\> .\Create-SelfSignedCertificate.ps1 -CommonName "MyCert" -StartDate 2015-11-21 -EndDate 2017-11-21
This will create a new self signed certificate with the common name "CN=MyCert". During creation you will be asked to provide a password to protect the private key.
.EXAMPLE
PS C:\> .\Create-SelfSignedCertificate.ps1 -CommonName "MyCert" -StartDate 2015-11-21 -EndDate 2017-11-21 -Password (ConvertTo-SecureString -String "MyPassword" -AsPlainText -Force)
This will create a new self signed certificate with the common name "CN=MyCert". The password as specified in the Password parameter will be used to protect the private key
.EXAMPLE
PS C:\> .\Create-SelfSignedCertificate.ps1 -CommonName "MyCert" -StartDate 2015-11-21 -EndDate 2017-11-21 -Force
This will create a new self signed certificate with the common name "CN=MyCert". During creation you will be asked to provide a password to protect the private key. If there is already a certificate with the common name you specified, it will be removed first.
#>
Param(

   [Parameter(Mandatory=$true)]
   [string]$CommonName,

   [Parameter(Mandatory=$true)]
   [DateTime]$StartDate,
   
   [Parameter(Mandatory=$true)]
   [DateTime]$EndDate,

   [Parameter(Mandatory=$false, HelpMessage="Will overwrite existing certificates")]
   [Switch]$Force,

   [Parameter(Mandatory=$false)]
   [SecureString]$Password
)

# DO NOT MODIFY BELOW

function CreateSelfSignedCertificate(){
    
    #Remove and existing certificates with the same common name from personal and root stores
    #Need to be very wary of this as could break something
    if($CommonName.ToLower().StartsWith("cn="))
    {
        # Remove CN from common name
        $CommonName = $CommonName.Substring(3)
    }
    $certs = Get-ChildItem -Path Cert:\LocalMachine\my | Where-Object{$_.Subject -eq "CN=$CommonName"}
    if($certs -ne $null -and $certs.Length -gt 0)
    {
        if($Force)
        {
        
            foreach($c in $certs)
            {
                remove-item $c.PSPath
            }
        } else {
            Write-Host -ForegroundColor Red "One or more certificates with the same common name (CN=$CommonName) are already located in the local certificate store. Use -Force to remove them";
            return $false
        }
    }

    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"
    $name.Encode("CN=$CommonName", 0)

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
    $key.KeySpec = 1
    $key.Length = 2048 
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"
    $key.MachineContext = 1
    $key.ExportPolicy = 1 # This is required to allow the private key to be exported
    $key.Create()

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1") # Server Authentication
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"
    $ekuoids.add($serverauthoid)
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"
    $ekuext.InitializeEncode($ekuoids)

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"
    $cert.InitializeFromPrivateKey(2, $key, "")
    $cert.Subject = $name
    $cert.Issuer = $cert.Subject
    $cert.NotBefore = $StartDate
    $cert.NotAfter = $EndDate
    $cert.X509Extensions.Add($ekuext)
    $cert.Encode()

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"
    $enrollment.InitializeFromRequest($cert)
    $certdata = $enrollment.CreateRequest(0)
    $enrollment.InstallResponse(2, $certdata, 0, "")
    return $true
}

function ExportPFXFile()
{
    if($CommonName.ToLower().StartsWith("cn="))
    {
        # Remove CN from common name
        $CommonName = $CommonName.Substring(3)
    }
    if($Password -eq $null)
    {
        $Password = Read-Host -Prompt "Enter Password to protect private key" -AsSecureString
    }
    $cert = Get-ChildItem -Path Cert:\LocalMachine\my | where-object{$_.Subject -eq "CN=$CommonName"}
    
    Export-PfxCertificate -Cert $cert -Password $Password -FilePath "$($CommonName).pfx"
    Export-Certificate -Cert $cert -Type CERT -FilePath "$CommonName.cer"
}

function RemoveCertsFromStore()
{
    # Once the certificates have been been exported we can safely remove them from the store
    if($CommonName.ToLower().StartsWith("cn="))
    {
        # Remove CN from common name
        $CommonName = $CommonName.Substring(3)
    }
    $certs = Get-ChildItem -Path Cert:\LocalMachine\my | Where-Object{$_.Subject -eq "CN=$CommonName"}
    foreach($c in $certs)
    {
        remove-item $c.PSPath
    }
}

if(CreateSelfSignedCertificate)
{
    ExportPFXFile
    RemoveCertsFromStore
}
```

<span data-ttu-id="8464f-115">Werden Sie aufgefordert, ein Kennwort zum Verschlüsseln von Ihrem privaten Schlüssel, und beide Vorführen der. PFX-Datei und. CER-Datei wird im aktuellen Ordner exportiert werden.</span><span class="sxs-lookup"><span data-stu-id="8464f-115">You will be asked to give a password to encrypt your private key, and both the .PFX file and .CER file will be exported to the current folder.</span></span> 

<span data-ttu-id="8464f-116">Als Nächstes ist eine Azure AD-Anwendung im Mandanten Azure Active Directory registrieren, die mit Ihrem Office 365-Mandanten verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="8464f-116">Next step is registering an Azure AD application in the Azure Active Directory tenant that is linked to your Office 365 tenant.</span></span> <span data-ttu-id="8464f-117">Öffnen Sie dazu im Office 365 Admin Center (https://portal.office.com) mit dem Konto des ein Benutzer Mitglied der Mandant globale Admins.</span><span class="sxs-lookup"><span data-stu-id="8464f-117">To do that, open the Office 365 Admin Center (https://portal.office.com) using the account of a user member of the Tenant Global Admins group.</span></span> <span data-ttu-id="8464f-118">Klicken Sie auf den Link "Azure AD", der unter der Gruppe "Admin zentriert" in der Strukturansicht links im Office 365 Admin Center verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="8464f-118">Click on the "Azure AD" link that is available under the "Admin centers" group in the left-side treeview of the Office 365 Admin Center.</span></span> <span data-ttu-id="8464f-119">In den neuen Browser-Registerkarte, die geöffnet wird finden Sie die Microsoft Azure-Verwaltungsportal.</span><span class="sxs-lookup"><span data-stu-id="8464f-119">In the new browser's tab that will be opened you will find the Microsoft Azure Management Portal.</span></span> <span data-ttu-id="8464f-120">Wenn es zum ersten Mal, dass Sie dem Azure-Verwaltungsportal mit Ihrem Konto zugreifen wird, müssen Sie ein neues Azure-Abonnement registrieren einige Informationen und eine Kreditkarte für die Zahlung müssen bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="8464f-120">If it is the first time that you access the Azure Management Portal with your account, you will have to register a new Azure subscription, providing some information and a credit card for any payment need.</span></span> <span data-ttu-id="8464f-121">Aber keine Sorge, zur Wiedergabe mit Azure AD und zum Registrieren einer Office 365-Anwendung wird nicht bezahlen nichts.</span><span class="sxs-lookup"><span data-stu-id="8464f-121">But don't worry, in order to play with Azure AD and to register an Office 365 Application you will not pay anything.</span></span> <span data-ttu-id="8464f-122">Tatsächlich sind die kostenlose Funktionen.</span><span class="sxs-lookup"><span data-stu-id="8464f-122">In fact, those are free capabilities.</span></span> <span data-ttu-id="8464f-123">Einmal Zugang zu dem Azure-Verwaltungsportal, wählen Sie im Abschnitt "Active Directory", und wählen die Option "App Registrierungen".</span><span class="sxs-lookup"><span data-stu-id="8464f-123">Once having access to the Azure Management Portal, select the "Active Directory" section and choose the option "App Registrations".</span></span> <span data-ttu-id="8464f-124">Finden Sie in der nächsten Abbildung Weitere Details.</span><span class="sxs-lookup"><span data-stu-id="8464f-124">See the next figure for further details.</span></span>

![Zeigt Azure Ad-portal](media/apponly/azureadapponly1.png)

<span data-ttu-id="8464f-126">In der Registerkarte "App Registrierungen" finden Sie die Liste der Azure AD-Anwendungen in Ihrem Mandanten registriert.</span><span class="sxs-lookup"><span data-stu-id="8464f-126">In the "App Registrations" tab you will find the list of Azure AD applications registered in your tenant.</span></span> <span data-ttu-id="8464f-127">Klicken Sie auf "neue Anwendung Registrierung" in der oberen linken Teil der Blade.</span><span class="sxs-lookup"><span data-stu-id="8464f-127">Click the "New application registration" button in the upper left part of the blade.</span></span> <span data-ttu-id="8464f-128">Im nächsten Schritt geben Sie einen Namen für die Anwendung, wählen Sie die Option "Web app / API", und füllen Sie die "Sign-on URL" mit einer URL ein (muss nicht vorhanden, z. B. https://www.pnp.com).</span><span class="sxs-lookup"><span data-stu-id="8464f-128">Next, provide a name for your application, select the option "Web app / API", and fill in the "Sign-on URL" with a URL (does not have to exist, e.g. https://www.pnp.com).</span></span> <span data-ttu-id="8464f-129">Klicken Sie auf "Erstellen", um die Azure AD-Anwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8464f-129">Click on “Create” to create the Azure AD application.</span></span>

![erstellt eine neue Azure Ad-Anwendung](media/apponly/azureadapponly2.png)

<span data-ttu-id="8464f-131">Nach der Erstellung müssen Sie Ihre Azure AD-Anwendung erneut nachschlagen und öffnen Sie es:</span><span class="sxs-lookup"><span data-stu-id="8464f-131">Once created you need to look up your Azure AD application again and open it:</span></span>

![Öffnet neue Azure Ad-Anwendung aus portal](media/apponly/azureadapponly3.png)

> [!IMPORTANT]
> <span data-ttu-id="8464f-133">Nach dem Öffnen der Anwendung kopieren Sie die ID der Anwendung, wie Sie es später benötigen.</span><span class="sxs-lookup"><span data-stu-id="8464f-133">Once the application has been opened copy the application ID as you’ll need it later.</span></span>

<span data-ttu-id="8464f-134">Jetzt klicken Sie auf "Erforderliche Berechtigungen", und klicken Sie auf die Schaltfläche "Hinzufügen" ein neuer Blade wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8464f-134">Now click on "Required Permissions", and click on the "Add" button, a new blade will appear.</span></span> <span data-ttu-id="8464f-135">Sie müssen die folgenden Berechtigungen zu konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="8464f-135">You need to configure the following permissions:</span></span>
 - <span data-ttu-id="8464f-136">Office 365 für SharePoint Online (Anwendung die Berechtigung)</span><span class="sxs-lookup"><span data-stu-id="8464f-136">Office 365 SharePoint Online (Application Permission)</span></span>
     - <span data-ttu-id="8464f-137">Lesen und Schreiben von verwalteten Metadaten</span><span class="sxs-lookup"><span data-stu-id="8464f-137">Read and write managed metadata</span></span>
     - <span data-ttu-id="8464f-138">Vollzugriff auf alle Websitesammlung haben</span><span class="sxs-lookup"><span data-stu-id="8464f-138">Have full control of all site collection</span></span>

<span data-ttu-id="8464f-139">Die "Berechtigungen" gelten, auf die Anwendung erteilt werden, wenn als nur-App ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="8464f-139">The "Application Permissions" are those granted to the application when running as App Only.</span></span>

![Erteilen von Berechtigungen für Azure Ad-Anwendung](media/apponly/azureadapponly4.png)

<span data-ttu-id="8464f-141">Lediglich ist "" das Zertifikat erstellten wir zuvor Herstellen einer Verbindung mit der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="8464f-141">Final step is “connecting” the certificate we created earlier to the application.</span></span> <span data-ttu-id="8464f-142">Sie müssen Sie das Get-SelfSignedCertificateInformation.ps1 Skript ausführen.</span><span class="sxs-lookup"><span data-stu-id="8464f-142">You need to execute the Get-SelfSignedCertificateInformation.ps1 script.</span></span> 

```powershell
.\Get-SelfSignedCertificateInformation.ps1 | clip
```

<span data-ttu-id="8464f-143">Von hier aus kann das eigentliche Skript kopiert werden:</span><span class="sxs-lookup"><span data-stu-id="8464f-143">The actual script can be copied from here:</span></span>

```powershell
$certPath = Read-Host "Enter certificate path (.cer)"
$cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$cert.Import($certPath)
$rawCert = $cert.GetRawCertData()
$base64Cert = [System.Convert]::ToBase64String($rawCert)
$rawCertHash = $cert.GetCertHash()
$base64CertHash = [System.Convert]::ToBase64String($rawCertHash)
$KeyId = [System.Guid]::NewGuid().ToString()

$keyCredentials = 
'"keyCredentials": [
    {
      "customKeyIdentifier": "'+ $base64CertHash + '",
      "keyId": "' + $KeyId + '",
      "type": "AsymmetricX509Cert",
      "usage": "Verify",
      "value":  "' + $base64Cert + '"
     }
  ],'
$keyCredentials

Write-Host "Certificate Thumbprint:" $cert.Thumbprint
```

<span data-ttu-id="8464f-144">Sie müssen den vollständigen qualifizierten Pfad der angeben die. CER-Datei, die Sie erstellt haben, wenn Sie das Zertifikat für die Konfiguration der AppOnly Kontext erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="8464f-144">You will have to provide the full qualified path of the .CER file that you created when you created the certificate for the AppOnly context configuration.</span></span> <span data-ttu-id="8464f-145">Der Befehl kopiert in die Zwischenablage einen JSON-Ausschnitt, den Sie verwenden möchten in den kommenden Schritten.</span><span class="sxs-lookup"><span data-stu-id="8464f-145">The command will copy into the clipboard a JSON snippet that you will use in the upcoming steps.</span></span> <span data-ttu-id="8464f-146">Fügen Sie den Inhalt der Zwischenablage an einem sicheren Ort (wie eine frische neue Editor-Datei).</span><span class="sxs-lookup"><span data-stu-id="8464f-146">Paste the content of the clipboard in a safe place (like a fresh new notepad file).</span></span>

<span data-ttu-id="8464f-147">Wechseln Sie wieder zum Azure AD-Anwendung, die Sie im vorherigen Schritt erstellt haben, und klicken Sie auf die Schaltfläche "Manifest" am oberen Rand der Blade und dann auf Bearbeiten '.</span><span class="sxs-lookup"><span data-stu-id="8464f-147">Go back to the Azure AD Application that you created in the previous step and click the "Manifest" button at the top of the blade, then click Edit'.</span></span> <span data-ttu-id="8464f-148">Für die Eigenschaft **KeyCredentials** suchen und Ersetzen Sie ihn durch den Codeausschnitt, dem Sie vor dem generiert, wie werden:</span><span class="sxs-lookup"><span data-stu-id="8464f-148">Search for the **keyCredentials** property and replace it with the snippet you generated before, this will be like:</span></span>

```JSON
  "keyCredentials": [
    {
      "customKeyIdentifier": "<$base64CertHash>",
      "keyId": "<$KeyId>",
      "type": "AsymmetricX509Cert",
      "usage": "Verify",
      "value":  "<$base64Cert>"
     }
  ],
```

<span data-ttu-id="8464f-149">Wenn Sie diesen Schritt abgeschlossen haben, klicken Sie auf Speichern.</span><span class="sxs-lookup"><span data-stu-id="8464f-149">Click Save when you complete this step.</span></span>

<span data-ttu-id="8464f-150">In diesem Beispiel wird die Anwendung die Berechtigung Sites.FullControl.All Admin Zustimmung in einem Mandanten müssen, bevor sie verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="8464f-150">In this sample the Sites.FullControl.All application permission require admin consent in a tenant before it can be used.</span></span> <span data-ttu-id="8464f-151">Erstellen Sie eine Zustimmung URL wie folgt:</span><span class="sxs-lookup"><span data-stu-id="8464f-151">Create a consent URL like the following:</span></span>

```
https://login.microsoftonline.com/<tenant>/adminconsent?client_id=<application id>&state=<something>
```

<span data-ttu-id="8464f-152">Verwenden die Id der Anwendung von meiner app Azure AD und damit einverstanden, die app aus meinem contoso.onmicrosoft.com Mandanten, sieht die URL folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="8464f-152">Using the application id from my Azure AD app and consenting to the app from my tenant contoso.onmicrosoft.com, the URL looks like this:</span></span>

```
https://login.microsoftonline.com/contoso.onmicrosoft.com/adminconsent?client_id=6e4433ca-7011-4a11-85b6-1195b0114fea&state=12345
```

<span data-ttu-id="8464f-153">Durchsuchen, um das erstellte URL und melden Sie sich als Administrator und Zustimmung an die Anwendung.</span><span class="sxs-lookup"><span data-stu-id="8464f-153">Browsing to the created URL and log in as a tenant admin, and consent to the application.</span></span> <span data-ttu-id="8464f-154">Sie können den Zustimmung Bildschirm zeigen Sie den Namen der Anwendung als auch die von Ihnen konfigurierten berechtigungsbereiche sehen.</span><span class="sxs-lookup"><span data-stu-id="8464f-154">You can see the consent screen show the name of your application as well as the permission scopes you configured.</span></span>

![Erteilen von Berechtigungen für Azure Ad-Anwendung](media/apponly/azureadapponly5.png)

> [!NOTE]
> <span data-ttu-id="8464f-156">Nach dem Klicken auf "Accept" Sie an die Anmelde-URL umgeleitet sind angegebene früheren (https://www.pnp.com in unserem Fall)... und dieses Listenfeld, die URL die Umleitung schlägt fehl, aber die Grant erfolgreich durchgeführt wurde ungültig ist, in diesem Fall Nothing sorgen.</span><span class="sxs-lookup"><span data-stu-id="8464f-156">After clicking “Accept” you’re redirected to the sign-in URL you specified earlier (https://www.pnp.com in our case) …if that URL is not valid the redirect will fail but the grant was done successful, so nothing to worry about.</span></span>


## <a name="using-this-principal-in-your-application-using-the-sharepoint-pnp-sites-core-library"></a><span data-ttu-id="8464f-157">Verwenden diesen Prinzipal in der Anwendung, die mithilfe der Hauptbibliothek der SharePoint Plug & Play-Websites</span><span class="sxs-lookup"><span data-stu-id="8464f-157">Using this principal in your application using the SharePoint PnP Sites Core library</span></span>
<span data-ttu-id="8464f-158">Im ersten Schritt, die Sie hinzufügen SharePointPnPCoreOnline Bibliothek Nuget-Paket: https://www.nuget.org/packages/SharePointPnPCoreOnline.</span><span class="sxs-lookup"><span data-stu-id="8464f-158">In a first step, you add the SharePointPnPCoreOnline library nuget package: https://www.nuget.org/packages/SharePointPnPCoreOnline.</span></span> <span data-ttu-id="8464f-159">Danach können Sie unter Codekonstrukt verwenden:</span><span class="sxs-lookup"><span data-stu-id="8464f-159">Once that’s done you can use below code construct:</span></span>

```C#
using OfficeDevPnP.Core;
using System;

namespace AzureADCertAuth
{
    class Program
    {
        static void Main(string[] args)
        {
            string siteUrl = "https://contoso.sharepoint.com/sites/demo";
            using (var cc = new AuthenticationManager().GetAzureADAppOnlyAuthenticatedContext(siteUrl, "<application id>", "contoso.onmicrosoft.com", @"C:\BertOnlineAzureADAppOnly.pfx", "<password>"))
            {
                cc.Load(cc.Web, p => p.Title);
                cc.ExecuteQuery();
                Console.WriteLine(cc.Web.Title);
            };
        }
    }
}
```

## <a name="faq"></a><span data-ttu-id="8464f-160">Häufig gestellte Fragen</span><span class="sxs-lookup"><span data-stu-id="8464f-160">FAQ</span></span>
### <a name="can-i-use-other-means-besides-certificates-for-realizing-app-only-access-for-my-azure-ad-app"></a><span data-ttu-id="8464f-161">Kann ich anderweitig neben Zertifikate für nur-app-Zugriff für meine app Azure AD Realität verwenden?</span><span class="sxs-lookup"><span data-stu-id="8464f-161">Can I use other means besides certificates for realizing app-only access for my Azure AD app?</span></span>
<span data-ttu-id="8464f-162">Keine, alle anderen Optionen sind gesperrte und von SharePoint Online und führt zum Fehler Zugriff verweigert.</span><span class="sxs-lookup"><span data-stu-id="8464f-162">No, all other options are blocked and by SharePoint Online and will result in an Access Denied message.</span></span>

