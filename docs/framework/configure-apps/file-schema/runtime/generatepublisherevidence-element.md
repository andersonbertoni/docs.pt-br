---
title: Elemento <generatePublisherEvidence>
ms.date: 03/30/2017
helpviewer_keywords:
- generatePublisherEvidence element
- <generatePublisherEvidence> element
ms.assetid: 7d208f50-e8d5-4a42-bc1a-1cf3590706a8
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1a0861436ca727d63cdae58e3222826bf6414610
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489448"
---
# <a name="generatepublisherevidence-element"></a>\<generatePublisherEvidence > elemento
Especifica se o tempo de execução cria <xref:System.Security.Policy.Publisher> evidência de segurança de acesso do código (CAS).  
  
 \<configuration>  
\<runtime>  
\<generatePublisherEvidence>  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<generatePublisherEvidence    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`enabled`|Atributo obrigatório.<br /><br /> Especifica se o tempo de execução cria <xref:System.Security.Policy.Publisher> evidência.|  
  
## <a name="enabled-attribute"></a>Atributo habilitado  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`false`|Não cria <xref:System.Security.Policy.Publisher> evidência.|  
|`true`|Cria <xref:System.Security.Policy.Publisher> evidência. Esse é o padrão.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|  
|`runtime`|Contém informações sobre opções de inicialização do tempo de execução.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
>  No .NET Framework 4 e posterior, esse elemento não tem efeito sobre os tempos de carregamento de assembly. Para obter mais informações, consulte a seção de "Simplificação de política de segurança" em [alterações de segurança](../../../../../docs/framework/security/security-changes.md).  
  
 O common language runtime (CLR) tenta verificar a assinatura Authenticode no tempo de carregamento para criar <xref:System.Security.Policy.Publisher> evidência para o assembly. No entanto, por padrão, a maioria dos aplicativos não precisam <xref:System.Security.Policy.Publisher> evidência. Política de CAS padrão não depende do <xref:System.Security.Policy.PublisherMembershipCondition>. Você deve evitar o custo de inicialização desnecessários associado ao verificar a assinatura do publicador, a menos que seu aplicativo é executado em um computador com a política de CAS personalizada ou pretende atender às demandas de <xref:System.Security.Permissions.PublisherIdentityPermission> em um ambiente de confiança parcial. (Demandas de permissões de identidade sempre terá êxito em um ambiente de confiança total).  
  
> [!NOTE]
>  É recomendável que os serviços usam o `<generatePublisherEvidence>` elemento para melhorar o desempenho de inicialização.  Usar esse elemento também pode ajudar a evitar atrasos que podem causar um tempo limite e o cancelamento da inicialização do serviço.  
  
## <a name="configuration-file"></a>Arquivo de Configuração  
 Esse elemento pode ser usado apenas no arquivo de configuração do aplicativo.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o `<generatePublisherEvidence>` elemento para desabilitar a verificação de política de editor de autoridades de certificação para um aplicativo.  
  
```xml  
<configuration>  
    <runtime>  
        <generatePublisherEvidence enabled="false"/>  
    </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- [Esquema de configurações do tempo de execução](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [Esquema de arquivos de configuração](../../../../../docs/framework/configure-apps/file-schema/index.md)
