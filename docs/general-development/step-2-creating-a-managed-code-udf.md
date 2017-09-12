---
title: Step 2 Creating a Managed-Code UDF
keywords: soap
f1_keywords: soap
ms.prod: SHAREPOINT
ms.assetid: 3c9edf82-ee2d-41f0-9d66-e88e8dc0cc69
ms.openlocfilehash: 1baa3fb29c7890b85c0b18f599922d41caef3e49
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="step-2-creating-a-managed-code-udf"></a><span data-ttu-id="f6a83-103">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="f6a83-103">Step 2: Creating a Managed-Code UDF</span></span>

<span data-ttu-id="f6a83-104">After you have added a reference to Microsoft.Office.Excel.Server.Udf.dll to your project, the next step is to create some custom functions and mark them with the Excel Services user-defined function (UDF) attributes.</span><span class="sxs-lookup"><span data-stu-id="f6a83-104">After you have added a reference to Microsoft.Office.Excel.Server.Udf.dll to your project, the next step is to create some custom functions and mark them with the Excel Services user-defined function (UDF) attributes.</span></span> 
  
    
    

<span data-ttu-id="f6a83-p101">You must mark your UDF class with the **Microsoft.Office.Excel.Server.Udf.UdfClass** attribute, and mark the UDF methods with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute. Any methods that are not marked with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute in the UDF assembly will be ignored, because they will not be considered UDF methods.</span><span class="sxs-lookup"><span data-stu-id="f6a83-p101">You must mark your UDF class with the **Microsoft.Office.Excel.Server.Udf.UdfClass** attribute, and mark the UDF methods with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute. Any methods that are not marked with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute in the UDF assembly will be ignored, because they will not be considered UDF methods.</span></span>
  
    
    

<span data-ttu-id="f6a83-p102">The **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute has an **IsVolatile** property. You use the **IsVolatile** property to specify a UDF method as volatile or nonvolatile. The **IsVolatile** property takes a Boolean value. The default value is **false**, which means that particular UDF method is nonvolatile.</span><span class="sxs-lookup"><span data-stu-id="f6a83-p102">The **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute has an **IsVolatile** property. You use the **IsVolatile** property to specify a UDF method as volatile or nonvolatile. The **IsVolatile** property takes a Boolean value. The default value is **false**, which means that particular UDF method is nonvolatile.</span></span> 
## <a name="creating-udfs"></a><span data-ttu-id="f6a83-111">Creating UDFs</span><span class="sxs-lookup"><span data-stu-id="f6a83-111">Creating UDFs</span></span>


### <a name="to-add-directives"></a><span data-ttu-id="f6a83-112">To add directives</span><span class="sxs-lookup"><span data-stu-id="f6a83-112">To add directives</span></span>


- <span data-ttu-id="f6a83-p103">The types to use are defined in the **Microsoft.Office.Excel.Server.Udf** namespace. Adding a **using** (or **Imports**) directive at the top of the Class1.cs file will allow you to use the types in **Microsoft.Office.Excel.Server.Udf** without having to fully qualify the types in the namespace.</span><span class="sxs-lookup"><span data-stu-id="f6a83-p103">The types to use are defined in the **Microsoft.Office.Excel.Server.Udf** namespace. Adding a **using** (or **Imports**) directive at the top of the Class1.cs file will allow you to use the types in **Microsoft.Office.Excel.Server.Udf** without having to fully qualify the types in the namespace.</span></span>
    
    <span data-ttu-id="f6a83-115">To add this directive, add the following code to the beginning of your code in the Class1.cs file, after  `using System.Text:`</span><span class="sxs-lookup"><span data-stu-id="f6a83-115">To add this directive, add the following code to the beginning of your code in the Class1.cs file, after  `using System.Text:`</span></span>
    


```cs
  
using Microsoft.Office.Excel.Server.Udf; 
```




```VB.net
  Imports Microsoft.Office.Excel.Server.Udf
```


### <a name="to-mark-a-udf-class-and-methods"></a><span data-ttu-id="f6a83-116">To mark a UDF class and methods</span><span class="sxs-lookup"><span data-stu-id="f6a83-116">To mark a UDF class and methods</span></span>


1. <span data-ttu-id="f6a83-117">Mark  `Class1` as a UDF class by adding the following attribute just above `public class Class1`:</span><span class="sxs-lookup"><span data-stu-id="f6a83-117">Mark  `Class1` as a UDF class by adding the following attribute just above `public class Class1`:</span></span> 
    
```cs
  [UdfClass]
```


```VB.net
  <UdfClass>_
```

2. <span data-ttu-id="f6a83-p104">Create a function that takes a number (of type **double**), and in the function, multiply the number by 9. The function is a UDF method that is nonvolatile. Add the following code to  `Class1`:</span><span class="sxs-lookup"><span data-stu-id="f6a83-p104">Create a function that takes a number (of type **double**), and in the function, multiply the number by 9. The function is a UDF method that is nonvolatile. Add the following code to  `Class1`:</span></span>
    
