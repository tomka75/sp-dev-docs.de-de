---
title: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a76ab289-3256-45de-ac63-d5112a74e3c7
ms.openlocfilehash: d76397e79d1580c2b113810523c2ce119a731ba4
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="convert-an-html-file-into-a-master-page-in-sharepoint"></a>Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint

Mit dem Entwurfs-Manager können Sie eine HTML-Datei in eine SharePoint-Gestaltungsvorlage (MASTER-Datei) konvertieren. Nach der Konvertierung wird die HTML-Datei mit der Gestaltungsvorlage verknüpft, sodass nach dem Bearbeiten und Speichern der HTML-Datei die Änderungen mit der zugeordneten Gestaltungsvorlage synchronisiert werden.

## <a name="introduction-to-converting-a-master-page"></a>Einführung in das Konvertieren in eine Gestaltungsvorlage
<a name="Introduction"> </a>

 Mit dem Entwurfs-Manager können Sie eine HTML-Datei in eine SharePoint-Gestaltungsvorlage mit der Erweiterung ".master" konvertieren. Nach der Konvertierung werden die HTML-Datei und Gestaltungsvorlage miteinander verknüpft, sodass nach Bearbeiten und Speichern der HTML-Datei die Änderungen mit der zugeordneten Gestaltungsvorlage synchronisiert werden.
  
    
    
Warum sollen Sie eine HTML-Datei konvertieren, anstatt eine Gestaltungsvorlage von Grund auf neu zu erstellen? In SharePoint funktionieren Gestaltungsvorlagen exakt wie in ASP.NET. Doch SharePoint verlangt außerdem, dass bestimmte für SharePoint spezifische Elemente wie Steuerelemente und Inhaltsplatzhalter auf der Seite vorhanden sein müssen, damit SharePoint die jeweilige Gestaltungsvorlage ordnungsgemäß rendern kann. Durch das Konvertieren einer HTML-Datei in eine voll funktionsfähige SharePoint-Gestaltungsvorlage mit dem Entwurfs-Manager müssen Sie nicht mit ASP.NET- oder SharePoint-spezifischem Markup vertraut sein. Stattdessen können Sie sich auf das Entwerfen Ihrer Website in HTML, CSS und JavaScript konzentrieren.
  
    
    
Beim Konvertieren einer HTML-Datei in eine Gestaltungsvorlage passiert Folgendes:
  
    
    

- Eine MASTER-Datei, die denselben Namen wie Ihre HTML-Datei hat, wird im Gestaltungsvorlagenkatalog erstellt.
    
  
- Das gesamte von SharePoint verlangte Markup wird der MASTER-Datei hinzugefügt, damit die Gestaltungsvorlage ordnungsgemäß gerendert wird.
    
  
- Markup wie Kommentare, **\<div\>**-Tags, Codeausschnitte und Inhaltsplatzhalter werden Ihrer ursprünglichen HTML-Datei hinzugefügt.
    
  
- Die HTML-Datei und Gestaltungsvorlage werden miteinander verknüpft, damit spätere Änderungen an der HTML-Datei mit der MASTER-Datei synchronisiert werden, sobald die HTML-Datei gespeichert wird.
    
> [!NOTE]
> Die Synchronisierung erfolgt nur in eine Richtung. Änderungen an der HTML-Gestaltungsvorlage werden mit der zugehörigen .master-Datei synchronisiert, aber wenn Sie die .master-Datei direkt bearbeiten, werden diese Änderungen nicht mit der HTML-Datei synchronisiert. Jede HTML-Gestaltungsvorlage (und jedes HTML-Seitenlayout) verfügt über eine Eigenschaft mit dem Namen **Zugeordnete Datei**, die standardmäßig auf **True** festgelegt ist und mit deren Hilfe die Zuordnung und die Synchronisierung zwischen Dateien eingerichtet wird.
  
    
    

Wenn Sie über ein Paar miteinander verknüpfter Dateien (HTML und MASTER) verfügen und Sie die MASTER-Datei bearbeiten, ohne die Verknüpfung zu unterbrechen, werden die Änderungen an der MASTER-Datei gespeichert. Doch Sie können die MASTER-Datei weder einchecken noch veröffentlichen, weshalb die Änderungen nicht auf sinnvolle Weise gespeichert werden. Bei Änderungen an der HTML-Datei wird die MASTER-Datei überschrieben. Wenn Sie die HTML-Datei einchecken oder veröffentlichen, überschreiben die Änderungen an der HTML-Datei alle Änderungen, die an der MASTER-Datei erfolgt sind. Die Änderungen an der MASTER-Datei gehen daraufhin verloren.
  
    
    
