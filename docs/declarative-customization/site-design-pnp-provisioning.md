---
title: "Erstellen eines vollständigen SharePoint-Websitedesigns mithilfe des PnP-Bereitstellungsmoduls"
description: "Erstellen eines vollständigen SharePoint-Websitedesigns mithilfe des PnP-Bereitstellungsmoduls"
ms.date: 12/14/2017
ms.openlocfilehash: 303aca9f0103634e247ec75a0323321a77709113
ms.sourcegitcommit: 28690b54f1ef7c811d64393d2eaaff0a8635cc72
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="calling-the-pnp-provisioning-engine-from-a-site-script"></a><span data-ttu-id="c2b1f-103">Aufrufen des PnP-Bereitstellungsmoduls aus einem Websiteskript</span><span class="sxs-lookup"><span data-stu-id="c2b1f-103">Calling the PnP Provisioning Engine from a Site Script</span></span>

> [!NOTE]
> <span data-ttu-id="c2b1f-104">Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="c2b1f-105">Sie werden in Produktionsumgebungen derzeit nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="c2b1f-106">Websitedesigns bieten eine hervorragende Möglichkeit, das Aussehen und Verhalten Ihrer Websitesammlungen zu standardisieren.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-106">Site Designs offer a great way to standardize the look and feel of your site collections.</span></span> <span data-ttu-id="c2b1f-107">Wenn Sie jedoch noch einen Schritt weitergehen möchten, indem Sie beispielsweise jeder Seite eine Fußzeile hinzufügen, werden Sie feststellen, dass Websitedesigns diese Option nicht bieten.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-107">But if you want to take this one step further, by for instance adding a footer to every page, you might notice that Site Designs do not offer you that option.</span></span> <span data-ttu-id="c2b1f-108">Mit dem PnP-Bereitstellungsmodul können Sie eine Vorlage erstellen, mit der Sie einen Application Customizer für eine Website bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-108">With the PnP Provisioning engine you can hover create a template which allows you to provision an application customizer to a site.</span></span> <span data-ttu-id="c2b1f-109">Dieser Application Customizer kann dann auf jeder Seite eine Fußzeile registrieren.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-109">This application customizer then can register a footer on every page.</span></span> <span data-ttu-id="c2b1f-110">In diesem Artikel erfahren Sie, wie ein Websitedesign erstellt wird, das eine PnP-Bereitstellungsvorlage auf eine Website anwendet, die wiederum einen Application Customier zum Rendern einer Fußzeile hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-110">In this article you will learn how to create a site design that applies a PnP Provisioning Template to a site which in turn will add an application customizer to render a footer.</span></span>

<span data-ttu-id="c2b1f-111">In unserem Setup werden die folgenden Komponenten verwendet:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-111">We use the following components in our setup:</span></span>

1. <span data-ttu-id="c2b1f-112">Ein Websitedesign und ein Websiteskript</span><span class="sxs-lookup"><span data-stu-id="c2b1f-112">A Site Design and a Site Script</span></span>
1. <span data-ttu-id="c2b1f-113">Ein Microsoft-Fluss</span><span class="sxs-lookup"><span data-stu-id="c2b1f-113">A Microsoft Flow</span></span>
1. <span data-ttu-id="c2b1f-114">Eine Azure-Speicherwarteschlange</span><span class="sxs-lookup"><span data-stu-id="c2b1f-114">An Azure Storage Queue</span></span>
1. <span data-ttu-id="c2b1f-115">Eine Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="c2b1f-115">An Azure Function</span></span>
1. <span data-ttu-id="c2b1f-116">Eine SPFX-Lösung</span><span class="sxs-lookup"><span data-stu-id="c2b1f-116">An SPFX Solution</span></span>
1. <span data-ttu-id="c2b1f-117">Eine PnP-Bereitstellungsvorlage</span><span class="sxs-lookup"><span data-stu-id="c2b1f-117">A PnP Provisioning Template</span></span>
1. <span data-ttu-id="c2b1f-118">Ein PnP-PowerShell-Skript</span><span class="sxs-lookup"><span data-stu-id="c2b1f-118">A PnP PowerShell Script</span></span>
1. <span data-ttu-id="c2b1f-119">Eine AppID und ein AppSecret mit Verwaltungsrechten auf Ihrem Mandanten.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-119">An AppId and AppSecret with administration rights on your tenant.</span></span>

<span data-ttu-id="c2b1f-120">Wir benötigen alle diese Komponenten, damit wir den PnP-Bereitstellungscode in kontrollierter Weise auslösen können, direkt nachdem die Website erstellt und das Websitedesign angewendet wurde.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-120">We need all these component so we can trigger the PnP Provisioning code in a controller manner right after the site has been created and the Site Design is being applied.</span></span>

## <a name="setting-up-app-only-access-to-your-tenant"></a><span data-ttu-id="c2b1f-121">Einrichten des Nur-App-Zugriffs auf Ihren Mandanten</span><span class="sxs-lookup"><span data-stu-id="c2b1f-121">Setting up App Only Access to your tenant</span></span>

