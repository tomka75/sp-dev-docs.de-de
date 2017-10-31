---
title: Vorgehensweise POST eines anspruchsanbieters in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3a5fcedc-aa9a-4ff4-95c0-0e0a7dea9d1f
ms.openlocfilehash: bdf882e8a6e59a74c351f2c76427442fcd790fcf
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-deploy-a-claims-provider-in-sharepoint"></a><span data-ttu-id="b1df1-102">Vorgehensweise: POST eines anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1df1-102">How to: Deploy a claims provider in SharePoint</span></span>
<span data-ttu-id="b1df1-103">In diesem Artikel erfahren Sie, wie Sie einen SharePoint-Anspruchsanbieter mithilfe der Featureinfrastruktur und durch Erstellen einer Klasse, die von  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) erbt, bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="b1df1-103">Learn how to deploy a SharePoint claims provider by using the features infrastructure and creating a class that inherits from  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) .</span></span>
## <a name="deploying-a-claims-provider-as-part-of-a-setup"></a><span data-ttu-id="b1df1-104">Bereitstellen eines Anspruchsanbieters im Rahmen einer Installation</span><span class="sxs-lookup"><span data-stu-id="b1df1-104">Deploying a claims provider as part of a setup</span></span>
<span data-ttu-id="b1df1-105"><a name="SP15_HowToDeployClaimsProvider_DeployingClaimsSetup"> </a></span><span class="sxs-lookup"><span data-stu-id="b1df1-105"><a name="SP15_HowToDeployClaimsProvider_DeployingClaimsSetup"> </a></span></span>

<span data-ttu-id="b1df1-p101">Die einfachste Möglichkeit zum Bereitstellen eines Anspruchsanbieters wird mithilfe der Features-Infrastruktur. Zu diesem Zweck zunächst definieren Sie ein Feature und ein Featureempfänger, der von der  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) -Klasse abgeleitet ist, und überschreiben Sie die Basiseigenschaften.</span><span class="sxs-lookup"><span data-stu-id="b1df1-p101">The easiest way to deploy a claims provider is by using the features infrastructure. To do this, first define a feature and a feature receiver that derives from the  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) class, and override the base properties.</span></span>
  
    
    
<span data-ttu-id="b1df1-108">Der folgende Code bietet ein Beispiel für diese Vorgehensweise.</span><span class="sxs-lookup"><span data-stu-id="b1df1-108">The following is an example of how to do this.</span></span>
  
    
    



```cs

public class MyClaimProviderFeatureReceiver : SPClaimProviderFeatureReceiver
    {
        public override string ClaimProviderAssembly { get { return typeof(MyClaimProvider).Assembly.FullName; } }
        public override string ClaimProviderType { get { return typeof(MyClaimProvider).FullName; } }
        public override string ClaimProviderDisplayName
        {
            get
            {
                return StringResourceManager.GetString(MyLocalizedClaimProviderName);
            }
        }
        public override string ClaimProviderDescription
        {
            get
            {
                return StringResourceManager.GetString(MyLocalizedClaimProviderDescription);
            }
            }
    }
```


## <a name="deploying-a-claims-provider-using-the-feature-infrastructure"></a><span data-ttu-id="b1df1-109">Bereitstellen eines Forderungsanbieters mithilfe der Featureinfrastruktur</span><span class="sxs-lookup"><span data-stu-id="b1df1-109">Deploying a claims provider using the feature infrastructure</span></span>
<span data-ttu-id="b1df1-110"><a name="SP15_HowToDeployClaimsProvider_DeployingClaimsFeature"> </a></span><span class="sxs-lookup"><span data-stu-id="b1df1-110"><a name="SP15_HowToDeployClaimsProvider_DeployingClaimsFeature"> </a></span></span>

<span data-ttu-id="b1df1-111">Es folgt ein Beispiel, das veranschaulicht, wie ein Feature und ein Featureempfänger, der von  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) abgeleitet wird, und überschreiben die Basiseigenschaften definieren.</span><span class="sxs-lookup"><span data-stu-id="b1df1-111">The following is a sample that demonstrates how to define a feature and a feature receiver that derives from  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) and override the base properties.</span></span>
  
    
    

