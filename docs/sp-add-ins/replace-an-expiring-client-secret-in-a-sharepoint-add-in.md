
# <a name="replace-an-expiring-client-secret-in-a-sharepoint-add-in"></a><span data-ttu-id="1abb3-101">Austauschen eines ablaufenden geheimen Clientschlüssels in einem SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="1abb3-101">Replace an expiring client secret in a SharePoint Add-in</span></span>
<span data-ttu-id="1abb3-102">Erfahren Sie, wie Sie einen neuen geheimen Clientschlüssel für ein SharePoint-Add-In hinzufügen können, der bei AppRegNew.aspx registriert ist.</span><span class="sxs-lookup"><span data-stu-id="1abb3-102">Learn how to add a new client secret for a spappsing that is registered with AppRegNew.aspx.</span></span>
 

 <span data-ttu-id="1abb3-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="1abb3-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="1abb3-p102">Geheime Clientschlüssel für SharePoint-Add-Ins, die mithilfe der AppRegNew.aspx-Seite registriert wurden, laufen nach einem Jahr ab. In diesem Artikel wird erläutert, wie Sie einen neuen geheimen Schlüssel für das Add-In hinzufügen und wie Sie einen neuen geheimen Clientschlüssel erstellen können, der drei Jahre gültig ist.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p102">Client secrets for spappplural that are registered using the AppRegNew.aspx page expire after one year. This article explains how to add a new secret for the add-in, as well as how to create a new client secret that is valid for three years.</span></span>
 

 <span data-ttu-id="1abb3-p103">**Hinweis** In diesem Artikel geht es um SharePoint-Add-Ins, die über einen Organisationskatalog verteilt und über die Seite AppRegNew.aspx registriert werden. Wenn das Add-In über das Verkäuferdashboard registriert ist, finden Sie weitere Informationen unter [Erstellen oder Aktualisieren von Client-IDs und geheimen Clientschlüsseln im Verkäuferdashboard](https://dev.office.com/officestore/docs/create-or-update-client-ids-and-secrets#bk_update).</span><span class="sxs-lookup"><span data-stu-id="1abb3-p103">**Note** This article is about SharePoint Add-ins that are distributed through an organization catalog and registered with the AppRegNew.aspx page. If the add-in is registered on the Seller Dashboard, see  [Create or update client IDs and secrets in the Seller Dashboard](https://dev.office.com/officestore/docs/create-or-update-client-ids-and-secrets#bk_update).</span></span>
 


## <a name="prerequisites-for-refreshing-a-client-secret"></a><span data-ttu-id="1abb3-110">Voraussetzungen zum Aktualisieren eines geheimen Clientschlüssels</span><span class="sxs-lookup"><span data-stu-id="1abb3-110">Prerequisites for refreshing a client secret</span></span>

<span data-ttu-id="1abb3-111">Stellen Sie vor Beginn Folgendes sicher:</span><span class="sxs-lookup"><span data-stu-id="1abb3-111">Ensure the following before you begin:</span></span>
 

 

-  <span data-ttu-id="1abb3-112">[Der Microsoft Online Services-Anmeldeassistent](http://www.microsoft.com/download/details.aspx?id=39267) ist auf dem Entwicklungscomputer installiert.</span><span class="sxs-lookup"><span data-stu-id="1abb3-112">[Microsoft Online Services Sign-In Assistant](http://www.microsoft.com/download/details.aspx?id=39267) is installed on the development computer.</span></span>
    
 
- <span data-ttu-id="1abb3-113">Das Microsoft Online Services PowerShell-Modul ( [32-Bit](http://go.microsoft.com/fwlink/p/?linkid=236298);  [64-Bit](http://go.microsoft.com/fwlink/p/?linkid=236297)) wird auf dem Entwicklungscomputer installiert.</span><span class="sxs-lookup"><span data-stu-id="1abb3-113">Microsoft Online Services PowerShell Module ( [32-bit](http://go.microsoft.com/fwlink/p/?linkid=236298);  [64-bit](http://go.microsoft.com/fwlink/p/?linkid=236297)) is installed on the development computer.</span></span>
    
 
- <span data-ttu-id="1abb3-114">Sie sind der Mandantenadministrator für den Office 365-Mandanten (oder ein Farmadministrator in der Farm), auf dem das Add-In mit der AppRegNew.aspx-Seite registriert wurde.</span><span class="sxs-lookup"><span data-stu-id="1abb3-114">You are a tenant administrator for the Office 365 tenant (or a farm administrator on the farm) where the add-in was registered with the AppRegNew.aspx page.</span></span>
    
 

## <a name="find-out-the-expiration-dates-of-the-sharepoint-add-ins-installed-to-the-office-365-tenancy"></a><span data-ttu-id="1abb3-115">Ermitteln der Ablaufdaten des auf dem Office 365-Mandanten installierten SharePoint-Add-Inss</span><span class="sxs-lookup"><span data-stu-id="1abb3-115">Find out the expiration dates of the SharePoint Add-ins installed to the Office 365 tenancy</span></span>


 

 

1. <span data-ttu-id="1abb3-116">Öffnen Sie Windows PowerShell und führen Sie folgendes Cmdlet aus:</span><span class="sxs-lookup"><span data-stu-id="1abb3-116">Open Windows PowerShell and run the following cmdlet:</span></span>
    
```
  Connect-MsolService

```

2. <span data-ttu-id="1abb3-117">Geben Sie bei der Anmeldeaufforderung die Mandantenadministrator-Anmeldeinformationen (oder Farmadministrator) für die Office 365-Mandantschaft oder die Farm ein, auf der das Add-In mit der AppRegNew.aspx-Seite registriert wurde.</span><span class="sxs-lookup"><span data-stu-id="1abb3-117">At the login prompt, enter tenant-administrator (or farm administrator) credentials for the Office 365 tenancy or farm where the add-in was registered with AppRegNew.aspx.</span></span>
    
 
3. <span data-ttu-id="1abb3-p104">Generieren Sie einen Bericht mit den folgenden Zeilen, in denen das jeweilige Add-In und das Datum, an dem ihr geheimer Schlüssel abläuft, aufgeführt sind. Beachten Sie zu diesem Code Folgendes:</span><span class="sxs-lookup"><span data-stu-id="1abb3-p104">Generate a report that lists each add-in and the date that its secret expires with the following lines. Note the following about this code:</span></span>
    
      - <span data-ttu-id="1abb3-120">Zunächst werden eigene Anwendungen von Microsoft und Add-Ins, die noch entwickelt werden, herausgefiltert.</span><span class="sxs-lookup"><span data-stu-id="1abb3-120">It first filters out Microsoft's own applications, add-ins still under development (and a now-deprecated type of add-in that was called autohosted).</span></span>
    
 
  - <span data-ttu-id="1abb3-121">Aus dem Rest werden Nicht-SharePoint-Add.Ins und Add-Ins, die asymmetrische Schlüssel verwenden, z. B. Workflows, herausgefiltert.</span><span class="sxs-lookup"><span data-stu-id="1abb3-121">From the remainder, it filters out non-SharePoint add-ins and add-ins that use asymmetric keys, like workflows.</span></span>
    
 

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

4. <span data-ttu-id="1abb3-p105">Öffnen Sie die Datei „C:\temp\appsec.txt“, um den Bericht anzuzeigen. Lassen Sie das Windows PowerShell-Fenster für die nächste Prozedur geöffnet, wenn sich das Ablaufdatum für einen der geheimen Schlüssel nähert.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p105">Open the file C:tempappsec.txt to see the report. Leave the Windows PowerShell window open for the next procedure, if any of the secrets is near to expiration.</span></span>
    
 

## <a name="generate-a-new-secret"></a><span data-ttu-id="1abb3-124">Generieren eines neuen geheimen Schlüssels</span><span class="sxs-lookup"><span data-stu-id="1abb3-124">Generate a new secret</span></span>


 

 

1. <span data-ttu-id="1abb3-125">Erstellen Sie eine Client-ID-Variable mit folgender Zeile, und verwenden Sie dafür die Client-ID des SharePoint-Add-Ins als Parameter.</span><span class="sxs-lookup"><span data-stu-id="1abb3-125">Create a client ID variable with the following line, using the client ID of the SharePoint Add-in as the parameter.</span></span>
    
```
  $clientId = 'client id of the add-in'

```

2. <span data-ttu-id="1abb3-126">Generieren Sie mit den folgenden Zeilen einen neuen geheimen Clientschlüssel:</span><span class="sxs-lookup"><span data-stu-id="1abb3-126">Generate a new client secret with the following lines:</span></span>
    
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

3. <span data-ttu-id="1abb3-p106">Der neue geheime Clientschlüssel wird in der Windows PowerShell -Konsole angezeigt. Kopieren Sie ihn in eine Textdatei. Sie benötigen ihn in der nächsten Prozedur.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p106">The new client secret will appear on the Windows PowerShell console. Copy it to a text file. You use it in the next procedure.</span></span>
    
 

 <span data-ttu-id="1abb3-p107">**Tipp** Standardmäßig ist der geheime Schlüssel des Add-Ins ein Jahr gültig. Sie können diesen Zeitraum verkürzen oder verlängern (bis auf maximal drei Jahre), indem Sie den Parameter **-EndDate** für die drei Aufrufe des Cmdlets **New-MsolServicePrincipalCredential** verwenden. Der Wert des Parameters muss ein [DateTime](http://msdn2.microsoft.com/EN-US/library/03ybds8y)-Objekt sein, das nicht mehr als drei Jahre nach **DateTime.Now** liegt.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p107">**TIP** By default, the add-in secret lasts one year. You can set this to a shorter or longer (up to 3 years maximum) by using the **-EndDate** parameter on the three calls of the **New-MsolServicePrincipalCredential** cmdlet. The value of the parameter must be a [DateTime](http://msdn2.microsoft.com/EN-US/library/03ybds8y) object set to no longer than 3 years from **DateTime.Now**.</span></span>
 


## <a name="update-the-remote-web-application-in-visual-studio-to-use-the-new-secret"></a><span data-ttu-id="1abb3-133">Aktualisieren der Remote-Webanwendung in Visual Studio zum Verwenden des neuen geheimen Schlüssels</span><span class="sxs-lookup"><span data-stu-id="1abb3-133">Update the remote web application in Visual Studio to use the new secret</span></span>


 <span data-ttu-id="1abb3-p108">**Wichtig** Wenn Ihr Add-In ursprünglich mit einer Vorabversion der Microsoft Office Developer Tools für Visual Studio erstellt wurde, enthält es möglicherweise eine veraltete Version der Datei TokenHelper.cs (oder TokenHelper.vb). Wenn die Datei die Zeichenfolge „secondaryClientSecret" nicht enthält, ist sie veraltet und muss ausgetauscht werden, bevor Sie die Webanwendung durch einen neuen geheimen Schlüssel aktualisieren können. Um eine Kopie einer endgültigen Version der Datei abzurufen, benötigen Sie Visual Studio 2012 oder höher. Erstellen Sie ein neues SharePoint-Add-In-Projekt in Visual Studio. Kopieren Sie die TokenHelper-Datei in das Webanwendungsprojekt Ihres SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p108">**Important** If your add-in was originally created with a prerelease version the Microsoft Office Developer Tools for Visual Studio, it may contain an out-of-date version of the TokenHelper.cs (or .vb) file. If the file does not contain the string "secondaryClientSecret", it is out-of-date and it must be replaced before you can update the web application with a new secret. To obtain a copy of a release version of the file, you need Visual Studio 2012 or later. Create a new SharePoint Add-in project in Visual Studio. Copy the TokenHelper file from it to the web application project of your SharePoint Add-in.</span></span> 
 


1. <span data-ttu-id="1abb3-p109">Öffnen Sie das SharePoint-Add-In-Projekt in Visual Studio, und öffnen Sie die Datei „web.config“ für das Webanwendungsprojekt. Im Abschnitt **appSettings** finden Sie Schlüssel für die Client-ID und den geheimen Clientschlüssel. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="1abb3-p109">Open the SharePoint Add-in project in Visual Studio, and open the web.config file for the web application project. In the **appSettings** section, there are keys for the client ID and client secret. The following is an example:</span></span>
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>

```

2. <span data-ttu-id="1abb3-142">Ändern Sie den Namen des **ClientSecret**-Schlüssels in „SecondaryClientSecret“ wie im folgenden Beispiel:</span><span class="sxs-lookup"><span data-stu-id="1abb3-142">Change the name of the **ClientSecret** key to "SecondaryClientSecret" as shown in the following example:</span></span>
    
```XML
  <add key="SecondaryClientSecret" value="your old secret here" />
```

> <span data-ttu-id="1abb3-p110">**Hinweis** Wenn Sie diesen Vorgang das erste Mal ausführen, gibt es zu diesem Zeitpunkt noch keinen **SecondaryClientSecret**-Eigenschaftseintrag in der Konfigurationsdatei. Wenn Sie das Verfahren jedoch für beim Ablauf eines nachfolgenden geheimen Clientschlüssels durchführen (zweiter oder dritter), ist die Eigenschaft **SecondaryClientSecret** bereits vorhanden und enthält den ursprünglichen bzw. bereits vor einiger Zeit abgelaufenen alten geheimen Clientschlüssel. Löschen Sie in diesem Fall zunächst die **SecondaryClientSecret**-Eigenschaft, bevor Sie **ClientSecret** umbenennen.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p110">**Note** If you are performing this procedure for the first time there will be no **SecondaryClientSecret** property entry at this point in the configuration file. However if you are performing the procedure for a subsequent client secret expiration (second or third) the property **SecondaryClientSecret** is already present and containing the initial or already longer time ago expired old secret. In this case delete the **SecondaryClientSecret** property first before renaming **ClientSecret**.</span></span>

3. <span data-ttu-id="1abb3-p111">Fügen Sie einen neuen **ClientSecret**-Schlüssel hinzu, und übergeben Sie den neuen geheimen Clientschlüssel. Ihr Markup sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="1abb3-p111">Add a new **ClientSecret** key and give it your new client secret. Your markup should now look like the following:</span></span>
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your new secret here" />
  <add key="SecondaryClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>
```

4. <span data-ttu-id="1abb3-148">Wenn Sie zu einer neuen „TokenHelper“-Datei gewechselt haben, müssen Sie das Projekt neu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1abb3-148">If you changed to a new TokenHelper file, rebuild the project.</span></span>
    
 
5. <span data-ttu-id="1abb3-149">Veröffentlichen Sie die Webanwendung erneut.</span><span class="sxs-lookup"><span data-stu-id="1abb3-149">Republish the web application.</span></span>
    
 

## <a name="create-a-client-secret-that-is-valid-for-three-years"></a><span data-ttu-id="1abb3-150">Erstellen eines geheimen Clientschlüssels, der drei Jahre gültig ist</span><span class="sxs-lookup"><span data-stu-id="1abb3-150">Create a client secret that is valid for three years</span></span>

<span data-ttu-id="1abb3-p112">Für abgelaufene geheime Clientschlüssel müssen Sie zunächst alle abgelaufenen Schlüssel für eine bestimmte **ClientId** löschen. Sie erstellen dann einen neuen mit MSOPowerShell, warten mindestens 24 Stunden, und testen die App mit der neuen **ClientId** und dem neuen **ClientSecret**-Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p112">For expired client secrets, first you must delete all of the expired secrets for a given **clientId**. Then you create a new one with MSO PowerShell, wait at least 24 hours, and test the app with the new **clientId** and **ClientSecret** key.</span></span>
 

 

1. <span data-ttu-id="1abb3-153">Stellen Sie eine Verbindung mit MSOnline anhand des Mandanten-Admininistratorbenutzers und dem unten aufgeführten Markup her, indem Sie SharePoint Windows PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="1abb3-153">Connect to MSOnline using the tenant admin user with the below markup using SharePoint Windows PowerShell.</span></span>
    
```
  import-module MSOnline
$msolcred = get-credential
connect-msolservice -credential $msolcred

```

2. <span data-ttu-id="1abb3-p113">Rufen Sie **ServicePrincipals** und die Schlüssel ab. Durch das Drucken von **$keys** werden drei Datensätze zurückgegeben. Ersetzen Sie jede **KeyId** unter *KeyId1* , *KeyId2* und *KeyId3*. Außerdem wird Ihnen das **EndDate** der einzelnen Schlüssel angezeigt. Vergewissern Sie sich, dass dort die abgelaufenen Schlüssel angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p113">Get **ServicePrincipals** and keys. Printing **$keys** returns three records. Replace each **KeyId** in *KeyId1*  , *KeyId2*  and *KeyId3*  . You will also see the **EndDate** of each key. Confirm whether your expired key appers there.</span></span>
    
     <span data-ttu-id="1abb3-p114">**Hinweis:** Die **clientId** muss der abgelaufenen **clientId** entsprechen. Es wird empfohlen, alle Schlüssel für diese **clientId** zu löschen, sowohl die abgelaufenen als auch die noch nicht abgelaufenen.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p114">**Note:** The **clientId** needs to match your expired **clientId**. It's recommended to delete all keys, both expired and unexpired, for this **clientId**.</span></span>
    


```
  $clientId = "27c5b286-62a6-45c7-beda-abbaea6eecf2"
$keys = Get-MsolServicePrincipalCredential -AppPrincipalId $clientId
Remove-MsolServicePrincipalCredential -KeyIds @("KeyId1"," KeyId2"," KeyId3") -AppPrincipalId $clientId 

```

3. <span data-ttu-id="1abb3-p115">Generieren Sie ein neues **ClientSecret** für diese **clientID**. Es verwendet die gleiche **clientId**, die im vorhergehenden Schritt eingerichtet wurde. Das neue **ClientSecret** ist 3 Jahre gültig.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p115">Generate a new **ClientSecret** for this **clientID**. It uses the same **clientId** as set in the above step. The new **ClientSecret** is valid for 3 years.</span></span>
    
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

4. <span data-ttu-id="1abb3-164">Kopieren Sie die Ausgabe von **$newClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="1abb3-164">Copy the output of **$newClientSecret**.</span></span>
    
 
5. <span data-ttu-id="1abb3-p116">Ersetzen Sie die **Web.config** durch diese **ClientId** und das **ClientSecret**. Sie benötigen nicht die **SecondaryClientSecret**-App-Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="1abb3-p116">Replace the **Web.config** with this **ClientId** and **ClientSecret**. You don't need **SecondaryClientSecret** app settings.</span></span>
    
 
6. <span data-ttu-id="1abb3-167">Warten Sie mindestens 24 Stunden mit dem Auffüllen des **ClientSecret** in SharePoint Office (SPO).</span><span class="sxs-lookup"><span data-stu-id="1abb3-167">Wait at least 24 hours to propagate **ClientSecret** to SharePoint Office (SPO).</span></span>
    
 

## <a name="see-also"></a><span data-ttu-id="1abb3-168">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="1abb3-168">See also</span></span>


#### <a name="other-resources"></a><span data-ttu-id="1abb3-169">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="1abb3-169">Other resources</span></span>


 
 [<span data-ttu-id="1abb3-170">Vom Anbieter gehostete fällt bei SPO aus</span><span class="sxs-lookup"><span data-stu-id="1abb3-170">Provider Hosted App fails on SPO</span></span>](http://blogs.technet.com/b/sharepointdevelopersupport/archive/2015/03/11/provider-hosted-app-fails-on-spo.aspx)
