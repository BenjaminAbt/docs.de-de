---
title: Garbage Collection | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- memory, garbage collection
- garbage collection, automatic memory management
- GC [.NET Framework]
- memory, allocating
- common language runtime, garbage collection
- garbage collector
- cleanup operations
- garbage collection
- memory, releasing
- common language runtime, automatic memory management
- automatic memory management
- runtime, automatic memory management
- runtime, garbage collection
- garbage collection, about
ms.assetid: 22b6cb97-0c80-4eeb-a2cf-5ed7655e37f9
caps.latest.revision: 36
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: e6c68eb589ce80fa6154c77840c8d4fdee4d8a81
ms.openlocfilehash: b48c375c86b435e880e9ad9650941ab0f2329c3a
ms.lasthandoff: 04/11/2017

---
# <a name="garbage-collection"></a>Garbage Collection
Der Garbage Collector von .NET verwaltet die Belegung und Freigabe von Arbeitsspeicher für die Anwendung. Bei jedem Erstellen eines neuen Objekts belegt die Common Language Runtime (CLR) Speicher für das Objekt aus dem verwalteten Heap. Solange ein Adressbereich im verwalteten Heap verfügbar ist, reserviert die Laufzeit Arbeitsspeicher für neue Objekte. Arbeitsspeicher ist jedoch nicht unendlich verfügbar. Möglicherweise muss mithilfe der Garbage Collection Arbeitsspeicher freigegeben werden. Das Optimierungsmodul der Garbage Collection bestimmt den besten Zeitpunkt für das Einsammeln anhand der erfolgten Speicherbelegungen. Beim Einsammeln durch die Garbage Collection wird nach Objekten im verwalteten Heap gesucht, die nicht mehr von der Anwendung verwendet werden. Anschließend werden die für das Freigeben des Arbeitsspeichers erforderlichen Operationen ausgeführt.  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Verwandte Themen  
  
|Titel|Beschreibung|  
|-----------|-----------------|  
|[Grundlagen der Garbage Collection](../../../docs/standard/garbage-collection/fundamentals.md)|Beschreibt, wie die Garbage Collection funktioniert, wie Objekte auf dem verwalteten Heap zugeordnet werden und erläutert andere Kernkonzepte.|  
|[Garbage Collection und Leistung](../../../docs/standard/garbage-collection/performance.md)|Beschreibt die Leistungsprüfungen, die Sie verwenden können, um Probleme mit der Garbage Collection oder der Leistung zu analysieren.|  
|[Induzierte Sammlungen](../../../docs/standard/garbage-collection/induced.md)|Beschreibt, wie eine Garbage Collection initiiert wird.|  
|[Latenzmodi](../../../docs/standard/garbage-collection/latency.md)|Beschreibt die Modi, die das Ausmaß der Garbage Collection bestimmen.|  
|[Optimierung für freigegebenes Webhosting](../../../docs/standard/garbage-collection/optimization-for-shared-web-hosting.md)|Beschreibt, wie die Garbage Collection auf Servern, die von mehreren kleinen Websites gemeinsam verwendet werden, optimiert werden kann.|  
|[Garbage Collection-Benachrichtigungen](../../../docs/standard/garbage-collection/notifications.md)|Beschreibt, wie festgestellt werden kann, wann eine vollständige Garbage Collection ansteht und wann sie abgeschlossen ist.|  
|[Überwachung von Anwendungsdomänenressourcen](../../../docs/standard/garbage-collection/app-domain-resource-monitoring.md)|Beschreibt, wie die durch eine Anwendungsdomäne verursachte CPU- und Speicherauslastung überwacht wird.|  
|[Schwache Verweise](../../../docs/standard/garbage-collection/weak-references.md)|Beschreibt Funktionen, die dem Garbage Collector ermöglichen, ein Objekt zu sammeln, während die Anwendung nach wie vor auf das Objekt zugreifen kann.|  
  
## <a name="reference"></a>Verweis  
 <xref:System.GC?displayProperty=fullName>  
  
 <xref:System.GCCollectionMode?displayProperty=fullName>  
  
 <xref:System.GCNotificationStatus?displayProperty=fullName>  
  
 <xref:System.Runtime.GCLatencyMode?displayProperty=fullName>  
  
 <xref:System.Runtime.GCSettings?displayProperty=fullName>  
  
 <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=fullName>  
  
 <xref:System.Object.Finalize%2A?displayProperty=fullName>  
  
 <xref:System.IDisposable?displayProperty=fullName>  
  
## <a name="see-also"></a>Siehe auch  
 [Bereinigen von nicht verwalteten Ressourcen](../../../docs/standard/garbage-collection/unmanaged.md)
