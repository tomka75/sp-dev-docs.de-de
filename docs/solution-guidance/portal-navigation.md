---
title: "Bewährte Methoden für SharePoint Online-Portale - Navigation Lösungen"
ms.date: 11/03/2017
ms.openlocfilehash: 691e451aa2c1f9c7a0c0f6db969c36029f319235
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="proven-practices-for-sharepoint-online-portals---navigation-solutions"></a>Bewährte Methoden für SharePoint Online-Portale - Navigation Lösungen

Jedes Portal Projekt muss zum Implementieren einer Lösung für die Navigation. Basierend auf der Project-Anforderungen, die Navigation Lösung kann festlegen, dass nur Out-of-Box (OOB) Navigation-Komponenten nutzen nur benutzerdefinierte Navigationskomponenten oder eine Kombination von OOB und benutzerdefinierten Komponenten. 

Unabhängig von der Auswahl, eine Frage bleibt: Gewusst wie: Erstellen einer gut funktionierende Navigationssystem in SharePoint Online? In diesem Artikel werden diese Frage beantwortet.

> [!NOTE] 
> Obwohl dieser Anleitung in erster Linie SharePoint Online bezieht, die meisten davon gilt auch für Portale in einer lokalen SharePoint-Umgebung gehostet.

_**Gilt für:** SharePoint Online_

## <a name="anti-patterns-in-other-words-dont-do-these-things"></a>Anti-Muster (also nicht sollten Sie folgende Aktionen)
<a name="bk_antiPatterns"> </a>

Wenn Sie Probleme mit Ihrem Portal im Allgemeinen und Ihre Lösung Navigation insbesondere haben möchten, sollten Sie die folgenden Anti-Muster:

- Verwenden Sie **strukturelle** Websitenavigation Out-of-Box (OOB) Wenn die Websitesammlungen von Ihrem Portal komplexe Struktur (mehrere Ebene von Websites und/oder eindeutige Berechtigungen)  
- Verwenden Sie eine benutzerdefinierte Navigation-Lösung, die alle Navigationsknoten für alle benutzerdefinierten Navigationssteuerelemente anfordert, sobald das Laden der Seite, auch für Steuerelemente, die Anfangs reduziert/ausgeblendet sind
- Verwenden Sie eine benutzerdefinierte Navigation-Lösung, die nicht die Navigationsknoten Zwischenspeichern erhaltenen
- Verwenden Sie eine benutzerdefinierte Navigation-Lösung, die beruht auf den Vorversion listet (SOAP)-Webdienst
    - zusätzliche Probleme möglich ist übergeben sie einige schlecht formulierte CAML-Abfragen

## <a name="rationale-for-a-custom-navigation-solution"></a>Begründung für eine benutzerdefinierte Navigation-Lösung
<a name="bk_customNavRationale"> </a>

Es gibt eine Reihe von Gründe, warum eine Portal-Architekt entscheiden möglicherweise eine benutzerdefinierte Navigation Lösung verfolgen. Die meisten Gründe beziehen sich auf die Tatsache, dass moderne Portal plant reagierend Natur sind und in der Regel ein funktionsreiche Navigation mit dem enthalten; als solche fehl zum Zuordnen des vorgeschlagenen Entwurfs auf SharePoint letztlich, da die serverseitige Navigationssteuerelemente Out-of-Box (OOB) konfiguriert werden können, um eine oder mehrere der vorgeschlagenen Entwurf erfüllen. Beispiele für bestimmte gehen Sie folgendermaßen vor:

