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
# <a name="get-a-quick-overview-of-the-sharepoint-object-model"></a><span data-ttu-id="db123-102">Schnelle Übersicht über das SharePoint-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="db123-102">Get a quick overview of the SharePoint object model</span></span>
<span data-ttu-id="db123-103">Hier erhalten Sie eine kurze Einführung in einige der wichtigsten Klassen im SharePoint-Objektmodell.</span><span class="sxs-lookup"><span data-stu-id="db123-103">Get a quick introduction to some of the major classes in the SharePoint object model.</span></span>
 

 <span data-ttu-id="db123-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="db123-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="db123-107">Dies ist der vierte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von vom Anbieter gehosteten SharePoint-Add-Ins. Sie sollten sich zuerst mit [SharePoint Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut machen:</span><span class="sxs-lookup"><span data-stu-id="db123-107">This is the fourth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="db123-108">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="db123-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="db123-109">Übertragen des SharePoint-Aussehens und -Verhaltens auf Ihr vom Anbieter gehostetes Add-In</span><span class="sxs-lookup"><span data-stu-id="db123-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
    
 
-  [<span data-ttu-id="db123-110">Einfügen einer benutzerdefinierten Schaltfläche in das vom Anbieter gehostete Add-In</span><span class="sxs-lookup"><span data-stu-id="db123-110">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in.md)
    
 

 <span data-ttu-id="db123-p102">**Hinweis** Wenn Sie diese Reihe zu vom Anbieter gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei „BeforeSharePointWriteOps.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="db123-p102">**Note**  If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeSharePointWriteOps.sln file.</span></span>
 

<span data-ttu-id="db123-p103">In diesem Artikel unterbrechen wir die Programmierung kurz, um einen schnellen Überblick über das clientseitige SharePoint-Objektmodell (CSOM) bereitzustellen. Dieses Modell ist umfassend und gut mit Referenzthemen, „Gewusst wie"-Artikeln und Codebeispielen in MSDN dokumentiert. In diesem Artikel können wir nur die alleroberste Spitze des Eisbergs darstellen. Aber selbst eine sehr kurze Einführung wird einen Großteil des Codes, den Sie in dieser Reihe sehen, viel weniger mysteriös erscheinen lassen.</span><span class="sxs-lookup"><span data-stu-id="db123-p103">In this article you'll take a brief break from coding to get a quick overview of the SharePoint Client-side Object Model (CSOM). This model is large and well-documented in MSDN with reference topics, "how to"s, and code samples. In this article, we can only provide the tip of the tip of the tip of the iceberg. But even a very short introduction will make much of the code you will see in this series a lot less mysterious.</span></span> 
 

## <a name="content-hierarchy"></a><span data-ttu-id="db123-117">Inhaltshierarchie</span><span class="sxs-lookup"><span data-stu-id="db123-117">Content Hierarchy</span></span>

<span data-ttu-id="db123-p104">In der folgenden Tabelle finden Sie die Hierarchie von Inhalten in SharePoint und die CSOM-Klassen, die diese Inhalte darstellen. Jede dieser Entitäten verfügt über untergeordnete Elemente des Typs direkt darunter.</span><span class="sxs-lookup"><span data-stu-id="db123-p104">The table below shows the hierarchy of content in SharePoint and the CSOM classes that represent them. Each of these entities has children of the type just below it.</span></span>
 

|<span data-ttu-id="db123-120">**Entität**</span><span class="sxs-lookup"><span data-stu-id="db123-120">**Entity**</span></span>|<span data-ttu-id="db123-121">**Klasse**</span><span class="sxs-lookup"><span data-stu-id="db123-121">**Class**</span></span>|<span data-ttu-id="db123-122">**Bemerkungen**</span><span class="sxs-lookup"><span data-stu-id="db123-122">**Remarks**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="db123-123">Lokale SharePoint-Farm oder SharePoint Online-Abonnement (auch als Mandant bezeichnet)</span><span class="sxs-lookup"><span data-stu-id="db123-123">SharePoint on-premises farm or SharePoint Online subscription (also called a tenant)</span></span>||<span data-ttu-id="db123-p105">Es gibt nur eingeschränkten programmgesteuerten Zugriff auf diese Ebene in CSOM. Es gibt z. B. keine Klasse „Farm" oder „Abonnements" oder „Mandant". (Das serverseitige SharePoint-Objektmodell, das in Add-Ins nicht verwendet werden kann, ermöglicht den programmgesteuerten Zugriff auf diese Entitäten.)</span><span class="sxs-lookup"><span data-stu-id="db123-p105">There is only limited programmatic access to this level in CSOM. There is no Farm or Subscription or Tenant class, for example. (SharePoint's server-side object model, which cannot be used in add-ins, enables programmatic access to these entities.)</span></span>|
|<span data-ttu-id="db123-127">Websitesammlung</span><span class="sxs-lookup"><span data-stu-id="db123-127">site collection</span></span>|<span data-ttu-id="db123-128">**Site**</span><span class="sxs-lookup"><span data-stu-id="db123-128">**Site**</span></span>|<span data-ttu-id="db123-p106">Eine Sammlung von Websites, die hauptsächlich aus administrativen Gründen und zum Unterbringen von SharePoint-Komponenten wie firmenspezifischen Masterseiten oder benutzerdefinierten Sicherheitsgruppen gruppiert werden und für alle untergeordneten Websites angewendet werden können. Alle Websites gehören zu irgendeiner Websitesammlung.</span><span class="sxs-lookup"><span data-stu-id="db123-p106">A collection of websites that are grouped together for mainly administrative reasons and to house SharePoint components, such as branded master pages, or custom security groups, that can be applied to all the child websites. All websites belong to some site collection.</span></span>|
|<span data-ttu-id="db123-131">Website</span><span class="sxs-lookup"><span data-stu-id="db123-131">website</span></span>|<span data-ttu-id="db123-132">**Web**</span><span class="sxs-lookup"><span data-stu-id="db123-132">**Web**</span></span>|<span data-ttu-id="db123-p107">Eine Reihe von Seiten und SharePoint-Komponenten, die Unterwebsites haben können.</span><span class="sxs-lookup"><span data-stu-id="db123-p107">A set of pages and SharePoint components. Can have subwebsites.</span></span>|
|<span data-ttu-id="db123-135">Liste</span><span class="sxs-lookup"><span data-stu-id="db123-135">list</span></span>|<span data-ttu-id="db123-136">**List**</span><span class="sxs-lookup"><span data-stu-id="db123-136">**List**</span></span>|<span data-ttu-id="db123-p108">Dokumentbibliotheken und andere Arten von Dateibibliotheken sind ebenfalls auf dieser Ebene. Eine Dokumentbibliothek ist eine besondere Art von Liste, in der jede Zeile ein angefügtes Dokument enthält und die anderen Spalten Daten über das Dokument sind, z. B. der Autor, wann es zuletzt bearbeitet wurde und wer es ausgecheckt hat.</span><span class="sxs-lookup"><span data-stu-id="db123-p108">Document libraries and other kinds of file libraries are also at this level. A document library is a special kind of list in which each row includes an attached document, and the other columns are data about the document, such as its author, when it was last edited, and who has it checked out.</span></span> |
|<span data-ttu-id="db123-139">Listenelement</span><span class="sxs-lookup"><span data-stu-id="db123-139">list item</span></span>|<span data-ttu-id="db123-140">**ListItem**</span><span class="sxs-lookup"><span data-stu-id="db123-140">**ListItem**</span></span>|<span data-ttu-id="db123-p109">Eine Zeile in einer Liste, d. h. ein Listenelement mit bestimmten Werten in den Feldern der Zeile. Es hat auch einen Typ. Mehr dazu in der nächsten Zeile.</span><span class="sxs-lookup"><span data-stu-id="db123-p109">A row in a list—that is, a list item—with particular values in the fields of the row. Also has a type. See next row.</span></span> |
|<span data-ttu-id="db123-144">Listenelement</span><span class="sxs-lookup"><span data-stu-id="db123-144">list item</span></span>|<span data-ttu-id="db123-145">**Inhaltstyp**</span><span class="sxs-lookup"><span data-stu-id="db123-145">**Content Type**</span></span>|<span data-ttu-id="db123-p110">Der Typ eines Listenelements. Diese werden von der Klasse **ContentType** dargestellt und sind im Wesentlichen eine Reihe von Spalten und Metadaten. Der einfachste Typ ist der integrierte **Item**-Inhaltstyp. Alle anderen Inhaltstypen werden von **Item** abgeleitet. SharePoint enthält viele integrierte Inhaltstypen, z. B. Ereignis und Ankündigung. </span><span class="sxs-lookup"><span data-stu-id="db123-p110">The type of a list item. These are represented by the  **ContentType** class. Each is basically a set of columns and metadata. The simplest is the built-in **Item** content type. All other content types are derived from **Item**. SharePoint includes many built-in content types, such as Event and Announcement.</span></span> |
|<span data-ttu-id="db123-152">Spalte</span><span class="sxs-lookup"><span data-stu-id="db123-152">column</span></span>|<span data-ttu-id="db123-153">**Field**</span><span class="sxs-lookup"><span data-stu-id="db123-153">**Field**</span></span>|<span data-ttu-id="db123-154">Ein **Field**-Objekt enthält nicht nur Informationen zum zugrunde liegenden Datentyp, sondern auch Informationen darüber, wie die Daten formatiert und in Formularen gerendert werden, z. B. in Formularen zum Erstellen, Anzeigen und Bearbeiten bestimmter Listenelemente.</span><span class="sxs-lookup"><span data-stu-id="db123-154">A  **Field** object includes not only information about the underlying data type, but also information about how the data is formatted and rendered on forms, such as the forms for creating, displaying, and editing specific list items.</span></span>|

 

 
<span data-ttu-id="db123-155">Sie können benutzerdefinierte Listen, Inhaltstypen, Spaltentypen und Listenelemente programmgesteuert erstellen.</span><span class="sxs-lookup"><span data-stu-id="db123-155">You can programmatically create custom lists, content types, column types, and list items.</span></span> 
 

 
<span data-ttu-id="db123-156">Zusätzlich zum Inhalt ermöglicht das CSOM den Zugriff auf Benutzer, Gruppen, Rollen &amp; Berechtigungen, Taxonomie, Suche und mehr.</span><span class="sxs-lookup"><span data-stu-id="db123-156">In addition to content, the CSOM gives you access to users, groups, roles &amp; permissions, taxonomy, search, and more.</span></span>
 

 

## <a name="client-side-runtime-and-batching"></a><span data-ttu-id="db123-157">Clientseitige Laufzeit und Batchverarbeitung</span><span class="sxs-lookup"><span data-stu-id="db123-157">Client-side runtime and batching</span></span>
<span data-ttu-id="db123-158"><a name="CSOMBatching"> </a></span><span class="sxs-lookup"><span data-stu-id="db123-158"></span></span>

<span data-ttu-id="db123-p111">CSOM verwendet ein Batchverarbeitungssystem. Abschnitte von verwaltetem Code werden in XML konvertiert und in einer einzigen HTTP-Anforderung an den Server gesendet. Für jeden Befehl erfolgt ein entsprechender Serverobjektmodell-Aufruf, und der Server gibt eine Antwort an den Client imb JSON-Format (JavaScript Object Notation) zurück.</span><span class="sxs-lookup"><span data-stu-id="db123-p111">CSOM uses a batching system. Chunks of managed code is converted into XML and sent to the server in a single HTTP request. For every command, a corresponding server object model call is made, and the server returns a response to the client in JavaScript Object Notation (JSON) format.</span></span> 
 

 
<span data-ttu-id="db123-p112">SharePoint-Code auf einem Client beginnt mit dem Abrufen eines Clientkontextobjekts, das den aktuellen Anforderungskontext darstellt, einschließlich der Identität der SharePoint-Website (und ihrer übergeordneten Websitesammlung). Durch diesen Kontext können Zugriff auf CSOM-Objekte erhalten. Im Folgenden ist die grundlegende Struktur gezeigt, die Sie immer wieder sehen werden. Beachten Sie Folgendes bei diesem Code:</span><span class="sxs-lookup"><span data-stu-id="db123-p112">SharePoint code on a client begins by retrieving a client context object that represents the current request context, including the identity of the SharePoint website (and its parent site collection) and through this context you can obtain access to CSOM objects. The following is the basic structure that you will see again and again. Note the following about this code:</span></span>
 

 

- <span data-ttu-id="db123-p113">Das Objekt  `spContext` ist vom Typ **SharePointContext** und wird in einer SharePointContext.cs-Datei (oder. vb) definiert, die von Office-Entwicklertools für Visual Studio generiert wird. Diese Datei kann geändert werden, dies ist aber nicht häufig erforderlich. Für die meisten SharePoint-Add-In-Projekte, fungieren diese und die TokenHelper.cs-Datei (oder .vb), die ebenfalls von den Tools generiert wird, effektiv als Erweiterungen von CSOM selbst.</span><span class="sxs-lookup"><span data-stu-id="db123-p113">The  `spContext` object is of the type **SharePointContext** and is defined in a the SharePointContext.cs (or .vb) file that is generated by the Office Developer Tools for Visual Studio. This file can be modified, but it is not often that you need to do so. For most SharePoint Add-in projects, this file, and the TokenHelper.cs (or .vb) file that is also generated by the tools, effectively function as extensions of CSOM itself.</span></span>
    
 
- <span data-ttu-id="db123-168">Das `clientContext`-Objekt ist der CSOM-Typ **ClientContext**.</span><span class="sxs-lookup"><span data-stu-id="db123-168">The  `clientContext` object is the CSOM type **ClientContext**.</span></span>
    
 
- <span data-ttu-id="db123-p114">Die Methode **ExecuteQuery** bündelt den CRUD-Vorgangscode in einer XML-Nachricht, die an den SharePoint-Server gesendet wird. Dort wird sie in entsprechenden serverseitigen Objektmodellcode übersetzt und ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="db123-p114">The  **ExecuteQuery** method bundles up the CRUD operation code in and XML message that it sends to the SharePoint server. There it is translated into equivalent server-side object model code and executed.</span></span>
    
 



```C#
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    // CRUD operation or query code goes here.

    clientContext.ExecuteQuery();
}
```

<span data-ttu-id="db123-p115">Im vorherigen Artikel dieser Reihe war ein Beispiel dieses Musters in der unten gezeigten Methode  `GetLocalEmployeeName` dargestellt. Beachten Sie Folgendes zu dieser Methode:</span><span class="sxs-lookup"><span data-stu-id="db123-p115">There was an example of this pattern in the previous article of this series, in the  `GetLocalEmployeeName` method shown below. Note the following about this method:</span></span>
 

 

- <span data-ttu-id="db123-p116">Die ersten beiden Zeilen im **using**-Block scheinen Verweise auf die Liste und das Listenelementobjekt abzurufen. Aber tatsächlich werden diese Zeilen, wenn sie in der clientseitigen SharePoint-Laufzeit ausgeführt werden, einfach in ein XML-Format übersetzt. Die Methode **ExecuteQuery** sendet diesen XML-Code an den Server.</span><span class="sxs-lookup"><span data-stu-id="db123-p116">The first two lines in the  **using** block appear to get references to the list and the list item object. But actually when these lines execute in the SharePoint client-side runtime, they are simply translated into an XML format. The **ExecuteQuery** method sends that XML to the server.</span></span>
    
 
-  <span data-ttu-id="db123-p117">Die Methode **Load** fügt zusätzlich etwas in die Nachricht ein: Sie teilt dem Server mit, das angegebene Objekt an den Client zu senden. Die Methode **ExecuteQuery** empfängt dieses Objekt (als JSON) und verwendet es, um die clientseitige Variable `selectedLocalEmployee` zu initialisieren. Nachfolgender clientseitiger Code verweist dann auf dieses **ListItem**-Objekt und dessen Member. Wie Sie sehen können, verweist die nächste Zeile auf den Wert des Felds „Titel" für das Element. Diese Zeile hätte eine Ausnahme ausgelöst, wenn die Methode **Load** nicht aufgerufen worden wäre, da das Objekt nicht wirklich auf der Clientseite vorhanden ist, bis es geladen wird.</span><span class="sxs-lookup"><span data-stu-id="db123-p117">The **Load** method adds something extra to the message: it tells the server to send the specified object down to the client. The **ExecuteQuery** method receives this object (as JSON) and uses it to initialize the client-side `selectedLocalEmployee` variable. Subsequent client-side code and then reference that **ListItem** object and its members. As you can see, the next line references the value of the item's "Title" field. This line would have thrown an exception if the **Load** method had not been called because the object doesn't really exist on the client-side until its loaded.</span></span>
    
 



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
<span data-ttu-id="db123-181"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="db123-181"></span></span>

 <span data-ttu-id="db123-182">Im nächsten Artikel kehren wir zum Programmieren zurück, und Sie erfahren, wie Sie Daten an SharePoint schreiben: [Hinzufügen von SharePoint-Schreibvorgängen zum vom Anbieter gehosteten Add-In](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)</span><span class="sxs-lookup"><span data-stu-id="db123-182">In the next article, we get back to coding and learn how to write data to SharePoint: [Add SharePoint write operations to the provider-hosted add-in](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)</span></span>
 

 

