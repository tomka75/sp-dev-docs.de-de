---
title: Entwickeln von SharePoint-Add-Ins
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: db07ab3033222bf7240db0b99f4a9fafb961c3e7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="develop-sharepoint-add-ins"></a>Entwickeln von SharePoint-Add-Ins
Hier finden Sie ausführliche Artikel und Ressourcen, die Sie dabei unterstützen, erweiterte Funktionen in Ihre SharePoint-Add-Ins zu integrieren.
 
 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 
> **Hinweis** In diesem Artikel wird davon ausgegangen, dass Sie mit dem Artikel [SharePoint-Add-Ins](sharepoint-add-ins.md) und den Einstiegsmaterialien, auf die dieser verweist, vertraut sind.

Unter **Entwicklung** finden Sie folgende Ressourcen, in denen die verschiedenen Möglichkeiten in einem SharePoint-Add-In veranschaulicht werden:


- Ausführliche Übersichten
- Gewusst-wie-Artikel
- Codeausschnitte
    
 
Sie finden dort Artikel zu folgenden Themen: 
 
- Durchführen von Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen (CRUD-Operationen) für Listen
- Erstellen von REST-Abfragen und Interaktion mit den neuen APIs
- Konfigurieren von OAuth für Sicherheit
    
SharePoint verfügt über Funktionen für soziale Netzwerke für Unternehmen, wie Aktivitätsfeeds und Benutzerprofile, sowie über Funktionen für das Enterprise Content Management, LOB-Interoperabilitätsfunktionen und Funktionen zum Entwurf von Websites, durch die sich Ihre Add-Ins wirklich aus der Masse herausheben können. Weitere Informationen hierzu finden Sie unter [Hinzufügen von SharePoint-Funktionen](http://msdn.microsoft.com/library/11ecb65e-6dc5-4cf1-80ca-3c16418697b6%28Office.15%29.aspx).
 
Da der Code das Wichtigste ist, sehen Sie sich im Dev Center das Menü "Beispiele" an. Es enthält Hyperlinks zu unseren Codebeispielen für Add-Ins. Sobald Sie Ihre Entwicklungsumgebung eingerichtet haben, sollten Sie sich einige unserer Beispiele ansehen. Nutzen Sie die Community-Funktion, mit der Sie ein Codebeispiel anfordern können, falls Sie in unseren Beispielen nicht das finden, was Sie suchen. Wir nutzen diese Anforderungen zusammen mit anderen Rückmeldungen für unsere laufenden Aktualisierungen des Inhalts und der Beispiele. Lassen Sie uns also bitte wissen, wenn Sie sich etwas wünschen!

## <a name="get-started-with-sharepoint-add-ins-resources"></a>Erste Schritte mit Ressourcen für SharePoint-Add-Ins
<a name="bk_gettingstarted"> </a>

Wenn Sie Neuling in der Entwicklung mit SharePoint-Add-Ins sind, sehen Sie sich  [SharePoint-Add-Ins](sharepoint-add-ins.md) an. Diese Seite enthält Verweise auf wichtige Artikel, die Sie schnell mit verschiedenen Arten von SharePoint-Add-Ins vertraut machen. Bevor Sie beginnen, anspruchsvollere Projekte mit SharePoint-Add-Ins entwickeln, sollten Sie sich darüber im Klaren sein, welche Art von Add-Ins Sie erstellen möchten, welche Technologien Sie einbeziehen möchten und welche Hostingoptionen Sie verwenden möchten.
 
### <a name="essential-tasks-and-resources-for-developing-sharepoint-add-ins-using-the-client-object-model-javascript-object-model-and-rest-endpoints-in-sharepoint"></a>Grundlegende Aufgaben und Ressourcen für die Entwicklung von SharePoint-Add-Ins mit dem Clientobjektmodell, dem JavaScript-Objektmodell und REST-Endpunkten in SharePoint
<a name="bk_essentials"> </a>

Gleichgültig, welche Art von SharePoint-Add-In Sie erstellen werden, das Add-In interagiert immer auf irgendeine Weise mit einer SharePoint-Website. Die Artikel in Tabelle 1 beschreiben, wie viele der wichtigsten Arten von Add-Ins mithilfe der drei Schnittstellen, die für SharePoint-Add-Ins zur Verfügung stehen, mit SharePoint-Sites zusammenarbeiten. Diese Schnittstellen sind das Clientobjektmodell, das JavaScript-Objektmodell und REST-Endpunkte.

**Tabelle 1. Grundlegende Vorgänge mit dem SharePoint-Clientobjektmodell, dem JavaScript-Objektmodell und der REST-Schnittstelle**


|**Thema**|**Beschreibung**|
|:-----|:-----|
| [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](complete-basic-operations-using-sharepoint-client-library-code.md)|Erläutert, wie allgemeine Vorgänge mit C# und dem Clientobjektmodell ausgeführt werden.|
| [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md)|Erläutert, wie allgemeine Vorgänge mit dem JavaScript-Objektmodell ausgeführt werden.|
| [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten](complete-basic-operations-using-sharepoint-rest-endpoints.md)|Erläutert, wie allgemeine Vorgänge mit der REST-Schnittstelle ausgeführt werden.|

## <a name="learn-the-fundamental-concepts-for-development-with-sharepoint-add-ins"></a>Informationen über die grundlegenden Konzepte für die Entwicklung mit SharePoint-Add-Ins
<a name="bk_fundamentals"> </a>

Neben den grundlegenden Vorgängen sollten Sie auch die grundlegenden Konzepte des Add-In-Entwicklungsmodells von SharePoint verstehen. Jede Art von SharePoint-Add-In enthält eine Add-In-Manifestdatei und wird in ein Add-In-Paket integriert, das Sie auf einer SharePoint-Website bereitstellen. Bei der Entwicklung jeder Art von Add-In müssen Sie außerdem verschiedene Aspekte bezüglich der Authentifizierung und Autorisierung, des Datenzugriffs und der Benutzerfreundlichkeit berücksichtigen. Die Artikel in Tabelle 2 machen Sie mit diesen Themen vertraut und erklären die Implikationen, die diese für jede Art von haben.

**Tabelle 2. Grundlegende Konzepte für die Entwicklung mit SharePoint-Add-Ins**

|**Thema**|**Beschreibung**|
|:-----|:-----|
| [Autorisierung und Authentifizierung für Add-Ins in SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md)|In diesem Thema werden die Grundkonzepte in Bezug auf den Erwerb der notwendigen Berechtigungen für die Arbeit mit SharePoint-Ressourcen erläutert.|
| [Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md)|Erläutert, wie Add-In-Manifeste funktionieren und Add-In-Pakete erstellt werden.|
| [Erstellen von UX-Komponenten in SharePoint](create-ux-components-in-sharepoint.md)|Untersucht die Methoden, mit denen Sie eine funktionsreiche Benutzeroberfläche in SharePoint-Add-Ins erstellen können.|
| [Arbeiten mit externen Daten in SharePoint](work-with-external-data-in-sharepoint.md)|Erläutert die Optionen und Verfahren für den Datenzugriff, die in verschiedene Arten von SharePoint-Add-Ins verfügbar sind.|
| [Lizenzieren von Office- und SharePoint-Add-Ins](http://msdn.microsoft.com/library/license-your-office-and-sharepoint-add-ins%28Office.15%29.aspx)|Führt Sie durch das Add-In-Lizenzframework für Office- und SharePoint-Add-Ins.|

## <a name="put-the-pieces-together-building-advanced-sharepoint-add-ins-by-integrating-capabilities"></a>Zusammensetzen der Einzelteile: Erstellen erweiterter SharePoint-Add-Ins durch Integrieren von Funktionen
<a name="bk_integrate"> </a>

Wenn Sie mit den Funktionen und Features von SharePoint-Add-Ins vertraut sind, können Sie komplexere Add-Ins erstellen, indem Sie die Funktionen und Elemente so kombinieren, dass Ihre Anforderungen erfüllt werden. Die Artikel in Tabelle 3 zeigen, wie Funktionen integriert und SharePoint-Add-Ins mit einem größeren Funktionsumfang erstellt werden.
 
**Tabelle 3. Erweiterte Konzepte in SharePoint-Add-Ins**

|**Thema**|**Beschreibung**|
|:-----|:-----|
| [Erstellen eines von einem Anbieter gehosteten Add-Ins, das eine benutzerdefinierte SharePoint-Liste und einen benutzerdefinierten Inhaltstyp enthält](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md)|Erläutert, wie Sie SharePoint-Add-Ins erstellen, die in der Cloud gehostet werden und benutzerdefinierte SharePoint-Listen und -Inhaltstypen enthalten.|

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins](tools-and-environments-for-developing-sharepoint-add-ins.md) 
-  [Entwerfen von SharePoint-Add-Ins](design-sharepoint-add-ins.md)
-  [Veröffentlichen von SharePoint-Add-Ins](publish-sharepoint-add-ins.md)
-  [Beispielpaket für SharePoint-Add-Ins](http://code.msdn.microsoft.com/office/Apps-for-SharePoint-sample-64c80184)
 
