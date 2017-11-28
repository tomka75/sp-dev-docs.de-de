---
title: "Implementieren einer Lösung mit SharePoint-Website-Klassifizierung"
ms.date: 11/03/2017
ms.openlocfilehash: e1ab5cde87390d51a648815cce427ae4930aab85
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="implement-a-sharepoint-site-classification-solution"></a>Implementieren einer Lösung mit SharePoint-Website-Klassifizierung

Implementieren Sie eine Lösung auf Klassifizierung in SharePoint.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

SharePoint-Websites können sogar mit gute Governance Unterdessen und wachsen aus Steuerelement. Websites werden erstellt, wie sie sind erforderlich, aber nur selten gelöscht werden. Durchforstung mit der Suche nach nicht verwendeter Websitesammlungen belastet wird und Suche veraltete oder irrelevante Ergebnisse erzeugt. Website-Klassifizierung können Sie identifizieren und Aufbewahren von vertraulichen Daten. In diesem Artikel zeigt, wie Sie mithilfe das [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) -Beispiel: Implementieren einer Website Klassifizierung-Lösung sowie Verwenden von SharePoint-websiterichtlinien zum Erzwingen von löschen. Sie können diese Lösung in Ihrer vorhandenen Website Benutzerwebsite für eine bessere Verwaltung Ihrer Websites integrieren.

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Herunterladen Sie das [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) -Beispiel um zu Beginn des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="define-and-set-site-policies"></a>Definieren und Festlegen von Richtlinien für Website

Zunächst müssen Sie definieren, und legen die websiterichtlinien, die alle Websitesammlungen verfügbar ist. Im Beispiel Core.SiteClassification gilt für SharePoint Online MT, jedoch kann sowie in SharePoint Online dedizierter oder SharePoint lokal verwendet werden. Website-Richtlinien werden festgelegt, im Content Type Hub, die in SharePoint Online MT sich unter `https://[tenanatname]/sites/contentTypeHub`. Wechseln Sie zum Festlegen von Richtlinien für Website zu **Einstellungen** > **Websitesammlungsverwaltung** > **Websiterichtlinien** > ** erstellen **. Die Seite **Neue Standortrichtlinie** wird angezeigt. Weitere Informationen zu Website Richtlinienoptionen finden Sie unter [Übersicht über websiterichtlinien in SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).

Geben Sie auf der Seite **Neue Standortrichtlinie** die folgenden Felder aus:

-  **Name:** HBI
    
-  **Beschreibung:** Dies ist super geheimen.
    
- Legen Sie Optionsfeld **Websites automatisch löschen**.
    
- Für **Delete-Ereignis:**, Datum + 1 Jahre erstellten Website verwenden.
    
- Wählen Sie aus der **Senden einer e-Mail-Benachrichtigung an Websitebesitzer dies ganz vor Löschung:** Kontrollkästchen, und legen Sie ihn auf 1 Monate.
    
- Wählen Sie aus der **Weitere Benachrichtigungen senden alle:** Kontrollkästchen, und legen Sie es auf 14 Tage.
    
- Wählen Sie aus der **Besitzer können anstehender Löschung für verschieben:** Kontrollkästchen, und legen Sie ihn auf 1 Monate.
    
- Aktivieren Sie das Kontrollkästchen **schreibgeschützt, wenn es geschlossen wird, wird die Websitesammlung werden** .
    
Wiederholen Sie diese Schritte für die Namen **MBI** und **LBI**noch zweimal. Verwenden Sie unterschiedliche Einstellungen für löschen oder Retention Policies. Wenn Sie fertig sind, können Sie die neuen Richtlinien veröffentlichen.

## <a name="insert-a-custom-action"></a>Einfügen einer benutzerdefinierten Aktion

