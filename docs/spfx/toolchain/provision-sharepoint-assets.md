---
title: "Bereitstellen von SharePoint-Objekten mit dem Lösungspaket"
description: "Mit der SharePoint-Framework-Toolkette können Sie SharePoint-Elemente mit ihrem clientseitigen Lösungspaket verpacken und bereitstellen. Diese Elemente werden dann bereitgestellt werden, wenn die clientseitige Lösung auf einer Website installiert wird."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 03d69afdc7f66a9c1e95a4832b4f591a79b998aa
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2018
---
# <a name="provision-sharepoint-assets-with-your-solution-package"></a><span data-ttu-id="3e8f1-104">Bereitstellen von SharePoint-Objekten mit dem Lösungspaket</span><span class="sxs-lookup"><span data-stu-id="3e8f1-104">Provision SharePoint assets with your solution package</span></span>

<span data-ttu-id="3e8f1-105">Manchmal müssen Sie vielleicht eine SharePoint-Liste oder einer Dokumentbibliothek zusammen mit Ihrem clientseitigen Lösungspaket bereitstellen, damit die Liste oder Bibliothek für Ihre clientseitigen Komponenten, z. B. Webparts, verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-105">At times, you may need to provision a SharePoint list or a document library along with your client-side solution package so that that list or library is available for your client-side components, such as web parts. SharePoint Framework toolchain allows you to package and deploy SharePoint items with your client-side solution package. These items are then provisioned when the client-side solution is installed on a site.</span></span> <span data-ttu-id="3e8f1-106">Mit der SharePoint-Framework-Toolkette können Sie SharePoint-Elemente mit ihrem clientseitigen Lösungspaket verpacken und bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-106">SharePoint Framework toolchain allows you to package and deploy SharePoint items with your client-side solution package.</span></span> <span data-ttu-id="3e8f1-107">Diese Elemente werden dann bereitgestellt werden, wenn die clientseitige Lösung auf einer Website installiert wird.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-107">These items are then provisioned when the client-side solution is installed on a site.</span></span> 

<span data-ttu-id="3e8f1-108">Details zu den Bereitstellungsoptionen finden Sie auch in diesem SharePoint PnP-Webcast im [YouTube-Kanal von SharePoint PnP](https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS).</span><span class="sxs-lookup"><span data-stu-id="3e8f1-108">You can also find details on the provisioning options from a SharePoint PnP webcast available from [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS).</span></span> 

<a href="https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS">
<img src="../../images/spfx-webcast-youtube-provision-feature-elements.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="provision-items-using-javascript-code"></a><span data-ttu-id="3e8f1-109">Bereitstellen von Elementen mithilfe von JavaScript-Code</span><span class="sxs-lookup"><span data-stu-id="3e8f1-109">Provisioning items using JavaScript code</span></span>

<span data-ttu-id="3e8f1-110">Es ist zwar möglich, SharePoint-Elemente mithilfe von JavaScript-Code in Ihrer Komponente, z. B. Webparts, zu erstellen, dies ist jedoch auf den Kontext des aktuellen Benutzers beschränkt, der diese Komponente verwendet.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-110">While it is possible to create SharePoint items using JavaScript code in your component, such as web parts, it is limited to the context of the current user using that component.</span></span> <span data-ttu-id="3e8f1-111">Wenn der Benutzer nicht über ausreichende Berechtigungen zum Erstellen oder Ändern von SharePoint-Elementen verfügt, stellt der JavaScript-Code diese Elemente nicht bereit.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-111">If the user doesn't have sufficient permissions to create or modify SharePoint items, the JavaScript code does not provision those items.</span></span> <span data-ttu-id="3e8f1-112">Wenn Sie SharePoint-Elemente in einem Kontext mit erhöhten Rechten bereitstellen möchten, müssen Sie in solchen Fällen die Elemente zusammen mit Ihrem Lösungspaket verpacken und bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-112">In such cases, when you want to provision SharePoint items in an elevated context, you must package and deploy the items along with your solution package.</span></span>

## <a name="provision-sharepoint-items-in-your-solution"></a><span data-ttu-id="3e8f1-113">Bereitstellen von SharePoint-Elementen in Ihrer Lösung</span><span class="sxs-lookup"><span data-stu-id="3e8f1-113">Create SharePoint items in your solution</span></span>

<span data-ttu-id="3e8f1-114">Die folgenden SharePoint-Ressourcen können zusammen mit Ihrem clientseitigen Lösungspaket bereitgestellt werden:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-114">The following SharePoint assets can be provisioned along with your client-side solution package:</span></span>

* <span data-ttu-id="3e8f1-115">Felder</span><span class="sxs-lookup"><span data-stu-id="3e8f1-115">Fields</span></span>
* <span data-ttu-id="3e8f1-116">Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="3e8f1-116">Content types</span></span>
* <span data-ttu-id="3e8f1-117">Listeninstanzen</span><span class="sxs-lookup"><span data-stu-id="3e8f1-117">List instances</span></span>
* <span data-ttu-id="3e8f1-118">Listeninstanzen mit benutzerdefiniertem Schema</span><span class="sxs-lookup"><span data-stu-id="3e8f1-118">List instances with custom schema</span></span>

