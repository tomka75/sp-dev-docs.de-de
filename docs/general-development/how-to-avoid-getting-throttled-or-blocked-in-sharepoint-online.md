---
title: Vorgehensweise verhindern, dass gedrosselt oder blockiert in SharePoint Online
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 33ed8106-d850-42b1-8d7f-5ba83901149c
ms.openlocfilehash: 4be030d0e9ee97d6f5c704e5ffa7d1be87c23325
ms.sourcegitcommit: 61f26b4fe41d3cd80622d9950d8f6599df48f26f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/26/2017
---
# <a name="how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online"></a>Gewusst wie: Vermeiden von Drosselung und Sperren in SharePoint Online
In diesem Artikel erfahren Sie mehr über das Thema Drosselung in SharePoint Online. Außerdem erläutern wir Ihnen, wie Sie eine Drosselung oder Sperre vermeiden können, und stellen Ihnen CSOM- und REST-Beispielcode bereit, mit denen Sie die nötigen Aufgaben leichter umsetzen können.

-  [Was bedeutet Drosselung?](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Whatisthrottling)

-  [Drosselung Standardszenarien SharePoint Online](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Commonthrottlingscenarios)

-  [Warum teilt können nicht Sie nur die Grenzwerte für die genauen Drosselung mir?](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Whycantyoujusttellmetheexactthrottlinglimits)

-  [Bewährte Methoden für die Vermeidung von Drosselung](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Bestpracticestohandlethrottling)
    
- [Ausgestalten von Datenverkehr zur Vermeidung von Drosselung](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_DecorateSharePointOnlineThrottling)
  
