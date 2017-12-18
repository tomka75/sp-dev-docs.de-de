---
title: "Hinzufügen von Spalten zu einem von SharePoint gehosteten SharePoint-Add-In"
description: "Erstellen Sie benutzerdefinierte Spaltentypen, führen Sie das Add-In aus, und testen Sie die Spalten."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 5b341c7f554dc1c4163b0fe37c15270edf30882e
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="743ca-103">Hinzufügen von Spalten zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="743ca-103">Add custom columns to a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="743ca-104">Dies ist der dritte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut:</span><span class="sxs-lookup"><span data-stu-id="743ca-104">This is the ninth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>

-  [<span data-ttu-id="743ca-105">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="743ca-105">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)  
-  [<span data-ttu-id="743ca-106">Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="743ca-106">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
    
> [!NOTE]
> <span data-ttu-id="743ca-107">Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, können Sie das Thema mit einer Visual Studio-Lösung weiter vertiefen.</span><span class="sxs-lookup"><span data-stu-id="743ca-107">Note  If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  SharePoint_SP-hosted_Add-Ins_Tutorials and open the BeforeClientRenderedControl.sln file.</span></span> <span data-ttu-id="743ca-108">Sie können auch das Repository von [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeColumns.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="743ca-108">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeColumns.sln file.</span></span>

<span data-ttu-id="743ca-109">In diesem Artikel kehren wir zum Programmieren zurück, indem wir einige Websitespalten zum SharePoint-Add-In „Orientierung für Mitarbeiter“ hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="743ca-109">In this article we get back to coding by adding some site columns to the Employee Orientation SharePoint Add-in.</span></span>
 
## <a name="create-custom-column-types"></a><span data-ttu-id="743ca-110">Erstellen benutzerdefinierter Spaltentypen</span><span class="sxs-lookup"><span data-stu-id="743ca-110">Create custom column types</span></span>

1. <span data-ttu-id="743ca-111">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie **Neuen Ordner** > ** hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="743ca-111">In **Solution Explorer**, right-click the project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="743ca-112">Nennen Sie den Ordner **Websitespalten**.</span><span class="sxs-lookup"><span data-stu-id="743ca-112">Name the folder **Site Columns**.</span></span>    
 
2. <span data-ttu-id="743ca-113">Klicken Sie mit der rechten Maustaste auf den neuen Ordner, und wählen Sie **Neues Element** > **hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="743ca-113">Right-click the new folder, and select **Add** > **New Item**.</span></span> <span data-ttu-id="743ca-114">Das Dialogfeld **Neues Element hinzufügen** wird geöffnet, und der **Office/SharePoint**-Knoten wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="743ca-114">Right-click the new folder and choose  AddNew Item. The  **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>
     
3. <span data-ttu-id="743ca-115">Wählen Sie **Websitespalte** aus, geben Sie ihr den Namen **Abteilung**, und wählen Sie **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="743ca-115">Choose  **Site Column**, give it the name Division, and choose  **Add**.</span></span>
    
4. <span data-ttu-id="743ca-116">Bearbeiten Sie in der Datei „elements.xml“ für die neue Websitespalte das Element **Feld** so, dass es die im folgenden Beispiel gezeigten Attribute und Werte hat, mit der Ausnahme, dass *Sie **nicht** den Wert der GUID* für das Attribut **ID** ändern sollten, der von Visual Studio dafür generiert wurde. *Seien Sie also vorsichtig, wenn Sie Kopieren und Einfügen verwenden.*</span><span class="sxs-lookup"><span data-stu-id="743ca-116">In the elements.xml file for the new site column, edit the  **Field** element so that it has the attributes and values shown in the following example, except that *you should  **not** change the GUID*  for the **ID** attribute from the value that Visual Studio generated for it, *so be careful if you are using copy-and-paste*  .</span></span>
    
    ```
      <Field ID="{generated GUID}" 
           Name="Division" 
           Title="Division" 
           DisplayName="Division" 
           Description="The division of the company where the employee works." 
           Group="Employee Orientation" 
           Type="Text" 
           Required ="FALSE">
    </Field>
    ```
    
    <br/>

5. <span data-ttu-id="743ca-117">Fügen Sie eine weitere **Websitespalte** mit dem Namen **OrientationStage** im selben Ordner hinzu.</span><span class="sxs-lookup"><span data-stu-id="743ca-117">Add another **Site Column** to the same folder named OrientationStage.</span></span>
    
6. <span data-ttu-id="743ca-118">Bearbeiten Sie in der Datei „elements.xml“ für die neue Websitespalte das Element **Feld** so, dass es die im folgenden Beispiel dargestellten Attribute und Werte aufweist, mit der Ausnahme, dass der Wert der GUID für das Attribut **ID**, den Visual Studio dafür generiert hat, nicht geändert werden sollte.</span><span class="sxs-lookup"><span data-stu-id="743ca-118">In the elements.xml file for the new site column, edit the  **Field** element so that it has the attributes and values shown in the following example, except that you should not change the GUID for the **ID** attribute from the value that Visual Studio generated for it.</span></span>
    
    ```
      <Field ID="{generated GUID}" 
           Name="OrientationStage" 
           Title="OrientationStage"
           DisplayName="Orientation Stage" 
           Group="Employee Orientation" 
           Description="The current orientation stage of the employee." 
           Type="Choice"
           Required ="TRUE">
    </Field>
    ```
    
    <br/>

7. <span data-ttu-id="743ca-119">Weil es sich um ein Auswahlfeld handelt, müssen Sie die Auswahlmöglichkeiten und die Reihenfolge ihrer Anzeige in der Dropdownliste, wenn ein Benutzer eine Auswahl trifft, angeben.</span><span class="sxs-lookup"><span data-stu-id="743ca-119">Because this is a Choice field, you must specify the possible choices, the order in which they should appear in the drop-down list when a user is making a choice, and the default choice. Add the following child markup to the Field element.</span></span> <span data-ttu-id="743ca-120">Da dies ein Pflichtfeld ist, müssen Sie einen Standardwert angeben.</span><span class="sxs-lookup"><span data-stu-id="743ca-120">Because it is a required field, you must specify a default value.</span></span> <span data-ttu-id="743ca-121">Fügen Sie das folgende untergeordnete Markup zum **Feld**-Element hinzu, und speichern Sie dann alle Dateien.</span><span class="sxs-lookup"><span data-stu-id="743ca-121">Add the following child markup to the **Field** element, and then save all the files.</span></span>
    
    ```
      <CHOICES>
          <CHOICE>Not Started</CHOICE>
          <CHOICE>Tour of building</CHOICE>
          <CHOICE>HR paperwork</CHOICE>
          <CHOICE>Corporate network access</CHOICE>
          <CHOICE>Completed</CHOICE>
    </CHOICES>
    <MAPPINGS>
          <MAPPING Value="1">Not Started</MAPPING>
          <MAPPING Value="2">Tour of building</MAPPING>
          <MAPPING Value="3">HR paperwork</MAPPING>
          <MAPPING Value="4">Corp network access</MAPPING>
          <MAPPING Value="5">Completed</MAPPING>
    </MAPPINGS>
    <Default>Not Started</Default>
    ```

    </br>
    
## <a name="run-the-add-in-and-test-the-columns"></a><span data-ttu-id="743ca-122">Ausführen des Add-Ins und Testen der Spalten</span><span class="sxs-lookup"><span data-stu-id="743ca-122">Run the add-in and test the columns</span></span>

1. <span data-ttu-id="743ca-p105">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="743ca-p105">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span>  
 
2. <span data-ttu-id="743ca-125">Wenn die Standardseite des Add-Ins geöffnet wird, wählen Sie den Link für **Neue Mitarbeiter in Seattle** aus, um die benutzerdefinierte Listeninstanz zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="743ca-125">When the add-in's default page opens, choose the  **New Employees in Seattle** link to open the custom list instance.</span></span>
 
3. <span data-ttu-id="743ca-126">Öffnen Sie die Seite **Einstellungen** der Liste, und fügen Sie die zwei Spalten mit den folgenden Schritten hinzu.</span><span class="sxs-lookup"><span data-stu-id="743ca-126">Open the list's  **Settings** page and add the two columns to it with these steps.</span></span>
    
    1. <span data-ttu-id="743ca-127">Wählen Sie die Popupschaltfläche **· · ·** direkt über der Liste aus, und wählen Sie dann **Ansicht erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="743ca-127">Click the callout button,  **· · ·**, just above the list, and then choose  **Create View**.</span></span>
    2. <span data-ttu-id="743ca-128">Die Seite **Ansichtstyp** wird mit der Breadcrumb-Struktur **Einstellungen und Ansichtstyp** im oberen Bereich geöffnet.</span><span class="sxs-lookup"><span data-stu-id="743ca-128">The  **View Type** page opens, with the breadcrumb structure **Settings > View Type** near the top. Click the Settings breadcrumb.</span></span> <span data-ttu-id="743ca-129">Klicken Sie auf den Breadcrumb **Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="743ca-129">Select the **Settings** breadcrumb.</span></span>
    
        <span data-ttu-id="743ca-130">*Abbildung 1. Schritte zum Öffnen der Seite mit Listeneinstellungen*</span><span class="sxs-lookup"><span data-stu-id="743ca-130">*Steps to open the list settings page*</span></span>

        ![Liste "Neue Mitarbeiter in Seattle", wobei die Beschriftungsschaltfläche und das Element "Ansicht erstellen" als erster Schritt markiert sind. Dann über den Pfeil zur Seite "Ansicht erstellen", wobei das Breadcrumb "Einstellungen" markiert ist.](../images/6c119cae-adf8-42ff-9890-f3aa1e11719d.png)
 
    3. <span data-ttu-id="743ca-133">Öffnen Sie auf der Seite **Einstellungen** den Link **Aus vorhandenen Websitespalten hinzufügen** etwa in der Mitte der Seite links.</span><span class="sxs-lookup"><span data-stu-id="743ca-133">On the  **Settings** page, open the **Add from existing site columns** link on the left about halfway down the page.</span></span>
    
        <span data-ttu-id="743ca-134">*Abbildung 2. Seite mit Listeneinstellungen*</span><span class="sxs-lookup"><span data-stu-id="743ca-134">*Figure 2. List settings page*</span></span>

        ![Die Seite mit Listeninstanzeinstellungen, auf der der Link für „Spalten aus Websitespalten hinzufügen“ hervorgehoben ist.](../images/a8698b77-b9d2-40f6-89f6-ccc3c6e06073.png)

    4. <span data-ttu-id="743ca-136">Wählen Sie auf der Seite **Spalten aus Websitespalten hinzufügen** in der Dropdownliste **Websitespalten auswählen aus** die Option **Orientierung für Mitarbeiter** aus.</span><span class="sxs-lookup"><span data-stu-id="743ca-136">On the  **Add Columns from Site Columns** page, choose **Employee Orientation** on the **Select site columns from** drop down list.</span></span>
    
        <span data-ttu-id="743ca-137">*Abbildung 3. Spalten von der Seite Websitespalten hinzufügen*</span><span class="sxs-lookup"><span data-stu-id="743ca-137">*Figure 3. Add Columns from Site Columns page*</span></span>

        ![Das Steuerelement für die SharePoint-Spaltenauswahl, wobei „Orientierung für Mitarbeiter“ in der Dropdownliste mit der Bezeichnung „Websitespalten auswählen“ ausgewählt ist.](../images/3b33c622-c52a-45fd-8ea1-d7f307539753.png)

    5. <span data-ttu-id="743ca-139">Fügen Sie die Spalten **Abteilung** und **Orientierungsphase** zum Feld **Hinzuzufügende Spalten** hinzu.</span><span class="sxs-lookup"><span data-stu-id="743ca-139">Add the  **Division** and **OrientationStage** columns to the **Columns to add** box.</span></span>

    6. <span data-ttu-id="743ca-140">Wählen Sie **OK** aus, um zur Seite **Einstellungen** zurückzukehren, und wählen Sie dann den Breadcrumb **Neue Mitarbeiter in Seattle** im oberen Bereich der Seite aus.</span><span class="sxs-lookup"><span data-stu-id="743ca-140">Choose  **OK** to return to the **Settings** page, and then click the **New Employees in Seattle** breadcrumb near the top of the page.</span></span>
    
4. <span data-ttu-id="743ca-141">Die neuen Spalten sind jetzt in der Liste enthalten.</span><span class="sxs-lookup"><span data-stu-id="743ca-141">The new columns are now on the list.</span></span> <span data-ttu-id="743ca-142">Fügen Sie ein neues Element zu der Liste hinzu.</span><span class="sxs-lookup"><span data-stu-id="743ca-142">Add a new item to the project</span></span> <span data-ttu-id="743ca-143">Das Bearbeitungsformular des Feldes **Orientierungsphase** besitzt bereits den Standardwert **Nicht gestartet**.</span><span class="sxs-lookup"><span data-stu-id="743ca-143">On the edit form, the **Orientation Stage** field will already have the default value **Not Started**.</span></span> <span data-ttu-id="743ca-144">(Die vorhandenen Elemente sind in diesem Feld leer, da sie erstellt wurden, bevor das Feld in der Liste war.)</span><span class="sxs-lookup"><span data-stu-id="743ca-144">(The existing items will be blank in this field because they were created before the field was on the list.)</span></span>
    
    <span data-ttu-id="743ca-145">*Abbildung 4. Die Liste mit neuen Spalten*</span><span class="sxs-lookup"><span data-stu-id="743ca-145">*The list with new columns*</span></span>

    ![Die Liste mit den neuen Spalten „Abteilung“ und „Orientierungsphase“.](../images/d4e17424-c06b-4635-aab8-4912cee5fe35.png)
 
5. <span data-ttu-id="743ca-147">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="743ca-147">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span> <span data-ttu-id="743ca-148">Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="743ca-148">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
6. <span data-ttu-id="743ca-149">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben.</span><span class="sxs-lookup"><span data-stu-id="743ca-149">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  Solution Explorer and choose Retract.</span></span> <span data-ttu-id="743ca-150">Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="743ca-150">Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>
    

## <a name="next-steps"></a><span data-ttu-id="743ca-151">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="743ca-151">Next steps</span></span>
<span data-ttu-id="743ca-152"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="743ca-152"></span></span>

<span data-ttu-id="743ca-153">Da Sie nicht wirklich möchten, dass Ihre Benutzer die benutzerdefinierten Spalten manuell zur Liste hinzufügen müssen, erstellen Sie im nächsten Artikel dieser Reihe einen benutzerdefinierten Inhaltstyp, der die benutzerdefinierten Spalten enthält und automatisch mit der Listenvorlage für neue Mitarbeiter verknüpft wird: [Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="743ca-153">You don't really want your users to have to manually add the custom columns to the list, so in the next article in this series, you'll create a custom content type that includes the custom columns and is automatically associated with the New Employees list template:  [Add a custom content type to a SharePoint-hostedSharePoint Add-in](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md).</span></span> 
 

 

