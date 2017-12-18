---
title: Zugriff auf externe Daten mit REST in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0663cc8c-a736-434d-9858-6ce12ce7f748
ms.openlocfilehash: 9b1cab4d79db115c705cf0264bafee0593dfd5bc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="access-external-data-by-using-rest-in-sharepoint"></a>Zugriff auf externe Daten mit REST in SharePoint

Erfahren Sie, wie externe Daten mithilfe von Representational State Transfer (REST) URLs für Business Connectivity Services (BCS)SharePoint zugreifen. In diesem Artikel veranschaulicht, wie eine externe Liste einrichten, die Daten aus einer Open Data Protocol (OData) Datenquelle abruft.
  
    
    


## <a name="prerequisites-for-accessing-external-data-using-rest"></a>Erforderliche Komponenten für den Zugriff auf externe Daten mithilfe von REST
<a name="bkmk_Prerequisites"> </a>

Zugriff auf externe Daten aus SharePoint unter Verwendung von REST, benötigen Sie Folgendes:
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
- Office Developer Tools für Visual Studio 2012
    
  
- Eine funktionsfähige SharePoint-Add-Ins Entwicklungsumgebung: befolgen Sie die Anweisungen in  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
    
  
- Zugriff auf den öffentlichen OData.org Herstellern
    
  

### <a name="core-concepts-to-know-when-accessing-external-data-with-rest"></a>Kernkonzepte beim Zugriff auf externe Daten mit REST

Der REST-Dienst SharePoint bietet eine Möglichkeit Zugriff auf externe Daten mithilfe einer speziell gestalteten URL. Funktionsweise und Ihre Verwendung finden Sie unter den folgenden Artikeln.
  
    
    

**In Tabelle 1. Kernkonzepte für REST in SharePoint**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx) <br/> |Erfahren Sie, wie den SharePoint-REST-Dienst verwenden, der eine Programmierschnittstelle vergleichbar mit der vorhandenen SharePoint-Clientobjektmodell REST bietet.  <br/> |
| [Erste Schritte mit den SharePoint REST-Dienst](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx) <br/> |Hier erhalten Sie grundlegende Informationen zum Verwenden des SharePoint REST-Diensts zum Zugreifen auf und Aktualisieren von SharePoint-Daten mithilfe der REST- und OData-Webprotokollstandards.  <br/> |
| [Verwenden des SharePoint REST-Diensts](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx) <br/> |Erfahren Sie, wie die SharePoint-Datenstruktur dargestellt in der REST-Dienst zu navigieren, führen Sie allgemeine CRUD (erstellen, lesen, aktualisieren und löschen)-Vorgänge zu SharePoint-Elemente über den REST-Dienst Synchronisieren von SharePoint-Elemente anwendungsübergreifend und Element Parallelität steuern.  <br/> |
   

## <a name="create-an-sharepoint-add-in-to-access-external-data-using-rest"></a>Erstellen einer SharePoint-Add-In zum Zugreifen auf externe Daten mithilfe von REST
<a name="bkmk_CreateApp"> </a>

Die folgenden Schritte führen Sie durch eine SharePoint-Add-In einrichten und Konfigurieren von einer Webseite zum Verwenden von REST-Funktionen zum Abrufen von Daten aus einer externen Datenquelle anzufordern.
  
    
    

### <a name="to-create-an-sharepoint-add-in"></a>Erstellen einer SharePoint-Add-In


1. Öffnen Sie Visual Studio 2012.
    
  
2. Erstellen einer **App für SharePoint**-Projekt.
    
  
3. Geben Sie die Appeinstellungen, einschließlich app-Name die URL der Website für das Debuggen der app und wie Sie die app (automatisch gehostet, vom Anbieter gehosteten, SharePoint-Hosting) hosten möchten. Weitere Informationen zu Hostingoptionen finden Sie unter  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).
    
  
4. Wählen Sie auf **Fertig stellen**, um die app zu erstellen.
    
  

### <a name="to-generate-the-external-content-type"></a>Um den externen Inhaltstyp zu generieren.


1. Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.
    
  
2. **OData-Quelle geben** Sie auf der Seite Geben Sie die URL der OData-Dienst, den, dem Sie mit verbinden möchten. In diesem Fall verwenden Sie die Northwind-OData-Quelle auf [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem)veröffentlicht. Legen Sie die URL für den OData-Dienst auf  `http://services.odata.org/Northwind/Northwind.svc/`, und geben Sie einen Namen für die Datenquelle.
    
    Wählen Sie **Weiter** aus.
    
  
