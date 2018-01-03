---
title: Erstellen eines UDF, das einen Webdienst aufruft
ms.date: 09/25/2017
keywords: how to,howdoi,howto,UDF
f1_keywords: how to,howdoi,howto,UDF
ms.prod: sharepoint
ms.assetid: 360c5766-4b5d-4a48-9f23-8955036924ce
ms.openlocfilehash: 37202a89818446d1a3730d09012469a7f7e110d4
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="create-a-udf-that-calls-a-web-service"></a><span data-ttu-id="68235-103">Erstellen eines UDF, das einen Webdienst aufruft</span><span class="sxs-lookup"><span data-stu-id="68235-103">Create a UDF that calls a web service</span></span>

<span data-ttu-id="68235-p101">This example shows how to call an external Web service from a user-defined function (UDF). The Web service used in this example is:</span><span class="sxs-lookup"><span data-stu-id="68235-p101">This example shows how to call an external Web service from a user-defined function (UDF). The Web service used in this example is:</span></span>
  
    
    

 <span data-ttu-id="68235-106">`http://webservices.imacination.com/distance/Distance.jws?wsdl` Sie müssen zum Erstellen dieses Beispiels Microsoft Visual Studio 2005 oder ein vergleichbares, mit Microsoft .NET Framework 2.0-kompatibles, Programm verwenden.</span><span class="sxs-lookup"><span data-stu-id="68235-106">`http://webservices.imacination.com/distance/Distance.jws?wsdl` You must use Microsoft Visual Studio 2005 or a similar Microsoft .NET Framework 2.0-compatible development tool to create this sample.</span></span> 
  
> [!NOTE]
> <span data-ttu-id="68235-107">Stellen Sie vor dem Testen dieses Codes sicher, dass der aufzurufende Webdienst verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="68235-107">Note: Before testing the code, make sure that the Web service you are calling is available.</span></span> <span data-ttu-id="68235-108">Möglicherweise steht der Webdienstserver nicht zur Verfügung oder der Webdienst wird nicht mehr unterstützt.</span><span class="sxs-lookup"><span data-stu-id="68235-108">The Web service server could be down or the Web service discontinued.</span></span> <span data-ttu-id="68235-109">Wenn der Webdienst nicht verfügbar ist, tritt bei den Webdienstaufrufen von Ihrem Code aus ein Fehler auf.</span><span class="sxs-lookup"><span data-stu-id="68235-109">If the Web service is unavailable, the calls you make to the Web service from your code will fail.</span></span> <span data-ttu-id="68235-110">Sie können überprüfen, ob ein Webdienst verfügbar ist, indem Sie die Website öffnen.</span><span class="sxs-lookup"><span data-stu-id="68235-110">> You can check if a Web service is available by visiting its site.</span></span> <span data-ttu-id="68235-111">In diesem Beispiel lautet die URL: > `http://webservices.imacination.com/distance/Distance.jws?wsdl`>. Wenn der Webdienst verfügbar ist, wird Web Services Description Language (WSDL) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="68235-111">In this example, the URL is: >  `http://webservices.imacination.com/distance/Distance.jws?wsdl`> If the Web service is available, you will be able to see the Web Services Description Language (WSDL).</span></span> <span data-ttu-id="68235-112">Wenn er nicht verfügbar ist, wird die übliche Fehlermeldung „Webseite nicht gefunden“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="68235-112">If it is not available, you will get the usual "Web page not found" error.</span></span> 
  
    
    


## <a name="example"></a><span data-ttu-id="68235-113">Beispiel</span><span class="sxs-lookup"><span data-stu-id="68235-113">Example</span></span>

<span data-ttu-id="68235-114">You can learn more about the Web service used in this example by examining its WSDL.</span><span class="sxs-lookup"><span data-stu-id="68235-114">You can learn more about the Web service used in this example by examining its WSDL.</span></span>
  
    
    
<span data-ttu-id="68235-p103">One service it provides is to return geographical coordinates in decimal form. In this sample, the  `ToDegreeNotation` function has been added to show how you can convert coordinates to degrees/minutes/seconds, which is more appropriate for displaying coordinates.</span><span class="sxs-lookup"><span data-stu-id="68235-p103">One service it provides is to return geographical coordinates in decimal form. In this sample, the  `ToDegreeNotation` function has been added to show how you can convert coordinates to degrees/minutes/seconds, which is more appropriate for displaying coordinates.</span></span>
  
    
    



