---
title: Erstellen einer Klassenbibliothek mit Visual Basic und .NET Core in Visual Studio 2017
description: Erfahren Sie, wie Sie eine in Visual Basic geschriebene Klassenbibliothek mithilfe von Visual Studio 2017 erstellen.
keywords: .NET Core, .NET Standard-Klassenbibliothek, Visual Studio 2017, Visual Basic
author: rpetrusha
ms.author: ronpet
ms.date: 08/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-vb
ms.devlang: vb
ms.translationtype: HT
ms.sourcegitcommit: 3a25c1c3b540bac8ef963a8bbf708b0700c3e9e2
ms.openlocfilehash: a933e1eef6e4e9814aeba4206469a64563a7e91d
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---

# <a name="building-a-class-library-with-visual-basic-and-net-core-in-visual-studio-2017"></a>Erstellen einer Klassenbibliothek mit Visual Basic und .NET Core in Visual Studio 2017

Eine *Klassenbibliothek* definiert die Typen und Methoden, die von einer Anwendung aufgerufen werden können. Eine Klassenbibliothek, die sich auf .NET Standard 2.0 bezieht, ermöglicht das Aufrufen der Bibliothek aus jeder .NET-Implementierung, die diese Version von .NET Standard unterstützt. Wenn Sie die Klassenbibliothek fertig stellen, können Sie entscheiden, ob Sie sie als Drittanbieterkomponente verteilen oder als Komponente mit einer oder mehreren Anwendungen in ein Paket einbeziehen möchten.

> [!NOTE]
> Eine Liste der .NET Standard-Versionen und der Plattformen, die sie unterstützen, finden Sie unter [.NET-Standard](../../standard/net-standard.md).

In diesem Thema erstellen Sie eine einfache Hilfsprogrammbibliothek, die eine einzelne Methode zur Behandlung von Zeichenfolgen enthält. Sie implementieren sie als [Erweiterungsmethode](../../visual-basic/programming-guide/language-features/procedures/extension-methods.md), damit sie aufgerufen werden kann, als wäre sie ein Mitglied der <xref:System.String> Klasse.

## <a name="creating-a-class-library-solution"></a>Erstellen einer Klassenbibliotheks-Projektmappe

Zunächst erstellen Sie eine Projektmappe für Ihre Klassenbibliotheksprojekt und die zugehörigen Projekte. Eine Visual Studio-Projektmappe dient nur als Container für ein oder mehrere Projekte. So erstellen Sie die Projektmappe:

1. Wählen Sie auf der Visual Studio-Menüleiste **Datei** > **Neu** > **Projekt** aus.

1. Erweitern Sie im Dialogfeld **Neues Projekt** den Knoten **Andere Projekttypen**, und wählen Sie **Visual Studio-Projektmappen** aus. Nennen Sie die Projektmappe „ClassLibraryProjects“, und wählen Sie die **OK**-Schaltfläche aus.

   ![Dialogfeld "Neues Projekt"](./media/library-with-visual-studio/newproject.png)

## <a name="creating-the-class-library-project"></a>Erstellen des Klassenbibliotheksprojekts

Erstellen Sie Ihr Klassenbibliotheksprojekt:

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf die Projektmappendatei **ClassLibraryProjects**, und wählen Sie im Kontextmenü **Hinzufügen** > **Neues Projekt** aus.

1. Erweitern Sie den Knoten **Visual Basic** im Dialogfeld **Neues Projekt hinzufügen**, klicken Sie dann auf den Knoten **.NET Standard** und anschließend auf die Projektvorlage **Klassenbibliothek (.NET Standard)**. Geben Sie im Textfeld **Name** „StringLibrary“ als Namen des Projekts ein. Wählen Sie **OK**, um das Klassenbibliotheksprojekt zu erstellen.

   ![Dialogfeld „Neues Projekt hinzufügen“](./media/vb-library-with-visual-studio/libproject.png)

   Das Codefenster öffnet sich dann in der Visual Studio-Entwicklungsumgebung. 
 
   ![Visual Studio-Anwendungsfenster, das die den Standardvorlagencode der Klassenbibliothek zeigt](./media/vb-library-with-visual-studio/stringlibrary.png)

1. Stellen Sie sicher, dass die Bibliothek auf die richtige Version von .NET Standard zielt. Klicken Sie mit der rechten Maustaste auf das Bibliotheksprojekt im Fenster des **Projektmappen-Explorer**, und klicken Sie dann auf **Eigenschaften**. Das Textfeld **Zielframework** zeigt dann, dass .NET Standard 2.0 als Ziel verwendet wird.

   ![Projekteigenschaften für die Klassenbibliothek](./media/library-with-visual-studio/properties.png)

1. Löschen Sie im Dialogfeld **Eigenschaften** außerdem den Text im Textfeld **Stammnamespace**. Für jedes Projekt erstellt Visual Basic automatisch einen Namespace, der dem Projektnamen entspricht. Außerdem sind alle Namespaces, die in den Quellcodedateien definiert sind, übergeordnete Elemente dieses Namespace. Wir möchten einen Namespace auf oberster Ebene definieren, indem wir das Schlüsselwort [`namespace`](../../visual-basic/language-reference/statements/namespace-statement.md) verwenden.
  
1. Ersetzen Sie den Code im Codefenster durch den folgenden Code, und speichern Sie die Datei:

  [!CODE-vb[ClassLib #1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/stringlibrary.vb)]

   Die Klassenbibliothek, `UtilityLibraries.StringLibrary`, enthält eine Methode namens `StartsWithUpper`, welche einen <xref:System.Boolean> Wert zurückgibt, der angibt, ob die aktuelle Zeichenfolgeninstanz mit einem Großbuchstaben beginnt. Der Unicode-Standard unterscheidet Groß- und Kleinschreibung. Die Methode <xref:System.Char.IsUpper(System.Char)?displayProperty=fullName> gibt `true` zurück, wenn ein Zeichen ein Großbuchstabe ist.

1. Wählen Sie auf der Menüleiste **Erstellen** > **Projektmappe erstellen** aus. Das Projekt sollte fehlerfrei kompiliert werden.

   ![Ausgabebereich, der zeigt, dass der Buildvorgang erfolgreich war](./media/library-with-visual-studio/buildsucceeds.png)



## <a name="next-step"></a>Nächster Schritt

Sie haben die Bibliothek erfolgreich erstellt. Aber da Sie keine ihrer Methoden aufgerufen haben, wissen Sie nicht, ob sie wie erwartet funktioniert. Der nächste Schritt bei der Entwicklung Ihrer Bibliothek ist ihr Test mithilfe eines [Komponententestprojekts](testing-library-with-visual-studio.md).
