---
title: "Autotagging Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 6b210688ddd9082a1199cacf0c75cc2401137ccc
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="autotagging-sample-add-in-for-sharepoint"></a>Autotagging Beispiel-add-in für SharePoint

Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie automatisch Markieren von Dokumenten mit Metadaten wenn sie erstellt oder in SharePoint hochgeladen werden. 
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Die [ECM. AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) Beispiel zeigt, wie Sie eine vom Anbieter gehosteten add-in, automatisch Inhalt des Tags, einer SharePoint-Bibliothek mit Daten aus einer benutzerdefinierten Benutzerprofileigenschaft stammende hinzugefügt wurde. Dieses Add-in verwendet remote-Ereignisempfänger, gehostet auf einer Azure-Website an:   

- Felder, Inhaltstypen und Dokumentbibliotheken zu erstellen.
    
- Rufen Sie den Wert einer benutzerdefinierten Profileigenschaft.
    
- Festlegen Sie Taxonomie Felder.
    
Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:

- Implementieren von Ereignisempfängern in SharePoint Online. 
    
- Verbessern der Suchergebnisse durch Anfügen von zusätzliche Metadaten zum Inhalt erstellt wird.
    
- Klassifizieren von Inhalten.
    
- Modernisieren Code vor der Migration zu einer neueren Version von SharePoint, und Sie in der Vergangenheit Ereignisempfänger verwendet haben.
    
## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zunächst die [ECM. AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Vor dem Ausführen dieses Add-in führen Sie die folgenden Schritte aus:

1. Erstellen einer Azure-Website und die ECM bereitstellen. AutoTaggingWeb-Projekt hinzu.
    
2. Registrieren Sie Ihr Add-in über die Seite "appregnew.aspx" in Office 365. 
    
3. Dieses Add-In wird nur-app-Berechtigungen verwendet. Sie müssen nur-app-Berechtigungen, die über die Seite "appinv.aspx" in Office 365 zuweisen. Kopieren Sie den folgenden XML-Code aus der Datei AppManifest.XML in die Berechtigung anfordern XML TextBox-Steuerelement auf der Seite "appinv.aspx", wie in Abbildung 1 dargestellt. 

    ``` 
      <AppPermissionRequests AllowAppOnlyPolicy="true">
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
        <AppPermissionRequest Scope="http://sharepoint/taxonomy" Right="Read" />
        <AppPermissionRequest Scope="http://sharepoint/social/tenant" Right="Read" />
      </AppPermissionRequests>
    ```

    **Abbildung 1. Zuweisen von nur-app-Berechtigungen mithilfe der Seite "appinv.aspx" in Office 365**

    ![Screenshot der Seite "appinv.aspx" mit den Feldern App-ID und die Berechtigung anfordern XML hervorgehoben](media/d733e2b0-55f3-4aee-872b-49e7e2baf470.png)

4. In der ECM. AutoTaggingWeb-Projekt, in der Datei ReceiverHelper.cs, in der Methode **CreateEventReciever** aktualisieren die **ReceiverUrl** -Eigenschaft mit der URL von der Azure-Website.

    ```C#
        public static EventReceiverDefinitionCreationInformation CreateEventReciever(string receiverName, EventReceiverType type)
            {
    
                EventReceiverDefinitionCreationInformation _rer = new EventReceiverDefinitionCreationInformation();
                _rer.EventType = type;
                _rer.ReceiverName = receiverName;
                _rer.ReceiverClass = "ECM.AutoTaggingWeb.Services.AutoTaggingService";
                _rer.ReceiverUrl = "https://<Your domain>.azurewebsites.net/Services/AutoTaggingService.svc";
                _rer.Synchronization = EventReceiverSynchronization.Synchronous;
                return _rer;
            }
    
    ```
5. Packen Sie und Bereitstellen Sie Ihrer add-Ins. 
    
Beim Starten Sie das Add-in, die Startseite des Dokuments Autotagging vom Anbieter gehosteten-Add-in angezeigt, wie in Abbildung 2 dargestellt. Die Startseite zeigt zusätzliche Konfigurationsschritte, dass Sie vor dem zuweisen oder Entfernen von Ereignisempfängern ausgeführt werden müssen. 

**Abbildung 2. Zusätzliche Konfigurationsschritte erforderlich, um auf der Startseite in SharePoint ausgeführt werden**

![Screenshot des Autotagging-add-Ins der Startseite mit drei Einrichtungsschritte hervorgehoben.](media/eb0521b2-11e2-4c57-8026-d7e838c21eae.png)

## <a name="using-the-ecmautotagging-sample-add-in"></a>Verwenden die ECM. Autotagging Beispiel-add-in 
<a name="sectionSection1"> </a>

