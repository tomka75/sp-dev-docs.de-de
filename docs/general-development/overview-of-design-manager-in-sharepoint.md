---
title: "Übersicht über den Entwurfs-Manager in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 29834b3f-3815-4347-91d3-296387663114
ms.openlocfilehash: 253207ef3191f5868cd69b273c5e42c4b54ac410
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="overview-of-design-manager-in-sharepoint"></a>Übersicht über den Entwurfs-Manager in SharePoint
In diesem Artikel erfahren Sie, wie Sie den Entwurfs-Manager zum Branding von SharePoint-Websites verwenden können. Der Entwurfs-Manager ist ein Veröffentlichungsfeature, das auf Veröffentlichungswebsites in SharePoint und Office 365 verfügbar ist. 
## <a name="introduction-to-design-manager"></a>Einführung in den Entwurfs-Manager
<a name="Introduction"> </a>

Ihre SharePoint-Website soll Ihre Marke repräsentieren und nicht „wie SharePoint“ aussehen? Mit einem benutzerdefinierten Design und Entwurfs-Manager können Sie das sicherstellen. Der Entwurfs-Manager ist ein Feature in SharePoint und macht es einfacher, vollständig individuell angepasste, pixelgenaue Designs zu erstellen, mit den Ihnen bereits vertrauten Webdesigntools. Der Entwurfs-Manager ist ein Veröffentlichungsfeature, das auf Veröffentlichungswebsites in SharePoint und Office 365 verfügbar ist. 
  
    
    
Mit dem Entwurfs-Manager können Sie mithilfe eines beliebigen Webdesigntools oder eines von Ihnen bevorzugten HTML-Editors nur mit HTML und CSS ein visuelles Design für Ihre Website erstellen und dieses Design dann in SharePoint hochladen. Der Entwurfs-Manager ist die zentrale Schnittstelle, über die Sie sämtliche Aspekte eines benutzerdefinierten Designs verwalten.
  
    
    
