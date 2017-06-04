---
title: "Exemplarische Vorgehensweise: Beziehungs&#252;bergreifende Abfragen (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a7da43e3-769f-4e07-bcd6-552b8bde66f4
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Exemplarische Vorgehensweise: Beziehungs&#252;bergreifende Abfragen (Visual Basic)
Diese exemplarische Vorgehensweise veranschaulicht die Verwendung von [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]\-*Zuordnungen*, um Fremdschlüsselbeziehungen in der Datenbank darzustellen.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Diese exemplarische Vorgehensweise wurde mithilfe von Visual Basic\-Entwicklungseinstellungen geschrieben.  
  
## Vorbereitungsmaßnahmen  
 Sie müssen die [Exemplarische Vorgehensweise: Einfaches Objektmodell und Abfrage \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-simple-object-model-and-query-visual-basic.md) abgeschlossen haben.  Diese exemplarische Vorgehensweise basiert auf diesem Schritt und erfordert die Datei northwnd.mdf im Verzeichnis c:\\linqtest.  
  
## Übersicht  
 Diese exemplarische Vorgehensweise umfasst drei Hauptaufgaben:  
  
-   Hinzufügen einer Entitätsklasse zur Darstellung der Orders\-Tabelle in der Beispieldatenbank Northwind.  
  
-   Ergänzen von Anmerkungen zur `Customer`\-Klasse, um die Beziehung zwischen der `Customer`\-Klasse und der `Order`\-Klasse zu erweitern.  
  
-   Erstellen und Ausführen einer Abfrage, um das Abrufen von `Order`\-Informationen unter Verwendung der `Customer`\-Klasse zu testen.  
  
## Zuordnen von Beziehungen über Tabellen hinweg  
 Erstellen Sie nach der Definition der `Customer`\-Klasse die Definition der `Order`\-Entitätsklasse, die den folgenden Code enthält. Dieser gibt an, dass `Orders.Customer` ein Fremdschlüssel zu `Customers.CustomerID` ist.  
  
#### So fügen Sie die Order\-Entitätsklasse hinzu  
  
-   Geben Sie den folgenden Code nach der `Customer`\-Klasse ein, oder fügen Sie ihn ein:  
  
     [!code-vb[DLinqWalk2VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#1)]  
  
## Hinzufügen von Anmerkungen zu einer Customer\-Klasse  
 In diesem Schritt fügen Sie der `Customer`\-Klasse Anmerkungen hinzu, um deren Beziehung zur `Order`\-Klasse anzugeben.  \(Diese Ergänzung ist nicht unbedingt erforderlich, da die Definition der Beziehungen in beide Richtungen zum Erstellen der Verbindung ausreicht.  Mithilfe dieser Anmerkung können Sie jedoch leicht in allen Richtungen zwischen den Objekten navigieren.\)  
  
#### So fügen Sie der Customer\-Klasse Anmerkungen hinzu  
  
-   Geben Sie den folgenden Code in die `Customer`\-Klasse ein, oder fügen Sie ihn ein:  
  
     [!code-vb[DLinqWalk2VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#2)]  
  
## Erstellen und Ausführen einer Abfrage über die Customer\-Order\-Beziehung hinweg  
 Sie können nun direkt auf die `Order`\-Objekte zugreifen, und zwar von den `Customer`\-Objekten aus oder in umgekehrter Richtung.  Sie benötigen keinen expliziten *Join* zwischen Kunden und Bestellungen.  
  
#### So greifen Sie mithilfe von Customer\-Objekten auf Order\-Objekte zu  
  
1.  Ändern Sie die `Sub Main`\-Methode durch das Eingeben oder Einfügen des folgenden Codes in die Methode:  
  
     [!code-vb[DLinqWalk2VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#3)]  
  
2.  Drücken Sie F5, um die Anwendung zu debuggen.  
  
     Zwei Namen werden im Meldungsfeld angezeigt, und das Konsolenfenster zeigt den generierten SQL\-Code an.  
  
3.  Schließen Sie das Meldungsfeld, um das Debuggen zu beenden.  
  
## Erstellen einer Datenbankansicht mit strikter Typbindung  
 Es ist viel leichter, mit einer Datenbankansicht mit strikter Typbindung zu beginnen.  Bei strikter Typbindung des <xref:System.Data.Linq.DataContext.GetTable%2A>\-Objekts benötigen Sie keine Aufrufe von <xref:System.Data.Linq.DataContext>.  Sie können Tabellen mit strikter Typbindung in allen Abfragen verwenden, wenn Sie das <xref:System.Data.Linq.DataContext>\-Objekt mit strikter Typbindung verwenden.  
  
 In den folgenden Schritten erstellen Sie `Customers` als Tabelle mit strikter Typbindung und Zuordnung zur Customers\-Tabelle in der Datenbank.  
  
#### So erstellen Sie die striktre Typbindung für das DataContext\-Objekt  
  
1.  Fügen Sie den folgenden Code oberhalb der Deklaration der `Customer`\-Klasse hinzu.  
  
     [!code-vb[DLinqWalk2VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#4)]  
  
2.  Ändern Sie die `Sub Main`\-Methode wie folgt, damit diese den <xref:System.Data.Linq.DataContext> mit strikter Typbindung verwendet:  
  
     [!code-vb[DLinqWalk2VB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#5)]  
  
3.  Drücken Sie F5, um die Anwendung zu debuggen.  
  
     Die Ausgabe im Konsolenfenster lautet:  
  
     `ID=WHITC`  
  
4.  Drücken Sie die EINGABETASTE im Konsolenfenster, um die Anwendung zu schließen.  
  
5.  Klicken Sie im Menü **Datei** auf **Alle speichern**, wenn Sie diese Anwendung speichern möchten.  
  
## Nächste Schritte  
 Die nächste exemplarische Vorgehensweise \([Exemplarische Vorgehensweise: Bearbeiten von Daten \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-manipulating-data-visual-basic.md)\) veranschaulicht, wie Daten bearbeitet werden.  Diese exemplarische Vorgehensweise setzt nicht voraus, dass Sie die beiden in dieser Serie abgeschlossenen exemplarischen Vorgehensweisen speichern.  
  
## Siehe auch  
 [Lernen mit exemplarischen Vorgehensweisen](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)