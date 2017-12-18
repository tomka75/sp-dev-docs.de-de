---
title: Unternehmens-Ereignis app-Integration in SharePoint
ms.date: 11/03/2017
ms.openlocfilehash: 959fea4e8fcdfe5c73a9a53e6c5da09c325d781d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="corporate-event-app-integration-with-sharepoint"></a><span data-ttu-id="9eea5-102">Unternehmens-Ereignis app-Integration in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9eea5-102">Corporate event app integration with SharePoint</span></span>

<span data-ttu-id="9eea5-103">Integrieren Sie-add-ins für SharePoint in Ihre Geschäftsabläufe mithilfe eines vom Anbieter gehosteten add-Ins, die mehrere komplexe Business Aufgaben implementieren kann.</span><span class="sxs-lookup"><span data-stu-id="9eea5-103">Integrate add-ins for SharePoint into your business operations by using a provider-hosted add-in that can implement multiple complex business tasks.</span></span>

<span data-ttu-id="9eea5-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="9eea5-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="9eea5-105">Das [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) -Beispiel zeigt, wie eine zentralisierte corporate Ereignisse Managementsystem als eine vom Anbieter gehosteten-add-in implementiert wird, die in Ihrer vorhandenen Line-of-Business (LOB)-Anwendungen integriert.</span><span class="sxs-lookup"><span data-stu-id="9eea5-105">The  [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) sample shows you how to implement a centralized corporate events management system as a provider-hosted add-in that integrates with your existing line-of-business (LOB) applications.</span></span>

<span data-ttu-id="9eea5-106">Im Beispiel [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) zeigt, genauer gesagt, wie eine ASP.NET-Webanwendung implementieren, die mit SharePoint als Datenspeicher für LOB-Entitäten interagiert.</span><span class="sxs-lookup"><span data-stu-id="9eea5-106">More specifically, the  [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) sample shows you how to implement an ASP.NET web application that interacts with SharePoint as a data store for LOB entities.</span></span> <span data-ttu-id="9eea5-107">Es auch zeigt, wie mehrere Schritte in einer komplexen Aufgabe mit einem einzelnen vom Anbieter gehosteten add-in implementiert.</span><span class="sxs-lookup"><span data-stu-id="9eea5-107">It also shows you how to implement multiple steps in a complex business task with a single provider-hosted add-in.</span></span>
<span data-ttu-id="9eea5-108">In diesem Beispiel-app implementiert eine zentralisierte Verwaltung-System, der SharePoint-Entitäten (Listen und Inhaltstypen) besteht.</span><span class="sxs-lookup"><span data-stu-id="9eea5-108">This sample app implements a centralized management system that consists of SharePoint entities (lists and content types).</span></span> <span data-ttu-id="9eea5-109">Für jeden neuen Inhaltstyp erstellt es entsprechende LOB-Entitäten in einer ASP.NET-Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="9eea5-109">For each new content type, it creates corresponding LOB entities in an ASP.NET web application.</span></span> <span data-ttu-id="9eea5-110">Komponenten der Webanwendung an, wie Remote ausführen gehostet-add-in Webparts innerhalb der SharePoint-Benutzeroberfläche und auch als vollständig auf den remotewebhost ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-110">Components of the web application run as remotely hosted add-in parts within the SharePoint interface and also as pages running entirely on the remote web host.</span></span> <span data-ttu-id="9eea5-111">Das Add-in überschreibt die standardmäßige Willkommensseite für Ihre SharePoint-Website, damit eine benutzerdefinierte-Branding-Schnittstelle auf der Homepage der Website angezeigt werden kann.</span><span class="sxs-lookup"><span data-stu-id="9eea5-111">The add-in overrides the default welcome page for your SharePoint site so that it can present a custom-branded interface on the site home page.</span></span>

## <a name="using-the-businessappscorporateeventapp-sample"></a><span data-ttu-id="9eea5-112">Verwenden des Beispiels BusinessApps.CorporateEventApp</span><span class="sxs-lookup"><span data-stu-id="9eea5-112">Using the BusinessApps.CorporateEventApp sample</span></span>

