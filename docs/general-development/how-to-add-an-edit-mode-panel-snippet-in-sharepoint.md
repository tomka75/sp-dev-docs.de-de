---
title: "Hinzufügen eines Bearbeitungsmodusbereichs-Codeausschnitts in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 39fa1e32-9129-407d-914f-96f4c6e66dc8
ms.openlocfilehash: c5b971b72d8910ac511b27d96a441400afce5323
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-an-edit-mode-panel-snippet-in-sharepoint"></a>Hinzufügen eines Bearbeitungsmodusbereichs-Codeausschnitts in SharePoint

Ein Bearbeitungsmodusbereich ist ein Codeausschnitt, den Sie verwenden können, um Anweisungen oder andere Inhalte für Inhaltsautoren anzuzeigen, die Inhalte dieses Bereichs nur sehen können, wenn sie eine Seite bearbeiten. Dieser Codeausschnitt kann hingegen auch so konfiguriert werden, dass seine Inhalte nur im regulären Modus (Ansichtsmodus) statt im Bearbeitungsmodus angezeigt werden.

## <a name="introduction-to-the-edit-mode-panel"></a>Einführung in die Bearbeitungsbereich Modus
<a name="Introduction"> </a>

Inhaltsautoren mit den erforderlichen Berechtigungen können in einer Veröffentlichungssite erstellen oder Bearbeiten von Seiten, die sich in der Bibliothek für Seiten befinden. In der Regel ein Autor erstellen oder Bearbeiten einer Seite auswählt und dann werden die verschiedenen Seitenfelder Inhalt hinzugefügt.
  
    
    
Wie ein Designer können Sie ein bearbeiten im Bereich zu einer Gestaltungsvorlage oder Seitenlayout hinzufügen, und den Inhalt der das Snippet werden für Inhaltsautoren sichtbar, nur, wenn sie entscheiden, basierend auf dieses Seitenlayout eine Seite oder eine Seite mit der Masterseite verknüpften bearbeiten. Ein bearbeiten im Bereich können Sie beispielsweise den folgenden Inhalt nur für Inhaltsautoren anzuzeigen, wenn die Seite im Bearbeitungsmodus befindet:
  
    
    

- Ein Page-Feld, wie etwa **Schedule Publishing Date**, dies ist wichtig, zu der Inhaltsautor, jedoch nicht für Besucher die Seite auf der online geschalteten Website anzeigen.
    
  
- Eine Beschreibung des welche Art von Inhalt in einem Feld eingegeben werden sollen.
    
  
- Ein Hinweis für Autoren von Inhalten, die sie berücksichtigen sollten, wie die Seite für verschiedenen Gerätekanälen aussieht.
    
  
Sie können auch Links zu anderen Stylesheets in einer bearbeiten im Bereich ablegen, damit Sie verschiedene Formate für den Bearbeitungsmodus im Vergleich zu Ansichtsmodus bereitstellen können.
  
    
    
Sie sollten im Modus bearbeiten, einem Seitenlayout hinzufügen, wenn die Notizen für Autoren von Inhalten für den Inhaltstyp spezifisch sind auf dem dieses Seitenlayout basiert. Sie können auch dieser Ausschnitt in eine Gestaltungsvorlage hinzufügen, wenn die Notizen für Autoren, die alle Seiten gelten, die der Masterseite zugeordnet werden, z. B., ob die Systemsteuerung Anweisungen für die Angabe von Inhalt für ein bestimmtes Gerätekanal enthalten ist, verwendet die Masterseite.
  
    
    
Sie können auch ein bearbeiten im Bereich zum Anzeigen des Inhalts nur im regulären Modus, anstatt Bearbeitungsmodus festlegen, wenn Sie ein Szenario haben, in dem es ist hilfreich oder hilfreiche Inhalte nur für Besucher der Website anzeigen (jedoch nicht content-Autoren) Wenn sie eine Seite bearbeiten.
  
    
    

### <a name="insert-an-edit-mode-panel"></a>Einfügen eines bearbeiten im Bereichs
<a name="InsertSnippet"> </a>

Wie alle Ausschnitte fügen Sie dieser Ausschnitt aus Codeausschnittkatalog. Zum Codeausschnittkatalog zu navigieren, müssen Sie zuerst eine Gestaltungsvorlage oder Seitenlayout bearbeiten auswählen.
  
    
    

### <a name="to-insert-an-edit-mode-panel"></a>So fügen Sie einen Bereich Bearbeitungsmodus ein