Die Erstellung des visuellen Designs einer Websites erfolgt häufig im Rahmen eines umfangreicheren Prozesses, an dem mehrere Personen oder Organisationen beteiligt sind. Eine allgemeinere Übersicht über die Aufgaben finden Sie unter  [Design und Branding in SharePoint](http://go.microsoft.com/fwlink/?LinkId=262838)
  
    
    
Im Allgemeinen führt der Webdesigner die folgenden Aufgaben durch:
  
    
    

- Verstehen der wesentlichen SharePoint-Designkonzepte. Weitere Informationen finden Sie unter  [Übersicht über das SharePoint-Seitenmodell](overview-of-the-sharepoint-page-model.md).
    
  
- Erstellen eines Modells des Designs in HTML and CSS. Die Designerstellung ist eine zentrale Kompetenz eines Webdesigners und wird in diesem Artikel nicht behandelt.
    
  
- Implementieren des Designs mithilfe des Entwurfs-Managers. Abschnitte dieses Artikels bieten eine Einführung zum Entwurfs-Manager und den Prozess der Verwendung des Entwurfs-Managers zum Implementieren eines visuellen Designs.
    
 


## <a name="use-design-manager-to-implement-a-design"></a>Implementieren eines Designs mit dem Entwurfs-Manager
<a name="Use"> </a>

Wenn Sie den Entwurfs-Manager öffnen, sehen Sie auf der linken Seite eine Reihe von Links, welche die allgemeinen Aufgaben darstellen, die Sie durchführen müssen. Je nach Ihrem Design und den Anforderungen Ihrer Website müssen Sie möglicherweise nicht alle diese Aufgaben durchführen, und Sie müssen sie nicht unbedingt in dieser Reihenfolge durchführen. Diese Abfolge ist dennoch ein hilfreicher Ausgangspunkt.
  
    
    

### <a name="before-you-begin"></a>Bevor Sie beginnen:

Bevor Sie den Entwurfs-Manager verwenden können, benötigen Sie ein Design. Sie können Ihr eigenes erstellen oder eine fertige Websitevorlage verwenden. Ein "Design" ist einfach eine Gruppe von Dateien, die das visuelle Design Ihrer Website implementieren. Diese Gruppe umfasst i. d. R. Folgendes:
  
    
    

- Mindestens eine HTML-Datei, die in eine SharePoint-Gestaltungsvorlage umgewandelt wird
    
  
- Eine oder mehrere CSS-Dateien
    
  
- JavaScript-Dateien
    
  
- Bilder
    
  
- Andere unterstützende Dateien
    
  
Wenn Sie Ihre Website in HTML und CSS modellieren, haben Sie wahrscheinlich mehrere HTML-Dateien, die Designs dafür implementieren, wie verschiedene Seiten oder Typen von Seiten angezeigt werden sollen. Bedenken Sie, dass nur eine dieser HTML-Dateien in die Gestaltungsvorlage konvertiert wird (es sein denn, Sie haben mehrere Gerätekanäle, wobei jeder Kanal über eine eigene Gestaltungsvorlage verfügt – siehe folgender Abschnitt). Nachdem Sie den Entwurfs-Manager zum Erstellen anderer Websiteelemente wie Seitenlayouts oder Anzeigevorlagen verwendet haben, können Sie Markup von Ihren HTML-Modellen in die HTML- und CSS-Dateien übertragen, die mit der Gestaltungs- oder Anzeigevorlage verknüpft sind.
  
    
    
Bevor Sie beginnen, benötigen Sie auch die erforderlichen SharePoint-Berechtigungen. Um den Entwurfs-Manager zu verwenden, benötigen Sie mindestens die Designer-Berechtigungsstufe.
  
    
    

### <a name="manage-device-channels"></a>Verwalten von Gerätekanälen

Bereits bevor Sie Ihre Website entwerfen, sollten Sie bedenken, auf welche Geräte Ihre Website ausgelegt sein soll, und wie die Benutzererfahrung auf jedem Gerät aussehen soll. So möchten Sie das Design Ihrer Website vielleicht für eine bestimmte Klasse von Smartphones oder Tablet-PCs optimieren.
  
    
    
Je nachdem, welche Kanäle Sie definieren, möchten Sie vielleicht mehrere Designs und damit mehrere HTML-Dateien verwenden, wobei jede Datei in eine eigene Gestaltungsvorlage konvertiert wird. Außerdem kann jede HTML-Datei (und somit jede Gestaltungsvorlage) ihre eigene CSS-Datei referenzieren. Gerätekanäle sollten gleich am Anfang, bevor Sie mit dem Entwerfen Ihrer Website beginnen, berücksichtigt werden.
  
    
    
Mit Gerätekanälen können Sie eine einzelne Veröffentlichungswebsite auf verschiedene Weise rendern, indem Sie unterschiedlichen Geräten unterschiedliche Designs zuordnen. Jeder Kanal kann seine eigene Gestaltungsvorlage besitzen, die mit einem Stylesheet verknüpft ist, das für ein bestimmtes Gerät optimiert ist. Jeder Kanal gibt die Benutzer-Agent-Unterzeichenfolge für ein oder mehrere Geräte an, wie z. B. "Windows Phone OS". Dies sind Regeln, die festlegen, welche Geräte in jeden Kanal eingeschlossen werden. Wenn Besucher dann zu Ihrer Website navigieren, erfasst jeder Kanal den Datenverkehr für das entsprechende Gerät oder die entsprechende Geräteklasse, wie z. B. Windows Phones, und Besuchern wird Ihre Website in einem für ihr jeweiliges Gerät optimierten Design angezeigt.
  
    
    
Gerätekanäle werden in einer SharePoint-Liste erstellt und gespeichert, in der die Reihenfolge eine Rolle spielt, da Gerätekanäle auch Ranglisten haben. Gerätekanäle sind in der Liste von oben nach unten geordnet, und die Einschlussregeln werden in dieser Reihenfolge verarbeitet. Das bedeutet, dass Gerätekanäle mit den spezifischsten Regeln an oberster Stelle stehen sollten. So sollte etwa ein Kanal, der auf "Windows Phone OS 7.0" ausgelegt ist, über einem Kanal stehen, der auf "Windows Phone OS" ausgelegt ist.
  
    
    

### <a name="upload-design-files"></a>Hochladen von Designdateien

Wenn Sie ein Design erstellen, können Sie einen beliebigen HTML-Editor verwenden und mit Dateien lokal auf Ihrem Computer arbeiten. Sie müssen diese Dateien aber letztendlich in die Gestaltungsvorlagengalerie Ihrer SharePoint-Website hochladen, sodass Sie Ihr Design mithilfe des Entwurfs-Managers konvertieren, in der Vorschau anzeigen und optimieren können.
  
    
    
Der einfachste Weg, Designdateien hochzuladen und weiter daran zu arbeiten, ist, der Gestaltungsvorlagengalerie Ihrer SharePoint-Website ein Laufwerk auf Ihrem Computer zuzuordnen. Dadurch wird ein Ordner auf Ihrem Computer mit der Gestaltungsvorlagengalerie verbunden, sodass Sie an Dateien arbeiten können, die sich auf dem Server in SharePoint befinden, als ob es sich um lokale Dateien handeln würde.
  
    
    
Nachdem Sie ein Netzwerklaufwerk zugeordnet haben, können Sie Ihr Design in SharePoint hochladen, indem Sie die Designdateien einfach in einen Ordner auf dem zugeordneten Laufwerk Ihres Computers hochladen, der mit SharePoint verbunden ist. Nachdem Sie Ihre HTML-Datei in eine SharePoint-Gestaltungsvorlage konvertiert und Seitenlayouts und Anzeigevorlagen erstellt haben, die jeweils eine eigene zugeordnete HTML-Datei aufweisen, können Sie diese zugeordneten HTML-Dateien in Ihrem HTML-Editor auf Ihrem Computer weiter bearbeiten. Immer wenn Sie eine Datei im zugeordneten Laufwerk speichern, synchronisiert SharePoint die Dateien auf Ihrem Computer automatisch mit der Gestaltungsvorlagengalerie. Sie können auf dem zugeordneten Laufwerk Ihre eigene Ordnerstruktur erstellen, und diese Struktur wird von SharePoint aufrechterhalten und in der Gestaltungsvorlagengalerie angezeigt. Sie sollten alle Dateien, die sich auf ein Design beziehen, in einem einzelnen Ordner ablegen und diesen Ordner dann auf das zugeordnete Laufwerk kopieren, wenn Sie bereit sind, Ihr Design hochzuladen.
  
    
    
Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
  
    
    

### <a name="edit-master-pages"></a>Bearbeiten von Gestaltungsvorlagen

Die Erstellung einer Gestaltungsvorlage mit vollständigem Branding, die alle von Ihnen gewünschten SharePoint-Funktionen wie Navigation und Suche enthält, umfasst im Wesentlichen drei Schritte:
  
    
    

1. Konvertieren einer HTML-Datei in eine SharePoint-Gestaltungsvorlage
    
  
2. Anzeigen der Gestaltungsvorlage in der Vorschau und Beheben etwaiger Probleme
    
  
3. Hinzufügen von SharePoint-Ausschnitten zur Gestaltungsvorlage
    
  
Jeder dieser drei Schritte wird auf einer anderen Seite im Entwurfs-Manager durchgeführt.
  
    
    

#### <a name="convert-an-html-file"></a>Konvertieren einer HTML-Datei

Das wichtigste Feature des Entwurfs-Managers ist, dass er Ihr HTML-Design in eine SharePoint-Gestaltungsvorlage konvertiert. Damit das Design erfolgreich gerendert wird, muss eine SharePoint-Gestaltungsvorlage viele ASP.NET- und SharePoint-spezifische Elemente enthalten. Wenn Sie eine HTML-Datei in eine Gestaltungsvorlage konvertieren, erstellt der Entwurfs-Manager eine .master-Datei, die all diese erforderlichen Elemente enthält, sodass Sie diese nicht kennen müssen. Bei der Konvertierung wird Ihrer ursprünglichen HTML-Datei auch HTML-Markup (wie Kommentare) hinzugefügt.
  
    
    
Nach der Konvertierung werden Ihre HTML-Datei und die SharePoint-Gestaltungsvorlage verknüpft, sodass die Gestaltungsvorlage automatisch aktualisiert wird, wenn Sie die HTML-Datei bearbeiten und auf Ihrem zugeordneten Laufwerk speichern. Die HTML-Gestaltungsvorlage besitzt im Entwurfs-Manager eine Eigenschaft mit der Bezeichnung **Zugeordnete Datei**. Mit dieser Eigenschaft wird festgelegt, ob Änderungen an der HTML-Datei mit der .master-Datei synchronisiert werden.
  
> [!NOTE]
> Der Entwurfs-Manager bietet auch die Option, Ihr Design mithilfe einer minimalen Gestaltungsvorlage zu beginnen. In diesem Szenario müssen Sie nicht mit einem HTML-Design beginnen; Sie können stattdessen eine HTML-Gestaltungsvorlage erstellen, welche die mindestens erforderlichen Seitenelemente enthält, damit die Gestaltungsvorlage in SharePoint korrekt gerendert wird, und dann Ihr eigenes Design erstellen, indem Sie die HTML-Gestaltungsvorlage bearbeiten. 
  
    
    


#### <a name="preview-the-master-page"></a>Anzeigen der Gestaltungsvorlage in der Vorschau

Zusätzlich zur Konvertierung Ihrer Gestaltungsvorlage bietet der Entwurfs-Manager eine serverseitige Vorschau (im Gegensatz zur Entwurfszeitvorschau in Ihrem HTML-Editor), sodass Sie eine Live-Vorschau Ihrer Gestaltungsvorlage erhalten und etwaige Probleme beheben können, die das Rendern der Seite verhindern können. Da Ihre HTML-Datei z. B. XML-konform sein muss, müssen Sie möglicherweise kleinere Markup-Probleme beheben und z. B. für alle Elemente schließende Tags angeben. Um Probleme zu beheben, sollten Sie die HTML-Datei bearbeiten, speichern und dann die serverseitige Vorschau aktualisieren.
  
    
    
Wenn Sie eine Gestaltungsvorlage in der Vorschau anzeigen, können Sie die Option **Vorschau-Seite ändern** links oben verwenden, um die Gestaltungsvorlage sowie jede vorhandene Seite in der Vorschau anzuzeigen, oder eine neue Seite erstellen, die in der Vorschau angezeigt werden soll. Im Gegensatz zur Entwurfszeitvorschau Ihrer HTML-Gestaltungsvorlage in einem HTML-Editor ist diese serverseitige Vorschau eine Live-Vorschau mit sämtlichen Funktionen. Daher ziehen Sie es möglicherweise vor, die HTML-Datei zu bearbeiten und speichern, sodass die verknüpfte .master-Datei mit den aktuellen Änderungen synchronisiert wird, die Live-Vorschau zu aktualisieren und die aktuellen Designänderungen im Browser anzuzeigen.
  
    
    

#### <a name="add-snippets"></a>Hinzufügen von Ausschnitten

Nachdem Sie Ihre Gestaltungsvorlage konvertiert und erfolgreich in der Vorschau angezeigt haben, können Sie der Gestaltungsvorlage Ausschnitte hinzufügen. Ein Ausschnitt ist eine HTML-Darstellung einer SharePoint-Komponente, wie ein Navigationssteuerelement, ein Suchfeld oder ein Webpart, das Sie Ihrer Gestaltungsvorlage hinzufügen können. Durch Hinzufügen von Ausschnitten zu Ihrer Gestaltungsvorlage können Sie schnell eine breite Palette von SharePoint-Funktionen in Ihre Gestaltungsvorlage integrieren. Das Hinzufügen von Ausschnitten umfasst im Wesentlichen drei Schritte:
  
    
    

1. Suchen und Konfigurieren von Ausschnitten im Codeausschnittkatalog
    
  
2. Kopieren von Ausschnitten in Ihre HTML-Gestaltungsvorlage
    
  
3. Anzeigen von Ausschnitten in der Vorschau und Formatieren von Ausschnitten mit CSS
    
Weitere Informationen finden Sie unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).
    
  

