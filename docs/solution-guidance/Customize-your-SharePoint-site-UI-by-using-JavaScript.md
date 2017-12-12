---
title: "Anpassen der Benutzeroberfläche der SharePoint-Website mithilfe von JavaScript"
ms.date: 11/03/2017
ms.openlocfilehash: f539d8e889f65a607d075e146d4ee0148862a0b0
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="customize-your-sharepoint-site-ui-by-using-javascript"></a>Anpassen der Benutzeroberfläche der SharePoint-Website mithilfe von JavaScript

Sie können Ihre SharePoint-Website-Benutzeroberfläche mithilfe von JavaScript aktualisieren.
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_
    
[Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) -Beispiel-add-in allen Seiten auf einer SharePoint-Website eine Meldung in der Statusleiste hinzugefügt und entfernt den Link **neue Unterwebsite** auf der Seite **Websiteinhalte** mithilfe von JavaScript. 
    
Verwenden Sie diese Lösung, wenn Sie anstelle von benutzerdefinierten Gestaltungsvorlagen erstellen UI-Updates mithilfe von JavaScript (auch als die Technik JavaScript einbetten bezeichnet) auf der SharePoint-Website anwenden möchten. 

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="using-the-coreembedjavascript-app"></a>Verwenden der app Core.EmbedJavaScript
<a name="sectionSection1"> </a>

Wenn Sie dieses Codebeispiel ausführen, angezeigt wird ein Add-in vom Anbieter gehostet, wie in Abbildung 1 dargestellt. 

**Abbildung 1. Screenshot des Core.EmbedJavaScript-add-in-Startseite**

![Screenshot der Startseite des Beispiels JavaScript einbetten](media/bdbf1df9-5027-4c6c-8ae9-152747fbbc1c.png)

Auswählen von **Embed-Anpassung** passt die SharePoint-Website durch:

- Erstellen eine Meldung in der Statusleiste auf allen Seiten in der SharePoint-Website, wie in Abbildung 2 dargestellt.
    
- Entfernen den Link **neue Unterwebsite** aus **Websiteinhalte** , wie in Abbildung 3 dargestellt.

**Abbildung 2. Screenshot der Statusleiste für alle Seiten hinzugefügt**

![Statusleiste hinzugefügt, um alle SharePoint-Websiteseiten](media/ccae4093-4640-4339-a5f2-1df66c117cdc.png)

**Abbildung 3. Screenshot der neuen Unterwebsite Verknüpfung von der Seite Websiteinhalte entfernt**

![Die neue Unterwebsite Verknüpfung auf Websiteinhalte wurde entfernt.](media/0631ce39-76e8-446a-b628-f41c2a066e4c.png)

In Abbildung 1 ruft auswählen **Embed Anpassung** **BtnSubmit_Click** default.aspx. **BtnSubmit_Click** ruft **AddJsLink**, die Folgendes ermöglicht:

1. Erstellt eine Zeichenfolge, die eine Definition der Skript-Block darstellt. Dieses Skript blockieren Definition verweist auf eine JavaScript-Datei (scenario1.js), die auf allen Seiten auf der SharePoint-Website verfügbar ist. 
    
