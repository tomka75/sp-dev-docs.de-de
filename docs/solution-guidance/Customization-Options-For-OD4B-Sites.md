---
title: "Anpassung von OneDrive für Unternehmen Websites #"
ms.date: 11/03/2017
ms.openlocfilehash: 82fe71f4974ce83d7d08e78d8835e5ace8e8d219
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="customization-of-onedrive-for-business-sites"></a>Anpassung von OneDrive for Business-Websites #

### <a name="summary"></a>Summary ###
OneDrive for Business-Websites kann in Office 365 oder mit app-Modell im Allgemeinen angepasst werden basierend auf Unternehmens-Anforderungen. Tatsächliche Techniken zum Ausführen diese Anpassung unterscheiden sich in der lokalen, da nur app-Modell Techniken verwendet werden können. Diese Seite enthält Details über die tatsächliche Muster die mit app-Mdoel zum Anpassen von OneDrive for Business-Websites verwendet werden kann. 

# <a name="why-would-you-customize-onedrive-for-business-sites"></a>Warum würde OneDrive for Business-Websites werden angepasst? #

Es gibt zahlreiche verschiedene Aspekte zum Anwenden von Anpassungen auf OneDrive für Websites mit Geschäftsdaten (OD4B). Sie können diese Websites natürlich, da sie die SharePoint-Websites sind, aber gleichzeitig immer Sie die kurz- und langfristigen Auswirkungen der Anpassungen sollten anpassen. In der Regel von einer Ziehpunkt möchten wir geben Sie die folgenden auf hoher Ebene Richtlinien für das Anpassen von OD4B Websites. 

- Anwenden von branding Anpassungen, die mit Office 365-Designs oder Designmodul für SharePoint-Website
- Wenn Design Module nicht genug sind, können Sie einige CSS-Einstellungen mit alternativen CSS-Option anpassen.
- Vermeiden Sie OD4B-Websites mithilfe von benutzerdefinierten Gestaltungsvorlagen, da Sie zusätzliche langfristig Kosten und Probleme mit zukünftige Updates Dadurch wird anpassen
  + In den meisten Fällen erreichen Sie alle branding Standardszenarien mit Designs und alternative CSS, damit dies nicht wirklich diese Beschränkung ist
  + Wenn Sie benutzerdefinierte Masterseiten verwenden möchten, bereiten Sie zum Anwenden von Änderungen auf die Websites, wenn wichtige Updates funktionsfähig zu Office 365 angewendet werden
- Sie können zum Ändern oder Ausblenden der Funktionen von der Website Einbetten von JavaScript
- CSOM können Sie beispielsweise steuern Sprache oder regionalen Einstellungen in der OD4B-Websites (Siehe neue APIs)
- Wir empfehlen die Verwendung von Inhaltstypen und site Spalten in OD4B Websites zur Vermeidung von Problemen mit nicht die 
  + Stellen Sie sich OD4B Websites wie für persönliche nicht strukturierten Daten und Dokumenten. Teamwebsites und befindet sich für die Zusammenarbeit sind dann für Unternehmensdaten und Dokumente, in dem Sie sicherlich jegliches Informationsverwaltungsrichtlinien und Metadaten verwenden können, sollen.

Als eine Zusammenfassung Anpassungen definitiv Office 365 unterstützt werden, und Sie können beibehalten auf ihrer Verwendung in OD4B Websites. Nur tatsächlich möchten wir sicherstellen, dass Sie die kurz- und langfristigen Auswirkungen dieser Anpassungen in den Betrieb und Wartung Perspektive berücksichtigen. Dies ist nicht wirklich spezifisch für SharePoint, vielmehr Daumenregel für alle IT-Lösung Build mit einer beliebigen Plattform. 

Es folgt ein Beispiel der OD4B-Website, die von oben angegebenen Richtlinien angepasst wurde. In diesem Fall hat das Endergebnis mit Kombination von Office 365-Designs, Websitedesign und Nutzung von so genannte JavaScript Einbetten von Muster erreicht wurde.

![Eine angepasste OD4B-Website.](media/Customization-Options-For-OD4B-Sites/Customization-Options-For-OD4B-Sites-01.png)

