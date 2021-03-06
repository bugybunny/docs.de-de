---
title: Strukturen (C#-Programmierhandbuch)
ms.date: 08/21/2018
helpviewer_keywords:
- C# language, structs
- structs [C#]
ms.assetid: b7cf4ff2-0eb7-4e5c-93d5-b2196b4f5d89
ms.openlocfilehash: 27d4b0d7edf1b5e89e84ac1df5783d68ebb4efe0
ms.sourcegitcommit: 4b6490b2529707627ad77c3a43fbe64120397175
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2018
ms.locfileid: "44259486"
---
# <a name="structs-c-programming-guide"></a>Strukturen (C#-Programmierhandbuch)

Strukturen werden mit dem [struct](../../language-reference/keywords/struct.md)-Schlüsselwort definiert, beispielsweise:  
  
[!code-csharp[csProgGuideObjects#39](./codesnippet/CSharp/structs_1.cs)]  
  
Strukturen weisen größtenteils die gleiche Syntax wie Klassen auf. Der Name der Struktur muss ein gültiger C#- [Bezeichnername](../inside-a-program/identifier-names.md) sein. Strukturen sind auf folgende Weisen eingeschränkter als Klassen:  
  
- Innerhalb einer Strukturdeklaration können Felder nicht initialisiert werden, außer Sie werden als const oder static deklariert.  
- Eine Struktur kann keinen Standardkonstruktor (ein Konstruktor ohne Parameter) oder Finalizer deklarieren.  
- Strukturen werden bei Zuweisung kopiert. Wenn eine Struktur einer neuen Variable zugewiesen wird, werden alle Daten kopiert, und jede Änderung an der neuen Kopie ändert nicht die Daten für das Original. Es ist wichtig, sich das zu merken, wenn Sie mit Sammlungen von Wertetypen wie `Dictionary<string, myStruct>` arbeiten.  
- Im Gegensatz zu Klassen, die Verweistypen sind, sind Strukturen Werttypen.  
- Strukturen können im Gegensatz zu Klassen ohne den Operator `new` instanziiert werden.  
- Strukturen können Konstruktoren deklarieren, die Parameter besitzen. 
- Eine Struktur kann nicht von einer anderen Struktur oder Klasse erben, und sie kann auch nicht die Basis einer Klasse sein. Alle Strukturen erben direkt von <xref:System.ValueType>, das von <xref:System.Object> erbt.  
- Eine Struktur kann Schnittstellen implementieren.  
- Eine Struktur kann als ein Nullable-Typ verwendet werden und kann einen NULL-Wert zugewiesen bekommen.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  

Weitere Informationen finden Sie unter:   
  
- [Verwenden von Strukturen](using-structs.md)
- [Konstruktoren](constructors.md)
- [Typen mit Nullwert](../nullable-types/index.md)
- [Gewusst wie: Unterschiede zwischen dem Übergeben einer Struktur und dem Übergeben eines Klassenverweises an eine Methode](how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md)
- [Gewusst wie: Implementieren von benutzerdefinierten Konvertierungen zwischen Strukturen](../statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)

## <a name="see-also"></a>Siehe auch

- [C#-Programmierhandbuch](../index.md)
- [Klassen und Strukturen](index.md)
- [Klassen](classes.md)
- [Bezeichnernamen](../inside-a-program/identifier-names.md)