2. Verwendet [UserCustomActions](https://msdn.microsoft.com/library/office/microsoft.sharepoint.spweb.usercustomactions%28v=office.15%29.aspx) zum Abrufen von benutzerdefinierten Aktionen aller Benutzer auf der SharePoint-Website definiert sind. Alle vorhandenen Verweis auf eine JavaScript-Datei scenario1.js aufgerufen wurde entfernt.
    
3.  Erstellt eine neue benutzerdefinierte Aktion, und weist die Skript blockieren Definition in Schritt 1, um die neue benutzerdefinierte Aktion erstellt.
    
4. Fügt die neue benutzerdefinierte Aktion auf der Website.
    
Alle Seiten auf der SharePoint-Website werden jetzt führen scenario1.js und zeigen die Anpassungen der Benutzeroberfläche in Abbildung 2 und Abbildung 3 dargestellt.
    
> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
 public void AddJsLink(ClientContext ctx, Web web)
        {
            string scenarioUrl = String.Format("{0}://{1}:{2}/Scripts", this.Request.Url.Scheme, 
                                                this.Request.Url.DnsSafeHost, this.Request.Url.Port);
            string revision = Guid.NewGuid().ToString().Replace("-", "");
            string jsLink = string.Format("{0}/{1}?rev={2}", scenarioUrl, "scenario1.js", revision);

            StringBuilder scripts = new StringBuilder(@"
                var headID = document.getElementsByTagName('head')[0]; 
                var");

            scripts.AppendFormat(@"
                newScript = document.createElement('script');
                newScript.type = 'text/javascript';
                newScript.src = '{0}';
                headID.appendChild(newScript);", jsLink);
            string scriptBlock = scripts.ToString();

            var existingActions = web.UserCustomActions;
            ctx.Load(existingActions);
            ctx.ExecuteQuery();
            var actions = existingActions.ToArray();
            foreach (var action in actions)
            {
                if (action.Description == "scenario1" &amp;&amp;
                    action.Location == "ScriptLink")
                {
                    action.DeleteObject();
                    ctx.ExecuteQuery();
                }
            }

            var newAction = existingActions.Add();
            newAction.Description = "scenario1";
            newAction.Location = "ScriptLink";

            newAction.ScriptBlock = scriptBlock;
            newAction.Update();
            ctx.Load(web, s => s.UserCustomActions);
            ctx.ExecuteQuery();
        }
```

SharePoint verwendet minimale herunterladen Strategie (MDS), um die Datenmenge zu reduzieren Browser heruntergeladen wird, wenn Benutzer zwischen den Seiten auf einer SharePoint-Website navigieren. Weitere Informationen finden Sie unter [Übersicht über die minimale Downloadstrategie](https://msdn.microsoft.com/library/office/dn456544%28v=office.15%29.aspx). In scenario1.js gewährleistet der folgende Code, die unabhängig davon, ob der SharePoint-Website verwendet die minimale Downloadstrategie, **RemoteManager_Inject** immer ausgeführt wird.

```
// Is MDS enabled?
if ("undefined" != typeof g_MinimalDownload &amp;&amp; g_MinimalDownload &amp;&amp; (window.location.pathname.toLowerCase()).endsWith("/_layouts/15/start.aspx") &amp;&amp; "undefined" != typeof asyncDeltaManager) {
    // Register script for MDS if possible
    RegisterModuleInit("scenario1.js", RemoteManager_Inject); //MDS registration
    RemoteManager_Inject(); //non MDS run
} else {
    RemoteManager_Inject();
}
```

**RemoteManager_Inject** führt die folgenden Aufgaben auf Ihrer SharePoint-Website:

- Erstellt eine Statusleiste auf dem hostweb.  **RemoteManager_Inject** verwendet [SP. SOD.executeOrDelayUntilScriptLoaded](https://msdn.microsoft.com/library/office/ff411788%28v=office.14%29.aspx) um sicherzustellen, dass sp.js zuerst geladen wird, vor dem Aufruf von **SetStatusBar** , um die Statusleiste der Website hinzufügen. Da JavaScript-Dateien asynchron geladen wird, mithilfe von **SP. SOD.executeOrDelayUntilScriptLoaded** wird sichergestellt, die JavaScript-Datei (sp.js) wird geladen, bevor der Code eine Funktion in der JavaScript-Datei definiert aufruft.
    
- Blendet die **neue Unterwebsite** Link auf der Seite **Websiteinhalte** aus.

```
function RemoteManager_Inject() {

    loadScript(jQuery, function () {
        $(document).ready(function () {
            var message = "<img src='/_Layouts/Images/STS_ListItem_43216.gif' align='absmiddle'> <font color='#AA0000'>JavaScript customization is <i>fun</i>!</font>"

            // Execute status setter only after SP.JS has been loaded
            SP.SOD.executeOrDelayUntilScriptLoaded(function () { SetStatusBar(message); }, 'sp.js');

            // Customize the viewlsts.aspx page
            if (IsOnPage("viewlsts.aspx")) {
                //hide the subsites link on the viewlsts.aspx page
                $("#createnewsite").parent().hide();
            }
        });
    });
}

function SetStatusBar(message) {
    var strStatusID = SP.UI.Status.addStatus("Information : ", message, true);
    SP.UI.Status.setStatusPriColor(strStatusID, "yellow");
}

function IsOnPage(pageName) {
    if (window.location.href.toLowerCase().indexOf(pageName.toLowerCase()) > -1) {
        return true;
    } else {
        return false;
    }
}

```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
    
-  [Vorgehensweise: Anpassen einer Listenansicht in-add-ins für SharePoint mithilfe von clientseitiges Rendering](https://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86.aspx)
