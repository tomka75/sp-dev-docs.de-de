---
title: Passen Sie die UX mithilfe von SharePoint gehostet durch Drittanbieter-add-ins
ms.date: 11/03/2017
ms.openlocfilehash: 28f14fa6a15e367232b1384952ed6b7fefbfb3de
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="customize-the-ux-by-using-sharepoint-provider-hosted-add-ins"></a><span data-ttu-id="5721c-102">Passen Sie die UX mithilfe von SharePoint gehostet durch Drittanbieter-add-ins</span><span class="sxs-lookup"><span data-stu-id="5721c-102">Customize the UX by using SharePoint provider-hosted add-ins</span></span>

<span data-ttu-id="5721c-103">Anpassen von SharePoint-UX-Komponenten Remote mit vom Anbieter gehosteten-add-ins.</span><span class="sxs-lookup"><span data-stu-id="5721c-103">Customize SharePoint UX components remotely by using provider-hosted add-ins.</span></span> 

<span data-ttu-id="5721c-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="5721c-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="5721c-105">In diesem Artikel wird beschrieben, Beispiele, in denen bewährte Methoden zum Anpassen von SharePoint-UX-Komponenten, einschließlich der folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="5721c-105">This article describes samples that show best practices for customizing SharePoint UX components, including the following scenarios:</span></span>

- <span data-ttu-id="5721c-106">Seite Manipulation (hinzufügen und Ändern von Wiki-Seiten).</span><span class="sxs-lookup"><span data-stu-id="5721c-106">Page manipulation (adding and modifying a wiki page).</span></span>
    
- <span data-ttu-id="5721c-107">-Add-ins und Daten anzeigt in modale Dialogfelder.</span><span class="sxs-lookup"><span data-stu-id="5721c-107">Showing add-ins and data in modal dialog boxes.</span></span>
    
- <span data-ttu-id="5721c-108">Erstellen von personalisierten Benutzeroberflächenelemente.</span><span class="sxs-lookup"><span data-stu-id="5721c-108">Creating personalized UI elements.</span></span>
    
- <span data-ttu-id="5721c-109">Clientseitiges Rendering (JSLink-Dateien, die das Rendern von Feldern in SharePoint-Listen anpassen bereitstellen).</span><span class="sxs-lookup"><span data-stu-id="5721c-109">Client-side rendering (deploying JSLink files that customize the rendering of fields in SharePoint lists).</span></span>
    
- <span data-ttu-id="5721c-110">Webpart und Webpart-Add-in Bearbeitung (Remote bereitstellen und Ausführen eines Add-in-Skript-Webparts in einer vom Anbieter gehosteten-Add-in).</span><span class="sxs-lookup"><span data-stu-id="5721c-110">Web Part and add-in part manipulation (remotely provision and run an add-in script part in a provider-hosted add-in).</span></span>
    
- <span data-ttu-id="5721c-111">Datenaggregation und Zwischenspeichern (mit lokalen Speicher HTML5 und HTTP-Cookies reduzieren Sie die Anzahl der Aufrufe an SharePoint Service).</span><span class="sxs-lookup"><span data-stu-id="5721c-111">Data aggregation and caching (using HTML5 local storage and HTTP cookies to reduce the number of service calls to SharePoint).</span></span>

## <a name="page-manipulation"></a><span data-ttu-id="5721c-112">Seite zum Bearbeiten</span><span class="sxs-lookup"><span data-stu-id="5721c-112">Page manipulation</span></span>
<span data-ttu-id="5721c-113"><a name="bmPageManipulate"> </a></span><span class="sxs-lookup"><span data-stu-id="5721c-113"></span></span>

<span data-ttu-id="5721c-114">Im Beispiel [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ModifyPages) umfasst zwei Szenarien für die Bearbeitung von Seiten:</span><span class="sxs-lookup"><span data-stu-id="5721c-114">The [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ModifyPages) sample includes two page manipulation scenarios:</span></span>

- <span data-ttu-id="5721c-115">Erstellen Sie eine Wiki-Seite.</span><span class="sxs-lookup"><span data-stu-id="5721c-115">Create a wiki page.</span></span>
    
- <span data-ttu-id="5721c-116">Ändern des Layouts einer Wiki-Seite.</span><span class="sxs-lookup"><span data-stu-id="5721c-116">Modify the layout of a wiki page.</span></span> 
    
<span data-ttu-id="5721c-117">Dieses Beispiel verwendet die standardmäßige Website Seitenbibliothek und vorhandenen Out-of-the-Box Layouts.</span><span class="sxs-lookup"><span data-stu-id="5721c-117">This sample uses the default site pages library and existing out-of-the-box layouts.</span></span> <span data-ttu-id="5721c-118">Sie können auch aktualisieren, um eine benutzerdefinierte Wiki-Seitenbibliothek und benutzerdefinierten Layouts verwenden.</span><span class="sxs-lookup"><span data-stu-id="5721c-118">You can also update it to use a custom wiki page library and custom layouts.</span></span> <span data-ttu-id="5721c-119">Die UI-Add-in enthält zwei Schaltflächen, die erstellen sowohl Wiki-Seiten und zwei Links für die Anzeige von Wiki-Seiten, die Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="5721c-119">The add-in UI includes two buttons that create both wiki pages, and two links for viewing the wiki pages you create.</span></span>

<span data-ttu-id="5721c-120">**Abbildung 1. Startseite für das Beispiel für das Zusammenstellen**</span><span class="sxs-lookup"><span data-stu-id="5721c-120">**Figure 1. Start page for the page manipulation sample**</span></span>

![Startseite für das Beispiel für das Zusammenstellen](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/8c6353d9-b339-4563-b945-eaea3d4da2a8.png)

<span data-ttu-id="5721c-122">Der Beispielcode für das erste Szenario bestimmt, ob Sie bereits die Wiki-Seite erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="5721c-122">The sample code for the first scenario determines whether you've already created the wiki page.</span></span> <span data-ttu-id="5721c-123">Wenn dies nicht der Fall, fügt die Datei in der Seitenbibliothek der Website, und gibt den URL zurück.</span><span class="sxs-lookup"><span data-stu-id="5721c-123">If not, it adds the file to the site pages library and returns its URL.</span></span>

