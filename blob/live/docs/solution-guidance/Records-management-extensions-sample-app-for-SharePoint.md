---
title: "Records Management Extensions Beispiel-app für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 34184d4f1b7f2c75c7167d86cc1cf90e1a40323e
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="records-management-extensions-sample-app-for-sharepoint"></a><span data-ttu-id="be4e8-102">Records Management Extensions Beispiel-app für SharePoint</span><span class="sxs-lookup"><span data-stu-id="be4e8-102">Records management extensions sample app for SharePoint</span></span>

<span data-ttu-id="be4e8-103">Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie aktivieren und für die direkte datensatzverwaltung für Ihre SharePoint-Websites und Listen ändern.</span><span class="sxs-lookup"><span data-stu-id="be4e8-103">As part of your Enterprise Content Management (ECM) strategy, you can enable and change in-place records management settings on your SharePoint sites and lists.</span></span>

<span data-ttu-id="be4e8-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="be4e8-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="be4e8-105">Die [ECM. RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) Beispiel zeigt, wie Sie eine vom Anbieter gehosteten SharePoint-app, um zu steuern, die für die direkte datensatzverwaltung für eine Website oder Liste.</span><span class="sxs-lookup"><span data-stu-id="be4e8-105">The [ECM.RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) sample shows you how to use a provider-hosted SharePoint app to control the in-place records management settings for a site or list.</span></span>    

<span data-ttu-id="be4e8-106">Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:</span><span class="sxs-lookup"><span data-stu-id="be4e8-106">Use this solution if you want to:</span></span>

- <span data-ttu-id="be4e8-107">Konfigurieren Sie für die direkte datensatzverwaltung während Ihrer benutzerdefinierten Site Bereitstellungsprozesses.</span><span class="sxs-lookup"><span data-stu-id="be4e8-107">Configure in-place records management settings during your custom site provisioning process.</span></span>
 
## <a name="before-you-begin"></a><span data-ttu-id="be4e8-108">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="be4e8-108">Before you begin</span></span>
<span data-ttu-id="be4e8-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="be4e8-109"></span></span>

<span data-ttu-id="be4e8-110">Laden Sie Sie zunächst die [ECM. RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) Beispiel-app des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="be4e8-110">To get started, download the  [ECM.RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) sample app from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="be4e8-111">Bevor Sie diese app ausführen:</span><span class="sxs-lookup"><span data-stu-id="be4e8-111">Before you run this app:</span></span>

- <span data-ttu-id="be4e8-112">Aktivieren Sie das In-Place-Datensatzverwaltung Feature in der Websitesammlung, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="be4e8-112">Activate the In-Place Records Management feature on the site collection, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="be4e8-113">**Abbildung 1. Aktivieren von Compliance-Records Management in der Websitesammlung**</span><span class="sxs-lookup"><span data-stu-id="be4e8-113">**Figure 1. Activating In-Place Records Management on your site collection**</span></span>

    ![Screenshot der Seite Websitefeatures für Websitesammlungen mit dem aktivierten In-Place-Eintrag Management Feature hervorgehoben.](media/d99269ae-b8fc-445b-a1b8-1612b16dcba6.png)

- <span data-ttu-id="be4e8-115">In den websiteeinstellungen stellen Sie sicher, dass Sie **Datensatz Deklaration Einstellungen** in **Die Verwaltung von Websitesammlungen**, finden Sie unter wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="be4e8-115">In site settings, verify that you see  **Record declaration settings** in **Site Collection Administration**, as shown in Figure 2.</span></span>
    
    <span data-ttu-id="be4e8-116">**Abbildung 2. Notieren Sie die Deklaration Einstellungen in den Websiteeinstellungen**</span><span class="sxs-lookup"><span data-stu-id="be4e8-116">**Figure 2. Record declaration settings in Site Settings**</span></span>

    ![Screenshot der Seite Websiteeinstellungen mit Datensatz Deklaration Einstellungen hervorgehoben.](media/13a6a490-68cd-4f70-8714-cd6222325890.png)

