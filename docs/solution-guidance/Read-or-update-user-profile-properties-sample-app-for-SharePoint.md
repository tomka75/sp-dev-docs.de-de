---
title: "Lesen oder Aktualisieren von Benutzerprofileigenschaften Beispiel-add-in für SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a8bbb4cba2414d7c95beb8e09f480b8e5307c02f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="read-or-update-user-profile-properties-sample-add-in-for-sharepoint"></a>Lesen oder Aktualisieren von Benutzerprofileigenschaften Beispiel-add-in für SharePoint

Sie können eine vom Anbieter gehosteten-add-in zu lesen oder Aktualisieren von SharePoint ein- und mehrwertige Benutzerprofileigenschaften.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_
    
Das [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) -Beispiel zeigt, wie Sie zum Lesen und Aktualisieren von Benutzerprofileigenschaften für einen bestimmten Benutzer. In diesem Beispiel wird eine vom Anbieter gehosteten add-in, verwendet:

- Lesen und alle Benutzerprofileigenschaften für einen Benutzer anzuzeigen.
    
- Aktualisieren einer einwertige Benutzerprofileigenschaft.
    
- Aktualisieren einer mehrwertigen Benutzerprofileigenschaft.
    
Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:

- Lesen oder Schreiben von Daten in einer Benutzerprofileigenschaft für einen Benutzer. 
    
- Verwenden Sie Benutzerprofil Eigenschaftswerte, um SharePoint zu personalisieren.

> [!NOTE] 
> In diesem Codebeispiel wird nur in Office 365 ausgeführt. 

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Vor dem Ausführen von Szenario 1:

1. Am oberen Rand der Office 365-Website wählen Sie Ihr Profilbild aus, und wählen Sie **über mich**, wie in Abbildung 1 dargestellt. 
    
2. Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.
    
3. Geben Sie im **über mich**, ich arbeite bei Contoso.
    
4. Wählen Sie **Speichern und schließen**. 
    
Vor dem Ausführen von Szenario 3:

1. Klicken Sie oben auf der Website wählen Sie Ihres Profilbilds aus, und wählen Sie **über mich**, wie in Abbildung 1 dargestellt. 
    
2. Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.
    
3. Wählen Sie auf **Details bearbeiten** **Details**.
    
4. **Kenntnisse**Geben Sie in JavaScript c#.
    
5. Wählen Sie **Speichern und schließen**. 

**Abbildung 1. Navigieren zu Profilseite des Benutzers über mich auswählen**

![Screenshot der Profilseite des Benutzers mit über mich hervorgehoben](media/692b9a82-45df-4c82-960b-42281be39f1c.png)

## <a name="using-the-userprofilemanipulationcsom-app"></a>Verwenden der app UserProfile.Manipulation.CSOM
<a name="sectionSection1"> </a>

Wenn Sie dieses Beispiel ausführen, startet eine vom Anbieter gehosteten-add-in, wie in Abbildung 2 dargestellt.

**Abbildung 2. Startseite der app UserProfile.Manipulation.CSOM**

![Screenshot der Startseite der app UserProfile.Manipulation.CSOM](media/ec62daf7-1323-4a12-b2c4-a95e0312c58f.png)

In diesem Codebeispiel enthält drei Szenarios.

|Szenario|Zeigt, wie Sie...|
|:---|:---|
|1|Lesen Sie alle Benutzerprofileigenschaften für den Benutzer die app ausführt.|
|2|<p>Aktualisieren einer einwertige Benutzerprofileigenschaft.</p><p>**Hinweis**: in diesem Szenario wird nur in Office 365 unterstützt.</p>|
|3|<p>Aktualisieren einer mehrwertigen Benutzerprofileigenschaft.</p><p>**Hinweis**: in diesem Szenario wird nur in Office 365 unterstützt.</p>|

### <a name="scenario-1-read-all-user-profile-properties"></a>Szenario 1: Lesen Sie alle Benutzerprofileigenschaften

Bei der Auswahl **Führen Sie Szenario 1**das Add-in liest alle Benutzerprofileigenschaften für den aktuellen Benutzer, und klicken Sie dann die Benutzerprofildaten im **aktuellen Benutzerprofileigenschaften**, zeigt, wie in Abbildung 3 dargestellt.

**Abbildung 3. Des aktuellen Benutzers Profildaten Eigenschaften**

![Screenshot des des aktuellen Benutzers Profildaten Eigenschaften](media/012475be-21d7-48b1-bce2-1e863e025c0d.png)

**Führen Sie Szenario 1** auswählen, ruft die **btnScenario1_Click** -Methode in CodeSample1.aspx.cs die folgenden Aufgaben ausführen:

- Verwenden Sie **PeopleManager** , um alle Benutzerprofileigenschaften für den aktuellen Benutzer abzurufen.
    
- Durchlaufen Sie **PersonProperties.UserProfileProperties** die Werte der Benutzerprofileigenschaften in einem Textfeld aufgelistet.
    
> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

### <a name="scenario-2-update-a-single-valued-user-profile-property"></a>Szenario 2: Aktualisieren einer einwertige Benutzerprofileigenschaft

