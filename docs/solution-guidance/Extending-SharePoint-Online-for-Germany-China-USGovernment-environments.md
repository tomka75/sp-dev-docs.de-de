---
title: "Aspekte der Autorisierung für den Mandanten in Deutschland, China oder US-Regierung-Umgebungen gehostet"
ms.date: 11/03/2017
ms.openlocfilehash: fd1ac87cf2dd2eb4ef2acf46e11afc7ea0192a44
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="authorization-considerations-for-tenants-hosted-in-the-germany-china-or-us-government-environments"></a>Aspekte der Autorisierung für den Mandanten in Deutschland, China oder US-Regierung-Umgebungen gehostet

Wenn Ihre Office 365-Mandanten in einer bestimmten Umgebung wie der Deutschland gehostet wird, müssen können Sie China oder US-Regierung Umgebungen nehmen dieses Konto aus, wenn Sie anhand Ihres Mandanten entwickeln. 

_**Gilt für:** Office 365 gehostet in Deutschland, China oder US-Regierung-Umgebungen_


## <a name="introduction"></a>Einführung
<a name="introduction"> </a>

Microsoft hat bestimmte Office 365-Bereitstellungen in Deutschland, China und für US-Regierung für diese Bereiche die spezifischen Vorschriften zu erfüllen. Unten Links bieten Sie mehr Kontext:
- [Office 365 Deutschland](https://technet.microsoft.com/en-us/library/mt793278.aspx)
- [Office 365 handelt, das von 21Vianet (China)](https://technet.microsoft.com/en-us/library/mt651782.aspx)
- [Office 365 US-Regierung](https://technet.microsoft.com/library/mt774581.aspx)

Wenn Sie ein Entwickler sind dedizierte Zielgruppenadressierung von Anwendungen für SharePoint Online in dieser Umgebung gehostet wird, müssen Sie im Konto ausgeführt wird, die diesen Umgebungen haben ihre eigenen Azure AD Authentication Endpunkte, die Sie als Entwickler verwenden müssen. Unter Kapitel wird erläutert, wie verwenden Sie diese dedizierten Endpunkte für die typischen Anpassungsoptionen für SharePoint Online.

## <a name="using-azure-ad-to-authorize"></a>Verwenden zum Autorisieren von Azure AD
<a name="usingazureadtoauthorize"> </a>

### <a name="azure-ad-endpoints"></a>Azure AD-Endpunkte
<a name="adendpoints"> </a>

Wenn die Azure AD-Anwendung so autorisieren Sie muss soll den richtigen Endpunkt verwenden. Unter Tabelle beschreibt die Endpunkte verwenden, je nachdem, wo die Azure AD-Anwendung definiert wurde:

|**Umgebung**|**Endpoint**|
|:-----|:-----|
| Produktion | https://Login.Windows.NET |
| Deutschland | https://Login.microsoftonline.de |
| China | https://Login.chinacloudapi.CN |
| US-Regierung | https://Login-US.microsoftonline.com |

### <a name="using-pnp-to-authorize-using-azure-ad"></a>Verwenden von Plug & Play-zum Autorisieren von Azure AD
<a name="adpnp"> </a>

Die Plug & Play- [CustomTargetNameDictionary](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) bietet eine einfache Möglichkeit zum Abrufen einer SharePoint ClientContext-Objekts bei Verwendung eine Azure AD-Anwendung. Die betroffenen Methoden wurden erweitert wurde, mit einem optionalen `AzureEnvironment` Enum

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

Beachten Sie die unten Ausschnitt zeigt eine nur-app-Autorisierung, den letzten Parameter in der `GetAzureADAppOnlyAuthenticatedContext` Methode:
```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string aadAppId = "079d8797-cebc-4cda-a3e0-xxxx"; 
string pfxPassword = "my password";
ClientContext cc = new AuthenticationManager().GetAzureADAppOnlyAuthenticatedContext(siteUrl, 
            aadAppId, "contoso.onmicrosoft.de", @"C:\contoso.pfx", pfxPassword, AzureEnvironment.Germany);
```

Ein interaktiver Benutzer Anmeldung mit einer anderen Ausschnitt mit der die `GetAzureADNativeApplicationAuthenticatedContext` Methode:

```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string aadAppId = "ff76a9f4-430b-4ee4-8602-xxxx"; 
ClientContext cc = new AuthenticationManager().GetAzureADNativeApplicationAuthenticatedContext(siteUrl, 
            aadAppId, "https://contoso.com/test", environment: AzureEnvironment.Germany);
```

## <a name="using-azure-acs-to-authorize-your-sharepoint-add-in"></a>Verwendung von Azure ACS zum Autorisieren von Ihrer SharePoint-add-Ins
<a name="usingazureacs"> </a>

Beim Erstellen von SharePoint-add-ins müssen sie in der Regel niedriger Vertrauenswürdigkeit Autorisierung abhängig von Azure ACS als Descrived in [Erstellen von SharePoint-Add-ins, die niedriger Vertrauenswürdigkeit Autorisierung verwenden](https://msdn.microsoft.com/en-us/library/office/dn790707.aspx).


### <a name="azure-acs-endpoints"></a>Azure ACS-Endpunkte
<a name="endpointsacs"> </a>


|**Umgebung**|**Endpunkt-Präfix**|**Endpoint**|
|:-----|:-----|:-----|
| Produktion | Konten | AccessControl.Windows.NET |
| Deutschland | Anmeldung | microsoftonline.de |
| China | Konten | AccessControl.chinacloudapi.CN |
| US-Regierung | Konten | AccessControl.Windows.NET |

Mit diesem Modell der ACS-Endpunkt-Url wie https:// + Endpunkt formatiert ist Präfix + / + Endpunkt. Damit die URL für die Produktion https://accounts.accesscontrol.windows.net werden, wird ein für Deutschland https://login.microsoftonline.de sein.

### <a name="updating-tokenhelpercs-in-your-applications"></a>Aktualisieren von "tokenhelper.cs" in der Anwendung
<a name="tokenhelperacs"> </a>

Wenn Sie SharePoint-add-ins Autorisierung mit Azure ACS, und klicken Sie dann Sie nutzen tun möchten `tokenhelper.cs` (oder `tokenhelper.vb`). Die standardmäßige Tokenhelper-Klasse verfügen hartcodierten Verweise auf die Azure ACS Endpunkte und Methoden, um den ACS-Endpunkt wie unten dargestellt zu erwerben:

```C#
...

private static string GlobalEndPointPrefix = "accounts";
private static string AcsHostUrl = "accesscontrol.windows.net";

...
```

#### <a name="tokenhelpercs-updates-for-germany"></a>Updates für Deutschland "tokenhelper.cs"
Aktualisieren Sie die statischen Variablen `GlobalEndPointPrefix` und `AcsHostUrl` auf die Deutschland Azure ACS-Werte.

```C#
...

private static string GlobalEndPointPrefix = "login";
private static string AcsHostUrl = "microsoftonline.de";

...
```

#### <a name="tokenhelpercs-updates-for-china"></a>Tokenhelper.cs Updates für China
Aktualisieren Sie die statischen Variablen `GlobalEndPointPrefix` und `AcsHostUrl` auf die China Azure ACS-Werte:

```C#
...

private static string GlobalEndPointPrefix = "accounts";
private static string AcsHostUrl = "accesscontrol.chinacloudapi.cn";

...
```

### <a name="using-pnp-to-authorize-your-add-in-using-azure-acs"></a>Verwenden zum Autorisieren von Ihr Add-in mithilfe von Azure ACS Plug & Play-
<a name="pnpacs"> </a>

Die Plug & Play- [CustomTargetNameDictionary](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) bietet eine einfache Möglichkeit, eine SharePoint-ClientContext-Objekt zu erhalten, wenn Sie zum Autorisieren von Azure ACS verwenden. Die betroffenen Methoden wurden erweitert wurde, mit einem optionalen `AzureEnvironment` Enum

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

Beachten Sie die unten Ausschnitt zeigt eine nur-app-Autorisierung, den letzten Parameter in der `GetAppOnlyAuthenticatedContext` Methode:
```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string acsAppId = "955c10f2-7072-47f8-8bc1-xxxxx"; 
string acsAppSecret = "jgTolmGXU9DW8hUKgletoxxxxx"; 
ClientContext cc = new AuthenticationManager().GetAppOnlyAuthenticatedContext(siteUrl, acsAppId, 
                acsAppSecret, AzureEnvironment.Germany);
```


### <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Informieren Sie sich über Office 365 Deutschland](https://support.office.com/en-US/article/Learn-about-Office-365-Germany-8a5a4bbc-667a-4cac-8769-d8ac9015db4c) 
- [Informieren Sie sich über Office 365 handelt, das von 21Vianet (China)](https://support.office.com/en-us/article/Learn-about-Office-365-operated-by-21Vianet-A8AB5061-3346-4DA0-BB7C-5260822B53AE)