<span data-ttu-id="9eea5-113">Wenn Sie die BusinessApps.CorporateEventApp Beispiel-app starten, bietet der Homepage eine Option für das Beispiel konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="9eea5-113">When you start the BusinessApps.CorporateEventApp sample app, the Home page provides an option for you to configure the sample.</span></span> <span data-ttu-id="9eea5-114">Es verweist auch eine Anzahl von Ressourcen für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="9eea5-114">It also points you to a number of resources for more information.</span></span>

<span data-ttu-id="9eea5-115">Wenn Sie **Konfiguration**auswählen, wechseln Sie auf der Seite Konfiguration, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-115">When you choose  **Start configuration**, you go to the Configuration page, as shown in Figure 1.</span></span> <span data-ttu-id="9eea5-116">Bei der Auswahl **Initialisieren Datenspeicher** auf der Seite Konfiguration wird im Beispiel bereitgestellt, die SharePoint-Entitäten und Beispieldaten, die im Beispiel zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="9eea5-116">When you choose  **Initialize the data store** on the Configuration page, the sample deploys the SharePoint entities and sample data that support the sample.</span></span>

<span data-ttu-id="9eea5-117">**Abbildung 1. Konfigurationsseite**</span><span class="sxs-lookup"><span data-stu-id="9eea5-117">**Figure 1. Configuration page**</span></span>

![Screenshot, der die Initialize-Datenbildschirm anzeigt](media/ee213035-b014-45cc-94f4-d8c1c58a047e.png)

<span data-ttu-id="9eea5-119">Nachdem Sie den Datenspeicher initialisieren, können Sie zurückgehen zu Ihrer Website, um eine neue Willkommensseite (EventsHome.aspx-Seite) anzuzeigen, die von zwei Webparts, die das Add-in bereitgestellt, aufgefüllt wird, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-119">After you initialize the data store, you can go back to your site to see a new welcome page (the EventsHome.aspx page), which is populated by two web parts that the add-in deployed, as shown in Figure 2.</span></span> <span data-ttu-id="9eea5-120">In der linken Spalte sehen Sie die vier neuen Listen, die von der app installiert, die Corporate Ereignisliste von Beispieldaten aufgefüllt wird.</span><span class="sxs-lookup"><span data-stu-id="9eea5-120">In the left column, you'll see the four new lists installed by the app, The Corporate Events list is populated by sample data.</span></span>

<span data-ttu-id="9eea5-121">**Abbildung 2. Homepage mit Webparts initialisiert**</span><span class="sxs-lookup"><span data-stu-id="9eea5-121">**Figure 2. Welcome page with web parts initialized**</span></span>

![Screenshot, der zeigt, die Startseite-Add-in mit Webparts bereitgestellt](media/aa4dbd35-70f0-43c2-845c-615632090c44.png)

<span data-ttu-id="9eea5-123">Jedes Webpart enthält Links zu jedes der angezeigten Ereignisse, wobei Sie die Ereignisdetails anzeigen können.</span><span class="sxs-lookup"><span data-stu-id="9eea5-123">Each web part contains links to each of the displayed events, where you can see the event details.</span></span> <span data-ttu-id="9eea5-124">Wenn Sie einen Link auswählen, führt die Detailseite Ereignis separat auf dem Remotehost, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-124">When you choose a link, the event details page runs separately on the remote host, as shown in Figure 3.</span></span> <span data-ttu-id="9eea5-125">Sie können auf der Seite zurückkehren zu der SharePoint-Website und registrieren Sie sich für das Ereignis **zurück zur Website** auswählen.</span><span class="sxs-lookup"><span data-stu-id="9eea5-125">You can choose  **Back to Site** on the page to return to the SharePoint site, and also to register yourself for the event.</span></span>

<span data-ttu-id="9eea5-126">**Abbildung 3. Ereignis-Detailseite**</span><span class="sxs-lookup"><span data-stu-id="9eea5-126">**Figure 3. Event details page**</span></span>

