---
title: "Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 9d84d130cc12e7784aa7b87fecd268acc1e6b7c5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="set-up-an-on-premises-development-environment-for-sharepoint-add-ins"></a><span data-ttu-id="d5d30-102">Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="d5d30-102">Set up an on-premises development environment for SharePoint Add-ins</span></span>
<span data-ttu-id="d5d30-103">Erfahren Sie, wie eine Entwicklungsumgebung einrichten, die speziell für die Entwicklung von SharePoint-Add-Ins mit einer lokalen Installation von SharePoint geeignet ist.</span><span class="sxs-lookup"><span data-stu-id="d5d30-103">Learn how to set up a development environment that is specifically suited to developing SharePoint Add-ins with an on-premises installation of SharePoint.</span></span>
 

 <span data-ttu-id="d5d30-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="d5d30-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="install-the-operating-system-for-your-development-environment-for-sharepoint-add-ins"></a><span data-ttu-id="d5d30-107">Installieren des Betriebssystems für Ihre Entwicklungsumgebung für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="d5d30-107">Install the operating system for your development environment for SharePoint Add-ins</span></span>
<span data-ttu-id="d5d30-108"><a name="bk_installOS"> </a></span><span class="sxs-lookup"><span data-stu-id="d5d30-108"><a name="bk_installOS"> </a></span></span>

