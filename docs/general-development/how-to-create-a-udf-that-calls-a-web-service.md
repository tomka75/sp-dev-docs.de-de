---
title: How to Create a UDF That Calls a Web Service
ms.date: 09/25/2017
keywords: how to,howdoi,howto,UDF
f1_keywords: how to,howdoi,howto,UDF
ms.prod: sharepoint
ms.assetid: 360c5766-4b5d-4a48-9f23-8955036924ce
ms.openlocfilehash: 3a5c92ead3b481e9462f33863027d827ea157baa
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-a-udf-that-calls-a-web-service"></a>How to: Create a UDF That Calls a Web Service

This example shows how to call an external Web service from a user-defined function (UDF). The Web service used in this example is:
  
    
    

 `http://webservices.imacination.com/distance/Distance.jws?wsdl` Sie müssen zum Erstellen dieses Beispiels Microsoft Visual Studio 2005 oder ein vergleichbares, mit Microsoft .NET Framework 2.0-kompatibles, Programm verwenden. 
  
    
    


> **Hinweis:** Stellen Sie vor dem Testen dieses Codes sicher, dass der aufzurufende Webdienst verfügbar ist. Möglicherweise steht der Webdienstserver nicht zur Verfügung oder der Webdienst wird nicht mehr unterstützt. Wenn der Webdienst nicht verfügbar ist, tritt bei den Webdienstaufrufen von Ihrem Code aus ein Fehler auf. Sie können überprüfen, ob ein Webdienst verfügbar ist, indem Sie die Website öffnen. In diesem Beispiel lautet die URL: > `http://webservices.imacination.com/distance/Distance.jws?wsdl`>. Wenn der Webdienst verfügbar ist, wird Web Services Description Language (WSDL) angezeigt. Wenn er nicht verfügbar ist, wird die übliche Fehlermeldung „Webseite nicht gefunden“ angezeigt. 
  
    
    


## <a name="example"></a>Beispiel

You can learn more about the Web service used in this example by examining its WSDL.
  
    
    
One service it provides is to return geographical coordinates in decimal form. In this sample, the  `ToDegreeNotation` function has been added to show how you can convert coordinates to degrees/minutes/seconds, which is more appropriate for displaying coordinates.
  
    
    



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

If your Internet Explorer LAN setting is configured to use a proxy server, your code must explicitly make a call to set the proxy server. Otherwise, your Web service calls will fail. You can set the proxy server in the constructor as follows:
  
    
    



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

For more information about how to test and call UDFs from cells, see  [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md).
  
    
    



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


## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [Step 1: Creating a Project and Adding a UDF Reference](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md)
  
    
    
 [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [Step 4: Testing and Calling UDFs from Cells](step-4-testing-and-calling-udfs-from-cells.md)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Accessing the SOAP API](accessing-the-soap-api.md)
#### <a name="other-resources"></a>Sonstige Ressourcen


  
    
    
 [Step 2: Adding a Web Reference](step-2-adding-a-web-reference.md)
  
    
    
 [Step 3: Accessing the Web Service](step-3-accessing-the-web-service.md)
  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)