---
title: Plug & Play-Bereitstellung framework
ms.date: 11/03/2017
ms.openlocfilehash: 863e69641e103c1cac264a9ca05ecb28e744eebe
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="pnp-provisioning-framework"></a>Plug & Play-Bereitstellung framework

Rufen Sie eine allgemeine Übersicht über remote Bereitstellung verfügbaren Features für Ihre Office 365 und SharePoint Online-Websitesammlungen sowie Kenntnisse über Warum Erstellen von Sandkasten und voll vertrauenswürdige Lösungen nicht mehr empfohlen wird.

Bieten Sie eine Code-centric und Vorlage basierende Plattform für die Bereitstellung Ihrer Websitesammlungen. Das neue Modul Bereitstellung können Sie beibehalten und Wiederverwenden von provisioning Modelle in Ihrer Office 365 und SharePoint Online als auch lokale-Websitesammlungen.

## <a name="why-the-new-approach"></a>Warum neuer Ansatz?

Dies führt zu folgender Frage &mdash; _warum die Notwendigkeit für ein neuer Ansatz?_ Und die Frage _Was sind die Vorteile dieses Ansatzes gegenüber mithilfe von sandkastenlösungen und voll vertrauenswürdige Lösungen?_

Die Antwort auf die erste Frage bezieht sich auf die Einführung von SharePoint-Add-ins und das Add-In Modell (früher als "App-Modell" bezeichnet). Durch diese Änderung Microsoft wurde von sandkastenlösungen und voll vertrauenswürdige Lösungen wird vom Anbieter gehosteten-add-ins verschoben und lokale Lösungen. Diese Innovationen haben eine retooling des provisioning Modells und der Einführung von eine neue Bereitstellung Engine gesteuert.

Im Hinblick auf die zweite Frage &mdash; _Was sind die Vorteile der neuen Bereitstellung Modell?_ &mdash;Es gibt mehrere:

- Anpassen von Vorlagen. Da Websitesammlungen immer mit einer Out-of-Box-Vorlage zu starten, werden die Anpassungen, die Sie mit dem neuen remote provisioning Objektmodell einführen automatische Updates ohne weitere Datenbankwartung erforderlich integrieren. Darüber hinaus vermeidet dadurch Probleme, die aus dem Vorhandensein unterschiedliche Vorlagen in anderen Websitesammlungen verwendet.
    
- Verwenden einer Vorlage basierendes Modell. Bietet eine einfache, Vorlage basierende provisioning-Modell, mit dem Sie ein vorhandenes Design der Website als Vorlage provisioning speichern kann. 
    
- Verwenden verschiedene Ansätze Vorlagen definieren. Alternativ können Sie Ihre Vorlage manuell in XML, das anhand des [Plug & Play-Bereitstellung Schema](pnp-provisioning-schema.md)überprüft definieren, oder Sie können Ihre Vorlage mithilfe von verwaltetem Code zum Erstellen einer Objekthierarchie definieren. Sie können auch die Ansätze kombinieren.
    
- Serialisieren und Wiederverwenden von Vorlagen. Sie können serialisieren und klicken Sie dann Ihre Bereitstellung Vorlagen wiederverwenden.
    
- Beibehalten von Vorlagen in serialisierten Format. Sie können Ihre Bereitstellung Vorlagen in Standarddateiformate Serialisierung für Sie am besten beibehalten &mdash; , beispielsweise XML oder JSON.
    
- Bereitstellen Sie neue Websitesammlungen. Sie können auf einfache Weise neue Websitesammlungen bereitstellen, durch Anwenden von Ihrer Bereitstellung Vorlage auf einer Zielwebsite serialisierten Standarddateiformate Sie auswählen.
    
- Integrieren Sie mit dem Clientobjektmodell. Integration von das Clientobjektmodell (CSOM) können Sie enorme Flexibilität durch automatisierte, codebasierte Bereitstellung aktivieren. Sie können eine neue Websitesammlung mit Ihrer Bereitstellung Vorlage mithilfe von CSOM/REST Code oder Windows PowerShell-Skripts bereitstellen.
    
- Verwenden Sie die Delta-Bereitstellung. Sie können die Bereitstellung Vorlagen auf der Basis vorhandener Websites anwenden. Das Bereitstellung Modul unterstützt die Bereitstellung von Delta und, daher wird hinzufügen/aktualisieren Websites basierend auf den verwendeten Bereich in der Vorlagendefinition bereitgestellt wird.
    
- Erweitern Sie das Modul bereitgestellt werden soll. Sie können auf einfache Weise die Bereitstellung Engine erweitern, mithilfe von benutzerdefinierten Erweiterbarkeit Rollenanbietern, mit denen Sie benutzerdefinierten Logik auszuführen, den Sie mithilfe von CSOM/REST verwalteter Code geschrieben haben.
    
