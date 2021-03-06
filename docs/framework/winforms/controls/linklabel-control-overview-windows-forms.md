---
title: Übersicht über das LinkLabel-Steuerelement (Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- LinkLabel
helpviewer_keywords:
- links [Windows Forms], LinkLabel control
- Label control [Windows Forms], about Label control
- LinkLabel control [Windows Forms], about LinkLabel control
ms.assetid: 9e248549-10ca-43a3-bb5e-60f583d369f1
ms.openlocfilehash: 40326a9055ff51efae5f4c64744d0966870c6f6b
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33535011"
---
# <a name="linklabel-control-overview-windows-forms"></a>Übersicht über das LinkLabel-Steuerelement (Windows Forms)
Windows Forms <xref:System.Windows.Forms.LinkLabel> Steuerelement ermöglicht es Ihnen, Windows Forms-Anwendungen Weblinks hinzu. Können Sie die <xref:System.Windows.Forms.LinkLabel> Control für alle Elemente, die Sie verwenden können, die <xref:System.Windows.Forms.Label> für steuern; Sie können auch Teile des Texts als Link in einer Datei, einem Ordner oder einer Webseite festlegen.  
  
## <a name="what-you-can-do-with-the-linklabel-control"></a>Was können Sie mit dem LinkLabel-Steuerelement tun.  
 Zusätzlich zu allen Eigenschaften, Methoden und Ereignisse der <xref:System.Windows.Forms.Label> -Steuerelement, das <xref:System.Windows.Forms.LinkLabel> Steuerelement verfügt über Eigenschaften für Links und Linkfarben. Die <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> Eigenschaft legt den Bereich des Texts, der die Verknüpfung aktiviert. Die <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>, <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>, und <xref:System.Windows.Forms.LinkLabel.ActiveLinkColor%2A> Eigenschaften legen die Farben des Links. Die <xref:System.Windows.Forms.LinkLabel.LinkClicked> Ereignis bestimmt, was geschieht, wenn der Text des Links ausgewählt ist.  
  
 Der einfachsten Verwendung von der <xref:System.Windows.Forms.LinkLabel> Steuerelement wird zum Anzeigen einer einzelnen Link mit der <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> -Eigenschaft, aber Sie können auch mehrere Links mit Anzeigen der <xref:System.Windows.Forms.LinkLabel.Links%2A> Eigenschaft. Die <xref:System.Windows.Forms.LinkLabel.Links%2A> Eigenschaft ermöglicht Ihnen, eine Sammlung von Links zugreifen. Sie können auch angeben, Daten in die <xref:System.Windows.Forms.LinkLabel.Link.LinkData%2A> -Eigenschaft jedes einzelnen <xref:System.Windows.Forms.LinkLabel.Link> Objekt. Der Wert, der die <xref:System.Windows.Forms.LinkLabel.Link.LinkData%2A> Eigenschaft kann verwendet werden, um den Speicherort einer Datei mit Anzeige oder die Adresse einer Website zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.LinkLabel>  
 [Übersicht über das Label-Steuerelement](../../../../docs/framework/winforms/controls/label-control-overview-windows-forms.md)  
 [Gewusst wie: Verknüpfen eines Objekts oder einer Webseite mit dem LinkLabel-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/link-to-an-object-or-web-page-with-wf-linklabel-control.md)  
 [Gewusst wie: Ändern der Darstellung des LinkLabel-Steuerelements in Windows Forms](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)
