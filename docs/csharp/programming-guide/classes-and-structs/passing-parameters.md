---
title: Passando parâmetros – Guia de Programação em C#
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- parameters [C#], passing
- passing parameters [C#]
- arguments [C#]
- methods [C#], passing parameters
- C# language, method parameters
ms.assetid: a5c3003f-7441-4710-b8b1-c79de77e0b77
ms.openlocfilehash: 77228def3a6426b6e0383d657c2eaeac37e5e273
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64600147"
---
# <a name="passing-parameters-c-programming-guide"></a>Passando parâmetros (Guia de Programação em C#)
No C#, argumentos podem ser passados para parâmetros por valor ou por referência. A passagem por referência permite que métodos, propriedades, indexadores, operadores, construtores e membros da função alterem o valor dos parâmetros e façam essa alteração persistir no ambiente de chamada. Para passar um parâmetro por referência com a intenção de alterar o valor, use a palavra-chave `ref` ou `out`. Para passar por referência com a intenção de evitar a cópia, mas não alterar o valor, use o modificador `in`. Para simplificar, somente a palavra-chave `ref` é usada nos exemplos neste tópico. Para obter mais informações sobre a diferença entre `in`, `ref` e `out`, consulte [in](../../../csharp/language-reference/keywords/in-parameter-modifier.md), [ref](../../../csharp/language-reference/keywords/ref.md) e [out](../../../csharp/language-reference/keywords/out-parameter-modifier.md).  
  
 O exemplo a seguir ilustra a diferença entre parâmetros de valor e referência.  
  
 [!code-csharp[csProgGuideParameters#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#10)]  
  
 Para mais informações, consulte os seguintes tópicos:  
  
- [Passando parâmetros de tipo de valor](../../../csharp/programming-guide/classes-and-structs/passing-value-type-parameters.md)  
  
- [Passando parâmetros de tipo de referência](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)  
  
## <a name="c-language-specification"></a>Especificação da Linguagem C#  

Para obter mais informações, veja as [listas de argumentos](~/_csharplang/spec/expressions.md#argument-lists) na [Especificação da linguagem C#](../../language-reference/language-specification/index.md). A especificação da linguagem é a fonte definitiva para a sintaxe e o uso de C#.
  
## <a name="see-also"></a>Consulte também

- [Guia de Programação em C#](../../../csharp/programming-guide/index.md)
- [Métodos](../../../csharp/programming-guide/classes-and-structs/methods.md)
