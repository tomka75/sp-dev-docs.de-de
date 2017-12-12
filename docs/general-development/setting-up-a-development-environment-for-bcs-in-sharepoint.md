---
title: "Einrichten einer Entwicklungsumgebung für BCS in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d83c8a43-49dd-47eb-94d4-23aa2cf71a9a
ms.openlocfilehash: 33956da39dedd23fa5f81ce131d84e22eca9d60f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="setting-up-a-development-environment-for-bcs-in-sharepoint"></a>Einrichten einer Entwicklungsumgebung für BCS in SharePoint
Informationen Sie zum Einrichten einer Entwicklungsumgebung für die Entwicklung von Lösungen SharePoint und SharePoint-Add-Ins mit Business Connectivity Services (BCS). Sie können die SharePoint Lösungen und SharePoint-Add-Ins erstellen, mithilfe von BCS auf einem Clientcomputer oder auf einem Servercomputer, abhängig von der Art der Lösung, die Sie erstellen.
  
    
    


## <a name="building-server-based-solutions-and-sharepoint-add-ins"></a>Erstellen von Server-basierte Lösungen und SharePoint-Add-Ins
<a name="SP15SettingupdevenvBCS_server"> </a>

In der Regel wird die Mehrheit der BCS Lösungen und apps in einer Server-Umgebung gehostet werden. Diese Lösungen für Server und apps bieten die größte Maß an Flexibilität mit allen Features von BCS in SharePoint.
  
    
    
Für Server-basierte Lösungen empfiehlt es sich in der Regel die Lösung auf einem lokalen Computer zu entwickeln, auf dem SharePoint installiert ist, und dann, wenn die Lösung wird erstellt und getestet, Bereitstellen auf den Produktionsserver. Sie können eine Entwicklungsumgebung installieren, auf einer Host-Arbeitsstation oder auf einen oder mehrere virtuelle Computer, auf dem Windows Server 2008 Service Pack 2 ausgeführt werden.
  
    
    

### <a name="setting-up-an-environment-to-build-sharepoint-add-ins"></a>Einrichten einer Umgebung SharePoint-Add-Ins erstellen

Die Umgebung, die Sie verwenden, für die Entwicklung von apps mit BCS ist die gleichen wie für eine beliebige SharePoint-Add-In entwickeln. 
  
    
    
Weitere Informationen zum Installieren der Komponenten von einer Entwicklungsumgebung, einschließlich Betriebssystem, SharePoint, Visual Studio 2012 und Office Developer Tools für Visual Studio 2012, befolgen Sie die Anweisungen in  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

## <a name="building-client-based-solutions"></a>Erstellen von Client-basierte Lösungen
<a name="SP15SettingupdevenvBCS_client"> </a>

Client-basierter Lösungen aktivieren Office 2013-Clientanwendungen auf die gleichen externen Daten zugreifen, die eine SharePoint Lösung oder SharePoint-Add-In kann. Hierzu können Sie Code mithilfe von BCS-Clientcache implementieren. Die Clientkomponenten kommunizieren mit BCS über den clientseitigen Code und Clientcache. Dadurch wird die Office-Clientanwendungen mit den umfangreichen Daten, die über externe Inhaltstypen in SharePoint verfügbar sind.
  
    
    
Da diese Lösungen Code nicht erforderlich ist, können Sie SharePoint Designer 2013 und Office 2013 verwenden.
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="SP15SettingupdevenvBCS_addresources"> </a>


-  [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx)
    
  
-  [Erste Schritte mit den Business Connectivity Services in SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Übersicht über die SharePoint-Entwicklung](sharepoint-development-overview.md)
    
  

