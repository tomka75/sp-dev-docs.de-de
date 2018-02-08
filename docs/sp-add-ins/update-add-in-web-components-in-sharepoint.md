---
title: Aktualisieren von SharePoint-Add-In-Webkomponenten
description: Aktualisieren von Seiten, Listen, Inhaltstypen und anderen Webkomponenten in einem SharePoint-Add-In.
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 19692bcf7cea9d077b5eeaa9a78097f365207b0b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="update-add-in-web-components-in-sharepoint"></a>Aktualisieren von SharePoint-Webkomponenten

Voraussetzungen für die Aktualisierung der Add-In-Webkomponenten:

- Kenntnisse des Themas [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md) und der darin aufgeführten erforderlichen Komponenten und Kernkonzepte.

- Sie haben die neueste Version des Add-Ins entwickelt und getestet, wie unter [Erstellen und Debuggen Sie die neue Version, als ob es ein ganz neues Add-In wäre](update-sharepoint-add-ins.md#DebugFirst) beschrieben.

<a name="UpdatingAppWeb"> </a>
## <a name="update-sharepoint-components-in-the-add-in-web"></a>Aktualisieren von SharePoint-Komponenten im Add-In-Web

Alle SharePoint-Komponenten, die im Add-In-Web bereitgestellt werden, sind in **Web**bereichs-Features im Add-In-Paket enthalten. Aus diesem Grund werden beim Aktualisieren dieser Komponenten eine oder mehrere Features aktualisiert. Dieser Prozess hat sich seit SharePoint 2010 nicht geändert und ist im SharePoint 2010 SDK unter [Hinzufügen von Elementen zu einem vorhandenen Feature](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) dokumentiert. 

Möglicherweise sind auch andere Artikel im Knoten [Aktualisieren von Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) hilfreich, bedenken Sie jedoch, dass Add-Ins keinen benutzerdefinierten Code auf dem SharePoint-Server enthalten dürfen, einige Aspekte des Aktualisierens von Features in SharePoint 2010 sind daher für das Aktualisieren von Add-Ins nicht relevant. Sie können beispielsweise das Element [CustomUpgradeAction](http://msdn.microsoft.com/library/16a2182e-80aa-4184-8071-8f717ee5c572%28Office.15%29.aspx) nicht beim Aktualisieren des Features eines SharePoint-Add-Ins verwenden.

### <a name="what-can-and-cannot-be-done-declaratively"></a>Welche Aufgaben deklarativ ausgeführt werden können und welche nicht

Bei einem auf SharePoint gehosteten Add-In können Sie nur XML-Markup zum Aktualisieren eines Add-Ins verwenden, und es gibt einige Einschränkungen dahingehend, wie Sie ein Add-In in einem Update deklarativ ändern können. Bei einem von einem Anbieter gehosteten Add-In können Sie einen [UpdatedEventEndpoint-Handler](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md) für alle Vorgänge implementieren, die nicht deklarativ ausgeführt werden können. 

Das Hinzufügen von Komponenten zu einem Add-In ist einfach. Alle Komponenten, die in ein Add-In eingeschlossen werden können, können auch zu einem Update hinzugefügt werden (weitere Informationen finden Sie unter [Typen von SharePoint-Komponenten in einem SharePoint-Add-In](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps)). Wenn Sie jedoch eine vorhandene Komponente deklarativ ändern möchten, müssen Sie die folgenden Punkte berücksichtigen. 

- Die Datentypen einer Liste oder eines Inhaltstypfelds (Spalte) können nach der anfänglichen Bereitstellung unter keinen Umständen geändert werden. Ändern Sie insbesondere nicht den Datentyp eines Felds als Teil eines Add-In-Updates (*nicht einmal programmgesteuert*). Alternativ können Sie ein neues Feld hinzufügen. Wenn das Add-In benutzerdefinierte Formulare zum Erstellen, Bearbeiten oder Anzeigen enthält, müssen Sie in diesen Formularen entsprechende Änderungen vornehmen. Fügen Sie beispielsweise eine Benutzeroberfläche für das neue Feld hinzu, und entfernen Sie die Benutzeroberfläche für das alte Feld. (Bei einem von einem Anbieter gehosteten Add-In können Sie Daten programmgesteuert aus dem alten Feld in das neue verschieben und dann das alte Feld löschen.)

- Listen, Listeninstanzen, Inhaltstypen oder Felder können im Updatemarkup nicht gelöscht werden.

- Dateien können nicht aus dem Add-In-Web im Updatemarkup gelöscht werden. Allerdings können Sie den Inhalt einer Datei ändern.

- Die Elemente **CustomUpgradeAction** und **MapFile** können beim Aktualisieren eines SharePoint-Add-In s nicht verwendet werden, auch wenn sie in Visual Studio-IntelliSense verfügbar zu sein scheinen.

### <a name="update-the-add-in-web-for-the-first-time"></a>Erstmaliges Aktualisieren des Add-In-Webs

Die Verfahren in diesem Abschnitt zeigen, wie Sie Inhaltstypen, Listen, Dateien und andere SharePoint-Komponenten im Add-In-Web hinzufügen oder aktualisieren. Der Einfachheit halber wird davon ausgegangen, dass alle Komponenten Teil eines einzigen Features im Add-In-Web sind, Add-In-Webs können jedoch mehrere Funktionen aufweisen, und Sie können mehrere Features im selben Update aktualisieren.

Die Microsoft Office-Entwicklertools für Visual Studio sind für das Erstellen neuer Add-Ins gedacht, und das Standardverhalten der Tools ist beim Aktualisieren eines Add-Ins nicht immer optimal. Um mehr Kontrolle über den Prozess zu erlangen, sollten Sie damit beginnen, den Feature-Designer zu deaktivieren, indem Sie die folgenden Schritte ausführen, um den unformatierten Feature-XML-Code direkt zu bearbeiten. 

#### <a name="to-edit-the-feature-xml"></a>So bearbeiten Sie den Feature-XML-Code

1. Öffnen Sie im **Projektmappen-Explorer** die Datei _{FeatureName}_.features. Sie wird im Feature-Designer geöffnet.

2. Öffnen Sie die Registerkarte **Manifest** und erweitern Sie dann **Bearbeitungsoptionen**.

3. Wählen Sie **Generierten XML-Code überschreiben und Manifest im XML-Editor bearbeiten** aus.

4. Wählen Sie **Ja**, wenn Sie gefragt werden, ob Sie den Designer deaktivieren möchten.

5. Wählen Sie in der Ansicht, die daraufhin geöffnet wird, die Option  **Manifest im XML-Editor bearbeiten** aus. Die Datei _{FeatureName}_.Template.xml wird geöffnet. 

*Abbildung 1: Öffnen des Feature-XML-Editors*

![Schritte zum Öffnen des Feature-XML-Editors](../images/UpdateAppOpenFeatureXML.png)

> [!CAUTION]
> Fügen Sie keine `"<!-- -->"`-Kommentare zur Datei _{FeatureName}_.features hinzu. Kommentare werden von der Upgradeinfrastruktur nicht unterstützt, und das Upgrade schlägt fehl, wenn sich Kommentare in der Datei befinden. Sie werden nur in Markupbeispielen dieses Artikels verwendet, um darauf hinzuweisen, wo das Markup platziert werden sollte.

#### <a name="to-update-the-add-in-web-feature-the-first-time"></a>So aktualisieren Sie das Add-In-Web-Feature zum ersten Mal

1. Erhöhen Sie das **Version**-Attribut des [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx)-Elements, wenn dies nicht bereits durch die Office-Entwicklertools für Visual Studio erfolgt ist, als Sie die Versionsnummer im Add-In-Manifest erhöht haben (die Tools führen diesen Schritt nicht in jedem Szenario aus, Sie müssen dies deshalb überprüfen). 

   Sie sollten dieselbe Versionsnummer wie auch für das Add-In verwenden. Sie sollten auch dann in Erwägung ziehen, die Feature-Version zu erhöhen, wenn andere Komponenten des Add-Ins aktualisiert werden, jedoch nicht das Add-In-Webfeature selbst. Die Logik des [VersionRange](http://msdn.microsoft.com/library/cd715e38-6ec3-43b2-8007-6d0ed8865d91%28Office.15%29.aspx)-Elements (die im Abschnitt [Anschließende Aktualisierungen des Add-In-Webs](#SubsequentUpgrades) erläutert wird) ist leichter zu verwalten, wenn die Add-In-Version und die Feature-Version immer gleich sind. 

2. Löschen Sie nichts im [ElementManifests](http://msdn.microsoft.com/library/d8d4db7e-2bc2-40c6-958b-d5683bdee87a%28Office.15%29.aspx)-Abschnitt der Datei. Aus diesem Abschnitt wird niemals etwas gelöscht.

3. Wenn sie nicht bereits vorhanden sind, fügen Sie der Datei die folgenden Elemente hinzu: 
    
   - Ein untergeordnetes [UpgradeActions](http://msdn.microsoft.com/library/5af24ac1-a290-454d-b32b-bc7f7a4634f0%28Office.15%29.aspx)-Element im **Feature**-Element. Fügen Sie diesem Element *kein* **ReceiverAssembly**- oder **ReceiverClass**-Attribut hinzu. Diese sind beim Aktualisieren eines SharePoint-Add-Ins nicht hilfreich. (Diese Attribute verweisen auf eine benutzerdefinierte Assembly, die in SharePoint-Add-Ins nicht unterstützt wird. Wenn Sie eine benutzerdefinierte Assembly in ein Add-In einschließen, installiert SharePoint das Add-In nicht.)

   - Ein untergeordnetes **VersionRange**-Element im Element **UpgradedActions**. Fügen Sie dem Element kein **BeginVersion**- oder **EndVersion**-Attribut hinzu. Diese haben bei der ersten Aktualisierung eines Add-Ins keine Funktion. Ihre Verwendung wird im Abschnitt  [Anschließende Aktualisierungen des Add-In-Webs](#SubsequentUpgrades) dargestellt.

   - Ein untergeordnetes [ApplyElementManifests](http://msdn.microsoft.com/library/c087a0c3-1e27-4034-b4da-e025991454d6%28Office.15%29.aspx)-Element im **VersionRange**-Element.

An diesem Punkt sollte die Datei ähnlich wie das folgende Beispiel aussehen:
    
> [!IMPORTANT]
> Die Office-Entwicklertools für Visual Studio haben das obige Markup möglicherweise bereits hinzugefügt und einige Elemente aus dem Abschnitt **ElementManifests** in den Abschnitt **ApplyElementManifests** kopiert. *Löschen Sie diese Elemente.* Vielleicht fügen Sie später wieder einige ein, aber es ist einfacher und sicherer, mit einem leeren **ApplyElementManifests**-Abschnitt zu beginnen. Redundante Einträge für Komponenten, die sich nicht geändert haben, können negative Auswirkungen haben, darunter zum Beispiel eine Verlängerung des Updateprozesses derart, dass eine Zeitüberschreitung auftritt und der Vorgang fehlschlägt.

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

#### <a name="to-add-components-to-the-add-in"></a>So fügen Sie dem Add-In Komponenten hinzu

1. Gehen Sie beim Hinzufügen von neuen Komponenten zum Feature genauso vor wie beim Erstellen eines neuen SharePoint-Add-In-Projekts.

2. Wenn Sie eine Komponente eines Typs hinzufügen, der in der vorherigen Version des Add-Ins nicht vorhanden war, z. B. das Hinzufügen einer List zu einem Add-In, das zuvor nicht über eine Liste verfügte, fügen die Office-Entwicklertools für Visual Studio eine elements.xml-Datei zu dem Projekt hinzu. Dies ist das Elementmanifest für die Komponente. Sie sollten die neue Versionsnummer des Add-Ins zu dieser Datei hinzufügen (z. B. „elements.2.0.0.0.xml“). Dies kann sehr hilfreich bei der Behandlung von Problemen sein. Nehmen Sie die Änderung im **Projektmappen-Explorer** vor, um sicherzustellen, dass Verweise auf die Datei, z. B. in der CSPROJ-Datei und dem im Feature-XML-Code, entsprechend geändert werden.

3. Fügen Sie für jedes neues Elementmanifest ein [ElementManifest](http://msdn.microsoft.com/library/5a6a2865-5d31-45a2-a402-6da6e0f5567a%28Office.15%29.aspx)-Element als untergeordnetes Element sowohl zu dem Element **ElementManifests** als auch zum Element **ApplyElementManifests** der Feature-XML hinzu (das genau gleiche **ElementManifest**-Element in beiden Stellen). Das **Location**-Attribut des Elements sollte auf den relativen Pfad der Datei „elements.2.0.0.0.xml“ zeigen. Wenn Sie beispielsweise eine Liste mit dem Namen „MyCustomList“ hinzugefügt haben, würde das **ElementManifest**-Element folgendermaßen aussehen: 
    
    ```XML
      <ElementManifest Location="MyCustomList\elements.2.0.0.0.xml" />
    ```

4. Manche Arten von Komponenten fügen Dateien zum Projekt hinzu. Beim Hinzufügen einer Liste wird beispielsweise eine schema.xml-Datei erstellt, beim Hinzufügen einer Seite wird eine page-Datei erstellt. Fügen Sie für jede solche Datei ein [ElementFile](http://msdn.microsoft.com/library/bd43638e-8f18-4a0d-b122-1c055f97aa71%28Office.15%29.aspx)-Element als untergeordnetes Element für das **ElementManifests**-Element hinzu (fügen Sie es nicht zum **ApplyElementManifests**-Element hinzu). Das **Location**-Attribut des Elements sollte auf den relativen Pfad der Datei zeigen. Wenn Sie beispielsweise eine Liste hinzugefügt haben, würde das **ElementFile**-Element für die Datei „schema.xml“ folgendermaßen aussehen: 
    
    ```XML
      <ElementFile Location="MyCustomList\Schema.xml" />
    ```

5. Wenn Sie ein anderes Element eines Typs hinzufügen, der bereits in der vorherigen Version des Add-Ins vorhanden war, kann von den Office-Entwicklertools für Visual Studio ein Verweis auf das neue Element zu einem vorhandenen Elementmanifest hinzugefügt werden, anstatt einen neuen zu erstellen. Um eine Seite zu einem Add-In-Web hinzuzufügen, würden Sie normalerweise mit der rechten Maustaste auf den Knoten **Pages** im **Projektmappen-Explorer** klicken und dann zu **Hinzufügen** > **Neues Element** > **Seite** > **Hinzufügen** gehen. Die Office-Entwicklertools für Visual Studio fügen ein neues **File**-Element zum **Pages**-Modul in der vorhandenen Elementmanifestdatei (die in der Regel den Namen „elements.xml“ trägt) hinzu anstatt ein neues Elementmanifest zu erstellen.
    
    Das ist nicht wünschenswert. Die bewährte Methode besteht darin, das Bearbeiten vorhandener Elementmanifestdateien beim Aktualisieren eines Add-Ins möglichst zu vermeiden (d. h. von Elementmanifesten aus früheren Versionen des Add-Ins). Im Allgemeinen sollten neue Elemente in neue Elementmanifestdateien platziert werden (auf die im **ApplyElementManifests**-Element der Feature-XML-Datei verwiesen wird). (Einige Ausnahmen zu dieser Vorgehensweise werden später beschrieben.) Gehen Sie beispielsweise wie folgt vor, um eine neue Seite hinzuzufügen:
    
   1. Erstellen Sie ein neues Modul mit dem Namen **Pages.2.0.0.0**.

   2. Entfernen Sie die Datei „sample.txt", die automatisch von den Office-Entwicklertools für Visual Studio hinzugefügt wurde.

   3. Benennen Sie das Elementmanifest im neuen Modul in **elements.2.0.0.0.xml** um.

   4. Klicken Sie mit der rechten Maustaste auf das Modul **Pages.2.0.0.0**, und gehen Sie dann zu **Hinzufügen** > **Neues Element** > **Seite** > **Hinzufügen**. Die neue Seite wird erstellt. Im Elementmanifest für **Pages.2.0.0.0** wird auf diese Seite und nicht auf **Pages** verwiesen.

   5. Stellen Sie sicher, dass ein **ElementsFile**-Element für die neue Seite im **ElementManifests**-Element der Feature-XML-Datei vorhanden ist. Stellen Sie ebenso sicher, dass ein **ElementManifest**-Element für die elements.2.0.0.0.xml-Datei in den Abschnitten **ElementManifests** und **ApplyElementManifests** vorhanden ist.
    
      Eine weitere Option in jeder Situation, in der die Office-Entwicklertools für Visual Studio ein vorhandenes Elementmanifest geändert haben, besteht darin, manuell eine neue elements.2.0.0.0.xml-Datei zu erstellen und das Markup, das dem alten Manifest hinzugefügt war, dem neuen hinzuzufügen. (Sie können das neue im selben Knoten im **Projektmappen-Explorer** ablegen wie das alte.)

6. Wenn Sie ein Feld zu einem Inhaltstyp im Feature hinzufügen, fügen Sie ein [AddContentTypeField](http://msdn.microsoft.com/library/cb04a3ac-f41a-4ffe-aaa1-d4bf3fb6347d%28Office.15%29.aspx)-Element zum **VersionRange**-Abschnitt hinzu. Weisen Sie den Attributen  **ContentTypeId** und **FieldId** unbedingt die korrekten Werte zu. Verwenden Sie optional das  **PushDown**-Attribut, um anzugeben, ob das neue Feld zu abgeleiteten Inhaltstypen hinzugefügt werden soll. Es folgt ein Beispiel.
    
    ```XML
     <VersionRange>
       <AddContentTypeField 
         ContentTypeId="0x0101000728167cd9c94899925ba69c4af6743e"
         FieldId="{CCDD361F-A3FB-40D8-A272-3A3C858F4116}"
         PushDown="TRUE" />
       <!-- Other child elements of VersionRange -->
     </VersionRange>
    ```

#### <a name="to-modify-existing-components-of-the-add-in"></a>So ändern Sie vorhandene Komponenten des Add-Ins

Wenn Sie eine Datei geändert habe, auf die in einer Elementmanifestdatei verwiesen wird, z. B. eine Default.aspx-Datei“, müssen Sie das **ElementFile**-Element für die Datei überhaupt nicht ändern. Sie müssen die Updateinfrastruktur jedoch anweisen, die alte Version der Datei durch die neue zu ersetzen. Dies erfolgt durch Hinzufügen eines **ElementManifest**-Elements für das Modul zum **ApplyElementManifests**-Abschnitt. 

Da bereits ein solches Element im **ElementManifests**-Abschnitt vorhanden ist, können Sie dieses einfach in **ApplyElementManifests** kopieren (nicht verschieben), dies ist jedoch nur ratsam, wenn jede Datei, auf die im Manifest verwiesen wird, geändert wurde. Allgemein empfiehlt es sich, eine unveränderte Datei nicht durch eine Kopie von sich selbst zu ersetzen. In manchen Szenarios kann dies negative Auswirkungen haben. Wenn die Seite beispielsweise so konfiguriert wurde, dass Benutzer diese anpassen können, kann es durch Ersetzen dieser Seite dazu kommen, dass die Anpassungen entfernt werden. (Wenn Sie die Seite geändert hätten, hätten Sie diese Konsequenz akzeptieren müssen, Sie möchten Ihren Kunden diese Unannehmlichkeit sicherlich ersparen.)
    
1. Um sicherzustellen, dass nur die geänderten Dateien im Modul ersetzt werden, erstellen Sie ein zweites Elementmanifest für das Modul, in dem nur auf die geänderten Dateien verwiesen wird, und wenden Sie das zweite Manifest in **ApplyElementManifests** an, indem Sie wie folgt vorgehen:
    
   1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Knoten des Moduls, und fügen Sie eine XML-Datei (keine Seite) namens **elements.2.0.0.0.xml** hinzu.

   2.  Wählen Sie die neue Datei im **Projektmappen-Explorer** aus, um ihren Eigenschaftsbereich anzuzeigen, und ändern Sie die Eigenschaft **Deployment Type** in **ElementManifest**. Das ist wichtig, um sicherzustellen, dass die Office-Entwicklertools für Visual Studio die Datei ordnungsgemäß verarbeiten.

   3. Kopieren Sie die Inhalte des ursprünglichen Manifests in das neue Manifest, und löschen Sie dann im neuen Manifest alle  [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx)-Elemente, die **nicht** geänderten Dateien entsprechen.

   4. Fügen Sie ein **ElementManifest**-Element zum Abschnitt **ApplyElementManifests** hinzu, in dem wie in diesem Beispiel auf die neue Manifestdatei verwiesen wird.
    
       ```XML
             <ElementManifest Location="Pages\elements.2.0.0.0.xml" />
       ```

      > [!NOTE]
      > Löschen Sie nicht das ursprüngliche Manifest. Der Feature-XML-Code verwendet sowohl das alte als auch das neue. Kopieren Sie keine **ElementFile**-Elemente aus dem Abschnitt **ElementManifests** in den Abschnitt **ApplyElementManifests**, selbst wenn sich die Datei, auf die in **ElementFile** verwiesen wird, geändert hat.
      
2. Öffnen Sie jede Elementmanifestdatei, auf die im Abschnitt **ApplyElementManifests** verwiesen wird, und stellen Sie sicher, dass alle [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx)-Elemente über ein **ReplaceContents**-Attribut verfügen, das auf **TRUE** festgelegt ist. 

   Es folgt ein Beispiel. Die Office-Entwicklertools für Visual Studio haben dies möglicherweise bereits ausgeführt, Sie müssen dies jedoch überprüfen. Führen Sie dies auch für die Elementmanifeste aus den früheren Versionen des Add-Ins aus. Dies ist eine der wenigen Möglichkeiten, bei denen es ratsam ist, eine vorhandene Elementmanifestdatei zu bearbeiten.
    
    ```XML
     <Module Name="Pages">
       <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" />
     </Module>
    ```

3. Seiten können eingebettete Webparts aufweisen, wie in [Einschließen eines Webparts auf einer Webseite im Add-In-Web](include-a-web-part-in-a-webpage-on-the-add-in-web.md) erläutert. Wenn Sie eine Seite mit einem Webpart ändern (oder die Eigenschaften des Webparts ändern), gibt es einen zusätzlichen Schritt: Sie müssen das folgende Markup zu der Seite hinzufügen, um zu verhindern, dass SharePoint eine zweite Kopie des Webparts zu der Seite hinzufügt. Das Markup sollte zu dem **asp:Content**-Element mit der ID `PlaceHolderAdditionalPageHead` hinzugefügt werden. (Dieses wurde von den Office-Entwicklertools für Visual Studio möglicherweise bereits hinzugefügt, als die Seite zum ersten Mal erstellt wurde, Sie sollten jedoch überprüfen, ob es vorhanden ist.)
    
    ```XML
      <meta name="WebPartPageExpansion" content="full" />
    ```

   > [!NOTE]
   > Wenn die Seite so konfiguriert wurde, dass Benutzer sie anpassen können, hat dieses Markup den Nebeneffekt, dass diese Anpassungen entfernt werden. Benutzer müssen die Anpassungen wiederholen. Wenn das Webpart mithilfe der Anweisungen unter [Einschließen eines Webparts auf einer Webseite im Add-In-Web](include-a-web-part-in-a-webpage-on-the-add-in-web.md) hinzugefügt wurde, befindet sich das Webpartmarkup im Elementmanifest. Das Ändern der Eigenschaften des Webparts ist also eine Ausnahme zu der allgemeinen Regeln, dass eine Elementmanifestdatei nicht als Teil eines Add-In-Updates bearbeitet werden sollte. 

4. Anstatt eine Seite zu ändern, können Sie alternativ auch eine Umleitung zu einer neuen Seite vornehmen; führen Sie hierfür die folgenden Schritte aus: 
    
   1. Erstellen Sie die neue Seite, und konfigurieren Sie das Updatemarkup wie weiter oben im Verfahren **So fügen Sie dem Add-In Komponenten hinzu** beschrieben.

   2. Öffnen Sie die alte Seite, und entfernen Sie alle Markups aus dem **asp:Content**-Element mit der ID  `PlaceHolderAdditionalPageHead`. 

   3. Fügen Sie das folgende Markup zu dem **asp:Content**-Element hinzu, und ersetzen Sie dann _{RelativePathToNewPageFile}_ durch den neuen Pfad und Dateinamen. Das Skript leitet den Browser auf die neue Seite um und schließt die Abfrageparameter ein. Außerdem wird die alte Seite aus dem Browserverlauf beibehalten.
    
       ```
        <script type="text/javascript">
              var queryString = window.location.search.substring(1);
              window.location.replace("{RelativePathToNewPageFile}" + "?" + queryString);
        </script>
       ```

   4. Löschen Sie alle anderen **asp:Content**-Elemente auf der Seite.
  
   5. Wenn die Seite, die Sie ersetzen, die Startseite für das Add-In ist, ändern Sie das **StartPage**-Element im Add-In-Manifest so, dass es auf die neue Seite verweist.

5. Wenn das Add-In-Web des Add-Ins eine **CustomAction** oder ein **ClientWebPart** enthält und Sie diese bzw. dieses als Teil eines Updates ändern, müssen Sie das Elemenmanifest ändern, da diese Komponenten hier definiert werden. (Dies ist eine Ausnahme zu der allgemein bewährten Methode, gemäß der Sie ein Elementmanifest aus einer früheren Version des Add-Ins beim Aktualisieren des Add-Ins nicht bearbeiten sollten.) Sie müssen auch das **ElementManifest**-Element aus dem **ElementManifests**-Abschnitt in den **ApplyElementManifests**-Abschnitt kopieren (nicht verschieben).

#### <a name="example-of-feature-xml-for-upgrading-an-add-in-the-first-time"></a>Feature-XML-Beispielcode für das erstmalige Upgrade eines Add-Ins

Nachfolgend finden Sie ein Beispiel einer vollständigen _{FeatureName}_.Template.xml-Datei für ein erstmaliges Update eines Add-Ins. Das aktualisierte Add-In in diesem Beispiel umfasst eine geänderte Default.aspx-Datei, auf die in der Datei `Pages\Elements.xml` verwiesen wird, und diese stellt drei neue jQuery-Dateien bereit, auf die jeweils in der Datei `Scripts\Elements.xml` verwiesen wird. Beachten Sie, das sich alle Instanzen von **ElementFile** im Abschnitt **ElementManifests** befinden und dass `<ElementManifest Location="Pages\Elements.xml" />` aus dem **ElementManifests**-Abschnitt in den **ApplyElementManifests**-Abschnitt kopiert (nicht verschoben) wurde.

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

<a name="SubsequentUpgrades"> </a>
### <a name="subsequent-updates-of-the-add-in-web"></a>Anschließende Aktualisierungen des Add-In-Webs

Wenn Sie ein SharePoint-Add-In zum zweiten (oder dritten usw.) Mal aktualisieren, müssen Sie berücksichtigen, dass einige Ihrer Kunden frühere Updates möglicherweise nicht ausgeführt haben. Wenn ein Benutzer also auf die Aufforderung „Update verfügbar“ reagiert, nachdem Ihr neuestes Update im Add-In-Katalog der Organisation oder im Office Store bereitgestellt wurde, wird seine Instanz des Add-Ins in einem einzigen Updateprozess möglicherweise über mehrere Version aktualisiert. 

In den meisten Fällen ist dies genau das, was passieren soll: Sie möchten, dass jede frühere Version des Add-Ins auf die neueste Version aktualisiert wird. Sie möchten jedoch nicht, dass jede Updateaktion für dass Add-In-Webfeature für jede Instanz des Add-Ins wiederholt wird. Es gibt manche Updateaktionen, die nicht mehrmals für eine bestimmte Add-In-Instanz ausgeführt werden sollten. Wenn Sie in einem Update beispielsweise ein Feld zu einem Inhaltstyp hinzufügen, soll dieses Feld im nächsten Update nicht erneut hinzugefügt werden. Im folgenden Verfahren wird gezeigt, wie das **VersionRange**-Element verwendet wird, um zu steuern, welche Updateaktionen basierend auf der Version des Features ausgeführt werden, das aktualisiert wird.

#### <a name="to-change-the-add-in-web-feature-on-later-updates"></a>So ändern Sie das Add-In-Web-Feature bei späteren Updates

1. Öffnen Sie die Datei „_FeatureName_.Template.xml“ zur Bearbeitung, wie im Verfahren **So bearbeiten Sie den Feature-XML-Code** weiter oben in diesem Artikel beschrieben, und erhöhen Sie das Attribut **Version** des Elements [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx).  Sie sollten für das Feature dieselbe Versionsnummer verwenden wie für das Add-In.
    
   Um unser Beispiel weiterzuführen, nehmen wir an, dass Sie das Add-In zuvor von Version 1.0.0.0 auf Version 2.0.0.0 aktualisiert haben und nun auf Version 3.0.0.0 aktualisieren. Legen Sie das Attribut **Version** also auf „3.0.0.0“ fest.    
 
2. Fügen Sie ein neues **VersionRange**-Element unter allen vorhandenen **VersionRange**-Elementen hinzu. Fügen Sie *kein* **BeginVersion**- oder **EndVersion**-Attribut zu diesem Element hinzu.    
 
3. Füllen Sie das **VersionRange**-Element, wie im Verfahren **So aktualisieren Sie das Add-In-Web-Feature zum ersten Mal** weiter oben in diesem Artikel beschrieben, um die Änderungen zu berücksichtigen, die Sie an dieser aktualisierten Version des Features vorgenommen haben. Immer dann, wenn dieses Verfahren auf den **ApplyElementManifests**-Abschnitt verweist, behandeln Sie dies wie einen Verweis auf das **ApplyElementManifests**-Element, das ein untergeordnetes Element des **VersionRange**-Elements ist, das Sie soeben hinzugefügt haben, also das *unterste* in der Feature-XML-Datei.
    
4. Gehen Sie zum vorherigen **VersionRange**-Element (das Element, das Sie bei der letzten Aktualisierung des Add-Ins von 1.0.0.0 auf 2.0.0.0 im folgenden Beispiel hinzugefügt haben), und fügen Sie ein **EndVersion**-Attribut hinzu. Sie möchten, dass die Upgradeaktionen in diesem **VersionRange** auf alle anderen Versionen des Add-Ins angewendet werden, auf die diese noch nicht angewendet wurden (Version 1.0.0.0), die Aktionen sollen jedoch nicht erneut auf Versionen angewendet werden, auf die diese bereits angewendet wurden (Version 2.0.0.0). Der Wert **EndVersion** ist *ausschließlich*, Sie legen ihn daher auf die niedrigste Version fest, auf die die Upgradeaktionen *nicht* angewendet werden sollen. Im folgenden Beispiel wird dieser Wert auf  2.0.0.0 festgelegt. Die Datei sollte nun etwa wie folgt aussehen.
    
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

   Folgen Sie bei jeder Aktualisierung des Features demselben Muster. Fügen Sie einen neuen **VersionRange** für die neuesten Updateaktionen hinzu. Fügen Sie ein **EndVersion**-Element zu dem _vorherigen_ **VersionRange**-Element hinzu, und legen Sie es auf die frühere Versionsnummer fest. Im folgenden Beispiel würde die Datei für das Update von 3.0.0.0 auf 4.0.0.0 folgendermaßen aussehen.

     
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

   Beachten Sie, dass das aktuellste **VersionRange**-Element kein **BeginVersion**- oder **EndVersion**-Attribut besitzt. Dies gewährleistet, dass die in diesem **VersionRange**-Element enthaltenen Aktualisierungsaktionen auf alle vorherigen Versionen des Features angewendet werden. Dies sollte der Fall sein, da in diesem **VersionRange**-Element auf alle aktuellen Änderungen verwiesen wird und keine davon bereits in einer Instanz des Features vorgenommen wurde.
    
   Beachten Sie auch, dass das **BeginVersion**-Attribut in keiner der Instanzen von **VersionRange** verwendet wird. Der Grund dafür ist, dass der Standardwert für das Attribut **BeginVersion** „0.0.0.0" lautet, und dies der gewünschte Wert ist, denn alle Aktualisierungsaktionen sollen auf jede Instanz des Add-Ins angewendet werden, dessen Version unter dem im Attribut **EndVersion** festgelegten Wert liegt.
    
   > [!IMPORTANT]
   > Das **VersionRange**-Element bestimmt nur, auf welche Versionen des Features die Upgrades angewendet werden. Es bestimmt nicht, welche Versionen des Add-Ins eine Benachrichtigung erhalten, dass ein Update verfügbar ist (die Benachrichtigung wird nur von der Add-In-Versionsnummer ausgelöst). Innerhalb von 24 Stunden, nachdem eine neue Version des Add-Ins im Add-In-Katalog der Organisation oder im Office Store verfügbar gemacht wurde, erhält jede installierte Instanz des Add-Ins, unabhängig von der Version, die Benachrichtigung, dass ein Update verfügbar ist, auf seiner Kachel auf der Seite **Site Contents**. Der **VersionRange** hat keine Auswirkungen auf die neue Versionsnummer des neu aktualisierten Features oder des neu aktualisierten Add-Ins. Diese beiden Nummern werden immer auf die neueste Versionsnummer geändert, unabhängig davon, in welchem Versionsbereich sich das Feature vor dem Upgrade befand. 

   > Dies ist ein weiterer guter Grund, die Verwendung eines **BeginVersion**-Attributs zu vermeiden. Das **BeginVersion**-Attribut kann verwendet werden, um zu verhindern, dass einige Upgradeaktionen für dieselben Add-In-Instanzen ausgeführt werden. Es kann jedoch nicht verhindern, dass die Version des Features oder von Add-Ins auf die neueste Version angehoben werden. Durch Verwendung eines **BeginVersion**-Attributs könnte eine Situation entstehen, in der zwei Instanzen Ihres Add-Ins dieselbe Add-In-Versionsnummer und dieselbe Add-In-Webfeature-Versionsnummer aufweisen, jedoch unterschiedliche Komponenten in ihren Add-In-Webs haben.

<a name="VerifyDeployAppWebComp"> </a>
## <a name="verify-deployment-of-add-in-web-components"></a>Überprüfen der Bereitstellung von Add-In-Webkomponenten

Führen Sie die folgenden Schritte aus, um die Bereitstellung des Add-In-Web-Features und seiner Komponenten zu überprüfen.

### <a name="to-verify-the-provisioning-of-the-add-in-web"></a>So überprüfen Sie die Bereitstellung des Add-In-Webs

1. Öffnen Sie die Seite **Websiteeinstellungen** des Hostwebs. Klicken Sie im Abschnitt **Websitesammlungsverwaltung** auf den Link **Websitehierarchie**.

2. Auf der Seite **Websitehierarchie** wird das Add-In-Web nach URL aufgeführt. Starten Sie es nicht. Kopieren Sie stattdessen die URL und verwenden Sie diese in den übrigen Schritten.

3. Navigieren Sie zu „_URL_des_Add-In-Webs_/\_/_layouts/15/ManageFeatures.aspx“, und überprüfen Sie auf der daraufhin geöffneten Seite **Websitefeatures**, ob das Feature ein Mitglied der alphabetischen Liste von Features und der Status **Aktiv** ist. 

4. Wenn Ihr Add-In-Web-Feature benutzerdefinierte Websitespalten enthält, öffnen Sie „_URL_des_Add-In-Webs_/\_/_layouts/15/mngfield.aspx“, und prüfen Sie auf der sich öffnenden Seite **Websitespalten**, ob Ihre neuen benutzerdefinierten Websitespalten aufgeführt sind.

5. Wenn Ihr Add-In-Web-Feature benutzerdefinierte Inhaltstypen enthält, öffnen Sie „_URL_des_Add-In-Webs_/\_/_layouts/15/mngctype.aspx“, und prüfen Sie auf der sich öffnenden Seite **Websiteinhaltstypen**, ob Ihre neuen Inhaltstypen aufgeführt sind.

6. Wählen Sie für jeden benutzerdefinierten Inhaltstyp und jeden Inhaltstyp, dem Sie eine Spalte hinzugefügt haben, den Link zu dem Inhaltstyp aus. Überprüfen Sie auf der Seite **Websiteinhaltstyp**, die geöffnet wird, dass der Inhaltstyp über die entsprechenden Websitespalten verfügt.

7. Wenn Ihr Add-In-Web-Feature Listeninstanzen enthält, öffnen Sie „_URL_des_Add-In-Webs_/\_/_layouts/15/mcontent.aspx“, und überprüfen Sie auf der sich öffnenden Seite **Websitebibliotheken und -listen**, ob für jede benutzerdefinierte Listeninstanz ein Link zu **„Name_der_Liste“ anpassen** vorhanden ist.

8. Klicken Sie bei jeder dieser benutzerdefinierten Listeninstanzen auf den Link **„Name_der_Liste“ anpassen**, und überprüfen Sie auf der Seite „Listeneinstellungen“, ob die Liste über die richtigen Inhaltstypen und -spalten verfügt.
    
   > [!NOTE]
   > Wenn auf der Seite der Abschnitt **Inhaltstypen** nicht vorhanden ist, müssen Sie die Verwaltung von Inhaltstypen aktivieren. Wählen Sie den Link **Erweiterte Einstellungen** aus, und aktivieren Sie auf der Seite „Erweiterte Einstellungen“ die Verwaltung von Inhaltstypen, und klicken Sie dann auf **OK**. Sie kehren zur vorherigen Seite zurück, und nun wird eine Liste von **Inhaltstyp**-Abschnitten angezeigt.

9. Im oberen Bereich der Seite befindet sich die **Webadresse** der Liste. Wenn Sie Beispielelemente in Ihre Listeninstanzdefinition eingeschlossen haben, kopieren Sie die Adresse, und fügen Sie sie in die Adressleiste des Browsers ein, und gehen Sie dann zur Liste. Überprüfen Sie, ob die Liste die erstellten Beispielelemente enthält.

## <a name="next-steps"></a>Nächste Schritte
<a name="Next"> </a>

Kehren Sie zu [Wichtige Schritte beim Aktualisieren eines Add-Ins](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) zurück, oder rufen Sie direkt einen der folgenden Artikel auf, um zu erfahren, wie Sie die nächste Hauptkomponente Ihres SharePoint-Add-Ins aktualisieren.

-  [Aktualisieren von Hostwebkomponenten in SharePoint](update-host-web-components-in-sharepoint.md)
-  [Erstellen eines Handlers für das Updateereignis in SharePoint-Add-Ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
-  [Aktualisieren von Remotekomponenten in SharePoint-Add-Ins](update-remote-components-in-sharepoint-add-ins.md)

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Aktualisieren von SharePoint-Add-Ins](update-sharepoint-add-ins.md)
-  [Hinzufügen von Elementen zu einem vorhandenen Feature](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) im Microsoft SharePoint 2010-Software Development Kit (SDK).
-  [Aktualisieren von Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) im Microsoft SharePoint 2010-Software Development Kit (SDK).

