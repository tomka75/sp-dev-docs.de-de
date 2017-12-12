---
title: "Ändern der SharePoint-Host-Web-Listen zum Zeitpunkt der Erstellung"
ms.date: 11/03/2017
ms.openlocfilehash: f9febeb90286fd49a28ff543692de62fb10f611a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="modify-sharepoint-host-web-lists-at-creation-time"></a><span data-ttu-id="02521-102">Ändern der SharePoint-Host-Web-Listen zum Zeitpunkt der Erstellung</span><span class="sxs-lookup"><span data-stu-id="02521-102">Modify SharePoint host web lists at creation time</span></span>

<span data-ttu-id="02521-103">Ändern einer SharePoint-Liste im hostweb zum Zeitpunkt der Erstellung Liste erstellt.</span><span class="sxs-lookup"><span data-stu-id="02521-103">Modify a SharePoint list created in the host web at list creation time.</span></span>

<span data-ttu-id="02521-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="02521-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="02521-105">Wenn Sie eine neue Liste in der Hostwebsite erstellen, können Sie einen **ListAdded** remote-Ereignisempfänger verwenden, um dieser Liste zu ändern.</span><span class="sxs-lookup"><span data-stu-id="02521-105">When you create a new list in the host web, you can use a **ListAdded** remote event receiver to modify that list.</span></span> <span data-ttu-id="02521-106">Sie können beispielsweise Versioning, aktivieren oder Hinzufügen eines Inhaltstyps in die Liste oder eine beliebige andere Änderungen durch das Clientobjektmodell (CSOM) implementiert.</span><span class="sxs-lookup"><span data-stu-id="02521-106">For example, you can enable versioning, or add a content type to the list, or make any other changes implemented by the client object model (CSOM).</span></span>

<span data-ttu-id="02521-107">Wenn die Liste mit der Hostwebsite hinzugefügt wird, müssen Sie den Ereignisempfänger programmgesteuert anfügen.</span><span class="sxs-lookup"><span data-stu-id="02521-107">When the list is added to the host web, you need to programmatically attach the event receiver.</span></span> <span data-ttu-id="02521-108">Das [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) -Beispiel zeigt, wie Sie ein Add-in vom Anbieter gehosteten dazu verwenden.</span><span class="sxs-lookup"><span data-stu-id="02521-108">The [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) sample shows you how to use a provider-hosted add-in to do this.</span></span> <span data-ttu-id="02521-109">Wenn das Add-in installiert ist, ein **AppInstalled** -Ereignis tritt ein, und verwenden Sie dieses Ereignis So fügen Sie das **ListAdded** -Ereignis an.</span><span class="sxs-lookup"><span data-stu-id="02521-109">When the add-in is installed, an **AppInstalled** event occurs, and you use this event to attach the **ListAdded** event.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="02521-110">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="02521-110">Before you begin</span></span>

