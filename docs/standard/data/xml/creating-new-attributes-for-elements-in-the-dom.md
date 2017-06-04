---
title: "Erstellen von neuen Attributen f&#252;r Elemente im Dokumentobjektmodell | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: dd6dc920-b011-418a-b3db-f1580a7d9251
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Erstellen von neuen Attributen f&#252;r Elemente im Dokumentobjektmodell
Das Erstellen von neuen Attributen unterscheidet sich vom Erstellen anderer Knotentypen, da Attribute keine Knoten sind, sondern Eigenschaften eines Elementknotens, und in einer **XmlAttributeCollection** enthalten sind, die mit dem Element verknüpft ist.  Es gibt verschiedene Möglichkeiten, ein Attribut zu erstellen und an ein Element anzuhängen:  
  
-   Den Elementknoten abrufen und dann mit **SetAttribute** der Attributauflistung dieses Elements ein Attribut hinzufügen.  
  
-   Mit der **CreateAttribute**\-Methode einen **XmlAttribute**\-Knoten erstellen, den Elementknoten abrufen und dann mit **SetAttributeNode** den Knoten der Attributauflistung dieses Elements hinzufügen.  
  
 Im folgenden Beispiel wird veranschaulicht, wie Sie einem Element mit der **SetAttribute**\-Methode ein Attribut hinzufügen.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
  
public class Sample  
  
  public shared sub Main()  
  
  Dim doc as XmlDocument = new XmlDocument()  
  doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" & _  
              "<title>Pride And Prejudice</title>" & _  
              "</book>")  
  Dim root as XmlElement = doc.DocumentElement  
  
  'Add a new attribute.  
  root.SetAttribute("genre", "urn:samples", "novel")  
  
  Console.WriteLine("Display the modified XML...")  
  Console.WriteLine(doc.InnerXml)  
  
  end sub  
end class  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
  
public class Sample  
{  
  public static void Main()  
  {  
    XmlDocument doc = new XmlDocument();  
    doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" +  
                "<title>Pride And Prejudice</title>" +  
                "</book>");  
    XmlElement root = doc.DocumentElement;  
  
    // Add a new attribute.  
    root.SetAttribute("genre", "urn:samples", "novel");  
  
    Console.WriteLine("Display the modified XML...");  
    Console.WriteLine(doc.InnerXml);  
  }  
```  
  
 Im folgenden Beispiel wird dargestellt, wie mit der **CreateAttribute**\-Methode ein neues Attribut erstellt wird.  Anschließend wird das Attribut mithilfe der **SetAttributeNode**\-Methode der Attributauflistung des **book**\-Elements hinzugefügt.  
  
 Mit dem folgenden XML\-Code  
  
```  
<book genre='novel' ISBN='1-861001-57-5'>  
<title>Pride And Prejudice</title>  
</book>  
```  
  
 erstellen Sie ein neues Attribut. Geben Sie ihm einen Wert  
  
```vb  
Dim attr As XmlAttribute = doc.CreateAttribute("publisher")  
   attr.Value = "WorldWide Publishing"  
```  
  
```csharp  
XmlAttribute attr = doc.CreateAttribute("publisher");  
attr.Value = "WorldWide Publishing";  
```  
  
 , und fügen Sie es an das Element an  
  
```vb  
doc.DocumentElement.SetAttributeNode(attr)  
```  
  
```csharp  
doc.DocumentElement.SetAttributeNode(attr);  
```  
  
 **Ausgabe**  
  
```  
<book genre="novel" ISBN="1-861001-57-5" publisher="WorldWide Publishing">  
<title>Pride And Prejudice</title>  
</book>  
```  
  
 Den vollständigen Beispielcode finden Sie unter [XmlDocument.CreateAttribute\-Methode](frlrfSystemXmlXmlDocumentClassCreateAttributeTopic).  
  
 Sie können auch einen **XmlAttribute**\-Knoten erstellen und diesen mit der **InsertBefore**\-Methode oder der **InsertAfter**\-Methode an der entsprechenden Position in der Auflistung platzieren.  Wenn ein Attribut mit demselben Namen bereits in der Attributauflistung vorhanden ist, wird der bisherige **XmlAttribute**\-Knoten aus der Auflistung entfernt, und der neue **XmlAttribute**\-Knoten wird eingefügt.  Dies erfolgt auf die gleiche Weise wie bei der **SetAttribute**\-Methode.  Diese Methoden erfordern als Parameter einen vorhandenen Knoten, der als Referenzpunkt für die **InsertBefore**\-Methode und die **InsertAfter**\-Methode dient.  Wenn Sie keinen Referenzknoten bereitstellen, der angibt, wo der neue Knoten eingefügt werden soll, wird mit der **InsertAfter**\-Methode der neue Knoten standardmäßig am Anfang der Auflistung eingefügt.  Die Standardposition für die **InsertBefore**\-Methode ist das Ende der Auflistung, wenn kein Referenzknoten angegeben wird.  
  
 Wenn Sie eine aus Attributen bestehende **XmlNamedNodeMap** erstellt haben, können Sie mithilfe der [SetNamedItem](frlrfSystemXmlXmlNamedNodeMapClassSetNamedItemTopic)\-Methode ein Attribut anhand des Namens hinzufügen.  Weitere Informationen hierzu finden Sie unter [Knotenauflistungen in "NamedNodeMaps" und "NodeLists"](../../../../docs/standard/data/xml/node-collections-in-namednodemaps-and-nodelists.md)  
  
## Standardattribute  
 Wenn Sie ein Element erstellen, das gemäß Deklaration ein Standardattribut aufweist, wird durch das Dokumentobjektmodell \(DOM\) ein neues Standardattribut mit seinem Standardwert erstellt und an das Element angehängt.  Gleichzeitig werden die untergeordneten Knoten des Standardattributs erstellt.  
  
## Untergeordnete Knoten von Attributen  
 Die Werte eines Attributknotens werden zu dessen untergeordneten Knoten.  Es gibt nur zwei Typen von zulässigen untergeordneten Knoten: **XmlText**\-Knoten und **XmlEntityReference**\-Knoten.  Diese sind dahingehend als untergeordnete Knoten zu betrachten, dass sie von Methoden wie **FirstChild** und **LastChild** als untergeordnete Knoten verarbeitet werden.  Dieses Merkmal eines Attributs mit untergeordneten Knoten ist von Bedeutung, wenn Sie versuchen, Attribute oder untergeordnete Knoten von Attributen zu entfernen.  Weitere Informationen hierzu finden Sie unter [Entfernen von Attributen aus einem Elementknoten im Dokumentobjektmodell](../../../../docs/standard/data/xml/removing-attributes-from-an-element-node-in-the-dom.md).  
  
## Siehe auch  
 [XML\-Dokumentobjektmodell \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)