- Das Steuerelement OOB und seine UX Management unterstützt keine schnell Benutzeroberflächendesign
- Das Steuerelement OOB treten keine die erforderlichen Verhaltensweisen (flyoutmenü/beim Daraufzeigen, hilfsspalten Menü, rich-Media, verzögerte Laden usw.).
- Das OOB-Steuerelement unterstützt nicht die gewünschte Navigation Hierarchie Attribute (Header, gruppieren, die Tiefe, Link Grenzwert usw.) 
- Das OOB-Steuerelement unterstützt nicht die gewünschte Navigation Link-Attribute (Miniaturansichten, Bild verknüpfen, veröffentlichen Start-/End, hervorgehobenem usw..) 
- Das OOB-Steuerelement ist nicht oder ist nicht mehr verfügbar (Fußzeile, Breadcrumb usw.).
- Das Steuerelement OOB lässt sich nicht in Datenspeichern und ältere benutzerdefinierte Navigation integrieren.
- Die OOB Management UX inkonsistent über Navigationssteuerelemente und ist nicht benutzerfreundlichen

Berücksichtigen Sie ausreichen der Gründe addieren, eine benutzerdefinierte Navigation Lösung.

## <a name="youve-decided-to-use-an-out-of-box-oob-navigation-solution"></a>Sie haben entschieden, eine Out-of-Box (OOB) Navigation Lösung verwenden
<a name="bk_oobNavSolution"> </a>

Sie haben die Gründe für eine benutzerdefinierte Navigation Lösung ausgewertet und haben entschieden, dass keines dieser Gründe anwenden. Die gute Nachricht ist, dass Sie bewährten Muster für eine Out-of-Box (OOB) Navigation Lösung nutzen können.

Kurz gesagt besteht aus einem Satz von Navigationssteuerelementen, die ihre Daten in einem Speicher Navigation erhalten eine Lösung für die Navigation. Bei der Auswahl einer OOB Navigation-Lösung ist OOB verwaltete Navigation (weiter unten in diesem Artikel beschrieben) in der Regel die erste Wahl für einen OOB Navigation Speicher, da es eine bessere seitenladeleistung bietet. Die anderen Wahl OOB strukturierte Navigation (weiter unten in diesem Artikel beschrieben), können auf einfache Weise werden sehr Ressource Intensive (insbesondere für komplexe Site Collection Strukturen) und das Ergebnis in erheblich langsamer Seite laden Leistung.

## <a name="youve-decided-to-use-a-custom-navigation-solution"></a>Sie haben entschieden, eine benutzerdefinierte Navigation Lösung verwenden
<a name="bk_customNavSolution"> </a>

Sie haben die Gründe für eine benutzerdefinierte Navigation Lösung ausgewertet und haben entschieden, dass genügend dieser Gründe anwenden. Die gute Nachricht ist, dass Sie bewährten Muster für das Entwickeln einer benutzerdefinierten Navigation Lösung nutzen können.

Das folgende Diagramm veranschaulicht die logische Architektur einer benutzerdefinierte Navigation Lösung:

![Logische Architektur für die benutzerdefinierte Navigation-Lösung](./media/logicalNavSoln.png)

Den folgenden Abschnitten werden die wichtigsten Komponenten der logischen Architektur:

### <a name="navigation-display-control"></a>Steuerelement für die Registerkartennavigation
<a name="bk_navDisplayControl"> </a> 

Dies ist ein benutzerdefiniertes clientseitiges JavaScript Anzeige-Steuerelement, das sich auf der Seite befindet. 

Im Allgemeinen fragt das Steuerelement die Navigation Store, wenn die Seite geladen wird, die Navigation Datenantwort verarbeitet und die Navigationskomponente (Presentation, Informationen und Verhalten rendert). In der Praxis, sollte das Steuerelement ein Muster für die verzögerte Laden beobachten: führt die Navigation Daten Anforderung nur bei Bedarf, und es so lange wie möglich zurückstellen.

Das Anzeige-Steuerelement die statische Definition der Seite zur Entwurfszeit hinzugefügt werden kann (über eine Gestaltungsvorlage (Beachten Sie die Warnhinweise), einem Seitenlayout oder ein Webpart) oder auf der Seite zur Laufzeit (über das Einbetten von JavaScript-Verfahren) den dynamischen Status hinzugefügt werden.

Das Anzeige-Steuerelement nutzt die Client-Side Datenzugriffsschicht (weiter unten in diesem Artikel beschrieben) zum Optimieren der Leistung der Seite.

