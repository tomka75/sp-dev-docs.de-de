---
title: "Vorgehensweise Hinzufügen eines Webpart-Zonenausschnitts in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7583b217-200c-4569-8f88-fe975c8ebd72
ms.openlocfilehash: 5085f1a8fa2a79e78cc8c337bab0e03fe924f65d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-add-a-web-part-zone-snippet-in-sharepoint"></a>Vorgehensweise: Hinzufügen eines Webpart-Zonenausschnitts in SharePoint
Eine Webpartzone ist ein Ausschnitt, den Sie einem Seitenlayout hinzufügen können, damit Inhaltsautoren Webparts in dieser Zone hinzufügen, bearbeiten und löschen können.
## <a name="introduction-to-the-web-part-zone-snippet"></a>Einführung in den Codeausschnitt "Webpartzone"
<a name="Introduction"> </a>

Ein Webpart ist ein Serversteuerelement, das eine bestimmte SharePoint-Funktionalität bietet. Eine Webpartzone ist ein Container zum Bestimmen des Layouts, Verhaltens und anderer Eigenschaften der in dieser Zone enthaltenen Webparts. Eine Webpartzone kann beispielsweise angeben, ob die Webparts in der Zone:
  
    
    

- mit einem horizontalen oder vertikalen Layout angeordnet werden. 
    
  
- gemeinsame Benutzeroberflächenelemente wie Titelleiste oder Rand aufweisen.
    
  
- von Inhaltsautoren angepasst werden können, wenn diese eine Seite im Browser bearbeiten.
    
  
- von Websitebesuchern individuell angepasst werden können, die bei der Anzeige einer Seite im Browser eine persönliche Ansicht erstellen können.
    
  
Auf einer Veröffentlichungswebsite können Inhaltsautoren mit den erforderlichen Berechtigungen Seiten erstellen oder in der Bibliothek Seiten enthaltene Seiten bearbeiten. Als Designer können Sie einem Seitenlayout eine Webpartzone hinzufügen. Wenn ein Inhaltsautor eine Seite basierend auf diesem Seitenlayout erstellt oder bearbeitet, kann er Webparts in dieser Zone hinzufügen, bearbeiten oder löschen. Sie können beispielsweise einem Seitenlayout eine Webpartzone hinzufügen, damit Inhaltsautoren folgende Aufgaben ausführen können:
  
    
    

- Anzeigen der Ergebnisse einer Suchabfrage mithilfe eines Inhaltssuche-Webparts. Autoren können die Suchabfrage aktualisieren oder ändern, wenn sich ein suchgesteuertes Webpart in einer Webpartzone befindet.
    
  
- Einbetten von Video- oder Audioclips in eine Webseite mithilfe eines Medienwebparts.
    
  
- Erstellen von Listen mit Hyperlinks, die mit einem Hyperlinkübersicht-Webpart mühelos bearbeitet, gruppiert oder neu angeordnet werden können.
    
  
- Erstellen einer Siteübersicht mit allen Seiten einer Website, die automatisch aktualisiert wird, wenn eine Seite mit einem Inhaltsverzeichnis-Webpart hinzugefügt, gelöscht, umbenannt oder entfernt wird.
    
  

### <a name="when-to-use-web-part-zones"></a>Verwendung von Webpartzonen

Wenn ein Seitenlayout eine oder mehrere Webpartzonen enthält, stehen diese auf allen Seiten zur Verfügung, die dieses Layout verwendet, sodass Autoren Webparts auf diesen Seiten einfügen können. Wenn Sie Autoren das Einfügen von Webparts auf Seiten ermöglichen, verringern sich Ihre Steuerungsmöglichkeiten der Benutzeroberfläche der Website. Ein Autor kann beispielsweise ein Inhaltsverzeichnis-Webpart einer Seite hinzufügen, das Teile Ihrer Website verfügbar macht, die Sie Benutzern auf der aktuellen Seite nicht zur Verfügung stellen möchten.
  
    
    
Wenn Sie die volle Kontrolle darüber wünschen, wie ein Webpart auf Ihrer Website angezeigt wird, und es auf allen Seiten eines bestimmten Typs angezeigt werden soll, fügen Sie das Webpart direkt einem Seitenlayout hinzu. Wenn ein Webpart auf allen Seiten einer Website angezeigt werden soll, können Sie es auch direkt einer Gestaltungsvorlage hinzufügen.
  
    
    

>  **Hinweis:** Webpartzonen stehen für Seitenlayouts, aber nicht für Gestaltungsvorlagen zur Verfügung. Zweck der Zonen ist es, Autoren das Ändern von Webparts zu erlauben, denn Autoren bearbeiten in der Regel keine Gestaltungsvorlagen. 
  
    
    

