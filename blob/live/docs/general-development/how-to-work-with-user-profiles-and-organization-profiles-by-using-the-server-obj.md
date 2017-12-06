---
title: Vorgehensweise Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 13f16dc3-f652-4fb3-996b-5f2166236d2b
ms.openlocfilehash: bbafd85e96f16d89481a3d1dba3ed06893b56c92
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-object-model-in-sharepoint"></a><span data-ttu-id="40be0-102">Vorgehensweise: Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="40be0-102">How to: Work with user profiles and organization profiles by using the server object model in SharePoint</span></span>
<span data-ttu-id="40be0-103">In diesem Artikel erfahren Sie, wie Sie Benutzerprofile und Benutzerprofileigenschaften in SharePoint programmgesteuert mithilfe des SharePoint-Serverobjektmodells erstellen, abrufen und ändern können.</span><span class="sxs-lookup"><span data-stu-id="40be0-103">Learn how to create, retrieve, and change SharePoint user profiles and user profile properties programmatically by using the SharePoint server object model.</span></span>
## <a name="what-are-user-profiles-in-sharepoint"></a><span data-ttu-id="40be0-104">Was sind Benutzerprofile in SharePoint?</span><span class="sxs-lookup"><span data-stu-id="40be0-104">What are user profiles in SharePoint?</span></span>

<span data-ttu-id="40be0-p101">Benutzerprofile stellen in SharePoint SharePoint-Benutzer dar. Benutzerprofileigenschaften stellen Informationen über die Benutzer und über die Eigenschaften selbst dar. Eigenschaften umfassen beispielsweise den Kontonamen oder die E-Mail-Adresse eines Benutzers und den Datentyp einer Eigenschaft. Sie können das Serverobjektmodell verwenden, um Benutzerprofile, Profiluntertypen und Profileigenschaften zu erstellen, abzurufen und zu ändern.</span><span class="sxs-lookup"><span data-stu-id="40be0-p101">In SharePoint, user profiles represent SharePoint users. User profile properties represent information about the users and also about the properties themselves. For example, properties include the account name or email address of a user and the data type of a property. You can use the server object model to programmatically create, retrieve, and change user profiles, profile subtypes, and profile properties.</span></span>
  
    
    

