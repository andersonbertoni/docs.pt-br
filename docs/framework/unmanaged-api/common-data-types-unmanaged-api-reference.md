---
title: Tipos de dados comuns (referência API não gerenciada)
ms.date: 03/30/2017
ms.assetid: e4ab2c4c-9433-4eba-9e9a-096de406cafb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b56840ce68caa3eed50773668c64e2622a646ddf
ms.sourcegitcommit: 46c68557bf6395f0ab9915f7558f2faae0097695
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892084"
---
# <a name="common-data-types-unmanaged-api-reference"></a>Tipos de dados comuns (referência API não gerenciada)
Este tópico lista tipos de dados simples usados pelas APIs não gerenciadas para o .NET Framework que são definidas por instruções `typedef` do C/C++. Esses tipos de dados são geralmente aliases para tipos de dados primitivos do C/C++. Geralmente, os valores desses tipos de dados são opacos, ou seja, eles são retornados por uma função ou um método específico para que possam ser transmitidos para outras funções ou métodos sem modificação.  
  
|Tipo de dados|Definição|Definido em|Descrição|  
|---------------|----------------|----------------|-----------------|  
|AppDomainID|`typedef UINT_PTR AppDomainID;`|corprof.h|O identificador de um domínio de aplicativo.|  
|AssemblyID|`typedef UINT_PTR AssemblyID;`|corprof.h|O identificador de um assembly.|  
|ClassID|`typedef UINT_PTR ClassID;`|corprof.h|O identificador de uma classe gerenciada.|  
|CLRDATA_ADDRESS|`typedef ULONG64 CLRDATA_ADDRESS;`|clrdata.h|Um endereço de memória de 64 bits.|
|CLRDATA_ENUM|`typedef ULONG64 CLRDATA_ADDRESS;`|Indisponível|Um endereço de memória de 64 bits.|
|CONNID|`typedef DWORD CONNID;`|cordebug.h, mscoree.h|O identificador de conexão para um thread que está conectado a uma instância do Microsoft SQL Server.|  
|ContextID|`typedef UINT_PTR ContextID;`|corprof.h|O identificador do contexto associado a um thread gerenciado específico.|  
|COR_PRF_ELT_INFO|`typedef UINT_PTR COR_PRF_ELT_INFO;`|corprof.h|Um identificador opaco que representa informações sobre um registro de ativação específico.|  
|COR_PRF_FRAME_INFO|`typedef UINT_PTR COR_PRF_FRAME_INFO;`|corprof.h|Um identificador opaco que aponta para um registro de ativação. Ele é válido somente durante o retorno de chamada para o qual é transmitido.|  
|CORDB_ADDRESS|`typedef ULONG64 CORDB_ADDRESS;`|cordebug.h|Um endereço na memória.|  
|CORDB_CONTINUE_STATUS|`typedef DWORD CORDB_CONTINUE_STATUS;`|cordebug.h|O status de continuação.|  
|CORDB_REGISTER|`typedef ULONG64 CORDB_REGISTER;`|cordebug.h|O valor de um registro da CPU.|
|FunctionID|`typedef UINT_PTR FunctionID;`|corprof.h|O identificador de uma função ou um método.|  
|GCHandleID|`typedef UINT_PTR GCHandleID;`|corprof.h|Um identificador da coleta de lixo.|  
|mdMethodDef|`typedef mdToken mdMethodDef;`|cordebug.h|Um token de definição de método.|
|mdToken|`typedef UINT32 mdToken;`|corprof.h|Um token de metadados (uma linha em uma tabela de metadados).|  
|ModuleID|`typedef UINT_PTR ModuleID;`|corprof.h|O identificador de um módulo de assembly.|  
|ObjectID|`typedef UINT_PTR ObjectID;`|corprof.h|O identificador de um objeto.|  
|PCCOR_SIGNATURE|`typedef SIZE_T PCCOR_SIGNATURE;`|cordebug.h|Um ponteiro para um membro ou assinatura de metadados.|
|ProcessID|`typedef UINT_PTR ProcessID;`|corprof.h|O identificador de um processo gerenciado.|  
|ReJITID|`typedef UINT_PTR ReJITID;`|corprof.h|O identificador de uma função com compilação JIT.|  
|SIZE_T|`typedef ULONG_PTR SIZE_T;`|corsym. h|Um ponteiro para um endereço de memória de 64 bits.|
|TASKID|`typedef UINT64 TASKID;`|cordebug.h, mscoree.h|O identificador de uma instância de [ICLRTask](../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) .|  
|ThreadID|`typedef UINT_PTR ThreadID;`|corprof.h|O identificador de um thread gerenciado.|  
  
## <a name="see-also"></a>Consulte também

- [Referência de API não gerenciada](../../../docs/framework/unmanaged-api/index.md)
