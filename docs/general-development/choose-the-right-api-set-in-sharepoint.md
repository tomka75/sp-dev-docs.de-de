---
title: "Auswählen des richtigen API-Satzes in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f36645da-77c5-47f1-a2ca-13d4b62b320d
ms.openlocfilehash: 7d2fb4dadd47e19483ff22e93f0b990c41a75540
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="choose-the-right-api-set-in-sharepoint"></a>Auswählen des richtigen API-Satzes in SharePoint
Erfahren Sie mehr über die verschiedenen API-Gruppen, die in SharePoint bereitgestellt werden, einschließlich des Serverobjektmodells und der verschiedenen Clientobjektmodellen und des REST/OData-Webdiensts.
    
    

## <a name="factors-that-determine-which-api-set-to-use"></a>Faktoren, die bestimmen, welche API-Gruppe verwendet werden soll
<a name="Factors"> </a>

Sie können aus verschiedenen API-Gruppen wählen, um auf die SharePoint-Plattform zuzugreifen. Welche Sie verwenden sollten, hängt von folgenden Faktoren ab:
  
    
    

- **Der Anwendungstyp.** Zu den Möglichkeiten gehören u. a. folgende, sich nicht gegenseitig ausschließende Kategorien: eine SharePoint-Add-In, ein Webpart auf einer SharePoint-Seite, eine Silverlight-Anwendung, die auf einem Client-Computer oder einem Client-Mobilgerät ausgeführt wird, eine ASP.NET-Anwendung, die in SharePoint über ein IFrame-Element verfügbar ist, JavaScript, das auf einer SharePoint-Websiteseite ausgeführt wird, eine SharePoint-Anwendungsseite, eine Microsoft .NET Framework-Anwendung, die auf einem Client-Computer ausgeführt wird, ein Windows PowerShell-Skript und ein Zeitgeberauftrag, der auf einem SharePoint-Server ausgeführt wird.
    
  
- **Ihre vorhandenen Fachkenntnisse.** Überraschenderweise können Sie Anwendungen in SharePoint erstellen, ohne sich mit dem Programmieren in SharePoint beschäftigen zu müssen. Sie können direkt mit der SharePoint-Entwicklung beginnen, wenn Sie bereits versiert im Umgang mit folgenden Programmierungsmodellen sind:
    
  - JavaScript
    
  
  - ASP.NET
    
  
  - REST/OData
    
  
  - .NET Framework
    
  
  - Windows Phone
    
  
  - Silverlight
    
  
  - Windows PowerShell
    
  
- **Das Gerät, auf dem der Code ausgeführt wird.** Zu den Möglichkeiten gehört ein Server in der SharePoint-Farm, ein externer Server, wie z. B. ein Server in der Cloud, ein Client-Computer und ein Mobilgerät.
    
  
In diesem Thema erhalten Sie einen Überblick zu den verschiedenen API-Gruppen, die von SharePoint bereitgestellt werden. In Abbildung 1 ist dargestellt, welche API-Gruppen verwendet werden können, um eine der 13 allgemeinen SharePoint-bezogenen Anwendungen zu entwickeln. Bei vielen Anwendungen können Sie verschiedene APIs auswählen.
  
    
    

**Abbildung 1. Ausgewählte SharePoint-Erweiterungstypen und API-Gruppen in SharePoint**

  
    
    

  
    
    
![Mengendiagramm von API-Sätzen und SharePoint-App-Typen](../images/SharePointAPIsetsandselectedSharePointextensions.png)
  
    
    

  
    
    
In der folgenden Tabelle finden Sie Anleitungen dazu, welche API-Gruppen Sie für eine ausgewählte Liste allgemeiner SharePoint-Erweiterungsprojekte verwenden sollten. In den restlichen Abschnitten dieses Themas werden die verschiedenen API-Gruppen erläutert.
  
    
    


