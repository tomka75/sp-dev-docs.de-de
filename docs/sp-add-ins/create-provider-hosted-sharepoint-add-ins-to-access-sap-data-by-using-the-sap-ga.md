---
title: "Erstellen von vom Anbieter gehosteten SharePoint-Add-Ins zum Zugreifen auf SAP-Daten mithilfe des SAP-Gateway für Microsoft"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d32e94567b67e3f3acdfb042daa6a9de68c5209f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="create-provider-hosted-sharepoint-add-ins-to-access-sap-data-by-using-the-sap-gateway-for-microsoft"></a>Erstellen von vom Anbieter gehosteten SharePoint-Add-Ins für den Zugriff auf SAP-Daten mithilfe des SAP-Gateway für Microsoft
Erfahren Sie, wie Sie ein SharePoint-Add-In erstellen, das auf SAP-Daten zugreifen kann.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 

Sie können ein SharePoint-Add-In erstellen, das SAP-Daten und optional SharePoint-Daten liest und schreibt, indem Sie das SAP-Gateway für Microsoft und die Azure AD-Authentifizierungsbibliothek für .NET verwenden. In diesem Artikel werden Sie die Verfahren für das Entwerfen des SharePoint-Add-Ins für einen autorisierten Zugriff auf SAP beschrieben. 
 

## <a name="before-you-begin"></a>Bevor Sie beginnen

Für die in diesem Artikel beschriebenen Verfahren müssen die folgenden erforderlichen Komponenten vorhanden sein:
 

 

