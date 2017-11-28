---
title: "Remote Zeitgeberaufträge in der SharePoint-add-in-Objektmodell"
ms.date: 11/03/2017
ms.openlocfilehash: edd7747655afb18aee647a17e7c4e47d7af0b394
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="remote-timer-jobs-in-the-sharepoint-add-in-model"></a>Remote Zeitgeberaufträge in der SharePoint-add-in-Objektmodell
================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Implementieren von Zeitgeberaufträgen unterscheidet in das neue SharePoint-Add-in-Modell mit vollständigen vertrauen Code war.  In einer typischen vollständige vertrauen Code (FTC) / SharePoint-Zeitgeberaufträgen Farmlösung Szenario wurden durch den SharePoint Server-Side Object Model Code erstellt, über Farmlösungen bereitgestellt und in der Website der SharePoint-Zentraladministration verwaltet. SharePoint verarbeitet die Planung und die Ausführung des Zeitgeberauftrags in diesem Szenario. 

Im Modell SharePoint-Add-in Szenario Zeitgeberaufträge erstellt und außerhalb von SharePoint geplant.  SharePoint ist nicht für die Planung oder die Ausführung des Zeitgeberauftrags in diesem Szenario verantwortlich.

<a name="high-level-guidelines"></a>Allgemeine Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden allgemeinen Richtlinien für das Erstellen von Zeitgeberaufträgen bereitstellen.

- Zeitgeberaufträge sollte außerhalb von SharePoint implementiert werden.
- Planen von Zeitgeberaufträgen sollte außerhalb von SharePoint implementiert werden.
- Zeitgeberaufträge sollte über ein Dienstkonto oder OAuth authentifizieren.

<a name="challenges-creating-timer-jobs"></a>Erstellen von Zeitgeberaufträgen Herausforderungen
------------------------------

Die größte Herausforderung Erstellen von Zeitgeberaufträgen in Office 365-Mandanten zugeordnet ist, dass die Tatsache, dass Sie die Farm bereitstellen können nicht als Lösungen zu Office 365-Instanz Bereich. Ohne eine farmlösung bezogenen kann keinen SharePoint-Zeitgeberauftrag bereitgestellt werden.

Die neue Möglichkeit zum Erstellen eines Zeitgeberauftrags ist außerhalb von SharePoint erstellt und zum Verarbeiten von außerhalb von SharePoint als auch planen. Faktoren Sie die folgenden zugeordneten SharePoint-Zeitgeberaufträgen für eine lokale SharePoint-Umgebung.

- SharePoint mit Hunderten von Out-of-Box Zeitgeberaufträge, mit denen der SharePoint-Scheduler zu struggles verwendet werden soll.  
OK-Sie können die Menge an Arbeitsspeicher und Power reduzieren erforderlich auf dem SharePoint-Server durch die Implementierung verschieben code in Azure oder einer anderen Umgebung.
- Planung und Implementierung Code für die Zeitgeberaufträge auf einen anderen Server verschieben legt den sharepointserver besser skalierbar und stabil als Ergebnis.

<a name="options-to-schedule-timer-jobs"></a>Optionen zum Planen von Zeitgeberaufträgen
----------------------------

Sie haben eine Reihe von Optionen für die Implementierung der Planung für einen Zeitgeberauftrag.

- Windows-Taskplaner
    + Windows-Dienst
- Azure WebJob
    + Azure-Arbeitsprozess

<a name="windows-scheduler"></a>Windows-Taskplaner
-----------------
In diesem Muster verarbeitet die Windows-Taskplaner die Planung Aspekte eines Zeitgeberauftrags zugeordnet.  Code zur Implementierung möglicherweise eine Konsolenanwendung oder ein PowerShell-Skript oder anderen Code, den die Windows-Taskplaner aufrufen können.

**Windows Service Sub-Option** Ein Windows-Dienst hat die gleichen Merkmale wie die Windows-Taskplaner. Microsoft empfiehlt sich nicht auf dieses Muster, aber es ist erwähnt, da sie häufig verwendet wird.

**Ist Windows-Taskplaner geeignet?**

Wenn Sie keinen Zugriff auf ein Azure-Abonnement zum Planen von Zeitgeberaufträgen mit Azure WebJobs ist mit einem Windows-Taskplaner gut geeignet, da diese Option auf allen Computern mit Windows-Betriebssystems implementiert werden kann.

- Erfordert zusätzliche Hardware zum Ausführen der Windows-Taskplaner.
- Erfordert zusätzliche Hardware, um den Timer Job Code auszuführen.

