---
title: "Dokumentbibliothek Vorlagen Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: ef53fbf5f15a3c82245b2842c1460a7d2dcad5f9
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="document-library-templates-sample-add-in-for-sharepoint"></a><span data-ttu-id="20289-102">Dokumentbibliothek Vorlagen Beispiel-add-in für SharePoint</span><span class="sxs-lookup"><span data-stu-id="20289-102">Document library templates sample add-in for SharePoint</span></span>

<span data-ttu-id="20289-103">Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie implementieren eine benutzerdefinierten Dokumentbibliotheksvorlage und Anpassen von Websitespalten, Websiteinhaltstypen, Taxonomie Felder, versionneinstellungen und den Standardinhaltstyp des Dokuments.</span><span class="sxs-lookup"><span data-stu-id="20289-103">As part of your Enterprise Content Management (ECM) strategy, you can implement a custom document library template, and customize site columns, site content types, taxonomy fields, version settings, and the default document content type.</span></span>
    
<span data-ttu-id="20289-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="20289-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="20289-105">Die [ECM. DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) Beispiel veranschaulicht, wie ein vom Anbieter gehosteten add-in einer Liste oder Dokumentbibliothek erstellen, weisen Sie einen Inhaltstyp zu, und entfernen den Standardinhaltstyp verwenden.</span><span class="sxs-lookup"><span data-stu-id="20289-105">The [ECM.DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) sample shows you how to use a provider-hosted add-in to create a list or document library, assign a content type to it, and remove the default content type.</span></span> <span data-ttu-id="20289-106">Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:</span><span class="sxs-lookup"><span data-stu-id="20289-106">Use this solution if you want to:</span></span>    

- <span data-ttu-id="20289-107">Erstellen einer Liste oder Dokumentbibliothek und eine Standardinhaltstyp anwenden.</span><span class="sxs-lookup"><span data-stu-id="20289-107">Create a list or document library and apply a default content type.</span></span>
    
- <span data-ttu-id="20289-108">Größere Kontrolle über das Hinzufügen, die Wartung oder die Implementierung der lokalisierten Versionen Ihrer benutzerdefinierten Feldern zu bestätigen.</span><span class="sxs-lookup"><span data-stu-id="20289-108">Assert greater control over the addition, maintenance, or implementation of localized versions of your custom fields.</span></span>
    
- <span data-ttu-id="20289-109">Entfernen Sie den Standardinhaltstyp für eine Liste oder Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="20289-109">Remove the default content type on a list or library.</span></span>
    
- <span data-ttu-id="20289-110">Anwenden von Konfigurationseinstellungen Bibliothek beim Erstellen einer Liste oder Bibliothek.</span><span class="sxs-lookup"><span data-stu-id="20289-110">Apply library configuration settings when you create a list or library.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="20289-111">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="20289-111">Before you begin</span></span>
<span data-ttu-id="20289-112"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="20289-112"></span></span>

