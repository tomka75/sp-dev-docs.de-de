---
title: "SharePoint-Add-Ins im Vergleich mit SharePoint-Lösungen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0e9efadb-aaf2-4c0d-afd5-d6cf25c4e7a8
ms.openlocfilehash: 3d441639ab0ec465ad6bc7309c4e9ac4e45d59d2
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-add-ins-compared-with-sharepoint-solutions"></a>SharePoint-Add-Ins im Vergleich mit SharePoint-Lösungen
Erfahren Sie, wann Sie Ihre SharePoint-Erweiterung als SharePoint-Add-In, als SharePoint-Farmlösung oder als codelose Sandkastenlösung entwickeln sollten.
    

In diesem Artikel werden Anwendungsfälle für SharePoint-Add-Ins, Farmlösungen und codelose Sandkastenlösungen (NCSSs) verglichen.
- Neue SharePoint-Add-Ins sind eigenständige Erweiterungen, die möglicherweise cloudbasierte Logik und Daten, SharePoint-Komponenten und clientseitige Skripts, aber keinen benutzerdefiniert verwalteten Code enthalten, der auf SharePoint-Servern ausgeführt wird. Sie werden entweder über den Office Store oder den Add-In-Katalog einer Organisation installiert und können auf lokalen Farmen oder Microsoft SharePoint Online installiert werden. Eine Übersicht über SharePoint-Add-Ins finden Sie unter  [SharePoint-Add-Ins]((http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)).
    
  
- SharePoint-Farmlösungen sind Pakete mit SharePoint-Komponenten. Sie werden in einen farmweiten Katalog hochgeladen, aus dem sie installiert werden können. Sie können nicht über den Office Store verteilt werden und lassen sich nicht unter SharePoint Online installieren. Sie dürfen benutzerdefinierten verwalteten Code enthalten, der auf den Servern der SharePoint-Farm ausgeführt wird. Weitere Informationen zu den Grundlagen von Farmlösungen finden Sie unter[Übersicht über Lösungen]((http://msdn.microsoft.com/library/1983cab9-4b29-494a-a62a-0f8e83908744%28Office.15%29.aspx)) sowie unter [Farmlösungen in SharePoint 2010]((http://msdn.microsoft.com/library/845f7524-b9ff-412b-aa29-3afacda91100%28Office.15%29.aspx)).
    
  
- NCSSs sind ebenfalls Pakete mit SharePoint-Komponenten, werden aber an einen Websitesammlungskatalog hochgeladen, aus dem sie installiert werden können. Sie können entweder auf lokalen Farmen oder auf SharePoint Online installiert, aber nicht über den Office Store verteilt werden. Sie können nahezu dieselbe Art von beschreibenden Komponenten wie SharePoint-Add-Ins beinhalten und, wie Add-Ins, über JavaScript verfügen, enthalten aber keinen benutzerdefinierten verwalteten Code, der auf den SharePoint-Servern ausgeführt wird. Unterschiede in den Bereitstellungssystemen von Add-Ins und NCSSs bedingen, dass NCSSs für einige wenige Szenarien die bessere Bereitstellungsoption sind. Informationen zu Sandkastenlösungen finden Sie unter  [Übersicht über Sandkastenlösungen (SharePoint Server 2010)](https://technet.microsoft.com/en-us/library/ee721992%28v=office.14%29.aspx).
    
  

> **Wichtig:** Die Entwicklung von Sandkastenlösungen, die ausschließlich deklaratives Markup und JavaScript enthalten (codelose Sandkastenlösungen, NCSS [No-Code Sandboxed Solutions), wird weiterhin unterstützt. Nicht länger unterstützt wird jedoch die Verwendung von benutzerdefiniertem verwalteten Code in Sandkastenlösungen. Als Ersatz für Szenarien, die verwalteten Code erfordern, haben wir das neue SharePoint-Add-In-Modell eingeführt. Das Add-In-Modell entkoppelt das SharePoint-Kernprodukt von der Add-In-Laufzeit. Dadurch sind Sie flexibler und können den Code in der Umgebung Ihrer Wahl ausführen. Uns ist bewusst, dass unsere Kunden bereits in codebasierte Sandkastenlösungen investiert haben, und wir werden dies bei der Einstellung dieser Lösungen entsprechend berücksichtigen. Bereits vorhandene codebasierte Sandkastenlösungen lassen sich bis auf Weiteres wie gewohnt in lokalen SharePoint-Farmen nutzen. Angesichts der Dynamik von Onlinediensten werden wir zukünftig ausgehend von der Kundennachfrage entscheiden, ob wir Unterstützung für codebasierte Sandkastenlösungen in SharePoint Online implementieren. Codelose Sandkastenlösungen (NCSS) werden weiterhin unterstützt werden. Unser Entwicklungsschwerpunkt wird jedoch zukünftig darauf liegen, das neue SharePoint-Add-In-Modell leistungsfähiger und funktionsreicher zu machen. Daher empfehlen wir Ihnen, für alle neuen Entwicklungsprojekte wann immer möglich das neue Add-In-Modell zu verwenden. In Szenarien, in denen Sie eine Farmlösung oder codebasierte Sandkastenlösung entwickeln müssen, empfehlen wir die Wahl eines Designs, das sich unkompliziert an ein stärker entkoppeltes Entwicklungsmodell anpassen lässt. 
  
    
    


## <a name="develop-an-add-in-whenever-you-can"></a>Entwickeln Sie wann immer möglich Add-Ins.
<a name="AppWhenYouCan"> </a>

Unser wichtigster Ratschlag ist, wann immer möglich ein SharePoint-Add-In anstelle einer Farmlösung oder NCSS zu entwickeln. SharePoint-Add-Ins haben im Vergleich zu klassischen Lösungen die folgenden Vorteile:
  
    
    

- Einfachster Such-, Erwerbs- und Installationsprozess für Benutzer
    
  
- Sicherste SharePoint-Erweiterungen für Administratoren
    
  
- Einfachstes Marketing- und Vertriebssystem auf der Basis eines Microsoft Online Add-In Stores
    
  
- Maximale Flexibilität bei der Entwicklung zukünftiger Upgrades
    
  
- Maximale Nutzung Ihrer vorhandenen Nicht-SharePoint-Programmierkenntnisse
    
  
- Integration cloudbasierter Ressourcen auf reibungslosere und flexiblere Weise
    
  
- Festlegen von Berechtigungen für Ihre Erweiterung, die sich von den Berechtigungen des Benutzers unterscheiden, der das Add-In ausführt
    
  
- Verwendung von plattformübergreifenden Standards wie HTML, REST, OData, JavaScript und OAuth
    
  
- Nutzung der domänenübergreifenden SharePoint-JavaScript-Bibliothek für den Zugriff auf SharePoint-Daten oder alternative Verwendung eines von Microsoft bereitgestellten, mit OAuth kompatiblen sicheren Tokendiensts oder Benutzung digitaler Zertifikate, um die Autorisierung für SharePoint-Daten zu erhalten
    
  

## <a name="design-add-ins-or-ncsss-for-end-users-and-design-farm-solutions-for-administrators"></a>Entwerfen von Add-Ins oder NCSSs für Endbenutzer und Entwerfen von Farmlösungen für Administratoren
<a name="SPAppVsClassic_Overview"> </a>

SharePoint-Add-Ins und NCSSs verwenden eins der SharePoint-Clientobjektmodelle oder einen der REST-Endpunkte, um auf SharePoint-Inhalte und -Komponenten zuzugreifen. Diese Client-APIs ermöglichen SharePoint-Erweiterungen, die auf Endbenutzer ausgelegt sind. („Endbenutzer" sind in diesem Kontext Administratoren von Websitesammlungen, Websitebesitzer und Websitemitglieder.) Das Serverobjektmodell bietet zusätzliche APIs, die programmatische Erweiterungen der Verwaltung, Konfiguration und Sicherheit von SharePoint ermöglichen. Dazu zählen Erweiterungen der Zentraladministration, benutzerdefinierte Windows PowerShell-Befehle, Zeitgeberaufträge und benutzerdefinierte Sicherungen. Weitere Informationen zu der Art von administrativen Erweiterungen, die Sie entwickeln können, finden Sie unter  [SharePoint Foundation-Administration]((http://msdn.microsoft.com/library/cdcc1b8a-4144-446f-b471-03d4a754a8ab%28Office.15%29.aspx)). Diese administrativen Erweiterungen werden in SharePoint-Features auf Farm-, Webanwendungs- oder Websitesammlungsebene bereitgestellt. SharePoint-Farmlösungen werden zudem von Farmadministratoren installiert, während Add-Ins und NCSSs von Administratoren von Mandanten und Websitesammlungen installiert werden können.
  
    
    
Das Serverobjektmodell bietet APIs für Vorgänge zum Erstellen, Lesen, Aktualisieren und Löschen (CRUD-Vorgänge) in Listen, Bibliotheken und Websites sowie für Vorgänge in anderen SharePoint-Komponenten. Das bedeutet, dass das Serverobjektmodell für Erweiterungen verwendet werden kann, die für Endbenutzer vorgesehen sind. Aber aus den im vorherigen Abschnitt erwähnten Gründen sind Farmlösungen für gewöhnlich nicht die beste Wahl für solche Erweiterungen. Daher ist es nicht überraschend, dass Farmlösungen nicht auf Microsoft SharePoint Online installiert werden können. Da Microsoft die gesamte Verwaltung von SharePoint Online übernimmt, sind keine administrativen Erweiterungen erforderlich. Weitere Informationen zu den verschiedenen API-Sätzen in SharePoint und den Überlappungen zwischen diesen finden Sie unter  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    
Die Clientobjektmodelle und REST-Endpunkte sind keine Duplizierung der verwaltungsorientierten APIs des Serverobjektmodells. Darüber hinaus können Sie diese administrativen APIs nicht aufrufen, da weder eine SharePoint-Add-In noch eine NCSS benutzerdefinierten Code enthalten kann, der auf den SharePoint-Servern ausgeführt wird. Zusätzlich müssen alle Features in SharePoint-Add-Ins über den Websitebereich und Features in NCSSs entweder den Websitesammlungs- oder Websitebereich verfügen. Daher ist eine verwaltungsorientierte SharePoint-Erweiterung mit einer SharePoint-Add-In oder einer NCSS nicht wirklich möglich. Das zweite Prinzip, aber keine absolute Regel, ist also, dass Add-Ins und NCSSs für Endbenutzer und Farmlösungen für Administratoren vorgesehen sind.
  
    
    

## <a name="design-ncsss-for-branding-and-template-like-extensions"></a>Entwerfen von NCSSs für Branding und vorlagenartige Erweiterungen
<a name="SPAppVsClassic_Overview"> </a>

Möglicherweise treffen Sie auf eines der geringen Anzahl von SharePoint-Entwicklungsszenarien, für die das Add-In-Modell nicht gut geeignet ist, das Sie aber auch nicht mit einer Farmlösung implementieren können, vielleicht weil die Lösung in SharePoint Online oder von einem Websitesammlungsadministrator installierbar sein muss. Es gibt zwei breite und überlappende Kategorien für derartige Szenarien.
  
    
    

- **Branding:** SharePoint-Benutzer möchten das Design ihrer SharePoint-Websites und SharePoint Online-Websites häufig individuell anpassen, mit eigenen Farben, Formatvorlagen, Layouts und Logos. Das lässt sich im Allgemeinen leichter mit NCSS umsetzen als mit SharePoint-Add-Ins. SharePoint-Add-Ins können lediglich die Darstellung ihres eigenen Add-In-Webs deklarativ steuern. Zum Hostweb können sie deklarativ lediglich Menüband-Schaltflächen und Menüelemente (sowie Add-In-Parts) hinzufügen. Alle anderen Änderungen am Hostweb oder der übergeordneten Websitesammlung, dem Mandanten oder der lokalen SharePoint-Webanwendung müssen mittels Code oder Skript umgesetzt werden. Dabei muss eines der SharePoint-Clientobjektmodelle verwendet werden. Neue Symbole oder CSS-Dateien beispielsweise müssten programmgesteuert bereitgestellt werden. Dieser Code könnte vom Add-In selbst ausgeführt werden, nachdem es installiert wurde, oder im Ereignishandler für die Add-In-Installation. Allerdings wäre die Erstellung dieses Codes sehr arbeitsintensiv. Darüber hinaus würde das Add-In zur Änderung von Websites außerhalb seines eigenen Web und Hostweb Berechtigungen benötigen, die für die gesamte Websitesammlung gelten. Soll es mehr als nur seine übergeordnete Websitesammlung ändern können, bräuchte es Berechtigungen, die für den gesamten Mandaten gelten. Eine NCSS mit Branding lässt sich jedoch in jeder Websitesammlung bereitstellen und aktivieren und könnte lediglich einige rein deklarative Komponenten enthalten. 
    
    > [!NOTE]
    > SharePoint-Farmlösungen eignen sich für Brandingzwecke potenziell besser als NCSS oder SharePoint-Add-Ins, stehen aber in SharePoint Online nicht zur Verfügung. 

- **„Vorlagenartige" Erweiterungen:** Nehmen wir an, Sie müssen eine Krisenmanagementerweiterung für SharePoint für die gemeinsame Analyse und Lösung von Geschäftskrisen erstellen. Ihre Erweiterung enthält einige benutzerdefinierte Listentypen, codelose Workflows und andere SharePoint-Komponenten, die alle in einer benutzerdefinierten Webvorlage kombiniert sind. Nehmen wir weiterhin an, Sie beschließen, die Erweiterung als NCSS zu packen und bereitzustellen. Nachdem das Feature in der Lösung aktiviert wurde, können Benutzer ein Unterweb für das Krisenmanagement ihrer SharePoint-Website erstellen, wann immer es zu einer Krise kommt. Sie können die Website mit speziell für die Krise relevanten Daten füllen. Andererseits könnten Sie dieselbe Erweiterung als SharePoint-Add-In implementieren und dabei exakt dieselbe Sammlung von SharePoint-Komponenten verwenden. Wenn das Add-In auf der Teamwebsite installiert ist, wird das Unterweb (das als „Add-In-Web" bezeichnet wird) sofort erstellt. Auch hier füllen Benutzer die Website mit relevanten Daten.
    
    Was geschieht jetzt aber, wenn es zu einer zweiten Krise kommt? Wenn Sie die Erweiterung als NCSS implementiert haben, können Ihre Benutzer lediglich ein weiteres Unterweb aus Ihrer benutzerdefinierten Webvorlage erstellen. Wenn die Erweiterung jedoch als SharePoint-Add-In implementiert wurde, haben seine Benutzer ein Problem. Sie können keine zweite Instanz des gleichen Add-Ins auf der übergeordneten Website installieren. In einem Hostweb kann nur eine Instanz eines Add-Ins installiert werden. Das Beste, was Sie tun können, ist die Erstellung eines Unterwebs der übergeordneten Website, das dann als Standort für eine weitere Instanz des zu installierenden Add-Ins dient. Wenn das Add-In installiert ist, wird ein neues Add-In-Web, das ein Unter-Unterweb der übergeordneten Website ist, für die Add-In-Komponenten erstellt. Dieser Vergleich zeigt ein allgemeines, aber nicht absolutes Prinzip: SharePoint-Erweiterungen, die eine „vorlagenartige" Eigenschaft haben - das heißt, eine wiederverwendbare Sammlung von Komponenten, die für jeden speziellen Anwendungsfall konfiguriert werden muss, natürlicherweise aber über mehrere Instanzen verfügt, die mit derselben SharePoint-Website verbunden sind - passen besser zum NCSS-Bereitstellungsmodell als zum Add-In-Modell. In diesem Beispiel ist das variable Element die Krise, aber Sie können sich leicht vorlagenartige SharePoint-Erweiterungen vorstellen, in denen sich die Instanzen nach Region, Datum oder beliebigen anderen Eigenschaften unterscheiden.
    
  
Informationen zum Erweitern der Möglichkeiten von SharePoint-Add-Ins finden Sie unter  [Konservativer Einsatz von Add-In-Ereignishandlern](#AppEventHandlers) und [Add-Ins, die Erweiterungen erstellen](#ExtensionFactories).
  
    
    

## <a name="doing-things-the-add-in-way"></a>Add-In-gerechte Lösungen für Funktionen
<a name="Questions"> </a>

Wie bereits erwähnt, ist benutzerdefinierter Code, der auf den SharePoint-Servern ausgeführt wird, in SharePoint-Add-Ins nicht zulässig. Das ist  *keine*  bedeutende Einschränkung, sondern heißt einfach, dass Ihre benutzerdefinierte Geschäftslogik entweder „nach unten" zum Clientgerät oder „nach oben" in die Cloud verschoben wird. In jedem Fall können Sie den [SharePoint-REST-/OData-Dienst]((http://msdn.microsoft.com/library/f60ed19e-9840-4f39-911e-4676751a2f6b%28Office.15%29.aspx)) verwenden, um auf SharePoint-Websites, Listen und andere Daten zuzugreifen. Auch ein Remotezugriff auf SharePoint-Daten ist über die [SharePoint-JavaScript-, Silverlight- oder .NET Framework-Clientobjektmodelle]((http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx)) möglich. Auf Windows Phones schließlich erfolgt der Zugriff auf SharePoint über das SharePointWindows Phone-Objektmodell. Weitere Informationen zu den verschiedenen API-Sätzen in SharePoint finden Sie unter [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    
Ein ähnlicher Punkt ist, dass Features in SharePoint-Add-Ins keinen Websitesammlungs-, Webanwendungs- oder Farmbereich haben können. Dennoch müssen Sie nicht auf Benutzeroberflächenenelemente oder -funktionalität verzichten. Das bedeutet, dass die Implementierung der Komponente aus SharePoint heraus auf einen Client oder in eine Remotewebanwendung oder Remotedatenbank verschoben wird.
  
    
    
In der folgenden Tabelle sind die SharePoint-Komponenten aufgeführt, die nicht in einem SharePoint-Add-In bereitgestellt werden können. Außerdem wird beschrieben, wie Sie dieselbe Funktionalität auf „Add-In-gerechte Weise" erhalten können.
  
    
    


|**Wenn Sie die folgende Funktionalität haben möchten ...**|**... probieren Sie die folgenen Ansätze aus.**|
|:-----|:-----|
|Benutzerdefinierte Webparts  <br/> |Ein SharePoint-Add-In kann über Remoteseiten verfügen, die benutzerdefinierte Webparts enthalten. Eine weitere Option besteht darin, eine Seite von einer Remotewebanwendung in einem Add-In-Webpart auf einer SharePoint -Websiteseite bereitzustellen. Die Remoteseite kann im Wesentlichen über dieselben Benutzeroberflächen-Steuerelemente und -funktionen verfügen wie ein Webpart. Weitere Informationen finden Sie unter  [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In]((http://msdn.microsoft.com/library/a2664289-6c56-4cb1-987a-22367fad55eb%28Office.15%29.aspx)).<br/> |
|Ereignis- und Funktionsempfänger  <br/> |Ein SharePoint-Add-In kann funktional äquivalente Remoteereignisempfänger enthalten. Weitere Informationen finden Sie unter  [Behandeln von Ereignissen in SharePoint-Add-Ins]((http://msdn.microsoft.com/library/c050d056-8548-4496-a053-016779d723d9%28Office.15%29.aspx)).<br/> |
|Benutzerdefinierte Feldtypen (Spaltentypen)  <br/> |Ein Add-In kann ein neues Feld (Spalte) bereitstellen, das auf einem der  [vorhandenen Feldtypen]((http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfieldtype.aspx%28Office.15%29.aspx)) basiert. Die Feldtypen [Calculated]((http://msdn.microsoft.com/library/8703373d-bb55-4132-8c5f-37a41c383f81%28Office.15%29.aspx)) und [Computed]((http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.spfieldcomputed.aspx%28Office.15%29.aspx)) sind besonders flexibel. Eine weitere Option besteht darin, Ihre Daten auf einer Remotewebseite darzustellen, indem Sie benutzerdefinierte Steuerelemente oder Raster verwenden<br/> |
|Benutzerdefinierte Webdienste, die im SharePoint  [Service Application Framework]((http://msdn.microsoft.com/library/6d0300d2-5b5c-4477-a9e2-17594aea5a7d%28Office.15%29.aspx)) integriert sind <br/> |Sie können Ihre benutzerdefinierten Webdienste als Remotedienste entwickeln.  <br/> |
|Anwendungsseiten  <br/> |Ein SharePoint-Add-In kann Remotewebseiten enthalten, die von jeder Website verfügbar sind, auf der das Add-In installiert ist. Ein Add-In kann außerdem beliebige der integrierten SharePoint-Webparts auf Websiteseiten verwenden.  <br/> |
   
Einige SharePoint-Komponenten, die unten aufgelistet sind, werden in Endbenutzerszenarien verwendet, haben aber keine Entsprechung im SharePoint-Add-In-Modell und können nicht in NCSSs bereitgestellt werden. Für diese müssen Sie Farmlösungen verwenden.
  
    
    

- **Benutzerdefinierte Websitedefinitionen** Benutzerdefinierte Webvorlagen, die funktionell Websitedefinitionen ähneln, sind in NCSSs und SharePoint-Add-Ins jedoch verfügbar. Weitere Informationen finden Sie unter [Websitetypen: WebTemplates und Websitedefinitionen]((http://msdn.microsoft.com/library/1edf6d4d-eddb-4cb5-9034-ed394e8a3e01%28Office.15%29.aspx)).
    
  
- **Stellvertretungs-Steuerelemente** Weitere Informationen finden Sie unter [Stellvertretungs-Steuerelement (Erstellen von Vorlagen für Steuerelemente)]((http://msdn.microsoft.com/library/e979328d-4985-4ed6-9085-7ff32a998dfc%28Office.15%29.aspx)).
    
  
- **Benutzerdefinierte Designs**
    
  
- **Benutzerdefinierte Aktionsgruppen und benutzerdefiniertes Ausblenden von Aktionen**
    
  
- **Benutzersteuerelemente (.ascx-Dateien)** Diese sind tatsächlich in keinem Szenario erforderlich.
    
  

### <a name="use-add-in-event-handlers-conservatively"></a>Konservativer Einsatz von Add-In-Ereignishandlern
<a name="AppEventHandlers"> </a>

Sie können einige der Einschränkungen von SharePoint-Add-Ins überwinden, indem Sie Handler für das Installationsereignis, das Updateereignis und das Deinstallationsereignis von Add-Ins erstellen. Diese Handler sind Webdienste, die auf Webservern außerhalb der SharePoint-Farm, möglicherweise in der Cloud, gehostet werden. Sie können das SharePoint-Clientobjektmodell oder die REST-APIs verwenden, um CRUD-Vorgänge bei SharePoint-Komponenten durchzuführen, einschließlich der Komponenten im Hostweb. Theoretisch könnten Sie solche Handler verwenden, um einige Bereitstellungseinschränkungen in den **Branding-** und **vorlagenartigen Erweiterungselementen** zu überwinden, die zuvor dargestellt wurden. Sie sollten solche Handler jedoch nur als letztes Mittel verwenden, wenn keinerlei andere Möglichkeit vorhanden ist, Kunden die Funktionalität bereitzustellen, die in Ihrem Anwendungsfall erforderlich ist. Bedenken Sie Folgendes bei der Entscheidung, ob Sie einen Handler erstellen sollten:
  
    
    

- Für die programmgesteuerte Bereitstellung an das Hostweb muss das Add-In Vollzugriff auf das Hostweb anfordern. Add-Ins, die diese Berechtigungsstufe benötigen, können nicht über den Office Store verkauft werden.
    
  
- Die Bereitstellung von Komponenten an das Hostweb untergräbt oft die Sicherheitsvorteile, die es mit sich bringt, wenn Sie SharePoint-Komponenten in ein Add-In-Web mit einer eigenen Domäne stellen.
    
  
- Das Erstellen und Debuggen von umfangreichem Bereitstellungscode bedeutet im Vergleich mit dem beschreibenden Bereitstellungs-Markup, das für Add-In-Webkomponenten und in NCSSs verwendet werden kann, eine Menge Arbeit.
    
  
- Es gibt einige wichtige bewährte Methoden, die bei der Erstellung von Add-In-Ereignishandlern befolgt werden müssen. Ihr Code muss eine Rollback-Logik enthalten, um alle bisher durchgeführten Aktionen rückgängig machen zu können, wenn es zu einem Fehler kommt. Außerdem muss die SharePoint-Infrastruktur über den Fehler informiert werden, damit die Infrastruktur ein Rollback aller bisher von ihr durchgeführten Aktionen ausführen kann.
    
  
- Add-In-Ereignishandler sind mit der Art von SharePoint-Add-In, die als von SharePoint gehostet bezeichnet werden, nicht möglich.
    
  
Weitere Informationen zu Add-In-Ereignishandlern finden Sie im SDK-Knoten  [Behandeln von Ereignissen in SharePoint-Add-Ins]((http://msdn.microsoft.com/library/c050d056-8548-4496-a053-016779d723d9%28Office.15%29.aspx)). Informationen zur Rollback-Logik finden Sie im Abschnitt **Hinzufügen von Rollback-Logik zum Handler** des Themas [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins]((http://msdn.microsoft.com/library/0fa088c5-54c6-482c-84ed-51c4f77c4127%28Office.15%29.aspx)). Letzteres ist im Zusammenhang mit dem Add-In-Updateereignis geschrieben, aber die grundlegenden Prinzipien gelten für alle Add-In-Ereignishandler..
  
    
    

### <a name="add-ins-that-create-extensions"></a>Add-Ins, die Erweiterungen erstellen
<a name="ExtensionFactories"> </a>

Eine andere Möglichkeit, das SharePoint-Clientobjektmodell - oder seine REST-APIs - für die Lösung von Problemen bei der Komponentenbereitstellung mit SharePoint-Add-Ins zu verwenden, besteht darin, den CRUD-Code in das Add-In statt in einen Add-In-Ereignishandler einzufügen. Das Add-In wird dann zu einer Art Zuordnungsinstanz für einen benutzerdefinierten Erweiterungstyp. Ein in SharePoint gehostetes Add-In könnte beispielsweise das SharePoint-JavaScript-Objektmodell verwenden, um die Bereitstellung und andere CRUD-Vorgänge im Hostweb oder an anderen Stellen im Mandanten oder der Webanwendung durchzuführen. Ein weiteres Beispiel finden Sie im Abschnitt **Schnelle Einführung in die Remotebereitstellung** unter [Techniken für die Websitebereitstellung und Remotebereitstellung in SharePoint]((http://blogs.msdn.com/b/vesku/archive/2013/08/23/site-provisioning-techniques-and-remote-provisioning-in-sharepoint.aspx)). Hier wird beschrieben, wie ein vom Anbieter gehostetes SharePoint-Add-In verwendet wird, um eine Unterwebbereitstellung auf sehr ähnliche Weise wie die Unterwebbereitstellung von SharePoint durchzuführen. Allerdings müssen Sie quasi das Rad neu erfinden und viel Arbeit leisten, um eine Zuordnungsinstanz-SharePoint-Add-In zu erstellen. Darüber hinaus kann diese Art von Add-Innicht über den Office Store verkauft werden, da das Add-In einen Vollzugriff auf das Hostweb erfordert.
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Programmiermodelle in SharePoint](programming-models-in-sharepoint.md)
    
  
-  [Verwenden von Lösungen]((http://msdn.microsoft.com/library/0da0518c-24eb-48e0-89bd-21282fdeef94%28Office.15%29.aspx))
    
  