-  **Eine Website für Office 365-Entwickler** in einer Office 365-Domain, die mit einem Microsoft Azure Active Directory-Abonnement verknüpft ist. Weitere Informationen finden Sie unter [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) oder [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription.md).
    
 
-  **Visual Studio 2013 Update 2** oder höher, das Sie unter [Willkommen bei Visual Studio 2013](http://msdn.microsoft.com/library/dd831853.aspx) abrufen können.
    
 
-  **Microsoft Office Developer Tools für Visual Studio**. Die Version, die in Update 2 von Visual Studio 2013 oder höher enthalten ist.
    
 
-  **SAP-Gateway für Microsoft** wird in Microsoft Azure bereitgestellt und konfiguriert. Weitere Informationen finden Sie in der Dokumentation zum [SAP-Gateway für Microsoft](http://go.microsoft.com/fwlink/?LinkId=507635).
    
 
-  **Ein Organisationskonto in Microsoft Azure**Informationen finden Sie unter [Manually register your app with Azure AD so it can access Office 365 APIs](http://msdn.microsoft.com/library/95479f73-15d7-426e-abdf-ae2c72b5cd33%28Office.15%29.aspx#bk_CreateOrganizationAccount).
    
     **Hinweis** Melden Sie sich bei Ihrem Office 365-Konto an (login.microsoftonline.com), um das temporäre Kennwort zu ändern, nachdem das Konto erstellt wurde.
-  **Ein SAP-OData-Endpunkt** mit Beispieldaten. Weitere Informationen finden Sie in der Dokumentation zum [SAP-Gateway für Microsoft](http://go.microsoft.com/fwlink/?LinkId=507635).
    
 
-  **Grundkenntnisse zu Azure AD.** Weitere Informationen finden Sie unter [Erste Schritte mit Azure AD](http://msdn.microsoft.com/library/azure/dn655157.aspx).
    
 
-  **Grundkenntnisse in der Erstellung von SharePoint-Add-Ins.** Weitere Informationen finden Sie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).
    
 
-  **Grundkenntnisse zu OAuth 2.0 in Azure AD**. Weitere Informationen finden Sie unter [OAuth 2.0 in Azure AD](http://msdn.microsoft.com/library/azure/dn645545.aspx) und den untergeordneten Themen.
    
 
 **Codebeispiel:** [SharePoint: Verwenden des SAP-Gateway für Microsoft in einem SharePoint-Add-In](http://code.msdn.microsoft.com/SharePoint-Using-the-0931abce)
 

 

## <a name="understand-authentication-and-authorization-to-sap-gateway-for-microsoft-and-sharepoint"></a>Grundlegendes zur Authentifizierung und Autorisierung beim SAP-Gateway für Microsoft und SharePoint
<a name="AuthOverview"> </a>

Mit OAuth 2.0 in Azure AD können Anwendungen auf mehrere Ressourcen zugreifen, die von Microsoft Azure gehostet werden, und SAP-Gateway für Microsoft ist eine davon. Mit OAuth 2.0 sind Anwendungen, zusätzlich zu Benutzern, Sicherheitsprinzipale. Für Anwendungsprinzipale ist eine Authentifizierung und Autorisierung bei geschützten Ressourcen zusätzlich zu (und manchmal anstelle von) Benutzern erforderlich. Der Prozess beinhaltet einen OAuth-"Ablauf", bei dem die Anwendung, die ein SharePoint-Add-In sein kann, ein Zugriffstoken (und Aktualisierungstoken) abruft, das von allen von Microsoft Azure gehosteten Diensten und Anwendungen akzeptiert wird, die für die Verwendung von Azure AD als OAuth 2.0-Autorisierungsserver konfiguriert sind. Der Prozess ähnelt der Art und Weise, wie die Remotekomponenten eines von einem Anbieter gehostetes SharePoint-Add-In eine Autorisierung für SharePoint erhalten, wie in  [Erstellen von SharePoint-Add-Ins, die die Autorisierung mit niedriger Vertrauensebene verwenden](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) und den untergeordneten Artikeln beschrieben. Das ACS-Autorisierungssystem verwendet jedoch Microsoft Azure Access Control Service (ACS) anstelle von Azure AD als vertrauenswürdigen Tokenherausgeber.
 

 

 **Tipp** Wenn Ihr SharePoint-Add-In außer auf das SAP-Gateway für Microsoft auf SharePoint zugreift, muss es *beide* Systeme verwenden: Azure AD, um ein Zugriffstoken für das SAP-Gateway für Microsoft abzurufen, und das ACS-Autorisierungssystem, um ein Zugriffstoken für SharePoint abzurufen. Die Token aus den zwei Quellen sind nicht austauschbar. Weitere Informationen finden Sie unter [Optionales Hinzufügen eines Zugriffs auf SharePoint zur ASP.NET-Anwendung](#SharePoint).
 

Eine ausführliche Beschreibung und ein Diagramm zu dem in OAuth 2.0 verwendeten OAuth-Ablauf in Azure AD finden Sie unter  [Ablauf für die Gewährung eines Autorisierungscodes](http://msdn.microsoft.com/library/azure/dn645542.aspx). (Eine ähnliche Beschreibung und ein Diagramm für den Ablauf beim Zugriff auf SharePoint finden Sie unter  [Die einzelnen Schritte des Kontexttokenablaufs](context-token-oauth-flow-for-sharepoint-add-ins.md#OAuth_ProcessFlowSteps).)
 

 

## <a name="create-the-sharepoint-add-in"></a>Erstellen des SharePoint-Add-Ins
<a name="AuthOverview"> </a>


### <a name="create-the-visual-studio-solution"></a>Erstellen der Visual Studio-Projektmappe


1. Erstellen Sie ein **SharePoint-Add-In**-Projekt in Visual Studio mit den folgenden Schritten. (Für das fortlaufende Beispiel in diesem Artikel wird davon ausgegangen, die Sie C# verwenden. Sie können ein SharePoint-Add-In-Projekt aber auch im Abschnitt **Visual Basic** der Vorlagen für neue Projekte starten.)
    
      1. Geben Sie im Assistenten **Neues SharePoint-Add-In** einen Namen für das Projekt ein, und klicken Sie auf **OK**. Verwenden Sie für das fortlaufende Beispiel den Namen „SAP2SharePoint“.
    
 
  2. Geben Sie die Domänen-URL Ihrer Office 365-Entwicklerwebsite (einschließlich eines abschließenden Schrägstrichs) als Debugging-Website an, z. B. „https://<O365_Domäne>.sharepoint.com/“. Geben Sie **Von Anbieter gehostet** als Add-In-Typ an. Klicken Sie auf **Weiter**.
    
 
  3. Wählen Sie einen Projekttyp aus. Wählen Sie für das fortlaufende Beispiel **ASP.NET Web Forms-Anwendung**. (Sie können auch ASP.NET-MVC-Anwendungen erstellen, die auf das SAP-Gateway für Microsoft zugreifen.) Klicken Sie auf **Weiter**.
    
 
  4. Wählen Sie Azure ACS als Authentifizierungssystem aus. (Ihr SharePoint-Add-In verwendet dieses System, wenn es auf SharePoint zugreift. Es verwendet das System nicht, wenn es auf das SAP-Gateway für Microsoft zugreift.) Klicken Sie auf **Fertig stellen**.
    
 
2. Nachdem das Projekt erstellt ist, werden Sie aufgefordert, sich beim Office 365-Konto anzumelden. Verwenden Sie die Anmeldeinformationen eines Kontoadministrators, z. B. Bob@<O365_domain>.onmicrosoft.com.
    
 
3. Die Visual Studio-Projektmappe enthält zwei Projekte: das eigentliche SharePoint-Add-In-Projekt und ein ASP.NET Web Forms-Projekt. Fügen Sie mit den folgenden Schritten das Paket der **Active Directory-Authentifizierungsbibliothek** (ADAL) zum ASP.NET-Projekt hinzu:
    
      1. Klicken Sie mit der rechten Maustaste auf den Ordner **Referenzen** im ASP.NET-Projekt (mit dem Namen **SAP2SharePointWeb** im fortlaufenden Beispiel), und wählen Sie **NuGet-Pakete verwalten** aus. 
    
 
  2. Wählen Sie im daraufhin geöffneten Dialogfeld auf der linken Seite **Online** aus. Geben Sie „Microsoft.IdentityModel.Clients.ActiveDirectory“ in das Suchfeld ein.
    
 
  3. Wenn die ADAL-Bibliothek in den Suchergebnissen angezeigt wird, klicken Sie auf die Schaltfläche **Installieren** daneben, und akzeptieren Sie die Lizenz, wenn Sie dazu aufgefordert werden.
    
 
4. Fügen Sie das Json.net-Paket mit den folgenden Schritten zum ASP.NET-Projekt hinzu:
    
      1. Geben Sie „Json.net“ in das Suchfeld ein. Wenn dies zu viele Treffer zurückgibt, suchen Sie stattdessen nach „onNewtonsoft.json“.
    
 
  2. Wenn „Json.net“ in den Suchergebnissen angezeigt wird, klicken Sie auf die Schaltfläche **Installieren** daneben.
    
 
5. Klicken Sie auf **Schließen**.
    
 

### <a name="register-your-web-application-with-azure-ad"></a>Registrieren Ihrer Webanwendung bei Azure AD


1. Melden Sie sich mit Ihrem Azure-Administratorkonto beim [Azure-Verwaltungsportal](https://manage.windowsazure.com) an.
    
     **Hinweis** Aus Sicherheitsgründen wird empfohlen, bei der Entwicklung von Add-Ins kein Administratorkonto zu verwenden.
2. Wählen Sie auf der linken Seite **Active Directory** aus.
    
 
3. Klicken Sie auf Ihr Verzeichnis. 
    
 
4. Wählen Sie **ANWENDUNGEN** (in der obersten Navigationsleiste) aus.
    
 
5. Wählen Sie in der Symbolleiste am unteren Rand des Bildschirms **Hinzufügen** aus.
    
 
6. Wählen Sie im daraufhin geöffneten Dialogfeld **Eine Anwendung hinzufügen, die meine Organisation entwickelt**.
    
 
7. Geben Sie der Anwendung im Dialogfeld **ANWENDUNG HINZUFÜGEN** einen Namen. Verwenden Sie für das fortlaufende Beispiel den Namen „ContosoAutomobileCollection“. 
    
 
8. Wählen Sie **Webanwendung und/oder Web-API** als Anwendungstyp aus, und klicken Sie dann auf den Pfeil nach rechts.
    
 
9. Verwenden Sie auf der zweiten Seite des Dialogfelds die SSL-Debugging-URL aus dem ASP.NET-Projekt in der Visual Studio-Projektmappe als **ANMELDE-URL**. Sie finden die URL mit den folgenden Schritten. ***(Sie müssen das Add-In anfangs bei der Debugging-URL registrieren, damit Sie den Visual Studio-Debugger (F5) ausführen können. Wenn Ihr Add-In für das Staging bereit ist, registrieren Sie es erneut bei der zugehörigen Azure-Website-Staging-URL. [Ändern Sie das Add-In, und stellen Sie es für Azure und Office 365 bereit](#Stage).)***
    
      1. Markieren Sie das ASP.NET-Projekt im **Projektmappen-Explorer**. 
    
 
  2. Kopieren Sie im Fenster **Eigenschaften** den Wert der Eigenschaft **SSL-URL**. Ein Beispiel ist „https://localhost:44300/“.
    
 
  3. Fügen Sie ihn in das Feld **ANMELDE-URL** im Dialogfeld **ANWENDUNG HINZUFÜGEN** ein.
    
 
10. Weisen Sie der Anwendung im Feld **APP-ID-URI** einen eindeutigen URI zu, wie den an das Ende der SSL-URL angehängten Anwendungsnamen, z. B. https://localhost:44300/ContosoAutomobileCollection.
    
 
11. Klicken Sie auf die Schaltfläche mit dem Häkchen. Das Azure-Dashboard für die Anwendung wird mit einer Erfolgsmeldung geöffnet.
    
 
12. Wählen Sie im oberen Bereich der Seite **KONFIGURIEREN** aus.
    
 
13. Scrollen Sie zu **CLIENT-ID**, und erstellen Sie eine Kopie der ID. Diese benötigen Sie für ein späteres Verfahren.
    
 
14. Erstellen Sie im Abschnitt **Schlüssel** einen Schlüssel. Dieser wird anfangs nicht angezeigt. Klicken Sie im unteren Bereich der Seite auf **SPEICHERN**, damit der Schlüssel sichtbar wird. Erstellen Sie eine Kopie des Schlüssels. Diese benötigen Sie für ein späteres Verfahren.
    
 
15. Scrollen Sie zu **Berechtigungen für andere Anwendungen**, und wählen Sie Ihre SAP-Gateway für Microsoft-Dienstanwendung aus.
    
 
16. Öffnen Sie die Dropdownliste **Delegierte Berechtigungen**, und aktivieren Sie die Kontrollkästchen für die Berechtigungen für den SAP-Gateway für Microsoft-Dienst, die Ihr SharePoint-Add-In benötigt.
    
 
17. Klicken Sie unten im Bildschirm auf **SPEICHERN**.
    
 

### <a name="configure-the-application-to-communicate-with-azure-ad"></a>Konfigurieren der Anwendung für die Kommunikation mit Azure AD


1. Öffnen Sie in Visual Studio die Datei „web.config“ im ASP.NET-Projekt.
    
 
2. Im Abschnitt  `<appSettings>` verfügen die Office-Entwicklertools für Visual Studio über hinzugefügte Elemente für **ClientID** und **ClientSecret** des SharePoint-Add-In. (Diese werden im Azure ACS-Autorisierungssystem verwendet, wenn die ASP.NET-Anwendung auf SharePoint zugreift. Sie können diese für das fortlaufende Beispiel ignorieren, sollten sie aber nicht löschen. Sie sind in vom Anbieter gehosteten SharePoint-Add-Ins erforderlich, selbst wenn die App nicht auf SharePoint-Daten zugreift. Ihre Werte ändern sich jedes Mal, wenn Sie F5 in Visual Studio drücken.) Fügen Sie die folgenden zwei Elemente zum Abschnitt hinzu. Diese werden von der Anwendung für die Authentifizierung bei Azure AD verwendet. (Denken Sie daran, dass Anwendungen und Benutzer in OAuth-basierten Authentifizierungs- und Autorisierungssystemen Sicherheitsprinzipale sind.)
    
```
  <add key="ida:ClientID" value="" />
<add key="ida:ClientKey" value="" />
```

3. Geben Sie die Client-ID, die Sie in einem früheren Schritt aus Ihrem Azure AD-Verzeichnis gespeichert haben, als Wert des Schlüssels **ida:ClientID** ein. Behalten Sie Groß-/Kleinschreibung und Satzzeichen exakt so bei, wie Sie sie kopiert haben, und achten Sie darauf, am Anfang oder Ende des Werts kein Leerzeichen einzufügen. Verwenden Sie als **ida:ClientKey**-Schlüssel den *Schlüssel*, den Sie aus dem Verzeichnis gespeichert haben. Achten Sie auch hier darauf, keine Leerzeichen einzufügen oder den Wert auf irgendeine Weise zu ändern. Der Abschnitt `<appSettings>` sollte jetzt ungefähr wie das folgende Beispiel aussehen. (Der Wert **ClientId** enthält möglicherweise eine GUID oder eine leere Zeichenfolge.)
    
```
  <appSettings>
  <add key="ClientId" value="" />
  <add key="ClientSecret" value="LypZu2yVajlHfPLRn5J2hBrwCk5aBOHxE4PtKCjIQkk=" />
  <add key="ida:ClientID" value="4da99afe-08b5-4bce-bc66-5356482ec2df" />
  <add key="ida:ClientKey" value="URwh/oiPay/b5jJWYHgkVdoE/x7gq3zZdtcl/cG14ss=" />
</appSettings>
```


     **Note**  Your application is known to Azure AD by the "localhost" URL you used to register it. The client ID and client key are associated with that identity. When you are ready to stage your application to an Azure Web Site, you will re-register it with a new URL.
4. Fügen Sie weiterhin im Bereich **appSettings** einen **Authority**-Schlüssel hinzu, und legen Sie seinen Wert auf die Office 365-Domäne ( *beliebige_Domäne*.onmicrosoft.com) Ihres Organisationskontos fest. Im fortlaufenden Beispiel ist das Organisationskonto „Bob@<O365_domain>.onmicrosoft.com“, deshalb ist die Autorität `<O365_domain>.onmicrosoft.com`. 
    
```
  <add key="Authority" value="<O365_domain>.onmicrosoft.com" />
```

5. Fügen Sie immer noch im Abschnitt **appSettings** einen **AppRedirectUrl**-Schlüssel hinzu, und legen Sie seinen Wert auf die Seite fest, auf die der Browser des Benutzers umgeleitet werden soll, nachdem das ASP.NET-Add-In einen Autorisierungscode von Azure AD erhalten hat. Normalerweise ist dies dieselbe Seite, auf der sich der Benutzer befand, als der Aufruf an Azure AD stattfand. Im fortlaufenden Beispiel verwenden Sie den SSL-URL-Wert, an den Sie „/Pages/Default.aspx“ anhängen, wie unten gezeigt. (Dies ist ein weiterer Wert, den Sie für das Staging verändern werden.)
    
```
  <add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />
```

6. Fügen Sie weiterhin im Abschnitt **appSettings** einen **ResourceUrl**-Schlüssel hinzu, und legen Sie seinen Wert auf den APP-ID-URI des SAP-Gateway für Microsoft fest (*nicht* den APP-ID-URI Ihrer ASP.NET-Anwendung). Sie erhalten diesen Wert vom SAP-Gateway für Microsoft-Administrator. Im Folgenden sehen Sie ein Beispiel.
    
```
  <add key="ResourceUrl" value="http://<SAP_gateway_domain>.cloudapp.net/" />
```


    The  `<appSettings>` section should now look something like this:
    


```
  <appSettings>
  <add key="ClientId" value="06af1059-8916-4851-a271-2705e8cf53c6" />
  <add key="ClientSecret" value="LypZu2yVajlHfPLRn5J2hBrwCk5aBOHxE4PtKCjIQkk=" />
  <add key="ida:ClientID" value="4da99afe-08b5-4bce-bc66-5356482ec2df" />
  <add key="ida:ClientKey" value="URwh/oiPay/b5jJWYHgkVdoE/x7gq3zZdtcl/cG14ss=" />
  <add key="Authority" value="<O365_domain>.onmicrosoft.com" />
  <add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />
  <add key="ResourceUrl" value="http://<SAP_gateway_domain>.cloudapp.net/" />
</appSettings>
```

7. Speichern und schließen Sie die Datei „web.config“.
    
     **Tipp** Lassen Sie die Datei „web.config“ nicht geöffnet, während Sie den Visual Studio-Debugger (F5) ausführen. Die Office Developer Tools für Visual Studio ändern den **ClientId**-Wert (nicht die **ida:ClientID**) jedes Mal, wenn Sie F5 drücken. Daher müssen Sie auf eine Aufforderung zum erneuten Laden der Datei „web.config“ reagieren, wenn sie geöffnet ist, bevor das Debugging ausgeführt werden kann.

### <a name="add-a-helper-class-to-authenticate-to-azure-ad"></a>Hinzufügen einer Hilfsklasse zur Authentifizierung bei Azure-AD


1. Klicken Sie mit der rechten Maustaste auf das ASP.NET-Projekt, und verwenden Sie das Visual Studio-Verfahren zum Hinzufügen von Elementen, um dem Projekt eine neue Klassendatei mit dem Namen „AADAuthHelper.cs“ hinzuzufügen.
    
 
2. Fügen Sie der Datei die folgenden **using**-Anweisungen hinzu.
    
```
  using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using System.Web.UI;

```

3. Ändern Sie das Zugriffsschlüsselwort von **public** in **internal**, und fügen Sie das **static**-Schlüsselwort zur Klassendeklaration hinzu.
    
```
  internal static class AADAuthHelper
```

4. Fügen Sie der Klasse die folgenden Felder hinzu. In diesen Feldern werden Informationen gespeichert, die die ASP.NET-Anwendung zum Abrufen von Zugriffstoken von AAD verwendet.
    
```
  private static readonly string _authority = ConfigurationManager.AppSettings["Authority"];
private static readonly string _appRedirectUrl = ConfigurationManager.AppSettings["AppRedirectUrl"];
private static readonly string _resourceUrl = ConfigurationManager.AppSettings["ResourceUrl"];     
private static readonly string _clientId = ConfigurationManager.AppSettings["ida:ClientID"];        
private static readonly ClientCredential _clientCredential = new ClientCredential(
                           ConfigurationManager.AppSettings["ida:ClientID"],
                           ConfigurationManager.AppSettings["ida:ClientKey"]);

private static readonly AuthenticationContext _authenticationContext = 
            new AuthenticationContext("https://login.windows.net/common/" + 
                                      ConfigurationManager.AppSettings["Authority"]);
```

5. Fügen Sie der Klasse die folgende Eigenschaft hinzu. Diese Eigenschaft hält die URL zum Azure AD-Anmeldebildschirm.
    
```
  private static string AuthorizeUrl
{
    get
    {
        return string.Format("https://login.windows.net/{0}/oauth2/authorize?response_type=code&amp;redirect_uri={1}&amp;client_id={2}&amp;state={3}",
            _authority,
            _appRedirectUrl,
            _clientId,
            Guid.NewGuid().ToString());
    }
}

```

6. Fügen Sie der Klasse die folgenden Eigenschaften hinzu. Diese speichern das Zugriffs- und Aktualisierungstoken zwischen und überprüfen ihre Gültigkeit.
    
```
  public static Tuple<string, DateTimeOffset> AccessToken
{
    get {
return HttpContext.Current.Session["AccessTokenWithExpireTime-" + _resourceUrl] 
       as Tuple<string, DateTimeOffset>;
    }

    set { HttpContext.Current.Session["AccessTokenWithExpireTime-" + _resourceUrl] = value; }
}

private static bool IsAccessTokenValid
{
   get 
   { 
       return AccessToken != null &amp;&amp;
       !string.IsNullOrEmpty(AccessToken.Item1) &amp;&amp;
       AccessToken.Item2 > DateTimeOffset.UtcNow;
   }
}

private static string RefreshToken
{
    get { return HttpContext.Current.Session["RefreshToken" + _resourceUrl] as string; }
    set { HttpContext.Current.Session["RefreshToken-" + _resourceUrl] = value; }
}

private static bool IsRefreshTokenValid
{
    get { return !string.IsNullOrEmpty(RefreshToken); }
}

```

7. Fügen Sie der Klasse die folgenden Methoden hinzu. Diese werden verwendet, um die Gültigkeit des Autorisierungscodes zu überprüfen und ein Zugriffstoken von Azure AD zu erhalten, indem entweder ein Authentifizierungscode oder ein Aktualisierungstoken verwendet wird.
    
```
  private static bool IsAuthorizationCodeNotNull(string authCode)
{
    return !string.IsNullOrEmpty(authCode);
}

private static Tuple<Tuple<string,DateTimeOffset>,string> AcquireTokensUsingAuthCode(string authCode)
{
    var authResult = _authenticationContext.AcquireTokenByAuthorizationCode(
                authCode,
                new Uri(_appRedirectUrl),
                _clientCredential,
                _resourceUrl);

    return new Tuple<Tuple<string, DateTimeOffset>, string>(
                new Tuple<string, DateTimeOffset>(authResult.AccessToken, authResult.ExpiresOn), 
                authResult.RefreshToken);
}

private static Tuple<string, DateTimeOffset> RenewAccessTokenUsingRefreshToken()
{
    var authResult = _authenticationContext.AcquireTokenByRefreshToken(
                         RefreshToken,
                         _clientCredential.OwnerId,
                         _clientCredential,
                         _resourceUrl);

    return new Tuple<string, DateTimeOffset>(authResult.AccessToken, authResult.ExpiresOn);
}

```

8. Fügen Sie der Klasse die folgende Methode hinzu. Sie wird vom ASP.NET-Code dahinter aufgerufen, um ein gültiges Zugriffstoken zu erhalten, bevor ein Aufruf zum Abrufen von SAP-Daten über SAP-Gateway für Microsoft erfolgt.
    
```
  internal static void EnsureValidAccessToken(Page page)
{
    if (IsAccessTokenValid) 
    {
        return;
    }
    else if (IsRefreshTokenValid) 
    {
        AccessToken = RenewAccessTokenUsingRefreshToken();
        return;
    }
    else if (IsAuthorizationCodeNotNull(page.Request.QueryString["code"]))
    {
        Tuple<Tuple<string, DateTimeOffset>, string> tokens = null;
        try
        {
            tokens = AcquireTokensUsingAuthCode(page.Request.QueryString["code"]);
        }
        catch 
        {
            page.Response.Redirect(AuthorizeUrl);
        }
        AccessToken = tokens.Item1;
        RefreshToken = tokens.Item2;
        return;
    }
    else
    {
        page.Response.Redirect(AuthorizeUrl);
    }
}
```


 **Tipp** Die AADAuthHelper-Klasse bietet nur eine minimale Fehlerbehandlung. Für ein robustes SharePoint-Add-In in Produktionsqualität fügen Sie mehr Fehlerbehandlung hinzu, wie im folgenden MSDN-Knoten beschrieben: [Fehlerbehandlung in OAuth 2.0](http://msdn.microsoft.com/library/561bf289-3ff9-4eea-b165-4f5f02bcc520.aspx).
 


### <a name="create-data-model-classes"></a>Erstellen von Datenmodellklassen


1. Erstellen Sie eine oder mehrere Klassen, um die Daten zu modellieren, die Ihre App von SAP abruft. Im fortlaufenden Beispiel gibt es nur eine Datenmodellklasse. Klicken Sie mit der rechten Maustaste auf das ASP.NET-Projekt, und verwenden Sie den Visual Studio-Prozess zum Hinzufügen von Elementen, um eine neue Klassendatei zum Projekt mit dem Namen Automobile.cs hinzuzufügen.
    
 
2. Fügen Sie den folgenden Code zum Textteil der Klasse hinzu:
    
```
  public string Price;
public string Brand;
public string Model;
public int Year;
public string Engine;
public int MaxPower;
public string BodyStyle;
public string Transmission;
```


### <a name="add-code-behind-to-get-data-from-sap-via-the-sap-gateway-for-microsoft"></a>Hinzufügen des zugrunde liegenden Codes, um Daten über das SAP-Gateway für Microsoft aus SAP abzurufen


1. Öffnen Sie die Datei „Default.aspx.cs“, und fügen Sie die folgenden **using**-Anweisungen hinzu.
    
```
  using System.Net;
using Newtonsoft.Json.Linq;
```

2. Fügen Sie eine **const**-Deklaration zur Default-Klasse hinzu, deren Wert die Basis-URL des SAP-OData-Endpunkts ist, auf den das Add-In zugreift. Im Folgenden ist ein Beispiel dargestellt:
    
```
  private const string SAP_ODATA_URL = @"https://<SAP_gateway_domain>.cloudapp.net:8081/perf/sap/opu/odata/sap/ZCAR_POC_SRV/";
```

3. Die Office Developer Tools für Visual Studio haben eine **Page_PreInit**-Methode und eine **Page_Load**-Methode hinzugefügt. Kommentieren Sie den Code in der **Page_Load**-Methode und die gesamte **Page_Init**-Methode aus. Dieser Code wird im Beispiel nicht verwendet. (Wenn Ihr SharePoint-Add-In auf SharePoint zugreifen wird, stellen Sie diesen Code wieder her. Informationen finden Sie unter [Optionales Hinzufügen eines Zugriffs auf SharePoint zur ASP.NET-Anwendung](#SharePoint).)
    
 
4. Fügen Sie die folgende Zeile im oberen Bereich der **Page_Load**-Methode hinzu. Damit wird der Debugging-Prozess vereinfacht, da Ihre ASP.NET-Anwendung über SSL (HTTPS) mit dem SAP-Gateway für Microsoft kommuniziert. Ihr „localhost:port“-Server ist aber nicht so konfiguriert, dass er dem Zertifikat des SAP-Gateway für Microsoft vertraut. Mit dieser Codezeile würden Sie eine Warnung zu einem ungültigen Zertifikat erhalten, bevor „Default.aspx“ geöffnet wird. In einigen Browsern können Sie diesen Fehler einfach wegklicken, aber in anderen können Sie „Default.aspx“ gar nicht öffnen.
    
```
  ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;
```


     **Important**  Delete this line when you are ready to deploy the ASP.NET application to staging. See  [Modify the add-in and stage it to Azure and Office 365](#Stage).
1. Fügen Sie der **Page_Load**-Methode den folgenden Code hinzu. Die an die `GetSAPData`-Methode übergebene Zeichenfolge ist eine OData-Abfrage.
    
```
  if (!IsPostBack)
{
    GetSAPData("DataCollection?$top=3");
}

```

6. Fügen Sie die folgende Methode zur Default-Klasse hinzu. Diese Methode stellt zunächst sicher, dass der Cache für das Zugriffstoken ein gültiges Zugriffstoken enthält, das von Azure AD abgerufen wurde. Dann erstellt sie eine HTTP **GET**-Anforderung, die das Zugriffstoken enthält, und sendet diese an den SAP-OData-Endpunkt. Das Ergebnis wird als JSON-Objekt zurückgegeben, das in ein .NET **List**-Objekt konvertiert wird. Drei Eigenschaften der Elemente werden in einem Array verwendet, das an **DataListView** gebunden ist.
    
```
  private void GetSAPData(string oDataQuery)
{
    AADAuthHelper.EnsureValidAccessToken(this);

    using (WebClient client = new WebClient())
    {
        client.Headers[HttpRequestHeader.Accept] = "application/json";
        client.Headers[HttpRequestHeader.Authorization] = "Bearer " + AADAuthHelper.AccessToken.Item1;
        var jsonString = client.DownloadString(SAP_ODATA_URL + oDataQuery);
        var jsonValue = JObject.Parse(jsonString)["d"]["results"];
        var dataCol = jsonValue.ToObject<List<Automobile>>();

        var dataList = dataCol.Select((item) => {
            return item.Brand + " " + item.Model + " " + item.Price;
            }).ToArray();

        DataListView.DataSource = dataList;
        DataListView.DataBind();
    }
}

```


### <a name="create-the-user-interface"></a>Erstellen der Benutzeroberfläche


1. Öffnen Sie die „Datei Default.aspx“, und fügen Sie dem **form**-Element der Seite das folgende Markup hinzu:
    
```
  <div>
  <h3>Data from SAP via SAP Gateway for Microsoft</h3>

  <asp:ListView runat="server" ID="DataListView">
    <ItemTemplate>
      <tr runat="server">
        <td runat="server">
          <asp:Label ID="DataLabel" runat="server"
            Text="<%# Container.DataItem.ToString()%>" /><br />
        </td>
      </tr>
    </ItemTemplate>
  </asp:ListView>
</div>
```

2. Geben Sie der Webseite optional das Erscheinungsbild einer SharePoint-Seite, indem Sie das SharePoint [-Chromsteuerelement](use-the-client-chrome-control-in-sharepoint-add-ins.md) und [das Stylesheet der Host-SharePoint-Website](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md) verwenden.
    
 

### <a name="test-the-add-in-with-f5-in-visual-studio"></a>Testen des Add-Ins mit F5 in Visual Studio


1. Drücken Sie in Visual Studio F5.
    
 
2. Wenn Sie F5 zum ersten Mal verwenden, werden Sie möglicherweise aufgefordert, sich bei der Website für Entwickler anzumelden, die Sie verwenden. Benutzen Sie dafür die Anmeldeinformationen des Websiteadministrators. Im fortlaufenden Beispiel ist das Bob@<O365_domain>.onmicrosoft.com.
    
 
3. Wenn Sie F5 zum ersten Mal verwenden, werden Sie aufgefordert, dem Add-In Berechtigungen zu gewähren. Klicken Sie auf **Vertrauen**.
    
 
4. Nach einer kurzen Verzögerung, während der das Zugriffstoken abgerufen wird, wird die Seite „Default.aspx“ geöffnet. Stellen Sie sicher, dass die SAP-Daten angezeigt werden.
    
 

## <a name="optionally-add-sharepoint-access-to-the-aspnet-application"></a>Optional können Sie der ASP.NET-Anwendung SharePoint-Zugriff hinzufügen.
<a name="SharePoint"> </a>

Natürlich muss Ihr SharePoint-Add-In nicht nur SAP-Daten auf einer von SharePoint gestarteten Webseite anzeigen. Es kann auch SharePoint-Daten erstellen, lesen, aktualisieren und löschen. Ihr zugrunde liegender Code kann dafür entweder das SharePoint-Clientobjektmodell (CSOM) oder die REST-APIs von SharePoint verwenden. Das CSOM wird als Assemblypaar bereitgestellt, das die Office Developer Tools für Visual Studio automatisch in das ASP.NET-Projekt eingefügt und auf **Lokale Kopie** in Visual Studio festgelegt haben, damit es im ASP.NET-Anwendungspaket enthalten ist. Weitere Informationen zum Verwenden von CSOM finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](complete-basic-operations-using-sharepoint-client-library-code.md). Informationen zum Verwenden der REST-APIs finden Sie unter [Erläuterungen zur REST-Schnittstelle von SharePoint und zu ihrer Verwendung](http://msdn.microsoft.com/de-DE/magazine/dn198245.aspx). 
 

 
Unabhängig davon, ob Sie CSOM oder die REST-APIs für den Zugriff auf SharePoint verwenden, muss Ihre ASP.NET-Anwendung ein Zugriffstoken für SharePoint abrufen, ebenso wie für das SAP-Gateway für Microsoft. Weitere Informationen finden Sie unter  [Verstehen der Authentifizierung und Autorisierung beim SAP-Gateway für Microsoft und SharePoint](#AuthOverview) weiter oben. Das Verfahren unten stellt einige grundlegende Anweisungen zur entsprechenden Vorgehensweise bereit, aber wir empfehlen, dass Sie zunächst die folgenden Artikel lesen:
 

 

-  [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
-  [Autorisierung und Authentifizierung für Add-Ins in SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md)
    
 
-  [Drei Autorisierungssysteme für SharePoint-Add-Ins](three-authorization-systems-for-sharepoint-add-ins.md)
    
 
-  [Erstellen von SharePoint-Add-Ins, die die Autorisierung mit niedriger Vertrauensebene verwenden](creating-sharepoint-add-ins-that-use-low-trust-authorization.md)
    
 
-  [OAuth-Ablauf mit Kontexttoken für SharePoint-Add-In](context-token-oauth-flow-for-sharepoint-add-ins.md)
    
 

1. Öffnen Sie die Datei „Default.aspx.cs“, und kommentieren Sie die **Page_PreInit**-Methode aus. Kommentieren Sie außerdem den Code aus, den die Office Developer Tools für Visual Studio zur **Page_Load**-Methode hinzugefügt haben.
    
 
2. Wenn Ihr SharePoint-Add-In auf SharePoint-Daten zugreifen wird, müssen Sie das SharePoint-Kontexttoken zwischenspeichern, das beim Starten des Add-Ins in SharePoint an die Seite „Default.aspx“ übertragen wurde. Damit wird sichergestellt, dass das SharePoint-Kontexttoken nicht verloren geht, wenn der Browser nach der Azure AD-Authentifizierung umgeleitet wird. (Sie haben mehrere Optionen für das Zwischenspeichern dieses Kontexts.) Die Office Developer Tools für Visual Studio fügen eine SharePointContext.cs-Datei zum ASP.NET-Projekt hinzu, die den größten Teil der Arbeit übernimmt. Zum Verwenden des Sitzungscaches fügen Sie einfach den folgenden Code in den Block „`if (!IsPostBack)`“ *vor* dem Code ein, der den Aufruf an das SAP-Gateway für Microsoft durchführt:
    
```
  if (HttpContext.Current.Session["SharePointContext"] == null) 
{
     HttpContext.Current.Session["SharePointContext"]
        = SharePointContextProvider.Current.GetSharePointContext(Context);
}
```

3. Die Datei „SharePointContext.cs“ sendet Aufrufe an eine andere Datei, die die Office Developer Tools für Visual Studio zum Projekt hinzugefügt haben: TokenHelper.cs. Diese Datei stellt den größten Teil des Codes bereit, der erforderlich ist, um Zugriffstoken für SharePoint abzurufen und zu verwenden. Sie stellt jedoch keinen Code für das Erneuern eines abgelaufenen Zugriffstoken oder Aktualisierungstoken bereit. Sie enthält außerdem keinen Code zum Zwischenspeichern von Token. Für ein SharePoint-Add-In in Produktionsqualität benötigen Sie solchen Code. Die Zwischenspeicherlogik im vorherigen Schritt ist ein Beispiel. Ihr Code sollte außerdem das Zugriffstoken zwischenspeichern und es wiederverwenden, bis es abgelaufen ist. Wenn das Zugriffstoken abgelaufen ist, sollte Ihr Code das Aktualisierungstoken verwenden, um ein neues Zugriffstoken abzurufen.
    
 
4. Fügen Sie die Datenaufrufe an SharePoint entweder über CSOM oder REST hinzu. Im folgenden Beispiel wurde CSOM-Code geändert, den die Office Developer Tools für Visual Studio zur **Page_Load**-Methode hinzufügen. In diesem Beispiel wurde der Code in eine separate Methode verschoben und beginnt mit dem Abrufen des zwischengespeicherten Kontexttokens.
    
```
  private void GetSharePointTitle()
{
    var spContext = HttpContext.Current.Session["SharePointContext"] as SharePointContext;
    using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        clientContext.Load(clientContext.Web, web => web.Title);
        clientContext.ExecuteQuery();
        SharePointTitle.Text = "SharePoint web site title is: " + clientContext.Web.Title;
    }
}
```

5. Fügen Sie die Benutzeroberflächenelemente zum Rendern der SharePoint-Daten hinzu. Nachfolgend sehen Sie das HTML-Steuerelement, auf das in der vorstehenden Methode verwiesen wird:
    
```
  <h3>SharePoint title</h3><asp:Label ID="SharePointTitle" runat="server"></asp:Label><br />
```


 **Hinweis** Während Sie das SharePoint-Add-In debuggen, wird es von den Office Developer Tools für Visual Studio jedes Mal erneut bei Azure ACS registriert, wenn Sie F5 in Visual Studio drücken. Wenn Sie das SharePoint-Add-In bereitstellen, müssen Sie ihm eine langfristige Registrierung geben. Weitere Informationen finden Sie im Abschnitt [Ändern des Add-Ins und Bereitstellen für Azure und Office 365](#Stage).
 


## <a name="modify-the-add-in-and-stage-it-to-azure-and-office-365"></a>Ändern des Add-Ins und Bereitstellen für Azure und Office 365
<a name="Stage"> </a>

Wenn Sie das Debugging des SharePoint-Add-In mit F5 in Visual Studio abgeschlossen haben, müssen Sie die ASP.NET-Anwendung an eine tatsächliche Azure-Website bereitstellen.
 

 

### <a name="create-the-azure-web-site"></a>Erstellen der Azure-Website


1. Öffnen Sie im Microsoft Azure-Portal in der linken Navigationsleiste den Eintrag **WEBSITES**.
    
 
2. Klicken Sie im unteren Bereich der Seite auf **NEU**, und wählen Sie im Dialogfeld **NEU** die Option **WEBSITE** |**SCHNELLERFASSUNG** aus.
    
 
3. Geben Sie einen Domänennamen ein, und klicken Sie auf **WEBSITE ERSTELLEN**. Kopieren Sie die URL der neuen Website. Diese hat das Format `my_domain.azurewebsites.net`.
    
 

### <a name="modify-the-code-and-markup-in-the-application"></a>Ändern des Codes und Markups in der Anwendung


1. Entfernen Sie in Visual Studio die Zeile `ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;` aus der Datei „Default.aspx.cs“.
    
 
2. Öffnen Sie die Datei „web.config“ des ASP.NET-Projekts, und ändern Sie den Domänenteil des Werts für den **AppRedirectUrl**-Schlüssel im Abschnitt **appSettings** in die Domäne der Azure-Website. Ändern Sie beispielsweise `<add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />` in `<add key="AppRedirectUrl" value="https://my_domain.azurewebsites.net/Pages/Default.aspx" />`.
    
 
3. Klicken Sie mit der rechten Maustaste auf die Datei AppManifest.xml im SharePoint-Add-In-Projekt, und wählen Sie **Code anzeigen** aus.
    
 
4. Ersetzen Sie im Wert **StartPage** die Zeichenfolge `~remoteAppUrl` durch die vollständige Domäne der Azure-Website, einschließlich Protokoll, z. B. `https://my_domain.azurewebsites.net`. Der gesamte **StartPage**-Wert sollte jetzt wie folgt aussehen: `https://my_domain.azurewebsites.net/Pages/Default.aspx`. (Normalerweise ist der **StartPage**-Wert identisch mit dem Wert des **AppRedirectUrl**-Schlüssels in der Datei „web.config“.)
    
 

### <a name="modify-the-aad-registration-and-register-the-add-in-with-acs"></a>Ändern der AAD-Registrierung und Registrieren des Add-Ins bei ACS


1. Melden Sie sich mit Ihrem Azure-Administratorkonto beim [Azure-Verwaltungsportal](https://manage.windowsazure.com) an.
    
 
2. Wählen Sie auf der linken Seite **Active Directory** aus.
    
 
3. Klicken Sie auf Ihr Verzeichnis.
    
 
4. Wählen Sie **ANWENDUNGEN** (in der obersten Navigationsleiste) aus.
    
 
5. Öffnen Sie die von Ihnen erstellte Anwendung. Im fortlaufenden Beispiel ist das **ContosoAutomobileCollection**.
    
 
6. Ändern Sie für jeden der folgenden Werte den Teil „localhost:*port*“ des Werts in die Domäne Ihrer neuen Azure-Website:
    
      -  **ANMELDE-URL**
    
 
  -  **APP-ID-URI**
    
 
  -  **ANTWORT-URL**
    
 

    Wenn beispielsweise der **APP-ID-URI****https://localhost:44304/ContosoAutomobileCollection** ist, ändern Sie ihn in **https://<my_domain>.azurewebsites.net/ContosoAutomobileCollection**.
    
 
7. Klicken Sie unten im Bildschirm auf **SPEICHERN**.
    
 
8. Sie das Add-In bei Azure ACS. Dies muss auch dann durchgeführt werden, wenn das Add-In nicht auf SharePoint zugreift und keine Token von ACS verwendet, da derselbe Prozess das Add-In auch beim App-Verwaltungsdienst des Office 365-Abonnements registriert, was erforderlich ist. (Er wird als „App-Verwaltungsdienst“ bezeichnet, da SharePoint-Add-Ins ursprünglich „Apps für SharePoint“ hießen). Sie führen die Registrierung auf der Seite „AppRegNew.aspx“ einer beliebigen SharePoint-Website im Office 365-Abonnement durch. Ausführliche Informationen finden Sie unter [Registrieren von SharePoint-Add-Ins 2013](register-sharepoint-add-ins.md). Im Rahmen dieses Prozesses erhalten Sie eine neue Client-ID und einen neuen geheimen Clientschlüssel. Geben Sie diese Werte in die Datei „web.config“ für die Schlüssel **ClientId** (nicht **ida:ClientID**) und **ClientSecret** ein.
    
     **Vorsicht** Wenn Sie aus irgendeinem Grund nach dieser Änderung F5 drücken, überschreiben die Office Developer Tools für Visual Studio einen oder beide dieser Werte. Aus diesem Grund sollten Sie die mit „AppRegNew.aspx“ abgerufenen Werte aufzeichnen und immer sicherstellen, dass die Werte in der „web.config“ korrekt sind, kurz bevor Sie die ASP.NET-Anwendung veröffentlichen. 

### <a name="publish-the-aspnet-application-to-azure-and-install-the-add-in-to-sharepoint"></a>Veröffentlichen der ASP.NET-Anwendung in Azure und Installieren des SharePoint-Add-Ins


1. Es gibt verschiedene Möglichkeiten, eine ASP.NET-Anwendung an eine Azure-Website zu veröffentlichen. Weitere Informationen finden Sie unter  [Bereitstellen einer Azure-Website](http://azure.microsoft.com/de-DE/documentation/articles/web-sites-deploy/).
    
 
2. Klicken Sie in Visual Studio mit der rechten Maustaste auf das SharePoint-Add-In-Projekt, und wählen Sie **Paket** aus. Klicken Sie auf der sich öffnenden Seite **Add-In veröffentlichen** auf **Add-In verpacken**. Der Datei-Explorer öffnet sich im Ordner mit dem Add-In-Paket.
    
 
3. Melden Sie sich bei Office 365 als globaler Administrator an, und navigieren Sie zur App-Katalog-Websitesammlung der Organisation. (Falls keine vorhanden ist, erstellen Sie eine. Informationen finden Sie unter  [Verwenden des App-Katalogs zur Bereitstellung von benutzerdefinierten Geschäfts-Apps für Ihre SharePoint Online-Umgebung](http://office.microsoft.com/de-DE/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).)
    
 
4. Laden Sie das Add-In in den Add-In-Katalog hoch.
    
 
5. Navigieren Sie zur Seite **Websiteinhalt** einer beliebigen Website im Abonnement, und klicken Sie auf **Add-In hinzufügen**.
    
 
6. Scrollen Sie auf der Seite **Ihre Add-Ins** zum Abschnitt **Add-Ins, die Sie hinzufügen können**, und klicken Sie auf das Symbol für Ihr Add-In.
    
 
7. Nachdem das Add-In installiert wurde, klicken Sie auf das zugehörige Symbol auf der Seite **Websiteinhalt**, um das Add-In zu starten.
    
 
Unter [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) finden Sie weitere Informationen über die Installation von SharePoint-Add-Ins.
 

## <a name="deploying-the-add-in-to-production"></a>Bereitstellen des Add-Ins an die Produktion
<a name="Stage"> </a>

Wenn Sie alle Tests abgeschlossen haben, können Sie das Add-In in Produktion bereitstellen. Dafür sind möglicherweise einige Änderungen erforderlich.
 

 

1. Wenn die Produktionsdomäne der ASP.NET-Anwendung eine andere als die Stagingdomäne ist, müssen Sie den **AppRedirectUrl**-Wert in der Datei „web.config“ und den **StartPage**-Wert in der Datei „AppManifest.xml“ ändern und das SharePoint-Add-In erneut packen. Informationen dazu finden Sie im Verfahren **Ändern des Codes und Markups in der Anwendung** weiter oben.
    
 
2. Durch die Domänenänderung müssen Sie außerdem die Add-In-Registrierung bei AAD ändern. Informationen dazu finden Sie im Verfahren **Ändern der AAD-Registrierung und Registrieren des Add-Ins bei ACS** weiter oben.
    
 
3. Durch die Domänenänderung müssen Sie zudem das Add-In erneut bei ACS (und dem App-Verwaltungsdienst des Abonnements) registrieren, wie im selben Verfahren beschrieben wird. (Es gibt keine Möglichkeit, die Registrierung eines Add-Ins bei ACS zu *bearbeiten*.) Es ist allerdings nicht erforderlich, eine neue Client-ID oder einen neuen geheimen Clientschlüssel auf der Seite „AppRegNew.aspx“ zu generieren. Sie können die ursprünglichen Werte aus den Schlüsseln **ClientId** (nicht **ida:ClientID**) und **ClientSecret** der „web.config“ in das AppRegNew-Formular kopieren. *Wenn Sie neue Werte generieren, achten Sie darauf, dass Sie die neuen Werte in die Schlüssel in der „web.config“ kopieren.* 
    
 