-  [CSOM-Codebeispiele in GitHub: SharePoint Online-Drosselung](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_GitHubCSOMandRESTcodesamplesSharePointOnlineThrottling)
    
  
-  [Was sollten Sie tun, wenn Sie in SharePoint Online blockiert werden?](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Whatshouldyoudoifyougetblocked)
    
  
-  [Zusätzliche Ressourcen](how-to-avoid-getting-throttled-or-blocked-in-sharepoint-online.md#BKMK_Additionalresources)

Kommt diese bekannt? Sie sind einen CSOM Prozess - beispielsweise Informationen zum Migrieren von Dateien in SharePoint Online - ausführen, aber Sie gedrosselt erste beibehalten. Oder sogar schlechter erhalten Sie vollständig ausgeschlossen. Was geschieht, und was können Sie tun, sodass sie beenden?
  
## <a name="what-is-throttling"></a>Was ist Drosselung bzw. Einschränkung?
<a name="BKMK_Whatisthrottling"> </a>

SharePoint Online verwendet Einschränkung, um eine optimale Leistung und Zuverlässigkeit des Diensts SharePoint Online verwalten. Einschränkungsgrenzwerte Ruft die Anzahl von Aktionen eines Benutzers oder gleichzeitige (von Code- oder Skriptblock), um Ressourcen zu verhindern.
  
Dies bedeutet, dass es in SharePoint Online gedrosselt erhalten Benutzer äußerst selten ist. Der Dienst ist robuste und sehr große Menge behandeln soll. Wenn Sie die Schritte aus gedrosselt erhalten möchten, 99 % der Zeit aufgrund von benutzerdefiniertem Code ist. Keine bedeutet, dass keine andere Möglichkeiten zum Abrufen gedrosselt, einfach, dass sie weniger häufig sind vorhanden sind. Beispiel 10 Computer hochfahren und einen Sync-Client auf alle 10 haben. Synchronisieren Sie auf jedem 1TB von Inhalten. Dies wird wahrscheinlich gedrosselt angezeigt.
  

![Wie es zu Einschränkungen kommt](../images/3b9184db-99a4-416e-ba1e-7f8653484cee.png)
  
### <a name="what-happens-when-you-get-throttled-in-sharepoint-online"></a>Was geschieht, wenn Sie in SharePoint Online gedrosselt abrufen?

Wenn ein Benutzer Einschränkungen überschreitet, anforderungsdrosselungen SharePoint Online keine weiteren Anforderungen von mit dem Benutzerkonto für kurze Zeit. Alle Benutzeraktionen Drosselungen während der Drosselung aktiviert ist.
  
- Bei Anforderungen, die ein Benutzer direkt im Browser ausführt, wird er von SharePoint Online zu einer Seite mit Informationen zur Einschränkung weitergeleitet. Die Anforderungen schlagen fehl.
  
- Für alle anderen Anforderungen, einschließlich CSOM oder REST-Aufrufe SharePoint Online gibt den HTTP-Statuscode 429 ("zu viele Anforderungen"), und die Anforderungen fehl.
  
Wenn der problematische Prozess Usage Grenzwerte überschreitet weiterhin, möglicherweise SharePoint Online den Vorgang vollständig blockieren; in diesem Fall mangelndes HTTP-Statuscode 503 ("Dienst nicht verfügbar"), und benachrichtigen wir Sie den Block in Office 365 Message Center. Die Fehlermeldung ist unten aufgeführt:
      
![Meldung: 503 Server nicht verfügbar](../images/e70a43c1-43ba-4f5c-b25f-e3995f18dd16.png)
      
503 Servermeldung nicht verfügbar.

## <a name="common-throttling-scenarios-in-sharepoint-online"></a>Drosselung Standardszenarien SharePoint Online
<a name="BKMK_Commonthrottlingscenarios"> </a>

Die häufigsten Ursachen für Drosselungen in SharePoint Online pro Benutzer werden mithilfe der clientseitigen Objektmodell (CSOM) oder Representational State Transfer (REST) Code, der zu häufig zu viele Aktionen ausführt.
    

- **Bewusst Datenverkehr**
    
    Nicht viel des Datenverkehrs an jedem beliebigen Zeitpunkt aber genug über einen Zeitraum, den Sie innerhalb und außerhalb der Drosselung episodische Weise ausführen.
    
  - Beispielsweise nach dem Migrieren von Dateien zum SharePoint Online, Ausführung ein benutzerdefiniertes CSOM oder REST-Skripts, um Metadaten für die Dateien zu aktualisieren. Das Skript CSOM/REST wird eine große Anzahl von Dateien mit einer sehr großer Häufigkeit aktualisiert das Drosselung auslöst. In ähnlicher Weise kann auch ein AutoVervollständigen-UI-Widget mit REST-Diensten zu viele Aufrufe an Listen während jeder Endbenutzer-Operation verursachen Drosselung, je nachdem, welche anderen Vorgängen Ressourcen zur selben Zeit in Anspruch nehmen.
    
  ![Sporadische Einschränkung](../images/a61afe25-9597-403f-b3fa-d3f630155021.png)
  
- **Overwhelming Datenverkehr**
    
    Ein einzelner Prozess überschreitet erheblich Drosselung Grenzwerte ständig, über einen längeren Zeitraum Zeitraum.
    
  - Sie verwendet Webdienste zum Erstellen eines Tools zum Synchronisieren von Benutzerprofileigenschaften haben. Das Tool aktualisiert Benutzerprofileigenschaften basierend auf Informationen aus der Line-of-Business (LOB) Personalabteilung (HR)-System. Das Tool führt Aufrufe Zeitabständen zu hoch.
  
  - Sie sind ein Auslastungstests Skript auf SharePoint Online ausgeführt, und Sie erhalten gedrosselt. Auslastungstests ist SharePoint Online nicht zulässig.
  
  - Sie haben Ihre Teamwebsite auf SharePoint Online, beispielsweise durch Hinzufügen einer Statusanzeige auf der Homepage angepasst. Dieser Statusindikator aktualisiert häufig, die bewirkt, dass der Seite zu viele Aufrufe an den Dienst SharePoint Online - dieser Einschränkung ausgelöst.
    
  ![Stabile Einschränkung der maximalen Bandbreite](../images/7849d413-381f-4558-9e50-b3cc9990d3e3.png)
  
## <a name="why-cant-you-just-tell-me-the-exact-throttling-limits"></a>Warum teilt können nicht Sie nur die Grenzwerte für die genauen Drosselung mir?
<a name="BKMK_Whycantyoujusttellmetheexactthrottlinglimits"> </a>

Festlegen und Veröffentlichen von genauen Einschränkung beschränkt Sounds ganz einfach, aber es ist tatsächlich nicht die beste Möglichkeit zum wechseln. Wir überwachen ständig der Ressourcenverwendung auf SharePoint Online. Je nach Verwendung optimieren wir Schwellenwerte, damit Benutzer die maximale Anzahl von Ressourcen verbraucht werden können, ohne Beeinträchtigung der Zuverlässigkeit und Leistung von SharePoint Online. Deshalb ist es ist also wichtig für den CSOM oder REST Einbeziehung inkrementelle Back deaktiviert zum Verarbeiten von Beschränkung; auf diese Weise können Code auf jedem beliebigen Tag so schnell wie möglich ausgeführt, und es Codes wieder aus "nur genügend" kann, wenn es Drosselung Grenzwerte besucht. Die folgenden Codebeispiele weiter unten in diesem Artikel zeigen, wie verwenden inkrementeller wieder aus.

## <a name="best-practices-to-handle-throttling"></a>Bewährte Methoden zum Behandeln der Einschränkungen
<a name="BKMK_Bestpracticestohandlethrottling"> </a>

- Reduzieren Sie die Anzahl der Vorgänge pro Anforderung
    
- Reduzieren Sie die Aufrufhäufigkeit.
    
- Gestalten Sie Ihren Datenverkehr so aus, dass Ihre Identität ersichtlich ist (siehe Abschnitt mit den bewährten Methoden zur Datenverkehrsausgestaltung weiter unten).
    
Falls es doch zu einer Drosselung kommt, empfehlen wir einen inkrementellen Backoff zur Reduzierung der Anzahl und der Häufigkeit von Aufrufen, so lange, bis keine Drosselung mehr vorgenommen wird.

Inkrementelle Back deaktiviert Verwendungsmöglichkeiten stetig länger wartet zwischen den versuchen, bevor Sie erneut versuchen, den Code auszuführen, der gedrosselt wurde. Die Codebeispiele GitHub können weiter unten in diesem Artikel als Erweiterungsmethoden, Sie inkrementelle Back aus dem Code hinzufügen.
    
Sichern deaktiviert, ist die schnellste Methode zum Verarbeiten, da die Ressource: Einsatz melden, während ein Benutzer gedrosselt wird weiterhin SharePoint Online gedrosselt wird. Anders ausgedrückt, arbeiten aggressive Wiederholungsversuche gegen Sie, da, obwohl die Anrufe ausfallen, diese weiterhin vor Ihrer Verwendung Grenzwerte anfallen. Schneller dem Sichern deaktiviert, schneller Sie nicht mehr Usage überschreiten. 

For information about ways to monitor your SharePoint Online activity, see  [Diagnosing performance issues with SharePoint Online](https://support.office.com/de-DE/article/3c364f9e-b9f6-4da4-a792-c8e8c8cd2e86).

Eine ausführlichere Erläuterung zum Thema Drosselung in der Microsoft Cloud finden Sie unter [Throttling Pattern](http://msdn.microsoft.com/library/4baf5af2-32fc-47ab-8569-3e5c59a5ebd5.aspx).

## <a name="how-to-decorate-your-http-traffic-to-avoid-throttling"></a>Ausgestalten von HTTP-Datenverkehr zur Vermeidung von Drosselung
<a name="BKMK_DecorateSharePointOnlineThrottling"> </a>

Unter Umständen wird bestimmter Datenverkehr gedrosselt, um hohe Verfügbarkeit sicherzustellen. Gedrosselt wird, wenn die Systemintegrität gefährdet ist. Ein Kriterium für die Drosselung ist dabei die Ausgestaltung des Datenverkehrs. Sie wirkt sich unmittelbar auf die Datenverkehrspriorisierung aus. Korrekt ausgestalteter Datenverkehr hat Vorrang vor nicht korrekt ausgestaltetem Datenverkehr.
 
Wann gilt Datenverkehr als nicht ausgestaltet?

- Datenverkehr gilt als nicht ausgestaltet, wenn im SharePoint-Aufruf der CSOM-API oder der REST-API keine Zeichenfolge des Typs „AppID“/„AppTitle“ oder des Typs „UserAgent“ enthalten ist.

Was empfiehlt Microsoft?

- Wenn Sie eine Anwendung erstellt haben, sollten Sie sie registrieren und die Zeichenfolgen „AppID“ und „AppTitle“ verwenden. Das gewährleistet eine optimale Benutzererfahrung und zügige Fehlerbehebung. Sie sollten zudem die Zeichenfolge des Benutzer-Agenten einfügen, wie im nachfolgenden Beispiel beschrieben.

- Verwenden Sie für die Zeichenfolge des Benutzer-Agenten im API-Aufruf auf jeden Fall die folgende Namenskonvention:

| Typ  | Benutzer-Agent  | Beschreibung   |
|---|---|---|
| ISV-Anwendung | ISV&#124;CompanyName&#124;AppName/Version | Diese Zeichenfolge identifiziert Sie als „ISV“ und enthält den Namen Ihres Unternehmens sowie den Namen der App, alles jeweils getrennt durch einen senkrechten Strich und gefolgt von einem Schrägstrich und der Versionsnummer.  |
| Unternehmensanwendung | NONISV&#124;CompanyName&#124;AppName/Version | Diese Zeichenfolge identifiziert Sie als „NONISV“ und enthält den Namen Ihres Unternehmens sowie den Namen der App, alles jeweils getrennt durch einen senkrechten Strich und gefolgt von einem Schrägstrich und der Versionsnummer. |

- Wenn Sie eigene JavaScript-Bibliotheken erstellen, die für Aufrufe von SharePoint Online-APIs verwendet werden, müssen Sie die Benutzer-Agent-Informationen in Ihre HTTP-Anforderung aufnehmen. Möglicherweise müssen Sie Ihre Webanwendung außerdem als Anwendung registrieren.

> [!NOTE]
> Das Format der Benutzer-Agent-Zeichenfolge muss dem Standard [RFC2616](http://www.ietf.org/rfc/rfc2616.txt) entsprechen. Informieren Sie sich also über die korrekten Trennzeichen. Sie können die erforderlichen Informationen auch an bereits vorhandene Benutzer-Agent-Zeichenfolgen anfügen.

### <a name="example-of-decorating-traffic-with-user-agent-when-using-client-side-object-model-csom"></a>Beispiel für die Ausgestaltung von Datenverkehr mit einem Benutzer-Agenten bei Verwendung des clientseitigen Objektmodells (CSOM)

```cs
// Get access to source site
using (var ctx = new ClientContext("https://contoso.sharepoint.com/sites/team"))
{
    //Provide account and pwd for connecting to SharePoint Online
    var passWord = new SecureString();
    foreach (char c in pwd.ToCharArray()) passWord.AppendChar(c);
    ctx.Credentials = new SharePointOnlineCredentials("contoso@contoso.onmicrosoft.com", passWord);

    // Add our User Agent information
    ctx.ExecutingWebRequest += delegate (object sender, WebRequestEventArgs e)
    {
        e.WebRequestExecutor.WebRequest.UserAgent = "NONISV|Contoso|GovernanceCheck/1.0";
    };
                
    // Normal CSOM Call with custom User-Agent information
    Web site = ctx.Web;
    ctx.Load(site);
    ctx.ExecuteQuery();
}
```

### <a name="example-of-decorating-traffic-with-user-agent-when-using-rest-apis"></a>Beispiel für die Ausgestaltung von Datenverkehr mit einem Benutzer-Agenten bei Verwendung von REST-APIs

Das folgende Beispiel verwendet das C#-Format. Dasselbe Format sollte auch für Benutzer-Agent-Informationen in JavaScript-Bibliotheken verwendet werden, die Sie auf SharePoint Online-Seiten verwenden.

```cs
HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + "/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.UserAgent = "NONISV|Contoso|GovernanceCheck/1.0";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse endpointResponse = (HttpWebResponse)endpointRequest.GetResponse();
```


## <a name="github-csom-code-samples-sharepoint-online-throttling"></a>CSOM-Codebeispiele in GitHub: SharePoint Online-Drosselung
<a name="BKMK_GitHubCSOMandRESTcodesamplesSharePointOnlineThrottling"> </a>

 [CoreThrottling](https://github.com/OfficeDev/PnP/tree/dev/Samples/Core.Throttling) in der [Office 365 Developer Mustern und Methoden Repository ](http://github.com/OfficeDev/PnP) ist ein Codebeispiel, das die inkrementelle Back deaktiviert Verfahren veranschaulicht. Diese Vorgehensweise erfordert minimale Änderungen am Code.
  
    
    
Bevor Sie dieses Codebeispiel ausführen:
  
    
    

- Öffnen Sie **Program.cs**, und geben Sie die folgende Informationen in der **Main** -Methode:
    
  - Die Anmeldeinformationen Ihres Office 365 Developer-Kontos.
    
  
  - Die URL der Ihrer Office 365 Developer Site.
    
  
  - Der Name einer Test-Dokumentbibliothek auf Ihrer Office 365 Developer Site.
    
  
- Wenn Sie eine Fehlermeldung besagt erhalten, dass die Datei **' App.config '** ungültig ist, wechseln Sie auf den **Projektmappen-Explorer**, **App.config** Rechtsklick, und wählen Sie **Aus Projekt ausschließen**.
    
  
 **Core.Throttling** ausgeführt wird, als eine Konsolenanwendung, die mit einer Autorisierungsrichtlinie nur-, was bedeutet, dass in diesem Codebeispiel wird die Berechtigungen des aktuellen Benutzers verwendet. In der **Main** -Methode in Program.cs, eine While-Schleife wiederholt erstellt neue Ordner in der testdokumentbibliothek. Klicken Sie dann auf **Ctx aufgerufen. ExecuteQueryWithExponentialRetry**, die CSOM zum Ausführen der **ExecuteQuery** -Methode verwendet. **ExecuteQueryWithExponentialRetry** ist eine Erweiterungsmethode für das [ClientContext](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.clientcontext%28v=office.15%29.aspx) -Objekt, und im **ClientContextExtension.cs** definiert ist.
  

**ExecuteQueryWithIncrementalRetry** beginnt SharePoint Online die **"ExecuteQuery"** -Anweisung anforderungsdrosselungen, die inkrementelle Back deaktiviert Verfahren durch:

- Abfangen von eine **WebException** sowie zum Überprüfen der **HttpWebResponse.StatusCode**. Wenn SharePoint Online die Anweisung **ExecuteQuery** gedrosselt werden, ist die **HttpWebResponse.StatusCode** 429.

- Der aktuelle Thread wird für den Zeitraum in **BackoffInterval** angegebenen angehalten.

- Der aktuelle Thread fortgesetzt, die **BackoffInterval** verdoppelt und die Anzahl der Wiederholungsversuche ausgeführt ( **RetryAttempts** ) wird erhöht. Durch verdoppeln **BackoffInterval** hält Ihr Code Aktivität für einen längeren Zeitraum vor der Wiederholung des Codes, die durch SharePoint Online gedrosselt wurde.

- Der Vorgang wird wiederholt, bis die Anweisung **ExecuteQuery** erfolgreich ist, oder die Anzahl der zulässigen Versuche ( **RetryCount** ) überschritten wird.

### <a name="csom-code-sample-incremental-back-off-and-retry-calls-executequerywithincrementalretry-method-later-in-this-article"></a>CSOM-Codebeispiel: inkrementelle Back deaktiviert und "Wiederholen" (ruft ExecuteQueryWithIncrementalRetry-Methode, weiter unten in diesem Artikel)

```

using (var ctx = new ClientContext(serverUrl))
       {
           //Provide account and pwd for connecting to the source
           var passWord = new SecureString();
           foreach (char c in password.ToCharArray()) passWord.AppendChar(c);
           ctx.Credentials = new SharePointOnlineCredentials(login, passWord);
            try
           {
               int number = 0;
               // This loop will be executed 1000 times, which will cause throttling to occur
               while (number < 1000)
               {
                   // Try to create new folder based on Ticks to the given list as an example process
                   var folder = ctx.Site.RootWeb.GetFolderByServerRelativeUrl(listUrlName);
                   ctx.Load(folder);
                   folder = folder.Folders.Add(DateTime.Now.Ticks.ToString());
                   // Extension method for executing query with throttling checks
                   ctx.ExecuteQueryWithIncrementalRetry(5, 30000); //5 retries, with a base delay of 30 secs.
                   // Status indication for execution.
                   Console.WriteLine("CSOM request successful.");
                   // For loop handling.
                   number = number + 1;
               }
           }
           catch (MaximumRetryAttemptedException mex)
           {
               // Exception handling for the Maximum Retry Attempted
               Console.WriteLine(mex.Message);
           }
       }

```


### <a name="csom-code-sample-executequerywithincrementalretry-method"></a>CSOM-Codebeispiel: ExecuteQueryWithIncrementalRetry-Methode


```

public static void ExecuteQueryWithIncrementalRetry(this ClientContext context, int retryCount, int delay)
        {
            int retryAttempts = 0;
            int backoffInterval = delay;
            if (retryCount <= 0)
                throw new ArgumentException("Provide a retry count greater than zero.");
           if (delay <= 0)
                throw new ArgumentException("Provide a delay greater than zero.");
           while (retryAttempts < retryCount)
            {
                try
                {
                    context.ExecuteQuery();
                    return;
                }
                catch (WebException wex)
                {
                    var response = wex.Response as HttpWebResponse;
                    if (response != null &amp;&amp; response.StatusCode == (HttpStatusCode)429)
                    {
                        Console.WriteLine(string.Format("CSOM request exceeded usage limits. Sleeping for {0} seconds before retrying.", backoffInterval));
                        //Add delay.
                        System.Threading.Thread.Sleep(backoffInterval);
                        //Add to retry count and increase delay.
                        retryAttempts++;
                        backoffInterval = backoffInterval * 2;
                    }
                    else
                    {
                        throw;
                    }
                }
            }
            throw new MaximumRetryAttemptedException(string.Format("Maximum retry attempts {0}, have been attempted.", retryCount));
       }

```


## <a name="what-should-you-do-if-you-get-blocked-in-sharepoint-online"></a>Was sollten Sie tun, wenn Sie in SharePoint Online blockiert werden?
<a name="BKMK_Whatshouldyoudoifyougetblocked"> </a>

Blockieren ist die äußerste Form der Einschränkung. Wir blockiert selten jemals einen Mandanten, sofern es langfristige, extrem übermäßig viele Datenverkehr zu erkennen, die die allgemeine Integrität des Diensts SharePoint Online gefährden kann. Wir setzen Blöcke, um zu verhindern, dass übermäßig viele Datenverkehr beeinträchtigt die Leistung und Zuverlässigkeit von SharePoint Online. Ein Block - die in der Regel auf der Ebene der Instanz platziert wird - verhindert, dass den problematischen Prozess ausgeführt, bis Sie das Problem zu beheben. Wenn Ihr Abonnement blockiert werden, müssen Sie Aktion die problematischen Prozesse ändern, bevor der Block entfernt werden kann.
  
Wenn wir Ihr Abonnement zu blockieren, sehen Sie die HTTP-Statuscode 503 und benachrichtigen wir Sie den Block in Office 365 Message Center. Die Nachricht wird beschrieben, was die Optionen blockieren verursacht, enthält Anleitungen zur Behebung des Problems problematischen und informiert Sie, wer kontaktieren, um den Block abrufen entfernt.
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="BKMK_Additionalresources"> </a>

-  [Diagnosing performance issues with SharePoint Online](https://support.office.com/de-DE/article/3c364f9e-b9f6-4da4-a792-c8e8c8cd2e86)
  
-  [Capacity planning and load testing SharePoint Online](http://msdn.microsoft.com/library/22fa7e7e-7554-4987-b56f-b39bbf303a0a.aspx)
  
-  [GitHub: Codebeispiel für SharePoint Online-Einschränkung ](https://github.com/OfficeDev/PnP/tree/dev/Samples/Core.Throttling)