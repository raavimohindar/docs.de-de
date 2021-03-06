---
ms.openlocfilehash: eef5633ec8566f6d5216b7dca4387766cacb600d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620383"
---
### <a name="netdatacontractserializer-fails-to-deserialize-a-concurrentdictionary-serialized-with-a-different-net-version"></a>„NetDataContractSerializer“ kann eine ConcurrentDictionary-Klasse nicht deserialisieren, die mit einer anderen Version von .NET serialisiert wurde

#### <a name="details"></a>Details

Programmbedingt kann <xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=fullName> daher nur verwendet werden, wenn sowohl der Endpunkt für die Serialisierung als auch der Endpunkt für die Deserialisierung den gleichen CLR-Typ aufweisen. Deshalb kann nicht gewährleistet werden, dass ein Objekt, das mit einer Version von .NET Framework serialisiert wurde, mit einer anderen Version deserialisiert werden kann. <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> ist ein Typ, bei dem bekannt ist, dass die Deserialisierung nicht korrekt durchgeführt wird, wenn dieser mit .NET Framework 4.5 oder früher serialisiert wurde und mit .NET Framework 4.5.1 oder höher deserialisiert wird.

#### <a name="suggestion"></a>Vorschlag

Es gibt einige Möglichkeiten, dieses Problem zu umgehen:<ul><li>Führen Sie ein Upgrade durch, sodass der serialisierende Computer ebenfalls .NET Framework 4.5.1 verwendet.</li><li>Verwenden Sie <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> statt <xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=fullName>, da dadurch nicht genau die gleichen CLR-Typen bei den Endpunkten für die Serialisierung und Deserialisierung erwartet werden.</li><li>Verwenden Sie <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> statt <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>, da dieses Element nicht die Unterbrechung zwischen 4.5 und 4.5.1 aufweist.</li></ul>

| name    | Wert       |
|:--------|:------------|
| Bereich   |Gering|
|Version|4.5.1|
|Typ|Laufzeit

#### <a name="affected-apis"></a>Betroffene APIs

-<xref:System.Runtime.Serialization.NetDataContractSerializer.Deserialize(System.IO.Stream)?displayProperty=nameWithType></li></ul>|
