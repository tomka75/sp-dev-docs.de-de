---
title: OneDrive for Business Anpassung in der SharePoint-add-in-Objektmodell
ms.date: 11/03/2017
ms.openlocfilehash: 321dd53b1c8040318069edbbc4471bf47c27c7f2
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
<a name="onedrive-for-business-customization-in-the-sharepoint-add-in-model"></a>OneDrive for Business Anpassung in der SharePoint-add-in-Objektmodell
==================================================================

<a name="summary"></a>Summary
-------

Ansatz verwenden Sie zum Anpassen von OneDrive für Websites mit Geschäftsdaten in das neue SharePoint-Add-in-Modell ist gegenüber mit vollständigen vertrauen Code geändert.  In einer typischen vollständige vertrauen Code (FTC) / SharePoint-Zeitgeberaufträgen Farmlösung Szenario wurden durch den SharePoint Server-Side Object Model Code erstellt, über Farmlösungen bereitgestellt und in der Website der SharePoint-Zentraladministration verwaltet.  SharePoint verarbeitet die Planung und die Ausführung des Zeitgeberauftrags in diesem Szenario. 

In einem Szenario mit SharePoint-Add-Ins Modell Zeitgeberaufträge erstellt und außerhalb von SharePoint geplant.  SharePoint ist nicht für die Planung oder die Ausführung des Zeitgeberauftrags in diesem Szenario verantwortlich.

<a name="why-would-you-customize-onedrive-for-business-sites"></a>Warum würde OneDrive for Business-Websites werden angepasst?
----------------------------------------------------
Zahlreiche verschiedene Aspekte Leuchten Anpassung zu OneDrive für Unternehmen (OD4B) Websites anwenden. Sie können diese Websites natürlich, da sie die SharePoint-Websites sind, aber gleichzeitig immer Sie die kurz- und langfristigen Auswirkungen der Anpassung sollten anpassen.

<a name="high-level-guidelines"></a>Hohe Stufe Richtlinien
---------------------

In der Regel von einer Ziehpunkt möchten wir die folgenden Richtlinien auf hohen Ebenen für das Anpassen von OD4B Websites bereitstellen.

- Anwenden von branding anpassen, die mit Office 365-Designs oder Designmodul für SharePoint-Website
- Wenn Design Module nicht genug sind, können Sie einige CSS-Einstellungen mit alternativen CSS-Option anpassen.
- Vermeiden Sie OD4B-Websites mithilfe von benutzerdefinierten Gestaltungsvorlagen, da Sie zusätzliche langfristig Kosten und Probleme mit zukünftige Updates Dadurch wird anpassen
    + In den meisten Fällen erreichen Sie alle branding Standardszenarien mit Designs und alternative CSS, damit dies nicht wirklich diese Beschränkung ist
    + Wenn Sie benutzerdefinierte Masterseiten verwenden möchten, bereiten Sie zum Anwenden von Änderungen auf die Websites, wenn wichtige Updates funktionsfähig zu Office 365 angewendet werden
