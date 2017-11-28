---
title: "SharePoint-Metadaten, die Websitenavigation und Veröffentlichung Websitefeatures"
ms.date: 11/03/2017
ms.openlocfilehash: 6917e097fd9b329d07ebfc82952150f30c63a8af
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/24/2017
---
# <a name="sharepoint-metadata-site-navigation-and-publishing-site-features"></a>SharePoint-Metadaten, die Websitenavigation und Veröffentlichung Websitefeatures

Verwenden Sie SharePoint Online-Metadaten-Management-Features, die Websitenavigation und Veröffentlichung Websitefeatures zur Unterstützung von SharePoint-Veröffentlichungswebsites.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

In diesem Artikel wird erläutert, wie zum Verwalten von Metadaten und Anpassen der Websitenavigation und Features von Websites in SharePoint Online mithilfe des Objektmodells-Add-in veröffentlichen. Dazu gehört auch Methoden zum Arbeiten mit gemeinsamen Web Programmiermuster und Bibliotheken für das SharePoint-Veröffentlichung der Websitebranding anpassen.

## <a name="key-metadata-navigation-and-publishing-terms-and-concepts"></a>Metadaten, Navigation und Veröffentlichung Begriffe und Konzepte

|**Begriff oder Konzept**|**Beschreibung und Anleitung**|
|:-----|:-----|
|Inhaltssuche-Webpart|Ein SharePoint-Webpart, das dynamische Suche Inhalte auf den Seiten in Möglichkeiten anzeigt, die Sie auf einfache Weise formatieren können. Weitere Informationen finden Sie unter: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://technet.microsoft.com/en-us/library/jj679900(v=office.15).aspx" target="_blank">Konfigurieren von Such-Webparts in SharePoint Server 2013</a></p></li><li><p><a href="https://support.office.com/en-us/article/Configure-a-Content-Search-Web-Part-in-SharePoint-0dc16de1-dbe4-462b-babb-bf8338c36c9a?CorrelationId=5024de0f-f4f4-436a-9c4a-b578b74b4764&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Konfigurieren eines Inhaltssuche-Webparts in SharePoint</a></p></li><li><p><a href="https://technet.microsoft.com/en-us/library/sharepoint-online-search-service-description.aspx" target="_blank">Suchfeatures in SharePoint Online</a></p></li></ul>|
|ContentTypeId|Eindeutiger Bezeichner der Inhaltstypen, die rekursiv sein sollen. Weitere Informationen finden Sie unter [ContentTypeId-Klasse](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.contenttypeid.aspx) (CSOM).|
|Inhaltstyp|Eine wieder verwendbare, zentrale Auflistung von Metadaten (Spalten), Workflow, Verhalten und andere Einstellungen für eine Kategorie von Informationen. Informationen finden Sie unter: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://msdn.microsoft.com/en-us/library/office/ms196085(v=office.14).aspx" target="_blank">Columns</a></p></li><li><p><a href="https://msdn.microsoft.com/en-us/library/office/ms460224(v=office.14).aspx" target="_blank">Erstellen von Inhaltstypen</a></p></li><li><p><a href="https://msdn.microsoft.com/en-us/library/office/ms468437(v=office.14).aspx" target="_blank">Benutzerdefinierte Informationen in Inhaltstypen</a></p></li></ul>|
|Inhaltstyphub|Teil der verwalteten Metadatendienstanwendung, also Hub-Standort, die für andere Websitesammlungen von Inhaltstypen veröffentlicht. Ermöglicht Ihnen das Veröffentlichen, veröffentlichen und Aufheben der Veröffentlichung von Inhaltstypen von einem zentralen Ort. Informationen finden Sie unter: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://support.office.com/en-us/article/Publish-a-content-type-from-a-content-publishing-hub-58081155-118d-4e7a-9cc5-d43b5dbb7d02?CorrelationId=49ebfe9f-6cf8-4f04-86a3-4d3fe23324fe&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Veröffentlichen eines Inhaltstyps aus einem Content publishing bereit</a></p></li><li><p><a href="https://support.office.com/en-us/article/View-error-logs-for-content-type-publishing-fa8bc6d4-f03e-4ce7-94de-5fd1c38fe32c?CorrelationId=3aaa4607-0888-417a-a0ff-8c1e44ce8167&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Anzeigen von Fehlerprotokollen für die Inhaltstyp-Veröffentlichung</a></p></li></ul>|
|Gerätekanäle|Eine Methode für das rendering Website Veröffentlichungsseiten verschiedene Arten mit unterschiedlichen Design, abzielen mehrere Geräte. Weitere Informationen finden Sie unter [wie: Hinzufügen ein Ausschnitts Gerät Channel Systemsteuerung in SharePoint 2013](http://msdn.microsoft.com/library/612780a8-6267-49f6-a32d-33600bb5f6b4%28Office.15%29.aspx).|
|Anzeigevorlage|Verwendet in Webparts, die suchtechnologie verwenden, werden Vorlagen-Steuerelement das Rendering der Ergebnisse von Abfragen an den Suchindex angezeigt. Anzeigevorlagen sind für alle Such-Webparts zur Verfügung. Weitere Informationen finden Sie unter [Anzeigen der vorlagenreferenz in SharePoint Server 2013](https://technet.microsoft.com/en-us/library/jj944947%28v=office.15%29.aspx).|
|Verwaltete Navigation|Bereitgestellt von SharePoint verwalteten Metadatendienst (Taxonomie) Websitenavigation. Verwenden sie zum Erstellen der Websitenavigation einer Taxonomie für verwaltete Metadaten abgeleitet. Verwalteter Navigation häufig funktioniert am besten mit dem Katalog.|
|Verwaltete Metadaten|Eine hierarchische Auflistung zentral verwalteter Begriffe, die Sie definieren und Attributtyp Elemente in SharePoint verwenden können. Verwalteten Metadaten zum Verwalten von Inhaltstyp-Veröffentlichung und Taxonomien erstellen können. In SharePoint 2013 und SharePoint Online, wird der verwaltete Metadatendienst verwendet, um die verwalteten Navigation erstellen&mdash;Sitenavigation bereitgestellt von Taxonomie. Weitere Informationen finden Sie unter: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://msdn.microsoft.com/en-us/library/office/bb897739(v=office.14).aspx" target="_blank">Anpassen von Navigationssteuerelementen und Anbietern in SharePoint Server 2010 (ECM)</a></p></li><li><p><a href="https://support.office.com/en-us/article/Introduction-to-managed-metadata-a180fa28-6405-4679-9ec3-81d2028c4efc?CorrelationId=2a4dbdb0-0199-40e2-ac58-568ca0a3f099&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Einführung in verwaltete Metadaten</a></p></li><li><p><a href="https://support.office.com/en-us/article/Introduction-to-managed-metadata-in-SharePoint-Server-2010-b324aebd-67ab-45a8-933d-ceedb2d909ea?CorrelationId=9152b80c-9fe4-43c5-bacc-178cc49d0e8f&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Einführung in verwaltete Metadaten in SharePoint Server 2010</a></p></li><li><p><a href="https://technet.microsoft.com/en-us/library/ee530393(v=office.14).aspx" target="_blank">Verwaltung verwalteter Metadaten (SharePoint Server 2010)</a></p></li><li><p><a href="http://msdn.microsoft.com/library/b66d4ec1-a2ef-49cc-8ca5-a6b516bff02e(Office.15).aspx" target="_blank">Verwaltete Metadaten und Navigation in SharePoint 2013</a></p></li><li><p><a href="http://msdn.microsoft.com/library/c9da5011-3c73-4b83-8e00-e7a03a71ed02(Office.15).aspx" target="_blank">Verwaltete Navigation in SharePoint 2013</a></p></li><li><p><a href="https://msdn.microsoft.com/en-us/library/office/hh147179(v=office.14).aspx" target="_blank">Migrieren von verwalteten Metadaten in SharePoint Server 2010</a></p></li></ul>|
|[Navigation namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.navigation.aspx)|Enthält Client Objektmodell (CSOM) Objektklassen, die Websitenavigation für Veröffentlichungswebsites unterstützen. |
|[Taxonomie-namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.aspx)|Enthält Klassen, CSOM, die Taxonomie Features unterstützen. Weitere Informationen finden Sie unter [Synchronize ausdrucksgruppen Beispiel SharePoint-Add-in](http://msdn.microsoft.com/library/76caa8e2-2a37-432c-8f98-9aa4acf86f79%28Office.15%29.aspx).|
|Anheften|Ähnlich wie in einen Ausdruckssatz wiederverwenden, verankern verwaltet eine freigegebene Beziehung zwischen der Quelle Begriff und die Wiederverwendung-Instanz. Beispielsweise kann die freigegebene Beziehung in allen Websitesammlungen in einem Cross-Site publishing-Szenario umfassen. Jederzeit der Begriff hinzugefügt oder entfernt wird, wird diese Aktion in der Hierarchie anywhere aktualisiert, die der Begriff fixiert ist. Weitere Informationen finden Sie unter [wie: Verwenden von Code zum Pin Begriffe im Zusammenhang mit Navigationsausdruck in SharePoint 2013 festgelegt](http://msdn.microsoft.com/library/4a2811dc-25fd-4eb2-b0ab-1edded64c556%28Office.15%29.aspx).|
|Produktkatalog|Informationen finden Sie unter den folgenden: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="http://msdn.microsoft.com/library/33f49e69-c1d3-4a6e-8887-5df683cba022(Office.15).aspx" target="_blank">Websiteübergreifende Veröffentlichung in SharePoint 2013</a></p></li><li><p><a href="https://technet.microsoft.com/en-us/library/jj656774(v=office.15).aspx" target="_blank">Konfigurieren der websiteübergreifenden Veröffentlichung in SharePoint Server 2013</a></p></li></ul>|
|Ausschnitt|Ein Teil der HTML-Funktionalität, die von den [Entwurfs-Manager](http://msdn.microsoft.com/library/29834b3f-3815-4347-91d3-296387663114%28Office.15%29.aspx)generierte HTML-Datei hinzugefügt werden können. Möglicherweise möchten beispielsweise Ihre Veröffentlichungsseite ein Bereich Gerätekanal hinzugefügt&mdash;ein Ausschnitt für diese vorhanden ist. In den folgenden Artikeln finden Sie einige Beispiele: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="http://msdn.microsoft.com/library/612780a8-6267-49f6-a32d-33600bb5f6b4(Office.15).aspx" target="_blank">Vorgehensweise: Hinzufügen ein Ausschnitts Gerät Channel Systemsteuerung in SharePoint 2013</a></p></li><li><p><a href="http://msdn.microsoft.com/library/7583b217-200c-4569-8f88-fe975c8ebd72(Office.15).aspx" target="_blank">Vorgehensweise: Hinzufügen ein Webpart-zonenausschnitts in SharePoint 2013</a></p></li><li><p><a href="http://msdn.microsoft.com/library/4beaab08-760b-408a-b768-906312779379(Office.15).aspx" target="_blank">Vorgehensweise: Hinzufügen ein Ausschnitts erhöhen, Sicherheit in SharePoint 2013</a></p></li></ul>|
|Strukturierte navigation|Informationen zur Verwendung von strukturierte Navigation finden Sie unter [Vorgehensweise: Anpassen von Navigation in SharePoint Server 2010 (ECM)](https://msdn.microsoft.com/en-us/library/office/ms558975%28v=office.14%29.aspx)|

## <a name="prerequisites-for-using-csom-to-brand-publishing-sites"></a>Erforderliche Komponenten für die Verwendung von CSOM zur Veröffentlichung von Websites mit Branding versehen

Standardmäßig ist die Webinhalte auf Öffentliche SharePoint lokalen Websites veröffentlicht für anonyme Benutzer verfügbar. Standardmäßig sind nicht CSOM und REST für anonyme Benutzer verfügbar.

**Wichtig:**  In diesem Szenario wird eine schwerwiegende Bedrohung für lokale SharePoint-Websites. Bevor Sie in [Use remote bereitstellen auf SharePoint-Seiten Marke](Use-remote-provisioning-to-brand-SharePoint-pages.md) beschriebene remote provisioning Modell zum Bereitstellen von branding zu Veröffentlichungssites verwenden, stellen Sie sicher, dass Ihre Website Sicherheit und Berechtigungen richtig eingestellt sind, und betrachten Sie die Sicherheit Auswirkungen der anonymen Zugriff.

Den Fall, dass der Standort-Administrator eine neue Webanwendung, die eine Websitesammlung enthält, die der Veröffentlichungsvorlage verwendet und lässt zu, anonymen Zugriff erstellt, werden anonymer Zugriff für alle Benutzer der Website verfügbar, wenn die Anwendung in hochgeladen wird der Katalog-Add-in. Da der anonyme Zugriff für die Veröffentlichung der lokale SharePoint-Website aktiviert ist, wenn ein Benutzer Vorgänge, die nicht authentifiziert ist zu der Website navigiert?

Wenn Sie ein SharePoint-Hosting-Add-in erstellen und ein Client-Add-in-Webparts zum Projekt hinzufügen, navigieren Sie zur **Zentraladministration** > **-Add-ins** > **Add-in - Katalog verwalten** und einen Katalog-Add-in für die Webanwendung erstellen, veröffentlichen das SharePoint-Hosting Add-in mit Visual Studio-Add-in-Paket zu erstellen und anschließendes Hochladen des Add-In-Pakets mit dem Katalog-Add-in. Zu diesem Zeitpunkt kann der Administrator der Websitesammlung das Add-in der Veröffentlichungswebsite hinzufügen. Das Add-in steht jetzt hinzufügen zu einer Seite auf der Veröffentlichungswebsite.

Wenn Sie die Hauptseite der Veröffentlichungswebsite bearbeiten und veröffentlichen Sie das Add-in hinzu, funktioniert das Add-in erwartungsgemäß. Auswählen des verknüpften Titels des Add-ins lädt ganzseitigen Benutzeroberfläche. Wenn SharePoint einen Fehler ausgelöst wird, bedeutet dies, dass der anonyme Benutzer keinen Zugriff auf das CSOM verwenden. Dies ist sinnvoll, da CSOM und REST nicht standardmäßig für anonyme Benutzer verfügbar sind.

### <a name="be-aware-that-disabling-use-remote-interfaces-permissions-can-introduce-a-security-risk"></a>Beachten Sie, dass das Deaktivieren von Berechtigungen Remoteschnittstellen verwenden kann ein Sicherheitsrisiko einführen

**Projektwebsite-Berechtigungen**ist das Kontrollkästchen **erfordern Remoteschnittstellen verwenden Berechtigung** standardmäßig aktiviert. Deaktivieren Sie das Kontrollkästchen **Berechtigung Remoteschnittstellen verwenden** , um anonymen Benutzern den Zugriff auf verwenden Sie CSOM und REST erlauben. Dies trennt den Benutzer aus Remoteschnittstellen verwenden-Berechtigungen, der den Benutzerzugriff SOAP, WebDAV und CSOM gewährt. Deaktivieren des Kontrollkästchens entfernt auch der Möglichkeit, SharePoint Designer verwenden.

Möglicherweise gibt es vorkommen, dass Sie die Möglichkeit zum Verwenden von SharePoint Designer, aber dennoch zulassen, dass die Verwendung von CSOM entfernen möchten. Das Kontrollkästchen **Berechtigung Remoteschnittstellen verwenden,** können Sie CSOM verwenden, ohne dass diese Remoteschnittstellen verwenden Berechtigungen verfügen anonyme Benutzer zu ermöglichen. Wenn das Kontrollkästchen **Berechtigung Remoteschnittstellen verwenden** deaktiviert ist, und wählen Sie den verknüpften Titel des Add-ins ganzseitigen Benutzeroberfläche geladen werden, auslöst SharePoint keine Fehler. Grundlegende Fehlerbehandlungscode wird in diesem Fall als anonymer Benutzer interpretiert.

**Vorsicht:**  
- Hinzufügen von apps öffentlich zugängliche SharePoint-Websites, die die Veröffentlichung verwenden Vorlage, deaktivieren Sie das Kontrollkästchen **Remoteschnittstellen verwenden Berechtigungen** in Websiteberechtigungen nicht. Aktivieren von CSOM für anonyme Benutzer zeigt eine mögliche potenzielles Sicherheitsrisiko??? Es divulges wesentlich mehr Informationen, als Sie erwarten würden. Andererseits sogar mit Zugriff auf die vollständige CSOM SharePoint-Berechtigungen weiterhin anwenden. Anonyme Benutzer werden nur sehen, Listen oder Elemente, die explizit verfügbar für anonyme Benutzer vorgenommen wurden. Mehr als sehen Sie auf der Webseite ist für anonyme Benutzer über CSOM und REST verfügbar.
- Sofern nicht unbedingt erforderlich ist, deaktivieren Sie das Kontrollkästchen **erfordern Remoteschnittstellen verwenden Berechtigung** nicht auf, wenn Berechtigungen für anonymen Zugriff auf eine lokale SharePoint-aktiviert sind Veröffentlichungswebsite. Dadurch können beide verfügbar gemacht werden kann veröffentlicht und Veröffentlichung nicht aufgehoben von Websiteinhalten für anonyme Benutzer und konnte lassen Sie Ihre Website zu einer Denial-of-Service-Angriff.

### <a name="use-the-viewformpageslockdown-feature"></a>Verwenden Sie die ViewFormPagesLockdown-Funktion

Um zu verhindern, dass Benutzer den Zugriff auf Formularseiten (beispielsweise Pages/Forms/AllItems.aspx) in einer SharePoint-Website öffentlich zugängliche, verwenden Sie das Feature **ViewFormPagesLockdown** . Es wurde entwickelt, um Benutzer daran zu hindern, erstellt von und geändert von Informationen einsehen können. Dieses Feature entfernt die Berechtigung zum **Anwendungsseiten anzeigen** oder **Remoteschnittstellen verwenden**. Wenn dieses Feature aktiviert ist, können nicht mit Pages/Forms/AllItems.aspx und Anzeigen von Elementen in dieser Bibliothek Benutzer wechseln.

Wenn CSOM und REST allen anonymen Benutzern zur Verfügung stehen&mdash; Wenn das Kontrollkästchen **Remoteschnittstellen verwenden Berechtigungen** deaktiviert ist&mdash;dann zwar diese Informationen **Erstellt von** und **Geändert von** im Browser immer noch nicht angezeigt wird, sie können Verwenden Sie CSOM oder REST Zugriff auf diese Informationen.

### <a name="security-trimming"></a>Aus Sicherheitsgründen

Durch Konfigurieren des anonymen Zugriffs für die Webanwendung aus, geben Sie die Richtlinie für anonymen Zugriff: _Schreiben verweigern&mdash;verfügt über keinen Schreibzugriff_ . Dies bedeutet, dass Benutzer mit anonymem Zugriff auf die Website schreiben können&mdash;auch mit CSOM oder REST Code. Anonyme Benutzer können nur die Informationen anzeigen, die Ihnen gewährt wurde, wenn der anonymer Zugriff auf die Website konfiguriert wurde.

Seiten nicht aufgehoben werden nicht für anonyme Benutzer standardmäßig angezeigt. Sie können nur Listen sehen, die den anonymen Zugriff aktivieren. 

**Wichtig:**  Wenn das Kontrollkästchen **Berechtigungen Remoteschnittstellen verwenden** deaktiviert ist, verwenden Sie das Modell der Berechtigungen und andere Vorsichtsmaßnahmen um sicherzustellen, dass anonyme Benutzer keinen Zugriff auf Dinge, die sie nicht sollte haben.

### <a name="prevent-denial-of-service-attacks"></a>Denial-of-Service-Angriffe zu verhindern, dass

Es ist kein Zwischenspeichern mit CSOM. Dies bedeutet, dass ein Angreifer Tausende von Elementen aus Listen gleichzeitig abgefragt werden kann und unter der Liste Ansicht Standardschwellenwert Kontaktpflege und belasten der SharePoint-Datenbank. Dadurch konnte verteilt und in einem ausgestattete Denial-of-Service-Angriffs ausweiten. 

### <a name="use-app-only-policy"></a>Nur-app Richtlinie verwenden

Nur-app Richtlinie können mit der Add-Ins vom Anbieter gehosteten nur-App-Richtlinie erlaubt das Add-in für Aktionen, die der aktuelle Benutzer nicht ist berechtigt, auszuführen. Beispielsweise kann ein Benutzer mit Schreibschutz Berechtigungen zum Schreiben in eine Liste wichtiger ein Add-in mit nur-app-Berechtigungen verwenden zum Schreiben in eine Liste.

Weitere Informationen finden Sie unter [Autorisierung und Authentifizierung von SharePoint-Add-ins](http://msdn.microsoft.com/library/bde5647a-fff1-4b51-b67b-2139de79ce4a%28Office.15%29.aspx) und [Grundlegendes zur Authentifizierung und Berechtigungen mit SharePoint-Add-ins und deaktiviert werden kann](http://channel9.msdn.com/Events/Build/2013/3-603) (Channel 9-Video).

### <a name="implement-ssl"></a>Implementieren von SSL

Wenn Sie das Add-in-Objektmodell verwenden, implementieren Sie das Protokoll Secure Sockets Layer (SSL) zum Verwalten der Sicherheit der Nachrichtenübermittlung im Internet. SSL funktioniert, indem die Remotewebsite, dass ein Zugriffstoken im HTTP-Header Autorisierung mit dem Wert Bearer "+" eine base64-codierte (nicht verschlüsselte) Zeichenfolge senden.

**Wichtig:**  SSL schützt Ihrer SharePoint-Veröffentlichungswebsite vor Angriffen, erhalten Sie auf Authentifizierungstoken und ausnutzen, zugreifen möchten.

## <a name="remote-provisioning-and-publishing-sites"></a>Remote-Bereitstellung und Veröffentlichen von Websites

Sie können [remote provisioning Methoden](Use-remote-provisioning-to-brand-SharePoint-pages.md) zum Bereitstellen von branding und anderen Anpassungen um SharePoint-Veröffentlichungswebsites bereitzustellen.

Veröffentlichungssites hängen davon ab, Inhaltstypen und **ContentTypeId**, die Inhaltstypen, um Seitenlayouts und Anzeigevorlagen verknüpft. Anpassen und Bereitstellen von SharePoint-Veröffentlichung Seiteninhalten hängt davon ab, diese Funktionalität. Andere Aspekte der benutzerdefinierten Veröffentlichungswebsite Verhalten, wie die verwalteten Metadatendienste und verwaltete Navigation der Bereitstellung **ContentTypeId** nicht abhängen und werden in CSOM vollständig unterstützt.

Andere publishing Site Anpassungsoptionen wie Gerätekanäle und Anzeigevorlagen, erfordern keine benutzerdefinierte CSOM. Sie hängen von Features, CSS und HTML-Entwurfs-Manager. Sie sind Anpassungen nach der Bereitstellung, die Sie neu erstellt und müssen nicht migriert.

## <a name="managed-metadata"></a>Verwaltete Metadaten

Verwaltete Metadaten-Funktion, die erstmals in SharePoint 2010, können Sie eine benutzerdefinierte Hierarchie zu definieren, oder Taxonomie, der Metadaten für die Verwendung in SharePoint-tags. Wenn Sie eine benutzerdefinierte Websitenavigation erstellen möchten, können Sie das Feature verwaltete Navigation der für verwaltete Metadaten-Infrastruktur erstellt wird.

Eine Taxonomie ist eine hierarchische Klassifizierung von Wörtern, Etiketten oder Begriffe, die basierend auf der Ähnlichkeit in Gruppen organisiert sind. Die kleinste Einheit in einer SharePoint-Taxonomie ist der Begriff. Ausdrücke können in Ausdruckssätze gruppiert werden. Ausdruckssätze können nach Affinität in Gruppen größeren gruppiert werden.

Eine kurze Einführung in die Taxonomie in SharePoint finden Sie [eine kurze Einführung in verwaltete Metadaten von Unternehmen in SharePoint 2010](https://msdn.microsoft.com/en-us/library/office/ee832800%28v=office.14%29.aspx) und [Einführung in verwaltete Metadaten in SharePoint 2010](https://support.office.com/en-us/article/Introduction-to-managed-metadata-in-SharePoint-Server-2010-b324aebd-67ab-45a8-933d-ceedb2d909ea?CorrelationId=2251ec3f-51ef-4924-89cc-d828b5068851&amp;ui=en-US&amp;rs=en-US&amp;ad=US).

SharePoint 2013 gehören neue APIs und Funktionen für die Featuregruppe für verwaltete Metadaten.

### <a name="managed-metadata-programming-model"></a>Verwaltete Metadaten-Programmiermodell

Für SharePoint 2013 ist die .NET Server Programmierbarkeitsmodell für verwaltete Metadaten in den folgenden Namespaces definiert: 

- [Taxonomie-namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.aspx)
    
- [ContentTypeSync-namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.contenttypesync.aspx)
    
- [Generische namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.generic.aspx)
    
- [CodeBehind-namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.om.codebehind.aspx)
    
- [Upgrade-namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.upgrade.aspx)
    
- [WebServices-namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.webservices.aspx)
    
Die entsprechenden CSOM Klassen befinden sich im Namespace [Client.Taxonomy-Namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.aspx) .

Im Gegensatz zu einigen anderen Bereichen des SharePoint-Objektmodells für verwaltete Metadaten besteht eine enge Beziehung zwischen den .NET Server programming Modellklassen und Member und die CSOM-Klassen und Member zwischen. Es folgen einige wichtige Unterschiede:

- CSOM unterstützt inhaltstypsynchronisierung nicht.
    
- Die **Gruppe** -Klasse, die Organisation in der [TermStore](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termstore.aspx) -Klasse die oberste Ebene darstellt, ist nur im Objektmodell von .NET Server verfügbar. Der entsprechenden CSOM ist die [TermGroup](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termgroup.aspx) -Klasse.
    
- [GroupCollection-Klasse](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.groupcollection.aspx), die eine Auflistung von Group-Objekte darstellt, ist nur im Objektmodell von .NET Server verfügbar. Der entsprechenden CSOM ist die [TermGroupCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termgroupcollection.aspx) -Klasse.
    
- CSOM enthält die [CustomPropertyMatchInformation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.custompropertymatchinformation.aspx) und [LabelMatchInformation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.labelmatchinformation.aspx) Klassen, die benutzerdefinierte Eigenschaft und Beschriftung Daten mit dem Server synchronisiert halten.
    
Die folgende Tabelle vergleicht Klassen in .NET Serverobjektmodell und dem CSOM-Objektmodell.

|**.NET Server-Objektmodell**|**Entsprechende CSOM-API**|
|:-----|:-----|
|[Microsoft.SharePoint.Taxonomy.ChangedGroup](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedgroup.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedGroup](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedgroup.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changeditem.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changeditem.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedItemCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changeditemcollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedItemCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changeditemcollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedItemType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changeditemtype.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedItemType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changeditemtype.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedOperationType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedoperationtype.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedOperationType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedoperationtype.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedSite](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedsite.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedSite](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedsite.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedTerm](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedterm.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedTerm](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedterm.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedTermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedtermset.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedTermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedtermset.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedTermStore](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedtermstore.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedTermStore](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedtermstore.aspx)|
|Nicht zutreffend|[Microsoft.SharePoint.Client.Taxonomy.ChangeInformation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changeinformation.aspx)|
|Nicht zutreffend|[Microsoft.SharePoint.Client.Taxonomy.CustomPropertyMatchInformation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.custompropertymatchinformation.aspx)|
|[Microsoft.SharePoint.Taxonomy.FeatureIds](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.featureids.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.Group](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.group.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.HiddenListFullSyncJobDefinition](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.hiddenlistfullsyncjobdefinition.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.ImportManager](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.importmanager.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.Label](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.label.aspx)|[Microsoft.SharePoint.Client.Taxonomy.Label](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.label.aspx)|
|[Microsoft.SharePoint.Taxonomy.LabelCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.labelcollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.LabelCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.labelcollection.aspx)|
|Nicht zutreffend|[Microsoft.SharePoint.Client.Taxonomy.LabelMatchInformation]()|
|[Microsoft.SharePoint.Taxonomy.MobileTaxonomyField](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.mobiletaxonomyfield.aspx)|[Microsoft.SharePoint.Client.Taxonomy.MobileTaxonomyField](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.mobiletaxonomyfield.aspx)|
|[Microsoft.SharePoint.Taxonomy.StringMatchOption](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.stringmatchoption.aspx)|[Microsoft.SharePoint.Client.Taxonomy.StringMatchOption]()|
|[Microsoft.SharePoint.Taxonomy.TaxonomyField](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfield.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomyField](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.stringmatchoption.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyFieldControl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfieldcontrol.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.TaxonomyFieldEditor](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfieldeditor.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.TaxonomyFieldValue](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfieldvalue.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomyFieldValue](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.taxonomyfieldvalue.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyFieldValueCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfieldvaluecollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomyFieldValueCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.taxonomyfieldvaluecollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyitem.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomyItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.taxonomyitem.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyItemPicker](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyitempicker.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.TaxonomyRights](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyrights.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.TaxonomySession](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomysession.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomySession](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.taxonomysession.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyWebTaggingControl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomywebtaggingcontrol.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.Term](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.term.aspx)|[Microsoft.SharePoint.Client.Taxonomy.Term](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.term.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termcollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termcollection.aspx)|
|Nicht zutreffend|[Microsoft.SharePoint.Client.Taxonomy.TermGroup](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termgroup.aspx)|
|Nicht zutreffend|[Microsoft.SharePoint.Client.Taxonomy.TermGroupCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termgroupcollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermProperty](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termproperty.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.TermPropertyToolPart](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termpropertytoolpart.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.TermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termset.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termset.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermSetCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termsetcollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermSetCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termsetcollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermSetItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termsetitem.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermSetItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termsetitem.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermStore](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termstore.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermStore](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termstore.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermStoreCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termstorecollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermStoreCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termstorecollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermStoreOperationException](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termstoreoperationexception.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Taxonomy.TreeControl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.treecontrol.aspx)|Nicht zutreffend|

## <a name="page-layouts"></a>Seitenlayouts

Für Veröffentlichungssites definiert das Seitenlayout das Layout einer bestimmten Klasse von Seiten. Darüber hinaus definiert die anpassbare Bereiche einer Seite mit Inhaltsplatzhaltern von Inhalt aus übereinstimmenden Regionen auf Seitenlayouts ausgefüllt werden. Seitenlayouts basieren auf eines benutzerdefinierten Inhaltstyps in der Regel. Inhaltstypen definieren benutzerdefinierter Inhaltsfelder, die auf einer Seite angezeigt werden soll. In der Regel Erstellen eines benutzerdefinierten Inhaltstyps, das Felder enthält, die den Seitenentwurf Sie zugeordnet sind, oder Ihr Entwicklungsteam hatte zuvor geplanten.

Benutzerdefinierte Feldsteuerelemente können Text, Bilder, Video oder andere Arten von Inhalt enthalten. SharePoint bietet Inhaltstypen, Artikel, Katalog, Willkommensseite und vieles mehr. Die Seite Layout Inhaltstypen zugreifen, indem Sie zu **Websiteeinstellungen** > **Websiteinhaltstypen**. Diese Standardseitenlayout Content-Typen verwendet werden können, wie das übergeordnete Inhaltstypen für eine benutzerdefinierte Inhalte, die Geben Sie erstellen möchten.

Alle Seite Layout Inhaltstypen erben von Inhaltstyp. Nach der Erstellung eines benutzerdefinierten Inhaltstyps zeigt SharePoint Spalten, die der neue Inhaltstyp vom Inhaltstyp Seite geerbt. Sie können neue benutzerdefinierte Felder darstellen, die Sie in das Seitenlayout anzeigen möchten, um neue Websitespalten hinzufügen. Geben Sie für jede Websitespalte an. Ein Typ ist ein Wert wie "eine Textzeile" oder "Vollständiger HTML". Berücksichtigen Sie Faktoren wie der Grad der Descriptiveness oder -Steuerelement, das der Benutzer mit dem Feld verfügen soll, wenn Sie dieses Typs angeben.

Nachdem Sie alle Felder, die den Inhalt in das Seitenlayout speichern erstellen, können Sie das Seitenlayout im Entwurfs-Manager erstellen. Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx). Nachdem Sie das Seitenlayout erstellen, indem Sie auf **Websiteeinstellungen**veröffentlichen > **Masterseiten und Seitenlayouts**. Eine HTML-Datei und eine ASPX-Datei sind vorhanden. Die HTML-Datei ist das Master-Shape, und Sie können einen beliebigen HTML-Editor bearbeiten. Nachdem Sie die Datei speichern und veröffentlichen, Entwurfs-Manager enthält Änderungen und konvertiert die aktualisierte HTML-Datei in aspx-Format dar, die SharePoint zum Rendern der Seite verwendet wird. Um das Seitenlayout zu veröffentlichen, wählen Sie die HTML-Datei aus, und wählen Sie **Veröffentlichen** im Menüband.

Um eine Seite basierend auf dem neuen Layout zu erstellen, wechseln Sie zur **Neuen Seite** > **Seite** > **Seitenlayouts** , um das neue Seitenlayout in der Liste der verfügbaren Seitenlayouts finden Sie unter. Wenn Sie das neue Seitenlayout auswählen, sollte Sie alle neuen Felder angezeigt werden, die Sie beim Erstellen eines neuen Inhaltstyps für das neue Seitenlayout angegeben. Wenn Sie die Seite anzeigen und der HTML-Code wird nicht die Möglichkeit, die Sie erwarten rendern, können Sie den HTML-Code bearbeiten und dann Entwurfs-Manager verwenden, um die aktualisierte Datei hochzuladen.

## <a name="site-navigation"></a>Der Websitenavigation

Es gibt vier Arten von der Websitenavigation: 

- Globale navigation
    
- Lokale navigation
    
- Strukturierte navigation
    
- Verwaltete Navigation
    
Globale Navigation bezieht sich auf Navigationselemente, mit denen Benutzer aus einer SharePoint-Website in eine andere verschieben. Lokale Navigation bezieht sich auf die Navigation in einer SharePoint-Website. Strukturierte und verwaltete Navigation sind etwas komplizierter.

### <a name="structured-navigation"></a>Strukturierte navigation

Strukturierte Navigation ist eine statische Vorgehensweise zum Implementieren der Navigation in SharePoint-Websites. Es entspricht normalerweise des Unternehmens-Struktur, die Umstrukturierung der SharePoint-Websitenavigation erfordert. Neustrukturierung von Arbeit häufig bedeutet Unterwebsites und/oder Seiten verschieben und Aktualisieren von Links zu auf neue Ziele zeigen.

Strukturierte Navigation Ursachen für relativ flachen, flache Websitestrukturen ausreichend Wenn Ihr Unternehmen Struktur (und damit der Websitestruktur) für längere Zeit stabil ist. Für tiefer und komplexere Websitestrukturen und Unternehmen beim Veröffentlichen von Website Navigationsstrukturen, die erweitern und dynamisch ändern müssen, möglicherweise verwalteter Navigation Kontaktpersonen. Weitere Informationen zur strukturierte Navigation finden Sie unter [Vorgehensweise: Anpassen von Navigation in SharePoint Server 2010](https://msdn.microsoft.com/en-us/library/office/ms558975%28v=office.14%29.aspx).

### <a name="managed-navigation"></a>Verwaltete Navigation

Verwalteter Navigation basiert auf der Website und Taxonomie-Infrastruktur veröffentlichen Core. Verwalteter Navigation für eine einzelne Websitesammlung gebunden ist. Definieren Sie globale und lokale Navigation verwendet Ausdruckssätze und Ausdrücke. Beispielsweise können Sie erstellen einen Ausdruckssatz, der globalen Navigation insgesamt definiert, und fügen Sie Ausdrücke zu diesem Ausdruckssatz für bestimmte Navigationselemente in der globalen Navigation.

Weitere Informationen zur verwalteten Navigation finden Sie in den folgenden Artikeln:

- [Verwaltete Navigation in SharePoint 2013](http://msdn.microsoft.com/library/c9da5011-3c73-4b83-8e00-e7a03a71ed02%28Office.15%29.aspx)
    
- [Übersicht über die verwaltete Navigation in SharePoint Server 2013](https://technet.microsoft.com/en-us/library/dn194311%28v=office.15%29.aspx)
    
Es folgen einige wichtige allgemeine Punkte zu Klassen, Methoden und Eigenschaften in der SharePoint-Navigationsmodell Erweiterbarkeit für Veröffentlichungssites:

-  **NavigationTerm** und **NavigationTermSet** Klassen hinzufügen, Eigenschaften und Methoden, die für die verwaltete Navigation spezifisch sind. Zusätzliche Zustand wird in die **CustomProperties** -Eigenschaft der **NavigationTerm** -Klasse gespeichert.
    
-  **NavigationTerm** und **NavigationTermSet** Klassen haben zwei Modi: bearbeitet werden, und schreibgeschützt. Im Objektmodell .NET Server werden **NavigationTerm** -Objekte in der Taxonomie Navigation Cache gespeichert, die nur von Funktionen in der statischen **TaxonomyNavigation** -Klasse zugegriffen werden kann.
    
-  **PortalSiteMapNodeProvider** -Objekte im Objektmodell von .NET Server bieten eine Schnittstelle zwischen dem datengesteuerten Navigation Websitefeatures und Website Zuordnen von Datenquellen. In der Regel schreiben Sie eine benutzerdefinierte Knoten Websiteübersichtsanbieter zum Speichern von Siteübersichten in eine XML-Datei oder ein Datenformat, die standardmäßig von SharePoint nicht unterstützt wird.
    
CSOM umfasst einige eindeutige Klassen und Enumerationen:

- Die **NavigationLinkType** -Enumeration definiert den Typ des Navigationsknotens in einer Navigationsstruktur. Sie können einen Knoten als Stammknoten, eine benutzerfreundliche URL oder einen standard Link angeben.
    
- Die **StandardNavigationScheme** -Aufzählung identifiziert die Navigation als lokal oder global.
    
- Die **StandardNavigationSource** -Enumeration umfasst drei Optionen für die globale Navigation und lokale Navigation. Jede Auswahl stellt einen Zustand, der die die Konfiguration der zugrunde liegenden Anbieter entspricht.
    
- Die **StandardNavigationSettings** -Klasse verwaltet die globale und lokale Navigation Farbschemas.
    
Die folgende Tabelle enthält die Veröffentlichung Navigation Klassen in den Objektmodus von Server und die entsprechenden CSOM.

|**Serverobjektmodell**|**CSOM**|
|:-----|:-----|
|[Microsoft.SharePoint.Publishing.Navigation.CachedObjectSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.cachedobjectsitemapnode.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationComparer](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationcomparer.aspx)|Nicht zutreffend|
|Nicht zutreffend|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationLinkType](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.navigationlinktype.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationTerm](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationterm.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTerm](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.navigation.navigationterm.aspx)|
|Nicht zutreffend|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTermCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.navigation.navigationtermcollection.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationTermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationtermset.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTermSet](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.navigationtermset.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationTermSetItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationtermsetitem.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTermSetItem](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.navigationtermsetitem.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationTermSetView](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationtermsetview.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTermSetView](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.navigationtermsetview.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.PortalHierarchicalDataSourceView](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalhierarchicaldatasourceview.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalHierarchicalEnumerable](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalhierarchicalenumerable.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalHierarchyData](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalhierarchydata.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalListItemSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portallistitemsitemapnode.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalListSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portallistsitemapnode.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalNavigation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalnavigation.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalSiteMapDataSource](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalsitemapdatasource.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalSiteMapDataSourceSwitch](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalsitemapdatasourceswitch.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portallistsitemapnode.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalSiteMapProvider](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalsitemapprovider.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.PortalWebSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalwebsitemapnode.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.ProxySiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.proxysitemapnode.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.SiteNavigationSettings](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.sitenavigationsettings.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.SiteNavigationSettingsWriter](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.sitenavigationsettingswriter.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.SPNavigationSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.spnavigationsitemapnode.aspx)|Nicht zutreffend|
|Nicht zutreffend|[Microsoft.SharePoint.Client.Publishing.Navigation.StandardNavigationSource](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.standardnavigationsource.aspx)|
|Nicht zutreffend|[Microsoft.SharePoint.Client.Publishing.Navigation.StandardNavigationSettings](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.standardnavigationsettings.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomyNavigation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomynavigation.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.TaxonomyNavigation](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.taxonomynavigation.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomyNavigationCacheConfig](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomynavigationcacheconfig.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomyNavigationCacheStatistics](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomynavigationcachestatistics.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomyNavigationContext](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomynavigationcontext.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomysitemapnode.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapProvider](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomysitemapprovider.aspx)|Nicht zutreffend|
|[Microsoft.SharePoint.Publishing.Navigation.WebNavigationSettings](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.webnavigationsettings.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.WebNavigationSettings](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.webnavigationsettings.aspx)|

## <a name="publishing-site-features"></a>Website-Veröffentlichungsfeatures

SharePoint 2013 und SharePoint Online enthalten einige Features, die spezifisch für SharePoint-Veröffentlichungswebsites sind:

- Gerätekanäle können Sie einen einzelnen publishing Site Entwurf an mehrere Geräte und Browser anwenden.
    
- Anzeigevorlagen ermöglichen von Branding und die Darstellung des Webparts suchbezogene anpassen.
    
- Bilddarstellungen definieren Sie die Dimensionen, die zum Anzeigen von Bildern auf den Seiten in SharePoint 2013-Veröffentlichungswebsites verwendet werden.
    
Sie können diese Features mithilfe der Klassen im Namespace des CSOM-Programmiermodells [Publishing](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.aspx) implementieren.

### <a name="device-channels-and-device-channel-panels"></a>Gerätekanäle und gerätekanalbereiche

Gerätekanäle und gerätekanalbereiche können Sie die Website für Mobiltelefone und Tablets optimieren. Erstellen einen eindeutigen Kanal für jedes Gerät, den Sie als Ziel möchten, können Sie eine SharePoint-Veröffentlichungswebsite in mehr als eine Art Rendern. Sie können eine einzelne Website einmal erstellen und dann ordnen Sie die Website und seinen Inhalt verschiedene Gestaltungsvorlagen und Stylesheets auf verschiedene Ziele aufzunehmen.

Erstellen von Kanälen mithilfe des [Entwurfs-Manager](http://msdn.microsoft.com/library/29834b3f-3815-4347-91d3-296387663114%28Office.15%29.aspx). Nachdem Sie einen Kanal erstellen, ordnen sie das mobile Gerät oder den Browser mit der Benutzer-Agent-Zeichenfolge des eingehenden Geräts.

Ein Gerät kann mehrere Kanäle angehören. In diesem Fall können Sie Kanäle rank, wenn ein Gerät gehört. Angenommen, wenn Sie einen Kanal für Smartphones und einen Kanal für ein bestimmtes Gerätekonfiguration erstellen, können Sie die Kanäle einstufen, sodass Geräte mit der Workflowkonfiguration den DDE-Kanal für diese rufen und alle anderen Smartphones den DDE-Kanal Smartphones.

Sie können bis zu 10 Kanäle (einschließlich des Standard-Kanals) im Entwurfs-Manager erstellen. Der Standardkanal erfasst alle Datenverkehr nicht durch eine der anderen Kanäle abgefangen wird. Wenn Sie einen neuen Kanal erstellen, füllen Sie die Felder, die in der folgenden Tabelle aufgeführt.

|**Feld**|**Erforderlich oder optional?**|**Beschreibung**|
|:-----|:-----|:-----|
|Name|Erforderlich|Identifiziert den Kanal, um es von anderen unterscheiden.|
|Kanal-alias|Erforderlich|Wie Code, der Abfragezeichenfolgen, Cookies oder Gerätekanalbereiche Unterschiede zwischen Kanäle unterscheiden.|
|Gerät Inklusion Regeln|Erforderlich|Die Benutzer-Agent-Teilzeichenfolgen, die leiten Sie Anforderungen von Geräten (jeweils sollte in einer anderen Zeile sein).|
|Beschreibung|Optional|Beschreibt die Funktionsweise dieser Kanal.|
|Active|Optional|Wenn diese Option aktiviert ist, verwendet der DDE-Kanal verwandten Ressourcen für den DDE-Kanal, um Datenverkehr zu leiten. Andernfalls die Abfragezeichenfolge `?DeviceChannel=<alias>` zeigt eine Vorschau die Website im Kanal.|
 **Gerätekanalbereiche**

Nachdem Gerätekanäle erstellt wurde, ordnen Sie eine Gestaltungsvorlage jedem Befehl die EINGABETASTE. Da Gestaltungsvorlage Anpassungen selten geworden sind, ist dies häufig die Standardgestaltungsvorlage (seattle.master). Wenn Sie eine eindeutige Masterseite für eine oder mehrere Gerätekanäle erstellen, können Sie die verschiedene CSS-Datei als die Masterseite für die Standardkanal verweisen. Seitenlayouts, die Sie erstellen werden alle Kanäle entwickelt, die Sie erstellen. Das Gerät Channel Panel-Steuerelement können Sie die um Seite Layout Entwürfe zwischen Kanälen zu unterscheiden.

Weitere Informationen finden Sie unter [SharePoint 2013 Design Manager Gerätekanäle](http://msdn.microsoft.com/library/a924bd7b-a5e3-41bf-b0a7-3e43945fa951%28Office.15%29.aspx).

Der Gerät Channel-Bereich ist ein Container-Steuerelement, das einen oder mehrere Kanäle zugeordnet ist. Sie können ein Gerät Channel Panel-Steuerelement, einem Seitenlayout hinzufügen, und wird die Systemsteuerung steuern, welche Inhalte in den einzelnen Kanälen gerendert wird. Wenn eine oder mehrere dieser Kanäle aktiv sind, wenn die Seite gerendert wird, werden alle Inhalte des Bereichs Channel Gerät gerendert. Verwenden Sie die Gerät Channel-Systemsteuerung, wann bestimmte Inhalte für eine oder mehrere bestimmte Kanäle enthalten soll.

Berücksichtigen Sie ein Seitenlayout, die zehn Felder enthält. Einige dieser Felder stehen alle Kanäle, und einige nur in bestimmten Kanälen gerendert werden soll. Angenommen Sie, ein mobiler Banner Kopfzeilenfeld, die nur auf Smartphones oder einer großen benutzerdefinierten Randleiste, die nur auf Desktops und Tablets rendert rendert.

Die Gerät Channel Systemsteuerung können auch der Format- und Platzierung des Inhalts auf einer Seite durch Hinzufügen von DDE-Kanal-spezifischen CSS ändern. Weitere Informationen finden Sie unter [wie: Hinzufügen ein Ausschnitts Gerät Channel Systemsteuerung in SharePoint 2013](http://msdn.microsoft.com/library/612780a8-6267-49f6-a32d-33600bb5f6b4%28Office.15%29.aspx) und [wie: Branding von Ausschnitten mit CSS in SharePoint 2013](http://msdn.microsoft.com/library/d18d07b6-1a6b-4589-a65c-932b67cef595%28Office.15%29.aspx).

**Benutzer-Agent Zeichenfolgen und Gerätekanäle**

Eine Zeichenfolge des Benutzer-Agent ist eine kleine Zeichenfolge mit Daten, die den Browser identifiziert. Diese Informationen kann an den Server gesendet werden, die den Benutzer-Agent identifiziert. Gerätekanäle weisen eine Anforderung an einen entsprechenden Gerätekanal basierend auf dem Benutzer-Agent-Zeichenfolge (oder Teilzeichenfolgen) der Benutzer ist Durchsuchen des Geräts (oder Browser) aus. Der Front-End-Webentwickler erstellt und richtet Kanäle Datenverkehr zu erfassen. Weitere Informationen finden Sie unter [Was wird Windows Internet Explorer-Bericht als Benutzer-Agent-Zeichenfolge?](https://msdn.microsoft.com/en-us/library/cc817582.aspx)

**Reihenfolge der Lösung für Gerätekanäle**

Wenn Sie mehrere Kanäle erstellen, sollten Sie diese in der Reihenfolge, in der Sie beheben möchten. Der erste Kanal, der eine Platzhalterinklusion Geräteregel enthält, die die Benutzer-Agent-Zeichenfolge übereinstimmt, wird verwendet. Die folgende Tabelle zeigt ein Beispiel für diese Regel.

|**DDE-Kanal**|**Reihenfolge 1**|**Reihenfolge 2**|
|:-----|:-----|:-----|
|1|Windows Phone 8|Windows Phone|
|2|Windows Phone|Windows Phone 8|
|3|Default|Default|
Wenn Reihenfolge 1 aktiv ist, mit der ein Benutzer fordert, dass eine Seite aus einem Windows 8-Telefon Gerätekanal 1 erhält Windows Phone 8 Bezeichnung. Ein Benutzer mit einem anderen Windows-Telefon verwenden Kanal 2, und alle anderen würde Kanal 3 verwenden. Jedoch Reihenfolge 2 verwenden, ein Benutzer fordert, dass eine Seite mit einem Windows 8-Telefon immer Gerätekanal 1 erhalten würden mit der Bezeichnung Windows Phone und der dafür angegebene Gerätekanal würde nie verwenden.

Nachdem Sie definieren und Gerätekanäle bestellen, können Sie verschiedene Gestaltungsvorlagen auf jeden Kanal anwenden. Standardmäßig werden alle Kanäle die Masterseite des Kanals Standard verwenden. 

**Hinweis:**  CSOM ist eine öffentliche API zum Bearbeiten von Gerätekanäle und gerätekanalbereiche nicht enthalten.

### <a name="display-templates"></a>Anzeigevorlagen

SharePoint-Veröffentlichungswebsites verwenden, die Vorlagen, die steuern, welche Eigenschaften verwalteten angezeigt werden, in den Suchergebnissen und wie sie im Webpart angezeigt werden. Suchen Sie nur Anzeigevorlagen für Webparts verwenden. das Webpart für Inhaltsabfragen ist keine Suche-Webparts und Anzeigevorlagen wird nicht verwendet.

Die folgende Tabelle enthält die Arten von Anzeigevorlagen in der Reihenfolge, in der Sie SharePoint gilt. 

|**Anzeigevorlage**|**Hinweise**|
|:-----|:-----|
|Steuern von Anzeigevorlagen|Gilt für das gesamte Webpart, damit SharePoint first wendet und nur einmal. HTML, die das allgemeine Layout für die Darstellung von Suchergebnissen Strukturen bereitgestellt. Beispielsweise können Sie eine Steuerelement-Anzeigevorlage für die Überschrift und Anfang und Ende einer Liste HTML bereitstellen. Diese Vorlage ist nur einmal im Webpart gerendert. |
|Gruppe Anzeigevorlagen|Zweitens angewendet, und wird einmal pro Gruppe angewendet, um die Suche Suchergebnisse-Webpart. |
|Elementanzeigevorlagen|Zuletzt angewendet, es sei denn, eine Anzeigevorlage Filter angewendet wird. Elementanzeigevorlagen gelten für jedes Element. Diese Vorlage bestimmt, wie jedes Element im Resultset im Webpart angezeigt wird. Beispielsweise kann es den HTML-Code für ein Listenelement, das nur-Text ist, ein Listenelement, das eine Grafik enthält oder ein Listenelement, das einen Block mit zusätzlichen Links und zusammenfassenden Beschreibungsinformationen zu bieten mehr Kontext für die Suchergebnisse formatiert bieten. |
SharePoint speichert Anzeigevorlagen in den Ordner Anzeigevorlagen im Gestaltungsvorlagenkatalog. Jede Anzeigevorlage ist eines Inhaltstyps in the Master Page Gallery zugeordnet. Um den Inhaltstyp für jede Anzeige-Vorlagendatei zu identifizieren, während über ein zugeordnetes Laufwerk, verwenden Sie den Dateinamen.

Der Ereignisempfänger, die konvertieren und Aktualisieren von Gestaltungsvorlagen und Seitenlayouts aus HTML, JavaScript auch konvertiert Anzeigevorlagen von HTML in JavaScript. Die Konvertierung und synchronisiert ist unidirektional; nicht werden aus JavaScript zurück zu HTML konvertiert.

**Hinweis:**  CSOM ist eine öffentliche API zum Bearbeiten von Anzeigevorlagen nicht enthalten.

**Anzeigevorlagenstruktur**

Jede Anzeigevorlage enthält Folgendes: 

- Ein Titel.
    
- Eine Kopfzeile, die benutzerdefinierte Elemente enthält begrenzt wird durch eine `<mso:CustomDocumentProperties>` Tag.
    
- Ein `<body>` -Tag, das einen Script-Block enthält.
    
- Eine `<div>` Tag.
    
Die benutzerdefinierten Dokumenteigenschaften enthalten wichtige Informationen über die Anzeigevorlage in SharePoint. Jede Anzeigevorlage einen Inhaltstyp identifizierte zugeordnet ist `<ContenTypeId>`. Sie können andere Eigenschaften, die bestimmen, ob auf die Vorlage in der Liste der verfügbaren Anzeigevorlagen für das Webpart anzuzeigen oder auszublenden, die HTML, JavaScript eigenschaftenzuordnung verwaltet, die im Kontext, in dem die Anzeigevorlage verwendet wird, festzulegen, ob eine JS-Datei ist die HTML-Anzeigevorlage derzeit zugeordnet und gibt an, ob die Konvertierung von HTML in JavaScript erfolgreich war oder wenn Sie Warnungen und Fehler erstellt wurden. 

Innerhalb der `<script>` -Tag, können Sie externe CSS oder JavaScript-Dateien außerhalb der Hauptbildschirm Vorlagen HTML-Datei verweisen.

Wenn die Genehmigung von Inhalten in the Master Page Gallery, alle CSS, JavaScript erforderlich ist, und andere Ressourcendateien müssen vor dem veröffentlicht werden werden sie Gestaltungsvorlagen und Seitenlayouts zur Verfügung. Weitere Informationen finden Sie unter [Festlegen einer Genehmigungserfordernis für Elemente in einer Liste oder Bibliothek](https://support.office.com/en-us/article/Require-approval-of-items-in-a-site-list-or-library-cd0761c4-8c3f-4ea2-9435-13c28aa23d08?CorrelationId=4efce7db-3017-4f50-854d-1f07eaf6bc16&amp;ui=en-US&amp;rs=en-US&amp;ad=US). Die `<div>` -Tag enthält eine ID, die mit dem Namen der Vorlage HTML-Anzeigedatei übereinstimmt. Ort CSS oder JavaScript, die Sie einschließen möchten, die angepasst wird, wie in diesem Webpart angezeigt wird die `<div>` blockieren.

**Verarbeitung der Anzeige-Vorlage**

SharePoint definiert Anzeigevorlagen in HTML-Dateien und JavaScript. Wenn im Entwurfs-Manager ändern eine HTML-Datei, die eine Anzeige Vorlagendefinition enthält und Änderungen zu speichern, kompiliert SharePoint Änderungen in einer JavaScript-Datei mit dem gleichen Namen. SharePoint verwendet diese JavaScript-Datei zum Rendern von Webparts auf Seiten.

**Wichtig:**  Bearbeiten Sie die JavaScript-Datei, die die Anzeige Vorlagendefinition enthält nicht. Aktualisieren Sie nur die HTML-Datei. Der Konvertierungsprozess erfordert die HTML-Datei XML-kompatibel sein. Verwenden Sie beispielsweise ** &lt;Br&gt;**, nicht ** &lt;Br /&gt;**. Weitere Informationen finden Sie unter [Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint 2013](http://msdn.microsoft.com/library/a76ab289-3256-45de-ac63-d5112a74e3c7%28Office.15%29.aspx).

**Erstellen von neuen Anzeigevorlagen**

Die einfachste Möglichkeit zum Erstellen einer neuen Anzeigevorlage ist so ändern Sie eine vorhandene Vorlage. Verschiedenen Anzeigevorlagen Ändern der Darstellung eines anderen suchbezogene Webparts, darunter das Inhaltssuche-Webpart, das Einschränkungsbereich-Webpart, der Taxonomie-Einschränkungsbereich-Webpart, und die Suchergebnisse-Webpart. Weitere Informationen finden Sie unter:

- [SharePoint 2013 Design Manager Anzeigevorlagen](http://msdn.microsoft.com/library/1a782bac-48ee-4baf-8751-0f943a306e0f%28Office.15%29.aspx)
    
- [Konfigurieren von Such-Webparts in SharePoint Server 2013](https://technet.microsoft.com/en-us/library/jj679900%28v=office.15%29.aspx)
    
- [Konfigurieren von Eigenschaften eines Einschränkungsbereich-Webparts in SharePoint Server 2013](https://technet.microsoft.com/en-us/library/gg549985%28v=office.15%29.aspx)
    
- [Anzeigen der vorlagenreferenz in SharePoint Server 2013](https://technet.microsoft.com/en-us/library/jj944947%28v=office.15%29.aspx)
    
**Anzeigevorlagen für Eigenschaften, die in verwendet werden können**

Bevor Sie beginnen, um Eigenschaften zu identifizieren, die Sie in einer Anzeigevorlage verwenden können, suchen Sie eine vorhandene Anzeigevorlage, den, die Sie aus, und speichern Sie es unter einem neuen Namen erstellen möchten. Anzeige der vorlagecode befindet sich in der `<mso:ManagedPropertyMapping>` Tag.

```
<mso:ManagedPropertyMapping msdt:dt="string">'Picture URL'{Picture URL}:'PublishingImage;PictureURL;PictureThumbnailURL','Link URL'{Link URL}:'Path','Line 1'{Line 1}:'Title','Line 2'{Line 2}:'Description','Line 3'{Line3}:'','SecondaryFileExtension','ContentTypeId'</mso:ManagedPropertyMapping>
```

Öffnen Sie als Nächstes **Websiteeinstellungen** > **Suchschema**, und suchen Sie nach ein Spaltenname in das Feld verwaltete Eigenschaft Filter, die in einer Anzeigevorlage enthalten sein sollen. Wählen Sie die verwaltete Eigenschaft aus, und klicken Sie dann bearbeiten Sie, und kopieren Sie der Name der Eigenschaft. 

```
<mso:ManagedPropertyMapping msdt:dt="string">'Picture URL'{Picture URL}:'PublishingImage;PictureURL;PictureThumbnailURL','Link URL'{Link URL}:'Path','Line 1'{Line 1}:'Title','Line 2'{Line 2}:'Description','Line 3'{Line3}:'','owsTXTPrice','owsTXTColor'</mso:ManagedPropertyMapping>
```

**Hinweis:**  In diesem Beispiel wird **Bild-URL** der ersten verwalteten Eigenschaft zugeordnet, die vorliegt, wenn die Suche Ergebnisse für **PublishingImage**, **PictureURL**oder **PictureThumbnailURL**erhält.

### <a name="image-renditions"></a>Bilddarstellungen

Eine Wiedergabe eines beschnittenen Bildes definiert die Dimensionen, die zum Anzeigen von Bildern auf den Seiten in SharePoint 2013-Veröffentlichungswebsites verwendet werden. Sie können CSOM bilddarstellungen zu instanziieren. Sie können mithilfe der [ImageRendition](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.imagerendition.aspx) -Klasse Metadaten wie der Höhe, Breite, Name und Version des ein Wiedergabe eines beschnittenen Bildes angeben. Sie können Methoden und Eigenschaften in der [SiteImageRenditions](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.siteimagerenditions.aspx) -Klasse zum Lesen und Schreiben von bilddarstellungen aus einer Websitesammlung.

Weitere Informationen finden Sie unter [SharePoint 2013 Design Manager bilddarstellungen](http://msdn.microsoft.com/library/d08a74c0-5674-4f26-8646-11ea1f081c85%28Office.15%29.aspx).

## <a name="sharepoint-and-common-web-programming-techniques"></a>SharePoint- und allgemeine Web Programmiertechniken

SharePoint Designer und Entwickler möchten häufig Programmiertechniken standard Web mit SharePoint verwenden, wenn sie Veröffentlichungssites entwerfen. Sie können schnell Entwurf, adaptive entwerfen, oder Gerätekanäle und schnell Design gemeinsam verwendet.

### <a name="responsive-design"></a>Schnell design

Mit Gerätekanälen können Sie eine Website einmal erstellen, und klicken Sie dann auf mehreren Geräten und Browsern, die als Ziel. Der Web-Entwicklungscommunity verwendet normalerweise schnell Entwurf und die "Fluid Raster" Ansatz zum Verwalten von Layouts wie Rendern und zum Entwerfen von Websites auf eine beliebige Browser oder das Gerät ordnungsgemäß gerendert werden soll. In einem Design schnell neu anordnen Elemente auf einer Seite selbst, um das Gerät des Benutzers und die Ausrichtung der Bildschirm passt.

Schnell Design basiert auf das Feature zum Abfragen von Medien in CSS3. Es verwendet Media Abfragen, um die Breite der Anzeige des Geräts angepasst und anschließend Formatvorlagen auf der Clientseite Rendern des Inhalts angewendet. Abfragen ermöglichen es für einen bestimmten Standort Eigenschaften Ziel, wie etwa Bildschirmbreite-Designer. Sie können mithilfe von Medienabfragen erstellen flexible Layouts und Bilder und CSS-Datei alternativen bedingt aufrufen.

Weitere Informationen und Beispiele finden Sie unter [SharePoint 2013/2016/Online schnell UI](https://dev.office.com/patterns-and-practices-detail/7267), [Schnell SharePoint](http://responsivesharepoint.codeplex.com/) und [Implementieren Sie Ihre Entwürfe schnell auf SharePoint 2013](http://blogs.msdn.com/b/sharepointdev/archive/2013/04/01/implementing-your-responsive-designs-on-sharepoint-2013.aspx). 

### <a name="adaptive-design"></a>Adaptive design

Adaptive Webdesigns (adaptive Web-Bereitstellung bezeichnet) ähnelt schnell Webdesigns. Eine adaptive Design wartet auf Geräten oder Browsern und wählt die optimale Methode zum Rendern von Seiten. 

Das Gerät Kanäle Feature in SharePoint 2013 ist eine adaptive Entwurf. Es bietet adaptive Layouts für jedes Gerät basierend auf Seitenlayouts, die Spezifikationen der einzelnen Gerätekanal und der Reihenfolge, in der Systemsteuerung Gerät DDE-Kanal definiert. 

### <a name="device-channels-and-responsive-design-together"></a>Gerätekanäle und schnell Design zusammen

Gerätekanäle und schnell Web Entwicklungstechniken können zusammen zum Erstellen einer schnell öffentliche SharePoint-Veröffentlichungswebsite. Erstellen Sie eine einzelne benutzerdefinierte Masterseite für Geräte wie Telefone und Tablets und einen anderen Webbrowser, und ordnen Sie jeweils mit einer Gerätekanal. Anschließend verwenden Sie flexible Raster, flexible Bilder und CSS3 Media Abfragen gestalten Sie die beste Wiedergabequalität für jedes Gerät und Browser benötigten Ihrer Website zu unterstützen.

## <a name="add-jquery-to-a-sharepoint-site"></a>Hinzufügen von jQuery zu einer SharePoint-Website

Sie können einer SharePoint-Website auf der Websiteebene der Seitenebene jQuery hinzufügen oder innerhalb von Abschnitten einer Seite, beispielsweise eine der die Bereiche der SharePoint-Seite oder ein Webpart hinzugefügte auf das Seitenlayout.

Eine benutzerdefinierte Aktion können Sie um jQuery aus einer Dokumentbibliothek zu laden. Dies, wenn Sie jQuery in einer SharePoint-Website für alle Seiten verfügbar machen müssen. Dieser Ansatz ist flexibel, aber ist nicht einfach auf das Steuerelement, und dies wirkt sich auf die Website-Designer und vom Administrator. Speichern und JavaScript-Dateien in der Dokumentbibliothek verwaltet werden können, aber sie können auch versehentlich geändert oder gelöscht werden soll. Aus diesem Grund empfohlen nicht diese Vorgehensweise.

Sie können auch im SharePoint-Stammverzeichnis jQuery laden, mithilfe von [ScriptLinkControl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.webcontrols.scriptlink.aspx). Sie können mithilfe des Skripts einzufügen, die auf einer Remotewebsite ausgeführt werden, und ändern die Skripts ohne direkten Zugriff auf die SharePoint-Installation. Der **ScriptLinkControl** Ansatz ist sinnvoll, wenn Sie auf einer Anwendungsseite oder in einem Webpart, das auf einer Seite angezeigt wird, jQuery verwenden möchten. Während der Bereitstellung mit dieser Option sind langsam und wirkt sich auf Leistung, da jQuery jeweils eine Seite hinzugefügt wird, umgeht das Bereitstellen der jQuery-Datei für die SharePoint-Regel andere legacy-Anforderungen. Dies ist hilfreich, wenn die csom Ihrer SharePoint 2013-Lösung voll vertrauenswürdiger Code (FTC) migriert werden müssen, und die Migration umfasst, verschieben und Umgestalten von benutzerdefinierten JavaScript und jQuery Verhaltensweisen.

Schließlich können Sie den Inhalts-Editor-Webpart zum Laden der jQuery aus einer Content Delivery Network (CDN) verwenden. Dies ist nützlich, wenn Sie ein oder mehrere Seiten, einschließlich der Webpart und Wiki-Seiten jQuery hinzufügen müssen. Da Sie die Datei jQuery aus einem CDN laden, müssen Sie keine zusätzliche Dateien auf dem SharePoint-Server zu speichern, und Benutzer können von einer verteilten, zwischengespeicherte Version der Dateien jQuery nutzen. SharePoint Ruft die jQuery-Datei aus dem CDN, und Sie können benutzerdefinierte jQuery-Code, die Sie erstellen den Inhalts-Editor-Webpart hinzufügen. 

## <a name="build-sharepoint-provider-hosted-add-ins-with-aspnet-mvc-5"></a>Erstellen von SharePoint gehostet durch Drittanbieter-add-ins mit ASP.NET MVC-5

Sie können benutzerdefinierte Anbieter-Hosting-add-ins mit dem Muster für Model-View-Controller (MVC) in SharePoint erstellen. Dieses Modell trennt die Anwendung in drei Teile miteinander verbunden. Dies trennt die interne Darstellung der Informationen aus wie diese angezeigt und vom Benutzer angenommen werden. Das Modell stellt die zugrunde liegende Struktur der Software, die Ansicht (in der Regel Benutzeroberflächenelemente) und der Controller der Klassen sind, die einzelnen Details des Modells und der Ansicht zu verbinden. 

Sie können ASP.NET MVC in SharePoint-Gestaltungsvorlage Websiteinhaltstyp umbrochen werden soll. Tatsächlich können Sie Office 365-APIs zum Erstellen eines SharePoint 2013-add-Ins mit ASP.NET MVC 5 aus. 

APIs für MVC für SharePoint-Entwicklung in definiert sind `Filters\SharePointContextFilterAttribute.cs` und `SharePointContext.cs`. Diese APIs Text fließt um die Schritte, die das Webprojekt erwartet nahtlos kommunizieren mit SharePoint in einem einzigen Aufruf und vereinfacht die Logik, die implementiert werden müssen.

Das Attribut SharePoint Context Filter führt weitere Verarbeitung weiterleitet, um Standardinformationen beim Umleitung von SharePoint auf Ihre remote-Webanwendung, wie die Host-Web-URL zu erhalten. Außerdem wird bestimmt, ob das Add-in zu SharePoint für den Benutzer, sich anzumelden (beispielsweise Lesezeichen) weitergeleitet werden muss. Sie können diesen Filter für den Controller oder zu einer Ansicht anwenden. SharePoint-Context-Klassen kapseln alle Informationen aus SharePoint, damit Sie bestimmte Kontexte für die Add-ins Web und Hostwebsite erstellen und mit SharePoint kommunizieren können.

Weitere Informationen finden Sie unter [Informationen zu ASP.NET MVC](http://www.asp.net/mvc/overview) und[Einführung in MVC für SharePoint-Add-ins zu unterstützen](http://blogs.msdn.com/b/officeapps/archive/2013/07/09/introducing-mvc-support-for-apps-for-sharepoint.aspx).

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website](Branding-and-site-provisioning-solutions-for-SharePoint.md)
    
- [Vorgehensweise: Anwenden von Formaten auf Seitenfelder in SharePoint 2013](http://msdn.microsoft.com/library/e227613d-0e4d-4312-924d-bb55e1fe4293%28Office.15%29.aspx)
    
- [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx)
    
- [Vorgehensweise: Anpassen von Seitenlayouts für eine Catalog-based Site in SharePoint 2013](http://msdn.microsoft.com/library/21d8db99-73b3-4429-b6cb-04e375af9f55%28Office.15%29.aspx)
    
- [Vorgehensweise: Zuordnen eines Netzlaufwerks zum SharePoint 2013 Master Page Gallery](http://msdn.microsoft.com/library/7d416f6e-2471-4d03-97ae-4e8d907784c6%28Office.15%29.aspx)