## <a name="using-the-ecmrecordsmanagement-sample-app"></a><span data-ttu-id="be4e8-118">Verwenden die ECM. RecordsManagement Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="be4e8-118">Using the ECM.RecordsManagement sample app</span></span>
<span data-ttu-id="be4e8-119"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="be4e8-119"></span></span>

 <span data-ttu-id="be4e8-120">Wenn Sie die app starten, zeigt die Startseite die zwei Szenarien, die verfügbar sind:</span><span class="sxs-lookup"><span data-stu-id="be4e8-120">When you start the app, the start page displays the two scenarios that are available:</span></span>

- <span data-ttu-id="be4e8-121">Aktivieren der direkten datensatzverwaltung für Websites</span><span class="sxs-lookup"><span data-stu-id="be4e8-121">Enabling in-place records management for sites</span></span>
    
- <span data-ttu-id="be4e8-122">Aktivieren der direkten datensatzverwaltung für Listen</span><span class="sxs-lookup"><span data-stu-id="be4e8-122">Enabling in-place records management for lists</span></span>

<span data-ttu-id="be4e8-123">**Abbildung 3. ECM. RecordsManagement app-Startseite**</span><span class="sxs-lookup"><span data-stu-id="be4e8-123">**Figure 3. ECM.RecordsManagement app start page**</span></span>

![Screenshot der app-Startseite, die zwei Szenarien mit.](media/a5fb2d86-2365-4d39-b41e-29719ab88287.png) 

<span data-ttu-id="be4e8-125">Szenario 1 können Sie eine Benutzeroberfläche zum Steuern der für die datensatzverwaltung in Ihrer Websitesammlung erstellen.</span><span class="sxs-lookup"><span data-stu-id="be4e8-125">You can use scenario 1 to build a UI to control the records management settings on your site collection.</span></span> <span data-ttu-id="be4e8-126">Die Benutzeroberfläche in diese app ähnelt der Benutzeroberfläche in **Deklaration für die Datensatzverwaltung** in den **Websiteeinstellungen** gefunden wurde (siehe Abbildung 2).</span><span class="sxs-lookup"><span data-stu-id="be4e8-126">The UI in this app is similar to the UI found in **Records declaration settings** in **Site Settings** (see Figure 2).</span></span> <span data-ttu-id="be4e8-127">Sie können auch aktivieren oder Deaktivieren des In-Place Records Management-Features in der Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="be4e8-127">You can also activate or deactivate the In-Place Records Management feature on your site collection.</span></span>

<span data-ttu-id="be4e8-128">Szenario 2 können Sie um eine Benutzeroberfläche zum Steuern der für die datensatzverwaltung in Listen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="be4e8-128">You can use Scenario 2 to build a UI to control the records management settings on lists.</span></span> <span data-ttu-id="be4e8-129">Die Benutzeroberfläche in diese app ähnelt der Benutzeroberfläche in **Deklaration für die Datensatzverwaltung** in die bibliothekeinstellungen in der Liste gefunden.</span><span class="sxs-lookup"><span data-stu-id="be4e8-129">The UI in this app is similar to the UI found in  **Records declaration settings** in the library settings on your list.</span></span>

<span data-ttu-id="be4e8-130">**Abbildung 4. Notieren Sie Deklaration Einstellungen in einer Liste**</span><span class="sxs-lookup"><span data-stu-id="be4e8-130">**Figure 4. Record declaration settings on a list**</span></span>

![Screenshot der Seite Bibliothekeinstellungen Datensatz-Methodendeklaration hinzu.](media/2522e4b0-5d5c-40bc-829d-f13d96a2b233.png)
### <a name="scenaro-1"></a><span data-ttu-id="be4e8-132">Scenaro 1</span><span class="sxs-lookup"><span data-stu-id="be4e8-132">Scenaro 1</span></span>

