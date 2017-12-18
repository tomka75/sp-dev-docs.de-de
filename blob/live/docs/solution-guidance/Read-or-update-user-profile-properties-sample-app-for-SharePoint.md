---
title: "Lesen oder Aktualisieren von Benutzerprofileigenschaften Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a8bbb4cba2414d7c95beb8e09f480b8e5307c02f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="read-or-update-user-profile-properties-sample-add-in-for-sharepoint"></a><span data-ttu-id="2145f-102">Lesen oder Aktualisieren von Benutzerprofileigenschaften Beispiel-add-in für SharePoint</span><span class="sxs-lookup"><span data-stu-id="2145f-102">Read or update user profile properties sample add-in for SharePoint</span></span>

<span data-ttu-id="2145f-103">Sie können eine vom Anbieter gehosteten-add-in zu lesen oder Aktualisieren von SharePoint ein- und mehrwertige Benutzerprofileigenschaften.</span><span class="sxs-lookup"><span data-stu-id="2145f-103">You can use a provider-hosted add-in to read or update SharePoint single and multivalued user profile properties.</span></span>

<span data-ttu-id="2145f-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="2145f-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="2145f-105">Das [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) -Beispiel zeigt, wie Sie zum Lesen und Aktualisieren von Benutzerprofileigenschaften für einen bestimmten Benutzer.</span><span class="sxs-lookup"><span data-stu-id="2145f-105">The [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) sample shows you how to read and update user profile properties for a particular user.</span></span> <span data-ttu-id="2145f-106">In diesem Beispiel wird eine vom Anbieter gehosteten add-in, verwendet:</span><span class="sxs-lookup"><span data-stu-id="2145f-106">This sample uses a provider-hosted add-in to:</span></span>

- <span data-ttu-id="2145f-107">Lesen und alle Benutzerprofileigenschaften für einen Benutzer anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="2145f-107">Read and display all user profile properties for a user.</span></span>
    
- <span data-ttu-id="2145f-108">Aktualisieren einer einwertige Benutzerprofileigenschaft.</span><span class="sxs-lookup"><span data-stu-id="2145f-108">Update a single-valued user profile property.</span></span>
    
- <span data-ttu-id="2145f-109">Aktualisieren einer mehrwertigen Benutzerprofileigenschaft.</span><span class="sxs-lookup"><span data-stu-id="2145f-109">Update a multivalued user profile property.</span></span>
    
<span data-ttu-id="2145f-110">Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:</span><span class="sxs-lookup"><span data-stu-id="2145f-110">Use this solution if you want to:</span></span>

- <span data-ttu-id="2145f-111">Lesen oder Schreiben von Daten in einer Benutzerprofileigenschaft für einen Benutzer.</span><span class="sxs-lookup"><span data-stu-id="2145f-111">Read or write data to a user profile property for a user.</span></span> 
    
- <span data-ttu-id="2145f-112">Verwenden Sie Benutzerprofil Eigenschaftswerte, um SharePoint zu personalisieren.</span><span class="sxs-lookup"><span data-stu-id="2145f-112">Use user profile property values to personalize SharePoint.</span></span>

> [!NOTE] 
> <span data-ttu-id="2145f-113">In diesem Codebeispiel wird nur in Office 365 ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="2145f-113">This code sample only runs on Office 365.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="2145f-114">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="2145f-114">Before you begin</span></span>
<span data-ttu-id="2145f-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="2145f-115"></span></span>