<span data-ttu-id="c2b1f-122">Hierfür müssen Sie zwei unterschiedliche Seiten auf Ihrem Mandanten öffnen, eine, die sich in einer normalen Website befindet, und eine andere, die sich in Ihrer SharePoint-Administrationswebsite befindet.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-122">This requires that you open 2 different pages on your tenant, one located in a normal site, the other located in your SharePoint Administration site.</span></span>

1. <span data-ttu-id="c2b1f-123">Navigieren Sie zu der folgenden URL in Ihrem Mandanten: https://[IhrMandant].sharepoint.com/_layouts/appregnew.aspx (Sie können zu einer beliebigen Website navigieren, aber vorerst sollten Sie die Stammwebsite auswählen).</span><span class="sxs-lookup"><span data-stu-id="c2b1f-123">Navigate to following URL in your tenant: https://[yourtenant].sharepoint.com/_layouts/appregnew.aspx (you can navigate to any site, but for now pick the root site)</span></span>
1. <span data-ttu-id="c2b1f-124">Klicken Sie auf die beiden Schaltflächen **Generieren**.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-124">Click both **Generate** buttons</span></span>
1. <span data-ttu-id="c2b1f-125">Geben Sie einen Titel für Ihre App ein, z. B. „Websitebereitstellung“.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-125">Enter a title for your App, for instance "Site Provisioning"</span></span>
1. <span data-ttu-id="c2b1f-126">Geben Sie als App-Domäne **localhost** ein.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-126">Enter **localhost** as the App Domain</span></span>
1. <span data-ttu-id="c2b1f-127">Geben Sie für den Umleitungs-URI **https://localhost** ein.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-127">Enter **http://localhost:3000/token** as the Redirect URI.</span></span>

    ![App erstellen](images/pnpprovisioning-createapponly.png)

1. <span data-ttu-id="c2b1f-129">Klicken Sie auf **Erstellen**, und kopieren Sie die Werte für **Client-ID** und **Geheimer Clientschlüssel**, da Sie diese später benötigen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-129">Click **Create** and copy the values for **Client Id** and **Client Secret** as you will need them later</span></span>

<span data-ttu-id="c2b1f-130">Nun vertrauen wir dieser App, dass sie über den entsprechenden Zugriff auf Ihren Mandanten verfügt:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-130">Now we will trust this app to have the appropriate access to your tenant:</span></span>
1. <span data-ttu-id="c2b1f-131">Navigieren Sie zu „https://[IhrMandant]-admin.sharepoint.com/_layouts/appinv.aspx“ (beachten Sie den Abschnitt „-admin“ in der URL).</span><span class="sxs-lookup"><span data-stu-id="c2b1f-131">Navigate to https://[yourtenant]-admin.sharepoint.com/_layouts/appinv.aspx (notice the -admin in the URL)</span></span>
1. <span data-ttu-id="c2b1f-132">Fügen Sie die oben kopierte Client-ID in das Feld **App-ID**, und wählen Sie **Nachschlagen** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-132">Paste in the Client Id you copied above into the **App Id** field and select **Lookup**</span></span>
1. <span data-ttu-id="c2b1f-133">Fügen Sie den folgenden XML-Code in das Feld **Berechtigungsanforderungs-XML** ein.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-133">Paste the following XML in the **Permission Request XML** field:</span></span>

    ```xml
    <AppPermissionRequests AllowAppOnlyPolicy="true" >
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
    </AppPermissionRequests>
    ```

1. <span data-ttu-id="c2b1f-134">Wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-134">Select **Create**</span></span>
1. <span data-ttu-id="c2b1f-135">Es wird die Frage angezeigt, ob Sie der App vertrauen möchten.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-135">You will receive a question if you want to trust this app.</span></span> <span data-ttu-id="c2b1f-136">Bestätigen Sie dies, indem Sie **Vertrauen** auswählen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-136">Confirm this by selecting **Trust It**</span></span>


## <a name="creating-the-azure-storage-queue"></a><span data-ttu-id="c2b1f-137">Erstellen der Azure-Speicherwarteschlange</span><span class="sxs-lookup"><span data-stu-id="c2b1f-137">Creating the Azure Storage Queue</span></span>

<span data-ttu-id="c2b1f-138">In diesem Szenario verwenden wir eine Azure-Speicherwarteschlange, um Nachrichten von einem Microsoft-Flow zu empfangen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-138">In this scenario we will use an Azure Storage Queue to receive messages from a Microsoft Flow.</span></span> <span data-ttu-id="c2b1f-139">Jedes Mal, wenn eine Nachricht in der Speicherwarteschlange angezeigt wird, wird eine Azure-Funktion zum Ausführen eines PowerShell-Skripts ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-139">Every time a message shows up in the Storage Queue an Azure Function will get triggered to execute a PowerShell script.</span></span> <span data-ttu-id="c2b1f-140">Lassen Sie uns aber zunächst die Speicherwarteschlange einrichten:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-140">But let us set up the Storage Queue first:</span></span>

