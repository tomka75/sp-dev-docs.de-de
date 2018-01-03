---
title: Externe Ereignisse und Warnungen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e48e4812-a185-43c5-b243-04b1d79b88ee
ms.openlocfilehash: 287b8f87327973b9fd9ffd720a8f24f60fab3f4e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="external-events-and-alerts-in-sharepoint"></a>Externe Ereignisse und Warnungen in SharePoint
Hier erfahren Sie, die Konzepte hinter der Erstellung von remote-Ereignisempfänger in SharePoint, die an externen Listen angefügt werden kann, und führen Sie bei der Aktualisierung der externen Daten, die die Liste darstellt.
## <a name="what-are-event-receivers"></a>Was sind Ereignisempfänger?
<a name="Externalevents_overview"> </a>

Ein Ereignisempfänger ist ein Teil von verwaltetem Code, der auf SharePoint Auslösen von Ereignissen wie hinzufügen, verschieben, löschen, Einchecken und Auschecken reagiert. Beim Auftreten dieser Ereignisse und den Ereignisempfänger Kriterien erfüllt sind, wird der Code, den Sie schreiben, um zusätzliche Funktionen bereitzustellen ausgeführt. Wenn SharePoint-Objekten wie Listen, Workflows und Features, um auf diese Ereignisse zu warten konfiguriert sind, werden sie Ereignishostsbezeichnet. 
  
    
    
Ereignisempfänger können Sie die Geschäftslogik auszuführen, wenn ein bestimmtes Ereignis eintritt. Dies sind im Wesentlichen die Haken, in dem Sie Code zum Behandeln von bestimmten Bedingungen, Benachrichtigungen erstellen, Aktualisieren von anderen Systemen und usw. erstellen können. Wenn Sie Ereignisempfänger erstellen, wird eine DLL generiert. Sie können diese DLL in den globalen Assemblycache platzieren, damit der Ereignisempfänger als Reaktion auf Änderungen in einem externen System aufgerufen werden.
  
    
    
Das folgende Beispiel enthält einen einfachen externen-Ereignisempfänger in C#-, der ausgeführt wird, wenn der Liste ein neues Element hinzugefügt wird.
  
    
    



```cs

public class EntryContentEventReceiver : SPItemEventReceiver
{
   public override void ItemAdded(SPItemEventProperties properties)
   {
      base.ItemAdded(properties);

      // properties.ExternalNotificationMessage holds the message sent by the external 
      // system.
   }
```

Externe Ereignisempfänger können auch erweitert werden, um anhand eines Ereignisempfängers Entität und als remote-Ereignisempfänger als einen Dienst am Standort oder in Microsoft Azure bereitgestellt wurden, funktionieren. 
  
    
    

## <a name="what-are-remote-event-receivers"></a>Was sind remote-Ereignisempfänger?
<a name="WhatIsARemoteEventReceiver"> </a>

Remote-Ereignisempfänger sind für SharePoint neu. In einer herkömmlichen SharePoint-Lösung verwenden Sie einen Ereignisempfänger zum Verarbeiten von Ereignissen, wie Benutzer erstellen oder Löschen von Listen oder Elemente in Listen. In einer SharePoint-Add-In verwenden Sie einen remote-Ereignisempfänger, ähnliche Ereignisse behandeln. Remote-Ereignisempfänger funktionieren ähnlich wie reguläre Ereignisempfänger, außer dass remote-Ereignisempfänger Ereignisse, die eintreten behandeln, wenn ein SharePoint-Add-In auf einem anderen System aus der Host-Web-Anwendung ist.
  
    
    
Business Connectivity Services (BCS) verwendet remote-Ereignisempfänger, externe Listen und Entitäten zugeordnet ist, können Sie Code schreiben, der reagieren kann auf Änderungen an Daten im externen System gehostet werden.
  
    
    
Um dies zu unterstützen, wurden zwei Stereotype zum BDC-Modell hinzugefügt: **EventSubscriber** und **EventUnsubscriber**.
  
> [!NOTE]
> Ereignisempfänger werden in Sandkastenlösungen nicht unterstützt. 
  
    
    