<span data-ttu-id="be4e8-133">Szenario 1 behandelt Features zur in-Place-datensatzverwaltung und Einstellungen für Websites.</span><span class="sxs-lookup"><span data-stu-id="be4e8-133">Scenario 1 addresses in-place records management features and settings for sites.</span></span> <span data-ttu-id="be4e8-134">Die app-Benutzeroberfläche enthält eine Schaltfläche **Deaktivieren** (oder **Aktivieren**), wie in Abbildung 5 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="be4e8-134">The app UI includes a  **Deactivate** (or **Activate**) button, as shown in Figure 5.</span></span> <span data-ttu-id="be4e8-135">Wenn Sie diese Schaltfläche deaktiviert (oder aktiviert) des In-Place Records Management-Features für die Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="be4e8-135">Choosing this button deactivates (or activates) the In-Place Records Management feature on the site collection.</span></span> 

<span data-ttu-id="be4e8-136">**Abbildung 5. Deaktivieren der Schaltfläche für das Feature In-Place-Datensatzverwaltung**</span><span class="sxs-lookup"><span data-stu-id="be4e8-136">**Figure 5. Deactivate button for the In-Place Records Management feature**</span></span>

![Screenshot, der zeigt die deaktivieren oder aktivieren Sie die Schaltfläche für die direkte datensatzverwaltung.](media/b1a29cad-4239-4f49-a3e8-ca4e8ca99667.png)

<span data-ttu-id="be4e8-138">Der folgende Code aktiviert oder deaktiviert das Feature In-Place-Datensatzverwaltung in der Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="be4e8-138">The following code activates or deactivates the In-Place Records Management feature on the site collection.</span></span> <span data-ttu-id="be4e8-139">Die Methoden **DisableInPlaceRecordsManagementFeature** und **EnableSiteForInPlaceRecordsManagement** sind Teil der AppModelExtensions\RecordsManagementExtensions.cs-Datei in die [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).</span><span class="sxs-lookup"><span data-stu-id="be4e8-139">The  **DisableInPlaceRecordsManagementFeature** and **EnableSiteForInPlaceRecordsManagement** methods are part of the AppModelExtensions\RecordsManagementExtensions.cs file in the [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).</span></span>
    
<span data-ttu-id="be4e8-140">**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="be4e8-140">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
protected void btnToggleIPRStatus_Click(object sender, EventArgs e)
        {
            if (cc.Site.IsInPlaceRecordsManagementActive())
            {
                cc.Site.DisableInPlaceRecordsManagementFeature();
                IPRStatusUpdate(false);
            }
            else
            {
                cc.Site.EnableSiteForInPlaceRecordsManagement();
                IPRStatusUpdate(true);
            }
        }
```

<span data-ttu-id="be4e8-141">OfficeDevPnP.Core enthält Erweiterungsmethoden zum Abrufen und festlegen, dass alle auf Standortebene in-Place-Datensätze für das Management.</span><span class="sxs-lookup"><span data-stu-id="be4e8-141">OfficeDevPnP.Core includes extension methods to get and set all site-scoped in-place records management settings.</span></span> <span data-ttu-id="be4e8-142">Der folgende Code aus der **EnableSiteForInPlaceRecordsManagement** -Methode veranschaulicht, wie diese Erweiterungsmethoden Einschränkungen und angeben können, von wem deklarieren oder Deklarierung Datensätze auf Ihrer Website verwenden.</span><span class="sxs-lookup"><span data-stu-id="be4e8-142">The following code from the  **EnableSiteForInPlaceRecordsManagement** method shows how to use these extension methods to set restrictions, and specify who can declare or undeclare records on your site.</span></span>

```C#
public static void EnableSiteForInPlaceRecordsManagement(this Site site)
        {
            // Activate the In-Place Records Management feature if not yet enabled.
            if (!site.IsFeatureActive(new Guid(INPLACE_RECORDS_MANAGEMENT_FEATURE_ID)))
            {
                // Note: this also sets the ECM_SITE_RECORD_RESTRICTIONS value to "BlockDelete, BlockEdit".
                site.ActivateInPlaceRecordsManagementFeature();
            }

            // Enable in-place records management in all locations.
            site.SetManualRecordDeclarationInAllLocations(true);

            // Set restrictions to default values after enablement (this is also done at feature activation).
            EcmSiteRecordRestrictions restrictions = EcmSiteRecordRestrictions.BlockDelete | EcmSiteRecordRestrictions.BlockEdit;
            site.SetRecordRestrictions(restrictions);

            // Set record declaration to default value.
            site.SetRecordDeclarationBy(EcmRecordDeclarationBy.AllListContributors);

            // Set record undeclaration to default value.
            site.SetRecordUnDeclarationBy(EcmRecordDeclarationBy.OnlyAdmins);

        }
