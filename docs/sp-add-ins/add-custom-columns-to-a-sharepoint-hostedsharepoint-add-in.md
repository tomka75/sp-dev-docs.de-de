---
title: "Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In"
ms.date: 10/26/2017
ms.prod: sharepoint
redirect_url: https://docs.microsoft.com/en-us/sharepoint/dev/sp-add-ins/add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in/
ms.openlocfilehash: 35e29bf1ef2d5d694db49fbfa574c6a6514ebb88
ms.sourcegitcommit: 56dde2f5d7919cc9998846c8c137108ca326ba43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2017
---
# <a name="add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in"></a><span data-ttu-id="b4c3e-102">Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="b4c3e-102">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>
<span data-ttu-id="b4c3e-103">Erfahren Sie, wie Sie benutzerdefinierte Spalten in SharePoint-Add-Ins einschließen.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-103">Learn how to include custom columns in an SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="b4c3e-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="b4c3e-107">Dies ist der dritte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut:</span><span class="sxs-lookup"><span data-stu-id="b4c3e-107">This is the third in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the pervious articles in this series:</span></span>
 

-  [<span data-ttu-id="b4c3e-108">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="b4c3e-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="b4c3e-109">Bereitstellung und Installation eines von SharePoint gehosteten Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b4c3e-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
    
 

 <span data-ttu-id="b4c3e-p102">**Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_SP-Hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeColumns.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p102">**Note**  If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeColumns.sln file.</span></span>
 

<span data-ttu-id="b4c3e-112">In diesem Artikel kehren wir zum Codieren zurück, indem wir einige Websitespalten zum SharePoint-Add-In „Orientierung für Mitarbeiter“ hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-112">In this article we get back to coding by adding some site columns to the Employee Orientation SharePoint Add-in.</span></span>
 

## <a name="create-custom-column-types"></a><span data-ttu-id="b4c3e-113">Erstellen benutzerdefinierter Spaltentypen</span><span class="sxs-lookup"><span data-stu-id="b4c3e-113">Create custom column types</span></span>


 

 

1. <span data-ttu-id="b4c3e-p103">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie **Hinzufügen** > **Neuer Ordner** aus. Nennen Sie den Ordner „Websitespalten“.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p103">In  **Solution Explorer**, right-click the project and choose  **Add** > **New Folder**. Name the folder Site Columns.</span></span>
    
 
2. <span data-ttu-id="b4c3e-p104">Klicken Sie mit der rechten Maustaste auf den neuen Ordner, und wählen Sie **Hinzufügen** > **Neues Element** aus. Das Dialogfeld **Neues Element hinzufügen** wird mit dem Knoten **Office/SharePoint** geöffnet.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p104">Right-click the new folder and choose  **Add** > **New Item**. The  **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>
    
 
3. <span data-ttu-id="b4c3e-118">Wählen Sie **Websitespalte** aus, geben Sie ihr den Namen „Abteilung“, und wählen Sie **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-118">Choose  **Site Column**, give it the name Division, and choose  **Add**.</span></span>
    
 
4. <span data-ttu-id="b4c3e-119">Bearbeiten Sie in der Datei „elements.xml“ für die neue Websitespalte das Element **Field** so, dass es die im folgenden Beispiel gezeigten Attribute und Werte hat, mit der Ausnahme, dass *Sie **nicht** den Wert der GUID* für das Attribut **ID** ändern sollten, der von Visual Studio dafür generiert wurde. *Seien Sie also vorsichtig, wenn Sie Kopieren und Einfügen verwenden.*</span><span class="sxs-lookup"><span data-stu-id="b4c3e-119">In the elements.xml file for the new site column, edit the  **Field** element so that it has the attributes and values shown in the following example, except that *you should  **not** change the GUID*  for the **ID** attribute from the value that Visual Studio generated for it, *so be careful if you are using copy-and-paste*  .</span></span>
    
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

5. <span data-ttu-id="b4c3e-120">Fügen Sie eine weitere **Websitespalte** im selben Ordner mit dem Namen „OrientationStage“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-120">Add another  **Site Column** to the same folder namedOrientationStage.</span></span>
    
 
6. <span data-ttu-id="b4c3e-121">Bearbeiten Sie in der Datei „elements.xml“ für die neue Websitespalte das Element **Field** so, dass es die im folgenden Beispiel dargestellten Attribute und Werte aufweist, mit der Ausnahme, dass der Wert der GUID für das Attribut **ID**, den Visual Studio dafür generiert hat, nicht geändert werden sollte.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-121">In the elements.xml file for the new site column, edit the  **Field** element so that it has the attributes and values shown in the following example, except that you should not change the GUID for the **ID** attribute from the value that Visual Studio generated for it.</span></span>
    
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

7. <span data-ttu-id="b4c3e-p105">Da es sich um ein Auswahlfeld handelt, müssen Sie die Auswahlmöglichkeiten und die Reihenfolge angeben, in der diese in der Dropdownliste angezeigt werden sollen, wenn ein Benutzer eine Auswahl vornimmt. Und da es ein Pflichtfeld ist, müssen Sie einen Standardwert angeben. Fügen Sie das folgende untergeordnete Markup zum Element **Field** hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p105">Because this is a Choice field, you must specify the possible choices and the order in which they should appear in the drop-down list when a user is making a choice. And because it is a required field, you must specify a default value. Add the following child markup to the  **Field** element.</span></span>
    
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

8. <span data-ttu-id="b4c3e-125">Speichern Sie alle Dateien.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-125">Save all files.</span></span>
    
 

## <a name="run-the-add-in-and-test-the-columns"></a><span data-ttu-id="b4c3e-126">Ausführen des Add-Ins und Testen der Spalten</span><span class="sxs-lookup"><span data-stu-id="b4c3e-126">Run the add-in and test the columns</span></span>


 

 

1. <span data-ttu-id="b4c3e-p106">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p106">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
    
 
2. <span data-ttu-id="b4c3e-129">Wenn die Standardseite des Add-Ins geöffnet wird, wählen Sie den Link für **Neue Mitarbeiter in Seattle** aus, um die benutzerdefinierte Listeninstanz zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-129">When the add-in's default page opens, choose the  **New Employees in Seattle** link to open the custom list instance.</span></span>
    
 
3. <span data-ttu-id="b4c3e-130">Öffnen Sie die Seite **Einstellungen** der Liste, und fügen Sie die zwei Spalten mit den folgenden Schritten hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-130">Open the list's  **Settings** page and add the two columns to it with these steps.</span></span>
    
      1. <span data-ttu-id="b4c3e-131">Klicken Sie auf die Popupschaltfläche **· · ·** direkt über der Liste, und wählen Sie dann **Ansicht erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-131">Click the callout button,  **· · ·**, just above the list, and then choose  **Create View**.</span></span>
    
 
  2. <span data-ttu-id="b4c3e-p107">Die Seite **Ansichtstyp** wird mit der Breadcrumb-Struktur **Einstellungen und Ansichtstyp** im oberen Bereich geöffnet. Klicken Sie auf den Breadcrumb **Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p107">The  **View Type** page opens, with the breadcrumb structure **Settings > View Type** near the top. Click the **Settings** breadcrumb.</span></span>
    
    <span data-ttu-id="b4c3e-134">**Schritte zum Öffnen der Seite mit Listeneinstellungen**</span><span class="sxs-lookup"><span data-stu-id="b4c3e-134">**Steps to open the list settings page**</span></span>

 

  ![Liste "Neue Mitarbeiter in Seattle", wobei die Beschriftungsschaltfläche und das Element "Ansicht erstellen" als erster Schritt markiert sind. Dann über den Pfeil zur Seite "Ansicht erstellen", wobei das Breadcrumb "Einstellungen" markiert ist.](../images/6c119cae-adf8-42ff-9890-f3aa1e11719d.png)
 

    
    
 
  3. <span data-ttu-id="b4c3e-137">Öffnen Sie auf der Seite **Einstellungen** den Link **Aus vorhandenen Websitespalten hinzufügen** etwa in der Mitte der Seite links.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-137">On the  **Settings** page, open the **Add from existing site columns** link on the left about halfway down the page.</span></span>
    
    <span data-ttu-id="b4c3e-138">**Seite mit Listeneinstellungen**</span><span class="sxs-lookup"><span data-stu-id="b4c3e-138">**List settings page**</span></span>

 

  ![Die Seite mit Listeninstanzeinstellungen, auf der der Link für „Spalten aus Websitespalten hinzufügen“ hervorgehoben ist.](../images/a8698b77-b9d2-40f6-89f6-ccc3c6e06073.png)
 

    
    
 
  4. <span data-ttu-id="b4c3e-140">Wählen Sie auf der Seite **Spalten aus Websitespalten hinzufügen** in der Dropdownliste **Websitespalten auswählen aus** die Option **Orientierung für Mitarbeiter** aus.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-140">On the  **Add Columns from Site Columns** page, choose **Employee Orientation** on the **Select site columns from** drop down list.</span></span>
    
    <span data-ttu-id="b4c3e-141">**Seite „Spalten aus Websitespalten hinzufügen“**</span><span class="sxs-lookup"><span data-stu-id="b4c3e-141">**Add Columsn from Site Columns page**</span></span>

 

  ![Das Steuerelement für die SharePoint-Spaltenauswahl, wobei „Orientierung für Mitarbeiter“ in der Dropdownliste mit der Bezeichnung „Websitespalten auswählen“ ausgewählt ist.](../images/3b33c622-c52a-45fd-8ea1-d7f307539753.png)
 

    
    
 
  5. <span data-ttu-id="b4c3e-143">Fügen Sie die Spalten **Abteilung** und **Orientierungsphase** zum Feld **Hinzuzufügende Spalten** hinzu.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-143">Add the  **Division** and **OrientationStage** columns to the **Columns to add** box.</span></span>
    
 
  6. <span data-ttu-id="b4c3e-144">Wählen Sie **OK** aus, um zur Seite **Einstellungen** zurückzukehren, und klicken Sie dann auf den Breadcrumb **Neue Mitarbeiter in Seattle** im oberen Bereich der Seite.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-144">Choose  **OK** to return to the **Settings** page, and then click the **New Employees in Seattle** breadcrumb near the top of the page.</span></span>
    
 
4. <span data-ttu-id="b4c3e-p109">Die neuen Spalten befinden sich jetzt in der Liste. Fügen Sie der Liste ein neues Element hinzu. Auf dem Bearbeitungsformular enthält das Feld **Orientierungsphase** bereits den Standardwert „Nicht gestartet“. (Die vorhandenen Elemente in diesem Feld sind leer, da sie erstellt wurden, bevor sich das Feld in der Liste befand.)</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p109">The new columns are now on the list. Add a new item to the list. On the edit form, the  **Orientation Stage** field will already have the default valueNot Started. (The existing items will be blank in this field because they were created before the field was on the list.)</span></span>
    
    <span data-ttu-id="b4c3e-149">**Die Liste mit neuen Spalten**</span><span class="sxs-lookup"><span data-stu-id="b4c3e-149">**The list with new columns**</span></span>

 

  ![Die Liste mit den neuen Spalten „Abteilung“ und „Orientierungsphase“.](../images/d4e17424-c06b-4635-aab8-4912cee5fe35.png)
 

    
    
 
5. <span data-ttu-id="b4c3e-p110">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p110">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
6. <span data-ttu-id="b4c3e-p111">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewähr, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="b4c3e-p111">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="b4c3e-155"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="b4c3e-155"></span></span>

<span data-ttu-id="b4c3e-156">Da Sie nicht wirklich möchten, dass Ihre Benutzer die benutzerdefinierten Spalten manuell zur Liste hinzufügen müssen, erstellen Sie im nächsten Artikel dieser Reihe einen benutzerdefinierten Inhaltstyp, der die benutzerdefinierten Spalten enthält und automatisch mit der Listenvorlage für neue Mitarbeiter verknüpft wird: [Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="b4c3e-156">You don't really want your users to have to manually add the custom columns to the list, so in the next article in this series, you'll create a custom content type that includes the custom columns and is automatically associated with the New Employees list template:  [Add a custom content type to a SharePoint-hostedSharePoint Add-in](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in.md).</span></span> 
 

 

