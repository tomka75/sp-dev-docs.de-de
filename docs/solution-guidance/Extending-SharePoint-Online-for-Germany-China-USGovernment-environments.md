---
title: "Aspekte der Autorisierung für den Mandanten in Deutschland, China oder US-Regierung-Umgebungen gehostet"
ms.date: 11/03/2017
ms.openlocfilehash: fd1ac87cf2dd2eb4ef2acf46e11afc7ea0192a44
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="authorization-considerations-for-tenants-hosted-in-the-germany-china-or-us-government-environments"></a><span data-ttu-id="2d2c5-102">Aspekte der Autorisierung für den Mandanten in Deutschland, China oder US-Regierung-Umgebungen gehostet</span><span class="sxs-lookup"><span data-stu-id="2d2c5-102">Authorization considerations for tenants hosted in the Germany, China or US Government environments</span></span>

<span data-ttu-id="2d2c5-103">Wenn Ihre Office 365-Mandanten in einer bestimmten Umgebung wie der Deutschland gehostet wird, müssen können Sie China oder US-Regierung Umgebungen nehmen dieses Konto aus, wenn Sie anhand Ihres Mandanten entwickeln.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-103">When your Office 365 tenant is hosted in an specific environment like the Germany, China or US Government environments then you'll need to take this in account when you're developing against your tenant.</span></span> 

<span data-ttu-id="2d2c5-104">_**Gilt für:** Office 365 gehostet in Deutschland, China oder US-Regierung-Umgebungen_</span><span class="sxs-lookup"><span data-stu-id="2d2c5-104">_**Applies to:** Office 365 hosted in the Germany, China or US Government environments_</span></span>


## <a name="introduction"></a><span data-ttu-id="2d2c5-105">Einführung</span><span class="sxs-lookup"><span data-stu-id="2d2c5-105">Introduction</span></span>
<span data-ttu-id="2d2c5-106"><a name="introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="2d2c5-106"></span></span>

