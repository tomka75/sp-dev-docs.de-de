---
title: Registrieren von SharePoint 2013-Add-Ins
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 037e8ea5ca0ca79a1e3144c7cf415279db4a6347
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="register-sharepoint-add-ins-2013"></a>Registrieren von SharePoint 2013-Add-Ins
Registrieren Sie Ihre SharePoint-Add-Ins in Azure ACS mithilfe von Visual Studio, dem Verkäuferdashboard oder einer AppRegNew.aspx-Seite, und rufen Sie Registrierungsinformationen ab.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 

Damit die Remotekomponenten eines vom Anbieter gehosteten SharePoint-Add-Ins mit SharePoint über OAuth interagieren können, muss das Add-In zunächst beim cloudbasierten Dienst [Azure ACS](https://msdn.microsoft.com/de-DE/library/azure/gg429788.aspx) sowie beim SharePoint App-Verwaltungsdienst der Mandantschaft oder der Farm registriert werden (Er wird als „App-Verwaltungsdienst“ bezeichnet, da SharePoint-Add-Ins ursprünglich „Apps für SharePoint“ hießen).
 

 **Hinweis** Dies ist für von SharePoint gehostete Add-Ins nicht erforderlich.
 

Um das Add-In bei Azure ACS zu registrieren, geben Sie die folgenden Informationen ein:
 

- Eine GUID für das Add-In, die als Client-ID bezeichnet wird.
    
 
- Ein Kennwort für das Add-In, das als geheimer Clientschlüssel bezeichnet wird.
    
 
- Ein Anzeigename für das Add-In, der auf der Zustimmungsseite verwendet wird, auf der der Benutzer aufgefordert wird, dem Add-In zu vertrauen.
    
 
- Eine URL für die Domäne, in der das Remote-Add-In gehostet wird.
    
 
- Eine Umleitungs-URL.
    
 
Nachdem Sie das Add-In registriert haben, verfügt es über eine Add-In-Identität und ist ein *Sicherheitsprinzipal*, der als Add-In-Prinzipal bezeichnet wird. Wenn Sie das Add-In installieren, können SharePoint-Administratoren Informationen zum jeweiligen Add-In-Prinzipal abrufen.
 
Wenn ein Benutzer zum ersten Mal Add-In-Berechtigungen zum Zugreifen auf SharePoint-Ressourcen gewährt (dies kann entweder während der Installation oder zur Laufzeit erfolgen, abhängig vom Design des Add-Ins), erhält SharePoint Informationen über das Add-In von Azure ACS. SharePoint speichert diese Informationen dann in der Datenbank des App-Verwaltungsdiensts in der SharePoint-Mandantschaft oder -Farm. Der geheime Clientschlüssel wird nur mit Azure ACS gespeichert. SharePoint ist das Geheimnis des Add-Ins niemals bekannt. Der Inhaltsdatenbankdienst und andere Komponenten, wie z. B. der Benutzerprofildienst, können den Anzeigenamen und andere grundlegende Informationen über das Add-In direkt vom freigegebenen App-Verwaltungsdienst abrufen. Weitere Informationen finden Sie unter [Abrufen von Informationen zur Add-In-Registrierung und zum Add-In-Prinzipal ](register-sharepoint-add-ins.md#Retrieve) in diesem Artikel.
 

 **Hinweis** In diesem Artikel wird davon ausgegangen, dass Sie mit den grundlegenden Konzepten und Prinzipien des OAuth 2.0-Frameworks vertraut sind. Weitere Informationen finden Sie unter [OAuth.net](http://oauth.net/) und [Web-Autorisierungsprotokoll (oauth)](http://datatracker.ietf.org/doc/active/).
 


## <a name="register-your-sharepoint-add-in-in-azure-acs"></a>Registrieren Ihres SharePoint-Add-Ins bei Azure ACS

Es gibt drei Möglichkeiten zum Registrieren eines Add-Ins. Welche Methode Sie auswählen, hängt davon ab, an welcher Stelle des Add-In-Entwicklungslebenszyklus Sie sich befinden, sowie von der Architektur Ihres Add-Ins und dem geplanten Markteinführungsverfahren.
 

 


|**Registrierungsmethode**|**Details**|
|:-----|:-----|
|Verwenden von Visual Studio und Microsoft Office Developer Tools für Visual Studio zum Erstellen einer temporären Add-In-Identität|Der Assistent der Office Developer Tools für Visual Studio erstellt eine temporäre Registrierung für Ihr Add-In bei ACS und beim App-Verwaltungsdienst Ihrer SharePoint-Testwebsite. Wenn Sie das Add-In in Visual Studio ausführen (F5), wird diese Identität verwendet. Die Tools fügen außerdem die Client-ID und den geheimen Clientschlüssel in die Dateien „web.config“ und „AppManifest.xml“ ein. Wenn Sie Ihr Add-In veröffentlichen möchten, können Sie den Visual Studio-Veröffentlichungs-Assistenten verwenden, um zum Verkäuferdashboard zu wechseln und das Add-In zu registrieren. Wenn Sie Ihre SharePoint-Add-Ins nicht im Office Store vermarkten, verwenden Sie „AppRegNew.aspx“ für die Registrierung. (Die genauen Schritte finden Sie unten.) **Hinweis** Wenn das Add-In die Berechtigung zum Zugreifen auf SharePoint-Ressourcen dynamisch zur Laufzeit anfordert anstatt bei der Add-In-Installation, können Sie Visual Studio nicht zum Erstellen von Add-In-Identitäten verwenden. |
|Registrieren des Add-Ins über das Verkäuferdashboard.|Wenn Sie Ihr Add-In in mehreren SharePoint-Mandanten oder -Farmen verwenden möchten, verwenden Sie das Verkäuferdashboard zum Registrieren des Add-Ins, unabhängig davon, ob Sie es im Office Store vermarkten oder über den Add-In-Katalog zur Verfügung stellen möchten. Bei der Registrierung im Verkäuferdashboard können Sie Ihr Add-In mit einer mehrinstanzfähigen Architektur entwerfen, ohne dass Mandanten- oder Farmadministratoren es separat registrieren müssen. Wenn Sie beabsichtigen, Ihr Add-In im Office Store zu veröffentlichen, müssen Sie das Verkäuferdashboard zum Registrieren des Add-Ins verwenden. Sie müssen nicht den Store verwenden, um ein Add-In zu veröffentlichen, das beim Verkäuferdashboard registriert ist. Weitere Informationen finden Sie unter [Erstellen oder Aktualisieren von Client-IDs und geheimen Clientschlüsseln im Verkäuferdashboard](http://msdn.microsoft.com/library/create-or-update-client-ids-and-secrets-in-the-seller-dashboard%28Office.15%29.aspx).|
|Verwenden der Seite „AppRegNew.aspx“|Verwenden Sie das AppRegNew-Formular zum Registrieren Ihres SharePoint-Add-Ins, wenn Sie das Add-In nur in einem Mandanten oder einer Farm verwenden möchten. Beispiel: Wenn Sie Add-Ins für eine einzelne Organisation erstellen und sie über den Add-In-Katalog der Organisation verteilen werden, können Sie die Seite „AppRegNew.aspx“ jeder Website in einem Mandanten oder einer Farm verwenden, um das Add-In zu registrieren. Add-Ins, die bei „AppRegNew.aspx“ registriert sind, können nicht im Office Store veröffentlicht werden. Für Add-Ins, die im Office Store veröffentlicht werden sollen, müssen Sie eine Identität aus dem Verkäuferdashboard abrufen.|

### <a name="to-register-by-using-appregnewaspx"></a>So führen Sie die Registrierung mit „AppRegNew.aspx“ durch


1.  Navigieren Sie zu `http://` *<SharePointWebsite>* `/_layouts/15/AppRegNew.aspx` im Mandanten oder der Farm.
    
    **AppRegNew-Seitenformular**

 

  ![Das Formular auf der Seite „AppRegNew“ mit Feldern für die Client-ID, den geheimen Clientschlüssel, den Titel, die App-Domäne &amp; die Umleitungs-URL. Neben den ersten beiden werden Schaltflächen namens „Generieren“ angezeigt. In der Ecke befinden sich die Schaltflächen „Erstellen“ und „Abbrechen“.](../images/9a38d876-2189-418c-9314-ae493a4cab61.PNG)
 

 

 
2. Geben Sie Werte für die folgenden Formularfelder ein:
    
      -  **Add-In-ID**: Die Add-In-ID, die auch als Client-ID bezeichnet wird, ist eine GUID, die generiert (wenn Sie **Generieren** wählen) oder in AppRegNew.aspx eingefügt werden kann. Der Wert muss für jedes Add-In eindeutig sein und *kleingeschrieben*  werden.
    
 
  -  **Geheimer Add-In-Schlüssel**: Der geheime Add-In-Schlüssel, der auch als geheimer Clientschlüssel bezeichnet wird, ist eine opake Zeichenkette. Er wird auf der Seite AppRegNew.aspx über die Schaltfläche **Generieren** generiert. Im Folgenden sehen Sie ein Beispiel für einen geheimen Add-In-Schlüssel: **xvVpG0AgVIJfch6ldu4dLUlcZyysmGqBRbpFDu6AfJw=**.
    
     **Wichtig** Geheime Add-In-Schlüssel laufen ab. Wenn Sie das Add-In im Verkäuferdashboard registrieren, können Sie die Ablaufdauer auf bis zu 3 Jahre festlegen. Im Dashboard können Sie außerdem neue geheime Schlüssel hinzufügen, wenn sich die alten ihrem Ablaufdatum nähern. Der neue geheime Schlüssel wird in allen Instanzen des Add-Ins aktiviert. Wenn Sie das Add-In bei AppRegNew.aspx registrieren, läuft der geheime Schlüssel nach einem Jahr ab. Ausführliche Informationen finden Sie unter [Austauschen eines ablaufenden geheimen Clientschlüssels in einem SharePoint-Add-In](replace-an-expiring-client-secret-in-a-sharepoint-add-in.md).
  -  **Titel**: Ein benutzerfreundlicher Titel, zum BeispielContoso-Fotodruck-Add-In. Benutzer werden aufgefordert, dem Add-In die Berechtigungen zu gewähren oder zu verweigern, die das Add-In anfordert. Dieser Titel wird als Name des Add-Ins bei der Zustimmungseingabeaufforderung angezeigt. 
    
 
  -  **Add-In-Domäne**: Der Hostname der Remotekomponente des SharePoint-Add-In. Wenn die Remoteanwendung nicht Port 443 verwendet, muss die Add-In-Domäne auch die Portnummer enthalten. Die Add-In-Domäne muss mit den URL-Bindungen übereinstimmen, die Sie für Ihre Webanwendung verwenden. Geben Sie in diesem Wert kein Protokoll („https:") oder „/"-Zeichen an. (Wenn Ihr Webanwendungshost einen DNS-CNAME-Aliasnamen verwendet, benutzen Sie den Alias.) Nachfolgend sind einige Beispiele aufgeführt:
    
      - www.contoso.com:3333
    
 
  - www.fabrikam.com
    
 
  -  **Umleitungs-URI:**: Der Endpunkt in Ihrer Remoteanwendung oder dem Dienst, an die bzw. den ACS einen Authentifizierungscode sendet. Genau genommen verwenden SharePoint-Add-Ins diesen Wert nicht. Der Umleitungs-URI ist für Webanwendungen erforderlich, die außerhalb von SharePoint gestartet werden und den [Authentifizierungscodeablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) verwenden, um autorisierten Zugriff auf SharePoint-Daten zu erhalten. Der Umleitungs-URI wird für echte SharePoint-Add-Ins ignoriert (die von SharePoint gestartet werden und den [Kontexttokenablauf](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) verwenden). Der Umleitungs-URI ist in der Regel dieselbe Seite, Controllermethode oder Webdienstmethode, die den Authentifizierungscode von ACS angefordert hat, es kann sich jedoch auch um einen anderen Endpunkt handeln. Der Endpunkt muss über Logik verfügen, die den Autorisierungscode aus der von ACS gesendeten HTTP-Antwort abruft und dann diesen Code verwendet, um ein Zugriffs- und Aktualisierungstoken anzufordern. Weitere Informationen finden Sie unter [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](authorization-code-oauth-flow-for-sharepoint-add-ins.md). Das Formular erfordert, dass Sie auch für echte SharePoint-Add-Ins einen gültigen Wert eingeben, obwohl er nicht verwendet wird.
    
    Der Wert muss eine vollständige Endpunkt-URL, einschließlich des Protokolls sein; dieses muss *HTTPS* sein. Beispiel:
    
      - https://www.contoso.com/Default.aspx
    
 
  - https://www.fabrikam.com/RedirectAccept.aspx
    
 
  - https://www.northwindtraders.com/home/index
    
 
  - https://adventureworks.com/vacationdata.svc
    
 
3. Wählen Sie im Formular **Erstellen** aus. Die Seite wird neu geladen und zeigt eine Bestätigung der von Ihnen eingegebenen Werte an. Zeichnen Sie diese Werte in einer Form auf, die einfach kopiert und eingefügt werden kann. Sie müssen die Werte in die Dateien „web.config“ und „AppManifest.xml“ oder den Visual Studio-Assistenten zum **Veröffentlichen** eingeben.
    
 
Unabhängig davon, wie Sie Ihr SharePoint-Add-In registrieren, wenn Sie bereit sind, das Add-In für Staging oder Produktion bereitzustellen, müssen Sie  [Eingeben der Registrierungswerte in die Dateien web.config und AppManifest.xml](#EditConfigFiles). Wenn Sie Visual Studio verwenden, übernehmen die Microsoft Office-Entwicklertools für Visual Studio diese Konfiguration für Sie.
 

 

## <a name="enter-the-registration-values-into-the-webconfig-and-appmanifestxml-files"></a>Eingeben der Registrierungswerte in die Dateien „web.config“ und „AppManifest.xml“
<a name="EditConfigFiles"> </a>

Bevor Sie das SharePoint-Add-In verpacken und seine Remotekomponenten bereitstellen, geben Sie einige der Registrierungswerte in die Dateien „AppManifest.xml" und „web.config" ein.
 

 

 **Tipp** Wenn Sie Ihr SharePoint-Add-In mithilfe des Visual Studio-Veröffentlichungs-Assistenten veröffentlichen, werden Sie von Visual Studio während des Veröffentlichungsprozesses zur Eingabe einer Client-ID und eines geheimen Clientschlüssels aufgefordert. Diese Informationen werden für Sie jeweils an der richtigen Stelle eingefügt.
 


1. Geben Sie im Visual Studio-Projekt in der Datei „Web.config“ den Add-In-ID-Wert als **ClientId**-Wert ein (der den temporären Wert ersetzt, den die Tools eingegeben haben).
    
     **Wichtig** Alle Buchstaben in der Client-ID-GUID müssen kleingeschrieben sein.

    Es folgt ein Beispiel.
    


```XML
  <appSettings>
  <add key="ClientId" value="a044e184-7de2-4d05-aacf-52118008c44e " />
   .  .  .
</appSettings>
```

2. Geben Sie den Wert für den geheimen Add-In-Schlüssel als **ClientSecret**-Wert ein (der den temporären Wert ersetzt, den die Tools eingegeben haben).
    
    Nachfolgend sehen Sie ein Beispiel für die Verwendung der Werte in der Datei „Web.config“ einer Webanwendung.
    


```XML
  <appSettings>
  <add key="ClientId" value="a044e184-7de2-4d05-aacf-52118008c44e " />
  <add key="ClientSecret" value="l0z/8TzWN0yQBzMBSEZtYts2Vt3Eo/oE3rfCdPaogKQ= " />
</appSettings>
```

3. Geben Sie im Visual Studio-Projekt in der Datei „AppManifest.xml“ den Add-In-ID-Wert als **ClientId** *in Kleinbuchstaben* ein.
    
     **Hinweis** Das Add-In-Manifest gilt nicht für Webanwendungen, bei denen die Berechtigung für den Zugriff auf SharePoint-Ressourcen spontan abgerufen wird. Diese sind eigentlich keine „SharePoint-Add-Ins“. Sie werden nicht in SharePoint installiert und haben kein Add-In-Manifest. Weitere Informationen finden Sie unter [OAuth-Ablauf mit Authentifizierungscode für SharePoint-Add-Ins](authorization-code-oauth-flow-for-sharepoint-add-ins.md).

    Das folgende Beispiel veranschaulicht die Verwendung des **ClientId**-Werts in der Datei „AppManifest.xml“.
    


```XML
  <AppPrincipal>
  <RemoteWebApplication ClientId="a044e184-7de2-4d05-aacf-52118008c44e "/>
</AppPrincipal>
```

4. Die Office Developer Tools für Visual Studio verwenden das Token `~remoteAppUrl` im **StartPage**-Element (z. B. `<StartPage>~remoteAppUrl/Pages/Default.aspx?{StandardTokens}</StartPage>`). Dieses Token löst sich in die URL der Remotekomponente auf, wenn Sie den **Veröffentlichungs**-Assistenten in Visual Studio verwenden. Wenn Sie den Assistenten nicht verwenden (oder wenn Sie ihn verwenden, die Remotekomponente jedoch in Azure veröffentlichen), müssen Sie das Token manuell durch den Wert **Add-In-Domäne** ersetzen, den Sie bei der Registrierung des Add-Ins verwendet haben. Verwenden Sie dabei *exakt* denselben Wert, einschließlich Portnummer (falls vorhanden), es sei denn, dass Sie auch das HTTPS-Protokoll einschließen. Nachfolgend ist ein Beispiel hierfür aufgeführt.
    
```XML
  <StartPage>https://www.contoso.com/Pages/Default.aspx?{StandardTokens}</StartPage>
```

5. Ziehen Sie die Verwendung desselben Werts für das **Title**-Element in der AppManifest.xml-Datei in Betracht, den Sie für das Feld **Titel** in AppRegNew.aspx verwendet haben. Der Wert für das **Title**-Element ist der Name des Add-Ins, den Benutzer nach der Installation des Add-Ins sehen. Für Benutzer ist es möglicherweise verwirrend, wenn das Add-In im Zustimmungsdialogfeld einen anderen Namen hat als in der SharePoint-Benutzeroberfläche.
    
    Das folgende Beispiel zeigt diese Werte im Add-In-Manifest.
    


```XML
  <Properties>
  <Title>Contoso photo printing app</Title>
  <StartPage>https://www.contoso.com/Pages/Default.aspx?{StandardTokens}</StartPage>
</Properties>
```


## <a name="use-the-redirect-url-in-an-add-in-that-asks-for-permissions-on-the-fly"></a>Verwenden der Umleitungs-URL in einem Add-In, das Berechtigungen im laufenden Betrieb anfordert
<a name="UseRedirectUrl"> </a>

Wenn Ihre Webanwendung außerhalb von SharePoint gestartet wird (und daher kein wirkliches SharePoint-Add-In ist), muss sie so ausgelegt sein, dass sie zur Laufzeit Berechtigungen von SharePoint anfordert. Darüber hinaus muss sie Code enthalten, der den Umleitungs-URI zusammen mit anderen Informationen verwendet, um ein Zugriffstoken von ACS abzurufen. Suchen Sie die Stelle, an der dieser URI festgelegt ist, und verwenden Sie  *exakt*  den Wert, den Sie für das Feld **Umleitungs-URI** auf der Seite „AppRegNew.aspx" oder im Verkäuferdashboard verwendet haben. Dieser kann sich in einer Codedatei oder einer Konfigurationsdatei befinden.
 

 

## <a name="retrieve-add-in-registration-and-add-in-principal-information"></a>Abrufen von Informationen zu Add-In-Registrierung und Add-In-Prinzipal
<a name="Retrieve"> </a>

Sie können die Informationen zu Add-In-Registrierung und Add-In-Prinzipal für Ihre Add-Ins abrufen, die Sie unter SharePoint installiert oder registriert haben. 
 

 
Um nach Registrierungsinformationen für ein Add-In zu suchen, das Sie registriert haben, wechseln Sie zu `http://` *<SharePointWebsite>* `/_layouts/15/AppInv.aspx`.
 

 
Zum Nachschlagen benötigen Sie die Client-ID (auch als Add-In-ID bezeichnet), die Sie bei der Registrierung des Add-Ins verwendet haben. Der Nachschlagevorgang gibt für die entsprechende Client-ID die folgenden Informationen zurück:
 

 

- Titel
    
 
- Add-In-Domäne
    
 
- Umleitungs-URL (entspricht dem Umleitungs-URI)
    
 
Der Nachschlagevorgang gibt nicht den Wert des geheimen Add-In-Schlüssels zurück.
 

 
Um eine Liste der registrierten Add-In-Prinzipale anzuzeigen, wechseln Sie zu:
 

 
 `http://` *<SharePointWebsite>*  `/_layouts/15/AppPrincipals.aspx`
 

 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="AR"> </a>


-  [Autorisierung und Authentifizierung für Add-Ins in SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md)
    
 
-  [Drei Autorisierungssysteme für SharePoint-Add-Ins](three-authorization-systems-for-sharepoint-add-ins.md)
    
 
-  [Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