#### <a name="find-and-configure-snippets-in-the-snippet-gallery"></a>Suchen und Konfigurieren von Ausschnitten im Codeausschnittkatalog

Im Codeausschnittkatalog können Sie schnell sehen, welche Komponenten für den Typ von Datei verfügbar sind, die Sie bearbeiten: Gestaltungsvorlage oder Seitenlayout. Sie wählen auf dem Menüband einen Ausschnitt aus. Im Eigenschaftsraster auf der rechten Seite können Sie die Eigenschaften für diese Instanz eines Ausschnitts konfigurieren, und dann links **Aktualisieren** auswählen, um den HTML-Ausschnitt zu aktualisieren.
  
    
    

#### <a name="copy-snippets-to-your-html-master-page"></a>Kopieren von Ausschnitten in Ihre HTML-Gestaltungsvorlage

Nachdem Sie einen Ausschnitt konfiguriert haben, kopieren Sie ihn in die Zwischenablage, und fügen Sie ihn dann in Ihrer HTML-Datei an der richtigen Stelle ein. Falls Ihr HTML-Design bereits Modellsteuerelemente oder statische Steuerelemente enthält, löschen oder kommentieren Sie diese aus, wenn Sie sie durch dynamische Ausschnitte aus der Codeausschnittkatalog ersetzen.
  
    
    

