---
title: Verpacken einer Assembly für COM
ms.date: 03/30/2017
helpviewer_keywords:
- exposing .NET Framework components to COM
- COM interop, packaging assemblies
- packaging assemblies for COM
- Tlbexp.exe
- TypeLibConverter class
- .NET Services Installation tool
- Assembly Registration tool
- Type Library Exporter
- Reqsvcs.exe
- interoperation with unmanaged code, exposing .NET Framework components
- interoperation with unmanaged code, packaging assemblies
- COM interop, exposing COM components
- Reqasm.exe
ms.assetid: 39dc55aa-f2a1-4093-87bb-f1c0edb6e761
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f2906159c7474b42f81bdf066855072466b6be63
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33392395"
---
# <a name="packaging-an-assembly-for-com"></a>Verpacken einer Assembly für COM
COM-Entwickler profitieren von den folgenden Informationen zu den verwalteten Typen, die sie in ihre Anwendung integrieren möchten:  
  
-   Eine Liste von Typen, die COM-Anwendungen nutzen können  
  
     Einige verwalteten Typen sind nicht für COM sichtbar; einige sind sichtbar, aber nicht erstellbar, und andere sind sichtbar und erstellbar. Eine Assembly kann eine beliebige Kombination von nicht sichtbaren, sichtbaren, nicht erstellbaren und erstellbaren Typen umfassen. Aus Gründen der Vollständigkeit identifizieren Sie die Typen in einer Assembly, die für COM verfügbar gemacht werden sollen, insbesondere, wenn diese Typen eine Teilmenge der Typen sind, die für .NET Framework verfügbar gemacht werden sollen.  
  
     Weitere Informationen finden Sie unter [Qualifizieren von .NET-Typen für die Interoperation](qualifying-net-types-for-interoperation.md).  
  
