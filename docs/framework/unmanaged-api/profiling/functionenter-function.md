---
title: Função FunctionEnter
ms.date: 03/30/2017
api_name:
- FunctionEnter
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionEnter
helpviewer_keywords:
- FunctionEnter function [.NET Framework profiling]
ms.assetid: bf4ffa50-4506-4dd4-aa13-a0457b47ca74
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9279e50630ea074b70955ca8ed218cd39a613b58
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781299"
---
# <a name="functionenter-function"></a>Função FunctionEnter
Notifica o criador de perfil que o controle está sendo passado para uma função.  
  
> [!NOTE]
>  O `FunctionEnter` função foi preterida no .NET Framework versão 2.0, e seu uso provocará uma penalidade de desempenho. Use o [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md) function em vez disso.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
void __stdcall FunctionEnter (  
    [in]  FunctionID funcID  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `funcID`  
 [in] O identificador da função à qual o controle é passado.  
  
## <a name="remarks"></a>Comentários  
 O `FunctionEnter` função é um retorno de chamada; você deve implementá-la. A implementação deve usar o `__declspec`(`naked`) atributo de classe de armazenamento.  
  
 O mecanismo de execução não salva qualquer registros antes de chamar essa função.  
  
- Na entrada, você deve salvar todos os registros que você usa, incluindo aqueles na unidade de ponto flutuante (FPU).  
  
- Na saída, você deve restaurar a pilha de popping desativar todos os parâmetros que foram enviados por push ao seu chamador.  
  
 A implementação de `FunctionEnter` não devem bloquear porque isso atrasará a coleta de lixo. A implementação não deve tentar uma coleta de lixo, porque a pilha não pode estar em um estado de amigável para coleta de lixo. Se você tentar uma coleta de lixo, o tempo de execução será bloqueado até que `FunctionEnter` retorna.  
  
 Além disso, o `FunctionEnter` função não deve chamar código gerenciado ou em qualquer causa de maneira uma alocação de memória gerenciada.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf.idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET framework:** 1.1, 1.0  
  
## <a name="see-also"></a>Consulte também

- [Função FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)
- [Função FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)
- [Função FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)
- [Método SetEnterLeaveFunctionHooks2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [Criando perfil de funções estáticas globais](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
