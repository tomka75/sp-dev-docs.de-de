---
title: "Vorgehensweise Hinzufügen von Ausschnitt glätten Sicherheit in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4beaab08-760b-408a-b768-906312779379
ms.openlocfilehash: 4b6dd168f921d249159a05cf6266ae2ca79cf698
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-add-a-security-trim-snippet-in-sharepoint"></a>Vorgehensweise: Hinzufügen von Ausschnitt glätten Sicherheit in SharePoint
Sie können einen Codeausschnitt für die Sicherheitskürzung verwenden, um Inhalte nur bestimmten Benutzern basierend auf einer bestimmten Berechtigung, über die diese Benutzer verfügen müssen, und abhängig davon, ob es sich um authentifizierte oder anonyme Benutzer handelt, anzuzeigen.
## <a name="introduction-to-the-security-trim-snippet"></a>Einführung in die Sicherheit erhöhen, Ausschnitt
<a name="Introduction"> </a>

Sie können einen Ausschnitt Sicherheit erhöhen, anzuzeigenden Inhalt nur für bestimmte Benutzer, basierend auf eine bestimmte Berechtigung, die diese Benutzer verfügen müssen, und gibt an, ob die Benutzer sind, authentifiziert oder anonym. Sie können eine Gestaltungsvorlage oder Seitenlayout ein Bereich Sicherheit erhöhen, hinzugefügt. Ein Bereich Sicherheit erhöhen, ist ein Container, der andere Komponenten oder Ausschnitte, wie Webparts, zusätzlich zu statischer Inhalt enthalten kann.
  
    
    
Einen Bereich Sicherheit erhöhen, können Sie beispielsweise die folgende Inhalte für bestimmte Benutzer anzuzeigen:
  
    
    

- Ein Inhalt-nach-Search-Webpart, welche Dokumente angezeigt, als authentifizierter Benutzer gerade arbeitet.
    
  
- Eine Liste der zuletzt geänderte Dokumente anzeigen, damit authentifizierte Benutzer sehen, was auf der Website neue ist.
    
  
- Ein Inhalt-nach-Search Web Part, die für Besucher von nicht authentifizierten eine Liste der zeigt empfohlene Links, die basierend auf den aktuellen Artikel. Diese Liste enthält Empfehlungen möglicherweise Noise authentifizierten Inhaltsautoren arbeiten in der Website, aber es ist wichtig für Besucher von nicht authentifizierten.
    
  
- Ein vom Menüband unabhängiger Anmeldelink für nicht authentifizierte Benutzer oder Benutzer, die noch authentifiziert werden müssen.
    
    > **Hinweis:** Dieser Anmeldelink wird automatisch in eine Gestaltungsvorlage eingefügt, die mithilfe des Entwurfs-Manager erstellt wird, Sie können ihn jedoch löschen, wenn er nicht benötigt wird. 
      > Ein Sicherheitskürzungsbereich hat zwei wichtige Eigenschaftseinstellungen, eine für die Authentifizierung und eine für Berechtigungen (oder Autorisierung). Sie können einen Sicherheitskürzungsbereich z. B. verwenden, um bestimmten Benutzern den folgenden Inhalt anzuzeigen:
  
    
    

- **AuthenticationRestrictions** Mit dieser Eigenschaft können Sie die Systemsteuerung auf authentifizierte oder anonyme Benutzer beschränken, oder wählen Sie alle Benutzer (alle Benutzer ist die Standardeinstellung).
    
  
- **Berechtigungen** Mit dieser Eigenschaft können Sie eine bestimmte Berechtigung auswählen, die Benutzer benötigen, um den Inhalt im Bereich anzuzeigen.
    
    > **Hinweis:** Sie wählen eine einzelne Berechtigung aus, keine Berechtigungsstufe. (Eine Berechtigungsstufe ist ein Satz erteilter Berechtigungen.) Wenn Sie die Authentifizierung nur auf anonyme Benutzer beschränken, ist es normalerweise nicht erforderlich, eine bestimmte Berechtigung anzugeben, da anonymen Benutzern in der Regel keine SharePoint-Berechtigungen zugewiesen sind. Es ist sinnvoll, Berechtigungen nur für alle Benutzer oder für alle authentifizierten Benutzer zu verwenden.
  
    
    
