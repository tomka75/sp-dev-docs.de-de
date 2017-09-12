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
# <a name="frequently-asked-questions-about-excel-services-udfs"></a><span data-ttu-id="e11cd-103">Häufig gestellte Fragen zu Excel Services-UDFs</span><span class="sxs-lookup"><span data-stu-id="e11cd-103">Frequently Asked Questions About Excel Services UDFs</span></span>

<span data-ttu-id="e11cd-104">Here are some frequently asked questions about Excel Services user-defined functions (UDFs).</span><span class="sxs-lookup"><span data-stu-id="e11cd-104">Here are some frequently asked questions about Excel Services user-defined functions (UDFs).</span></span> 
  
    
    


## <a name="creating-managed-code-udfs"></a><span data-ttu-id="e11cd-105">Creating Managed-Code UDFs</span><span class="sxs-lookup"><span data-stu-id="e11cd-105">Creating Managed-Code UDFs</span></span>


### <a name="what-is-a-supported-udf-class"></a><span data-ttu-id="e11cd-106">What is a supported UDF class?</span><span class="sxs-lookup"><span data-stu-id="e11cd-106">What is a supported UDF class?</span></span>

<span data-ttu-id="e11cd-p101">The UDF class in a UDF assembly must be public. It can be sealed. It cannot be abstract, internal, or private. It must have a parameterless, public constructor. For languages that automatically generate a parameterless, public constructor (for example, C#), you can have no constructor at all.</span><span class="sxs-lookup"><span data-stu-id="e11cd-p101">The UDF class in a UDF assembly must be public. It can be sealed. It cannot be abstract, internal, or private. It must have a parameterless, public constructor. For languages that automatically generate a parameterless, public constructor (for example, C#), you can have no constructor at all.</span></span>
  
    
    

### <a name="what-is-a-supported-udf-method"></a><span data-ttu-id="e11cd-112">What is a supported UDF method?</span><span class="sxs-lookup"><span data-stu-id="e11cd-112">What is a supported UDF method?</span></span>

<span data-ttu-id="e11cd-p102">The UDF method in a UDF assembly must be public. The UDF method must be thread-safe.</span><span class="sxs-lookup"><span data-stu-id="e11cd-p102">The UDF method in a UDF assembly must be public. The UDF method must be thread-safe.</span></span>
  
    
    
<span data-ttu-id="e11cd-115">A UDF method cannot have:</span><span class="sxs-lookup"><span data-stu-id="e11cd-115">A UDF method cannot have:</span></span> 
  
    
    

- <span data-ttu-id="e11cd-116">**ref** or **out** parameters</span><span class="sxs-lookup"><span data-stu-id="e11cd-116">**ref** or **out** parameters</span></span>
    
  
- <span data-ttu-id="e11cd-117">**retval** attributes</span><span class="sxs-lookup"><span data-stu-id="e11cd-117">**retval** attributes</span></span>
    
  
- <span data-ttu-id="e11cd-118">**Optional** arguments</span><span class="sxs-lookup"><span data-stu-id="e11cd-118">**Optional** arguments</span></span>
    
  
- <span data-ttu-id="e11cd-119">unsupported data types</span><span class="sxs-lookup"><span data-stu-id="e11cd-119">unsupported data types</span></span>
    
  
<span data-ttu-id="e11cd-p103">The UDF method must also have a supported return type. For a list of supported data types, see the "Data Types" section of this topic.</span><span class="sxs-lookup"><span data-stu-id="e11cd-p103">The UDF method must also have a supported return type. For a list of supported data types, see the "Data Types" section of this topic.</span></span>
  
    
    

### <a name="can-i-call-a-web-service-from-a-udf-assembly"></a><span data-ttu-id="e11cd-122">Can I call a Web service from a UDF assembly?</span><span class="sxs-lookup"><span data-stu-id="e11cd-122">Can I call a Web service from a UDF assembly?</span></span>

<span data-ttu-id="e11cd-p104">Yes. For an example, see the following UDF sample code. Also see  [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service).</span><span class="sxs-lookup"><span data-stu-id="e11cd-p104">Yes. For an example, see the following UDF sample code. Also see  [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service).</span></span>
  
    
    

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


## <a name="data-types"></a><span data-ttu-id="e11cd-126">Datentypen</span><span class="sxs-lookup"><span data-stu-id="e11cd-126">Data Types</span></span>


### <a name="what-are-the-data-types-that-can-be-used-as-udf-parameters"></a><span data-ttu-id="e11cd-127">What are the data types that can be used as UDF parameters?</span><span class="sxs-lookup"><span data-stu-id="e11cd-127">What are the data types that can be used as UDF parameters?</span></span>

<span data-ttu-id="e11cd-128">The supported data types are as follows:</span><span class="sxs-lookup"><span data-stu-id="e11cd-128">The supported data types are as follows:</span></span>
  
    
    

- <span data-ttu-id="e11cd-129">Numeric types: Double, Single, Int32, UInt32, Int16, UInt16, Byte, Sbyte</span><span class="sxs-lookup"><span data-stu-id="e11cd-129">Numeric types: Double, Single, Int32, UInt32, Int16, UInt16, Byte, Sbyte</span></span>
    
  
- <span data-ttu-id="e11cd-130">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e11cd-130">String</span></span>
    
  
- <span data-ttu-id="e11cd-131">Boolean</span><span class="sxs-lookup"><span data-stu-id="e11cd-131">Boolean</span></span>
    
  
- <span data-ttu-id="e11cd-132">Object arrays: one- or two- dimensional arrays, that is, object [] and object [,]</span><span class="sxs-lookup"><span data-stu-id="e11cd-132">Object arrays: one- or two- dimensional arrays, that is, object [] and object [,]</span></span>
    
  
- <span data-ttu-id="e11cd-133">DateTime</span><span class="sxs-lookup"><span data-stu-id="e11cd-133">DateTime</span></span> 
    
  

### <a name="what-are-the-supported-return-value-types"></a><span data-ttu-id="e11cd-134">What are the supported return value types?</span><span class="sxs-lookup"><span data-stu-id="e11cd-134">What are the supported return value types?</span></span>

<span data-ttu-id="e11cd-135">The supported return value types are as follows:</span><span class="sxs-lookup"><span data-stu-id="e11cd-135">The supported return value types are as follows:</span></span>
  
    
    

- <span data-ttu-id="e11cd-136">Numeric types: Double, Single, Int32, UInt32, Int16, UInt16, Byte, Sbyte</span><span class="sxs-lookup"><span data-stu-id="e11cd-136">Numeric types: Double, Single, Int32, UInt32, Int16, UInt16, Byte, Sbyte</span></span>
    
  
- <span data-ttu-id="e11cd-137">Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="e11cd-137">String</span></span>
    
  
- <span data-ttu-id="e11cd-138">Boolean</span><span class="sxs-lookup"><span data-stu-id="e11cd-138">Boolean</span></span>
    
  
- <span data-ttu-id="e11cd-139">Object arrays: one- or two-dimensional arrays, that is, object [], object [,], int[] and int[,])</span><span class="sxs-lookup"><span data-stu-id="e11cd-139">Object arrays: one- or two-dimensional arrays, that is, object [], object [,], int[] and int[,])</span></span>
    
  
- <span data-ttu-id="e11cd-140">DateTime</span><span class="sxs-lookup"><span data-stu-id="e11cd-140">DateTime</span></span> 
    
  
- <span data-ttu-id="e11cd-141">Object</span><span class="sxs-lookup"><span data-stu-id="e11cd-141">Object</span></span>
    
  

