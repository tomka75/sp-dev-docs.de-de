---
title: Datenspeicheroptionen in SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: 0e9264de4cb19e4f32939e02786611580d41c82d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="data-storage-options-in-sharepoint-online"></a>Datenspeicheroptionen in SharePoint Online

Bei der Entwicklung von SharePoint Online-add-ins müssen Sie eine Reihe von verschiedenen Optionen zum Speichern von Daten. Sie können das in diesem Artikel beschriebene Beispiel erkunden die Unterschiede zwischen den einzelnen Optionen, und lernen Sie die Vorteile der Verwendung von remote-Datenspeicher verwenden. 

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

In diesem Artikel werden die [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) Beispiel-app, die jeder der folgenden Datenspeicheroptionen und die Vorteile und Nachteile der einzelnen anzeigt:

- SharePoint-Liste auf dem hostweb
    
- SharePoint-Liste im Web app
    
- SQL Azure-Datenbank
    
- Azure Warteschlangenspeicher
    
- Azure-tabellenspeicherung
    
- Externen Webdienst
    
Die [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) Beispiel-app ist eine vom Anbieter gehosteten app geschrieben in c# und JavaScript, das eine Anzahl von SharePoint-Artefakte (Listen, app-Webpart, Webpart) für das hostweb und app-Webs bereitstellt. Es interagiert mit SharePoint-Listen auf der app-Web und Host-Web und führt auch Aufrufe an eine SQL Azure-Datenbank, ein Azure Warteschlangen- und Tabelle Speicherung und ein Remotewebdienst, die OData implementiert wird. In diesem Beispiel wird das Muster Model-View-Controller (MVC) verwendet.
Die [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) Beispiel-app gilt jede Speicheroption Daten auf eine bestimmte Funktion für die die Option gut geeignet ist, wie in der folgenden Tabelle beschrieben.

|Beispiel-app-Speicheroption|Verwendet für|
|:--|:--|
|SharePoint-Liste app-web|Kunden-Notizen|
|SharePoint-Liste Hostwebsite|Support-Anfragen|
|Northwind-OData-Dienst|Kunden|
|Azure-tabellenspeicherung|CSR-Bewertungen|
|Azure Warteschlangenspeicher|Aufrufen der Warteschlange|
|SQL Azure-Datenbank Northwind|Aufträge, Bestelldetails, Produkte|

Die app implementiert ein Customer Service Dashboard und zugehörige Schnittstellen, die aktuellen Aufträge, Kunden repräsentative Umfrage Bewertungen, Kunden Notizen, Support-Anfragen und eine Customer Vertreter Warteschlange anzeigen. Die ersten beiden Szenarien können Sie das Abrufen von Daten mithilfe von relativ einfach, Client-Objektmodellcode oder REST-Abfragen, aber durch Liste Abfrage Schwellenwerte begrenzt werden. Die folgenden vier Szenarien verwendet unterschiedliche Typen von Remotespeicher. 

**Abbildung 1. Startseite für Data Storage Modelle fordert Sie zum Bereitstellen von SharePoint-Komponenten**

![Screenshot des app-Beispiel-UI](media/bb3b58ca-b983-4ec4-b36d-18a911edb5d5.png)

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Bevor Sie dieses Beispiel verwenden, stellen Sie sicher, dass Sie über Folgendes verfügen:

- Ein Microsoft Azure-Konto können Sie eine SQL Azure-Datenbank bereitstellen und erstellen Sie ein Konto Azure-Speicher. 
    
- SharePoint-Entwickler-Standort, damit Sie das Beispiel aus Visual Studio 2013 bereitstellen können.
    
Darüber hinaus müssen Sie die Northwind-Datenbank in Microsoft Azure bereitstellen.

### <a name="to-deploy-the-northwind-database"></a>Zum Bereitstellen der Northwind-Datenbank

1. Melden Sie sich an dem Azure-Verwaltungsportal, und wählen Sie **SQL-Datenbanken**> **Server**.
    
2. Wählen Sie **einen SQL-Datenbankserver zu erstellen**.
    
3. Geben Sie Werte für **Benutzername**, **Kennwort**und **Region**, wie in Abbildung 2 dargestellt im Format **Server erstellen** .
    
    **Abbildung 2. Servereinstellungen für SQL-Datenbank**

    ![Zeigt die SQL-Datenbank für den server](media/7ae059fa-eecc-4446-8171-294e44acb189.png)

4. Wählen Sie die Taste mit dem Häkchen auf Fertig stellen, und erstellen Sie den Server.
    
5. Nun, dass Sie die Datenbank erstellt haben, wählen Sie den Namen des Servers, den Sie erstellt haben, wie in Abbildung 3 dargestellt.
    
    **Abbildung 3. Servernamen, klicken Sie auf der Seite Server**

    ![Zeigt die Liste der SQL-Datenbanken](media/a6b097e4-5ad2-47df-9e31-ac0d699efd76.png)

6. Wählen Sie **Konfigurieren**, und wählen Sie den Pfeil in der unteren rechten Ecke, um die Konfiguration abzuschließen, und wählen Sie **Speichern**.
    
7. Öffnen Sie SQL Server Management Studio auf Ihrem lokalen Entwicklungscomputer und erstellen Sie eine neue Datenbank mit dem Namen **NorthWind**.
    