Als Entwickler, der mit ASP.NET vertraut ist, können Sie nach Wunsch nur mit der MASTER-Datei arbeiten und die Verknüpfung zwischen den Dateien aufheben. Dazu wählen Sie im Entwurfs-Manager den Befehl **Eigenschaften bearbeiten** für die HTML-Datei aus und deaktivieren das Kontrollkästchen **Zugeordnete Datei**. Sie können später die Verknüpfung zwischen den Datei wieder aktivieren, indem Sie die Eigenschaften bearbeiten und dieses Kontrollkästchen aktivieren. In diesem Fall wird die MASTER-Datei erneut von der HTML-Datei überschrieben, und an der MASTER-Datei erfolgte Änderungen gehen verloren.
  
    
    

## <a name="prepare-the-html-file-for-conversion"></a>Vorbereiten der HTML-Datei auf die Konvertierung
<a name="Prepare"> </a>

Vor der Konvertierung Ihrer HTML-Datei sollten Sie einige bewährte Methoden und Tipps befolgen:
  
    
    

- Berücksichtigen Sie das SharePoint-Seitenmodell. Weitere Informationen finden Sie unter  [Übersicht über das SharePoint-Seitenmodell](overview-of-the-sharepoint-page-model.md). Wenn Sie die HTML-Modelle Ihrer Website entwerfen, verfügen Sie wahrscheinlich über mehrere HTML-Dateien für verschiedene Seitentypen, so z. B. über eine Artikel- oder Kategorieseite, die Webparts enthält, mit denen eine Kategorie von Elementen in einem Katalog angezeigt wird. Doch nur eine HTML-Datei wird in eine Gestaltungsvorlage konvertiert. Eine HTML-Datei kann in eine Gestaltungsvorlage konvertiert werden, doch eine HTML-Datei kann nicht direkt in ein Seitenlayout umgewandelt werden, da für ein Seitenlayout Seitenfelder erforderlich sind.
    
  
- Stellen Sie sicher, dass Ihre HTML-Datei XML-kompatibel ist. Damit die Umwandlung funktioniert, muss die HTML-Datei XML-kompatibel sein. Leider setzt diese Anforderung einige HTML 5-Normen außer Kraft. Beispielsweise können Sie den **Dokumenttyp** **(doctype)** in HTML 5 in Kleinschreibung angeben, während er in XML in Großbuchstaben geschrieben sein muss. Darüber hinaus sollten Sie alle ** \<form\>**-Tags aus der HTML-Datei entfernen. Ziehen Sie in Betracht, Ihre HTML-Datei einer externen XML-Datenprüfung zu unterziehen, um XML-Fehler vor der Konvertierung zu ermitteln.
    
  
- Berücksichtigen Sie diese wichtigen Leitlinien für Ihre CSS-Verweise:
    
  - Platzieren Sie keine **\<Formatvorlagen\>**-Bausteine im ** \<head\> **-Tag. Dieses Formate werden während der Konvertierung entfernt. Stellen Sie stattdessen eine Verknüpfung von Ihrer HTML-Datei zu einer externen CSS-Datei her.
    
  
  - Fügen Sie `ms-design-css-conversion="no"` zum **\<CSS-Link\>**-Tag hinzu, wenn Sie eine Webschriftart verwenden.
    
  
  - Seien Sie vorsichtig, wenn Sie Formatvorlagen auf allgemeine HTML-Tags wie **\<body\>**, **\<div\>** und **\<img\>** anwenden. Alles, was sich in Ihrem SharePoint-Entwurf befindet, einschließlich des Menübands, befindet sich im **\<body\>**-Tag. Formatvorlagen, die Sie in der Regel dem ** \<body\>**-Tag zuweisen, sollten Sie stattdessen **\<div id="s4-bodyContainer"\>** zuweisen, da SharePoint diesen Tag für den Hauptteil der Seite verwendet. Darüber hinaus verwendet SharePoint viele Bilder, die von allen Formatvorlagen, die Sie auf das **\<img\>**-Tag anwenden, beeinflusst werden.
    
  
  - Viele Designer gestalten die Navigation durch Anwenden von Klassen auf **\<ul\>**- und **\<li\>**-Elemente. SharePoint verwendet jedoch dynamische Navigationssteuerelemente, die Sie über Ihre Gestaltungsvorlage aus dem Codeausschnittkatalog hinzufügen können. SharePoint-Navigationssteuerelemente werden standardmäßig Formatvorlagen zugeordnet, die Sie überschreiben müssen.
    
  
