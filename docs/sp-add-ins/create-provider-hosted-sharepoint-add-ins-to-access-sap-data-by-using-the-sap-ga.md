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
# <a name="create-provider-hosted-sharepoint-add-ins-to-access-sap-data-by-using-the-sap-gateway-for-microsoft"></a><span data-ttu-id="51715-102">Erstellen von vom Anbieter gehosteten SharePoint-Add-Ins für den Zugriff auf SAP-Daten mithilfe des SAP-Gateway für Microsoft</span><span class="sxs-lookup"><span data-stu-id="51715-102">Create provider-hosted SharePoint Add-ins to access SAP data by using the SAP Gateway for Microsoft</span></span>
<span data-ttu-id="51715-103">Erfahren Sie, wie Sie ein SharePoint-Add-In erstellen, das auf SAP-Daten zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="51715-103">Learn how you can build a SharePoint Add-in that can access SAP data.</span></span>
 

 <span data-ttu-id="51715-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="51715-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="51715-p102">Sie können ein SharePoint-Add-In erstellen, das SAP-Daten und optional SharePoint-Daten liest und schreibt, indem Sie das SAP-Gateway für Microsoft und die Azure AD-Authentifizierungsbibliothek für .NET verwenden. In diesem Artikel werden Sie die Verfahren für das Entwerfen des SharePoint-Add-Ins für einen autorisierten Zugriff auf SAP beschrieben.</span><span class="sxs-lookup"><span data-stu-id="51715-p102">You can create a SharePoint Add-in that reads and writes SAP data, and optionally reads and writes SharePoint data, by using SAP Gateway for Microsoft and the Azure AD Authentication Library for .NET. This article provides the procedures for how you can design the SharePoint Add-in to get authorized access to SAP.</span></span> 
 

## <a name="before-you-begin"></a><span data-ttu-id="51715-109">Bevor Sie beginnen</span><span class="sxs-lookup"><span data-stu-id="51715-109">Before you begin</span></span>

<span data-ttu-id="51715-110">Für die in diesem Artikel beschriebenen Verfahren müssen die folgenden erforderlichen Komponenten vorhanden sein:</span><span class="sxs-lookup"><span data-stu-id="51715-110">The following are prerequisites to the procedures in this article:</span></span>
 

 

