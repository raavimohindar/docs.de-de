---
title: Gewährleisten der Datenintegrität über Hashcodes
description: Erfahren Sie, wie Sie die Datenintegrität mithilfe von Hashcodes in .net gewährleisten. Ein Hashwert ist ein numerischer Wert einer festen Länge, der die Daten eindeutig identifiziert.
ms.date: 07/14/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generating hash
- verifying hash codes
- cryptography [.NET], hash
- data integrity
- checking hash codes
- encryption [.NET], hash
- hash
ms.assetid: 33660f33-b70f-4dca-8c87-ab35cfc2961a
ms.openlocfilehash: 3205e37f283cb205f5edfc5948a9cb9f7256f752
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87556955"
---
# <a name="ensuring-data-integrity-with-hash-codes"></a>Gewährleisten der Datenintegrität über Hashcodes
Ein Hashwert ist ein numerischer Wert einer festen Länge, der die Daten eindeutig identifiziert. Hashwerte stellen große Mengen von Daten als viel kleinere numerische Werte dar, damit sie mit digitalen Signaturen verwendet werden. Sie können einen Hashwert effizienter signieren als den größeren Wert. Hashwerte sind auch zum Überprüfen der Integrität der Daten nützlich, die über unsichere Kanäle gesendet werden. Der Hashwert der empfangenen Daten kann mit dem Hashwert der Daten verglichen werden, da sie gesendet wurden, um festzustellen, ob die Daten verändert wurden.  
  
In diesem Thema wird beschrieben, wie Hashcodes mit den Klassen im <xref:System.Security.Cryptography>-Namespace generiert und überprüft werden.  
  
## <a name="generating-a-hash"></a>Generieren eines Hashs

 Die verwalteten Hashklassen können entweder ein Bytearray oder ein verwaltetes Streamobjekt hashen. Im folgenden Beispiel wird der SHA1-Hashalgorithmus verwendet, um einen Hashwert für eine Zeichenfolge zu erstellen. Im Beispiel wird die <xref:System.Text.UnicodeEncoding>-Klasse verwendet, um die Zeichenfolge in ein Bytearray zu konvertieren, dem mithilfe der <xref:System.Security.Cryptography.SHA256>-Klasse ein Hash hinzugefügt werden soll. Der Hashwert wird dann in der Konsole angezeigt.  

 [!code-csharp[GeneratingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/generatingahash/cs/program.cs#1)]
 [!code-vb[GeneratingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/generatingahash/vb/program.vb#1)]  
  
 Dieser Code zeigt die folgende Zeichenfolge in der Konsole an:  
  
 `185 203 236 22 3 228 27 130 87 23 244 15 87 88 14 43 37 61 106 224 81 172 224 211 104 85 194 197 194 25 120 217`  
  
## <a name="verifying-a-hash"></a>Überprüfen eines Hashs

 Die Daten können mit einem Hashwert verglichen werden, um die Integrität zu bestimmen. In der Regel werden die Daten zu einem bestimmten Zeitpunkt gehasht, und der Hashwert wird entsprechend geschützt. Zu einem späteren Zeitpunkt werden die Daten erneut gehasht und mit dem geschützten Wert verglichen. Wenn die Hashwerte übereinstimmen, wurden die Daten nicht geändert. Wenn die Werte nicht übereinstimmen, sind die Daten beschädigt wurden. Damit dieses System funktioniert, muss der geschützte Hash verschlüsselt oder vor allen nicht vertrauenswürdigen Parteien geheim gehalten werden.  
  
 Im folgenden Beispiel wird der vorherige Hashwert einer Zeichenfolge mit einem neuen Hashwert verglichen. In diesem Beispiel wird jedes Byte der Hashwerte durchlaufen und verglichen.  
  
 [!code-csharp[VerifyingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/verifyingahash/cs/program.cs#1)]
 [!code-vb[VerifyingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/verifyingahash/vb/program.vb#1)]  
  
 Wenn die beiden Hashwerte übereinstimmen, zeigt dieser Code Folgendes in der Konsole an:  
  
```console  
The hash codes match.  
```  
  
 Wenn sie nicht übereinstimmen, zeigt der Code Folgendes an:  
  
```console  
The hash codes do not match.  
```  
  
## <a name="see-also"></a>Weitere Informationen

- [Kryptografiemodell](cryptography-model.md)
- [Kryptografische Dienste](cryptographic-services.md)
- [Plattformübergreifende Kryptografie](cross-platform-cryptography.md)
- [ASP.net Core Datenschutz](/aspnet/core/security/data-protection/introduction)
