---
title: 'Bereitstellen von Websites in Office 365 Development in Microsoft Azure #'
ms.date: 11/03/2017
ms.openlocfilehash: c7e975f54da33125d6e8261efa1b525ba525747d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="deploying-development-office-365-sites-to-microsoft-azure"></a>Bereitstellen von Websites in Office 365 Development in Microsoft Azure #

### <a name="summary"></a>Summary ###

Bei der Entwicklung von beliebigen Typs aus einer Webanwendung, ist die meisten Entwicklung lokal mit http://localhost durchgeführt. Einige Projekte verwenden Sie lokale Ressourcen oder eine Kombination von Ressourcen für lokale und Remoteverbindungen. Nutzen diese Projekte aus lokalen entwicklungsumgebungen umfasst eine Reihe von Aufgaben ausführen, wie beispielsweise das Ändern der Datenbank-Verbindungszeichenfolgen, URLs, Konfigurationen usw..

Web, Projekte, die die Office 365-APIs nutzen unterscheiden sich nicht. Diese Projekte nutzen von Microsoft Azure AD-Dienst zum Authentifizieren der Anwendungen und OAuth 2.0-Zugriffstoken zu erhalten. Diese Token werden durch die Webanwendungen zur Authentifizierung mit den Office 365-APIs verwendet.

