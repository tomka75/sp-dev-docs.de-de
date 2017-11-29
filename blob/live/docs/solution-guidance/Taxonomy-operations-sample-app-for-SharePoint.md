---
title: "Taxonomie Vorgänge Beispiel-app für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c50bfe1afada0cfe907c4e11c4d2d6c6eb772b41
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="taxonomy-operations-sample-app-for-sharepoint"></a><span data-ttu-id="9eab9-102">Taxonomie Vorgänge Beispiel-app für SharePoint</span><span class="sxs-lookup"><span data-stu-id="9eab9-102">Taxonomy operations sample app for SharePoint</span></span>

<span data-ttu-id="9eab9-103">Sie können im Rahmen Ihrer Strategie für die Enterprise Content Management (ECM) erstellt und taxonomiedaten auf einer SharePoint-Liste lesen.</span><span class="sxs-lookup"><span data-stu-id="9eab9-103">As part of your Enterprise Content Management (ECM) strategy, you can create and read taxonomy data on a SharePoint list.</span></span>
    
<span data-ttu-id="9eab9-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="9eab9-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="9eab9-105">Die Core.MMS Beispiel Konsolenanwendung zeigt, wie für die Interaktion mit den SharePoint verwalteten Metadatendienst erstellen und Abrufen von Ausdrücke, Ausdruckssätze und Gruppen.</span><span class="sxs-lookup"><span data-stu-id="9eab9-105">The Core.MMS sample console application shows you how to interact with the SharePoint managed metadata service to create and retrieve terms, term sets, and groups.</span></span> <span data-ttu-id="9eab9-106">In diesem Beispiel werden auch in einer vom Anbieter gehosteten app, wie etwa einer ASP.NET MVC-Web-Anwendung ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="9eab9-106">This sample will also run in a provider-hosted app, such as an ASP.NET MVC web application.</span></span> <span data-ttu-id="9eab9-107">Verwenden Sie diese Lösung, wenn Sie möchten migrieren Begriffe zwischen SharePoint-Farmen oder Begriffe in Ihrer benutzerdefinierten Anwendung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="9eab9-107">Use this solution if you want to migrate terms between SharePoint farms or display terms in your custom app.</span></span>   

## <a name="before-you-begin"></a><span data-ttu-id="9eab9-108">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="9eab9-108">Before you begin</span></span>
<span data-ttu-id="9eab9-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="9eab9-109"></span></span>

<span data-ttu-id="9eab9-110">Laden Sie Sie zunächst die [Core.MMS](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) Beispiel-app des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="9eab9-110">To get started, download the  [Core.MMS](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) sample app from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="9eab9-111">Bevor Sie diese app ausführen, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="9eab9-111">Before you run this app, you'll need:</span></span>

- <span data-ttu-id="9eab9-112">Die URL der SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="9eab9-112">The URL of your SharePoint site.</span></span>
    
- <span data-ttu-id="9eab9-113">In den verwalteten Metadatendienst Zugriffsberechtigung für den Ausdruck zu speichern.</span><span class="sxs-lookup"><span data-stu-id="9eab9-113">Permission to access the term store in the managed metadata service.</span></span> <span data-ttu-id="9eab9-114">Abbildung 1 zeigt das Office 365 Administrationscenter, wo diese Berechtigungen zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="9eab9-114">Figure 1 shows the Office 365 admin center where these permissions are assigned.</span></span> 
    
    <span data-ttu-id="9eab9-115">**Abbildung 1. Zuweisen von Berechtigungen auf den Ausdruck speichern, in der SharePoint-Verwaltungskonsole**</span><span class="sxs-lookup"><span data-stu-id="9eab9-115">**Figure 1. Assigning permissions to the term store in the SharePoint admin center**</span></span>

    ![Screenshot des im SharePoint Administrationscenter mit den Terminologiespeicher, Taxonomie Begriff Store Suchfeld, Begriff Store Administratoren Feldern und hervorgehoben.](media/5a9d8c07-afce-4d9e-b0d1-10b28e089278.png)
    
