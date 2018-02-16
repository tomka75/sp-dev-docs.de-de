---
title: Herstellen einer Verbindung zu einer mit Azure Active Directory (Azure AD) gesicherten API
description: Schrittweises Verfahren zum Erstellen und Herstellen einer Verbindung zu einer mit einer mit Azure AD gesicherten API.
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 98718f3eff9c1698e7ac8161c7fa4a40ad1a935a
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="connect-to-api-secured-with-azure-active-directory"></a><span data-ttu-id="657bb-103">Herstellen einer Verbindung zu einer mit Azure Active Directory gesicherten API</span><span class="sxs-lookup"><span data-stu-id="657bb-103">Connect to API secured with Azure Active Directory</span></span>

<span data-ttu-id="657bb-104">Beim Erstellen von SharePoint-Framework-Lösungen müssen Sie möglicherweise eine Verbindung mit Ihrer benutzerdefinierten API herstellen, um Daten abzurufen oder um mit Geschäftsanwendungen zu kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-104">When building SharePoint Framework solutions, you might need to connect to your custom API to retrieve some data or to communicate with line of business applications.</span></span> <span data-ttu-id="657bb-105">Das Sichern von benutzerdefinierten APIs mit Microsoft Azure Active Directory (Azure AD) bietet zahlreiche Vorzüge und kann auf verschiedene Arten erfolgen.</span><span class="sxs-lookup"><span data-stu-id="657bb-105">Securing custom APIs with Microsoft Azure Active Directory (Azure AD) offers you many benefits and can be done in a number of ways.</span></span> <span data-ttu-id="657bb-106">Nachdem Sie die API erstellt haben, gibt es verschiedene Arten, wie Sie darauf zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="657bb-106">After you have built the API, there are several ways in which you can access it.</span></span> <span data-ttu-id="657bb-107">Diese Methoden sind unterschiedlich komplex und bei jeder müssen bestimmte Aspekte beachtet werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-107">These ways vary in complexity and each have their specific considerations.</span></span> 

<span data-ttu-id="657bb-108">Dieser Artikel beschreibt die verschiedenen Ansätze und das schrittweise Verfahren zum Erstellen und Herstellen einer Verbindung zu einer mit Azure AD gesicherten API.</span><span class="sxs-lookup"><span data-stu-id="657bb-108">This article discusses the different approaches and describes the step-by-step process of building and connecting to an API secured with Azure AD.</span></span>

## <a name="secure-an-api-with-azure-ad"></a><span data-ttu-id="657bb-109">Sichern einer API mit Azure AD</span><span class="sxs-lookup"><span data-stu-id="657bb-109">Secure an API with Azure Active Directory</span></span>

<span data-ttu-id="657bb-110">Wenn Sie Office 365 verwenden, ist das Sichern von benutzerdefinierten APIs mit Azure AD eine Architekturoption, die Sie definitiv berücksichtigen sollten.</span><span class="sxs-lookup"><span data-stu-id="657bb-110">If you're using Office 365, securing custom APIs using Azure AD is an architectural option that you should definitely consider.</span></span> <span data-ttu-id="657bb-111">Vor allem können sie Sie zum Sichern des Zugriffs auf die API mit vorhandenen Anmeldeinformationen Ihrer Organisation verwenden, die bereits über Office 365 und Azure AD verwaltet werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-111">First and foremost, it allows you to secure the access to the API using existing organizational credentials that are already managed through Office 365 and Azure AD.</span></span> <span data-ttu-id="657bb-112">Benutzer mit einem aktiven Konto können problemlos mit Anwendungen arbeiten, die mit Azure AD gesicherte APIs nutzen.</span><span class="sxs-lookup"><span data-stu-id="657bb-112">Users with an active account can seamlessly work with applications that leverage APIs secured with Azure AD.</span></span> <span data-ttu-id="657bb-113">Azure AD-Administratoren können Zugriff auf die API zentral verwalten, und zwar auf die gleiche Weise, wie sie den Zugriff auf alle anderen Anwendungen verwalten, die mit Azure AD registriert sind.</span><span class="sxs-lookup"><span data-stu-id="657bb-113">Azure AD administrators can centrally manage access to the API, the same way they manage access to all other applications registered with Azure AD.</span></span>

<span data-ttu-id="657bb-114">Als API-Entwickler müssen Sie durch das Sichern Ihrer APIs mit Azure AD keinen proprietären Satz von Benutzeranmeldeinformationen mehr verwalten und keine benutzerdefinierte Sicherheitsebene für Ihre API implementieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-114">As the API developer, using Azure AD to secure your API frees you from managing a proprietary set of user credentials and implementing a custom security layer for your API. Additionally, Azure Active Directory supports the OAuth protocol which allows you to connect to the API from a range of application types varying from mobile apps to client-side solutions.</span></span> <span data-ttu-id="657bb-115">Darüber hinaus unterstützt Azure AD das OAuth-Protokoll, das es Ihnen ermöglicht, über verschiedene Gerätetypen eine Verbindung zur API herzustellen, darunter mobile Apps bis hin zu clientseitigen Lösungen.</span><span class="sxs-lookup"><span data-stu-id="657bb-115">As the API developer, using Azure AD to secure your API frees you from managing a proprietary set of user credentials and implementing a custom security layer for your API. Additionally, Azure Active Directory supports the OAuth protocol which allows you to connect to the API from a range of application types varying from mobile apps to client-side solutions.</span></span>

<span data-ttu-id="657bb-116">Beim Erstellen von benutzerdefinierten APIs gibt es zwei Hauptmöglichkeiten, um Ihre API mit Azure AD zu sichern.</span><span class="sxs-lookup"><span data-stu-id="657bb-116">When building custom APIs, there are two main ways in which you can secure your API with Azure AD.</span></span> <span data-ttu-id="657bb-117">Wenn Sie die API im Microsoft Azure App Service hosten, können Sie von der Option „App Service-Authentifizierung“ profitieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-117">If you host the API in Microsoft Azure App Service, you can benefit from the App Service Authentication option.</span></span> <span data-ttu-id="657bb-118">Wenn Sie mehr Flexibilität beim Hosting für Ihre API wünschen (zum Beispiel Hosten in der eigenen Infrastruktur oder in Docker-Containern), müssen Sie sie mit Code sichern.</span><span class="sxs-lookup"><span data-stu-id="657bb-118">If you look for more hosting flexibility for your API, such as hosting it on your own infrastructure or in Docker containers, you need to secure it in code.</span></span> <span data-ttu-id="657bb-119">In solchen Fällen richtet sich die Implementierung nach Ihrer Programmiersprache und nach Ihrem Framework.</span><span class="sxs-lookup"><span data-stu-id="657bb-119">In such cases, the implementation depends on your programming language and framework.</span></span> 

<span data-ttu-id="657bb-120">Beim Erörtern dieser Option in diesem Artikel verwenden Sie C# und die [ASP.NET-Web-API](https://www.asp.net/web-api) als Framework.</span><span class="sxs-lookup"><span data-stu-id="657bb-120">In this article, when discussing this option, you will use C# and the [ASP.NET Web API](https://www.asp.net/web-api) as the framework.</span></span>

### <a name="secure-the-api-using-azure-app-service-authentication"></a><span data-ttu-id="657bb-121">Sichern einer API durch Azure App Service-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="657bb-121">Secure the API using Azure App Service Authentication</span></span>

<span data-ttu-id="657bb-122">Bei der Bereitstellung benutzerdefinierter APIs für den Azure App Service können Sie von der Option „App Service-Authentifizierung“ zum Sichern der API mit Azure AD profitieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-122">When deploying custom APIs to Azure App Service, you can benefit from the App Service Authentication option to secure the API with Azure AD.</span></span> <span data-ttu-id="657bb-123">Der größte Vorteil bei der Verwendung von App Service-Authentifizierung ist die Einfachheit: Befolgen Sie einfach die Konfigurationsschritte im Azure-Portal und der Assistent richtet die Authentifizierungskonfiguration für Sie ein.</span><span class="sxs-lookup"><span data-stu-id="657bb-123">The biggest benefit of using App Service Authentication is its simplicity: by following the configuration steps available in the Azure Portal, you can have the wizard set up the authentication configuration for you.</span></span> <span data-ttu-id="657bb-124">Wenn Sie das grundlegende Setup auswählen, erstellt der Assistent eine neue Azure AD-Anwendung in Azure AD, die dem aktuellen Abonnement zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="657bb-124">If you choose the basic setup, the wizard creates a new Azure AD application in Azure AD associated with the current subscription.</span></span> <span data-ttu-id="657bb-125">In der erweiterten Konfiguration können Sie auswählen, welche Azure AD-Anwendung verwendet werden soll, um den Zugriff auf den App Service zu sichern, der die API hostet.</span><span class="sxs-lookup"><span data-stu-id="657bb-125">In the advanced configuration, you can choose which Azure AD application should be used to secure the access to the App Service hosting the API.</span></span>

![Im Azure Portal angezeigt App Service-Authentifizierungseinstellungen](../../../images/api-aad-azure-app-service-authentication.png)

<span data-ttu-id="657bb-127">Nachdem die App Service-Authentifizierung konfiguriert wurde, werden Benutzer, die auf Ihre API zugreifen möchten, dazu aufgefordert, sich mit ihrem Unternehmenskonto anzumelden, das zu demselben Azure AD gehört wie die Azure AD-Anwendung, die zum Sichern der API verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="657bb-127">After App Service Authentication has been configured, users trying to access your API are prompted to sign in with their organizational account that belongs to the same Azure AD as the Azure AD application used to secure the API.</span></span> <span data-ttu-id="657bb-128">Nach der Anmeldung können Sie über die Eigenschaft `HttpContext.Current.User` auf die Informationen zum aktuellen Benutzer zugreifen.</span><span class="sxs-lookup"><span data-stu-id="657bb-128">After signing in, you are able to access the information about the current user through the `HttpContext.Current.User` property.</span></span> <span data-ttu-id="657bb-129">Bei der Verwendung der Azure App Service-Authentifizierung ist keine zusätzliche Konfiguration in Ihrer Anwendung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="657bb-129">When using Azure App Service Authentication, there is no additional configuration required in your application.</span></span>

<span data-ttu-id="657bb-130">Azure App Service-Authentifizierung ist ein Feature, das nur im Azure App Service verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="657bb-130">Azure App Service Authentication is a feature available only in Azure App Service.</span></span> <span data-ttu-id="657bb-131">Diese Funktionalität vereinfacht die Implementierung der Authentifizierung in Ihrer API erheblich, bindet sie jedoch gleichzeitig an die Ausführung im Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="657bb-131">While this capability significantly simplifies implementing authentication in your API, it ties it to running inside Azure App Service.</span></span> <span data-ttu-id="657bb-132">Wenn Sie die API mit einem anderen Cloudanbieter oder in einem Container-Docker hosten möchten, müssen Sie zuerst die Authentifizierungsebene implementieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-132">If you want to host the API with another cloud provider or inside a Docker container, you need to implement the authentication layer first.</span></span>

### <a name="secure-the-api-using-aspnet-authentication"></a><span data-ttu-id="657bb-133">Sichern einer API durch ASP.NET-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="657bb-133">Secure the API using ASP.NET authentication</span></span>

<span data-ttu-id="657bb-134">Wenn Sie größtmögliche Flexibilität im Hinblick auf das Hosting und die Bereitstellung Ihre API wünschen, sollten Sie in Erwägung ziehen, den Support für Azure AD-Authentifizierung in ASP.NET zu implementiert.</span><span class="sxs-lookup"><span data-stu-id="657bb-134">If you want to have the maximum flexibility with regards to where your API is hosted and how it is deployed, you should consider implementing the support for AAD authentication in ASP.NET. Visual Studio simplifies the implementation process significantly and after completing the authentication setup wizard, your API will require users to sign in using their organizational account.</span></span> <span data-ttu-id="657bb-135">Visual Studio vereinfacht den Vorgang der Implementierung erheblich und nach Abschluss des Setup-Assistenten für die Authentifizierung fordert Ihre API Benutzer dazu auf, sich über ihr Unternehmenskonto anzumelden.</span><span class="sxs-lookup"><span data-stu-id="657bb-135">Visual Studio simplifies the implementation process significantly, and after completing the authentication setup wizard, your API requires users to sign in by using their organizational account.</span></span>

![Setup-Assistent für die Visual Studio-Authentifizierung](../../../images/api-aad-visual-studio-authentication-wizard.png)

<span data-ttu-id="657bb-137">Während des Konfigurationsvorgangs fügt Visual Studio alle erforderlichen Verweise und Einstellungen dem ASP.NET-Web-API-Projekt hinzu, einschließlich der Registrierung einer neuen Azure AD-Anwendung zum Sichern Ihrer API.</span><span class="sxs-lookup"><span data-stu-id="657bb-137">During the configuration process, Visual Studio will add all the necessary references and settings to your ASP.NET Web API project, including registering a new AAD application to secure your API.</span></span>

## <a name="access-an-api-secured-with-azure-ad-from-sharepoint-framework-solutions"></a><span data-ttu-id="657bb-138">Zugriff auf eine durch Azure AD gesicherte API über SharePoint-Framework-Lösungen</span><span class="sxs-lookup"><span data-stu-id="657bb-138">Access an API secured with Azure Active Directory from SharePoint Framework solutions</span></span>

<span data-ttu-id="657bb-139">SharePoint-Framework-Lösungen sind vollständig clientseitig und daher nicht in der Lage, vertraulichen Daten sicher zu speichern, die zum Verbinden mit sicheren APIs erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="657bb-139">SharePoint Framework solutions are fully client-side and as such are incapable of securely storing secrets required to connect to secured APIs. To support secure communication with client-side solutions, Azure Active Directory supports a number of mechanisms such as authentication cookies or the OAuth implicit flow.</span></span> <span data-ttu-id="657bb-140">Zur Unterstützung von sicherer Kommunikation mit clientseitigen Lösungen unterstützt Azure AD eine Reihe von Mechanismen wie Authentifizierungscookies oder den impliziten OAuth-Fluss.</span><span class="sxs-lookup"><span data-stu-id="657bb-140">SharePoint Framework solutions are fully client-side and as such are incapable of securely storing secrets required to connect to secured APIs. To support secure communication with client-side solutions, Azure Active Directory supports a number of mechanisms such as authentication cookies or the OAuth implicit flow.</span></span>

### <a name="access-the-api-using-adal-js"></a><span data-ttu-id="657bb-141">Zugreifen auf eine API mit ADAL JS</span><span class="sxs-lookup"><span data-stu-id="657bb-141">Access the API using ADAL JS</span></span>

