---
title: "Problembehandlung besonders vertrauenswürdiger Add-Ins"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f195d06c28eae988551d2bd4eb2add49007876dc
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="troubleshooting-high-trust-sharepoint-add-ins"></a><span data-ttu-id="6d2be-102">Problembehandlung bei SharePoint-Add-Ins mit hoher Vertrauensstellung</span><span class="sxs-lookup"><span data-stu-id="6d2be-102">Troubleshooting high-trust SharePoint Add-ins</span></span>
<span data-ttu-id="6d2be-103">Hier erhalten Sie Unterstützung bei Problemen mit der Entwicklung von besonders vertrauenswürdigen Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="6d2be-103">Get some help with problems developing high-trust SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="6d2be-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="6d2be-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="6d2be-107">Dieser Artikel beschreibt das Fiddler-Tool und enthält Hinweise zum Beheben von einiger spezieller Probleme.</span><span class="sxs-lookup"><span data-stu-id="6d2be-107">This article describes the Fiddler tool and also provides some guidance for resolving some specific issues.</span></span>
 

## <a name="use-the-fiddler-tool"></a><span data-ttu-id="6d2be-108">Verwenden des Fiddler-Tools</span><span class="sxs-lookup"><span data-stu-id="6d2be-108">Use the Fiddler tool</span></span>