#### <a name="preview-and-style-snippets-by-using-css"></a>Anzeigen von Ausschnitten in der Vorschau und Formatieren von Ausschnitten mit CSS

Nachdem Sie Ausschnitte in Ihre HTML-Datei kopiert und die Änderungen dann gespeichert haben, können Sie die serverseitige Vorschau der Gestaltungsvorlage aktualisieren, um zu sehen, wie das Steuerelement gerendert wird. Ausschnitte enthalten Markup, das eine Entwurfszeitvorschau in einem HTML-Editor ermöglicht. Die serverseitige Vorschau zeigt dagegen eine wirklich getreue Vorschau mit Livedaten an. So zeigt ein Navigationssteuerelement z. B. die aktuelle Navigationsstruktur der Website mit Livedaten aus Ihrer Datenquelle an.
  
    
    
Die meisten Ausschnitte erben standardmäßig Formate vom SharePoint-Haupt-Stylesheet, corev15.css. Um einen Ausschnitt zu formatieren, müssen Sie ermitteln, welche Formate auf den Ausschnitt angewendet werden, und diese dann mit benutzerdefiniertem CSS überschreiben. Um diese Standardformate zu ermitteln, können Sie ein Browsertool wie die Entwicklertools in Internet Explorer verwenden. Drücken Sie, während Sie Ihre Gestaltungsvorlage in der serverseitigen Vorschau in Internet Explorer anzeigen, die Taste **F12**, wählen Sie **Suchen** und dann **Element durch Klicken auswählen** aus. Dann können Sie auf den Ausschnitt klicken und genau sehen, welche Formate überschrieben werden müssen, indem Sie dem entsprechenden benutzerdefinierten Stylesheet, mit dem Ihre Gestaltungsvorlage verknüpft ist, CSS hinzufügen.
  
    
    

