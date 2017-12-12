---
title: "Transformieren von farmlösungen für das SharePoint-add-in-Objektmodell"
ms.date: 11/03/2017
ms.openlocfilehash: 1a85b977905013c129be5a8d2eb8febdd8b4d5c1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="transform-farm-solutions-to-the-sharepoint-add-in-model"></a>Transformieren von farmlösungen für das SharePoint-add-in-Objektmodell
Transformieren Sie oder konvertieren Sie Ihrer Farm Solutions in der SharePoint-add-in-Objektmodell. Erfahren Sie, wie Webparts, Seitenlayouts, Gestaltungsvorlagen, Zeitgeberaufträge, und so weiter in der SharePoint-add-in-Objektmodell zu konvertieren.

_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_

Wenn Sie Ihrer SharePoint-Umgebung mithilfe von farmlösungen erweitert haben, und Sie eigene Erweiterungen der SharePoint-add-in-Modells des Übergangs zu SharePoint Online zu erleichtern migrieren möchten, müssen Sie Transformieren Ihrer farmlösungen zur des SharePoint-add-Ins Modell. Transformieren von Ihrer farmlösungen auf die SharePoint umfasst-add-in-Objektmodell, Analysieren Ihrer vorhandenen Extensions, Entwerfen und entwickeln Ihre neue Add-In für SharePoint, und klicken Sie dann testen und Bereitstellen Ihr Add-in in Ihrer produktionsumgebung. Dieser Artikel beschreibt den Prozess und bewährte Methoden bei der Transformation Ihrer farmlösungen zur SharePoint-add-in-Objektmodell verwenden.

## <a name="plan-the-transformation-process"></a>Planen des Transformationsprozesses
<a name="sectionSection0"> </a>

Wenn Sie Ihre Farm Solutions auf das SharePoint-add-in-Objektmodell transformieren, um sicherzustellen, dass die Auswirkung auf die Benutzer minimal ist werden soll. Analysieren Sie, um die aktuelle Farm Solutions, und klicken Sie dann das neue Add-In für SharePoint an den Bedürfnissen des Unternehmens entwerfen. Es wird empfohlen, den folgenden Vorgang aus, um eine erfolgreiche Umstrukturierung sicherzustellen.