Auf dieser Seite erläutert die Schritte zum Offlineschalten einer Office 365-API-Entwicklungsprojekt und starten es an ein Arbeitsbeispiel vollständig in Microsoft Azure mit [Office 365](http://products.office.com/en-us/business/explore-office-365-for-business), [Azure Active Directory](http://azure.microsoft.com/en-us/services/active-directory/) & [Azure Websites] (http:// gehostet Azure.Microsoft.com/en-US/Services/Websites/.

Bereitstellen einer Office 365-API-Web-Anwendung in Microsoft Azure aus einer lokalen Entwicklungsumgebung muss drei allgemeine Schritte ausgeführt werden, wie auf dieser Seite beschrieben:

- [Erstellen und Konfigurieren einer Azure-Website](#create-and-configure-an-azure-website)
- [Konfigurieren der Azure AD-Anwendung](#configure-the-azure-ad-application)
- [Konfigurieren Sie das Projekt ASP.NET](#configure-the-aspnet-project)
- [Bereitstellen von Office 365-API ASP.NET-Webanwendung](#deploy-the-office-365-api-aspnet-web-application)

> Auf dieser Seite wird davon ausgegangen, dass Sie eine lokale Arbeiten ASP.NET-Anwendung verfügen, die die Office 365-APIs verwendet. Zur Referenz wird das **[O365-WebApp-SingleTenant](https://github.com/SharePoint/O365-WebApp-SingleTenant)** das Projekt wurde gefunden in **[OfficeDev](https://github.com/SharePoint)** Konto GitHub verwendet.

# <a name="create-and-configure-an-azure-website"></a>Erstellen und Konfigurieren einer Azure-Website

In diesem Schritt erstellen Sie eine Azure-Website, die zum Hosten der Anwendung verwendet werden. 

1. Navigieren Sie zu der [Azure-Verwaltungsportal](https://manage.windowsazure.com) und melden Sie sich mit Ihrem Organisations-ID-Konto.
1. Wählen Sie nach der Anmeldung in der Navigation Randleiste **WEBSITES**.
1. Klicken Sie auf der Seite **Websites** auf den Link **neu** in der Fußzeile in der unteren linken Ecke der Seite gefunden.
1. Der Assistent, der angezeigt wird, wählen Sie **Für schnelles Erstellen**, geben Sie einen Namen für die Website im Feld **URL** wählen Sie in einer **Web-Hosting planen** und **Abonnement**. 

  ![Die Einstellungen für schnelles erstellen: das URL-Feld o365api-01 festgelegt ist, Web-Hosting planen auf Default1 festgelegt ist (ostasiatischen US, Standard) Abonnement auf Azure MSDN (primär) festgelegt ist.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-01.png)

  > Stellen Sie sicher, dass Sie notieren Sie den Namen der Website beibehalten, den Sie erstellen, wie es später benötigt werden.

1. Klicken Sie dann auf den Link **Website erstellen** , um die Website zu erstellen.

Geben Sie Azure einen Moment Zeit, um die Website zu erstellen. Nach dem Erstellen der Website können Sie die *app-Einstellungen* über die Webschnittstelle angeben. Hiermit können Sie alle außer Kraft setzen `<appSettings>` innerhalb des Projekts `web.config` Datei über die Verwaltung der Weboberfläche für die Website ohne die Bereitstellung von Ihrer Website Codebasis für einfache `web.config` Änderungen.

1. Klicken Sie auf der Website, die Sie gerade erstellt, in der **Azure-Verwaltungsportal haben**.
1. Klicken Sie auf den Link **Konfigurieren** in der oberen Navigationsleiste.
1. Führen Sie einen Bildlauf nach unten zum Abschnitt **App-Einstellungen** , und fügen Sie drei neue Einträge hinzu:
  - **IDA: ClientID**
  - **IDA: Kennwort** 
  - **IDA: TenantID** 
1. Kopieren Sie die entsprechenden Werte aus des arbeiten Projekts `web.config` auf diese Einstellungswerte in der Azure-Website wie in der folgenden Abbildung dargestellt:

  ![WEBSITE_NODE_DEFAULT_VERSION ist 0.10.32, Ida: ClientID 92b1e137-c36f-4bfe-9e1c-01ef546ce4a9, Ida: Kennwort ist Bns06N18ZiyYfMcyU9qUfGnZbnkBiPZfUptLDsU6cml, Ida: TenantId ist teilweise geschwärzten. Sind die Nummern Center, der die GUID - 45ee - 8afc-.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-02.png)

1. Klicken Sie in der Fußzeile auf die Schaltfläche **Speichern** , um die Änderungen zu speichern.

Zu diesem Zeitpunkt die Azure-Website wird Setup und so konfiguriert, dass das Office 365-API-Webprojekt hosten, das die in einem späteren Schritt bereitgestellt werden.

[zurück zum Seitenanfang](#deploying-development-office-365-sites-to-microsoft-azure)

# <a name="configure-the-azure-ad-application"></a>Konfigurieren der Azure AD-Anwendung

In diesem Schritt ändern Sie die Azure AD-Anwendung verwendet bei der Entwicklung und Testen der Anwendung Office 365.

1. Navigieren Sie zu der [Azure-Verwaltungsportal](https://manage.windowsazure.com) und melden Sie sich mit Ihrem Organisations-ID-Konto.
1. Wählen Sie nach der Anmeldung in der Navigation Randleiste mit **ACTIVE DIRECTORY**.
1. Wählen Sie auf der Seite **active Directory** das Verzeichnis, das mit Ihrem Office 365-Mandanten verknüpft ist.
1. Klicken Sie anschließend auf das **ANWENDUNGEN** -Element in der oberen Navigationsleiste.
1. Aktualisieren Sie innerhalb des Abschnitts **Eigenschaften** die **SIGN-ON URL** So zeigen Sie auf der Standard-URL der Azure-Website, die Sie erstellt haben. Beachten Sie den HTTPS-Endpunkt, der bereitgestellt wird mit allen Azure Websites verwenden.

  ![Name auf Office 365-WebApp-SingleTenant.Office365App festgelegt ist, Sign-on URL auf https://o365api-01.azurewebsites.net festgelegt ist](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-03.png)

1. Aktualisieren Sie innerhalb des Abschnitts **Single Sign-On** der **App ID URI** hinzufügt, um die Domäne der Azure-Website (in der folgenden Abbildung dargestellt) verwenden.
1. Aktualisieren Sie die **Antwort-URL** im nächsten Schritt, daher ist die einzige aufgelistete URL der Homepage der Azure-Website:

  ![App-ID URI ist https://o365api-01.azurewebsites.net/O365-WebApp-SingleTenant, Antwort-URL ist https://o365api-01.azurewebsites.net/](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-04.png)

1. Klicken Sie in der Fußzeile auf die Schaltfläche **Speichern** , um die Änderungen zu speichern.

Zu diesem Zeitpunkt wurde die Azure AD-Anwendung, die vom Office 365-API-Web-Projekt verwendet, um die neue Azure-Website entwickelt konfiguriert.

[zurück zum Seitenanfang](#deploying-development-office-365-sites-to-microsoft-azure)

# <a name="configure-the-aspnet-project"></a>Konfigurieren Sie das Projekt ASP.NET

In diesem Schritt konfigurieren Sie das Projekt ASP.NET in der Anwendung in die neue Azure-Website verwenden.

Für die beispielanwendung im Beispiel für diese Anweisungen verwendet ist kein zusätzlicher Aufwand tatsächlich erforderlich ist. Enthält jedoch die Webanwendung die Einstellungen in der `web.config` Datei für die Azure AD-Anwendung und Azure AD-Mandanten bei der Entwicklung verwendet. Einige Entwickler können mit verschiedenen Azure AD-Applikationen oder sogar auf verschiedene Azure-Abonnements für ihre Entwicklung und Produktion Instanzen auswählen.

In einem vorherigen Schritt auf dieser Seite beschrieben, bei der Erstellung der Azure-Website festlegen die Add-in-Einstellungen für die Anwendung, die in der Regel im gefunden wird die `web.config`. Zur Sicherstellung der Anwendung erhält diese Werte aus der Azure-Website Konfiguration empfohlen wird Sie ersetzen Sie die Werte in der `web.config` mit Platzhalter stattdessen Werte.

1. Öffnen Sie das Projekt `web.config` Datei.
1. Suchen Sie die Add-in-Einstellungen für **Ida: ClientID**, **Ida: Kennwort** und **Ida: TenantId**.
1. Ersetzen Sie die Werte dieser Einstellungen mit einem Platzhalterwert:

  ````xml
  <add key="ida:TenantId" value="set-in-azure-website-config" />
  <add key="ida:ClientID" value="set-in-azure-website-config" />
  <add key="ida:Password" value="set-in-azure-website-config" />
  ````

1. Speichern Sie die Änderungen.

Die Webanwendung, Azure-Website und in Azure AD-Anwendung sind zu diesem Zeitpunkt alle ordnungsgemäß konfiguriert und bereitgestellt werden.

[zurück zum Seitenanfang](#deploying-development-office-365-sites-to-microsoft-azure)

# <a name="deploy-the-office-365-api-aspnet-web-application"></a>Bereitstellen von Office 365-API ASP.NET-Webanwendung

In diesem Schritt werden Sie Office 365-API-Webanwendung an, der Azure-Website veröffentlichen. Nach der Bereitstellung der Website sollten Sie testen, um sicherzustellen, dass alles wie gewünscht funktioniert.

> Dieser Schritt wird vorausgesetzt, dass er Microsoft [Azure SDK](http://azure.microsoft.com/en-us/downloads/), Version 2.0 oder höher, installiert. 

## <a name="deploy-the-aspnet-web-application"></a>Bereitstellen der ASP.NET-Webanwendung

1. Öffnen Sie Ihre Office 365-API-Webanwendung in Visual Studio 2013.
1. Klicken Sie im Fenster Projektmappen-Explorer-Tool mit der rechten Maustaste in des Projekts, und wählen Sie **Veröffentlichen** Starten der **Web veröffentlichen** -Assistent.
1. Wählen Sie auf der Registerkarte **Profil** **Microsoft Azure-Website**ein.

  Zu diesem Zeitpunkt werden Sie aufgefordert, zum Azure-Abonnement mit Ihrer Organisation ID anmelden

1. Wählen Sie nach der Anmeldung die Website, die Sie in einem vorherigen Schritt auf dieser Seite erstellt haben, und klicken Sie auf **OK**.

  ![Im Dialogfeld die vorhandene Website auswählen zeigt, dass für vorhandene Websites o365api-01 festgelegt.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-05.png)

1. Klicken Sie auf der Registerkarte **Verbindung** auf die Schaltfläche **Verbindung überprüfen** , um sicherzustellen, das Verbindungsprofil erfolgreich heruntergeladen und angewendet wurde.

  ![Ein Pfeil verweist auf die Schaltfläche Verbindung überprüfen unten im Dialogfeld mit ein grünes Häkchen neben der Schaltfläche angezeigt.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-06.png)

1. Klicken Sie auf die Schaltfläche **Veröffentlichen** , um die Webanwendung der Azure-Website zu veröffentlichen.

## <a name="test-the-aspnet-web-application"></a>Testen Sie die ASP.NET-Webanwendung

Nach dem Veröffentlichen der Webanwendung auf der Azure-Website, Visual Studio öffnen ein Browsers und navigieren Sie zur Homepage der Website. 

Standardmäßig ist dies der HTTP-Endpunkt. Denken Sie daran aus dem vorherigen Schritt, wenn Sie die Azure AD-Anwendung so konfiguriert, dass nur Anmelde-Ons von HTTPS-Endpunkt akzeptieren festlegen. Bevor Sie dem Anwendungsupdate die Url verwenden, um an den HTTPS-Endpunkt zu verweisen.

1. Aktualisieren Sie im Browser die URL So wechseln zur Homepage HTTPS für die Azure-Website ein. Im Beispiel auf dieser Seite ist, https://o365api-01.azurewebsites.net.
1. Klicken Sie auf den Link " **Anmelden** " in der Kopfzeile in der oberen rechten Seitenrand. Dadurch werden Sie auf der Anmeldeseite angezeigt wird Azure AD weitergeleitet.

  > Wenn Sie zu diesem Zeitpunkt ein Fehler auftritt, ist es wahrscheinlich ein Problem mit den drei Add-in-Einstellungen, die Sie für die Azure-Website erstellt haben. Wechseln Sie wieder, und stellen Sie sicher, dass die Werte aus dem Azure AD-Mandanten & Anwendung die richtigen Werte sind. Sie sollte eine URL, die aussieht angezeigt. 

1. Nach der erfolgreichen Anmeldung werden Sie wieder auf der Homepage für die Webanwendung der Azure-Website umgeleitet werden, die Sie erstellt haben.

An dieser Stelle haben Sie Ihre Office 365-API-Webanwendungsprojekt zur Ausführung in Azure-Website erfolgreich bereitgestellt.

[zurück zum Seitenanfang](#deploying-development-office-365-sites-to-microsoft-azure)

----------

### <a name="related-links"></a>Verwandte links ###
-  [O365-WebApp-SingleTenant](https://github.com/SharePoint/O365-WebApp-SingleTenant)

### <a name="applies-to"></a>Gilt für ###
-  Office 365 mit mehreren Mandanten (MT)
-  Office 365 dedizierte (D)

### <a name="author"></a>Autor
Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)

### <a name="version-history"></a>Versionsverlauf ###
Version  | Datum | Kommentare
---------| -----| --------
0,1  | 2 Januar 2015 | Erster Entwurf


