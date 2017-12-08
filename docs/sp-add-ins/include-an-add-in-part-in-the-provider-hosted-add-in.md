---
title: "Einfügen eines Add-In-Webparts in das vom Anbieter gehostete Add-In"
description: Anzeigen eines Remotewebformulars in einer SharePoint-Seite in einer vom Anbieter gehosteten SharePoint-Add-In
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 0bfdb5ad61a4d16ae11b1b8666e12953d154b7b4
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="include-an-add-in-part-in-the-provider-hosted-add-in"></a>Einfügen eines Add-In-Webparts in das vom Anbieter gehostete Add-In

Dies ist der sechste in einer Reihe von Artikeln über die Grundlagen der Entwicklung von vom Anbieter gehosteten SharePoint-Add-Ins. Sie sollten sich zuerst mit [SharePoint Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut machen:

-  [Erste Schritte beim Erstellen von vom Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md)
-  [Übertragen des SharePoint-Aussehens und -Verhaltens auf Ihr vom Anbieter gehostetes Add-In](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
-  [Einfügen einer benutzerdefinierten Schaltfläche in das vom Anbieter gehostete Add-In](include-a-custom-button-in-the-provider-hosted-add-in.md)
-  [Schnelle Übersicht über das SharePoint-Objektmodell](get-a-quick-overview-of-the-sharepoint-object-model.md)
-  [Hinzufügen von SharePoint-Schreibvorgängen zum vom Anbieter gehosteten Add-In](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)
    
> [!NOTE]
> Wenn Sie diese Reihe zu vom Anbieter gehosteten Add-Ins durchgearbeitet haben, können Sie das Thema mit einer Visual Studio-Lösung weiter vertiefen. Sie können auch das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei BeforeAdd-inPart.sln öffnen.

In diesem Artikel fügen Sie einen besonderen Webpart-Typ namens Add-In-Webpart zu dem SharePoint-Add-In hinzu. Das Add-In-Webpart stellt das Add-In-Bestellformular auf einer SharePoint-Seite zur Verfügung.

## <a name="create-the-add-in-part"></a>Erstellen des Add-In-Webparts

> [!NOTE]
> Die Einstellungen für Startprojekte in Visual Studio werden in der Regel nach dem erneuten Öffnen wieder auf die Standardwerte eingestellt. Gehen Sie nach dem erneuten Öffnen der Beispiel-Lösung in dieser Artikelreihe immer folgendermaßen vor: 
> 1. Klicken Sie mit der rechten Maustaste oben im **Projektmappen-Explorer** auf den Projektmappenknoten, und wählen Sie **Startprojekte festlegen** aus.  
> 2. Stellen Sie sicher, dass alle drei Projekte in der Spalte **Aktion** auf **Start** festgelegt sind.

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das **ChainStore**-Projekt, und wählen Sie **Hinzufügen** > **Neues Element** aus.
    
2. Wählen Sie **Client-Webpart (Hostweb)**, geben Sie dem Webpart den Namen **Bestellung absenden**, und wählen Sie dann **Hinzufügen** aus. ("Clientwebpart" ist ein anderer Name für "Webpart-Add-In").
 
3. Wählen Sie auf der nächsten Seite des Assistenten die zweite Option aus: **URL einer vorhandenen Webseite für den Clientwebpart-Inhalt auswählen oder eingeben**.

4. Wählen Sie in der Dropdownliste die URL für die Seite **OrderForm.aspx** aus, und wählen Sie dann **Fertig stellen** aus.
    
   Eine Datei „elements.xml“, die das Add-In-Webpart definiert, wird dem Projekt hinzugefügt und geöffnet.
    
5. Ändern Sie im Element **ClientWebPart** die folgenden Attribute auf die folgenden Werte:
   
    |**Attribut**|**Wert**|
    |:-----|:-----|
    |Title|Bestellung absenden|
    |Beschreibung|Formular zum Aufgeben einer Bestellung|
    |DefaultHeight|320|

    Behalten Sie für alle anderen Attribute die Standardwerte bei, und speichern Sie die Datei.
    
## <a name="run-the-add-in-and-test-the-add-in-part"></a>Ausführen des Add-Ins und Testen des Add-In-Websparts

1. Verwenden Sie die F5-Taste, um Ihr Add-In auszuführen und bereitzustellen. Visual Studio hostet die remote Webanwendung in IIS Express und die SQL-Datenbank in SQL Express. Visual Studio führt zudem eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus. Sie werden aufgefordert, Berechtigungen für das Add-In zu erteilen, bevor die Startseite geöffnet wird.

2. Wenn die Add-In-Startseite geöffnet wird, wurde das Add-In bereitgestellt, und das Add-In-Webpart **Bestellung absenden** steht Benutzern zum Hinzufügen zu einem beliebigen Webpart-Bereich auf einer beliebigen SharePoint-Seite der Hongkong Store-Website zur Verfügung. Führen Sie die folgenden Schritte aus, um es zur Startseite hinzuzufügen:
    
   1. Wählen Sie **Zurück zur Website** im Chromsteuerelement am oberen Rand der Startseite, um die Homepage des Stores in Hongkong zu öffnen.
   2. Öffnen Sie auf dem Menüband die Registerkarte **Seite**, und wählen Sie **Bearbeiten**.
   3. Nachdem sich die Seite im Bearbeitungsmodus befindet, öffnen Sie die Registerkarte **Einfügen** auf dem Menüband, und wählen Sie **Add-In-Webpart** (die Schaltfläche heißt möglicherweise immer noch **App-Webpart**).
   4. Wählen Sie im geöffneten Webpart-Einfügesteuerelement das Add-In-Webpart **Bestellung absenden** aus. Das Steuerelement sieht ähnlich aus wie folgt.

      *Abbildung 1. Webpart-Einfügesteuerelement in SharePoint*

      ![Das Webpart-Einfügesteuerelement in SharePoint. Das Webpart „Bestellung absenden“ ist hervorgehoben. Sein Name und seine Beschreibung werden in einem Feld auf der rechten Seite angezeigt.](../images/aae61f89-2e9e-4808-8b0c-2439dad7c701.PNG)

   5. Wählen Sie in eine beliebige Webpartzone im Formular, um den Standort festzulegen, an dem das Add-In-Webpart eingefügt wird. 
   6. Wählen Sie **Hinzufügen** im Webpart-Einfügesteuerelement aus. Das Add-In-Webpart **Bestellung absenden** wird zur Webpartzone hinzugefügt.
   7. Wählen Sie im Menüband **Speichern**.
    
3. Das Bestellformular wird nun auf der Seite angezeigt und hat das Aussehen und Verhalten des Rests der Seite übernommen. Es sollte wie folgt aussehen: 
    
   *Abbildung 2. Add-In-Webpart „Bestellung absenden“*

   ![Das Add-In-Webpart „Bestellung absenden“ auf der Seite mit Textfeldern für Produkt, Lieferant und Menge. Auch eine Schaltfläche „Bestellung absenden“ ist verfügbar.](../images/beae2e3c-c1f4-4334-8ab8-0c42252cb2a2.PNG)

4. Geben Sie Werte für **Lieferant**, **Produkt** und **Menge** ein, und wählen Sie dann **Bestellung absenden**. Augenscheinlich geschieht nichts, aber eine Bestellung wird in der Datenbank des Unternehmens eingegeben. Optional können Sie die Felder des Add-In-Webparts leeren, indem Sie die Seite aktualisieren.

5. Verwenden Sie im Browser die Schaltfläche „Zurück“, bis Sie wieder auf die Startseite für das ChainStore-Add-In zurückgekehrt sind, und wählen Sie dann die Schaltfläche **Bestellungen anzeigen**. Ihre neue Bestellung wird jetzt aufgelistet.

6. Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.

7. Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.

## <a name="next-steps"></a>Nächste Schritte
<a name="Nextsteps"> </a>

Das Add-In hängt von zwei Listen ab, die Sie manuell erstellt haben; Ihre Benutzer müssen keine Listen erstellen.  Im nächsten Artikel wird erklärt, wie Sie diese Listen automatisch erstellen. Zunächst müssen Sie benutzerdefinierte Handler für das Ereignis der Installation eines Add-Ins erstellen: [Behandeln von Add-In-Ereignissen im vom Anbieter gehosteten Add-In](handle-add-in-events-in-the-provider-hosted-add-in.md).
 

 

