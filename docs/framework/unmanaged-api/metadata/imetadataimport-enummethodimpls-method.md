---
title: Método IMetaDataImport::EnumMethodImpls
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMethodImpls
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMethodImpls
helpviewer_keywords:
- EnumMethodImpls method [.NET Framework metadata]
- IMetaDataImport::EnumMethodImpls method [.NET Framework metadata]
ms.assetid: 4e0f865d-88b5-44bd-be35-492622e5e08e
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b8be30e8c3b6bc7c03ede5f897f176e04153003b
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781975"
---
# <a name="imetadataimportenummethodimpls-method"></a>Método IMetaDataImport::EnumMethodImpls
Enumera MethodBody e MethodDeclaration tokens que representam os métodos do tipo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumMethodImpls (  
   [in, out] HCORENUM    *phEnum,   
   [in]      mdTypeDef   td,   
   [out]     mdToken     rMethodBody[],   
   [out]     mdToken     rMethodDecl[],   
   [in]      ULONG       cMax,   
   [in]      ULONG       *pcTokens  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `phEnum`  
 [no, out] Um ponteiro para o enumerador. Isso deve ser NULL para a primeira chamada desse método.  
  
 `td`  
 [in] Um TypeDef de token para o tipo cujas implementações de método para enumerar.  
  
 `rMethodBody`  
 [out] A matriz para armazenar os tokens de MethodBody.  
  
 `rMethodDecl`  
 [out] A matriz para armazenar os tokens de MethodDeclaration.  
  
 `cMax`  
 [in] O tamanho máximo do `rMethodBody` e `rMethodDecl` matrizes.  
  
 `pcTokens`  
 [in] O número real de métodos retornados na `rMethodBody` e `rMethodDecl`.  
  
## <a name="return-value"></a>Valor de retorno  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|`S_OK`|`EnumMethodImpls` retornado com êxito.|  
|`S_FALSE`|Não há nenhum token de método para enumerar. Nesse caso, `pcTokens` é zero.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor.h  
  
 **Biblioteca:** Incluído como um recurso em mscoree. dll  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [Interface IMetaDataImport2](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
