---
title: Anpassen von "modernen" Websiteseiten
description: "Benutzerdefiniertes branding in SharePoint Online verwenden, programmgesteuert \"moderne\" Seiten hinzufügen und hinzufügen, löschen oder Aktualisieren von Client-Side-Webparts auf \"modernen\" Seiten."
ms.date: 11/09/2017
ms.openlocfilehash: 28a6c8739d5ac47bb182f2fa5bc347c0dd3e947d
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="customizing-modern-site-pages"></a>Anpassen von "modernen" Websiteseiten

Im 2016 wurde die Erfahrung "modernen" Seite vom SharePoint-Team veröffentlicht. Websiteseiten modernen Team sind schnell, einfach zu Autor und unterstützen umfangreichen multimedia-Inhalt. Darüber hinaus Seiten auf jedem Gerät, das in einem Browser oder innerhalb großartige die mobile SharePoint-app. 

SharePoint-Seiten werden mit Webparts, erstellt, die Sie entsprechend Ihren Anforderungen anpassen können. Sie können Dokumente, Videos, Bilder, Website Aktivitäten, Yammer-Feeds und vieles mehr hinzufügen. Nur auswählen die + signieren, und wählen Sie einen Webpart aus der Toolbox Hinzufügens von Inhalt auf der Seite an. Das neue "hervorgehoben Inhalte" Webpart können Sie die Kriterien einrichten, damit bestimmte Inhalt automatisch und dynamisch in diesem Bereich der Seite wird. Mithilfe der SharePoint-Framework können Entwickler benutzerdefinierte Webparts, die nach oben rechts in der Toolbox anzeigen.

