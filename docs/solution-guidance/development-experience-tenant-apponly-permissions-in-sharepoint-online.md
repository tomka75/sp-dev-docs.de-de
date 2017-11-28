---
title: Entwickeln mit dem Mandanten Berechtigungen mit App-Only in SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: 7e4080cf1847a1dcf98d1dbb19149a4bbfa8edd5
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="developing-using-tenant-permissions-with-app-only-in-sharepoint-online"></a>Entwickeln mit dem Mandanten Berechtigungen mit App-Only in SharePoint Online

Die Entwicklerarbeit wurde SharePoint **gehostet durch Drittanbieter-Add-ins** , die **in Kombination mit nur-app - Mandanten**Erlaubnis geändert. Dieser Artikel führt Sie durch die neue Oberfläche für die Entwicklung und das Debuggen diese Lösungen. 

_**Gilt für:** Vom Anbieter gehosteten-Add-ins für SharePoint Online_


## <a name="understanding-the-problem"></a>Beschreibung des Problems
In Visual Studio Navigieren Sie zum Debuggen, Debuggen starten und eine Meldung angezeigt, "**Ihrer mandantenadministrator verfügt über diese app genehmigt**" wie im folgenden dargestellt werden.
![](http://i.imgur.com/oFH9oqb.png). 

Der Grund, warum Sie ist nicht möglich, **vertrauensbezogener klicken,** ist, da Visual Studio für die Websitesammlung Dev funktioniert Sie in Ihrem projekteinstellungen festgelegt haben, die Berechtigungsstufe mit nur-app-Mandanten nur über [gewährt werden können sie anhand Ihres Mandanten vertrauen Verwaltungssite](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online).

## <a name="walkthrough"></a>Exemplarische Vorgehensweise
### <a name="step-1-create-a-new-service-principal"></a>Schritt 1: Erstellen einer neuen Dienstprinzipalnamen
Navigieren Sie zu einer Websitesammlung in Ihrem Mandanten, und generieren Sie eine neue Client-Id und geheimen Schlüssel. (Z. B. https://contoso.sharepoint.com/_layouts/15/appregnew.aspx). Klicken Sie auf dieser Seite auf **generieren** für sowohl die **Client-Id**, **Geheimer Clientschlüssel** Felder und geben Sie die restlichen Felder an. Während Sie entwickeln des Add-Ins Stellen Sie sicher, dass Sie den Port als App-Domäne einschließlich localhost.com verwenden. Sie sollten dann in etwa wie unten verfügen.

![](http://i.imgur.com/5CfHgFD.png)

### <a name="step-2-grant-tenant-permissions"></a>Schritt 2: Grant-Mandanten Berechtigungen
Um diesen Schritt ausführen zu können, müssen Sie eine SharePoint Online-Administrator sein. 

Navigieren Sie zu der SharePoint-Verwaltungskonsole (z. B. https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx) und erteilen Sie den Mandanten Berechtigungen.![](http://i.imgur.com/EGuJG3a.png)

![](http://i.imgur.com/dst9ZdP.png)


### <a name="step-3-update-your-manifest-and-webconfig"></a>Schritt 3: Aktualisieren Sie Ihrer Manifest und in "Web.config"
In der Visual Studio-Lösung Aktualisieren Sie das Manifest und web.config mit die Client-Id, die in Schritt 1 erstellte.
![](http://i.imgur.com/fKkLIde.png)


### <a name="step-4-package-the-app-and-add-the-app-file-to-the-app-catalog"></a>Schritt 4: Packen Sie die app und fügen die Datei am Seitenrand zum App-Katalog hinzu
Klicken Sie mit der rechten Maustaste auf die SharePoint-Add-in-Projekt, und klicken Sie auf veröffentlichen.

Geben Sie die **Client-ID** und ** Clientgeheimnis ** in Schritt 1 erstellt haben.

![](http://i.imgur.com/XpM9rwb.png)

Da Sie das Add-in debuggen möchten, müssen sicherstellen Sie, dass Sie https://localhost.com einschließlich des Ports, wie folgt angeben.
![](http://i.imgur.com/nQmSbPC.png)

Nun das Add-in in der App-Katalog-Website bereitstellen.

### <a name="step-5-install-your-add-in-in-your-developer-site-collection"></a>Schritt 5: Installieren der add-Ins in Ihrer Websitesammlung für Entwickler

Navigieren Sie zu der Entwicklerwebsite für und fügen Sie die app hinzu. Klicken Sie auf **App-Details**.
![](http://i.imgur.com/Aihr4r7.png)

Wenn Sie auf die Kachel app geklickt haben, müssen Sie auf klicken auf "**erfahren Sie, warum**" und Ihre app anfordern![](http://i.imgur.com/DwWUkG0.png)

Nachdem die Anforderung gesendet wurde werden der Status in aussteht, bis der SharePoint-Administrator oder den App-Katalog-Administrator die Anforderung genehmigt hat. Um die Anforderung zu genehmigen, navigieren Sie zu den app-Katalog, App-Anforderungen und Genehmigen der Anforderung.

![](http://i.imgur.com/yZ8vNEc.png)

Nachdem die Anforderung genehmigt wurde kann das Add-in jetzt installiert werden.

![](http://i.imgur.com/PMitOEY.png)

### <a name="step-6-debug-your-add-in"></a>Schritt 6: Debuggen von Ihr Add-in
In Visual Studio rechten Maustaste klicken Sie auf das Webprojekt, und wählen Sie neue Instanz **Debuggen** starten. Nach dem Start, navigieren Sie zu Ihrer Website, und starten Sie das Add-in.

![](http://i.imgur.com/Y5vAlDr.png)

>**HINWEIS**
> - Wenn aus irgendeinem Grund der app beim Ändern Verpacken müssen Sie es in der app-Katalog erneut bereitstellen und installieren es erneut mit Ihrer Websitesammlung für die Entwicklung
> - Wenn Sie add-Ins sind hat einen Appinstalled Ereignisempfänger, den Sie benötigen, um sicherzustellen, dass Sie Schritt 6 durchgeführt haben, bevor Sie Schritt 5


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>
- [Add-in-app nur Mandanten Administratorberechtigungen in SharePoint Online](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online)
- [Add-in-Berechtigungen in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp142383.aspx)
- [Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/fp179918.aspx)