Das Anzeige-Steuerelement vorsehen optional einen Link Einstellungen für die Seite Navigation die eine Benutzeroberfläche zum Verwalten der Konfiguration für das Navigationssteuerelement bereitstellt.

**Normale Anzeige Navigationssteuerelemente** 
 <a name="bk_navDisplayControls"> </a> 

Hier finden Sie einige allgemeine Richtlinien für die verschiedenen Typen von Navigationssteuerelementen, die in der Regel in einer benutzerdefinierten Lösung Navigation verwendet:

- **Globale Navigation**: implementieren ein benutzerdefiniertes Steuerelements, das eine zentrale Portal-spezifischen Navigation Konfigurationsentität beruht. Verwenden Sie einen öffentlichen Cache für den Navigationsknoten. Berücksichtigen der Seite OOB-Verwaltung.
- **Fußzeile Navigation**: implementieren ein benutzerdefiniertes Steuerelements, das eine zentrale Portal-spezifischen Navigation Konfigurationsentität beruht. Verwenden Sie einen öffentlichen Cache für den Navigationsknoten. Berücksichtigen der Seite OOB-Verwaltung.
- **Siteübersicht**: implementieren ein benutzerdefiniertes Steuerelements, das eine zentrale Portal-spezifischen Navigation Konfigurationsentität abzielt
- **Aktuelle Navigation** (d. h., linken): implementieren ein benutzerdefiniertes Steuerelements, das eine lokale, Web-spezifische Navigation Konfigurationsentität beruht. Verwenden Sie einen öffentlichen Cache für den Navigationsknoten. Berücksichtigen der Seite OOB-Verwaltung.
- **Breadcrumb**: *Implementieren dieser benutzerdefinierten Steuerelements zu vermeiden*. Konstruktion Webobjekte, basierend auf der Url der aktuellen Website an, der übergeordnete Kette ist ein kostspieliger Vorgang
- **Hilfreiche Links**: implementieren ein benutzerdefiniertes Steuerelements, das eine lokale, Web-spezifische Navigation Konfigurationsentität beruht. Verwenden Sie einen öffentlichen Cache für den Navigationsknoten. Berücksichtigen der Seite OOB-Verwaltung.
- **Meine Hyperlinks**: implementieren ein benutzerdefiniertes Steuerelements, das eine **private**, benutzerspezifische Navigation Konfigurationsentität abzielt. Verwenden Sie einen **privaten** Cache für den Navigationsknoten. Geben Sie eine benutzerdefinierte Seite Management.

### <a name="navigation-store"></a>Navigation Store
<a name="bk_navStore"> </a> 

Die Navigation Store behält die Konfiguration des Steuerelements benutzerdefinierte Navigation. Sie können auch das benutzerdefiniertes Navigationssteuerelement eine benutzerdefinierte Navigation Store oder einen Out-of-Box (OOB) Navigation Datenspeicher verwendet haben.

**Benutzerdefinierte Navigation Speicher:** 
 <a name="bk_customNavStores"> </a> 

Die am häufigsten verwendeten benutzerdefinierten schafft Navigation Store, eine benutzerdefinierte SharePoint-Liste, ein Gleichgewicht zwischen Erweiterbarkeit, Verwaltbarkeit und Leistung (Wenn Sie über die Suche abgefragt wird). Das Listenschema kann auf einfache Weise erweitert werden, mit benutzerdefinierten Inhaltstypen, die Kopf-/Navigationsgruppen und Navigationslinks darstellen und Websitespalten, die die gewünschten benutzerdefinierten Attributen (z. B. Anzeigereihenfolge) zu definieren. Durchforstete Eigenschaften für diese Websitespalten können verwaltete Eigenschaften in SharePoint-Suche zugeordnet werden. Die Navigationsdaten werden über die vertrauten OOB Liste Management Seiten auf einfache Weise verwaltet. Die Navigationsdaten können über die SharePoint Search-REST-API remote zugegriffen werden.

