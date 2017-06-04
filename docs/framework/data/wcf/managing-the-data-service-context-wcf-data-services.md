---
title: "Verwalten des Datendienstkontextes (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 15b19d09-7de7-4638-9556-6ef396cc45ec
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Verwalten des Datendienstkontextes (WCF Data Services)
Die <xref:System.Data.Services.Client.DataServiceContext>\-Klasse kapselt Vorgänge, die für einen angegebenen Datendienst unterstützt werden.  Im Gegensatz zu [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]\-Diensten ist der Kontext nicht zustandslos.  Sie können daher mithilfe der <xref:System.Data.Services.Client.DataServiceContext>\-Klasse den Zustand auf dem Client zwischen Interaktionen mit dem Datendienst beibehalten, um Funktionen wie das Änderungsmanagement zu unterstützen.  Von dieser Klasse werden auch Identitäten verwaltet und Änderungen nachverfolgt.  
  
## Zusammenführungsoptionen und Identitätsauflösung  
 Wenn eine <xref:System.Data.Services.Client.DataServiceQuery%601> ausgeführt wird, werden die Entitäten im Antwortfeed in Objekte materialisiert.  Weitere Informationen finden Sie unter [Materialisieren von Objekten](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md).  Die Methode, mit der Einträge in einer Antwortnachricht in Objekte materialisiert werden, ist von der Identitätsauflösung und von der Zusammenführungsoption abhängig, mit der die Abfrage ausgeführt wurde.  Wenn im Bereich eines einzelnen <xref:System.Data.Services.Client.DataServiceContext> verschiedene Abfragen oder Ladeanforderungen ausgeführt werden, verfolgt der [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]\-Client nur eine einzelne Instanz eines Objekts, das über einen bestimmten Schlüsselwert verfügt.  Dieser Schlüssel, der für das Ausführen einer Identitätsauflösung verwendet wird, identifiziert eine Entität eindeutig.  
  
 In der Standardeinstellung wird vom Client nur ein Eintrag im Antwortfeed in ein Objekt für Entitäten materialisiert, die noch nicht vom <xref:System.Data.Services.Client.DataServiceContext> verfolgt werden.  Dies bedeutet, dass Änderungen an Objekten, die sich bereits im Cache befinden, nicht überschrieben werden.  Dieses Verhalten wird gesteuert, indem für Abfragen und Ladevorgänge ein <xref:System.Data.Services.Client.MergeOption>\-Wert angegeben wird.  Diese Option wird festgelegt, indem die <xref:System.Data.Services.Client.DataServiceContext.MergeOption%2A>\-Eigenschaft auf dem <xref:System.Data.Services.Client.DataServiceContext> festgelegt wird.  Der Standardwert der Zusammenführungsoption lautet <xref:System.Data.Services.Client.MergeOption>.  Mit dieser Einstellung werden nur Objekte für Entitäten materialisiert, die noch nicht verfolgt werden, d. h. vorhandene Objekte werden nicht überschrieben.  Um zu verhindern, dass Änderungen an Objekten auf dem Client durch Aktualisierungen des Datendiensts überschrieben werden, kann auch die Option <xref:System.Data.Services.Client.MergeOption> festgelegt werden.  Wenn <xref:System.Data.Services.Client.MergeOption> festgelegt wird, werden Werte von Objekten des Clients durch die aktuellen Werte aus Einträgen im Antwortfeed ersetzt. Dies gilt auch, wenn an diesen Objekten bereits Änderungen vorgenommen wurden.  Wenn eine <xref:System.Data.Services.Client.MergeOption>\-Zusammenführungsoption verwendet wird, kann der <xref:System.Data.Services.Client.DataServiceContext> keine Änderungen, die an Clientobjekten gemacht wurden, an den Datendienst senden.  Mit dieser Option werden Änderungen immer durch Werte des Datendiensts überschrieben.  
  