8. Wählen Sie aus der **Nordwind** -Datenbank im **Objekt-Explorer**, und wählen Sie dann auf **Neue Abfrage**.
    
9. Öffnen Sie in einem Text-Editor Ihrer Wahl northwind.sql-SQL-Skript, das bereitgestellt wird mit dem Beispiel [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) .
    
10. Kopieren Sie den Text in der Datei northwind.sql, und fügen Sie ihn in das **Fenster SQL-Abfrage** in der SQL Server Management Studio, und wählen Sie dann auf **Ausführen**.
    
11. Öffnen Sie im **Objekt-Explorer**das Kontextmenü (Rechtsklick) der **Northwind** -Datenbank, wählen Sie **Tasks**aus, und wählen Sie dann auf **Datenbank in SQL Azure bereitstellen**.
    
12. Wählen Sie auf dem Bildschirm **Einführung in die** **nächste**.
    
13. Wählen Sie **verbinden...** , und geben Sie den **Servernamen** für den soeben erstellten SQL Azure-Datenbankserver.
    
14. Wählen Sie im Dropdownmenü für die **Authentifizierung** **SQL Server-Authentifizierung**aus.
    
15. Geben Sie den Benutzernamen und das Kennwort, mit dem Sie den Server SQL Azure-Datenbank erstellt, und wählen Sie dann **Verbinden**.
    
16. Wählen Sie **Weiter**, und wählen Sie **Fertig stellen**, und warten Sie, bis die Datenbank erstellt wird. Nachdem er erstellt wurde, wählen Sie **Schließen** , um den Assistenten zu schließen.
    