### <a name="edit-display-templates"></a>Bearbeiten von Anzeigevorlagen

Wenn Sie eine lokale Installation von SharePoint Server verwenden, können Sie mit dem Inhaltssuche-Webpart und anderen suchbasierten Webparts die Ergebnisse Ihrer Suchabfragen als Inhalte in Ihren Seiten anzeigen. Suchbasierte Webparts zeigen Vorlagen im Wesentlichen zu zwei Zwecken an:
  
    
    

- Um die verwalteten Eigenschaften, die in Suchergebniselementen zurückgegeben werden, Eigenschaften zuzuordnen, die für JavaScript verfügbar sind, einschließlich des benutzerdefinierten JavaScript, das Sie implementieren möchten.
    
  
- Um diese Eigenschaften mithilfe von HTML und CSS anzuzeigen und die Anzeige zu formatieren.
    
  
Bei Gestaltungsvorlagen und Seitenlayouts bearbeiten Sie eine verknüpfte HTML-Datei, jedoch nicht die .master-Datei oder die .aspx-Datei. Auf ähnliche Weise bestehen Anzeigevorlagen aus einer HTML-Datei und einer verknüpften .js-Datei, wobei Sie nur die HTML-Datei bearbeiten. Jedes Mal, wenn Sie die HTML-Datei speichern, aktualisiert SharePoint automatisch die verknüpfte .js-Datei.
  
    
    