> [!NOTE] 
> Navigation suchbasierte ist abhängig von den Suchindex. SharePoint crawlt kontinuierlich Portalinhalt; allerdings noch wird eine kurze Verzögerung bevor Änderungen an der SharePoint-Liste im Suchindex angezeigt werden.

Die einfachste und besten Leistung benutzerdefinierte Navigation-Speicher ist eine JavaScript-Ressourcendatei (z. B. nav.js), die eine Komponente-spezifische Konfigurationsvariable (z. B. FooterNav) deklariert, die durch eine JSON-Zeichenfolge initialisiert wird. Der Browser automatisch lädt die Datei herunter, und speichert ihn zur späteren Verwendung.  Die Daten zur Konfiguration ist für die Verwendung bereit, nachdem es in der JavaScript-Laufzeitumgebung geladen. Der primäre Kompromiss bei diesem Ansatz betrifft die Benutzeroberfläche Verwaltung: mindestens muss ein Administrator eine JSON-Zeichenfolge in einer JavaScript-Datei manuell bearbeiten. Eine benutzerdefinierte Benutzeroberfläche wäre abstrakten den Speicher aus dem Admin, und stellen Dinge etwas benutzerfreundlichere erforderlich.

An das andere Ende des Spektrums der benutzerdefinierten Navigation Speicher ist die benutzerdefinierte Datenbank. Diese Option bietet Ihnen ultimative Flexibilität, erfordert aber auch die am häufigsten benutzerdefinierte Entwicklung. Darüber hinaus wird für die Datenbank, die benutzerdefinierte Web-API und die Navigation Verwaltungsseite eine Hostingumgebung benötigt. 

> [!NOTE] 
> Eine hervorragende Beispiel zeigt, wie Sie eine benutzerdefinierte Navigation Store Implementieren der Verwendungsmöglichkeiten mithilfe der clientseitigen Datenzugriffsschicht aus dem SharePoint-Plug & Play-Repository verfügbar ist: [Client-Side Data Access Layer (DAL)-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Portal.DataAccessLayer)

**Speicher des Out-of-Box (OOB) Navigation:** 
 <a name="bk_oobNavStores"> </a> 

- **OOB verwaltete Navigation (MMS)**: <a name="bk_managedNavStore"></a> verwaltete Navigation können Sie einen Ausdruckssatz Managed Metadata Service (MMS) verwenden, um den Navigationsknoten für eine angegebene Websitesammlung zu konfigurieren. OOB Anzeige Navigationssteuerelemente verbraucht automatisch diese Daten. Die Seite OOB Navigation bietet eine leicht zu bedienende Benutzeroberfläche zum Verwalten von Navigationsknoten innerhalb einer Hierarchie von *uneingeschränkt* (unbegrenzte Tiefe). Benutzerdefinierte Anzeige Navigationssteuerelemente können auch diese Daten nutzen, aber Sie müssen dazu über JSOM wie es derzeit keine REST-API für die verwaltete Navigation Bearbeitung verfügbar ist.

    > [!NOTE] 
    > Es ist sehr schwierig, konfigurieren und verwalten eine globale Navigation Definition über verwaltete Navigation. Als jeweils neu, wenn eine Websitesammlung erstellt wird, müssen Sie die Konfiguration für die Websitesammlung und die zugehörigen Ausdruckssatz duplizieren. Denken Sie daran, die verwaltete Navigation ist auch nicht eingeschränkt, weshalb die Benutzer Links sichtbar ist, die sie nicht zugreifen können.