![](https://blogs.office.com/wp-content/uploads/2016/08/New-capabilities-in-SharePoint-Online-team-sites-including-integration-with-Office-365-Groups-1.gif)

Dieser Artikel befasst sich die Erweiterbarkeitsoptionen die Seite "modernen" wünschen. Allerdings erfahren Sie mehr über die Funktionen von "modernen" dieser Kommunikationskanäle angeboten, finden Sie unter [neue Funktionen in SharePoint Online Teamwebsites einschließlich Integration mit Office 365-Gruppen](https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups).

Im weiteren Verlauf des Artikels verwenden "modernen" für die neue Benutzeroberfläche und "klassische" für die ältere Benutzeroberfläche wir. 

> [!IMPORTANT]
> Wir sind nicht die "klassische" Erfahrung veralteter; "klassische" und "modernen" werden gleichzeitig verwendet werden.

## <a name="supported-customizations-for-modern-pages"></a>Unterstützte Anpassungen für "modernen" Seiten

Die Anzahl von Anpassungen für "modernen" Seiten verfügbar bleiben, in das Wachstum und in diesem Artikel, wir gebe Details und Beispiele für die unterstützten Optionen. SharePoint-Team ist funktionsfähig, um weitere Optionen in der Zukunft zu unterstützen. Die folgende Liste enthält einen schnellen Überblick über die unterstützten Funktionen für "modernen" Seiten:

 - Benutzerdefiniertes branding
 - Programmgesteuertes Hinzufügen von "modernen" Seiten
 - Hinzufügen, löschen und Aktualisieren von Client-Side-Webparts auf "modernen" Seiten
 - Alternative Layouts (siehe Hinweis auf *SharePoint virtuellen Summit*)

Für diese Anpassungen werden derzeit nicht für "modernen" Seiten unterstützt:

 - Hinzufügen von "klassische"-Webparts auf Seiten "modern"
 - Benutzerdefinierte CSS über AlternateCSSUrl Web-Eigenschaft
 - Benutzerdefiniertes JavaScript eingebettet über benutzerdefinierte Aktionen des Benutzers (siehe Hinweis auf *SharePoint-Framework-Erweiterungen*)
 - Benutzerdefinierte Masterseiten (umfangreichere branding wird unterstützt werden später mit alternativen)
 - Minimale Downloadstrategie (MDS)

> [!NOTE]
> - Es wird nicht empfohlen, "modernen" Seitenfunktionalität mit "klassische" SharePoint veröffentlichungsportale kombiniert. Standardmäßig ist die Seitenfunktionalität "modernen" auf "klassische" SharePoint veröffentlichungsportale nicht aktiviert.
> - Im Juni 2017, [SharePoint-Framework-Erweiterungen in Vorschau für Entwickler hinausgehen](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview). Dieser Erweiterungen der SharePoint-Framework verwenden, können Sie steuern, das Rendering eines Felds über den benutzerdefinierten Code, und Sie können benutzerdefinierte Aktionen, die Ihre benutzerdefinierten Code auszuführen, Benutzer erstellen. Finden Sie weitere Informationen finden Sie unter [Übersicht über SharePoint Framework Extensions](http://aka.ms/spfx-extensions). 
> - Im Mai 2017, während die virtuellen SharePoint-Summit angekündigt wir [kommunikationswebsites mit konfigurierbaren Seitenlayouts](https://blogs.office.com/2017/05/16/new-sharepoint-and-onedrive-capabilities-accelerate-your-digital-transformation/).  

<a name="themingimpact"> </a>
## <a name="custom-branding"></a>Benutzerdefiniertes branding

Verwenden eines benutzerdefinierten Designs Fall Ihrer Website wird dieses Design "modern" Seite Oberfläche wie im folgenden Beispiel dargestellt berücksichtigt.

*Abbildung 1. Moderne Seite mit benutzerdefinierten branding kommen aus Design-Einstellungen*

<img src="media/modern-experiences/modern-page-with-custom-theme.png" alt="Modern page with custom branding coming from theme settings" width="600">

<a name="sitesversusmodernpages"> </a>
## <a name="why-a-site-may-not-have-modern-pages-functionality"></a>Warum kann eine Website nicht "modernen" Seiten Funktionen zur Verfügung

"Modernen" Seiten werden übermittelt, mithilfe der Seiten der Website Webbereich-Funktion (B6917CB1-93A0-4B97-A84D-7CF49975D4EC), damit Wenn dieses Feature aktiviert wird, Ihre Website die Option hat "moderne" Seiten verwenden. Wenn Sie dieses Feature Microsoft gerollt, aktiviert wir dies für alle "modernen" Teamwebsites (Gruppe #0-Websites) und für die meisten "klassische" Teamwebsites (STS #0). 

Wäre eine Teamwebsite "klassische" eine große Anzahl von Webparts oder Wiki-Seiten, das Feature wurde nicht automatisch aktiviert, und das gleiche gilt für "klassische" Teamwebsites mit Features für die Veröffentlichung aktiviert. Wenn "modernen" Seitenfunktionalität auf diesen Websites werden soll, können Sie weiterhin das Seiten der Website-Feature aktivieren. Dies bedeutet auch, dass Websites basierend auf anderen Vorlagen nicht aktivierte "modernen" Seiten-Funktionalität verfügen. 

Der vorherige Absatz gesprochen zu wie das Feature "modernen" Seite für vorhandene Websites aktiviert wurde. Wenn Sie eine neue "Modern" oder "klassische" team Site (Gruppe #0 oder STS #0), "moderne" Seiten der Website-Feature wird bei der Bereitstellung Zeit aktiviert. Das "moderne" Seiten der Website-Feature ist nicht auf Websites aktiviert, die auf andere Vorlagen basieren.

<a name="configuremodernpages"> </a>
## <a name="configuring-the-end-user-experience"></a>Konfigurieren des Endbenutzers

Sie haben mehrere Optionen können Sie steuern, ob die Seite "modernen" oder "klassische" Erfahrung verwendet wird. 

### <a name="tenant-level-configuration"></a>Ebene Mandantenkonfiguration

Wenn Sie die "moderne" Erfahrung vollständig deaktivieren möchten, empfiehlt es sich mit dem Mandanten für diese Einstellung. Wechseln Sie zu Ihrem Mandanten Administrationscenter (beispielsweise Contoso-admin.sharepoint.com), wechseln Sie zu Einstellungen, und wählen Sie die "klassische" wünschen.

*Abbildung 2. Im Abschnitt Website-Seiten in der SharePoint-Mandanten bezogenen Einstellungen in Admin UI*

![Im Abschnitt Website-Seiten in der SharePoint-Mandanten bezogenen Einstellungen in Admin UI](media/modern-experiences/site-pages-setting-admin-ui.png)

> [!NOTE]
> - Die Einstellung der Mandant kann etwas verwirrend sein. **Verhindern, dass Benutzer Seiten der Website erstellen** werden tatsächlich die "klassische" wünschen.
> - Die aktuelle Konfiguration zwischengespeichert ist, und meldet sich ab sofort die Sitzung mit dem Effekt der von dieser Änderung.

### <a name="web-level-configuration"></a>Konfiguration der Web-Ebene

Sie können verhindern, dass eine Web mithilfe der Seite "modernen" Erfahrung durch das Webbereich Feature mit der ID **B6917CB1-93A0-4B97-A84D-7CF49975D4EC** deaktivieren (Name = "Seiten der Website"). Um die Seite "modernen" Erfahrung auf der Ebene der Webserver wieder zu aktivieren, müssen Sie das Feature wieder aktivieren.

Verwenden Sie die folgenden [Plug & Play-PowerShell](http://aka.ms/sppnp-powershell) So aktivieren oder deaktivieren Sie die erforderlichen Features:

```PowerShell
# Connect to a site
$cred = Get-Credential
Connect-PnPOnline -Url https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Prevent site pages at web level
Disable-PnPFeature -Identity B6917CB1-93A0-4B97-A84D-7CF49975D4EC -Scope Web 
# And again enable site pages at web
#Enable-PnPFeature -Identity B6917CB1-93A0-4B97-A84D-7CF49975D4EC -Scope Web 
```

> [!NOTE]
> Wenn Sie das Feature deaktivieren, können Sie nicht mehr neue "moderne" Seiten erstellen, aber die bereits erstellten Seiten arbeiten, verwenden die "modernen" Benutzeroberfläche bleiben. 

### <a name="commenting-configuration"></a>Kommentierung Konfiguration

Standardmäßig können Benutzer Kommentare (Juli 2017) auf "modernen" Seiten hinzufügen. Wenn Ihre Organisation dieses Feature nicht möchte, kann es über den Mandanten Administrationscenter auf der Seite Einstellungen deaktiviert werden.

*Abbildung 3. Aktivieren oder Deaktivieren der Kommentare*

![Aktivieren oder Deaktivieren der Kommentare](http://i.imgur.com/atl91Vh.png)

> [!NOTE]
> Können Sie auch programmgesteuert das Kommentare Verhalten mithilfe der Website verwalten und Mandanten-Level-APIs (erfordert SharePoint Client-Side Object Model 16.1.6621.1200 (CSOM) oder höher):
> - Microsoft.Online.SharePoint.TenantAdministration.SiteProperties.CommentsOnSitePagesDisabled 
> - Microsoft.SharePoint.Client.Site.CommentsOnSitePagesDisabled


## <a name="programming-modern-pages"></a>Programmieren von "modernen" Seiten

### <a name="adding-modern-pages"></a>Hinzufügen von "modernen" Seiten
Erstellen einer Seite "modernen" darum, Erstellen eines Listenelements in der Seitenbibliothek der Website und Zuweisen des richtigen Inhaltstyps in Kombination mit einige zusätzlichen Eigenschaften festlegen, wie im folgenden Codeausschnitt dargestellt:

```C#
// pagesLibrary is List object for the "site pages" library of the site
ListItem item = pagesLibrary.RootFolder.Files.AddTemplateFile(serverRelativePageName, TemplateFileType.ClientSidePage).ListItemAllFields;

// Make this page a "modern" page
item["ContentTypeId"] = "0x0101009D1CB255DA76424F860D91F20E6C4118";
item["Title"] = System.IO.Path.GetFileNameWithoutExtension("mypage.aspx");
item["ClientSideApplicationId"] = "b6917cb1-93a0-4b97-a84d-7cf49975d4ec";
item["PageLayoutType"] = "Article";
item["PromotedState"] = "0";
item["CanvasContent1"] = "<div></div>";
item["BannerImageUrl"] = "/_layouts/15/images/sitepagethumbnail.png";
item.Update();
clientContext.Load(item);
clientContext.ExecuteQuery();

```

<br/>

Wenn Sie Plug & Play-(seit der Version März 2017) verwenden, können Sie unsere Erweiterungsmethoden nutzen, erhalten Sie ein Modell für eine Seite auf einfache Weise hinzufügen:

```C#
cc.Web.AddClientSidePage("mypage.aspx", true);
```

> [!IMPORTANT]
> Ab September 2017, erstellte Seiten der `AddTemplateFile` Methode haben keine Vorschau, wenn Sie von der Suchergebnisseite darüber bewegen. Microsoft arbeitet an einem Fix/Alternative Lösung für dieses.

### <a name="using-the-pnp-support-for-modern-pages-and-client-side-web-parts"></a>Verwenden die Plug & Play-Unterstützung für "modernen" Seiten und clientseitige Webparts

Die März 2017-Version unterstützt die [Plug & Play-Websites core-Bibliothek](http://aka.ms/sppnp) erstellen, aktualisieren und Löschen von Seiten mithilfe der clientseitigen. In diesem Abschnitt finden Sie Informationen dazu, wie Sie mithilfe der clientseitigen-Seiten, die mithilfe der [Plug & Play-Websites core-Bibliothek auf GitHub](https://github.com/SharePoint/PnP-Sites-Core)entwickelt.

#### <a name="create-a-new-page-and-add-a-text-web-part"></a>Erstellen einer neuen Seite und Hinzufügen eines Text-Webparts

In diesem Beispiel erstellen eine neue Seite mithilfe der clientseitigen im Arbeitsspeicher wir, fügen Sie ein rich-Text-Editor-Steuerelement und schließlich die Seite in der Bibliothek für Seiten Website als mypage.aspx speichern. Im erste Schritt wird eine Instanz des ClientSidePage erstellen, und klicken Sie dann wir instanziieren Sie ein Steuerelement, das wir mithilfe von auf der Seite hinzufügen die `AddControl` Methode. Nachdem ausgeführt wurde, wird die Seite gespeichert.

```C#
// cc is the ClientContext instance for the site you're working with
ClientSidePage myPage = new ClientSidePage(cc);

ClientSideText txt1 = new ClientSideText() { Text = "PnP Rocks" };
myPage.AddControl(txt1, 0);
myPage.Save("mypage.aspx");
```

#### <a name="load-an-existing-page"></a>Laden Sie eine vorhandene Seite 

Wenn Sie ändern oder eine vorhandene Seite kopieren möchten, können Sie diese Seite in der Plug & Play-Client-seitigen Objektmodell laden; das Laden transformiert"" HTML-Inhalte Sie in ein Objektmodell, die Sie bearbeiten können. Laden eine vorhandene Seite erfolgt mithilfe der `Load` Methode.

```C#
// load the page with name "page3.aspx"
ClientSidePage p = ClientSidePage.Load(cc, "page3.aspx");

// perform your page updates
...

// save the page back to SharePoint
p.Save()
```

#### <a name="add-a-section"></a>Hinzufügen eines Abschnitts

Seiten können ein flexibles Layout haben. Sie können einen oder mehrere Abschnitte auf einer Seite hinzufügen, und diese Abschnitte können bis zu drei Spalten haben. Sie können mithilfe der SharePoint-Benutzeroberfläche von Abschnitten Seiten hinzufügen, oder können Sie dies programmgesteuert tun.

```C#
var page2 = cc.Web.AddClientSidePage("PageWithSections.aspx", true);
page2.AddSection(CanvasSectionTemplate.ThreeColumn, 5);
page2.AddSection(CanvasSectionTemplate.TwoColumn, 10);
```

#### <a name="add-an-out-of-the-box-web-part"></a>Hinzufügen eines Out-of-Box-Webparts 
Das folgende Beispiel zeigt, wie Sie ein Out-of-Box- **Bild** mithilfe der clientseitigen-Webpart auf einer Seite hinzufügen können. Beachten Sie, dass wir mithilfe von Webpart-Objekts Instanziieren der `InstantiateDefaultWebPart` -Methodenaufruf. Nachdem das Webpart gestartet wurde, sind die Standardeigenschaften im Webpart-Manifest definiert seine Eigenschaften fest. Für die meisten Webparts müssen Sie die Eigenschaften zu aktualisieren, wie in diesem Beispiel dargestellt.

```C#
ClientSidePage page5 = new ClientSidePage(cc);
var imageWebPart = page5.InstantiateDefaultWebPart(DefaultClientSideWebParts.Image);
imageWebPart.Properties["imageSourceType"] = 2;
imageWebPart.Properties["siteId"] = "c827cb03-d059-4956-83d0-cd60e02e3b41";
imageWebPart.Properties["webId"] = "9fafd7c0-e8c3-4a3c-9e87-4232c481ca26";
imageWebPart.Properties["listId"] = "78d1b1ac-7590-49e7-b812-55f37c018c4b";
imageWebPart.Properties["uniqueId"] = "3C27A419-66D0-4C36-BF24-BD6147719052";
imageWebPart.Properties["imgWidth"] = 1002;
imageWebPart.Properties["imgHeight"] = 469;
page5.AddControl(imageWebPart);
page5.Save("page5.aspx");

```

#### <a name="add-a-custom-client-side-web-part"></a>Hinzufügen eines benutzerdefinierten Webparts mithilfe der clientseitigen

Vorherigen Beispiele zum Arbeiten mit Webparts Out-of-Box ergab, aber Sie können auch Ihre benutzerdefinierte erstellt mithilfe der clientseitigen-Webparts zu einer Seite hinzufügen. Zunächst Abrufen Ihrer Webpart Informationen mithilfe der `AvailableClientSideComponents` -Methode, und suchen Sie nach Ihrem Web Teil, und verwenden Sie die Informationen zur Instanziierung finden Sie eine `ClientSideWebPart` -Instanz, die die Seite im letzten Schritt hinzugefügt wird.

```C#
ClientSidePage p = new ClientSidePage(cc);

// get a list of possible client side web parts that can be added
var components = p.AvailableClientSideComponents();

// Find our custom "HelloWord" web part
var myWebPart = components.Where(s => s.ComponentType == 1 && s.Name == "HelloWorld").FirstOrDefault();
if (myWebPart != null)
{
    // Instantiate a client side web part from our found web part information
    ClientSideWebPart helloWp = new ClientSideWebPart(myWebPart) { Order = 10 };
    // Add the custom client side web part to the page
    p.AddControl(helloWp);
}

// Persist the page to SharePoint
p.Save("PnPRocks.aspx");
```

#### <a name="adjust-control-order"></a>Reihenfolge Steuerelements anpassen
Sie haben verschiedene Methoden, um die Reihenfolge zu steuern, in der die Steuerelemente auf der Seite angezeigt werden. Der wichtige Aspekt ist die `Order` -Attribut für das aktuelle Steuerelement: die Liste der Steuerelemente wird durch den Wert der, die sortiert `Order` Attribut, wenn die HTML-Seite wird generiert, und die Reihenfolge, in der HTML-Code die Reihenfolge auch zur Seite Renderingzeit ist.

```C#
// Set the order when initiating the control
ClientSideText txt1 = new ClientSideText() { Text = "PnP Rocks", Order = 5 };

// Set the order when you add the control to the page, in this case we want the control to be the first
myPage.AddControl(txt1, -1);

// Manipulate the control order on the page...e.g. move a control to the back
myPage.Controls[1].Order = 10;

```

#### <a name="delete-a-control"></a>Löschen eines Steuerelements

Wenn Sie ein Steuerelement auf einer Seite löschen möchten, können Sie einfach Aufrufen der `Delete` Methode für das Steuerelement, und speichern Sie die Seite zurück.

```C#
ClientSidePage deleteDemoPage = ClientSidePage.Load(cc, "page3.aspx");
deleteDemoPage.Controls[0].Delete();
deleteDemoPage.Save();
```

#### <a name="delete-a-page"></a>Löschen einer Seite 

Schließlich können Sie eine Client-seitigen Seite löschen.

```C#
ClientSidePage p = ClientSidePage.Load(cc, "deleteme.aspx");
p.Delete();
```

#### <a name="class-model"></a>Klassenmodell

Die folgende Abbildung zeigt die wichtigsten Klassen, die, denen Sie beim Verwenden des Plug & Play-Client-seitigen Seite-Objektmodells mit arbeiten werden.

*Abbildung 4. Plug & Play-Client-seitigen Objektmodell*

![Plug & Play-Client-seitigen Objektmodell](media/pnpclientsideobjectmodel.png)

## <a name="additional-considerations"></a>Zusätzliche Überlegungen

Es werden weitere Optionen zur Anpassung der "modernen" Seiten wünschen schrittweise einzuführen. Diese Optionen werden mit der Veröffentlichung von SharePoint-Framework Zusatzfunktionen ausgerichtet. Derzeit keine genauen Zeitplan vorhanden ist, aber wir werden in den Artikeln "modernen" Erfahrung aktualisieren, sobald neue Funktionen freigegeben werden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Anpassen der „modernen“ Benutzeroberflächen in SharePoint Online](modern-experience-customizations.md)
- [Erlauben Sie oder verhindern Sie der Erstellung von modernen Websiteseiten durch Endbenutzer](https://support.office.com/en-us/article/Allow-or-prevent-creation-of-modern-site-pages-by-end-users-c41d9cc8-c5c0-46b4-8b87-ea66abc6e63b?ui=en-US&rs=en-US&ad=US)