# <a name="challenge-with-applying-onedrive-for-business-site-customizations"></a>Anwenden von OneDrive for Business-websiteanpassungen-Abfrage? #

Beginnen Sie mit definieren, was die Herausforderung ist, und was versuchen wir hier lösen. Technisch gesehen jedes OneDrive for Business-Website ist zurzeit identisch-Architektur in der persönlichen oder Meine Websites in SharePoint 2007 oder 2010 Version verwendet verwenden. Dies bedeutet, technisch jedes OneDrive für Business-Website ihre eigene Websitesammlung ist und wir keine zentralen Ort zum branding oder eines anderen Anpassungen gelten müssen.

![Jede OneDrive for Business-Website ist eine eigene Websitesammlung unter der verwaltete Pfad der persönlichen, und die Url wird basierend auf dem zugeordneten Benutzerprofil erstellt. In der Abbildung werden drei Standorte als untergeordnete Websites aufgelistet. Die URL der ersten untergeordneten Website endet mit /bill_contoso_com. Die zweite endet mit /vesa_contoso_com. Die dritte endet mit /john_contoso_com.](media/Customization-Options-For-OD4B-Sites/Customization-Options-For-OD4B-Sites-02.png)

Klassische Lösung erforderlichen Konfiguration auf die OneDrive for Business-Websites anwenden (einschließlich Meine oder persönliche Websites) wurde basierend auf Funktion Heften in auf Farmebene. Dies bedeutete, dass Sie farmlösung für die SharePoint-Farm bereitgestellt und Feature-Framework zum Zuordnen von Ihrem benutzerdefinierten Features jedes Mal aktiviert werden verwendet eine Meine Website erstellt wurden, klicken Sie dann der Anwendung erforderlichen Anpassungen verantwortlich war. Diese ähnlichen Ansatz funktioniert nicht in Office 365, da es erfordert farmlösung bereitgestellt werden und das geht einfach mit Office 365-Websites. Daher müssen wir Alternativen zum Anwenden der erforderlichen Änderungen auf die Websites zu suchen.

In Office 365 es keine zentrale Ereignis ausgelöst ist, die wir unsere benutzerdefinierten Code, wenn verbinden konnte wird OD4B-Website erstellt. Dies bedeutet, dass wir genauer alternative Lösungen müssen also durchaus üblich mit app-Modell Ansätze. Führen Sie nicht auf dem alten Modellen bleiben Sie, überlegen Sie, wie Sie dieselbe Endergebnis mit neuen APIs und Technologien zu erzielen. Im Hinblick auf reine Anforderung es spielt keine Rolle wirklich wie wir die Anpassungen anwenden auf den Websites, solange sie angewendet werden, da geschäftsanforderung ist nicht für das Heften Feature verwenden, er hat zum Anwenden benötigt Anpassungen mit, was unterstützt Technische Mechanismus. 

# <a name="different-options-for-applying-customizations"></a>Verschiedene Optionen zum Anwenden von Anpassungen #

In der Praxis haben wir vier verschiedene Mechanismen OD4B Websites in Office 365 zentralisierte Anpassungen zuweisen. Sie könnten auch manuelle Option wie der fünften berücksichtigen, aber im Fall müssen Hunderte oder Tausende von OD4B Websites, mit der manuellen Optionen ist nicht wirklich eine realistische Option. Nachfolgend finden Sie die verschiedenen Optionen haben wir.
 
1. Office 365-Suite-Ebene Settings (Office 365-Designs und andere Einstellungen)
2. Ausgeblendete app-Webpart mit Benutzerkontext
3. Vor dem Erstellen und Anwenden von Konfiguration
4. Remote Zeitgeberauftrag basierend auf Profil benutzeraktualisierungen

Die Optionen haben Vorteile und Nachteile in diese und die richtige Option hängt von Ihrer detaillierte geschäftlichen Anforderungen. Einige dieser Einstellungen Sie können auch anwenden der Office 365-Suite-Ebene, aber häufig würde werden Suchen Sie einige weitere Einzelheiten damit tatsächliche Anpassungen erforderlich sind. Natürlich kommt es auf die genaue Anforderungen und betriebliche Analysen auf deren Einfluss auf die kurz- und langfristigen.

## <a name="office-365-suite-level-settings"></a>Office 365-Suite Einstellungen auf Poolebene ##

