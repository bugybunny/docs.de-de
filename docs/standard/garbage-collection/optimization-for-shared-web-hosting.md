---
title: Optimierung für freigegebenes Webhosting
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- garbage collection, Web hosting
- garbage collection, optimizing
- garbage collection, shared Web hosting
ms.assetid: be98c0ab-7ef8-409f-8a0d-cb6e5b75ff20
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7831e383a3048523909b79ac5a4706f3c1c48371
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2018
ms.locfileid: "47216132"
---
# <a name="optimization-for-shared-web-hosting"></a>Optimierung für freigegebenes Webhosting
Wenn Sie Administrator eines Servers sind, der zum Hosten von mehreren kleinen Websites freigegeben ist, können Sie die Leistung optimieren und die Websitekapazität erhöhen, indem Sie die folgende `gcTrimCommitOnLowMemory`-Einstellung für den `runtime`-Knoten in der Datei „aspnet.config“ im .NET-Verzeichnis festlegen:  
  
 `<gcTrimCommitOnLowMemory enabled="true|false"/>`  
  
> [!NOTE]
>  Diese Einstellung wird nur für freigegebene Webhostingszenarien empfohlen.  
  
 Da der Garbage Collector den Speicher für zukünftige Belegungen beibehält, kann sein belegter Speicher größer sein als der unbedingt erforderliche Speicher. Sie können diesen Speicher im Hinblick auf Zeiten reduzieren, in denen eine hohe Auslastung des Systemspeichers vorherrscht. Durch eine Reduzierung des belegten Speichers wird die Leistung verbessert und die Kapazität zum Hosten mehrerer Websites erweitert.  
  
 Wenn die Einstellung `gcTrimCommitOnLowMemory` aktiviert ist, wertet der Garbage Collector die Speichersystemlast aus und wechselt in einen eingeschränkten Modus, wenn die Last 90 % erreicht. Dabei bleibt der eingeschränkte Modus bestehen, bis die Last unter 85 % fällt.  
  
 Wenn die Umstände es erlauben, kann der Garbage Collector veranlassen, dass die `gcTrimCommitOnLowMemory`-Einstellung nicht die aktuelle Anwendung unterstützt und diese ignoriert.  
  
## <a name="example"></a>Beispiel  
 Das folgende XML-Fragment zeigt, wie die `gcTrimCommitOnLowMemory`-Einstellung aktiviert wird. Ellipsen weisen auf andere Einstellungen hin, die im `runtime`-Knoten festgelegt wären.  
  
```xml  
<?xml version="1.0" encoding="UTF-8"?>  
<configuration>  
    <runtime>  
    . . .  
    <gcTrimCommitOnLowMemory enabled="true"/>  
    </runtime>  
    . . .  
</configuration>  
```  
  
## <a name="see-also"></a>Siehe auch

- [Garbage Collection](../../../docs/standard/garbage-collection/index.md)