![Screenshot, der die UI-Add-in mit corporate Ereignis Bildschirm Ereignisdetails anzeigen Zeigt die](media/b967e4ec-e0a6-4aae-af81-e22b92cef0d9.png)

<span data-ttu-id="9eea5-128">Registrierungsseite auch unabhängig auf dem Remotehost ausgeführt, und enthält außerdem einen Link zurück zur SharePoint-Host-Website (siehe Abbildung 4).</span><span class="sxs-lookup"><span data-stu-id="9eea5-128">The registration page also runs separately on the remote host, and also contains a link back to the SharePoint host site (see Figure 4).</span></span> <span data-ttu-id="9eea5-129">Am Ende der Registrierung für das Ereignis, wird Ihr Name in der Liste der neu installierten **Ereignisregistrierung** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-129">When you finish registering for the event, your name will appear on the newly installed  **Event Registration** list.</span></span>

<span data-ttu-id="9eea5-130">**Abbildung 4. Ereignis Registrierungsseite**</span><span class="sxs-lookup"><span data-stu-id="9eea5-130">**Figure 4. Event registration page**</span></span>

![Screenshot, der die app im Unternehmen Ereignisse Ereignis Registrierungsbildschirm anzeigt](media/d2ec4156-5806-4b20-ab5b-3d25fcc33f1a.png)

<span data-ttu-id="9eea5-132">Die Models\DataInitializer.cs-Datei enthält den Code, der ausgeführt wird, wenn Sie auf diese Schaltfläche geklickt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-132">The Models\DataInitializer.cs file contains the code that runs when you choose this button.</span></span> <span data-ttu-id="9eea5-133">Der Code in der Datei erstellt und vier neue SharePoint-Listen zusammen mit vier entsprechenden Inhaltstypen bereitstellt:</span><span class="sxs-lookup"><span data-stu-id="9eea5-133">The code in this file creates and deploys four new SharePoint lists, along with four corresponding content types:</span></span>

- <span data-ttu-id="9eea5-134">Unternehmens-Ereignisse</span><span class="sxs-lookup"><span data-stu-id="9eea5-134">Corporate events</span></span>
    
- <span data-ttu-id="9eea5-135">Ereignisregistrierung</span><span class="sxs-lookup"><span data-stu-id="9eea5-135">Event registration</span></span>
    
- <span data-ttu-id="9eea5-136">Ereignis Lautsprecher</span><span class="sxs-lookup"><span data-stu-id="9eea5-136">Event speakers</span></span>
    
- <span data-ttu-id="9eea5-137">Ereignis-Sitzungen</span><span class="sxs-lookup"><span data-stu-id="9eea5-137">Event sessions</span></span>
    
<span data-ttu-id="9eea5-138">Der Code in dieser Datei verwendet eine Methode ähnelt, die in der Stichprobe [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages) verwendet wird, um eine benutzerdefinierte Seite der Website hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="9eea5-138">The code in this file uses a method similar to the one that is used in the  [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages) sample to add a custom page to the site.</span></span>

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

<span data-ttu-id="9eea5-139">Die Datei Models\DataInitializer.cs auch definiert das XML für beide Webparts, die auf der neuen Seite Willkommen angezeigt werden und fügt dann jeweils auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="9eea5-139">The Models\DataInitializer.cs file also defines the XML for both web parts that are displayed on the new welcome page and then adds each one to the page.</span></span> <span data-ttu-id="9eea5-140">Die folgenden Beispiele zeigen, wie dies für das ausgewählte Ereignisse-Webpart funktioniert.</span><span class="sxs-lookup"><span data-stu-id="9eea5-140">The following examples show how this works for the Featured Events web part.</span></span>

<span data-ttu-id="9eea5-141">**Definieren von XML-Webpart**</span><span class="sxs-lookup"><span data-stu-id="9eea5-141">**Define web part XML**</span></span>

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