<span data-ttu-id="2145f-116">Laden Sie Sie zuerst [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="2145f-116">To get started, download the  [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="2145f-117">Vor dem Ausführen von Szenario 1:</span><span class="sxs-lookup"><span data-stu-id="2145f-117">Before you run Scenario 1:</span></span>

1. <span data-ttu-id="2145f-118">Am oberen Rand der Office 365-Website wählen Sie Ihr Profilbild aus, und wählen Sie **über mich**, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2145f-118">At the top of your Office 365 site, choose your profile picture, and then choose  **About me**, as shown in Figure 1.</span></span> 
    
2. <span data-ttu-id="2145f-119">Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="2145f-119">On the  **About me** page, choose **edit your profile**.</span></span>
    
3. <span data-ttu-id="2145f-120">Geben Sie im **über mich**, ich arbeite bei Contoso.</span><span class="sxs-lookup"><span data-stu-id="2145f-120">In  **About me**, enter I work at Contoso.</span></span>
    
4. <span data-ttu-id="2145f-121">Wählen Sie **Speichern und schließen**.</span><span class="sxs-lookup"><span data-stu-id="2145f-121">Choose  **Save all and close**.</span></span> 
    
<span data-ttu-id="2145f-122">Vor dem Ausführen von Szenario 3:</span><span class="sxs-lookup"><span data-stu-id="2145f-122">Before you run Scenario 3:</span></span>

1. <span data-ttu-id="2145f-123">Klicken Sie oben auf der Website wählen Sie Ihres Profilbilds aus, und wählen Sie **über mich**, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2145f-123">At the top of your site, choose your profile picture, and then choose  **About me**, as shown in Figure 1.</span></span> 
    
2. <span data-ttu-id="2145f-124">Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="2145f-124">On the  **About me** page, choose **edit your profile**.</span></span>
    
3. <span data-ttu-id="2145f-125">Wählen Sie auf **Details bearbeiten** **Details**.</span><span class="sxs-lookup"><span data-stu-id="2145f-125">On  **Edit Details**, choose  **Details**.</span></span>
    
4. <span data-ttu-id="2145f-126">**Kenntnisse**Geben Sie in JavaScript c#.</span><span class="sxs-lookup"><span data-stu-id="2145f-126">In  **Skills**, enter C#, JavaScript.</span></span>
    
5. <span data-ttu-id="2145f-127">Wählen Sie **Speichern und schließen**.</span><span class="sxs-lookup"><span data-stu-id="2145f-127">Choose  **Save all and close**.</span></span> 

<span data-ttu-id="2145f-128">**Abbildung 1. Navigieren zu Profilseite des Benutzers über mich auswählen**</span><span class="sxs-lookup"><span data-stu-id="2145f-128">**Figure 1. Navigating to a user's profile page by choosing About me**</span></span>

![Screenshot der Profilseite des Benutzers mit über mich hervorgehoben](media/692b9a82-45df-4c82-960b-42281be39f1c.png)

## <a name="using-the-userprofilemanipulationcsom-app"></a><span data-ttu-id="2145f-130">Verwenden der app UserProfile.Manipulation.CSOM</span><span class="sxs-lookup"><span data-stu-id="2145f-130">Using the UserProfile.Manipulation.CSOM app</span></span>
<span data-ttu-id="2145f-131"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="2145f-131"></span></span>

<span data-ttu-id="2145f-132">Wenn Sie dieses Beispiel ausführen, startet eine vom Anbieter gehosteten-add-in, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2145f-132">When you run this sample, a provider-hosted add-in starts, as shown in Figure 2.</span></span>

<span data-ttu-id="2145f-133">**Abbildung 2. Startseite der app UserProfile.Manipulation.CSOM**</span><span class="sxs-lookup"><span data-stu-id="2145f-133">**Figure 2. Start page of the UserProfile.Manipulation.CSOM app**</span></span>

![Screenshot der Startseite der app UserProfile.Manipulation.CSOM](media/ec62daf7-1323-4a12-b2c4-a95e0312c58f.png)

<span data-ttu-id="2145f-135">In diesem Codebeispiel enthält drei Szenarios.</span><span class="sxs-lookup"><span data-stu-id="2145f-135">This code sample includes three scenarios.</span></span>

|<span data-ttu-id="2145f-136">Szenario</span><span class="sxs-lookup"><span data-stu-id="2145f-136">Scenario</span></span>|<span data-ttu-id="2145f-137">Zeigt, wie Sie...</span><span class="sxs-lookup"><span data-stu-id="2145f-137">Shows how to...</span></span>|
|:---|:---|
|<span data-ttu-id="2145f-138">1</span><span class="sxs-lookup"><span data-stu-id="2145f-138">1</span></span>|<span data-ttu-id="2145f-139">Lesen Sie alle Benutzerprofileigenschaften für den Benutzer die app ausführt.</span><span class="sxs-lookup"><span data-stu-id="2145f-139">Read all user profile properties for the user running the app.</span></span>|
|<span data-ttu-id="2145f-140">2</span><span class="sxs-lookup"><span data-stu-id="2145f-140">2</span></span>|<p><span data-ttu-id="2145f-141">Aktualisieren einer einwertige Benutzerprofileigenschaft.</span><span class="sxs-lookup"><span data-stu-id="2145f-141">Update a single-valued user profile property.</span></span></p><p><span data-ttu-id="2145f-142">**Hinweis**: in diesem Szenario wird nur in Office 365 unterstützt.</span><span class="sxs-lookup"><span data-stu-id="2145f-142">**Note**: This scenario is only supported in Office 365.</span></span></p>|
|<span data-ttu-id="2145f-143">3</span><span class="sxs-lookup"><span data-stu-id="2145f-143">3</span></span>|<p><span data-ttu-id="2145f-144">Aktualisieren einer mehrwertigen Benutzerprofileigenschaft.</span><span class="sxs-lookup"><span data-stu-id="2145f-144">Update a multivalued user profile property.</span></span></p><p><span data-ttu-id="2145f-145">**Hinweis**: in diesem Szenario wird nur in Office 365 unterstützt.</span><span class="sxs-lookup"><span data-stu-id="2145f-145">**Note**: This scenario is only supported in Office 365.</span></span></p>|

### <a name="scenario-1-read-all-user-profile-properties"></a><span data-ttu-id="2145f-146">Szenario 1: Lesen Sie alle Benutzerprofileigenschaften</span><span class="sxs-lookup"><span data-stu-id="2145f-146">Scenario 1: Read all user profile properties</span></span>

<span data-ttu-id="2145f-147">Bei der Auswahl **Führen Sie Szenario 1**das Add-in liest alle Benutzerprofileigenschaften für den aktuellen Benutzer, und klicken Sie dann die Benutzerprofildaten im **aktuellen Benutzerprofileigenschaften**, zeigt, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="2145f-147">When you choose  **Run scenario 1**, the add-in reads all user profile properties for the current user, and then displays the user profile data in  **Current user profile properties**, as shown in Figure 3.</span></span>

<span data-ttu-id="2145f-148">**Abbildung 3. Des aktuellen Benutzers Profildaten Eigenschaften**</span><span class="sxs-lookup"><span data-stu-id="2145f-148">**Figure 3. Current user's profile properties data**</span></span>

![Screenshot des des aktuellen Benutzers Profildaten Eigenschaften](media/012475be-21d7-48b1-bce2-1e863e025c0d.png)

<span data-ttu-id="2145f-150">**Führen Sie Szenario 1** auswählen, ruft die **btnScenario1_Click** -Methode in CodeSample1.aspx.cs die folgenden Aufgaben ausführen:</span><span class="sxs-lookup"><span data-stu-id="2145f-150">Choosing  **Run scenario 1** calls the **btnScenario1_Click** method in CodeSample1.aspx.cs to perform the following tasks:</span></span>

- <span data-ttu-id="2145f-151">Verwenden Sie **PeopleManager** , um alle Benutzerprofileigenschaften für den aktuellen Benutzer abzurufen.</span><span class="sxs-lookup"><span data-stu-id="2145f-151">Use  **PeopleManager** to retrieve all the user profile properties for the current user.</span></span>
    
- <span data-ttu-id="2145f-152">Durchlaufen Sie **PersonProperties.UserProfileProperties** die Werte der Benutzerprofileigenschaften in einem Textfeld aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="2145f-152">Iterate over  **PersonProperties.UserProfileProperties** to list the values of the user profile properties in a text box.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="2145f-153">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="2145f-153">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
protected void btnScenario1_Click(object sender, EventArgs e)
        {

            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Get the people manager instance and load current properties.
                PeopleManager peopleManager = new PeopleManager(clientContext);
                PersonProperties personProperties = peopleManager.GetMyProperties();
                clientContext.Load(personProperties);
                clientContext.ExecuteQuery();

                // Output user profile properties to a text box.
                txtProperties.Text = "";
                foreach (var item in personProperties.UserProfileProperties)
                {
                    txtProperties.Text += string.Format("{0} - {1}{2}", item.Key, item.Value, Environment.NewLine);
                }
            }
        }
```

### <a name="scenario-2-update-a-single-valued-user-profile-property"></a><span data-ttu-id="2145f-154">Szenario 2: Aktualisieren einer einwertige Benutzerprofileigenschaft</span><span class="sxs-lookup"><span data-stu-id="2145f-154">Scenario 2: Update a single-valued user profile property</span></span>

<span data-ttu-id="2145f-155">Szenario 2 zeigt, wie ein einwertiges Benutzerprofileigenschaft aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="2145f-155">Scenario 2 shows how to update a single-valued user profile property.</span></span> <span data-ttu-id="2145f-156">Wie in Abbildung 4 dargestellt, ist der aktuelle Wert der **über mich** Benutzerprofileigenschaft für den Benutzer dieses Add-in ausführt, **ich arbeite bei Contoso**.</span><span class="sxs-lookup"><span data-stu-id="2145f-156">As shown in Figure 4, the current value of the  **About me** user profile property for the user running this add-in is **I work at Contoso**.</span></span> <span data-ttu-id="2145f-157">So aktualisieren Sie den Wert der **über mich** Benutzerprofileigenschaft, in das Feld **über mich neuen Wert** EnterI bin Softwareentwickler bei Contoso und anschließend auf **Szenario 2 ausführen**.</span><span class="sxs-lookup"><span data-stu-id="2145f-157">To update the value of the  **About me** user profile property, in the **About me new value** box, enterI am a software engineer at Contoso and then choose **Run scenario 2**.</span></span> <span data-ttu-id="2145f-158">Der Code aktualisiert den Wert der Eigenschaft **über mich** auf **ich bin Softwareentwickler bei Contoso**.</span><span class="sxs-lookup"><span data-stu-id="2145f-158">The code updates the value of the  **About me** property to **I am a software engineer at Contoso**.</span></span> <span data-ttu-id="2145f-159">Wie in Abbildung 5 gezeigt, aktualisiert **über mich aktuellen Wert** des Add-Ins mit den neuen Wert der **über mich** Benutzerprofileigenschaft.</span><span class="sxs-lookup"><span data-stu-id="2145f-159">As shown in Figure 5, the add-in updates  **About me current value** with the new value of the **About me** user profile property.</span></span>

<span data-ttu-id="2145f-160">**Abbildung 4. Szenario 2-Startseite**</span><span class="sxs-lookup"><span data-stu-id="2145f-160">**Figure 4. Scenario 2 start page**</span></span>

![Screenshot der Startseite für Szenario 2](media/ca229e30-e418-4701-a991-cf669cbc7483.png)

<span data-ttu-id="2145f-162">**Abbildung 5. Über mich aktualisiert Benutzerprofileigenschaft**</span><span class="sxs-lookup"><span data-stu-id="2145f-162">**Figure 5. Updated About me user profile property**</span></span>

![Screenshot des aktualisierten über mich Benutzerprofileigenschaft](media/9ffc34d9-b9b5-481c-8b63-fa28bc883d04.png)

<span data-ttu-id="2145f-164">**Führen Sie Szenario 2** auswählen, ruft die **btnScenario2_Click** -Methode in CodeSample2.aspx.cs folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="2145f-164">Choosing  **Run scenario 2** calls the **btnScenario2_Click** method in CodeSample2.aspx.cs to do the following:</span></span>

- <span data-ttu-id="2145f-165">Verwenden Sie **PeopleManager** , um die Benutzerprofileigenschaften des aktuellen Benutzers abrufen.</span><span class="sxs-lookup"><span data-stu-id="2145f-165">Use  **PeopleManager** to get the user profile properties of the current user.</span></span>
    
- <span data-ttu-id="2145f-166">Der vom Benutzer im HTML-Format eingegebene Text formatiert.</span><span class="sxs-lookup"><span data-stu-id="2145f-166">Format the text entered by the user in HTML.</span></span>
    
- <span data-ttu-id="2145f-167">Aktualisieren Sie den Wert der Benutzerprofileigenschaft **Mich-Seite** mithilfe von **SetSingleValueProfileProperty**.</span><span class="sxs-lookup"><span data-stu-id="2145f-167">Update the value of the  **AboutMe** user profile property by using **SetSingleValueProfileProperty**.</span></span>  <span data-ttu-id="2145f-168">**SetSingleValueProfileProperty** akzeptiert drei Parameter:</span><span class="sxs-lookup"><span data-stu-id="2145f-168">**SetSingleValueProfileProperty** accepts three parameters:</span></span>
    
    - <span data-ttu-id="2145f-169">Der Kontoname des Benutzers, dessen Benutzerprofil, die Sie aktualisieren möchten.</span><span class="sxs-lookup"><span data-stu-id="2145f-169">The account name of the user whose user profile you're updating.</span></span>
    
    - <span data-ttu-id="2145f-170">Die Eigenschaftenname der Benutzerprofildienst ( **Mich-Seite** in diesem Szenario).</span><span class="sxs-lookup"><span data-stu-id="2145f-170">The user profile property name ( **AboutMe** in this scenario).</span></span>
    
    - <span data-ttu-id="2145f-171">Der Wert-Eigenschaft im HTML-Format (** ich bin Softwareentwickler bei Contoso ** in diesem Szenario).</span><span class="sxs-lookup"><span data-stu-id="2145f-171">The property value, in HTML format ( ** I am a software engineer at Contoso** in this scenario).</span></span>
    
```C#
protected void btnScenario2_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Get the people manager instance and initialize the account name.
                PeopleManager peopleManager = new PeopleManager(clientContext);
                PersonProperties personProperties = peopleManager.GetMyProperties();
                clientContext.Load(personProperties, p => p.AccountName);
                clientContext.ExecuteQuery();

                // Convert entry to HTML.
                string updatedValue = (txtAboutMe.Text).Replace(Environment.NewLine, "");

                // Update the AboutMe property for the user using account name from the user profile.
                peopleManager.SetSingleValueProfileProperty(personProperties.AccountName, "AboutMe", updatedValue);
                clientContext.ExecuteQuery();

            }
        }
