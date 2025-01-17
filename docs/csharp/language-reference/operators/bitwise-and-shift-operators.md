---
title: Operadores bit a bit e de deslocamento – referência do C#
description: Saiba mais sobre operadores C# que executam operações de deslocamento ou lógicas bit a bit com operandos de tipos integrais.
ms.date: 04/18/2019
author: pkulikov
f1_keywords:
- ~_CSharpKeyword
- <<_CSharpKeyword
- '>>_CSharpKeyword'
- '&_CSharpKeyword'
- ^_CSharpKeyword
- '|_CSharpKeyword'
helpviewer_keywords:
- bitwise logical operators [C#]
- shift operators [C#]
- tilde operator [C#]
- one's complement operator [C#]
- bitwise complement operator [C#]
- ~ operator [C#]
- left shift operator [C#]
- << operator [C#]
- right shift operator [C#]
- '>> operator [C#]'
- bitwise logical AND operator [C#]
- ampersand operator [C#]
- '& operator [C#]'
- bitwise logical exclusive OR operator [C#]
- bitwise logical XOR operator [C#]
- ^ operator [C#]
- bitwise logical OR operator [C#]
- '| operator [C#]'
ms.openlocfilehash: c18a06971887049a443f0bd1af7c77610a787a27
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2019
ms.locfileid: "67609947"
---
# <a name="bitwise-and-shift-operators-c-reference"></a>Operadores bit a bit e de deslocamento (referência do C#)

Os operadores a seguir executam operações de deslocamento ou bit a bit com operandos de [tipos integrais](../builtin-types/integral-numeric-types.md):

- Operador unário [`~` (complemento bit a bit)](#bitwise-complement-operator-)
- Operadores binários [`<<` (deslocamento à esquerda)](#left-shift-operator-) e [`>>` (deslocamento à direita)](#right-shift-operator-)
- Operadores binários [`&` (AND lógico)](#logical-and-operator-), [`|` (OR lógico)](#logical-or-operator-) e [`^` (OR exclusivo lógico)](#logical-exclusive-or-operator-)

Esses operadores são definidos para os tipos `int`, `uint`, `long` e `ulong`. Quando ambos os operandos são de outros tipos integrais (`sbyte`, `byte`, `short`, `ushort` ou `char`), seus valores são convertidos no tipo `int`, que também é o tipo de resultado de uma operação. Quando os operandos são de tipos integrais diferentes, seus valores são convertidos no tipo integral mais próximo que o contém. Para saber mais, confira a seção [Promoções numéricas](~/_csharplang/spec/expressions.md#numeric-promotions) da [Especificação da linguagem C#](~/_csharplang/spec/introduction.md).

Os operadores `&`, `|` e `^` também são definidos para os operandos do tipo `bool`. Para obter mais informações, veja [Operadores lógicos boolianos](boolean-logical-operators.md).

As operações de deslocamento e bit a bit nunca causam estouro e produzem os mesmos resultados nos contextos [marcados e desmarcados](../keywords/checked-and-unchecked.md).

## <a name="bitwise-complement-operator-"></a>Operador de complemento bit a bit ~

O operador `~` produz um complemento bit a bit de seu operando invertendo cada bit:

[!code-csharp-interactive[bitwise NOT](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseComplement)]

Você também pode usar o símbolo `~` para declarar finalizadores. Para mais informações, consulte [Finalizadores](../../programming-guide/classes-and-structs/destructors.md).

## <a name="left-shift-operator-"></a>Operador de deslocamento à esquerda \<\<

O operador `<<` desloca para esquerda o operando à esquerda pelo número de bits definido pelo seu operando à direita.

A operação de deslocamento à esquerda descarta os bits de ordem superior que estão fora do intervalo do tipo de resultado e define as posições de bits vazios de ordem inferior como zero, como mostra o exemplo a seguir:

[!code-csharp-interactive[left shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#LeftShift)]

Como os operadores de deslocamento são definidos apenas para os tipos `int`, `uint`, `long` e `ulong`, o resultado de uma operação sempre contém pelo menos 32 bits. Se o operando à esquerda for de outro tipo integral (`sbyte`, `byte`, `short`, `ushort` ou `char`), seu valor será convertido no tipo `int`, como mostra o exemplo a seguir:

[!code-csharp-interactive[left shift with promotion](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#LeftShiftPromoted)]

Para saber mais sobre como o operando à direita do operador `<<` define a contagem de deslocamento, veja a seção [Contagem de deslocamento dos operadores de deslocamento](#shift-count-of-the-shift-operators).

## <a name="right-shift-operator-"></a>Operador de deslocamento à direita >>

O operador `>>` desloca para direita o operando à esquerda pelo número de bits definido pelo seu operando à direita.

A operação de deslocamento à direita descarta os bits de ordem inferior, como mostra o exemplo a seguir:

[!code-csharp-interactive[right shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#RightShift)]

As posições vazias de bit de ordem superior são definidas com base no tipo do operando à esquerda da seguinte maneira:

- Se o operando à esquerda for do tipo [int](../builtin-types/integral-numeric-types.md) ou [long](../builtin-types/integral-numeric-types.md), o operador de deslocamento à direita executará um deslocamento *aritmético*: o valor do bit mais significativo (o bit de sinal) do operando à esquerda é propagado para as posições vazias de bits de ordem superior. Ou seja, as posições vazias de bit de ordem superior são definidas como zero se o operando à esquerda for positivo e definidas como um se ele for negativo.

  [!code-csharp-interactive[arithmetic right shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#ArithmeticRightShift)]

- Se o operando à esquerda for do tipo [uint](../builtin-types/integral-numeric-types.md) ou [ulong](../builtin-types/integral-numeric-types.md), o operador de deslocamento à direita executará um deslocamento *lógico*: as posições vazias de bit de ordem superior são sempre definidas como zero.

  [!code-csharp-interactive[logical right shift](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#LogicalRightShift)]

Para saber mais sobre como o operando à direita do operador `>>` define a contagem de deslocamento, veja a seção [Contagem de deslocamento dos operadores de deslocamento](#shift-count-of-the-shift-operators).

## <a name="logical-and-operator-"></a> Operador AND lógico &amp;

O operador `&` computa o AND lógico bit a bit de seus operandos:

[!code-csharp-interactive[bitwise AND](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseAnd)]

Para os operandos do tipo `bool`, o operador `&` computa o [AND lógico](boolean-logical-operators.md#logical-and-operator-) de seus operandos. O operador `&` unário é o [operador address-of](pointer-related-operators.md#address-of-operator-).

## <a name="logical-exclusive-or-operator-"></a>Operador OR exclusivo lógico ^

O operador `^` computa o OR exclusivo lógico bit a bit, também conhecido como o XOR lógico bit a bit, de seus operandos:

[!code-csharp-interactive[bitwise XOR](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseXor)]

Para os operandos do tipo `bool`, o operador `^` computa o [OR exclusivo lógico](boolean-logical-operators.md#logical-exclusive-or-operator-) de seus operandos.

## <a name="logical-or-operator-"></a>Operador OR lógico |

O operador `|` computa o OR lógico bit a bit de seus operandos:

[!code-csharp-interactive[bitwise OR](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#BitwiseOr)]

Para os operandos do tipo `bool`, o operador `|` computa o [OR lógico](boolean-logical-operators.md#logical-or-operator-) de seus operandos.

## <a name="compound-assignment"></a>Atribuição composta

Para um operador binário `op`, uma expressão de atribuição composta do formato

```csharp
x op= y
```

equivale a

```csharp
x = x op y
```

exceto que `x` é avaliado apenas uma vez.

O seguinte exemplo demonstra o uso da atribuição composta com operadores bit a bit e de deslocamento:

[!code-csharp-interactive[compound assignment](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#CompoundAssignment)]

Devido a [promoções numéricas](~/_csharplang/spec/expressions.md#numeric-promotions), o resultado da operação `op` pode não ser implicitamente conversível no tipo `T` de `x`. Nesse caso, se `op` for um operador predefinido e o resultado da operação for explicitamente convertido no tipo `T` de `x`, uma expressão de atribuição composta da forma `x op= y` será equivalente a `x = (T)(x op y)`, exceto que `x` será avaliada apenas uma vez. O exemplo a seguir demonstra esse comportamento:

[!code-csharp-interactive[compound assignment with cast](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#CompoundAssignmentWithCast)]

## <a name="operator-precedence"></a>Precedência do operador

A lista a seguir ordena os operadores lógicos, começando da mais alta precedência até a mais baixa:

- Operador de complemento bit a bit `~`
- Operadores de deslocamento `<<` e `>>`
- Operador AND lógico `&`
- Operador OR exclusivo lógico `^`
- Operador OR lógico `|`

Use parênteses, `()`, para alterar a ordem de avaliação imposta pela precedência do operador:

[!code-csharp-interactive[operator precedence](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#Precedence)]

Para obter a lista completa de operadores do C# ordenada pelo nível de precedência, confira [Operadores do C#](index.md).

## <a name="shift-count-of-the-shift-operators"></a>Contagem de deslocamento dos operadores de deslocamento

Para os operadores de deslocamento `<<` e `>>`, o tipo do operando à direita deve ser [int](../builtin-types/integral-numeric-types.md) ou um tipo que tenha uma [conversão numérica implícita predefinida](../keywords/implicit-numeric-conversions-table.md) para `int`.

Para as expressões `x << count` e `x >> count`, a contagem real de deslocamento depende do tipo de `x` da seguinte maneira:

- Se o tipo de `x` for [int](../builtin-types/integral-numeric-types.md) ou [uint](../builtin-types/integral-numeric-types.md), a contagem de deslocamentos será definida pelos *cinco* bits de ordem inferior do operando à direita. Ou seja, a contagem de deslocamentos é calculada a partir de `count & 0x1F` (ou `count & 0b_1_1111`).

- Se o tipo de `x` for [long](../builtin-types/integral-numeric-types.md) ou [ulong](../builtin-types/integral-numeric-types.md), a contagem de deslocamentos será definida pelos *seis* bits de ordem inferior do operando à direita. Ou seja, a contagem de deslocamentos é calculada a partir de `count & 0x3F` (ou `count & 0b_11_1111`).

O exemplo a seguir demonstra esse comportamento:

[!code-csharp-interactive[shift count example](~/samples/csharp/language-reference/operators/BitwiseAndShiftOperators.cs#ShiftCount)]

## <a name="enumeration-logical-operators"></a>Operadores lógicos de enumeração

Os operadores `~`, `&`, `|` e `^` também são definidos para qualquer tipo de [enumeração](../keywords/enum.md). Para operandos do mesmo tipo de enumeração, uma operação lógica é executada nos valores correspondentes do tipo integral subjacente. Por exemplo, para qualquer `x` e `y` de um tipo de enumeração `T` com um tipo subjacente `U`, a expressão `x & y` produz o mesmo resultado que a expressão `(T)((U)x & (U)y)`.

Geralmente, você usa os operadores lógicos bit a bit com um tipo de enumeração definido com o atributo [sinalizadores](xref:System.FlagsAttribute). Para obter mais informações, veja a seção [Tipos de enumeração como sinalizadores de bit](../../programming-guide/enumeration-types.md#enumeration-types-as-bit-flags) do artigo [Tipos de enumeração](../../programming-guide/enumeration-types.md).

## <a name="operator-overloadability"></a>Capacidade de sobrecarga do operador

Um tipo definido pelo usuário pode [sobrecarregar](operator-overloading.md) os operadores `~`, `<<`, `>>`, `&`, `|` e `^`. Quando um operador binário está sobrecarregado, o operador de atribuição composta correspondente também é implicitamente sobrecarregado. Um tipo definido pelo usuário não pode sobrecarregar explicitamente um operador de atribuição composta.

Se um tipo definido pelo usuário `T` sobrecarregar o operador `<<` ou `>>`, o tipo do operando à esquerda deverá ser `T` e o tipo do operando à direita deverá ser `int`.

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, confira as seguintes seções da [especificação da linguagem C#](~/_csharplang/spec/introduction.md):

- [Operador de complemento bit a bit](~/_csharplang/spec/expressions.md#bitwise-complement-operator)
- [Operadores shift](~/_csharplang/spec/expressions.md#shift-operators)
- [Operadores lógicos](~/_csharplang/spec/expressions.md#logical-operators)
- [Atribuição composta](~/_csharplang/spec/expressions.md#compound-assignment)
- [Promoções numéricas](~/_csharplang/spec/expressions.md#numeric-promotions)

## <a name="see-also"></a>Consulte também

- [Referência de C#](../index.md)
- [Operadores do C#](index.md)
- [Operadores lógicos boolianos](boolean-logical-operators.md)
