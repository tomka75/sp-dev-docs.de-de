---
title: "Bewährte Methoden für SharePoint Online-Portal Informationsarchitektur"
ms.date: 11/03/2017
ms.openlocfilehash: 25cefe4e220213d51752450f7a9e73c721970776
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="proven-practices-for-sharepoint-online-portal-information-architecture"></a>Bewährte Methoden für SharePoint Online-Portal Informationsarchitektur

Eine einfarbige Informationsarchitektur ist eine wichtige Voraussetzung für die Realität ein Portal gut zu verwaltende und ausführen. Entwerfen der optimalen Struktur erfordert eine detaillierte Planung. Wenn nicht ordnungsgemäß ausgeführt wird, ein hohes Risiko einer Beeinträchtigung der Benutzer Annahme oder möglich erhebliche Leistungsprobleme vorhanden ist und die Wahrscheinlichkeit, dass beide ist sehr möglich. 

Sie sollten folgende Faktoren berücksichtigen:

- Von Unternehmenszielen und der Organisationsstruktur.
- Welche Art von Inhalt, die Sie zuständig sind. Ist der Content collaborative oder veröffentlichte Inhalt? 
- Content-Klassifizierung und Vertraulichkeit 
- Lebenszyklus der Strategien Inhalts- und mögliche Aufbewahrung und Löschung. Dies gilt auch für Websites sowie. 
- Benutzer von den Inhalt, Verhaltensweisen von allgemeine Aufgaben und erwartet.

Wenn Sie weitere Informationen zu den Benutzern, den Inhalt, wissen es ist beabsichtigt Nutzung, Sie haben eine gute Grundlage zu und können möglicherweise einige der allgemeinen Fehlerquellen um Informationsarchitektur vermeiden.

> [!NOTE] 
> Obwohl dieser Anleitung SharePoint Online Zielgruppenadressierung ist die meisten davon gilt auch für Portale in einer lokalen SharePoint-Umgebung gehostet wird.
>
> In diesem Artikel soll keine tief in alle Aspekte der Unternehmensleitung und die Informationsarchitektur zu wechseln. Der vorgesehene Punkt besteht darin, häufig auftretender Probleme, die Einfluss auf Benutzerakzeptanz und/oder Leistung, markieren Sie beide gleichmäßig Hauptprobleme sind.

_**Gilt für:** SharePoint Online_

## <a name="anti-patternsor-you-shouldnt-be-doing-this"></a>Anti-Muster oder Sie sollte nicht dafür werden
<a name="sectionSectionAntiPatterns"></a> Unterhalb der Liste enthält die wichtigsten Punkte **nicht** zu tun, wenn es darum geht, Entwerfen der Architektur Portal-Informationen:

- Zu viele übergeordnete Portalwebsite Sammlungen - dadurch Verwechslungen und negative Auswirkungen auf Verwaltung, Hinweise zur Sicherheit, Verwendbarkeit, Navigation und Annahme können im Allgemeinen aufweisen.
- Dies kann zu tief Hierarchien in einzelne Websitesammlung mit eindeutigen Berechtigungen - Leistung Herausforderungen führen.
- Verdeckte Inhalte - wirkt sich auf Inhalte, die zu tief sind, Suchen nach Möglichkeit als auch Annahme. Wenn der Benutzer den Inhalt nicht, die, den Sie finden kann für, nach der ein paar Ebenen tief, suchen, sie ihre Arbeit verwerfen und erachten das Portal als ineffiziente, die wiederum Annahme bricht ab. 
- Veraltete Inhalte - niemand "gefällt mir" veraltete Inhalte und erst, nachdem ein paar Mal der auszublenden, sie werden nicht zurückkehren aus diesem Grund. 
- Keine Verwendung der Content-Dispositionsstrategien - wird benötigt Vermeidung veraltete Inhalte sowie innerhalb der Grenzen festgelegte Kapazität bleiben. 
- Vertrauende Seite auf den resultierenden in einen Entwurf für eine schlechte SharePoint Online Taxonomie masterdatenverwaltung schlechter Enterprise. 
 

## <a name="key-considerations"></a>Wichtige Überlegungen
<a name="sectionSection0"></a> Informationsarchitektur ist nicht als einmaligen Vorgang, es einen fortlaufenden Prozess. Während eine optimalen Informationsarchitektur möglicherweise nicht immer offensichtlich für Endbenutzer an, eine mangelhaft entworfene und verwaltete Informationen Architektur wird sicherlich beibehalten Sie, falls der eine falsche verwendet wird. Behalten Sie messen, behalten Sie weiterentwickelt, und bewahren Sie relevant und aktuell auf.

