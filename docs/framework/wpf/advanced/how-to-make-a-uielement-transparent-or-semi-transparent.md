---
title: 'Gewusst wie: Formatieren von "UIElement" als transparent oder halbtransparent'
ms.date: 03/30/2017
helpviewer_keywords:
- UIElements [WPF], transparency
- opacity [WPF], of UIElements
- transparency of UIElements [WPF]
- UIElements [WPF], opacity
ms.assetid: a49fc8d6-7b32-4f28-9122-39b632a19b4b
ms.openlocfilehash: 7bf79848edb84a5bd93d1196fbe0b3196d159ff3
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33545310"
---
# <a name="how-to-make-a-uielement-transparent-or-semi-transparent"></a>Gewusst wie: Formatieren von "UIElement" als transparent oder halbtransparent
Dieses Beispiel zeigt, wie Sie eine <xref:System.Windows.UIElement> transparenten oder halb transparent. Um ein Element transparenten oder halb transparent zu gestalten, legen Sie dessen <xref:System.Windows.UIElement.Opacity%2A> Eigenschaft. Der Wert `0.0` Blendet das Element vollständig transparent, während ein Wert von `1.0` vollständig deckend das Element. Der Wert `0.5` Blendet das Element 50 % undurchsichtig usw. Ein Element <xref:System.Windows.UIElement.Opacity%2A> festgelegt ist, um `1.0` standardmäßig.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die <xref:System.Windows.UIElement.Opacity%2A> einer Schaltfläche `0.25`, dass die Schaltfläche und dessen Inhalt (in diesem Fall wird der Text der Schaltfläche) mit 25 % nicht transparent.  
  
 [!code-xaml[brushsamples_snip#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#2)]  
  
 [!code-csharp[brushsamples_procedural_snip#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#2)]  
  
 Wenn Inhalt des Elements eigene haben <xref:System.Windows.UIElement.Opacity%2A> Einstellungen, die diese Werte werden auf das enthaltende Elemente multipliziert <xref:System.Windows.UIElement.Opacity%2A>.  
  
 Im folgenden Beispiel wird einer Schaltfläche <xref:System.Windows.UIElement.Opacity%2A> auf `0.25`, und die <xref:System.Windows.UIElement.Opacity%2A> von einer <xref:System.Windows.Controls.Image> Steuerelement auf die Schaltfläche mit `0.5`. Daher wird das Bild 12,5 % undurchsichtig angezeigt wird: 0,25 * 0,5 = 0,125.  
  
 [!code-xaml[brushsamples_snip#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#3)]  
  
 [!code-csharp[brushsamples_procedural_snip#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#3)]  
  
 Eine weitere Möglichkeit zum Steuern der Deckkraft eines Elements wird die Deckkraft der Festlegen der <xref:System.Windows.Media.Brush> , zeichnet das Element. Dieser Ansatz ermöglicht es Ihnen, gezielt die Deckkraft der Teile eines Elements zu ändern, und bietet Leistungsvorteile gegenüber des Elements <xref:System.Windows.UIElement.Opacity%2A> Eigenschaft. Im folgenden Beispiel wird die <xref:System.Windows.Media.Brush.Opacity%2A> von einer <xref:System.Windows.Media.SolidColorBrush> verwendet, um der Schaltfläche zu zeichnen <xref:System.Windows.Controls.Control.Background%2A> festgelegt ist, um `0.25`. Folglich des Pinsels Hintergrund ist 25 % undurchsichtig, aber dessen Inhalt (der Text der Schaltfläche) bleiben 100 % undurchsichtig.  
  
 [!code-xaml[brushsamples_snip#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#4)]  
  
 [!code-csharp[brushsamples_procedural_snip#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#4)]  
  
 Sie können auch die Deckkraft einzelner Farben innerhalb eines Pinsels steuern. Weitere Informationen zu Farben und Pinsel, finden Sie unter [Zeichnen mit Volltonfarben und Farbverläufen (Übersicht)](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md). Ein Beispiel zum Animieren der Deckkraft eines Elements finden Sie unter [Animieren der Deckkraft eines Elements oder Pinsel](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-the-opacity-of-an-element-or-brush.md).
