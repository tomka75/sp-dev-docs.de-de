---
title: Ersetzen Sie SharePoint-Inhaltstypen und Websitespalten
ms.date: 11/03/2017
ms.openlocfilehash: a707962d8a46dbc2f82a3bccd8668613f078d13d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="replace-sharepoint-content-types-and-site-columns"></a><span data-ttu-id="c4780-102">Ersetzen Sie SharePoint-Inhaltstypen und Websitespalten</span><span class="sxs-lookup"><span data-stu-id="c4780-102">Replace SharePoint content types and site columns</span></span>

<span data-ttu-id="c4780-103">Verwenden Sie CSOM, um SharePoint Content Inhaltstypen und Websitespalten, neue Inhaltstypen Websitespalten hinzufügen, und ersetzen die Inhaltstypen durch neue Inhaltstypen zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="c4780-103">Use CSOM to replace SharePoint content types and site columns, add site columns to new content types, and replace the content types with new content types.</span></span>

<span data-ttu-id="c4780-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="c4780-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="c4780-105">Hier erfahren Sie den XSL-Transformationsprozess beim Ersetzen von Inhaltstypen und Websitespalten, neue Inhaltstypen, Websitespalten hinzugefügt, und dann mit neue Inhaltstypen, die mit dem SharePoint mithilfe der clientseitigen Objektmodell (CSOM) ersetzen vorherige Inhaltstypen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c4780-105">Learn the transformation process to use when replacing content types and site columns, adding site columns to new content types, and then replacing previous content types with new content types using the SharePoint client-side object model (CSOM).</span></span>