<span data-ttu-id="5721c-124">**Hinweis:** Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="5721c-124">**Note:** The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
var newpage = pageLibrary.RootFolder.Files.AddTemplateFile(newWikiPageUrl, TemplateFileType.WikiPage);
ctx.Load(newpage);
ctx.ExecuteQuery();
wikiPageUrl = String.Format("sitepages/{0}", wikiPageName);
```

<span data-ttu-id="5721c-125">In beiden Fällen wird im Beispiel den HTML-Code über das Textfeld auf der Startseite mit der **AddHtmlToWikiPage** -Methode in einer Hilfsklasse, die mit dem Namen **LabHelper**eingegeben werden.</span><span class="sxs-lookup"><span data-stu-id="5721c-125">In both scenarios, the sample adds the HTML entered via the text box on the start page by using the **AddHtmlToWikiPage** method in a helper class named **LabHelper**.</span></span> <span data-ttu-id="5721c-126">Diese Methode fügt den HTML-Code aus dem Formular in das Feld _WikiField_ der Wiki-Seite.</span><span class="sxs-lookup"><span data-stu-id="5721c-126">This method inserts the HTML from the form inside the _WikiField_ field of the wiki page.</span></span>

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

<span data-ttu-id="5721c-127">Der Beispielcode für das zweite Szenario erstellt eine neue Instanz des **WebPartEntity** .</span><span class="sxs-lookup"><span data-stu-id="5721c-127">The sample code for the second scenario creates a new **WebPartEntity** instance.</span></span> <span data-ttu-id="5721c-128">Anschließend wird Methoden in einer Hilfsklasse zum Auffüllen der Webpart mit XML.</span><span class="sxs-lookup"><span data-stu-id="5721c-128">It then uses methods in a helper class to populate the Web Part with XML.</span></span> <span data-ttu-id="5721c-129">Der XML-Code zeigt eine höher gestuften Verknüpfungsliste, einschließlich [http://www.bing.com](http://www.bing.com) und die Homepage des Repositorys [OfficeDev/PnP GitHub](https://github.com/SharePoint/PnP) .</span><span class="sxs-lookup"><span data-stu-id="5721c-129">The XML displays a promoted links list, including both [http://www.bing.com](http://www.bing.com) and the home page of the [OfficeDev/PnP GitHub](https://github.com/SharePoint/PnP) repository.</span></span>

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

<span data-ttu-id="5721c-130">Der Hilfscode zeigt die höher gestuften Verknüpfungen mit einer Tabelle in einem **XsltListViewWebPart** -Webpart.</span><span class="sxs-lookup"><span data-stu-id="5721c-130">The helper code displays the promoted links with a table inside an **XsltListViewWebPart** Web Part.</span></span>

<span data-ttu-id="5721c-131">**Abbildung 2. Zweite Wiki-Seiten mit XsltListViewWebPart und höher gestuften Verknüpfungen-Tabelle**</span><span class="sxs-lookup"><span data-stu-id="5721c-131">**Figure 2. Second wiki page with XsltListViewWebPart and promoted links table**</span></span>

![Zweite Wiki-Seiten mit XsltListViewWeb Teil und höher gestuften Verknüpfungen-Tabelle](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/6dc60a0b-b11a-4fe9-ad06-6b4d0d4b8b24.png)

<span data-ttu-id="5721c-133">Das **WpPromotedLinks** -Objekt auf der **LabHelper** -Instanz enthält XML, das die Darstellung des Webparts definiert, die in der Wiki-Seiten eingebettet werden.</span><span class="sxs-lookup"><span data-stu-id="5721c-133">The **WpPromotedLinks** object on the **LabHelper** instance contains XML that defines the appearance of the Web Part that will be embedded into the wiki page.</span></span> <span data-ttu-id="5721c-134">Die **AddWebPartToWikiPage** -Methode fügt dann das neu definierte-Webpart in einem neuen `div` -Tag auf Wiki-Seiten.</span><span class="sxs-lookup"><span data-stu-id="5721c-134">The **AddWebPartToWikiPage** method then inserts the newly defined Web Part inside a new `div` tag on the wiki page.</span></span>

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

## <a name="showing-add-ins-and-data-in-modal-dialog-boxes"></a><span data-ttu-id="5721c-135">Add-ins und Daten anzeigen in modale Dialogfelder</span><span class="sxs-lookup"><span data-stu-id="5721c-135">Showing add-ins and data in modal dialog boxes</span></span>
<span data-ttu-id="5721c-136"><a name="bmPageManipulate"> </a></span><span class="sxs-lookup"><span data-stu-id="5721c-136"></span></span>

<span data-ttu-id="5721c-137">Im Beispiel [Core.Dialog](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.Dialog) zeigt zwei Methoden für das Einbetten von modales Dialogfeld Feld Links.</span><span class="sxs-lookup"><span data-stu-id="5721c-137">The [Core.Dialog](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.Dialog) sample shows two methods for embedding modal dialog box links.</span></span> <span data-ttu-id="5721c-138">Diese Links anzeigen eine vom Anbieter gehosteten Add-in-Seite in einer SharePoint-Website-Host.</span><span class="sxs-lookup"><span data-stu-id="5721c-138">These links display a provider-hosted add-in page into a SharePoint host site.</span></span> <span data-ttu-id="5721c-139">Das Add-In wird verwendet das Clientobjektmodell (CSOM) zum Erstellen der benutzerdefinierten Aktion und JavaScript starten und Anzeigen von Informationen in das Dialogfeld ein.</span><span class="sxs-lookup"><span data-stu-id="5721c-139">The add-in uses the client object model (CSOM) to create the custom action and JavaScript to start and display information inside the dialog box.</span></span> <span data-ttu-id="5721c-140">Da einige dieser Informationen von der Hostwebsite abgerufen werden, wird auch das JavaScript-Objektmodell (JSOM) zum Abrufen von Informationen aus der Hostwebsite verwendet.</span><span class="sxs-lookup"><span data-stu-id="5721c-140">Because some of this information comes from the host site, it also uses the JavaScript object model (JSOM) to retrieve information from the host site.</span></span> <span data-ttu-id="5721c-141">Und, da das Add-in in einer anderen Domäne als der SharePoint-Website-Host ausgeführt wird, außerdem wird durch die domänenübergreifende SharePoint-Dokumentbibliothek der Hostwebsite anrufen.</span><span class="sxs-lookup"><span data-stu-id="5721c-141">And because the add-in is running in a different domain than the SharePoint host site, it also uses the SharePoint cross-domain library to make the calls to the host site.</span></span>

<span data-ttu-id="5721c-142">**Hinweis:** Weitere Informationen zur Verwendung der domänenübergreifenden Bibliothek in diesem Szenario finden Sie unter [Zugriff auf SharePoint 2013-Daten aus-add-ins mithilfe der domänenübergreifenden Bibliothek](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="5721c-142">**Note:** For more information about using the cross-domain library in this scenario, see [Access SharePoint 2013 data from add-ins using the cross-domain library](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx).</span></span>

<span data-ttu-id="5721c-143">Die Startseite ist die Seite, die im Dialogfeld angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-143">The start page is the page that appears in the dialog box.</span></span> <span data-ttu-id="5721c-144">So behandeln Sie alle Unterschiede zwischen den angegebenen Anzeigekontext (Dialogfeld im Vergleich zu ganzseitigen) anzeigen, bestimmt das Add-in, ob sie in einem Dialogfeld angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-144">To handle any differences in display given the display context (dialog box versus full-page), the add-in determines whether it's being displayed in a dialog box.</span></span> <span data-ttu-id="5721c-145">Dies geschieht mithilfe von einen Abfragezeichenfolgen-Parameter, der zusammen mit den Links übergeben wird, die die Dialogfelder zu starten.</span><span class="sxs-lookup"><span data-stu-id="5721c-145">It does this by using a query string parameter that is passed along with the links that start the dialog boxes.</span></span>

```
private string SetIsDlg(string isDlgValue)
        {
            var urlParams = HttpUtility.ParseQueryString(Request.QueryString.ToString());
            urlParams.Set("IsDlg", isDlgValue);
            return string.Format("{0}://{1}:{2}{3}?{4}", Request.Url.Scheme, Request.Url.Host, Request.Url.Port, Request.Url.AbsolutePath, urlParams.ToString());
        }
