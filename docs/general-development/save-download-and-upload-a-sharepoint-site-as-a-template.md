---
title: Speichern, Herunter- und Hochladen einer SharePoint-Website als Vorlage
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2e637172-ddac-4a70-bd77-55a1645a3db1
ms.openlocfilehash: f018af03acc5536b9abc4abe244664f9d9bed4ab
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="save-download-and-upload-a-sharepoint-site-as-a-template"></a>Speichern, Herunter- und Hochladen einer SharePoint-Website als Vorlage
Hier erfahren Sie, wie Sie mithilfe von SharePoint-Websitevorlagen stabile Anwendungen entwerfen und erstellen. Sie können zuverlässige SharePoint-Anwendungen entwerfen und erstellen, die mehrere Datenquellen, benutzerorientierte Ansichten und Formulare, hochgradig angepasste Workflows u. v. a. m. beinhalten. Sobald Sie eine Geschäftslösungs-Website erstellt haben, können Sie diese direkt in der SharePoint-Umgebung verwenden. Sie können die Lösung aber auch in eine Vorlage umwandeln und in einer anderen Umgebung bereitstellen und für andere Benutzer verfügbar machen, sodass sie als Vorlage zum Erstellen neuer Websites verwendet oder zur weiteren Entwicklung in Visual Studio weitergegeben werden kann.
  
    
    


## <a name="what-is-a-sharepoint-site-template"></a>Was ist eine SharePoint-Websitevorlage?
<a name="bkmk_WhatIsTemplate"> </a>

SharePoint-Websitevorlagen sind vorkonfigurierte Definitionen, die einem bestimmten Geschäftszweck dienen. Sie können auf Grundlage dieser Vorlagen Ihre eigene SharePoint-Website erstellen und die Website dann beliebig anpassen. Wahrscheinlich sind Sie mit den Standardwebsitevorlagen wie Teamwebsite, Projektwebsite und Communitywebsite vertraut.
  
    
    
Zusätzlich zu den Standardvorlagen können Sie auf Basis einer Website, die Sie erstellt und angepasst haben, Ihre eigene Websitevorlage erstellen. Dies ist ein nützliches Feature, mit dem Sie eine benutzerdefinierte Lösung erstellen und diese dann für Ihre Kollegen, das gesamte Unternehmen oder andere Unternehmen freigeben können. Sie können die Website auch verpacken und in einer anderen Umgebung oder Anwendung wie Visual Studio öffnen und sie auch dort anpassen.
  
    
    
Das Umwandeln einer angepassten Website bzw. einer Geschäftslösung in eine Vorlage stellt eine äußerst hilfreiche und leistungsstarke Funktion dar. Sobald Sie Ihre Lösung als Vorlage verpacken, werden Sie erkennen, welches Potenzial SharePoint als Plattform für Geschäftsanwendungen bietet. Die Option zur Erstellung einer Websitevorlage macht all dies möglich.
  
    
    
Beim Speichern der Website als Vorlage wird eine WSP-Datei (Web Solution Package) erstellt. Dabei handelt es sich um eine CAB-Datei mit dem Lösungsmanifest. Die erstellte Lösung wird im Lösungskatalog für die SharePoint-Websitesammlung gespeichert. Sobald Sie die Vorlage speichern, wird eine Lösungsdatei (WSP-Datei) erstellt und im Lösungskatalog gespeichert. Dort können Sie die Lösung herunterladen oder aktivieren.
  
    
    

> **Hinweis:** Die erstelle WSP-Datei ist eine teilweise vertrauenswürdige Benutzerlösung, die über das gleiche deklarative Format wie eine voll vertrauenswürdige SharePoint-Lösung verfügt. Er werden jedoch nicht alle Feature-Elementtypen von vollständig vertrauenswürdigen Lösungen unterstützt. 
  
    
    


### <a name="what-gets-saved-in-a-template"></a>Was wird in einer Vorlage gespeichert?

Wenn Sie eine SharePoint-Website als Vorlage speichern, speichern Sie das gesamte Framework der Website: die Listen und Bibliotheken, Ansichten und Formulare sowie die Workflows. Zusätzlich zu diesen Komponenten können Sie die Inhalte der Website in die Vorlage einschließen, z. B. die in den Dokumentbibliotheken gespeicherten Dokumente. Dies könnte nützlich sein, um Benutzern zum Einstieg Beispielinhalte zur Verfügung zu stellen. Beachten Sie, dass dies auch die Größe Ihrer Vorlage über die 50 MB Standardgrenze für Websitevorlagen hinaus erhöhen könnte.
  
    
    
Der Großteil der Objekte in einer Website werden in die Vorlage eingeschlossen und von dieser unterstützt. Es gibt jedoch einige Objekte und Features, die nicht unterstützt werden. 
  
    
    