In diesem Beispiel wird einen remote-Ereignisempfänger automatisch Tag (Metadaten hinzufügen) Profileigenschaft Dokumente, die in einer Dokumentbibliothek, mit der Daten von einem benutzerdefinierten Benutzer hinzugefügt werden. Der Prozessfluss für Autotagging Dokumente mithilfe des remote-Ereignisempfängers wird in Abbildung 3 dargestellt.

**Abbildung 3. Prozessfluss zum Markieren von Dokumenten in einer Dokumentbibliothek mithilfe eines remoteereignisempfängers**

![Abbildung des Prozesses zum Markieren von einem Dokument in einer Bibliothek. Wenn der Benutzer auf Inhalte erstellt, kontaktiert das Add-in den Ereignisempfänger, die greift auf das Profil des Benutzers und sendet die Informationen in SharePoint.](media/430eee99-5ab9-49d8-8021-71d7cee79a73.png)

Zuweisen von Metadaten für das neu erstellte Dokument in der Dokumentbibliothek mithilfe eines remoteereignisempfängers

1. Ein Benutzer erstellt oder neuen Inhalte in einer Dokumentbibliothek hochgeladen. Ein remote-Ereignisempfänger zugeordnet ist, **ItemAdding** oder **ItemAdded** Ereignisse in dieser Dokumentbibliothek behandelt.
    
2. Die **ItemAdding** oder **ItemAdded** -Methode führt einen Aufruf an den Ereignisempfänger entfernen.
    
3. Das Add-in vom Anbieter gehosteten Ruft den Wert einer benutzerdefinierten Profileigenschaft in der User Profile Service von SharePoint für diesen Benutzer. In diesem Beispiel-add-in wird die Klassifizierung benutzerdefinierte Benutzerprofileigenschaft, die zuvor hinzugefügten abgerufen.
    
4. Der remote-Ereignisempfänger aktualisiert die Metadaten für das neue Dokument mit dem Wert des benutzerdefinierten Benutzerprofileigenschaft für diesen Benutzer. 

### <a name="run-scenario-1"></a>Führen Sie Szenario 1

Wenn Sie die Schaltfläche **Führen Sie Szenario 1**geklickt haben, führt das Add-in Folgendes aus:

1. Erstellt eine Dokumentbibliothek.
    
2. Den remote-Ereignisempfänger für das ItemAdding-Ereignis erstellt.
    
    **Hinweis**  Dieser Artikel beschreibt den Ereignistyp Empfänger ItemAdding. Im Allgemeinen führt eine höhere Leistung als das ItemAdded-Ereignisempfängertyp der Ereignistyp Empfänger ItemAdding. Die ECM. Autotagging Beispiel stellt Code für die ItemAdding und die ItemAdded-Ereignis Receiver Typen bereit.

3. Fügt den remote-Ereignisempfänger in die Dokumentbibliothek.
    
Der folgende Code in die **btnScenario1_Click** -Methode der Seite "default.aspx.cs" in der ECM. AutoTaggingWeb-Projekt zeigt diese Schritte.

**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.

```C#
protected void btnScenario1_Click(object sender, EventArgs e)
        {
            var _libraryToCreate = this.GetLibaryInformationItemAdding();
 
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var ctx = spContext.CreateUserClientContextForSPHost())
            {
                try 
                { 
                    if(!ctx.Web.ListExists(_libraryToCreate.Title))
                    {
                        ScenarioHandler _scenario = new ScenarioHandler();
                        _scenario.CreateContosoDocumentLibrary(ctx, _libraryToCreate);
                    }
                    List _list = ctx.Web.Lists.GetByTitle(_libraryToCreate.Title);
                    EventReceiverDefinitionCreationInformation _rec = ReceiverHelper.CreateEventReciever(ScenarioHandler.AUTOTAGGING_ITEM_ADDING_RERNAME, EventReceiverType.ItemAdding);
                    ReceiverHelper.AddEventReceiver(ctx, _list, _rec);
                }
                catch(Exception _ex)
                {

                }
            }
        }  
```

Die **CreateContosoDocumentLibrary** -Methode ist aufgerufen. Der folgende Code in der Datei ScenarioHandler.cs werden Methoden von OfficeDevPnP.Core zum Erstellen einer benutzerdefinierten Dokumentbibliothek mit einem benutzerdefinierten Inhaltstyp verwendet. Der Standard-Inhaltstyp in der Dokumentbibliothek wurde entfernt.

