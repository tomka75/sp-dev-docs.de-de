---
title: "Dokumentbibliothek Vorlagen Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: ef53fbf5f15a3c82245b2842c1460a7d2dcad5f9
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="document-library-templates-sample-add-in-for-sharepoint"></a>Dokumentbibliothek Vorlagen Beispiel-add-in für SharePoint

Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie implementieren eine benutzerdefinierten Dokumentbibliotheksvorlage und Anpassen von Websitespalten, Websiteinhaltstypen, Taxonomie Felder, versionneinstellungen und den Standardinhaltstyp des Dokuments.
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Die [ECM. DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) Beispiel veranschaulicht, wie ein vom Anbieter gehosteten add-in einer Liste oder Dokumentbibliothek erstellen, weisen Sie einen Inhaltstyp zu, und entfernen den Standardinhaltstyp verwenden. Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:    

- Erstellen einer Liste oder Dokumentbibliothek und eine Standardinhaltstyp anwenden.
    
- Größere Kontrolle über das Hinzufügen, die Wartung oder die Implementierung der lokalisierten Versionen Ihrer benutzerdefinierten Feldern zu bestätigen.
    
- Entfernen Sie den Standardinhaltstyp für eine Liste oder Bibliothek.
    
- Anwenden von Konfigurationseinstellungen Bibliothek beim Erstellen einer Liste oder Bibliothek.

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zunächst die [ECM. DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Benutzern den Zugriff auf dem ECM. DocumentLibraries-add-Ins muss Berechtigungen zum Verwalten von Listen verfügen. Die **DoesUserHavePermission** -Methode in der Datei Default.aspx.cs überprüft die Berechtigungen des Benutzers, um sicherzustellen, dass sie Listen verwalten können. Wenn der Benutzer nicht über Berechtigungen zum Verwalten von Listen verfügt, zeigt eine Fehlermeldung an das Add-in für dem Benutzer.

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

## <a name="using-the-ecmdocumentlibraries-sample-add-in"></a>Verwenden die ECM. DocumentLibraries Beispiel-add-in 
<a name="sectionSection1"> </a>

Wenn Sie dieses Add-in starten, zeigt die Startseite wie in Abbildung 1 dargestellt. Die ECM. DocumentLibraries starten Seite sieht wie folgt aus der Seite, um eine neue Dokumentbibliothek hinzufügen, wenn Sie **Websiteinhalte**auswählen > **app hinzufügen** > **Dokumentbibliothek** > **Erweiterte Optionen** – mit einem Unterschied. Wenn Sie das Add-in starten, zeigt der Dokumentvorlage Dropdown-Liste benutzerdefinierter Dokumentbibliotheksvorlage, IT-Dokument und Contoso-Dokument. Wenn der Benutzer **Erstellen**, wird die neue Dokumentbibliothek der ausgewählte benutzerdefinierte Inhaltstyp zugewiesen. 

** Abbildung 1. Startseite des der ECM. DocumentLibraries-add-Ins **

![Screenshot, der die ECM anzeigt. Starten Seite DocumentLibraries-add-in mit einer Dokumentvorlage Dropdown-Listenfeld, die IT-Dokument als Option aufgelistet.](media/d58b9d12-808e-4f2b-9065-31e6d735dbaa.png)

Wenn Benutzer **Erstellen**auswählen, überprüft die ausgewählten Standardvorlage und Aufrufe an die **CreateITDocumentLibrary** oder **CreateContosoDocumentLibrary** -Methode in die **CreateLibrary_Click** -Methode in "default.aspx.cs" ContentTypeManager.cs, wie im folgenden Code dargestellt.
    
**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.

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

Die **CreateContosoDocumentLibrary** -Methode führt dann die folgenden Aufgaben wie das nächste Codebeispiel gezeigt:

1. Benutzerdefinierte Felder erstellt in den verwalteten Metadatendienst.
    
2. Erstellt einen Inhaltstyp an. 
    
3. Ordnet die benutzerdefinierten Felder die Inhaltstypen.
    
4. Die Dokumentbibliothek erstellt mit der Inhaltstyp.

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

**CreateContosoDocumentLibrary** Ruft die **CreateTaxonomyField** -Methode, die Teil der OfficeDevPnP.Core ist. **CreateTaxonomyField** erstellt ein Feld in den verwalteten Metadatendienst vom Anbieter gehostete-add-in.

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

**CreateContosoDocumentLibrary** Ruft die **CreateContentType** -Methode, die Teil des OfficeDevPnP.Core ist. **CreateContentType** erstellt einen neuen Inhaltstyp.

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

**CreateContosoDocumentLibrary** Ruft die **AddFieldToContentTypeById** -Methode, die OfficeDevPnP.Core gehört. **AddFieldToContentTypeById** ordnet einem Inhaltstyp ein Feld.

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

**CreateContosoDocumentLibrary** Ruft die **CreateLibrary** -Methode im ContentTypeManager.cs, um die Dokumentbibliothek zu erstellen. Die **CreateLibrary** -Methode weist bibliothekeinstellungen wie Beschreibung, dokumentversionierung und zugeordneten Inhaltstypen der Dokumentbibliothek.

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

**CreateLibrary** ruft **RemoveContentTypeByName** in ListExtensions.cs, der Teil des OfficeDevPnP.Core ist. **RemoveContentTypeByName** entfernt den Standardinhaltstyp der Dokumentbibliothek.

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

Nachdem Sie die Dokumentbibliothek erstellt haben, wechseln Sie zum die **in der Formularbibliothek** auf Ihre Dokumentbibliothek zum Überprüfen der Name, Beschreibung, dokumentieren Sie Versioning, Inhaltstyp und benutzerdefinierte Felder des Add-Ins zu Ihrer Dokumentbibliothek zugewiesen.

** Abbildung 2. In der Formularbibliothek angewendet, indem Sie das Add-in **

![Screenshot der Seite Dokumentbibliothekseinstellungen mit Name, Beschreibung und Webadresse Feldern hervorgehoben.](media/aedf5107-bacb-4872-8ad4-8e66b1afead8.png)

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [ECM. Autotagging Beispiel-app](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.Autotagging)
