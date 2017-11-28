---
title: "BCS und Secure Store Service-Konfiguration für einen SharePoint Multi-Geo-Mandanten"
ms.date: 11/03/2017
ms.openlocfilehash: 8059eeb117f2bc90c5221ee7a0d0168f8a97cc62
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="bcs-and-secure-store-service-configuration-for-a-sharepoint-multi-geo-tenant"></a>BCS und Secure Store Service-Konfiguration für einen SharePoint Multi-Geo-Mandanten 

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

Wenn Sie externe Daten wie Daten aus den anderen Geschäftsanwendungen oder Partnerressourcen in SharePoint Online verwenden möchten, können Sie Business Connectivity Services (BCS) zusammen mit der Secure Store Service. BCS unterstützt integrierte datenlösungen, um externe Daten in SharePoint zu bringen. Auf diese Weise können SharePoint zum interagieren mit Daten, die in ihrer Umgebung gehostet nicht zur Verfügung. BCS können externen Datenbanken, die Daten verfügbar über einen Webdienst Daten verbinden, die als einer OData-Quelle und anderen Arten von externen Daten veröffentlicht wird. 

Zum Verbinden mit externen Daten verwenden Sie BCS So richten Sie eine Verbindung mit der Zielanwendung und Secure Store Service die Anmeldeinformationen verwalten, die die externe Datenquelle erforderlich sind.

Ein Mandant SharePoint Multi-Geo verfügt über einen Standardspeicherort für geografisch und mindestens Satelliten-Speicherorte. Die Speicherorte der Satelliten haben eindeutige Domänenadressen, die diese Standorte Geo entsprechen. Jeder Standort Geo wird von den anderen, um sicherzustellen, dass Daten vor-Ort-logisch getrennt. Um für einen Mandanten Multi-Geo BCS konfigurieren möchten, erstellen Sie eine Verbindung zwischen der Datenquelle und verschiedenen SharePoint Geo Speicherorte, die mit externen Daten gefüllt werden soll. 

## <a name="see-also"></a>Siehe auch

- [Business Connectivity Services in SharePoint] (https://technet.microsoft.com/en-us/library/ee661740.aspx#section1 "Übersicht über Business Connectivity Services") 
- [Erstellen oder Bearbeiten einer Secure Store-Zielanwendung] (https://support.office.com/en-us/article/Create-or-edit-a-Secure-Store-Target-Application-F724DEC2-CE28-4B76-9235-31728DCE64B5#__toc346879710 "Erstellen oder Bearbeiten einer Secure Store-Zielanwendung") 