```

<span data-ttu-id="be4e8-143">Wenn der Benutzer ihre für die in-Place-datensatzverwaltung ändert und die Schaltfläche **Speichern wählt** , führt der folgende Code in die **BtnSaveSiteScopedIPRSettings_Click** -Methode.</span><span class="sxs-lookup"><span data-stu-id="be4e8-143">When the user changes their in-place records management settings and chooses the  **Save changes** button, the following code in the **btnSaveSiteScopedIPRSettings_Click** method runs.</span></span>

```C#
protected void btnSaveSiteScopedIPRSettings_Click(object sender, EventArgs e)
        {
            EcmSiteRecordRestrictions restrictions = (EcmSiteRecordRestrictions)Convert.ToInt32(rdRestrictions.SelectedValue);
            cc.Site.SetRecordRestrictions(restrictions);
            cc.Site.SetManualRecordDeclarationInAllLocations(Convert.ToBoolean(rdAvailability.SelectedValue));
            EcmRecordDeclarationBy declareBy = (EcmRecordDeclarationBy)Convert.ToInt32(rdDeclarationBy.SelectedValue);
            cc.Site.SetRecordDeclarationBy(declareBy);
            EcmRecordDeclarationBy unDeclareBy = (EcmRecordDeclarationBy)Convert.ToInt32(rdUndeclarationBy.SelectedValue);
            cc.Site.SetRecordUnDeclarationBy(unDeclareBy);
        }
```

<span data-ttu-id="be4e8-144">Im vorherigen Code wird die **SetRecordRestrictions** -Methode in RecordsManagementExtensions.cs aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="be4e8-144">In the previous code, a call is made to the  **SetRecordRestrictions** method in RecordsManagementExtensions.cs.</span></span> <span data-ttu-id="be4e8-145">Die **SetRecordRestrictions** -Methode im nächsten Beispiel zeigt, wie Einschränkungen für Datensätze festgelegt.</span><span class="sxs-lookup"><span data-stu-id="be4e8-145">The **SetRecordRestrictions** method in the next example shows how to set restrictions on the records.</span></span>

```C#
public static void SetRecordRestrictions(this Site site, EcmSiteRecordRestrictions restrictions)
        {
            string restrictionsProperty = "";

            if (restrictions.Has(EcmSiteRecordRestrictions.None))
            {
                restrictionsProperty = EcmSiteRecordRestrictions.None.ToString();
            }
            else if (restrictions.Has(EcmSiteRecordRestrictions.BlockEdit))
            {
                // BlockEdit is always used in conjunction with BlockDelete.
                restrictionsProperty = EcmSiteRecordRestrictions.BlockDelete.ToString() + ", " + EcmSiteRecordRestrictions.BlockEdit.ToString();
            }
            else if (restrictions.Has(EcmSiteRecordRestrictions.BlockDelete))
            {
                restrictionsProperty = EcmSiteRecordRestrictions.BlockDelete.ToString();
            }

            // Set property bag entry.
            site.RootWeb.SetPropertyBagValue(ECM_SITE_RECORD_RESTRICTIONS, restrictionsProperty);
        }
