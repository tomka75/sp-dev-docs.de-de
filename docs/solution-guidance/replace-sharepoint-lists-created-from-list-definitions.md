---
title: Ersetzen von Listendefinitionen erstellte SharePoint-Listen
ms.date: 11/03/2017
ms.openlocfilehash: 99ccd2fa75968236ccd5505c5937e2dd2e1afe78
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="replace-sharepoint-lists-created-from-list-definitions"></a>Ersetzen von Listendefinitionen erstellte SharePoint-Listen
Ersetzen Sie Listen und Bibliotheken, die mithilfe von Listendefinitionen in SharePoint erstellt wurden. 

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Wenn Sie Listendefinitionen verwendet, um Listen in Ihrer farmlösung zu erstellen, erfahren Sie, wie sie in neue Lösungen umgewandelt, die ähnliche Funktionalität mithilfe des Clientobjektmodells (CSOM) zu ermöglichen. In diesem Artikel wird beschrieben, wie das Clientobjektmodell (CSOM) zu verwenden:

- Hier finden Sie Listen und Bibliotheken, die mithilfe von Listendefinitionen erstellt wurden.
    
- Erstellen und Konfigurieren von neuen Listen.
    
- Hinzufügen und Entfernen von Ansichten von Listen.
    
- Migrieren von Inhalten aus der ursprünglichen Liste in die neue Liste.

