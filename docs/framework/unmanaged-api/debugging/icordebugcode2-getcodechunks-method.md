---
title: ICorDebugCode2::GetCodeChunks-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugCode2.GetCodeChunks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode2::GetCodeChunks
helpviewer_keywords:
- GetCodeChunks method [.NET Framework debugging]
- ICorDebugCode2::GetCodeChunks method [.NET Framework debugging]
ms.assetid: 210a2f02-2678-4555-bc4a-78a0408764c8
topic_type:
- apiref
ms.openlocfilehash: e419ebb6ffd404368baf32e591e08c4a70645127
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73121119"
---
# <a name="icordebugcode2getcodechunks-method"></a>ICorDebugCode2::GetCodeChunks-Methode

Ruft die Codeabschnitte ab, aus denen dieses Codeobjekt besteht.

## <a name="syntax"></a>Syntax

```cpp
HRESULT GetCodeChunks (
    [in]  ULONG32     cbufSize,
    [out] ULONG32     *pcnumChunks,
    [out, size_is(cbufSize), length_is(*pcnumChunks)]
        CodeChunkInfo chunks[]
);
```

## <a name="parameters"></a>Parameter

`cbufSize`  
in Größe des `chunks` Arrays.

`pcnumChunks`  
vorgenommen Die Anzahl der Blöcke, die im `chunks` Array zurückgegeben werden.

`chunks`  
vorgenommen Ein Array von CodeChunkInfo-Strukturen, von denen jedes einen einzelnen Codeblock darstellt. Wenn der Wert von `cbufSize` 0 (null) ist, kann dieser Parameter NULL sein.

## <a name="remarks"></a>Hinweise

Die Code Blöcke werden nie überlappen, und Sie folgen der Reihenfolge, in der Sie von [ICorDebugCode:: GetCode](icordebugcode-getcode-method.md)verkettet worden wären. Ein MSIL-Code Objekt (Microsoft Intermediate Language) in der .NET Framework Version 2,0 besteht aus einem einzelnen Codeblock.

## <a name="requirements"></a>Anforderungen

**Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../get-started/system-requirements.md).

**Header:** CorDebug.idl, CorDebug.h

**Bibliothek:** CorGuids.lib

**.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
