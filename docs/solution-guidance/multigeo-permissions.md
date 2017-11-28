---
title: Berechtigungsmodell in OneDrive und SharePoint Online Multi-Geo-Vorschau
ms.date: 11/03/2017
ms.openlocfilehash: 3f0d47ce0f791dd41dce8ca95e877e2e64a35c06
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="permission-model-in-onedrive-and-sharepoint-online-multi-geo-preview"></a>Berechtigungsmodell in OneDrive und SharePoint Online Multi-Geo-Vorschau

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

Das Berechtigungsmodell in einem Mandanten OneDrive und SharePoint Online mit mehreren geografisch Preview ist identisch mit der für einen einzelnen Geo-Mandanten.

Ein Mandant Multi-Geo weist eine einzige Azure AD-Umgebung auf allen Speicherorten für alle geografisch verteilt. Diese Azure AD-Umgebung umfasst: 

- Alle Benutzer und Gruppen - gelten, wenn Sie einen Benutzer oder Gruppenberechtigungen erteilen diese Berechtigungen an alle Geo-Speicherorte.
- Alle Sicherheitsprinzipale -, ob Sie die Anwendung im Azure Active Directory mithilfe eines der Azure-Portale registrieren oder über Azure Access Control Services (in SharePoint "appregnew.aspx"), die Berechtigungen für alle Geo-Speicherorte gelten.

Die folgende Abbildung zeigt einen Multi-Geo-Mandanten mit:

- Einen Standardspeicherort Geo in Nordamerika
- Einen Satelliten Geo Speicherort in Europa
- Einen Satelliten Geo Speicherort in Asien

Diesen Mandanten verfügt über eine verteilte Azure Active Directory (AD Azure)-Umgebung, die allen Benutzern, Gruppen und Berechtigungen enthält. Die wichtigsten Azure AD-Instanz an alle Speicherorte geografisch verteilt ist. 

![Eine Karte zur Erläuterung von eines Standardspeicherorts für geografisch in Nordamerika und Satelliten Geo Speicherorte in Europa und Asien, mit Benutzerkonten und Gruppen in AAD gespeichert world](media/multigeo/multigeopermissions_intro.png)

Zum Konfigurieren von Anwendungen für Multi-Geo Mandanten in Azure AD finden Sie unter [Einrichten einer Serverfarm mit mehreren geografisch beispielanwendung](multigeo-sampleapplicationsetup.md).

