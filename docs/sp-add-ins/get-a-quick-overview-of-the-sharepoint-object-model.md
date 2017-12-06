---
title: "Schnelle Übersicht über das SharePoint-Objektmodell"
description: "Einführung in die Inhaltshierarchie sowie die clientseitige Runtime und Batchverarbeitung"
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: eedec2c5116d1844ff0d2e052aa83a64b14a411e
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="get-a-quick-overview-of-the-sharepoint-object-model"></a>Schnelle Übersicht über das SharePoint-Objektmodell

Dies ist der vierte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von vom Anbieter gehosteten SharePoint-Add-Ins. Sie sollten sich zuerst mit [SharePoint Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut machen:

-  [Erste Schritte beim Erstellen von vom Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md)
-  [Übertragen des SharePoint-Aussehens und -Verhaltens auf Ihr vom Anbieter gehostetes Add-In](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
-  [Einfügen einer benutzerdefinierten Schaltfläche in das vom Anbieter gehostete Add-In](include-a-custom-button-in-the-provider-hosted-add-in.md)
 
> [!NOTE]
> Wenn Sie diese Reihe zu vom Anbieter gehosteten Add-Ins durchgearbeitet haben, können Sie das Thema mit einer Visual Studio-Lösung weiter vertiefen. Sie können auch das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei BeforeSharePointWriteOps.sln öffnen.

In diesem Artikel legen Sie eine kurze Pause vom Codieren ein, um einen schnellen Überblick über das SharePoint-Clientobjektmodell (CSOM) zu erhalten. Dieses Modell ist durch Referenzthemen, Vorgehensweisen und Codebeispiele ausführlich und gut in MSDN dokumentiert. In diesem Artikel können wir nur einen ganz kurzen Einblick liefern. Doch selbst eine sehr kurze Einführung wird bewirken, dass Ihnen ein Großteil des Codes dieser Reihe weitaus weniger rätselhaft erscheint. 

## <a name="content-hierarchy"></a>Inhaltshierarchie

Die folgende Tabelle zeigt die Hierarchie der Inhalte in SharePoint und deren Darstellung durch CSOM-Klassen. Alle Entitäten verfügen über untergeordnete Dateien.
 

|**Entität**|**Klasse**|**Bemerkungen**|
|:-----|:-----|:-----|
|Lokale SharePoint-Farm oder SharePoint Online-Abonnement (auch als Mandant bezeichnet)||Es gibt nur eingeschränkten programmgesteuerten Zugriff auf diese Ebene in CSOM. Es gibt z. B. keine Klasse „Farm" oder „Abonnements" oder „Mandant". (Das serverseitige SharePoint-Objektmodell, das in Add-Ins nicht verwendet werden kann, ermöglicht den programmgesteuerten Zugriff auf diese Entitäten.)|
|Websitesammlung|**Website**|Eine Sammlung von Websites, die hauptsächlich aus administrativen Gründen und zum Unterbringen von SharePoint-Komponenten wie firmenspezifischen Masterseiten oder benutzerdefinierten Sicherheitsgruppen gruppiert werden und für alle untergeordneten Websites angewendet werden können. Alle Websites gehören zu einer Websitesammlung.|
|Website|**Web**|Eine Reihe von Seiten und SharePoint-Komponenten, die Unterwebsites haben können.|
|Liste|**List**|Dokumentbibliotheken und andere Arten von Dateibibliotheken sind ebenfalls auf dieser Ebene. Eine Dokumentbibliothek ist eine besondere Art von Liste, in der jede Zeile ein angefügtes Dokument enthält und die anderen Spalten Daten über das Dokument sind, z. B. der Autor, wann es zuletzt bearbeitet wurde und wer es ausgecheckt hat. |
|Listenelement|**ListItem**|Eine Zeile in einer Liste, d. h. ein Listenelement mit bestimmten Werten in den Feldern der Zeile. Es hat auch einen Typ. Mehr dazu in der nächsten Zeile. |
|Listenelement|**Inhaltstyp**|Der Typ eines Listenelements. Diese werden von der Klasse **ContentType** dargestellt und sind im Wesentlichen eine Reihe von Spalten und Metadaten. Der einfachste Typ ist der integrierte **Item**-Inhaltstyp. Alle anderen Inhaltstypen werden von **Item** abgeleitet. SharePoint enthält viele integrierte Inhaltstypen, z. B. Ereignis und Ankündigung.  |
|Spalte|**Field**|Ein **Field**-Objekt enthält nicht nur Informationen zum zugrunde liegenden Datentyp, sondern auch Informationen darüber, wie die Daten formatiert und in Formularen gerendert werden, z. B. in Formularen zum Erstellen, Anzeigen und Bearbeiten bestimmter Listenelemente.|

Sie können benutzerdefinierte Listen, Inhaltstypen, Spaltentypen und Listenelemente programmgesteuert erstellen. 

Zusätzlich zum Inhalt ermöglicht das CSOM den Zugriff auf Benutzer, Gruppen, Rollen und Berechtigungen, Taxonomie, Suche und mehr.

<a name="CSOMBatching"> </a>
## <a name="client-side-runtime-and-batching"></a>Clientseitige Runtime und Batchverarbeitung

CSOM verwendet ein Batchverarbeitungssystem. Datenteile aus verwaltetem Code werden in XML-Code konvertiert und in einer einzelnen HTTP-Anforderung an den Server gesendet. Für jeden Befehl erfolgt ein entsprechender Serverobjektmodell-Aufruf, und der Server gibt eine Antwort an den Client im Format JavaScript Object Notation (JSON) zurück. 

SharePoint-Code auf einem Client beginnt mit dem Abrufen eines Clientkontextobjekts, das den aktuellen Anforderungskontext darstellt, einschließlich der Identität der SharePoint-Website (und ihrer übergeordneten Websitesammlung). Durch diesen Kontext können Sie Zugriff auf CSOM-Objekte erhalten. Im Folgenden ist die grundlegende Struktur abgebildet, die Sie immer wieder sehen werden. 

```C#
  using (var clientContext = spContext.CreateUserClientContextForSPHost())
  {
      // CRUD operation or query code goes here.

      clientContext.ExecuteQuery();
  }
```

Beachten Sie Folgendes bei diesem Code:

- Das `spContext`-Objekt ist vom Typ **SharePointContext** und in der Datei SharePointContext.cs (oder .vb) definiert, die von den Office Developer Tools für Visual Studio generiert wird. Diese Datei kann geändert werden, aber dies ist in den meisten Fällen nicht notwendig. Bei den meisten SharePoint-Add-In-Projekten funktionieren diese Datei und die Datei TokenHelper.cs (oder .vb), die ebenfalls von den Tools generiert wird, effektiv als Erweiterungen des CSOM.

- Das `clientContext`-Objekt ist der CSOM-Typ **ClientContext**.

- Die **ExecuteQuery**-Methode bündelt den CRUD-Vorgangscode in einer XML-Nachricht, die an den SharePoint-Server gesendet wird. Dort wird der Code in den entsprechenden serverseitige Modellobjektcode übertragen und ausgeführt.

Im vorherigen Artikel dieser Reihe war ein Beispiel dieses Musters in der gezeigten Methode `GetLocalEmployeeName` dargestellt. 

```C#
private string GetLocalEmployeeName()
{
    ListItem localEmployee;

    using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        List localEmployeesList = clientContext.Web.Lists.GetByTitle("Local Employees");
        selectedLocalEmployee = localEmployeesList.GetItemById(listItemID);
        clientContext.Load(selectedLocalEmployee);
        clientContext.ExecuteQuery();
    }
    return localEmployee["Title"].ToString();
}
```

Beachten Sie Folgendes zu dieser Methode:

- Die ersten beiden Zeilen im **using**-Block scheinen Verweise auf die Liste und das Listenelementobjekt abzurufen. Aber tatsächlich werden diese Zeilen, wenn sie in der clientseitigen SharePoint-Laufzeit ausgeführt werden, einfach in ein XML-Format übersetzt. Die Methode **ExecuteQuery** sendet diese XML an den Server.

-  Mit der **Laden**-Methode wird etwas zur der Nachricht hinzugefügt: Dem Server wird aufgetragen, das angegebene Objekt auf den Client zu übertragen. Die **ExecuteQuery**-Methode empfängt dieses Objekt (als JSON) und verwendet es, um die clientseitige Variable `selectedLocalEmployee` zu initialisieren. Nachfolgender clientseitiger Code verweist dann auf dieses **ListItem**-Objekt und seine Elemente. Wie Sie sehen, verweist die nächste Zeile auf den Wert des Feldes `"Title"` des Elements. Diese Zeile würde eine Ausnahme auslösen, wenn die **Laden**-Methode nicht aufgerufen worden wäre, da das Objekt erst auf der Clientseite vorhanden ist, nachdem es geladen wurde.
 
## <a name="next-steps"></a>Nächste Schritte
<a name="Nextsteps"> </a>

Im nächsten Artikel kehren wir zum Programmieren zurück, und Sie erfahren, wie Sie [SharePoint-Schreibvorgänge zum einem vom Anbieter gehosteten Add-In hinzufügen](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md).
 

 

