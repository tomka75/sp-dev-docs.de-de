---
title: "Konfigurieren und Verwenden von Pushbenachrichtigungen in SharePoint-Apps für Windows Phone"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 68fa2138-86d9-4e35-9c7c-5cd292087b80
ms.openlocfilehash: b9e6c480be922250a62a524a703ea2cd0925b548
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="configure-and-use-push-notifications-in-sharepoint-apps-for-windows-phone"></a>Konfigurieren und Verwenden von Pushbenachrichtigungen in SharePoint-Apps für Windows Phone

Erstellen Sie eine Lösung in SharePoint Server, um Pushbenachrichtigungen zu senden, und entwickeln Sie eine Windows Phone-App, um die Benachrichtigungen zu empfangen. Verwenden die Microsoft Push Notification Service (MPNS), können Windows Phone-apps Benachrichtigungen über das Internet über Ereignisse ausgelöst werden auf Microsoft SharePoint Server empfangen. Phone-app keinen Server für Änderungen an, beispielsweise die Elemente in einer Liste die Abfragen auf der Phone-app basiert. Die app Erhalt von Benachrichtigungen auf dem Server registriert werden, und ein Ereignisempfänger initiieren Sie eine Benachrichtigung und senden Sie sie an die empfangende app für die Behandlung von kann. Das Push Notification wird an der Windows Phone-Geräten von MPNS weitergeleitet.
  
    
    