```

### <a name="scenario-2"></a><span data-ttu-id="be4e8-146">Szenario 2</span><span class="sxs-lookup"><span data-stu-id="be4e8-146">Scenario 2</span></span>

<span data-ttu-id="be4e8-147">Szenario 2 zeigt, wie mit direkten Datensätzen Einstellungen für die Verwaltung für Listen interagieren.</span><span class="sxs-lookup"><span data-stu-id="be4e8-147">Scenario 2 shows how to interact with in-place records management settings for lists.</span></span> <span data-ttu-id="be4e8-148">Wenn die app installiert wird, erstellt er eine Dokumentbibliothek namens IPRTest.</span><span class="sxs-lookup"><span data-stu-id="be4e8-148">When the app installs, it creates a document library called IPRTest.</span></span> <span data-ttu-id="be4e8-149">Wenn Sie diese app zu ändern, und speichern Sie die für die direkte datensatzverwaltung verwenden, werden die Änderungen auf IPRTest angewendet.</span><span class="sxs-lookup"><span data-stu-id="be4e8-149">When you use this app to change and save the in-place records management settings, the changes are applied to IPRTest.</span></span> 

<span data-ttu-id="be4e8-150">**Hinweis**  Um für die in-Place-datensatzverwaltung auf eine Liste verwenden, müssen Sie die Compliance-Records Management-Funktion in Ihrer Websitesammlung aktivieren, wie in Abbildung 1 weiter oben in diesem Artikel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="be4e8-150">**Note**  To use in-place records management settings on a list, you must activate the In-place Records Management feature on your site collection, as shown in Figure 1 earlier in this article.</span></span> 

<span data-ttu-id="be4e8-151">Der folgende Code in Default.aspx.cs ausgeführt, wenn ein Benutzer auf die Schaltfläche " **Save Changes** " auswählt.</span><span class="sxs-lookup"><span data-stu-id="be4e8-151">The following code in Default.aspx.cs runs when a user chooses the  **Save Changes** button.</span></span>

```C#
protected void btnSaveListScopedIPRSettings_Click(object sender, EventArgs e)
        {
            List ipr = cc.Web.GetListByTitle(IPR_LIBRARY);
            EcmListManualRecordDeclaration listManual = (EcmListManualRecordDeclaration)Convert.ToInt32(rdListAvailability.SelectedValue);
            ipr.SetListManualRecordDeclaration(listManual);
            ipr.SetListAutoRecordDeclaration(chbAutoDeclare.Checked);

            // Refresh the settings as AutoDeclare changes the manual settings.
            if (ipr.IsListRecordSettingDefined())
            {
                rdListAvailability.SelectedValue = Convert.ToString((int)ipr.GetListManualRecordDeclaration());
                chbAutoDeclare.Checked = ipr.GetListAutoRecordDeclaration();
                rdListAvailability.Enabled = !chbAutoDeclare.Checked;
            }

        }
```

<span data-ttu-id="be4e8-152">Der Code Ruft die folgenden beiden Methoden in der Datei RecordsManagementExtensions.cs OfficeDevPnP.Core:</span><span class="sxs-lookup"><span data-stu-id="be4e8-152">The code calls the following two methods in the RecordsManagementExtensions.cs file of OfficeDevPnP.Core:</span></span>

-  <span data-ttu-id="be4e8-153">**SetListManualRecordDeclaration** - definiert die manuelle Datensätze Deklaration Einstellung für diese Liste.</span><span class="sxs-lookup"><span data-stu-id="be4e8-153">**SetListManualRecordDeclaration** - Defines the manual records declaration setting for this list.</span></span>
    
-  <span data-ttu-id="be4e8-154">**SetListAutoRecordDeclaration** - automatisch Elemente in der Liste als Datensatz deklariert wird.</span><span class="sxs-lookup"><span data-stu-id="be4e8-154">**SetListAutoRecordDeclaration** - Automatically declares items added to this list as a record.</span></span> <span data-ttu-id="be4e8-155">Wenn Datensätze aus der Deklaration, automatisch in dieser Liste, die manuelle Datensätze Deklaration Einstellungen in der Liste festgelegt ist nicht mehr angewendet.</span><span class="sxs-lookup"><span data-stu-id="be4e8-155">If records declaration is set to automatic on this list, the manual records declaration settings on the list no longer apply.</span></span> <span data-ttu-id="be4e8-156">Ereignisempfänger werden der Liste, um bestimmte Datensätze Management Aktionen starten beim Auftreten von Ereignissen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="be4e8-156">Event receivers are added to the list to start specific records management actions when events occur.</span></span>

```C#
public static void SetListManualRecordDeclaration(this List list, EcmListManualRecordDeclaration settings)
        {
            if (settings == EcmListManualRecordDeclaration.UseSiteCollectionDefaults)
            {
                // If you set list record declaration back to the default values, you also need to 
                // turn off auto record declaration. Other property bag values are left as is; when 
                // settings are changed again these properties are also again usable.
                if (list.PropertyBagContainsKey(ECM_AUTO_DECLARE_RECORDS))
                {
                    list.SetListAutoRecordDeclaration(false);
                }
                // Set the property that dictates custom list record settings to false.
                list.SetPropertyBagValue(ECM_IPR_LIST_USE_LIST_SPECIFIC, false.ToString());
            }
            else if (settings == EcmListManualRecordDeclaration.AlwaysAllowManualDeclaration)
            {
                list.SetPropertyBagValue(ECM_ALLOW_MANUAL_DECLARATION, true.ToString());
                // Set the property that dictates custom list record settings to true.
                list.SetPropertyBagValue(ECM_IPR_LIST_USE_LIST_SPECIFIC, true.ToString());
            } 
            else if (settings == EcmListManualRecordDeclaration.NeverAllowManualDeclaration)
            {
                list.SetPropertyBagValue(ECM_ALLOW_MANUAL_DECLARATION, false.ToString());
                // Set the property that dictates custom list record settings to true.
                list.SetPropertyBagValue(ECM_IPR_LIST_USE_LIST_SPECIFIC, true.ToString());
            }
            else
            {
                throw new ArgumentOutOfRangeException("settings");
            }
        }

