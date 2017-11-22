---
title: Application Lifecycle Management in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a
ms.openlocfilehash: a969bc3ae2e64de2214e8e85443ddc3164c10341
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-application-lifecycle-management"></a>Application Lifecycle Management in SharePoint
In diesem Artikel erfahren Sie, wie Sie gängige ALM (Application Lifecycle Management)-Konzepte und -Methoden auf die Anwendungsentwicklung mit SharePoint-Technologien anwenden können.

**Bereitgestellt von:** Eric Charran, Microsoft Corporation

**Mitwirkende:** Vesa Juvonen, Microsoft Corporation | Steve Peschka, Microsoft Corporation

> **Wichtig:** In diesem Artikel wird Bezug genommen auf automatisch gehostete SharePoint-Add-Ins. Die Preview-Phase für automatisch gehostete Apps ist beendet. Bitte ignorieren Sie alle Verweise auf automatisch gehostete SharePoint-Add-Ins. 


## <a name="overview-of-application-lifecycle-management-alm"></a>Überblick über ALM (Application Lifecycle Management)
<a name="Overview"> </a>

Entwickler haben in Microsoft SharePoint mehrere Möglichkeiten, mithilfe von SharePoint-Technologien Anwendungen zu erstellen und bereitzustellen –sowohl lokale Anwendungen als auch Anwendungen für gehostete Plattformen oder Public-Cloud-Plattformen. Dabei bietet SharePoint jetzt noch mehr Flexibilität hinsichtlich der unterstützten Anwendungstypen sowie neue Optionen für die Verwendung standardbasierter Technologien in Anwendungen. Doch auch, wenn Entwickler mit den Anwendungsfunktionen und Bereitstellungsoptionen des neuen SharePoint-Anwendungsmodells innovative und immersive Anwendungen entwickeln können: Sie müssen gleichzeitig in der Lage sein,die Aspekte Qualitätssicherung, Anwendungstests und ALM in ihren Entwicklungsprozess zu integrieren. In diesem Artikel erfahren Sie, wie Sie gängige ALM-Konzepte und -Methoden auf die Anwendungsentwicklung mit SharePoint-Technologien anwenden können.

### <a name="whats-new"></a>Neuerungen
<a name="WhatsNew"> </a>

SharePoint etabliert ein neues Paradigma für die Implementierung von Anwendungen. Angesichts dieser kompletten Neuorientierung des Modells für die Anwendungsentwicklung mit SharePoint-Technologien müssen Entwickler und Architekten sich umfassend in die neuen Muster, Methoden und Bereitstellungsmodelle einarbeiten, die SharePoint für die Anwendungsentwicklung bereitstellt. Ein wichtiger Punkt dabei: Zwar hat sich das Anwendungsmodell für die Entwicklung von Lösungen mit SharePoint verändert, doch sind viele der zur Lösungsentwicklung verwendeten Muster (inklusive der verfügbaren Technologien und Implementierungstechniken) konform mit den aktuell verfügbaren Technologien für die Entwicklung von Webanwendungen.
  
    
    
Nachfolgend erläutern wir Ihnen, welche Typen von Anwendungen Sie mit den SharePoint-Technologien erstellen können, und geben Ihnen wichtige Tipps für lokale Anwendungen und Cloudanwendungen. Informationen zu Hostingoptionen für SharePoint-Add-Ins finden Sie unter [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).
  
    
    
Da SharePoint jetzt mehr Flexibilität in puncto Lösungsimplementierung bietet, empfiehlt Microsoft seinen Kunden außerdem eine Evaluierung der zur Anwendungsentwicklung mit SharePoint verwendeten Technologien. Bei der Anwendungsentwicklung können Sie für die Darstellungsschicht und die Benutzerschicht auf standardbasierte Technologien wie HTML5 und JavaScript setzen und gleichzeitig OData und OAuth für dienstbasierte Zugriffe auf Back-End-Dienste wie SharePoint verwenden. Dabei sollten Sie genau abwägen, ob voll vertrauenswürdiger Code erforderlich ist (d. h. in SharePoint bereitgestellte kompilierte Assemblys). Dieses Entwicklungsparadigma wird zwar weiterhin unterstützt und ist in manchen Szenarien auch erforderlich, führt jedoch im ALM-Prozess zu signifikantem Overhead.
  
    
    
Weitere Informationen zu den neuen flexiblen Entwicklungstechnologien für Anwendungen in SharePoint finden Sie unter [Übersicht über die SharePoint-Entwicklung](sharepoint-development-overview.md).
  
    
    

### <a name="benefits-and-changes"></a>Vorteile und Änderungen
<a name="Benefits"> </a>

Die von SharePoint unterstützten Technologien zur Anwendungsentwicklung bieten jetzt mehr Flexibilität hinsichtlich der Auswahl von Programmiersprachen und Programmierarchitekturen. Entwickler müssen daher ihre aktuellen ALM-Methoden an die von SharePoint unterstützten Optionen anpassen. Neben den Konzepten Testing, Buildimplementierung, Bereitstellung und Qualitätslenkung sollte jetzt auch die Bereitstellung in SharePoint als SharePoint-Anwendung in die ALM-Strategie aufgenommen werden. Konkret bedeutet das: Auch wenn viele Entwickler ausgiebige Erfahrung mit der Programmierung und Bereitstellung serverseitiger Farmlösungen haben, die die Kernfunktionen von SharePoint erweitern, müssen sie nun möglicherweise gängige ALM-Methoden für das neue flexible Entwicklungsmodell für SharePoint-Anwendungen in ihren Implementierungsprozess integrieren.
  
    
    
Da immer mehr Kunden auf in der Cloud gehostete SharePoint-Implementierungen umsteigen, müssen Entwickler wissen, wie sie die Entwicklung, das Testing und die Bereitstellung von Zielumgebungen außerhalb der physischen Grenzen ihrer Organisation in ihre ALM-Strategie aufnehmen können. Dazu müssen sie unter anderem die Technologien auf den Prüfstand stellen, die sie nutzen, um ihre Anwendungen zu entwickeln, zu testen und bereitzustellen.
  
    
    
Entwickler und Architekten erstellen heute verstärkt Lösungen aus mehreren Anwendungskomponenten, die unterschiedliche Hostingoptionen miteinander kombinieren. Dabei sollten ALM-Verfahren einheitlich auf alle in der Lösung enthaltenen Anwendungen angewendet werden. Ein Beispiel: Ein Entwickler muss eine Anwendung bereitstellen, für die sowohl lokale Dienste wie IIS, ASP.NET, MVC, WebAPI und WCF bereitgestellt werden müssen als auch Microsoft Azure, SharePoint und SQL Azure. Gleichzeitig müssen die Anwendungskomponenten Qualitätstests unterzogen werden, und es gilt festzustellen, ob seit dem letzten Build Regressionen eingefügt wurden. Um all diesen Anforderungen gerecht werden zu können, müssen die Entwickler und ihre Teams die altbekannten und gut dokumentierten Build- und Bereitstellungsprozesse für lokale und serverseitige Lösungen möglicherweise von Grund auf überdenken.
  
    
    

### <a name="development-team-considerations"></a>Wichtige Aspekte für Entwicklungsteams
<a name="DevTeam"> </a>

Organisationen mit mehr als einem Anwendungsentwickler oder Anwendungsarchitekten müssen die Teamarbeit an SharePoint-Entwicklungsprojekten sorgfältig planen, um höchste Anwendungsqualität und eine ausreichend hohe Entwicklerproduktivität zu gewährleisten. Da die Methode für die Anwendungsentwicklung jetzt flexibler ist, müssen die Teams nicht nur mit ALM-Methoden und -Mustern vertraut sein und diese genau definieren; sie müssen auch festlegen, wie die einzelnen Entwickler den Code programmieren werden, und sicherstellen, dass die Gewährleistung höchster Codequalität fester Bestandteil des Anwendungserstellungsprozesses wird.
  
    
    
