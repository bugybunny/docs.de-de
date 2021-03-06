---
title: Application Insights – serverlose apps
description: Application Insights ist eine serverlose Diagnose-Plattform, mit der Entwickler zu erkennen, selektieren und Diagnostizieren von Problemen in Web-apps, mobile apps, desktop-apps und Microservices.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 57b1f70825251c48f720dcd78d094f5e8fb1edb8
ms.sourcegitcommit: 4c158beee818c408d45a9609bfc06f209a523e22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2018
ms.locfileid: "49369944"
---
# <a name="telemetry-with-application-insights"></a>Telemetrie mit Application Insights

[Application Insights](https://docs.microsoft.com/azure/application-insights) ist eine Plattform für die serverlose Diagnose, mit der Entwickler zu erkennen, selektieren und Diagnostizieren von Problemen in Web-apps, mobilen apps, desktop-apps und Microservices. Sie können für Funktionen-apps in Application Insights aktivieren, indem Sie einfach das Umlegen eines Schalters im Portal. Application Insights bietet alle Funktionen, ohne dass Sie einen Server konfigurieren, oder richten Sie Ihre eigene Datenbank. Alle Application Insights-Funktionen werden als Dienst bereitgestellt, die automatisch mit Ihren apps integriert ist.

![Application Insights-logo](./media/application-insights-logo.png)

Hinzufügen von Application Insights auf vorhandene apps ist so einfach wie das Hinzufügen eines instrumentierungsschlüssels von, um die Einstellungen Ihrer Anwendung. Mit Application Insights können Sie folgende Aktionen ausführen:

* Erstellen Sie benutzerdefinierte Diagramme und Warnungen basierend auf Metriken wie die Anzahl der Aufrufe, die Zeit zum Ausführen einer Funktion und Ausnahmen
* Analysieren von Fehlern und Serverausnahmen
* Drilldown in die Leistung von Vorgang aus, und messen die Zeit, die es dauert, rufen Sie die Drittanbieter-Abhängigkeiten
* Überwachen der CPU-Auslastung, Arbeitsspeicher und Gebühren auf allen Servern, die Ihre Funktionen-apps hosten
* Zeigen Sie einen Livestream der Metriken anzeigen, einschließlich der Anzahl der Anforderungen und der Latenz für Ihre Funktions-apps
* Verwendung [Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics) zum Durchsuchen, Abfragen und erstellen Sie benutzerdefinierte Diagramme für Ihre Funktionsdaten

![Metrik-explorer](./media/metrics-explorer.png)

Zusätzlich zur integrierten Telemetriedaten ist es auch möglich, benutzerdefinierte Telemetriedaten zu generieren. Der folgende Codeausschnitt erstellt einen benutzerdefinierte Telemetrie-Client mit dem instrumentationsschlüssel, der für die Funktions-app festgelegt:

```csharp
public static TelemetryClient telemetry = new TelemetryClient()
{
    InstrumentationKey = Environment.GetEnvironmentVariable("APPINSIGHTS_INSTRUMENTATIONKEY")
};
```

Der folgende Code wird gemessen, wie lange es dauert, fügen Sie eine neue Zeile in einer [Azure Table Storage](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview) Instanz:

```csharp
var operation = TableOperation.Insert(entry);
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
await table.ExecuteAsync(operation);
telemetry.TrackDependency("AzureTableStorageInsert", "Insert", startTime, timer.Elapsed, true);
```

Das resultierende Leistungsdiagramm wird angezeigt:

![Benutzerdefinierte Telemetrie](./media/custom-telemetry.png)

Die benutzerdefinierte Telemetrie zeigt an, dass die durchschnittliche Zeit zum Einfügen einer neuen Zeile 32.6 Millisekunden ist.

Application Insights bietet eine leistungsfähige und bequeme Möglichkeit, detaillierte Telemetriedaten über Ihre serverlosen Anwendungen anzumelden. Haben vollständige Kontrolle über die Stufe der Ablaufverfolgung und Protokollierung, bereitgestellt wird. Sie können benutzerdefinierte Statistiken wie Ereignisse, Abhängigkeiten und Seitenansicht nachverfolgen. Aktivieren Sie schließlich die leistungsstarken Analysen Sie Abfragen schreiben, die wichtige Fragen stellen und Diagramme und erweiterte Einblicke zu generieren.

Weitere Informationen finden Sie unter [Überwachen von Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring).

>[!div class="step-by-step"]
[Zurück](azure-functions.md)
[Weiter](logic-apps.md)