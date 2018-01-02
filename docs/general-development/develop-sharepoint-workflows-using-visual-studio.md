---
title: Entwickeln von SharePoint-Workflows mit Visual Studio
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 28f5d3b1-6fe8-4b1f-8c4e-b11105fe6f46
ms.openlocfilehash: 8968b1f15a929aed1bb713cb2dccccc495f18743
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="develop-sharepoint-workflows-using-visual-studio"></a>Entwickeln von SharePoint-Workflows mit Visual Studio
SharePoint unterstützt zwei primäre Workflowentwicklungsumgebungen zur Erstellung von Workflows: SharePoint Designer und Visual Studio. Dieser Artikel bietet einen Überblick über beide und erläutert die jeweiligen Vor- und Nachteile.
## <a name="authoring-basics-for-sharepoint-workflows"></a>Grundlegendes zur Erstellung von SharePoint-Workflows
<a name="bkm_AuthoringBasics"> </a>

> [!NOTE]
> Hinweise zur Einrichtung und Konfiguration von Microsoft SharePoint und dem Workflow-Manager-Client 1.0-Server finden Sie unter [Einrichten und Konfigurieren von SharePoint-Workflow-Manager](set-up-and-configure-sharepoint-workflow-manager.md). 
  
    
    

Wie bei früheren Versionen stellt Microsoft SharePoint zwei primäre Workflowentwicklungsumgebungen zur Erstellung von Workflows bereit: Microsoft SharePoint Designer und Microsoft Visual Studio. Der Unterschied zu früheren Version besteht allerdings darin, dass bei Verwendung von Visual Studio keine codebasierte Erstellungsstrategie mehr bereitgestellt wird. Stattdessen bieten sowohl SharePoint Designer als auch Visual Studio unabhängig von dem von Ihnen ausgewählten Entwicklungstool eine vollständig deklarative, codefreie Erstellungsumgebung.
  
> [!NOTE]
> Als Ergänzung zur Erstellung von Workflows in SharePoint Designer können Sie auch Microsoft Visio 2013 verwenden, um Ihre Workflowlogik mithilfe von Visio 2013-Shapes zu strukturieren, und Ihre Logik dann in SharePoint Designer 2013 importieren. Informationen zur Verwendung von Visio 2013 zum Erstellen Ihrer Workflowlogik finden Sie unter [Workflowentwicklung in SharePoint Designer und Visio](workflow-development-in-sharepoint-designer-and-visio.md). 
  
    
    


### <a name="declarative-workflows"></a>Deklarative Workflows

Zunächst sollten Sie wissen, was unter "deklarativen" Workflows zu verstehen ist. Dieser Begriff bedeutet, dass der Workflow nicht in Form von Code erstellt und dann zu verwalteten Assemblys kompiliert wird, sondern in XAML (wortwörtlich) beschrieben und dann zur Laufzeit interpretativ ausgeführt wird.
  
    
    
Das XAML wird von den Workflowbausteinen abgeleitet, die Sie in Workflow-Designer (falls Sie Visual Studio verwenden) oder der Workflowdesignoberfläche von SharePoint Designer (oder Visio, mehr dazu später) bearbeiten. Die Bausteine selbst sind die visuellen Workflowdesignobjekte in der Entwurfstoolbox: Stufen, Bedingungen, Aktionen, Ereignisse usw. Der Satz von Tools in den entsprechenden Toolboxes (Visual Studio oder SharePoint Designer) unterscheidet sich geringfügig, das Konzept des deklarativen Workflows bleibt jedoch das gleiche.
  
    
    

## <a name="decision-tree-sharepoint-designer-vs-visual-studio"></a>Entscheidungsbaum: SharePoint Designer im Vergleich zu Visual Studio
<a name="bkm_DecisionTree"> </a>

Zu den größten Vorteilen des Workflowframeworks in SharePoint zählt die Benutzerfreundlichkeit, die es Information Workern erlaubt, mithilfe der codefreien Umgebung von SharePoint Designer umfangreiche und leistungsfähige Workflows zu erstellen. Darüber hinaus bietet eine deklarative Erstellungsumgebung wie Visual Studio ein hohes Maß an Flexibilität und Anpassung.
  
    
    
Beide dieser Workflowerstellungsumgebungen, SharePoint Designer und Visual Studio, sind mit spezifischen Vor- und Nachteilen verbunden. In diesem Abschnitt erfahren Sie, wie Sie herausfinden, welche Erstellungsumgebung für Ihre Anforderungen im Hinblick auf die Workflowentwicklung am besten geeignet ist.
  
    
    

### <a name="using-sharepoint-designer"></a>Verwenden von SharePoint Designer