Office 365 ist viel mehr als nur SharePoint, wie Sie kennen. Finden Sie mehr zusätzliche Dienste die nicht auch der SharePoint-Architektur, wie Delve, Yammer und viele anstehende Dienste basieren. Dies bedeutet, dass die Enterprise branding und Konfiguration ist nicht praktisch steuern was wir in der SharePoint-Websites haben, vielmehr wir sollten werden Planen der allgemeinen Endbenutzer Erfahrung und wie wir stellen, dass die einheitliche Konfigurationen verschiedene Dienste schneidet.

Klassisches Beispiel für diesen Anforderungen Enterprise ist branding und dafür haben wir bereits Office 365 Designoberfläche eingeführt, die verwendet werden kann, um einige branding steuern. Wir haben auch andere in Kürze verfügbare Features, einschließlich der hilfreichen steuern, die Steuerung Ihrer Website und andere Einstellungen von zentralen Standort außerhalb der websitesammlungseinstellungen, wie das anstehende Compliance Center für Office 365, die derzeit in der Übersicht über die aufgeführt ist der Office 365.

Folgende Abbildung zeigt die unterschiedlichen Einstellungen jetzt für die Office 365-Designoberfläche, die dann firewallübergreifenden alle Office 365-Dienste angewendet wird.

![Zeigt die Office 365-Website mit der benutzerdefinierten Designs Registerkartenseite berechtigt Verwalten benutzerdefinierter Designs für Ihre Organisation, Anpassen von Office 365 zu einer Ihrer Organisation der Marke widerspiegeln. Einstellungen sind verfügbar für benutzerdefinierte-Logo-URL für eine Tabellentitel Logo, Hintergrundbild, Akzentfarbe, Navigation Leiste Hintergrundfarbe, Text-und Symbole und App-Menü Symbolfarbe.](media/Customization-Options-For-OD4B-Sites/Customization-Options-For-OD4B-Sites-03.png)

Da standardmäßig Einstellungen für Office 365-Design für steuernde OD4B Website Suite Balken sind, werden in den meisten Fällen verwenden Sie diese Optionen zusammen mit anderen Optionen um sicherzustellen, dass Sie mindestens bereitstellen können, dass die richtigen Brandingelemente Ihre Websites OD4B schneidet. Beachten Sie, wenn Sie beispielsweise Office 365 Design für Office 365-Verwaltungstool ändern, es dauert, ziemlich sehr lange angewendeten für OD4B Websites, für die erste also Verständnis sein. 

## <a name="hidden-app-part-with-user-context"></a>Ausgeblendete app-Webpart mit Benutzerkontext ##

Hierbei handelt es sich um einen Ansatz verwenden zentralisiert, in dem Zielseite als Speicherort für den benötigten Anpassungsprozess starten. Dies bedeutet, dass Sie an einem zentralen Ort wie Unternehmen Intranet Front-Seite haben, in dem der Benutzer immer beim Öffnen von ihrem Browser Zielseite werden müssten. Dies ist ziemlich typische Prozess mit mittelgroße und größere Unternehmen wobei corporate Zielseite dann mithilfe von Gruppenrichtlinien in den Active Directory gesteuert. Dadurch wird sichergestellt, dass Endbenutzer können Sie nicht die standardmäßige Willkommensseite der Domäne beitreten Browser Unternehmen überschreiben.

Wenn Benutzer mit dem Intranet eingeht, haben wir wird app-Webpart auf der Seite ausgeblendet die den Anpassungsprozess gestartet wird. Es können tatsächlich von der gesamten OD4B Site Creation auch zuständig sein, da normalerweise Benutzer die Website OD4B einmal besuchen müssten Zeit, bevor die websiteerkennungsprozess gestartet wird. Ausgeblendete app-Webpart eine Seite vom Anbieter gehosteten-add-in in Azure gehostete tatsächlich gehostet werden. Diese Seite ist dann starten Sie den Anpassungsprozess verantwortlich.

Lassen Sie uns näher auf der logische Entwurf dieses Ansatzes.

