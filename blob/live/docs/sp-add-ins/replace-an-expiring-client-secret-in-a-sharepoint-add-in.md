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
# <a name="replace-an-expiring-client-secret-in-a-sharepoint-add-in"></a><span data-ttu-id="da3f7-102">Austauschen eines ablaufenden geheimen Clientschlüssels in einem SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="da3f7-102">Replace an expiring client secret in a SharePoint Add-in</span></span>
<span data-ttu-id="da3f7-103">Erfahren Sie, wie Sie einen neuen geheimen Clientschlüssel für ein SharePoint-Add-In hinzufügen können, der bei AppRegNew.aspx registriert ist.</span><span class="sxs-lookup"><span data-stu-id="da3f7-103">Learn how to add a new client secret for a SharePoint Add-in that is registered with AppRegNew.aspx.</span></span>
 

> [!NOTE]
> <span data-ttu-id="da3f7-104">Der Name "Apps für SharePoint" wird in "SharePoint-Add-Ins" geändert.</span><span class="sxs-lookup"><span data-stu-id="da3f7-104">The name "apps for SharePoint" is changing to "SharePoint Add-ins".</span></span> <span data-ttu-id="da3f7-105">Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Tools für Visual Studio möglicherweise weiterhin der Begriff "Apps für SharePoint" verwendet.</span><span class="sxs-lookup"><span data-stu-id="da3f7-105">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see New name for apps for Office and SharePoint.</span></span> <span data-ttu-id="da3f7-106">Weitere Einzelheiten finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="da3f7-106">For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="da3f7-p102">Geheime Clientschlüssel für SharePoint-Add-Ins, die mithilfe der AppRegNew.aspx-Seite registriert wurden, laufen nach einem Jahr ab. In diesem Artikel wird erläutert, wie Sie einen neuen geheimen Schlüssel für das Add-In hinzufügen und wie Sie einen neuen geheimen Clientschlüssel erstellen können, der drei Jahre gültig ist.</span><span class="sxs-lookup"><span data-stu-id="da3f7-p102">Client secrets for SharePoint Add-ins that are registered using the AppRegNew.aspx page expire after one year. This article explains how to add a new secret for the add-in, as well as how to create a new client secret that is valid for three years.</span></span>
 

