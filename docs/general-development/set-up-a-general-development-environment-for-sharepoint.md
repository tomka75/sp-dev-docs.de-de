---
title: "Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint"
ms.date: 09/25/2017
keywords: Installieren von SharePoint, Einrichten von SharePoint, SharePoint einrichten
f1_keywords: install SharePoint,set up SharePoint,setup SharePoint
ms.prod: sharepoint
ms.assetid: 08e4e4e1-d960-43fa-85df-f3c279ed6927
ms.openlocfilehash: 657d7f9a3a7238e8b3d9862e6ba637ccebdb3f79
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="set-up-a-general-development-environment-for-sharepoint"></a>Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint
Hier finden Sie Informationen zu den Schritten zur Einrichtung einer SharePoint-Entwicklungsumgebung, indem Sie SharePoint und Visual Studio installieren.
## <a name="how-to-determine-the-sharepoint-development-environment-you-need"></a>Ermitteln der benötigten SharePoint-Umgebung
<a name="SP15_bk_determinedevenv"> </a>

Entscheiden Sie zuerst, welche Art von Lösungen Sie erstellen möchten (weitere Informationen zu SharePoint-Add-Ins finden Sie unter  [SharePoint-Add-Ins]((http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx))):
  
    
    

- Wenn Sie Farmlösungen erstellen möchten, finden Sie in diesem Artikel die entsprechenden Schritte. 
    
  
- Wenn Sie SharePoint-Add-Ins erstellen möchten, finden Sie weitere Informationen unter  [Tools und Umgebungen für die Entwicklung von Add-Ins für SharePoint]((http://msdn.microsoft.com/library/6906eb86-8270-4098-8106-1e8d0d3c212e%28Office.15%29.aspx)). 
    
  

## <a name="create-a-sharepoint-development-environment-on-a-microsoft-azure-virtual-machine"></a>Erstellen einer SharePoint-Entwicklungsumgebung auf einem virtuellen Microsoft Azure-Computer
<a name="SP15_bk_devenvazure"> </a>

Wenn Sie über ein MSDN-Abonnement verfügen, können Sie schnell einen virtuellen Computer in Azure bereitstellen.
  
    
    
Wenn Sie den Microsoft Azure-Vorteil, der mit Ihrem MSDN-Abonnement verbunden ist, nicht aktiviert haben, können Sie sich unter  [Microsoft Azure-Vorteil für MSDN-Abonnenten]((http://azure.microsoft.com/de-DE/pricing/member-offers/msdn-benefits/)) darüber informieren.
  
> [!NOTE]
> Im Microsoft Azure-Image-Katalog werden keine Images mehr bereitgestellt, in denen SharePoint und Visual Studio bereits vorinstalliert sind. Ein virtueller Computer in Microsoft Azure ist aber dennoch eine gute Option für einen Entwicklungscomputer. > Melden Sie sich beim [Microsoft Azure-Verwaltungsportal]((https://manage.windowsazure.com)) an. > Erstellen Sie einen virtuellen Computer mithilfe eines der Images aus dem Katalog (Windows Server 2008 R2 Service Pack 1 x64, Windows Server 2012 oder höher). Befolgen Sie die Anweisungen im Assistenten für die Erstellung virtueller Computer. Für SharePoint-Entwicklungsprojekte empfehlen wir die VM-Größe **Sehr groß**. > Sobald der virtuelle Computer bereitgestellt wurde und ausgeführt wird, können Sie die Einrichtung abschließen. Befolgen Sie dazu die Anleitung im Abschnitt **Erstellen einer lokalen SharePoint-Entwicklungsumgebung** weiter unten. (Überspringen Sie den Abschnitt zum Thema Betriebssysteminstallation.) > Nachdem Sie Ihre Entwicklungsumgebung eingerichtet haben, können Sie auf dem virtuellen Computer in Visual Studio über eine Azure-Point-to-Site-Verbindung auf Ihre Quellcodeverwaltung zugreifen. Eine Anleitung finden Sie in unserem Artikel zum Thema [Konfigurieren einer Point-to-Site-VPN-Verbindung zu einem virtuellen Azure-Netzwerk]((https://azure.microsoft.com/de-DE/documentation/articles/vpn-gateway-point-to-site-create/)).
  
    
    


## <a name="create-a-sharepoint-development-environment-on-premises"></a>Erstellen einer lokalen SharePoint-Entwicklungsumgebung
<a name="SP15_bk_devenvazure"> </a>


  
    
    

### <a name="install-the-operating-system-for-your-sharepoint-add-ins-development-environment"></a>Installieren des Betriebssystems für Ihre SharePoint-Add-Ins-Entwicklungsumgebung
<a name="SP15_bk_InstallOS"> </a>

Die Anforderungen für eine Entwicklungsumgebung für eine SharePoint-Installation sind weniger stringent und kostengünstiger als die Anforderungen für eine Produktionsumgebung. In einer Entwicklungsumgebung sollten Sie einen Computer mit einer x64-fähigen CPU, und mindestens 16 GB RAM, um SharePoint zu installieren und auszuführen; 24 GB RAM sind empfehlenswert. Je nach Anforderungen und Budget können Sie aus den folgenden Optionen wählen:
  
    
    

- Installieren Sie SharePoint unter Windows Server 2008 R2 Service Pack 1 x64 oder Windows Server 2012 (oder höher).
    
  
- Verwenden Sie Microsoft Hyper-V, und installieren Sie SharePoint auf einem virtuellen Computer unter einem Gastbetriebssystem Windows Server 2008 R2 Service Pack 1 x64 oder Windows Server 2012. Eine Anleitung zum Einrichten eines virtuellen Microsoft Hyper-V-Computers für SharePoint finden Sie unter  [Verwenden bewährter Konfigurationsmethoden für virtuelle SharePoint-Computer und die Hyper-V-Umgebung](http://technet.microsoft.com/en-US/library/ff621103%28v=office.15%29.aspx).
    
  

### <a name="install-the-app-development-prerequisites-for-the-operating-system-and-sharepoint"></a>Installieren der Voraussetzungen zur App-Entwicklung für das Betriebssystem und SharePoint
<a name="SP15_bk_prereqsOS"> </a>

Für SharePoint müssen auf Ihrem Betriebssystem als Voraussetzung bestimmte Komponenten installiert sein, bevor die Installation beginnt. Aus diesem Grund enthält SharePoint das PrerequisiteInstaller.exe-Tool, das alle vorausgesetzten Komponenten für Sie installiert. Führen Sie dieses Tool aus, bevor Sie das Setup.exe-Tool ausführen.
  
    
    

1. Führen Sie das PrerequisiteInstaller.exe-Tool aus.
    
  
2. Führen Sie das in den Installationsdateien enthaltene Setup.exe-Tool aus.
    
  
3. Akzeptieren Sie die Microsoft-Software-Lizenzbedingungen.
    
  
4. Wählen Sie auf der Seite **Gewünschte Installation auswählen** die Option **Eigenständig** aus.
    
   **Abbildung 2. Wahl des Installationstyps**

  

  ![SharePoint-Installationsservertyp](../images/SP15_app_ServerType.gif)
  

  

  
5. Wenn bei der Installation Fehler auftreten, überprüfen Sie die Protokolldatei. Sie finden die Protokolldatei, indem Sie ein Eingabeaufforderungsfenster öffnen und die folgenden Befehle an der Eingabeaufforderung eingeben. Beim Abschluss der Installation wird ebenfalls ein Link zur Protokolldatei angezeigt.
    
```
  
cd %temp
dir /od *.log
```

6. Nach Abschluss der Installation werden Sie aufgefordert, den Konfigurations-Assistenten für SharePoint-Produkte und -Technologien zu starten.
    
    > [!NOTE]
    > Der Konfigurations-Assistent für SharePoint-Produkte und -Technologien kann fehlschlagen, wenn Sie einen Computer verwenden, der Mitglied einer Domäne ist, aber mit keinem Domänencontroller verbunden ist. Wenn dieser Fehler auftritt, stellen Sie entweder direkt oder über ein VPN (Virtual Private Network) eine Verbindung zu einem Domänencontroller her, oder melden Sie sich mit einem lokalen Konto an, das auf dem Computer über Administratorrechte verfügt. 

7. Nach Abschluss des Konfigurations-Assistenten wird die Seite **Vorlagenauswahl** der neuen SharePoint-Website angezeigt.
    
   **Abbildung 3: Auswählen der Websitevorlagenseite**

  

  ![SharePoint-Websitevorlagen](../images/SP15_app_ChooseSiteTemplates.gif)
  

  

  

### <a name="install-visual-studio"></a>Installieren von Visual Studio
<a name="SP15_bk_installVS"> </a>

Wenn Sie Visual Studio installieren, erhalten Sie alle Vorlagen, Tools und Assemblys, um SharePoint auf Ihrem lokalen Entwicklungscomputer zu entwickeln.
  
    
    
Unter  [Installieren von Visual Studio]((http://msdn.microsoft.com/de-DE/library/e2h7fzkw.aspx)) finden Sie Anleitungen zum Installieren von Visual Studio.
  
    
    

#### <a name="verbose-logging-in-visual-studio"></a>Ausführliche Protokollierung in Visual Studio

Führen Sie die folgenden Schritte aus, wenn Sie die ausführliche Protokollierung aktivieren möchten:
  
    
    

1. Öffnen Sie die Registrierung und navigieren Sie zu **HKEY_CURRENT_USER\\Software\\Microsoft\\VisualStudio\\ _nn.n_\\SharePointTools**, dabei steht _nn.n_ für die Version von Visual Studio, z. B. 12.0 oder 14.0.
    
  
2. Fügen Sie einen DWORD-Schlüssel mit dem Namen **EnableDiagnostics** hinzu.
    
  
3. Geben Sie dem Schlüssel den Wert **1**.
    
  
Der Registrierungspfad wird sich in kommenden Versionen von Visual Studio ändern.
  
    
    

## <a name="next-steps"></a>Nächste Schritte
<a name="SP15_bk_devenvazure"> </a>

Wenn Sie Workflows erstellen, fahren Sie mit  [Einrichten und Konfigurieren von SharePoint-Workflow-Manager](set-up-and-configure-sharepoint-workflow-manager.md).
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="SP15_bk_AddlResources"> </a>


-  
  [Installieren von Visual Studio](http://msdn.microsoft.com/en-us/library/e2h7fzkw%28v=vs.110%29.aspx)
    
  
-  [Tools und Umgebungen für die Entwicklung von Add-Ins für SharePoint]((http://msdn.microsoft.com/library/6906eb86-8270-4098-8106-1e8d0d3c212e%28Office.15%29.aspx))
    
  

  
    
    