Die Sicherheit erhöhen, Systemsteuerung verfügt über drei Optionen klicken Sie im Menüband in der linken Spalte von Tabelle 1 aufgeführt. Tabelle 1 zeigt, wie diese Einstellungen bestimmen, die bestimmte Berechtigung, die Benutzer verfügen müssen, die niedrigste Standardberechtigungsstufe, die diese bestimmte Berechtigung enthält und die Gruppe, die mit dieser Berechtigungsstufe standardmäßig verknüpft ist.)
  
    
    

> **Hinweis** Dies sind die Standardeinstellungen, die für jeden gegebenen Bereich, wie eine Websitesammlung, Website, Liste oder ein Element, geändert werden können. 
  
    
    

Wenn Sie einen Bereich erhöhen, Sicherheit **für Autoren** anzeigen festlegen, ist beispielsweise durch Standardinhalt innerhalb dieses Bereichs für Benutzer in der Gruppe Mitglieder und der Gruppe "Besitzer" angezeigt.
  
    
    

**In Tabelle 1. Zuordnung von Optionen im standardmäßigen Berechtigungsebenen und Gruppen**


|**Sicherheit Trim Systemsteuerung option**|**Permissions-Eigenschaft**|**Berechtigung**|**Berechtigungsstufe**|**Group**|
|:-----|:-----|:-----|:-----|:-----|
|Autoren anzeigen  <br/> |**AddAndCustomizePages** <br/> |Seiten hinzufügen und anpassen  <br/> |Contribute (oder höher)  <br/> |Elemente  <br/> |
|Für authentifizierte Benutzer anzeigen  <br/> |**ViewPages** <br/> |Seiten anzeigen  <br/> |Lesen (oder höher)  <br/> |Besucher  <br/> |
|Für Administratoren anzeigen  <br/> |**FullMask** <br/> |Alles markieren  <br/> |Vollzugriff  <br/> |Besitzer  <br/> |
   

### <a name="inserting-a-security-trim-panel"></a>Einfügen eines Bereichs Sicherheit erhöhen
<a name="InsertSnippet"> </a>

Wie alle Ausschnitte fügen Sie den Codeausschnitt Sicherheit erhöhen, aus der Codeausschnittkatalog. Zum Codeausschnittkatalog zu navigieren, müssen Sie zuerst eine Gestaltungsvorlage oder Seitenlayout bearbeiten auswählen.
  
    
    

### <a name="to-insert-a-security-trim-panel"></a>So fügen Sie einen Bereich Sicherheit erhöhen, ein


1. Wechseln Sie zu Ihrer Veröffentlichungswebsite.
    
  
2. Wählen Sie in der rechten oberen Ecke der Seite das Zahnradsymbol für Einstellungen und dann **Entwurfs-Manager** aus.
    
  
3. Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten** oder **Seitenlayouts bearbeiten** aus, je nachdem, welchen Dateityp Sie bearbeiten.
    
  
4. Wählen Sie den Namen der Masterseite oder Seitenlayout, das Sie den Codeausschnitt hinzufügen möchten.
    
  
5. Wählen Sie zum Öffnen des Codeausschnittkatalogs in der serverseitigen Vorschau in der rechten oberen Ecke **Codeausschnitte** aus.
    
  
6. Wählen Sie auf dem Menüband auf der Registerkarte **Entwurf** **Sicherheit zu erhöhen**.
    
    In der Dropdown-Liste auf die Schaltfläche **Sicherheit zu erhöhen**, können Sie optional die Benutzer auswählen, denen der Inhalt des Bereichs werden angezeigt, oder Sie können weitere Optionen anzeigen, indem die wichtige Eigenschaftswerte für den Bereich konfigurieren.
    
  