### <a name="fields"></a><span data-ttu-id="3e8f1-119">Felder</span><span class="sxs-lookup"><span data-stu-id="3e8f1-119">Fields</span></span>

<span data-ttu-id="3e8f1-p104">Ein Feld oder eine Websitespalte stellt ein Attribut oder Metadaten dar, die der Benutzer für die Elemente in der Liste oder im Inhaltstyp verwalten möchte, zu der bzw. dem sie die Spalte hinzugefügt haben. Es handelt sich um eine wieder verwendbare Spaltendefinition oder Vorlage, die Sie mehreren Listen über mehrere SharePoint-Websites hinweg zuweisen können. Websitespalten reduzieren den Überarbeitungsaufwand und helfen Ihnen, die Konsistenz von Metadaten über Websites und Listen hinweg sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-p104">A field or a site column represents an attribute, or piece of metadata, that the user wants to manage for the items in the list or content type to which they added the column. It is a reusable column definition, or template, that you can assign to multiple lists across multiple SharePoint sites. Site columns decrease rework and help you ensure consistency of metadata across sites and lists.</span></span> 

<span data-ttu-id="3e8f1-123">Nehmen wir beispielsweise an, dass Sie eine Websitespalte mit dem Namen „Kunde“ definieren.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-123">For example, suppose you define a site column named Customer.</span></span> <span data-ttu-id="3e8f1-124">Benutzer können diese Spalte zu ihren Listen hinzufügen und in ihren Inhaltstypen darauf verweisen.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-124">Users can add that column to their lists and reference it in their content types.</span></span> <span data-ttu-id="3e8f1-125">Dadurch wird sichergestellt, dass die Spalte – zumindest zu Beginn – dieselben Attribute aufweist, unabhängig davon, wo sie angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-125">This ensures that the column has the same attributes—at least to start with—wherever it appears.</span></span>