- **OOB strukturelle Navigation (Website)**: <a name="bk_structuralNavStore"></a> strukturelle Navigation können Sie die systemeigene Struktur der Websitesammlung (seine Webs und Seiten), verwenden, und erstellter Überschriften und Hyperlinks, so konfigurieren Sie die Navigationsknoten für eine angegebene Websitesammlung. Die Seite OOB Navigation bietet eine Benutzeroberfläche zum Verwalten von Navigationsknoten innerhalb einer Hierarchie *eingeschränkt* (beschränkt Tiefe). Benutzerdefinierte Anzeige Navigationssteuerelemente können auch diese Daten nutzen, jedoch müssen dazu über JSOM wie derzeit keine REST-API entwickelt strukturelle Navigation verfügbar ist.

    > [!NOTE] 
    > Die OOB Anzeige Navigationssteuerelemente verwenden Datenbankabfragen (d. h., Inhalt-nach-Abfrage), um die Navigationsdaten abzurufen. Sie hierzu bei jedem Laden der Seite, die sehr ressourcenintensiv für komplexe Websitestrukturen-Auflistung ist. Die Verwendung von strukturelle Navigation wird nur für kleine Portale mit einfachen Websitestrukturen-Auflistung empfohlen. Strukturelle Navigation ist immer sicherheitsoptimiert Ergebnisse zurückgibt.

- **OOB Suchindex (Suche)**: <a name="bk_searchNavStore"></a> Suche gesteuerte Navigation können Sie Abfragen SharePoint-Suchindex für Websites und Seiten, indem Sie die richtige Suchabfrage zu erstellen. Es gibt keine bestimmte OOB Navigation Management-Seite, und Sie müssen zum Implementieren von benutzerdefinierten Anzeige Navigationssteuerelemente, um die von der Suchabfragen abgerufenen Daten nutzen.

    > [!NOTE] 
    > Bei Verwendung suchgesteuerter ist Navigation wichtig, dass Sie die Ergebnisse der abgerufene zwischenspeichern, wie Sie nicht, drücken Sie den Server bei jedem Laden der Seite möchten. Weiter unten in diesem Artikel die mithilfe der clientseitigen Daten wird Access Layer erläutert dem Modell in Kombination mit der Suche gesteuerte Navigation verwendet wird. Genau wie strukturelle Navigation wird bei der Suche gesteuerte Navigation sicherheitsoptimiert, damit die Benutzer nicht erreichbar Links nicht angezeigt werden. Nachteil der Suche gesteuerte Navigation ist, dass die Reihenfolge der die zurückgegebene Navigationselemente steuern ist.


### <a name="navigation-management-page"></a>Navigation-Verwaltungsseite
<a name="bk_navManagementPage"> </a> 

Die Navigation Management-Seite bietet eine Benutzeroberfläche, um die Konfiguration von Navigations-Steuerelement auf eine benutzerfreundliche Weise verwalten.  Die Seite direkt zugegriffen werden kann, als auch aus einem optionalen link für die Navigationssteuerelement (z. B. Link Einstellungen). Die Seite mithilfe der entsprechenden Navigation Store-APIs für den ausgewählten Navigation Store, um die Konfiguration des Navigationssteuerelements verwalten.

Sie können auch das benutzerdefiniertes Navigationssteuerelement, verwenden Sie eine benutzerdefinierte Navigation Management Seite oder eine Seite Navigation Out-of-Box (OOB) haben. 

In vielen Fällen zugeordnet ist die Standardeinstellung OOB Navigation-Verwaltungsseite (z. B. SharePoint-Listenansicht oder-Begriff festgelegt Verwaltungsseite) ausgewählten, die Navigation Store ausreichend sollten. Wenn eine Standardseite nicht verfügbar ist, müssen Sie eine benutzerdefinierte Seite offensichtlich entwickeln. Bei der Entscheidung, ob die vorhandenen Standardseite akzeptabel ist, sollten Sie unbedingt die Gesamtkosten der Entwicklung von einer benutzerdefinierten Seite (Entwurf, Entwicklung und Wartung, hosting und benutzerschulungen) zu berücksichtigen.

Als Daumenregel unterschiedliche benutzerdefinierte Seiten nur, wenn eine Standardoption nicht vorhanden ist, wenn die Seite eine schnell Benutzeroberfläche unterstützen muss, oder wenn die Seite über den Front-End-User-Ansicht des Portals (im Gegensatz zu den Back-End-Admin-Ansicht) verwendet werden soll.  

### <a name="navigation-store-api"></a>Navigation Store-API
<a name="bk_navStoreApi"> </a> 

