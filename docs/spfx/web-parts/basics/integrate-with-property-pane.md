---
title: Machen Sie Ihr clientseitiges SharePoint-Webpart konfigurierbar
description: Konfigurieren Sie benutzerdefinierte Eigenschaften in Ihrem Webpart mithilfe des Eigenschaftenbereichs.
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: cfb2686d46058cd1bf97321c7928576ba96cf875
ms.sourcegitcommit: 1f1044e59d987d878bb8bc403413e3090234ad44
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/11/2018
---
# <a name="make-your-sharepoint-client-side-web-part-configurable"></a><span data-ttu-id="a5d24-103">Machen Sie Ihr clientseitiges SharePoint-Webpart konfigurierbar</span><span class="sxs-lookup"><span data-stu-id="a5d24-103">Make your SharePoint client-side web part configurable</span></span>

<span data-ttu-id="a5d24-104">Im Eigenschaftenbereich können Endbenutzer das Webpart mit einer Reihe von Eigenschaften konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="a5d24-104">The property pane allows end users to configure the web part with several properties.</span></span> <span data-ttu-id="a5d24-105">Im Artikel [Erstellen Ihres ersten Webparts](../get-started/build-a-hello-world-web-part.md) wird beschrieben, wie der Eigenschaftenbereich in der **HelloWorldWebPart**-Klasse definiert ist.</span><span class="sxs-lookup"><span data-stu-id="a5d24-105">The property pane allows end users to configure the web part with a bunch of properties. The article [Build your first web part](../get-started/build-a-hello-world-web-part.md) describes how the property pane is defined in the **HelloWorldWebPart** class. The property pane properties are defined in  propertyPaneSettings.</span></span> <span data-ttu-id="a5d24-106">Die Eigenschaften des Eigenschaftenbereichs sind in **propertyPaneSettings** definiert.</span><span class="sxs-lookup"><span data-stu-id="a5d24-106">The property pane properties are defined in **propertyPaneSettings**.</span></span>

<span data-ttu-id="a5d24-107">Ein Eigenschaftenbereich weist drei wichtige Metadaten auf: eine Seite, einen optionalen Header und mindestens eine Gruppe.</span><span class="sxs-lookup"><span data-stu-id="a5d24-107">A property pane should contain a page, an optional header, and at least one group.</span></span> 

- <span data-ttu-id="a5d24-108">Über **Seiten** haben Sie die Flexibilität, komplexe Interaktionen zu trennen und diese auf einer oder mehreren Seiten zu platzieren.</span><span class="sxs-lookup"><span data-stu-id="a5d24-108">Pages provide you the flexibility to separate complex interactions and put them into one or more pages. Pages then contain Header and Groups.</span></span> <span data-ttu-id="a5d24-109">Seiten enthalten dann eine Kopfzeile und Gruppen.</span><span class="sxs-lookup"><span data-stu-id="a5d24-109">Pages contain a header and groups.</span></span>
- <span data-ttu-id="a5d24-110">**Kopfzeilen** ermöglichen es Ihnen, den Titel des im Eigenschaftenbereich zu definieren.</span><span class="sxs-lookup"><span data-stu-id="a5d24-110">**Headers** allow you to define the title of the property pane.</span></span> 
- <span data-ttu-id="a5d24-111">**Gruppen** ermöglichen es Ihnen, die verschiedenen Abschnitte oder Felder für die Eigenschaftenbereiche zu definieren, über die Sie Ihre Feldsätze gruppieren können.</span><span class="sxs-lookup"><span data-stu-id="a5d24-111">Header allows you to define the title of the property pane and Groups let you define the various sections for the property pane through which you want to group your field sets.</span></span>  

<span data-ttu-id="a5d24-112">Die folgende Abbildung zeigt ein Beispiel für einen Eigenschaftenbereich in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a5d24-112">The following figure shows an example of a property pane in SharePoint.</span></span>

![Beispiel für Eigenschaftenbereich](../../../images/property-pane-example.png)

## <a name="configure-the-property-pane"></a><span data-ttu-id="a5d24-114">Konfigurieren des Eigenschaftenbereichs</span><span class="sxs-lookup"><span data-stu-id="a5d24-114">Configure the Web part property pane</span></span>

<span data-ttu-id="a5d24-p103">Im folgenden Codebeispiel wird der Eigenschaftenbereich in Ihrem Webpart initialisiert und konfiguriert. Sie setzen die Methode **getPropertyPaneConfiguration** außer Kraft und geben eine Auflistung der Eigenschaftbereichsseite(n) zurück.</span><span class="sxs-lookup"><span data-stu-id="a5d24-p103">The following code example initializes and configures the property pane in your web part. You override the **getPropertyPaneConfiguration** method and return a collection of property pane page(s).</span></span>