## <a name="what-features-and-capabilities-does-the-new-external-event-receiver-infrastructure-provide"></a>Welche Features und Funktionen stellt die neue externe Ereignisempfängerinfrastruktur bereit?
<a name="FeaturesAddedWithRER"> </a>

BCS kann durch verwenden und die SharePoint Ereignisempfänger Features erweitern können Warnungen, externe Liste Ereignisempfänger und Entität Ereignisempfänger eine erweiterte Funktionalität hinzufügen.
  
    
    

- **Warnungen:** Warnungen bereits ein integraler Bestandteil von SharePoint für mehrere Versionen bis SharePoint, würden sie nicht mit externen Listen funktionieren. Ein Benutzer kann jetzt Benachrichtigungen erstellen, für eine externe Liste, die dasselbe Verhalten wie Warnungen für eine standardmäßige SharePoint-Liste verfügen.
    
  
- **Ereignisempfänger für externe Liste:** Ereignisempfänger können jetzt an externen Listen, wie sie für standard-Listen können angefügt werden soll. Dadurch wird die ein Erweiterungsmechanismus, mit dem Sie Code schreiben, die zu bestimmten Zeiten ausgeführt wird.
    
  
- **Ereignisempfänger Entität:** Entity-Ereignisempfänger bieten die Flexibilität heraus robusteren Code schreiben, der andere Vorgänge wie die Bereitstellung von Benutzerkontext zum Filtern von Daten ermöglicht. Dadurch kann eine bessere Personalisierung und benutzerdefinierte Sicherheit.
    
  
Remote-Ereignisdienst in SharePoint ermöglicht verschiedene interessante Szenarien. Beispielsweise müssen Sie eine Anwendung "Sales führen Tracking" möglicherweise, die ein Verkaufsteam benachrichtigt werden, wenn neue Vertriebskontakte in eine Anwendung externen Lead eingegeben werden können. Bei der Eingabe eines neuen Vertriebsleads wird SharePoint durch das Benachrichtigungssystem benachrichtigt, die Teil der Lead-Anwendung ist. SharePoint empfängt die Benachrichtigung und erstellt dann neue Vorgänge für die angegebene Vertriebsmitarbeiter jeder neuen Lead Nachverfolgung. Konfigurieren Sie die Anwendung Vertriebsleads Eintrag für das externe System zum Senden einer Benachrichtigung in SharePoint auf die Erstellung der einzelnen neuen Lead, ist SharePoint vollständig auf dem neuesten Stand.
  
    
    

## <a name="prerequisites-for-using-event-receivers-for-external-lists"></a>Voraussetzungen für die Verwendung von Ereignisempfängern für externe Listen
<a name="bkmk_Prerequisites"> </a>

Um Ereignisempfänger für externe Listen verwenden, benötigen Sie Folgendes:
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
For more information about setting up a SharePoint development environment, see  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

## <a name="configure-the-external-system-to-notify-sharepoint-of-external-events"></a>Konfigurieren Sie das externe System, um SharePoint externe Ereignisse benachrichtigen
<a name="Externalevents_components"> </a>

Für externe Ereignisse arbeiten müssen eine Reihe von Komponenten installiert und in der SharePoint-Host und dem externen System konfiguriert werden.
  
    
    
Sie müssen das externe System konfigurieren, sodass es das folgende Aufgaben ausführen kann:
  
    
    