Sie können einem Seitenlayout auch Webpartzonen hinzufügen, ihre Nutzung jedoch einschränken. Sie können beispielsweise Webparts einer Zone hinzufügen und anschließend eine Eigenschaft dieser Zone so festlegen, dass Inhaltsautoren die Eigenschaften vorhandener Webparts ändern, aber der Zone keine Webparts hinzufügen oder daraus entfernen können. Webpartzonen verfügen über Gruppen von Eigenschaften mit einem doppelten Zweck. Mit einer Untergruppe von Eigenschaften lassen sich das Layout und Format von Webparts auf der Seite organisieren. Mithilfe einer anderen Untergruppe können Sie eine weitere Schutzebene gegen Änderungen der Webparts innerhalb der Zone hinzufügen (sie also sperren).
  
    
    
Sie haben folgende Möglichkeiten, die Darstellung von Webparts auf Ihrer Website zu steuern:
  
    
    

- Webparts direkt einer Gestaltungsvorlage oder einem Seitenlayout hinzufügen. Dies bringt mit sich, dass Inhaltsautoren die Webparts nicht ändern können.
    
  
- Webparts zu Zonen in Seitenlayouts hinzufügen, doch diese Zonen ausschließlich auf die Standardwebparts beschränken, die Sie hinzufügen.
    
  
- Webpartzonen zu Seitenlayouts hinzufügen und Inhaltsautoren die vollständige Kontrolle darüber geben, welche Webparts in diesen Zonen angezeigt und wie diese konfiguriert werden.
    
  
Mit den Eigenschaften einer Webpartzone kann angegeben werden, ob Inhaltsautoren Folgendes ändern dürfen:
  
    
    

- Das Layout von Webparts in der Zone durch Hinzufügen, Löschen, Verschieben oder Verändern der Größe von Webparts.
    
  
- Die Webparteinstellungen für alle Benutzer (die freigegebene Ansicht eines Webparts).
    
  
- Die persönlichen Webparteinstellungen (die persönliche Ansicht eines Webparts).
    
  
Tabelle 1 zeigt wichtige Eigenschaften, die beim Einschränken einer Webpartzone berücksichtigt werden müssen.
  
    
    

**Tabelle 1. Eigenschaften von Webpartzonen zum Einschränken von Inhaltsautoren**


|**Eigenschaftenname**|**Beschreibung**|
|:-----|:-----|
|**AllowLayoutChange** <br/> |Gibt an, ob Webparts innerhalb der Zone geschlossen, minimiert, gelöscht oder wiederhergestellt werden können.  <br/> Bei Festlegung auf **False** können Benutzer Webparts in der Zone nicht schließen, minimieren, löschen oder wiederherstellen, nicht in eine andere Zone ziehen und nicht neu anordnen oder innerhalb der Zone verschieben. Benutzer können außerdem keine Webparts aus dem Webpartkatalog hinzufügen. Zudem sind mehrere Eigenschaften deaktiviert, die sich auf die Benutzeroberfläche von Webparts in der Zone auswirken. Diese Eigenschaft wirkt sich nicht auf die Fähigkeit aus, das Layout programmgesteuert zu ändern.<br/> Bei Festlegung auf **True** können Benutzer mit den entsprechenden Berechtigungen diese Aktionen ausführen.  <br/> |
|**LockLayout** <br/> |Gibt an, ob Webparts innerhalb der Zone hinzugefügt, gelöscht oder verschoben werden können bzw. ob ihre Größe geändert werden kann. Diese Eigenschaft funktioniert unabhängig davon gleich, ob die Webpartseite in der persönlichen oder freigegebenen Ansicht angezeigt wird.<br/>  Bei Festlegung auf **True** sind die folgenden spezifischen Webparteigenschaften für jedes Webpart in der Zone betroffen: **Zone (ZoneID)**, **Reihenfolge der Teile (PartOrder)**, **Auf Seite sichtbar (IsVisible)**, **Höhe (Height)**, **Breite (Width)**, **Schließen zulassen (AllowRemove)** und **IsIncluded** (der Befehl **Schließen** im Menü **Webpart**). Andere Webparteigenschaften sind nicht betroffen.  <br/> Bei Festlegung auf **False** bestimmen die Webparteigenschaften (gemeinsam mit den entsprechenden Websiteberechtigungen), ob Änderungen erfolgen dürfen.  <br/> |
|**AllowCustomization** <br/> |Gibt an, ob freigegebene Eigenschaftenwerte von Webparts innerhalb der Zone geändert werden können.  <br/> Bei Festlegung auf **True** können Benutzer mit den entsprechenden Berechtigungen Änderungen an der Webparts in der Zone für alle Benutzer vornehmen.  <br/> Bei Festlegung auf **False** können Benutzer auf der Benutzeroberfläche der freigegebenen Ansicht keine Änderungen an den Webparts in der Zone vornehmen. Änderungen können jedoch weiter programmgesteuert und über die Seite Webpartwartung erfolgen.  <br/> |
|**AllowPersonalization** <br/> |Gibt an, ob persönliche Eigenschaftenwerte von Webparts innerhalb der Zone geändert werden können.  <br/> Bei Festlegung auf **True** können Benutzer mit den entsprechenden Berechtigungen persönliche Änderungen an den Webparts in der Zone vornehmen.  <br/> Bei Festlegung auf **False** können Benutzer auf der Benutzeroberfläche keine persönlichen Änderungen vornehmen, es sei denn, das Webpart ist privat und sie verfügen über die benötigten Berechtigungen.  <br/> |
   

