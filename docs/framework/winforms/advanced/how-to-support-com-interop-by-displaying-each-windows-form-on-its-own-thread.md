---
title: 'Gewusst wie: Unterstützen von COM-Interop durch das Anzeigen einzelner Windows Forms in einem eigenen Thread'
ms.date: 03/30/2017
dev_langs:
- vb
helpviewer_keywords:
- COM interop [Windows Forms], Windows Forms
- COM [Windows Forms]
- Windows Forms, unmanaged
- ActiveX controls [Windows Forms], COM interop
- Windows Forms, interop
ms.assetid: a9e04765-d2de-4389-a494-a9a6d07aa6ee
ms.openlocfilehash: d0d8dfd4a19b31be790d2643847396d136098278
ms.sourcegitcommit: 64f4baed249341e5bf64d1385bf48e3f2e1a0211
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44085607"
---
# <a name="how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread"></a>Gewusst wie: Unterstützen von COM-Interop durch das Anzeigen einzelner Windows Forms in einem eigenen Thread
Sie können Probleme mit der COM-Interoperabilität beheben, indem Sie das Formular in einer [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]-Nachrichtenschleife anzeigen, die Sie mit der <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType>-Methode erstellen können.   
  
 Damit ein Windows Form aus einer COM-Clientanwendung heraus ordnungsgemäß funktioniert, müssen Sie das Formular in einer Windows Forms-Nachrichtenschleife ausführen. Hierzu können Sie einen der folgenden Ansätze verwenden:  
  
-   Verwenden Sie die <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType>-Methode, um das Windows Form anzuzeigen. Weitere Informationen finden Sie unter [Vorgehensweise: Unterstützen von COM-Interop durch Anzeigen eines Windows Forms mit der ShowDialog-Methode](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md).  
  
-   Zeigen Sie jedes Windows Form in einem separaten Thread an.  
  
 Bietet umfassende Unterstützung für dieses Feature in Visual Studio.  
  
 Siehe auch [Exemplarische Vorgehensweise: unterstützen von COM-Interop durch Anzeigen jedes Windows Forms in einem eigenen Thread](https://msdn.microsoft.com/library/ms233639\(v=vs.110\)).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird veranschaulicht, wie Sie das Formular über einen separaten Thread anzeigen und die <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType>-Methode aufrufen, um ein Windows Forms-Nachrichtensystem über diesen Thread zu starten Um diesen Ansatz zu verwenden, müssen Sie jeden Aufruf des Formulars aus der nicht verwalteten Anwendung marshallen, indem Sie die <xref:System.Windows.Forms.Control.Invoke%2A> Methode verwenden.  
  
 Dieser Ansatz erfordert, dass jede Instanz eines Formulars über ihren eigenen Thread ausgeführt wird, indem sie ihre eigene Nachrichtenschleife verwendet. Es ist nicht möglich, mehrere Nachrichtenschleifen pro Thread auszuführen. Daher können Sie die Nachrichtenschleife der Clientanwendung nicht ändern. Sie können jedoch die [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] -Komponente ändern, um einen neuen Thread zu beginnen, der seine eigene Nachrichtenschleife verwendet.  
  
 [!code-vb[System.Windows.Forms.ComInterop#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ComInterop/VB/COMForm.vb#1)]  
  
 [!code-vb[System.Windows.Forms.ComInterop#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ComInterop/VB/FormManager.vb#10)]  
  
 [!code-vb[System.Windows.Forms.ComInterop#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ComInterop/VB/Form1.vb#100)]  
  
## <a name="compiling-the-code"></a>Kompilieren des Codes  
  
-   Kompilieren Sie die Typen `COMForm`, `Form1`und `FormManager` in eine Assembly namens `COMWinform.dll`. Registrieren Sie die Assembly für COM-Interop, indem Sie eine der Methoden verwenden, die unter [Packaging an Assembly for COM](../../../../docs/framework/interop/packaging-an-assembly-for-com.md)beschrieben sind. Sie können die Assembly und deren entsprechende Typbibliotheksdatei (.tlb) in nicht verwalteten Anwendungen verwenden. Beispielsweise können Sie die Typbibliothek als Verweis in einem ausführbaren Visual Basic 6.0-Projekt verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Verfügbarmachen von .NET Framework-Komponenten in COM](../../../../docs/framework/interop/exposing-dotnet-components-to-com.md)  
 [Verpacken einer Assembly für COM](../../../../docs/framework/interop/packaging-an-assembly-for-com.md)  
 [Registrieren von Assemblys bei COM](../../../../docs/framework/interop/registering-assemblies-with-com.md)  
 [Gewusst wie: Unterstützen von COM-Interop durch Anzeigen eines Windows Forms mit der ShowDialog-Methode](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md)  
 [Übersicht über Windows Forms und nicht verwaltete Anwendungen](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications-overview.md)
