---
title: Função StrongNameGetBlobFromImage
ms.date: 03/30/2017
api_name:
- StrongNameGetBlobFromImage
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameGetBlobFromImage
helpviewer_keywords:
- StrongNameGetBlobFromImage function [.NET Framework strong naming]
ms.assetid: 1de658e6-da32-4d01-9097-6f43c92222e1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b076c39ccf40ca5b613cab94ecc75716158d97a9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67780123"
---
# <a name="strongnamegetblobfromimage-function"></a>Função StrongNameGetBlobFromImage
Obtém uma representação binária da imagem do assembly no endereço de memória especificado.  
  
 Essa função foi preterida. Use o [iclrstrongname:: Strongnamegetblobfromimage](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetblobfromimage-method.md) método em vez disso.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
BOOLEAN StrongNameGetBlobFromImage (  
    [in]  BYTE        *pbBase,  
    [in]  DWORD       dwLength,  
    [in]  BYTE        *pbBlob,  
    [in, out] DWORD   *pcbBlob  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `pbBase`  
 [in] O endereço de memória do manifesto do assembly mapeados.  
  
 `dwLength`  
 [in] O tamanho, em bytes, da imagem no `pbBase`.  
  
 `pbBlob`  
 [in] Um buffer que conterá a representação binária da imagem.  
  
 `pcbBlob`  
 [no, out] O solicitada tamanho máximo, em bytes, da `pbBlob`. Após o retorno, o tamanho real, em bytes, do `pbBlob`.  
  
## <a name="return-value"></a>Valor de retorno  
 `true` Após a conclusão bem-sucedida; Caso contrário, `false`.  
  
## <a name="remarks"></a>Comentários  
 Se o `StrongNameGetBlobFromImage` função não for concluída com êxito, chame o [StrongNameErrorInfo](../../../../docs/framework/unmanaged-api/strong-naming/strongnameerrorinfo-function.md) função para recuperar o último erro gerado.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** StrongName.h  
  
 **Biblioteca:** Incluído como um recurso em mscoree. dll  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método StrongNameGetBlobFromImage](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetblobfromimage-method.md)
- [Método StrongNameGetBlob](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetblob-method.md)
- [Interface ICLRStrongName](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
