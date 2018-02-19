---
title: "Aktualisieren von Add-Ins für SharePoint"
description: "Erstellen und Bereitstellen eines Updates für ein SharePoint-Add-In"
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: a1ff2202cba1fd9c85203ee335848f8894051f59
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="update-sharepoint-add-ins"></a>Aktualisieren von Add-Ins für SharePoint

Sie können Ihr SharePoint-Add-In aktualisieren, indem Sie die in SharePoint integrierte Updateunterstützung verwenden. Innerhalb von 24 Stunden, nachdem Sie eine aktualisierte Version des Add-Ins in den Add-In-Katalog einer Organisation hochgeladen haben oder das Add-In im Office Store angenommen wurde, wird auf der Seite **Websiteinhalte** jeder Website, auf der das Add-In installiert ist, neben dem Add-In angezeigt, dass ein Update verfügbar ist. Wie Sie in Abbildung 1 sehen können, wird Benutzern ein Link angezeigt, um das Update sofort zu installieren.
 
*Abbildung 1: Updateprozess für SharePoint-Add-Ins*

![Die Schritte auf der Benutzeroberfläche zum Aktualisieren einer App](../images/UpdatingApp_AppTileUpdateNotice.png)
 
Ein Benutzer kann das Update installieren, ohne vorher die frühere Version zu deinstallieren. Die Updateinfrastruktur testet die Updateinstallation und setzt sie zurück, falls Fehler auftreten.
 
> [!IMPORTANT]
> Der *Add-In-Typ* kann nicht mithilfe des Updatesystems geändert werden. Sie können beispielsweise nicht ein von SharePoint gehostetes Add-In durch ein Update in ein vom Anbieter gehostetes Add-In ändern. Um den Add-In-Typ zu ändern, müssen Sie [von einem alten Add-In zu einem neuen migrieren](sharepoint-add-ins-update-process.md#Major). Insbesondere weil [das Vorschauprogramm für automatisch gehostete Add-Ins beendet wurde](http://blogs.office.com/2014/05/16/update-on-autohosted-apps-preview-program/.md), sollten Sie beachten, dass ein automatisch gehostetes Add-In nicht durch ein Update in ein vom Anbieter gehostetes Add-In geändert werden kann. Sie müssen das Add-In wie in [Konvertieren eines automatisch gehosteten Add-Ins für SharePoint in ein vom Anbieter gehostetes Add-In](convert-an-autohosted-sharepoint-add-in-to-a-provider-hosted-add-in.md) erklärt konvertieren.

<a name="Prerequisites"> </a>
## <a name="prerequisites-for-updating-a-sharepoint-add-in"></a>Voraussetzungen für das Aktualisieren eines SharePoint-Add-Ins

Bevor Sie ein SharePoint-Add-In aktualisieren, benötigen Sie Folgendes:

- Eine für die Add-In-Isolation konfigurierte SharePoint-Testinstallation. Anweisungen zum Einrichten einer Office 365-Entwicklerwebsite finden Sie unter [Einrichten einer Entwicklungsumgebung für SharePoint-Add-Ins in Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md).

- Die zum Erstellen eines SharePoint-Add-Ins verwendeten Tools werden normalerweise auch zum Aktualisieren des Add-Ins verwendet. Die meisten Entwickler verwenden zum Beispiel Visual Studio und Microsoft Office Developer Tools für Visual Studio zum Erstellen von SharePoint-Add-Ins.

### <a name="core-concepts-to-know-to-update-a-sharepoint-add-in"></a>Kernkonzepte für das Aktualisieren eines SharePoint-Add-Ins

Lesen Sie die Konzepte in der folgenden Tabelle, bevor Sie das Add-In aktualisieren.

|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md)|Informieren Sie sich über die verschiedenen Typen von SharePoint-Add-Ins. Der Updateprozess variiert je nach Typ.|
| [Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process.md)|Informieren Sie sich über das Verfahren zum Aktualisieren von SharePoint-Add-Ins.|
| [Aktualisieren von Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx)|Informieren Sie sich über das Aktualisieren von Features (SharePoint 2010 SDK).|
| [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md)|Informieren Sie sich über die Methoden zum Veröffentlichen, Installieren und Deinstallieren eines SharePoint-Add-Ins.|
| [Behandeln von Ereignissen in SharePoint-Add-Ins](handle-events-in-sharepoint-add-ins.md)|Informieren Sie sich über Remoteereignisempfänger in SharePoint.|

<a name="MajorAppUpgradeSteps"> </a>
## <a name="major-steps-for-updating-an-add-in"></a>Wichtige Schritte beim Aktualisieren eines Add-Ins