Windows Phone 7 unterstützt nicht mehrere apps gleichzeitig ausgeführt. Als die Komponenten des Betriebssystems Windows Phone (OS) selbst kann nur eine app auf dem Telefon zu einem Zeitpunkt ausgeführt werden. Ein Ereignis, die einer bestimmten Phone-app für die Überprüfung relevante auftreten (z. B., beispielsweise ein Listenelement zu einer Liste hinzugefügte) Wenn die app auf dem Telefon im Vordergrund ausgeführt nicht zur Verfügung (d. h., wenn die app veraltete oder geschlossen ist). Konnten Sie einen Hintergrunddienst auf dem Telefon mit einem periodischen Vorgang, der Überprüfung auf Änderungen an der Liste auf dem Server möglicherweise entwickeln, aber diese Vorgehensweise würde Ressourcen (z. B. Netzwerk Bandbreite und Batterie Power) auf dem Telefon nutzen. Mit MPNS und die Komponenten, die in der Windows Phone 7-Betriebssystem integrierten Benachrichtigungen zu unterstützen, kann das Telefon selbst eine Benachrichtigung, die über eine bestimmte app für den Kontext relevant empfangen - selbst wenn diese app ausgeführt wird nicht - der Benutzer die Möglichkeit zum Starten der relevanten app als Antwort auf die Benachrichtigung gewährt werden kann. (Weitere Informationen zu Pushbenachrichtigungen, finden Sie unter  [Push Notifications Overview for Windows Phone](http://msdn.microsoft.com/de-DE/library/ff402558%28VS.92%29.aspx) in der MSDN Library). In diesem Thema erstellen Sie eine serverseitige Lösung zum Senden von Pushbenachrichtigungen zu einer Phone-app basierend auf eine Änderung in der Liste auf der die app basiert. Erstellen Sie dann die Phone-app für den Empfang von diese Benachrichtigungen.
  
    
    


## <a name="create-a-server-side-solution-to-send-push-notifications-based-on-a-list-item-event"></a>Erstellen Sie eine serverseitige Lösung zum Senden von Pushbenachrichtigungen basierend auf einer listenelementereignis
<a name="BKMK_ServerSideSolution"> </a>

Die serverseitige Lösung kann es sich entweder einer SharePoint-app in einem isolierten **SPWeb** -Objekt bereitgestellt oder einer SharePoint-Farm-Lösung verpackt als ein SharePoint-Lösungspaket (d. h., eine WSP-Datei), die ein Feature mit Web-Bereich enthält. In den Verfahren in diesem Abschnitt entwickeln Sie eine einfache SharePoint-Lösung, die eine Zielliste von einer Windows Phone-app verwendet werden erstellt und, Push-Notification-Mechanismus auf dem Server aktiviert. Im nachfolgenden Abschnitt wird die Windows Phone-app zum Empfang von Benachrichtigungen aus der serverseitigen Lösung entwickelt.
  
    
    

### <a name="to-create-the-server-side-project"></a>So erstellen Sie das serverseitige Projekt


1. Starten Sie Visual Studio 2012 mit der Option **Als Administrator ausführen**.
    
  
2. Klicken Sie auf **Datei**, **Neu**, **Projekt**.
    
    Das Dialogfeld **Neues Projekt** wird angezeigt.
    
  
3. Klicken Sie im Dialogfeld **Neues Projekt** den Knoten **SharePoint** unter **Visual c#**, und wählen Sie dann den Knoten **15**.
    
  
4. Wählen Sie im Bereich **Vorlagen** **SharePoint-Projekts** aus, und geben Sie einen Namen für das Projekt, wie etwaPushNotificationsList.
    
  
5. Wählen Sie die Schaltfläche **OK**. Im Assistenten zum Anpassen von SharePoint wird angezeigt. Mit diesem Assistenten können Sie die Zielwebsite für das Entwickeln und Debuggen des Projekts und die Vertrauensebene der Lösung auswählen.
    
  
6. Geben Sie die URL einer Website SharePoint Server. Wählen Sie eine Website, die Sie später in die Entwicklung von SharePoint-Listen-app für Windows Phone verwendet werden.
    
  
7. Wählen Sie **als farmlösung bereitstellen** aus, und klicken Sie dann auf **Fertig stellen**, um das Projekt zu erstellen.
    
  
Im nächsten Schritt fügen Sie dem Projekt eine Klassendatei hinzu, und erstellen Sie eine Reihe von Klassen zum Kapseln und Verwalten von Pushbenachrichtigungen.
  
    
    

### <a name="to-create-the-classes-for-managing-push-notifications"></a>So erstellen Sie die Klassen für die Verwaltung von Pushbenachrichtigungen


1. Wählen Sie im **Projektmappen-Explorer** den Knoten ab, das Projekt (mit dem NamenPushNotificationsList , wenn Sie die Namenskonventionen in diesen Verfahren befolgen).
    
  
2. Klicken Sie im Menü **Projekt** auf **Klasse hinzufügen**. Das Dialogfeld **Neues Element hinzufügen** wird angezeigt. Die C#-Vorlage **Klasse** ist bereits ausgewählt.
    
  
3. Geben Sie PushNotification.cs als Namen der Datei, und klicken Sie auf **Hinzufügen**. Die Klassendatei ist die Lösung hinzugefügt und zur Bearbeitung geöffnet.
    
  
4. Ersetzen Sie den Inhalt der Datei durch den folgenden Code:
    
```cs
  
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Net;
using System.Text;
using Microsoft.SharePoint;

namespace PushNotificationsList
{
    internal static class WP7Constants
    {
        internal static readonly string[] WP_RESPONSE_HEADERS = 
            {
                "X-MessageID",
                "X-DeviceConnectionStatus",
                "X-SubscriptionStatus",
                "X-NotificationStatus"
            };
    }

    public enum TileIntervalValuesEnum
    {
        ImmediateTile = 1,
        Delay450SecondsTile = 11,
        Delay900SecondsTile = 21,
    }

    public enum ToastIntervalValuesEnum
    {
        ImmediateToast = 2,
        Delay450SecondsToast = 12,
        Delay900SecondsToast = 22,
    }

    public enum RawIntervalValuesEnum
    {
        ImmediateRaw = 3,
        Delay450SecondsRaw = 13,
        Delay900SecondsRaw = 23
    }

    public enum NotificationTypeEnum
    {
        Tile = 1,
        Toast = 2,
        Raw = 3
    }

    class PushNotification
    {
        public PushNotificationResponse PushToast(SPPushNotificationSubscriber subscriber, string toastTitle, string toastMessage, string toastParam, ToastIntervalValuesEnum intervalValue)
        {
            // Construct toast notification message from parameter values.
            string toastNotification = "<?xml version=\\"1.0\\" encoding=\\"utf-8\\"?>" +
            "<wp:Notification xmlns:wp=\\"WPNotification\\">" +
               "<wp:Toast>" +
                    "<wp:Text1>" + toastTitle + "</wp:Text1>" +
                    "<wp:Text2>" + toastMessage + "</wp:Text2>" +
                    "<wp:Param>" + toastParam + "</wp:Param>" +
               "</wp:Toast> " +
            "</wp:Notification>";

            return SendPushNotification(NotificationTypeEnum.Toast, subscriber, toastNotification, (int)intervalValue);
        }

        public PushNotificationResponse PushRaw(SPPushNotificationSubscriber subscriber, string rawMessage, RawIntervalValuesEnum intervalValue)
        {
            return SendPushNotification(NotificationTypeEnum.Raw, subscriber, rawMessage, (int)intervalValue);
        }

        private PushNotificationResponse SendPushNotification(NotificationTypeEnum notificationType, SPPushNotificationSubscriber subscriber, string message, int intervalValue)
        {
            // Create HTTP Web Request object.
            string subscriptionUri = subscriber.ServiceToken;
            HttpWebRequest sendNotificationRequest = (HttpWebRequest)WebRequest.Create(subscriptionUri);

            // MPNS expects a byte array, so convert message accordingly.
            byte[] notificationMessage = Encoding.Default.GetBytes(message);
            
            // Set the notification request properties.
            sendNotificationRequest.Method = WebRequestMethods.Http.Post;
            sendNotificationRequest.ContentLength = notificationMessage.Length;
            sendNotificationRequest.ContentType = "text/xml";
            sendNotificationRequest.Headers.Add("X-MessageID", Guid.NewGuid().ToString());

            switch (notificationType)
            {
                case NotificationTypeEnum.Tile:
                    sendNotificationRequest.Headers.Add("X-WindowsPhone-Target", "token");
                    break;
                case NotificationTypeEnum.Toast:
                    sendNotificationRequest.Headers.Add("X-WindowsPhone-Target", "toast");
                    break;
                case NotificationTypeEnum.Raw:
                    // A value for the X-WindowsPhone-Target header is not specified for raw notifications.
                    break;
            }            

            sendNotificationRequest.Headers.Add("X-NotificationClass", intervalValue.ToString());

            // Merge byte array payload with headers.
            using (Stream requestStream = sendNotificationRequest.GetRequestStream())
            {
                requestStream.Write(notificationMessage, 0, notificationMessage.Length);
            }

            string statCode = string.Empty;
            PushNotificationResponse notificationResponse;

            try
            {
                // Send the notification and get the response.
                HttpWebResponse response = (HttpWebResponse)sendNotificationRequest.GetResponse();
                statCode = Enum.GetName(typeof(HttpStatusCode), response.StatusCode);

                // Create PushNotificationResponse object.
                notificationResponse = new PushNotificationResponse((int)intervalValue, subscriber.ServiceToken);
                notificationResponse.StatusCode = statCode;
                foreach (string header in WP7Constants.WP_RESPONSE_HEADERS)
                {
                    notificationResponse.Properties[header] = response.Headers[header];
                }                
            }
            catch (Exception ex)
            {
                statCode = ex.Message;
                notificationResponse = new PushNotificationResponse((int)intervalValue, subscriber.ServiceToken);
                notificationResponse.StatusCode = statCode;
            }

            return notificationResponse;
        }
    }     

    /// <summary>
    /// Object used for returning notification request results.
    /// </summary>
    class PushNotificationResponse
    {
        private DateTime timestamp;
        private int notificationIntervalValue;
        private string statusCode = string.Empty;
        private string serviceToken;
        private Dictionary<string, string> properties;

        public PushNotificationResponse(int numericalIntervalValue, string srvcToken)
        {
            timestamp = DateTime.UtcNow;
            notificationIntervalValue = numericalIntervalValue;
            serviceToken = srvcToken;
            properties = new Dictionary<string, string>();
        }

        public DateTime TimeStamp
        {
            get { return timestamp; }
        }

        public int NotificationIntervalValue
        {
            get { return notificationIntervalValue; }
        }

        public string StatusCode
        {
            get { return statusCode; }
            set { statusCode = value; }
        }

        public string ServiceToken
        {
            get { return serviceToken; }
        }

        public Dictionary<string, string> Properties
        {
            get { return properties; }
        }
    }
}
```

5. Speichern Sie die Datei.
    
  
In diesem Code Argumente die Methoden **PushToast** und **PushRaw** Parameter für den angegebenen Typ der Benachrichtigung zu senden, diese Argumente verarbeiten, und rufen Sie dann die **SendPushNotification** -Methode, die die senden die Benachrichtigung mit der Microsoft-Pushbenachrichtigungsdienst funktioniert. (In diesen Beispielcode wurde eine Methode zum Senden von Benachrichtigungen Kachel nicht implementiert.) Die **PushNotificationResponse** -Klasse ist einfach ein Mechanismus zum Kapseln des Ergebnis aus der Benachrichtigung Anforderung empfangen hat. Die Klasse fügt hier einige Informationen auf das Objekt (Cast als Objekt **HttpWebResponse** ) von der **GetResponse** -Methode des **HttpWebRequest** -Objekts zurückgegeben. Der Ereignisempfänger, den Sie in der folgenden Prozedur erstellen verwendet diese **PushNotificationResponse** -Klasse, um eine Ergebnisliste Benachrichtigungen auf dem Server zu aktualisieren.
  
    
    
Nun Erstellen einer Ereignisempfängerklasse, die Pushbenachrichtigungen an Geräte senden, die erfasst wurden, um sie zu erhalten. (Dieser Ereignisempfänger binden zu der Liste der Projekte, die in einem späteren Verfahren erstellt wird.)
  
    
    

### <a name="to-create-the-event-receiver-class-for-a-list"></a>Eine Liste die Ereignisempfängerklasse erstellen


1. Wählen Sie im **Projektmappen-Explorer** den Knoten ab, das Projekt aus.
    
  
2. Klicken Sie im Menü **Projekt** auf **Klasse hinzufügen**. Das Dialogfeld **Neues Element hinzufügen** wird angezeigt, mit der C#- **Klasse** Vorlage bereits ausgewählt.
    
  
3. Geben Sie ListItemEventReceiver.cs als Namen der Datei, und klicken Sie auf **Hinzufügen**. Die Klassendatei ist die Lösung hinzugefügt und zur Bearbeitung geöffnet.
    
  
4. Ersetzen Sie den Inhalt der Datei durch den folgenden Code:
    
```cs
  
using System;
using System.Security.Permissions;
using System.Text;
using Microsoft.SharePoint;
using Microsoft.SharePoint.Utilities;

namespace PushNotificationsList
{
    /// <summary>
    /// List Item Events
    /// </summary>
    public class ListItemEventReceiver : SPItemEventReceiver
    {
        internal static string ResultsList = "Push Notification Results";

        /// <summary>
        /// An item was added.
        /// </summary>
        public override void ItemAdded(SPItemEventProperties properties)
        {
            SPWeb spWeb = properties.Web;
            SPPushNotificationSubscriberCollection pushSubscribers = spWeb.PushNotificationSubscribers;
            PushNotification pushNotification = new PushNotification();

            SPListItem listItem = properties.ListItem;

            string jobAssignment = "[Unassigned]";

            // This event receiver is intended to be associated with a specific list,
            // but the list may not have an "AssignedTo" field, so using try/catch here.
            try
            {
                jobAssignment = listItem["AssignedTo"].ToString();
            }
            catch { }

            PushNotificationResponse pushResponse = null;

            foreach (SPPushNotificationSubscriber ps in pushSubscribers)
            {
                // Send a toast notification to be displayed on subscribed phones on which the app is not running.
                pushResponse = pushNotification.PushToast(ps, "New job for:", jobAssignment, string.Empty, ToastIntervalValuesEnum.ImmediateToast);
                UpdateNotificationResultsList(spWeb, ps.User.Name, pushResponse);

                // Also send a raw notification to be displayed on subscribed phones on which the app is running when the item is added.
                pushResponse = pushNotification.PushRaw(ps, string.Format("New job for: {0}", jobAssignment), RawIntervalValuesEnum.ImmediateRaw);
                UpdateNotificationResultsList(spWeb, ps.User.Name, pushResponse);
            }

            base.ItemAdded(properties);
        }

        private void UpdateNotificationResultsList(SPWeb spWeb, string subscriberName, PushNotificationResponse pushResponse)
        {
            SPList resultsList = spWeb.Lists.TryGetList(ResultsList);

            if (resultsList == null)
                return;

            try
            {
                SPListItem resultItem = resultsList.Items.Add();
                resultItem["Title"] = subscriberName;
                resultItem["Notification Time"] = pushResponse.TimeStamp;
                resultItem["Status Code"] = pushResponse.StatusCode;
                resultItem["Service Token"] = pushResponse.ServiceToken;

                StringBuilder builder = new StringBuilder();
                foreach (string key in pushResponse.Properties.Keys)
                {
                    builder.AppendFormat("{0}: {1}; ", key, pushResponse.Properties[key]);
                }
                resultItem["Headers"] = builder.ToString();

                resultItem["Interval Value"] = pushResponse.NotificationIntervalValue;
                resultItem.Update();
            }
            catch
            {
                // Could log to ULS here if adding list item fails.
            }
        }
    }
}
```

5. Speichern Sie die Datei.
    
  
In diesem Code nach der Liste ein Element hinzugefügt wird, der der Ereignisempfänger gebunden ist, werden Pushbenachrichtigungen an Abonnenten gesendet, die Erhalt von Benachrichtigungen registriert haben. Der Wert des Felds AssignedTo aus dem hinzugefügten Listenelement ist in der Benachrichtigung an Abonnenten gesendet enthalten. Für die Toast-Benachrichtigung werden die Werte des Parameters **toastTitle** (für die **PushToast** -Methode definiert, die im vorhergehenden Verfahren) und der Parameter **toastMessage** festgelegt. Diese Werte entsprechen den Eigenschaften **Text1** und **Text2** im XML-Schema, das Toast-Benachrichtigung definiert.
  
    
    
Eine leere Zeichenfolge ist einfach als Wert des Parameters **toastParam** übergeben wird, der die **Param** -Eigenschaft im XML-Schema für Toast-Benachrichtigung entspricht. Sie können diesen Parameter verwenden, an, beispielsweise eine Seite mit den Phone-app zu öffnen, wenn der Benutzer auf die Benachrichtigung in das Telefon klickt. In der Beispiel-app entwickelt, die weiter unten in diesem Thema für diese Benachrichtigungen werden vom Server empfangen wurde wird die **Param** -Eigenschaft nicht verwendet. Im Formular List (List.xaml) in der app ist einfach geöffnet, wenn der Benutzer auf die Benachrichtigung klickt.
  
    
    

> **Hinweis:** Die **Param**-Eigenschaft für Toast-Benachrichtigung wird nur in Windows Phone OS Version 7.1 oder höher unterstützt.
  
    
    

Für die unformatierte Benachrichtigung in diesem Beispiel wird eine Zeichenfolge übergeben, die den Wert des Felds AssignedTo aus dem hinzugefügten Listenelement enthält.
  
    
    
Notiz, die auf die Toast-Benachrichtigung angezeigt wird abonniert Telefone (wenn die Phone-app für die die Benachrichtigung vorgesehen ist nicht ausgeführt wird), und die angezeigte Meldung wird abgeschnitten werden, wenn es ungefähr 41 Zeichen nicht überschreitet. Unformatierte Benachrichtigung in MPNS sind auf 1024 Byte (1 KB) beschränkt. (Die genaue Anzahl von Zeichen, die gesendet werden können hinsichtlich des Typs der verwendet wird, wie beispielsweise UTF-8-Codierung ist). Kachel Benachrichtigungen werden auch Größe Einschränkungen. Große Datenmengen können nicht mit einer der Typen Benachrichtigungen gesendet werden. Verwenden des diese Benachrichtigungen ist nicht als einen Mechanismus zum Übertragen von Daten, aber als eine Möglichkeit zum Senden von kurzer Nachrichten abonniert Telefone, damit bestimmte Aktionen auf dem Telefon durchgeführt werden können. Diese Aktionen wie das Aktualisieren einer Liste auf das Telefon mit Daten aus dem Server können größere Datenmengen, je nach den Entwurf der Windows Phone-app umfassen.
  
    
    
Das **PushNotificationResponse** -Objekt, das von einer Benachrichtigung zurückgegeben wird, wird an die **UpdateNotificationResultsList** -Methode übergeben. Diese Methode fügt Informationen über die Anforderung an eine SharePoint-Liste mit dem Namen Push Notification Ergebnisse (falls die Liste vorhanden ist). Dies ist einfach eine Möglichkeit, verwenden Sie das zurückgegebene Objekt veranschaulicht. Sie können in einer produktionslösung anspruchsvollere verwendet das zurückgegebene Objekt einfügen. Sie können beispielsweise das zurückgegebene Objekt für bestimmte Statuscodes untersuchen, wenn eine Benachrichtigung an einem bestimmten Benutzer (wie der Benutzer für die Zuordnung im Feld AssignedTo festgelegte) gesendet wird und die entsprechende Aktion. In einer Anwendung Produktion würde nicht Sie wahrscheinlich alle diese Informationen in einer Liste auf dem Server speichern. Die Informationen werden hier, um die MPNS Benachrichtigungen zugeordneten Eigenschaften Verständnis gespeichert wird.
  
    
    
Im nächsten Schritt erstellen Sie eine einfache SharePoint Liste, mit dem Namen Aufträge, mit einer Kategorie, eine Beschreibung der einen Auftrag und die Person, die der Auftrag zugewiesen ist. Darüber hinaus erstellen Sie eine Hilfs Liste, mit dem Namen Push Notification Ergebnisse zum Speichern von Informationen im Zusammenhang mit pushbenachrichtigungsanforderungen Abonnement Telefone gesendet.
  
    
    
Im folgenden Verfahren erstellen Sie eine Klasse, **ListCreator**, die umfasst eine **CreateJobsList** -Methode zum Erstellen und konfigurieren die Liste der Projekte auf dem Server, wenn die Lösung aktiviert ist. Die Klasse fügt auch den **ItemAdded** Ereignisempfänger (weiter oben in der **ListItemEventReceiver** -Klasse erstellt) der **EventReceivers** -Auflistung der Liste zugeordnet. Die **ListCreator** -Klasse enthält auch eine Methode zum Erstellen der Push Notification Ergebnisse SharePoint-Liste.
  
    
    

### <a name="to-create-a-class-for-adding-and-configuring-the-lists"></a>Erstellen eine Klasse zum Hinzufügen und Konfigurieren der Listen


1. Wählen Sie im **Projektmappen-Explorer** den Knoten ab, das Projekt (erneut, benanntePushNotificationsList Wenn Sie die Namenskonventionen in diesen Verfahren befolgen).
    
  
2. Klicken Sie im Menü **Projekt** auf **Klasse hinzufügen**. Das Dialogfeld **Neues Element hinzufügen** wird angezeigt, mit der C#- **Klasse** Vorlage bereits ausgewählt.
    
  
3. Geben Sie ListCreator.cs als Namen der Datei, und klicken Sie auf **Hinzufügen**. Die Klassendatei ist die Lösung hinzugefügt und zur Bearbeitung geöffnet.
    
  
4. Ersetzen Sie den Inhalt der Datei durch den folgenden Code:
    
```cs
  
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Xml;
using Microsoft.SharePoint;

namespace PushNotificationsList
{
    class ListCreator
    {
        internal void CreateJobsList(SPWeb spWeb)
        {
            string listTitle = "Jobs";
            string listDescription = "List of jobs and assignments.";
            Dictionary<string, SPFieldType> columns = new Dictionary<string, SPFieldType>();

            // The "Title" column will be added based on the GenericList template. That field
            // will be used as the category name for the job (e.g., Shopping), so only need to add
            // the remaining fields.
            columns.Add("Description", SPFieldType.Text);
            columns.Add("AssignedTo", SPFieldType.Text);

            // Creating list (or retrieving GUID for list if it already exists).
            Guid listId = CreateCustomList(spWeb, listTitle, listDescription, columns, false);
            if (listId.Equals(Guid.Empty))
                return;

            SPList list = spWeb.Lists[listId];

            // Add event receiver (if the current Jobs list is not already associated with the receiver).
            bool ReceiverExists = false;
            string receiverClassName = "PushNotificationsList.ListItemEventReceiver";

            for (int i = 0; i < list.EventReceivers.Count; i++)
            {
                SPEventReceiverDefinition rd = list.EventReceivers[i];
                if (rd.Class == receiverClassName &amp;&amp; rd.Type == SPEventReceiverType.ItemAdded)
                {
                    ReceiverExists = true;
                    break;
                }
            }

            if (ReceiverExists == false)
            {
                SPEventReceiverDefinition eventReceiver = list.EventReceivers.Add();
                // Must specify information here for this specific assembly.
                eventReceiver.Assembly = "PushNotificationsList,
                    Version=1.0.0.0, Culture=Neutral,
                    PublicKeyToken=[YOUR TOKEN VALUE HERE]";
                eventReceiver.Class = receiverClassName;
                eventReceiver.Name = "ItemAdded Event";
                eventReceiver.Type = SPEventReceiverType.ItemAdded;
                eventReceiver.SequenceNumber = 10000;
                eventReceiver.Synchronization = SPEventReceiverSynchronization.Synchronous;
                eventReceiver.Update();
            }
        }

        internal void CreateNotificationResultsList(SPWeb spWeb)
        {
            string listTitle = "Push Notification Results";
            string listDescription = "List for results from push notification operations.";

            Dictionary<string, SPFieldType> columns = new Dictionary<string, SPFieldType>();
            columns.Add("Notification Time", SPFieldType.Text);
            columns.Add("Status Code", SPFieldType.Text);
            columns.Add("Service Token", SPFieldType.Text);
            columns.Add("Headers", SPFieldType.Text);
            columns.Add("Interval Value", SPFieldType.Integer);

            // Creating the list for storing notification results.
            CreateCustomList(spWeb, listTitle, listDescription, columns, true);
        }

        /// <summary>
        /// Creates a SharePoint list (based on the Generic List template).
        /// </summary>
        /// <param name="spWeb">The target Web site for the list.</param>
        /// <param name="listTitle">The title of the list.</param>
        /// <param name="listDescription">A description for the list.</param>
        /// <param name="columns">A Dictionary object containing field names and types.</param>
        /// <param name="replaceExistingList">Indicates whether to overwrite an existing list of the same name on the site.</param>
        /// <returns>A GUID for the created (or existing) list.</returns>
        internal Guid CreateCustomList(SPWeb spWeb, string listTitle, string listDescription, Dictionary<string, SPFieldType> columns, bool replaceExistingList)
        {
            SPList list = spWeb.Lists.TryGetList(listTitle);

            if (list != null)
            {
                if (replaceExistingList == true)
                {
                    try
                    {
                        list.Delete();
                    }
                    catch
                    {
                        return Guid.Empty;
                    }
                }
                else
                {
                    return list.ID;
                }
            }

            try
            {
                Guid listId = spWeb.Lists.Add(listTitle, listDescription, SPListTemplateType.GenericList);
                list = spWeb.Lists[listId];
                SPView view = list.DefaultView;

                foreach (string key in columns.Keys)
                {
                    list.Fields.Add(key, columns[key], false);
                    view.ViewFields.Add(key);
                }
                
                list.Update();
                view.Update();

                return listId;
            }
            catch
            {
                return Guid.Empty;
            }
        }
    }
}
```


    Be sure to specify the appropriate Public Key Token value for particular your assembly. To add a tool to Visual Studio for getting the Public Key Token value for your assembly, see  [How to: Create a Tool to Get the Public Key of an Assembly](http://msdn.microsoft.com/en-us/library/ee539398.aspx) in the MSDN Library. Note that you will have to compile your project at least once to be able to get the Public Key Token value for your output assembly.
    
  
5. Speichern Sie die Datei.
    
  
In diesem Code die **CreateJobsList**-Methode der **ListCreator**-Klasse erstellt die Liste (oder ruft die Liste ab, wenn sie auf dem Server vorhanden ist) und bindet den Ereignisempfänger erstellt in einem früheren Verfahren zur Liste der Liste zugeordneten **EventReceivers**-Klasse hinzu. Die **CreateNotificationResultsList** -Methode erstellt der Push Notification Ergebnisliste aus.
  
    
    
Fügen Sie anschließend ein Feature auf das Projekt, um die Initialisierungsvorgänge auf dem Server ausführen, wenn die Lösung bereitgestellt und aktiviert ist. Das Feature zum Verarbeiten von Ereignissen der **FeatureActivated** und **FeatureDeactivating** hinzugefügt eine Ereignisempfängerklasse.
  
    
    

### <a name="to-add-a-feature-to-your-project"></a>So fügen Sie dem Projekt ein Feature hinzu


1. Zeigen Sie in Visual Studio 2012 im Menü **Ansicht** auf **Weitere Fenster**, und klicken Sie dann auf **Paket-Explorer**.
    
  
2. Im **Paket-Explorer** mit der rechten Maustaste in des Knotens ab, das Projekt, und klicken Sie auf **Funktion hinzufügen**. Projekt unter einem **Features**-Knoten (im **Projektmappen-Explorer** ) wird ein neues Feature (namens "Feature1" standardmäßig) hinzugefügt.
    
  
3. Nun, klicken Sie im **Projektmappen-Explorer** unter dem Knoten **Funktionen** mit der rechten Maustaste des neu hinzugefügten Features (d. h., **Feature1** ), und klicken Sie auf **Ereignisempfänger hinzufügen**. Ein Ereignis empfängerklassendatei (Feature1.EventReceiver.cs) ist das Feature hinzugefügt und zur Bearbeitung geöffnet.
    
  
4. Fügen Sie in der Implementierung (abgegrenzt öffnenden und schließenden geschweiften Klammern) der **Feature1EventReceiver** -Klasse den folgenden Code ein.
    
```cs
  
internal const string PushNotificationFeatureId = "41E1D4BF-B1A2-47F7-AB80-D5D6CBBA3092";
```


    This string variable stores the identifier for the Push Notification Feature on the server.
    
    > **Tip:**
      > You can obtain a list of unique identifiers for the Features on a SharePoint Server by executing the following Windows PowerShell cmdlet: >  `Get-SPFeature | Sort -Property DisplayName`> The Push Notification Feature appears as "PhonePNSubscriber" in the results returned by this cmdlet. 
5. Das Ereignis empfängerklassendatei wird mit einige Standard-Methodendeklarationen für die Ereignisbehandlung Feature erstellt. Die Methodendeklarationen in der Datei werden zunächst auskommentiert. Ersetzen Sie die **FeatureActivated** -Methode in der Datei durch den folgenden Code ein.
    
```cs
  public override void FeatureActivated(SPFeatureReceiverProperties properties)
{
    base.FeatureActivated(properties);
    SPWeb spWeb = (SPWeb)properties.Feature.Parent;

    ListCreator listCreator = new ListCreator();
    listCreator.CreateJobsList(spWeb);
    listCreator.CreateNotificationResultsList(spWeb);

    // Then activate the Push Notification Feature on the server.
    // The Push Notification Feature is not activated by default in a SharePoint Server installation.
    spWeb.Features.Add(new Guid(PushNotificationFeatureId), false);
}
```

6. Ersetzen Sie die **FeatureDeactivating** -Methode in der Datei durch den folgenden Code ein.
    
```cs
  
public override void FeatureDeactivating(SPFeatureReceiverProperties properties)
{
    base.FeatureDeactivating(properties);
    SPWeb spWeb = (SPWeb)properties.Feature.Parent;

    // Deactivate the Push Notification Feature on the server
    // when the PushNotificationsList Feature is deactivated.
    spWeb.Features.Remove(new Guid(PushNotificationFeatureId), false);
}
```

7. Speichern Sie die Datei.
    
  
In der Implementierung der **FeatureActivated** -Ereignishandler wird eine Instanz der **ListCreator** -Klasse instanziiert und dessen Methoden **CreateJobsList** und **CreateNotificationResultsList** aufgerufen, mit **SPWeb**, in dem das Feature bereitgestellt und aktiviert wird, als den Speicherort, in dem die Listen erstellt werden. Darüber hinaus, da Push Notification Funktionalität, die standardmäßig in einer Standardinstallation von SharePoint Server nicht aktiviert ist, wird der Ereignishandler des Pushbenachrichtigungsfeatures auf dem Server aktiviert. In den **FeatureDeactivating** -Ereignishandler ist Push Notification Funktionalität deaktiviert, wenn die Anwendung deaktiviert wurde. Es ist nicht erforderlich, dieses Ereignis behandeln. Sie können oder möchten möglicherweise nicht Pushbenachrichtigungen auf dem Server deaktivieren, wenn die Anwendung deaktiviert wird, verwenden Sie je nach den von der Installation und gibt an, ob andere Anwendungen auf dem Ziel-stellen Website von Pushbenachrichtigungen.
  
    
    

## <a name="create-a-windows-phone-sharepoint-list-app-to-receive-push-notifications"></a>Erstellen einer SharePoint-Listen-App für Windows Phone zum Empfangen von Pushbenachrichtigungen
<a name="BKMK_NotificationPhoneApp"> </a>

In diesem Abschnitt erstellen Sie eine Windows Phone-app aus der Vorlage Windows Phone SharePoint List Application angeben der SharePoint-Liste als der Zielliste für die app im vorherigen Abschnitt erstellt. Sie entwickeln, klicken Sie dann eine **Notifications** -Klasse für das abonnieren, um Benachrichtigungen zu verschieben, Handler für Benachrichtigungsereignisse implementieren und Speichern von Informationen im Zusammenhang mit der Benachrichtigungen auf dem Telefon. Sie hinzufügen können Ihre app mit Steuerelementen, damit Benutzer registrieren oder Aufheben der Registrierung für Pushbenachrichtigungen eine XAML-Seite.
  
    
    
Um die Verfahren in diesem Abschnitt befolgen, führen Sie zuerst die Schritte im Verfahren beschrieben in  [Vorgehensweise: Erstellen eine Windows Phone SharePoint Liste app](how-to-create-a-windows-phone-sharepoint-list-app.md) zum Erstellen eines Visual Studio-Projekts aus der Vorlage für Windows Phone SharePoint List Application, mit der Liste der Projekte als SharePoint-Zielliste für das Projekt im vorherigen Abschnitt erstellt. Die Verfahren in diesem Abschnitt wird davon ausgegangen, dass der angegebene Name für das ProjektSPListAppForNotificationsist.
  
    
    

### <a name="to-create-the-class-for-managing-subscriptions-and-received-notifications"></a>So erstellen Sie die Klasse zum Verwalten von Abonnements und empfangenen Benachrichtigungen


1. Wählen Sie im **Projektmappen-Explorer** den Knoten, der das Projekt (mit dem NamenSPListAppForNotifications) darstellt.
    
  
2. Klicken Sie im Menü **Projekt** auf **Klasse hinzufügen**. Das Dialogfeld **Neues Element hinzufügen** wird angezeigt, mit der C#- **Klasse** Vorlage bereits ausgewählt.
    
  
3. Geben Sie "Notifications.cs" als den Namen der Datei, und klicken Sie auf **Hinzufügen**. Die Klassendatei ist die Lösung hinzugefügt und zur Bearbeitung geöffnet.
    
  
4. Ersetzen Sie den Inhalt der Datei durch den folgenden Code:
    
```cs
  
using System;
using System.Linq;
using System.Net;
using System.Windows;
using Microsoft.Phone.Notification;
using Microsoft.SharePoint.Client;
using System.Diagnostics;
using System.Collections.Generic;
using Microsoft.Phone.Shell;
using System.IO;
using System.IO.IsolatedStorage;

namespace SPListAppForNotifications
{
    public class Notifications
    {
        static HttpNotificationChannel httpChannel;
        private const string RegStatusKey = "RegistrationStatus";
        public static string DeviceAppIdKey = "DeviceAppInstanceId";
        public static string ChannelName = "JobsListNotificationChannel";
        public static ClientContext Context { get; set; }

        public static void OpenNotificationChannel(bool isInitialRegistration)
        {
            try
            {
                // Get channel if it was created in a previous session of the app.
                httpChannel = HttpNotificationChannel.Find(ChannelName);

                // If channel is not found, create one.
                if (httpChannel == null)
                {
                    httpChannel = new HttpNotificationChannel(ChannelName);

                    // Add event handlers. When the Open method is called, the ChannelUriUpdated event will fire.
                    // A call is made to the SubscribeToService method in the ChannelUriUpdated event handler.                    
                    AddChannelEventHandlers();
                    httpChannel.Open();
                }
                else
                {
                    // The channel exists and is already open. Add handlers for channel events.
                    // The ChannelUriUpdated event won't fire in this case.
                    AddChannelEventHandlers();

                    // If app instance is registering for first time
                    // (instead of just starting up again), then call SubscribeToService.
                    if (isInitialRegistration)
                    {
                        SubscribeToService();
                    }
                }
            }
            catch (Exception ex)
            {                
                ShowMessage(ex.Message, "Error Opening Channel");
                CloseChannel();
            }
        }

        private static void AddChannelEventHandlers()
        {
            httpChannel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(httpChannel_ChannelUriUpdated);
            httpChannel.ErrorOccurred += new EventHandler<NotificationChannelErrorEventArgs>(httpChannel_ExceptionOccurred);
            httpChannel.ShellToastNotificationReceived += new EventHandler<NotificationEventArgs>(httpChannel_ShellToastNotificationReceived);
            httpChannel.HttpNotificationReceived += new EventHandler<HttpNotificationEventArgs>(httpChannel_HttpNotificationReceived);
        }

        private static void httpChannel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            UpdateChannelUriOnServer();
            SubscribeToService();
        }

        private static void httpChannel_ExceptionOccurred(object sender, NotificationChannelErrorEventArgs e)
        {
            // Simply showing the exception error.
            ShowMessage(e.Message, "Channel Event Error");
        }

        static void httpChannel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            if (e.Collection != null)
            {
                Dictionary<string, string> collection = (Dictionary<string, string>)e.Collection;
                ShellToast toast = new ShellToast();
                toast.Title = collection["wp:Text1"];
                toast.Content = collection["wp:Text2"];

                // Note that the Show method for a toast notification won't
                // display the notification in the UI of the phone when the app
                // that calls the method is running (as the foreground app on the phone).
                // toast.Show();
               //Toast and Raw notification will be displayed if user is running the app. Be default only Toast notification
               // will be displayed when the app is tombstoned                                               

                // Showing the toast notification with the ShowMessage method.
                ShowMessage(string.Format("Title: {0}\\r\\nContent: {1}", toast.Title, toast.Content), "Toast Notification");
            }
        }

        static void httpChannel_HttpNotificationReceived(object sender, HttpNotificationEventArgs e)
        {
            Stream messageStream = e.Notification.Body;
            string message = string.Empty;

            // Replacing NULL characters in stream.
            using (var reader = new StreamReader(messageStream))
            {
                message = reader.ReadToEnd().Replace('\\0', ' ');
            }

            // Simply displaying the raw notification.
            ShowMessage(message, "Raw Notification");
        }

        private static void SubscribeToService()
        {
            Guid deviceAppInstanceId = GetSettingValue<Guid>(DeviceAppIdKey, false);

            Context.Load(Context.Web, w => w.Title, w => w.Description);

            PushNotificationSubscriber pushSubscriber = Context.Web.RegisterPushNotificationSubscriber(deviceAppInstanceId, httpChannel.ChannelUri.AbsoluteUri);

            Context.Load(pushSubscriber);

            Context.ExecuteQueryAsync
                (
                    (object sender, ClientRequestSucceededEventArgs args) =>
                        {
                            SetRegistrationStatus(true);

                            // Indicate that tile and toast notifications can be
                            // received by phone shell when phone app is not running.
                            if (!httpChannel.IsShellTileBound)
                                httpChannel.BindToShellTile();

                            if (!httpChannel.IsShellToastBound)
                                httpChannel.BindToShellToast();

                            ShowMessage(
                                string.Format("Subscriber successfully registered: {0}", pushSubscriber.User.LoginName),
                                "Success");
                        },
                    (object sender, ClientRequestFailedEventArgs args) =>
                        {
                            ShowMessage(args.Exception.Message, "Error Subscribing");
                        });
        }

        private static void UpdateChannelUriOnServer()
        {
            Guid deviceAppInstanceId = GetSettingValue<Guid>(DeviceAppIdKey, false);

            Context.Load(Context.Web, w => w.Title, w => w.Description);            

            PushNotificationSubscriber subscriber = Context.Web.GetPushNotificationSubscriber(deviceAppInstanceId);

            Context.Load(subscriber);

            Context.ExecuteQueryAsync(
                    (object sender1, ClientRequestSucceededEventArgs args1) =>
                    {
                        subscriber.ServiceToken = httpChannel.ChannelUri.AbsolutePath;
                        subscriber.Update();
                        Context.ExecuteQueryAsync(
                            (object sender2, ClientRequestSucceededEventArgs args2) =>
                                {
                                    ShowMessage("Channel URI updated on server.", "Success");
                                },
                            (object sender2, ClientRequestFailedEventArgs args2) =>
                                {
                                    ShowMessage(args2.Exception.Message, "Error Upating Channel URI");
                                });
                    },
                   (object sender1, ClientRequestFailedEventArgs args1) =>
                   {
                       // This condition can be ignored. Getting to this point means the subscriber
                       // doesn't yet exist on the server, so updating the Channel URI is unnecessary.
                       //ShowMessage("Subscriber doesn't exist on server.", "DEBUG");
                   });
        }

        public static void UnSubscribe()
        {
            Context.Load(Context.Web, w => w.Title, w => w.Description);
            Guid deviceAppInstanceId = GetSettingValue<Guid>(DeviceAppIdKey, false);

            Context.Web.UnregisterPushNotificationSubscriber(deviceAppInstanceId);

            Context.ExecuteQueryAsync
                (
                    (object sender, ClientRequestSucceededEventArgs args) =>
                    {
                        CloseChannel();
                        SetRegistrationStatus(false);
                        //SetInitializationStatus(false);
                        ShowMessage("Subscriber successfully unregistered.", "Success");
                    },
                    (object sender, ClientRequestFailedEventArgs args) =>
                    {
                        ShowMessage(args.Exception.Message, "Error Unsubscribing");
                    });
        }

        public static void ClearSubscriptionStore()
        {
            Context.Load(Context.Web, w => w.Title, w => w.Description);
            List subscriptionStore = Context.Web.Lists.GetByTitle("Push Notification Subscription Store");
            Context.Load(subscriptionStore);
            ListItemCollection listItems = subscriptionStore.GetItems(new CamlQuery());
            Context.Load(listItems);

            Context.ExecuteQueryAsync
                (
                    (object sender1, ClientRequestSucceededEventArgs args1) =>
                    {
                        foreach (ListItem listItem in listItems.ToList())
                        {
                            listItem.DeleteObject();                            
                        }                        
                        Context.ExecuteQueryAsync(
                                (object sender2, ClientRequestSucceededEventArgs args2) =>
                                {
                                    // Close channel if open and set registration status for current app instance.
                                    CloseChannel();
                                    SetRegistrationStatus(false);

                                    ShowMessage("Subscriber store cleared.", "Success");
                                },
                                (object sender2, ClientRequestFailedEventArgs args2) =>
                                {
                                    ShowMessage(args2.Exception.Message, "Error Deleting Subscribers");
                                });
                    },
                    (object sender1, ClientRequestFailedEventArgs args1) =>
                    {
                        ShowMessage(args1.Exception.Message, "Error Loading Subscribers List");
                    });
        }

        private static void CloseChannel()
        {
            if (httpChannel == null) return;
            try
            {
                httpChannel.UnbindToShellTile();
                httpChannel.UnbindToShellToast();
                httpChannel.Close();
            }
            catch (Exception ex)
            {
                ShowMessage(ex.Message, "Error Closing Channel");
            }
        }

        public static void SaveDeviceAppIdToStorage()
        {
            if (!IsolatedStorageSettings.ApplicationSettings.Contains(DeviceAppIdKey))
            {
                Guid DeviceAppId = Guid.NewGuid();
                SetSettingValue<Guid>(DeviceAppIdKey, DeviceAppId, false);
            }
        }

        public static bool GetRegistrationStatus()
        {
            bool status = GetSettingValue<bool>(RegStatusKey, false);
            return status;
        }

        private static void SetRegistrationStatus(bool isRegistered)
        {
            SetSettingValue<bool>(RegStatusKey, isRegistered, false);
        }

        private static T GetSettingValue<T>(string key, bool fromTransientStorage)
        {
            if (fromTransientStorage == false)
            {
                if (IsolatedStorageSettings.ApplicationSettings.Contains(key))
                    return (T)IsolatedStorageSettings.ApplicationSettings[key];
                return default(T);
            }

            if (PhoneApplicationService.Current.State.ContainsKey(key))
                return (T)PhoneApplicationService.Current.State[key];
            return default(T);
        }

        private static void SetSettingValue<T>(string key, T value, bool toTransientStorage)
        {
            if (toTransientStorage == false)
            {
                if (IsolatedStorageSettings.ApplicationSettings.Contains(key))
                    IsolatedStorageSettings.ApplicationSettings[key] = value;
                else
                    IsolatedStorageSettings.ApplicationSettings.Add(key, value);

                IsolatedStorageSettings.ApplicationSettings.Save();
            }
            else
            {
                if (PhoneApplicationService.Current.State.ContainsKey(key))
                    PhoneApplicationService.Current.State[key] = value;
                else
                    PhoneApplicationService.Current.State.Add(key, value);
            }
        }

        // Method for showing messages on UI thread coming from a different originating thread.
        private static void ShowMessage(string message, string caption)
        {
            Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show(message, caption, MessageBoxButton.OK);
            });
        }
    }
}
```

5. Speichern Sie die Datei.
    
  
In diesem Code wird die **OpenNotificationChannel** Benachrichtigung bereitgestellt für den Empfang von Benachrichtigungen aus MPNS erstellt. Ereignishandler werden auf das Channelobjekt für den Umgang mit Benachrichtigungsereignisse, und klicken Sie dann auf der DDE-Kanal geöffnet wird. In diesem Beispiel wird das Ereignis **HttpNotificationReceived** (für den Empfang von Rohdaten Benachrichtigungen) implementiert. Nur, wenn die Phone-app ausgeführt wird, können Rohdaten Benachrichtigungen empfangen werden. Der Ereignishandler für das **ShellToastNotificationReceived** -Ereignis (für den Empfang von Benachrichtigungen Toast) wird auch hier implementiert, um ihre Verwendung. Kachel Benachrichtigungen können nur, wenn die Abonnement Phone-app nicht ausgeführt wird, also keine Notwendigkeit besteht implementieren Sie einen Ereignishandler in der app zum Empfang von Benachrichtigungen Kachel empfangen werden.
  
    
    
Die **SubscribeToService** -Methode führt die **RegisterPushNotificationSubscriber** -Methode des Objekts **SPWeb** asynchron (übergeben Sie einen Wert zum Identifizieren der Phone-app und einen URI-Wert mit dem Kanal Benachrichtigung zugeordnet) mit der SharePoint Server zum Empfangen von Pushbenachrichtigungen zu registrieren. Wenn die Registrierung erfolgreich ist, wird der Windows Phone-Shell festgelegt ist, empfangen (und angezeigt) erachten und Kachel Benachrichtigungen auf die Benachrichtigung Kanal mit der SharePoint Server registriert werden, wenn die Phone-app selbst nicht ausgeführt wird.
  
    
    
Die **UnSubscribe** -Methode in diesem Code Ruft die **UnregisterPushNotificationSubscriber** -Methode des SPWeb-Objekts. Die Richtlinien für die Entwicklung für Windows Phone-apps wird empfohlen, dass Benutzer zugelassen werden, ob Sie abonnieren, um Benachrichtigungen oder nicht verschieben möchten. In einem späteren Verfahren fügen Sie einen Mechanismus für den Benutzer registrieren oder Aufheben der Registrierung für Benachrichtigungen und diesem Zustand Registrierung wird zwischen der app, leicht nicht erforderlich, bitten Sie registrieren bei jedem Start die app-Sitzungen beibehalten. Die **GetRegistrationStatus** -Methode wird zur Verfügung gestellt, damit die Phone-app ermitteln kann, ob der Benutzer (in einer früheren Sitzung) zum Empfangen von Pushbenachrichtigungen registriert und anschließend der Benachrichtigung DDE-Kanal geöffnet wird hat. Die **SaveDeviceAppIdToStorage** speichert den Bezeichner (dargestellt als GUID) für die app-Instanz auf einem bestimmten Windows Phone isolierten Speicher.
  
    
    
Die **ClearSubscriptionStore** -Methode ist hier als Beispiel für eine Möglichkeit, die Abonnenten aus dem Abonnementspeicher auf die SharePoint Server deaktivieren. Abonnenten für Pushbenachrichtigungen werden in einer SharePoint-Liste mit dem Namen "Pushbenachrichtigungs-Abonnementspeichers" gespeichert. Eine Schaltfläche zum Aufrufen dieser Methode der **Notifications** -Klasse wird zur Einstellungsseite Benachrichtigungen, die app in einem späteren Verfahren hinzugefügt wurde hinzugefügt.
  
    
    
Beachten Sie, dass Vorgänge, bei denen Zugriff auf die SharePoint Server zum Konfigurieren von Einstellungen oder Benachrichtigungen (beispielsweise die Methode **RegisterPushNotificationSubscriber** ) vorbereiten, je nach den Bedingungen des Netzwerks und der Zugriff auf dem Server dauern können. Diese Vorgänge sind daher asynchron ausgeführt (insbesondere mithilfe der **ExecuteQueryAsync** -Methode eines Objekts **ClientContext** ) um die app weiterhin andere Prozesse und die Benutzeroberfläche für den Benutzer schnell bleibt zu ermöglichen.
  
    
    
Im nächsten Schritt fügen Sie eine Seite, auf der app mit Steuerelementen, mit denen einen Benutzer für registrieren oder Aufheben der Registrierung von Pushbenachrichtigungen vom Server.
  
    
    

### <a name="to-add-a-notification-settings-page-to-the-app"></a>Hinzufügen eine Benachrichtigung Einstellungsseite für die app


1. Wählen Sie im **Projektmappen-Explorer** den Knoten ab, das Projekt (mit dem NamenSPListAppForNotifications , wenn Sie die Benennungskonvention in diesen Verfahren befolgen).
    
  
2. Klicken Sie im Menü **Projekt** auf **Neues Element hinzufügen**. Das Dialogfeld **Neues Element hinzufügen** wird angezeigt.
    
  
3. Wählen Sie im Bereich **Vorlagen** Seitenvorlage für **Windows Phone Hochformat**. Geben Sie Settings.xaml als Namen der Datei für die Seite, und klicken Sie auf **Hinzufügen**. Die Seite wird dem Projekt hinzugefügt und zur Bearbeitung geöffnet.
    
  
4. Ersetzen Sie in der XAML-Ansicht für die Seite des Inhalts für die schließende Klammer des XML-Tags, die das **PhoneApplicationPage** -Element definiert und dem schließenden-Tag des Elements ( `</phone:PhoneApplicationPage>`), durch das folgende Markup.
    
```
  
<Grid x:Name="LayoutRoot" Background="Transparent">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>

    <!--TitlePanel contains the name of the application and page title-->
    <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
        <TextBlock x:Name="ApplicationTitle" Text="JOBS LIST" Style="{StaticResource PhoneTextNormalStyle}"/>
        <TextBlock x:Name="PageTitle" Text="Settings" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
    </StackPanel>

    <!--ContentPanel - place additional content here-->
    <Grid x:Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
        <StackPanel Margin="0,5,0,5">
            <StackPanel Orientation="Vertical" Margin="0,5,0,5">
                <TextBlock TextWrapping="Wrap" HorizontalAlignment="Center" Style="{StaticResource PhoneTextTitle2Style}">Notification Registration</TextBlock>
                <StackPanel Orientation="Vertical" Margin="0,5,0,5">
                    <TextBlock x:Name="txtRegistrationStatus" TextWrapping="Wrap" HorizontalAlignment="Center" Text="Registered: No" Style="{StaticResource PhoneTextAccentStyle}" Foreground="{StaticResource PhoneAccentBrush}" />
                    <Button x:Name="btnRegister" Content="Register" Height="71" Width="260" Click="OnRegisterButtonClick" />
                    <Button x:Name="btnUnregister" Content="Unregister" Height="71" Width="260" Click="OnUnregisterButtonClick" />
                </StackPanel>
            </StackPanel>
            <StackPanel Orientation="Vertical" Margin="0,5,0,5">
                <TextBlock TextWrapping="Wrap" HorizontalAlignment="Center" Style="{StaticResource PhoneTextTitle2Style}">Subscriber Management</TextBlock>
                <Button x:Name="btnDeleteSubscribers" Content="Delete Subscribers" Height="71" Width="260" Click="OnDeleteSubscribersButtonClick" />
            </StackPanel>
        </StackPanel>
    </Grid>
</Grid>
 
<!--Sample code showing usage of ApplicationBar-->
<phone:PhoneApplicationPage.ApplicationBar>
    <shell:ApplicationBar IsVisible="True" IsMenuEnabled="False">
        <shell:ApplicationBarIconButton x:Name="btnOK" IconUri="/Images/appbar.check.rest.png" Text="OK" Click="OnOKButtonClick" />
    </shell:ApplicationBar>
</phone:PhoneApplicationPage.ApplicationBar>
```

5. Die Settings.xaml-Datei im **Projektmappen-Explorer** ausgewählt und drücken SieF7um seine zugeordnete Code-Behind-Datei Settings.xaml.cs, zur Bearbeitung zu öffnen.
    
  
6. Ersetzen Sie den Inhalt der CodeBehind-Datei durch den folgenden Code ein.
    
```cs
  
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using Microsoft.Phone.Controls;
using Microsoft.SharePoint.Client;

namespace SPListAppForNotifications
{
    public partial class Settings : PhoneApplicationPage
    {
        private const string RegisteredYesText = "Registered: Yes";
        private const string RegisteredNoText = "Registered: No";

        public Settings()
        {
            InitializeComponent();
        }

        protected override void OnNavigatedTo(System.Windows.Navigation.NavigationEventArgs e)
        {
            this.txtRegistrationStatus.Text = (Notifications.GetRegistrationStatus()) ? RegisteredYesText : RegisteredNoText;
        }

        private void OnOKButtonClick(object sender, EventArgs e)
        {
            NavigationService.Navigate(new Uri("/Views/List.xaml", UriKind.Relative));
        }

        private void OnRegisterButtonClick(object sender, RoutedEventArgs e)
        {
            Notifications.OpenNotificationChannel(true);
            // Navigating back to List form. User will be notified when process is complete.
            NavigationService.Navigate(new Uri("/Views/List.xaml", UriKind.Relative));
        }

        private void OnUnregisterButtonClick(object sender, RoutedEventArgs e)
        {
            Notifications.UnSubscribe();
            // Navigating back to List form. User will be notified when process is complete.
            NavigationService.Navigate(new Uri("/Views/List.xaml", UriKind.Relative));
        }

        private void OnDeleteSubscribersButtonClick(object sender, RoutedEventArgs e)
        {            
            Notifications.ClearSubscriptionStore();
            // Navigating back to List form. User will be notified when process is complete.
            NavigationService.Navigate(new Uri("/Views/List.xaml", UriKind.Relative));
        }
    }
}
```

7. Speichern Sie die Datei.
    
  
8. Um Sie dem Projekt die Bilddatei (appbar.check.rest.png) für die Schaltfläche **ApplicationBar** (BtnOK) in der Datei Settings.xaml deklarierten hinzuzufügen, wählen Sie im **Projektmappen-Explorer** den Knoten Bilder Ordner.
    
  
9. Klicken Sie im Menü **Projekt** auf **Vorhandenes Element hinzufügen**. Das Fenster **Dateibrowser** wird geöffnet.
    
  
10. Navigieren Sie zu dem Ordner, in dem die standardmäßigen Windows Phone-Symbolbilder durch den Windows Phone SDK 7.1 installiert wurden.
    
    > **Hinweis:** Die Bilder mit einem hellen Vorder- und ein dunkler Hintergrund sind in % Programme %(x86) \\Microsoft SDKs\\Windows Phone\\v7.1\\Icons\\dark in einer Standardinstallation des SDK. 
11. Wählen Sie die Bilddatei "appbar.check.rest.png" und klicken Sie auf **Hinzufügen**. Das Bild wird unter dem Bilderknoten zum Projekt hinzugefügt.
    
  
12. Wählen Sie im **Projektmappen-Explorer** die Bilddatei gerade hinzugefügt, und legen im **Eigenschaftenfenster** für die Datei, die Eigenschaft **Buildvorgang** für die Bilddatei, die "Content" und legen Sie die Eigenschaft " **In Ausgabeverzeichnis kopieren** ", "Kopieren, wenn neuer" aus.
    
  
Im nächsten Schritt fügen Sie eine Schaltfläche zum Listenformular (List.xaml) in das Projekt, und implementieren Sie den **Click** -Ereignishandler der Schaltfläche zum Navigieren zu der Seite Einstellungen in den vorherigen Schritten erstellte. Ändern Sie auch den **OnViewModelInitialization** -Ereignishandler, um eine Benachrichtigung Kanal öffnen (wenn der Benutzer sich entschieden hat, um Pushbenachrichtigungen zu abonnieren).
  
    
    

### <a name="to-modify-the-list-form"></a>So ändern Sie das Listenformular


1. Doppelklicken Sie im **Projektmappen-Explorer** unter dem Knoten **Ansichten** auf die Datei List.xaml. Die Datei wird zur Bearbeitung geöffnet.
    
  
2. Fügen Sie Markup um eine weitere Schaltfläche im **ApplicationBar** -Element der Datei, wie im folgenden Beispiel zu deklarieren.
    
```
  
...
    <phone:PhoneApplicationPage.ApplicationBar>
        <shell:ApplicationBar IsVisible="True" IsMenuEnabled="True">
            <shell:ApplicationBarIconButton x:Name="btnNew" 
                   IconUri="/Images/appbar.new.rest.png" Text="New" 
                    Click="OnNewButtonClick" />
            <shell:ApplicationBarIconButton x:Name="btnRefresh" 
                    IconUri="/Images/appbar.refresh.rest.png" Text="Refresh" IsEnabled="True" 
                    Click="OnRefreshButtonClick" />
            <shell:ApplicationBarIconButton x:Name="btnSettings" IconUri="/Images/appbar.feature.settings.rest.png" Text="Settings" IsEnabled="True" Click="OnSettingsButtonClick" />
        </shell:ApplicationBar>
    </phone:PhoneApplicationPage.ApplicationBar>
...
```

3. Die List.xaml-Datei im **Projektmappen-Explorer** ausgewählt und drücken SieF7um seine zugeordnete Code-Behind-Datei List.xaml.cs, zur Bearbeitung zu öffnen.
    
  
4. Innerhalb der Codeblock (abgegrenzt durch öffnende und schließende geschweifte Klammern), der die partiellen Klasse **ListForm** implementiert wird, fügen Sie in der Datei den folgenden Ereignishandler hinzu.
    
```cs
  
private void OnSettingsButtonClick(object sender, EventArgs e)
{
    NavigationService.Navigate(new Uri("/Settings.xaml", UriKind.Relative));
}
```

5. Suchen Sie die **OnViewModelInitialization** in der List.xaml.cs-Datei, und fügen Sie einen Anruf an die **OpenNotificationChannel** -Methode der zuvor erstellten **Notifications** -Klasse. Die geänderte Implementierung der Handler sollte dem folgenden Code ähneln.
    
```cs
  
private void OnViewModelInitialization(object sender, InitializationCompletedEventArgs e)
{
    this.Dispatcher.BeginInvoke(() =>
    {
        //If initialization has failed, show error message and return
        if (e.Error != null)
        {
            MessageBox.Show(e.Error.Message, e.Error.GetType().Name, MessageBoxButton.OK);
            return;
        }

        App.MainViewModel.LoadData(((PivotItem)Views.SelectedItem).Name);
        this.DataContext = (sender as ListViewModel);
    });

    // Open notification channel here if user has chosen to subscribe to notifications.
    if (Notifications.GetRegistrationStatus() == true)
        Notifications.OpenNotificationChannel(false);
}
```

6. Speichern Sie die Datei.
    
  
7. Um Sie dem Projekt die Bilddatei (appbar.feature.settings.rest.png) für die Schaltfläche **ApplicationBar** (BtnSettings) in der Datei List.xaml deklarierten hinzuzufügen, wählen Sie im **Projektmappen-Explorer** den Knoten Bilder Ordner.
    
  
8. Klicken Sie im Menü **Projekt** auf **Vorhandenes Element hinzufügen**. Das Fenster **Dateibrowser** wird geöffnet.
    
  
9. Navigieren Sie zu dem Ordner, in dem die standardmäßigen Windows Phone Symbolbilder durch die Windows Phone SDK 7.1 installiert wurden. (Siehe die Anmerkung im vorherigen Verfahren für den Speicherort der Bilddateien in einer Standardinstallation des SDK).
    
  
10. Wählen Sie die Datei mit dem Namen appbar.feature.settings.rest.png, und klicken Sie auf **Hinzufügen**. Das Bild wird dem Projekt unter dem Knoten Bilder hinzugefügt wird hinzugefügt.
    
  
11. Wählen Sie im **Projektmappen-Explorer** die Bilddatei gerade hinzugefügt, und legen im **Eigenschaftenfenster** für die Datei, die Eigenschaft **Buildvorgang** für die Bilddatei, die "Content" und legen Sie die Eigenschaft " **In Ausgabeverzeichnis kopieren** ", "Kopieren, wenn neuer" aus.
    
  
Fügen Sie abschließend Code hinzu der **Application_Launching** -Ereignishandler in der Datei App.xaml.cs, um die app zum Empfangen von Pushbenachrichtigungen, mithilfe der Eigenschaften und Methoden der zuvor erstellten **Notifications** -Klasse vorzubereiten.
  
    
    

### <a name="to-add-code-to-the-appxamlcs-file"></a>So fügen Sie Code in die Datei App.xaml.cs hinzu


1. Wählen Sie im **Projektmappen-Explorer** unter dem Knoten, der das Projekt Objektebene aus.
    
  
2. Drücken SieF7um seine zugeordnete Code-Behind-Datei App.xaml.cs, zur Bearbeitung zu öffnen.
    
  
3. Suchen Sie den **Application_Launching** -Ereignishandler in der Datei. (Für neue Projekte aus der Vorlage für Windows Phone SharePoint List Application erstellt, die Signatur für die Methode, die für die Ereignisbehandlung **Application_Launching** enthalten ist, aber keine Logik in der-Methode implementiert ist.)
    
  
4. Ersetzen Sie den **Application_Launching** -Ereignishandler durch den folgenden Code ein.
    
```cs
  
private void Application_Launching(object sender, LaunchingEventArgs e)
{
    // Get set up for notifications.
    Notifications.Context = App.DataProvider.Context;
    Notifications.SaveDeviceAppIdToStorage();
}
```

5. Speichern Sie die Datei.
    
  
Wenn Sie das Projekt kompilieren und die app in der Windows Phone-Emulator bereitstellen, um Sie auszuführen, können Sie durch Klicken auf die Schaltfläche **Einstellungen** in der **Anwendungsleiste** zum Anzeigen einer Seite, aus der Sie für Pushbenachrichtigungen (Abbildung 1) registrieren können.
  
    
    

**Abbildung 1. Einstellungsseite für benachrichtigungsregistrierung**

  
    
    

  
    
    
![Einstellungen-Seite für Benachrichtigungsregistrierung](../images/bee8bbc5-a93d-4695-927b-c10e0e63ddf9.gif)
  
    
    
Wenn bereitgestellt und aktiviert die PushNotificationsList -Lösung (entwickelt im Abschnitt [Erstellen Sie eine serverseitige Lösung zum Senden von Pushbenachrichtigungen basierend auf einer listenelementereignis](#BKMK_ServerSideSolution) weiter oben in diesem Thema) zu Ihrer Ziel SharePoint Server und Registrierung auf dem Telefon für Benachrichtigungen erfolgreich ist, können Sie der Liste der Projekte auf dem Server ein Element hinzugefügt, und Sie erhalten beide eine Toast-Benachrichtigung (Abbildung 2) und , wenn die app auf dem Telefon ausgeführt wird, wenn Sie eine unformatierte Benachrichtigung (Abbildung 3) in der Liste das Element hinzugefügt wird.
  
    
    

**Abbildung 2. Popupbenachrichtigung (ausgeführte app)**

  
    
    

  
    
    
![Toast-Benachrichtigung (App wird ausgeführt)](../images/19b38f1b-8f98-4e91-8384-ba0e2d3da744.gif)
  
    
    
Die Meldung angezeigt, wenn Ihre app eine Toast-Benachrichtigung empfangen, während er ausgeführt wird, hängt davon ab, wie Sie den **ShellToastNotificationReceived** -Ereignishandler in Ihrer app implementiert haben. In der **Notifications** -Klasse für in diesem Beispiel werden der Titel und Inhalt der Nachricht einfach an den Benutzer angezeigt.
  
    
    

**Abbildung 3. Unformatierte Benachrichtigung**

  
    
    

  
    
    
![Unformatierte Benachrichtigung](../images/2e5dc58a-55d2-48c6-a162-974199ff5e5c.gif)
  
    
    
Wenn die app nicht ausgeführt wird, wenn das Element der Liste hinzugefügt wird, sollte das Telefon noch eine Toast-Benachrichtigung (Abbildung 4) angezeigt werden.
  
    
    

**Abbildung 4. Toast-Benachrichtigung (app läuft nicht)**

  
    
    

  
    
    
![Toast-Benachrichtigung (App wird nicht ausgeführt)](../images/c046bc5c-1e31-4ac6-9cba-05482cc36915.gif)
  
    
    
Wenn Sie ein Element der Aufträge SharePoint-Liste, den Code hinzufügen in der Ereignisprozedur Receiver Zusammenhang mit der Liste versucht zum Senden von Benachrichtigungen mithilfe von MPNS auf Telefonen abonniert, jedoch je nach netzwerkbedingungen und anderen Faktoren, möglicherweise eine bestimmte Benachrichtigung nicht von einem Telefon empfangen werden. Sie können auf dem Server, insbesondere die Werte in den Spalten Statuscode und Header, um den Status und die Ergebnisse im Zusammenhang mit der einzelnen Benachrichtigungen zu bestimmen der Push Notification Ergebnisliste anzeigen.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15Configurepushnot_addlresources"> </a>


-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Push Notifications-Übersicht für Windows Phone](http://msdn.microsoft.com/de-DE/library/ff402558%28VS.92%29.aspx)
    
  
-  [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Microsoft SharePoint SDK für Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Microsoft SharePoint SDK für Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