## Verwalten der Parallelität  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] unterstützt vollständige Parallelität, sodass der Datendienst Updatekonflikte erkennen kann.  Der Datendienstanbieter kann so konfiguriert werden, dass der Datendienst mithilfe eines Parallelitätstokens nach Änderungen an Entitäten sucht.  Dieses Token beinhaltet mindestens eine Eigenschaft eines Entitätstyps, die vom Datendienst überprüft wird, um zu bestimmen, ob sich eine Ressource geändert hat.  Parallelitätstoken, die im eTag\-Header von Antworten vom und Anforderungen an den Datendienst enthalten sind, werden vom [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]\-Client verwaltet. Weitere Informationen finden Sie unter [Aktualisieren des Datendiensts](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md).  
  
 Der <xref:System.Data.Services.Client.DataServiceContext> verfolgt Änderungen, die an Objekten vorgenommen wurden, die manuell mit <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A>, <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> und <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> oder von einer <xref:System.Data.Services.Client.DataServiceCollection%601> gemeldet wurden.  Wenn die <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>\-Methode aufgerufen wird, sendet der Client die Änderungen zurück an den Datendienst.  <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> kann fehlschlagen, wenn zwischen den Datenänderungen auf dem Client und den Änderungen im Datendienst ein Konflikt auftritt.  In einem solchen Fall müssen Sie die Entitätsressource erneut abfragen, um die Updatedaten zu erhalten.  Um Änderungen im Datendienst zu überschreiben, führen Sie die Abfrage mit der <xref:System.Data.Services.Client.MergeOption>\-Zusammenführungsoption aus.  Wenn Sie <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> erneut aufrufen, werden die auf dem Client beibehaltenen Änderungen im Datendienst beibehalten, sofern an der Ressource im Datendienst noch keine anderen Änderungen vorgenommen wurden.  
  
## Speichern von Änderungen  
 Änderungen werden in der <xref:System.Data.Services.Client.DataServiceContext>\-Instanz nachverfolgt, jedoch nicht unmittelbar an den Server gesendet.  Wenn Sie die erforderlichen Änderungen für eine bestimmte Aktivität vorgenommen haben, rufen Sie <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> auf, um alle Änderungen an den Datendienst zu übergeben.  Ein <xref:System.Data.Services.Client.DataServiceResponse>\-Objekt wird zurückgegeben, nachdem der <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>\-Vorgang abgeschlossen wurde.  Das <xref:System.Data.Services.Client.DataServiceResponse>\-Objekt enthält eine Folge von <xref:System.Data.Services.Client.OperationResponse>\-Objekten, die wiederum eine Folge von <xref:System.Data.Services.Client.EntityDescriptor>\-Instanzen oder <xref:System.Data.Services.Client.LinkDescriptor>\-Instanzen enthalten, die die beibehaltenen Änderungen oder Änderungsversuche darstellen.  Wenn eine Entität im Datendienst erstellt oder geändert wird, schließt der <xref:System.Data.Services.Client.EntityDescriptor> einen Verweis auf die aktualisierte Entität ein, der alle vom Server generierten Eigenschaftswerte enthält, z. B. den generierten `ProductID`\-Wert im vorherigen Beispiel.  Das [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]\-Objekt wird von der Clientbibliothek automatisch mit diesen neuen Werten aktualisiert.  
  
 Bei erfolgreichen Einfüge\- und Aktualisierungsvorgängen wird die Zustandseigenschaft des <xref:System.Data.Services.Client.EntityDescriptor>\- oder <xref:System.Data.Services.Client.LinkDescriptor>\-Objekts, das dem Vorgang zugeordnet ist, auf <xref:System.Data.Services.Client.EntityStates> festgelegt, und die neuen Werte werden mithilfe von <xref:System.Data.Services.Client.MergeOption> zusammengeführt.  Wenn im Datendienst ein Einfüge\-, Aktualisierungs\- oder Löschvorgang fehlschlägt, entspricht der Entitätszustand weiterhin dem Zustand vor dem Aufrufen von <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A>, und die <xref:System.Data.Services.Client.OperationResponse.Error%2A>\-Eigenschaft der <xref:System.Data.Services.Client.OperationResponse> wird auf eine <xref:System.Data.Services.Client.DataServiceRequestException> festgelegt, die Informationen zum Fehler enthält.  Weitere Informationen finden Sie unter [Aktualisieren des Datendiensts](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md).  
  