> **Hinweis:** Sie können keine Webpartzone in einen Gerätekanalbereich einfügen. Wenn Sie zulassen möchten, dass Autoren Webparts zu einer Seite hinzufügen können, und wenn Sie sich keine Sorgen über die Seitengewichtung für mobile Geräte machen, können Sie ein Rich-Text-Editor-Seitenfeld in einen Gerätekanalbereich einfügen und dann die Autoren anweisen, Webparts dort hinzuzufügen. Sie können Webparts direkt zu einem Gerätekanalbereich (ohne eine Webpartzone) hinzufügen. Weitere Informationen finden Sie unter [Vorgehensweise: Hinzufügen eines Gerätekanalbereich-Ausschnitts in SharePoint](how-to-add-a-device-channel-panel-snippet-in-sharepoint.md). 
  
    
    


## <a name="inserting-a-web-part-zone-snippet"></a>Einfügen eines Webpartzone-Ausschnitts
<a name="InsertSnippet"> </a>

Wie alle Codeausschnitte können Sie diesen Codeausschnitt aus dem Codeausschnittkatalog hinzufügen. Sie müssen zunächst ein zu bearbeitendes Seitenlayout auswählen, um zum Codeausschnittkatalog zu gelangen. Sie können Webpartzonen zwar Seitenlayouts, aber nicht Gestaltungsvorlagen hinzufügen.
  
    
    

### <a name="to-insert-a-web-part-zone-snippet"></a>So fügen Sie den Codeausschnitt "Webpartzone" ein


1. Wechseln Sie zu Ihrer Veröffentlichungswebsite.
    
  
2. Wählen Sie in der rechten oberen Ecke der Seite das Zahnradsymbol für Einstellungen und dann **Entwurfs-Manager** aus.
    
  
3. Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Seitenlayouts bearbeiten** aus.
    
  
4. Wählen Sie den Namen des Seitenlayouts aus, dem Sie den Codeausschnitt hinzufügen möchten.
    
  
5. Wählen Sie zum Öffnen des Codeausschnittkatalogs in der serverseitigen Vorschau in der rechten oberen Ecke **Codeausschnitte** aus.
    
  
6. Wählen Sie auf dem Menüband auf der Registerkarte **Entwurf** die Option **Webpartzone** aus.
    
  
7. Im Codeausschnittkatalog können auf der rechten Seite auf **Infos zu dieser Komponente** klicken oder diese Option auswählen, um Eigenschaftengruppen ein- oder auszublenden, und anschließend die gewünschten benutzerdefinierten Einstellungen konfigurieren.
    
    Der Abschnitt **Wichtig** enthält die Eigenschaften, die bekannt sein müssen, um die Funktionsweise dieses bestimmten Codeausschnitts zu kennen. Für eine Webpartzone hat der Codeausschnitt eine eindeutige ID. Nachdem Sie den Codeausschnitt in Ihr Seitenlayout kopiert haben, dürfen Sie diese ID nicht wiederverwenden. Wenn Sie einen weiteren Codeausschnitt "Webpartzone" hinzufügen möchten, wählen Sie **Aktualisieren**, um eine neue ID für den nächsten Codeausschnitt zu generieren.
    
    Eine Beschreibung der Eigenschaften, die erforderlich sind, um eine Webpartzone einzuschränken (**LockLayout**, **AllowCustomization** und **AllowPersonalization**) finden Sie in Tabelle 1.
    
    > **Hinweis:** Sie werden möglicherweise feststellen, dass einige Eigenschaftennamen im Eigenschaftenraster des Codeausschnittkatalogs fett formatiert sind. Diese Eigenschaften besitzen Werte, die von der Standardeinstellung für diese Komponente geändert wurden, diese Eigenschaften sind jedoch für ein Designer-Szenario nicht zwingend relevant. In anderen Worten: Eine Eigenschaft ist möglicherweise fett formatiert, aber nicht notwendigerweise wichtig für Ihr Szenario. 
