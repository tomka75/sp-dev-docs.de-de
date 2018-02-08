---
title: "Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins"
description: "Installieren Sie ein Betriebssystem sowie die erforderlichen Komponenten und konfigurieren Sie Dienste sowie eine isolierte Add-In-Domäne."
ms.date: 11/03/2017
ms.prod: sharepoint
ms.openlocfilehash: 9d5ed586e02b108ada842518f54a90df6513f1f7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="set-up-an-on-premises-development-environment-for-sharepoint-add-ins"></a>Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins

Die Anforderungen für eine Entwicklungsumgebung sind weniger strikt und nicht so kostspielig wie die Anforderungen für eine Produktionsumgebung, und die hier beschriebenen Richtlinien gelten nicht für die Installation einer Produktionsumgebung. 

Die Anweisungen zur Installation einer SharePoint-Produktionsumgebung finden Sie unter:

- [Übersicht über die SharePoint-Installation und -Konfiguration](http://technet.microsoft.com/de-DE/library/ee667264%28v=office.15%29)
- [Hardware- und Softwareanforderungen für SharePoint](http://technet.microsoft.com/de-DE/library/cc262485%28v=office.15%29)
- [Konfigurieren einer Umgebung für SharePoint-Add-Ins](http://technet.microsoft.com/de-DE/library/fp161236%28office.15%29.aspx) 

<a name="bk_installOS"> </a>
## <a name="install-the-operating-system-for-your-development-environment-for-sharepoint-add-ins"></a>Installieren des Betriebssystems für Ihre Entwicklungsumgebung für SharePoint-Add-Ins

In jeder Entwicklungsumgebung sollten Sie einen Computer mit einer x64-fähigen CPU und mindestens 16 Gigabyte (GB) RAM für die Installation und Ausführung von SharePoint verwenden (24 GB RAM empfohlen).

Je nach Ihren spezifischen Anforderungen und Ihrem Budget können Sie unter folgenden Optionen wählen:

- Installieren von SharePoint unter Windows Server 2008 R2 Servicepack 1 x64 oder Windows Server 2012.
 
- Verwenden Sie Microsoft Hyper-V und installieren Sie SharePoint auf einem virtuellen Computer mit dem Gastbetriebssystem Windows Server 2008 R2 Service Pack 1 X64 oder Windows Server 2012. Eine Anleitung zum Einrichten eines virtuellen Microsoft Hyper-V-Computers für SharePoint finden Sie unter [Anwenden bewährter Konfigurationsmethoden für virtuelle SharePoint-Computer und Hyper-V-Umgebung](http://technet.microsoft.com/de-DE/library/ff621103%28v=office.15%29.aspx). 
    
> [!NOTE]
> Die Installation von SharePoint wir nur unter Windows Server 2008 R2 Servicepack 1 x64 oder Windows Server 2012 unterstützt. Wenn Sie SharePoint-Add-Ins für SharePoint unter Windows 7 oder Windows 8 entwickeln möchten, können Sie sich für eine Office 365 Entwicklerwebsite registrieren und Add-Ins remote entwickeln. 

<a name="bk_prereqsOS"> </a>
## <a name="install-the-prerequisites-for-the-operating-system-and-sharepoint"></a>Installieren der Voraussetzungen für das Betriebssystem und SharePoint

1. Führen Sie das Tool „PrerequisiteInstaller.exe“ aus, das in Ihren Installationsdateien enthalten ist.

2. Führen Sie das in den Installationsdateien enthaltene Setup.exe-Tool aus.

3. Akzeptieren Sie die Microsoft-Software-Lizenzbedingungen.

4. Wählen Sie auf der Seite **Gewünschte Installation auswählen** die Option **Eigenständig** aus.
    
   *Abbildung 1. Wahl des Installationstyps*

   ![SharePoint-Installationsservertyp](../images/SP15_app_ServerType.gif)

5. Wenn bei der Installation Fehler auftreten, überprüfen Sie die Protokolldatei. Sie finden die Protokolldatei, indem Sie ein Eingabeaufforderungsfenster öffnen und die folgenden Befehle an der Eingabeaufforderung eingeben. Beim Abschluss der Installation wird ebenfalls ein Link zur Protokolldatei angezeigt.
    
   ```
     cd %temp%
   dir /od *.log
   ```

6. Nach Abschluss der Installation werden Sie aufgefordert, den Konfigurations-Assistenten für SharePoint-Produkte und -Technologien zu starten.
    
   > [!NOTE]
   > Der Konfigurations-Assistent für SharePoint-Produkte und -Technologien kann fehlschlagen, wenn Sie einen Computer verwenden, der zwar Mitglied einer Domäne ist, jedoch nicht an einen Domänencontroller angebunden ist. Falls dieser Fehler auftritt, müssen Sie entweder eine direkte Verbindung oder eine VPN (Virtual Private Network)-Verbindung zu einem Domänencontroller herstellen oder sich mit einem lokalen Konto anmelden, das auf dem Computer über Administratorrechte verfügt.

7. Nach Abschluss des Konfigurations-Assistenten wird die Seite **Vorlagenauswahl** der neuen SharePoint-Website angezeigt. Wählen Sie auf dieser Seite die Vorlage **Entwicklerwebsite**. Sie können SharePoint-Add-Ins aus Visual Studio nur auf einer Entwicklerwebsite bereitstellen.
    
   *Abbildung 2: Auswählen der Websitevorlagenseite*

   ![Websitevorlagenseite](../images/SP15_appChooseSiteTemplate.gif)

<a name="Servertoserver"> </a>
## <a name="configure-services-in-sharepoint-for-server-to-server-add-in-use"></a>Konfigurieren von Diensten in SharePoint für die Verwendung in Server-zu-Server-Add-Ins

In diesem Schritt konfigurieren Sie Dienste in SharePoint für die Verwendung in Server-zu-Server-Add-Ins. Mit diesen Schritten wird gewährleistet, dass Sie mit Ihrer Installation vom Anbieter gehostete Add-Ins mit hoher Vertrauensstellung erstellen können. Weitere Informationen zum Erstellen dieser Art von Add-Ins finden Sie unter [Erstellen von SharePoint-Add-Ins mit hoher Vertrauensstellung](create-high-trust-sharepoint-add-ins.md).

Stellen Sie sicher, dass der App-Verwaltungsdienst und die Benutzerprofilanwendung konfiguriert sind. (Es heißt „App-Verwaltungsdienst“, da SharePoint-Add-Ins ursprünglich „Apps für SharePoint“ hießen). Führen Sie dazu folgende Schritte aus:
    
1. Wählen Sie in **Zentraladministration** unter **Anwendungsverwaltung** den Eintrag **Dienstanwendungen verwalten** aus.
   
2. Überzeugen Sie sich auf der Seite **Dienstanwendungen** davon, dass die folgenden Dienste gestartet wurden:
   
   - Benutzerprofildienst-Anwendung
   - App-Verwaltungsdienst
    
3. Wählen Sie unter **Anwendungsverwaltung** den Eintrag **Dienstanwendungen verwalten** aus. 
   
4. Stellen Sie auf der Seite **Dienste auf dem Server** sicher, dass die folgenden Dienste gestartet wurden:
    
   - Benutzerprofildienst 

Stellen Sie sicher, dass mindestens ein Profil in der **Benutzerprofildienst-Anwendung** erstellt wird. Führen Sie dazu folgende Schritte aus:
    
1. Wählen Sie in **Zentraladministration** unter **Anwendungsverwaltung** den Eintrag **Dienstanwendungen verwalten** aus.
    
2. Wählen Sie dann **Benutzerprofildienst-Anwendung** aus.
    
3. Wählen Sie auf der Seite **Profildienst verwalten: Benutzerprofildienst-Anwendung** unter **Personen** den Eintrag **Benutzerprofile verwalten** aus.
    
4. Wählen Sie auf der Seite **Benutzerprofile verwalten** die Option **Neue Profile** aus.
    
5. Geben Sie auf der Seite **Benutzerprofil hinzufügen** Ihren Kontonamen und Ihre E-Mail-Adresse ein.
    
6. Wählen Sie **Speichern und schließen** aus.
    
   > [!NOTE]
   > Wenn eine Meldung mit der Information angezeigt wird, dass das zu erstellende Profil bereits vorhanden ist, wählen Sie **Abbrechen und zurückgehen** aus.

7. Die Seite **Benutzerprofile verwalten**, die daraufhin wieder angezeigt wird, sollte den Eintrag **Gesamtanzahl der Profile: 1** enthalten.
    

<a name="SP15Appdevonprem_bk_installVS"> </a> 
## <a name="install-visual-studio-and-office-developer-tools-for-visual-studio"></a>Installieren von Visual Studio und Office Developer Tools für Visual Studio

- Wenn Sie **Visual Studio** 2013 oder höher noch nicht installiert haben, installieren Sie es mithilfe der Anweisungen unter [Install Visual Studio](https://docs.microsoft.com/de-DE/visualstudio/install/install-visual-studio). Wir empfehlen die Verwendung der [aktuellsten Version aus dem Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).

- Visual Studio umfasst die **Microsoft Office Developer Tools für Visual Studio**, manchmal wird eine Version der Tools jedoch zwischen Updates von Visual Studio veröffentlicht. Um sicherzustellen, dass Sie über die neueste Version der Tools verfügen, führen Sie das [Installationsprogramm für Office Developer Tools für Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) oder das [Installationsprogramm für Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015) aus.

### <a name="verbose-logging-in-visual-studio"></a>Ausführliche Protokollierung in Visual Studio

Gehen Sie wie folgt vor, wenn Sie die ausführliche Protokollierung aktivieren möchten:

1. Öffnen Sie die Registrierung, und navigieren Sie zu **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**. Dabei ist _nn.n_ die Version von Visual Studio, beispielsweise 12.0 oder 14.0.

2. Fügen Sie einen DWORD-Schlüssel mit dem Namen **EnableDiagnostics** hinzu.

3. Geben Sie dem Schlüssel den Wert **1**.

In zukünftigen Versionen von Visual Studio wird ein anderer Registrierungspfad verwendet werden.

<a name="SP15appdevonprem_bk_configure"> </a>
## <a name="configure-an-isolated-add-in-domain-in-sharepoint"></a>Konfigurieren einer isolierten Add-In-Domäne in SharePoint

Bevor Sie Vorgänge dieses Abschnitts ausführen, lesen Sie zunächst [Hostwebs, Add-In-Webs und die isolierte Domäne](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain).

Sie müssen auf der Test-SharePoint-Farm eine isolierte Domäne erstellen. Außerdem erfordert Ihre SharePoint-Installation eine allgemeine Platzhalter-Hostheaderdomäne, auf der sie in SharePoint gehostete Add-Ins Apps bereitstellen.

Für Entwicklungszwecke können Sie Ihre Hostdatei nach Bedarf ändern, um den Entwicklungscomputer zum Testen einer Instanz von SharePoint-Add-In weiterzuleiten. Visual Studio ändert Ihre Hostdatei automatisch, wenn Sie das Add-In erstellen und bereitstellen. 
 
> [!NOTE]
> Für Produktionsfarmen müssen Sie eine DNS-Routingstrategie innerhalb Ihres Intranets erstellen. Optional können Sie Ihre Firewall konfigurieren. Weitere Informationen zum Erstellen und Konfigurieren einer Produktionsumgebung für SharePoint-Add-Ins finden Sie unter [Installieren und Verwalten von SharePoint-Add-Ins](http://technet.microsoft.com/de-DE/library/fp161232%28v=office.15%29).

Führen Sie die Schritte im folgenden Verfahren aus, um eine isolierte Add-In-Domäne zu erstellen.
 
> [!NOTE]
> Führen Sie alle Schritte im folgenden Verfahren aus, während Sie als Farmadministrator angemeldet sind. Führen Sie die Eingabeaufforderung und die SharePoint-Verwaltungsshell als Administrator aus.

### <a name="create-an-isolated-add-in-domain-on-your-development-computer"></a>Erstellen einer isolierten Add-In-Domäne auf Ihrem Entwicklungscomputer

1. Stellen Sie sicher, dass der spadmin- und der sptimer-Dienst ausgeführt werden, indem Sie eine Eingabeaufforderung öffnen und die folgenden Befehle eingeben.
    
    ```
      net start spadminv4
      net start sptimerv4
    ```

2. Erstellen Sie die isolierte Add-In-Domäne, indem Sie die SharePoint-Verwaltungsshell als Administrator ausführen und den folgenden Befehl eingeben.

   Ersetzen Sie _contosoaddins.com_ durch Ihre Add-In-Domäne. Es sollte sich dabei *nicht* um eine Unterdomäne der Host-SharePoint-Domäne handeln. Wenn Sie dennoch eine solche Unterdomäne verwenden, werden die Sicherheitsvorteile von isolierten Add-In-Domänen größtenteils zunichte gemacht. Wenn die Hostdomäne z. B. "contoso.com" ist, verwenden Sie nicht addins.contoso.com als Add-In-Domäne.
    
    ```
      Set-SPAppDomain "contosoaddins.com"
    ```

3. Stellen Sie sicher, dass die Dienste SPSubscriptionSettingsService und AppManagementServiceInstance ausgeführt werden, indem Sie den folgenden Befehl in die SharePoint-Verwaltungsshell eingeben.
    
    ```
      Get-SPServiceInstance | where{$_.GetType().Name -eq "AppManagementServiceInstance" -or $_.GetType().Name -eq "SPSubscriptionSettingsServiceInstance"} | Start-SPServiceInstance
    ```

4. Überprüfen Sie, dass die Dienste SPSubscriptionSettingsService und AppManagementServiceInstance ausgeführt werden, indem Sie den folgenden Befehl in die SharePoint-Verwaltungsshell eingeben. Die Ausgabe zeigt an, ob alle Dienste online sind.
    
    ```
      Get-SPServiceInstance | where{$_.GetType().Name -eq "AppManagementServiceInstance" -or $_.GetType().Name -eq "SPSubscriptionSettingsServiceInstance"}
    ```

5. Sie müssen ein Konto angeben, unter dem die Dienstinstanzen SPSubscriptionService und AppManagementServiceInstance ausgeführt werden. Dieses Konto muss ein SPManagedAccount sein. Sie können ein SPManagedAccount erstellen, indem Sie den folgenden Befehl in die SharePoint-Verwaltungsshell eingeben (Sie werden zur Eingabe der Kontodomäne/des Kontobenutzers und des Kennworts aufgefordert):
    
    ```
      $account = New-SPManagedAccount
    ```

6. Geben Sie ein Konto, einen Anwendungspool und Datenbankeinstellungen für die Dienste SPSubscriptionService und AppManagementServiceInstance an, indem Sie den folgenden Code in der SharePoint-Verwaltungsshell eingeben. Wenn Sie im vorherigen Schritt ein SPManagedAccount erstellt haben, verwenden Sie diesen Kontonamen hier.
    
    ```
     $account = Get-SPManagedAccount "domain\user" 
     $appPoolSubSvc = New-SPServiceApplicationPool -Name SettingsServiceAppPool -Account $account
     $appPoolAppSvc = New-SPServiceApplicationPool -Name AppServiceAppPool -Account $account
     $appSubSvc = New-SPSubscriptionSettingsServiceApplication -ApplicationPool $appPoolSubSvc -Name SettingsServiceApp -DatabaseName SettingsServiceDB 
     $proxySubSvc = New-SPSubscriptionSettingsServiceApplicationProxy -ServiceApplication $appSubSvc
     $appAppSvc = New-SPAppManagementServiceApplication -ApplicationPool $appPoolAppSvc -Name AppServiceApp -DatabaseName AppServiceDB
     $proxyAppSvc = New-SPAppManagementServiceApplicationProxy -ServiceApplication $appAppSvc

    ```

7. Geben Sie Ihr Add-In-Präfix an (siehe [Hostwebs, Add-In-Webs und die isolierte Domäne](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain)), indem Sie folgenden Code in die SharePoint-Verwaltungsshell eingeben.
    
    ```
      Set-SPAppSiteSubscriptionName -Name "add-in" -Confirm:$false
    ```

**Führen Sie die Schritte in der folgenden Prozedur nur durch, wenn Sie einen Proxyserver verwenden.** Nachdem Sie Ihre isolierte Add-In-Domäne erstellt haben, führen Sie die in der folgenden Prozedur beschriebenen Schritte durch, um die Domäne zu Ihrer Umgehungsliste im Internet Explorer hinzuzufügen. Dadurch wird sichergestellt, dass Sie zu dieser Domäne navigieren können, nachdem Sie ein in SharePoint gehostetes Add-In oder ein vom Anbieter gehostetes Add-In bereitgestellt haben, das ein Add-In-Web umfasst.

### <a name="add-your-isolated-add-in-domain-to-your-bypass-list-in-internet-explorer"></a>Hinzufügen der isolierten Add-In-Domäne zu Ihrer Umgehungsliste in Internet Explorer

1. Gehen Sie im Internet Explorer auf **Extras**.

2. Wählen Sie **Internetoptionen** aus.

3. Wählen Sie auf der Registerkarte **Verbindungen** die Schaltfläche **LAN-Einstellungen** aus.

4. Deaktivieren Sie das Kontrollkästchen **Automatische Suche der Einstellungen**.

5. Aktivieren Sie das Kontrollkästchen **Proxyserver für LAN verwenden**.

6. Wählen Sie die Schaltfläche **Erweitert** aus, und fügen Sie dann \*.YourAddInDomain.com zu der Liste **Ausnahmen** hinzu.

7. Wählen Sie **OK** aus.

8. Wählen Sie **OK** aus, um das Dialogfeld **Einstellungen für lokales Netzwerk** zu schließen.

9. Wählen Sie **OK** aus, um das Dialogfeld **Internetoptionen** zu schließen.
    
Weitere Informationen über die verfügbaren Optionen für die Bereitstellung Ihrer Add-Ins finden Sie unter [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md).
 
> [!TIP]
> Nachdem Sie eine von SharePoint gehostete Add-In in Ihrer Installation bereitgestellt haben, werden Sie möglicherweise beim Start der Add-In aufgefordert, sich mit Ihren Anmeldeinformationen anzumelden. Sie müssen die Loopbacküberprüfung deaktivieren, um diese Aufforderungen auszuschalten. Informationen zum Deaktivieren der Loopbacküberprüfung finden Sie unter [ Anzeige des Fehlers 401.1 beim Durchsuchen einer Website, die die integrierte Authentifizierung verwendet und mit IIS 5.1 oder einer höheren Version gehostet wird](http://support.microsoft.com/kb/896861).
 

## <a name="see-also"></a>Siehe auch
<a name="SP15SetupSPO365_bk_addlresources"> </a>

- [SharePoint-Add-Ins](sharepoint-add-ins.md)
- [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md)
- [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
- [Installieren älterer Versionen von Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx)
- [Visual Studio-Dokumentation](https://docs.microsoft.com/de-DE/visualstudio/)    
 