<span data-ttu-id="c4780-106">**Wichtig:**  Farmlösungen können nicht mit SharePoint Online migriert werden.</span><span class="sxs-lookup"><span data-stu-id="c4780-106">**Important:**  Farm solutions cannot be migrated to SharePoint Online.</span></span> <span data-ttu-id="c4780-107">Durch die Techniken und den Code in diesem Artikel beschriebenen anwenden, können Sie eine neue Lösung erstellen, die aktualisierte Inhaltstypen und Websitespalten verwendet und bietet eine ähnliche Funktionalität der farmlösungen oder dem deklarativen sandkastenlösungen.</span><span class="sxs-lookup"><span data-stu-id="c4780-107">By applying the techniques and code described in this article, you can build a new solution that uses updated content types and site columns and provides similar functionality to your farm solutions or declarative sandbox solutions.</span></span> <span data-ttu-id="c4780-108">Die neue Lösung kann dann mit SharePoint Online bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="c4780-108">The new solution can then be deployed to SharePoint Online.</span></span> <span data-ttu-id="c4780-109">Der Code in diesem Artikel erfordert zusätzlichen Code, um eine voll funktionsfähige Lösung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="c4780-109">The code in this article requires additional code to provide a fully working solution.</span></span> <span data-ttu-id="c4780-110">In diesem Artikel erläutern beispielsweise nicht Anleitung zu Office 365, authentifizieren Implementierung Ausnahmebehandlung erforderlich, und so weiter.</span><span class="sxs-lookup"><span data-stu-id="c4780-110">For example, this article does not discuss how to authenticate to Office 365, how to implement required exception handling, and so on.</span></span> <span data-ttu-id="c4780-111">Zusätzliche Codebeispiele finden Sie unter [Office 365 Developer Mustern und Methoden Projekt](https://github.com/SharePoint/PnP).</span><span class="sxs-lookup"><span data-stu-id="c4780-111">For additional code samples, see the [Office 365 Developer Patterns and Practices project](https://github.com/SharePoint/PnP).</span></span>

## <a name="replace-content-types-and-site-columns"></a><span data-ttu-id="c4780-112">Ersetzen Sie Inhaltstypen und Websitespalten</span><span class="sxs-lookup"><span data-stu-id="c4780-112">Replace content types and site columns</span></span>

<span data-ttu-id="c4780-113">So ersetzen Sie Inhaltstypen und Spalten von Websites mithilfe von CSOM:</span><span class="sxs-lookup"><span data-stu-id="c4780-113">To replace content types and site columns by using CSOM:</span></span>

1. <span data-ttu-id="c4780-114">Erstellen eines neuen Inhaltstyps.</span><span class="sxs-lookup"><span data-stu-id="c4780-114">Create a new content type.</span></span> 
    
2. <span data-ttu-id="c4780-115">Erstellen Sie neuer Websitespalten (auch als Felder bezeichnet).</span><span class="sxs-lookup"><span data-stu-id="c4780-115">Create new site columns (also referred to as fields).</span></span>
    
3. <span data-ttu-id="c4780-116">Fügen Sie die neuen Websitespalten für den neuen Inhaltstyp hinzu.</span><span class="sxs-lookup"><span data-stu-id="c4780-116">Add the new site columns to the new content type.</span></span>
    
4. <span data-ttu-id="c4780-117">Ersetzen Sie alte Inhaltstyp Verweise mit den neuen Inhaltstyp.</span><span class="sxs-lookup"><span data-stu-id="c4780-117">Replace old content type references with the new content type.</span></span>
    
<span data-ttu-id="c4780-118">Im folgenden Code gezeigt **Main** die Reihenfolge der Vorgänge zum Ersetzen von Inhaltstypen und Websitespalten mithilfe von CSOM ausführen.</span><span class="sxs-lookup"><span data-stu-id="c4780-118">In the following code,  **Main** shows the order of operations to perform to replace content types and site columns by using CSOM.</span></span>

<span data-ttu-id="c4780-119">**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="c4780-119">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="c4780-120">Im folgenden Code ruft **GetContentTypeByName** einen Inhaltstyp von der aktuellen Website durch:</span><span class="sxs-lookup"><span data-stu-id="c4780-120">In the following code,  **GetContentTypeByName** gets a content type from the current site by:</span></span>

1. <span data-ttu-id="c4780-121">Verwenden die [Web.ContentTypes](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.contenttypes.aspx) -Eigenschaft zum Abrufen einer [ContentTypeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.aspx), die eine Auflistung von Inhaltstypen in der aktuellen Website ist.</span><span class="sxs-lookup"><span data-stu-id="c4780-121">Using the [Web.ContentTypes](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.contenttypes.aspx) property to get a [ContentTypeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.aspx), which is a collection of content types on the current site.</span></span>
    
2. <span data-ttu-id="c4780-122">Geben suchen, und klicken Sie dann zurückgeben eines Inhaltstyps aus der Website durch den Abgleich der Website Content Name auf den Namen des vorhandenen Inhaltstyp angegeben, das von der **Name** -Parameter bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="c4780-122">Finding and then returning a content type from the site, by matching the site content type name to the name of the existing content type, which is submitted by the **name** parameter.</span></span>

```C#
private static ContentType GetContentTypeByName(ClientContext cc, Web web, string name)
{
    ContentTypeCollection contentTypes = web.ContentTypes;
    cc.Load(contentTypes);
    cc.ExecuteQuery();
    return contentTypes.FirstOrDefault(o => o.Name == name);
}
```

<span data-ttu-id="c4780-123">Im folgenden Code wird **CreateContentType** durch einen neuen Inhaltstyp erstellt:</span><span class="sxs-lookup"><span data-stu-id="c4780-123">In the following code,  **CreateContentType** creates a new content type by:</span></span>

1. <span data-ttu-id="c4780-124">Erstellen eine Konstante als **Inhaltstypname** zum Speichern des Namens des Inhaltstyps bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="c4780-124">Creating a constant called  **contentTypeName** to store the name of the content type.</span></span> <span data-ttu-id="c4780-125">Der Name des neuen Inhaltstyps wird auf den Namen des vorherigen Inhaltstyps festgelegt.</span><span class="sxs-lookup"><span data-stu-id="c4780-125">The name of the new content type will be set to the name of the previous content type.</span></span>
    
2. <span data-ttu-id="c4780-126">Aufrufen von **GetContentTypeByName** , um einen übereinstimmenden Inhaltstyp auf der Website zu suchen.</span><span class="sxs-lookup"><span data-stu-id="c4780-126">Calling  **GetContentTypeByName** to find a matching content type on the site.</span></span>
    
3. <span data-ttu-id="c4780-127">Wenn der Inhaltstyp bereits vorhanden ist, keine weitere Aktion erforderlich ist und die Steuerung übergeben zurück zur **Hauptseite** , **zurückgeben** aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="c4780-127">If the content type already exists, no further action is necessary and control passes back to  **Main** when **return** is called.</span></span> <span data-ttu-id="c4780-128">Wenn der Inhaltstyp nicht vorhanden ist, werden Inhaltstypeigenschaften mithilfe eines [komplexer ContentTypeCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecreationinformation.aspx) -Objekts aufgerufen **NewCt**festgelegt.</span><span class="sxs-lookup"><span data-stu-id="c4780-128">If the content type does not exist, content type properties are set using a [ContentTypeCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecreationinformation.aspx) object called **newCt**.</span></span> <span data-ttu-id="c4780-129">**NewCt.Id** mit der Basis Dokument Inhaltstyp-ID **0 x 0101**wird die neue Inhaltstyp-ID zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="c4780-129">The new content type ID is assigned to **newCt.Id** using the base document content type ID **0x0101**.</span></span> <span data-ttu-id="c4780-130">Weitere Informationen finden Sie unter [Base Content Type Hierarchy](https://msdn.microsoft.com/library/office/ms452896%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4780-130">For more information, see [Base Content Type Hierarchy](https://msdn.microsoft.com/library/office/ms452896%28v=office.14%29.aspx).</span></span>
    
4. <span data-ttu-id="c4780-131">Den neuen Inhaltstyp mit [ContentTypeCollection.Add](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.add.aspx)hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c4780-131">Adding the new content type using [ContentTypeCollection.Add](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.add.aspx).</span></span>

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

<span data-ttu-id="c4780-132">Im folgenden Code wird **CreateSiteColumn** durch eine neue Websitespalte erstellt:</span><span class="sxs-lookup"><span data-stu-id="c4780-132">In the following code,  **CreateSiteColumn** creates a new site column by:</span></span>

1. <span data-ttu-id="c4780-133">Erstellen eine Konstante namens **FieldName** zum Speichern des Namens des Felds.</span><span class="sxs-lookup"><span data-stu-id="c4780-133">Creating a constant called  **fieldName** to store the name of the field.</span></span> <span data-ttu-id="c4780-134">Der Name des neuen Felds wird auf den Namen des vorherigen Feld festgelegt.</span><span class="sxs-lookup"><span data-stu-id="c4780-134">The name of the new field will be set to the name of the previous field.</span></span>
    
2. <span data-ttu-id="c4780-135">Abrufen der Websitespalten, die auf der Website mithilfe der [Web.Fields](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.fields.aspx) -Eigenschaft definiert.</span><span class="sxs-lookup"><span data-stu-id="c4780-135">Getting the site columns defined on the site by using the [Web.Fields](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.fields.aspx) property.</span></span>
    
3. <span data-ttu-id="c4780-136">Suchen ein entsprechendes Feld auf der Website durch den Namen der Felder auf der Website können **FieldName**abgleichen.</span><span class="sxs-lookup"><span data-stu-id="c4780-136">Finding a matching field on the site by matching the field names on the site to  **fieldName**.</span></span> <span data-ttu-id="c4780-137">Wenn das Feld bereits vorhanden ist, keine weitere Aktion erforderlich ist und die Steuerung übergeben zurück zur **Hauptseite** , **zurückgeben** aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="c4780-137">If the field already exists, no further action is necessary and control passes back to **Main** when **return** is called.</span></span> <span data-ttu-id="c4780-138">Wenn das Feld nicht vorhanden ist, eine CAML Zeichenfolge zur Angabe des Feldschema **FieldAsXML**zugewiesen ist, und klicken Sie dann wird das Feld mit [FieldCollection.AddFieldAsXml](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldcollection.addfieldasxml.aspx)erstellt.</span><span class="sxs-lookup"><span data-stu-id="c4780-138">If the field does not exist, a CAML string specifying the field schema is assigned to **FieldAsXML**, and then the field is created using [FieldCollection.AddFieldAsXml](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldcollection.addfieldasxml.aspx).</span></span>

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

<span data-ttu-id="c4780-139">Im folgenden Code wird **AddSiteColumnToContentType** eine Verbindung zwischen den Inhaltstyp und das Feld, nach erstellt:</span><span class="sxs-lookup"><span data-stu-id="c4780-139">In the following code,  **AddSiteColumnToContentType** creates a connection between the content type and field by:</span></span>

1. <span data-ttu-id="c4780-140">Laden den Inhaltstyp, und klicken Sie dann die Feldverweise in diesem Inhaltstyp mithilfe der [ContentType.FieldLinks](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.fieldlinks.aspx) -Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="c4780-140">Loading the content type, and then the field references in that content type by using the [ContentType.FieldLinks](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.fieldlinks.aspx) property.</span></span>
    
2. <span data-ttu-id="c4780-141">Laden das Feld.</span><span class="sxs-lookup"><span data-stu-id="c4780-141">Loading the field.</span></span>
    
3. <span data-ttu-id="c4780-142">Bestimmen, ob der Inhaltstyp auf das Feld, mithilfe von verweist **contentType.FieldLinks.Any (f = > f.Name == FieldName)** , der auf der Name des Felds entspricht.</span><span class="sxs-lookup"><span data-stu-id="c4780-142">Determining whether the content type refers to the field by using  **contentType.FieldLinks.Any(f => f.Name == fieldName)** to match on the field name.</span></span>
    
4.  <span data-ttu-id="c4780-143">Wenn der Inhaltstyp bereits auf das Feld verweist, keine weitere Aktion erforderlich ist und die Steuerung übergeben zurück zur **Hauptseite** , **zurückgeben** aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="c4780-143">If the content type refers to the field already, no further action is necessary and control passes back to **Main** when **return** is called.</span></span> <span data-ttu-id="c4780-144">Wenn der Inhaltstyp nicht in das Feld verweist, werden Feldeigenschaften Verweis für ein [FieldLinkCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldlinkcreationinformation.aspx) -Objekt festgelegt.</span><span class="sxs-lookup"><span data-stu-id="c4780-144">If the content type does not refer to the field, field reference properties are set on a [FieldLinkCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldlinkcreationinformation.aspx) object.</span></span>
    
5. <span data-ttu-id="c4780-145">Die **ContentType.FieldLinks** -Eigenschaft hinzugefügt das **FieldLinkCreationInformation** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="c4780-145">Adding the  **FieldLinkCreationInformation** object to the **ContentType.FieldLinks** property.</span></span>

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

<span data-ttu-id="c4780-146">Im folgenden Code überprüft **ReplaceContentType** alle Elemente in allen Bibliotheken für Inhalt, verweist auf den alten Inhaltstyp, und klicken Sie dann ersetzt die Verweise mit den neuen Inhaltstyp (**ContosoDocumentByCSOM**) durch:</span><span class="sxs-lookup"><span data-stu-id="c4780-146">In the following code,  **ReplaceContentType** checks all items in all libraries for content that references the old content type, and then replaces those references with the new content type (**ContosoDocumentByCSOM**) by:</span></span>

1. <span data-ttu-id="c4780-147">Eine Konstante die alten Inhaltstyp-ID zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="c4780-147">Assigning the old content type ID to a constant.</span></span>
    
2. <span data-ttu-id="c4780-148">Abrufen von den neuen Inhaltstyp mithilfe von **GetContentTypeByName**.</span><span class="sxs-lookup"><span data-stu-id="c4780-148">Getting the new content type by using  **GetContentTypeByName**.</span></span>
    
3. <span data-ttu-id="c4780-149">Abrufen von allen Listen auf der Website mithilfe von [Web.Lists](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.lists.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4780-149">Getting all the lists on the site by using [Web.Lists](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.lists.aspx).</span></span>
    
4. <span data-ttu-id="c4780-150">Laden alle Listen auf der Website und alle Inhaltstypen für jede Liste mithilfe von **cc. Load (Listen, l = > l.Include (Liste = > Liste. ContentTypes)**.</span><span class="sxs-lookup"><span data-stu-id="c4780-150">Loading all the lists on the site, and all content types on each list by using  **cc.Load(lists, l => l.Include(list => list.ContentTypes)**.</span></span>
    
5. <span data-ttu-id="c4780-151">Suchen für jede Liste zurückgegebenen Inhaltstypen der Liste, um einen Inhaltstyp mit der alten Inhaltstyp-ID mithilfe von **Liste übereinstimmen. ContentTypes.Any (c = > c.StringId.StartsWith(oldContentTypeId))**.</span><span class="sxs-lookup"><span data-stu-id="c4780-151">For each returned list, searching the list's content types to match a content type with the old content type ID by using  **list.ContentTypes.Any(c => c.StringId.StartsWith(oldContentTypeId))**.</span></span> <span data-ttu-id="c4780-152">Wenn eine Übereinstimmung gefunden wird, wird die Liste mit den alten Inhaltstyp **ListsWithContentType**hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="c4780-152">If a match is found, the list with the old content type is added to **listsWithContentType**.</span></span>
    
6. <span data-ttu-id="c4780-153">Für jede Liste in **ListsWithContentType**:</span><span class="sxs-lookup"><span data-stu-id="c4780-153">For each list in  **listsWithContentType**:</span></span>
    
  1. <span data-ttu-id="c4780-154">Bestimmen, ob der neue Inhaltstyp der Liste zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="c4780-154">Determining whether the new content type is attached to the list.</span></span> <span data-ttu-id="c4780-155">Wenn Sie der neue Inhaltstyp der Liste nicht angeschlossen ist, verwenden Sie [ContentTypeCollection.AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) So fügen Sie den neuen Inhaltstyp der Liste an.</span><span class="sxs-lookup"><span data-stu-id="c4780-155">If the new content type is not attached to the list, use [ContentTypeCollection.AddExistingContentType ](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) to attach the new content type to the list.</span></span>
    
  2. <span data-ttu-id="c4780-156">Abrufen aller Listenelemente in der Liste.</span><span class="sxs-lookup"><span data-stu-id="c4780-156">Getting all list items in the list.</span></span>
    
  3. <span data-ttu-id="c4780-157">Für jedes Listenelement Abrufen von Inhaltstyp-ID des Listenelements.</span><span class="sxs-lookup"><span data-stu-id="c4780-157">For each list item, getting the content type ID of the list item.</span></span> <span data-ttu-id="c4780-158">Bestimmen Sie, ob die Inhaltstyp-ID des Listenelements alte Inhaltstyp-ID entspricht</span><span class="sxs-lookup"><span data-stu-id="c4780-158">Determine whether the content type ID of the list item is equal to the old content type ID.</span></span> <span data-ttu-id="c4780-159">Wenn der Inhaltstyp-IDs nicht gleich sind, fahren Sie mit der nächsten Listenelement.</span><span class="sxs-lookup"><span data-stu-id="c4780-159">If the content type IDs are not equal, skip to the next list item.</span></span> <span data-ttu-id="c4780-160">Wenn der Inhaltstyp-IDs gleich sind, verwenden Sie [ContentType.StringId](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.stringid.aspx) das Element der Liste die neuen Inhaltstyp-ID zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="c4780-160">If the content type IDs are equal, use [ContentType.StringId](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.stringid.aspx) to assign the new content type ID to the list item.</span></span>
    

<span data-ttu-id="c4780-161">**Hinweis:**  Der alte Inhaltstyp ist weiterhin in der Liste, aber er wird nicht mehr verwendet.</span><span class="sxs-lookup"><span data-stu-id="c4780-161">**Note:**  The old content type is still in the list but it is not used anymore.</span></span> <span data-ttu-id="c4780-162">Sie können jetzt den alten Inhaltstyp aus der Liste löschen, und es dann zurückgezogen. In diesem Artikel wird beschrieben, wie nur Dokumentinhaltstypen ersetzen.</span><span class="sxs-lookup"><span data-stu-id="c4780-162">You can now delete the old content type from the lists, and then retract it.This article describes how to replace document content types only.</span></span> <span data-ttu-id="c4780-163">Wenn Sie Inhaltstypen auf Seitenlayouts ersetzen möchten, stellen Sie sicher, dass Sie die [AssociatedContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.publishing.pagelayout.associatedcontenttype.aspx) -Eigenschaft auf jeder Seitenlayout in der Websitesammlung aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="c4780-163">If you are replacing content types on page layouts, ensure you update the [AssociatedContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.publishing.pagelayout.associatedcontenttype.aspx) property on each page layout in the site collection.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="c4780-164">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c4780-164">Additional resources</span></span>
<span data-ttu-id="c4780-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c4780-165"></span></span>

- [<span data-ttu-id="c4780-166">Transformieren von Farmlösungen in das SharePoint-Add-In-Modell</span><span class="sxs-lookup"><span data-stu-id="c4780-166">Transform farm solutions to the SharePoint add-in model</span></span>](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [<span data-ttu-id="c4780-167">SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="c4780-167">SharePoint 2013</span></span>](https://msdn.microsoft.com/library/office/jj162979.aspx)
