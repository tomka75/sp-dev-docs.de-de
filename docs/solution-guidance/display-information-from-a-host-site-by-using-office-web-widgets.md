---
title: Anzeigen von Informationen aus einer Hostwebsite mithilfe von Office Web Widgets
ms.date: 11/03/2017
ms.openlocfilehash: b981754845acf967f9a0beb23dd9f0a73186a6ed
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="display-information-from-a-host-site-by-using-office-web-widgets"></a>Anzeigen von Informationen aus einer Hostwebsite mithilfe von Office Web Widgets

Implementieren Sie Office Web Widgets-Steuerelemente in einem SharePoint vom Anbieter gehosteten add-in zum Anzeigen von Informationen aus einer Hostwebsite.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Sie können Office Web Widgets verwenden, zum Anzeigen von Informationen aus einer Website in SharePoint gehostete im Zusammenhang mit einer vom Anbieter gehosteten-add-in. Office Web Widgets sind eine Reihe von Steuerelementen, mit denen Aussehen und Verhalten wie SharePoint-Hosting-Steuerelemente. Die Steuerelemente werden als ein [NuGet](https://www.nuget.org/) -Paket bereitgestellt und die [Bibliothek zu Office Web Widgets stellt](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).

**Vorsicht:**  Office Web Widgets sind ein Feature von Drittanbietern. Da sie einige Einschränkungen haben, verwenden sie mit Vorsicht. Weitere Informationen finden Sie unter:

Das [Core.OfficeWebWidgets](https://github.com/SharePoint/PnP/tree/dev/Components/Core.OfficeWebWidgets) -Beispiel veranschaulicht das Implementieren Sie die Personenauswahl und Listenansicht-Steuerelemente, die in der Bibliothek zu Office Web Widgets enthalten sind. In diesem Beispiel-add-in die Steuerelemente in der HTML-Code auf der Startseite eingefügt, und konfiguriert dann die Steuerelemente mithilfe der app.js-JavaScript-Datei, die sich in Skripts-Projektordner befindet.

Das Beispiel starten Seite zeigt die personenauswahlsteuerung. Auf dieser Seite können Sie mehrere Benutzer hinzufügen, und es enthält zwei Textfelder für die Eingabe des Benutzers.

**Abbildung 1. Personen Personenauswahl Demo-Startseite**

![Personen Personenauswahl Demo-Startseite](media/display-information-from-a-host-site-by-using-office-web-widgets/2d6c1585-9615-45c4-b931-a2e0e7d57b3d.png)

Der folgende Code aus der Datei "default.aspx" des Webprojekts umfasst die personenauswahlsteuerung innerhalb einer `<div>` Tag.

```
<div id="peoplePickerBackupSiteOwners" data-office-control="Office.Controls.PeoplePicker" data-office-options=
      '{ "placeholder" : "Please choose one or more backup site owner", 
      "allowMultipleSelections" : true,
      "onChange" : handleSiteOwnerBackupChange}'>
</div>

```

Die Startseite zeigt auch das Listenansicht-Steuerelement, das Listen aus dem hostweb und der Web-Add-in der SharePoint-Website anzeigen kann.

**Abbildung 2. Steuerelement Start Listenansichtsseite**

![Steuerelement Einführung Listenansichtsseite](media/display-information-from-a-host-site-by-using-office-web-widgets/c8bc86d4-6cae-4dc0-94a4-97a0e5a49c7d.png)

Der folgende HTML-Code aus der Datei Default.aspx enthält zwei `<div>` Tags für die Anzeige von zwei Instanzen der Liste Steuerelement anzuzeigen.

```
The list view widget can show (currently no inline editing) data from a list on the add-in web:<br />
<div id="listViewAppWeb"></div>
        <br /><br />
        But the same applies for a list on the host web web:<br />
        <div id="listViewHostWeb"></div>
```

Der folgende Code aus der Datei app.js erstellt die zwei Instanzen des Listenansicht-Steuerelements.

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

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [UX-Komponenten in SharePoint 2013 und SharePoint Online](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