1. <span data-ttu-id="c2b1f-141">Navigieren Sie zum Azure-Portal unter „https://portal.azure.com“, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-141">Navigate to the Azure portal at https://portal.azure.com and log in.</span></span>
1. <span data-ttu-id="c2b1f-142">Wählen Sie **+Neu** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-142">Choose **+ New**</span></span>
1. <span data-ttu-id="c2b1f-143">Wählen Sie aus den Azure Marketplace-Angeboten **Speicher** aus, und wählen Sie in der Spalte „Unterstützt“ **Speicherkonto – Blob, Datei, Tabelle, Warteschlange**</span><span class="sxs-lookup"><span data-stu-id="c2b1f-143">Select **Storage** from the Azure Marketplace listings and select **Storage account - blob, file, table, queue** in the Featured column</span></span>
1. <span data-ttu-id="c2b1f-144">Geben Sie für die erforderlichen Felder entsprechende Werte ein.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-144">Provide values for the required fields as requested.</span></span> <span data-ttu-id="c2b1f-145">Wählen Sie unbedingt **An Dashboard anheften** aus, um die Option später leichter zu finden, und klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-145">Make sure to select **Pin to dashboard** for easy location later and click **Create**.</span></span> <span data-ttu-id="c2b1f-146">Das Speicherkonto wird erstellt.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-146">The storage account is being created.</span></span> <span data-ttu-id="c2b1f-147">Das kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-147">This might take a few minutes.</span></span>
1. <span data-ttu-id="c2b1f-148">Öffnen Sie das Speicherkonto, nachdem es erstellt wurde, und navigieren Sie in der Navigation zu **Warteschlangen**</span><span class="sxs-lookup"><span data-stu-id="c2b1f-148">Open the Storage Account after it has been created and navigate to **Queues** in the navigation</span></span>
1. <span data-ttu-id="c2b1f-149">Wählen Sie oben im Hauptbereich des Bildschirms **+ Warteschlange** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-149">Choose **+ Queue** at the top of the main area of the screen.</span></span>
1. <span data-ttu-id="c2b1f-150">Geben Sie **pnpprovisioningqueue** als Name ein, oder geben Sie einen eigenen Namen gemäß dem erzwungenen Benennungsstandard ein.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-150">Enter **pnpprovisioningqueue** as the name or enter your own following the naming standard that is enforced.</span></span> <span data-ttu-id="c2b1f-151">Notieren Sie sich den Warteschlangennamen, da Sie diesen Wert später beim Erstellen der Azure-Funktion benötigen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-151">Make a note of the queue name as you need this value later when creating the Azure Function.</span></span>
1. <span data-ttu-id="c2b1f-152">Navigieren Sie zu **Zugriffsschlüssel**, und notieren Sie sich den **Speicherkontonamen** und den **key1-Schlüsselwert**, da Sie diese Werte im nächsten Schritt beim Erstellen des Flusses benötigen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-152">Navigate to **Access Keys** and make note of the **Storage Account Name** and the **key1 Key value**, you will need those values in the next step where you create the flow.</span></span>


## <a name="the-flow"></a><span data-ttu-id="c2b1f-153">Der Fluss</span><span class="sxs-lookup"><span data-stu-id="c2b1f-153">The Flow</span></span>

<span data-ttu-id="c2b1f-154">Um eine Nachricht in der Warteschlange zu platzieren, müssen Sie einen Fluss erstellen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-154">In order to put a message on the queue we have to create a flow.</span></span> 

1. <span data-ttu-id="c2b1f-155">Navigieren Sie zu **https://flow.microsoft.com**, melden Sie sich an, und erstellen Sie einen neuen Fluss, indem Sie oben auf  **Ohne Vorlage erstellen** klicken.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-155">Navigate to **https://flow.microsoft.com**, log in and create a new flow by clicking **Create from Blank** at the top.</span></span>
1. <span data-ttu-id="c2b1f-156">Klicken Sie auf **Hunderte von Connectors und Triggern durchsuchen**, um den Auslöser auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-156">Click **Search hundreds of connectors and triggers** to select your trigger</span></span>
1. <span data-ttu-id="c2b1f-157">Suchen Sie nach **Anforderung**, und wählen Sie **Anforderung - Beim Empfang einer HTTP-Anforderung** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-157">Search for **Request** and select **Request - When a HTTP Request is received**</span></span>
1. <span data-ttu-id="c2b1f-158">Geben Sie den folgenden JSON-Code als Anforderungstext ein:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-158">Enter the following JSON as your request body:</span></span>

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

