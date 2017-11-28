---
title: "Durchsuchen von Anpassungen für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c8afb3e0589e65e100ca3512926e931e966e510a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="search-customizations-for-sharepoint"></a>Durchsuchen von Anpassungen für SharePoint

Erstellen Sie benutzerdefinierte SharePoint 2013 und SharePoint Online-Suche Szenarien mithilfe von suchbasierten Websiteverzeichnis und eine personalisierte Suche, oder suchen Sie Konfiguration Portabilität. 

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

## <a name="search-based-site-directory"></a>Suchbasierte Websiteverzeichnis

SharePoint-Suche können Sie eine suchbasierte Websiteverzeichnis ohne Schreiben von benutzerdefiniertem Code erstellen. 

So erstellen Sie ein Websiteverzeichnis

1. Erstellen der Website Directory Anzeigevorlagen.
    
2. Definieren Sie den Site Directory Ergebnistyp.
    
3. Erstellen der Ergebnisseite an.
    
4. Bearbeiten Sie die Eigenschaften des Suchergebnisse-Webpart.
    
Zum Erstellen der Website Directory Anzeigevorlagen:

**Hinweis:**  Dieses Verfahren verwendet die Website bezogenen Anzeigevorlagen unverändert. Wenn Sie ändern, wie Site Directory Ergebnisse angezeigt werden, ändern die Anzeigevorlagen, die Sie erstellen möchten.