Sie können eine benutzerdefinierte Aktion für die Website-Klassifizierung auf der Seite **Einstellungen** und das **SharePoint Fanggeräte** -Symbol einfügen. Diese Aktion ist nur verfügbar für Benutzer mit der Berechtigung **ManageWeb** . Weitere Informationen finden Sie unter [Default Custom Action Locations and IDs](http://msdn.microsoft.com/en-us/library/office/bb802730%28v=office.15%29.aspx).

**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

## <a name="custom-site-classification"></a>Benutzerdefinierte Website-Klassifizierung

Die Seite **Informationen zum Bearbeiten der Website** können Sie die folgenden bestimmte Klassifizierung Optionen auswählen:

-  **Benutzergruppe Bereich:** Legen Sie auf **Enterprise**, **Organisation**oder **Team**.
    
-  **Sicherheit Klassifizierung:** Legen Sie auf eine der eingegebene, wie etwa **LBI**Klassifizierung Kategorien.
    
-  **Ablaufdatum:** Überschreiben Sie das standardmäßige Ablaufdatum, die auf der zuvor eingegebenen Klassifikation basiert.
    
**Zielgruppe haben** und **Website-Klassifizierung** sind durchsuchbar und werden Eigenschaften zugeordnet, nachdem eine Durchforstung stattfindet verwaltet haben. Diese Eigenschaften können dann um für bestimmte Arten von Websites mithilfe einer benutzerdefinierten verborgenen Liste innerhalb der Websitesammlung zu suchen. Diese Liste wird in das Projekt [Core.SiteClassification.Common](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification/Core.SiteClassification.Common) in der **SiteManagerImpl** -Klasse implementiert.

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

In der Standardeinstellung beim Erstellen einer Liste sofort einsetzbar oder CSOM, mit sind die Liste im Menü " **zuletzt verwendet** " verfügbar. Die Liste muss jedoch ausgeblendet werden. Der folgende Code entfernt das Element aus dem letzten Menü.

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

Im Beispiel Core.SiteClassification bietet die Möglichkeit, dass ein Administrator oder Benutzer mit der Berechtigung die neue Liste entfernen kann. Beim Zugriff auf diese Seite ist die Liste wird erneut erstellt, aber im Beispiel nicht legen Sie die Eigenschaften zurück. Sie können dies vermeiden, durch die Erweiterung des Beispiels, um die Berechtigungen in der Liste zu ändern, sodass nur Websitesammlungs-Administratoren Zugriff haben. Alternativ können Sie das [Core.SiteEnumeration](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration) Plug & Play-Beispiel überprüft in der Liste und Websiteadministratoren entsprechend benachrichtigt.

Überprüfen der Liste ist auch in der **SiteManagerImpl** -Klasse, in der Member **Initialisieren** implementiert.

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

**Hinweis:**  Weitere Informationen finden Sie unter [Erstellen einer Liste in der Hostwebsite bei Ihrer SharePoint-add-in installiert ist, und entfernen Sie ihn aus der Liste der zuletzt verwendeten Elemente](http://blogs.technet.com/b/speschka/archive/2014/05/07/create-a-list-in-the-host-web-when-your-sharepoint-app-is-installed-and-remove-it-from-the-recent-stuff-list.aspx).

## <a name="add-a-classification-indicator-to-site-page"></a>Hinzufügen eines Indikators Klassifizierung zu Websiteseite

Sie können ein Symbol zu einer Websiteseite zum Anzeigen der Einstufung hinzufügen. Die Core.SiteClassificationsample zeigt, wie ein Bild mit der Klassifikation neben dem **Titel der Website**eingebettet ist. In früheren Versionen von SharePoint erfolgt dies über ein serverseitiges stellvertretungs-Steuerelement. Auch wenn Sie eine benutzerdefinierte Gestaltungsvorlage mit JavaScript verwenden können, wird in diesem Beispiel ein eingebettetes JavaScript-Muster. Wenn Sie die **Standortrichtlinie** auf der Seite **Informationen zum Bearbeiten der Website** ändern, ändert diese das Website-Symbol, um ein kleines Feld mithilfe verschiedener Hintergrundfarben für den Standort Klassifizierung Entwurfsoptionen anzuzeigen.

Die folgende Methode ist in den Core.SiteClassificationWeb-Projekt, Skripts und classifier.js definiert. Die Bilder werden in einer Microsoft Azure-Website gespeichert. Sie müssen die hartcodierte URLs entsprechend Ihrer Umgebung ändern.

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

## <a name="alternative-approach"></a>Alternativer Ansatz

Erweiterungsmethode **Web.AddIndexedPropertyBagKey** können in der Datei ObjectPropertyBagEntry.cs[OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core) Sie um die klassifizierungswerte in Website-Eigenschaftenbehälter anstelle einer Liste zu speichern. Die Methode ermöglicht Eigenschaftenbehälter durchforsteten oder durchsuchbar sein.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [SharePoint-Website Bereitstellen von Lösungen](sharepoint-site-provisioning-solutions.md)
    
- [OfficeDevPnP.Core-Beispiel](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core)
    
- [Core.SiteEnumeration-Beispiel](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration)