- Berücksichtigen Sie diese potenziellen Probleme beim Benennen von Dateien:
    
  - Wenn Sie über Index.html und Index.htm verfügen, haben diese Dateien dieselbe MASTER-Datei.
    
  
  - Wenn Sie über Design/Index.html und Design/SubDesign/Index.html verfügen, können diese Dateien in eigene, getrennte MASTER-Dateien konvertiert werden. Sie werden jedoch im Entwurfs-Manager in der Gestaltungsvorlagenliste als Index.html angezeigt. Um sie eindeutig zu machen, klicken Sie für jede Datei auf die Schaltfläche mit den Auslassungszeichen, um den vollständigen Pfad anzuzeigen.
    
  
- Wenn Sie ein JavaScript-Widget hinzufügen, vergewissern Sie sich, dass sich das Starttag **\<script\>** in einer eigenen Zeile befindet.
    
```
  
<script>
(function( …

```

Geben Sie die Tags nicht in der gleichen Zeile ein (siehe unten).
    


```
  
<Script> (function( …
```

- Ein Verweis auf die JQuery-Bibliothek (ein externer Verweis) muss sich vor dem **\</head\>**-Tag befinden.
    
  

## <a name="convert-the-html-file-into-a-master-page"></a>Konvertieren der HTML-Datei in eine Gestaltungsvorlage
<a name="Convert"> </a>

Bevor Sie eine HTML-Datei konvertieren, müssen Sie zunächst alle Ihre Entwurfsdateien samt Ihrer HTML-Datei hochladen. Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
  
    
    

### <a name="to-convert-the-html-file-into-a-master-file"></a>So konvertieren Sie die HTML-Datei in eine Gestaltungsvorlage


1. Wechseln Sie zu Ihrer Veröffentlichungswebsite.
    
  
2. Wählen Sie in der rechten oberen Ecke der Seite **Einstellungen** und dann **Entwurfs-Manager**.
    
  
3. Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten**.
    
  
4. Wählen Sie **Konvertieren einer HTML-Datei in eine SharePoint-Gestaltungsvorlage**.
    
  
5. Wählen Sie im Dialogfeld **Ein Objekt auswählen** die HTML-Datei aus, die Sie konvertieren möchten.
    
    > [!NOTE]
    > Wenn Sie Ihre Entwurfsdateien hochladen, sollten Sie alle Dateien im Zusammenhang mit einem einzelnen Entwurf in einem eigenen Ordner im Gestaltungsvorlagenkatalog ablegen. Wenn Sie Ihren Entwurfsordner auf das zugeordnete Netzwerklaufwerk kopieren, behält der Gestaltungsvorlagenkatalog Ihre angelegte Ordnerstruktur bei. 
6. Wählen Sie **Einfügen**.
    
    An dieser Stelle konvertiert SharePoint Ihre HTML-Datei in eine MASTER-Datei mit demselben Namen.
    
    Im Entwurfs-Manager wird Ihre HTML-Datei nun mit der Spalte Status mit einem von zwei möglichen Status angezeigt:
    
  - Fehler
    
  
  - **Konvertierung erfolgreich**
    
  
7. Öffnen Sie den Link in der Spalte Status, um eine Vorschau der Datei und etwaige Fehler oder Warnungen zur Gestaltungsvorlage anzuzeigen.
    
    Die Vorschauseite zeigt eine aktuelle Vorschau auf Serverseite Ihrer Gestaltungsvorlage. Oben in der Vorschau werden etwaige Warnungen oder Fehler angezeigt, die Sie ggf. durch Bearbeiten der HTML-Datei in einem HTML-Editor beheben müssen. Fehler müssen korrigiert werden, damit die Gestaltungsvorlage in der Vorschau ordnungsgemäß angezeigt wird.
    
    Weitere Informationen zum Beheben von Fehlern und Warnungen finden Sie unter  [Vorgehensweise: Beheben von Fehlern und Warnungen bei der Vorschau einer Seite in SharePoint](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md).
    
    Weitere Informationen zur Vorschau der Gestaltungsvorlage mit unterschiedlichen Seiten finden Sie unter  [Vorgehensweise: ändern die Vorschauseite in SharePoint-Design-Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).
    
    Die Vorschauseite enthält außerdem einen Ausschnitte-Link in der oberen rechten Ecke. Über diesen Link können Sie den Codeausschnittkatalog öffnen, mit dem Sie statische oder Modellsteuerelemente in Ihrem Entwurf durch dynamische SharePoint-Steuerelemente ersetzt können. Weitere Informationen finden Sie unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).
    
  
