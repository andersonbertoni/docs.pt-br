---
title: Matrizes
description: Saiba como criar e usar matrizes na linguagem F# de programação.
ms.date: 05/16/2016
ms.openlocfilehash: 142d2c8d9aa7247e1490867a7bb905e2e7fec41e
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630045"
---
# <a name="arrays"></a>Matrizes

> [!NOTE]
> O link de referência da API levará você até o MSDN.  A referência da API docs.microsoft.com não está completa.

As matrizes são coleções de tamanho fixo, com base em zero e mutáveis de elementos de dados consecutivos que são do mesmo tipo.

## <a name="creating-arrays"></a>Criando matrizes

Você pode criar matrizes de várias maneiras. Você pode criar uma pequena matriz listando valores consecutivos `[|` entre `|]` e e separados por ponto e vírgula, conforme mostrado nos exemplos a seguir.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet1.fs)]

Você também pode colocar cada elemento em uma linha separada; nesse caso, o separador de ponto-e-vírgula é opcional.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet2.fs)]

O tipo dos elementos da matriz é inferido a partir dos literais usados e deve ser consistente. O código a seguir causa um erro porque 1,0 é um float e 2 e 3 são inteiros.

```fsharp
// Causes an error.
// let array2 = [| 1.0; 2; 3 |]
```

Você também pode usar expressões de sequência para criar matrizes. Veja a seguir um exemplo que cria uma matriz de quadrados de inteiros de 1 a 10.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet3.fs)]

Para criar uma matriz na qual todos os elementos são inicializados como zero, `Array.zeroCreate`use.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet4.fs)]

## <a name="accessing-elements"></a>Acessando elementos

Você pode acessar elementos de matriz usando um operador de ponto`.`() e colchetes`[` ( `]`e).

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet5.fs)]

Os índices de matriz começam em 0.

Você também pode acessar elementos de matriz usando a notação de fatia, que permite especificar um subintervalo da matriz. Seguem exemplos de notação de fatia.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet51.fs)]

Quando a notação de fatia é usada, uma nova cópia da matriz é criada.

## <a name="array-types-and-modules"></a>Módulos e tipos de matriz

O tipo de todas F# as matrizes é o <xref:System.Array?displayProperty=nameWithType>tipo de .NET Framework. Portanto, F# as matrizes oferecem suporte a todas <xref:System.Array?displayProperty=nameWithType>as funcionalidades disponíveis no.