```cs

// Sample claims provider feature receiver class through which
// the sample claims provider registers itself 
// with the Microsoft.SharePoint.Administration.Claims.SPClaimProviderManager class.

using System;
using Microsoft.SharePoint.Administration;
using Microsoft.SharePoint.Administration.Claims;

namespace MySample.Sample.Server.SampleClaimsProvider
{
    /// <summary>
    /// The NameIdentifierClaimProviderFeatureReceiver class is a feature receiver class
    /// that registers the claims provider with the claims provider manager.
    /// </summary>
    
    [Microsoft.SharePoint.Security.SharePointPermission(System.Security.Permissions.SecurityAction.Demand, ObjectModel = true)]
    public sealed class NameIdentifierClaimProviderFeatureReceiver : SPClaimProviderFeatureReceiver
    {
        #region Private Methods
        /// <summary>
        /// Because use of base keyword can lead to unverifiable code inside a lambda expression, 
        /// this function is created as a wrapper for the base.FeatureActivated function.
        /// This function gets called in the following lambda expression.
        /// </summary>
        
        /// <param name="properties">Represents the properties of a feature activation.</param>
        /// <returns> void </returns>

        private void ExecBaseFeatureActivated(Microsoft.SharePoint.SPFeatureReceiverProperties properties)
        {
            base.FeatureActivated(properties);
        }
        #endregion Private Methods

        #region Public Method\\Properties
        /// <summary>
        /// Gets the fully qualified name of the MySample.Sample.Server.SampleClaimsProvider assembly.
        /// </summary>
        
        /// <returns>String representing fully qualified name of the MySample.Sample.Server.SampleClaimsProvider
        /// assembly.</returns>
        public override string ClaimProviderAssembly
        {
            get{ return typeof(SampleNameIdClaimProvider).Assembly.FullName; }
        }

        /// <summary>
        /// Gets the fully qualified name of the claims provider type, including the namespace of the type. 
        /// </summary>
        /// <returns>String representing the fully qualified name of the 
        ///SampleNameIdClaimProvider class.</returns>
        public override string ClaimProviderType
        {
            get{ return typeof(NameIdentifierClaimProvider).FullName; }
        }

        /// <summary>
        /// Gets the display name of the claims provider.
        /// </summary>
        
        /// <returns>String representing display name of the claim provider.</returns>
        public override string ClaimProviderDisplayName
        {
            get{ return "Sample NameId Claim Provider"; }
        }

        /// <summary>
        /// Gets the description about the claims provider. 
        /// </summary>
        
        /// <returns>String representing the description about the SampleClaimProvider.</returns>
        public override string ClaimProviderDescription
        {
            get
            {
                return "This feature adds SampleNameId claim type in the SAML token created by the STS.";
            }
        }

        /// <summary>
        /// This methods gets called after the activation of the feature.
        /// </summary>
        
        /// <param name="properties">Represents the properties of a feature activation<./param>
        /// <returns>void.</returns>
        public override void FeatureActivated(Microsoft.SharePoint.SPFeatureReceiverProperties properties)
        {     
            {
                ExecBaseFeatureActivated(properties);
            }            
        }
        #endregion Public Method\\Properties
    }
}

```


## <a name="additional-resources"></a><span data-ttu-id="b1df1-112">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="b1df1-112">Additional resources</span></span>
<span data-ttu-id="b1df1-113"><a name="SP15_HowToDeployClaimsProvider_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="b1df1-113"><a name="SP15_HowToDeployClaimsProvider_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="b1df1-114">Anspruchsbasierte Identität in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1df1-114">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b1df1-115">Eingehende Ansprüche: Anmelden bei SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1df1-115">Incoming claims: Signing into SharePoint</span></span>](incoming-claims-signing-into-sharepoint.md)
    
  
-  [<span data-ttu-id="b1df1-116">Anspruchsanbieter in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1df1-116">Claims provider in SharePoint</span></span>](claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b1df1-117">Vorgehensweise: Erstellen ein anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1df1-117">How to: Create a claims provider in SharePoint</span></span>](how-to-create-a-claims-provider-in-sharepoint.md)
    
  

