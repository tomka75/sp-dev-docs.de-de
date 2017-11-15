---
title: Vorgehensweise Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 87ee28e6-8170-4dba-8c9d-f04ab9e632dc
ms.openlocfilehash: 20d1cfd4d8056c3b38405b3e14f4351eb3454322
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using-vss"></a><span data-ttu-id="72e4e-102">Vorgehensweise: Sichern und Wiederherstellen eine Suchdienstanwendung in SharePoint mit VSS</span><span class="sxs-lookup"><span data-stu-id="72e4e-102">How to: Back up and restore a search service application in SharePoint using VSS</span></span>
 <span data-ttu-id="72e4e-103">**Zusammenfassung:** Informationen Sie zum Sichern und Wiederherstellen einer Suchdienstanwendung in SharePoint mithilfe der Gruppenrichtlinien-Verwaltungskonsole (Volume Shadow Copy Service, VSS).</span><span class="sxs-lookup"><span data-stu-id="72e4e-103">**Summary:** Learn how to back up and restore a search service application in SharePoint by using the Volume Shadow Copy Service (VSS).</span></span>
## <a name="prerequisites-for-backing-up-and-restoring-sharepoint-with-the-volume-shadow-copy-service"></a><span data-ttu-id="72e4e-104">Voraussetzungen für das Sichern und Wiederherstellen von SharePoint mit den Volumeschattenkopie-Dienst</span><span class="sxs-lookup"><span data-stu-id="72e4e-104">Prerequisites for backing up and restoring SharePoint with the Volume Shadow Copy Service</span></span>

<span data-ttu-id="72e4e-105">Um eine Sicherung und Wiederherstellung-Lösung für SharePoint, müssen Sie verstehen, wie VSS funktioniert und mit der SharePoint-Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="72e4e-105">To program a backup and restore solution for SharePoint, you need to understand how VSS works and the SharePoint interface with it.</span></span>
  
    
    

<span data-ttu-id="72e4e-106">**In Tabelle 1. Kernkonzepte für das Sichern und Wiederherstellen von SharePoint mit den Volumeschattenkopie-Dienst**</span><span class="sxs-lookup"><span data-stu-id="72e4e-106">**Table 1. Core concepts for backing up and restoring SharePoint with the Volume Shadow Copy Service**</span></span>


