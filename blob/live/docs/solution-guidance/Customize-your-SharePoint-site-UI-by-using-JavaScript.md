---
title: "Anpassen der Benutzeroberfläche der SharePoint-Website mithilfe von JavaScript"
ms.date: 11/03/2017
ms.openlocfilehash: d5ab48173acb91fdcdfd0ce1ce4c57c86bef49a0
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="customize-your-sharepoint-site-ui-by-using-javascript"></a><span data-ttu-id="61ff8-102">Anpassen der Benutzeroberfläche der SharePoint-Website mithilfe von JavaScript</span><span class="sxs-lookup"><span data-stu-id="61ff8-102">Customize your SharePoint site UI by using JavaScript</span></span>

<span data-ttu-id="61ff8-103">Sie können Ihre SharePoint-Website-Benutzeroberfläche mithilfe von JavaScript aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="61ff8-103">You can update your SharePoint site's UI by using JavaScript.</span></span>
    
<span data-ttu-id="61ff8-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="61ff8-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="61ff8-105">[Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) -Beispiel-add-in allen Seiten auf einer SharePoint-Website eine Meldung in der Statusleiste hinzugefügt und entfernt den Link **neue Unterwebsite** auf der Seite **Websiteinhalte** mithilfe von JavaScript.</span><span class="sxs-lookup"><span data-stu-id="61ff8-105">The [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) sample add-in adds a status bar message to all pages on a SharePoint site, and removes the **new subsite** link from the **Site Contents** page by using JavaScript.</span></span> 
    
<span data-ttu-id="61ff8-106">Verwenden Sie diese Lösung, wenn Sie anstelle von benutzerdefinierten Gestaltungsvorlagen erstellen UI-Updates mithilfe von JavaScript (auch als die Technik JavaScript einbetten bezeichnet) auf der SharePoint-Website anwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="61ff8-106">Use this solution if you want to apply UI updates to your SharePoint site by using JavaScript (sometimes referred to as the Embed JavaScript technique) instead of creating custom master pages.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="61ff8-107">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="61ff8-107">Before you begin</span></span>
<span data-ttu-id="61ff8-108"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="61ff8-108"></span></span>