Wenn Sie eine benutzerdefinierte Anzeigevorlage erstellen möchten, sollten Sie zunächst eine der vorhandenen Anzeigevorlagen kopieren und dann bearbeiten. Dies ist hilfreich, da die Standardanzeigevorlagen in Kommentaren in den HTML-Dateien Informationen enthalten und Sie die richtige Seitengrundstruktur und einen Rahmen für einfache Aufgaben wie das Zuordnen von Eingabefeldern zur Hand haben.
  
    
    

### <a name="edit-page-layouts"></a>Bearbeiten von Seitenlayouts

Der Prozess zur Erstellung eines Seitenlayouts unterscheidet sich ein wenig vom Prozess zur Erstellung einer Gestaltungsvorlage. Bei einer Gestaltungsvorlage beginnen Sie mit einem HTML-Design, konvertieren dieses in eine SharePoint-Gestaltungsvorlage und bearbeiten dann weiterhin die verknüpfte HTML-Datei. Bei einem Seitenlayout hingegen erstellen Sie zuerst das Seitenlayout im Entwurfs-Manager, der eine .aspx-Datei und eine HTML-Datei erstellt, und bearbeiten dann in Ihrem HTML-Editor die verknüpfte HTML-Datei auf dem zugeordneten Laufwerk. Der Grund dafür, dass Sie den Entwurfs-Manager zum Erstellung eines Seitenlayouts verwenden müssen, ist, dass dem Seitenlayout der korrekte Satz von Seitenfeldern hinzugefügt werden kann.
  
    
    
Wenn Sie ein Seitenlayout erstellen, wählen Sie eine Gestaltungsvorlage, mit der Sie Ihr Seitenlayout in der Vorschau anzeigen, sowie einen Seitenlayout-Inhaltstypen aus. Ein Inhaltstyp ist ein Schema von Feldern und Datentypen, und die im Seitenlayout-Inhaltstyp verfügbaren Felder bestimmen, welche Seitenfeld-Steuerelemente im von Ihnen entworfenen Seitenlayout verfügbar sind. Sie erstellen zuerst ein Seitenlayout im Browser, sodass die Seitenfelder hinzugefügt werden können.
  
    
    
Nachdem Sie ein Seitenlayout mit der verknüpften HTML-Datei erstellt haben, sind die restlichen Schritte die gleichen wie bei einer Gestaltungsvorlage:
  
    
    

- Anzeigen des Seitenlayouts in der Vorschau und Beheben etwaiger Probleme durch das Bearbeiten und Speichern der HTML-Version
    
  
- Hinzufügen von Ausschnitten zum Seitenlayout (Konfigurieren, Kopieren, in der Vorschau anzeigen, Formatieren)
    
  
In der Codeausschnittgalerie sind für Seitenlayouts und Gestaltungsvorlagen verschiedene Ausschnitte verfügbar, und das Menüband zeigt nur die Ausschnitte an, die für diesen Dateityp relevant sind. So sind z. B. Navigations- und Suchfeldausschnitte nur für eine Gestaltungsvorlage verfügbar, während Seitenfelder nur in einem Seitenlayout verfügbar sind.
  
    
    
Wenn Sie ein Seitenlayout entwerfen, besteht Ihre wichtigste Aufgabe darin, die Seitenfeldsteuerelemente zu positionieren und zu formatieren, die von Inhaltsautoren erstellte Inhalte anzeigen. Die Formate für ein Seitenlayout können sich in einem Stylesheet befinden, mit dem die Gestaltungsvorlage verknüpft ist, oder jedes Seitenlayout kann mit einem eigenen spezifischen Stylesheet verknüpft sein. Wenn Ihr HTML-Design geeignetere Inhalte für ein Seitenlayout enthält als eine Gestaltungsvorlage, sollten Sie diese Inhalte aus Ihrer HTML-Gestaltungsvorlage übertragen und diese Formate dann auf die richtigen Steuerelemente und Elemente des relevanten Seitenlayouts anwenden.
  
    
    
Weitere Informationen finden Sie unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).
  
    
    

### <a name="create-themes-and-composed-looks"></a>Erstellen von Design und zusammengesetzten Layouts