1. <span data-ttu-id="c2b1f-159">Wählen Sie **+ Neuer Schritt** aus, und klicken Sie dann auf **Aktion hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-159">Select **+ New Step** and select **Add an action**</span></span>
1. <span data-ttu-id="c2b1f-160">Suchen Sie nach **Azure-Warteschlangen**, und wählen Sie **Azure-Warteschlangen - Nachricht in einer Warteschlange ablegen** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-160">Search for **Azure Queues** and select **Azure Queues - Put a message on a queue**</span></span>
1. <span data-ttu-id="c2b1f-161">Geben Sie einen beliebigen aussagekräftigen Namen für die Verbindung ein. </span><span class="sxs-lookup"><span data-stu-id="c2b1f-161">Enter a name for the connection, this can be anything descriptive</span></span>
1. <span data-ttu-id="c2b1f-162">Geben Sie den Speicherkontonamen ein, den Sie im vorherigen Abschnitt kopiert haben.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-162">Enter the storage account name you copied in the previous section</span></span>
1. <span data-ttu-id="c2b1f-163">Geben Sie den freigegebenen Speicherschlüssel ein, bei dem es sich um den Wert des **Key1-Schlüsselwerts** Ihres Speicherkontos handelt.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-163">Enter the storage shared key, which is the value of the **Key1 key value** of your storage account.</span></span>
1. <span data-ttu-id="c2b1f-164">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-164">Click **Create**.</span></span>
1. <span data-ttu-id="c2b1f-165">Wählen Sie **pnpprovisioningqueue** als Warteschlangenname aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-165">Select **pnpprovisioningqueue** as the Queue Name.</span></span>
1. <span data-ttu-id="c2b1f-166">In dem in Schritt 4 angegebenen Text haben wir einen eingehenden Parameter mit dem Namen „webUrl“ angegeben.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-166">In the body specified in step 4 we specified an incoming parameter called webUrl.</span></span> <span data-ttu-id="c2b1f-167">Wir werden den Wert dieses Parameters in der Warteschlange ablegen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-167">We will put the value of that parameter on the queue.</span></span> <span data-ttu-id="c2b1f-168">Klicken Sie in das Feld **Nachricht**, und wählen Sie aus der Auswahl für dynamische Inhalte **webUrl** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-168">Click in the **message** field and select **webUrl** from the Dynamic Content picker.</span></span>
1. <span data-ttu-id="c2b1f-169">Klicken Sie auf **Flow speichern**.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-169">Click **Save Flow**.</span></span> <span data-ttu-id="c2b1f-170">Daraufhin wird die URL generiert, die wir im nächsten Schritt kopieren werden.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-170">This will generate the URL we will copy in the next step.</span></span>
1. <span data-ttu-id="c2b1f-171">Klicken Sie auf den ersten Schritt in Ihrem Flow („Beim Empfang einer HTTP-Anforderung), und kopieren Sie die URL.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-171">Click on the first step in your flow ('When an HTTP request is received') and copy the URL.</span></span> <span data-ttu-id="c2b1f-172">Wir benötigen diese, um zum späteren Testen in unserem Websitedesign.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-172">We will need that to test and later on in our Site Design.</span></span>
1. <span data-ttu-id="c2b1f-173">Speichern Sie Ihren Flow.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-173">Save your flow.</span></span>

<span data-ttu-id="c2b1f-174">Dieser sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-174">Your registry should look like this: </span></span>

![Hyperion](images/pnpprovisioning-flow-overview.png)

## <a name="testing-the-flow"></a><span data-ttu-id="c2b1f-176">Testen des Flows</span><span class="sxs-lookup"><span data-stu-id="c2b1f-176">Testing the flow</span></span>

<span data-ttu-id="c2b1f-177">Um Ihren Flow zu testen, müssen Sie eine POST-Anforderung stellen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-177">In order to test your flow you have will have to make a post request.</span></span> <span data-ttu-id="c2b1f-178">Am einfachsten ist hierfür auf einem Windows-Computer die Verwendung von PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-178">The easiest for that, if you are on a Windows PC, is to use PowerShell:</span></span>

```powershell
$uri = "[the URI you copied in step 8 when creating the flow]"
$body = "{webUrl:'somesiteurl'}
Invoke-RestMethod -Uri $uri -Method Post -ContentType "application/json" -Body $body
```

<span data-ttu-id="c2b1f-179">Wenn Sie nun zum Hauptbildschirm des Flows navigieren, sehen Sie einen Ausführungsverlauf.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-179">If you now navigate to the main screen of your flow you will see a run history.</span></span> <span data-ttu-id="c2b1f-180">Wenn alles ordnungsgemäß verlief, sollte dieser „Succeeded“ lauten.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-180">If everything went okay it should say 'Succeeded'.</span></span>
<span data-ttu-id="c2b1f-181">Navigieren Sie nun zur Warteschlange, die Sie soeben in Azure erstellt haben, und klicken Sie auf **Aktualisieren**.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-181">Now navigate to the queue you just created in Azure and click **Refresh**.</span></span> <span data-ttu-id="c2b1f-182">Es sollte ein Eintrag vorhanden sein, der angibt, dass Sie den Flow korrekt aufgerufen haben.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-182">There should be an entry showing that you correctly invoked the Flow.</span></span>

## <a name="provision-the-spfx-solution"></a><span data-ttu-id="c2b1f-183">Bereitstellen der SPFX-Lösung</span><span class="sxs-lookup"><span data-stu-id="c2b1f-183">Provision the SPFX Solution</span></span>