- **Bestimmen, wann die Basisdaten.** Für das externe System wissen, wann Änderungen vorgenommen wurden müssen Sie einen Mechanismus für das Abrufen bestimmter Änderungen erstellen. Hierzu können Sie mit einem Intervallen Dienst, der die Datenquelle in bestimmten Abständen abfragt.
    
  
- **Empfangen und Anforderungen aufzuzeichnen für Abonnements zu Änderungsbenachrichtigungen.** Das externe System besitzt eine Abonnementspeicher implementieren, damit es speichern kann, wer Änderungsbenachrichtigungen erhalten soll. Die einfachste Lösung ist wahrscheinlich eine Datenbanktabelle. Die Tabelle (oder jegliches Mechanismus Sie wählen) sollten SubscriptionID, Empfänger-, Ereignistyp und Entitätsname aufzeichnen.
    
  
- **Buchen Benachrichtigungen Representational State Transfer (REST) Endpunkte.** Damit können SharePoint wissen Abonnenten, dass eine Änderung aufgetreten ist, die Anwendung externen System muss einen HTTP-WebRequest an die Empfängeradresse aufgezeichnet, in dem Abonnementspeicher zu senden. Diese Empfängeradresse ist eine REST-Endpunkt von SharePoint während des Aktivierungsvorgangs Abonnement generiert.
    
  

## <a name="configure-sharepoint-to-allow-communication-with-external-systems"></a>Konfigurieren von SharePoint, um die Kommunikation mit externen Systemen zu ermöglichen
<a name="bkmk_configureSP"> </a>

Um eine Kommunikation mit dem externen System zu ermöglichen, muss SharePoint durch Folgendes konfiguriert werden:
  
    
    

- Ein BDC-Modell mit **EventSubscriber** und **EventUnsubscriber** Stereotypen konfiguriert
    
  
- Ereignisempfänger
    
  

### <a name="how-is-external-eventing-enabled"></a>Wie ist die externe Ereignisdienst aktiviert?

Sie können externe Ereignisdienst in SharePoint über die **Websiteeinstellungen** oder durch die folgenden benutzerdefinierten Feature-Id zu Ihrem Projekt hinzufügen aktivieren.
  
    
    

```XML

<ActivationDependency FeatureTitle="BCSEvents" FeatureId="60c8481d-4b54-4853-ab9f-ed7e1c21d7e4" />
```

Ereignisdienst für ein externes System ist aktiviert, wenn SharePoint die Empfängeradresse erstellt und ihn an das externe System während des Aktivierungsvorgangs abonnieren sendet.
  
    
    

## <a name="overall-flow-of-external-eventing-between-sharepoint-and-external-systems"></a>Projektfluss Abonnementmethode für externe Ereignisse zwischen SharePoint und externen Systemen
<a name="bkmk_overallflow"> </a>

In Abbildung 1 Beachten Sie, dass drei Einzelschritte umfasst bei Verwendung von externen Ereignisempfänger: abonnieren, Benachrichtigung, und melden Sie sich ab.
  
    
    

**Abbildung 1 vollständige Datenfluss für externe Benachrichtigungen**

  
    
    

  
    
    
![Datenfluss bei externen Ereignisbenachrichtigungen](../images/ExtEvtsAndAlrts_Figure1.jpg)
  
    
    

  
    
    

  
    
    

## <a name="eventsubscriber-subscribe-to-notifications"></a>EventSubscriber: Abonnieren Sie Benachrichtigungen
<a name="bkmk_eventsubscriber"> </a>

Für einen Benutzer (SharePoint-Objekt) zum Empfangen von Benachrichtigungen, wenn sich die zugrunde liegenden Daten geändert hat muss der Benutzer für eine Entität Abonnieren von Benachrichtigungen. Um dies zu ermöglichen, wurde das Schema BDC-Modell erweitert, um das Stereotyp **Subscribe** enthalten. Das Stereotyp **Subscribe** wird von SharePoint lassen Sie das externe System wissen, dass der Absender aufgefordert wird, Änderungen an den zugrunde liegenden Daten benachrichtigt werden sollen.
  
    
    
Abbildung 2 zeigt die des Informationsflusses zwischen SharePoint und das externe System während des Aktivierungsvorgangs abonnieren.
  
    
    

**Abbildung 2. Prozessfluss abonnieren**

  
    
    

  
    
    
![Prozessablauf der Abonniermethode für externe Ereignisse](../images/ExtEvtsAndAlerts_Figure2.jpg)
  
    
    
Im folgenden werden den allgemeinen Ablauf des Prozesses Abonnement beschrieben:
  
    
    

  
    
    

