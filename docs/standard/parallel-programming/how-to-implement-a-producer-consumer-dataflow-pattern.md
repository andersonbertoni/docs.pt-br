---
title: 'Como: implementar um padrão de fluxo de dados de produtor-consumidor'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TPL dataflow library, implementing producer-consumer pattern
- Task Parallel Library, dataflows
- producer-consumer patterns, implementing [TPL]
ms.assetid: 47a1d38c-fe9c-44aa-bd15-937bd5659b0b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0ff0cc339a26ef97e8036d905bf3c9530d5dee94
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593117"
---
# <a name="how-to-implement-a-producer-consumer-dataflow-pattern"></a>Como: implementar um padrão de fluxo de dados de produtor-consumidor
Este documento descreve como usar a Biblioteca de fluxo de dados TPL para implementar um padrão de produtor-consumidor. Nesse padrão, o *produtor* envia mensagens a um bloco de mensagens e o *consumidor* lê mensagens nesse bloco.  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra um modelo básico de produtor-consumidor que usa o fluxo de dados. O método `Produce` grava matrizes que contêm bytes de dados aleatórios em um objeto <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601?displayProperty=nameWithType> e o método `Consume` lê bytes de um objeto <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601?displayProperty=nameWithType>. Ao agir nas interfaces <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> e <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601>, em vez de seus tipos derivados, você pode gravar o código reutilizável que pode agir em uma variedade de tipos de bloco de fluxo de dados. Este exemplo usa a classe <xref:System.Threading.Tasks.Dataflow.BufferBlock%601>. Como a classe <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> atua como um bloco de origem e um bloco de destino, o produtor e consumidor podem usar um objeto compartilhado para transferir dados.  
  
 O método `Produce` chama o método <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> em um loop para gravar dados de forma síncrona no bloco de destino. Após o método `Produce` gravar todos os dados no bloco de destino, ele chama o método <xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A> para indicar que o bloco nunca terá dados adicionais disponíveis. O método `Consume` usa os operadores [async](~/docs/csharp/language-reference/keywords/async.md) e [await](~/docs/csharp/language-reference/keywords/await.md) ([Async](~/docs/visual-basic/language-reference/modifiers/async.md) e [Await](~/docs/visual-basic/language-reference/operators/await-operator.md) em Visual Basic) para calcular de forma assíncrona o número total de bytes que são recebidos do objeto <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601>. Para agir de forma assíncrona, o método `Consume` chama o método <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A> para receber uma notificação quando o bloco de origem tiver dados disponíveis e o bloco de origem nunca terá outros dados disponíveis.  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#1)]
 [!code-vb[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#1)]  
  
## <a name="robust-programming"></a>Programação robusta  
 O exemplo anterior usa apenas um consumidor para processar os dados de origem. Se você tiver vários consumidores em seu aplicativo, use o método <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> para ler dados do bloco de origem, conforme mostrado no exemplo a seguir.  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#2)]
 [!code-vb[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#2)]  
  
 O método <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> retorna `False` quando não há dados disponíveis. Quando vários consumidores têm que acessar simultaneamente o bloco de origem, esse mecanismo garante que os dados ainda estarão disponíveis após a chamada para o <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A>.  
  
## <a name="see-also"></a>Consulte também

- [Fluxo de dados](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
