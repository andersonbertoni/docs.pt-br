---
title: Método ICorProfilerInfo3::EnumJITedFunctions
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.EnumJITedFunctions Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::EnumJITedFunctions
helpviewer_keywords:
- ICorProfilerInfo3::EnumJITedFunctions method [.NET Framework profiling]
- EnumJITedFunctions method [.NET Framework profiling]
ms.assetid: e2847a36-f460-45e2-9b6c-b33b008f40d9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c1b088d138948ed7e9ae5514fb62e37c324427dd
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782187"
---
# <a name="icorprofilerinfo3enumjitedfunctions-method"></a>Método ICorProfilerInfo3::EnumJITedFunctions
Retorna um enumerador para todas as funções que foram previamente compilado por JIT.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumJITedFunctions([out] ICorProfilerFunctionEnum** ppEnum);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `ppEnum`  
 [out] Um ponteiro para o [ICorProfilerFunctionEnum](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctionenum-interface.md) enumerador.  
  
## <a name="remarks"></a>Comentários  
 Esse método pode se sobrepor `JITCompilation` retornos de chamada, como o [ICorProfilerCallback:: Jitcompilationstarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md) método. O enumerador retornado por esse método não inclui funções que são carregadas de imagens nativas geradas com Ngen.exe.  
  
> [!NOTE]
>  Enumeração retornada inclui apenas "0" para o valor da `COR_PRF_FUNCTION::reJitId` campo.  Se você precisar válida `COR_PRF_FUNCTION::reJitId` valores, use o [ICorProfilerInfo4::EnumJITedFunctions2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-enumjitedfunctions2-method.md) método.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo3](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)
- [Interfaces de criação de perfil](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [Criação de perfil](../../../../docs/framework/unmanaged-api/profiling/index.md)