<span data-ttu-id="c2b1f-184">Für diese exemplarische Vorgehensweise verwenden wir eine vorhandene SPFX-Lösung, die unter „https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer“ verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-184">For this walkthrough we are going to use an existing SPFX solution which is available at https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer</span></span>

<span data-ttu-id="c2b1f-185">Befolgen Sie die Schritte wie in der „README.MD“, die in diesem Repository verfügbar ist, um die Lösung zu erstellen und bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-185">Follow the steps as provided in the README.MD available in that repository to build and provision your solution.</span></span>

# <a name="create-a-pnp-provisioning-template"></a><span data-ttu-id="c2b1f-186">Erstellen einer PnP-Bereitstellungsvorlage</span><span class="sxs-lookup"><span data-stu-id="c2b1f-186">Create a PnP Provisioning Template</span></span>

<span data-ttu-id="c2b1f-187">Kopieren Sie den folgenden XML-Code in eine neue Datei, und speichern Sie die Datei als „FlowDemoTemplate.xml“</span><span class="sxs-lookup"><span data-stu-id="c2b1f-187">Copy the following XML to a new file and save the file as FlowDemoTemplate.xml</span></span>

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
</pnp:Provisioning>
```

> [!NOTE]
> <span data-ttu-id="c2b1f-188">Die Vorlage fügt eine benutzerdefinierte Aktion zu dem Web hinzu, auf das sie angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-188">The template adds a custom action to the the web it is being applied to.</span></span> <span data-ttu-id="c2b1f-189">Sie verweist auf „ClientSideComponentId“, die aus der SPFX-Lösung stammt, die Sie zuvor bereitgestellt haben.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-189">It refers to ClientSideComponentId which is the one coming from the SPFX Solution you provisioned earlier.</span></span> <span data-ttu-id="c2b1f-190">Wenn Sie diese Demo mit Ihrer eigenen SPFX-Lösung ausführen, müssen Sie die „ClientSideComponentId“ und optional die Attributwerte „ClientSideComponentProperties“ in der XML ändern.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-190">If you run this demo with your own SPFX Solution you will have to change the ClientSideComponentId and optionally the ClientSideComponentProperties attribute values in the XML.</span></span>

## <a name="create-the-azure-function"></a><span data-ttu-id="c2b1f-191">Erstellen der Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="c2b1f-191">Create an Azure Function</span></span>

1. <span data-ttu-id="c2b1f-192">Navigieren Sie zum Azure-Portal unter „https://portal.azure.com“.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-192">Navigate to the Azure Portal at https://portal.azure.com.</span></span>
1. <span data-ttu-id="c2b1f-193">Suchen Sie nach „Funktionen-App“, und erstellen Sie eine neue Funktionen-App.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-193">Search for 'Function App' and create a new Function App.</span></span> <span data-ttu-id="c2b1f-194">Wählen Sie im Feld **Speicher** die Option, dass das vorhandene Speicherkonto ****verwendet wird, und wählen Sie das zuvor erstellte Speicherkonto aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-194">In the **Storage** field select **Use existing** and select your previously created storage account.</span></span> <span data-ttu-id="c2b1f-195">Legen Sie die anderen Werte wie erforderlich fest.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-195">Set the other values as required.</span></span>
1. <span data-ttu-id="c2b1f-196">Nachdem die Funktionen-App erstellt wurde, öffnen Sie sie, und wählen Sie **Funktionen** und dann **Neue Funktion** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-196">After the function app has been created open it and select **Functions**, then select **New function**.</span></span>

  ![Erstellen einer neuen Funktion](images/pnpprovisioning-create-function.png)

1. <span data-ttu-id="c2b1f-198">Wählen Sie aus der Dropdownliste „Sprache“ die Option **PowerShell** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-198">From the Language drop-down, select **PowerShell**.</span></span>
1. <span data-ttu-id="c2b1f-199">Wählen Sie **QueueTrigger - PowerShell** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-199">Select **QueueTrigger - PowerShell**.</span></span>
1. <span data-ttu-id="c2b1f-200">Geben Sie der Funktion den Namen **ApplyPnPProvisioningTemplate**.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-200">Name the function **ApplyPnPProvisioningTemplate**</span></span> 
1. <span data-ttu-id="c2b1f-201">Geben Sie den Namen der Warteschlange ein, die Sie in den vorherigen Schritten erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-201">Enter the name of your queue you created in the previous steps.</span></span>
1. <span data-ttu-id="c2b1f-202">Wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-202">Select **Create**</span></span>
1. <span data-ttu-id="c2b1f-203">Es wird ein Editor angezeigt, in dem Sie PowerShell-Cmdlets eingeben können.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-203">You will be presented with a Editor where you can enter PowerShell Cmdlets.</span></span> <span data-ttu-id="c2b1f-204">Wir laden nun das PnP-PowerShell-Modul hoch, damit wir es in der Azure-Funktion verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-204">We will now upload the PnP PowerShell module so we can use it in the Azure function.</span></span>

## <a name="uploading-pnp-powershell-for-your-azure-function"></a><span data-ttu-id="c2b1f-205">Hochladen von PnP-PowerShell für Ihre Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="c2b1f-205">Uploading PnP PowerShell for your Azure Function</span></span>

<span data-ttu-id="c2b1f-206">Wir müssen zuerst das PnP-PowerShell-Modul herunterladen, damit es später einfach hochgeladen werden kann.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-206">We first have to download the PnP PowerShell module so you can easy upload it later.</span></span>

1. <span data-ttu-id="c2b1f-207">Erstellen sie einen temporären Ordner auf Ihrem Computer.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-207">Create a temporary folder somewhere on your computer</span></span>
1. <span data-ttu-id="c2b1f-208">Starten Sie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-208">Launch PowerShell and enter</span></span>
    ```powershell
    Save-Module -Name SharePointPnPPowerShellOnline -Path [pathtoyourfolder]
    ```
1. <span data-ttu-id="c2b1f-209">Die PowerShell-Moduldateien werden in einen Ordner innerhalb des soeben ausgewählten Ordners heruntergeladen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-209">The PowerShell module files will be downloaded to a folder inside the folder you just selected.</span></span> 

<span data-ttu-id="c2b1f-210">Nun können Sie diese Dateien hochladen, damit die Azure-Funktion das Modul verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-210">Now it is time to upload those files so your Azure Function can make use of the module:</span></span>

1. <span data-ttu-id="c2b1f-211">Navigieren Sie zur Hauptseite der Funktionen-App, und wählen Sie **Plattformfeatures** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-211">Navigate to the main page of your Function App and select **Platform Features**</span></span>

    ![Navigieren Sie zu „Plattformfeatures“.](images/pnpprovisioning-platform-features.png)

1. <span data-ttu-id="c2b1f-213">Wählen Sie **Erweiterte Tools (Kudu)** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-213">Select **Advanced tools (Kudu)**</span></span>

    ![Wählen Sie „Erweiterte Tools (Kudu)“ aus.](images/pnpprovisioning-select-kudu.png)

1. <span data-ttu-id="c2b1f-215">Wählen Sie auf der Kudu-Hauptseite **Debugging-Konsole** aus, und klicken Sie entweder auf **CMD** oder auf **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-215">On the main Kudu page, select **Debug Console** and pick either **CMD** or **PowerShell**</span></span>
1. <span data-ttu-id="c2b1f-216">Im oberen Teil der Seite wird ein Datei-Explorer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-216">In the upper part of the page you see a file explorer.</span></span> <span data-ttu-id="c2b1f-217">Navigieren Sie zu **site\wwwroot\\[NameIhrerAzure-Funktion]**</span><span class="sxs-lookup"><span data-stu-id="c2b1f-217">Navigate to **site\wwwroot\\[nameofyourazurefunction]**</span></span>
1. <span data-ttu-id="c2b1f-218">Erstellen Sie einen neuen Ordner, und geben Sie diesem den Namen **modules**.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-218">Create a new folder and call that folder **modules**</span></span>
    
    ![Neuen Ordner erstellen](images/pnpprovisioning-kudu-create-folder.png)

1. <span data-ttu-id="c2b1f-220">Erstellen Sie in diesem Ordner einen weiteren Ordner mit dem Namen **SharePointPnPPowerShellOnline**, und navigieren Sie zu dem Ordner.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-220">In that folder create another folder called **SharePointPnPPowerShellOnline** and navigate to the folder</span></span>
1. <span data-ttu-id="c2b1f-221">Navigieren Sie im Datei-Explorer auf Ihrem Computer zu dem Ordner, aus dem Sie alle PnP-PowerShell-Moduldateien heruntergeladen haben.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-221">In your File Explorer on your computer navigate to the folder where you downloaded all the PnP PowerShell Module files.</span></span> <span data-ttu-id="c2b1f-222">Öffnen Sie den Ordner **SharePointPnPPowerShellOnline\2.20.1711.0** (beachten Sie, dass die Versionsnummer anders sein kann, wenn Sie diese exemplarische Vorgehensweise befolgen).</span><span class="sxs-lookup"><span data-stu-id="c2b1f-222">Open the **SharePointPnPPowerShellOnline\2.20.1711.0** folder (notice that depending on when you follow this walkthrough the version number can be different).</span></span>
1. <span data-ttu-id="c2b1f-223">Laden Sie alle Dateien in diesen Ordner hoch, indem Sie alle Dateien aus dem Ordner in den Ordner in Kudu ziehen und dort ablegen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-223">Upload all files in that folder by dragging and dropping all the files from this folder into the folder in Kudu.</span></span>

   ![Neuen Ordner erstellen](images/pnpprovisioning-module-files-uploaded.png)

## <a name="finishing-the-azure-function"></a><span data-ttu-id="c2b1f-225">Abschließen der Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="c2b1f-225">Finishing the Azure Function</span></span>

1. <span data-ttu-id="c2b1f-226">Navigieren Sie zurück zur Azure-Funktion, und erweitern Sie die Registerkarte „Dateien“ rechts.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-226">Navigate back to your Azure Function and expand the files tab to the right.</span></span>

    ![Dateien anzeigen](images/pnpprovisioning-view-files.png)

1. <span data-ttu-id="c2b1f-228">Klicken Sie auf **Hochladen**, und laden Sie Ihre Bereitstellungsvorlagendatei hoch, die Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-228">Select **Upload** and upload your provisioning template file you created earlier.</span></span>
1. <span data-ttu-id="c2b1f-229">Ersetzen Sie das PowerShell-Skript durch Folgendes:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-229">Replace the PowerShell script with the following</span></span>

```powershell
$in = Get-Content $triggerInput -Raw
Write-Output "Incoming request for '$in'"
Connect-PnPOnline -AppId $env:SPO_AppId -AppSecret $env:SPO_AppSecret -Url $in
Write-Output "Connected to site"
Apply-PnPProvisioningTemplate -Path D:\home\site\wwwroot\ApplyPnPProvisioningTemplate\FlowDemoTemplate.xml
```

<span data-ttu-id="c2b1f-230">Beachten Sie, dass wir zwei Umgebungsvariablen verwenden, eine mit dem Namen ```SPO_AppId```, die andere mit dem Namen ```SPO_AppSecret```.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-230">Notice that we are using 2 environment variables, one called ```SPO_AppId```, the other ```SPO_AppSecret```.</span></span> <span data-ttu-id="c2b1f-231">Um diese Variablen festzulegen, navigieren Sie zur Hauptseite der Funktionen-App in Ihrem Azure-Portal, wählen Sie **Anwendungseinstellungen** aus, und fügen Sie zwei neue Anwendungseinstellungen hinzu:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-231">In order to set those variables navigate to your main Function App page in your Azure Portal, select **Application Settings** and add two new Application Settings:</span></span>

1. <span data-ttu-id="c2b1f-232">```SPO_AppId```: Legen Sie den Wert auf die im ersten Schritt beim Erstellen der App auf dem Mandanten kopierte Client-ID fest.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-232">```SPO_AppId```: set the value to the Client Id you copied in the first step when creating your app on your tenant.</span></span>
2. <span data-ttu-id="c2b1f-233">```SPO_AppSecret```: Legen Sie den Wert auf den im ersten Schritt beim Erstellen der App auf dem Mandanten kopierten geheimen Clientschlüssel fest.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-233">```SPO_AppSecret```: set the value to the Client Secret you copied in the first step when creating your app on your tenant.</span></span>

## <a name="creating-the-site-design"></a><span data-ttu-id="c2b1f-234">Erstellen des Websitedesigns</span><span class="sxs-lookup"><span data-stu-id="c2b1f-234">Creating a Site Design</span></span>

<span data-ttu-id="c2b1f-235">Öffnen Sie PowerShell, und vergewissern Sie sich, dass Sie die Microsoft Office 365-Verwaltungsshell installiert haben.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-235">Open PowerShell and make sure you have the Microsoft Office 365 Management Shell installed.</span></span>

<span data-ttu-id="c2b1f-236">Stellen Sie zuerst über Connect-SPOService eine Verbindung zu Ihrem Mandanten her:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-236">First connect to your tenant using Connect-SPOService:</span></span>

```powershell
Connect-SPOService -Url https://[yourtenant]-admin.sharepoint.com
```

<span data-ttu-id="c2b1f-237">Nun können Sie die vorhandenen Websitedesigns abrufen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-237">Now you can retrieve the existing Site Designs using</span></span> 

```powershell
Get-SPOSiteDesign
```

<span data-ttu-id="c2b1f-238">Um ein Websitedesign zu erstellen, müssen Sie zuerst ein Websiteskript erstellen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-238">In order to create a Site Design you first need to create a Site Script.</span></span> <span data-ttu-id="c2b1f-239">Ein Websitedesign können Sie sich als Container vorstellen, der auf ein oder mehrere Webskripts verweist.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-239">Think of a Site Design as a container which refers to 1 or more Site Scripts.</span></span>
1. <span data-ttu-id="c2b1f-240">Kopieren Sie den folgenden JSON-Code in die Zwischenablage, und ändern Sie ihn.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-240">Copy the following JSON code to your clipboard and modify it.</span></span> <span data-ttu-id="c2b1f-241">Legen Sie die url-Eigenschaft auf den beim Erstellen des Flows kopierten Wert fest.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-241">Set the url property to the value you copied when creating the flow.</span></span> <span data-ttu-id="c2b1f-242">Die URL sieht wie `https://prod-27.westus.logic.azure.com:443/workflows/ef7434cf0d704dd48ef5fb6...oke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun` aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-242">The URL looks alike    `https://prod-27.westus.logic.azure.com:443/workflows/ef7434cf0d704dd48ef5fb6...oke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun`</span></span>

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

