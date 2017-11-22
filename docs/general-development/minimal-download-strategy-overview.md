---
title: "Minimale Downloadstrategie – Übersicht"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 9aafff627fcc47dbb8bbd4402585669dd6ef5bae
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="minimal-download-strategy-overview"></a>Minimale Downloadstrategie – Übersicht
Erfahren Sie mehr über minimale herunterladen Strategie (MDS), ein neues Feature in SharePoint, die Ladezeit der Seite durch Senden nur die Unterschiede beim Benutzer navigieren zu einer neuen Seite reduziert. Minimale herunterladen Strategie (MDS) ist eine neue Technologie in SharePoint, die die Menge der Daten, die im Browser herunter verringert, wenn Benutzer von einer Seite in eine andere in einer SharePoint Website navigieren. Wenn Benutzer eine MDS-fähigen Website navigieren, verarbeitet der Client nur die Unterschiede (oder Delta) zwischen der aktuellen Seite und die angeforderte Seite. Abbildung 1 zeigt, dass die Abschnitte, die von einer Seite zum und deshalb ändern ein Update erforderlich. Das Delta umfasst in der Regel die Daten in den Abschnitten (1) Inhalte sowie andere Komponenten wie Navigationssteuerelemente (2).
  
    
    


**Abbildung 1. Seite verarbeitet mit MDS**

  
    
    

  
    
    
![Mit MDS bearbeitete Seite](../images/MDS_UpdateSections.png)
  
    
    
