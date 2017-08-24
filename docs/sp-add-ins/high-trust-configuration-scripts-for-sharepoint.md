
# <a name="high-trust-configuration-scripts-for-sharepoint"></a><span data-ttu-id="9be95-101">Konfigurationsskripts mit hoher Vertrauenswürdigkeit für SharePoint</span><span class="sxs-lookup"><span data-stu-id="9be95-101">High-trust configuration scripts for SharePoint</span></span>
<span data-ttu-id="9be95-102">Anpassbare Windows PowerShell-Skripts, die eine Microsoft SharePoint-Farm so konfigurieren, dass sie ein besonders vertrauenswürdiges SharePoint-Add-In verwendet.</span><span class="sxs-lookup"><span data-stu-id="9be95-102">Get customizable Windows PowerShell scripts that configure a Microsoft SharePoint farm to use a high-trust SharePoint Add-in.</span></span>
 

 <span data-ttu-id="9be95-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="9be95-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="how-to-use-the-scripts"></a><span data-ttu-id="9be95-106">Informationen zur Verwendung der Skripts</span><span class="sxs-lookup"><span data-stu-id="9be95-106">How to use the scripts</span></span>
<span data-ttu-id="9be95-107"><a name="Usage"> </a></span><span class="sxs-lookup"><span data-stu-id="9be95-107"></span></span>

<span data-ttu-id="9be95-p102">Die unten aufgeführten Skripts werden verwendet, um ein oder mehrere digitale X.509-Zertifikate als Aussteller von Zugriffstoken in einer Staging- oder ProduktionsMicrosoft SharePoint-Farm zu definieren. (Ein geeigneteres Skript für eine SharePoint-Add-Ins-Entwicklungsumgebung finden Sie unter  [Erstellen besonders vertrauenswürdiger Add-Ins für SharePoint](create-high-trust-sharepoint-add-ins).) Es gibt keine einzelne Skriptgruppe, die für jede SharePoint-Farm funktioniert, da es zu viele Optionen gibt, wie das Zertifikat bezogen und gespeichert wird. Beachten Sie deshalb Folgendes:</span><span class="sxs-lookup"><span data-stu-id="9be95-p102">The scripts below are used to designate one or more X.509 digital certificates as trusted issuers of access tokens in a staging or production Microsoft SharePoint farm. (For a script that is more appropriate for an SharePoint Add-ins development environment, see  [Create high-trust SharePoint Add-ins](create-high-trust-sharepoint-add-ins).) No single set of scripts can work for every SharePoint farm because there are too many different ways that the certificates can be acquired and stored. For that reason, please note the following:</span></span>
 

 

- <span data-ttu-id="9be95-111">Die Skripts sind zum Ausführen in der SharePoint-Verwaltungsshell auf einem SharePoint-Server in der Farm vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="9be95-111">The scripts are meant to be run in SharePoint Management Shell on any SharePoint server in the farm.</span></span>
    
 
- <span data-ttu-id="9be95-112">Diese Skripts sollten als Entwürfe betrachtet werden, die ggf. angepasst werden müssen.</span><span class="sxs-lookup"><span data-stu-id="9be95-112">These scripts should be thought of as drafts that may need to be customized.</span></span>
    
 
- <span data-ttu-id="9be95-p103">Sie werden als Teil des gesamten Veröffentlichungsvorgangs einer besonders vertrauenswürdigen SharePoint-Add-In verwendet. Sie sollten nur von jemandem verwendet werden, der mit den Themen  [Erstellen von Add-Ins für SharePoint, die eine Autorisierung mit hoher Vertrauenswürdigkeit verwenden](creating-sharepoint-add-ins-that-use-high-trust-authorization) und [Packen und Veröffentlichen besonders vertrauenswürdiger Add-Ins für SharePoint](package-and-publish-high-trust-sharepoint-add-ins) und den darin aufgeführten Voraussetzungen vertraut ist.</span><span class="sxs-lookup"><span data-stu-id="9be95-p103">They are used as part of the overall process of publishing a high-trust SharePoint Add-in. They should only be used by someone familiar with the topics  [Creating SharePoint Add-ins that use high-trust authorization](creating-sharepoint-add-ins-that-use-high-trust-authorization) and [Package and publish high-trust SharePoint Add-ins](package-and-publish-high-trust-sharepoint-add-ins) and the prerequisites listed in them.</span></span>
    
 
- <span data-ttu-id="9be95-115">Sie sollten außerdem von jemandem geprüft und angepasst werden, der mit den Kundenzertifikatsrichtlinien des Add-Ins vertraut ist.</span><span class="sxs-lookup"><span data-stu-id="9be95-115">They should also be reviewed and customized as needed by someone familiar with the add-in customer's certificate policies.</span></span>
    
 
- <span data-ttu-id="9be95-116">Bei den zwei Hauptskripts unten, **HighTrustConfig-ForSharedCertificate.ps1** und **HighTrustConfig-ForSingleApp.ps1**, wird davon ausgegangen, dass der Administrator ein Zertifikat für die Remote-Webanwendungskomponente des Add-Ins oder der Add-Ins abgerufen hat und eine CER-Version des Zertifikats (das nicht den privaten Schlüssel enthält) in einem Ordner gespeichert hat, zu dem die Benutzerkonten für folgende IIS-Anwendungspools auf den SharePoint-Servern Lesezugriff besitzen:</span><span class="sxs-lookup"><span data-stu-id="9be95-116">The two major scripts below, **HighTrustConfig-ForSharedCertificate.ps1** and **HighTrustConfig-ForSingleApp.ps1**, assume that an administrator has acquired a certificate for the remote web application component of the add-in or add-ins and that the administrator has temporarily stored a .cer version of the certificate (that does not contain the private key) in a folder to which the user accounts for the following IIS application pools on the SharePoint servers have Read access:</span></span>
    
      -  <span data-ttu-id="9be95-117">**SecurityTokenServiceApplicationPool**</span><span class="sxs-lookup"><span data-stu-id="9be95-117">**SecurityTokenServiceApplicationPool**</span></span>
    
 
  - <span data-ttu-id="9be95-p104">Der Add-In-Pool, der die IIS-Website bedient, die die übergeordnete SharePoint-Webanwendung für Ihre SharePoint-Testwebsite hostet. Für die IIS-Website **SharePoint - 80** wird der Pool als **OServerPortalAppPool** bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="9be95-p104">The add-in pool that serves the IIS web site that hosts the parent SharePoint web application for your test SharePoint website. For the **SharePoint - 80** IIS website, the pool is called **OServerPortalAppPool**.</span></span>
    
 

    <span data-ttu-id="9be95-p105">Um das Benutzerkonto zu finden, das ein Anwendungspool verwendet, öffnen Sie den IIS-Manager auf einem SharePoint-Server, und doppelklicken Sie im Bereich **Verbindungen** auf **Anwendungspools**. Die Spalte **Identität** in der Liste **Anwendungspools** zeigt die Benutzer für die Anwendungspools an.</span><span class="sxs-lookup"><span data-stu-id="9be95-p105">To find the user account that an application pool is using, open IIS Manager on a SharePoint server and double-click **Application Pools** in the **Connections** pane. The **Identity** column in the **Application Pools** list that opens shows the users for the application pools.</span></span>
    
 