- **Zielgruppe:** Information Worker, Geschäftsanalysten, SharePoint-Entwickler
    
  
- **Schwierigkeitsstufe:** Gute Kenntnisse im Umgang mit SharePoint Designer, einschließlich der zentralen Workflowkomponenten wie Stufen, Gates, Aktionen, Bedingungen und Schleifen
    
  
Mit SharePoint Designer können Benutzer mithilfe eines codefreien, textbasierten Entwurfstools einen Workflow erstellen, der mit einer Liste, Bibliothek oder Website verknüpft ist. Sie können auch die neue visuelle Entwurfsumgebung verwenden, in der grafische Elemente so auf einer Entwurfsoberfläche angeordnet sind, dass sie den logischen Ablauf eines Geschäftsprozesses darstellen. SharePoint Designer bietet unvergleichliche Funktionen, um technisch wenig versierten Benutzern die schnelle Entwicklung von Workflows zu ermöglichen.
  
    
    

### <a name="using-visual-studio"></a>Verwenden von Visual Studio


- **Zielgruppe:** Softwareentwickler mit mittleren oder erweiterten Kenntnissen.
    
  
- **Schwierigkeitsstufe:** Gute Kenntnisse im Umgang mit Visual Studio, einschließlich Konzepten der Softwareentwicklung wie Ereignisempfänger, Verpackung und Bereitstellung und Sicherheit
    
  
Die Workflowerstellung in Visual Studio bietet die Flexibilität, Workflows zur Unterstützung quasi jedes Geschäftsprozesses zu erstellen, unabhängig von dessen Komplexität, und erlaubt das Debuggen und Wiederverwenden von Workflowdefinitionen. Der vielleicht wichtigste Punkt ist, dass Visual Studio Entwicklern erlaubt, SharePoint-Workflows als Teil einer umfassenderen SharePoint-Lösung oder SharePoint-Add-In einzubinden.
  
    
    
Visual Studio erlaubt Entwicklern die Erstellung benutzerdefinierter Aktionen, die von SharePoint Designer verwendet werden, und stellt die Mittel zur Ausführung benutzerdefinierter Logik bereit. Mit Visual Studio können Entwickler auch Workflowvorlagen erstellen, die auf mehreren Websites bereitgestellt werden können.
  
    
    

## <a name="comparing-sharepoint-designer-with-visual-studio"></a>Vergleich zwischen SharePoint Designer und Visual Studio
<a name="bkm_Comparing"> </a>

In der folgenden Tabelle werden die Features und Anforderungen für die Verwendung von SharePoint Designer und Visual Studio zur Erstellung von SharePoint-Workflows gegenübergestellt.
  
    
    

**Tabelle 1. Vergleich von Tools zur Workflowerstellung**


|**Feature/Anforderung**|**SharePoint Designer**|**Visual Studio**|
|:-----|:-----|:-----|
|Erlaubt schnelle Workflowentwicklung  <br/> |Ja  <br/> |Ja  <br/> |
|Erlaubt Wiederverwendung von Workflows  <br/> |Ein Workflow kann nur von der Liste oder Bibliothek verwendet werden, in der er entwickelt wurde. SharePoint Designer bietet allerdings wiederverwendbare Workflows, die auf der gleichen Website mehrmals verwendet werden können.  <br/> |Ein Workflow kann als Vorlage geschrieben werden, sodass er nach der Bereitstellung wiederverwendet und einer Liste oder Bibliothek zugeordnet werden kann.  <br/> |
|Erlaubt Ihnen, einen Workflow als Teil einer SharePoint-Lösung oder SharePoint-Add-In einzubinden  <br/> |Nein  <br/> |Ja  <br/> |
|Erlaubt Ihnen, benutzerdefinierte Aktionen zu erstellen  <br/> |Nein. Allerdings kann SharePoint Designer benutzerdefinierte Aktionen verwenden und implementieren, die mithilfe von Visual Studio erstellt und bereitgestellt werden.  <br/> |Ja. Beachten Sie allerdings, dass in Visual Studio die zugrunde liegenden Aktivitäten, nicht die entsprechenden Aktionen, verwendet werden.  <br/> |
|Erlaubt Ihnen, benutzerdefinierten Code zu schreiben  <br/> |Nein  <br/> |Nein  <br/> **Hinweis:** Dies ist anders als bei früheren Versionen. In SharePoint sind Workflows nur deklarativ, und Visual Studio benötigt für die Workflowentwicklung die visuelle Designüberfläche.           |
|Visio Professional kann zum Erstellen der Workflowlogik verwendet werden  <br/> |Ja  <br/> |Nein  <br/> |
|Bereitstellung)  <br/> |Werden automatisch in der Liste, Bibliothek oder Website bereitgestellt, in der sie erstellt wurden  <br/> |Erstellen einer SharePoint-Lösungspaketdatei (.wsp) und Bereitstellen des Lösungspakets auf der Website (SPWeb)  <br/> |
|Veröffentlichen per Mausklick für Workflows verfügbar  <br/> |Ja  <br/> |Ja  <br/> |
|Workflows können verpackt und auf einem Remoteserver bereitgestellt werden  <br/> |Ja  <br/> |Ja  <br/> |
|Debugging  <br/> |Kein Debuggen möglich.  <br/> |Workflow kann mithilfe von Visual Studio debuggt werden.  <br/> |
|Kann nur Aktionen verwenden, die vom Websiteadministrator genehmigt wurden  <br/> |Ja  <br/> |Ja  <br/> **Hinweis:** Dies ist anders als bei früheren Versionen. Zuvor waren Workflows und Aktionen, die mit Visual Studio erstellt wurden, codebasiert und wurden im Farmbereich bereitgestellt, sodass keine Administratorgenehmigung erforderlich war.           |
   