1. **Benutzer fordert ein Abonnement für Benachrichtigungen.** SharePoint initiiert mit einer benutzerdefinierten Benutzeroberfläche (eine Schaltfläche auf einer Seite oder ein Menüband) eine Anforderung an das externe System-app für Benachrichtigungen.
    
  
2. **SharePoint generiert eine Empfängeradresse.** Im Rahmen des Prozesses zum Abonnieren erstellt SharePoint einen REST-Endpunkt, in denen Benachrichtigungen zugestellt werden.
    
  
3. **Abonnementanforderung wird an das externe System gesendet.** SharePoint anschließend kapselt die Anforderer Informationen zusammen mit der dynamisch generierte REST-URL und sendet eine Webanforderung an das externe System.
    
  
4. **Externes System Anforderung empfängt.** Es gibt verschiedene Möglichkeiten für die Implementierung einer Abonnementspeicher. In diesem Beispiel verwenden Sie eine SQL Server-Datenbanktabelle.
    
  
5. **Externes System generiert eine SubscriptionId.** Eine neue **subscriptionId** wird mithilfe von Code in der Anwendung Line-of-Business (LOB) generiert. Die **subscriptionId** sollte eine GUID.
    
  
6. **Externes System zeichnet das Abonnement.** Die externe Systemanwendung zeichnet die **subscriptionId**, Empfänger-, Ereignistyp und andere Informationen aus SharePoint gesendet, in dem Abonnementspeicher.
    
  
7. **Externes System sendet die SubscriptionId an SharePoint.** Für SharePoint korrekt weiterzuleiten, die Updates, die vom externen System gesendet werden die **subscriptionId** zurück an SharePoint gesendet, und SharePoint zeichnet diese Informationen in der Datenbank.
    
    Das BDC-Modell ist gegen **Subscribe** Function Import funktionsfähig. In diesem Beispiel wird die Metadaten für den Funktionsimport angezeigt.
    


```XML
  FunctionImport
 
<EntityType Name="EntitySubscribe">
   <Key>
      <PropertyRef Name="SubscriptionId" />
   </Key>
   <Property Name="SubscriptionId" Type="Edm.Int32" Nullable="false" 
      p6:StoreGeneratedPattern="Identity" 
      xmlns:p6="http://schemas.microsoft.com/ado/2009/02/edm/annotation" />
   <Property Name="EntityName" Type="Edm.String" MaxLength="250" FixedLength="false" 
      Unicode="true" />
   <Property Name="DeliveryURL" Type="Edm.String" MaxLength="250" FixedLength="false" 
      Unicode="true" />
   <Property Name="EventType" Type="Edm.Int32" />
   <Property Name="UserId" Type="Edm.String" MaxLength="50" FixedLength="false" 
      Unicode="true" />
   <Property Name="SubscribeTime" Type="Edm.Binary" MaxLength="8" FixedLength="true" 
      p6:StoreGeneratedPattern="Computed" 
      xmlns:p6="http://schemas.microsoft.com/ado/2009/02/edm/annotation" />
   <Property Name="SelectColumns" Type="Edm.String" MaxLength="10" FixedLength="false" 
      Unicode="true" />
</EntityType>

```


### <a name="code-example-bdc-model-with-subscribe"></a>Codebeispiel: BDC-Modell mit abonnieren

Es folgt ein Beispiel für ein BDC-Modell mit der **Subscribe** -Methode hinzugefügt.
  
    
    

