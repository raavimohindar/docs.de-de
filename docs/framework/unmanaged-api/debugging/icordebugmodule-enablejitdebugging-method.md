---
title: ICorDebugModule::EnableJITDebugging-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugModule.EnableJITDebugging
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::EnableJITDebugging
helpviewer_keywords:
- ICorDebugModule::EnableJITDebugging method [.NET Framework debugging]
- EnableJITDebugging method [.NET Framework debugging]
ms.assetid: 0a65e2a4-5bb6-496c-ae6f-40474426b5a6
topic_type:
- apiref
ms.openlocfilehash: bdf027f94c8416d052cb807d04be76a39868ccf7
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212931"
---
# <a name="icordebugmoduleenablejitdebugging-method"></a>ICorDebugModule::EnableJITDebugging-Methode
Steuert, ob der JIT-Compiler (Just-in-Time) Debuginformationen für Methoden in diesem Modul beibehält.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT EnableJITDebugging(  
    [in] BOOL bTrackJITInfo,  
    [in] BOOL bAllowJitOpts  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `bTrackJITInfo`  
 in Legen Sie diesen Wert auf fest, `true` um dem JIT-Compiler das Beibehalten von Zuordnungsinformationen zwischen der MSIL-Version (Microsoft Intermediate Language) und der JIT-kompilierten Version der einzelnen Methoden in diesem Modul zu ermöglichen.  
  
 `bAllowJitOpts`  
 in Legen Sie diesen Wert auf fest, `true` um dem JIT-Compiler das Generieren von Code mit bestimmten JIT-spezifischen Optimierungen für das Debuggen zu ermöglichen.  
  
## <a name="remarks"></a>Hinweise  
 Das JIT-Debuggen ist standardmäßig für alle Module aktiviert, die geladen werden, wenn der Debugger aktiv ist. Die programmgesteuerte Aktivierung oder Deaktivierung der Einstellungen überschreibt globale Einstellungen.  
  
## <a name="requirements"></a>Requirements (Anforderungen)  
 **Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