<span data-ttu-id="9eab9-117">Zuweisen von Berechtigungen auf den Terminologiespeicher</span><span class="sxs-lookup"><span data-stu-id="9eab9-117">To assign permissions to the term store:</span></span>

  1. <span data-ttu-id="9eab9-118">Wählen Sie das Office 365 Administrationscenter **Ausdruck zu speichern**.</span><span class="sxs-lookup"><span data-stu-id="9eab9-118">From the Office 365 admin center, choose  **term store**.</span></span>
    
  2. <span data-ttu-id="9eab9-119">Wählen Sie im **TAXONOMIETERMINOLOGIESPEICHER**den Ausdruckssatz, dass Sie ein Administrator zuweisen möchten.</span><span class="sxs-lookup"><span data-stu-id="9eab9-119">In  **TAXONOMY TERM STORE**, choose the term set that you want to assign an administrator to.</span></span>
    
  3. <span data-ttu-id="9eab9-120">Geben Sie im **Ausdruck speichern Administratoren**die organisationskonto, die Berechtigungen für Administrator den Begriff erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="9eab9-120">In  **Term Store Administrators**, enter the organizational account that requires term store administrator permissions.</span></span>

## <a name="using-the-coremms-sample-app"></a><span data-ttu-id="9eab9-121">Verwenden die Core.MMS Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="9eab9-121">Using the Core.MMS sample app</span></span>
<span data-ttu-id="9eab9-122"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="9eab9-122"></span></span>

<span data-ttu-id="9eab9-123">Wenn Sie die Anwendung zu starten, eine Konsolenanwendung, die ähnlich wie in Abbildung 2 angezeigt.</span><span class="sxs-lookup"><span data-stu-id="9eab9-123">When you start the app, you see a console application similar to Figure 2.</span></span> <span data-ttu-id="9eab9-124">Sie werden aufgefordert, die URL Ihrer SharePoint 2013 oder SharePoint Online-Website und Ihre Anmeldeinformationen eingeben.</span><span class="sxs-lookup"><span data-stu-id="9eab9-124">You are prompted to enter the URL of your SharePoint 2013 or SharePoint Online site and your credentials.</span></span> 

<span data-ttu-id="9eab9-125">**Abbildung 2. Core.MMS Konsolenanwendung**</span><span class="sxs-lookup"><span data-stu-id="9eab9-125">**Figure 2. Core.MMS console application**</span></span>

![Screenshot der Konsole Core.MMS Beispiel-app für die SharePoint-Benutzername und Kennwort aufgefordert werden.](media/5ddaf3f1-2d7c-4818-9a9a-b0e905226db5.png)

<span data-ttu-id="9eab9-127">Nachdem Sie die SharePoint-URL und Ihre Anmeldeinformationen angeben, tritt ein, der Benutzerauthentifizierung.</span><span class="sxs-lookup"><span data-stu-id="9eab9-127">After you supply the SharePoint URL and your credentials, user authentication occurs.</span></span> <span data-ttu-id="9eab9-128">Der folgende Code führt die Benutzerauthentifizierung in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="9eab9-128">The following code performs user authentication in SharePoint Online.</span></span>
    