8. Nachdem Sie Eigenschaften konfiguriert haben, wählen Sie **Aktualisieren**. Dadurch wird der HTML-Codeausschnitt links auf der Seite aktualisiert, sodass das Markup Ihre benutzerdefinierten Einstellungen widerspiegelt. Sie können stets **Zurücksetzen** wählen, um alle Eigenschaften auf ihre Standardeinstellungen zurückzusetzen.
    
  
9. Wählen Sie links im Codeausschnittkatalog unter **HTML-Codeausschnitt** den Befehl **In Zwischenablage kopieren**.
    
  
10. Öffnen Sie im HTML-Editor das zugeordnete Netzlaufwerk auf dem Computer, und öffnen Sie dann die HTML-Datei für die Gestaltungsvorlage oder das Seitenlayout, der bzw. dem Sie den Codeausschnitt hinzufügen.
    
    Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
    
  
11. Fügen Sie den Codeausschnitt in der HTML-Datei an der Stelle ein, an der das Markup angezeigt werden soll.
    
    Wenn Sie den Codeausschnitt dem Seitenlayout hinzufügen, vergewissern Sie sich, dass Sie den Codeausschnitt innerhalb des **PlaceHolderMain**-Tags einfügen.
    
  
12. Ersetzen Sie im **<div>**-Tag  `class="DefaultContentBlock"` durch Ihren eigenen spezifischen Inhalt.
    
  
13. Wenn Sie die Zone vorab mit Webparts auffüllen möchten, um z. B. festzulegen, dass Inhaltsautoren nur vorhandene Webparts ändern, aber keine neuen hinzufügen dürfen, fügen Sie Webpart-Codeausschnitte dort ein, wo das **<!--DC … -->**-Tag angezeigt wird.
    
  
14. Speichern Sie die Seite, und aktualisieren Sie anschließend im Entwurfs-Manager die serverseitige Vorschau, um sicherzustellen, dass die Seite wie gewünscht angezeigt wird.
    
  

## <a name="understanding-the-snippet-markup"></a>Grundlegendes zum Codeausschnittmarkup
<a name="UnderstandMarkup"> </a>

Die beiden wichtigsten Teile eines Webpartzonen-Codeausschnitts sind die Eigenschaft **ID** und der Kommentar **<!--DC … -->**. Jede Zone muss eine eindeutige ID haben. Wenn Sie Ihrem Seitenlayout mehr als eine Webpartzone hinzufügen möchten, wählen Sie im Codeausschnittkatalog **Aktualisieren** aus, bevor Sie die einzelnen Codeausschnitte kopieren, damit eine neue ID generiert wird. Der Kommentar **<!--DC … -->** muss durch Webparts ersetzt werden, die standardmäßig in der Zone angezeigt werden sollen.
  
    
    
Der folgende Code enthält weitere Eigenschaft zum Einschränken, wie Inhaltsautoren Zonen verwenden können ( **AllowCustomization**, **AllowPersonalization** und **LockLayout**).
  
    
    

>  **Hinweis:** Die Eigenschaften **AllowCustomization**, **AllowPersonalization** und **LockLayout** werden nur dann im Markup angezeigt, wenn Sie ihre Standardwerte im Eigenschaftenraster ändern.
  
    
    




```HTML

<div data-name="WebPartZone">
    <!--CS: Start Web Part Zone Snippet-->
    <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <div xmlns:ie="ie">
        <!--MS:<WebPartPages:WebPartZone runat="server" ID="x0e5f5212505f48a9aac43df13eeae4f9" AllowCustomization="True" AllowPersonalization="False" FrameType="TitleBarOnly" LockLayout="True" Orientation="Vertical">-->
            <!--MS:<ZoneTemplate>-->
               <!--DC: Replace this comment with default web parts for new pages. -->
            <!--ME:</ZoneTemplate>-->
        <!--ME:</WebPartPages:WebPartZone>-->
    </div>
    <!--CE: End Web Part Zone Snippet-->
</div>

```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="AdditionalResources"> </a>


-  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md)
    
  
-  
  [WebPartZone-Klasse](http://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.webparts.webpartzone.aspx)
    
  
-  
  [WebPartZoneBase-Eigenschaften](http://msdn.microsoft.com/en-us/library/335sw9k3.aspx)
    
  
-  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint.md)
    
  
-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
    
  

