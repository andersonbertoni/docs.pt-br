---
title: Método ICLRAppDomainResourceMonitor::GetCurrentCpuTime
ms.date: 03/30/2017
api_name:
- ICLRAppDomainResourceMonitor.GetCurrentCpuTime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentCpuTime
helpviewer_keywords:
- ICLRAppDomainResourceMonitor::GetCurrentCpuTime method [.NET Framework hosting]
- GetCurrentCpuTime method [.NET Framework hosting]
ms.assetid: ebc9cc33-fcd6-4cae-9ecb-ea21c51874e6
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4d5149c7e3430c5e7c59a47c4ab5dc98d878de39
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67766671"
---
# <a name="iclrappdomainresourcemonitorgetcurrentcputime-method"></a>Método ICLRAppDomainResourceMonitor::GetCurrentCpuTime
Obtém o tempo total do processador que foi usado por todos os threads durante a execução no domínio do aplicativo atual, desde que o domínio do aplicativo foi criado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCurrentCpuTime([in]  DWORD dwAppDomainId,  
                          [out] ULONGLONG* pMilliseconds);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `dwAppDomainId`  
 [in] A ID do domínio do aplicativo solicitado.  
  
 `pMilliseconds`  
 [out] Um ponteiro para o tempo total do processador que foi usado por todos os threads durante a execução no domínio do aplicativo atual desde que o domínio do aplicativo foi criado. Esse parâmetro pode ser `null`.  
  
## <a name="return-value"></a>Valor de retorno  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|COR_E_APPDOMAINUNLOADED|O domínio do aplicativo foi descarregado ou não existe.|  
|E_FAIL|Monitoramento de recursos de domínio do aplicativo não está habilitado.<br /><br /> - ou -<br /><br /> Todas as outras falhas.|  
  
## <a name="remarks"></a>Comentários  
 Esse método é não gerenciado equivalente gerenciado <xref:System.AppDomain.MonitoringTotalProcessorTime%2A?displayProperty=nameWithType> propriedade.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost.h  
  
 **Biblioteca:** Incluído como um recurso em mscoree. dll  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRAppDomainResourceMonitor](../../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md)
- [Hospedagem de Interfaces](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [Monitoramento de recursos de domínio do aplicativo](../../../../docs/standard/garbage-collection/app-domain-resource-monitoring.md)
- [Hospedagem](../../../../docs/framework/unmanaged-api/hosting/index.md)