<span data-ttu-id="20289-113">Laden Sie Sie zunächst die [ECM. DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="20289-113">To get started, download the  [ECM.DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="20289-114">Benutzern den Zugriff auf dem ECM. DocumentLibraries-add-Ins muss Berechtigungen zum Verwalten von Listen verfügen.</span><span class="sxs-lookup"><span data-stu-id="20289-114">Users accessing the ECM.DocumentLibraries add-in must have permissions to manage lists.</span></span> <span data-ttu-id="20289-115">Die **DoesUserHavePermission** -Methode in der Datei Default.aspx.cs überprüft die Berechtigungen des Benutzers, um sicherzustellen, dass sie Listen verwalten können.</span><span class="sxs-lookup"><span data-stu-id="20289-115">The  **DoesUserHavePermission** method in Default.aspx.cs checks the user's permissions to ensure they can manage lists.</span></span> <span data-ttu-id="20289-116">Wenn der Benutzer nicht über Berechtigungen zum Verwalten von Listen verfügt, zeigt eine Fehlermeldung an das Add-in für dem Benutzer.</span><span class="sxs-lookup"><span data-stu-id="20289-116">If the user does not have permissions to manage lists, the add-in presents an error message to the user.</span></span>

```C#
private bool DoesUserHavePermission()
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var ctx = spContext.CreateUserClientContextForSPHost())
            {
                BasePermissions perms = new BasePermissions();
                perms.Set(PermissionKind.ManageLists);
                ClientResult<bool> _permResult = ctx.Web.DoesUserHavePermissions(perms);
                ctx.ExecuteQuery();
                return _permResult.Value;
            }
        }

```

## <a name="using-the-ecmdocumentlibraries-sample-add-in"></a><span data-ttu-id="20289-117">Verwenden die ECM. DocumentLibraries Beispiel-add-in</span><span class="sxs-lookup"><span data-stu-id="20289-117">Using the ECM.DocumentLibraries sample add-in</span></span> 
<span data-ttu-id="20289-118"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="20289-118"></span></span>

<span data-ttu-id="20289-119">Wenn Sie dieses Add-in starten, zeigt die Startseite wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="20289-119">When you start this add-in , the start page displays as shown in Figure 1.</span></span> <span data-ttu-id="20289-120">Die ECM. DocumentLibraries starten Seite sieht wie folgt aus der Seite, um eine neue Dokumentbibliothek hinzufügen, wenn Sie **Websiteinhalte**auswählen > **app hinzufügen** > **Dokumentbibliothek** > **Erweiterte Optionen** – mit einem Unterschied.</span><span class="sxs-lookup"><span data-stu-id="20289-120">The ECM.DocumentLibraries start page looks like the page to add a new document library when you select  **Site Contents** > **add an app** > **Document Library** > **Advanced Options** - with one difference.</span></span> <span data-ttu-id="20289-121">Wenn Sie das Add-in starten, zeigt der Dokumentvorlage Dropdown-Liste benutzerdefinierter Dokumentbibliotheksvorlage, IT-Dokument und Contoso-Dokument.</span><span class="sxs-lookup"><span data-stu-id="20289-121">When you start the add-in , the Document Template dropdown list displays custom document library template, IT Document and Contoso Document.</span></span> <span data-ttu-id="20289-122">Wenn der Benutzer **Erstellen**, wird die neue Dokumentbibliothek der ausgewählte benutzerdefinierte Inhaltstyp zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="20289-122">When the user chooses **Create**, the selected custom content type is assigned to the new document library.</span></span> 

<span data-ttu-id="20289-123">** Abbildung 1.</span><span class="sxs-lookup"><span data-stu-id="20289-123">**Figure 1.</span></span> <span data-ttu-id="20289-124">Startseite des der ECM. DocumentLibraries-add-Ins **</span><span class="sxs-lookup"><span data-stu-id="20289-124">Start page of the ECM.DocumentLibraries add-in **</span></span>

![Screenshot, der die ECM anzeigt. Starten Seite DocumentLibraries-add-in mit einer Dokumentvorlage Dropdown-Listenfeld, die IT-Dokument als Option aufgelistet.](media/d58b9d12-808e-4f2b-9065-31e6d735dbaa.png)

<span data-ttu-id="20289-126">Wenn Benutzer **Erstellen**auswählen, überprüft die ausgewählten Standardvorlage und Aufrufe an die **CreateITDocumentLibrary** oder **CreateContosoDocumentLibrary** -Methode in die **CreateLibrary_Click** -Methode in "default.aspx.cs" ContentTypeManager.cs, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="20289-126">When users choose  **Create**, the  **CreateLibrary_Click** method in Default.aspx.cs checks the selected default template and makes calls to either the **CreateITDocumentLibrary** or **CreateContosoDocumentLibrary** method in ContentTypeManager.cs, as shown in the following code.</span></span>
    
<span data-ttu-id="20289-127">**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="20289-127">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
protected void CreateLibrary_Click(object sender, EventArgs e)
        {
            try
            {
                var _spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
                var _templateSelectedItem = this.DocumentTemplateType.Value;
                var _libraryToCreate = this.GetLibraryToCreate();
                using (var _ctx = _spContext.CreateUserClientContextForSPHost())
                {
                    
                    _ctx.ApplicationName = "AMS ECM.DocumentLibraries";
                    ContentTypeManager _manager = new ContentTypeManager();
                    switch(_templateSelectedItem)
                    {
                        case "IT Document":
                            _manager.CreateITDocumentLibrary(_ctx, _libraryToCreate);
                            break;
                        case "Contoso Document":
                            _manager.CreateContosoDocumentLibrary(_ctx, _libraryToCreate);
                            break;
                    }
                 }

                Response.Redirect(this.Url.Value);
            }
            catch (Exception _ex)
            {
                throw;
            }
        }

```

<span data-ttu-id="20289-128">Die **CreateContosoDocumentLibrary** -Methode führt dann die folgenden Aufgaben wie das nächste Codebeispiel gezeigt:</span><span class="sxs-lookup"><span data-stu-id="20289-128">The  **CreateContosoDocumentLibrary** method then performs the following tasks, as shown in the next code example:</span></span>

1. <span data-ttu-id="20289-129">Benutzerdefinierte Felder erstellt in den verwalteten Metadatendienst.</span><span class="sxs-lookup"><span data-stu-id="20289-129">Creates custom fields in the Managed Metadata Service.</span></span>
    
2. <span data-ttu-id="20289-130">Erstellt einen Inhaltstyp an.</span><span class="sxs-lookup"><span data-stu-id="20289-130">Creates a content type.</span></span> 
    
3. <span data-ttu-id="20289-131">Ordnet die benutzerdefinierten Felder die Inhaltstypen.</span><span class="sxs-lookup"><span data-stu-id="20289-131">Associates the custom fields with the content types.</span></span>
    
4. <span data-ttu-id="20289-132">Die Dokumentbibliothek erstellt mit der Inhaltstyp.</span><span class="sxs-lookup"><span data-stu-id="20289-132">Creates the document library with the content type.</span></span>

```C#
        public void CreateContosoDocumentLibrary(ClientContext ctx, Library library)
        {
            // Check the fields.
            if (!ctx.Web.FieldExistsById(FLD_CLASSIFICATION_ID)){
                ctx.Web.CreateTaxonomyField(FLD_CLASSIFICATION_ID, 
                                            FLD_CLASSIFICATION_INTERNAL_NAME, 
                                            FLD_CLASSIFICATION_DISPLAY_NAME, 
                                            FIELDS_GROUP_NAME, 
                                            TAXONOMY_GROUP, 
                                            TAXONOMY_TERMSET_CLASSIFICATION_NAME);
            }
            
            // Check the content type.
            if (!ctx.Web.ContentTypeExistsById(CONTOSODOCUMENT_CT_ID)){
                ctx.Web.CreateContentType(CONTOSODOCUMENT_CT_NAME, 
                                          CT_DESC, CONTOSODOCUMENT_CT_ID, 
                                          CT_GROUP);
            }

            // Associate fields to content types.
            if (!ctx.Web.FieldExistsByNameInContentType(CONTOSODOCUMENT_CT_NAME, FLD_CLASSIFICATION_INTERNAL_NAME)){
                ctx.Web.AddFieldToContentTypeById(CONTOSODOCUMENT_CT_ID, 
                                                  FLD_CLASSIFICATION_ID.ToString(), 
                                                  false);
            }
            CreateLibrary(ctx, library, CONTOSODOCUMENT_CT_ID);
          
        }

```

<span data-ttu-id="20289-133">**CreateContosoDocumentLibrary** Ruft die **CreateTaxonomyField** -Methode, die Teil der OfficeDevPnP.Core ist.</span><span class="sxs-lookup"><span data-stu-id="20289-133">**CreateContosoDocumentLibrary** calls the **CreateTaxonomyField** method, which is part of the OfficeDevPnP.Core.</span></span> <span data-ttu-id="20289-134">**CreateTaxonomyField** erstellt ein Feld in den verwalteten Metadatendienst vom Anbieter gehostete-add-in.</span><span class="sxs-lookup"><span data-stu-id="20289-134">**CreateTaxonomyField** creates a field in the managed metadata service from the provider-hosted add-in .</span></span>

```C#
public static Field CreateTaxonomyField(this Web web, Guid id, string internalName, string displayName, string group, TermSet termSet, bool multiValue = false)
        {
            internalName.ValidateNotNullOrEmpty("internalName");
            displayName.ValidateNotNullOrEmpty("displayName");
            termSet.ValidateNotNullOrEmpty("termSet");

            try
            {
                var _field = web.CreateField(id, internalName, multiValue ? "TaxonomyFieldTypeMulti" : "TaxonomyFieldType", true, displayName, group, "ShowField=\"Term1033\"");

                WireUpTaxonomyField(web, _field, termSet, multiValue);
                _field.Update();

                web.Context.ExecuteQuery();

                return _field;
            }
            catch (Exception)
            {
                /// If there is an exception, the hidden field might be present.
                FieldCollection _fields = web.Fields;
                web.Context.Load(_fields, fc => fc.Include(f => f.Id, f => f.InternalName));
                web.Context.ExecuteQuery();
                var _hiddenField = id.ToString().Replace("-", "");

                var _field = _fields.FirstOrDefault(f => f.InternalName == _hiddenField);
                if (_field != null)
                {
                    _field.DeleteObject();
                    web.Context.ExecuteQuery();
                }
                throw;

            }
        }
```

<span data-ttu-id="20289-135">**CreateContosoDocumentLibrary** Ruft die **CreateContentType** -Methode, die Teil des OfficeDevPnP.Core ist.</span><span class="sxs-lookup"><span data-stu-id="20289-135">**CreateContosoDocumentLibrary** calls the **CreateContentType** method which is part of OfficeDevPnP.Core.</span></span> <span data-ttu-id="20289-136">**CreateContentType** erstellt einen neuen Inhaltstyp.</span><span class="sxs-lookup"><span data-stu-id="20289-136">**CreateContentType** creates a new content type.</span></span>

```C#
public static ContentType CreateContentType(this Web web, string name, string description, string id, string group, ContentType parentContentType = null)
        {
            LoggingUtility.Internal.TraceInformation((int)EventId.CreateContentType, CoreResources.FieldAndContentTypeExtensions_CreateContentType01, name, id);

            // Load the current collection of content types.
            ContentTypeCollection contentTypes = web.ContentTypes;
            web.Context.Load(contentTypes);
            web.Context.ExecuteQuery();
            ContentTypeCreationInformation newCt = new ContentTypeCreationInformation();

            // Set the properties for the content type.
            newCt.Name = name;
            newCt.Id = id;
            newCt.Description = description;
            newCt.Group = group;
            newCt.ParentContentType = parentContentType;
            ContentType myContentType = contentTypes.Add(newCt);
            web.Context.ExecuteQuery();

            // Return the content type object.
            return myContentType;
        }

```

<span data-ttu-id="20289-137">**CreateContosoDocumentLibrary** Ruft die **AddFieldToContentTypeById** -Methode, die OfficeDevPnP.Core gehört.</span><span class="sxs-lookup"><span data-stu-id="20289-137">**CreateContosoDocumentLibrary** calls the **AddFieldToContentTypeById** method, which is part of OfficeDevPnP.Core.</span></span> <span data-ttu-id="20289-138">**AddFieldToContentTypeById** ordnet einem Inhaltstyp ein Feld.</span><span class="sxs-lookup"><span data-stu-id="20289-138">**AddFieldToContentTypeById** associates a field with a content type.</span></span>

```C#
public static void AddFieldToContentTypeById(this Web web, string contentTypeID, string fieldID, bool required = false, bool hidden = false)
        {
            // Get content type.
            ContentType ct = web.GetContentTypeById(contentTypeID);
            web.Context.Load(ct);
            web.Context.Load(ct.FieldLinks);
            web.Context.ExecuteQuery();

            // Get field.
            Field fld = web.Fields.GetById(new Guid(fieldID));

            // Add field association to content type.
            AddFieldToContentType(web, ct, fld, required, hidden);
        }
```

<span data-ttu-id="20289-139">**CreateContosoDocumentLibrary** Ruft die **CreateLibrary** -Methode im ContentTypeManager.cs, um die Dokumentbibliothek zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="20289-139">**CreateContosoDocumentLibrary** calls the **CreateLibrary** method in ContentTypeManager.cs to create the document library.</span></span> <span data-ttu-id="20289-140">Die **CreateLibrary** -Methode weist bibliothekeinstellungen wie Beschreibung, dokumentversionierung und zugeordneten Inhaltstypen der Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="20289-140">The **CreateLibrary** method assigns library settings such as the document library's description, document versioning, and associated content types.</span></span>

```C#
private void CreateLibrary(ClientContext ctx, Library library, string associateContentTypeID)
        {
            if (!ctx.Web.ListExists(library.Title))
            {
                ctx.Web.AddList(ListTemplateType.DocumentLibrary, library.Title, false);
                List _list = ctx.Web.GetListByTitle(library.Title);
                if(!string.IsNullOrEmpty(library.Description)) {
                    _list.Description = library.Description;
                }

                if(library.VerisioningEnabled) {
                    _list.EnableVersioning = true;
                }

                _list.ContentTypesEnabled = true;
                _list.Update();
                ctx.Web.AddContentTypeToListById(library.Title, associateContentTypeID, true);
                // Remove the default Document Content Type.
                _list.RemoveContentTypeByName(ContentTypeManager.DEFAULT_DOCUMENT_CT_NAME);
                ctx.Web.Context.ExecuteQuery();
            }
            else
            {
                throw new Exception("A list, survey, discussion board, or document library with the specified title already exists in this Web site.  Please choose another title.");
            }
        }
```

<span data-ttu-id="20289-141">**CreateLibrary** ruft **RemoveContentTypeByName** in ListExtensions.cs, der Teil des OfficeDevPnP.Core ist.</span><span class="sxs-lookup"><span data-stu-id="20289-141">**CreateLibrary** calls **RemoveContentTypeByName** in ListExtensions.cs, which is part of OfficeDevPnP.Core.</span></span> <span data-ttu-id="20289-142">**RemoveContentTypeByName** entfernt den Standardinhaltstyp der Dokumentbibliothek.</span><span class="sxs-lookup"><span data-stu-id="20289-142">**RemoveContentTypeByName** removes the default content type on the document library.</span></span>

```C#
        public static void RemoveContentTypeByName(this List list, string contentTypeName)
        {
            if (string.IsNullOrEmpty(contentTypeName))
            {
                throw (contentTypeName == null)
                  ? new ArgumentNullException("contentTypeName")
                  : new ArgumentException(CoreResources.Exception_Message_EmptyString_Arg, "contentTypeName");
            }

            ContentTypeCollection _cts = list.ContentTypes;
            list.Context.Load(_cts);

            IEnumerable<ContentType> _results = list.Context.LoadQuery<ContentType>(_cts.Where(item => item.Name == contentTypeName));
            list.Context.ExecuteQuery();

            ContentType _ct = _results.FirstOrDefault();
            if (_ct != null)
            {
                _ct.DeleteObject();
                list.Update();
                list.Context.ExecuteQuery();
            }
        }
```

<span data-ttu-id="20289-143">Nachdem Sie die Dokumentbibliothek erstellt haben, wechseln Sie zum die **in der Formularbibliothek** auf Ihre Dokumentbibliothek zum Überprüfen der Name, Beschreibung, dokumentieren Sie Versioning, Inhaltstyp und benutzerdefinierte Felder des Add-Ins zu Ihrer Dokumentbibliothek zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="20289-143">After you create the document library, go to the  **Library settings** on your document library to review the name, description, document versioning setting, content type, and custom fields the add-in assigned to your document library.</span></span>

<span data-ttu-id="20289-144">** Abbildung 2.</span><span class="sxs-lookup"><span data-stu-id="20289-144">**Figure 2.</span></span> <span data-ttu-id="20289-145">In der Formularbibliothek angewendet, indem Sie das Add-in **</span><span class="sxs-lookup"><span data-stu-id="20289-145">Library settings applied by the add-in **</span></span>

![Screenshot der Seite Dokumentbibliothekseinstellungen mit Name, Beschreibung und Webadresse Feldern hervorgehoben.](media/aedf5107-bacb-4872-8ad4-8e66b1afead8.png)

## <a name="additional-resources"></a><span data-ttu-id="20289-147">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="20289-147">Additional resources</span></span>
<span data-ttu-id="20289-148"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="20289-148"></span></span>

-  [<span data-ttu-id="20289-149">Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="20289-149">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="20289-150">ECM. Autotagging Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="20289-150">ECM.Autotagging sample app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.Autotagging)
