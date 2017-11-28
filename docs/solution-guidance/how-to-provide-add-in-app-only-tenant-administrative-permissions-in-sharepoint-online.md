---
title: Zum Bereitstellen von Add-in-app nur Mandanten Administratorberechtigungen in SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: a1d00ef42547116af8dfa569681566ac40cd97fc
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online"></a>Zum Bereitstellen von Add-in-app nur Mandanten Administratorberechtigungen in SharePoint Online
================================================

Wenn Sie SharePoint-Add-ins entwickeln und diese mit ACS-Modell ("appregnew.aspx" und "appinv.aspx") erfassen möchten, müssen Sie einen speziellen Prozess, folgen, wenn ein Add-in Mandanten Administratorberechtigungen aufgefordert wird und in nur-app-Modus. 

Schritte zum Mandanten Administratorberechtigung für die app nur-add-in bereitstellen:

- Registrieren von app-Id für das Add-in unter normalen Websitesammlung im Mandanten-Add-in dem bereitgestellt wird. 
  - URL: *https://[tenant].sharepoint.com/_layouts/15/appregnew.aspx*
- Geben Sie die erforderliche Informationen für die Registrierung-Add-in und registrieren Sie-ID und geheimen Schlüssel für das Add-in
- Wechseln Sie zur Seite "appinv.aspx", unter Ihrer Mandanten Admin-Website
  - URL: *https://[tenant]-admin.sharepoint.com/_layouts/15/appinv.aspx*
- Führen Sie eine Suche für die app-Id in der vorherigen Schritte auf der Seite "appinv.aspx" registriert
- Bereitstellen der erforderliche Berechtigungen für Ihre Add-in-Registrierung
- Führen Sie die Vertrauensstellung für die aktualisierte-add-in-Registrierung

Beachten Sie, dass diese Operation hat, unter die Mandantenverwaltungs-Website ausgeführt werden und für diese Vorgänge verwendete Konto Mandanten Administratorberechtigungen verfügen müssen. Wenn Sie niedriger Berechtigungsstufe für das add-in bereitstellen, können Sie die unter normalen Websitesammlungs-URLs mit niedrigeren Berechtigungen abschließen. 


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Registrieren von SharePoint-Add-Ins 2013](https://msdn.microsoft.com/en-us/library/office/jj687469.aspx)
    
- [Add-in-Berechtigungen in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp142383.aspx)