<span data-ttu-id="9eea5-142">**Hinzufügen der Webparts zur Seite**</span><span class="sxs-lookup"><span data-stu-id="9eea5-142">**Add the web parts to the page**</span></span>

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

<span data-ttu-id="9eea5-143">Im Verzeichnis Modelle des Webprojekts werden Sie feststellen, dass diese MVC ASP.NET-Webanwendung vier Klassennamen, die entsprechen enthält, die Listen und Inhaltstypen, die die app installiert:</span><span class="sxs-lookup"><span data-stu-id="9eea5-143">In the Models directory of your web project, you'll notice that this MVC ASP.NET web application contains four class names that correspond to the lists and content types that the app installed:</span></span>

- <span data-ttu-id="9eea5-144">Event.cs (Corporate Ereignisse)</span><span class="sxs-lookup"><span data-stu-id="9eea5-144">Event.cs (Corporate Events)</span></span>
    
- <span data-ttu-id="9eea5-145">Registration.cs (Ereignisregistrierung)</span><span class="sxs-lookup"><span data-stu-id="9eea5-145">Registration.cs (Event Registration)</span></span>
    
- <span data-ttu-id="9eea5-146">Session.cs (Ereignis Sitzungen)</span><span class="sxs-lookup"><span data-stu-id="9eea5-146">Session.cs (Event Sessions)</span></span>
    
- <span data-ttu-id="9eea5-147">Speaker.cs (Ereignis Lautsprecher)</span><span class="sxs-lookup"><span data-stu-id="9eea5-147">Speaker.cs (Event Speakers)</span></span>
    
<span data-ttu-id="9eea5-148">Diese vier Klassen und ihre entsprechenden SharePoint-Inhaltstypen zusammen bilden die vier LOB Entitäten in add-Ins.</span><span class="sxs-lookup"><span data-stu-id="9eea5-148">These four classes and their corresponding SharePoint content types together make up the four LOB entities used in this add-in.</span></span>

<span data-ttu-id="9eea5-149">Die Datei DataInitializer.cs hinzugefügt Beispieldaten für die Ereignisliste **Im Unternehmen** durch Erstellen von Beispiel- **Event** -Objekte, die mit dem Inhaltstyp **Corporate Ereignisse** entsprechen und, die app einfügt, um die **Corporate** Ereignisliste.</span><span class="sxs-lookup"><span data-stu-id="9eea5-149">The DataInitializer.cs file adds sample data for the  **Corporate Events** list by creating sample **Event** objects that correspond with the **Corporate Events** content type and which the app adds to the **Corporate Events** list.</span></span> <span data-ttu-id="9eea5-150">Wenn Sie für ein Ereignis registrieren, wird die app ein **Registration** -Objekt, das den Inhaltstyp **-Ereignisregistrierung** entspricht, und die app, die die **Ereignisregistrierung** Liste hinzufügt, erstellt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-150">When you register for an event, the app creates a **Registration** object that corresponds with the **Event Registration** content type and that the app adds to the **Event Registration** list.</span></span> <span data-ttu-id="9eea5-151">Im Beispiel wurde noch nicht vollständig die **Sitzung** und **Lautsprecher** Objekte, implementiert, damit die app nicht aktuell mit dieser Objekte funktioniert.</span><span class="sxs-lookup"><span data-stu-id="9eea5-151">The sample has not yet fully implemented the **Session** and **Speaker** objects, so the app currently doesn't work with those objects.</span></span>

<span data-ttu-id="9eea5-152">Die folgende Tabelle enthält die Eigenschaften müssen durch die Klassen implementiert werden, die von der abstrakten **BaseListItem** -Klasse erbt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-152">The following table lists the properties need to be implemented by the classes that inherit from the  **BaseListItem** abstract class.</span></span>

<span data-ttu-id="9eea5-153">** Tabelle 1.</span><span class="sxs-lookup"><span data-stu-id="9eea5-153">**Table 1.</span></span> <span data-ttu-id="9eea5-154">Methoden zum erben von Klassen implementieren ** BaseListItem ***</span><span class="sxs-lookup"><span data-stu-id="9eea5-154">Methods to implement in classes inheriting from  **BaseListItem****</span></span>

