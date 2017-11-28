---
title: Verwendung von OneDrive for Business in einem Multi-Geo-Mandanten
ms.date: 11/03/2017
ms.openlocfilehash: 4373f4073a36326d250317bf05f4dd82cd19a84f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="using-onedrive-for-business-in-a-multi-geo-tenant"></a>Verwendung von OneDrive for Business in einem Multi-Geo-Mandanten

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

OneDrive for Business-Website eines Benutzers zugreifen, auch bekannt als persönliche Websites oder Meine Website ist ein allgemeines Szenario in benutzerdefinierte Anwendungen. In diesem Artikel wird beschrieben, wie OneDrive for Business-Websites in einer Serverfarm mit mehreren geografisch Mandanten entwickelt.

Eine von mehreren APIs können Sie eine OneDrive for Business-Website zugreifen:

- Microsoft Graph (empfohlen)
- SharePoint-Clientobjektmodell 
- SharePoint-REST-API


## <a name="read-onedrive-for-business-files-using-microsoft-graph"></a>Lesen von OneDrive for Business-Dateien mithilfe von Microsoft Graph
Wenn Sie Microsoft Graph zum Lesen einer OneDrive for Business-Datei verwenden, müssen Sie wissen, wo OneDrive-Website eines Benutzers befindet. Wenn Sie auf das Laufwerk, anfordern, wie in den folgenden Beispielen dargestellt, erhalten Sie die Dateien, die Sie benötigen. 

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com/drive/root/children


GET https://graph.microsoft.com/v1.0/users/me/drive/root/children
```

## <a name="get-the-location-of-a-users-onedrive-for-business-site-using-microsoft-graph"></a>Rufen Sie Standort des Benutzers OneDrive for Business-Site mithilfe von Microsoft Graph ab
Die folgenden Beispiele zeigen, wie Sie die Position des eine OneDrive for Business-Website mit der Microsoft Graph-API abgerufen wird.

```
GET https://graph.microsoft.com/v1.0/users/admin@a830edad9050849524e17052212.onmicrosoft.com/mySite


GET https://graph.microsoft.com/v1.0/users/me/mySite
```

Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

## <a name="get-the-location-of-a-users-onedrive-for-business-site-using-csom-and-rest"></a>Rufen Sie Standort des Benutzers OneDrive for Business-Site mithilfe von CSOM und REST ab
Das folgende Beispiel zeigt eine REST-basierte Abfrage an die Position des ein OneDrive for Business-Website abgerufen.

```
GET https://contoso.sharepoint.com/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)/PersonalUrl?%40v=%27i%3A0%23.f%7Cmembership%7Cbert%40contoso.onmicrosoft.com%27
```

Wenn Sie c# verwenden, können Sie CSOM, um die Position des ein OneDrive for Business-Website abgerufen.

```C#
public string GetUserPersonalUrlCSOM(ClientContext ctx, string userPrincipalName)
{
    string result = null;

    PeopleManager peopleManager = new PeopleManager(ctx);
    var userProperties = peopleManager.GetPropertiesFor(userPrincipalName);
    this.clientContext.ExecuteQuery();
    result = userProperties.PersonalUrl;

    return result;
}
```

## <a name="read-onedrive-for-business-files-using-csom-and-rest"></a>Lesen von OneDrive for Business-Dateien mithilfe von CSOM und REST

Lesen von Dateien mit CSOM ist identisch mit Lesen von Dateien in anderen Websitesammlungen, die eine OneDrive for Business-Website ist eine reguläre SharePoint-Websitesammlung mit einer Dokumentbibliothek mit Dateien. Finden Sie im Ressourcenabschnitt Beispiele zur Verwendung von CSOM und REST zum Hochladen von Dateien.

## <a name="see-also"></a>Siehe auch

- [Lesen von Dateien mithilfe der Microsoft Graph-API](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/item_list_children)
- [Hochladen von Dateien mithilfe von REST](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RestFileUpload)
- [Datei hochladen CSOM SharePoint-Add-Ins](https://github.com/SharePoint/PnP/tree/master/Samples/Core.FileUpload)
- [Große Dateien hochladen mit CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)