<span data-ttu-id="2d2c5-107">Microsoft hat bestimmte Office 365-Bereitstellungen in Deutschland, China und für US-Regierung für diese Bereiche die spezifischen Vorschriften zu erfüllen.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-107">Microsoft has specific Office 365 deployments in Germany, China and for US Government to fulfill the specific regulations for those areas.</span></span> <span data-ttu-id="2d2c5-108">Unten Links bieten Sie mehr Kontext:</span><span class="sxs-lookup"><span data-stu-id="2d2c5-108">Below links provide more context:</span></span>
- [<span data-ttu-id="2d2c5-109">Office 365 Deutschland</span><span class="sxs-lookup"><span data-stu-id="2d2c5-109">Office 365 Germany</span></span>](https://technet.microsoft.com/en-us/library/mt793278.aspx)
- [<span data-ttu-id="2d2c5-110">Office 365 handelt, das von 21Vianet (China)</span><span class="sxs-lookup"><span data-stu-id="2d2c5-110">Office 365 operated by 21Vianet (China)</span></span>](https://technet.microsoft.com/en-us/library/mt651782.aspx)
- [<span data-ttu-id="2d2c5-111">Office 365 US-Regierung</span><span class="sxs-lookup"><span data-stu-id="2d2c5-111">Office 365 US Government</span></span>](https://technet.microsoft.com/library/mt774581.aspx)

<span data-ttu-id="2d2c5-112">Wenn Sie ein Entwickler sind dedizierte Zielgruppenadressierung von Anwendungen für SharePoint Online in dieser Umgebung gehostet wird, müssen Sie im Konto ausgeführt wird, die diesen Umgebungen haben ihre eigenen Azure AD Authentication Endpunkte, die Sie als Entwickler verwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-112">If you are a developer targeting applications for SharePoint Online hosted in these environments then you'll need to take in account that these environments have their own dedicated Azure AD authentication endpoints that you as developer need to use.</span></span> <span data-ttu-id="2d2c5-113">Unter Kapitel wird erläutert, wie verwenden Sie diese dedizierten Endpunkte für die typischen Anpassungsoptionen für SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-113">Below chapters explain how do use these dedicated endpoints for the typical SharePoint Online customization options.</span></span>

## <a name="using-azure-ad-to-authorize"></a><span data-ttu-id="2d2c5-114">Verwenden zum Autorisieren von Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d2c5-114">Using Azure AD to authorize</span></span>
<span data-ttu-id="2d2c5-115"><a name="usingazureadtoauthorize"> </a></span><span class="sxs-lookup"><span data-stu-id="2d2c5-115"></span></span>

### <a name="azure-ad-endpoints"></a><span data-ttu-id="2d2c5-116">Azure AD-Endpunkte</span><span class="sxs-lookup"><span data-stu-id="2d2c5-116">Azure AD endpoints</span></span>
<span data-ttu-id="2d2c5-117"><a name="adendpoints"> </a></span><span class="sxs-lookup"><span data-stu-id="2d2c5-117"></span></span>

<span data-ttu-id="2d2c5-118">Wenn die Azure AD-Anwendung so autorisieren Sie muss soll den richtigen Endpunkt verwenden.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-118">When your Azure AD application needs to authorize it needs to use the correct endpoint.</span></span> <span data-ttu-id="2d2c5-119">Unter Tabelle beschreibt die Endpunkte verwenden, je nachdem, wo die Azure AD-Anwendung definiert wurde:</span><span class="sxs-lookup"><span data-stu-id="2d2c5-119">Below table describes the endpoints to use depending on where your Azure AD application has been defined:</span></span>

|<span data-ttu-id="2d2c5-120">**Umgebung**</span><span class="sxs-lookup"><span data-stu-id="2d2c5-120">**Environment**</span></span>|<span data-ttu-id="2d2c5-121">**Endpoint**</span><span class="sxs-lookup"><span data-stu-id="2d2c5-121">**Endpoint**</span></span>|
|:-----|:-----|
| <span data-ttu-id="2d2c5-122">Produktion</span><span class="sxs-lookup"><span data-stu-id="2d2c5-122">Production</span></span> | <span data-ttu-id="2d2c5-123">https://Login.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="2d2c5-123">https://login.windows.net</span></span> |
| <span data-ttu-id="2d2c5-124">Deutschland</span><span class="sxs-lookup"><span data-stu-id="2d2c5-124">Germany</span></span> | <span data-ttu-id="2d2c5-125">https://Login.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="2d2c5-125">https://login.microsoftonline.de</span></span> |
| <span data-ttu-id="2d2c5-126">China</span><span class="sxs-lookup"><span data-stu-id="2d2c5-126">China</span></span> | <span data-ttu-id="2d2c5-127">https://Login.chinacloudapi.CN</span><span class="sxs-lookup"><span data-stu-id="2d2c5-127">https://login.chinacloudapi.cn</span></span> |
| <span data-ttu-id="2d2c5-128">US-Regierung</span><span class="sxs-lookup"><span data-stu-id="2d2c5-128">US Government</span></span> | <span data-ttu-id="2d2c5-129">https://Login-US.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="2d2c5-129">https://login-us.microsoftonline.com</span></span> |

### <a name="using-pnp-to-authorize-using-azure-ad"></a><span data-ttu-id="2d2c5-130">Verwenden von Plug & Play-zum Autorisieren von Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d2c5-130">Using PnP to authorize using Azure AD</span></span>
<span data-ttu-id="2d2c5-131"><a name="adpnp"> </a></span><span class="sxs-lookup"><span data-stu-id="2d2c5-131"></span></span>

<span data-ttu-id="2d2c5-132">Die Plug & Play- [CustomTargetNameDictionary](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) bietet eine einfache Möglichkeit zum Abrufen einer SharePoint ClientContext-Objekts bei Verwendung eine Azure AD-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-132">The PnP [AuthenticationManager](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) offers an easy way to obtain an SharePoint ClientContext object when you're using an Azure AD application.</span></span> <span data-ttu-id="2d2c5-133">Die betroffenen Methoden wurden erweitert wurde, mit einem optionalen `AzureEnvironment` Enum</span><span class="sxs-lookup"><span data-stu-id="2d2c5-133">The impacted methods have been extended with an optional `AzureEnvironment` enum</span></span>

```c#
/// <summary>
/// Enum to identify the supported Office 365 hosting environments
/// </summary>
public enum AzureEnvironment
{
    Production=0,
    PPE=1,
    China=2,
    Germany=3,
    USGovernment=4
}
```

<span data-ttu-id="2d2c5-134">Beachten Sie die unten Ausschnitt zeigt eine nur-app-Autorisierung, den letzten Parameter in der `GetAzureADAppOnlyAuthenticatedContext` Methode:</span><span class="sxs-lookup"><span data-stu-id="2d2c5-134">Below snippet shows an app-only authorization, notice the last parameter in the `GetAzureADAppOnlyAuthenticatedContext` method:</span></span>
```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string aadAppId = "079d8797-cebc-4cda-a3e0-xxxx"; 
string pfxPassword = "my password";
ClientContext cc = new AuthenticationManager().GetAzureADAppOnlyAuthenticatedContext(siteUrl, 
            aadAppId, "contoso.onmicrosoft.de", @"C:\contoso.pfx", pfxPassword, AzureEnvironment.Germany);
```

<span data-ttu-id="2d2c5-135">Ein interaktiver Benutzer Anmeldung mit einer anderen Ausschnitt mit der die `GetAzureADNativeApplicationAuthenticatedContext` Methode:</span><span class="sxs-lookup"><span data-stu-id="2d2c5-135">Another snippet is showing an interactive user login using the `GetAzureADNativeApplicationAuthenticatedContext` method:</span></span>

```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string aadAppId = "ff76a9f4-430b-4ee4-8602-xxxx"; 
ClientContext cc = new AuthenticationManager().GetAzureADNativeApplicationAuthenticatedContext(siteUrl, 
            aadAppId, "https://contoso.com/test", environment: AzureEnvironment.Germany);
```

## <a name="using-azure-acs-to-authorize-your-sharepoint-add-in"></a><span data-ttu-id="2d2c5-136">Verwendung von Azure ACS zum Autorisieren von Ihrer SharePoint-add-Ins</span><span class="sxs-lookup"><span data-stu-id="2d2c5-136">Using Azure ACS to authorize your SharePoint add-in</span></span>
<span data-ttu-id="2d2c5-137"><a name="usingazureacs"> </a></span><span class="sxs-lookup"><span data-stu-id="2d2c5-137"></span></span>

<span data-ttu-id="2d2c5-138">Beim Erstellen von SharePoint-add-ins müssen sie in der Regel niedriger Vertrauenswürdigkeit Autorisierung abhängig von Azure ACS als Descrived in [Erstellen von SharePoint-Add-ins, die niedriger Vertrauenswürdigkeit Autorisierung verwenden](https://msdn.microsoft.com/en-us/library/office/dn790707.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d2c5-138">When you create SharePoint add-ins they'll typically low-trust authorization which depends on Azure ACS as descrived in [Creating SharePoint Add-ins that use low-trust authorization](https://msdn.microsoft.com/en-us/library/office/dn790707.aspx).</span></span>


### <a name="azure-acs-endpoints"></a><span data-ttu-id="2d2c5-139">Azure ACS-Endpunkte</span><span class="sxs-lookup"><span data-stu-id="2d2c5-139">Azure ACS endpoints</span></span>
<span data-ttu-id="2d2c5-140"><a name="endpointsacs"> </a></span><span class="sxs-lookup"><span data-stu-id="2d2c5-140"></span></span>


|<span data-ttu-id="2d2c5-141">**Umgebung**</span><span class="sxs-lookup"><span data-stu-id="2d2c5-141">**Environment**</span></span>|<span data-ttu-id="2d2c5-142">**Endpunkt-Präfix**</span><span class="sxs-lookup"><span data-stu-id="2d2c5-142">**Endpoint prefix**</span></span>|<span data-ttu-id="2d2c5-143">**Endpoint**</span><span class="sxs-lookup"><span data-stu-id="2d2c5-143">**Endpoint**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="2d2c5-144">Produktion</span><span class="sxs-lookup"><span data-stu-id="2d2c5-144">Production</span></span> | <span data-ttu-id="2d2c5-145">Konten</span><span class="sxs-lookup"><span data-stu-id="2d2c5-145">accounts</span></span> | <span data-ttu-id="2d2c5-146">AccessControl.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="2d2c5-146">accesscontrol.windows.net</span></span> |
| <span data-ttu-id="2d2c5-147">Deutschland</span><span class="sxs-lookup"><span data-stu-id="2d2c5-147">Germany</span></span> | <span data-ttu-id="2d2c5-148">Anmeldung</span><span class="sxs-lookup"><span data-stu-id="2d2c5-148">login</span></span> | <span data-ttu-id="2d2c5-149">microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="2d2c5-149">microsoftonline.de</span></span> |
| <span data-ttu-id="2d2c5-150">China</span><span class="sxs-lookup"><span data-stu-id="2d2c5-150">China</span></span> | <span data-ttu-id="2d2c5-151">Konten</span><span class="sxs-lookup"><span data-stu-id="2d2c5-151">accounts</span></span> | <span data-ttu-id="2d2c5-152">AccessControl.chinacloudapi.CN</span><span class="sxs-lookup"><span data-stu-id="2d2c5-152">accesscontrol.chinacloudapi.cn</span></span> |
| <span data-ttu-id="2d2c5-153">US-Regierung</span><span class="sxs-lookup"><span data-stu-id="2d2c5-153">US Government</span></span> | <span data-ttu-id="2d2c5-154">Konten</span><span class="sxs-lookup"><span data-stu-id="2d2c5-154">accounts</span></span> | <span data-ttu-id="2d2c5-155">AccessControl.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="2d2c5-155">accesscontrol.windows.net</span></span> |

<span data-ttu-id="2d2c5-156">Mit diesem Modell der ACS-Endpunkt-Url wie https:// + Endpunkt formatiert ist Präfix + / + Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-156">Using this model the ACS endpoint url to use is formatted like https:// + endpoint prefix + / + endpoint.</span></span> <span data-ttu-id="2d2c5-157">Damit die URL für die Produktion https://accounts.accesscontrol.windows.net werden, wird ein für Deutschland https://login.microsoftonline.de sein.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-157">So the URL for production will be https://accounts.accesscontrol.windows.net, the one for Germany will be https://login.microsoftonline.de.</span></span>

### <a name="updating-tokenhelpercs-in-your-applications"></a><span data-ttu-id="2d2c5-158">Aktualisieren von "tokenhelper.cs" in der Anwendung</span><span class="sxs-lookup"><span data-stu-id="2d2c5-158">Updating tokenhelper.cs in your applications</span></span>
<span data-ttu-id="2d2c5-159"><a name="tokenhelperacs"> </a></span><span class="sxs-lookup"><span data-stu-id="2d2c5-159"></span></span>

<span data-ttu-id="2d2c5-160">Wenn Sie SharePoint-add-ins Autorisierung mit Azure ACS, und klicken Sie dann Sie nutzen tun möchten `tokenhelper.cs` (oder `tokenhelper.vb`).</span><span class="sxs-lookup"><span data-stu-id="2d2c5-160">When you want to do SharePoint add-in authorization using Azure ACS then you're using `tokenhelper.cs` (or `tokenhelper.vb`).</span></span> <span data-ttu-id="2d2c5-161">Die standardmäßige Tokenhelper-Klasse verfügen hartcodierten Verweise auf die Azure ACS Endpunkte und Methoden, um den ACS-Endpunkt wie unten dargestellt zu erwerben:</span><span class="sxs-lookup"><span data-stu-id="2d2c5-161">The default tokenhelper class will have hardcoded references to the Azure ACS endpoints and methods to acquire the ACS endpoint as shown below:</span></span>

```C#
...

private static string GlobalEndPointPrefix = "accounts";
private static string AcsHostUrl = "accesscontrol.windows.net";

...
```

#### <a name="tokenhelpercs-updates-for-germany"></a><span data-ttu-id="2d2c5-162">Updates für Deutschland "tokenhelper.cs"</span><span class="sxs-lookup"><span data-stu-id="2d2c5-162">Tokenhelper.cs updates for Germany</span></span>
<span data-ttu-id="2d2c5-163">Aktualisieren Sie die statischen Variablen `GlobalEndPointPrefix` und `AcsHostUrl` auf die Deutschland Azure ACS-Werte.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-163">Update the static variables `GlobalEndPointPrefix` and `AcsHostUrl` to the Germany Azure ACS values.</span></span>

```C#
...

private static string GlobalEndPointPrefix = "login";
private static string AcsHostUrl = "microsoftonline.de";

...
```

#### <a name="tokenhelpercs-updates-for-china"></a><span data-ttu-id="2d2c5-164">Tokenhelper.cs Updates für China</span><span class="sxs-lookup"><span data-stu-id="2d2c5-164">Tokenhelper.cs updates for China</span></span>
<span data-ttu-id="2d2c5-165">Aktualisieren Sie die statischen Variablen `GlobalEndPointPrefix` und `AcsHostUrl` auf die China Azure ACS-Werte:</span><span class="sxs-lookup"><span data-stu-id="2d2c5-165">Update the static variables `GlobalEndPointPrefix` and `AcsHostUrl` to the China Azure ACS values:</span></span>

```C#
...

private static string GlobalEndPointPrefix = "accounts";
private static string AcsHostUrl = "accesscontrol.chinacloudapi.cn";

...
```

### <a name="using-pnp-to-authorize-your-add-in-using-azure-acs"></a><span data-ttu-id="2d2c5-166">Verwenden zum Autorisieren von Ihr Add-in mithilfe von Azure ACS Plug & Play-</span><span class="sxs-lookup"><span data-stu-id="2d2c5-166">Using PnP to authorize your add-in using Azure ACS</span></span>
<span data-ttu-id="2d2c5-167"><a name="pnpacs"> </a></span><span class="sxs-lookup"><span data-stu-id="2d2c5-167"></span></span>

<span data-ttu-id="2d2c5-168">Die Plug & Play- [CustomTargetNameDictionary](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) bietet eine einfache Möglichkeit, eine SharePoint-ClientContext-Objekt zu erhalten, wenn Sie zum Autorisieren von Azure ACS verwenden.</span><span class="sxs-lookup"><span data-stu-id="2d2c5-168">The PnP [AuthenticationManager](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) offers an easy way to obtain an SharePoint ClientContext object when you're using Azure ACS to authorize.</span></span> <span data-ttu-id="2d2c5-169">Die betroffenen Methoden wurden erweitert wurde, mit einem optionalen `AzureEnvironment` Enum</span><span class="sxs-lookup"><span data-stu-id="2d2c5-169">The impacted methods have been extended with an optional `AzureEnvironment` enum</span></span>

```c#
/// <summary>
/// Enum to identify the supported Office 365 hosting environments
/// </summary>
public enum AzureEnvironment
{
    Production=0,
    PPE=1,
    China=2,
    Germany=3,
    USGovernment=4
}
```

<span data-ttu-id="2d2c5-170">Beachten Sie die unten Ausschnitt zeigt eine nur-app-Autorisierung, den letzten Parameter in der `GetAppOnlyAuthenticatedContext` Methode:</span><span class="sxs-lookup"><span data-stu-id="2d2c5-170">Below snippet shows an app-only authorization, notice the last parameter in the `GetAppOnlyAuthenticatedContext` method:</span></span>
```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string acsAppId = "955c10f2-7072-47f8-8bc1-xxxxx"; 
string acsAppSecret = "jgTolmGXU9DW8hUKgletoxxxxx"; 
ClientContext cc = new AuthenticationManager().GetAppOnlyAuthenticatedContext(siteUrl, acsAppId, 
                acsAppSecret, AzureEnvironment.Germany);
```


### <a name="see-also"></a><span data-ttu-id="2d2c5-171">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2d2c5-171">See also</span></span>
<span data-ttu-id="2d2c5-172"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2d2c5-172"></span></span>

- [<span data-ttu-id="2d2c5-173">Informieren Sie sich über Office 365 Deutschland</span><span class="sxs-lookup"><span data-stu-id="2d2c5-173">Learn about Office 365 Germany</span></span>](https://support.office.com/en-US/article/Learn-about-Office-365-Germany-8a5a4bbc-667a-4cac-8769-d8ac9015db4c) 
- [<span data-ttu-id="2d2c5-174">Informieren Sie sich über Office 365 handelt, das von 21Vianet (China)</span><span class="sxs-lookup"><span data-stu-id="2d2c5-174">Learn about Office 365 operated by 21Vianet (China)</span></span>](https://support.office.com/en-us/article/Learn-about-Office-365-operated-by-21Vianet-A8AB5061-3346-4DA0-BB7C-5260822B53AE)