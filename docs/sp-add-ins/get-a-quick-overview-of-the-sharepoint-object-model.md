---
title: "Schnelle Übersicht über das SharePoint-Objektmodell"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: c703d0edf04b77313d6a7276df4e444dee2250cf
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="get-a-quick-overview-of-the-sharepoint-object-model"></a>Schnelle Übersicht über das SharePoint-Objektmodell
Hier erhalten Sie eine kurze Einführung in einige der wichtigsten Klassen im SharePoint-Objektmodell.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 

Dies ist der vierte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von vom Anbieter gehosteten SharePoint-Add-Ins. Sie sollten sich zuerst mit [SharePoint Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut machen:
 

-  [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
-  [Übertragen des SharePoint-Aussehens und -Verhaltens auf Ihr vom Anbieter gehostetes Add-In](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
    
 
-  [Einfügen einer benutzerdefinierten Schaltfläche in das vom Anbieter gehostete Add-In](include-a-custom-button-in-the-provider-hosted-add-in.md)
    
 

 **Hinweis** Wenn Sie diese Reihe zu vom Anbieter gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei „BeforeSharePointWriteOps.sln“ öffnen.
 

In diesem Artikel unterbrechen wir die Programmierung kurz, um einen schnellen Überblick über das clientseitige SharePoint-Objektmodell (CSOM) bereitzustellen. Dieses Modell ist umfassend und gut mit Referenzthemen, „Gewusst wie"-Artikeln und Codebeispielen in MSDN dokumentiert. In diesem Artikel können wir nur die alleroberste Spitze des Eisbergs darstellen. Aber selbst eine sehr kurze Einführung wird einen Großteil des Codes, den Sie in dieser Reihe sehen, viel weniger mysteriös erscheinen lassen. 
 

## <a name="content-hierarchy"></a>Inhaltshierarchie

In der folgenden Tabelle finden Sie die Hierarchie von Inhalten in SharePoint und die CSOM-Klassen, die diese Inhalte darstellen. Jede dieser Entitäten verfügt über untergeordnete Elemente des Typs direkt darunter.
 

|**Entität**|**Klasse**|**Bemerkungen**|
|:-----|:-----|:-----|
|Lokale SharePoint-Farm oder SharePoint Online-Abonnement (auch als Mandant bezeichnet)||Es gibt nur eingeschränkten programmgesteuerten Zugriff auf diese Ebene in CSOM. Es gibt z. B. keine Klasse „Farm" oder „Abonnements" oder „Mandant". (Das serverseitige SharePoint-Objektmodell, das in Add-Ins nicht verwendet werden kann, ermöglicht den programmgesteuerten Zugriff auf diese Entitäten.)|
|Websitesammlung|**Site**|Eine Sammlung von Websites, die hauptsächlich aus administrativen Gründen und zum Unterbringen von SharePoint-Komponenten wie firmenspezifischen Masterseiten oder benutzerdefinierten Sicherheitsgruppen gruppiert werden und für alle untergeordneten Websites angewendet werden können. Alle Websites gehören zu irgendeiner Websitesammlung.|
|Website|**Web**|Eine Reihe von Seiten und SharePoint-Komponenten, die Unterwebsites haben können.|
|Liste|**List**|Dokumentbibliotheken und andere Arten von Dateibibliotheken sind ebenfalls auf dieser Ebene. Eine Dokumentbibliothek ist eine besondere Art von Liste, in der jede Zeile ein angefügtes Dokument enthält und die anderen Spalten Daten über das Dokument sind, z. B. der Autor, wann es zuletzt bearbeitet wurde und wer es ausgecheckt hat. |
|Listenelement|**ListItem**|Eine Zeile in einer Liste, d. h. ein Listenelement mit bestimmten Werten in den Feldern der Zeile. Es hat auch einen Typ. Mehr dazu in der nächsten Zeile. |
|Listenelement|**Inhaltstyp**|Der Typ eines Listenelements. Diese werden von der Klasse **ContentType** dargestellt und sind im Wesentlichen eine Reihe von Spalten und Metadaten. Der einfachste Typ ist der integrierte **Item**-Inhaltstyp. Alle anderen Inhaltstypen werden von **Item** abgeleitet. SharePoint enthält viele integrierte Inhaltstypen, z. B. Ereignis und Ankündigung.  |
|Spalte|**Field**|Ein **Field**-Objekt enthält nicht nur Informationen zum zugrunde liegenden Datentyp, sondern auch Informationen darüber, wie die Daten formatiert und in Formularen gerendert werden, z. B. in Formularen zum Erstellen, Anzeigen und Bearbeiten bestimmter Listenelemente.|

 

 
Sie können benutzerdefinierte Listen, Inhaltstypen, Spaltentypen und Listenelemente programmgesteuert erstellen. 
 

 
Zusätzlich zum Inhalt ermöglicht das CSOM den Zugriff auf Benutzer, Gruppen, Rollen &amp; Berechtigungen, Taxonomie, Suche und mehr.
 

 

## <a name="client-side-runtime-and-batching"></a>Clientseitige Laufzeit und Batchverarbeitung
<a name="CSOMBatching"> </a>

CSOM verwendet ein Batchverarbeitungssystem. Abschnitte von verwaltetem Code werden in XML konvertiert und in einer einzigen HTTP-Anforderung an den Server gesendet. Für jeden Befehl erfolgt ein entsprechender Serverobjektmodell-Aufruf, und der Server gibt eine Antwort an den Client imb JSON-Format (JavaScript Object Notation) zurück. 
 

 
SharePoint-Code auf einem Client beginnt mit dem Abrufen eines Clientkontextobjekts, das den aktuellen Anforderungskontext darstellt, einschließlich der Identität der SharePoint-Website (und ihrer übergeordneten Websitesammlung). Durch diesen Kontext können Zugriff auf CSOM-Objekte erhalten. Im Folgenden ist die grundlegende Struktur gezeigt, die Sie immer wieder sehen werden. Beachten Sie Folgendes bei diesem Code:
 

 

- Das Objekt  `spContext` ist vom Typ **SharePointContext** und wird in einer SharePointContext.cs-Datei (oder. vb) definiert, die von Office-Entwicklertools für Visual Studio generiert wird. Diese Datei kann geändert werden, dies ist aber nicht häufig erforderlich. Für die meisten SharePoint-Add-In-Projekte, fungieren diese und die TokenHelper.cs-Datei (oder .vb), die ebenfalls von den Tools generiert wird, effektiv als Erweiterungen von CSOM selbst.
    
 
- Das `clientContext`-Objekt ist der CSOM-Typ **ClientContext**.
    
 
- Die Methode **ExecuteQuery** bündelt den CRUD-Vorgangscode in einer XML-Nachricht, die an den SharePoint-Server gesendet wird. Dort wird sie in entsprechenden serverseitigen Objektmodellcode übersetzt und ausgeführt.
    
 



```C#
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    // CRUD operation or query code goes here.

    clientContext.ExecuteQuery();
}
```

Im vorherigen Artikel dieser Reihe war ein Beispiel dieses Musters in der unten gezeigten Methode  `GetLocalEmployeeName` dargestellt. Beachten Sie Folgendes zu dieser Methode:
 

 

- Die ersten beiden Zeilen im **using**-Block scheinen Verweise auf die Liste und das Listenelementobjekt abzurufen. Aber tatsächlich werden diese Zeilen, wenn sie in der clientseitigen SharePoint-Laufzeit ausgeführt werden, einfach in ein XML-Format übersetzt. Die Methode **ExecuteQuery** sendet diesen XML-Code an den Server.
    
 
-  Die Methode **Load** fügt zusätzlich etwas in die Nachricht ein: Sie teilt dem Server mit, das angegebene Objekt an den Client zu senden. Die Methode **ExecuteQuery** empfängt dieses Objekt (als JSON) und verwendet es, um die clientseitige Variable `selectedLocalEmployee` zu initialisieren. Nachfolgender clientseitiger Code verweist dann auf dieses **ListItem**-Objekt und dessen Member. Wie Sie sehen können, verweist die nächste Zeile auf den Wert des Felds „Titel" für das Element. Diese Zeile hätte eine Ausnahme ausgelöst, wenn die Methode **Load** nicht aufgerufen worden wäre, da das Objekt nicht wirklich auf der Clientseite vorhanden ist, bis es geladen wird.
    
 



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


## 
<a name="Nextsteps"> </a>

 Im nächsten Artikel kehren wir zum Programmieren zurück, und Sie erfahren, wie Sie Daten an SharePoint schreiben: [Hinzufügen von SharePoint-Schreibvorgängen zum vom Anbieter gehosteten Add-In](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)
 

 