```

<span data-ttu-id="5721c-146">Sie könnten beispielsweise auswählen, zum Anzeigen bestimmter Elemente der Benutzeroberfläche (wie Schaltflächen) oder sogar auf verschiedene Seitenlayouts, je nachdem, ob der Inhalt in einem Dialogfeld angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-146">You could, for example, choose to display certain UI elements (like buttons) or even different page layouts, depending on whether or not the content is being displayed in a dialog box.</span></span>

<span data-ttu-id="5721c-147">Die Benutzeroberfläche der Startseite stellt zwei Optionen zum Erstellen von Links, um das Dialogfeld zusammen mit einer Liste aller Listen auf dem hostweb.</span><span class="sxs-lookup"><span data-stu-id="5721c-147">The start page UI presents two options for creating links to the dialog box, along with a list of all the lists on the host web.</span></span> <span data-ttu-id="5721c-148">Es stellt auch **OK** und **Abbrechen** Schaltflächen, dass Sie im Dialogfeld Feld Kontext verwenden können, um das Dialogfeld Feld und/oder Aufforderung weiteren Aktionen in das Add-in zu schließen.</span><span class="sxs-lookup"><span data-stu-id="5721c-148">It also presents **OK** and **Cancel** buttons that you can use in the dialog box context to close the dialog box and/or prompt additional actions in the add-in.</span></span>

<span data-ttu-id="5721c-149">Wenn Sie die **Option hinzufügen** Schaltfläche geklickt haben, erstellt das Add-in ein **CustomActionEntity** -Objekt, das das Dialogfeld beginnt.</span><span class="sxs-lookup"><span data-stu-id="5721c-149">When you choose the **Add menu item** button, the add-in creates a **CustomActionEntity** object that starts the dialog box.</span></span> <span data-ttu-id="5721c-150">Anschließend wird die [Erweiterung OfficeDevPnP Core](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) -Methode mit dem Namen **AddCustomAction** , um die neue benutzerdefinierte Aktion im Menü **Einstellungen der Website** hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="5721c-150">It then uses the [OfficeDevPnP Core extension](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) method named **AddCustomAction** to add the new custom action to the **Site Settings** menu.</span></span>

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

<span data-ttu-id="5721c-151">Die **AddCustomAction** -Methode hinzugefügt der **UserCustomActions** -Auflistung, die die SharePoint-Website zugeordnet ist die benutzerdefinierte Aktion.</span><span class="sxs-lookup"><span data-stu-id="5721c-151">The **AddCustomAction** method adds the custom action to the **UserCustomActions** collection that is associated with the SharePoint site.</span></span>

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

<span data-ttu-id="5721c-152">Wenn Sie die **Seite mit den Skript-Editor-Webpart hinzufügen** Schaltfläche geklickt haben, verwendet die Methoden **AddWikiPage** und **AddWebPartToWikiPage** des Add-Ins zum Erstellen einer Wiki-Seiten innerhalb der Website-Bibliothek für Seiten und Hinzufügen eines konfigurierten Skript-Editor-Webparts auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="5721c-152">When you choose the **Add page with script editor web part** button, the add-in uses the methods **AddWikiPage** and **AddWebPartToWikiPage** to create a wiki page inside the site pages library and add a configured Script Editor Web Part to the page.</span></span>

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

<span data-ttu-id="5721c-153">Die **AddWikiPage** -Methode lädt der Seitenbibliothek der Website.</span><span class="sxs-lookup"><span data-stu-id="5721c-153">The **AddWikiPage** method loads the site pages library.</span></span> <span data-ttu-id="5721c-154">Wenn die Wiki-Seiten durch das Add-in [OfficeDevPnP Core](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) angegebenen nicht bereits vorhanden ist, wird die Seite erstellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-154">If the wiki page specified by the add-in [OfficeDevPnP core](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) doesn't already exist, it creates the page.</span></span>

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

<span data-ttu-id="5721c-155">Die **AddWebPartToWikiPage** -Methode fügt der neu definierten Webparts innerhalb einer neuen `<div>` -Tag auf Wiki-Seiten.</span><span class="sxs-lookup"><span data-stu-id="5721c-155">The **AddWebPartToWikiPage** method inserts the newly defined Web Part inside a new `<div>` tag on the wiki page.</span></span> <span data-ttu-id="5721c-156">Anschließend wird JSOM und der domänenübergreifenden Bibliothek zum Abrufen der Informationen, die die Liste der SharePoint-Listen auf dem hostweb aufgefüllt wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-156">It then uses JSOM and the cross-domain library to retrieve the information that populates the list of SharePoint lists on the host web.</span></span>

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

## <a name="personalized-ui-elements"></a><span data-ttu-id="5721c-157">Personalisierte Benutzeroberflächenelemente</span><span class="sxs-lookup"><span data-stu-id="5721c-157">Personalized UI elements</span></span>
<span data-ttu-id="5721c-158"><a name="bmPersonalized"> </a></span><span class="sxs-lookup"><span data-stu-id="5721c-158"></span></span>

<span data-ttu-id="5721c-159">Das [Branding.UIElementPersonalization](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization) -Beispiel veranschaulicht, wie eingebettete JavaScript und Werte in Benutzerprofilen gespeichert und SharePoint-Listen für Benutzeroberflächenelemente auf dem hostweb zu personalisieren.</span><span class="sxs-lookup"><span data-stu-id="5721c-159">The [Branding.UIElementPersonalization](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization) sample shows how to use embedded JavaScript and values stored in user profiles and SharePoint lists to personalize UI elements on the host web.</span></span> <span data-ttu-id="5721c-160">Auch wird HTML5 lokalen Speicher verwendet, um Anrufe an die Hostwebsite zu minimieren.</span><span class="sxs-lookup"><span data-stu-id="5721c-160">It also uses HTML5 local storage to minimize calls to the host site.</span></span>

<span data-ttu-id="5721c-161">Startseite des Beispiels aufgefordert, eine der drei Zeichenfolgen (XX, JJ oder ZZ) in den Abschnitt **Über mich** von Ihrer Profilseite des Benutzers hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="5721c-161">The sample's start page prompts you to add one of three strings (XX, YY, or ZZ) to the **About Me** section of your user profile page.</span></span>

<span data-ttu-id="5721c-162">Das Add-In wurde bereits bereitgestellt, drei Bilder und einer SharePoint-Liste, die Titel und URLs für jedes Bild, sowie ein weiteres Feld enthält, der eine der drei Zeichenfolgen pro Bild verbindet.</span><span class="sxs-lookup"><span data-stu-id="5721c-162">The add-in has already deployed three images and a SharePoint list that contains titles and URLs for each image, along with an additional field that ties each image to one of the three strings.</span></span> <span data-ttu-id="5721c-163">Nachdem Sie die **Anpassung der Eingabe-** Schaltfläche geklickt haben, bettet die personalize.js-Datei des Add-Ins in der Auflistung benutzerdefinierte Aktionen.</span><span class="sxs-lookup"><span data-stu-id="5721c-163">After you choose the **Inject customization** button, the add-in embeds the personalize.js file into the user custom actions collection.</span></span>

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

<span data-ttu-id="5721c-164">Da SharePoint-Teamwebsites standardmäßig die [Minimale herunterladen Strategie (MDS)](http://msdn.microsoft.com/en-us/library/office/dn456544%28v=office.15%29.aspx)verwenden, versucht der Code in der Datei personalize.js zuerst selbst MDS registrieren.</span><span class="sxs-lookup"><span data-stu-id="5721c-164">Because SharePoint team sites by default use the [Minimal Download Strategy (MDS)](http://msdn.microsoft.com/en-us/library/office/dn456544%28v=office.15%29.aspx), the code in the personalize.js file first attempts to register itself with MDS.</span></span> <span data-ttu-id="5721c-165">Auf diese Weise beim Laden der Seite, die die JavaScript-Code enthält engine der MDS Starets der main-Funktion (**RemoteManager_Inject**).</span><span class="sxs-lookup"><span data-stu-id="5721c-165">This way, when you load the page that contains the JavaScript, the MDS engine starets the main function (**RemoteManager_Inject**).</span></span> <span data-ttu-id="5721c-166">Wenn MDS deaktiviert ist, wird diese Funktion sofort gestartet.</span><span class="sxs-lookup"><span data-stu-id="5721c-166">If MDS is disabled, this function starts right away.</span></span>

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

<span data-ttu-id="5721c-167">Die Funktion **personalizeIt()** überprüft HTML5 lokalen Speicher, bevor Benutzerprofilinformationen gesucht.</span><span class="sxs-lookup"><span data-stu-id="5721c-167">The **personalizeIt()** function checks HTML5 local storage before it looks up user profile information.</span></span> <span data-ttu-id="5721c-168">Wenn es in der Benutzerprofilinformationen geht, werden die Informationen, die abgerufen, im lokalen Speicher HTML5 gespeichert.</span><span class="sxs-lookup"><span data-stu-id="5721c-168">If it goes to user profile information, it stores the information that it retrieves in HTML5 local storage.</span></span>

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

<span data-ttu-id="5721c-169">Die Datei personalize.js enthält auch Code, der überprüft, um festzustellen, ob der lokalen Speicherschlüssel abgelaufen ist.</span><span class="sxs-lookup"><span data-stu-id="5721c-169">The personalize.js file also contains code that checks to determine whether the local storage key has expired.</span></span> <span data-ttu-id="5721c-170">Dies ist nicht in HTML5 lokalen Speicher integriert.</span><span class="sxs-lookup"><span data-stu-id="5721c-170">This isn't built into HTML5 local storage.</span></span>

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

## <a name="client-side-rendering"></a><span data-ttu-id="5721c-171">Clientseitiges Rendering</span><span class="sxs-lookup"><span data-stu-id="5721c-171">Client-side rendering</span></span>
<span data-ttu-id="5721c-172"><a name="bmPersonalized"> </a></span><span class="sxs-lookup"><span data-stu-id="5721c-172"></span></span>

<span data-ttu-id="5721c-173">Das [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering) -Beispiel veranschaulicht, wie ein vom Anbieter gehosteten add-in verwenden, um Remote Bereitstellen von SharePoint-Artefakte und JSLink-Dateien, die clientseitiges Rendering verwenden, um das Aussehen und Verhalten von SharePoint-Listenfelder anpassen.</span><span class="sxs-lookup"><span data-stu-id="5721c-173">The [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering) sample shows how to use a provider-hosted add-in to remotely provision SharePoint artifacts and JSLink files that use client-side rendering to customize the look and behavior of SharePoint list fields.</span></span> <span data-ttu-id="5721c-174">JSLink-Dateien und clientseitiges Rendering können Sie, wie Sie steuern einer SharePoint-Seite Steuerelemente (Listenansichten, Listenfelder, und hinzufügen und Bearbeiten von Formularen) gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="5721c-174">JSLink files and client-side rendering give you control over how controls on a SharePoint page (list views, list fields, and add and edit forms) are rendered.</span></span> <span data-ttu-id="5721c-175">Dieses Steuerelement kann reduzieren oder benutzerdefinierte Feldtypen überflüssig.</span><span class="sxs-lookup"><span data-stu-id="5721c-175">This control can reduce or eliminate the need for custom field types.</span></span> <span data-ttu-id="5721c-176">Clientseitiges Rendering ermöglicht die Liste Feld Darstellung Remote Remote steuern.</span><span class="sxs-lookup"><span data-stu-id="5721c-176">Client-side rendering makes it possible to remotely control list field appearance remotely.</span></span>

<span data-ttu-id="5721c-177">Im Beispiel kombiniert die JSLink Beispiele von der [Client-Side Rendering (JSLink)-Codebeispiele](http://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a) zu einer einzelnen vom Anbieter gehosteten-add-in für SharePoint fest, stellt die JSLink-Dateien.</span><span class="sxs-lookup"><span data-stu-id="5721c-177">The sample combines the JSLink samples from the [Client-side rendering (JSLink) code samples](http://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a) into a single provider-hosted add-in for SharePoint that provisions the JSLink files.</span></span> <span data-ttu-id="5721c-178">Clientseitiges Rendering können Sie standardmäßigen-Technologien, wie HTML und JavaScript, verwenden, um benutzerdefinierte und vordefinierte Feldtypen Renderinglogik definieren.</span><span class="sxs-lookup"><span data-stu-id="5721c-178">Client-side rendering enables you to use standard web technologies, such as HTML and JavaScript, to define the rendering logic of custom and predefined field types.</span></span>

<span data-ttu-id="5721c-179">Wenn Sie das Beispiel starten, fordert die Startseite Sie alle Beispiele bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="5721c-179">When you start the sample, the start page prompts you to provision all the samples.</span></span>

<span data-ttu-id="5721c-180">**Abbildung 3. Startseite des Beispiels clientseitiges rendering**</span><span class="sxs-lookup"><span data-stu-id="5721c-180">**Figure 3. Start page of the client-side rendering sample**</span></span>

![Startseite des Beispiels clientseitiges rendering](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/bfa1b472-976b-4bdc-95df-537cee5570e6.png)

<span data-ttu-id="5721c-182">Bei der Auswahl **Provision Beispiele**wird das Add-in bereitgestellt, ein Bild als auch alle der SharePoint-Listen, Listenansichten, Listenelemente, Formulare und JavaScript-Dateien, die in jedem Beispiel verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="5721c-182">When you choose **Provision Samples**, the add-in deploys an image as well as all the SharePoint lists, list views, list items, forms, and JavaScript files that are used in each sample.</span></span> <span data-ttu-id="5721c-183">Das Add-in erstellt einen Ordner namens JSLink-Beispiele in der Formatbibliothek, und klicken Sie dann die JavaScript-Dateien in diesen Ordner hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="5721c-183">The add-in creates a folder named JSLink-Samples in the Style Library, and then uploads the JavaScript files into that folder.</span></span> <span data-ttu-id="5721c-184">Die **UploadFileToFolder** -Methode führt die Arbeit des Hochladens und jeder JavaScript-Datei einchecken.</span><span class="sxs-lookup"><span data-stu-id="5721c-184">The **UploadFileToFolder** method does the work of uploading and checking in each JavaScript file.</span></span>

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

### <a name="sample-1-apply-formatting-to-a-list-column"></a><span data-ttu-id="5721c-185">Beispiel 1: Formatieren einer Listenspalte</span><span class="sxs-lookup"><span data-stu-id="5721c-185">Sample 1: Apply formatting to a list column</span></span>

<span data-ttu-id="5721c-186">Beispiel 1 zeigt, wie um einer Listenspalte basierend auf den Wert des Felds zu formatieren.</span><span class="sxs-lookup"><span data-stu-id="5721c-186">Sample 1 shows how to apply formatting to a list column based on the field value.</span></span> <span data-ttu-id="5721c-187">Priorität Feldwerte von 1 (hoch), 2 (Normal) und 3 (niedrig) werden in Rot, Gelb und Orange angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5721c-187">Priority field values of 1 (High), 2 (Normal), and 3 (Low) are displayed in red, orange, and yellow.</span></span>

<span data-ttu-id="5721c-188">**Abbildung 4. Benutzerdefinierte Liste Feldanzeige**</span><span class="sxs-lookup"><span data-stu-id="5721c-188">**Figure 4. Custom list field display**</span></span>

![Benutzerdefinierte Liste Feldanzeige](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/1481adfa-efc9-4b59-b07f-bb330f02d2bb.png)

<span data-ttu-id="5721c-190">Das folgende JavaScript überschreibt die Standardanzeige dar und erstellt eine neue Anzeigevorlage für das Feld der Liste **Priorität** .</span><span class="sxs-lookup"><span data-stu-id="5721c-190">The following JavaScript overrides the default field display and creates a new display template for the **Priority** list field.</span></span> <span data-ttu-id="5721c-191">Das Verfahren in die anonyme Funktion, die die Kontextinformationen über das Feld lädt, deren Anzeige Sie außer Kraft setzen möchten, die in alle Beispiele verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-191">The technique in the anonymous function that loads the contextual information about the field whose display you want to override is used in all the samples.</span></span>

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

### <a name="sample-2-shorten-long-text"></a><span data-ttu-id="5721c-192">Beispiel 2: Kürzen Sie langen text</span><span class="sxs-lookup"><span data-stu-id="5721c-192">Sample 2: Shorten long text</span></span>

<span data-ttu-id="5721c-193">Beispiel 2 zeigt, wie zu kürzende langen Text im Feld **Text** , der einer Liste mit **Ankündigungen** gespeichert.</span><span class="sxs-lookup"><span data-stu-id="5721c-193">Sample 2 shows you how to truncate long text stored in the **Body** field of an **Announcements** list.</span></span> <span data-ttu-id="5721c-194">Der vollständige Text zeigt als ein Popup-Fenster, das angezeigt wird, wenn Sie über ein Listenelement bewegen, wie in Abbildung 8 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-194">The full text displays as a popup that appears whenever you hover over a list item, as shown in Figure 8.</span></span>

<span data-ttu-id="5721c-195">**Abbildung 5. Verkürzte Liste Feld Anzeige mit popup**</span><span class="sxs-lookup"><span data-stu-id="5721c-195">**Figure 5. Shortened list field display showing popup**</span></span>

![Abgeschnittene Liste Feld Anzeige mit popup](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/a5e6d2af-f1f9-4bcc-9278-e56fd42c2e64.png)

<span data-ttu-id="5721c-197">Das folgende JavaScript verkürzt **den Textkörper dar** und festgelegt, dass den vollständigen Text als ein Popup über das **Title** -Attribut für das **span** -Tag angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="5721c-197">The following JavaScript shortens the **Body** field text and causes the full text to appear as a popup via the **title** attribute on the **span** tag.</span></span>

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

### <a name="sample-3-display-an-image-with-a-document-name"></a><span data-ttu-id="5721c-198">Beispiel 3: Ein Bild mit einem Dokumentnamen anzeigen</span><span class="sxs-lookup"><span data-stu-id="5721c-198">Sample 3: Display an image with a document name</span></span>

<span data-ttu-id="5721c-199">Beispiel 3 zeigt, wie ein Bild neben dem Dokumentnamen eines in einer Dokumentbibliothek angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5721c-199">Sample 3 shows you how to display an image next to a document name inside a document library.</span></span> <span data-ttu-id="5721c-200">Eine rote Logo wird angezeigt, wenn der Wert des Felds **vertraulich** auf **Ja**festgelegt ist, wie in Abbildung 6 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-200">A red badge appears whenever the **Confidential** field value is set to **Yes**, as shown in Figure 6.</span></span> 

<span data-ttu-id="5721c-201">**Abbildung 6. Anzeige von Bildern neben den Namen des Dokuments**</span><span class="sxs-lookup"><span data-stu-id="5721c-201">**Figure 6. Image display next to document name**</span></span>

![Anzeige von Bildern neben den Namen des Dokuments](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/f2768dfd-ae05-4afc-8dbe-26dc4e7dca6d.png)

<span data-ttu-id="5721c-203">Das folgende JavaScript überprüft den Wert des Felds **vertraulich** und passt anschließend die **Namen** Feldanzeige basierend auf dem Wert eines anderen Felds.</span><span class="sxs-lookup"><span data-stu-id="5721c-203">The following JavaScript checks the **Confidential** field value and then customizes the **Name** field display based on the value of another field.</span></span> <span data-ttu-id="5721c-204">Das Beispiel verwendet das Bild, das hochgeladen wird, wenn Sie eine **Bereitstellung Beispiele**auswählen.</span><span class="sxs-lookup"><span data-stu-id="5721c-204">The sample uses the image that is uploaded when you choose **Provision Samples**.</span></span> 

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

### <a name="sample-4-display-a-bar-chart"></a><span data-ttu-id="5721c-205">Beispiel 4: Ein Balkendiagramm angezeigt</span><span class="sxs-lookup"><span data-stu-id="5721c-205">Sample 4: Display a bar chart</span></span>

<span data-ttu-id="5721c-206">Beispiel 4 zeigt, wie ein Balkendiagramm in das Feld **% abgeschlossen** einer Aufgabenliste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5721c-206">Sample 4 shows you how to display a bar chart in the **% Complete** field of a task list.</span></span> <span data-ttu-id="5721c-207">Die Darstellung des Balkendiagramm verwendet wird, hängt vom Wert im Feld **% abgeschlossen** , wie in Abbildung 10 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-207">The appearance of the bar chart depends on the value of the **% Complete** field, as shown in Figure 10.</span></span> <span data-ttu-id="5721c-208">Beachten Sie, dass ein Balkendiagramm auch in den Formularen für das Erstellen und Bearbeiten von Listenelementen Aufgabe angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-208">Note that a bar chart will also appear in the forms for creating and editing task list items.</span></span>

<span data-ttu-id="5721c-209">Mit dem folgende Code wird die Anzeige Balkendiagramm erstellt und ordnet sie mit den Formularen anzeigen und -Anzeige (**PercentCompleteViewFiledTemplate**), und klicken Sie dann mit der neuen und Bearbeitungsformulare (**PercentCompleteEditFiledTemplate**).</span><span class="sxs-lookup"><span data-stu-id="5721c-209">The following code creates the bar chart display and associates it with the view and display forms (**percentCompleteViewFiledTemplate**) and then with the new and edit forms (**percentCompleteEditFiledTemplate**).</span></span>

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

<span data-ttu-id="5721c-210">**Abbildung 7. Balkendiagramm angezeigt, in das Feld % abgeschlossen**</span><span class="sxs-lookup"><span data-stu-id="5721c-210">**Figure 7. Bar chart displayed in the % Complete field**</span></span>

![Balkendiagramm angezeigt, in das Feld % abgeschlossen](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/fb36f27a-2eb7-4c5f-8428-b85b65369ea9.png)

### <a name="sample-5-change-the-rendering-template"></a><span data-ttu-id="5721c-212">Beispiel 5: Ändern der Renderingvorlage</span><span class="sxs-lookup"><span data-stu-id="5721c-212">Sample 5: Change the rendering template</span></span>

<span data-ttu-id="5721c-213">Beispiel 5 zeigt, wie die Renderingvorlage für eine Listenansicht zu ändern.</span><span class="sxs-lookup"><span data-stu-id="5721c-213">Sample 5 shows you how to change the rendering template for a list view.</span></span> <span data-ttu-id="5721c-214">Diese Ansicht zeigt Element Listentitel, die wie Akkordeons erweitern, wenn Sie diese auswählen.</span><span class="sxs-lookup"><span data-stu-id="5721c-214">This view displays list item titles that expand like accordions when you select them.</span></span> <span data-ttu-id="5721c-215">Die erweiterte Ansicht zeigt, zusätzliche Felder für Listenelemente, wie in Abbildung 8 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-215">The expanded view shows you additional list item fields, as shown in Figure 8.</span></span>

<span data-ttu-id="5721c-216">**Abbildung 8. Reduzierte und erweiterte Element Listenansichten**</span><span class="sxs-lookup"><span data-stu-id="5721c-216">**Figure 8. Collapsed and expanded list item views**</span></span>

![Reduzierte und erweiterte Element Listenansichten](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/fd185eef-e2be-4523-9adb-d524b84ecc26.png)

<span data-ttu-id="5721c-218">Der folgende Code richtet die Vorlage und registriert dieses in die Vorlage Liste aus.</span><span class="sxs-lookup"><span data-stu-id="5721c-218">The following code sets up the template and registers it with the list template.</span></span> <span data-ttu-id="5721c-219">Es richtet das allgemeine Layout, und klicken Sie dann den **OnPostRender** -Ereignishandler verwendet, um die JavaScript-Funktion zu registrieren, die ausgeführt wird, wenn die Liste dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-219">It sets up the overall layout, and then uses the **OnPostRender** event handler to register the JavaScript function that executes when the list is rendered.</span></span> <span data-ttu-id="5721c-220">Diese Funktion das Ereignis den CSS-Code zugeordnet und Ereignisbehandlung, die die Akkordeon Funktionalität implementiert.</span><span class="sxs-lookup"><span data-stu-id="5721c-220">This function associates the event with the CSS and event handling that implements the accordion functionality.</span></span>

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

### <a name="sample-6-validate-field-values"></a><span data-ttu-id="5721c-221">Beispiel 6: Überprüfen der Feldwerte</span><span class="sxs-lookup"><span data-stu-id="5721c-221">Sample 6: Validate field values</span></span>

<span data-ttu-id="5721c-222">Beispiel 6 zeigt, wie Sie reguläre Ausdrücke verwenden, um vom Benutzer eingegebenen Feldwerte überprüfen.</span><span class="sxs-lookup"><span data-stu-id="5721c-222">Sample 6 shows you how to use regular expressions to validate field values supplied by the user.</span></span> <span data-ttu-id="5721c-223">Eine rote Fehlermeldung wird angezeigt, wenn der Benutzer eine ungültige e-Mail-Adresse in das Textfeld **E-Mail** eingibt.</span><span class="sxs-lookup"><span data-stu-id="5721c-223">A red error message appears when the user types an invalid email address into the **Email** field text box.</span></span> <span data-ttu-id="5721c-224">Dies geschieht, wenn der Benutzer erstellt oder ein Listenelement bearbeitet, wie in Abbildung 9 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-224">This happens when the user either creates or edits a list item, as shown in Figure 9.</span></span>

<span data-ttu-id="5721c-225">**Abbildung 9. Fehlermeldung ungültigem Texteingabe**</span><span class="sxs-lookup"><span data-stu-id="5721c-225">**Figure 9. Error message for invalid field text input**</span></span>

![Fehlermeldung ungültigem Texteingabe](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/d0d1faf1-aa03-4df8-a1a6-db86fff1f463.png)

<span data-ttu-id="5721c-227">Der folgende Code richtet die Vorlage mit einem Platzhalter für die Anzeige der Fehlermeldung und registriert Callback-Funktionen, die ausgelöst werden, wenn der Benutzer versucht, die Formulare übermitteln.</span><span class="sxs-lookup"><span data-stu-id="5721c-227">The following code sets up the template with a placeholder for displaying the error message and registers the callback functions that fire whenever the user tries to submit the forms.</span></span> <span data-ttu-id="5721c-228">Der erste Rückruf zurückgegeben wird des Werts der **E-Mail** -Spalte und der zweite Rückruf verwendet reguläre Ausdrücke, um den Zeichenfolgenwert zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="5721c-228">The first callback returns the value of the **Email** column, and the second callback uses regular expressions to validate the string value.</span></span>

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

### <a name="sample-7-make-list-item-edit-fields-read-only"></a><span data-ttu-id="5721c-229">Beispiel 7: Stellen Sie Listenelement schreibgeschützte Felder bearbeiten</span><span class="sxs-lookup"><span data-stu-id="5721c-229">Sample 7: Make list item edit fields read-only</span></span>

<span data-ttu-id="5721c-230">Beispiel sieben zeigt, wie Sie Felder für Listenelemente bearbeiten Formular nur-Lese-Liste.</span><span class="sxs-lookup"><span data-stu-id="5721c-230">Sample seven shows you how to make list item edit form fields read-only.</span></span> <span data-ttu-id="5721c-231">Der schreibgeschützte Felder anzeigen mit keine Bearbeitungssteuerelemente, wie in Abbildung 10 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-231">The read-only fields show with no editing controls, as shown in Figure 10.</span></span>

<span data-ttu-id="5721c-232">**Abbildung 10. Schreibgeschütztes Feld auf eine benutzerdefinierte Liste Bearbeitungsformular**</span><span class="sxs-lookup"><span data-stu-id="5721c-232">**Figure 10. Read-only field on a custom list edit form**</span></span>

![Schreibgeschützte Felder in einer benutzerdefinierten Liste Bearbeitungsformular](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/de441289-8276-4e7c-8530-d08192e29000.png)

<span data-ttu-id="5721c-234">Das folgende Codebeispiel ändert den **Titel**, **AssignedTo**und Felder des Listenelements **Priorität** Bearbeitungsformular so, dass sie die Feldwerte nur mit keine Bearbeitungssteuerelemente anzeigen.</span><span class="sxs-lookup"><span data-stu-id="5721c-234">The following code example modifies the **Title**, **AssignedTo**, and **Priority** fields in the list item edit form so that they show the field values only with no editing controls.</span></span> <span data-ttu-id="5721c-235">Der Code zeigt, wie die Abfrageanalyse Anforderungen für die verschiedenen Feldtypen behandeln.</span><span class="sxs-lookup"><span data-stu-id="5721c-235">The code shows how to handle the parsing requirements for different field types.</span></span>

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

### <a name="sample-8-hide-fields"></a><span data-ttu-id="5721c-236">Beispiel 8: Ausblenden Felder</span><span class="sxs-lookup"><span data-stu-id="5721c-236">Sample 8: Hide fields</span></span>

<span data-ttu-id="5721c-237">Beispiel 8 zeigt, wie Felder in neuen Listenelement ausblenden und Formulare bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="5721c-237">Sample 8 shows you how to hide fields in list item new and edit forms.</span></span> <span data-ttu-id="5721c-238">Im Beispiel blendet das Feld **Vorgänger** , wenn ein Benutzer erstellt oder ein Aufgabenelement Liste bearbeitet.</span><span class="sxs-lookup"><span data-stu-id="5721c-238">The sample hides the **Predecessors** field when a user creates or edits a task list item.</span></span>

<span data-ttu-id="5721c-239">In diesem Beispiel wird als bearbeiten und neue Formular für eine Liste namens **Liste CSR-ausblenden-Steuerelemente**bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-239">This sample deploys as the edit and new form for a list called **CSR-Hide-Controls list**.</span></span> <span data-ttu-id="5721c-240">Informationen dazu, wie Sie die Ansicht des Formulars nach der Bereitstellung des Beispiels finden Sie unter [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering).</span><span class="sxs-lookup"><span data-stu-id="5721c-240">For information about how to view the form after you deploy the sample, see [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering).</span></span>

<span data-ttu-id="5721c-241">Der folgende Code sucht das Feld **Vorgänger** in der HTML-Code des Formulars und ausgeblendet werden.</span><span class="sxs-lookup"><span data-stu-id="5721c-241">The following code finds the **Predecessors** field in the HTML of the form and hides it.</span></span> <span data-ttu-id="5721c-242">Das Feld bleibt in der HTML-Code vorhanden, aber der Benutzer nicht im Browser angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5721c-242">The field remains present in the HTML, but the user can't see it in the browser.</span></span>

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

## <a name="web-part-and-add-in-part-manipulation"></a><span data-ttu-id="5721c-243">Add-in-Teil zusammenstellen und Webparts</span><span class="sxs-lookup"><span data-stu-id="5721c-243">Web part and add-in part manipulation</span></span>
<span data-ttu-id="5721c-244"><a name="bmPersonalized"> </a></span><span class="sxs-lookup"><span data-stu-id="5721c-244"></span></span>

<span data-ttu-id="5721c-245">Das [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) -Beispiel veranschaulicht, wie Add-in-Skript-Komponenten nutzen, Skripts, die in einer vom Anbieter gehosteten-add-in ausgeführt wird, auf einer SharePoint-Seite einbetten.</span><span class="sxs-lookup"><span data-stu-id="5721c-245">The [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) sample shows how to use add-in script parts to embed scripts running in a provider-hosted add-in on a SharePoint page.</span></span> <span data-ttu-id="5721c-246">Dieses Beispiel zeigt, wie die Benutzeroberfläche einer Seite auf der Hostwebsite zu ändern, indem Sie ein Webpart-Add-in-Skript bereitstellen und es einer SharePoint-Seite aus dem Webpartkatalog hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="5721c-246">This sample shows how to modify the UI of a page on the host site by deploying an add-in script part and adding it to a SharePoint page from the webpart gallery.</span></span>

<span data-ttu-id="5721c-247">Ein Webpart-Add-in-Skript ist wie ein Webpart, können Sie es zu einer SharePoint-Seite aus dem Webpartkatalog hinzufügen, aber die Webpart-Datei eingebettet in diesem Fall eine JavaScript-Datei, die in einer vom Anbieter gehosteten-Add-in Remote ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-247">An add-in script part is like a web part in that you can add it to a SharePoint page from the web part gallery, but in this case the .webpart file embeds a JavaScript file that runs remotely in a provider-hosted add-in.</span></span> <span data-ttu-id="5721c-248">Das Webpart-Add-in-Skript ausgeführt wird, innerhalb einer `<div>` -Tag auf der SharePoint-Seite und bietet eine verbesserte Reaktionsgeschwindigkeit Design- und Erfahrung als Sie abrufen mit Add-in-Webparts, die in IFrames ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="5721c-248">The add-in script part runs inside a  `<div>` tag on the SharePoint page and therefore provides a more responsive design and experience than you get with add-in parts that run in IFrames.</span></span>

<span data-ttu-id="5721c-249">Die Startseite enthält eine **Szenario ausführen** -Schaltfläche, die das Webpart-Add-in-Skript in den Webpartkatalog bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-249">The start page includes a **Run Scenario** button that deploys the add-in script part to the web part gallery.</span></span> <span data-ttu-id="5721c-250">Das folgende Codebeispiel erstellt eine **FileCreationInformationObject** -Instanz, die den Inhalt der Webpart-Datei enthält, und dann wird die neue Datei in den Webpartkatalog hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="5721c-250">The following code example constructs a **FileCreationInformationObject** instance that contains the contents of the .webpart file and then uploads the new file into the web part gallery.</span></span> <span data-ttu-id="5721c-251">Beachten Sie, dass Sie auch diesen Code automatisch ausgeführt werden können, wenn das Webpart-Add-in installiert oder als Teil der Websitesammlung Bereitstellungsprozesses.</span><span class="sxs-lookup"><span data-stu-id="5721c-251">Note that you can also run this code automatically when the add-in part installs or as part of the site collection provisioning process.</span></span>

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

<span data-ttu-id="5721c-252">Nachdem Sie diesen Schritt abgeschlossen haben, können Sie in den Webpartkatalog das **Benutzerprofilinformationen** Add-in-Skript in eine neue **Add-in-Skript Teil** Kategorie Teil suchen.</span><span class="sxs-lookup"><span data-stu-id="5721c-252">After you finish this step, you can locate the **User profile information** add-in script part inside a new **Add-in Script Part** category in the web part gallery.</span></span> <span data-ttu-id="5721c-253">Nachdem Sie das Webpart-Add-in-Skript auf der Seite hinzufügen, steuert das Remote ausgeführte JavaScript die Anzeige von Informationen auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="5721c-253">After you add the add-in script part to the page, the remotely running JavaScript controls the display of the information on the page.</span></span>

<span data-ttu-id="5721c-254">Wenn Sie das Add-in-Skript-Webpart im Bearbeitungsmodus anzeigen, sehen Sie sich, dass sie die JavaScript-Datei eingebettet, die Remote ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="5721c-254">When you view the add-in script part in edit mode, you'll see that it embeds the JavaScript file that is running remotely.</span></span> <span data-ttu-id="5721c-255">Das userprofileinformation.js-Skript verwendet die JSON Benutzerprofilinformationen aus der Hostwebsite abrufen.</span><span class="sxs-lookup"><span data-stu-id="5721c-255">The userprofileinformation.js script uses the JSON to get user profile information from the host site.</span></span> 

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

## <a name="provisioning-publishing-features"></a><span data-ttu-id="5721c-256">Bereitstellen von Veröffentlichungsfeatures</span><span class="sxs-lookup"><span data-stu-id="5721c-256">Provisioning publishing features</span></span>
<span data-ttu-id="5721c-257"><a name="bmPersonalized"> </a></span><span class="sxs-lookup"><span data-stu-id="5721c-257"></span></span>

<span data-ttu-id="5721c-258">Das [Provisioning.PublishingFeatures](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.PublishingFeatures) -Beispiel zeigt, wie für allgemeine Aufgaben mit der Veröffentlichung von Websites, die in Office 365 gehostet werden. Bereitstellung und mithilfe von Seitenlayouts, Masterseiten und Designs oder Einbetten von JavaScript in Seitenlayouts.</span><span class="sxs-lookup"><span data-stu-id="5721c-258">The [Provisioning.PublishingFeatures](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.PublishingFeatures) sample shows how to do common tasks with publishing sites that are hosted on Office 365; for example, provisioning and using page layouts, master pages, and themes, or embedding JavaScript in page layouts.</span></span> <span data-ttu-id="5721c-259">Außerdem gezeigt, wie Filter anwenden, die steuern, welche Websitevorlagen für Unterwebsites verfügbar sind und welche Seitenlayouts sind auf dem hostweb verfügbar.</span><span class="sxs-lookup"><span data-stu-id="5721c-259">It also shows how to apply filters that control what site templates are available for subsites and what page layouts are available on the host web.</span></span>

<span data-ttu-id="5721c-260">Das Add-in vom Anbieter gehosteten CSOM Benutzeroberflächenelemente auf Veröffentlichungswebsites Bereitstellung häufig verwendet werden und verwendet JavaScript, dynamischere Erfahrungen in Seitenlayouts zu erstellen, die Sie für die Veröffentlichung von Websites bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="5721c-260">The provider-hosted add-in uses CSOM to provision commonly used UI elements on publishing sites, and it uses JavaScript to create more dynamic experiences in page layouts that you can deploy to publishing sites.</span></span> <span data-ttu-id="5721c-261">Es werden auch die Unterschiede zwischen der Verwendung von Masterseiten und Designs in Veröffentlichungswebsites.</span><span class="sxs-lookup"><span data-stu-id="5721c-261">It also shows the differences between using master pages and themes in publishing sites.</span></span>

<span data-ttu-id="5721c-262">**Wichtig:**  Wenn die Funktionalität in diese Beispiel arbeiten möchten, müssen Sie die Veröffentlichungsfeatures auf Ihrer Website zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="5721c-262">**Important:**  To make the functionality in this sample work, you need to activate the publishing features on your site.</span></span> <span data-ttu-id="5721c-263">Informationen finden Sie unter [Aktivieren von Veröffentlichungsfeatures](https://support.office.com/en-us/article/Enable-publishing-features-479677a6-8b33-4ac7-907d-071c1c7e4518?CorrelationId=22291615-2acd-46be-8813-9e6c48d01a32&amp;ui=en-US&amp;rs=en-US&amp;ad=US).</span><span class="sxs-lookup"><span data-stu-id="5721c-263">For information, see [Enable publishing features](https://support.office.com/en-us/article/Enable-publishing-features-479677a6-8b33-4ac7-907d-071c1c7e4518?CorrelationId=22291615-2acd-46be-8813-9e6c48d01a32&amp;ui=en-US&amp;rs=en-US&amp;ad=US).</span></span>

<span data-ttu-id="5721c-264">Die Start-Beispielseite bietet Ihnen drei Szenarien für die Anpassung der Benutzeroberfläche der Veröffentlichungswebsites:</span><span class="sxs-lookup"><span data-stu-id="5721c-264">The sample start page presents you with three scenarios for customizing the UI of publishing sites:</span></span> 

- <span data-ttu-id="5721c-265">Bereitstellen von Seitenlayouts.</span><span class="sxs-lookup"><span data-stu-id="5721c-265">Deploy page layouts.</span></span>
    
- <span data-ttu-id="5721c-266">Bereitstellen von Masterseiten und Designs.</span><span class="sxs-lookup"><span data-stu-id="5721c-266">Deploy master pages and themes.</span></span>
    
- <span data-ttu-id="5721c-267">Die verfügbaren Seitenlayouts und Websitevorlagen auf der Hostwebsite zu filtern.</span><span class="sxs-lookup"><span data-stu-id="5721c-267">Filter the available page layouts and site templates on the host site.</span></span>

### <a name="scenario-1-deploy-pages"></a><span data-ttu-id="5721c-268">Szenario 1: Bereitstellen von Seiten</span><span class="sxs-lookup"><span data-stu-id="5721c-268">Scenario 1: Deploy pages</span></span>

<span data-ttu-id="5721c-269">Szenario 1 zeigt, wie ein benutzerdefiniertes Seitenlayout bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="5721c-269">Scenario 1 shows you how to deploy a custom page layout.</span></span> <span data-ttu-id="5721c-270">Die in Abbildung 11 dargestellte **Deploy Seitenlayouts** Schaltfläche erstellt ein neues Seitenlayout und die Seite, die das Layout verwendet.</span><span class="sxs-lookup"><span data-stu-id="5721c-270">The **Deploy page layouts** button shown in Figure 11 creates a new page layout and a page that uses that layout.</span></span>

<span data-ttu-id="5721c-271">**Abbildung 11. Schaltfläche zum Bereitstellen von Seitenlayouts**</span><span class="sxs-lookup"><span data-stu-id="5721c-271">**Figure 11. Button to deploy page layouts**</span></span>

![Schaltfläche, die Seitenlayouts bereitgestellt wird.](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/141b3b83-9a74-4528-825a-efd94183526d.png)

<span data-ttu-id="5721c-273">Sie können die neue Seite durch Aufrufen der neu erstellten Demoseite auf Ihrer Hostwebsite, die enthält eingebetteten JavaScript und zeigt die Benutzerprofilinformationen anzeigen.</span><span class="sxs-lookup"><span data-stu-id="5721c-273">You can view the new page by going to the newly created demo page on your host site, which contains embedded JavaScript and displays user profile information.</span></span>

<span data-ttu-id="5721c-274">Das Beispiel zeigt Informationen des Benutzers auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="5721c-274">The sample displays this user's information on the page.</span></span> <span data-ttu-id="5721c-275">Außerdem wird eine Seite hinzugefügt, in diesem Fall es ein **PublishingPageInformation** -Objekt verwendet, um die neue Seite erstellen.</span><span class="sxs-lookup"><span data-stu-id="5721c-275">It also adds a page, although in this case it uses a **PublishingPageInformation** object to create the new page.</span></span>

<span data-ttu-id="5721c-276">Im Beispiel wird ein neues Seitenlayout durch Hochladen einer Datei auf den Gestaltungsvorlagenkatalog und Zuweisen des Seite Layout Inhaltstyps hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="5721c-276">The sample adds a new page layout by uploading a file to the master page gallery and assigning it the page layout content type.</span></span> <span data-ttu-id="5721c-277">Der folgende Code akzeptiert den Pfad zu einer ASPX-Datei (die Sie in Ihrem Visual Studio 2013-Projekt als Ressource bereitstellen können) und fügt es als ein Seitenlayout im Gestaltungsvorlagenkatalog hinzu.</span><span class="sxs-lookup"><span data-stu-id="5721c-277">The following code takes the path to a *.aspx file (which you can deploy as a resource in your Visual Studio 2013 project) and adds it as a page layout in the master page gallery.</span></span>

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

<span data-ttu-id="5721c-278">Sie können überprüfen, ob die neue Seite auf das neue Seitenlayout verwendet wird, durch das Aufrufen der Bibliothek für **Seiten** der Hostwebsite.</span><span class="sxs-lookup"><span data-stu-id="5721c-278">You can verify that your new page is using the new page layout by going to the **Pages** library of the host site.</span></span>

### <a name="scenario-2-deploy-master-pages-and-themes"></a><span data-ttu-id="5721c-279">Szenario 2: Bereitstellen von Masterseiten und Designs</span><span class="sxs-lookup"><span data-stu-id="5721c-279">Scenario 2: Deploy master pages and themes</span></span>

<span data-ttu-id="5721c-280">Szenario 2 zeigt, wie zum Bereitstellen und Festlegen von Masterseiten und Designs für die Hostwebsite aus einer vom Anbieter gehosteten-add-in.</span><span class="sxs-lookup"><span data-stu-id="5721c-280">Scenario 2 shows you how to deploy and set master pages and themes for the host site from a provider-hosted add-in.</span></span> <span data-ttu-id="5721c-281">Wenn Sie **Deploy master herunter, und** klicken Sie auf der Startseite Beispiel auswählen, wird im Beispiel bereitgestellt und wendet eine benutzerdefinierte Gestaltungsvorlage auf der Hostwebsite.</span><span class="sxs-lookup"><span data-stu-id="5721c-281">When you choose **Deploy master and use it** on the sample start page, the sample deploys and applies a custom master page to the host site.</span></span> <span data-ttu-id="5721c-282">Sie können neue Gestaltungsvorlage sehen, indem Sie auf der Homepage der Website.</span><span class="sxs-lookup"><span data-stu-id="5721c-282">You can see the new master page by going to the home page of the site.</span></span>

<span data-ttu-id="5721c-283">Im Beispiel wird eine neue Gestaltungsvorlage durch Hochladen einer Master-Datei in den Gestaltungsvorlagenkatalog und Zuweisen des Gestaltungsvorlage Inhaltstyps hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="5721c-283">The sample adds a new master page by uploading a *.master file to the master page gallery and assigning it the master page content type.</span></span> <span data-ttu-id="5721c-284">Der folgende Code akzeptiert den Pfad zu einem Master-Datei (die Sie in Ihrem Visual Studio 2013-Projekt als Ressource bereitstellen können) und fügt es als eine Gestaltungsvorlage im Gestaltungsvorlagenkatalog hinzu.</span><span class="sxs-lookup"><span data-stu-id="5721c-284">The following code takes the path to a *.master file (which you can deploy as a resource in your Visual Studio 2013 project) and adds it as a master page in the master page gallery.</span></span>

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

<span data-ttu-id="5721c-285">Im nächste Schritt wird die URL der neuen Gestaltungsvorlage als Wert für die **MasterUrl** und die **CustomMasterUrl** Eigenschaften des **Web** -Objekts festgelegt, das die Website darstellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-285">The next step is to set the URL of the new master page as the value for both the **MasterUrl** and **CustomMasterUrl** properties of the **Web** object that represents the site.</span></span> <span data-ttu-id="5721c-286">Im Beispiel behandelt dies mit einer einzelnen Methode, die die URL der neuen Gestaltungsvorlage im Gestaltungsvorlagenkatalog abruft und klicken Sie dann auf die Eigenschaften **Web.MasterUrl** und **Web.CustomMasterUrl** weist diesen Wert.</span><span class="sxs-lookup"><span data-stu-id="5721c-286">The sample handles this with a single method that fetches the URL of the new master page in the master page gallery and then assigns that value to the **Web.MasterUrl** and **Web.CustomMasterUrl** properties.</span></span>

```
// Assign master page to the host web.
                clientContext.Web.SetMasterPagesForSiteByName("contoso.master", "contoso.master");