<span data-ttu-id="61ff8-109">Laden Sie Sie zuerst [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="61ff8-109">To get started, download the  [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-coreembedjavascript-app"></a><span data-ttu-id="61ff8-110">Verwenden der app Core.EmbedJavaScript</span><span class="sxs-lookup"><span data-stu-id="61ff8-110">Using the Core.EmbedJavaScript app</span></span>
<span data-ttu-id="61ff8-111"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="61ff8-111"></span></span>

<span data-ttu-id="61ff8-112">Wenn Sie dieses Codebeispiel ausführen, angezeigt wird ein Add-in vom Anbieter gehostet, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="61ff8-112">When you run this code sample, a provider-hosted add-in appears, as shown in Figure 1.</span></span> 

<span data-ttu-id="61ff8-113">**Abbildung 1. Screenshot des Core.EmbedJavaScript-add-in-Startseite**</span><span class="sxs-lookup"><span data-stu-id="61ff8-113">**Figure 1. Screen shot of Core.EmbedJavaScript add-in start page**</span></span>

![Screenshot der Startseite des Beispiels JavaScript einbetten](media/bdbf1df9-5027-4c6c-8ae9-152747fbbc1c.png)

<span data-ttu-id="61ff8-115">Auswählen von **Embed-Anpassung** passt die SharePoint-Website durch:</span><span class="sxs-lookup"><span data-stu-id="61ff8-115">Choosing  **Embed customization** customizes the SharePoint site by:</span></span>

- <span data-ttu-id="61ff8-116">Erstellen eine Meldung in der Statusleiste auf allen Seiten in der SharePoint-Website, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="61ff8-116">Creating a status bar message on all pages in the SharePoint site, as shown in Figure 2.</span></span>
    
- <span data-ttu-id="61ff8-117">Entfernen den Link **neue Unterwebsite** aus **Websiteinhalte** , wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="61ff8-117">Removing the  **new subsite** link from **Site Contents** as shown in Figure 3.</span></span>

<span data-ttu-id="61ff8-118">**Abbildung 2. Screenshot der Statusleiste für alle Seiten hinzugefügt**</span><span class="sxs-lookup"><span data-stu-id="61ff8-118">**Figure 2. Screen shot of status bar added to all pages**</span></span>

![Statusleiste hinzugefügt, um alle SharePoint-Websiteseiten](media/ccae4093-4640-4339-a5f2-1df66c117cdc.png)

<span data-ttu-id="61ff8-120">**Abbildung 3. Screenshot der neuen Unterwebsite Verknüpfung von der Seite Websiteinhalte entfernt**</span><span class="sxs-lookup"><span data-stu-id="61ff8-120">**Figure 3. Screen shot of new subsite link removed from the Site Contents page**</span></span>

![Die neue Unterwebsite Verknüpfung auf Websiteinhalte wurde entfernt.](media/0631ce39-76e8-446a-b628-f41c2a066e4c.png)

<span data-ttu-id="61ff8-122">In Abbildung 1 ruft auswählen **Embed Anpassung** **BtnSubmit_Click** default.aspx.</span><span class="sxs-lookup"><span data-stu-id="61ff8-122">In Figure 1, choosing  **Embed customization** calls **btnSubmit_Click** in default.aspx.</span></span> <span data-ttu-id="61ff8-123">**BtnSubmit_Click** ruft **AddJsLink**, die Folgendes ermöglicht:</span><span class="sxs-lookup"><span data-stu-id="61ff8-123">**btnSubmit_Click** calls **AddJsLink**, which does the following:</span></span>

1. <span data-ttu-id="61ff8-124">Erstellt eine Zeichenfolge, die eine Definition der Skript-Block darstellt.</span><span class="sxs-lookup"><span data-stu-id="61ff8-124">Creates a string representing a script block definition.</span></span> <span data-ttu-id="61ff8-125">Dieses Skript blockieren Definition verweist auf eine JavaScript-Datei (scenario1.js), die auf allen Seiten auf der SharePoint-Website verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="61ff8-125">This script block definition points to a JavaScript file (scenario1.js) which is included on all pages on the SharePoint site.</span></span> 
    
2. <span data-ttu-id="61ff8-126">Verwendet [UserCustomActions](https://msdn.microsoft.com/library/office/microsoft.sharepoint.spweb.usercustomactions%28v=office.15%29.aspx) zum Abrufen von benutzerdefinierten Aktionen aller Benutzer auf der SharePoint-Website definiert sind.</span><span class="sxs-lookup"><span data-stu-id="61ff8-126">Uses  [UserCustomActions](https://msdn.microsoft.com/library/office/microsoft.sharepoint.spweb.usercustomactions%28v=office.15%29.aspx) to get all user custom actions defined on the SharePoint site.</span></span> <span data-ttu-id="61ff8-127">Alle vorhandenen Verweis auf eine JavaScript-Datei scenario1.js aufgerufen wurde entfernt.</span><span class="sxs-lookup"><span data-stu-id="61ff8-127">Any existing reference to a JavaScript file called scenario1.js is removed.</span></span>
    
3.  <span data-ttu-id="61ff8-128">Erstellt eine neue benutzerdefinierte Aktion, und weist die Skript blockieren Definition in Schritt 1, um die neue benutzerdefinierte Aktion erstellt.</span><span class="sxs-lookup"><span data-stu-id="61ff8-128">Creates a new custom action, and assigns the script block definition created in step 1 to the new custom action.</span></span>
    
4. <span data-ttu-id="61ff8-129">Fügt die neue benutzerdefinierte Aktion auf der Website.</span><span class="sxs-lookup"><span data-stu-id="61ff8-129">Adds the new custom action to the website.</span></span>
    
<span data-ttu-id="61ff8-130">Alle Seiten auf der SharePoint-Website werden jetzt führen scenario1.js und zeigen die Anpassungen der Benutzeroberfläche in Abbildung 2 und Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="61ff8-130">All pages on your SharePoint site will now run scenario1.js and display the UI customizations shown in Figure 2 and Figure 3.</span></span>
    
<span data-ttu-id="61ff8-131">**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="61ff8-131">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="61ff8-132">SharePoint verwendet minimale herunterladen Strategie (MDS), um die Datenmenge zu reduzieren Browser heruntergeladen wird, wenn Benutzer zwischen den Seiten auf einer SharePoint-Website navigieren.</span><span class="sxs-lookup"><span data-stu-id="61ff8-132">SharePoint uses Minimal Download Strategy (MDS) to reduce the amount of data the browser downloads when users navigate between pages on a SharePoint site.</span></span> <span data-ttu-id="61ff8-133">Weitere Informationen finden Sie unter [Übersicht über die minimale Downloadstrategie](https://msdn.microsoft.com/library/office/dn456544%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="61ff8-133">For more information, see  [Minimal Download Strategy overview](https://msdn.microsoft.com/library/office/dn456544%28v=office.15%29.aspx).</span></span> <span data-ttu-id="61ff8-134">In scenario1.js gewährleistet der folgende Code, die unabhängig davon, ob der SharePoint-Website verwendet die minimale Downloadstrategie, **RemoteManager_Inject** immer ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="61ff8-134">In scenario1.js, the following code ensures that whether or not your SharePoint site uses Minimal Download Strategy,  **RemoteManager_Inject** always runs.</span></span>

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

<span data-ttu-id="61ff8-135">**RemoteManager_Inject** führt die folgenden Aufgaben auf Ihrer SharePoint-Website:</span><span class="sxs-lookup"><span data-stu-id="61ff8-135">**RemoteManager_Inject** performs the following tasks on your SharePoint site:</span></span>

- <span data-ttu-id="61ff8-136">Erstellt eine Statusleiste auf dem hostweb.</span><span class="sxs-lookup"><span data-stu-id="61ff8-136">Creates a status bar on the host web.</span></span>  <span data-ttu-id="61ff8-137">**RemoteManager_Inject** verwendet [SP. SOD.executeOrDelayUntilScriptLoaded](https://msdn.microsoft.com/library/office/ff411788%28v=office.14%29.aspx) um sicherzustellen, dass sp.js zuerst geladen wird, vor dem Aufruf von **SetStatusBar** , um die Statusleiste der Website hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="61ff8-137">**RemoteManager_Inject** uses [SP.SOD.executeOrDelayUntilScriptLoaded](https://msdn.microsoft.com/library/office/ff411788%28v=office.14%29.aspx) to ensure sp.js is loaded first, before calling **SetStatusBar** to add the status bar to the site.</span></span> <span data-ttu-id="61ff8-138">Da JavaScript-Dateien asynchron geladen wird, mithilfe von **SP. SOD.executeOrDelayUntilScriptLoaded** wird sichergestellt, die JavaScript-Datei (sp.js) wird geladen, bevor der Code eine Funktion in der JavaScript-Datei definiert aufruft.</span><span class="sxs-lookup"><span data-stu-id="61ff8-138">Because JavaScript files load asynchronously, using **SP.SOD.executeOrDelayUntilScriptLoaded** ensures your JavaScript file (sp.js) is loaded before your code calls a function defined in that JavaScript file.</span></span>
    
- <span data-ttu-id="61ff8-139">Blendet die **neue Unterwebsite** Link auf der Seite **Websiteinhalte** aus.</span><span class="sxs-lookup"><span data-stu-id="61ff8-139">Hides the  **new subsite** link on the **Site Contents** page.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="61ff8-140">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="61ff8-140">Additional resources</span></span>
<span data-ttu-id="61ff8-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="61ff8-141"></span></span>

-  [<span data-ttu-id="61ff8-142">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="61ff8-142">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="61ff8-143">Core.JavaScriptCustomization</span><span class="sxs-lookup"><span data-stu-id="61ff8-143">Core.JavaScriptCustomization</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
    
-  [<span data-ttu-id="61ff8-144">Vorgehensweise: Anpassen einer Listenansicht in-add-ins für SharePoint mithilfe von clientseitiges Rendering</span><span class="sxs-lookup"><span data-stu-id="61ff8-144">How to: Customize a list view in add-ins for SharePoint using client-side rendering</span></span>](https://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86.aspx)