17. Geben Sie an der Azure-Verwaltungsportal ( [https://manage.windowsazure.com/](https://manage.windowsazure.com/)), stellen Sie sicher, dass die Nordwind-Datenbank erfolgreich erstellt wurde. Sie sollte angezeigt werden, dass es auf dem Bildschirm Sql-Datenbanken aufgeführt wie in Abbildung 4 dargestellt.
    
    **Abbildung 4. Übersicht über SQL Server-Datenbanken**

    ![Zeigt eine Liste aller SQL-Datenbanken, einschließlich Nordwind (engl.)](media/036b4252-f57b-4f39-9f60-ddaa30daf23c.png)

18. Wählen Sie aus der Nordwind-Datenbank, und wählen Sie dann auf **Ansicht SQL-Datenbank-Verbindungszeichenfolgen**.
    
19. Kopieren Sie die Verbindungszeichenfolge, und fügen Sie ihn in eine Textdatei, und speichern Sie es lokal. Sie werden diese Verbindungszeichenfolge später benötigen. Das Dialogfeld **Verbindungszeichenfolgen** zu schließen.
    
20. Wählen Sie den Link zum **Einrichten von Windows Azure-Firewall-Regeln für diese IP-Adresse** , und fügen Sie Ihre IP-Adresse den Firewall-Regeln, die Zugriff auf die Datenbank zu ermöglichen.
    
21. Öffnen Sie das Core.DataStorageModels.sln-Projekt in Visual Studio 2013.
    
22. Suchen Sie im Visual Studio- **Projektmappen-Explorer**die Datei "Web.config".
    
23. Suchen Sie in der Datei Web.config hinzufügen `name="NorthWindEntities"` Element, und ersetzen den vorhandenen ConnectionString-Wert mit der Verbindungszeichenfolge, die Sie in Schritt 19 lokal gespeichert. 
    
    ```XML
      <add name="NorthWindEntities" connectionString="metadata=res://*/Northwind.csdl|res://*/Northwind.ssdl|res://*/Northwind.msl;provider=System.Data.SqlClient;provider connection string=&amp;quot;data source=<Your Server Here>.database.windows.net;initial catalog=NorthWind;user id=<Your Username Here>@<Your Server Here>;password=<Your Password Here>;MultipleActiveResultSets=True;App=EntityFramework&amp;quot;" providerName="System.Data.EntityClient" />
    ```
24. Speichern Sie die Datei "Web.config".

## <a name="sharepoint-list-on-the-app-web-notes-scenario"></a>SharePoint-Liste im Web app (Notes Szenario)
<a name="sectionSection1"> </a>

Das Notes Liste Szenario, das in einer SharePoint-Liste für eine app-Website verwendet wird, zeigt, wie Listen in einer SharePoint-app-Web ausführen. In der app-Website mit einem Feld Titel und Beschreibung wird die Liste Notizen erstellt. Die SharePoint-REST-API führt eine Abfrage die Liste Notizen und gibt alle Notizen basierend auf eine Kunden-ID

Von Listen im Web app hat eine wichtige Vorteil gegenüber der anderen Speicher Lösungen: Sie können einfache SharePoint REST-API-Aufrufe zum Abfragen von Daten verwenden. Es gibt jedoch auch einige Nachteile:

- Um listenmetadaten zu aktualisieren, müssen Sie aktualisieren und erneut bereitstellen die app.
    
- Um die Datenstruktur zu aktualisieren, müssen Sie die Logik für das Speichern und Aktualisieren von Daten umschreiben.
    
- In der Liste gespeicherten Informationen kann nicht mit anderen add-ins auf einfache Weise gemeinsam genutzt werden.
    
- Sie können keine Daten in SharePoint suchen.
    
- Die Menge der Daten, die in Listen gespeichert werden können und die Größe des Abfrageresultsets sind beschränkt.
    
Der Code, der im Abschnitt "Hinweise" des Kunden Dashboards zugrunde liegt verwendet REST-Abfragen zum Abrufen von Daten aus einer Liste, die in der app-Web bereitgestellt wird. Diese Liste enthält die Felder für Titel, Autoren, Kunden-IDs und Beschreibungen. Sie können die app-Schnittstelle zum Hinzufügen und Abrufen von Notizen für einen angegebenen Kunden, verwenden, wie in Abbildung 5 dargestellt.

**Abbildung 5. Benutzeroberfläche für die Notes-app**

![Ein Screenshot der Benutzeroberfläche für das Datenmodell Speicher Notizen](media/d98ce2cf-5022-4f2b-ad3e-da4eea52dfb2.png)

Der **Notizen der Ansichtsliste in App-Web** -Link bietet eine Ansicht "sofort einsatzbereit" den Listendaten.

Diese app mithilfe des Model-View-Controller (MVC). Sie können den Code für das Szenario Notizen in der Datei Views/CustomerDashboard/Notes.cshtml sehen. Einfache REST-Aufrufen verwendet zum Hinzufügen und Abrufen von Daten. Der folgende Code ruft Notes aus der Liste Notizen für einen angegebenen Kunden.

```C#
function getNotesAndShow() {
    var executor = new SP.RequestExecutor(appWebUrl);
    executor.executeAsync(
       {
           url: appWebUrl + "/_api/web/lists/getByTitle('Notes')/items/" +
                "?$select=FTCAM_Description,Modified,Title,Author/ID,Author/Title" +
                "&amp;$expand=Author/ID,Author/Title" +
                "&amp;$filter=(Title eq '" + customerID + "')",
           type: "GET",
           dataType: 'json',
           headers: { "accept": "application/json;odata=verbose" },
           success: function (data) {
               var value = JSON.parse(data.body);
               showNotes(value.d.results);
           },
           error: function (error) { console.log(JSON.stringify(error)) }
       }

    );
}
```

Der folgende Code Fügt einen Hinweis für einen bestimmten Kunden zur Notizenliste.

```C#
function addNoteToList(note, customerID) {
    var executor = new SP.RequestExecutor(appWebUrl);
    var bodyProps = {
        '__metadata': { 'type': 'SP.Data.NotesListItem' },
        'Title': customerID,
        'FTCAM_Description': note
    };
    executor.executeAsync({
        url: appWebUrl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('Notes')/items?@target='" + appWebUrl + "'",
        contentType: "application/json;odata=verbose",
        method: "POST",
        headers: {
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        body: JSON.stringify(bodyProps),
        success: getNotesAndShow,
        error: addNoteFailed
    });
}
```

Sie können 5000 Elemente hinzufügen, um der Liste angezeigt wird, dass die Liste Abfragen, die ein Ergebnis Generieren von 5000 oder mehr Elemente erreicht den Schwellenwert für die Abfrage werden und ein Fehler auftritt. Sie können auch große Menge an Daten hinzufügen, Ihrer Liste der app-Web, dass den Speichergrenzwert für Ihre Websitesammlung überschritten (hängt wie viel Speicher Sie darauf zugewiesen haben). Diese Szenarien zeigen zwei die wichtigsten Nachteile dieses Ansatzes: Abfrage größenbeschränkungen für Nachrichten und Speicherplatz Speichergrenzwerte aufgeführt. Wenn Ihr Unternehmen Ihnen das Arbeiten mit großen Datenmengen und Abfrageresultsets notwendig ist, funktioniert diese Vorgehensweise nicht.

### <a name="list-query-threshold"></a>Schwellenwert für die Liste Abfrage
<a name="bk_listquerythreshold"> </a>

So laden Sie genügend Daten, um die Liste Abfrage Schwellenwert überschritten:


1. Wählen Sie im linken Menü **Beispiel-Homepage**.
    
2. Wählen Sie im Abschnitt **Liste Abfrage Schwellenwerte** **Hinzufügen Listenelemente in der Liste Notizen im App-Web**.
    
3. Pro die Anweisungen, die über der Schaltfläche angezeigt werden, führen Sie diesen Vorgang 10-Mal.
    
    Bei der Aktualisierung der Liste Notizen am oberen Rand der Seite, die angibt, wie viele Listenelemente (Notes) Sie hinzugefügt haben, wird eine Meldung angezeigt, und wie viele sind Links, um Sie hinzuzufügen.
    
    **Hinweis**  Der Vorgang dauert ungefähr einer Minute jedes Mal ausgeführt werden, den Sie die Schaltfläche auswählen. Ausführen des Vorgangs: 10-Mal Ergebnis wird in Abbildung 6 dargestellt.
4. Nachdem Sie die Liste 5,001 Elemente hinzugefügt haben, wählen Sie im linken Menü Notizen. Beim Laden der Seite sehen Sie die Fehlermeldung, die in Abbildung 6, die anhand der SharePoint-REST-API wird angezeigt.
    
    **Abbildung 6. Liste Abfrage Thresold Fehlermeldung überschritten**

    ![Ein Screenshot, der eine Fehlermeldung, die besagt anzeigt, dass der Vorgang der Liste Ansicht Threshol überschritten.](media/90202b64-4b14-4764-9a4c-8fb236f8d10b.png)

5. Wählen Sie **Ansicht Notizenliste im App-Web** und Seite durch die Liste zu sehen, dass sie 500 Zeilen enthält. Beachten Sie, dass zwar SharePoint-Listenansichten Durchsuchen dieses viele Einträge aufnehmen können, die REST-API aufgrund der Drosselung Schwellenwert Listenabfrage fällt aus.
    
### <a name="data-storage-limit"></a>Speichergrenzwert Daten
<a name="bk_listquerythreshold"> </a>

So laden Sie genügend Daten, um die Speichergrenzwerte für Daten überschritten:

1. Wählen Sie im linken Menü **Beispiel-Homepage**.
    
2. Wählen Sie der Schwellenwert für die Daten im Abschnitt **die Liste App-Web-Notizen mit 1 GB Daten zu füllen**.
    
3. Pro die Anweisungen, die über der Schaltfläche zum **Auffüllen der Liste App-Web-Notizen mit 1 GB Daten** angezeigt werden, führen Sie diesen Vorgang 11 Mal.
    
    Bei der Aktualisierung der Liste Notizen am oberen Rand der Seite, die angibt, wie viele Listenelemente (Notes) Sie hinzugefügt haben, wird eine Meldung angezeigt, und wie viele sind Links, um Sie hinzuzufügen.
    
    **Hinweis**  Der Vorgang dauert ungefähr einer Minute jedes Mal ausgeführt werden, den Sie die Schaltfläche auswählen. Ausführen des Vorgangs 11 Mal Ergebnis wird in Abbildung 7 dargestellt.
4. Nach dem Ausführen dieses Vorgangs 11 Mal eine Fehlermeldung tritt auf, wenn Sie die Schaltfläche auswählen wie in Abbildung 7 dargestellt.
    
    **Abbildung 7. Data Storage Schwellenwert überschritten-Fehlermeldung**

    ![Ein Screenshot, der die Fehlermeldung angezeigt, die tritt auf, wenn die Daten überschritten wird](media/0bc55483-0ee1-487a-ba34-e827ec47aadd.png)

5. Nachdem Sie den Speichergrenzwert Daten überschreiten, wählen Sie im Webbrowser die zurück-Schaltfläche, und wählen Sie dann den **Notizen** Link im linken Menü.
    
6. Wählen Sie **Ansicht Notizenliste im App-Web**.
    
    Beim Laden der Seite wird am oberen Rand der Seite, die angibt, dass die Website nicht genügend freier Speicherplatz ist eine Fehlermeldung angezeigt.

## <a name="sharepoint-list-on-the-host-web-support-cases-scenario"></a>SharePoint-Liste auf dem hostweb (Support-Anfragen Szenario)
<a name="sectionSection2"> </a>

Das Support-Anfragen Szenario zeigt Daten, die in einer SharePoint-Liste im hostweb gespeichert ist. In diesem Szenario werden zwei unterschiedliche Muster und interagieren mit den Daten zugreifen. Das erste Muster enthält den SharePoint-Suchdienst, und die vom Inhaltssuche mit einer benutzerdefinierten Anzeigevorlage angewendet. Das zweite Muster enthält ein App-Webpart (Clientwebpart), die eine MVC-Ansicht angezeigt wird, die die **SP verwendet wird RequestExecutor** -Klasse, um die SharePoint-REST-API-aufrufen.

Es gibt mehrere Vorteile der Verwendung von diesem Ansatz:

- Sie können Daten auf einfache Weise mit einfachen REST-Abfragen oder Client-Objektmodellcode Abfragen.
    
- Sie können nach Daten in SharePoint suchen.
    
- Sie können aktualisieren Sie die listenmetadaten und neue Ansichten für eine Liste erstellen, ohne zu aktualisieren und erneutes Bereitstellen der app. Diese Änderungen werden nicht beeinflusst das Verhalten Ihrer App.
    
- Listen auf der Hostwebsite werden nicht gelöscht, wenn Sie Ihre app zu deinstallieren, wenn die app das **AppUninstalled** -Ereignis verwendet, um der Liste entfernen und/oder Löschen der Daten.
    
Versetzen diese Vorteile sind die folgenden Nachteile:

- Die Hostwebsite beschränkt die Datenmenge, die in Listen gespeichert werden können, und die Größe der Ergebnisse der Abfrage. Wenn Ihr Unternehmen benötigt gespeichert und/oder Abfragen großen Datasets, ist dies kein empfohlener Ansatz.
    
- Für komplexe Abfragen führen Listen sowie Datenbanken nicht aus.
    
- Zum Sichern und Wiederherstellen von Daten, führen Sie Listen sowie Datenbanken nicht aus.
    
Die Daten für dieses Szenario werden in einer SharePoint-Liste bereitgestellt, mit der Hostwebsite gespeichert. Daten abgerufen und mithilfe der folgenden angezeigt: 

- Ein [Inhaltssuche-Webpart](https://msdn.microsoft.com/en-us/library/office/jj163789%28v=office.15%29.aspx).
    
- Ein app-Webpart, das als Model-View-Controller Ansicht implementiert wird. 
    
Der Code in dieser Ansicht verwendet REST-Abfragen zum Abrufen von Informationen aus der Liste, während das Inhaltssuche-Webpart den SharePoint-Suchdienst verwendet, um die Daten abzurufen. Die zwei Ansätze veranschaulichen den bedeutenden Vorteil dieser Option: Sie können den Suchdienst und den REST/CSOM-APIs verwenden, um Informationen aus einer Liste auf dem hostweb abzurufen.

Wenn Sie einen Kunden aus der Unterstützung von Fällen Dropdown-Liste auswählen, sehen Sie die Groß-/Kleinschreibung Support-Daten für dieses Kunden anzeigen in das Webpart und das app-Webpart (Abbildung 8) angezeigt. Das Webpart möglicherweise nicht sofort, Inhalte zurück, da bis zu 24 Stunden für den SharePoint-Suchdienst dauert, die Daten zu indizieren. Sie können auch den Link **Ansicht Support Fällen Liste im Hostweb** um eine herkömmliche Ansicht der Listendaten anzuzeigen.

**Abbildung 8. Benutzeroberfläche für den Support-Fall**

![Ein Screenshot der Benutzeroberfläche für die Interaktion mit den Support-Fall](media/eac41f5c-90b7-4fe3-b47e-0d65b79cbf1c.png)

Das Inhaltssuche-Webpart bereitgestellt, die diese App verwendet eine benutzerdefinierte Anzeige-Vorlage. Abbildung 9 zeigt im Verzeichnis **Anlagen** des Webprojekts finden Sie auf das Webpart und die zugeordnete Vorlage.

**Abbildung 9. Inhalt des Verzeichnisses Anlagen des Webprojekts**

![Screenshot des Verzeichnisses Objekte](media/95db9118-9e56-4e39-84b1-271e54447792.png)

Der folgende JavaScript-Code, den finden Sie in der Datei Views/SupportCaseAppPart\Index.cshtml mithilfe die domänenübergreifenden Bibliothek eine REST-Abfrage für die SharePoint-Liste auf dem hostweb aufgerufen. 

```C#
function execCrossDomainRequest() {
var executor = new SP.RequestExecutor(appWebUrl);

executor.executeAsync(
   {
        url: appWebUrl + "/_api/SP.AppContextSite(@@target)" +
                "/web/lists/getbytitle('Support Cases')/items" +
              "?$filter=(FTCAM_CustomerID eq '" + customerID + "')" +
            "&amp;$top=30" +
                    "&amp;$select=Id,Title,FTCAM_Status,FTCAM_CSR" +
                    "&amp;@@target='" + hostWebUrl + "'",
method: "GET",
              headers: { "Accept": "application/json; odata=verbose" },
              success: successHandler,
              error: errorHandler
   }
);
}
```

Sie können 5000 Elemente hinzufügen, um der Liste angezeigt wird, dass die Liste Abfragen, die ein Ergebnis Generieren von 5000 oder mehr Elemente erreicht den Schwellenwert für die Abfrage werden und ein Fehler auftritt. In diesem Szenario wird ein wichtigste Nachteil dieser Vorgehensweise: Auflisten der Abfrage größenbeschränkungen für Nachrichten. Wenn Ihr Unternehmen Ihnen das Arbeiten mit großen Datenmengen und Abfrageresultsets notwendig ist, funktioniert diese Vorgehensweise nicht. Weitere Informationen finden Sie unter [Liste Abfrage Schwellenwert](#bk_listquerythreshold) weiter oben in diesem Artikel.

## <a name="northwind-odata-web-service-customer-dashboard-scenario"></a>Northwind-OData-Webdienst (Kunden-Dashboard Szenario)
<a name="sectionSection3"> </a>

Das Kunden-Dashboard-Szenario wird JQuery AJAX zum Aufrufen des NorthWind OData-Diensts zum Zurückgeben von Kundeninformationen verwendet. Die app speichert seine Daten in einem Webdienst, und klicken Sie dann [OData](http://www.odata.org/) verwendet, um es abzurufen.

Im folgenden sind die Vorteile der Verwendung von diesem Ansatz:

- Ein bestimmten Webdienst kann mehrere Add-Ins unterstützen.
    
- Sie können den Webdienst aktualisieren, ohne zu aktualisieren und erneut bereitstellen Ihrer app.
    
- Ihre SharePoint und Web-Service-Installationen wirken sich nicht voneinander.
    
- Hosten Dienste, wie Microsoft Azure ermöglichen es Ihnen, die Webdienste zu skalieren.
    
- Sie können sichern und Wiederherstellen von Informationen auf Ihre Webdienste separat aus Ihrer SharePoint-Website.
    
- Sie verloren nicht Daten, wenn Ihre app zu deinstallieren, es sei denn, die app das **AppUninstalled** -Ereignis verwendet, um die Daten zu löschen.
    
Dashboard Kundenszenarien speichert seine Daten in einem Webdienst, der zum Abrufen der Daten des OData-Standards implementiert. In der Benutzeroberfläche des Kunden-Dashboard wählen Sie einen Kunden aus einem Dropdown-Menü und Informationen Kundenanzeige im Bereich **Kundeninformationen** .

Auf dieser Seite Benutzeroberfläche ist eine Model-View-Controller-Ansicht. Die Anzeige wird in der Datei Views/CustomerDashboard\Home.cshtml definiert. Der zugrunde liegende Code ist in der Datei Scripts/CustomerDashboard.js. Der JavaScript-Code verwendet AJAX, um die Northwind-Webdienst abzufragen. Da dies ein OData-Dienst ist, besteht aus den Webdienstabfrage Abfragezeichenfolgenargumente, eine URL für einen Webdienst-Endpunkt zugeordnet ist. Der Dienst gibt Kundeninformationen im JSON-Format zurück.

Mit dem folgende Code wird ausgeführt, wenn Sie den Link **Kunden-Dashboard** auswählen. Die Namen der Kunden und IDs, um das Dropdown-Menü Auffüllen abgerufen.

```C#
var getCustomerIDsUrl = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json&amp;$select=CustomerID";
    $.get(getCustomerIDsUrl).done(getCustomerIDsDone)
        .error(function (jqXHR, textStatus, errorThrown) {
            $('#topErrorMessage').text('Can\'t get customers. An error occurred: ' + jqXHR.statusText);
        });
```

Mit dem folgende Code wird ausgeführt, wenn Sie einen Kundennamen aus dem Dropdown-Menü auswählen. Das OData **$filter** -Argument verwendet, um die Kunden-ID und andere Abfragezeichenfolgenargumente zum Abrufen von Informationen im Zusammenhang mit diesen Kunden angeben.

```C#
var url = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json" +  "&amp;$select=CustomerID,CompanyName,ContactName,ContactTitle,Address,City,Country,Phone,Fax" + "&amp;$filter=CustomerID eq '" + customerID + "'";

$.get(url).done(getCustomersDone)
   .error(function (jqXHR, textStatus, errorThrown) {
          alert('Can\'t get customer ' + customerID + '. An error occurred: ' + 
                 jqXHR.statusText);
});
```

## <a name="azure-table-storage-customer-service-survey-scenario"></a>Azure-tabellenspeicherung (Customer Service Umfrage Szenario)
<a name="sectionSection4"> </a>

Das Dienst Umfrage Szenario ermöglicht dem Kunden Mitarbeiter zu ihrer Bewertung basierend auf Kundenumfragen finden Sie unter und Azure-tabellenspeicherung und der Microsoft.WindowsAzure.Storage.Table.CloudTable-API zum Speichern und interagieren mit den Daten verwendet.

Im folgenden sind die Vorteile der Verwendung von diesem Ansatz:

- Azure-Speichertabellen unterstützen mehr als eine app.
    
- Sie können die Azure-Speichertabellen aktualisieren, ohne zu aktualisieren und erneut bereitstellen Ihrer app.
    
- Ihre SharePoint-Installation und Azure-Speichertabellen haben keine Auswirkung auf die Leistung des jeweils anderen.
    
- Azure-Speicher Tabellen horizontal ganz einfach.
    
- Sie können sichern und Wiederherstellen die Azure-Speichertabellen separat von Ihrer SharePoint-Website.
    
- Sie verloren keine Daten, wenn Sie Ihre app zu deinstallieren, es sei denn, die app das **AppUninstalled** -Ereignis verwendet, um die Daten zu löschen.
    
Die app-Schnittstelle des aktuellen Benutzers Umfrage Bewertung in der Center-Seite angezeigt. Wenn die Azure-Speicher-Tabelle leer ist, wird die app einige Informationen zur Tabelle hinzufügen, bevor es angezeigt.

Der folgende Code aus der CSRInfoController.cs definiert die **Start** -Methode, die der Benutzer **NameId**abruft.

```C#
[SharePointContextFilter]
public ActionResult Home()
{
    var context = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);
    var sharePointService = new SharePointService(context);
    var currentUser = sharePointService.GetCurrentUser();
    ViewBag.UserName = currentUser.Title;

    var surveyRatingsService = new SurveyRatingsService();
    ViewBag.Score = surveyRatingsService.GetUserScore(currentUser.UserId.NameId);

    return View();
}
```

Der folgende Code aus der Datei SurveyRatingService.cs definiert den **SurveyRatingsService** -Konstruktor Einrichten der Verbindung mit dem Azure-Speicher-Konto festgelegt.

```C#
public SurveyRatingsService(string storageConnectionStringConfigName = 
        "StorageConnectionString")
{
    var connectionString = Util.GetConfigSetting("StorageConnectionString");
    var storageAccount = CloudStorageAccount.Parse(connectionString);

    this.tableClient = storageAccount.CreateCloudTableClient();
    this.surveyRatingsTable = this.tableClient.GetTableReference("SurveyRatings");
    this.surveyRatingsTable.CreateIfNotExists();
}
```

Der folgende Code aus der gleichen Datei definiert die **GetUserScore** -Methode, die aus der Tabelle Azure-Speicher des Benutzers Umfrage Score abruft.

```C#
public float GetUserScore(string userName)
{
    var query = new TableQuery<Models.Customer>()
    .Select(new List<string> { "Score" })
    .Where(TableQuery.GenerateFilterCondition("Name", 
    QueryComparisons.Equal, userName));

    var items = surveyRatingsTable
         .ExecuteQuery(query)
             .ToArray();

    if (items.Length == 0)           
    return AddSurveyRatings(userName);

    return (float)items.Average(c => c.Score);
}
```

Wenn die Tabelle keine Umfragedaten im Zusammenhang mit den aktuellen Benutzer enthält, weist die **AddSurveyRating** -Methode nach dem Zufallsprinzip eine Bewertung für den Benutzer.

```C#
private float AddSurveyRatings(string userName)
{
    float sum = 0;
    int count = 4;
    var random = new Random();

    for (int i = 0; i < count; i++)
    {
    var score = random.Next(80, 100);
    var customer = new Models.Customer(Guid.NewGuid(), userName, score);

    var insertOperation = TableOperation.Insert(customer);
    surveyRatingsTable.Execute(insertOperation);

    sum += score;
    }
    return sum / count;
}
```

## <a name="azure-queue-storage-customer-call-queue-scenario"></a>Azure Warteschlangenspeicher (Customer aufrufen Warteschlange Szenario)
<a name="sectionSection5"> </a>

Das Szenario Customer aufrufen Warteschlange aufgelistet Anrufer in der Warteschlange Support und simuliert Nachrichtenempfang Anrufe. Das Szenario wird Warteschlangen Azure-Speicher zum Speichern von Daten und die **Microsoft.WindowsAzure.Storage.Queue.CloudQueue** API mit Model-View-Controller verwendet.

Im folgenden sind die Vorteile der Verwendung von diesem Ansatz:

- Azure-Speicher Warteschlangen unterstützen mehr als eine app.
    
- Sie können die Warteschlangen Azure-Speicher aktualisieren, ohne zu aktualisieren und erneut bereitstellen Ihrer app.
    
- Ihre SharePoint-Installation und Azure-Speicher Warteschlangen haben keine Auswirkung auf die Leistung des jeweils anderen.
    
- Azure-Speicher Warteschlangen skalieren einfach.
    
- Sie können sichern und Wiederherstellen die Azure-Speicher Warteschlangen separat von Ihrer SharePoint-Website.
    
- Sie verloren keine Daten, wenn Sie Ihre app zu deinstallieren, es sei denn, die app das **AppUninstalled** -Ereignis verwendet, um die Daten zu löschen.
    
Die app-Schnittstelle angezeigt ein Anruf Supportgruppe im mittleren Bereich, wenn Sie den Link **Aufrufen Warteschlange** auswählen. Simulieren Sie den Empfang von Anrufen (Hinzufügen eines Anrufs an die Warteschlange), indem **Simulieren Anrufe**auswählen, und nutzen den ältesten Anruf (entfernen einen Anruf aus der Warteschlange) können Sie durch Auswählen der **Anruf annehmen** Aktion in Verbindung mit einem bestimmten Anruf simulieren.

Diese Seite ist eine Model-View-Controller-Ansicht, die in der Datei Views\CallQueue\Home.cshmtl definiert ist. Die Datei Controllers\CallQueueController.cs definiert die **CallQueueController** -Klasse, die Methoden zum Abrufen aller Anrufe in die Warteschlange enthält, einen Anruf an die Warteschlange (simulieren eines Anrufs) hinzufügen und Entfernen von einen Anruf aus der Warteschlange (einen Anruf nutzen). Jeder der folgenden Methoden ruft Methoden in der Datei Services\CallQueueService.cs, die die Azure-Speicher-Warteschlange API verwendet, um die zugrunde liegenden Informationen in der Speicherwarteschlange abrufen definiert.

```C#
public class CallQueueController : Controller
{
    public CallQueueService CallQueueService { get; private set; }

    public CallQueueController()
    {
        CallQueueService = new CallQueueService();
    }

    // GET: CallQueue
    public ActionResult Home(UInt16 displayCount = 10)
    {
        var calls = CallQueueService.PeekCalls(displayCount);
        ViewBag.DisplayCount = displayCount;
        ViewBag.TotalCallCount = CallQueueService.GetCallCount();
        return View(calls);
    }

    [HttpPost]
    public ActionResult SimulateCalls(string spHostUrl)
    {
        int count = CallQueueService.SimulateCalls();
        TempData["Message"] = string.Format("Successfully simulated {0} calls and added them to the call queue.", count);
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }

    [HttpPost]
    public ActionResult TakeCall(string spHostUrl)
    {
        CallQueueService.DequeueCall();
        TempData["Message"] = "Call taken successfully and removed from the call queue!";
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }
}
```

Die CallQueueService.cs-Datei definiert die **CallQueueService** -Klasse, die an die Warteschlange Azure-Speicher die Verbindung herstellt. Diese Klasse enthält auch die Methoden zum Hinzufügen, entfernen (entfernen) und der Aufrufe aus der Warteschlange abruft.

```C#
public class CallQueueService
{
    private CloudQueueClient queueClient;

    private CloudQueue queue;

    public CallQueueService(string storageConnectionStringConfigName = "StorageConnectionString")
    {
        var connectionString = CloudConfigurationManager.GetSetting(storageConnectionStringConfigName);
        var storageAccount = CloudStorageAccount.Parse(connectionString);

        this.queueClient = storageAccount.CreateCloudQueueClient();
        this.queue = queueClient.GetQueueReference("calls");
        this.queue.CreateIfNotExists();
        }

        public int? GetCallCount()
        {
        queue.FetchAttributes();
        return queue.ApproximateMessageCount;
    }

    public IEnumerable<Call> PeekCalls(UInt16 count)
    {
        var messages = queue.PeekMessages(count);

        var serializer = new JavaScriptSerializer();
        foreach (var message in messages)
        {
        Call call = null;
        try
        {
        call = serializer.Deserialize<Call>(message.AsString);
        }
        catch { }

        if (call != null) yield return call;
        }
    }

    public void AddCall(Call call)
    {
        var serializer = new JavaScriptSerializer();
        var content = serializer.Serialize(call);
        var message = new CloudQueueMessage(content);
        queue.AddMessage(message);
    }

    public void DequeueCall()
    {
        var message = queue.GetMessage();
        queue.DeleteMessage(message);
    }

    public int SimulateCalls()
    {
        Random random = new Random();
        int count = random.Next(1, 6);
        for (int i = 0; i < count; i++)
        {
        int phoneNumber = random.Next();
        var call = new Call
        {
        ReceivedDate = DateTime.Now,
        PhoneNumber = phoneNumber.ToString("+1-000-000-0000")
        };
        AddCall(call);

        return count;
    }
}
```

## <a name="sql-azure-database-recent-orders-scenario"></a>SQL Azure-Datenbank (aktuellen Aufträge Szenario)
<a name="sectionSection6"> </a>

Das aktuellen Aufträge Szenario verwendet einen direkten Aufruf der Northwind SQL Azure-Datenbank, um alle Aufträge für einen bestimmten Kunden zurückzugeben.

Im folgenden sind die Vorteile der Verwendung von diesem Ansatz:

- Eine Datenbank kann mehrere app unterstützen.
    
- Sie können das Datenbankschema aktualisieren, ohne dass aktualisieren und erneut bereitstellen Ihrer app, solange die Schemaversion Abfragen in Ihrer app keine Auswirkung auf.
    
- Eine relationale Datenbank kann n: n-Beziehungen unterstützt und daher die komplexere Geschäftsszenarien unterstützen.
    
- Datenbank-Designtools können Sie um den Entwurf Ihrer Datenbank zu optimieren.
    
- Relationale Datenbanken bieten eine bessere Leistung als die anderen Optionen, wenn Sie komplexe Vorgänge in Abfragen, wie etwa Berechnungen und Joins ausführen müssen.
    
- Eine SQL Azure-Datenbank können Sie zum Importieren und Exportieren von Daten auf einfache Weise, daher es einfacher ist zu verwalten und Ihre Daten zu verschieben.
    
- Sie verloren keine Daten, wenn Sie Ihre app zu deinstallieren, wenn die app das **AppUninstalled** -Ereignis verwendet, um die Daten zu löschen.
    
Die letzte Orders Schnittstelle funktioniert ähnlich wie die Kunden-Dashboard-Schnittstelle. Sie wählen Sie auf den Link **Aktuellen Aufträge** in der linken Spalte aus, und wählen Sie dann im Dropdown-Menü am oberen Rand der mittleren Bereich ein Kunden. Eine Liste der Aufträge dieses Kunden anzeigen wird im mittleren Bereich angezeigt.

Diese Seite ist eine Model-View-Controller-Ansicht in der Datei Views\CustomerDashboard\Orders.cshtml definiert. Code in der Datei Controllers\CustomerDashboardController.cs verwendet das [Entity Framework](https://msdn.microsoft.com/en-us/data/ef.aspx) zum Abfragen der **Orders** -Tabelle in SQL Azure-Datenbank. Die Kunden-ID wird mithilfe der in der URL, die übergeben wird, wenn der Benutzer einen Kunden aus dem Dropdown-Menü auswählt einen Abfragezeichenfolgen-Parameter übergeben. Die Abfrage erstellt eine Verknüpfung für die Tabellen **Kunden**, **Lieferanten** und **Mitarbeiter**. Das Abfrageergebnis wird dann an die Model-View-Controller-Ansicht übergeben, die die Ergebnisse angezeigt werden.

Der folgende Code aus der Datei CustomerDashboardController.cs Datenbankabfrage ausführt und gibt die Daten zur Ansicht zurück.

```C#
public ActionResult Orders(string customerId)
{            
    Order[] orders;
    using (var db = new NorthWindEntities())
    {
            orders = db.Orders
                  .Include(o => o.Customer)
                  .Include(o => o.Employee)
                  .Include(o => o.Shipper)
                  .Where(c => c.CustomerID == customerId)
                  .ToArray();
    }

    ViewBag.SharePointContext = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);

    return View(orders);
}
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Zusammengesetzte Business-add-ins für SharePoint 2013 und SharePoint Online](Composite-buisness-apps-for-SharePoint.md)
    
-  [Office 365-Entwicklungsmuster und -übungen auf GitHub](https://github.com/SharePoint/PnP)
