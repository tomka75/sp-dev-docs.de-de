# <a name="deploy-and-install-a-sharepoint-hosted-sharepoint-add-in"></a>Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins
Erfahren Sie, wie SharePoint-Add-Ins bereitgestellt und installiert werden.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Dies ist der zweite einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit dem Thema [SharePoint-Add-Ins](sharepoint-add-ins) und den vorherigen Themen der Reihe vertraut:
 

-  [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 

 **Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_SP-Hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeColumns.sln“ öffnen.
 

Sie werden feststellen, dass die Entwicklung von SharePoint gehosteter SharePoint-Add-Ins viel einfacher ist, wenn Sie wissen, wie Benutzer bereitgestellt und Ihre Add-Ins installiert werden. Deshalb unterbrechen wir in diesem Artikel kurz die Codierung, um einen Add-In-Katalog zu erstellen und zu verwenden, und installieren dann das Add-In, an dem Sie gearbeitet haben.
 

## <a name="create-an-add-in-catalog"></a>Erstellen eines Add-In-Katalogs


 

 

1. Melden Sie sich als Administrator bei Ihrem Office 365-Abonnement an. Wählen Sie das Add-In-Startprogrammsymbol, und wählen Sie dann das Add-In **Admin**.
    
    **Add-In-Startprogramm für Office 365**

 

  ![App-Startfeld für Office 365](../../images/ec60797c-d329-4922-a811-70c64598f4d5.PNG)
 

    
    
 
2. Erweitern Sie im **Admin Center** den Knoten **Admin** im Aufgabenbereich, und wählen Sie dann **SharePoint**.
    
 
3. Wählen Sie im **SharePoint Admin Center** die Option **Add-Ins** im Aufgabenbereich.
    
 
4. Wählen Sie auf der Seite **Add-Ins** die Option **Add-In-Katalog** aus. (Wenn bereits eine Add-In-Katalog-Websitesammlung im Abonnement vorhanden ist, wird diese geöffnet, und Sie sind fertig. Sie können nicht mehrere Add-In-Kataloge in einem Abonnement erstellen.)
    
 
5. Wählen Sie auf der Seite **Add-In-Katalogwebsite** **OK** aus, um die Standardoption zu akzeptieren und eine neue Add-In-Katalogwebsite zu erstellen.
    
 
6. Geben Sie im Dialogfeld **Add-In-Katalog-Websitesammlung erstellen** den Titel und die Websiteadresse Ihrer App-Katalogwebsite an. Es wird empfohlen, „Katalog" in den Titel und die URL einzuschließen, damit Sie sich beides besser merken und im **SharePoint Admin Center** leichter erkennen können.
    
 
7. Geben Sie eine **Zeitzone** an, und legen Sie sich selbst als **Administrator** fest.
    
 
8. Legen Sie das **Speicherkontingent** auf den niedrigsten möglichen Wert fest (derzeit 110, das kann sich jedoch ändern), da die Add-In-Pakete, die Sie an diese Websitesammlung hochladen, sehr klein sind.
    
 
9. Legen Sie das **Serverressourcenkontingent** auf 0 (Null) fest, und wählen Sie dann **OK** aus. (Das Serverressourcenkontingent bezieht sich auf die Einschränkung von Sandkastenlösungen mit schlechter Leistung, aber Sie werden keine Sandkastenlösungen auf Ihrer Add-In-Katalogwebsite installieren.)
    
 
Wenn die Websitesammlung erstellt wird, bringt SharePoint Sie zurück zum **SharePoint Admin Center**. Nach ein paar Minuten sehen Sie, dass die Websitesammlung erstellt wurde.
 

## <a name="package-the-add-in-and-upload-it-to-the-catalog"></a>Packen des Add-Ins und Hochladen in den Katalog


 

 

1. Öffnen Sie die Visual Studio-Projektmappe, und klicken Sie anschließend im **Projektmappen-Explorer** mit der rechten Maustaste auf den Projektknoten. Wählen Sie **Veröffentlichen**.
    
 
2. Wählen Sie im Bereich **Veröffentlichen** die Option **Add-In verpacken** aus. Das Add-In wird gepackt und als APP-Datei im Ordner „\bin\debug\web.publish\1.0.0.0“ der Projektmappe gespeichert.
    
 
3. Öffnen Sie die Add-In-Katalogwebsite in einem Browser, und wählen Sie **SharePoint-Add-Ins** in der Navigationsleiste.
    
 
4. Der **SharePoint-Add-Ins**-Katalog ist eine Standard-SharePoint-Objektbibliothek. Laden Sie das Add-In-Paket mithilfe einer der Methoden zum Hochladen von Dateien in SharePoint-Bibliotheken in den Katalog hoch.
    
 

## <a name="install-the-add-in-as-end-users-do"></a>Installieren des Add-Ins als Endbenutzer


1. Navigieren Sie zu einer beliebigen Website im SharePoint Online-Abonnement, und öffnen Sie die Seite **Websiteinhalt**.
    
 
2. Wählen Sie **Add-In hinzufügen**, um die Seite **Ihre Add-Ins** zu öffnen.
    
 
3. Suchen Sie das Add-In **Orientierung für Mitarbeiter** im Abschnitt **Add-Ins, die Sie hinzufügen können**, und klicken Sie auf die zugehörige Kachel.
    
 
4. Wählen Sie im Zustimmungsdialogfeld **Vertrauen** aus. Die Seite **Websiteinhalt** wird automatisch geöffnet, und das Add-In wird mit dem Hinweis angezeigt, dass sie installiert wird. Nach der Installation können Benutzer die Kachel auswählen, um das Add-In auszuführen.
    
 

## <a name="remove-the-add-in"></a>Entfernen des Add-Ins

Um das gleiche SharePoint-Add-In in Visual Studio noch weiter zu verbessern (siehe [nächste Schritte](#Nextsteps)), entfernen Sie das Add-In mit den folgenden Schritten:
 

 

1. Bewegen Sie den Cursor auf der Seite **Websiteinhalte** über das Add-In, sodass die Popupschaltfläche **...** angezeigt wird.
    
 
2. Klicken Sie auf die Popupschaltfläche, und wählen Sie dann **ENTFERNEN** im Popup.
    
 
3. Navigieren Sie zurück zur Add-In-Katalogwebsite, und wählen Sie **SharePoint-Add-Ins** in der Navigationsleiste.
    
 
4. Markieren Sie das Add-In, wählen Sie **Verwalten** auf der Taskleiste direkt oberhalb der Liste, und wählen Sie dann **Löschen** im Verwaltungsmenü.
    
 

## 

Es wird dringend empfohlen, mit dieser Reihe zu von SharePoint gehosteten Add-Ins fortzufahren, bevor Sie zu den fortgeschritteneren Themen übergehen. Als Nächstes kehren wir in  [Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten Add-In für SharePoint](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in) zum Codieren zurück.
 

 