- Arbeiten Sie in lokalen und Office 365-Bereitstellungen. Die Bereitstellung Engine ermöglicht jetzt nahtlos in lokalen und Office 365-Bereitstellungen ordnungsgemäß ausgeführt. Dies ist eine Verbesserung der über vorherige provisioning Techniken, wobei wurden benutzerdefinierter Websitedefinitionen nicht in Office 365 unterstützt, da diese Farm beschränkte Bereitstellungen benötigt.

## <a name="remote-provisioning-in-a-nutshell"></a>Remote kurz gesagt-Bereitstellung

In diesem Abschnitt detailliert wir mit einzelnen remote-Bereitstellung. Allerdings kann es hilfreich sein, zuerst den Überblick betrachten, und fassen Sie remote-Bereitstellung in der einfachsten Form. Auf diese Weise untersucht, umfasst remote-Bereitstellung nur drei Elemente:

1. Entwerfen und Erstellen einer Website Anpassungstools.
    
2. Erstellen Sie und optional beibehalten Sie können Ihre Bereitstellung Vorlage in einem serialisierten Format, das Sie auswählen.
    
3. Wenden Sie die Bereitstellung Vorlage in eine neue oder vorhandene Websitesammlung, die mit einer Out-of-Box-Websitevorlage erstellt wurde.

### <a name="1-model-your-site-and-the-site-artifacts"></a>1. Modellieren Sie Ihrer Website und die websiteartefakte

Schritt 1 wird die websiteanpassungen erstellen, die Sie speichern und für eine Websitesammlung anwenden möchten. Es gibt mehrere Methoden zur Verfügung. Am einfachsten stellen Sie die gewünschten Änderungen an einer vorhandenen Websiteseite, und klicken Sie dann auf dieser Seite als provisioning Vorlage zu speichern. Weitere Informationen finden Sie unter [Provisioning Vorlagen](http://msdn.microsoft.com/library/b3eeb7e7-37cf-4e70-8486-34f67220fe33%28Office.15%29.aspx).

Sie können auch manuell Ihre Bereitstellung Vorlage als XML-Datei oder zum Erstellen einer Hierarchie von Objekten zur Darstellung der websiteartefakte und Struktur mithilfe von verwaltetem Code (CSOM/REST) erstellen. Wenn Sie eine Schemadatei erstellen, müssen Sie die Datei anhand der Bereitstellung XSD-Schemas überprüfen (siehe [Plug & Play-Bereitstellung Schema](pnp-provisioning-schema.md)).

Hier finden Sie ausführlichere Informationen zu Ihrer Website im [Plug & Play-Modul- und der Hauptbibliothek provisioning](pnp-provisioning-engine-and-the-core-library.md) Artikel modellieren.

### <a name="2-export-and-persist-your-provisioning-template"></a>2. exportieren und Ihre Bereitstellung Vorlage beibehalten

Exportieren Sie das angepasste Website-Modell in Ihrer bevorzugten serialisierten Format; Das provisioning Modul ist in Bezug auf Speicherformat unabhängig. Diese gespeicherte Instanz einer Anpassung ist der Bereitstellung-Vorlage, die mit minimalem Aufwand, klicken Sie dann auf neue Websitesammlungen angewendet werden können. Beachten Sie, dass serialisieren und speichern Sie Ihre Vorlage von ein optionaler Schritt, der erforderlich ist ist, nur, wenn die Vorlage erhalten bleiben soll. Es ist nicht erforderlich sind, um die Vorlage serialisieren, um auf eine neue Websitesammlung angewendet.

### <a name="3-apply-your-provisioning-template-to-a-new-site-collection"></a>3. gelten Sie Ihre Bereitstellung Vorlage für eine neue Websitesammlung

Entweder ein Windows PowerShell-Skript oder eine CSOM/REST Code können Sie Ihre Bereitstellung Vorlage für neue oder vorhandene Websitesammlungen angewendet. Sie können auch eine komplette Websitesammlung oder nur einen Teil davon bereitstellen. Ein Beispiel für remote-Bereitstellung in der Praxis, einschließlich der Bereitstellung Vorlage, XML, Serialisierung finden Sie unter [Provisioning Console Application Sample](provisioning-console-application-sample.md).

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [PnP-Remotebereitstellung](pnp-remote-provisioning.md)
    
- [Beispiel einer Anwendung in Konsole-Bereitstellung](provisioning-console-application-sample.md)
    
- [Plug & Play-Bereitstellung Modul- und die Core-Bibliothek](pnp-provisioning-engine-and-the-core-library.md)
    
- [Plug & Play-Bereitstellung schema](pnp-provisioning-schema.md)