**Wichtig** <p>Farmlösungen können nicht mit SharePoint Online migriert werden. Durch die Techniken und den Code in diesem Artikel beschriebenen anwenden, können Sie einer neuen Lösung mit ähnlicher Funktionalität erstellen, dass Ihre farmlösungen zu ermöglichen, können in SharePoint Online bereitgestellt werden. Wenn Sie einen direkte Transformation Ansatz verwenden, müssen Sie die neue Lösung in SharePoint Online bereitzustellen. Wenn Sie den Einsatz oder der Inhaltsmigration Ansatz verwenden, können die Tools von Drittanbietern die Listen für Sie erstellen. Weitere Informationen finden Sie unter [Transformation Ansätze für Ihr neues SharePoint-Add-in bereitstellen](https://msdn.microsoft.com/library/dn986827.aspx#sectionSection1). Der Code in diesem Artikel erfordert zusätzlichen Code, um eine voll funktionsfähige Lösung bereitzustellen. In diesem Artikel erläutern beispielsweise nicht Anleitung zu Office 365, authentifizieren Implementierung Ausnahmebehandlung erforderlich, und so weiter. Zusätzliche Codebeispiele finden Sie unter [Office 365 Developer Mustern und Methoden Projekt](https://github.com/SharePoint/PnP).</p><p>Verwenden Sie die beschriebenen Verfahren in diesem Artikel nur ein paar Listen zu einem Zeitpunkt zu aktualisieren. Bei der Suche nach Listen zu aktualisieren, wird, sollte die Listen vom Listentyp nicht gefiltert werden.</p>

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Idealerweise sollten Sie überprüfen Ihrer vorhandenen farmlösungen, erfahren Sie mehr über die in diesem Artikel beschriebenen Verfahren und klicken Sie dann planen, wie diese Techniken beziehen sich auf die vorhandene Farm Solutions. Wenn Sie mit farmlösungen vertraut sind, oder nicht über eine vorhandene farmlösung verfügen entwickelt, kann es für Sie hilfreich sein:

1. Laden Sie die [Projektmappe Contoso.Intranet](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet). [Überprüfen der Anfangszustand der Website und Bibliothek für den Austausch](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-2%20Replacing%20Lists%20Created%20from%20Custom%20Templates/Lab.md#examine-the-initial-state-of-the-site-and-library-for-replacement) zum Abrufen von Listen erstellt wurden mit deklarativ Listendefinitionen einer schnellen Übersicht lesen.
    
    > [!NOTE] 
    > In Contoso.Intranet, in der Datei elements.xml für SP\ListTemplate\LTContosoLibrary ist die ID für die benutzerdefinierte Listenvorlage 10003. Sie verwenden diese zum Identifizieren der Vorlage, die zum Erstellen der Liste verwendet wurde. Überprüfen Sie auch die Konfigurationseinstellungen und Ansichten, die in Ihrer Liste definiert sind.

2. Informationen Sie zu farmlösungen. Weitere Informationen finden Sie unter [Übersicht über SharePoint 2010-Architekturen](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) und [Farmlösungen in SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).
    
## <a name="replace-lists-created-from-list-definitions"></a>Ersetzen von Listendefinitionen erstellte Listen

So ersetzen Sie Listen von Listendefinitionen erstellt:

1. Hier finden Sie Listen, die mit einer bestimmten Basis Vorlage erstellt wurden.
    
2. Erstellen Sie die neue Liste mit der Out-of-Box Listendefinition. 
    
3. Konfigurieren von Einstellungen für die Liste.
    
4. Festlegen von Inhaltstypen für die neue Liste basierend auf den Inhaltstypen, die für die ursprüngliche Liste festgelegt wurden.
    
5. (Optional) Ansichten hinzufügen. 
    
6. (Optional) Ansichten zu entfernen.
    
7. Migrieren von Inhalten aus der ursprünglichen Liste in die neue Liste.
    
Im folgenden Code veranschaulicht die Methode Listen zu suchen, die mit einer bestimmten Basis Vorlage erstellt wurden. Diese Methode:

1. Mithilfe der [ClientContext](https://msdn.microsoft.com/library/microsoft.sharepoint.client.clientcontext.aspx) alle Listen im aktuellen Web mit [Web.Lists](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.lists.aspx)abgerufen. Die Include-Anweisung wird in der Lambda-Ausdruck verwendet, um eine Sammlung von Listen zurückzugeben. Die zurückgegebenen Listen müssen alle Eigenschaftswerte für [BaseTemplate](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetemplate.aspx) [BaseType](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetype.aspx)und [Titel](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.title.aspx)angegeben haben.
    
2. Für jede Liste in der Auflistung der zurückgegebenen Listen Wenn die **List.BaseTemplate** 10003 gleich ist, hinzugefügt die Liste eine Sammlung von Listen ersetzt werden, **ListsToReplace**aufgerufen. Denken Sie daran, dass 10003 Bezeichner der benutzerdefinierten Listenvorlage war, als es in der Stichprobe Contoso.Intranet überprüft.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
static void Main(string[] args)
{
    using (var clientContext = new ClientContext("http://w15-sp/sites/ftclab"))
    {
        Web web = clientContext.Web;
        ListCollection listCollection = web.Lists;
        clientContext.Load(listCollection,
                            l => l.Include(list => list.BaseTemplate,
                                            list => list.BaseType,
                                            list => list.Title));
        clientContext.ExecuteQuery();
        var listsToReplace = new List<List>();
        foreach (List list in listCollection)
        {
            // 10003 is the custom list template ID of the list template you're replacing.
            if (list.BaseTemplate == 10003)
            {
                listsToReplace.Add(list);
            }
        }
        foreach (List list in listsToReplace)
        {
            ReplaceList(clientContext, listCollection, list);
        }
    }
}
```

**Wichtig:**  Im vorherigen Code durchlaufen zuerst die ListCollection auswählen, welche Listen müssen geändert werden, und rufen Sie dann ReplaceList, der gestartet wird, ändern die Listen. Dieses Muster ist erforderlich, da Ändern des Inhalts einer Auflistung beim Durchlaufen der Auflistung eine Ausnahme ausgelöst wird.

Nach der Identifizierung einer Liste, die ersetzt werden soll, zeigt **ReplaceList** die Reihenfolge der Vorgänge ausführen, um die Liste zu ersetzen.

```C#
private static void ReplaceList(ClientContext clientContext, ListCollection listCollection, List listToBeReplaced)
{
    var newList = CreateReplacementList(clientContext, listCollection, listToBeReplaced);

    SetListSettings(clientContext, listToBeReplaced, newList);

    SetContentTypes(clientContext, listToBeReplaced, newList);

    AddViews(clientContext, listToBeReplaced, newList);

    RemoveViews(clientContext, listToBeReplaced, newList);

    MigrateContent(clientContext, listToBeReplaced, newList);
}
```

So erstellen Sie eine neue Liste, verwendet **CreateReplacementList** [ListCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.listcreationinformation.aspx). Der Titel der neuen Liste wird auf den Titel der vorhandenen Liste mit Add-in angehängt festgelegt. Die [ListTemplateType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.listtemplatetype.aspx) -Enumeration wird der Listentyp Vorlage auf einer Dokumentbibliothek festgelegt. Wenn Sie eine Liste basierend auf einen anderen Vorlagentyp erstellen, stellen Sie sicher, dass Sie den richtige Vorlagentyp verwenden. Wenn Sie eine Kalenderliste erstellen, verwenden Sie **ListTemplateType.Events** anstelle von **ListTemplateType.DocumentLibrary**fest.

```C#
private static List CreateReplacementList(ClientContext clientContext, ListCollection lists,List listToBeReplaced)
{
    var creationInformation = new ListCreationInformation
    {
        Title = listToBeReplaced.Title + "add-in",
        TemplateType = (int) ListTemplateType.DocumentLibrary,
    };
    List newList = lists.Add(creationInformation);
    clientContext.ExecuteQuery();
    return newList;
}
```

**SetListSettings** gilt die ursprüngliche listeneinstellungen für die neue Liste durch:

1. Abrufen von verschiedenen Einstellungen für die Liste aus der ursprünglichen Liste.
    
2. Die Liste Einstellung aus der ursprünglichen Liste in die neue Liste anwenden.

```C#
private static void SetListSettings(ClientContext clientContext, List listToBeReplaced, List newList)
{
    clientContext.Load(listToBeReplaced, 
                        l => l.EnableVersioning, 
                        l => l.EnableModeration, 
                        l => l.EnableMinorVersions,
                        l => l.DraftVersionVisibility );
    clientContext.ExecuteQuery();
    newList.EnableVersioning = listToBeReplaced.EnableVersioning;
    newList.EnableModeration = listToBeReplaced.EnableModeration;
    newList.EnableMinorVersions= listToBeReplaced.EnableMinorVersions;
    newList.DraftVersionVisibility = listToBeReplaced.DraftVersionVisibility;
    newList.Update();
    clientContext.ExecuteQuery();
}
```

> [!NOTE] 
> Basierend auf Ihren Anforderungen, können die Einstellungen für die Liste Ihrer ursprünglichen Listen abweichen. Überprüfen Sie die listeneinstellungen, und ändern Sie **SetListSettings** , um sicherzustellen, dass die ursprünglichen listeneinstellungen auf Ihre neuen Listen angewendet werden.

**SetContentTypes** setzt die Inhaltstypen in der neuen Liste durch:

1. Abrufen von Inhaltstyp-Informationen aus der ursprünglichen Liste.
    
2. Abrufen von Inhaltstyp-Informationen aus der neuen Liste.
    
3. Bestimmen, ob die ursprüngliche Liste Inhaltstypen ermöglicht. Wenn die ursprüngliche Liste Inhaltstypen nicht aktiviert wird, beendet **SetContentTypes** . Wenn die ursprüngliche Liste Inhaltstypen aktiviert, und klicken Sie dann **SetContentTypes** ermöglicht Inhaltstypen auf die neue Liste mit **newList.ContentTypesEnabled = True**.
    
4. Für jeden Inhaltstyp in der ursprünglichen Liste, suchen den Inhalt für die neue Liste, eine entsprechende Content Type basierend auf den Namen des Inhaltstyps mithilfe von **newList.ContentTypes.Any erhalten Typen (ct = > ct. Name == contentType.Name)**. Wenn der Inhaltstyp nicht in der neuen Liste ist, wird es der Liste hinzugefügt.
    
5. Laden ein zweites Mal **NewList** , da [AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) möglicherweise die Inhaltstypen geändert haben.
    
6. Für jeden Inhaltstyp in **NewList**, bestimmen, ob der Inhaltstyp ein Inhaltstyps in der ursprünglichen Liste basierend auf [ContentType.Name](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.name.aspx) mithilfe von **listToBeReplaced.ContentTypes.Any entspricht (ct = > ct. Name == contentType.Name)**. Wenn eine Übereinstimmung gefunden wird, wird der Inhaltstyp **ContentTypesToDelete** aus der neuen Liste gelöscht werden hinzugefügt.
    
7. Löschen des Inhaltstyps [ContentType.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.deleteobject.aspx)aufrufen.

> [!NOTE] 
> Wenn Sie einen direkte Transformation Ansatz verwenden und Ihre Inhaltstypen deklarativ mithilfe des Feature-Frameworks bereitgestellt wurden, müssen Sie: 

 1. Erstellen Sie neue Inhaltstypen.

 2. Legen Sie den Inhaltstyp für die Listenelemente beim Migrieren von Inhalt aus der ursprünglichen Liste auf die neue Liste im MigrateContent.


```C#
private static void SetContentTypes(ClientContext clientContext, List listToBeReplaced, List newList)
{
    clientContext.Load(listToBeReplaced,
                        l => l.ContentTypesEnabled,
                        l => l.ContentTypes);
    clientContext.Load(newList,
                        l => l.ContentTypesEnabled,
                        l => l.ContentTypes);
    clientContext.ExecuteQuery();

    // If the original list doesn't use content types, do not proceed any further.
    if (!listToBeReplaced.ContentTypesEnabled) return;

    newList.ContentTypesEnabled = true;
    newList.Update();
    clientContext.ExecuteQuery();
    foreach (var contentType in listToBeReplaced.ContentTypes)
    {
        if (!newList.ContentTypes.Any(ct => ct.Name == contentType.Name))
        {
            // Current content type needs to be added to the new list. Note that the content type is added to the list, not the site.           
            newList.ContentTypes.AddExistingContentType(contentType.Parent);
            newList.Update();
            clientContext.ExecuteQuery();
        }
    }
    // Reload the content types on newList because they might have changed when AddExistingContentType was called. 
    clientContext.Load(newList, l => l.ContentTypes);
    clientContext.ExecuteQuery();
    // Remove any content types that are not needed.
    var contentTypesToDelete = new List<ContentType>();
    foreach (var contentType in newList.ContentTypes)
    {
        if (!listToBeReplaced.ContentTypes.Any(ct => ct.Name == contentType.Name))
        {
            // Current content type needs to be removed from new list.
            contentTypesToDelete.Add(contentType);
        }
    }
    foreach (var contentType in contentTypesToDelete)
    {
        contentType.DeleteObject();
    }
    newList.Update();
    clientContext.ExecuteQuery();
}
```

> [!NOTE] 
> Zu diesem Zeitpunkt kann die neue Liste Inhalt aus der ursprünglichen Liste annehmen. Sie können auch optional hinzufügen und Entfernen von Ansichten. 

Benutzer können hinzufügen oder Entfernen von Ansichten in einer Liste zu ihrer geschäftlichen Anforderungen definiert. Aus diesem Grund müssen Sie zum Hinzufügen oder Entfernen von Ansichten für die neue Liste.  **AddViews** hinzugefügt der neuen Liste von Ansichten aus der ursprünglichen Liste:

1. Verwenden zum Abrufen aller Ansichten in der ursprünglichen Liste [List.Views](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.views.aspx) .
    
2. Verwenden des Lambda-Ausdrucks geladen werden verschiedene Eigenschaften anzeigen auf die **Views** -Auflistung.
    
3. Erstellen eine Ansicht für die einzelnen Ansichten in der ursprünglichen Liste mithilfe von [komplexer ViewCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewcreationinformation.aspx). Verschiedene Eigenschaften für die neue Ansicht basierend auf Eigenschaften anzeigen, aus der ursprünglichen Ansicht festgelegt. Die Hilfsmethode **GetViewType** wird aufgerufen, um die [ViewType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewtype.aspx) der Ansicht zu bestimmen. Die Liste der Ansichten **ViewsToCreate**aufgerufen wird dann die neue Ansicht hinzugefügt.
    
4. Die Ansichten hinzufügen mithilfe der **Add** -Methode in der Liste Views-Auflistung der **List.Views** -Auflistung.

```C#
private static void AddViews(ClientContext clientContext, List listToBeReplaced, List newList)
{
    ViewCollection views = listToBeReplaced.Views;
    clientContext.Load(views,
                        v => v.Include(view => view.Paged,
                            view => view.PersonalView,
                            view => view.ViewQuery,
                            view => view.Title,
                            view => view.RowLimit,
                            view => view.DefaultView,
                            view => view.ViewFields,
                            view => view.ViewType));
    clientContext.ExecuteQuery();

    // Build a list of views which exist on the original list only.
    var viewsToCreate = new List<ViewCreationInformation>();
    foreach (View view in listToBeReplaced.Views)
    {
      var createInfo = new ViewCreationInformation
      {
          Paged = view.Paged,
          PersonalView = view.PersonalView,
          Query = view.ViewQuery,
          Title = view.Title,
          RowLimit = view.RowLimit,
          SetAsDefaultView = view.DefaultView,
          ViewFields = view.ViewFields.ToArray(),
          ViewTypeKind = GetViewType(view.ViewType),
      };
      viewsToCreate.Add(createInfo);
    }
    
    foreach (ViewCreationInformation newView in viewsToCreate)
    {
        newList.Views.Add(newView);
    }
    newList.Update();
}

private static ViewType GetViewType(string viewType)
{
    switch (viewType)
    {
        case "HTML":
            return ViewType.Html;
        case "GRID":
            return ViewType.Grid;
        case "CALENDAR":
            return ViewType.Calendar;
        case "RECURRENCE":
            return ViewType.Recurrence;
        case "CHART":
            return ViewType.Chart;
        case "GANTT":
            return ViewType.Gantt;
        default:
            return ViewType.None;
    }
}
```

Im folgenden Code werden **RemoveViews** Ansichten aus der neuen Liste entfernt:

1. Abrufen von Listenansichten auf die neue Liste mithilfe der **List.Views** -Eigenschaft.
    
2. Für jede Ansicht in der neuen Liste bestimmen, ob die Ansicht in der ursprünglichen Liste nicht vorhanden ist, durch Klicken auf den Titel der Ansicht mithilfe von **entsprechende! listToBeReplaced.Views.Any (V = > v.Title == anzeigen. Titel**. Wenn eine Ansicht in der neuen Liste eine entsprechende Ansicht nicht in der ursprünglichen Liste verfügt, fügen Sie der Ansicht **ViewsToRemove**hinzu.
    
3. Löschen aller Ansichten in **ViewsToRemove** mit [View.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.view.deleteobject.aspx).
    
```C#
private static void RemoveViews(ClientContext clientContext, List listToBeReplaced, List newList)
{
    // Get the list of views on the new list.
    clientContext.Load(newList, l => l.Views);
    clientContext.ExecuteQuery();

    var viewsToRemove = new List<View>();
    foreach (View view in newList.Views)
    {
        if (!listToBeReplaced.Views.Any(v => v.Title == view.Title))
        {
            // If there is no matching view in the source list, add the view to the list of views to be deleted.
            viewsToRemove.Add(view);
        }
    }
    foreach (View view in viewsToRemove)
    {
        view.DeleteObject();
    }
    newList.Update();
    clientContext.ExecuteQuery();
}
```

**MigrateContent** migriert die Inhalte aus der ursprünglichen Liste auf die neue Liste durch:

1. Das Ziel, um die Dateien zu kopieren oder den Stammordner der neuen Liste mithilfe von [List.RootFolder](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.rootfolder.aspx)abgerufen. Mithilfe von [Folder.ServerRelativeUrl](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.folder.serverrelativeurl.aspx)ist die serverrelative URL des Listenordners Ziel abgerufen.
    
2. Abrufen der Quelle für die Dateien oder den Stammordner der ursprünglichen Liste mit **List.RootFolder**. Die serverrelative URL des Listenordners und alle Dateien im Stammordner der Quelle werden mithilfe des **ClientContext** -Objekts geladen.
    
3. Für jede Datei in der Quelle erstellen **NewUrl**, womit die neue URL der Datei gespeichert. **NewUrl** wird erstellt, durch das Ziel Stammordner der Stamm des Quellordners ersetzen.
    
4. Kopieren die Datei auf die URL des Stammordners Ziel mithilfe [File.CopyTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.copyto.aspx) . Alternativ können Sie die [File.MoveTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.moveto.aspx) -Methode verwenden, um die Datei an die Ziel-URL zu verschieben.
    
> [!NOTE] 
> Der folgende Code gibt alle Listenelemente. Sollten Sie in Ihrer produktionsumgebung den folgenden Code durch Implementieren einer Schleife, und Migrieren von kleine Mengen von Listenelementen mithilfe mehrerer Iterationen optimieren.

```C#
private static void MigrateContent(ClientContext clientContext, List listToBeReplaced, List newList)
{
    ListItemCollection items = listToBeReplaced.GetItems(CamlQuery.CreateAllItemsQuery());
    Folder destination = newList.RootFolder;
    Folder source = listToBeReplaced.RootFolder;
    clientContext.Load(destination,
                        d => d.ServerRelativeUrl);
    clientContext.Load(source,
                        s => s.Files,
                        s => s.ServerRelativeUrl);
    clientContext.Load(items,
                        i => i.IncludeWithDefaultProperties(item => item.File));
    clientContext.ExecuteQuery();


    foreach (File file in source.Files)
    {
        string newUrl = file.ServerRelativeUrl.Replace(source.ServerRelativeUrl, destination.ServerRelativeUrl);
          file.CopyTo(newUrl, true);
          //file.MoveTo(newUrl, MoveOperations.Overwrite);
    }
    clientContext.ExecuteQuery();
}
```

> [!NOTE] 
> Der vorstehende Code veranschaulicht, wie zum Migrieren von Dateien in einer Liste im Stammordner gespeichert. Wenn Ihre Liste Unterordner umfasst, müssen Sie zusätzlichen Code zum Migrieren der Unterordner und deren Inhalt hinzu. Wenn in Ihrer Liste Workflows verwendet wird, ist zusätzlicher Code erforderlich, können Sie den Workflow auf die neue Liste zuordnen.

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Transformieren von Farmlösungen in das SharePoint-Add-In-Modell](Transform-farm-solutions-to-the-SharePoint-app-model.md)
- [SharePoint 2013](https://msdn.microsoft.com/library/office/jj162979.aspx)