Sie können anhand der URL erkennen, ob MDS für eine Website aktiviert ist. Bei einer MDS-fähigen Website ist die Seite **_layouts/15/start.aspx** (3) Teil der URL, gefolgt von einem Hashzeichen (**#**) und der relativen URL der angeforderten Ressource (siehe Abbildung 1). Die MDS-formatierte URL für die Seite **newpage.aspx** beispielsweise würde wie folgt aussehen: **https://sp_site/_layouts/15/start.aspx#/SitePages/newpage.aspx**. Diese URL ist äquivalent zur folgenden URL ohne MDS-Formatierung: **https://sp_site/SitePages/newpage.aspx**. Entwickler müssen einige ihrer SharePoint-Komponenten möglicherweise zunächst aktualisieren, bevor sie MDS nahtlos unterstützen. 
## <a name="enable-mds"></a>Aktivieren von MDS
<a name="SP15MDSOverview_Enable"> </a>

MDS können in Ihrer Website Sie mithilfe der Websiteverwaltungsseiten oder die SharePoint Clientobjektmodelle.
  
    
    
Wenn Sie MDS über die Verwaltungsseiten aktivieren möchten: Klicken Sie auf **Websiteeinstellungen** > **Websitefeatures verwalten**, und aktivieren Sie das Feature **Minimal Download Strategy**.
  
    
    
Da das Feature aktiviert ist, indem Sie die  [EnableMinimalDownload](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Web.EnableMinimalDownload.aspx) -Eigenschaft ändern, können Sie auch den Client-APIs. Der folgende Code zeigt, wie MDS mit dem JavaScript-Objektmodell (JSOM) zu aktivieren.
  
    
    



```

var clientContext;

clientContext = new SP.ClientContext.get_current();
this.oWebsite = clientContext.get_web();

this.oWebsite.set_enableMinimalDownload(true);
this.oWebsite.update();

clientContext.load(this.oWebsite);

clientContext.executeQueryAsync(
    Function.createDelegate(this, successHandler),
    Function.createDelegate(this, errorHandler)
);

function successHandler() {
    alert("MDS is enabled in this site.");
}

function errorHandler() {
    alert("Request failed: " + arguments[1].get_message());
}
```


## <a name="benefits-of-using-mds"></a>Vorteile der Verwendung von MDS
<a name="SP15MDSOverview_Benefits"> </a>

Mit MDS bietet verschiedene Vorteile, einschließlich:
  
    
    

- **Geschwindigkeit:** Dies ist das wichtigste Ziel der MDS. Bei Verwendung von MDS keinen Browser die Chrome-Benutzeroberfläche (UI) zu verarbeiten. MDS wird auch im Vergleich zu einer Auslastung vollständige Seite Nutzlast reduziert.
    
  
- **Fließende Übergänge:** Durch die Aktualisierung nur die Bereiche, die sich ändern, zeichnen Sie Auge des Benutzers in Richtung dieser Bereiche, im Gegensatz zu einer ganzseitigen laden, in die gesamte Seite "blinkt." Wenn die gesamte Seite aktualisiert wird, muss der Benutzer analysieren in seiner Gesamtheit um Neuigkeiten zu erkennen. Benutzer haben erleichtern Navigieren in einer Website, die nur die Bereiche aktualisiert, die von der vorherigen Seite geändert.
    
  
- **Navigationssteuerelemente Browser:** Andere AJAX-basierte Systeme Verwechseln Sie die **vorherigen** und **nächsten** Schaltflächen im Browser. Da die URL im Browserfenster MDS aktualisiert werden, funktionieren die Schaltflächen vorherigen und nächsten wie jedoch.
    
  
- **Abwärtskompatibilität:** Das Modul MDS MDS Navigation unmittelbar enthält, oder erkennt, wenn es nicht möglich. In der Fall, in dem MDS Navigation nicht möglich, tritt eine ganze Seite Last stattdessen. Dieser Prozess wird als **Failover** bezeichnet, und es wird sichergestellt, dass alle Seiten ordnungsgemäß gerendert wird, unabhängig davon, ob sie MDS-kompatible Komponenten enthalten. MDS funktioniert auch gut mit Suchmaschinen, da das **Href** -Attribut des Ankertags die URLs regulären, nicht MDS-Format verwendet. Das Modul MDS im Client stattdessen zeichnet das **Onclick** -Ereignis auf und wird verwendet, um eine Kommunikation mit dem Server.
    
  

## <a name="mds-architecture"></a>MDS-Architektur
<a name="SP15MDSOverview_Architecture"> </a>

Die grundlegende Funktionsweise der MDS sind relativ einfach. Die wichtigsten Komponenten der MDS sind zwei Module, eine auf dem Server und eine im-Client, die zusammenarbeiten, um die Änderungen zu berechnen, und die Seiten im Browser gerendert werden, wenn der Benutzer von einer Seite auf der Website navigiert. Abbildung 2 zeigt den MDS-Ablauf, wenn ein Benutzer über ein MDS-fähigen Website navigiert.
  
    
    

**Abbildung 2. MDS-Ablauf, wenn ein Benutzer die Website navigiert**

  
    
    

  
    
    
![MDS-Ablauf, wenn ein Benutzer durch die Website navigiert](../images/MDS_GeneralFlow.png)
  
    
    

  
    
    

1. Der Browser fordert die Unterschiede zwischen der aktuellen Seite und eine neue auf der Website SharePoint.
    
  
2. Das Modul MDS auf dem Server berechnet das Delta zwischen dem aktuellen und die neuen Seiten.
    
  
3. MDS-Modul auf dem Server sendet das Delta an das Modul MDS im-Client.
    
  
4. Das Modul MDS im Client ersetzt die geänderten Bereiche auf der aktuellen Seite mit den Inhalt der neuen Seite.
    
  
Die resultierende Seite ist genau, wie es hätte die Seite ohne MDS heruntergeladen wurde, hatte.
  
    
    
Das Modul MDS im-Client enthält einen Download-Manager. Alle Anfragen auf der Seite werden durch die Download-Manager weitergeleitet. Alle Steuerelemente auf der Seite müssen Abonnieren der Download-Manager, um sich zu informieren, wenn eine URL geändert hat. Der Download-Manager sendet eine Anforderung für den neuen Steuerelementdaten. Um Suchmaschinen entwickelt werden, verwenden nicht das Modul MDS direkt das **href** -Attribut des Ankertags, um URLs MDS-Format speichern. Stattdessen wird die Funktion **SPUpdatePage** behandelt das **onclick** -Ereignis und wird verwendet, um eine Kommunikation mit dem Server. Die **SPUpdatePage** -Funktion ist in der Datei **_layouts/15/start.js** deklariert.
  
    
    
Das Modul MDS auf dem Server sendet die Informationen an den Client zurück. Diese Informationen kann HTML mit eingebetteten Skripts und Formatvorlagen, XML oder JavaScript Object Notation (JSON) enthalten.
  
    
    
Die URL spielt eine wichtige Rolle in MDS. Eine URL MDS sieht folgendermaßen aus: **https://sp_site/_layouts/15/start.aspx#/SitePages/newpage.aspx**. **Start.aspx** enthält minimale freigegebenen Benutzeroberfläche und Anweisungen zum Laden der Seite geändert wird. MDS berücksichtigt das Webpart nach der Hashmarkierung (#) als Zielseite. Die Zielseite beginnt mit einem Schrägstrich (/) gefolgt von der URL relativ zu der Website SharePoint. Wenn im Browser die URL erhält, sieht es, dass das Webpart links neben der Hashmarkierung nicht geändert werden, damit es eine lokale Navigationsereignis wird ausgelöst. Das Modul MDS im Client zeichnet das lokale Navigationsereignis und wird verwendet, um ein MDS Update ausführen.
  
    
    
Wie zuvor in diesem Artikel erwähnt, ist in manchen Fällen es nicht möglich, zu bestimmen, ob die Seite ordnungsgemäß aktualisiert werden kann. In den folgenden Situationen gibt das Modul MDS ein **Failover**, der ein zusätzlicher Roundtrip zum Umleiten von im Browsers auf die Vollversion der neuen Seite besteht. Dies sind die häufigsten Gründe, warum Failover auftritt:
  
    
    

- Die neue Seite verfügt über eine andere Gestaltungsvorlage.
    
  
- Die aktuelle Gestaltungsvorlage wurde geändert.
    
  
- Das Modul MDS erkennt nicht kompatible HTML, beispielsweise:
    
  - Seiten mit ASP.NET 2.0
    
  
  - CSS oder Skripts, die in das Modul MDS nicht registriert
    
  
  - Unzulässige HTML
    
  
- Es gibt beispielsweise nicht kompatible Steuerelemente auf der Seite:
    
  - Das Steuerelement ist nicht in der weißen Liste MDS-Modul.
    
  
  - Die Assembly des Steuerelements wird nicht als kompatibel markiert.
    
  
  - Die Steuerelementklasse keinen MDS-Attribut.
    
  
Das Modul MDS versucht, die von einem Failover wiederhergestellt werden, nachdem der Benutzer noch eine andere neue Seite navigiert.
  
    
    

## <a name="developer-controls"></a>Entwickler-Steuerelemente
<a name="SP15MDSOverview_DevControls"> </a>

Dank der Failovermechanismus nahtlos Steuerelemente unabhängig davon, ob MDS in Ihrer Benutzer Websites aktiviert ist. Jedoch ist es ratsam, Ihre SharePoint Steuerelemente und Komponenten MDS vollständig nutzen zu aktualisieren. Benutzer erhalten optimal, wenn die Seiten und Steuerelemente MDS kompatibel sind. Die folgenden Komponenten sind gute Kandidaten für MDS optimiert abrufen:
  
    
    

- Gestaltungsvorlagen
    
  
- ASP.NET-Seiten
    
  
- Steuerelemente und Webparts
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [EnableMinimalDownload](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Web.EnableMinimalDownload.aspx)
    
  
-  [Ändern von SharePoint-Komponenten für MDS](modify-sharepoint-components-for-mds.md)
    
  
-  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint.md)
    
  