|**Wenn Sie diese Funktionen verwenden möchten...**|**... sollten Sie diese APIs einsetzen**|
|:-----|:-----|
|Erstellen Sie eine ASP.NET-Webanwendung, die Erstell-/Lese-/Aktualisier-/Lösch-Vorgänge über eine Firewall zu SharePoint-Daten oder externen Daten durchführt, die in SharePoint durch einen Microsoft Business Connectivity Services (BCS) externen Inhaltstyp dargestellt werden  <br/> |JavaScript-Clientobjektmodell  <br/> |
|Erstellen Sie eine ASP.NET-Webanwendung, die CRUD-Vorgänge zu SharePoint-Daten oder externen Daten durchführt, die in SharePoint durch einen externen BCS-Inhaltstyp dargestellt werden, SharePoint jedoch nicht über eine Firewall aufrufen müssen  <br/> |.NET Framework-Clientobjektmodell, Silverlight-Clientobjektmodell oder REST/OData-Endpunkte  <br/> |
|Erstellen Sie eine LAMP-Webanwendung, die CRUD-Vorgänge zu SharePoint-Daten oder externen Daten durchführt, die in SharePoint durch einen externen BCS-Inhaltstyp dargestellt werden  <br/> |REST/OData-Endpunkte  <br/> |
|Erstellen Sie eine Windows Phone-App, die CRUD-Vorgänge zu SharePoint-Daten durchführt  <br/> |Mobiles Clientobjektmodell  <br/> |
|Erstellen Sie eine Windows Phone-App, die den Microsoft-Pushbenachrichtigungsdienst verwendet, um das Mobilgerät über Ereignisse in SharePoint zu benachrichtigen  <br/> |Mobiles Clientobjektmodell und das Serverobjektmodell  <br/> |
|Erstellen Sie eine iOS- oder Android-App, die CRUD-Vorgänge zu SharePoint-Daten durchführt  <br/> |REST-/OData-Endpunkte  <br/> |
|Erstellen Sie eine .NET Framework-Anwendung, die CRUD-Vorgänge zu SharePoint-Daten durchführt  <br/> |.NET Framework-Clientobjektmodell  <br/> |
|Erstellen Sie eine Silverlight-Anwendung, die CRUD-Vorgänge zu SharePoint-Daten durchführt  <br/> |Silverlight-Clientobjektmodell  <br/> |
|Erstellen Sie eine HTML/JavaScript-Anwendung, die CRUD-Vorgänge zu SharePoint-Daten durchführt  <br/> |JavaScript-Clientobjektmodell  <br/> |
|Erstellen Sie eine Office-Add-In, die mit SharePoint funktioniert  <br/> |JavaScript-Clientobjektmodell  <br/> |
|Erstellen Sie einen benutzerdefinierten Windows PowerShell-Befehl  <br/> |Serverobjektmodell  <br/> |
|Erstellen eines Zeitgeberauftrags  <br/> |Serverobjektmodell  <br/> |
|Erstellen einer Erweiterung der Zentraladministration  <br/> |Serverobjektmodell  <br/> |
|Erstellen eines konsistenten Branding in einer ganzen SharePoint-Farm  <br/> |Serverobjektmodell  <br/> |
|Erstellen eines benutzerdefinierten Webparts, einer Anwendungsseite oder eines ASP.NET-Benutzersteuerelements  <br/> |Serverobjektmodell  <br/> **Wichtig:** Wenn sich die Funktion, die Sie Kunden anbieten möchten, nicht an der SharePoint-Verwaltung in einem breiteren Bereich als eine Websitesammlung orientiert, wird empfohlen, anstatt das Serverobjektmodell zu verwenden, ein SharePoint-Add-In zu erstellen, das eine ASP.NET-Remote-Webanwendung mit benutzerdefinierten Webparts und ggf. Benutzersteuerelementen umfasst. Weitere Informationen dazu finden Sie in den oberen beiden Zeilen dieser Tabelle.           |
   

## <a name="server-object-model"></a>Serverobjektmodell
<a name="ServerOM"> </a>