```XML

<Method Name="SubscribeCustomer" DefaultDisplayName="Customer Subscribe" IsStatic="true">
   <Properties>
     <Property Name="ODataEntityUrl" Type="System.String">/EntitySubscribes</Property>
     <Property Name="ODataHttpMethod" Type="System.String">POST</Property>
     <Property Name="ODataPayloadKind" Type="System.String">Entry</Property>
     <Property Name="ODataFormat" Type="System.String">application/atom+xml</Property>
     <Property Name="ODataServiceOperation" Type="System.Boolean">false</Property>
   </Properties>
   <AccessControlList>
      <AccessControlEntry Principal="NT Authority\\Authenticated Users">
         <Right BdcRight="Edit" />
         <Right BdcRight="Execute" />
         <Right BdcRight="SetPermissions" />
         <Right BdcRight="SelectableInClients" />
      </AccessControlEntry>
   </AccessControlList>
   <Parameters>
      <Parameter Direction="In" Name="@DeliveryURL">
         <TypeDescriptor TypeName="System.String" Name="DeliveryURL" >
            <Properties>
               <Property Name="IsDeliveryAddress" Type="System.Boolean">true</Property>
            </Properties>
         </TypeDescriptor>
      </Parameter>
      <Parameter Direction="In" Name="@EventType">
         <TypeDescriptor TypeName="System.Int32" Name="EventType" >
            <Properties>
               <Property Name="IsEventType" Type="System.Boolean">true</Property>
            </Properties>
         </TypeDescriptor>
      </Parameter>
      <Parameter Direction="In" Name="@EntityName">
         <TypeDescriptor TypeName="System.String" Name="EntityName" >
            <DefaultValues>
               <DefaultValue MethodInstanceName="SubscribeCustomer" 
                  Type="System.String">Customers</DefaultValue>
            </DefaultValues>
      </TypeDescriptor>
    </Parameter>
    <Parameter Direction="In" Name="@SelectColumns">
      <TypeDescriptor TypeName="System.String" Name="SelectColumns" >
        <DefaultValues>
          <DefaultValue MethodInstanceName="SubscribeCustomer" Type="System.String">*</DefaultValue>
        </DefaultValues>
      </TypeDescriptor>
    </Parameter>
    <Parameter Direction="Return" Name="SubscribeReturn">
      <TypeDescriptor Name="SubscribeReturnRootTd" TypeName="Microsoft.BusinessData.Runtime.DynamicType">
        <TypeDescriptors>
          <TypeDescriptor Name="SubscriptionId" TypeName="System.String" >
            <Properties>
              <Property Name="SubscriptionIdName" Type="System.String">Default</Property>
            </Properties>
            <Interpretation>
              <ConvertType LOBType="System.Int32" BDCType="System.String"/>
            </Interpretation>
          </TypeDescriptor>
          <TypeDescriptor Name="DeliveryURL" TypeName="System.String" />
          <TypeDescriptor Name="SelectColumns" TypeName="System.String" >
          </TypeDescriptor>
          <TypeDescriptor Name="EntityName" TypeName="System.String" />
          <TypeDescriptor Name="EventType" TypeName="System.Int32" />
          <TypeDescriptor Name="UserId" TypeName="System.String" />
          <!--TypeDescriptor Name="SubscribeTime" TypeName="System." /-->
        </TypeDescriptors>
      </TypeDescriptor>
    </Parameter>
  </Parameters>
  <MethodInstances>
    <MethodInstance Type="EventSubscriber" ReturnParameterName="SubscribeReturn" ReturnTypeDescriptorPath="SubscribeReturnRootTd" Default="true" Name="SubscribeCustomer" DefaultDisplayName="Customer Subscribe">
      <AccessControlList>
        <AccessControlEntry Principal="NT Authority\\Authenticated Users">
          <Right BdcRight="Edit" />
          <Right BdcRight="Execute" />
          <Right BdcRight="SetPermissions" />
          <Right BdcRight="SelectableInClients" />
        </AccessControlEntry>
      </AccessControlList>
    </MethodInstance>
  </MethodInstances>
</Method>
```

Tabelle 1 sind die wichtigen Attribute des BDC-Modells, die erforderlich sind, stellen Sie das **Subscribe** Stereotyp arbeiten.
  
    
    

**In Tabelle 1. BDC-Modellattribute**


