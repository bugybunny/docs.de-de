---
title: 'Ausnahmen: Der try...with-Ausdruck (F#)'
description: Erfahren Sie, wie der F#-"try...with-" Ausdruck für die Ausnahmebehandlung zu verwenden.
ms.date: 05/16/2016
ms.openlocfilehash: 588960c0f8ccedb431c37d0f1314bf1a293b638c
ms.sourcegitcommit: a885cc8c3e444ca6471348893d5373c6e9e49a47
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2018
ms.locfileid: "44042165"
---
# <a name="exceptions-the-trywith-expression"></a>Ausnahmen: Der try...with-Ausdruck

In diesem Thema wird beschrieben, die `try...with` Ausdruck, der Ausdruck, der für die Ausnahmebehandlung in der Sprache f# verwendet wird.

## <a name="syntax"></a>Syntax

```fsharp
try
    expression1
with
| pattern1 -> expression2
| pattern2 -> expression3
...
```

## <a name="remarks"></a>Hinweise

Die `try...with` Ausdruck wird verwendet, um die Behandlung von Ausnahmen in F# erläutert werden. Es ähnelt der `try...catch` -Anweisung in c#. In der vorherigen Syntax wird der Code in *expression1* möglicherweise eine Ausnahme generiert. Die `try...with` Ausdruck gibt einen Wert zurück. Wenn keine Ausnahme ausgelöst wird, wird der gesamte Ausdruck gibt den Wert der *expression1*. Wenn eine Ausnahme ausgelöst wird, jede *Muster* wiederum verglichen wird, mit der Ausnahme und für das erste übereinstimmende Muster, die den entsprechenden *Ausdruck*, bekannt als die *Ausnahmehandler*für diesen Branch ausgeführt wird und der gesamte Ausdruck den Wert des Ausdrucks, in dieser Ausnahmehandler gibt. Wenn keine übereinstimmt, wird die Ausnahme der Aufrufliste nach oben weitergegeben, bis ein entsprechender Handler gefunden wird. Die Typen der von jeder Ausdruck in die Ausnahmehandler zurückgegebenen Werte müssen der Rückgabetyp der Ausdruck in übereinstimmen der `try` Block.

In vielen Fällen bedeutet die Tatsache, dass Fehler auch, dass es keinen gültiger Wert, der die Ausdrücke in jeder Ausnahmehandler zurückgegeben werden kann. Ein häufig verwendetes Muster ist der Typ des Ausdrucks ein Optionstyp werden. Das folgende Codebeispiel veranschaulicht dieses Muster.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5601.fs)]

Ausnahmen können .NET Ausnahmen sein, oder sie können die F#-Ausnahmen werden. Sie können die F#-Ausnahmen definieren, mit der `exception` Schlüsselwort.

Eine Vielzahl von Mustern können Sie den Ausnahmetyp und andere Bedingungen filtern; die Optionen werden in der folgenden Tabelle zusammengefasst.

|Muster|Beschreibung|
|-------|-----------|
|:? *Typ der Ausnahme*|Entspricht den angegebenen Ausnahmetyp von .NET.|
|:? *Typ der Ausnahme* als *Bezeichner*|Mit der angegebenen Ausnahme .NET Typ übereinstimmt, doch bieten der Ausnahme einen benannten Wert.|
|*Ausnahme-Name*(*Argumente*)|Einen F#-Ausnahmetyp entspricht, und bindet die Argumente.|
|*identifier*|Entspricht einer beliebigen Ausnahme aus, und bindet den Namen an das Ausnahmeobjekt. Äquivalent zu **:? System.Exception als *** Bezeichner*|
|*Bezeichner* beim *Bedingung*|Entspricht einer beliebigen Ausnahme aus, wenn die Bedingung "true" ist.|

## <a name="examples"></a>Beispiele

Die folgenden Codebeispiele veranschaulichen die Verwendung der verschiedenen Ausnahme-Handler-Muster.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5602.fs)]

>[!NOTE]
Die `try...with` Konstrukt ist ein separater Ausdruck aus der `try...finally` Ausdruck. Aus diesem Grund Wenn der Code sowohl erfordert eine `with` Block und ein `finally` blockieren, müssen Sie die beiden Ausdrücke schachteln.

>[!NOTE]
Sie können `try...with` in asynchronen Workflows und anderen Berechnungsausdrücken, in dem Fall einer angepassten Version von der `try...with` Ausdruck wird verwendet. Weitere Informationen finden Sie unter [asynchrone Workflows](../asynchronous-workflows.md), und [Berechnungsausdrücke](../computation-expressions.md).

## <a name="see-also"></a>Siehe auch

- [Ausnahmebehandlung](index.md)
- [Ausnahmetypen](exception-types.md)
- [Ausnahmen: Der `try...finally`-Ausdruck](the-try-finally-expression.md)