Die größte API-Gruppe befindet sich im Serverobjektmodell der verwalteten Klassen. Auf der SharePoint Foundation 2013-Ebene umfasst dieses Objektmodell Klassen und Elemente, mit denen die Programmsteuerung der Basiswebsite und der Listenstruktur von SharePoint Foundation erfolgen kann. Der Großteil dieser Klassen befindet sich im  [Microsoft.SharePoint](https://msdn.microsoft.com/library/Microsoft.SharePoint.aspx) -Namespace. Außerdem können Sie fast jede SharePoint Foundation-Komponente erweitern, indem Sie das Serverobjektmodell verwenden, dazu gehören auch Workflows, Warnungen, Webparts, Standardsuchen und Microsoft Business Connectivity Services (BCS). Das Serverobjektmodell umfasst außerdem umfangreiche API-Gruppen-Aktivierungserweiterungen der Verwaltung und des Sicherheitssystems von SharePoint Foundation, einschließlich Sicherung, Farmintegrität und Diagnose, Protokollierung, Farm- und Webanwendungsverwaltung, Upgrade, Bereitstellung, Zwischenspeicherung und Windows PowerShell-Anpassung.
  
    
    
Auf der SharePoint-Ebene werden noch viele weitere Klassen hinzugefügt, um die Programmierung von Enterprise Content Management (ECM), Benutzerprofilen, Taxonomien, der erweiterten Suche und weiterer Features von SharePoint zu ermöglichen.
  
    
    
Sie können  [LINQ to Objects](http://msdn.microsoft.com/de-DE/library/bb397919.aspx) verwenden, um jede **IEnumerable**-Sammlung im Speicher abzufragen, mit  [LINQ to SharePoint-Anbieter](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx) haben Sie jedoch die Möglichkeit, die Listen direkt in den SharePoint-Inhaltsdatenbanken abzufragen. Genau genommen ist dieser Anbieter nicht für die anderen in diesem Thema erläuterten API-Gruppen verfügbar; es gibt jedoch Möglichkeiten, LINQ-Syntax für den Großteil der anderen Gruppen zu verwenden.
  
    
    
Die Assemblys, die die integrierten serverseitigen Klassen definieren, sind im globalen Assemblycache jedes Servers installiert, wenn SharePoint installiert ist. Wenn Sie etwas für das Serverobjektmodell programmieren, werden Ihre Assemblys als Farmlösungen im globalen Assemblycache installiert.
  
> [!NOTE]
> Das Entwickeln von neuen Sandkastenlösungen für SharePoint ist eine veraltete Methode, die dem Entwickeln von SharePoint-Add-Ins gewichen ist. Sandkastenlösungen können jedoch weiterhin in Websitesammlungen in SharePoint installiert werden. Die Assemblys dieser Lösungen verbleiben im Paket, sofern sie nicht verwendet werden, ansonsten werden sie temporär in einem Ordner auf dem Server installiert. Weitere Informationen finden Sie unter [Wo werden Assemblys in Sandkastenlösungen bereitgestellt?](http://msdn.microsoft.com/library/dadbb20b-1bf7-442c-9eeb-bd9f01dbda45%28Office.15%29.aspx). 
  
    
    


### <a name="limitations-on-when-you-can-use-the-server-object-model"></a>Beschränkungen zum Verwenden des Serverobjektmodells

Die benutzerdefinierte Logik in SharePoint-Add-Ins wird immer "hinunter" bis zum Client oder "hinauf" zur Cloud verteilt (oder "hinüber" zu einem Server außerhalb der SharePoint-Farm). In all diesen Verteilungsmodellen muss eines der Clientobjektmodelle oder die die REST/OData-Endpunkte verwendet werden. (Sie können das Serverobjektmodell nicht in einer SharePoint-Add-In verwenden). Wenn die App beispielsweise von SharePoint gehostete Seiten enthält, können diese Seiten auf SharePoint-Daten zugreifen, indem Sie das JavaScript-Clientobjektmodell verwenden. Diese Seiten können auch Silverlight-Anwendungen verfügbar machen, die das SharePoint Silverlight-Clientobjektmodell verwenden. Weitere Informationen über SharePoint-Add-Ins finden Sie unter  [Wichtige Aspekte der Architektur und Entwicklungslandschaft von Add-Ins für SharePoint](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx).
  
    
    

## <a name="client-object-models-for-managed-code"></a>Clientobjektmodelle für verwalteten Code
<a name="ClientManagedOM"> </a>

SharePoint verfügt über drei Clientobjektmodelle für verwalteten Code: .NET, Silverlight und Mobil.
  
    
    

### <a name="net-client-object-model"></a>.NET-Clientobjektmodell

Das SharePoint-Objektmodell für .NET Framework wird in .NET Framework-Anwendungen verwendet, die auf einem Windows-Client (kein Telefon) ausgeführt werden. Folgende Clients gehören zu dieser Gruppe:
  
    
    

- Ein Benutzer-Computer
    
  
- Ein Server außerhalb der SharePoint-Farm
    
  
- Eine Webrolle oder Workerrolle in Microsoft Azure
    
  
Nahezu jede Klasse im zentralen serverseitigen Objektmodell für Websites und Listen verfügt über eine entsprechende Klasse im .NET Framework-Clientobjektmodell. Außerdem macht das .NET Framework-Clientobjektmodell eine vollständige API-Gruppe zum Erweitern weiterer Features verfügbar. Dazu gehören einige SharePoint-Features, wie z. B. ECM, Taxonomie, Benutzerprofile, erweiterte Suche, Analyse, BCS und andere.
  
    
    
Um die Leistung zu verbessern, werden im .NET Framework-Clientobjektmodell geschriebene Codezeilen in Batches an den SharePoint-Server gesendet. Dort werden sie in serverseitigen Code konvertiert und ausgeführt. Die abgefragten Ergebnisse und der neue Status aller Variablen werden anschließend an den Client zurückgegeben. Als Entwickler können Sie bestimmen, ob ein Batch synchron oder asynchron ausgeführt wird. (Bei einem synchronen Batch wartet die .NET Framework-Anwendung auf die vom Server zurückgegebenen Ergebnisse, bevor sie fortfährt; bei einem asynchronen Batch wird die clientseitige Verarbeitung sofort fortgesetzt und Client-Benutzeroberfläche bleibt reaktionsfähig.
  
    
    
Sie können LINQ-Abfragesyntax in Ihrem Clientcode verwenden, um beliebige **IEnumerable**-Objekte abzufragen, dazu gehören auch SharePoint-Objekte, in denen **IEnumerable** implementiert ist. Wenn Sie so vorgehen, verwenden Sie jedoch [LINQ to Objects](http://msdn.microsoft.com/de-DE/library/bb397919.aspx) und nicht [LINQ to SharePoint-Anbieter](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx), die dazugehörige Dokumentation ist also für clientseitigen Code nicht relevant.
  
    
    
Die Assemblys für das .NET Framework-Clientobjektmodel muss auf dem Client installiert sein. Sie sind in einem verteilbaren Paket enthalten, das Sie unter  [SharePoint-Clientkomponenten](http://www.microsoft.com/en-us/download/details.aspx?id=35585) abrufen können.
  
    
    
Beispiele zur Verwendung des .NET Framework-Objektmodells finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx).
  
> [!NOTE]
> Sie können auch die SharePoint REST/OData-Endpunkte in einer .NET Framework-Anwendung verwenden. Einen Vergleich des .NET Framework-Clientobjektmodells mit den SharePoint REST-/OData-Endpunkten finden Sie im Abschnitt [REST-/OData-Endpunkte](#RESTOData) weiter unten in diesem Artikel.
  
    
    


### <a name="silverlight-client-object-model"></a>Silverlight-Clientobjektmodell

Das SharePoint-Objektmodell für Silverlight wird in Silverlight-Anwendungen unabhängig davon verwendet, wo die kompilierte XAP-Datei gespeichert ist. Das kann eine Objektbibliothek auf einer SharePoint-Website, ein Client-Computer, ein Cloud-Speicher oder ein externer Server sein. In der Regel wird eine Silverlight-Anwendung SharePoint in einem  [SilverlightWebPart](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebPartPages.SilverlightWebPart.aspx) -Objekt dargestellt. Das Silverlight-Clientobjektmodell in SharePoint ist fast identisch mit dem .NET Framework-Clientobjektmodell und umfasst Unterstützung für die gleichen Erweiterbarkeitsbereiche. Der Hauptunterschied liegt darin, dass in der Silverlight-Version alle Batches der Befehle asynchron an den Server gesendet werden, damit die Benutzeroberfläche aktiv bleibt.
  
    
    
Die Assemblys für das Silverlight-Clientobjektmodel werden auf jedem SharePoint-Server unter %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin gespeichert. Sie müssen nicht auf dem Computer installiert werden, auf dem die Silverlight-Anwendung läuft, haben jedoch die Möglichkeit dazu. Sie können sie auch in der XAP-Datei der Anwendung zu einem Paket zusammenfassen.
  
    
    
Silverlight XAP-Dateien können einer SharePoint-Add-Ins hinzugefügt werden, darunter auch von SharePoint gehostete Apps. Dabei wird die XAP-Datei in einer Bibliothek im App-Web bereitgestellt. (Weitere Informationen zu App-Webs finden Sie unter [Hostwebsites, Add-In-Websites und SharePoint-Komponenten in SharePoint](http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx).) So erhält man mit der Silverlight-App eine nützliche Methode zum Hinzufügen von benutzerdefiniertem SharePoint-Code in einer App, da benutzerdefinierter serverseitiger Code in SharePoint-Add-Ins nicht zulässig ist. Zudem können Silverlight-Entwickler für die Erstellung von SharePoint-Anwendungen mit einer minimalen Lernkurve nutzen.
  
> [!NOTE]
> Sie können auch die SharePoint REST-/OData-Endpunkte in einer Silverlight-Anwendung verwenden. Einen Vergleich des Silverlight-Clientobjektmodells mit den SharePoint REST-/OData-Endpunkten finden Sie im Abschnitt [REST-/OData-Endpunkte](#RESTOData) weiter unten in diesem Artikel.
  
    
    


### <a name="mobile-object-model"></a>Mobiles Objektmodell

Für Windows Phone-Geräte ist eine spezielle Version des Silverlight-Clientobjektmodells verfügbar. Es umfasst zusätzliche APIs, die nur für Telefone relevant sind, wie z. B. APIs, mit der sich eine Smartphone-App für Benachrichtigungen vom Microsoft-Pushbenachrichtigungsdienst registrieren kann. Sie unterstützt alle wichtigen SharePoint-Funktionen; es bietet jedoch keine Unterstützung für Nebenerweiterungsbereiche, die von den anderen beiden Clientobjektmodellen für verwalteten Code unterstützt werden. Verwenden Sie zum Zugreifen auf diese zusätzlichen Bereiche die SharePoint REST/OData-Endpunkte in Ihrer mobilen App. Weitere Informationen dazu finden Sie im Abschnitt  [REST/OData-Endpunkte](#RESTOData) weiter unten in diesem Artikel.
  
    
    
Die Assemblys für das mobile Objektmodell werden auf jedem SharePoint-Server unter %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin gespeichert. Sie können Sie in der XAP-Datei in Ihrer Windows Phone-Anwendung zu einem Paket zusammenfassen.
  
    
    

## <a name="javascript-object-model"></a>JavaScript-Objektmodell
<a name="JavaScriptOM"> </a>

SharePoint stellt ein JavaScript-Objektmodell für die Nutzung in einem Inline-Skript oder separaten JS-Dateien bereit. Es umfasst die gleichen Funktionen wie die Clientobjektmodelle .NET Framework und Silverlight. Genau wie das Silverlight-Clientobjektmodell bietet das JavaScript-Objektmodell eine nützliche Methode zum Hinzufügen von benutzerdefiniertem SharePoint-Code in einer App, da benutzerdefinierter serverseitiger Code in SharePoint-Add-Ins nicht zulässig ist. Zudem können Webentwickler ihre vorhandenen JavaScript-Kenntnisse für die Erstellung von SharePoint-Anwendungen mit einer minimalen Lernkurve nutzen.
  
    
    
Genau wie Objektmodelle mit verwaltetem Code interagiert die JavaScript-Infrastruktur für SharePoint mit den Farm-Servern in Batches. Diese Batches werden immer asynchron ausgeführt. Außerdem ist es nun möglich, in JavaScript domänenübergreifend auf SharePoint-Daten zuzugreifen (jedoch nur Daten, die sich in der gleichen übergeordneten Websitesammlung befinden), was in vorherigen SharePoint-Versionen nicht möglich war. Weitere Informationen finden Sie unter  [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx). Daten werden in JavaScript Object Notation (JSON) vom Server zurückgegeben.
  
    
    
Das JavaScript-Objektmodell ist in einer JS-Dateigruppe definiert, die sich auf jedem Server unter %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS befinden.
  
    
    
Beispiele zur Verwendung des .NET Framework-Objektmodells finden Sie unter [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx).
  
> [!NOTE]
> Sie können auch die SharePoint REST-/OData-Endpunkte in einer JavaScript-Anwendung verwenden. Einen Vergleich des JavaScript-Clientobjektmodells mit den SharePoint REST-/OData-Endpunkten finden Sie im Abschnitt [REST-/OData-Endpunkte](#RESTOData). 
  
    
    


## <a name="restodata-endpoints"></a>REST-/OData-Endpunkte
<a name="RESTOData"> </a>

Für den Zugriff auf SharePoint-Entitäten über Clienttechnologien, die nicht JavaScript verwenden und nicht auf den Plattformen .NET Framework oder Silverlight basieren, bietet SharePoint eine Implementierung eines REST-Webdiensts, der CRUDQ-Vorgänge bei SharePoint-Listendaten über das  [OData-Protokoll](http://www.odata.org/) ausführt. Zudem verfügt nahezu jede API in den Clientobjektmodellen über einen entsprechenden REST-Endpunkt. Dadurch kann im Code mithilfe jeder Technologie, die REST-Standardfunktionen unterstützt, direkt mit SharePoint interagiert werden. Der Webdienst "svc.web" behandelt die HTTP-Anforderung und liefert eine Antwort im Atom- oder JSON-Format.
  
    
    
Weitere Informationen über den REST/OData-Webdienst finden Sie unter dem Knoten  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx); Beispiele dazu finden Sie im Thema  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).
  
    
    

### <a name="comparing-restodata-programming-with-client-object-model-programming"></a>Vergleich zur REST/OData-Programmierung mit der Clientobjektmodell-Programmierung

In einigen Situationen ist die Verwendung von REST-Endpunkten möglicherweise vorzuziehen, selbst in Anwendungen, in denen ein SharePoint-Objektmodell verfügbar ist. Insbesondere für Entwickler, die über keine Erfahrung Im Entwickeln von Windows-basiertem Code haben. In der folgenden Tabelle finden Sie einen Vergleich zwischen den wichtigsten Funktionen dieser Programmierungsoptionen für einen Entwickler, der eine Anwendung auf einer Windows-Plattform oder mit einer Plattform erstellt, die JavaScript unterstützt.
  
    
    


|**Funktion**|**.NET Framework oder Silverlight-Objektmodelle**|**JavaScript-Objektmodell**|**Von einer Windows-Plattform oder von JavaScript abgerufene REST/OData-Endpunkte**|
|:-----|:-----|:-----|:-----|
|Objektorientiertes Programmieren  <br/> |Ja  <br/> |Ja  <br/> |Nein  <br/> |
|Batch-Verarbeitung  <br/> |Ja  <br/> |Ja  <br/> |Ja  <br/> |
|APIs für die bedingte Verarbeitung und Ausnahmebehandlungen  <br/> |Ja  <br/> |Nein  <br/> |Nein  <br/> |
|Verfügbarkeit der LINQ-Syntax  <br/> |Ja  <br/> |Nein  <br/> |Nein  <br/> |
|Kombinieren von Listendaten aus verschiedenen SharePoint-Webanwendungen  <br/> |Ja  <br/> |Nein  <br/> |Ja  <br/> |
|Vertrautheit für erfahrene REST/OData-Entwickler  <br/> |Nein  <br/> |Nein  <br/> |Ja  <br/> |
|Ähnlichkeiten zur nicht-Windows-Programmierung oder JavaScript-Programmierung  <br/> |Nein  <br/> |Ja  <br/> |Ja  <br/> |
|Starke Typisierung für Listenelementfelder  <br/> |Nein (außer mit LINQ)  <br/> |Nein  <br/> |Ja, von einer Windows-Plattform          Nein, von JavaScript  <br/> |
|Nutzen von jQuery, Knockout und anderen JavaScript-Bibliotheken  <br/> |Nein  <br/> |Ja  <br/> |Nein, von einer Windows-Plattform          Ja, von JavaScript  <br/> |
   

## <a name="wcf-data-services-framework"></a>Framework für die WCF Data Services
<a name="WCFDataServices"> </a>

Wenn Sie LINQ-Syntax in .NET Framework- oder Silverlight-Clientanwendungen bevorzugen, unterstützt SharePoint die  [WCF Data Services](http://msdn.microsoft.com/de-DE/library/cc668792.aspx) als LINQ-Anbieter. Sie können wie in vorherigen Versionen von SharePoint Foundation die "listdata.svc" (nur für Listendaten) vorgeben, oder die gleiche "client.svc" vorgeben, die die OData-Schnittstelle für den Zugriff auf alle SharePoint-Entitäten und Listendaten unterstützt. Weitere Informationen dazu finden Sie unter [Abfragen von SharePoint Foundation mit ADO.NET Data Services](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx).
  
    
    
In Abbildung 2 ist die Beziehung zwischen den verschiedenen Client-APIs, verschiedenen Client-Anwendungstypen und SharePoint dargestellt. Die unterschiedlichen _api*-URLs sind die farmrelativen URLs für die REST-Endpunkte. Weitere Informationen dazu finden Sie unter dem Thema  [Weitere Informationen zum SharePoint 15 REST-Dienste](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx#bk_learnmore).
  
    
    

**Abbildung 2. Client-Anwendungen und APIs in SharePoint**

  
    
    

  
    
    
![Programmiermodell für Apps für SharePoint](../images/Sp15_app_.png)
  
    
    

  
    
    

  
    
    

## <a name="deprecated-api-sets"></a>Veraltete API-Gruppen
<a name="DeprecatedAPIs"> </a>

Zwei API-Gruppen werden weiterhin im SharePoint-Framework für die Abwärtskompatibilität unterstützt, es wird jedoch empfohlen, sie nicht für neue Projekte zu verwenden: die  [ASP.NET-Webdienste (asmx)](http://msdn.microsoft.com/library/c587ee90-1f88-43f3-b1a7-5f3072d038f8%28Office.15%29.aspx) und [direkte Remoteprozeduraufrufe rufen die Datei owssvr.dll](http://msdn.microsoft.com/library/4aa5c82b-90fb-4be5-b30c-d35ecae42a81%28Office.15%29.aspx) auf.
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Übersicht über die SharePoint-Entwicklung](sharepoint-development-overview.md)
    
  
-  [Programmiermodelle in SharePoint](programming-models-in-sharepoint.md)
    
  
-  [SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen](sharepoint-add-ins-compared-with-sharepoint-solutions.md)
    
  
-  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx)
    
  
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
-  [Abfragen von SharePoint Foundation mit ADO.NET Data Services](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx)
    
  

  
    
    