<span data-ttu-id="02521-111">Laden Sie Sie zuerst [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="02521-111">To get started, download the [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="attach-the-listadded-event"></a><span data-ttu-id="02521-112">Fügen Sie das ListAdded-Ereignis</span><span class="sxs-lookup"><span data-stu-id="02521-112">Attach the ListAdded event</span></span>

<span data-ttu-id="02521-113">Um die Ereignishandler für das Add-in zu implementieren, zeigen Sie die Eigenschaften für das SharePoint-Projekt, und **Handle-Add-in installiert** und **Handle-Add-in deinstallieren** auf **True**festgelegt.</span><span class="sxs-lookup"><span data-stu-id="02521-113">To implement the event handlers for the add-in, display the properties for the SharePoint project, and set both  **Handle Add-in Installed** and **Handle Add-in Uninstalling** to **True**.</span></span>

<span data-ttu-id="02521-114">Im folgenden Codebeispiel wird veranschaulicht, wie der Ereignisempfänger **AppInstalled** So fügen Sie den Ereignisempfänger **ListAdded** geändert wird.</span><span class="sxs-lookup"><span data-stu-id="02521-114">The following code example shows how the  **AppInstalled** event receiver is modified to attach the **ListAdded** event receiver.</span></span>

> [!NOTE] 
> <span data-ttu-id="02521-115">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="02521-115">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
bool rerExists = false;
cc.Load(cc.Web.EventReceivers);
cc.ExecuteQuery();

foreach (var rer in cc.Web.EventReceivers)
{
  if (rer.ReceiverName == RECEIVER_NAME)
  {
    rerExists = true;
  }
}

if (!rerExists)
{
  EventReceiverDefinitionCreationInformation receiver = new EventReceiverDefinitionCreationInformation();
  receiver.EventType = EventReceiverType.ListAdded;

  // Get WCF URL where this message was handled.
  OperationContext op = OperationContext.Current;
  Message msg = op.RequestContext.RequestMessage;
  receiver.ReceiverUrl = msg.Headers.To.ToString();
  receiver.ReceiverName = RECEIVER_NAME;
  receiver.Synchronization = EventReceiverSynchronization.Synchronous;
  cc.Web.EventReceivers.Add(receiver);
  cc.ExecuteQuery();
}
```

## <a name="customize-the-added-lists"></a><span data-ttu-id="02521-116">Anpassen der hinzugefügten Listen</span><span class="sxs-lookup"><span data-stu-id="02521-116">Customize the added lists</span></span>

<span data-ttu-id="02521-117">Wenn der Ereignishandler **ListAdded** ausgelöst wird, wird der folgende Code ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="02521-117">When the  **ListAdded** event handler is firing, the following code runs.</span></span>

```C#
private void HandleListAdded(SPRemoteEventProperties properties)
{
  using (ClientContext cc = TokenHelper.CreateRemoteEventReceiverClientContext(properties))
  {
    if (cc != null)
    {
      try
        {
          if (properties.ListEventProperties.TemplateId == (int)ListTemplateType.DocumentLibrary)
          {
          //set versioning 
   cc.Web.GetListByTitle(properties.ListEventProperties.ListTitle).UpdateListVersioning(true, true);
          }
        }
         catch (Exception ex)
         {
           System.Diagnostics.Trace.WriteLine(ex.Message);
         }
       }
    }
  }
}
```

## <a name="uninstalling-the-event-receiver"></a><span data-ttu-id="02521-118">Deinstallieren den Ereignisempfänger</span><span class="sxs-lookup"><span data-stu-id="02521-118">Uninstalling the event receiver</span></span>

<span data-ttu-id="02521-119">Wenn das Add-in deinstalliert wird, sollte der Ereignisempfänger auch entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="02521-119">When the add-in is uninstalled, the event receiver should also be removed.</span></span> <span data-ttu-id="02521-120">Damit dies funktioniert während des Debuggens, wechseln Sie zu der Dokumentbibliothek **im Test-Add-ins** , und verwenden Sie die Option **Entfernen** , klicken Sie auf das Add-in.</span><span class="sxs-lookup"><span data-stu-id="02521-120">To make this work during debugging, go to the  **Add-ins in testing** library and use the **remove** option on the add-in.</span></span> <span data-ttu-id="02521-121">Dadurch wird das Ereignis **AppUninstalling** mit den entsprechenden Berechtigungen den erstellte remote Ereignishandler entfernt.</span><span class="sxs-lookup"><span data-stu-id="02521-121">This triggers the **AppUninstalling** event with the proper permissions to remove the created remote event handler.</span></span> <span data-ttu-id="02521-122">Wenn Sie nur schließen Sie den Browser oder des Add-Ins auf **Websiteinhalte deinstallieren**, nie der Ereignisempfänger ausgelöst wird, oder der Ereignisempfänger **AppUninstalling** mit nicht über ausreichende Berechtigungen zum Entfernen des Ereignisempfängers **ListAdded** ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="02521-122">If you just close the browser or uninstall the add-in from **site contents**, either the event receiver never fires or the **AppUninstalling** event receiver runs with insufficient permissions to remove the **ListAdded** event receiver.</span></span> <span data-ttu-id="02521-123">Dies ist, da-add-ins anders bereitgestellt werden, wenn diese Seite geladen ist, die Funktionsweise Visual Studio werden, wenn Sie F5 drücken.</span><span class="sxs-lookup"><span data-stu-id="02521-123">This is because add-ins are deployed differently when they are side loaded, which is what Visual Studio does when you press F5.</span></span>

> [!NOTE] 
> <span data-ttu-id="02521-124">Es wird empfohlen, dieses Beispiels in einer Neuinstallation Developer-Website testen.</span><span class="sxs-lookup"><span data-stu-id="02521-124">We recommend that you test this sample in a clean developer site.</span></span>

## <a name="see-also"></a><span data-ttu-id="02521-125">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="02521-125">See also</span></span>
<span data-ttu-id="02521-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="02521-126"></span></span>

- [<span data-ttu-id="02521-127">SharePoint-Website Bereitstellen von Lösungen</span><span class="sxs-lookup"><span data-stu-id="02521-127">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="02521-128">Core.EventReceiversBasedModifications-Beispiel</span><span class="sxs-lookup"><span data-stu-id="02521-128">Core.EventReceiversBasedModifications sample</span></span>](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications)
