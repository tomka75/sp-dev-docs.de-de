
# <a name="replace-an-expiring-client-secret-in-a-sharepoint-add-in"></a>Austauschen eines ablaufenden geheimen Clientschlüssels in einem SharePoint-Add-In
Erfahren Sie, wie Sie einen neuen geheimen Clientschlüssel für ein SharePoint-Add-In hinzufügen können, der bei AppRegNew.aspx registriert ist.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Geheime Clientschlüssel für SharePoint-Add-Ins, die mithilfe der AppRegNew.aspx-Seite registriert wurden, laufen nach einem Jahr ab. In diesem Artikel wird erläutert, wie Sie einen neuen geheimen Schlüssel für das Add-In hinzufügen und wie Sie einen neuen geheimen Clientschlüssel erstellen können, der drei Jahre gültig ist.
 

 **Hinweis** In diesem Artikel geht es um SharePoint-Add-Ins, die über einen Organisationskatalog verteilt und über die Seite AppRegNew.aspx registriert werden. Wenn das Add-In über das Verkäuferdashboard registriert ist, finden Sie weitere Informationen unter [Erstellen oder Aktualisieren von Client-IDs und geheimen Clientschlüsseln im Verkäuferdashboard](https://dev.office.com/officestore/docs/create-or-update-client-ids-and-secrets#bk_update).
 


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
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Sign -Value $newClientSecret
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Verify -Value $newClientSecret
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Password -Usage Verify -Value $newClientSecret
$newClientSecret
```

3. Der neue geheime Clientschlüssel wird in der Windows PowerShell -Konsole angezeigt. Kopieren Sie ihn in eine Textdatei. Sie benötigen ihn in der nächsten Prozedur.
    
 

 **Tipp** Standardmäßig ist der geheime Schlüssel des Add-Ins ein Jahr gültig. Sie können diesen Zeitraum verkürzen oder verlängern (bis auf maximal drei Jahre), indem Sie den Parameter **-EndDate** für die drei Aufrufe des Cmdlets **New-MsolServicePrincipalCredential** verwenden. Der Wert des Parameters muss ein [DateTime](http://msdn2.microsoft.com/EN-US/library/03ybds8y)-Objekt sein, das nicht mehr als drei Jahre nach **DateTime.Now** liegt.
 


## <a name="update-the-remote-web-application-in-visual-studio-to-use-the-new-secret"></a>Aktualisieren der Remote-Webanwendung in Visual Studio zum Verwenden des neuen geheimen Schlüssels


 **Wichtig** Wenn Ihr Add-In ursprünglich mit einer Vorabversion der Microsoft Office Developer Tools für Visual Studio erstellt wurde, enthält es möglicherweise eine veraltete Version der Datei TokenHelper.cs (oder TokenHelper.vb). Wenn die Datei die Zeichenfolge „secondaryClientSecret" nicht enthält, ist sie veraltet und muss ausgetauscht werden, bevor Sie die Webanwendung durch einen neuen geheimen Schlüssel aktualisieren können. Um eine Kopie einer endgültigen Version der Datei abzurufen, benötigen Sie Visual Studio 2012 oder höher. Erstellen Sie ein neues SharePoint-Add-In-Projekt in Visual Studio. Kopieren Sie die TokenHelper-Datei in das Webanwendungsprojekt Ihres SharePoint-Add-Ins. 
 


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

> **Hinweis** Wenn Sie diesen Vorgang das erste Mal ausführen, gibt es zu diesem Zeitpunkt noch keinen **SecondaryClientSecret**-Eigenschaftseintrag in der Konfigurationsdatei. Wenn Sie das Verfahren jedoch für beim Ablauf eines nachfolgenden geheimen Clientschlüssels durchführen (zweiter oder dritter), ist die Eigenschaft **SecondaryClientSecret** bereits vorhanden und enthält den ursprünglichen bzw. bereits vor einiger Zeit abgelaufenen alten geheimen Clientschlüssel. Löschen Sie in diesem Fall zunächst die **SecondaryClientSecret**-Eigenschaft, bevor Sie **ClientSecret** umbenennen.

3. Fügen Sie einen neuen **ClientSecret**-Schlüssel hinzu, und übergeben Sie den neuen geheimen Clientschlüssel. Ihr Markup sollte wie folgt aussehen:
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your new secret here" />
  <add key="SecondaryClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>
```

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
    
     **Hinweis:** Die **clientId** muss der abgelaufenen **clientId** entsprechen. Es wird empfohlen, alle Schlüssel für diese **clientId** zu löschen, sowohl die abgelaufenen als auch die noch nicht abgelaufenen.
    


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


#### <a name="other-resources"></a>Sonstige Ressourcen


 
 [Vom Anbieter gehostete fällt bei SPO aus](http://blogs.technet.com/b/sharepointdevelopersupport/archive/2015/03/11/provider-hosted-app-fails-on-spo.aspx)