|<span data-ttu-id="72e4e-107">**Artikel**</span><span class="sxs-lookup"><span data-stu-id="72e4e-107">**Article**</span></span>|<span data-ttu-id="72e4e-108">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="72e4e-108">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="72e4e-109">
  [Volumeschattenkopie-Dienst](http://msdn.microsoft.com/en-us/library/windows/desktop/bb968832%28v=vs.85%29.aspx) und seine untergeordneten Artikel.</span><span class="sxs-lookup"><span data-stu-id="72e4e-109">[Volume Shadow Copy Service](http://msdn.microsoft.com/en-us/library/windows/desktop/bb968832%28v=vs.85%29.aspx) and its child articles.</span></span> <br/> |<span data-ttu-id="72e4e-110">Informationen Sie zu den VSS und zum Programmieren dafür.</span><span class="sxs-lookup"><span data-stu-id="72e4e-110">Learn about the VSS and how to program for it.</span></span>  <br/> |
| <span data-ttu-id="72e4e-111">[SharePoint Foundation und der Volumeschattenkopie-Dienst](http://msdn.microsoft.com/library/adae101a-078e-40b9-9cfa-db2cfb10270a%28Office.15%29.aspx) und seine untergeordneten Artikel.</span><span class="sxs-lookup"><span data-stu-id="72e4e-111">[Windows SharePoint Services and the Volume Shadow Copy Service](http://msdn.microsoft.com/library/adae101a-078e-40b9-9cfa-db2cfb10270a%28Office.15%29.aspx) and its child articles.</span></span> <br/> |<span data-ttu-id="72e4e-112">Allgemeine Informationen und Vorgehensweisen schrittweise Verfahren zum Sichern und Wiederherstellen von SharePoint Daten mit der VSS und der SharePoint-Benutzeroberfläche mit VSS an.</span><span class="sxs-lookup"><span data-stu-id="72e4e-112">Overview information and step-by-step, how-to procedures for backing up and restoring SharePoint data using the VSS and the SharePoint interface with VSS.</span></span>  <br/> |
   

## <a name="use-the-volume-shadow-copy-service-to-back-up-and-restore-a-search-service-application"></a><span data-ttu-id="72e4e-113">Verwenden Sie den Volumeschattenkopie-Dienst zum Sichern und Wiederherstellen einer Suchdienstanwendung</span><span class="sxs-lookup"><span data-stu-id="72e4e-113">Use the Volume Shadow Copy Service to back up and restore a search service application</span></span>
<span data-ttu-id="72e4e-114"><a name="Use"> </a></span><span class="sxs-lookup"><span data-stu-id="72e4e-114"></span></span>

<span data-ttu-id="72e4e-p101">Die folgenden Verfahren dienen zur Unterstützung der Entwickler Erstellen einer Sichern/Wiederherstellen der Anwendung, die die VSS verwendet Wenn Sie die IT-Experten finden Anweisungen zum Sichern oder Wiederherstellen einer Suchdienstanwendung SharePoint haben, finden Sie unter  [Sichern und Wiederherstellen von SharePoint](http://technet.microsoft.com/en-us/library/ee662536.aspx).</span><span class="sxs-lookup"><span data-stu-id="72e4e-p101">The following procedures are intended to help developers with creating a backup/restore application that uses the VSS. If you are an IT professional looking for instructions for how to back up or restore a SharePoint search service application, see  [Backup and restore SharePoint](http://technet.microsoft.com/en-us/library/ee662536.aspx).</span></span> 
  
    
    
 <span data-ttu-id="72e4e-p102">**Erforderliche:** Herunterladen und Installieren von [Microsoft Windows SDK für Windows 7 und .NET Framework 4](http://www.microsoft.com/en-us/download/details.aspx?id=8279) mit dem Server mit der Suchdienstanwendung (SSA) und auf jedem Server mit einer Suchkomponente Index. Unter anderem wird dies `C:\\Program Files\\Microsoft SDKs\\Windows\\v7.1\\Bin\\x64\\vsstools`vshadow.exe und betest.exe installieren.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p102">**Prerequisite:** Download and install [Microsoft Windows SDK for Windows 7 and .NET Framework 4](http://www.microsoft.com/en-us/download/details.aspx?id=8279) to the server with the search service application (SSA) and to every server with a search index component. Among other things, this will install vshadow.exe and betest.exe to `C:\\Program Files\\Microsoft SDKs\\Windows\\v7.1\\Bin\\x64\\vsstools`.</span></span>
  
    
    

> <span data-ttu-id="72e4e-119">
>   **Tipp:** Ausführliche Informationen zu den in diesem Artikel erwähnten Windows PowerShell-Cmdlets finden Sie unter  [Windows PowerShell für SharePoint (Referenz)](http://technet.microsoft.com/en-us/library/ee890108.aspx).</span><span class="sxs-lookup"><span data-stu-id="72e4e-119">**TIP** For details about the Windows PowerShell cmdlets mentioned in this article, see  [Windows PowerShell for SharePoint reference](http://technet.microsoft.com/en-us/library/ee890108.aspx).</span></span> 
  
    
    


### <a name="to-register-the-sharepoint-vss-writer-and-prepare-the-servers-for-backing-up-and-restoring"></a><span data-ttu-id="72e4e-120">So registrieren Sie den SharePoint VSS Writer und bereiten die Server für das Sichern und Wiederherstellen vor</span><span class="sxs-lookup"><span data-stu-id="72e4e-120">To register the SharePoint VSS Writer and prepare the servers for backing up and restoring</span></span>


- <span data-ttu-id="72e4e-121">Registrieren Sie die SharePoint-VSS-Writer mit beiden Methoden:</span><span class="sxs-lookup"><span data-stu-id="72e4e-121">Register the SharePoint VSS Writer with either of these methods:</span></span>
    
  - <span data-ttu-id="72e4e-122">Öffnen Sie **Dienste** in **Verwaltung**, und starten Sie den **SharePoint VSS Writer**-Dienst.</span><span class="sxs-lookup"><span data-stu-id="72e4e-122">Open **Services** in **Administrative Tools** and start the **SharePoint VSS Writer** service.</span></span>
    
  
  - <span data-ttu-id="72e4e-p103">Öffnen Sie eine Befehlskonsole und führen Sie  `stsadm.exe -o registerwsswriter` aus. Dienstprogramm Stsadm befindet sich im %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ BIN. Stellen Sie sicher, dass der Dienst **Dienste** in **Verwaltung** ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p103">Open a command console and execute  `stsadm.exe -o registerwsswriter`. The stsadm utility is found in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\BIN. Verify that the service is running in **Services** in **Administrative Tools**.</span></span>
    
  

### <a name="to-back-up-a-sharepoint-search-service-application-using-vss"></a><span data-ttu-id="72e4e-126">So sichern Sie eine SharePoint-Suchdienstanwendung mit VSS</span><span class="sxs-lookup"><span data-stu-id="72e4e-126">To back up a SharePoint search service application using VSS</span></span>


1. <span data-ttu-id="72e4e-p104">Rufen Sie VSS-Metadaten  `vshadow.exe -wm > writers.txt` an der Befehlszeile ausführen, auf jedem Server, die eine Indexkomponente enthält und auch auf dem Computer, auf der SQL Server ausgeführt wird, wo sich die Suchdatenbanken befinden. Die erstellte Datei writers.txt enthält alle VSS Writer-Server zugeordnet. Verwenden Sie diese Datei in den nächsten Schritten, um Manifestdateien für die Suchdienstanwendung (SSA) und den Suchindex zu generieren.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p104">Get VSS metadata by executing  `vshadow.exe -wm > writers.txt` at a command line on each server that contains an index component and also on the computer that is running SQL Server where the search databases are located. The writers.txt file that is created lists all VSS writers associated with the server. You use this file in the next steps to generate manifest files for the search service application (SSA) and search index.</span></span>
    
  
2. <span data-ttu-id="72e4e-130">Führen Sie diese Schritte zum Erstellen eines Manifests für die SSA auf dem Computer, auf dem SQL Server ausgeführt wird, wo sich die Suchdatenbanken befinden.</span><span class="sxs-lookup"><span data-stu-id="72e4e-130">Follow these steps to create a manifest for the SSA on the computer that is running SQL Server where the search databases are located.</span></span>
    
1. <span data-ttu-id="72e4e-131">Erstellen Sie eine XML-Datei, und fügen Sie die folgenden:</span><span class="sxs-lookup"><span data-stu-id="72e4e-131">Create an XML file and copy the following into it:</span></span> 
    
```XML
  
<BETest>
  <Writer writerid="SharePoint Services Writer ID">
    <Component logicalPath="PathSSA" componentName="SearchAppOffice" />
    <Component logicalPath="PathC" componentName="SearchAppOffice_CrawlStore" />
    <Component logicalPath="PathA" componentName="SearchAppOffice_AnalyticsReportingStore" />
    <Component logicalPath="PathL" componentName="SearchAppOffice_LinksStore" />
  </Writer>
  <Writer writerid="SQL Server Writer ID">
    <Component logicalPath="PathDbSSA" componentName="SearchAppOffice" />
    <Component logicalPath="PathDbC" componentName="SearchAppOffice_CrawlStore" />
    <Component logicalPath="PathDbA" componentName="SearchAppOffice_AnalyticsReportingStore" />
    <Component logicalPath="PathDbL" componentName="SearchAppOffice_LinksStore" />
  </Writer>
</BETest>

```

2. <span data-ttu-id="72e4e-p105">Ersetzen Sie die 10 Platzhalter in der Datei durch die entsprechenden Werte aus der writer.txt-Datei, die Sie im ersten Schritt generiert. Anhand der folgenden Tabelle als Leitfaden.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p105">Replace the 10 placeholders in this file with appropriate values from the writer.txt file that you generated in the first step. Use the following table as a guide.</span></span> 
    
    > <span data-ttu-id="72e4e-134">**Hinweis:** In der rechten Spalte ist  _SSA_ selbst ein Platzhalter für den Namen der Suchdienstanwendung.</span><span class="sxs-lookup"><span data-stu-id="72e4e-134">**Note** In the right-hand column,  _SSA_ is itself a placeholder for the name of the Search Service Application.</span></span>

   <span data-ttu-id="72e4e-135">**Tabelle 2. Platzhalter für SSA-Manifestdatei und Werte aus „writers.txt“**</span><span class="sxs-lookup"><span data-stu-id="72e4e-135">**Table 2. SSA manifest file placeholders and values from writers.txt**</span></span>


|<span data-ttu-id="72e4e-136">**Platzhalter**</span><span class="sxs-lookup"><span data-stu-id="72e4e-136">**Placeholder**</span></span>|<span data-ttu-id="72e4e-137">**Wo befindet sich die Informationen im writers.txt.**</span><span class="sxs-lookup"><span data-stu-id="72e4e-137">**Where the information is located in writers.txt.**</span></span>|
|:-----|:-----|
| <span data-ttu-id="72e4e-138">_SharePoint Services Writer ID_</span><span class="sxs-lookup"><span data-stu-id="72e4e-138">_SharePoint Services Writer ID_</span></span> <br/> |<span data-ttu-id="72e4e-139">Die WriterId-GUID angezeigt, unter dem Eintrag "SharePoint Services-Writer"</span><span class="sxs-lookup"><span data-stu-id="72e4e-139">The WriterId GUID listed under the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-140">_PathSSA_</span><span class="sxs-lookup"><span data-stu-id="72e4e-140">_PathSSA_</span></span> <br/> |<span data-ttu-id="72e4e-141">Der logische Path-Eintrag mit dem Namen der Suchdienstanwendung in den Eintrag "SharePoint Services-Writer" aufgeführt</span><span class="sxs-lookup"><span data-stu-id="72e4e-141">The logical path entry listed with the name of the Search Service Application in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-142">_PathC_</span><span class="sxs-lookup"><span data-stu-id="72e4e-142">_PathC_</span></span> <br/> |<span data-ttu-id="72e4e-143">Der logische Path-Eintrag aufgelistet, für die Komponente mit dem Namen" _SSA__CrawlStore" im "SharePoint Services-Writer"-Eintrag</span><span class="sxs-lookup"><span data-stu-id="72e4e-143">The logical path entry listed for the component named " _SSA__CrawlStore" in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-144">_PathA_</span><span class="sxs-lookup"><span data-stu-id="72e4e-144">_PathA_</span></span> <br/> |<span data-ttu-id="72e4e-145">Der logische Path-Eintrag aufgelistet, für die Komponente mit dem Namen" _SSA_ _AnalyticsReportingStore" im "SharePoint Services-Writer"-Eintrag</span><span class="sxs-lookup"><span data-stu-id="72e4e-145">The logical path entry listed for the component named " _SSA_ _AnalyticsReportingStore" in the "SharePoint Services Writer" entry</span></span> <br/> |
| <span data-ttu-id="72e4e-146">_PathL_</span><span class="sxs-lookup"><span data-stu-id="72e4e-146">_PathL_</span></span> <br/> |<span data-ttu-id="72e4e-147">Der logische Path-Eintrag aufgelistet, für die Komponente mit dem Namen" _SSA__LinksStore" im "SharePoint Services-Writer"-Eintrag</span><span class="sxs-lookup"><span data-stu-id="72e4e-147">The logical path entry listed for the component named " _SSA__LinksStore" in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-148">_SQL Server Writer ID_</span><span class="sxs-lookup"><span data-stu-id="72e4e-148">_SQL Server Writer ID_</span></span> <br/> |<span data-ttu-id="72e4e-149">Die WriterId-GUID angezeigt, unter dem Eintrag "SqlServerWriter"</span><span class="sxs-lookup"><span data-stu-id="72e4e-149">The WriterId GUID listed under the "SqlServerWriter" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-150">_PathDbSSA_</span><span class="sxs-lookup"><span data-stu-id="72e4e-150">_PathDbSSA_</span></span> <br/> |<span data-ttu-id="72e4e-151">Der logische Path-Eintrag für die Komponente mit dem Namen der Suchdienstanwendung in der Eintrag "SqlServerWriter" aufgeführt</span><span class="sxs-lookup"><span data-stu-id="72e4e-151">The logical path entry listed for the component with the name of the Search Service Application in the "SqlServerWriter" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-152">_PathDbC_</span><span class="sxs-lookup"><span data-stu-id="72e4e-152">_PathDbC_</span></span> <br/> |<span data-ttu-id="72e4e-153">Der logische Path-Eintrag für die Komponente mit dem Namen" _SSA__CrawlStore" in den Eintrag "SqlServerWriter" aufgeführt</span><span class="sxs-lookup"><span data-stu-id="72e4e-153">The logical path entry listed for the component named " _SSA__CrawlStore" in the "SqlServerWriter" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-154">_PathDbA_</span><span class="sxs-lookup"><span data-stu-id="72e4e-154">_PathDbA_</span></span> <br/> |<span data-ttu-id="72e4e-155">Der logische Path-Eintrag für die Komponente mit dem Namen" _SSA__AnalyticsReportingStore" in den Eintrag "SqlServerWriter" aufgeführt</span><span class="sxs-lookup"><span data-stu-id="72e4e-155">The logical path entry listed for the component named " _SSA__AnalyticsReportingStore" in the "SqlServerWriter" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-156">_PathDbL_</span><span class="sxs-lookup"><span data-stu-id="72e4e-156">_PathDbL_</span></span> <br/> |<span data-ttu-id="72e4e-157">Der logische Path-Eintrag für die Komponente mit dem Namen" _SSA__LinksStore" in den Eintrag "SqlServerWriter" aufgeführt</span><span class="sxs-lookup"><span data-stu-id="72e4e-157">The logical path entry listed for the component named " _SSA__LinksStore" in the "SqlServerWriter" entry</span></span>  <br/> |
   

    This is the SSA manifest file. For an example of a completed SSA manifest file, see  [Example manifest files](#Examples).
    
  
3. <span data-ttu-id="72e4e-p106">Befolgen Sie diese Schritte zum Erstellen eines Manifests für die Suche Indexdateien. Wiederholen Sie diese Schritte auf jedem Server, der eine Indexkomponente hat.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p106">Follow these steps to create a manifest for the search index files. Repeat these steps on every server that has an index component.</span></span>
    
1. <span data-ttu-id="72e4e-160">Erstellen Sie eine XML-Datei, und fügen Sie die folgenden:</span><span class="sxs-lookup"><span data-stu-id="72e4e-160">Create an XML file and copy the following into it:</span></span>
    
```XML
  
<BETest>
   <Writer writerid="SharePoint Services Writer ID">
      <Component logicalPath="PathIndex" componentName="NameIndex" />
   </Writer>
   <Writer writerid="OSearch15 Writer ID">
      <Component logicalPath="PathOSearch15" componentName="IndexComponentGroup" />
   </Writer>    
</BETest>
```

2. <span data-ttu-id="72e4e-p107">Ersetzen Sie die sechs Platzhalter in der Datei durch die entsprechenden Werte aus der writer.txt-Datei, die Sie im ersten Schritt generiert. Anhand der folgenden Tabelle als Leitfaden.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p107">Replace the six placeholders in this file with appropriate values from the writer.txt file that you generated in the first step. Use the following table as a guide.</span></span>
    
   <span data-ttu-id="72e4e-163">**Tabelle 3. Search Index Manifestdatei Platzhalter und Werten aus writer.txt**</span><span class="sxs-lookup"><span data-stu-id="72e4e-163">**Table 3. Search index manifest file placeholders and values from writer.txt**</span></span>


|<span data-ttu-id="72e4e-164">**Platzhalter**</span><span class="sxs-lookup"><span data-stu-id="72e4e-164">**Placeholder**</span></span>|<span data-ttu-id="72e4e-165">**Wo die Informationen im writers.txt befindet**</span><span class="sxs-lookup"><span data-stu-id="72e4e-165">**Where the information is located in writers.txt**</span></span>|
|:-----|:-----|
| <span data-ttu-id="72e4e-166">_SharePoint Services Writer ID_</span><span class="sxs-lookup"><span data-stu-id="72e4e-166">_SharePoint Services Writer ID_</span></span> <br/> |<span data-ttu-id="72e4e-167">Die WriterId-GUID angezeigt, unter dem Eintrag "SharePoint Services-Writer"</span><span class="sxs-lookup"><span data-stu-id="72e4e-167">The WriterId GUID listed under the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-168">_PathIndex_</span><span class="sxs-lookup"><span data-stu-id="72e4e-168">_PathIndex_</span></span> <br/> |<span data-ttu-id="72e4e-169">Der logische Path-Eintrag aufgelistet, die für die Komponente, deren Namen mit "IndexComponentGroup" in den Eintrag "SharePoint Services-Writer" beginnt</span><span class="sxs-lookup"><span data-stu-id="72e4e-169">The logical path entry listed for the component whose name starts with "IndexComponentGroup" in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-170">_NameIndex_</span><span class="sxs-lookup"><span data-stu-id="72e4e-170">_NameIndex_</span></span> <br/> |<span data-ttu-id="72e4e-171">Den Eintrag aufgeführt, die für die Komponente, deren Namen mit "IndexComponentGroup" in den Eintrag "SharePoint Services-Writer" beginnt</span><span class="sxs-lookup"><span data-stu-id="72e4e-171">The name entry listed for the component whose name starts with "IndexComponentGroup" in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-172">_OSearch15 Writer ID_</span><span class="sxs-lookup"><span data-stu-id="72e4e-172">_OSearch15 Writer ID_</span></span> <br/> |<span data-ttu-id="72e4e-173">Die WriterId-GUID angezeigt, unter dem Eintrag "OSearch15 VSS Writer"</span><span class="sxs-lookup"><span data-stu-id="72e4e-173">The WriterId GUID listed under the "OSearch15 VSS Writer" entry</span></span>  <br/> |
| <span data-ttu-id="72e4e-174">_PathOSearch15_</span><span class="sxs-lookup"><span data-stu-id="72e4e-174">_PathOSearch15_</span></span> <br/> |<span data-ttu-id="72e4e-p108">Der logische Path-Eintrag aufgelistet, die für die Komponente, deren Namen mit "IndexComponentGroup" in den Eintrag "OSearch15 VSS Writer" beginnt. Es ist normalerweise leer.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p108">The logical path entry listed for the component whose name starts with "IndexComponentGroup" in the "OSearch15 VSS Writer" entry. It is normally empty.</span></span>  <br/> |
| <span data-ttu-id="72e4e-177">_IndexComponentGroup_</span><span class="sxs-lookup"><span data-stu-id="72e4e-177">_IndexComponentGroup_</span></span> <br/> |<span data-ttu-id="72e4e-178">Den Eintrag aufgeführt, die für die Komponente, deren Namen mit "IndexComponentGroup" in den Eintrag "OSearch15 VSS Writer" beginnt</span><span class="sxs-lookup"><span data-stu-id="72e4e-178">The name entry listed for the component whose name starts with "IndexComponentGroup" in the "OSearch15 VSS Writer" entry</span></span>  <br/> |
   

    This is the search index manifest file. For an example of a completed search index manifest file, see  [Example manifest files](#Examples).
    
  
4. <span data-ttu-id="72e4e-p109">(Optional) Notieren Sie die Größe der **IndexComponent** Ordner auf jedem Server, die eine Indexkomponente enthält. Sie können diese Informationen später so überprüfen Sie die Sicherung verwenden.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p109">(Optional) Record the sizes of **IndexComponent** folders on each server that contains an index component. You can use this information later to verify the backup.</span></span>
    
  
5. <span data-ttu-id="72e4e-p110">Öffnen Sie bei jedem Server in der Farm die SharePoint-Verwaltungsshell, und führen Sie die folgenden Zeilen, wobei  _name of search service application_ die SSA ist, die Sie sichern möchten. Lassen Sie das Fenster SharePoint-Verwaltungsshell geöffnet danach.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p110">On any server in the farm, open the SharePoint Management Shell and execute the following lines, where  _name of search service application_ is the SSA that you want to back up. Leave the SharePoint Management Shell window open afterward.</span></span>
    
```
  
$ssa = Get-SpenterpriseSearchServiceApplication -Identity "name of search service application"
Suspend-SPEnterpriseSearchServiceApplication -Identity $ssa
```

6. <span data-ttu-id="72e4e-183">Führen Sie Sicherungen der SSA Datenbanken und der Index folgende Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="72e4e-183">Perform backups of the SSA databases and the index by following these steps:</span></span>
    
1. <span data-ttu-id="72e4e-184">Führen Sie auf dem Server mit den Datenbanken SSA den folgenden Befehl an der Befehlszeile aus, wobei  _destination backup folder_ ist der vollständige Pfad des Ordners für die Sicherungsdateien, _backup log file_ ist der vollständige Pfad und Namen der Protokolldatei der Sicherung und _SSA manifest file_ ist der Pfad und Dateiname der Manifestdatei SSA.</span><span class="sxs-lookup"><span data-stu-id="72e4e-184">On the server with the SSA databases, execute the following command at a command line, where  _destination backup folder_ is the full path of the folder for the backup files, _backup log file_ is the full path and name of the backup log file, and _SSA manifest file_ is the path and file name of the SSA manifest file.</span></span>
    
```
  
betest.exe /v /b /d "destination backup folder" /s "backup log file" /x "SSA manifest file"
```

2. <span data-ttu-id="72e4e-p111">Führen Sie auf dem Server mit dem open SharePoint-Verwaltungsshell-Fenster die folgende Zeile, wobei  _topology file name_ den vollständigen Pfad und Namen der exportierten Datei, die die Topologieinformationen enthält. Sie verwenden diese Datei in der Wiederherstellungsvorgang für die SSA.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p111">On the server with the open SharePoint Management Shell window, execute the following line, where  _topology file name_ is the full path and name of the exported file containing the topology information. You will use this file in the restore procedure for the SSA.</span></span>
    
```
  Export-SPEnterpriseSearchTopology -SearchApplication $ssa -Filename "topology file name"
```

3. <span data-ttu-id="72e4e-187">Stellen Sie sicher, dass die Datei erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="72e4e-187">Verify that the file is created.</span></span>
    
  
4. <span data-ttu-id="72e4e-188">Führen Sie auf jedem Server, der eine Indexkomponente verfügt folgenden Befehl an der Befehlszeile aus, wobei  _destination backup folder_ ist der vollständige Pfad des Ordners für die Sicherungsdateien, _backup log file_ ist der vollständige Pfad und Namen der Protokolldatei der Sicherung und _index manifest file_ ist der Pfad und Dateiname des Manifests Index.</span><span class="sxs-lookup"><span data-stu-id="72e4e-188">On each server that has an index component, execute the following at a command line, where  _destination backup folder_ is the full path of the folder for the backup files, _backup log file_ is the full path and name of the backup log file, and _index manifest file_ is the path and file name of the index manifest.</span></span>
    
```
  betest.exe /v /b /d "destination backup folder" /s "backup log file" /x "index manifest file"
```

5. <span data-ttu-id="72e4e-p112">(Optional) Prüfen Sie die Index-Ordner, die gesichert wurde. Stellen Sie sicher, dass Ordnernamen und Größen mit den im vorherigen Schritt aufgezeichnet werden soll.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p112">(Optional) Inspect the index folders that have been backed up. Verify that folder names and sizes match with those recorded in the earlier step.</span></span>
    
  

### <a name="to-restore-a-sharepoint-search-service-application-using-vss"></a><span data-ttu-id="72e4e-191">Wiederherstellen eine SharePoint-Suchdienstanwendung mit VSS</span><span class="sxs-lookup"><span data-stu-id="72e4e-191">To restore a SharePoint search service application using VSS</span></span>


1. <span data-ttu-id="72e4e-p113">Öffnen Sie bei jedem Server in der Farm die SharePoint-Verwaltungsshell, und führen Sie die folgenden Zeilen, um die vorhandene Suchdienstanwendung und Stellvertreter, wobei  _name of search service application_ die SSA aus, die Sie wiederherstellen möchten und _name of proxy_ ist seine Anwendungsproxy zu entfernen. Hinweis: Diese _name of SSA proxy_ normalerweise identisch mit den Namen der SSA mit dem Wort "Proxy" Ende hinzugefügten ist. Die Option `RemoveData` wird sichergestellt, dass die Suchdatenbanken entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p113">On any server in the farm, open the SharePoint Management Shell and execute the following lines to remove the existing search service application and its proxy, where  _name of search service application_ is the SSA that you want to restore and _name of proxy_ is its application proxy. Note that _name of SSA proxy_ is normally the same as the name of the SSA with the word "Proxy" added to the end. The `RemoveData` switch ensures that the search databases are removed.</span></span>
    
```
  $ssa = Get-SPEnterpriseSearchServiceApplication -Identity "name of search service application"
Remove-SPEnterpriseSearchServiceApplication -Identity $ssa -RemoveData
Remove-SPEnterpriseSearchServiceApplicationProxy -Identity "name of SSA proxy"
```

2. <span data-ttu-id="72e4e-195">Führen Sie auf dem gleichen Server Folgendes an der Befehlszeile zum Wiederherstellen der Datenbanken SSA where  _destination backup folder_ ist der vollständige Pfad des Ordners für die Sicherungsdateien, _backup log file_ ist der vollständige Pfad und Namen der Protokolldatei der Sicherung und _SSA manifest file_ ist der Pfad und Dateiname der Manifestdatei SSA.</span><span class="sxs-lookup"><span data-stu-id="72e4e-195">On the same server, execute the following at a command line to restore the SSA databases, where  _destination backup folder_ is the full path of the folder for the backup files, _backup log file_ is the full path and name of the backup log file, and _SSA manifest file_ is the path and file name of the SSA manifest file.</span></span>
    
```
  
betest.exe /v /r /d "destination backup folder" /s "backup log file" /x SSA_manifest_file
```

3. <span data-ttu-id="72e4e-196">Öffnen Sie auf dem gleichen Server ein SharePoint-Verwaltungsshell, und führen Sie die folgenden Zeilen, um die SSA wiederherzustellen, wobei  _application pool name_ ist der Name des neuen Pools, _domain\\user_ ist der Domänenname des Benutzers, der der zu verwendenden Anwendungspool als von in der Ereignisprotokollen, _name of the search service application_ ist der Name der SSA und _topology_file_name_ ist der Pfad und Name der Aufschlüsselung-Datei, die Sie erstellt haben, wenn die SSA gesichert wurde.</span><span class="sxs-lookup"><span data-stu-id="72e4e-196">On the same server, open a SharePoint Management Shell and execute the following lines to restore the SSA, where  _application pool name_ is the name of the new pool, _domain\\user_ is the domain name of the user that the application pool logs in as, _name of the search service application_ is the name of the SSA, and _topology_file_name_ is the path and name of the typology file you created when the SSA was backed up.</span></span>
    
    > <span data-ttu-id="72e4e-197">**Tipp:** Dieser Code erstellt eine neue Anwendungspoolidentität für die Ausführung der wiederhergestellten SSA. Sie können aber auch ein vorhandenes Konto mit dem Cmdlet **Get-SPServiceApplicationPool** verwenden.</span><span class="sxs-lookup"><span data-stu-id="72e4e-197">**TIP** This code creates a new application pool identity to run the restored SSA, but you can also use an existing account with the **Get-SPServiceApplicationPool** cmdlet.</span></span>

```
  $applicationPool = New-SPServiceApplicationPool -name "application pool name" -account "domain\\user"
Restore-SPEnterpriseSearchServiceApplication -Name "name of the search service application" -ApplicationPool $applicationPool -TopologyFile "topology_file_name" -KeepId
```

4. <span data-ttu-id="72e4e-p114">Erstellen Sie einen Proxy für die SSA mit den folgenden Cmdlets. Es wird empfohlen, dass Sie die gleichen Werte für  _name of the search service application_ und _name of SSA proxy_ verwenden, wie Sie in Schritt 1 verwendet.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p114">Create a proxy for the SSA with the following cmdlets. We recommend that you use the same values for  _name of the search service application_ and _name of SSA proxy_ as you used in step 1.</span></span>
    
```
  
$ssa = Get-SpenterpriseSearchServiceApplication -Identity "name of search service application"
New-SPEnterpriseSearchServiceApplicationProxy -Name "name of SSA proxy" -SearchApplication $ssa
```

5. <span data-ttu-id="72e4e-p115">(Optional) Stellen Sie sicher, dass die SSA und dessen Proxy vorhanden sind, indem **Zentraladministration** öffnen. Wählen Sie **Dienstanwendungen verwalten**, und stellen Sie sicher, dass die SSA und dessen Proxy aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p115">(Optional) Verify that the SSA and its proxy exist by opening **Central Administration**. Choose **Manage Service Applications** and verify that the SSA and its proxy are listed.</span></span>
    
  
6. <span data-ttu-id="72e4e-p116">(Optional) Klicken Sie auf die SSA in der Liste der Dienste, und klicken Sie dann auf der Seite, die geöffnet wird, überprüfen Sie, ob die **Suchtopologie**-Tabelle der Aufschlüsselung gesucht, die Sie in den Sicherungsvorgang exportiert haben. (Sie können auch die Topologie mit dem Cmdlet **Get-SPEnterpriseSearchStatus**überprüfen.)</span><span class="sxs-lookup"><span data-stu-id="72e4e-p116">(Optional) Click the SSA on the list of services, and then, on the page that opens, verify that the **Search Application Topology** table matches the typology that you exported in the backup procedure. (You can also verify the topology with the cmdlet **Get-SPEnterpriseSearchStatus**.)</span></span>
    
  
7. <span data-ttu-id="72e4e-204">Stellen Sie die Indexdateien mit dem folgenden Verfahren **auf allen Servern mit indexkomponenten** wieder her.</span><span class="sxs-lookup"><span data-stu-id="72e4e-204">Restore the index files with the following procedure **on all servers with index components**.</span></span>
    
1. <span data-ttu-id="72e4e-205">Beenden Sie den Hostcontroller service entweder in **Verwaltung > Dienste**, oder indem Sie das folgende Cmdlet in SharePoint-Verwaltungsshell ausführen:</span><span class="sxs-lookup"><span data-stu-id="72e4e-205">Stop the Host Controller service either in **Administrative Tools > Services**, or by executing the following cmdlet in SharePoint Management Shell:</span></span>
    
```
  
stop-service SPSearchHostController
```

2. <span data-ttu-id="72e4e-206">Führen Sie auf den gleichen Servern folgenden Befehl an der Befehlszeile aus, wobei  _index manifest file_ der Pfad und Dateiname des Manifests Index ist, die Sie in den Sicherungsvorgang erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="72e4e-206">On the same servers, execute the following at a command line, where  _index manifest file_ is the path and file name of the index manifest that you created in the backup procedure.</span></span>
    
```
  betest.exe /v /r /d "destination backup folder" /s "backup log file" /x "index manifest file"
```

3. <span data-ttu-id="72e4e-207">(Optional) Stellen Sie sicher, dass die Ordnernamen und Größen übereinstimmen, die Sie in den Sicherungsvorgang aufgezeichnet.</span><span class="sxs-lookup"><span data-stu-id="72e4e-207">(Optional) Verify that the folder names and sizes match those that you recorded in the backup procedure.</span></span>
    
  
4. <span data-ttu-id="72e4e-208">Benennen Sie für jede Indexkomponente Daten unter den Datenordner, indem Sie folgende Schritte:</span><span class="sxs-lookup"><span data-stu-id="72e4e-208">For every index component, rename data under the data folder by following these steps:</span></span>
    
1. <span data-ttu-id="72e4e-209">Führen Sie das folgende Cmdlet in SharePoint-Verwaltungsshell.</span><span class="sxs-lookup"><span data-stu-id="72e4e-209">In SharePoint Management Shell, execute the following cmdlet.</span></span>
    
```
  Get-SPEnterpriseSearchVssDataPath
```

2. <span data-ttu-id="72e4e-p117">Tragen Sie anhand der Ausgabe des Cmdlets den letzten Teil der einzelnen GUID. Beispielsweise ist eine Zeile der Ausgabe  `IndexComponentGroup_e255918b-6ab0-4d7c-8049-720b2744c62f`, zeichnen Sie 720b2744c62f auf.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p117">From the output of the cmdlet, record the last part of each GUID. For example, if one line of the output is  `IndexComponentGroup_e255918b-6ab0-4d7c-8049-720b2744c62f`, record 720b2744c62f.</span></span>
    
  
3. <span data-ttu-id="72e4e-212">Navigieren Sie zu  `C:\\Program Files\\Microsoft Office Servers\\15.0\\Data\\Office Server\\Applications\\Search\\Nodes\\24488A\\IndexComponentN\\storage\\data`, wobei  *N*  die Anzahl der eine Indexkomponente ist, im **Datei-Explorer** (oder **Windows-Explorer** unter Windows Server 2008).</span><span class="sxs-lookup"><span data-stu-id="72e4e-212">In **File Explorer** (or **Windows Explorer** on Windows Server 2008), navigate to `C:\\Program Files\\Microsoft Office Servers\\15.0\\Data\\Office Server\\Applications\\Search\\Nodes\\24488A\\IndexComponentN\\storage\\data`, where  *N*  is the number of an index component.</span></span>
    
  
4. <span data-ttu-id="72e4e-p118">Jeder dieser Ordner ist einen Unterordner, deren Namen mit "SP", gefolgt von 12 hex-Ziffern, gefolgt von einer Version Zahl beginnt. Benennen Sie für jede der folgenden Unterordner, bei denen die 12 hex-Ziffern eines der Endung GUID übereinstimmen, die Sie im vorherigen Schritt notiert haben den Unterordner in Importindex. Im als fortlaufendes Beispiel würden Sie die Unterordner  `SP720b2744c62f.1.I.1.0` inImportindexumbenennen.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p118">Each of these folders has a subfolder whose name begins with "SP" followed by 12 hex digits followed by a version number. For each of these subfolders where the 12 hex digits match one of the GUID endings that you recorded in the earlier step, rename the subfolder to importindex. In the continuing example, you would rename the subfolder  `SP720b2744c62f.1.I.1.0` toimportindex.</span></span>
    
  
5. <span data-ttu-id="72e4e-216">Neustart der Hostcontroller service entweder in **Verwaltung > Dienste**, oder indem Sie das folgende Cmdlet in SharePoint-Verwaltungsshell ausführen:</span><span class="sxs-lookup"><span data-stu-id="72e4e-216">Restart the host controller service either in **Administrative Tools > Services**, or by executing the following cmdlet in SharePoint Management Shell:</span></span>
    
```
  start-service SPSearchHostController
```

6. <span data-ttu-id="72e4e-p119">Stellen Sie sicher, dass die Index Daten Ordnernamen wieder auf den vorherigen Namen wiederhergestellt haben. (In der als fortlaufendes Beispiel wäre "" SP720b2744c62f.1.I.1.0 ".)</span><span class="sxs-lookup"><span data-stu-id="72e4e-p119">Verify that the index data folder names have reverted back to their previous name. (In the continuing example, this would be "'SP720b2744c62f.1.I.1.0".)</span></span>
    
  
8. <span data-ttu-id="72e4e-219">(Optional) Stellen Sie sicher, dass die Größe der **IndexComponent** Ordner die Größen entsprechen, die Sie in den Sicherungsvorgang notiert haben.</span><span class="sxs-lookup"><span data-stu-id="72e4e-219">(Optional) Verify that the sizes of **IndexComponent** folders match the sizes you recorded in the backup procedure.</span></span>
    
  
9. <span data-ttu-id="72e4e-220">Starten Sie die SSA neu.</span><span class="sxs-lookup"><span data-stu-id="72e4e-220">Restart the SSA.</span></span>
    
  
10. <span data-ttu-id="72e4e-221">Führen Sie das folgende Cmdlet in SharePoint-Verwaltungsshell, um sicherzustellen, dass der Suchdienst für die Anwendung ordnungsgemäß ausgeführt wird, auf den betroffenen Servern:</span><span class="sxs-lookup"><span data-stu-id="72e4e-221">On all the affected servers, run the following cmdlet in SharePoint Management Shell to verify that the search application service is running properly:</span></span>
    
```
  Get-SPEnterpriseSearchStatus
```

11. <span data-ttu-id="72e4e-p120">Stellen Sie sicher, dass Zuführung und für neue Dokumente durchsuchen funktioniert. Überprüfen Sie die Größe des Indexes beispielsweise mithilfe der Abfrage "Größe > = 0". Außerdem ein neues Dokument hinzufügen, und stellen Sie sicher, dass es durchsuchbar ist.</span><span class="sxs-lookup"><span data-stu-id="72e4e-p120">Verify that feeding and searching for new documents works. For example, check the size of the index by using the query "size>=0". Also add a new document and verify that it is searchable.</span></span>
    
  

## <a name="example-manifest-files"></a><span data-ttu-id="72e4e-225">Beispiel-Manifestdateien</span><span class="sxs-lookup"><span data-stu-id="72e4e-225">Example manifest files</span></span>
<span data-ttu-id="72e4e-226"><a name="Examples"> </a></span><span class="sxs-lookup"><span data-stu-id="72e4e-226"></span></span>

 <span data-ttu-id="72e4e-227">**Manifestdatei SSA**</span><span class="sxs-lookup"><span data-stu-id="72e4e-227">**SSA manifest file**</span></span>
  
    
    

```XML
<BETest>
  <Writer writerid="da452614-4858-5e53-a512-38aab25c61ad">
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\2e1f9435-d714-4bcb-be8d-ae1214e2ea22" componentName="SearchAppOffice" />
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\b8bb09b8-a823-43b0-a131-7bd5464f91fb" componentName="SearchAppOffice_CrawlStore" />
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\20c0c0b5-2086-4b16-8ce8-2cecb5186ebe" componentName="SearchAppOffice_AnalyticsReportingStore" />
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\15004c47-21ca-441e-80fe-9e068ef4ad14" componentName="SearchAppOffice_LinksStore" />
  </Writer>
  <Writer writerid="a65faa63-5ea8-4ebc-9dbd-a0c4db26912a">
    <Component logicalPath="DDDVSS4\\SQLEXPRESS" componentName="SearchAppOffice" />
    <Component logicalPath="DDDVSS4\\SQLEXPRESS" componentName="SearchAppOffice_CrawlStore" />
    <Component logicalPath="DDDVSS4\\SQLEXPRESS" componentName="SearchAppOffice_AnalyticsReportingStore" />
    <Component logicalPath="DDDVSS4\\SQLEXPRESS" componentName="SearchAppOffice_LinksStore" />
  </Writer>
</BETest>

```

 <span data-ttu-id="72e4e-228">**Index-Manifestdatei**</span><span class="sxs-lookup"><span data-stu-id="72e4e-228">**Index manifest file**</span></span>
  
    
    



```XML

<BETest>
  <Writer writerid="da452614-4858-5e53-a512-38aab25c61ad">
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\cfbddb07-2409-4b3d-997b-ee1b936c3dbd" componentName="IndexComponentGroup_3bca1050-c15a-4987-93dc-8f911d35a0ba" />
  </Writer>
  <Writer writerid="0ff1ce15-0201-0000-0000-000000000000">
    <Component logicalPath="" componentName="IndexComponentGroup_3bca1050-c15a-4987-93dc-8f911d35a0ba" />
  </Writer>
</BETest>
```


## <a name="additional-resources"></a><span data-ttu-id="72e4e-229">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="72e4e-229">Additional resources</span></span>
<span data-ttu-id="72e4e-230"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="72e4e-230"></span></span>


-  [<span data-ttu-id="72e4e-231">SharePoint Foundation und der Volumeschattenkopie-Dienst</span><span class="sxs-lookup"><span data-stu-id="72e4e-231">Windows SharePoint Services and the Volume Shadow Copy Service</span></span>](http://msdn.microsoft.com/library/adae101a-078e-40b9-9cfa-db2cfb10270a%28Office.15%29.aspx)
    
  

