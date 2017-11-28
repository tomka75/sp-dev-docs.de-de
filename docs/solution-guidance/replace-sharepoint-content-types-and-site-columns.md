---
title: Ersetzen Sie SharePoint-Inhaltstypen und Websitespalten
ms.date: 11/03/2017
ms.openlocfilehash: a707962d8a46dbc2f82a3bccd8668613f078d13d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="replace-sharepoint-content-types-and-site-columns"></a>Ersetzen Sie SharePoint-Inhaltstypen und Websitespalten

Verwenden Sie CSOM, um SharePoint Content Inhaltstypen und Websitespalten, neue Inhaltstypen Websitespalten hinzufügen, und ersetzen die Inhaltstypen durch neue Inhaltstypen zu ersetzen.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Hier erfahren Sie den XSL-Transformationsprozess beim Ersetzen von Inhaltstypen und Websitespalten, neue Inhaltstypen, Websitespalten hinzugefügt, und dann mit neue Inhaltstypen, die mit dem SharePoint mithilfe der clientseitigen Objektmodell (CSOM) ersetzen vorherige Inhaltstypen verwendet werden.

**Wichtig:**  Farmlösungen können nicht mit SharePoint Online migriert werden. Durch die Techniken und den Code in diesem Artikel beschriebenen anwenden, können Sie eine neue Lösung erstellen, die aktualisierte Inhaltstypen und Websitespalten verwendet und bietet eine ähnliche Funktionalität der farmlösungen oder dem deklarativen sandkastenlösungen. Die neue Lösung kann dann mit SharePoint Online bereitgestellt werden. Der Code in diesem Artikel erfordert zusätzlichen Code, um eine voll funktionsfähige Lösung bereitzustellen. In diesem Artikel erläutern beispielsweise nicht Anleitung zu Office 365, authentifizieren Implementierung Ausnahmebehandlung erforderlich, und so weiter. Zusätzliche Codebeispiele finden Sie unter [Office 365 Developer Mustern und Methoden Projekt](https://github.com/SharePoint/PnP).

## <a name="replace-content-types-and-site-columns"></a>Ersetzen Sie Inhaltstypen und Websitespalten

So ersetzen Sie Inhaltstypen und Spalten von Websites mithilfe von CSOM:

1. Erstellen eines neuen Inhaltstyps. 
    
2. Erstellen Sie neuer Websitespalten (auch als Felder bezeichnet).
    
3. Fügen Sie die neuen Websitespalten für den neuen Inhaltstyp hinzu.
    
4. Ersetzen Sie alte Inhaltstyp Verweise mit den neuen Inhaltstyp.
    
Im folgenden Code gezeigt **Main** die Reihenfolge der Vorgänge zum Ersetzen von Inhaltstypen und Websitespalten mithilfe von CSOM ausführen.

**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
static void Main(string[] args)
{
    using (var clientContext = new ClientContext("http://contoso.sharepoint.com"))
    {

        Web web = clientContext.Web;
        
        CreateContentType(clientContext, web);
        CreateSiteColumn(clientContext, web);
        AddSiteColumnToContentType(clientContext, web);

        // Replace the old content type with the new content type.
        ReplaceContentType(clientContext, web);
    }

}
```

Im folgenden Code ruft **GetContentTypeByName** einen Inhaltstyp von der aktuellen Website durch:

1. Verwenden die [Web.ContentTypes](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.contenttypes.aspx) -Eigenschaft zum Abrufen einer [ContentTypeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.aspx), die eine Auflistung von Inhaltstypen in der aktuellen Website ist.
    
2. Geben suchen, und klicken Sie dann zurückgeben eines Inhaltstyps aus der Website durch den Abgleich der Website Content Name auf den Namen des vorhandenen Inhaltstyp angegeben, das von der **Name** -Parameter bereitgestellt wird.

```C#
private static ContentType GetContentTypeByName(ClientContext cc, Web web, string name)
{
    ContentTypeCollection contentTypes = web.ContentTypes;
    cc.Load(contentTypes);
    cc.ExecuteQuery();
    return contentTypes.FirstOrDefault(o => o.Name == name);
}
```

Im folgenden Code wird **CreateContentType** durch einen neuen Inhaltstyp erstellt:

1. Erstellen eine Konstante als **Inhaltstypname** zum Speichern des Namens des Inhaltstyps bezeichnet. Der Name des neuen Inhaltstyps wird auf den Namen des vorherigen Inhaltstyps festgelegt.
    
2. Aufrufen von **GetContentTypeByName** , um einen übereinstimmenden Inhaltstyp auf der Website zu suchen.
    
3. Wenn der Inhaltstyp bereits vorhanden ist, keine weitere Aktion erforderlich ist und die Steuerung übergeben zurück zur **Hauptseite** , **zurückgeben** aufgerufen wird. Wenn der Inhaltstyp nicht vorhanden ist, werden Inhaltstypeigenschaften mithilfe eines [komplexer ContentTypeCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecreationinformation.aspx) -Objekts aufgerufen **NewCt**festgelegt. **NewCt.Id** mit der Basis Dokument Inhaltstyp-ID **0 x 0101**wird die neue Inhaltstyp-ID zugewiesen. Weitere Informationen finden Sie unter [Base Content Type Hierarchy](https://msdn.microsoft.com/library/office/ms452896%28v=office.14%29.aspx).
    
4. Den neuen Inhaltstyp mit [ContentTypeCollection.Add](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.add.aspx)hinzufügen.

```C#
private static void CreateContentType(ClientContext cc, Web web)
{
    // The new content type will be created using this name.
    const string contentTypeName = "ContosoDocumentByCSOM";

    // Determine whether the content type already exists.
    var contentType = GetContentTypeByName(cc, web, contentTypeName);

    // The content type exists already. No further action required.
    if (contentType != null) return;

    // Create the content type using the ContentTypeInformation object.
    ContentTypeCreationInformation newCt = new ContentTypeCreationInformation();
    newCt.Name = "ContosoDocumentByCSOM";

    // Create the new content type based on the out-of-the-box document (0x0101) and assign the ID to the new content type.
    newCt.Id = "0x0101009189AB5D3D2647B580F011DA2F356FB2";

    // Assign the content type to a specific content type group.
    newCt.Group = "Contoso Content Types";

    ContentType myContentType = web.ContentTypes.Add(newCt);
    cc.ExecuteQuery();
}
```

Im folgenden Code wird **CreateSiteColumn** durch eine neue Websitespalte erstellt:

1. Erstellen eine Konstante namens **FieldName** zum Speichern des Namens des Felds. Der Name des neuen Felds wird auf den Namen des vorherigen Feld festgelegt.
    
2. Abrufen der Websitespalten, die auf der Website mithilfe der [Web.Fields](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.fields.aspx) -Eigenschaft definiert.
    
3. Suchen ein entsprechendes Feld auf der Website durch den Namen der Felder auf der Website können **FieldName**abgleichen. Wenn das Feld bereits vorhanden ist, keine weitere Aktion erforderlich ist und die Steuerung übergeben zurück zur **Hauptseite** , **zurückgeben** aufgerufen wird. Wenn das Feld nicht vorhanden ist, eine CAML Zeichenfolge zur Angabe des Feldschema **FieldAsXML**zugewiesen ist, und klicken Sie dann wird das Feld mit [FieldCollection.AddFieldAsXml](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldcollection.addfieldasxml.aspx)erstellt.

```C#
private static void CreateSiteColumn(ClientContext cc, Web web)
{
    // The new field will be created using this name.
    const string fieldName = "ContosoStringCSOM";

    // Load the list of fields on the site.
    FieldCollection fields = web.Fields;
    cc.Load(fields);
    cc.ExecuteQuery();

    // Check fields on the site for a match.
    var fieldExists = fields.Any(f => f.InternalName == fieldName);

     // The field exists already. No further action required.    
    if (fieldExists) return;

    // Field does not exist, so create the new field.
    string FieldAsXML = @"<Field ID='{CB8E24F6-E1EE-4482-877B-19A51B4BE319}' 
                                Name='" + fieldName + @"' 
                                DisplayName='Contoso String by CSOM' 
                                Type='Text' 
                                Hidden='False' 
                                Group='Contoso Site Columns' 
                                Description='Contoso Text Field' />";
    Field fld = fields.AddFieldAsXml(FieldAsXML, true, AddFieldOptions.DefaultValue);
    cc.ExecuteQuery();
}
```

Im folgenden Code wird **AddSiteColumnToContentType** eine Verbindung zwischen den Inhaltstyp und das Feld, nach erstellt:

1. Laden den Inhaltstyp, und klicken Sie dann die Feldverweise in diesem Inhaltstyp mithilfe der [ContentType.FieldLinks](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.fieldlinks.aspx) -Eigenschaft.
    
2. Laden das Feld.
    
3. Bestimmen, ob der Inhaltstyp auf das Feld, mithilfe von verweist **contentType.FieldLinks.Any (f = > f.Name == FieldName)** , der auf der Name des Felds entspricht.
    
4.  Wenn der Inhaltstyp bereits auf das Feld verweist, keine weitere Aktion erforderlich ist und die Steuerung übergeben zurück zur **Hauptseite** , **zurückgeben** aufgerufen wird. Wenn der Inhaltstyp nicht in das Feld verweist, werden Feldeigenschaften Verweis für ein [FieldLinkCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldlinkcreationinformation.aspx) -Objekt festgelegt.
    
5. Die **ContentType.FieldLinks** -Eigenschaft hinzugefügt das **FieldLinkCreationInformation** -Objekt.

```C#
private static void AddSiteColumnToContentType(ClientContext cc, Web web)
{
    // The name of the content type. 
    const string contentTypeName = "ContosoDocumentByCSOM";
    // The field name
    const string fieldName = "ContosoStringCSOM";

    // Load the content type.
    var contentType = GetContentTypeByName(cc, web, contentTypeName);
    if (contentType == null) return; // content type was not found

    // Load field references in the content type.
    cc.Load(contentType.FieldLinks);
    cc.ExecuteQuery();

    // Load the new field.
    Field fld = web.Fields.GetByInternalNameOrTitle(fieldName);
    cc.Load(fld);
    cc.ExecuteQuery();

    // Determine whether the content type refers to the field.
    var hasFieldConnected = contentType.FieldLinks.Any(f => f.Name == fieldName);

    // A reference exists already, no further action is required.
    if (hasFieldConnected) return;

    // The reference does not exist, so we have to create the reference.
    FieldLinkCreationInformation link = new FieldLinkCreationInformation();
    link.Field = fld;
    contentType.FieldLinks.Add(link);
    contentType.Update(true);
    cc.ExecuteQuery();
}
```

Im folgenden Code überprüft **ReplaceContentType** alle Elemente in allen Bibliotheken für Inhalt, verweist auf den alten Inhaltstyp, und klicken Sie dann ersetzt die Verweise mit den neuen Inhaltstyp (**ContosoDocumentByCSOM**) durch:

1. Eine Konstante die alten Inhaltstyp-ID zugewiesen.
    
2. Abrufen von den neuen Inhaltstyp mithilfe von **GetContentTypeByName**.
    
3. Abrufen von allen Listen auf der Website mithilfe von [Web.Lists](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.lists.aspx).
    
4. Laden alle Listen auf der Website und alle Inhaltstypen für jede Liste mithilfe von **cc. Load (Listen, l = > l.Include (Liste = > Liste. ContentTypes)**.
    
5. Suchen für jede Liste zurückgegebenen Inhaltstypen der Liste, um einen Inhaltstyp mit der alten Inhaltstyp-ID mithilfe von **Liste übereinstimmen. ContentTypes.Any (c = > c.StringId.StartsWith(oldContentTypeId))**. Wenn eine Übereinstimmung gefunden wird, wird die Liste mit den alten Inhaltstyp **ListsWithContentType**hinzugefügt.
    
6. Für jede Liste in **ListsWithContentType**:
    
  1. Bestimmen, ob der neue Inhaltstyp der Liste zugeordnet ist. Wenn Sie der neue Inhaltstyp der Liste nicht angeschlossen ist, verwenden Sie [ContentTypeCollection.AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) So fügen Sie den neuen Inhaltstyp der Liste an.
    
  2. Abrufen aller Listenelemente in der Liste.
    
  3. Für jedes Listenelement Abrufen von Inhaltstyp-ID des Listenelements. Bestimmen Sie, ob die Inhaltstyp-ID des Listenelements alte Inhaltstyp-ID entspricht Wenn der Inhaltstyp-IDs nicht gleich sind, fahren Sie mit der nächsten Listenelement. Wenn der Inhaltstyp-IDs gleich sind, verwenden Sie [ContentType.StringId](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.stringid.aspx) das Element der Liste die neuen Inhaltstyp-ID zugewiesen.
    

**Hinweis:**  Der alte Inhaltstyp ist weiterhin in der Liste, aber er wird nicht mehr verwendet. Sie können jetzt den alten Inhaltstyp aus der Liste löschen, und es dann zurückgezogen. In diesem Artikel wird beschrieben, wie nur Dokumentinhaltstypen ersetzen. Wenn Sie Inhaltstypen auf Seitenlayouts ersetzen möchten, stellen Sie sicher, dass Sie die [AssociatedContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.publishing.pagelayout.associatedcontenttype.aspx) -Eigenschaft auf jeder Seitenlayout in der Websitesammlung aktualisieren.

```C#
private static void ReplaceContentType(ClientContext cc, Web web)
{
    // The old content type. 
    const string oldContentTypeId = "0x010100C32DDAB6381C44868DCD5ADC4A5307D6";
    // The new content type name
    const string newContentTypeName = "ContosoDocumentByCSOM";

    // Get the new content type and lists on the site.
    ContentType newContentType = GetContentTypeByName(cc, web, newContentTypeName);
    ListCollection lists = web.Lists;
    
    // Load the new content type and the content types on all lists on the site. 
    cc.Load(newContentType);
    cc.Load(lists,
            l => l.Include(list => list.ContentTypes));
    cc.ExecuteQuery();
    var listsWithContentType = new List<List>();
    foreach (List list in lists)
    {
        bool hasOldContentType = list.ContentTypes.Any(c => c.StringId.StartsWith(oldContentTypeId));
        if (hasOldContentType)
        {
            listsWithContentType.Add(list);
        }
    }
    foreach (List list in listsWithContentType)
    {
        // Determine whether the new content type is already attached to the list.
        var listHasContentTypeAttached = list.ContentTypes.Any(c => c.Name == newContentTypeName);
        if (!listHasContentTypeAttached)
        {
            // Attach content type to list.
            list.ContentTypes.AddExistingContentType(newContentType);
            cc.ExecuteQuery();
        }
        // Get all list items.
        CamlQuery query = CamlQuery.CreateAllItemsQuery();
        ListItemCollection items = list.GetItems(query);
        cc.Load(items);
        cc.ExecuteQuery();

        // For each list item, determine whether the old content type is used, and then update to the new content type. 
        foreach (ListItem listItem in items)
        {
            // Get the current content type for this list item.
            var currentContentTypeId = listItem["ContentTypeId"] + "";
            var isOldContentTypeAssigned = currentContentTypeId.StartsWith(oldContentTypeId);

            // This item does not use the old content type - skip to next list item.
            if (!isOldContentTypeAssigned) continue;

            // Update the list item content type to the new content type.
            listItem["ContentTypeId"] = newContentType.StringId; // new content type Id;
            listItem.Update();
        }
        // Save all changes.
        cc.ExecuteQuery();
    }
}
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Transformieren von Farmlösungen in das SharePoint-Add-In-Modell](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [SharePoint 2013](https://msdn.microsoft.com/library/office/jj162979.aspx)
