---
title: Tipos de retorno assíncronos (C#)
ms.date: 05/29/2017
ms.assetid: ddb2539c-c898-48c1-ad92-245e4a996df8
ms.openlocfilehash: ca429db9b3ad81555df3c7e02d8827136734e26c
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67347736"
---
# <a name="async-return-types-c"></a>Tipos de retorno assíncronos (C#)
Métodos assíncronos podem conter os seguintes tipos de retorno:

- <xref:System.Threading.Tasks.Task%601>, para um método assíncrono que retorna um valor. 
 
- <xref:System.Threading.Tasks.Task>, para um método assíncrono que executa uma operação, mas não retorna nenhum valor.

- `void`, para um manipulador de eventos. 

- Começando com o C# 7.0, qualquer tipo que tenha um método acessível `GetAwaiter`. O objeto retornado pelo método `GetAwaiter` deve implementar a interface <xref:System.Runtime.CompilerServices.ICriticalNotifyCompletion?displayProperty=nameWithType>.
  
Para obter mais informações sobre os métodos assíncronos, consulte [Programação assíncrona com async e await (C#)](../../../../csharp/programming-guide/concepts/async/index.md).  
  
Cada tipo de retorno é examinado em uma das seções a seguir e você pode encontrar um exemplo completo que usa todos os três tipos no final do tópico.  
  
## <a name="BKMK_TaskTReturnType"></a> Tipo de retorno Task\<TResult\>  
O tipo de retorno <xref:System.Threading.Tasks.Task%601> é usado para um método assíncrono que contém uma instrução [return](../../../../csharp/language-reference/keywords/return.md) (C#), na qual o operando tem o tipo `TResult`.  
  
No exemplo a seguir, o método assíncrono `GetLeisureHours` contém uma instrução `return` que retorna um número inteiro. Portanto, a declaração do método deve especificar um tipo de retorno de `Task<int>`.  O método assíncrono <xref:System.Threading.Tasks.Task.FromResult%2A> é um espaço reservado para uma operação que retorna uma cadeia de caracteres.
  
[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns1.cs)]

Quando `GetLeisureHours` é chamado de dentro de uma expressão await no método `ShowTodaysInfo`, a expressão await recupera o valor inteiro (o valor de `leisureHours`) que está armazenado na tarefa que é retornada pelo método `GetLeisureHours`. Para obter mais informações sobre expressões await, consulte [await](../../../../csharp/language-reference/keywords/await.md).  
  
Você pode entender melhor como isso acontece, separando a chamada ao `GetLeisureHours` da aplicação do `await`, como mostrado no código a seguir. Uma chamada ao método `GetLeisureHours` que não é aguardada imediatamente, retorna um `Task<int>`, como você esperaria da declaração do método. A tarefa é atribuída à variável `integerTask` no exemplo. Já que `integerTask` é um <xref:System.Threading.Tasks.Task%601>, ele contém uma propriedade <xref:System.Threading.Tasks.Task%601.Result> do tipo `TResult`. Nesse caso, `TResult` representa um tipo inteiro. Quando `await` é aplicado à `integerTask`, a expressão await é avaliada como o conteúdo da propriedade <xref:System.Threading.Tasks.Task%601.Result%2A> de `integerTask`. O valor é atribuído à variável `ret`.  
  
> [!IMPORTANT]
>  A propriedade <xref:System.Threading.Tasks.Task%601.Result%2A> é uma propriedade de bloqueio. Se você tentar acessá-la antes que sua tarefa seja concluída, o thread que está ativo no momento será bloqueado até que a tarefa seja concluída e o valor esteja disponível. Na maioria dos casos, você deve acessar o valor usando `await` em vez de acessar a propriedade diretamente. <br/> O exemplo anterior recuperou o valor da propriedade <xref:System.Threading.Tasks.Task%601.Result%2A> para bloquear o thread principal, de modo que o método `ShowTodaysInfo` pudesse concluir a execução antes do encerramento do aplicativo.  

[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns1a.cs#1)]
  
## <a name="BKMK_TaskReturnType"></a> Tipo de retorno Task  
Os métodos assíncronos que não contêm uma instrução `return` ou que contêm uma instrução `return` que não retorna um operando, normalmente têm um tipo de retorno de <xref:System.Threading.Tasks.Task>. Esses métodos retornam `void` se eles são executados de forma síncrona. Se você usar um tipo de retorno <xref:System.Threading.Tasks.Task> para um método assíncrono, um método de chamada poderá usar um operador `await` para suspender a conclusão do chamador até que o método assíncrono chamado seja concluído.  
  
No exemplo a seguir, o método assíncrono `WaitAndApologize` não contém uma instrução `return`, então o método retorna um objeto <xref:System.Threading.Tasks.Task>. Isso permite que `WaitAndApologize` seja aguardado. Observe que o tipo <xref:System.Threading.Tasks.Task> não inclui uma propriedade `Result` porque ele não tem nenhum valor retornado.  

[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns2.cs)]  
  
O `WaitAndApologize` é aguardado, usando uma instrução await, em vez de uma expressão await, semelhante à instrução de chamada a um método síncrono de retorno void. A aplicação de um operador await, nesse caso, não produz um valor.  
  
Como no exemplo <xref:System.Threading.Tasks.Task%601> anterior, você pode separar a chamada ao `WaitAndApologize`, da aplicação de um operador await, como mostrado no código a seguir. No entanto, lembre-se que uma `Task` não tem uma propriedade `Result` e que nenhum valor será produzido quando um operador await for aplicado a uma `Task`.  
  
O código a seguir separa a chamada ao método `WaitAndApologize` da espera pela tarefa que o método retorna.  
 
[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns2a.cs#1)]  
 
## <a name="BKMK_VoidReturnType"></a> Tipo de retorno void

O tipo de retorno `void` é usado em manipuladores de eventos assíncronos, que exigem um tipo de retorno `void`. Para métodos diferentes de manipuladores de eventos que não retornam um valor, você deve retornar um <xref:System.Threading.Tasks.Task>, porque não é possível esperar por um método assíncrono que retorna `void`. Qualquer chamador desse método deve ser capaz de continuar até a conclusão, sem aguardar a conclusão do método assíncrono chamado e o chamador deve ser independente de todos os valores ou exceções gerados pelo método assíncrono.  
  
O chamador de um método assíncrono de retorno void não pode capturar exceções que são lançadas pelo método e essas exceções sem tratamento provavelmente causarão falha do seu aplicativo. Se ocorrer uma exceção em um método assíncrono que retorna uma <xref:System.Threading.Tasks.Task> ou uma <xref:System.Threading.Tasks.Task%601>, a exceção será armazenada na tarefa retornada e relançada quando a tarefa for aguardada. Portanto, verifique se qualquer método assíncrono que pode produzir uma exceção tem um tipo de retorno de <xref:System.Threading.Tasks.Task> ou <xref:System.Threading.Tasks.Task%601> e que as chamadas ao método são aguardadas.  
  
Para obter mais informações de como capturar exceções em métodos assíncronos, confira a seção [Exceções em métodos assíncronos](../../../language-reference/keywords/try-catch.md#exceptions-in-async-methods) do tópico [try-catch](../../../language-reference/keywords/try-catch.md).  
  
O exemplo a seguir mostra o comportamento de um manipulador de eventos assíncrono. Observe que o código de exemplo, um manipulador de eventos assíncrono, deve informar o thread principal quando ele for concluído. Em seguida, o thread principal pode aguardar um manipulador de eventos assíncronos ser concluído antes de sair do programa.
 
[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns3.cs)]  
 
## <a name="generalized-async-return-types-and-valuetasktresult"></a>Tipos de retorno assíncronos generalizados e ValueTask\<TResult\>

Começando com o C# 7.0, um método assíncrono pode retornar qualquer tipo que tenha um método `GetAwaiter` acessível.
 
Já que <xref:System.Threading.Tasks.Task> e <xref:System.Threading.Tasks.Task%601> são tipos de referência, a alocação de memória em caminhos críticos para o desempenho, especialmente quando alocações ocorrerem em loops estreitos, podem afetar o desempenho. Suporte para tipos de retorno generalizados significa que você pode retornar um tipo de valor leve em vez de um tipo de referência para evitar as alocações de memória adicionais. 

O .NET fornece a estrutura <xref:System.Threading.Tasks.ValueTask%601?displayProperty=nameWithType> como uma implementação leve de um valor de retorno de tarefa generalizado. Para usar o tipo <xref:System.Threading.Tasks.ValueTask%601?displayProperty=nameWithType>, você deve adicionar o pacote NuGet `System.Threading.Tasks.Extensions` ao seu projeto. O exemplo a seguir usa a estrutura <xref:System.Threading.Tasks.ValueTask%601> para recuperar o valor de dois lançamentos de dados. 
  
[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-valuetask.cs)]

## <a name="see-also"></a>Consulte também

- <xref:System.Threading.Tasks.Task.FromResult%2A>
- [Passo a passo: acesso à Web com o uso de Async e Await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [Fluxo de controle em programas assíncronos (C#)](../../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md)
- [async](../../../../csharp/language-reference/keywords/async.md)
- [await](../../../../csharp/language-reference/keywords/await.md)
