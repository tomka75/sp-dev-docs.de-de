---
title: Verwenden des passenden Register-SPWorkflowService-Cmdlets
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 91fca6c2-60ca-4177-8560-2b310dac0e2c
ms.openlocfilehash: 93941c54931812e0333c2297705d5196dff164a6
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="using-the-pairing-cmdlet-register-spworkflowservice"></a>Verwenden des Kopplungs-Cmdlets Register-SPWorkflowService
Erfahren Sie, wie Sie das Cmdlet **Register-SPWorkflowService** verwenden, um SharePoint erfolgreich mit dem Workflow-Manager zu koppeln.
Wenn Sie Microsoft SharePoint installieren und für die Workflowentwicklung nutzen möchten, müssen Sie die Installationen von SharePoint und des Workflow-Managers koppeln. In den meisten Szenarien erfolgt diese Kopplung problemlos mit dem Cmdlet **Register-SPWorkflowService**, das in der SharePoint-Installation enthalten ist.
  
    
    

Wichtig: Die Verwendung dieses Cmdlets ist nicht in allen Kopplungsszenarien sinnvoll. **Register-SPWorkflowService** ist nur in den folgenden Kopplungsszenarien nützlich:
- 1-Computer-Serverfarm, bei der sich SharePoint und der Workflow-Manager auf dem gleichen Server befinden.
    
  
- 3-Computer-Serverfarm, bei der sich SharePoint und der Workflow-Manager auf allen drei Computern befinden. (Fügen Sie einen vierten Computer hinzu, wenn sich Suche auf einem separaten Computer befinden muss und der Workflow-Manager HA benötigt wird. Falls Letzteres der Fall ist, muss der Workflow-Manager HA auf allen drei Computern installiert werden.
    
  
- 3-Computer-SharePoint-Farm gekoppelt mit einer Workflow-Manager-Serverfarm, die sich nicht auf dem gleichen Server befindet.
    
  
Beachten Sie zudem, dass **Register-SPWorkflowService** die Anmeldeinformationen des aktuellen Benutzers verwendet.
## <a name="cmdlet-design"></a>Cmdlet-Entwurf





|**Detail**|**Beschreibung**|
|:-----|:-----|
|Verb  <br/> |Register  <br/> |
|Subjekt  <br/> |SPWorkflowService  <br/> |
|Beschreibung  <br/> |-Paare eine sps15short-Farm mit einer Workflow-Manager Farm aus. Sie müssen dieses Cmdlet einmal pro Farm ausführen. Bevor Sie das Cmdlet ausführen, müssen Sie im Zertifikatspeicher des Computers und SharePoint-Zertifikatspeicher Stammzertifikat der Zertifizierungsstelle installieren. Verwenden Sie hierzu das Cmdlet **New-SPTrustedRootAuthority**. (Siehe unten).<br/> |
|Ausgabetyp  <br/> |Keine.  <br/> |
|Syntax  <br/> | `Register-SPWorkflowService -SPSite <URI or GUID representing an SPSite object> -WorkflowHostUri <workflow service endpoint URL> -ScopeName <string> [-PartitionMode] [-AllowOAuthHttp] [-Force]` <br/> |
   

## <a name="cmdlet-parameters"></a>Cmdlet-Parameter



|**Parameter**|**Typ**|**Beschreibung**|
|:-----|:-----|:-----|
|SPSite          (erforderlich)  <br/> |**SPSitePipeBind** <br/> |Die URL einer Websitesammlung langfristig in der SharePoint Server-Farm, die als paarungs Endpunkt fungiert. Informationen für die Bildung wird von dieser URL abgeleitet.  <br/> |
|WorkflowHostUri          (Required)  <br/> |Zeichenfolge  <br/> |Die URL des Endpunkts Workflow-Manager für die Verbindung. Ermöglicht es dem Workflowhost URI zusammen mit der Portnummer.  <br/> |
|ScopeName  <br/> |Zeichenfolge  <br/> |Der Name, der vom Workflowdienst zum Identifizieren der kombinierte SharePoint Server Farm verwendet werden. Der Standardwert ist "SharePoint". Sie müssen nur diesen Parameter angeben, wenn Sie mehrere SharePoint-Serverfarmen zu einer Farm Workflow-Manager Kopplung möchten.  <br/> |
|PartitionMode  <br/> |SwitchParameter  <br/> |Verwenden Sie diesen Parameter nur für SharePoint-Farm mit mehreren Mandanten. Die partitionsmodus wird pro SharePoint-Dienst angegeben. Beachten Sie, dass Sie mehrmandantenfähigkeit in einer SharePoint-Farm erstellen können, nachdem dieses Cmdlet ausgeführt wird. aus diesem Grund kann nicht mit dem Cmdlet dieser Parameterwert implizit aus dem bestehenden Zustand der SharePoint-Farm abzuleiten.  <br/> |
|AllowOAuthHttp  <br/> |SwitchParameter  <br/> |Ermöglicht Exchange OAuth und Metadaten über HTTP. Dies ist nützlich, testen, aber nicht in den Produktionsmodus versetzen. Verwenden Sie diese nur, wenn SharePoint zur Unterstützung von HTTP konfiguriert ist. Es ist nicht erforderlich, dass die Workflow-Manager für die Verwendung von HTTP konfiguriert werden.  <br/> |
|Force  <br/> |SwitchParameter  <br/> |Erzwingt das Erstellen eines Bereichs mit dem Parameter _ScopeName_ oder aktualisiert einen vorhandenen Bereich, der dem gleichen _Bereichsnamen_ entspricht. Wenn der Parameter nicht angegeben wird und bereits ein Bereich mit dem gleichen Namen vorhanden ist, gibt das Cmdlet einen Fehler zurück.  <br/> |
   

## <a name="example"></a>Beispiel


```

PS> Register-SPWorkflowService -SPSite "https://myserver/mysitecollection" -WorkflowHostUri "http://workflow.example.com:12291" -ScopeName "SharePoint2" -PartitionMode -AllowOAuthHttp  -Force
```


## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  
  [Installieren und Konfigurieren von Workflows in SharePoint](http://technet.microsoft.com/de-DE/library/jj658588.aspx)
    
  
-  
  [Videoreihe: Installieren und Konfigurieren von Workflows in SharePoint](http://technet.microsoft.com/de-DE/library/dn201724.aspx)
    
  
-  
  [Workflow-Manager 1.0](http://msdn.microsoft.com/de-DE/library/jj193528%28Azure.10%29)
    
  