In Office 365 können Sie mit dem Entwurfs-Manager Designs und durchkomponierte Looks erstellen. (Diese Möglichkeit besteht nicht in lokalen SharePoint-Installationen.) Ein Design ist ein Satz von Schriftarten und Farben, das auf ein benutzerdefiniertes Design angewendet werden kann (d. h. eine Gestaltungsvorlage). Designs werden in XML-Dateien definiert, die wiederum in den Designkatalog hochgeladen werden. Soll eine benutzerdefinierte Gestaltungsvorlage Designs unterstützen, müssen Sie der Gestaltungsvorlage spezielles Markup hinzufügen. SharePoint erkennt dieses Markup und fügt Designelemente wie Schriftarten und Farben ein.
  
    
Ein durchkomponierter Look besteht aus einem Hintergrundbild, einem Design (d. h. Schriftarten und Farben) und einer Gestaltungsvorlage. Mithilfe eines durchkomponierten Looks können Sie vordefinierte Designelemente (Designs, Hintergrundbilder und Gestaltungsvorlagen) in den unterschiedlichsten Kombinationen verwenden.
  
    

### <a name="publish-and-apply-design"></a>Veröffentlichen und Anwenden eines Designs

Die meisten von Ihrem Design verwendeten Objekte, wie Bilder, HTML-, CSS- und JavaScript-Dateien, befinden sich in der Gestaltungsvorlagengalerie. Die Gestaltungsvorlagengalerie ist eine SharePoint-Dokumentbibliothek mit standardmäßig aktivierter Versionsverwaltung, sodass jedes Mal, wenn Sie eine Datei bearbeiten, Haupt- und Nebenversionen (Entwurfsversionen) erstellt werden.
  
    
    
Bevor Sie Ihr Design auf eine Website anwenden können, müssen Sie zuerst eine Hauptversion jeder Datei oder jedes Objekts veröffentlichen, das von Ihrem Design verwendet wird. Wenn Sie Ihre Website in einer Testumgebung entwerfen, sollten Sie die Versionsverwaltung für die Gestaltungsvorlagengalerie deaktivieren, sodass Sie nicht jede Datei veröffentlichen müssen, bevor Sie die Website in der Vorschau anzeigen. Dies wird jedoch nicht empfohlen, wenn Sie Ihr Design auf einer Livewebsite entwerfen.
  
    
    
Wenn Sie alle Designdateien veröffentlicht haben, können Sie das Design anwenden, indem Sie Ihrer Website Ihre fertigen Gestaltungsvorlagen zuweisen. Jede Website kann jedem Gerätekanal eine andere Gestaltungsvorlage zuweisen, und auf dieser Seite des Entwurfs-Managers wenden Sie eine Gestaltungsvorlage auf einen Kanal an.
  
    
    

### <a name="create-a-design-package"></a>Erstellen eines Designpakets

Ein Designpaket stellt eine einfache Möglichkeit dar, alle von Ihrem Design verwendeten Dateien und Objekte zu sammeln, sie von einer Website zu exportieren, sie in eine andere Website zu importieren und das Design auf die neue Website anzuwenden. Wenn Sie Ihr Design in einer Testwebsitesammlung implementieren und optimieren und es in einer Livewebsitesammlung bereitstellen möchten, können Sie zum Übertragen Ihres Designs ein Designpaket verwenden.
  
    
    
Ein Designpaket ist eine .wsp-Datei, eine SharePoint-Lösungsdatei, bei der es sich im Grunde um einen speziellen Typ von .cab-Datei handelt. Wenn Sie ein Designpaket erstellen oder importieren, wird die .wsp-Datei in der Lösungsgalerie gespeichert. Nachdem Sie ein Designpaket importiert haben, wird das Paket automatisch aktiviert. Wenn die Gestaltungsvorlagen und Seitenlayouts veröffentlicht wurden, bevor sie verpackt wurden, und wenn die Gestaltungsvorlagen Gerätekanälen zugeordnet wurden, bevor sie verpackt wurden, wird das Design automatisch auf die Website angewendet, wenn das Designpaket bereitgestellt wird. Um das Design auf die neue Website anzuwenden, müssen Sie ansonsten einfach die Designdateien veröffentlichen und die Gestaltungsvorlagen pro Gerätekanal anwenden.
  



## <a name="see-also"></a>Siehe auch
<a name="Additional"> </a>


-  [Übersicht über das SharePoint-Seitenmodell](overview-of-the-sharepoint-page-model.md)
    
  
-  [Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
    
  

