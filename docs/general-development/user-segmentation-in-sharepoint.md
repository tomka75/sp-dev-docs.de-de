---
title: Benutzersegmentierung in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 60809bfb16706709b448ba2d0fb3849cf5a33277
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="user-segmentation-in-sharepoint"></a>Benutzersegmentierung in SharePoint
Zeigen Sie maßgeschneiderte Inhalte für von Ihnen definierte Benutzersegmente an – z. B. basierend auf Gebietsschema, Interessen, Geschlecht oder Empfehlungslinks –, indem Sie eine Kombination aus Ausdruckssätzen, dem Inhaltssuche-Webpart und Abfrageregeln in SharePoint verwenden.
SharePoint bietet die Bausteine, um die Inhalte, die Sie auf einer SharePoint-Website anzeigen, je nach bestimmten Attributen der Endbenutzer maßgeschneidert anzupassen, z. B. auf Basis des Geschlechts, des Wohnorts, ihrer Interessen oder Empfehlungslinks. Diese Gruppierungen von Benutzerattributen werden als Benutzersegmente bezeichnet. 
  
    
    

In SharePoint kann diese Benutzersegmentierungsfunktion in vielen Szenarios von Vorteil sein, z. B.:
- Anzeigen von verschiedenen Banner auf einer Seite je nach der Endbenutzer Geschlecht 
    
  
- Je nach Gebietsschema des Endbenutzers bietet verschiedene Rabatt anzeigen 
    
  
- Anzeigen von anderen Artikeln auf einer Seite je nach der Endbenutzer verweisende Link (der Website, die auf der Seite an den Endbenutzer geschaltet). 
    
  
Zum Implementieren der benutzersegmentierung in SharePoint, führen Sie drei Dinge: Erstellen des Ausdruckssatzes für jede Benutzersegment, erweitern Sie die Inhaltssuche-Webpart, um Ihre Benutzersegmente aufmerksam zu machen und dann Abfrageregeln für bestimmte Aktionen für jede Benutzersegment verwenden.
## <a name="prerequisites"></a>Voraussetzungen
<a name="SP15_Prerequisites"> </a>

