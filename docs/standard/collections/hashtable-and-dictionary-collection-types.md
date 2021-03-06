---
title: Hashtable-Sammlungstyp und Dictionary-Sammlungstyp | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Hashtable class, grouping data in collections
- Hashtable collection type
- hash tables
- grouping data in collections, Hashtable collection type
- hash function
- collections [.NET Framework], Hashtable collection type
ms.assetid: bfc20837-3d02-4fc7-8a8f-c5215b6b7913
caps.latest.revision: 16
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 59aa4bd6160491ac6c6a4f45131531226ec7e58f
ms.lasthandoff: 04/18/2017

---
# <a name="hashtable-and-dictionary-collection-types"></a>Hashtable-Sammlungstyp und Dictionary-Sammlungstyp
Die Klasse <xref:System.Collections.Hashtable?displayProperty=fullName> und die generischen Klassen <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> und <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> implementieren die <xref:System.Collections.IDictionary?displayProperty=fullName>-Schnittstelle. Die generische Klasse <xref:System.Collections.Generic.Dictionary%602> implementiert darüber hinaus auch die generische Schnittstelle <xref:System.Collections.Generic.IDictionary%602>. Daher ist jedes Element in diesen Auflistungen ein Schlüssel-Wert-Paar.  
  
 Ein <xref:System.Collections.Hashtable>-Objekt besteht aus Buckets, die die Elemente der Auflistung enthalten. Ein Bucket ist eine virtuelle Untergruppe von Elementen innerhalb der <xref:System.Collections.Hashtable>, die das Suchen und Abrufen schneller und einfacher als in den meisten Auflistungen ermöglicht. Jedem Bucket ist ein Hashcode zugeordnet, der mithilfe einer Hashfunktion generiert wird und auf dem Schlüssel des Elements basiert.  
  
 Die generische Klasse <xref:System.Collections.Generic.HashSet%601> ist eine ungeordnete Auflistung für eindeutige Elemente.  
  
 Eine Hashfunktion ist ein Algorithmus, der einen numerischen Hashcode anhand eines Schlüssels zurückgibt. Der Schlüssel ist der Wert einer Eigenschaft des Objekts, das gespeichert wird. Eine Hashfunktion muss immer denselben Hashcode für denselben Schlüssel zurückgeben. Es ist möglich, dass eine Hashfunktion, den gleichen Hashcode für zwei verschiedene Schlüssel generiert. Eine Hashfunktion, die einen eindeutigen Hashcode für jeden eindeutigen Schlüssel generiert, führt jedoch zu besserer Leistung beim Abrufen von Elementen aus der Hashtabelle.  
  
 Jedes Objekt, das als ein Element in einer <xref:System.Collections.Hashtable> verwendet wird, muss in der Lage sein, einen Hashcode für sich selbst zu generieren, indem eine Implementierung der Methode <xref:System.Object.GetHashCode%2A> verwendet wird. Jedoch können Sie auch eine Hashfunktion für alle Elemente in einer <xref:System.Collections.Hashtable> mithilfe eines <xref:System.Collections.Hashtable>-Konstruktors angeben, der eine <xref:System.Collections.IHashCodeProvider>-Implementierung als einen seiner Parameter akzeptiert.  
  
 Wenn ein Objekt einer <xref:System.Collections.Hashtable> hinzugefügt wird, wird es in dem Bucket gespeichert, der dem Hashcode zugeordnet ist, der mit dem Hashcode des Objekts übereinstimmt. Wenn in der <xref:System.Collections.Hashtable> nach einem Wert gesucht wird, wird der Hashcode für diesen Wert generiert, dann wird der diesem Hashcode zugeordnete Bucket durchsucht.  
  
 Eine Hashfunktion für eine Zeichenfolge kann z. B. die ASCII-Codes jedes Zeichens in der Zeichenfolge annehmen und sie dann zusammen hinzufügen, um einen Hashcode zu generieren. Die Zeichenfolge "Segel" besitzt z. B. einen anderen Hashcode als die Zeichenfolge "Seife". Daher werden die Zeichenfolgen "Segel" und "Seife" in verschiedenen Buckets gespeichert. Im Gegensatz dazu weisen "nie" und "ein" den gleichen Hashcode auf und befinden sich im gleichen Bucket.  
  
 Die Klassen <xref:System.Collections.Generic.Dictionary%602> und <xref:System.Collections.Concurrent.ConcurrentDictionary%602> weisen die gleiche Funktionalität wie die Klasse <xref:System.Collections.Hashtable> auf. Ein <xref:System.Collections.Generic.Dictionary%602> eines bestimmten Typs (mit Ausnahme von <xref:System.Object>) bietet für Werttypen bessere Leistung als eine <xref:System.Collections.Hashtable>. Der Grund hierfür ist, dass die Elemente von <xref:System.Collections.Hashtable> vom Typ <xref:System.Object> sind. Daher treten das Boxing und das Unboxing in der Regel beim Speichern oder Abrufen eines Werttyps auf. Die <xref:System.Collections.Concurrent.ConcurrentDictionary%602>-Klasse sollte verwendet werden, wenn möglicherweise von mehreren Threads zugleich auf die Sammlung zugegriffen wird.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Collections.Hashtable>   
 <xref:System.Collections.IDictionary>   
 <xref:System.Collections.IHashCodeProvider>   
 <xref:System.Collections.Generic.Dictionary%602>   
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>   
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>   
 [Häufig verwendete Auflistungstypen](../../../docs/standard/collections/commonly-used-collection-types.md)
