---
title: "Häufig gestellte Fragen zu Excel Services-UDFs"
keywords: faqs
f1_keywords: faqs
ms.prod: SHAREPOINT
ms.assetid: 3d94d040-eecf-4f8e-a316-6d1cca95e7eb
ms.openlocfilehash: 292b8486009585961a3568b9c7d56c550df6711a
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="frequently-asked-questions-about-excel-services-udfs"></a>Häufig gestellte Fragen zu Excel Services-UDFs

Here are some frequently asked questions about Excel Services user-defined functions (UDFs). 
  
    
    


## <a name="creating-managed-code-udfs"></a>Creating Managed-Code UDFs


### <a name="what-is-a-supported-udf-class"></a>What is a supported UDF class?

The UDF class in a UDF assembly must be public. It can be sealed. It cannot be abstract, internal, or private. It must have a parameterless, public constructor. For languages that automatically generate a parameterless, public constructor (for example, C#), you can have no constructor at all.
  
    
    

### <a name="what-is-a-supported-udf-method"></a>What is a supported UDF method?

The UDF method in a UDF assembly must be public. The UDF method must be thread-safe.
  
    
    
A UDF method cannot have: 
  
    
    

- **ref** or **out** parameters
    
  
- **retval** attributes
    
  
- **Optional** arguments
    
  
- unsupported data types
    
  
The UDF method must also have a supported return type. For a list of supported data types, see the "Data Types" section of this topic.
  
    
    

### <a name="can-i-call-a-web-service-from-a-udf-assembly"></a>Can I call a Web service from a UDF assembly?

Yes. For an example, see the following UDF sample code. Also see  [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service).
  
    
    

```cs

using System;
using System.Collections.Generic;
using System.Text;
using Microsoft.Office.Excel.Server.Udf;
using UdfWS.dk.iter.webservices;

namespace UdfWS
{
    [UdfClass]
    public class MyUdfClass
    {
        // Instantiate the Web service. The Web service used is at   
        // http://webservices.iter.dk/calculator.asmx
        Calculator calc = new Calculator();

        [UdfMethod]
        public int MyFunction()
        {
            int i;
            i = (i + 88) * 2;
            return i;
        }

        [UdfMethod(IsVolatile = true)]
        public double MyDouble(double d)
        {
            return d * 9;
        }

        [UdfMethod]
        public int AddMe(int a, int b)
        {
            int c;
            // Call the Web service Add method
            c = calc.Add(a, b);
            return c;
        }        
    }
}
```


```VB.net

Imports System
Imports System.Collections.Generic
Imports System.Text
Imports Microsoft.Office.Excel.Server.Udf
Imports UdfWS.dk.iter.webservices

Namespace UdfWS
    <UdfClass> _
    Public Class MyUdfClass
        ' Instantiate the Web service. The Web service used is at   
        ' http://webservices.iter.dk/calculator.asmx
        Private calc As New Calculator()

        <UdfMethod> _
        Public Function MyFunction() As Integer
            Dim i As Integer
            i = (i + 88) * 2
            Return i
        End Function

        <UdfMethod(IsVolatile := True)> _
        Public Function MyDouble(ByVal d As Double) As Double
            Return d * 9
        End Function

        <UdfMethod> _
        Public Function AddMe(ByVal a As Integer, ByVal b As Integer) As Integer
            Dim c As Integer
            ' Call the Web service Add method
            c = calc.Add(a, b)
            Return c
        End Function
    End Class
End Namespace
```


## <a name="data-types"></a>Datentypen


### <a name="what-are-the-data-types-that-can-be-used-as-udf-parameters"></a>What are the data types that can be used as UDF parameters?

The supported data types are as follows:
  
    
    

- Numeric types: Double, Single, Int32, UInt32, Int16, UInt16, Byte, Sbyte
    
  
- Zeichenfolge
    
  
- Boolean
    
  
- Object arrays: one- or two- dimensional arrays, that is, object [] and object [,]
    
  
- DateTime 
    
  

### <a name="what-are-the-supported-return-value-types"></a>What are the supported return value types?

The supported return value types are as follows:
  
    
    

- Numeric types: Double, Single, Int32, UInt32, Int16, UInt16, Byte, Sbyte
    
  
- Zeichenfolge
    
  
- Boolean
    
  
- Object arrays: one- or two-dimensional arrays, that is, object [], object [,], int[] and int[,])
    
  
- DateTime 
    
  
- Object
    
  

## <a name="xlls"></a>XLLs


### <a name="are-xlls-supported"></a>Are XLLs supported?

Not directly. Excel Services will load and call only managed-code UDFs. However, you can write a managed-code wrapper to call the XLLs and deploy the XLLs to the server, together with the managed-code wrapper assembly.
  
    
    

## <a name="see-also"></a>Siehe auch


#### <a name="tasks"></a>Aufgaben


  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service)
  
    
    
 [How to: Trust a Location](how-to-trust-a-location)
  
    
    
 [How to: Catch Exceptions](how-to-catch-exceptions)
#### <a name="concepts"></a>Konzepte


  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs)
  
    
    
 [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf)
  
    
    
 [Excel Services-Architektur](excel-services-architecture)
  
    
    
 [Excel Services Alerts](excel-services-alerts)
  
    
    
 [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips)
  
    
    
 [Excel Services Best Practices](excel-services-best-practices)