![Diagramm zum Anzeigen der Beziehungen. Das App-Webpart auf der SharePoint-Website verwendet instanziieren, um zur Provider-Hosted Apps zu wechseln. Provider-Hosted Apps wird die Nachricht hinzufügen So wechseln zur Speicherung Warteschlange verwendet. Speicher Warteschlange verwendet instanziieren, um zur WebJob zu wechseln. WebJob verwendet Änderungen übernehmen, fahren Sie mit der OD4B-Website.](media/Customization-Options-For-OD4B-Sites/Customization-Options-For-OD4B-Sites-04.png)

1. Ort ausgeblendet app-Webparts zum zentralen Standort, auf dem Endbenutzer sorgt wird. In der Regel ist dies das Unternehmensintranet-Startseite.
2. App-Webpart eine Seite vom Anbieter gehosteten add-in, gehostet werden, wobei in den serverseitigen Code wir den Anpassungsprozess initiieren, indem Sie erforderlichen Metadaten der Azure-Speicher-Warteschlange hinzufügen. Dies bedeutet, dass diese Seite wird nur die Anpassung Anforderung empfangen, aber Änderungen die Verarbeitungszeit normalen beibehalten wird nicht tatsächlich angewendet.
3. Dies ist die Warteschlange tatsächlichen Azure-Speicher, die Nachrichten, die in die Warteschlange für die Verarbeitung empfangen. Auf diese Weise können wir die Anpassung Prozess asynchron steuern, sodass es wie lange Endbenutzer eigentlich keine Rolle spielt behandeln wird in der ersten Seite des Intranets bleiben. Wenn der Anpassungsprozess synchrone wäre, würden wir werden abhängig vom Endbenutzer im Browser in der Front-Seite im Intranet geöffnet lassen, bis die seitenausführung abgeschlossen ist. Optimale Endbenutzers würde dies nicht eindeutig sein. 
4. WebJob verknüpft, um die Speicherwarteschlange führen die aufgerufen wird, wenn ein neues Element in die Speicherwarteschlange platziert wird. In diesem WebJob erhält die erforderlichen Parameter und Metadaten aus der Nachricht in der Warteschlange auf rechten Websitesammlung zugreifen. WebJob app nur token verwendet und haben die erforderlichen Berechtigungen zum Bearbeiten von Websitesammlungen in der Ebene der Mandant gewährt wurde.
5. Tatsächliche Anpassungen sind nacheinander angewendet, auf Websites für die Personen, die besuchen die Front-Intranet-Seite, um den zu starten.

Dies ist auf jeden Fall den zuverlässigste Prozess, um sicherzustellen, dass die richtige Konfigurationen auf den Websites OD4B vorhanden ist. Sie können auf einfache Weise Anpassung Versioning Logik, an den Prozess hinzufügen auch benötigte Updates auf den Websites OD4B anwenden ist, wenn eine Aktualisierung erforderlich ist und Benutzer Intranet-Startseite beim nächsten besucht. Diese Option erfordert jedoch, dass Sie diesen zentralen Speicherort verfügen, in dem die Endbenutzer Zielseite sind.

Wenn Sie der klassische Modelle der SharePoint-Entwicklung mit farmlösungen vertraut sind, ist dies als einmal ausführen von Zeitgeberaufträgen sehr ähnlich.

## <a name="pre-create-and-apply-configuration"></a>Vor dem Erstellen und Anwenden von Konfiguration ##

Diese Option basiert auf das vor dem Erstellen der OD4B Websites, bevor Benutzer darauf zugreift. Dies kann mithilfe von relativ neu-API die uns abwesend zum Erstellen von Websites für bestimmte Benutzer OD4B in Batch-Verarbeitung bietet mit CSOM oder REST erreicht werden. Erforderliche Code initiiert werden kann mithilfe eines PowerShell-Skripts oder vom tatsächlichen Code die remote-APIs aufrufen, ist. 

![Ein Administrator verwendet, vor dem Erstellen und anpassen, um eine OD4B-Website zu erstellen.](media/Customization-Options-For-OD4B-Sites/Customization-Options-For-OD4B-Sites-05.png)

1. Administrator wird mithilfe die remote-Erstellung APIs OD4B Websites für Benutzer erstellen und die erforderlichen Anpassungen ist auf den Websites OD4B im Rahmen des Prozesses zum Skript anwenden.
2. Tatsächliche OD4B Websites sind auf der Office 365 für bestimmte Benutzer erstellt und deren Benutzerprofilen verknüpft

