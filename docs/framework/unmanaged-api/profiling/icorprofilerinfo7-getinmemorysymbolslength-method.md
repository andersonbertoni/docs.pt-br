---
title: Método ICorProfilerInfo7::GetInMemorySymbolsLength
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo7.GetInMemorySymbolsLength
api_location:
- mscorwks.dll
- icorprof.idl
api_type:
- COM
ms.assetid: d62c4a4c-8a62-45aa-8f01-a8387cf36159
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 03c70b97e7af9fdc76c579c5940e2436232f6bc2
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67748653"
---
# <a name="icorprofilerinfo7getinmemorysymbolslength-method"></a>Método ICorProfilerInfo7::GetInMemorySymbolsLength
[Com suporte no .NET Framework 4.6.1 e versões posteriores]  
  
 Retorna o comprimento de um fluxo de símbolo na memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetInMemorySymbolsLength(  
        [in] ModuleID moduleId,  
        [out] DWORD* pCountSymbolBytes  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `moduleId`  
 [in] O identificador do módulo que contém o fluxo de memória.  
  
 pCountSymbolBytes  
 [out] Um ponteiro para um `DWORD` valor que, quando o método retorna, contém o comprimento do fluxo em bytes.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna `S_OK` se o comprimento do fluxo de memória pode ser determinado, mesmo se for zero (0).  
  
 O método retornará `CORPROF_E_MODULE_IS_DYNAMIC` se o método foi criado usando <xref:System.Reflection.Emit?displayProperty=nameWithType>.  
  
## <a name="remarks"></a>Comentários  
 Se o módulo tiver símbolos na memória, o comprimento do fluxo é colocado no `pCountSymbolBytes`. Se o módulo não tem símbolos na memória, `*pCountSymbolBytes = 0`.  
  
> [!NOTE]
>  A implementação atual não oferece suporte a Reflection. Emit. Se o módulo foi criado usando Reflection. Emit, o método retorna `CORPROF_E_MODULE_IS_DYNAMIC`.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo7](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md)