## <a name="developing-workflows-using-visual-studio"></a>Entwickeln von Workflows mit Visual Studio
<a name="bkm_Developing"> </a>

Anders als in früheren Versionen sind Workflows in SharePoint vollständig deklarativ. Visual Studio, das nun auf Windows Workflow Foundation 4 basiert, bietet eine visuelle Workflow-Designeroberfläche, mit der Sie benutzerdefinierte Workflows, Workflowvorlagen, Formulare und benutzerdefinierte Workflowaktivitäten vollständig in der Designerumgebung erstellen können. Ihr Workflow wird dann verpackt und als ein SharePoint-Feature bereitgestellt. Informationen zum Verpacken von Features finden Sie unter  [Workflowentwicklung in Visual Studio](http://msdn.microsoft.com/de-DE/library/ms461324.aspx).
  
    
    
Die vielleicht wichtigste Änderung für Visual Studio-Entwickler ist, dass benutzerdefinierte Workflows nicht mehr als .NET Framework-Assemblys zusammengestellt und bereitgestellt werden. Darüber hinaus verwendet SharePoint keine Microsoft InfoPath-Formulare mehr; stattdessen werden zur Formularerstellung Microsoft ASP.NET-Formulare benötigt. 
  
    
    
Außerdem wurden die Visual Studio-Workflowprojektvorlagen geändert. Während früher Vorlagen für Zustandsautomat- und sequenzielle Workflows bereitgestellt wurden, ist diese Unterscheidung nun nicht mehr relevant. Stattdessen stehen im Visual Studio-Build auf Ihrem virtuelle Computer Visual Studio-Projektvorlagen zur Verfügung.
  
    
    

## <a name="enabling-on-premises-workflow-debugging"></a>Aktivieren von lokalem Workflow-Debuggen
<a name="bkm_Enabling"> </a>

Um lokale Workflows in Visual Studio zu debuggen, müssen Sie den Workflow-Manager-Tools vorübergehend Zugriff auf Ihr System über die Firewall erlauben.
  
    
    

1. Wählen Sie in der **Systemsteuerung** **System und Sicherheit**, **Windows-Firewall** aus.
    
  
2. Wählen Sie in der Liste **Startseite der Systemsteuerung** den Link **Erweiterte Einstellungen** aus.
    
  
3. Wählen Sie im linken Fenster von "Windows-Firewall" **Eingehende Regeln** aus.
    
  
4. Wählen Sie in der Liste **Eingehende Regeln** **Workflow Manager Tools 1.0 for Visual Studio 2012 - Test Service Host** aus.
    
  
5. Wählen Sie in der Liste **Aktionen** **Regel aktivieren** aus.
    
  
6. Wählen Sie auf der Eigenschaftenseite Ihres SharePoint-Projekts die Registerkarte **SharePoint** aus, und aktivieren Sie dann das Kontrollkästchen **Workflow-Debugging aktivieren**.
    
  

## <a name="debugging-sharepoint-online-workflows-using-visual-studio"></a>Debuggen von SharePoint Online-Workflows mit Visual Studio
<a name="bkm_Debug"> </a>

Führen Sie die folgenden Schritte durch, um SharePoint Online-Workflows in Visual Studio zu debuggen:
  
    
    

1. Wenn sich Ihr Computer hinter einer Firewall befindet, müssen Sie je nach Netzwerktopologie Ihres Unternehmens möglicherweise einen Proxyclient (wie den  [Forefront Threat Management Gateway (TMG)-Client](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=10504)) installieren.
    
  
2. Registrieren Sie sich für ein Microsoft Azure-Konto, wenn Sie dies nicht bereits getan haben, und melden Sie sich dann bei diesem Konto an.
    
    Informationen dazu, wie Sie sich für ein Microsoft Azure-Konto registrieren, finden Sie unter  [Microsoft Azure](http://www.windowsazure.com).
    
  
3. Erstellen Sie einen Microsoft Azure-Servicebus-Namespace, den Sie zum Debuggen von Remoteworkflows verwenden können. Sie können dies im  [Microsoft Azure-Verwaltungsportal](http://manage.windowsazure.com) tun.
    
    Weitere Informationen zum Microsoft Azure Service Bus finden Sie unter  [Verwalten von Service Bus-Dienstnamespaces](http://msdn.microsoft.com/de-DE/library/windowsazure/hh690928.aspx).
    
    > [!NOTE]
    > Das SharePoint Online-Workflowdebugging verwendet die Relay-Dienst-Komponente von Microsoft Azure Service Bus, sodass Ihnen die Nutzung von Service Bus berechnet wird. Siehe [Preise-FAQ zu Service Bus](http://msdn.microsoft.com/library/hh667438.aspx). Sie erhalten in jedem Monat, in dem Sie Visual Studio Professional mit MSDN, Visual Studio Premium mit MSDN oder Visual Studio Ultimate mit MSDN abonnieren, kostenlosen Zugriff auf Microsoft Azure. Mit diesem Zugriff können Sie das Service Bus-Relay je nach MSDN-Abonnement 1.500, 3.000 oder 3.000 Stunden verwenden. Siehe [Begrenzte monatliche Nutzung von Microsoft Azure Services ohne Zusatzkosten](http://www.windowsazure.com/de-DE/pricing/member-offers/msdn-benefits/). 
4. Wählen Sie in Microsoft Azure Ihren Service-Namespace, klicken Sie auf den **Zugriffsschlüssel**-Link und kopieren Sie dann den Text im Feld **Verbindungszeichenfolge**.
    
  
5. Wählen Sie auf der Eigenschaftenseite Ihres SharePoint-Add-In-Projekts die Registerkarte **SharePoint** aus, und aktivieren Sie dann das Kontrollkästchen **Workflow-Debugging aktivieren**.
    
    Sie müssen dieses Feature aktivieren, um Workflows in SharePoint Online zu debuggen. Diese Eigenschaft wird auf alle Ihre SharePoint-Projekte in Visual Studio angewendet. Visual Studio deaktiviert Workflow-Debugging automatisch, wenn Sie Ihre App zur Verteilung im Office Store verpacken.
    
  
6. Aktivieren Sie das Kontrollkästchen **Debugging über Microsoft Azure Service Bus aktivieren**. Fügen Sie dann im Textfeld **Verbindungszeichenfolge für Microsoft Azure Service Bus** die kopierte Verbindungszeichenfolge ein.
    
  
Nachdem Sie Workflow-Debugging aktualisiert und eine gültige Verbindungszeichenfolge für Microsoft Azure Service Bus eingegeben haben, können Sie SharePoint Online-Workflows debuggen.
  
> [!NOTE]
> Wenn Sie Workflow-Debugging nicht deaktiviert haben und nicht jedes Mal eine Benachrichtigung erhalten möchten, wenn Ihr Projekt einen Workflow enthält, deaktivieren Sie das Kontrollkästchen **Mich benachrichtigen, wenn Microsoft Azure Service Bus-Debugging nicht konfiguriert ist**.
  
    
    


## <a name="see-also"></a>Siehe auch
<a name="workflowbk_addres"> </a>

Die Entwicklung von SharePoint-Workflows bleibt für den Visual Studio-Entwickler größteils unverändert. Die wichtigsten Abschnitte der Dokumentation für SharePoint 2010 sind weiterhin relevant:
  
    
    

- Informationen zur Verwendung von Visual StudioWorkflow-Designer finden Sie unter  [Visual Studio Designer für Windows Workflow Foundation (Übersicht)](http://msdn.microsoft.com/de-DE/library/ms441543.aspx).
    
  
- Informationen zur Erstellung von Formularen mit Microsoft ASP.NET finden Sie unter  [Workflowformulare (Übersicht)](http://msdn.microsoft.com/de-DE/library/ms457061.aspx).
    
  
- Informationen zum Verpacken von Features finden Sie unter  [Workflowentwicklung in Visual Studio](http://msdn.microsoft.com/de-DE/library/ms461324.aspx).
    
  