```

<span data-ttu-id="5721c-287">Bei der Auswahl **Design bereitstellen und verwenden sie**das Beispiel bereitgestellt und ein benutzerdefiniertes Design auf der Hostwebsite angewendet.</span><span class="sxs-lookup"><span data-stu-id="5721c-287">When you choose **Deploy theme and use it**, the sample deploys and applies a custom theme to the host site.</span></span> <span data-ttu-id="5721c-288">Im Beispiel wird die Farbpalette, Hintergrundbild und Schriftartenschema des Designs durch Hinzufügen eines neuen Designs mit diesen Werten (die Sie als Ressourcen innerhalb des Visual Studio 2013-Projekts bereitstellen) in den Designkatalog.</span><span class="sxs-lookup"><span data-stu-id="5721c-288">The sample sets the color palette, background image, and font scheme of the theme by adding a new theme with those values (which you can deploy as resources inside your Visual Studio 2013 project) to the theme gallery.</span></span> <span data-ttu-id="5721c-289">Mit dem folgende Code wird das neue Design erstellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-289">The following code creates the new theme.</span></span>

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

<span data-ttu-id="5721c-290">Im nächste Schritt wird das dieses neue Design als das Design für die Website festgelegt.</span><span class="sxs-lookup"><span data-stu-id="5721c-290">The next step is to set this new theme as the theme for the site.</span></span> <span data-ttu-id="5721c-291">Mit dem folgende Code wird das Abrufen des Designs aus der Design Gallery und die Werte auf der Hostwebsite anwenden.</span><span class="sxs-lookup"><span data-stu-id="5721c-291">The following code does this by fetching the theme from the theme gallery and then applying its values to the host site.</span></span>

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

### <a name="scenario-3-filter-available-page-layouts-and-site-templates"></a><span data-ttu-id="5721c-292">Szenario 3: Filtern Sie verfügbaren Seitenlayouts und Websitevorlagen</span><span class="sxs-lookup"><span data-stu-id="5721c-292">Scenario 3: Filter available page layouts and site templates</span></span>

<span data-ttu-id="5721c-293">Szenario 3 zeigt, wie die Optionen zu begrenzen, die Benutzer haben, wenn sie Vorlagen für neue Websites und Layouts, um neue Seiten gelten.</span><span class="sxs-lookup"><span data-stu-id="5721c-293">Scenario 3 shows you how to limit the options that users have when they apply templates to new sites, and layouts to new pages.</span></span> <span data-ttu-id="5721c-294">Wenn Sie auf **Apply Filter mit Hostwebsite** wählen im Beispiel Startseite, im Beispiel wird ein benutzerdefiniertes Seitenlayout als Standard und eine zusätzliche Seitenlayout als einzige andere Option für neuen Seiten, die ein Benutzer erstellt.</span><span class="sxs-lookup"><span data-stu-id="5721c-294">When you choose **Apply filters to host web** on the sample start page, the sample sets a custom page layout as the default and one additional page layout as the only other option for any new pages that a user creates.</span></span> <span data-ttu-id="5721c-295">Im Beispiel reduziert auch die Anzahl der verfügbaren Optionen für Benutzer beim Erstellen von neuen Unterwebsites.</span><span class="sxs-lookup"><span data-stu-id="5721c-295">The sample also reduces the number of available options for users when they create new subsites.</span></span> <span data-ttu-id="5721c-296">Abbildung 12 zeigt, wie das Auswahlfeld Vorlage Website aussieht, bevor und nachdem die Filter angewendet wurden.</span><span class="sxs-lookup"><span data-stu-id="5721c-296">Figure 12 shows what the site template selection box looks like both before and after the filters have been applied.</span></span>

<span data-ttu-id="5721c-297">**Abbildung 12. Site-Vorlagenauswahl before und after Beispielfilter angewendet wurden**</span><span class="sxs-lookup"><span data-stu-id="5721c-297">**Figure 12. Site template selection before and after sample filters have been applied**</span></span>

![Site-Vorlagenauswahl before und after Beispielfilter angewendet wurden](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/46c0e39d-dfec-45ed-9b72-ff3f6d5e1916.png)

<span data-ttu-id="5721c-299">Festgelegt sowohl Standard-als auch verfügbaren Seitenlayouts, indem Sie die zugeordneten ASPX-Dateien, die Methoden zum Erweiterungsmethoden, übergeben, wie im Code gezeigt.</span><span class="sxs-lookup"><span data-stu-id="5721c-299">The sample sets both the default and available page layouts by passing the associated *.aspx files to methods to extension methods, as shown in the code.</span></span>

```
                List<string> pageLayouts = new List<string>();
                pageLayouts.Add("ContosoLinksBelow.aspx");
                pageLayouts.Add("ContosoLinksRight.aspx");
                clientContext.Web.SetAvailablePageLayouts(clientContext.Web, pageLayouts);

                // Set default page layout for the site
                clientContext.Web.SetDefaultPageLayoutForSite(clientContext.Web, "ContosoLinksBelow.aspx");

