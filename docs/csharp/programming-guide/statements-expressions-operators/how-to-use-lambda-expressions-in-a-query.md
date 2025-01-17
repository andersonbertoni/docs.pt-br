---
title: 'Como: usar expressões lambda em uma consulta – Guia de Programação em C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [C#], in LINQ
ms.assetid: 3cac4d25-d11f-4abd-9e7c-0f02e97ae06d
ms.openlocfilehash: ad9feed7ea3d96267d632f4ca4bc992f2c8d335f
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796650"
---
# <a name="how-to-use-lambda-expressions-in-a-query-c-programming-guide"></a>Como: usar expressões lambda em uma consulta (Guia de Programação em C#)
Você não usa expressões lambda diretamente na sintaxe da consulta, mas as usa em chamadas de método e as expressões de consulta podem conter chamadas de método. Na verdade, algumas operações de consulta podem ser expressas na sintaxe de método. Para obter mais informações sobre a diferença entre a sintaxe de consulta e sintaxe de método, consulte [Sintaxe de consulta e sintaxe de método em LINQ](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar uma expressão lambda em uma consulta baseada em método usando operador de consulta padrão <xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType>. O método <xref:System.Linq.Enumerable.Where%2A> nesse exemplo tem um parâmetro de entrada do tipo delegado <xref:System.Func%602>, e esse delegado utiliza um inteiro como entrada e retorna um booliano. A expressão lambda pode ser convertida para esse delegado. Se essa fosse uma consulta [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] que usasse o método <xref:System.Linq.Queryable.Where%2A?displayProperty=nameWithType>, o tipo de parâmetro seria um `Expression<Func<int,bool>>`, mas a expressão lambda teria exatamente a mesma aparência. Para saber mais sobre o tipo de expressão, confira <xref:System.Linq.Expressions.Expression?displayProperty=nameWithType>.  
  
 [!code-csharp[csProgGuideLINQ#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csrefLINQHowTos.cs#1)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como usar uma expressão lambda em uma chamada de método de uma expressão de consulta. O lambda é necessário porque o operador de consulta padrão <xref:System.Linq.Enumerable.Sum%2A> não pode ser invocado usando a sintaxe de consulta.  
  
 A consulta primeiro agrupa os alunos de acordo com o nível de ensino, conforme definido no enum `GradeLevel`. Em seguida, para cada grupo, ela adiciona as pontuações totais de cada aluno. Isso requer duas operações `Sum`. O `Sum` interno calcula a pontuação total para cada estudante e o `Sum` externo mantém um total acumulado combinado para todos os alunos no grupo.  
  
 [!code-csharp[csProgGuideLINQ#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csrefLINQHowTos.cs#2)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Para executar esse código, copie e cole o método para o `StudentClass` que é fornecido em [Como consultar uma coleção de objetos](../../../csharp/programming-guide/linq-query-expressions/how-to-query-a-collection-of-objects.md) e chame-o do método `Main`.  
  
## <a name="see-also"></a>Consulte também

- [Expressões Lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)
- [Árvores de expressão (C#)](../concepts/expression-trees/index.md)
