---
title: "Hinzufügen eines Gerätekanalbereich-Codeausschnitts in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 612780a8-6267-49f6-a32d-33600bb5f6b4
ms.openlocfilehash: b5a208a87ee7b8af55fa6c6c1c96a0ae11df5de8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-device-channel-panel-snippet-in-sharepoint"></a>Hinzufügen eines Gerätekanalbereich-Codeausschnitts in SharePoint

Ein Gerätekanalbereich ist ein Codeausschnitt, den Sie einer Gestaltungsvorlage oder einem Seitenlayout hinzufügen können, um zu steuern, welche Inhalte für jeden von Ihnen erstellten Kanal gerendert werden. Der Hauptzweck eines Gerätekanalbereichs ist die selektive Anzeige verschiedener Seitenfelder in verschiedenen Kanälen eines einzigen Seitenlayouts.

## <a name="introduction-to-the-device-channel-panel-snippet"></a>Einführung in den Codeausschnitt Gerät Channel-Systemsteuerung
<a name="Introduction"> </a>

Ein Gerät Channel Bereich ist ein Steuerelement, das Sie zu einer Gestaltungsvorlage oder Seitenlayout zu steuern, welche Inhalte in den einzelnen Kanälen gerendert wird, die Sie erstellen hinzufügen können. Ein Gerät Channel Bereich ist ein Container, der einen oder mehrere Kanäle angibt; Wenn eine oder mehrere dieser Kanäle aktiviert sind, wenn die Seite gerendert wird, werden alle Inhalte des Bereichs Channel Gerät auch gerendert. Ein Gerät Channel-Systemsteuerung kann nahezu alle Arten von Inhalten, einschließlich einer Verknüpfung zu einer CSS-Datei oder eine JS-Datei enthalten. Es ist eine einfache Möglichkeit, bestimmte Inhalte für bestimmte Kanäle enthalten.
  
    
    
Möglicherweise ist das am häufigsten verwendete Szenario für die Verwendung von Gerätekanalbereiche Teile der ein Seitenlayout für bestimmte Kanäle einschließen. Beispielsweise können Sie ein Seitenlayout mit separaten Textfelder für eine lange Begrüßung und eine kurze Begrüßung verfügen. Indem Sie die Seitenfelder in Gerätekanalbereiche platzieren, können Sie die kurze Begrüßung nur für Telefone und die lange Grußformel nur auf dem Desktop anzeigen. Der Inhalt eines Bereichs Channel Gerät wird nicht angezeigt, auf Kanäle nicht enthalten - tatsächlich der Inhalt wird nicht wiedergegeben, die verhindern, dass Bytes Wechsel zu über das Netzwerk. Aus diesem Grund ist mit Gerätekanalbereiche eine bessere Möglichkeit zum Anzeigen von Inhalten auf bestimmte Kanäle als eine CSS-Klasse mit  `Display:None` , da Gerätekanalbereiche Hilfe, um die Seite Gewichtung für einen bestimmten Kanal zu verringern.
  
    
    
Sie können auch Gerätekanalbereiche auf Gestaltungsvorlagen. Wenn Sie eine Gestaltungsvorlage, die zwei unterschiedliche Geräte (oder zwei verschiedenen Browsern) bewältigen kann mit nur minimale Änderungen verfügen, können Sie auf den Inhalt auf der Masterseite enthalten, die entweder dieser Geräte spezifisch sind beispielsweise Gerätekanalbereiche verwenden.
  
    
    
Es gibt zwei Einschränkungen der Kanal mithilfe eines Geräts:
  
    
    

