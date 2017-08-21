
# <a name="troubleshooting-document-libraries"></a>Problembehandlung bei Dokumentbibliotheken
In diesem Thema erfahren Sie von Problemen, die auftreten können, wenn Sie von einem Cloud-Geschäfts-Add-In auf eine SharePoint-Dokumentbibliothek zugreifen, und mit welchen Techniken Sie diese Probleme beheben können.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 


 

## <a name="error-this-add-in-does-not-support-uploading-documents-from-your-current-browser"></a>Fehler: Dieses Add-Un unterstützt das Hochladen von Dokumenten in diesem Browser nicht.

Wenn Sie ein Dokument in eine verbundene Dokumentbibliothek in einem Cloud-Geschäfts-Add-In hochladen wollen, scheitert der Versuch mit folgender Fehlermeldung: "Dieses Add-In unterstützt nicht das Hochladen von Dokumenten aus dem aktuellen Browser. Verwenden Sie die neueste Version." Dieses Problem tritt nur bei einigen älteren Browsern auf, die die HTML5 FileReader-API nicht unterstützen. Fügen Sie das NuGet-Paket zu Ihrem Projekt hinzu, und stellen Sie das Add-In erneut bereit, um das Problem zu beheben.
 

 

### <a name="to-prevent-the-error"></a>So verhindern Sie den Fehler


1. Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für das Projekt **Server**, und wählen Sie **NuGet-Pakete verwalten**.
    
 
2. Erweitern Sie im Dialogfeld **NuGet-Pakete verwalten** den Knoten **Online**, und geben Sie dann im Feld **Online suchen** Webseiten ein, wie in Abbildung 1 gezeigt.
    
    **Abbildung 1. Auswahloptionen im Dialogfeld „NuGet-Pakete verwalten“**

 

  ![Auswahloptionen im Dialogfeld „NuGet-Pakete verwalten“](../../images/NuGet.PNG)
 

 

 
3. Wählen Sie in der Ergebnisliste den Eintrag **Microsoft ASP.NET-Webseiten**, und klicken Sie dann auf **Installieren**.
    
    Das Dialogfeld **Zustimmung zur Lizenz** wird geöffnet.
    
 
4. Lesen Sie im Dialogfeld **Zustimmung zur Lizenz** die Lizenzbedingungen. Klicken Sie auf **Annehmen**, wenn Sie den Bedingungen zustimmen.
    
 
5. Wenn das Paket fertig installiert ist, klicken Sie auf **Schließen**.
    
 
6. Veröffentlichen Sie das aktualisierte Add-In auf Ihrer SharePoint-Website.
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Zuordnen einer Dokumentbibliothek zu einer Entität](associate-a-document-library-with-an-entity)
    
 