## <a name="xlls"></a><span data-ttu-id="e11cd-142">XLLs</span><span class="sxs-lookup"><span data-stu-id="e11cd-142">XLLs</span></span>


### <a name="are-xlls-supported"></a><span data-ttu-id="e11cd-143">Are XLLs supported?</span><span class="sxs-lookup"><span data-stu-id="e11cd-143">Are XLLs supported?</span></span>

<span data-ttu-id="e11cd-p105">Not directly. Excel Services will load and call only managed-code UDFs. However, you can write a managed-code wrapper to call the XLLs and deploy the XLLs to the server, together with the managed-code wrapper assembly.</span><span class="sxs-lookup"><span data-stu-id="e11cd-p105">Not directly. Excel Services will load and call only managed-code UDFs. However, you can write a managed-code wrapper to call the XLLs and deploy the XLLs to the server, together with the managed-code wrapper assembly.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="e11cd-147">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="e11cd-147">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="e11cd-148">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="e11cd-148">Tasks</span></span>


  
    
    
 [<span data-ttu-id="e11cd-149">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="e11cd-149">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service)
  
    
    
 [<span data-ttu-id="e11cd-150">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="e11cd-150">How to: Trust a Location</span></span>](how-to-trust-a-location)
  
    
    
 [<span data-ttu-id="e11cd-151">How to: Catch Exceptions</span><span class="sxs-lookup"><span data-stu-id="e11cd-151">How to: Catch Exceptions</span></span>](how-to-catch-exceptions)
#### <a name="concepts"></a><span data-ttu-id="e11cd-152">Konzepte</span><span class="sxs-lookup"><span data-stu-id="e11cd-152">Concepts</span></span>


  
    
    
 [<span data-ttu-id="e11cd-153">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="e11cd-153">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs)
  
    
    
 [<span data-ttu-id="e11cd-154">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="e11cd-154">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf)
  
    
    
 [<span data-ttu-id="e11cd-155">Excel Services-Architektur</span><span class="sxs-lookup"><span data-stu-id="e11cd-155">Excel Services Architecture</span></span>](excel-services-architecture)
  
    
    
 [<span data-ttu-id="e11cd-156">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="e11cd-156">Excel Services Alerts</span></span>](excel-services-alerts)
  
    
    
 [<span data-ttu-id="e11cd-157">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="e11cd-157">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips)
  
    
    
 [<span data-ttu-id="e11cd-158">Excel Services Best Practices</span><span class="sxs-lookup"><span data-stu-id="e11cd-158">Excel Services Best Practices</span></span>](excel-services-best-practices)
