---
title: Plug & Play-Bereitstellung schema
ms.date: 11/03/2017
ms.openlocfilehash: acc16112e79972db74f97d50e20c1b0f1f0bb4f6
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="pnp-provisioning-schema"></a><span data-ttu-id="9ff9c-102">Plug & Play-Bereitstellung schema</span><span class="sxs-lookup"><span data-stu-id="9ff9c-102">PnP provisioning schema</span></span>

<span data-ttu-id="9ff9c-103">Wie Sie in unseren [Plug & Play-Bereitstellung Framework](pnp-provisioning-framework.md) und an anderer Stelle haben, hat das Format für die Bereitstellung von Vorlagen aus der Speicherformat abgekoppelt werden, damit Sie eine beliebige Format verwenden können, die Sie bevorzugen.</span><span class="sxs-lookup"><span data-stu-id="9ff9c-103">As you learned in our [PnP provisioning framework](pnp-provisioning-framework.md) and elsewhere, the format for provisioning templates has been decoupled from the persistence format so that you can use any format you prefer.</span></span> <span data-ttu-id="9ff9c-104">Trotzdem, da mit der Bereitstellung XML-Schema für beibehalten von Vorlagen allgemeine dies der Fall ist, sind wir bereit einige zusätzliche Informationen zur Verwendung des XML-Schemas zum Serialisieren und speichern Sie Ihre Bereitstellung Vorlagen.</span><span class="sxs-lookup"><span data-stu-id="9ff9c-104">Nevertheless, because using the XML provisioning schema for persisting templates is such a common scenario, we're providing some additional information about how to use the XML schema to serialize and save your provisioning templates.</span></span>

<span data-ttu-id="9ff9c-105">**Wichtig:** Während das Bereitstellung Schema offensichtlich XML-Serialisierung der Bereitstellung Vorlagen unterstützt, werden auch die Struktur für die Serialisierung im JSON-Format enthält.</span><span class="sxs-lookup"><span data-stu-id="9ff9c-105">**Important:** While the provisioning schema obviously supports XML serialization of provisioning templates, it also provides the structure for serialization in JSON format.</span></span> <span data-ttu-id="9ff9c-106">Im Allgemeinen stellt das Schema für die Bereitstellung Strukturen definieren.</span><span class="sxs-lookup"><span data-stu-id="9ff9c-106">More generally, the schema provides the model for defining provisioning structures.</span></span>

## <a name="provisioning-schema-resources"></a><span data-ttu-id="9ff9c-107">Bereitstellen von Schema Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9ff9c-107">Provisioning schema resources</span></span>

<span data-ttu-id="9ff9c-108">Sie erhalten das Bereitstellung Schema zusammen mit den unterstützenden Dateien, auf GitHub: [PnP-Provisioning-Schema](https://github.com/SharePoint/PnP-Provisioning-Schema)</span><span class="sxs-lookup"><span data-stu-id="9ff9c-108">You can get the provisioning schema, along with its supporting files, on GitHub: [PnP-Provisioning-Schema](https://github.com/SharePoint/PnP-Provisioning-Schema)</span></span>

<span data-ttu-id="9ff9c-109">Es wird eine 20 Minuten Channel 9-Video, die das Schema Bereitstellung erläutert: [Betrachtung der Sequenzierung auf PnP provisioning Engine Schema](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema).</span><span class="sxs-lookup"><span data-stu-id="9ff9c-109">There is a 20-minute Channel 9 video that discusses the provisioning schema: [Deep dive to PnP provisioning engine schema](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema).</span></span>

<span data-ttu-id="9ff9c-110">Beispiel-Schemas auf verfügbar sind: [GitHub am PnP-Provisioning-Schema/Beispiele](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="9ff9c-110">Sample schemas are available on: [GitHub at PnP-Provisioning-Schema/Samples](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples).</span></span>

<span data-ttu-id="9ff9c-111">Der Codeabschnitt darunter werden das Schemastammelement und direkte untergeordnete Elemente des Stammverzeichnisses angezeigt.</span><span class="sxs-lookup"><span data-stu-id="9ff9c-111">The code block below displays the schema's root element and direct child elements of the root.</span></span> <span data-ttu-id="9ff9c-112">Bereitstellung Schemadokumentation finden Sie unter GitHub: [Plug & Play-Bereitstellung Schema](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md).</span><span class="sxs-lookup"><span data-stu-id="9ff9c-112">You can find provisioning schema documentation on GitHub: [PnP Provisioning Schema](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md).</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="9ff9c-113">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9ff9c-113">Additional resources</span></span>
<span data-ttu-id="9ff9c-114"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9ff9c-114"></span></span>

- [<span data-ttu-id="9ff9c-115">Betrachtung der Sequenzierung Plug & Play-Bereitstellung Engine-Schema</span><span class="sxs-lookup"><span data-stu-id="9ff9c-115">Deep dive to PnP provisioning engine schema</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)
    
- [<span data-ttu-id="9ff9c-116">Plug & Play-Bereitstellung Schema</span><span class="sxs-lookup"><span data-stu-id="9ff9c-116">PnP Provisioning Schema</span></span>](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md)
    
- [<span data-ttu-id="9ff9c-117">GitHub am PnP-Provisioning-Schema/Beispiele (engl.)</span><span class="sxs-lookup"><span data-stu-id="9ff9c-117">GitHub at PnP-Provisioning-Schema/Samples</span></span>](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples)