|**Attribut**|**Beschreibung**|
|:-----|:-----|
|**IsDeliveryAddress** <br/> |Ein **Boolean** -Flag, das in einer **TypeDescriptor** verwendet, um anzugeben, ob die bereitgestellten Empfängeradresse verwendet werden, um Benachrichtigungen zu übermitteln. <br/> |
|**IsEventType** <br/> |Ein **Boolean** -Flag, das in einer **TypeDescriptor** verwendet, um anzugeben, ob der bereitgestellten Ereignistyp ist als den Ereignistyp verwendet werden soll. Gültige Ereignistypen sind **ItemAdded**, **ItemUpdated**, **ItemDeleted**und So weiter. <br/> |
|**SubscriptionIdName** <br/> |Eine Zeichenfolge, die auf eine **TypeDescriptor**, die den Namen eines Teils **subscriptionId** darstellt. <br/> |
   

## <a name="notifications"></a>Benachrichtigungen
<a name="bkmk_notifications"> </a>

In SharePoint wurde die Ereignisbehandlung Infrastruktur zum Zulassen von externen Datenquellen zum SharePoint zu benachrichtigen, wenn die Informationen im externen System geändert wurden verbessert. Klicken Sie dann können SharePoint eine Benachrichtigung erhält, von Ereignisempfängern, die dem externen SharePoint-Liste oder Entität zugeordnet sind Code zum Ausführen der angegebenen Aktionen ausführen.
  
    
    
Wenn ein Abonnement erstellt wird, benötigt das externe System eine Möglichkeit zum Teilen Sie SharePoint auf eine bestimmte Entität zu den Änderungen, die aufgetreten sind. Das externe System wird erwartet, dass Benachrichtigungen an die Empfängeradresse von SharePoint mit dem externen System während des Subscribe-Prozesses mit einer OData-Atom-Format Nutzlast bereitgestellten übermitteln.
  
    
    
Abbildung 3 zeigt den Kommunikationsfluss zwischen dem externen System und SharePoint auf, wenn die Daten im externen System ein neuer Datensatz hinzugefügt wird.
  
    
    

**Abbildung 3 Benachrichtigungsprozess**

  
    
    

  
    
    
![Benachrichtigungsprozess für externe Ereignisse](../images/ExtEvtsAndAlerts_Figure3.jpg)
  
    
    

  
    
    

1. **Neuer Datensatz hinzugefügt wird, mit externen System.** In diesem Beispiel wird ein neuer Datensatz mit dem externen System über die Benutzeroberfläche der Anwendung oder direkt in der Datenbank hinzugefügt.
    
  
2. **Externen System-Anwendung ist von der Änderung benachrichtigt.** Die externen System-Anwendung enthält, sollten Sie die Änderungen vorgenommen werden, die an die zugrunde liegenden Daten gestellt werden sollen. Es gibt mehrere Möglichkeiten, um diese Schritte durchführen. Sie können SQL-Trigger, die ausgelöst werden, wenn Daten für bestimmte Tabellen geändert, oder Sie können einen Abrufmechanismus zum Abfragen von Datenspeicher für Änderungen erstellen. Andere Möglichkeiten zur Verfügung stehen, aber jede muss mit Leistung berücksichtigen ausgewertet werden soll.
    
  
3. **Externes System sendet Benachrichtigungsanforderung an SharePoint über Empfängeradresse.** Um die Änderungen zu kommunizieren, verfügt über eine Anforderung Atom-Format an die Empfängeradresse gesendet werden, die in die Branchenanwendung Abonnementspeicher gespeichert ist.
    
  

### <a name="notification-payload"></a>Nutzdaten der Benachrichtigung

Bei der Erstellung die Benachrichtigung LOB-System eine HTTP-Nutzlast erstellen, die alle Details des Elements enthält, die geändert, wurde, oder nur die Identität des geänderten Elements.
  
    
    

- **Identität:** Wenn die Nutzlast als Identität gesendet wird, wird erwartet, dass die Nutzlast haben nur Informationen über die Identität des geänderten Elements. Beispielsweise würde für einen Kunden in einer Kundenentität, die Nutzlast nur enthalten die ID des Kunden, die sich geändert hat.
    
  
- **Vollständige Element:** In diesem Fall ist die Nutzlast ein vollständiger Datensatz, der im externen System geändert hat. Im Kundenbeispiel wird der gesamte geänderten Kundendatensatz aufgenommen.
    