<span data-ttu-id="6d2be-p102">Das kostenlose  [Fiddler-Tool](http://www.telerik.com/fiddler) kann verwendet werden, um die HTTP-Anforderungen zu erfassen, die von der Remotekomponente Ihres Add-Ins an SharePoint gesendet werden. Es gibt eine [kostenlose Erweiterung für das Tool](https://github.com/andrewconnell/SPOAuthFiddlerExt), die automatisch die Zugriffstoken in den Anforderungen dekodiert.</span><span class="sxs-lookup"><span data-stu-id="6d2be-p102">The free  [Fiddler tool](http://www.telerik.com/fiddler) can be used to capture the HTTP Requests sent by the remote component of your add-in to SharePoint. There is a [free extension to the tool](https://github.com/andrewconnell/SPOAuthFiddlerExt) that automatically decodes the access tokens in the requests.</span></span>
 

 
<span data-ttu-id="6d2be-p103">Nachdem Sie Fiddler auf dem Webanwendungsserver installiert haben, fügen Sie das folgende Markup zur Datei web.config hinzu, damit Anforderungen von Ihrer Remoteweb-App über diesen Proxy gehen. Auf diese Weise können Sie eine Fiddler-Ablaufverfolgung erfassen und die vollständige Antwort von SharePoint anzeigen, wenn Sie eine Fehlermeldung erhalten.</span><span class="sxs-lookup"><span data-stu-id="6d2be-p103">After you have installed Fiddler on the web application server, add the following markup to your web.config file to make requests from your remote web app go through this proxy. This way, you can capture a Fiddler trace and see the full response from SharePoint when you get an error.</span></span>
 

 

 <span data-ttu-id="6d2be-p104">**Hinweis** Stellen Sie sicher, dass Sie dieses Markup entfernen, wenn Fiddler nicht ausgeführt wird. Wenn Sie das Markup nicht entfernen, kann Ihr Add-In keine HTTP-Anforderungen durchführen.</span><span class="sxs-lookup"><span data-stu-id="6d2be-p104">**Note**  Ensure that you remove this markup if you are not running Fiddler. If you don't remove the markup, your add-in won't be able to make HTTP requests.</span></span>
 




```XML
<system.net>
  <defaultProxy>
    <proxy usesystemdefault="False" bypassonlocal="False" proxyaddress="http://127.0.0.1:8888" />
  </defaultProxy>
</system.net>

```

<span data-ttu-id="6d2be-p105">Nachdem Fiddler installiert wurde, können Sie außerdem die Antwortheader von SharePoint überprüfen, die eine Anforderungs-GUID enthalten. Diese Anforderungs-GUID ist eine Korrelations-ID, die Sie in den Protokollen suchen können, um dieser Anforderung zugeordnete Protokollfehler zu finden.</span><span class="sxs-lookup"><span data-stu-id="6d2be-p105">After you have Fiddler installed, you can also check the response headers from SharePoint, which will include a request GUID. This request GUID is a correlation ID you can look up in the logs to find any log errors associated with that request.</span></span>
 

 

## <a name="401-unauthorized-error"></a><span data-ttu-id="6d2be-117">Fehler „401 - Nicht autorisiert“</span><span class="sxs-lookup"><span data-stu-id="6d2be-117">401 Unauthorized error</span></span>
<span data-ttu-id="6d2be-118"><a name="UnauthorizedException"> </a></span><span class="sxs-lookup"><span data-stu-id="6d2be-118"></span></span>

<span data-ttu-id="6d2be-p106">Ein Fehler **401 - Nicht autorisiert** kann durch verschiedene Dinge verursacht werden, wenn das besonders vertrauenswürdige Add-In erstmals auf SharePoint zugreift. Wenn Sie das clientseitige Objektmodell (CSOM) verwenden, sieht der Fehler in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="6d2be-p106">Several things can cause a  **401 Unauthorized** error when the high-trust add-in first accesses SharePoint. If you are using the Client-side Object Model (CSOM), the error looks something like the following:</span></span>
 

 

```C#
[WebException: The remote server returned an error: (401) Unauthorized.]
   System.Net.HttpWebRequest.GetResponse() +8515936
   Microsoft.SharePoint.Client.SPWebRequestExecutor.Execute() +178
   Microsoft.SharePoint.Client.ClientRequest.ExecuteQueryToServer(ChunkStringBuilder sb) +1427
   Microsoft.SharePoint.Client.ClientRequest.ExecuteQuery() +270
   Microsoft.SharePoint.Client.ClientRuntimeContext.ExecuteQuery() +146
   Microsoft.SharePoint.Client.ClientContext.ExecuteQuery() +666
   S2STestWeb.Default.Page_Load(Object sender, EventArgs e) in c:\MyFiles\HightrustTest\HightrustTestWeb\Default.aspx.cs:28
   System.Web.UI.Control.LoadRecursive() +71
   System.Web.UI.Page.ProcessRequestMain(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint) +3178
```

<span data-ttu-id="6d2be-121">Wenn Sie die TokenHelper-Datei und Windows-Identität verwenden, sieht der Code, der die Ausnahme auslöst, folgendermaßen aus:</span><span class="sxs-lookup"><span data-stu-id="6d2be-121">If you are using the TokenHelper file and Windows identity, the code that triggers the exception looks like the following:</span></span>
 

 



```C#
ClientContext clientContext = 
    TokenHelper.GetS2SClientContextWithWindowsIdentity(sharepointUrl, Request.LogonUserIdentity); 
clientContext.Load(clientContext.Web);
clientContext.ExecuteQuery();
```

<span data-ttu-id="6d2be-p107">Der erste Schritt zur Behebung des Problems besteht darin, mit dem Visual Studio-Debugger zu überprüfen, ob das Zugriffstoken und das **ClientContext**-Objekt erfolgreich aufgebaut sind. Falls ja, untersuchen Sie die folgenden Möglichkeiten:</span><span class="sxs-lookup"><span data-stu-id="6d2be-p107">Your first step in troubleshooting the issue is to use the Visual Studio debugger to verify that the access token and the  **ClientContext** object are constructed successfully. If they are, investigate the following possibilities:</span></span>
 

 
 <span data-ttu-id="6d2be-124">**Mögliche Probleme und Lösung:**</span><span class="sxs-lookup"><span data-stu-id="6d2be-124">**Possible issues and resolution:**</span></span>
 

 

- <span data-ttu-id="6d2be-p108">Es wurde kein Benutzerprofil für den Benutzer erstellt, der auf die Remotewebanwendung zugreift. Erstellen Sie das Benutzerprofil.</span><span class="sxs-lookup"><span data-stu-id="6d2be-p108">There is no user profile created for the user who is accessing the remote web application. Create the user profile.</span></span>
    
 
- <span data-ttu-id="6d2be-p109">Ihr Add-In verfügt nicht über die Berechtigung für die Ressource, auf die Sie zugreifen möchten. Öffnen Sie die SharePoint-Verwaltungsshell, und führen Sie das folgende Windows PowerShell-Cmdlet aus. Die Variable  `$web` ist die SharePoint-Website, auf die Sie zugreifen möchten, und `$appPrincipal`) ist die Add-In-ID. Weitere Informationen finden Sie unter  [Set-SPAppPrincipalPermission](http://technet.microsoft.com/de-DE/library/jj219714%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d2be-p109">Your add-in does not have permission to the resource you are trying to access. Open the SharePoint Management Shell and run that the following Windows PowerShell cmdlet. The variable  `$web` is the SharePoint website you are trying to get access to and `$appPrincipal`) is the add-in ID. For more information, see  [Set-SPAppPrincipalPermission](http://technet.microsoft.com/de-DE/library/jj219714%28v=office.15%29.aspx).</span></span>
    
```
  Set-SPAppPrincipalPermission -Site $web -AppPrincipal $appPrincipal -Scope Site -Right FullControl
```

- <span data-ttu-id="6d2be-p110">Ihre Webanwendung akzeptiert anonyme Anforderungen. Dies bedeutet, dass das Zugriffstoken keine echte Benutzeridentität enthält. Stellen Sie sicher, dass für das Stammverzeichnis Ihrer Remotewebanwendung der anonyme Zugriff in IIS deaktiviert ist. Sie können dies auch überprüfen, indem Sie Ihre Remotewebanwendung debuggen und den Wert von **Request.LogonUserIdentity** in der Datei „default.aspx.cs“ (oder .vb) überprüfen, um sicherzustellen, dass es sich nicht um einen anonymen Benutzer handelt.</span><span class="sxs-lookup"><span data-stu-id="6d2be-p110">Your web application is accepting anonymous requests. This means there is not a real user identity in the access token. Ensure that anonymous access has been disabled in IIS for the root directory of your remote web application. You can also check this by debugging your remote web application, and checking the value of  **Request.LogonUserIdentity** in the default.aspx.cs (or .vb) file to ensure that it's not an anonymous user.</span></span>
    
 
- <span data-ttu-id="6d2be-p111">Ihr digitales Zertifikat wurde dem vertrauenswürdigen Zertifikatspeicher nicht hinzugefügt. Stellen Sie sicher, dass Sie die Verfahren in  [Packen und Veröffentlichen besonders vertrauenswürdiger Add-Ins für SharePoint](package-and-publish-high-trust-sharepoint-add-ins.md) befolgt haben.</span><span class="sxs-lookup"><span data-stu-id="6d2be-p111">Your digital certificate was not added to the trusted certificate store. Be sure you have followed the procedures in  [Package and publish high-trust SharePoint Add-ins](package-and-publish-high-trust-sharepoint-add-ins.md).</span></span>
    
 

## <a name="miscellaneous-ssl-and-domain-related-authorization-errors"></a><span data-ttu-id="6d2be-137">Verschiedene SSL- und domänenbezogene Autorisierungsfehler</span><span class="sxs-lookup"><span data-stu-id="6d2be-137">Miscellaneous SSL and domain-related authorization errors</span></span>
<span data-ttu-id="6d2be-138"><a name="DomainRelatedErrors"> </a></span><span class="sxs-lookup"><span data-stu-id="6d2be-138"></span></span>

<span data-ttu-id="6d2be-p112">Die fehlende Übereinstimmung von Domänennamen in Konfigurationsdateien und Registrierungsformularen kann die Autorisierung verhindern. Die folgenden vier Werte müssen exakt gleich sein:</span><span class="sxs-lookup"><span data-stu-id="6d2be-p112">A mismatch of domain names in configuration files and registration forms can prevent authorization. The following four values have to be exactly the same:</span></span>
 

 

- <span data-ttu-id="6d2be-141">Die **Add-In-Domäne**, die angegeben wird, wenn das SharePoint-Add-In auf der Seite „AppRegNew.aspx“ registriert wird</span><span class="sxs-lookup"><span data-stu-id="6d2be-141">The  **Add-in Domain** that is specified when the SharePoint Add-in is registered on AppRegNew.aspx.</span></span>
    
 
- <span data-ttu-id="6d2be-142">Die Domäne, die unter der das Sicherheitszertifikat der Remotewebanwendung registriert ist</span><span class="sxs-lookup"><span data-stu-id="6d2be-142">The domain under which the remote web application's security certificate is registered.</span></span>
    
 
- <span data-ttu-id="6d2be-143">Der Domänenteil des Werts **StartPage** in der Datei „AppManifest.xml“</span><span class="sxs-lookup"><span data-stu-id="6d2be-143">The domain part of the  **StartPage** value in the AppManifest.xml file.</span></span>
    
 
- <span data-ttu-id="6d2be-144">Der Domänenteil der URL aller Ereignisempfänger, die in der Datei „AppManifest.xml“ angegeben sind</span><span class="sxs-lookup"><span data-stu-id="6d2be-144">The domain part of the URLs of any event receivers specified in the AppManifest.xml.</span></span>
    
 
<span data-ttu-id="6d2be-145">Beachten Sie in Verbindung mit diesem Punkt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6d2be-145">In connection with this point, note the following:</span></span>
 

 

- <span data-ttu-id="6d2be-p113">Wenn die Remotekomponente Ihres SharePoint-Add-In einen anderen Port als 443 verwendet, müssen Sie den Port ausdrücklich als Teil der Domäne an allen vier Stellen einschließen, beispielsweise  `MarketingServer:3333`. (Sie müssen das HTTPS-Protokoll verwenden, für das der Standardport 443 ist.)</span><span class="sxs-lookup"><span data-stu-id="6d2be-p113">If the remote component of your SharePoint Add-in is using any port other than 443, you must explicitly include the port as part of the domain in all four places; for example,  `MarketingServer:3333`. (You must use the HTTPS protocol for which the default port is 443.)</span></span>
    
 
- <span data-ttu-id="6d2be-p114">Die Domäne muss in den Wert **StartPage** (und allen URLs von Ereignisempfängern) der Datei „AppManifest.xml“ hartcodiert werden, bevor das Add-In gepackt wird. Wenn Sie den **Veröffentlichungs**-Assistenten in Visual Studio verwenden, um das Add-In zu packen, werden Sie aufgefordert, die Domäne anzugeben, und die Office Developer Tools für Visual Studio fügen diese für Sie in den Wert **StartPage** ein (anstelle des `~remoteWebUrl`-Tokens, das während des Debuggings verwendet wird). Wenn Sie den **Veröffentlichungs**-Assistenten jedoch nicht verwenden, müssen Sie das Token manuell durch die Domäne (und das Protokoll) ersetzen, z. B. `https://MarketingServer` oder `https://MarketingServer:3333`.</span><span class="sxs-lookup"><span data-stu-id="6d2be-p114">The domain needs to be hardcoded in the  **StartPage** value (and any event receiver URLs) of the AppManifest.xml file before the add-in is packaged. If you use the **Publish** wizard in Visual Studio to package the add-in, you will be prompted for the domain and the Office Developer Tools for Visual Studio will insert it into the **StartPage** value for you (in place of the `~remoteWebUrl` token that is used during debugging. But if you are not using the **Publish** wizard you must manually replace the token with the domain (and protocol); for example `https://MarketingServer` or `https://MarketingServer:3333`.</span></span>
    
 

## <a name="runtime-error-saying-that-theres-no-certificate-with-that-serial-number"></a><span data-ttu-id="6d2be-151">Laufzeitfehler, der darauf hinweist, dass kein Zertifikat mit der Seriennummer vorhanden ist</span><span class="sxs-lookup"><span data-stu-id="6d2be-151">Runtime error saying that there's no certificate with that serial number</span></span>
<span data-ttu-id="6d2be-152"><a name="DomainRelatedErrors"> </a></span><span class="sxs-lookup"><span data-stu-id="6d2be-152"></span></span>

<span data-ttu-id="6d2be-p115">Wenn Sie sicher sind, dass Sie die richtige Zertifikatseriennummer in der Datei „web.config“ angegeben haben, und Sie das Zertifikat im **Windows-Zertifikatspeicher** sehen, enthält die Seriennummer in „web.config“ möglicherweise ein ausgeblendetes zusätzliches Zeichen. Dies geschieht, wenn die Seriennummer aus der **Microsoft Management Console** kopiert und eingefügt wird. Löschen Sie den gesamten Seriennummernwert aus der Datei „web.config“, und geben Sie ihn *manuell* erneut ein.</span><span class="sxs-lookup"><span data-stu-id="6d2be-p115">If you are sure you have the correct certificate serial number in the web.config and you can see the certificate in the  **Windows Certificate Store**, then there may be a hidden extra character in the serial number in the web.config. This will happen if the serial number is copy'n'pasted from the **Microsoft Management Console**. Delete the entire serial number value from the web.config and *manually*  retype it.</span></span>
 

 