- **Unterstützt** Listen, Bibliotheken, externe Listen, Datenquellenverbindungen, Listenansichten und Datenansichten, benutzerdefinierte Formulare, Workflows, Inhaltstypen, benutzerdefinierte Aktionen, Navigation, Websiteseiten, Gestaltungsvorlagen, Module und Webvorlagen
    
  
- **Nicht unterstützt** Angepasste Berechtigungen, ausgeführte Workflowinstanzen, Versionsverlauf von Listenelementen, mit ausgeführten Workflows verknüpfte Workflowaufgaben, Personen- oder Gruppenfeldwerte, Taxonomiefeldwerte, Veröffentlichungsseiten und Veröffentlichungswebsites, Meine Websites, Features zum Anheften, SharePoint-Add-Ins und Remoteereignisempfänger
    
    > **Hinweis:** Für Veröffentlichungswebsites, können Sie die Websitevorlagen-Definition verwenden. Weitere Informationen finden Sie in den am Ende dieses Themas unter [Zusätzliche Ressourcen](save-download-and-upload-a-sharepoint-site-as-a-template.md#bkmk_additionalresources).

### <a name="what-can-you-do-with-sharepoint-templates"></a>Was können Sie mit SharePoint-Vorlagen tun?

Das Speichern einer Website als Vorlage stellt ein sehr nützliches Feature dar, da es so viele Verwendungsmöglichkeiten für benutzerdefinierte Websites eröffnet. Im Folgenden sind die unmittelbaren Vorteile der Speicherung einer Website als Vorlage aufgelistet:
  
    
    

- **Unmittelbare Lösungsbereitstellung** Speichern und aktivieren Sie die Vorlage im Lösungskatalog, und erlauben Sie anderen Mitarbeitern, auf Basis dieser Vorlage neue Websites zu erstellen. Sie können sie auswählen und dann auf dieser Grundlage eine neue Website erstellen, welche die Komponenten der Website, ihre Struktur, ihre Workflows und mehr erbt. Sie benötigen Visual Studio nicht zum Erstellen Ihrer Lösung, müssen nicht direkt auf den Server zugreifen und Serveradministratorbefehle ausführen. Speichern Sie die Website einfach als Vorlage, aktivieren Sie sie und los geht's.
    
  
- **Portabilität** Zusätzlich zur Bereitstellung einer benutzerdefinierten Lösung in Ihrer Umgebung können Sie die WSP-Datei herunterladen, sie unterwegs verwenden und in einer anderen SharePoint-Umgebung bereitstellen. Sämtliche Websiteanpassungen Ihrerseits werden bequem in einer Datei gespeichert.
    
  
- **Erweiterbarkeit** Sie können Ihre angepasste Website als Weblösungspaket in Visual Studio öffnen, zusätzliche Entwicklungsanpassungen an der Vorlage vornehmen und sie dann in SharePoint bereitstellen. SharePoint-Websiteentwicklung kann daher einen Lösungslebenszyklus (Entwicklung, Staging und Aufnahme in die Produktion) durchlaufen, der SharePoint Designer 2013, Visual Studio und den Browser umfasst.
    
  
Wenn Sie mit der Erstellung benutzerdefinierter Websites in SharePoint beginnen, entdecken Sie noch mehr Vorteile der Umwandlung Ihrer Website in eine Lösung, die im gesamten Unternehmen verwendet werden kann. Die grundlegenden Schritte beim Arbeiten mit Websitevorlagen sind folgende:
  
    
    

- Speichern Sie eine Website als Vorlage im Lösungskatalog.
    
  
- Laden Sie die Websitevorlage aus dem Lösungskatalog in eine WSP-Datei herunter.
    
  
- Laden Sie die WSP-Datei in den Lösungskatalog hoch.
    
  
Nachdem Sie eine Websitevorlage im Lösungskatalog hinzugefügt haben und die Vorlage aktiviert wurde, steht die Vorlage auf der Registerkarte **Benutzerdefiniert** im Abschnitt **Vorlagenauswahl** auf der Seite **Neue SharePoint-Website** zur Auswahl zur Verfügung, wenn Sie das nächste Mal eine Website oder Unterwebsite erstellen.
  
    
    

## <a name="save-a-site-as-a-template-to-the-solutions-gallery"></a>Speichern einer Website als Vorlage im Lösungskatalog
<a name="bkmk_SaveTemplate"> </a>


1. Navigieren Sie zur Website auf oberster Ebene der Websitesammlung.
    
  
2. Klicken Sie auf **Einstellungen** und dann auf **Websiteeinstellungen**.
    
  
3. Klicken Sie im Bereich **Websiteaktionen** auf **Website als Vorlage speichern**.
    
  
4. Geben Sie im Bild **Dateiname** einen Namen an, der für die Vorlage verwendet werden soll.
    
  
5. Geben Sie in den Feldern **Vorlagenname** und **Vorlagenbeschreibung** einen Namen und eine Beschreibung für die Vorlage an.
    
  
6. Wenn Sie den Inhalt der Website in die Websitevorlage integrieren möchten, wählen Sie das Feld **Inhalte einschließen**.
    
    > **Hinweis:** Das Einbeziehen des Inhalts der Website kann die Größe die Vorlage erheblich erhöhen. Der Standardgrenzwert für eine Websitevorlage beträgt 50 MB, kann in Ihrer Organisation jedoch auch geringer sein. Sie können Inhalte immer ausschließen und dann später die benötigten Inhalte in die neue Website kopieren. Sie können auch den Grenzwert erhöhen. Wenn Sie den Grenzwert beispielsweise auf ein Maximum erhöhen möchten, verwenden Sie die folgende Stsadm-Befehlssyntax. >  `stsadm -o setproperty -pn max-template-document-size -pv 524288000`
7. Klicken Sie auf **OK**, um die Vorlage zu speichern.
    
    Wenn alle Komponenten auf der Website gültig sind, wird die Vorlage erstellt, und es wird die Meldung angezeigt, dass der Vorgang erfolgreich abgeschlossen wurde.
    
  
8. Führen Sie einen der folgenden Schritte aus:
    
  - Klicken Sie auf **OK**, um zu Ihrer Website zurückzukehren.
    
  
  - Klicken Sie auf **Lösungskatalog**, um direkt zur Websitevorlage zu wechseln.
    
  

## <a name="download-the-site-template-from-the-solutions-gallery-to-a-file"></a>Herunterladen der Websitevorlage aus dem Lösungskatalog in eine Datei
<a name="bkmk_DownloadTemplate"> </a>


1. Navigieren Sie zur Website auf oberster Ebene der Websitesammlung.
    
  
2. Klicken Sie auf **Einstellungen** und dann auf **Websiteeinstellungen**.
    
  
3. Klicken Sie im Abschnitt **Web-Designer-Kataloge** auf **Lösungen**.
    
  
4. Wenn es erforderlich ist, die Lösung zu aktivieren, markieren Sie sie und klicken Sie in der **Befehle**-Gruppe auf **Aktivieren**. Klicken Sie dann im Bildschirm **Lösungsaktivierung bestätigen** der **Befehle**-Gruppe auf **Aktivieren**.
    
  
5. Klicken Sie zum Herunterladen der Lösung im Lösungskatalog auf deren Name, und klicken Sie auf **Speichern**. Navigieren Sie dann im Dialogfeld **Speichern unter** zum Speicherort, an dem Sie die Lösung speichern möchten, klicken Sie auf **Speichern**, und klicken Sie dann auf **Schließen**.
    
  

## <a name="upload-the-site-template-file-to-a-solutions-gallery"></a>Hochladen der Websitevorlagendatei in einen Lösungskatalog
<a name="bkmk_UploadTemplate"> </a>


1. Navigieren Sie zur Website auf oberster Ebene der Websitesammlung.
    
  
2. Klicken Sie auf **Einstellungen** und dann auf **Websiteeinstellungen**.
    
  
3. Klicken Sie im Abschnitt **Web-Designer-Kataloge** auf **Lösungen**.
    
  
4. Klicken Sie zum Hochladen der Lösung in der Gruppe **Befehle** auf **Hochladen**, und klicken Sie dann im Dialogfeld **Dokument hinzufügen** auf **Durchsuchen**. Suchen Sie dann im Dialogfeld **Datei zum Hochladen auswählen** die Datei, klicken Sie auf **Öffnen**, und klicken Sie dann auf **OK**.
    
  
5. Klicken Sie zum Aktivieren der Lösung auf dem Bildschirm zur Bestätigung der Lösungsaktivierung in der Gruppe **Befehle** auf **Aktivieren**.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bkmk_additionalresources"> </a>


-  
  [Websitetypen: WebTemplates und Websitedefinitionen](http://msdn.microsoft.com/en-us/library/ms434313.aspx)
    
  
-  
  [Grundlegendes zu packen und POST von Workflows in SharePoint](http://msdn.microsoft.com/en-us/library/jj819316%28v=office.15%29.aspx)
    
  
-  
  [Farmlösungen in SharePoint erstellen](http://msdn.microsoft.com/en-us/library/jj163902%28v=office.15%29.aspx)
    
  
-  [Kopieren oder Verschieben einer Liste mithilfe einer Listenvorlage](http://office.com/redir/HA101782479.aspx)
    
  
-  [Kopieren oder Verschieben einer Bibliothek mithilfe einer Bibliotheksvorlage](http://office.com/redir/HA101814157.aspx)
    
  
-  [Kopieren oder Verschieben von Bibliotheksdateien mit "Öffnen" im Windows-Explorer](http://office.com/redir/HA101811182.aspx)
    
  

