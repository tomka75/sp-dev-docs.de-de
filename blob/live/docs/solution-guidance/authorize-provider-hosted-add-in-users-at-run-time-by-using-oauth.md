---
title: Autorisieren von vom Anbieter gehosteten-add-in Benutzern zur Laufzeit mithilfe von OAuth
ms.date: 11/03/2017
ms.openlocfilehash: 45d76f2f005361e3d8fe5ce73355b5c139e87c9e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="authorize-provider-hosted-add-in-users-at-run-time-by-using-oauth"></a><span data-ttu-id="87dae-102">Autorisieren von vom Anbieter gehosteten-add-in Benutzern zur Laufzeit mithilfe von OAuth</span><span class="sxs-lookup"><span data-stu-id="87dae-102">Authorize provider-hosted add-in users at run time by using OAuth</span></span>

<span data-ttu-id="87dae-103">Bieten Sie autorisierten Zugriff auf SharePoint-Ressourcen mithilfe von OAuth in vom Anbieter gehosteten-add-ins zur Laufzeit.</span><span class="sxs-lookup"><span data-stu-id="87dae-103">Provide authorized access to SharePoint resources by using OAuth in provider-hosted add-ins at run time.</span></span>

<span data-ttu-id="87dae-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="87dae-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="87dae-105">In der Regel greifen Ihre Benutzer SharePoint-Add-ins Öffnen einer SharePoint-Website **Auf Websiteinhalte**, klicken Sie dann auswählen und das Add-in.</span><span class="sxs-lookup"><span data-stu-id="87dae-105">Normally, your users access SharePoint add-ins by opening a SharePoint site, choosing  **Site Contents**, and then choosing the add-in.</span></span> <span data-ttu-id="87dae-106">SharePoint leitet den Benutzer auf die Remotewebsite, wo Ihre vom Anbieter gehosteten-add-in ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="87dae-106">SharePoint redirects users to the remote web where your provider-hosted add-in runs.</span></span> <span data-ttu-id="87dae-107">Da Benutzer das Add-in von SharePoint zugreifen zu können, sind Benutzer von SharePoint berechtigt, bevor sie das Add-in zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="87dae-107">Because users access the add-in from SharePoint, users are authorized by SharePoint before they can access the add-in.</span></span>

<span data-ttu-id="87dae-108">Alternativ Wenn Ihre Benutzer direkt an die URL der Ihr Add-in vom Anbieter gehosteten wechseln, muss das Add-in sie zur Laufzeit zu autorisieren mithilfe von OAuth.</span><span class="sxs-lookup"><span data-stu-id="87dae-108">Alternatively, if your users go directly to the URL of your provider-hosted add-in, that add-in must authorize them at run time by using OAuth.</span></span> <span data-ttu-id="87dae-109">In diesem Szenario muss das Add-in vom Anbieter gehosteten Autorisierung behandeln, da die Benutzer zuerst vom SharePoint autorisiert war nicht.</span><span class="sxs-lookup"><span data-stu-id="87dae-109">In this scenario, the provider-hosted add-in must handle authorization because your user wasn't authorized by SharePoint first.</span></span> <span data-ttu-id="87dae-110">Das [Core.DynamicPermissions](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) -Beispiel veranschaulicht die dynamisch Berechtigungen von einer Website mithilfe von OAuth anfordern.</span><span class="sxs-lookup"><span data-stu-id="87dae-110">The [Core.DynamicPermissions ](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) sample shows you how to dynamically request permissions from a website by using OAuth.</span></span>
<span data-ttu-id="87dae-111">Mit dieser Lösung können:</span><span class="sxs-lookup"><span data-stu-id="87dae-111">Use this solution to:</span></span>

- <span data-ttu-id="87dae-112">Autorisieren von Benutzern, die direkt an Ihr Add-in vom Anbieter gehosteten statt den Zugriff auf Ihr Add-in aus SharePoint navigieren.</span><span class="sxs-lookup"><span data-stu-id="87dae-112">Authorize users who navigate directly to your provider-hosted add-in rather than accessing your add-in from SharePoint.</span></span> <span data-ttu-id="87dae-113">Beispielsweise sollten Sie nicht die Benutzer der SharePoint-UI verwenden.</span><span class="sxs-lookup"><span data-stu-id="87dae-113">For example, you might not want your users to use the SharePoint UI.</span></span> <span data-ttu-id="87dae-114">Ihre Benutzer möglicherweise stattdessen eine vom Anbieter gehosteten-add-in verwenden, die relevante Daten aus SharePoint abgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="87dae-114">Instead, your users might use a provider-hosted add-in that shows relevant data retrieved from SharePoint.</span></span>
    