&nbsp;

![](http://i.imgur.com/Ugw1qWn.png)

&nbsp;

### <a name="site-organization-patterns"></a>Website Organisation Muster
Berücksichtigen Sie minimieren die Anzahl der Knoten auf oberster Ebene Ebene der Websitesammlung und die Anzahl der Ebenen in der Informationsarchitektur Unterwebsite.

Die Diskussionen haben um Horizontal/flach Site Collections Vs vertikal/hierarchische geändert. In der Vergangenheit heraufgestuft wir reduzieren Hierarchien in potenziell mehrere separate Websitesammlungen. Dieses wurde vielen Gründen wie IA bewährte Methoden, Menüstrukturen, Inhaltsdatenbank Management, Kapazität usw.. Soweit aus Gründen der Kapazität mit SharePoint Online, die nicht zu wichtig mehr sind. Es gibt jedoch auch andere Aspekte nun wie URL-Einschränkungen. 

Weitere Informationen finden Sie unter [SharePoint Online-Softwarebeschränkungen und-Grenzen](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/sharepoint-online-software-boundaries-and-limits-HA102694293.aspx)

Empfohlene Muster einschließen von Websitesammlungen und Websites in verschiedenen logischen Gruppen wie Unternehmensebene gruppieren und Veröffentlichen von Websites. Einige Beispiele suchcentern, Datenarchive, Ediscovery Center.  Dies können entweder am Stamm Ebene oder unter der verwaltete Pfad "/ sites" sein. Intranetwebsites Veröffentlichung-Portal können auch am Stamm oder unter der verwaltete Pfad "/ sites" sein. Beispiel:

Websites berücksichtigt, dass Ebene Unternehmenswebsites als strukturiert sein können:

    - / Sites /
        - Suche
        - Datenarchiv
        - eDiscovery-Center
        - Medien
        - Compliance-Richtlinie Center
        - Business Intelligence-Portal
        - Inhaltstyphub

Veröffentlichen von Portalwebsites als Websites möglicherweise als strukturiert sein:

    -/sites/
        - Intranet Home
        - Corporate Function A
        - Corporate Function B
        - ...
        - Business Unit A
        - Business Unit B
        - ...


In der Regel wird nicht alles sofort und alle gleichzeitig in die Cloud migrieren, also für eine hybride IA planen und weiterentwickelt nach Bedarf. Planen Sie entsprechend für hybridszenarien.

[SharePoint-Hybrid-Websites und Suche](https://support.office.com/en-us/article/SharePoint-hybrid-sites-and-search-5ff7e56a-7af2-4511-adec-1e043afe244e)

### <a name="permissions"></a>Berechtigungen
Strukturieren von Berechtigungen ist schwierig jedes Mal, und ein weiteres Thema, das erfordert sorgfältige Planung. Die Verwendung von Benutzerkonten, SharePoint-Gruppen und Active Directory-Gruppen/Azure Active Directory-Gruppen zum Festlegen von Berechtigungen kann bisweilen sehr anspruchsvoll sein. SharePoint Online kann eine Kombination aus drei verwenden:

- Direkte Benutzer Berechtigungen Ansatz
- Ansatz für SharePoint-Gruppen
- AD-Sicherheitsgruppen (AAD Sicherheitsgruppen)

> [!NOTE] 
> Wenn Sie sich in SPO befinden, synchronisieren Sie Ihrer Gruppen mit Active Directory verbinden

Versuchen Sie beim Planen der Berechtigungen die folgenden Richtlinien beachten:

- Führen Sie das Prinzip der geringsten Rechte auf starten, erweitern bei Bedarf
- Verwenden Sie den Standard, Standard zunächst gruppiert (Mitglieder, Besucher, Besitzer). Natürlich Beschränken der die Anzahl von Personen zur Gruppe Besitzer
- Verwenden Sie die Vererbung von Berechtigungen und verwenden Sie Gruppen über Personen, wenn Sie Berechtigungen erteilen
- Organisieren von Inhalten nutzen Sie die Vererbung von Berechtigungen oder Organisieren, indem Sie eindeutige Berechtigungen und Segment nach Möglichkeit Klassifizierung Ebenen.

Nicht zugegriffen werden Inhalte, die sollte nicht werden, wird sorgen für Frustration und schließlich beeinträchtigen Akzeptanz durch den Endbenutzer und Suchproblemen Ergebnissen führen.

### <a name="search"></a>Suche
Eine große Anzahl von Entwurfsaspekte im Zusammenhang mit den Konfigurationsoptionen, die speziell für die Suche in SPO sind vorhanden. Eine ausführliche Suche Spezifikation sollten insbesondere für erweiterte Konfigurationen entwickelt werden. Kann die Suchfunktion für Leistung optimiert werden Relevanz und angepasst werden können. Dazu gehören:

- Definieren von verwalteten Eigenschaften suchen können 
- Identifizieren von Seiten für die Optimierung der Relevanz hohe Qualität 
- Verwalten von Abfrageregeln und ergebnisquellen 

Content-Sammlung kann erhebliche Auswirkungen auf die Leistung Ihres Portals und die dazugehörigen Seiten haben. Näheres im [Portal Datenaggregation Artikel](portal-data-aggregation.md) Weitere Informationen zum Content-Sammlung.

### <a name="taxonomy"></a>Taxonomie
Taxonomie werden sowohl der **Navigation** als auch **Daten**behandelt. Durch eine sorgfältige Planung ist aus Sicht der Steuerung als auch einen Bezug auf die Leistung erforderlich. Überlegen Sie Kernaufgaben zu starten, aber auch überlegen künftiges Wachstum und verwaltbarkeit. 

**Inhaltstypen** Ordnungsgemäße Planung, Konfiguration und Implementierung von Inhaltstypen und deren zugeordnete Metadaten ist unerlässlich für die Möglichkeit zum Organisieren, verwalten, klassifizieren und Informationen finden unter SharePoint.

Definieren Sie eine kleine Gruppe von globalen Inhaltstypen – die basiert auf Legal oder Records Management-Teams sowie authoring Anforderungen für tagging usw..

Diese Inhaltstypen sollten mindestens einige Felder haben:
    
    - Informationen Klassifikation
    - BusinessFunction
    - CorporateFunction
    - ...

Diese im Hub-Inhaltstyp erstellen und Verwenden von SharePoint-CSOM zum Erstellen Content-Typen mithilfe von eindeutige ID. Sie müssen immer noch manuell diese Inhaltstypen veröffentlicht. Verwenden Sie den Inhaltstyp-Hub nicht, wenn Sie annehmen, dass in der Websitesammlung Sie müssten die Inhaltstypen zu ändern.

Weitere Informationen zu Inhaltstypen und Content Type Publishing, finden Sie unter: [Einführung in Inhaltstyp und Content Type Publishing](https://support.office.com/en-US/article/Introduction-to-content-types-and-content-type-publishing-A5026D23-8DF8-42F6-B0D6-1920880C0D03)

**Verwaltete Metadaten** Hierbei handelt es sich um ein anderes Thema ähnlich wie Inhaltstypen, die für den Rahmen dieses Artikels zu groß ist. Einen guten Einstieg und Weitere Informationen finden Sie unter [Einführung in verwaltete Metadaten](https://support.office.com/en-us/article/Introduction-to-managed-metadata-a180fa28-6405-4679-9ec3-81d2028c4efc)

Metadaten in SharePoint kann Unternehmen die Vorteile der formelle, verwaltete Taxonomien mit der dynamischen Vorteile von thematischen Kategorien in benutzerdefinierten Möglichkeiten Zuordnung unterschiedliche Informationen Verwendung und Verwaltung von Szenarien zu kombinieren.

Enterprise-metadatenhierarchien können vom Informationen Sicherheit Klassifikationen basieren. Verwalteter Metadaten kann auch Dokumente, Listenelemente, über die Verwendung von Websitespalten und Inhaltstypen usw. zugeordnet werden. Diese verwaltete metadatenausdruckssätze können Manager und Mitwirkende und die Möglichkeit, Ausdrücke zu Ausdruck hinzufügen legt auch kontrolliert werden verwaltet werden. 

Enterprise Begriff Store Hierarchien werden normalerweise von einem Lenkungsausschuss Steuerung mit input ein Prozess, der aus anderen Teams in der Organisation verwaltet werden.  

> [!NOTE] 
> Eine schlechte Planung und schlechte Management können Probleme mit großen taxonomiehierarchien und Tiefe Sortierung verursachen. Die Daten müssen sortierte clientseitige sein, damit es wird empfohlen, überlegen Sie sich die potenzielle Tiefe der Hierarchie und die Anzahl von Ausdrücken zurückgegeben wird. Je tiefer kann die Hierarchie in Kombination mit mehr Begriffe der Client DOM sortieren, um mehrere Sekunden dauern, verursachen. 
>
> Keine löschen Sie Terminologiespeicher Elemente, deren verwerfen der. Beibehalten der Terminologiespeicher bereinigen potenziell fehlende Objekte oder fehlerhafte Berechtigungen, wodurch Verzögerungen in der zurückgegebenen Daten.
>
> Begriffe sind nicht eingeschränkt, damit Vertraulichkeit berücksichtigt werden muss

Für verwaltete Metadaten planen stehen die folgenden Arbeitsblätter:

[Verwaltete Metadatendienste Planungsarbeitsblatt](http://go.microsoft.com/fwlink/p/?LinkId=164578)

[Detaillierten festlegen Planungsarbeitsblatt](http://go.microsoft.com/fwlink/p/?LinkId=163487)

**Navigation** Finden Sie im [Artikel Portal Navigation Lösungen](portal-navigation.md) für Weitere Informationen zu bewährten Methoden Navigation.

### <a name="large-media"></a>Große Medien
Große Dateien, beispielsweise Videos, Bilder, PowerPoint-Dateien können Kummer für Benutzer dazu führen, dass sie erwartungsgemäß relativ schnell abgerufen werden sollen. Dateien wie Videos müssen in bestimmten Abständen stream und einige apps möglicherweise nicht gerendert werden, bis sie die erforderlichen Dateien abgerufen haben. Erwägen Sie das externalisieren große Mediendateien. Dies hilft mit Benutzerakzeptanz. 

Hier sind einige Optionen zu berücksichtigen sind:
- [Erfüllen von Office 365-Videos](https://support.office.com/en-us/article/Meet-Office-365-Video-ca1cc1a9-a615-46e1-b6a3-40dbd99939a6)
- [Verwalten Sie Ihre Office 365-Video-portal](https://support.office.com/en-us/article/Manage-your-Office-365-Video-portal-c059465b-eba9-44e1-b8c7-8ff7793ff5da?ui=en-US&rs=en-US&ad=US)

Die Artikel [Portal Branding](portal-branding.md) und [Portal Leistung](portal-performance.md) markieren sowie die Verwendung des CDN.

Weitere Informationen zu den CDN finden Sie unter:
- [Office 365 öffentliches/privates CDN-Funktion](https://dev.office.com/blogs/general-availability-of-office-365-cdn)
- [Verwenden die Inhaltsübermittlung mit SharePoint Online](https://support.office.com/en-gb/article/Using-content-delivery-networks-with-SharePoint-Online-9a64268c-0b74-4eaa-b971-fb6380b1b165)
- [CDN-Manager](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.CDNManager)


### <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

Patterns & Practices:

- [Office 365-Entwicklung und SharePoint Mustern und Methoden ausgesprochen](https://msdn.microsoft.com/en-us/pnp_articles/office-365-development-patterns-and-practices-solution-guidance)

Lebenszyklus Informationsverwaltung:

- [Übersicht über dokumentlöschrichtlinien](https://technet.microsoft.com/en-US/library/dn790608.aspx)
- [Informationsverwaltungsrichtlinien in Office 365](https://technet.microsoft.com/en-us/library/dn792007.aspx)
- [Einführung in die Anwendungslebenszyklus-Verwaltung von Informationen](https://support.office.com/en-US/article/Introduction-to-information-management-policies-63a0b501-ba59-44b7-a35c-999f3be057b2)

Speicher- und Serverressourcen

- [Verwalten von Speichergrenzen für Websitesammlungen](https://support.office.com/en-US/Article/Manage-site-collection-storage-limits-77389c2c-8e7e-4b16-ab97-1c7103784b08?ui=en-US&rs=en-US&ad=US)
- [SharePoint Online-Softwarebeschränkungen und-Grenzen](https://support.office.com/en-us/article/SharePoint-Online-software-boundaries-and-limits-8f34ff47-b749-408b-abc0-b605e1f6d498?CTT=1&CorrelationId=ab0c93e3-8a23-4a72-887e-bac52c0a874d&ui=en-US&rs=en-US&ad=US)
