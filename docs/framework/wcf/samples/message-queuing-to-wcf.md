---
title: Message Queuing zu Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: 6d718eb0-9f61-4653-8a75-d2dac8fb3520
ms.openlocfilehash: cbbbab700a6602fa02160733c383a0fcaa84297b
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/08/2018
ms.locfileid: "48850673"
---
# <a name="message-queuing-to-windows-communication-foundation"></a>Message Queuing zu Windows Communication Foundation
In diesem Beispiel wird veranschaulicht, wie eine Anwendung für Message Queuing (MSMQ) eine MSMQ-Nachricht an einen Windows Communication Foundation (WCF)-Dienst senden kann. Der Dienst ist eine selbst gehostete Konsolenanwendung, die es Ihnen ermöglicht, den Dienst beim Empfang von Nachrichten in der Warteschlange zu beobachten.  
  
 Der Dienstvertrag ist `IOrderProcessor`, der einen unidirektionalen Dienst definiert, der für die Verwendung mit Warteschlangen geeignet ist. Eine MSMQ-Nachricht verfügt über keinen Aktionsheader, d h. es ist nicht möglich, verschiedene MSMQ-Nachrichten Vorgangsverträgen automatisch zuzuordnen. Deshalb kann es nur einen Vorgangsvertrag geben. Wenn Sie mehr als einen Vorgangsvertrag für den Dienst definieren möchten, muss die Anwendung Informationen darüber bereitstellen, welcher Header in der MSMQ-Nachricht (z. B. die Bezeichnung oder CorrelationID) für die Entscheidung, welcher Vorgangsvertrag erteilt werden soll, verwendet werden kann.
  
 Die MSMQ-Nachricht enthält keine Informationen darüber, welche Header den verschiedenen Parametern des Vorgangsvertrags zugeordnet sind. Der Parameter ist vom Typ <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>(`MsmqMessage<T>`), der die zugrunde liegende MSMQ-Nachricht enthält. Der Typ "T" in der Klasse <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>(`MsmqMessage<T>`) steht für die Daten, die zum MSMQ-Nachrichtentext serialisiert werden. In diesem Beispiel wird der `PurchaseOrder`-Typ zum MSMQ-Nachrichtentext serialisiert.  
  
 Im folgenden Beispielcode wird der Dienstvertrag des Diensts für die Auftragsverarbeitung gezeigt.  

```csharp
// Define a service contract.
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]
[ServiceKnownType(typeof(PurchaseOrder))]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true, Action = "*")]
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);
}
```

 Der Dienst ist selbst gehostet. Bei Verwendung von MSMQ muss die Warteschlange im Voraus erstellt werden. Dies kann manuell erfolgen oder mithilfe eines Codes. In diesem Beispiel prüft der Dienst, ob die Warteschlange vorhanden ist, und erstellt sie gegebenenfalls. Der Warteschlangenname wird aus der Konfigurationsdatei gelesen.

```csharp
public static void Main()
{
    // Get the MSMQ queue name from the application settings in
    // configuration.
    string queueName = ConfigurationManager.AppSettings["queueName"];
    // Create the MSMQ queue if necessary.
    if (!MessageQueue.Exists(queueName))
        MessageQueue.Create(queueName, true);
    …
}
```

 Der Dienst erstellt und öffnet einen <xref:System.ServiceModel.ServiceHost> für den `OrderProcessorService`, wie im folgenden Beispielcode gezeigt.

```csharp
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))
{
    serviceHost.Open();
    Console.WriteLine("The service is ready.");
    Console.WriteLine("Press <ENTER> to terminate service.");
    Console.ReadLine();
    serviceHost.Close();
}
```

 Der Name der MSMQ-Warteschlange wird im appSettings-Abschnitt der Konfigurationsdatei angegeben, wie in der folgenden Beispielkonfiguration gezeigt.

> [!NOTE]
>  Im Warteschlangennamen wird ein Punkt (.) für den lokalen Computer verwendet, und in der Pfadangabe werden umgekehrte Schrägstriche als Trennzeichen verwendet. Die WCF-Endpunktadresse gibt ein msmq.formatname-Schema, und verwendet "localhost" für den lokalen Computer. Die Adresse der Warteschlange für jeden MSMQ-Formatnamen, der sich auf Richtlinien bezieht, folgt dem msmq.formatname-Schema.

```xml
<appSettings>
    <add key="orderQueueName" value=".\private$\Orders" />
</appSettings>
```

 Die Clientanwendung ist eine MSMQ-Anwendung, die sich der <xref:System.Messaging.MessageQueue.Send%2A>-Methode bedient, um eine permanente Transaktionsnachricht an die Warteschlange zu senden, wie im folgenden Beispielcode gezeigt.

