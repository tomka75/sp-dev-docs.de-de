---
title: "Abfragen von SharePoint-Änderungsprotokoll mit komplexer ChangeQuery und komplexer ChangeToken"
ms.date: 11/03/2017
ms.openlocfilehash: b255a298743e00c4616b691d4671ec5bea7c4463
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="query-sharepoint-change-log-with-changequery-and-changetoken"></a><span data-ttu-id="48033-102">Abfragen von SharePoint-Änderungsprotokoll mit komplexer ChangeQuery und komplexer ChangeToken</span><span class="sxs-lookup"><span data-stu-id="48033-102">Query SharePoint change log with ChangeQuery and ChangeToken</span></span>

<span data-ttu-id="48033-103">Verwenden Sie **komplexer ChangeQuery** und **komplexer ChangeToken** , um das SharePoint-Änderungsprotokoll nach Änderungen an einer SharePoint-Inhaltsdatenbank, Websitesammlung, Website oder Liste abzufragen.</span><span class="sxs-lookup"><span data-stu-id="48033-103">Use  **ChangeQuery** and **ChangeToken** to query the SharePoint change log for changes made to a SharePoint content database, site collection, site, or list.</span></span>

<span data-ttu-id="48033-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="48033-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="48033-105">Sie können das Änderungsprotokoll für SharePoint mithilfe von [komplexer ChangeQuery](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery.aspx) und [komplexer ChangeToken](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.changetoken.aspx) Suchen Abfragen und Prozess Änderungen vorgenommen, auf einer SharePoint-Inhaltsdatenbank, Websitesammlung, Website oder Liste.</span><span class="sxs-lookup"><span data-stu-id="48033-105">You can query the SharePoint change log by using [ChangeQuery](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery.aspx) and [ChangeToken](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.changetoken.aspx) to find and process changes made on a SharePoint content database, site collection, site, or list.</span></span>

<span data-ttu-id="48033-106">Das [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) -Codebeispiel zeigt, wie mithilfe SharePoints-Änderungsprotokoll suchen und Verarbeiten von Änderungen auf einer SharePoint-Liste.</span><span class="sxs-lookup"><span data-stu-id="48033-106">The [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) code sample shows you how to use SharePoint's change log to find and process changes made on a SharePoint list.</span></span> <span data-ttu-id="48033-107">Verwenden Sie dieses Codebeispiel an:</span><span class="sxs-lookup"><span data-stu-id="48033-107">Use this code sample to:</span></span>

- <span data-ttu-id="48033-108">Überwachen von SharePoint für Änderungen auf eine Liste, Website, Websitesammlung oder Inhaltsdatenbank.</span><span class="sxs-lookup"><span data-stu-id="48033-108">Monitor SharePoint for changes on a list, site, site collection, or content database.</span></span>
    
- <span data-ttu-id="48033-109">Starten Sie einen Geschäftsprozess, nachdem ein Element in einer Liste geändert wird.</span><span class="sxs-lookup"><span data-stu-id="48033-109">Start a business process after a change is made to an item in a list.</span></span>
    
