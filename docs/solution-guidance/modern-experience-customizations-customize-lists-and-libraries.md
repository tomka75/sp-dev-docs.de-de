---
title: Anpassen von "modernen" Listen und Bibliotheken
description: "Rufen Sie eine SharePoint Online Erfahrung schnellere, mehr intuitive und schnell durch Anpassen der Listen und Bibliotheken für die \"modernen\" Erfahrung im Umgang mit benutzerdefinierten Benutzeraktionen und benutzerdefiniertes branding."
ms.date: 11/09/2017
ms.openlocfilehash: 086485e4749fb6adbba5cd252415d5d62fbacc74
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="customizing-modern-lists-and-libraries"></a>Anpassen von "modernen" Listen und Bibliotheken

2016 veröffentlicht das SharePoint Online-Team "modernen" Dokument Listen und Bibliotheken, in denen eine höhere benutzerfreundlichkeit zu bringen, die schneller, mehr intuitiv und schnell ist. **"Modernen" dieser Kommunikationskanäle bieten viele Vorteile, und es wird ausdrücklich empfohlen verwenden können**. Wenn Ihre aktuellen Anpassungen noch nicht mit der "modernen" Erfahrung funktionieren, sich Gedanken darüber machen, denen Laufe, damit Ihre Benutzer die umfangreiche Verbesserungen nutzen können:

 - "Modernen" Dokumentbibliotheken haben eine aktualisierte Benutzeroberfläche, die eine OneDrive, ähnelt wünschen bietet, damit es mehr intuitive ist, erstellen Sie einen neuen Ordner und Hochladen von Dateien im Browser.
 
 - Sie können die **Pin zum Anfang der Seite** zum Hinzufügen von Dokumenten "oberhalb der Faltung" in einer beliebigen Ansicht auf dem Bildschirm auswählen.
 
 - Kopieren ist nicht neu, aber die Gesten verschieben und kopieren sind intelligent zum Anzeigen Ihrer Informationsarchitektur und lassen Sie den neuen Ordner zu erstellen.
 
 - Möglicherweise müssen nicht mehr so viele Kopien. Dokumentbibliotheken sind intelligent zu anderen Dateien verwendeten Sie in SharePoint, damit Sie anderen Dateien aus anderen Bibliotheken als Links, importieren können ohne Dateien zwischen mehreren Websites zu duplizieren.
 
 - Die neue Dokumentbibliotheken können Sie Dateien direkt auf der Hauptseite ohne vorherige einen separaten Admin Bildschirm gruppieren. Sie können auch ziehen, um die Größe der Spalten als auch sortieren, Filtern und Gruppieren von eine Spaltenüberschrift zu ändern.
 
 - Mobile Browser haben die gleichen Funktionen wie den Desktop, wodurch SharePoint produktive für jeden Benutzer, ob sie über die Maus, Tastatur, Fingereingabe oder Bildschirmsprachausgabe interagieren.
 
 - Sie können jetzt Metadaten direkt in der Hauptansicht in der Systemsteuerung Informationen bearbeiten. Nicht mehr in mehrere Bildschirme zum Anwenden von Updates auf!
 
 - Dank der Integration von Office Online können Sie eine vollständige Dokumentvorschau am oberen Rand der Dokumentinformationsbereich navigieren. Die Systemsteuerung bietet Metadaten, einschließlich des Verlaufs der letzte Aktivität auf die Datei aktualisiert und, die eine Freigabe in der Datei empfangen.

Dieser Artikel befasst sich die der Erweiterbarkeitsoptionen in der Bibliothek "modernen" und Liste auftritt. Allerdings erfahren Sie mehr über die Funktionen von "modernen" dieser Kommunikationskanäle angeboten werden soll, finden Sie unter den folgenden Ressourcen:

