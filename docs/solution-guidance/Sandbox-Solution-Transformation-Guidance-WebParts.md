---
title: Sandkasten-Transformation ausgesprochen - Webparts
ms.date: 11/03/2017
ms.openlocfilehash: e15cc7d7677019b3f60e75a2dd6a81398c0d5db1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sandbox-solution-transformation-guidance---web-parts"></a>Sandkasten-Transformation ausgesprochen - Webparts
Transformieren oder Konvertieren von codebasierte sandkastenlösungen in der SharePoint-add-in-Objektmodell. Hier erfahren Sie, über die Optionen und Strategien für die vorhandenen Funktionalität in SharePoint-add-in-Modell oder alternative Lösungen zu konvertieren.

_**Gilt für:** Add-ins für SharePoint | SharePoint 2013 | SharePoint-2016 | SharePoint Online_


## <a name="summary"></a>Summary

Einer der Gründe, dass viele Entwickler codebasierte sandkastenlösungen genutzt haben ist Wunsch visuelle Webparts nutzen. Dies bietet eine hervorragende Möglichkeit zum Trennen von Code aus Layout als auch ASP.net-Steuerelemente verwenden. Sie können natürlich auch weiterhin mithilfe visuelle Webparts in einer vom Anbieter gehosteten-add-in über die Client-WebParts. Dies ist ein hervorragendes Ansatz und bietet einen direkte Migrationspfad für viele Clientanwendungen.

Eine andere Methode ist das Webpart als Client Side Lösung neu zu schreiben. Dies planungslösung Neuentwurf der Lösung, um JavaScript, HTML-Fragmente verwenden und eine oder mehrere Frameworks unterstützen. Obwohl dies Net neue Arbeit ist, hat sie den Vorteil Einrichten Ihrer Lösung, die einfache Integration in die in Kürze verfügbare SharePoint-Framework. Dies ist eine gute Wahl für einfache Anzeige- oder Daten Eintrag Webparts und Clientanwendungen ganze Seite skalieren kann.


## <a name="options-for-replacing-web-parts"></a>Optionen für den Austausch von Webparts
<a name="sectionSection2"> </a>

|**Ansatz**|**Weitere Informationen**|
|:-----|:-----|
|Vom Anbieter gehosteten Add-in-Client-Webpart|<ul><li>[Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/fp142381.aspx)</li><li>[Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](https://msdn.microsoft.com/en-us/library/a2664289-6c56-4cb1-987a-22367fad55eb)</li><li>[Client Webpart-Definitionsschema](https://msdn.microsoft.com/en-us/library/office/dn481208.aspx)</li><li>[Einrichten einer lokalen Entwicklungsumgebung für SharePoint-Add-Ins](https://msdn.microsoft.com/en-us/library/office/fp179923.aspx)</li></ul>|
|Client-Side-Lösung|<ul><li>[Beispiel für einfache reagieren Formular](https://github.com/SharePoint/PnP/tree/dev/Samples/SharePoint.React.SupportTicket)</li><li>[Einbetten von Beispiele JavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScript)[*](#actionsupportnote)</li><li>[Muster und Methoden JS-Core](https://github.com/SharePoint/PnP-JS-Core/)</li></ul>|


## <a name="design-considerations"></a>Entwurfsaspekte

### <a name="provider-hosted-add-in"></a>Vom Anbieter gehosteten-Add-Ins

<ul>
<li>Erfordert Hostinginfrastruktur ab</li>
<li>Hosting-Infrastruktur muss hoch verfügbar sein.</li>
<li>Client-Webpart wird in einem Iframe Beschränken der Kommunikation mit dem Rest der Seite angezeigt.</li>
<li>Remote-APIs entweder über CSOM oder REST muss verwendet werden.</li>
</ul>

### <a name="client-side-solution"></a>Client-Side-Lösung

<ul>
<li>
<a name="actionsupportnote"></a>Bitte beachten Sie, dass die Möglichkeit zum Einbetten von JavaScript in der vorgeschriebenen Weise (über eine UserCustomAction) derzeit nicht außerhalb der klassische Erfahrung funktioniert. In diesen Fällen können Sie die Dateien mit einem Skript-Editor-Webpart Verknüpfung herstellen.</li>
<li>Berechtigungen zu erhöhen, verwenden Sie einen Micro-Dienst stattdessen Add-in-Berechtigungen ist nicht möglich</li>
<li>Abhängig von der Berechtigungen des aktuellen Benutzers</li>
</ul>


## <a name="removing-your-sandbox-code-from-your-site"></a>Entfernen des Sandkasten-Codes aus Ihrer Website
<a name="sectionSection3"></a> Wenn Sie Ihre vorhandenen Sandkasten-Lösung aus Ihrer Websites deaktivieren, alle Elemente oder Dateien, die mithilfe von deklarativer Optionen bereitgestellt werden nicht jedoch entfernt werden, die Features in der Sandkasten-Projektmappe werden automatisch deaktiviert und der Ereignisempfänger werden entfernt.


## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>
-  [Entfernen codebasierte Sandkastenlösungen in SharePoint Online](http://dev.office.com/blogs/removing-code-based-sandbox-solutions-in-sharepoint-online)
-  [Hilfestellung zur Transformation von Sandkastenlösungen](https://msdn.microsoft.com/en-us/pnp_articles/sandbox-solution-transformation-guidance)
-  [Entfernen Sie Assemblyverweis aus der Sandkasten-Lösung in Visual Studio erstellten](https://support.microsoft.com/en-us/kb/3183084)
-  [Erstellen von Add-Ins für SharePoint](https://msdn.microsoft.com/library/office/fp179930.aspx)
-  [Office 365-Entwicklung und SharePoint Mustern und Methoden ausgesprochen](https://msdn.microsoft.com/en-us/pnp_articles/office-365-development-patterns-and-practices-solution-guidance)
