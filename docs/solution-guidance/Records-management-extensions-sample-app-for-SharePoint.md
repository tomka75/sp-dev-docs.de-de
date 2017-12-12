---
title: "Records Management Extensions Beispiel-app für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: cfc4269c4510b5bb9207e45458affcd99a9a2eab
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="records-management-extensions-sample-app-for-sharepoint"></a>Records Management Extensions Beispiel-app für SharePoint

Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie aktivieren und für die direkte datensatzverwaltung für Ihre SharePoint-Websites und Listen ändern.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Die [ECM. RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) Beispiel zeigt, wie Sie eine vom Anbieter gehosteten SharePoint-app, um zu steuern, die für die direkte datensatzverwaltung für eine Website oder Liste.    

Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:

- Konfigurieren Sie für die direkte datensatzverwaltung während Ihrer benutzerdefinierten Site Bereitstellungsprozesses.
 
## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zunächst die [ECM. RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) Beispiel-app des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Bevor Sie diese app ausführen:

- Aktivieren Sie das In-Place-Datensatzverwaltung Feature in der Websitesammlung, wie in Abbildung 1 dargestellt.
    
    **Abbildung 1. Aktivieren von Compliance-Records Management in der Websitesammlung**

    ![Screenshot der Seite Websitefeatures für Websitesammlungen mit dem aktivierten In-Place-Eintrag Management Feature hervorgehoben.](media/d99269ae-b8fc-445b-a1b8-1612b16dcba6.png)

- In den websiteeinstellungen stellen Sie sicher, dass Sie **Datensatz Deklaration Einstellungen** in **Die Verwaltung von Websitesammlungen**, finden Sie unter wie in Abbildung 2 dargestellt.
    
    **Abbildung 2. Notieren Sie die Deklaration Einstellungen in den Websiteeinstellungen**

    ![Screenshot der Seite Websiteeinstellungen mit Datensatz Deklaration Einstellungen hervorgehoben.](media/13a6a490-68cd-4f70-8714-cd6222325890.png)

## <a name="using-the-ecmrecordsmanagement-sample-app"></a>Verwenden die ECM. RecordsManagement Beispiel-app
<a name="sectionSection1"> </a>

 Wenn Sie die app starten, zeigt die Startseite die zwei Szenarien, die verfügbar sind:

- Aktivieren der direkten datensatzverwaltung für Websites
    
- Aktivieren der direkten datensatzverwaltung für Listen

**Abbildung 3. ECM. RecordsManagement app-Startseite**

![Screenshot der app-Startseite, die zwei Szenarien mit.](media/a5fb2d86-2365-4d39-b41e-29719ab88287.png) 

Szenario 1 können Sie eine Benutzeroberfläche zum Steuern der für die datensatzverwaltung in Ihrer Websitesammlung erstellen. Die Benutzeroberfläche in diese app ähnelt der Benutzeroberfläche in **Deklaration für die Datensatzverwaltung** in den **Websiteeinstellungen** gefunden wurde (siehe Abbildung 2). Sie können auch aktivieren oder Deaktivieren des In-Place Records Management-Features in der Websitesammlung.

Szenario 2 können Sie um eine Benutzeroberfläche zum Steuern der für die datensatzverwaltung in Listen zu erstellen. Die Benutzeroberfläche in diese app ähnelt der Benutzeroberfläche in **Deklaration für die Datensatzverwaltung** in die bibliothekeinstellungen in der Liste gefunden.

**Abbildung 4. Notieren Sie Deklaration Einstellungen in einer Liste**

![Screenshot der Seite Bibliothekeinstellungen Datensatz-Methodendeklaration hinzu.](media/2522e4b0-5d5c-40bc-829d-f13d96a2b233.png)
### <a name="scenaro-1"></a>Scenaro 1

Szenario 1 behandelt Features zur in-Place-datensatzverwaltung und Einstellungen für Websites. Die app-Benutzeroberfläche enthält eine Schaltfläche **Deaktivieren** (oder **Aktivieren**), wie in Abbildung 5 dargestellt. Wenn Sie diese Schaltfläche deaktiviert (oder aktiviert) des In-Place Records Management-Features für die Websitesammlung. 

**Abbildung 5. Deaktivieren der Schaltfläche für das Feature In-Place-Datensatzverwaltung**

![Screenshot, der zeigt die deaktivieren oder aktivieren Sie die Schaltfläche für die direkte datensatzverwaltung.](media/b1a29cad-4239-4f49-a3e8-ca4e8ca99667.png)

Der folgende Code aktiviert oder deaktiviert das Feature In-Place-Datensatzverwaltung in der Websitesammlung. Die Methoden **DisableInPlaceRecordsManagementFeature** und **EnableSiteForInPlaceRecordsManagement** sind Teil der AppModelExtensions\RecordsManagementExtensions.cs-Datei in die [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).
    
> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

OfficeDevPnP.Core enthält Erweiterungsmethoden zum Abrufen und festlegen, dass alle auf Standortebene in-Place-Datensätze für das Management. Der folgende Code aus der **EnableSiteForInPlaceRecordsManagement** -Methode veranschaulicht, wie diese Erweiterungsmethoden Einschränkungen und angeben können, von wem deklarieren oder Deklarierung Datensätze auf Ihrer Website verwenden.

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

Wenn der Benutzer ihre für die in-Place-datensatzverwaltung ändert und die Schaltfläche **Speichern wählt** , führt der folgende Code in die **BtnSaveSiteScopedIPRSettings_Click** -Methode.

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

Im vorherigen Code wird die **SetRecordRestrictions** -Methode in RecordsManagementExtensions.cs aufgerufen. Die **SetRecordRestrictions** -Methode im nächsten Beispiel zeigt, wie Einschränkungen für Datensätze festgelegt.

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

### <a name="scenario-2"></a>Szenario 2

Szenario 2 zeigt, wie mit direkten Datensätzen Einstellungen für die Verwaltung für Listen interagieren. Wenn die app installiert wird, erstellt er eine Dokumentbibliothek namens IPRTest. Wenn Sie diese app zu ändern, und speichern Sie die für die direkte datensatzverwaltung verwenden, werden die Änderungen auf IPRTest angewendet. 

> [!NOTE] 
> Um für die in-Place-datensatzverwaltung auf eine Liste verwenden, müssen Sie die Compliance-Records Management-Funktion in Ihrer Websitesammlung aktivieren, wie in Abbildung 1 weiter oben in diesem Artikel dargestellt. 

Der folgende Code in Default.aspx.cs ausgeführt, wenn ein Benutzer auf die Schaltfläche " **Save Changes** " auswählt.

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

Der Code Ruft die folgenden beiden Methoden in der Datei RecordsManagementExtensions.cs OfficeDevPnP.Core:

-  **SetListManualRecordDeclaration** - definiert die manuelle Datensätze Deklaration Einstellung für diese Liste.
    
-  **SetListAutoRecordDeclaration** - automatisch Elemente in der Liste als Datensatz deklariert wird. Wenn Datensätze aus der Deklaration, automatisch in dieser Liste, die manuelle Datensätze Deklaration Einstellungen in der Liste festgelegt ist nicht mehr angewendet. Ereignisempfänger werden der Liste, um bestimmte Datensätze Management Aktionen starten beim Auftreten von Ereignissen hinzugefügt.

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

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [OfficeDevPnP.Core-Beispiel](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