Diese Überlegungen beginnen mit der Auswahl der geeigneten Entwicklungsumgebung. In der Vergangenheit waren Entwickler dazu gezwungen, Entwicklungsarbeiten auf separaten Maschinen durchzuführen, die an ein gemeinsames Coderepository wie Visual Studio TFS 2012 angeschlossen waren, das Funktionen für Erstellung, Bereitstellung und Tests bereitstellte. TFS stellt weiterhin eine wichtige instrumentelle Komponente einer ALM-Strategie dar, die für Entwicklungsaktivitäten zentral ist, allerdings sollten sich Teams überlegen, wie sie TFS für die verschiedenen Typen von Entwicklungsumgebungsoptionen verwenden können.
  
    
    
Je nach Zielumgebung und Lösungstyp (d. h. welche Komponenten lokal und welche in Cloud-Infrastruktur oder bei Cloud-Diensten gehostet werden) können Entwickler jetzt aus einer Kombination neuer Entwicklungsumgebungsoptionen wählen. Diese Optionen bestehen aus neuen Auswahlmöglichkeiten, wie der SharePoint-Entwicklungswebsitevorlage und einem Office 365-Entwicklungsmandanten, sowie älteren Auswahlmöglichkeiten, wie z. B. auf virtuellen Maschinen basierte Entwicklung mithilfe von Hyper-V in Windows 8 oder Windows Server 2012.
  
    
    
Im folgenden Abschnitt werden für Anwendungsentwickler und -teams Überlegungen zur Entwicklungsumgebung beschrieben.
  
    
    

## <a name="development-environment-considerations"></a>Überlegungen zur Entwicklungsumgebung
<a name="DevEnvironment"> </a>

Die Auswahl einer Entwicklungsumgebung sollte auf Basis mehrerer Faktoren erfolgen. Diese Überlegungen werden größtenteils durch den Typ der entwickelten Anwendung und die Zielplattform für die Anwendung beeinflusst. Wenn Entwickler in der Vergangenheit Anwendungen für SharePoint Server 2010 erstellten, stellten sie virtuelle Maschinen bereit und führten die Entwicklung in Isolation durch. Dies lag daran, dass die Bereitstellung voll vertrauenswürdiger Lösungen Neustarts von SharePoint-Kernabhängigkeiten wie IIS erfordert hätte, was verhindert hätte, dass mehrere Entwickler eine einzelne SharePoint-Umgebung verwenden. Da sich Entwicklungstechnologien verändert haben und es nun mehr Optionen für Entwickler gibt, die Anwendungen erstellen, sollten Entwickler und Teams wissen, welche verschiedenen Entwicklungsumgebungen ihnen zur Verfügung stehen. Abbildung 1 zeigt die Entwicklungsumgebung und die verschiedenen Tools, einschließlich der Typen von Lösungen, die in den Zielumgebungen bereitgestellt werden können.
  
    
    

