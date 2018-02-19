---
title: "Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In"
description: "Erstellen Sie einen benutzerdefinierten Inhaltstyp, führen Sie das Add-In aus und testen Sie es."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: c6171e06ba9e3db26d043b9f31b2536967142184
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="237a2-103">Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem in SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="237a2-103">Add a custom content type to a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="237a2-104">Dies ist der vierte einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln dieser Reihe vertraut, die Sie unter [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md#Nextsteps) finden.</span><span class="sxs-lookup"><span data-stu-id="237a2-104">This is the fourth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 
    
> [!NOTE]
> <span data-ttu-id="237a2-105">Wenn Sie unsere Artikelreihe zum Thema SharePoint-gehostete Add-Ins durchgearbeitet haben, haben Sie bereits eine Visual Studio-Lösung, die Sie für diesen Artikel verwenden können.</span><span class="sxs-lookup"><span data-stu-id="237a2-105">If you have been working through this series about SharePoint-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="237a2-106">Sie können auch das Repository von [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeContentType.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="237a2-106">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeContentType.sln file.</span></span>

<span data-ttu-id="237a2-107">In diesem Artikel fügen Sie dem SharePoint-Add-In „Orientierung für Mitarbeiter“ einen benutzerdefinierten Inhaltstyp hinzu.</span><span class="sxs-lookup"><span data-stu-id="237a2-107">In this article, you add a custom content type to the Employee Orientation SharePoint Add-in.</span></span>
 

## <a name="create-the-custom-content-type"></a><span data-ttu-id="237a2-108">Erstellen des benutzerdefinierten Inhaltstyps</span><span class="sxs-lookup"><span data-stu-id="237a2-108">Create the custom content type</span></span>

1. <span data-ttu-id="237a2-109">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie **Neuen Ordner** > ** hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="237a2-109">In **Solution Explorer**, right-click the project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="237a2-110">Nennen Sie den Ordner **Inhaltstypen**.</span><span class="sxs-lookup"><span data-stu-id="237a2-110">Name the folder **Content Types**.</span></span>
     
2. <span data-ttu-id="237a2-111">Klicken Sie mit der rechten Maustaste auf den neuen Ordner, und wählen Sie **Neues Element** > **hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="237a2-111">Right-click the new folder and select **Add** > **New Item**.</span></span> <span data-ttu-id="237a2-112">Das Dialogfeld **Neues Element hinzufügen** wird geöffnet, und der **Office/SharePoint**-Knoten wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="237a2-112">The **Add New Item** dialog box opens to the **Office/SharePoint** node.</span></span>
     
3. <span data-ttu-id="237a2-113">Wählen Sie **Inhaltstyp** aus, und geben Sie ihm den Namen **NewEmployee**, und wählen Sie dann **hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="237a2-113">Select **Content Type** and give it the name **NewEmployee**, and then select **Add**.</span></span> <span data-ttu-id="237a2-114">Wenn Sie vom Assistenten aufgefordert werden, den Basisinhaltstyp auszuwählen, wählen Sie **Element** und dann **Fertig stellen** aus.</span><span class="sxs-lookup"><span data-stu-id="237a2-114">When prompted by the wizard to select the base content type, select **Item**, and then select **Finish**.</span></span>   
 
4. <span data-ttu-id="237a2-115">Wenn der Inhaltstyp-Designer nicht automatisch geöffnet wird, wählen Sie den Inhaltstyp **NewEmployee** im **Projektmappen-Explorer** aus, um ihn zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="237a2-115">If the content type designer does not automatically open, select the **NewEmployee** content type in **Solution Explorer** to open it.</span></span>
    
5. <span data-ttu-id="237a2-116">Öffnen Sie die Registerkarte **Inhaltstyp** im Designer, und füllen Sie die Textfelder wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="237a2-116">Open the **Content Type** tab in the designer, and fill in the text boxes as follows:</span></span>
    
   -  <span data-ttu-id="237a2-117">**Inhaltstypname**: NewEmployee</span><span class="sxs-lookup"><span data-stu-id="237a2-117">**Content Type Name**: NewEmployee</span></span>
   -  <span data-ttu-id="237a2-118">**Beschreibung**: Stellt einen neuen Mitarbeiter dar.</span><span class="sxs-lookup"><span data-stu-id="237a2-118">**Description**: Represents a new employee</span></span>
   -  <span data-ttu-id="237a2-119">**Gruppenname**: Orientierung für Mitarbeiter</span><span class="sxs-lookup"><span data-stu-id="237a2-119">**Group Name**: Employee Orientation</span></span>
 
6. <span data-ttu-id="237a2-120">Stellen Sie sicher, dass *keines* der Kontrollkästchen auf der Registerkarte ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="237a2-120">Verify that *none* of the check boxes on the tab are selected.</span></span> <span data-ttu-id="237a2-121">Das Kontrollkästchen für **Erbt die Spalten vom übergeordneten Inhaltstyp** ist möglicherweise standardmäßig aktiviert.</span><span class="sxs-lookup"><span data-stu-id="237a2-121">The check box for **Inherits the columns from the parent Content Type** may be selected by default.</span></span> <span data-ttu-id="237a2-122">*Achten Sie darauf, es zu deaktivieren.*</span><span class="sxs-lookup"><span data-stu-id="237a2-122">*Be sure to clear it.*</span></span>  <span data-ttu-id="237a2-123">Die Registerkarte sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="237a2-123">The tab should now look like the following:</span></span>
    
    <span data-ttu-id="237a2-124">*Abbildung 1. Registerkarte „Inhaltstyp“*</span><span class="sxs-lookup"><span data-stu-id="237a2-124">*Figure 1. Content Type Tab*</span></span>

    ![Der Inhaltstyp-Designer, in dem „NewEmployee“ als Typname, „Stellt einen neuen Mitarbeiter dar“ als Beschreibung und „Orientierung für Mitarbeiter“ als Gruppe angezeigt wird.](../images/8a9768f4-315d-45c0-88d7-687dbf84495c.PNG)
 
7. <span data-ttu-id="237a2-126">Öffnen Sie die Registerkarte **Spalten** im Designer.</span><span class="sxs-lookup"><span data-stu-id="237a2-126">Open the **Columns** tab in the designer.</span></span>
     
8. <span data-ttu-id="237a2-127">Wählen Sie im Raster **Hier klicken, um eine Spalte hinzufügen** aus, um eine Dropdownliste der Spalten zu öffnen, und fügen Sie die Spalte **Abteilung** hinzu.</span><span class="sxs-lookup"><span data-stu-id="237a2-127">In the grid, select **Click here to add a column** to open a drop-down list of columns, and add the **Division** column.</span></span> <span data-ttu-id="237a2-128">Sie ist in der Dropdown-Liste mit dem Anzeigenamen **Abteilung** aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="237a2-128">It is listed in the drop-down list by its display name **Division**.</span></span> <span data-ttu-id="237a2-129">Wiederholen Sie diesen Schritt für die Spalte **Orientierungsphase**.</span><span class="sxs-lookup"><span data-stu-id="237a2-129">Do the same for the **Orientation Stage** column.</span></span> <span data-ttu-id="237a2-130">(Wenn die Spalten nicht aufgeführt sind, haben Sie möglicherweise mit der falschen Visual Studio-Lösung begonnen.</span><span class="sxs-lookup"><span data-stu-id="237a2-130">(If they are not listed, you may not have started with the correct Visual Studio solution.</span></span> <span data-ttu-id="237a2-131">Beginnen Sie mit BeforeContentType.sln.) Wenn Sie fertig sind, sollte das Raster wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="237a2-131">Start with BeforeContentType.sln.) When you are finished, the grid should look like the following:</span></span>
    
    <span data-ttu-id="237a2-132">*Abbildung 2. Registerkarte „Spalten“*</span><span class="sxs-lookup"><span data-stu-id="237a2-132">*Figure 2. Columns Tab*</span></span>

    ![Die Registerkarte „Spalten“ des Inhaltstyp-Designers, wobei „Mitarbeiter“, „Abteilung“ und „Orientierungsphase“ im Raster aufgeführt sind.](../images/835e78b3-a073-45b2-b4ee-3f9be9d88495.PNG)

9. <span data-ttu-id="237a2-134">Speichern Sie die Datei, und schließen Sie den Designer.</span><span class="sxs-lookup"><span data-stu-id="237a2-134">Save the file and close the designer.</span></span>

### <a name="modify-the-elementsxml-file"></a><span data-ttu-id="237a2-135">Ändern der Datei „Elements.xml“</span><span class="sxs-lookup"><span data-stu-id="237a2-135">Modify the elements.xml file</span></span>

1. <span data-ttu-id="237a2-136">Der nächste Schritt erfordert, dass Sie direkt im unformatierten XML des Inhaltstyps arbeiten. Wählen Sie daher im **Projektmappen-Explorer** die dem Inhaltstyp **NewEmployee** untergeordnete Datei elements.xml aus.</span><span class="sxs-lookup"><span data-stu-id="237a2-136">The next step requires that you work directly in the raw XML for the content type, so in **Solution Explorer**, select the elements.xml file child of the **NewEmployee** content type.</span></span>
    
2. <span data-ttu-id="237a2-137">Es sind bereits **FieldRef**-Elemente in der Datei für die zwei Spalten, die Sie hinzugefügt haben, vorhanden.</span><span class="sxs-lookup"><span data-stu-id="237a2-137">There are already **FieldRef** elements in the file for the two columns that you added.</span></span> <span data-ttu-id="237a2-138">Fügen Sie **FieldRef**-Elemente für zwei integrierte SharePoint-Spalten als Peers für die beiden bereits vorhandenen Spalten hinzu.</span><span class="sxs-lookup"><span data-stu-id="237a2-138">Add **FieldRef** elements for two built-in SharePoint columns as peers of the two that are already there.</span></span> <span data-ttu-id="237a2-139">Nachfolgend finden Sie das Markup für die Elemente.</span><span class="sxs-lookup"><span data-stu-id="237a2-139">The following is the markup for the elements.</span></span> <span data-ttu-id="237a2-140">*Sie müssen dieselben GUIDs für das ID-Attribut verwenden, da es sich um integrierte Feldtypen mit festen IDs handelt.*</span><span class="sxs-lookup"><span data-stu-id="237a2-140">*You must use these same GUIDs for the ID attribute because these are built-in field types with fixed IDs.*</span></span> <span data-ttu-id="237a2-141">Fügen Sie sie *über* den beiden **FieldRef**-Elementen für die benutzerdefinierten Websitespalten hinzu.</span><span class="sxs-lookup"><span data-stu-id="237a2-141">Add these *above* the two **FieldRef** elements for the custom site columns.</span></span> <span data-ttu-id="237a2-142">Beachten Sie, dass wir diesen Feldern den benutzerdefinierten Anzeigenamen **Employee** gegeben haben.</span><span class="sxs-lookup"><span data-stu-id="237a2-142">Note that we have given these fields the custom display name **Employee**.</span></span>
    
    ```
      <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
      <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
    ```
 
3. <span data-ttu-id="237a2-143">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="237a2-143">Save and close the file.</span></span>
 
###  <a name="modify-content-type-settings"></a><span data-ttu-id="237a2-144">Ändern der Inhaltstypeinstellungen</span><span class="sxs-lookup"><span data-stu-id="237a2-144">Modify Content Type settings</span></span>

1. <span data-ttu-id="237a2-145">Erweitern Sie den Knoten **Listen** im **Projektmappen-Explorer**, und wählen Sie **NewEmployeeOrientation**, um den Listentyp-Designer zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="237a2-145">Expand the **Lists** node in **Solution Explorer**, and select **NewEmployeeOrientation** to open the list type designer.</span></span>
    
2. <span data-ttu-id="237a2-146">Öffnen Sie die Registerkarte **Spalten** im Designer, und wählen Sie dann die Schaltfläche **Inhaltstypen** aus.</span><span class="sxs-lookup"><span data-stu-id="237a2-146">Open the **Columns** tab in the designer, and then select the **Content Types** button.</span></span>
    
3. <span data-ttu-id="237a2-147">Fügen Sie im Dialogfeld **Inhaltstypeinstellungen** den Inhaltstyp **NewEmployee** hinzu.</span><span class="sxs-lookup"><span data-stu-id="237a2-147">In the **Content Type Settings** dialog box, add the **NewEmployee** content type.</span></span>
    
4. <span data-ttu-id="237a2-148">Wählen Sie in der Liste der Typen den Inhaltstyp **NewEmployee** aus, und wählen Sie dann die Schaltfläche **Als Standard festlegen** aus.</span><span class="sxs-lookup"><span data-stu-id="237a2-148">Select the **NewEmployee** content type in the list of types, and then select the **Set as Default** button.</span></span>
 
5. <span data-ttu-id="237a2-149">Wählen Sie den Inhaltstyp **Element** aus, klicken Sie mit der rechten Maustaste auf die kleine Pfeilspitze, die links vom Inhaltstypnamen angezeigt wird, und wählen Sie dann **Löschen** aus.</span><span class="sxs-lookup"><span data-stu-id="237a2-149">Select the **Item** content type, right-click the small arrowhead that appears to the left of the content type name, and then select **Delete**.</span></span>
    
6. <span data-ttu-id="237a2-150">Wiederholen Sie den vorherigen Schritt für den Inhaltstyp **Ordner**, sodass **NewEmployee** als einziger Inhaltstyp angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="237a2-150">Repeat the preceding step for the **Folder** content type, so that **NewEmployee** is the only content type listed.</span></span> <span data-ttu-id="237a2-151">Das Dialogfeld sollte nun wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="237a2-151">The dialog box should now look like the following:</span></span>
    
    <span data-ttu-id="237a2-152">*Abbildung 3. Dialogfeld „Inhaltstypeinstellungen“*</span><span class="sxs-lookup"><span data-stu-id="237a2-152">*Figure 3. Content Type Settings dialog box*</span></span>

    ![Das Dialogfeld „Inhaltstypeinstellungen“, in dem nur ein einziger Inhaltstyp mit dem Namen „NewEmployee“ aufgeführt ist.](../images/b90699f4-40de-4f50-ad47-3e8773d0eb92.PNG)
 
7.  <span data-ttu-id="237a2-154">Wählen Sie **OK** aus, um das Dialogfeld zu schließen, und speichern und schließen Sie anschließend die Datei.</span><span class="sxs-lookup"><span data-stu-id="237a2-154">Select **OK** to close the dialog box, and then save and close the file.</span></span>

### <a name="modify-the-schemaxml-file-and-elementxml-file"></a><span data-ttu-id="237a2-155">Ändern der Dateien „schema.xml“ und „element.xml“</span><span class="sxs-lookup"><span data-stu-id="237a2-155">Modify the schema.xml file and element.xml file</span></span>

1. <span data-ttu-id="237a2-156">Öffnen Sie die Datei „schema.xml“.</span><span class="sxs-lookup"><span data-stu-id="237a2-156">Open the schema.xml file.</span></span>
    
2. <span data-ttu-id="237a2-157">Suchen Sie das **Felder**-Element.</span><span class="sxs-lookup"><span data-stu-id="237a2-157">Find the **Fields** element.</span></span> <span data-ttu-id="237a2-158">Es müssen drei **Feld**-Elemente vorhanden sein: **Titel**, **Abteilung** und **Orientierungsphase**.</span><span class="sxs-lookup"><span data-stu-id="237a2-158">It should have three **Field** elements: **Title**, **Division**, and **OrientationStage**.</span></span> <span data-ttu-id="237a2-159">(Diese Elemente befinden sich möglicherweise auf einer einzelnen Linie in dieser generierten Datei.</span><span class="sxs-lookup"><span data-stu-id="237a2-159">(These elements may be on a single line in this generated file.</span></span> <span data-ttu-id="237a2-160">Wenn dies der Fall ist, trennen Sie sie durch Zeilenumbrüche.)</span><span class="sxs-lookup"><span data-stu-id="237a2-160">If so, separate them with line breaks.)</span></span>
 
3. <span data-ttu-id="237a2-161">Lassen Sie die Datei geöffnet, und erweitern Sie im **Projektmappen-Explorer** den Ordner **Websitespalten** und den Knoten **Abteilung**, und öffnen Sie dann die Datei „elements.xml“ für **Abteilung**.</span><span class="sxs-lookup"><span data-stu-id="237a2-161">Leave the file open, and in **Solution Explorer**, expand the **Site Columns** folder and the **Division** node, and then open the elements.xml file for **Division**.</span></span> <span data-ttu-id="237a2-162">Das **Feld**-Element für **Abteilung** in „schema.xml“ sollte das **Feld**-Element für **Abteilung** in „elements.xml“ exakt duplizieren.</span><span class="sxs-lookup"><span data-stu-id="237a2-162">The **Field** element for **Division** in schema.xml should exactly duplicate the **Field** element in the **Division** elements.xml.</span></span> <span data-ttu-id="237a2-163">Wenn keine exakte Übereinstimmung besteht, kopieren Sie das **Feld**-Element aus der Datei „elements.xml“ der Websitespalte, und fügen Sie es anstelle des nicht übereinstimmenden **Feld**-Elements in die Datei „schema.xml“ ein.</span><span class="sxs-lookup"><span data-stu-id="237a2-163">If there is not an exact match, copy the **Field** element from the site column elements.xml file and paste it in place of the mismatched **Field** element in the schema.xml file.</span></span> <span data-ttu-id="237a2-164">Schließen Sie die Datei „element.xml“.</span><span class="sxs-lookup"><span data-stu-id="237a2-164">Close the element.xml file.</span></span>
    
4. <span data-ttu-id="237a2-165">Öffnen Sie die Datei „elements.xml“ für **Orientierungsphase**.</span><span class="sxs-lookup"><span data-stu-id="237a2-165">Open the elements.xml file for **OrientationStage**.</span></span> <span data-ttu-id="237a2-166">Auch hier muss eine exakte Übereinstimmung des **Feld**-Elements in beiden Dateien für die **Orientierungsphase** vorliegen, einschließlich aller untergeordneten Elemente, wie z. B. der Elemente **AUSWAHLMÖGLICHKEITEN** und ** ZUORDNUNGEN**.</span><span class="sxs-lookup"><span data-stu-id="237a2-166">Here, too, there must be an exact match of the  **Field** elements in the two files for **OrientationStage**, including all child elements, such as the **CHOICES** and **MAPPINGS** elements.</span></span> <span data-ttu-id="237a2-167">Wenn keine exakte Übereinstimmung besteht, kopieren Sie das **Feld**-Element aus der Datei „elements.xml“, und fügen Sie es anstelle des nicht übereinstimmenden **Feld**-Elements in die Datei „schema.xml“ ein.</span><span class="sxs-lookup"><span data-stu-id="237a2-167">If there isn't, copy the **Field** in the elements.xml file and paste it in place of the mismatched **Field** element in the schema.xml file.</span></span> <span data-ttu-id="237a2-168">Schließen Sie die Datei „element.xml“.</span><span class="sxs-lookup"><span data-stu-id="237a2-168">Close the element.xml file.</span></span>
 
5. <span data-ttu-id="237a2-169">Während Sie sich weiterhin in der Datei „schema.xml" befinden, suchen Sie im Element **View**, dessen **BaseViewID**-Wert gleich 1 ist, nach dem untergeordneten **ViewFields**-Element, und fügen Sie ihm dann die folgenden zwei **FieldRef**-Elemente als untergeordnete Elemente hinzu.</span><span class="sxs-lookup"><span data-stu-id="237a2-169">Still in the schema.xml file, in the **View** element whose **BaseViewID** value is "1", find the child **ViewFields** element, and then add the following two **FieldRef** elements as children of it.</span></span> <span data-ttu-id="237a2-170"> Möglicherweise sind sie bereits vorhanden, jedoch fehlt ein **ID**-Attribut.</span><span class="sxs-lookup"><span data-stu-id="237a2-170">They may already be there but missing an **ID** attribute.</span></span> <span data-ttu-id="237a2-171">Wenn dies der Fall ist, fügen Sie das ID-Attribut hinzu.</span><span class="sxs-lookup"><span data-stu-id="237a2-171">If so, add the ID attribute.</span></span>
    
    ```
      <FieldRef Name="Division" ID="{GUID from the Field element}" />
      <FieldRef Name="OrientationStage" ID="{GUID from the Field element}" />

    ```

6. <span data-ttu-id="237a2-172">Ersetzen Sie die zwei Platzhalter- **ID**-Attributwerte durch die GUIDs aus den entsprechenden **Field**-Elementen im Element **ContentType** für **NewEmployee**, das sich zuvor in der Datei „schema.xml" befand.</span><span class="sxs-lookup"><span data-stu-id="237a2-172">Replace the two placeholder **ID** attribute values with the GUIDs from the corresponding **Field** elements in the **ContentType** element for **NewEmployee** that is earlier in the schema.xml file.</span></span> <span data-ttu-id="237a2-173">Vergessen Sie nicht die umschließenden Klammern „{}".</span><span class="sxs-lookup"><span data-stu-id="237a2-173">Don't forget the framing braces "{}".</span></span> <span data-ttu-id="237a2-174">Das **ViewFields**-Element für das **View**-Element „1“ sollte wie folgt aussehen (Ihre GUIDs können abweichen):</span><span class="sxs-lookup"><span data-stu-id="237a2-174">The **ViewFields** for the "1" **View** should look like the following (your GUIDs may be different):</span></span>

    ```
      <ViewFields>
        <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
        <FieldRef Name="Division" ID="{509d2d67-9a96-4596-9b3b-58449cdcc6ff}" />
        <FieldRef Name="OrientationStage" ID="{38a3b54c-acf3-4ddf-b748-55c7c28d4cc2}" />        
      </ViewFields>
    ```

7. <span data-ttu-id="237a2-175">Suchen Sie in der Datei „schema.xml“ nach dem **View**-Element, dessen **BaseViewID** den Wert „0“ hat.</span><span class="sxs-lookup"><span data-stu-id="237a2-175">Still in the schema.xml file, find the **View** element whose **BaseViewID** value is "0".</span></span> <span data-ttu-id="237a2-176">Suchen Sie nach dem **ViewFields**-Element in diesem Element.</span><span class="sxs-lookup"><span data-stu-id="237a2-176">Find the **ViewFields** element within it.</span></span>

8. <span data-ttu-id="237a2-177">Kopieren Sie den gesamten **ViewFields**-Abschnitt aus der Ansicht „1“ in den **ViewFields**-Abschnitt der Ansicht „0“.</span><span class="sxs-lookup"><span data-stu-id="237a2-177">Copy the entire **ViewFields** section from View "1" over the **ViewFields** section of View "0".</span></span> <span data-ttu-id="237a2-178">Die beiden Ansichten sollten jetzt identische **ViewFields**-Abschnitte besitzen.</span><span class="sxs-lookup"><span data-stu-id="237a2-178">The two views should now have identical **ViewFields** sections.</span></span>
    
9. <span data-ttu-id="237a2-179">Speichern und schließen Sie die Datei schema.xml.</span><span class="sxs-lookup"><span data-stu-id="237a2-179">Save and close the schema.xml file.</span></span>

10. <span data-ttu-id="237a2-180">Erweitern Sie im Ordner **Listen** den Knoten **NewEmployeeOrientation** und die untergeordnete Listeninstanz **NewEmployeesInSeattle**.</span><span class="sxs-lookup"><span data-stu-id="237a2-180">In the **Lists** folder, expand both the **NewEmployeeOrientation** node and its child list instance **NewEmployeesInSeattle**.</span></span> <span data-ttu-id="237a2-181">Sie sollten die elements.xls für die Vorlage deutlich von der elements.xls für die Instanz unterscheiden können.</span><span class="sxs-lookup"><span data-stu-id="237a2-181">You should be able to clearly see and distinguish the elements.xml for the template from the elements.xml for the instance.</span></span> <span data-ttu-id="237a2-182">Öffnen Sie die Datei für die Instanz.</span><span class="sxs-lookup"><span data-stu-id="237a2-182">Open the one for the instance.</span></span> 
    
11. <span data-ttu-id="237a2-183">Fügen Sie zwei **Field**-Elemente zum ersten **Row**-Element hinzu, sodass das **Row**-Element wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="237a2-183">Add two **Field** elements to the first **Row** element, so that the **Row** element looks like the following:</span></span>
    
    ``` 
    <Row>
      <Field Name="Title">Tom Higginbotham</Field>
      <Field Name="Division">Manufacturing</Field>
      <Field Name="OrientationStage">Tour of building</Field>
    </Row>
    ```

12. <span data-ttu-id="237a2-184">Speichern und schließen Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="237a2-184">Save and close the file.</span></span>
    

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="237a2-185">Ausführen und Testen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="237a2-185">Run and test the add-in</span></span>

1. <span data-ttu-id="237a2-p117">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="237a2-p117">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
     
2. <span data-ttu-id="237a2-188">Wenn die Standardseite des Add-Ins geöffnet wird, wählen Sie den Link für **Neue Mitarbeiter in Seattle** aus, um die benutzerdefinierte Listeninstanz zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="237a2-188">When the add-in's default page opens, select the **New Employees in Seattle** link to open the custom list instance.</span></span>
 
3. <span data-ttu-id="237a2-189">Die Listenseite mit den Spalten **Abteilung** und **Orientierungsphase** sind darin enthalten.</span><span class="sxs-lookup"><span data-stu-id="237a2-189">The list page opens and the **Division** and **OrientationStage** columns are on it.</span></span> <span data-ttu-id="237a2-190">Es ist nicht erforderlich, dass ein Benutzer sie manuell hinzufügt, da sie Bestandteil des Listeninhaltstyps sind.</span><span class="sxs-lookup"><span data-stu-id="237a2-190">It is not necessary for a user to add them manually because they are part of the list's content type.</span></span> <span data-ttu-id="237a2-191">Das erste Element enthält die Daten, die Sie hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="237a2-191">The top item has the data you added.</span></span>
    
    <span data-ttu-id="237a2-192">*Abbildung 4. Liste „Neue Mitarbeiter in Seattle“*</span><span class="sxs-lookup"><span data-stu-id="237a2-192">*Figure 4. New Employees in Seattle list*</span></span>

    ![Die Liste „Neue Mitarbeiter in Seattle“, in der die Spalten „Abteilung“ und „Orientierungsphase“ bereits vorhanden sind.](../images/b654af45-663e-425c-b7c7-b8b5524cb316.PNG) 
 
4. <span data-ttu-id="237a2-194">Versuchen Sie, der Liste neue Elemente hinzuzufügen und vorhandene Elemente zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="237a2-194">Try adding new items to the list and editing existing items.</span></span>
    
5. <span data-ttu-id="237a2-195">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="237a2-195">To end the debugging session, close the browser window or stop debugging in Visual Studio.</span></span> <span data-ttu-id="237a2-196">Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="237a2-196">Each time that you select F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
6. <span data-ttu-id="237a2-197">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben.</span><span class="sxs-lookup"><span data-stu-id="237a2-197">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while.</span></span> <span data-ttu-id="237a2-198">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="237a2-198">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="237a2-199">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="237a2-199">Next steps</span></span>
<span data-ttu-id="237a2-200"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="237a2-200"></span></span>

<span data-ttu-id="237a2-201">Im nächsten Artikel dieser Reihe [fügen Sie ein Webpart zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In hinzu](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="237a2-201">In the next article in this series, you'll [add a Web Part to a page in a SharePoint-hosted SharePoint Add-in](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md).</span></span>