8. Bearbeiten zum Korrigieren von Fehlern die HTML-Datei, die sich direkt auf dem Server befindet, mithilfe eines HTML-Editors, mit dem Sie die HTML-Datei auf dem zugeordneten Laufwerk öffnen und bearbeiten können. Bei jeder Speicherung der HTML-Datei werden Änderungen mit der zugeordneten MASTER-Datei synchronisiert.
    
  
9. Nachdem eine Vorschau der Gestaltungsvorlage angezeigt wurde, wird ein **\<div\>**-Tag Ihrer HTML-Datei hinzugefügt. Sie müssen möglicherweise bis zum Ende der Seite scrollen, um das **\<div\>**-Tag zu sehen.
    
    Dieses **\<div\>**-Tag ist im Hauptinhaltsblock vorhanden. Es befindet sich in einem Inhaltsplatzhalter **ContentPlaceHolderMain**. Wenn ein Besucher zur Laufzeit Ihre Website durchsucht und eine Seite anfordert, wird dieser Platzhalter mit Inhalt aus einem Seitenlayout gefüllt, der die Inhalte in einem passenden Inhaltsbereich enthält. Sie sollten das **\<div\>**-Tag dort positionieren, wo Ihre Seitenlayouts in der Gestaltungsvorlage angezeigt werden sollen.
    
    Wenn Ihre HTML-Datei statische oder Modellinhalte im Textkörper der Seite enthält, leiten Sie nun das Entfernen dieser statischen Inhalte aus der HTML-Gestaltungsvorlage ein, und Sie wenden diese Formate auf andere Elemente des SharePoint-Seitenmodells an, z. B. Seitenlayouts, Seitenfeld-Steuerelemente, Codeausschnitte und Anzeigevorlagen. Ein Beispiel finden Sie unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).
    
  

## <a name="understanding-the-html-file-after-conversion"></a>Grundlegendes zur HTML-Datei nach der Konvertierung
<a name="Understand"> </a>

Wenn Sie eine HTML-Datei in eine Gestaltungsvorlage konvertieren, werden der HTML-Datei viele Markupzeilen hinzugefügt. Sie können einen Großteil dieses Markups getrost ignorieren, denn das meiste davon wird nicht im endgültigen Markup Ihrer Website enthalten sein, wenn Sie den Quellcode im Browser anzeigen. Doch dieses Markup ist wichtig für das Konvertieren Ihrer HTML-Datei in die MASTER-Datei, die SharePoint tatsächlich verwendet. Jedes Mal, wenn sie eine Änderung an Ihrer HTML-Datei speichern, ermöglicht dieses SharePoint-Markup, dass dieselbe Änderung im Hintergrund an der zugeordneten MASTER-Datei erfolgt.
  
    
    
Das Markup, das hinzugefügt wird, enthält Tags vor und im **\<head\>**-Tag, Ausschnitte und Inhaltsplatzhalter. Das meiste Markup befindet sich innerhalb von Kommentartags. Immer wenn Sie eine Änderung an der HTML-Datei speichern, entfernt der Konvertierungsprozess die Kommentare, um das enthaltene ASP.NET-Markup zu verwenden.
  
    
    

### <a name="types-of-markup"></a>Arten von Markup

Es folgt eine Übersicht der Arten von Markup, die der HTML-Datei hinzugefügt werden:
  
    
    

- **Dokumenteigenschaften** Das **\<mso\>**-Tag enthält SharePoint-Metadaten, einschließlich Informationen zur Datei selbst und einiger Eigenschaften, die für die erfolgreiche Konvertierung in die MASTER-Datei benötigt werden.
    