```cs

[UdfMethod]
public string ToDegreeNotation(double angle)
{
    int deg = (int)angle;
    double minutesAndSeconds = Math.Abs(angle - deg) * 60;
    int minutes = (int)minutesAndSeconds;
    int seconds = (int)(Math.Abs(minutesAndSeconds - minutes) * 60);

    return deg.ToString() + "°" + minutes.ToString() + "\\'" + 
        seconds.ToString() + "\\"";
}
```




```VB.net

<UdfMethod> _
Public Function ToDegreeNotation(ByVal angle As Double) As String
    Dim deg As Integer = CInt(Fix(angle))
    Dim minutesAndSeconds As Double = Math.Abs(angle - deg) * 60
    Dim minutes As Integer = CInt(Fix(minutesAndSeconds))
    Dim seconds As Integer = CInt(Fix(Math.Abs(minutesAndSeconds - minutes) * 60))

    Return deg.ToString() &amp; "°" &amp; minutes.ToString() &amp; "'" &amp; seconds.ToString() &amp; """"
End Function
```

<span data-ttu-id="68235-p104">If your Internet Explorer LAN setting is configured to use a proxy server, your code must explicitly make a call to set the proxy server. Otherwise, your Web service calls will fail. You can set the proxy server in the constructor as follows:</span><span class="sxs-lookup"><span data-stu-id="68235-p104">If your Internet Explorer LAN setting is configured to use a proxy server, your code must explicitly make a call to set the proxy server. Otherwise, your Web service calls will fail. You can set the proxy server in the constructor as follows:</span></span>
  
    
    



```cs

namespace ZipCodeUdfSample
{
    [UdfClass]
    public class ZipCodeUdfs
    {
        DistanceService distanceService = null;
        public ZipCodeUdfs()
        {
            this.distanceService = new DistanceService();
            this.distanceService.Proxy = 
                new WebProxy("http://myproxy:80", true);
        }
```




```VB.net

Namespace ZipCodeUdfSample
    <UdfClass> _
    Public Class ZipCodeUdfs
        Private distanceService As DistanceService = Nothing

        Public Sub New()
            Me.distanceService = New DistanceService()
            'this.distanceService.Proxy = new WebProxy("http://myproxy:80", true);
        End Sub
```

<span data-ttu-id="68235-120">For more information about how to test and call UDFs from cells, see  [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md).</span><span class="sxs-lookup"><span data-stu-id="68235-120">For more information about how to test and call UDFs from cells, see  [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md).</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.Text;
using System.Net;
using Microsoft.Office.Excel.Server.Udf;
using ZipCodes.com.imacination.webservices;

namespace ZipCodeUdfSample
{
    [UdfClass]
    public class ZipCodeUdfs
    {
        DistanceService distanceService = null;

        public ZipCodeUdfs()
        {
            this.distanceService = new DistanceService();
            //this.distanceService.Proxy = new WebProxy("http://myproxy:80", true);
        }

        [UdfMethod]
        public double GetDistanceBetweenTwoZipCodes(int zip1, int zip2)
        {
            string zip1String = Convert.ToString(zip1);
            string zip2String = Convert.ToString(zip2);

            return (distanceService.getDistance(zip1String, zip2String));
        }

        [UdfMethod]
        public string GetCityFromZip(int zip)
        {
            string zipString = Convert.ToString(zip);

            return (distanceService.getCity(zipString));
        }

        [UdfMethod]
        public string GetStateFromZip(int zip)
        {
            string zipString = Convert.ToString(zip);

            return (distanceService.getState(zipString));
        }

        [UdfMethod]
        public string GetLocationFromZip(int zip)
        {
            string zipString = Convert.ToString(zip);

            return (distanceService.getLocation(zipString));
        }

        [UdfMethod]
        public double GetLatitudeFromZip(int zip)
        {
            string zipString = Convert.ToString(zip);

            return (distanceService.getLatitude(zipString));
        }

        [UdfMethod]
        public double GetLongitudeFromZip(int zip)
        {
            string zipString = Convert.ToString(zip);

            return (distanceService.getLongitude(zipString));
        }

        [UdfMethod]
        public string ToDegreeNotation(double angle)
        {
            int deg = (int)angle;
            double minutesAndSeconds = Math.Abs(angle - deg) * 60;
            int minutes = (int)minutesAndSeconds;
            int seconds = (int)(Math.Abs(minutesAndSeconds - minutes) * 60);

            return deg.ToString() + "°" + minutes.ToString() + "\\'" + seconds.ToString() + "\"";
        }
    }
}
```




```VB.net

