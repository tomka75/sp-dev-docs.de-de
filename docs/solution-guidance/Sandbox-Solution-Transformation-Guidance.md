---
title: Sandkasten-Transformation ausgesprochen
ms.date: 11/03/2017
ms.openlocfilehash: b3b254b0bc1c7b086fff73f4b02e7691da6dd945
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sandbox-solution-transformation-guidance"></a>Sandkasten-Transformation ausgesprochen 
Transformieren oder Konvertieren von codebasierte sandkastenlösungen in der SharePoint-add-in-Objektmodell. Informationen Sie zu den Optionen und Strategien zum Konvertieren von vorhandener Code basierende Funktionen in SharePoint-add-in-Modell oder alternative Lösungen.

_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_

Sandkasten codebasierte Lösungen [als veraltet gekennzeichnet wurden](https://blogs.msdn.microsoft.com/sharepointdev/2014/01/14/deprecation-of-custom-code-in-sandboxed-solutions/) , wieder in 2014 und SharePoint online gestartet Upgradeprozess für diese Funktion vollständig zu entfernen. Codebasierte sandkastenlösungen sind auch in SharePoint 2013 und SharePoint 2016 veraltet.

Transformieren von Ihrer sandkastenlösungen auf die SharePoint umfasst-add-in-Objektmodell, Analysieren Ihrer vorhandenen Extensions, Entwerfen und entwickeln Ihre neue Add-in (s) für SharePoint, und klicken Sie dann testen und Bereitstellen Ihrer add-Ins in Ihrer produktionsumgebung. 

## <a name="what-is-a-code-based-sandbox-solution-in-sharepoint"></a>Was ist eine Sandbox codebasierte Lösung in SharePoint
<a name="sectionSection0"></a> Sandkastenlösungen sind Anpassung Pakete, die zum Bereitstellen von Anpassungen für SharePoint in der Ebene der Websitesammlung verwendet werden kann. Sandkasten-Lösung Code enthält, hat es in speziellen isolierten Prozess mit begrenzten Satz von APIs Zugriff auf SharePoint-Dienste und Inhalte ausgeführt wurde.

Es gibt zwei Arten von sandkastenlösungen
- Codebasierte sandkastenlösungen, die eine benutzerdefinierte Assembly im Paket enthalten.
- Deklarative sandkastenlösungen, die nur Xml enthalten basierend Konfigurationen und Verwandte Ressourcen 

Declarative (Xml basierende) sandkastenlösungen können weiter auf folgenden basierend auf ihren Anwendungsfall Typen unterteilt.
- Websitevorlage – generierte mithilfe der Funktion "Speichern Website als Vorlage" aus vorhandenen Websites
- Design-Paket – mithilfe des Entwurfs-Manager von Veröffentlichungswebsite generiert
- Benutzerdefinierte sandkastenlösungen - Beispiel für das branding von Anlagen in Visual Studio erstellten und enthalten keine Assemblys

Codebasierte sandkastenlösungen können weiter auf folgenden basierend auf die Anwendungsfälle Typen unterteilt werden. 
- Deklarative Sandkasten-Lösung mit leeren assembly
- Sandkasten-Lösung mit InfoPath-Formular mit code 
- Codebasierte sandkastenlösungen mit Anpassungen wie Webparts, Ereignisempfängern und/oder Featureempfänger
- Sandkastenlösungen mit benutzerdefinierte Workflowaktion

Wenn Sie beabsichtigen, aus der sandkastenlösungen verschoben werden, sollten Sie die funktionsfähig und geschäftlichen Anforderungen bestimmte Lösung bewerten und schließt die Richtung zukünftige Design auf die. 


## <a name="steps-to-perform-transformation"></a>Schritte zum Ausführen der XSL-transformation
<a name="sectionSection1"> </a>

Wenn Sie Ihre sandkastenlösungen auf das SharePoint-add-in-Objektmodell transformieren, um sicherzustellen, dass die Auswirkung auf die Benutzer minimal ist werden soll. Analysieren Sie, um zu Ihrer aktuellen sandkastenlösungen, und klicken Sie dann das neue Add-In für SharePoint an den Bedürfnissen des Unternehmens entwerfen. Es wird empfohlen, den folgenden Vorgang aus, um eine erfolgreiche Umstrukturierung sicherzustellen.


1. Bereitschaft. Erfahren Sie mehr über:
    
    - Die SharePoint-add-in-Modell, verschiedene Arten von add-ins und Hostingoptionen. Weitere Informationen finden Sie unter [Overview of add-ins für SharePoint](https://msdn.microsoft.com/library/office/fp179930.aspx) und [SharePoint-Muster und Methoden Anweisungen](https://msdn.microsoft.com/en-us/pnp_articles/office-365-development-patterns-and-practices-solution-guidance).

2. Bewertung der Lösung. Analysieren Sie die funktionalen und geschäftlichen Anforderungen durch: 
    
    - Identifizieren von bereitgestellt sandkastenlösungen in der aktuellen Umgebung für die Sie entweder können mithilfe der [SharePoint-Sandkasten-Lösung Scanner](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.SandBoxTool) ([video](https://www.youtube.com/watch?v=pK4p2mGYXpU)) oder [bestimmte Sandkasten Lösung Inventar Skript](https://github.com/SharePoint/PnP-Tools/tree/master/Scripts/SharePoint.Sandbox.ListSolutionsFromTenant). Die erste ist ein Tool bietet viele Optionen und eine ausführliche Bestandsaufnahme, die zweite ein PowerShell-Skript bietet Ihnen eine grundlegende Inventar. Beide Tools sind als open-Source von Plug & Play-SharePoint-Team bereitgestellt.
    
    - Überprüfen der Anforderungen für die Benutzer. Bitten Sie Ihren Benutzern zeigen, wie sie die vorhandenen sandkastenlösungen zu ihrer täglichen Arbeit verwenden.
    
    - Identifizieren, dokumentieren und neuen Funktionen zum Einschließen in das neue Add-In für SharePoint zu entwerfen. Erwägen Sie die Liste der neuen Funktion Anforderungen von den Benutzern für zusätzliche Hinweise überprüfen.
    
    - Identifizieren von nicht verwendeten Features, und stimmen mit den Benutzern die ausgelassen werden, diese Funktion vom neuen-add-in für SharePoint. 
    
    - Für jede bereitzustellende Lösung ermittelt, ob der ersetzen Sie ihn durch ein Add-In für SharePoint oder implementieren, die entweder mit einigen aus dem Feld Funktionen verwenden oder eine alternative Lösung verwenden.
    
3.  Planen der Lösung. Entwerfen Sie die neue Anwendung mit dem SharePoint-add-in-Modell basierend auf:
    
    - Die Anforderungen in Schritt 2 gesammelt werden.
    
    - Analyse der vorhandenen Code. Während der Codeanalyse, Sie sollten Teile des Codes, die gelöscht werden können (beispielsweise nicht mehr im Code verwendet wird, oder die Anforderungen geändert haben).
    
4. Entwickeln Sie und Testen Sie die SharePoint-add-in-Objektmodellversion der Anwendung. 
    
5. Das neue Add-in bereitstellen. 

## <a name="replacing-sandbox-solution-customizations"></a>Ersetzen Sandkasten-Lösung Anpassungen
<a name="sectionSection2"> </a>

Hier ist normalerweise Anpassungen, die in den sandkastenlösungen und potenzielle Transformationsoptionen enthalten sind. Wir suchen nach wegen, zum Hinzufügen von weiteren Informationen für die verschiedenen Anpassung, damit Sie reale Beispiele zu den Transformationsoptionen verwendet werden können. 

|**Anpassung**|**Transformationsoptionen für die**|
|:-----|:-----|
|Deklarative Lösung mit leeren assembly|<p>Sie können die Erstellung von Visual Studio-Lösung Projekteigenschaften Assembly steuern. Finden Sie unter following KB-Artikel für Detais - [Assemblyverweis aus der Sandkasten-Lösung in Visual Studio erstellten entfernen](https://support.microsoft.com/en-us/kb/3183084). </p> <p>**Wichtig:** , wenn Sie verwenden Sie den [SharePoint-Sandkasten-Lösung Scanner](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.SandBoxTool) die Scanausgabe listet welche Lösungen eine leere Assembly haben + das Tool erstellt Sandkasten-Lösungspakete für Sie aktualisiert in dem die Assembly verworfen wird. Anschließend können Sie einfach die vorhandenen Sandkasten-Lösung durch die aktualisierte ersetzen.</p> |
|InfoPath-Formular mit code|<p>Wenn Sie ein InfoPath-Formular aus dem InfoPath-Client, die Code enthält veröffentlicht haben, wird sie tatsächlich auf die SharePoint als Lösung Sandkasten veröffentlicht. Dies bedeutet, dass die Formularcode tatsächlich vom Sandkasten-Modul in SharePoint ausgeführt wird.</p> <p>Weg von der InfoPath-Formulare codebasierte hängt von der tatsächlichen Geschäftsfall verwenden. Es gibt mehrere verschiedene Optionen generiert benutzerdefinierte Benutzeroberfläche als Add-in- oder anderen Formular Techniken nutzen.</p><p>Weitere Informationen zu den Optionen über unsere [InfoPath Transformation Anleitungen Artikel](Sandbox-Solution-Transformation-Guidance-InfoPath.md) finden Sie</p>|
|Webpart|<p>Webparts sind normalerweise entweder zu Add-in konvertiert werden Teile oder sie mit vollständig Seite Clienttechnologien mithilfe von damit gewählte JavaScript einbetten Muster implementiert. </p><p>Siehe folgende Ressourcen für zusätzliche Informationen<lu><li>[Anpassen Ihrer SharePoint site-Benutzeroberfläche mithilfe von JavaScript](https://msdn.microsoft.com/en-us/pnp_articles/customize-your-sharepoint-site-ui-by-using-javascript)</li><li>[Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](https://msdn.microsoft.com/en-us/library/office/fp179921.aspx)</li><li>[Gewusst wie: Aktualisieren Sie Ihre SharePoint-Seiten über das Einbetten von JavaScript](https://channel9.msdn.com/blogs/OfficeDevPnP/JavaScript-embedding-demo)</li><li>[Schneidet websitesammlungsnavigation](https://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)</li></lu></p>|
|Visual-Webpart|<p>Visuelle Webparts werden als normale-Webparts auf ähnliche Weise transformiert. Auch ersetzt werden, da in der Sandkasten-Lösung müssen innerhalb der Assembly enthalten ist, müssen Benutzersteuerelement in visual-Webpart verwendet wird.</p>|
|Ereignisempfänger|<p>Ereignisempfänger können in vielen Fällen durch die remote-Ereignisempfänger implementiert ersetzt werden. Remote-Ereignisempfänger müssen jedoch in einigen-Plattform, in der Regel auf bestimmte vom Anbieter gehosteten-add-ins gehostet.</p><p>Siehe folgende Ressourcen für zusätzliche Informationen<lu><li>[Verwenden von remote-Ereignisempfänger in SharePoint](https://msdn.microsoft.com/en-us/pnp_articles/use-remote-event-receivers-in-sharepoint)</li><li>[Verwendung von remote-Ereignisempfänger für Ihre SharePoint-add-ins](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-use-remote-event-receivers-for-your-SharePoint-add-ins)</li></lu></p>|
|Featureempfänger|<p>In der Regel werden mit einem remote basierende API-Vorgang entspricht der Verwendung von CSOM oder REST zum Anwenden der erforderlichen Anpassung oder Konfiguration auf Websiteebene ersetzt. Wenn erforderliche API aus der remote-APIs (CSOM/REST) fehlt, melden Sie die Lücke mithilfe von [SharePoint-UserVoice](https://sharepoint.uservoice.com/).</p><p>Featureempfänger sind beispielsweise verwendet, um eine benutzerdefinierte Gestaltungsvorlage oder ein Design auf Website festgelegt werden, wenn sie aktiviert werden. Diese Art der Vorgänge kann auf einfache Weise mit Remote ersetzt je Lösungen im code oder [Plug & Play-PowerShell](https://github.com/SharePoint/PnP-PowerShell/blob/master/README.md)mithilfe der einfache Befehlen für steuernde Standortkonfiguration bietet.</p>|
|Benutzerdefinierte Workflowaktion|<p>Typische Code Migrationspfad für diese Art von Anpassungen wird entweder SharePoint 2013-Workflows mit Starten über alternative Lösung, wie Microsoft Flow oder mithilfe von Lösungen für Drittanbieter verschoben.</p>|

Wir interessieren sich für bestimmte Artikel auf der Transformation Techniken, die für bestimmte technische Szenarien hinzufügen. 

## <a name="removing-your-sandbox-code--from-your-site"></a>Entfernen des Sandkasten-Codes aus Ihrer Website
<a name="sectionSection3"></a> Wenn Sie Ihre vorhandenen Sandkasten-Lösung von Websites deaktivieren, alle Elemente oder Dateien, die mithilfe von deklarativer Optionen bereitgestellt nicht entfernt werden. Wenn Sie sandkastenlösungen einführen neuer codebasierte Webparts verwendet haben, werden diese Funktionen von den Websites deaktiviert. Dies bedeutet, die die Seiten in der Regel noch gerendert werden, damit keine direkte Endbenutzer Auswirkungen vorhanden ist, wenn Lösung, mit Ausnahme des Entfernens die Funktionalitäten codebasierte deaktiviert wird wie WebParts.

## <a name="how-will-support-of-code-based-sandbox-solution-be-removed-from-sharepoint-online"></a>Wie entfernt Support Sandkasten codebasierte Lösung aus SharePoint Online werden?
<a name="howremoved"></a> Unterstützung durch Deaktivieren codebasierte Vorgänge von Sandkasten-Lösung-basierte Code ausgeführt werden, entfernt werden. Dies bedeutet, dass Ihre sandkastenlösungen nicht explizit deaktivierten aus dem Lösungsspeicher werden, aber Grundlage Code nicht mehr ausgeführt wird. Sandkastenlösungen werden "verbleiben im aktiviert ' Status im Lösungskatalog. Features, die mithilfe von Sandkasten Lösungen werden nicht abrufen deaktiviert automatisch, was bedeutet dieser möglichen Code zur Deaktivierung des Features verknüpft ist oder deinstallieren Handler bereitgestellt werden nicht ausgeführt. 

Alle deklarative Definitionen in der Sandkasten-Lösung werden weiterhin arbeiten, nachdem diese Änderung in SharePoint Online angewendet werden soll. 

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Entfernen codebasierte Sandkastenlösungen in SharePoint Online](http://dev.office.com/blogs/removing-code-based-sandbox-solutions-in-sharepoint-online)

-  [Entfernen Sie Assemblyverweis aus der Sandkasten-Lösung in Visual Studio erstellten](https://support.microsoft.com/en-us/kb/3183084)

-  [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Erstellen von Add-Ins für SharePoint](https://msdn.microsoft.com/library/jj163230.aspx)