- **Anzeigevorlagen** Da Anzeigevorlagen auf dem Client gerendert werden und Gerätekanalbereiche auf dem Server ausgeführt werden, nicht Gerät Channel Bereichs innerhalb einer Anzeigevorlage verwendet werden. Verwenden Sie stattdessen Sie sollten zwei verschiedene Inhaltssuche-Webparts innerhalb der Gerätekanalbereiche auf das Seitenlayout, oder verwenden Sie die JavaScript-Variable auf das Verhalten auslösen innerhalb der Anzeigevorlage selbst gewünschten.
    
  
- **Webpartzonen** Eine Webpartzone in einem Gerät Channel Bereich kann nicht eingefügt werden. Wenn Sie zulassen Autoren Webparts zu einer Seite hinzufügen möchten, und wenn Sie nicht die Seite Gewichtung für mobile Geräte besorgt sind, können Sie ein Seitenfeld Rich-Text-Editor zu einem Gerät Channel-Element hinzufügen, und weisen Sie Autoren Webparts hinzufügen vorhanden. Sie können Webparts direkt zu einem Gerät Channel-Element (ohne eine Webpartzone) hinzufügen.
    
  

## <a name="inserting-a-device-channel-panel-snippet"></a>Einen Gerät Channel Systemsteuerung Ausschnitt einfügen
<a name="InsertSnippet"> </a>

Wie alle Ausschnitte fügen Sie einen Gerät Channel Systemsteuerung Ausschnitt aus Codeausschnittkatalog. Zum Codeausschnittkatalog zu navigieren, müssen Sie zuerst eine Gestaltungsvorlage oder Seitenlayout bearbeiten auswählen.
  
    
    

### <a name="to-insert-a-device-channel-panel-snippet"></a>So fügen Sie ein Gerät Channel Systemsteuerung Ausschnitt ein


1. Wechseln Sie zu Ihrer Veröffentlichungswebsite.
    
  
2. Wählen Sie in der rechten oberen Ecke der Seite das Zahnradsymbol für Einstellungen und dann **Entwurfs-Manager** aus.
    
  
3. Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten** oder **Seitenlayouts bearbeiten** aus, je nachdem, welchen Dateityp Sie bearbeiten.
    
  
4. Wählen Sie den Namen der Masterseite oder Seitenlayout, das Sie den Codeausschnitt hinzufügen möchten.
    
  
5. Wählen Sie zum Öffnen des Codeausschnittkatalogs in der serverseitigen Vorschau in der rechten oberen Ecke **Codeausschnitte** aus.
    
  
6. Wählen Sie auf dem Menüband auf der Registerkarte **Entwurf** **Gerät Channel Systemsteuerung** aus.
    
  
7. Im Codeausschnittkatalog können auf der rechten Seite auf **Infos zu dieser Komponente** klicken oder diese Option auswählen, um Eigenschaftengruppen ein- oder auszublenden, und anschließend die gewünschten benutzerdefinierten Einstellungen konfigurieren.
    
    Im Abschnitt mit dem Namen **Wichtig** enthält die Eigenschaften, die-Taste, um die Funktionsweise dieser bestimmten Ausschnitts sind. Für ein Gerät Channel-Bereich ist die **IncludedChannels**-Eigenschaft die wichtigste. Geben Sie für diese Eigenschaft den Alias des einzelnen Gerätekanal, die Sie den Inhalt im Kanal dieses Gerät anzeigen möchten. Wenn Sie mehr als einen Alias eingeben, trennen Sie die einzelnen durch ein Komma.
    
    > [!NOTE]
    > Wenn Sie den Alias eines Kanals in der Liste „Gerätekanäle“ bearbeiten, müssen Sie den Alias manuell suchen und alle Vorkommen in Ihren Designdateien aktualisieren. Zudem müssen Sie die **IncludedChannels**-Eigenschaft für jeden Gerätekanalbereich aktualisieren, der den Alias verwendet.

8. Nachdem Sie alle anderen Eigenschaften konfiguriert haben, wählen Sie **Aktualisieren**. Den HTML-Codeausschnitt auf der linken Seite der Seite aktualisiert, damit das Markup Ihre benutzerdefinierten Einstellungen widerspiegelt. Sie können immer auf alle Eigenschaften auf die Standardeinstellungen zurück **Zurücksetzen** auswählen.
    
  
9. Wählen Sie links im Codeausschnittkatalog unter **HTML-Codeausschnitt** den Befehl **In Zwischenablage kopieren**.
    
  
10. Öffnen Sie im HTML-Editor das zugeordnete Netzlaufwerk auf dem Computer, und öffnen Sie dann die HTML-Datei für die Gestaltungsvorlage oder das Seitenlayout, der bzw. dem Sie den Codeausschnitt hinzufügen.
    
    Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
    
  