```ts
protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
  return {
    pages: [
      {
        header: {
          description: strings.PropertyPaneDescription
        },
        groups: [
          {
            groupName: strings.BasicGroupName,
            groupFields: [
              PropertyPaneTextField('description', {
                label: strings.DescriptionFieldLabel
              })
            ]
          }
        ]
      }
    ]
  };
}
```

### <a name="property-pane-fields"></a><span data-ttu-id="a5d24-117">Felder des Eigenschaftenbereichs</span><span class="sxs-lookup"><span data-stu-id="a5d24-117">Property pane fields</span></span>

<span data-ttu-id="a5d24-118">Die folgenden Feldtypen werden unterstützt:</span><span class="sxs-lookup"><span data-stu-id="a5d24-118">The following field types are supported:</span></span>

* <span data-ttu-id="a5d24-119">Schaltfläche</span><span class="sxs-lookup"><span data-stu-id="a5d24-119">Button</span></span>
* <span data-ttu-id="a5d24-120">Kontrollkästchen</span><span class="sxs-lookup"><span data-stu-id="a5d24-120">Checkbox</span></span>
* <span data-ttu-id="a5d24-121">Auswahlgruppe</span><span class="sxs-lookup"><span data-stu-id="a5d24-121">Choice group</span></span>
* <span data-ttu-id="a5d24-122">Dropdown</span><span class="sxs-lookup"><span data-stu-id="a5d24-122">Dropdown</span></span>
* <span data-ttu-id="a5d24-123">Horizontales Lineal</span><span class="sxs-lookup"><span data-stu-id="a5d24-123">Horizontal rule</span></span>
* <span data-ttu-id="a5d24-124">Beschriftung</span><span class="sxs-lookup"><span data-stu-id="a5d24-124">Label</span></span>
* <span data-ttu-id="a5d24-125">Link</span><span class="sxs-lookup"><span data-stu-id="a5d24-125">Link</span></span>
* <span data-ttu-id="a5d24-126">Schieberegler</span><span class="sxs-lookup"><span data-stu-id="a5d24-126">Slider</span></span>
* <span data-ttu-id="a5d24-127">Textfeld</span><span class="sxs-lookup"><span data-stu-id="a5d24-127">Textbox</span></span>
* <span data-ttu-id="a5d24-128">Mehrzeiliges Textfeld</span><span class="sxs-lookup"><span data-stu-id="a5d24-128">Multi-line Textbox</span></span>
* <span data-ttu-id="a5d24-129">Umschaltfläche</span><span class="sxs-lookup"><span data-stu-id="a5d24-129">Toggle</span></span>
* <span data-ttu-id="a5d24-130">Benutzerdefiniert</span><span class="sxs-lookup"><span data-stu-id="a5d24-130">Custom</span></span>

<span data-ttu-id="a5d24-p104">Die Feldtypen sind in **sp-client-platform** als Module verfügbar. Bevor sie im Code verwendet werden können, müssen sie importiert werden:</span><span class="sxs-lookup"><span data-stu-id="a5d24-p104">The field types are available as modules in **sp-client-platform**. They require an import before you can use them in your code:</span></span>

```ts
import {
  PropertyPaneTextField,
  PropertyPaneCheckbox,
  PropertyPaneLabel,
  PropertyPaneLink,
  PropertyPaneSlider,
  PropertyPaneToggle,
  PropertyPaneDropdown
} from '@microsoft/sp-webpart-base';
```

<span data-ttu-id="a5d24-133">Jede Feldtypmethode ist wie folgt definiert, wobei **PropertyPaneTextField** als Beispiel verwendet wird:</span><span class="sxs-lookup"><span data-stu-id="a5d24-133">Every field type method is defined as follows, taking **PropertyPaneTextField** as an example:</span></span>

```ts
PropertyPaneTextField('targetProperty',{
  //field properties are defined here
})
```

<span data-ttu-id="a5d24-134">**targetProperty** definiert das zugeordnete Objekt für diesen Feldtyp und ist auch in der Eigenschaftenschnittstelle Ihres Webparts definiert.</span><span class="sxs-lookup"><span data-stu-id="a5d24-134">**targetProperty** defines the associated object for that field type and is also defined in the props interface in your web part.</span></span>

<span data-ttu-id="a5d24-135">Um diesen Eigenschaften Typen zuzuordnen, definieren Sie eine Schnittstelle in Ihrer Webpartklasse, die eine oder mehrere Zieleigenschaften umfasst.</span><span class="sxs-lookup"><span data-stu-id="a5d24-135">To assign types to these properties, define an interface in your web part class that includes one or more target properties.</span></span>

```ts
export interface IHelloWorldWebPartProps {
    targetProperty: string
}
```

<span data-ttu-id="a5d24-136">Diese steht dann in Ihrem Webpart über die **this.properties.targetProperty** zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="a5d24-136">This is then available in your web part using **this.properties.targetProperty**.</span></span>