O módulo [`Microsoft.FSharp.Collections.Array`](https://msdn.microsoft.com/library/0cda8040-9396-40dd-8dcd-cf48542165a1) de biblioteca dá suporte a operações em matrizes unidimensionais. Os módulos `Array2D`, `Array3D`e `Array4D` contêm funções que dão suporte a operações em matrizes de duas, três e quatro dimensões, respectivamente. Você pode criar matrizes de classificação maior que quatro usando <xref:System.Array?displayProperty=nameWithType>.

### <a name="simple-functions"></a>Funções simples

[`Array.get`](https://msdn.microsoft.com/library/dd93e85d-7e80-4d76-8de0-b6d45bcf07bc)Obtém um elemento. [`Array.length`](https://msdn.microsoft.com/library/0d775b6a-4a8f-4bd1-83e5-843b3251725f)fornece o comprimento de uma matriz. [`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790)define um elemento para um valor especificado. O exemplo de código a seguir ilustra o uso dessas funções.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet9.fs)]

A saída é a seguinte.

```
0 1 2 3 4 5 6 7 8 9
```

### <a name="functions-that-create-arrays"></a>Funções que criam matrizes

Várias funções criam matrizes sem a necessidade de uma matriz existente. [`Array.empty`](https://msdn.microsoft.com/library/c3694b92-1c16-4c54-9bf2-fe398fadce32)Cria uma nova matriz que não contém nenhum elemento. [`Array.create`](https://msdn.microsoft.com/library/e848c8d6-1142-4080-9727-8dacc26066be)Cria uma matriz de um tamanho especificado e define todos os elementos para os valores fornecidos. [`Array.init`](https://msdn.microsoft.com/library/ee898089-63b0-40aa-910c-5ae7e32f6665)Cria uma matriz, dada uma dimensão e uma função para gerar os elementos. [`Array.zeroCreate`](https://msdn.microsoft.com/library/fa5b8e7a-1b5b-411c-8622-b58d7a14d3b2)Cria uma matriz na qual todos os elementos são inicializados com o valor zero para o tipo da matriz. O código a seguir demonstra essas funções.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet91.fs)]

A saída é a seguinte.

```
Length of empty array: 0
Area of floats set to 5.0: [|5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0|]
Array of squares: [|0; 1; 4; 9; 16; 25; 36; 49; 64; 81|]
```

[`Array.copy`](https://msdn.microsoft.com/library/9d0202f1-1ea0-475e-9d66-4f8ccc3c5b5f)Cria uma nova matriz que contém elementos que são copiados de uma matriz existente. Observe que a cópia é uma cópia superficial, o que significa que se o tipo de elemento for um tipo de referência, somente a referência será copiada, não o objeto subjacente. O exemplo de código a seguir ilustra isso.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet11.fs)]

A saída do código anterior é a seguinte:

```
[|Test1; Test2; |]
[|; Test2; |]
```

A cadeia `Test1` de caracteres aparece apenas na primeira matriz porque a operação de criação de um novo elemento substitui a referência em `firstArray` , mas não afeta a referência original a uma cadeia de caracteres vazia que ainda está `secondArray`presente no. A cadeia `Test2` de caracteres aparece em ambas as `Insert` matrizes porque <xref:System.Text.StringBuilder?displayProperty=nameWithType> a operação no tipo <xref:System.Text.StringBuilder?displayProperty=nameWithType> afeta o objeto subjacente, que é referenciado em ambas as matrizes.

[`Array.sub`](https://msdn.microsoft.com/library/40fb12ba-41d7-4ef0-b33a-56727deeef9d)gera uma nova matriz de um subintervalo de uma matriz. Você especifica o subintervalo fornecendo o índice inicial e o comprimento. O código a seguir demonstra o uso de `Array.sub`.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet12.fs)]

A saída mostra que a submatriz começa no elemento 5 e contém 10 elementos.

```
[|5; 6; 7; 8; 9; 10; 11; 12; 13; 14|]
```

[`Array.append`](https://msdn.microsoft.com/library/08836310-5036-4474-b9a2-2c73e2293911)Cria uma nova matriz combinando duas matrizes existentes.

O código a seguir demonstra o **array. Append**.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet13.fs)]

A saída do código anterior é a seguinte.

```
[|1; 2; 3; 4; 5; 6|]
```

[`Array.choose`](https://msdn.microsoft.com/library/f5c8a5e2-637f-44d4-b35c-be96a6618b09)seleciona os elementos de uma matriz para incluir em uma nova matriz. O código a seguir `Array.choose`demonstra. Observe que o tipo de elemento da matriz não precisa corresponder ao tipo de valor retornado no tipo de opção. Neste exemplo, o tipo de elemento é `int` e a opção é o resultado de uma função polinomial `elem*elem - 1`,, como um número de ponto flutuante.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet14.fs)]

A saída do código anterior é a seguinte.

```
[|3.0; 15.0; 35.0; 63.0; 99.0|]
```

[`Array.collect`](https://msdn.microsoft.com/library/c3b60c3b-9455-48c9-bc2b-e88f0434342a)executa uma função especificada em cada elemento da matriz de uma matriz existente e, em seguida, coleta os elementos gerados pela função e os combina em uma nova matriz. O código a seguir `Array.collect`demonstra.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet15.fs)]

A saída do código anterior é a seguinte.

```
[|0; 1; 0; 1; 2; 3; 4; 5; 0; 1; 2; 3; 4; 5; 6; 7; 8; 9; 10|]
```

[`Array.concat`](https://msdn.microsoft.com/library/f7219b79-1ec8-4a25-96b1-edbedb358302)usa uma sequência de matrizes e as combina em uma única matriz. O código a seguir `Array.concat`demonstra.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet16.fs)]

A saída do código anterior é a seguinte.

```
[|(1, 1, 1); (1, 2, 2); (1, 3, 3); (2, 1, 2); (2, 2, 4); (2, 3, 6); (3, 1, 3);
(3, 2, 6); (3, 3, 9)|]
```

[`Array.filter`](https://msdn.microsoft.com/library/b885b214-47fc-4639-9664-b8c183a39ede)usa uma função de condição booliana e gera uma nova matriz que contém somente os elementos da matriz de entrada para a qual a condição é verdadeira. O código a seguir `Array.filter`demonstra.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet17.fs)]

A saída do código anterior é a seguinte.

```
[|2; 4; 6; 8; 10|]
```

[`Array.rev`](https://msdn.microsoft.com/library/1bbf822c-763b-4794-af21-97d2e48ef709)gera uma nova matriz revertendo a ordem de uma matriz existente. O código a seguir `Array.rev`demonstra.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet18.fs)]

A saída do código anterior é a seguinte.

```
"Hello world!"
```

Você pode combinar facilmente funções no módulo de matriz que transformam matrizes usando o operador`|>`de pipeline (), conforme mostrado no exemplo a seguir.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet19.fs)]

A saída é

```
[|100; 36; 16; 4|]
```

### <a name="multidimensional-arrays"></a>Matrizes multidimensionais

Uma matriz multidimensional pode ser criada, mas não há nenhuma sintaxe para gravar um literal de matriz multidimensional. Use o operador [`array2D`](https://msdn.microsoft.com/library/1d52503d-2990-49fc-8fd3-6b0e508aa236) para criar uma matriz de uma sequência de sequências de elementos de matriz. As sequências podem ser literais de matriz ou lista. Por exemplo, o código a seguir cria uma matriz bidimensional.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet20.fs)]

Você também pode usar a função [`Array2D.init`](https://msdn.microsoft.com/library/9de07e95-bc21-4927-b5b4-08fdec882c7b) para inicializar matrizes de duas dimensões e funções semelhantes estão disponíveis para matrizes de três e quatro dimensões. Essas funções usam uma função que é usada para criar os elementos. Para criar uma matriz bidimensional que contém elementos definidos como um valor inicial em vez de especificar uma função, use [`Array2D.create`](https://msdn.microsoft.com/library/36c9d980-b241-4a20-bc64-bcfa0205d804) a função, que também está disponível para matrizes de até quatro dimensões. O exemplo de código a seguir mostra primeiro como criar uma matriz de matrizes que contêm os elementos desejados `Array2D.init` e, em seguida, usa para gerar a matriz bidimensional desejada.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet21.fs)]

A indexação de matriz e a sintaxe de divisão têm suporte para matrizes até a classificação 4. Quando você especifica um índice em várias dimensões, usa vírgulas para separar os índices, conforme ilustrado no exemplo de código a seguir.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet22.fs)]

O tipo de uma matriz bidimensional é `<type>[,]` escrito como (por exemplo `double[,]`, `int[,]`), e o tipo de uma matriz tridimensional é escrito como `<type>[,,]`e assim por diante para matrizes de dimensões superiores.

Somente um subconjunto das funções disponíveis para matrizes unidimensionais também está disponível para matrizes multidimensionais. Para obter mais informações, [`Collections.Array Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array-module-%5bfsharp%5d)consulte [`Collections.Array2D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array2d-module-%5bfsharp%5d) [`Collections.Array3D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array3d-module-%5bfsharp%5d),, e [`Collections.Array4D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array4d-module-%5bfsharp%5d).

### <a name="array-slicing-and-multidimensional-arrays"></a>Fatias de matrizes e matrizes multidimensionais

Em uma matriz bidimensional (uma matriz), você pode extrair uma submatriz especificando intervalos e usando um caractere curinga (`*`) para especificar linhas ou colunas inteiras.

```fsharp
// Get rows 1 to N from an NxM matrix (returns a matrix):
matrix.[1.., *]

// Get rows 1 to 3 from a matrix (returns a matrix):
matrix.[1..3, *]

// Get columns 1 to 3 from a matrix (returns a matrix):
matrix.[*, 1..3]

// Get a 3x3 submatrix:
matrix.[1..3, 1..3]
```

A partir F# de 3,1, você pode decompor uma matriz multidimensional em subconjuntos da mesma dimensão ou menor. Por exemplo, você pode obter um vetor de uma matriz especificando uma única linha ou coluna.

```fsharp
// Get row 3 from a matrix as a vector:
matrix.[3, *]

// Get column 3 from a matrix as a vector:
matrix.[*, 3]
```

Você pode usar essa sintaxe de divisão para tipos que implementam os operadores de acesso do elemento e `GetSlice` os métodos sobrecarregados. Por exemplo, o código a seguir cria um tipo de matriz que encapsula F# a matriz 2D, implementa uma propriedade item para fornecer suporte para indexação de matriz e implementa três versões `GetSlice`do. Se você puder usar esse código como um modelo para os tipos de matriz, poderá usar todas as operações de divisão que esta seção descreve.

```fsharp
type Matrix<'T>(N: int, M: int) =
    let internalArray = Array2D.zeroCreate<'T> N M

    member this.Item
        with get(a: int, b: int) = internalArray.[a, b]
        and set(a: int, b: int) (value:'T) = internalArray.[a, b] <- value

    member this.GetSlice(rowStart: int option, rowFinish : int option, colStart: int option, colFinish : int option) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[rowStart..rowFinish, colStart..colFinish]

    member this.GetSlice(row: int, colStart: int option, colFinish: int option) =
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[row, colStart..colFinish]

    member this.GetSlice(rowStart: int option, rowFinish: int option, col: int) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        internalArray.[rowStart..rowFinish, col]

module test =
    let generateTestMatrix x y =
        let matrix = new Matrix<float>(3, 3)
        for i in 0..2 do
            for j in 0..2 do
                matrix.[i, j] <- float(i) * x - float(j) * y
        matrix

    let test1 = generateTestMatrix 2.3 1.1
    let submatrix = test1.[0..1, 0..1]
    printfn "%A" submatrix

    let firstRow = test1.[0,*]
    let secondRow = test1.[1,*]
    let firstCol = test1.[*,0]
    printfn "%A" firstCol
```

### <a name="boolean-functions-on-arrays"></a>Funções booleanas em matrizes

As funções [`Array.exists`](https://msdn.microsoft.com/library/8e47ad6c-c065-4876-8cb4-ec960ec3e5c9) e [`Array.exists2`](https://msdn.microsoft.com/library/2e384a6a-f99d-4e23-b677-250ffbc1dd8e) os elementos de teste em uma ou duas matrizes, respectivamente. Essas funções usam uma função de teste e `true` retornam se há um elemento (ou par de `Array.exists2`elementos para) que satisfaça a condição.

O código a seguir demonstra o uso `Array.exists` de `Array.exists2`e. Nesses exemplos, novas funções são criadas aplicando-se apenas um dos argumentos, nesses casos, o argumento da função.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet23.fs)]

A saída do código anterior é a seguinte.

```
true
false
false
true
```

Da mesma forma, [`Array.forall`](https://msdn.microsoft.com/library/d88f2cd0-fa7f-45cf-ac15-31eae9086cc4) a função testa uma matriz para determinar se cada elemento atende a uma condição booliana. A variação [`Array.forall2`](https://msdn.microsoft.com/library/c68f61a1-030c-4024-b705-c4768b6c96b9) faz a mesma coisa usando uma função booleana que envolve elementos de duas matrizes de comprimento igual. O código a seguir ilustra o uso dessas funções.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet24.fs)]

A saída desses exemplos é a seguinte.

```
false
true
true
false
```

### <a name="searching-arrays"></a>Pesquisando matrizes

[`Array.find`](https://msdn.microsoft.com/library/db6d920a-de19-4520-85a4-d83de77c1b33)usa uma função booliana e retorna o primeiro elemento para o qual a `true`função retorna, ou <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> gera um elemento If nenhum que satisfaça a condição é encontrado. [`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f)é como `Array.find`, exceto pelo fato de que ele retorna o índice do elemento em vez do próprio elemento.

O código a seguir `Array.find` usa `Array.findIndex` e para localizar um número que seja um cubo perfeito e um quadrado perfeitos.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet25.fs)]

A saída é a seguinte.

```
The first element that is both a square and a cube is 64 and its index is 62.
```

[`Array.tryFind`](https://msdn.microsoft.com/library/7bd65f6c-df77-454c-ac3a-6f7baecec9d9)é como `Array.find`, exceto que seu resultado é um tipo de opção e retorna `None` se nenhum elemento for encontrado. `Array.tryFind`deve ser usado em vez `Array.find` de quando você não sabe se um elemento correspondente está na matriz. Da mesma [`Array.tryFindIndex`](https://msdn.microsoft.com/library/da82f7fe-95e9-4fd5-a924-cd3c9d10618a) forma, [`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f) é como, exceto que o tipo de opção é o valor de retorno. Se nenhum elemento for encontrado, a opção será `None`.

O código a seguir demonstra o uso de `Array.tryFind`. Esse código depende do código anterior.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet26.fs)]

A saída é a seguinte.

```
Found an element: 1
Found an element: 729
```

Use [`Array.tryPick`](https://msdn.microsoft.com/library/72d45f85-037b-43a9-97fd-17239f72713e) quando precisar transformar um elemento, além de localizá-lo. O resultado é o primeiro elemento para o qual a função retorna o elemento transformado como um valor `None` de opção ou se nenhum elemento desse tipo é encontrado.

O código a seguir demonstra o uso de `Array.tryPick`. Nesse caso, em vez de uma expressão lambda, várias funções auxiliares locais são definidas para simplificar o código.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet27.fs)]

A saída é a seguinte.

```
Found an element 1 with square root 1 and cube root 1.
Found an element 64 with square root 8 and cube root 4.
Found an element 729 with square root 27 and cube root 9.
Found an element 4096 with square root 64 and cube root 16.
```

### <a name="performing-computations-on-arrays"></a>Executando cálculos em matrizes

A [`Array.average`](https://msdn.microsoft.com/library/7029f2b9-91ea-41cb-be1b-466a5a0db20e) função retorna a média de cada elemento em uma matriz. Ele é limitado a tipos de elementos que dão suporte à divisão exata por um inteiro, que inclui tipos de ponto flutuante, mas não tipos integrais. A [`Array.averageBy`](https://msdn.microsoft.com/library/e9d64609-06a3-48f0-bc07-226ab0f85c54) função retorna a média dos resultados da chamada de uma função em cada elemento. Para uma matriz de tipo integral, você pode usar `Array.averageBy` e fazer com que a função Converta cada elemento em um tipo de ponto flutuante para a computação.

Use [`Array.max`](https://msdn.microsoft.com/library/f03fbda0-fce6-40e2-a85d-79c9d81f710b) [ou`Array.min`](https://msdn.microsoft.com/library/d6b3da5f-bac0-4355-9846-4b72d95bc3fd) para obter o elemento máximo ou mínimo, se o tipo de elemento oferecer suporte a ele. Da mesma [`Array.maxBy`](https://msdn.microsoft.com/library/18dbe7c5-482e-4766-8e01-12a76f847045) forma [`Array.minBy`](https://msdn.microsoft.com/library/24091583-be78-4cc9-9fab-de6d7506af4f) , e permite que uma função seja executada primeiro, talvez para transformar em um tipo que dê suporte à comparação.

[`Array.sum`](https://msdn.microsoft.com/library/4ffdb8c8-cd94-4b0b-9e5c-a7c9c17963c2)Adiciona os elementos de uma matriz e [`Array.sumBy`](https://msdn.microsoft.com/library/41698ba6-1adc-4169-8cc5-7a0e3f8de56b) chama uma função em cada elemento e adiciona os resultados juntos.

Para executar uma função em cada elemento em uma matriz sem armazenar os valores de retorno, [`Array.iter`](https://msdn.microsoft.com/library/94eba0f1-ecd7-459f-b89f-ed2a2923e516)use. Para uma função que envolva duas matrizes de comprimento igual [`Array.iter2`](https://msdn.microsoft.com/library/018aa9b9-f186-4142-be8a-a62462794fdc), use. Se você também precisar manter uma matriz dos resultados da função, use [`Array.map`](https://msdn.microsoft.com/library/38cbe824-0480-47be-85fd-df3afdd97a45) ou [`Array.map2`](https://msdn.microsoft.com/library/bb7aafe8-4a1f-45b9-92fc-1af9eafbea5c), que opera em duas matrizes por vez.

As variações [`Array.iteri`](https://msdn.microsoft.com/library/8bbe2ed4-ada7-4906-ac3e-cb09f9db6486) e [`Array.iteri2`](https://msdn.microsoft.com/library/c041b91f-6080-45b7-867b-2ed983a90405) permitem que o índice do elemento esteja envolvido na computação; o mesmo é verdadeiro para [`Array.mapi`](https://msdn.microsoft.com/library/f7e45994-b0a1-49e6-8fb5-5641cea8fde4) e [`Array.mapi2`](https://msdn.microsoft.com/library/5edb33d2-47da-44e1-9290-40c00c47d5b0).

As funções [`Array.fold`](https://msdn.microsoft.com/library/5ed9dd3b-3694-4567-94d0-fd9a24474e09), [`Array.foldBack`](https://msdn.microsoft.com/library/1121a453-dead-4711-a0ca-cc147752989c), [`Array.reduce`](https://msdn.microsoft.com/library/fd62a985-89fe-4f49-a9d4-0c808ac6749d), [`Array.reduceBack`](https://msdn.microsoft.com/library/4fdd4cbe-2238-4c5c-b286-597a7e9036f9) [,e`Array.scanBack`](https://msdn.microsoft.com/library/7610f406-7a5c-41db-a0ca-8e2a2a4826ad) executam algoritmos que envolvem todos os elementos de uma matriz. [`Array.scan`](https://msdn.microsoft.com/library/f6893608-9146-450d-9ebb-a0016803fbb0) Da mesma forma, [`Array.fold2`](https://msdn.microsoft.com/library/5c845087-d041-476e-8cc4-53ae6849ef79) as [`Array.foldBack2`](https://msdn.microsoft.com/library/aa51b405-df20-4c51-9998-a6530f7db862) variações e executam cálculos em duas matrizes.

Essas funções para executar computações correspondem às funções de mesmo nome no módulo de [lista](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788). Para obter exemplos de uso, consulte [listas](lists.md).

### <a name="modifying-arrays"></a>Modificando matrizes

[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790)define um elemento para um valor especificado. [`Array.fill`](https://msdn.microsoft.com/library/c83c9886-81d9-44f9-a195-61c7b87f7df2)define um intervalo de elementos em uma matriz para um valor especificado. O código a seguir fornece um exemplo `Array.fill`de.

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet28.fs)]

A saída é a seguinte.

```
[|1; 2; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 23; 24; 25|]
```

Você pode usar [`Array.blit`](https://msdn.microsoft.com/library/675e13e4-7fb9-4e0d-a5be-a112830de667) para copiar uma subseção de uma matriz para outra matriz.

### <a name="converting-to-and-from-other-types"></a>Convertendo de e para outros tipos

[`Array.ofList`](https://msdn.microsoft.com/library/e7225239-f561-45a4-b0b5-69a1cdcae78b)Cria uma matriz de uma lista. [`Array.ofSeq`](https://msdn.microsoft.com/library/6bedf5e0-4b22-46da-b09c-6aa09eff220c)Cria uma matriz de uma sequência. [`Array.toList`](https://msdn.microsoft.com/library/4deff724-0be4-4688-92e7-9d67a1097786)e [`Array.toSeq`](https://msdn.microsoft.com/library/ac28dbab-406c-4fe0-ab08-c1ce5e247af4) converter para esses outros tipos de coleção do tipo de matriz.

### <a name="sorting-arrays"></a>Classificando matrizes

Use [`Array.sort`](https://msdn.microsoft.com/library/c6679075-e7eb-463c-9be5-c89be140c312) para classificar uma matriz usando a função de comparação genérica. Use [`Array.sortBy`](https://msdn.microsoft.com/library/144498dc-091d-4575-a229-c0bcbd61426b) para especificar uma função que gera um valor, chamado de *chave*, para classificar usando a função de comparação genérica na chave. Use [`Array.sortWith`](https://msdn.microsoft.com/library/699d3638-4244-4f42-8496-45f53d43ce95) se você quiser fornecer uma função de comparação personalizada. `Array.sort`, `Array.sortBy` e`Array.sortWith` todos retornam a matriz classificada como uma nova matriz. As variações [`Array.sortInPlace`](https://msdn.microsoft.com/library/36f39947-8a88-4823-9e9b-e9d838d292e0), [`Array.sortInPlaceBy`](https://msdn.microsoft.com/library/7fb9d2dd-d461-4c67-8b43-b5c59fc12c3f)e [`Array.sortInPlaceWith`](https://msdn.microsoft.com/library/454f9e11-972d-47a6-a854-8031cb0c7b0b) modificam a matriz existente em vez de retornar uma nova.

### <a name="arrays-and-tuples"></a>Matrizes e tuplas

As funções [`Array.zip`](https://msdn.microsoft.com/library/23e086b8-b266-4db2-8b68-e88e6a8e2187) e [`Array.unzip`](https://msdn.microsoft.com/library/a529b47c-2e2b-4f79-ad44-c578432d2f48) convertem matrizes de pares de tupla para tuplas de matrizes e vice-versa. [`Array.zip3`](https://msdn.microsoft.com/library/1745744a-d2ca-4c3e-b825-3f15d9f4000d)e [`Array.unzip3`](https://msdn.microsoft.com/library/bc3e6db0-f334-444f-8c30-813942880677) são semelhantes, exceto que funcionam com tuplas de três elementos ou tuplas de três matrizes.

## <a name="parallel-computations-on-arrays"></a>Cálculos paralelos em matrizes

O módulo [`Array.Parallel`](https://msdn.microsoft.com/library/60f30b77-5af4-4050-9a5c-bcdb3f5cbb09) contém funções para executar cálculos paralelos em matrizes. Este módulo não está disponível em aplicativos que visam versões do .NET Framework antes da versão 4.

## <a name="see-also"></a>Consulte também

- [Referência da Linguagem F#](index.md)
- [Tipos F#](fsharp-types.md)