-   Anweisungen der Versionsverwaltung  
  
     Verwaltete Klassen, die die Klassenschnittstelle (eine von COM-Interop generierte Schnittstelle) implementieren, unterliegen Einschränkungen der Versionsverwaltung.  
  
     Richtlinien zur Verwendung der Klassenschnittstelle finden Sie unter [Einführung in die Klassenschnittstelle](com-callable-wrapper.md#introducing-the-class-interface).  
  
-   Anweisungen zur Bereitstellung  
  
     Assemblys mit starken Namen, die von einem Herausgeber signiert wurden, können im globalen Assemblycache installiert werden. Nicht signierte Assemblys müssen als private Assemblys auf dem Computer des Benutzers installiert werden.  
  
     Weitere Informationen finden Sie unter [Überlegungen zur Assemblysicherheit](../app-domains/assembly-security-considerations.md).  
  
-   Einbindung der Typbibliothek  
  
     Die meisten Typen erfordern eine Typbibliothek, wenn sie von einer COM-Anwendung genutzt werden. Sie können eine Typbibliothek generieren oder COM-Entwickler mit der Ausführung dieser Aufgabe betreuen. Die [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] bietet die folgenden Optionen zum Generieren einer Typbibliothek:  
  
    -   [Type Library Exporter-Tool](#cpconpackagingassemblyforcomanchor1)  
  
    -   [TypeLibConverter-Klasse](#cpconpackagingassemblyforcomanchor2)  
  
    -   [Assembly Registration-Tool](#cpconpackagingassemblyforcomanchor3)  
  
    -   [.NET Services Installation-Tool](#cpconpackagingassemblyforcomanchor4)  
  
     Unabhängig vom Mechanismus, den Sie auswählen, sind nur öffentliche Typen in der von Ihnen bereitgestellten Assembly in der generierten Typbibliothek enthalten.  
  
     Sie können eine Typbibliothek als separate Datei verpacken oder sie als Win32-Ressourcendatei in eine .NET-basierte Anwendung einbetten. Microsoft Visual Basic 6.0 führt diese Aufgabe automatisch für Sie aus. Bei der Verwendung von [!INCLUDE[vbprvbext](../../../includes/vbprvbext-md.md)] müssen Sie die Typbibliothek jedoch manuell einbetten. Weitere Informationen finden Sie unter [Vorgehensweise: Einbetten von Typbibliotheken als Win32-Ressourcen in .NET-basierten Anwendungen](https://msdn.microsoft.com/library/c97b4b8c-2ab7-4ac7-8fc8-0ba5c5d59c44(v=vs.100)).  
  
<a name="cpconpackagingassemblyforcomanchor1"></a>   
## <a name="type-library-exporter"></a>Type Library Exporter-Tool  
 [Type Library Exporter (Tlbexp.exe)](../tools/tlbexp-exe-type-library-exporter.md) ist ein Befehlszeilentool, das die in einer Assembly enthaltenen Klassen und Schnittstellen in eine COM-Typbibliothek konvertiert. Sobald die Typinformationen der Klasse verfügbar sind, können COM-Clients eine Instanz der .NET-Klasse erstellen und die Methoden der Instanz aufrufen, als ob es sich um ein COM-Objekt handeln würde. Tlbexp.exe konvertiert eine ganze Assembly gleichzeitig. Sie können mit Tlbexp.exekeine Typinformationen für einen Teil der in der Assembly definierten Typen generieren.  
  
<a name="cpconpackagingassemblyforcomanchor2"></a>   
## <a name="typelibconverter-class"></a>TypeLibConverter-Klasse  
 Die <xref:System.Runtime.InteropServices.TypeLibConverter>-Klasse im **System.Runtime.Interop**-Namespace konvertiert die Klassen und Schnittstellen, die in einer Assembly enthalten sind, in eine COM-Typbibliothek. Diese API erzeugt dieselben Typinformationen wie das Type Library Exporter-Tool, das im vorherigen Abschnitt beschrieben ist.  
  
 Die **TypeLibConverter-Klasse** implementiert die <xref:System.Runtime.InteropServices.ITypeLibConverter>.  
  
<a name="cpconpackagingassemblyforcomanchor3"></a>   
## <a name="assembly-registration-tool"></a>Assembly Registration-Tool  
 Das [Assembly Registration-Tool (Regasm.exe)](../tools/regasm-exe-assembly-registration-tool.md) kann eine Typbibliothek beim Anwenden der **/tlb:**-Option generieren und registrieren. COM-Clients erfordern, dass Typbibliotheken in der Windows-Registrierung installiert werden. Ohne diese Option registriert Regasm.exe nur die Typen in einer Assembly, nicht die Typbibliothek. Die Registrierung der Typen in einer Assembly, und die Registrierung der Typbibliothek sind verschiedene Aktivitäten.  
  
<a name="cpconpackagingassemblyforcomanchor4"></a>   
## <a name="net-services-installation-tool"></a>.NET Services Installation-Tool  
 Das [.NET Services Installation-Tool (Regsvcs.exe)](../tools/regsvcs-exe-net-services-installation-tool.md) fügt verwaltete Klassen zu Windows 2000-Komponentendiensten hinzu, kombiniert mehrere Aufgaben innerhalb eines einzigen Tools. Zusätzlich zum Laden und Registrieren der Assembly, generiert, registriert und installiert Regsvcs.exe die Typbibliothek in eine vorhandene COM+ 1.0-Anwendung.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Runtime.InteropServices.TypeLibConverter>  
 <xref:System.Runtime.InteropServices.ITypeLibConverter>  
 [Verfügbarmachen von .NET Framework-Komponenten in COM](exposing-dotnet-components-to-com.md)  
 [Qualifizieren von .NET-Typen für die Interoperation](qualifying-net-types-for-interoperation.md)  
 [Einführung in die Klassenschnittstelle](com-callable-wrapper.md#introducing-the-class-interface)  
 [Überlegungen zur Assemblysicherheit](../app-domains/assembly-security-considerations.md)  
 [Tlbexp.exe (Type Library Exporter-Tool)](../tools/tlbexp-exe-type-library-exporter.md)  
 [Registrieren von Assemblys bei COM](registering-assemblies-with-com.md)  
 [Vorgehensweise: Einbetten von Typbibliotheken als Win32-Ressourcen in Anwendungen](https://msdn.microsoft.com/library/c97b4b8c-2ab7-4ac7-8fc8-0ba5c5d59c44(v=vs.100))