```
<span data-ttu-id="5721c-300">Im Beispiel wird die verfügbaren Websitevorlagen durch dann in etwa wie folgt.</span><span class="sxs-lookup"><span data-stu-id="5721c-300">The sample sets the available site templates by doing something similar.</span></span> <span data-ttu-id="5721c-301">In diesem Fall wird die **WebTemplateEntity** -Instanzen, die jede Websitevorlage für eine Erweiterungsmethode namens **SetAvailableWebTemplates**definieren.</span><span class="sxs-lookup"><span data-stu-id="5721c-301">In this case it passes the **WebTemplateEntity** instances that define each site template to an extension method called **SetAvailableWebTemplates**.</span></span>

```
List<WebTemplateEntity> templates = new List<WebTemplateEntity>();
                templates.Add(new WebTemplateEntity() { LanguageCode = "1035", TemplateName = "STS#0" });
                templates.Add(new WebTemplateEntity() { LanguageCode = "", TemplateName = "STS#0" });
                templates.Add(new WebTemplateEntity() { LanguageCode = "", TemplateName = "BLOG#0" });
                clientContext.Web.SetAvailableWebTemplates(templates);

```

<span data-ttu-id="5721c-302">Alle drei dieser Erweiterungsmethoden - **SetAvailablePageLayouts**, **SetDefaultPageLayoutForSite**und **SetAvailableWebTemplates** - Arbeit in die gleiche Weise.</span><span class="sxs-lookup"><span data-stu-id="5721c-302">All three of these extension methods - **SetAvailablePageLayouts**, **SetDefaultPageLayoutForSite**, and **SetAvailableWebTemplates** - work in the same way.</span></span> <span data-ttu-id="5721c-303">Sie erstellen eine XML-Dokumente, die Schlüssel/Wert-Paare enthalten, die die verfügbaren und Standardlayouts und die verfügbaren Vorlagen definieren.</span><span class="sxs-lookup"><span data-stu-id="5721c-303">They create XML documents that contain key/value pairs that define the available and default layouts and the available templates.</span></span> <span data-ttu-id="5721c-304">Sie übergeben dann diese Dokumente an eine weitere Erweiterungsmethode **SetPropertyBagValue**aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="5721c-304">They then pass these documents to an additional extension method called **SetPropertyBagValue**.</span></span> <span data-ttu-id="5721c-305">Diese Methode ist in [OfficeDevPnPCore Erweiterung](hhttps://github.com/SharePoint/PnP-sites-core)implementiert.</span><span class="sxs-lookup"><span data-stu-id="5721c-305">This method is implemented in [OfficeDevPnPCore extension](hhttps://github.com/SharePoint/PnP-sites-core).</span></span> <span data-ttu-id="5721c-306">Nachdem sie die entsprechenden Eigenschaftenbehälter einrichtet, werden diese Eigenschaftenbehälter klicken Sie dann zum Filtern von Optionen auf der Benutzeroberfläche verwendet.</span><span class="sxs-lookup"><span data-stu-id="5721c-306">After it sets up the appropriate property bags, these property bags are then used to filter options in the interface.</span></span>

<span data-ttu-id="5721c-307">Die drei Methoden zeigt **SetAvailableWebTemplates** das vollständige Muster.</span><span class="sxs-lookup"><span data-stu-id="5721c-307">Of the three methods, **SetAvailableWebTemplates** shows the full pattern.</span></span>

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

<span data-ttu-id="5721c-308">Die Eigenschaftensammlung **InheritWebTemplates** stellt sicher, dass alle Vorlagen, die normalerweise von der übergeordneten Website geerbt werden beim Erstellen von Unterwebsites auch ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="5721c-308">The **InheritWebTemplates** property bag makes sure that any templates that are normally inherited from the parent site also are ignored when you create subsites.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5721c-309">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="5721c-309">Additional resources</span></span>
<span data-ttu-id="5721c-310"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="5721c-310"></span></span>

- [<span data-ttu-id="5721c-311">UX-Komponenten in SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="5721c-311">UX Components in SharePoint 2013 and SharePoint Online</span></span>](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [<span data-ttu-id="5721c-312">Provisioning.Pages</span><span class="sxs-lookup"><span data-stu-id="5721c-312">Provisioning.Pages</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages)
    
- [<span data-ttu-id="5721c-313">Branding.ApplyBranding</span><span class="sxs-lookup"><span data-stu-id="5721c-313">Branding.ApplyBranding</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ApplyBranding)
