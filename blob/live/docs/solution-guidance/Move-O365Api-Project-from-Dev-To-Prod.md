---
title: 'Bereitstellen von Websites in Office 365 Development in Microsoft Azure #'
ms.date: 11/03/2017
ms.openlocfilehash: c7e975f54da33125d6e8261efa1b525ba525747d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="deploying-development-office-365-sites-to-microsoft-azure"></a><span data-ttu-id="e5b93-102">Bereitstellen von Websites in Office 365 Development in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e5b93-102">Deploying Development Office 365 Sites to Microsoft Azure</span></span> #

### <a name="summary"></a><span data-ttu-id="e5b93-103">Summary</span><span class="sxs-lookup"><span data-stu-id="e5b93-103">Summary</span></span> ###

<span data-ttu-id="e5b93-104">Bei der Entwicklung von beliebigen Typs aus einer Webanwendung, ist die meisten Entwicklung lokal mit http://localhost durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="e5b93-104">When developing any type a web application, most development is done locally using http://localhost.</span></span> <span data-ttu-id="e5b93-105">Einige Projekte verwenden Sie lokale Ressourcen oder eine Kombination von Ressourcen für lokale und Remoteverbindungen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-105">Some projects use local resources or a mix of local and remote resources.</span></span> <span data-ttu-id="e5b93-106">Nutzen diese Projekte aus lokalen entwicklungsumgebungen umfasst eine Reihe von Aufgaben ausführen, wie beispielsweise das Ändern der Datenbank-Verbindungszeichenfolgen, URLs, Konfigurationen usw..</span><span class="sxs-lookup"><span data-stu-id="e5b93-106">Taking these projects from local development environments involves a handful of tasks to perform like changing database connection strings, URLs, configurations, etc.</span></span>

<span data-ttu-id="e5b93-107">Web, Projekte, die die Office 365-APIs nutzen unterscheiden sich nicht.</span><span class="sxs-lookup"><span data-stu-id="e5b93-107">Web projects that leverage the Office 365 APIs are no different.</span></span> <span data-ttu-id="e5b93-108">Diese Projekte nutzen von Microsoft Azure AD-Dienst zum Authentifizieren der Anwendungen und OAuth 2.0-Zugriffstoken zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="e5b93-108">These projects leverage Microsoft's Azure AD service to authenticate the applications and obtain OAuth 2.0 access tokens.</span></span> <span data-ttu-id="e5b93-109">Diese Token werden durch die Webanwendungen zur Authentifizierung mit den Office 365-APIs verwendet.</span><span class="sxs-lookup"><span data-stu-id="e5b93-109">These tokens are used by the web applications to authenticate with the Office 365 APIs.</span></span>