- Sie können zum Ändern oder Ausblenden von Funktionen in der Website Einbetten von JavaScript
- CSOM können Sie beispielsweise steuern Sprache oder regionalen Einstellungen in der OD4B-Websites (siehe [neue APIs](http://blogs.msdn.com/b/vesku/archive/2014/12/15/latest-api-updates-in-client-side-object-model-dec-2014-cu-for-sp2013.aspx))
- Wir empfehlen nicht die Verwendung von Inhaltstypen und Websitespalten in OD4B Websites zur Vermeidung von Problemen mit den erforderlichen Feldern oder andere Elemente, die wodurch Probleme bei normalen Anwendungsfälle mit OD4B Websites könnte
    + Stellen Sie sich OD4B Websites wie für persönliche unstrukturierte Daten und Dokumenten. Teamwebsites und befindet sich für die Zusammenarbeit sind dann für Unternehmensdaten und Dokumente, in dem Sie sicherlich jegliches Informationsverwaltungsrichtlinien und Metadaten verwenden können, sollen.

Als eine Zusammenfassung Anpassung wird auf jeden Fall in Office 365 unterstützt und Sie können beibehalten auf ihrer Verwendung in OD4B Websites. Nur tatsächlich möchten wir sicherstellen, dass Sie die kurz- und langfristigen Auswirkungen der Anpassung von Betrieb und Wartung Perspektive berücksichtigen. Dies ist nicht wirklich spezifisch für SharePoint, vielmehr Daumenregel für alle IT-Lösung Build mit einer beliebigen Plattform.

Es folgt ein Beispiel der OD4B-Website, die von oben angegebenen Richtlinien angepasst wurde. In diesem Fall hat das Endergebnis mit Kombination von Office 365-Designs, Websitedesign und Nutzung von so genannte JavaScript Einbetten von Muster erreicht wurde.

![Eine Ansicht einer nach Abschluss des Vorgangs benutzerdefinierte OD4B-Website.](media/Recipes/OD4BCustomization/OD4B-branded.png)

<a name="challenge-with-applying-onedrive-for-business-site-customizations"></a>Anwenden von OneDrive for Business-websiteanpassungen-Abfrage
-----------------------------------------------------------------

Beginnen Sie mit definieren, was die Herausforderung ist, und was versuchen wir hier lösen. Technisch gesehen jedes OneDrive for Business-Website ist zurzeit identisch-Architektur in der persönlichen oder Meine Websites in SharePoint 2007 oder 2010 Version verwendet verwenden. Dies bedeutet, technisch jedes OneDrive für Business-Website ihre eigene Websitesammlung ist und wir keine zentralen Ort zum branding oder eines anderen Anpassungen gelten müssen.

![Jede OneDrive for Business-Website ist eine eigene Websitesammlung unter der verwaltete Pfad der persönlichen und jede Url wird basierend auf dem Benutzerprofil erstellt. Wenn Contoso-my.sharepoint.com der Hauptwebsite ist, werden Johns Website beispielsweise contoso-my.sharepoint.com/personal/john_contoso_com.](media/Recipes/OD4BCustomization/OD4B-topolgy.png)

Klassische Lösung erforderlichen Konfiguration auf die OneDrive for Business-Websites anwenden (einschließlich Meine oder persönliche Websites) wurde basierend auf [Funktion Heften in auf Farmebene](http://cks.codeplex.com/releases/view/2824). Dies bedeutete, dass Sie farmlösung für die SharePoint-Farm bereitgestellt und Feature-Framework zum Zuordnen von Ihrem benutzerdefinierten Features jedes Mal aktiviert werden verwendet eine Meine Website erstellt wurden, klicken Sie dann der Anwendung erforderlichen Anpassungen verantwortlich war. Diese ähnlichen Ansatz funktioniert nicht in Office 365, da es erfordert farmlösung bereitgestellt werden und das geht einfach mit Office 365-Websites. Daher müssen wir Alternativen zum Anwenden der erforderlichen Änderungen auf die Websites zu suchen.

In Office 365 es keine zentrale Ereignis ausgelöst ist, die wir unsere benutzerdefinierten Code, wenn verbinden konnte wird OD4B-Website erstellt. Dies bedeutet, dass wir genauer alternative Lösungen müssen also durchaus üblich mit app-Modell Ansätze. Führen Sie nicht auf dem alten Modellen bleiben Sie, überlegen Sie, wie Sie dieselbe Endergebnis mit neuen APIs und Technologien zu erzielen. Im Hinblick auf reine Anforderung es spielt keine Rolle wirklich wie wir die Anpassungen anwenden auf den Websites, solange sie angewendet werden, da geschäftsanforderung ist nicht für das Heften Feature verwenden, er hat zum Anwenden benötigt Anpassungen mit, was unterstützt Technische Mechanismus.

<a name="different-options-for-applying-customization"></a>Verschiedene Optionen zum Anwenden der Anpassung
============================================

In der Praxis haben wir vier verschiedene Mechanismen OD4B Websites in Office 365 zentralisierte Anpassung zuweisen. Sie könnten auch manuelle Option wie der fünften berücksichtigen, aber im Fall müssen Hunderte oder Tausende von OD4B Websites, mit der manuellen Optionen ist nicht wirklich eine realistische Option. Nachfolgend finden Sie die verschiedenen Optionen haben wir.

1. Office 365-Suite-Ebene Settings (Office 365-Designs und andere Einstellungen)
2. Ausgeblendete app-Webpart mit Benutzerkontext
3. Vor dem Erstellen und Anwenden von Konfiguration
4. Remote Zeitgeberauftrag basierend auf Profil benutzeraktualisierungen

Die Optionen haben Vorteile und Nachteile in diese und die richtige Option hängt von Ihrer detaillierte geschäftlichen Anforderungen. Einige dieser Einstellungen Sie können auch anwenden der Office 365-Suite-Ebene, aber häufig würde werden Suchen Sie einige weitere Einzelheiten damit tatsächliche Anpassungen erforderlich sind. Natürlich kommt es auf die genaue Anforderungen und betriebliche Analysen auf deren Einfluss auf die kurz- und langfristigen.

<a name="office-365-suite-level-settings"></a>Office 365-Suite Einstellungen auf Poolebene
-------------------------------

Office 365 ist viel mehr als nur SharePoint, wie Sie kennen. Finden Sie mehr zusätzliche Dienste die nicht auch der SharePoint-Architektur, wie Delve, Yammer und viele anstehende Dienste basieren. Dies bedeutet, dass die Enterprise branding und Konfiguration ist nicht praktisch steuern was wir in der SharePoint-Websites haben, vielmehr wir sollten werden Planen der allgemeinen Endbenutzer Erfahrung und wie wir stellen, dass die einheitliche Konfigurationen verschiedene Dienste schneidet.

Klassisches Beispiel für diesen Anforderungen Enterprise ist branding und dafür haben wir bereits Office 365 Designoberfläche eingeführt, die verwendet werden kann, um einige branding steuern. Wir haben auch andere in Kürze verfügbare Features, einschließlich der hilfreichen steuern die Steuerung Ihrer Website und andere Einstellungen, aus der zentralen Ort außerhalb der websitesammlungseinstellungen, wie das anstehende Compliance Center für Office 365, die derzeit in der [aufgeführt ist Wegweiser für Office 365](http://office.microsoft.com/en-us/products/office-365-roadmap-FX104343353.aspx).

Folgende Abbildung zeigt die unterschiedlichen Einstellungen jetzt für die Office 365-Designoberfläche, die dann firewallübergreifenden alle Office 365-Dienste angewendet wird.

![Zeigt die Office 365-Website mit der benutzerdefinierten Designs Registerkartenseite berechtigt Verwalten benutzerdefinierter Designs für Ihre Organisation, Anpassen von Office 365 zu einer Ihrer Organisation der Marke widerspiegeln. Einstellungen sind verfügbar für benutzerdefinierte-Logo-URL für eine Tabellentitel Logo, Hintergrundbild, Akzentfarbe, Navigation Leiste Hintergrundfarbe, Text-und Symbole und App-Menü Symbolfarbe.](media/Recipes/OD4BCustomization/O365-theme-settings.png)

Da standardmäßig Einstellungen für Office 365-Design für steuernde OD4B Website Suite Balken sind, werden in den meisten Fällen verwenden Sie diese Optionen zusammen mit anderen Optionen um sicherzustellen, dass Sie mindestens bereitstellen können, dass die richtigen Brandingelemente Ihre Websites OD4B schneidet. Beachten Sie, wenn Sie beispielsweise Office 365 Design für Office 365-Verwaltungstool ändern, es dauert, ziemlich sehr lange angewendeten für OD4B Websites, für die erste also Verständnis sein.

<a name="hidden-app-part-with-user-context"></a>Ausgeblendete app-Webpart mit Benutzerkontext
---------------------------------

Hierbei handelt es sich um einen Ansatz verwenden zentralisiert, in dem Zielseite als Speicherort für den benötigten Anpassungsprozess starten. Dies bedeutet, dass Sie an einem zentralen Ort wie Unternehmen Intranet Front-Seite haben, in dem der Benutzer immer beim Öffnen von ihrem Browser Zielseite werden müssten. Dies ist ziemlich typische Prozess mit mittelgroße und größere Unternehmen wobei corporate Zielseite dann mithilfe von Gruppenrichtlinien in den Active Directory gesteuert. Dadurch wird sichergestellt, dass Endbenutzer können Sie nicht die standardmäßige Willkommensseite der Domäne beitreten Browser Unternehmen überschreiben.

Wenn Benutzer mit dem Intranet eingeht, haben wir wird app-Webpart auf der Seite ausgeblendet die den Anpassungsprozess gestartet wird. Es können tatsächlich von der gesamten OD4B Site Creation auch zuständig sein, da normalerweise Benutzer die Website OD4B einmal besuchen müssten Zeit, bevor die websiteerkennungsprozess gestartet wird. Ausgeblendete app-Webpart ist tatsächlich eine Seite vom Anbieter gehosteten app in Azure gehostete hosten. Diese Seite ist dann starten Sie den Anpassungsprozess verantwortlich.

Lassen Sie uns näher auf der logische Entwurf dieses Ansatzes.

![Diagramm zum Anzeigen der Beziehungen. Das App-Webpart auf der SharePoint-Website verwendet instanziieren, um zur Provider-Hosted Apps zu wechseln. Provider-Hosted Apps wird die Nachricht hinzufügen So wechseln zur Speicherung Warteschlange verwendet. Speicher Warteschlange verwendet instanziieren, um zur WebJob zu wechseln. WebJob verwendet Änderungen übernehmen, fahren Sie mit der OD4B-Website.](media/Recipes/OD4BCustomization/hidden-app-part-logical-diagram.png)

1. Ort ausgeblendet app-Webparts zum zentralen Standort, auf dem Endbenutzer sorgt wird. In der Regel ist dies das Unternehmensintranet-Startseite.
2. App-Webpart eine Seite vom Anbieter gehosteten app, gehostet werden, wobei in den serverseitigen Code wir den Anpassungsprozess initiieren, indem Sie erforderlichen Metadaten der Azure-Speicher-Warteschlange hinzufügen. Dies bedeutet, dass diese Seite wird nur die Anpassung Anforderung empfangen, aber Änderungen die Verarbeitungszeit normalen beibehalten wird nicht tatsächlich angewendet.
3. Dies ist die Warteschlange tatsächlichen Azure-Speicher, die Nachrichten, die in die Warteschlange für die Verarbeitung empfangen. Auf diese Weise können wir die Anpassung Prozess asynchron steuern, sodass es wie lange Endbenutzer eigentlich keine Rolle spielt behandeln wird in der ersten Seite des Intranets bleiben. Wenn der Anpassungsprozess synchrone wäre, würden wir werden abhängig vom Endbenutzer im Browser in der Front-Seite im Intranet geöffnet lassen, bis die seitenausführung abgeschlossen ist. Dies nicht auf jeden Fall würde eine optimale und es Stand vor der Herausforderung, mit dem [ursprünglichen OD4B Anpassungsvorgang](http://blogs.msdn.com/b/vesku/archive/2013/11/25/office365-apply-automatically-custom-branding-to-personal-site-skydrive-pro.aspx), welche ich einem Blog beschrieben hat, während zurück.
4. WebJob verknüpft, um die Speicherwarteschlange führen die aufgerufen wird, wenn ein neues Element in die Speicherwarteschlange platziert wird. In diesem WebJob erhält die erforderlichen Parameter und Metadaten aus der Nachricht in der Warteschlange auf rechten Websitesammlung zugreifen. WebJob app nur token verwendet und haben die erforderlichen Berechtigungen zum Bearbeiten von Websitesammlungen in der Ebene der Mandant gewährt wurde.
5. Tatsächliche Anpassungen sind nacheinander angewendet, auf Websites für die Personen, die besuchen die Front-Intranet-Seite, um den zu starten.
Dies ist auf jeden Fall den zuverlässigste Prozess, um sicherzustellen, dass die richtige Konfigurationen auf den Websites OD4B vorhanden ist. Sie können auf einfache Weise Anpassung Versioning Logik, an den Prozess hinzufügen auch benötigte Updates auf den Websites OD4B anwenden ist, wenn eine Aktualisierung erforderlich ist und Benutzer Intranet-Startseite beim nächsten besucht. Diese Option erfordert jedoch, dass Sie diesen zentralen Speicherort verfügen, in dem die Endbenutzer Zielseite sind.

Wenn Sie der klassische Modelle der SharePoint-Entwicklung mit farmlösungen vertraut sind, ist dies als einmal ausführen von Zeitgeberaufträgen sehr ähnlich.

<a name="pre-create-and-apply-configuration"></a>Vor dem Erstellen und Anwenden von Konfiguration
----------------------------------

Diese Option basiert auf das vor dem Erstellen der OD4B Websites, bevor Benutzer darauf zugreift. Dies kann mithilfe von [relativ neue API](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.OneDriveProvisioning) die uns abwesend zum Erstellen von Websites für bestimmte Benutzer OD4B in Batch-Verarbeitung bietet mit CSOM oder REST erreicht werden. Erforderliche Code initiiert werden kann mithilfe eines PowerShell-Skripts oder vom tatsächlichen Code die remote-APIs aufrufen, ist.

![Ein Administrator verwendet, vor dem Erstellen und anpassen, um eine OD4B-Website zu erstellen.](media/Recipes/OD4BCustomization/pre-create-and-apply.png)

1. Administrator wird mithilfe die remote-Erstellung APIs OD4B Websites für Benutzer erstellen und die erforderlichen Anpassungen ist auf den Websites OD4B im Rahmen des Prozesses zum Skript anwenden.
2. Tatsächliche OD4B Websites sind auf der Office 365 für bestimmte Benutzer erstellt und deren Benutzerprofilen verknüpft

In gewisser Dies ist auch wirklich zuverlässigen Prozess, jedoch müssen Sie neue Personen und Updates "manuell", verwalten die kann mehr Arbeit, klicken Sie dann mithilfe der Methode *Ausgeblendete app-Webpart* bedeuten. Dies ist definitiv Ansatz ergriffen und insbesondere dann hilfreich sein kann, wenn Sie migrieren in eine andere Datei Freigabe Lösung für die OD4B und vermeiden Sie die Notwendigkeit der Endbenutzer Zugriff auf die OD4B Site einmal, vor dem Starten der aktuelle Werte Website erstellen möchten.

<a name="remote-timer-job-based-on-user-profile-updates"></a>Remote Zeitgeberauftrag basierend auf Profil benutzeraktualisierungen
----------------------------------------------

Dieser Ansatz bedeutet Durchsuchen von Benutzerprofilen für die Überprüfung, auf denen die OD4B-Website erstellt wurde, und dann die Änderungen auf die Websites anwenden, je nach Bedarf. Dies bedeutet, dass geplanter Auftrag ausgeführt außerhalb von SharePoint, in dem regelmäßig den Status überprüfen und führen Sie die Anpassungen erforderlich. Geplanter Auftrag konnte als eine WebJob in Azure ausgeführt wird oder so einfach wie das PowerShell-Skript in Ihre eigene Windows-Taskplaner geplant werden. Natürlich hat die Skala der Bereitstellung außerordentlich Einfluss auf der ausgewählten Option planen.

![Ein Remote-Zeitgeberauftrag verwendet wird, durchlaufen Websitesammlungen, zum Anpassen von jedem Standort.](media/Recipes/OD4BCustomization/remote-timer-job.png)

1. Geplante Aufgabe wird die zugreift Benutzerprofile der Benutzer für die Überprüfung, die OD4B-Website bereitgestellt wurde initiiert
2. Tatsächliche Websites sind benutzerdefinierte-nacheinander basierend auf den geschäftlichen Anforderungen

Eines der wichtigsten Nachteile der diese Option ist, dass es kann deutlich eine Situationen, in dem Benutzer die OD4B Websites zugreifen können, bevor die Anpassungen installiert worden sind. Diese Option ist gleichzeitig interessante Add-on für andere Optionen, um sicherzustellen, dass Endbenutzer beliebige der erforderlichen Einstellungen auf den Websites nicht geändert haben oder zu überprüfen, ob die Websiteinhalte OD4B mit den Unternehmensrichtlinien abschließt.

<a name="enhanced-app-part-based-customization"></a>Erweiterte app-Webpart-basierte Anpassung
-------------------------------------

Hier wurde detaillierte Beschreibung der erweiterten app Teil basierend Anpassungen, die scheint der typische Ansatz zum Anwenden und Verwalten von Anpassungen für die Websites OD4B benötigt werden. Quellcode und Weitere Informationen zu dieser Lösung wird von [Office 365 Developer Mustern und Methoden Anleitungen](http://aka.ms/officedevpnp)zur Verfügung.

Tatsächlicher logischer Entwurf entspricht den ausgeblendeten app Teil Ansatz, in [diesem Blogbeitrag](http://blogs.msdn.com/b/vesku/archive/2013/11/25/office365-apply-automatically-custom-branding-to-personal-site-skydrive-pro.aspx)erwähnt. Dies bedeutet, dass wird davon ausgegangen, dass Sie haben Intranet in der Office 365-Umgebung, in dem Sie das erforderlichen app-Webpart einfügen können, zentral und die Endbenutzer auf dieser Seite Willkommen Zielseite werden wird, wenn sie von ihrem Browser öffnen. Es ist üblich, dass jedes Unternehmen Browser dieselbe Homepage mithilfe von Gruppenrichtlinien, so festgelegt hat, dass Endbenutzer immer von einem zentralen Standort gestartet wird, wenn sie von ihrem Browser öffnen. Dies ist der Speicherort, wo Sie app-Webparts platziert würde die festgelegt werden kann, um als 0 Pixelbreite und Höhe vergrößert oder verkleinert werden. Hier ist, dass Sie den Endbenutzer-Kontext verwenden, um das app-Webpart, führen Sie, das Seite vom Anbieter gehosteten-add-in enthält.

**Leistungsaspekte Optimierung und Wartung**

Da diese app-Webpart ausgeführt wird jedes Mal Benutzer Front-Seite des Intranets kommt, müssen wir berücksichtigen der Leistung durch this oder wie Sie den Code effizient arbeiten, und führen Sie nur die wichtigsten Punkte der Code Ausführungen, wenn Sie tatsächlich benötigt. Zweite Optimierung Überlegung ist auch, in dem wir tatsächliche Objekte, die verwendet werden, in den einzelnen Websites platzieren. Dies sind ziemlich typische Herausforderungen zur Lösung mit Anpassungen. Es folgt kleine Gruppe von Aspekte, die in der app-Modell Implementierungen konzentrieren.

- Speicherort der Anlagen – zentralisierte Content Delivery Network (CDN)-Lösung in jeder Websitesammlung oder in Stammwebsitesammlung?
- Aktualisieren Sie die Anzahl der Objekte oder wie Sie sicherstellen, dass unabhängig davon clientseitige Browser Zwischenspeichern wir sicherstellen können, dass wir führen Sie die aktuelle Versionen von Skripts (JavaScript) oder die aktuellen Versionen der Bilder anzeigen?
- Eingeschränkter Ausführung des Codes zu vermeiden Sie unnötige Belastung für Azure und Office 365-Dienst
- Version Anpassungen, die auf OD4B Website angewendet werden

**Speicherort der Anlagen**

Es gibt einige andere Lösungen für diese. Im Code Verweis Beispiel verwenden wir JavaScript in den einzelnen die OD4B Einbetten von Websites zum Bereitstellen des Unternehmens Richtlinie Nachricht und entfernen Sie die Möglichkeit zum Erstellen von Sub Websites werden sollen (oder blenden Sie die Verknüpfung). In dieser bestimmten Lösung werden wir die erforderliche JavaScript-Datei hochladen, Stammwebsitesammlung der OneDrive for Business-Adressschema und wir diese Datei direkt aus dieser Position in den einzelnen Standorten OD4B verweisen. Dies bedeutet, dass Sie nur zentral verwalten und Aktualisieren der JavaScript-Datei verfügen, wenn keine Änderungen erforderlich sind.

In dieser referenzimplementierung wir tatsächlich auch aktualisieren diese Datei jedes Mal die WebJob ausgeführt wird, das ist sicherlich nicht erforderlich, aber Beispielcode werden einfach ohne zusätzlichen Schritte Arbeitszeiten und mögliche vorgesehen war. Ebenso konnten Sie die JavaScript-Datei manuell um root-Websitesammlung und verweisen, die dann von dort hochladen. Alternative Lösung wäre auch einige CND verwenden, um die benötigte Datei speichern oder JavaScript von der vom Anbieter gehosteten app-Seite darauf verweisen. Solange Sie nur eine Kopie der Datei haben, müssen Sie

![Jede OneDrive for Business-Website ist eine eigene Websitesammlung unter der verwaltete Pfad der persönlichen und jede Url wird basierend auf dem Benutzerprofil erstellt. Wenn Contoso-my.sharepoint.com der Hauptwebsite ist, werden Johns Website beispielsweise contoso-my.sharepoint.com/personal/john_contoso_com.](media/Recipes/OD4BCustomization/asset-locations.png)

**Client-seitigen caching Herausforderung und, die Lösung**

Zu den Aufgaben mit JavaScript-basiertes Implementierung ist Clientseite Zwischenspeichern. Wenn Browsern verwendete JavaScript-Dateien herunterladen, werden sie diese Dateien zur Reduzierung des heruntergeladenen Elemente für die folgenden Anforderungen zwischengespeichert. Dies ist hervorragend Hinblick auf die Leistung zu optimieren, aber bewirkt, dass eine Herausforderung Wenn wir die JavaScript-Datei aktualisieren müssen. Im schlimmsten Fall kann zwischengespeicherten JavaScript-Datei Ausnahmen mit anderen Updates aktualisierte Versionen eingeführt.

Um dieses Problem zu entfernen, können wir die JavaScript-URL-Verweis Revisionsattribut mit starten. Wenn wir benutzerdefinierten Aktion des Benutzers zu der Website OD4B zuordnen, schließen wir Sie die URL der JavaScript-eindeutige GUID in der URL haben. Hier ist Beispiel für die Referenz für die auf der Stammwebsite der Websitesammlung zeigen wird. Beachten Sie die zusätzliche GUID, die nach dem Rev-Attribut in der URL hinzugefügt wurde. Jedes Mal, wenn die Anpassung ausgeführt wird, für bestimmte OD4B Site wird dieses Attribut Update sein. In der Praxis bedeutet dies, dass die JavaScript-Datei an Browser zwischengespeichert wird, bis es eine neue Version OD4B-Website, die die URL zu ändern ist, wird hinzugefügt und daher Browser wird die neue Version herunterladen und zwischenspeichern, die nach der nächsten Aktualisierung.

- /OneDriveCustomization/OneDriveConfiguration.js?Rev=4bb89029e7ba470e893170d4cba7de00

Es folgt der Code die zum Generieren der JavaScript-URL für die benutzerdefinierte Aktion des Benutzers verwendet wird.
    
    /// <summary>
    /// Just to build the JS path which can be then pointed to the OneDrive site.
    /// </summary>
    /// <returns></returns>
    public string BuildJavaScriptUrl(string siteUrl)
    {
        // Solve root site collection URL
        Uri url = new Uri(siteUrl);
        string scenarioUrl = String.Format("{0}://{1}:{2}/{3}", 
                               url.Scheme, url.DnsSafeHost, 
                               url.Port, JSLocationFolderName);
       // Unique rev generated each time JS is added, so that we force browsers to 
       // refresh JS file wiht latest version
       string revision = Guid.NewGuid().ToString().Replace("-", "");
       return string.Format("{0}/{1}?rev={2}", scenarioUrl, JSFileName, revision);
    }

**Eingeschränkter Ausführung von code**

Da dieser Prozess basiert auf mit dem app-Webpart auf der ersten Seite des Intranets ausgeblendet, wird dies bedeutet, dass der Code ausgeführt wird jedes Mal Benutzer ihre aktualisieren oder wechseln sie zur Seite. Da diese Front-Seite als Standard-Browser-Startseite für die Benutzer häufig festgelegt ist, würde Code jedes Mal ausgeführt werden, wenn eine Browser-Sitzung gestartet wird.

Da wir jedoch nicht aktualisieren aktualisiert die Anpassungen, die an die OD4B Websites angewendet werden, dass häufig, es ist wirklich zu keiner Zeit wird die gesamte Anpassung muss im ersten. Auf diese Weise reduziert wir die Verwendung der Warteschlangen Speicher und die Ausführung der Web-Auftrag, die direkt senken die Kosten auf der Seite vom Anbieter gehosteten app, da wir in unseren Design nicht als viel CPU und andere Ressourcen verwenden werden.

Um sicherzustellen, dass unsere Verarbeitung nicht bei jeder Anforderung erfolgt einfachsten klassische Browser Cookie Ansatz verwendet, in dem wir bestimmtes Clientbrowser mit bestimmten Lebensdauer-Cookie gespeichert werden. Mobilgeräts auf dieses Cookie vorhanden ist, können wir die Ausführung überspringen, bis das Cookie abgelaufen wurde und wann wir den tatsächlichen anpassungsstatus auf den Websites OD4B überprüfen.

Hier ist, was wir in die Seite Load-Methode für das app-Webpart haben. Dieser Methodenaufruf Vorhandensein des Cookies überprüft, und das Cookie vorhanden ist, können wir den Code für die tatsächliche wird übersprungen, bis Ausführung erneut benötigt wird.

    // Check if we should skip this check. We do this only once per hour to avoid 
    // perf issues and there's really no point even hitting the user profile 
    // in every request.
    if (CookieCheckSkip())
        return;

Tatsächliche Cookiestatus und Einstellung des Cookies wie folgt durchgeführt.

    /// <summary>
    /// Checks if we need to execute the code customization code again. 
    /// Timer set to 60 minutes to avoid constant execution of the code for nothing.
    /// </summary>
    /// <returns></returns>
    private bool CookieCheckSkip()
    {
        // Get cookie from the current request.
        HttpCookie cookie = Request.Cookies.Get("OneDriveCustomizerCheck");
    
       // Check if cookie exists in the current request.
       if (cookie == null)
       {
           // Create cookie.
           cookie = new HttpCookie("OneDriveCustomizerCheck");
           // Set value of cookie to current date time.
           cookie.Value = DateTime.Now.ToString();
           // Set cookie to expire in 60 minutes.
           cookie.Expires = DateTime.Now.AddMinutes(60);
           // Insert the cookie in the current HttpResponse.
           Response.Cookies.Add(cookie);
           // Output debugging information
           WriteDebugInformationIfNeeded(
               string.Format(@"Cookie did not exist, adding new cookie with {0} 
                               as expiration. Execute code.",
                               cookie.Expires));
           // Since cookie did not existed, let's execute the code, 
           // so skip is false.
           return false;
       }
       else
       {
           // Output debugging information
           WriteDebugInformationIfNeeded(string.Format(@"Cookie did existed, 
                                       with {0} as expiration. Skipping code.", 
                                       cookie.Expires));
           //  Since cookie did existed, let's skip the code
           return true;
       }
    }

Wenn Sie für den Code im app-Webpart-Seite näher haben, sehen Sie, die in jedem Aufruf, dass wir die Existences der OD4B-Website für die Endbenutzer aktivieren. Da nur Dies kann durch Zugreifen auf Benutzerprofildienst, wird Code auf die Leistung auswirken. Mithilfe das oben genannten Cookie Kontrollkästchen können wir die Endbenutzer auftreten besser machen, und wir vermeiden Drücken des Benutzerprofildiensts ständig ohne die tatsächlichen Anforderungen. Es ist außerdem ratsam, beachten Sie, dass wir diese Überprüfung Cookie als ersten Schritt in der *Page_Load* -Methode gesetzt haben, sodass wir alle Verarbeitung überspringen, falls erforderlich. Hier ist ein kurzer Ausschnitt aus der *Page_Load* -Methode aus der *Customizer.aspx* an den Prozess Code anzeigen. 

    protected void Page_Load(object sender, EventArgs e)
    {
        // Check if we should skip this check. We do this only once per hour to avoid 
        // perf issues and there's really no point even hitting the user profile 
        // in every request.
        if (CookieCheckSkip())
            return;
     
        var spContext = 
           SharePointContextProvider.Current.GetSharePointContext(Context);
       using (ClientContext clientContext = 
           spContext.CreateUserClientContextForSPHost())
       {
           // Get user profile
           ProfileLoader loader = ProfileLoader.GetProfileLoader(clientContext);
           UserProfile profile = loader.GetUserProfile();
           Microsoft.SharePoint.Client.Site personalSite = profile.PersonalSite;
    
           clientContext.Load(profile, prof => prof.AccountName);
           clientContext.Load(personalSite);
           clientContext.ExecuteQuery();
    
           // Let's check if the site already exists
           if (personalSite.ServerObjectIsNull.Value)
           {

**Version Anpassungen, die auf OD4B Website angewendet werden**

Zweite Ebene der Optimierung auf unsere Code Verarbeitung durch versionsverwaltung insbesondere die Anpassungen erfolgt die wir die OD4B Websites bereitstellen. Dies bedeutet, dass wir die Version der Anpassungen der OD4B Website-Eigenschaftensammlung zu speichern und Dateien und Elemente nur aktualisiert, falls erforderlich. Dies bedeutet, dass bei der Ausführung WebJob wir vergleichen die derzeit Anpassung Version in OD4B auf die Version, die wir kurz vor dem Bereitstellen und nur, wenn die Anpassung Version Odes nicht auf der Website OD4B vorhanden sind, wir die erforderlichen Anlagen hochladen und andere Einstellungen anwenden.

Dieser Ansatz auch reduziert die benötigten Ressourcen aus Microsoft Azure, da es vermeiden, aktualisieren oder tatsächlichen Anpassungscode ausgeführt, wenn er nicht benötigt wird. Dies bedeutet Verringerung der auf die CPU und andere Ressource: Einsatz in der Microsoft Azure und weniger Anfragen zu Office 365.

Gesamte Logik für die Anpassung wird gespeichert, in diesem Beispiel befindet sich im *ApplySiteConfiguration* -Methode am *OD4B.Configuration.Async.Common.SiteModificationManager* -Klasse. Diese Methode wird auch von der WebJob mit den richtigen Parametern zum Starten des Anpassungsprozesses aufgerufen. Bevor wir tatsächlich alle Vorgänge ausführen, wird überprüft, dass Eigenschaftensammlung Eigenschaftswert mit einem Schlüssel von 'Contoso_OneDriveVersion' und die Ausführung bei aktuelle Version auf der Website niedriger als die Version die wir planen ist, gelten nur fortgesetzt.  Es folgt der tatsächliche Code, der [Plug & Play-Kernkomponenten von Office](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core) verwendet, um den Code zu vereinfachen.

    // Check current site configuration status - is it already in right version?
    if (ctx.Web.GetPropertyBagValueInt(
        SiteModificationManager.OneDriveMarkerBagID, 0) 
        < SiteModificationManager.BrandingVersion)
    {

Bei der Anpassung der Website angewendet wird, werden wir die angewendete Anpassung Version der Eigenschaftensammlung für die folgenden Ausführung festgelegt.

    // Save current branding applied indicator to site
    ctx.Web.SetPropertyBagValue(SiteModificationManager.OneDriveMarkerBagID, SiteModificationManager.BrandingVersion);

Dies ist relativ einfach, aber reduziert die erforderlichen Ressourcen von Azure und reduziert auch Unnecesasrey remote Vorgänge zu Office 365, die positiv auf die Leistung auswirken.

<a name="needed-configuration-in-azure"></a>Erforderliche Konfiguration in Azure
-----------------------------

Wichtige Voraussetzung für dieses Beispiel einwandfrei funktioniert besteht darin, dass Sie Azure Speicherdienst Daten erstellt haben und Verbindungszeichenfolgen Speicher wurden aktualisiert entsprechend für die Projekte, die verwenden werden. Sie können einfach als Speicherdienst aus dem Azure-Verwaltungsportal (manage.windowssazure.com), erstellen, indem Sie auswählen **neu hat Data Services hat Speicher hat Schnelles Erstellen**. Danach müssen Sie werden nur Name, Position und einige andere Einstellungen zu definieren, und Sie werden an.

![Die Einstellungen für schnelles erstellen: das URL-Feld auf Myveryownstorage festgelegt ist, Gruppe Standort-Affinität auf West US festgelegt ist, Abonnement auf MSDN Ultimate festgelegt ist und Replikation auf Georedundantes festgelegt ist.](media/Recipes/OD4BCustomization/azure-config-1.png)

Wenn Speicher erstellt wurde, müssen Sie wechseln und kopieren Sie den Schlüssel für die Verbindungszeichenfolge. Wenn Sie auf der Detailseite Speicher verschieben, können Sie wichtige Informationen zugreifen, indem Sie auf "*Zugriffstasten verwalten*" vom unteren Rand der Seite.

![Den Link zur Zugriffstasten verwalten wird am unteren Rand der Seite hervorgehoben.](media/Recipes/OD4BCustomization/azure-config-2.png)

Sie müssen so aktualisieren Sie App.config-Datei für die folgenden Projekte in Visual Studio-Projektmappe. Jedes der Projekte werden detaillierte weiter unten in diesem Blogbeitrag erläutert.

OD4B. Configuration.Async.WebJob OD4B. Configuration.Async.Console.SendMessage WebJob Projekt zwei Schlüssel, die aktualisiert werden können, so zeigen Sie auf die gleiche Verbindung und SendMessage hat nur einen Schlüssel aktualisieren.

![Die Datei ' App.config ' ist das AppSettings-Element in Visual Studio geöffnet. Zwei untergeordnete Elemente mit dem Namen hinzufügen werden unter dem AppSettings-Element aufgelistet. Für das erste hinzufügen-Element, das Attributschlüssel ClientId und den Wert = Attribut ist ein Paar von doppelten Anführungszeichen gleich. Für das zweite hinzufügen-Element, das Attribut Key = ClientSecret und den Wert Attribut ist auch ein Paar von doppelten Anführungszeichen gleich.](media/Recipes/OD4BCustomization/app-config.png)

<a name="reference-solution-structure"></a>Verweis Lösungsstruktur
----------------------------

In Visual Studio Lösung besteht aus den von ein paar Lösungen, aber jede von ihnen ziemlich angemessene Grund haben, vorhanden sein. Einführung in die drei Projekte in der Lösung und warum sie vorhanden sind oder was für sind ist hier.

![Klicken Sie im Projektmappen-Explorer zeigt einen Ordner namens Dokumentation, gefolgt von sechs Projekte, die im folgenden ausführlich beschrieben werden.](media/Recipes/OD4BCustomization/solution-explorer.png)

**OD4B.Configuration.Async**

Dies ist das Projekt aktuelle SharePoint-app, die lernen der vom Anbieter gehosteten app für SharePoint und fragt die benötigten Berechtigungen. Beachten Sie, dass, obwohl es nicht tatsächlich durchführen Mandanten, die von der app Vorgänge auf der Anwendungsebene es selbst, Teil sehr hohe Berechtigungen für das Add-in wird gefragt. Dies ist, da wir den gleichen Client-ID und den Schlüssel aus dieser Datei app unsere WebJob Ausführung verwendet wird. Mit diesem Ansatz, Sie müssen nicht manuell registrieren von app-Id und geheimen zum SharePoint, wir lieber verwenden die gleichen-ID und geheimen Cross-Lösung.

![Die Liste der Berechtigungen: der Bereich Mandanten hat die Berechtigung Vollzugriff. Der Bereich von Benutzerprofilen (Nutzung von sozialen Netzwerken) verfügt über die Berechtigung Vollzugriff. Das Kontrollkästchen der app erlauben, app-only-Aufrufe bei SharePoint zu machen ist aktiviert.](media/Recipes/OD4BCustomization/app-permissions.png)

Dieses Projekt enthält auch die Definition der app-Webpart, klicken Sie dann mit der Hostwebsite bereitgestellt werden soll.

**OD4B.Configuration.Async.Common**

Dieses Projekt enthält die tatsächlichen Geschäftslogik und freigegebenen Code schneidet Projekte, wie die Definition für das Datenobjekt die an die Speicherwarteschlange und die tatsächlichen Geschäftslogik zum Anpassen von Websites OD4B platziert wird. Hier Code versehen ist einfach bei Angabe einfacher entwickeln und testen die Vorgänge aus, wenn das Projekt erstellt wird. Wie mit allgemeine Entwicklung, setzen Sie kein wirklich Ihr Code für die Geschäftslogik direkt an die WebJob oder app-Part sollten, vielmehr zu suchen, die in Geschäftslogik Layer zum leichteren testen und Code wiederverwenden.

Die tatsächlichen Operationen in Richtung der OD4B Websites befinden sich in *OD4B.Configuration.Async.Common.SiteModificationManager* -Klasse.

**OD4B. Configuration.Async.Console.Reset**

Dieses Projekt ist unsere Test und debugging Projekt für die tatsächlichen Anpassungen. Hiermit können Sie die gewünschten Anpassungen manuell zu einer beliebigen OD4B Website anwenden. Dieses Projekt wurde während der Entwicklungszeit unsere Tests Project den Anpassungsprozess testen, bevor sie mit der WebJob verknüpft wurde. Projekt kann auch zurücksetzen Anpassungen aus einer beliebigen Website OD4B für Demo oder zu Testzwecken verwendet werden. Da tatsächlichen Geschäftslogik in das Projekt common befindet, wird dieses Projekt mithilfe der gleiche *SiteModificationManager* Klasse wie die anderen anwenden oder Zurücksetzen von Anpassungen von den Websites.

Wenn Sie die Anpassungen testen, können Sie den Code in der Main-Methode zwischen übernehmen und zurücksetzen, um die gewünschte Operation geändert einfach ändern.

    static void Main(string[] args)
    {
     
        Uri url = 
            new Uri("https://vesaj-my.sharepoint.com/personal/vesaj_veskuonline_com");
     
            //get the new site collection
        string realm = TokenHelper.GetRealmFromTargetUrl(url);
        var token = TokenHelper.GetAppOnlyAccessToken(
                       TokenHelper.SharePointPrincipal, 
                       url.Authority, realm).AccessToken;
       using (var ctx = 
           TokenHelper.GetClientContextWithAccessToken(url.ToString(), 
           token))
       {
           // Uncomment the one you need for testing/reset
           // Apply(ctx, url);
           Reset(ctx);
       }
    }

Beachten Sie, die Sie benötigen, um sicherzustellen, dass die app-Id und geheimen Schlüssel für dieses Projekt in app.config derjenigen, die entsprechende sind eingegebene benötigt Berechtigungen Ihrem Mandanten. Können Sie das Projekt auf einfache Weise ausführen, indem Sie rechts auf das Projekt, und auswählen **Debug – neue Instanz starten**, damit Sie den tatsächlichen Code durchlaufen können also zeilenweise ausgeführt.

**OD4B. Configuration.Async.Console.SendMessage**

Dieses Projekt wurde hinzugefügt, um die Lösung für die Speicherung Warteschlangenmechanismus testen, bevor es auf das app-Webpart verknüpft wurde. Projekt kann durch übergeben den app-Teil-Prozess für das Hinzufügen von neuer Nachrichten an die Speicherwarteschlange verwendet werden. Beachten Sie, dass Sie die Verbindungszeichenfolge für die Speicherung Warteschlange entsprechend aktualisieren müssen in app.config, stellen Sie das Projekt ordnungsgemäß funktioniert.

Können Sie das Projekt auf einfache Weise ausführen, indem Sie rechts auf das Projekt, und auswählen Debug – neue Instanz starten, damit Sie den tatsächlichen Code durchlaufen können also zeilenweise ausgeführt.

**OD4B. Configuration.Async.WebJob**

Dies ist das tatsächliche WebJob-Projekt, die mit WebJob-Projektvorlage in Visual Studio 2013 Update 4 eingeführt erstellt wurde. Diese Vorlage vereinfacht die WebJob Projekte zu erstellen, indem Sie rechts Verweise vorhanden und bietet auch noch etwas Bereitstellung Automatisierung mit Rechte Unterstützung für das Projekt. Sie können einfach ursprüngliche Version oder eine neue Version des Projekts in der Azure bereitstellen, indem Sie rechts auf und veröffentlichen als Azure Webauftrag auswählen... die oben im Veröffentlichen-Assistent geöffnet wird.

![Das Dialogfeld "Web veröffentlichen" wird angezeigt, und zeigt die Registerkarte Verbindung. Im Feld Server den Wert Vesaj-od4bconf.scm.azurewebsites.net:443 enthält, das Namensfeld Website enthält den Wert Vesaj-0d4bconf, im Feld Benutzername geschwärzten ist, wird das Feld Kennwort maskiert, das Kontrollkästchen Kennwort speichern aktiviert ist, und die Ziel-URL Feld enthält den Wert http://vesaj-od4bconf.azurewebsites.net.](media/Recipes/OD4BCustomization/publish-to-azure.png)

Dieser WebJob wird als einer continuous WebJob, erstellt für die Verarbeitung der Warteschlange basiert. Dies bedeutet, dass in der Main-Methode, wir nur den Prozess ausgeführt werden wie folgt kontinuierliche festgelegt.

    class Program
    {
        // Please set the following connection strings in app.config for this 
        // WebJob to run: AzureWebJobsDashboard and AzureWebJobsStorage
        static void Main()
        {
            var host = new JobHost();
            // The following code ensures that the WebJob will be 
            // running continuously
           host.RunAndBlock();
       }
    }

Tatsächliche warteschlangenverarbeitung ist wirklich einfach mit WebJobs. Lediglich die müssen wir besteht darin, die richtigen Attribute für die Methode festzulegen und um sicherzustellen, dass die Verbindungszeichenfolgen von Azure-Speicher in der app-Konfiguration entsprechend aktualisiert werden und Vergleich der Speicherwarteschlange in Microsoft Azure erstellt haben. Es folgt die *ProcessQueueMessage* -Methode aus der functions.cs-Klasse. Beachten Sie, wie wir das App nur token Objektmodell verwenden, um Zugriff auf die SharePoint aus der WebJob. Damit dies funktioniert, müssen Sie sicherstellen, dass Sie die richtigen app-Id und geheimen Clientschlüssel in app.config des Projekts kopiert haben. Tatsächliche Geschäftslogik befindet sich die *SiteModificationManager* -Klasse, sodass wir gerade, die mit dem richtigen Client Kontext- und Parameter aufrufen.

    // This function will get triggered/executed when a new message is written 
    // on an Azure Queue called queue.
    public static void ProcessQueueMessage(
        [QueueTrigger(SiteModificationManager.StorageQueueName)] 
        SiteModificationData request, TextWriter log)
    {
        Uri url = new Uri(request.SiteUrl);
     
        //Connect to the OD4B site sing App Only access
       string realm = TokenHelper.GetRealmFromTargetUrl(url);
       var token = TokenHelper.GetAppOnlyAccessToken(
           TokenHelper.SharePointPrincipal, url.Authority, realm).AccessToken;
    
       using (var ctx = TokenHelper.GetClientContextWithAccessToken(
           url.ToString(), token))
       {
           // Set configuration object properly for setting the config
           SiteModificationConfig config = new SiteModificationConfig()
           {
               SiteUrl = url.ToString(),
               JSFile = Path.Combine(Environment.GetEnvironmentVariable
                   ("WEBROOT_PATH"), "Resources\\OneDriveConfiguration.js"),
               ThemeName = "Garage",
               ThemeColorFile = Path.Combine(Environment.GetEnvironmentVariable
                   ("WEBROOT_PATH"), "Resources\\Themes\\Garage\\garagewhite.spcolor"),
               ThemeBGFile = Path.Combine(Environment.GetEnvironmentVariable
                   ("WEBROOT_PATH"), "Resources\\Themes\\Garage\\garagebg.jpg"),
               ThemeFontFile = "" // Ignored in this case, but could be also obviously set
           };
    
           new SiteModificationManager().ApplySiteConfiguration(ctx, config);
       }
    }

Andere wichtiger ist, dass Sie benötigen, um sicherzustellen, dass Sie die *Lokale Kopie* -Eigenschaft für die SharePoint-CSOM-Assembly Verweise-Eigenschaft für das Projekt festgelegt haben, damit alle abhängigen Assemblys in Azure ordnungsgemäß kopiert werden, wenn Sie den Webauftrag bereitstellen . Hierbei handelt es sich einfach, da diese Assemblys standardmäßig nicht im normalen Azure-Website enthalten sind, also durch Festlegen dieser Eigenschaft *True*, Sie stellt sicher, dass Assemblys, auf die verwiesen wird, um auch cloud kopiert werden.

**OD4B. Configuration.AsyncWeb**

Dies ist die tatsächliche vom Anbieter gehosteten app, die in Microsoft Azure gehostet wird. Sie enthält die Seite laded mit dem app-Webpart, die auf der ersten Seite des Intranets platziert wird. Seite "default.aspx" dieser App nicht tatsächlich alle Vorgänge enthält, zeigt Details zum Verwenden der app bereitstellt.

*Beachten Sie die. Wenn Sie Probleme mit der WebJob wurde verweigert konfrontiert oder app im Allgemeinen nur zugreifen werden, stellen Sie sicher, dass Sie die app-Client-Id und geheimen Schlüssel in app.config entsprechend die Werten in der Datei web.config aus diesem Projekt aktualisiert haben. Visual Studio kann diese Werte in bestimmten Szenarien ändern.* 

<a name="queue-processing-in-webjob"></a>Verarbeitung in WebJob Warteschlange
--------------------------

Mithilfe der Warteschlangen Speicher ist wirklich einfach mit den APIs von Azure zur Verfügung. Einfachste Einstieg ist das "*Windows Azure Storage*" Nuget-Paket, mit das alle erforderlichen APIs und andere Pakete dem Projekt zuordnen möchten. Nachdem Sie diese Nuget-Paket hinzugefügt haben, können Sie einfach starten, verwenden die Speicherwarteschlange APIs für die Verarbeitung. Es folgt Ausschnitt aus der *OD4B. Configuration.Async.Common* Project (AddConfigRequestToQueue-Methode in SiteModificationManager-Klasse), der Code zum Behandeln von tatsächlichen Warteschlange Nachricht enthält und zahlreiche Projekte (bereitgestellten einfacher Entwicklung Time-Debuggen) verwendet wird.

    public void AddConfigRequestToQueue(
                string account, string siteUrl, string storageConnectionString)
    {
        CloudStorageAccount storageAccount = 
                            CloudStorageAccount.Parse(storageConnectionString);
     
        // Get queue... create if does not exist.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        CloudQueue queue = 
           queueClient.GetQueueReference(SiteModificationManager.StorageQueueName);
       queue.CreateIfNotExists();
    
       // Pass in data for modification
       var newSiteConfigRequest = new SiteModificationData()
       {
           AccountId = account,
           SiteUrl = siteUrl
       };
    
       // Add entry to queue
       queue.AddMessage(
           new CloudQueueMessage(
               JsonConvert.SerializeObject(newSiteConfigRequest)));
    }

Tatsächliche Warteschlange in diesem Fall Verarbeitung erfolgte, mit dem WebJob-Projekt. Im Fall von WebJob können wir einfach bestimmte Attribute verwenden, um die Warteschlange Handhabung automatisieren. Nur ist wir brauchen, um sicherzustellen, dass wir gleichen Speicher Zeichenfolge und Warteschlange Verbindungsnamen in senden und Empfangen von Webpart verwenden.

    // This function will get triggered/executed when a new message is written 
    // on an Azure Queue called queue.
    public static void ProcessQueueMessage(
        [QueueTrigger(SiteModificationManager.StorageQueueName)] 
        SiteModificationData request, TextWriter log)
    {
        Uri url = new Uri(request.SiteUrl);

Es ist wirklich nicht einfacher, als dies abgerufen werden. Beachten Sie, dass wir *SiteModificationManager.StorageQueueName* auf beiden Seiten verwenden, um sicherzustellen, dass die Warteschlange Namensvergleich.

**Tatsächliche Konfigurationen auf der Website anwenden**

In dieser Referenz Implementierungen sind wir folgende Anpassungen für jede der OD4B Sites ausführen.

- Fügen Sie Unternehmen Richtlinie Nachricht der immer, auf den Websites OD4B angezeigt wird hinzu
- Ausblenden Sub-Website die Verknüpfungsoption aus Inhaltsseite Website erstellen
- Anwenden von benutzerdefinierten Designs für die Website OD4B Unternehmen branding entsprechen

Unternehmensrichtlinie und Ausblenden der Link erstellen Sub-Website sind erreicht wird mit so JavaScript Einbetten von Muster genannt, in dem wir hinzufügen benutzerdefinierten Benutzeraktion auf der Websiteebene bei bestimmten JavaScript-Datei, klicken Sie dann in jede Anforderung einer Seite ausgeführt wird. Dies bedeutet, dass wir die Seite Verarbeitung von Client-Side-Technologien durch Hinzufügen, entfernen oder aktualisieren ein Element in einer beliebigen Seite steuern können. Mit diesem Ansatz wir keine einführen eine benutzerdefinierte Gestaltungsvorlage müssen, die uns wichtiger langfristig Wartungskosten, könnte insbesondere dann, wenn die erforderlichen Änderungen minimal sind.

Zweiter Vorgang mit der benutzerdefinierten Designs erfordern, dass wir einige zusätzlichen Dateien auf der Website hochladen, und legen Sie dann die als Design Einstellungen verwendet werden soll. Streng verwenden wir CSOM, um alle erforderlichen Dateien in die Websites, um zu vermeiden alle zukünftigen mit Feature Framework-Element Zuordnungen hoch. Da Hochladen einer Datei auf die Verwendung des CSOM SharePoint ganz einfach ist, dies auf jeden Fall die einfachste Möglichkeit zum Ausführen der Automatisierungs ist und nicht erforderlich, damit alle XML-spezifischen Konfigurationen Abhängigkeit zu sandkastenlösungen sorgen. Hier wird die aktuelle Website Konfigurationsmethode von OD4B.Configuration.Async.Common.SiteModificationManager-Klasse. Beachten Sie, dass wir Office 365 Developer Plug & Play-Hauptkomponenten verwenden, um einige der erforderlichen Vorgänge zu vereinfachen.

Es ist außerdem ratsam, beachten Sie, dass wir neue Version des der JS tatsächlich Stammwebsitesammlung jedes hochladen wir Anpassung persönliche OD4B Website Zeit. Dies ist definitiv keine optimale Lösung, sondern vielmehr es Zwecken Einfachheit für diese Lösung Verweis. Sie konnte sollten Sie JavaScript-Datei hochladen Operation app Installed-Ereignis, hinzufügen, damit es nur einmal ausgeführt wird, wenn die app installiert ist, aber in diesem Fall müssen Sie einige zusätzliche Arbeiten mit Updates für diese JS-Datei.

    // This function will get triggered/executed when a new message is written 
    // on an Azure Queue called queue.
    public static void ProcessQueueMessage(
        [QueueTrigger(SiteModificationManager.StorageQueueName)] 
        SiteModificationData request, TextWriter log)
    {
        Uri url = new Uri(request.SiteUrl);
     
        //Connect to the OD4B site using App Only token
       string realm = TokenHelper.GetRealmFromTargetUrl(url);
       var token = TokenHelper.GetAppOnlyAccessToken(
           TokenHelper.SharePointPrincipal, url.Authority, realm).AccessToken;
    
       using (var ctx = TokenHelper.GetClientContextWithAccessToken(
           url.ToString(), token))
       {
           // Set configuration object properly for setting the config
           SiteModificationConfig config = new SiteModificationConfig()
           {
               SiteUrl = url.ToString(),
               JSFile = Path.Combine(Environment.GetEnvironmentVariable
                   ("WEBROOT_PATH"), "Resources\\OneDriveConfiguration.js"),
               ThemeName = "Garage",
               ThemeColorFile = 
                   Path.Combine(Environment.GetEnvironmentVariable
                   ("WEBROOT_PATH"), "Resources\\Themes\\Garage\\garagewhite.spcolor"),
               ThemeBGFile = 
                   Path.Combine(Environment.GetEnvironmentVariable
                   ("WEBROOT_PATH"), "Resources\\Themes\\Garage\\garagebg.jpg"),
               ThemeFontFile = "" // Ignored in this case, but could be also set
           };
    
           new SiteModificationManager().ApplySiteConfiguration(ctx, config);
       }
    }

Offensichtlich sind die erforderlichen Vorgänge hochgradig abhängig von Ihren geschäftlichen Anforderungen. Sie können mehrere unterschiedliche Muster suchen und Ansätze mit CSOM-basierte Vorgänge aus dem [Office 365 Developer Mustern und Methoden](http://aka.ms/officedevpnp).

<a name="additional-notes-on-webjob-based-solutions"></a>Zusätzliche Hinweise auf WebJob-basierte Lösungen
==========================================

Nachfolgend finden Sie einige zusätzliche Hinweise zur WebJob-Entwicklung in Azure im Zusammenhang. Dies ist äußerst Verfahren, die überwiegend definitiv cross-Anpassungen der Office 365 verwendet werden soll. Sicherlich sehen Sie die neue und verbesserte Lösungen auf Grundlage der WebJob Technologie der Office 365 Developer Patterns & Practices Programm sowie hinzugefügt werden.

<a name="debugging-webjob-and-customization-process"></a>Debugvorgang WebJob und Anpassung
------------------------------------------

Die folgende Vorgehensweisen für Code im Allgemeinen ist die tatsächlichen Operationen außerhalb die eigentliche letzte ausgeführte suchen, damit Sie können ersten konzentrieren sich auf den Tests benötigt Code auf einfache Weise einfach mithilfe Verwaltungskonsole Anwendung oder z. B. mit Testprojekten in der Visual Studio. Auf diese Weise können Sie sicherstellen, dass die eigentliche Geschäftslogik Funktionalität vollständig ist, bevor Sie tatsächlich, die die letzte Prozess einbinden bedeutet in diesem Fall die WebJob. In diesem Fall der Verweis Lösung wir den Business Code auf die Klasse OD4B.Configuration.Async.Common.SiteModificationManager platziert werden und wir aufrufen, die von zahlreichen Standorten.

Dies bedeutete, dass während der Entwicklungszeit wir OD4B verwenden könnten. Configuration.Async.Console.Reset Konsolenanwendung zum Testen und Zurücksetzen der Anpassungen so oft wie von den Websites benötigt, um sicherzustellen, dass diese Geschäftslogik ist vollständig Durchgezogen. Dies hat eigentlich nichts tun mit SharePoint-Add-in-Modell oder Azure-Entwicklung, vielmehr praktische schrittweise Entwicklungskonzepten unabhängig davon welche Technologie, die Sie verwenden. In Zeiten, wenn ich ein Lautsprecher in der MCM für SharePoint Zertifizierung Schulung wurde, ich wurde in Bezug auf diese wie die [NKOTB-Methode](https://www.youtube.com/watch?v=iCrargw1rrM), aber das ist nicht wirklich eine Industrie-standard-Terminologie :-)

Eine der hervorragende Verbesserungen hinsichtlich der debugging für die WebJobs wurde in das Visual Studio 2014 4 eingeführt. Die neu eingeführten Azure Verbindungen und Projektvorlagen können Sie tatsächlich Remotedebuggen mit WebJob in der Azure-Seite ausgeführt. Sie müssen die WebJob für die Azure und nach dem bereitstellen, auf denen können Sie die Debugsitzung starten, indem rechts auf WebJob-Instanz aus klicken Sie im *Server-Explorer* , und wählen im Kontextmenü die Option *Debugger anfügen* .

![Klicken Sie im Server-Explorer erweitert die geschachtelte Objekte-Websites, Vesaj-od4bconf, WebJobs, kontinuierliche, OD4BConfigurationAsyncWebJob. Über OD4BConfigurationAsyncWebJob und die Kontextmenüoption, den, die Debugger angefügt hervorgehoben ist, wird ein Kontextmenü angezeigt.](media/Recipes/OD4BCustomization/server-explorer.png)

Es gibt sogar ein Tester zum Senden von Recht formatierter Nachrichten an die Warteschlange in der Referenz-Lösung. *OD4B. Configuration.Async.Console.SendMessage* Projekt einfach um haben die Möglichkeit, den Prozess WebJob Debuggen, ohne das app-Webpart an ein anderes bereitstellen erstellt wurde. Trat wieder auf das Debuggen und testen den gesamten Prozess schrittweise erneut.

<a name="webjob-environment-variables"></a>WebJob Umgebungsvariablen
----------------------------

Eine interessante Aspekte zu den WebJobs sind, dass sie unter einem Azure Websites ausgeführt werden, aber ihre Ausführung Speicherort ist geringfügig normalen Websites in Azure. Bedeutung ich dabei ist, wenn Sie zusätzliche Dateien oder Objekte zusammen mit der WebJob für die Azure bereitstellen, Probleme auftreten kann, wenn Sie davon ausgehen, dass Sie die Ressourcen direkt im Code WebJob mit klassischen relative Pfade verweisen können.

In diesem Fall haben wir eine JavaScript-Datei und einige Dateien für das benutzerdefinierte Design, die auf der Azure-Website bereitgestellt wurden, damit sie bei Bedarf in der SharePoint-Websites hochgeladen werden konnte. Sie können diese Dateien in der Azure sehen, wenn Sie die Verzweigung Dateien unter bestimmten Website erweitern.

![Klicken Sie im Server-Explorer erweitert geschachtelte Objekte-Websites, Vesaj od4bconf, Dateien, Ressourcen, Designs, Garage und Dateien im Ordner Garage angezeigt.](media/Recipes/OD4BCustomization/azure-web-site.png)

In der Regel in Azure-Websites verweisen Sie auf diese Dateien mit folgendem format

    string path = HostingEnvironment.MapPath(
        string.Format("~/{0}", "Resources/OneDriveConfiguration.js"));

Da WebJobs jedoch in anderen Speicherort und nicht im Kontext von IIS ausgeführt werden, funktioniert über den Verweis auf die Datei nicht, da Zuordnung aus dem Kontext des Prozesses WebJob fehlschlägt. Dies ist, in dem bestimmte Umgebungsvariablen WebJob helfen kann.  Im Fall Lösung Verweis verwendet haben wir bestimmte Umgebungsvariable WEBROOT_PATH WebJob für den Zugriff auf den Ordner zugeordnete Website.

    string jsFile = Path.Combine(
        Environment.GetEnvironmentVariable("WEBROOT_PATH"), 
        "Resources\\OneDriveConfiguration.js");

Es gibt auch einige Umgebungsvariablen für WebJobs, die Ihnen helfen kann. Sie können die anderen Umgebungsvariablen mithilfe von Code überprüfen und eine gute Verweise in der GitHub für [diese](https://gist.github.com/sayedihashimi/831d8883cdf1d23823f3)vorhanden ist.

<a name="video-demonstrating-the-solution-and-the-actions"></a>Video zum Demonstrieren der Lösung und Aktionen
================================================

[Nachfolgend finden Sie ein Video](http://video.ch9.ms/ch9/053b/3496f324-dc88-4e1f-937f-e1a177fc053b/OD4BCustomizer_high.mp4) zeigt die Lösung in der Praxis, einschließlich Erläuterung der Lösung Strukturen und wie Sie es in der Office 365-Umgebung verwenden würden OneDrive for Business-Websites zu ändern.

<a name="related-links"></a>Verwandte links
=============
- [Anpassen der OneDrive für Unternehmen Websitebranding](Customization-Options-For-OD4B-Sites.md)
- Artikel mit Hinweisen zur [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Artikel mit Hinweisen zur")
- Feldverweise in MSDN unter [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Verweise in MSDN")
- Videos zur [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")

<a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele
===================

- [OD4B. Configuration.Async (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Solutions/OD4B.Configuration.Async)
- [Provisioning.OneDriveProvisioning (O365 Plug & Play-Beispiel)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.OneDriveProvisioning)
- [Plug & Play-Hauptkomponente von Office](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
- Beispiele und Inhalte am https://github.com/SharePoint/PnP

<a name="applies-to"></a>Gilt für
==========
- Office 365 mit mehreren Mandanten (MT)
- Office 365 dedizierte (D) *teilweise*
- SharePoint 2013 lokal – *teilweise*

*Muster für dedizierte und lokalen sind identisch mit SharePoint-Add-in-Objektmodell Techniken, aber Unterschiede bestehen, auf die möglichen-Technologien, die verwendet werden können.*
