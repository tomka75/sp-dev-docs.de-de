---
title: Verwenden des Office 365 Content Delivery Network
ms.date: 1/11/2018
ms.prod: sharepoint
ms.assetid: 21ac1941-6a8b-4f33-8408-0c1f36295893
ms.openlocfilehash: f9d44f6dcb6cf21d9d273b6a469ae99e41d6d744
ms.sourcegitcommit: 9f492519d4eeb3f62a1fddc71cdca79263651a56
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="use-the-office-365-content-delivery-network-cdn"></a>Verwenden des Office 365 Content Delivery Network (CDN)

_**Gilt für:** Office 365_

Sie können statische Objekte im Office 365 Content Delivery Network (CDN) hosten, um eine bessere Leistung für Ihre SharePoint Online-Seiten zu ermöglichen. Statische Objekte sind Dateien, die nicht oft geändert werden, wie Bilder, Video und Audio, Stylesheets, Schriftarten und JavaScript-Dateien. Das CDN funktioniert als geografisch verteilter Cacheproxy, mit dem statische Objekte näher bei den anfordernden Browsern zwischengespeichert werden.

## <a name="office-365-cdn-basics"></a>Office 365 CDN-Grundlagen

Das Office 365 CDN ist in Ihrem SharePoint Online-Abonnement enthalten. Sie müssen nicht extra dafür bezahlen. Office 365 bietet Unterstützung für den privaten und öffentlichen Zugriff und ermöglicht Ihnen das Hosten statischer Objekte an mehreren Standorten oder Ursprüngen. Das Office 365 CDN ist nicht identisch mit dem Azure CDN. Wenn Sie weitere Informationen zu den Gründen für die Verwendung eines CDN oder zu allgemeinen CDN-Konzepten benötigen, finden Sie diese unter [Content Delivery Networks](https://support.office.com/de-DE/article/Content-delivery-networks-0140f704-6614-49bb-aa6c-89b75dcd7f1f).

## <a name="office-365-cdn-types"></a>Typen von Office 365 CDNs

Office 365 bietet zwei Typen von CDNs: öffentliches und privates CDN. Beide Optionen bieten eine Leistungsverbesserung, aber jede Option hat spezielle Attribute und Vorteile.

### <a name="office-365-public-cdn"></a>Öffentliches Office 365 CDN

![Diagramm zur Verwendung des öffentlichen Office 365 CDN](../images/o365-cdn-public-logical.png)

1. Der Administrator aktiviert das öffentliche Office 365 CDN für den Mandanten.
1. Statische Objekte, die vom CDN freigegeben werden sollen, werden in SharePoint-Bibliotheken hochgeladen, die als öffentliche CDN-Ursprünge aktiviert sind.
1. Objekte aus den konfigurierten Bibliotheken und Ordnern werden an den CDN-Dienst weitergegeben.
1. Auf den CDN-Speicherort verweisende URLs können auf SharePoint-Websites und in Anpassungen verwendet werden, die auf SharePoint-Seiten ausgeführt werden.

> [!NOTE]
> Sie sollten niemals Ressourcen, die in Ihrer Organisation als vertraulich gelten, in einer Dokumentbibliothek platzieren, die als öffentlicher CDN-Ursprung konfiguriert ist.

#### <a name="office-365-public-cdn-attributes-and-advantages"></a>Attribute und Vorteile des öffentlichen Office 365 CDN

- Objekte, die an einem öffentlichen Ursprung verfügbar gemacht werden, sind für jeden Benutzer anonym zugänglich.
- Wenn Sie ein Objekt aus einem öffentlichen Ursprung entfernen, ist es unter Umständen bis zu 30 Tage lang weiterhin über den Cache verfügbar. Links zu dem Objekt im CDN werden jedoch innerhalb von 15 Minuten ungültig.
- Wenn Sie Stylesheets (CSS-Dateien) an einem öffentlichen Ursprung hosten, können Sie im Code relative Pfade und URIs verwenden. Dies bedeutet, dass Sie auf den Speicherort von Hintergrundbildern und anderen Objekten relativ zum Speicherort des Objekts, das sie aufruft, verweisen können.
- Die URL eines öffentlichen Ursprungs kann zwar hartcodiert werden, dies wird jedoch nicht empfohlen. Der Grund hierfür ist folgender: Wenn der Zugriff auf das CDN nicht mehr verfügbar ist, wird die URL nicht automatisch auf Ihre Organisation in SharePoint Online aufgelöst, was zu fehlerhaften Links und anderen Fehlern führen kann. Daher wird empfohlen, SharePoint-URLs zu verwenden und die URL automatisch von SharePoint in die URL des öffentlichen CDN ändern zu lassen, wenn es aktiviert wird.
- Die standardmäßigen Dateitypen, die für öffentliche Ursprünge eingeschlossen werden, sind CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF. Sie können weitere Dateitypen angeben, indem Sie die CDN-Konfiguration ändern.
- Auf Wunsch können Sie eine Richtlinie konfigurieren, um Objekte auszuschließen, die mit von Ihnen angegebenen Websiteklassifizierungen festgelegt wurden. Beispielsweise können Sie alle Objekte ausschließen, die als „vertraulich“ oder „eingeschränkt“ gekennzeichnet sind, auch wenn sie einen zulässigen Dateityp haben und sich an einem öffentlichen Ursprung befinden.

### <a name="office-365-private-cdn"></a>Privates Office 365 CDN

![Diagramm zur Verwendung des privaten Office 365 CDN](../images/o365-cdn-private-logical.png)

1. Der Administrator aktiviert ein privates Office 365 CDN für den Mandanten.
1. Statische Objekte, die vom CDN freigegeben werden sollen, werden in SharePoint-Bibliotheken hochgeladen, die als private CDN-Ursprünge aktiviert sind.
1. Objekte aus den vorgesehenen privaten CDN-Ursprüngen werden an den CDN-Dienst verteilt.
1. Wenn Benutzer Seiten mit Objekten anfordern, die in einem CDN-Ursprung gespeichert sind, schreibt SharePoint automatisch die URL der Objekte in die CDN-URL um, sodass diese Objekte aus dem CDN bereitgestellt werden.
1. Für aus dem CDN bediente Objekte muss eine Hauptversion veröffentlicht werden, und Benutzer müssen über Zugriffsberechtigungen für diese Objekte verfügen, wenn das Umschreiben der URL erfolgt.

#### <a name="office-365-private-cdn-attributes-and-advantages"></a>Attribute und Vorteile des privaten Office 365 CDN

- Benutzer können nur auf die Objekte an einem privaten Ursprung zugreifen, wenn sie dazu berechtigt sind. Der anonyme Zugriff auf diese Objekte wird verhindert.
- Wenn Sie ein Objekt aus dem privaten Ursprung entfernen, ist es unter Umständen noch bis zu einer Stunde lang weiterhin über den Cache verfügbar. Links zu dem Objekt im CDN werden jedoch innerhalb von 15 Minuten ungültig.
- Die standardmäßigen Dateitypen, die für private Ursprünge eingeschlossen werden, sind GIF, ICO, JPEG, JPG, JS und PNG. Sie können weitere Dateitypen angeben, indem Sie die CDN-Konfiguration ändern.
- Ebenso wie bei öffentlichen Ursprüngen können Sie eine Richtlinie konfigurieren, um Objekte auszuschließen, die Sie mithilfe von eigens festgelegten Websiteklassifizierungen identifiziert haben, auch wenn Sie Platzhalter verwendet haben, um alle Objekte in einem Ordner oder einer Websitebibliothek einzuschließen.

### <a name="publishing-feature-auto-rewriting-to-cdn-urls"></a>Automatisches Umschreiben des Veröffentlichungsfeatures auf CDN-URLs

Damit Organisationen die Office 365 CDN-Funktionen ohne Update ihrer Portale nutzen können, wurde das SharePoint-Veröffentlichungsfeature so aktualisiert, dass URLs von in CDN-Ursprüngen gespeicherten Objekten automatisch in ihre CDN-Äquivalente umgeschrieben werden. Somit werden die Objekte dann vom CDN-Dienst statt von SharePoint bereitgestellt.

Es folgt eine Übersicht über die Links, die automatisch vom SharePoint-Veröffentlichungsfeature umgeschrieben werden:

- IMG/LINK/CSS-URLs in der HTML-Antwort klassischer Veröffentlichungsseiten
  - Dies schließt von Autoren im HTML-Inhalt einer Seite hinzugefügte Bilder ein.
  - Wenn Sie Seiten erweitern, können Sie das automatische Umschreiben von URLs auf einer Seite folgendermaßen vorübergehend deaktivieren:
    - Auschecken der Seite
    - Angeben des Abfragezeichenfolgenparameters `?NoAutoReWrites=true`
- WebPart-Objekte für Inhalt nach Suche
  - JavaScript-Dateien für Anzeigevorlagen
  - Bilder in Abfrageergebnissen – URLs in den folgenden standardmäßigen verwalteten Eigenschaften werden automatisch ersetzt: _PictureUrl_, _PictureThumbnailUrl_, _PublishingImage_
- Bild-URLs des Webparts „Bildbibliothek-Bildschirmpräsentation“
- Bildfelder in Ergebnissen der SPList-REST-API (RenderListDataAsStream)
  - Verwenden Sie die neue Eigenschaft „ImageFieldsToTryRewriteToCdnUrls“, um eine durch Trennzeichen getrennte Liste von Feldern bereitzustellen.
  - Unterstützt Linkfelder (Bild oder Link) und PublishingImage-Felder.
- SharePoint-Bildwiedergaben

## <a name="set-up-and-configure-the-office-365-cdn"></a>Einrichten und Konfigurieren des Office 365 CDN

Sie können das Office 365 CDN in Ihrem Mandanten mithilfe der SharePoint Online-Verwaltungsshell oder der Office 365 CLI einrichten und konfigurieren.

### <a name="set-up-and-configure-the-office-365-cdn-using-the-sharepoint-online-management-shell"></a>Einrichten und Konfigurieren des Office 365 CDN mithilfe der SharePoint Online-Verwaltungsshell

> [!NOTE]
> Bevor Sie Websitesammlungs-App-Kataloge in Ihrem Mandanten verwalten können, müssen Sie sicherstellen, dass Sie die [SharePoint Online-Verwaltungsshell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) installiert haben. Stellen Sie als Nächstes mit dem Cmdlet `Connect-SPOService` eine Verbindung mit Ihrem SharePoint Online-Mandanten her.

#### <a name="enable-office-365-cdn"></a>Aktivieren von Office 365 CDN

Sie können den Status des Office 365 CDN in Ihrem Mandanten mit dem Cmdlet [Set-SPOTenantCdnEnabled](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/set-spotenantcdnenabled?view=sharepoint-ps) verwalten.

Um das öffentliche Office 365 CDN in Ihrem Mandanten zu aktivieren, führen Sie Folgendes aus:

```powershell
Set-SPOTenantCdnEnabled -CdnType Public -Enable $true
```

Um das private Office 365 CDN in Ihrem Mandanten zu aktivieren, führen Sie Folgendes aus:

```powershell
Set-SPOTenantCdnEnabled -CdnType Private -Enable $true
```

Wenn Sie beide CDN-Typen verwenden möchten, können sie diese alternativ auch mit folgendem Befehl aktivieren:

```powershell
Set-SPOTenantCdnEnabled -CdnType Both -Enable $true
```

Wenn Sie nicht die standardmäßigen CDN-Ursprünge verwenden möchten, fügen Sie den Parameter `-NoDefaultOrigins` hinzu:

```powershell
Set-SPOTenantCdnEnabled -CdnType Both -Enable $true -NoDefaultOrigins
```

#### <a name="view-the-current-status-of-the-office-365-cdn"></a>Anzeigen des aktuellen Status des Office 365 CDN

Um zu überprüfen, ob der gewünschte Typ von Office 365 CDN aktiviert oder deaktiviert ist, verwenden Sie das Cmdlet [Get-SPOTenantCdnEnabled](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/get-spotenantcdnenabled?view=sharepoint-ps).

Um zu überprüfen, ob das öffentliche Office 365 CDN aktiviert ist, führen Sie Folgendes aus:

```powershell
Get-SPOTenantCdnEnabled -CdnType Public
```

#### <a name="view-office-365-cdn-origins"></a>Anzeigen der Office 365 CDN-Ursprünge

Um die derzeit konfigurierten öffentlichen Office 365 CDN-Ursprünge anzuzeigen, führen Sie Folgendes aus:

```powershell
Get-SPOTenantCdnOrigins -CdnType Public
```

#### <a name="add-office-365-cdn-origin"></a>Hinzufügen von Office 365 CDN-Ursprüngen

> [!NOTE]
> Sie sollten niemals Ressourcen, die in Ihrer Organisation als vertraulich gelten, in einer SharePoint-Dokumentbibliothek platzieren, die als öffentlicher CDN-Ursprung konfiguriert ist.

Verwenden Sie das Cmdlet [Add-SPOTenantCdnOrigin](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/add-spotenantcdnorigin?view=sharepoint-ps), um einen CDN-Ursprung zu definieren. Sie können mehrere Ursprünge definieren. Der Ursprung ist eine URL, die auf eine SharePoint-Bibliothek oder einen Ordner mit den Objekten verweist, die vom CDN gehostet werden sollen.

```powershell
Add-SPOTenantCdnOrigin -CdnType <Public | Private> -OriginUrl <path>
```

Dabei ist `path` der Pfad zu dem Ordner, der die Objekte enthält. Sie können Platzhalter zusätzlich zu relativen Pfaden verwenden.

Um alle Objekte in den Gestaltungsvorlagenkatalog aller Websites als öffentlichen CDN-Ursprung zu verwenden, führen Sie Folgendes aus:

```powershell
Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */masterpage
```

Um einen privaten Ursprung für eine bestimmte Websitesammlung zu konfigurieren, führen Sie Folgendes aus:

```powershell
Add-SPOTenantCdnOrigin -CdnType Private -OriginUrl sites/site1/siteassets
```

> [!NOTE]
> Nach dem Hinzufügen eines CDN-Ursprungs dauert es bis zu 15 Minuten, bis Sie Dateien mithilfe des CDN-Diensts abrufen können. Sie können überprüfen, ob ein bestimmter Ursprung bereits aktiviert wurde, indem Sie das Cmdlet [Get-SPOTenantCdnOrigins](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/get-spotenantcdnorigins?view=sharepoint-ps) ausführen.

#### <a name="remove-office-365-cdn-origin"></a>Entfernen von Office 365 CDN-Ursprüngen

Verwenden Sie das Cmdlet [Remove-SPOTenantCdnOrigin](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/remove-spotenantcdnorigin?view=sharepoint-ps) zum Entfernen eines CDN-Ursprungs für den angegebenen CDN-Typ.

Um einen Ursprung aus der Konfiguration des öffentlichen CDN zu entfernen, führen Sie Folgendes aus:

```powershell
Remove-SPOTenantCdnOrigin -CdnType Public -OriginUrl */masterpage
```

> [!NOTE]
> Das Entfernen eines CDN-Ursprungs wirkt sich nicht auf die in einer Dokumentbibliothek gespeicherten Dateien aus, die mit diesem Ursprung übereinstimmt. Wenn diese Objekte über ihre SharePoint-URL referenziert wurden, wechselt SharePoint automatisch wieder zur ursprünglichen URL, die auf die Dokumentbibliothek verweist. Wenn auf Objekte jedoch über die URL des öffentlichen CDN verwiesen wurde, sind diese Links jetzt ungültig und müssen manuell geändert werden.

#### <a name="modify-office-365-cdn-origin"></a>Ändern von Office 365 CDN-Ursprüngen

Es ist nicht möglich, einen vorhandenen CDN-Ursprung zu ändern. Stattdessen sollten Sie den zuvor definierten CDN-Ursprung mit dem Cmdlet `Remove-SPOTenantCdnOrigin` entfernen und mit dem Cmdlet `Add-SPOTenantCdnOrigin` einen neuen hinzufügen.

#### <a name="change-the-types-of-files-to-include-in-office-365-cdn"></a>Ändern der in Office 365 CDN einzuschließenden Dateitypen

Standardmäßig sind die folgenden Dateitypen im öffentlichen CDN enthalten: _CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF_. Wenn Sie weitere Dateitypen in das CDN einbeziehen müssen, können Sie die CDN-Konfiguration mit dem Cmdlet [Set-SPOTenantCdnPolicy](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/set-spotenantcdnpolicy?view=sharepoint-ps) ändern.

> [!NOTE]
> Durch das Ändern der Liste von Dateitypen überschreiben Sie die aktuell definierte Liste. Wenn Sie weitere Dateitypen einbeziehen möchten, verwenden Sie das Cmdlet [Get-SPOTenantCdnPolicies](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/get-spotenantcdnpolicies?view=sharepoint-ps), um herauszufinden, welche Dateitypen derzeit konfiguriert sind.

Um den Dateityp _JSON_ der Standardliste von Dateitypen im öffentlichen CDN hinzuzufügen, führen Sie Folgendes aus:

```powershell
Set-SPOTenantCdnPolicy -CdnType Public -PolicyType IncludeFileExtensions -PolicyValue "CSS,EOT,GIF,ICO,JPEG,JPG,JS,MAP,PNG,SVG,TTF,WOFF,JSON"
```

#### <a name="change-the-list-of-site-classifications-you-want-to-exclude-from-the-office-365-cdn"></a>Ändern der Liste von Websiteklassifizierungen, die Sie aus dem Office 365 CDN ausschließen möchten

Verwenden Sie das Cmdlet [Set-SPOTenantCdnPolicy](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/set-spotenantcdnpolicy?view=sharepoint-ps) -Cmdlet zum Ausschließen von Websiteklassifizierungen, die Sie nicht über das CDN zur Verfügung stellen möchten. Standardmäßig sind keine Websiteklassifizierungen ausgeschlossen.

> [!NOTE]
> Durch das Ändern der Liste der ausgeschlossenen Websiteklassifizierungen überschreiben Sie die aktuell definierte Liste. Wenn Sie zusätzliche Klassifizierungen ausschließen möchten, verwenden Sie das Cmdlet [Get-SPOTenantCdnPolicies](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/get-spotenantcdnpolicies?view=sharepoint-ps), um herauszufinden, welche Klassifizierungen derzeit konfiguriert sind.

Um als _HBI_ klassifizierte Websites aus dem öffentlichen CDN auszuschließen, führen Sie Folgendes aus:

```powershell
Set-SPOTenantCdnPolicy -CdnType Public -PolicyType ExcludeRestrictedSiteClassifications -PolicyValue "HBI"
```

#### <a name="disable-office-365-cdn"></a>Deaktivieren von Office 365 CDN

Um das Office 365 CDN zu deaktivieren, verwenden Sie das Cmdlet `Set-SPOTenantCdnEnabled`. Beispiel:

```powershell
Set-SPOTenantCdnEnabled -CdnType Public -Enable $false
```

### <a name="set-up-and-configure-the-office-365-cdn-using-the-office-365-cli"></a>Einrichten und Konfigurieren des Office 365 CDN mithilfe von Office 365 CLI

> [!NOTE]
> Damit Sie Websitesammlungs-App-Kataloge in Ihrem Mandanten verwalten können, müssen Sie sicherstellen, dass [Office 365 CLI](https://aka.ms/o365cli) installiert ist. Als Nächstes stellen Sie mit dem Befehl [spo connect](https://sharepoint.github.io/office365-cli/cmd/spo/connect/) eine Verbindung mit Ihrem SharePoint Online-Mandanten her.

#### <a name="enable-office-365-cdn"></a>Aktivieren von Office 365 CDN

Sie können den Status des Office 365 CDN in Ihrem Mandanten mithilfe des Cmdlets [spo cdn set](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-set/) verwalten.

Um das öffentliche Office 365 CDN in Ihrem Mandanten zu aktivieren, führen Sie Folgendes aus:

```sh
spo cdn set --type Public --enabled true
```

Um das private Office 365 CDN in Ihrem Mandanten zu aktivieren, führen Sie Folgendes aus:

```sh
spo cdn set --type Private --enabled true
```

#### <a name="view-the-current-status-of-the-office-365-cdn"></a>Anzeigen des aktuellen Status des Office 365 CDN

Um zu überprüfen, ob der betreffende Typ von Office 365 CDN aktiviert oder deaktiviert ist, verwenden Sie den Befehl [spo cdn get](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-get/).

Um zu überprüfen, ob das öffentliche Office 365 CDN aktiviert ist, führen Sie Folgendes aus:

```sh
spo cdn get --type Public
```

#### <a name="view-office-365-cdn-origins"></a>Anzeigen der Office 365 CDN-Ursprünge

Um die derzeit konfigurierten öffentlichen Office 365 CDN-Ursprünge anzuzeigen, führen Sie Folgendes aus:

```sh
spo cdn origin list --type Public
```

#### <a name="add-office-365-cdn-origin"></a>Hinzufügen von Office 365 CDN-Ursprüngen

> [!NOTE]
> Sie sollten niemals Ressourcen, die in Ihrer Organisation als vertraulich gelten, in einer SharePoint-Dokumentbibliothek platzieren, die als öffentlicher CDN-Ursprung konfiguriert ist.

Verwenden Sie den Befehl [spo cdn origin add](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-origin-add/) zum Definieren eines CDN-Ursprungs. Sie können mehrere Ursprünge definieren. Der Ursprung ist eine URL, die auf eine SharePoint-Bibliothek oder einen Ordner mit den Objekten verweist, die vom CDN gehostet werden sollen.

```sh
spo cdn origin add --type [Public | Private] --origin <path>
```

Dabei ist `path` der Pfad zu dem Ordner, der die Objekte enthält. Sie können Platzhalter zusätzlich zu relativen Pfaden verwenden.

Um alle Objekte in den Gestaltungsvorlagenkatalog aller Websites als öffentlichen CDN-Ursprung zu verwenden, führen Sie Folgendes aus:

```sh
spo cdn origin add --type Public --origin */masterpage
```

Um einen privaten Ursprung für eine bestimmte Websitesammlung zu konfigurieren, führen Sie Folgendes aus:

```sh
spo cdn origin add --type Private --origin sites/site1/siteassets
```

> [!NOTE]
> Nach dem Hinzufügen eines CDN-Ursprungs dauert es bis zu 15 Minuten, bis Sie Dateien mithilfe des CDN-Diensts abrufen können. Sie können überprüfen, ob der betreffende Ursprung bereits aktiviert wurde, indem Sie den Befehl [spo cdn origin list](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-origin-list/) verwenden.

#### <a name="remove-office-365-cdn-origin"></a>Entfernen von Office 365 CDN-Ursprüngen

Verwenden Sie den Befehl [spo cdn origin remove](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-origin-remove/), um einen CDN-Ursprung für den angegebenen CDN-Typ zu entfernen.

Um einen Ursprung aus der Konfiguration des öffentlichen CDN zu entfernen, führen Sie Folgendes aus:

```sh
spo cdn origin remove --type Public --origin */masterpage
```

> [!NOTE]
> Das Entfernen eines CDN-Ursprungs wirkt sich nicht auf die in einer Dokumentbibliothek gespeicherten Dateien aus, die mit diesem Ursprung übereinstimmt. Wenn diese Objekte über ihre SharePoint-URL referenziert wurden, wechselt SharePoint automatisch wieder zur ursprünglichen URL, die auf die Dokumentbibliothek verweist. Wenn auf Objekte jedoch über die URL des öffentlichen CDN verwiesen wurde, sind diese Links jetzt ungültig und müssen manuell geändert werden.

#### <a name="modify-office-365-cdn-origin"></a>Ändern von Office 365 CDN-Ursprüngen

Es ist nicht möglich, einen vorhandenen CDN-Ursprung zu ändern. Stattdessen sollten Sie den zuvor definierten CDN-Ursprung mit dem Befehl `spo cdn origin remove` entfernen und mit dem Befehl `spo cdn origin add` einen neuen hinzufügen.

#### <a name="change-the-types-of-files-to-include-in-office-365-cdn"></a>Ändern der in Office 365 CDN einzuschließenden Dateitypen

Standardmäßig sind die folgenden Dateitypen im CDN enthalten: _CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF und WOFF_. Wenn Sie weitere Dateitypen in das CDN einbeziehen müssen, können Sie die CDN-Konfiguration mit dem Befehl [spo cdn policy set](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-policy-set/) ändern.

> [!NOTE]
> Durch das Ändern der Liste von Dateitypen überschreiben Sie die aktuell definierte Liste. Wenn Sie weitere Dateitypen einbeziehen möchten, verwenden Sie den Befehl [spo cdn policy list](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-origin-list/), um herauszufinden, welche Dateitypen derzeit konfiguriert sind.

Um den Dateityp _JSON_ der Standardliste von Dateitypen im öffentlichen CDN hinzuzufügen, führen Sie Folgendes aus:

```sh
spo cdn policy set --type Public --policy IncludeFileExtensions --value "CSS,EOT,GIF,ICO,JPEG,JPG,JS,MAP,PNG,SVG,TTF,WOFF,JSON"
```

#### <a name="change-the-list-of-site-classifications-you-want-to-exclude-from-the-office-365-cdn"></a>Ändern der Liste von Websiteklassifizierungen, die Sie aus dem Office 365 CDN ausschließen möchten

Verwenden Sie den Befehl [spo cdn policy set](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-policy-set/) zum Ausschließen von Websiteklassifizierungen, die Sie nicht über das CDN zur Verfügung stellen möchten. Standardmäßig sind keine Websiteklassifizierungen ausgeschlossen.

> [!NOTE]
> Durch das Ändern der Liste der ausgeschlossenen Websiteklassifizierungen überschreiben Sie die aktuell definierte Liste. Wenn Sie zusätzliche Klassifizierungen ausschließen möchten, verwenden Sie den Befehl [spo cdn policy list](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-policy-list/), um herauszufinden, welche Klassifizierungen derzeit konfiguriert sind.

Um als _HBI_ klassifizierte Websites aus dem öffentlichen CDN auszuschließen, führen Sie Folgendes aus:

```sh
spo cdn policy set --type Public --policy ExcludeRestrictedSiteClassifications --value "HBI"
```

#### <a name="disable-office-365-cdn"></a>Deaktivieren von Office 365 CDN

Um das Office 365 CDN zu deaktivieren, verwenden Sie den Befehl `spo cdn set`. Beispiel:

```sh
spo cdn set --type Public --enabled false
```

## <a name="see-also"></a>Siehe auch

- [Verwenden des Office 365 Content Delivery Network mit SharePoint Online](https://support.office.com/de-DE/article/use-the-office-365-content-delivery-network-with-sharepoint-online-bebb285f-1d54-4f79-90a5-94985afc6af8)
- [Video zu den ersten Schritten mit Office 365 CDN](https://youtu.be/2kI2LnQ-3wQ?list=PLR9nK3mnD-OWSbg0o9a7mx_E7s2u7h_o2)