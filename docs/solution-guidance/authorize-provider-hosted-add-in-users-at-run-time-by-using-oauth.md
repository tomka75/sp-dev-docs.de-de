---
title: Autorisieren von vom Anbieter gehosteten-add-in Benutzern zur Laufzeit mithilfe von OAuth
ms.date: 11/03/2017
ms.openlocfilehash: 45d76f2f005361e3d8fe5ce73355b5c139e87c9e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="authorize-provider-hosted-add-in-users-at-run-time-by-using-oauth"></a>Autorisieren von vom Anbieter gehosteten-add-in Benutzern zur Laufzeit mithilfe von OAuth

Bieten Sie autorisierten Zugriff auf SharePoint-Ressourcen mithilfe von OAuth in vom Anbieter gehosteten-add-ins zur Laufzeit.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

In der Regel greifen Ihre Benutzer SharePoint-Add-ins Öffnen einer SharePoint-Website **Auf Websiteinhalte**, klicken Sie dann auswählen und das Add-in. SharePoint leitet den Benutzer auf die Remotewebsite, wo Ihre vom Anbieter gehosteten-add-in ausgeführt wird. Da Benutzer das Add-in von SharePoint zugreifen zu können, sind Benutzer von SharePoint berechtigt, bevor sie das Add-in zugreifen können.

Alternativ Wenn Ihre Benutzer direkt an die URL der Ihr Add-in vom Anbieter gehosteten wechseln, muss das Add-in sie zur Laufzeit zu autorisieren mithilfe von OAuth. In diesem Szenario muss das Add-in vom Anbieter gehosteten Autorisierung behandeln, da die Benutzer zuerst vom SharePoint autorisiert war nicht. Das [Core.DynamicPermissions](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) -Beispiel veranschaulicht die dynamisch Berechtigungen von einer Website mithilfe von OAuth anfordern.
Mit dieser Lösung können:

- Autorisieren von Benutzern, die direkt an Ihr Add-in vom Anbieter gehosteten statt den Zugriff auf Ihr Add-in aus SharePoint navigieren. Beispielsweise sollten Sie nicht die Benutzer der SharePoint-UI verwenden. Ihre Benutzer möglicherweise stattdessen eine vom Anbieter gehosteten-add-in verwenden, die relevante Daten aus SharePoint abgerufen wird.
    
- Erstellen einer vom Anbieter gehosteten add-Ins, können Benutzer mit OAuth authentifiziert und die über den Office Store verkauft werden können.
    
## <a name="before-you-begin"></a>Bevor Sie beginnen:

Laden Sie Sie zuerst [Core.DynamicPermissions](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Bevor Sie das Codebeispiel ausführen: 

- Stellen Sie sicher, dass Sie Berechtigungen **Verwalten** auf der Website verfügen. Weitere Informationen unter [Understanding Berechtigungsstufen](https://support.office.com/article/Understanding-permission-levels-87ECBB0E-6550-491A-8826-C075E4859848).
    
- Registrieren Sie das Add-in auf einer SharePoint-Website mithilfe von "appregnew.aspx": 
    
    1. Navigieren Sie zu "appregnew.aspx" auf Ihrer SharePoint-Website. Angenommen, wenn Sie das add-in auf der Website contoso.sharepoint.com verwenden möchten, navigieren Sie zu http://contoso.sharepoint.com/_layouts/15/appregnew.aspx.
    
    2. Wählen Sie **generieren** , um eine neue **Client-Id**zu generieren.
    
    3. Wählen Sie Sie **generieren** , um einen neuen **Geheimen Clientschlüssel**generieren. 
    
    4. Geben Sie einen Titel für Ihr Add-in in das Feld **Titel**ein.
    
    5. Geben Sie im **Add-in - Domäne**die URL der vom Anbieter gehosteten Add-in. Beispielsweise geben Sie Localhost ein. 
    
    6. Geben Sie im **URI umleiten**die URL der vom Anbieter gehosteten Add-in. SharePoint wird Ihr Add-in zu dieser URL umleiten, nach der Autorisierung und Zustimmung eingeholt wurde. Geben Sie beispielsweise Https://localhost:44363/Home/Rückruf an. Sie können den Domänennamen abrufen und Portnummer aus der **SSL-URL** -Eigenschaft auf das Core.DynamicPermissionsWeb-Projekt in Visual Studio.
    
    7. Wählen Sie **Erstellen**. 
    
- Kopieren Sie die Client-ID und den geheimen Clientschlüssel in das **AppSettings** -Element in Core.DynamicPermissionsWeb\web.config.

## <a name="using-the-coredynamicpermissions-add-in"></a>Mithilfe des Core.DynamicPermissions-add-Ins

Wenn Sie das Codebeispiel ausführen:

1. Geben Sie in **Verbindung mit Office 365 herstellen**die URL der SharePoint-Website, der Sie auf Ihr Add-In registriert, und wählen Sie dann **Verbinden**. Geben Sie beispielsweise https://contoso.sharepoint.com.
    
2. Melden Sie sich bei Ihrem Office 365-Website.
    
3. Wenn Sie aufgefordert werden, die Erlaubnis, die Berechtigungen erteilen, die das Add-in anfordert, wählen Sie **Vertrauen**. Beachten Sie, dass Sie auf der Seite /_layouts/15/OAuthAuthorize.aspx umgeleitet werden. 
    
    > [!NOTE] 
    > Die Benutzer benötigen Berechtigungen **Verwalten** die Erlaubnis, die Berechtigungen erteilen, die das Add-in anfordert. Erfahren Sie unter [Authorization Code OAuth-Ablauf für SharePoint-Add-ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).

4. Geben Sie in **Verbindung mit Contoso**den Namen der neuen Liste zu erstellen, und wählen Sie dann auf **Liste erstellen**.
    
5. Überprüfen Sie, ob die neue Liste **Listen in Contoso**, die alle Listen angezeigt wird, die die Contoso-Website angehören, angezeigt wird. 
    
Bei der Auswahl **Verbinden** auf **Connect to Office 365** **Verbinden** in Controllers\HomeController aufgerufen wird, die und ruft dann **TokenRepository.Connect** . Die URL auf **Connect to Office 365** vom Benutzer eingegebene wird als **HostUrl**an **TokenRepository.Connect** übergeben.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
 public ActionResult Connect(string hostUrl)
        {
            TokenRepository repository = new TokenRepository(Request, Response);
            repository.Connect(hostUrl);
            return View();            
        }
```

**TokenRepository.Connect** ruft **TokenHelper.GetAuthorizationUrl** . **TokenHelper.GetAuthorizationUrl** gibt die umleitungs-URL "oauthauthorize.aspx" automatisch mithilfe der **HostUrl** und die gewünschten Berechtigungen für die SharePoint-Ressource. "Oauthauthorize.aspx" automatisch dient zum Autorisieren von Benutzern mit OAuth. Wenn an OAuthorize.aspx umgeleitet wird, muss der Benutzer zu Office 365 anmelden und stimmen Sie dann die Berechtigungen des Add-ins anfordert, oder das Add-in als vertrauenswürdig. Die gewünschte Berechtigung für die SharePoint-Ressource ist **Web.Manage** . Nach der benutzerautorisierung erstellt das Codebeispiel Listen auf der SharePoint-Website. Zum Erstellen von Listen auf einer SharePoint-Website, benötigen Benutzer **Web.Manage** Berechtigungen.

> [!NOTE] 
> **TokenHelper.GetAuthorizationUrl** gibt eine URL des Formulars **https://contoso.sharepoint.com/_layouts/15/OAuthAuthorize.aspx?IsDlg=1&amp;Client_id =<Client ID>&amp;scope=Web.Manage&amp;Response_type = Code** , wobei ** &lt;Client-ID&gt; ** wird das Add-in Client-ID Wenn das Add-in über das Seller Dashboard registriert ist, kann das Add-in einer beliebigen Office 365-Website installieren. Wenn Ihr Add-in nicht über das Seller Dashboard registriert ist, müssen Sie Registrieren Ihrer add-Ins mithilfe von "appregnew.aspx", und klicken Sie dann aktualisieren Core.DynamicPermissionsWeb\web.config. Finden Sie weitere Informationen finden Sie unter[Registrieren von SharePoint-Add-ins 2013](http://msdn.microsoft.com/library/be41a5dc-2af9-4fd9-bf4e-ad6dfa849524%28Office.15%29.aspx).

```C#
 public void Connect(string hostUrl)
        {
            if (!IsConnectedToO365)
            {
                HttpCookie spHostUrlCookie = new HttpCookie("SPHostUrl");
                spHostUrlCookie.Value = hostUrl;
                spHostUrlCookie.Expires = DateTime.Now.AddYears(5);
                _response.Cookies.Add(spHostUrlCookie);
                _response.Redirect(TokenHelper.GetAuthorizationUrl(hostUrl, "Web.Manage"));
            }
        }
```

Nach Genehmigung wird das Add-in umgeleitet an **Rückruf** in Controllers\HomeController, den umleiten URI in der appregnew.aspx angegeben. **TokenHelper** übergibt den Autorisierungscode **Code** an **Rückruf** an. Um das Zugriffstoken weiter unten in diesem Artikel beschriebenen zu erteilen, muss der Autorisierungscode **Code** an **Rückruf** zurückgegeben werden. Anschließend ruft **Rückruf** **TokenRepository.Callback** .

```C#
 public ActionResult Callback(string code)
        {
            TokenRepository repository = new TokenRepository(Request, Response);
            repository.Callback(code);
            return RedirectToAction("Index");
        }
```

**TokenRepository.Callback** ruft **TokenCache.UpdateCacheWithCode** , die **TokenHelper.GetAccessToken** verwendet, um ein OAuth-Zugriffstoken basierend auf den Autorisierungscode **Code** abzurufen.

```C#
public void Callback(string code)
        {
            HttpCookie spHostUrlCookie = _request.Cookies["SPHostUrl"];
            if (null != spHostUrlCookie)
            {
                Uri sharePointSiteUrl = new Uri(spHostUrlCookie.Value);
                TokenCache.UpdateCacheWithCode(_request, _response, sharePointSiteUrl);
            }
        }
```

```C#
 public static void UpdateCacheWithCode(HttpRequestBase request, HttpResponseBase response, Uri targetUri)
        {
            string refreshToken = TokenHelper.GetAccessToken(request.QueryString["code"], "00000003-0000-0ff1-ce00-000000000000", targetUri.Authority, TokenHelper.GetRealmFromTargetUrl(targetUri), new Uri(request.Url.GetLeftPart(UriPartial.Path))).RefreshToken;
            SetRefreshTokenCookie(response.Cookies, refreshToken);
            SetRefreshTokenCookie(request.Cookies, refreshToken);
        }
```

Ihr Add-in jetzt hat das Zugriffstoken für diesen Benutzer und zum Erstellen von Listen auf der SharePoint-Website kann fortgesetzt werden. 

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Office 365 Development Mustern und Methoden ausgesprochen](Office-365-development-patterns-and-practices-solution-guidance.md).
    