- <span data-ttu-id="9be95-p106">In den Anweisungen zu den zwei Hauptskripts wird außerdem davon ausgegangen, dass die Zertifikate im IIS auf den Servern installiert sind, die die Remoteanwendungen hosten. Die Anweisungen finden Sie unter  [Konfigurieren des Remotewebservers mit dem Zertifikat](package-and-publish-high-trust-sharepoint-add-ins#ConfigureRemote).</span><span class="sxs-lookup"><span data-stu-id="9be95-p106">The instructions for the two major scripts also assume that the certificate(s) have been installed to IIS on server(s) that host the remote web application(s). For instructions, see  [Configure the remote web server with the certificate](package-and-publish-high-trust-sharepoint-add-ins#ConfigureRemote).</span></span>
    
 
<span data-ttu-id="9be95-124">Verwendungshinweise zu den Skripts finden Sie in den weiter unten aufgeführten Abschnitten.</span><span class="sxs-lookup"><span data-stu-id="9be95-124">See specific usage notes for each script in the sections below.</span></span>
 

 

## <a name="addsprootauthorityps1"></a><span data-ttu-id="9be95-125">AddSPRootAuthority.ps1</span><span class="sxs-lookup"><span data-stu-id="9be95-125">AddSPRootAuthority.ps1</span></span>
<span data-ttu-id="9be95-126"><a name="RootScript"> </a></span><span class="sxs-lookup"><span data-stu-id="9be95-126"></span></span>

<span data-ttu-id="9be95-p107">Das Zertifikat der Remotewebanwendungskomponente der besonders vertrauenswürdigen SharePoint-Add-In wird von einer kommerziellen Zertifizierungsstelle oder einer Zertifizierungsstelle der Domäne abgerufen. In beiden Fällen ist das Zertifikat das niedrigste Bindeglied einer Kette von Zertifikaten, dabei vertraut jedes dem darüberliegenden Zertifikat, da aus einer Stamm-Zertifizierungsstelle (kommerziell oder der Domäne) stammt. SharePoint verlangt, dass  *alle*  Zertifikate in der Kette zur SharePoint-Liste der vertrauenswürdigen Stamm-Zertifizierungsstellen hinzugefügt werden. Das unten aufgeführte Skript kann verwendet werden, um jedes der Zertifikate in der Kette *abgesehen vom niedrigsten*  zur Liste hinzuzufügen. Das niedrigste Zertifikat in der Kette, das direkt an die Remotewebanwendung gebunden ist, wird zu den Stamm-Zertifizierungsstellen in einem der Hauptskripts hinzugefügt, die in Abschnitten weiter unten beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="9be95-p107">The certificate of the remote web application component of the high-trust SharePoint Add-in is obtained from either a commercial Certificate Authority (CA) or a domain CA. In either case, the certificate is the lowest link in a chain of certificates, each trusting the one above it, which originates with a root CA (commercial or domain). SharePoint requires that  *all*  the certificates in the chain be added to SharePoint's list of trusted root authorities. The script below can be used to add each certificate in the chain *except the lowest one*  to the list. The lowest certificate in the chain, the certificate that is directly bound to the remote web application, is added to the root authorities in one of the major scripts described in later sections.</span></span>
 

 
<span data-ttu-id="9be95-132">Für das Skript sind folgende Parameter verfügbar:</span><span class="sxs-lookup"><span data-stu-id="9be95-132">The parameters for the script are the following:</span></span>
 

 


|<span data-ttu-id="9be95-133">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="9be95-133">**Parameter**</span></span>|<span data-ttu-id="9be95-134">**Wert**</span><span class="sxs-lookup"><span data-stu-id="9be95-134">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9be95-135">-CertPath</span><span class="sxs-lookup"><span data-stu-id="9be95-135">-CertPath (required)</span></span>|<span data-ttu-id="9be95-136">Der vollständige Pfad und der Dateiname des Zertifikats (die CER-Datei).</span><span class="sxs-lookup"><span data-stu-id="9be95-136">The full path and filename of the certificate (the .cer file).</span></span>|
|<span data-ttu-id="9be95-137">-CertName</span><span class="sxs-lookup"><span data-stu-id="9be95-137">-CertName (required)</span></span>|<span data-ttu-id="9be95-p108">Der Name des Zertifikats. Um den Namen zu finden, müssen Sie die Eigenschaften des Zertifikats anzeigen.</span><span class="sxs-lookup"><span data-stu-id="9be95-p108">The name of the certificate. To find the name, view the properties of the certificate.</span></span>|
<span data-ttu-id="9be95-p109">In dem gängigen Szenario, in dem das Zertifikat der Webanwendung von einem Zertifizierungsstellenserver auf mittlerer Ebene (auch als „Enterprise" bezeichnet) ausgestellt wird und das Zertifikat beispielsweise wiederum von einem Stammzertifizierungsserver (auch als „eigenständig" bezeichnet) ausgestellt wird, sollte das Skript je einmal für die Zertifikate und die beiden Zertifizierungsstellenserver ausgeführt werden. Dies wird im folgenden Absatz verdeutlicht:</span><span class="sxs-lookup"><span data-stu-id="9be95-p109">For example, in the common scenario where the web application's certificate is issued by an intermediate (also called 'enterprise') CA server and its certificate, in turn, is issued by a root (also called 'standalone') CA server, the script should be run once for each of the certificates of the two CA servers. The following shows this:</span></span>
 

 



```
./AddSPRootAuthority.ps1 -CertPath "\\CertStorage\RootCA.cer" -CertName "Contoso Root CA"

./AddSPRootAuthority.ps1 -CertPath "C:\RegionalCerts\NorthRegion.cer" -CertName "North Region Intermediate CA"

```

<span data-ttu-id="9be95-142">Wenn alle Zertifikate der besonders vertrauenswürdigen SharePoint-Add-Ins des Kunden aus der gleichen Zertifikatskette stammen, wie es in der Regel der Fall wäre, wird dieses Skript nicht erneut verwendet.</span><span class="sxs-lookup"><span data-stu-id="9be95-142">If all of certificates of the customer's high-trust SharePoint Add-ins come from the same chain of certificates, as would typically be the case, then this script is never used again.</span></span>
 

 
<span data-ttu-id="9be95-p110">Im Folgenden ist der Code für dieses Skript aufgeführt. Fügen Sie ihn einfach in einen Text-Editor oder den PowerShell-Editor (IPowerShell ISE) ein, und speichern Sie ihn als „AddSPRootAuthority.ps1".</span><span class="sxs-lookup"><span data-stu-id="9be95-p110">The following is the code for the script. Simply paste it into any text editor or the PowerShell editor (IPowerShell ISE) and save it as AddSPRootAuthority.ps1.</span></span>
 

 

 <span data-ttu-id="9be95-p111">**Hinweis** Die Datei muss im ANSI-Format, nicht im UTF-8-Format, gespeichert werden. PowerShell gibt möglicherweise Syntaxfehler aus, wenn eine Datei in einem anderen Format als ANSI ausgeführt wird. Der Editor und der PowerShell-Editor speichern die Datei standardmäßig im ANSI-Format. Wenn Sie zum Speichern der Datei einen anderen Editor verwenden, achten Sie darauf, die Datei im ANSI-Format zu speichern.</span><span class="sxs-lookup"><span data-stu-id="9be95-p111">**Note** The file has to be saved as ANSI format, not UTF-8. PowerShell may give syntax errors when it runs a file with a non-ANSI format. NotePad and the PowerShell editor will default to saving it as ANSI. If you use any other editor to save the file, be sure you are saving it as ANSI.</span></span>
 




```
param(
    [Parameter(Mandatory)][String] $CertName = $(throw "Usage: AddSPRootAuthority.ps1 -CertPath <full path to .cer file> -CertName <name of certificate>"),
    [Parameter(Mandatory)][String] $CertPath
)
# Stop if there's an error
$ErrorActionPreference = "Stop"

# Make the certificate a trusted root authority in SharePoint
$cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($CertPath)
New-SPTrustedRootAuthority -Name $CertName -Certificate $cert

```


## <a name="hightrustconfig-forsharedcertificateps1"></a><span data-ttu-id="9be95-149">HighTrustConfig-ForSharedCertificate.ps1</span><span class="sxs-lookup"><span data-stu-id="9be95-149">HighTrustConfig-ForSharedCertificate.ps1</span></span>
<span data-ttu-id="9be95-150"><a name="MultipleAppScript"> </a></span><span class="sxs-lookup"><span data-stu-id="9be95-150"></span></span>

<span data-ttu-id="9be95-p112">Die primären Aufgabe dieses Skript ist das Registrieren des freigegebenen Zertifikats der Remotewebanwendungskomponenten in mehreren besonders vertrauenswürdigen SharePoint-Add-Ins mit SharePoint als Stammzertifizierungsstelle und vertrauenswürdiger Aussteller eines Zugriffstoken. Dieses Skript wird nicht verwendet, wenn der Kunde separate Zertifikate für jede besonders vertrauenswürdige SharePoint-Add-In verwendet. Weitere Informationen zu diesem Szenario finden Sie unter  [HighTrustConfig-ForSingleApp.ps1](#SingleAppScript) weiter unten. Wenn alle Add-Ins das gleiche Zertifikat verwenden, wird dieses Skript nur einmal ausgeführt. Wenn einige Add-In-Gruppen ein anderes Zertifikat aus anderen Gruppen verwenden, wird diese Skript einmal für jede Gruppe ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="9be95-p112">The primary tasks of this script are to register the shared certificate of the remote web application components in multiple high-trust SharePoint Add-ins with SharePoint as both a root authority and as a trusted access token issuer. This script is not used if the customer is using separate certificates with each high-trust SharePoint Add-in. For that scenario, see  [HighTrustConfig-ForSingleApp.ps1](#SingleAppScript) below. If all of the add-ins use the same certificate, then this script is run only once. If some sets of add-ins use a different certificate from other sets, then this script is run once for each set.</span></span>
 

 
<span data-ttu-id="9be95-p113">In der folgenden Tabelle werden die Parameter und Schalter für das Skript erläutert. Durch Anpassungen des Skripts sind möglicherweise Änderungen an dieser Tabelle erforderlich.</span><span class="sxs-lookup"><span data-stu-id="9be95-p113">The following table describes the parameters and switches for the script. Customization of the script may require changes to this table.</span></span>
 

 


|<span data-ttu-id="9be95-158">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="9be95-158">**Parameter**</span></span>|<span data-ttu-id="9be95-159">**Wert**</span><span class="sxs-lookup"><span data-stu-id="9be95-159">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9be95-160">-CertPath (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="9be95-160">-CertPath (required)</span></span>|<span data-ttu-id="9be95-161">Der vollständige Pfad zur freigegebenen CER-Datei.</span><span class="sxs-lookup"><span data-stu-id="9be95-161">The full path to the shared *.cer file.</span></span>|
|<span data-ttu-id="9be95-162">-CertName (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="9be95-162">-CertName (required)</span></span>|<span data-ttu-id="9be95-p114">Der Name des freigegebenen Zertifikats. Um den Namen zu finden, müssen Sie IIS auf dem Remotewebserver öffnen, der die Remotewebanwendung hostet. Markieren Sie den Knoten  _Servername_ und klicken Sie doppelt auf **Zertifikate**. Das Zertifikat wird mit dem Namen aufgelistet.  </span><span class="sxs-lookup"><span data-stu-id="9be95-p114">The name of the shared certificate. To find the name, open IIS on the remote web server that hosts the remote web application. Highlight the  _server name_ node and double-click **Certificates**. The certificate will be listed by its name.</span></span>|
|<span data-ttu-id="9be95-167">-TokenIssuerFriendlyName (optional)</span><span class="sxs-lookup"><span data-stu-id="9be95-167">-TokenIssuerFriendlyName (optional)</span></span>|<span data-ttu-id="9be95-p115">Ein eindeutiger Anzeigename für den Tokenaussteller mit bis zu 50 Zeichen. Dies kann beim Debuggen von Problemen mit Tokenausstellern hilfreich sein. Der Name muss eindeutig sein. Dies könnte mit einer GUID sichergestellt werden, aber eine GUID belegt 32 der 50 Zeichen. Sie können die Konvertierung einer GUID in eine Base-64-Zeichenfolge in Betracht ziehen, die auf 22 Zeichen reduziert werden kann. Wenn dieser Parameter nicht verwendet wird, verwendet das Skript den Namen „Besonders vertrauenswürdige Add-Ins _<base64 version of issuer GUID>_“.</span><span class="sxs-lookup"><span data-stu-id="9be95-p115">A unique friendly name for the token issuer, up to 50 characters. This can be helpful if you are debugging issues with token issuers. The name must be unique. Including a GUID would ensure that it is, but a GUID uses up 32 of the 50 characters, consider converting a GUID to a Base 64 string which can be reduced to 22 characters. If this parameter is not used, the script uses the name "High-Trust Add-ins   base64 version of issuer GUID ".</span></span>|
<span data-ttu-id="9be95-173">Im Folgenden finden Sie ein Beispiel zum Ausführen dieses Skripts.</span><span class="sxs-lookup"><span data-stu-id="9be95-173">The following is an example of running this script.</span></span>
 

 
 `./HighTrustConfig-ForSharedCertificate.ps1 -CertPath "C:\Certs\MyCert.cer" -CertName "My Cert" -TokenIssuerFriendlyName "SharePoint High-Trust Add-ins Token Issuer"`
 

 

 <span data-ttu-id="9be95-p116">**Wichtig** Die Registrierung des Zertifikats als Tokenaussteller wird nicht sofort wirksam. Es kann bis zu 24 Stunden dauern, bis alle SharePoint-Server den neuen Tokenaussteller erkannt haben. Durch Ausführen von „iisreset“ auf allen SharePoint-Servern wird der Aussteller sofort erkannt, wenn dies möglich ist, ohne die SharePoint-Benutzer zu stören.</span><span class="sxs-lookup"><span data-stu-id="9be95-p116">**Important** The registration of the certificate as a token issuer is not effective immediately. It may take as long as 24 hours before all the SharePoint servers recognize the new token issuer. Running an iisreset on all the SharePoint servers would cause them to immediately recognize the issuer, if you can do that without disturbing SharePoint users.</span></span>
 

<span data-ttu-id="9be95-p117">Beginnen Sie eine neue Datei in einem Text-Editor oder dem PowerShell-Editor und kopieren Sie das Folgende in eine Textdatei und speichern Sie sie als HighTrustConfig-ForSharedCertificate.ps1. Verwenden Sie dazu das ANSI-Format, nicht UTF-8.</span><span class="sxs-lookup"><span data-stu-id="9be95-p117">Start a new file in a text editor, or the PowerShell editor, and copy the following into a text file and save it as HighTrustConfig-ForSharedCertificate.ps1. Use ANSI format, not UTF-8.</span></span>
 

 



```
param(
    [Parameter(Mandatory)][String] $CertPath = $(throw "Usage: HighTrustConfig-ForSharedCertificate.ps1 -CertPath <full path to .cer file> -CertName <name of certificate> [-TokenIssuerFriendlyName <friendly name>]"),
    [Parameter(Mandatory)][String] $CertName,
    [Parameter()][String] $TokenIssuerFriendlyName
) 
# Stop if there's an error
$ErrorActionPreference = "Stop"

# Ensure friendly name is short enough
if ($TokenIssuerFriendlyName.Length -gt 50)
{
    throw "-TokenIssuerFriendlyName must be unique name of no more than 50 characters."
} 

# Get the certificate
$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($CertPath)

# Make the certificate a trusted root authority in SharePoint
New-SPTrustedRootAuthority -Name $CertName -Certificate $certificate 

# Get the GUID of the authentication realm
$realm = Get-SPAuthenticationRealm

# Generate a unique specific issuer ID
$specificIssuerId = [System.Guid]::NewGuid().ToString()

# Create full issuer ID in the required format
$fullIssuerIdentifier = $specificIssuerId + '@' + $realm 

# Create issuer name
if ($TokenIssuerFriendlyName.Length -ne 0)
{
    $tokenIssuerName = $TokenIssuerFriendlyName
}
else
{
    $tokenIssuerName = "High-Trust Add-ins " + [System.Convert]::ToBase64String($specificIssuerId.ToByteArray()).TrimEnd('=') 
}

# Register the token issuer
New-SPTrustedSecurityTokenIssuer -Name $tokenIssuerName -Certificate $certificate -RegisteredIssuerName $fullIssuerIdentifier -IsTrustBroker

# Output the specific issuer ID to a file in the same folder as this script. The file should be given to the developer of the high-trust SharePoint Add-in.
$specificIssuerId | select * | Out-File -FilePath "SecureTokenIssuerID.txt"
```


 <span data-ttu-id="9be95-p118">**Tipp** Wenn das Skript einen Fehler ausgibt, nachdem die `New-SPTrustedRootAuthority`-Zeile erfolgreich ausgeführt wurde, kann das Skript nicht erneut ausgeführt werden, bis das Objekt entfernt wurde. Verwenden Sie das folgende Cmdlet an der Stelle, an der der Wert des `-Identity`-Parameters dem des verwendeten `-CertName`-Parameters im Skript entspricht. `Remove-SPTrustedRootAuthority -Identity <certificate name>`Wenn der Tokenaussteller entfernt werden muss, verwenden Sie folgendes Cmdlet: `Remove-SPTrustedSecurityTokenIssuer -Identity <issuer name>`Wenn der `-TokenIssuerFriendlyName`-Parameter verwendet wurde, verwenden Sie für `-Identity` denselben Wert. Wenn der `-TokenIssuerFriendlyName`-Parameter nicht verwendet wurde, ist eine zufällige GUID Teil des Ausstellernamens. Zum Abrufen des für `-Identity` erforderlichen Werts führen Sie das folgende Cmdlet aus. Öffnen Sie dann die erzeugte TokenIssuers.txt-Datei, und suchen Sie den Aussteller mit dem Namen „Besonders vertrauenswürdige Add-Ins _<base64 version of issuer GUID>_“. Verwenden Sie diesen vollständigen Namen für `-Identity`. `Get-SPTrustedSecurityTokenIssuer | Out-File -FilePath "TokenIssuers.txt"`</span><span class="sxs-lookup"><span data-stu-id="9be95-p118">**Tip**  If the script throws an error after the  `New-SPTrustedRootAuthority` line has run successfully, the script cannot be rerun until that object has been removed. Use the following cmdlet, where the value of the `-Identity` parameter is the same as was used for the `-CertName` parameter in the script. `Remove-SPTrustedRootAuthority -Identity <certificate name>`If the token issuer needs to be removed for any reason, use the following cmdlet: `Remove-SPTrustedSecurityTokenIssuer -Identity <issuer name>`If the  `-TokenIssuerFriendlyName` parameter was used, then use the same value for `-Identity`. If the  `-TokenIssuerFriendlyName` parameter was not used, then a random GUID is part of the issuer name. To obtain value needed for `-Identity`, run the following cmdlet. Then open the TokenIssuers.txt file that is produced and find the issuer whose name is "High-Trust Add-ins  _<base64 version of issuer GUID>_". Use that entire name for  `-Identity`.  `Get-SPTrustedSecurityTokenIssuer | Out-File -FilePath "TokenIssuers.txt"`</span></span>
 


## <a name="hightrustconfig-forsingleappps1"></a><span data-ttu-id="9be95-186">HighTrustConfig-ForSingleApp.ps1</span><span class="sxs-lookup"><span data-stu-id="9be95-186">HighTrustConfig-ForSingleApp.ps1</span></span>
<span data-ttu-id="9be95-187"><a name="SingleAppScript"> </a></span><span class="sxs-lookup"><span data-stu-id="9be95-187"></span></span>

<span data-ttu-id="9be95-p119">Die primäre Aufgabe dieses Skripts ist das Registrieren des Zertifikats der Remotewebanwendung in einer besonders vertrauenswürdigen SharePoint-Add-In mit SharePoint als Stammautorisierungsstelle und vertrauenswürdigen Zugriffstokenaussteller. Dieses Skript wird nicht verwendet, wenn der Kunde für mehrere SharePoint-Add-Ins ein einzelnes Zertifikat verwendet. Weitere Informationen zu diesem Szenario finden Sie unter  [HighTrustConfig-ForSharedCertificate.ps1](#MultipleAppScript) weiter oben. Dieses Skript wird für jede besonders vertrauenswürdige SharePoint-Add-In ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="9be95-p119">The primary tasks of this script are to register the certificate of the remote web application in a high-trust SharePoint Add-in with SharePoint as both a root authority and as a trusted access token issuer. This script is not used if the customer is using a single certificate for multiple SharePoint Add-ins. For that scenario, see  [HighTrustConfig-ForSharedCertificate.ps1](#MultipleAppScript) above. This script is run for each high-trust SharePoint Add-in.</span></span>
 

 
<span data-ttu-id="9be95-p120">In der folgenden Tabelle werden die Parameter und Schalter für das Skript erläutert. Durch Anpassungen des Skripts sind möglicherweise Änderungen an dieser Tabelle erforderlich.</span><span class="sxs-lookup"><span data-stu-id="9be95-p120">The following table describes the parameters and switches for the script. Customization of the script may require changes to this table.</span></span>
 

 


|<span data-ttu-id="9be95-194">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="9be95-194">**Parameter**</span></span>|<span data-ttu-id="9be95-195">**Wert**</span><span class="sxs-lookup"><span data-stu-id="9be95-195">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9be95-196">-CertPath (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="9be95-196">-CertPath (required)</span></span>|<span data-ttu-id="9be95-197">Der vollständige Pfad zur freigegebenen CER-Datei.</span><span class="sxs-lookup"><span data-stu-id="9be95-197">The full path to the shared *.cer file.</span></span>|
|<span data-ttu-id="9be95-198">-CertName (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="9be95-198">-CertName (required)</span></span>|<span data-ttu-id="9be95-p121">Der Name des freigegebenen Zertifikats. Um den Namen zu finden, öffnen Sie IIS auf dem Remotewebserver, der die Remotewebanwendung hostet. Markieren Sie den Knoten  _Servername_ und klicken Sie doppelt auf **Zertifikate**. Das Zertifikat wird mit dem Namen aufgelistet.  </span><span class="sxs-lookup"><span data-stu-id="9be95-p121">The name of the shared certificate. To find the name, open IIS on the remote web server that hosts the remote web application. Highlight the  _server name_ node and double-click **Certificates**. The certificate will be listed by its name.</span></span>|
|<span data-ttu-id="9be95-203">-SPAppClientID (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="9be95-203">-SPAppClientID (required)</span></span>|<span data-ttu-id="9be95-p122">Die Client-ID (eine GUID), die beim Registrieren der SharePoint-Add-In auf appregnew.aspx verwendet wurde. Sie wird als Aussteller-ID für den Tokenaussteller verwendet. Das Skript stellt sicher, dass sie kleingeschrieben wird, da dies eine Anforderung an die Aussteller-IDs ist.</span><span class="sxs-lookup"><span data-stu-id="9be95-p122">The client ID (a GUID) that was used when the SharePoint Add-in was registered on appregnew.aspx. This is used as the issuer ID for the token issuer. The script ensures that it is lower-case, which is a requirement for issuer IDs.</span></span>|
|<span data-ttu-id="9be95-207">-TokenIssuerFriendlyName (optional)</span><span class="sxs-lookup"><span data-stu-id="9be95-207">-TokenIssuerFriendlyName (optional)</span></span>|<span data-ttu-id="9be95-p123">Ein eindeutiger Anzeigename für den Tokenaussteller mit bis zu 50 Zeichen. Dies kann beim Debuggen von Problemen mit Tokenausstellern hilfreich sein. Der Name muss eindeutig sein. Erwägen Sie die Verwendung des Namens der SharePoint-Add-In. Wenn dieser Parameter nicht verwendet wird, verwendet das Skript den Wert der  `-SPAppClientID` als Namen.</span><span class="sxs-lookup"><span data-stu-id="9be95-p123">A unique friendly name for the token issuer, up to 50 characters. This can be helpful if you are debugging issues with token issuers. The name must be unique. Consider using the name of the SharePoint Add-in. If this parameter is not used, the script uses the value of  `-SPAppClientID` as the name.</span></span>|
<span data-ttu-id="9be95-213">Im Folgenden finden Sie ein Beispiel zum Aufrufen des Skripts:</span><span class="sxs-lookup"><span data-stu-id="9be95-213">The following is an example of calling the script:</span></span>
 

 
 `./HighTrustConfig-ForSingleApp.ps1 -CertPath "\\MyServer\Certs\MyCert.cer" -CertName "My Cert" -SPAppClientID "afe332f4-1f87-4c31-89b8-9c343ad7f24e" -TokenIssuerFriendlyName "Payroll add-in"`
 

 

 <span data-ttu-id="9be95-p124">**Wichtig** Die Registrierung des Zertifikats als Tokenaussteller wird nicht sofort wirksam. Es kann bis zu 24 Stunden dauern, bis alle SharePoint-Server den neuen Tokenaussteller erkannt haben. Durch Ausführen von „iisreset“ auf allen SharePoint-Servern wird der Aussteller sofort erkannt, wenn dies möglich ist, ohne die SharePoint-Benutzer zu stören.</span><span class="sxs-lookup"><span data-stu-id="9be95-p124">**Important** The registration of the certificate as a token issuer is not effective immediately. It may take as long as 24 hours before all the SharePoint servers recognize the new token issuer. Running an iisreset on all the SharePoint servers would cause them to immediately recognize the issuer, if you can do that without disturbing SharePoint users.</span></span>
 

<span data-ttu-id="9be95-p125">Beginnen Sie eine neue Datei in einem Text-Editor oder dem PowerShell-Editor und kopieren Sie das Folgende in eine Textdatei und speichern Sie sie als HighTrustConfig-ForSharedCertificate.ps1. Verwenden Sie dazu das ANSI-Format, nicht UTF-8.</span><span class="sxs-lookup"><span data-stu-id="9be95-p125">Start a new file in a text editor, or the PowerShell editor, and copy the following into a text file and save it as HighTrustConfig-ForSingleApp.ps1. Use ANSI format, not UTF-8.</span></span>
 

 



```
param(
    [Parameter(Mandatory)][String] $CertPath = $(throw "Usage: HighTrustConfig-ForSingleApp.ps1 -CertPath <full path to .cer file> -CertName <name of certificate> [-SPAppClientID <client ID of SharePoint add-in>] [-TokenIssuerFriendlyName <friendly name>]"),
    [Parameter(Mandatory)][String] $CertName,
    [Parameter(Mandatory)][String] $SPAppClientID,
    [Parameter()][String] $TokenIssuerFriendlyName
) 
# Stop if there's an error
$ErrorActionPreference = "Stop"

# Ensure friendly name is short enough
if ($TokenIssuerFriendlyName.Length -gt 50)
{
    throw "-TokenIssuerFriendlyName must be unique name of no more than 50 characters."
} 

# Get the certificate
$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($CertPath)

# Make the certificate a trusted root authority in SharePoint
New-SPTrustedRootAuthority -Name $CertName -Certificate $certificate 

# Get the GUID of the authentication realm
$realm = Get-SPAuthenticationRealm

# Must use the client ID as the specific issuer ID. Must be lower-case!
$specificIssuerId = New-Object System.String($SPAppClientID).ToLower()

# Create full issuer ID in the required format
$fullIssuerIdentifier = $specificIssuerId + '@' + $realm 

# Create issuer name
if ($TokenIssuerFriendlyName.Length -ne 0)
{
    $tokenIssuerName = $TokenIssuerFriendlyName
}
else
{
    $tokenIssuerName = $specificIssuerId 
}

# Register the token issuer
New-SPTrustedSecurityTokenIssuer -Name $tokenIssuerName -Certificate $certificate -RegisteredIssuerName $fullIssuerIdentifier

```


 <span data-ttu-id="9be95-219">**Tipp** Die Tipps am Ende des vorherigen Abschnitts gelten auch hier, verwenden Sie jedoch für den Parameter `-Identity` des Cmdlets `Remove-SPTrustedSecurityTokenIssuer` die Client-ID, wenn der Parameter `-TokenIssuerFriendlyName` nicht mit HighTrustConfig-ForSingleApp.ps1. verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="9be95-219">**TIP** The tips at the end of the preceding section apply here as well, but for the  `-Identity` parameter of the `Remove-SPTrustedSecurityTokenIssuer` cmdlet, use the client ID if the `-TokenIssuerFriendlyName` parameter was not used with HighTrustConfig-ForSingleApp.ps1.</span></span>
 


## <a name="modifications-needed-for-site-subscriptions"></a><span data-ttu-id="9be95-220">Erforderliche Änderungen für Website-Abonnements</span><span class="sxs-lookup"><span data-stu-id="9be95-220">Modifications needed for site subscriptions</span></span>
<span data-ttu-id="9be95-221"><a name="SiteSubscriptions"> </a></span><span class="sxs-lookup"><span data-stu-id="9be95-221"></span></span>

<span data-ttu-id="9be95-p126">Ein Websiteabonnement, manchmal auch als Mandant bezeichnet, ist eine Untergruppe von Websitesammlungen in einer SharePoint-Farm. Websiteabonnements werden in der Regel in gehosteten SharePoint-Farmen erstellt. Wenn der Kunde dem besonders vertrauenswürdigen SharePoint-Add-In das Add-In in einer Farm installieren möchte, die für Websiteabonnements konfiguriert wurde, muss eins der beiden verwendeten HighTrustConfig-*.ps1-Skripts geändert werden. Jedes Websiteabonnement hat seine eigene Bereichs-ID, die Zeile `$realm = Get-SPAuthenticationRealm` in den Skripts gibt jedoch immer den Bereich der Farm zurück. Die von einem Tokenaussteller ausgegebenen Zugriffstoken werden von SharePoint nur für den Bereich als gültig angesehen, der in der vollständigen Aussteller-ID nach dem „@"-Zeichen angegeben ist. Um den korrekten Bereich für die Website abzurufen, in dem das Add-In installiert wird, muss das Skript den `-ServiceContext`-Parameter in dem Aufruf an  `Get-SPAuthenticationRealm` verwenden. Das Dienstkontextobjekt wird wiederum aus der übergeordneten Websitesammlung der Zielwebsite erstellt. Es folgt ein Beispiel, bei dem `$WebURL` eine Zeichenfolgenvariable mit der vollständigen URL einer SharePoint-Website darstellt, z. B. „http://marketing.contoso.com/sites/northteam/july." Mit diesem Code kann das besonders vertrauenswürdige Add-In ausgeführt werden, nicht nur auf der angegeben Website, sondern auf jeder Website innerhalb des gleichen Websiteabonnements.</span><span class="sxs-lookup"><span data-stu-id="9be95-p126">A site subscription, sometimes called a tenancy, is a subset of the site collections on a SharePoint farm. Site subscriptions are typically created on hosted SharePoint farms. If the customer of the high-trust SharePoint Add-in wants to install the add-in on a farm that has been configured for site subscriptions, then whichever of the two HighTrustConfig-*.ps1 scripts is being used needs to be modified. Each site subscription has its own realm ID, but the line  `$realm = Get-SPAuthenticationRealm` in the scripts always returns the realm of the farm. The access tokens issued by a token issuer are only regarded as valid by SharePoint for the realm that is specified after the "@" character in the full issuer ID. To get the correct realm for the website where the add-in is going to be installed, the script has to use the `-ServiceContext` parameter in the call to `Get-SPAuthenticationRealm`. The service context object, in turn, is created from the parent site collection of the of the target website. The following is an example, where  `$WebURL` is a string variable with the full URL of a SharePoint website, such as "http://marketing.contoso.com/sites/northteam/july." This code enables the high-trust add-in to be run, not just on the website specified, but on every website within the same site subscription.</span></span>
 

 

```
$Web = Get-SPWeb $WebURL
$sc = Get-SPServiceContext -Site $Web.Site
$realm = Get-SPAuthenticationRealm -ServiceContext $sc
```

<span data-ttu-id="9be95-231">Um die Änderung des Skripts abzuschließen, fügen Sie oben in der Datei einen zusätzlichen erforderlichen Parameter  `$WebURL` wie folgt zur Parameterliste hinzu:</span><span class="sxs-lookup"><span data-stu-id="9be95-231">To complete the modification of the script, add an additional required parameter  `$WebURL` to the param list at the top of the file, like this:</span></span>
 

 



```
param (
    # other parameters omitted 
    [Parameter()][String] $WebURL
)
```

<span data-ttu-id="9be95-p127">Achten Sie darauf, nach dem Parameter ein Komma zu setzen, der vor dem neuen steht. Und erweitern Sie das Verwendungsbeispiel in der oberen Zeile, um den neuen Parameter folgendermaßen zu berücksichtigen:  `-WebURL <full URL where SP add-in will be installed>`.</span><span class="sxs-lookup"><span data-stu-id="9be95-p127">Be sure to add a comma after the parameter that precedes the new one. And expand the "Usage" example on the top line to take into account the new parameter with something like this:  `-WebURL <full URL where SP add-in will be installed>`.</span></span>
 

 
<span data-ttu-id="9be95-p128">Damit die SharePoint-Add-In bei jedem Websiteabonnement vertrauenswürdig ist, müssen Sie mit dem  `Get-SPFarm`-Cmdlet einen Verweis zur Farm abrufen, und anschließend die **SiteSubscriptions**-Eigenschaft durchlaufen. Übergeben Sie jedes **SPSiteSubscription**-Objekt als Wert des  `-SiteSubscription`-Parameters an das  `Get-SPServiceContext`-Cmdlet. Im Folgenden finden Sie dazu ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="9be95-p128">To make the SharePoint Add-in trusted on every site subscription, get a reference to the farm with the  `Get-SPFarm` cmdlet, and then iterate through its **SiteSubscriptions** property. Pass each **SPSiteSubscription** object to the `Get-SPServiceContext` cmdlet as the value of the `-SiteSubscription` parameter. The following is an example.</span></span>
 

 



```
$Farm = Get-SPFarm
foreach ($ss in $Farm.SiteSubscriptions)
{
    $sc = Get-SPServiceContext -SiteSubscription $ss
    $realm = Get-SPAuthenticationRealm -ServiceContext $sc

    # All of the lines from the draft script below the call to 
    # Get-SPAuthenticationRealm are inserted here inside the loop.
}
# end of script
```