3. Dadurch wird eine Liste aller Datenentitäten, die vom OData Service verfügbar gemacht werden. Wählen Sie die **Kunden**-Entität. Stellen Sie sicher, dass das Kontrollkästchen **für die ausgewählten Datenentitäten (mit Ausnahme von Dienstvorgänge) Listeninstanzen erstellen** ausgewählt ist.
    
  
4. Wählen Sie **Fertig stellen** aus.
    
  

## <a name="code-example-add-scripts-and-html-to-the-homeaspx-page"></a>Codebeispiel: Hinzufügen von Skripts und HTML auf der Seite Home.aspx
<a name="bkmk_AddUIelements"> </a>

Zu diesem Zeitpunkt haben Sie einen externen Inhaltstyp und eine externe Liste, in der die Daten aus der Northwind OData-Quelle angezeigt werden. 
  
    
    
Nächste Ziel ist es, die Seite "default.aspx" zu ändern, die erstellt wurde, wenn Sie Ihre app erstellt haben. Fügen Sie einen Container zum Speichern der Ergebnisse der Abfrage, die mit Laden der Seite ausgeführt wird. Durch Ausführen des Skripts auf der Seite Load-Ereignis, stellen Sie sicher, dass das Skript ausgeführt wird, jedes Mal wird die Seite durchsucht, und die resultierenden REST-Aufrufe auf die Northwind OData-Quelle erfolgen Datensätze auf der Seite hinzufügen.
  
    
    

### <a name="to-add-the-container-to-the-defaultaspx-page"></a>So fügen Sie dem Container zur Seite Default.aspx hinzu


1. Öffnen Sie im **Projektmappen-Explorer** die Seite "Default.aspx" im Modul **Seiten**.
    
  
2. Fügen Sie das folgende **div** Element auf der Seite.
    
```HTML
  
<div id="displayDiv"></div>
```

3. Speichern Sie die Seite.
    
  
Zum Schluss fügen Sie Code auf die Datei App.js, die beim Laden der Seite ausgeführt.
  
    
    

### <a name="to-modify-the-appjs-file-to-make-rest-calls"></a>So ändern Sie die Datei App.js REST-Anrufe


1. Öffnen Sie die Datei App.js in das Modul Skripts Ihrer SharePoint-Projekts.
    
  
2. Fügen Sie den folgenden Code am Ende der Datei.
    
```
  $(document).ready(function () {

    // Namespace
    window.AppLevelECT = window.AppLevelECT || {};

    // Constructor
    AppLevelECT.Grid = function (hostElement, surlWeb) {
        this.hostElement = hostElement;
        if (surlWeb.length > 0 &amp;&amp; surlWeb.substring(surlWeb.length - 1, surlWeb.length) != "/")
            surlWeb += "/";
        this.surlWeb = surlWeb;
    }

    // Prototype
    AppLevelECT.Grid.prototype = {

        init: function () {

            $.ajax({
                url: this.surlWeb + "_api/lists/getbytitle('Customer')/items?$select=BdcIdentity,CustomerID,ContactName",
                headers: {
                    "accept": "application/json",
                    "X-RequestDigest": $("#__REQUESTDIGEST").val()
                },
                success: this.showItems
            });
        },

        showItems: function (data) {
            var items = [];

            items.push("<table>");
            items.push('<tr><td>Customer ID</td><td>Customer Name</td></tr>');

            $.each(data.d.results, function (key, val) {
                items.push('<tr id="' + val.BdcIdentity + '"><td>' +
                    val.CustomerID + '</td><td>' +
                    val.ContactName + '</td></tr>');
            });

            items.push("</table>");

            $("#displayDiv").html(items.join(''));
        }
    }

    ExecuteOrDelayUntilScriptLoaded(getCustomers, "sp.js");
});

function getCustomers() {
    var grid = new AppLevelECT.Grid($("#displayDiv"), _spPageContextInfo.webServerRelativeUrl);
    grid.init();
}
```

Drücken Sie F5, um die app in SharePoint bereitstellen. Wechseln Sie zur Seite Default.aspx in der app, und eine Liste der Kunden wird auf der Seite angezeigt.
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bkmk_Addres"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Erste Schritte mit den SharePoint REST-Dienst](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx)
    
  
-  [Verwenden des SharePoint REST-Diensts](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx)
    
  
-  [Add-in-bezogenen externen Inhaltstypen in SharePoint](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  