Die Navigation Store-API bietet eine Programmierschnittstelle zum Verwalten der Konfiguration des Navigationssteuerelements in einer konsistenten und sichere Weise.  

Sie können auch das benutzerdefiniertes Navigationssteuerelement, verwenden Sie eine benutzerdefinierte Navigation Store API oder eine Out-of-Box (OOB) Navigation Store-API haben. Wenn Sie entwickeln und Bereitstellen einer benutzerdefinierten Navigations-API Store möchten, beachten Sie die folgenden Richtlinien:

- Implementieren Sie mit der Technologie Ihrer Wahl (ASP.Net Web-API 2.0, Node.js)
- Hosten der API in einer Internet zugänglichen Umgebung 
- Verwenden Sie Öffentliche DNS-Server für die namensauflösung
- Anfordern von SSL und das SSL-Zertifikat von einer öffentlichen Zertifizierungsstelle erhalten
- Aktivieren des anonymen Zugriffs und Sichern der mit Azure AD-API
- Implementieren Sie die Unterstützung für Cross-Origin Resource unterstützen (CORS)

Für .net Clientumgebungen:

- Ziel-SharePoint-APIs über das SharePoint mithilfe der clientseitigen Objektmodell (CSOM oder REST) 
- Adressieren Sie Ihre benutzerdefinierte Web-APIs über REST
- Adressieren von Drittanbieter-APIs über REST (verwenden Sie SOAP nur bei Bedarf)

Für Browser Clientumgebungen:

- Ziel-SharePoint-APIs über die SharePoint-REST-APIs (Verwenden von JSOM nur bei Bedarf)
    - Verwenden Sie die domänenübergreifende Bibliothek, wenn Sie eine anderen Websitesammlung als Ziel
- Adressieren Sie Ihre benutzerdefinierte Web-APIs über REST
    - Verwenden von Azure AD Authentication Bibliothek für JavaScript (ADAL.js) und implizite OAuth-Ablauf
- Adressieren von Drittanbieter-APIs über REST (oder SOAP-bei Bedarf)

### <a name="client-side-data-access-layer"></a>Mithilfe der clientseitigen Datenzugriffsschicht
<a name="bk_clientSideDal"> </a> 

Der Client-Side Data Access Layer ist eine benutzerdefinierte clientseitige JavaScript-Frameworks für alle benutzerdefinierten clientseitigen Anzeige-Steuerelemente, einschließlich der benutzerdefinierten Anzeige Navigationssteuerelemente zur Verfügung gestellt.  Intelligente Datenladevorgänge-Muster unterstützt, abstrahiert die Details der Client-zu-Server-Anforderungen, bietet Funktionen für die Client-zu-Server-Datenverkehr zu minimieren das Zwischenspeichern von Daten und verbessert die Seite wahrgenommenen Leistung.

Finden Sie im [Artikel Portal Leistung](portal-performance.md) für Weitere Informationen zu den clientseitigen Datenzugriffsschicht.

## <a name="see-also"></a>Siehe auch
<a name="bk_additionalResources"> </a>

- [Leitfaden zur Portal Leistung](portal-performance.md)
- [Optionen für die Websitenavigation für SharePoint Online](https://support.office.com/en-us/article/Navigation-options-for-SharePoint-Online-adb92b80-b342-4ecb-99a1-da2a2b4782eb?ui=en-US&rs=en-US&ad=US)
- [Übersicht über die verwaltete Navigation in SharePoint Server 2013](https://technet.microsoft.com/en-us/library/dn194311.aspx)
- [Client-Side Data Access Layer (DAL) und Navigation Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Portal.DataAccessLayer)
- [Plug & Play-O365 Starter Intranet - Navigation details](http://thecollaborationcorner.com/2016/08/31/part-4-the-navigation-implementation/#.WNoU5oVOKiM)
- [ASP.Net Web-API 2.0](https://msdn.microsoft.com/en-us/library/dn448365(v=vs.118))
- [Azure AD Authentication Bibliothek für JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js)