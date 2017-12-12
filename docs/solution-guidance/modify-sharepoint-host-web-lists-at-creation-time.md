---
title: "Ändern der SharePoint-Host-Web-Listen zum Zeitpunkt der Erstellung"
ms.date: 11/03/2017
ms.openlocfilehash: f9febeb90286fd49a28ff543692de62fb10f611a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="modify-sharepoint-host-web-lists-at-creation-time"></a>Ändern der SharePoint-Host-Web-Listen zum Zeitpunkt der Erstellung

Ändern einer SharePoint-Liste im hostweb zum Zeitpunkt der Erstellung Liste erstellt.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Wenn Sie eine neue Liste in der Hostwebsite erstellen, können Sie einen **ListAdded** remote-Ereignisempfänger verwenden, um dieser Liste zu ändern. Sie können beispielsweise Versioning, aktivieren oder Hinzufügen eines Inhaltstyps in die Liste oder eine beliebige andere Änderungen durch das Clientobjektmodell (CSOM) implementiert.

Wenn die Liste mit der Hostwebsite hinzugefügt wird, müssen Sie den Ereignisempfänger programmgesteuert anfügen. Das [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) -Beispiel zeigt, wie Sie ein Add-in vom Anbieter gehosteten dazu verwenden. Wenn das Add-in installiert ist, ein **AppInstalled** -Ereignis tritt ein, und verwenden Sie dieses Ereignis So fügen Sie das **ListAdded** -Ereignis an.

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Laden Sie Sie zuerst [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="attach-the-listadded-event"></a>Fügen Sie das ListAdded-Ereignis

Um die Ereignishandler für das Add-in zu implementieren, zeigen Sie die Eigenschaften für das SharePoint-Projekt, und **Handle-Add-in installiert** und **Handle-Add-in deinstallieren** auf **True**festgelegt.

Im folgenden Codebeispiel wird veranschaulicht, wie der Ereignisempfänger **AppInstalled** So fügen Sie den Ereignisempfänger **ListAdded** geändert wird.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

## <a name="customize-the-added-lists"></a>Anpassen der hinzugefügten Listen

Wenn der Ereignishandler **ListAdded** ausgelöst wird, wird der folgende Code ausgeführt.

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

## <a name="uninstalling-the-event-receiver"></a>Deinstallieren den Ereignisempfänger

Wenn das Add-in deinstalliert wird, sollte der Ereignisempfänger auch entfernt werden. Damit dies funktioniert während des Debuggens, wechseln Sie zu der Dokumentbibliothek **im Test-Add-ins** , und verwenden Sie die Option **Entfernen** , klicken Sie auf das Add-in. Dadurch wird das Ereignis **AppUninstalling** mit den entsprechenden Berechtigungen den erstellte remote Ereignishandler entfernt. Wenn Sie nur schließen Sie den Browser oder des Add-Ins auf **Websiteinhalte deinstallieren**, nie der Ereignisempfänger ausgelöst wird, oder der Ereignisempfänger **AppUninstalling** mit nicht über ausreichende Berechtigungen zum Entfernen des Ereignisempfängers **ListAdded** ausgeführt wird. Dies ist, da-add-ins anders bereitgestellt werden, wenn diese Seite geladen ist, die Funktionsweise Visual Studio werden, wenn Sie F5 drücken.

> [!NOTE] 
> Es wird empfohlen, dieses Beispiels in einer Neuinstallation Developer-Website testen.

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [SharePoint-Website Bereitstellen von Lösungen](sharepoint-site-provisioning-solutions.md)
    
- [Core.EventReceiversBasedModifications-Beispiel](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications)
