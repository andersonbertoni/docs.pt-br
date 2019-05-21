---
title: Operadores de acesso a membro – referência de C#
description: Aprenda sobre operadores de C# que você pode usar para acessar membros de tipo.
ms.date: 05/09/2019
author: pkulikov
f1_keywords:
- ._CSharpKeyword
- '[]_CSharpKeyword'
- ()_CSharpKeyword
helpviewer_keywords:
- member access operators [C#]
- member access operator [C#]
- dot operator [C#]
- . operator [C#]
- subscript operator [C#]
- square brackets [] operator [C#]
- indexer operator [C#]
- '[] operator [C#]'
- null-conditional operators [C#]
- ?. operator [C#]
- ?[] operator [C#]
- invocation operator [C#]
- method call [C#]
- method invocation [C#]
- delegate invocation [C#]
- () operator [C#]
ms.openlocfilehash: 921d69e3deb7e5bb5115eb723727462839af9b6b
ms.sourcegitcommit: 4c10802ad003374641a2c2373b8a92e3c88babc8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65452888"
---
# <a name="member-access-operators"></a><span data-ttu-id="bf363-103">Operadores de acesso a membro</span><span class="sxs-lookup"><span data-stu-id="bf363-103">Member access operators</span></span>

<span data-ttu-id="bf363-104">Quando você acessa um membro de tipo, você pode usar os seguintes operadores:</span><span class="sxs-lookup"><span data-stu-id="bf363-104">You might use the following operators when you access a type member:</span></span>

- <span data-ttu-id="bf363-105">[`.` (acesso a membro)](#member-access-operator-): para acessar um membro de um namespace ou um tipo</span><span class="sxs-lookup"><span data-stu-id="bf363-105">[`.` (member access)](#member-access-operator-): to access a member of a namespace or a type</span></span>
- <span data-ttu-id="bf363-106">[`[]` (acesso a um indexador ou elemento de matriz)](#indexer-operator-): para acessar um elemento de matriz ou um indexador de tipo</span><span class="sxs-lookup"><span data-stu-id="bf363-106">[`[]` (array element or indexer access)](#indexer-operator-): to access an array element or a type indexer</span></span>
- <span data-ttu-id="bf363-107">[`?.` e `?[]` (operadores condicionais nulos)](#null-conditional-operators--and-): para executar uma operação de acesso a membro ou elemento somente se um operando for não nulo</span><span class="sxs-lookup"><span data-stu-id="bf363-107">[`?.` and `?[]` (null-conditional operators)](#null-conditional-operators--and-): to perform a member or element access operation only if an operand is non-null</span></span>
- <span data-ttu-id="bf363-108">[`()` (invocação)](#invocation-operator-): chamar um método acessado ou invocar um delegado</span><span class="sxs-lookup"><span data-stu-id="bf363-108">[`()` (invocation)](#invocation-operator-): to call an accessed method or invoke a delegate</span></span>

## <a name="member-access-operator-"></a><span data-ttu-id="bf363-109">Operador de acesso a membro.</span><span class="sxs-lookup"><span data-stu-id="bf363-109">Member access operator .</span></span>

<span data-ttu-id="bf363-110">Use o token `.` para acessar um membro de um namespace ou um tipo, como demonstram os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf363-110">You use the `.` token to access a member of a namespace or a type, as the following examples demonstrate:</span></span>

- <span data-ttu-id="bf363-111">Use `.` para acessar um namespace aninhado dentro de um namespace, como mostra o exemplo a seguir de uma [diretiva `using`](../keywords/using-directive.md):</span><span class="sxs-lookup"><span data-stu-id="bf363-111">Use `.` to access a nested namespace within a namespace, as the following example of a [`using` directive](../keywords/using-directive.md) shows:</span></span>

  [!code-csharp[nested namespaces](~/samples/snippets/csharp/language-reference/operators/MemberAccessOperators.cs#NestedNamespace)]

- <span data-ttu-id="bf363-112">Use `.` para formar um *nome qualificado* para acessar um tipo dentro de um namespace, como mostra o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf363-112">Use `.` to form a *qualified name* to access a type within a namespace, as the following code shows:</span></span>

  [!code-csharp[qualified name](~/samples/snippets/csharp/language-reference/operators/MemberAccessOperators.cs#QualifiedName)]

  <span data-ttu-id="bf363-113">Use uma [diretiva `using`](../keywords/using-directive.md) para tornar o uso de nomes qualificados opcional.</span><span class="sxs-lookup"><span data-stu-id="bf363-113">Use a [`using` directive](../keywords/using-directive.md) to make the use of qualified names optional.</span></span>

- <span data-ttu-id="bf363-114">Use `.` para acessar [membros de tipo](../../programming-guide/classes-and-structs/index.md#members), estático e não-estático, como mostra o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf363-114">Use `.` to access [type members](../../programming-guide/classes-and-structs/index.md#members), static and non-static, as the following code shows:</span></span>

  [!code-csharp-interactive[type members](~/samples/snippets/csharp/language-reference/operators/MemberAccessOperators.cs#TypeMemberAccess)]

<span data-ttu-id="bf363-115">Você também pode usar `.` para acessar um [método de extensão](../../programming-guide/classes-and-structs/extension-methods.md).</span><span class="sxs-lookup"><span data-stu-id="bf363-115">You can also use `.` to access an [extension method](../../programming-guide/classes-and-structs/extension-methods.md).</span></span>

## <a name="indexer-operator-"></a><span data-ttu-id="bf363-116">Operador de indexador []</span><span class="sxs-lookup"><span data-stu-id="bf363-116">Indexer operator []</span></span>

<span data-ttu-id="bf363-117">Os colchetes, `[]`, normalmente são usados para acesso de elemento de matriz, indexador ou ponteiro.</span><span class="sxs-lookup"><span data-stu-id="bf363-117">Square brackets, `[]`, are typically used for array, indexer, or pointer element access.</span></span>

### <a name="array-access"></a><span data-ttu-id="bf363-118">Acesso de matriz</span><span class="sxs-lookup"><span data-stu-id="bf363-118">Array access</span></span>

<span data-ttu-id="bf363-119">O exemplo a seguir demonstra como acessar elementos de matriz:</span><span class="sxs-lookup"><span data-stu-id="bf363-119">The following example demonstrates how to access array elements:</span></span>

[!code-csharp-interactive[array access](~/samples/snippets/csharp/language-reference/operators/MemberAccessOperators.cs#Arrays)]

<span data-ttu-id="bf363-120">Se um índice de matriz estiver fora dos limites da dimensão correspondente de uma matriz, uma <xref:System.IndexOutOfRangeException> será gerada.</span><span class="sxs-lookup"><span data-stu-id="bf363-120">If an array index is outside the bounds of the corresponding dimension of an array, an <xref:System.IndexOutOfRangeException> is thrown.</span></span>

<span data-ttu-id="bf363-121">Como mostra o exemplo anterior, você também usar colchetes quando declara um tipo de matriz ou instancia uma instância de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf363-121">As the preceding example shows, you also use square brackets when you declare an array type or instantiate an array instance.</span></span>

<span data-ttu-id="bf363-122">Para obter mais informações sobre matrizes, confira [Matrizes](../../programming-guide/arrays/index.md).</span><span class="sxs-lookup"><span data-stu-id="bf363-122">For more information about arrays, see [Arrays](../../programming-guide/arrays/index.md).</span></span>

### <a name="indexer-access"></a><span data-ttu-id="bf363-123">Acesso de indexador</span><span class="sxs-lookup"><span data-stu-id="bf363-123">Indexer access</span></span>

<span data-ttu-id="bf363-124">O exemplo a seguir usa o tipo <xref:System.Collections.Generic.Dictionary%602> do .NET para demonstrar o acesso de indexador:</span><span class="sxs-lookup"><span data-stu-id="bf363-124">The following example uses .NET <xref:System.Collections.Generic.Dictionary%602> type to demonstrate indexer access:</span></span>

[!code-csharp-interactive[indexer access](~/samples/snippets/csharp/language-reference/operators/MemberAccessOperators.cs#Indexers)]

<span data-ttu-id="bf363-125">Os indexadores permitem indexar instâncias de um tipo definido pelo usuário de maneira semelhante à indexação de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf363-125">Indexers allow you to index instances of a user-defined type in the similar way as array indexing.</span></span> <span data-ttu-id="bf363-126">Ao contrário dos índices da matriz, que precisam ser um inteiro, os argumentos do indexador podem ser declarados como qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="bf363-126">Unlike array indices, which must be integer, the indexer arguments can be declared to be of any type.</span></span>

<span data-ttu-id="bf363-127">Para obter mais informações sobre indexadores, confira [Indexadores](../../programming-guide/indexers/index.md).</span><span class="sxs-lookup"><span data-stu-id="bf363-127">For more information about indexers, see [Indexers](../../programming-guide/indexers/index.md).</span></span>

### <a name="other-usages-of-"></a><span data-ttu-id="bf363-128">Outros usos de []</span><span class="sxs-lookup"><span data-stu-id="bf363-128">Other usages of []</span></span>

<span data-ttu-id="bf363-129">Para obter informações sobre o acesso de elemento de ponteiro, veja [Como acessar um elemento de matriz com um ponteiro](../../programming-guide/unsafe-code-pointers/how-to-access-an-array-element-with-a-pointer.md).</span><span class="sxs-lookup"><span data-stu-id="bf363-129">For information about pointer element access, see [How to: access an array element with a pointer](../../programming-guide/unsafe-code-pointers/how-to-access-an-array-element-with-a-pointer.md).</span></span>

<span data-ttu-id="bf363-130">Os colchetes também são usados para especificar [atributos](../../programming-guide/concepts/attributes/index.md):</span><span class="sxs-lookup"><span data-stu-id="bf363-130">You also use square brackets to specify [attributes](../../programming-guide/concepts/attributes/index.md):</span></span>

```csharp
[System.Diagnostics.Conditional("DEBUG")]
void TraceMethod() {}
```

## <a name="null-conditional-operators--and-"></a><span data-ttu-id="bf363-131">Operadores condicionais nulos ?.</span><span class="sxs-lookup"><span data-stu-id="bf363-131">Null-conditional operators ?.</span></span> <span data-ttu-id="bf363-132">e ?[]</span><span class="sxs-lookup"><span data-stu-id="bf363-132">and ?[]</span></span>

<span data-ttu-id="bf363-133">Disponível no C# 6 e versões posteriores, um operador nulo condicional aplicará a seu operando uma operação de acesso a membro, `?.`, ou de acesso a elemento, `?[]`, somente se o operando for avaliado como não nulo.</span><span class="sxs-lookup"><span data-stu-id="bf363-133">Available in C# 6 and later, a null-conditional operator applies a member access, `?.`, or element access, `?[]`, operation to its operand only if that operand evaluates to non-null.</span></span> <span data-ttu-id="bf363-134">Se o operando for avaliado como `null`, o resultado da aplicação do operador será `null`.</span><span class="sxs-lookup"><span data-stu-id="bf363-134">If the operand evaluates to `null`, the result of applying the operator is `null`.</span></span>

<span data-ttu-id="bf363-135">Os operadores condicionais nulos estão entrando em curto-circuito.</span><span class="sxs-lookup"><span data-stu-id="bf363-135">The null-conditional operators are short-circuiting.</span></span> <span data-ttu-id="bf363-136">Ou seja, se uma operação em uma cadeia de membro operações condicionais de acesso a membro ou elemento retornar `null`, o restante da cadeia não será executado.</span><span class="sxs-lookup"><span data-stu-id="bf363-136">That is, if one operation in a chain of conditional member or element access operations returns `null`, the rest of the chain doesn't execute.</span></span> <span data-ttu-id="bf363-137">No exemplo a seguir, `B` não será avaliado se `A` for avaliado como `null` e `C` não será avaliado se `A` ou `B` for avaliado como `null`:</span><span class="sxs-lookup"><span data-stu-id="bf363-137">In the following example, `B` is not evaluated if `A` evaluates to `null` and `C` is not evaluated if `A` or `B` evaluates to `null`:</span></span>

```csharp
A?.B?.Do(C);
A?.B?[C];
```

<span data-ttu-id="bf363-138">O exemplo a seguir demonstra o uso dos operadores `?.` e `?[]`:</span><span class="sxs-lookup"><span data-stu-id="bf363-138">The following example demonstrates the usage of the `?.` and `?[]` operators:</span></span>

[!code-csharp-interactive[null-conditional operators](~/samples/snippets/csharp/language-reference/operators/MemberAccessOperators.cs#NullConditional)]

<span data-ttu-id="bf363-139">O exemplo anterior também mostra o uso do [operador de coalescência nula](null-coalescing-operator.md).</span><span class="sxs-lookup"><span data-stu-id="bf363-139">The preceding example also shows the usage of the [null-coalescing operator](null-coalescing-operator.md).</span></span> <span data-ttu-id="bf363-140">Você pode usar o operador de coalescência nula para fornecer uma expressão alternativa a avaliar caso o resultado da operação condicional nula seja `null`.</span><span class="sxs-lookup"><span data-stu-id="bf363-140">You might use the null-coalescing operator to provide an alternative expression to evaluate in case the result of the null-conditional operation is `null`.</span></span>

### <a name="thread-safe-delegate-invocation"></a><span data-ttu-id="bf363-141">Invocação de delegado thread-safe</span><span class="sxs-lookup"><span data-stu-id="bf363-141">Thread-safe delegate invocation</span></span>

<span data-ttu-id="bf363-142">Use o operador `?.` para verificar se um delegado é não nulo e chame-o de uma forma thread-safe (por exemplo, quando você [aciona um evento](../../../standard/events/how-to-raise-and-consume-events.md)), conforme mostrado no código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf363-142">Use the `?.` operator to check if a delegate is non-null and invoke it in a thread-safe way (for example, when you [raise an event](../../../standard/events/how-to-raise-and-consume-events.md)), as the following code shows:</span></span>

```csharp
PropertyChanged?.Invoke(…)
```

<span data-ttu-id="bf363-143">Esse código é equivalente ao código a seguir que você usaria no C# 5 ou anterior:</span><span class="sxs-lookup"><span data-stu-id="bf363-143">That code is equivalent to the following code that you would use in C# 5 or earlier:</span></span>

```csharp
var handler = this.PropertyChanged;
if (handler != null)
{
    handler(…);
}
```

## <a name="invocation-operator-"></a><span data-ttu-id="bf363-144">Operador de invocação ()</span><span class="sxs-lookup"><span data-stu-id="bf363-144">Invocation operator ()</span></span>

<span data-ttu-id="bf363-145">Use parênteses, `()`, para chamar um [método](../../programming-guide/classes-and-structs/methods.md) ou invocar um [delegado](../../programming-guide/delegates/index.md).</span><span class="sxs-lookup"><span data-stu-id="bf363-145">Use parentheses, `()`, to call a [method](../../programming-guide/classes-and-structs/methods.md) or invoke a [delegate](../../programming-guide/delegates/index.md).</span></span>

<span data-ttu-id="bf363-146">O exemplo a seguir demonstra como chamar um método (com ou sem argumentos) e invocar um delegado:</span><span class="sxs-lookup"><span data-stu-id="bf363-146">The following example demonstrates how to call a method, with or without arguments, and invoke a delegate:</span></span>

[!code-csharp-interactive[invocation with ()](~/samples/snippets/csharp/language-reference/operators/MemberAccessOperators.cs#Invocation)]

<span data-ttu-id="bf363-147">Você também pode usar parênteses ao invocar um [construtor](../../programming-guide/classes-and-structs/constructors.md) com um operador [`new`](../keywords/new-operator.md).</span><span class="sxs-lookup"><span data-stu-id="bf363-147">You also use parentheses when you invoke a [constructor](../../programming-guide/classes-and-structs/constructors.md) with a [`new`](../keywords/new-operator.md) operator.</span></span>

### <a name="other-usages-of-"></a><span data-ttu-id="bf363-148">Outros usos de ()</span><span class="sxs-lookup"><span data-stu-id="bf363-148">Other usages of ()</span></span>

<span data-ttu-id="bf363-149">Você também pode usar parênteses para especificar a ordem na qual as operações em uma expressão são avaliada.</span><span class="sxs-lookup"><span data-stu-id="bf363-149">You also use parentheses to specify the order in which to evaluate operations in an expression.</span></span> <span data-ttu-id="bf363-150">Para obter mais informações, confira a seção [Adicionando parênteses](../../programming-guide/statements-expressions-operators/operators.md#adding-parentheses) o artigo [Operadores](../../programming-guide/statements-expressions-operators/operators.md).</span><span class="sxs-lookup"><span data-stu-id="bf363-150">For more information, see the [Adding parentheses](../../programming-guide/statements-expressions-operators/operators.md#adding-parentheses) section of the [Operators](../../programming-guide/statements-expressions-operators/operators.md) article.</span></span> <span data-ttu-id="bf363-151">Para obter a lista de operadores ordenada pelo nível de precedência, confira [Operadores do C#](index.md).</span><span class="sxs-lookup"><span data-stu-id="bf363-151">For the list of operators ordered by precedence level, see [C# operators](index.md).</span></span>

<span data-ttu-id="bf363-152">[Expressões de conversão](invocation-operator.md#cast-expression), que invocam um operador de conversão, também usam parênteses.</span><span class="sxs-lookup"><span data-stu-id="bf363-152">[Cast expressions](invocation-operator.md#cast-expression), which invoke a conversion operator, also use parentheses.</span></span>

## <a name="operator-overloadability"></a><span data-ttu-id="bf363-153">Capacidade de sobrecarga do operador</span><span class="sxs-lookup"><span data-stu-id="bf363-153">Operator overloadability</span></span>

<span data-ttu-id="bf363-154">Os operadores `.` e `()` não podem ser sobrecarregados.</span><span class="sxs-lookup"><span data-stu-id="bf363-154">The `.` and `()` operators cannot be overloaded.</span></span> <span data-ttu-id="bf363-155">O operador `[]` também é considerado um operador não sobrecarregável.</span><span class="sxs-lookup"><span data-stu-id="bf363-155">The `[]` operator is also considered a non-overloadable operator.</span></span> <span data-ttu-id="bf363-156">Use [indexadores](../../programming-guide/indexers/index.md) para permitir a indexação com tipos definidos pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="bf363-156">Use [indexers](../../programming-guide/indexers/index.md) to support indexing with user-defined types.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="bf363-157">Especificação da linguagem C#</span><span class="sxs-lookup"><span data-stu-id="bf363-157">C# language specification</span></span>

<span data-ttu-id="bf363-158">Para obter mais informações, confira as seguintes seções da [especificação da linguagem C#](~/_csharplang/spec/introduction.md):</span><span class="sxs-lookup"><span data-stu-id="bf363-158">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="bf363-159">Acesso de membros</span><span class="sxs-lookup"><span data-stu-id="bf363-159">Member access</span></span>](~/_csharplang/spec/expressions.md#member-access)
- [<span data-ttu-id="bf363-160">Acesso a elemento</span><span class="sxs-lookup"><span data-stu-id="bf363-160">Element access</span></span>](~/_csharplang/spec/expressions.md#element-access)
- [<span data-ttu-id="bf363-161">Operador condicional nulo</span><span class="sxs-lookup"><span data-stu-id="bf363-161">Null-conditional operator</span></span>](~/_csharplang/spec/expressions.md#null-conditional-operator)
- [<span data-ttu-id="bf363-162">Expressões de invocação</span><span class="sxs-lookup"><span data-stu-id="bf363-162">Invocation expressions</span></span>](~/_csharplang/spec/expressions.md#invocation-expressions)

## <a name="see-also"></a><span data-ttu-id="bf363-163">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bf363-163">See also</span></span>

- [<span data-ttu-id="bf363-164">Referência de C#</span><span class="sxs-lookup"><span data-stu-id="bf363-164">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="bf363-165">Guia de Programação em C#</span><span class="sxs-lookup"><span data-stu-id="bf363-165">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="bf363-166">Operadores do C#</span><span class="sxs-lookup"><span data-stu-id="bf363-166">C# Operators</span></span>](index.md)
- [<span data-ttu-id="bf363-167">?? (operador de união nula)</span><span class="sxs-lookup"><span data-stu-id="bf363-167">?? (null-coalescing operator)</span></span>](null-coalescing-operator.md)