
# <a name="update-sharepoint-add-ins"></a>Aktualisieren von Add-Ins für SharePoint
Erfahren Sie, wie Sie ein Update für ein SharePoint-Add-In erstellen und bereitstellen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Sie können Ihr SharePoint-Add-In mithilfe der in SharePoint integrierten Updateunterstützung aktualisieren. Innerhalb von 24 Stunden, nachdem Sie eine aktualisierte Version des Add-Ins in den Add-In-Katalog eines Unternehmens hochgeladen haben oder das Add-In im Office Store angenommen wurde, wird auf der Seite **Websiteinhalte** jeder Website, auf der das Add-In installiert ist, neben dem Add-In angezeigt, dass ein Update verfügbar ist. Wie Sie in Abbildung 1 sehen können, wird Benutzern ein Link angezeigt, um das Update sofort zu installieren.
 

**Abbildung 1: Updateprozess für SharePoint-Add-Ins**

 

 
![Die Schritte auf der Benutzeroberfläche zum Aktualisieren einer App](../../images/UpdatingApp_AppTileUpdateNotice.png)
 
Ein Benutzer kann das Update installieren, ohne vorher die frühere Version zu deinstallieren. Die Updateinfrastruktur testet die Updateinstallation und setzt sie zurück, falls Fehler auftreten.
 

    
 **Wichtig** Sie können den *Add-In-Typ* nicht über ein Update des Systems ändern. Sie können beispielsweise nicht ein in SharePoint gehostetes Add-In durch ein Update in ein vom Anbieter gehostetes Add-In ändern. Um den Add-In-Typ zu ändern, müssen Sie [von einem alten Add-In zu einem neuen Add-In migrieren](sharepoint-add-ins-update-process#Major). Insbesondere da [das Vorabprogramm für automatisch gehostete Add-Ins beendet wurde](http://blogs.office.com/2014/05/16/update-on-autohosted-apps-preview-program/), sollten Sie beachten, dass ein automatisch gehostetes Add-In nicht durch ein Update in ein vom Anbieter gehostetes Add-In geändert werden kann. Sie müssen das Add-In wie in [Konvertieren eines automatisch gehosteten SharePoint-Add-Ins in ein vom Anbieter gehostetes Add-In](convert-an-autohosted-sharepoint-add-in-to-a-provider-hosted-add-in) erklärt konvertieren.
 


## <a name="prerequisites-for-updating-a-sharepoint-add-in"></a>Voraussetzungen für das Aktualisieren eines SharePoint-Add-Ins
<a name="Prerequisites"> </a>


 

 

- Eine für die Add-In-Isolation konfigurierte SharePoint-Testinstallation. Weitere Informationen zum Einrichten einer Website für Office 365-Entwickler finden Sie unter  [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365).
    
 
- Die zum Erstellen einer SharePoint-Add-In verwendeten Tools werden normalerweise auch zum Aktualisieren des Add-Ins verwendet. Die meisten Entwickler verwenden beispielsweise Visual Studio und Microsoft Office-Entwicklertools für Visual Studio zum Erstellen von SharePoint-Add-Ins.
    
 

### <a name="core-concepts-to-know-to-update-a-sharepoint-add-in"></a>Kernkonzepte für das Aktualisieren eines SharePoint-Add-Ins


 

 

**Tabelle 1. Kernkonzepte für das Aktualisieren eines SharePoint-Add-Ins**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [Auswählen von Mustern für die Entwicklung und das Hosten Ihres SharePoint-Add-Ins](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in)|Informieren Sie sich über die verschiedenen Typen von SharePoint-Add-Ins. Der Updateprozess variiert je nach Typ.|
| [Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process)|Informieren Sie sich über das Verfahren zum Aktualisieren von SharePoint-Add-Ins.|
| [Aktualisieren von Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx)|Informieren Sie sich über das Aktualisieren von Features (SharePoint 2010 SDK).|
| [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options)|Informieren Sie sich über die Methoden zum Veröffentlichen, Installieren und Deinstallieren eines SharePoint-Add-Ins.|
| [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins)|Informieren Sie sich über Remoteereignisempfänger in SharePoint.|

## <a name="major-steps-in-updating-an-add-in"></a>Wichtige Schritte beim Aktualisieren eines Add-Ins
<a name="MajorAppUpgradeSteps"> </a>

Im Folgenden werden die wichtigsten Schritte beschrieben, die beim Erstellen eines Updates für ein SharePoint-Add-In erforderlich sein können. Jeder Schritt wird in verlinkten Abschnitten oder Artikeln näher erläutert. Nicht alle Schritte sind in jedem Updateprojekt erforderlich. Welche Schritte für Ihr Add-In erforderlich sind, hängt von den Komponenten ab, die sich bereits in Ihrem Add-In befinden, und davon, welche Komponenten Sie hinzufügen. Nur die mit ***** markierten Elemente sind immer erforderlich.
 

 

- Aktualisieren Sie das Add-In-Manifest.
    
      -  ***** Erhöhen Sie die **Version**snummer im  [App](http://msdn.microsoft.com/library/d5f30dfe-7500-5f85-0f08-f4f220c0c692%28Office.15%29.aspx)-Element der appmanifest.xml-Datei. (Add-Ins wurden bei der ersten Veröffentlichung des Schemas noch "Apps" genannt) Ändern Sie  *nicht*  die **ProductID**-Nummer.
    
 
  - Ändern Sie den [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx)-Abschnitt der appmanifest.xml-Datei.
    
 
  - Ändern Sie den [AppPrerequisites](http://msdn.microsoft.com/library/7622b55f-01a1-2c39-9daa-7cfb1a3c890f%28Office.15%29.aspx)-Abschnitt der appmanifest.xml-Datei.
    
 

    Weitere Informationen finden Sie unter [Aktualisieren von Add-In-Version, Berechtigungsanforderungen und Voraussetzungen](#UpdateManifest).
    
 
- Fügen Sie das Markup für Add-In-Web-Komponenten hinzu, oder aktualisieren Sie es. Weitere Informationen finden Sie unter [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint-2013).
    
 
- Fügen Sie das Markup für Hostwebkomponenten hinzu, oder aktualisieren Sie es. Weitere Informationen finden Sie unter [Aktualisieren von Hostwebkomponenten in SharePoint](update-host-web-components-in-sharepoint-2013).
    
 
- Fügen Sie einem  [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) benutzerdefinierte Logik hinzu, und registrieren Sie ihn in der appmanifest.xml-Datei. Weitere Informationen finden Sie unter [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins).
    
 
- Aktualisieren Sie die Remotekomponenten:
    
      - Aktualisieren Sie bei einem vom Anbieter gehosteten Add-In die Remotekomponenten mithilfe der Techniken, die für den Hostingplattformstapel geeignet sind.
    
 

    Weitere Informationen finden Sie unter [Aktualisieren von Remotekomponenten in SharePoint-Add-Ins](update-remote-components-in-sharepoint-add-ins).
    
 
-  ***** Laden Sie das Add-In-Paket in den Office Store oder den Add-In-Katalog des Unternehmens hoch.
    
 

## <a name="best-practices-for-add-in-updates"></a>Bewährte Vorgehensweisen für Add-In-Updates
<a name="BestUpdatePractices"> </a>

In den folgenden Abschnitten werden Praktiken, die Sie befolgen sollten, und wichtige Punkte erläutert, die Sie bei der Planung eines Updates berücksichtigen sollten.
 

 

### <a name="decide-whether-you-really-have-to-update"></a>Entscheiden Sie, ob ein Update wirklich erforderlich ist

Bei einem vom Anbieter gehosteten SharePoint-Add-In erfordern Verbesserungen an dem Add-In nicht unbedingt eine Aktualisierung des Add-Ins. Wenn sich alle Änderungen auf Remotekomponenten beziehen und diese Änderungen nicht in SharePoint-Komponenten übernommen werden müssen, können Sie die Remotekomponenten ändern, ohne das Add-In zu aktualisieren. Solange sich die URLs und Verbindungszeichenfolgen, welche die SharePoint-Komponenten für den Zugriff auf die Remotekomponenten verwenden, nicht ändern, funktioniert die SharePoint-Add-In weiterhin. Beispiel: Angenommen, Sie fügen einer Remotewebanwendung eine Schaltfläche hinzu, die eine Spalte aus einer SharePoint-Liste liest, welche die Webanwendung bisher nicht gelesen hat. Wenn die Spalte in der Liste bereits vorhanden ist, müssen Sie in SharePoint keine Änderungen vornehmen. Sie können die überarbeitete Webseite und den überarbeiteten Code dahinter oder JavaScript in die Remotewebanwendung hochladen. Die neue Funktion steht Benutzern sofort zur Verfügung, wenn sie die SharePoint-Add-In starten.
 

 

### <a name="remember-that-updating-is-optional-for-users"></a>Bedenken Sie, dass Aktualisieren für Benutzer optional ist

Wenn eine neue Version Ihrer SharePoint-Add-In im Office Store oder im Add-In-Katalog des Unternehmens verfügbar ist, wird auf der Seite **Websiteinhalte** auf der Kachel des Add-Ins eine Meldung angezeigt, die Benutzer darüber informiert, dass ein Update verfügbar ist. Es dauert maximal 24 Stunden, bis diese Meldung angezeigt wird. Es gibt aber nichts in der SharePoint-Infrastruktur, das Benutzer zum Aktualisieren zwingt. Änderungen, die Sie an Remotekomponenten vornehmen, dürfen also die älteren Versionen des Add-Ins nicht unbrauchbar machen. In den meisten Fällen gilt, dass Sie Remotekomponenten Elemente *hinzufügen* , aber das Schema, die Verbindungszeichenfolge oder die URL einer bestehenden Komponente nicht löschen, umbenennen, verschieben oder ändern sollten.
 

 
Wenn eine Remotekomponente die Version der Add-In-Instanz kennen muss, von der sie aufgerufen wird, können Sie diese Informationen von SharePoint übergeben. Sie können die Add-In-Version beispielsweise als Abfrageparameter in der URL der  [Startseite](http://msdn.microsoft.com/library/3092674c-a6c3-9021-3d7e-e716562a4a4f%28Office.15%29.aspx) des Add-Ins hinzufügen.
 

 

### <a name="create-and-debug-the-new-version-as-if-it-were-a-brand-new-add-in"></a>Erstellen und Debuggen Sie die neue Version, als ob es ein ganz neues Add-In wäre
<a name="DebugFirst"> </a>

Sie sollten die Entwicklung und das Debuggen der neuen Version eines Add-Ins vom Debuggen des Update-Markups und der Updatelogik trennen. Deinstallieren Sie dazu die frühere Version des Add-Ins auf Ihrer SharePoint-Entwicklungstestwebsite. Speichern Sie eine Kopie der Add-In-Paketdatei für die frühere Version. Fügen Sie nach Bedarf Komponenten des Add-In hinzu, und ändern Sie diese, und testen und debuggen Sie diese dann mithilfe der Testwebsite, als ob es sich um ein ganz neues Add-In handeln würde, die Sie von Grund auf neu erstellen.
 

 

### <a name="test-the-update-with-each-earlier-version-of-the-add-in"></a>Testen Sie das Update mit jeder früheren Version des Add-Ins
<a name="DebugFirst"> </a>

Wenn die neue Version des Add-Ins als ein "neues" Add-In korrekt funktioniert, strukturieren Sie den Code und das Markup so um, dass das Projekt ein Update des alten Add-Ins ist. Erhöhen Sie die Add-In-Versionsnummer z. B. so, wie unter  [Wichtige Schritte beim Aktualisieren eines Add-Ins](#MajorAppUpgradeSteps) angegeben. Weitere Informationen dazu, wie Sie das Projekt in ein Update verwandeln, finden Sie in den untergeordneten Themen dieses Themas.
 

 
Wenn Sie zum Testen Ihres Updates bereit sind, entfernen Sie die neue Version auf der Testwebsite, und stellen Sie die frühere Version erneut bereit, damit Sie die Updatelogik testen können. Wenn Sie mehrere frühere Versionen des Add-Ins bereitgestellt haben, installieren Sie jede frühere Version auf einer anderen Unterwebsite Ihrer Testwebsite. Laden Sie dann die neueste Version des Add-Ins in den Add-In-Katalog Ihrer Testwebsite hoch, und aktualisieren Sie jede Instanz des Add-Ins. Stellen Sie sicher, dass jede Instanz die neueste Add-In-Versionsnummer und die neuste Version aller Komponenten aufweist. Wenn das Add-In ein Add-In-Web enthält, stellen Sie sicher, dass die Add-In-Web-Komponenten mithilfe des Verfahrens in  [Überprüfen der Bereitstellung von Add-In-Web-Komponenten](update-add-in-web-components-in-sharepoint-2013#VerifyDeployAppWebComp) bereitgestellt wurden.
 

 

### <a name="update-an-add-in-without-waiting-24-hours"></a>Aktualisieren eines Add-Ins, ohne 24 Stunden zu warten
<a name="ImmediateUpdateNotice"> </a>

Wenn Sie ein Update für ein Add-In auf Ihrer SharePoint-Testwebsite entwickeln, ist es unpraktisch, zwischen Updates 24 Stunden zu warten. Sie (und Benutzer auf einer SharePoint-Produktionswebsite) können ein Add-In mit diesen Schritten sofort aktualisieren, nachdem sie in den Office Store oder den Add-In-Katalog des Unternehmens hochgeladen wurde:
 

 

### <a name="to-immediately-update-an-add-in"></a>So aktualisieren Sie ein Add-In sofort


1. Nachdem das aktuelle Update zum Add-In-Katalog hochgeladen wurde, öffnen Sie auf der Website, auf der das Add-In installiert wird, die Seite **Websiteinhalte**, und wählen Sie auf der Kachel des Add-Ins die Schaltfläche **...** aus.
    
 
2. Wählen Sie im daraufhin angezeigten Popup die Registerkarte **Info** aus. Die angezeigte **Info**-Seite enthält einen Hinweis darauf, dass eine neue Version verfügbar ist.
    
 
3. Wählen Sie die Schaltfläche **Herunterladen** aus. Die Seite **Websiteinhalte** wird erneut geöffnet, und auf der Kachel des Add-Ins wird ein Hinweis angezeigt, dass das Add-In aktualisiert wird.
    
 
Abbildung 2 illustriert diese Schritte.
 

 

**Abbildung 2. Vorgehensweise, um ein SharePoint-Add-In sofort zu aktualisieren**

 

 
![Unmittelbarer App-Upgradeprozess](../../images/UpdatingApp_ImmediateUpgradeProcess.png)
 

    
 **Hinweis** Wenn Sie den Hinweis auf der Kachel des Add-Ins, dass ein Update verfügbar ist, häufiger als alle 24 Stunden anzeigen müssen, können Sie die unter [Aktualisierungsverfahren für einSharePoint-Add-In](sharepoint-add-ins-update-process#Minor) beschriebene Methode verwenden, um den Hinweis sofort anzuzeigen.
 


## <a name="update-the-add-in-version-permission-requests-and-prerequisites"></a>Aktualisieren von Add-In-Version, Berechtigungsanforderungen und Voraussetzungen
<a name="UpdateManifest"> </a>

Öffnen Sie das Add-In-Projekt, nachdem Sie eine Sicherungskopie des Visual Studio-Projektordners erstellt haben. Öffnen Sie das Add-In-Manifest, und erhöhen Sie im Manifest-Designer auf der Registerkarte **Allgemein** die Versionsnummer.
 

 
Wenn die aktualisierte Version des Add-Ins weitere (oder weniger) Berechtigungen für die Komponenten des Hostwebs benötigt, nehmen Sie nach Bedarf Änderungen  [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx) des Add-Ins vor. Verwenden Sie in Visual Studio die Registerkarte **Berechtigungen** des Manifest-Designers. Wenn ein Add-In aktualisiert wird, wird der Benutzer immer zur Gewährung von Berechtigungen aufgefordert, unabhängig davon, ob sich die Berechtigungen im Vergleich zu der vorherigen Version geändert haben. Wenn die neue Version *weniger*  Berechtigungen als die vorherige erfordert, werden die zusätzlichen Berechtigung der vorherigen Version *nicht abgerufen*  . Die einzige Möglichkeit zum Einschränken der Add-In-Berechtigungen ist, dass der Benutzer die Seite *{SharePointDomain}*  `/_layouts/15/appinv.aspx` öffnet, nachdem das Add-In aktualisiert wurde und anschließend das Berechtigungsmarkup manuell einzugeben, dass dem [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx)-Schema entspricht.
 

 
Wenn die aktualisierte Version des Add-Ins Anforderungen hat, die frühere Versionen nicht hatten (oder keine Anforderungen mehr hat, die frühere Versionen hatten), nehmen Sie nach Bedarf Änderungen am Abschnitt  [AppPrerequisites](http://msdn.microsoft.com/library/7622b55f-01a1-2c39-9daa-7cfb1a3c890f%28Office.15%29.aspx) des Add-Ins vor. Verwenden Sie in Visual Studio die Registerkartte **Anforderungen** des Manifest-Designers.
 

 

## <a name="next-steps"></a>Nächste Schritte
<a name="Next"> </a>

Fahren Sie mit dem nächsten Aufzählungspunkt im Abschnitt [Wichtige Schritte beim Aktualisieren eines Add-Ins](#MajorAppUpgradeSteps) fort, oder wechseln Sie direkt zu einem der folgenden Artikel:
 

 

-  [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint-2013)
    
 
-  [Aktualisieren von Hostwebkomponenten in SharePoint](update-host-web-components-in-sharepoint-2013)
    
 
-  [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins)
    
 
-  [Aktualisieren von Remotekomponenten in SharePoint-Add-Ins](update-remote-components-in-sharepoint-add-ins)
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Entwickeln von SharePoint-Add-Ins](develop-sharepoint-add-ins)
    
 
-  [Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process)
    
 