-  <span data-ttu-id="51715-p103">**Eine Website für Office 365-Entwickler** in einer Office 365-Domain, die mit einem Microsoft Azure Active Directory-Abonnement verknüpft ist. Weitere Informationen finden Sie unter [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) oder [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="51715-p103">**An Office 365 Developer Site** in an Office 365 domain that is associated with a Microsoft Azure Active Directory subscription. See [Set up a development environment for SharePoint Add-ins on Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) or [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span>
    
 
-  <span data-ttu-id="51715-113">**Visual Studio 2013 Update 2** oder höher, das Sie unter [Willkommen bei Visual Studio 2013](http://msdn.microsoft.com/library/dd831853.aspx) abrufen können.</span><span class="sxs-lookup"><span data-stu-id="51715-113">**Visual Studio 2013 Update 2** or later, which you can obtain from [Welcome to Visual Studio 2013](http://msdn.microsoft.com/library/dd831853.aspx).</span></span>
    
 
-  <span data-ttu-id="51715-p104">**Microsoft Office Developer Tools für Visual Studio**. Die Version, die in Update 2 von Visual Studio 2013 oder höher enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="51715-p104">**Microsoft Office Developer Tools for Visual Studio**. The version that is included in Update 2 of Visual Studio 2013 or later.</span></span>
    
 
-  <span data-ttu-id="51715-p105">**SAP-Gateway für Microsoft** wird in Microsoft Azure bereitgestellt und konfiguriert. Weitere Informationen finden Sie in der Dokumentation zum [SAP-Gateway für Microsoft](http://go.microsoft.com/fwlink/?LinkId=507635).</span><span class="sxs-lookup"><span data-stu-id="51715-p105">**SAP Gateway for Microsoft** is deployed and configured in Microsoft Azure. See the documentation for [SAP Gateway for Microsoft](http://go.microsoft.com/fwlink/?LinkId=507635).</span></span>
    
 
-  <span data-ttu-id="51715-p106">**Ein Organisationskonto in Microsoft Azure**Informationen finden Sie unter [Manually register your app with Azure AD so it can access Office 365 APIs](http://msdn.microsoft.com/library/95479f73-15d7-426e-abdf-ae2c72b5cd33%28Office.15%29.aspx#bk_CreateOrganizationAccount).</span><span class="sxs-lookup"><span data-stu-id="51715-p106">**An organizational account in Microsoft Azure**. See  [Manually register your app with Azure AD so it can access Office 365 APIs](http://msdn.microsoft.com/library/95479f73-15d7-426e-abdf-ae2c72b5cd33%28Office.15%29.aspx#bk_CreateOrganizationAccount).</span></span>
    
     <span data-ttu-id="51715-120">**Hinweis** Melden Sie sich bei Ihrem Office 365-Konto an (login.microsoftonline.com), um das temporäre Kennwort zu ändern, nachdem das Konto erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="51715-120">**Note**  Login to your Office 365 account (login.microsoftonline.com) to change the temporary password after the account is created.</span></span>
-  <span data-ttu-id="51715-p107">**Ein SAP-OData-Endpunkt** mit Beispieldaten. Weitere Informationen finden Sie in der Dokumentation zum [SAP-Gateway für Microsoft](http://go.microsoft.com/fwlink/?LinkId=507635).</span><span class="sxs-lookup"><span data-stu-id="51715-p107">**A SAP OData endpoint** with sample data in it. See the documentation for [SAP Gateway for Microsoft](http://go.microsoft.com/fwlink/?LinkId=507635).</span></span>
    
 
-  <span data-ttu-id="51715-p108">**Grundkenntnisse zu Azure AD.** Weitere Informationen finden Sie unter [Erste Schritte mit Azure AD](http://msdn.microsoft.com/library/azure/dn655157.aspx).</span><span class="sxs-lookup"><span data-stu-id="51715-p108">**A basic familiarity with Azure AD.** See [Getting started with Azure AD](http://msdn.microsoft.com/library/azure/dn655157.aspx).</span></span>
    
 
-  <span data-ttu-id="51715-125">**Grundkenntnisse in der Erstellung von SharePoint-Add-Ins.** Weitere Informationen finden Sie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="51715-125">**A basic familiarity with creating SharePoint Add-ins.** See [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>
    
 
-  <span data-ttu-id="51715-p109">**Grundkenntnisse zu OAuth 2.0 in Azure AD**. Weitere Informationen finden Sie unter [OAuth 2.0 in Azure AD](http://msdn.microsoft.com/library/azure/dn645545.aspx) und den untergeordneten Themen.</span><span class="sxs-lookup"><span data-stu-id="51715-p109">**A basic familiarity OAuth 2.0 in Azure AD**. See  [OAuth 2.0 in Azure AD](http://msdn.microsoft.com/library/azure/dn645545.aspx) and its child topics.</span></span>
    
 
 <span data-ttu-id="51715-128">**Codebeispiel:** [SharePoint: Verwenden des SAP-Gateway für Microsoft in einem SharePoint-Add-In](http://code.msdn.microsoft.com/SharePoint-Using-the-0931abce)</span><span class="sxs-lookup"><span data-stu-id="51715-128">**Code sample:** [SharePoint: Using the SAP Gateway to Microsoft in a SharePoint Add-in](http://code.msdn.microsoft.com/SharePoint-Using-the-0931abce)</span></span>
 

 

## <a name="understand-authentication-and-authorization-to-sap-gateway-for-microsoft-and-sharepoint"></a><span data-ttu-id="51715-129">Grundlegendes zur Authentifizierung und Autorisierung beim SAP-Gateway für Microsoft und SharePoint</span><span class="sxs-lookup"><span data-stu-id="51715-129">Understand authentication and authorization to SAP Gateway for Microsoft and SharePoint</span></span>
<span data-ttu-id="51715-130"><a name="AuthOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="51715-130"></span></span>

<span data-ttu-id="51715-p110">Mit OAuth 2.0 in Azure AD können Anwendungen auf mehrere Ressourcen zugreifen, die von Microsoft Azure gehostet werden, und SAP-Gateway für Microsoft ist eine davon. Mit OAuth 2.0 sind Anwendungen, zusätzlich zu Benutzern, Sicherheitsprinzipale. Für Anwendungsprinzipale ist eine Authentifizierung und Autorisierung bei geschützten Ressourcen zusätzlich zu (und manchmal anstelle von) Benutzern erforderlich. Der Prozess beinhaltet einen OAuth-"Ablauf", bei dem die Anwendung, die ein SharePoint-Add-In sein kann, ein Zugriffstoken (und Aktualisierungstoken) abruft, das von allen von Microsoft Azure gehosteten Diensten und Anwendungen akzeptiert wird, die für die Verwendung von Azure AD als OAuth 2.0-Autorisierungsserver konfiguriert sind. Der Prozess ähnelt der Art und Weise, wie die Remotekomponenten eines von einem Anbieter gehostetes SharePoint-Add-In eine Autorisierung für SharePoint erhalten, wie in  [Erstellen von SharePoint-Add-Ins, die die Autorisierung mit niedriger Vertrauensebene verwenden](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) und den untergeordneten Artikeln beschrieben. Das ACS-Autorisierungssystem verwendet jedoch Microsoft Azure Access Control Service (ACS) anstelle von Azure AD als vertrauenswürdigen Tokenherausgeber.</span><span class="sxs-lookup"><span data-stu-id="51715-p110">OAuth 2.0 in Azure AD enables applications to access multiple resources hosted by Microsoft Azure and SAP Gateway for Microsoft is one of them. With OAuth 2.0, applications, in addition to users, are security principals. Application principals require authentication and authorization to protected resources in addition to (and sometimes instead of) users. The process involves an OAuth "flow" in which the application, which can be a SharePoint Add-in, obtains an access token (and refresh token) that is accepted by all of the Microsoft Azure-hosted services and applications that are configured to use Azure AD as an OAuth 2.0 authorization server. The process is very similar to the way that the remote components of a provider-hosted SharePoint Add-in gets authorization to SharePoint as described in  [Creating SharePoint Add-ins that use low-trust authorization](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) and its child articles. However, the ACS authorization system uses Microsoft Azure Access Control Service (ACS) as the trusted token issuer rather than Azure AD.</span></span>
 

 

 <span data-ttu-id="51715-p111">**Tipp** Wenn Ihr SharePoint-Add-In außer auf das SAP-Gateway für Microsoft auf SharePoint zugreift, muss es *beide* Systeme verwenden: Azure AD, um ein Zugriffstoken für das SAP-Gateway für Microsoft abzurufen, und das ACS-Autorisierungssystem, um ein Zugriffstoken für SharePoint abzurufen. Die Token aus den zwei Quellen sind nicht austauschbar. Weitere Informationen finden Sie unter [Optionales Hinzufügen eines Zugriffs auf SharePoint zur ASP.NET-Anwendung](#SharePoint).</span><span class="sxs-lookup"><span data-stu-id="51715-p111">**Tip**  If your SharePoint Add-in accesses SharePoint in addition to accessing SAP Gateway for Microsoft, then it will need to use  *both*  systems: Azure AD to get an access token to SAP Gateway for Microsoft and the ACS authorization system to get an access token to SharePoint. The tokens from the two sources are not interchangeable. For more information, see [Optionally, add SharePoint access to the ASP.NET application](#SharePoint).</span></span>
 

<span data-ttu-id="51715-p112">Eine ausführliche Beschreibung und ein Diagramm zu dem in OAuth 2.0 verwendeten OAuth-Ablauf in Azure AD finden Sie unter  [Ablauf für die Gewährung eines Autorisierungscodes](http://msdn.microsoft.com/library/azure/dn645542.aspx). (Eine ähnliche Beschreibung und ein Diagramm für den Ablauf beim Zugriff auf SharePoint finden Sie unter  [Die einzelnen Schritte des Kontexttokenablaufs](context-token-oauth-flow-for-sharepoint-add-ins.md#OAuth_ProcessFlowSteps).)</span><span class="sxs-lookup"><span data-stu-id="51715-p112">For a detailed description and diagram of the OAuth flow used by OAuth 2.0 in Azure AD, see  [Authorization Code Grant Flow](http://msdn.microsoft.com/library/azure/dn645542.aspx). (For a similar description, and a diagram, of the flow for accessing SharePoint, see  [See the steps in the Context Token flow](context-token-oauth-flow-for-sharepoint-add-ins.md#OAuth_ProcessFlowSteps).)</span></span>
 

 

## <a name="create-the-sharepoint-add-in"></a><span data-ttu-id="51715-142">Erstellen des SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="51715-142">Create the SharePoint Add-in</span></span>
<span data-ttu-id="51715-143"><a name="AuthOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="51715-143"></span></span>


### <a name="create-the-visual-studio-solution"></a><span data-ttu-id="51715-144">Erstellen der Visual Studio-Projektmappe</span><span class="sxs-lookup"><span data-stu-id="51715-144">Create the Visual Studio solution</span></span>


1. <span data-ttu-id="51715-p113">Erstellen Sie ein **SharePoint-Add-In**-Projekt in Visual Studio mit den folgenden Schritten. (Für das fortlaufende Beispiel in diesem Artikel wird davon ausgegangen, die Sie C# verwenden. Sie können ein SharePoint-Add-In-Projekt aber auch im Abschnitt **Visual Basic** der Vorlagen für neue Projekte starten.)</span><span class="sxs-lookup"><span data-stu-id="51715-p113">Create an  **SharePoint Add-in** project in Visual Studio with the following steps. (The continuing example in this article assumes you are using C#; but you can start a SharePoint Add-in project in the **Visual Basic** section of the new project templates as well.)</span></span>
    
      1. <span data-ttu-id="51715-p114">Geben Sie im Assistenten **Neues SharePoint-Add-In** einen Namen für das Projekt ein, und klicken Sie auf **OK**. Verwenden Sie für das fortlaufende Beispiel den Namen „SAP2SharePoint“.</span><span class="sxs-lookup"><span data-stu-id="51715-p114">In the  **New SharePoint Add-in** wizard, name the project and click **OK**. For the continuing example, use SAP2SharePoint.</span></span>
    
 
  2. <span data-ttu-id="51715-p115">Geben Sie die Domänen-URL Ihrer Office 365-Entwicklerwebsite (einschließlich eines abschließenden Schrägstrichs) als Debugging-Website an, z. B. „https://<O365_Domäne>.sharepoint.com/“. Geben Sie **Von Anbieter gehostet** als Add-In-Typ an. Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="51715-p115">Specify the domain URL of your Office 365 Developer Site (including a final forward slash) as the debugging site; for example, https://<O365_domain>.sharepoint.com/. Specify  **Provider-hosted** as the add-in type. Click **Next**.</span></span>
    
 
  3. <span data-ttu-id="51715-p116">Wählen Sie einen Projekttyp aus. Wählen Sie für das fortlaufende Beispiel **ASP.NET Web Forms-Anwendung**. (Sie können auch ASP.NET-MVC-Anwendungen erstellen, die auf das SAP-Gateway für Microsoft zugreifen.) Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="51715-p116">Choose a project type. For the continuing example, choose  **ASP.NET Web Forms Application**. (You can also make ASP.NET MVC applications that access SAP Gateway for Microsoft.) Click  **Next**.</span></span>
    
 
  4. <span data-ttu-id="51715-p117">Wählen Sie Azure ACS als Authentifizierungssystem aus. (Ihr SharePoint-Add-In verwendet dieses System, wenn es auf SharePoint zugreift. Es verwendet das System nicht, wenn es auf das SAP-Gateway für Microsoft zugreift.) Klicken Sie auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="51715-p117">Choose Azure ACS as the authentication system. (Your SharePoint Add-in will use this system if it accesses SharePoint. It does not use this system when it accesses SAP Gateway for Microsoft.) Click  **Finish**.</span></span>
    
 
2. <span data-ttu-id="51715-p118">Nachdem das Projekt erstellt ist, werden Sie aufgefordert, sich beim Office 365-Konto anzumelden. Verwenden Sie die Anmeldeinformationen eines Kontoadministrators, z. B. Bob@<O365_domain>.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="51715-p118">After the project is created, you are prompted to login to the Office 365 account. Use the credentials of an account administrator; for example Bob@<O365_domain>.onmicrosoft.com.</span></span>
    
 
3. <span data-ttu-id="51715-p119">Die Visual Studio-Projektmappe enthält zwei Projekte: das eigentliche SharePoint-Add-In-Projekt und ein ASP.NET Web Forms-Projekt. Fügen Sie mit den folgenden Schritten das Paket der **Active Directory-Authentifizierungsbibliothek** (ADAL) zum ASP.NET-Projekt hinzu:</span><span class="sxs-lookup"><span data-stu-id="51715-p119">There are two projects in the Visual Studio solution; the SharePoint Add-in proper project and an ASP.NET web forms project. Add the  **Active Directory Authentication Library** (ADAL) package to the ASP.NET project with these steps:</span></span>
    
      1. <span data-ttu-id="51715-162">Klicken Sie mit der rechten Maustaste auf den Ordner **Referenzen** im ASP.NET-Projekt (mit dem Namen **SAP2SharePointWeb** im fortlaufenden Beispiel), und wählen Sie **NuGet-Pakete verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="51715-162">Right-click the  **References** folder in the ASP.NET project (named **SAP2SharePointWeb** in the continuing example) and select **Manage NuGet Packages**.</span></span> 
    
 
  2. <span data-ttu-id="51715-p120">Wählen Sie im daraufhin geöffneten Dialogfeld auf der linken Seite **Online** aus. Geben Sie „Microsoft.IdentityModel.Clients.ActiveDirectory“ in das Suchfeld ein.</span><span class="sxs-lookup"><span data-stu-id="51715-p120">In the dialog that opens, select  **Online** on the left. EnterMicrosoft.IdentityModel.Clients.ActiveDirectory in the search box.</span></span>
    
 
  3. <span data-ttu-id="51715-165">Wenn die ADAL-Bibliothek in den Suchergebnissen angezeigt wird, klicken Sie auf die Schaltfläche **Installieren** daneben, und akzeptieren Sie die Lizenz, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="51715-165">When the ADAL library appears in the search results, click the  **Install** button beside it, and accept the license when prompted.</span></span>
    
 
4. <span data-ttu-id="51715-166">Fügen Sie das Json.net-Paket mit den folgenden Schritten zum ASP.NET-Projekt hinzu:</span><span class="sxs-lookup"><span data-stu-id="51715-166">Add the Json.net package to the ASP.NET project with these steps:</span></span>
    
      1. <span data-ttu-id="51715-p121">Geben Sie „Json.net“ in das Suchfeld ein. Wenn dies zu viele Treffer zurückgibt, suchen Sie stattdessen nach „onNewtonsoft.json“.</span><span class="sxs-lookup"><span data-stu-id="51715-p121">Enter Json.net in the search box. If this produces too many hits, try searching onNewtonsoft.json.</span></span>
    
 
  2. <span data-ttu-id="51715-169">Wenn „Json.net“ in den Suchergebnissen angezeigt wird, klicken Sie auf die Schaltfläche **Installieren** daneben.</span><span class="sxs-lookup"><span data-stu-id="51715-169">When Json.net appears in the search results, click the  **Install** button beside it.</span></span>
    
 
5. <span data-ttu-id="51715-170">Klicken Sie auf **Schließen**.</span><span class="sxs-lookup"><span data-stu-id="51715-170">Click  **Close**.</span></span>
    
 

### <a name="register-your-web-application-with-azure-ad"></a><span data-ttu-id="51715-171">Registrieren Ihrer Webanwendung bei Azure AD</span><span class="sxs-lookup"><span data-stu-id="51715-171">Register your web application with Azure AD</span></span>


1. <span data-ttu-id="51715-172">Melden Sie sich mit Ihrem Azure-Administratorkonto beim [Azure-Verwaltungsportal](https://manage.windowsazure.com) an.</span><span class="sxs-lookup"><span data-stu-id="51715-172">Login into the  [Azure Management portal](https://manage.windowsazure.com) with your Azure administrator account.</span></span>
    
     <span data-ttu-id="51715-173">**Hinweis** Aus Sicherheitsgründen wird empfohlen, bei der Entwicklung von Add-Ins kein Administratorkonto zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="51715-173">**Note**  For security purposes, we recommend against using an administrator account when developing add-ins.</span></span>
2. <span data-ttu-id="51715-174">Wählen Sie auf der linken Seite **Active Directory** aus.</span><span class="sxs-lookup"><span data-stu-id="51715-174">Choose  **Active Directory** on the left side.</span></span>
    
 
3. <span data-ttu-id="51715-175">Klicken Sie auf Ihr Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="51715-175">Click on your directory.</span></span> 
    
 
4. <span data-ttu-id="51715-176">Wählen Sie **ANWENDUNGEN** (in der obersten Navigationsleiste) aus.</span><span class="sxs-lookup"><span data-stu-id="51715-176">Choose  **APPLICATIONS** (on the top navigation bar).</span></span>
    
 
5. <span data-ttu-id="51715-177">Wählen Sie in der Symbolleiste am unteren Rand des Bildschirms **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="51715-177">Choose  **Add** on the toolbar at the bottom of the screen.</span></span>
    
 
6. <span data-ttu-id="51715-178">Wählen Sie im daraufhin geöffneten Dialogfeld **Eine Anwendung hinzufügen, die meine Organisation entwickelt**.</span><span class="sxs-lookup"><span data-stu-id="51715-178">On the dialog that opens, choose  **Add an application my organization is developing**.</span></span>
    
 
7. <span data-ttu-id="51715-p122">Geben Sie der Anwendung im Dialogfeld **ANWENDUNG HINZUFÜGEN** einen Namen. Verwenden Sie für das fortlaufende Beispiel den Namen „ContosoAutomobileCollection“.</span><span class="sxs-lookup"><span data-stu-id="51715-p122">On the  **ADD APPLICATION** dialog, give the application a name. For the continuing example, useContosoAutomobileCollection.</span></span> 
    
 
8. <span data-ttu-id="51715-181">Wählen Sie **Webanwendung und/oder Web-API** als Anwendungstyp aus, und klicken Sie dann auf den Pfeil nach rechts.</span><span class="sxs-lookup"><span data-stu-id="51715-181">Choose  **Web Application And/Or Web API** as the application type, and then click the right arrow button.</span></span>
    
 
9. <span data-ttu-id="51715-p123">Verwenden Sie auf der zweiten Seite des Dialogfelds die SSL-Debugging-URL aus dem ASP.NET-Projekt in der Visual Studio-Projektmappe als **ANMELDE-URL**. Sie finden die URL mit den folgenden Schritten. ***(Sie müssen das Add-In anfangs bei der Debugging-URL registrieren, damit Sie den Visual Studio-Debugger (F5) ausführen können. Wenn Ihr Add-In für das Staging bereit ist, registrieren Sie es erneut bei der zugehörigen Azure-Website-Staging-URL. [Ändern Sie das Add-In, und stellen Sie es für Azure und Office 365 bereit](#Stage).)***</span><span class="sxs-lookup"><span data-stu-id="51715-p123">On the second page of the dialog, use the SSL debugging URL from the ASP.NET project in the Visual Studio solution as the  **SIGN-ON URL**. You can find the URL using the following steps.  ***(You need to register the add-in initially with the debugging URL so that you can run the Visual Studio debugger (F5). When your add-in is ready for staging, you will re-register it with its staging Azure Web Site URL.  [Modify the add-in and stage it to Azure and Office 365](#Stage).)***</span></span>
    
      1. <span data-ttu-id="51715-185">Markieren Sie das ASP.NET-Projekt im **Projektmappen-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="51715-185">Highlight the ASP.NET project in  **Solution Explorer**.</span></span> 
    
 
  2. <span data-ttu-id="51715-p124">Kopieren Sie im Fenster **Eigenschaften** den Wert der Eigenschaft **SSL-URL**. Ein Beispiel ist „https://localhost:44300/“.</span><span class="sxs-lookup"><span data-stu-id="51715-p124">In the  **Properties** window, copy the value of the **SSL URL** property. An example ishttps://localhost:44300/.</span></span>
    
 
  3. <span data-ttu-id="51715-188">Fügen Sie ihn in das Feld **ANMELDE-URL** im Dialogfeld **ANWENDUNG HINZUFÜGEN** ein.</span><span class="sxs-lookup"><span data-stu-id="51715-188">Paste it into the  **SIGN-ON URL** on the **ADD APPLICATION** dialog.</span></span>
    
 
10. <span data-ttu-id="51715-189">Weisen Sie der Anwendung im Feld **APP-ID-URI** einen eindeutigen URI zu, wie den an das Ende der SSL-URL angehängten Anwendungsnamen, z. B. https://localhost:44300/ContosoAutomobileCollection.</span><span class="sxs-lookup"><span data-stu-id="51715-189">For the  **APP ID URI**, give the application a unique URI, such as the application name appended to the end of the SSL URL; for example https://localhost:44300/ContosoAutomobileCollection.</span></span>
    
 
11. <span data-ttu-id="51715-p125">Klicken Sie auf die Schaltfläche mit dem Häkchen. Das Azure-Dashboard für die Anwendung wird mit einer Erfolgsmeldung geöffnet.</span><span class="sxs-lookup"><span data-stu-id="51715-p125">Click the checkmark button. The Azure dashboard for the application opens with a success message.</span></span>
    
 
12. <span data-ttu-id="51715-192">Wählen Sie im oberen Bereich der Seite **KONFIGURIEREN** aus.</span><span class="sxs-lookup"><span data-stu-id="51715-192">Choose  **CONFIGURE** on the top of the page.</span></span>
    
 
13. <span data-ttu-id="51715-p126">Scrollen Sie zu **CLIENT-ID**, und erstellen Sie eine Kopie der ID. Diese benötigen Sie für ein späteres Verfahren.</span><span class="sxs-lookup"><span data-stu-id="51715-p126">Scroll to the  **CLIENT ID** and make a copy of it. You will need it for a later procedure.</span></span>
    
 
14. <span data-ttu-id="51715-p127">Erstellen Sie im Abschnitt **Schlüssel** einen Schlüssel. Dieser wird anfangs nicht angezeigt. Klicken Sie im unteren Bereich der Seite auf **SPEICHERN**, damit der Schlüssel sichtbar wird. Erstellen Sie eine Kopie des Schlüssels. Diese benötigen Sie für ein späteres Verfahren.</span><span class="sxs-lookup"><span data-stu-id="51715-p127">In the  **keys** section, create a key. It won't appear initially. Click **SAVE** at the bottom of the page and the key will be visible. Make a copy of it. You will need it for a later procedure.</span></span>
    
 
15. <span data-ttu-id="51715-200">Scrollen Sie zu **Berechtigungen für andere Anwendungen**, und wählen Sie Ihre SAP-Gateway für Microsoft-Dienstanwendung aus.</span><span class="sxs-lookup"><span data-stu-id="51715-200">Scroll to  **permissions to other applications** and select your SAP Gateway for Microsoft service application.</span></span>
    
 
16. <span data-ttu-id="51715-201">Öffnen Sie die Dropdownliste **Delegierte Berechtigungen**, und aktivieren Sie die Kontrollkästchen für die Berechtigungen für den SAP-Gateway für Microsoft-Dienst, die Ihr SharePoint-Add-In benötigt.</span><span class="sxs-lookup"><span data-stu-id="51715-201">Open the  **Delegated Permissions** drop down list and enable the boxes for the permissions to the SAP Gateway for Microsoft service that your SharePoint Add-in will need.</span></span>
    
 
17. <span data-ttu-id="51715-202">Klicken Sie unten im Bildschirm auf **SPEICHERN**.</span><span class="sxs-lookup"><span data-stu-id="51715-202">Click  **SAVE** at the bottom of the screen.</span></span>
    
 

### <a name="configure-the-application-to-communicate-with-azure-ad"></a><span data-ttu-id="51715-203">Konfigurieren der Anwendung für die Kommunikation mit Azure AD</span><span class="sxs-lookup"><span data-stu-id="51715-203">Configure the application to communicate with Azure AD</span></span>


1. <span data-ttu-id="51715-204">Öffnen Sie in Visual Studio die Datei „web.config“ im ASP.NET-Projekt.</span><span class="sxs-lookup"><span data-stu-id="51715-204">In Visual Studio, open the web.config file in the ASP.NET project.</span></span>
    
 
2. <span data-ttu-id="51715-p128">Im Abschnitt  `<appSettings>` verfügen die Office-Entwicklertools für Visual Studio über hinzugefügte Elemente für **ClientID** und **ClientSecret** des SharePoint-Add-In. (Diese werden im Azure ACS-Autorisierungssystem verwendet, wenn die ASP.NET-Anwendung auf SharePoint zugreift. Sie können diese für das fortlaufende Beispiel ignorieren, sollten sie aber nicht löschen. Sie sind in vom Anbieter gehosteten SharePoint-Add-Ins erforderlich, selbst wenn die App nicht auf SharePoint-Daten zugreift. Ihre Werte ändern sich jedes Mal, wenn Sie F5 in Visual Studio drücken.) Fügen Sie die folgenden zwei Elemente zum Abschnitt hinzu. Diese werden von der Anwendung für die Authentifizierung bei Azure AD verwendet. (Denken Sie daran, dass Anwendungen und Benutzer in OAuth-basierten Authentifizierungs- und Autorisierungssystemen Sicherheitsprinzipale sind.)</span><span class="sxs-lookup"><span data-stu-id="51715-p128">In the  `<appSettings>` section, the Office Developer Tools for Visual Studio have added elements for the **ClientID** and **ClientSecret** of the SharePoint Add-in. (These are used in the Azure ACS authorization system if the ASP.NET application accesses SharePoint. You can ignore them for the continuing example, but do not delete them. They are required in provider-hosted SharePoint Add-ins even if the add-in is not accessing SharePoint data. Their values will change each time you press F5 in Visual Studio.) Add the following two elements to the section. These are used by the application to authenticate to Azure AD. (Remember that applications, as well as users, are security principals in OAuth-based authentication and authorization systems.)</span></span>
    
```
  <add key="ida:ClientID" value="" />
<add key="ida:ClientKey" value="" />
```

3. <span data-ttu-id="51715-p129">Geben Sie die Client-ID, die Sie in einem früheren Schritt aus Ihrem Azure AD-Verzeichnis gespeichert haben, als Wert des Schlüssels **ida:ClientID** ein. Behalten Sie Groß-/Kleinschreibung und Satzzeichen exakt so bei, wie Sie sie kopiert haben, und achten Sie darauf, am Anfang oder Ende des Werts kein Leerzeichen einzufügen. Verwenden Sie als **ida:ClientKey**-Schlüssel den *Schlüssel*, den Sie aus dem Verzeichnis gespeichert haben. Achten Sie auch hier darauf, keine Leerzeichen einzufügen oder den Wert auf irgendeine Weise zu ändern. Der Abschnitt `<appSettings>` sollte jetzt ungefähr wie das folgende Beispiel aussehen. (Der Wert **ClientId** enthält möglicherweise eine GUID oder eine leere Zeichenfolge.)</span><span class="sxs-lookup"><span data-stu-id="51715-p129">Insert the client ID that you saved from your Azure AD directory in the earlier procedure as the value of the  **ida:ClientID** key. Leave the casing and punctuation exactly as you copied it and be careful not to include a space character at the beginning or end of the value. For the **ida:ClientKey** key use the *key*  that you saved from the directory. Again, be careful not to introduce any space characters or change the value in any way. The `<appSettings>` section should now look something like the following. (The **ClientId** value may have a GUID or an empty string.)</span></span>
    
```
  <appSettings>
  <add key="ClientId" value="" />
  <add key="ClientSecret" value="LypZu2yVajlHfPLRn5J2hBrwCk5aBOHxE4PtKCjIQkk=" />
  <add key="ida:ClientID" value="4da99afe-08b5-4bce-bc66-5356482ec2df" />
  <add key="ida:ClientKey" value="URwh/oiPay/b5jJWYHgkVdoE/x7gq3zZdtcl/cG14ss=" />
</appSettings>
```


     **Note**  Your application is known to Azure AD by the "localhost" URL you used to register it. The client ID and client key are associated with that identity. When you are ready to stage your application to an Azure Web Site, you will re-register it with a new URL.
4. <span data-ttu-id="51715-p130">Fügen Sie weiterhin im Bereich **appSettings** einen **Authority**-Schlüssel hinzu, und legen Sie seinen Wert auf die Office 365-Domäne ( *beliebige_Domäne*.onmicrosoft.com) Ihres Organisationskontos fest. Im fortlaufenden Beispiel ist das Organisationskonto „Bob@<O365_domain>.onmicrosoft.com“, deshalb ist die Autorität `<O365_domain>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="51715-p130">Still in the  **appSettings** section, add an **Authority** key and set its value to the Office 365 domain ( *some_domain*  .onmicrosoft.com) of your organizational account. In the continuing example, the organizational account is Bob@<O365_domain>.onmicrosoft.com, so the authority is `<O365_domain>.onmicrosoft.com`.</span></span> 
    
```
  <add key="Authority" value="<O365_domain>.onmicrosoft.com" />
```

5. <span data-ttu-id="51715-p131">Fügen Sie immer noch im Abschnitt **appSettings** einen **AppRedirectUrl**-Schlüssel hinzu, und legen Sie seinen Wert auf die Seite fest, auf die der Browser des Benutzers umgeleitet werden soll, nachdem das ASP.NET-Add-In einen Autorisierungscode von Azure AD erhalten hat. Normalerweise ist dies dieselbe Seite, auf der sich der Benutzer befand, als der Aufruf an Azure AD stattfand. Im fortlaufenden Beispiel verwenden Sie den SSL-URL-Wert, an den Sie „/Pages/Default.aspx“ anhängen, wie unten gezeigt. (Dies ist ein weiterer Wert, den Sie für das Staging verändern werden.)</span><span class="sxs-lookup"><span data-stu-id="51715-p131">Still in the  **appSettings** section, add an **AppRedirectUrl** key and set its value to the page that the user's browser should be redirected to after the ASP.NET add-in has obtained an authorization code from Azure AD. Usually, this is the same page that the user was on when the call to Azure AD was made. In the continuing example, use the SSL URL value with "/Pages/Default.aspx" appended to it as shown below. (This is another value that you will change for staging.)</span></span>
    
```
  <add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />
```

6. <span data-ttu-id="51715-p132">Fügen Sie weiterhin im Abschnitt **appSettings** einen **ResourceUrl**-Schlüssel hinzu, und legen Sie seinen Wert auf den APP-ID-URI des SAP-Gateway für Microsoft fest (*nicht* den APP-ID-URI Ihrer ASP.NET-Anwendung). Sie erhalten diesen Wert vom SAP-Gateway für Microsoft-Administrator. Im Folgenden sehen Sie ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="51715-p132">Still in the  **appSettings** section, add a **ResourceUrl** key and set its value to the APP ID URI of SAP Gateway for Microsoft ( *not*  the APP ID URI of your ASP.NET application). Obtain this value from the SAP Gateway for Microsoft administrator. The following is an example.</span></span>
    
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

7. <span data-ttu-id="51715-227">Speichern und schließen Sie die Datei „web.config“.</span><span class="sxs-lookup"><span data-stu-id="51715-227">Save and close the web.config file.</span></span>
    
     <span data-ttu-id="51715-p133">**Tipp** Lassen Sie die Datei „web.config“ nicht geöffnet, während Sie den Visual Studio-Debugger (F5) ausführen. Die Office Developer Tools für Visual Studio ändern den **ClientId**-Wert (nicht die **ida:ClientID**) jedes Mal, wenn Sie F5 drücken. Daher müssen Sie auf eine Aufforderung zum erneuten Laden der Datei „web.config“ reagieren, wenn sie geöffnet ist, bevor das Debugging ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="51715-p133">**Tip**  Do not leave the web.config file open when you run the Visual Studio debugger (F5). The Office Developer Tools for Visual Studio change the  **ClientId** value (not the **ida:ClientID**) every time you press F5. This requires you to respond to a prompt to reload the web.config file, if it is open, before debugging can execute.</span></span>

### <a name="add-a-helper-class-to-authenticate-to-azure-ad"></a><span data-ttu-id="51715-231">Hinzufügen einer Hilfsklasse zur Authentifizierung bei Azure-AD</span><span class="sxs-lookup"><span data-stu-id="51715-231">Add a helper class to authenticate to Azure AD</span></span>


1. <span data-ttu-id="51715-232">Klicken Sie mit der rechten Maustaste auf das ASP.NET-Projekt, und verwenden Sie das Visual Studio-Verfahren zum Hinzufügen von Elementen, um dem Projekt eine neue Klassendatei mit dem Namen „AADAuthHelper.cs“ hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="51715-232">Right-click the ASP.NET project and use the Visual Studio item adding process to add a new class file to the project named AADAuthHelper.cs.</span></span>
    
 
2. <span data-ttu-id="51715-233">Fügen Sie der Datei die folgenden **using**-Anweisungen hinzu.</span><span class="sxs-lookup"><span data-stu-id="51715-233">Add the following  **using** statements to the file.</span></span>
    
```
  using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using System.Web.UI;

```

3. <span data-ttu-id="51715-234">Ändern Sie das Zugriffsschlüsselwort von **public** in **internal**, und fügen Sie das **static**-Schlüsselwort zur Klassendeklaration hinzu.</span><span class="sxs-lookup"><span data-stu-id="51715-234">Change the access keyword from  **public** to **internal** and add the **static** keyword to the class declaration.</span></span>
    
```
  internal static class AADAuthHelper
```

4. <span data-ttu-id="51715-p134">Fügen Sie der Klasse die folgenden Felder hinzu. In diesen Feldern werden Informationen gespeichert, die die ASP.NET-Anwendung zum Abrufen von Zugriffstoken von AAD verwendet.</span><span class="sxs-lookup"><span data-stu-id="51715-p134">Add the following fields to the class. These fields store information that your ASP.NET application uses to get access tokens from AAD.</span></span>
    
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

5. <span data-ttu-id="51715-p135">Fügen Sie der Klasse die folgende Eigenschaft hinzu. Diese Eigenschaft hält die URL zum Azure AD-Anmeldebildschirm.</span><span class="sxs-lookup"><span data-stu-id="51715-p135">Add the following property to the class. This property holds the URL to the Azure AD login screen.</span></span>
    
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

6. <span data-ttu-id="51715-p136">Fügen Sie der Klasse die folgenden Eigenschaften hinzu. Diese speichern das Zugriffs- und Aktualisierungstoken zwischen und überprüfen ihre Gültigkeit.</span><span class="sxs-lookup"><span data-stu-id="51715-p136">Add the following properties to the class. These cache the access and refresh tokens and check their validity.</span></span>
    
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

7. <span data-ttu-id="51715-p137">Fügen Sie der Klasse die folgenden Methoden hinzu. Diese werden verwendet, um die Gültigkeit des Autorisierungscodes zu überprüfen und ein Zugriffstoken von Azure AD zu erhalten, indem entweder ein Authentifizierungscode oder ein Aktualisierungstoken verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="51715-p137">Add the following methods to the class. These are used to check the validity of the authorization code and to obtain an access token from Azure AD by using either an authentication code or a refresh token.</span></span>
    
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

8. <span data-ttu-id="51715-p138">Fügen Sie der Klasse die folgende Methode hinzu. Sie wird vom ASP.NET-Code dahinter aufgerufen, um ein gültiges Zugriffstoken zu erhalten, bevor ein Aufruf zum Abrufen von SAP-Daten über SAP-Gateway für Microsoft erfolgt.</span><span class="sxs-lookup"><span data-stu-id="51715-p138">Add the following method to the class. It is called from the ASP.NET code behind to obtain a valid access token before a call is made to get SAP data via SAP Gateway for Microsoft.</span></span>
    
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


 <span data-ttu-id="51715-p139">**Tipp** Die AADAuthHelper-Klasse bietet nur eine minimale Fehlerbehandlung. Für ein robustes SharePoint-Add-In in Produktionsqualität fügen Sie mehr Fehlerbehandlung hinzu, wie im folgenden MSDN-Knoten beschrieben: [Fehlerbehandlung in OAuth 2.0](http://msdn.microsoft.com/library/561bf289-3ff9-4eea-b165-4f5f02bcc520.aspx).</span><span class="sxs-lookup"><span data-stu-id="51715-p139">**Tip**  The AADAuthHelper class has only minimal error handling. For a robust, production quality SharePoint Add-in, add more error handling as described in this MSDN node:  [Error Handling in OAuth 2.0](http://msdn.microsoft.com/library/561bf289-3ff9-4eea-b165-4f5f02bcc520.aspx).</span></span>
 


### <a name="create-data-model-classes"></a><span data-ttu-id="51715-247">Erstellen von Datenmodellklassen</span><span class="sxs-lookup"><span data-stu-id="51715-247">Create data model classes</span></span>


1. <span data-ttu-id="51715-p140">Erstellen Sie eine oder mehrere Klassen, um die Daten zu modellieren, die Ihre App von SAP abruft. Im fortlaufenden Beispiel gibt es nur eine Datenmodellklasse. Klicken Sie mit der rechten Maustaste auf das ASP.NET-Projekt, und verwenden Sie den Visual Studio-Prozess zum Hinzufügen von Elementen, um eine neue Klassendatei zum Projekt mit dem Namen Automobile.cs hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="51715-p140">Create one or more classes to model the data that your add-in gets from SAP. In the continuing example, there is just one data model class. Right-click the ASP.NET project and use the Visual Studio item adding process to add a new class file to the project named Automobile.cs.</span></span>
    
 
2. <span data-ttu-id="51715-251">Fügen Sie den folgenden Code zum Textteil der Klasse hinzu:</span><span class="sxs-lookup"><span data-stu-id="51715-251">Add the following code to the body of the class:</span></span>
    
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


### <a name="add-code-behind-to-get-data-from-sap-via-the-sap-gateway-for-microsoft"></a><span data-ttu-id="51715-252">Hinzufügen des zugrunde liegenden Codes, um Daten über das SAP-Gateway für Microsoft aus SAP abzurufen</span><span class="sxs-lookup"><span data-stu-id="51715-252">Add code behind to get data from SAP via the SAP Gateway for Microsoft</span></span>


1. <span data-ttu-id="51715-253">Öffnen Sie die Datei „Default.aspx.cs“, und fügen Sie die folgenden **using**-Anweisungen hinzu.</span><span class="sxs-lookup"><span data-stu-id="51715-253">Open the Default.aspx.cs file and add the following  **using** statements.</span></span>
    
```
  using System.Net;
using Newtonsoft.Json.Linq;
```

2. <span data-ttu-id="51715-p141">Fügen Sie eine **const**-Deklaration zur Default-Klasse hinzu, deren Wert die Basis-URL des SAP-OData-Endpunkts ist, auf den das Add-In zugreift. Im Folgenden ist ein Beispiel dargestellt:</span><span class="sxs-lookup"><span data-stu-id="51715-p141">Add a  **const** declaration to the Default class whose value is the base URL of the SAP OData endpoint that the add-in will be accessing. The following is an example:</span></span>
    
```
  private const string SAP_ODATA_URL = @"https://<SAP_gateway_domain>.cloudapp.net:8081/perf/sap/opu/odata/sap/ZCAR_POC_SRV/";
```

3. <span data-ttu-id="51715-p142">Die Office Developer Tools für Visual Studio haben eine **Page_PreInit**-Methode und eine **Page_Load**-Methode hinzugefügt. Kommentieren Sie den Code in der **Page_Load**-Methode und die gesamte **Page_Init**-Methode aus. Dieser Code wird im Beispiel nicht verwendet. (Wenn Ihr SharePoint-Add-In auf SharePoint zugreifen wird, stellen Sie diesen Code wieder her. Informationen finden Sie unter [Optionales Hinzufügen eines Zugriffs auf SharePoint zur ASP.NET-Anwendung](#SharePoint).)</span><span class="sxs-lookup"><span data-stu-id="51715-p142">The Office Developer Tools for Visual Studio have added a  **Page_PreInit** method and a **Page_Load** method. Comment out the code inside the **Page_Load** method and comment out the whole **Page_Init** method. This code is not used in this sample. (If your SharePoint Add-in is going to access SharePoint, then you restore this code. See [Optionally, add SharePoint access to the ASP.NET application](#SharePoint).)</span></span>
    
 
4. <span data-ttu-id="51715-p143">Fügen Sie die folgende Zeile im oberen Bereich der **Page_Load**-Methode hinzu. Damit wird der Debugging-Prozess vereinfacht, da Ihre ASP.NET-Anwendung über SSL (HTTPS) mit dem SAP-Gateway für Microsoft kommuniziert. Ihr „localhost:port“-Server ist aber nicht so konfiguriert, dass er dem Zertifikat des SAP-Gateway für Microsoft vertraut. Mit dieser Codezeile würden Sie eine Warnung zu einem ungültigen Zertifikat erhalten, bevor „Default.aspx“ geöffnet wird. In einigen Browsern können Sie diesen Fehler einfach wegklicken, aber in anderen können Sie „Default.aspx“ gar nicht öffnen.</span><span class="sxs-lookup"><span data-stu-id="51715-p143">Add the following line to the top of the  **Page_Load** method. This will ease the process of debugging because your ASP.NET application is communicating with SAP Gateway for Microsoft using SSL (HTTPS); but your "localhost:port" server is not configured to trust the certificate of SAP Gateway for Microsoft. Without this line of code, you would get an invalid certificate warning before Default.aspx will open. Some browsers allow you to click past this error, but some will not let you open Default.aspx at all.</span></span>
    
```
  ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;
```


     **Important**  Delete this line when you are ready to deploy the ASP.NET application to staging. See  [Modify the add-in and stage it to Azure and Office 365](#Stage).
1. <span data-ttu-id="51715-p144">Fügen Sie der **Page_Load**-Methode den folgenden Code hinzu. Die an die `GetSAPData`-Methode übergebene Zeichenfolge ist eine OData-Abfrage.</span><span class="sxs-lookup"><span data-stu-id="51715-p144">Add the following code to the  **Page_Load** method. The string you pass to the `GetSAPData` method is an OData query.</span></span>
    
```
  if (!IsPostBack)
{
    GetSAPData("DataCollection?$top=3");
}

```

6. <span data-ttu-id="51715-p145">Fügen Sie die folgende Methode zur Default-Klasse hinzu. Diese Methode stellt zunächst sicher, dass der Cache für das Zugriffstoken ein gültiges Zugriffstoken enthält, das von Azure AD abgerufen wurde. Dann erstellt sie eine HTTP **GET**-Anforderung, die das Zugriffstoken enthält, und sendet diese an den SAP-OData-Endpunkt. Das Ergebnis wird als JSON-Objekt zurückgegeben, das in ein .NET **List**-Objekt konvertiert wird. Drei Eigenschaften der Elemente werden in einem Array verwendet, das an **DataListView** gebunden ist.</span><span class="sxs-lookup"><span data-stu-id="51715-p145">Add the following method to the Default class. This method first ensures that the cache for the access token has a valid access token in it that has been obtained from Azure AD. It then creates an HTTP  **GET** Request that includes the access token and sends it to the SAP OData endpoint. The result is returned as a JSON object that is converted to a .NET **List** object. Three properties of the items are used in an array that is bound to the **DataListView**.</span></span>
    
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


### <a name="create-the-user-interface"></a><span data-ttu-id="51715-272">Erstellen der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="51715-272">Create the user interface</span></span>


1. <span data-ttu-id="51715-273">Öffnen Sie die „Datei Default.aspx“, und fügen Sie dem **form**-Element der Seite das folgende Markup hinzu:</span><span class="sxs-lookup"><span data-stu-id="51715-273">Open the Default.aspx file and add the following markup to the  **form** of the page:</span></span>
    
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

2. <span data-ttu-id="51715-274">Geben Sie der Webseite optional das Erscheinungsbild einer SharePoint-Seite, indem Sie das SharePoint [-Chromsteuerelement](use-the-client-chrome-control-in-sharepoint-add-ins.md) und [das Stylesheet der Host-SharePoint-Website](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md) verwenden.</span><span class="sxs-lookup"><span data-stu-id="51715-274">Optionally, give the web page the "look 'n' feel" of a SharePoint page with the SharePoint  [Chrome Control](use-the-client-chrome-control-in-sharepoint-add-ins.md) and [the host SharePoint website's style sheet](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md).</span></span>
    
 

### <a name="test-the-add-in-with-f5-in-visual-studio"></a><span data-ttu-id="51715-275">Testen des Add-Ins mit F5 in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51715-275">Test the add-in with F5 in Visual Studio</span></span>


1. <span data-ttu-id="51715-276">Drücken Sie in Visual Studio F5.</span><span class="sxs-lookup"><span data-stu-id="51715-276">Press F5 in Visual Studio.</span></span>
    
 
2. <span data-ttu-id="51715-p146">Wenn Sie F5 zum ersten Mal verwenden, werden Sie möglicherweise aufgefordert, sich bei der Website für Entwickler anzumelden, die Sie verwenden. Benutzen Sie dafür die Anmeldeinformationen des Websiteadministrators. Im fortlaufenden Beispiel ist das Bob@<O365_domain>.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="51715-p146">The first time that you use F5, you may be prompted to login to the Developer Site that you are using. Use the site administrator credentials. In the continuing example, it is Bob@<O365_domain>.onmicrosoft.com.</span></span>
    
 
3. <span data-ttu-id="51715-p147">Wenn Sie F5 zum ersten Mal verwenden, werden Sie aufgefordert, dem Add-In Berechtigungen zu gewähren. Klicken Sie auf **Vertrauen**.</span><span class="sxs-lookup"><span data-stu-id="51715-p147">The first time that you use F5, you are prompted to grant permissions to the add-in. Click  **Trust It**.</span></span>
    
 
4. <span data-ttu-id="51715-p148">Nach einer kurzen Verzögerung, während der das Zugriffstoken abgerufen wird, wird die Seite „Default.aspx“ geöffnet. Stellen Sie sicher, dass die SAP-Daten angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="51715-p148">After a brief delay while the access token is being obtained, the Default.aspx page opens. Verify that the SAP data appears.</span></span>
    
 

## <a name="optionally-add-sharepoint-access-to-the-aspnet-application"></a><span data-ttu-id="51715-284">Optional können Sie der ASP.NET-Anwendung SharePoint-Zugriff hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="51715-284">Optionally, add SharePoint access to the ASP.NET application</span></span>
<span data-ttu-id="51715-285"><a name="SharePoint"> </a></span><span class="sxs-lookup"><span data-stu-id="51715-285"></span></span>

<span data-ttu-id="51715-p149">Natürlich muss Ihr SharePoint-Add-In nicht nur SAP-Daten auf einer von SharePoint gestarteten Webseite anzeigen. Es kann auch SharePoint-Daten erstellen, lesen, aktualisieren und löschen. Ihr zugrunde liegender Code kann dafür entweder das SharePoint-Clientobjektmodell (CSOM) oder die REST-APIs von SharePoint verwenden. Das CSOM wird als Assemblypaar bereitgestellt, das die Office Developer Tools für Visual Studio automatisch in das ASP.NET-Projekt eingefügt und auf **Lokale Kopie** in Visual Studio festgelegt haben, damit es im ASP.NET-Anwendungspaket enthalten ist. Weitere Informationen zum Verwenden von CSOM finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](complete-basic-operations-using-sharepoint-client-library-code.md). Informationen zum Verwenden der REST-APIs finden Sie unter [Erläuterungen zur REST-Schnittstelle von SharePoint und zu ihrer Verwendung](http://msdn.microsoft.com/de-DE/magazine/dn198245.aspx).</span><span class="sxs-lookup"><span data-stu-id="51715-p149">Of course, your SharePoint Add-in doesn't have to expose only SAP data in a web page launched from SharePoint. It can also create, read, update, and delete (CRUD) SharePoint data. Your code behind can do this using either the SharePoint client object model (CSOM) or the REST APIs of SharePoint. The CSOM is deployed as a pair of assemblies that the Office Developer Tools for Visual Studio automatically included in the ASP.NET project and set to  **Copy Local** in Visual Studio so that they are included in the ASP.NET application package. For information about using CSOM, start with [Complete basic operations using SharePoint client library code](complete-basic-operations-using-sharepoint-client-library-code.md). For information about using the REST APIs, start with  [Understanding and Using the SharePoint REST Interface](http://msdn.microsoft.com/de-DE/magazine/dn198245.aspx).</span></span> 
 

 
<span data-ttu-id="51715-p150">Unabhängig davon, ob Sie CSOM oder die REST-APIs für den Zugriff auf SharePoint verwenden, muss Ihre ASP.NET-Anwendung ein Zugriffstoken für SharePoint abrufen, ebenso wie für das SAP-Gateway für Microsoft. Weitere Informationen finden Sie unter  [Verstehen der Authentifizierung und Autorisierung beim SAP-Gateway für Microsoft und SharePoint](#AuthOverview) weiter oben. Das Verfahren unten stellt einige grundlegende Anweisungen zur entsprechenden Vorgehensweise bereit, aber wir empfehlen, dass Sie zunächst die folgenden Artikel lesen:</span><span class="sxs-lookup"><span data-stu-id="51715-p150">Regardless, of whether you use CSOM or the REST APIs to access SharePoint, your ASP.NET application must get an access token to SharePoint, just as it does to SAP Gateway for Microsoft. See  [Understand authentication and authorization to SAP Gateway for Microsoft and SharePoint](#AuthOverview) above. The procedure below provides some basic guidance about how to do this, but we recommend that you first read the following articles:</span></span>
 

 

-  [<span data-ttu-id="51715-295">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="51715-295">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="51715-296">Autorisierung und Authentifizierung für Add-Ins in SharePoint</span><span class="sxs-lookup"><span data-stu-id="51715-296">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="51715-297">Drei Autorisierungssysteme für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="51715-297">Three authorization systems for SharePoint Add-ins</span></span>](three-authorization-systems-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="51715-298">Erstellen von SharePoint-Add-Ins, die die Autorisierung mit niedriger Vertrauensebene verwenden</span><span class="sxs-lookup"><span data-stu-id="51715-298">Creating SharePoint Add-ins that use low-trust authorization</span></span>](creating-sharepoint-add-ins-that-use-low-trust-authorization.md)
    
 
-  [<span data-ttu-id="51715-299">OAuth-Ablauf mit Kontexttoken für SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="51715-299">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins.md)
    
 

1. <span data-ttu-id="51715-p151">Öffnen Sie die Datei „Default.aspx.cs“, und kommentieren Sie die **Page_PreInit**-Methode aus. Kommentieren Sie außerdem den Code aus, den die Office Developer Tools für Visual Studio zur **Page_Load**-Methode hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="51715-p151">Open the Default.aspx.cs file and uncomment the  **Page_PreInit** method. Also uncomment the code that the Office Developer Tools for Visual Studio added to the **Page_Load** method.</span></span>
    
 
2. <span data-ttu-id="51715-p152">Wenn Ihr SharePoint-Add-In auf SharePoint-Daten zugreifen wird, müssen Sie das SharePoint-Kontexttoken zwischenspeichern, das beim Starten des Add-Ins in SharePoint an die Seite „Default.aspx“ übertragen wurde. Damit wird sichergestellt, dass das SharePoint-Kontexttoken nicht verloren geht, wenn der Browser nach der Azure AD-Authentifizierung umgeleitet wird. (Sie haben mehrere Optionen für das Zwischenspeichern dieses Kontexts.) Die Office Developer Tools für Visual Studio fügen eine SharePointContext.cs-Datei zum ASP.NET-Projekt hinzu, die den größten Teil der Arbeit übernimmt. Zum Verwenden des Sitzungscaches fügen Sie einfach den folgenden Code in den Block „`if (!IsPostBack)`“ *vor* dem Code ein, der den Aufruf an das SAP-Gateway für Microsoft durchführt:</span><span class="sxs-lookup"><span data-stu-id="51715-p152">If your SharePoint Add-in is going to access SharePoint data, then you have to cache the SharePoint context token that is POSTed to the Default.aspx page when the add-in is launched in SharePoint. This is to ensure that the SharePoint context token is not lost when the browser is redirected following the Azure AD authentication. (You have several options for how to cache this context.) The Office Developer Tools for Visual Studio add a SharePointContext.cs file to the ASP.NET project that does most of the work. To use the session cache, you simply add the following code inside the " `if (!IsPostBack)`" block  *before*  the code that calls out to SAP Gateway for Microsoft:</span></span>
    
```
  if (HttpContext.Current.Session["SharePointContext"] == null) 
{
     HttpContext.Current.Session["SharePointContext"]
        = SharePointContextProvider.Current.GetSharePointContext(Context);
}
```

3. <span data-ttu-id="51715-p153">Die Datei „SharePointContext.cs“ sendet Aufrufe an eine andere Datei, die die Office Developer Tools für Visual Studio zum Projekt hinzugefügt haben: TokenHelper.cs. Diese Datei stellt den größten Teil des Codes bereit, der erforderlich ist, um Zugriffstoken für SharePoint abzurufen und zu verwenden. Sie stellt jedoch keinen Code für das Erneuern eines abgelaufenen Zugriffstoken oder Aktualisierungstoken bereit. Sie enthält außerdem keinen Code zum Zwischenspeichern von Token. Für ein SharePoint-Add-In in Produktionsqualität benötigen Sie solchen Code. Die Zwischenspeicherlogik im vorherigen Schritt ist ein Beispiel. Ihr Code sollte außerdem das Zugriffstoken zwischenspeichern und es wiederverwenden, bis es abgelaufen ist. Wenn das Zugriffstoken abgelaufen ist, sollte Ihr Code das Aktualisierungstoken verwenden, um ein neues Zugriffstoken abzurufen.</span><span class="sxs-lookup"><span data-stu-id="51715-p153">The SharePointContext.cs file makes calls to another file that the Office Developer Tools for Visual Studio added to the project: TokenHelper.cs. This file provides most of the code needed to obtain and use access tokens for SharePoint. However, it does not provide any code for renewing an expired access token or an expired refresh token. Nor does it contain any token caching code. For a production quality SharePoint Add-in, you need to add such code. The caching logic in the preceding step is an example. Your code should also cache the access token and reuse it until it expires. When the access token is expired, your code should use the refresh token to get a new access token.</span></span>
    
 
4. <span data-ttu-id="51715-p154">Fügen Sie die Datenaufrufe an SharePoint entweder über CSOM oder REST hinzu. Im folgenden Beispiel wurde CSOM-Code geändert, den die Office Developer Tools für Visual Studio zur **Page_Load**-Methode hinzufügen. In diesem Beispiel wurde der Code in eine separate Methode verschoben und beginnt mit dem Abrufen des zwischengespeicherten Kontexttokens.</span><span class="sxs-lookup"><span data-stu-id="51715-p154">Add the data calls to SharePoint using either CSOM or REST. The following example is a modification of CSOM code that Office Developer Tools for Visual Studio adds to the  **Page_Load** method. In this example, the code has been moved to a separate method and it begins by retrieving the cached context token.</span></span>
    
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

5. <span data-ttu-id="51715-p155">Fügen Sie die Benutzeroberflächenelemente zum Rendern der SharePoint-Daten hinzu. Nachfolgend sehen Sie das HTML-Steuerelement, auf das in der vorstehenden Methode verwiesen wird:</span><span class="sxs-lookup"><span data-stu-id="51715-p155">Add UI elements to render the SharePoint data. The following shows the HTML control that is referenced in the preceding method:</span></span>
    
```
  <h3>SharePoint title</h3><asp:Label ID="SharePointTitle" runat="server"></asp:Label><br />
```


 <span data-ttu-id="51715-p156">**Hinweis** Während Sie das SharePoint-Add-In debuggen, wird es von den Office Developer Tools für Visual Studio jedes Mal erneut bei Azure ACS registriert, wenn Sie F5 in Visual Studio drücken. Wenn Sie das SharePoint-Add-In bereitstellen, müssen Sie ihm eine langfristige Registrierung geben. Weitere Informationen finden Sie im Abschnitt [Ändern des Add-Ins und Bereitstellen für Azure und Office 365](#Stage).</span><span class="sxs-lookup"><span data-stu-id="51715-p156">**Note**  While you are debugging the SharePoint Add-in, the Office Developer Tools for Visual Studio re-register it with Azure ACS each time you press F5 in Visual Studio. When you stage the SharePoint Add-in, you have to give it a long-term registration. See the section  [Modify the add-in and stage it to Azure and Office 365](#Stage).</span></span>
 


## <a name="modify-the-add-in-and-stage-it-to-azure-and-office-365"></a><span data-ttu-id="51715-322">Ändern des Add-Ins und Bereitstellen für Azure und Office 365</span><span class="sxs-lookup"><span data-stu-id="51715-322">Modify the add-in and stage it to Azure and Office 365</span></span>
<span data-ttu-id="51715-323"><a name="Stage"> </a></span><span class="sxs-lookup"><span data-stu-id="51715-323"></span></span>

<span data-ttu-id="51715-324">Wenn Sie das Debugging des SharePoint-Add-In mit F5 in Visual Studio abgeschlossen haben, müssen Sie die ASP.NET-Anwendung an eine tatsächliche Azure-Website bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="51715-324">When you have finished debugging the SharePoint Add-in using F5 in Visual Studio, you need to deploy the ASP.NET application to an actual Azure Web Site.</span></span>
 

 

### <a name="create-the-azure-web-site"></a><span data-ttu-id="51715-325">Erstellen der Azure-Website</span><span class="sxs-lookup"><span data-stu-id="51715-325">Create the Azure Web Site</span></span>


1. <span data-ttu-id="51715-326">Öffnen Sie im Microsoft Azure-Portal in der linken Navigationsleiste den Eintrag **WEBSITES**.</span><span class="sxs-lookup"><span data-stu-id="51715-326">In the Microsoft Azure portal, open  **WEB SITES** on the left navigation bar.</span></span>
    
 
2. <span data-ttu-id="51715-327">Klicken Sie im unteren Bereich der Seite auf **NEU**, und wählen Sie im Dialogfeld **NEU** die Option **WEBSITE** |**SCHNELLERFASSUNG** aus.</span><span class="sxs-lookup"><span data-stu-id="51715-327">Click  **NEW** at the bottom of the page and on the **NEW** dialog select **WEB SITE** |**QUICK CREATE**.</span></span>
    
 
3. <span data-ttu-id="51715-p157">Geben Sie einen Domänennamen ein, und klicken Sie auf **WEBSITE ERSTELLEN**. Kopieren Sie die URL der neuen Website. Diese hat das Format `my_domain.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="51715-p157">Enter a domain name and click  **CREATE WEB SITE**. Make a copy of the new site's URL. It will have the form  `my_domain.azurewebsites.net`.</span></span>
    
 

### <a name="modify-the-code-and-markup-in-the-application"></a><span data-ttu-id="51715-331">Ändern des Codes und Markups in der Anwendung</span><span class="sxs-lookup"><span data-stu-id="51715-331">Modify the code and markup in the application</span></span>


1. <span data-ttu-id="51715-332">Entfernen Sie in Visual Studio die Zeile `ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;` aus der Datei „Default.aspx.cs“.</span><span class="sxs-lookup"><span data-stu-id="51715-332">In Visual Studio, remove the line  `ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;` from the Default.aspx.cs file.</span></span>
    
 
2. <span data-ttu-id="51715-p158">Öffnen Sie die Datei „web.config“ des ASP.NET-Projekts, und ändern Sie den Domänenteil des Werts für den **AppRedirectUrl**-Schlüssel im Abschnitt **appSettings** in die Domäne der Azure-Website. Ändern Sie beispielsweise `<add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />` in `<add key="AppRedirectUrl" value="https://my_domain.azurewebsites.net/Pages/Default.aspx" />`.</span><span class="sxs-lookup"><span data-stu-id="51715-p158">Open the web.config file of the ASP.NET project and change the domain part of the value of the  **AppRedirectUrl** key in the **appSettings** section to the domain of the Azure Web Site. For example, change `<add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />` to `<add key="AppRedirectUrl" value="https://my_domain.azurewebsites.net/Pages/Default.aspx" />`.</span></span>
    
 
3. <span data-ttu-id="51715-335">Klicken Sie mit der rechten Maustaste auf die Datei AppManifest.xml im SharePoint-Add-In-Projekt, und wählen Sie **Code anzeigen** aus.</span><span class="sxs-lookup"><span data-stu-id="51715-335">Right-click the AppManifest.xml file in the SharePoint Add-in project and select  **View Code**.</span></span>
    
 
4. <span data-ttu-id="51715-p159">Ersetzen Sie im Wert **StartPage** die Zeichenfolge `~remoteAppUrl` durch die vollständige Domäne der Azure-Website, einschließlich Protokoll, z. B. `https://my_domain.azurewebsites.net`. Der gesamte **StartPage**-Wert sollte jetzt wie folgt aussehen: `https://my_domain.azurewebsites.net/Pages/Default.aspx`. (Normalerweise ist der **StartPage**-Wert identisch mit dem Wert des **AppRedirectUrl**-Schlüssels in der Datei „web.config“.)</span><span class="sxs-lookup"><span data-stu-id="51715-p159">In the  **StartPage** value, replace the string `~remoteAppUrl` with the full domain of the Azure Web Site including the protocol; for example `https://my_domain.azurewebsites.net`. The entire  **StartPage** value should now be: `https://my_domain.azurewebsites.net/Pages/Default.aspx`. (Usually, the  **StartPage** value is exactly the same as the value of the **AppRedirectUrl** key in the web.config file.)</span></span>
    
 

### <a name="modify-the-aad-registration-and-register-the-add-in-with-acs"></a><span data-ttu-id="51715-339">Ändern der AAD-Registrierung und Registrieren des Add-Ins bei ACS</span><span class="sxs-lookup"><span data-stu-id="51715-339">Modify the AAD registration and register the add-in with ACS</span></span>


1. <span data-ttu-id="51715-340">Melden Sie sich mit Ihrem Azure-Administratorkonto beim [Azure-Verwaltungsportal](https://manage.windowsazure.com) an.</span><span class="sxs-lookup"><span data-stu-id="51715-340">Login into  [Azure Management portal](https://manage.windowsazure.com) with your Azure administrator account.</span></span>
    
 
2. <span data-ttu-id="51715-341">Wählen Sie auf der linken Seite **Active Directory** aus.</span><span class="sxs-lookup"><span data-stu-id="51715-341">Choose  **Active Directory** on the left side.</span></span>
    
 
3. <span data-ttu-id="51715-342">Klicken Sie auf Ihr Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="51715-342">Click on your directory.</span></span>
    
 
4. <span data-ttu-id="51715-343">Wählen Sie **ANWENDUNGEN** (in der obersten Navigationsleiste) aus.</span><span class="sxs-lookup"><span data-stu-id="51715-343">Choose  **APPLICATIONS** (on the top navigation bar).</span></span>
    
 
5. <span data-ttu-id="51715-p160">Öffnen Sie die von Ihnen erstellte Anwendung. Im fortlaufenden Beispiel ist das **ContosoAutomobileCollection**.</span><span class="sxs-lookup"><span data-stu-id="51715-p160">Open the application you created. In the continuing example, it is  **ContosoAutomobileCollection**.</span></span>
    
 
6. <span data-ttu-id="51715-346">Ändern Sie für jeden der folgenden Werte den Teil „localhost:*port*“ des Werts in die Domäne Ihrer neuen Azure-Website:</span><span class="sxs-lookup"><span data-stu-id="51715-346">For each of the following values, change the "localhost: *port*  " part of the value to the domain of your new Azure Web Site:</span></span>
    
      -  <span data-ttu-id="51715-347">**ANMELDE-URL**</span><span class="sxs-lookup"><span data-stu-id="51715-347">**SIGN-ON URL**</span></span>
    
 
  -  <span data-ttu-id="51715-348">**APP-ID-URI**</span><span class="sxs-lookup"><span data-stu-id="51715-348">**APP ID URI**</span></span>
    
 
  -  <span data-ttu-id="51715-349">**ANTWORT-URL**</span><span class="sxs-lookup"><span data-stu-id="51715-349">**REPLY URL**</span></span>
    
 

    <span data-ttu-id="51715-350">Wenn beispielsweise der **APP-ID-URI****https://localhost:44304/ContosoAutomobileCollection** ist, ändern Sie ihn in **https://<my_domain>.azurewebsites.net/ContosoAutomobileCollection**.</span><span class="sxs-lookup"><span data-stu-id="51715-350">For example, if the  **APP ID URI** is **https://localhost:44304/ContosoAutomobileCollection**, change it to  **https://<my_domain>.azurewebsites.net/ContosoAutomobileCollection**.</span></span>
    
 
7. <span data-ttu-id="51715-351">Klicken Sie unten im Bildschirm auf **SPEICHERN**.</span><span class="sxs-lookup"><span data-stu-id="51715-351">Click  **SAVE** at the bottom of the screen.</span></span>
    
 
8. <span data-ttu-id="51715-p161">Sie das Add-In bei Azure ACS. Dies muss auch dann durchgeführt werden, wenn das Add-In nicht auf SharePoint zugreift und keine Token von ACS verwendet, da derselbe Prozess das Add-In auch beim App-Verwaltungsdienst des Office 365-Abonnements registriert, was erforderlich ist. (Er wird als „App-Verwaltungsdienst“ bezeichnet, da SharePoint-Add-Ins ursprünglich „Apps für SharePoint“ hießen). Sie führen die Registrierung auf der Seite „AppRegNew.aspx“ einer beliebigen SharePoint-Website im Office 365-Abonnement durch. Ausführliche Informationen finden Sie unter [Registrieren von SharePoint-Add-Ins 2013](register-sharepoint-add-ins.md). Im Rahmen dieses Prozesses erhalten Sie eine neue Client-ID und einen neuen geheimen Clientschlüssel. Geben Sie diese Werte in die Datei „web.config“ für die Schlüssel **ClientId** (nicht **ida:ClientID**) und **ClientSecret** ein.</span><span class="sxs-lookup"><span data-stu-id="51715-p161">Register the add-in with Azure ACS. This must be done even if the add-in does not access SharePoint and will not use tokens from ACS, because the same process also registers the add-in with the Add-in Management Service of the Office 365 subscription, which is a requirement. (It is called "Add-in Management Service" because SharePoint Add-ins were originally called "apps for SharePoint".) You perform the registration on the AppRegNew.aspx page of any SharePoint website in the Office 365 subscription. For details, see  [Register SharePoint Add-ins 2013](register-sharepoint-add-ins.md). As part of this process you will obtain a new client ID and client secret. Insert these values in the web.config for the  **ClientId** (not **ida:ClientID**) and  **ClientSecret** keys.</span></span>
    
     <span data-ttu-id="51715-p162">**Vorsicht** Wenn Sie aus irgendeinem Grund nach dieser Änderung F5 drücken, überschreiben die Office Developer Tools für Visual Studio einen oder beide dieser Werte. Aus diesem Grund sollten Sie die mit „AppRegNew.aspx“ abgerufenen Werte aufzeichnen und immer sicherstellen, dass die Werte in der „web.config“ korrekt sind, kurz bevor Sie die ASP.NET-Anwendung veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="51715-p162">**Caution**  If for any reason you press F5 after making this change, the Office Developer Tools for Visual Studio will overwrite one or both of these values. For that reason, you should keep a record of the values obtained with AppRegNew.aspx and always verify that the values in the web.config are correct just before you publish the ASP.NET application.</span></span> 

### <a name="publish-the-aspnet-application-to-azure-and-install-the-add-in-to-sharepoint"></a><span data-ttu-id="51715-360">Veröffentlichen der ASP.NET-Anwendung in Azure und Installieren des SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="51715-360">Publish the ASP.NET application to Azure and install the add-in to SharePoint</span></span>


1. <span data-ttu-id="51715-p163">Es gibt verschiedene Möglichkeiten, eine ASP.NET-Anwendung an eine Azure-Website zu veröffentlichen. Weitere Informationen finden Sie unter  [Bereitstellen einer Azure-Website](http://azure.microsoft.com/de-DE/documentation/articles/web-sites-deploy/).</span><span class="sxs-lookup"><span data-stu-id="51715-p163">There are several ways to publish an ASP.NET application to an Azure Web Site. For more information, see  [How to Deploy an Azure Web Site](http://azure.microsoft.com/de-DE/documentation/articles/web-sites-deploy/).</span></span>
    
 
2. <span data-ttu-id="51715-p164">Klicken Sie in Visual Studio mit der rechten Maustaste auf das SharePoint-Add-In-Projekt, und wählen Sie **Paket** aus. Klicken Sie auf der sich öffnenden Seite **Add-In veröffentlichen** auf **Add-In verpacken**. Der Datei-Explorer öffnet sich im Ordner mit dem Add-In-Paket.</span><span class="sxs-lookup"><span data-stu-id="51715-p164">In Visual Studio, right-click the SharePoint add-in project and select  **Package**. On the  **Publish your add-in** page that opens, click **Package the add-in**. File explorer opens to the folder with the add-in package.</span></span>
    
 
3. <span data-ttu-id="51715-p165">Melden Sie sich bei Office 365 als globaler Administrator an, und navigieren Sie zur App-Katalog-Websitesammlung der Organisation. (Falls keine vorhanden ist, erstellen Sie eine. Informationen finden Sie unter  [Verwenden des App-Katalogs zur Bereitstellung von benutzerdefinierten Geschäfts-Apps für Ihre SharePoint Online-Umgebung](http://office.microsoft.com/de-DE/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).)</span><span class="sxs-lookup"><span data-stu-id="51715-p165">Login to Office 365 as a global administrator, and navigate to the organization add-in catalog site collection. (If there isn't one, create it. See  [Use the Add-in Catalog to make custom business add-ins available for your SharePoint Online environment](http://office.microsoft.com/de-DE/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).)</span></span>
    
 
4. <span data-ttu-id="51715-369">Laden Sie das Add-In in den Add-In-Katalog hoch.</span><span class="sxs-lookup"><span data-stu-id="51715-369">Upload the add-in package to the add-in catalog.</span></span>
    
 
5. <span data-ttu-id="51715-370">Navigieren Sie zur Seite **Websiteinhalt** einer beliebigen Website im Abonnement, und klicken Sie auf **Add-In hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="51715-370">Navigate to the  **Site Contents** page of any website in the subscription and click **add an add-in**.</span></span>
    
 
6. <span data-ttu-id="51715-371">Scrollen Sie auf der Seite **Ihre Add-Ins** zum Abschnitt **Add-Ins, die Sie hinzufügen können**, und klicken Sie auf das Symbol für Ihr Add-In.</span><span class="sxs-lookup"><span data-stu-id="51715-371">On the  **Your Add-ins** page, scroll to the **Add-ins you can add** section and click the icon for your add-in.</span></span>
    
 
7. <span data-ttu-id="51715-372">Nachdem das Add-In installiert wurde, klicken Sie auf das zugehörige Symbol auf der Seite **Websiteinhalt**, um das Add-In zu starten.</span><span class="sxs-lookup"><span data-stu-id="51715-372">After the add-in has installed, click it's icon on the  **Site Contents** page to launch the add-in.</span></span>
    
 
<span data-ttu-id="51715-373">Unter [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) finden Sie weitere Informationen über die Installation von SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="51715-373">For more information about installing SharePoint Add-ins, see  [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options.md).</span></span>
 

## <a name="deploying-the-add-in-to-production"></a><span data-ttu-id="51715-374">Bereitstellen des Add-Ins an die Produktion</span><span class="sxs-lookup"><span data-stu-id="51715-374">Deploying the add-in to production</span></span>
<span data-ttu-id="51715-375"><a name="Stage"> </a></span><span class="sxs-lookup"><span data-stu-id="51715-375"></span></span>

<span data-ttu-id="51715-p166">Wenn Sie alle Tests abgeschlossen haben, können Sie das Add-In in Produktion bereitstellen. Dafür sind möglicherweise einige Änderungen erforderlich.</span><span class="sxs-lookup"><span data-stu-id="51715-p166">When you have finished all testing you can deploy the add-in in production. This may require some changes.</span></span>
 

 

1. <span data-ttu-id="51715-p167">Wenn die Produktionsdomäne der ASP.NET-Anwendung eine andere als die Stagingdomäne ist, müssen Sie den **AppRedirectUrl**-Wert in der Datei „web.config“ und den **StartPage**-Wert in der Datei „AppManifest.xml“ ändern und das SharePoint-Add-In erneut packen. Informationen dazu finden Sie im Verfahren **Ändern des Codes und Markups in der Anwendung** weiter oben.</span><span class="sxs-lookup"><span data-stu-id="51715-p167">If the production domain of the ASP.NET application is different from the staging domain, you will have to change  **AppRedirectUrl** value in the web.config and the **StartPage** value in the AppManifest.xml file, and repackage the SharePoint Add-in. See the procedure **Modify the code and markup in the application** above.</span></span>
    
 
2. <span data-ttu-id="51715-p168">Durch die Domänenänderung müssen Sie außerdem die Add-In-Registrierung bei AAD ändern. Informationen dazu finden Sie im Verfahren **Ändern der AAD-Registrierung und Registrieren des Add-Ins bei ACS** weiter oben.</span><span class="sxs-lookup"><span data-stu-id="51715-p168">The change in domain also requires that you edit the add-ins registration with AAD. See the procedure  **Modify the AAD registration and register the add-in with ACS** above.</span></span>
    
 
3. <span data-ttu-id="51715-p169">Durch die Domänenänderung müssen Sie zudem das Add-In erneut bei ACS (und dem App-Verwaltungsdienst des Abonnements) registrieren, wie im selben Verfahren beschrieben wird. (Es gibt keine Möglichkeit, die Registrierung eines Add-Ins bei ACS zu *bearbeiten*.) Es ist allerdings nicht erforderlich, eine neue Client-ID oder einen neuen geheimen Clientschlüssel auf der Seite „AppRegNew.aspx“ zu generieren. Sie können die ursprünglichen Werte aus den Schlüsseln **ClientId** (nicht **ida:ClientID**) und **ClientSecret** der „web.config“ in das AppRegNew-Formular kopieren. *Wenn Sie neue Werte generieren, achten Sie darauf, dass Sie die neuen Werte in die Schlüssel in der „web.config“ kopieren.*</span><span class="sxs-lookup"><span data-stu-id="51715-p169">The change in domain also requires that you re-register the add-in with ACS (and the subscription's Add-in Management Service) as described in the same procedure. (There is no way to  *edit*  an add-in's registration with ACS.) However, it is not necessary to generate a new client ID or client secret on the AppRegNew.aspx page. You can copy the original values from the **ClientId** (not **ida:ClientID**) and  **ClientSecret** keys of the web.config into the AppRegNew form. *If you do generate new ones, be sure to copy the new values to the keys in web.config.*</span></span> 
    
 

