---
title: 'Gewusst wie: Aufrufen einer Delegatenmethode (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: b56866ae-abf9-4a5a-a855-486359455e9c
ms.openlocfilehash: c50a32d300aaf52efe0c55cef69d5793a98305ac
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/08/2018
ms.locfileid: "44204604"
---
# <a name="how-to-invoke-a-delegate-method-visual-basic"></a>Gewusst wie: Aufrufen einer Delegatenmethode (Visual Basic)
Dieses Beispiel zeigt, wie Sie eine Methode mit einem Delegaten zuweisen, und rufen danach diese Methode über den Delegaten.  
  
### <a name="create-the-delegate-and-matching-procedures"></a>Erstellen des Delegaten und die entsprechenden Verfahren  
  
1.  Erstellen Sie einen Delegaten, mit dem Namen `MySubDelegate`.  
  
    ```  
    Delegate Sub MySubDelegate(ByVal x As Integer)  
    ```  
  
2.  Deklarieren Sie eine Klasse, die eine Methode mit der gleichen Signatur wie der Delegat enthält.  
  
    ```  
    Class class1  
        Sub Sub1(ByVal x As Integer)  
            MsgBox("The value of x is: " & CStr(x))  
        End Sub  
    End Class  
    ```  
  
3.  Definieren Sie eine Methode, erstellt eine Instanz des Delegaten und ruft die Methode dem Delegaten zugeordnet sind, durch Aufrufen der integriertes `Invoke` Methode.  
  
    ```  
    Protected Sub DelegateTest()  
        Dim c1 As New class1  
        ' Create an instance of the delegate.  
        Dim msd As MySubDelegate = AddressOf c1.Sub1  
        ' Call the method.  
        msd.Invoke(10)  
    End Sub  
    ```  
  
## <a name="see-also"></a>Siehe auch

- [Delegate-Anweisung](../../../../visual-basic/language-reference/statements/delegate-statement.md)  
- [Delegaten](../../../../visual-basic/programming-guide/language-features/delegates/index.md)  
- [Ereignisse](../../../../visual-basic/programming-guide/language-features/events/index.md)  
- [Multithreadanwendungen](../../../../standard/threading/using-threads-and-threading.md)