> <span data-ttu-id="40be0-109">**Hinweis:** Weitere Informationen zu gängigen Programmierungsaufgaben bei der Arbeit mit Benutzerprofilen und der zur Aufgabenausführung verwendeten API finden Sie unter [Work with user profiles in SharePoint](work-with-user-profiles-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="40be0-109">**Note** For more information about common programming tasks for working with user profiles and the API that you use to perform the tasks, see  [Work with user profiles in SharePoint](work-with-user-profiles-in-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-user-profiles-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="40be0-110">Voraussetzungen für die Einrichtung der Entwicklungsumgebung für die Arbeit mit Benutzerprofilen mithilfe des SharePoint-Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="40be0-110">Prerequisites for setting up your development environment to work with user profiles by using the SharePoint server object model</span></span>
<span data-ttu-id="40be0-111"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="40be0-111"></span></span>

<span data-ttu-id="40be0-112">Zur Erstellung einer Konsolenanwendung, die das Serverobjektmodell für die Arbeit mit Benutzerprofilen und Benutzerprofileigenschaften verwendet, benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="40be0-112">To create a console application that uses the server object model to work with user profiles and user profile properties, you'll need:</span></span>
  
    
    

- <span data-ttu-id="40be0-113">SharePoint mit dem für den aktuellen Benutzer erstellten Profil</span><span class="sxs-lookup"><span data-stu-id="40be0-113">SharePoint Server 2013 with the profile created for the current user.</span></span>
    
  
- <span data-ttu-id="40be0-114">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="40be0-114">Visual Studio 2012.</span></span>
    
  
- <span data-ttu-id="40be0-p102">Berechtigungen zum Erstellen, Abrufen und Ändern der Benutzerprofilobjekte. (Für das Erstellen und Ändern der Profile ist die Berechtigung **Benutzerprofile ändern** erforderlich.)</span><span class="sxs-lookup"><span data-stu-id="40be0-p102">Permissions to create, retrieve, and change user profile objects. (Creating and modifying profiles requires the **Modify User Profiles** permission.)</span></span>
    
  

## <a name="create-a-console-application-that-works-with-user-profiles-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="40be0-117">Erstellen einer mit Benutzerprofilen funktionierenden Konsolenanwendung mithilfe des SharePoint-Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="40be0-117">Create a console application that works with user profiles by using the SharePoint server object model</span></span>
<span data-ttu-id="40be0-118"><a name="bkmk_CreateConsoleApp"> </a></span><span class="sxs-lookup"><span data-stu-id="40be0-118"></span></span>


1. <span data-ttu-id="40be0-119">Öffnen Sie Visual Studio, und wählen Sie **Datei**, **Neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="40be0-119">Open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="40be0-120">Wählen Sie im Dialogfeld **Neues Projekt** aus der Dropdownliste oben im Dialogfeld die Option **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="40be0-120">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="40be0-121">Wählen Sie in der Liste **Vorlagen** **Windows** und dann **Konsolenanwendung**.</span><span class="sxs-lookup"><span data-stu-id="40be0-121">In the **Templates** list, choose **Windows**, and then choose **Console Application**.</span></span>
    
  
4. <span data-ttu-id="40be0-122">Geben Sie dem Projekt den Namen „UserProfilesSSOM“, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="40be0-122">Name the project UserProfilesSSOM, and then choose the **OK** button.</span></span>
    
  > <span data-ttu-id="40be0-123">Hinweis: Vergewissern Sie sich, dass die Einstellung **32-Bit bevorzugen** in den **Buildeigenschaften** des Projekts deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="40be0-123">Note Make sure the Prefer 32-bit setting is not selected in the project's Build properties.</span></span>

5. <span data-ttu-id="40be0-124">Fügen Sie Verweise auf die folgenden Assemblys hinzu:</span><span class="sxs-lookup"><span data-stu-id="40be0-124">Add references to the following assemblies:</span></span>
    
  - <span data-ttu-id="40be0-125">Microsoft.Office.Server</span><span class="sxs-lookup"><span data-stu-id="40be0-125">Microsoft.Office.Server</span></span>
  - <span data-ttu-id="40be0-126">Microsoft.Office.Server.UserProfiles</span><span class="sxs-lookup"><span data-stu-id="40be0-126">Microsoft.Office.Server.UserProfiles</span></span>
  - <span data-ttu-id="40be0-127">Microsoft.SharePoint</span><span class="sxs-lookup"><span data-stu-id="40be0-127">Microsoft.SharePoint</span></span>
  - <span data-ttu-id="40be0-128">System.Web</span><span class="sxs-lookup"><span data-stu-id="40be0-128">System.Web</span></span>

  
6. <span data-ttu-id="40be0-129">Ersetzen Sie die Inhalte der **Program**-Klasse durch das Codebeispiel aus einem der folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="40be0-129">Replace the contents of the **Program** class with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="40be0-130">Erstellen eines Benutzerprofils</span><span class="sxs-lookup"><span data-stu-id="40be0-130">Create a user profile</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_CreateUP)
  -  [<span data-ttu-id="40be0-131">Erstellen einer Benutzerprofileigenschaft</span><span class="sxs-lookup"><span data-stu-id="40be0-131">Create a user profile property</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_CreateUPProp)
  -  [<span data-ttu-id="40be0-132">Abrufen und Ändern von Benutzerprofilen</span><span class="sxs-lookup"><span data-stu-id="40be0-132">Retrieve and change user profiles</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_GetChangeUP)
  -  [<span data-ttu-id="40be0-133">Abrufen und Ändern der Attribute für Benutzerprofile</span><span class="sxs-lookup"><span data-stu-id="40be0-133">Retrieve and change attributes for user profile properties</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_GetChangePropAttributes)
  -  [<span data-ttu-id="40be0-134">Abrufen und Ändern der Werte für Benutzereigenschaften</span><span class="sxs-lookup"><span data-stu-id="40be0-134">Retrieve and change values for user properties</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_GetChangePropValues)
    
  
7. <span data-ttu-id="40be0-p103">Wählen Sie zum Testen der Konsolenanwendung auf der Menüleiste **Debuggen**, **Debuggen starten** aus. Sie können die Änderungen auf der Seite **Profildienst verwalten** für die Benutzerprofildienst-Anwendung in der SharePoint-Zentraladministration überprüfen.</span><span class="sxs-lookup"><span data-stu-id="40be0-p103">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**. You can check your changes from the **Manage Profile Service** page for the User Profile Service Application in Central Administration.</span></span>
    
  

## <a name="code-example-create-user-profiles-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="40be0-137">Codebeispiel: Erstellen von Benutzerprofilen mithilfe des SharePoint-Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="40be0-137">Code example: Create user profiles by using the SharePoint server object model</span></span>
<span data-ttu-id="40be0-138"><a name="bkmk_CreateUP"> </a></span><span class="sxs-lookup"><span data-stu-id="40be0-138"></span></span>

<span data-ttu-id="40be0-p104">Benutzerprofile stellen in SharePoint SharePoint-Benutzer dar. Profiltypen und Untertypen helfen bei der Kategorisierung von Profilen in Gruppen wie Mitarbeiter oder Kunden. Profiltypen und Untertypen werden zum Festlegen von allgemeinen Profileigenschaften und Attributen auf Untertypebene verwendet. SharePoint Server enthält einen standardmäßigen Benutzerprofil-Untertyp.</span><span class="sxs-lookup"><span data-stu-id="40be0-p104">In SharePoint, user profiles represent SharePoint users. Profile types and subtypes help categorize profiles into groups, such as employees or customers. Profile types and subtypes are used to set common profile properties and attributes at the subtype level. SharePoint Server includes a default user profile subtype.</span></span>
  
    
    
<span data-ttu-id="40be0-p105">Das folgende Codebeispiel erstellt ein  [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) -Objekt, das dem standardmäßigen Benutzerprofil-Untertyp zugeordnet ist. Einige Benutzerprofileigenschaften werden automatisch mit Informationen gefüllt, die aus dem Verzeichnis mit den Benutzerkonten importiert werden, z. B. Active Directory-Domänendienste. Ein Codebeispiel, mit dem ein benutzerdefinierter Untertyp erstellt wird, finden Sie unter [ProfileSubtype](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtype.aspx) .</span><span class="sxs-lookup"><span data-stu-id="40be0-p105">The following code example creates a  [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) object that is associated with the default user profile subtype. Some user profile properties are automatically populated with information that is imported from the directory that contains user accounts, such as Active Directory Domain Services. For a code example that creates a custom subtype, see [ProfileSubtype](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtype.aspx) .</span></span>
  
    
    

> <span data-ttu-id="40be0-146">**Hinweis:** Ändern Sie die Werte der Platzhalter „domain\\username“ und „servername“, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="40be0-146">**Note** Change the domain\\username andservername placeholder values before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "domain\\username" and "servername" with actual values.
            string newAccountName = "domain\\username";
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);
                try
                {

                    // Create a user profile that uses the default user profile
                    // subtype.
                    UserProfileManager userProfileMgr = new UserProfileManager(serviceContext);
                    UserProfile userProfile = userProfileMgr.CreateUserProfile(newAccountName);

                    Console.WriteLine("A profile was created for " + userProfile.DisplayName);
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="code-example-create-user-profile-properties-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="40be0-147">Codebeispiel: Erstellen von Benutzerprofileigenschaften mithilfe des SharePoint-Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="40be0-147">Code example: Create user profile properties by using the SharePoint server object model</span></span>
<span data-ttu-id="40be0-148"><a name="bkmk_CreateUPProp"> </a></span><span class="sxs-lookup"><span data-stu-id="40be0-148"></span></span>

<span data-ttu-id="40be0-p106">Benutzerprofileigenschaften beschreiben persönliche und Organisationsinformationen über Benutzer. Sie können eine benutzerdefinierte Profileigenschaft erstellen oder sie zu dem Standardsatz der SharePoint-Profileigenschaften hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="40be0-p106">User profile properties describe personal and organizational information about users. You can create and add a custom profile property to the default set of SharePoint profile properties.</span></span>
  
    
    
<span data-ttu-id="40be0-151">Eine Profileigenschaft und die dazugehörigen Attribute werden von einem Satz verknüpfter Objekte dargestellt: einem  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) -Objekt, einem [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) -Objekt und einem [ProfileSubtypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.aspx) -Objekt.</span><span class="sxs-lookup"><span data-stu-id="40be0-151">A profile property and its attributes are represented by a set of linked objects: a  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) object, a [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) object, and a [ProfileSubtypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.aspx) object.</span></span>
  
    
    
