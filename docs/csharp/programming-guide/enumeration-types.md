---
title: Tipos de enumeração – Guia de Programação em C#
ms.custom: seodec18
ms.date: 09/10/2017
helpviewer_keywords:
- enumerations [C#]
- enums [C#]
- C# Language, enums
- bit flags [C#]
ms.assetid: 64a9b731-9e3c-4336-8a09-018db2aa10b7
ms.openlocfilehash: 669357bbd6527324bbedbcf1f537bf570c63ce5b
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67423662"
---
# <a name="enumeration-types-c-programming-guide"></a>Tipos de enumeração (Guia de Programação em C#)

Um tipo de enumeração (também chamado de uma enumeração ou enum) fornece uma maneira eficiente para definir um conjunto de constantes integrais nomeadas que podem ser atribuídas a um valor. Por exemplo, suponha que você precisa definir uma variável cujo valor representará um dia da semana. Há apenas sete valores significativos que essa variável armazenará. Para definir esses valores, você pode usar um tipo de enumeração, que é declarado usando a palavra-chave [enum](../../csharp/language-reference/keywords/enum.md).

[!code-csharp[csProgGuideEnums#1](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEnums/CS/Enums.cs#1)]

Por padrão o tipo subjacente de cada elemento na enumeração é [int](../../csharp/language-reference/builtin-types/integral-numeric-types.md). Você pode especificar outro tipo numérico integral usando dois-pontos, como mostrado no exemplo anterior. Para obter uma lista completa dos tipos possíveis, consulte [enum (Referência de C#)](../../csharp/language-reference/keywords/enum.md).

Você pode verificar os valores numéricos subjacentes com a conversão em tipo subjacente, como mostra o exemplo a seguir.

```csharp
Day today = Day.Monday;
int dayNumber =(int)today;
Console.WriteLine("{0} is day number #{1}.", today, dayNumber);

Month thisMonth = Month.Dec;
byte monthNumber = (byte)thisMonth;
Console.WriteLine("{0} is month number #{1}.", thisMonth, monthNumber);

// Output:
// Monday is day number #1.
// Dec is month number #11.
```

A seguir estão as vantagens de usar uma enumeração, em vez de um tipo numérico:

- Você especifica claramente para o código do cliente quais valores são válidos para a variável.

- No Visual Studio, o IntelliSense lista os valores definidos.

Quando você não especifica valores para os elementos na lista de enumerador, os valores são automaticamente incrementados em 1. No exemplo anterior, `Day.Sunday` tem um valor de 0, `Day.Monday` tem um valor de 1 e assim por diante. Ao criar um novo objeto `Day`, ele terá um valor padrão de `Day.Sunday` (0) se você não atribuir explicitamente um valor a ele. Quando você criar uma enumeração, selecione o valor padrão mais lógico e forneça a ele um valor igual a zero. Isso fará com que todos os enumeradores tenham esse valor padrão se eles não tiverem um valor explicitamente atribuído quando forem criados.

Se a variável `meetingDay` for do tipo `Day`, (sem uma conversão explícita) você pode apenas atribuir a ele um dos valores definidos por `Day`. E se o dia da reunião for alterado, você poderá atribuir um novo valor de `Day` para `meetingDay`:

[!code-csharp[csProgGuideEnums#4](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEnums/CS/Enums.cs#4)]

> [!NOTE]
> É possível atribuir qualquer valor inteiro arbitrário a `meetingDay`. Por exemplo, esta linha de código não produz um erro: `meetingDay = (Day) 42`. No entanto, você não deve fazer isso porque a expectativa implícita é que uma variável enum conterá apenas um dos valores definidos pela enumeração. Atribuir um valor arbitrário a uma variável de um tipo de enumeração é introduzir um alto risco de erros.

Você pode atribuir quaisquer valores aos elementos na lista de enumeradores de um tipo de enumeração e também pode usar valores computados:

[!code-csharp[csProgGuideEnums#3](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEnums/CS/Enums.cs#3)]

## <a name="enumeration-types-as-bit-flags"></a>Tipos de Enumeração como Sinalizadores de Bit

Você pode usar um tipo de enumeração para definir sinalizadores de bits, que permite que uma instância do tipo de enumeração armazenar qualquer combinação dos valores que são definidos na lista de enumeradores. (Claro, algumas combinações podem não ser significativas ou permitidas em seu código de programa.)

Crie uma enumeração de sinalizadores de bits aplicando o atributo <xref:System.FlagsAttribute?displayProperty=nameWithType> e definindo os valores apropriadamente para que operações bit a bit `AND`, `OR`, `NOT` e `XOR` possam ser executadas neles. Em uma enumeração de sinalizadores de bits, inclua uma constante nomeada com um valor de zero que significa “nenhum sinalizador está definido”. Não forneça um valor de zero a um sinalizador se isso não significar “nenhum sinalizador está definido”.

No exemplo a seguir, outra versão da enumeração `Day`, que é chamada de `Days`, é definida. `Days` tem o atributo `Flags` e a cada valor é atribuída a próxima maior potência de 2. Isso permite que você crie uma variável `Days` cujo valor é `Days.Tuesday | Days.Thursday`.

[!code-csharp[csProgGuideEnums#2](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEnums/CS/Enums.cs#2)]

Para definir um sinalizador em uma enumeração, use o operador `OR` de bit a bit mostrado no exemplo a seguir:

[!code-csharp[csProgGuideEnums#6](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEnums/CS/Enums.cs#6)]

Para determinar se um sinalizador específico é definido, use uma operação `AND` bit a bit, conforme mostrado no exemplo a seguir:

[!code-csharp[csProgGuideEnums#7](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEnums/CS/Enums.cs#7)]

Para saber mais sobre o que considerar ao definir tipos de enumeração com o atributo <xref:System.FlagsAttribute?displayProperty=nameWithType>, veja <xref:System.Enum?displayProperty=nameWithType>.

## <a name="using-the-systemenum-methods-to-discover-and-manipulate-enum-values"></a>Usando os Métodos System.Enum Methods para Descobrir e Manipular Valores Enum

Todas as enumerações são instâncias do tipo <xref:System.Enum?displayProperty=nameWithType>. Não é possível derivar novas classes de <xref:System.Enum?displayProperty=nameWithType>, mas você pode usar seus métodos para descobrir informações sobre e manipular valores em uma instância de enumeração.

[!code-csharp[csProgGuideEnums#5](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEnums/CS/Enums.cs#5)]

Para obter mais informações, consulte <xref:System.Enum?displayProperty=nameWithType>.

Você também pode criar um novo método para uma enumeração usando um método de extensão. Para obter mais informações, confira [Como: criar um novo método para uma enumeração](../../csharp/programming-guide/classes-and-structs/how-to-create-a-new-method-for-an-enumeration.md).

## <a name="see-also"></a>Consulte também

- <xref:System.Enum?displayProperty=nameWithType>
- [Guia de Programação em C#](../../csharp/programming-guide/index.md)
- [enum](../../csharp/language-reference/keywords/enum.md)