**Abbildung 1: Entwicklungsumgebungen - Komponenten und Tools**


    
 [![Die zur App-Entwicklung verwendete Umgebung kann Office 365, Visual Studio oder ein virtueller Computer sein.](../images/AppDevelopmentEnvironment.png)
  
    
    

### <a name="development-environment-philosophy"></a>Grundsätze für Entwicklungsumgebungen
<a name="DevPhilosophy"> </a>

Angesichts der neuen Möglichkeiten für den Entwurf und die Implementierung von Anwendungen in SharePoint sollten Entwickler evaluieren, ob sie für die Entwicklung ihrer Anwendungen serverseitigen Code benötigen. Da heute verstärkt in der Cloud gehostete Anwendungen entwickelt werden, besteht immer seltener die Notwendigkeit für virtualisierte Entwicklungsumgebungen. Das gilt insbesondere für SharePoint. Entwickler sollten für die Lösungserstellung stattdessen auf das Remoteentwicklungsmodell setzen, das auf ihrer bereits vorhandenen cloudbasierten Infrastruktur aufsetzt (öffentliche Cloud oder private Cloud). Wenn sich Entwicklungsumgebungen schnell und unkompliziert bereitstellen lassen, ohne dass zunächst eine virtualisierte Umgebung erstellt und orchestriert werden muss, können die Entwickler ihre Zeit verstärkt in die tatsächliche Programmierung und die Qualitätssicherung investieren statt in die Infrastrukturverwaltung.
  
    
    
Ob Sie sich für eine virtualisierte Instanz von SharePoint oder die neue SharePoint-Entwicklerwebsitevorlage entscheiden sollten, hängt davon ob, ob für Ihre Anwendung voll vertrauenswürdiger Code in SharePoint bereitgestellt und ausgeführt werden muss. Ist kein voll vertrauenswürdiger Code erforderlich, empfehlen wir die Verwendung der Entwicklerwebsitevorlage. Diese Vorlage finden Sie in Office 365-Entwicklermandanten oder in der lokalen SharePoint-Implementierung Ihrer Organisation. Mithilfe von Entwicklerwebsitevorlagen können Sie Ihre Anwendungen direkt aus Visual Studio in SharePoint bereitstellen. Auf Office 365-Entwicklerwebsites sind Anwendungsisolation und OAuth bereits vorkonfiguriert. Sie können also sofort mit der Anwendungsprogrammierung und den Anwendungstests beginnen.
  
    
    
In den nachfolgenden Abschnitten beschreiben wir detailliert, wann Sie welche Entwicklungsumgebung für die Erstellung Ihrer Anwendungen nutzen sollten.
  
    
    

### <a name="o365-development-sites-public-cloud"></a>O365-Entwicklungswebsites (öffentliche Cloud)
<a name="O365Development"> </a>

Abbildung 2 zeigt, wie Entwickler Office 365 als eine Entwicklungsumgebung verwenden können, und umfasst die Typen von Tools, mit denen SharePoint-Anwendungen erstellt werden, die in Office 365 gehostet werden können.
  
    
    

**Abbildung 2. Office 365-App-Entwicklung**

  
    
    
 [![Erstellen von Apps für SharePoint mit Office 365, Visual Studio und Napa](../images/Office365AppDevelpment.png)
  
    
    
Entwickler mit MSDN-Abonnements können einen Entwicklungsmandanten erhalten, der eine SharePointWebsite für Entwickler enthält. Die SharePointWebsite für Entwickler ist für die Entwicklung von Anwendungen vorkonfiguriert. Benutzer können Visual Studio 2012 nicht nur für die Entwicklung von Anwendungen verwenden. Mit Office 365-Entwicklerwebsites kann Napa innerhalb der Website zur Erstellung von Anwendungen verwendet werden. Weitere Informationen zum Einstieg in eine Website für Office 365-Entwickler finden Sie unter  [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx).
  
    
    
Entwickler können Anwendungen erstellen, die in Office 365, lokal oder in einer anderen, anbietergehosteten Infrastruktur gehostet werden. Der Vorteil dieser Umgebung: Sämtliche Infrastruktur-, Virtualisierungs- und Hostingaspekte für SharePoint-Entwicklungsumgebungen werden von Office 365 abstrahiert, sodass Anwendungen ohne Zeitverzögerung erstellt werden können. Wichtig zu bedenken ist dabei, dass Entwicklungsumgebungen dieser Art nicht für Anwendungen geeignet sind, für die voll vertrauenswürdiger Code in SharePoint bereitgestellt werden muss. Microsoft empfiehlt, wann immer möglich das clientseitige Objektmodell (CSOM) von SharePoint sowie clientseitige Technologien wie JavaScript zu verwenden. Sollte zwar voll vertrauenswürdiger Code erforderlich sein, nicht jedoch die Bereitstellung und Ausführung dieses Codes in SharePoint, empfehlen wir, den serverseitigen Code im Rahmen eines Modells mit automatischem oder anbieterbasiertem Hosting bereitzustellen. Dabei verwenden in anbietergehosteten Infrastrukturen bereitgestellte Lösungen mit voll vertrauenswürdigem Code ebenfalls CSOM, unterstützen jedoch auch Programmiersprachen wie C#. Ebenso können in einem anbietergehosteten Modell bereitgestellte Anwendungen auch dann CSOM zur Interaktion mit SharePoint verwenden, wenn sie andere Technologiestacks nutzen.
  
    
    
Entwicklungsteams, die separate Features oder Anwendungen erstellen, die eine größere Lösung enthalten, benötigen ein zentralisiertes Entwicklungsziel, um Testkomponenten zu integrieren. Da jeder Entwickler Features und Anwendungen auf seiner eigenen Office 365-Entwicklersite erstellt, sollte eine zentralisierte Websitesammlung in einem Zielmandanten oder einer lokalen Umgebung so bereitgestellt werden, dass dort die Anwendungskomponenten jedes Entwicklers bereitgestellt werden können. Dieser Ansatz ermöglicht die zentrale Durchführung von Integrationstests für Lösungskomponenten. Im  [Abschnitt zur Durchführung von Tests](#Testing) in diesem Dokument wird näher auf diesen Prozess eingegangen.
  
    
    

#### <a name="napaoffice-365-development-tools"></a>NapaOffice 365-Entwicklungstools
<a name="NapaDevelopment"> </a>

Die Napa-Entwicklungstools können von Entwicklern verwendet werden, um die Erstellung von Anwendungen in einer Office 365-Entwicklerwebsite zu vereinfachen. Die Napa-Tools sind für Entwickler oder Poweruser gedacht, die mit clientseitigen Technologien vertraut sind, um rasch Anwendungen für einen Prototyp, eine Machbarkeitsstudie oder eine schnelle Geschäftslösung zu entwickeln und bereitzustellen. Diese Tools bieten die Möglichkeit, Anwendungsfunktionen in SharePoint zu entwickeln. Während des Lebenszyklus einer Anwendung kann unter bestimmten Umständen ein Import der Anwendung in Visual Studio erforderlich sind. Zu diesen Umständen zählen folgende:
  
    
    

- Wenn mehr als ein Entwickler zu einer Lösung beitragen muss bzw. einen Teil der Lösung entwickeln muss
    
  
- Wenn eine Anwendung einen Abhängigkeitsgrad von Benutzern erreicht, der die Anwendung von Praktiken der Lebenszyklusverwaltung erfordert
    
  
- Wenn sich funktionsbezogene Anforderungen für die Anwendung mit der Zeit ändern und ergänzende Lösungskomponenten erforderlich sind (wie kompilierte Dienste oder Datenquellen)
    
  
- Wenn die Anwendung in andere Anwendungen oder Lösungskomponenten integriert werden muss
    
  
- Wenn Entwickler Qualitätskontrollmaßnahmen wie automatisierte Builds und Tests verwenden müssen
    
  
Sobald eine dieser Bedingungen oder eine ähnliche Bedingung eintritt, müssen Entwickler die Lösung in eine Umgebung unter Quellcodeverwaltung wie TFS exportieren und Überlegungen und Verfahren des ALM-Entwurfs auf die künftige Entwicklung der Anwendung anwenden.
  
    
    

### <a name="development-sites-remote-development"></a>Entwicklungswebsites (Remoteentwicklung)
<a name="OnPremDevelopment"> </a>

Für Organisationen oder Entwickler, die SharePoint-Anwendungen nicht hauptsächlich in Office 365-Entwicklerwebsites entwickeln möchten, können zur Entwicklung von SharePoint-Anwendungen lokale Entwicklungswebsites verwendet werden. In diesem Modell werden die Funktionen der Office 365-Entwicklerwebsites durch lokale Entwicklungswebsites ersetzt, die in einer SharePoint-Farm gehostet werden. Kunden können eine Private Cloud für die Entwicklung erstellen, indem Sie auf internen Entwicklerwebsiteinstanzen eine SharePoint-Farm bereitstellen. Kunden können ihre eigene Governance-Automatisierung verwenden, um Entwicklerwebsite-Vorlagenerstellung zu ermöglichen, oder die in SharePoint integrierten Funktionen zur Bereitstellung von Entwicklerwebsiteinstanzen verwenden. Abbildung 3 illustriert diesen Aufbau.
  
    
    

**Abbildung 3. Lokale App-Entwicklung mit der Entwicklerwebsitevorlage**

  
    
    
 [![Erstellen von Apps für SharePoint in einer lokalen SharePoint-Bereitstellung mit der Entwicklerwebsitevorlage](../images/OnPremDevSites.png)
  
    
    
    
    
Abbildung 3 beschreibt die Entwicklungstools und Anwendungstypen, die Entwicklerwebsites ermöglichen, wenn eine lokale SharePoint-Farm als Host verwendet wird. Beachten Sie, dass NapaOffice 365-Entwicklungstools in dieser Umgebung nicht eingesetzt werden können, da diese nur in Office 365-Entwicklungswebsites verwendet werden können.
  
    
    
Die SharePoint-Farm, die Website für Entwickler-Instanzen hostet, muss überwacht werden und Service-, Recovery Point- und zeitbezogene Ziele erfüllen, damit Entwickler, die damit Anwendungen erstellen, produktiv und unterbrechungsfrei arbeiten können. Kunden können auf diese Umgebung Private Cloud-Konzepte wie Elastizität, Skalierungseinheiten und eine Verwaltungs-Fabric anwenden. Betrieb und Verwaltung müssen auf die SharePoint-Farm angewendet werden, in der auch die Entwicklerwebsites verwaltet werden. Dadurch lässt sich eine unkontrollierte Verbreitung zahlreicher Entwicklerwebsites vermeiden, die nicht in Verwendung sind. Außerdem bietet dies die Möglichkeit zu ermitteln, wann die Umgebung skaliert werden muss.
  
    
    
Kunden können IaaS-Funktionen (Infrastructure-as-a-Service) wie Microsoft Azure verwenden, um die SharePoint-Farms zu hosten, die Entwicklerwebsites enthalten und hosten. Sie können auch ihre eigenen lokalen virtuellen oder physischen Umgebungen verwenden. Beachten Sie, dass bei Verwendung dieses Modells SharePoint nicht für jeden Entwickler installiert werden muss. Zur Remoteanwendungsentwicklung müssen nur Visual Studio und Office- und SharePoint-Entwicklungstools auf der Arbeitsstation des Entwicklers installiert sein.
  
    
    
Entwickler müssen vom Anbieter gehostete Infrastruktur schaffen, um die vom Anbieter gehosteten Anwendungen bereitzustellen. Vom Anbieter gehostete Komponenten einer SharePoint-Anwendung können zwar in einer Vielzahl von Technologien implementiert werden, doch Entwickler müssen eine Infrastruktur zum Hosten dieser Komponenten der Anwendungen bereitstellen, die außerhalb von SharePoint ausgeführt werden. Wenn ein Team z. B. eine SharePoint-Anwendung entwickelt, bei der sich die Komponente für die Benutzeroberfläche und sonstige Komponenten in einer ASP.NET-Anwendung befinden, sollte das Entwicklungsteam lokale Versionen von IIS,SQL Server usw. verwenden und herkömmliche ALM-Teamentwicklungsmuster für ASP.NET verwenden.
  
    
    

### <a name="self-contained-farm-environments-virtualized-farm-development"></a>Eigenständige Farmumgebungen (virtualisierte Farmentwicklung)
<a name="SelfContained"> </a>

Erfordert Ihre Lösung die Bereitstellung und Ausführung von voll vertrauenswürdigem Code in einer SharePoint-Farm, ist eine vollständige (und häufig auch virtualisierte) Implementierung von SharePoint nötig. Eine Anleitung für die Erstellung einer lokalen Entwicklungsumgebung für SharePoint finden Sie unter [Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx).
  
    
    
Abbildung 4 gibt einen Überblick über die verschiedenen Typen von Anwendungen, die sich in einer lokalen virtualisierten Umgebung erstellen lassen.
  
    
    

**Abbildung 4. Lokale Entwicklung mit einer virtuellen Umgebung**

  
    
    
 [![Erstellen von Apps für SharePoint in einer virtuellen lokalen Umgebung](../images/AppDevelopmentVirtualEnvironment.png)
  
    
    
    
    
Entwickler können Remoteentwicklung für die SharePoint und in der Cloud gehosteten Anwendungen in ihren eigenen SharePoint-Farmen sowie die Entwicklung von Farmlösungen mit voller Vertrauenswürdigkeit verwenden. Diese Farmen werden oft in einem Virtualisierungsserver gehostet, der auf der Arbeitsstation des Entwicklers oder in einer zentralen Private Cloud gehostet wird, die für Entwickler leicht zugänglich ist. Die SharePoint-Farmumgebung ist normalerweise von den Farmen anderer Entwickler getrennt und bietet einen Isolationsgrad, der beim Entwickeln von voll vertrauenswürdigem Code erforderlich ist und den Neustart kritischer Dienste (z. B. IIS) erfordern kann.
  
    
    
Remoteentwicklung und die Entwicklung von voll vertrauenswürdigem Code können innerhalb der eigenständigen Farm erfolgen, da jede Entwicklungsfarm isoliert ist und nur einem Entwickler zugeordnet ist.
  
    
    
Organisationen oder Entwickler müssen die SharePoint-Farmen, die in den virtuellen Computern ausgeführt werden, verwalten und aktualisieren. Entwickler, die an einer einzelnen Anwendung mitarbeiten, müssen die Parität zwischen den Entwicklungsfarmen wahren, die in den virtuellen Computern ausgeführt werden. Dadurch wird sichergestellt, dass jede für die Anwendung entwickelte Codekomponente konsistent ist. Weitere gängige Überlegungen sind eine Standardkonfiguration für die Farmen, einschließlich Domänenzugriff und Anmeldeinformationen, Dienstanwendungs-Anmeldeinformationen, Testidentitäten oder -konten und andere umgebungsbezogene Konfigurationselemente (wie Zertifikate).
  
    
    
Ähnlich einer zentralisierten Farm für Entwicklungswebsites können diese virtuellen Maschinen, auf denen SharePoint-Entwicklerfarmen ausgeführt werden, in IaaS-Plattformen wie Microsoft Azure und lokalen Private Cloud-Angeboten gehostet werden.
  
    
    
Obgleich virtuelle Maschinen einen hohen Grad an Isolation und Unabhängigkeit von anderen virtuellen Entwicklermaschinen bieten, sollten Teams gleiche Konfigurationen für virtuelle Maschinen anstreben. Dazu zählen eine gemeinsame Konfiguration für Domäne, Konto und Sicherheit und SharePoint und eine Verbindung zu einem Quellcodeverwaltungs-Repository wie Visual Studio Team Foundation Server (TFS).
  
    
    

## <a name="alm-design-considerations"></a>Überlegungen zum ALM-Entwurf
<a name="ALMDesign"> </a>

Bei der Erstellung von SharePoint-Anwendungen müssen einige Punkte beachtet werden, um zu Konsistenz- und Qualitätszwecken Governance- und gängige Entwicklungspraktiken bereitzustellen. Wenn ALM-Prinzipien auf die SharePoint-Anwendungsentwicklung angewendet werden, müssen sich Entwickler auf technische sowie prozessgesteuerte Überlegungen konzentrieren.
  
    
    
Zur Anwendungsentwicklung, insbesondere wenn Teams von Entwicklern an den gleichen Projekten arbeiten, ist normalerweise die Unterstützung einer ALM-Plattform wie Visual Studio Team Foundation Server 2012 erforderlich. SharePoint-Anwendungen erfordern wie andere technische Lösungen Coderepository-Verwaltung und Versionsverwaltung, Builddienste, Testdienste und Praktiken der Releaseverwaltung. Im folgenden Abschnitt werden Überlegungen für ALM mit Bezug auf die verschiedenen Anwendungsmodelle für SharePoint-Anwendungen beschrieben.
  
    
    

### <a name="overview"></a>Übersicht
<a name="ALMDesignOverview"> </a>

Für jede Art von SharePoint-Anwendung müssen die ALM-Überlegungen unverändert angewendet werden. Praktiken und Verfahren rund um Build, Tests und Änderungsverwaltung müssen allerdings angepasst werden.
  
    
    
Einige SharePoint-Anwendungen verwenden clientseitige Technologien. Die meisten Entwickler, die Erfahrung in der Entwicklung von SharePoint Server 2010-Anwendungen haben, müssen sich daran gewöhnen, nicht kompilierten Code zu entwickeln und darauf ALM-Prinzipien anzuwenden. So müssen etwa auch Konzepte wie ein "Build" auf eine Lösung angewendet werden, die möglicherweise keinen kompilierten Code aufweist. ALM-Plattformen wie Visual Studio 2012 weisen integrierte Funktionen zur Validierung von Builds auf. Dabei wird der Code zuerst kompiliert, und anschließend werden Buildüberprüfungstests ausgeführt.
  
    
    
Bei SharePoint-Anwendungen sollte der Build- und Testprozess mit den herkömmlichen Anwendungsentwicklungsprozessen übereinstimmen. Dazu zählt die Erstellung eines Buildzeitplans durch die ALM-Plattform, welche die Lösung kompiliert und in der Zielumgebung bereitstellt.
  
    
    

### <a name="build-processes"></a>Buildprozesse
<a name="ALMBuildProcess"> </a>

Die SharePoint-Anwendungsbuildprozesse werden durch die ALM-Plattform erleichtert. Visual Studio Team Foundation Server 2012 bietet sowohl Build- als auch Testdienste, die beim Einchecken der Lösung von Visual Studio 2012 (fortlaufende Integration) oder in bestimmten geplanten Zeitabständen ausgelöst werden können.
  
    
    

#### <a name="sharepoint-build-components"></a>SharePoint-Buildkomponenten
<a name="ALMBuildComponents"> </a>

Wenn Entwickler Buildprozesse für die Entwicklung von SharePoint-Anwendung planen, müssen sie die Interaktionen zwischen den Komponenten berücksichtigen (siehe Abbildung 5).
  
    
    

**Abbildung 5. In SharePoint gehostete App-Buildkomponenten**

  
    
    

  
    
    
![Visual Studio-Builds arbeiten mit App-Manifesten, Seiten und Hilfsdateien.](../images/AppDevelopmentClientBuildComponents.png)
  
    
    
Die Illustration in Abbildung 5 ist eine logische Darstellung einer SharePoint-Anwendung. Diese Illustration zeigt eine Von SharePoint gehostetes Add-In und hebt wichtige Anwendungsobjekte als Bestandteil eines Visual Studio 2012Von SharePoint gehostetes Add-In-Projekts hervor. Das SharePoint-App-Projekt enthält die Features, das Paket und das Manifest, welche bei SharePoint registriert werden. Das Projekt enthält außerdem Seiten, Skriptbibliotheken und andere Elemente der Benutzeroberfläche, welche die SharePoint-Anwendung bilden. Darüber hinaus enthält das SharePoint-Projekt unterstützende Dateien, welche die zur Bereitstellung in einer SharePoint-Zielumgebung erforderlichen Zertifikate umfassen.
  
    
    

**Abbildung 6. Vom Anbieter und automatisch gehostete App-Build-Komponenten**

  
    
    

  
    
    
![Vom Anbieter gehostete Apps enthalten sowohl SharePoint-App-Pakete als auch in der Cloud gehostete Komponenten.](../images/ProviderHostedAppBuildComponents.png)
  
    
    
Abbildung 6 zeigt eine in der Cloud gehostete (d. h. automatisch oder vom Anbieter gehostete) SharePoint-Anwendung. Der Hauptunterschied in der Projektstruktur ist, dass die Visual Studio 2012-Lösung zusätzlich zu einem oder mehreren Projekten, welche die in der Cloud gehosteten Anwendungskomponenten enthalten, ein SharePoint-Anwendungsprojekt enthält. Dazu können Webanwendungen, SQL-Datenbankprojekte oder Dienstanwendungen zählen, die in Azure oder einer lokalen vom Anbieter gehosteten Infrastruktur (wie ASP.NET) bereitgestellt werden, und andere Lösungskomponenten zählen. Eine Anleitung zum Packen und Bereitstellen besonders vertrauenswürdiger Anwendungen finden Sie unter  [Packen und Veröffentlichen besonders vertrauenswürdiger Add-Ins für SharePoint](http://msdn.microsoft.com/library/3c28aed8-c037-407c-9154-39a74073e170%28Office.15%29.aspx).
  
    
    

**Abbildung 7. ALM mit Visual Studio Team Foundation Server**

  
    
    

  
    
    
![TFS kann für die Durchführung von Build- und Bereitstellungsaktivitäten mit einer SharePoint-Anwendung über Builddefinitionen konfiguriert sein.](../images/ALMWithTFS.png)
  
    
    
Abbildung 7 zeigt TFS als die ALM-Plattform. Teams verwenden TFS zum Speichern von Code und zur Durchführung von Teamentwicklungsarbeiten mit lokal bereitgestelltem TFS oder mit cloudbasierten TFS-Diensten von Microsoft. TFS kann für die Durchführung von Build- und Bereitstellungsaktivitäten mit einer SharePoint-Anwendung durch Builddefinitionen konfiguriert werden. TFS kann auch zur Durchführung von Buildüberprüfungstests verwendet werden, die durch die Ausführung kodierter UI-Tests automatisiert werden können, die Teil der Builddefinition sind.
  
    
    

**Abbildung 8. TFS-Buildziele**

  
    
    

  
    
    
![Von einer TFS-Builddefinition ausgeführte Skripts stellen die SharePoint-Anwendungskomponenten auf SharePoint Online und in lokalen SharePoint-Umgebungen bereit.](../images/TFSBuildTargets.png)
  
    
    
Abbildung 8 zeigt die Zielumgebungen, in denen durch eine TFS-Builddefinition ausgeführte Skripts die SharePoint-Anwendungskomponenten bereitstellen. Bei in SharePoint gehosteten Anwendungen umfasst dies die Bereitstellung in SharePoint Online oder in lokalen SharePoint-Anwendungskatalogen.
  
    
    
Bei in der Cloud gehosteten SharePoint-Anwendungen werden die Komponenten der Lösung, die zusätzliche Infrastruktur außerhalb von SharePoint erfordern, in Zielumgebungen bereitgestellt. Bei automatisch gehosteten Anwendungen ist dies Microsoft Azure. Bei vom Anbieter gehosteten Anwendungen kann es sich bei dieser Infrastruktur um Microsoft Azure oder andere lokale oder IaaS-gehostete Umgebungen handeln.
  
    
    

#### <a name="creating-a-build-for-sharepoint-applications"></a>Erstellen eines Builds für SharePoint-Anwendungen
<a name="CreateBuild"> </a>

TFS stellt Builddienste bereit, die in die Quellcodeverwaltung eingecheckte Lösungen kompilieren und die Ausgabe auf automatisierte Weise an einem zentralen Ort zur Bereitstellung in Zielumgebungen ablegen können. Die vorrangig verwendete Methode, um TFS für automatisierte Builds, Bereitstellungen und das Testen von SharePoint-Anwendungen zu konfigurieren, stellt die Erstellung einer Builddefinition in Visual Studio dar. Die Builddefinition enthält Informationen darüber, welche Codeprojekte kompiliert werden sollen, sowie alle Aktivitäten nach der Kompilierung, wie die Durchführung von Tests und die eigentliche Bereitstellung in den Zielumgebungen. Weitere Informationen zum Team Foundation-Builddienst finden Sie unter  [Einrichten des Team Foundation-Builddiensts](http://msdn.microsoft.com/de-DE/library/vstudio/ee259687.aspx).
  
    
    
Um eine fortlaufende Integration zu erzielen, kann die Builddefinition ausgelöst werden, wenn Entwickler Code einchecken. Außerdem kann die Ausführung der Builddefinition in festen zeitlichen Abständen geplant werden.
  
    
    
Bei SharePoint-Anwendungen sollten Entwickler das Builddefinitionsprojekt  [Fortlaufende Integration von Office/SharePoint in TFS 2012](http://officesharepointci.codeplex.com/) verwenden, um geplante Builds oder fortlaufende Integration zu erzielen. Dieses Projekt bietet Builddefinitionen, Windows PowerShell-Skripts und Prozessanleitungen zum Konfigurieren von Visual Studio Online oder einer lokalen Version von TFS zur Erstellung und Bereitstellung von SharePoint-Anwendungen in einem fortlaufenden Integrationsmodell. Entwickler sollten die Komponenten in diesem Projekt herunterladen und ihre TFS-Instanz entsprechend konfigurieren. Eine Anleitung zum Konfigurieren von TFS mit der bereitgestellten Builddefinition für SharePoint-Anwendungen und zum Konfigurieren der Builddefinition für die Verwendung der Windows PowerShell-Skripte zur Bereitstellung der SharePoint-Anwendung in einer Zielumgebung finden Sie unter [Fortlaufende Integration von Office/SharePoint in TFS 2012 - Dokumentation](http://officesharepointci.codeplex.com/documentation).
  
    
    

#### <a name="configuring-build-and-deployment-procedures"></a>Konfigurieren von Build- und Bereitstellungsverfahren
<a name="ConfigureBuilds"> </a>

Abbildung 9 zeigt einen Standardprozess für SharePoint-Anwendungsbuilds und Bereitstellungen, wenn die Builddefinition in der TFS-Instanz des Teams erstellt, konfiguriert und bereitgestellt wurde.
  
    
    

**Abbildung 9. Build- und Bereitstellungsprozess mit TFS**

  
    
    
 [![TFS-Builddienste führen die in der Builddefinition der SharePoint-Anwendung festgelegten Schritte aus.](../images/ALMBuildDeployProcess.png)
  
    
    
    
Der Entwickler checkt die SharePointVisual Studio 2012-Lösung ein. Je nach gewünschter Konfiguration (d. h. fortlaufende Integration oder geplanter Build) führen TFS-Builddienste die von der SharePoint-Anwendungsbuilddefinition definierten Schritte aus. Diese vom Entwicklern konfigurierte Definition enthält die Vorlage für den Buildprozess mit fortlaufender Integration sowie Anleitungen nach dem Build zur Ausführung von Windows PowerShell-Skripts zur Anwendungsbereitstellung. Beachten Sie, dass die Erweiterungen der SharePoint Online-Verwaltungsshell erforderlich sind, um die Anwendung in SharePoint Online bereitzustellen. Weitere Informationen zu Erweiterungen der SharePoint Online-Verwaltungsshell finden Sie im Download Center auf der Seite zur  [SharePoint Online-Verwaltungsshell](http://www.microsoft.com/en-us/download/details.aspx?id=35588).
  
    
    
Nachdem der Build ausgelöst wurde, kompiliert TFS die mit der SharePoint-Anwendung verknüpften Projekte und führt Windows PowerShell-Skripts aus, um die Lösung in der SharePoint-Zielumgebung bereitzustellen.
  
    
    

#### <a name="trusting-the-sharepoint-application"></a>Der SharePoint-Anwendung vertrauen
<a name="TrustingApp"> </a>

Im Anschluss an die Bereitstellung der Anwendungskomponenten in den Zielumgebungen sollte beachtet werden, dass ein Mandantenadministrator (oder Websitesammlungsadministrator) der Anwendung auf der App-Informationsseite in SharePoint vertrauen muss, bevor jemand auf die Anwendung zugreift oder automatisierte Tests durchgeführt werden, die Teil des Builds sein können. Diese Anforderung bezieht sich auf automatisch gehostete und in SharePoint gehostete Apps. Dieser manuelle Prozess stellt eine Änderung im Buildprozess dar, da Tests, die normalerweise am Anschluss an die Bereitstellung in der Zielumgebung ausgeführt würden, angehalten werden müssen, bis der Anwendung vertraut wurde.
  
    
    
Beachten Sie, dass Entwickler bei in der Cloud (automatisch oder vom Anbieter) gehosteten Anwendungen die Nicht-SharePoint-Komponenten in der in der Cloud gehosteten Infrastruktur getrennt vom Anwendungspaket bereitstellen können, das in SharePoint bereitgestellt wurde.
  
    
    

**Abbildung 10. Bereitstellen von Nicht-SharePoint-Komponenten**

  
    
    
 [![Wenn Entwickler Änderungen an der Lösung vornehmen, die die SharePoint-Anwendung darstellt, kann es vorkommen, dass Änderungen an den Projekten in der Lösung vorgenommen werden, die nicht für das eigentliche SharePoint-Anwendungsprojekt gelten.](../images/ALMChangeManagement.png)
  
    
    
    
Wenn Entwickler Änderungen an der Lösung vornehmen, welche die SharePoint-Anwendung darstellt, kann es, wie Abbildung 10 zeigt, Fälle geben, in denen Änderungen an den Projekten in der Lösung vorgenommen werden, die nicht für das SharePoint-Anwendungsprojekt selbst gelten. In diesem Fall muss das SharePoint-Anwendungsprojekt nicht erneut bereitgestellt werden, da es nicht geändert wurde. Die mit den in der Cloud gehosteten Projekten verbundenen Änderungen müssen erneut bereitgestellt werden.
  
    
    
Änderungen an der Anwendung, die in Infrastruktur außerhalb von SharePoint bereitgestellt wird, können getrennt von den Anwendungskomponenten vorgenommen werden, die in der Zielwebsitesammlung oder im Zielmandanten bereitgestellt werden. Für Entwickler bedeutet dies, dass ein automatisierter Buildprozess erstellt werden kann, um die in der Cloud gehosteten Komponenten häufig (bei Auslösung) und getrennt vom SharePoint-Anwendungsprojekt bereitzustellen. Somit ist der manuelle Schritt zur Genehmigung der Berechtigung der Anwendung auf der App-Informationsseite in SharePoint nicht erforderlich, was den Bereitstellungs- und Testprozess für die Builddefinition reibungsloser macht. Die SharePoint-Anwendungskomponente der Lösung müsste nur bereitgestellt werden, wenn die Elmente in diesem Projekt geändert wurden und eine erneute Bereitstellung erforderlich ist.
  
    
    

### <a name="testing"></a>Testen
<a name="Testing"> </a>

Wie im  [Abschnitt zu Buildprozessen](#ALMBuildProcess) beschrieben, stellen Anwendungstests eine Methode dar, mit der ermittelt werden kann, ob die Kompilierung und Bereitstellung der Anwendung erfolgreich war. Der Einsatz von Tests zur Überprüfung des Builds und der Bereitstellung der Anwendung ermöglicht dem Team ein besseres Verständnis der Qualität und erlaubt ihm zu erkennen, wann eine kürzliche Änderung am Anwendungscode die SharePoint-Anwendung beeinträchtigt hat.
  
    
    
Abbildung 11 zeigt, welche Arten von Testansätzen für SharePoint-Anwendungsmodelle am besten geeignet sind.
  
    
    

**Abbildung 11. Testansätze**

  
    
    
 [![Tests der programmierten UI empfehlen sich für in SharePoint gehostete Anwendungen, bei denen sich die Geschäftslogik und die Benutzeroberfläche auf derselben Schicht befinden.](../images/ALMTestingTypes.png)
  
   
    
    
Abbildung 11 schlägt die Verwendung verschiedener Typen von Tests zum Testen von SharePoint-Anwendungen nach Typ vor. Kodierte UI-Tests sollten für in SharePoint gehostete Anwendungen verwendet werden, bei denen sich Geschäftslogik und Benutzeroberfläche auf der gleichen Ebene befinden. Geschäftslogik kann zwar in JavaScript-Bibliotheken abstrahiert werden, jedoch wird diese Logik vorrangig über die Benutzeroberfläche getestet.
  
    
    
In der Cloud (d. h. automatisch und vom Anbieter) gehostete Anwendungen können vollständig kodierte UI-Tests und auch Komponententests zur Überprüfung der Dienstkomponenten der Lösung verwenden. So kann der Entwickler aus einer funktionsbezogenen Perspektive Vertrauen in die Qualität der Implementierung der gehosteten Infrastruktur der Anwendung gewinnen.
  
    
    
Die folgenden Abschnitte enthalten die Überlegungen zu kodierten UI-Tests und anderen Testtypen im Hinblick auf SharePoint-Anwendungen.
  
    
    

#### <a name="client-side-code-and-coded-ui-tests"></a>Clientseitiger Code und kodierte UI-Tests
<a name="CodedUITests"> </a>

Für Buildüberprüfungstests sowie vollständige Systemtests werden kodierte UI-Tests empfohlen. Diese Tests basieren auf aufgezeichneten Aktionen, um nicht nur die Geschäftslogik und die mittlere Anwendungsebene, sondern auch die Benutzeroberfläche zu testen. Bei SharePoint-Anwendungen, die clientseitigen Code verwenden, können sich Einstiegspunkte und Ausführung der Geschäftslogik größtenteils in der Benutzeroberflächenebene befinden. Aus diesem Grund können kodierte UI-Tests nicht nur die Benutzeroberfläche, sondern auch die Geschäftslogik der Anwendung testen. Weitere Informationen zum kodierten UI-Test finden Sie unter  [Überprüfen von Code mithilfe der Benutzeroberflächenautomatisierung](http://msdn.microsoft.com/de-DE/library/dd286726.aspx).
  
    
    
Kodierte UI-Tests können in Von SharePoint gehostetes Add-Ins verwendet werden, bei denen Benutzeroberfläche und Geschäftslogik nicht getrennt sind. Diese Tests können wie andere Tests über eine Builddefinition in TFS ausgeführt werden, sodass sie die Funktionalität einer Anwendung nach der Bereitstellung (und nachdem der Anwendung von SharePoint vertraut wurde) überprüfen können.
  
    
    

#### <a name="non-coded-ui-tests"></a>Nicht kodierte UI-Tests
<a name="NonCodedUITests"> </a>

In Fällen, in denen sich die Anwendungslogik außerhalb der Benutzeroberflächenebene der Anwendung befindet, wie bei in der Cloud gehosteten Anwendungen, sollte eine Kombination aus kodierten und nicht kodierten UI-Tests verwendet werden. Tests wie herkömmliche Komponententests können verwendet werden, um die Buildqualität der Dienstlogik zu überprüfen, die in einer vom Anbieter gehosteten Infrastruktur implementiert wurde. Dadurch kann der Entwickler aus einer testbezogenen Perspektive umfassendes Vertrauen in das ordnungsgemäße Funktionieren der vom Anbieter gehosteten Komponenten gewinnen.
  
    
    

#### <a name="web-performance-and-load-tests"></a>Webleistungs- und Auslastungstests
<a name="LoadTests"> </a>

Durch Webleistungs- und Auslastungstests gewinnen Entwickler Vertrauen in das ordnungsgemäße Funktionieren der Anwendung unter erwarteten oder prognostizierten Benutzerlasten. Bei diesen Tests wird auch ermittelt, inwiefern die Anwendung gleichzeitig eine vorhersehbare Benutzerbasis verarbeiten kann, die mit der Zeit in angemessenem Umfang ansteigt. Sowohl kodierte Tests als auch Komponententests können als Quelle für den Webleistungs- und Auslastungstest dienen. Mithilfe einer ALM-Plattform wie TFS können diese Tests verwendet werden, um einen Auslastungstest für Ihre Anwendung durchzuführen.
  
    
    
Beachten Sie, dass das Testen der Infrastruktur nicht das vorrangige Ziel dieser Tests ist, wenn mit diesen SharePoint-Anwendungen getestet werden. Für die Infrastruktur, ob in SharePoint oder vom Anbieter gehostet, sollte ein ähnlicher Bezugswert für Auslastung und Leistung festgelegt werden. Die Webleistungs- und Auslastungstests für die Anwendung machen zwar Herausforderungen der Infrastruktur deutlich, sollten aber hauptsächlich als Methode zum Testen der Anwendungsleistung betrachtet werden.
  
    
    
Weitere Informationen zu Webleistungs- und Auslastungstests finden Sie unter  [Ausführen von Leistungstests für eine Anwendung vor der Veröffentlichung](http://msdn.microsoft.com/de-DE/library/vstudio/dn250793.aspx).
  
    
    

#### <a name="quality-and-testing-environments"></a>Qualität und Testumgebungen
<a name="TestingEnvironments"> </a>

Viele Organisationen besitzen mehrere Testumgebungen, die physisch oder virtuell und voneinander getrennt sein können. Diese Umgebungen können in Abhängigkeit vom ALM-Prozess eines Teams und von den rechtlichen Anforderungen oder einer Kombination dieser beiden Faktoren variieren. Um die Anzahl und die Typen von Testumgebungen zu ermitteln, die Teams verwenden sollten, wurden die folgenden Richtlinien auf Basis funktionsbezogener Praktiken erstellt, die sich speziell auf SharePoint-Anwendungen beziehen. Es sind aber auch ALM-Praktiken enthalten, die für Softwareentwicklung im Allgemeinen gelten.
  
    
    

#### <a name="developer-testing"></a>Entwicklertests
<a name="DevTesting"> </a>

Entwicklertests können in der Umgebung durchgeführt werden, in der die Entwickler ihre Komponente der Lösung erstellen. Zahlreiche Entwickler, die jeweils an verschiedenen Aspekten oder Komponenten einer größeren Anwendung arbeiten, führen jeweils Komponententests und kodierte UI-Tests durch und stellen den Anwendungscode in ihrer Entwicklungswebsite bereit.
  
    
    

**Abbildung 12. Prozess für Entwicklertests**

  
    
    
 [![Die Entwickler testen die auf ihrer Office 365-Entwicklerwebsite oder ihrer lokalen Entwicklerwebsite bereitgestellten Lösungskomponenten direkt über Visual Studio.](../images/ALMDeveloperTesting.png)
  
    
    
    
Entwickler führen Tests in Visual Studio mit den in ihrer eigenen Office 365-Entwicklerwebsite oder in der lokalen Entwicklerwebsite bereitgestellten Lösungskomponenten durch. Bei in der Cloud gehosteten Anwendungen werden die Tests in Visual Studio auch mit den Lösungskomponenten durchgeführt, die sich in vom Anbieter gehosteter Infrastruktur befinden. Diese Komponenten befinden sich im Microsoft Azure-Abonnement des Entwicklers.
  
    
    
Beachten Sie, dass bei diesem Ansatz davon ausgegangen wird, dass Entwickler einzelne Office 365-Entwicklerwebsites und Microsoft Azure-Abonnements besitzen, die durch MSDN-Abonnements bereitgestellt werden. Auch wenn Entwickler Anwendungen für die lokale Bereitstellung erstellen, können diese Entwicklerdienste für Entwicklung und Tests verwendet.
  
    
    
Wenn Entwickler diese Dienste nicht besitzen oder Entwicklungsarbeiten vollständig lokal durchführen müssen, führen sie Tests für ihre Komponenten mit der Entwicklungswebsitesammlung einer lokalen Farm und entwicklerspezifischer, vom Anbieter gehosteten Infrastruktur durch. Die vom Anbieter gehostete Infrastruktur kann sich in speziellen virtuellen Maschinen des Entwicklers befinden. Zur Entwicklung voll vertrauenswürdiger Lösungen benötigen Entwickler eine eigene virtuelle SharePoint-Farm und vom Anbieter gehostete Infrastruktur.
  
    
    

#### <a name="integration-and-systems-testing"></a>Integrations- und Systemtests
<a name="IntegrationTesting"> </a>

Um die Anwendung zu testen, sollten alle Entwicklungskomponenten in einer zentralen Umgebung zusammengeführt und bereitgestellt werden. Diese Integrationsumgebung bietet einen Ort, an dem Entwickler die von ihnen erstellten Komponenten der Lösung bereitstellen und beobachten können, wie sie mit anderen Lösungskomponenten interagieren, die von anderen Entwicklern geschrieben wurden.
  
    
    

**Abbildung 13. Integrationstestumgebung**

  
    
    
 [![TFS erstellt die SharePoint-Anwendung sowie alle erforderlichen Komponenten und stellt sie in den Zielumgebungen bereit.](../images/ALMIntegrationTesting.png)
  
    
    
Für Tests dieser Art erstellt die ALM-Plattform die SharePoint-Anwendung sowie alle erforderlichen Komponenten und stellt sie in den Zielumgebungen bereit. Im Fall von in SharePoint gehosteten Anwendungen ist das entweder eine Office 365-Website oder eine lokale/IaaS-basierte SharePoint-Websitesammlung, die speziell für Integrations- und Systemtests eingerichtet wurde. Im Fall von in der Cloud gehosteten SharePoint-Anwendungen stellt TFS die Komponenten außerdem in einem zentralisierten Microsoft Azure-Abonnement bereit, in dem die Dienste speziell für Integrations- und Systemtests konfiguriert werden. Anschließend führt TFS die Tests der programmierten UI und die Komponententests für die SharePoint-Anwendungen sowie für alle Komponenten aus, die die Lösung in der gehosteten Infrastruktur benötigt.
  
    
    

#### <a name="uat-and-qa-testing"></a>Benutzerakzeptanztests und Qualitätssicherungstests
<a name="UATTesting"> </a>

Für Benutzerakzeptanztests haben Organisationen oft separate Umgebungen, in denen diese Tests getrennt von Integrations- und Systemtests durchgeführt werden. Eine Trennung dieser Testumgebung verhindert, dass automatisierte fortlaufende Freigaben und Tests Benutzerakzeptanztests beeinträchtigen, wobei Benutzer über einen längeren Zeitraum Tests mit einem speziellen Build der Anwendung durchführen.
  
    
    

**Abbildung 14. Benutzerakzeptanztests**

  
    
    
 [![Benutzer, die Abnahmetests zugewiesen sind, oder organisatorische Testressourcen führen Testskripts in einer stabilen Umgebung aus, die auf eine allgemein veröffentlichte Buildversion der Anwendung abzielt.](../images/ALMUATTesting.png)
  
    
    
    
Wie in Abbildung 14 gezeigt, führen Benutzer, die mit der Durchführung von Akzeptanztests oder Testressourcen der Organisation beauftragt wurden, Testskripts in einer stabilen Umgebung aus, die auf einen umfassend veröffentlichten Build der Anwendung konzentriert ist. Codebereitstellung und Tests werden zwar in der Integrationsumgebung fortgeführt, doch Benutzer führen manuelle Tests durch, um zu überprüfen, ob die Anwendung die erforderlichen Verwendungs- und Testfälle erfüllt. Die Anwendung und jegliche vom Anbieter gehostete Infrastruktur werden - normalerweise von einem Versions-Manager - in dieser Testumgebung bereitgestellt. Auch eine automatisierte Bereitstellung ist möglich. Diese Art von Bereitstellung verwendet in TFS eine spezielle Builddefinition für Benutzerakzeptanztests, die derjenigen entspricht, welche die Bereitstellung für die Integrations- und Systemtestumgebung durchführt.
  
    
    
Bei in der Cloud gehosteter Infrastruktur ist eine Bereitstellung in einem Microsoft Azure-Abonnement möglich, das auch von der Integrations- und Systemtestumgebung verwendet wird, wenn die Dienste so benannt und konfiguriert sind, dass sie nebeneinander als verschiedene Dienste oder Datenbanken bereitgestellt werden können. Dieser Ansatz bietet eine Reihe von Diensten und Datenbanken im Microsoft Azure-Testabonnement für Integrations- und Systemtests sowie Benutzerakzeptanz und QA-Tests (siehe Abbildung 15).
  
    
    

**Abbildung 15. Integrations- und Benutzerakzeptanztests**

  
    
    
 [![Die Bereitstellung in einem mit der Integrations-/Systemtestumgebung gemeinsam genutzten Microsoft Azure-Abonnement ist möglich, wenn die Dienste so benannt und konfiguriert werden, dass sie als verschiedene Dienste oder Datenbanken parallel bereitgestellt werden können.](../images/ALMIntegrationandUAT.png)
  
   
    
    

#### <a name="code-promotion-practices"></a>Methoden für die Codeheraufstufung
<a name="CodePromotion"> </a>

Der Prozess des Heraufstufens von Code zwischen den Entwicklungs- und Testumgebungen sowie der Produktionsumgebung sollte mithilfe eines klar definierten Releaseverwaltungsprozesses erfolgen. Abbildung 16 zeigt, wie Entwickler ihre Lösungskomponenten in Entwicklungsumgebungen bereitstellen, um Komponententests durchzuführen.
  
    
    

**Abbildung 16. Releaseverwaltungsprozess**

  
    
    
 [![Nach dem Einchecken in TFS wird die Lösung in einem automatisierten Buildverfahren kompiliert und in der Zielumgebung bereitgestellt. Dabei werden im Rahmen der Builddefinition in TFS Buildüberprüfungstests ausgeführt.](../images/ALMCodePromotion.png)
  
   
    
    
Im Anschluss an das Einchecken bei TFS stellt ein automatisiertes Buildverfahren die Lösung zusammen und stellt sie in der Zielumgebung für Integrations- und Systemtests bereit, wo Buildüberprüfungstests als Bestandteil der Builddefinition in TFS ausgeführt werden. Dieser Ansatz umfasst die Bereitstellung der vom Anbieter gehosteten Komponenten der Lösung in der Zielumgebung (Microsoft Azure oder lokale Umgebungen). Beachten Sie, dass bei Microsoft Azure-Infrastruktur für Integrations- und Systemtests sowie Benutzerakzeptanz- und QA-Tests das gleiche Microsoft Azure-Abonnement verwendet werden kann, vorausgesetzt, dass diese in unterschiedlichen Namespaces und eigenen SQL-Datenbanken bereitgestellt werden.
  
    
    
Ein Versions-Manager oder eine separate TFS-Build-Definition, die in den meisten Fällen manuell aufgerufen wird, kann Komponenten in der Umgebung für Benutzerakzeptanz- und QA-Tests bereitstellen. Mit diesem Ansatz lässt sich die Buildversion steuern, mit der Benutzer testen. Versions-Manager können die Builds von einer TFS-Freigabe herunterladen und den Bereitstellungsprozess selbst ausführen. Von der Heraufstufung bis zur Produktion ist die Releaseverwaltung an der Bereitstellung der Anwendung in der Produktionsumgebung und der Überwachung der Installation und der Buildüberprüfung durch Tests beteiligt.
  
    
    

## <a name="application-patching-and-upgrades"></a>Patches und Upgrades für Anwendungen
<a name="AppPatching"> </a>

Microsoft hat für Anwendungsentwickler dedizierte Richtlinien für Anwendungsupgrades formuliert. Mit der SharePoint-Plattform können Anwendungen so konfiguriert werden, dass Benutzer über die Verfügbarkeit neuer Anwendungsversionen informiert werden.
  
    
    
Was Sie bei der Ausarbeitung der Upgrade- und Patchingstrategie für Ihre SharePoint-Anwendung beachten sollten, können Sie unter [Aktualisieren von Add-Ins für SharePoint](http://msdn.microsoft.com/library/3edcb33c-fa9e-4e9e-82d6-5519fd981324%28Office.15%29.aspx) nachlesen.
  
    
    
Für Änderungen an Anwendungen entspricht das Muster, dessen Befolgung empfohlen wird, vorhandenen Mustern für Codeentwicklung und Sustained Engineering. Dazu zählen eindeutiges Verzweigen und Zusammenführen für Programmfehlerbehebungen und Featureentwicklung sowie inkrementelle Bereitstellungen in Zielanwendungskatalogen. Die obige Anleitung kann verwendet werden, um Änderungen an Anwendungen für SharePoint durchzuführen und diese in Zielanwendungskatalogen oder dem Store bereitzustellen.
  
    
    
Die Informationen in  [Aktualisierungsverfahren für Add-Ins für SharePoint](http://msdn.microsoft.com/library/3dba209d-cb98-4e5d-b4b2-fad31e667ca1%28Office.15%29.aspx) bieten zusätzliche taktische Anleitungen zu den Aktualisierungsverfahren für SharePoint-Anwendungen. Dazu zählt die Beschleunigung von Entwicklungstests durch die Verkürzung des Zyklus, in dem Anwendungsupdates in der Farm in Testumgebungen übernommen werden. Darüber hinaus bietet dieser Artikel Anleitungen dazu, wie Sie in verschiedenen Anwendungsbereitstellungsmodellen den Status berücksichtigen.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [Einrichten des Team Foundation-Builddiensts](http://msdn.microsoft.com/de-DE/library/vstudio/ee259687.aspx)
    
  
-  [Verwenden einer Office 365 SharePoint-Website, um vom Anbieter gehostete Add-Ins auf einer lokalen SharePoint-Website zu autorisieren](http://msdn.microsoft.com/library/2f65ba3f-b246-4064-b4fb-ad18399d387a%28Office.15%29.aspx)
    
  
-  [Übersicht über die SharePoint-Entwicklung](sharepoint-development-overview.md)
    
  
-  [Was ist das Open Data Protocol?](http://www.odata.org/)
    
  
-  [Das OAuth 2.0-Autorisierungsframework](http://oauth.net/)
    
  

  
    
    