```HTML
  
<mso:CustomDocumentProperties>
<mso:HtmlDesignFromMaster msdt:dt="string"></mso:HtmlDesignFromMaster>
<mso:HtmlDesignStatusAndPreview msdt:dt="string">http://[server_name]/sites/PubSite/_catalogs/masterpage/[site_name]/index.html, Conversion successful.</mso:HtmlDesignStatusAndPreview>
<mso:ContentTypeId msdt:dt="string">0x0101000F1C8B9E0EB4BE489F09807B2C53288F0054AD6EF48B9F7B45A142F8173F171BD10003D357F861E29844953D5CAA1D4D8A3A0084F0F9C7FCB65541A59990D173DA60FA</mso:ContentTypeId>
<mso:HtmlDesignAssociated msdt:dt="string">1</mso:HtmlDesignAssociated>
<mso:HtmlDesignConversionSucceeded msdt:dt="string">True</mso:HtmlDesignConversionSucceeded>
</mso:CustomDocumentProperties>
```

- **Registrierung eines SharePoint-Namespace** Das **\<SPM\>**-Tag ("SharePoint-Markup") bietet eine Zeile zur Registrierung eines SharePoint-Namespace.
    
```HTML
  
<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
```

- **Kommentare** Die Tags **\<CS\>** und **\<CE\>** ("Kommentaranfang" und "Kommentarende") werden während des Konvertierungsprozesses ignoriert. Diese Tags dienen zur Analyse der Markupzeilen.
    
```HTML
  
<!--CS: Start Page Head Contents Snippet-->
…
<!--CE: End Page Head Contents Snippet-->

  <!--CS: Start Ribbon Snippet-->
…
<!--CE: End Ribbon Snippet-->

<!--CS: Start PlaceHolderMain Snippet-->
…
<!--CE: End PlaceHolderMain Snippet-->
```

- **Ausschnitte** Die **\<MS\>**- und **\<ME\>**-Tags ("Markup-Anfang" und "Markup-Ende") kennzeichnen den Anfang und das Ende eines SharePoint-Steuerelements oder -Ausschnitts. Ein Ausschnitt ist ein SharePoint-Steuerelement, mit dem Sie SharePoint-Funktionalität zu Ihrer Seite hinzufügen. Mit dem Codeausschnittkatalog können Sie selbst Codeausschnitte hinzufügen. Weitere Informationen finden Sie unter [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).
    
```HTML
  
<!--MS:<SharePoint:RobotsMetaTag runat="server">-->
        <!--ME:</SharePoint:RobotsMetaTag>-->
        <!--MS:<SharePoint:PageTitle runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
                <!--MS:<SharePoint:ProjectProperty Property="Title" runat="server">-->
                <!--ME:</SharePoint:ProjectProperty>-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:PageTitle>-->
        <!--MS:<SharePoint:StartScript runat="server">-->
        <!--ME:</SharePoint:StartScript>-->
        <!--MS:<SharePoint:CssLink runat="server" Version="15">-->
        <!--ME:</SharePoint:CssLink>-->
        <!--MS:<SharePoint:CacheManifestLink runat="server">-->
        <!--ME:</SharePoint:CacheManifestLink>-->
        <!--MS:<SharePoint:PageRenderMode runat="server" RenderModeType="Standard">-->
        <!--ME:</SharePoint:PageRenderMode>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="core.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="menu.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="callout.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="sharing.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="suitelinks.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:CustomJSUrl runat="server">-->
        <!--ME:</SharePoint:CustomJSUrl>-->
        <!--MS:<SharePoint:SoapDiscoveryLink runat="server">-->
        <!--ME:</SharePoint:SoapDiscoveryLink>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaPlaceHolderAdditionalPageHead" Container="false" runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderAdditionalPageHead" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
            <!--MS:<SharePoint:DelegateControl runat="server" ControlId="AdditionalPageHead" AllowMultipleControls="true">-->
            <!--ME:</SharePoint:DelegateControl>-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderBodyAreaClass" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--MS:<SharePoint:CssRegistration Name="Themable/corev15.css" runat="server">-->
        <!--ME:</SharePoint:CssRegistration>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaSPWebPartManager" runat="server">-->
            <!--MS:<WebPartPages:SPWebPartManager runat="server">-->
            <!--ME:</WebPartPages:SPWebPartManager>-->
        <!--ME:</SharePoint:AjaxDelta>-->
```