<span data-ttu-id="9eab9-129">**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.</span><span class="sxs-lookup"><span data-stu-id="9eab9-129">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
ClientContext cc = new ClientContext(siteUrl);
cc.AuthenticationMode = ClientAuthenticationMode.Default;
// For SharePoint Online.
cc.Credentials = new SharePointOnlineCredentials(userName, pwd);
```

<span data-ttu-id="9eab9-130">Der folgende Code führt die Benutzerauthentifizierung in SharePoint Online dedizierte oder in einer lokalen SharePoint 2013-Farm.</span><span class="sxs-lookup"><span data-stu-id="9eab9-130">The following code performs user authentication in SharePoint Online Dedicated or in an on-premises SharePoint 2013 farm.</span></span>

```C#
ClientContext cc = new ClientContext(siteUrl);
cc.AuthenticationMode = ClientAuthenticationMode.Default;
// For SharePoint Online Dedicated or on-premises .
cc.Credentials = new NetworkCredential(userName, pwd);
```

<span data-ttu-id="9eab9-131">Die **CreateNecessaryMMSTermsToCloud** -Methode erstellt eine Gruppe, Ausdruckssatz und mehrere Begriffe in den verwalteten Metadatendienst.</span><span class="sxs-lookup"><span data-stu-id="9eab9-131">The  **CreateNecessaryMMSTermsToCloud** method creates a group, term set, and several terms in the managed metadata service.</span></span> <span data-ttu-id="9eab9-132">Der Code ruft zuerst einem Verweis auf das **TaxonomySession** -Objekt, klicken Sie dann das **TermStore** -Objekt vor dem Erstellen der benutzerdefinierten **TermGroup** **TermSet**und neue Ausdrücke.</span><span class="sxs-lookup"><span data-stu-id="9eab9-132">The code first gets a reference to the **TaxonomySession** object, then the **TermStore** object, before creating the custom **TermGroup**,  **TermSet**, and new terms.</span></span> 

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

<span data-ttu-id="9eab9-133">Nach dem Erstellen der neue Ausdrücke, ruft die **GetMMSTermsFromCloud()** -Methode alle ausdrucksgruppen, Ausdruckssätze und Ausdrücke aus den verwalteten Metadatendienst.</span><span class="sxs-lookup"><span data-stu-id="9eab9-133">After creating the new terms, the  **GetMMSTermsFromCloud()** method retrieves all term groups, term sets, and terms from the managed metadata service.</span></span> <span data-ttu-id="9eab9-134">Mit der **CreateNecessaryMMSTermsToCloud()** -Methode vergleichbar, ruft der Code zuerst einen Verweis auf das **TaxonomySession** -Objekt, das **TermStore** -Objekt, vor dem Abrufen und Anzeigen der Begriff Informationen.</span><span class="sxs-lookup"><span data-stu-id="9eab9-134">Similar to the **CreateNecessaryMMSTermsToCloud()** method, the code first gets a reference to the **TaxonomySession** object, then the **TermStore** object, before retrieving and displaying the term information.</span></span>

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

<span data-ttu-id="9eab9-135">Die Begriff Daten aus der verwalteten Metadatendienst in der Konsolenanwendung angezeigt, wie in Abbildung 3 dargestellt, und speichern in den Ausdruck in Ihrer verwalteten Metadatendienst, wird angezeigt, wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="9eab9-135">You will see your term data from your managed metadata service displayed in the console application, as shown in Figure 3, and in the term store in your managed metadata service, as shown in Figure 4.</span></span>

<span data-ttu-id="9eab9-136">**Abbildung 3. Anzeigen von Gruppen, Ausdruckssätze und Ausdrücke in den verwalteten Metadatendienst Konsolenanwendung**</span><span class="sxs-lookup"><span data-stu-id="9eab9-136">**Figure 3. Console application showing Groups, TermSets, and Terms in the managed metadata service**</span></span>

![Screenshot der Konsole an, mit dem Begriff Daten ausgegeben.](media/a8907a10-8b4d-463f-89bc-811f9af4b34e.png)

<span data-ttu-id="9eab9-138">**Abbildung 4. SharePoint Administrationscenter, in dem Gruppen, Ausdruckssätze und Ausdrücke in den verwalteten Metadatendienst**</span><span class="sxs-lookup"><span data-stu-id="9eab9-138">**Figure 4. SharePoint admin center showing Groups, TermSets, and Terms in the managed metadata service**</span></span>

![Screenshot von der SharePoint-Verwaltungskonsole mit der taxonomieterminologiespeicher erweitert.](media/9e623deb-569b-457a-ad1c-fa6d0d4d0a38.png)

## <a name="additional-resources"></a><span data-ttu-id="9eab9-140">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9eab9-140">Additional resources</span></span>
<span data-ttu-id="9eab9-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9eab9-141"></span></span>

-  [<span data-ttu-id="9eab9-142">Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="9eab9-142">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="9eab9-143">Core.MMSSync-Beispiel</span><span class="sxs-lookup"><span data-stu-id="9eab9-143">Core.MMSSync sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)
    
-  [<span data-ttu-id="9eab9-144">Core.ContentTypesAndFields-Beispiel</span><span class="sxs-lookup"><span data-stu-id="9eab9-144">Core.ContentTypesAndFields sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ContentTypesAndFields)
