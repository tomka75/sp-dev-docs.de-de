---
title: Unternehmens-Ereignis app-Integration in SharePoint
ms.date: 11/03/2017
ms.openlocfilehash: 959fea4e8fcdfe5c73a9a53e6c5da09c325d781d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="corporate-event-app-integration-with-sharepoint"></a>Unternehmens-Ereignis app-Integration in SharePoint

Integrieren Sie-add-ins für SharePoint in Ihre Geschäftsabläufe mithilfe eines vom Anbieter gehosteten add-Ins, die mehrere komplexe Business Aufgaben implementieren kann.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Das [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) -Beispiel zeigt, wie eine zentralisierte corporate Ereignisse Managementsystem als eine vom Anbieter gehosteten-add-in implementiert wird, die in Ihrer vorhandenen Line-of-Business (LOB)-Anwendungen integriert.

Im Beispiel [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) zeigt, genauer gesagt, wie eine ASP.NET-Webanwendung implementieren, die mit SharePoint als Datenspeicher für LOB-Entitäten interagiert. Es auch zeigt, wie mehrere Schritte in einer komplexen Aufgabe mit einem einzelnen vom Anbieter gehosteten add-in implementiert.
In diesem Beispiel-app implementiert eine zentralisierte Verwaltung-System, der SharePoint-Entitäten (Listen und Inhaltstypen) besteht. Für jeden neuen Inhaltstyp erstellt es entsprechende LOB-Entitäten in einer ASP.NET-Webanwendung. Komponenten der Webanwendung an, wie Remote ausführen gehostet-add-in Webparts innerhalb der SharePoint-Benutzeroberfläche und auch als vollständig auf den remotewebhost ausgeführt. Das Add-in überschreibt die standardmäßige Willkommensseite für Ihre SharePoint-Website, damit eine benutzerdefinierte-Branding-Schnittstelle auf der Homepage der Website angezeigt werden kann.

## <a name="using-the-businessappscorporateeventapp-sample"></a>Verwenden des Beispiels BusinessApps.CorporateEventApp

Wenn Sie die BusinessApps.CorporateEventApp Beispiel-app starten, bietet der Homepage eine Option für das Beispiel konfiguriert. Es verweist auch eine Anzahl von Ressourcen für Weitere Informationen.

Wenn Sie **Konfiguration**auswählen, wechseln Sie auf der Seite Konfiguration, wie in Abbildung 1 dargestellt. Bei der Auswahl **Initialisieren Datenspeicher** auf der Seite Konfiguration wird im Beispiel bereitgestellt, die SharePoint-Entitäten und Beispieldaten, die im Beispiel zu unterstützen.

**Abbildung 1. Konfigurationsseite**

![Screenshot, der die Initialize-Datenbildschirm anzeigt](media/ee213035-b014-45cc-94f4-d8c1c58a047e.png)

Nachdem Sie den Datenspeicher initialisieren, können Sie zurückgehen zu Ihrer Website, um eine neue Willkommensseite (EventsHome.aspx-Seite) anzuzeigen, die von zwei Webparts, die das Add-in bereitgestellt, aufgefüllt wird, wie in Abbildung 2 dargestellt. In der linken Spalte sehen Sie die vier neuen Listen, die von der app installiert, die Corporate Ereignisliste von Beispieldaten aufgefüllt wird.

**Abbildung 2. Homepage mit Webparts initialisiert**

![Screenshot, der zeigt, die Startseite-Add-in mit Webparts bereitgestellt](media/aa4dbd35-70f0-43c2-845c-615632090c44.png)

Jedes Webpart enthält Links zu jedes der angezeigten Ereignisse, wobei Sie die Ereignisdetails anzeigen können. Wenn Sie einen Link auswählen, führt die Detailseite Ereignis separat auf dem Remotehost, wie in Abbildung 3 dargestellt. Sie können auf der Seite zurückkehren zu der SharePoint-Website und registrieren Sie sich für das Ereignis **zurück zur Website** auswählen.

**Abbildung 3. Ereignis-Detailseite**

![Screenshot, der die UI-Add-in mit corporate Ereignis Bildschirm Ereignisdetails anzeigen Zeigt die](media/b967e4ec-e0a6-4aae-af81-e22b92cef0d9.png)

Registrierungsseite auch unabhängig auf dem Remotehost ausgeführt, und enthält außerdem einen Link zurück zur SharePoint-Host-Website (siehe Abbildung 4). Am Ende der Registrierung für das Ereignis, wird Ihr Name in der Liste der neu installierten **Ereignisregistrierung** angezeigt.