Imports System
Imports System.Collections.Generic
Imports System.Text
Imports System.Net
Imports Microsoft.Office.Excel.Server.Udf
Imports ZipCodes.com.imacination.webservices

Namespace ZipCodeUdfSample
    <UdfClass> _
    Public Class ZipCodeUdfs
        Private distanceService As DistanceService = Nothing

        Public Sub New()
            Me.distanceService = New DistanceService()
            'this.distanceService.Proxy = new WebProxy("http://myproxy:80", true);
        End Sub

        <UdfMethod> _
        Public Function GetDistanceBetweenTwoZipCodes(ByVal zip1 As Integer, ByVal zip2 As Integer) As Double
            Dim zip1String As String = Convert.ToString(zip1)
            Dim zip2String As String = Convert.ToString(zip2)

            Return (distanceService.getDistance(zip1String, zip2String))
        End Function

        <UdfMethod> _
        Public Function GetCityFromZip(ByVal zip As Integer) As String
            Dim zipString As String = Convert.ToString(zip)

            Return (distanceService.getCity(zipString))
        End Function

        <UdfMethod> _
        Public Function GetStateFromZip(ByVal zip As Integer) As String
            Dim zipString As String = Convert.ToString(zip)

            Return (distanceService.getState(zipString))
        End Function

        <UdfMethod> _
        Public Function GetLocationFromZip(ByVal zip As Integer) As String
            Dim zipString As String = Convert.ToString(zip)

            Return (distanceService.getLocation(zipString))
        End Function

        <UdfMethod> _
        Public Function GetLatitudeFromZip(ByVal zip As Integer) As Double
            Dim zipString As String = Convert.ToString(zip)

            Return (distanceService.getLatitude(zipString))
        End Function

        <UdfMethod> _
        Public Function GetLongitudeFromZip(ByVal zip As Integer) As Double
            Dim zipString As String = Convert.ToString(zip)

            Return (distanceService.getLongitude(zipString))
        End Function

        <UdfMethod> _
        Public Function ToDegreeNotation(ByVal angle As Double) As String
            Dim deg As Integer = CInt(Fix(angle))
            Dim minutesAndSeconds As Double = Math.Abs(angle - deg) * 60
            Dim minutes As Integer = CInt(Fix(minutesAndSeconds))
            Dim seconds As Integer = CInt(Fix(Math.Abs(minutesAndSeconds - minutes) * 60))

            Return deg.ToString() &amp; "°" &amp; minutes.ToString() &amp; "'" &amp; seconds.ToString() &amp; """"
        End Function
    End Class
End Namespace
```


## <a name="see-also"></a><span data-ttu-id="68235-121">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="68235-121">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="68235-122">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="68235-122">Tasks</span></span>


  
    
    
 [<span data-ttu-id="68235-123">Step 1: Creating a Project and Adding a UDF Reference</span><span class="sxs-lookup"><span data-stu-id="68235-123">Step 1: Creating a Project and Adding a UDF Reference</span></span>](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [<span data-ttu-id="68235-124">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="68235-124">Step 2: Creating a Managed-Code UDF</span></span>](step-2-creating-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="68235-125">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="68235-125">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [<span data-ttu-id="68235-126">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="68235-126">Step 4: Testing and Calling UDFs from Cells</span></span>](step-4-testing-and-calling-udfs-from-cells.md)
#### <a name="concepts"></a><span data-ttu-id="68235-127">Konzepte</span><span class="sxs-lookup"><span data-stu-id="68235-127">Concepts</span></span>


  
    
    
 [<span data-ttu-id="68235-128">Accessing the SOAP API</span><span class="sxs-lookup"><span data-stu-id="68235-128">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
#### <a name="other-resources"></a><span data-ttu-id="68235-129">Sonstige Ressourcen</span><span class="sxs-lookup"><span data-stu-id="68235-129">Other resources</span></span>


  
    
    
 [<span data-ttu-id="68235-130">Step 2: Adding a Web Reference</span><span class="sxs-lookup"><span data-stu-id="68235-130">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="68235-131">Step 3: Accessing the Web Service</span><span class="sxs-lookup"><span data-stu-id="68235-131">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="68235-132">Walkthrough: Developing a Custom Application Using Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="68235-132">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