Szenario 2 zeigt, wie ein einwertiges Benutzerprofileigenschaft aktualisiert. Wie in Abbildung 4 dargestellt, ist der aktuelle Wert der **über mich** Benutzerprofileigenschaft für den Benutzer dieses Add-in ausführt, **ich arbeite bei Contoso**. So aktualisieren Sie den Wert der **über mich** Benutzerprofileigenschaft, in das Feld **über mich neuen Wert** EnterI bin Softwareentwickler bei Contoso und anschließend auf **Szenario 2 ausführen**. Der Code aktualisiert den Wert der Eigenschaft **über mich** auf **ich bin Softwareentwickler bei Contoso**. Wie in Abbildung 5 gezeigt, aktualisiert **über mich aktuellen Wert** des Add-Ins mit den neuen Wert der **über mich** Benutzerprofileigenschaft.

**Abbildung 4. Szenario 2-Startseite**

![Screenshot der Startseite für Szenario 2](media/ca229e30-e418-4701-a991-cf669cbc7483.png)

**Abbildung 5. Über mich aktualisiert Benutzerprofileigenschaft**

![Screenshot des aktualisierten über mich Benutzerprofileigenschaft](media/9ffc34d9-b9b5-481c-8b63-fa28bc883d04.png)

**Führen Sie Szenario 2** auswählen, ruft die **btnScenario2_Click** -Methode in CodeSample2.aspx.cs folgende Aktionen ausführen:

- Verwenden Sie **PeopleManager** , um die Benutzerprofileigenschaften des aktuellen Benutzers abrufen.
    
- Der vom Benutzer im HTML-Format eingegebene Text formatiert.
    
- Aktualisieren Sie den Wert der Benutzerprofileigenschaft **Mich-Seite** mithilfe von **SetSingleValueProfileProperty**.  **SetSingleValueProfileProperty** akzeptiert drei Parameter:
    
    - Der Kontoname des Benutzers, dessen Benutzerprofil, die Sie aktualisieren möchten.
    
    - Die Eigenschaftenname der Benutzerprofildienst ( **Mich-Seite** in diesem Szenario).
    
    - Der Wert-Eigenschaft im HTML-Format (** ich bin Softwareentwickler bei Contoso ** in diesem Szenario).
    
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
> Wenn Sie benutzerdefinierte Benutzerprofileigenschaften verwenden, konfigurieren Sie die Eigenschaft, um die von Benutzern bearbeitet werden. Das Verfahren in diesem Szenario verwendet wird für benutzerdefinierte Benutzerprofileigenschaften verwendet werden. 

### <a name="scenario-3-update-a-multivalued-user-profile-property"></a>Szenario 3: Aktualisieren einer mehrwertigen Benutzerprofileigenschaft

Szenario 3 gezeigt, wie eine mehrwertige Benutzerprofileigenschaft aktualisiert. Abbildung 6 zeigt die Startseite für Szenario 3.  **Fähigkeiten aktuellen Wert** zeigt die Fähigkeiten des Benutzers, der die app. Die Fähigkeiten werden für den Benutzer aus der SPS-Kenntnisse Benutzerprofileigenschaft gelesen.

**Abbildung 6. Szenario 3-Startseite**

![Screenshot der Startseite für Szenario 3](media/30926c45-3ecc-4c7d-bc27-d896fc6136b2.png)

So fügen neue Fähigkeiten hinzu Benutzerprofileigenschaft SPS-Kenntnisse von add-in:

1. Geben Sie HTML5, und wählen Sie dann **Fertigkeiten hinzufügen**. 
    
2. Geben Sie ASP.Net, und wählen Sie dann **Fertigkeiten hinzufügen**. 
    
3. Wählen Sie **Szenario 3 ausführen**.
    
4. Stellen Sie sicher, ob die neue Liste der Fähigkeiten für den Benutzer **Fähigkeiten aktuellen Wert** angezeigt wird.
    
5. Stellen Sie sicher, dass die Benutzerprofileigenschaft **SPS-Kenntnisse** für den Benutzer nun die neue Liste der Fähigkeiten zeigt.
    
**Führen Sie Szenario 3** auswählen, ruft **btnScenario3_Click** in CodeSample3.aspx.cs folgende Aktionen ausführen:

- Verwenden Sie **PeopleManager** , um die Benutzerprofileigenschaften des aktuellen Benutzers abrufen.
    
- Lesen Sie die Liste der Fähigkeiten im Listenfeld angezeigt. 
    
- Speichern Sie die neuen Fähigkeiten in **SPS-Kenntnisse** Benutzerprofileigenschaft mithilfe von **SetMultiValuedProfileProperty**.  **SetMultiValuedProfileProperty** akzeptiert drei Parameter:
    
    - Der Kontoname des Benutzers, dessen Benutzerprofil aktualisiert wird.
    
    - Die Eigenschaftenname der Benutzerprofildienst, die **SPS-Kenntnisse**ist.
    
    - Die Eigenschaftswerte als **Liste** von String-Objekten.

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
## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [User Profile Lösungen für SharePoint 2013 und SharePoint Online](user-profile-solutions-for-sharepoint.md)
    
-  [Search.PersonalizedResults-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