```csharp
//Connect to the queue.
MessageQueue orderQueue = new MessageQueue(ConfigurationManager.AppSettings["orderQueueName"]);

// Create the purchase order.
PurchaseOrder po = new PurchaseOrder();
po.CustomerId = "somecustomer.com";
po.PONumber = Guid.NewGuid().ToString();

PurchaseOrderLineItem lineItem1 = new PurchaseOrderLineItem();
lineItem1.ProductId = "Blue Widget";
lineItem1.Quantity = 54;
lineItem1.UnitCost = 29.99F;

PurchaseOrderLineItem lineItem2 = new PurchaseOrderLineItem();
lineItem2.ProductId = "Red Widget";
lineItem2.Quantity = 890;
lineItem2.UnitCost = 45.89F;

po.orderLineItems = new PurchaseOrderLineItem[2];
po.orderLineItems[0] = lineItem1;
po.orderLineItems[1] = lineItem2;

// Submit the purchase order.
Message msg = new Message();
msg.Body = po;
//Create a transaction scope.
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))
{

    orderQueue.Send(msg, MessageQueueTransactionType.Automatic);
    // Complete the transaction.
    scope.Complete();

}
Console.WriteLine("Placed the order:{0}", po);
Console.WriteLine("Press <ENTER> to terminate client.");
Console.ReadLine();
```

 Wenn Sie das Beispiel ausführen, werden die Client- und Dienstaktivitäten sowohl im Dienst- als auch im Clientkonsolenfenster angezeigt. Sie können sehen, wie der Dienst Nachrichten vom Client empfängt. Drücken Sie die EINGABETASTE in den einzelnen Konsolenfenstern, um den Dienst und den Client zu schließen. Beachten Sie, dass aufgrund der Verwendung einer Warteschlange der Client und der Dienst nicht gleichzeitig ausgeführt werden müssen. Sie können beispielsweise den Client ausführen, ihn schließen und anschließend den Dienst starten, der dann trotzdem noch die Nachrichten des Clients empfängt.

### <a name="to-setup-build-and-run-the-sample"></a>So richten Sie das Beispiel ein, erstellen es und führen es aus

1.  Stellen Sie sicher, dass Sie ausgeführt haben die [Schritte der Einrichtung einmaligen Setupverfahren für Windows Communication Foundation-Beispiele](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).

2.  Wenn der Dienst zuerst ausgeführt wird, wird überprüft, ob die Warteschlange vorhanden ist. Ist die Warteschlange nicht vorhanden, wird sie vom Dienst erstellt. Sie können zuerst den Dienst ausführen, um die Warteschlange zu erstellen, oder Sie können sie über den MSMQ-Warteschlangen-Manager erstellen. Führen Sie zum Erstellen einer Warteschlange in Windows 2008 die folgenden Schritte aus:

    1.  Öffnen Sie Server-Manager in Visual Studio 2012.

    2.  Erweitern Sie die **Features** Registerkarte.

    3.  Mit der rechten Maustaste **Private Meldungswarteschlangen**, und wählen Sie **neu**, **Private Warteschlange**.

    4.  Überprüfen Sie die **transaktional** Feld.

    5.  Geben Sie `ServiceModelSamplesTransacted` als Name der neuen Warteschlange.

3.  Um die C#- oder Visual Basic .NET-Edition der Projektmappe zu erstellen, befolgen Sie die unter [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)aufgeführten Anweisungen.

4.  Folgen Sie den Anweisungen, um das Beispiel in einer Konfiguration für die einzelnen Computer ausführen, [Ausführen der Windows Communication Foundation-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).

### <a name="to-run-the-sample-across-computers"></a>So führen Sie das Beispiel computerübergreifend aus

1.  Kopieren Sie die Dienstprogrammdateien aus dem Ordner \service\bin\ (unterhalb des sprachspezifischen Ordners) auf den Dienstcomputer.

2.  Kopieren Sie die Clientprogrammdateien aus dem Ordner \client\bin\ (unterhalb des sprachspezifischen Ordners) auf den Clientcomputer.

3.  Ändern Sie in der Datei Client.exe.config den Wert von orderQueueName, und geben Sie anstelle von "." den Namen des Dienstcomputers an.

4.  Starten Sie auf dem Dienstcomputer Service.exe an einer Eingabeaufforderung.

5.  Starten Sie auf dem Clientcomputer Client.exe an einer Eingabeaufforderung.

> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, fahren Sie mit [Windows Communication Foundation (WCF) und Windows Workflow Foundation (WF) Samples für .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) alle Windows Communication Foundation (WCF) herunterladen und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] Beispiele. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\MsmqToWcf`  
  
## <a name="see-also"></a>Siehe auch  
 [Warteschlangen in WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)  
 [Vorgehensweise: Nachrichtenaustausch mit WCF-Endpunkten und Message Queuing-Anwendungen](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)  
 [Message Queuing-](https://go.microsoft.com/fwlink/?LinkId=94968)