Im folgenden werden die wichtigsten Schritte erläutert, die beim Erstellen einer Aktualisierung für ein SharePoint-Add-In durchgeführt werden müssen. Jeder Schritt wird in den zugehörigen Abschnitten oder Artikeln ausführlich erläutert. Nicht alle Schritte sind in jedem Updateprojekt erforderlich. Welche Schritte Sie durchführen müssen, hängt von den Komponenten in Ihrem Add-In und den Komponenten ab, die Sie hinzufügen. Nur die mit `**` gekennzeichneten Elemente sind immer erforderlich.

- Aktualisieren Sie das Add-In-Manifest.

   - `**` Erhöhen Sie die **Versions**nummer im [App](http://msdn.microsoft.com/library/d5f30dfe-7500-5f85-0f08-f4f220c0c692%28Office.15%29.aspx)-Element der Datei „appmanifest.xml“. (Add-Ins wurden bei der ersten Veröffentlichung des Schemas noch „Apps“ genannt). Ändern Sie *nicht* die **ProductID**-Nummer.
   
   - Ändern Sie den [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx)-Abschnitt der Datei „appmanifest.xml“.
   
   - Ändern Sie den [AppPrerequisites](http://msdn.microsoft.com/library/7622b55f-01a1-2c39-9daa-7cfb1a3c890f%28Office.15%29.aspx)-Abschnitt der Datei „appmanifest.xml“.
    
   Weitere Informationen finden Sie unter [Aktualisieren von Add-In-Version, Berechtigungsanforderungen und Voraussetzungen](#UpdateManifest).

- Fügen Sie das Markup für die Add-In-Webkomponenten hinzu, oder aktualisieren Sie dieses. Weitere Informationen finden Sie unter [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint.md).

- Fügen Sie das Markup für die Hostwebkomponenten hinzu, oder aktualisieren Sie dieses. Weitere Informationen finden Sie unter [Aktualisieren von Hostwebkomponenten in SharePoint](update-host-web-components-in-sharepoint.md).

- Fügen Sie benutzerdefinierte Logik zu [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) hinzu, und registrieren Sie sie in der Datei „appmanifest.xml“. Weitere Informationen finden Sie unter [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).
    
- Aktualisieren Sie die Remotekomponenten:
    
   - Aktualisieren Sie bei einem vom Anbieter gehosteten Add-In die Remotekomponenten mithilfe der Techniken, die für den Hostingplattformstapel geeignet sind. 
   
   Weitere Informationen finden Sie unter [Aktualisieren von Remotekomponenten in SharePoint-Add-Ins](update-remote-components-in-sharepoint-add-ins.md).
    
- `**` Laden Sie das Add-In-Paket in den Office Store oder den Add-In-Katalog der Organisation hoch.

<a name="BestUpdatePractices"> </a>
## <a name="best-practices-for-add-in-updates"></a>Bewährte Vorgehensweisen für Add-In-Updates

In den folgenden Abschnitten werden Praktiken, die Sie befolgen sollten, und wichtige Punkte erläutert, die Sie bei der Planung eines Updates berücksichtigen sollten.

### <a name="decide-whether-you-really-have-to-update"></a>Entscheiden Sie, ob ein Update wirklich erforderlich ist

Für ein vom Anbieter gehostetes SharePoint-Add-In ist es für Verbesserungen des Add-Ins nicht unbedingt erforderlich, das Add-In zu aktualisieren. Wenn alle Änderungen an Remotekomponenten vorgenommen werden und diese Änderungen nicht in SharePoint-Komponenten angezeigt werden sollen, können Sie die Remotekomponenten ändern, ohne das Add-In zu aktualisieren. Solange keine Änderungen an den URLs und Verbindungszeichenfolgen erfolgen, die die SharePoint-Komponenten für den Zugriff auf Remotekomponenten verwenden, funktioniert das SharePoint-Add-In weiterhin. 

Beispiel: Sie fügen eine Schaltfläche in einer webbasierten Remoteanwendung hinzu, mit der eine Spalte aus einer SharePoint-Liste gelesen wird, die die Webanwendung zuvor nicht gelesen hat. Wenn die Spalte bereits in der Liste vorhanden ist, müssen Sie keine Änderungen in SharePoint vornehmen. Sie können die überarbeitete Webseite und die überarbeitete CodeBehind-Datei oder JavaScript-Code in der Remote-Webanwendung hochladen. Die neue Funktionalität ist sofort für Benutzer verfügbar, wenn sie das SharePoint-Add-In starten.

### <a name="remember-that-updating-is-optional-for-users"></a>Bedenken Sie, dass Aktualisieren für Benutzer optional ist

Wenn eine neue Version Ihres SharePoint-Add-Ins in dem Office Store oder dem Add-In-Katalog der Organisation verfügbar ist, wird auf der Add-In-Kachel auf der Seite **Websiteinhalte** eine Meldung angezeigt, in der Benutzer darauf hingewiesen werden, dass ein Update verfügbar ist. Es dauert nicht länger als 24 Stunden, bis diese Meldung angezeigt wird. In der SharePoint-Infrastruktur gibt es jedoch keine Möglichkeit, den Benutzer zum Aktualisieren zu zwingen. Änderungen, die Sie an Remotekomponenten vornehmen, dürfen somit nicht die älteren Versionen des Add-Ins zerstören. Sie sollten in der Regel Elemente zu Remotekomponenten *hinzufügen* und es jedoch vermeiden, Elemente zu löschen, umzubenennen, zu verschieben, Änderungen am Schema, der Verbindungszeichenfolge oder der URL vorhandener Komponenten vorzunehmen.

Wenn eine Remotekomponente die Version der aufzurufenden Add-In-Instanz kennen muss, können Sie diese Information aus SharePoint übergeben. Sie können z. B. die Add-In-Version als Abfrageparameter hinzufügen zu der [StartPage](http://msdn.microsoft.com/library/3092674c-a6c3-9021-3d7e-e716562a4a4f%28Office.15%29.aspx)-URL des Add-Ins hinzufügen.

<a name="DebugFirst"> </a>
### <a name="create-and-debug-the-new-version-as-if-it-were-a-brand-new-add-in"></a>Erstellen und Debuggen Sie die neue Version, als ob es ein ganz neues Add-In wäre

Sie sollten die Entwicklung und das Debuggen der neuen Version eines Add-Ins vom Debuggen des Update-Markups und der Updatelogik trennen. Deinstallieren Sie dazu die frühere Version des Add-Ins auf Ihrer SharePoint-Entwicklungstestwebsite. Speichern Sie eine Kopie der Add-In-Paketdatei für die frühere Version. Fügen Sie nach Bedarf Komponenten des Add-In hinzu, und ändern Sie diese, und testen und debuggen Sie diese dann mithilfe der Testwebsite, als ob es sich um ein ganz neues Add-In handeln würde, die Sie von Grund auf neu erstellen.

### <a name="test-the-update-with-each-earlier-version-of-the-add-in"></a>Testen Sie das Update mit jeder früheren Version des Add-Ins

Wenn die neue Version des Add-Ins als neues Add-In ordnungsgemäß funktioniert, strukturieren Sie den Code und das Markup so neu, dass das Projekt ein Update des alten Add-Ins darstellt. Erhöhen Sie zum Beispiel die Add-In-Versionsnummer wie in [Wichtige Schritte beim Aktualisieren eines Add-Ins](#MajorAppUpgradeSteps) angegeben. Weitere Informationen zum Umwandeln des Projekts in ein Update finden Sie in den untergeordneten Themen dieses Themas.

Wenn Sie das Update testen möchten, ziehen Sie die neue Version von der Testwebsite zurück und stellen Sie die frühere Version erneut bereit, damit Sie die Logik des Updates testen können. Wenn Sie über mehrere Vorgängerversionen des Add-Ins verfügen, installieren Sie jede Vorgängerversion auf einer anderen Unterwebsite Ihrer Testwebsite. Laden Sie anschließend die neueste Version des Add-Ins in den Add-In-Katalog der Testwebsite hoch und aktualisieren Sie jede Instanz des Add-Ins. Stellen Sie sicher, dass jede Instanz über die neueste Add-In-Versionsnummer und die neueste Version aller Komponenten verfügt. Wenn das Add-In über ein Add-In-Web verfügt, stellen Sie sicher, dass die Add-In-Webkomponenten mithilfe des Verfahrens unter [Überprüfen der Bereitstellung von-Add-In-Webkomponenten](update-add-in-web-components-in-sharepoint.md#VerifyDeployAppWebComp) bereitgestellt wurden.

<a name="ImmediateUpdateNotice"> </a>
### <a name="update-an-add-in-without-waiting-24-hours"></a>Aktualisieren eines Add-Ins, ohne 24 Stunden zu warten

Wenn Sie ein Update für ein Add-In auf Ihrer SharePoint-Testwebsite entwickeln, ist es unpraktisch, 24 Stunden zwischen Updates warten zu müssen. Sie (und Benutzer auf einer SharePoint-Produktionswebsite) können ein Add-In unmittelbar aktualisieren, nachdem es in den Office Store oder den Add-In-Katalog der Organisation mit diesen Schritten hochgeladen wurde.

#### <a name="to-immediately-update-an-add-in"></a>So aktualisieren Sie ein Add-In sofort

1. Nachdem das aktuelle Update zum Add-In-Katalog hochgeladen wurde, öffnen Sie auf der Website, auf der das Add-In installiert wird, die Seite **Websiteinhalte**, und wählen Sie auf der Kachel des Add-Ins die Schaltfläche **...** aus.

2. Wählen Sie im daraufhin angezeigten Popup die Registerkarte **Info** aus. Die angezeigte **Info**-Seite enthält einen Hinweis darauf, dass eine neue Version verfügbar ist.

3. Wählen Sie die Schaltfläche **Herunterladen** aus. Die Seite **Websiteinhalte** wird erneut geöffnet, und auf der Kachel des Add-Ins wird ein Hinweis angezeigt, dass das Add-In aktualisiert wird.

Abbildung 2 illustriert diese Schritte.

*Abbildung 2. Vorgehensweise, um ein SharePoint-Add-In sofort zu aktualisieren*

![Unmittelbarer App-Upgradeprozess](../images/UpdatingApp_ImmediateUpgradeProcess.png)

> [!NOTE]
> Wenn Sie den Hinweis auf der Kachel des Add-Ins, dass ein Update verfügbar ist, häufiger als alle 24 Stunden anzeigen müssen, können Sie die unter [Aktualisierungsverfahren für ein Add-In für SharePoint](sharepoint-add-ins-update-process.md#Minor) beschriebene Methode verwenden, um den Hinweis sofort anzuzeigen.

<a name="UpdateManifest"> </a>
## <a name="update-the-add-in-version-permission-requests-and-prerequisites"></a>Aktualisieren von Add-In-Version, Berechtigungsanforderungen und Voraussetzungen

Öffnen Sie nach dem Erstellen einer Sicherungskopie des Visual Studio-Projektordners das Add-In-Projekt. Öffnen Sie das Add-In-Manifest und erhöhen Sie im Manifest-Designer die Versionsnummer auf der Registerkarte **Allgemein**.

Wenn die aktualisierte Version des Add-Ins mehr (oder weniger) Berechtigungen für Komponenten des Hostwebs benötigt, nehmen Sie nach Bedarf Änderungen am Abschnitt [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx) des Add-ins vor. Verwenden Sie in Visual Studio die Registerkarte **Berechtigungen** des Manifest-Designers. 

Wenn ein Add-In aktualisiert wird, wird der Benutzer immer aufgefordert, Berechtigungen zu gewähren, unabhängig davon, ob sich die Berechtigungen seit der vorherigen Version geändert haben. Wenn die neue Version *weniger* Berechtigungen als die vorherige Version benötigt, werden die zusätzlichen Berechtigungen der vorherigen Version *nicht widerrufen*. Die einzige Möglichkeit, die Berechtigungen für das Add-In einzugrenzen, die die neue Version benötigt, besteht für Benutzer darin, die Seite *{SharePointDomain}* `/_layouts/15/appinv.aspx` nach der Aktualisierung des Add-Ins zu öffnen und das Berechtigungsmarkup manuell einzugeben, das dem [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx)-Schema entspricht.

Wenn die aktualisierte Version des Add-Ins Anforderungen hat, die frühere Versionen nicht hatten (oder keine Anforderungen mehr hat, die frühere Versionen hatten), nehmen Sie nach Bedarf Änderungen am Abschnitt [AppPrerequisites](http://msdn.microsoft.com/library/7622b55f-01a1-2c39-9daa-7cfb1a3c890f%28Office.15%29.aspx) des Add-Ins vor. Verwenden Sie in Visual Studio die Registerkarte **Erforderliche Komponenten** des Manifest-Designers.

## <a name="next-steps"></a>Nächste Schritte
<a name="Next"> </a>

Fahren Sie mit dem nächsten Aufzählungspunkt im Abschnitt [Wichtige Schritte beim Aktualisieren eines Add-Ins](#MajorAppUpgradeSteps) fort, oder wechseln Sie direkt zu einem der folgenden Artikel:

-  [Aktualisieren von Add-In-Webkomponenten in SharePoint](update-add-in-web-components-in-sharepoint.md)
-  [Aktualisieren von Hostwebkomponenten in SharePoint](update-host-web-components-in-sharepoint.md)
-  [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
-  [Aktualisieren von Remotekomponenten in SharePoint-Add-Ins](update-remote-components-in-sharepoint-add-ins.md)
    
## <a name="see-also"></a>Weitere Artikel
<a name="bk_addresources"> </a>

-  [Entwickeln von SharePoint-Add-ins](develop-sharepoint-add-ins.md)
-  [Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process.md) 
    
 

