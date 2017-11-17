---
title: Verwenden des passenden Register-SPWorkflowService-Cmdlets
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 91fca6c2-60ca-4177-8560-2b310dac0e2c
ms.openlocfilehash: b04bb57d3583ea7fb4e8927ff867ab5ff3e2b264
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="using-the-pairing-cmdlet-register-spworkflowservice"></a><span data-ttu-id="6989c-102">Verwenden des Kopplungs-Cmdlets Register-SPWorkflowService</span><span class="sxs-lookup"><span data-stu-id="6989c-102">Using the pairing cmdlet Register-SPWorkflowService</span></span>
<span data-ttu-id="6989c-103">Erfahren Sie, wie Sie das Cmdlet **Register-SPWorkflowService** verwenden, um SharePoint erfolgreich mit dem Workflow-Manager zu koppeln.</span><span class="sxs-lookup"><span data-stu-id="6989c-103">Learn how to use the cmdlet **Register-SPWorkflowService** to successfully pair SharePoint with Workflow Manager.</span></span>
<span data-ttu-id="6989c-104">Wenn Sie Microsoft SharePoint installieren und für die Workflowentwicklung nutzen möchten, müssen Sie die Installationen von SharePoint und des Workflow-Managers koppeln.</span><span class="sxs-lookup"><span data-stu-id="6989c-104">Installing and configuring Microsoft SharePoint to support workflow development requires "pairing" your installations of SharePoint and Workflow Manager.</span></span> <span data-ttu-id="6989c-105">In den meisten Szenarien erfolgt diese Kopplung problemlos mit dem Cmdlet **Register-SPWorkflowService**, das in der SharePoint-Installation enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="6989c-105">In most scenarios, this pairing is easily done by using the cmdlet **Register-SPWorkflowService**, which is included with your SharePoint installation.</span></span>
  
    
    

