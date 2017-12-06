---
title: "Austauschen eines ablaufenden geheimen Clientschlüssels in einem Add-In für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 4c5295ea0cd345f01264f86c6d84230029c6ace8
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="replace-an-expiring-client-secret-in-a-sharepoint-add-in"></a>Austauschen eines ablaufenden geheimen Clientschlüssels in einem SharePoint-Add-In
Erfahren Sie, wie Sie einen neuen geheimen Clientschlüssel für ein SharePoint-Add-In hinzufügen können, der bei AppRegNew.aspx registriert ist.
 

> [!NOTE]
> Der Name "Apps für SharePoint" wird in "SharePoint-Add-Ins" geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Tools für Visual Studio möglicherweise weiterhin der Begriff "Apps für SharePoint" verwendet. Weitere Einzelheiten finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 

Geheime Clientschlüssel für SharePoint-Add-Ins, die mithilfe der AppRegNew.aspx-Seite registriert wurden, laufen nach einem Jahr ab. In diesem Artikel wird erläutert, wie Sie einen neuen geheimen Schlüssel für das Add-In hinzufügen und wie Sie einen neuen geheimen Clientschlüssel erstellen können, der drei Jahre gültig ist.
 

> [!NOTE]
> Dieser Artikel enthält Informationen zu SharePoint-Add-Ins, die über einen Organisationskatalog verteilt werden und bei der Seite "AppRegNew.aspx" registriert sind. Wenn das Add-In auf dem Verkäuferdashboard registriert ist, finden Sie weitere Informationen unter [Erstellen oder Aktualisieren von Client-IDs und geheimen Clientschlüsseln im Verkäuferdashboard](https://dev.office.com/officestore/docs/create-or-update-client-ids-and-secrets#bk_update).
 


## <a name="prerequisites-for-refreshing-a-client-secret"></a>Voraussetzungen zum Aktualisieren eines geheimen Clientschlüssels

Stellen Sie vor Beginn Folgendes sicher:
 

 

-  [Der Microsoft Online Services-Anmeldeassistent](http://www.microsoft.com/download/details.aspx?id=39267) ist auf dem Entwicklungscomputer installiert.
    
 
- Das Microsoft Online Services PowerShell-Modul ( [32-Bit](http://go.microsoft.com/fwlink/p/?linkid=236298);  [64-Bit](http://go.microsoft.com/fwlink/p/?linkid=236297)) wird auf dem Entwicklungscomputer installiert.
    
 
- Sie sind der Mandantenadministrator für den Office 365-Mandanten (oder ein Farmadministrator in der Farm), auf dem das Add-In mit der AppRegNew.aspx-Seite registriert wurde.
    
 

## <a name="find-out-the-expiration-dates-of-the-sharepoint-add-ins-installed-to-the-office-365-tenancy"></a>Ermitteln der Ablaufdaten des auf dem Office 365-Mandanten installierten SharePoint-Add-Inss


 

 

1. Öffnen Sie Windows PowerShell und führen Sie folgendes Cmdlet aus:
    
```
  Connect-MsolService

```

2. Geben Sie bei der Anmeldeaufforderung die Mandantenadministrator-Anmeldeinformationen (oder Farmadministrator) für die Office 365-Mandantschaft oder die Farm ein, auf der das Add-In mit der AppRegNew.aspx-Seite registriert wurde.
    
 
3. Generieren Sie einen Bericht mit den folgenden Zeilen, in denen das jeweilige Add-In und das Datum, an dem ihr geheimer Schlüssel abläuft, aufgeführt sind. Beachten Sie zu diesem Code Folgendes:
    
      - Zunächst werden eigene Anwendungen von Microsoft und Add-Ins, die noch entwickelt werden, herausgefiltert.
    
 
  - Aus dem Rest werden Nicht-SharePoint-Add.Ins und Add-Ins, die asymmetrische Schlüssel verwenden, z. B. Workflows, herausgefiltert.
    
 

```
  $applist = Get-MsolServicePrincipal -all  |Where-Object -FilterScript { ($_.DisplayName -notlike "*Microsoft*") -and ($_.DisplayName -notlike "autohost*") -and  ($_.ServicePrincipalNames -notlike "*localhost*") }

foreach ($appentry in $applist)
{
    $principalId = $appentry.AppPrincipalId
    $principalName = $appentry.DisplayName
    
    Get-MsolServicePrincipalCredential -AppPrincipalId $principalId -ReturnKeyValues $false | Where-Object { ($_.Type -ne "Other") -and ($_.Type -ne "Asymmetric") }
    
     $date = get-date
     Write-Host "$principalName;$principalId;$appentry.KeyId;$appentry.type;$date;$appentry.Usage"

}  > c:\temp\appsec.txt
```

4. Öffnen Sie die Datei „C:\temp\appsec.txt“, um den Bericht anzuzeigen. Lassen Sie das Windows PowerShell-Fenster für die nächste Prozedur geöffnet, wenn sich das Ablaufdatum für einen der geheimen Schlüssel nähert.
    
 

## <a name="generate-a-new-secret"></a>Generieren eines neuen geheimen Schlüssels


 

 

1. Erstellen Sie eine Client-ID-Variable mit folgender Zeile, und verwenden Sie dafür die Client-ID des SharePoint-Add-Ins als Parameter.
    
```
  $clientId = 'client id of the add-in'

```

2. Generieren Sie mit den folgenden Zeilen einen neuen geheimen Clientschlüssel:
    
```
  $bytes = New-Object Byte[] 32
$rand = [System.Security.Cryptography.RandomNumberGenerator]::Create()
$rand.GetBytes($bytes)
$rand.Dispose()
$newClientSecret = [System.Convert]::ToBase64String($bytes)
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Sign -Value $newClientSecret -StartDate (Get-Date) -EndDate (Get-Date).AddYears(1)
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Verify -Value $newClientSecret -StartDate (Get-Date) -EndDate (Get-Date).AddYears(1)
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Password -Usage Verify -Value $newClientSecret -StartDate (Get-Date) -EndDate (Get-Date).AddYears(1)
$newClientSecret
```

3. Der neue geheime Clientschlüssel wird in der Windows PowerShell -Konsole angezeigt. Kopieren Sie ihn in eine Textdatei. Sie benötigen ihn in der nächsten Prozedur.
    
 

> [!TIP]
> Standardmäßig sind geheime Add-In-Schlüssel ein Jahr gültig. Sie können diesen Zeitraum mit dem Parameter **-EndDate** der drei Aufrufe des Cmdlets **New-MsolServicePrincipalCredential** verkürzen oder verlängern (bis maximal drei Jahre). Der Wert des Parameters muss ein [DateTime](http://msdn2.microsoft.com/de-DE/library/03ybds8y)-Objekt sein, das maximal auf einen Zeitraum von drei Jahren ab **DateTime.Now** eingestellt werden darf.
 
## <a name="update-the-remote-web-application-in-visual-studio-to-use-the-new-secret"></a>Aktualisieren der Remote-Webanwendung in Visual Studio zum Verwenden des neuen geheimen Schlüssels


> [!IMPORTANT]
>  Wenn das Add-In ursprünglich mit einer Vorabversion des Microsoft Office Developer Tools für Visual Studio erstellt wurde, kann es eine veraltete Version der Datei TokenHelper.cs (oder .vb) enthalten. Wenn die Datei nicht die Zeichenfolge "SecondaryClientSecret" enthält, ist sie veraltet und muss ersetzt werden, bevor Sie die Webanwendung mit einem neuen Schlüssel aktualisieren können. Sie benötigen Visual Studio 2012 oder höher, um eine Kopie der Veröffentlichungsversion der Datei erhalten zu können. Erstellen Sie ein neues SharePoint-Add-In-Projekt in Visual Studio. Kopieren Sie die darin enthaltene Datei TokenHelper in das Webanwendungsprojekt Ihrer SharePoint-Add-In. 
 


1. Öffnen Sie das SharePoint-Add-In-Projekt in Visual Studio, und öffnen Sie die Datei „web.config“ für das Webanwendungsprojekt. Im Abschnitt **appSettings** finden Sie Schlüssel für die Client-ID und den geheimen Clientschlüssel. Beispiel:
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>

```

2. Ändern Sie den Namen des **ClientSecret**-Schlüssels in „SecondaryClientSecret“ wie im folgenden Beispiel:
    
```XML
  <add key="SecondaryClientSecret" value="your old secret here" />
```

> [!NOTE]
> Wenn Sie dieses Verfahren zum ersten Mal durchführen, ist zu diesem Zeitpunkt in der Konfigurationsdatei kein **SecondaryClientSecret**-Eigenschaftseintrag vorhanden. Wenn Sie das Verfahren für einen nachfolgenden (zweiten oder dritten) Ablauf eines geheimen Clientschlüssels durchführen, ist die Eigenschaft **SecondaryClientSecret** bereits vorhanden und enthält den ursprünglichen oder noch älteren abgelaufenen alten Schlüssel . Löschen Sie in diesem Fall zuerst die Eigenschaft **SecondaryClientSecret**, bevor Sie **ClientSecret** umbenennen.

3. Fügen Sie einen neuen **ClientSecret**-Schlüssel hinzu, und übergeben Sie den neuen geheimen Clientschlüssel. Ihr Markup sollte wie folgt aussehen:
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your new secret here" />
  <add key="SecondaryClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>
```

> [!IMPORTANT]
> Sie können den neu generierten geheimen Clientschlüssel erst verwenden, nachdem der aktuelle geheime Clientschlüssel abgelaufen ist. Daher ist es nicht möglich, den Client-ID-Schlüssel ohne den vorhandenen SecondaryClientSecret-Schlüssel in den neuen geheimen Clientschlüssel zu ändern. Sie müssen die Verfahrensweise dieses Artikels befolgen und warten, bis der vorherige geheime Clientschlüssel abgelaufen ist. Dann können Sie den SecondaryClientSecret entfernen, wenn Sie möchten.

4. Wenn Sie zu einer neuen „TokenHelper“-Datei gewechselt haben, müssen Sie das Projekt neu erstellen.
    
 
5. Veröffentlichen Sie die Webanwendung erneut.
    
 

## <a name="create-a-client-secret-that-is-valid-for-three-years"></a>Erstellen eines geheimen Clientschlüssels, der drei Jahre gültig ist

Für abgelaufene geheime Clientschlüssel müssen Sie zunächst alle abgelaufenen Schlüssel für eine bestimmte **ClientId** löschen. Sie erstellen dann einen neuen mit MSOPowerShell, warten mindestens 24 Stunden, und testen die App mit der neuen **ClientId** und dem neuen **ClientSecret**-Schlüssel.
 

 

1. Stellen Sie eine Verbindung mit MSOnline anhand des Mandanten-Admininistratorbenutzers und dem unten aufgeführten Markup her, indem Sie SharePoint Windows PowerShell verwenden.
    
```
  import-module MSOnline
$msolcred = get-credential
connect-msolservice -credential $msolcred

```

2. Rufen Sie **ServicePrincipals** und die Schlüssel ab. Durch das Drucken von **$keys** werden drei Datensätze zurückgegeben. Ersetzen Sie jede **KeyId** unter *KeyId1* , *KeyId2* und *KeyId3*. Außerdem wird Ihnen das **EndDate** der einzelnen Schlüssel angezeigt. Vergewissern Sie sich, dass dort die abgelaufenen Schlüssel angezeigt werden.
    
     >**Hinweis:** Die **clientId** muss der abgelaufenen **clientId** entsprechen. Es wird empfohlen, alle Schlüssel für diese **clientId** zu löschen, sowohl die abgelaufenen als auch die noch nicht abgelaufenen.
    


```
  $clientId = "27c5b286-62a6-45c7-beda-abbaea6eecf2"
$keys = Get-MsolServicePrincipalCredential -AppPrincipalId $clientId
Remove-MsolServicePrincipalCredential -KeyIds @("KeyId1"," KeyId2"," KeyId3") -AppPrincipalId $clientId 

```

3. Generieren Sie ein neues **ClientSecret** für diese **clientID**. Es verwendet die gleiche **clientId**, die im vorhergehenden Schritt eingerichtet wurde. Das neue **ClientSecret** ist 3 Jahre gültig.
    
```
  $bytes = New-Object Byte[] 32
$rand = [System.Security.Cryptography.RandomNumberGenerator]::Create()
$rand.GetBytes($bytes)
$rand.Dispose()
$newClientSecret = [System.Convert]::ToBase64String($bytes)
$dtStart = [System.DateTime]::Now
$dtEnd = $dtStart.AddYears(3)
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Sign -Value $newClientSecret -StartDate $dtStart  -EndDate $dtEnd
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Verify -Value $newClientSecret   -StartDate $dtStart  -EndDate $dtEnd
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Password -Usage Verify -Value $newClientSecret   -StartDate $dtStart  -EndDate $dtEnd
$newClientSecret

```

4. Kopieren Sie die Ausgabe von **$newClientSecret**.
    
 
5. Ersetzen Sie die **Web.config** durch diese **ClientId** und das **ClientSecret**. Sie benötigen nicht die **SecondaryClientSecret**-App-Einstellungen.
    
 
6. Warten Sie mindestens 24 Stunden mit dem Auffüllen des **ClientSecret** in SharePoint Office (SPO).
    
 

## <a name="see-also"></a>Siehe auch

[Vom Anbieter gehostete App fällt bei SPO aus](http://blogs.technet.com/b/sharepointdevelopersupport/archive/2015/03/11/provider-hosted-app-fails-on-spo.aspx)