In gewisser ist dies auch wirklich zuverlässigen Prozess, jedoch müssen Sie neue Personen und Updates "manuell", verwalten die kann mehr Arbeit, klicken Sie dann mithilfe der ausgeblendeten app-Webpart-Methode bedeuten. Dies ist definitiv Ansatz ergriffen und insbesondere dann hilfreich sein kann, wenn Sie migrieren in eine andere Datei Freigabe Lösung für die OD4B und vermeiden Sie die Notwendigkeit der Endbenutzer Zugriff auf die OD4B Site einmal, vor dem Starten der aktuelle Werte Website erstellen möchten.

## <a name="remote-timer-job-based-on-user-profile-updates"></a>Remote Zeitgeberauftrag basierend auf Profil benutzeraktualisierungen ##

Dieser Ansatz bedeutet Durchsuchen von Benutzerprofilen für die Überprüfung, auf denen die OD4B-Website erstellt wurde, und dann die Änderungen auf die Websites anwenden, je nach Bedarf. Dies bedeutet, dass geplanter Auftrag ausgeführt außerhalb von SharePoint, in dem regelmäßig den Status überprüfen und führen Sie die Anpassungen erforderlich. Geplanter Auftrag konnte als eine WebJob in Azure ausgeführt wird oder so einfach wie das PowerShell-Skript in Ihre eigene Windows-Taskplaner geplant werden. Natürlich hat die Skala der Bereitstellung außerordentlich Einfluss auf der ausgewählten Option planen.

![Ein Remote-Zeitgeberauftrag verwendet wird, durchlaufen Websitesammlungen, zum Anpassen von jedem Standort.](media/Customization-Options-For-OD4B-Sites/Customization-Options-For-OD4B-Sites-06.png)

1. geplante Aufgabe wird die Benutzerprofile, die der Benutzer für die Überprüfung, wer OD4B hat Website bereitgestellt 2.Klicken Istwert Websites angepassten-nacheinander basierend auf den geschäftlichen Anforderungen sind zugreifen wird initiiert

Eines der wichtigsten Nachteile der diese Option ist, dass es kann deutlich eine Situationen, in dem Benutzer die OD4B Websites zugreifen können, bevor die Anpassungen installiert worden sind. Diese Option ist gleichzeitig interessante Add-on für andere Optionen, um sicherzustellen, dass Endbenutzer beliebige der erforderlichen Einstellungen auf den Websites nicht geändert haben oder zu überprüfen, ob die Websiteinhalte OD4B mit den Unternehmensrichtlinien abschließt.

----------

### <a name="related-links"></a>Verwandte links ###
-  [Anpassen von OneDrive for Business-Websites mit-add-in-Objektmodell (MSDN-Blog-Artikel)](http://blogs.msdn.com/b/vesku/archive/2015/01/01/customizing-onedrive-for-business-sites-with-app-model.aspx)

### <a name="related-pnp-samples"></a>Verwandte Plug & Play-Beispiele ###
-  [Anpassen von OD4B Websites mit Async-Muster](#)
-  [Klassische app Teil und Synchronisierung Prozess zum Anpassen der OD4B-Website](https://github.com/SharePoint/PnP/tree/master/Solutions/Provisioning.OneDrive)
-  [Vor dem Erstellen von OD4B Websites für Benutzer](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.OneDriveProvisioning)

### <a name="applies-to"></a>Gilt für ###
-  Office 365 mit mehreren Mandanten (MT)
-  Office 365 dediziert (D) - *teilweise*
-  SharePoint 2013 lokal - *teilweise*

*Muster für dediziert und lokale sind identisch mit der add-in-Modell Techniken, es gibt jedoch Unterschiede auf die möglichen Technologien, die verwendet werden kann.*

### <a name="author"></a>Autor
VESA Juvonen (Microsoft) - [@vesajuvonen](https://twitter.com/vesajuvonen)

### <a name="version-history"></a>Versionsverlauf ###
Version  | Datum | Kommentare
---------| -----| --------
1.0  | 2. Januar 2015 | Erstveröffentlichung | VESA Juvonen (Microsoft)
