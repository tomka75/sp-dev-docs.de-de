---
title: SharePoint-Seiten und das Seitenmodell
ms.date: 11/03/2017
ms.openlocfilehash: 74cb39e91919d872f1a5e8eda7b9b36b8ef67108
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="sharepoint-pages-and-the-page-model"></a>SharePoint-Seiten und das Seitenmodell

In diesem Artikel wird das SharePoint-Seitenmodell, einschließlich Masterseiten, Inhaltsseiten, Teile einer SharePoint-Seite und standardmäßige Seite Dateitypen. 

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Eine gerenderte SharePoint-Seite ist eine Kombination aus drei Seitentypen: 

- Eine Gestaltungsvorlage, die das Layout und die Darstellung des Inhalts steuert.
    
- Eine Inhaltsseite, die die Steuerelementen für Seitenfelder enthält.
    
- Eine benutzerfreundliche authoring Seite, in dem der Benutzer Inhalt hinzugefügt wird.
    
Dieser Artikel enthält eine Übersicht über das SharePoint-Seitenmodell, einschließlich der Seitentypen Dateien der Standard-Seite, die in SharePoint 2013 und SharePoint Online und Informationen zur Verarbeitung von Seiten verfügbar sind. 

## <a name="key-terms-and-concepts-related-to-the-sharepoint-page-model"></a>Wichtige Begriffe und Konzepte im Zusammenhang mit der SharePoint-Seitenmodell
<a name="sectionSection0"> </a>