- <span data-ttu-id="48033-110">Ergänzen Sie Ihre remote-Ereignisempfänger.</span><span class="sxs-lookup"><span data-stu-id="48033-110">Complement your remote event receiver.</span></span> <span data-ttu-id="48033-111">Das Muster der Änderung melden Sie sich werden mit einer remote-Ereignisempfänger Muster eine zuverlässigere Architektur für die Verarbeitung aller Änderungen an SharePoint-Inhaltsdatenbanken, Websitesammlungen, Websites oder Listen.</span><span class="sxs-lookup"><span data-stu-id="48033-111">Using the change log pattern with a remote event receiver pattern provides a more reliable architecture for handling all changes made to SharePoint content databases, site collections, sites, or lists.</span></span> <span data-ttu-id="48033-112">Remote-Ereignisempfänger sofort ausgeführt, aber, da sie auf einem Remoteserver ausgeführt werden, treten möglicherweise ein Fehler bei der Kommunikation.</span><span class="sxs-lookup"><span data-stu-id="48033-112">Remote event receivers run immediately, but because they run on a remote server, you might encounter a communication failure.</span></span> <span data-ttu-id="48033-113">Das Muster der Änderung Protokoll wird sichergestellt, dass alle Änderungen für die Verarbeitung verfügbar sind, aber die Anwendung die Änderungen bei der Verarbeitung in der Regel nach einem Zeitplan (beispielsweise einen Zeitgeberauftrag) ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="48033-113">The change log pattern ensures that all changes are available for processing, but the application processing the changes usually runs on a schedule (for example, a timer job).</span></span> <span data-ttu-id="48033-114">Dies bedeutet, dass die Änderungen nicht sofort verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="48033-114">This means that changes are not processed immediately.</span></span> <span data-ttu-id="48033-115">Wenn Sie diese beiden Muster gemeinsam verwenden, stellen Sie sicher, dass Sie einen Mechanismus verwenden, um zu verhindern, dass die gleiche Änderung zweimal verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="48033-115">If you use these two patterns together, ensure you use a mechanism to prevent processing the same change twice.</span></span> <span data-ttu-id="48033-116">Weitere Informationen finden Sie unter [Verwendung von remote-Ereignisempfänger in SharePoint](Use-remote-event-receivers-in-SharePoint.md).</span><span class="sxs-lookup"><span data-stu-id="48033-116">For more information, see [Use remote event receivers in SharePoint](Use-remote-event-receivers-in-SharePoint.md).</span></span>
    
## <a name="before-you-begin"></a><span data-ttu-id="48033-117">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="48033-117">Before you begin</span></span>