- **Anzeigen einer Blockvorschau** Die **\<PS\>**- und **\<PE\>**-Tags ("Vorschau-Anfang" und "Vorschau-Ende") umgeben den Bereich eines HTML-Codes, den Sie nicht bearbeiten sollten, da sich dieser Abschnitt nur auf die Entwurfszeit-Vorschau auswirkt. Diese Vorschaubereiche sind eine Momentaufnahme der SharePoint-Steuerelemente, die der Abschnitt einfügt. Eine Vorschau ermöglicht es Ihnen, in einem clientseitigen HTML-Editor effektiver an der HTML-Datei zu arbeiten. Wenn Sie jedoch den Inhalt oder das Format in dieser Vorschau ändern, hat dies keine dauerhaften Auswirkung auf die .master-Datei, die SharePoint letztendlich verwendet. Um einen Ausschnitt zu formatieren, müssen Sie die SharePoint-Formatvorlagen ermitteln und mit Ihren eigenen benutzerdefinierten CSS-Formatvorlagen überschreiben.
    
```HTML
  
<!--PS: Start of READ-ONLY PREVIEW (do not modify) -->
<div class="DefaultContentBlock" style="background:rgb(0, 114, 198); color:white; width:100%; padding:8px; height:64px; overflow:hidden;">The SharePoint ribbon will be here when your file is either previewed on or applied to your site.</div>
<!--PE: End of READ-ONLY PREVIEW -->
```

- **SharePoint-IDs** Zwei der Codeausschnitte, die Ihrer HTML-Datei während der Konvertierung hinzugefügt werden (der Codeausschnitt "Seitenkopfinhalte" und das SharePoint-Menüband), haben eine zugeordnete SharePoint-ID bzw. SID (00 bzw. 02). Diese IDs ermöglichen das Kürzen der Codeausschnitte und vereinfachen das Lesen des HTML-Codes auf der Seite.
    
```HTML
  
<!--SID:00 -->

<!--SID:02 {Ribbon}-->
```


### <a name="added-snippets"></a>Hinzugefügte Codeausschnitte

Wichtig ist es, die beiden Codeausschnitte zu kennen, die Ihrer HTML-Datei hinzugefügt werden. Diese Codeausschnitte werden während der Konvertierung automatisch hinzugefügt. Sie stehen jedoch nicht zum Hinzufügen über den Codeausschnittkatalog zur Verfügung.
  
    
    

- **Das Menüband** Damit Inhaltsautoren Seiten und Inhalte auf Ihrer SharePoint-Website erstellen können, benötigt Ihre Gestaltungsvorlage ein Menüband und das neue "Suite Navigationssteuerelement" von SharePoint. Das Menüband ist in einem Codeausschnitt mit Einschränkung aus Sicherheitsgründen enthalten, sodass, wenn ein Benutzer Ihre Website durchstöbert, das Menüband nur authentifizierten Benutzern und nicht anonymen Benutzern angezeigt wird. Sie können das Menüband an eine andere Position auf der Seite verschieben oder es durch Überschreiben der CSS-Standardklassen formatieren. Jedoch wird das Verschieben oder Neuanordnen der Komponenten (z. B. des Menüs Websiteaktionen), die sich auf dem Menüband befinden, nicht empfohlen.
    
```HTML
  
<!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AnonymousUsersOnly">-->
<!--MS:<wssucw:Welcome runat="server" EnableViewState="false">-->
<!--ME:</wssucw:Welcome>-->
<!--ME:</SharePoint:SPSecurityTrimmedControl>-->
```

- **ContentPlaceHolderMain** Unter dem **\<div id="s4-bodyContainer"\>**-Tag und vor dem schließenden **\</body\>**-Tag fügt der Konvertierungsprozess einen Inhaltsplatzhalter mit dem Namen **PlaceHolderMain** ein. In diesem Codeausschnitt befindet sich das schwarz umrandete, gelbe **\<div\>**, das in der Entwurfsansicht des HTML-Editors oder in der serverseitigen Vorschau im Entwurfs-Manager angezeigt wird.
    
    Dieses **\<div\>** steht für den Bereich, in den der von Ihrem Seitenlayout und Ihren Seiten definierte Inhalt gelangt. Sie müssen den Codeausschnitt **PlaceHolderMain** an die Stellen in Ihrer Gestaltungsvorlage verschieben, die durch Ihre Seitenlayouts gefüllt werden, d. h. in den Bereich Ihres Websiteentwurfs, der auf allen Seiten Ihrer Website nicht identisch ist.
    


