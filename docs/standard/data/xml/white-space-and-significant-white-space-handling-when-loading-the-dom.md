---
title: Behandlung von Leerräumen und signifikanten Leerräumen beim Laden des DOM
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1b141a0a-50d8-4ebd-83cd-a84449bb22b2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1d9bbb14320b84a6d417c5c28026b169092de219
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/28/2018
ms.locfileid: "47230774"
---
# <a name="white-space-and-significant-white-space-handling-when-loading-the-dom"></a>Behandlung von Leerräumen und signifikanten Leerräumen beim Laden des DOM
Beim Laden des Dokuments können Sie festlegen, dass Leerraum beibehalten wird und in der Dokumentstruktur **XmlWhitespace**-Knoten erstellt werden. Legen Sie die **PreserveWhitespace**-Eigenschaft auf „true“ fest, wenn Leerraumknoten erstellen werden sollen. Wenn die Eigenschaft auf **false** festgelegt wird (Standardeinstellung), werden keine Leerraumknoten erstellt. Knoten für signifikante Leerräume bleiben stets erhalten, und **XmlSignificantWhitespace**-Knoten werden ungeachtet der Einstellung des **PreserveWhitespace**-Flags stets im Speicher erstellt, um diese Daten darzustellen.  
  
 Wenn das Dokument aus einem Reader geladen wird, beeinflusst die Einstellung der **PreserveWhitespace**-Eigenschaft für die **XmlDocument**-Klasse nur dann das Erstellen von **XmlWhitespace**-Knoten, wenn die **WhitespaceHandling**-Eigenschaft des **XmlTextReader** nicht auf **WhitespaceHandling.None** festgelegt ist. Der Wert der **WhitespaceHandling**-Eigenschaft des Readers hat Vorrang vor der Einstellung dieses Flags für das **XmlDocument**. Weitere Informationen zu **XmlSignificantWhitespace** finden Sie unter <xref:System.Xml.XmlSignificantWhitespace>.  
  
## <a name="see-also"></a>Siehe auch

- [XML-Dokumentobjektmodell (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
