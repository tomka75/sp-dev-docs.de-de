---
title: Verarbeiten von Listenelementereignissen im vom Anbieter gehosteten Add-In
description: "Stellen Sie programmgesteuert eine Liste bereit, erstellen und registrieren Sie den Listenelement-Ereignisempfänger, führen Sie das vom Anbieter gehostete SharePoint-Add-In aus und testen Sie den Empfänger. "
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 86238eba8d6ff9c506f8d6162295b26004a673cd
ms.sourcegitcommit: df82c72574631093a93f8a75ecbcb79cff765ea7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/28/2017
---
# <a name="handle-list-item-events-in-the-provider-hosted-add-in"></a><span data-ttu-id="33b9a-103">Verarbeiten von Listenelementereignissen in anbietergehosteten Add-Ins</span><span class="sxs-lookup"><span data-stu-id="33b9a-103">Handle list item events in the provider-hosted add-in</span></span>

<span data-ttu-id="33b9a-104">Dies ist der zehnte einer Reihe von Artikeln über die Grundlagen der Entwicklung von vom Anbieter gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln dieser Reihe vertraut, die Sie unter [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md#SP15createprovider_nextsteps) finden.</span><span class="sxs-lookup"><span data-stu-id="33b9a-104">This is the tenth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 

> [!NOTE]
> <span data-ttu-id="33b9a-105">Wenn Sie unsere Artikelreihe zum Thema anbietergehostete Add-Ins durchgearbeitet haben, haben Sie bereits eine Visual Studio-Lösung, die Sie für diesen Artikel verwenden können.</span><span class="sxs-lookup"><span data-stu-id="33b9a-105">If you have been working through this series about provider-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="33b9a-106">Sie können auch das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei BeforeRER.sln öffnen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-106">You can also download the repository at [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeRER.sln file.</span></span>

<span data-ttu-id="33b9a-107">In einem vorherigen Artikel dieser Reihe haben Sie gesehen, dass ein Auftrag bei der Auftragserteilung zur **Aufträge**-Tabelle der Unternehmensdatenbank und ein Element für diesen Auftrag automatisch zu der **Erwartete Lieferungen**-Liste hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="33b9a-107">You saw in an earlier article in this series that when an order is placed, it is added to the **Orders** table in the corporate database, and an item for it is automatically added to the **Expected Shipments** list.</span></span> <span data-ttu-id="33b9a-108">Wenn die Lieferung im lokalen Geschäft eintrifft, setzt ein Benutzer die Spalte **Angekommen** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-108">When it arrives at the local store, a user sets the **Arrived** column to **Yes**.</span></span> <span data-ttu-id="33b9a-109">Das Ändern eines Feldwerts für ein Element erstellt ein Element aktualisiert-Ereignis, für das Sie einen benutzerdefinierten Handler hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="33b9a-109">Changing a field value for an item creates an item updated event for which you can add a custom handler.</span></span> 

<span data-ttu-id="33b9a-110">In diesem Artikel erstellen Sie einen Handler für dieses Listenelement-Ereignis und stellen es dann programmgesteuert in der ersten Ausführungslogik des SharePoint-Add-Ins bereit.</span><span class="sxs-lookup"><span data-stu-id="33b9a-110">In this article, you create a handler for this list item event and then programmatically deploy it in the first-run logic of the SharePoint Add-in.</span></span> <span data-ttu-id="33b9a-111">Ihr Handler fügt das Element zur **Bestand**-Tabelle der Unternehmensdatenbank hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-111">Your handler adds the item into the **Inventory** table in the corporate database.</span></span> <span data-ttu-id="33b9a-112">Dann wird die **Zum Bestand hinzugefügt**-Spalte der **Erwartete Lieferungen**-Liste auf **Ja** gesetzt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-112">It then sets the **Added to Inventory** column of the **Expected Shipments** list to **Yes**.</span></span> <span data-ttu-id="33b9a-113">Sie erfahren auch, wie Sie das zweite Elementaktualisierungsereignis vermeiden, indem Sie eine unbegrenzte Serie Elementaktualisierungsereignisse auslösen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-113">You also learn how to prevent this second item updated event from setting off an infinite series of item updated events.</span></span>

## <a name="programmatically-deploy-the-expected-shipments-list"></a><span data-ttu-id="33b9a-114">Programmgesteuertes Bereitstellen der Liste „Erwartete Lieferungen“</span><span class="sxs-lookup"><span data-stu-id="33b9a-114">Programmatically deploy the Expected Shipments list</span></span>

> [!NOTE]
> <span data-ttu-id="33b9a-115">Die Einstellungen für Startprojekte in Visual Studio werden in der Regel nach jedem erneuten Öffnen der Lösung wieder auf die Standardwerte zurückgesetzt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-115">The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened.</span></span> <span data-ttu-id="33b9a-116">Wann immer Sie beim Durcharbeiten dieser Artikelreihe die Beispiellösung erneut öffnen, müssen Sie umgehend die folgenden Schritte durchführen:</span><span class="sxs-lookup"><span data-stu-id="33b9a-116">Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> 
> 1. <span data-ttu-id="33b9a-117">Klicken Sie oben im **Projektmappen-Explorer** mit der rechten Maustaste auf den Lösungsknoten, und wählen Sie die Option **Startprojekte festlegen** aus.</span><span class="sxs-lookup"><span data-stu-id="33b9a-117">Right-click the solution node at the top of **Solution Explorer**, and then select **Set startup projects**.</span></span>  
> 2. <span data-ttu-id="33b9a-118">Stellen Sie sicher, dass alle drei Projekte in der Spalte **Aktion** auf **Start** festgelegt sind.</span><span class="sxs-lookup"><span data-stu-id="33b9a-118">Ensure that all three projects are set to **Start** in the **Action** column.</span></span>

1. <span data-ttu-id="33b9a-119">Öffnen Sie im **Projektmappen-Explorer** die Datei Utilities\SharePointComponentDeployer.cs im Projekt **ChainStoreWeb**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-119">In **Solution Explorer**, open the Utilities\SharePointComponentDeployer.cs file in the **ChainStoreWeb** project.</span></span> <span data-ttu-id="33b9a-120">Fügen Sie der Klasse `SharePointComponentDeployer` die folgende Methode hinzu:</span><span class="sxs-lookup"><span data-stu-id="33b9a-120">Add the following method to the `SharePointComponentDeployer` class.</span></span> 

     ```C#
      private static void CreateExpectedShipmentsList()
     {
        using (var clientContext = sPContext.CreateUserClientContextForSPHost())
        {
        var query = from list in clientContext.Web.Lists
                where list.Title == "Expected Shipments"
                select list;
        IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
        clientContext.ExecuteQuery();

        if (matchingLists.Count() == 0)
        {
            ListCreationInformation listInfo = new ListCreationInformation();
            listInfo.Title = "Expected Shipments";
            listInfo.TemplateType = (int)ListTemplateType.GenericList;
            listInfo.Url = "Lists/ExpectedShipments";
            List expectedShipmentsList = clientContext.Web.Lists.Add(listInfo);

            Field field = expectedShipmentsList.Fields.GetByInternalNameOrTitle("Title");
            field.Title = "Product";
            field.Update();

            expectedShipmentsList.Fields.AddFieldAsXml("<Field DisplayName='Supplier'" 
                                    + " Type='Text' />", 
                                    true,
                                    AddFieldOptions.DefaultValue);
            expectedShipmentsList.Fields.AddFieldAsXml("<Field DisplayName='Quantity'" 
                                    + " Type='Number'" 
                                    + " Required='TRUE' >" 
                                    + "<Default>1</Default></Field>",
                                    true, 
                                    AddFieldOptions.DefaultValue);
            expectedShipmentsList.Fields.AddFieldAsXml("<Field DisplayName='Arrived'" 
                                   + " Type='Boolean'"
                                   + " ShowInNewForm='FALSE'>"
                                   + "<Default>FALSE</Default></Field>",
                                    true, 
                                    AddFieldOptions.DefaultValue);
            expectedShipmentsList.Fields.AddFieldAsXml("<Field DisplayName='Added to Inventory'" 
                                    + " Type='Boolean'" 
                                    + " ShowInNewForm='FALSE'>"
                                    + "<Default>FALSE</Default></Field>", 
                                    true, 
                                    AddFieldOptions.DefaultValue);

            clientContext.ExecuteQuery();
        }
         }
     }
     ```

    <span data-ttu-id="33b9a-121">Der Code fügt nur Funktionen hinzu, die Sie bereits in vorherigen Artikeln dieser Reihe kennengelernt haben, beachten Sie jedoch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="33b9a-121">This code doesn't introduce any functionality that you haven't already seen in a previous article of this series, but note the following:</span></span>
   
    - <span data-ttu-id="33b9a-122">Das Attribut **Required** des Felds **Menge** wird auf **TRUE** festgelegt, sodass das Feld immer einen Wert enthalten muss.</span><span class="sxs-lookup"><span data-stu-id="33b9a-122">It sets the **Required** attribute of the **Quantity** field to **TRUE** so the field must always have a value.</span></span> <span data-ttu-id="33b9a-123">Der Standardwert wird dann auf 1 festgelegt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-123">It then sets the default value to 1.</span></span>
   
    - <span data-ttu-id="33b9a-124">Die Felder **Angekommen** und **Zum Bestand hinzugefügt** sind im Formular für ein neues Element ausgeblendet.</span><span class="sxs-lookup"><span data-stu-id="33b9a-124">The **Arrived** and **Added to Inventory** fields are hidden on the New Item form.</span></span>
   
    - <span data-ttu-id="33b9a-125">Idealerweise wäre das Feld **Zum Bestand hinzugefügt** auch auf dem Formular Element bearbeiten ausgeblendet, da es nur in **Ja** geändert werden sollte, wenn der aktualisierte Ereignishandler das Element zum ersten Mal zu der Tabelle **Bestand** hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-125">Ideally, the **Added to Inventory** field would also be hidden on the Edit Item form because it should only be changed to **Yes** when the item updated event handler has first added the item to the corporate **Inventory** table.</span></span> <span data-ttu-id="33b9a-126">Aus technischen Gründen, die wir in einem späteren Schritt erläutern möchten, muss ein Feld im Formular Element bearbeiten angezeigt werden, wenn es in einem Elementaktualisierungsereignis-Handler programmgesteuert ausgefüllt werden soll.</span><span class="sxs-lookup"><span data-stu-id="33b9a-126">For technical reasons that we'll explain in a later step, a field has to be visible in the Edit Item form if we want to programmatically write to it in an item updated event handler.</span></span>


2. <span data-ttu-id="33b9a-127">Fügen Sie in der Methode **DeployChainStoreComponentsToHostWeb** die folgende Zeile direkt über der Zeile `RemoteTenantVersion = localTenantVersion` ein.</span><span class="sxs-lookup"><span data-stu-id="33b9a-127">In the **DeployChainStoreComponentsToHostWeb** method, add the following line, just above the line `RemoteTenantVersion = localTenantVersion`.</span></span>
    
    ```C#
      CreateExpectedShipmentsList();
    ```

## <a name="create-the-list-item-event-receiver"></a><span data-ttu-id="33b9a-128">Erstellen des Listenelement-Ereignisempfängers</span><span class="sxs-lookup"><span data-stu-id="33b9a-128">Create the list item event receiver</span></span>

> [!NOTE]
> <span data-ttu-id="33b9a-129">Wenn Sie diese Reihe von Artikeln durchgearbeitet haben, haben Sie bereits Ihre Entwicklungsumgebung für das Debuggen von Remote-Ereignisempfängern konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="33b9a-129">If you have been working through this series of articles, you have already configured your development environment for debugging remote event receivers.</span></span> <span data-ttu-id="33b9a-130">Falls dies nicht der Fall ist, lesen Sie bitte [Konfigurieren der Lösung für das Debuggen des Ereignisempfängers](handle-add-in-events-in-the-provider-hosted-add-in.md#RERDebug), bevor Sie mit diesem Thema fortfahren.</span><span class="sxs-lookup"><span data-stu-id="33b9a-130">If you have not done that, see [Configure the solution for event receiver debugging](handle-add-in-events-in-the-provider-hosted-add-in.md#RERDebug) before you go any further in this topic.</span></span>

<span data-ttu-id="33b9a-131">Die Office Developer Tools für Visual Studio enthalten eine **Remote-Ereignisempfänger**-Element, das zu einer SharePoint-Add-In-Lösung hinzugefügt werden kann.</span><span class="sxs-lookup"><span data-stu-id="33b9a-131">The Office Developer Tools for Visual Studio includes a **Remote Event Receiver** item that can be added to a SharePoint Add-in solution.</span></span> <span data-ttu-id="33b9a-132">Als dieser Artikel geschrieben wurde, nahm dieses Element jedoch an, dass sich die Liste (mit der der Empfänger registriert wird) im Add-In-Web befindet, und daher erstellen die Tools ein Add-In-Web mit einigen SharePoint-Artefakten.</span><span class="sxs-lookup"><span data-stu-id="33b9a-132">However, at the time this article was written, this project item assumes that the list (with which the receiver will be registered) is on the add-in web, and consequently the tools create an add-in web and some SharePoint artifacts in it.</span></span> <span data-ttu-id="33b9a-133">Der Empfänger für das Chain Store-Add-In wird (in einem späteren Schritt) mit der Liste **Erwartete Lieferungen** im Hostweb registriert, sodass das Add-In kein Add-In-Web benötigt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-133">But the receiver for the Chain Store add-in is going to be registered (in a later step) with the **Expected Shipments** list on the host web, so the add-in does not need an add-in web.</span></span> <span data-ttu-id="33b9a-134">(Eine Auffrischung zur Unterscheidung zwischen Add-In-Webs und Hostwebs finden Sie unter [SharePoint-Add-Ins](sharepoint-add-ins.md).)</span><span class="sxs-lookup"><span data-stu-id="33b9a-134">(For a reminder of the distinction between add-in webs and host webs, see [SharePoint Add-ins](sharepoint-add-ins.md).)</span></span>
 
> [!NOTE]
> <span data-ttu-id="33b9a-135">Listen- und Listenelement-Ereignisempfänger heißen Remoteereignisempfänger (RER), da sich ihr Code remote von SharePoint in der Cloud oder auf einem lokalen Server außerhalb der SharePoint-Farm befindet.</span><span class="sxs-lookup"><span data-stu-id="33b9a-135">List and list item event receivers are called remote event receivers (RER) because their code is remote from SharePoint, either in the cloud or in an on-premises server outside the SharePoint farm.</span></span> <span data-ttu-id="33b9a-136">Allerdings befinden sich die Ereignisse, die diese auslösen, in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="33b9a-136">However, the events that trigger them are in SharePoint.</span></span>

1. <span data-ttu-id="33b9a-137">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Ordner **Dienste** im Projekt **ChainStoreWeb**, und wählen Sie **Hinzufügen** > **WCF-Dienst Service** aus.</span><span class="sxs-lookup"><span data-stu-id="33b9a-137">In **Solution Explorer**, right-click the **Services** folder in the **ChainStoreWeb** project, and select **Add** > **WCF Service**.</span></span>

2. <span data-ttu-id="33b9a-138">Wenn Sie aufgefordert werden, nennen Sie den Dienst **RemoteEventReceiver1**, und wählen Sie dann **OK**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-138">When prompted, name the service **RemoteEventReceiver1**, and then select **OK**.</span></span> 

3. <span data-ttu-id="33b9a-139">Die Tools erstellen eine Schnittstellendatei, eine \*.svc-Datei und eine CodeBehind-Datei.</span><span class="sxs-lookup"><span data-stu-id="33b9a-139">The tools create an interface file, an \*.svc file, and a code-behind file.</span></span> <span data-ttu-id="33b9a-140">Die Benutzeroberflächendatei IRemoteEventReceiver1.cs ist nicht erforderlich und kann gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="33b9a-140">We don't need the interface file IRemoteEventReceiver1.cs, so delete it.</span></span> <span data-ttu-id="33b9a-141">(Möglicherweise wurde sie von den Tools automatisch geöffnet, falls dies der Fall ist, schließen und löschen Sie sie.)</span><span class="sxs-lookup"><span data-stu-id="33b9a-141">(The tools may have opened it automatically; if so, close and delete it.)</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="33b9a-142">Beim Erstellen des Add-In-Ereignisempfängers für die installierten und deinstallierten Ereignisse in einem früheren Artikel dieser Reihe wurden die URLs von den Office Developer Tools für Visual Studio zu der Manifestdatei hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-142">When you created the add-in event receivers for the installed and uninstalling events in an earlier article in this series, the Office Developer Tools for Visual Studio added their URLs to the app manifest file.</span></span> <span data-ttu-id="33b9a-143">Listen- und Listenelement-Ereignisempfänger werden nicht im App-Manifest registriert.</span><span class="sxs-lookup"><span data-stu-id="33b9a-143">List and list item event receivers are not registered in the app manifest.</span></span> <span data-ttu-id="33b9a-144">Stattdessen werden sie (bei einem vom Anbieter gehosteten Add-in) programmgesteuert registriert.</span><span class="sxs-lookup"><span data-stu-id="33b9a-144">Instead, they are registered (in a provider-hosted add-in) programmatically.</span></span> <span data-ttu-id="33b9a-145">Dies wird in einem späteren Schritt behandelt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-145">You'll do that in a later step.</span></span>

4. <span data-ttu-id="33b9a-146">Öffnen Sie die CodeBehind-Datei RemoteEventReceiver1.svc.cs.</span><span class="sxs-lookup"><span data-stu-id="33b9a-146">Open the code-behind file RemoteEventReceiver1.svc.cs.</span></span> <span data-ttu-id="33b9a-147">Ersetzen Sie den gesamten Inhalt durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="33b9a-147">Replace its entire contents with the following code.</span></span> 

    ```C#
      using System;
    using System.Collections.Generic;
    using Microsoft.SharePoint.Client;
    using Microsoft.SharePoint.Client.EventReceivers;
    using System.Data.SqlClient;
    using System.Data;
    using ChainStoreWeb.Utilities;

    namespace ChainStoreWeb.Services
    {
        public class RemoteEventReceiver1 : IRemoteEventService
        {
        /// <summary>
        /// Handles events that occur before an action occurs, 
        /// such as when a user is adding or deleting a list item.
        /// </summary>
        /// <param name="properties">Holds information about the remote event.</param>
        /// <returns>Holds information returned from the remote event.</returns>
        public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {
            throw new NotImplementedException();
        }

        /// <summary>
        /// Handles events that occur after an action occurs, 
        /// such as after a user adds an item to a list or deletes an item from a list.
        /// </summary>
        /// <param name="properties">Holds information about the remote event.</param>
        public void ProcessOneWayEvent(SPRemoteEventProperties properties)
        {

        }
        }
    }
    ```

   <span data-ttu-id="33b9a-148">Beachten Sie Folgendes zu diesem Code:</span><span class="sxs-lookup"><span data-stu-id="33b9a-148">Note the following about this code:</span></span>
    
   - <span data-ttu-id="33b9a-149">Die Schnittstelle `IRemoteEventService` ist im Namespace **Microsoft.SharePoint.Client.EventReceivers** definiert.</span><span class="sxs-lookup"><span data-stu-id="33b9a-149">The interface `IRemoteEventService` is defined in the **Microsoft.SharePoint.Client.EventReceivers** namespace.</span></span>
    
   - <span data-ttu-id="33b9a-150">Im ChainStore-Add-In werden keine „Bevor“-Ereignisse verarbeitet, aber die Methode **ProcessEvent** ist für die Schnittstelle `IRemoteEventService` erforderlich.</span><span class="sxs-lookup"><span data-stu-id="33b9a-150">There won't be any "before" events handled in the Chain Store add-in, but the **ProcessEvent** method is required by the `IRemoteEventService` interface.</span></span>

5. <span data-ttu-id="33b9a-151">Fügen Sie den folgenden Code zur **ProcessOneWayEvent**-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-151">Add the following code to the **ProcessOneWayEvent** method.</span></span> <span data-ttu-id="33b9a-152">Beachten Sie, dass das **ItemUpdated**-Ereignis das einzige ist, das in diesem Beispiel behandelt wird, daher hätten wir eine einfache **Wenn**-Struktur anstelle einer **Wechseln**-Struktur verwenden können.</span><span class="sxs-lookup"><span data-stu-id="33b9a-152">Note that the **ItemUpdated** event is the only one that this sample will handle, so we could have used a simple **if** structure instead of a **switch**.</span></span> <span data-ttu-id="33b9a-153">Aber Ereignisempfänger verarbeiten in der Regel mehrere Ereignisse, daher möchten wir die Vorgehensweise zeigen, die Sie als SharePoint-Add-In-Entwickler am häufigsten in Ihren Ereignishandlern verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="33b9a-153">But event receivers typically handle multiple events, so we want you to see the pattern you'll most commonly be using in your event handlers as a SharePoint add-in developer.</span></span>
    
    ```C#
      switch (properties.EventType)
    {
        case SPRemoteEventType.ItemUpdated:

        // TODO12: Handle the item updated event.

        break;
    }  
    ```

6. <span data-ttu-id="33b9a-154">Ersetzen Sie `TODO12` durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="33b9a-154">Replace `TODO12` with the following code.</span></span> <span data-ttu-id="33b9a-155">Auch hier verwenden wir eine **switch**-Struktur, obwohl eine einfache **if**-Struktur ausreichend wäre, da Sie das typische Muster in SharePoint-Ereignisempfängern sehen sollen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-155">Again, here, we are using a **switch** structure when a simple **if** structure would do because we want you to see the common pattern in SharePoint event receivers.</span></span>
    
    ```C#
      switch (properties.ItemEventProperties.ListTitle)
    {
        case "Expected Shipments":

        // TODO13: Handle the arrival of a shipment.

        break;
    }
    ```

7. <span data-ttu-id="33b9a-156">Der Code, der auf den Eingang einer Lieferung reagiert, sollten zwei Aufgaben ausführen:</span><span class="sxs-lookup"><span data-stu-id="33b9a-156">The code that responds to the arrival of a shipment should do two things:</span></span>
    
   - <span data-ttu-id="33b9a-157">Hinzufügen des Elements, das im Geschäft eingetroffen ist, zum Unternehmensbestand</span><span class="sxs-lookup"><span data-stu-id="33b9a-157">Add the item that has arrived at the store into the corporate inventory.</span></span>
    
   - <span data-ttu-id="33b9a-158">Setzen Sie das **Zum Bestand hinzugefügt**-Feld der **Erwartete Lieferungen**-Liste auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-158">Set the **Added to Inventory** field on the **Expected Shipments** list to **Yes**.</span></span> <span data-ttu-id="33b9a-159">Dies geschieht normalerweise nur, wenn das Element erfolgreich zum Bestand hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="33b9a-159">But this should only happen if the item was successfully added to the inventory.</span></span>
    
   <span data-ttu-id="33b9a-160">Fügen Sie den folgenden Code anstelle von `TODO13` hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-160">Add the following code in place of `TODO13`.</span></span> <span data-ttu-id="33b9a-161">Die beiden Methoden `TryUpdateInventory` und `RecordInventoryUpdateLocally` werden in späteren Schritten erstellt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-161">The two methods, `TryUpdateInventory` and `RecordInventoryUpdateLocally` are created in later steps.</span></span>

    ```C#
      bool updateComplete = TryUpdateInventory(properties);
    if (updateComplete)
    {
        RecordInventoryUpdateLocally(properties);
    }
    ```


8. <span data-ttu-id="33b9a-162">Die **ProcessOneWayEvent**-Methode sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="33b9a-162">The **ProcessOneWayEvent** method should now look like the following:</span></span>

    ```C#
      public void ProcessOneWayEvent(SPRemoteEventProperties properties)
    {
        switch (properties.EventType)
        {
        case SPRemoteEventType.ItemUpdated:

            switch (properties.ItemEventProperties.ListTitle)
            {
            case "Expected Shipments":
                bool updateComplete = UpdateInventory(properties);
                if (updateComplete)
                {
                RecordInventoryUpdateLocally(properties);
                }
                break;
            }
            break;
        }          
    }
    ```

9. <span data-ttu-id="33b9a-163">Fügen Sie der Klasse `RemoteEventReceiver1` die unten aufgeführte Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-163">Add the following method to the `RemoteEventReceiver1` class.</span></span>
    
    ```C#
      private bool TryUpdateInventory(SPRemoteEventProperties properties)
    {
        bool successFlag = false;

        // TODO14: Test whether the list item is changing because the product has arrived
        // or for some other reason. If the former, add it to the inventory and set the success flag
        // to true.     

        return successFlag;
    }
    ```

10. <span data-ttu-id="33b9a-164">Es gibt fünf Spalten in der **Lieferung erwartet**-Liste, aber bei den meisten Arten der Updates möchten wir nicht, dass der Handler reagiert.</span><span class="sxs-lookup"><span data-stu-id="33b9a-164">There are five columns on the **Expected Shipments** list, but we don't want the handler to react to most kinds of updates to an item.</span></span> <span data-ttu-id="33b9a-165">Wenn ein Benutzer z.B. die Schreibweise des Namens eines Lieferanten korrigiert, wird das Elementaktualisierungsereignis ausgelöst, aber unser Handler sollte nicht reagieren.</span><span class="sxs-lookup"><span data-stu-id="33b9a-165">For example, if a user corrects the spelling of a supplier's name, the item updated event is triggered, but our handler should do nothing.</span></span> <span data-ttu-id="33b9a-166">Der Handler sollte nur reagieren, wenn das **Angekommen**-Feld auf **Ja** gesetzt wurde.</span><span class="sxs-lookup"><span data-stu-id="33b9a-166">The handler should only act when the **Arrived** field has just been set to **Yes**.</span></span> 
    
    <span data-ttu-id="33b9a-167">Es gibt eine weitere Bedingung, die getestet werden muss.</span><span class="sxs-lookup"><span data-stu-id="33b9a-167">There's another condition that needs to be tested.</span></span> <span data-ttu-id="33b9a-168">Nehmen wir einmal an, **Angekommen** wurde auf **Ja** festgelegt und das Produkt im Element wird zum Bestand hinzugefügt (und **Zum Bestand hinzugefügt** ist auf **Ja**) festgelegt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-168">Suppose **Arrived** is set to **Yes** and the product in the item is added to inventory (and **Added to Inventory** is set to **Yes**).</span></span> <span data-ttu-id="33b9a-169">Später ändert ein Benutzer jedoch versehentlich das **Angekommen**-Feld einer Lieferung zurück auf **Nein**. Später behebt er den Fehler, indem er es erneut auf **Ja** setzt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-169">But later a user mistakenly changes the **Arrived** field of a shipment back to **No** and then fixes his mistake by setting it again to **Arrived**.</span></span> <span data-ttu-id="33b9a-170">Sowohl der Fehler als auch die Korrektur lösen das Elementaktualisierungsereignis aus.</span><span class="sxs-lookup"><span data-stu-id="33b9a-170">Both the mistake and the fix trigger the item updated event.</span></span> <span data-ttu-id="33b9a-171">Der Handler reagiert nicht auf den Fehler, da er nur reagiert, wenn **Angekommen** auf **Ja** festgelegt ist, aber er reagiert auf die Korrektur, bei der **Angekommen** zurück auf **Ja** gesetzt wird, sodass das gleiche Produkt und die gleiche Menge ein zweites Mal zum Bestand hinzugefügt würden.</span><span class="sxs-lookup"><span data-stu-id="33b9a-171">The handler won't react to the mistake because it only acts when **Arrived** is **Yes**, but it would react to the fix that sets **Arrived** back to **Yes**, so the same product and quantity would get added into the inventory a second time.</span></span> <span data-ttu-id="33b9a-172">Aus diesem Grund sollte der Handler nur reagieren, wenn der Wert **Zum Bestand hinzugefügt** auf **Nein** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="33b9a-172">For this reason, the handler should only act when the **Added to Inventory** value is **No**.</span></span> 
    
    <span data-ttu-id="33b9a-173">Daher muss der Handler wissen, welche Werte diese Felder besitzen, nachdem der Benutzer das Element aktualisiert hat.</span><span class="sxs-lookup"><span data-stu-id="33b9a-173">Therefore, the handler needs to know what the values of these fields are just after the user updates the item.</span></span> <span data-ttu-id="33b9a-174">Das **SPRemoteEventProperties**-Objekt verfügt über die **ItemEventProperties**-Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="33b9a-174">The **SPRemoteEventProperties** object has an **ItemEventProperties** property.</span></span> <span data-ttu-id="33b9a-175">Es enthält aber auch eine indizierte **AfterProperties**-Eigenschaft mit den Werten der Felder des aktualisierten Elements.</span><span class="sxs-lookup"><span data-stu-id="33b9a-175">And, in turn, it has an indexed **AfterProperties** property that holds the values of the fields in the updated item.</span></span> <span data-ttu-id="33b9a-176">Der folgende Code verwendet diese Eigenschaften, um zu testen, ob der Handler reagieren soll.</span><span class="sxs-lookup"><span data-stu-id="33b9a-176">The following code uses these properties to test whether the handler should react.</span></span> <span data-ttu-id="33b9a-177">Setzen Sie dies an die Stelle von `TODO14`.</span><span class="sxs-lookup"><span data-stu-id="33b9a-177">Put this in place of `TODO14`.</span></span>

     ```C#
      var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);
    var addedToInventory = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Added_x0020_to_x0020_Inventory"]);

    if (arrived &amp;&amp; !addedToInventory)
    {

        // TODO15: Add the item to inventory

        successFlag = true;
    }
     ```

11. <span data-ttu-id="33b9a-178">Ersetzen Sie `TODO15` durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="33b9a-178">Replace `TODO15` with the following code.</span></span> 

     ```C#
      using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
    using (SqlCommand cmd = conn.CreateCommand())
    {
        conn.Open();
        cmd.CommandText = "UpdateInventory";
        cmd.CommandType = CommandType.StoredProcedure;
        SqlParameter tenant = cmd.Parameters.Add("@Tenant", SqlDbType.NVarChar);
        tenant.Value = properties.ItemEventProperties.WebUrl + "/";
        SqlParameter product = cmd.Parameters.Add("@ItemName", SqlDbType.NVarChar, 50);
        product.Value = properties.ItemEventProperties.AfterProperties["Title"]; // not "Product"
        SqlParameter quantity = cmd.Parameters.Add("@Quantity", SqlDbType.SmallInt);
        quantity.Value = Convert.ToUInt16(properties.ItemEventProperties.AfterProperties["Quantity"]);
        cmd.ExecuteNonQuery();
    }
     ```

    <span data-ttu-id="33b9a-179">Da es sich hierbei hauptsächlich um SQL- und ASP.NET-Programmierung handelt, werden wir nicht näher darauf eingehen, aber beachten Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="33b9a-179">This is mainly SQL and ASP.NET programming, so we don't discuss it in detail, but note:</span></span>
    
    - <span data-ttu-id="33b9a-180">Wir verwenden die Eigenschaft **ItemEventProperties.WebUrl**, um den Mandantennamen abzurufen, der der Hostweb-URL entspricht.</span><span class="sxs-lookup"><span data-stu-id="33b9a-180">We use the **ItemEventProperties.WebUrl** property to get the tenant name, which is the host web URL.</span></span>

    - <span data-ttu-id="33b9a-181">Wir verwenden erneut **AfterProperties**, um die Werte für Produktname und Menge abzurufen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-181">We use the **AfterProperties** again to get the values of the product name and quantity.</span></span>
    
    - <span data-ttu-id="33b9a-182">Wir bezeichnen das Produktnamensfeld als „Titel“, obwohl der Anzeigename auf „Produkt“ geändert wurde (in der Methode **CreateExpectedShipmentsList**), da auf Felder immer mit den internen Namen verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="33b9a-182">We refer to the product name field as "Title", even though the display name was changed to "Product" (in the  **CreateExpectedShipmentsList** method) because fields are always referred to by their internal names.</span></span>
 

12. <span data-ttu-id="33b9a-183">Wir sind noch nicht mit der **TryUpdateInventory**-Methode fertig, aber an diesem Punkt sollte sie wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-183">We are not finished with the **TryUpdateInventory** method yet, but at this point it should look like the following.</span></span>
    
     ```C#
      private bool TryUpdateInventory(SPRemoteEventProperties properties)
    {
        bool successFlag = false;

        var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);
        var addedToInventory = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Added_x0020_to_x0020_Inventory"]);

        if (arrived &amp;&amp; !addedToInventory)
        {
        using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
        using (SqlCommand cmd = conn.CreateCommand())
        {
            conn.Open();
            cmd.CommandText = "UpdateInventory";
            cmd.CommandType = CommandType.StoredProcedure;
            SqlParameter tenant = cmd.Parameters.Add("@Tenant", SqlDbType.NVarChar);
            tenant.Value = properties.ItemEventProperties.WebUrl + "/";
            SqlParameter product = cmd.Parameters.Add("@ItemName", SqlDbType.NVarChar, 50);
            product.Value = properties.ItemEventProperties.AfterProperties["Title"]; // not "Product"
            SqlParameter quantity = cmd.Parameters.Add("@Quantity", SqlDbType.SmallInt);
            quantity.Value = Convert.ToUInt16(properties.ItemEventProperties.AfterProperties["Quantity"]);
            cmd.ExecuteNonQuery();
        }            
        successFlag = true;
        }  
        return successFlag;
    }
     ```

13. <span data-ttu-id="33b9a-184">Wenn die **TryUpdateInventory**-Methode **true** zurückgibt, ruft der Handler eine Methode (noch nicht geschrieben) auf, die das gleiche Element in der **Lieferung erwartet**-Liste aktualisiert, indem das Feld **Zum Bestand hinzugefügt** auf **Ja** gesetzt wird.</span><span class="sxs-lookup"><span data-stu-id="33b9a-184">When the **TryUpdateInventory** method returns **true**, our handler calls a method (not yet written) that updates the same item in the **Expected Shipments** list by setting the **Added to Inventory** field to **Yes**.</span></span> <span data-ttu-id="33b9a-185">Dies ist wiederum ein Elementaktualisierungsereignis, sodass der Handler erneut aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="33b9a-185">This is itself an item update event, so the handler is called again.</span></span> <span data-ttu-id="33b9a-186">(Die Tatsache, dass das **Zum Bestand hinzugefügt**-Feld nun auf **Ja** gesetzt ist, verhindert, dass der Handler die gleiche Lieferung ein zweites Mal zum Bestand hinzufügt, aber der Handler wird trotzdem aufgerufen.)</span><span class="sxs-lookup"><span data-stu-id="33b9a-186">(The fact that the **Added to Inventory** field is now **Yes** prevents the handler from adding the same shipment to inventory a second time, but the handler is still called.)</span></span> 
    
    <span data-ttu-id="33b9a-187">SharePoint verhält sich ein wenig anders, wenn das Ereignis für aktualisierte Elemente durch eine programmgesteuerte Aktualisierung ausgelöst wird: *Es schließt nur die Felder in __AfterProperties__ ein, die bei der Aktualisierung geändert wurden.*</span><span class="sxs-lookup"><span data-stu-id="33b9a-187">SharePoint behaves a little differently when the item updated event is triggered by a programmatic update: *it only includes in the __AfterProperties__ the fields that changed in the update.*</span></span> <span data-ttu-id="33b9a-188">Das heißt, dass das Feld **Angekommen** nicht vorhanden ist, da nur das Feld **Zum Bestand hinzugefügt** geändert wurde.</span><span class="sxs-lookup"><span data-stu-id="33b9a-188">So the **Arrived** field won't be present because only the **Added to Inventory** field changed.</span></span> 
    
    <span data-ttu-id="33b9a-189"> Die Zeile –</span><span class="sxs-lookup"><span data-stu-id="33b9a-189">The line...</span></span>
    
    `var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);`
    
    <span data-ttu-id="33b9a-190">löst eine **KeyNotFoundException** aus.</span><span class="sxs-lookup"><span data-stu-id="33b9a-190">...throws a **KeyNotFoundException**.</span></span> 
    
    <span data-ttu-id="33b9a-191">Es gibt mehre Möglichkeiten dieses Problem  zu beheben.</span><span class="sxs-lookup"><span data-stu-id="33b9a-191">There is more than one way to resolve this problem.</span></span> <span data-ttu-id="33b9a-192">In diesem Beispiel fangen wir die Ausnahme ab und verwenden den **catch**-Block, um sicherzustellen, dass `successFlag` auf **false** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="33b9a-192">In this sample we are going to catch the exception and use the **catch** block to ensure that the `successFlag` is set to **false**.</span></span> <span data-ttu-id="33b9a-193">Auf diese Weise wird sichergestellt, dass das Element nicht ein drittes Mal aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="33b9a-193">Doing this ensures that the item isn't updated a third time.</span></span>
    
    <span data-ttu-id="33b9a-194">Platzieren Sie alles, was sich in der Methode zwischen der ersten Zeile, `bool successFlag = false;`, und der letzten Zeile, `return successFlag;`, befindet, in einem **try**-Block.</span><span class="sxs-lookup"><span data-stu-id="33b9a-194">Put everything in the method that is between the first line `bool successFlag = false;` and the last line `return successFlag;` in a **try** block.</span></span>
    
14. <span data-ttu-id="33b9a-195">Fügen Sie den folgenden **catch**-Block direkt unterhalb des **try**-Blocks hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-195">Add the following **catch** block just under the **try** block.</span></span>
    
     ```C#
      catch (KeyNotFoundException)
    {
        successFlag = false;
    }
     ```

    > [!NOTE]
    > <span data-ttu-id="33b9a-196">Die **KeyNotFoundException** ist auch ein Grund dafür, dass das **Zum Bestand hinzugefügt**-Feld im Formular Element bearbeiten angezeigt werden muss.</span><span class="sxs-lookup"><span data-stu-id="33b9a-196">The **KeyNotFoundException** is also the reason why we have to leave the **Added to Inventory** field visible on the Edit Item form.</span></span> <span data-ttu-id="33b9a-197">SharePoint bezieht keine Felder mit ein, die im Formular Element bearbeiten in **AfterProperties** ausgeblendet sind.</span><span class="sxs-lookup"><span data-stu-id="33b9a-197">SharePoint does not include fields that are hidden on the Edit Item form in **AfterProperties**.</span></span>

15. <span data-ttu-id="33b9a-198">Die gesamte Methode sollte jetzt wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-198">The entire method should now look like the following.</span></span>

     ```C#
      private bool TryUpdateInventory(SPRemoteEventProperties properties)
    {
        bool successFlag = false;

        try 
        {
        var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);
        var addedToInventory = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Added_x0020_to_x0020_Inventory"]);

        if (arrived &amp;&amp; !addedToInventory)
        {
            using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
            using (SqlCommand cmd = conn.CreateCommand())
            {
            conn.Open();
            cmd.CommandText = "UpdateInventory";
            cmd.CommandType = CommandType.StoredProcedure;
            SqlParameter tenant = cmd.Parameters.Add("@Tenant", SqlDbType.NVarChar);
            tenant.Value = properties.ItemEventProperties.WebUrl + "/";
            SqlParameter product = cmd.Parameters.Add("@ItemName", SqlDbType.NVarChar, 50);
            product.Value = properties.ItemEventProperties.AfterProperties["Title"]; // not "Product"
            SqlParameter quantity = cmd.Parameters.Add("@Quantity", SqlDbType.SmallInt);
            quantity.Value = Convert.ToUInt16(properties.ItemEventProperties.AfterProperties["Quantity"]);
            cmd.ExecuteNonQuery();
            }            
            successFlag = true;
        }  
        }
        catch (KeyNotFoundException)
        {
        successFlag = false;
        }
        return successFlag;
    }
     ```

16. <span data-ttu-id="33b9a-199">Fügen Sie der Klasse `RemoteEventReceiver1` die unten aufgeführte Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-199">Add the following method to the `RemoteEventReceiver1` class.</span></span> 

     ```C#
      private void RecordInventoryUpdateLocally(SPRemoteEventProperties properties)
    {
        using (ClientContext clientContext = TokenHelper.CreateRemoteEventReceiverClientContext(properties))
        {
        List expectedShipmentslist = clientContext.Web.Lists.GetByTitle(properties.ItemEventProperties.ListTitle);
        ListItem arrivedItem = expectedShipmentslist.GetItemById(properties.ItemEventProperties.ListItemId);
        arrivedItem["Added_x0020_to_x0020_Inventory"] = true;
        arrivedItem.Update();
        clientContext.ExecuteQuery();
        }
    }
     ```

    <span data-ttu-id="33b9a-200">Bis hierhin ist das Codemuster aus früheren Artikeln dieser Reihe bekannt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-200">By now this pattern of code is familiar from earlier articles in this series.</span></span> <span data-ttu-id="33b9a-201">Beachten Sie jedoch einen Unterschied:</span><span class="sxs-lookup"><span data-stu-id="33b9a-201">But note one difference:</span></span>
    
    - <span data-ttu-id="33b9a-202">Der Code erhält das **ClientContext**- Objekt durch Aufrufen der **TokenHelper.CreateRemoteEventReceiverClientContext**-Methode anstelle der ** SharePointContext.CreateUserClientContextForSPHost**-Methode, wie wir sie für den Code verwendet haben, der SharePoint über Seiten abgerufen hat, wie beispielsweise die Seite "EmployeeAdder".</span><span class="sxs-lookup"><span data-stu-id="33b9a-202">The code gets the **ClientContext** object by calling **TokenHelper.CreateRemoteEventReceiverClientContext** method instead of the **SharePointContext.CreateUserClientContextForSPHost** method as we used in code that called into SharePoint from pages, such as the EmployeeAdder page.</span></span> 
    
    - <span data-ttu-id="33b9a-203">Der Hauptgrund für die beiden verschiedenen Methoden zum Abrufen eines **ClientContext**-Objekts ist, dass SharePoint die für die Erstellung eines solchen Objekts benötigten Informationen anders zu Ereignisempfängern weiterleitet als wenn SharePoint diese Informationen an Seiten übergibt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-203">The primary reason for having different methods to get a **ClientContext** object is that SharePoint passes the information needed to create such objects differently to event receivers from how it passes it to pages.</span></span> <span data-ttu-id="33b9a-204">Für Ereignisempfänger gibt SharePoint ein **SPRemoteEventProperties**-Objekt weiter, aber für Seiten übergibt SharePoint ein spezielles Feld, das als Kontexttoken bezeichnet wird, in den Textkörper der Anforderung, die die Add-In-Seite startet.</span><span class="sxs-lookup"><span data-stu-id="33b9a-204">For event receivers, it passes an **SPRemoteEventProperties** object, but for pages it passes a special field, called a context token, in the body of the request that launches the add-in page.</span></span>

17. <span data-ttu-id="33b9a-205">Speichern und schließen Sie die Datei mit dem Empfängercode.</span><span class="sxs-lookup"><span data-stu-id="33b9a-205">Save and close the receiver code file.</span></span>
    
## <a name="register-the-receiver"></a><span data-ttu-id="33b9a-206">Registrieren des Empfängers</span><span class="sxs-lookup"><span data-stu-id="33b9a-206">Register the receiver</span></span>

<span data-ttu-id="33b9a-207">Die letzte Aufgabe besteht darin, SharePoint mitzuteilen, dass wir einen benutzerdefinierten Empfänger haben, den SharePoint immer dann aufrufen soll, wenn ein Element in der Liste **Erwartete Lieferungen** aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="33b9a-207">The final task is to tell SharePoint that we have a custom receiver that we want SharePoint to call whenever an item on the **Expected Shipments** list is updated.</span></span>

1. <span data-ttu-id="33b9a-208">Öffnen Sie die Datei „SharePointComponentDeployer.cs“ und fügen Sie die folgende Zeile zur Methode **DeployChainStoreComponentsToHostWeb** hinzu, und zwar direkt unterhalb der Zeile, die die **Erwartete Lieferungen**-Liste erstellt (wir fügen diese Methode im nächsten Schritt hinzu).</span><span class="sxs-lookup"><span data-stu-id="33b9a-208">Open the SharePointContentDeployer.cs file and add the following line to the **DeployChainStoreComponentsToHostWeb** method, just under the line that creates the **Expected Shipments** list (we'll add this method in the next step).</span></span> <span data-ttu-id="33b9a-209">Beachten Sie, dass wir die Methode an das **HttpRequest**-Objekt übergeben, das die Add-In-Startseite an die Methode **DeployChainStoreComponentsToHostWeb** übergeben hat.</span><span class="sxs-lookup"><span data-stu-id="33b9a-209">Note that we are passing to the method the **HttpRequest** object that the add-in's start page passed to the **DeployChainStoreComponentsToHostWeb** method.</span></span>
    
    ```C#
      RegisterExpectedShipmentsEventHandler(request);
    ```

2. <span data-ttu-id="33b9a-210">Fügen Sie der Klasse `SharePointComponentDeployer` die folgende Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-210">Add the following method to the `SharePointComponentDeployer` class.</span></span>
    
    ```C#
      private static void RegisterExpectedShipmentsEventHandler(HttpRequest request)
    {
        using (var clientContext = sPContext.CreateUserClientContextForSPHost())    
        {
        var query = from list in clientContext.Web.Lists
                where list.Title == "Expected Shipments"
                select list;
        IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
        clientContext.ExecuteQuery();

        List expectedShipmentsList = matchingLists.Single();

        // TODO16: Add the event receiver to the list's collection of event receivers.       

        clientContext.ExecuteQuery();
        }
    }
    ```

3. <span data-ttu-id="33b9a-211">Ersetzen Sie `TODO16` durch die folgenden Zeilen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-211">Replace `TODO16` with the following lines.</span></span> <span data-ttu-id="33b9a-212">Beachten Sie, dass es eine einfache **CreationInformation**-Klasse für Ereignisempfänger ebenso wie für Listen und Listenelemente gibt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-212">Note that there is a lightweight **CreationInformation** class for event receivers just as there is for lists and list items.</span></span>
    
    ```C#
    EventReceiverDefinitionCreationInformation receiver = new EventReceiverDefinitionCreationInformation();
    receiver.ReceiverName = "ExpectedShipmentsItemUpdated";
    receiver.EventType = EventReceiverType.ItemUpdated;

     // TODO17: Set the URL of the receiver.

    expectedShipmentsList.EventReceivers.Add(receiver);

    ```

4. <span data-ttu-id="33b9a-213">Jetzt müssen Sie SharePoint die URL des Ereignisempfängers mitteilen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-213">Now you need to tell SharePoint the URL of the event receiver.</span></span> <span data-ttu-id="33b9a-214">In der Produktion befindet sie sich in der gleichen Domäne wie die Remote-Seiten. Der Pfad lautet /Services/RemoteEventReceiver1.svc.</span><span class="sxs-lookup"><span data-stu-id="33b9a-214">In production, it's going to be at the same domain as the remote pages, with the path of /Services/RemoteEventReceiver1.svc.</span></span> <span data-ttu-id="33b9a-215">Da der Handler in der ersten Ausführungslogik über die Add-In-Startseite registriert wird, befindet sich die Domäne im Hostheader des **HttpRequest**-Objekts der Anforderung, die die Seite aufgerufen hat.</span><span class="sxs-lookup"><span data-stu-id="33b9a-215">Because the handler is being registered in first-run logic from the add-in's start page, the domain is in the host header of the **HttpRequest** object for the request that called the page.</span></span> <span data-ttu-id="33b9a-216">Unser Code hat dieses Objekt von der Seite an die **DeployChainStoreComponentsToHostWeb**-Methode übergeben, die es wiederum an die **RegisterExpectedShipmentsEventHandler**-Methode weitergegeben hat.</span><span class="sxs-lookup"><span data-stu-id="33b9a-216">Our code has passed that object from the page to the **DeployChainStoreComponentsToHostWeb** method, which itself passed it to the **RegisterExpectedShipmentsEventHandler** method.</span></span> <span data-ttu-id="33b9a-217">Daher können wir die Empfänger-URL mit dem folgenden Code angeben.</span><span class="sxs-lookup"><span data-stu-id="33b9a-217">So we can set the receiver's URL with the following code.</span></span>
    
    `receiver.ReceiverUrl = "https://" + request.Headers["Host"] + "/Services/RemoteEventReceiver1.svc";`
    
   <span data-ttu-id="33b9a-218">Dies funktioniert leider nicht, wenn Sie das Add-In in Visual Studio debuggen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-218">Unfortunately, this won't work when you are debugging the add-in from Visual Studio.</span></span> <span data-ttu-id="33b9a-219">Beim Debuggen wird der Empfänger in der Azure Service Bus gehostet und nicht in der Localhost-URL, in der die Remote-Seiten gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="33b9a-219">When you are debugging, the receiver is hosted in the Azure Service Bus, not in the localhost URL where the remote pages are hosted.</span></span> <span data-ttu-id="33b9a-220">Je nachdem, ob wir debuggen oder nicht, müssen wir unterschiedliche URLs für den Empfänger festlegen. Ersetzen Sie also `TODO17` durch die folgende Struktur, die C#-Compiler-Richtlinien verwendet.</span><span class="sxs-lookup"><span data-stu-id="33b9a-220">We need to set distinct URLs for the receiver depending on whether we are debugging or not, so replace `TODO17` with the following structure that uses C# compiler directives.</span></span> <span data-ttu-id="33b9a-221">Beachten Sie, dass die URL des Empfängers im Debugmodus von der Einstellung web.config gelesen wird (diese Einstellung wird in einem späteren Schritt erstellt).</span><span class="sxs-lookup"><span data-stu-id="33b9a-221">Note that in debug mode the receiver's URL is read from a web.config setting (you will create this setting in a later step).</span></span> 

    ```C#
      #if DEBUG
                receiver.ReceiverUrl = WebConfigurationManager.AppSettings["RERdebuggingServiceBusUrl"].ToString();
    #else
                receiver.ReceiverUrl = "https://" + request.Headers["Host"] + "/Services/RemoteEventReceiver1.svc"; 
    #endif

    ```


5. <span data-ttu-id="33b9a-222">Die gesamte **RegisterExpectedShipmentsEventHandler**-Methode sollte jetzt wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-222">The entire **RegisterExpectedShipmentsEventHandler** method should now look like the following.</span></span>
    
    ```C#
      private static void RegisterExpectedShipmentsEventHandler(HttpRequest request)
    {    
        using (var clientContext = sPContext.CreateUserClientContextForSPHost())
        {
        var query = from list in clientContext.Web.Lists
                    where list.Title == "Expected Shipments"
                    select list;
        IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
        clientContext.ExecuteQuery();

        List expectedShipmentsList = matchingLists.Single();

        EventReceiverDefinitionCreationInformation receiver = new EventReceiverDefinitionCreationInformation();
        receiver.ReceiverName = "ExpectedShipmentsItemUpdated";
        receiver.EventType = EventReceiverType.ItemUpdated;

    #if DEBUG
        receiver.ReceiverUrl = WebConfigurationManager.AppSettings["RERdebuggingServiceBusUrl"].ToString();
    #else
        receiver.ReceiverUrl = "https://" + request.Headers["Host"] + "/Services/RemoteEventReceiver1.svc"; 
    #endif
        expectedShipmentsList.EventReceivers.Add(receiver);
        clientContext.ExecuteQuery();
        }
    }
    ```

6. <span data-ttu-id="33b9a-223">Fügen Sie die folgenden **using**-Anweisung an den Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-223">Add the following **using** statement to the top of the file.</span></span>
    
    ```C#
      using System.Web.Configuration;
    ```

7. <span data-ttu-id="33b9a-224">Um sicherzustellen, dass `DEBUG` dann und nur dann „true“ ist, wenn das Add-In gedebuggt wird, führen Sie die folgende Unterprozedur aus:</span><span class="sxs-lookup"><span data-stu-id="33b9a-224">To ensure that `DEBUG` is true if and only if the add-in is being debugged, carry out the following subprocedure:</span></span>
    
   1. <span data-ttu-id="33b9a-225">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt **ChainStoreWeb **, und wählen Sie **Eigenschaften** aus.</span><span class="sxs-lookup"><span data-stu-id="33b9a-225">In **Solution Explorer**, right-click the **ChainStoreWeb** project and select **Properties**.</span></span>
   
   2. <span data-ttu-id="33b9a-226">Öffnen Sie die Registerkarte **Build** der **Eigenschaften**, und wählen Sie dann **Debuggen** in der Dropdownliste **Konfiguration** im oberen Bereich aus.</span><span class="sxs-lookup"><span data-stu-id="33b9a-226">Open the **Build** tab of the **Properties**, and then select **Debug** from the **Configuration** drop-down at the top.</span></span>
   
   3. <span data-ttu-id="33b9a-227">Stellen Sie sicher, dass das **DEBUG-Konstante definieren**-Kontrollkästchen aktiviert ist (in der Regel ist es standardmäßig aktiviert).</span><span class="sxs-lookup"><span data-stu-id="33b9a-227">Ensure that the **Define DEBUG constant** check box is selected (it usually is by default).</span></span> <span data-ttu-id="33b9a-228">Im folgenden Screenshot ist die korrekte Einstellung abgebildet.</span><span class="sxs-lookup"><span data-stu-id="33b9a-228">The following screen shot shows the proper setting.</span></span>

      <span data-ttu-id="33b9a-229">*Abbildung 1. Erstellen einer untergeordneten Registerkarte der Registerkarte „Eigenschaften“ in Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="33b9a-229">*Figure 1. Build sub-tab of the Properties tab in Visual Studio*</span></span>

      ![Erstellen Sie eine untergeordnete Registerkarte der Registerkarte "Eigenschaften" in Visual Studio.](../images/4f81174f-d875-4a9e-bff4-adea0f176f00.PNG)

   4. <span data-ttu-id="33b9a-233">Ändern Sie die Auswahl in der Dropdownliste **Konfiguration** in **Version**, und stellen Sie sicher, dass das Kontrollkästchen **DEBUG-Konstante definieren** *nicht* aktiviert ist. (Das ist normalerweise standardmäßig nicht der Fall.)</span><span class="sxs-lookup"><span data-stu-id="33b9a-233">Change the **Configuration** drop-down to **Release**, and then ensure that the **Define DEBUG constant** check box is *not* selected (it usually is not by default).</span></span> <span data-ttu-id="33b9a-234">Im folgenden Screenshot ist die korrekte Einstellung abgebildet.</span><span class="sxs-lookup"><span data-stu-id="33b9a-234">The following screenshot shows the proper setting.</span></span>
  
      <span data-ttu-id="33b9a-235">*Abbildung 2. Erstellen einer untergeordneten Registerkarte der Registerkarte „Eigenschaften“ mit deaktiviertem Kontrollkästchen*</span><span class="sxs-lookup"><span data-stu-id="33b9a-235">*Figure 2. Build sub-tab of the Properties tab with check box cleared*</span></span>

      ![Die Unterregisterkarte „Build“ der Registerkarte „Eigenschaften“. In der Dropdownliste „Konfiguration“ ist „Version“ ausgewählt. Das Kontrollkästchen für „DEBUG-Konstante definieren“ ist deaktiviert.](../images/7fd942de-a324-4f70-a750-f5304c993832.PNG)

   5. <span data-ttu-id="33b9a-238">Wenn Sie Änderungen vorgenommen haben, speichern Sie diese, und schließen Sie dann die Registerkarte **Eigenschaften**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-238">If you made any changes, save and then close the **Properties** tab.</span></span>
    
 
8. <span data-ttu-id="33b9a-239">Öffnen Sie die Datei „web.config“, und fügen Sie das folgende Markup als untergeordnetes Element des Elements **appSettings** hinzu. (Der Wert der Einstellung wird im nächsten Abschnitt abgerufen.)</span><span class="sxs-lookup"><span data-stu-id="33b9a-239">Open the web.config file, and add the following markup as a child of the **appSettings** element (we get the value of the setting in the next section).</span></span>
    
    ```XML
      <add key="RERdebuggingServiceBusUrl" value="" />
    ```

## <a name="get-the-receiver-url-for-debugging"></a><span data-ttu-id="33b9a-240">Abrufen der Empfänger-URL für das Debuggen</span><span class="sxs-lookup"><span data-stu-id="33b9a-240">Get the receiver URL for debugging</span></span>

<span data-ttu-id="33b9a-241">Das Add-In-Ereignis und die Listenelement-Ereignisempfänger sind Windows Communication Service (WCF)-Dienste, und jeder WCF-Dienst kennt seinen eigenen Endpunkt und speichert ihn an mehreren Orten, einschließlich des ** System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri**-Objekts.</span><span class="sxs-lookup"><span data-stu-id="33b9a-241">The add-in event and list item event receivers are Windows Communication Service (WCF) services, and every WCF service knows its own endpoint and stores it in multiple places, including the **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri** object.</span></span> 

<span data-ttu-id="33b9a-242">Beim Debuggen wird der Add-In-Empfänger auf einem Azure Service Bus-Endpunkt gehostet, der nahezu identisch mit dem Endpunkt für den Listenelement-Empfänger ist.</span><span class="sxs-lookup"><span data-stu-id="33b9a-242">When you are debugging, the add-in receiver is hosted at an Azure Service Bus endpoint that is almost the same as the endpoint for the list item receiver.</span></span> <span data-ttu-id="33b9a-243">Der Unterschied besteht darin, dass die URL des Add-In-Endpunkts auf „AppEventReceiver.svc“ endet, aber die URL des Listenelement-Empfängers auf „RemoteEventReceiver1.svc“.</span><span class="sxs-lookup"><span data-stu-id="33b9a-243">The difference is that the URL of the add-in endpoint ends with "AppEventReceiver.svc", but the list item receiver's URL ends with "RemoteEventReceiver1.svc."</span></span> <span data-ttu-id="33b9a-244">Daher können wir die URL des Endpunkts des Add-In-Empfänger verwenden, ein paar Änderungen am Ende vornehmen und sie dann als Wert für die Einstellung **RERdebuggingServiceBusUrl** verwenden.</span><span class="sxs-lookup"><span data-stu-id="33b9a-244">So we can get the URL of the endpoint in the add-in receiver, make a small change to the end of it, and then use it as the value of our web.config **RERdebuggingServiceBusUrl** setting.</span></span>

1. <span data-ttu-id="33b9a-245">Öffnen Sie die Datei „AppEventReceiver.svc.cs“ im Ordner **Dienste** des Projekts **ChainStoreWeb**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-245">Open the AppEventReceiver.svc.cs file in the **Services** folder of the **ChainStoreWeb** project.</span></span>

2. <span data-ttu-id="33b9a-246">Fügen Sie Folgendes als erste Zeile in der Methode **ProcessEvent** hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-246">Add the following as the very first line in the **ProcessEvent** method.</span></span>
    
    ```C#
      string debugEndpoint = System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri.ToString(); 
    ```

3. <span data-ttu-id="33b9a-247">Fügen Sie einen Haltepunkt zur nächsten Zeile der Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-247">Add a breakpoint to the very next line of the method.</span></span>

4. <span data-ttu-id="33b9a-248">Wählen Sie F5, um das Add-In zu debuggen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-248">Select F5 to debug the add-in.</span></span> <span data-ttu-id="33b9a-249">Da „web.config“ geöffnet ist und Office Developer Tools für Visual Studio jedes Mal eine Einstellung darin ändert, wenn Sie F5 wählen, werden Sie aufgefordert, die Datei neu zu laden.</span><span class="sxs-lookup"><span data-stu-id="33b9a-249">Because web.config is open and Office Developer Tools for Visual Studio changes a setting in it every time you select F5, you are prompted to reload it.</span></span> <span data-ttu-id="33b9a-250">Wählen Sie **Ja**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-250">Select **Yes**.</span></span> 

5. <span data-ttu-id="33b9a-251">Wenn der Haltepunkt erreicht ist, bewegen Sie den Cursor über die `debugEndpoint`-Variable.</span><span class="sxs-lookup"><span data-stu-id="33b9a-251">When the breakpoint is hit, hover the cursor over the `debugEndpoint` variable.</span></span> <span data-ttu-id="33b9a-252">Wenn der Visual Studio-Datentipp angezeigt wird, wählen Sie den Pfeil nach unten, und wählen Sie dann **Text-Schnellansicht**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-252">When the Visual Studio Data Tip appears, select the down arrow, and then select **Text Visualizer**.</span></span>
  
   <span data-ttu-id="33b9a-253">*Abbildung 3. Eine Textschnellansicht in Visual Studio mit einer Azure Service Bus-URL*</span><span class="sxs-lookup"><span data-stu-id="33b9a-253">*Figure 3. Visual Studio text visualizer with an Azure Service Bus URL*</span></span>

   ![Eine Textschnellansicht in Visual Studio mit einer Azure Service Bus-URL](../images/494cf01e-3e17-4092-b239-9312ac4ab258.PNG)

6. <span data-ttu-id="33b9a-255">Kopieren Sie den Zeichenfolgenwert aus der Schnellansicht, und fügen Sie ihn an einer beliebigen anderen Stelle ein.</span><span class="sxs-lookup"><span data-stu-id="33b9a-255">Copy the string value from the visualizer and paste it somewhere.</span></span>

7. <span data-ttu-id="33b9a-256">Schließen Sie die Schnellansicht, und beenden Sie das Debuggen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33b9a-256">Close the visualizer, and then stop debugging in Visual Studio.</span></span>

8. <span data-ttu-id="33b9a-257">Löschen Sie die Zeile, die Sie im zweiten Schritt dieses Verfahrens hinzugefügt haben, oder kommentieren Sie sie aus, und löschen Sie auch den Haltepunkt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-257">Delete or comment out the line you added in the second step of this procedure, and then delete the breakpoint as well.</span></span>

9. <span data-ttu-id="33b9a-258">Ersetzen Sie in der kopierten Zeichenfolge das „AppEventReceiver.svc“ am Ende durch „RemoteEventReceiver1.svc“.</span><span class="sxs-lookup"><span data-stu-id="33b9a-258">In the string you copied, replace the "AppEventReceiver.svc" at the end with "RemoteEventReceiver1.svc".</span></span>

10. <span data-ttu-id="33b9a-259">Kopieren Sie die geänderte URL und fügen Sie sie als Wert für den Schlüssel **RERdebuggingServiceBusUrl** in der web.config-Datei ein.</span><span class="sxs-lookup"><span data-stu-id="33b9a-259">Copy and paste the modified URL as the value of the **RERdebuggingServiceBusUrl** key in the web.config file.</span></span>

> [!NOTE]
> <span data-ttu-id="33b9a-260">Das manuelle Kopieren und Einfügen der Servicebus-URL (einer modifizierten Version davon) in die web.config-Datei ist nicht die einzige Möglichkeit für den Umgang mit der Notwendigkeit einer anderen URL beim Debuggen eines Remoteereignisempfängers, wenn dieser in der Produktion ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="33b9a-260">Manually copying the service bus URL and pasting (a modified version of) it into the web.config is not the only way of dealing with the need for a different URL when debugging a remote event receiver when it is running in production.</span></span> <span data-ttu-id="33b9a-261">Wir könnten den Wert von **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri** programmgesteuert an einer beliebigen Stelle in SharePoint oder der Remotedatenbank speichern und ihn dann vom zuerst ausgeführten Code lesen und der Eigenschaft `receiver.ReceiverUrl` zuweisen lassen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-261">We could programmatically store the value of **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri** somewhere in SharePoint or the remote database, and then have our first-run code read it and assign it to the `receiver.ReceiverUrl` property.</span></span> <span data-ttu-id="33b9a-262">Wir könnten den Listenelement-Ereignisempfänger als Teil des im Add-In installierten Ereignishandlers registrieren.</span><span class="sxs-lookup"><span data-stu-id="33b9a-262">We could register the list item event receiver as part of the add-in installed event handler.</span></span> <span data-ttu-id="33b9a-263">Dann könnten wir programmgesteuert **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri** ohne zu speichern lesen, ändern und `receiver.ReceiverUrl` zuweisen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-263">We could then programmatically read **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri**, modify it, and assign it to `receiver.ReceiverUrl` without having to store it anywhere.</span></span> 
>
> <span data-ttu-id="33b9a-264">Diese Vorgehensweise erfordert, dass die **Erwartete Lieferungen**-Liste ebenfalls in dem im Add-In installierten Ereignishandler erstellt wird, da sie vorhanden sein muss, bevor der Handler damit registriert werden kann.</span><span class="sxs-lookup"><span data-stu-id="33b9a-264">This strategy requires that the **Expected Shipments** list also be created in the add-in installed event handler because it would have to exist before the handler could be registered with it.</span></span> 
>
> <span data-ttu-id="33b9a-265">Beachten Sie auch, dass wir den Add-In-Ereignisempfänger und den Listenelement-Ereignisempfänger in einem einzigen Empfänger kombinieren könnten (d. h. in den gleichen .svc- und .svc-cs-Dateien).</span><span class="sxs-lookup"><span data-stu-id="33b9a-265">Note also that we could combine our add-in event receiver and list item event receiver into a single receiver (that is, the same .svc and .svc.cs files).</span></span> <span data-ttu-id="33b9a-266">In diesem Fall ist erst eine Änderung der URL erforderlich, wenn sie als Wert `receiver.ReceiverUrl` verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="33b9a-266">In that case, no modification of the URL is necessary before using it as the value of `receiver.ReceiverUrl`.</span></span>

## <a name="run-the-add-in-and-test-the-list-item-receiver"></a><span data-ttu-id="33b9a-267">Ausführen des Add-Ins und Testen des Listenelementempfängers</span><span class="sxs-lookup"><span data-stu-id="33b9a-267">Run the add-in and test the list item receiver</span></span>

1. <span data-ttu-id="33b9a-268">Öffnen Sie die Seite **Websiteinhalte** der Website für den Hongkong-Store, und entfernen Sie die Liste **Erwartete Lieferungen**, falls sie vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="33b9a-268">Open the **Site Contents** page of the Hong Kong store's website, and remove the **Expected Shipments** list if there is one.</span></span> 

2. <span data-ttu-id="33b9a-269">Drücken Sie auf die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-269">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="33b9a-270">Visual Studio hostet die Remotewebanwendung in IIS Express und die SQL-Datenbank in SQL Express.</span><span class="sxs-lookup"><span data-stu-id="33b9a-270">Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in SQL Express.</span></span> <span data-ttu-id="33b9a-271">Zudem installiert Visual Studio das Add-In vorübergehend auf Ihrer SharePoint-Testwebsite und führt es sofort aus.</span><span class="sxs-lookup"><span data-stu-id="33b9a-271">It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="33b9a-272">Bevor die Startseite des Add-Ins geöffnet wird, werden Sie aufgefordert, dem Add-In Berechtigungen zu erteilen.</span><span class="sxs-lookup"><span data-stu-id="33b9a-272">You are prompted to grant permissions to the add-in before its start page opens.</span></span>

3. <span data-ttu-id="33b9a-273">Die Startseite des Add-Ins wird geöffnet. Wählen Sie oben im Chromsteuerelement die Schaltfläche **Zurück zur Website**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-273">When the add-in's start page opens, select the **Back to Site** button on the chrome control at the top.</span></span>

4. <span data-ttu-id="33b9a-274">Wechseln Sie von der Startseite des Hongkong-Stores zur Seite **Websiteinhalte**, und öffnen Sie die Liste **Erwartete Lieferungen**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-274">From the home page of the Hong Kong store, go to the **Site Contents** page and open the **Expected Shipments** list.</span></span>

5. <span data-ttu-id="33b9a-275">Erstellen Sie ein Element, und beachten Sie auf dem Formular für ein neues Element, dass die Felder **Eingetroffen** und **Zum Bestand hinzugefügt** nicht angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="33b9a-275">Create an item, and on the new item form, notice that the **Arrived** and **Added to Inventory** fields do not appear.</span></span>
 
6. <span data-ttu-id="33b9a-276">Nachdem das Element erstellt wurde, öffnen Sie es für die Bearbeitung.</span><span class="sxs-lookup"><span data-stu-id="33b9a-276">After the item is created, reopen it for editing.</span></span> <span data-ttu-id="33b9a-277">Wählen Sie das **Angekommen**-Kontrollkästchen, und speichern Sie das Element.</span><span class="sxs-lookup"><span data-stu-id="33b9a-277">Select the **Arrived** check box and save the item.</span></span> <span data-ttu-id="33b9a-278">Dadurch wird das Element aktualisiert-Ereignis ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="33b9a-278">This triggers the item updated event.</span></span> <span data-ttu-id="33b9a-279">Das Element wird zum Bestand hinzugefügt, und der Wert des Feldes **Zum Bestand hinzugefügt** ändert sich in **Ja** (möglicherweise müssen Sie die Seite aktualisieren, damit die Änderung an **Zum Bestand hinzugefügt** sichtbar werden).</span><span class="sxs-lookup"><span data-stu-id="33b9a-279">The item is added to inventory and the value of the **Added to Inventory** field changes to **Yes** (you may have to refresh the page to see the change to **Added to Inventory**).</span></span>

7. <span data-ttu-id="33b9a-280">Verwenden Sie im Browser die Schaltfläche „Zurück“, bis Sie wieder auf die Startseite für das ChainStore-Add-In zurückgekehrt sind, und wählen Sie dann die Schaltfläche **Bestand anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-280">Use the browser's back button until you are back at the start page for the Chain Store add-in, and then select the **Show Inventory** button.</span></span> <span data-ttu-id="33b9a-281">Das Element, das Sie als **Angekommen** gekennzeichnet haben, wird nun aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="33b9a-281">The item you marked as **Arrived** is now listed.</span></span>

8. <span data-ttu-id="33b9a-282">Gehen Sie zurück zur Liste **Erwartete Lieferungen**, und fügen Sie ein weiteres Element *mit exakt demselben Produktnamen und Lieferantennamen*, aber einer anderen Menge hinzu.</span><span class="sxs-lookup"><span data-stu-id="33b9a-282">Go back to the **Expected Shipments** list and add another item *with exactly the same product name and supplier name*, but a different quantity.</span></span>

9. <span data-ttu-id="33b9a-283">Nachdem das Element erstellt wurde, öffnen Sie es für die Bearbeitung.</span><span class="sxs-lookup"><span data-stu-id="33b9a-283">After the item is created, reopen it for editing.</span></span> <span data-ttu-id="33b9a-284">Ändern Sie den Wert für **Angekommen** auf **Ja** , und speichern Sie das Element.</span><span class="sxs-lookup"><span data-stu-id="33b9a-284">Change the value of **Arrived** to **Yes** and save the item.</span></span>

10. <span data-ttu-id="33b9a-285">Verwenden Sie im Browser die Schaltfläche „Zurück“, bis Sie wieder auf die Startseite für das ChainStore-Add-In zurückgekehrt sind, und wählen Sie dann die Schaltfläche **Bestand anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="33b9a-285">Use the browser's back button until you are back at the start page for the Chain Store add-in, and then select the **Show Inventory** button.</span></span> <span data-ttu-id="33b9a-286">Es gibt nur noch ein Element für den Produktname und Lieferanten, aber die Menge ist nun die Summe der beiden Elemente der **Erwartete Lieferungen**-Liste.</span><span class="sxs-lookup"><span data-stu-id="33b9a-286">There is still just one item for the product name and supplier, but the quantity is now the total of the two items on the **Expected Shipments** list.</span></span>

11. <span data-ttu-id="33b9a-287">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33b9a-287">To end the debugging session, close the browser window or stop debugging in Visual Studio.</span></span> <span data-ttu-id="33b9a-288">Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="33b9a-288">Each time you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

12. <span data-ttu-id="33b9a-289">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben.</span><span class="sxs-lookup"><span data-stu-id="33b9a-289">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while.</span></span> <span data-ttu-id="33b9a-290">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="33b9a-290">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33b9a-291">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="33b9a-291">Next steps</span></span>
<span data-ttu-id="33b9a-292"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="33b9a-292"></span></span>

<span data-ttu-id="33b9a-293">Um zu erfahren, wie Sie Ihr Add-In auf einer SharePoint-Website veröffentlichen, lesen Sie [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md).</span><span class="sxs-lookup"><span data-stu-id="33b9a-293">To learn how to publish your add-in to a SharePoint site, see [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options.md).</span></span> <span data-ttu-id="33b9a-294">Weitere Arbeitsschritte für die SharePoint-Add-In-Entwicklung finden Sie auf den folgenden Seiten:</span><span class="sxs-lookup"><span data-stu-id="33b9a-294">You can also pursue advanced work in SharePoint add-in development on the following pages:</span></span>

-  [<span data-ttu-id="33b9a-295">Entwerfen von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="33b9a-295">Design SharePoint Add-ins</span></span>](design-sharepoint-add-ins.md)
-  [<span data-ttu-id="33b9a-296">Entwickeln von SharePoint-Add-ins</span><span class="sxs-lookup"><span data-stu-id="33b9a-296">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
-  [<span data-ttu-id="33b9a-297">Veröffentlichen von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="33b9a-297">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins.md)
-  [<span data-ttu-id="33b9a-298">Tools und Umgebungen für die Entwicklung von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="33b9a-298">Tools and environments for developing SharePoint Add-ins</span></span>](tools-and-environments-for-developing-sharepoint-add-ins.md)
    
 

