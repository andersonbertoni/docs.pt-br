---
title: Método ImportFileEx2
ms.date: 03/30/2017
api_name:
- IALink2.ImportFileEx2
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ImportFileEx2
helpviewer_keywords:
- ImportFileEx2 method
ms.assetid: 02c789fd-16fc-48c6-9619-56e87e2a37ca
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e6584d31674670bcd005161a846b74df71a27a5f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67741640"
---
# <a name="importfileex2-method"></a>Método ImportFileEx2
Importa os assemblies e módulos não associados. Esse método é como [método ImportFile](../../../../docs/framework/unmanaged-api/alink/importfile-method.md), mas funciona mesmo se o arquivo que está sendo importado não existe no disco.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ImportFileEx2(  
    LPCWSTR pszFilename,  
    LPCWSTR pszTargetName,  
    IMetaDataAssemblyImport* pAssemblyScopeIn,  
    BOOL fSmartImport,  
    DWORD dwOpenFlags,  
    mdToken* pImportToken,  
    IMetaDataAssemblyImport** ppAssemblyScope,  
    DWORD* pdwCountOfScopes  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  
 `pszFilename`  
 Nome do arquivo a ser importado.  
  
 `pszTargetName`  
 Nome opcional do arquivo de destino.  
  
 `pAssemblyScopeIn`  
 Escopo de importação opcional [IMetaDataAssemblyImport Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md) interface.  
  
 `fSmartImport`  
 Se for TRUE, ImportTypes é usado, caso contrário, a importação deve ser executada manualmente.  
  
 `dwOpenFlags`  
 Sinalizadores a serem passados para [método OpenScope](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-openscope-method.md).  
  
 `pImportToken`  
 Recebe a ID exclusiva para o arquivo ou assembly.  
  
 `ppAssemblyScope`  
 Recebe o escopo de importação de assembly [IMetaDataAssemblyImport Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md) interface. Pode ser NULL se o arquivo não é um assembly.  
  
 `pdwCountOfScopes`  
 Recebe o número de arquivos e/ou importados de escopos.  
  
## <a name="return-value"></a>Valor de retorno  
 Se o método for bem-sucedido, retornará S_OK.  
  
## <a name="requirements"></a>Requisitos  
 Requer alink.h.  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink2](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [Interface IALink](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [API do ALink](../../../../docs/framework/unmanaged-api/alink/index.md)