1. <span data-ttu-id="c2b1f-243">Nach dem Bearbeiten des JSON-Codes durch Einfügen der korrekten URL zum Auslösen des Flows, wählen Sie alles aus, und kopieren alles erneut in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-243">After modifying the JSON by inserting the correct URL to trigger your flow, select it all and copy it again to your clipboard</span></span>
1. <span data-ttu-id="c2b1f-244">Öffnen Sie PowerShell, und geben Sie Folgendes ein, um das Skript in eine Variable zu kopieren und das Websiteskript zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-244">Open PowerShell and enter the following to copy the script into a variable and create the site script</span></span>

    ```powershell
    $script = Get-Clipboard -Raw
    Add-SPOSiteScript -Title "Apply PnP Provisioning Template" -Content $script
    Get-SPOSiteScript
    ```

1. <span data-ttu-id="c2b1f-245">Es sollte eine Liste mit einem oder mehreren Skripts angezeigt werden, einschließlich des soeben erstellten Websiteskripts.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-245">You should be presented with a list of one or more site scripts, including the site script you just created</span></span>
1. <span data-ttu-id="c2b1f-246">Wählen Sie die ID des soeben erstellten Websiteskripts aus, und kopieren Sie sie in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-246">Select the ID of the Site Script you just created and copy it to the clipboard</span></span>
1. <span data-ttu-id="c2b1f-247">Erstellen Sie das Websitedesigns:</span><span class="sxs-lookup"><span data-stu-id="c2b1f-247">Create the Site Design:</span></span>

    ```powershell
    Add-SPOSiteDesign -Title "Site with footer" -SiteScripts [Paste the ID of the Site Script here] -WebTemplate "64"
    ```

