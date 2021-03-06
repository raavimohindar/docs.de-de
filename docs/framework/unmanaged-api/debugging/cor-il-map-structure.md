---
title: COR_IL_MAP-Struktur
ms.date: 03/30/2017
api_name:
- COR_IL_MAP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_IL_MAP
helpviewer_keywords:
- COR_IL_MAP structure [.NET Framework debugging]
ms.assetid: 534ebc17-963d-4b26-8375-8cd940281db3
topic_type:
- apiref
ms.openlocfilehash: 4c79d0e4e37f3f884651e49c8fff6db72fac4f50
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179290"
---
# <a name="cor_il_map-structure"></a>COR_IL_MAP-Struktur
Gibt Änderungen im relativen Offset einer Funktion an.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef struct _COR_IL_MAP {  
    ULONG32 oldOffset;
    ULONG32 newOffset;
    BOOL    fAccurate;  
} COR_IL_MAP;  
```  
  
## <a name="members"></a>Members  
  
|Member|Beschreibung|  
|------------|-----------------|  
|`oldOffset`|Der alte Microsoft-Zwischensprache (MSIL)-Offset relativ zum Anfang der Funktion.|  
|`newOffset`|Der neue MSIL-Offset relativ zum Anfang der Funktion.|  
|`fAccurate`|`true`wenn die Zuordnung als korrekt bekannt ist; andernfalls `false`.|  
  
## <a name="remarks"></a>Bemerkungen  
 Das Format der Karte ist wie folgt: `oldOffset` Der Debugger geht davon aus, dass sich der MSIL-Offset innerhalb des ursprünglichen, unveränderten MSIL-Codes bezieht. Der `newOffset` Parameter bezieht sich auf den entsprechenden MSIL-Offset innerhalb des neuen, instrumentierten Codes.  
  
 Damit das Schrittwerk ordnungsgemäß funktioniert, sollten die folgenden Anforderungen erfüllt sein:  
  
- Die Karte sollte in aufsteigender Reihenfolge sortiert werden.  
  
- Instrumentierter MSIL-Code sollte nicht neu angeordnet werden.  
  
- Der ursprüngliche MSIL-Code sollte nicht entfernt werden.  
  
- Die Karte sollte Einträge enthalten, um alle Sequenzpunkte aus der Programmdatenbankdatei (PDB) zuzuordnen.  
  
 Die Karte interpoliert keine fehlenden Einträge. Das folgende Beispiel zeigt eine Karte und ihre Ergebnisse.  
  
 Karte:  
  
- 0 alter Offset, 0 neuer Offset  
  
- 5 alter Offset, 10 neuer Offset  
  
- 9 alter Offset, 20 neuer Offset  
  
 Ergebnisse:  
  
- Ein alter Offset von 0, 1, 2, 3 oder 4 wird einem neuen Offset von 0 zugeordnet.  
  
- Ein alter Offset von 5, 6, 7 oder 8 wird dem neuen Offset 10 zugeordnet.  
  
- Ein alter Offset von 9 oder höher wird dem neuen Offset 20 zugeordnet.  
  
- Ein neuer Offset von 0, 1, 2, 3, 4, 5, 6, 7, 8 oder 9 wird dem alten Offset 0 zugeordnet.  
  
- Ein neuer Offset von 10, 11, 12, 13, 14, 15, 16, 17, 18 oder 19 wird dem alten Offset 5 zugeordnet.  
  
- Ein neuer Offset von 20 oder höher wird dem alten Offset 9 zugeordnet.  
  
## <a name="requirements"></a>Requirements (Anforderungen)  
 **Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../get-started/system-requirements.md).  
  
 **Kopfzeile:** CorDebug.idl, CorProf.idl  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen

- [Debuggen von Strukturen](debugging-structures.md)
- [Debuggen](index.md)
