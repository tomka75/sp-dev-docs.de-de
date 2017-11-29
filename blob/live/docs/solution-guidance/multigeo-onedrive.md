---
title: Verwendung von OneDrive for Business in einem Multi-Geo-Mandanten
ms.date: 11/03/2017
ms.openlocfilehash: 4373f4073a36326d250317bf05f4dd82cd19a84f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="using-onedrive-for-business-in-a-multi-geo-tenant"></a><span data-ttu-id="2da88-102">Verwendung von OneDrive for Business in einem Multi-Geo-Mandanten</span><span class="sxs-lookup"><span data-stu-id="2da88-102">Using OneDrive for Business in a Multi-Geo tenant</span></span>

> <span data-ttu-id="2da88-103">**Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.</span><span class="sxs-lookup"><span data-stu-id="2da88-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="2da88-104">OneDrive for Business-Website eines Benutzers zugreifen, auch bekannt als persönliche Websites oder Meine Website ist ein allgemeines Szenario in benutzerdefinierte Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="2da88-104">Accessing a user's OneDrive for Business site, also known as personal site or my site, is a common scenario in custom applications.</span></span> <span data-ttu-id="2da88-105">In diesem Artikel wird beschrieben, wie OneDrive for Business-Websites in einer Serverfarm mit mehreren geografisch Mandanten entwickelt.</span><span class="sxs-lookup"><span data-stu-id="2da88-105">This article describes how to work with OneDrive for Business sites in a Multi-Geo tenant.</span></span>

<span data-ttu-id="2da88-106">Eine von mehreren APIs können Sie eine OneDrive for Business-Website zugreifen:</span><span class="sxs-lookup"><span data-stu-id="2da88-106">You can use one of several APIs to access a OneDrive for Business site:</span></span>

- <span data-ttu-id="2da88-107">Microsoft Graph (empfohlen)</span><span class="sxs-lookup"><span data-stu-id="2da88-107">Microsoft Graph (preferred)</span></span>
- <span data-ttu-id="2da88-108">SharePoint-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="2da88-108">SharePoint CSOM</span></span> 
- <span data-ttu-id="2da88-109">SharePoint-REST-API</span><span class="sxs-lookup"><span data-stu-id="2da88-109">SharePoint REST API</span></span>


## <a name="read-onedrive-for-business-files-using-microsoft-graph"></a><span data-ttu-id="2da88-110">Lesen von OneDrive for Business-Dateien mithilfe von Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="2da88-110">Read OneDrive for Business files using Microsoft Graph</span></span>
<span data-ttu-id="2da88-111">Wenn Sie Microsoft Graph zum Lesen einer OneDrive for Business-Datei verwenden, müssen Sie wissen, wo OneDrive-Website eines Benutzers befindet.</span><span class="sxs-lookup"><span data-stu-id="2da88-111">When you use Microsoft Graph to read a OneDrive for Business file, you don't have to know where a user's OneDrive site is located.</span></span> <span data-ttu-id="2da88-112">Wenn Sie auf das Laufwerk, anfordern, wie in den folgenden Beispielen dargestellt, erhalten Sie die Dateien, die Sie benötigen.</span><span class="sxs-lookup"><span data-stu-id="2da88-112">When you request the drive, as shown in the following examples, you'll get the files you need.</span></span> 

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com/drive/root/children


GET https://graph.microsoft.com/v1.0/users/me/drive/root/children
```

## <a name="get-the-location-of-a-users-onedrive-for-business-site-using-microsoft-graph"></a><span data-ttu-id="2da88-113">Rufen Sie Standort des Benutzers OneDrive for Business-Site mithilfe von Microsoft Graph ab</span><span class="sxs-lookup"><span data-stu-id="2da88-113">Get the location of a user's OneDrive for Business site using Microsoft Graph</span></span>
<span data-ttu-id="2da88-114">Die folgenden Beispiele zeigen, wie Sie die Position des eine OneDrive for Business-Website mit der Microsoft Graph-API abgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="2da88-114">The following examples show how to get the location of a OneDrive for Business site using the Microsoft Graph API.</span></span>

```
GET https://graph.microsoft.com/v1.0/users/admin@a830edad9050849524e17052212.onmicrosoft.com/mySite


GET https://graph.microsoft.com/v1.0/users/me/mySite
```

<span data-ttu-id="2da88-115">Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="2da88-115">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

## <a name="get-the-location-of-a-users-onedrive-for-business-site-using-csom-and-rest"></a><span data-ttu-id="2da88-116">Rufen Sie Standort des Benutzers OneDrive for Business-Site mithilfe von CSOM und REST ab</span><span class="sxs-lookup"><span data-stu-id="2da88-116">Get the location of a user's OneDrive for Business site using CSOM and REST</span></span>
<span data-ttu-id="2da88-117">Das folgende Beispiel zeigt eine REST-basierte Abfrage an die Position des ein OneDrive for Business-Website abgerufen.</span><span class="sxs-lookup"><span data-stu-id="2da88-117">The following example shows a REST-based query to get the location of an OneDrive for Business site.</span></span>

```
GET https://contoso.sharepoint.com/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)/PersonalUrl?%40v=%27i%3A0%23.f%7Cmembership%7Cbert%40contoso.onmicrosoft.com%27
```

<span data-ttu-id="2da88-118">Wenn Sie c# verwenden, können Sie CSOM, um die Position des ein OneDrive for Business-Website abgerufen.</span><span class="sxs-lookup"><span data-stu-id="2da88-118">If you're using C#, you can use CSOM to get the location of an OneDrive for Business site.</span></span>

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

## <a name="read-onedrive-for-business-files-using-csom-and-rest"></a><span data-ttu-id="2da88-119">Lesen von OneDrive for Business-Dateien mithilfe von CSOM und REST</span><span class="sxs-lookup"><span data-stu-id="2da88-119">Read OneDrive for Business files using CSOM and REST</span></span>

<span data-ttu-id="2da88-120">Lesen von Dateien mit CSOM ist identisch mit Lesen von Dateien in anderen Websitesammlungen, die eine OneDrive for Business-Website ist eine reguläre SharePoint-Websitesammlung mit einer Dokumentbibliothek mit Dateien.</span><span class="sxs-lookup"><span data-stu-id="2da88-120">Reading files using CSOM is identical to reading files on other site collections, a OneDrive for Business site is a regular SharePoint site collection with a document library containing files.</span></span> <span data-ttu-id="2da88-121">Finden Sie im Ressourcenabschnitt Beispiele zur Verwendung von CSOM und REST zum Hochladen von Dateien.</span><span class="sxs-lookup"><span data-stu-id="2da88-121">See the resources section for samples on using CSOM and REST to upload files.</span></span>

## <a name="see-also"></a><span data-ttu-id="2da88-122">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2da88-122">See also</span></span>

- [<span data-ttu-id="2da88-123">Lesen von Dateien mithilfe der Microsoft Graph-API</span><span class="sxs-lookup"><span data-stu-id="2da88-123">Reading files using the Microsoft Graph API</span></span>](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/item_list_children)
- [<span data-ttu-id="2da88-124">Hochladen von Dateien mithilfe von REST</span><span class="sxs-lookup"><span data-stu-id="2da88-124">Uploading files using REST</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RestFileUpload)
- [<span data-ttu-id="2da88-125">Datei hochladen CSOM SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="2da88-125">File Upload CSOM SharePoint Add-in</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.FileUpload)
- [<span data-ttu-id="2da88-126">Große Dateien hochladen mit CSOM</span><span class="sxs-lookup"><span data-stu-id="2da88-126">Large file upload with CSOM</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)