<span data-ttu-id="6989c-p102">Wichtig: Die Verwendung dieses Cmdlets ist nicht in allen Kopplungsszenarien sinnvoll. **Register-SPWorkflowService** ist nur in den folgenden Kopplungsszenarien nützlich:</span><span class="sxs-lookup"><span data-stu-id="6989c-p102">Importantly, this cmdlet is not useful for every pairing scenario. **Register-SPWorkflowService** is useful only in the following pairing scenarios:</span></span>
- <span data-ttu-id="6989c-108">1-Computer-Serverfarm, bei der sich SharePoint und der Workflow-Manager auf dem gleichen Server befinden.</span><span class="sxs-lookup"><span data-stu-id="6989c-108">One-computer server farm where SharePoint Server 2013 and Workflow Manager are co-located on the server box.</span></span>
    
  
- <span data-ttu-id="6989c-109">3-Computer-Serverfarm, bei der sich SharePoint und der Workflow-Manager auf allen drei Computern befinden.</span><span class="sxs-lookup"><span data-stu-id="6989c-109">Three-computer server farm where SharePoint and Workflow Manager are co-located on all three computers.</span></span> <span data-ttu-id="6989c-110">(Fügen Sie einen vierten Computer hinzu, wenn sich Suche auf einem separaten Computer befinden muss und der Workflow-Manager HA benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="6989c-110">(Add a fourth computer is search needs to be on a separate computer and Workflow Manager HA is required.</span></span> <span data-ttu-id="6989c-111">Falls Letzteres der Fall ist, muss der Workflow-Manager HA auf allen drei Computern installiert werden.</span><span class="sxs-lookup"><span data-stu-id="6989c-111">If the latter is required, it must be installed on all three machines.</span></span>
    
  
- <span data-ttu-id="6989c-112">3-Computer-SharePoint-Farm gekoppelt mit einer Workflow-Manager-Serverfarm, die sich nicht auf dem gleichen Server befindet.</span><span class="sxs-lookup"><span data-stu-id="6989c-112">Three-computer SharePoint Server 2013 farm paired with a non-co-located Workflow Manager server farm.</span></span>
    
  
<span data-ttu-id="6989c-113">Beachten Sie zudem, dass **Register-SPWorkflowService** die Anmeldeinformationen des aktuellen Benutzers verwendet.</span><span class="sxs-lookup"><span data-stu-id="6989c-113">Also note that **Register-SPWorkflowService** uses the credentials of the current user.</span></span>
## <a name="cmdlet-design"></a><span data-ttu-id="6989c-114">Cmdlet-Entwurf</span><span class="sxs-lookup"><span data-stu-id="6989c-114">Cmdlet design</span></span>





|<span data-ttu-id="6989c-115">**Detail**</span><span class="sxs-lookup"><span data-stu-id="6989c-115">**Detail**</span></span>|<span data-ttu-id="6989c-116">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6989c-116">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6989c-117">Verb</span><span class="sxs-lookup"><span data-stu-id="6989c-117">Verb</span></span>  <br/> |<span data-ttu-id="6989c-118">Register</span><span class="sxs-lookup"><span data-stu-id="6989c-118">Register</span></span>  <br/> |
|<span data-ttu-id="6989c-119">Subjekt</span><span class="sxs-lookup"><span data-stu-id="6989c-119">Noun</span></span>  <br/> |<span data-ttu-id="6989c-120">SPWorkflowService</span><span class="sxs-lookup"><span data-stu-id="6989c-120">SPWorkflowService</span></span>  <br/> |
|<span data-ttu-id="6989c-121">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="6989c-121">Description</span></span>  <br/> |<span data-ttu-id="6989c-p104">-Paare eine sps15short-Farm mit einer Workflow-Manager Farm aus. Sie müssen dieses Cmdlet einmal pro Farm ausführen. Bevor Sie das Cmdlet ausführen, müssen Sie im Zertifikatspeicher des Computers und SharePoint-Zertifikatspeicher Stammzertifikat der Zertifizierungsstelle installieren. Verwenden Sie hierzu das Cmdlet **New-SPTrustedRootAuthority**. (Siehe unten).</span><span class="sxs-lookup"><span data-stu-id="6989c-p104">Pairs a sps15short farm with a Workflow Manager farm. You must run this cmdlet once per farm. Before running the cmdlet, you must install root CA certificate in machine certificate store and SharePoint certificate store. To do this, use the cmdlet **New-SPTrustedRootAuthority**. (See instructions below.)  </span></span><br/> |
|<span data-ttu-id="6989c-127">Ausgabetyp</span><span class="sxs-lookup"><span data-stu-id="6989c-127">Output type</span></span>  <br/> |<span data-ttu-id="6989c-128">Keine.</span><span class="sxs-lookup"><span data-stu-id="6989c-128">None.</span></span>  <br/> |
|<span data-ttu-id="6989c-129">Syntax</span><span class="sxs-lookup"><span data-stu-id="6989c-129">Syntax</span></span>  <br/> | `Register-SPWorkflowService -SPSite <URI or GUID representing an SPSite object> -WorkflowHostUri <workflow service endpoint URL> -ScopeName <string> [-PartitionMode] [-AllowOAuthHttp] [-Force]` <br/> |
   

## <a name="cmdlet-parameters"></a><span data-ttu-id="6989c-130">Cmdlet-Parameter</span><span class="sxs-lookup"><span data-stu-id="6989c-130">Cmdlet parameters</span></span>



|<span data-ttu-id="6989c-131">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="6989c-131">**Parameter**</span></span>|<span data-ttu-id="6989c-132">**Typ**</span><span class="sxs-lookup"><span data-stu-id="6989c-132">**Type**</span></span>|<span data-ttu-id="6989c-133">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="6989c-133">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6989c-134">SPSite          (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="6989c-134">SPSite          (Required)</span></span>  <br/> |<span data-ttu-id="6989c-135">**SPSitePipeBind**</span><span class="sxs-lookup"><span data-stu-id="6989c-135">**SPSitePipeBind**</span></span> <br/> |<span data-ttu-id="6989c-p105">Die URL einer Websitesammlung langfristig in der SharePoint Server-Farm, die als paarungs Endpunkt fungiert. Informationen für die Bildung wird von dieser URL abgeleitet.</span><span class="sxs-lookup"><span data-stu-id="6989c-p105">The URL of a long-lasting site collection on the SharePoint Server farm that serves as the pairing endpoint. Information for pairing is deduced from this URL.</span></span>  <br/> |
|<span data-ttu-id="6989c-138">WorkflowHostUri          (Required)</span><span class="sxs-lookup"><span data-stu-id="6989c-138">WorkflowHostUri          (Required)</span></span>  <br/> |<span data-ttu-id="6989c-139">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="6989c-139">String</span></span>  <br/> |<span data-ttu-id="6989c-p106">Die URL des Endpunkts Workflow-Manager für die Verbindung. Ermöglicht es dem Workflowhost URI zusammen mit der Portnummer.</span><span class="sxs-lookup"><span data-stu-id="6989c-p106">The URL of the Workflow Manager endpoint for the pairing. Provides the workflow host URI along with port number.</span></span>  <br/> |
|<span data-ttu-id="6989c-142">ScopeName</span><span class="sxs-lookup"><span data-stu-id="6989c-142">ScopeName</span></span>  <br/> |<span data-ttu-id="6989c-143">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="6989c-143">String</span></span>  <br/> |<span data-ttu-id="6989c-p107">Der Name, der vom Workflowdienst zum Identifizieren der kombinierte SharePoint Server Farm verwendet werden. Der Standardwert ist "SharePoint". Sie müssen nur diesen Parameter angeben, wenn Sie mehrere SharePoint-Serverfarmen zu einer Farm Workflow-Manager Kopplung möchten.</span><span class="sxs-lookup"><span data-stu-id="6989c-p107">The name to be used by the workflow service to identify the paired SharePoint Server farm. The default value is "SharePoint". You only need to specify this parameter if trying to pair multiple SharePoint farms to a Workflow Manager farm.</span></span>  <br/> |
|<span data-ttu-id="6989c-147">PartitionMode</span><span class="sxs-lookup"><span data-stu-id="6989c-147">PartitionMode</span></span>  <br/> |<span data-ttu-id="6989c-148">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="6989c-148">SwitchParameter</span></span>  <br/> |<span data-ttu-id="6989c-p108">Verwenden Sie diesen Parameter nur für SharePoint-Farm mit mehreren Mandanten. Die partitionsmodus wird pro SharePoint-Dienst angegeben. Beachten Sie, dass Sie mehrmandantenfähigkeit in einer SharePoint-Farm erstellen können, nachdem dieses Cmdlet ausgeführt wird. aus diesem Grund kann nicht mit dem Cmdlet dieser Parameterwert implizit aus dem bestehenden Zustand der SharePoint-Farm abzuleiten.</span><span class="sxs-lookup"><span data-stu-id="6989c-p108">Use this parameter only for multi-tenant SharePoint farm. The partition mode is specified per SharePoint service. Note that you can create multi-tenancy in a SharePoint farm after this cmdlet runs; therefore, the cmdlet cannot deduce this parameter value implicitly from the existing state of the SharePoint farm.</span></span>  <br/> |
|<span data-ttu-id="6989c-152">AllowOAuthHttp</span><span class="sxs-lookup"><span data-stu-id="6989c-152">AllowOAuthHttp</span></span>  <br/> |<span data-ttu-id="6989c-153">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="6989c-153">SwitchParameter</span></span>  <br/> |<span data-ttu-id="6989c-p109">Ermöglicht Exchange OAuth und Metadaten über HTTP. Dies ist nützlich, testen, aber nicht in den Produktionsmodus versetzen. Verwenden Sie diese nur, wenn SharePoint zur Unterstützung von HTTP konfiguriert ist. Es ist nicht erforderlich, dass die Workflow-Manager für die Verwendung von HTTP konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="6989c-p109">Enables OAuth and metadata exchange over HTTP. This is useful in testing, but not in production mode. Use this only when SharePoint is configured to support HTTP. It is not necessary that the Workflow Manager be configured to use HTTP.</span></span>  <br/> |
|<span data-ttu-id="6989c-158">Force</span><span class="sxs-lookup"><span data-stu-id="6989c-158">Force</span></span>  <br/> |<span data-ttu-id="6989c-159">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="6989c-159">SwitchParameter</span></span>  <br/> |<span data-ttu-id="6989c-160">Erzwingt das Erstellen eines Bereichs mit dem Parameter _ScopeName_ oder aktualisiert einen vorhandenen Bereich, der dem gleichen _Bereichsnamen_ entspricht.</span><span class="sxs-lookup"><span data-stu-id="6989c-160">Enforces the creating of scope using  _ScopeName_ parameter, or updates an existing scope corresponding to the same _ScopeName_.</span></span> <span data-ttu-id="6989c-161">Wenn der Parameter nicht angegeben wird und bereits ein Bereich mit dem gleichen Namen vorhanden ist, gibt das Cmdlet einen Fehler zurück.</span><span class="sxs-lookup"><span data-stu-id="6989c-161">If not specified and scope with the same name exists, the cmdlet will throw an error.</span></span>  <br/> |
   

## <a name="example"></a><span data-ttu-id="6989c-162">Beispiel</span><span class="sxs-lookup"><span data-stu-id="6989c-162">Example</span></span>


```

PS> Register-SPWorkflowService -SPSite "https://myserver/mysitecollection" -WorkflowHostUri "http://workflow.example.com:12291" -ScopeName "SharePoint2" -PartitionMode -AllowOAuthHttp  -Force
```


## <a name="additional-resources"></a><span data-ttu-id="6989c-163">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6989c-163">Additional resources</span></span>
<span data-ttu-id="6989c-164"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6989c-164"></span></span>


-  <span data-ttu-id="6989c-165">
  [Installieren und Konfigurieren von Workflows in SharePoint](http://technet.microsoft.com/en-us/library/jj658588.aspx)</span><span class="sxs-lookup"><span data-stu-id="6989c-165">[Install and configure workflow for SharePoint Server 2013](http://technet.microsoft.com/en-us/library/jj658588.aspx)</span></span>
    
  
-  <span data-ttu-id="6989c-166">
  [Videoreihe: Installieren und Konfigurieren von Workflows in SharePoint](http://technet.microsoft.com/en-us/library/dn201724.aspx)</span><span class="sxs-lookup"><span data-stu-id="6989c-166">[Video series: Install and configure Workflow in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/dn201724.aspx)</span></span>
    
  
-  <span data-ttu-id="6989c-167">
  [Workflow-Manager 1.0](http://msdn.microsoft.com/en-us/library/jj193528%28Azure.10%29)</span><span class="sxs-lookup"><span data-stu-id="6989c-167">[Workflow Manager 1.0](http://msdn.microsoft.com/en-us/library/jj193528%28Azure.10%29)</span></span>
    
  