<span data-ttu-id="e5b93-110">Auf dieser Seite erläutert die Schritte zum Offlineschalten einer Office 365-API-Entwicklungsprojekt und starten es an ein Arbeitsbeispiel vollständig in Microsoft Azure mit [Office 365](http://products.office.com/en-us/business/explore-office-365-for-business), [Azure Active Directory](http://azure.microsoft.com/en-us/services/active-directory/) & [Azure Websites] (http:// gehostet Azure.Microsoft.com/en-US/Services/Websites/.</span><span class="sxs-lookup"><span data-stu-id="e5b93-110">This page explains the steps involved in taking an Office 365 API development project and launching it to a working sample hosted entirely in Microsoft Azure using [Office 365](http://products.office.com/en-us/business/explore-office-365-for-business), [Azure Active Directory](http://azure.microsoft.com/en-us/services/active-directory/) & [Azure Websites](http://azure.microsoft.com/en-us/services/websites/.</span></span>

<span data-ttu-id="e5b93-111">Bereitstellen einer Office 365-API-Web-Anwendung in Microsoft Azure aus einer lokalen Entwicklungsumgebung muss drei allgemeine Schritte ausgeführt werden, wie auf dieser Seite beschrieben:</span><span class="sxs-lookup"><span data-stu-id="e5b93-111">Deploying an Office 365 API web application to Microsoft Azure from a local development environment requires three high-level steps to be performed as outlined in this page:</span></span>

- [<span data-ttu-id="e5b93-112">Erstellen und Konfigurieren einer Azure-Website</span><span class="sxs-lookup"><span data-stu-id="e5b93-112">Create and Configure an Azure Website</span></span>](#create-and-configure-an-azure-website)
- [<span data-ttu-id="e5b93-113">Konfigurieren der Azure AD-Anwendung</span><span class="sxs-lookup"><span data-stu-id="e5b93-113">Configure the Azure AD Application</span></span>](#configure-the-azure-ad-application)
- [<span data-ttu-id="e5b93-114">Konfigurieren Sie das Projekt ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e5b93-114">Configure the ASP.NET Project</span></span>](#configure-the-aspnet-project)
- [<span data-ttu-id="e5b93-115">Bereitstellen von Office 365-API ASP.NET-Webanwendung</span><span class="sxs-lookup"><span data-stu-id="e5b93-115">Deploy the Office 365 API ASP.NET Web Application</span></span>](#deploy-the-office-365-api-aspnet-web-application)

> <span data-ttu-id="e5b93-116">Auf dieser Seite wird davon ausgegangen, dass Sie eine lokale Arbeiten ASP.NET-Anwendung verfügen, die die Office 365-APIs verwendet.</span><span class="sxs-lookup"><span data-stu-id="e5b93-116">This page assumes that you have a local working ASP.NET application that uses the Office 365 APIs.</span></span> <span data-ttu-id="e5b93-117">Zur Referenz wird das **[O365-WebApp-SingleTenant](https://github.com/SharePoint/O365-WebApp-SingleTenant)** das Projekt wurde gefunden in **[OfficeDev](https://github.com/SharePoint)** Konto GitHub verwendet.</span><span class="sxs-lookup"><span data-stu-id="e5b93-117">For reference, it will use the **[O365-WebApp-SingleTenant](https://github.com/SharePoint/O365-WebApp-SingleTenant)** project found in the **[OfficeDev](https://github.com/SharePoint)** account in GitHub.</span></span>

# <a name="create-and-configure-an-azure-website"></a><span data-ttu-id="e5b93-118">Erstellen und Konfigurieren einer Azure-Website</span><span class="sxs-lookup"><span data-stu-id="e5b93-118">Create and Configure an Azure Website</span></span>

<span data-ttu-id="e5b93-119">In diesem Schritt erstellen Sie eine Azure-Website, die zum Hosten der Anwendung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e5b93-119">In this step you will create an Azure website that will be used to host the web application.</span></span> 

1. <span data-ttu-id="e5b93-120">Navigieren Sie zu der [Azure-Verwaltungsportal](https://manage.windowsazure.com) und melden Sie sich mit Ihrem Organisations-ID-Konto.</span><span class="sxs-lookup"><span data-stu-id="e5b93-120">Navigate to the [Azure Management Portal](https://manage.windowsazure.com) and login using your Organization ID account.</span></span>
1. <span data-ttu-id="e5b93-121">Wählen Sie nach der Anmeldung in der Navigation Randleiste **WEBSITES**.</span><span class="sxs-lookup"><span data-stu-id="e5b93-121">After logging in, using the navigation sidebar, select **WEBSITES**.</span></span>
1. <span data-ttu-id="e5b93-122">Klicken Sie auf der Seite **Websites** auf den Link **neu** in der Fußzeile in der unteren linken Ecke der Seite gefunden.</span><span class="sxs-lookup"><span data-stu-id="e5b93-122">On the **websites** page, click the **NEW** link in the footer found in the lower-left corner of the page.</span></span>
1. <span data-ttu-id="e5b93-123">Der Assistent, der angezeigt wird, wählen Sie **Für schnelles Erstellen**, geben Sie einen Namen für die Website im Feld **URL** wählen Sie in einer **Web-Hosting planen** und **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e5b93-123">In the wizard that appears, select **Quick Create**, enter a name for the site in the **URL** field, select a **Web Hosting Plan** and **Subscription**.</span></span> 

  ![Die Einstellungen für schnelles erstellen: das URL-Feld o365api-01 festgelegt ist, Web-Hosting planen auf Default1 festgelegt ist (ostasiatischen US, Standard) Abonnement auf Azure MSDN (primär) festgelegt ist.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-01.png)

  > <span data-ttu-id="e5b93-125">Stellen Sie sicher, dass Sie notieren Sie den Namen der Website beibehalten, den Sie erstellen, wie es später benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="e5b93-125">Make sure to keep a note of the name of the website you create as it will be needed later.</span></span>

1. <span data-ttu-id="e5b93-126">Klicken Sie dann auf den Link **Website erstellen** , um die Website zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-126">Finally click the **Create Website** link to create the site.</span></span>

<span data-ttu-id="e5b93-127">Geben Sie Azure einen Moment Zeit, um die Website zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-127">Give Azure a few moments to create the site.</span></span> <span data-ttu-id="e5b93-128">Nach dem Erstellen der Website können Sie die *app-Einstellungen* über die Webschnittstelle angeben.</span><span class="sxs-lookup"><span data-stu-id="e5b93-128">After creating the site you can specify *app settings* through the web interface.</span></span> <span data-ttu-id="e5b93-129">Hiermit können Sie alle außer Kraft setzen `<appSettings>` innerhalb des Projekts `web.config` Datei über die Verwaltung der Weboberfläche für die Website ohne die Bereitstellung von Ihrer Website Codebasis für einfache `web.config` Änderungen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-129">This allows you to override any `<appSettings>` within the project's `web.config` file through the web administration interface for the website without deploying your site codebase for simple `web.config` changes.</span></span>

1. <span data-ttu-id="e5b93-130">Klicken Sie auf der Website, die Sie gerade erstellt, in der **Azure-Verwaltungsportal haben**.</span><span class="sxs-lookup"><span data-stu-id="e5b93-130">Click the website that you just created within the **Azure Management Portal**.</span></span>
1. <span data-ttu-id="e5b93-131">Klicken Sie auf den Link **Konfigurieren** in der oberen Navigationsleiste.</span><span class="sxs-lookup"><span data-stu-id="e5b93-131">CLick the **CONFIGURE** link in the top navigation.</span></span>
1. <span data-ttu-id="e5b93-132">Führen Sie einen Bildlauf nach unten zum Abschnitt **App-Einstellungen** , und fügen Sie drei neue Einträge hinzu:</span><span class="sxs-lookup"><span data-stu-id="e5b93-132">Scroll down to the **App Settings** section and add three new entries:</span></span>
  - <span data-ttu-id="e5b93-133">**IDA: ClientID**</span><span class="sxs-lookup"><span data-stu-id="e5b93-133">**ida:ClientID**</span></span>
  - <span data-ttu-id="e5b93-134">**IDA: Kennwort**</span><span class="sxs-lookup"><span data-stu-id="e5b93-134">**ida:Password**</span></span> 
  - <span data-ttu-id="e5b93-135">**IDA: TenantID**</span><span class="sxs-lookup"><span data-stu-id="e5b93-135">**ida:TenantID**</span></span> 
1. <span data-ttu-id="e5b93-136">Kopieren Sie die entsprechenden Werte aus des arbeiten Projekts `web.config` auf diese Einstellungswerte in der Azure-Website wie in der folgenden Abbildung dargestellt:</span><span class="sxs-lookup"><span data-stu-id="e5b93-136">Copy the corresponding values from the working project's `web.config` to these settings values in your Azure website as shown in the following figure:</span></span>

  ![WEBSITE_NODE_DEFAULT_VERSION ist 0.10.32, Ida: ClientID 92b1e137-c36f-4bfe-9e1c-01ef546ce4a9, Ida: Kennwort ist Bns06N18ZiyYfMcyU9qUfGnZbnkBiPZfUptLDsU6cml, Ida: TenantId ist teilweise geschwärzten.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-02.png)

1. <span data-ttu-id="e5b93-139">Klicken Sie in der Fußzeile auf die Schaltfläche **Speichern** , um die Änderungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="e5b93-139">In the footer, click the **SAVE** button to save your changes.</span></span>

<span data-ttu-id="e5b93-140">Zu diesem Zeitpunkt die Azure-Website wird Setup und so konfiguriert, dass das Office 365-API-Webprojekt hosten, das die in einem späteren Schritt bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="e5b93-140">At this point the Azure website is setup and configured to host the Office 365 API web project that you will deploy in a later step.</span></span>

[<span data-ttu-id="e5b93-141">zurück zum Seitenanfang</span><span class="sxs-lookup"><span data-stu-id="e5b93-141">back to top</span></span>](#deploying-development-office-365-sites-to-microsoft-azure)

# <a name="configure-the-azure-ad-application"></a><span data-ttu-id="e5b93-142">Konfigurieren der Azure AD-Anwendung</span><span class="sxs-lookup"><span data-stu-id="e5b93-142">Configure the Azure AD Application</span></span>

<span data-ttu-id="e5b93-143">In diesem Schritt ändern Sie die Azure AD-Anwendung verwendet bei der Entwicklung und Testen der Anwendung Office 365.</span><span class="sxs-lookup"><span data-stu-id="e5b93-143">In this step you will modify the Azure AD application used in the development & testing of the Office 365 application.</span></span>

1. <span data-ttu-id="e5b93-144">Navigieren Sie zu der [Azure-Verwaltungsportal](https://manage.windowsazure.com) und melden Sie sich mit Ihrem Organisations-ID-Konto.</span><span class="sxs-lookup"><span data-stu-id="e5b93-144">Navigate to the [Azure Management Portal](https://manage.windowsazure.com) and login using your Organization ID account.</span></span>
1. <span data-ttu-id="e5b93-145">Wählen Sie nach der Anmeldung in der Navigation Randleiste mit **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="e5b93-145">After logging in, using the navigation sidebar, select **ACTIVE DIRECTORY**.</span></span>
1. <span data-ttu-id="e5b93-146">Wählen Sie auf der Seite **active Directory** das Verzeichnis, das mit Ihrem Office 365-Mandanten verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="e5b93-146">On the **active directory** page, select the directory that is linked to your Office 365 tenant.</span></span>
1. <span data-ttu-id="e5b93-147">Klicken Sie anschließend auf das **ANWENDUNGEN** -Element in der oberen Navigationsleiste.</span><span class="sxs-lookup"><span data-stu-id="e5b93-147">Next, click the **APPLICATIONS** item in the top navigation.</span></span>
1. <span data-ttu-id="e5b93-148">Aktualisieren Sie innerhalb des Abschnitts **Eigenschaften** die **SIGN-ON URL** So zeigen Sie auf der Standard-URL der Azure-Website, die Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="e5b93-148">Within the **Properties** section, update the **SIGN-ON URL** to point to the default URL of the Azure Website you created.</span></span> <span data-ttu-id="e5b93-149">Beachten Sie den HTTPS-Endpunkt, der bereitgestellt wird mit allen Azure Websites verwenden.</span><span class="sxs-lookup"><span data-stu-id="e5b93-149">Take note to use the HTTPS endpoint that is provided with all Azure websites.</span></span>

  ![Name auf Office 365-WebApp-SingleTenant.Office365App festgelegt ist, Sign-on URL auf https://o365api-01.azurewebsites.net festgelegt ist](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-03.png)

1. <span data-ttu-id="e5b93-151">Aktualisieren Sie innerhalb des Abschnitts **Single Sign-On** der **App ID URI** hinzufügt, um die Domäne der Azure-Website (in der folgenden Abbildung dargestellt) verwenden.</span><span class="sxs-lookup"><span data-stu-id="e5b93-151">Within the **Single Sign-On** section, update the **App ID URI** to use the domain for the Azure website (shown in the following figure).</span></span>
1. <span data-ttu-id="e5b93-152">Aktualisieren Sie die **Antwort-URL** im nächsten Schritt, daher ist die einzige aufgelistete URL der Homepage der Azure-Website:</span><span class="sxs-lookup"><span data-stu-id="e5b93-152">Next, update the **REPLY URL** so the only URL listed is the homepage of the Azure website:</span></span>

  ![App-ID URI ist https://o365api-01.azurewebsites.net/O365-WebApp-SingleTenant, Antwort-URL ist https://o365api-01.azurewebsites.net/](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-04.png)

1. <span data-ttu-id="e5b93-154">Klicken Sie in der Fußzeile auf die Schaltfläche **Speichern** , um die Änderungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="e5b93-154">In the footer, click the **SAVE** button to save your changes.</span></span>

<span data-ttu-id="e5b93-155">Zu diesem Zeitpunkt wurde die Azure AD-Anwendung, die vom Office 365-API-Web-Projekt verwendet, um die neue Azure-Website entwickelt konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="e5b93-155">At this point, the Azure AD application used by the Office 365 API web project has been configured to work with the new Azure website.</span></span>

[<span data-ttu-id="e5b93-156">zurück zum Seitenanfang</span><span class="sxs-lookup"><span data-stu-id="e5b93-156">back to top</span></span>](#deploying-development-office-365-sites-to-microsoft-azure)

# <a name="configure-the-aspnet-project"></a><span data-ttu-id="e5b93-157">Konfigurieren Sie das Projekt ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e5b93-157">Configure the ASP.NET Project</span></span>

<span data-ttu-id="e5b93-158">In diesem Schritt konfigurieren Sie das Projekt ASP.NET in der Anwendung in die neue Azure-Website verwenden.</span><span class="sxs-lookup"><span data-stu-id="e5b93-158">In this step you will configure the ASP.NET project in your application to use the new Azure Website.</span></span>

<span data-ttu-id="e5b93-159">Für die beispielanwendung im Beispiel für diese Anweisungen verwendet ist kein zusätzlicher Aufwand tatsächlich erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="e5b93-159">For the sample application used in the example for this guidance, no extra work is actually required.</span></span> <span data-ttu-id="e5b93-160">Enthält jedoch die Webanwendung die Einstellungen in der `web.config` Datei für die Azure AD-Anwendung und Azure AD-Mandanten bei der Entwicklung verwendet.</span><span class="sxs-lookup"><span data-stu-id="e5b93-160">However the web application does contain the settings within the `web.config` file for the Azure AD application and Azure AD tenant used during development.</span></span> <span data-ttu-id="e5b93-161">Einige Entwickler können mit verschiedenen Azure AD-Applikationen oder sogar auf verschiedene Azure-Abonnements für ihre Entwicklung und Produktion Instanzen auswählen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-161">Some developers may choose to use different Azure AD applications or even different Azure subscriptions for their development and production instances.</span></span>

<span data-ttu-id="e5b93-162">In einem vorherigen Schritt auf dieser Seite beschrieben, bei der Erstellung der Azure-Website festlegen die Add-in-Einstellungen für die Anwendung, die in der Regel im gefunden wird die `web.config`.</span><span class="sxs-lookup"><span data-stu-id="e5b93-162">In a previous step outlined in this page, when you created the Azure website you set the add-in settings for the application that are typically found in the `web.config`.</span></span> <span data-ttu-id="e5b93-163">Zur Sicherstellung der Anwendung erhält diese Werte aus der Azure-Website Konfiguration empfohlen wird Sie ersetzen Sie die Werte in der `web.config` mit Platzhalter stattdessen Werte.</span><span class="sxs-lookup"><span data-stu-id="e5b93-163">To ensure the web application receives these values from the Azure website configuration, it's recommended you replace the values within the `web.config` with placeholder values instead.</span></span>

1. <span data-ttu-id="e5b93-164">Öffnen Sie das Projekt `web.config` Datei.</span><span class="sxs-lookup"><span data-stu-id="e5b93-164">Open the project's `web.config` file.</span></span>
1. <span data-ttu-id="e5b93-165">Suchen Sie die Add-in-Einstellungen für **Ida: ClientID**, **Ida: Kennwort** und **Ida: TenantId**.</span><span class="sxs-lookup"><span data-stu-id="e5b93-165">Locate the add-in settings for the **ida:ClientID**, **ida:Password** and **ida:TenantId**.</span></span>
1. <span data-ttu-id="e5b93-166">Ersetzen Sie die Werte dieser Einstellungen mit einem Platzhalterwert:</span><span class="sxs-lookup"><span data-stu-id="e5b93-166">Replace the values of these settings with a placeholder value:</span></span>

  ````xml
  <add key="ida:TenantId" value="set-in-azure-website-config" />
  <add key="ida:ClientID" value="set-in-azure-website-config" />
  <add key="ida:Password" value="set-in-azure-website-config" />
  ````

1. <span data-ttu-id="e5b93-167">Speichern Sie die Änderungen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-167">Save your changes.</span></span>

<span data-ttu-id="e5b93-168">Die Webanwendung, Azure-Website und in Azure AD-Anwendung sind zu diesem Zeitpunkt alle ordnungsgemäß konfiguriert und bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="e5b93-168">At this point the web application, Azure website & application in Azure AD are all configured correctly and ready to be deployed.</span></span>

[<span data-ttu-id="e5b93-169">zurück zum Seitenanfang</span><span class="sxs-lookup"><span data-stu-id="e5b93-169">back to top</span></span>](#deploying-development-office-365-sites-to-microsoft-azure)

# <a name="deploy-the-office-365-api-aspnet-web-application"></a><span data-ttu-id="e5b93-170">Bereitstellen von Office 365-API ASP.NET-Webanwendung</span><span class="sxs-lookup"><span data-stu-id="e5b93-170">Deploy the Office 365 API ASP.NET Web Application</span></span>

<span data-ttu-id="e5b93-171">In diesem Schritt werden Sie Office 365-API-Webanwendung an, der Azure-Website veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-171">In this step you will publish the Office 365 API web application to the Azure website.</span></span> <span data-ttu-id="e5b93-172">Nach der Bereitstellung der Website sollten Sie testen, um sicherzustellen, dass alles wie gewünscht funktioniert.</span><span class="sxs-lookup"><span data-stu-id="e5b93-172">Once the site has been deployed you will test it to ensure everything works as desired.</span></span>

> <span data-ttu-id="e5b93-173">Dieser Schritt wird vorausgesetzt, dass er Microsoft [Azure SDK](http://azure.microsoft.com/en-us/downloads/), Version 2.0 oder höher, installiert.</span><span class="sxs-lookup"><span data-stu-id="e5b93-173">This step assumes you have he Microsoft [Azure SDK](http://azure.microsoft.com/en-us/downloads/), version 2.0 or higher, installed.</span></span> 

## <a name="deploy-the-aspnet-web-application"></a><span data-ttu-id="e5b93-174">Bereitstellen der ASP.NET-Webanwendung</span><span class="sxs-lookup"><span data-stu-id="e5b93-174">Deploy the ASP.NET Web Application</span></span>

1. <span data-ttu-id="e5b93-175">Öffnen Sie Ihre Office 365-API-Webanwendung in Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="e5b93-175">Open your Office 365 API web application in Visual Studio 2013.</span></span>
1. <span data-ttu-id="e5b93-176">Klicken Sie im Fenster Projektmappen-Explorer-Tool mit der rechten Maustaste in des Projekts, und wählen Sie **Veröffentlichen** Starten der **Web veröffentlichen** -Assistent.</span><span class="sxs-lookup"><span data-stu-id="e5b93-176">Within the Solution Explorer tool window, right-click the project and select **Publish** start the **Publish Web** wizard.</span></span>
1. <span data-ttu-id="e5b93-177">Wählen Sie auf der Registerkarte **Profil** **Microsoft Azure-Website**ein.</span><span class="sxs-lookup"><span data-stu-id="e5b93-177">On the **Profile** tab, select **Microsoft Azure Website**.</span></span>

  <span data-ttu-id="e5b93-178">Zu diesem Zeitpunkt werden Sie aufgefordert, zum Azure-Abonnement mit Ihrer Organisation ID anmelden</span><span class="sxs-lookup"><span data-stu-id="e5b93-178">At this point you will be prompted to login to your Azure subscription using your Organization ID.</span></span>

1. <span data-ttu-id="e5b93-179">Wählen Sie nach der Anmeldung die Website, die Sie in einem vorherigen Schritt auf dieser Seite erstellt haben, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5b93-179">After logging in, select the website that you created in a previous step from this page and click **OK**.</span></span>

  ![Im Dialogfeld die vorhandene Website auswählen zeigt, dass für vorhandene Websites o365api-01 festgelegt.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-05.png)

1. <span data-ttu-id="e5b93-181">Klicken Sie auf der Registerkarte **Verbindung** auf die Schaltfläche **Verbindung überprüfen** , um sicherzustellen, das Verbindungsprofil erfolgreich heruntergeladen und angewendet wurde.</span><span class="sxs-lookup"><span data-stu-id="e5b93-181">On the **Connection** tab, click the **Validate Connection** button to ensure the connection profile was successfully downloaded and applied.</span></span>

  ![Ein Pfeil verweist auf die Schaltfläche Verbindung überprüfen unten im Dialogfeld mit ein grünes Häkchen neben der Schaltfläche angezeigt.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-06.png)

1. <span data-ttu-id="e5b93-183">Klicken Sie auf die Schaltfläche **Veröffentlichen** , um die Webanwendung der Azure-Website zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-183">Click the **Publish** button to publish the web application to the Azure website.</span></span>

## <a name="test-the-aspnet-web-application"></a><span data-ttu-id="e5b93-184">Testen Sie die ASP.NET-Webanwendung</span><span class="sxs-lookup"><span data-stu-id="e5b93-184">Test the ASP.NET Web Application</span></span>

<span data-ttu-id="e5b93-185">Nach dem Veröffentlichen der Webanwendung auf der Azure-Website, Visual Studio öffnen ein Browsers und navigieren Sie zur Homepage der Website.</span><span class="sxs-lookup"><span data-stu-id="e5b93-185">After publishing the web application to the Azure website, Visual Studio will open a browser and navigate to the site's homepage.</span></span> 

<span data-ttu-id="e5b93-186">Standardmäßig ist dies der HTTP-Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="e5b93-186">By default this is the HTTP endpoint.</span></span> <span data-ttu-id="e5b93-187">Denken Sie daran aus dem vorherigen Schritt, wenn Sie die Azure AD-Anwendung so konfiguriert, dass nur Anmelde-Ons von HTTPS-Endpunkt akzeptieren festlegen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-187">Recall from the previous step when you configured the Azure AD application that you set it to only accept sign ons from the HTTPS endpoint.</span></span> <span data-ttu-id="e5b93-188">Bevor Sie dem Anwendungsupdate die Url verwenden, um an den HTTPS-Endpunkt zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="e5b93-188">Before you use the application update the url to point to the HTTPS endpoint.</span></span>

1. <span data-ttu-id="e5b93-189">Aktualisieren Sie im Browser die URL So wechseln zur Homepage HTTPS für die Azure-Website ein.</span><span class="sxs-lookup"><span data-stu-id="e5b93-189">In the browser, update the URL to go to the HTTPS homepage for the Azure website.</span></span> <span data-ttu-id="e5b93-190">Im Beispiel auf dieser Seite ist, https://o365api-01.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="e5b93-190">In the example in this page, that is https://o365api-01.azurewebsites.net.</span></span>
1. <span data-ttu-id="e5b93-191">Klicken Sie auf den Link " **Anmelden** " in der Kopfzeile in der oberen rechten Seitenrand.</span><span class="sxs-lookup"><span data-stu-id="e5b93-191">Click the **Sign In** link in the header at the top-right of the page.</span></span> <span data-ttu-id="e5b93-192">Dadurch werden Sie auf der Anmeldeseite angezeigt wird Azure AD weitergeleitet.</span><span class="sxs-lookup"><span data-stu-id="e5b93-192">This will redirect you to the Azure AD sign on page.</span></span>

  > <span data-ttu-id="e5b93-193">Wenn Sie zu diesem Zeitpunkt ein Fehler auftritt, ist es wahrscheinlich ein Problem mit den drei Add-in-Einstellungen, die Sie für die Azure-Website erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="e5b93-193">If you get an error at this point, it's likely an issue with the three add-in settings you created for the Azure website.</span></span> <span data-ttu-id="e5b93-194">Wechseln Sie wieder, und stellen Sie sicher, dass die Werte aus dem Azure AD-Mandanten & Anwendung die richtigen Werte sind.</span><span class="sxs-lookup"><span data-stu-id="e5b93-194">Go back and make sure the values are the correct values from the Azure AD tenant & application.</span></span> <span data-ttu-id="e5b93-195">Sie sollte eine URL, die aussieht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e5b93-195">You should see a URL that looks</span></span> 

1. <span data-ttu-id="e5b93-196">Nach der erfolgreichen Anmeldung werden Sie wieder auf der Homepage für die Webanwendung der Azure-Website umgeleitet werden, die Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="e5b93-196">After successfully logging in, you will be redirected back to the homepage for the web application of the Azure website you created.</span></span>

<span data-ttu-id="e5b93-197">An dieser Stelle haben Sie Ihre Office 365-API-Webanwendungsprojekt zur Ausführung in Azure-Website erfolgreich bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="e5b93-197">At this point you have successfully deployed your Office 365 API web application project to run in an Azure website.</span></span>

[<span data-ttu-id="e5b93-198">zurück zum Seitenanfang</span><span class="sxs-lookup"><span data-stu-id="e5b93-198">back to top</span></span>](#deploying-development-office-365-sites-to-microsoft-azure)

----------

### <a name="related-links"></a><span data-ttu-id="e5b93-199">Verwandte links</span><span class="sxs-lookup"><span data-stu-id="e5b93-199">Related links</span></span> ###
-  [<span data-ttu-id="e5b93-200">O365-WebApp-SingleTenant</span><span class="sxs-lookup"><span data-stu-id="e5b93-200">O365-WebApp-SingleTenant</span></span>](https://github.com/SharePoint/O365-WebApp-SingleTenant)

### <a name="applies-to"></a><span data-ttu-id="e5b93-201">Gilt für</span><span class="sxs-lookup"><span data-stu-id="e5b93-201">Applies to</span></span> ###
-  <span data-ttu-id="e5b93-202">Office 365 mit mehreren Mandanten (MT)</span><span class="sxs-lookup"><span data-stu-id="e5b93-202">Office 365 Multi Tenant (MT)</span></span>
-  <span data-ttu-id="e5b93-203">Office 365 dedizierte (D)</span><span class="sxs-lookup"><span data-stu-id="e5b93-203">Office 365 Dedicated (D)</span></span>

### <a name="author"></a><span data-ttu-id="e5b93-204">Autor</span><span class="sxs-lookup"><span data-stu-id="e5b93-204">Author</span></span>
<span data-ttu-id="e5b93-205">Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)</span><span class="sxs-lookup"><span data-stu-id="e5b93-205">Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)</span></span>

### <a name="version-history"></a><span data-ttu-id="e5b93-206">Versionsverlauf</span><span class="sxs-lookup"><span data-stu-id="e5b93-206">Version history</span></span> ###
<span data-ttu-id="e5b93-207">Version</span><span class="sxs-lookup"><span data-stu-id="e5b93-207">Version</span></span>  | <span data-ttu-id="e5b93-208">Datum</span><span class="sxs-lookup"><span data-stu-id="e5b93-208">Date</span></span> | <span data-ttu-id="e5b93-209">Kommentare</span><span class="sxs-lookup"><span data-stu-id="e5b93-209">Comments</span></span>
---------| -----| --------
<span data-ttu-id="e5b93-210">0,1</span><span class="sxs-lookup"><span data-stu-id="e5b93-210">0.1</span></span>  | <span data-ttu-id="e5b93-211">2 Januar 2015</span><span class="sxs-lookup"><span data-stu-id="e5b93-211">January 2, 2015</span></span> | <span data-ttu-id="e5b93-212">Erster Entwurf</span><span class="sxs-lookup"><span data-stu-id="e5b93-212">First draft</span></span>


