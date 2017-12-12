---
title: "Abfragen von SharePoint-Änderungsprotokoll mit komplexer ChangeQuery und komplexer ChangeToken"
ms.date: 11/03/2017
ms.openlocfilehash: b255a298743e00c4616b691d4671ec5bea7c4463
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="query-sharepoint-change-log-with-changequery-and-changetoken"></a>Abfragen von SharePoint-Änderungsprotokoll mit komplexer ChangeQuery und komplexer ChangeToken

Verwenden Sie **komplexer ChangeQuery** und **komplexer ChangeToken** , um das SharePoint-Änderungsprotokoll nach Änderungen an einer SharePoint-Inhaltsdatenbank, Websitesammlung, Website oder Liste abzufragen.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Sie können das Änderungsprotokoll für SharePoint mithilfe von [komplexer ChangeQuery](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery.aspx) und [komplexer ChangeToken](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.changetoken.aspx) Suchen Abfragen und Prozess Änderungen vorgenommen, auf einer SharePoint-Inhaltsdatenbank, Websitesammlung, Website oder Liste.

Das [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) -Codebeispiel zeigt, wie mithilfe SharePoints-Änderungsprotokoll suchen und Verarbeiten von Änderungen auf einer SharePoint-Liste. Verwenden Sie dieses Codebeispiel an:

- Überwachen von SharePoint für Änderungen auf eine Liste, Website, Websitesammlung oder Inhaltsdatenbank.
    
- Starten Sie einen Geschäftsprozess, nachdem ein Element in einer Liste geändert wird.
    
- Ergänzen Sie Ihre remote-Ereignisempfänger. Das Muster der Änderung melden Sie sich werden mit einer remote-Ereignisempfänger Muster eine zuverlässigere Architektur für die Verarbeitung aller Änderungen an SharePoint-Inhaltsdatenbanken, Websitesammlungen, Websites oder Listen. Remote-Ereignisempfänger sofort ausgeführt, aber, da sie auf einem Remoteserver ausgeführt werden, treten möglicherweise ein Fehler bei der Kommunikation. Das Muster der Änderung Protokoll wird sichergestellt, dass alle Änderungen für die Verarbeitung verfügbar sind, aber die Anwendung die Änderungen bei der Verarbeitung in der Regel nach einem Zeitplan (beispielsweise einen Zeitgeberauftrag) ausgeführt wird. Dies bedeutet, dass die Änderungen nicht sofort verarbeitet werden. Wenn Sie diese beiden Muster gemeinsam verwenden, stellen Sie sicher, dass Sie einen Mechanismus verwenden, um zu verhindern, dass die gleiche Änderung zweimal verarbeiten. Weitere Informationen finden Sie unter [Verwendung von remote-Ereignisempfänger in SharePoint](Use-remote-event-receivers-in-SharePoint.md).
    
## <a name="before-you-begin"></a>Bevor Sie beginnen:

Laden Sie Sie zuerst [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Bevor Sie dieses Codebeispiel ausführen, folgendermaßen Sie vor:

1. Melden Sie sich bei Ihrem Office 365-Website, in dem Sie die Liste erstellen möchten.
    
2. Wählen Sie **Websiteinhalte**.
    
3. Wählen Sie **ein Add-In hinzufügen**.
    
4. Wählen Sie **benutzerdefinierte Liste**aus.
    
5. Geben Sie im Feld **Name** **TestList**aus.
    
6. Wählen Sie **Erstellen**.
    
Um eine Demo des in diesem Codebeispiel angezeigt wird, führen Sie die folgenden Schritte aus:

1. Wählen Sie in Visual Studio **Starten** .
    
2. Geben Sie Ihre Office 365-Website-URL, die den Namen der Liste (**TestList**) und Office 365-Anmeldeinformationen. Jetzt die Konsolenanwendung wartet, bis Änderungen an die **TestList**vorgenommen werden. Standardmäßig werden die Konsolenanwendung überprüft das Änderungsprotokoll und aktualisiert die Anzeige alle 30 Sekunden.
    
3. Fügen Sie ein neues Element hinzu **TestList**:
    
    1. Öffnen Sie Ihre Office 365-Website, und navigieren Sie zu **Websiteinhalte** > **TestList**.
    
    2. Wählen Sie **Neues Element**aus.
    
    3. Geben Sie in das Feld **Titel** **MyTitle** ein, und wählen Sie dann auf **Speichern**.
    
4. Stellen Sie sicher, dass die Änderung in der Konsole angezeigt wird. Sie können die Konsolenanwendung zum Lesen von SharePoint Änderungsprotokoll, indem Sie in der Konsolenanwendung **R** eingeben erzwingen.

## <a name="use-the-corelistitemchangemonitor-add-in"></a>Verwenden des Core.ListItemChangeMonitor-add-Ins

In Program.cs Anrufe **Main** **DoWork** zum Lesen und Verarbeiten von SharePoint Änderungsprotokoll aus:

1. Erstellen Sie ein **komplexer ChangeQuery** -Objekt Zugriff auf SharePoint Änderungsprotokoll.
    
2. Verwenden Sie das Änderungsprotokoll, um Änderungen auf Elemente zurückgeben, indem Sie **Cq. Item = True**. Dazu gehören:
    
    - Neue Elemente hinzugefügt werden, mithilfe von **Cq. Hinzufügen von = True**.
    
    - Gelöschte Elemente mithilfe von **Cq. DeleteObject = True**.
    
    - Geändert von Elementen mithilfe von **Cq. Update = True**.
    
3. Erstellen Sie ein **komplexer ChangeToken** -Objekt zum Lesen von Änderungen aus dem Änderungsprotokoll aus einem bestimmten Punkt in der Zeit.
    
4. Legen Sie mit der Versionsnummer [ChangeToken.StringValue](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changetoken.stringvalue.aspx) , ändern Sie Umfang, GUID **TestList** , Datum und Uhrzeit, wenn geändert wurde, und der Wert des Elements ändern auf ' changeToken ' (mit einem Wert von-1 initialisieren) zu. In diesem Codebeispiel beschränkt die Änderungen, die durch die Initialisierung von Datum und Uhrzeit, wann die Änderungen an den letzten zwei Tagen aufgetreten ist, mithilfe von **DateTime.Now.AddDays(-2) aus dem Änderungsprotokoll lesen. ToUniversalTime(). Ticks.ToString()**.
    
5.  Lesen das Änderungsprotokoll entweder alle 30 Sekunden (die durch die Konstante **WaitSeconds**der Standard-Wartezeit festgelegt ist), oder wenn der Benutzer **R**eingibt. Wenn das Änderungsprotokoll zu lesen, führt die Konsolenanwendung die folgenden Schritte aus:
    
    1.  Verwendet [List.GetChanges](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.getchanges.aspx) , um die [ChangeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changecollection.aspx)zurückzugeben, die eine von Änderungen Sammlung vorgenommen zur Liste seit der letzten Daylight verarbeitet wurden.
    
    2. Ruft die **DisplayChanges** , um die Änderungen im **ChangeCollection** -Objekt darzustellen.
    
    3. Die neue Nummer festgelegt im Zeit zum Lesen von Änderungen aus dem Änderungsprotokoll. Wenn Änderungen an der Liste (die in **Coll**zurückgegeben wurde) vorhanden sind, legen **ChangeTokenStart** zum letzten Datum und Uhrzeit des ändern.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [Verwenden von remote-Ereignisempfänger in SharePoint](Use-remote-event-receivers-in-SharePoint.md)
    
- [Komplexer ChangeQuery-Member](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery_members.aspx)
    
- [Muster und Practices-Entwicklercenter](http://dev.office.com/patterns-and-practices)