```cs
  [UdfMethod]
public double MyDouble(double d)
{
    return d * 9;
}
```


```VB.net
  
<UdfMethod> _
Public Function MyDouble(ByVal d As Double) As Double
    Return d * 9
End Function
```


    > **Note:**
      > The default value for the **IsVolatile** property is **false**, which means that particular UDF method is nonvolatile. Therefore, it is sufficient to mark a nonvolatile UDF method as  `[UdfMethod]`. It is not necessary to mark it as  `[UdfMethod(IsVolatile = false)]`. 
3. <span data-ttu-id="f6a83-p105">Create another function that returns the current date using the **System.DateTime.Today** property. The function is a UDF method that is volatile. Add the following code to `Class1`:</span><span class="sxs-lookup"><span data-stu-id="f6a83-p105">Create another function that returns the current date using the **System.DateTime.Today** property. The function is a UDF method that is volatile. Add the following code to `Class1`:</span></span>
    
```cs
  
[UdfMethod(IsVolatile = true)]
public DateTime ReturnDateTimeToday()
{
    return (DateTime.Today);
}      
```


```VB.net
  
<UdfMethod(IsVolatile := True)> _
Public Function ReturnDateTimeToday() As Date
    Return (Date.Today)
End Function
```


### <a name="to-build-the-project"></a><span data-ttu-id="f6a83-124">To build the project</span><span class="sxs-lookup"><span data-stu-id="f6a83-124">To build the project</span></span>


1. <span data-ttu-id="f6a83-125">On the **Build** menu, click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="f6a83-125">On the **Build** menu, click **Build Solution**.</span></span>
    
  
2. <span data-ttu-id="f6a83-126">You should find SampleUdf.dll assembly in the directory where you have saved your project.</span><span class="sxs-lookup"><span data-stu-id="f6a83-126">You should find SampleUdf.dll assembly in the directory where you have saved your project.</span></span> 
    
  

### <a name="complete-code"></a><span data-ttu-id="f6a83-127">Vollständiger Code</span><span class="sxs-lookup"><span data-stu-id="f6a83-127">Complete Code</span></span>

<span data-ttu-id="f6a83-128">The following code sample is the complete code in the Class1.cs example file described in the previous procedures.</span><span class="sxs-lookup"><span data-stu-id="f6a83-128">The following code sample is the complete code in the Class1.cs example file described in the previous procedures.</span></span>
  
    
    

```cs

using System;
using System.Collections.Generic;
using System.Text;
using Microsoft.Office.Excel.Server.Udf;

namespace SampleUdf
{
    [UdfClass]
    public class Class1
    {
        [UdfMethod]
        public double MyDouble(double d)
        {
            return d * 9;
        }  

        [UdfMethod(IsVolatile = true)]
        public DateTime ReturnDateTimeToday()
        {
            return (DateTime.Today);
        }
    }
}
```


```VB.net

Imports System
Imports System.Collections.Generic
Imports System.Text
Imports Microsoft.Office.Excel.Server.Udf

Namespace SampleUdf
    <UdfClass> _
    Public Class Class1
        <UdfMethod> _
        Public Function MyDouble(ByVal d As Double) As Double
            Return d * 9
        End Function

        <UdfMethod(IsVolatile := True)> _
        Public Function ReturnDateTimeToday() As Date
            Return (Date.Today)
        End Function
    End Class
End Namespace
```


## <a name="see-also"></a><span data-ttu-id="f6a83-129">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f6a83-129">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="f6a83-130">Aufgaben</span><span class="sxs-lookup"><span data-stu-id="f6a83-130">Tasks</span></span>


  
    
    
 [<span data-ttu-id="f6a83-131">Step 1: Creating a Project and Adding a UDF Reference</span><span class="sxs-lookup"><span data-stu-id="f6a83-131">Step 1: Creating a Project and Adding a UDF Reference</span></span>](step-1-creating-a-project-and-adding-a-udf-reference)
  
    
    
 [<span data-ttu-id="f6a83-132">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="f6a83-132">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs)
  
    
    
 [<span data-ttu-id="f6a83-133">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="f6a83-133">Step 4: Testing and Calling UDFs from Cells</span></span>](step-4-testing-and-calling-udfs-from-cells)
  
    
    
 [<span data-ttu-id="f6a83-134">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="f6a83-134">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service)
#### <a name="concepts"></a><span data-ttu-id="f6a83-135">Konzepte</span><span class="sxs-lookup"><span data-stu-id="f6a83-135">Concepts</span></span>


  
    
    
 [<span data-ttu-id="f6a83-136">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="f6a83-136">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf)
  
    
    
 [<span data-ttu-id="f6a83-137">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="f6a83-137">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs)