1. Bereitschaft. Erfahren Sie mehr über:
    
    - Die SharePoint-add-in-Modell, verschiedene Arten von add-ins und Hostingoptionen. Weitere Informationen finden Sie unter [Übersicht über Add-Ins für SharePoint](https://msdn.microsoft.com/library/office/fp179930.aspx).
    
    - RAS-Technologien für den Zugriff auf Ihre lokale Daten.
    
2. Bewertung der Lösung. Analysieren Sie die funktionalen und geschäftlichen Anforderungen durch: 
    
    - Identifizieren von werden farmlösungen in der aktuellen Umgebung bereitgestellt. Sollten Sie mithilfe von Drittanbietertools um bereitgestellten Extensions zu identifizieren. Führen Sie eine detaillierte Analyse der einzelnen farmlösung identifiziert.
    
    - Überprüfen der Anforderungen für die Benutzer. Bitten Sie Ihren Benutzern zeigen, wie sie die vorhandene Farm Solutions zu ihrer täglichen Arbeit verwenden.
    
    - Identifizieren, dokumentieren und neuen Funktionen zum Einschließen in das neue Add-In für SharePoint zu entwerfen. Erwägen Sie die Liste der neuen Funktion Anforderungen von den Benutzern für zusätzliche Hinweise überprüfen.
    
    - Identifizieren von nicht verwendeten Features, und stimmen mit den Benutzern die ausgelassen werden, diese Funktion vom neuen-add-in für SharePoint. 
    
    - Für jede farmlösung, die bestimmen, ob durch ein Add-In für SharePoint zu ersetzen. Einige Lösungen, wie SharePoint-Zentraladministration-Erweiterungen, können in der SharePoint-add-in-Objektmodell nicht dupliziert werden. Weitere Informationen finden Sie unter [add-ins für SharePoint im Vergleich zu SharePoint-Lösungen](http://msdn.microsoft.com/library/0e9efadb-aaf2-4c0d-afd5-d6cf25c4e7a8.aspx) und [entscheiden zwischen-add-ins für SharePoint und SharePoint Solutions](http://msdn.microsoft.com/library/8459e265-b8fd-4bf8-911e-d63cae8bf96f.aspx).
    
3.  Planen der Lösung. Entwerfen Sie die neue Anwendung mit dem SharePoint-add-in-Modell basierend auf:
    
    - Die Anforderungen in Schritt 2 gesammelt werden.
    
    - Analyse der vorhandenen Code. Während der Codeanalyse, Sie sollten Teile des Codes, die gelöscht werden können (beispielsweise nicht mehr im Code verwendet wird, oder die Anforderungen geändert haben).
    
4. Entwickeln Sie und Testen Sie die SharePoint-add-in-Objektmodellversion der Anwendung. Dies ist in der Regel der zeitaufwendigste Schritt im Transformationsprozess. 
    
5. Das neue Add-in bereitstellen. Je nach Ihren Anforderungen vielleicht lassen Sie die Farm Solutions parallel zu den neuen Add-In für SharePoint ausgeführt, oder Sie können die farmlösung zurückziehen und nur ermöglichen Benutzern die Verwendung des neuen add-Ins für SharePoint. Stellen Sie in beiden Fällen sicher, dass Ihre Bereitstellung stabil ist, und Senden der entsprechenden Kommunikation an Ihre Benutzer. Wenn Ihre Inhalte in der vorhandenen Website, die Sammlungen Ihrer Farm Solutions (z. B. abhängen, wenn Inhalte mit einem Inhaltstyp erstellt wurde), bevor Sie vollständig die farmlösung zurückgezogen haben, müssen Sie den vorhandenen Inhalt mithilfe der neuen SharePoint-add-in-Objektmodell transformieren Lösung. Stellen Sie sicher, dass Sie genügend Zeit zum Abschließen dieser Aufgabe, da es kann zeitaufwändig und schwierig sein können.

## <a name="transformation-approaches-to-deploy-your-new-add-in-for-sharepoint"></a>XSL-Transformation Ansätze zum Bereitstellen von Ihr neues Add-In für SharePoint
<a name="sectionSection1"> </a>

Nach Abschluss der Entwicklung und Komponententests Ihrer neuen-add-in für SharePoint, starten Sie Transformieren von Ihrer farmlösung für das neue Add-In für SharePoint mithilfe der in der folgenden Tabelle aufgeführten Vorgehensweisen Transformation zu.

|**XSL-Transformation Ansatz**|**Beschreibung**|**Vorteile**|**Nachteile**|
|:-----|:-----|:-----|:-----|
|In-place|Das neue Add-In für SharePoint in einer vorhandenen SharePoint-Umgebung bereitstellen. Sie müssen sicherstellen, dass Ihre Website das neue Add-In für SharePoint verwendet wird, bevor Sie die farmlösung zurückziehen.|<ul><li>Weniger allgemeine Beeinträchtigung für die Benutzer.</li><li>Weniger Ressourcen benötigt, da Sie eine vorhandene SharePoint-Umgebung verwenden.</li><li>Keine Notwendigkeit zur Drittanbieter-Tools.</li><li>Minimale Website Ausfallzeiten.</li><li>Aktualisieren Sie eine Websitesammlung, anstatt die gesamte Farm alle gleichzeitig zu aktualisieren.</li><li>URLs werden nicht geändert.</li></ul>|<ul><li>Schwierig zum Nachverfolgen des Status aller betroffenen Anlagen auf einer Website.</li><li>Erhöhte Gefahr von verwaisten Objekte erstellen. Wenn eine Anlage in eine Datei im Dateisystem, der nicht vorhanden ist verweist, wird dies als verwaist bezeichnet.</li></ul>|
|Einsatz oder Migration von Inhalten|Extrahieren Sie Ihre Inhalte aus vorhandenen Websitesammlungen, in Ihrer Farm Solutions werden derzeit bereitgestellt und Bereitstellung des Inhalts in einer neuen Websitesammlung, die das neue Add-In für SharePoint verwendet. Wenn Sie Inhalte zu SharePoint Online migrieren, wird dieser Prozess normalerweise verwendet.|<ul><li>Bereinigen Sie SharePoint-Umgebung mit keine vorherigen Farm lösungsabhängigkeiten.</li><li>Die neue Websitesammlung wird von der produktionsumgebung isoliert. Freigeben die aktualisierten Websitesammlung beim bereit. < / li.</ul>|<ul><li>Erfordert Drittanbieter-Tools, die mit der Migration von Inhalten zu unterstützen.</li><li>Eine zusätzliche SharePoint-Umgebung erforderlich ist.</li><li>Website Ausfallzeit erforderlich.</li><li>URLs können sich ändern, wenn Sie beide Websites für eine bestimmte Zeitspanne die parallele Ausführung beibehalten.</li>|

## <a name="best-practices-for-specific-farm-solutions"></a>Bewährte Methoden für bestimmte farmlösungen
<a name="sectionSection2"> </a>

Gelten Sie die folgenden bewährten Methoden bei der Umwandlung von bestimmten Lösungen:


- Seitenlayouts und Masterseiten. Benutzerdefinierten Seitenlayouts und Masterseiten können vorhanden sein, in der Veröffentlichung von Websites und Teamwebsites mit die Veröffentlichungsfeatures aktiviert. Seitenlayouts und Masterseiten zu ersetzen:
    
  1. Laden Sie die neue Seite Layout oder des Masters Seite zu Ihrer Website hoch. Laden Sie neue Masterseiten und Seitenlayouts in Ihrer Websitesammlung manuell oder mithilfe von remote-APIs. Remote-APIs umfassen das Client-seitigen Objektmodell (CSOM) oder REST. Dadurch wird sichergestellt, dass die Gestaltungsvorlagen und Seitenlayouts nicht Abhängigkeiten auf einer farmlösung haben. 
    
  2. Konfigurieren Sie Ihre Website, um die neuen Seitenlayouts und Masterseiten verwenden.
    
  3. Ziehen Sie die vorherige Version des Seitenlayouts und Masterseiten zurück.
    
- Webparts und Steuerelemente. So ersetzen Sie Webparts und Steuerelemente
    
  1. Überprüft alle vorhandenen Seiten, um zu bestimmen, welche Seiten WebParts.
    
  2. (Optional) Überprüfen Sie Out-of-Box-Webparts zu ermitteln, ob alle Ihre benutzerdefinierten Webparts ersetzen können.
    
  3. Ersetzen Sie vorhandenen Webparts mit app-Webpart-Instanzen, oder verwenden andere Techniken (beispielsweise eingebettete JavaScript in Seiten oder Seitenlayouts), um die gleiche Funktionalität zu erreichen.

  4. Verwenden Sie eingebettetes JavaScript zum Manipulieren von UI-Elemente.
    
    > [!NOTE] 
    > Um Ihre vorhandenen Webparts mit app-Webparts zu ersetzen, müssen Sie:

    - Seite Laden von Add-Ins in Office 365-Abonnement aktivieren. Wenden Sie sich an den Office 365-Administrator.
    - Verwenden Sie CSOM, um die Seite Laden des add-Ins auf Ihrer Website zu aktivieren. Weitere Informationen finden Sie im Codebeispiel Core.SideLoading.
    - Installieren Sie Ihr app-Webpart auf Ihrer Website ein.
    - Seite Laden von add-ins auf Ihrer Website deaktivieren.
    - Deaktivieren Sie die Seite Laden von Add-Ins in Office 365-Abonnements. Wenden Sie sich an den Office 365-Administrator.

- Seite zum Bearbeiten. Sie müssen möglicherweise Seite Bearbeitung während Ihrer benutzerdefinierten Site Bereitstellungsprozesses implementieren. Im Codebeispiel [Provisioning.Pages](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages) zeigt die Seite Techniken zur Bearbeitung, einschließlich des Erstellens einer Wiki-Seiten, Hinzufügen von HTML auf der Seite Erstellen einer Liste mit höher gestuften Links, Erstellen von Seiten mit verschiedenen Layouts, Hinzufügen von Out-of-Box-Webparts auf der Seite Inhalten, und Entfernen von der Seite.
    
- Websitespalten, Listendefinitionen und Inhaltstypen. Wenn Ihre Websitespalten, Listendefinitionen und Inhaltstypen erstellt wurden mithilfe der Feature-Framework-Elemente, die über farmlösungen bereitgestellt wurden, müssen Sie den Einsatz oder der Inhaltsmigration Transformation Ansatz verwenden. Dies gilt nicht für Feature-Framework-Elemente mithilfe von sandkastenlösungen bereitgestellt. Um die Inhaltsmigration Transformation Ansatz verwenden, müssen Sie Drittanbietertools verwenden, um die Farm lösungsabhängigkeiten zu entfernen.
    
- Module oder Feature Framework. Module verwenden von Zeigern zum Dateien, was bedeutet, dass die Dateien nicht angepasst werden und im Dateisystem bereitgestellt werden. Wenn Ihre Farm Solutions Module verwenden, Anpassen der Dateien durch die Bereitstellung von alternativen Versionen der gleichen Dateien in die Inhaltsdatenbank, überprüfen und Aktualisieren von Lösungen, zeigen Sie auf die neuen Dateien in der Inhaltsdatenbank gespeichert und Zurückziehen klicken Sie dann die farmlösung, die auf das verwiesen Dateien im Dateisystem gespeichert.
    
- Websitevorlagen und Webvorlagen. Sie sollten Schwerpunktthemen Transformieren von featureelementen Framework mithilfe der Websitevorlage oder eine Webvorlage bereitgestellt. Angenommen, stellen Sie sicher, dass die Seite "default.aspx" der Website nicht ersetzt wird, wenn die farmlösung zurückziehen.
    
- Zeitgeberaufträge. Wenn Sie SharePoint Online verwenden, können nicht Sie erstellen und Verwalten von Zeitgeberaufträgen. Stattdessen können Sie eine Konsolenanwendung erstellen, die Windows-Taskplaner oder ein [Azure Webauftrag](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/) planen und Ausführen der Konsolenanwendung Remote verwendet. Wenn Sie einen benutzerdefinierten Zeitgeberauftrag zu erstellen, bestimmen Sie, ob Sie ein bestimmtes Konto oder eine nur-app-Token OAuth-basierte verwenden müssen. Im Codebeispiel [Core.TimerJobs.Samples](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples) zeigt, wie Ihre eigenen benutzerdefinierten Zeitgeberauftrag zu erstellen.
    
    > [!NOTE] 
    > Wenn der Zeitgeberauftrag für serverseitigen Code verwendet wird, müssen Sie Umgestalten des Zeitgeberauftrags, um das CSOM oder eine andere Methode zu verwenden.

|**Artikel**|**Zeigt, wie Sie auf**|
|:-----|:-----|
|[Ersetzen Sie Inhaltstypen und Websitespalten](replace-sharepoint-content-types-and-site-columns.md)|Verwenden Sie CSOM, um SharePoint Content Inhaltstypen und Websitespalten, neue Inhaltstypen Websitespalten hinzufügen, und ersetzen die Inhaltstypen durch neue Inhaltstypen zu ersetzen.|
|[Ersetzen von Dateien mithilfe von Modulen in farmlösungen bereitgestellt](replace-files-deployed-using-modules-in-sharepoint-farm-solutions.md)|Ersetzen Sie Dateien wie Masterseiten und Seitenlayouts in SharePoint, die Verwendung von Modulen in farmlösungen durch Hochladen und Aktualisieren der Verweise von neuen Dateien bereitgestellt wurden.|
|[Ersetzen von Listendefinitionen erstellte Listen](replace-sharepoint-lists-created-from-list-definitions.md)|Ersetzen Sie Listen und Bibliotheken, die mithilfe von Listendefinitionen in SharePoint erstellt wurden.|
|[Ersetzen Sie die Webparts durch Add-in-Webparts](replace-sharepoint-web-parts-with-add-in-parts.md)|Verwenden des Transformationsprozess Webparts mithilfe des SharePoint-Clientobjektmodells (CSOM) mit Add-in-Webparts zu ersetzen.|

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
-  [Erstellen von Add-Ins für SharePoint](https://msdn.microsoft.com/library/jj163230.aspx)
