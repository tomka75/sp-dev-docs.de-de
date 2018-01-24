---
title: "Erstellen eines vollständigen SharePoint-Websitedesigns mithilfe des PnP-Bereitstellungsmoduls"
description: "Erstellen eines vollständigen SharePoint-Websitedesigns mithilfe des PnP-Bereitstellungsmoduls"
ms.date: 12/14/2017
ms.openlocfilehash: 028a028822c234dcbbbad290c642ec03dd4b6392
ms.sourcegitcommit: d9372f6009de1c1e48e272fd3629a99aed7fef9f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="calling-the-pnp-provisioning-engine-from-a-site-script"></a><span data-ttu-id="c5d88-103">Aufrufen des PnP-Bereitstellungsmoduls über ein Websiteskript</span><span class="sxs-lookup"><span data-stu-id="c5d88-103">Calling the PnP Provisioning Engine from a Site Script</span></span>

> [!NOTE]
> <span data-ttu-id="c5d88-104">Websitedesigns und Websiteskripts befinden sich derzeit in der Preview-Phase und können jederzeit geändert verwenden.</span><span class="sxs-lookup"><span data-stu-id="c5d88-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="c5d88-105">Sie werden in Produktionsumgebungen derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c5d88-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="c5d88-106">Websitedesigns sind eine hervorragende Möglichkeit, das Aussehen und Verhalten Ihrer Websitesammlungen zu standardisieren.</span><span class="sxs-lookup"><span data-stu-id="c5d88-106">Site Designs offer a great way to standardize the look and feel of your site collections.</span></span> <span data-ttu-id="c5d88-107">Bestimmte Dinge lassen sich mit Websitedesigns jedoch nicht umsetzen. Beispielsweise ist es nicht möglich, jeder Seite eine Fußzeile hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-107">You can't do some things with site designs, however, like add a footer to every page.</span></span> <span data-ttu-id="c5d88-108">Mit dem PnP-Bereitstellungsmodul können Sie eine Vorlage erstellen, mit der Sie einen Application Customizer auf einer Website bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="c5d88-108">You can use the PnP provisioning engine to create a template that you can use to provision an application customizer to a site.</span></span> <span data-ttu-id="c5d88-109">Ein solcher Application Customizer kann das Seitendesign aktualisieren und so beispielsweise eine Fußzeile auf jeder Seite registrieren.</span><span class="sxs-lookup"><span data-stu-id="c5d88-109">This application customizer can then update your page design, for example to register a footer on every page.</span></span> 

<span data-ttu-id="c5d88-110">In diesem Artikel wird beschrieben, wie Sie ein Websitedesign erstellen können, das eine PnP-Bereitstellungsvorlage auf eine Website anwendet.</span><span class="sxs-lookup"><span data-stu-id="c5d88-110">This article describes how to create a site design that applies a PnP provisioning template to a site.</span></span> <span data-ttu-id="c5d88-111">Die Vorlage wird einen Application Customizer hinzufügen, der eine Fußzeile rendert.</span><span class="sxs-lookup"><span data-stu-id="c5d88-111">The template will add an application customizer to render a footer.</span></span>

<span data-ttu-id="c5d88-112">In der Anleitung in diesem Artikel verwenden wir die folgenden Komponenten:</span><span class="sxs-lookup"><span data-stu-id="c5d88-112">The steps in this article use the following components:</span></span>

- <span data-ttu-id="c5d88-113">Ein Websitedesign und ein Websiteskript</span><span class="sxs-lookup"><span data-stu-id="c5d88-113">A Site Design and a Site Script</span></span>
- <span data-ttu-id="c5d88-114">Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="c5d88-114">A Microsoft Flow</span></span>
- <span data-ttu-id="c5d88-115">Azure Queue-Speicher</span><span class="sxs-lookup"><span data-stu-id="c5d88-115">Azure Queue storage</span></span>
- <span data-ttu-id="c5d88-116">Eine Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="c5d88-116">An Azure Function</span></span>
- <span data-ttu-id="c5d88-117">Eine SharePoint-Framework-Lösung (SPFx-Lösung)</span><span class="sxs-lookup"><span data-stu-id="c5d88-117">A SharePoint Framework (SPFx) solution</span></span>
- <span data-ttu-id="c5d88-118">Eine PnP-Bereitstellungsvorlage</span><span class="sxs-lookup"><span data-stu-id="c5d88-118">A PnP Provisioning Template</span></span>
- <span data-ttu-id="c5d88-119">Ein PnP-PowerShell-Skript</span><span class="sxs-lookup"><span data-stu-id="c5d88-119">A PnP PowerShell Script</span></span>
- <span data-ttu-id="c5d88-120">Eine App-ID und einen geheimen App-Schlüssel mit Administratorrechten in Ihrem Mandanten</span><span class="sxs-lookup"><span data-stu-id="c5d88-120">An app ID and app secret with administrative rights on your tenant</span></span>

<span data-ttu-id="c5d88-121">Mithilfe dieser Komponenten wird der PnP-Bereitstellungscode ausgelöst, sobald Sie die Website erstellt und das Websitedesign angewendet haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-121">You'll use these components to trigger the PnP provisioning code after you create the site and apply the site design.</span></span>

## <a name="set-up-app-only-access-to-your-tenant"></a><span data-ttu-id="c5d88-122">Einrichten von App-exklusivem Zugriff auf Ihren Mandanten</span><span class="sxs-lookup"><span data-stu-id="c5d88-122">Set up app-only access to your tenant</span></span>