<span data-ttu-id="657bb-142">Ein häufig verwendeter Ansatz für die Kommunikation mit APIs, die über clientseitige Lösungen mit Azure AD gesichert sind, ist die Verwendung der [ADAL JS](https://github.com/AzureAD/azure-activedirectory-library-for-js)-Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="657bb-142">A commonly used approach for communicating with APIs secured with Azure AD from client-side solutions is using the [ADAL JS](https://github.com/AzureAD/azure-activedirectory-library-for-js) library.</span></span> <span data-ttu-id="657bb-143">ADAL JS vereinfacht die Implementierung der Authentifizierung bei Azure AD in clientseitigen Anwendungen sowie das Abrufen von Zugriffstoken für bestimmte Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="657bb-143">ADAL JS simplifies implementing authentication against Azure AD in client-side applications as well as retrieving access tokens for specific resources.</span></span> <span data-ttu-id="657bb-144">Für Anwendungen, die basierend auf AngularJS erstellt werden, bietet ADAL JS einen Interceptor für HTTP-Anforderungen, der automatisch erforderliche Zugriffstoken zu Kopfzeilen von ausgehenden Webanforderungen hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="657bb-144">For applications built using AngularJS, ADAL JS offers an HTTP request interceptor that automatically adds required access tokens to headers of outgoing web requests.</span></span> <span data-ttu-id="657bb-145">Mithilfe dieses Anforderers müssen Entwickler Webanforderungen an mit Azure AD gesicherte APIs nicht ändern und können sich stattdessen auf das Erstellen der Anwendung konzentrieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-145">By using this requestor, developers don't need to modify web requests to APIs secured with Azure AD and can focus on building the application instead.</span></span>

#### <a name="benefits-of-using-adal-js-to-communicate-with-apis-secured-with-azure-ad"></a><span data-ttu-id="657bb-146">Vorteile der Verwendung von ADAL JS zur Kommunikation mit Azure AD-gesicherten APIs</span><span class="sxs-lookup"><span data-stu-id="657bb-146">Benefits of using ADAL JS to communicate with APIs secured with AAD</span></span>

<span data-ttu-id="657bb-147">Wenn Sie ADAL JS verwenden, haben clientseitige Anwendungen vollständigen Zugriff auf die Identitätsinformationen des derzeit angemeldeten Benutzers.</span><span class="sxs-lookup"><span data-stu-id="657bb-147">When using ADAL JS, client-side applications have full access to the identity information of the currently signed-in user.</span></span> <span data-ttu-id="657bb-148">Dies ist praktisch für Anforderungen wie das Anzeigen des Benutzernamens oder des Profilfotos in der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="657bb-148">This is convenient for requirements such as displaying a user name or profile picture in the application.</span></span> <span data-ttu-id="657bb-149">Beim Erstellen von Lösungen, die in SharePoint gehostet werden, können Entwickler erweiterte Profilinformationen mithilfe der SharePoint-API abrufen, aber für eigenständige Anwendungen ist dies nicht möglich.</span><span class="sxs-lookup"><span data-stu-id="657bb-149">When building solutions hosted in SharePoint, developers can retrieve extended profile information by using the SharePoint API, but for standalone applications this isn't possible.</span></span>

<span data-ttu-id="657bb-150">Neben einer leichteren Authentifizierung bei Azure Active Directory kann ADAL JS auch Zugriffstoken für bestimmte Ressourcen abrufen.</span><span class="sxs-lookup"><span data-stu-id="657bb-150">Besides facilitating authentication against Azure AD, ADAL JS is capable of retrieving access tokens to specific resources.</span></span> <span data-ttu-id="657bb-151">Mit diesen Zugriffstoken können Anwendungen sicher auf Azure AD-gesicherte APIs zugreifen, zum Beispiel [Microsoft Graph](./call-microsoft-graph-from-your-web-part.md) oder andere benutzerdefinierte APIs.</span><span class="sxs-lookup"><span data-stu-id="657bb-151">With these access tokens, applications can securely access APIs secured with Azure AD such as [Microsoft Graph](./call-microsoft-graph-from-your-web-part.md) or other custom APIs.</span></span> <span data-ttu-id="657bb-152">Bevor eine clientseitige Anwendung ADAL JS verwenden kann, muss sie zunächst als Anwendung in Azure AD registriert werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-152">Before a client-side application can use ADAL JS, it has to be registered as an application in Azure AD.</span></span> <span data-ttu-id="657bb-153">Bei der Registrierung geben Entwickler eine Reihe von Parametern an, wie die URL, unter der die Anwendung gehostet wird, und die Ressourcen, auf die die Anwendung zugreifen muss (entweder eigenständig oder im Namen des derzeit angemeldeten Benutzers).</span><span class="sxs-lookup"><span data-stu-id="657bb-153">In the registration process, developers specify a number of parameters such as the URL where the application is hosted and the resources to which the application requires access, either by itself or on behalf of the currently signed-in user.</span></span>

![Registrieren einer neuen Azure AD-Anwendung im Azure-Portal](../../../images/api-aad-create-new-aad-app.png)

<span data-ttu-id="657bb-155">Bei der ersten Ausführung der Anwendung wird der Benutzer dazu aufgefordert, die erforderlichen Berechtigungen zu erteilen.</span><span class="sxs-lookup"><span data-stu-id="657bb-155">The first time the application is used, it prompts the user to grant it the necessary permissions.</span></span> <span data-ttu-id="657bb-156">Dies wird häufig als Zustimmungsfluss bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="657bb-156">This is often referred to as consent flow.</span></span> <span data-ttu-id="657bb-157">Nach der Genehmigung kann die Anwendung Zugriffstoken für bestimmte Ressourcen anfordern und sicher mit ihnen kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-157">After it's approved, the application can then request access tokens for the specific resources and communicate with them securely.</span></span>

#### <a name="considerations-when-using-adal-js-to-communicate-with-apis-secured-with-azure-ad"></a><span data-ttu-id="657bb-158">Überlegungen bei der Verwendung von ADAL JS zur Kommunikation mit Azure AD-gesicherten APIs</span><span class="sxs-lookup"><span data-stu-id="657bb-158">Considerations when using ADAL JS to communicate with APIs secured with AAD</span></span>

<span data-ttu-id="657bb-p114">ADAL JS ist für die Verwendung von Einzelseitenanwendungen ausgelegt. Daher funktioniert es standardmäßig bei der Verwendung mit SharePoint-Framework-Lösungen nicht richtig. Durch das [Anwenden eines Patches](./call-microsoft-graph-from-your-web-part.md) können Sie es jedoch erfolgreich in SharePoint-Framework-Projekten verwenden.</span><span class="sxs-lookup"><span data-stu-id="657bb-p114">ADAL JS has been designed to be used with single-page applications. As such, by default it doesn't work correctly when used with SharePoint Framework solutions. By [applying a patch](./call-microsoft-graph-from-your-web-part.md) however, it can be successfully used in SharePoint Framework projects.</span></span>

<span data-ttu-id="657bb-162">Bei der Verwendung von ADAL JS und OAuth für den Zugriff auf Azure AD-gesicherte APIs wird der Authentifizierungsfluss durch Azure erleichtert.</span><span class="sxs-lookup"><span data-stu-id="657bb-162">When using ADAL JS and OAuth to access APIs secured with Azure AD, the authentication flow is facilitated by Azure.</span></span> <span data-ttu-id="657bb-163">Alle Fehler werden von der Azure-Anmeldeseite verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="657bb-163">Any errors are handled by the Azure sign-in page.</span></span> <span data-ttu-id="657bb-164">Nachdem der Benutzer sich mit seinem Unternehmenskonto angemeldet hat, versucht die Anwendung, ein gültiges Zugriffstoken abzurufen.</span><span class="sxs-lookup"><span data-stu-id="657bb-164">After the user has signed-in with her organizational account, the application tries to retrieve a valid access token.</span></span> <span data-ttu-id="657bb-165">Alle Fehler, die zu diesem Zeitpunkt auftreten, müssen explizit vom Entwickler der Anwendung behoben werden, da das Abrufen von Zugriffstoken ein nicht interaktiver Vorgang ist, bei dem dem Benutzer keine Benutzeroberfläche angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="657bb-165">All errors that occur at this stage have to be explicitly handled by the developer of the application because retrieving access tokens is non-interactive and doesn't present any UI to the user.</span></span>

<span data-ttu-id="657bb-166">Jede clientseitige Anwendung, die ADAL JS verwenden möchte, muss als Azure AD-Anwendung registriert werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-166">Every client-side application that wants to use ADAL JS needs to be registered as an Azure AD application.</span></span> <span data-ttu-id="657bb-167">Ein Teil der Registrierungsinformationen ist die URL, unter der sich die Anwendung befindet.</span><span class="sxs-lookup"><span data-stu-id="657bb-167">A part of the registration information is the URL where the application is located.</span></span> <span data-ttu-id="657bb-168">Da die Anwendung vollständig clientseitig ist und nicht in der Lage ist, vertrauliche Daten sicher zu speichern, ist die URL zur Gewährleistung von Sicherheit Teil des Vertrags zwischen der Anwendung und Azure AD.</span><span class="sxs-lookup"><span data-stu-id="657bb-168">Because the application is fully client-side and is not capable of securely storing a secret, the URL is a part of the contract between the application and Azure AD to establish security.</span></span> <span data-ttu-id="657bb-169">Diese Anforderung ist problematisch für SharePoint-Framework-Lösungen, da Entwickler nicht im Vorhinein alle URLs kennen, in denen ein bestimmtes Webpart verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="657bb-169">This requirement is problematic for SharePoint Framework solutions because developers cannot simply know upfront all URLs where a particular web part will be used.</span></span> <span data-ttu-id="657bb-170">Darüber hinaus unterstützt Azure AD zu diesem Zeitpunkt die Angabe von bis zu 10 Antwort-URLs, was in einigen Szenarien eventuell nicht ausreichend sein könnte.</span><span class="sxs-lookup"><span data-stu-id="657bb-170">Additionally, at this moment, Azure AD supports specifying up to 10 reply URLs, which might not be sufficient in some scenarios.</span></span>

<span data-ttu-id="657bb-171">Bevor eine clientseitige Anwendung ein Zugriffstoken für eine bestimmte Ressource abrufen kann, muss sie den Benutzer authentifizieren, um das ID-Token abzurufen, das dann durch das Zugriffstoken ausgetauscht werden kann.</span><span class="sxs-lookup"><span data-stu-id="657bb-171">Before a client-side application can retrieve an access token to a specific resource, it needs to authenticate the user to obtain the ID token which can then be exchanged for an access token.</span></span> <span data-ttu-id="657bb-172">Obwohl SharePoint-Framework-Lösungen in SharePoint gehostet werden, wo Benutzer bereits mit ihrem Organisationskonto angemeldet sind, stehen die Authentifizierungsinformationen für den aktuellen Benutzer für SharePoint-Framework-Lösungen nicht zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="657bb-172">Even though SharePoint Framework solutions are hosted in SharePoint, where users are already signed in using their organizational accounts, the authentication information for the current user isn't available to SharePoint Framework solutions.</span></span> <span data-ttu-id="657bb-173">Stattdessen muss jede Lösung den Benutzer explizit auffordern, sich anzumelden.</span><span class="sxs-lookup"><span data-stu-id="657bb-173">Instead, each solution must explicitly request the user to sign in.</span></span> <span data-ttu-id="657bb-174">Dies kann entweder durch Umleiten des Benutzers auf die Azure-Anmeldeseite oder durch Anzeigen eines Popupfensters mit der Anmeldeseite erfolgen.</span><span class="sxs-lookup"><span data-stu-id="657bb-174">This can be done either by redirecting the user to the Azure sign-in page or by showing a pop-up window with the sign-in page.</span></span> <span data-ttu-id="657bb-175">Letzteres erfordert weniger Eingriff im Fall eines Webparts (eines der vielen Elemente auf einer Seite).</span><span class="sxs-lookup"><span data-stu-id="657bb-175">The latter is less intrusive in the case of a web part, which is one of the many elements on a page.</span></span> <span data-ttu-id="657bb-176">Wenn auf der Seite mehrere clientseitige SharePoint-Frameworks-Webparts vorhanden sind, verwaltet jedes seinen Status separat und fordert den Benutzer explizit zum Anmelden bei diesem bestimmten Webpart auf.</span><span class="sxs-lookup"><span data-stu-id="657bb-176">If there are multiple SharePoint Framework client-side web parts on the page, each of them manages its state separately and requires the user to explicitly sign in to that particular web part.</span></span>

<span data-ttu-id="657bb-177">Durch ausgeblendete Iframes, die für die Umleitung zu Azure AD-Endpunkten sorgen, wird das Abrufen von Zugriffstoken vereinfacht, die für die Kommunikation mit Azure AD-gesicherten APIs erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="657bb-177">Retrieving access tokens required to communicate with APIs secured with Azure AD is facilitated by hidden iframes that handle redirects to Azure AD endpoints.</span></span> <span data-ttu-id="657bb-178">Es gibt eine bekannte Einschränkung in Microsoft Internet Explorer, bei der das Abrufen von Zugriffstoken im impliziten OAuth-Fluss fehlschlägt, wenn die Azure AD-Anmeldeendpunkte und die SharePoint Online-URL sich nicht in derselben Sicherheitszone befinden.</span><span class="sxs-lookup"><span data-stu-id="657bb-178">There is a known limitation in Microsoft Internet Explorer where obtaining access tokens in OAuth implicit flow fails, if the Azure AD sign-in endpoints and the SharePoint Online URL are not in the same security zone.</span></span> <span data-ttu-id="657bb-179">Wenn Ihre Organisation Internet Explorer verwendet, stellen Sie sicher, dass der Azure AD-Endpunkt und die SharePoint Online-URLs in derselben Sicherheitszone konfiguriert sind.</span><span class="sxs-lookup"><span data-stu-id="657bb-179">If your organization is using Internet Explorer, ensure that the Azure AD endpoint and SharePoint Online URLs are configured in the same security zone.</span></span> <span data-ttu-id="657bb-180">Einige Organisationen entscheiden sich aus Konsistenzgründen dafür, diese Einstellungen an Endbenutzer weiterzugeben, die Gruppenrichtlinien verwenden.</span><span class="sxs-lookup"><span data-stu-id="657bb-180">To maintain consistency, some organizations choose to push these settings to end-users using group policies.</span></span>

<span data-ttu-id="657bb-181">Auf mit Azure AD gesicherte APIs kann nicht anonym zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-181">APIs secured with Azure AD cannot be accessed anonymously.</span></span> <span data-ttu-id="657bb-182">Stattdessen muss die Anwendung, die sie aufruft, gültige Anmeldeinformationen vorweisen können.</span><span class="sxs-lookup"><span data-stu-id="657bb-182">Instead they require a valid credential to be presented by the application calling them.</span></span> <span data-ttu-id="657bb-183">Wenn Sie den impliziten OAuth-Fluss mit clientseitigen Anwendungen verwenden, sind diese Anmeldeinformationen das Trägerzugriffstoken, das mithilfe von ADAL JS abgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="657bb-183">When using the OAuth implicit flow with client-side applications, this credential is the bearer access token obtained using ADAL JS.</span></span> <span data-ttu-id="657bb-184">Haben Sie Ihre SharePoint-Framework-Lösung mithilfe von AngularJS erstellt, stellt JS ADAL automatisch sicher, dass Sie über ein gültiges Zugriffstoken für die bestimmte Ressource verfügen, und fügt dieses allen ausgehenden Anfragen zu, die mithilfe des AngularJS `$http`-Diensts ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-184">If you have built your SharePoint Framework solution using AngularJS, ADAL JS automatically ensures that you have a valid access token for the particular resource, and adds it to all outgoing requests executed by using the AngularJS `$http` service.</span></span> <span data-ttu-id="657bb-185">Wenn Sie andere JavaScript-Bibliotheken verwenden, müssen Sie ein gültiges Zugriffstoken abzurufen und es, falls erforderlich, aktualisieren. Anschließend müssen Sie es eigenständig an die ausgehende Webanfrage anfügen.</span><span class="sxs-lookup"><span data-stu-id="657bb-185">When using other JavaScript libraries, you have to obtain a valid access token, and if necessary refresh it, and attach it to the outgoing web requests yourself.</span></span>

### <a name="access-the-api-by-leveraging-sharepoint-online-authentication-cookie"></a><span data-ttu-id="657bb-186">Zugreifen auf eine API mit einem SharePoint Online-Authentifizierungscookie</span><span class="sxs-lookup"><span data-stu-id="657bb-186">Access the API by leveraging SharePoint Online authentication cookie</span></span>

<span data-ttu-id="657bb-187">Eine alternative Möglichkeit zur Verwendung von ADAL JS zum Herstellen einer Verbindung mit Azure AD-gesicherten APIs ist die Nutzung eines vorhandenen Authentifizierungscookies für die nahtlose Authentifizierung bei der benutzerdefinierten API.</span><span class="sxs-lookup"><span data-stu-id="657bb-187">An alternative approach to using ADAL JS for connecting to APIs secured with AAD is levering the existing authentication cookie for seamless authentication to the custom API.</span></span>

#### <a name="how-it-works"></a><span data-ttu-id="657bb-188">Funktionsweise</span><span class="sxs-lookup"><span data-stu-id="657bb-188">How it works</span></span>

<span data-ttu-id="657bb-189">Wenn Sie sich mit Ihrem Organisationskonto bei SharePoint Online anmelden, wird ein Authentifizierungscookie in Ihrem Browser festgelegt.</span><span class="sxs-lookup"><span data-stu-id="657bb-189">When you sign in with your organizational account to SharePoint Online, an authentication cookie is set in your browser.</span></span> <span data-ttu-id="657bb-190">Dieses Cookie wird bei jeder Anforderung an SharePoint gesendet, sodass Websites und Dokumenten bearbeitet werden können.</span><span class="sxs-lookup"><span data-stu-id="657bb-190">This cookie is sent with every request to SharePoint allowing to work sites and documents.</span></span> <span data-ttu-id="657bb-191">Um mit diesem Cookie eine Verbindung zu einer benutzerdefinierten API herzustellen, die mit Azure AD gesichert ist, platzieren Sie einen ausgeblendeten Iframe auf der Seite, der auf eine URL verweist, unter der die API gehostet wird und die ebenfalls mit Azure AD gesichert ist.</span><span class="sxs-lookup"><span data-stu-id="657bb-191">To use this cookie, to connect to a custom API secured with Azure AD, you place a hidden iframe on the page pointing to a URL where the API is hosted and which is also secured with Azure AD.</span></span> <span data-ttu-id="657bb-192">Nachdem der Browser versucht, diese URL zu laden, wird er zur der Azure AD-Anmeldeseite umgeleitet, da anonymer Zugriff nicht zulässig ist.</span><span class="sxs-lookup"><span data-stu-id="657bb-192">After the browser tries to load this URL, it gets redirected to the Azure AD sign-in page because anonymous access is not allowed.</span></span> <span data-ttu-id="657bb-193">Da Sie sich bereits mit Ihrem Organisationskonto für den Zugriff auf SharePoint angemeldet haben, wird die Authentifizierung automatisch abgeschlossen und Sie werden zurück zur ursprünglichen URL weitergeleitet.</span><span class="sxs-lookup"><span data-stu-id="657bb-193">Because you are already signed in with your organization account to access SharePoint, the authentication completed automatically, redirecting you back to the original URL.</span></span> <span data-ttu-id="657bb-194">An diesem Punkt verfügt Ihr Browser über das Azure AD-Authentifizierungscookie für den Zugriff auf die benutzerdefinierte, mit Azure AD gesicherte API.</span><span class="sxs-lookup"><span data-stu-id="657bb-194">At this point, your browser has the Azure AD authentication cookie for accessing the custom API secured with Azure AD.</span></span>

<span data-ttu-id="657bb-p121">Nachdem Sie den IFrame auf der Seite platziert haben, fügen Sie einen `onload`-Ereignislistener daran an, der ausgelöst wird, wenn der Authentifizierungsfluss abgeschlossen ist. In diesem Ereignislistener legen Sie eine Kennzeichnung fest, die angibt, dass die Authentifizierung abgeschlossen ist. Sie können nun die benutzerdefinierte API sicher aufrufen. Alle Webanforderungen an die benutzerdefinierten APIs sollten verzögert werden, bis diese Kennzeichnung festgelegt ist, da sie sonst fehlschlagen.</span><span class="sxs-lookup"><span data-stu-id="657bb-p121">After placing the iframe on the page, you attach an `onload` event listener to it, which is triggered after the authentication flow completed. In this event listener, you set a flag indicating that authentication completed and you can now securely call the custom API. All web requests to your custom APIs should be delayed until this flag is set or they will fail.</span></span>

```typescript
// ...

export default class LatestOrdersWebPart extends BaseClientSideWebPart<ILatestOrdersWebPartProps> {
  private remotePartyLoaded: boolean = false;
  private orders: IOrder[];

  public render(): void {
    this.domElement.innerHTML = `
    <div class="${styles.latestOrders}">
      <iframe src="https://contoso.azurewebsites.net/"
          style="display:none;"></iframe>
      <div class="ms-font-xxl">Recent orders</div>
      <div class="loading"></div>
      <table class="data" style="display:none;">
        <thead>
          <tr>
            <th>ID</th>
            <th>Date</th>
            <th>Region</th>
            <th>Rep</th>
            <th>Item</th>
            <th>Units</th>
            <th>Unit cost</th>
            <th>Total</th>
          </tr>
        </thead>
        <tbody>
        </tbody>
      </table>
    </div>`;

    this.context.statusRenderer.displayLoadingIndicator(
      this.domElement.querySelector(".loading"), "orders");

    this.domElement.querySelector("iframe").addEventListener("load", (): void => {
      this.remotePartyLoaded = true;
    });

    this.executeOrDelayUntilRemotePartyLoaded((): void => {
      // retrieve and render data
    });
  }

  private executeOrDelayUntilRemotePartyLoaded(func: Function): void {
    if (this.remotePartyLoaded) {
      func();
    } else {
      setTimeout((): void => { this.executeOrDelayUntilRemotePartyLoaded(func); }, 100);
    }
  }

  // ...
}
```

<span data-ttu-id="657bb-198">Beim Ausführen von AJAX-Anforderungen in Ihren Webparts müssen Sie festlegen, dass das Authentifizierungscookie domänenübergreifend gesendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="657bb-198">When executing AJAX requests in your web parts, you have to specify that the authentication cookie should be sent cross-domain.</span></span> <span data-ttu-id="657bb-199">Sie können dies aktivieren, indem Sie die Eigenschaft **credentials** der Webanforderung auf **include** festlegen.</span><span class="sxs-lookup"><span data-stu-id="657bb-199">You can enable this by setting the **credentials** property of the web request to **include**.</span></span> <span data-ttu-id="657bb-200">Wenn Sie dies nicht tun, wird die Anforderung im Browser blockiert, und Sie können die API aufrufen.</span><span class="sxs-lookup"><span data-stu-id="657bb-200">Without this, the request is blocked in the browser and you are not able to call the API.</span></span>

```typescript
// ...

export default class LatestOrdersWebPart extends BaseClientSideWebPart<ILatestOrdersWebPartProps> {
    // ...

    private retrieveAndRenderData(): void {
        this.context.httpClient.get("https://contoso.azurewebsites.net/api/orders",
        HttpClient.configurations.v1, {
          credentials: "include"
        })
        .then((response: HttpClientResponse): Promise<IOrder[]> => {
          // ...
        });
    }

    // ...
}
```

<span data-ttu-id="657bb-201">Zur Unterstützung dieser Methode erfordert die benutzerdefinierte API ebenfalls eine spezifische Konfiguration.</span><span class="sxs-lookup"><span data-stu-id="657bb-201">To support this method, the custom API requires some specific configurations as well.</span></span> <span data-ttu-id="657bb-202">Zunächst benötigt sie Unterstützung für den Empfang von Anmeldeinformationen von domänenübergreifenden Aufrufen.</span><span class="sxs-lookup"><span data-stu-id="657bb-202">First, it requires support for receiving credentials from cross-domain calls.</span></span> <span data-ttu-id="657bb-203">Dies erfolgt durch Festlegen des Antwortheader **Access-Control-Allow-Credentials** auf **true**.</span><span class="sxs-lookup"><span data-stu-id="657bb-203">This is done by setting the **Access-Control-Allow-Credentials** response header to **true**.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="657bb-204">Bei der Verwendung von **Access-Control-Allow-Credentials** dürfen Sie nur einen Ursprung angeben.</span><span class="sxs-lookup"><span data-stu-id="657bb-204">Important: When using the **Access-Control-Allow-Credentials** you are allowed to specify only one origin.</span></span>

<span data-ttu-id="657bb-205">Als Nächstes muss angegeben werden, welcher Ursprung zulässig ist, um die API aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="657bb-205">Next, it needs to specify what origin is allowed to call the API.</span></span> <span data-ttu-id="657bb-206">Dies wird im Antwortheader **Access-Control-Allow-Origin** konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="657bb-206">This is configured in the **Access-Control-Allow-Origin** response header.</span></span>

<span data-ttu-id="657bb-207">Wie diese Header genau konfiguriert werden sollten, hängt von der Implementierung Ihrer API ab.</span><span class="sxs-lookup"><span data-stu-id="657bb-207">How these headers should be configured exactly depends on the implementation of your API.</span></span> <span data-ttu-id="657bb-208">Wenn Sie eine Azure Functions verwenden, um die API beispielsweise mit Node.js zu erstellen, würden Sie diese Header für das Antwortobjekt festlegen:</span><span class="sxs-lookup"><span data-stu-id="657bb-208">How these headers should be configured exactly, depends on the implementation of your API. If you use an Azure Function to build the API using Node.js for example, you would set these headers on the response object:</span></span>

```js
context.res = {
    body: "response",
    headers: {
        "Access-Control-Allow-Credentials" : "true",
        "Access-Control-Allow-Origin" : "https://contoso.sharepoint.com"
    }
};
```

<span data-ttu-id="657bb-209">Bei Verwendung der ASP.NET-Web-API installieren Sie das NuGet-Paket **Microsoft.AspNet.WebApi.Cors**, rufen die Methode `config.EnableCors()` auf und verwenden das Attribut **EnableCors**, um die Headerwerte festzulegen:</span><span class="sxs-lookup"><span data-stu-id="657bb-209">When using ASP.NET Web API, you would install the **Microsoft.AspNet.WebApi.Cors** NuGet package, call the `config.EnableCors()` method and use the **EnableCors** attribute to set the header values:</span></span>

```cs
[EnableCors("origins": "*", "headers": "*", "methods": "*", SupportsCredentials = true)]
public string Get() {
    return "response";
}
```

#### <a name="benefits-of-using-the-sharepoint-online-authentication-cookie-for-seamless-authentication"></a><span data-ttu-id="657bb-210">Vorteile der Verwendung von SharePoint Online-Authentifizierungscookies zur nahtlosen Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="657bb-210">Benefits of using the SharePoint Online authentication cookie for seamless authentication</span></span>

<span data-ttu-id="657bb-211">Der wichtigste Vorteil bei der Verwendung des SharePoint Online-Authentifizierungscookies zum Herstellen einer Verbindung mit benutzerdefinierten APIs, die mit Azure AD gesichert sind, besteht darin, dass Sie bei diesem Ansatz keine Azure AD-Anwendung für jedes Webpart registrieren müssen.</span><span class="sxs-lookup"><span data-stu-id="657bb-211">The most important benefit for using the SharePoint Online authentication cookie to connect to custom APIs secured with AAD is the fact that in this approach you don't need to register an AAD application for every web part. This frees you from having to manage reply URLs of pages where each web part is used and doesn't have the limitation of maximum 10 reply URLs per AAD application.</span></span> <span data-ttu-id="657bb-212">Dies erspart Ihnen das Verwalten von Antwort-URLs von Seiten, auf denen jedes Webpart verwendet wird, und Sie unterliegen nicht der Einschränkung von maximal 10 Antwort-URLs pro Azure AD-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="657bb-212">This frees you from having to manage reply URLs of pages where each web part is used and doesn't have the limitation of maximum 10 reply URLs per Azure AD application.</span></span>

<span data-ttu-id="657bb-213">Der Authentifizierungsfluss wird problemlos verarbeitet, und es ist keine Benutzerinteraktion erforderlich, um den Vorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="657bb-213">The authentication flow is handled seamlessly, and there is no user interaction required to complete.</span></span> <span data-ttu-id="657bb-214">Im Vergleich dazu basiert bei der Verwendung von ADAL JS jedes Webpart auf einer anderen Azure AD-Anwendung und der Benutzer muss sich explizit bei dieser anmelden.</span><span class="sxs-lookup"><span data-stu-id="657bb-214">The authentication flow is handled seamlessly and there is no user interaction required to complete. In comparison, when using ADAL JS, each web part is based on a different AAD application and requires user to explicitly sign in to it.</span></span>

#### <a name="considerations-when-using-the-sharepoint-online-authentication-cookie-for-seamless-authentication"></a><span data-ttu-id="657bb-215">Überlegungen bei der Verwendung von SharePoint Online-Authentifizierungscookies zur nahtlosen Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="657bb-215">Considerations when using the SharePoint Online authentication cookie for seamless authentication</span></span>

<span data-ttu-id="657bb-216">Aus funktionaler Sicht können Sie sowohl mit ADAL JS als auch mit SharePoint Online-Authentifizierungscookies eine Verbindung zu mit Azure AD gesicherten APIs herstellen.</span><span class="sxs-lookup"><span data-stu-id="657bb-216">From the functional point of view, using both ADAL JS and the SharePoint Online authentication cookie allows you to connect to APIs secured with AAD. There are however a few important differences between the two approaches that you should be aware of.</span></span> <span data-ttu-id="657bb-217">Es gibt jedoch einige wichtige Unterschiede zwischen den beiden Ansätzen, die Ihnen bewusst sein sollten.</span><span class="sxs-lookup"><span data-stu-id="657bb-217">There are, however, a few important differences between the two approaches that you should be aware of.</span></span>

<span data-ttu-id="657bb-218">Wenn Sie ADAL JS verwenden, ruft die clientseitige Anwendung das Identitätstoken für den aktuellen Benutzer ab, bevor sie das Zugriffstoken abruft.</span><span class="sxs-lookup"><span data-stu-id="657bb-218">When using ADAL JS, before the client-side application retrieves an access token, it retrieves the identity token for the current user.</span></span> <span data-ttu-id="657bb-219">Dieses Token enthält Informationen zum aktuellen Benutzer, die aus Azure AD abgerufen werden, z. B. Benutzername oder Kennwort.</span><span class="sxs-lookup"><span data-stu-id="657bb-219">This token contains information about the current user retrieved from Azure AD such as the user name or password.</span></span> <span data-ttu-id="657bb-220">Wenn Sie das Authentifizierungscookie verwenden, gibt es kein Identitätstoken.</span><span class="sxs-lookup"><span data-stu-id="657bb-220">When using the authentication cookie, there is no identity token.</span></span> <span data-ttu-id="657bb-221">Da Sie mit SharePoint arbeiten, ist dies nicht wirklich eine Einschränkung, da Sie dieselben Informationen über den aktuellen Benutzer von SharePoint abrufen können.</span><span class="sxs-lookup"><span data-stu-id="657bb-221">Because you're working with SharePoint, this isn't really a limitation, since you can retrieve the same information about the current user from SharePoint.</span></span>

<span data-ttu-id="657bb-222">Mit ADAL JS können Sie eine Verbindung zu jeder beliebigen, mit Azure AD gesicherten API herstellen.</span><span class="sxs-lookup"><span data-stu-id="657bb-222">ADAL JS allows you to connect to any API secured with Azure AD.</span></span> <span data-ttu-id="657bb-223">Wenn Sie das Authentifizierungscookie verwenden, muss die API explizit das Empfangen von Anmeldeinformationen aus domänenübergreifenden Aufrufen unterstützen.</span><span class="sxs-lookup"><span data-stu-id="657bb-223">When using the authentication cookie, the API must explicitly support receiving credentials from cross-domain calls.</span></span> <span data-ttu-id="657bb-224">Beim Entwerfen von APIs sollten Sie diese Anforderung berücksichtigen, um sicherzustellen, dass Sie diese APIs in SharePoint-Framework-Lösungen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="657bb-224">When designing APIs, you should take this requirement into account to ensure that you are able to use these APIs in SharePoint Framework solutions.</span></span>

<span data-ttu-id="657bb-225">Mit ADAL JS und dem SharePoint Online-Authentifizierungscookie können Sie auf mit Azure AD gesicherte APIs zugreifen.</span><span class="sxs-lookup"><span data-stu-id="657bb-225">With both ADAL JS and the SharePoint Online authentication cookie, you can access APIs secured with Azure AD.</span></span> <span data-ttu-id="657bb-226">Aber nicht alle APIs unterstützen die Verwendung beider Methoden.</span><span class="sxs-lookup"><span data-stu-id="657bb-226">But not all APIs support use of both methods.</span></span> <span data-ttu-id="657bb-227">Für den Zugriff auf Microsoft Graph müssen Sie z. B. ein gültiges OAuth-Zugriffstoken mit speziellen Microsoft Graph-Berechtigungen haben.</span><span class="sxs-lookup"><span data-stu-id="657bb-227">For example, to access Microsoft Graph, you need to have a valid OAuth access token with specific Microsoft Graph permissions.</span></span> <span data-ttu-id="657bb-228">Sie können dieses Token mithilfe von ADAL JS, aber nicht mithilfe eines SharePoint Online-Authentifizierungscookies abrufen.</span><span class="sxs-lookup"><span data-stu-id="657bb-228">You can obtain this token by using ADAL JS but not by using a SharePoint Online authentication cookie.</span></span>

<span data-ttu-id="657bb-229">Wenn Sie das SharePoint Online-Authentifizierungscookie verwenden, um auf mit Azure AD gesicherte APIs zuzugreifen, werden keine zusätzlichen Autorisierungsinformationen zusammen mit der Anforderung gesendet.</span><span class="sxs-lookup"><span data-stu-id="657bb-229">When using the SharePoint Online authentication cookie to access APIs secured with Azure AD, no additional authorization information is being sent along with the request.</span></span> <span data-ttu-id="657bb-230">Dies bedeutet, dass standardmäßig jeder Benutzer mit einem gültigen Organisationskonto in Azure AD, das mit der API verknüpft ist, auf die API zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="657bb-230">This means, that by default, every user with a valid organizational account in Azure AD associated with the API can access the API.</span></span> <span data-ttu-id="657bb-231">Wenn Sie die API erstellen, müssen Sie sich um die Autorisierung kümmern, um sicherzustellen, dass alle API-Operationen von Benutzern mit ausreichenden Berechtigungen ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-231">When building the API, you must take care of authorization to ensure that all API operations are performed by users with sufficient privileges.</span></span>

<span data-ttu-id="657bb-232">Benutzerdefinierte APIs werden außerhalb von SharePoint Online gehostet und Sie können mithilfe von domänenübergreifenden Webanforderungen auf sie zugreifen.</span><span class="sxs-lookup"><span data-stu-id="657bb-232">Custom APIs are hosted outside of SharePoint Online and can be accessed by using cross-domain web requests.</span></span> <span data-ttu-id="657bb-233">Standardmäßig enthalten Webbrowser keine Anmeldeinformationen, wenn domänenübergreifende AJAX-Anforderungen ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-233">By default, web browsers don't include credentials when performing cross-domain AJAX requests.</span></span> <span data-ttu-id="657bb-234">Zum Verbinden mit diesen gesicherten APIs müssen Sie das domänenübergreifende Senden von Anmeldeinformationen explizit für jede ausgehende Webanforderung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-234">To connect to these secured APIs, you have to enable sending credentials with cross-domains explicitly for each outgoing web request.</span></span>

### <a name="general-considerations"></a><span data-ttu-id="657bb-235">Allgemeine Überlegungen</span><span class="sxs-lookup"><span data-stu-id="657bb-235">General considerations</span></span>

<span data-ttu-id="657bb-236">Sowohl bei ADAL JS als auch bei der Methode, bei der das SharePoint Online-Authentifizierungscookie zum Einsatz kommt, werden Iframes für die Kommunikation mit Azure AD verwendet.</span><span class="sxs-lookup"><span data-stu-id="657bb-236">Both ADAL JS and the method that uses the SharePoint Online authentication cookie use iframes for communicating with Azure AD.</span></span> <span data-ttu-id="657bb-237">Der Grund dafür sind die Umleitungen, die Bestandteil des OAuth-Flusses sind und die nicht automatisch von AJAX-Anforderungen gefolgt werden können.</span><span class="sxs-lookup"><span data-stu-id="657bb-237">The reason for that are the redirects that are a part of the OAuth flow, and which cannot be automatically followed by AJAX requests.</span></span> <span data-ttu-id="657bb-238">Microsoft Internet Explorer verwendet Sicherheitszonen, um je nach zugeordneter Zone Sicherheitsrichtlinien auf Websites anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="657bb-238">Microsoft Internet Explorer uses security zones to apply security policies to websites depending on the associated zone.</span></span> <span data-ttu-id="657bb-239">Damit die Skripte auf Informationen aus einem Iframe zugreifen können, müssen die Ressource im Iframe und die Seite, auf der das Iframe gehostet wird, sich in der gleichen Sicherheitszone befinden.</span><span class="sxs-lookup"><span data-stu-id="657bb-239">For the scripts to be able to access information from an iframe, the resource in the iframe and the page hosting the iframe must be located in the same security zone.</span></span> <span data-ttu-id="657bb-240">Um eine richtige Konfiguration sicherzustellen, können Organisationen Gruppenrichtlinien verwenden, um die Einstellungen konsistent für ihre Benutzer zu verteilen.</span><span class="sxs-lookup"><span data-stu-id="657bb-240">To ensure correct configuration, organizations can use group policies to distribute the settings consistently to their users.</span></span>

## <a name="build-an-api-secured-with-azure-ad"></a><span data-ttu-id="657bb-241">Erstellen einer durch Azure AD gesicherten API</span><span class="sxs-lookup"><span data-stu-id="657bb-241">Build an API secured with Azure Active Directory</span></span>

<span data-ttu-id="657bb-242">Das Sichern des Zugriffs auf eine mit Azure AD gesicherte API ist nicht komplex und erfordert nur einige wenige Schritte.</span><span class="sxs-lookup"><span data-stu-id="657bb-242">Securing the access to an API with Azure AD isn't complex and requires just a few steps.</span></span> <span data-ttu-id="657bb-243">Der genaue Vorgang variiert in Abhängigkeit von der Implementierung Ihrer API.</span><span class="sxs-lookup"><span data-stu-id="657bb-243">The exact process varies depending on the implementation of your API.</span></span> <span data-ttu-id="657bb-244">Wenn Sie Azure Functions verwenden, können Sie die Sicherheit über das Azure-Portal konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-244">If you choose to use Azure Functions, you are able to configure the security through the Azure Portal.</span></span> <span data-ttu-id="657bb-245">Wenn Sie Ihre API mithilfe der ASP.NET-Web-API erstellen und Sie sie an einem anderen Ort als dem Azure App Service hosten möchten, müssen Sie den Code der Web-API erweitern, um Authentifizierung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="657bb-245">If you built your API by using the ASP.NET Web API and want to host it somewhere else than in Azure App Service, you need to extend the Web API's code to add authentication to it.</span></span> <span data-ttu-id="657bb-246">Es folgt eine schrittweise Beschreibung der Erstellung und Konfiguration einer mit Azure AD gesicherten API mithilfe von Azure Functions und der ASP.NET-Web-API.</span><span class="sxs-lookup"><span data-stu-id="657bb-246">Following is a step-by-step description of how you would build and configure an API secured with Azure AD by using both Azure Functions and ASP.NET Web API.</span></span>

### <a name="build-the-api-using-an-azure-function"></a><span data-ttu-id="657bb-247">Erstellen einer API mit einer Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="657bb-247">Build the API using an Azure Function</span></span>

<span data-ttu-id="657bb-248">Das Erstellen von APIs mithilfe von Azure Functions-Angeboten bietet Ihnen eine Reihe von Vorteilen.</span><span class="sxs-lookup"><span data-stu-id="657bb-248">Building APIs using Azure Functions offers you a number of benefits.</span></span> <span data-ttu-id="657bb-249">Vor allem vereinfacht es erheblich den Vorgang der Entwicklung und Bereitstellung der API.</span><span class="sxs-lookup"><span data-stu-id="657bb-249">First and foremost, it significantly simplifies the development and deployment process of the API.</span></span> <span data-ttu-id="657bb-250">Azure Functions bietet umfassende Konfigurationsoptionen.</span><span class="sxs-lookup"><span data-stu-id="657bb-250">Azure Functions offer a rich set of configuration options.</span></span> <span data-ttu-id="657bb-251">Das einzige, worum Sie sich kümmern müssen, ist der tatsächliche API-Code.</span><span class="sxs-lookup"><span data-stu-id="657bb-251">The only thing that you need to take care of is the actual API code.</span></span> <span data-ttu-id="657bb-252">Für alles andere, von der Authentifizierung bis hin zur Unterstützung von Cross-Origin Resource Sharing (CORS) und zur Dokumentierung der AP, können Sie das Azure-Portal verwenden.</span><span class="sxs-lookup"><span data-stu-id="657bb-252">For everything else, from authentication to supporting Cross-Origin Resource Sharing (CORS) and documenting the API, you can use the Azure Portal.</span></span>

<span data-ttu-id="657bb-253">Azure Functions wird im Azure App Service gehostet und nutzt viele Funktionen des zugrunde liegenden Diensts.</span><span class="sxs-lookup"><span data-stu-id="657bb-253">Azure Functions are hosted in Azure App Service and benefit from many capabilities available in the underlying service.</span></span> <span data-ttu-id="657bb-254">Neben der Sicherung der API mit einem Funktions- oder Administratorschlüssel können Sie wahlweise Azure App Service-Sicherheit aktivieren und Ihre API mit Azure AD oder mit einem der anderen verfügbaren Authentifizierungsanbieter sichern.</span><span class="sxs-lookup"><span data-stu-id="657bb-254">Azure Functions are hosted in Azure App Service and benefit of many capabilities available in the underlying service. On top of securing the API using a function or admin key, you can choose to enable Azure App Service security and protect your API using Azure Active Directory or one of the other available authentication providers. App Service authentication can be configured via the Azure Portal and doesn't require any changes in the API code.</span></span> <span data-ttu-id="657bb-255">App Service-Authentifizierung kann über das Azure-Portal konfiguriert werden und es müssen dafür keine Änderungen am API-Code vorgenommen werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-255">App Service Authentication can be configured via the Azure Portal and doesn't require any changes in the API code.</span></span>

<span data-ttu-id="657bb-256">Nachfolgend wird erläutert, wie Sie Azure Functions zum Erstellen einer API verwenden, die durch Azure AD gesichert ist und die von einem domänenübergreifenden Ursprung auf sichere Weise aufgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="657bb-256">Following is how you would use Azure Functions to create an API secured with Azure Active Directory and capable of being called from a cross-domain origin in a secured way.</span></span>

#### <a name="create-a-new-azure-function"></a><span data-ttu-id="657bb-257">Erstellen einer neuen Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="657bb-257">Create new Azure Function</span></span>

1. <span data-ttu-id="657bb-258">Wechseln Sie im Azure-Portal zu Ihrer Ressourcengruppe, und fügen Sie eine Funktionen-App hinzu.</span><span class="sxs-lookup"><span data-stu-id="657bb-258">In the Azure Portal go to your Resource Group and add a Function App.</span></span>

    ![In der Liste der verfügbaren Dienste hervorgehobene Funktionen-App, die einer Ressourcengruppe hinzugefügt werden kann](../../../images/api-aad-create-new-function-app.png)

2. <span data-ttu-id="657bb-260">Öffnen Sie, nachdem die Funktionen-App bereitgestellt wurde, die neu erstellte Funktionen-App, und fügen Sie eine neue Funktion hinzu, indem Sie das Pluszeichen neben der Beschriftung „Funktionen“ auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-260">Once the Function App has been provisioned, open the newly created Function App and add a new function by clicking the plus icon next to the Functions label.</span></span>

    ![Das Pluszeichen neben der hervorgehobenen Beschriftung „Funktionen“ auf dem Funktionen-App-Blatt](../../../images/api-aad-add-function.png)

3. <span data-ttu-id="657bb-262">Scrollen Sie im Schnellstartbildschirm zum Abschnitt **Selbständig einsteigen**, und wählen Sie die Option **Benutzerdefinierte Funktion**.</span><span class="sxs-lookup"><span data-stu-id="657bb-262">On the quick start screen, scroll down to the **Get started on your own** section and choose the **Custom function** option.</span></span>

    ![Die Verknüpfung „Benutzerdefinierte Funktion“, hervorgehoben im Bildschirm zum Hinzufügen einer neuen Funktion](../../../images/api-aad-custom-function.png)

4. <span data-ttu-id="657bb-264">Wählen Sie aus der Liste der Vorlagen **HttpTrigger-JavaScript** aus.</span><span class="sxs-lookup"><span data-stu-id="657bb-264">From the list of templates, select **HttpTrigger-JavaScript**.</span></span> 

5. <span data-ttu-id="657bb-265">Geben Sie für den Funktionsnamen **Aufträge** ein, und legen Sie die Funktionsautorisierungsebene auf **Anonym** fest, da Sie Azure AD zum Sichern des Zugriffs auf die Azure-Funktion verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="657bb-265">From the list of templates choose HttpTrigger-JavaScript. As the function name, use **Orders** and set the function Authorization level to **Anonymous** as you will use Azure AD to secure the access to the Azure Function. Confirm your selection by clicking the Create button.</span></span> <span data-ttu-id="657bb-266">Bestätigen Sie Ihre Auswahl, indem Sie **Erstellen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-266">Confirm your selection by selecting **Create**.</span></span>

    ![Konfiguration einer neuen Azure-Funktion](../../../images/api-aad-add-function-parameters.png)

#### <a name="implement-api-code"></a><span data-ttu-id="657bb-268">Implementieren des API-Codes</span><span class="sxs-lookup"><span data-stu-id="657bb-268">Implement API code</span></span>

1. <span data-ttu-id="657bb-269">Ersetzen den Code der Funktion durch den folgenden Codeausschnitt:</span><span class="sxs-lookup"><span data-stu-id="657bb-269">Replace the function's code with the following snippet:</span></span>

    ```js
    module.exports = function (context, req) {
        context.res = {
            body: [
                {
                id: 1,
                orderDate: new Date(2016, 0, 6),
                region: "east",
                rep: "Jones",
                item: "Pencil",
                units: 95,
                unitCost: 1.99,
                total: 189.05
                },
                {
                id: 2,
                orderDate: new Date(2016, 0, 23),
                region: "central",
                rep: "Kivell",
                item: "Binder",
                units: 50,
                unitCost: 19.99,
                total: 999.50
                },
                {
                id: 3,
                orderDate: new Date(2016, 1, 9),
                region: "central",
                rep: "Jardine",
                item: "Pencil",
                units: 36,
                unitCost: 4.99,
                total: 179.64
                },
                {
                id: 4,
                orderDate: new Date(2016, 1, 26),
                region: "central",
                rep: "Gill",
                item: "Pen",
                units: 27,
                unitCost: 19.99,
                total: 539.73
                },
                {
                id: 5,
                orderDate: new Date(2016, 2, 15),
                region: "west",
                rep: "Sorvino",
                item: "Pencil",
                units: 56,
                unitCost: 2.99,
                total: 167.44
                }],
            headers: {
                "Access-Control-Allow-Credentials" : "true",
                "Access-Control-Allow-Origin" : "https://contoso.sharepoint.com"
            }
        };
        context.done();
    };
    ```

2. <span data-ttu-id="657bb-270">Ändern Sie die im Header **Access-Control-Allow-Origin** angegebene URL so, dass sie mit der URL des SharePoint Online-Mandanten übereinstimmt, von dem aus Sie diese API aufrufen.</span><span class="sxs-lookup"><span data-stu-id="657bb-270">Change the URL specified in the **Access-Control-Allow-Origin** header to match the URL of your SharePoint Online tenant from which you will be calling this API.</span></span>

3. <span data-ttu-id="657bb-271">Speichern Sie die Änderungen im Code der Funktion, indem Sie **Speichern** auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-271">Save the changes to the function's code by clicking the **Save** button.</span></span>

    ![Schaltfläche „Speichern“, hervorgehoben im Bildschirm des Azure-Funktionscodes](../../../images/api-aad-function-code.png)

#### <a name="change-cors-settings"></a><span data-ttu-id="657bb-273">Ändern der CORS-Einstellungen</span><span class="sxs-lookup"><span data-stu-id="657bb-273">Change CORS settings</span></span>

<span data-ttu-id="657bb-274">Azure Functions wird im Azure App Service gehostet, sodass Sie die Cross-Origin Resource Sharing (CORS)-Einstellungen über das Azure-Portal konfigurieren können.</span><span class="sxs-lookup"><span data-stu-id="657bb-274">Azure Functions are hosted in Azure App Service, which allows you to configure its Cross-Origin Resource Sharing (CORS) settings through the Azure Portal.</span></span> <span data-ttu-id="657bb-275">Dies ist zwar bequem, aber wenn die Einstellungen über das Portal konfiguriert werden, können sie nicht in Kombination mit dem Header **Access-Control-Allow-Credentials** verwendet werden, der für die API zum Akzeptieren von Authentifizierungscookies aus einem anderen Ursprung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="657bb-275">Azure Functions are hosted in Azure App Service which allows you to configure its Cross-Origin Resource Sharing (CORS) settings through the Azure Portal. While this is convenient, if configured through the portal, it cannot be used in combination with the **Access-Control-Allow-Credentials** header, which is required by the API to accept authentication cookie coming from another origin. For the client-sie authentication to work correctly, CORS settings of the Azure App Service must be cleared.</span></span> <span data-ttu-id="657bb-276">Damit die clientseitige Authentifizierung ordnungsgemäß funktioniert, müssen die CORS-Einstellungen des Azure App Service gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-276">For the client-side authentication to work correctly, CORS settings of the Azure App Service must be cleared.</span></span>

1. <span data-ttu-id="657bb-277">Wählen Sie in der Funktionen-App Ihre Azure-Funktion aus, und wechseln Sie zum Blatt **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="657bb-277">In the Function App, select your Azure Function and navigate to the **Platform features** blade.</span></span>

    ![Die Plattformfeatures-Verknüpfung, hervorgehoben in den Azure-Funktionseinstellungen](../../../images/api-aad-platform-features.png)

2. <span data-ttu-id="657bb-279">Wählen Sie im Abschnitt **API** die Option **CORS**.</span><span class="sxs-lookup"><span data-stu-id="657bb-279">From the **API** section, choose the **CORS** option.</span></span>

    ![Die CORS-Option, hervorgehoben auf dem Plattformfeatures-Blatt der Azure-Funktion](../../../images/api-aad-function-cors.png)

3. <span data-ttu-id="657bb-281">Löschen Sie auf dem Blatt mit den **CORS-Einstellungen** alle Einträge, sodass die CORS-Konfiguration leer ist.</span><span class="sxs-lookup"><span data-stu-id="657bb-281">On the CORS settings blade, delete all entries so that the CORS configuration is empty.</span></span>

    ![Die Option „Löschen“, hervorgehoben im ersten CORS-Eintrag](../../../images/api-aad-function-cors-delete.png)

4. <span data-ttu-id="657bb-283">Bestätigen Sie den Löschvorgang, indem Sie **Speichern** auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-283">Confirm the deletion by clicking the **Save** button.</span></span>

    ![Die Schaltfläche „Speichern“, hervorgehoben auf dem Blatt mit CORS-Einstellungen](../../../images/api-aad-function-cors-save.png)

#### <a name="enable-app-service-authentication"></a><span data-ttu-id="657bb-285">Aktivieren der App Service-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="657bb-285">Enable App Service Authentication</span></span>

1. <span data-ttu-id="657bb-286">Kehren Sie in den Einstellungen der Funktionen-App zurück zum Blatt **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="657bb-286">In the Function App settings, go back to the Platform settings blade. From the **Networking** section, select the Authentication / Authorization option.</span></span> 

2. <span data-ttu-id="657bb-287">Wählen Sie im Bereich **Netzwerk** die Option **Authentifizierung/Autorisierung** aus.</span><span class="sxs-lookup"><span data-stu-id="657bb-287">In the Function App settings, go back to the Platform settings blade. From the **Networking** section, select the **Authentication / Authorization** option.</span></span>

    ![Die Option „Authentifizierung/Autorisierung“, hervorgehoben auf dem Blatt mit den Plattformeinstellungen in der Funktionen-App](../../../images/api-aad-function-authentication.png)

3. <span data-ttu-id="657bb-289">Aktivieren Sie die App Service-Authentifizierung, indem Sie die Option **App Service-Authentifizierung** auf **Ein** stellen.</span><span class="sxs-lookup"><span data-stu-id="657bb-289">Enable the App Service Authentication by setting the **App Service Authentication** toggle to **On**.</span></span>

    ![Die aktivierte Option „App Service-Authentifizierung“](../../../images/api-aad-function-authentication-on.png)

4. <span data-ttu-id="657bb-291">Um den anonymen Zugriff auf die API zu verhindern und die Authentifizierung mithilfe von Azure AD zu erzwingen, legen Sie in der Liste **Die auszuführende Aktion, wenn die Anforderung nicht authentifiziert ist** den Wert auf **Mit Azure Active Directory anmelden** fest.</span><span class="sxs-lookup"><span data-stu-id="657bb-291">To disallow anonymous access to the API and force authentication using Azure AD, set the value of the **Action to take when request is not authenticated** drop-down to **Login with Azure Active Directory**.</span></span>

    ![Die Option „Mit Azure Active Directory anmelden“, ausgewählt im Dropdownmenü „Die auszuführende Aktion, wenn die Anforderung nicht authentifiziert ist“](../../../images/api-aad-function-authentication-login-aad.png)

5. <span data-ttu-id="657bb-293">Wählen Sie in der Liste der Authentifizierungsanbieter **Azure Active Directory** aus, um es zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-293">Next, in the list of authentication providers, select Azure Active Directory to configure it.</span></span>

    ![Azure Active Directory, hervorgehoben in der Liste der Authentifizierungsanbieter](../../../images/api-aad-function-authentication-aad.png)

6. <span data-ttu-id="657bb-295">Stellen Sie auf dem Blatt **Active Directory-Authentifizierung** den **Verwaltungsmodus** auf **Express** ein, und erstellen Sie eine neue Azure AD-App.</span><span class="sxs-lookup"><span data-stu-id="657bb-295">On the Active Directory Authentication blade, set the **Management mode** to **Express** and create a new AAD app.</span></span>

    > [!IMPORTANT] 
    > <span data-ttu-id="657bb-296">Wenn Sie den Konfigurationsmodus Express verwenden, erstellt das Azure-Portal eine neue Azure AD-Anwendung im gleichen Verzeichnis, in dem sich auch die Funktionen-App befindet.</span><span class="sxs-lookup"><span data-stu-id="657bb-296">When using the Express configuration mode, the Azure Portal creates a new Azure AD application from the same directory where the Function App is located.</span></span> <span data-ttu-id="657bb-297">Wenn die Funktionen-App in einem anderen Azure-Abonnement mit einem anderen Verzeichnis gehostet wird, sollten Sie stattdessen den erweiterten Modus verwenden und die ID des Verzeichnisses und der Anwendung angeben, die zum Sichern des Zugriffs auf die API verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="657bb-297">Important: when using the express configuration mode, the Azure Portal will create a new AAD application from the same directory as where the Function App is located. If the Function App is hosted in a different Azure subscription with a different directory, you should use the advanced mode instead, and specify the ID of the directory and application that should be used to secure the access to the API.</span></span>
    >
    > <span data-ttu-id="657bb-298">Wenn Sie vorhandene Azure AD-Anwendungen verwenden, konfigurieren Sie die Anwendung so, dass nur Anmeldeinformationen von einem einzigen Mandanten akzeptiert werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-298">When using existing Azure AD applications, configure the application to accept credentials from a single tenant only.</span></span> <span data-ttu-id="657bb-299">Durch das Konfigurieren der Anwendung für mehrere Mandanten können Benutzer mit einem gültigen Organisations- oder persönlichen Konto eine Verbindung mit Ihrer API herstellen.</span><span class="sxs-lookup"><span data-stu-id="657bb-299">When using existing AAD applications you should configure the application to accept credentials from a single tenant only. Configuring the application as multi-tenant would allow any user with a valid organization or personal account to connect to your API.</span></span>
    >
    > <span data-ttu-id="657bb-300">Die Verwendung einer Azure AD-Anwendung für das Sichern des Zugriffs auf Ihre API bezieht sich nur auf die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="657bb-300">Using an Azure AD application to secure the access to your API only accounts for authentication.</span></span> <span data-ttu-id="657bb-301">Beim Erstellen Ihrer API müssen Sie auch Anforderungen im Code der API autorisieren, um sicherzustellen, dass nur Benutzer mit entsprechenden Berechtigungen die API verwenden.</span><span class="sxs-lookup"><span data-stu-id="657bb-301">Using an AAD application to secure the access to your API only accounts for authentication. When building your API, you should also authorize requests in your API's code, to ensure that only users with sufficient privileges are using the API.</span></span>

7. <span data-ttu-id="657bb-302">Da die App nur zum Sichern des Zugriffs auf die Azure-Funktion vorgesehen ist, sind keine zusätzlichen Berechtigungen erforderlich. </span><span class="sxs-lookup"><span data-stu-id="657bb-302">Because the app is only meant to secure the access to the Azure Function, it doesn't require any additional permissions. Confirm the selection by clicking the OK button.</span></span> <span data-ttu-id="657bb-303">Bestätigen Sie die Auswahl, indem Sie **OK** auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-303">Confirm the selection by selecting **OK**.</span></span>

    ![Azure Active Directory-Authentifizierungseinstellungen](../../../images/api-aad-function-authentication-aad-app.png)

8. <span data-ttu-id="657bb-305">Wenn das Blatt **Azure Active Directory** geschlossen wird, wählen Sie auf dem Blatt **Authentifizierung/Autorisierung** **Speichern** aus, um alle Änderungen an den Authentifizierungseinstellungen zu bestätigen.</span><span class="sxs-lookup"><span data-stu-id="657bb-305">When the Azure Active Directory blade closes, back on the Authentication / Authorization blade, click the Save button to confirm all changes to authentication settings.</span></span>

    ![Die Schaltfläche „Speichern“, hervorgehoben auf dem Blatt „Authentifizierung/Autorisierung“](../../../images/api-aad-function-authentication-save.png)

9. <span data-ttu-id="657bb-307">Wenn Sie versuchen, in einem neuen privaten Fenster zur API-URL zu navigieren, sollten Sie aufgefordert werden, sich mit Ihrem Azure AD-Konto anzumelden.</span><span class="sxs-lookup"><span data-stu-id="657bb-307">If you try to navigate to your API URL in a new private window, you should be prompted to sign in using your Azure AD account.</span></span>

    ![Azure AD-Anmeldeseite](../../../images/api-aad-sign-in.png)

<span data-ttu-id="657bb-309">Zu diesem Zeitpunkt ist die API bereit, mit dem Authentifizierungscookie sicher von einem clientseitigen SharePoint-Framework-Webpart aufgerufen zu werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-309">At this point, the API is ready to be called securely from a SharePoint Framework client-side web part using the authentication cookie.</span></span>

### <a name="build-the-api-by-using-aspnet-web-api"></a><span data-ttu-id="657bb-310">Erstellen der API mit der ASP.NET-Web-API</span><span class="sxs-lookup"><span data-stu-id="657bb-310">Build the API using ASP.NET Web API</span></span>

<span data-ttu-id="657bb-311">Eine weitere Möglichkeit zum Implementieren der API ist die ASP.NET-Web-API.</span><span class="sxs-lookup"><span data-stu-id="657bb-311">Another way to implement the API is by using the ASP.NET Web API.</span></span> <span data-ttu-id="657bb-312">Im Vergleich zur Nutzung von Azure Functions zum Erstellen der API erfordert die ASP.NET-Web-API wesentlich mehr Arbeit.</span><span class="sxs-lookup"><span data-stu-id="657bb-312">Compared to using Azure Functions to build the API, the ASP.NET Web API requires significantly more work.</span></span> <span data-ttu-id="657bb-313">Sie müssen nicht nur ein vollständiges Projekt dafür einrichten, sondern Sie müssen sich auch überlegen, wo die API bereitgestellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="657bb-313">Not only do you have to set up a complete project for it, but you also have to think about where the API will be deployed.</span></span> <span data-ttu-id="657bb-314">Andererseits bietet die ASP.NET-Web-API mehr Flexibilität und ermöglicht es Ihnen, die API auf verschiedenen Plattformen wie z. B. dem Azure App Service, Docker-Containern, anderen Cloudanbieter oder sogar in Ihrer Infrastruktur bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="657bb-314">On the other hand, using the ASP.NET Web API offers you more flexibility and allows you to deploy the API to different platforms such as Azure App Service, Docker containers, other cloud providers, or even on your infrastructure.</span></span>

<span data-ttu-id="657bb-315">Im Folgenden finden Sie die Schritte zum Erstellen einer API mit der ASP.NET-Web-API, zum Bereitstellen der API im Azure App Service und zum Sichern der API mithilfe von Azure App Service-Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="657bb-315">Following are steps to build an API using the ASP.NET Web API, deploy it to Azure App Service, and secure it by using Azure App Service Authentication.</span></span> <span data-ttu-id="657bb-316">Später erweitern Sie die API so, dass sie die Authentifizierung eigenständig durchführen kann, damit sie auf anderen Plattformen bereitgestellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="657bb-316">Following is how you would build an API using ASP.NET WebAPI, deploy it to Azure App Service and secure it using Azure App Service Authentication. Later, you will extend the API to perform the authentication by itself, so that it can be deployed to other platforms as well.</span></span>

#### <a name="create-a-new-aspnet-web-api-project"></a><span data-ttu-id="657bb-317">Erstellen eines neuen ASP.NET-Web-API-Projekts</span><span class="sxs-lookup"><span data-stu-id="657bb-317">Create a new ASP.NET Web API project</span></span>

1. <span data-ttu-id="657bb-318">Wählen Sie in Visual Studio im Menü **Datei** die Option **Neues Projekt** aus.</span><span class="sxs-lookup"><span data-stu-id="657bb-318">In Visual Studio, on the **File** menu, select the **New / Project** option.</span></span> 

2.  <span data-ttu-id="657bb-319">Wählen Sie im Dialogfeld **Neues Projekt** Visual C#-Webvorlagen, und wählen Sie aus der Liste der verfügbaren Vorlagen die Vorlage **ASP.NET-Webanwendung**.</span><span class="sxs-lookup"><span data-stu-id="657bb-319">In Visual Studio, from the **File menu, choose the New / Project option. In the New Project** dialog, select C# Web templates and from the list of available templates, select the **ASP.NET Web Application** template.</span></span>

    ![Die Projektvorlage „ASP.NET-Webanwendung“, ausgewählt im Dialogfeld „Neues Projekt“](../../../images/api-aad-webapi-vs-web-application.png)

3. <span data-ttu-id="657bb-321">Wählen Sie als Typ des ASP.NET-Webanwendungsprojekts die Option **Web-API**.</span><span class="sxs-lookup"><span data-stu-id="657bb-321">As the type of ASP.NET Web Application project, select **Web API**.</span></span>

    ![„Web-API“, ausgewählt als Typ des zu erstellenden ASP.NET-Webanwendungsprojekts](../../../images/api-aad-webapi-vs-webapi.png)

4. <span data-ttu-id="657bb-323">Da Sie die Azure App Service-Authentifizierung zum Sichern des Zugriffs auf die API verwenden möchten, wählen Sie die Schaltfläche **Authentifizierung ändern** und anschließend die Option **Keine Authentifizierung** aus.</span><span class="sxs-lookup"><span data-stu-id="657bb-323">Because you will use Azure App Service Authentication to secure the access to the API, click the **Change Authentication** button and select the **No Authentication** option.</span></span>

    ![Die Option „Keine Authentifizierung“, ausgewählt als Authentifizierungsoption für die neu erstellte ASP.NET-Webanwendung](../../../images/api-aad-webapi-vs-no-authentication.png)

5. <span data-ttu-id="657bb-325">Bestätigen Sie Ihre Auswahl, indem Sie **OK** auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-325">Confirm your choice by clicking the **OK** button.</span></span>

6. <span data-ttu-id="657bb-326">Mit Visual Studio können Sie Ihre Web-API ganz einfach für den Azure App Service bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="657bb-326">Visual Studio allows you to easily deploy your Web API to Azure App Service.</span></span> <span data-ttu-id="657bb-327">Um diese Funktion zu nutzen, wählen Sie im Abschnitt **Microsoft Azure** das Dialogfeld **ASP.NET-Webanwendung** aus, aktivieren Sie das Kontrollkästchen **In der Cloud hosten**, und wählen Sie in der Liste die Option **App Service** aus.</span><span class="sxs-lookup"><span data-stu-id="657bb-327">Visual Studio allows you to easily deploy your WebAPI to Azure App Service. To benefit of this capability, in the **New ASP.NET Web Application** dialog, in the **Microsoft Azure** section, select the **Host in the cloud** section and in the drop-down select the **App Service** option.</span></span>

    ![„App Service“, ausgewählt als Hostingplattform für die Webanwendung](../../../images/api-aad-webapi-vs-host-app-service.png)

7. <span data-ttu-id="657bb-329">Geben Sie im Dialogfeld **App Service erstellen** den Namen für die Web-App an, die erstellt werden soll, und wählen Sie das **Azure-Abonnement**, die **Ressourcengruppe** und den **App Service-Plan**, den Sie für diese Anwendung verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="657bb-329">In the Create App Service dialog, specify the name for the web app to be created and select your Azure subscription, Resource Group and App Service Plan that you want to use for this application.</span></span>

    ![Einstellungendialogfeld für App Service-Erstellung](../../../images/api-aad-webapi-vs-create-app-service.png)

8. <span data-ttu-id="657bb-331">Bestätigen Sie Ihre Auswahl, indem Sie **Erstellen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-331">Confirm your choice by selecting **Create**.</span></span> <span data-ttu-id="657bb-332">Zu diesem Punkt erstellt Visual Studio eine neue Azure-Web-App zum Hosten Ihrer Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="657bb-332">Confirm your choice by clicking the Create button. At this point, Visual Studio will create a new Azure Web App to host your web application.</span></span>

#### <a name="add-support-for-cors"></a><span data-ttu-id="657bb-333">Hinzufügen der Unterstützung für CORS</span><span class="sxs-lookup"><span data-stu-id="657bb-333">Add support for CORS</span></span>

<span data-ttu-id="657bb-334">Standardmäßig bieten mit der Projektvorlage ASP.NET-Webanwendung erstellte APIs keine Unterstützung für CORS und können nicht von den Clientanwendungen aufgerufen werden, die auf unterschiedlichen Domänen gehostete werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-334">By default, APIs created using the ASP.NET Web Application project template don't support CORS and cannot be called by client-applications hosted on different domains. To add support for CORS to your WebAPI, click right on the project, and from the context menu choose the Manage NuGet Packages... option.</span></span> 

1. <span data-ttu-id="657bb-335">Um Ihrer Web-API Unterstützung für CORS hinzuzufügen, klicken Sie mit der rechten Maustaste auf das Projekt, und wählen Sie im Kontextmenü die Option **NuGet-Pakete verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="657bb-335">To add support for CORS to your Web API, right-click the project, and from the context menu, select the **Manage NuGet Packages** option.</span></span>

    ![Die Option „NuGet-Pakete verwalten“, hervorgehoben im Projektkontextmenü in Visual Studio](../../../images/api-aad-webapi-vs-manage-nuget.png)

2. <span data-ttu-id="657bb-337">Suchen Sie auf der Registerkarte **NuGet-Pakete verwalten** nach einem Paket mit dem Namen **Microsoft.AspNet.WebApi.Cors**, und installieren Sie es in Ihrem Projekt.</span><span class="sxs-lookup"><span data-stu-id="657bb-337">On the **Manage NuGet Packages** tab, search for a package named **Microsoft.AspNet.WebApi.Cors** and install it in your project.</span></span>

    ![Das Paket „Microsoft.AspNet.WebApi.Cors“, hervorgehoben auf der Registerkarte „NuGet-Pakete verwalten“](../../../images/api-aad-webapi-vs-cors-nuget.png)


#### <a name="add-data-model"></a><span data-ttu-id="657bb-339">Hinzufügen eines Datenmodells</span><span class="sxs-lookup"><span data-stu-id="657bb-339">Add data model</span></span>

<span data-ttu-id="657bb-340">Definieren Sie im Projekt ein Modell, das die von der API zurückgegebenen Daten darstellt.</span><span class="sxs-lookup"><span data-stu-id="657bb-340">In the project, define a model that represents the data returned by the API.</span></span> <span data-ttu-id="657bb-341">Fügen Sie im Ordner **Modelle** eine neue Klasse hinzu, und nennen Sie sie **Auftrag**.</span><span class="sxs-lookup"><span data-stu-id="657bb-341">In the **Models** folder, add a new class and name it **Order**.</span></span> <span data-ttu-id="657bb-342">Fügen Sie den folgenden Code in die neu erstellte Datei ein.</span><span class="sxs-lookup"><span data-stu-id="657bb-342">Paste the following code into the file.</span></span>

```cs
    using Newtonsoft.Json;
    using Newtonsoft.Json.Converters;
    using System;

    namespace PnP.Aad.Api.Models {
        public class Order {
            [JsonProperty(PropertyName = "id")]
            public int Id { get; set; }
            [JsonProperty(PropertyName = "orderDate")]
            public DateTime OrderDate { get; set; }
            [JsonConverter(typeof(StringEnumConverter))]
            [JsonProperty(PropertyName = "region")]
            public Region Region { get; set; }
            [JsonProperty(PropertyName = "rep")]
            public string Rep { get; set; }
            [JsonProperty(PropertyName = "item")]
            public string Item { get; set; }
            [JsonProperty(PropertyName = "units")]
            public uint Units { get; set; }
            [JsonProperty(PropertyName = "unitCost")]
            public double UnitCost { get; set; }
            [JsonProperty(PropertyName = "total")]
            public double Total { get; set; }
        }

        public enum Region {
            East,
            Central,
            West
        }
    }
```

#### <a name="add-orders-api"></a><span data-ttu-id="657bb-343">Hinzufügen der Auftrags-API</span><span class="sxs-lookup"><span data-stu-id="657bb-343">Add Orders API</span></span>

<span data-ttu-id="657bb-344">Fügen Sie eine API hinzu, die die Informationen zu den neuesten Aufträgen zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="657bb-344">Add an API that returns the information about the latest orders.</span></span> <span data-ttu-id="657bb-345">Erstellen Sie im Ordner **Controller** eine neue Klasse, und nennen Sie sie **OrdersController**.</span><span class="sxs-lookup"><span data-stu-id="657bb-345">In the **Controllers** folder, create a new class and name it **OrdersController**.</span></span> <span data-ttu-id="657bb-346">Fügen Sie den folgenden Code in die neu erstellte Datei ein.</span><span class="sxs-lookup"><span data-stu-id="657bb-346">Paste the following code into the file.</span></span>

```cs
using PnP.Aad.Api.Models;
using System;
using System.Collections.Generic;
using System.Web.Http;

namespace PnP.Aad.Api.Controllers {
    public class OrdersController : ApiController {
        private List<Order> orders = new List<Order> {
            new Order {
                Id = 1,
                OrderDate = new DateTime(2016, 1, 6),
                Region = Region.East,
                Rep = "Jones",
                Item = "Pencil",
                Units = 95,
                UnitCost = 1.99,
                Total = 189.05
            },
            new Order {
                Id = 2,
                OrderDate = new DateTime(2016, 1, 23),
                Region = Region.Central,
                Rep = "Kivell",
                Item = "Binder",
                Units = 50,
                UnitCost = 19.99,
                Total = 999.50
            },
            new Order {
                Id = 3,
                OrderDate = new DateTime(2016, 2, 9),
                Region = Region.Central,
                Rep = "Jardine",
                Item = "Pencil",
                Units = 36,
                UnitCost = 4.99,
                Total = 179.64
            },
            new Order {
                Id = 4,
                OrderDate = new DateTime(2016, 2, 26),
                Region = Region.Central,
                Rep = "Gill",
                Item = "Pen",
                Units = 27,
                UnitCost = 19.99,
                Total = 539.73
            },
            new Order {
                Id = 5,
                OrderDate = new DateTime(2016, 3, 15),
                Region = Region.West,
                Rep = "Sorvino",
                Item = "Pencil",
                Units = 56,
                UnitCost = 2.99,
                Total = 167.44
            }
        };

        public IEnumerable<Order> Get() {
            return orders;
        }
    }
}
```

#### <a name="extend-the-api-with-support-for-cors"></a><span data-ttu-id="657bb-347">Erweitern der API zur Unterstützung von CORS</span><span class="sxs-lookup"><span data-stu-id="657bb-347">Extend the API with support for CORS</span></span>

<span data-ttu-id="657bb-348">Auch wenn Sie in Ihrem Projekt Unterstützung für CORS installiert haben, wird die Option noch nicht aktiv verwendet.</span><span class="sxs-lookup"><span data-stu-id="657bb-348">Even though you have installed support for CORS in your project, it's not being actively used yet.</span></span> <span data-ttu-id="657bb-349">Wenn Sie von einer Clientanwendung in einer anderen Domäne die neu erstellte „Aufträge“-API aufrufen, erhalten Sie einen CORS-Fehler und die Anforderung schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="657bb-349">If you call the newly created Orders API from a client application hosted on another domain, you get a CORS error and the request fails.</span></span> 

1. <span data-ttu-id="657bb-350">Damit eine API CORS unterstützt, muss sie durch das Attribut **EnableCors** ergänzt werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-350">For an API to support CORS, it has to be decorated with the **EnableCors** attribute.</span></span>

    ```cs
    using PnP.Aad.Api.Models;
    using System;
    using System.Collections.Generic;
    using System.Web.Http;
    using System.Web.Http.Cors;

    namespace PnP.Aad.Api.Controllers {
        public class OrdersController : ApiController {
            private List<Order> orders = new List<Order> {
                // ...
            };

            [EnableCors("*", "*", "GET", SupportsCredentials = true)]
            public IEnumerable<Order> Get() {
                return orders;
            }
        }
    }
    ```

2. <span data-ttu-id="657bb-351">Öffnen Sie die Datei **.\App_Start\WebApiConfig.cs**, und fügen Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="657bb-351">Next, open the **.\App_Start\WebApiConfig.cs** file and paste the following code:</span></span>

    ```cs
    using System.Web.Http;

    namespace PnP.Aad.Api {
        public static class WebApiConfig {
            public static void Register(HttpConfiguration config) {
                // Web API configuration and services

                // Web API routes
                config.MapHttpAttributeRoutes();

                config.EnableCors();

                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
    }
    ```

<span data-ttu-id="657bb-352">An diesem Punkt ist der API-Code vollständig und kann in der Azure-Web-App veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-352">At this point, the API is code complete and can be published to the Azure Web App.</span></span>

#### <a name="publish-the-api-to-azure-web-app"></a><span data-ttu-id="657bb-353">Veröffentlichen der API in der Azure-Web-App</span><span class="sxs-lookup"><span data-stu-id="657bb-353">Publish the API to Azure Web App</span></span>

1. <span data-ttu-id="657bb-354">Klicken Sie in Visual Studio mit der rechten Maustaste auf das Projekt, und wählen Sie im Kontextmenü die Option **Veröffentlichen **.</span><span class="sxs-lookup"><span data-stu-id="657bb-354">In Visual Studio, right click on the project, and from the context menu choose the **Publish...** option.</span></span>

    ![Die Option „Veröffentlichen“, hervorgehoben im Kontextmenü des Projekts](../../../images/api-aad-webapi-vs-publish.png)

2. <span data-ttu-id="657bb-356">Stellen Sie sicher, dass im Dialogfeld **Veröffentlichen** alle Informationen richtig sind, und wählen Sie die Schaltfläche **Veröffentlichen** aus, um den Veröffentlichungsvorgang zu starten.</span><span class="sxs-lookup"><span data-stu-id="657bb-356">In the Publish dialog, verify that all information is correct and click the Publish button to start the publishing process.</span></span>

    ![Dialogfeld „Veröffentlichen“ mit den Veröffentlichungsinformationen](../../../images/api-aad-webapi-vs-publish-settings.png)

3. <span data-ttu-id="657bb-358">Nach Abschluss des Veröffentlichungsvorgangs navigieren Sie in Ihrem Webbrowser zur URL-API, z. B. `http://pnp-aad-api.azurewebsites.net/api/orders`.</span><span class="sxs-lookup"><span data-stu-id="657bb-358">After the publishing process completes, navigate in your web browser to the API URL, for example, `http://pnp-aad-api.azurewebsites.net/api/orders`.</span></span> <span data-ttu-id="657bb-359">An diesem Punkt ist die API nicht gesichert, und anonyme Benutzer können auf sie zugreifen.</span><span class="sxs-lookup"><span data-stu-id="657bb-359">Once the publishing process completes, navigate in your web browser to the API URL, eg. http://pnp-aad-api.azurewebsites.net/api/orders. At this point the API is not secured and can be accessed by anonymous users.</span></span>

    ![API-Antwort, die im Webbrowser für einen anonymen Benutzer angezeigt wird](../../../images/api-aad-webapi-response-anonymous.png)

#### <a name="secure-the-api-using-azure-app-service"></a><span data-ttu-id="657bb-361">Sichern der API durch Azure App Service</span><span class="sxs-lookup"><span data-stu-id="657bb-361">Secure the API using Azure App Service</span></span>

1. <span data-ttu-id="657bb-362">Um die API mithilfe von Azure AD zu sichern, wechseln Sie zum Azure-Portal, und öffnen Sie das Web-App-Hosting Ihrer API.</span><span class="sxs-lookup"><span data-stu-id="657bb-362">To secure the API using Azure AD go to the Azure Portal and open the Web App hosting your API. From the Settings group, select the Authentication / Authorization option.</span></span> 

2. <span data-ttu-id="657bb-363">Wählen Sie in der Gruppe **Einstellungen** die Option **Authentifizierung/Autorisierung** aus.</span><span class="sxs-lookup"><span data-stu-id="657bb-363">From the **Settings** group, select the **Authentication / Authorization** option.</span></span>

    ![Seite „Authentifizierung/Autorisierung“ von Azure App Service, angezeigt im Azure-Portal](../../../images/api-aad-webapi-authentication.png)

3. <span data-ttu-id="657bb-365">Legen Sie zum Aktivieren der Authentifizierung für Ihre Web App die Option **App Service-Authentifizierung** auf **Ein** fest.</span><span class="sxs-lookup"><span data-stu-id="657bb-365">To enable authentication for your Web App, set the **App Service Authentication** toggle to **On**.</span></span>

    ![Option „App Service-Authentifizierung“, für die Web-App, die die WebAPI hostet, auf „Ein“ festgelegt ](../../../images/api-aad-webapi-authentication-on.png)

4. <span data-ttu-id="657bb-367">Um den anonymen Zugriff auf die API zu verweigern, wählen Sie in der Liste **Die auszuführende Aktion, wenn die Anforderung nicht authentifiziert ist** die Option **Mit Azure Active Directory anmelden** aus.</span><span class="sxs-lookup"><span data-stu-id="657bb-367">To disallow anonymous access to the API, in the **Action to take when request is not authenticated** drop-down, select the **Login with Azure Active Directory** option.</span></span>

    ![Die Option „Mit Azure Active Directory anmelden“, ausgewählt im Dropdownmenü „Die auszuführende Aktion, wenn die Anforderung nicht authentifiziert ist“ in den Einstellungen für die Web-App-Authentifizierung](../../../images/api-aad-webapi-authentication-aad-login.png)

5. <span data-ttu-id="657bb-369">Konfigurieren Sie die Azure Active Directory-Authentifizierung in der Liste der Authentifizierungsanbieter, indem Sie **Azure Active Directory** auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-369">Finally, configure Azure Active Directory authentication by from the list of authentication providers selecting **Azure Active Directory**.</span></span>

    ![Azure Active Directory, hervorgehoben in der Liste der Authentifizierungsanbieter](../../../images/api-aad-webapi-authentication-aad.png)

6. <span data-ttu-id="657bb-371">Stellen Sie auf dem Blatt **Active Directory-Authentifizierung** den **Verwaltungsmodus** auf **Express** ein, und erstellen Sie eine neue Azure AD-App.</span><span class="sxs-lookup"><span data-stu-id="657bb-371">On the Active Directory Authentication blade, set the **Management mode** to **Express** and create a new AAD app.</span></span>

    > [!IMPORTANT] 
    > <span data-ttu-id="657bb-372">Wenn Sie den Konfigurationsmodus Express verwenden, erstellt das Azure-Portal eine neue Azure AD-Anwendung im gleichen Verzeichnis, in dem sich auch die Funktionen-App befindet.</span><span class="sxs-lookup"><span data-stu-id="657bb-372">When using the Express configuration mode, the Azure Portal creates a new Azure AD application from the same directory where the Function App is located.</span></span> <span data-ttu-id="657bb-373">Wenn die Funktionen-App in einem anderen Azure-Abonnement mit einem anderen Verzeichnis gehostet wird, sollten Sie stattdessen den erweiterten Modus verwenden und die ID des Verzeichnisses und der Anwendung angeben, die zum Sichern des Zugriffs auf die API verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="657bb-373">Important: when using the express configuration mode, the Azure Portal will create a new AAD application from the same directory as where the Function App is located. If the Function App is hosted in a different Azure subscription with a different directory, you should use the advanced mode instead, and specify the ID of the directory and application that should be used to secure the access to the API.</span></span>
    >
    > <span data-ttu-id="657bb-374">Wenn Sie vorhandene Azure AD-Anwendungen verwenden, konfigurieren Sie die Anwendung so, dass nur Anmeldeinformationen von einem einzigen Mandanten akzeptiert werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-374">When using existing Azure AD applications, configure the application to accept credentials from a single tenant only.</span></span> <span data-ttu-id="657bb-375">Durch das Konfigurieren der Anwendung für mehrere Mandanten können Benutzer mit einem gültigen Organisations- oder persönlichen Konto eine Verbindung mit Ihrer API herstellen.</span><span class="sxs-lookup"><span data-stu-id="657bb-375">When using existing AAD applications you should configure the application to accept credentials from a single tenant only. Configuring the application as multi-tenant would allow any user with a valid organization or personal account to connect to your API.</span></span>
    >
    > <span data-ttu-id="657bb-376">Die Verwendung einer Azure AD-Anwendung für das Sichern des Zugriffs auf Ihre API bezieht sich nur auf die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="657bb-376">Using an Azure AD application to secure the access to your API only accounts for authentication.</span></span> <span data-ttu-id="657bb-377">Beim Erstellen Ihrer API müssen Sie auch Anforderungen im Code der API autorisieren, um sicherzustellen, dass nur Benutzer mit entsprechenden Berechtigungen die API verwenden.</span><span class="sxs-lookup"><span data-stu-id="657bb-377">Using an AAD application to secure the access to your API only accounts for authentication. When building your API, you should also authorize requests in your API's code, to ensure that only users with sufficient privileges are using the API.</span></span>

7. <span data-ttu-id="657bb-378">Da die App nur zum Sichern des Zugriffs auf die Azure-Funktion vorgesehen ist, sind keine zusätzlichen Berechtigungen erforderlich. </span><span class="sxs-lookup"><span data-stu-id="657bb-378">Because the app is only meant to secure the access to the Azure Function, it doesn't require any additional permissions. Confirm the selection by clicking the OK button.</span></span> <span data-ttu-id="657bb-379">Bestätigen Sie die Auswahl, indem Sie **OK** auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-379">Confirm the selection by selecting **OK**.</span></span>

    ![Azure Active Directory-Authentifizierungseinstellungen](../../../images/api-aad-webapi-authentication-aad-ok.png)

8. <span data-ttu-id="657bb-381">Wenn das Blatt **Azure Active Directory** geschlossen wird, wählen Sie auf dem Blatt **Authentifizierung/Autorisierung** **Speichern** aus, um alle Änderungen an den Authentifizierungseinstellungen zu bestätigen.</span><span class="sxs-lookup"><span data-stu-id="657bb-381">When the Azure Active Directory blade closes, back on the Authentication / Authorization blade, click the Save button to confirm all changes to authentication settings.</span></span>

    ![Die Schaltfläche „Speichern“, hervorgehoben auf dem Blatt „Authentifizierung/Autorisierung“](../../../images/api-aad-webapi-authentication-save.png)

9. <span data-ttu-id="657bb-383">Wenn Sie versuchen, in einem neuen privaten Fenster zur API-URL zu navigieren, sollten Sie aufgefordert werden, sich mit Ihrem Azure AD-Konto anzumelden.</span><span class="sxs-lookup"><span data-stu-id="657bb-383">If you try to navigate to your API URL in a new private window, you should be prompted to sign in using your Azure AD account.</span></span>

    ![Azure AD-Anmeldeseite](../../../images/api-aad-webapi-azure-sign-in.png)

<span data-ttu-id="657bb-385">Zu diesem Zeitpunkt ist die API bereit, mit dem Authentifizierungscookie sicher von einem clientseitigen SharePoint-Framework-Webpart aufgerufen zu werden.</span><span class="sxs-lookup"><span data-stu-id="657bb-385">At this point, the API is ready to be called securely from a SharePoint Framework client-side web part using the authentication cookie.</span></span>

#### <a name="secure-the-api-using-openid"></a><span data-ttu-id="657bb-386">Sichern der API mit OpenID</span><span class="sxs-lookup"><span data-stu-id="657bb-386">Secure the API using OpenID</span></span>

<span data-ttu-id="657bb-387">Wenn Sie Ihr ASP.NET-Web-API-Projekt an einem anderen Ort als dem Azure App Service bereitstellen und es mit Azure AD sichern möchten, können Sie sich nicht auf die App Service-Authentifizierung verlassen.</span><span class="sxs-lookup"><span data-stu-id="657bb-387">If you want to deploy your ASP.NET WebAPI project to other location than Azure App Service and want it to be secured with AAD, you can't rely on App Service Authentication. Instead, you have to extend the Web Application to require itself its users to authenticate before they can use the API.</span></span> <span data-ttu-id="657bb-388">Stattdessen müssen Sie die Webanwendung so erweitern, dass Benutzer zur Authentifizierung aufgefordert werden, bevor sie die API verwenden können.</span><span class="sxs-lookup"><span data-stu-id="657bb-388">Instead, you have to extend the web application to require its users to authenticate before they can use the API.</span></span>

##### <a name="disable-anonymous-access-to-all-resources"></a><span data-ttu-id="657bb-389">Deaktivieren des anonymen Zugriffs auf alle Ressourcen</span><span class="sxs-lookup"><span data-stu-id="657bb-389">Disable anonymous access to all resources</span></span>

1. <span data-ttu-id="657bb-390">Ausgehend davon, dass alle Ressourcen gesichert sein sollen,öffnen Sie die Datei **.\App_Start\FilterConfig.cs**, und fügen Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="657bb-390">Assuming you want all resources secured, open the **.\App_Start\FilterConfig.cs** file and paste the following code:</span></span>

    ```cs
    using System.Web.Mvc;

    namespace PnP.Aad.Api {
        public class FilterConfig {
            public static void RegisterGlobalFilters(GlobalFilterCollection filters) {
                filters.Add(new HandleErrorAttribute());
                filters.Add(new AuthorizeAttribute());
            }
        }
    }
    ```

2. <span data-ttu-id="657bb-391">Um die Authentifizierung für alle APIs vorauszusetzen, öffnen Sie die Datei **.\App_Start\WebApiConfig.cs**, und fügen Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="657bb-391">To require authentication for all APIs, open the **.\App_Start\WebApiConfig.cs** file and paste the following code:</span></span>

    ```cs
    using System.Web.Http;

    namespace PnP.Aad.Api {
        public static class WebApiConfig {
            public static void Register(HttpConfiguration config) {
                // Web API configuration and services

                // Web API routes
                config.MapHttpAttributeRoutes();

                config.EnableCors();
                config.Filters.Add(new AuthorizeAttribute());

                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
    }
    ```

3. <span data-ttu-id="657bb-392">Wenn Sie versuchen, entweder auf die API oder eine andere Ressource in der Webanwendung zuzugreifen, erhalten Sie die Fehlermeldung „401 - nicht autorisiert“.</span><span class="sxs-lookup"><span data-stu-id="657bb-392">If you would try to access either the API or any other resource in your web application, you would get a 401 Unauthorized response.</span></span>

    ![Antwort „Nicht autorisiert“ bei dem Versuch, auf die API zuzugreifen](../../../images/api-aad-webapi-anonymous-unauthorized.png)

<span data-ttu-id="657bb-394">An diesem Punkt setzt die Webanwendung voraus, dass alle Anforderungen an ihre Ressourcen authentifiziert werden, aber sie startet nicht den Azure AD-Anmeldefluss.</span><span class="sxs-lookup"><span data-stu-id="657bb-394">At this point, the web application requires that all requests to its resources are authenticated, but it doesn't start the Azure AD sign-in flow.</span></span> 

<span data-ttu-id="657bb-395">In den folgenden Schritten erweitern Sie die Webanwendung so, dass Benutzer zur Azure AD-Anmeldeseite weitergeleitet werden, wenn sie zuvor nicht authentifiziert wurden.</span><span class="sxs-lookup"><span data-stu-id="657bb-395">In the following steps, you extend the web application so that it redirects users to the Azure AD sign-in page, if they weren't previously authenticated.</span></span>

##### <a name="register-azure-ad-application"></a><span data-ttu-id="657bb-396">Registrieren der Azure AD-Anwendung</span><span class="sxs-lookup"><span data-stu-id="657bb-396">Register Azure AD application</span></span>

<span data-ttu-id="657bb-397">Um eine API mit Azure AD zu sichern, müssen Sie eine Azure AD-Anwendung registrieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-397">To secure an API with Azure AD, you need to register an Azure AD application.</span></span> <span data-ttu-id="657bb-398">Auf diese Anwendung wird dann im Webanwendungsprojekt verwiesen, und die OWIN-Middleware verwendet sie zum Sichern des Zugriffs auf Ihre API mit Azure AD.</span><span class="sxs-lookup"><span data-stu-id="657bb-398">In order to secure an API with Azure Active Directory, you need to register an Azure AD application. This application is then referenced in the web application project and used by the OWIN middleware to secure the access to your API with Azure AD.</span></span>

1. <span data-ttu-id="657bb-399">Wenn Sie noch keine Azure AD-Anwendung haben, können Sie eine im Azure-Portal erstellen, indem Sie das Blatt **Azure Active Directory** aufrufen.</span><span class="sxs-lookup"><span data-stu-id="657bb-399">If you don't have an existing AAD application yet, you can create one in the Azure Portal, by navigating to the Azure Active Directory blade.</span></span>

    > [!IMPORTANT] 
    > <span data-ttu-id="657bb-400">Die Azure AD-Anwendung, die zum Sichern der API verwendet wird, muss in demselben Azure Active Directory erstellt werden, das Ihre Organisation zum Zugreifen auf Office 365 verwendet.</span><span class="sxs-lookup"><span data-stu-id="657bb-400">Important: the Azure AD application, used to secure the API, should be created in the same Azure Active Directory which is used by your organization to access Office 365.</span></span>

    ![Blatt „Azure Active Directory“, geöffnet im Azure-Portal](../../../images/api-aad-webapi-azure-aad.png)

2. <span data-ttu-id="657bb-402">Wechseln Sie auf dem Blatt **Azure Active Directory** zum Blatt **App-Registrierungen**.</span><span class="sxs-lookup"><span data-stu-id="657bb-402">On the Azure Active Directory blade, navigate to the **App registrations** blade.</span></span>

    ![Abschnitt „App-Registrierungen“, hervorgehoben auf dem Blatt „Azure Active Directory“](../../../images/api-aad-webapi-azure-app-registrations.png)

3. <span data-ttu-id="657bb-404">Klicken Sie auf dem Blatt **App-Registrierungen** auf die Schaltfläche **Registrierung einer neuen Anwendung**, um eine neue Azure AD-Anwendung zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-404">On the **App registrations** blade, click the **New application registration** button to register a new Azure AD application.</span></span>

    ![Die Schaltfläche „Registrierung einer neuen Anwendung“, hervorgehoben auf dem Blatt „App-Registrierungen“](../../../images/api-aad-webapi-azure-new-app-registration.png)

4. <span data-ttu-id="657bb-406">Stellen Sie auf dem Blatt **Erstellen** die Informationen zu Ihrer Anwendung bereit, und bestätigen Sie die Erstellung, indem Sie **Erstellen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="657bb-406">On the **Create** blade, provide the information about your application and confirm the creation by clicking the **Create** button.</span></span>

    ![Die Schaltfläche „Erstellen“, hervorgehoben auf dem Blatt zum Erstellen einer neuen Anwendungsregistrierung](../../../images/api-aad-webapi-azure-new-app-registration-create.png)

5. <span data-ttu-id="657bb-408">Nachdem die Anwendungsregistrierung erfolgreich erstellt wurde, wählen Sie diese in der Liste aus, um die Details anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="657bb-408">After the application registration is successfully created, select it in the list to view its details.</span></span>

    ![Im Azure-Portal angezeigte Informationen zur Anwendungsregistrierung](../../../images/api-aad-webapi-azure-app-details.png)

6. <span data-ttu-id="657bb-410">Kopieren Sie aus den Informationen zur Anwendungsregistrierung die **ID der Anwendung**, und speichern Sie diese, da Sie sie bei der Konfiguration der Azure AD-Authentifizierung für Ihre Webanwendung benötigen.</span><span class="sxs-lookup"><span data-stu-id="657bb-410">From the application registration information, copy the **Application ID** and store it as you will need it when configure Azure AD authentication for your web application.</span></span>

##### <a name="redirect-anonymous-requests-to-azure-ad-sign-in-page"></a><span data-ttu-id="657bb-411">Umleiten von anonymen Anforderungen zur Azure AD-Anmeldeseite</span><span class="sxs-lookup"><span data-stu-id="657bb-411">Redirect anonymous requests to Azure AD login page</span></span>

1. <span data-ttu-id="657bb-412">Klicken Sie in Visual Studio mit der rechten Maustaste auf das Projekt, und wählen Sie im Kontextmenü die Option **NuGet-Pakete verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="657bb-412">In Visual Studio, rightclick the project, and from the context menu, select the **Manage NuGet Packages** option.</span></span> 

2. <span data-ttu-id="657bb-413">Fügen Sie im Fenster **NuGet-Pakete verwalten** die folgenden Pakete zum Projekt hinzu:</span><span class="sxs-lookup"><span data-stu-id="657bb-413">In the **Manage NuGet Packages** window, add the following packages to your project:</span></span>

    - <span data-ttu-id="657bb-414">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="657bb-414">Microsoft.Owin.Host.SystemWeb</span></span>
    - <span data-ttu-id="657bb-415">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="657bb-415">Microsoft.Owin.Security.Cookies</span></span>
    - <span data-ttu-id="657bb-416">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="657bb-416">Microsoft.Owin.Security.OpenIdConnect</span></span>

3. <span data-ttu-id="657bb-417">Fügen Sie im Stammverzeichnis des Projekts eine neue Klasse mit dem Namen **Startup** hinzu, und fügen Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="657bb-417">In the root directory of your project, add a new class named **Startup** and paste the following code:</span></span>

    ```cs
    using Owin;

    namespace PnP.Aad.Api {
        public partial class Startup
        {
            public void Configuration(IAppBuilder app)
            {
                ConfigureAuth(app);
            }
        }
    }
    ```

4. <span data-ttu-id="657bb-418">Erstellen Sie im Ordner **App_Start** eine neue Klasse mit dem Namen **Startup.Auth**, und fügen Sie den folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="657bb-418">Then, in the **App_Start** folder, create a new class named **Startup.Auth** and paste the following code:</span></span>

    ```cs
    using Microsoft.Owin.Security;
    using Microsoft.Owin.Security.Cookies;
    using Microsoft.Owin.Security.OpenIdConnect;
    using Owin;
    using System.Configuration;

    namespace PnP.Aad.Api {
        public partial class Startup {
            // For more information on configuring authentication, please visit http://go.microsoft.com/fwlink/?LinkId=301864
            public void ConfigureAuth(IAppBuilder app) {
                app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

                app.UseCookieAuthentication(new CookieAuthenticationOptions());

                app.UseOpenIdConnectAuthentication(
                    new OpenIdConnectAuthenticationOptions {
                        ClientId = ConfigurationManager.AppSettings["ida:ClientId"],
                        Authority = $"https://login.microsoftonline.com/{(ConfigurationManager.AppSettings["ida:Tenant"])}",
                        PostLogoutRedirectUri = ConfigurationManager.AppSettings["ida:PostLogoutRedirectUri"],
                    });
            }
        }
    }
    ```

5. <span data-ttu-id="657bb-419">Öffnen Sie in Visual Studio die Datei **Web.config**, und fügen Sie im Abschnitt **appSettings** die folgenden Elemente hinzu:</span><span class="sxs-lookup"><span data-stu-id="657bb-419">In Visual Studio, open the **Web.config** file and in the **appSettings** section add the following elements:</span></span>

    ```xml
    <add key="ida:Tenant" value="contoso.onmicrosoft.com" />
    <add key="ida:ClientId" value="eeb40f1f-c5fa-4096-896b-71c77d459e21" />
    <add key="ida:PostLogoutRedirectUri" value="https://localhost:44320/" />
    ```

    - <span data-ttu-id="657bb-420">Der Wert des Schlüssels **ida:Tenat** ist der Name des Azure AD, in dem die Azure AD-App definiert ist, die zum Sichern der API verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="657bb-420">The value of the **ida:Tenant** key is the name of the Azure AD where the Azure AD app used to secure the API is defined.</span></span> 
    - <span data-ttu-id="657bb-421">**ida:ClientId** gibt die ID der Azure AD-Anwendung an, die verwendet wird, um die API zu sichern.</span><span class="sxs-lookup"><span data-stu-id="657bb-421">**ida:ClientId** specifies the ID of the Azure AD application used to secure the API.</span></span> 
    - <span data-ttu-id="657bb-422">Die in der Eigenschaft **Ida: PostLogoutRedirectUri** angegebene URL ist das Ziel, zu dem Azure AD Benutzer nach dem Abmelden von der Anwendung weiterleiten würde. Dieses wird in diesem Fall nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="657bb-422">The URL specified in the **ida:PostLogoutRedirectUri** property is where Azure AD would redirect to after signing out of your application, which isn't used in this case.</span></span>

<span data-ttu-id="657bb-423">Dadurch wird der Konfigurationsvorgang abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="657bb-423">This concludes the configuration process.</span></span> <span data-ttu-id="657bb-424">Wenn Sie Ihre Webanwendung starten, ehe Sie auf die Ressourcen zugreifen können, werden Sie aufgefordert, sich mit Ihrem Azure AD-Konto anzumelden.</span><span class="sxs-lookup"><span data-stu-id="657bb-424">If you start your web application, before you are able to access any of its resources, you are prompted to sign in with your Azure AD account.</span></span> <span data-ttu-id="657bb-425">Um sicherzustellen, dass nur autorisierte Benutzer auf eine bestimmte API zugreifen, sollten Sie in Ihren benutzerdefinierten APIs Autorisierung implementieren.</span><span class="sxs-lookup"><span data-stu-id="657bb-425">To ensure that only authorized users are accessing the particular API, you should implement authorization in your custom APIs.</span></span> <span data-ttu-id="657bb-426">Dazu können Sie den Benutzernamen aus der Eigenschaft `RequestContext.Principal.Identity` abrufen und ihn mit Ihrer Sicherheitsmatrix abgleichen.</span><span class="sxs-lookup"><span data-stu-id="657bb-426">You can do that by retrieving the user name from the `RequestContext.Principal.Identity` property, and verifying it against your security matrix.</span></span>

## <a name="see-also"></a><span data-ttu-id="657bb-427">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="657bb-427">See also</span></span>

- [<span data-ttu-id="657bb-428">Aufrufen von benutzerdefinierten APIs, die mit Azure Active Directory ohne ADAL JS gesichert sind (Codebeispiel)</span><span class="sxs-lookup"><span data-stu-id="657bb-428"> Call custom APIs secured with Azure Active Directory without ADAL JS (code sample)</span></span>](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/aad-api-spo-cookie)
