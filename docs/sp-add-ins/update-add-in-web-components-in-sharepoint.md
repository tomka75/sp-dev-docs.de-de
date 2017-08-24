
# <a name="update-add-in-web-components-in-sharepoint"></a><span data-ttu-id="32060-101">Aktualisieren von SharePoint-Add-In-Webkomponenten</span><span class="sxs-lookup"><span data-stu-id="32060-101">Update add-in web components in SharePoint</span></span>
<span data-ttu-id="32060-102">Aktualisieren von Seiten, Listen, Inhaltstypen und anderen Add-In-Webkomponenten in einem SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="32060-102">Update pages, lists, content types, and other add-in web components in a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="32060-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="32060-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="prerequisites-for-updating-the-add-in-web-components"></a><span data-ttu-id="32060-106">Voraussetzungen für die Aktualisierung der Add-In-Webkomponenten</span><span class="sxs-lookup"><span data-stu-id="32060-106">Prerequisites for updating the add-in web components</span></span>
<span data-ttu-id="32060-107"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="32060-107"></span></span>

<span data-ttu-id="32060-108">Kenntnisse des Themas [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins) und der darin aufgeführten erforderlichen Komponenten und Kernkonzepte.</span><span class="sxs-lookup"><span data-stu-id="32060-108">Be familiar with  [Update SharePoint Add-ins](update-sharepoint-add-ins) and the prerequisites and core concepts included in it.</span></span>
 

 
<span data-ttu-id="32060-109">In diesem Thema wird davon ausgegangen, dass Sie die neueste Version des Add-Ins entwickelt und getestet haben, wie unter  [Erstellen und Debuggen Sie die neue Version, als ob es ein ganz neues Add-In wäre](update-sharepoint-add-ins#DebugFirst) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="32060-109">This topic assumes that you have developed and tested the latest version of the add-in as described in the  [Create and debug the new version as if it were a brand new add-in](update-sharepoint-add-ins#DebugFirst).</span></span>
 

 

## <a name="update-sharepoint-components-in-the-add-in-web"></a><span data-ttu-id="32060-110">Aktualisieren von SharePoint-Komponenten im Add-In-Web</span><span class="sxs-lookup"><span data-stu-id="32060-110">Update SharePoint components in the add-in web</span></span>
<span data-ttu-id="32060-111"><a name="UpdatingAppWeb"> </a></span><span class="sxs-lookup"><span data-stu-id="32060-111"></span></span>

<span data-ttu-id="32060-p102">Alle SharePoint-Komponenten, die im Add-In-Web bereitgestellt werden, sind in Features im **Web**-Bereich des Add-In-Pakets enthalten. Aus diesem Grund muss zur Aktualisierung dieser Komponenten mindestens eines der Features aktualisiert werden. Dieser Vorgang hat sich seit SharePoint 2010 nicht verändert und ist im Artikel [Vorgehensweise: Hinzufügen von Elementen zu einem vorhandenen Feature](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) im SharePoint 2010 SDK dokumentiert. Andere Artikel unter dem Knoten [Aktualisieren von Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) können ebenfalls hilfreich sein. Beachten Sie jedoch, dass Add-Ins auf dem SharePoint-Server keinen benutzerdefinierten Code enthalten dürfen; manche Aspekte des Featureupgrades in SharePoint 2010 gelten daher nicht für das Aktualisieren von Add-Ins. Sie können beispielsweise nicht das Element [CustomUpgradeAction](http://msdn.microsoft.com/library/16a2182e-80aa-4184-8071-8f717ee5c572%28Office.15%29.aspx) verwenden, wenn Sie das Feature eines SharePoint-Add-Ins aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="32060-p102">All of the SharePoint components that are deployed to the add-in web are contained in **Web**-scoped Features in the add-in package. For that reason, updating these components is a matter of updating one or more of the Features. This process has not changed since SharePoint 2010 and is documented in  [How to: Add Elements to an Existing Feature](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) in the SharePoint 2010 SDK. Other articles in the [Upgrading Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) node may be helpful also, but consider that add-ins must not include custom code on the SharePoint server, so some aspects of Feature upgrading in SharePoint 2010 are not relevant to updating add-ins. For example, you can't use the [CustomUpgradeAction](http://msdn.microsoft.com/library/16a2182e-80aa-4184-8071-8f717ee5c572%28Office.15%29.aspx) element when you upgrade the Feature of a SharePoint Add-in.</span></span>
 

 

### <a name="what-can-and-cannot-be-done-declaratively"></a><span data-ttu-id="32060-117">Welche Aufgaben deklarativ ausgeführt werden können und welche nicht</span><span class="sxs-lookup"><span data-stu-id="32060-117">What can and cannot be done declaratively</span></span>

<span data-ttu-id="32060-p103">Bei einem SharePoint-gehosteten Add-In können Sie nur XML-Markup zum Aktualisieren eines Add-Ins verwenden, und es gelten einige Einschränkungen, wie Sie ein Add-In in einem Update deklarativ ändern können. In einem vom Anbieter gehosteten Add-In können Sie einen  [UpdatedEventEndpoint Handler](create-a-handler-for-the-update-event-in-sharepoint-add-ins) implementieren, um Aktionen auszuführen, die nicht deklarativ ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="32060-p103">With a SharePoint-hosted add-in, you can only use XML markup to update an add-in and there are some limits on how you can declaratively change an add-in in an update. In a provider-hosted add-in, you can implement a  [UpdatedEventEndpoint handler](create-a-handler-for-the-update-event-in-sharepoint-add-ins) to do things that can't be done declaratively.</span></span>
 

 
<span data-ttu-id="32060-p104">Das Hinzufügen von Komponenten zu einem Add-In ist einfach. Alle Komponenten, die zum Einfügen in ein Add-In berechtigt sind, können auch in einem Update hinzugefügt werden. (Informationen zu den Komponenten, die in einem Add-In enthalten sein können, finden Sie unter  [Typen von SharePoint-Komponenten, die in einem SharePoint-Add-In enthalten sein können](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013#TypesOfSPComponentsInApps).) Wenn Sie eine vorhandene Komponente deklarativ ändern möchten, sollten Sie die folgenden Punkte in Betracht ziehen.</span><span class="sxs-lookup"><span data-stu-id="32060-p104">Adding components to an add-in is easy. Any component that is eligible to be included in an add-in can also be added in an update. (For details about what components can be in an add-in, see  [Types of SharePoint components that can be in a SharePoint Add-in](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013#TypesOfSPComponentsInApps). ) But when you want to modify an existing component declaratively, consider the following points.</span></span> 
 

 

- <span data-ttu-id="32060-p105">Der Datentyp einer Liste oder eines Inhaltstypfelds (einer Spalte) kann nach der anfänglichen Bereitstellung in keinem Fall geändert werden. Ändern Sie vor allem nicht den Datentyp eines Felds im Rahmen eines Add-In-Updates ( *auch nicht programmgesteuert*  ). Alternativ können Sie ein neues Feld hinzufügen und das alte Feld ausblenden. Wenn das Add-In benutzerdefinierte Formulare zum Erstellen, Bearbeiten oder Anzeigen von Elementen enthält, müssen Sie in diesen Formularen entsprechende Änderungen vornehmen. Fügen Sie beispielsweise Benutzeroberflächenelemente für das neue Feld hinzu, und entfernen Sie Benutzeroberflächenelemente für das alte Feld. (In einem vom Anbieter gehosteten Add-In können Sie Daten programmgesteuert vom alten zum neuen Feld verschieben und dann das alte Feld löschen.)</span><span class="sxs-lookup"><span data-stu-id="32060-p105">The data type of a list or content type field (column) cannot be changed after its initial deployment in any circumstance. In particular, do not change the data type of a field as part of an add-in update ( *not even programmatically*  ). As an alternative, you can add a new field. If the add-in includes custom item create, edit, or view forms; be sure to make corresponding changes in these forms. For example, add UI for the new field and remove UI for the old one. (In a provider-hosted add-in, you can programmatically move data from the old field to the new one and then delete the old. )</span></span>
    
 
- <span data-ttu-id="32060-131">Listen, Listeninstanzen, Inhaltstypen oder Felder können im Updatemarkup nicht gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="32060-131">Lists, list instances, content types, or fields cannot be deleted in the update markup.</span></span>
    
 
- <span data-ttu-id="32060-p106">Dateien können nicht aus dem Add-In-Web im Updatemarkup gelöscht werden. Allerdings können Sie den Inhalt einer Datei ändern.</span><span class="sxs-lookup"><span data-stu-id="32060-p106">Files cannot be deleted from the add-in web in update markup. However, you can change the contents of any file.</span></span>
    
 
- <span data-ttu-id="32060-134">Die Elemente **CustomUpgradeAction** und **MapFile** können beim Aktualisieren eines SharePoint-Add-Ins nicht verwendet werden, auch wenn sie in Visual Studio-IntelliSense verfügbar zu sein scheinen.</span><span class="sxs-lookup"><span data-stu-id="32060-134">The **CustomUpgradeAction** and **MapFile** elements cannot be used when updating a SharePoint Add-in, although they may appear available in Visual Studio intellisense.</span></span>
    
 

### <a name="update-the-add-in-web-for-the-first-time"></a><span data-ttu-id="32060-135">Erstmaliges Aktualisieren des Add-In-Webs</span><span class="sxs-lookup"><span data-stu-id="32060-135">Update the add-in web for the first time</span></span>

<span data-ttu-id="32060-p107">Die Verfahren in diesem Abschnitt zeigen, wie Sie Inhaltstypen, Listen, Dateien und andere SharePoint-Komponenten im Add-In-Web hinzufügen oder aktualisieren. Der Einfachheit halber wird davon ausgegangen, dass alle Komponenten Teil eines einzigen Features im Add-In-Web sind, Add-In-Webs können jedoch mehrere Funktionen aufweisen, und Sie können mehrere Features im selben Update aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="32060-p107">The procedures in this section explain how to add or update content types, lists, files, and other SharePoint components in the add-in web. For simplicity, we assume that all the components are part of a single Feature in the add-in web, but add-in webs can have multiple Features and you can update more than one in the same update.</span></span>
 

 
<span data-ttu-id="32060-p108">Die Microsoft Office-Entwicklertools für Visual Studio sind darauf ausgelegt, neue Add-Ins zu erstellen, und das Standardverhalten der Tools ist manchmal nicht optimal, wenn Sie ein Add-In aktualisieren. Für mehr Kontrolle über den Prozess sollten Sie damit beginnen, den Feature-Designer mithilfe des folgenden Verfahrens zu deaktivieren, damit Sie die rohe XML-Datei für das Feature direkt bearbeiten können.</span><span class="sxs-lookup"><span data-stu-id="32060-p108">The Microsoft Office Developer Tools for Visual Studio are oriented to creating new add-ins and the default behavior of the tools is sometimes not optimal when you are updating an add-in. To get more control over the process, you should begin by disabling the Feature Designer using the following procedure, so that you can directly edit the raw feature XML.</span></span> 
 

 

### <a name="to-edit-the-feature-xml"></a><span data-ttu-id="32060-140">So bearbeiten Sie den Feature-XML-Code</span><span class="sxs-lookup"><span data-stu-id="32060-140">To edit the Feature XML</span></span>


1. <span data-ttu-id="32060-p109">Öffnen Sie im **Projektmappen-Explorer** die Datei „_{FeatureName}_.features“. Sie wird im Feature-Designer geöffnet.</span><span class="sxs-lookup"><span data-stu-id="32060-p109">In **Solution Explorer**, open the  _{FeatureName}_.features file. It opens in the Feature designer.</span></span>
    
 
2. <span data-ttu-id="32060-143">Öffnen Sie die Registerkarte **Manifest**, und erweitern Sie **Bearbeitungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="32060-143">Open the **Manifest** tab and expand **Edit Options**.</span></span>
    
 
3. <span data-ttu-id="32060-144">Wählen Sie **Generierten XML-Code überschreiben und Manifest im XML-Editor bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="32060-144">Choose **Overwrite generated XML and edit manifest in the XML editor**.</span></span>
    
 
4. <span data-ttu-id="32060-145">Wählen Sie **Ja**, wenn Sie gefragt werden, ob Sie den Designer deaktivieren möchten.</span><span class="sxs-lookup"><span data-stu-id="32060-145">Choose **Yes** to the prompt to disable the designer.</span></span>
    
 
5. <span data-ttu-id="32060-p110">Wählen Sie in der daraufhin geöffneten Ansicht **Bearbeiten Sie das Manifest im XML-Editor**. Die Datei „_{FeatureName}_.Template.xml“ wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="32060-p110">On the view that opens, choose **Edit manifest in the XML editor**. The  _{FeatureName}_.Template.xml file opens.</span></span> 
    
    <span data-ttu-id="32060-148">**Öffnen des Feature-XML-Editors**</span><span class="sxs-lookup"><span data-stu-id="32060-148">**Opening the Feature XML editor**</span></span>

 

  ![Schritte zum Öffnen des Feature-XML-Editors](../../images/UpdateAppOpenFeatureXML.png)
 

 

 

 <span data-ttu-id="32060-p111">**Vorsicht** Fügen Sie keine „<!-- -->“-Kommentare zur Datei „_{FeatureName}_.features“ hinzu. Kommentare werden von der Upgradeinfrastruktur nicht unterstützt, und beim Upgrade tritt ein Fehler auf, wenn sich Kommentare in der Datei befinden. Sie werden in den Markupbeispielen in diesem Artikel nur verwendet, um Ihnen zu zeigen, wo Sie das Markup einfügen sollten.</span><span class="sxs-lookup"><span data-stu-id="32060-p111">**Caution** Do not add "!-- --<!-- -->" comments to the  _{FeatureName}_.features file. Comments are not supported by the upgrade infrastructure and the upgrade will fail if comments are in the file. They are used in the markup examples of this article only to indicate to you where your markup should go.</span></span>
 

<span data-ttu-id="32060-153">Verwenden Sie die folgenden Schritte zum Aktualisieren des Add-In-Web-Features.</span><span class="sxs-lookup"><span data-stu-id="32060-153">Use the following steps to update the add-in web Feature.</span></span>
 

 

### <a name="to-update-the-add-in-web-feature-the-first-time"></a><span data-ttu-id="32060-154">So aktualisieren Sie das Add-In-Web-Feature zum ersten Mal</span><span class="sxs-lookup"><span data-stu-id="32060-154">To update the add-in web Feature the first time</span></span>


1. <span data-ttu-id="32060-p112">Erhöhen Sie das Attribut **Version** des [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx)-Elements, wenn dies noch nicht über die Office Developer Tools für Visual Studio ausgeführt wurde, als Sie die Versionsnummer im Add-In-Manifest erhöht haben. (Die Tools führen die Erhöhung nicht in jedem Szenario durch, deshalb müssen Sie dies überprüfen.) Sie sollten dieselbe Versionsnummer wie für das Add-In verwenden. Sie sollten eine Erhöhung der Featureversion auch dann in Betracht ziehen, wenn andere Komponenten des Add-Ins aktualisiert werden, aber nicht das Add-In-Web-Feature selbst. Die Logik des [VersionRange](http://msdn.microsoft.com/library/cd715e38-6ec3-43b2-8007-6d0ed8865d91%28Office.15%29.aspx)-Elements (das im Abschnitt [Anschließende Aktualisierungen des Add-In-Webs](#SubsequentUpgrades) erläutert wird) ist einfacher zu verwalten, wenn die Add-In-Version und die Featureversion immer gleich sind.</span><span class="sxs-lookup"><span data-stu-id="32060-p112">Increment the **Version** attribute of the [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx) element, if the Office Developer Tools for Visual Studio did not already do so when you incremented the version number in the add-in manifest. (The tools don't do this in every scenario, so you need to verify.) You should use the same version number that you use for the add-in. You should even consider raising the Feature version when other components of the add-in are being updated, but not the add-in web Feature itself. The logic of the [VersionRange](http://msdn.microsoft.com/library/cd715e38-6ec3-43b2-8007-6d0ed8865d91%28Office.15%29.aspx) element (which is discussed in the section [Subsequent updates of the add-in web](#SubsequentUpgrades)) is easier to manage when the add-in version and the Feature version are always the same.</span></span> 
    
 
2. <span data-ttu-id="32060-p113">Löschen Sie nichts im [ElementManifests](http://msdn.microsoft.com/library/d8d4db7e-2bc2-40c6-958b-d5683bdee87a%28Office.15%29.aspx)-Abschnitt der Datei. Aus diesem Abschnitt wird niemals etwas gelöscht.</span><span class="sxs-lookup"><span data-stu-id="32060-p113">Don't delete anything in the  [ElementManifests](http://msdn.microsoft.com/library/d8d4db7e-2bc2-40c6-958b-d5683bdee87a%28Office.15%29.aspx) section of the file. Nothing is ever deleted from this section.</span></span>
    
 
3. <span data-ttu-id="32060-161">Wenn sie nicht bereits vorhanden sind, fügen Sie der Datei die folgenden Elemente hinzu:</span><span class="sxs-lookup"><span data-stu-id="32060-161">If they are not already present, add the following elements to the file:</span></span> 
    
      - <span data-ttu-id="32060-p114">Ein untergeordnetes  [UpgradeActions](http://msdn.microsoft.com/library/5af24ac1-a290-454d-b32b-bc7f7a4634f0%28Office.15%29.aspx)-Element im Element **Feature**. Fügen Sie dem Element  *kein* **ReceiverAssembly**- oder **ReceiverClass**-Attribut hinzu. Diese haben bei der Aktualisierung eines SharePoint-Add-In s keine Funktion. (Die Attribute beziehen sich auf eine benutzerdefinierte Assembly, die in SharePoint-Add-Ins nicht unterstützt wird. Wenn Sie einem Add-In eine benutzerdefinierte Assembly hinzufügen, installiert SharePoint dieses Add-In nicht.)</span><span class="sxs-lookup"><span data-stu-id="32060-p114">An  [UpgradeActions](http://msdn.microsoft.com/library/5af24ac1-a290-454d-b32b-bc7f7a4634f0%28Office.15%29.aspx) child element in the **Feature** element. Do *not*  add **ReceiverAssembly** or **ReceiverClass** attributes to the element. These have no use when you are updating a SharePoint Add-in. (These attributes refer to a custom assembly, which is not supported in SharePoint Add-ins. If you include a custom assembly in an add-in, SharePoint will not install the add-in.)</span></span>
    
 
  - <span data-ttu-id="32060-p115">Ein untergeordnetes **VersionRange**-Element im **UpgradedActions**-Element. Fügen Sie dem Element kein **BeginVersion**- oder **EndVersion**-Attribut hinzu. Diese haben bei der ersten Aktualisierung eines Add-Ins keine Funktion. Ihre Verwendung wird im Abschnitt [Anschließende Aktualisierungen des Add-In-Webs](#SubsequentUpgrades) erläutert.</span><span class="sxs-lookup"><span data-stu-id="32060-p115">A **VersionRange** child element in the **UpgradedActions** element. Do not add **BeginVersion** or **EndVersion** attributes to the element. These serve no purpose when an add-in is being updated for the first time. Their use is discussed in the section [Subsequent updates of the add-in web](#SubsequentUpgrades).</span></span>
    
 
  - <span data-ttu-id="32060-171">Ein untergeordnetes [ApplyElementManifests](http://msdn.microsoft.com/library/c087a0c3-1e27-4034-b4da-e025991454d6%28Office.15%29.aspx)-Element im **VersionRange**-Element.</span><span class="sxs-lookup"><span data-stu-id="32060-171">An  [ApplyElementManifests](http://msdn.microsoft.com/library/c087a0c3-1e27-4034-b4da-e025991454d6%28Office.15%29.aspx) child element in the **VersionRange** element.</span></span>
    
 

    <span data-ttu-id="32060-172">An diesem Punkt sollte die Datei ähnlich wie das folgende Beispiel aussehen:</span><span class="sxs-lookup"><span data-stu-id="32060-172">At this point the file should resemble the following example.</span></span>
    
     <span data-ttu-id="32060-p116">**Wichtig** Die Office Developer Tools für Visual Studio haben möglicherweise bereits das obige Markup hinzugefügt und einige Elemente als Abbildung aus dem Abschnitt **ElementManifests** in den Abschnitt **ApplyElementManifests** kopiert. *Löschen Sie diese Elemente.* Auch wenn Sie einige dieser Elemente möglicherweise im Laufe der nächsten Schritte wieder einfügen müssen, ist es leichter und sicherer, mit einem leeren **ApplyElementManifests**-Abschnitt zu beginnen. Redundante Einträge für nicht geänderte Komponenten können negative Auswirkungen haben, z. B. kann der Updateprozess dadurch so viel Zeit in Anspruch nehmen, dass er eine Zeitüberschreitung verursacht und abgebrochen wird.</span><span class="sxs-lookup"><span data-stu-id="32060-p116">**Important** The Office Developer Tools for Visual Studio may have already added the above markup and copied some elements from the **ElementManifests** section to the **ApplyElementManifests** section as an illustration. *Delete these.*  Although you may end up putting some of them back in later steps, it is easier and safer to start with an empty **ApplyElementManifests** section. Redundant entries for components that have not changed can have bad consequences, including possibly lengthening the update process enough that it times-out and fails.</span></span>



```XML
  <Feature <!-- Some attributes omitted --> 
               Version="2.0.0.0">
  <ElementManifests>
    <!-- ElementManifest elements omitted -->
  </ElementManifests>
  <UpgradeActions>
   <VersionRange>
     <ApplyElementManifests>
       
     </ApplyElementManifests>
   </VersionRange>
  </UpgradeActions>
</Feature>
```


### <a name="to-add-components-to-the-add-in"></a><span data-ttu-id="32060-177">So fügen Sie dem Add-In Komponenten hinzu</span><span class="sxs-lookup"><span data-stu-id="32060-177">To add components to the add-in</span></span>


1. <span data-ttu-id="32060-178">Gehen Sie beim Hinzufügen von neuen Komponenten zum Feature genauso vor wie beim Erstellen eines neuen SharePoint-Add-In-Projekts.</span><span class="sxs-lookup"><span data-stu-id="32060-178">Add any new components to the Feature exactly as you would if you were creating a new SharePoint Add-in project.</span></span>
    
 
2. <span data-ttu-id="32060-p117">Wenn Sie eine Komponente eines Typs hinzufügen, der in der vorherigen Version des Add-Ins nicht enthalten war, beispielsweise wenn Sie eine Liste zu einem Add-In hinzufügen, das zuvor keine Liste hatte, fügen die Office Developer Tools für Visual Studio dem Projekt eine Datei „elements.xml“ hinzu, die das Elementmanifest für die Komponente ist. Sie sollten die neue Versionsnummer des Add-Ins zu dieser Datei hinzufügen (z. B. „elements.2.0.0.0.xml“). Dies kann hilfreich bei der Problembehandlung sein. Achten Sie darauf, diese Änderung im **Projektmappen-Explorer** durchzuführen, um sicherzustellen, dass Verweise auf die Datei, beispielsweise in der CSPROJ-Datei und im Feature-XML-Code, entsprechend geändert werden.</span><span class="sxs-lookup"><span data-stu-id="32060-p117">When you add a component of a type that wasn't in the previous verison of the add-in, such as adding a list to an add-in that did not previously have a list, the Office Developer Tools for Visual Studio will add an elements.xml file to the project. This is the elements manifest for the component. You should add the new version number of the add-in to this file (for example, elements.2.0.0.0.xml). This can be helpful in troubleshooting. Be sure to make the change in **Solution Explorer** to ensure that references to the file, such as in the csproj file and the feature XML, are changed accordingly.</span></span>
    
 
3. <span data-ttu-id="32060-p118">Fügen Sie für jedes neue Elemente ein  [ElementManifest](http://msdn.microsoft.com/library/5a6a2865-5d31-45a2-a402-6da6e0f5567a%28Office.15%29.aspx)-Element als untergeordnetes Element der Elemente **ElementManifests** und **ApplyElementManifests** der Feature-XML-Datei hinzu (exakt dasselbe **ElementManifest**-Element an beiden Stellen). Das **Location**-Attribut des Elements sollte auf den relativen Pfad der elements.2.0.0.0.xml-Datei verweisen. Wenn Sie beispielsweise eine Liste namens MyCustomList hinzugefügt haben, würde das **ElementManifest**-Element wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="32060-p118">For each new element manifest, add an  [ElementManifest](http://msdn.microsoft.com/library/5a6a2865-5d31-45a2-a402-6da6e0f5567a%28Office.15%29.aspx) element as a child to both the **ElementManifests** and the **ApplyElementManifests** elements of the feature xml. (The exact same **ElementManifest** element in both places.) The **Location** attribute of the element should point to the relative path of the elements.2.0.0.0.xml file. For example, if you added a list named MyCustomList, the **ElementManifest** element would look like the following.</span></span>
    
```XML
  <ElementManifest Location="MyCustomList\elements.2.0.0.0.xml" />
```

4. <span data-ttu-id="32060-p119">Einige Arten von Komponenten fügen Dateien zu dem Projekt hinzu. Beispielsweise wird eine schema.xml-Datei erstellt, wenn Sie eine Liste hinzufügen, oder eine page-Datei, wenn Sie eine Seite hinzufügen. Fügen Sie für jede dieser Dateien ein  [ElementFile](http://msdn.microsoft.com/library/bd43638e-8f18-4a0d-b122-1c055f97aa71%28Office.15%29.aspx)-Element als untergeordnetes Element für das **ElementManifests**-Element hinzu. (Fügen Sie es nicht zum **ApplyElementManifests**-Element hinzu.) Das **Location**-Attribut sollte auf den relativen Pfad der Datei verweisen. Wenn Sie beispielsweise eine Liste hinzugefügt haben, würde das **ElementFile**-Element für die schema.xml-Datei wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="32060-p119">Some kinds of components add files to the project. For example, a schema.xml file is created when you add a list; and when you add a page, a page file is created. For each such file, add an  [ElementFile](http://msdn.microsoft.com/library/bd43638e-8f18-4a0d-b122-1c055f97aa71%28Office.15%29.aspx) element as a child to the **ElementManifests** element. (Do not add it to the **ApplyElementManifests** element.) The **Location** attribute should point to the relative path of the file. For example, if you added a list, the **ElementFile** element for the schema.xml would look like the following.</span></span>
    
```XML
  <ElementFile Location="MyCustomList\Schema.xml" />
```

5. <span data-ttu-id="32060-p120">Wenn Sie ein weiteres Element eines Typs hinzufügen, der bereits in der vorherigen Version des Add-Ins vorhanden war, fügen die Office Developer Tools für Visual Studio möglicherweise einen Verweis zu dem neuen Element zu einem vorhandenen Elementmanifest hinzu, statt ein neues zu erstellen. Die Standardmethode zum Hinzufügen einer Seite zu einem Add-In-Web besteht beispielsweise darin, im **Projektmappen-Explorer** mit der rechten Maustaste auf den Knoten **Seiten** zu klicken und dann zu **Hinzufügen | Neues Element | Seite | Hinzufügen** zu navigieren. Die Office Developer Tools für Visual Studio fügen ein neues **File**-Element zum **Pages**-Modul in der vorhandenen Elementmanifestdatei hinzu (die normalerweise den Namen „elements.xml“ hat), statt ein neues Elementmanifest zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="32060-p120">When you add another item of a type that was already in the previous version of the add-in, the Office Developer Tools for Visual Studio may add a reference to the new item to an existing elements manifest instead of creating a new one. For example, the standard way to add a page to an add-in web is to right-click the **Pages** node in **Solution Explorer** and then navigate through **Add | New Item | Page | Add**. The Office Developer Tools for Visual Studio will add a new **File** element to the **Pages** module in the existing elements manifest file (usually called elements.xml) rather than create a new element manifest.</span></span>
    
    <span data-ttu-id="32060-p121">Dies ist nicht wünschenswert. Die bewährte Methode besteht darin, das Bearbeiten vorhandener Elementmanifestdateien beim Aktualisieren eines Add-Ins möglichst zu vermeiden (d. h. von Elementmanifesten aus früheren Versionen des Add-Ins). Im Allgemeinen sollten neue Elemente in neuen Elementmanifestdateien platziert werden (auf die im **ApplyElementManifests**-Element des Feature-XML-Codes verwiesen wird). (Einige Ausnahmen zu dieser Vorgehensweise werden später beschrieben.) Gehen Sie beispielsweise wie folgt vor, um eine neue Seite hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="32060-p121">This is not desirable. The best practice is to avoid, when possible, editing any existing element manifest files when updating an add-in (that is, any element manifests from previous versions of the add-in). In general, new items should be in new element manifest files (which are themselves referenced in the **ApplyElementManifests** element of the Feature XML). (A few of exceptions to this practice are described later.) For example, to add a new page, take these steps:</span></span>
    
      1. <span data-ttu-id="32060-199">Erstellen Sie ein neues Modul mit dem Namen „Pages.2.0.0.0“.</span><span class="sxs-lookup"><span data-stu-id="32060-199">Create a new module named Pages.2.0.0.0</span></span>
    
 
  2. <span data-ttu-id="32060-200">Entfernen Sie die Datei „sample.txt", die automatisch von den Office-Entwicklertools für Visual Studio hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="32060-200">Remove the sample.txt file from it that theOffice Developer Tools for Visual Studio add automatically.</span></span>
    
 
  3. <span data-ttu-id="32060-201">Benennen Sie das Elementmanifest im neuen Modul in „elements.2.0.0.0.xml“ um.</span><span class="sxs-lookup"><span data-stu-id="32060-201">Rename the elements manifest in the new module to elements.2.0.0.0.xml.</span></span>
    
 
  4. <span data-ttu-id="32060-p122">Klicken Sie mit der rechten Maustaste auf das Modul **Pages.2.0.0.0**, und navigieren Sie dann zu **Hinzufügen | Neues Element | Seite | Hinzufügen**. Die neue Seite wird erstellt und im Elementmanifest für **Pages.2.0.0.0** anstelle von **Seiten** referenziert.</span><span class="sxs-lookup"><span data-stu-id="32060-p122">Right-click the **Pages.2.0.0.0** module and then navigate through **Add | New Item | Page | Add**. The new page is created and it is referenced in the elements manifest for **Pages.2.0.0.0** instead of **Pages**.</span></span>
    
 
  5. <span data-ttu-id="32060-204">Stellen Sie sicher, dass ein **ElementsFile**-Element für die neue Seite im **ElementManifests**-Element des Feature-XML-Codes vorhanden ist. Stellen Sie ebenso sicher, dass ein **ElementManifest**-Element für die elements.2.0.0.0.xml-Datei in den Abschnitten **ElementManifests** und **ApplyElementManifests** vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="32060-204">Ensure that there is an **ElementsFile** element for the new page in the **ElementManifests** element of the feature XML, and ensure that there is an **ElementManifest** element for the elements.2.0.0.0.xml file in both the **ElementManifests** and **ApplyElementManifests** sections.</span></span>
    
 

    <span data-ttu-id="32060-p123">Eine weitere Option in jeder Situation, in der die Office Developer Tools für Visual Studio ein vorhandenes Elementmanifest geändert haben, besteht darin, manuell eine neue elements.2.0.0.0.xml-Datei zu erstellen und das Markup, das dem alten Manifest hinzugefügt war, dem neuen hinzuzufügen. (Sie können das neue im selben Knoten im **Projektmappen-Explorer** ablegen wie das alte.)</span><span class="sxs-lookup"><span data-stu-id="32060-p123">Another option in any situation in which Office Developer Tools for Visual Studio has changed an existing elements manifest, is to manually create a new elements.2.0.0.0.xml and move the markup that was added to the old manifest to your new one. (You can put the new one in the same **Solution Explorer** node as the old one if you want.)</span></span>
    
 
6. <span data-ttu-id="32060-p124">Wenn Sie ein Feld zu einem Inhaltstyp im Feature hinzufügen, fügen Sie ein  [AddContentTypeField](http://msdn.microsoft.com/library/cb04a3ac-f41a-4ffe-aaa1-d4bf3fb6347d%28Office.15%29.aspx)-Element zum Abschnitt **VersionRange** hinzu. Achten Sie darauf, den Attributen **ContentTypeId** und **FieldId** die richtigen Werte zuzuweisen. Optional können Sie das Attribut **PushDown** verwenden, um festzulegen, ob ein neues Feld zu abgeleiteten Inhaltstypen hinzugefügt werden soll. Im Folgenden finden Sie ein Beispiel dafür.</span><span class="sxs-lookup"><span data-stu-id="32060-p124">If you add a field to a content type in the Feature, add an  [AddContentTypeField](http://msdn.microsoft.com/library/cb04a3ac-f41a-4ffe-aaa1-d4bf3fb6347d%28Office.15%29.aspx) element to the **VersionRange** section. Be sure to assign the correct values to the **ContentTypeId** and **FieldId** attributes. Optionally, use the **PushDown** attribute to specify whether the new field should be added to any derived content types. The following is an example.</span></span>
    
```XML
  <VersionRange>
  <AddContentTypeField 
    ContentTypeId="0x0101000728167cd9c94899925ba69c4af6743e"
    FieldId="{CCDD361F-A3FB-40D8-A272-3A3C858F4116}"
    PushDown="TRUE" />
  <!-- Other child elements of VersionRange -->
</VersionRange>
```


### <a name="to-modify-existing-components-of-the-add-in"></a><span data-ttu-id="32060-211">So ändern Sie vorhandene Komponenten des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="32060-211">To modify existing components of the add-in</span></span>


1. <span data-ttu-id="32060-p125">Wenn Sie eine Datei geändert haben, auf die in einer Elementmanifestdatei verwiesen wird, z. B. eine Datei „Default.aspx“, müssen Sie das **ElementFile**-Element für die Datei nicht ändern. Aber Sie müssen der Updateinfrastruktur anweisen, die alte Version der Datei durch die neue zu ersetzen. Dafür fügen Sie ein **ElementManifest**-Element für das Modul zum Abschnitt **ApplyElementManifests** hinzu. Da bereits ein solches Element im Abschnitt **ElementManifests** vorhanden ist, ist das einfache Kopieren (nicht Verschieben) in **ApplyElementManifests** manchmal eine Option, aber das ist nur empfehlenswert, wenn alle Dateien geändert wurden, auf die im Manifest verwiesen wird. Als allgemeine Vorgehensweise sollten Sie eine unveränderte Datei nicht durch eine Kopie der Datei ersetzen. In einigen Szenarios kann dies negative Auswirkungen haben. Wenn die Seite beispielsweise so konfiguriert wurde, dass sie von Benutzern angepasst werden kann, kann das Ersetzen dazu führen, dass die Anpassungen entfernt werden. (Wenn Sie die Seite geändert haben, müssten Sie diese Konsequenz akzeptieren, aber Sie sollten Ihren Benutzern diese Unannehmlichkeit nicht unnötigerweise auferlegen.)</span><span class="sxs-lookup"><span data-stu-id="32060-p125">If you have changed a file that is referenced in an elements manifest file, such as a Default.aspx file, you do not have to change the **ElementFile** element for the file at all. But you do have to tell the update infrastructure to replace the old version of the file with the new one. You do this by adding an **ElementManifest** element for the module to the **ApplyElementManifests** section. Since there is already such an element in the **ElementManifests** section, simply copying (not moving) it to the **ApplyElementManifests** is sometimes an option, but this is only advisable if every file that is referenced in the manifest has been changed. As a general practice, you shouldn't replace an unchanged file with a copy of itself. In some scenarios this can have bad effects. For example, if the page has been configured to allow users to customize it, replacing it can cause the customizations to be removed. (If you had changed the page, then you'd have to accept this consequence, but you don't want to impose this inconvenience on your customers pointlessly.)</span></span>
    
    <span data-ttu-id="32060-220">Um sicherzustellen, dass nur die geänderten Dateien im Modul ersetzt werden, erstellen Sie ein zweites Elementmanifest für das Modul, in dem nur auf die geänderten Dateien verwiesen wird, und wenden Sie das zweite Manifest in **ApplyElementManifests** an, indem Sie wie folgt vorgehen.</span><span class="sxs-lookup"><span data-stu-id="32060-220">To ensure that only the changed files in the module are replaced, create a second element manifest for the module that only references the changed files and apply the second manifest in the **ApplyElementManifests** by following these steps.</span></span>
    
      1. <span data-ttu-id="32060-221">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Knoten des Moduls, und fügen Sie eine XML-Datei (keine Seite) namens „elements.2.0.0.0.xml“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="32060-221">Right-click the module's node in **Solution Explorer** and add an XML file (not a page) named elements.2.0.0.0.xml.</span></span>
    
 
  2.  <span data-ttu-id="32060-p126">Wählen Sie die neue Datei im **Projektmappen-Explorer** aus, um ihren Eigenschaftsbereich anzuzeigen, und ändern Sie die Eigenschaft **Deployment Type** in **ElementManifest**. Das ist wichtig, um sicherzustellen, dass die Office-Entwicklertools für Visual Studio die Datei ordnungsgemäß verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="32060-p126">Select the new file in **Solution Explorer** to make its property pane visible and change the **Deployment Type** property to **ElementManifest**. This is important to ensure that the Office Developer Tools for Visual Studio handle the file properly.</span></span>
    
 
  3. <span data-ttu-id="32060-224">Kopieren Sie die Inhalte des ursprünglichen Manifests in das neue Manifest, und löschen Sie dann im neuen Manifest alle  [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx)-Elemente, die **nicht** geänderten Dateien entsprechen.</span><span class="sxs-lookup"><span data-stu-id="32060-224">Copy the contents of the original manifest to the new one, and then delete from the new manifest all the  [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx) elements that correspond to files that have **not** changed.</span></span>
    
 
  4. <span data-ttu-id="32060-225">Fügen Sie ein **ElementManifest**-Element zum Abschnitt **ApplyElementManifests** hinzu, in dem wie in diesem Beispiel auf die neue Manifestdatei verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="32060-225">Add an **ElementManifest** element to the **ApplyElementManifests** section that references the new manifest file such as in this example.</span></span>
    
```XML
  <ElementManifest Location="Pages\elements.2.0.0.0.xml" />
```


     **Note**   Do not delete the original manifest. The Feature XML is using both of the old and new ones. Do not copy any **ElementFile** elements from the **ElementManifests** section to the **ApplyElementManifests** section even if the file that is referenced in the **ElementFile** has been changed.
2. <span data-ttu-id="32060-p127">Öffnen Sie jede Elementmanifestdatei, auf die im Abschnitt **ApplyElementManifests** verwiesen wird, und stellen Sie sicher, dass alle [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx)-Elemente über ein **ReplaceContents**-Attribut verfügen und dies auf **TRUE** festgelegt ist. Nachfolgend sehen Sie ein Beispiel. Die Office Developer Tools für Visual Studio haben dies möglicherweise bereits durchgeführt, aber Sie sollten es überprüfen, auch für die Elementemanifeste aus früheren Versionen des Add-Ins. Dies ist eine der Situationen, in denen es eine bewährte Vorgehensweise ist, eine vorhandene Elementmanifestdatei zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="32060-p127">Open every element manifest file that is referenced in the **ApplyElementManifests** section and ensure that any [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx) elements have a **ReplaceContents** attribute and that it is set to **TRUE**. The following is an example. The Office Developer Tools for Visual Studio may have done this already, but you should verify it. Do this even for the element manifests from previous versions of the add-in. This is one of the few ways in which it is a good practice to edit an existing element manifest file.</span></span>
    
```XML
  <Module Name="Pages">
  <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" />
</Module>
```

3. <span data-ttu-id="32060-p128">In Seiten können Webparts eingebettet werden, wie in [Einschließen eines Webparts auf einer Webseite im Add-In-Web](include-a-web-part-in-a-webpage-on-the-add-in-web) erläutert. Wenn Sie eine Seite mit einem Webpart ändern (oder die Eigenschaften des Webparts ändern), ist ein zusätzlicher Schritt erforderlich: Sie müssen das folgende Markup zur Seite hinzufügen, um zu verhindern, dass SharePoint eine zweite Kopie des Webparts auf der Seite hinzufügt. Das Markup sollte zum **asp:Content**-Element mit der ID `PlaceHolderAdditionalPageHead` hinzugefügt werden. (Die Office Developer Tools für Visual Studio haben es möglicherweise beim ersten Erstellen der Seite bereits hinzugefügt, aber Sie sollten überprüfen, ob es vorhanden ist.)</span><span class="sxs-lookup"><span data-stu-id="32060-p128">Pages can have Web Parts embedded in them as explained in  [Include a Web Part in a webpage on the add-in web](include-a-web-part-in-a-webpage-on-the-add-in-web). If you change a page that has a Web Part on it (or change the properties of the Web Part), then there is an additional step: you have to add the following markup to the page to prevent the SharePoint from adding a second copy of the Web Part onto the page. The markup should be added to the **asp:Content** element with the ID `PlaceHolderAdditionalPageHead`. (The Office Developer Tools for Visual Studio may have already added it when the page was first created, but you should verify that it is there.)</span></span>
    
```XML
  <meta name="WebPartPageExpansion" content="full" />
```


     **Note**   If the page was configured to allow users to customize it, then this markup has the side effect of removing those customizations. Users will have to repeat them. If the Web Part was added to the page following the guidance in [Include a Web Part in a webpage on the add-in web](include-a-web-part-in-a-webpage-on-the-add-in-web), then the Web Part markup is in the elements manifest, so changing the Web Part's properties is an exception to the general rule that you should not edit an element manifest file as part of an add-in update. 
4. <span data-ttu-id="32060-235">Anstatt eine Seite zu ändern, können Sie alternativ auch eine Umleitung zu einer neuen Seite vornehmen; führen Sie hierfür die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="32060-235">As an alternative to changing a page, you also have the option of using redirection to a new page using the following steps.</span></span> 
    
      1. <span data-ttu-id="32060-236">Erstellen Sie die neue Seite, und konfigurieren Sie das Updatemarkup wie weiter oben im Verfahren **So fügen Sie dem Add-In Komponenten hinzu** beschrieben.</span><span class="sxs-lookup"><span data-stu-id="32060-236">Create the new page and configure its update markup as described in the procedure **To add components to the add-in** above.</span></span>
    
 
  2. <span data-ttu-id="32060-237">Öffnen Sie die alte Seite, und entfernen Sie alle Markups aus dem **asp:Content**-Element mit der ID `PlaceHolderAdditionalPageHead`.</span><span class="sxs-lookup"><span data-stu-id="32060-237">Open the old page and remove all markup from the **asp:Content** element with the ID `PlaceHolderAdditionalPageHead`.</span></span> 
    
 
  3. <span data-ttu-id="32060-p129">Fügen Sie das folgende Markup zum **asp:Content**-Element hinzu, und ersetzen Sie dann _{RelativePathToNewPageFile}_ durch den neuen Pfad und Dateinamen. Dieses Skript leitet den Browser zur neuen Seite um und enthält die Abfrageparameter. Es sorgt außerdem dafür, dass die alte Seite nicht im Browserverlauf angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="32060-p129">Add the following markup to the **asp:Content** element, and then replace _{RelativePathToNewPageFile}_ with the new path and filename. This script will redirect the browser to the new page and include the query parameters. It will also keep the old page out of the browser history.</span></span>
    
```
  <script type="text/javascript">
        var queryString = window.location.search.substring(1);
        window.location.replace("{RelativePathToNewPageFile}" + "?" + queryString);
</script>
```

  4. <span data-ttu-id="32060-241">Löschen Sie alle anderen **asp:Content**-Elemente auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="32060-241">Delete any other **asp:Content** elements on the page.</span></span>
    
 
  5. <span data-ttu-id="32060-242">Wenn die Seite, die Sie ersetzen, die Startseite für das Add-In ist, ändern Sie das **StartPage**-Element im Add-In-Manifest so, dass es auf die neue Seite verweist.</span><span class="sxs-lookup"><span data-stu-id="32060-242">If the page you are replacing is the start page for the add-in, change the **StartPage** element in the add-in manifest to point to the new page.</span></span>
    
 
5. <span data-ttu-id="32060-p130">Wenn das Add-In-Web des Add-Ins ein **CustomAction**- oder ein **ClientWebPart**-Element enthält und Sie es im Rahmen eines Updates ändern, müssen Sie das Elementmanifest ändern, da diese Komponenten dort definiert sind. (Dies ist eine Ausnahme zur allgemeinen Vorgehensweise, dass ein Elementmanifest aus einer früheren Version des Add-Ins beim Aktualisieren des Add-Ins nicht geändert werden sollte.) Sie müssen außerdem das Element **ElementManifest** aus dem Abschnitt **ElementManifests** in den Abschnitt **ApplyElementManifests** kopieren (nicht verschieben).</span><span class="sxs-lookup"><span data-stu-id="32060-p130">If the add-in web of the add-in contains a **CustomAction** or a **ClientWebPart**, and you modify it as part of an update, then you must modify the element manifest since that is where these components are defined. (This is an exception to the general practice that you should not edit an element manifest from a previous version of the add-in when updating the add-in.) You also have to copy (not move) the **ElementManifest** element from the **ElementManifests** section to the **ApplyElementManifests** section.</span></span>
    
 

#### <a name="example-of-feature-xml-for-upgrading-an-add-in-the-first-time"></a><span data-ttu-id="32060-245">Feature-XML-Beispielcode für das erstmalige Upgrade eines Add-Ins</span><span class="sxs-lookup"><span data-stu-id="32060-245">Example of Feature XML for upgrading an add-in the first time</span></span>

<span data-ttu-id="32060-p131">Im Folgenden sehen Sie ein Beispiel für eine vollständige „_{FeatureName}_.Template.xml“-Datei beim erstmaligen Update eines Add-Ins. Das aktualisierte Add-In in diesem Beispiel beinhaltet eine geänderte „Default.aspx“-Datei, auf die in der Datei `Pages\Elements.xml` verwiesen wird, und sie stellt drei neue jQuery-Dateien bereit, auf die jeweils in der Datei `Scripts\Elements.xml` verwiesen wird. Beachten Sie, dass alle **ElementFile**s in den Abschnitt **ElementManifests** eingefügt werden und dass `<ElementManifest Location="Pages\Elements.xml" />` vom Abschnitt **ElementManifests** in den Abschnitt **ApplyElementManifests** kopiert (nicht verschoben) wurde.</span><span class="sxs-lookup"><span data-stu-id="32060-p131">The following is an example of a complete  _{FeatureName}_.Template.xml file for a first time update of an add-in. The updated add-in in this example includes a modified Default.aspx file that is referenced in the  `Pages\Elements.xml` file, and it deploys three new jQuery files, each of which is referenced in the `Scripts\Elements.xml` file. Note that all **ElementFile**s go in the **ElementManifests** section and note how `<ElementManifest Location="Pages\Elements.xml" />` has been copied (not moved) from the **ElementManifests** section to the **ApplyElementManifests** section.</span></span>
 

 

```XML
<Feature xmlns="http://schemas.microsoft.com/sharepoint/" Title="MyApp Feature1" 
      Description="SharePoint Add-in Feature" Id="85d309a8-107e-4a7d-b3a2-51341d3b11ff" 
      Scope="Web" Version="2.0.0.0">
  <ElementManifests>
    <ElementFile Location="Pages\Default.aspx" />
    <ElementManifest Location="Pages\Elements.xml" />
    <ElementFile Location="Content\App.css" />
    <ElementManifest Location="Content\Elements.xml" />
    <ElementFile Location="Images\AppIcon.png" />
    <ElementManifest Location="Images\Elements.xml" />
    <ElementFile Location="Scripts\jquery-3.0.0.intellisense.js" />
    <ElementFile Location="Scripts\jquery-3.0.0.js" />
    <ElementFile Location="Scripts\jquery-3.0.0.min.js" />
  </ElementManifests> 
  <UpgradeActions>
      <VersionRange>      
        <ApplyElementManifests>
          <ElementManifest Location="Pages\Elements.xml" />
          <ElementManifest Location="Scripts\elements.2.0.0.0.xml" />
        </ApplyElementManifests>
      </VersionRange>
  </UpgradeActions>
</Feature>

```


### <a name="subsequent-updates-of-the-add-in-web"></a><span data-ttu-id="32060-249">Anschließende Aktualisierungen des Add-In-Webs</span><span class="sxs-lookup"><span data-stu-id="32060-249">Subsequent updates of the add-in web</span></span>
<span data-ttu-id="32060-250"><a name="SubsequentUpgrades"> </a></span><span class="sxs-lookup"><span data-stu-id="32060-250"></span></span>

<span data-ttu-id="32060-p132">Wenn Sie ein SharePoint-Add-In zum zweiten (oder dritten usw.) Mal aktualisieren, müssen Sie berücksichtigen, dass einige Ihrer Kunden die vorherigen Aktualisierungen eventuell nicht vorgenommen haben. Wenn also ein Benutzer auf die Eingabeaufforderung „Aktualisierung ist verfügbar“ reagiert, nachdem Ihre letzte Aktualisierung im Add-In-Katalog der Organisation oder dem Office Store bereitgestellt wurde, wird seine Instanz des Add-Ins gegebenenfalls über mehrere Versionen des Add-Ins hinweg aktualisiert. Im Grunde ist dies genau das, was geschehen sollte: Jede frühere Version des Add-Ins soll auf die neueste Version aktualisiert werden. Allerdings soll nicht immer jede Aktualisierungsaktion für das Add-In-Web-Feature für jede Instanz des Add-Ins erneut durchgeführt werden. Manche Aktualisierungsaktionen sollten nicht mehrfach für eine Add-In-Instanz erfolgen. Wenn Sie beispielsweise bei einer Aktualisierung ein Feld zu einem Inhaltstyp hinzufügen, soll das Feld bei der nächsten Aktualisierung nicht erneut hinzugefügt werden. Das folgende Verfahren zeigt, wie Sie das **VersionRange**-Element verwenden, um ausgehend von der Version des zu aktualisierenden Features zu bestimmen, welche Aktualisierungsaktionen durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="32060-p132">When you update a SharePoint Add-in for the second (or third, and so on) time, you have to consider that some of your customers may not have made the previous updates. So if a user responds to the "update is available" prompt after your latest update is deployed to the organization's add-in catalog or to the Office Store, their instance of the add-in may be updated through multiple versions in a single update process. For the most part, this is exactly what should occur: you want every earlier version of the add-in updated to the latest version. But you do not always want every update action for the add-in web Feature to reoccur for every instance of the add-in. There are some update actions that should not occur multiple times on a given add-in instance. For example, if you add a field to a content type in one update, you do not want that field added again in the next update. The following procedure shows how to use the **VersionRange** element to control which update actions occur based on the version of the Feature that is being updated.</span></span>
 

 

### <a name="to-change-the-add-in-web-feature-on-later-updates"></a><span data-ttu-id="32060-258">So ändern Sie das Add-In-Web-Feature bei späteren Updates</span><span class="sxs-lookup"><span data-stu-id="32060-258">To change the add-in web Feature on later updates</span></span>


1. <span data-ttu-id="32060-p133">Öffnen Sie die Datei „_FeatureName_.Template.xml“ zur Bearbeitung, wie im Verfahren **So bearbeiten Sie den Feature-XML-Code** weiter oben in diesem Artikel beschrieben, und erhöhen Sie das Attribut **Version** des Elements [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx). Sie sollten für das Feature dieselbe Versionsnummer verwenden wie für das Add-In.</span><span class="sxs-lookup"><span data-stu-id="32060-p133">Open the  _FeatureName_.Template.xml file for editing as described in the procedure **To edit the Feature XML** earlier in this article, and increment the **Version** attribute of the [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx) element. You should use the same version number for the Feature as you used for the add-in.</span></span>
    
    <span data-ttu-id="32060-p134">Um unser Beispiel weiterzuführen, nehmen wir an, dass Sie das Add-In zuvor von Version 1.0.0.0 auf Version 2.0.0.0 aktualisiert haben und nun auf Version 3.0.0.0 aktualisieren. Legen Sie das Attribut **Version** also auf „3.0.0.0“ fest.</span><span class="sxs-lookup"><span data-stu-id="32060-p134">For purposes of a continuing example, let's suppose that you previously updated the add-in from version 1.0.0.0 to version 2.0.0.0, and now you are updating it to version 3.0.0.0. So set the **Version** attribute to 3.0.0.0.</span></span>
    
 
2. <span data-ttu-id="32060-p135">Fügen Sie ein neues **VersionRange**-Element unter allen vorhandenen **VersionRange**-Elementen hinzu. Fügen Sie diesem Element *kein***BeginVersion**- oder **EndVersion**-Attribut hinzu.</span><span class="sxs-lookup"><span data-stu-id="32060-p135">Add a new **VersionRange** element under all existing **VersionRange** elements. Do *not*  add a **BeginVersion** or **EndVersion** attribute to this element.</span></span>
    
 
3. <span data-ttu-id="32060-p136">Füllen Sie das **VersionRange**-Element wie im Verfahren unter **So aktualisieren Sie das Add-In-Web-Feature zum ersten Mal** weiter oben in diesem Artikel beschrieben aus, um die Änderungen an dieser aktualisierten Version des Features zu berücksichtigen. Wann immer in diesem Verfahren auf den Abschnitt **ApplyElementManifests** verwiesen wird, behandeln Sie dies als Verweis auf das **ApplyElementManifests**-Element, das ein untergeordnetes Element des **VersionRange**-Elements ist, das Sie soeben hinzugefügt haben, d. h. das *niedrigste* im Feature-XML-Code.</span><span class="sxs-lookup"><span data-stu-id="32060-p136">Populate the **VersionRange** element as described in the procedure **To update the add-in web Feature the first time** earlier in this article to account for the changes that you have made in this updated version of the Feature. Whenever that procedure refers to the **ApplyElementManifests** section, treat this as referring to the **ApplyElementManifests** element that is a child of the **VersionRange** element that you just added; that is, the *lowest*  one in the Feature XML file.</span></span>
    
 
4. <span data-ttu-id="32060-p137">Wechseln Sie zum vorherigen **VersionRange**-Element – demjenigen, das Sie bei der letzten Aktualisierung des Add-Ins (von 1.0.0.0 auf 2.0.0.0 in unserem fortgesetzten Beispiel) hinzugefügt haben – und fügen Sie ihm ein **EndVersion**-Attribut hinzu. Aktualisierungsaktionen im Bereich dieses **VersionRange**-Elements sollten auf alle Versionen des Add-Ins angewendet werden, auf die sie nicht schon angewendet wurden (Version 1.0.0.0), jedoch nicht auf Versionen, die bereits damit aktualisiert wurden (Version 2.0.0.0). Der **EndVersion**-Wert ist ein *ausschließender* Wert, daher legen Sie ihn auf die niedrigste Version fest, auf die die Aktualisierungsaktionen *nicht* angewendet werden sollen. In dem weitergeführten Beispiel setzen Sie ihn auf 2.0.0.0. Ihre Datei sollte nun wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="32060-p137">Go to the previous **VersionRange** element—the one you added the last time you updated the add-in (from 1.0.0.0 to 2.0.0.0 in the continuing example)—and add an **EndVersion** attribute to it. You want the upgrade actions in this **VersionRange** to be applied to any versions of the add-in to which they haven't already been applied (version 1.0.0.0), but you don't want them to be reapplied to versions to which they were already applied (version 2.0.0.0). The **EndVersion** value is *exclusive*  , so you set it to the lowest version to which you do *not*  want the upgrade actions applied. In the continuing example, you set it to 2.0.0.0. Your file should now resemble the following.</span></span>
    
```XML
  <Feature <!-- Some attributes omitted --> 
               Version="3.0.0.0">
  <ElementManifests>
    <!-- ElementManifest elements omitted -->
  </ElementManifests>
  <UpgradeActions>
    <VersionRange EndVersion="2.0.0.0">
      <!--  Child elements for upgrade from 1.0.0.0 to 2.0.0.0 go here. -->
    </VersionRange>
   <VersionRange>
      <!--  Child elements for upgrade from 2.0.0.0 to 3.0.0.0 go here. -->
   </VersionRange>
  </UpgradeActions>
</Feature>
```


    Each time that you upgrade the Feature, follow the same pattern. Add a new  **VersionRange** for the latest update actions. Then add an **EndVersion** element to the *previous*  **VersionRange** element and set it to the previous version number. In the continuing example, the file would resemble the following for the update from 3.0.0.0 to 4.0.0.0.
    


```XML
  <Feature <!-- Some attributes omitted --> 
               Version="4.0.0.0">
  <ElementManifests>
    <!-- Child elements omitted -->
  </ElementManifests>
  <UpgradeActions>
    <VersionRange EndVersion="2.0.0.0">
       <!-- Child elements for upgrade from 1.0.0.0 to 2.0.0.0 go here. -->
    </VersionRange>
    <VersionRange EndVersion="3.0.0.0">
       <!-- Child elements for upgrade from 2.0.0.0 to 3.0.0.0 go here. -->
    </VersionRange>
    <VersionRange>
       <!-- Child elements for upgrade from 3.0.0.0 to 4.0.0.0 go here. -->
    </VersionRange>
  </UpgradeActions>
</Feature>
```


    Notice that the most recent  **VersionRange** element has no **BeginVersion** or **EndVersion** attributes. This ensures that the upgrade actions that go into this **VersionRange** element are applied to all previous versions of the Feature, which is what you want because all the latest changes are referenced in this **VersionRange**, and none of them have already occurred for any instance of the Feature.
    
    Notice also that the  **BeginVersion** attribute is not used in any of the **VersionRange**s. This is because the default value for the  **BeginVersion** attribute is 0.0.0.0, and that is the value that you want because you want all upgrade actions applied to every instance of the add-in that is earlier than the version that is specified in the **EndVersion** attribute.
    
     **Important**   The **VersionRange** element determines only which versions of the Feature the upgrades are applied to. It does not determine which versions of the add-in get a notification that an update is available???the notification is triggered only by the add-in version number. Within 24 hours of a new version of the add-in being available in the organization's add-in catalog or the Office Store, every installed instance of the add-in, regardless of version, has the notification that an update is available appear on its tile in the **Site Contents** page. The **VersionRange** does not affect the new version number of the newly upgraded Feature or the newly updated add-in. Those two numbers are always changed to the latest version number, regardless of what version range the Feature was in before the upgrade. This provides another good reason to avoid using a **BeginVersion** attribute. The **BeginVersion** attribute can be used to block some upgrade actions from ever occurring on some add-in instances. But it cannot block the Feature or add-in versions from being raised to the latest version. So the use of a **BeginVersion** attribute could create a situation in which two instances of your add-in could have the same add-in version number and the same add-in web Feature version number, but have different components in their add-in webs.

## <a name="verify-deployment-of-add-in-web-components"></a><span data-ttu-id="32060-272">Überprüfen der Bereitstellung von Add-In-Webkomponenten</span><span class="sxs-lookup"><span data-stu-id="32060-272">Verify deployment of add-in web components</span></span>
<span data-ttu-id="32060-273"><a name="VerifyDeployAppWebComp"> </a></span><span class="sxs-lookup"><span data-stu-id="32060-273"></span></span>

<span data-ttu-id="32060-274">Führen Sie die folgenden Schritte aus, um die Bereitstellung des Add-In-Web-Features und seiner Komponenten zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="32060-274">Follow these steps to verify the deployment of the add-in web Feature and its components.</span></span>
 

 

### <a name="to-verify-the-provisioning-of-the-add-in-web"></a><span data-ttu-id="32060-275">So überprüfen Sie die Bereitstellung des Add-In-Webs</span><span class="sxs-lookup"><span data-stu-id="32060-275">To verify the provisioning of the add-in web</span></span>


1. <span data-ttu-id="32060-p138">Öffnen Sie die Seite **Websiteeinstellungen** des Hostwebs. Klicken Sie im Abschnitt **Websitesammlungsverwaltung** auf den Link **Websitehierarchie**.</span><span class="sxs-lookup"><span data-stu-id="32060-p138">Open the **Site Settings** page of the host web. In the **Site Collection Administration** section, choose the **Site hierarchy** link.</span></span>
    
 
2. <span data-ttu-id="32060-p139">Auf der Seite **Websitehierarchie** wird das Add-In-Web nach URL aufgeführt. Starten Sie es nicht. Kopieren Sie stattdessen die URL, und verwenden Sie diese in den übrigen Schritten.</span><span class="sxs-lookup"><span data-stu-id="32060-p139">On the **Site Hierarchy** page, you see your add-in web listed by its URL. Do not start it. Instead, copy the URL, and use the URL in the remaining steps.</span></span>
    
 
3. <span data-ttu-id="32060-281">Navigieren Sie zu „_URL_des_Add-In-Webs_/_layouts/15/ManageFeatures.aspx“, und überprüfen Sie auf der daraufhin geöffneten Seite **Websitefeatures**, ob das Feature ein Mitglied der alphabetischen Liste von Features und der Status **Aktiv** ist.</span><span class="sxs-lookup"><span data-stu-id="32060-281">Navigate to  _URL_of_app_web_/_layouts/15/ManageFeatures.aspx and, on the **Site Features** page that opens, verify that the Feature is a member of the alphabetical list of Features and that its status is **Active**.</span></span> 
    
 
4. <span data-ttu-id="32060-282">Wenn Ihr Add-In-Web-Feature benutzerdefinierte Websitespalten enthält, öffnen Sie „_URL_des_Add-In-Webs_/_layouts/15/mngfield.aspx“, und prüfen Sie auf der sich öffnenden Seite **Websitespalten**, ob Ihre neuen benutzerdefinierten Websitespalten aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="32060-282">If your add-in web Feature includes custom site columns, open  _URL_of_app_web_/_layouts/15/mngfield.aspx and, on the **Site Columns** page that opens, verify that your new custom site columns are listed.</span></span>
    
 
5. <span data-ttu-id="32060-283">Wenn Ihr Add-In-Web-Feature benutzerdefinierte Inhaltstypen enthält, öffnen Sie „_URL_des_Add-In-Webs_/_layouts/15/mngctype.aspx“, und prüfen Sie auf der sich öffnenden Seite **Websiteinhaltstypen**, ob Ihre neuen Inhaltstypen aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="32060-283">If your add-in web Feature includes any custom content types, open  _URL_of_app_web_/_layouts/15/mngctype.aspx and, on the **Site Content Types** page that opens, verify that your new content types are listed.</span></span>
    
 
6. <span data-ttu-id="32060-p140">Wählen Sie für jeden benutzerdefinierten Inhaltstyp und jeden Inhaltstyp, zu dem Sie eine Spalte hinzugefügt haben, den Link zu dem Inhaltstyp. Überprüfen Sie auf der sich öffnenden Seite **Websiteinhaltstyp**, ob der Inhaltstyp über die richtigen Websitespalten verfügt.</span><span class="sxs-lookup"><span data-stu-id="32060-p140">For each custom content type, and each content type to which you have added a column, choose the link to the content type. On the **Site Content Type** page that opens, verify that the content type has the site columns it should have.</span></span>
    
 
7. <span data-ttu-id="32060-286">Wenn Ihr Add-In-Web-Feature Listeninstanzen enthält, öffnen Sie „_URL_des_Add-In-Webs_/_layouts/15/mcontent.aspx“, und überprüfen Sie auf der sich öffnenden Seite **Websitebibliotheken und -listen**, ob für jede benutzerdefinierte Listeninstanz ein Link zu **„Name_der_Liste“ anpassen** vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="32060-286">If your add-in web Feature includes any list instances, open  _URL_of_app_web_/_layouts/15/mcontent.aspx and, on the **Site Libraries and Lists** page that opens, verify that there is a **Customize "name_of_list"** link for each custom list instance.</span></span>
    
 
8. <span data-ttu-id="32060-287">Klicken Sie bei jeder dieser benutzerdefinierten Listeninstanzen auf den Link **„Name_der_Liste“ anpassen**, und überprüfen Sie auf der Seite „Listeneinstellungen“, ob die Liste über die richtigen Inhaltstypen und -spalten verfügt.</span><span class="sxs-lookup"><span data-stu-id="32060-287">For each of these custom list instances, choose the **Customize "name_of_list "** link, and verify on the list settings page that the list has the expected content types and columns.</span></span>
    
     <span data-ttu-id="32060-p141">**Hinweis** Wenn es auf der Seite keinen Abschnitt **Inhaltstypen** gibt, müssen Sie die Verwaltung der Inhaltstypen aktivieren. Klicken Sie auf den Link **Erweiterte Einstellungen**, aktivieren Sie auf der Seite „Erweiterte Einstellungen“ die Verwaltung der Inhaltstypen, und klicken Sie anschließend auf **OK**. Sie werden dann wieder auf die vorherige Seite weitergeleitet, die jetzt einen Abschnitt mit einer Liste von **Inhaltstypen** enthält.</span><span class="sxs-lookup"><span data-stu-id="32060-p141">**Note** If there is no **Content Types** section on the page, you must enable management of content types. Choose the **Advanced Settings** link and, on the Advanced Settings page, enable management of content types, and then choose **OK**. You are returned to the previous page, and there is now a list of **Content Types** section.</span></span>
9. <span data-ttu-id="32060-p142">Am oberen Rand der Seite befindet sich die **Webadresse** der Liste. Wenn Sie Beispielelemente zu Ihrer Listeninstanzdefinition hinzugefügt haben, kopieren Sie die Adresse, fügen Sie diese in die Adressleiste Ihres Browsers ein, und navigieren Sie dann zu der Liste. Überprüfen Sie, ob in der Liste die von Ihnen erstellten Beispielelemente enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="32060-p142">Near the top of the page is the **web address** of the list. If you included sample items in your list instance definition, copy the address and paste it into the address bar of your browser, and then navigate to the list. Verify that the list has the sample items that you created.</span></span>
    
 

## <a name="next-steps"></a><span data-ttu-id="32060-294">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="32060-294">Next steps</span></span>
<span data-ttu-id="32060-295"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="32060-295"></span></span>

<span data-ttu-id="32060-296">Kehren Sie zu  [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="32060-296">Return to  [Major steps in updating an add-in](update-sharepoint-add-ins#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>
 

 

-  [<span data-ttu-id="32060-297">Aktualisieren von Hostwebkomponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="32060-297">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="32060-298">Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="32060-298">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="32060-299">Aktualisieren von Remotekomponenten in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="32060-299">Update remote components in SharePoint Add-ins</span></span>](update-remote-components-in-sharepoint-add-ins)
    
 

## <a name="additional-resources"></a><span data-ttu-id="32060-300">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="32060-300">Additional resources</span></span>
<span data-ttu-id="32060-301"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="32060-301"></span></span>


-  [<span data-ttu-id="32060-302">Aktualisieren von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="32060-302">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins)
    
 
-  <span data-ttu-id="32060-303">[Vorgehensweise: Hinzufügen von Elementen zu einem vorhandenen Feature](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) im Microsoft SharePoint 2010-Software Development Kit (SDK).</span><span class="sxs-lookup"><span data-stu-id="32060-303">[How to: Add Elements to an Existing Feature](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) in the Microsoft SharePoint 2010 Software Development Kit (SDK).</span></span>
    
 
-  <span data-ttu-id="32060-304">[Aktualisieren von Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) im Microsoft SharePoint 2010-Software Development Kit (SDK).</span><span class="sxs-lookup"><span data-stu-id="32060-304">[Upgrading Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) in the Microsoft SharePoint 2010 Software Development Kit (SDK).</span></span>
    
 

