---
title: Método ICLRRuntimeInfo::BindAsLegacyV2Runtime
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.BindAsLegacyV2Runtime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::BindAsLegacyV2Runtime
helpviewer_keywords:
- ICLRRuntimeInfo::BindAsLegacyV2Runtime method [.NET Framework hosting]
- BindAsLegacyV2Runtime method [.NET Framework hosting]
ms.assetid: 65fd55ac-4a24-4479-9384-a2e8013bfb2b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a0ea4bd222500015f6c78cb0455539aa2c24e681
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67765619"
---
# <a name="iclrruntimeinfobindaslegacyv2runtime-method"></a>Método ICLRRuntimeInfo::BindAsLegacyV2Runtime
Associa o tempo de execução atual para todos os herdados common language runtime (CLR) versão 2 ativação decisões de política.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT BindAsLegacyV2Runtime ();  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Esse método retorna os HRESULTs específicos a seguir:  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|Ou a associação foi bem-sucedida ou esse tempo de execução já foram associado como execução de política 2 de ativação de versão herdado CLR.|  
|CLR_E_SHIM_LEGACYRUNTIMEALREADYBOUND|Um tempo de execução diferente já foi associado à política de 2 de ativação de versão do CLR herdada.|  
  
## <a name="remarks"></a>Comentários  
 Se o tempo de execução atual já está associado para todos os herdados CLR versão 2 ativação política decisões (por exemplo, usando o `useLegacyV2RuntimeActivationPolicy` atributo o [ \<inicialização > elemento](../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md) no arquivo de configuração), esse método não retorna um resultado de erro; em vez disso, o resultado é S_OK, assim como seria se o método tinha associada com êxito a política de ativação herdados.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost.h  
  
 **Biblioteca:** Incluído como um recurso em mscoree. dll  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)
- [Hospedagem de Interfaces](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [Hospedagem](../../../../docs/framework/unmanaged-api/hosting/index.md)
- [Elemento \<startup>](../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)
