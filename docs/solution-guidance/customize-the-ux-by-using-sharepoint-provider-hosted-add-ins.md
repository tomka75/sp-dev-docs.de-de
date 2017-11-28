---
title: Passen Sie die UX mithilfe von SharePoint gehostet durch Drittanbieter-add-ins
ms.date: 11/03/2017
ms.openlocfilehash: 28f14fa6a15e367232b1384952ed6b7fefbfb3de
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="customize-the-ux-by-using-sharepoint-provider-hosted-add-ins"></a>Passen Sie die UX mithilfe von SharePoint gehostet durch Drittanbieter-add-ins

Anpassen von SharePoint-UX-Komponenten Remote mit vom Anbieter gehosteten-add-ins. 

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

In diesem Artikel wird beschrieben, Beispiele, in denen bewährte Methoden zum Anpassen von SharePoint-UX-Komponenten, einschließlich der folgenden Szenarien:

- Seite Manipulation (hinzufügen und Ändern von Wiki-Seiten).
    
- -Add-ins und Daten anzeigt in modale Dialogfelder.
    
- Erstellen von personalisierten Benutzeroberflächenelemente.
    
- Clientseitiges Rendering (JSLink-Dateien, die das Rendern von Feldern in SharePoint-Listen anpassen bereitstellen).
    
- Webpart und Webpart-Add-in Bearbeitung (Remote bereitstellen und Ausführen eines Add-in-Skript-Webparts in einer vom Anbieter gehosteten-Add-in).
    
- Datenaggregation und Zwischenspeichern (mit lokalen Speicher HTML5 und HTTP-Cookies reduzieren Sie die Anzahl der Aufrufe an SharePoint Service).

## <a name="page-manipulation"></a>Seite zum Bearbeiten
<a name="bmPageManipulate"> </a>

Im Beispiel [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ModifyPages) umfasst zwei Szenarien für die Bearbeitung von Seiten:

- Erstellen Sie eine Wiki-Seite.
    
- Ändern des Layouts einer Wiki-Seite. 
    
Dieses Beispiel verwendet die standardmäßige Website Seitenbibliothek und vorhandenen Out-of-the-Box Layouts. Sie können auch aktualisieren, um eine benutzerdefinierte Wiki-Seitenbibliothek und benutzerdefinierten Layouts verwenden. Die UI-Add-in enthält zwei Schaltflächen, die erstellen sowohl Wiki-Seiten und zwei Links für die Anzeige von Wiki-Seiten, die Sie erstellen.

**Abbildung 1. Startseite für das Beispiel für das Zusammenstellen**

![Startseite für das Beispiel für das Zusammenstellen](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/8c6353d9-b339-4563-b945-eaea3d4da2a8.png)

Der Beispielcode für das erste Szenario bestimmt, ob Sie bereits die Wiki-Seite erstellt haben. Wenn dies nicht der Fall, fügt die Datei in der Seitenbibliothek der Website, und gibt den URL zurück.

**Hinweis:** Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```
var newpage = pageLibrary.RootFolder.Files.AddTemplateFile(newWikiPageUrl, TemplateFileType.WikiPage);
ctx.Load(newpage);
ctx.ExecuteQuery();
wikiPageUrl = String.Format("sitepages/{0}", wikiPageName);
```

In beiden Fällen wird im Beispiel den HTML-Code über das Textfeld auf der Startseite mit der **AddHtmlToWikiPage** -Methode in einer Hilfsklasse, die mit dem Namen **LabHelper**eingegeben werden. Diese Methode fügt den HTML-Code aus dem Formular in das Feld _WikiField_ der Wiki-Seite.

```
public void AddHtmlToWikiPage(ClientContext ctx, Web web, string folder, string html, string page)
        {
            Microsoft.SharePoint.Client.Folder pagesLib = web.GetFolderByServerRelativeUrl(folder);
            ctx.Load(pagesLib.Files);
            ctx.ExecuteQuery();

            Microsoft.SharePoint.Client.File wikiPage = null;

            foreach (Microsoft.SharePoint.Client.File aspxFile in pagesLib.Files)
            {
                if (aspxFile.Name.Equals(page, StringComparison.InvariantCultureIgnoreCase))
                {
                    wikiPage = aspxFile;
                    break;
                }
            }

            if (wikiPage == null)
            {
                return;
            }

            ctx.Load(wikiPage);
            ctx.Load(wikiPage.ListItemAllFields);
            ctx.ExecuteQuery();

            string wikiField = (string)wikiPage.ListItemAllFields["WikiField"];

            Microsoft.SharePoint.Client.ListItem listItem = wikiPage.ListItemAllFields;
            listItem["WikiField"] = html;
            listItem.Update();
            ctx.ExecuteQuery();
        }
```