1. Wechseln Sie zu Ihrer Veröffentlichungswebsite.
    
  
2. Wählen Sie in der rechten oberen Ecke der Seite das Zahnradsymbol für Einstellungen und dann **Entwurfs-Manager** aus.
    
  
3. Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten** oder **Seitenlayouts bearbeiten** aus, je nachdem, welchen Dateityp Sie bearbeiten.
    
  
4. Wählen Sie den Namen der Masterseite oder Seitenlayout, das Sie den Codeausschnitt hinzufügen möchten.
    
  
5. Wählen Sie zum Öffnen des Codeausschnittkatalogs in der serverseitigen Vorschau in der rechten oberen Ecke **Codeausschnitte** aus.
    
  
6. Klicken Sie im Menüband auf der Registerkarte **Entwurf** wählen Sie **Im Bereich bearbeiten**, und wählen Sie dann den Modus, in dem Sie Ihre Ausschnitt angezeigt werden soll.
    
  
7. Im Codeausschnittkatalog können auf der rechten Seite auf **Infos zu dieser Komponente** klicken oder diese Option auswählen, um Eigenschaftengruppen ein- oder auszublenden, und anschließend die gewünschten benutzerdefinierten Einstellungen konfigurieren.
    
    Im Abschnitt mit dem Namen wichtig enthält die Eigenschaften, die angezeigt werden, die Funktionsweise dieser bestimmten Ausschnitts wichtig sind. Für einen Bereich bearbeiten Modus wird die **PageDisplayMode** -Eigenschaft festgelegt werden, **Edit** oder **Display**, je nach den Modus an, dem Sie auf dem Menüband ausgewählt.
    
  
8. Nachdem Sie Eigenschaften konfiguriert haben, wählen Sie **Aktualisieren**. Dadurch wird der HTML-Codeausschnitt links auf der Seite aktualisiert, sodass das Markup Ihre benutzerdefinierten Einstellungen widerspiegelt. Sie können stets **Zurücksetzen** wählen, um alle Eigenschaften auf ihre Standardeinstellungen zurückzusetzen.
    
  
9. Wählen Sie links im Codeausschnittkatalog unter **HTML-Codeausschnitt** den Befehl **In Zwischenablage kopieren**.
    
  
10. Öffnen Sie in der HTML-Editor das zugeordnete Netzlaufwerk, auf dem Computer, und öffnen Sie die HTML-Datei für die Gestaltungsvorlage oder das Seitenlayout, das Sie den Codeausschnitt hinzufügen möchten. Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
    
  
11. Fügen Sie den Codeausschnitt in der HTML-Datei an der Stelle ein, an der das Markup angezeigt werden soll.
    
    Wenn Sie im Modus bearbeiten, einem Seitenlayout hinzufügen, stellen Sie sicher, dass Sie den Codeausschnitt innerhalb des **PlaceHolderMain** einzufügen, sodass der Bereich Inhaltsautoren im Bearbeitungsmodus sichtbar ist. Können Sie den Codeausschnitt unmittelbar vor einem bestimmten Feld einfügen, oder Sie können eine oder mehrere Seitenfelder innerhalb des Bereichs der Bearbeiten Modus versetzen.
    
  
12. Ersetzen Sie die **<div>**, in dem `class="DefaultContentBlock"` mit Ihren eigenen spezifischen Inhalt - beispielsweise mit Anmerkungen oder Anweisungen, um Inhaltsautoren oder bestimmte Seitenfelder, die für Autoren, aber nicht Besucher der Website hilfreich sind.
    
  
13. Speichern Sie die Seite, und aktualisieren Sie die serverseitige Vorschau im Entwurfs-Manager, um sicherzustellen, dass im Modus bearbeiten wie gewünscht angezeigt wird.
    
  

## <a name="understand-the-snippet-markup"></a>Grundlegendes zu codeausschnittmarkup
<a name="UnderstandMarkup"> </a>

Die beiden wichtigsten Teile eines Ausschnitts bearbeiten im Bereich der **PageDisplayMode** -Eigenschaft und die **<div>** sind, in dem `class="DefaultContentBlock"`. Die **PageDisplayMode** -Eigenschaft bestimmt, ob der Inhalt des Bereichs angezeigt werden, nur im Bearbeitungsmodus oder reguläre/Anzeigemodus (d. h., wenn die Seite nicht im Bearbeitungsmodus befindet).
  
> [!NOTE]
> Diese Eigenschaft wird nicht im Markup angezeigt, es sei denn, Sie ändern den Wert in **Display**. Wenn die Eigenschaft nicht im Markup angezeigt wird, ist der Standardmodus für den Ausschnitt der Bearbeitungsmodus. 
  
    
    

Die **<div>**, wobei `class="DefaultContentBlock"` ist, was Sie mit Ihren eigenen Inhalt ersetzen die anderen Snippets und Steuerelemente enthalten können.
  
    
    



```HTML

<div data-name="EditModePanelShowInEdit">
    <!--CS: Start Edit Mode Panel Snippet-->
    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" PageDisplayMode="Display" CssClass="edit-mode-panel">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
        <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Edit Mode Panel Properties.
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</Publishing:EditModePanel>-->
    <!--CE: End Edit Mode Panel Snippet-->
</div>
```


## <a name="see-also"></a>Siehe auch
<a name="AdditionalResources"> </a>


-  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md)
    
  
-  [Vorgehensweise: Hinzufügen von Ausschnitt glätten Sicherheit in SharePoint](how-to-add-a-security-trim-snippet-in-sharepoint.md)
    
  
-  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint.md)
    
  
-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
    
  

