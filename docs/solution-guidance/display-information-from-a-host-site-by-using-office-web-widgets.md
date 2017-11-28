---
title: Anzeigen von Informationen aus einer Hostwebsite mithilfe von Office Web Widgets
ms.date: 11/03/2017
ms.openlocfilehash: 4554a56d4d7036a948cc1c992793efdf7325268d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="display-information-from-a-host-site-by-using-office-web-widgets"></a><span data-ttu-id="5e5d5-102">Anzeigen von Informationen aus einer Hostwebsite mithilfe von Office Web Widgets</span><span class="sxs-lookup"><span data-stu-id="5e5d5-102">Display information from a host site by using Office Web Widgets</span></span>

<span data-ttu-id="5e5d5-103">Implementieren Sie Office Web Widgets-Steuerelemente in einem SharePoint vom Anbieter gehosteten add-in zum Anzeigen von Informationen aus einer Hostwebsite.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-103">Implement Office Web Widget controls in a SharePoint provider-hosted add-in to display information from a host site.</span></span>

<span data-ttu-id="5e5d5-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="5e5d5-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="5e5d5-105">Sie können Office Web Widgets verwenden, zum Anzeigen von Informationen aus einer Website in SharePoint gehostete im Zusammenhang mit einer vom Anbieter gehosteten-add-in.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-105">You can use Office Web Widgets to display information from a SharePoint-hosted site in the context of a provider-hosted add-in.</span></span> <span data-ttu-id="5e5d5-106">Office Web Widgets sind eine Reihe von Steuerelementen, mit denen Aussehen und Verhalten wie SharePoint-Hosting-Steuerelemente.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-106">Office Web Widgets are a set of controls that are designed to look and behave like SharePoint-hosted controls.</span></span> <span data-ttu-id="5e5d5-107">Die Steuerelemente werden als ein [NuGet](https://www.nuget.org/) -Paket bereitgestellt und die [Bibliothek zu Office Web Widgets stellt](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span><span class="sxs-lookup"><span data-stu-id="5e5d5-107">The controls are provided as a [NuGet](https://www.nuget.org/) package, which provides the [Office Web Widgets library](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span></span>

<span data-ttu-id="5e5d5-108">**Vorsicht:**  Office Web Widgets sind ein Feature von Drittanbietern.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-108">**Caution:**  Office Web Widgets are a third-party feature.</span></span> <span data-ttu-id="5e5d5-109">Da sie einige Einschränkungen haben, verwenden sie mit Vorsicht.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-109">Because they have some limitations, use them with caution.</span></span> <span data-ttu-id="5e5d5-110">Weitere Informationen finden Sie unter:</span><span class="sxs-lookup"><span data-stu-id="5e5d5-110">For more information, see:</span></span>

<span data-ttu-id="5e5d5-111">Das [Core.OfficeWebWidgets](https://github.com/SharePoint/PnP/tree/dev/Components/Core.OfficeWebWidgets) -Beispiel veranschaulicht das Implementieren Sie die Personenauswahl und Listenansicht-Steuerelemente, die in der Bibliothek zu Office Web Widgets enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-111">The [Core.OfficeWebWidgets](https://github.com/SharePoint/PnP/tree/dev/Components/Core.OfficeWebWidgets) sample shows you how to implement the people picker and list view controls that are included in the Office Web Widgets library.</span></span> <span data-ttu-id="5e5d5-112">In diesem Beispiel-add-in die Steuerelemente in der HTML-Code auf der Startseite eingefügt, und konfiguriert dann die Steuerelemente mithilfe der app.js-JavaScript-Datei, die sich in Skripts-Projektordner befindet.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-112">This sample add-in inserts the controls into the HTML of the start page, and then configures the controls using the app.js JavaScript file that is located in the project's Scripts folder.</span></span>

<span data-ttu-id="5e5d5-113">Das Beispiel starten Seite zeigt die personenauswahlsteuerung.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-113">The sample start page shows the people picker control.</span></span> <span data-ttu-id="5e5d5-114">Auf dieser Seite können Sie mehrere Benutzer hinzufügen, und es enthält zwei Textfelder für die Eingabe des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-114">This page allows you to add multiple users, and it contains two text boxes for user input.</span></span>

<span data-ttu-id="5e5d5-115">**Abbildung 1. Personen Personenauswahl Demo-Startseite**</span><span class="sxs-lookup"><span data-stu-id="5e5d5-115">**Figure 1. People picker demo start page**</span></span>

![Personen Personenauswahl Demo-Startseite](media/display-information-from-a-host-site-by-using-office-web-widgets/2d6c1585-9615-45c4-b931-a2e0e7d57b3d.png)

<span data-ttu-id="5e5d5-117">Der folgende Code aus der Datei "default.aspx" des Webprojekts umfasst die personenauswahlsteuerung innerhalb einer `<div>` Tag.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-117">The following code from the Default.aspx file of the web project includes the people picker control inside a  `<div>` tag.</span></span>

```
<div id="peoplePickerBackupSiteOwners" data-office-control="Office.Controls.PeoplePicker" data-office-options=
      '{ "placeholder" : "Please choose one or more backup site owner", 
      "allowMultipleSelections" : true,
      "onChange" : handleSiteOwnerBackupChange}'>
</div>

```

<span data-ttu-id="5e5d5-118">Die Startseite zeigt auch das Listenansicht-Steuerelement, das Listen aus dem hostweb und der Web-Add-in der SharePoint-Website anzeigen kann.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-118">The start page also displays the list view control, which can display lists from both the host web and the add-in web of the SharePoint site.</span></span>

<span data-ttu-id="5e5d5-119">**Abbildung 2. Steuerelement Start Listenansichtsseite**</span><span class="sxs-lookup"><span data-stu-id="5e5d5-119">**Figure 2. List view control start page**</span></span>

![Steuerelement Einführung Listenansichtsseite](media/display-information-from-a-host-site-by-using-office-web-widgets/c8bc86d4-6cae-4dc0-94a4-97a0e5a49c7d.png)

<span data-ttu-id="5e5d5-121">Der folgende HTML-Code aus der Datei Default.aspx enthält zwei `<div>` Tags für die Anzeige von zwei Instanzen der Liste Steuerelement anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-121">The following HTML from the Default.aspx file includes two  `<div>` tags for displaying the two instances of the list view control.</span></span>

```
The list view widget can show (currently no inline editing) data from a list on the add-in web:<br />
<div id="listViewAppWeb"></div>
        <br /><br />
        But the same applies for a list on the host web web:<br />
        <div id="listViewHostWeb"></div>
```

<span data-ttu-id="5e5d5-122">Der folgende Code aus der Datei app.js erstellt die zwei Instanzen des Listenansicht-Steuerelements.</span><span class="sxs-lookup"><span data-stu-id="5e5d5-122">The following code from the app.js file creates the two instances of the list view control.</span></span>

```
 var listViewAppWeb = new Office.Controls.ListView(document.getElementById("listViewAppWeb"),
          {
                     listUrl: appWebUrl + "/_api/web/lists/getbytitle('Announcements')"
           });

var listViewHostWeb = new Office.Controls.ListView(document.getElementById("listViewHostWeb"),
           {
                     listUrl: spHostUrl + "/_api/web/lists/getbytitle('Site Pages')"
           });
```

## <a name="additional-resources"></a><span data-ttu-id="5e5d5-123">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="5e5d5-123">Additional resources</span></span>
<span data-ttu-id="5e5d5-124"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="5e5d5-124"></span></span>

- [<span data-ttu-id="5e5d5-125">UX-Komponenten in SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="5e5d5-125">UX Components in SharePoint 2013 and SharePoint Online</span></span>](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