<span data-ttu-id="48033-118">Laden Sie Sie zuerst [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="48033-118">To get started, download the [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="48033-119">Bevor Sie dieses Codebeispiel ausführen, folgendermaßen Sie vor:</span><span class="sxs-lookup"><span data-stu-id="48033-119">Before you run this code sample, do the following:</span></span>

1. <span data-ttu-id="48033-120">Melden Sie sich bei Ihrem Office 365-Website, in dem Sie die Liste erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="48033-120">Sign in to your Office 365 site where you want to create the list.</span></span>
    
2. <span data-ttu-id="48033-121">Wählen Sie **Websiteinhalte**.</span><span class="sxs-lookup"><span data-stu-id="48033-121">Choose  **Site Contents**.</span></span>
    
3. <span data-ttu-id="48033-122">Wählen Sie **ein Add-In hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="48033-122">Choose  **add an add-in**.</span></span>
    
4. <span data-ttu-id="48033-123">Wählen Sie **benutzerdefinierte Liste**aus.</span><span class="sxs-lookup"><span data-stu-id="48033-123">Choose  **Custom List**.</span></span>
    
5. <span data-ttu-id="48033-124">Geben Sie im Feld **Name** **TestList**aus.</span><span class="sxs-lookup"><span data-stu-id="48033-124">In  **Name**, enter  **TestList**.</span></span>
    
6. <span data-ttu-id="48033-125">Wählen Sie **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="48033-125">Choose  **Create**.</span></span>
    
<span data-ttu-id="48033-126">Um eine Demo des in diesem Codebeispiel angezeigt wird, führen Sie die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="48033-126">To see a demo of this code sample, perform the following steps:</span></span>

1. <span data-ttu-id="48033-127">Wählen Sie in Visual Studio **Starten** .</span><span class="sxs-lookup"><span data-stu-id="48033-127">Choose  **Start** in Visual Studio.</span></span>
    
2. <span data-ttu-id="48033-128">Geben Sie Ihre Office 365-Website-URL, die den Namen der Liste (**TestList**) und Office 365-Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="48033-128">Enter your Office 365 site's URL, the name of the list (**TestList**), and your Office 365 credentials.</span></span> <span data-ttu-id="48033-129">Jetzt die Konsolenanwendung wartet, bis Änderungen an die **TestList**vorgenommen werden.</span><span class="sxs-lookup"><span data-stu-id="48033-129">The console application now waits for changes to be made to **TestList**.</span></span> <span data-ttu-id="48033-130">Standardmäßig werden die Konsolenanwendung überprüft das Änderungsprotokoll und aktualisiert die Anzeige alle 30 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="48033-130">By default, the console application checks the change log and updates the display every 30 seconds.</span></span>
    
3. <span data-ttu-id="48033-131">Fügen Sie ein neues Element hinzu **TestList**:</span><span class="sxs-lookup"><span data-stu-id="48033-131">Add a new item to  **TestList**:</span></span>
    
    1. <span data-ttu-id="48033-132">Öffnen Sie Ihre Office 365-Website, und navigieren Sie zu **Websiteinhalte** > **TestList**.</span><span class="sxs-lookup"><span data-stu-id="48033-132">Open your Office 365 site and go to  **Site Contents** > **TestList**.</span></span>
    
    2. <span data-ttu-id="48033-133">Wählen Sie **Neues Element**aus.</span><span class="sxs-lookup"><span data-stu-id="48033-133">Choose  **new item**.</span></span>
    
    3. <span data-ttu-id="48033-134">Geben Sie in das Feld **Titel** **MyTitle** ein, und wählen Sie dann auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="48033-134">Enter  **MyTitle** in **Title**, and then choose  **Save**.</span></span>
    
4. <span data-ttu-id="48033-135">Stellen Sie sicher, dass die Änderung in der Konsole angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="48033-135">Verify that your change appears in the console application.</span></span> <span data-ttu-id="48033-136">Sie können die Konsolenanwendung zum Lesen von SharePoint Änderungsprotokoll, indem Sie in der Konsolenanwendung **R** eingeben erzwingen.</span><span class="sxs-lookup"><span data-stu-id="48033-136">You can force the console application to read SharePoint's change log by entering  **r** in the console application.</span></span>

## <a name="use-the-corelistitemchangemonitor-add-in"></a><span data-ttu-id="48033-137">Verwenden des Core.ListItemChangeMonitor-add-Ins</span><span class="sxs-lookup"><span data-stu-id="48033-137">Use the Core.ListItemChangeMonitor add-in</span></span>

<span data-ttu-id="48033-138">In Program.cs Anrufe **Main** **DoWork** zum Lesen und Verarbeiten von SharePoint Änderungsprotokoll aus:</span><span class="sxs-lookup"><span data-stu-id="48033-138">In Program.cs,  **Main** calls **DoWork** to read and process SharePoint's change log:</span></span>

1. <span data-ttu-id="48033-139">Erstellen Sie ein **komplexer ChangeQuery** -Objekt Zugriff auf SharePoint Änderungsprotokoll.</span><span class="sxs-lookup"><span data-stu-id="48033-139">Create a  **ChangeQuery** object to access SharePoint's change log.</span></span>
    
2. <span data-ttu-id="48033-140">Verwenden Sie das Änderungsprotokoll, um Änderungen auf Elemente zurückgeben, indem Sie **Cq. Item = True**.</span><span class="sxs-lookup"><span data-stu-id="48033-140">Use the change log to return changes to items by using  **cq.Item = true**.</span></span> <span data-ttu-id="48033-141">Dazu gehören:</span><span class="sxs-lookup"><span data-stu-id="48033-141">Changes include:</span></span>
    
    - <span data-ttu-id="48033-142">Neue Elemente hinzugefügt werden, mithilfe von **Cq. Hinzufügen von = True**.</span><span class="sxs-lookup"><span data-stu-id="48033-142">New items added by using  **cq.Add= true**.</span></span>
    
    - <span data-ttu-id="48033-143">Gelöschte Elemente mithilfe von **Cq. DeleteObject = True**.</span><span class="sxs-lookup"><span data-stu-id="48033-143">Deleted items by using  **cq.DeleteObject = true**.</span></span>
    
    - <span data-ttu-id="48033-144">Geändert von Elementen mithilfe von **Cq. Update = True**.</span><span class="sxs-lookup"><span data-stu-id="48033-144">Modified items by using  **cq.Update=true**.</span></span>
    
3. <span data-ttu-id="48033-145">Erstellen Sie ein **komplexer ChangeToken** -Objekt zum Lesen von Änderungen aus dem Änderungsprotokoll aus einem bestimmten Punkt in der Zeit.</span><span class="sxs-lookup"><span data-stu-id="48033-145">Create a  **ChangeToken** object to read changes from the change log from a certain point in time.</span></span>
    
4. <span data-ttu-id="48033-146">Legen Sie mit der Versionsnummer [ChangeToken.StringValue](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changetoken.stringvalue.aspx) , ändern Sie Umfang, GUID **TestList** , Datum und Uhrzeit, wenn geändert wurde, und der Wert des Elements ändern auf ' changeToken ' (mit einem Wert von-1 initialisieren) zu.</span><span class="sxs-lookup"><span data-stu-id="48033-146">Set [ChangeToken.StringValue](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changetoken.stringvalue.aspx) with the version number, change scope, GUID of **TestList** , date and time when changes occurred, and the change item value on the ChangeToken (initialize with a value of -1).</span></span> <span data-ttu-id="48033-147">In diesem Codebeispiel beschränkt die Änderungen, die durch die Initialisierung von Datum und Uhrzeit, wann die Änderungen an den letzten zwei Tagen aufgetreten ist, mithilfe von **DateTime.Now.AddDays(-2) aus dem Änderungsprotokoll lesen. ToUniversalTime(). Ticks.ToString()**.</span><span class="sxs-lookup"><span data-stu-id="48033-147">This code sample limits the amount of changes read from the change log by initializing the date and time when the changes occurred to the previous two days by using **DateTime.Now.AddDays(-2).ToUniversalTime().Ticks.ToString()**.</span></span>
    
5.  <span data-ttu-id="48033-148">Lesen das Änderungsprotokoll entweder alle 30 Sekunden (die durch die Konstante **WaitSeconds**der Standard-Wartezeit festgelegt ist), oder wenn der Benutzer **R**eingibt.</span><span class="sxs-lookup"><span data-stu-id="48033-148">Read the change log either every 30 seconds (which is the default waiting period set by the constant **WaitSeconds**), or when the user enters **r**.</span></span> <span data-ttu-id="48033-149">Wenn das Änderungsprotokoll zu lesen, führt die Konsolenanwendung die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="48033-149">When reading the change log, the console application performs the following steps:</span></span>
    
    1.  <span data-ttu-id="48033-150">Verwendet [List.GetChanges](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.getchanges.aspx) , um die [ChangeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changecollection.aspx)zurückzugeben, die eine von Änderungen Sammlung vorgenommen zur Liste seit der letzten Daylight verarbeitet wurden.</span><span class="sxs-lookup"><span data-stu-id="48033-150">Uses [List.GetChanges](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.getchanges.aspx) to return the [ChangeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changecollection.aspx), which is a collection of changes made to the list since the last time changes were processed.</span></span>
    
    2. <span data-ttu-id="48033-151">Ruft die **DisplayChanges** , um die Änderungen im **ChangeCollection** -Objekt darzustellen.</span><span class="sxs-lookup"><span data-stu-id="48033-151">Calls  **DisplayChanges** to display the changes in the **ChangeCollection** object.</span></span>
    
    3. <span data-ttu-id="48033-152">Die neue Nummer festgelegt im Zeit zum Lesen von Änderungen aus dem Änderungsprotokoll.</span><span class="sxs-lookup"><span data-stu-id="48033-152">Sets the new point in time to read changes from the change log.</span></span> <span data-ttu-id="48033-153">Wenn Änderungen an der Liste (die in **Coll**zurückgegeben wurde) vorhanden sind, legen **ChangeTokenStart** zum letzten Datum und Uhrzeit des ändern.</span><span class="sxs-lookup"><span data-stu-id="48033-153">If there are changes to the list (which was returned in  **coll**), set **ChangeTokenStart** to the last change's date and time.</span></span>

> [!NOTE] 
> <span data-ttu-id="48033-154">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="48033-154">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
private static void DoWork()
        {
            Console.WriteLine();
            Console.WriteLine("Url: " + url);
            Console.WriteLine("User name: " + userName);
            Console.WriteLine("List name: " + listName);
            Console.WriteLine();
            try
            {

                Console.WriteLine(string.Format("Connecting to {0}", url));
                Console.WriteLine();
                ClientContext cc = new ClientContext(url);
                cc.AuthenticationMode = ClientAuthenticationMode.Default;
                cc.Credentials = new SharePointOnlineCredentials(userName, password);

                ListCollection lists = cc.Web.Lists;
                IEnumerable<List> results = cc.LoadQuery<List>(lists.Where(lst => lst.Title == listName));
                cc.ExecuteQuery();
                List list = results.FirstOrDefault();
                if (list == null)
                {

                    Console.WriteLine("A list named \"{0}\" does not exist. Press any key to exit...", listName);
                    Console.ReadKey();
                    return;
                }

                nextRunTime = DateTime.Now;

                ChangeQuery cq = new ChangeQuery(false, false);
                cq.Item = true;
                cq.DeleteObject = true;
                cq.Add = true;
                cq.Update = true;

                // Set the ChangeTokenStart to two days ago to reduce how much data is returned from the change log. Depending on your requirements, you might want to change this value. 
                // The value of the string assigned to ChangeTokenStart.StringValue is semicolon delimited, and takes the following parameters in the order listed:
                // Version number. 
                // The change scope (0 - Content Database, 1 - site collection, 2 - site, 3 - list).
                // GUID of the item the scope applies to (for example, GUID of the list). 
                // Time (in UTC) from when changes occurred.
                // Initialize the change item on the ChangeToken using a default value of -1.

                cq.ChangeTokenStart = new ChangeToken();
                cq.ChangeTokenStart.StringValue = string.Format("1;3;{0};{1};-1", list.Id.ToString(), DateTime.Now.AddDays(-2).ToUniversalTime().Ticks.ToString());

                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine(string.Format("Ctrl+c to exit. Press \"r\" key to force the console application to read the change log without waiting {0} seconds.", WaitSeconds));
                Console.WriteLine();
                Console.ResetColor();
                do
                {
                    do
                    {
                        if (Console.KeyAvailable &amp;&amp; Console.ReadKey(true).KeyChar == 'r') { break; }
                    }
                    while (nextRunTime > DateTime.Now);

                    Console.WriteLine(string.Format("Looking for items modified after {0} UTC", GetDateStringFromChangeToken(cq.ChangeTokenStart)));

                    
                    ChangeCollection coll = list.GetChanges(cq);
                    cc.Load(coll);
                    cc.ExecuteQuery();


                    DisplayChanges(coll, cq.ChangeTokenStart);
                    // If there are changes to the list (which was returned in coll), set ChangeTokenStart to the last change's date and time. This will be used as the starting point for the next read from the change log.                      
                    cq.ChangeTokenStart = coll.Count > 0 ? coll.Last().ChangeToken : cq.ChangeTokenStart;

                    nextRunTime = DateTime.Now.AddSeconds(WaitSeconds);

                } while (true);
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
                Console.WriteLine("Press any key to exit...");
                Console.ReadKey();

            }
        }
```

## <a name="see-also"></a><span data-ttu-id="48033-155">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="48033-155">See also</span></span>
<span data-ttu-id="48033-156"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="48033-156"></span></span>

- [<span data-ttu-id="48033-157">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="48033-157">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [<span data-ttu-id="48033-158">Verwenden von remote-Ereignisempfänger in SharePoint</span><span class="sxs-lookup"><span data-stu-id="48033-158">Use remote event receivers in SharePoint</span></span>](Use-remote-event-receivers-in-SharePoint.md)
    
- [<span data-ttu-id="48033-159">Komplexer ChangeQuery-Member</span><span class="sxs-lookup"><span data-stu-id="48033-159">ChangeQuery members</span></span>](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery_members.aspx)
    
- [<span data-ttu-id="48033-160">Muster und Practices-Entwicklercenter</span><span class="sxs-lookup"><span data-stu-id="48033-160">Patterns and Practices developer center</span></span>](http://dev.office.com/patterns-and-practices)