> [!NOTE]
> Das vollständige Element wird nur unterstützt, wenn Sie den OData-Connector verwenden. 
  
    
    

Der Typ der Nutzlast, die vom externen System gesendet wird, muss während des Abonnementvorgangs angegeben werden.
  
    
    
Es folgt ein Beispiel für die BDC-Modell-Eigenschaft für Benachrichtigungen verwendet.
  
    
    



```XML

<Property Name="NotificationParserType" Type="System.String">
   ODataEntryContentNotificationParser
</Property>

```

Wenn sie nicht angegeben wird, ist die Standard-Nutzlast eine Identität.
  
    
    

### <a name="notification-delivery-address-virtual-address"></a>Notification Delivery-Adresse (virtuelle Adresse)

Der Anmeldevorgang initiiert aus SharePoint-Suchergebnissen in einer virtuellen Adresse von SharePoint, die einen Einstiegspunkt für das externe System zum Bereitstellen von Benachrichtigungen ermöglicht erstellt wird. Die Empfängeradresse wird vom externen System zum Bereitstellen von diese Benachrichtigungen verwendet. Die Empfängeradresse wird auch während der Abonnementanforderung an das externe System übergeben.
  
    
    

## <a name="eventunsubscriber-remove-subscription-from-the-notifications-list"></a>EventUnsubscriber: Abonnement aus der Benachrichtigungsliste entfernen
<a name="bkmk_eventunsubscriber"> </a>

Der Vorgang **Unsubscribe** entfernt ein Abonnement aus der Benachrichtigungsliste.
  
    
    
 Abbildung 4 zeigt, dass die **UnSubscribe** -Methode viel einfacher ist. Da die Abonnement-ID an SharePoint gesendet wurde, und SharePoint aufgezeichnet es, ist erforderlich ist, zum Senden der Anforderung zum Abmelden mit der richtigen Abonnement-ID.
  
    
    

**Abbildung 4 Codefluss für kündigen-Methode**

  
    
    

  
    
    
![Prozess zum Kündigen externer Benachrichtigungen](../images/ExternalEventsAndAlerts_UnsubscribeFlow.jpg)
  
    
    

### <a name="bdc-model-for-unsubscribe"></a>BDC-Modell für zum Abmelden

Im folgende XML-Beispiel zeigt die Erstellung einer hebt das Abonnement von BDC-Modell aus dem externen Systemereignisbenachrichtigungen.
  
    
    

```XML

<Method Name="UnSubscribeExpenseReport" DefaultDisplayName="ExpenseReport
    Unsubscribe">
    <Properties>
        <Property Name="ODataEntityUrl" Type="System.String">
            /Subscriptions(@ID)</Property>
        <Property Name="ODataHttpMethod" Type="System.String">DELETE</Property>
        <Property Name="ODataPayloadKind" Type="System.String">Property</Property>
        <Property Name="ODataServiceOperation" Type="System.Boolean">false</Property>
    </Properties>
    <AccessControlList>
        <AccessControlEntry Principal="NT Authority\\Authenticated Users">
            <Right BdcRight="Edit" />
            <Right BdcRight="Execute" />
            <Right BdcRight="SetPermissions" />
            <Right BdcRight="SelectableInClients" />
        </AccessControlEntry>
    </AccessControlList>
    <Parameters>
        <Parameter Name="@ID" Direction="In">
            <TypeDescriptor Name="ID" TypeName="System.Int32">
                <Properties>
                    <Property Name="SubscriptionIdName" Type="System.String">ID</Property>
                </Properties>
                <Interpretation>
                    <ConvertType LOBType="System.Int32" BDCType="System.String" />
                </Interpretation>
            </TypeDescriptor>
        </Parameter>
    </Parameters>
    <MethodInstances>
        <MethodInstance Name="UnSubscribeExpenseReport" DefaultDisplayName="ExpenseReport 
             Unsubscribe" Type="EventUnsubscriber" Default="true">
            <AccessControlList>
                <AccessControlEntry Principal="NT Authority\\Authenticated Users">
                    <Right BdcRight="Edit" />
                    <Right BdcRight="Execute" />
                    <Right BdcRight="SetPermissions" />
                    <Right BdcRight="SelectableInClients" />
                </AccessControlEntry>
            </AccessControlList>
        </MethodInstance>
    </MethodInstances>
</Method>



<Method IsStatic="false" Name="Unsubscribe">
    <AccessControlList>
        <AccessControlEntry Principal="NT AUTHORITY\\Authenticated Users">
            <Right BdcRight="Edit" />
            <Right BdcRight="Execute" />
            <Right BdcRight="SetPermissions" />
            <Right BdcRight="SelectableInClients" />
        </AccessControlEntry>
    </AccessControlList>
    <Parameters>
        <Parameter Direction="In" Name="subscriptionId">
            <TypeDescriptor TypeName="System.String" Name="subscriptionId" 
                IsSubscriptionId="true" />
         </Parameter>
    </Parameters>
    <MethodInstances>
        <MethodInstance Type="EventUnsubscriber" Default="true" Name="Unsubscribe" 
            DefaultDisplayName="UnSubscriber">
            <Properties>
                <Property Name="LastDesignedOfficeItemType" Type="System.String">None</Property>
            </Properties>
            <AccessControlList>
                <AccessControlEntry Principal=" NT AUTHORITY\\Authenticated Users ">
                    <Right BdcRight="Edit" />
                    <Right BdcRight="Execute" />
                    <Right BdcRight="SetPermissions" />
                    <Right BdcRight="SelectableInClients" />
                </AccessControlEntry>
            </AccessControlList>
        </MethodInstance>
    </MethodInstances>
</Method>

```


