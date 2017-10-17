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
# <a name="how-to-deploy-a-claims-provider-in-sharepoint"></a>Vorgehensweise: POST eines anspruchsanbieters in SharePoint
In diesem Artikel erfahren Sie, wie Sie einen SharePoint-Anspruchsanbieter mithilfe der Featureinfrastruktur und durch Erstellen einer Klasse, die von  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) erbt, bereitstellen.
## <a name="deploying-a-claims-provider-as-part-of-a-setup"></a>Bereitstellen eines Anspruchsanbieters im Rahmen einer Installation
<a name="SP15_HowToDeployClaimsProvider_DeployingClaimsSetup"> </a>

Die einfachste Möglichkeit zum Bereitstellen eines Anspruchsanbieters wird mithilfe der Features-Infrastruktur. Zu diesem Zweck zunächst definieren Sie ein Feature und ein Featureempfänger, der von der  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) -Klasse abgeleitet ist, und überschreiben Sie die Basiseigenschaften.
  
    
    
Der folgende Code bietet ein Beispiel für diese Vorgehensweise.
  
    
    



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


## <a name="deploying-a-claims-provider-using-the-feature-infrastructure"></a>Bereitstellen eines Forderungsanbieters mithilfe der Featureinfrastruktur
<a name="SP15_HowToDeployClaimsProvider_DeployingClaimsFeature"> </a>

Es folgt ein Beispiel, das veranschaulicht, wie ein Feature und ein Featureempfänger, der von  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) abgeleitet wird, und überschreiben die Basiseigenschaften definieren.
  
    
    

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


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_HowToDeployClaimsProvider_AdditionalResources"> </a>


-  [Anspruchsbasierte Identität in SharePoint](claims-based-identity-in-sharepoint.md)
    
  
-  [Eingehende Ansprüche: Anmelden bei SharePoint](incoming-claims-signing-into-sharepoint.md)
    
  
-  [Anspruchsanbieter in SharePoint](claims-provider-in-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen ein anspruchsanbieters in SharePoint](how-to-create-a-claims-provider-in-sharepoint.md)
    
  

