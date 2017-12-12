---
title: "Informationen Management Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c5e81e55cff89d6bf311c3fb6c7f40e0b0c87ee9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="information-management-sample-add-in-for-sharepoint"></a>Informationen Management Beispiel-add-in für SharePoint
Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie abrufen oder Festlegen von Richtlinien für Website zum Verwalten des Lebenszyklus der SharePoint-Website.
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Das [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) -Beispiel zeigt, wie Sie ein ASP.NET vom Anbieter gehosteten SharePoint-add-in zum Abrufen und Festlegen von Standortrichtlinien auf einer Website. Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:

- Anwenden von Richtlinieneinstellungen während Ihrer benutzerdefinierten Site Bereitstellungsprozesses. 
    
- Erstellen Sie eines neuen oder ändern Sie einer vorhandenen Website.
    
- Erstellen einer benutzerdefinierten ablaufformel. 
    
## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Es wird empfohlen, dass Sie mindestens eine Standortrichtlinie zu erstellen, und weisen Sie es zu Ihrer Website, bevor Sie dieses Add-in ausführen. Andernfalls wird das Add-In gestartet ohne Beispieldaten. Weitere Informationen finden Sie unter [Übersicht über websiterichtlinien in SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).

## <a name="using-the-coreinformationmanagement-sample-app"></a>Verwenden die Core.InformationManagement Beispiel-app
<a name="sectionSection1"> </a>

Wenn Sie die app starten, wird die Startseite die folgende Informationen angezeigt, wie in Abbildung 1 dargestellt:

- Die Website schließen und Ablauf Datumsangaben. Diese Daten sind spezifisch für eine Website und basieren auf die Konfigurationseinstellungen der Website-Richtlinie, die angewendet wird.
    
- Alle websiterichtlinien, die auf der Website angewendet werden können.
    
- Die Website-Richtlinie, die momentan angewendet werden.
    
- Die Option Feld auswählen und Zuweisen einer neuen Standortrichtlinie für die Website.

**Abbildung 1. Informationen Management Add-in-Startseite**

![Screenshot der Startseite-Add-in mit Website-Richtlinie zum Abschluss und Ablauf Werte, verfügbar und angewendeten Standortrichtlinien und andere Richtlinien hervorgehobenen anwenden.](media/8c5f39f7-700d-4300-bcc4-9ed9edf0e155.png)

Aus der SharePoint-Website können Sie Gehe zu der Anwendung, der auf dem Remotehost ausgeführt wird, indem Sie auf **zuletzt verwendet** > **Core.InformationManagement**. Um zu Ihrer SharePoint-Website zurückzukehren, wählen Sie **zurück zur Website**.

Die Datei Pages\Default.aspx.cs im Projekt Core.InformationManagementWeb enthält den Code für die Seite, die in Abbildung 1 angezeigt. 

Der folgende Code in der **Page_Load** -Methode der Seite "default.aspx.cs" abruft und die Daten zum Abschluss und Ablauf der Website, basierend auf der Website angewendete Richtlinie angezeigt. Dieser Code Ruft die Erweiterungsmethoden **GetSiteExpirationDate** und **GetSiteCloseDate** des Projekts OfficeDevPnP.Core.
    
> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
// Get site expiration and closure dates.
if (cc.Web.HasSitePolicyApplied())
{
        lblSiteExpiration.Text = String.Format("The expiration date for the site is {0}", cc.Web.GetSiteExpirationDate());
        lblSiteClosure.Text = String.Format("The closure date for the site is {0}", cc.Web.GetSiteCloseDate());
}

```

Der folgende Code in der **Page_Load** -Methode der Seite "default.aspx.cs" zeigt die Namen aller Website-Richtlinien, die auf der Website (einschließlich der derzeit angewendete Standortrichtlinie) angewendet werden können. Dieser Code Ruft die Erweiterungsmethode **GetSitePolicies** des Projekts OfficeDevPnP.Core.

```C#
// List the defined policies.
List<SitePolicyEntity> policies = cc.Web.GetSitePolicies();
string policiesString = "";
foreach (var policy in policies)
                    {
                        policiesString += String.Format("{0} ({1}) <BR />", policy.Name, policy.Description);
                    }
lblSitePolicies.Text = policiesString;
            };

```

Der folgende Code in der **Page_Load** -Methode der Seite "default.aspx.cs" zeigt den Namen der Website-Richtlinie, die derzeit auf der Website angewendet. Dadurch wird die **GetAppliedSitePolicy** -Erweiterungsmethode des Projekts OfficeDevPnP.Core aufgerufen.

```C#
// Show the assigned policy.
SitePolicyEntity appliedPolicy = cc.Web.GetAppliedSitePolicy();
if (appliedPolicy != null)
            {
            lblAppliedPolicy.Text = String.Format("{0} ({1})", appliedPolicy.Name, appliedPolicy.Description);
            }
else
            {
            lblAppliedPolicy.Text = "No policy has been applied";
            }

```

Der folgende Code in der **Page_Load** -Methode der Seite "default.aspx.cs" füllt die Dropdown-Liste mit den websiterichtlinien, die mit Ausnahme der Standortrichtlinie verfügbar sind, die der Website zugewiesen ist.

```C#
// Fill the policies combo.
foreach (var policy in policies)
{
if (appliedPolicy == null || !policy.Name.Equals(appliedPolicy.Name, StringComparison.InvariantCultureIgnoreCase))
{
                            drlPolicies.Items.Add(policy.Name);
           }
}
btnApplyPolicy.Enabled = drlPolicies.Items.Count > 0;

```

Der folgende Code in der Seite "default.aspx.cs" gilt die ausgewählte Standortrichtlinie für die Website. Die ursprüngliche Website Richtlinie wird durch die neue Standortrichtlinie ersetzt. 

```C#
protected void btnApplyPolicy_Click(object sender, EventArgs e)
{
if (drlPolicies.SelectedItem != null)
            {
                cc.Web.ApplySitePolicy(drlPolicies.SelectedItem.Text);
                Page.Response.Redirect(Page.Request.Url.ToString(), true);
            }
}

```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [OfficeDevPnP.Core-Beispiel](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
-  [Core.SiteClassification-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SiteClassification)
    
-  [ECM. AutoTagging Beispiel-app](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging)
    
-  [ECM. DocumentLibraries Beispiel-app](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
    
-  [ECM. RecordsManagement Beispiel-app](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement)