<span data-ttu-id="40be0-p107">Das folgende Codebeispiel erstellt einen  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) mit einem URL-Datentyp (oder optional einen [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) mit einem Zeichenfolgentyp mit mehreren Werten). Es erstellt auch einen [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) und einen [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) , die Verfügbarkeit, Datenschutz und weitere Einstellungen für die Eigenschaft definieren. Die [ProfileSubtypeProperty.DefaultPrivacy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.DefaultPrivacy.aspx) -Eigenschaft steuert die Sichtbarkeit der Eigenschaften und weiteren „Meine Website"-Inhalten. Eine vollständige Liste möglicher Datentypen für Profileigenschaftenwerte finden Sie unter [PropertyDataType](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyDataType.aspx) .</span><span class="sxs-lookup"><span data-stu-id="40be0-p107">The following code example creates a  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) that has a URL data type (or optionally a [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) that has a multivalue string data type). In addition, it creates a [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) and a [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) that define availability, privacy, and other settings for the property. The [ProfileSubtypeProperty.DefaultPrivacy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.DefaultPrivacy.aspx) property controls the visibility of properties and other My Site content. For a complete list of the possible data types for profile property values, see [PropertyDataType](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyDataType.aspx) .</span></span>
  
    
    

> <span data-ttu-id="40be0-156">**Hinweis:** Ändern Sie den Wert für den Platzhalter „servername“, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="40be0-156">**Note** Change the servername placeholder value before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.Administration;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "servername" with an actual value.
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);
                try
                {
                    ProfilePropertyManager profilePropMgr = new UserProfileConfigManager(serviceContext).ProfilePropertyManager;
                    CorePropertyManager corePropMgr = profilePropMgr.GetCoreProperties();

                    // Create a URL property.
                    CoreProperty coreProp = corePropMgr.Create(false);
                    coreProp.Name = "AppsWebsite";
                    coreProp.DisplayName = "Apps site";
                    coreProp.Type = PropertyDataType.URL;
                    coreProp.Length = 100;
                    corePropMgr.Add(coreProp);

                    //// Create a multivalue property.
                    //// To create this property, comment out the previous
                    //// block of code and uncomment this block of code.
                    //CoreProperty coreProp = corePropMgr.Create(false);
                    //coreProp.Name = "PublishedAppsList";
                    //coreProp.DisplayName = "Published apps";
                    //coreProp.Type = PropertyDataType.StringMultiValue;
                    //coreProp.IsMultivalued = true;
                    //coreProp.Length = 100;
                    //corePropMgr.Add(coreProp);

                    // Create a profile type property and make the core property 
                    // visible in the Details section page.
                    ProfileTypePropertyManager typePropMgr = profilePropMgr.GetProfileTypeProperties(ProfileType.User);
                    ProfileTypeProperty typeProp = typePropMgr.Create(coreProp);
                    typeProp.IsVisibleOnViewer = true;
                    typePropMgr.Add(typeProp);

                    // Create a profile subtype property.
                    ProfileSubtypeManager subtypeMgr = ProfileSubtypeManager.Get(serviceContext);
                    ProfileSubtype subtype = subtypeMgr.GetProfileSubtype(ProfileSubtypeManager.GetDefaultProfileName(ProfileType.User));
                    ProfileSubtypePropertyManager subtypePropMgr = profilePropMgr.GetProfileSubtypeProperties(subtype.Name);
                    ProfileSubtypeProperty subtypeProp = subtypePropMgr.Create(typeProp);
                    subtypeProp.IsUserEditable = true;
                    subtypeProp.DefaultPrivacy = Privacy.Public;
                    subtypeProp.UserOverridePrivacy = true;
                    subtypePropMgr.Add(subtypeProp);

                    Console.WriteLine("The properties were created.");
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="code-example-retrieve-and-change-user-profiles-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="40be0-157">Codebeispiel: Abrufen und Ändern von Benutzerprofilen mithilfe des SharePoint-Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="40be0-157">Code example: Retrieve and change user profiles by using the SharePoint server object model</span></span>
<span data-ttu-id="40be0-158"><a name="bkmk_GetChangeUP"> </a></span><span class="sxs-lookup"><span data-stu-id="40be0-158"></span></span>

<span data-ttu-id="40be0-p108">Das folgende Codebeispiel ruft alle Benutzerprofile innerhalb des Kontexts ab und ändert den Wert einer  [DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.DisplayName.aspx) -Benutzereigenschaft. Auf die meisten Profileigenschaften wird mit dem [UserProfile.Item](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.Item.aspx) -Accessor zugegriffen.</span><span class="sxs-lookup"><span data-stu-id="40be0-p108">The following code example retrieves all user profiles within the context and changes the value of a user's  [DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.DisplayName.aspx) property. Most profile properties are accessed by using the [UserProfile.Item](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.Item.aspx) accessor.</span></span>
  
    
    

> <span data-ttu-id="40be0-161">**Hinweis:** Ändern Sie die Werte der Platzhalter „domain\\username“ und „servername“, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="40be0-161">**Note** Change the domain\\username andservername placeholder values before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "domain\\username" and "servername" with actual values.
            string targetAccountName = "domain\\username";
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);
                try
                {

                    // Retrieve and iterate through all of the user profiles in this context.
                    Console.WriteLine("Retrieving user profiles:");
                    UserProfileManager userProfileMgr = new UserProfileManager(serviceContext);
                    IEnumerator userProfiles = userProfileMgr.GetEnumerator();
                    while (userProfiles.MoveNext())
                    {
                        UserProfile userProfile = (UserProfile)userProfiles.Current;
                        Console.WriteLine(userProfile.AccountName);
                    }

                    // Retrieve a specific user profile. Change the value of a user profile property
                    // and save (commit) the change on the server.
                    UserProfile user = userProfileMgr.GetUserProfile(targetAccountName);
                    Console.WriteLine("\\nRetrieving user profile for " + user.DisplayName + ".");
                    user.DisplayName = "Pat";
                    user.Commit();
                    Console.WriteLine("\\nThe user\\'s display name has been changed.");
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="code-example-retrieve-and-change-attributes-for-user-profile-properties-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="40be0-162">Codebeispiel: Abrufen und Ändern der Attribute von Benutzerprofileigenschaften mithilfe des SharePoint-Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="40be0-162">Code example: Retrieve and change attributes for user profile properties by using the SharePoint server object model</span></span>
<span data-ttu-id="40be0-163"><a name="bkmk_GetChangePropAttributes"> </a></span><span class="sxs-lookup"><span data-stu-id="40be0-163"></span></span>

<span data-ttu-id="40be0-p109">Das folgende Codebeispiel ruft den Eigenschaftensatz ab, der eine bestimmte Benutzereigenschaft und die dazugehörigen Attribute darstellt, und ändert dann die  [CoreProperty.DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.DisplayName.aspx) -, [ProfileTypeProperty.IsVisibleOnViewer](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.IsVisibleOnViewer.aspx) - und [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) -Attribute. Diese Änderungen gelten global für den Eigenschaftensatz. [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) gibt an, ob Benutzer einen Wert für die Eigenschaft angeben müssen. [PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) gilt nur für Benutzerprofileigenschaften.</span><span class="sxs-lookup"><span data-stu-id="40be0-p109">The following code example retrieves the set of properties that represent a specific user property and its attributes, and then it changes the  [CoreProperty.DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.DisplayName.aspx) attribute, [ProfileTypeProperty.IsVisibleOnViewer](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.IsVisibleOnViewer.aspx) attribute, and [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) attribute. These changes apply globally to the property set. [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) specifies whether users are required to provide a value for the property. [PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) applies to user profile properties only.</span></span>
  
    
    

> <span data-ttu-id="40be0-168">**Hinweis:** Ändern Sie den Wert für den Platzhalter „servername“, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="40be0-168">**Note** Change the servername placeholder value before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "servername" with an actual value.
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);
                try
                {
                    ProfilePropertyManager profilePropMgr = new UserProfileConfigManager(serviceContext).ProfilePropertyManager;
                    ProfileSubtypePropertyManager subtypePropMgr = profilePropMgr.GetProfileSubtypeProperties("UserProfile");

                    // Retrieve a specific property set (a profile subtype property and
                    // its associated core and profile type properties).
                    // Changing these properties affects all instances of this property set.
                    ProfileSubtypeProperty subtypeProp = subtypePropMgr.GetPropertyByName(PropertyConstants.Title);
                    CoreProperty coreProp = subtypeProp.CoreProperty;
                    ProfileTypeProperty typeProp = subtypeProp.TypeProperty;

                    Console.WriteLine("Property name: " + coreProp.DisplayName);
                    Console.WriteLine("IsVisibleOnViewer = " + typeProp.IsVisibleOnViewer);
                    Console.WriteLine("PrivacyPolicy = " + subtypeProp.PrivacyPolicy);
                    Console.WriteLine("Press Enter to change the values.");
                    Console.Read();

                    // Change attributes on the properties and save (commit) the changes
                    // on the server.
                    coreProp.DisplayName = "Position";
                    coreProp.Commit();
                    typeProp.IsVisibleOnViewer = true;
                    typeProp.Commit();
                    subtypeProp.PrivacyPolicy = PrivacyPolicy.OptOut;
                    subtypeProp.Commit();
                    Console.WriteLine("The property attributes have been changed.");
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="code-example-retrieve-and-change-values-for-user-properties-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="40be0-169">Codebeispiel: Abrufen und Ändern der Werte von Benutzereigenschaften mithilfe des SharePoint-Serverobjektmodells</span><span class="sxs-lookup"><span data-stu-id="40be0-169">Code example: Retrieve and change values for user properties by using the SharePoint server object model</span></span>
<span data-ttu-id="40be0-170"><a name="bkmk_GetChangePropValues"> </a></span><span class="sxs-lookup"><span data-stu-id="40be0-170"></span></span>

<span data-ttu-id="40be0-p110">Das folgende Beispiel ruft alle **UserProfile**-Typeigenschaften und Eigenschaftswerte für einen bestimmten Benutzer ab. Anschließend ändert es die  [PictureUrl](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PictureUrl.aspx) -Eigenschaft mit einem Wert und die [PastProjects](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PastProjects.aspx) -Eigenschaft mit mehreren Werten. Eine vollständige Liste der Profileigenschaften-Namenkonstanten finden Sie unter [PropertyConstants](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.aspx) .</span><span class="sxs-lookup"><span data-stu-id="40be0-p110">The following code example retrieves all **UserProfile** type properties and retrieves the property values for a specific user. Then, it changes the single-value [PictureUrl](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PictureUrl.aspx) property and the multivalue [PastProjects](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PastProjects.aspx) property. For the complete list of profile property name constants, see [PropertyConstants](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.aspx) .</span></span>
  
    
    

> <span data-ttu-id="40be0-174">**Hinweis:** Ändern Sie die Werte für die Platzhalter „domain\\username“, „http://servername/docLib/pic.jpg“ und „servername“, bevor Sie den Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="40be0-174">**Note** Change the domain\\username, http://servername/docLib/pic.jpg, and servername placeholder values before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "domain\\username," "http://servername/docLib/pic.jpg," and "servername" with actual values.
            string accountName = "domain\\username";
            string newPictureUrl = "http://servername/docLib/pic.jpg";
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);

                try
                {
                    UserProfileManager userProfileMgr = new UserProfileManager(serviceContext);
                    ProfilePropertyManager profilePropMgr = new UserProfileConfigManager(serviceContext).ProfilePropertyManager;
                   
                    // Retrieve all properties for the "UserProfile" profile subtype,
                    // and retrieve the property values for a specific user.
                    ProfileSubtypePropertyManager subtypePropMgr = profilePropMgr.GetProfileSubtypeProperties("UserProfile");
                    UserProfile userProfile = userProfileMgr.GetUserProfile(accountName);
                    IEnumerator<ProfileSubtypeProperty> userProfileSubtypeProperties = subtypePropMgr.GetEnumerator();
                    while (userProfileSubtypeProperties.MoveNext())
                    {
                        string propName = userProfileSubtypeProperties.Current.Name;
                        ProfileValueCollectionBase values = userProfile.GetProfileValueCollection(propName);
                        if (values.Count > 0)
                        {

                            // Handle multivalue properties.
                            foreach (var value in values)
                            {
                                Console.WriteLine(propName + ": " + value.ToString());
                            }
                        }
                        else
                        {
                            Console.WriteLine(propName + ": ");
                        }
                    }
                    Console.WriteLine("Press Enter to change the values.");
                    Console.Read();

                    // Change the value of a single-value user property.
                    userProfile[PropertyConstants.PictureUrl].Value = newPictureUrl;

                    // Add a value to a multivalue user property.
                    userProfile[PropertyConstants.PastProjects].Add((object)"Team Feed App");
                    userProfile[PropertyConstants.PastProjects].Add((object)"Social Ratings View Web Part");

                    // Save the changes to the server.
                    userProfile.Commit();
                    Console.WriteLine("The property values for the user have been changed.");
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="additional-resources"></a><span data-ttu-id="40be0-175">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="40be0-175">Additional resources</span></span>
<span data-ttu-id="40be0-176"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="40be0-176"></span></span>


-  [<span data-ttu-id="40be0-177">Arbeiten mit Benutzerprofilen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="40be0-177">Work with user profiles in SharePoint</span></span>](work-with-user-profiles-in-sharepoint.md)
    
  
-  [<span data-ttu-id="40be0-178">Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="40be0-178">How to: Retrieve user profile properties by using the .NET client object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)
    
  
-  [<span data-ttu-id="40be0-179">Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint</span><span class="sxs-lookup"><span data-stu-id="40be0-179">How to: Retrieve user profile properties by using the JavaScript object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)
    
  
-  [<span data-ttu-id="40be0-180">Microsoft.Office.Server.UserProfiles</span><span class="sxs-lookup"><span data-stu-id="40be0-180">Microsoft.Office.Server.UserProfiles</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.aspx)
    
  
