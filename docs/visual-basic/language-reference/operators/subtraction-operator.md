---
title: '- Operator (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.Negate
- vb.-
helpviewer_keywords:
- operator [Visual Basic]
- operators [Visual Basic], subtraction
- operators [Visual Basic], difference
- negation operator [Visual Basic]
- operators [Visual Basic], arithmetic
- subtraction operator [Visual Basic], syntax
- arithmetic operators [Visual Basic], subtraction
- difference operator [Visual Basic]
- math operators [Visual Basic]
- operators [Visual Basic], negation
- minus operator [Visual Basic]
ms.assetid: bff2c368-662d-4c92-ac87-1d9bdfd3426a
ms.openlocfilehash: 4df8eb3844ed20fd24ca375f77cea46b9c6cee37
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33604314"
---
# <a name="--operator-visual-basic"></a>--Operator (Visual Basic)
Gibt die Differenz zwischen zwei numerischen Ausdrücken oder den negativen Wert eines numerischen Ausdrucks zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
      expression1 – expression2  
- or -  
– expression1  
```  
  
## <a name="parts"></a>Teile  
 `expression1`  
 Erforderlich. Ein beliebiger numerischer Ausdruck.  
  
 `expression2`  
 Erforderlich, es sei denn, die `–` Operator einen negativen Wert berechnet wird. Ein beliebiger numerischer Ausdruck.  
  
## <a name="result"></a>Ergebnis  
 Das Ergebnis ist der Unterschied zwischen `expression1` und `expression2`, oder der negierte Wert der `expression1`.  
  
 Datentyp des Ergebnisses ist ein numerischer Typ für die Datentypen der entsprechenden `expression1` und `expression2`. Finden Sie in den Tabellen "Ganzzahlarithmetik" in [Datentypen von Operatorergebnissen Daten](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).  
  
## <a name="supported-types"></a>Unterstützte Typen  
 Alle numerischen Typen. Dazu gehören auch die Typen ohne Vorzeichen und Gleitkommatypen und `Decimal`.  
  
## <a name="remarks"></a>Hinweise  
 In der ersten Verwendung in der zuvor gezeigten Syntax gezeigt die `–` Operator ist der *binäre* arithmetischer Subtraktionsoperator für die Differenz zwischen zwei numerische Ausdrücke.  
  
 Im zweiten Anwendungsbeispiel in der zuvor gezeigten Syntax der `–` Operator ist der *unäre* Negationsoperator für den negativen Wert eines Ausdrucks. In diesem Sinn, besteht die Negation Umkehrung des Vorzeichens eines `expression1` , damit das Ergebnis positiv ist. wenn `expression1` ist ein negativer Wert.  
  
 Wenn einer der Ausdrücke ergibt [nichts](../../../visual-basic/language-reference/nothing.md)die `–` Operator wird er als 0 (null) behandelt.  
  
> [!NOTE]
>  Die `–` Operator kann *überladen*, was bedeutet, dass eine Klasse oder Struktur sein Verhalten definieren kann, wenn ein Operand den Typ der betreffenden Klasse oder Struktur hat. Wenn im Code dieser Operator auf eine solche Klasse oder Struktur verwendet, stellen Sie sicher, dass Sie dessen neu definierten Verhalten verstehen. Weitere Informationen finden Sie unter [Operatorprozeduren](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die `–` Operator zum Berechnen und Zurückgeben des Unterschied zwischen zwei Zahlen liegt, und klicken Sie dann eine Zahl zu negieren.  
  
 [!code-vb[VbVbalrOperators#10](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/subtraction-operator_1.vb)]  
  
 Nach der Ausführung dieser Anweisungen `binaryResult` enthält 124.45 und `unaryResult` –334.90 enthält.  
  
## <a name="see-also"></a>Siehe auch  
 [Operator-=-Operator (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md) [arithmetische Operatoren](../../../visual-basic/language-reference/operators/arithmetic-operators.md)  
 [Operator Precedence in Visual Basic (Operatorrangfolge in Visual Basic)](../../../visual-basic/language-reference/operators/operator-precedence.md)  
 [Nach Funktionalität sortierte Operatoren](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)  
 [Arithmetische Operatoren in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