**Abbildung 4. Ereignis Registrierungsseite**

![Screenshot, der die app im Unternehmen Ereignisse Ereignis Registrierungsbildschirm anzeigt](media/d2ec4156-5806-4b20-ab5b-3d25fcc33f1a.png)

Die Models\DataInitializer.cs-Datei enthält den Code, der ausgeführt wird, wenn Sie auf diese Schaltfläche geklickt. Der Code in der Datei erstellt und vier neue SharePoint-Listen zusammen mit vier entsprechenden Inhaltstypen bereitstellt:

- Unternehmens-Ereignisse
    
- Ereignisregistrierung
    
- Ereignis Lautsprecher
    
- Ereignis-Sitzungen
    
Der Code in dieser Datei verwendet eine Methode ähnelt, die in der Stichprobe [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages) verwendet wird, um eine benutzerdefinierte Seite der Website hinzufügen.

```
            // Create default wiki page.
            web.AddWikiPage("Site Pages", "EventsHome.aspx");
AddWikiPage is an extension method from the Core.DevPnPCore project to add a new page to the site. This new page also becomes the new WelcomePage for the site. It also prepares to add the web parts to this page.
            var welcomePage = "SitePages/EventsHome.aspx";
            var serverRelativeUrl = UrlUtility.Combine(web.ServerRelativeUrl, welcomePage);

            File webPartPage = web.GetFileByServerRelativeUrl(serverRelativeUrl);

            if (webPartPage == null) {
                return;
            }

            web.Context.Load(webPartPage);
            web.Context.Load(webPartPage.ListItemAllFields);
            web.Context.Load(web.RootFolder);
            web.Context.ExecuteQuery();

            web.RootFolder.WelcomePage = welcomePage;
            web.RootFolder.Update();
            web.Context.ExecuteQuery();

```

Die Datei Models\DataInitializer.cs auch definiert das XML für beide Webparts, die auf der neuen Seite Willkommen angezeigt werden und fügt dann jeweils auf der Seite. Die folgenden Beispiele zeigen, wie dies für das ausgewählte Ereignisse-Webpart funktioniert.

**Definieren von XML-Webpart**

```XML
            var webPart1 = new WebPartEntity(){
                WebPartXml = @"<webParts>
  <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>
    <metaData>
      <type name='Microsoft.SharePoint.WebPartPages.ClientWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />
      <importErrorMessage>Cannot import this Web Part.</importErrorMessage>
    </metaData>
    <data>
      <properties>
        <property name='Description' type='string'>Displays featured events</property>
        <property name='FeatureId' type='System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'>3a6d7f41-2de8-4e69-b4b4-0325bd56b32c</property>
        <property name='Title' type='string'>Featured Events</property>
        <property name='ProductWebId' type='System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'>12ae648f-27db-4a97-9c63-37155d3ace1e</property>
        <property name='WebPartName' type='string'>FeaturedEvents</property>
        <property name='ProductId' type='System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'>3a6d7f41-2de8-4e69-b4b4-0325bd56b32b</property>
        <property name='ChromeState' type='chromestate'>Normal</property>
      </properties>
    </data>
  </webPart>
</webParts>",
                WebPartIndex = 0,
                WebPartTitle = "Featured Events",
                WebPartZone = "Rich Content"
            };

```

**Hinzufügen der Webparts zur Seite**

```XML
            var limitedWebPartManager = webPartPage.GetLimitedWebPartManager(Microsoft.SharePoint.Client.WebParts.PersonalizationScope.Shared);
            web.Context.Load(limitedWebPartManager.WebParts);
            web.Context.ExecuteQuery();

            for (var i = 0; i < limitedWebPartManager.WebParts.Count; i++) {
                limitedWebPartManager.WebParts[i].DeleteWebPart();
            }
            web.Context.ExecuteQuery();

            var oWebPartDefinition1 = limitedWebPartManager.ImportWebPart(webPart1.WebPartXml);
            var oWebPartDefinition2 = limitedWebPartManager.ImportWebPart(webPart2.WebPartXml);
            var wpdNew1 = limitedWebPartManager.AddWebPart(oWebPartDefinition1.WebPart, webPart1.WebPartZone, webPart1.WebPartIndex);
            var wpdNew2 = limitedWebPartManager.AddWebPart(oWebPartDefinition2.WebPart, webPart2.WebPartZone, webPart2.WebPartIndex);
            web.Context.Load(wpdNew1);
            web.Context.Load(wpdNew2);
            web.Context.ExecuteQuery();

```