<span data-ttu-id="c5d88-123">Zur Einrichtung von App-exklusivem Zugriff benötigen Sie zwei unterschiedliche Seiten in Ihrem Mandanten: eine Seite auf der regulären Website und eine Seite auf Ihrer SharePoint-Administrationswebsite.</span><span class="sxs-lookup"><span data-stu-id="c5d88-123">To set up app-only access, you need to have two different pages on your tenant - one on the regular site, and the other on your SharePoint administration site.</span></span>

1. <span data-ttu-id="c5d88-124">Rufen Sie in Ihrem Mandanten die folgende URL auf: `https://[yourtenant].sharepoint.com/_layouts/appregnew.aspx`. (Sie können jede beliebige Seite aufrufen; für dieses Tutorial verwenden wir hier die Stammwebsite.)</span><span class="sxs-lookup"><span data-stu-id="c5d88-124">Navigate to following URL in your tenant: https://[yourtenant].sharepoint.com/_layouts/appregnew.aspx (you can navigate to any site, but for now pick the root site)</span></span>
1. <span data-ttu-id="c5d88-125">Klicken Sie neben den Feldern **Client-ID** und **Geheimer Clientschlüssel** jeweils auf die Schaltfläche **Generieren**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-125">Choose the **Generate** button next to the **Client Id** and **Client Secret** fields.</span></span>
1. <span data-ttu-id="c5d88-126">Geben Sie einen Titel für Ihre App ein, beispielsweise „Site Provisioning“.</span><span class="sxs-lookup"><span data-stu-id="c5d88-126">Enter a title for your app, such as "Site Provisioning".</span></span>
1. <span data-ttu-id="c5d88-127">Geben Sie in das Feld **App-Domäne** die Zeichenfolge **localhost** ein.</span><span class="sxs-lookup"><span data-stu-id="c5d88-127">In the **App Domain** box, enter **localhost**.</span></span>
1. <span data-ttu-id="c5d88-128">Geben Sie in das Feld **Umleitungs-URI** die Adresse **https://localhost** ein.</span><span class="sxs-lookup"><span data-stu-id="c5d88-128">In the **Redirect URI** box, enter **https://localhost**.</span></span>

    ![Seite „App erstellen“ mit den Feldern „Client-ID“, „Geheimer Clientschlüssel“, „Titel“, „App-Domäne“ und „Umleitungs-URI“](images/pnpprovisioning-createapponly.png)

1. <span data-ttu-id="c5d88-130">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-130">Choose **Create**.</span></span> 
1. <span data-ttu-id="c5d88-131">Notieren Sie sich die Werte für **Client-ID** und **Geheimer Clientschlüssel**. Sie werden sie später noch brauchen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-131">Click Create and copy the values for Client Id and Client Secret as you will need them later</span></span>

<span data-ttu-id="c5d88-132">Stufen Sie nun die App als vertrauenswürdig ein, damit Sie die entsprechenden Zugriffsrechte für Ihren Mandanten hat:</span><span class="sxs-lookup"><span data-stu-id="c5d88-132">Next, trust the app, so that it has the appropriate access to your tenant:</span></span>

1. <span data-ttu-id="c5d88-133">Rufen Sie `https://[yourtenant]-admin.sharepoint.com/_layouts/appinv.aspx` auf. (Wichtig hierbei ist der Teil `-admin` in der URL.)</span><span class="sxs-lookup"><span data-stu-id="c5d88-133">Go to `https://[yourtenant]-admin.sharepoint.com/_layouts/appinv.aspx` (notice the `-admin` in the URL).</span></span>
1. <span data-ttu-id="c5d88-134">Fügen Sie in das Feld **App-ID** die **Client-ID** ein, die Sie sich notiert haben, und klicken Sie auf **Lookup**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-134">In the **App Id** field, paste the **Client ID** that you copied, and choose **Lookup**.</span></span>
1. <span data-ttu-id="c5d88-135">Fügen Sie den folgenden XML-Code in das Feld **Berechtigungsanforderungs-XML** ein:</span><span class="sxs-lookup"><span data-stu-id="c5d88-135">In the **Permission Request XML** field, paste the following XML:</span></span>

    ```xml
    <AppPermissionRequests AllowAppOnlyPolicy="true" >
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
    </AppPermissionRequests>
    ```

1. <span data-ttu-id="c5d88-136">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-136">Choose **Create**.</span></span>
1. <span data-ttu-id="c5d88-137">Bestätigen Sie mit einem Klick auf **Trust It**, dass Sie der App vertrauen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-137">To confirm that you want to trust this app, choose **Trust It**.</span></span>


## <a name="create-the-azure-queue-storage"></a><span data-ttu-id="c5d88-138">Erstellen des Azure Queue-Speichers</span><span class="sxs-lookup"><span data-stu-id="c5d88-138">Create the Azure Queue storage</span></span>

<span data-ttu-id="c5d88-139">In diesem Szenario verwenden wir Azure Queue-Speicher als Empfänger für Microsoft Flow-Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="c5d88-139">In this scenario we will use an Azure Storage Queue to receive messages from a Microsoft Flow.</span></span> <span data-ttu-id="c5d88-140">Wann immer eine Nachricht im Queue-Speicher angezeigt wird, wird eine Azure-Funktion ausgelöst, die ein PowerShell-Skript ausführt.</span><span class="sxs-lookup"><span data-stu-id="c5d88-140">Every time a message shows up in the Storage Queue an Azure Function will get triggered to execute a PowerShell script.</span></span> 