- [Moderne Dokumentbibliotheken in SharePoint](https://blogs.office.com/2016/06/07/modern-document-libraries-in-sharepoint)
- [Moderne SharePoint-Listen sind hier – einschließlich Integration mit Microsoft Flow und PowerApps](https://blogs.office.com/2016/07/25/modern-sharepoint-lists-are-here-including-integration-with-microsoft-flow-and-powerapps)
- [Unterschiede zwischen dem neuen und die klassische Authentifizierung Erfahrungen für Listen und Bibliotheken](https://support.office.com/en-us/article/Differences-between-classic-and-new-experiences-for-lists-and-document-libraries-30e1aab0-a5cc-4363-b7f2-09e2ae07d4dc?ui=en-US&rs=en-US&ad=US)

Im weiteren Verlauf des Artikels verwenden "modernen" für die neue Benutzeroberfläche und "klassische" für die ältere Benutzeroberfläche wir. 

> [!IMPORTANT]
> Wir sind nicht die "klassische" Erfahrung veralteter; "klassische" und "modernen" werden gleichzeitig verwendet werden.


<a name="customizationoptions"> </a>
## <a name="overview-of-customization-options"></a>Übersicht über die Optionen für die Anpassung

"Modernen" Listen und Bibliotheken unterstützen keine beliebig viele Anpassungsoptionen als "klassische" Listen und Bibliotheken. In diesem Artikel finden Sie Informationen und Beispiele für die unterstützten Optionen. SharePoint-Team ist funktionsfähig, um weitere Optionen in der Zukunft zu unterstützen. Die folgende Liste enthält einen schnellen Überblick über die unterstützten Funktionen für "modernen" Listen und Bibliotheken:
 
 - Teilmenge der Benutzer benutzerdefinierte Aktionen
 - Benutzerdefiniertes branding
 - Integration von PowerApps und Ablauf

Für diese Anpassungen werden derzeit nicht für "modernen" Listen und Bibliotheken unterstützt:
 
 - Feld JSLink-basierte Anpassungen (siehe Hinweis auf *SharePoint-Framework-Erweiterungen*)
 - JSLink-basierte Ansicht Anpassungen (siehe Hinweis auf *SharePoint-Framework-Erweiterungen*)
 - Benutzerdefinierte CSS über AlternateCSSUrl Web-Eigenschaft
 - Benutzerdefiniertes JavaScript eingebettet über benutzerdefinierte Aktionen des Benutzers (siehe Hinweis auf *SharePoint-Framework-Erweiterungen*)
 - Benutzerdefinierte Masterseiten (umfangreichere branding wird unterstützt werden später mit alternativen)
 - Anpassung über InfoPath
 - Minimale Downloadstrategie (MDS)
 - SharePoint Server-Veröffentlichung

> [!NOTE]
> Im Juni 2017, [SharePoint-Framework-Erweiterungen in Vorschau für Entwickler hinausgehen](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview). Dieser Erweiterungen der SharePoint-Framework verwenden, können Sie steuern, das Rendering eines Felds über den benutzerdefinierten Code, und Sie können benutzerdefinierte Aktionen, die Ihre benutzerdefinierten Code auszuführen, Benutzer erstellen. Finden Sie weitere Informationen finden Sie unter [Übersicht über SharePoint Framework Extensions](http://aka.ms/spfx-extensions). 

<a name="supportedcustomactions"> </a>
## <a name="user-custom-actions"></a>Benutzerdefinierte Aktionen für Benutzer

"Modernen" dieser Kommunikationskanäle zulassen von bestimmten Benutzer benutzerdefinierte Aktionen in die neue Benutzeroberfläche verfügbar gemacht werden, jedoch nicht alle Benutzer-Aktion durch "klassische" unterstützten Konfigurationen "modernen" Oberfläche unterstützt werden. Die folgende Tabelle enthält einen allgemeinen Überblick über die unterstützten benutzerdefinierte aktionsspeicherorte und sie in der Benutzeroberfläche "modernen" Darstellung sind:

|**Speicherort für die benutzerdefinierte Aktion**|**Auf "modernen" Benutzeroberfläche sichtbar**|
|:-----|:-----|
| `EditControlBlock` | Ja, werden diese Einträge als benutzerdefinierter Menüelemente.|
| `CommandUI.Ribbon` | Ja, werden diese Einträge als Symbolleistenelementen. |
| Alle anderen Speicherorte (zum Beispiel `scriptlink`) | Es ist leider benutzerdefinierte Benutzervorgänge, funktionieren nicht. |

> [!NOTE]
> Benutzerdefinierten Aktionen werden in "modernen" Listen und Bibliotheken nur, wenn Sie auf "klassische" Websites mit "modernen" Benutzeroberfläche aktiviert sind. In der Standardeinstellung nicht sie auf "modernen" Websites angezeigt, da es nicht möglich ist, benutzerdefinierte Aktionen des Benutzers "modernen" Websites hinzufügen, da sie die Option NoScript aktiviert haben. Sie können jedoch NoScript auf "modernen" Websites zum erreichen Sie dasselbe Verhaltens für "modernen" Listen und Bibliotheken "klassische" und "modernen" Standorten deaktivieren.

<a name="editcontrolblockcustomactions"> </a>
### <a name="editcontrolblock-user-custom-actions"></a>EditControlBlock Benutzer benutzerdefinierte Aktionen 

Hinzufügen von benutzerdefinierten Links zum Kontextmenü ist möglich, mithilfe der `EditControlBlock` als Speicherort für die benutzerdefinierte Aktion. Das folgende XML des Plug & Play-Bereitstellung werden zwei benutzerdefinierten Einträge erstellt. 

```XML
<pnp:ProvisioningTemplate ID="EditControlBlockSamples" Version="1" xmlns:pnp="http://schemas.dev.office.com/PnP/2015/12/ProvisioningSchema">
  <pnp:CustomActions>
    <pnp:SiteCustomActions>
      <pnp:CustomAction Name="CA_1" Description="ca 1" Location="EditControlBlock" RegistrationType="List" RegistrationId="101" Title="CA 1 Title" Sequence="3000" Url="https://contoso.azurewebsites.net/pages/index.aspx" Enabled="true"/>
      <pnp:CustomAction Name="CA_2" Description="ca 2" Location="EditControlBlock" RegistrationType="ContentType" RegistrationId="0x0101" Title="CA 2 Title" Sequence="4000" Url="https://contoso.azurewebsites.net/pages/index.aspx" Enabled="true"/>
    </pnp:SiteCustomActions>
  </pnp:CustomActions>
</pnp:ProvisioningTemplate>
```

Sie können diese- [Plug & Play-Bereitstellung Vorlage](https://msdn.microsoft.com/en-us/pnp_articles/pnp-provisioning-engine-and-the-core-library) auf einer Website mit der Plug & Play-Core-Bibliothek oder [Plug & Play-PowerShell](http://aka.ms/sppnp-powershell)anwenden. Wir haben sich entschieden, den PowerShell-Ansatz in diesem Artikel zeigen. Zunächst wird [das Plug & Play-PowerShell-Modul](https://github.com/SharePoint/PnP-PowerShell)installieren. Die Sie nach Abschluss den Bereitstellung Plug & Play-XML-Code in einer Datei speichern, und die zwei einfachen Zeilen des Plug & Play-PowerShell ausreichen, um die Vorlage anwenden:

```PowerShell

# Connect to a previously created Modern Site
$cred = Get-Credential
Connect-PnPOnline -Url https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Apply the PnP provisioning template
Apply-PnPProvisioningTemplate -Path c:\customaction_modern_editcontrolblock.xml -Handlers CustomActions

```

Wenn Sie die "moderne" Ansicht einer Dokumentbibliothek auf Ihrer Website aktualisieren, sehen Sie die neuen Einträge angezeigt werden.

*Abbildung 1. Benutzerdefinierte EditControlBlock Aktionen im Menü sichtbar.*

<img src="media/modern-experiences/custom-editcontrolblock-actions.png" alt="Custom EditControlBlock actions visible in the menu" width="700">


> [!NOTE]
> - Wenn Sie dies auf einer [Teamwebsite "modernen"](modern-experience-customizations-customize-sites.md) herausfinden, in denen Sie die Option NoScript deaktiviert, verwenden Sie die April 2017 oder höhere Version von PnP-PowerShell. Verwenden Sie die aktuelle Version Dev Alternativ.
> - Wenn Sie in diesem Beispiel für eine Liste verwenden möchten, legen Sie die `RegistrationId` -Attribut auf 100.

<a name="ribboncustomactions"> </a>
### <a name="commanduiribbon-user-custom-actions"></a>CommandUI.Ribbon Benutzer benutzerdefinierte Aktionen 

Wenn Sie die Symbolleiste in der "modernen" Listen- und Bibliotheksdaten Erfahrungen erweitern möchten, können Sie dazu hinzufügen der benutzerdefinierten Aktion eines Benutzers für den Speicherort CommandUI.Ribbon wie bei diesem Plug & Play-Bereitstellung XML-Beispiel gezeigt.

```XML
<pnp:ProvisioningTemplate ID="CommandUIRibbonSamples" Version="1" xmlns:pnp="http://schemas.dev.office.com/PnP/2015/12/ProvisioningSchema">
  <pnp:CustomActions>
    <pnp:SiteCustomActions>
      <pnp:CustomAction Name="CA_4" Description="ca 4" Location="CommandUI.Ribbon" RegistrationType="List" RegistrationId="101" Title="CA 4 Title" Sequence="6000" Enabled="true">
        <pnp:CommandUIExtension>
          <CommandUIDefinitions>
            <CommandUIDefinition Location="Ribbon.Documents.Copies.Controls._children">
              <Button
                Id="Ribbon.Documents.Copies.OfficeDevPnPDownloadAll"
                Command="OfficeDevPnP.Cmd.DownloadAll"
                Image16by16="/_layouts/15/images/sharepointfoundation16.png"
                LabelText="Download All"
                Description="Download all files separately"
                ToolTipTitle="Download All"
                ToolTipDescription="Download all files separately"
                TemplateAlias="o1"
                Sequence="15"/>
            </CommandUIDefinition>
          </CommandUIDefinitions>
          <CommandUIHandlers>
            <CommandUIHandler
              Command="OfficeDevPnP.Cmd.DownloadAll"
              CommandAction="https://contoso.azurewebsites.net/pages/index.aspx" />
          </CommandUIHandlers>
        </pnp:CommandUIExtension>
      </pnp:CustomAction>
      <pnp:CustomAction Name="CA_6" Description="ca 6" Location="CommandUI.Ribbon" RegistrationType="ContentType" RegistrationId="0x0101" Title="CA 6 Title" Sequence="5000" Enabled="true">
        <pnp:CommandUIExtension>
            <CommandUIDefinitions>
              <CommandUIDefinition Location="Ribbon.Tabs._children">
                <Tab Id="Custom Tab" Title="Custom Tab" Description="Custom Tab">
                  <Scaling Id="Custom Tab.Scaling">
                    <MaxSize Id="Custom Group.Scaling.MaxSize" GroupId="Custom Group" Size="TwoLarge" />
                    <MaxSize Id="Custom Group 2.Scaling.MaxSize" GroupId="Custom Group 2" Size="OneLarge" />
                    <Scale Id="Custom Group.Scaling.Scale" GroupId="Custom Group" Size="TwoLarge" />
                    <Scale Id="Custom Group 2.Scaling.Scale" GroupId="Custom Group 2" Size="OneLarge" />
                  </Scaling>
                  <Groups Id="Custom Tab.Groups">
                    <Group Id="Custom Group 2" Title="Custom Group 2" Description="Custom Group 2" Sequence="7888" Template="Ribbon.Templates.OneLarge">
                      <Controls Id="Custom Group 2.Controls">
                        <Button Id="CustomButton3" LabelText="Custom Button 3" Image16by16="/_layouts/15/images/attach16.png" Image32by32="/_layouts/15/images/attach16.png" ToolTipTitle="Custom Button 3" ToolTipDescription="Custom Button 3" Command="CustomButton3.Command" TemplateAlias="c3" />
                      </Controls>
                    </Group>
                    <Group Id="Custom Group" Title="Custom Group 1" Description="Custom Group 1" Sequence="10000" Template="Ribbon.Templates.TwoLarge">
                      <Controls Id="Custom Group 1.Controls">
                        <Button Id="CustomButton1" LabelText="Custom Button 1" Image16by16="/_layouts/15/images/itslidelibrary.png" Image32by32="/_layouts/15/images/itslidelibrary.png" ToolTipTitle="Custom Button 1" ToolTipDescription="Custom Button 1" Command="CustomButton1.Command" TemplateAlias="c1" />
                        <Button Id="CustomButton2" LabelText="Custom Button 2" Image16by16="/_layouts/15/images/dldsln16.png" Image32by32="/_layouts/15/images/dldsln16.png" ToolTipTitle="Custom Button 2" ToolTipDescription="Custom Button 2" Command="CustomButton2.Command" TemplateAlias="c2" />
                      </Controls>
                    </Group>
                  </Groups>
                </Tab>
              </CommandUIDefinition>
              <CommandUIDefinition Location="Ribbon.Templates._children">
                <GroupTemplate Id="Ribbon.Templates.TwoLarge">
                  <Layout Title="TwoLarge" LayoutTitle="TwoLarge"> 
                    <Section Alignment="Top" Type="OneRow"> 
                      <Row> 
                        <ControlRef DisplayMode="Large" TemplateAlias="c1" /> 
                        <ControlRef DisplayMode="Large" TemplateAlias="c2" /> 
                      </Row> 
                    </Section> 
                  </Layout> 
                </GroupTemplate>
              </CommandUIDefinition>
              <CommandUIDefinition Location="Ribbon.Templates._children">
                <GroupTemplate Id="Ribbon.Templates.OneLarge">
                  <Layout Title="OneLarge" LayoutTitle="OneLarge"> 
                    <Section Alignment="Top" Type="OneRow"> 
                      <Row> 
                        <ControlRef DisplayMode="Large" TemplateAlias="c3" /> 
                      </Row> 
                    </Section> 
                  </Layout> 
                </GroupTemplate>
              </CommandUIDefinition>
            </CommandUIDefinitions>
            <CommandUIHandlers>
              <CommandUIHandler Command="CustomButton1.Command" CommandAction="https://contoso.azurewebsites.net/pages/index.aspx" />
              <CommandUIHandler Command="CustomButton2.Command" CommandAction="http://www.bing.com" />
              <CommandUIHandler Command="CustomButton3.Command" CommandAction="http://dev.office.com/sharepoint" />
            </CommandUIHandlers>
        </pnp:CommandUIExtension>
      </pnp:CustomAction>
    </pnp:SiteCustomActions>
  </pnp:CustomActions>
</pnp:ProvisioningTemplate>
```

<br/>

Nach dem Hinzufügen von benutzerdefinierten Benutzervorgänge, sehen Sie sie auf der Symbolleiste angezeigt. Beachten Sie, dass benutzerdefinierte Registerkarten in einem Dropdown-Menü umgewandelt werden.

*Abbildung 2. Benutzerdefinierte Aktion auf der Symbolleiste angezeigt*

![Benutzerdefinierte Aktion auf der Symbolleiste angezeigt](media/modern-experiences/custom-actions-toolbar.png)

<br/>

> [!NOTE]
> - Wenn Sie dies auf einer [Teamwebsite "modernen"](modern-experience-customizations-customize-sites.md) herausfinden, in denen Sie die Option NoScript deaktiviert, verwenden Sie die April 2017 oder höhere Version von PnP-PowerShell. Verwenden Sie die aktuelle Version Dev Alternativ.
> - Wenn Sie in diesem Beispiel für eine Liste verwenden möchten, legen Sie die `RegistrationId` 100 und Verwendung der folgenden XML-Code für die benutzerdefinierte Aktion des Benutzers CA_4 Attribute.
>
   ```XML
    <CommandUIDefinition Location="Ribbon.Templates._children">
      <Button
        Id="Ribbon.Templates.OfficeDevPnPDownloadAll"
        Command="OfficeDevPnP.Cmd.DownloadAll"
        Image16by16="/_layouts/15/images/sharepointfoundation16.png"
        LabelText="Download All"
        Description="Download all files separately"
        ToolTipTitle="Download All"
        ToolTipDescription="Download all files separately"
        TemplateAlias="o1"
        Sequence="15"/>
    </CommandUIDefinition>
   ```

<a name="customactionlimitations"> </a>
### <a name="user-custom-action-limitations"></a>Benutzerdefinierte Aktion Einschränkungen für Benutzer 

Berücksichtigen Sie beim Entwickeln von benutzerdefinierten Aktionen des Benutzers, die in "modernen" Erfahrungen arbeiten müssen die folgenden Nachteile:
 
 - Sie können nicht vollständig die Reihenfolge steuern, in der benutzerdefinierte Aktionen des Benutzers wird angezeigt; Benutzerdefinierte Aktionen des Benutzers in der Reihenfolge hinzugefügt werden die `_api/web/Lists(guid'listid')/CustomActionElements` gibt die benutzerdefinierte Aktionen des Benutzers und derzeit diese API ist nicht berücksichtigt die Sequenz Attribute. Schaltflächen innerhalb einer benutzerdefinierten Registerkarte definiert können hinzufügen und in der richtigen Reihenfolge im XML-CommandUIDefinition sortiert werden. Unserem Beispiel wird die Schaltfläche 3 als erste, und zwar aufgrund der Reihenfolge, in der XML-Code.
 
 - Gruppierung von benutzerdefinierten Benutzeraktionen innerhalb einer benutzerdefinierten Registerkarte wird gesteuert, durch das Vorhandensein von `Button` Elemente immer gibt es mehrere `Tab` oder `Group` Elemente im Xml-Element zurückgegebenen Benutzer benutzerdefinierte Aktion.
 
 - Befehlsaktionen können nicht JavaScript enthalten. Verwenden Sie beispielsweise `CommandAction="javascript:alert('My custom Action');"` bedeutet, der die benutzerdefinierte Aktion des Benutzers nicht angezeigt wird.
 
 - Mithilfe der `ScriptLink` oder `ScriptBlock` Eigenschaften ist nicht möglich, da sie nur verwendet werden können, mit dem Speicherort der benutzerdefinierten Aktion `ScriptLink`, die nicht unterstützt.
 
 - Mit der Bild-Karten (z. B. `Image16by16="/_layouts/15/1033/images/formatmap16x16.png?rev=33" Image16by16Left="-144" Image16by16Top="-107"`) funktioniert nicht; Sie müssen einzelne Bilder angeben. Beachten Sie außerdem, dass nur 16 x 16 Bilder relevant sind.

<a name="themingimpact"> </a>
## <a name="custom-branding"></a>Benutzerdefiniertes branding

Fall Ihrer Website verwenden eines benutzerdefinierten Designs dieses benutzerdefinierte Design wird in der Liste "modernen" berücksichtigt und Bibliothek auftritt, wie im folgenden Beispiel dargestellt.

*Abbildung 3. Moderne Liste mit benutzerdefinierten branding kommen aus benutzerdefinierten Designs*

<img src="media/modern-experiences/modern-list-with-custom-theme.png" alt="Modern list with custom branding coming from custom theme" width="700">

<a name="configuremodernlibrariesandlists"> </a>
## <a name="configure-the-end-user-experience"></a>Konfigurieren des Endbenutzers

Sie haben mehrere Optionen können Sie steuern, ob die "moderne" oder "klassische" Bibliotheks- und Erfahrung verwendet wird. 

### <a name="tenant-level-configuration"></a>Ebene Mandantenkonfiguration
Wenn Sie die "moderne" Erfahrung vollständig deaktivieren möchten, empfiehlt es sich mit dem Mandanten für diese Einstellung. Wechseln Sie zu Ihrem Mandanten Administrationscenter (beispielsweise Contoso-admin.sharepoint.com), wechseln Sie zu Einstellungen, und wählen Sie die "klassische" wünschen.

*Abbildung 4. Erleben Sie die SharePoint-Listen und Bibliotheken Einstellungen in der SharePoint-Admin-Benutzeroberfläche*

![Erleben Sie die SharePoint-Listen und Bibliotheken Einstellungen in der SharePoint-Admin-Benutzeroberfläche](media/modern-experiences/lists-libraries-tenant-settings.png)

> [!NOTE]
> - Beim Wechseln zwischen **neue Oberfläche (automatische Erkennung)** und **klassischen auftreten**, die Änderung nicht sofort sichtbar.
> - Bei Auswahl **neue Oberfläche (automatische Erkennung)**, immer sehen Sie die Option **zur klassischen SharePoint zurückzukehren** . Dies ist entwurfsbedingt, wenn die heute nicht alle Funktionen von "klassische" Listen und Bibliotheken in "modernen" Listen und Bibliotheken implementiert sind. Es gibt keine Option dieses Verhalten ändern.

### <a name="siteweb-level-configuration"></a>Konfiguration der Website /-Ebene
Sie können eine Websitesammlung oder Web verhindern, mithilfe der "modernen" Erfahrungen durch ein Feature zu aktivieren:

- Verwenden Sie für die Steuerung der Datensammlung Website die Features für die Websitesammlung als Bereich mit ID **E3540C7D-6BEA-403C-A224-1A12EAFEE4C4**. 
- Verwenden Sie für Websteuerelement das Feature Webbereich mit ID **52E14B6F-B1BB-4969-B89B-C4FAA56745EF**. 

Verwenden Sie die folgenden [Plug & Play-PowerShell](http://aka.ms/sppnp-powershell) So aktivieren oder deaktivieren Sie die erforderlichen Features:

```PowerShell
# Connect to a site
$cred = Get-Credential
Connect-PnPOnline -Url https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Prevent modern lists and libraries at site collection level
Enable-PnPFeature -Identity E3540C7D-6BEA-403C-A224-1A12EAFEE4C4 -Scope Site 
# And again enable modern lists and libraries at site collection level
#Disable-PnPFeature -Identity E3540C7D-6BEA-403C-A224-1A12EAFEE4C4 -Scope Site 

# Prevent modern lists and libraries at web level
#Enable-PnPFeature -Identity 52E14B6F-B1BB-4969-B89B-C4FAA56745EF  -Scope Web 
# And again enable modern lists and libraries at web
#Disable-PnPFeature -Identity 52E14B6F-B1BB-4969-B89B-C4FAA56745EF  -Scope Web 
```

### <a name="listlibrary-configuration"></a>Liste/Netzwerkbibliotheks-Konfiguration
Wenn Sie die Erfahrung Bibliotheksebene steuern möchten, wechseln Sie zu **Einstellungen für die Liste** > **Erweiterte Einstellungen**, und ändern Sie das Verhalten.

*Abbildung 5. Konfiguration der Liste Erfahrung in der SharePoint-Mandanten Einstellungen auf Poolebene in Admin UI*

![Konfiguration der Liste Erfahrung in der SharePoint-Mandanten Einstellungen auf Poolebene in Admin UI](media/modern-experiences/list-experience-setting.png)

Die gleichen kann auch mithilfe von CSOM, siehe dieser Ausschnitt erfolgen:

```C#
// Load the list you want to update
var list = context.Web.Lists.GetByTitle(title);
context.Load(list);
context.ExecuteQuery();

// Possible options are Auto (= what it's defined at tenant level), NewExperience (= "modern") and ClassicExperience
list.ListExperienceOptions = ListExperience.ClassicExperience;

// Persist the changes
list.Update();
context.ExecuteQuery();
```

> [!NOTE]
> - Die Einstellungen in der Bibliothek zu Ebene die Einstellungen auf Web, Website oder Mandant Ebene *außer Kraft setzen* . Dies bedeutet auch, dass Sie die "moderne" Listen- und Bibliotheksdaten Erfahrung zu einer Unterwebsite Websites evaluieren konnte, dass die "modernen" Experience auf der Ebene der Mandanten deaktiviert, aber Listenebene bezüglich der pilot Websites aktiviert.
> - Wenn Sie manuell ausgewählt haben "klassische" (d. h., nicht aufgrund von Liste, Website, Web oder Mandanten "klassische" Erzwingung), sehen Sie den Link **Beenden klassische Erfahrung** unterhalb im linken Navigationsbereich (ab Juli 2017). Durch die Aktivierung dieser gelangen Sie wieder zur der "modernen" wünschen.
> - Wenn Sie nicht die "moderne" Erfahrung angezeigt werden erhalten sind, prüfen Sie die Cookies an SharePoint übergeben wird, da es möglich ist, dass die lehnen "modernen" Erfahrungen Cookie (Splnu mit dem Wert 0) noch vorhanden ist. Deaktivieren der Browsercookies sollte dieses Problem zu beheben.

<a name="autodetect"> </a>
## <a name="when-does-the-built-in-auto-detect-automatically-switch-rendering-back-to-classic"></a>Wenn die integrierte Auto-erkennt automatisch Switch Rendering wieder auf "Classic"?

SharePoint verwendet ein System, um automatisch zur "Classic", vorausgesetzt, dass Sie nicht die "moderne" Erfahrung für die Liste deaktivieren mithilfe der Website, Web oder Liste als Bereich überschreibt, die im vorherigen Abschnitt erläutert das Rendering einer Liste wechseln automatisch erkennen. Dies automatisch erkennen, dass das System automatisch wechseln Sie wieder zum "Classic" bei jedem SharePoint erkennt, dass die Liste die Features verwendet, die noch nicht wurden () in "Modern" unterstützt.

Im folgenden sind die Einstellungen, die als Teil des ausgewertet werden die automatische Erkennung System und die Stellen Sie der Liste "klassische" zu rendern:

- Wenn die angeforderten Liste Formularseite NULL oder mehr als einen Webpart davon aufweist.

- (**Bis Juli 2017**) Wenn das Feature mit das Web Bereich ist "Navigation und Filtern von Metadaten" aktiviert. Wir sind [einführungsmethoden für verwaltete Metadaten Navigation-Unterstützung für "modernen" Listen und Bibliotheken](https://techcommunity.microsoft.com/t5/SharePoint-Blog/SharePoint-filters-pane-updates-filtering-and-metadata/ba-p/74162).

- Das Webpart verfügbar ist ein **XSLTListViewWebPart** (Standardmethode zum Rendern der Liste) und:
    - Es ist ein nicht standardmäßiger JSLink oder XslLink-Wert für die Webpart-Eigenschaften.
    - Die Seite wird in einem Dialogfeld angezeigt (IsDlg = 1).
    - Die Liste basiert nicht auf einem der folgenden Typen: Document Library (101), Bild-Bibliothek (109), Webseitenbibliothek (119) oder generische Liste (100). **Ab August 2017**, Ankündigungen (104) und Links (103) mit der Benutzeroberfläche der "modernen" gerendert werden.
    - Die JSLink-Eigenschaft wird auf eines der Felder zum Rendern festgelegt.
    - Eines der Felder zum Rendern vom Typ **BCS externe Daten**, **Geolocation**, **OutcomeChoice**, oder eine der Veröffentlichung Feldern Typen **Bild**, **Html**oder **von Hyperlinkübersichten**.
    - Liste bezogenen Benutzer benutzerdefinierte Aktionen, die ihre ScriptSrc-Eigenschaft festgelegt sind.

- Das Webpart verfügbar ist eine **ListFormWebPart** und: 
    - Die Seite wird in einem Dialogfeld angezeigt (IsDlg = 1). 
    - Es ist eine Formularseite "New" für eine Dokumentbibliothek.  
    - Die Felder zum Rendern sind keine der folgenden unterstützten Typen: **Anlagen**, **TaxonomyField**, **Boolean**, **Auswahl**, **Währung**, **DateTime**, **Datei**, **Suche**, **mit Mehrfachauswahl**, **MultiLine-Eigenschaft **außer wenn Append mit versionsverwaltung führt, **Zahl**, **Text**, **Benutzer**oder **Url**.

### <a name="programmatically-detect-if-your-librarylist-will-be-shown-using-modern-or-classic"></a>Programmgesteuertes erkennen Sie, ob Ihre Liste/Bibliothek angezeigt werden, mithilfe von "modernen" oder "klassische" 

Im vorherige Abschnitt erläutert die Logik hinter unserer Mechanismus automatisch erkennen, aber zum Glück ist eine einfache Möglichkeit für Sie als Entwickler zu verstehen, wie eine Liste/Bibliothek gerendert wird. Diese Informationen ist so einfach wie das Abrufen des Werts der **PageRenderType** Datei-Eigenschaft, die Sie mithilfe von CSOM oder REST abrufen können. In den folgenden Beispielen gezeigt, wie Sie zuerst die Seite geladen werden, die der Darstellung die Liste, und klicken Sie dann die **PageRenderType**abrufen:

#### <a name="csom-sample"></a>CSOM-Beispiel

```C#
using (var cc = new ClientContext(siteUrl))
{
    cc.Credentials = new SharePointOnlineCredentials(userName, password);
    
    // Load the AllItems.aspx file from the list
    File file = cc.Web.GetFileByServerRelativeUrl("/sites/dev/ECMTest/Forms/AllItems.aspx");
    cc.Load(file, f => f.PageRenderType);
    cc.ExecuteQuery();

    // Check page render type
    Console.WriteLine($"Status = {file.PageRenderType}");
}
```

<br/>

> [!NOTE]
> Die PageRenderType-Eigenschaft wurde in eingeführt [Januar 2017 CSOM Release (16.1.6112.1200)](https://dev.office.com/blogs/new-sharepoint-csom-version-released-for-Office-365-january-2017).

<br/>

#### <a name="rest-request"></a>REST-Anforderung

```Html
GET _api/web/getfilebyserverrelativeurl('/sites/dev/ECMTest/Forms/AllItems.aspx')/pageRenderType
```

Die REST-Aufrufs dient zum Abrufen der Ganzzahl, die in der folgenden Tabelle erläutert wird.

Wert | Grund
:------:|-------
0 | Undefined = 0, (es ist nicht ausreichend Informationen wissen den Renderingmodus)
1 | MultipeWePart
2 | JSLinkCustomization
3 | XslLinkCustomization
4 | NoSPList
5 | HasBusinessDataField
6 | HasTaskOutcomeField
7 | HasPublishingField
8 | HasGeolocationField
9 | HasCustomActionWithCode
10 | HasMetadataNavFeature 
11 | SpecialViewType
12 | ListTypeNoSupportForModernMode
13 | Anonymen
14 | ListSettingOff
15 | SiteSettingOff
16 | WebSettingOff
17 | TenantSettingOff
18 | CustomizedForm
19 | DocLibNewForm
20 | UnsupportedFieldTypeInForm
21 | InvalidFieldTypeInForm 
22 | InvalidControModeInForm
23 | CustomizedPage
24 | ListTemplateNotSupported
100 | Moderne


## <a name="additional-considerations"></a>Zusätzliche Überlegungen

Wir werden weitere Anpassungsoptionen für "modernen" Liste schrittweise einzuführen und Bibliothek auftritt. Dies werden mit der Veröffentlichung von SharePoint-Framework Zusatzfunktionen ausgerichtet. Derzeit keine genauen Zeitplan vorhanden ist, aber wir werden in den Artikeln "modernen" Erfahrung aktualisieren, sobald neue Funktionen freigegeben werden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Anpassen der „modernen“ Benutzeroberflächen in SharePoint Online](modern-experience-customizations.md)
- [Wechseln Sie die Standard-Erfahrung für Listen oder Dokumentbibliotheken von neuen oder klassische](https://support.office.com/en-us/article/Switch-the-default-experience-for-lists-or-document-libraries-from-new-or-classic-66dac24b-4177-4775-bf50-3d267318caa9)
- [Moderne Dokumentbibliotheken in SharePoint](https://blogs.office.com/2016/06/07/modern-document-libraries-in-sharepoint)
- [Moderne SharePoint-Listen sind hier – einschließlich Integration mit Microsoft Flow und PowerApps](https://blogs.office.com/2016/07/25/modern-sharepoint-lists-are-here-including-integration-with-microsoft-flow-and-powerapps) 
- [Unterschiede zwischen dem neuen und die klassische Authentifizierung Erfahrungen für Listen und Bibliotheken](https://support.office.com/en-us/article/Differences-between-the-new-and-classic-experiences-for-lists-and-libraries-30e1aab0-a5cc-4363-b7f2-09e2ae07d4dc?ui=en-US&rs=en-US&ad=US)