<span data-ttu-id="c2b1f-248">Durch „ Add-SPOSiteDesign“ wird das Websitedesign der Teamwebsite zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-248">The Add-SPOSiteDesign will associate the site design with the Team Site.</span></span> <span data-ttu-id="c2b1f-249">Wenn Sie das Design einer Kommunikationswebsite zuweisen möchten, verwenden Sie „68“.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-249">If you want to associate the design with a Communication Site use "68".</span></span>

## <a name="conclusion"></a><span data-ttu-id="c2b1f-250">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="c2b1f-250">Conclusion</span></span>

<span data-ttu-id="c2b1f-251">Nachdem Sie die Speicherwarteschlange erstellt haben, haben Sie die App-ID für den Nur-App-Zugriff erstellt. Anschließend haben Sie die Azure-Funktion und das Websitedesign erstellt und den korrekten Microsoft-Flow vom Websitedesign ausgelöst. Sie sind jetzt startklar!</span><span class="sxs-lookup"><span data-stu-id="c2b1f-251">After you created your Storage Queue, you created the app Id for the app only access, you correctly created the Azure Function, you created the Site Design and triggered the correct Microsoft Flow from the Site Design, you are all good to go.</span></span> 

<span data-ttu-id="c2b1f-252">Versuchen Sie, eine neue Website zu erstellen, indem Sie zu Ihrem SharePoint-Mandanten navigieren.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-252">Try creating a new site by navigating to your SharePoint Tenant.</span></span> <span data-ttu-id="c2b1f-253">Wählen Sie **SharePoint**, **Website erstellen** und **Teamwebsite** aus.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-253">Select **SharePoint**, select **Create Site**, Select **Team Site**.</span></span> <span data-ttu-id="c2b1f-254">Ihr neu erstelltes Websitedesign sollte nun als mögliche Designoption angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-254">Your newly created Site Design should show up as a possible design option.</span></span> <span data-ttu-id="c2b1f-255">Erstellen Sie Ihre Website, und beachten Sie das Websitedesign, das angewendet wird, nachdem die Website erstellt wurde. </span><span class="sxs-lookup"><span data-stu-id="c2b1f-255">Create your site and notice the Site Design being applied after the site has been created.</span></span> <span data-ttu-id="c2b1f-256">Wenn Sie alles korrekt konfiguriert haben, sollte Ihr Flow nun ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-256">If you configured it all correctly you should see your flow being triggered.</span></span> <span data-ttu-id="c2b1f-257">Sie können den Ausführungsverlauf des Flows überprüfen, um zu sehen, ob er korrekt ausgeführt wurde. </span><span class="sxs-lookup"><span data-stu-id="c2b1f-257">You can check the Run History of the flow if it was executed correctly.</span></span> <span data-ttu-id="c2b1f-258">Da es etwas dauern kann, bis die PnP-Bereitstellungsvorlage angewendet wird, kann es sein, dass die Fußzeile nicht sofort angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-258">As it can take a bit before the PnP Provisioning Template has been applied, it can be that the footer does not show up immediately.</span></span> <span data-ttu-id="c2b1f-259">Warten Sie einen Moment, und laden Sie die Website erneut.</span><span class="sxs-lookup"><span data-stu-id="c2b1f-259">Give it a minute and reload your site to check again.</span></span>