Im Verzeichnis Modelle des Webprojekts werden Sie feststellen, dass diese MVC ASP.NET-Webanwendung vier Klassennamen, die entsprechen enthält, die Listen und Inhaltstypen, die die app installiert:

- Event.cs (Corporate Ereignisse)
    
- Registration.cs (Ereignisregistrierung)
    
- Session.cs (Ereignis Sitzungen)
    
- Speaker.cs (Ereignis Lautsprecher)
    
Diese vier Klassen und ihre entsprechenden SharePoint-Inhaltstypen zusammen bilden die vier LOB Entitäten in add-Ins.

Die Datei DataInitializer.cs hinzugefügt Beispieldaten für die Ereignisliste **Im Unternehmen** durch Erstellen von Beispiel- **Event** -Objekte, die mit dem Inhaltstyp **Corporate Ereignisse** entsprechen und, die app einfügt, um die **Corporate** Ereignisliste. Wenn Sie für ein Ereignis registrieren, wird die app ein **Registration** -Objekt, das den Inhaltstyp **-Ereignisregistrierung** entspricht, und die app, die die **Ereignisregistrierung** Liste hinzufügt, erstellt. Im Beispiel wurde noch nicht vollständig die **Sitzung** und **Lautsprecher** Objekte, implementiert, damit die app nicht aktuell mit dieser Objekte funktioniert.

Die folgende Tabelle enthält die Eigenschaften müssen durch die Klassen implementiert werden, die von der abstrakten **BaseListItem** -Klasse erbt.

** Tabelle 1. Methoden zum erben von Klassen implementieren ** BaseListItem ***

|**Element  **|**Beschreibung**|
|:-----|:-----|
|**Inhaltstypname**|Ruft den Inhaltstyp, der das Element zugeordnet ist. Wenn null ist, wird der Bibliothek Standardinhaltstyp das Element zugewiesen werden beim Speichern.|
|**FieldInternalNames**|Eine Liste von Feldnamen, die zum Verbessern der Leistung bei Verwendung für die Überprüfung von Felddaten vor dem Speichern zwischengespeichert werden kann.|
|ListTitle|Ruft den Titel der Liste (Groß-/Kleinschreibung beachten) ab.|