1. Öffnen Sie das den **Gestaltungsvorlagenkatalog**zugeordnetes Netzwerklaufwerk. Weitere Informationen finden Sie unter [wie: Zuordnen eines Netzlaufwerks zum SharePoint 2013 Master Page Gallery](http://msdn.microsoft.com/en-us/library/office/jj733519%28v=office.15%29.aspx).
    
2. Erstellen Sie Kopien der Anzeigevorlage HTML-Dateien, die am besten zuordnen, was Sie tun möchten. Für die Website verzeichnisszenario wird dies Item_Site.html und Item_Site_HoverPanel.html sein. Beide Dateien befinden sich der `\Display Templates\Search` Ordner in der zugeordnetes Netzwerklaufwerk.
    
3. Benennen Sie die Kopien, die Sie der Item_SiteDirectory.html und Item_SiteDirectory_HoverPanel.html-Dateien vorgenommen, wie dargestellt.
    
    **Abbildung 1. Site Directory Anzeigevorlagen**

    ![Site Directory Anzeigevorlagen](media/search-customizations-for-sharepoint/4c084d31-bad4-45f0-950b-ba214f9487f7.png)

4. Öffnen Sie die Datei Item_SiteDirectory.html, und stellen Sie wie folgt geändert:
    
    - Ändern der `<title>` Wert von "Websiteelements" bis "Websiteverzeichnis" markieren.
    
    - Ändern Sie die erste `<div>` Tag nach dem öffnenden `<body>` Markieren von `<div id="Item_Site">` auf `<div id="Item_SiteDirectory">`.
    
    - Ändern der beim Daraufzeigen Systemsteuerung Vorlage JavaScript-Datei des Anzeigenamens von: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_Site_HoverPanel.js";`an:`var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_SiteDirectory_HoverPanel.js";`
    
5. Öffnen Sie die Datei Item_SiteDirectory_HoverPanel.html, und stellen Sie wie folgt geändert:
    
    - Ändern der `<div>` Tag nach dem öffnenden `<body>` markieren aus: `<title>Site Hover Panel Test</title>`an:`<title>Site Directory Hover Panel</title>`
    
    - Ändern der `<title>` markieren aus: `<div id="Item_Site_HoverPanel">`an:`<div id="Item_SiteDirectory_HoverPanel">`
    
So definieren Sie den Website Directory Ergebnistyp

1. Wechseln Sie zu **Websiteeinstellungen** > **Suche** > **Ergebnistypen**, und klicken Sie dann auf **Neuer Ergebnistyp**.
    
2. Name des neuen Ergebnistyps "Grundlegende Websiteverzeichnis".
    
3. In der **wie sollen diese Ergebnisse aussehen?** **Websiteverzeichnis**wählen Sie im Feld.
    
    **Abbildung 2. Ergebnis Standortkonfiguration**

    ![Beispiel für Ergebnis Standortkonfiguration](media/search-customizations-for-sharepoint/4f42a7c4-326b-4508-b9a7-e030ef34cd33.png)

4. Wählen Sie **Speichern**aus.
    
Auf die Ergebnisseite zu erstellen:

1. Klicken Sie im Menü **Einstellungen** **auf Websiteinhalte**.
    
2. Wählen Sie **Seiten**.
    
3. Wählen Sie in der Bibliothek für **Seiten** , **Dateien** > **Neues Dokument** > **Seite**.
    
4. Geben Sie auf der Seite **Seite erstellen** "Websiteverzeichnis" für den **Titel** und "Sitedirectory" für **URL-Name**.
    
5. Wählen Sie **Erstellen**.
    
So bearbeiten Sie die Eigenschaften des Suchergebnisse-Webpart

1. Wählen Sie auf der Seite **Websiteverzeichnis** **Einstellungen** > **Seite bearbeiten**.
    
2. Wählen Sie in den **Suchergebnisse-Webpart**im **Webpart** -Menü, und wählen Sie dann auf **Webpart bearbeiten**.
    
    **Abbildung 3. Webpart-Menü**

    ![Abb. 3](media/search-customizations-for-sharepoint/1b01ac59-3bc1-42eb-a63d-61c2ad15cee4.png)

3. Wählen Sie im Webpart-Toolbereich **Abfrage ändern** , um den Abfrage-Generator zu öffnen.
    
4. Geben Sie im Feld **Abfragetext** Folgendes ein:`ContentClass:STS_Web OR ContentClass:STS_Site path:http://<YourServer>`
    
5. Wählen Sie die **Abfrage testen** zu bestätigen, dass die Syntax korrekt ist. **Search Results** Vorschaubereich sollte Unterwebsites der Website angezeigt werden, die Sie für den _Pfad_ des **Abfragetext**angegeben.
    
    **Abbildung 4. Search Results-Webpart-Abfrage-Generator**

    ![Search Results Webpart Abfrage-Generator](media/search-customizations-for-sharepoint/7b55c821-4772-4874-bbcb-c757e2723599.png)

6. Wählen Sie **OK** , um den Abfrage-Generator zu schließen.
    
7. Wählen Sie im **Anzeigevorlagen** **Ergebnistypen zum Anzeigen von Elementen verwenden**.
    
8. Wählen Sie in der Dropdownliste **Ergebnistyp für Artikel** **Grundlegende Websiteverzeichnis** .
    
9. Klicken Sie im Abschnitt **Darstellung** ändern Sie den **Titel** in "sind Websites ich Zugriff auf".
    
10. Wählen Sie **OK** , um die Änderungen am Webpart zu speichern und schließen den Webpart-Toolbereich. Die folgende Abbildung zeigt ein Beispiel für eine suchbasierte Directory Websiteseite.
    
    **Abbildung 5. Beispiel für Contoso suchbasierte Website-Verzeichnis**

    ![Beispiel für Contoso suchbasierte Website-Verzeichnis](media/search-customizations-for-sharepoint/5d1317d5-2e82-4819-b5a4-5bb515898a7b.png)

## <a name="personalized-search-results"></a>Personalisierte Suchergebnisse

Personalisierte Suche ist beim Anzeigen von Suchergebnissen angegeben, an den Benutzer senden von der Suchanfrage vorgesehen sind. Dieser Abschnitt beschreibt einige Szenarien für personalisierte Such- und wie Sie sie implementieren können.

### <a name="your-news-scenario"></a>Die News-Szenario

In diesem Szenario erstellen Sie ein Search-add-in, das relevante Inhalte, wie Nachrichten und Ereignisse, geplant, für den Benutzer anzeigt.

**Abbildung 6. Ihr News personalisierte Search-Szenario**

![Ihr News personalisierte Search-Szenario](media/search-customizations-for-sharepoint/188af4d1-b8bb-4212-bfdb-c29a13f30286.png)

Um die News-Szenario zu implementieren, mit der die SharePoint-Suchergebnisse-Webparts und Anzeigevorlagen standardmäßig die News-Informationen, einschließlich Titel, Beschreibung und rollupbild angezeigt. Die ersten 10 Elemente News anzeigen. Wenn der Benutzer die rollupbild, Titel oder mehr lesen Link klickt, wird die Seite Neuigkeiten Artikel geladen.

Alternativ können Sie eine Suche-add-Ins mithilfe der Abfrage-API (CSOM oder REST) erstellen. Sie können die Anzahl der Nachrichtenelementen anzuzeigende mithilfe des add-ins Sucheigenschaften konfigurierbar machen.

Eine weitere Option ist mit der Abfrage-API die Abfrage-API-Code hinzufügen, der die Suchergebnisse direkt auf das Seitenlayout abruft.

News und Ereignis Informationen, die speziell für den Benutzer angezeigt:

1. Ändern der Abfrage zum Filtern von Nachrichten und Ereignis Ergebnisse basierend auf Benutzerprofileigenschaften wie Unternehmenseinheit, Region und Sprache.
    
2. Abrufen der Titel, Beschreibung, rollupbild und URL-Eigenschaften für die Elemente News oder Ereignis.
    
3. Sortieren der Logik für die kombinierte Neuigkeiten und Ereignisse, die auf Basis der **LastModifiedDate** -Eigenschaft implementieren.

### <a name="upcoming-events-scenario"></a>Anstehende Ereignisse-Szenario

In diesem Szenario zeigt die Search-add-ins relevanten Ereignisse geplant, für den Benutzer.

**Abbildung 7. Anstehende Ereignisse personalisierte Search-Szenario**

![Anstehende Ereignisse personalisierte Search-Szenario](media/search-customizations-for-sharepoint/35afac63-b4e9-4d94-abc1-a5fa11cc2dbf.png)

Zum Implementieren dieses Szenarios können Sie die SharePoint-Suchergebnisse-Webpart so ändern Sie die Abfrage aus, um nur in Kürze verfügbare Ereignisinformationen abrufen konfigurieren. Geben Sie hierzu `ContentClass:STS_ListItem_Events` für das Webpart Abfragetext. Erstellen Sie zum Ändern der Anzeige von Ereignis tritt auf, benutzerdefinierte Anzeigevorlagen, um die Ereignisinformationen zu rendern.

Sie können die elementanzeigevorlage ändern, sodass, wenn der Benutzer das Bild, Titel oder mehr lesen Link auswählt, die Informationsseite Ereignis geladen wird. Sie können auch die Steuerelement-Anzeigevorlage ändern, sodass die nächsten 10-Ereignisergebnisse im Webpart, wenn der Benutzer **Weitere**auswählt angezeigt werden.

Sie können auch ein Search-add-in erstellen, die die Abfrage-API verwendet, sogar Ergebnisse abzurufen. Sie können das Search-add-in, um anzuzeigen, werden standardmäßig nur 10 der neuesten anstehende Ereignisse, aber stellen Sie diese Einstellung über die Add-in-Sucheigenschaften konfigurierbar konfigurieren. 

### <a name="featured-news-scenario"></a>Empfohlene News-Szenario

In diesem Szenario Suchergebnisse der Suche-add-Ins dargestellt als Ziel für die Benutzer an Stellen wie Unternehmensintranet und Abteilungen Angebotsseiten Empfohlener Inhalt. Sie können dies mit einem Webpart-Add-in implementieren, die eine jQuery-Plug-in mit HTML-Code enthält, die der Search REST-Dienst oder die CSOM-Abfrage zum Abrufen von Suchergebnissen aus SharePoint und Anzeigen der Ergebnisse verwendet.

### <a name="code-sample-for-personalized-search"></a>Codebeispiel für personalisierte Suche

Die [SharePoint 2013: Personalisieren von Suchergebnisse in ein SharePoint-Add-in](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9) Beispiel zeigt ein Beispiel für einfache Suche und eine personalisierte Suchergebnisse Beispiel, die die Suchabfrage CSOM verwendet wird. Im Beispiel einfache Suche kann den Benutzer, die einen Suchfilter für einen Mandanten geltende Suche bereitstellen. Websites werden basierend auf den benutzerdefinierten Filter durchsucht.

Im Beispiel wird zunächst SharePoint Kontext mithilfe der **SharePointContextProvider** -Klasse.

```
var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
```

Im nächsten Schritt wird die Abfrage basierend auf der Benutzereingabe erstellt. Es beschränkt die Abfrage für Websitesammlungen und ruft dann die **ProcessQuery** -Methode, die den Kontext und die Abfrage im Methodenaufruf übergeben. Anschließend wird, dass die Ergebnisse **ProcessQuery** dementsprechend Tabelle die dann von der **FormatResults** -Methode analysiert, zurückgegeben.

```
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    string query = searchtext.Text + " contentclass:\"STS_Site\"";
    ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
    lblStatus1.Text = FormatResults(results);
}
```

Die **ProcessQuery** -Methode erstellt ein **KeywordQuery** -Objekt, das die Suchabfrage darstellt.

```
KeywordQuery keywordQuery = new KeywordQuery(ctx);
keywordQuery.QueryText = keywordQueryValue;
keywordQuery.RowLimit = 500;
keywordQuery.StartRow = 0;
keywordQuery.SelectProperties.Add("Title");
keywordQuery.SelectProperties.Add("SPSiteUrl");
keywordQuery.SelectProperties.Add("Description");
keywordQuery.SelectProperties.Add("WebTemplate");
keywordQuery.SortList.Add("SPSiteUrl", Microsoft.SharePoint.Client.Search.Query.SortDirection.Ascending);
```

Die Suchabfrage wird dann in SharePoint durch Aufrufen der Methode **ExecuteQuery_Client(Query)** versendet. Die Ergebnisse zurückgegeben werden, die **ClientResult < T&gt; ** Objekt.

```
SearchExecutor searchExec = new SearchExecutor(ctx);
ClientResult<ResultTableCollection> results = searchExec.ExecuteQuery(keywordQuery);
ctx.ExecuteQuery();
```

Die **FormatResults** -Methode durchlaufen und die Ergebnisse und erstellt eine HTML-Tabelle, um die Ergebniswerte anzuzeigen.

```
string responseHtml = "<h3>Results</h3>";
responseHtml += "<table>";
responseHtml += "<tr><th>Title</th><th>Site URL</th><th>Description</th><th>Template</th></tr>";
if (results.Value[0].RowCount > 0)
{
 foreach (var row in results.Value[0].ResultRows)
 {
   responseHtml += "<tr>";
   responseHtml += string.Format("<td>{0}</td>", row["Title"] != null ? row["Title"].ToString() : "");
   responseHtml += string.Format("<td>{0}</td>", row["SPSiteUrl"] != null ? row["SPSiteUrl"].ToString() : "");
   responseHtml += string.Format("<td>{0}</td>", row["Description"] != null ? row["Description"].ToString() : "");
   responseHtml += string.Format("<td>{0}</td>", row["WebTemplate"] != null ? row["WebTemplate"].ToString() : "");
   responseHtml += "</tr>";
 }
}
responseHtml += "</table>";
```

"Apptesten" überprüft die **ResolveAdditionalFilter** -Methode. Wenn sie gefunden wird, wird eine Liste mit Websitevorlagen eines beliebigen Typs in den Suchergebnissen zurückgegeben. Wenn es nicht gefunden wird, werden nur STS Webvorlagen in den Suchergebnissen zurückgegeben.

```
private string ResolveAdditionalFilter(string aboutMeValue)
{
    if (!aboutMeValue.Contains("AppTest"))
    {
        return "WebTemplate=STS";
    }
    return "";
}
```

Im Beispiel wird dann die Abfrage erstellt und ruft die **ProcessQuery** und **FormatResults** Methoden zum Abrufen, Format, und die Suchergebnisse angezeigt.

```
string query = "contentclass:\"STS_Site\" " + templateFilter;
ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
lblStatus2.Text = FormatResults(results);
```

Sie können die Benutzeroberfläche für die in diesem Beispiel wird in der folgenden Abbildung sehen.

**Abbildung 8. Personalisierte Suchergebnisse Beispiel-UI**

![Personalisierte Suchergebnisse Beispiel-UI](media/search-customizations-for-sharepoint/8e1c412b-71a7-42e2-b9f3-b7d045df3bde.png)

## <a name="search-configuration-portability"></a>Suche Konfiguration Portabilität

In SharePoint 2013 und SharePoint Online können Sie exportieren und importieren angepasster suchkonfigurationseinstellungen zwischen Websitesammlungen und Websites. Sie können nur exportieren angepasster suchkonfigurationseinstellungen auf der Ebene Search Service Application (SSA), und Sie müssen die Suche APIs programmgesteuert dazu verwenden. Die Export-Option ist nicht in der SharePoint-UI verfügbar.

Die [SharePoint 2013: Import und Export der sucheinstellungen für SharePoint Online](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac) Beispiel gezeigt, wie Sie zum Importieren und Exportieren von sucheinstellungen für eine SharePoint Online-Website verwenden des Suchdiensts CSOM in eine Konsolenanwendung.

### <a name="configuration-settings-that-are-portable"></a>Konfigurationseinstellungen, die portabel sind

Beim Exportieren angepasster suchkonfigurationseinstellungen erstellt SharePoint 2013 eine suchkonfigurationsdatei im XML-Format. Mit dieser Konfigurationsdatei Suche enthält alle exportierbar suchkonfigurationseinstellungen auf SSA, Websitesammlung oder der Websiteebene aus, in dem Sie den Export starten. Eine suchkonfigurationsdatei für eine Websitesammlung enthält keine suchkonfigurationseinstellungen aus den einzelnen Standorten innerhalb der Websitesammlung.

Beim Importieren einer suchkonfigurationsdatei SharePoint 2013 erstellt und aktiviert jede benutzerdefinierte suchkonfigurationseinstellung in der Websitesammlung oder Website aus, in dem Sie den Import starten.

In Tabelle 1 werden die Einstellungen, die Sie exportieren und importieren können und Abhängigkeiten von anderen angepassten suchkonfigurationseinstellungen. Wenn eine benutzerdefinierte suchkonfigurationseinstellung auf einer anderen Ebene die suchkonfigurationseinstellungen abhängen, müssen Sie exportieren und Importieren von Einstellungen in allen relevante Ebenen.

**In Tabelle 1. Für die Suche, die Sie exportieren und importieren können**

|**Einstellung für die Konfiguration**|**Abhängigkeiten**|
|:-----|:-----|
|Abfrageregeln, einschließlich Ergebnis Blocs, heraufgestufte Ergebnisse und Benutzersegmente|Ergebnisquellen, Ergebnistypen, Suchschema, Bewertungsmodell|
|Ergebnisquellen|Suchschema|
|Ergebnistypen|Suchschema, ergebnisquellen, Anzeigevorlagen|
|Suchschema|Keine|
|Bewertungsmodell|Suchschema|

Sie können suchkonfigurationseinstellungen aus einer SSA exportieren und importieren die Einstellungen von Websitesammlungen und Websites. Aber kann nicht importieren angepasster suchkonfigurationseinstellungen in eine SSA. Auch können nicht die standardmäßige suchkonfigurationseinstellungen exportiert werden.

Auf Ebene der Websitesammlung oder Website können Sie exportieren oder importieren suchkonfigurationseinstellungen mithilfe der SharePoint-UI. Diese Einstellungen befinden sich im Abschnitt **Suchen** der Seite **Websiteeinstellungen** .

**Websiteeinstellungen - Suche**

![Websiteeinstellungen - Suche](media/search-customizations-for-sharepoint/ada14bf4-d721-4974-ad50-a1f8ce01933f.png)

Diese Einstellungen sind auch im Abschnitt **Verwaltung der Websitesammlung** verfügbar. Alternativ können Sie programmgesteuert importieren und Exportieren diese Einstellungen mithilfe der SharePoint 2013-Suche CSOM.

### <a name="search-configuration-files"></a>Konfigurationsdateien für die Suche

Die folgende Tabelle enthält die Schemadateien, die eine Suchkonfiguration unterstützen. Informationen zum Schemaformat finden Sie unter [Share Point Search Settings Portability Schemas](http://msdn.microsoft.com/en-us/library/office/dn627953%28v=office.15%29.aspx).

**Hinweis:**  Sie können die Schemadateien [http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip](http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip)heruntergeladen werden. 

**In Tabelle 2. Search Settings Portability schemas**

|**Schema**|**Beschreibung**|
|:-----|:-----|
|[SPS15XSDSearchSet1](http://msdn.microsoft.com/en-us/library/office/dn639116%28v=office.15%29.aspx)|Gibt an, XML, das ergebnisquellen darstellt.|
|[SPS15XSDSearchSet2](http://msdn.microsoft.com/en-us/library/office/dn639118%28v=office.15%29.aspx)|Gibt an, XML, das administrative Typen und Member zum Verwalten von einer Instanz der SSA Suche darstellt. Dazu gehören ergebniselementtypen und Einstellungen der Regel.|
|[SPS15XSDSearchSet3](http://msdn.microsoft.com/en-us/library/office/dn639120%28v=office.15%29.aspx)|Gibt an, die Einstellungen darstellt, die Abfrageregeln, enthalten XML ergebnisquellen, verwalteten Eigenschaften, durchforstete Eigenschaften und rangmodelle.|
|[SPS15XSDSearchSet4](http://msdn.microsoft.com/en-us/library/office/dn639117%28v=office.15%29.aspx)|Gibt an, XML, Enumerationen, die in anderen Schemas verwendet darstellt.|
|[SPS15XSDSearchSet5](http://msdn.microsoft.com/en-us/library/office/dn639119%28v=office.15%29.aspx)|Gibt an, XML, Enumerationen wie **ResultType-Wert** darstellt, die in anderen Schemas verwendet werden.|
|[SPS15XSDSearchSet6](http://msdn.microsoft.com/en-us/library/office/dn639115%28v=office.15%29.aspx)|Gibt an, XML, Enumerationen im Schema **Microsoft.Office.Server.Search.Administration** verwendet darstellt.|

### <a name="using-csom-to-port-configuration-settings"></a>Verwenden CSOM zum Port-Konfigurationseinstellungen

Die CSOM-APIs, die Sie benötigen, um das Importieren und Exportieren von Ihrer suchkonfigurationseinstellungen sind in der **SearchConfigurationPortability** -Klasse im **Microsoft.SharePoint.Client.Search.Portability** -Namespace.

Im folgenden Codebeispiel wird veranschaulicht, wie suchkonfigurationseinstellungen für eine Website exportieren.

```
private static void ExportSearchSettings(ClientContext context, string settingsFile)
{
   SearchConfigurationPortability sconfig = new SearchConfigurationPortability(context);
   SearchObjectOwner owner = new SearchObjectOwner(context, SearchObjectLevel.SPWeb);
   ClientResult<string> configresults = sconfig.ExportSearchConfiguration(owner);
   context.ExecuteQuery();
   string results = configresults.Value;
   System.IO.File.WriteAllText(settingsFile, results);
}
```

Der folgende Code zeigt, wie Sie eine Website suchkonfigurationseinstellungen importieren.

```
private static void ImportSearchSettings(ClientContext context, string settingsFile)
{
   SearchConfigurationPortability sconfig = new SearchConfigurationPortability(context);
   SearchObjectOwner owner = new SearchObjectOwner(context, SearchObjectLevel.SPWeb);
   sconfig.ImportSearchConfiguration(owner, System.IO.File.ReadAllText(settingsFile));
   context.ExecuteQuery();            
}
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Suchlösungen in SharePoint 2013 und SharePoint Online](search-solutions-in-sharepoint-2013-and-sharepoint-online.md)
    
- [SharePoint 2013: Import und Export der sucheinstellungen für SharePoint Online](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac)
    
- [SharePoint 2013: Führt zu personalisieren der Suche in einer SharePoint-Add-in](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9)