<span data-ttu-id="d5d30-p102">Die Anforderungen an eine Entwicklungsumgebung sind weniger streng und kostenintensiv als die Anforderungen an eine Produktionsumgebung. Mit den hier beschriebenen Richtlinien ist die Installation einer Produktionsumgebung nicht möglich. Unter  [Übersicht über die SharePoint-Installation und -Konfiguration](http://technet.microsoft.com/en-us/library/ee667264%28v=office.15%29),  [Hardware- und Softwareanforderungen für SharePoint](http://technet.microsoft.com/en-us/library/cc262485%28v=office.15%29) und [Konfigurieren einer Umgebung für SharePoint-Add-Ins](http://technet.microsoft.com/en-us/library/fp161236%28office.15%29.aspx) finden Sie Anleitungen zum Einrichten der Installation einer Produktionsumgebung von SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p102">The requirements for a development environment are less stringent and costly than the requirements for a production environment, and the guidelines described here do not support a production environment installation. See  [Overview of SharePoint installation and configuration](http://technet.microsoft.com/en-us/library/ee667264%28v=office.15%29),  [Hardware and software requirements for SharePoint](http://technet.microsoft.com/en-us/library/cc262485%28v=office.15%29), and  [Configure an environment for SharePoint Add-ins](http://technet.microsoft.com/en-us/library/fp161236%28office.15%29.aspx) for the instructions to set up a production environment installation of SharePoint.</span></span>
 

 
<span data-ttu-id="d5d30-111">In jeder Entwicklungsumgebung sollten Sie einen Computer mit einer x64-fähigen CPU und mindestens 16 Gigabyte (GB) RAM für die Installation und Ausführung von SharePoint verwenden (24 GB RAM empfohlen).</span><span class="sxs-lookup"><span data-stu-id="d5d30-111">In any development environment, you should use a computer with an x64-capable CPU, and at least 16 GB of RAM to install and run SharePoint; 24 GB of RAM is preferable.</span></span>
 

 
<span data-ttu-id="d5d30-112">Je nach Ihren spezifischen Anforderungen und Ihrem Budget können Sie unter folgenden Optionen wählen:</span><span class="sxs-lookup"><span data-stu-id="d5d30-112">Depending on your specific requirements and budget, you can choose from the following options:</span></span>
 

 

- <span data-ttu-id="d5d30-113">Installieren von SharePoint unter Windows Server 2008 R2 Servicepack 1 x64 oder Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="d5d30-113">Install SharePoint on Windows Server 2008 R2 Service Pack 1 x64 or Windows Server 2012.</span></span>
    
 
- <span data-ttu-id="d5d30-p103">Verwenden Sie Microsoft Hyper-V, und installieren Sie SharePoint auf einem virtuellen Computer unter einem Gastbetriebssystem Windows Server 2008 R2 Service Pack 1 x64 oder Windows Server 2012. Eine Anleitung zum Einrichten eines virtuellen Microsoft Hyper-V-Computers für SharePoint finden Sie unter  [Verwenden bewährter Konfigurationsmethoden für virtuelle SharePoint-Computer und die Hyper-V-Umgebung](http://technet.microsoft.com/en-US/library/ff621103%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5d30-p103">Use Microsoft Hyper-V and install SharePoint on a virtual machine running a Windows Server 2008 R2 Service Pack 1 x64 or Windows Server 2012 guest operating system. See  [Use best practice configurations for the SharePoint virtual machines and Hyper-V environment](http://technet.microsoft.com/en-US/library/ff621103%28v=office.15%29.aspx) for guidance on setting up a Microsoft Hyper-V virtual machine for SharePoint.</span></span>
    
 

 <span data-ttu-id="d5d30-p104">**Hinweis** Die Installation von SharePoint wird nur unter Windows Server 2008 R2 Service Pack 1 x64 oder Windows Server 2012 unterstützt. Wenn Sie SharePoint-Add-Ins für SharePoint unter Windows 7 oder Windows 8 entwickeln möchten, können Sie sich für eine Office 365-Entwicklerwebsite registrieren und Add-Ins remote entwickeln.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p104">**Note**  Installation of SharePoint is supported only on Windows Server 2008 R2 Service Pack 1 x64 or Windows Server 2012. If you want to develop SharePoint Add-ins for SharePoint on Windows 7 or Windows 8, you can sign up for an Office 365 Developer Site and develop add-ins remotely.</span></span> 
 


## <a name="install-the-prerequisites-for-the-operating-system-and-sharepoint"></a><span data-ttu-id="d5d30-118">Installieren der Voraussetzungen für das Betriebssystem und SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5d30-118">Install the prerequisites for the operating system and SharePoint</span></span>
<span data-ttu-id="d5d30-119"><a name="bk_prereqsOS"> </a></span><span class="sxs-lookup"><span data-stu-id="d5d30-119"><a name="bk_prereqsOS"> </a></span></span>


1. <span data-ttu-id="d5d30-120">Führen Sie das Tool „PrerequisiteInstaller.exe“ aus, das in Ihren Installationsdateien enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="d5d30-120">Run the PrerequisiteInstaller.exe tool that is included with your installation files.</span></span>
    
 
2. <span data-ttu-id="d5d30-121">Führen Sie das in den Installationsdateien enthaltene Setup.exe-Tool aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-121">Run the Setup.exe tool that is included with your installation files.</span></span>
    
 
3. <span data-ttu-id="d5d30-122">Akzeptieren Sie die Microsoft-Software-Lizenzbedingungen.</span><span class="sxs-lookup"><span data-stu-id="d5d30-122">Accept the Microsoft Software License Terms.</span></span>
    
 
4. <span data-ttu-id="d5d30-123">Wählen Sie auf der Seite **Gewünschte Installation auswählen** die Option **Eigenständig** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-123">On the  **Choose the installation you want** page, choose **Stand-alone**.</span></span>
    
    <span data-ttu-id="d5d30-124">**Abbildung 1. Wahl des Installationstyps**</span><span class="sxs-lookup"><span data-stu-id="d5d30-124">**Figure 1. Installation type choice**</span></span>

 

  ![SharePoint-Installationsservertyp](../images/SP15_app_ServerType.gif)
 

 

 
5. <span data-ttu-id="d5d30-p105">Wenn bei der Installation Fehler auftreten, überprüfen Sie die Protokolldatei. Sie finden die Protokolldatei, indem Sie ein Eingabeaufforderungsfenster öffnen und die folgenden Befehle an der Eingabeaufforderung eingeben. Beim Abschluss der Installation wird ebenfalls ein Link zur Protokolldatei angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p105">If any errors occur in the installation, review the log file. To find the log file, open a Command Prompt window, and then type the following commands at the command prompt. A link to the log file also appears when the installation is complete.</span></span>
    
```
  cd %temp%
dir /od *.log
```

6. <span data-ttu-id="d5d30-129">Nach Abschluss der Installation werden Sie aufgefordert, den Konfigurations-Assistenten für SharePoint-Produkte und -Technologien zu starten.</span><span class="sxs-lookup"><span data-stu-id="d5d30-129">After the installation is complete, you're prompted to start the SharePoint Products and Technologies Configuration Wizard.</span></span>
    
     <span data-ttu-id="d5d30-p106">**Hinweis** Bei der Ausführung des Konfigurations-Assistenten für SharePoint-Produkte und -Technologien können Fehler auftreten, wenn Sie einen an eine Domäne angebundenen Computer verwenden, der nicht mit einem Domänencontroller verbunden ist. Bei diesem Fehler müssen Sie entweder direkt oder über eine VPN-Verbindung (Virtuelles Privates Netzwerk) eine Verbindung mit einem Domänencontroller herstellen oder sich mit einem lokalen Konto anmelden, das über Administratorrechte für den Computer verfügt.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p106">**Note**  The SharePoint Products and Technologies Configuration Wizard may fail if you're using a computer that is joined to a domain but that is not connected to a domain controller. If you see this failure, connect to a domain controller either directly or through a Virtual Private Network (VPN) connection, or sign in with a local account that has administrative privileges on the computer.</span></span>
7. <span data-ttu-id="d5d30-p107">Nach Abschluss des Konfigurations-Assistenten wird die neue Seite **Vorlagenauswahl** der neuen SharePoint-Website angezeigt. Wählen Sie auf dieser Seite die Vorlage **Entwicklerwebsite** aus. Sie können SharePoint-Add-Ins nur aus Visual Studio für eine Entwicklerwebsite bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p107">After the configuration wizard is complete, you see the  **Template Selection** page of the new SharePoint site. On this page, choose the **Developer Site** template. You can only deploy SharePoint Add-ins from Visual Studio to a Developer Site.</span></span>
    
    <span data-ttu-id="d5d30-135">**Abbildung 2: Auswählen der Websitevorlagenseite**</span><span class="sxs-lookup"><span data-stu-id="d5d30-135">**Figure 2. Choose the site template page**</span></span>

 

  ![Websitevorlagenseite](../images/SP15_appChooseSiteTemplate.gif)
 

 

 

## <a name="configure-services-in-sharepoint-for-server-to-server-add-in-use"></a><span data-ttu-id="d5d30-137">Konfigurieren von Diensten in SharePoint für die Verwendung in Server-zu-Server-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="d5d30-137">Configure services in SharePoint for server-to-server add-in use</span></span>
<span data-ttu-id="d5d30-138"><a name="Servertoserver"> </a></span><span class="sxs-lookup"><span data-stu-id="d5d30-138"><a name="Servertoserver"> </a></span></span>

<span data-ttu-id="d5d30-p108">IIn diesem Schritt konfigurieren Sie Dienste in SharePoint für die Verwendung in Server-zu-Server-Add-Ins. Mit diesen Schritten wird sichergestellt, dass Sie mit Ihrer Installation besonders vertrauenswürdige vom Anbieter gehostete Add-Ins erstellen können. Weitere Informationen zur Erstellung dieser Art von Add-In finden Sie unter  [Erstellen besonders vertrauenswürdiger Add-Ins für SharePoint](create-high-trust-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="d5d30-p108">In this step, you configure services in SharePoint for server-to-server add-in use. These steps ensure that you will be able to create high trust provider-hosted add-ins with your installation. See  [Create high-trust SharePoint Add-ins](create-high-trust-sharepoint-add-ins.md) for more information about creating this kind of add-in.</span></span>
 

 

1. <span data-ttu-id="d5d30-p109">Stellen Sie sicher, dass der App-Verwaltungsdienst und die Benutzerprofilanwendung konfiguriert sind. (Es heißt „App-Verwaltungsdienst", da SharePoint-Add-Ins ursprünglich „Apps für SharePoint" hießen). Führen Sie dazu folgende Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="d5d30-p109">Ensure that the App Management Service and user profile application are configured. (It is called "App Management Service" because SharePoint Add-ins were originally named "apps for SharePoint".) The steps are as follows:</span></span>
    
      1. <span data-ttu-id="d5d30-144">Wählen Sie in **Zentraladministration** unter **Anwendungsverwaltung** den Eintrag **Dienstanwendungen verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-144">In  **Central Administration**, under  **Application Management**, select  **Manage service applications**.</span></span>
    
 
  2. <span data-ttu-id="d5d30-145">Überzeugen Sie sich auf der Seite **Dienstanwendungen** davon, dass die folgenden Dienste gestartet wurden:</span><span class="sxs-lookup"><span data-stu-id="d5d30-145">On the  **Service Applications** page, ensure that the following services are started:</span></span>
    
      - <span data-ttu-id="d5d30-146">Benutzerprofildienst-Anwendung</span><span class="sxs-lookup"><span data-stu-id="d5d30-146">User Profile Service Application</span></span>
    
 
  - <span data-ttu-id="d5d30-147">App-Verwaltungsdienst</span><span class="sxs-lookup"><span data-stu-id="d5d30-147">App Management Service</span></span>
    
 
  3. <span data-ttu-id="d5d30-148">Wählen Sie unter **Anwendungsverwaltung** den Eintrag **Dienste auf dem Server verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-148">Under  **Application Management**, select  **Manage services on server**.</span></span> 
    
 
  4. <span data-ttu-id="d5d30-149">Stellen Sie auf der Seite **Dienste auf dem Server** sicher, dass die folgenden Dienste gestartet wurden:</span><span class="sxs-lookup"><span data-stu-id="d5d30-149">On the  **Services on Server** page, ensure that the following services are started:</span></span>
    
      - <span data-ttu-id="d5d30-150">Benutzerprofildienst</span><span class="sxs-lookup"><span data-stu-id="d5d30-150">User Profile Service</span></span> 
    
 
2. <span data-ttu-id="d5d30-p110">Stellen Sie sicher, dass mindestens ein Profil in der **Benutzerprofildienst-Anwendung** erstellt wird. Führen Sie dazu folgende Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="d5d30-p110">Ensure that at least one profile is created in the  **User Profile Service Application**. The steps are as follows:</span></span>
    
      1. <span data-ttu-id="d5d30-153">Wählen Sie in **Zentraladministration** unter **Anwendungsverwaltung** den Eintrag **Dienstanwendungen verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-153">In  **Central Administration**, under  **Application Management**, select  **Manage service applications**.</span></span>
    
 
  2. <span data-ttu-id="d5d30-154">Wählen Sie dann **Benutzerprofildienst-Anwendung** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-154">Next, select  **User Profile Service Application**.</span></span>
    
 
  3. <span data-ttu-id="d5d30-155">Wählen Sie auf der Seite **Profildienst verwalten: Benutzerprofildienst-Anwendung** unter **Personen** den Eintrag **Benutzerprofile verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-155">On the  **Manage Profile Service: User Profile Service Application** page, under **People**, select  **Manage User Profiles**.</span></span>
    
 
  4. <span data-ttu-id="d5d30-156">Wählen Sie auf der Seite **Benutzerprofile verwalten** die Option **Neue Profile** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-156">On the  **Manage User Profiles** page, select **New Profiles**.</span></span>
    
 
  5. <span data-ttu-id="d5d30-157">Geben Sie auf der Seite **Benutzerprofil hinzufügen** Ihren Kontonamen und Ihre E-Mail-Adresse ein.</span><span class="sxs-lookup"><span data-stu-id="d5d30-157">On the  **Add User Profile** page, type your account name and email address.</span></span>
    
 
  6. <span data-ttu-id="d5d30-158">Wählen Sie **Speichern und schließen** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-158">Select  **Save and Close**.</span></span>
    
     <span data-ttu-id="d5d30-159">**Hinweis** Wenn eine Meldung mit der Information angezeigt wird, dass das zu erstellende Profil bereits vorhanden ist, wählen Sie **Abbrechen und zurückgehen** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-159">**Note**  If you get a message saying that the profile you are trying to create already exists, select  **Cancel and Go Back**.</span></span>
  7. <span data-ttu-id="d5d30-160">Die Seite **Benutzerprofile verwalten**, die daraufhin wieder angezeigt wird, sollte den Eintrag **Gesamtanzahl der Profile: 1** enthalten.</span><span class="sxs-lookup"><span data-stu-id="d5d30-160">Back on the  **Manage User Profiles** page, you should see **Total number of profiles: 1**.</span></span>
    
 

## <a name="install-visual-studio-and-office-developer-tools-for-visual-studio"></a><span data-ttu-id="d5d30-161">Installieren von Visual Studio und Office Developer Tools für Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5d30-161">Install Visual Studio and Office Developer Tools for Visual Studio</span></span>
<span data-ttu-id="d5d30-162"><a name="SP15Appdevonprem_bk_installVS"> </a></span><span class="sxs-lookup"><span data-stu-id="d5d30-162"><a name="SP15Appdevonprem_bk_installVS"> </a></span></span>


- <span data-ttu-id="d5d30-p111">Wenn Sie **Visual Studio** 2013 oder höher noch nicht installiert haben, installieren Sie es mithilfe der Anweisungen unter [Install Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). Wir empfehlen die Verwendung der [aktuellsten Version aus dem Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="d5d30-p111">If you don't already have  **Visual Studio** 2013 or later installed, install it with the instructions at [Install Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). We recommend using the  [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
    
 
- <span data-ttu-id="d5d30-p112">Visual Studio umfasst **Microsoft Office Developer Tools für Visual Studio**, es gibt jedoch auch Fälle, in denen eine Version der Tools zwischen den Updates von Visual Studio veröffentlicht wird. Um sicherzustellen, dass Sie die aktuellste Version der Tools verwenden, führen Sie das [Installationsprogramm für Office Developer Tools für Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) oder das [Installationsprogramm für Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015) aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p112">Visual Studio includes the  **Microsoft Office Developer Tools for Visual Studio**, but sometimes a version of the tools is released between updates of Visual Studio. To be sure that you have the latest version of the tools use run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>
    
 

### <a name="verbose-logging-in-visual-studio"></a><span data-ttu-id="d5d30-167">Ausführliche Protokollierung in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5d30-167">Verbose logging in Visual Studio</span></span>

<span data-ttu-id="d5d30-168">Führen Sie die folgenden Schritte aus, wenn Sie die ausführliche Protokollierung aktivieren möchten:</span><span class="sxs-lookup"><span data-stu-id="d5d30-168">Follow these steps if you want to turn on verbose logging:</span></span>
 

 

1. <span data-ttu-id="d5d30-169">Öffnen Sie die Registrierung, und navigieren Sie zu **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, wobei _nn.n_ die Version von Visual Studio ist, z. B. 12.0 oder 14.0.</span><span class="sxs-lookup"><span data-stu-id="d5d30-169">Open the registry, and navigate to  **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, where _nn.n_ is the version of Visual Studio, such as 12.0 or 14.0.</span></span>
    
 
2. <span data-ttu-id="d5d30-170">Fügen Sie einen DWORD-Schlüssel mit dem Namen **EnableDiagnostics** hinzu.</span><span class="sxs-lookup"><span data-stu-id="d5d30-170">Add a DWORD key named  **EnableDiagnostics**.</span></span>
    
 
3. <span data-ttu-id="d5d30-171">Geben Sie dem Schlüssel den Wert **1**.</span><span class="sxs-lookup"><span data-stu-id="d5d30-171">Give the key the value  **1**.</span></span>
    
 
<span data-ttu-id="d5d30-172">Der Registrierungspfad wird sich in kommenden Versionen von Visual Studio ändern.</span><span class="sxs-lookup"><span data-stu-id="d5d30-172">The registry path will change in future versions of Visual Studio.</span></span>
 

 

## <a name="configure-an-isolated-add-in-domain-in-sharepoint"></a><span data-ttu-id="d5d30-173">Konfigurieren einer isolierten Add-In-Domäne in SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5d30-173">Configure an isolated add-in domain in SharePoint</span></span>
<span data-ttu-id="d5d30-174"><a name="SP15appdevonprem_bk_configure"> </a></span><span class="sxs-lookup"><span data-stu-id="d5d30-174"><a name="SP15appdevonprem_bk_configure"> </a></span></span>

<span data-ttu-id="d5d30-175">Lesen Sie zunächst [Hostwebs, Add-In-Webs und die isolierte Domäne](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain), bevor Sie Verfahren dieses Abschnitts ausführen.</span><span class="sxs-lookup"><span data-stu-id="d5d30-175">Please read  [Host webs, add-in webs, and the isolated domain](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain) before you carry out any procedures in this section.</span></span>
 

 
<span data-ttu-id="d5d30-p113">Sie müssen auf der Test-SharePoint-Farm eine isolierte Domäne erstellen. Außerdem erfordert Ihre SharePoint-Installation eine allgemeine Platzhalter-Hostheaderdomäne, auf der sie in SharePoint gehostete Add-Ins Apps bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p113">You must create an isolated domain in your test SharePoint farm. Also, your SharePoint installation needs a general wildcard host header domain where it can provision SharePoint-hosted add-ins.</span></span>
 

 
<span data-ttu-id="d5d30-p114">Für Entwicklungszwecke können Sie Ihre Hostdatei nach Bedarf ändern, um den Entwicklungscomputer zum Testen einer Instanz von SharePoint-Add-In weiterzuleiten. Visual Studio ändert Ihre Hostdatei automatisch, wenn Sie das Add-In erstellen und bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p114">For development purposes, you can modify your hosts file as you need to route your development computer to a test instance of a SharePoint Add-in. Visual Studio modifies your hosts file automatically when you build and deploy the add-in.</span></span> 
 

 

 <span data-ttu-id="d5d30-p115">**Hinweis** Für Produktionsfarmen müssen Sie eine DNS-Weiterleitungsstrategie innerhalb Ihres Intranets erstellen und die Firewall konfigurieren. Weitere Informationen zum Erstellen und Konfigurieren einer Produktionsumgebung für SharePoint-Add-Ins finden Sie unter [Installieren und Verwalten von SharePoint-Add-Ins](http://technet.microsoft.com/en-us/library/fp161232%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="d5d30-p115">**Note**  For production farms, you would have to create a DNS routing strategy within your intranet and optionally configure your firewall. See  [Install and Manage SharePoint Add-ins](http://technet.microsoft.com/en-us/library/fp161232%28v=office.15%29) for more information about how to create and configure a production environment for SharePoint Add-ins.</span></span>
 

<span data-ttu-id="d5d30-182">Führen Sie die Schritte im folgenden Verfahren aus, um eine isolierte Add-In-Domäne zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d5d30-182">Perform the steps in the following procedure to create an isolated add-in domain.</span></span>
 

 

 <span data-ttu-id="d5d30-183">**Hinweis** Führen Sie alle Schritte im folgenden Verfahren aus, während Sie als Farmadministrator angemeldet sind. Führen Sie die Eingabeaufforderung und die SharePoint-Verwaltungsshell als Administrator aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-183">**Note**  You must perform all of the steps in the following procedure while logged in as the farm administrator, and you must run the command prompt and the SharePoint Management Shell as an administrator.</span></span>
 


### <a name="create-an-isolated-add-in-domain-on-your-development-computer"></a><span data-ttu-id="d5d30-184">Erstellen einer isolierten Add-In-Domäne auf Ihrem Entwicklungscomputer</span><span class="sxs-lookup"><span data-stu-id="d5d30-184">Create an isolated add-in domain on your development computer</span></span>


1. <span data-ttu-id="d5d30-185">Stellen Sie sicher, dass der spadmin- und der sptimer-Dienst ausgeführt werden, indem Sie eine Eingabeaufforderung öffnen und die folgenden Befehle eingeben.</span><span class="sxs-lookup"><span data-stu-id="d5d30-185">Ensure that the spadmin and sptimer services are running by opening a command prompt and typing the following commands.</span></span>
    
```
  net start spadminv4
net start sptimerv4
```

2. <span data-ttu-id="d5d30-p116">Erstellen Sie die isolierte Add-In-Domäne, indem Sie die SharePoint-Verwaltungsshell als Administrator ausführen und den folgenden Befehl eingeben. Ersetzen Sie  _contosoaddins.com_ durch Ihre Add-In-Domäne. Dies sollte *keine*  Unterdomäne der Host-SharePoint-Domäne sein. Dadurch würden die Sicherheitsvorteile isolierter Add-In-Domänen weitgehend zunichte gemacht. Lautet die Hostdomäne zum Beispiel „contoso.com", sollten Sie nicht „addins.contoso.com" als Add-In-Domäne verwenden.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p116">Create your isolated add-in domain by running the SharePoint Management Shell as an administrator and typing the following command. Replace the  _contosoaddins.com_ with your add-in domain. It should *not*  be a subdomain of the host SharePoint domain. Doing so largely defeats the security advantages of having isolated add-in domains. For example, if the host domain is contoso.com, do not use addins.contoso.com as the add-in domain.</span></span>
    
```
  Set-SPAppDomain "contosoaddins.com"
```

3. <span data-ttu-id="d5d30-191">Stellen Sie sicher, dass die Dienste SPSubscriptionSettingsService und AppManagementServiceInstance ausgeführt werden, indem Sie den folgenden Befehl in der SharePoint-Verwaltungsshell eingeben.</span><span class="sxs-lookup"><span data-stu-id="d5d30-191">Ensure that the SPSubscriptionSettingsService and AppManagementServiceInstance services are running by typing the following command in the SharePoint Management Shell.</span></span>
    
```
  Get-SPServiceInstance | where{$_.GetType().Name -eq "AppManagementServiceInstance" -or $_.GetType().Name -eq "SPSubscriptionSettingsServiceInstance"} | Start-SPServiceInstance
```

4. <span data-ttu-id="d5d30-p117">Überprüfen Sie, ob die Dienste SPSubscriptionSettingsService und AppManagementServiceInstance ausgeführt werden, indem Sie den folgenden Befehl in der SharePoint-Verwaltungsshell eingeben. Die Ausgabe gibt an, ob jeder Dienst online ist.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p117">Verify that the SPSubscriptionSettingsService and AppManagementServiceInstance services are running by typing the following command in the SharePoint Management Shell. The output will indicate whether each service is online.</span></span>
    
```
  Get-SPServiceInstance | where{$_.GetType().Name -eq "AppManagementServiceInstance" -or $_.GetType().Name -eq "SPSubscriptionSettingsServiceInstance"}
```

5. <span data-ttu-id="d5d30-p118">Sie müssen ein Konto angeben, unter dem die Dienstinstanzen SPSubscriptionService und AppManagementServiceInstance ausgeführt werden sollen. Dieses Konto muss ein SPManagedAccount sein. Sie können ein SPManagedAccount erstellen, indem Sie den folgenden Befehl in der SharePoint-Verwaltungsshell eingeben. (Sie werden zur Eingabe von Kontodomäne\Benutzer und Kennwort aufgefordert.)</span><span class="sxs-lookup"><span data-stu-id="d5d30-p118">You must specify an account under which the SPSubscriptionService and AppManagementServiceInstance service instances will run. This account must be an SPManagedAccount. You can create an SPManagedAccount by typing the following command in the SharePoint Management Shell. (You'll be prompted for the account domain\user and password.)</span></span>
    
```
  $account = New-SPManagedAccount
```

6. <span data-ttu-id="d5d30-p119">Geben Sie ein Konto, einen Anwendungspool und Datenbankeinstellungen für die Dienste SPSubscriptionService und AppManagementServiceInstance an, indem Sie den folgenden Code in der SharePoint-Verwaltungsshell eingeben. Wenn Sie im vorherigen Schritt ein SPManagedAccount erstellt haben, verwenden Sie diesen Kontonamen hier.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p119">Specify an account, application pool, and database settings for the SPSubscriptionService and AppManagementServiceInstance services by typing the following code in the SharePoint Management Shell. If you created a SPManagedAccount in the preceding step, use that account name here.</span></span>
    
```
  $account = Get-SPManagedAccount "domain\user" 
$appPoolSubSvc = New-SPServiceApplicationPool -Name SettingsServiceAppPool -Account $account
$appPoolAppSvc = New-SPServiceApplicationPool -Name AppServiceAppPool -Account $account
$appSubSvc = New-SPSubscriptionSettingsServiceApplication -ApplicationPool $appPoolSubSvc -Name SettingsServiceApp -DatabaseName SettingsServiceDB 
$proxySubSvc = New-SPSubscriptionSettingsServiceApplicationProxy -ServiceApplication $appSubSvc
$appAppSvc = New-SPAppManagementServiceApplication -ApplicationPool $appPoolAppSvc -Name AppServiceApp -DatabaseName AppServiceDB
$proxyAppSvc = New-SPAppManagementServiceApplicationProxy -ServiceApplication $appAppSvc

```

7. <span data-ttu-id="d5d30-200">Geben Sie Ihr Add-In-Präfix an (siehe [Hostwebs, Add-In-Webs und die isolierte Domäne](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain)), indem Sie folgenden Code in der SharePoint-Verwaltungsshell eingeben.</span><span class="sxs-lookup"><span data-stu-id="d5d30-200">Specify your add-in prefix (see  [Host webs, add-in webs, and the isolated domain](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain)) by typing the following code in the SharePoint Management Shell.</span></span>
    
```
  Set-SPAppSiteSubscriptionName -Name "add-in" -Confirm:$false
```

 <span data-ttu-id="d5d30-p120">**Führen Sie die Schritte in der folgenden Prozedur nur durch, wenn Sie einen Proxyserver verwenden.** Nachdem Sie Ihre isolierte Add-In-Domäne erstellt haben, führen Sie die in der folgenden Prozedur beschriebenen Schritte durch, um die Domäne zu Ihrer Umgehungsliste im Internet Explorer hinzuzufügen. Dadurch wird sichergestellt, dass Sie zu dieser Domäne navigieren können, nachdem Sie ein in SharePoint gehostetes Add-In oder ein vom Anbieter gehostetes Add-In bereitgestellt haben, das ein Add-In-Web umfasst.</span><span class="sxs-lookup"><span data-stu-id="d5d30-p120">**Carry out the following procedure only if your environment uses a proxy server.** After you create your isolated add-in domain, perform the steps in the following procedure to add that domain to your bypass list in Internet Explorer. This ensures that you can navigate to this domain after you deploy a SharePoint-hosted add-in or a provider-hosted add-in that includes an add-in web.</span></span>
 

 

### <a name="add-your-isolated-add-in-domain-to-your-bypass-list-in-internet-explorer"></a><span data-ttu-id="d5d30-204">Hinzufügen der isolierten Add-In-Domäne zu Ihrer Umgehungsliste in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d5d30-204">Add your isolated add-in domain to your bypass list in Internet Explorer</span></span>


1. <span data-ttu-id="d5d30-205">Gehen Sie in Internet Explorer auf **Extras**.</span><span class="sxs-lookup"><span data-stu-id="d5d30-205">In Internet Explorer, go to  **Tools**.</span></span>
    
 
2. <span data-ttu-id="d5d30-206">Wählen Sie **Internetoptionen** aus.</span><span class="sxs-lookup"><span data-stu-id="d5d30-206">Choose  **Internet options**.</span></span>
    
 
3. <span data-ttu-id="d5d30-207">Klicken Sie auf der Registerkarte **Verbindungen** auf die Schaltfläche **LAN-Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="d5d30-207">On the  **Connections** tab, choose the **LAN Settings** button.</span></span>
    
 
4. <span data-ttu-id="d5d30-208">Deaktivieren Sie das Kontrollkästchen **Automatische Suche der Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="d5d30-208">Clear the  **Automatically detect settings** check box.</span></span>
    
 
5. <span data-ttu-id="d5d30-209">Aktivieren Sie das Kontrollkästchen **Proxyserver für LAN verwenden**.</span><span class="sxs-lookup"><span data-stu-id="d5d30-209">Select the  **Use a proxy server for your LAN** check box.</span></span>
    
 
6. <span data-ttu-id="d5d30-210">Klicken Sie auf die Schaltfläche **Erweitert**, und fügen Sie dann *.IhreAddInDomäne.com zu der Liste **Ausnahmen** hinzu.</span><span class="sxs-lookup"><span data-stu-id="d5d30-210">Choose the  **Advanced** button, and then add*.YourAddinsDomain.com to the **Exceptions** list.</span></span>
    
 
7. <span data-ttu-id="d5d30-211">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5d30-211">Choose the  **OK** button.</span></span>
    
 
8. <span data-ttu-id="d5d30-212">Klicken Sie auf **OK**, um das Dialogfeld **Einstellungen für lokales Netzwerk** zu schließen.</span><span class="sxs-lookup"><span data-stu-id="d5d30-212">Choose the  **OK** button to close the **Local Area Network (LAN) Settings** dialog box.</span></span>
    
 
9. <span data-ttu-id="d5d30-213">Klicken Sie auf **OK**, um das Dialogfeld **Internetoptionen** zu schließen.</span><span class="sxs-lookup"><span data-stu-id="d5d30-213">Choose the  **OK** button to close the **Internet Options** dialog box.</span></span>
    
 
<span data-ttu-id="d5d30-214">Unter [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) finden Sie weitere Informationen über die verfügbaren Optionen für die Bereitstellung Ihrer Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="d5d30-214">See  [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) for information about your options for deploying your add-ins.</span></span>
 

 

 <span data-ttu-id="d5d30-p121">**Tipp** Nachdem Sie in Ihrer Installation ein von SharePoint gehostetes Add-In bereitgestellt haben, werden Sie beim Starten des Add-Ins möglicherweise dazu aufgefordert, sich mit Ihren Anmeldeinformationen anzumelden. Sie müssen die Loopbackprüfung deaktivieren, um diese Aufforderungen zu vermeiden. Eine Anleitung zur Deaktivierung der Loopbackprüfung finden Sie unter [Fehler 401.1 beim Aufrufen einer Website, die integrierte Authentifizierung verwendet und mit IIS 5.1 oder einer höheren Version gehostet wird](http://support.microsoft.com/kb/896861).</span><span class="sxs-lookup"><span data-stu-id="d5d30-p121">**Tip**  After you deploy a SharePoint-hosted add-in to your installation, you may be prompted to log in with your credentials when you try to launch it. You will need to disable the loopback check to get rid of these prompts. See  [You receive error 401.1 when you browse a Web site that uses Integrated Authentication and is hosted on IIS 5.1 or a later version](http://support.microsoft.com/kb/896861) for instructions on how to disable the loopback check.</span></span>
 


## <a name="additional-resources"></a><span data-ttu-id="d5d30-218">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d5d30-218">Additional resources</span></span>
<span data-ttu-id="d5d30-219"><a name="SP15SetupSPO365_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d5d30-219"><a name="SP15SetupSPO365_bk_addlresources"> </a></span></span>


-  [<span data-ttu-id="d5d30-220">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="d5d30-220">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="d5d30-221">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="d5d30-221">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="d5d30-222">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="d5d30-222">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
 

 

 

