---
title: Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins
description: "Erstellen Sie einen Add-In-Katalog, packen Sie das Add-In, laden Sie es in den Katalog hoch, installieren Sie es und löschen Sie es."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 58a1810d34d06b76a7e0e12b21792200bfe1bc93
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="deploy-and-install-a-sharepoint-hosted-sharepoint-add-in"></a>Bereitstellen und Installieren eines in SharePoint gehosteten SharePoint-Add-Ins

Dies ist der zweite in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Sie sollten sich zuerst mit [SharePoint Add-Ins](sharepoint-add-ins.md) und dem Übersichtsartikel in dieser Reihe vertraut machen:

-  [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
> [!NOTE]
> Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, können Sie das Thema mit einer Visual Studio-Lösung weiter vertiefen. Sie können auch das Repository von [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeColumns.sln“ öffnen.

Sie werden feststellen, dass die Entwicklung von SharePoint gehosteter SharePoint-Add-Ins viel einfacher ist, wenn Sie wissen, wie Benutzer bereitgestellt und Ihre Add-Ins installiert werden. Deshalb unterbrechen wir in diesem Artikel kurz die Codierung, um einen Add-In-Katalog zu erstellen und zu verwenden, und installieren dann das Add-In, an dem Sie gearbeitet haben.

## <a name="create-an-add-in-catalog"></a>Erstellen eines Add-In-Katalogs

1. Melden Sie sich bei Ihrem Office 365-Abonnement als Administrator an. Wählen Sie das Symbol für das  Add-In-Startprogramm, und wählen Sie dann das **Admin**-Add-In.
    
   *Abbildung 1. Add-In-Startprogramm für Office 365*

   ![App-Startprogramm für Office 365](../images/ec60797c-d329-4922-a811-70c64598f4d5.PNG)
 
2. Erweitern Sie im **Admin Center** den Knoten **Admin** im Aufgabenbereich, und wählen Sie dann **SharePoint** aus.
     
3. Wählen Sie im **SharePoint Admin Center** die Option **Add-Ins** im Aufgabenbereich aus.
     
4. Wählen Sie auf der Seite  **Add-Ins** die Option **Add-In-Katalog** aus. (Wenn bereits eine Add-In-Katalog-Websitesammlung im Abonnement vorhanden ist, wird diese geöffnet, und Sie sind fertig. Sie können nur jeweils einen Add-In-Katalog pro Abonnement erstellen.)    
 
5. Wählen Sie auf der Seite  **Add-In-Katalogwebsite** **OK** aus, um die Standardoption zu akzeptieren und eine neue Add-In-Katalogwebsite zu erstellen.    
 
6. Geben Sie im Dialog  **Add-In-Katalog-Websitesammlung erstellen** den Titel und die Webadresse Ihrer Add-In-Katalogwebsite an. Wir empfehlen, den Begriff „Katalog“ im Titel und der URL zu verwenden, damit er einprägsamer ist und im **SharePoint Admin Center** besser unterschieden werden kann.   
 
7. Geben Sie eine **Zeitzone** an, und legen Sie sich selbst als **Administrator** fest.
    
8. Legen Sie das **Speicherkontingent** auf den niedrigsten möglichen Wert fest (derzeit 110, das kann sich jedoch ändern), da die Add-In-Pakete, die Sie an diese Websitesammlung hochladen, sehr klein sind.
    
9. Legen Sie das **Serverressourcenkontingent** auf 0 (null) fest, und wählen Sie dann **OK** aus. (Das Serverressourcenkontingent hat Auswirkungen auf die Einschränkung leistungsschwacher Sandkastenlösungen; Sie müssen jedoch keine Sandkastenlösungen auf der Add-In-Katalogwebsite installieren.) 
 
Während die Websitesammlung erstellt wird, gelangen Sie zurück zum **SharePoint Admin Center**. Nach ein paar Minuten sehen Sie, dass die Sammlung erstellt wurde.

## <a name="package-the-add-in-and-upload-it-to-the-catalog"></a>Packen des Add-Ins und Hochladen in den Katalog

1. Öffnen Sie die Visual Studio-Projektmappe, klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Projektknoten, und wählen Sie dann **Veröffentlichen** aus.
     
2. Wählen Sie im Bereich **Veröffentlichen** die Option **Add-In verpacken** aus. Das Add-In wird gepackt und als `*.app`-Datei im Ordner „\bin\debug\web.publish\1.0.0.0“ der Projektmappe gespeichert.  
 
3. Öffnen Sie die Add-In-Katalogwebsite in einem Browser, und wählen Sie dann **SharePoint-Add-Ins** in der Navigationsleiste aus.

4. Der **SharePoint-Add-Ins**-Katalog ist eine standardmäßige SharePoint-Objektbibliothek. Laden Sie das Add-In-Paket mithilfe einer der Methoden zum Hochladen von Dateien in SharePoint-Bibliotheken in den Katalog hoch.

## <a name="install-the-add-in-as-end-users-do"></a>Installieren des Add-Ins als Endbenutzer

1. Navigieren Sie zu einer beliebigen Website im SharePoint Online-Abonnement, und öffnen Sie die Seite **Websiteinhalt**.

2. Wählen Sie **Add-In hinzufügen** aus, um die Seite **Ihre Add-Ins** zu öffnen.

3. Suchen Sie das Add-In **Orientierung für Mitarbeiter** im Abschnitt **Add-Ins, die Sie hinzufügen können**, und wählen Sie die zugehörige Kachel aus.

4. Wählen Sie **Vertrauen** im Zustimmungsdialogfeld aus. Die Seite **Websiteinhalte** wird automatisch geöffnet, und das Add-In wird mit einer Anmerkung, dass es gerade installiert wird, angezeigt. Nach der Installation können Benutzer die Kachel auswählen, um das Add-In auszuführen.

## <a name="remove-the-add-in"></a>Entfernen des Add-Ins

Um das gleiche SharePoint-Add-In in Visual Studio noch weiter zu verbessern (siehe [nächste Schritte](#Nextsteps)), entfernen Sie das Add-In mit den folgenden Schritten:

1. Bewegen Sie den Cursor auf der Seite **Websiteinhalte** über das Add-In, sodass die Popupschaltfläche **...** angezeigt wird.

2. Wählen Sie die Popupschaltfläche aus, und wählen Sie dann **ENTFERNEN** im Popup aus.

3. Navigieren Sie zurück zur Add-In-Katalogwebsite, und wählen Sie **SharePoint-Add-Ins** in der Navigationsleiste aus.

4. Markieren Sie das Add-In, wählen Sie **Verwalten** auf der Taskleiste direkt oberhalb der Liste aus, und wählen Sie dann **Löschen** im Verwaltungsmenü aus.

## <a name="next-steps"></a>Nächste Schritte
<a name="Nextsteps"></a>

Es wird dringend empfohlen, dass Sie mit dieser Reihe zu von SharePoint gehosteten Add-Ins fortfahren, bevor Sie mit den fortgeschrittenen Themen beginnen. In [Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md) befassen wir uns wieder mit der Programmierung.
 

 