|**Begriff oder Konzept**|**Definition**|**Zugriff über**|**Weitere Informationen**|
|:-----|:-----|:-----|:-----|
|Website für die Zusammenarbeit|Eine Teamwebsite.|||
|Platzhalter für Inhalt|Ein Eintrag in einer Gestaltungsvorlage, die reserviert ein Leerzeichen für Steuerelemente oder Inhalte, die programmgesteuert später ersetzt werden kann.|Alle SharePoint-Gestaltungsvorlagen|Inhaltsplatzhalter sind die Bausteine von SharePoint-Gestaltungsvorlagen.|
|Gestaltungsvorlage|Eine Seite, die das Verhalten und die Darstellung von der linken und oberen Navigationselemente einer SharePoint-Seite standardisiert.|SharePoint-Dateisystems Master Page Gallery||
|Gestaltungsvorlagenkatalog|Eine spezielle Dokumentbibliothek in SharePoint 2013, in dem alle Brandingelemente - master-Seiten, Seitenlayouts, JavaScript-Dateien, CSS und Bilder – werden standardmäßig gespeichert. Jede Website besitzt einen eigenen Gestaltungsvorlagenkatalog.| **Einstellungen** > **Websiteeinstellungen** > **Gestaltungsvorlagen und Seitenlayouts**|The Master Page Gallery enthält Kataloge, die branding-Objekte wie etwa Gestaltungsvorlagen und CSS-Dateien zu speichern.<br/>**Tipp**  Bei der Erstellung von benutzerdefinierten Brandingelemente speichern Sie benutzerdefinierter Objekte in der Standardeinstellung Master Page Gallery-Dateistruktur.<br/>[Master Pages, the Master Page Gallery und Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/80b9a360-bc2e-46c6-b0ca-1bc487b73db6.aspx)|
|Minimale Downloadstrategie (MDS)|Eine Strategie, die die Menge der Daten, die im Browser heruntergeladen werden muss verringert, wenn Benutzer von einer SharePoint-Seite in eine andere navigieren.|Websiteeinstellungen|Bei aktivem MDS übergibt SharePoint über alle Seitenanforderungen `/_layouts/15/start.aspx` und visuelle Unterschiede zwischen Seitenaufrufe und der zuvor geladene Seite überprüft.<br/>[Optimieren der Leistung der Seite in SharePoint 2013](http://msdn.microsoft.com/library/262caeef-64fd-4e02-b947-d772faf01159.aspx)<br/>[Übersicht über die minimale Strategie herunterladen](http://msdn.microsoft.com/library/9caa7d99-1e74-4889-96c7-ba5a10772ad7.aspx)|
|Navigation|Funktionen, die Benutzer, um die Informationsarchitektur einer SharePoint-Website verschieben kann. Elemente für die Navigation in SharePoint enthalten, Suche, Strukturansichten, Schaltflächen, das Menüband, Hyperlinks, Registerkarten, Menüs und Taxonomie.||[Navigation-Klasse](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.navigation.aspx)<br/>[NavigationNode-Klasse](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.navigationnode.aspx)|
|Oslo Master-Shape|Eine Standardgestaltungsvorlage in SharePoint 2013.|SharePoint-Dateisystems Master Page Gallery|Im Gegensatz zu der Masterseite seattle.master befindet sich die aktuelle Navigation in derselben Position wie im oberen Navigationsbereich.|
|Seite Inhaltssteuerelement|Ein Steuerelement auf einer Veröffentlichungswebsite, die ein Webpart hinzugefügt werden kann.|||
|Seitenlayout|Eine Vorlage auf einer Veröffentlichungswebsite angewendete Seite, die die konsistente Präsentation von Inhalten erzwingt.|SharePoint-Dateisystems Master Page Gallery| [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80.aspx)|
|Seitenmodell|Dateien, Inhalte und Aktivitäten, die in einer SharePoint-Seite für Benutzer in einem Browser gerendert.|| [Übersicht über das Modell von SharePoint 2013](http://msdn.microsoft.com/library/808b1af3-89ab-4f02-89cc-ea86cb1f9a6e.aspx)|
|Veröffentlichungsseite|Eine ASPX-Seite in eine Website.|| [PublishingPage-Klasse](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.publishingpage.aspx)|
|Veröffentlichungswebsite|Eine SharePoint-Website, die Veröffentlichung von Websites und Seiten, die Seitenlayouts, Taxonomie, verwaltete Navigation und anderen Web Content Management und Enterprise Content Management-Features zugreifen kann. || [PublishingWeb-Klasse](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.publishingweb.aspx) [Was ist neu in SharePoint 2013-Websiteentwicklung](https://msdn.microsoft.com/en-us/library/office/jj163942.aspx)|
|Seattle.Master|Eine Standardgestaltungsvorlage in SharePoint 2013.|SharePoint-Dateisystems Master Page Gallery||
|Teamwebsite|Eine Website für die Benutzer für die Zusammenarbeit an Dokumenten, Wikis, Ideen, Prozesse und So weiter vorgesehen.|||
|TextLayout|Definiert die Inhaltsbereiche, die angezeigt werden auf einer Wikiseite.|||
|Text Layout-Steuerelement|Eine Wiki-Seite-Steuerelement, das Text, Bilder, Webparts und App-Webparts enthalten kann.|||
|Website auf oberster Ebene|Das standardmäßige vom Server bereitgestellten Website auf oberster Ebene.|| [Erstellen einer SharePoint-Website](https://support.office.com/en-us/article/Create-a-SharePoint-site-4b1c153a-ec2b-45df-9dd9-e31d25563d1b?CorrelationId=ad2fc24e-9e3e-4da4-be0f-500d2e89fc64&amp;ui=en-US&amp;rs=en-US&amp;ad=US)|
|Webpart|Serverseitige Steuerelemente, die innerhalb des Kontexts von Seiten einer Website ausgeführt.|| [Benutzerdefinierte Aktionen und Eigenschaft Eigenschaftensammlung Einträge aus einer SharePoint-app](http://blogs.msdn.com/b/vesku/archive/2013/10/02/ftc-to-cam-custom-actions-and-property-bag-entries.aspx)|
|Webpart-Seite|Eine Inhaltsseite bestehend aus Webpartzonen, die Webparts enthalten kann. Webparts sind auf Webpartseiten [WebPartDefinition](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.aspx) Objekte dargestellt.|| [Microsoft.SharePoint.Client.WebParts-namespace](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.webparts.aspx)|
|WebPartZone|Ein Bereich auf einer Seite an, der ein Webpart hinzugefügt werden können.|||
|Wiki-Seiten|Eine Inhaltsseite, die die Vorlage Unternehmenswiki-Website verwendet.|| [Provisioning.Pages Beispiel-app](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages)|

## <a name="sharepoint-master-pages"></a>SharePoint-Gestaltungsvorlagen
<a name="sectionSection1"> </a>

Eine Gestaltungsvorlage ist eine ASP.NET-Datei mit der Erweiterung Master. Es enthält einen `<%@ Master` Richtlinie, und das HTML-Elemente der obersten Ebene wie **HTML**, **Head**und **Form**definiert. Es zuerst listet Steuerelemente und Assemblys, und klicken Sie dann ein Document Type Definition des **DOCTYPE**, die im Browser mitteilt, wie die HTML-Rendering deklariert. SharePoint 2013 ist optimiert, um mit dem **XHTML 1.0** und **HTML5** DOCTYPES am besten geeignet.

SharePoint enthält verschiedene Masterseiten standardmäßig. Diese Gestaltungsvorlagen Geben Sie die Standardstruktur und Chrome einer bestimmten SharePoint-Seite, die für die SKU geeignet ist und Websitetyp, wobei dies sind Applicableâ€ "insbesondere auf der oberen und linken Rand der Seite. Tabelle 2 sind die Standardseiten SharePoint 2013 und SharePoint Online.

**In Tabelle 2. Standardmäßige SharePoint-Gestaltungsvorlagen**

|**Gestaltungsvorlage**|**Beschreibung**|
|:-----|:-----|
|Custom.Master|Systemseiten, wie Formulare und Ansichten. Alle SharePoint 2013 und SharePoint Online-SKUs verwendet.|
|Default.Master|Seiten der Website in Veröffentlichungswebsites. In allen SharePoint 2013 und SharePoint Online-SKUs enthalten. Verfügbar, wenn das Feature zum Veröffentlichen aktiviert wird.|
|"Application.Master"|Einige Systemseiten wie scope.aspx und keyword.aspx. In allen SharePoint 2013 und SharePoint Online-SKUs enthalten.|
|Minimal.Master|Verfügbare Gestaltungsvorlage Standardoption in alle SharePoint 2013-SKUs.|
|Seattle.Master|Verfügbare Gestaltungsvorlage Standardoption in allen SharePoint 2013 und SharePoint Online-SKUs.|
|Oslo.Master|Verfügbare Gestaltungsvorlage Standardoption in allen SharePoint 2013 und SharePoint Online-SKUs.|
|Kyoto.Master|Eine Gestaltungsvorlage in SharePoint Online verfügbar. |
|Berlin.Master|Eine Gestaltungsvorlage in SharePoint Online verfügbar. |
|Lyon.Master|Eine Gestaltungsvorlage in SharePoint Online verfügbar. |
|Mysite15.Master|OneDrive for Business-Websites (zuvor: "Meine Website", persönliche Websites oder OneDrive Pro Websites).|
Jeder SharePoint Standardgestaltungsvorlage enthält Steuerelemente, die für allgemeine Programmieraufgaben Technologien wie HTML, CSS und JavaScript-Funktion in SharePoint Web erforderlich sind.

Inhaltsplatzhalter halten die Stelle Informationen in Inhaltsseiten definiert. Inhaltsplatzhalter entsprechen Bereiche einer Seite. Jeder Bereich einer Seite Master wird durch zwischen wenige und Hunderten von Inhaltsplatzhalter definiert.

SharePoint-Gestaltungsvorlagen verwenden eine Kombination von ASP.NET ( `<asp:`) und SharePoint ( `<SharePoint:`) Deklarationen. Text nach der Doppelpunkt in einer Deklaration die Funktionalität des Steuerelements definiert. beispielsweise `SharePoint:PlaceholderGlobalNavigation` die globale Navigation von einer Seite in der entsprechenden HTML-auf der Seite Tags SharePoint einbettet. Inhaltssteuerelemente in eine Gestaltungsvorlage binden Inhaltsplatzhalter an Inhalt mit der **ContentPlaceHolderID**.

SharePoint bietet zwei Arten von Gestaltungsvorlagen: System Masterseiten Andsite Gestaltungsvorlagen. System Gestaltungsvorlagen gelten für alle von Formularseiten und Seiten auf einer SharePoint-Website anzeigen. Master-Shape Websiteseiten dienen andererseits, von allen Seiten in einer Veröffentlichung Website. Welche Art von Masterseite erkennen, die eine Website verwendet, indem Sie die Seite Master-Datei öffnen und Anzeigen der **Seite** Richtlinie. Eine Systemgestaltungsvorlage hat eine Seitendirektive wie folgt: `~masterurl/default.master`. Eine Gestaltungsvorlage der Website hat die folgende Seitendirektive: `~masterurl/custom.master`.

CSOM-Code können Sie Gestaltungsvorlage Propertiesâ festlegen "hauptsächlich von Schreiben von Code für [Das Webobjekt](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.aspx) . € Ändern der Systemgestaltungsvorlage mithilfe von dessen [MasterUrl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.masterurl.aspx) -Eigenschaft, und Gestaltungsvorlage der Website mithilfe des Objekts [CustomMasterUrl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.custommasterurl.aspx) -Eigenschaft.

Inhalte, dass Platzhalter häufig dynamische Token enthalten sind, die wichtige Teile des Codes, die Teil einer SharePoint-Seiten-URL zu bilden. SharePoint analysiert URL-Zeichenfolgen nach den Regeln der Protokolle, wie etwa HTTP, die definieren, wie Hypertext-Informationen zwischen dem Server und einer SharePoint-Seite übertragen werden. In der Regel verwendet ein Platzhalter für Inhalt, der auf ein Steuerelement CSS oder des Designs zeigt eine relative URL, die im SharePoint Server-Side Object Model als dargestellt ist `~SPUrl`.

SharePoint verwendet dynamische Token, um die Masterseite für die Inhaltsseite binden definiert in den `<asp:content>` Deklaration der Master Seitencode. Tabelle 3 Listen dynamische Token, die in SharePoint-Gestaltungsvorlagen und die CSOM-Eigenschaften, die sie bei der Verarbeitung der Seite ersetzen befinden oder URL-Zeichenfolge, die für diese Inhaltsplatzhalter SharePoint rendert.

**Tabelle 3. Dynamische Token in Gestaltungsvorlagen durch Eigenschaftswerte ersetzt**

|**Dynamische token**|**Ersetzt durch**|
|:-----|:-----|
|~MasterUrl/default.Master|SPWeb.MasterUrl|
|~masterurl/custom.Master|SPWeb.CustomMasterUrl|
|~Site/&lt;Xyz&gt;Master|http://&lt;SiteColl&gt;/&lt;dem Namen subsite1&gt;/&lt;subsite2&gt;/&lt;Xyz&gt;Master|
|~sitecollection/&lt;Abc&gt;Master|http://&lt;SiteColl&gt;/&lt;Abc&gt;Master|

**Hinweis**  Die dynamischen Token in Inhaltsplatzhalter entsprechen serverseitige-API-Eigenschaften und Methoden. Schreiben Sie Code in CSOM oder REST, bei der Verwendung von remote-Bereitstellung. Weitere Informationen zum SharePoint-URLs und dynamische Token finden Sie unter [URLs und Token in SharePoint 2013](http://msdn.microsoft.com/library/161418d7-8123-4c4e-91a1-97e43c17f0e6.aspx). Add-ins für SharePoint verwenden einige Token, die für die Website-URLs gelten.

## <a name="web-part-pages-and-wiki-pages"></a>Webpartseiten und Wiki-Seiten
<a name="sectionSection2"> </a>

Webpartseiten können strukturierten und unstrukturierten Informationen enthalten. Sie Webpartzonen bestehen. Webparts in Webpartzonen platziert Anzeigen von Daten aus Listen, Suchergebnisse und Abfragen können, und können benutzerdefinierte Ansichten der Daten aus mehreren Quellen darstellen. Eine Webpart-Seite enthält die gleichen Elemente als eine standardmäßige SharePoint-Teamwebsite. Die Titelleiste kann einen Titel, Titel, Beschreibung, Firmenlogo oder anderen Bilds enthalten. Der Webpartseite fügt die folgenden Elemente hinzu:

- Eine Webpartseite-Menü, das zum Hinzufügen oder Ändern von Webparts, das Seitenlayout und Wechseln zwischen den persönlichen und freigegebenen Ansichten verwendet werden kann.
    
- Ein Toolbereich zum Suchen und Hinzufügen von Webparts und Bearbeiten der Eigenschaften im Zusammenhang mit Webparts und die Webpartseite.
    
Im Vergleich zu Webparts-Seiten, sind Wiki-Seiten weniger strukturiert. Aufgrund ihrer halbstrukturierten zu unstrukturierten Form erleichtern sie Benutzern das Erstellen von Inhalten und miteinander zusammenarbeiten. SharePoint wird standardmäßig eine Wiki-Seite der erste Zeit, die Sie eine neue Teamwebsite anzeigen, angezeigt.

Enterprise Wiki-Funktionalität ist in allen Versionen von SharePoint zur Verfügung. Die Wiki-Unternehmensvorlage ermöglicht das Erstellen und Verwenden von Seitenlayouts mit Wiki-Seiten. Wenn Sie eine Wiki-Seite bearbeiten, wird von Webparts, Text und andere Inhalte in das Textlayout angezeigt. Das Textlayout ordnet Inhaltsbereiche auf einer Wikiseite.

Das remote provisioning Muster können Sie um eine Wiki-Seite zu erstellen. Die [WikiPageCreationInformation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.utilities.wikipagecreationinformation.aspx) -Klasse enthält Methoden, die Sie verwenden können, um die Wiki-Seiten zu erstellen, während die **WikiHtmlContent** -Eigenschaft ruft ab und HTML-Inhalte auf der Seite legt. Die [Utility](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.utilities.utility.aspx) -Klasse enthält eine **CreateWikiPageInContextWeb** -Methode, die SharePoint verwendet, um die Wiki-Seiten in der clientlaufzeitkontext mit Parametern von der **WikiPageCreationInformation** -Klasse zu erstellen.

## <a name="page-layouts"></a>Seitenlayouts
<a name="sectionSection3"> </a>

Das Seitenlayout wird die Inhaltsseite Wahl für Veröffentlichungssites. Seitenlayouts sind Vorlagen, die verschiedene Arten von Seiten in einer SharePoint-Website, wie beispielsweise Artikel definieren, indem Sie die Struktur des Textkörpers der Seite anpassen. Ebenso wie die Webpartseite eine Vorlage, die zum Anordnen von Webpartzonen und Webparts auf einer Seite vorhanden ist, vorhanden und Seitenlayouts Felder auf einer Seite anordnen. Die Feldsteuerelementen in einem Seitenlayout definiert werden Inhalte enthalten, die ein Autor erstellt, und die Struktur dieser Inhalte auf das Seitenlayout basieren.

**Hinweis**  Seitenlayouts können Webpartzonen enthalten.

Designer können Formate auf Seitenfeld-Steuerelemente anwenden. Dies ermöglicht Designern Kontrolle über wie CSS auf jedes Feld angewendet wird und gerendert, noch können Benutzer erstellen und Verwalten von Inhalten in jeder Seite dar.

In SharePoint sind Inhaltstypen wieder verwendbare Sammlungen von Metadaten (auch bekannt als Spalten) und das Verhalten, die bestimmte Elemente und Dokumente zu definieren. Sie möchten beispielsweise eine Art von Inhalt zu erstellen, die Darstellung und das Verhalten der Möglichkeit, den, die Sie vermutlich ein online magazine-Artikel würde. Inhaltstypen ermöglichen es Ihnen zu. Sie sollten auch andere eindeutigen Arten von Inhalten, aber Wiederverwendung erstellen und Freigeben von Merkmale einen Inhaltstyp in anderen. Jedes Seitenlayout basiert auf genau einen Inhaltstyp. Jeder Inhaltstyp ist eine eindeutige [Content-Typ-ID](https://msdn.microsoft.com/en-us/library/office/aa543822%28v=office.14%29.aspx)zugewiesen.

Weitere Informationen zu Inhaltstypen finden Sie unter [Einführung in Inhaltstypen](https://msdn.microsoft.com/en-us/library/office/ms472236%28v=office.14%29.aspx)und [Spalten](https://msdn.microsoft.com/en-us/library/office/ms196085%28v=office.14%29.aspx) [Custom Information in Content Types](https://msdn.microsoft.com/en-us/library/office/ms468437%28v=office.14%29.aspx).

**Wichtige**   Derzeit können Sie das remote provisioning Muster Out-of-Box-Seitenlayouts auf einer SharePoint-Website anwenden. Obwohl Sie benutzerdefinierte Inhaltstypen auf einer Website bereitstellen können, indem CSOM-Code über den benutzerdefinierten add-ins für SharePoint-Code, und Festlegen benutzerdefinierter wird **ContentTypeId** über CSOM in SharePoint Online und Festlegen der ContentTypeId für einen benutzerdefinierten Inhaltstyp über Remote unterstützt. Bereitstellung auf lokale SharePoint-Websites wird derzeit nicht unterstützt. Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80.aspx).

## <a name="sharepoint-page-processing-model"></a>SharePoint-seitenverarbeitungsmodell
<a name="sectionSection4"> </a>

SharePoint ist eine Vorlage basierende Seite-Renderingsystem, die Gestaltungsvorlagen und Inhaltsseiten erstelltem Inhalt zum Rendern von Seiten kombiniert. Das Seite Renderingsystem wird als die [Seite Verarbeitungsmodell](https://msdn.microsoft.com/en-us/library/office/ms498550%28v=office.14%29.aspx)bezeichnet. Gestaltungsvorlagen werden von allen Seiteninstanzen auf der Website verwendet, zu dem sie angewendet werden, und Inhaltsseiten werden von allen Instanzen der Seite, die auf dieser Seite Inhalt verwendet.

Die Seite Verarbeitungsmodell interpretiert und führt alle Anforderungen, Benutzer-Agents wie Webbrowser an den Server zu stellen. Angenommen Sie, einen Benutzer fordert eine Seite mit dem Namen contoso.aspx. Um die Anforderung abzuschließen, ruft das ASP.NET-Modul zwei Seiten: Inhaltsseite contoso.aspx zugeordnet und der Gestaltungsvorlage, die der Anbieter für die Datei mit der SharePoint-Website verknüpft. Das Modul auch Feldsteuerelemente und Webparts aus Feldern abgerufen und auf der Seite gerendert.

**Hinweis**  Die Seite Verarbeitungslogik für Team-Websites und Websites ähnelt, für die Veröffentlichung Seiten. 

### <a name="page-processing"></a>Verarbeitung Seite

Beim Laden einer Webpartseite eines SharePoint-Benutzers ruft SharePoint das durch den Pfad zu der Vorlage, Inhalt und Kontext analysieren. Außerdem die Webparts einer Webpartseite zugeordnet wird, weist eine [WebPartCollection](http://msdn2.microsoft.com/EN-US/library/k41e9930) -Instanz auf der Seite, und füllt die Webpartseite und zugehörigen Webparts mit Inhalten.

Beim Laden eines SharePoint-Benutzers eine Wiki-Seiten (entweder mithilfe der Vorlage Unternehmenswiki auf einer Teamwebsite oder einer Veröffentlichung Website), SharePoint wird durch den Pfad zu der Vorlage, Inhalt und Kontext analysieren abgerufen. Auch Layout Textsteuerelement Wiki-Seiten zugeordnet wird, und füllt das Unternehmenswiki-Seite und Textlayouts mit Inhalten. Finden Sie Informationen dazu, wie Sie eine Wiki-Seite bereit, mit dem remote provisioning Muster [Provisioning.Pages](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages) .

### <a name="minimal-download-strategy-and-ajaxdelta-controls"></a>Minimale downloadstrategie und <AjaxDelta> Steuerelemente

In SharePoint verwaltet das minimale Download Strategie Feature welche spezifischem Inhalt auf der Masterseite aktualisieren, bevor die Seite gerendert wird. Wenn die Strategie aktiviert ist, wird der Inhalt Inhaltsplatzhaltern in eingebunden zugeordnet `<SharePoint:AjaxDelta>` Tags auf der Gestaltungsvorlage vor dem Rendern der Seite aktualisiert. Dagegen Inhaltsplatzhalter nicht umgebrochen `<SharePoint:AjaxDelta>` Tags wird nicht gerendert werden, wenn die minimale downloadstrategie aktiviert ist.

Sie können aktivieren oder deaktivieren die minimale downloadstrategie über die Verwaltung der zentralen Standort oder mithilfe von SharePoint mithilfe der clientseitigen Objektmodell (CSOM). Sie können das Feature aktivieren, indem Sie mithilfe der [EnableMinimalDownload](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.enableminimaldownload.aspx) -Eigenschaft. Weitere Informationen finden Sie unter [Übersicht über die minimale Downloadstrategie](http://msdn.microsoft.com/library/9caa7d99-1e74-4889-96c7-ba5a10772ad7.aspx). Weitere Informationen dazu, wie Sie eine Gestaltungsvorlage auch die minimale downloadstrategie entwickelt optimieren finden Sie unter [Ändern von SharePoint-Komponenten für MDS](http://msdn.microsoft.com/library/c967be7c-f29f-481a-9ce2-915ead315dcd.aspx).

Das minimale Download Strategie Feature wird auf SharePoint-Teamwebsites standardmäßig aktiviert und standardmäßig auf SharePoint-Veröffentlichungswebsites und SharePoint-Teamwebsites mit aktivierter Veröffentlichung deaktiviert.

### <a name="creating-a-custom-master-page-based-on-seattlemaster"></a>Erstellen eine benutzerdefinierte Gestaltungsvorlage basierend auf seattle.master

Können Sie remote-Bereitstellung zur Bestimmung Website Brandingelemente wie Designs auf eine Website, und Sie können die CSS oder JavaScript verwenden, um Elemente oder Seitensteuerelemente anzeigen oder ausblenden. Anpassen einer Gestaltungsvorlage bietet ein höheres Maß an Kontrolle über die Seitenstruktur. Wenn Sie eine benutzerdefinierte Gestaltungsvorlage erstellen, nicht bearbeiten Sie, und speichern Sie eine standardmäßige master Pageby verwenden den Standardnamen (beispielsweise seattle.master). Stattdessen wird eine Kopie der Standardgestaltungsvorlage, den, die Sie ändern möchten, und benennen Sie sie.

**Wichtige**   Aufgrund der möglichen langfristige Auswirkungen von laufenden Supportkosten und Wartung wird empfohlen, dass Sie die Struktur der eine neue Gestaltungsvorlage nicht ändern. Sie können Änderungen an der Gestaltungsvorlage, die branding unterstützen, die die keine Auswirkung auf die Struktur, beispielsweise durch Ändern der Farben in der Kopfzeile, schwarzem Hintergrund auf bestimmte Elemente einer Seite hinzufügen oder anzeigen und Ausblenden von Website-Logo vornehmen. Enthält die Master-Standardseite verwendeten kein Strukturelement, wie eine Fußzeile, die Sie einschließen, klicken Sie auf der Seite möchten verwenden Sie eine andere Out-of-Box-Gestaltungsvorlage.

Zum Aufrechterhalten der Konsistenz bei einer benutzerdefinierten Gestaltungsvorlage, führen Sie das vorhandene Codierungsmuster-Hilfe. Beispielsweise in Bereiche der Seite, die mit Tabellen, unterstreichen Codierungsmuster mithilfe von Tabellen. In den Bereichen, in dem `<DIV>` Tags oder HTML5 verwendet werden, wird nach benutzerdefinierten Code mit `<DIV>` Tags oder HTML5. Dadurch wird langfristig, denen Sie einfacher zu verwalten, erstellen Sie benutzerdefinierten Masterseiten, und daher weniger kostspielige.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website](Branding-and-site-provisioning-solutions-for-SharePoint.md)
    
-  [Master Pages, the Master Page Gallery und Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/80b9a360-bc2e-46c6-b0ca-1bc487b73db6.aspx)
    
-  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80.aspx)
    
-  [SharePoint 2013: Verwenden Sie eine app für SharePoint zum Bereitstellen einer Wiki-Seiten](https://code.msdn.microsoft.com/SharePoint-2013-Use-an-app-5db977e8)
    
-  [Übersicht über die minimale Strategie herunterladen](http://msdn.microsoft.com/library/9caa7d99-1e74-4889-96c7-ba5a10772ad7.aspx)
    
-  [Einführung in Inhaltstypen](https://msdn.microsoft.com/en-us/library/office/ms472236%28v=office.14%29.aspx)
