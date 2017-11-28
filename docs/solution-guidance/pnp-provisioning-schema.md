---
title: Plug & Play-Bereitstellung schema
ms.date: 11/03/2017
ms.openlocfilehash: acc16112e79972db74f97d50e20c1b0f1f0bb4f6
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="pnp-provisioning-schema"></a>Plug & Play-Bereitstellung schema

Wie Sie in unseren [Plug & Play-Bereitstellung Framework](pnp-provisioning-framework.md) und an anderer Stelle haben, hat das Format für die Bereitstellung von Vorlagen aus der Speicherformat abgekoppelt werden, damit Sie eine beliebige Format verwenden können, die Sie bevorzugen. Trotzdem, da mit der Bereitstellung XML-Schema für beibehalten von Vorlagen allgemeine dies der Fall ist, sind wir bereit einige zusätzliche Informationen zur Verwendung des XML-Schemas zum Serialisieren und speichern Sie Ihre Bereitstellung Vorlagen.

**Wichtig:** Während das Bereitstellung Schema offensichtlich XML-Serialisierung der Bereitstellung Vorlagen unterstützt, werden auch die Struktur für die Serialisierung im JSON-Format enthält. Im Allgemeinen stellt das Schema für die Bereitstellung Strukturen definieren.

## <a name="provisioning-schema-resources"></a>Bereitstellen von Schema Ressourcen

Sie erhalten das Bereitstellung Schema zusammen mit den unterstützenden Dateien, auf GitHub: [PnP-Provisioning-Schema](https://github.com/SharePoint/PnP-Provisioning-Schema)

Es wird eine 20 Minuten Channel 9-Video, die das Schema Bereitstellung erläutert: [Betrachtung der Sequenzierung auf PnP provisioning Engine Schema](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema).

Beispiel-Schemas auf verfügbar sind: [GitHub am PnP-Provisioning-Schema/Beispiele](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples).

Der Codeabschnitt darunter werden das Schemastammelement und direkte untergeordnete Elemente des Stammverzeichnisses angezeigt. Bereitstellung Schemadokumentation finden Sie unter GitHub: [Plug & Play-Bereitstellung Schema](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md).

```
<pnp:ProvisioningTemplate
           xmlns:pnp="http://schemas.dev.office.com/PnP/2015/08/ProvisioningSchema"
           ID="xsd:ID"
           Version="xsd:decimal"
           ImagePreviewUrl="xsd:string"
           DisplayName="xsd:string"
           Description="xsd:string">
   <pnp:Properties />
   <pnp:SitePolicy />
   <pnp:RegionalSettings />
   <pnp:SupportedUILanguages />
   <pnp:AuditSettings />
   <pnp:PropertyBagEntries />
   <pnp:Security />
   <pnp:SiteFields />
   <pnp:ContentTypes />
   <pnp:Lists />
   <pnp:Features />
   <pnp:CustomActions />
   <pnp:Files />
   <pnp:Pages />
   <pnp:TermGroups />
   <pnp:ComposedLook />
   <pnp:Workflows />
   <pnp:SearchSettings />
   <pnp:Publishing />
   <pnp:AddIns />
   <pnp:Providers />
</pnp:ProvisioningTemplate>
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Betrachtung der Sequenzierung Plug & Play-Bereitstellung Engine-Schema](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)
    
- [Plug & Play-Bereitstellung Schema](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md)
    
- [GitHub am PnP-Provisioning-Schema/Beispiele (engl.)](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples)