> [!NOTE]
> <span data-ttu-id="da3f7-109">Dieser Artikel enthält Informationen zu SharePoint-Add-Ins, die über einen Organisationskatalog verteilt werden und bei der Seite "AppRegNew.aspx" registriert sind.</span><span class="sxs-lookup"><span data-stu-id="da3f7-109">Note  This article is about SharePoint Add-ins that are distributed through an organization catalog and registered with the AppRegNew.aspx page. If the add-in is registered on the Seller Dashboard, see  Create or update client IDs and secrets in the Seller Dashboard.</span></span> <span data-ttu-id="da3f7-110">Wenn das Add-In auf dem Verkäuferdashboard registriert ist, finden Sie weitere Informationen unter [Erstellen oder Aktualisieren von Client-IDs und geheimen Clientschlüsseln im Verkäuferdashboard](https://dev.office.com/officestore/docs/create-or-update-client-ids-and-secrets#bk_update).</span><span class="sxs-lookup"><span data-stu-id="da3f7-110">Note  This article is about SharePoint Add-ins that are distributed through an organization catalog and registered with the AppRegNew.aspx page. If the add-in is registered on the Seller Dashboard, see  [Create or update client IDs and secrets in the Seller Dashboard](https://dev.office.com/officestore/docs/create-or-update-client-ids-and-secrets#bk_update).</span></span>
 


## <a name="prerequisites-for-refreshing-a-client-secret"></a><span data-ttu-id="da3f7-111">Voraussetzungen zum Aktualisieren eines geheimen Clientschlüssels</span><span class="sxs-lookup"><span data-stu-id="da3f7-111">Prerequisites for refreshing a client secret</span></span>

<span data-ttu-id="da3f7-112">Stellen Sie vor Beginn Folgendes sicher:</span><span class="sxs-lookup"><span data-stu-id="da3f7-112">Ensure the following before you begin:</span></span>
 

 

-  <span data-ttu-id="da3f7-113">[Der Microsoft Online Services-Anmeldeassistent](http://www.microsoft.com/download/details.aspx?id=39267) ist auf dem Entwicklungscomputer installiert.</span><span class="sxs-lookup"><span data-stu-id="da3f7-113">[Microsoft Online Services Sign-In Assistant](http://www.microsoft.com/download/details.aspx?id=39267) is installed on the development computer.</span></span>
    
 
- <span data-ttu-id="da3f7-114">Das Microsoft Online Services PowerShell-Modul ( [32-Bit](http://go.microsoft.com/fwlink/p/?linkid=236298);  [64-Bit](http://go.microsoft.com/fwlink/p/?linkid=236297)) wird auf dem Entwicklungscomputer installiert.</span><span class="sxs-lookup"><span data-stu-id="da3f7-114">Microsoft Online Services PowerShell Module ( [32-bit](http://go.microsoft.com/fwlink/p/?linkid=236298);  [64-bit](http://go.microsoft.com/fwlink/p/?linkid=236297)) is installed on the development computer.</span></span>
    
 
- <span data-ttu-id="da3f7-115">Sie sind der Mandantenadministrator für den Office 365-Mandanten (oder ein Farmadministrator in der Farm), auf dem das Add-In mit der AppRegNew.aspx-Seite registriert wurde.</span><span class="sxs-lookup"><span data-stu-id="da3f7-115">You are a tenant administrator for the Office 365 tenant (or a farm administrator on the farm) where the add-in was registered with the AppRegNew.aspx page.</span></span>
    
 

## <a name="find-out-the-expiration-dates-of-the-sharepoint-add-ins-installed-to-the-office-365-tenancy"></a><span data-ttu-id="da3f7-116">Ermitteln der Ablaufdaten des auf dem Office 365-Mandanten installierten SharePoint-Add-Inss</span><span class="sxs-lookup"><span data-stu-id="da3f7-116">Find out the expiration dates of the SharePoint Add-ins installed to the Office 365 tenancy</span></span>


 

 

1. <span data-ttu-id="da3f7-117">Öffnen Sie Windows PowerShell und führen Sie folgendes Cmdlet aus:</span><span class="sxs-lookup"><span data-stu-id="da3f7-117">Open Windows PowerShell and run the following cmdlet:</span></span>
    
```
  Connect-MsolService

```

2. <span data-ttu-id="da3f7-118">Geben Sie bei der Anmeldeaufforderung die Mandantenadministrator-Anmeldeinformationen (oder Farmadministrator) für die Office 365-Mandantschaft oder die Farm ein, auf der das Add-In mit der AppRegNew.aspx-Seite registriert wurde.</span><span class="sxs-lookup"><span data-stu-id="da3f7-118">At the login prompt, enter tenant-administrator (or farm administrator) credentials for the Office 365 tenancy or farm where the add-in was registered with AppRegNew.aspx.</span></span>
    
 
3. <span data-ttu-id="da3f7-p104">Generieren Sie einen Bericht mit den folgenden Zeilen, in denen das jeweilige Add-In und das Datum, an dem ihr geheimer Schlüssel abläuft, aufgeführt sind. Beachten Sie zu diesem Code Folgendes:</span><span class="sxs-lookup"><span data-stu-id="da3f7-p104">Generate a report that lists each add-in and the date that its secret expires with the following lines. Note the following about this code:</span></span>
    
      - <span data-ttu-id="da3f7-121">Zunächst werden eigene Anwendungen von Microsoft und Add-Ins, die noch entwickelt werden, herausgefiltert.</span><span class="sxs-lookup"><span data-stu-id="da3f7-121">It first filters out Microsoft's own applications, add-ins still under development (and a now-deprecated type of add-in that was called autohosted).</span></span>
    
 
  - <span data-ttu-id="da3f7-122">Aus dem Rest werden Nicht-SharePoint-Add.Ins und Add-Ins, die asymmetrische Schlüssel verwenden, z. B. Workflows, herausgefiltert.</span><span class="sxs-lookup"><span data-stu-id="da3f7-122">From the remainder, it filters out non-SharePoint add-ins and add-ins that use asymmetric keys, like workflows.</span></span>
    
 

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

4. <span data-ttu-id="da3f7-p105">Öffnen Sie die Datei „C:\temp\appsec.txt“, um den Bericht anzuzeigen. Lassen Sie das Windows PowerShell-Fenster für die nächste Prozedur geöffnet, wenn sich das Ablaufdatum für einen der geheimen Schlüssel nähert.</span><span class="sxs-lookup"><span data-stu-id="da3f7-p105">Open the file C:\temp\appsec.txt to see the report. Leave the Windows PowerShell window open for the next procedure, if any of the secrets is near to expiration.</span></span>
    
 

## <a name="generate-a-new-secret"></a><span data-ttu-id="da3f7-125">Generieren eines neuen geheimen Schlüssels</span><span class="sxs-lookup"><span data-stu-id="da3f7-125">Generate a new secret</span></span>


 

 

1. <span data-ttu-id="da3f7-126">Erstellen Sie eine Client-ID-Variable mit folgender Zeile, und verwenden Sie dafür die Client-ID des SharePoint-Add-Ins als Parameter.</span><span class="sxs-lookup"><span data-stu-id="da3f7-126">Create a client ID variable with the following line, using the client ID of the SharePoint Add-in as the parameter.</span></span>
    
```
  $clientId = 'client id of the add-in'

```

2. <span data-ttu-id="da3f7-127">Generieren Sie mit den folgenden Zeilen einen neuen geheimen Clientschlüssel:</span><span class="sxs-lookup"><span data-stu-id="da3f7-127">Generate a new client secret with the following lines:</span></span>
    
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

3. <span data-ttu-id="da3f7-p106">Der neue geheime Clientschlüssel wird in der Windows PowerShell -Konsole angezeigt. Kopieren Sie ihn in eine Textdatei. Sie benötigen ihn in der nächsten Prozedur.</span><span class="sxs-lookup"><span data-stu-id="da3f7-p106">The new client secret will appear on the Windows PowerShell console. Copy it to a text file. You use it in the next procedure.</span></span>
    
 

> [!TIP]
> <span data-ttu-id="da3f7-131">Standardmäßig sind geheime Add-In-Schlüssel ein Jahr gültig.</span><span class="sxs-lookup"><span data-stu-id="da3f7-131">By default, the add-in secret lasts one year.</span></span> <span data-ttu-id="da3f7-132">Sie können diesen Zeitraum mit dem Parameter **-EndDate** der drei Aufrufe des Cmdlets **New-MsolServicePrincipalCredential** verkürzen oder verlängern (bis maximal drei Jahre).</span><span class="sxs-lookup"><span data-stu-id="da3f7-132">Tip  By default, the add-in secret lasts one year. You can set this to a shorter or longer (up to 3 years maximum) by using the  **-EndDate** parameter on the three calls of the **New-MsolServicePrincipalCredential** cmdlet. The value of the parameter must be a DateTime object set to no longer than 3 years from DateTime.Now.</span></span> <span data-ttu-id="da3f7-133">Der Wert des Parameters muss ein [DateTime](http://msdn2.microsoft.com/de-DE/library/03ybds8y)-Objekt sein, das maximal auf einen Zeitraum von drei Jahren ab **DateTime.Now** eingestellt werden darf.</span><span class="sxs-lookup"><span data-stu-id="da3f7-133">The value of the parameter must be a [DateTime](http://msdn2.microsoft.com/de-DE/library/03ybds8y) object set to no longer than 3 years from **DateTime.Now**.</span></span>
 
## <a name="update-the-remote-web-application-in-visual-studio-to-use-the-new-secret"></a><span data-ttu-id="da3f7-134">Aktualisieren der Remote-Webanwendung in Visual Studio zum Verwenden des neuen geheimen Schlüssels</span><span class="sxs-lookup"><span data-stu-id="da3f7-134">Update the remote web application in Visual Studio to use the new secret</span></span>


> [!IMPORTANT]
>  <span data-ttu-id="da3f7-135">Wenn das Add-In ursprünglich mit einer Vorabversion des Microsoft Office Developer Tools für Visual Studio erstellt wurde, kann es eine veraltete Version der Datei TokenHelper.cs (oder .vb) enthalten.</span><span class="sxs-lookup"><span data-stu-id="da3f7-135">If your add-in was originally created with a prerelease version the Microsoft Office Developer Tools for Visual Studio, it may contain an out-of-date version of the TokenHelper.cs (or .vb) file.</span></span> <span data-ttu-id="da3f7-136">Wenn die Datei nicht die Zeichenfolge "SecondaryClientSecret" enthält, ist sie veraltet und muss ersetzt werden, bevor Sie die Webanwendung mit einem neuen Schlüssel aktualisieren können.</span><span class="sxs-lookup"><span data-stu-id="da3f7-136">If the file does not contain the string "secondaryClientSecret", it is out-of-date and it must be replaced before you can update the web application with a new secret.</span></span> <span data-ttu-id="da3f7-137">Sie benötigen Visual Studio 2012 oder höher, um eine Kopie der Veröffentlichungsversion der Datei erhalten zu können.</span><span class="sxs-lookup"><span data-stu-id="da3f7-137">To obtain a copy of a release version of the file, you need Visual Studio 2012 or later.</span></span> <span data-ttu-id="da3f7-138">Erstellen Sie ein neues SharePoint-Add-In-Projekt in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da3f7-138">Create a SharePoint Add-in project in Visual Studio</span></span> <span data-ttu-id="da3f7-139">Kopieren Sie die darin enthaltene Datei TokenHelper in das Webanwendungsprojekt Ihrer SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="da3f7-139">Copy the TokenHelper file from it to the web application project of your SharePoint Add-in.</span></span> 
 


1. <span data-ttu-id="da3f7-p109">Öffnen Sie das SharePoint-Add-In-Projekt in Visual Studio, und öffnen Sie die Datei „web.config“ für das Webanwendungsprojekt. Im Abschnitt **appSettings** finden Sie Schlüssel für die Client-ID und den geheimen Clientschlüssel. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="da3f7-p109">Open the SharePoint Add-in project in Visual Studio, and open the web.config file for the web application project. In the  **appSettings** section, there are keys for the client ID and client secret. The following is an example:</span></span>
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>

```

2. <span data-ttu-id="da3f7-143">Ändern Sie den Namen des **ClientSecret**-Schlüssels in „SecondaryClientSecret“ wie im folgenden Beispiel:</span><span class="sxs-lookup"><span data-stu-id="da3f7-143">Change the name of the  **ClientSecret** key to "SecondaryClientSecret" as shown in the following example:</span></span>
    
```XML
  <add key="SecondaryClientSecret" value="your old secret here" />
```

> [!NOTE]
> <span data-ttu-id="da3f7-144">Wenn Sie dieses Verfahren zum ersten Mal durchführen, ist zu diesem Zeitpunkt in der Konfigurationsdatei kein **SecondaryClientSecret**-Eigenschaftseintrag vorhanden.</span><span class="sxs-lookup"><span data-stu-id="da3f7-144">If you are performing this procedure for the first time there will be no **SecondaryClientSecret** property entry at this point in the configuration file.</span></span> <span data-ttu-id="da3f7-145">Wenn Sie das Verfahren für einen nachfolgenden (zweiten oder dritten) Ablauf eines geheimen Clientschlüssels durchführen, ist die Eigenschaft **SecondaryClientSecret** bereits vorhanden und enthält den ursprünglichen oder noch älteren abgelaufenen alten Schlüssel .</span><span class="sxs-lookup"><span data-stu-id="da3f7-145">Note If you are performing this procedure for the first time there will be no SecondaryClientSecret property entry at this point in the configuration file. However if you are performing the procedure for a subsequent client secret expiration (second or third) the property **SecondaryClientSecret** is already present and containing the initial or already longer time ago expired old secret. In this case delete the SecondaryClientSecret property first before renaming ClientSecret.</span></span> <span data-ttu-id="da3f7-146">Löschen Sie in diesem Fall zuerst die Eigenschaft **SecondaryClientSecret**, bevor Sie **ClientSecret** umbenennen.</span><span class="sxs-lookup"><span data-stu-id="da3f7-146">In this case delete the **SecondaryClientSecret** property first before renaming **ClientSecret**.</span></span>

3. <span data-ttu-id="da3f7-p111">Fügen Sie einen neuen **ClientSecret**-Schlüssel hinzu, und übergeben Sie den neuen geheimen Clientschlüssel. Ihr Markup sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="da3f7-p111">Add a new  **ClientSecret** key and give it your new client secret. Your markup should now look like the following:</span></span>
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your new secret here" />
  <add key="SecondaryClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>
```

> [!IMPORTANT]
> <span data-ttu-id="da3f7-149">Sie können den neu generierten geheimen Clientschlüssel erst verwenden, nachdem der aktuelle geheime Clientschlüssel abgelaufen ist.</span><span class="sxs-lookup"><span data-stu-id="da3f7-149">You will not be able to use the newly generated client secret until the current client secret expires.</span></span> <span data-ttu-id="da3f7-150">Daher ist es nicht möglich, den Client-ID-Schlüssel ohne den vorhandenen SecondaryClientSecret-Schlüssel in den neuen geheimen Clientschlüssel zu ändern.</span><span class="sxs-lookup"><span data-stu-id="da3f7-150">Therefore, changing the ClientId key to the new client secret without the SecondaryClientSecret key present will not work.</span></span> <span data-ttu-id="da3f7-151">Sie müssen die Verfahrensweise dieses Artikels befolgen und warten, bis der vorherige geheime Clientschlüssel abgelaufen ist.</span><span class="sxs-lookup"><span data-stu-id="da3f7-151">You must follow the  procedure in this article and wait for the previous client secret to expire.</span></span> <span data-ttu-id="da3f7-152">Dann können Sie den SecondaryClientSecret entfernen, wenn Sie möchten.</span><span class="sxs-lookup"><span data-stu-id="da3f7-152">Then you can remove the SecondaryClientSecret if you want to.</span></span>

4. <span data-ttu-id="da3f7-153">Wenn Sie zu einer neuen „TokenHelper“-Datei gewechselt haben, müssen Sie das Projekt neu erstellen.</span><span class="sxs-lookup"><span data-stu-id="da3f7-153">If you changed to a new TokenHelper file, rebuild the project.</span></span>
    
 
5. <span data-ttu-id="da3f7-154">Veröffentlichen Sie die Webanwendung erneut.</span><span class="sxs-lookup"><span data-stu-id="da3f7-154">Republish the web application.</span></span>
    
 

## <a name="create-a-client-secret-that-is-valid-for-three-years"></a><span data-ttu-id="da3f7-155">Erstellen eines geheimen Clientschlüssels, der drei Jahre gültig ist</span><span class="sxs-lookup"><span data-stu-id="da3f7-155">Create a client secret that is valid for three years</span></span>

<span data-ttu-id="da3f7-p113">Für abgelaufene geheime Clientschlüssel müssen Sie zunächst alle abgelaufenen Schlüssel für eine bestimmte **ClientId** löschen. Sie erstellen dann einen neuen mit MSOPowerShell, warten mindestens 24 Stunden, und testen die App mit der neuen **ClientId** und dem neuen **ClientSecret**-Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="da3f7-p113">For expired client secrets, first you must delete all of the expired secrets for a given  **clientId**. Then you create a new one with MSO PowerShell, wait at least 24 hours, and test the app with the new **clientId** and **ClientSecret** key.</span></span>
 

 

1. <span data-ttu-id="da3f7-158">Stellen Sie eine Verbindung mit MSOnline anhand des Mandanten-Admininistratorbenutzers und dem unten aufgeführten Markup her, indem Sie SharePoint Windows PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="da3f7-158">Connect to MSOnline using the tenant admin user with the below markup using SharePoint Windows PowerShell.</span></span>
    
```
  import-module MSOnline
$msolcred = get-credential
connect-msolservice -credential $msolcred

```

2. <span data-ttu-id="da3f7-p114">Rufen Sie **ServicePrincipals** und die Schlüssel ab. Durch das Drucken von **$keys** werden drei Datensätze zurückgegeben. Ersetzen Sie jede **KeyId** unter *KeyId1* , *KeyId2* und *KeyId3*. Außerdem wird Ihnen das **EndDate** der einzelnen Schlüssel angezeigt. Vergewissern Sie sich, dass dort die abgelaufenen Schlüssel angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="da3f7-p114">Get  **ServicePrincipals** and keys. Printing **$keys** returns three records. Replace each **KeyId** in *KeyId1*  , *KeyId2*  and *KeyId3*  . You will also see the **EndDate** of each key. Confirm whether your expired key appers there.</span></span>
    
     ><span data-ttu-id="da3f7-p115">**Hinweis:** Die **clientId** muss der abgelaufenen **clientId** entsprechen. Es wird empfohlen, alle Schlüssel für diese **clientId** zu löschen, sowohl die abgelaufenen als auch die noch nicht abgelaufenen.</span><span class="sxs-lookup"><span data-stu-id="da3f7-p115">**Note:** The **clientId** needs to match your expired **clientId**. It's recommended to delete all keys, both expired and unexpired, for this **clientId**.</span></span>
    


```
  $clientId = "27c5b286-62a6-45c7-beda-abbaea6eecf2"
$keys = Get-MsolServicePrincipalCredential -AppPrincipalId $clientId
Remove-MsolServicePrincipalCredential -KeyIds @("KeyId1"," KeyId2"," KeyId3") -AppPrincipalId $clientId 

```

3. <span data-ttu-id="da3f7-p116">Generieren Sie ein neues **ClientSecret** für diese **clientID**. Es verwendet die gleiche **clientId**, die im vorhergehenden Schritt eingerichtet wurde. Das neue **ClientSecret** ist 3 Jahre gültig.</span><span class="sxs-lookup"><span data-stu-id="da3f7-p116">Generate a new  **ClientSecret** for this **clientID**. It uses the same **clientId** as set in the above step. The new **ClientSecret** is valid for 3 years.</span></span>
    
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

4. <span data-ttu-id="da3f7-169">Kopieren Sie die Ausgabe von **$newClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="da3f7-169">Copy the output of  **$newClientSecret**.</span></span>
    
 
5. <span data-ttu-id="da3f7-p117">Ersetzen Sie die **Web.config** durch diese **ClientId** und das **ClientSecret**. Sie benötigen nicht die **SecondaryClientSecret**-App-Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="da3f7-p117">Replace the  **Web.config** with this **ClientId** and **ClientSecret**. You don't need **SecondaryClientSecret** app settings.</span></span>
    
 
6. <span data-ttu-id="da3f7-172">Warten Sie mindestens 24 Stunden mit dem Auffüllen des **ClientSecret** in SharePoint Office (SPO).</span><span class="sxs-lookup"><span data-stu-id="da3f7-172">Wait at least 24 hours to propagate  **ClientSecret** to SharePoint Office (SPO).</span></span>
    
 

## <a name="see-also"></a><span data-ttu-id="da3f7-173">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="da3f7-173">See also</span></span>

[<span data-ttu-id="da3f7-174">Vom Anbieter gehostete App fällt bei SPO aus</span><span class="sxs-lookup"><span data-stu-id="da3f7-174">Provider Hosted App fails on SPO</span></span>](http://blogs.technet.com/b/sharepointdevelopersupport/archive/2015/03/11/provider-hosted-app-fails-on-spo.aspx)
