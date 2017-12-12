---
title: "Taxonomie Vorgänge Beispiel-app für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 32e7b535103dd20a988c1253afe7f505d6c0e6f0
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="taxonomy-operations-sample-app-for-sharepoint"></a>Taxonomie Vorgänge Beispiel-app für SharePoint

Sie können im Rahmen Ihrer Strategie für die Enterprise Content Management (ECM) erstellt und taxonomiedaten auf einer SharePoint-Liste lesen.
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Die Core.MMS Beispiel Konsolenanwendung zeigt, wie für die Interaktion mit den SharePoint verwalteten Metadatendienst erstellen und Abrufen von Ausdrücke, Ausdruckssätze und Gruppen. In diesem Beispiel werden auch in einer vom Anbieter gehosteten app, wie etwa einer ASP.NET MVC-Web-Anwendung ausgeführt. Verwenden Sie diese Lösung, wenn Sie möchten migrieren Begriffe zwischen SharePoint-Farmen oder Begriffe in Ihrer benutzerdefinierten Anwendung anzuzeigen.   

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zunächst die [Core.MMS](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) Beispiel-app des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Bevor Sie diese app ausführen, benötigen Sie Folgendes:

- Die URL der SharePoint-Website.
    
- In den verwalteten Metadatendienst Zugriffsberechtigung für den Ausdruck zu speichern. Abbildung 1 zeigt das Office 365 Administrationscenter, wo diese Berechtigungen zugewiesen werden. 
    
    **Abbildung 1. Zuweisen von Berechtigungen auf den Ausdruck speichern, in der SharePoint-Verwaltungskonsole**

    ![Screenshot des im SharePoint Administrationscenter mit den Terminologiespeicher, Taxonomie Begriff Store Suchfeld, Begriff Store Administratoren Feldern und hervorgehoben.](media/5a9d8c07-afce-4d9e-b0d1-10b28e089278.png)
    
Zuweisen von Berechtigungen auf den Terminologiespeicher

  1. Wählen Sie das Office 365 Administrationscenter **Ausdruck zu speichern**.
    
  2. Wählen Sie im **TAXONOMIETERMINOLOGIESPEICHER**den Ausdruckssatz, dass Sie ein Administrator zuweisen möchten.
    
  3. Geben Sie im **Ausdruck speichern Administratoren**die organisationskonto, die Berechtigungen für Administrator den Begriff erforderlich sind.

## <a name="using-the-coremms-sample-app"></a>Verwenden die Core.MMS Beispiel-app
<a name="sectionSection1"> </a>

Wenn Sie die Anwendung zu starten, eine Konsolenanwendung, die ähnlich wie in Abbildung 2 angezeigt. Sie werden aufgefordert, die URL Ihrer SharePoint 2013 oder SharePoint Online-Website und Ihre Anmeldeinformationen eingeben. 

**Abbildung 2. Core.MMS Konsolenanwendung**

![Screenshot der Konsole Core.MMS Beispiel-app für die SharePoint-Benutzername und Kennwort aufgefordert werden.](media/5ddaf3f1-2d7c-4818-9a9a-b0e905226db5.png)

Nachdem Sie die SharePoint-URL und Ihre Anmeldeinformationen angeben, tritt ein, der Benutzerauthentifizierung. Der folgende Code führt die Benutzerauthentifizierung in SharePoint Online.
    
> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
ClientContext cc = new ClientContext(siteUrl);
cc.AuthenticationMode = ClientAuthenticationMode.Default;
// For SharePoint Online.
cc.Credentials = new SharePointOnlineCredentials(userName, pwd);
```

Der folgende Code führt die Benutzerauthentifizierung in SharePoint Online dedizierte oder in einer lokalen SharePoint 2013-Farm.

```C#
ClientContext cc = new ClientContext(siteUrl);
cc.AuthenticationMode = ClientAuthenticationMode.Default;
// For SharePoint Online Dedicated or on-premises .
cc.Credentials = new NetworkCredential(userName, pwd);
```

Die **CreateNecessaryMMSTermsToCloud** -Methode erstellt eine Gruppe, Ausdruckssatz und mehrere Begriffe in den verwalteten Metadatendienst. Der Code ruft zuerst einem Verweis auf das **TaxonomySession** -Objekt, klicken Sie dann das **TermStore** -Objekt vor dem Erstellen der benutzerdefinierten **TermGroup** **TermSet**und neue Ausdrücke. 

```C#
private static void CreateNecessaryMMSTermsToCloud(ClientContext cc)
        {
            // Get access to taxonomy CSOM.
            TaxonomySession taxonomySession = TaxonomySession.GetTaxonomySession(cc);
            cc.Load(taxonomySession);
            cc.ExecuteQuery();

            if (taxonomySession != null)
            {
                TermStore termStore = taxonomySession.GetDefaultSiteCollectionTermStore();
                if (termStore != null)
                {
                    //
                    // Create group, termset, and terms.
                    //
                    TermGroup myGroup = termStore.CreateGroup("Custom", Guid.NewGuid());
                    TermSet myTermSet = myGroup.CreateTermSet("Colors", Guid.NewGuid(), 1033);
                    myTermSet.CreateTerm("Red", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Orange", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Yellow", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Green", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Blue", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Purple", 1033, Guid.NewGuid());

                    cc.ExecuteQuery();
                }
            }
        }
```

Nach dem Erstellen der neue Ausdrücke, ruft die **GetMMSTermsFromCloud()** -Methode alle ausdrucksgruppen, Ausdruckssätze und Ausdrücke aus den verwalteten Metadatendienst. Mit der **CreateNecessaryMMSTermsToCloud()** -Methode vergleichbar, ruft der Code zuerst einen Verweis auf das **TaxonomySession** -Objekt, das **TermStore** -Objekt, vor dem Abrufen und Anzeigen der Begriff Informationen.

```C#
private static void GetMMSTermsFromCloud(ClientContext cc)
        {
            //
            // Load up the taxonomy item names.
            //
            TaxonomySession taxonomySession = TaxonomySession.GetTaxonomySession(cc);
            TermStore termStore = taxonomySession.GetDefaultSiteCollectionTermStore();
            cc.Load(termStore,
                    store => store.Name,
                    store => store.Groups.Include(
                        group => group.Name,
                        group => group.TermSets.Include(
                            termSet => termSet.Name,
                            termSet => termSet.Terms.Include(
                                term => term.Name)
                        )
                    )
            );
            cc.ExecuteQuery();

            //
            // Writes the taxonomy item names.
            //
            if (taxonomySession != null)
            {
                if (termStore != null)
                {
                    foreach (TermGroup group in termStore.Groups)
                    {
                        Console.WriteLine("Group " + group.Name);

                        foreach (TermSet termSet in group.TermSets)
                        {
                            Console.WriteLine("TermSet " + termSet.Name);

                            foreach (Term term in termSet.Terms)
                            {
                                // Writes root-level terms only.
                                Console.WriteLine("Term " + term.Name);
                            }
                        }
                    }
                }
            }
        }
```

Die Begriff Daten aus der verwalteten Metadatendienst in der Konsolenanwendung angezeigt, wie in Abbildung 3 dargestellt, und speichern in den Ausdruck in Ihrer verwalteten Metadatendienst, wird angezeigt, wie in Abbildung 4 dargestellt.

**Abbildung 3. Anzeigen von Gruppen, Ausdruckssätze und Ausdrücke in den verwalteten Metadatendienst Konsolenanwendung**

![Screenshot der Konsole an, mit dem Begriff Daten ausgegeben.](media/a8907a10-8b4d-463f-89bc-811f9af4b34e.png)

**Abbildung 4. SharePoint Administrationscenter, in dem Gruppen, Ausdruckssätze und Ausdrücke in den verwalteten Metadatendienst**

![Screenshot von der SharePoint-Verwaltungskonsole mit der taxonomieterminologiespeicher erweitert.](media/9e623deb-569b-457a-ad1c-fa6d0d4d0a38.png)

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [Core.MMSSync-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)
    
-  [Core.ContentTypesAndFields-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ContentTypesAndFields)