```C#
public void CreateContosoDocumentLibrary(ClientContext ctx, Library library)
        {
            // Check the fields.
            if (!ctx.Web.FieldExistsById(FLD_CLASSIFICATION_ID))
            {
                ctx.Web.CreateTaxonomyField(FLD_CLASSIFICATION_ID,
                                            FLD_CLASSIFICATION_INTERNAL_NAME,
                                            FLD_CLASSIFICATION_DISPLAY_NAME,
                                            FIELDS_GROUP_NAME,
                                            TAXONOMY_GROUP,
                                            TAXONOMY_TERMSET_CLASSIFICATION_NAME);
            }

            // Check the content type.
            if (!ctx.Web.ContentTypeExistsById(CONTOSODOCUMENT_CT_ID))
            {
                ctx.Web.CreateContentType(CONTOSODOCUMENT_CT_NAME,
                                          CT_DESC, CONTOSODOCUMENT_CT_ID,
                                          CT_GROUP);
            }

            // Associate fields to content types.
            if (!ctx.Web.FieldExistsByNameInContentType(CONTOSODOCUMENT_CT_NAME, FLD_CLASSIFICATION_INTERNAL_NAME))
            {
                ctx.Web.AddFieldToContentTypeById(CONTOSODOCUMENT_CT_ID,
                                                  FLD_CLASSIFICATION_ID.ToString(),
                                                  false);
            }

            
            CreateLibrary(ctx, library, CONTOSODOCUMENT_CT_ID);
        }

private void CreateLibrary(ClientContext ctx, Library library, string associateContentTypeID)
        {
            if (!ctx.Web.ListExists(library.Title))
            {
                ctx.Web.AddList(ListTemplateType.DocumentLibrary, library.Title, false);
                List _list = ctx.Web.GetListByTitle(library.Title);
                if (!string.IsNullOrEmpty(library.Description))
                {
                    _list.Description = library.Description;
                }

                if (library.VerisioningEnabled)
                {
                    _list.EnableVersioning = true;
                }

                _list.ContentTypesEnabled = true;
                _list.RemoveContentTypeByName("Document");
                _list.Update();
                
     
                ctx.Web.AddContentTypeToListById(library.Title, associateContentTypeID, true);
                ctx.Web.Context.ExecuteQuery();
               
            }
            else
            {
                throw new Exception("A list, survey, discussion board, or document library with the specified title already exists in this Web site.  Please choose another title.");
            }
        }
```

Nach Ausführung dieses Codes wird die Dokumentbibliothek AutoTaggingSampleItemAdding in Websiteinhalte, erstellt, wie in Abbildung 4 dargestellt.

**Abbildung 4. AutoTaggingSampleItemAdding-Dokumentbibliothek**

![Screenshot Shwoing der Seite Websiteinhalte mit der neuen AutoTaggingSampleItemAdd-Dokumentbibliothek.](media/8820a44f-8df8-4c80-aeaa-e50c37b8912c.png)

In der ECM. AutoTaggingWeb-Projekt erstellt die ItemAdding-ereignisempfängerdefinition in der Datei ReceiverHelper.cs, die **CreateEventReciever** -Methode. In der ECM. AutoTaggingWeb-Projekt, der Ordner Services enthält einen Webdienst mit dem Namen AutoTaggingService.svc. Wenn Sie die ECM veröffentlicht haben. AutoTaggingWeb Projekt zu Ihrer Azure-Website, diesen Webdienst wurde auch auf Ihrer Website bereitgestellt. Die **CreateEventReciever** -Methode weist diesen Webdienst als der remote-Ereignisempfänger in der Dokumentbibliothek. Der folgende Code aus der **CreateEventReciever** -Methode veranschaulicht, wie der remote-Ereignisempfänger den Webdienst zugewiesen.

```C#
public static EventReceiverDefinitionCreationInformation CreateEventReciever(string receiverName, EventReceiverType type)
        {

            EventReceiverDefinitionCreationInformation _rer = new EventReceiverDefinitionCreationInformation();
            _rer.EventType = type;
            _rer.ReceiverName = receiverName;
            _rer.ReceiverClass = "ECM.AutoTaggingWeb.Services.AutoTaggingService";
            _rer.ReceiverUrl = "https://<Your domain>.azurewebsites.net/Services/AutoTaggingService.svc";
            _rer.Synchronization = EventReceiverSynchronization.Synchronous;
            return _rer;
        }

```

Der folgende Code aus der **AddEventReceiver** -Methode weist den remote-Ereignisempfänger zu der Dokumentbibliothek.

```C#
public static void AddEventReceiver(ClientContext ctx, List list, EventReceiverDefinitionCreationInformation eventReceiverInfo)
        {
            if (!DoesEventReceiverExistByName(ctx, list, eventReceiverInfo.ReceiverName))
            {
                list.EventReceivers.Add(eventReceiverInfo);
                ctx.ExecuteQuery();
            }
        }

```