```HTML
  
<!--CS: Start PlaceHolderMain Snippet-->
                    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
                    <!--MS:<SharePoint:AjaxDelta ID="DeltaPlaceHolderMain" IsMainContent="true" runat="server">-->
                        <!--MS:<asp:ContentPlaceHolder ID="PlaceHolderMain" runat="server">-->
                            <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
            This div, which you should delete, represents the content area that your Page Layouts and pages will fill. Design your Master Page around this content placeholder.
        
                            </div>
                        <!--ME:</asp:ContentPlaceHolder>-->
                    <!--ME:</SharePoint:AjaxDelta>-->
                    <!--CE: End PlaceHolderMain Snippet-->
```


## <a name="reference-examples-of-sharepoint-markup-added-to-the-html-file"></a>Referenz: Beispiele von zur HTML-Datei hinzugefügtem SharePoint-Markup
<a name="Reference"> </a>

Es folgt ein Beispiel des Markups, das einer HTML-Datei hinzugefügt wird, nachdem sie in eine Gestaltungsvorlage konvertiert wurde.
  
    
    

### <a name="markup-added-to-the-head-tag"></a>Dem \<head\>-Tag hinzugefügtes Markup


```HTML

<head>
        <meta http-equiv="X-UA-Compatible" content="IE=10" />
        <!--CS: Start Page Head Contents Snippet-->
        <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SID:00 -->
        <meta name="GENERATOR" content="Microsoft SharePoint" />
        <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
        <meta http-equiv="Expires" content="0" />
        <!--MS:<SharePoint:RobotsMetaTag runat="server">-->
        <!--ME:</SharePoint:RobotsMetaTag>-->
        <!--MS:<SharePoint:PageTitle runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
                <!--MS:<SharePoint:ProjectProperty Property="Title" runat="server">-->
                <!--ME:</SharePoint:ProjectProperty>-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:PageTitle>-->
        <!--MS:<SharePoint:StartScript runat="server">-->
        <!--ME:</SharePoint:StartScript>-->
        <!--MS:<SharePoint:CssLink runat="server" Version="15">-->
        <!--ME:</SharePoint:CssLink>-->
        <!--MS:<SharePoint:CacheManifestLink runat="server">-->
        <!--ME:</SharePoint:CacheManifestLink>-->
        <!--MS:<SharePoint:PageRenderMode runat="server" RenderModeType="Standard">-->
        <!--ME:</SharePoint:PageRenderMode>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="core.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="menu.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="callout.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="sharing.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="suitelinks.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:CustomJSUrl runat="server">-->
        <!--ME:</SharePoint:CustomJSUrl>-->
        <!--MS:<SharePoint:SoapDiscoveryLink runat="server">-->
        <!--ME:</SharePoint:SoapDiscoveryLink>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaPlaceHolderAdditionalPageHead" Container="false" runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderAdditionalPageHead" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
            <!--MS:<SharePoint:DelegateControl runat="server" ControlId="AdditionalPageHead" AllowMultipleControls="true">-->
            <!--ME:</SharePoint:DelegateControl>-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderBodyAreaClass" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--MS:<SharePoint:CssRegistration Name="Themable/corev15.css" runat="server">-->
        <!--ME:</SharePoint:CssRegistration>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaSPWebPartManager" runat="server">-->
            <!--MS:<WebPartPages:SPWebPartManager runat="server">-->
            <!--ME:</WebPartPages:SPWebPartManager>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--CE: End Page Head Contents Snippet-->
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <!--DC:Business Solutions-->
        <link rel="stylesheet" href="css/style.css" type="text/css" charset="utf-8" />
        <!--[if lte IE 7]>
  <link rel="stylesheet" href="css/ie.css" type="text/css" charset="utf-8"/> 
 <![endif]-->
        <!--[if gte mso 9]><xml>
<mso:CustomDocumentProperties>
<mso:HtmlDesignFromMaster msdt:dt="string"></mso:HtmlDesignFromMaster>
<mso:HtmlDesignStatusAndPreview msdt:dt="string">http://[server_name]/sites/PubSite/_catalogs/masterpage/[site_name]/index.html, Conversion successful.</mso:HtmlDesignStatusAndPreview>
<mso:ContentTypeId msdt:dt="string">0x0101000F1C8B9E0EB4BE489F09807B2C53288F0054AD6EF48B9F7B45A142F8173F171BD10003D357F861E29844953D5CAA1D4D8A3A0084F0F9C7FCB65541A59990D173DA60FA</mso:ContentTypeId>
<mso:HtmlDesignAssociated msdt:dt="string">1</mso:HtmlDesignAssociated>
<mso:HtmlDesignConversionSucceeded msdt:dt="string">True</mso:HtmlDesignConversionSucceeded>
</mso:CustomDocumentProperties>
</xml><![endif]-->
    </head>

```