Der Beispielcode für das zweite Szenario erstellt eine neue Instanz des **WebPartEntity** . Anschließend wird Methoden in einer Hilfsklasse zum Auffüllen der Webpart mit XML. Der XML-Code zeigt eine höher gestuften Verknüpfungsliste, einschließlich [http://www.bing.com](http://www.bing.com) und die Homepage des Repositorys [OfficeDev/PnP GitHub](https://github.com/SharePoint/PnP) .

```
WebPartEntity wp2 = new WebPartEntity();
wp2.WebPartXml = new LabHelper().WpPromotedLinks(linksID, string.Format("{0}/Lists/{1}", 
                                                                Request.QueryString["SPHostUrl"], "Links"), 
                                                                string.Format("{0}/{1}", Request.QueryString["SPHostUrl"], 
                                                                scenario2PageUrl), "$Resources:core,linksList");
wp2.WebPartIndex = 1;
wp2.WebPartTitle = "Links";

new LabHelper().AddWebPartToWikiPage(ctx, ctx.Web, "SitePages", wp2, scenario2Page, 2, 1, false);
new LabHelper().AddHtmlToWikiPage(ctx, ctx.Web, "SitePages", htmlEntry.Text, scenario2Page, 2, 2);

this.hplPage2.NavigateUrl = string.Format("{0}/{1}", Request.QueryString["SPHostUrl"], scenario2PageUrl);
```

Der Hilfscode zeigt die höher gestuften Verknüpfungen mit einer Tabelle in einem **XsltListViewWebPart** -Webpart.

**Abbildung 2. Zweite Wiki-Seiten mit XsltListViewWebPart und höher gestuften Verknüpfungen-Tabelle**

![Zweite Wiki-Seiten mit XsltListViewWeb Teil und höher gestuften Verknüpfungen-Tabelle](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/6dc60a0b-b11a-4fe9-ad06-6b4d0d4b8b24.png)

Das **WpPromotedLinks** -Objekt auf der **LabHelper** -Instanz enthält XML, das die Darstellung des Webparts definiert, die in der Wiki-Seiten eingebettet werden. Die **AddWebPartToWikiPage** -Methode fügt dann das neu definierte-Webpart in einem neuen `div` -Tag auf Wiki-Seiten.

```
XmlDocument xd = new XmlDocument();
            xd.PreserveWhitespace = true;
            xd.LoadXml(wikiField);

            // Sometimes the wikifield content seems to be surrounded by an additional div. 
            XmlElement layoutsTable = xd.SelectSingleNode("div/div/table") as XmlElement;
            if (layoutsTable == null)
            {
                layoutsTable = xd.SelectSingleNode("div/table") as XmlElement;
            }

            XmlElement layoutsZoneInner = layoutsTable.SelectSingleNode(string.Format("tbody/tr[{0}]/td[{1}]/div/div", row, col)) as XmlElement;
            // - space element
            XmlElement space = xd.CreateElement("p");
            XmlText text = xd.CreateTextNode(" ");
            space.AppendChild(text);

            // - wpBoxDiv
            XmlElement wpBoxDiv = xd.CreateElement("div");
            layoutsZoneInner.AppendChild(wpBoxDiv);

            if (addSpace)
            {
                layoutsZoneInner.AppendChild(space);
            }

            XmlAttribute attribute = xd.CreateAttribute("class");
            wpBoxDiv.Attributes.Append(attribute);
            attribute.Value = "ms-rtestate-read ms-rte-wpbox";
            attribute = xd.CreateAttribute("contentEditable");
            wpBoxDiv.Attributes.Append(attribute);
            attribute.Value = "false";
            // - div1
            XmlElement div1 = xd.CreateElement("div");
            wpBoxDiv.AppendChild(div1);
            div1.IsEmpty = false;
            attribute = xd.CreateAttribute("class");
            div1.Attributes.Append(attribute);
            attribute.Value = "ms-rtestate-read " + wpdNew.Id.ToString("D");
            attribute = xd.CreateAttribute("id");
            div1.Attributes.Append(attribute);
            attribute.Value = "div_" + wpdNew.Id.ToString("D");
            // - div2
            XmlElement div2 = xd.CreateElement("div");
            wpBoxDiv.AppendChild(div2);
            div2.IsEmpty = false;
            attribute = xd.CreateAttribute("style");
            div2.Attributes.Append(attribute);
            attribute.Value = "display:none";
            attribute = xd.CreateAttribute("id");
            div2.Attributes.Append(attribute);
            attribute.Value = "vid_" + wpdNew.Id.ToString("D");

            ListItem listItem = webPartPage.ListItemAllFields;
            listItem["WikiField"] = xd.OuterXml;
            listItem.Update();
            ctx.ExecuteQuery();
```

## <a name="showing-add-ins-and-data-in-modal-dialog-boxes"></a>Add-ins und Daten anzeigen in modale Dialogfelder
<a name="bmPageManipulate"> </a>

Im Beispiel [Core.Dialog](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.Dialog) zeigt zwei Methoden für das Einbetten von modales Dialogfeld Feld Links. Diese Links anzeigen eine vom Anbieter gehosteten Add-in-Seite in einer SharePoint-Website-Host. Das Add-In wird verwendet das Clientobjektmodell (CSOM) zum Erstellen der benutzerdefinierten Aktion und JavaScript starten und Anzeigen von Informationen in das Dialogfeld ein. Da einige dieser Informationen von der Hostwebsite abgerufen werden, wird auch das JavaScript-Objektmodell (JSOM) zum Abrufen von Informationen aus der Hostwebsite verwendet. Und, da das Add-in in einer anderen Domäne als der SharePoint-Website-Host ausgeführt wird, außerdem wird durch die domänenübergreifende SharePoint-Dokumentbibliothek der Hostwebsite anrufen.

**Hinweis:** Weitere Informationen zur Verwendung der domänenübergreifenden Bibliothek in diesem Szenario finden Sie unter [Zugriff auf SharePoint 2013-Daten aus-add-ins mithilfe der domänenübergreifenden Bibliothek](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx).

Die Startseite ist die Seite, die im Dialogfeld angezeigt wird. So behandeln Sie alle Unterschiede zwischen den angegebenen Anzeigekontext (Dialogfeld im Vergleich zu ganzseitigen) anzeigen, bestimmt das Add-in, ob sie in einem Dialogfeld angezeigt wird. Dies geschieht mithilfe von einen Abfragezeichenfolgen-Parameter, der zusammen mit den Links übergeben wird, die die Dialogfelder zu starten.

```
private string SetIsDlg(string isDlgValue)
        {
            var urlParams = HttpUtility.ParseQueryString(Request.QueryString.ToString());
            urlParams.Set("IsDlg", isDlgValue);
            return string.Format("{0}://{1}:{2}{3}?{4}", Request.Url.Scheme, Request.Url.Host, Request.Url.Port, Request.Url.AbsolutePath, urlParams.ToString());
        }
```

Sie könnten beispielsweise auswählen, zum Anzeigen bestimmter Elemente der Benutzeroberfläche (wie Schaltflächen) oder sogar auf verschiedene Seitenlayouts, je nachdem, ob der Inhalt in einem Dialogfeld angezeigt wird.

Die Benutzeroberfläche der Startseite stellt zwei Optionen zum Erstellen von Links, um das Dialogfeld zusammen mit einer Liste aller Listen auf dem hostweb. Es stellt auch **OK** und **Abbrechen** Schaltflächen, dass Sie im Dialogfeld Feld Kontext verwenden können, um das Dialogfeld Feld und/oder Aufforderung weiteren Aktionen in das Add-in zu schließen.

Wenn Sie die **Option hinzufügen** Schaltfläche geklickt haben, erstellt das Add-in ein **CustomActionEntity** -Objekt, das das Dialogfeld beginnt. Anschließend wird die [Erweiterung OfficeDevPnP Core](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) -Methode mit dem Namen **AddCustomAction** , um die neue benutzerdefinierte Aktion im Menü **Einstellungen der Website** hinzufügen.

```
StringBuilder modelDialogScript = new StringBuilder(10);
modelDialogScript.Append("javascript:var dlg=SP.UI.ModalDialog.showModalDialog({url: '");
modelDialogScript.Append(String.Format("{0}", SetIsDlg("1")));
modelDialogScript.Append("', dialogReturnValueCallback:function(res, val) {} });");       

// Create a custom action.
CustomActionEntity customAction = new CustomActionEntity()
{
  Title = "Office AMS Dialog sample",                
  Description = "Shows how to start an add-in inside a dialog box.",
  Location = "Microsoft.SharePoint.StandardMenu",
  Group = "SiteActions",
  Sequence = 10000,
  Url = modelDialogScript.ToString(),
};

// Add the custom action to the site.
cc.Web.AddCustomAction(customAction);
```

Die **AddCustomAction** -Methode hinzugefügt der **UserCustomActions** -Auflistung, die die SharePoint-Website zugeordnet ist die benutzerdefinierte Aktion.

```
var newAction = existingActions.Add();
            newAction.Description = customAction.Description;
            newAction.Location = customAction.Location;
            if (customAction.Location == JavaScriptExtensions.SCRIPT_LOCATION)
            {
                newAction.ScriptBlock = customAction.ScriptBlock;
            }
            else
            {
                newAction.Sequence = customAction.Sequence;
                newAction.Url = customAction.Url;
                newAction.Group = customAction.Group;
                newAction.Title = customAction.Title;
                newAction.ImageUrl = customAction.ImageUrl;
                if (customAction.Rights != null)
                {
                    newAction.Rights = customAction.Rights;
                }
            }
            newAction.Update();
            web.Context.Load(web, w => w.UserCustomActions);
            web.Context.ExecuteQuery();
```

Wenn Sie die **Seite mit den Skript-Editor-Webpart hinzufügen** Schaltfläche geklickt haben, verwendet die Methoden **AddWikiPage** und **AddWebPartToWikiPage** des Add-Ins zum Erstellen einer Wiki-Seiten innerhalb der Website-Bibliothek für Seiten und Hinzufügen eines konfigurierten Skript-Editor-Webparts auf der Seite.

```
string scenario1Page = String.Format("scenario1-{0}.aspx", DateTime.Now.Ticks);
string scenario1PageUrl = cc.Web.AddWikiPage("Site Pages", scenario1Page);
cc.Web.AddLayoutToWikiPage("SitePages", WikiPageLayout.OneColumn, scenario1Page);
WebPartEntity scriptEditorWp = new WebPartEntity();
scriptEditorWp.WebPartXml = ScriptEditorWebPart();
scriptEditorWp.WebPartIndex = 1;
scriptEditorWp.WebPartTitle = "Script editor test"; 
cc.Web.AddWebPartToWikiPage("SitePages", scriptEditorWp, scenario1Page, 1, 1, false);
```

Die **AddWikiPage** -Methode lädt der Seitenbibliothek der Website. Wenn die Wiki-Seiten durch das Add-in [OfficeDevPnP Core](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) angegebenen nicht bereits vorhanden ist, wird die Seite erstellt.

```
public static string AddWikiPage(this Web web, string wikiPageLibraryName, string wikiPageName)
        {
            string wikiPageUrl = "";


            var pageLibrary = web.Lists.GetByTitle(wikiPageLibraryName);

            web.Context.Load(pageLibrary.RootFolder, f => f.ServerRelativeUrl);
            web.Context.ExecuteQuery();

            var pageLibraryUrl = pageLibrary.RootFolder.ServerRelativeUrl;
            var newWikiPageUrl = pageLibraryUrl + "/" + wikiPageName;

            var currentPageFile = web.GetFileByServerRelativeUrl(newWikiPageUrl);

            web.Context.Load(currentPageFile, f => f.Exists);
            web.Context.ExecuteQuery();

            if (!currentPageFile.Exists)
            {
                var newpage = pageLibrary.RootFolder.Files.AddTemplateFile(newWikiPageUrl, TemplateFileType.WikiPage);

                web.Context.Load(newpage);
                web.Context.ExecuteQuery();

                wikiPageUrl = UrlUtility.Combine("sitepages", wikiPageName);
            }

            return wikiPageUrl;
        }
```

Die **AddWebPartToWikiPage** -Methode fügt der neu definierten Webparts innerhalb einer neuen `<div>` -Tag auf Wiki-Seiten. Anschließend wird JSOM und der domänenübergreifenden Bibliothek zum Abrufen der Informationen, die die Liste der SharePoint-Listen auf dem hostweb aufgefüllt wird.

```
function printAllListNamesFromHostWeb() {
        var context;
        var factory;
        var appContextSite;
        var collList;

        context = new SP.ClientContext(appWebUrl);
        factory = new SP.ProxyWebRequestExecutorFactory(appWebUrl);
        context.set_webRequestExecutorFactory(factory);
        appContextSite = new SP.AppContextSite(context, spHostUrl);

        this.web = appContextSite.get_web();
        collList = this.web.get_lists();
        context.load(collList);

        context.executeQueryAsync(
            Function.createDelegate(this, successHandler),
            Function.createDelegate(this, errorHandler)
        );
```

## <a name="personalized-ui-elements"></a>Personalisierte Benutzeroberflächenelemente
<a name="bmPersonalized"> </a>

Das [Branding.UIElementPersonalization](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization) -Beispiel veranschaulicht, wie eingebettete JavaScript und Werte in Benutzerprofilen gespeichert und SharePoint-Listen für Benutzeroberflächenelemente auf dem hostweb zu personalisieren. Auch wird HTML5 lokalen Speicher verwendet, um Anrufe an die Hostwebsite zu minimieren.

Startseite des Beispiels aufgefordert, eine der drei Zeichenfolgen (XX, JJ oder ZZ) in den Abschnitt **Über mich** von Ihrer Profilseite des Benutzers hinzufügen.

Das Add-In wurde bereits bereitgestellt, drei Bilder und einer SharePoint-Liste, die Titel und URLs für jedes Bild, sowie ein weiteres Feld enthält, der eine der drei Zeichenfolgen pro Bild verbindet. Nachdem Sie die **Anpassung der Eingabe-** Schaltfläche geklickt haben, bettet die personalize.js-Datei des Add-Ins in der Auflistung benutzerdefinierte Aktionen.

```
public void AddPersonalizeJsLink(ClientContext ctx, Web web)
        {
            string scenarioUrl = String.Format("{0}://{1}:{2}/Scripts", this.Request.Url.Scheme,
                                                this.Request.Url.DnsSafeHost, this.Request.Url.Port);
            string revision = Guid.NewGuid().ToString().Replace("-", "");
            string personalizeJsLink = string.Format("{0}/{1}?rev={2}", scenarioUrl, "personalize.js", revision);

            StringBuilder scripts = new StringBuilder(@"
                var headID = document.getElementsByTagName('head')[0]; 
                var");

            scripts.AppendFormat(@"
                newScript = document.createElement('script');
                newScript.type = 'text/javascript';
                newScript.src = '{0}';
                headID.appendChild(newScript);", personalizeJsLink);
            string scriptBlock = scripts.ToString();

            var existingActions = web.UserCustomActions;
            ctx.Load(existingActions);
            ctx.ExecuteQuery();

            var actions = existingActions.ToArray();
            foreach (var action in actions)
            {
                if (action.Description == "personalize" &amp;&amp;
                    action.Location == "ScriptLink")
                {
                    action.DeleteObject();
                    ctx.ExecuteQuery();
                }
            }

            var newAction = existingActions.Add();
            newAction.Description = "personalize";
            newAction.Location = "ScriptLink";
            
            newAction.ScriptBlock = scriptBlock;
            newAction.Update();
            ctx.Load(web, s => s.UserCustomActions);
            ctx.ExecuteQuery();
        }
```

Da SharePoint-Teamwebsites standardmäßig die [Minimale herunterladen Strategie (MDS)](http://msdn.microsoft.com/en-us/library/office/dn456544%28v=office.15%29.aspx)verwenden, versucht der Code in der Datei personalize.js zuerst selbst MDS registrieren. Auf diese Weise beim Laden der Seite, die die JavaScript-Code enthält engine der MDS Starets der main-Funktion (**RemoteManager_Inject**). Wenn MDS deaktiviert ist, wird diese Funktion sofort gestartet.

```
// Register script for MDS, if possible.
RegisterModuleInit("personalize.js", RemoteManager_Inject); //MDS registration
RemoteManager_Inject(); //non-MDS run

if (typeof (Sys) != "undefined" &amp;&amp; Boolean(Sys) &amp;&amp; Boolean(Sys.Application)) {
    Sys.Application.notifyScriptLoaded();h
}

if (typeof (NotifyScriptLoadedAndExecuteWaitingJobs) == "function") {
    NotifyScriptLoadedAndExecuteWaitingJobs("scenario1.js");
}
// The RemoteManager_Inject function is the entry point for loading the other scripts that perform the customizations. When a given script depends on another script, be sure to load the dependent script after the one on which it depends. This sample loads the JQuery library before the personalizeIt function that uses JQuery.
function RemoteManager_Inject() {

    var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";

    // Load jQuery. 
    loadScript(jQuery, function () {

        personalizeIt();

    });
}
```

Die Funktion **personalizeIt()** überprüft HTML5 lokalen Speicher, bevor Benutzerprofilinformationen gesucht. Wenn es in der Benutzerprofilinformationen geht, werden die Informationen, die abgerufen, im lokalen Speicher HTML5 gespeichert.

```
function personalizeIt() {
    clientContext = SP.ClientContext.get_current();

    var fileref = document.createElement('script');
    fileref.setAttribute("type", "text/javascript");
    fileref.setAttribute("src", "/_layouts/15/SP.UserProfiles.js");
    document.getElementsByTagName("head")[0].appendChild(fileref);

    SP.SOD.executeOrDelayUntilScriptLoaded(function () {        

        // Get localstorage values if they exist.
        buCode = localStorage.getItem("bucode");
        buCodeTimeStamp = localStorage.getItem("buCodeTimeStamp");

        // Determine whether the page already has embedded personalized image.
        var pageTitle = $('#pageTitle')[0].innerHTML;
        if (pageTitle.indexOf("img") > -1) {
            personalized = true;
        }
        else {
            personalized = false;
        }        

        // If nothing is in localstorage, get profile data, which will also populate localstorage.
        if (buCode == "" || buCode == null) {
            getProfileData(clientContext);
            personalized = false;
        }
        else {
            // Check for expiration.            
            if (isKeyExpired("buCodeTimeStamp")) {                
                getProfileData(clientContext);

                if (buCode != "" || buCode != null) {
                    // Set timestamp for expiration.
                    currentTime = Math.floor((new Date().getTime()) / 1000);
                    localStorage.setItem("buCodeTimeStamp", currentTime);

                    // Set personalized to false so that the code can check for a new image in case buCode was updated.
                    personalized = false;
                }
            }            
        }

        // Load image or make sure it is current based on the value in AboutMe.
        if (!personalized) {
            loadPersonalizedImage(buCode);
        }


    }, 'SP.UserProfiles.js');
}
```

Die Datei personalize.js enthält auch Code, der überprüft, um festzustellen, ob der lokalen Speicherschlüssel abgelaufen ist. Dies ist nicht in HTML5 lokalen Speicher integriert.

```
// Check to see if the key has expired
function isKeyExpired(TimeStampKey) {

    // Retrieve the example setting for expiration in seconds.
    var expiryStamp = localStorage.getItem(TimeStampKey);

    if (expiryStamp != null &amp;&amp; cacheTimeout != null) {

        // Retrieve the timestamp and compare against specified cache timeout settings to see if it is expired.
        var currentTime = Math.floor((new Date().getTime()) / 1000);

        if (currentTime - parseInt(expiryStamp) > parseInt(cacheTimeout)) {
            return true; //Expired
        }
        else {
            return false;
        }
    }
    else {
        //default 
        return true;
    }
}
```

## <a name="client-side-rendering"></a>Clientseitiges Rendering
<a name="bmPersonalized"> </a>

Das [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering) -Beispiel veranschaulicht, wie ein vom Anbieter gehosteten add-in verwenden, um Remote Bereitstellen von SharePoint-Artefakte und JSLink-Dateien, die clientseitiges Rendering verwenden, um das Aussehen und Verhalten von SharePoint-Listenfelder anpassen. JSLink-Dateien und clientseitiges Rendering können Sie, wie Sie steuern einer SharePoint-Seite Steuerelemente (Listenansichten, Listenfelder, und hinzufügen und Bearbeiten von Formularen) gerendert werden. Dieses Steuerelement kann reduzieren oder benutzerdefinierte Feldtypen überflüssig. Clientseitiges Rendering ermöglicht die Liste Feld Darstellung Remote Remote steuern.

Im Beispiel kombiniert die JSLink Beispiele von der [Client-Side Rendering (JSLink)-Codebeispiele](http://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a) zu einer einzelnen vom Anbieter gehosteten-add-in für SharePoint fest, stellt die JSLink-Dateien. Clientseitiges Rendering können Sie standardmäßigen-Technologien, wie HTML und JavaScript, verwenden, um benutzerdefinierte und vordefinierte Feldtypen Renderinglogik definieren.

Wenn Sie das Beispiel starten, fordert die Startseite Sie alle Beispiele bereitstellen.

**Abbildung 3. Startseite des Beispiels clientseitiges rendering**

![Startseite des Beispiels clientseitiges rendering](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/bfa1b472-976b-4bdc-95df-537cee5570e6.png)

Bei der Auswahl **Provision Beispiele**wird das Add-in bereitgestellt, ein Bild als auch alle der SharePoint-Listen, Listenansichten, Listenelemente, Formulare und JavaScript-Dateien, die in jedem Beispiel verwendet werden. Das Add-in erstellt einen Ordner namens JSLink-Beispiele in der Formatbibliothek, und klicken Sie dann die JavaScript-Dateien in diesen Ordner hochgeladen. Die **UploadFileToFolder** -Methode führt die Arbeit des Hochladens und jeder JavaScript-Datei einchecken.

```
public static void UploadFileToFolder(Web web, string filePath, Folder folder)
        {
            using (FileStream fs = new FileStream(filePath, FileMode.Open))
            {
                FileCreationInformation flciNewFile = new FileCreationInformation();

                flciNewFile.ContentStream = fs;
                flciNewFile.Url = System.IO.Path.GetFileName(filePath);
                flciNewFile.Overwrite = true;

                Microsoft.SharePoint.Client.File uploadFile = folder.Files.Add(flciNewFile);
                uploadFile.CheckIn("CSR sample js file", CheckinType.MajorCheckIn);

                folder.Context.Load(uploadFile);
                folder.Context.ExecuteQuery();
            }
        }
```

### <a name="sample-1-apply-formatting-to-a-list-column"></a>Beispiel 1: Formatieren einer Listenspalte

Beispiel 1 zeigt, wie um einer Listenspalte basierend auf den Wert des Felds zu formatieren. Priorität Feldwerte von 1 (hoch), 2 (Normal) und 3 (niedrig) werden in Rot, Gelb und Orange angezeigt.

**Abbildung 4. Benutzerdefinierte Liste Feldanzeige**

![Benutzerdefinierte Liste Feldanzeige](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/1481adfa-efc9-4b59-b07f-bb330f02d2bb.png)

Das folgende JavaScript überschreibt die Standardanzeige dar und erstellt eine neue Anzeigevorlage für das Feld der Liste **Priorität** . Das Verfahren in die anonyme Funktion, die die Kontextinformationen über das Feld lädt, deren Anzeige Sie außer Kraft setzen möchten, die in alle Beispiele verwendet wird.

```
(function () {

    // Create object that has the context information about the field that you want to render differently.
    var priorityFiledContext = {};
    priorityFiledContext.Templates = {};
    priorityFiledContext.Templates.Fields = {
        // Apply the new rendering for Priority field in List View.
        "Priority": { "View": priorityFiledTemplate }
    };

    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(priorityFiledContext);

})();

// This function provides the rendering logic for list view.
function priorityFiledTemplate(ctx) {

    var priority = ctx.CurrentItem[ctx.CurrentFieldSchema.Name];

    // Return HTML element with appropriate color based on the Priority column's value.
    switch (priority) {
        case "(1) High":
            return "<span style='color :#f00'>" + priority + "</span>";
            break;
        case "(2) Normal":
            return "<span style='color :#ff6a00'>" + priority + "</span>";
            break;
        case "(3) Low":
            return "<span style='color :#cab023'>" + priority + "</span>";
    }
}
```

### <a name="sample-2-shorten-long-text"></a>Beispiel 2: Kürzen Sie langen text

Beispiel 2 zeigt, wie zu kürzende langen Text im Feld **Text** , der einer Liste mit **Ankündigungen** gespeichert. Der vollständige Text zeigt als ein Popup-Fenster, das angezeigt wird, wenn Sie über ein Listenelement bewegen, wie in Abbildung 8 dargestellt.

**Abbildung 5. Verkürzte Liste Feld Anzeige mit popup**

![Abgeschnittene Liste Feld Anzeige mit popup](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/a5e6d2af-f1f9-4bcc-9278-e56fd42c2e64.png)

Das folgende JavaScript verkürzt **den Textkörper dar** und festgelegt, dass den vollständigen Text als ein Popup über das **Title** -Attribut für das **span** -Tag angezeigt werden.

```
function bodyFiledTemplate(ctx) {

    var bodyValue = ctx.CurrentItem[ctx.CurrentFieldSchema.Name];

    // This regex expression is used to delete HTML tags from the Body field.
    var regex = /(<([^>]+)>)/ig;

    bodyValue = bodyValue.replace(regex, "");

    var newBodyValue = bodyValue;

    if (bodyValue &amp;&amp; bodyValue.length >= 100)
    {
        newBodyValue = bodyValue.substring(0, 100) + " ...";
    }

    return "<span title='" + bodyValue + "'>" + newBodyValue + "</span>";

}
```

### <a name="sample-3-display-an-image-with-a-document-name"></a>Beispiel 3: Ein Bild mit einem Dokumentnamen anzeigen

Beispiel 3 zeigt, wie ein Bild neben dem Dokumentnamen eines in einer Dokumentbibliothek angezeigt. Eine rote Logo wird angezeigt, wenn der Wert des Felds **vertraulich** auf **Ja**festgelegt ist, wie in Abbildung 6 dargestellt. 

**Abbildung 6. Anzeige von Bildern neben den Namen des Dokuments**

![Anzeige von Bildern neben den Namen des Dokuments](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/f2768dfd-ae05-4afc-8dbe-26dc4e7dca6d.png)

Das folgende JavaScript überprüft den Wert des Felds **vertraulich** und passt anschließend die **Namen** Feldanzeige basierend auf dem Wert eines anderen Felds. Das Beispiel verwendet das Bild, das hochgeladen wird, wenn Sie eine **Bereitstellung Beispiele**auswählen. 

```
function linkFilenameFiledTemplate(ctx) {

    var confidential = ctx.CurrentItem["Confidential"];
    var title = ctx.CurrentItem["FileLeafRef"];

    // This Regex expression use to delete extension (.docx, .pdf ...) form the file name.
    title = title.replace(/\.[^/.]+$/, "")

    // Check confidential field value.
    if (confidential &amp;&amp; confidential.toLowerCase() == 'yes') {
        // Render HTML that contains the file name and the confidential icon
        return title + "&amp;nbsp;<img src= '" + _spPageContextInfo.siteServerRelativeUrl + "/Style%20Library/JSLink-Samples/imgs/Confidential.png' alt='Confidential Document' title='Confidential Document'/>";
    }
    else
    {
        return title;
    }
}
```

### <a name="sample-4-display-a-bar-chart"></a>Beispiel 4: Ein Balkendiagramm angezeigt

Beispiel 4 zeigt, wie ein Balkendiagramm in das Feld **% abgeschlossen** einer Aufgabenliste angezeigt. Die Darstellung des Balkendiagramm verwendet wird, hängt vom Wert im Feld **% abgeschlossen** , wie in Abbildung 10 dargestellt. Beachten Sie, dass ein Balkendiagramm auch in den Formularen für das Erstellen und Bearbeiten von Listenelementen Aufgabe angezeigt wird.

Mit dem folgende Code wird die Anzeige Balkendiagramm erstellt und ordnet sie mit den Formularen anzeigen und -Anzeige (**PercentCompleteViewFiledTemplate**), und klicken Sie dann mit der neuen und Bearbeitungsformulare (**PercentCompleteEditFiledTemplate**).

```
// This function provides the rendering logic for View and Display forms.
function percentCompleteViewFiledTemplate(ctx) {

    var percentComplete = ctx.CurrentItem[ctx.CurrentFieldSchema.Name];
    return "<div style='background-color: #e5e5e5; width: 100px;  display:inline-block;'> \
            <div style='width: " + percentComplete.replace(/\s+/g, '') + "; background-color: #0094ff;'> \
            &amp;nbsp;</div></div>&amp;nbsp;" + percentComplete;

}

// This function provides the rendering logic for New and Edit forms.
function percentCompleteEditFiledTemplate(ctx) {

    var formCtx = SPClientTemplates.Utility.GetFormContextForCurrentField(ctx);

    // Register a callback just before submit.
    formCtx.registerGetValueCallback(formCtx.fieldName, function () {
        return document.getElementById('inpPercentComplete').value;
    });

    return "<input type='range' id='inpPercentComplete' name='inpPercentComplete' min='0' max='100' \
            oninput='outPercentComplete.value=inpPercentComplete.value' value='" + formCtx.fieldValue + "' /> \
            <output name='outPercentComplete' for='inpPercentComplete' >" + formCtx.fieldValue + "</output>%";
}
```

**Abbildung 7. Balkendiagramm angezeigt, in das Feld % abgeschlossen**

![Balkendiagramm angezeigt, in das Feld % abgeschlossen](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/fb36f27a-2eb7-4c5f-8428-b85b65369ea9.png)

### <a name="sample-5-change-the-rendering-template"></a>Beispiel 5: Ändern der Renderingvorlage

Beispiel 5 zeigt, wie die Renderingvorlage für eine Listenansicht zu ändern. Diese Ansicht zeigt Element Listentitel, die wie Akkordeons erweitern, wenn Sie diese auswählen. Die erweiterte Ansicht zeigt, zusätzliche Felder für Listenelemente, wie in Abbildung 8 dargestellt.

**Abbildung 8. Reduzierte und erweiterte Element Listenansichten**

![Reduzierte und erweiterte Element Listenansichten](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/fd185eef-e2be-4523-9adb-d524b84ecc26.png)

Der folgende Code richtet die Vorlage und registriert dieses in die Vorlage Liste aus. Es richtet das allgemeine Layout, und klicken Sie dann den **OnPostRender** -Ereignishandler verwendet, um die JavaScript-Funktion zu registrieren, die ausgeführt wird, wenn die Liste dargestellt wird. Diese Funktion das Ereignis den CSS-Code zugeordnet und Ereignisbehandlung, die die Akkordeon Funktionalität implementiert.

```
(function () {

    // jQuery library is required in this sample.
    // Fallback to loading jQuery from a CDN path if the local is unavailable
    (window.jQuery || document.write('<script src="//ajax.aspnetcdn.com/ajax/jquery/jquery-1.10.0.min.js"><\/script>'));

    // Create object that has the context information about the field that you want to render differently.
    var accordionContext = {};
    accordionContext.Templates = {};

    // Be careful when adding the header for the template, because it will break the default list view render.
    accordionContext.Templates.Header = "<div class='accordion'>";
    accordionContext.Templates.Footer = "</div>";

    // Add OnPostRender event handler to add accordion click events and style.
    accordionContext.OnPostRender = accordionOnPostRender;

    // This line of code tells the TemplateManager that you want to change all the HTML for item row rendering.
    accordionContext.Templates.Item = accordionTemplate;

    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(accordionContext);

})();

// This function provides the rendering logic.
function accordionTemplate(ctx) {
    var title = ctx.CurrentItem["Title"];
    var description = ctx.CurrentItem["Description"];

    // Return whole item html
    return "<h2>" + title + "</h2><p>" + description + "</p><br/>";
}

function accordionOnPostRender() {

    // Register event to collapse and expand when selecting accordion header.
    $('.accordion h2').click(function () {
        $(this).next().slideToggle();
    }).next().hide();

    $('.accordion h2').css('cursor', 'pointer');
}
```

### <a name="sample-6-validate-field-values"></a>Beispiel 6: Überprüfen der Feldwerte

Beispiel 6 zeigt, wie Sie reguläre Ausdrücke verwenden, um vom Benutzer eingegebenen Feldwerte überprüfen. Eine rote Fehlermeldung wird angezeigt, wenn der Benutzer eine ungültige e-Mail-Adresse in das Textfeld **E-Mail** eingibt. Dies geschieht, wenn der Benutzer erstellt oder ein Listenelement bearbeitet, wie in Abbildung 9 dargestellt.

**Abbildung 9. Fehlermeldung ungültigem Texteingabe**

![Fehlermeldung ungültigem Texteingabe](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/d0d1faf1-aa03-4df8-a1a6-db86fff1f463.png)

Der folgende Code richtet die Vorlage mit einem Platzhalter für die Anzeige der Fehlermeldung und registriert Callback-Funktionen, die ausgelöst werden, wenn der Benutzer versucht, die Formulare übermitteln. Der erste Rückruf zurückgegeben wird des Werts der **E-Mail** -Spalte und der zweite Rückruf verwendet reguläre Ausdrücke, um den Zeichenfolgenwert zu überprüfen.

```
function emailFiledTemplate(ctx) {

    var formCtx = SPClientTemplates.Utility.GetFormContextForCurrentField(ctx);

    // Register a callback just before submit.
    formCtx.registerGetValueCallback(formCtx.fieldName, function () {
        return document.getElementById('inpEmail').value;
    });

    // Create container for various validations.
    var validators = new SPClientForms.ClientValidation.ValidatorSet();
    validators.RegisterValidator(new emailValidator());

    // Validation failure handler.
    formCtx.registerValidationErrorCallback(formCtx.fieldName, emailOnError);

    formCtx.registerClientValidator(formCtx.fieldName, validators);

    return "<span dir='none'><input type='text' value='" + formCtx.fieldValue + "'  maxlength='255' id='inpEmail' class='ms-long'> \
            <br><span id='spnError' class='ms-formvalidation ms-csrformvalidation'></span></span>";
}

// Custom validation object to validate email format.
emailValidator = function () {
    emailValidator.prototype.Validate = function (value) {
        var isError = false;
        var errorMessage = "";

        //Email format Regex expression
        var emailRejex = /\S+@\S+\.\S+/;

        if (!emailRejex.test(value) &amp;&amp; value.trim()) {
            isError = true;
            errorMessage = "Invalid email address";
        }

        // Send error message to error callback function (emailOnError).
        return new SPClientForms.ClientValidation.ValidationResult(isError, errorMessage);
    };
};

// Add error message to spnError element under the input field element.
function emailOnError(error) {
    document.getElementById("spnError").innerHTML = "<span role='alert'>" + error.errorMessage + "</span>";
}
```

### <a name="sample-7-make-list-item-edit-fields-read-only"></a>Beispiel 7: Stellen Sie Listenelement schreibgeschützte Felder bearbeiten

Beispiel sieben zeigt, wie Sie Felder für Listenelemente bearbeiten Formular nur-Lese-Liste. Der schreibgeschützte Felder anzeigen mit keine Bearbeitungssteuerelemente, wie in Abbildung 10 dargestellt.

**Abbildung 10. Schreibgeschütztes Feld auf eine benutzerdefinierte Liste Bearbeitungsformular**

![Schreibgeschützte Felder in einer benutzerdefinierten Liste Bearbeitungsformular](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/de441289-8276-4e7c-8530-d08192e29000.png)

Das folgende Codebeispiel ändert den **Titel**, **AssignedTo**und Felder des Listenelements **Priorität** Bearbeitungsformular so, dass sie die Feldwerte nur mit keine Bearbeitungssteuerelemente anzeigen. Der Code zeigt, wie die Abfrageanalyse Anforderungen für die verschiedenen Feldtypen behandeln.

```
function readonlyFieldTemplate(ctx) {

    // Reuse SharePoint JavaScript libraries.
    switch (ctx.CurrentFieldSchema.FieldType) {
        case "Text":
        case "Number":
        case "Integer":
        case "Currency":
        case "Choice":
        case "Computed":
            return SPField_FormDisplay_Default(ctx);

        case "MultiChoice":
            prepareMultiChoiceFieldValue(ctx);
            return SPField_FormDisplay_Default(ctx);

        case "Boolean":
            return SPField_FormDisplay_DefaultNoEncode(ctx);

        case "Note":
            prepareNoteFieldValue(ctx);
            return SPFieldNote_Display(ctx);

        case "File":
            return SPFieldFile_Display(ctx);

        case "Lookup":
        case "LookupMulti":
                return SPFieldLookup_Display(ctx);           

        case "URL":
            return RenderFieldValueDefault(ctx);

        case "User":
            prepareUserFieldValue(ctx);
            return SPFieldUser_Display(ctx);

        case "UserMulti":
            prepareUserFieldValue(ctx);
            return SPFieldUserMulti_Display(ctx);

        case "DateTime":
            return SPFieldDateTime_Display(ctx);

        case "Attachments":
            return SPFieldAttachments_Default(ctx);

        case "TaxonomyFieldType":
            //Re-use JavaScript from the sp.ui.taxonomy.js SharePoint JavaScript library
            return SP.UI.Taxonomy.TaxonomyFieldTemplate.renderDisplayControl(ctx);
    }
}

// User control needs specific formatted value to render content correctly.
function prepareUserFieldValue(ctx) {
    var item = ctx['CurrentItem'];
    var userField = item[ctx.CurrentFieldSchema.Name];
    var fieldValue = "";

    for (var i = 0; i < userField.length; i++) {
        fieldValue += userField[i].EntityData.SPUserID + SPClientTemplates.Utility.UserLookupDelimitString + userField[i].DisplayText;

        if ((i + 1) != userField.length) {
            fieldValue += SPClientTemplates.Utility.UserLookupDelimitString
        }
    }

    ctx["CurrentFieldValue"] = fieldValue;
}

// Choice control needs specific formatted value to render content correctly.
function prepareMultiChoiceFieldValue(ctx) {

    if (ctx["CurrentFieldValue"]) {
        var fieldValue = ctx["CurrentFieldValue"];

        var find = ';#';
        var regExpObj = new RegExp(find, 'g');

        fieldValue = fieldValue.replace(regExpObj, '; ');
        fieldValue = fieldValue.replace(/^; /g, '');
        fieldValue = fieldValue.replace(/; $/g, '');

        ctx["CurrentFieldValue"] = fieldValue;
    }
}

// Note control needs specific formatted value to render content correctly.
function prepareNoteFieldValue(ctx) {

    if (ctx["CurrentFieldValue"]) {
        var fieldValue = ctx["CurrentFieldValue"];
        fieldValue = "<div>" + fieldValue.replace(/\n/g, '<br />'); + "</div>";

        ctx["CurrentFieldValue"] = fieldValue;
    }
} 
```

### <a name="sample-8-hide-fields"></a>Beispiel 8: Ausblenden Felder

Beispiel 8 zeigt, wie Felder in neuen Listenelement ausblenden und Formulare bearbeiten. Im Beispiel blendet das Feld **Vorgänger** , wenn ein Benutzer erstellt oder ein Aufgabenelement Liste bearbeitet.

In diesem Beispiel wird als bearbeiten und neue Formular für eine Liste namens **Liste CSR-ausblenden-Steuerelemente**bereitgestellt. Informationen dazu, wie Sie die Ansicht des Formulars nach der Bereitstellung des Beispiels finden Sie unter [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering).

Der folgende Code sucht das Feld **Vorgänger** in der HTML-Code des Formulars und ausgeblendet werden. Das Feld bleibt in der HTML-Code vorhanden, aber der Benutzer nicht im Browser angezeigt.

```
(function () {

    // jQuery library is required in this sample.
    // Fallback to loading jQuery from a CDN path if the local is unavailable.
    (window.jQuery || document.write('<script src="//ajax.aspnetcdn.com/ajax/jquery/jquery-1.10.0.min.js"><\/script>'));

    // Create object that has the context information about the field that we want to render differently.
    var hiddenFiledContext = {};
    hiddenFiledContext.Templates = {}; 
    hiddenFiledContext.Templates.OnPostRender = hiddenFiledOnPreRender;
    hiddenFiledContext.Templates.Fields = {
        // Apply the new rendering for Predecessors field in New and Edit forms.
        "Predecessors": {
            "NewForm": hiddenFiledTemplate,
            "EditForm": hiddenFiledTemplate
        }
    };

    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(hiddenFiledContext);

})();


// This function provides the rendering logic.
function hiddenFiledTemplate() {
    return "<span class='csrHiddenField'></span>";
}

// This function provides the rendering logic.
function hiddenFiledOnPreRender(ctx) {
    jQuery(".csrHiddenField").closest("tr").hide();
}

```

## <a name="web-part-and-add-in-part-manipulation"></a>Add-in-Teil zusammenstellen und Webparts
<a name="bmPersonalized"> </a>

Das [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) -Beispiel veranschaulicht, wie Add-in-Skript-Komponenten nutzen, Skripts, die in einer vom Anbieter gehosteten-add-in ausgeführt wird, auf einer SharePoint-Seite einbetten. Dieses Beispiel zeigt, wie die Benutzeroberfläche einer Seite auf der Hostwebsite zu ändern, indem Sie ein Webpart-Add-in-Skript bereitstellen und es einer SharePoint-Seite aus dem Webpartkatalog hinzufügen.

Ein Webpart-Add-in-Skript ist wie ein Webpart, können Sie es zu einer SharePoint-Seite aus dem Webpartkatalog hinzufügen, aber die Webpart-Datei eingebettet in diesem Fall eine JavaScript-Datei, die in einer vom Anbieter gehosteten-Add-in Remote ausgeführt wird. Das Webpart-Add-in-Skript ausgeführt wird, innerhalb einer `<div>` -Tag auf der SharePoint-Seite und bietet eine verbesserte Reaktionsgeschwindigkeit Design- und Erfahrung als Sie abrufen mit Add-in-Webparts, die in IFrames ausgeführt.

Die Startseite enthält eine **Szenario ausführen** -Schaltfläche, die das Webpart-Add-in-Skript in den Webpartkatalog bereitgestellt wird. Das folgende Codebeispiel erstellt eine **FileCreationInformationObject** -Instanz, die den Inhalt der Webpart-Datei enthält, und dann wird die neue Datei in den Webpartkatalog hochgeladen. Beachten Sie, dass Sie auch diesen Code automatisch ausgeführt werden können, wenn das Webpart-Add-in installiert oder als Teil der Websitesammlung Bereitstellungsprozesses.

```
var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    var folder = clientContext.Web.Lists.GetByTitle("Web Part Gallery").RootFolder;
    clientContext.Load(folder);
    clientContext.ExecuteQuery();

    // Upload the OneDrive for Business Usage Guidelines.docx.
    using (var stream = System.IO.File.OpenRead(Server.MapPath("~/userprofileinformation.webpart")))
    {
        FileCreationInformation fileInfo = new FileCreationInformation();
        fileInfo.ContentStream = stream;
        fileInfo.Overwrite = true;
        fileInfo.Url = "userprofileinformation.webpart";
        File file = folder.Files.Add(fileInfo);
        clientContext.ExecuteQuery();
    }

    // Update the group for uplaoded web part.
    var list = clientContext.Web.Lists.GetByTitle("Web Part Gallery");
    CamlQuery camlQuery = CamlQuery.CreateAllItemsQuery(100);
    Microsoft.SharePoint.Client.ListItemCollection items = list.GetItems(camlQuery);
    clientContext.Load(items);
    clientContext.ExecuteQuery();
    foreach (var item in items)
    {
        // Random group name to differentiate it from the rest.
        if (item["FileLeafRef"].ToString().ToLowerInvariant() == "userprofileinformation.webpart")
        {
            item["Group"] = "add-in Script Part";
            item.Update();
            clientContext.ExecuteQuery();
        }
    }

    lblStatus.Text = string.Format("add-in script part has been added to web part gallery. You can find 'User Profile Information' script part under 'Add-in Script Part' group in the <a href='{0}'>host web</a>.", spContext.SPHostUrl.ToString());
}
```

Nachdem Sie diesen Schritt abgeschlossen haben, können Sie in den Webpartkatalog das **Benutzerprofilinformationen** Add-in-Skript in eine neue **Add-in-Skript Teil** Kategorie Teil suchen. Nachdem Sie das Webpart-Add-in-Skript auf der Seite hinzufügen, steuert das Remote ausgeführte JavaScript die Anzeige von Informationen auf der Seite.

Wenn Sie das Add-in-Skript-Webpart im Bearbeitungsmodus anzeigen, sehen Sie sich, dass sie die JavaScript-Datei eingebettet, die Remote ausgeführt wird. Das userprofileinformation.js-Skript verwendet die JSON Benutzerprofilinformationen aus der Hostwebsite abrufen. 

```
function sharePointReady() {
  clientContext = SP.ClientContext.get_current();

  var fileref = document.createElement('script');
  fileref.setAttribute("type", "text/javascript");
  fileref.setAttribute("src", "/_layouts/15/SP.UserProfiles.js");
  document.getElementsByTagName("head")[0].appendChild(fileref);

  SP.SOD.executeOrDelayUntilScriptLoaded(function () {

    //Get Instance of People Manager Class       
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext);

    //Get properties of the current user
    userProfileProperties = peopleManager.getMyProperties();
    clientContext.load(userProfileProperties);
    clientContext.executeQueryAsync(Function.createDelegate(this, function (sender, args) {
      var firstname = userProfileProperties.get_userProfileProperties()['FirstName'];
      var name = userProfileProperties.get_userProfileProperties()['PreferredName'];
      var title = userProfileProperties.get_userProfileProperties()['Title'];
      var aboutMe = userProfileProperties.get_userProfileProperties()['AboutMe'];
      var picture = userProfileProperties.get_userProfileProperties()['PictureURL'];

      var html = "<div><h2>Welcome " + firstname + "</h2></div><div><div style='float: left; margin-left:10px'><img style='float:left;margin-right:10px' src='" + picture + "' /><b>Name</b>: " + name + "<br /><b>Title</b>: " + title + "<br />" + aboutMe + "</div></div>";

      document.getElementById('UserProfileAboutMe').innerHTML = html;
    }), Function.createDelegate(this, function (sender, args) {
      console.log('The following error has occurred while loading user profile property: ' + args.get_message());
    }));
  }, 'SP.UserProfiles.js');
}

```

## <a name="provisioning-publishing-features"></a>Bereitstellen von Veröffentlichungsfeatures
<a name="bmPersonalized"> </a>

Das [Provisioning.PublishingFeatures](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.PublishingFeatures) -Beispiel zeigt, wie für allgemeine Aufgaben mit der Veröffentlichung von Websites, die in Office 365 gehostet werden. Bereitstellung und mithilfe von Seitenlayouts, Masterseiten und Designs oder Einbetten von JavaScript in Seitenlayouts. Außerdem gezeigt, wie Filter anwenden, die steuern, welche Websitevorlagen für Unterwebsites verfügbar sind und welche Seitenlayouts sind auf dem hostweb verfügbar.

Das Add-in vom Anbieter gehosteten CSOM Benutzeroberflächenelemente auf Veröffentlichungswebsites Bereitstellung häufig verwendet werden und verwendet JavaScript, dynamischere Erfahrungen in Seitenlayouts zu erstellen, die Sie für die Veröffentlichung von Websites bereitstellen können. Es werden auch die Unterschiede zwischen der Verwendung von Masterseiten und Designs in Veröffentlichungswebsites.

**Wichtig:**  Wenn die Funktionalität in diese Beispiel arbeiten möchten, müssen Sie die Veröffentlichungsfeatures auf Ihrer Website zu aktivieren. Informationen finden Sie unter [Aktivieren von Veröffentlichungsfeatures](https://support.office.com/en-us/article/Enable-publishing-features-479677a6-8b33-4ac7-907d-071c1c7e4518?CorrelationId=22291615-2acd-46be-8813-9e6c48d01a32&amp;ui=en-US&amp;rs=en-US&amp;ad=US).

Die Start-Beispielseite bietet Ihnen drei Szenarien für die Anpassung der Benutzeroberfläche der Veröffentlichungswebsites: 

- Bereitstellen von Seitenlayouts.
    
- Bereitstellen von Masterseiten und Designs.
    
- Die verfügbaren Seitenlayouts und Websitevorlagen auf der Hostwebsite zu filtern.

### <a name="scenario-1-deploy-pages"></a>Szenario 1: Bereitstellen von Seiten

Szenario 1 zeigt, wie ein benutzerdefiniertes Seitenlayout bereitstellen. Die in Abbildung 11 dargestellte **Deploy Seitenlayouts** Schaltfläche erstellt ein neues Seitenlayout und die Seite, die das Layout verwendet.

**Abbildung 11. Schaltfläche zum Bereitstellen von Seitenlayouts**

![Schaltfläche, die Seitenlayouts bereitgestellt wird.](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/141b3b83-9a74-4528-825a-efd94183526d.png)

Sie können die neue Seite durch Aufrufen der neu erstellten Demoseite auf Ihrer Hostwebsite, die enthält eingebetteten JavaScript und zeigt die Benutzerprofilinformationen anzeigen.

Das Beispiel zeigt Informationen des Benutzers auf der Seite. Außerdem wird eine Seite hinzugefügt, in diesem Fall es ein **PublishingPageInformation** -Objekt verwendet, um die neue Seite erstellen.

Im Beispiel wird ein neues Seitenlayout durch Hochladen einer Datei auf den Gestaltungsvorlagenkatalog und Zuweisen des Seite Layout Inhaltstyps hinzugefügt. Der folgende Code akzeptiert den Pfad zu einer ASPX-Datei (die Sie in Ihrem Visual Studio 2013-Projekt als Ressource bereitstellen können) und fügt es als ein Seitenlayout im Gestaltungsvorlagenkatalog hinzu.

```
// Get the path to the file that you are about to deploy.
            List masterPageGallery = web.GetCatalog((int)ListTemplateType.MasterPageCatalog);
            Folder rootFolder = masterPageGallery.RootFolder;
            web.Context.Load(masterPageGallery);
            web.Context.Load(rootFolder);
            web.Context.ExecuteQuery();

            var fileBytes = System.IO.File.ReadAllBytes(sourceFilePath);

            // Use CSOM to upload the file.
            FileCreationInformation newFile = new FileCreationInformation();
            newFile.Content = fileBytes;
            newFile.Url = UrlUtility.Combine(rootFolder.ServerRelativeUrl, fileName);
            newFile.Overwrite = true;

            Microsoft.SharePoint.Client.File uploadFile = rootFolder.Files.Add(newFile);
            web.Context.Load(uploadFile);
            web.Context.ExecuteQuery();

            // Check out the file if needed.
            if (masterPageGallery.ForceCheckout || masterPageGallery.EnableVersioning)
            {
                if (uploadFile.CheckOutType == CheckOutType.None)
                {
                    uploadFile.CheckOut();
                }
            }

            // Get content type for ID to assign associated content type information.
            ContentType associatedCt = web.GetContentTypeById(associatedContentTypeID);

            var listItem = uploadFile.ListItemAllFields;
            listItem["Title"] = title;
            listItem["MasterPageDescription"] = description;
            // Set the item as page layout.
            listItem["ContentTypeId"] = Constants.PAGE_LAYOUT_CONTENT_TYPE;
            // Set the associated content type ID property
            listItem["PublishingAssociatedContentType"] = string.Format(";#{0};#{1};#", associatedCt.Name, associatedCt.Id);
            listItem["UIVersion"] = Convert.ToString(15);
            listItem.Update();

            // Check in the page layout if needed.
            if (masterPageGallery.ForceCheckout || masterPageGallery.EnableVersioning)
            {
                uploadFile.CheckIn(string.Empty, CheckinType.MajorCheckIn);
                listItem.File.Publish(string.Empty);
            }
            web.Context.ExecuteQuery();
```

Sie können überprüfen, ob die neue Seite auf das neue Seitenlayout verwendet wird, durch das Aufrufen der Bibliothek für **Seiten** der Hostwebsite.

### <a name="scenario-2-deploy-master-pages-and-themes"></a>Szenario 2: Bereitstellen von Masterseiten und Designs

Szenario 2 zeigt, wie zum Bereitstellen und Festlegen von Masterseiten und Designs für die Hostwebsite aus einer vom Anbieter gehosteten-add-in. Wenn Sie **Deploy master herunter, und** klicken Sie auf der Startseite Beispiel auswählen, wird im Beispiel bereitgestellt und wendet eine benutzerdefinierte Gestaltungsvorlage auf der Hostwebsite. Sie können neue Gestaltungsvorlage sehen, indem Sie auf der Homepage der Website.

Im Beispiel wird eine neue Gestaltungsvorlage durch Hochladen einer Master-Datei in den Gestaltungsvorlagenkatalog und Zuweisen des Gestaltungsvorlage Inhaltstyps hinzugefügt. Der folgende Code akzeptiert den Pfad zu einem Master-Datei (die Sie in Ihrem Visual Studio 2013-Projekt als Ressource bereitstellen können) und fügt es als eine Gestaltungsvorlage im Gestaltungsvorlagenkatalog hinzu.

```
string fileName = Path.GetFileName(sourceFilePath);

            // Get the path to the file that you are about to deploy.
            List masterPageGallery = web.GetCatalog((int)ListTemplateType.MasterPageCatalog);
            Folder rootFolder = masterPageGallery.RootFolder;
            web.Context.Load(masterPageGallery);
            web.Context.Load(rootFolder);
            web.Context.ExecuteQuery();

            // Get the file name from the provided path.
            var fileBytes = System.IO.File.ReadAllBytes(sourceFilePath);

            // Use CSOM to upload the file.
            FileCreationInformation newFile = new FileCreationInformation();
            newFile.Content = fileBytes;
            newFile.Url = UrlUtility.Combine(rootFolder.ServerRelativeUrl, fileName);
            newFile.Overwrite = true;

            Microsoft.SharePoint.Client.File uploadFile = rootFolder.Files.Add(newFile);
            web.Context.Load(uploadFile);
            web.Context.ExecuteQuery();


            var listItem = uploadFile.ListItemAllFields;
            if (masterPageGallery.ForceCheckout || masterPageGallery.EnableVersioning)
            {
                if (uploadFile.CheckOutType == CheckOutType.None)
                {
                    uploadFile.CheckOut();
                }
            }

            listItem["Title"] = title;
            listItem["MasterPageDescription"] = description;
            // Set content type as master page.
            listItem["ContentTypeId"] = Constants.MASTERPAGE_CONTENT_TYPE;
            listItem["UIVersion"] = uiVersion;
            listItem.Update();
            if (masterPageGallery.ForceCheckout || masterPageGallery.EnableVersioning)
            {
                uploadFile.CheckIn(string.Empty, CheckinType.MajorCheckIn);
                listItem.File.Publish(string.Empty);
            }
            web.Context.Load(listItem);
            web.Context.ExecuteQuery();
```

Im nächste Schritt wird die URL der neuen Gestaltungsvorlage als Wert für die **MasterUrl** und die **CustomMasterUrl** Eigenschaften des **Web** -Objekts festgelegt, das die Website darstellt. Im Beispiel behandelt dies mit einer einzelnen Methode, die die URL der neuen Gestaltungsvorlage im Gestaltungsvorlagenkatalog abruft und klicken Sie dann auf die Eigenschaften **Web.MasterUrl** und **Web.CustomMasterUrl** weist diesen Wert.

```
// Assign master page to the host web.
                clientContext.Web.SetMasterPagesForSiteByName("contoso.master", "contoso.master");

```

Bei der Auswahl **Design bereitstellen und verwenden sie**das Beispiel bereitgestellt und ein benutzerdefiniertes Design auf der Hostwebsite angewendet. Im Beispiel wird die Farbpalette, Hintergrundbild und Schriftartenschema des Designs durch Hinzufügen eines neuen Designs mit diesen Werten (die Sie als Ressourcen innerhalb des Visual Studio 2013-Projekts bereitstellen) in den Designkatalog. Mit dem folgende Code wird das neue Design erstellt.

```
List themesOverviewList = web.GetCatalog((int)ListTemplateType.DesignCatalog);
           web.Context.Load(themesOverviewList);
           web.Context.ExecuteQuery(); 
                ListItemCreationInformation itemInfo = new ListItemCreationInformation();
                Microsoft.SharePoint.Client.ListItem item = themesOverviewList.AddItem(itemInfo);
                item["Name"] = themeName;
                item["Title"] = themeName;
                if (!string.IsNullOrEmpty(colorFileName))
                {
                    item["ThemeUrl"] = UrlUtility.Combine(rootWeb.ServerRelativeUrl, string.Format(Constants.THEMES_DIRECTORY, Path.GetFileName(colorFileName)));
                }
                if (!string.IsNullOrEmpty(fontFileName))
                {
                    item["FontSchemeUrl"] = UrlUtility.Combine(rootWeb.ServerRelativeUrl, string.Format(Constants.THEMES_DIRECTORY, Path.GetFileName(fontFileName)));
                }
                if (!string.IsNullOrEmpty(backgroundName))
                {
                    item["ImageUrl"] = UrlUtility.Combine(rootWeb.ServerRelativeUrl, string.Format(Constants.THEMES_DIRECTORY, Path.GetFileName(backgroundName)));
                }
                item["DisplayOrder"] = 11;
                item.Update();
                web.Context.ExecuteQuery();
```

Im nächste Schritt wird das dieses neue Design als das Design für die Website festgelegt. Mit dem folgende Code wird das Abrufen des Designs aus der Design Gallery und die Werte auf der Hostwebsite anwenden.

```
 CamlQuery query = new CamlQuery();
                // Find the theme by themeName.
                string camlString = string.Format(CAML_QUERY_FIND_BY_FILENAME, themeName);
                query.ViewXml = camlString;
                var found = themeList.GetItems(query);
                rootWeb.Context.Load(found);
                LoggingUtility.Internal.TraceVerbose("Getting theme: {0}", themeName);
                rootWeb.Context.ExecuteQuery();
                if (found.Count > 0)
                {
                    ListItem themeEntry = found[0];

                    / /Set the properties for applying the custom theme that was just uploaded.
                    string spColorURL = null;
                    if (themeEntry["ThemeUrl"] != null &amp;&amp; themeEntry["ThemeUrl"].ToString().Length > 0)
                    {
                        spColorURL = UrlUtility.MakeRelativeUrl((themeEntry["ThemeUrl"] as FieldUrlValue).Url);
                    }
                    string spFontURL = null;
                    if (themeEntry["FontSchemeUrl"] != null &amp;&amp; themeEntry["FontSchemeUrl"].ToString().Length > 0)
                    {
                        spFontURL = UrlUtility.MakeRelativeUrl((themeEntry["FontSchemeUrl"] as FieldUrlValue).Url);
                    }
                    string backGroundImage = null;
                    if (themeEntry["ImageUrl"] != null &amp;&amp; themeEntry["ImageUrl"].ToString().Length > 0)
                    {
                        backGroundImage = UrlUtility.MakeRelativeUrl((themeEntry["ImageUrl"] as FieldUrlValue).Url);
                    }

                    // Set theme for demonstration.
                    // TODO: Why is shareGenerated false? If deploying to root an inheriting, then maybe use shareGenerated = true.
                    web.ApplyTheme(spColorURL,
                                        spFontURL,
                                        backGroundImage,
                                        false);
                    web.Context.ExecuteQuery();
```

### <a name="scenario-3-filter-available-page-layouts-and-site-templates"></a>Szenario 3: Filtern Sie verfügbaren Seitenlayouts und Websitevorlagen

Szenario 3 zeigt, wie die Optionen zu begrenzen, die Benutzer haben, wenn sie Vorlagen für neue Websites und Layouts, um neue Seiten gelten. Wenn Sie auf **Apply Filter mit Hostwebsite** wählen im Beispiel Startseite, im Beispiel wird ein benutzerdefiniertes Seitenlayout als Standard und eine zusätzliche Seitenlayout als einzige andere Option für neuen Seiten, die ein Benutzer erstellt. Im Beispiel reduziert auch die Anzahl der verfügbaren Optionen für Benutzer beim Erstellen von neuen Unterwebsites. Abbildung 12 zeigt, wie das Auswahlfeld Vorlage Website aussieht, bevor und nachdem die Filter angewendet wurden.

**Abbildung 12. Site-Vorlagenauswahl before und after Beispielfilter angewendet wurden**

![Site-Vorlagenauswahl before und after Beispielfilter angewendet wurden](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/46c0e39d-dfec-45ed-9b72-ff3f6d5e1916.png)

Festgelegt sowohl Standard-als auch verfügbaren Seitenlayouts, indem Sie die zugeordneten ASPX-Dateien, die Methoden zum Erweiterungsmethoden, übergeben, wie im Code gezeigt.

```
                List<string> pageLayouts = new List<string>();
                pageLayouts.Add("ContosoLinksBelow.aspx");
                pageLayouts.Add("ContosoLinksRight.aspx");
                clientContext.Web.SetAvailablePageLayouts(clientContext.Web, pageLayouts);

                // Set default page layout for the site
                clientContext.Web.SetDefaultPageLayoutForSite(clientContext.Web, "ContosoLinksBelow.aspx");

```
Im Beispiel wird die verfügbaren Websitevorlagen durch dann in etwa wie folgt. In diesem Fall wird die **WebTemplateEntity** -Instanzen, die jede Websitevorlage für eine Erweiterungsmethode namens **SetAvailableWebTemplates**definieren.

```
List<WebTemplateEntity> templates = new List<WebTemplateEntity>();
                templates.Add(new WebTemplateEntity() { LanguageCode = "1035", TemplateName = "STS#0" });
                templates.Add(new WebTemplateEntity() { LanguageCode = "", TemplateName = "STS#0" });
                templates.Add(new WebTemplateEntity() { LanguageCode = "", TemplateName = "BLOG#0" });
                clientContext.Web.SetAvailableWebTemplates(templates);

```

Alle drei dieser Erweiterungsmethoden - **SetAvailablePageLayouts**, **SetDefaultPageLayoutForSite**und **SetAvailableWebTemplates** - Arbeit in die gleiche Weise. Sie erstellen eine XML-Dokumente, die Schlüssel/Wert-Paare enthalten, die die verfügbaren und Standardlayouts und die verfügbaren Vorlagen definieren. Sie übergeben dann diese Dokumente an eine weitere Erweiterungsmethode **SetPropertyBagValue**aufgerufen. Diese Methode ist in [OfficeDevPnPCore Erweiterung](hhttps://github.com/SharePoint/PnP-sites-core)implementiert. Nachdem sie die entsprechenden Eigenschaftenbehälter einrichtet, werden diese Eigenschaftenbehälter klicken Sie dann zum Filtern von Optionen auf der Benutzeroberfläche verwendet.

Die drei Methoden zeigt **SetAvailableWebTemplates** das vollständige Muster.

```
public static void SetAvailableWebTemplates(this Web web, List<WebTemplateEntity> availableTemplates)
        {
            string propertyValue = string.Empty;

            LanguageTemplateHash languages = new LanguageTemplateHash();
            foreach (var item in availableTemplates)
            {
                AddTemplateToCollection(languages, item);
            }

            if (availableTemplates.Count > 0)
            {
                XmlDocument xd = new XmlDocument();
                XmlNode xmlNode = xd.CreateElement("webtemplates");
                xd.AppendChild(xmlNode);
                foreach (var language in languages)
                {
                    XmlNode xmlLcidNode = xmlNode.AppendChild(xd.CreateElement("lcid"));
                    XmlAttribute xmlAttribute = xd.CreateAttribute("id");
                    xmlAttribute.Value = language.Key;
                    xmlLcidNode.Attributes.SetNamedItem(xmlAttribute);

                    foreach (string item in language.Value)
                    {
                        XmlNode xmlWTNode = xmlLcidNode.AppendChild(xd.CreateElement("webtemplate"));
                        XmlAttribute xmlAttributeName = xd.CreateAttribute("name");
                        xmlAttributeName.Value = item;
                        xmlWTNode.Attributes.SetNamedItem(xmlAttributeName);
                    }
                }
                propertyValue = xmlNode.OuterXml;
            }
            // Save the XML entry to property bag.
            web.SetPropertyBagValue(AvailableWebTemplates, propertyValue);
            // Set that templates are not inherited.
            web.SetPropertyBagValue(InheritWebTemplates, "False");

```

Die Eigenschaftensammlung **InheritWebTemplates** stellt sicher, dass alle Vorlagen, die normalerweise von der übergeordneten Website geerbt werden beim Erstellen von Unterwebsites auch ignoriert werden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [UX-Komponenten in SharePoint 2013 und SharePoint Online](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [Provisioning.Pages](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages)
    
- [Branding.ApplyBranding](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ApplyBranding)