Der remote-Ereignisempfänger wird jetzt in die Dokumentbibliothek hinzugefügt. Wenn Sie ein Dokument zur Dokumentbibliothek **AutoTaggingSampleItemAdding** hochladen, das Dokument mit dem Wert der Klassifizierung benutzerdefinierte Profileigenschaft für diesen Benutzer gekennzeichnet. Abbildung 5 veranschaulicht, wie die Eigenschaften in einem Dokument anzeigen. Abbildung 6 zeigt das Dokument Metadaten, bei denen das Feld Klassifikation.


**Abbildung 5. Anzeigen von Dokumenteigenschaften**

![Screenshot eines Dokuments in der Bibliothek mit den Eigenschaften Test erweitert. ](media/991dc064-1855-4897-a012-c56c0079131e.png)
 **Abbildung 6. Feld Klassifikation in die Dokumentmetadaten**

![Screenshot, der die Metadaten des Dokuments Test mit HBI in das Feld Klassifikation zeigt.](media/9dc5be77-70b3-400a-a636-f5fc2face335.png)

Die **HandleAutoTaggingItemAdding** -Methode verwendet in der Datei AutoTaggingService.svc.cs die **GetProfilePropertyFor** -Methode zum Abrufen des Werts der Benutzerprofileigenschaft Klassifikation.

```C#
public void HandleAutoTaggingItemAdding(SPRemoteEventProperties properties,SPRemoteEventResult result)
        {
            using (ClientContext ctx = TokenHelper.CreateRemoteEventReceiverClientContext(properties))
            {
                if (ctx != null)
                {
                    var itemProperties = properties.ItemEventProperties;
                    var _userLoginName = properties.ItemEventProperties.UserLoginName;
                    var _afterProperites = itemProperties.AfterProperties;
                    if(!_afterProperites.ContainsKey(ScenarioHandler.FLD_CLASSIFICATION_INTERNAL_NAME))
                    {
                        string _classficationToSet = ProfileHelper.GetProfilePropertyFor(ctx, _userLoginName, Constants.UPA_CLASSIFICATION_PROPERTY);
                        if(!string.IsNullOrEmpty(_classficationToSet))
                        { 
                            var _formatTaxonomy = AutoTaggingHelper.GetTaxonomyFormat(ctx, _classficationToSet);
                            result.ChangedItemProperties.Add(ScenarioHandler.FLD_CLASSIFICATION_INTERNAL_NAME, _formatTaxonomy);
                        }
                    }
                }
            }
        }

```
    
**Wichtige**  Nach dem Abrufen des **Klassifizierung** Werts aus der **GetProfilePropertyFor** -Methode, muss der **Klassifizierung** Wert auf eine bestimmte Weise formatiert werden, bevor sie als Metadaten für das Dokument gespeichert werden können. Die **GetTaxonomyFormat** -Methode in der Datei AutoTaggingHelper.cs zeigt, wie zum Formatieren des Werts **Klassifikation** .

```C#
public static string GetTaxonomyFormat(ClientContext ctx, string term)
        { 
            if(string.IsNullOrEmpty(term))
            {
                throw new ArgumentException(string.Format(EXCEPTION_MSG_INVALID_ARG, "term"));
            }
            string _result = string.Empty;
            var _list = ctx.Web.Lists.GetByTitle(TAXONOMY_HIDDEN_LIST_NAME);
            CamlQuery _caml = new CamlQuery();

            _caml.ViewXml = string.Format(TAXONOMY_CAML_QRY, term);
            var _listItemCollection = _list.GetItems(_caml);

            ctx.Load(_listItemCollection,
                eachItem => eachItem.Include(
                    item => item,
                    item => item.Id,
                    item => item[TAXONOMY_FIELDS_IDFORTERM]));
            ctx.ExecuteQuery();

            if (_listItemCollection.Count > 0)
            {
                var _item = _listItemCollection.FirstOrDefault();
                var _wssId = _item.Id;
                var _termId = _item[TAXONOMY_FIELDS_IDFORTERM].ToString(); ;
                _result = string.Format(TAXONOMY_FORMATED_STRING, _wssId, term, _termId);
            }

            return _result;
        }

```

### <a name="remove-event-scenario-1"></a>Szenario 1 entfernen

Wenn Sie die Schaltfläche **Entfernen Ereignis Szenario 1**geklickt haben, führt der folgende Code, um den Ereignisempfänger aus der Dokumentbibliothek zu entfernen.

```C#
public static void RemoveEventReceiver(ClientContext ctx, List list, string receiverName)
        {
            ctx.Load(list, lib => lib.EventReceivers);
            ctx.ExecuteQuery();

            var _rer = list.EventReceivers.Where(e => e.ReceiverName == receiverName).FirstOrDefault();
            if(_rer != null)
            {
                _rer.DeleteObject();
                ctx.ExecuteQuery();
            }
        }

```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [OfficeDevPnP.Core-Beispiel](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