```
    
> [!NOTE] 
> <span data-ttu-id="2145f-172">Wenn Sie benutzerdefinierte Benutzerprofileigenschaften verwenden, konfigurieren Sie die Eigenschaft, um die von Benutzern bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="2145f-172">If you use custom user profile properties, configure the property to be editable by users.</span></span> <span data-ttu-id="2145f-173">Das Verfahren in diesem Szenario verwendet wird für benutzerdefinierte Benutzerprofileigenschaften verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="2145f-173">The technique used in this scenario will work for custom user profile properties.</span></span> 

### <a name="scenario-3-update-a-multivalued-user-profile-property"></a><span data-ttu-id="2145f-174">Szenario 3: Aktualisieren einer mehrwertigen Benutzerprofileigenschaft</span><span class="sxs-lookup"><span data-stu-id="2145f-174">Scenario 3: Update a multivalued user profile property</span></span>

<span data-ttu-id="2145f-175">Szenario 3 gezeigt, wie eine mehrwertige Benutzerprofileigenschaft aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="2145f-175">Scenario 3 shows how to update a multivalued user profile property.</span></span> <span data-ttu-id="2145f-176">Abbildung 6 zeigt die Startseite für Szenario 3.</span><span class="sxs-lookup"><span data-stu-id="2145f-176">Figure 6 shows the start page for Scenario 3.</span></span>  <span data-ttu-id="2145f-177">**Fähigkeiten aktuellen Wert** zeigt die Fähigkeiten des Benutzers, der die app.</span><span class="sxs-lookup"><span data-stu-id="2145f-177">**Skills current value** shows the skills of the user running the app.</span></span> <span data-ttu-id="2145f-178">Die Fähigkeiten werden für den Benutzer aus der SPS-Kenntnisse Benutzerprofileigenschaft gelesen.</span><span class="sxs-lookup"><span data-stu-id="2145f-178">The skills are read from the SPS-Skills user profile property for the user.</span></span>

<span data-ttu-id="2145f-179">**Abbildung 6. Szenario 3-Startseite**</span><span class="sxs-lookup"><span data-stu-id="2145f-179">**Figure 6. Scenario 3 start page**</span></span>

![Screenshot der Startseite für Szenario 3](media/30926c45-3ecc-4c7d-bc27-d896fc6136b2.png)

<span data-ttu-id="2145f-181">So fügen neue Fähigkeiten hinzu Benutzerprofileigenschaft SPS-Kenntnisse von add-in:</span><span class="sxs-lookup"><span data-stu-id="2145f-181">To add new skills to the SPS-Skills user profile property from this add-in:</span></span>

1. <span data-ttu-id="2145f-182">Geben Sie HTML5, und wählen Sie dann **Fertigkeiten hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="2145f-182">Enter HTML5, and then choose  **Add Skill**.</span></span> 
    
2. <span data-ttu-id="2145f-183">Geben Sie ASP.Net, und wählen Sie dann **Fertigkeiten hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="2145f-183">Enter ASP.Net, and then choose  **Add Skill**.</span></span> 
    
3. <span data-ttu-id="2145f-184">Wählen Sie **Szenario 3 ausführen**.</span><span class="sxs-lookup"><span data-stu-id="2145f-184">Choose  **Run scenario 3**.</span></span>
    
4. <span data-ttu-id="2145f-185">Stellen Sie sicher, ob die neue Liste der Fähigkeiten für den Benutzer **Fähigkeiten aktuellen Wert** angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="2145f-185">Verify that  **Skills current value** shows the new list of skills for the user.</span></span>
    
5. <span data-ttu-id="2145f-186">Stellen Sie sicher, dass die Benutzerprofileigenschaft **SPS-Kenntnisse** für den Benutzer nun die neue Liste der Fähigkeiten zeigt.</span><span class="sxs-lookup"><span data-stu-id="2145f-186">Verify that the  **SPS-Skills** user profile property for the user now shows the new list of skills.</span></span>
    
<span data-ttu-id="2145f-187">**Führen Sie Szenario 3** auswählen, ruft **btnScenario3_Click** in CodeSample3.aspx.cs folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="2145f-187">Choosing  **Run scenario 3** calls **btnScenario3_Click** in CodeSample3.aspx.cs to do the following:</span></span>

- <span data-ttu-id="2145f-188">Verwenden Sie **PeopleManager** , um die Benutzerprofileigenschaften des aktuellen Benutzers abrufen.</span><span class="sxs-lookup"><span data-stu-id="2145f-188">Use  **PeopleManager** to get the user profile properties of the current user.</span></span>
    
- <span data-ttu-id="2145f-189">Lesen Sie die Liste der Fähigkeiten im Listenfeld angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2145f-189">Read the list of skills shown in the list box.</span></span> 
    
- <span data-ttu-id="2145f-190">Speichern Sie die neuen Fähigkeiten in **SPS-Kenntnisse** Benutzerprofileigenschaft mithilfe von **SetMultiValuedProfileProperty**.</span><span class="sxs-lookup"><span data-stu-id="2145f-190">Save the new skills to the  **SPS-Skills** user profile property by using **SetMultiValuedProfileProperty**.</span></span>  <span data-ttu-id="2145f-191">**SetMultiValuedProfileProperty** akzeptiert drei Parameter:</span><span class="sxs-lookup"><span data-stu-id="2145f-191">**SetMultiValuedProfileProperty** accepts three parameters:</span></span>
    
    - <span data-ttu-id="2145f-192">Der Kontoname des Benutzers, dessen Benutzerprofil aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="2145f-192">The account name of the user whose user profile is being updated.</span></span>
    
    - <span data-ttu-id="2145f-193">Die Eigenschaftenname der Benutzerprofildienst, die **SPS-Kenntnisse**ist.</span><span class="sxs-lookup"><span data-stu-id="2145f-193">The user profile property name, which is  **SPS-Skills**.</span></span>
    
    - <span data-ttu-id="2145f-194">Die Eigenschaftswerte als **Liste** von String-Objekten.</span><span class="sxs-lookup"><span data-stu-id="2145f-194">The property values as a  **List** of string objects.</span></span>

```C#
  protected void btnScenario3_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Get the people manager instance and initialize the account name.
                PeopleManager peopleManager = new PeopleManager(clientContext);
                PersonProperties personProperties = peopleManager.GetMyProperties();
                clientContext.Load(personProperties, p => p.AccountName);
                clientContext.ExecuteQuery();

                // Collect the user's skills from the list box in order to update the user's profile.
                List<string> skills = new List<string>();
                for (int i = 0; i < lstSkills.Items.Count; i++)
                {
                    skills.Add(lstSkills.Items[i].Value);
                }

                // Update the SPS-Skills property for the user using account name from the user's profile.
                peopleManager.SetMultiValuedProfileProperty(personProperties.AccountName, "SPS-Skills", skills);
                clientContext.ExecuteQuery();

                // Refresh the values.
                RefreshUIValues();
            }

        }
```
## <a name="see-also"></a><span data-ttu-id="2145f-195">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2145f-195">See also</span></span>
<span data-ttu-id="2145f-196"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2145f-196"></span></span>

-  [<span data-ttu-id="2145f-197">User Profile Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="2145f-197">User profile solutions for SharePoint 2013 and SharePoint Online</span></span>](user-profile-solutions-for-sharepoint.md)
    
-  [<span data-ttu-id="2145f-198">Search.PersonalizedResults-Beispiel</span><span class="sxs-lookup"><span data-stu-id="2145f-198"> Search.PersonalizedResults sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