<span data-ttu-id="3e8f1-126">Sie können in der Dokumentation [Field-Element (Field)](https://msdn.microsoft.com/en-us/library/aa979575(v=office.15).aspx) die Informationen über das Schema und die Attribute nachlesen, um ein neues Feld in Ihrer Lösung zu definieren.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-126">You can refer to the schema and attributes in the [Field Element](https://msdn.microsoft.com/en-us/library/aa979575(v=office.15).aspx) documentation to define a new field in your solution.</span></span> 

<span data-ttu-id="3e8f1-127">Nachfolgend sehen Sie ein Beispiel für ein neues DateTime-Feld:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-127">Below is an example of a new DateTime field:</span></span>

```xml
<Field ID="{1511BF28-A787-4061-B2E1-71F64CC93FD5}"
            Name="DateOpened"
            DisplayName="Date Opened"
            Type="DateTime"
            Format="DateOnly"
            Required="FALSE"
            Group="Financial Columns">
        <Default>[today]</Default>
    </Field>
```

### <a name="content-types"></a><span data-ttu-id="3e8f1-128">Inhaltstypen</span><span class="sxs-lookup"><span data-stu-id="3e8f1-128">Content types</span></span>

<span data-ttu-id="3e8f1-p106">Ein Inhaltstyp ist eine wieder verwendbare Sammlung von Metadaten (Spalten), Verhaltensweisen und anderen Einstellungen für eine Kategorie von Elementen oder Dokumenten in einer SharePoint-Liste oder Dokumentbibliothek. Mit Inhaltstypen können Sie Einstellungen für eine Kategorie von Informationen auf zentrale und wiederverwendbare Weise verwalten.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-p106">A content type is a reusable collection of metadata (columns), behavior, and other settings for a category of items or documents in a SharePoint list or document library. Content types enable you to manage the settings for a category of information in a centralized, reusable way.</span></span>

<span data-ttu-id="3e8f1-131">Stellen Sie die folgende Geschäftssituation vor: Sie verfügen über drei unterschiedliche Typen von Dokumenten: Spesenabrechnungen, Bestellungen und Rechnungen.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-131">For example, imagine a business situation in which you have three different types of documents: expense reports, purchase orders, and invoices.</span></span> <span data-ttu-id="3e8f1-132">Alle drei Typen von Dokumenten weisen gemeinsame Merkmale auf: bei allen drei handelt es sich um Finanzdokumente mit Daten in einer Währung.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-132">All three types of documents have some characteristics in common; for one thing, they are all financial documents and contain data with values in currency.</span></span> <span data-ttu-id="3e8f1-133">Jeder Typ von Dokument verfügt jedoch auch über eigene Datenanforderungen, eine eigene Dokumentvorlage und einen eigenen Workflow.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-133">Yet each type of document has its own data requirements, its own document template, and its own workflow.</span></span> 

<span data-ttu-id="3e8f1-134">Eine Lösung für dieses Geschäftsproblem ist die Erstellung von vier Inhaltstypen.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-134">One solution to this business problem is to create four content types.</span></span> <span data-ttu-id="3e8f1-135">Der erste Inhaltstyp „Finanzdokument“ könnte die Datenanforderungen kapseln, die alle Finanzdokumente in der Organisation gemeinsam haben.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-135">For example, you can define a list instance Finance Documents with a content type Financial Document that could encapsulate data requirements that are common to all financial documents in the organization.</span></span> <span data-ttu-id="3e8f1-136">Die verbleibenden drei Inhaltstypen „Spesenabrechnung“, „Bestellung“ und „Rechnung“ könnten gemeinsame Elemente vom Finanzdokument erben.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-136">The remaining three, Expense Report, Purchase Order, and Invoice, could inherit common elements from Financial Document.</span></span> <span data-ttu-id="3e8f1-137">Darüber hinaus könnten sie Merkmale definieren, die für jeden Typ eindeutig sind, z. B. ein bestimmter Satz von Metadaten, eine Dokumentvorlage, die beim Erstellen eines neuen Elements verwendet werden soll, und ein bestimmter Workflow für die Verarbeitung eines Elements.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-137">In addition, they could define characteristics that are unique to each type, such as a particular set of metadata, a document template to be used in creating a new item, and a specific workflow for processing an item.</span></span>

<span data-ttu-id="3e8f1-138">Sie können in der Dokumentation [ContentType-Element (ContentType)](https://msdn.microsoft.com/de-DE/library/aa544268.aspx) die Informationen über das Schema und die Attribute nachlesen, um einen neuen Inhaltstyp in Ihrer Lösung zu definieren.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-138">You can refer to the schema and attributes in the [Content Type Element](https://msdn.microsoft.com/de-DE/library/aa544268.aspx) documentation to define a new content type in your solution.</span></span> 

<span data-ttu-id="3e8f1-139">Nachfolgend sehen Sie ein Beispiel für einen Inhaltstyp:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-139">Below is an example of a content type:</span></span>

```xml
<ContentType ID="0x010042D0C1C200A14B6887742B6344675C8B" 
    Name="Cost Center" 
    Group="Financial Content Types" 
    Description="Financial Content Type">
    <FieldRefs>
        <FieldRef ID="{1511BF28-A787-4061-B2E1-71F64CC93FD5}" />
        <FieldRef ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}" /> 
    </FieldRefs>
</ContentType> 
```

### <a name="list-instances"></a><span data-ttu-id="3e8f1-140">Listeninstanzen</span><span class="sxs-lookup"><span data-stu-id="3e8f1-140">List instances</span></span>

<span data-ttu-id="3e8f1-p109">Listen sind ein wichtiges, zugrunde liegendes Feature einer SharePoint-Website. Team können damit Informationen sammeln, nachverfolgen und freigeben. Viele Clientanwendungen basieren auf Listen, die in der Website zur Datenspeicherung erstellt wurden, um ihre Verhaltensweisen zu implementieren. Eine Listeninstanz ist eine vordefinierte SharePoint-Liste, die einen bekannten Bezeichner aufweist. Sie können Elemente anpassen und zu diesen Listen hinzufügen, zusätzliche Listen aus den bereits verfügbaren Listenvorlagen erstellen und benutzerdefinierte Listen mit den ausgewählten Einstellungen und Spalten erstellen.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-p109">Lists are a key, underlying feature of a SharePoint site. They enable teams to gather, track, and share information. Many applications rely on lists created at the site for data storage to implement their behaviors. A list instance is a predefined SharePoint list that has a well-known identifier. You can customize and add items to these lists, create additional lists from the list templates that are already available, and create custom lists with just the settings and columns that you choose.</span></span>

<span data-ttu-id="3e8f1-146">SharePoint bietet mehrere Listenvorlagen, z. B. Kontaktlisten, Kalender, Aufgabenlisten usw.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-146">SharePoint provides several list templates such as contact list, calendar, task list, and more.</span></span> <span data-ttu-id="3e8f1-147">Sie können diese Vorlagen verwenden, um neue Listeninstanzen für Ihre Webparts oder andere Komponenten zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-147">You can use these templates to create new list instances for your web parts or other components.</span></span> <span data-ttu-id="3e8f1-148">Sie können z. B. die Listeninstanz „Finanzdokumente“ basierend auf der Vorlage für die Dokumentbibliothek definieren, um zugehörige Dokumente mit dem Webpart zu speichern.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-148">SharePoint provides several list templates such as contact list, calendar, task list and more. You can use these templates to create new list instances for your web parts or other components. For example, you can define a list instance Finance Documents based on the Document Library template to store associated documents with your web part.</span></span> 

<span data-ttu-id="3e8f1-149">Sie können in der Dokumentation [ListInstance-Element (List Instance)](https://msdn.microsoft.com/de-DE/library/office/ms476062.aspx) die Informationen über das Schema und die Attribute nachlesen, um eine neue Listeninstanz in Ihrer Lösung zu definieren.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-149">You can refer to the schema and attributes in the [List Instance Element](https://msdn.microsoft.com/de-DE/library/office/ms476062.aspx) documentation to define a list instance in your solution.</span></span>

<span data-ttu-id="3e8f1-150">Es folgt ein Beispiel für eine Listeninstanzdefinition:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-150">Below is an example of a list instance definition:</span></span>

```xml
<ListInstance 
    FeatureId="00bfea71-e717-4e80-aa17-d0c71b360101"
    Title="Finance Records" 
    Description="Finance documents"
    TemplateType="101"
    Url="Lists/FinanceRecords">
</ListInstance>
```

### <a name="list-instances-with-custom-schema"></a><span data-ttu-id="3e8f1-151">Listeninstanzen mit benutzerdefiniertem Schema</span><span class="sxs-lookup"><span data-stu-id="3e8f1-151">List instances with custom schema</span></span>

<span data-ttu-id="3e8f1-152">Sie können eine benutzerdefinierte Listenschemadefinition verwenden, um Ihre Felder, Inhaltstypen und Ansichten zu definieren, die in Ihrer Listeninstanz verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-152">You can use a custom list schema definition to define your fields, content types and views used in your list instance.</span></span> <span data-ttu-id="3e8f1-153">Das [CustomSchema](https://msdn.microsoft.com/de-DE/library/office/ms476062.aspx#sectionSection0)-Attribut im ListInstance-Element wird verwendet, um auf ein benutzerdefiniertes Schema für die Listeninstanz zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-153">You will use the  attribute in the list instance element to reference a custom schema for the list instance.</span></span> 

<span data-ttu-id="3e8f1-154">Sie können beispielsweise die Listeninstanz **Finanzdokumente** mit dem Inhaltstyp **Finanzdokument** definieren, der die Datenanforderungen kapseln könnte, die alle Finanzdokumente in der Organisation gemeinsam haben.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-154">For example, you can define a list instance Finance Documents with a content type Financial Document that could encapsulate data requirements that are common to all financial documents in the organization.</span></span> 

<span data-ttu-id="3e8f1-155">Nachfolgend sehen Sie ein Beispiel einer Listeninstanzdefinition, die ein benutzerdefiniertes Schema verwendet:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-155">Below is an example of a list instance definition that uses a custom schema:</span></span>

```xml
<ListInstance 
    CustomSchema="schema.xml"
    FeatureId="00bfea71-de22-43b2-a848-c05709900100"
    Title="Cost Centers" 
    Description="Cost Centers"
    TemplateType="100"
    Url="Lists/CostCenters">
</ListInstance>
```

<br/>

<span data-ttu-id="3e8f1-156">Dies ist die benutzerdefinierte Schemadefinition, die einen Inhaltstyp für die zuvor definierte Listeninstanz definiert:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-156">And the custom schema definition that defines a content type for the list instance defined above:</span></span>

```xml
<List xmlns:ows="Microsoft SharePoint" Title="Basic List" EnableContentTypes="TRUE" FolderCreation="FALSE" Direction="$Resources:Direction;" Url="Lists/Basic List" BaseType="0" xmlns="http://schemas.microsoft.com/sharepoint/">
  <MetaData>
    <ContentTypes>
      <ContentTypeRef ID="0x010042D0C1C200A14B6887742B6344675C8B" />
    </ContentTypes>
    <Fields></Fields>
    <Views>
      <View BaseViewID="1" Type="HTML" WebPartZoneID="Main" DisplayName="$Resources:core,objectiv_schema_mwsidcamlidC24;" DefaultView="TRUE" MobileView="TRUE" MobileDefaultView="TRUE" SetupPath="pages\viewpage.aspx" ImageUrl="/_layouts/images/generic.png" Url="AllItems.aspx">
        <XslLink Default="TRUE">main.xsl</XslLink>
        <JSLink>clienttemplates.js</JSLink>
        <RowLimit Paged="TRUE">30</RowLimit>
        <Toolbar Type="Standard" />
        <ViewFields>
          <FieldRef Name="LinkTitle"></FieldRef>
          <FieldRef Name="SPFxAmount"></FieldRef>
          <FieldRef Name="SPFxCostCenter"></FieldRef>
        </ViewFields>
        <Query>
          <OrderBy>
            <FieldRef Name="ID" />
          </OrderBy>
        </Query>
      </View>
    </Views>
    <Forms>
      <Form Type="DisplayForm" Url="DispForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
      <Form Type="EditForm" Url="EditForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
      <Form Type="NewForm" Url="NewForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
    </Forms>
  </MetaData>
</List>
```

## <a name="create-sharepoint-items-in-your-solution"></a><span data-ttu-id="3e8f1-157">Erstellen von SharePoint-Elementen in Ihrer Lösung</span><span class="sxs-lookup"><span data-stu-id="3e8f1-157">Create SharePoint items in your solution</span></span>

<span data-ttu-id="3e8f1-158">Das Lösungspaket verwendet [SharePoint-Features](https://msdn.microsoft.com/en-us/library/ee537350(office.14).aspx) zum Verpacken und Bereitstellen der SharePoint-Elemente.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-158">The solution package uses [SharePoint Features](https://msdn.microsoft.com/en-us/library/ee537350(office.14).aspx) to package and provision the SharePoint items.</span></span> <span data-ttu-id="3e8f1-159">Ein Feature ist ein Container, der ein oder mehrere SharePoint-Elemente für die Bereitstellung enthält.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-159">A Feature is a container that includes one or more SharePoint items to provision.</span></span> <span data-ttu-id="3e8f1-160">Ein Feature enthält eine Feature.xml-Datei und eine oder mehrere Elementmanifestdateien.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-160">A Feature contains a Feature.xml file and one or more element manifest files.</span></span> <span data-ttu-id="3e8f1-161">Diese XML-Dateien werden auch als Featuredefinitionen bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-161">These XML files are also known as Feature definitions.</span></span> 

<span data-ttu-id="3e8f1-162">Ein clientseitiges Lösungspaket enthält in der Regel ein Feature.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-162">Typically, a client-side solution package contains one feature.</span></span> <span data-ttu-id="3e8f1-163">Dieses Feature wird aktiviert, wenn die Lösung auf einer Website installiert wird.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-163">This feature is activated when the solution is installed on a site.</span></span> <span data-ttu-id="3e8f1-164">Es ist wichtig zu beachten, dass die Websiteadministratoren Ihr Lösungspaket und nicht das Feature installieren.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-164">Typically, a client-side solution package contains one feature. This feature is activated when the solution is installed in a site. It is important to note that the site administrators install your solution package and not the feature.</span></span> 

<span data-ttu-id="3e8f1-165">Ein Feature wird in erster Linie mithilfe der folgenden XML-Dateien erstellt:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-165">A feature is primarily constructed by using the following XML files:</span></span>

### <a name="element-manifest-file"></a><span data-ttu-id="3e8f1-166">Elementmanifestdatei</span><span class="sxs-lookup"><span data-stu-id="3e8f1-166">Element Manifest File</span></span>

<span data-ttu-id="3e8f1-167">Die Elementmanifestdatei enthält die SharePoint-Elementdefinitionen und wird ausgeführt, wenn das Feature aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-167">The element manifest file contains the SharePoint item definitions and is executed when the feature is activated.</span></span> <span data-ttu-id="3e8f1-168">Die XML-Definitionen zum Erstellen eines neuen Felds, Inhaltstyps oder einer Listeninstanz befinden sich beispielsweise im Elementmanifest.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-168">For example, the XML definitions to create a new field, content type, or list instance is in the element manifest.</span></span> 

<span data-ttu-id="3e8f1-169">Nachfolgend finden Sie in Beispiel einer Elementmanifestdatei, die ein neues DateTime-Feld definiert.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-169">Below is an example of an element manifest file that defines a new DateTime field.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <Field ID="{1511BF28-A787-4061-B2E1-71F64CC93FD5}"
            Name="DateOpened"
            DisplayName="Date Opened"
            Type="DateTime"
            Format="DateOnly"
            Required="FALSE"
            Group="Financial Columns">
        <Default>[today]</Default>
    </Field>
  </Elements>
```

### <a name="element-file"></a><span data-ttu-id="3e8f1-170">Elementdatei</span><span class="sxs-lookup"><span data-stu-id="3e8f1-170">Element File</span></span>

<span data-ttu-id="3e8f1-171">Alle unterstützten Dateien, die das Elementmanifest begleiten, sind Elementdateien.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-171">Any supported files that accompany the element manifest are element files.</span></span> <span data-ttu-id="3e8f1-172">Das Listeninstanzschema ist beispielsweise eine Elementdatei, die einer Listeninstanz zugeordnet ist, die in einem Elementmanifest definiert ist.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-172">Any supported files that accompany the element manifest will be an element file. For example, the list instance schema is an element manifest that is associated with a list instance that is defined in an element manifest.</span></span> 

<span data-ttu-id="3e8f1-173">Nachfolgend sehen Sie ein Beispiel für ein benutzerdefiniertes Listeninstanzschema:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-173">Below is an example of a custom list instance schema:</span></span>

```xml
<List xmlns:ows="Microsoft SharePoint" Title="Basic List" EnableContentTypes="TRUE" FolderCreation="FALSE"
      Direction="$Resources:Direction;" Url="Lists/Basic List" BaseType="0" xmlns="http://schemas.microsoft.com/sharepoint/">
  <MetaData>
    <ContentTypes>
      <ContentTypeRef ID="0x010042D0C1C200A14B6887742B6344675C8B" />
    </ContentTypes>    
  </MetaData>
</List>
```

### <a name="upgrade-actions-file"></a><span data-ttu-id="3e8f1-174">Upgradeaktionendatei</span><span class="sxs-lookup"><span data-stu-id="3e8f1-174">Upgrade Actions File</span></span>

<span data-ttu-id="3e8f1-175">Wie der Name schon sagt, ist das die Datei, die alle Upgradeaktionen umfasst, wenn die Lösung in der Website aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-175">As its name suggests, this is the file that includes any upgrade actions when the solution is updated on the site.</span></span> <span data-ttu-id="3e8f1-176">Als Teil der Upgradeaktionen könnte die Aktion angeben, dass auch ein oder mehrere Elementmanifeste eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-176">As part of the upgrade actions, the action could specify to include one or more element manifests as well.</span></span> <span data-ttu-id="3e8f1-177">Wenn für das Upgrade zum Beispiel ein neues Feld hinzugefügt werden muss, ist die Felddefinition als Elementmanifest verfügbar und wird der Datei mit Upgradeaktionen zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-177">For example, if the upgrade requires a new field to be added, the field definition is available as an element manifest and is associated in the upgrade actions file.</span></span> 

<span data-ttu-id="3e8f1-178">Nachfolgend sehen Sie ein Beispiel für eine Datei mit Upgradeaktionen, die eine Elementmanifestdatei während des Upgrades anwendet:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-178">Below is an example of an upgrade action file that applies an element manifest file during the upgrade:</span></span>

```xml
<ApplyElementManifests>
      <ElementManifest Location="9c0be970-a4d7-41bb-be21-4a683586db18\elements-v2.xml" />
</ApplyElementManifests>
```

## <a name="configure-the-sharepoint-feature"></a><span data-ttu-id="3e8f1-179">Konfigurieren des SharePoint-Features</span><span class="sxs-lookup"><span data-stu-id="3e8f1-179">Configure the SharePoint feature</span></span> 

<span data-ttu-id="3e8f1-180">Damit die XML-Dateien eingeschlossen werden, müssen Sie zunächst die Featurekonfiguration in der Konfigurationsdatei *package-solution.json* unterhalb des Ordners *config* in Ihrem Projekt definieren.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-180">In order to include the XML files, you will need to first define the feature configuration in the *package-solution.json* configuration file underneath the *config* folder in your project.</span></span> <span data-ttu-id="3e8f1-181">Die Datei *package-solution.json* enthält die wichtigsten Metadateninformationen zu Ihrem clientseitigen Lösungspaket, und es wird auf die Datei verwiesen, wenn Sie den `package-solution`-gulp-Task ausführen, durch den Ihre Lösung in einer `.sppkg`-Datei verpackt wird.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-181">The *package-solution.json* contains the key metadata information about your client-side solution package and is referenced when you run the `package-solution` gulp task which packages your solution into a `.sppkg` file.</span></span> 

```json
{
  "solution": {
    "name": "hello-world-client-side-solution",
    "id": "26364618-3056-4b45-98c1-39450adc5723",
    "version": "1.1.0.0",
    "features": [{
      "title": "hello-world-client-side-solution",
      "description": "hello-world-client-side-solution",
      "id": "d46cd9d6-87fc-473b-a4c0-db9ad9162b64",
      "version": "1.1.0.0",
      "assets": {        
        "elementManifests": [
          "elements.xml"
        ],
        "elementFiles":[
          "schema.xml"
        ],
        "upgradeActions":[
            "upgrade-actions-v1.xml"
        ]
      }
    }]
  },  
  "paths": {
    "zippedPackage": "solution/hello-world.sppkg"
  }
}
``` 

<br/>

<span data-ttu-id="3e8f1-182">Das `features`-JSON-Objekt enthält die Metadaten über das Feature, wie in der folgenden Tabelle gezeigt.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-182">The `features` JSON object contains the metadata about the feature, as shown in the following table.</span></span>

<span data-ttu-id="3e8f1-183">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="3e8f1-183">Property</span></span> | <span data-ttu-id="3e8f1-184">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3e8f1-184">Description</span></span> 
-----|------
<span data-ttu-id="3e8f1-185">id</span><span class="sxs-lookup"><span data-stu-id="3e8f1-185">id</span></span>|<span data-ttu-id="3e8f1-186">Eindeutiger Bezeichner (GUID) des Features</span><span class="sxs-lookup"><span data-stu-id="3e8f1-186">Unique identifier (GUID) of the feature</span></span>
<span data-ttu-id="3e8f1-187">title</span><span class="sxs-lookup"><span data-stu-id="3e8f1-187">title</span></span>|<span data-ttu-id="3e8f1-188">Der Titel des Features</span><span class="sxs-lookup"><span data-stu-id="3e8f1-188">Title of the feature</span></span>
<span data-ttu-id="3e8f1-189">description</span><span class="sxs-lookup"><span data-stu-id="3e8f1-189">description</span></span>| <span data-ttu-id="3e8f1-190">Beschreibung des Features</span><span class="sxs-lookup"><span data-stu-id="3e8f1-190">Description of the feature</span></span>
<span data-ttu-id="3e8f1-191">assets</span><span class="sxs-lookup"><span data-stu-id="3e8f1-191">assets</span></span>|<span data-ttu-id="3e8f1-192">Ein Array von XML-Dateien, die in dem Feature verwendet werden</span><span class="sxs-lookup"><span data-stu-id="3e8f1-192">An array of XML files used in the feature</span></span>
<span data-ttu-id="3e8f1-193">elementManifests</span><span class="sxs-lookup"><span data-stu-id="3e8f1-193">elementManifests</span></span>|<span data-ttu-id="3e8f1-194">Ein Array von Elementmanifestdateien, definiert in der `assets`-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="3e8f1-194">Defined within the `assets` property, an array of element manifest files</span></span>
<span data-ttu-id="3e8f1-195">elementFiles</span><span class="sxs-lookup"><span data-stu-id="3e8f1-195">elementFiles</span></span>|<span data-ttu-id="3e8f1-196">Ein Array von Elementdateien, definiert in der `assets`-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="3e8f1-196">Defined within the `assets` property, an array of element files</span></span>
<span data-ttu-id="3e8f1-197">upgradeActions</span><span class="sxs-lookup"><span data-stu-id="3e8f1-197">upgradeActions</span></span>|<span data-ttu-id="3e8f1-198">Ein Array von Upgradeaktionsdateien, definiert in der `assets`-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="3e8f1-198">Defined within the `assets` property, an array of upgrade action files</span></span>

### <a name="create-the-feature-xml-files"></a><span data-ttu-id="3e8f1-199">Erstellen der Feature-XML-Dateien</span><span class="sxs-lookup"><span data-stu-id="3e8f1-199">Create the feature XML files</span></span>

<span data-ttu-id="3e8f1-200">Die Toolkette sucht in Ihrem clientseitigen Lösungsprojekt nach den XML-Dateien, wie in der Konfiguration unter einem bestimmten Ordner definiert – *sharepoint\assets*.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-200">The toolchain looks for the XML files as defined in the configuration underneath a special folder - *sharepoint\assets* - in your client-side solution project.</span></span> 

![Feature-XML-Dateien im clientseitigen Lösungsprojekt](../../images/feature-provision-project-items.png)

<span data-ttu-id="3e8f1-202">Durch die in der `package-solution.json` definierten Konfigurationen werden die XML-Dateien hier ihrer entsprechenden Feature-XML-Datei zugeordnet, wenn der gulp-Task in `package-solution` ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-202">The configurations defined in the `package-solution.json` is what maps the XML files here to its appropriate feature XML file when the `package-solution` gulp task is executed.</span></span>

## <a name="package-sharepoint-items"></a><span data-ttu-id="3e8f1-203">Verpacken von SharePoint-Elementen</span><span class="sxs-lookup"><span data-stu-id="3e8f1-203">Package SharePoint items</span></span> 

<span data-ttu-id="3e8f1-204">Nachdem Sie Ihr Feature in der `package-solution.json` definiert und die entsprechenden Feature-XML-Dateien erstellt haben, können Sie den folgenden gulp-Task verwenden, um die SharePoint-Elemente zusammen mit Ihrem `.sppkg`-Paket zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-204">Once you have defined your feature in the `package-solution.json` and created the respective feature XML files, you can use the following gulp task to package the SharePoint items along with your `.sppkg` package.</span></span>

```js
gulp package-solution
```

<span data-ttu-id="3e8f1-205">Dieser Befehl verpackt eine oder mehrere clientseitige Komponentenmanifeste, z. B. Webparts, zusammen mit den Feature-XML-Dateien, auf die in der `package-solution.json`-Konfigurationsdatei verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-205">The command above will package one or more client-side component manifests, such as web parts, along with the feature XML files referenced in the `package-solution.json` configuration file.</span></span>

> [!NOTE] 
> <span data-ttu-id="3e8f1-206">Sie können das `--ship`-Flag verwenden, um minimierte Versionen Ihrer Komponenten zu verpacken.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-206">You can use the `--ship` flag to package minified versions of your components.</span></span> 

## <a name="upgrade-sharepoint-items"></a><span data-ttu-id="3e8f1-207">Aktualisieren von SharePoint-Elementen</span><span class="sxs-lookup"><span data-stu-id="3e8f1-207">Upgrade SharePoint items</span></span>

<span data-ttu-id="3e8f1-208">Sie können neue SharePoint-Elemente einschließen oder vorhandene SharePoint-Elemente aktualisieren, wenn Sie Ihre clientseitige Lösung aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-208">You may include new SharePoint items or update existing SharePoint items when you upgrade your client-side solution.</span></span> <span data-ttu-id="3e8f1-209">Da beim Bereitstellen von SharePoint-Elementen Features verwendet werden, verwenden Sie die XML-Datei [UpgradeActions](https://msdn.microsoft.com/en-us/library/office/ee537575(v=office.14).aspx), um eine Liste von Upgradeaktionen zu definieren.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-209">Since provisioning SharePoint items uses features, you will be using the [feature upgrade actions](https://msdn.microsoft.com/en-us/library/office/ee537575(v=office.14).aspx) XML file to define a list of upgrade actions.</span></span>

<span data-ttu-id="3e8f1-210">Das `upgradeActions`-JSON-Objektarray in der `package-solution.json` verweist auf die Feature-XML-Dateien, die den Upgradeaktionen für Ihr Feature zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-210">The `upgradeActions` JSON object array in the `package-solution.json` references the feature XML file(s) associated with the upgrade actions for your feature.</span></span> <span data-ttu-id="3e8f1-211">Eine Upgradeaktionsdatei definiert auf jeden Fall die Elementmanifest-XML-Datei, die ausgeführt wird, wenn das Feature aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-211">At the least, an upgrade action file will define the element manifest XML file that will be executed when upgrading the feature.</span></span> 

<span data-ttu-id="3e8f1-212">Wenn Sie eine SharePoint-Framework-Lösung aktualisieren, müssen Sie auch die Versionsattribute für Lösung und Feature aktualisieren, dort, wo Sie die Upgradeaktionen eingefügt haben.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-212">When you are upgrading a SharePoint Framework solution, you must also update version attributes for both the solution and the feature where the upgrade actions have been included.</span></span> <span data-ttu-id="3e8f1-213">Eine Heraufsetzung der Lösungsversion zeigt SharePoint und Endbenutzern, dass eine neue Version des Pakets verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-213">A solution version increase indicates to SharePoint end users that there is a new version of the package available.</span></span> <span data-ttu-id="3e8f1-214">Eine Heraufsetzung der Featureelementversion stellt sicher, dass die in den Upgradeaktionen definierten Tasks während des Lösungsupgrades abgearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-214">A feature element version increase ensures that the tasks defined in the upgrade actions are being processed as part of the solution upgrade.</span></span> 

<span data-ttu-id="3e8f1-215">Nachfolgend sehen Sie ein Beispiel für eine Datei mit Upgradeaktionen, die eine Elementmanifestdatei während des Upgrades anwendet:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-215">Below is an example of an upgrade action file that applies an element manifest file during the upgrade:</span></span>

```xml
<ApplyElementManifests>
      <ElementManifest Location="9c0be970-a4d7-41bb-be21-4a683586db18\elements-v2.xml" />
</ApplyElementManifests>
```

<br/>

<span data-ttu-id="3e8f1-216">Dies ist die entsprechende `element-v2.xml`, die ein neues Währungsfeld definiert, das während des Upgrades definiert wird:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-216">And the corresponding `element-v2.xml` which defines a new Currency Field to be provisioned during the upgrade:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <Field ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}"
            Name="Amount"
            DisplayName="Amount"
            Type="Currency"
            Decimals="2"
            Min="0"
            Required="FALSE"
            Group="Financial Columns" />
</Elements>
```

<br/>

### <a name="sub-elements"></a><span data-ttu-id="3e8f1-217">Unterelemente</span><span class="sxs-lookup"><span data-stu-id="3e8f1-217">Sub-elements</span></span>

<span data-ttu-id="3e8f1-218">Upgradeaktionen in clientseitigen Lösungen unterstützen die folgenden Unterelemente:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-218">Upgrade actions in client-side solutions support the following sub elements:</span></span>

#### <a name="addcontenttypefield"></a><span data-ttu-id="3e8f1-219">AddContentTypeField</span><span class="sxs-lookup"><span data-stu-id="3e8f1-219">AddContentTypeField</span></span>

<span data-ttu-id="3e8f1-p121">Fügt ein neues Feld zu einem vorhandenen bereitgestellten Inhaltstyp hinzu. Gibt die Änderung des Websiteinhaltstyps an alle untergeordneten Listen und Inhaltstypen innerhalb der Website weiter. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="3e8f1-p121">Adds a new field to an existing provisioned content type. Propagates the change from the site content type to all child lists and content types within the site. For example:</span></span>

```xml
<AddContentTypeField 
     ContentTypeId="0x010100A6F9CE1AFE2A48f0A3E6CB5BB770B0F7" 
     FieldId="{B250DCFD-9310-4e2d-85F2-BE2DA37A57D2}" 
     PushDown="TRUE" />
```

#### <a name="applyelementmanifests"></a><span data-ttu-id="3e8f1-223">ApplyElementManifests</span><span class="sxs-lookup"><span data-stu-id="3e8f1-223">ApplyElementManifests</span></span>

<span data-ttu-id="3e8f1-224">Fügt ein vorhandenes Element zu einem vorhandenen Feature hinzu.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-224">Add a new element to an existing feature</span></span> <span data-ttu-id="3e8f1-225">Wenn eine Funktion aktualisiert wird, werden alle nicht deklarativen Elemente, auf die in den angegebenen Elementmanifesten verwiesen wird, bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-225">Adds a new element to an existing Feature. When a Feature is upgraded, provisions all non-declarative elements that are referenced in the specified element manifests.</span></span>

#### <a name="versionrange"></a><span data-ttu-id="3e8f1-226">VersionRange</span><span class="sxs-lookup"><span data-stu-id="3e8f1-226">VersionRange</span></span>

<span data-ttu-id="3e8f1-227">Gibt einen Versionsbereich an, auf den die angegebenen Upgradeaktionen angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="3e8f1-227">Specifies a version range to which specified upgrade actions apply.</span></span>


## <a name="see-also"></a><span data-ttu-id="3e8f1-228">Weitere Artikel</span><span class="sxs-lookup"><span data-stu-id="3e8f1-228">See also</span></span>
 
- [<span data-ttu-id="3e8f1-229">Tutorial: Bereitstellen von SharePoint-Ressourcen aus Ihrem clientseitigen SharePoint-Webpart</span><span class="sxs-lookup"><span data-stu-id="3e8f1-229">Tutorial - Provisioning SharePoint assets from your SharePoint client-side web part</span></span>](../web-parts/get-started/provision-sp-assets-from-package.md)
- [<span data-ttu-id="3e8f1-230">SharePoint-Framework-Übersicht</span><span class="sxs-lookup"><span data-stu-id="3e8f1-230">SharePoint Framework Extensions Overview</span></span>](../sharepoint-framework-overview.md)