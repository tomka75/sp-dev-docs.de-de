---
title: "Implementieren einer Lösung mit SharePoint-Website-Klassifizierung"
ms.date: 11/03/2017
ms.openlocfilehash: 366b09990039dcb23ad21bf3259d3cafe1c9cee9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="implement-a-sharepoint-site-classification-solution"></a><span data-ttu-id="55880-102">Implementieren einer Lösung mit SharePoint-Website-Klassifizierung</span><span class="sxs-lookup"><span data-stu-id="55880-102">Implement a SharePoint site classification solution</span></span>

<span data-ttu-id="55880-103">Implementieren Sie eine Lösung auf Klassifizierung in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="55880-103">Implement a site classification solution in SharePoint.</span></span>

<span data-ttu-id="55880-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="55880-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="55880-105">SharePoint-Websites können sogar mit gute Governance Unterdessen und wachsen aus Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="55880-105">Even with good governance, SharePoint sites can proliferate and grow out of control.</span></span> <span data-ttu-id="55880-106">Websites werden erstellt, wie sie sind erforderlich, aber nur selten gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="55880-106">Sites are created as they are needed, but are rarely deleted.</span></span> <span data-ttu-id="55880-107">Durchforstung mit der Suche nach nicht verwendeter Websitesammlungen belastet wird und Suche veraltete oder irrelevante Ergebnisse erzeugt.</span><span class="sxs-lookup"><span data-stu-id="55880-107">Search crawl is burdened by unused site collections, and search produces outdated and irrelevant results.</span></span> <span data-ttu-id="55880-108">Website-Klassifizierung können Sie identifizieren und Aufbewahren von vertraulichen Daten.</span><span class="sxs-lookup"><span data-stu-id="55880-108">Site classification allows you to identify and preserve sensitive data.</span></span> <span data-ttu-id="55880-109">In diesem Artikel zeigt, wie Sie mithilfe das [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) -Beispiel: Implementieren einer Website Klassifizierung-Lösung sowie Verwenden von SharePoint-websiterichtlinien zum Erzwingen von löschen.</span><span class="sxs-lookup"><span data-stu-id="55880-109">This article shows you how to use the [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) sample to implement a site classification solution, as well as use SharePoint site policies to enforce deletion.</span></span> <span data-ttu-id="55880-110">Sie können diese Lösung in Ihrer vorhandenen Website Benutzerwebsite für eine bessere Verwaltung Ihrer Websites integrieren.</span><span class="sxs-lookup"><span data-stu-id="55880-110">You can integrate this solution into your existing site provisioning solution to better manage your sites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="55880-111">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="55880-111">Before you begin</span></span>

<span data-ttu-id="55880-112">Herunterladen Sie das [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) -Beispiel um zu Beginn des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="55880-112">To get started, download the [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) sample from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="define-and-set-site-policies"></a><span data-ttu-id="55880-113">Definieren und Festlegen von Richtlinien für Website</span><span class="sxs-lookup"><span data-stu-id="55880-113">Define and set site policies</span></span>