7. Im Codeausschnittkatalog können auf der rechten Seite auf **Infos zu dieser Komponente** klicken oder diese Option auswählen, um Eigenschaftengruppen ein- oder auszublenden, und anschließend die gewünschten benutzerdefinierten Einstellungen konfigurieren.
    
  
8. Nachdem Sie Eigenschaften konfiguriert haben, wählen Sie **Aktualisieren**. Dadurch wird der HTML-Codeausschnitt links auf der Seite aktualisiert, sodass das Markup Ihre benutzerdefinierten Einstellungen widerspiegelt. Sie können stets **Zurücksetzen** wählen, um alle Eigenschaften auf ihre Standardeinstellungen zurückzusetzen.
    
  
9. Wählen Sie links im Codeausschnittkatalog unter **HTML-Codeausschnitt** den Befehl **In Zwischenablage kopieren**.
    
  
10. Öffnen Sie im HTML-Editor das zugeordnete Netzlaufwerk auf dem Computer, und öffnen Sie dann die HTML-Datei für die Gestaltungsvorlage oder das Seitenlayout, der bzw. dem Sie den Codeausschnitt hinzufügen.
    
  
11. Fügen Sie den Codeausschnitt in der HTML-Datei an der Stelle ein, an der das Markup angezeigt werden soll.
    
    Wenn Sie den Codeausschnitt, einem Seitenlayout hinzufügen, stellen Sie sicher, dass Sie den Codeausschnitt innerhalb des **PlaceHolderMain**einfügen.
    
  
12. Ersetzen Sie im **<div>**-Tag  `class="DefaultContentBlock"` durch Ihren eigenen spezifischen Inhalt.
    
  
13. Speichern Sie die Seite, und aktualisieren Sie die serverseitige Vorschau im Entwurfs-Manager, um sicherzustellen, dass die Sicherheit erhöhen, wird angezeigt, wie erwartet.
    
  

## <a name="understanding-the-snippet-markup"></a>Grundlegendes zum Codeausschnittmarkup
<a name="UnderstandMarkup"> </a>

Die wichtigsten Teile des einen Ausschnitt Sicherheit erhöhen, sind die **AuthenticationRestrictions** -Eigenschaft und die **Permissions** -Eigenschaft und die **<div>** in Fettschrift unten. **AuthenticationRestrictions** im Markup nur, wenn von **AllUsers**, geändert Standard wird angezeigt. Wenn Sie **Zurücksetzen** für den Ausschnitt im Codeausschnittkatalog auswählen, wird **AuthenticationRestrictions** aus dem Markup entfernt, was bedeutet, dass der Ausschnitt den Standardwert **AllUsers**verwendet.
  
    
    
Die **<div>**, wobei `class="DefaultContentBlock"` ist, was Sie mit Ihren eigenen Inhalt ersetzen die anderen Snippets und Steuerelemente enthalten können.
  
    
    



```HTML

<div data-name="SecurityTrimmedAuthors">
    <!--CS: Start Security Trim Snippet-->
    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AuthenticatedUsersOnly" Permissions="AddAndCustomizePages" PermissionContext="RootSite">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><span><!--PE: End of READ-ONLY PREVIEW-->
        <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Security Trim Properties.
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--></span><!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
    <!--CE: End Security Trim Snippet-->
</div>
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="AdditionalResources"> </a>


-  [Einführung: Steuern des Benutzerzugriffs mit Berechtigungen](http://office.microsoft.com/en-us/sharepoint-foundation-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=1)
    
  
-  [Grundlegendes zu Berechtigungsstufen](http://office.microsoft.com/en-us/products/default-permission-levels-HA102772313.aspx?CTT=5&amp;origin=HA102771919)
    
  
-  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md)
    
  
-  [Erstellen von Websites für SharePoint](build-sites-for-sharepoint.md)
    
  
-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
    
  

