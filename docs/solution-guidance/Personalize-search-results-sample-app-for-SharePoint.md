---
title: "Personalisieren von Search Results Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: e2190e8d60bbca5f3353662823c921c1f59d1c27
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="personalize-search-results-sample-add-in-for-sharepoint"></a>Personalisieren von Search Results Beispiel-add-in für SharePoint

Filtern von Informationen, die dem Benutzer basierend auf dem Wert von einer Benutzerprofileigenschaft angezeigt werden, um SharePoint zu personalisieren.
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_
    
Das [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) -Codebeispiel wird veranschaulicht, wie Sie SharePoint durch Filterinformationen basierend auf dem Wert von einer Benutzerprofileigenschaft personalisieren können. Einige Beispiele für Pesonalization sind:

- Newsartikel oder andere Inhalte nach Land oder Speicherort gefiltert.
    
- Navigationslinks gefiltert basierend auf die Rolle des Benutzers oder der Organisation.
    
- Restaurants oder Retail Steckdose Listen basierend auf den Speicherort der Geschäft.
    
In diesem Codebeispiel verwendet eine vom Anbieter gehosteten-add-in zum Anzeigen der Suchergebnisse für den Benutzer, die enthalten alle Websites oder nur Teamwebsites, denen der Benutzer zugreifen kann. Im Beispiel dazu:

- Der Wert der Benutzerprofileigenschaft **Mich-Seite** überprüft.
    
- Erstellt eine Suche Abfragezeichenfolge Filter den Wert der Benutzerprofileigenschaft **Mich-Seite** zugeordnet.
    
- Führt die Suchabfrage und zeigt die Ergebnisse der Suchabfrage.

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="using-the-searchpersonalizedresults-app"></a>Verwenden der app Search.PersonalizedResults
<a name="sectionSection1"> </a>

Wenn Sie dieses Codebeispiel ausführen, wird eine vom Anbieter gehostete Anwendung angezeigt, wie in Abbildung 1 dargestellt. 

**Abbildung 1. Startseite der app Search.PersonalizedResults**

![Screenshot, der die Startseite der app Search.PersonalizedResults anzeigt](media/d5df9bb4-fa11-4bd6-91fd-c4d339687a8a.png)

Dieser Artikel beschreibt das Szenario **personalisierte ausführen das Durchsuchen von allen Websitevorlagen mit Profildaten** . **Personalisierte Suche ausführen** auswählen gibt gefilterte Suchergebnisse, die Teamwebsites nur, siehe Abbildung 2 enthalten. Beachten Sie, dass die **Vorlage** Spalte Websites vom Typ nur **STS** enthält.

**Abbildung 2. Suchergebnisse nur die Teamwebsites anzeigen**

![Screenshot der uchen Ergebnisse anzeigen nur für Teamwebsites](media/dde71d9f-a296-4bee-b48b-964f81193404.png)

Für die Verarbeitung von Szenarien Personalisierung, können Sie die Suchabfrage durch ändern:

- Lesen und den Wert der Benutzerprofileigenschaften für diesen Benutzer zu testen. In diesem Codebeispiel testet die **Über mich** -Eigenschaft für einen Wert der **Apptesten**.
    
- Nutzen einen bestimmten Kurs Aktion basierend auf dem Wert der Benutzerprofileigenschaft. Beispielsweise ist der Wert der **Über mich** Benutzerprofileigenschaft **Apptesten**, dieses Codebeispiel entfernt den Team Site Filter und liefert Suchergebnisse, die alle Websites enthalten.

### <a name="to-enter-apptest-in-the-about-me-user-profile-property"></a>Apptesten in über mich Benutzerprofileigenschaft eingeben

1. Am oberen Rand der Office 365-Website wählen Sie Ihr Profilbild und dann **Über mich**, wie in Abbildung 3 dargestellt.
    
2. Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.
    
3. Geben Sie **über mich** **Apptesten**.
    
4. Wählen Sie **Speichern und schließen**.

**Abbildung 3. Navigieren zu Profilseite des Benutzers über mich auswählen**

