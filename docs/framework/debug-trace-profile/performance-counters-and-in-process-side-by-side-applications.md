---
title: Contadores de desempenho e aplicativos lado a lado em processo
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- performance counters
- performance counters,and in-process side-by-side applications
- performance,.NET Framework applications
- performance monitoring,counters
ms.assetid: 6888f9be-c65b-4b03-a07b-df7ebdee2436
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dd3501bc74da2c9a812f9c4816b5a081b3780cd0
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490035"
---
# <a name="performance-counters-and-in-process-side-by-side-applications"></a>Contadores de desempenho e aplicativos lado a lado em processo
Usando o Monitor de Desempenho (Perfmon.exe), é possível diferenciar os contadores de desempenho por tempo de execução. Este tópico descreve a alteração do Registro necessária para habilitar essa funcionalidade.  
  
## <a name="the-default-behavior"></a>O comportamento padrão  
 Por padrão, o Monitor de Desempenho exibe os contadores de desempenho classificados por aplicativo. No entanto, há dois cenários em que isso torna-se um problema:  
  
- Ao monitorar dois aplicativos que têm o mesmo nome. Por exemplo, se ambos os aplicativos são nomeados myapp.exe, um é exibido como **myapp** e o outro como **myapp#1** na coluna **Instância**. Nesse caso, é difícil corresponder um contador de desempenho a um aplicativo específico. Não está claro se os dados coletados para **myapp#1** referem-se ao primeiro myapp.exe ou ao segundo.  
  
- Quando um aplicativo usa várias instâncias do Common Language Runtime. O .NET Framework 4 dá suporte a cenários de hospedagem de lado a lado em processo; ou seja, um único processo ou aplicativo pode carregar várias instâncias do common language runtime. Se um único aplicativo chamado myapp.exe carrega duas instâncias de tempo de execução, por padrão, elas serão designadas na coluna **Instância** como **myapp** e **myapp#1**. Nesse caso, não está claro se **myapp** e **myapp#1** referem-se a dois aplicativos de mesmo nome ou ao mesmo aplicativo com dois tempos de execução. Se vários aplicativos com o mesmo nome carregam vários tempos de execução, a ambiguidade é ainda maior.  
  
 Você pode definir uma chave do Registro para eliminar essa ambiguidade. Para aplicativos desenvolvidos usando o .NET Framework 4, essa alteração no registro adiciona um identificador de processo seguido por um identificador de instância de tempo de execução para o nome do aplicativo na **instância** coluna. Em vez de *aplicativo* ou *aplicativo*#1, o aplicativo agora é identificado como *aplicativo*_`p`*processID*\_`r`*runtimeID* na coluna **Instância**. Se um aplicativo foi desenvolvido usando uma versão anterior do common language runtime, essa instância é representada como *application\_* `p`*processID* desde que o. NET Framework 4 está instalado.  
  
## <a name="performance-counters-for-in-process-side-by-side-applications"></a>Contadores de desempenho para aplicativos lado a lado em processo  
 Para lidar com contadores de desempenho para várias versões do Common Language Runtime hospedadas em um único aplicativo, você deve alterar uma única configuração de chave do Registro, conforme mostrado na tabela a seguir.  
  
|||  
|-|-|  
|Nome da chave|HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\\.NETFramework\Performance|  
|Nome do valor|ProcessNameFormat|  
|Tipo de valor|REG_DWORD|  
|Valor|1 (0x00000001)|  
  
 Um valor de 0 para `ProcessNameFormat` indica que o comportamento padrão está habilitado, ou seja, Perfmon.exe exibe os contadores de desempenho por aplicativo. Quando você define esse valor como 1, Perfmon.exe elimina a ambiguidade de várias versões de um aplicativo e fornece contadores de desempenho por tempo de execução. Qualquer outro valor para a configuração da chave do Registro `ProcessNameFormat` não tem suporte e é reservada para uso futuro.  
  
 Depois de atualizar a configuração da chave do Registro `ProcessNameFormat`, você deve reiniciar Perfmon.exe ou outros consumidores de contadores de desempenho para que o novo recurso de nomeação de instância funcione corretamente.  
  
 O exemplo a seguir mostra como alterar o valor de `ProcessNameFormat` programaticamente.  
  
 [!code-csharp[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/cs/regsetting1.cs#1)]
 [!code-vb[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/vb/regsetting1.vb#1)]  
  
 Quando você alterar esse registro, Perfmon.exe exibe os nomes dos aplicativos destinados ao .NET Framework 4 como *application*_`p`*processID* \_ `r` *runtimeID*, onde *application* é o nome do aplicativo, *processID* é o identificador de processo do aplicativo, e  *runtimeID* é um identificador de tempo de execução de linguagem comum. Por exemplo, se um aplicativo chamado myapp.exe carrega duas instâncias nomeadas do Common Language Runtime, Perfmon.exe pode identificar uma instância como myapp_p1416_r10 e a segunda como myapp_p3160_r10. O identificador de tempo de execução apenas retira a ambiguidade os tempos de execução dentro de um processo; ele não fornece nenhuma outra informação sobre o tempo de execução. (Por exemplo, a ID de tempo de execução não tem nenhuma relação com a versão ou o SKU do tempo de execução.)  
  
 Se o .NET Framework 4 é instalado, a alteração do registro também afeta aplicativos que foram desenvolvidos usando versões anteriores do .NET Framework. Eles aparecem em Perfmon.exe como *aplicativo_* `p`*processID*, em que *aplicativo* é o nome do aplicativo e *processID* é o identificador de processo. Por exemplo, se os contadores de desempenho de dois aplicativos chamados myapp.exe são monitorados, um pode aparecer como myapp_p23900 e o outro como myapp_p24908.  
  
> [!NOTE]
>  O identificador de processo elimina a ambiguidade da resolução de dois aplicativos com o mesmo nome que usam versões anteriores do tempo de execução. Um identificador de tempo de execução não é necessário para versões anteriores, porque versões anteriores do Common Language Runtime não dão suporte a cenários lado a lado.  
  
 Se o .NET Framework 4 não está presente ou foi desinstalado, definir a chave do registro não tem nenhum efeito. Isso significa que dois aplicativos com o mesmo nome continuarão a aparecer no Perfmon.exe como *aplicativo* e *aplicativo#1* (por exemplo, como **myapp** e **myapp#1**).