11. Fügen Sie den Codeausschnitt in der HTML-Datei an der Stelle ein, an der das Markup angezeigt werden soll.
    
    Wenn Sie den Codeausschnitt, einem Seitenlayout hinzufügen, stellen Sie sicher, dass Sie den Codeausschnitt innerhalb des **PlaceHolderMain**einfügen.
    
  
12. Ersetzen Sie im **<div>**-Tag  `class="DefaultContentBlock"` durch Ihren eigenen spezifischen Inhalt.
    
    In der Regel, wenn Sie ein Gerät Channel-Systemsteuerung einem Seitenlayout hinzufügen, ersetzen Sie die **<div>** durch Kopieren Seitenfelder innerhalb des Bereichs.
    
  
13. Speichern Sie die Seite, und aktualisieren Sie die serverseitige Vorschau im Entwurfs-Manager, um sicherzustellen, dass das Gerät Channel wird angezeigt, wie erwartet.
    
    Um eine Vorschau die Systemsteuerung auf unterschiedliche Kanäle anzeigen, können Sie auf die URL Abfragezeichenfolgen-Parameter hinzufügen. Beispielsweise können Sie auf die URL einer beliebigen Seite in der serverseitigen Vorschau der Abfrage Zeichenfolge variabler  `"DeviceChannel=YourChannelAlias"` anfügen.
    
  

## <a name="understanding-the-snippet-markup"></a>Grundlegendes zum Codeausschnittmarkup
<a name="UnderstandMarkup"> </a>

Die beiden wichtigsten Teile eines Ausschnitts Gerät Channel Systemsteuerung sind die **IncludedChannels** -Eigenschaft und die **<div>**, in dem `class="DefaultContentBlock"`. Standardmäßig ist die **IncludedChannels** -Eigenschaft leer. Geben Sie im Abschnitt **wichtige** des Eigenschaftenrasters Aliase, durch Kommas getrennt, der die Gerätekanäle, die Sie den Inhalt in diesem Bereich anzeigen möchten.
  
> [!NOTE]
> Wenn Sie einen Alias in der Liste „Gerätekanäle“ ändern, müssen Sie alle Vorkommen des Alias im Markup ändern, einschließlich in der **IncludedChannels**-Eigenschaft für jeden Gerätekanalbereich, der den Alias verwendet.
  
    
    

Die **<div>**, in dem `class="DefaultContentBlock"` ersetzt werden soll, mit dem jeweils spezifischen Inhalt, anzuzeigende für Kanäle enthalten. Ein Gerät Channel-Systemsteuerung kann nahezu alle Arten von Inhalten, einschließlich einer Verknüpfung zu einer CSS-Datei oder eine JS-Datei enthalten. Das häufigste Szenario für die Verwendung von Gerätekanalbereiche ist bestimmte Seitenfelder in einem Seitenlayout für bestimmte Kanäle eingeschlossen. In diesem Fall kopieren Sie das Position der **<div>** innerhalb des Bereichs des Geräts Channel Feld Seitenmarkup.
  
    
    



```HTML

<div data-name="DeviceChannelPanel">
    <!--CS: Start Device Channel Panel Snippet-->
    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:DeviceChannelPanel runat="server" IncludedChannels="MyPhoneChannel, MyTabletChannel">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
       <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Device Channel Panel Properties.    
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</Publishing:DeviceChannelPanel>-->
    <!--CE: End Device Channel Panel Snippet-->
</div>

```


## <a name="see-also"></a>Siehe auch
<a name="AdditionalResources"> </a>


-  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md)
    
  
-  [SharePoint-Design-Manager-Gerätekanäle](sharepoint-design-manager-device-channels.md)
    
  
-  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint.md)
    
  
-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
    
  