![Screenshot der Benutzerprofilseite mit über mich hervorgehoben.](media/a7eccfcd-68f7-44b9-8f32-14a0d2f60398.png)

Zurück zu des **Search.PersonalizedResults** vom Anbieter gehosteten-add-Ins, und wählen Sie **Personalisierte Search führen Sie** erneut. Das Add-in ändert den Filter für die Suchabfrage alle Websites anstelle von Teamwebsites nur, wie in Abbildung 4 angezeigt. Die **Vorlage** Spalte enthält nun mehrere verschiedene Vorlage Websitetypen.

**Abbildung 4. Alle Websites mit Suchergebnissen**

![Screenshot von Suchergebnissen alle Websites anzeigen](media/3af49550-cd2d-4e7e-af1d-5227a5603730.png)

Auswählen von **Personalisierten Suche ausführen** Ruft die **BtnPersonalizedSearch_Click** -Methode in "default.aspx.cs". **BtnPersonalizedSearch_Click** führt die folgenden Aktionen aus:

- Wird mit **PeopleManager** alle Benutzerprofileigenschaften für den Benutzer dieses Add-in ausführt.
    
- Ruft ab, und der Wert der Benutzerprofileigenschaft **Mich-Seite** überprüft. Wenn der Wert der Eigenschaft **Mich-Seite** **Apptesten**ist, ruft die Suchabfrage alle Websites, die mit der Abfragezeichenfolge `contentclass:"STS_Site"`. Wenn der Wert der Eigenschaft **Mich-Seite** nicht **Apptesten**ist, wird der Team Site Filter an die Abfragezeichenfolge angehängt ( `WebTemplate=STS`), und die Suchabfrage nur Teamwebsites abgerufen.
    
- Ruft die **ProcessQuery** -Methode zum Abrufen der Suchergebnisse basierend auf der angegebenen Abfragezeichenfolge an. **ProcessQuery** wird veranschaulicht, wie eine Liste mit Eigenschaften mit den Suchergebnissen zurückgegeben werden sollen.
    
- Ruft die **FormatResults** -Methode, um die Suchergebnisse in eine HTML-Tabelle zu formatieren.
    
> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```
protected void btnPersonalizedSearch_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Load user profile properties.
                PeopleManager peopleManager = new PeopleManager(clientContext);
                PersonProperties personProperties = peopleManager.GetMyProperties();
                clientContext.Load(personProperties);
                clientContext.ExecuteQuery();
                // Check the value of About Me. 
                string aboutMeValue = personProperties.UserProfileProperties["AboutMe"];
                string templateFilter = ResolveAdditionalFilter(aboutMeValue);
                // Build the query string.
                string query = "contentclass:\"STS_Site\" " + templateFilter;
                ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
                lblStatus2.Text = FormatResults(results);
            }
        }

private ClientResult<ResultTableCollection> ProcessQuery(ClientContext ctx, string keywordQueryValue)
        {
            KeywordQuery keywordQuery = new KeywordQuery(ctx);
            keywordQuery.QueryText = keywordQueryValue;
            keywordQuery.RowLimit = 500;
            keywordQuery.StartRow = 0;
            keywordQuery.SelectProperties.Add("Title");
            keywordQuery.SelectProperties.Add("SPSiteUrl");
            keywordQuery.SelectProperties.Add("Description");
            keywordQuery.SelectProperties.Add("WebTemplate");
            keywordQuery.SortList.Add("SPSiteUrl", Microsoft.SharePoint.Client.Search.Query.SortDirection.Ascending);
            SearchExecutor searchExec = new SearchExecutor(ctx);
            ClientResult<ResultTableCollection> results = searchExec.ExecuteQuery(keywordQuery);
            ctx.ExecuteQuery();
            return results;
        }
```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [User Profile Lösungen für SharePoint 2013 und SharePoint Online](user-profile-solutions-for-sharepoint.md)
    
-  [Search.PersonalizedResults-app](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
    
-  [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [UserProfile.Manipulation.CSOM.Console](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
    
-  [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration)