<span data-ttu-id="55880-114">Zunächst müssen Sie definieren, und legen die websiterichtlinien, die alle Websitesammlungen verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="55880-114">Initially, you need to define and set the site policies that will be available in all your site collections.</span></span> <span data-ttu-id="55880-115">Im Beispiel Core.SiteClassification gilt für SharePoint Online MT, jedoch kann sowie in SharePoint Online dedizierter oder SharePoint lokal verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="55880-115">The Core.SiteClassification sample applies to SharePoint Online MT, but can be used as well in SharePoint Online Dedicated or SharePoint on-premises.</span></span> <span data-ttu-id="55880-116">Website-Richtlinien werden festgelegt, im Content Type Hub, die in SharePoint Online MT sich unter `https://[tenanatname]/sites/contentTypeHub`.</span><span class="sxs-lookup"><span data-stu-id="55880-116">Site polices are set in the Content Type Hub, which in SharePoint Online MT is located at  `https://[tenanatname]/sites/contentTypeHub`.</span></span> <span data-ttu-id="55880-117">Wechseln Sie zum Festlegen von Richtlinien für Website zu **Einstellungen** > **Websitesammlungsverwaltung** > **Websiterichtlinien** > ** erstellen **.</span><span class="sxs-lookup"><span data-stu-id="55880-117">To set site policies, go to  **Settings** > **Site Collection Administration** > **Site Policies** > ** create**.</span></span> <span data-ttu-id="55880-118">Die Seite **Neue Standortrichtlinie** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="55880-118">The  **New Site Policy** page appears.</span></span> <span data-ttu-id="55880-119">Weitere Informationen zu Website Richtlinienoptionen finden Sie unter [Übersicht über websiterichtlinien in SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="55880-119">For more information about site policy options, see [Overview of site policies in SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).</span></span>

<span data-ttu-id="55880-120">Geben Sie auf der Seite **Neue Standortrichtlinie** die folgenden Felder aus:</span><span class="sxs-lookup"><span data-stu-id="55880-120">On the  **New Site Policy** page, enter the following fields:</span></span>

-  <span data-ttu-id="55880-121">**Name:** HBI</span><span class="sxs-lookup"><span data-stu-id="55880-121">**Name:** HBI</span></span>
    
-  <span data-ttu-id="55880-122">**Beschreibung:** Dies ist super geheimen.</span><span class="sxs-lookup"><span data-stu-id="55880-122">**Description:** This is super secret.</span></span>
    
- <span data-ttu-id="55880-123">Legen Sie Optionsfeld **Websites automatisch löschen**.</span><span class="sxs-lookup"><span data-stu-id="55880-123">Set radio button  **Delete sites automatically**.</span></span>
    
- <span data-ttu-id="55880-124">Für **Delete-Ereignis:**, Datum + 1 Jahre erstellten Website verwenden.</span><span class="sxs-lookup"><span data-stu-id="55880-124">For  **Deletion Event:**, use Site created date + 1 years.</span></span>
    
- <span data-ttu-id="55880-125">Wählen Sie aus der **Senden einer e-Mail-Benachrichtigung an Websitebesitzer dies ganz vor Löschung:** Kontrollkästchen, und legen Sie ihn auf 1 Monate.</span><span class="sxs-lookup"><span data-stu-id="55880-125">Select the  **Send an email notification to site owners this far in advance of deletion:** check box, and set it to 1 months.</span></span>
    
- <span data-ttu-id="55880-126">Wählen Sie aus der **Weitere Benachrichtigungen senden alle:** Kontrollkästchen, und legen Sie es auf 14 Tage.</span><span class="sxs-lookup"><span data-stu-id="55880-126">Select the  **Send follow-up notifications every:** check box, and set it to 14 days.</span></span>
    
- <span data-ttu-id="55880-127">Wählen Sie aus der **Besitzer können anstehender Löschung für verschieben:** Kontrollkästchen, und legen Sie ihn auf 1 Monate.</span><span class="sxs-lookup"><span data-stu-id="55880-127">Select the  **Owners can postpone imminent deletion for:** check box, and set it to 1 months.</span></span>
    
- <span data-ttu-id="55880-128">Aktivieren Sie das Kontrollkästchen **schreibgeschützt, wenn es geschlossen wird, wird die Websitesammlung werden** .</span><span class="sxs-lookup"><span data-stu-id="55880-128">Select the  **The site collection will be read-only when it is closed** check box.</span></span>
    
<span data-ttu-id="55880-129">Wiederholen Sie diese Schritte für die Namen **MBI** und **LBI**noch zweimal.</span><span class="sxs-lookup"><span data-stu-id="55880-129">Repeat these steps two more times, for the names  **MBI** and **LBI**.</span></span> <span data-ttu-id="55880-130">Verwenden Sie unterschiedliche Einstellungen für löschen oder Retention Policies.</span><span class="sxs-lookup"><span data-stu-id="55880-130">Use different settings for deletion or retention policies.</span></span> <span data-ttu-id="55880-131">Wenn Sie fertig sind, können Sie die neuen Richtlinien veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="55880-131">When you're finished, you can publish the new policies.</span></span>

## <a name="insert-a-custom-action"></a><span data-ttu-id="55880-132">Einfügen einer benutzerdefinierten Aktion</span><span class="sxs-lookup"><span data-stu-id="55880-132">Insert a custom action</span></span>

<span data-ttu-id="55880-133">Sie können eine benutzerdefinierte Aktion für die Website-Klassifizierung auf der Seite **Einstellungen** und das **SharePoint Fanggeräte** -Symbol einfügen.</span><span class="sxs-lookup"><span data-stu-id="55880-133">You can insert a custom action for site classification to the  **Settings** page and the **SharePoint gear** icon.</span></span> <span data-ttu-id="55880-134">Diese Aktion ist nur verfügbar für Benutzer mit der Berechtigung **ManageWeb** .</span><span class="sxs-lookup"><span data-stu-id="55880-134">This action is only available to users with **ManageWeb** permission.</span></span> <span data-ttu-id="55880-135">Weitere Informationen finden Sie unter [Default Custom Action Locations and IDs](http://msdn.microsoft.com/en-us/library/office/bb802730%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="55880-135">For more information, see [Default Custom Action Locations and IDs](http://msdn.microsoft.com/en-us/library/office/bb802730%28v=office.15%29.aspx).</span></span>

> [!NOTE] 
> <span data-ttu-id="55880-136">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="55880-136">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
/// <summary>
/// Adds a custom Action to a Site Collection.
/// </summary>
/// <param name="ctx">The Authenticated client context.</param>
/// <param name="hostUrl">The Provider hosted URL for the Application</param>

static void AddCustomAction(ClientContext ctx, string hostUrl)
{
    var _web = ctx.Web;
    ctx.Load(_web);
    ctx.ExecuteQuery();

    // You only want the action to show up if you have manage web permissions.
    BasePermissions _manageWebPermission = new BasePermissions();
    _manageWebPermission.Set(PermissionKind.ManageWeb);

    CustomActionEntity _entity = new CustomActionEntity()
    {
        Group = "SiteTasks",
        Location = "Microsoft.SharePoint.SiteSettings",
        Title = "Site Classification",
        Sequence = 1000,
        Url = string.Format(hostUrl, ctx.Url),
        Rights = _manageWebPermission,
    };

    CustomActionEntity _siteActionSC = new CustomActionEntity()
    {
        Group = "SiteActions",
        Location = "Microsoft.SharePoint.StandardMenu",
        Title = "Site Classification",
        Sequence = 1000,
        Url = string.Format(hostUrl, ctx.Url),
        Rights = _manageWebPermission
    };
    _web.AddCustomAction(_entity);
    _web.AddCustomAction(_siteActionSC);
}
```

## <a name="custom-site-classification"></a><span data-ttu-id="55880-137">Benutzerdefinierte Website-Klassifizierung</span><span class="sxs-lookup"><span data-stu-id="55880-137">Custom site classification</span></span>

<span data-ttu-id="55880-138">Die Seite **Informationen zum Bearbeiten der Website** können Sie die folgenden bestimmte Klassifizierung Optionen auswählen:</span><span class="sxs-lookup"><span data-stu-id="55880-138">You can use the  **Edit Site Information** page to choose the following specific classification options:</span></span>

-  <span data-ttu-id="55880-139">**Benutzergruppe Bereich:** Legen Sie auf **Enterprise**, **Organisation**oder **Team**.</span><span class="sxs-lookup"><span data-stu-id="55880-139">**Audience Scope:** Set to **Enterprise**,  **Organization**, or  **Team**.</span></span>
    
-  <span data-ttu-id="55880-140">**Sicherheit Klassifizierung:** Legen Sie auf eine der eingegebene, wie etwa **LBI**Klassifizierung Kategorien.</span><span class="sxs-lookup"><span data-stu-id="55880-140">**Security Classification:** Set to one of the Classification categories you have entered, such as **LBI**.</span></span>
    
-  <span data-ttu-id="55880-141">**Ablaufdatum:** Überschreiben Sie das standardmäßige Ablaufdatum, die auf der zuvor eingegebenen Klassifikation basiert.</span><span class="sxs-lookup"><span data-stu-id="55880-141">**Expiration Date:** Override the default expiration date, which is based on the classification previously entered.</span></span>
    
<span data-ttu-id="55880-142">**Zielgruppe haben** und **Website-Klassifizierung** sind durchsuchbar und werden Eigenschaften zugeordnet, nachdem eine Durchforstung stattfindet verwaltet haben.</span><span class="sxs-lookup"><span data-stu-id="55880-142">Both  **Audience Reach** and **Site Classification** are searchable and will have managed properties associated with them after a crawl takes place.</span></span> <span data-ttu-id="55880-143">Diese Eigenschaften können dann um für bestimmte Arten von Websites mithilfe einer benutzerdefinierten verborgenen Liste innerhalb der Websitesammlung zu suchen.</span><span class="sxs-lookup"><span data-stu-id="55880-143">You can then use these properties to search for specific types of sites by using a custom hidden list within the site collection.</span></span> <span data-ttu-id="55880-144">Diese Liste wird in das Projekt [Core.SiteClassification.Common](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification/Core.SiteClassification.Common) in der **SiteManagerImpl** -Klasse implementiert.</span><span class="sxs-lookup"><span data-stu-id="55880-144">This list is implemented in the [Core.SiteClassification.Common](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification/Core.SiteClassification.Common) project in the **SiteManagerImpl** class.</span></span>

```C#
private void CreateSiteClassificationList(ClientContext ctx)
{
  var _newList = new ListCreationInformation()
    {
    Title = SiteClassificationList.SiteClassificationListTitle,
    Description = SiteClassificationList.SiteClassificationDesc,
    TemplateType = (int)ListTemplateType.GenericList,
    Url = SiteClassificationList.SiteClassificationUrl,
    QuickLaunchOption = QuickLaunchOptions.Off
    };

  if(!ctx.Web.ContentTypeExistsById(SiteClassificationContentType.SITEINFORMATION_CT_ID))
    {
    // Content type.
    ContentType _contentType = ctx.Web.CreateContentType(SiteClassificationContentType.SITEINFORMATION_CT_NAME,
    SiteClassificationContentType.SITEINFORMATION_CT_DESC,
    SiteClassificationContentType.SITEINFORMATION_CT_ID,
    SiteClassificationContentType.SITEINFORMATION_CT_GROUP);

    FieldLink _titleFieldLink = _contentType.FieldLinks.GetById(new Guid("fa564e0f-0c70-4ab9-b863-0177e6ddd247"));
    titleFieldLink.Required = false;
    contentType.Update(false);

    // Key Field.
    ctx.Web.CreateField(SiteClassificationFields.FLD_KEY_ID, 
      SiteClassificationFields.FLD_KEY_INTERNAL_NAME, 
      FieldType.Text, 
      SiteClassificationFields.FLD_KEY_DISPLAY_NAME, 
      SiteClassificationFields.FIELDS_GROUPNAME);

    // Value field.
    ctx.Web.CreateField(SiteClassificationFields.FLD_VALUE_ID, 
      SiteClassificationFields.FLD_VALUE_INTERNAL_NAME, 
      FieldType.Text, 
      SiteClassificationFields.FLD_VALUE_DISPLAY_NAME, 
      SiteClassificationFields.FIELDS_GROUPNAME);

    // Add Key Field to content type.
    ctx.Web.AddFieldToContentTypeById(SiteClassificationContentType.SITEINFORMATION_CT_ID, 
      SiteClassificationFields.FLD_KEY_ID.ToString(), 
      true);

    // Add Value Field to content type.
    ctx.Web.AddFieldToContentTypeById(SiteClassificationContentType.SITEINFORMATION_CT_ID,
      SiteClassificationFields.FLD_VALUE_ID.ToString(),
      true);
    }

  var _list = ctx.Web.Lists.Add(_newList);

  list.Hidden = true;
  list.ContentTypesEnabled = true;
  list.Update();
  ctx.Web.AddContentTypeToListById(SiteClassificationList.SiteClassificationListTitle,
    SiteClassificationContentType.SITEINFORMATION_CT_ID, true);
  this.CreateCustomPropertiesInList(_list);
  ctx.ExecuteQuery();
  this.RemoveFromQuickLaunch(ctx, SiteClassificationList.SiteClassificationListTitle);

}
```

<span data-ttu-id="55880-145">In der Standardeinstellung beim Erstellen einer Liste sofort einsetzbar oder CSOM, mit sind die Liste im Menü " **zuletzt verwendet** " verfügbar.</span><span class="sxs-lookup"><span data-stu-id="55880-145">By default, when you create a list either out of the box or by using CSOM, the list will be available in the  **Recent** menu.</span></span> <span data-ttu-id="55880-146">Die Liste muss jedoch ausgeblendet werden.</span><span class="sxs-lookup"><span data-stu-id="55880-146">The list needs to be hidden, however.</span></span> <span data-ttu-id="55880-147">Der folgende Code entfernt das Element aus dem letzten Menü.</span><span class="sxs-lookup"><span data-stu-id="55880-147">The following code removes the item from the Recent menu.</span></span>

```C#
private void RemoveFromQuickLaunch(ClientContext ctx, string listName)
  {
  Site _site = ctx.Site;
  Web _web = _site.RootWeb;

  ctx.Load(_web, x => x.Navigation, x => x.Navigation.QuickLaunch);
  ctx.ExecuteQuery();

  var _vNode = from NavigationNode _navNode in _web.Navigation.QuickLaunch
      where _navNode.Title == "Recent"
      select _navNode;

  NavigationNode _nNode = _vNode.First<NavigationNode>();
  ctx.Load(_nNode.Children);
  ctx.ExecuteQuery();
  var vcNode = from NavigationNode cn in _nNode.Children
     where cn.Title == listName
     select cn;
  NavigationNode _cNode = vcNode.First<NavigationNode>();
 _cNode.DeleteObject();
  ctx.ExecuteQuery();    
  }
```

<span data-ttu-id="55880-148">Im Beispiel Core.SiteClassification bietet die Möglichkeit, dass ein Administrator oder Benutzer mit der Berechtigung die neue Liste entfernen kann.</span><span class="sxs-lookup"><span data-stu-id="55880-148">The Core.SiteClassification sample provides for the possibility that a site administrator or someone with permission can remove the new list.</span></span> <span data-ttu-id="55880-149">Beim Zugriff auf diese Seite ist die Liste wird erneut erstellt, aber im Beispiel nicht legen Sie die Eigenschaften zurück.</span><span class="sxs-lookup"><span data-stu-id="55880-149">When this page is accessed, the list is created again, but the sample doesn't set the properties back.</span></span> <span data-ttu-id="55880-150">Sie können dies vermeiden, durch die Erweiterung des Beispiels, um die Berechtigungen in der Liste zu ändern, sodass nur Websitesammlungs-Administratoren Zugriff haben.</span><span class="sxs-lookup"><span data-stu-id="55880-150">You can avoid this by extending the sample to modify the permissions on the list so that only site collection administrators have access.</span></span> <span data-ttu-id="55880-151">Alternativ können Sie das [Core.SiteEnumeration](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration) Plug & Play-Beispiel überprüft in der Liste und Websiteadministratoren entsprechend benachrichtigt.</span><span class="sxs-lookup"><span data-stu-id="55880-151">Alternatively, you can use the [Core.SiteEnumeration](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration) PnP sample to do checks on the list and notify site administrators accordingly.</span></span>

<span data-ttu-id="55880-152">Überprüfen der Liste ist auch in der **SiteManagerImpl** -Klasse, in der Member **Initialisieren** implementiert.</span><span class="sxs-lookup"><span data-stu-id="55880-152">The list verification check is also implemented in the  **SiteManagerImpl** class, in the **Initialize** member.</span></span>

```C#
internal void Initialize(ClientContext ctx)
{
try {
         var _web = ctx.Web;
         var lists = _web.Lists;
         ctx.Load(_web);
         ctx.Load(lists, lc => lc.Where(l => l.Title == SiteClassificationList.SiteClassificationListTitle));
         ctx.ExecuteQuery();
                
          if (lists.Count == 0) {
                this.CreateSiteClassificationList(ctx); 
          }
      }
      catch(Exception _ex)
         {

         }
     }
}
```

> [!NOTE] 
> <span data-ttu-id="55880-153">Weitere Informationen finden Sie unter [Erstellen einer Liste in der Hostwebsite bei Ihrer SharePoint-add-in installiert ist, und entfernen Sie ihn aus der Liste der zuletzt verwendeten Elemente](http://blogs.technet.com/b/speschka/archive/2014/05/07/create-a-list-in-the-host-web-when-your-sharepoint-app-is-installed-and-remove-it-from-the-recent-stuff-list.aspx).</span><span class="sxs-lookup"><span data-stu-id="55880-153">For more information, see [Create a list in the host web when your SharePoint add-in is installed, and remove it from the recent stuff list](http://blogs.technet.com/b/speschka/archive/2014/05/07/create-a-list-in-the-host-web-when-your-sharepoint-app-is-installed-and-remove-it-from-the-recent-stuff-list.aspx).</span></span>

## <a name="add-a-classification-indicator-to-site-page"></a><span data-ttu-id="55880-154">Hinzufügen eines Indikators Klassifizierung zu Websiteseite</span><span class="sxs-lookup"><span data-stu-id="55880-154">Add a classification indicator to site page</span></span>

<span data-ttu-id="55880-155">Sie können ein Symbol zu einer Websiteseite zum Anzeigen der Einstufung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="55880-155">You can add an indicator to a site page to show its classification.</span></span> <span data-ttu-id="55880-156">Die Core.SiteClassificationsample zeigt, wie ein Bild mit der Klassifikation neben dem **Titel der Website**eingebettet ist.</span><span class="sxs-lookup"><span data-stu-id="55880-156">The Core.SiteClassificationsample shows how an image showing classification is embedded next to the  **Site Title**.</span></span> <span data-ttu-id="55880-157">In früheren Versionen von SharePoint erfolgt dies über ein serverseitiges stellvertretungs-Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="55880-157">In earlier versions of SharePoint, this is done via a server-side delegate control.</span></span> <span data-ttu-id="55880-158">Auch wenn Sie eine benutzerdefinierte Gestaltungsvorlage mit JavaScript verwenden können, wird in diesem Beispiel ein eingebettetes JavaScript-Muster.</span><span class="sxs-lookup"><span data-stu-id="55880-158">Although you can use a custom master page with JavaScript, this sample uses an embedded JavaScript pattern.</span></span> <span data-ttu-id="55880-159">Wenn Sie die **Standortrichtlinie** auf der Seite **Informationen zum Bearbeiten der Website** ändern, ändert diese das Website-Symbol, um ein kleines Feld mithilfe verschiedener Hintergrundfarben für den Standort Klassifizierung Entwurfsoptionen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="55880-159">When you change the **Site Policy** in the **Edit Site Information** page, this changes the site indicator to show a small box using different background colors for each of the site classification options.</span></span>

<span data-ttu-id="55880-160">Die folgende Methode ist in den Core.SiteClassificationWeb-Projekt, Skripts und classifier.js definiert.</span><span class="sxs-lookup"><span data-stu-id="55880-160">The following method is defined in the Core.SiteClassificationWeb project, scripts, and classifier.js.</span></span> <span data-ttu-id="55880-161">Die Bilder werden in einer Microsoft Azure-Website gespeichert.</span><span class="sxs-lookup"><span data-stu-id="55880-161">The images are stored in a Microsoft Azure website.</span></span> <span data-ttu-id="55880-162">Sie müssen die hartcodierte URLs entsprechend Ihrer Umgebung ändern.</span><span class="sxs-lookup"><span data-stu-id="55880-162">You will have to change the hard-coded URLs to match your environment.</span></span>

```C#
function setClassifier() {
    if (!classified)
    {
        var clientContext = SP.ClientContext.get_current();
        var query = "<View><Query><Where><Eq><FieldRef Name='SC_METADATA_KEY'/><Value Type='Text'>sc_BusinessImpact</Value></Eq></Where></Query><ViewFields><FieldRef Name='ID'/><FieldRef Name='SC_METADATA_KEY'/><FieldRef Name='SC_METADATA_VALUE'/></ViewFields></View>";
        var list = clientContext.get_web().get_lists().getByTitle("Site Information");
        clientContext.load(list);
        var camlQuery = new SP.CamlQuery();
        camlQuery.set_viewXml(query);
        var listItems = list.getItems(camlQuery);
        clientContext.load(listItems);

        clientContext.executeQueryAsync(Function.createDelegate(this, function (sender, args) {
            var listItemInfo;
            var listItemEnumerator = listItems.getEnumerator();

            while (listItemEnumerator.moveNext()) {
                listItemInfo = listItemEnumerator.get_current().get_item('SC_METADATA_VALUE');
                
                var pageTitle = $('#pageTitle')[0].innerHTML;
                if (pageTitle.indexOf("img") > -1) {
                    classified = true;
                }
                else {
                    var siteClassification = listItemInfo;
                    if (siteClassification == "HBI") {
                        var img = $("<a href='http://insertyourpolicy' target=_blank><img id=classifer name=classifer src='https://spmanaged.azurewebsites.net/content/img/hbi.png' title='Site contains personally identifiable information (PII), or unauthorized release of information on this site would cause severe or catastrophic loss to Contoso.' alt='Site contains personally identifiable information (PII), or unauthorized release of information on this site would cause severe or catastrophic loss to Contoso.'></a>");
                        $('#pageTitle').prepend(img);
                        classified = true;
                    }
                    else if (siteClassification == "MBI") {
                        var img = $("<a href='http://insertyourpolicy' target=_blank><img id=classifer name=classifer src='https://spmanaged.azurewebsites.net/content/img/mbi.png' title='Unauthorized release of information on this site would cause severe impact to Contoso.' alt='Unauthorized release of information on this site would cause severe impact to Contoso.'></a>");
                        $('#pageTitle').prepend(img);
                        classified = true;
                    }
                    else if (siteClassification == "LBI") {
                        var img = $("<a href='http://insertyourpolicy' target=_blank><img id=classifer name=classifer src='https://spmanaged.azurewebsites.net/content/img/lbi.png' title='Limited or no impact to Contoso if publically released.' alt='Limited or no impact to Contoso if publically released.'></a>");
                        $('#pageTitle').prepend(img);
                        classified = true;
                    }
                }
            }
        }));
    }
```

## <a name="alternative-approach"></a><span data-ttu-id="55880-163">Alternativer Ansatz</span><span class="sxs-lookup"><span data-stu-id="55880-163">Alternative approach</span></span>

<span data-ttu-id="55880-164">Erweiterungsmethode **Web.AddIndexedPropertyBagKey** können in der Datei ObjectPropertyBagEntry.cs[OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core) Sie um die klassifizierungswerte in Website-Eigenschaftenbehälter anstelle einer Liste zu speichern.</span><span class="sxs-lookup"><span data-stu-id="55880-164">You can use extension method  **Web.AddIndexedPropertyBagKey** in the ObjectPropertyBagEntry.cs file in[OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core) to store the classification values in site property bags instead of a list.</span></span> <span data-ttu-id="55880-165">Die Methode ermöglicht Eigenschaftenbehälter durchforsteten oder durchsuchbar sein.</span><span class="sxs-lookup"><span data-stu-id="55880-165">The method enables property bags to be crawled or searchable.</span></span>

## <a name="see-also"></a><span data-ttu-id="55880-166">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="55880-166">See also</span></span>
<span data-ttu-id="55880-167"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="55880-167"></span></span>

- [<span data-ttu-id="55880-168">SharePoint-Website Bereitstellen von Lösungen</span><span class="sxs-lookup"><span data-stu-id="55880-168">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="55880-169">OfficeDevPnP.Core-Beispiel</span><span class="sxs-lookup"><span data-stu-id="55880-169">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core)
    
- [<span data-ttu-id="55880-170">Core.SiteEnumeration-Beispiel</span><span class="sxs-lookup"><span data-stu-id="55880-170">Core.SiteEnumeration sample</span></span>](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration)