<span data-ttu-id="c5d88-141">So richten Sie den Azure Queue-Speicher ein</span><span class="sxs-lookup"><span data-stu-id="c5d88-141">To set up the Azure Queue storage:</span></span>

1. <span data-ttu-id="c5d88-142">Rufen Sie das [Azure-Portal](https://portal.azure.com) auf, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="c5d88-142">Go to the [Azure portal](https://portal.azure.com) and sign in.</span></span>
1. <span data-ttu-id="c5d88-143">Klicken Sie auf **+ Neu**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-143">Choose **+ New**</span></span>
1. <span data-ttu-id="c5d88-144">Wählen Sie aus den Azure Marketplace-Angeboten die Option **Storage** aus. Klicken Sie in der Spalte „Empfohlen“ auf **Speicherkonto – Blob, Datei, Tabelle, Warteschlange**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-144">From the Azure Marketplace listings, select **Storage**, and in the Featured column, choose **Storage account - blob, file, table, queue**.</span></span>
1. <span data-ttu-id="c5d88-145">Tragen Sie Werte in die Pflichtfelder ein.</span><span class="sxs-lookup"><span data-stu-id="c5d88-145">Provide values for the required fields as requested.</span></span> <span data-ttu-id="c5d88-146">Klicken Sie auf **Pin to dashboard** und anschließend auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-146">Select **Pin to dashboard**, and choose **Create**.</span></span> <span data-ttu-id="c5d88-147">Es kann einige Minuten dauern, bis das Speicherkonto erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="c5d88-147">It can take a few minutes for the storage account to be created.</span></span>
1. <span data-ttu-id="c5d88-148">Öffnen Sie das Speicherkonto, und klicken Sie auf **Warteschlangen**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-148">Open the storage account and go to **Queues**.</span></span>
1. <span data-ttu-id="c5d88-149">Klicken Sie oben im Bildschirm auf **+ Warteschlange**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-149">Choose **+ Queue** at the top of the main area of the screen.</span></span>
1. <span data-ttu-id="c5d88-150">Geben Sie als Namen **pnpprovisioningqueue** oder einen eigenen Wert ein. Beachten Sie dabei auf jeden Fall die Namenskonvention.</span><span class="sxs-lookup"><span data-stu-id="c5d88-150">Enter **pnpprovisioningqueue** for the name, or enter your own value; be sure to follow the naming standard.</span></span> <span data-ttu-id="c5d88-151">Notieren Sie sich den Namen der Warteschlange; Sie benötigen diesen Wert, wenn Sie die Azure-Funktion erstellen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-151">Make a note of the queue name as you need this value later when creating the Azure Function.</span></span>
1. <span data-ttu-id="c5d88-152">Klicken Sie auf **Zugriffsschlüssel**, und notieren Sie sich die Werte für **Speicherkontoname** sowie **key1 Key value**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-152">Go to **Access Keys** and note the **Storage Account Name** and the **key1 Key value**.</span></span> <span data-ttu-id="c5d88-153">Sie benötigen diese Werte, wenn Sie den Flow erstellen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-153">You will need these values when you create the flow.</span></span>


## <a name="create-the-flow"></a><span data-ttu-id="c5d88-154">Erstellen des Flows</span><span class="sxs-lookup"><span data-stu-id="c5d88-154">Create the flow</span></span>

<span data-ttu-id="c5d88-155">Damit Nachrichten in die Warteschlange gestellt werden können, müssen Sie zunächst einen Flow erstellen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-155">To put a message in the queue, you need to create a flow.</span></span> 

1. <span data-ttu-id="c5d88-156">Rufen Sie die [Microsoft Flow](https://flow.microsoft.com)-Website auf, melden Sie sich an, und klicken Sie oben auf der Seite auf **Create from Blank**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-156">Go to the [Microsoft Flow](https://flow.microsoft.com) site, sign in, and choose **Create from Blank** at the top of the page.</span></span>
1. <span data-ttu-id="c5d88-157">Klicken Sie auf **Hunderte von Connectors und Triggern durchsuchen**, um einen Trigger auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-157">Click **Search hundreds of connectors and triggers** to select your trigger</span></span>
1. <span data-ttu-id="c5d88-158">Suchen Sie nach **Anforderung**, und wählen Sie **Anforderung - Beim Empfang einer HTTP-Anforderung** aus.</span><span class="sxs-lookup"><span data-stu-id="c5d88-158">Search for **Request** and select **Request - When a HTTP Request is received**</span></span>
1. <span data-ttu-id="c5d88-159">Geben Sie den folgenden JSON-Code als Anforderungstext ein:</span><span class="sxs-lookup"><span data-stu-id="c5d88-159">Enter the following JSON as your request body:</span></span>

    ```json
    {
        "type": "object",
        "properties": {
            "webUrl": {
                "type": "string"
            },
            "parameters": {
                "type": "object",
                "properties": {
                    "event": {
                        "type": "string"
                    },
                    "product": {
                        "type": "string"
                    }
                }
            }
        }
    }
    ``` 

1. <span data-ttu-id="c5d88-160">Klicken Sie auf **+ Neuer Schritt** und anschließend auf **Aktion hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-160">Select **+ New Step** and select **Add an action**</span></span>
1. <span data-ttu-id="c5d88-161">Suchen Sie nach **Azure-Warteschlangen**, und wählen Sie **Azure-Warteschlangen - Nachricht in einer Warteschlange ablegen** aus.</span><span class="sxs-lookup"><span data-stu-id="c5d88-161">Search for **Azure Queues** and select **Azure Queues - Put a message on a queue**</span></span>
1. <span data-ttu-id="c5d88-162">Geben Sie einen aussagekräftigen Namen für die Verbindung ein.</span><span class="sxs-lookup"><span data-stu-id="c5d88-162">Enter a name for the connection, this can be anything descriptive</span></span>
1. <span data-ttu-id="c5d88-163">Geben Sie den Namen des Speicherkontos ein, den Sie sich im vorherigen Abschnitt notiert haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-163">Enter the storage account name you copied in the previous section</span></span>
1. <span data-ttu-id="c5d88-164">Geben Sie den freigegebenen Speicherschlüssel ein, also den Wert aus dem Feld **Key1 key value** in Ihrem Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="c5d88-164">Enter the storage shared key, which is the value of the **Key1 key value** of your storage account.</span></span>
1. <span data-ttu-id="c5d88-165">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-165">Choose **Create**.</span></span>
1. <span data-ttu-id="c5d88-166">Geben Sie **pnpprovisioningqueue** als Namen für die Warteschlange ein.</span><span class="sxs-lookup"><span data-stu-id="c5d88-166">Select **pnpprovisioningqueue** for the queue name.</span></span>
1. <span data-ttu-id="c5d88-167">Im Anforderungstext haben Sie einen Eingangsparameter *webUrl* angegeben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-167">In the body specified in step 4 we specified an incoming parameter called webUrl.</span></span> <span data-ttu-id="c5d88-168">Der Wert dieses Felds soll in die Warteschlange gestellt werden. Klicken Sie dazu in das Feld **Nachricht**, und wählen Sie aus der dynamischen Inhaltsauswahl die Option **webUrl** aus.</span><span class="sxs-lookup"><span data-stu-id="c5d88-168">To put the value of that field in the queue, click in the **message** field and select **webUrl** from the Dynamic Content picker.</span></span>
1. <span data-ttu-id="c5d88-169">Klicken Sie auf **Flow speichern**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-169">Choose **Save Flow**.</span></span> <span data-ttu-id="c5d88-170">Es wird eine URL generiert. Diese URL notieren Sie sich im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="c5d88-170">This will generate the URL we will copy in the next step.</span></span>
1. <span data-ttu-id="c5d88-171">Klicken Sie auf den ersten Schritt in Ihrem Flow („Beim Empfang einer HTTP-Anforderung“), und notieren Sie sich die URL.</span><span class="sxs-lookup"><span data-stu-id="c5d88-171">Click on the first step in your flow ('When an HTTP request is received') and copy the URL.</span></span>
1. <span data-ttu-id="c5d88-172">Speichern Sie Ihren Flow.</span><span class="sxs-lookup"><span data-stu-id="c5d88-172">Save your flow.</span></span>

<span data-ttu-id="c5d88-173">Ihr Flow sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="c5d88-173">Your code should look like the following TypeScript.</span></span>

![Screenshot eines Flows mit dem Namen „Beim Empfang einer HTTP-Anforderung“, mit den Feldern „URL“, „Anforderungstext“, „Warteschlangenname“ und „Nachricht“](images/pnpprovisioning-flow-overview.png)

## <a name="test-the-flow"></a><span data-ttu-id="c5d88-175">Testen des Flows</span><span class="sxs-lookup"><span data-stu-id="c5d88-175">Test the flow</span></span>

<span data-ttu-id="c5d88-176">Zum Testen Ihres Flows müssen Sie eine POST-Anforderung senden.</span><span class="sxs-lookup"><span data-stu-id="c5d88-176">In order to test your flow you have will have to make a post request.</span></span> <span data-ttu-id="c5d88-177">Das können Sie über die PowerShell tun, wie im Beispiel unten demonstriert:</span><span class="sxs-lookup"><span data-stu-id="c5d88-177">You can do this via PowerShell, as shown in the following example.</span></span>

```powershell
$uri = "[the URI you copied in step 14 when creating the flow]"
$body = "{webUrl:'somesiteurl'}
Invoke-RestMethod -Uri $uri -Method Post -ContentType "application/json" -Body $body
```

<span data-ttu-id="c5d88-178">Wenn Sie zum Hauptbildschirm des Flows navigieren, sehen Sie einen Ausführungsverlauf.</span><span class="sxs-lookup"><span data-stu-id="c5d88-178">If you now navigate to the main screen of your flow you will see a run history.</span></span> <span data-ttu-id="c5d88-179">Wurde Ihr Flow korrekt ausgeführt, wird `Succeeded` angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c5d88-179">If your flow worked correctly, it will show `Succeeded`.</span></span>
<span data-ttu-id="c5d88-180">Navigieren Sie nun zu der Warteschlange, die Sie soeben in Azure erstellt haben, und klicken Sie auf **Aktualisieren**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-180">Now navigate to the queue you just created in Azure and click **Refresh**.</span></span> <span data-ttu-id="c5d88-181">Sie sollten nun einen Eintrag sehen. Ist das der Fall, wurde der Flow korrekt aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-181">You should see an entry that shows that you correctly invoked the flow.</span></span>

## <a name="provision-the-spfx-solution"></a><span data-ttu-id="c5d88-182">Bereitstellen der SPFx-Lösung</span><span class="sxs-lookup"><span data-stu-id="c5d88-182">Provision the SPFX Solution</span></span>

<span data-ttu-id="c5d88-183">In diesem Abschnitt verwenden Sie eine vorhandene SPFx-Lösung, den [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer).</span><span class="sxs-lookup"><span data-stu-id="c5d88-183">In this section, you'll use an existing SPFx solution, the [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer).</span></span> <span data-ttu-id="c5d88-184">Befolgen Sie die Anleitung in der Datei [Readme](https://github.com/SharePoint/sp-dev-fx-extensions/blob/master/samples/react-application-regions-footer/README.md) im Beispielrepository, um die Lösung zu erstellen und bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-184">Follow the steps in the [Readme](https://github.com/SharePoint/sp-dev-fx-extensions/blob/master/samples/react-application-regions-footer/README.md) file in the sample repo to build and provision the solution.</span></span>

## <a name="create-a-pnp-provisioning-template"></a><span data-ttu-id="c5d88-185">Erstellen einer PnP-Bereitstellungsvorlage</span><span class="sxs-lookup"><span data-stu-id="c5d88-185">Create a PnP Provisioning Template</span></span>

<span data-ttu-id="c5d88-186">Kopieren Sie die folgende XML-Bereitstellungsvorlage in eine neue Datei, und speichern Sie die Datei als „FlowDemoTemplate.xml“.</span><span class="sxs-lookup"><span data-stu-id="c5d88-186">Copy the following XML to a new file and save the file as FlowDemoTemplate.xml</span></span>

```xml
<?xml version="1.0"?>
<pnp:Provisioning xmlns:pnp="http://schemas.dev.office.com/PnP/2017/05/ProvisioningSchema">
  <pnp:Preferences Generator="OfficeDevPnP.Core, Version=2.20.1711.0, Culture=neutral, PublicKeyToken=3751622786b357c2" />
  <pnp:Templates ID="CONTAINER-FLOWDEMO">
    <pnp:ProvisioningTemplate ID="TEMPLATE-FLOWDEMO" Version="1" BaseSiteTemplate="GROUP#0" Scope="RootSite">
      <pnp:CustomActions>
        <pnp:WebCustomActions>
          <pnp:CustomAction Name="spfx-react-app-customizer" Description="Custom action for Application Customizer" Location="ClientSideExtension.ApplicationCustomizer" Title="spfx-react-app-customizer" Sequence="0" Rights="" RegistrationType="None" ClientSideComponentId="67fd1d01-84e8-4fbf-85bd-4b80768c6080" ClientSideComponentProperties="{&quot;SourceTermSetName&quot;:&quot;Regions&quot;}" />
        </pnp:WebCustomActions>
      </pnp:CustomActions>
    </pnp:ProvisioningTemplate>
  </pnp:Templates>
</pnp:Provisioning>
```

> [!NOTE]
> <span data-ttu-id="c5d88-187">Die Bereitstellungsvorlage fügt einer Lösung eine benutzerdefinierte Aktion hinzu.</span><span class="sxs-lookup"><span data-stu-id="c5d88-187">The provisioning template adds a custom action to a solution.</span></span> <span data-ttu-id="c5d88-188">Dabei ist **ClientSideComponentId** mit dem [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer) verknüpft, den Sie zuvor bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-188">The **ClientSideComponentId** is associated with the [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer) that you provisioned earlier.</span></span> <span data-ttu-id="c5d88-189">Wenn Sie diese Demo mit einer eigenen SPFx-Lösung ausführen, müssen Sie im XML-Code den Wert von **ClientSideComponentId** und optional auch die Attributwerte von **ClientSideComponentProperties** ändern.</span><span class="sxs-lookup"><span data-stu-id="c5d88-189">If you run this demo with your own SPFX Solution you will have to change the ClientSideComponentId and optionally the ClientSideComponentProperties attribute values in the XML.</span></span>

## <a name="create-the-azure-function"></a><span data-ttu-id="c5d88-190">Erstellen der Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="c5d88-190">Create the Azure Function</span></span>

1. <span data-ttu-id="c5d88-191">Rufen Sie das [Azure-Portal](https://portal.azure.com) auf.</span><span class="sxs-lookup"><span data-stu-id="c5d88-191">Go to the [Azure Portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="c5d88-192">Suchen Sie nach **Funktionen-App**, und erstellen Sie eine neue Funktionen-App.</span><span class="sxs-lookup"><span data-stu-id="c5d88-192">Search for 'Function App' and create a new Function App.</span></span> <span data-ttu-id="c5d88-193">Wählen Sie im Feld **Speicher** die Option **Use existing** aus. Wählen Sie dann das Speicherkonto aus, das Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-193">In the **Storage** field select **Use existing** and select your previously created storage account.</span></span> <span data-ttu-id="c5d88-194">Legen Sie die anderen Werte wie erforderlich fest.</span><span class="sxs-lookup"><span data-stu-id="c5d88-194">Set the other values as required.</span></span>
1. <span data-ttu-id="c5d88-195">Öffnen Sie die Funktionen-App, und klicken Sie auf **Funktionen** > **Neue Funktion**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-195">Open the Function app and select **Functions** > **New function**.</span></span>

    ![Screenshot des Azure-Portals mit hervorgehobener Option „Neue Funktion“](images/pnpprovisioning-create-function.png)

1. <span data-ttu-id="c5d88-197">Wählen Sie aus dem Dropdownfeld „Sprache“ die Option **PowerShell** aus.</span><span class="sxs-lookup"><span data-stu-id="c5d88-197">From the Language drop-down, select **PowerShell**.</span></span>
1. <span data-ttu-id="c5d88-198">Wählen Sie **QueueTrigger - PowerShell** aus.</span><span class="sxs-lookup"><span data-stu-id="c5d88-198">Select **QueueTrigger - PowerShell**.</span></span>
1. <span data-ttu-id="c5d88-199">Geben Sie der Funktion den Namen **ApplyPnPProvisioningTemplate**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-199">Name the function **ApplyPnPProvisioningTemplate**</span></span> 
1. <span data-ttu-id="c5d88-200">Geben Sie den Namen der Warteschlange ein, die Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-200">Enter the name of the queue you created earlier.</span></span>
1. <span data-ttu-id="c5d88-201">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-201">Choose **Create**.</span></span> <span data-ttu-id="c5d88-202">Es wird ein Editor geöffnet, in den Sie PowerShell-Cmdlets eingeben können.</span><span class="sxs-lookup"><span data-stu-id="c5d88-202">An editor where you can enter PowerShell cmdlets will open.</span></span> 

<span data-ttu-id="c5d88-203">Im nächsten Schritt laden Sie das PnP-PowerShell-Modul hoch, damit Sie es in der Azure-Funktion verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c5d88-203">Next, you'll upload the PnP PowerShell module so that you can use it in the Azure Function.</span></span>

## <a name="upload-the-pnp-powershell-module-for-your-azure-function"></a><span data-ttu-id="c5d88-204">Hochladen des PnP-PowerShell-Moduls für Ihre Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="c5d88-204">Upload the PnP PowerShell module for your Azure Function</span></span>

<span data-ttu-id="c5d88-205">Sie müssen das PnP-PowerShell-Modul zunächst herunterladen, bevor Sie es für Ihre Azure-Funktion hochladen können.</span><span class="sxs-lookup"><span data-stu-id="c5d88-205">You'll need to download the PnP PowerShell module so that you can upload it for your Azure Function.</span></span>

1. <span data-ttu-id="c5d88-206">Erstellen sie einen temporären Ordner auf Ihrem Computer.</span><span class="sxs-lookup"><span data-stu-id="c5d88-206">Create a temporary folder somewhere on your computer</span></span>
1. <span data-ttu-id="c5d88-207">Starten Sie PowerShell, und geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="c5d88-207">Launch PowerShell and enter the following:</span></span>
    ```powershell
    Save-Module -Name SharePointPnPPowerShellOnline -Path [pathtoyourfolder]
    ```
<span data-ttu-id="c5d88-208">Die Dateien des PowerShell-Moduls werden in einen Unterordner des von Ihnen erstellten Ordners heruntergeladen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-208">The PowerShell module files will download to a folder within the folder that you created.</span></span> 

<span data-ttu-id="c5d88-209">Als Nächstes laden Sie die Dateien hoch, damit Ihre Azure-Funktion das Modul verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="c5d88-209">Next, upload the files so that your Azure Function can use the module.</span></span>

1. <span data-ttu-id="c5d88-210">Navigieren Sie zur Hauptseite Ihrer Funktionen-App, und klicken Sie auf **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-210">Navigate to the main page of your Function App and select **Platform Features**</span></span>

    ![Screenshot der Funktionen-App mit hervorgehobener Option „Plattformfeatures“](images/pnpprovisioning-platform-features.png)

1. <span data-ttu-id="c5d88-212">Klicken Sie auf **Erweiterte Tools (Kudu)**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-212">Select Advanced Tools (Kudu))</span></span>

    ![Screenshot der Liste „Entwicklungstools“ mit hervorgehobener Option „Erweiterte Tools (Kudu)“](images/pnpprovisioning-select-kudu.png)

1. <span data-ttu-id="c5d88-214">Klicken Sie auf der Kudu-Hauptseite auf **Debugging-Konsole**, und wählen Sie entweder **CMD** oder **PowerShell** aus.</span><span class="sxs-lookup"><span data-stu-id="c5d88-214">On the main Kudu page, select **Debug Console** and pick either **CMD** or **PowerShell**</span></span>
1. <span data-ttu-id="c5d88-215">Klicken Sie in den Datei-Explorer oben auf der Seite, und rufen Sie **site\wwwroot\\[NameIhrerAzureFunktion]** auf.</span><span class="sxs-lookup"><span data-stu-id="c5d88-215">Choose the file explorer on the upper part of the page, and go to **site\wwwroot\\[nameofyourazurefunction]**.</span></span>
1. <span data-ttu-id="c5d88-216">Erstellen Sie einen neuen Ordner mit dem Namen **modules**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-216">Create a new folder and call that folder **modules**</span></span>
    
    ![Screenshot mit der hervorgehobenen Option „Neuer Ordner“](images/pnpprovisioning-kudu-create-folder.png)

1. <span data-ttu-id="c5d88-218">Erstellen Sie im Ordner „modules“ einen Ordner mit dem Namen **SharePointPnPPowerShellOnline**, und wechseln Sie in diesen Ordner.</span><span class="sxs-lookup"><span data-stu-id="c5d88-218">In the modules folder, create another folder called **SharePointPnPPowerShellOnline** and go to that folder.</span></span>
1. <span data-ttu-id="c5d88-219">Navigieren Sie im Datei-Explorer auf Ihrem Computer zu dem Ordner, in den Sie die Dateien des PnP-PowerShell-Moduls heruntergeladen haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-219">In your File Explorer on your computer navigate to the folder where you downloaded all the PnP PowerShell Module files.</span></span> <span data-ttu-id="c5d88-220">Öffnen Sie den Ordner **SharePointPnPPowerShellOnline\2.20.1711.0**. (Die Versionsnummer ist möglicherweise eine andere.)</span><span class="sxs-lookup"><span data-stu-id="c5d88-220">Open the **SharePointPnPPowerShellOnline\2.20.1711.0** folder (notice that depending on when you follow this walkthrough the version number can be different).</span></span>
1. <span data-ttu-id="c5d88-221">Ziehen Sie alle Dateien aus diesem Ordner per Drag-and-Drop in den Ordner in Kudu, um sie hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-221">Drag and drop all the files from this folder into the folder in Kudu to upload them.</span></span>

   ![Screenshot des Kudu-Ordners mit 40 hinzugefügten Dateien](images/pnpprovisioning-module-files-uploaded.png)

## <a name="finish-the-azure-function"></a><span data-ttu-id="c5d88-223">Fertigstellen der Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="c5d88-223">Finishing the Azure Function</span></span>

1. <span data-ttu-id="c5d88-224">Wechseln Sie wieder zu Ihrer Azure-Funktion, und erweitern Sie die Registerkarte mit den Dateien.</span><span class="sxs-lookup"><span data-stu-id="c5d88-224">Navigate back to your Azure Function and expand the files tab to the right.</span></span>

    ![Screenshot der Registerkarte „Dateien anzeigen“](images/pnpprovisioning-view-files.png)

1. <span data-ttu-id="c5d88-226">Klicken Sie auf **Hochladen**, und laden Sie die Bereitstellungsvorlagendatei hoch, die Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-226">Select **Upload** and upload your provisioning template file you created earlier.</span></span>
1. <span data-ttu-id="c5d88-227">Ersetzen Sie das PowerShell-Skript durch folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="c5d88-227">Replace the PowerShell script with the following</span></span>

    ```powershell
    $in = Get-Content $triggerInput -Raw
    Write-Output "Incoming request for '$in'"
    Connect-PnPOnline -AppId $env:SPO_AppId -AppSecret $env:SPO_AppSecret -Url $in
    Write-Output "Connected to site"
    Apply-PnPProvisioningTemplate -Path D:\home\site\wwwroot\ApplyPnPProvisioningTemplate\FlowDemoTemplate.xml
    ```

<span data-ttu-id="c5d88-228">Wie Sie sehen, verwenden Sie zwei Umgebungsvariablen: ```SPO_AppId``` und ```SPO_AppSecret```.</span><span class="sxs-lookup"><span data-stu-id="c5d88-228">Notice that you're using two environment variables: ```SPO_AppId```and ```SPO_AppSecret```.</span></span> <span data-ttu-id="c5d88-229">Zum Festlegen dieser Variablen navigieren Sie zur Hauptseite der Funktionen-App im Azure-Portal, klicken auf **Anwendungseinstellungen** und fügen zwei neue Anwendungseinstellungen hinzu:</span><span class="sxs-lookup"><span data-stu-id="c5d88-229">To set those variables, go to the main Function App page in the Azure Portal, select **Application Settings**, and add two new application settings:</span></span>

1. <span data-ttu-id="c5d88-230">```SPO_AppId```: Tragen Sie hier als Wert die Client-ID ein, die Sie sich im ersten Schritt notiert haben, als Sie die App auf Ihrem Mandanten erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-230">```SPO_AppId```: set the value to the Client Secret you copied in the first step when creating your app on your tenant.</span></span>
2. <span data-ttu-id="c5d88-231">```SPO_AppSecret```: Tragen Sie hier als Wert den geheimen Clientschlüssel ein, den Sie sich im ersten Schritt notiert haben, als Sie die App auf Ihrem Mandanten erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-231">```SPO_AppSecret```: set the value to the Client Secret you copied in the first step when creating your app on your tenant.</span></span>

## <a name="create-the-site-design"></a><span data-ttu-id="c5d88-232">Erstellen des Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="c5d88-232">Create the site design</span></span>

<span data-ttu-id="c5d88-233">Öffnen Sie PowerShell, und vergewissern Sie sich, dass Sie die Microsoft Office 365-Verwaltungsshell installiert haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-233">Open PowerShell and make sure you have the Microsoft Office 365 Management Shell installed.</span></span>

<span data-ttu-id="c5d88-234">Stellen Sie über **Connect-SPOService** eine Verbindung zu Ihrem Mandanten her.</span><span class="sxs-lookup"><span data-stu-id="c5d88-234">First connect to your tenant using Connect-SPOService:</span></span>

```powershell
Connect-SPOService -Url https://[yourtenant]-admin.sharepoint.com
```

<span data-ttu-id="c5d88-235">Nun können Sie die vorhandenen Websitedesigns abrufen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-235">Now you can get the existing site designs.</span></span> 

```powershell
Get-SPOSiteDesign
```

<span data-ttu-id="c5d88-236">Bevor Sie ein Websitedesign erstellen können, müssen Sie zuerst ein Websiteskript erstellen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-236">To create a site design, you first need to create a site script.</span></span> <span data-ttu-id="c5d88-237">Ein Websitedesign ist ein Container, der ein oder mehrere Websiteskripts referenziert.</span><span class="sxs-lookup"><span data-stu-id="c5d88-237">A site design is a container that refers to one or more site scripts.</span></span>

1. <span data-ttu-id="c5d88-238">Kopieren Sie den folgenden JSON-Code in die Zwischenablage, und ändern Sie ihn.</span><span class="sxs-lookup"><span data-stu-id="c5d88-238">Copy the following JSON code to your clipboard and modify it.</span></span> <span data-ttu-id="c5d88-239">Geben Sie für die Eigenschaft **url** den Wert ein, den Sie sich bei der Erstellung des Flows notiert haben.</span><span class="sxs-lookup"><span data-stu-id="c5d88-239">Set the url property to the value you copied when creating the flow.</span></span> <span data-ttu-id="c5d88-240">Die URL sieht in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="c5d88-240">The control looks similar to the following.</span></span>

    `https://prod-27.westus.logic.azure.com:443/workflows/ef7434cf0d704dd48ef5fb6...oke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun`

        ```json
        {
            "$schema": "schema.json",
            "actions": [
            {
                    "verb": "triggerFlow",
                    "url": "[paste the workflow trigger URL here]",
                    "name": "Apply Template",
                    "parameters": {
                        "event":"",
                        "product":""
                    }
            }
            ],
            "bindata": {},
            "version": 1
        }
        ```

1. <span data-ttu-id="c5d88-241">Markieren Sie den JSON-Code erneut, und kopieren Sie ihn nochmals in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="c5d88-241">Select the JSON again and copy it again to your clipboard.</span></span>
1. <span data-ttu-id="c5d88-242">Öffnen Sie PowerShell, und geben Sie Folgendes ein, um das Skript in eine Variable zu kopieren und das Websiteskript zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="c5d88-242">Open PowerShell and enter the following to copy the script into a variable and create the site script</span></span>

    ```powershell
    $script = Get-Clipboard -Raw
    Add-SPOSiteScript -Title "Apply PnP Provisioning Template" -Content $script
    Get-SPOSiteScript
    ```

1. <span data-ttu-id="c5d88-243">Es wird eine Liste mit einem oder mehreren Skripts angezeigt, einschließlich des soeben erstellten Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="c5d88-243">You should be presented with a list of one or more site scripts, including the site script you just created</span></span> <span data-ttu-id="c5d88-244">Markieren Sie die ID des Websiteskripts, das Sie soeben erstellt haben, und kopieren Sie sie in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="c5d88-244">Select the ID of the Site Script you just created and copy it to the clipboard</span></span>
1. <span data-ttu-id="c5d88-245">Erstellen Sie mithilfe des folgenden Befehls das Websitedesign:</span><span class="sxs-lookup"><span data-stu-id="c5d88-245">Use the following command to create the site design:</span></span>

    ```powershell
    Add-SPOSiteDesign -Title "Site with footer" -SiteScripts [Paste the ID of the Site Script here] -WebTemplate "64"
    ```

<span data-ttu-id="c5d88-246">Das Cmdlet **Add-SPOSiteDesign** verknüpft das Websitedesign mit der Teamwebsite.</span><span class="sxs-lookup"><span data-stu-id="c5d88-246">The **Add-SPOSiteDesign** cmdlet associates the site design with the team site.</span></span> <span data-ttu-id="c5d88-247">Wenn Sie das Design mit einer Kommunikationswebsite verknüpfen möchten, müssen Sie den Wert „68“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="c5d88-247">If you want to associate the design with a Communication Site use "68".</span></span>

## <a name="verify-the-results"></a><span data-ttu-id="c5d88-248">Überprüfen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="c5d88-248">Verify the results</span></span>

<span data-ttu-id="c5d88-249">Nachdem Sie Ihren Azure Queue-Speicher erstellt haben, haben Sie eine App-ID für App-exklusiven Zugriff, die Azure-Funktion und das Websitedesign erstellt.</span><span class="sxs-lookup"><span data-stu-id="c5d88-249">After you created your Azure Queue storage, you created the app ID for app-only access, the Azure Function, and the site design.</span></span> <span data-ttu-id="c5d88-250">Anschließend haben Sie über das Websitedesign Microsoft Flow ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="c5d88-250">You then triggered the Microsoft Flow from the site design.</span></span> 

<span data-ttu-id="c5d88-251">Um die Ergebnisse zu testen, müssen Sie nun eine neue Website erstellen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-251">To test the results, create a new site.</span></span> <span data-ttu-id="c5d88-252">Klicken Sie in Ihrem SharePoint-Mandanten auf **SharePoint** > **Website erstellen** > **Teamwebsite**.</span><span class="sxs-lookup"><span data-stu-id="c5d88-252">In your SharePoint tenant, select **SharePoint** > **Create Site** > **Team Site**.</span></span> <span data-ttu-id="c5d88-253">Ihr neues Websitedesign sollte als Designoption angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c5d88-253">Your new site design should show up as a design option.</span></span> <span data-ttu-id="c5d88-254">Dabei ist zu beachten, dass das Websitedesign nach der Erstellung der Website angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="c5d88-254">Notice that the site design is applied after the site is created.</span></span> <span data-ttu-id="c5d88-255">Wenn Sie es ordnungsgemäß konfiguriert haben, wird Ihr Flow ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="c5d88-255">If you configured it all correctly you should see your flow being triggered.</span></span> <span data-ttu-id="c5d88-256">Ob der Flow korrekt ausgeführt wurde, können Sie in seinem Ausführungsverlauf überprüfen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-256">You can check the run history of the flow to verify that it ran correctly.</span></span> <span data-ttu-id="c5d88-257">Die Fußzeile wird möglicherweise nicht sofort angezeigt. Falls sie nicht angezeigt wird: Warten Sie eine Minute, und laden Sie Ihre Website neu, um es nochmals zu versuchen.</span><span class="sxs-lookup"><span data-stu-id="c5d88-257">Note that the footer might not show up immediately; if you don't see it, wait a minute and reload your site to check again.</span></span>


