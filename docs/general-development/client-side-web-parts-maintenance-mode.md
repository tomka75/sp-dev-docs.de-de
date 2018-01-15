---
title: "Wartungsmodus für clientseitige Webparts"
ms.date: 12/18/2017
ms.prod: sharepoint
ms.assetid: 3ebd2a11-8291-4228-add0-9e0cd899dd3c
ms.openlocfilehash: 208a9ef5fea879fa7d27811595ebc8d37881d3b2
ms.sourcegitcommit: 31f793b42ec75679f01e1a024d0375a2bc7b5ec7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2017
---
# <a name="maintenance-mode-for-client-side-web-parts"></a>Wartungsmodus für clientseitige Webparts

_**Gilt für:** Office 365_

Wenn Sie mit clientseitigen Webparts arbeiten, können Sie diese im Wartungsmodus laden. Der Wartungsmodus kann hilfreich sein, wenn Sie versuchen, Probleme im Zusammenhang mit Webparts auf der Seite zu debuggen.

## <a name="switch-to-maintenance-mode"></a>Wechseln in den Wartungsmodus

> [!NOTE]
> Um eine Seite im Wartungsmodus zu laden, benötigen Sie Bearbeitungsberechtigungen für diese spezielle Seite.

Navigieren Sie zu der Seite, und fügen Sie in der URL `?maintenancemode=true` an, um zum Wartungsmodus zu wechseln. Zum Beispiel:

```text
https://contoso.sharepoint.com/sites/team?maintenancemode=true
```

Um den Wartungsmodus zu verlassen, entfernen Sie `?maintenancemode=true` aus der URL, und laden Sie die Seite erneut.

## <a name="available-information"></a>Verfügbare Informationen

Im Wartungsmodus werden unterschiedliche Informationen zu jedem Webpart auf der Seite angezeigt.

### <a name="web-part-summary"></a>Webpart-Zusammenfassung

Wenn Sie sich im Wartungsmodus befinden, wird für jedes Webpart die folgende Zusammenfassung angezeigt:

![Zusammenfassende Webpartinformationen, die im Wartungsmodus angezeigt werden](../images/maintenance-mode-summary.png)

Eigenschaft|Beschreibung
--------|-----------
Alias|Webpart-Alias
Id|Die eindeutige ID des Webparts.
InstanceID|Die ID einer bestimmten Instanz eines Webparts (wenn auf einer Seite zwei oder mehr gleiche Webparts vorhanden sind, weisen diese jeweils dieselbe Webpart-ID auf, haben jedoch eine andere Instanz-ID).
IsInternal|Gibt an, ob das Webpart von Microsoft oder von einem Drittanbieter erstellt wurde. Bei `true` wurde das Webpart von Microsoft erstellt. Bei `false` wurde das Webpart von einem Drittanbieter erstellt.
Version|Die Versionsnummer des Webparts.
Umgebung|Eine Aufzählung, die die Umgebung angibt, in der das Webpart ausgeführt wird. Mögliche Werte: `1` - Lokale Workbench, `2` - SharePoint
UserAgent|Eine Zeichenfolge, die Informationen zu dem verwendeten Gerät und zu der verwendeten Software enthält (z. B. Browsertyp und Version).

### <a name="web-part-manifest"></a>Webpart-Manifest

Wechseln Sie zur Registerkarte **Manifest**, um weitere Informationen zu dem Webpart zu erhalten.

![Webpart-Manifestinformationen, die im Wartungsmodus angezeigt werden](../images/maintenance-mode-manifest.png)

Wenn Sie sich die Manifestinformationen näher ansehen, erhalten Sie Details über Folgendes:

- Wo das Webpart-Bundle gehostet wird.
- Welche externen Skripts das Webpart lädt und von wo.
- Auf welcher Version von SharePoint Framework das Webpart basiert.
- Welche Komponenten von SharePoint Framework das Webpart verwendet.

Diese Informationen können hilfreich sein, wenn Sie herausfinden möchten, warum ein bestimmtes Webpart nicht funktioniert.

### <a name="web-part-data"></a>Webpartdaten

Weitere Angaben, die im Wartungsmodus verfügbar sind, sind die Webpartdaten.

![Webpartdaten, die im Wartungsmodus angezeigt werden](../images/maintenance-mode-data.png)

Anhand der Informationen der Registerkarte **Daten** können Sie die Konfiguration jedes Webparts ermitteln. Dies ist hilfreich, wenn Sie versuchen, Fehler zu reproduzieren, die von Benutzern gemeldet wurden, die von der Konfiguration eines bestimmten Webparts verursacht worden sein könnten.

Wenn [die Eigenschaften des Webparts in SharePoint integriert sind](../spfx/web-parts/guidance/integrate-web-part-properties-with-sharepoint.md), werden im Datenabschnitt die Typen und Werte angezeigt, die zur weiteren Verarbeitung an SharePoint übergeben werden.

## <a name="considerations"></a>Überlegungen

- Der Wartungsmodus eignet sich für clientseitige Webparts  auf modernen und klassischen SharePoint-Seiten. Im Supportartikel [Öffnen und Verwenden der Webpart-Wartungsseite]((https://support.office.com/de-DE/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2)#PickTab=2016,_2013) erhalten Sie weitere Informationen zum Öffnen von klassischen Webparts in der Wartungsansicht.
- Um eine Seite im Wartungsmodus zu öffnen, benötigen Sie Bearbeitungsberechtigungen für diese spezielle Seite.
- Während Sie sich im Wartungsmodus befinden, wird der Code des Webparts nicht ausgeführt, und die Webparteigenschaften können nicht bearbeitet werden.
- Im Wartungsmodus können Sie Webparts auf der Seite löschen oder verschieben.
- Im Wartungsmodus werden nur Informationen zu Webparts angezeigt. Sie können ihn nicht verwenden, um Informationen zu SharePoint Framework-Erweiterungen anzuzeigen, die auf der Seite ausgeführt werden.
- Durch Wechseln in den Wartungsmodus wird nur das Ausführen des Webpartcodes deaktiviert. Alle SharePoint Framework-Erweiterungen, die auf der Seite registriert sind, werden weiterhin ausgeführt.

## <a name="see-also"></a>Siehe auch

- [Öffnen und Verwenden der Webpart-Wartungsseite]((https://support.office.com/de-DE/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2))