```ts
<p class="ms-font-l ms-fontColor-white">${this.properties.description}</p>
```

<span data-ttu-id="a5d24-137">Wenn die Eigenschaften definiert sind, können Sie in Ihrem Webpart mit der **this.properties.[Eigenschaftsname]** darauf zugreifen.</span><span class="sxs-lookup"><span data-stu-id="a5d24-137">When the properties are defined, you can access them in your web part using the **this.properties.[property-name]**. For details, see render method of the HelloWorldWebPart.</span></span> <span data-ttu-id="a5d24-138">Weitere Informationen finden Sie unter [Render-Methode von HelloWorldWebPart](../get-started/build-a-hello-world-web-part.md#web-part-render-method).</span><span class="sxs-lookup"><span data-stu-id="a5d24-138">For more information, see [render method of the HelloWorldWebPart](../get-started/build-a-hello-world-web-part.md#web-part-render-method).</span></span>

## <a name="handle-field-changes"></a><span data-ttu-id="a5d24-139">Behandeln von Feldänderungen</span><span class="sxs-lookup"><span data-stu-id="a5d24-139">Handle field changes</span></span>

<span data-ttu-id="a5d24-140">Der Eigenschaftenbereich besteht aus zwei Interaktionsmodi:</span><span class="sxs-lookup"><span data-stu-id="a5d24-140">The property pane has two interaction modes:</span></span>

* <span data-ttu-id="a5d24-141">Reaktiv</span><span class="sxs-lookup"><span data-stu-id="a5d24-141">Reactive</span></span>
* <span data-ttu-id="a5d24-142">Nicht reaktiv</span><span class="sxs-lookup"><span data-stu-id="a5d24-142">Non-reactive</span></span>

<span data-ttu-id="a5d24-p106">Im reaktiven Modus wird bei jeder Änderung ein Änderungsereignis ausgelöst. Durch das reaktive Verhalten wird das Webpart automatisch mit den neuen Werten aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="a5d24-p106">In reactive mode, on every change, a change event is triggered. Reactive behavior automatically updates the web part with the new values.</span></span>

<span data-ttu-id="a5d24-145">Der reaktive Modus ist zwar für viele Szenarios ausreichend, manchmal benötigen Sie aber das nicht reaktive Verhalten.</span><span class="sxs-lookup"><span data-stu-id="a5d24-145">While reactive mode is sufficient for many scenarios, at times you will need non-reactive behavior. Non-reactive does not update the web part automatically unless the user confirms the changes.</span></span> <span data-ttu-id="a5d24-146">Beim nicht reaktiven Verhalten wird das Webpart nicht automatisch aktualisiert, es sei denn, der Benutzer bestätigt die Änderungen.</span><span class="sxs-lookup"><span data-stu-id="a5d24-146">While reactive mode is sufficient for many scenarios, at times you will need non-reactive behavior. Non-reactive does not update the web part automatically unless the user confirms the changes.</span></span> 

<span data-ttu-id="a5d24-147">Fügen Sie den folgenden Code zu Ihrem Webpart hinzu, um den nicht reaktiven Modus zu aktivieren:</span><span class="sxs-lookup"><span data-stu-id="a5d24-147">To turn on the non-reactive mode, add the following code in your web part:</span></span>

```ts 
protected get disableReactivePropertyChanges(): boolean { 
  return true; 
}
```

## <a name="custom-property-pane-controls"></a><span data-ttu-id="a5d24-148">Benutzerdefinierte Eigenschaftenbereich-Steuerelemente</span><span class="sxs-lookup"><span data-stu-id="a5d24-148">Custom property pane controls</span></span>

<span data-ttu-id="a5d24-149">Das SharePoint Framework enthält eine Reihe von Standardsteuerelementen für den Eigenschaftenbereich.</span><span class="sxs-lookup"><span data-stu-id="a5d24-149">SharePoint Framework contains a set of standard controls for the property pane.</span></span> <span data-ttu-id="a5d24-150">Doch manchmal benötigen Sie zusätzliche Funktionen, die über die grundlegenden Steuerelemente hinausgehen.</span><span class="sxs-lookup"><span data-stu-id="a5d24-150">But sometimes you need additional functionality beyond the basic controls.</span></span> <span data-ttu-id="a5d24-151">Mit SharePoint Framework können Sie benutzerdefinierte Steuerelemente erstellen, um die erforderliche Funktionalität bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="a5d24-151">SharePoint Framework allows you to build custom controls to deliver the required functionality.</span></span> <span data-ttu-id="a5d24-152">Weitere Informationen finden Sie im Leitfaden [Erstellen benutzerdefinierter Steuerelemente für den Eigenschaftenbereich](../guidance/build-custom-property-pane-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a5d24-152">To learn more, read the [Build custom controls for the property pane](../guidance/build-custom-property-pane-controls.md) guide.</span></span>