- <span data-ttu-id="87dae-115">Erstellen einer vom Anbieter gehosteten add-Ins, können Benutzer mit OAuth authentifiziert und die über den Office Store verkauft werden können.</span><span class="sxs-lookup"><span data-stu-id="87dae-115">Build a provider-hosted add-in that can authenticate users with OAuth, and that can be sold through the Office Store.</span></span>
    
## <a name="before-you-begin"></a><span data-ttu-id="87dae-116">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="87dae-116">Before you begin</span></span>

<span data-ttu-id="87dae-117">Laden Sie Sie zuerst [Core.DynamicPermissions](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="87dae-117">To get started, download the [Core.DynamicPermissions ](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="87dae-118">Bevor Sie das Codebeispiel ausführen:</span><span class="sxs-lookup"><span data-stu-id="87dae-118">Before you run the code sample:</span></span> 

- <span data-ttu-id="87dae-119">Stellen Sie sicher, dass Sie Berechtigungen **Verwalten** auf der Website verfügen.</span><span class="sxs-lookup"><span data-stu-id="87dae-119">Make sure you have  **Manage** permissions on the site.</span></span> <span data-ttu-id="87dae-120">Weitere Informationen unter [Understanding Berechtigungsstufen](https://support.office.com/article/Understanding-permission-levels-87ECBB0E-6550-491A-8826-C075E4859848).</span><span class="sxs-lookup"><span data-stu-id="87dae-120">Learn more at [Understanding permission levels](https://support.office.com/article/Understanding-permission-levels-87ECBB0E-6550-491A-8826-C075E4859848).</span></span>
    
- <span data-ttu-id="87dae-121">Registrieren Sie das Add-in auf einer SharePoint-Website mithilfe von "appregnew.aspx":</span><span class="sxs-lookup"><span data-stu-id="87dae-121">Register the add-in on a SharePoint site by using AppRegNew.aspx:</span></span> 
    
    1. <span data-ttu-id="87dae-122">Navigieren Sie zu "appregnew.aspx" auf Ihrer SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="87dae-122">Navigate to appregnew.aspx on your SharePoint site.</span></span> <span data-ttu-id="87dae-123">Angenommen, wenn Sie das add-in auf der Website contoso.sharepoint.com verwenden möchten, navigieren Sie zu http://contoso.sharepoint.com/_layouts/15/appregnew.aspx.</span><span class="sxs-lookup"><span data-stu-id="87dae-123">For example, if you want to use your add-in on the contoso.sharepoint.com site, navigate to http://contoso.sharepoint.com/_layouts/15/appregnew.aspx.</span></span>
    
    2. <span data-ttu-id="87dae-124">Wählen Sie **generieren** , um eine neue **Client-Id**zu generieren.</span><span class="sxs-lookup"><span data-stu-id="87dae-124">Choose  **Generate** to generate a new **Client id**.</span></span>
    
    3. <span data-ttu-id="87dae-125">Wählen Sie Sie **generieren** , um einen neuen **Geheimen Clientschlüssel**generieren.</span><span class="sxs-lookup"><span data-stu-id="87dae-125">Choose  **Generate** to generate a new **Client Secret**.</span></span> 
    
    4. <span data-ttu-id="87dae-126">Geben Sie einen Titel für Ihr Add-in in das Feld **Titel**ein.</span><span class="sxs-lookup"><span data-stu-id="87dae-126">Enter a title for your add-in in  **Title**.</span></span>
    
    5. <span data-ttu-id="87dae-127">Geben Sie im **Add-in - Domäne**die URL der vom Anbieter gehosteten Add-in.</span><span class="sxs-lookup"><span data-stu-id="87dae-127">In  **Add-in Domain**, enter the URL of your provider-hosted add-in.</span></span> <span data-ttu-id="87dae-128">Beispielsweise geben Sie Localhost ein.</span><span class="sxs-lookup"><span data-stu-id="87dae-128">For example, enter localhost.</span></span> 
    
    6. <span data-ttu-id="87dae-129">Geben Sie im **URI umleiten**die URL der vom Anbieter gehosteten Add-in.</span><span class="sxs-lookup"><span data-stu-id="87dae-129">In  **Redirect URI**, enter the URL of your provider-hosted add-in.</span></span> <span data-ttu-id="87dae-130">SharePoint wird Ihr Add-in zu dieser URL umleiten, nach der Autorisierung und Zustimmung eingeholt wurde.</span><span class="sxs-lookup"><span data-stu-id="87dae-130">SharePoint will redirect your add-in to this URL after authorization and consent is granted.</span></span> <span data-ttu-id="87dae-131">Geben Sie beispielsweise Https://localhost:44363/Home/Rückruf an.</span><span class="sxs-lookup"><span data-stu-id="87dae-131">For example, enter https://localhost:44363/Home/Callback.</span></span> <span data-ttu-id="87dae-132">Sie können den Domänennamen abrufen und Portnummer aus der **SSL-URL** -Eigenschaft auf das Core.DynamicPermissionsWeb-Projekt in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87dae-132">You can get the domain name and port number from the  **SSL URL** property on the Core.DynamicPermissionsWeb project in Visual Studio.</span></span>
    
    7. <span data-ttu-id="87dae-133">Wählen Sie **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="87dae-133">Choose  **Create**.</span></span> 
    
- <span data-ttu-id="87dae-134">Kopieren Sie die Client-ID und den geheimen Clientschlüssel in das **AppSettings** -Element in Core.DynamicPermissionsWeb\web.config.</span><span class="sxs-lookup"><span data-stu-id="87dae-134">Copy the Client ID and Client Secret into the  **appSettings** element in Core.DynamicPermissionsWeb\web.config.</span></span>

## <a name="using-the-coredynamicpermissions-add-in"></a><span data-ttu-id="87dae-135">Mithilfe des Core.DynamicPermissions-add-Ins</span><span class="sxs-lookup"><span data-stu-id="87dae-135">Using the Core.DynamicPermissions add-in</span></span>

<span data-ttu-id="87dae-136">Wenn Sie das Codebeispiel ausführen:</span><span class="sxs-lookup"><span data-stu-id="87dae-136">When you run the code sample:</span></span>

1. <span data-ttu-id="87dae-137">Geben Sie in **Verbindung mit Office 365 herstellen**die URL der SharePoint-Website, der Sie auf Ihr Add-In registriert, und wählen Sie dann **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="87dae-137">In  **Connect to Office 365**, enter the URL of the SharePoint site that you registered your add-in on, and then choose  **Connect**.</span></span> <span data-ttu-id="87dae-138">Geben Sie beispielsweise https://contoso.sharepoint.com.</span><span class="sxs-lookup"><span data-stu-id="87dae-138">For example, enter https://contoso.sharepoint.com.</span></span>
    
2. <span data-ttu-id="87dae-139">Melden Sie sich bei Ihrem Office 365-Website.</span><span class="sxs-lookup"><span data-stu-id="87dae-139">Sign in to your Office 365 site.</span></span>
    
3. <span data-ttu-id="87dae-140">Wenn Sie aufgefordert werden, die Erlaubnis, die Berechtigungen erteilen, die das Add-in anfordert, wählen Sie **Vertrauen**.</span><span class="sxs-lookup"><span data-stu-id="87dae-140">If you are asked to grant consent to the permissions the add-in is requesting, choose  **Trust It**.</span></span> <span data-ttu-id="87dae-141">Beachten Sie, dass Sie auf der Seite /_layouts/15/OAuthAuthorize.aspx umgeleitet werden.</span><span class="sxs-lookup"><span data-stu-id="87dae-141">Notice that you are redirected to the /_layouts/15/OAuthAuthorize.aspx page.</span></span> 
    
    > [!NOTE] 
    > <span data-ttu-id="87dae-142">Die Benutzer benötigen Berechtigungen **Verwalten** die Erlaubnis, die Berechtigungen erteilen, die das Add-in anfordert.</span><span class="sxs-lookup"><span data-stu-id="87dae-142">Your user must have  **Manage** permissions to grant consent to the permissions the add-in is requesting.</span></span> <span data-ttu-id="87dae-143">Erfahren Sie unter [Authorization Code OAuth-Ablauf für SharePoint-Add-ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="87dae-143">You can learn more at [Authorization Code OAuth flow for SharePoint Add-ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span></span>

4. <span data-ttu-id="87dae-144">Geben Sie in **Verbindung mit Contoso**den Namen der neuen Liste zu erstellen, und wählen Sie dann auf **Liste erstellen**.</span><span class="sxs-lookup"><span data-stu-id="87dae-144">In  **Successfully connected to Contoso**, enter the name of a new list to create, and then choose  **Create List**.</span></span>
    
5. <span data-ttu-id="87dae-145">Überprüfen Sie, ob die neue Liste **Listen in Contoso**, die alle Listen angezeigt wird, die die Contoso-Website angehören, angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="87dae-145">Verify that  **Lists in Contoso**, which shows all the lists that belong to the Contoso site, shows your new list.</span></span> 
    
<span data-ttu-id="87dae-146">Bei der Auswahl **Verbinden** auf **Connect to Office 365** **Verbinden** in Controllers\HomeController aufgerufen wird, die und ruft dann **TokenRepository.Connect** .</span><span class="sxs-lookup"><span data-stu-id="87dae-146">When choosing  **Connect** on **Connect to Office 365**,  **Connect** in Controllers\HomeController.cs is called, which then calls **TokenRepository.Connect** .</span></span> <span data-ttu-id="87dae-147">Die URL auf **Connect to Office 365** vom Benutzer eingegebene wird als **HostUrl**an **TokenRepository.Connect** übergeben.</span><span class="sxs-lookup"><span data-stu-id="87dae-147">The URL entered by the user on **Connect to Office 365** is passed to **TokenRepository.Connect** as **hostUrl**.</span></span>

> [!NOTE] 
> <span data-ttu-id="87dae-148">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="87dae-148">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
 public ActionResult Connect(string hostUrl)
        {
            TokenRepository repository = new TokenRepository(Request, Response);
            repository.Connect(hostUrl);
            return View();            
        }
```

<span data-ttu-id="87dae-149">**TokenRepository.Connect** ruft **TokenHelper.GetAuthorizationUrl** .</span><span class="sxs-lookup"><span data-stu-id="87dae-149">**TokenRepository.Connect** calls **TokenHelper.GetAuthorizationUrl** .</span></span> <span data-ttu-id="87dae-150">**TokenHelper.GetAuthorizationUrl** gibt die umleitungs-URL "oauthauthorize.aspx" automatisch mithilfe der **HostUrl** und die gewünschten Berechtigungen für die SharePoint-Ressource.</span><span class="sxs-lookup"><span data-stu-id="87dae-150">**TokenHelper.GetAuthorizationUrl** returns the redirect URL to OAuthAuthorize.aspx using the **hostUrl** and the desired permissions on the SharePoint resource.</span></span> <span data-ttu-id="87dae-151">"Oauthauthorize.aspx" automatisch dient zum Autorisieren von Benutzern mit OAuth.</span><span class="sxs-lookup"><span data-stu-id="87dae-151">OAuthAuthorize.aspx is used to authorize users using OAuth.</span></span> <span data-ttu-id="87dae-152">Wenn an OAuthorize.aspx umgeleitet wird, muss der Benutzer zu Office 365 anmelden und stimmen Sie dann die Berechtigungen des Add-ins anfordert, oder das Add-in als vertrauenswürdig.</span><span class="sxs-lookup"><span data-stu-id="87dae-152">When redirected to OAuthorize.aspx, the user must sign in to Office 365, and then consent to the permissions the add-in is requesting, or trust the add-in.</span></span> <span data-ttu-id="87dae-153">Die gewünschte Berechtigung für die SharePoint-Ressource ist **Web.Manage** .</span><span class="sxs-lookup"><span data-stu-id="87dae-153">The desired permission on the SharePoint resource is **Web.Manage** .</span></span> <span data-ttu-id="87dae-154">Nach der benutzerautorisierung erstellt das Codebeispiel Listen auf der SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="87dae-154">After user authorization, the code sample creates lists on the SharePoint site.</span></span> <span data-ttu-id="87dae-155">Zum Erstellen von Listen auf einer SharePoint-Website, benötigen Benutzer **Web.Manage** Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="87dae-155">To create lists on a SharePoint site, users must have **Web.Manage** permissions.</span></span>

> [!NOTE] 
> <span data-ttu-id="87dae-156">**TokenHelper.GetAuthorizationUrl** gibt eine URL des Formulars **https://contoso.sharepoint.com/_layouts/15/OAuthAuthorize.aspx?IsDlg=1&amp;Client_id =<Client ID>&amp;scope=Web.Manage&amp;Response_type = Code** , wobei ** &lt;Client-ID&gt; ** wird das Add-in Client-ID</span><span class="sxs-lookup"><span data-stu-id="87dae-156">**TokenHelper.GetAuthorizationUrl** returns a URL of the form **https://contoso.sharepoint.com/_layouts/15/OAuthAuthorize.aspx?IsDlg=1&amp;client_id=<Client ID>&amp;scope=Web.Manage&amp;response_type=code** , where **&lt;Client ID&gt;** is the add-in's Client ID.</span></span> <span data-ttu-id="87dae-157">Wenn das Add-in über das Seller Dashboard registriert ist, kann das Add-in einer beliebigen Office 365-Website installieren.</span><span class="sxs-lookup"><span data-stu-id="87dae-157">If your add-in is registered through the Seller Dashboard, any Office 365 site can install the add-in.</span></span> <span data-ttu-id="87dae-158">Wenn Ihr Add-in nicht über das Seller Dashboard registriert ist, müssen Sie Registrieren Ihrer add-Ins mithilfe von "appregnew.aspx", und klicken Sie dann aktualisieren Core.DynamicPermissionsWeb\web.config. Finden Sie weitere Informationen finden Sie unter[Registrieren von SharePoint-Add-ins 2013](http://msdn.microsoft.com/library/be41a5dc-2af9-4fd9-bf4e-ad6dfa849524%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="87dae-158">If your add-in is not registered through the Seller Dashboard, you must register your add-in by using appregnew.aspx, and then update Core.DynamicPermissionsWeb\web.config. To learn more, see[Register SharePoint Add-ins 2013](http://msdn.microsoft.com/library/be41a5dc-2af9-4fd9-bf4e-ad6dfa849524%28Office.15%29.aspx).</span></span>

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

<span data-ttu-id="87dae-159">Nach Genehmigung wird das Add-in umgeleitet an **Rückruf** in Controllers\HomeController, den umleiten URI in der appregnew.aspx angegeben.</span><span class="sxs-lookup"><span data-stu-id="87dae-159">After authorization, the add-in is redirected to  **Callback** in Controllers\HomeController.cs, which is the Redirect URI specified on the appregnew.aspx.</span></span> <span data-ttu-id="87dae-160">**TokenHelper** übergibt den Autorisierungscode **Code** an **Rückruf** an.</span><span class="sxs-lookup"><span data-stu-id="87dae-160">**TokenHelper** passes the authorization code, **code** , to **Callback** .</span></span> <span data-ttu-id="87dae-161">Um das Zugriffstoken weiter unten in diesem Artikel beschriebenen zu erteilen, muss der Autorisierungscode **Code** an **Rückruf** zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="87dae-161">To grant the access token described later in this article, the authorization code, **code** , must be returned to **Callback** .</span></span> <span data-ttu-id="87dae-162">Anschließend ruft **Rückruf** **TokenRepository.Callback** .</span><span class="sxs-lookup"><span data-stu-id="87dae-162">**Callback** then calls **TokenRepository.Callback** .</span></span>

```C#
 public ActionResult Callback(string code)
        {
            TokenRepository repository = new TokenRepository(Request, Response);
            repository.Callback(code);
            return RedirectToAction("Index");
        }
```

<span data-ttu-id="87dae-163">**TokenRepository.Callback** ruft **TokenCache.UpdateCacheWithCode** , die **TokenHelper.GetAccessToken** verwendet, um ein OAuth-Zugriffstoken basierend auf den Autorisierungscode **Code** abzurufen.</span><span class="sxs-lookup"><span data-stu-id="87dae-163">**TokenRepository.Callback** calls **TokenCache.UpdateCacheWithCode** , which uses **TokenHelper.GetAccessToken** to obtain an OAuth access token based on the authorization code, **code** .</span></span>

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

<span data-ttu-id="87dae-164">Ihr Add-in jetzt hat das Zugriffstoken für diesen Benutzer und zum Erstellen von Listen auf der SharePoint-Website kann fortgesetzt werden.</span><span class="sxs-lookup"><span data-stu-id="87dae-164">Your add-in now has the access token for this user and can proceed to create lists on the SharePoint site.</span></span> 

## <a name="see-also"></a><span data-ttu-id="87dae-165">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="87dae-165">See also</span></span>
<span data-ttu-id="87dae-166"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="87dae-166"></span></span>

- <span data-ttu-id="87dae-167">[Office 365 Development Mustern und Methoden ausgesprochen](Office-365-development-patterns-and-practices-solution-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="87dae-167">[Office 365 development patterns and practices solution guidance](Office-365-development-patterns-and-practices-solution-guidance.md).</span></span>
    