**Erste Schritte**

In den folgenden Artikeln verwenden Sie das Windows-Taskplaner Muster und bieten die Codebeispiele, um Ihnen den Einstieg erleichtern.

- [Core.SimpleTimerJob (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
    + End-to-End-Artikel zu diesem Muster mit begleitendem Video.
- [Core.TimerJobs.Samples (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + Hervorragende Codebeispiele 10 verschiedene Beispiele einschließt. *Hinweis: Nicht alle zehn Codebeispiele gelten für das Windows-Taskplaner-Muster.*

<a name="azure-webjob"></a>Azure WebJob
------------
In diesem Muster der Azure-WebJob behandelt die Planung Aspekte eines Zeitgeberauftrags zugeordnet und enthält den Code zur Implementierung.

- Keine erforderlich zusätzliche Hardware zum Ausführen der Azure-WebJob (Planung und Implementierung Code).
- Vorteilhaft, da sie für die Planung sowie den Code zur Implementierung der Azure-WebJob verwendet, erleichtert die zentral verwalten.

**Azure Worker Sub Serverrollenoption** Ein Azure-Workerrolle hat die gleichen Merkmale wie ein Azure WebJob. Microsoft empfiehlt sich nicht auf dieses Muster, aber es ist erwähnt, da sie häufig verwendet wird.

**Ist Azure WebJob geeignet?**

Wann haben Sie Zugriff auf ein Azure-Abonnement Zeitgeberaufträge mit Azure WebJobs planen.

**Erste Schritte**

Die folgenden Artikel beschreiben das Muster Azure WebJob und geben Codebeispiele, um Ihnen den Einstieg.

- [Erste Schritte mit Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365-Websites (Office 365 Plug & Play-Artikel)](https://github.com/SharePoint/PnP-Guidance/blob/master/articles/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites.md)
    + Beschreibt das Erstellen einer Azure WebJob als ein geplanter Auftrag für Ihre Office 365 verwenden, oder klicken Sie mit der lokalen SharePoint-Umgebung. Enthält veröffentlichen und Überwachungsinformationen.
- [Core.SimpleTimerJob (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + Hervorragende Codebeispiele 10 verschiedene Beispiele einschließt. *Hinweis: Nicht alle zehn Codebeispiele sind für das Muster Azure WebJob gelten.*

<a name="authentication-options"></a>Authentifizierungsoptionen
----------------------

Sie müssen in der Reihenfolge für die Zeitgeberaufträge für die Interaktion mit SharePoint authentifizieren. Zurzeit stehen zwei Muster, mit denen Sie Zeitgeberaufträge authentifizieren können.

- Verwenden eines Dienstkontos
- Verwenden von OAuth

<a name="use-a-service-account"></a>Verwenden eines Dienstkontos
---------------------
In diesem Muster definieren Sie einen oder mehrere Dienstkonten verwendet, um Zeitgeberaufträge authentifizieren.

- Dienstkonten werden in SharePoint definiert.
    + In Office 365-Instanz, je nachdem, welche Funktionalität Ihre Zeitgeberaufträge verfügen, die Dienstkonten eine Office 365-Lizenz zugewiesen werden möglicherweise.
    + Erstellen Sie Dienstkonten auf einer pro Timer-Job-Basis, oder verwenden Sie ein einzelnes Konto für alle Zeitgeberaufträge.
    + Erstellen Sie klare und beschreibende Namen für die Dienstkonten, damit Sie auf einfache Weise die Vorgänge überwachen können, die sie durchführen.
    
    Beispiel: Wenn des Zeitgeberauftrags Listenelemente geändert wird, zeigt die Spalte geändert von für Listenelemente den Namen des Dienstkontos den Zeitgeberauftrag zugeordnet.

- Bei der Authentifizierung mit Dienstkonten müssen Sie einen Benutzernamen und ein Kennwort für das Dienstkonto abrufen.
    + Der folgende Codeausschnitt veranschaulicht die Verwendung von einen Benutzernamen und ein Kennwort um zu authentifizieren.
    + Achten Sie zum Speichern und abrufen, den Benutzernamen und das Kennwort auf sichere Weise.

    ```
    using (ClientContext context = new ClientContext("https://tenancy.sharepoint.com"))
    {   
        // Use default authentication mode
        context.AuthenticationMode = ClientAuthenticationMode.Default;  
        // Specify the credentials for the account that will execute the request
        context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
    }
    ```

**Erste Schritte**

In den folgenden Artikeln wird beschrieben, wie ein Dienstkonto authentifizierungsmuster verwenden, und geben Sie Codebeispiele, um Ihnen den Einstieg erleichtern.

- [Erstellen einer SharePoint-App als eines Zeitgeberauftrags (MSDN-Blog)](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx)
    + End-to-End-Artikel zu diesem Muster.
- [Core.SimpleTimerJob (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
    + End-to-End-Artikel zu diesem Muster mit begleitendem Video.
- [Core.TimerJobs.Samples (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + Hervorragende Codebeispiele 10 verschiedene Beispiele einschließt. *Hinweis: Nicht alle zehn Codebeispiele gelten für die authentifizierungsmuster für die Service-Konto.*

<a name="use-oauth"></a>Verwenden von OAuth
-----------
In diesem Muster definieren eine Anwendung in SharePoint oder Azure Active Directory und die der Anwendung zugeordneten Authentifizierungstoken zur Authentifizierung verwenden.

- Wenn Sie eine SharePoint-Anwendung mit authentifizieren Sie Erstellen einer app principal und Berechtigungen zuweisen.
    + In diesem Muster möglicherweise Zeitgeberaufträge über eine vom Anbieter gehosteten SharePoint-Add-in oder eine Konsolenanwendung implementiert werden.
    + Verwenden Sie zum Registrieren eines app-Prinzipals für die SharePoint-Add-in vom Anbieter gehostete oder Konsolenanwendung, die AppRegNew-Seite in SharePoint.
    
    Zugriff auf diese Seite unter der folgenden URL http://<tenancy>/<site>/_layouts/AppRegNew.aspx

    + Verwenden Sie zum Erteilen von Berechtigungen zu einem app-Prinzipal der Seite AppInv in SharePoint.
    
    Zugriff auf diese Seite unter der folgenden URL http://<tenancy>/<site>/_layouts/AppInv.aspx

- Zeitgeberaufträge verwenden nur-App-Berechtigungen, da sie nicht über ein interaktiver Benutzer, der ihnen zugeordneten verfügen. 
    + Der folgende Codeausschnitt veranschaulicht ein Zugriffstoken beziehen und Verwenden von nur-App-Berechtigungen in SharePoint zu authentifizieren.

    ```
    string accessToken = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUri.Authority, realm).AccessToken;
    
    using(var clientContext = TokenHelper.GetClientContextWithAccessToken(siteUri.ToString(),accessToken))
    {
        //Implement timer job code
    }
    ```

- Bei Verwendung einer Anwendung Azure Active Directory authentifiziert, die Sie erstellen eine Azure Active Directory-Anwendung in der Azure-Verwaltungsportal und Berechtigungen zuweisen.
    + In diesem Muster möglicherweise Zeitgeberaufträge über eine vom Anbieter gehosteten SharePoint-Add-in oder eine Konsolenanwendung implementiert werden.
    + In diesem Muster interagieren Sie mit der Active Directory-Authentifizierungsbibliothek oder die Microsoft Graph-API, um ein Zugriffstoken abzurufen.
    + Das Zugriffstoken wird zur Authentifizierung in SharePoint (und möglicherweise andere Office 365-Diensten in Office 365-Instanz) verwendet.

**Erste Schritte**

Die folgenden Artikel beschreiben das Muster der OAUth-Authentifizierung und geben Codebeispiele, um Ihnen den Einstieg erleichtern.

- [Erstellen einer SharePoint-App als eines Zeitgeberauftrags (MSDN-Blog)](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx)
    + End-to-End-Artikel zu diesem Muster.
- [Core.TimerJobs.Samples (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + Hervorragende Codebeispiele 10 verschiedene Beispiele einschließt. *Hinweis: Nicht alle zehn Codebeispiele gelten für das Muster der OAUth-Authentifizierung.*

<a name="related-links"></a>Verwandte links
=============
- [Azure WebJob Ressourcen (Azure-Dokumentation)](http://azure.microsoft.com/en-us/documentation/articles/websites-webjobs-resources/)
- [Bereitstellen von WebJobs mithilfe von Visual Studio (Azure-Dokumentation)](http://azure.microsoft.com/en-us/documentation/articles/websites-dotnet-deploy-webjobs/)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [Core.SimpleTimerJob (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
- [Core.TimerJobs.Samples (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
- [Provisioning.Services.SiteManager (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Services.SiteManager)
- [Provisioning.SiteCollectionCreation (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteCollectionCreation)
- Beispiele und Inhalte am https://github.com/SharePoint/PnP

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