### <a name="markup-added-after-the-start-body-tag"></a>Hinter dem \<body\>-Anfangstag hinzugefügtes Markup


#### <a name="ribbon-snippet"></a>Codeausschnitt des Menübands


```HTML

<!--CS: Start Ribbon Snippet-->
        <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="wssucw" TagName="Welcome" Src="~/_controltemplates/15/Welcome.ascx"%>-->
        <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" HideFromSearchCrawler="true" EmitDiv="true">-->
            <div id="TurnOnAccessibility" style="display:none" class="s4-notdlg noindex">
                <a id="linkTurnOnAcc" href="#" class="ms-accessible ms-acc-button" onclick="SetIsAccessibilityFeatureEnabled(true);UpdateAccessibilityUI();document.getElementById('linkTurnOffAcc').focus();return false;">
                    <!--MS:<SharePoint:EncodedLiteral runat="server" text="&amp;lt;%$Resources:wss,master_turnonaccessibility%&amp;gt;" EncodeMethod="HtmlEncode">-->
                    <!--ME:</SharePoint:EncodedLiteral>-->
                </a>
            </div>
            <div id="TurnOffAccessibility" style="display:none" class="s4-notdlg noindex">
                <a id="linkTurnOffAcc" href="#" class="ms-accessible ms-acc-button" onclick="SetIsAccessibilityFeatureEnabled(false);UpdateAccessibilityUI();document.getElementById('linkTurnOnAcc').focus();return false;">
                    <!--MS:<SharePoint:EncodedLiteral runat="server" text="&amp;lt;%$Resources:wss,master_turnoffaccessibility%&amp;gt;" EncodeMethod="HtmlEncode">-->
                    <!--ME:</SharePoint:EncodedLiteral>-->
                </a>
            </div>
        <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
        <div id="ms-designer-ribbon">
            <!--SID:02 {Ribbon}-->
            <!--PS: Start of READ-ONLY PREVIEW (do not modify) --><div class="DefaultContentBlock" style="background:rgb(0, 114, 198); color:white; width:100%; padding:8px; height:64px; overflow:hidden;">The SharePoint ribbon will be here when your file is either previewed on or applied to your site.</div><!--PE: End of READ-ONLY PREVIEW -->
        </div>
        <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AnonymousUsersOnly">-->
            <!--MS:<wssucw:Welcome runat="server" EnableViewState="false">-->
            <!--ME:</wssucw:Welcome>-->
        <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
        <!--CE: End Ribbon Snippet-->

```


#### <a name="two-sharepoint-div-tags"></a>Zwei SharePoint \<div\>-Tags


```HTML

<div id="s4-workspace">
            <div id="s4-bodyContainer">

```


### <a name="markup-added-before-the-closing-body-tag-and-two-closing-div-tags"></a>Vor dem schließenden \</body\>-Tag und zwei schließenden \</div\>-Tags hinzugefügtes Markup


```HTML

<div data-name="ContentPlaceHolderMain">
                    <!--CS: Start PlaceHolderMain Snippet-->
                    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
                    <!--MS:<SharePoint:AjaxDelta ID="DeltaPlaceHolderMain" IsMainContent="true" runat="server">-->
                        <!--MS:<asp:ContentPlaceHolder ID="PlaceHolderMain" runat="server">-->
                            <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
            This div, which you should delete, represents the content area that your Page Layouts and pages will fill. Design your Master Page around this content placeholder.
        
                            </div>
                        <!--ME:</asp:ContentPlaceHolder>-->
                    <!--ME:</SharePoint:AjaxDelta>-->
                    <!--CE: End PlaceHolderMain Snippet-->
                </div>

```


## <a name="see-also"></a>Siehe auch
<a name="Additional"> </a>


-  [Übersicht über den Entwurfs-Manager in SharePoint](overview-of-design-manager-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md)
    
  

