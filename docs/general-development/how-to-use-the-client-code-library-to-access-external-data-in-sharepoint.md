---
title: "Verwenden der Code-Clientbibliothek für den Zugriff auf externe Daten in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c280ae92-c52b-4658-b0f3-805fb215ef8e
ms.openlocfilehash: bee624e58e0b7b85adbbdbc6097e04961001422f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="use-the-client-code-library-to-access-external-data-in-sharepoint"></a>Verwenden der Code-Clientbibliothek für den Zugriff auf externe Daten in SharePoint

In diesem Artikel erfahren Sie, wie Sie das Clientobjektmodell in SharePoint verwenden, um mit Business Connectivity Services (BCS)-Objekten in SharePoint mithilfe von browserbasierten Skripts zu arbeiten.

In diesem Artikel wird gezeigt, wie eine externe Liste eingerichtet wird, die Daten von einer Open Data-Protokollquelle (OData) mithilfe des Clientobjektmodells in SharePoint abruft.
  
    
    


## <a name="prerequisites-for-accessing-external-data-using-the-sharepoint-client-object-model"></a>Erforderliche Komponenten für den Zugriff auf externe Daten mithilfe des Clientobjektmodells SharePoint
<a name="bkmk_Prerequisites"> </a>

Im folgenden sind die Anforderungen für die Entwicklung von apps mithilfe des SharePoint-Clientobjektmodells:
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
- Office Developer Tools für Visual Studio 2012
    
  
- Eine funktionsfähige SharePoint-Add-Ins Entwicklungsumgebung: befolgen Sie die Anweisungen in  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
    
  
- Zugriff auf den öffentlichen OData.org Herstellern
    
  

### <a name="core-concepts-to-know-when-accessing-external-data-with-the-sharepoint-client-object-model"></a>Kernkonzepte beim Zugriff auf externe Daten mit dem SharePoint-Clientobjektmodell

Das Clientobjektmodell SharePoint bietet eine Möglichkeit zum Zugriff auf externe Daten mit clientseitigen aufrufen, die die serverseitige APIs imitieren. Funktionsweise und Verwendungsweise, finden Sie in die Artikeln in Tabelle 1.
  
    
    

**In Tabelle 1. Kernkonzepte für die Verwendung des Clientobjektmodells**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx) <br/> |Erfahren Sie, wie Sie Code führen grundlegende Vorgänge mit dem SharePoint .NET Framework-Client-Objektmodell (CSOM) schreiben.  <br/> |
   

## <a name="create-an-sharepoint-add-in-to-access-external-data-using-the-client-object-model"></a>Erstellen einer SharePoint-Add-In Zugriff auf externe Daten mithilfe des Clientobjektmodells
<a name="bkmk_CreateApp"> </a>

Die folgenden Verfahren wird gezeigt, wie ein SharePoint-Add-In einrichten und Konfigurieren einer Webseite, sodass Anforderungen mithilfe der Methoden Client und Objekte zum Abrufen von Daten aus einer externen Datenquelle.
  
    
    

### <a name="to-create-an-sharepoint-add-in"></a>Erstellen einer SharePoint-Add-In


1. Öffnen Sie Visual Studio 2012.
    
  
2. Erstellen einer **App für SharePoint**-Projekt.
    
  
3. Geben Sie die Appeinstellungen, einschließlich app-Name die URL der Website für das Debuggen der app und wie Sie die app (automatisch gehostet, vom Anbieter gehosteten, SharePoint-Hosting) hosten möchten. Weitere Informationen zu Hostingoptionen finden Sie unter  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).
    
  
4. Klicken Sie auf **Fertig stellen**, um die app zu erstellen.
    
  

### <a name="to-generate-the-external-content-type"></a>Um den externen Inhaltstyp zu generieren.


1. Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.
    
  
2. Geben Sie im Assistenten **OData-Quelle angeben** die URL des OData-Diensts, die Sie mit verbinden möchten. In diesem Fall verwenden Sie die Northwind-OData-Quelle auf [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem)veröffentlicht. Legen Sie die URL für den OData-Dienst auf  `http://services.odata.org/Northwind/Northwind.svc/`
    
    Geben Sie einen Namen für die Datenquelle, und klicken auf **Weiter**.
    
  
3. Es wird eine Liste der Entitäten, die vom OData Service verfügbar gemacht werden angezeigt. Wählen Sie die **Kunden**-Entität. Stellen Sie sicher, dass das Kontrollkästchen **für die ausgewählten Datenentitäten (mit Ausnahme von Dienstvorgänge) Listeninstanzen erstellen** ausgewählt ist.
    
  
4. Wählen Sie **Fertig stellen** aus.
    
  

## <a name="code-example-add-scripts-and-html-to-the-defaultaspx-page"></a>Codebeispiel: Hinzufügen von Skripts und HTML auf der Seite "default.aspx"
<a name="bkmk_AddUIelements"> </a>

Zu diesem Zeitpunkt müssen Sie den externen Inhaltstyp und einer externen Liste, die die Daten aus der Netflix OData-Quelle angezeigt werden. 
  
    
    
Nächste Ziel ist es, die Seite "default.aspx" zu ändern, die Sie erstellt haben, wenn Sie Ihre app erstellt haben. Sie fügen einen Container, der die Ergebnisse der Abfrage enthalten soll, die mit Laden der Seite ausgeführt wird. Durch Ausführen des Skripts auf der Seite Load-Ereignis, stellen Sie sicher, dass das Skript ausgeführt wird, jedes Mal, wenn die Seite wird durchsucht und die resultierende Client Objektmodellaufrufe werden versucht, den Netflix-OData-Quelle Datensätze auf der Seite hinzufügen. 
  
    
    

### <a name="to-add-the-container-to-the-defaultaspx-page"></a>So fügen Sie dem Container zur Seite Default.aspx hinzu


1. Öffnen Sie im **Projektmappen-Explorer** die Seite Default.aspx in der **Pages**-Modul abgelegte.
    
  
2. Fügen Sie das folgende **div** -Element auf der Seite hinzu:
    
```HTML
  
<div id="displayDiv"></div>
```

3. Speichern Sie die Seite.
    
  
Zum Schluss fügen Sie Code auf die Datei App.js, die beim Laden der Seite ausgeführt.
  
    
    

### <a name="to-modify-the-appjs-file-to-make-client-object-model-calls"></a>So ändern Sie die Datei App.js, sodass Client ruft-Objektmodell


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
<a name="bkmk_Addresources"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Erste Schritte der Verwendung des Clientobjektmodells mit externen Daten in SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [BCS-Client-Objektmodellreferenz für SharePoint](bcs-client-object-model-reference-for-sharepoint.md)
    
  
-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  

