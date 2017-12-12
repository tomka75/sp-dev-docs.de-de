---
title: "Einführung in OneDrive und SharePoint Online Multi-Geo-Vorschau"
ms.date: 11/03/2017
ms.openlocfilehash: 1e13ce986e1ee84ce13dafb7bc8efad36b2c6348
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="introduction-to-onedrive-and-sharepoint-online-multi-geo-preview"></a>Einführung in OneDrive und SharePoint Online Multi-Geo-Vorschau

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

Die Multi-Geo OneDrive und SharePoint Online (ODSP) ermöglicht multinationale Unternehmen (MNCs), die Teil der Vorschau und haben einen oder mehrere geografische Standorten, erweitern ihre Office 365 ODSP-Instanz, um Daten vor-Ort-Anforderungen zu erfüllen.

In einer Konfiguration ODSP Multi-Geo Preview besteht aus Ihrem Office 365-Mandanten einen zentralen Speicherort (auch bekannt als Standardspeicherort) und einen oder mehrere Satelliten Geo-Speicherorte. Ein einzelner Mandant umfasst einen oder mehrere zusätzliche Geo-Speicherorte. Ihre Mandanten Informationen, einschließlich Geo-Standorten wird in Azure Active Directory (AAD) gespeichert.

> [!NOTE] 
> ODSP Multi-Geo Preview Features dienen nicht zum Optimieren der Leistung. Sie dienen Daten vor-Ort-Anforderungen erfüllen.

Im folgenden sind die wichtigsten Begriffe im Zusammenhang mit ODSP Multi-Geo-Vorschau:

- **Mandanten** – Darstellung von einer Organisation in Office 365, in der Regel mit einer oder mehreren Domänen. Beispielsweise "contoso.com".

- **Geo-Speicherort (oder Instanz)** – A Multi-Geo Mandanten mehrere Geo Speicherorte (oder Instanzen) zugeordnet werden kann. Ressourcen wie Postfächer oder Laufwerke können an diesen Speicherorten gespeichert werden. Contoso ist beispielsweise ein ODSP Multi-Geo Preview Mandanten mit drei Geo-Speicherorte: Name, EUR und APC.

- **Bevorzugte Daten Speicherort (Verteilerliste)** – eine-Eigenschaft, die vom Administrator AAD für den Benutzer oder eine Gruppe-Objekt, das Office 365-Dienste verwenden, um die entsprechenden Data-at-Rest-Ressourcen (Postfach, OneDrive, Gruppen Websites usw.) bereitzustellen.

Verwenden Sie Wenn Sie einen neue Anwendungen entwickeln, die in einem ODSP Multi-Geo Preview Mandanten arbeiten müssen oder Sie aktualisieren bestehenden Anwendungen Multi-Geo bewusst sein müssen, den Inhalt in der folgenden Tabelle, um mehr zu erfahren. 

|**Artikel**|**Beschreibung**|
|:-----|:-----|
|[Berechtigungsmodell](multigeo-permissions.md)|Beschreibt das zugrunde liegende Sicherheitsmodell in einem Multi-Geo-Mandanten.|
|[Entdecken Sie eine Multi-Geo-Konfiguration für einen SharePoint-Mandanten](multigeo-discovery.md)|Erläutert, wie die Erkennung von und Verstehen des Geo-Setups, einschließlich der standardmäßigen und Satelliten Geo Standorten.|
|[Access Onedrive for Business in einem Multi-Geo-Mandanten](multigeo-onedrive.md)|Beschreibt, wie Benutzer OneDrive für Unternehmen (ODB) Websites, auch bekannt als persönliche Websites oder Meine Websites, in der Serverfarm mit mehreren geografisch Mandanten entwickelt.|
|[Arbeiten Sie mit SharePoint-Websites in einer Serverfarm mit mehreren geografisch Mandanten](multigeo-sites.md)|Beschreibt das Arbeiten mit SharePoint-Websites über die standardmäßigen und Satelliten Geo Standorte Multi-Geo-Mandanten.|
|[Verwalten von Apps/Add-ins in einer Serverfarm mit mehreren geografisch Mandanten](multigeo-apps.md)|Erläutert die Auswirkungen der Bereitstellung und Verwaltung von SharePoint-Framework apps oder SharePoint-Add-in einer Multi-Geo-Mandanten.|
|[Multi-Geo Profil Benutzererlebnis](multigeo-userprofileexperience.md)|In einer Serverfarm mit mehreren geografisch Mandanten können Sie eine bevorzugte Datenspeicherort für einen Benutzer definieren, die in diesem Artikel erläutert wird. Wird außerdem erklärt, wie der Benutzer OneDrive Site finden und Lese-/Out-of-Box und benutzerdefinierten Benutzerprofileigenschaften aktualisieren.|
|[Suchen Sie in einer Serverfarm mit mehreren geografisch SharePoint Mandanten](multigeo-search.md)|Beschreibt die Funktionsweise der Suche in einer Serverfarm mit mehreren geografisch-Mandanten.|
|[Verwaltete Metadaten in einer Serverfarm mit mehreren geografisch Mandanten](multigeo-managedmetadata.md)|Erläutert, wie SharePoint verwalteten Metadaten in einer Umgebung mit mehreren geografisch nutzen.|
|[Inhaltstyphub in einem Multi-Geo-Mandanten](multigeo-contenttypehub.md)|Erläutert die Funktionsweise von dem inhaltstyphub in einem Multi-Geo-Mandanten.|
|[BCS und dem Secure Store in einer Serverfarm mit mehreren geografisch Mandanten](multigeo-bcsandsecurestore.md)|Beschreibt, wie Business Connectivity Services und Secure Store in einer Serverfarm mit mehreren geografisch-Mandanten verwenden.|