|<span data-ttu-id="9eea5-155">**Element  **</span><span class="sxs-lookup"><span data-stu-id="9eea5-155">**Member**</span></span>|<span data-ttu-id="9eea5-156">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="9eea5-156">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9eea5-157">**Inhaltstypname**</span><span class="sxs-lookup"><span data-stu-id="9eea5-157">**ContentTypeName**</span></span>|<span data-ttu-id="9eea5-158">Ruft den Inhaltstyp, der das Element zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="9eea5-158">Gets the content type that is associated with the item.</span></span> <span data-ttu-id="9eea5-159">Wenn null ist, wird der Bibliothek Standardinhaltstyp das Element zugewiesen werden beim Speichern.</span><span class="sxs-lookup"><span data-stu-id="9eea5-159">If null, the default library content type will be assigned to the item when you save it.</span></span>|
|<span data-ttu-id="9eea5-160">**FieldInternalNames**</span><span class="sxs-lookup"><span data-stu-id="9eea5-160">**FieldInternalNames**</span></span>|<span data-ttu-id="9eea5-161">Eine Liste von Feldnamen, die zum Verbessern der Leistung bei Verwendung für die Überprüfung von Felddaten vor dem Speichern zwischengespeichert werden kann.</span><span class="sxs-lookup"><span data-stu-id="9eea5-161">A list of field names that can be cached to improve performance when used for checking field data prior to save.</span></span>|
|<span data-ttu-id="9eea5-162">ListTitle</span><span class="sxs-lookup"><span data-stu-id="9eea5-162">ListTitle</span></span>|<span data-ttu-id="9eea5-163">Ruft den Titel der Liste (Groß-/Kleinschreibung beachten) ab.</span><span class="sxs-lookup"><span data-stu-id="9eea5-163">Gets the title of the list (case sensitive).</span></span>|