Die folgende Tabelle enthält die Methoden, die durch die Klassen implementiert werden, die von der **BaseListItem** abstrakten Klasse erben. Diese Methoden zurück Parameter, die auf [blitfähige Typen](https://msdn.microsoft.com/en-us/library/75dwhxf7%28v=vs.110%29.aspx) festgelegt werden soll, sodass sie auf mehreren Plattformen verwendet werden können.

 **In Tabelle 2. Methoden, die blitfähige Typen zurückgeben**

|**Methode**|**Beschreibung**|
|:-----|:-----|
|**ReadProperties(ListItem)**|Liest die Eigenschaften aus den **ListItem** -Objekt mit den **BaseGet** und **BaseGetEnum** -Methoden und Eigenschaften der Unterklasse zugewiesen.|
|**SetProperties(ListItem)**|Legt Eigenschaften für die Verwendung der Methoden **BaseSet** und **BaseSetTaxonomyField** der abstrakten Klasse **ListItem** -Objekt.|

Die folgende Tabelle listet die Hilfsmethoden von der **BaseListItem** -Klasse, die die Unterklassen **ReadProperties** und **SetProperties** -Methoden implementieren müssen.

**Tabelle 3. BaseListItem Hilfsmethoden**

|**Hilfsmethode**|**Beschreibung**|
|:-----|:-----|
|**BaseGet (ListItem-Element, Zeichenfolge InternalName)**|Ruft die Eigenschaft durch den Parameter *InternalName* von **ListItem** definiert, und des generischen Typs **T**zurückgeben.|
|**BaseSet (ListItem-Element, Zeichenfolge InternalName, Object-Wert)**|Die durch den Parameter *InternalName* definierte **ListItem** -Eigenschaft festgelegt.|
|**BaseSetTaxonomyField (ListItem-Element, Zeichenfolge InternalName, Beschriftung, Guid TermId)**|Legt das **ListItem** Taxonomie dar, die von den Parametern *InternalName* und *TermId* definiert.|
|**BaseGetEnum (ListItem-Element, Zeichenfolge InternalName, T DefaultValue)**|Ruft den Wert der durch den Parameter *InternalName* definiert Enumerationseigenschaft ab. Gibt den Wert des Parameters *DefaultValue* zurück, wenn die Eigenschaft nicht festgelegt ist.|

Die Datei Event.cs enthält die folgenden Implementierungen der Methoden **ReadProperties** und **SetProperties** .

**ReadProperties**

```C#
        protected override void ReadProperties(ListItem item) {
            RegisteredEventId = BaseGet<string>(item, FIELD_REGISTERED_EVENT_ID);
            Description = BaseGet<string>(item, FIELD_DESCRIPTION);
            Category = BaseGet<string>(item, FIELD_CATEGORY);
            EventDate = BaseGet<DateTime?>(item, FIELD_DATE);
            Location = BaseGet<string>(item, FIELD_LOCATION);
            ContactEmail = BaseGet<string>(item, FIELD_CONTACT_EMAIL);
            Status = BaseGetEnum<EventStatus>(item, FIELD_STATUS);
            var imageUrl = BaseGet<FieldUrlValue>(item, FIELD_IMAGE_URL);

            if (imageUrl != null)
                ImageUrl = imageUrl.Url;
        }
SetProperties:
        protected override void SetProperties(ListItem item) {
            BaseSet(item, FIELD_REGISTERED_EVENT_ID, RegisteredEventId);
            BaseSet(item, FIELD_DESCRIPTION, Description);
            BaseSet(item, FIELD_CATEGORY, Category);
            BaseSet(item, FIELD_DATE, EventDate);
            BaseSet(item, FIELD_LOCATION, Location);
            BaseSet(item, FIELD_CONTACT_EMAIL, ContactEmail);
            BaseSet(item, FIELD_STATUS, Status.ToEnumDescription());
            BaseSet(item, FIELD_IMAGE_URL, ImageUrl);
        }

```

Die folgenden Codebeispiele zeigen, wie die zugrunde liegenden Methoden **BaseGet** und **BaseSet** in BaseListItem.cs definiert sind.

**BaseGet**

```
protected T BaseGet<T>(ListItem item, string internalName){
            var field = _fields[internalName.ToLowerInvariant()];
            var value = item[field.InternalName];
            return (T)value;
        }

```

**BaseSet**

```
protected void BaseSet(ListItem item, string internalName, object value) {
            if (_fields.ContainsKey(internalName)) {
                var field = _fields[internalName.ToLowerInvariant()];

                if (field is FieldUrl &amp;&amp; value is string) {
                    var urlValue = new FieldUrlValue() {
                        Url = value.ToString()
                    };
                    value = urlValue;
                }
            }
            item[internalName] = value;
        }
```

Die **BaseListItem** -Klasse enthält auch eine **Speichern** -Methode, mit der einzelnen LOB-Entität zu speichern, die die app erstellt und bearbeitet. Diese Methode lädt die Liste und bestimmt, ob das aktuelle Element eine ID verfügt, die größer als 0 ist. Wenn die ID nicht größer als 0 ist, wird angenommen, dass es nicht gültig ist und ein neues Listenelement erstellt. **SetProperties** -Methode verwendet, um Eigenschaften für das **ListItem** festzulegen, und legt dann die Eigenschaften für die Unterklasse mithilfe der **ReadProperties** -Methode.

```
public void Save(Web web) {
            var context = web.Context;
            var list = web.GetListByTitle(ListTitle);
            if (!IsNew &amp;&amp; Id > 0) {
                ListItem = list.GetItemById(Id);
            }
            else {
                var listItemCreationInfo = new ListItemCreationInformation();
                ListItem = list.AddItem(listItemCreationInfo);
            }

            // Ensure that the fields have been loaded.
            EnsureFieldsRetrieved(ListItem);

            // Set the properties on the list item.
            SetProperties(ListItem);
            BaseSet(ListItem, TITLE, Title);

            // Use if you want to override the created/modified date.
            //BaseSet(ListItem, CREATED, Created);
            //BaseSet(ListItem, MODIFIED, Modified);

            ListItem.Update();

            if (!string.IsNullOrEmpty(ContentTypeName)) {
                var contentType = list.GetContentTypeByName(ContentTypeName);
                if (contentType != null)
                    BaseSet(ListItem, "ContentTypeId", contentType.Id.StringValue);
            }

            ListItem.Update();

            // Execute the batch.
            context.ExecuteQuery();

            // Reload the properties.
            ListItem.RefreshLoad();
            UpdateBaseProperties(ListItem);
            ReadProperties(ListItem);
        }

```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Zusammengesetzte Business-add-ins für SharePoint 2013 und SharePoint Online](Composite-buisness-apps-for-SharePoint.md)
    
-  [Core.ModifyPages-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages)
    
-  [Provisioning.Pages-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages)
    
-  [OfficeDevPnP.Core-Beispiel](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