## <a name="code-example-attach-an-event-receiver-to-an-external-list"></a>Codebeispiel: Anfügen eines Ereignisempfängers zu einer externen Liste
<a name="AttachingRER"> </a>

Der folgende Code enthält ein Beispiel dafür, wie Sie zum Anfügen eines Ereignisempfängers zu einer externen Liste. Nachdem sie verbunden ist, überwacht der Ereignisempfänger für Benachrichtigungen aus dem externen System zu Updates, Hinzufügungen und Löschungen, die für die systemeigenen Daten ausgeführt werden.
  
    
    

```XML

private static void AddEventReceiver(string siteUrl, string listTitle)
{ 
   string assembly = "SampleEventReceiver, Culture=neutral, Version=1.0.0.0, 
      PublicKeyToken=1bfafa687d2e46a7";
   string className = "SampleEventReceiver.EntryContentEventReceiver"; 
   
   try
   {
      using (SPSite site = new SPSite(siteUrl)) 
      { 
         using (SPWeb web = site.OpenWeb()) 
         {
            SPList list = web.Lists[listTitle]; 
            list.EventReceivers.Add(SPEventReceiverType.ItemAdded, 
               assembly, className); 
         }
      }
   }
   catch (Exception e) 
   { 
      Console.WriteLine(e); 
   }
}

```


## <a name="beyond-the-basics-learn-more-about-using-external-event-receivers"></a>Weiterführendes: Weitere Informationen zur Verwendung von externen Ereignisempfänger
<a name="Externalevents_Learnmore"> </a>

Weitere Informationen über externe Ereignisse und Warnungen finden Sie in der folgenden.
  
    
    

**In Tabelle 2. Erweiterte Konzepte für die Arbeit mit externen Ereignisempfänger**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [Vorgehensweise: Erstellen einer OData-Datendiensts zur Verwendung als einer externen BCS-System](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system.md) <br/> |Erfahren Sie, wie einen Internet-adressierbaren Windows Communication Foundation (WCF) Dienst erstellen, der OData wird verwendet, um Benachrichtigungen an SharePoint senden, wenn sich die zugrunde liegenden Daten ändert. Diese Benachrichtigungen werden verwendet, um Ereignisse auslösen, die externe Listen angefügt sind.  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="Externalevents_Addres"> </a>


-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Business Connectivity Services-Programmierreferenz für SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen von externen Ereignisempfängern](how-to-create-external-event-receivers.md)
    
  