<span data-ttu-id="9eea5-164">Die folgende Tabelle enthält die Methoden, die durch die Klassen implementiert werden, die von der **BaseListItem** abstrakten Klasse erben.</span><span class="sxs-lookup"><span data-stu-id="9eea5-164">The following table lists the methods that have to be implemented by the classes that inherit from the  **BaseListItem** abstract class.</span></span> <span data-ttu-id="9eea5-165">Diese Methoden zurück Parameter, die auf [blitfähige Typen](https://msdn.microsoft.com/en-us/library/75dwhxf7%28v=vs.110%29.aspx) festgelegt werden soll, sodass sie auf mehreren Plattformen verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="9eea5-165">These methods return parameters that should be set to [blittable types](https://msdn.microsoft.com/en-us/library/75dwhxf7%28v=vs.110%29.aspx) so that they can be used on multiple platforms.</span></span>

 <span data-ttu-id="9eea5-166">**In Tabelle 2. Methoden, die blitfähige Typen zurückgeben**</span><span class="sxs-lookup"><span data-stu-id="9eea5-166">**Table 2. Methods that return blittable types**</span></span>

|<span data-ttu-id="9eea5-167">**Methode**</span><span class="sxs-lookup"><span data-stu-id="9eea5-167">**Method**</span></span>|<span data-ttu-id="9eea5-168">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="9eea5-168">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9eea5-169">**ReadProperties(ListItem)**</span><span class="sxs-lookup"><span data-stu-id="9eea5-169">**ReadProperties(ListItem)**</span></span>|<span data-ttu-id="9eea5-170">Liest die Eigenschaften aus den **ListItem** -Objekt mit den **BaseGet** und **BaseGetEnum** -Methoden und Eigenschaften der Unterklasse zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="9eea5-170">Reads properties from the **ListItem** object using the **BaseGet** and **BaseGetEnum** methods and assigns them to properties of the subclass.</span></span>|
|<span data-ttu-id="9eea5-171">**SetProperties(ListItem)**</span><span class="sxs-lookup"><span data-stu-id="9eea5-171">**SetProperties(ListItem)**</span></span>|<span data-ttu-id="9eea5-172">Legt Eigenschaften für die Verwendung der Methoden **BaseSet** und **BaseSetTaxonomyField** der abstrakten Klasse **ListItem** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-172">Sets properties on the **ListItem** object using the **BaseSet** and **BaseSetTaxonomyField** methods of the abstract class.</span></span>|

<span data-ttu-id="9eea5-173">Die folgende Tabelle listet die Hilfsmethoden von der **BaseListItem** -Klasse, die die Unterklassen **ReadProperties** und **SetProperties** -Methoden implementieren müssen.</span><span class="sxs-lookup"><span data-stu-id="9eea5-173">The following table lists the helper methods from the  **BaseListItem** class that the subclasses need to implement the **ReadProperties** and **SetProperties** methods.</span></span>

<span data-ttu-id="9eea5-174">**Tabelle 3. BaseListItem Hilfsmethoden**</span><span class="sxs-lookup"><span data-stu-id="9eea5-174">**Table 3. BaseListItem helper methods**</span></span>

|<span data-ttu-id="9eea5-175">**Hilfsmethode**</span><span class="sxs-lookup"><span data-stu-id="9eea5-175">**Helper method**</span></span>|<span data-ttu-id="9eea5-176">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="9eea5-176">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9eea5-177">**BaseGet (ListItem-Element, Zeichenfolge InternalName)**</span><span class="sxs-lookup"><span data-stu-id="9eea5-177">**BaseGet(ListItem item, string internalName)**</span></span>|<span data-ttu-id="9eea5-178">Ruft die Eigenschaft durch den Parameter *InternalName* von **ListItem** definiert, und des generischen Typs **T**zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="9eea5-178">Gets the property defined by the *internalName* parameter from **ListItem** and returns them of generic type **T**.</span></span>|
|<span data-ttu-id="9eea5-179">**BaseSet (ListItem-Element, Zeichenfolge InternalName, Object-Wert)**</span><span class="sxs-lookup"><span data-stu-id="9eea5-179">**BaseSet(ListItem item, string internalName, object value)**</span></span>|<span data-ttu-id="9eea5-180">Die durch den Parameter *InternalName* definierte **ListItem** -Eigenschaft festgelegt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-180">Sets the **ListItem** property defined by the *internalName* parameter.</span></span>|
|<span data-ttu-id="9eea5-181">**BaseSetTaxonomyField (ListItem-Element, Zeichenfolge InternalName, Beschriftung, Guid TermId)**</span><span class="sxs-lookup"><span data-stu-id="9eea5-181">**BaseSetTaxonomyField(ListItem item, string internalName, string label, Guid termId)**</span></span>|<span data-ttu-id="9eea5-182">Legt das **ListItem** Taxonomie dar, die von den Parametern *InternalName* und *TermId* definiert.</span><span class="sxs-lookup"><span data-stu-id="9eea5-182">Sets the **ListItem** taxonomy field defined by the *internalName* and *termId* parameters.</span></span>|
|<span data-ttu-id="9eea5-183">**BaseGetEnum (ListItem-Element, Zeichenfolge InternalName, T DefaultValue)**</span><span class="sxs-lookup"><span data-stu-id="9eea5-183">**BaseGetEnum(ListItem item, string internalName, T defaultValue)**</span></span>|<span data-ttu-id="9eea5-184">Ruft den Wert der durch den Parameter *InternalName* definiert Enumerationseigenschaft ab.</span><span class="sxs-lookup"><span data-stu-id="9eea5-184">Gets the value of the enum property defined by the *internalName* parameter.</span></span> <span data-ttu-id="9eea5-185">Gibt den Wert des Parameters *DefaultValue* zurück, wenn die Eigenschaft nicht festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="9eea5-185">Returns the value of the *defaultValue* parameter if the property is not set.</span></span>|

<span data-ttu-id="9eea5-186">Die Datei Event.cs enthält die folgenden Implementierungen der Methoden **ReadProperties** und **SetProperties** .</span><span class="sxs-lookup"><span data-stu-id="9eea5-186">The Event.cs file contains the following implementations of the  **ReadProperties** and **SetProperties** methods.</span></span>

<span data-ttu-id="9eea5-187">**ReadProperties**</span><span class="sxs-lookup"><span data-stu-id="9eea5-187">**ReadProperties**</span></span>

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

<span data-ttu-id="9eea5-188">Die folgenden Codebeispiele zeigen, wie die zugrunde liegenden Methoden **BaseGet** und **BaseSet** in BaseListItem.cs definiert sind.</span><span class="sxs-lookup"><span data-stu-id="9eea5-188">The following code examples show how the underlying  **BaseGet** and **BaseSet** methods are defined in BaseListItem.cs.</span></span>

<span data-ttu-id="9eea5-189">**BaseGet**</span><span class="sxs-lookup"><span data-stu-id="9eea5-189">**BaseGet**</span></span>

```
protected T BaseGet<T>(ListItem item, string internalName){
            var field = _fields[internalName.ToLowerInvariant()];
            var value = item[field.InternalName];
            return (T)value;
        }

```

<span data-ttu-id="9eea5-190">**BaseSet**</span><span class="sxs-lookup"><span data-stu-id="9eea5-190">**BaseSet**</span></span>

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

<span data-ttu-id="9eea5-191">Die **BaseListItem** -Klasse enthält auch eine **Speichern** -Methode, mit der einzelnen LOB-Entität zu speichern, die die app erstellt und bearbeitet.</span><span class="sxs-lookup"><span data-stu-id="9eea5-191">The  **BaseListItem** class also contains a **Save** method that is used to save each LOB entity that the app creates and manipulates.</span></span> <span data-ttu-id="9eea5-192">Diese Methode lädt die Liste und bestimmt, ob das aktuelle Element eine ID verfügt, die größer als 0 ist.</span><span class="sxs-lookup"><span data-stu-id="9eea5-192">This method loads the list and determines whether the current item has an ID that is greater than 0.</span></span> <span data-ttu-id="9eea5-193">Wenn die ID nicht größer als 0 ist, wird angenommen, dass es nicht gültig ist und ein neues Listenelement erstellt.</span><span class="sxs-lookup"><span data-stu-id="9eea5-193">If the ID is not greater than 0, it assumes that it's not valid and creates a new list item.</span></span> <span data-ttu-id="9eea5-194">**SetProperties** -Methode verwendet, um Eigenschaften für das **ListItem** festzulegen, und legt dann die Eigenschaften für die Unterklasse mithilfe der **ReadProperties** -Methode.</span><span class="sxs-lookup"><span data-stu-id="9eea5-194">It uses the **SetProperties** method to set properties on the **ListItem** and then sets the properties on the subclass by using the **ReadProperties** method.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="9eea5-195">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="9eea5-195">See also</span></span>
<span data-ttu-id="9eea5-196"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9eea5-196"></span></span>

-  [<span data-ttu-id="9eea5-197">Zusammengesetzte Business-add-ins für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="9eea5-197">Composite business add-ins for SharePoint 2013 and SharePoint Online</span></span>](Composite-buisness-apps-for-SharePoint.md)
    
-  [<span data-ttu-id="9eea5-198">Core.ModifyPages-Beispiel</span><span class="sxs-lookup"><span data-stu-id="9eea5-198">Core.ModifyPages sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages)
    
-  [<span data-ttu-id="9eea5-199">Provisioning.Pages-Beispiel</span><span class="sxs-lookup"><span data-stu-id="9eea5-199">Provisioning.Pages sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages)
    
-  [<span data-ttu-id="9eea5-200">OfficeDevPnP.Core-Beispiel</span><span class="sxs-lookup"><span data-stu-id="9eea5-200">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