### Festlegen der HTTP\-Methode für Updates  
 Die .NET Framework\-Clientbibliothek sendet Updates an vorhandenen Entitäten standardmäßig als MERGE\-Anforderungen.  Durch eine MERGE\-Anforderung werden ausgewählte Eigenschaften der Entität aktualisiert. Der Client schließt jedoch immer alle Eigenschaften in die MERGE\-Anforderung ein, auch Eigenschaften, die nicht geändert wurden.  Das [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]\-Protokoll unterstützt auch das Senden von PUT\-Anforderungen zum Aktualisieren von Entitäten.  In einer PUT\-Anforderung wird eine vorhandene Entität im Grunde durch eine neue Instanz der Entität mit Eigenschaftswerten vom Client ersetzt.  Legen Sie zum Verwenden von PUT\-Anforderungen das <xref:System.Data.Services.Client.SaveChangesOptions>\-Flag für die <xref:System.Data.Services.Client.SaveChangesOptions>\-Enumeration fest, wenn Sie <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> aufrufen.  
  
> [!NOTE]
>  Eine PUT\-Anforderung verhält sich anders als eine MERGE\-Anforderung, wenn der Client nicht alle Eigenschaften der Entität kennt.  Dies kann vorkommen, wenn ein Entitätstyp in einen neuen Typ auf dem Client projiziert wird.  Diese Situation kann auch auftreten, wenn der Entität im Datenmodell des Diensts neue Eigenschaften hinzugefügt wurden und die <xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A>\-Eigenschaft des <xref:System.Data.Services.Client.DataServiceContext> auf `true` festgelegt ist, um solche Clientzuordnungsfehler zu ignorieren.  In diesen Fällen werden bei einer PUT\-Anforderung alle Eigenschaften, die dem Client nicht bekannt sind, auf die Standardwerte zurückgesetzt.  
  
### POST\-Tunneln  
 Standardmäßig sendet die Clientbibliothek Anforderungen zum Erstellen, Lesen, Aktualisieren und Löschen an einen [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]\-Dienst, indem die entsprechenden HTTP\-Methoden POST, GET, PUT\/MERGE\/PATCH und DELETE verwendet werden.  Auf diese Weise werden die grundlegenden REST\-Prinzipien \(Representational State Transfer\) aufrechterhalten.  Nicht jede Webserverimplementierung unterstützt jedoch den vollständigen Satz von HTTP\-Methoden.  In einigen Fällen könnten die unterstützten Methoden nur auf GET und POST beschränkt sein.  Dies kann geschehen, wenn ein Vermittler, z. B. eine Firewall, Anforderungen mit bestimmten Methoden blockiert.  Da die GET\-Methode und die POST\-Methode am häufigsten unterstützt werden, schreibt [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] eine Möglichkeit vor, um mit einer POST\-Anforderung nicht unterstützte HTTP\-Methoden auszuführen.  Dies wird als *Methodentunneln* oder *POST\-Tunneln* bezeichnet und ermöglicht es einem Client, eine POST\-Anforderung mit der Methode zu senden, die tatsächlich im benutzerdefinierten `X-HTTP-Method`\-Header angegeben ist.  Um POST\-Tunneln für Anforderungen zu ermöglichen, legen Sie die <xref:System.Data.Services.Client.DataServiceContext.UsePostTunneling%2A>\-Eigenschaft der <xref:System.Data.Services.Client.DataServiceContext>\-Instanz auf `true` fest.  
  
## Siehe auch  
 [WCF Data Services\-Clientbibliothek](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [Aktualisieren des Datendiensts](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)   
 [Asynchrone Vorgänge](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)   
 [Batchverarbeitungsvorgänge](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md)