Bevor Sie mit der Implementierung der Benutzersegmentierung in SharePoint beginnen, muss Folgendes in Ihrer Entwicklungsumgebung installiert sein:
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
In diesem Artikel wird davon ausgegangen, dass Sie Erfahrung zur Entwicklung von Webparts in SharePoint verfügen. Weitere Informationen zur Entwicklung von Webparts finden Sie unter  [Baustein: Webparts](http://msdn.microsoft.com/en-us/library/ee535520%28v=office.14%29.aspx)
  
    
    

## <a name="overview-on-adding-user-segmentation-functionality-to-your-sharepoint-site"></a>Übersicht über das Hinzufügen der benutzersegmentierungsfunktion zu Ihrer SharePoint-Website
<a name="SP15_Overview_User_Segmentation"> </a>

Abbildung 1 zeigt die grundlegenden Schritte zum Hinzufügen der benutzersegmentierungsfunktion zu Ihrer SharePoint-Website.
  
    
    

**Abbildung 1. Schritte zum Hinzufügen der benutzersegmentierungsfunktion zu Ihrer SharePoint-Website**

  
    
    

  
    
    
![Schritte zum Hinzufügen der Funktion für die Benutzersegmentierung](../images/SP15_User_Segmentation_with_ContentBySearchWebPart.jpg)
  
    
    

  
    
    

  
    
    

## <a name="create-a-term-set"></a>Erstellen des Ausdruckssatzes
<a name="SP15_Create_a_term_set"> </a>

Ein Ausdruck ist ein Wort oder Satz, das bzw. der einem Element in SharePoint zugeordnet werden kann. Ein Ausdruckssatz ist eine Sammlung verwandter Ausdrücke. Weitere Informationen finden Sie unter [Übersicht über verwaltete Metadaten in SharePoint](http://technet.microsoft.com/en-us/library/ee424402.aspx). Sie können Ausdruckssätze entweder mit dem SharePoint-Terminologiespeicher-Verwaltungstool oder programmgesteuert erstellen. 
  
    
    

> **Hinweis:** In den folgenden Themen finden Sie ausführliche Anweisungen zum Erstellen eines Ausdruckssatzes mit dem Terminologiespeicher-Verwaltungstool:> [Einrichten neuer Ausdruckssätze](http://office.microsoft.com/en-us/sharepoint-help/set-up-a-new-term-set-HA102922634.aspx)> [Erstellen und Verwalten von Ausdrücken in einem Ausdruckssatz](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/create-and-manage-terms-in-a-term-set-HA102771989.aspx)
  
    
    

Sie können einen Ausdruckssatz mithilfe von Typen über  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) programmgesteuert erstellen. Im folgenden Codebeispiel wird veranschaulicht, wie ein **TermSet** -Objekt erstellt und die **NavigationTermSet**zu erhalten. Im nächsten Schritt erstellen Sie **Term** -Objekte innerhalb Ihrer **TermSet**. Schließlich übernehmen Sie diese Änderungen in der **TermStore** zu, und Laden Sie die **TermSet** für die Navigation verwenden.
  
    
    
Jeden Ausdruck in Ihre hinzugefügte Set erhält einen eindeutigen Bezeichner. Dieser Bezeichner wird der Schlüssel zum Erstellen der  [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) sollten Sie Ihre Benutzersegmente.
  
    
    



```cs

static void CreateNavigationTermSet(string siteUrl)
{
    using (SPSite site = new SPSite(siteUrl))
    {
        using (SPWeb web = site.OpenWeb())
        {
            TaxonomySession taxonomySession = new TaxonomySession(site);
            taxonomySession.UpdateCache();
            TermStore termStore = taxonomySession.DefaultSiteCollectionTermStore;

            // Create a TermSet object in a default site collection term group.
            Group siteCollectionGroup = termStore.GetSiteCollectionGroup(site, createIfMissing: true);
            TermSet termSet = siteCollectionGroup.CreateTermSet("Navigation Demo", Guid.NewGuid(), lcid: 1033);

            // Obtain navigation term set.
            NavigationTermSet navigationTermSet = NavigationTermSet.GetAsResolvedByWeb(termSet, web, "GlobalNavigationTaxonomyProvider");

            // Create a term that points to a SharePoint page set at the term set level of hierarchy.
            NavigationTerm term1 = navigationTermSet.CreateTerm("Term 1", NavigationLinkType.FriendlyUrl, Guid.NewGuid());

            // Create a term that points to an already existing URL outside of SharePoint.
            NavigationTerm term2 = navigationTermSet.CreateTerm("Term 2", NavigationLinkType.SimpleLink, Guid.NewGuid());
            term2.SimpleLinkUrl = "http://www.bing.com/";

            // Create a term that points to an existing SharePoint page.
            NavigationTerm term3 = navigationTermSet.CreateTerm("Term 3", NavigationLinkType.FriendlyUrl, Guid.NewGuid());

            // Save all changes to the term store.
            termStore.CommitAll();
        }
    }
}
```


## <a name="create-a-custom-web-part-for-user-segmentation"></a>Erstellen eines benutzerdefinierten Webparts für benutzersegmentierung
<a name="SP15_Create_a_custom_web_part_user_segmentation"> </a>

Erstellen Sie in Visual Studio 2012 ein benutzerdefiniertes Webpart unter Verwendung der Vorlage für visuelle Webparts in der SharePoint-Kategorie. Ihr benutzerdefiniertes Webpart muss vom [ContentBySearchWebPart](https://msdn.microsoft.com/en-us/library/office/microsoft.office.server.search.webcontrols.contentbysearchwebpart.aspx)-Objekt erben.
  
    
    

> **Hinweis:** In diesem Artikel wird davon ausgegangen, dass Sie Erfahrung mit der Entwicklung von Webparts in SharePoint haben. Weitere Informationen zur Entwicklung von Webparts finden Sie unter [Baustein: Webparts](http://msdn.microsoft.com/en-us/library/ee535520%28v=office.14%29.aspx)
  
    
    


## <a name="configure-a-custom-web-part-with-user-segmentation-logic"></a>Konfigurieren eines benutzerdefinierten-Webparts mit Benutzersegmentierungslogik
<a name="SP15_Configure_custom_web_part_user_segmentation_logic"> </a>

In Ihrer benutzerdefinierten Webparts können Sie die  [OnLoad()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.OnLoad.aspx) -Methode oder die [OnInit()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.OnInit.aspx) -Methode, um Ihre benutzerdefinierte Logik auszuführen erneut implementieren. Diese beiden Methoden sind hilfreich festzulegen oder Anpassen von Eigenschaften des [ContentBySearchWebPart](https://msdn.microsoft.com/en-us/library/office/microsoft.office.server.search.webcontrols.contentbysearchwebpart.aspx) -Objekts.
  
    
    

### <a name="example-1-add-male-and-female-user-segments-to-your-sharepoint-site"></a>Beispiel 1: Hinzufügen von männlichen und weiblichen Benutzersegmenten zu Ihrer SharePoint-Website

Um die Benutzersegmente **Männlich** und **Weiblich** hinzuzufügen, können Sie die [OnLoad()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.OnLoad.aspx)-Methode erneut implementieren, wie im folgenden Code dargestellt.
  
    
    

```cs

protected override void OnLoad(EventArgs e)
{
    if (this.AppManager != null)
    {
        if (this.AppManager.QueryGroups.ContainsKey(this.QueryGroupName) &amp;&amp; this.AppManager.QueryGroups[this.QueryGroupName].DataProvider != null)
        {
            this.AppManager.QueryGroups[this.QueryGroupName].DataProvider.BeforeSerializeToClient += new
                BeforeSerializeToClientEventHandler(AddMycustomProperties);
        }
    }
    base.OnLoad(e);
}
```

Die entsprechende **AddMycustomProperties** -Methode sieht wie im folgenden Code aus.
  
    
    



```cs

private void AddMycustomProperties(object sender, BeforeSerializeToClientEventArgs e)
{
    DataProviderScriptWebPart dp = sender as DataProviderScriptWebPart;
    string gender = (string)Page.Session["DataProvider.Gender"];
    // Depends on what your DataProvider is: Facebook, LinkedIn, etc.

    if (dp != null &amp;&amp; gender != null)
    {   try
        {
            // Set property to male or female GUID.
            if (gender.CompareTo("female") == 0)
            {
                dp.Properties["TermSetName"] = new String[] { "TermUniqueIdentifier" };
                // E.g. 47ba9139-a4c5-4ff0-8f9a-2864be32da92
            }
            else if(gender.CompareTo("male") == 0)
            {
                dp.Properties["UserSegmentTerms"] = new String[] { "TermUniqueIdentifier" };
                // E.g. f5bf2195-2170-4b11-a018-a688a285e579
            }
        }
        catch (ArgumentException exp)
        {
             // Do something with the exception.
        }
   }
}
```


### <a name="example-2-create-user-segments-based-on-the-type-of-web-browser-your-end-user-is-using-when"></a>Beispiel 2: Erstellen von Benutzersegmenten abhängig vom Typ des vom Endbenutzer verwendeten Webbrowsers

Um Benutzersegmente basierend auf dem Typ des Webbrowsers zu erstellen, den der Endbenutzer zum Anzeigen Ihrer SharePoint-Website verwendet, implementieren Sie die **OnLoad**-Methode erneut, wie im folgenden Code dargestellt.
  
    
    

```cs

protected override void OnLoad(EventArgs e)
{
    if (this.AppManager != null)
    {
        if (this.AppManager.QueryGroups.ContainsKey(this.QueryGroupName) &amp;&amp; this.AppManager.QueryGroups[this.QueryGroupName].DataProvider != null)
        {
             this.AppManager.QueryGroups[this.QueryGroupName].DataProvider.BeforeSerializeToClient += new 
                 BeforeSerializeToClientEventHandler(AddMycustomProperties);
        }
    }
    base.OnLoad(e);
}
```

Der Code für die **AddMycustomProperties**-Methode würde wie im folgenden Beispiel aussehen.
  
    
    



```cs

private void AddMycustomProperties(object sender, BeforeSerializeToClientEventArgs e)
{
    DataProviderScriptWebPart dataProvider = sender as DataProviderScriptWebPart;
    SPSite site = SPContext.Current.Site;
  
    TaxonomySession session = new TaxonomySession(site);
    TermStore defaultSiteCollectionStore = session.DefaultSiteCollectionTermStore;
    List<string> userSegmentTerms = new List<string>();

    var userAgentparts = Page.Request.UserAgent.Split(new char[] { ';', '(', ')' });

    foreach (var part in userAgentparts)
    {
        var entry = part.Trim();
        var terms = termStore.GetTermsWithCustomProperty("UserAgent", entry, false);

            if (terms.Count > 0)
            {
                userSegmentTerms.Add(terms[0].Id.ToString());
            }
    }
    dataProvider.Properties["UserSegmentTerms"] = userSegmentTerms.ToArray();
}
```


## <a name="upload-the-custom-web-part-to-the-sharepoint-web-part-gallery"></a>Hochladen Sie das benutzerdefinierte Webpart auf der SharePoint-Webpartkatalog
<a name="SP15_Upload_custom_web_part"> </a>

Um das benutzerdefinierte Webpart auf der Seite verwenden, müssen Sie das Webpart in der **SharePoint Web Part Gallery**hoch.
  
    
    
Wählen Sie in der **SharePoint Web Part Gallery** **Websiteeinstellungen** aus, und wählen Sie dann auf **Webparts** im Rahmen der **Web-Designer-Kataloge**. Wählen Sie auf der Registerkarte **Dateien** **Dokument hochladen**.
  
    
    

## <a name="add-query-rules-to-carry-out-specific-actions-that-depend-on-the-user-segment"></a>Fügen Sie Abfrageregeln, um bestimmte Aktionen auszuführen, die abhängig von der Benutzersegment hinzu
<a name="SP15_Add_query_rules_to_carry_out_actions"> </a>

Eine Abfrageregel überträgt Abfragen zur Verbesserung der Relevanz von Suchergebnissen durch Intelligent reagieren, was der Benutzer möglicherweise versucht, zu erhalten. In einer Abfrageregel Geben Sie Bedingung und Aktion korrelierte. Wenn eine Abfrage die Bedingungen in einer Abfrageregel erfüllt, führt das Suchsystem die Aktionen in der Regel zur Verbesserung der Relevanz der Suchergebnisse, wie die Ergebnisse Eingrenzung oder Ändern der Reihenfolge, in der Ergebnisse angezeigt werden, angegeben.
  
    
    
Bei der Implementierung der benutzersegmentierung verwenden Sie Abfrageregeln, um Bedingungen und Aktionen für die Segmente definierten Benutzer zu definieren. Wenn ein Endbenutzer einen bestimmten Benutzersegment gehört, die Abfrageregel wird aktiviert, und die  [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebConrols.ContentBySearchWebPart.aspx) zeigt Inhalte, die für dieses Segment bestimmten Benutzer zugeschnitten ist.
  
    
    

### <a name="to-create-a-query-rule-that-will-activate-for-a-particular-user-segment"></a>Erstellen eine Abfrageregel, die für ein bestimmtes Benutzersegment aktivieren


1. Wählen Sie in der veröffentlichungswebsitesammlung in den **Websiteeinstellungen** **Die Verwaltung von Websitesammlungen**, und wählen Sie dann auf **Suchabfrageregeln**. 
    
  
2. Wählen Sie eine ergebnisquelle aus, und wählen Sie dann auf **Neue Abfrageregel**.
    
  
3. Geben Sie im Feld **Regelname** einen Regelnamen. Klicken Sie auf, um **Kontext** zu erweitern.
    
  
4. Klicken Sie im Abschnitt **Abfrage erfolgt über diese Benutzersegmente** wählen Sie **eine der folgenden Benutzersegmente**, und klicken Sie dann auf **Benutzersegment hinzufügen**.
    
  
5. Geben Sie im Feld **Titel** einen Namen für diese Benutzer Segment Abfrageregel ein. Wählen Sie **Add User Segment Begriff**.
    
  
6. Erweitern Sie den **Verwalteten Metadatendienst**, klicken Sie im Dialogfeld **Import von Ausdruck zu speichern**. Suchen Sie unter **Site Collection**; den Ausdruckssatz, der die benutzersegmentierung Begriffe enthält, die Sie zuvor definiert, in  [Erstellen des Ausdruckssatzes](#SP15_Create_a_term_set). Wählen Sie die Benutzersegment diese Abfrageregel angewendet werden soll. Klicken Sie auf **Speichern**.
    
  
7. Nennen Sie Ihre Benutzer Segment n im Dialogfeld **Benutzersegment hinzufügen**.
    
    Sie haben nun eine Abfrageregel auf ein Benutzersegment zugeordnet, das wiederum zu einem Benutzer Segment Ausdruck zugeordnet ist.
    
  
8. Wählen Sie unter **Abfragebedingungen** **Bedingung entfernen**. 
    
    Dies gibt an, dass die Abfrage, die in der  [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebConrols.ContentBySearchWebPart.aspx) konfiguriert die abfragebedingung fungiert.
    
  
9. Legen Sie die entsprechenden Aktionen, die Abfrageregel ausgeführt wird. Wählen Sie eine entsprechende Aktion, die Sie als Ergebnis - Ihrer Abfrageregel übernehmen möchten, klicken Sie im Abschnitt **Aktionen**. Sie können entweder **Heraufgestuft Ergebnis hinzufügen** oder **Hinzufügen eines Ergebnisblocks** auswählen.
    
  
10. Speichern Sie die Abfrageregel.
    
  
11. Wiederholen Sie die Schritte 1 bis 10 für die anderen Benutzersegmente, je nach den Aktionen, die Sie ausführen möchten.
    
  

## <a name="add-a-custom-web-part-to-the-sharepoint-page-and-configure-it-to-show-the-query-rule"></a>Der SharePoint-Seite ein benutzerdefiniertes Webpart hinzu und konfigurieren Sie, um die Abfrageregel anzuzeigen.
<a name="SP15_Add_custom_web_part_to_SharePoint"> </a>

Sie müssen Ihre benutzerdefinierten Webparts zu Ihrer SharePoint-Seite hinzufügen.
  
    
    

### <a name="to-add-your-custom-web-part"></a>So fügen Sie das benutzerdefinierte Webpart hinzu


1. Navigieren zu einer Kategorieseite, wählen Sie **Bearbeiten (Seite)**, und wählen Sie dann auf **Bearbeiten Seitenvorlage**.
    
  
2. Wählen Sie im oberen Bereich der Seite **Webpart hinzufügen**. Wählen Sie dann das benutzerdefinierte Webpart aus dem Dropdown-Menü in der oberen rechten Ecke des Webparts.
    
  
3. Klicken Sie auf **Webpart bearbeiten**.
    
  
4. Erweitern Sie den Abschnitt **Einstellungen**, und wählen Sie im Feld **Ergebnistabelle** **SpecialTermResults**. 
    
  
5. Speichern Sie Ihre Konfiguration.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Erstellen von Websites für SharePoint](https://officedevcentersite-release.azurewebsites.net/sharepoint/docs/general-development/build-sites-for-sharepoint)
    
  
-  [Einrichten von Benutzersegmentierung auf Laufwerk adaptive Erfahrung in einem Produktkatalog in SharePoint](http://blogs.msdn.com/b/adaptive_experiences_in_sharepoint_2013/archive/2012/11/14/set-up-user-segmentation-to-drive-adaptive-experiences-in-a-product-catalog-in-sharepoint.aspx)
    
  

  
    
    