public static void SetListAutoRecordDeclaration(this List list, bool autoDeclareRecords)
        {
            // Determine the SharePoint version based on the loaded CSOM library.
            Assembly asm = Assembly.GetAssembly(typeof(Microsoft.SharePoint.Client.Site));
            int sharePointVersion = asm.GetName().Version.Major;

            if (autoDeclareRecords)
            {
                // Set the property that dictates custom list record settings to true.
                list.SetPropertyBagValue(ECM_IPR_LIST_USE_LIST_SPECIFIC, true.ToString());
                // Prevent manual declaration.
                list.SetPropertyBagValue(ECM_ALLOW_MANUAL_DECLARATION, false.ToString());

                // Hook up the needed event handlers.
                list.Context.Load(list.EventReceivers);
                list.Context.ExecuteQuery();

                List<EventReceiverDefinition> currentEventReceivers = new List<EventReceiverDefinition>(list.EventReceivers.Count);
                currentEventReceivers.AddRange(list.EventReceivers);

                // Track changes to see if a list.Update is needed.
                bool eventReceiverAdded = false;
                
                // ItemUpdating receiver.
                EventReceiverDefinitionCreationInformation newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemUpdating, 1000, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemDeleting receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemDeleting, 1000, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemFileMoving receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemFileMoving, 1000, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemAdded receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemAdded, 1005, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemUpdated receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemUpdated, 1007, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemCheckedIn receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemCheckedIn, 1006, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                                
                if (eventReceiverAdded)
                {
                    list.Update();
                    list.Context.ExecuteQuery();
                }

                // Set the property that dictates the autodeclaration.
                list.SetPropertyBagValue(ECM_AUTO_DECLARE_RECORDS, autoDeclareRecords.ToString());
            }
            else
            {
                // Set the property that dictates the autodeclaration.
                list.SetPropertyBagValue(ECM_AUTO_DECLARE_RECORDS, autoDeclareRecords.ToString());
                //Note: Existing list event handlers will just stay as they are, no need to remove them.
            }
        }
```

## <a name="additional-resources"></a><span data-ttu-id="be4e8-157">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="be4e8-157">Additional resources</span></span>
<span data-ttu-id="be4e8-158"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="be4e8-158"></span></span>

-  [<span data-ttu-id="be4e8-159">Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="be4e8-159">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="be4e8-160">OfficeDevPnP.Core-Beispiel</span><span class="sxs-lookup"><span data-stu-id="be4e8-160">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
