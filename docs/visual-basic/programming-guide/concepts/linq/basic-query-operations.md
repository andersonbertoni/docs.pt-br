---
title: Operações de consulta básica (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- data sources [LINQ in Visual Basic]
- Join clause [LINQ in Visual Basic]
- ordering data [LINQ in Visual Basic]
- projections [LINQ in Visual Basic]
- LINQ [Visual Basic], query operations
- Order By clause [LINQ in Visual Basic]
- joining data [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], basic operations
- selecting data [LINQ in Visual Basic]
- Group By clause [LINQ in Visual Basic]
- grouping data [LINQ in Visual Basic]
- Select clause [LINQ in Visual Basic]
ms.assetid: 1146f6d0-fcb8-4f4d-8223-c9db52620d21
ms.openlocfilehash: af99a6c22239be1f9f03bafd8323c73f83df5c51
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64642270"
---
# <a name="basic-query-operations-visual-basic"></a>Operações de consulta básica (Visual Basic)
Este tópico fornece uma breve introdução ao [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] expressões no Visual Basic e para alguns dos tipos típicos de operações que podem ser executadas em uma consulta. Para mais informações, consulte os seguintes tópicos:  
  
 [Introdução ao LINQ no Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)  
  
 [Consultas](../../../../visual-basic/language-reference/queries/index.md)  
  
 [Passo a passo: Escrevendo consultas em Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)  
  
## <a name="specifying-the-data-source-from"></a>Especificando a Fonte de Dados (De)  
 Em um [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] consulta, a primeira etapa é especificar a fonte de dados que você deseja consultar. Portanto, o `From` cláusula em uma consulta sempre vem em primeiro lugar. Operadores de consulta selecionam e formatar o resultado com base no tipo da fonte.  
  
 [!code-vb[VbLINQBasicOps#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#1)]  
  
 O `From` cláusula Especifica a fonte de dados `customers`e um *variável de intervalo*, `cust`. A variável de intervalo é como uma variável de iteração do loop, exceto que em uma expressão de consulta, nenhuma iteração real ocorre. Quando a consulta é executada, geralmente usando um `For Each` loop, a variável de intervalo serve como uma referência para cada elemento sucessivo em `customers`. Uma vez que o compilador pode inferir o tipo de `cust`, você não precisa especificá-lo explicitamente. Para obter exemplos de consultas escritas com e sem tipagem explícita, consulte [relacionamentos de tipo em operações de consulta (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md).  
  
 Para obter mais informações sobre como usar o `From` cláusula no Visual Basic, consulte [cláusula From](../../../../visual-basic/language-reference/queries/from-clause.md).  
  
## <a name="filtering-data-where"></a>Filtrando Dados (Onde)  
 Provavelmente, a operação de consulta mais comuns é aplicar um filtro na forma de uma expressão booliana. A consulta, em seguida, retorna apenas os elementos para o qual a expressão for verdadeira. Um `Where` cláusula é usada para executar a filtragem. O filtro especifica quais elementos na fonte de dados para incluir na sequência resultante. No exemplo a seguir, são incluídos somente aqueles clientes que têm um endereço em Londres.  
  
 [!code-vb[VbLINQBasicOps#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#2)]  
  
 Você pode usar operadores lógicos, como `And` e `Or` combinar expressões de filtro em um `Where` cláusula. Por exemplo, para retornar somente os clientes que são de Londres e cujo nome é Devon, use o seguinte código:  
  
```vb  
Where cust.City = "London" And cust.Name = "Devon"   
```  
  
 Para retornar os clientes de Londres ou Paris, use o seguinte código:  
  
```vb  
Where cust.City = "London" Or cust.City = "Paris"   
```  
  
 Para obter mais informações sobre como usar o `Where` cláusula no Visual Basic, consulte [cláusula Where](../../../../visual-basic/language-reference/queries/where-clause.md).  
  
## <a name="ordering-data-order-by"></a>Ordenando Dados (Ordenar Por)  
 Muitas vezes é conveniente classificar dados retornados em uma ordem específica. O `Order By` cláusula fará com que os elementos na sequência retornada deve ser classificada em um campo ou campos especificados. Por exemplo, a consulta a seguir classifica os resultados com base no `Name` propriedade. Porque `Name` é uma cadeia de caracteres, os dados retornados serão classificados em ordem alfabética, de À Z.  
  
 [!code-vb[VbLINQBasicOps#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#3)]  
  
 Para ordenar os resultados na ordem inversa, de Z para a, use a cláusula `Order By...Descending`. O padrão é `Ascending` quando nenhuma `Ascending` nem `Descending` for especificado.  
  
 Para obter mais informações sobre como usar o `Order By` cláusula no Visual Basic, consulte [cláusula Order By](../../../../visual-basic/language-reference/queries/order-by-clause.md).  
  
## <a name="selecting-data-select"></a>Selecionando Dados (Selecionar)  
 O `Select` cláusula Especifica o formato e o conteúdo de elementos retornados. Por exemplo, você pode especificar se os resultados consistirão de concluída `Customer` objetos, apenas um `Customer` propriedade, um subconjunto de propriedades, uma combinação de propriedades de várias fontes de dados ou algum novo tipo de resultado com base em um cálculo. Quando a cláusula `Select` produz algo diferente de uma cópia do elemento de origem, a operação é chamada de *projeção*.  
  
 Para recuperar uma coleção que consiste em completa `Customer` objetos, selecione a variável de intervalo:  
  
 [!code-vb[VbLINQBasicOps#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#4)]  
  
 Se um `Customer` instância é um objeto grande com muitos campos, e tudo o que você deseja recuperar é o nome, você pode selecionar `cust.Name`, conforme mostrado no exemplo a seguir. Inferência de tipo local reconhece que isso altera o tipo de resultado de uma coleção de `Customer` objetos a uma coleção de cadeias de caracteres.  
  
 [!code-vb[VbLINQBasicOps#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#5)]  
  
 Para selecionar vários campos da fonte de dados, você tem duas opções:  
  
- No `Select` cláusula, especifique os campos que você deseja incluir no resultado. O compilador definirá um tipo anônimo que tem esses campos como suas propriedades. Para obter mais informações, consulte [Tipos anônimos](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
     Como os elementos retornados no exemplo a seguir são instâncias de um tipo anônimo, você não pode se referir ao tipo por nome em outro lugar no seu código. O nome para o tipo designado pelo compilador contém caracteres que não são válidos no código normal do Visual Basic. No exemplo a seguir, os elementos da coleção que é retornado pela consulta em `londonCusts4` são instâncias de um tipo anônimo  
  
     [!code-vb[VbLINQBasicOps#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#6)]  
  
     - ou -  
  
- Definir um tipo nomeado que contém os campos específicos que você deseja incluir no resultado, criar e inicializar instâncias do tipo no `Select` cláusula. Use essa opção somente se você precisa usar os resultados individuais fora da coleção na qual eles são retornados, ou se você tiver passá-los como parâmetros nas chamadas de método. O tipo de `londonCusts5` no exemplo a seguir é IEnumerable (Of NamePhone).  
  
     [!code-vb[VbLINQBasicOps#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#7)]  
  
     [!code-vb[VbLINQBasicOps#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#8)]  
  
 Para obter mais informações sobre como usar o `Select` cláusula no Visual Basic, consulte [cláusula Select](../../../../visual-basic/language-reference/queries/select-clause.md).  
  
## <a name="joining-data-join-and-group-join"></a>Ingressando Dados (Ingressar e Agrupar Junções)  
 Você pode combinar mais de uma fonte de dados no `From` cláusula de várias maneiras. Por exemplo, o código a seguir usa duas fontes de dados e implicitamente combina as propriedades de ambos no resultado. A consulta seleciona os alunos cujos sobrenomes começam com uma vogal.  
  
 [!code-vb[VbLINQBasicOps#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#9)]  
  
> [!NOTE]
>  Você pode executar esse código com a lista de alunos criado no [como: Criar uma lista de itens](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md).  
  
 O `Join` palavra-chave é equivalente a um `INNER JOIN` no SQL. Ele combina duas coleções com base nos valores de chave de correspondência entre os elementos em duas coleções. A consulta retorna todo ou parte dos elementos da coleção que têm valores de chave de correspondência. Por exemplo, o código a seguir duplica a ação da junção implícita anterior.  
  
 [!code-vb[VbLINQBasicOps#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#10)]  
  
 `Group Join` combina coleções em uma única coleção hierárquica, assim como um `LEFT JOIN` no SQL. Para obter mais informações, consulte [cláusula Join](../../../../visual-basic/language-reference/queries/join-clause.md) e [cláusula de junção de grupo](../../../../visual-basic/language-reference/queries/group-join-clause.md).  
  
## <a name="grouping-data-group-by"></a>Agrupando Dados (Agrupar Por)  
 Você pode adicionar um `Group By` cláusula para agrupar os elementos em um resultado de consulta acordo com um ou mais campos dos elementos. Por exemplo, o código a seguir agrupa os alunos por ano de classe.  
  
 [!code-vb[VbLINQBasicOps#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#11)]  
  
 Se você executar esse código usando a lista de alunos criado no [como: Criar uma lista de itens](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md), a saída do `For Each` instrução é:  
  
 Ano: Júnior  
  
 Tucker, Michael  
  
 Garcia, Hugo  
  
 Garcia, Debra  
  
 Tucker, Lance  
  
 Ano: Sênior  
  
 Omelchenko, Svetlana  
  
 Osada, Michiko  
  
 Fakhouri, Fadi  
  
 Feng, Hanying  
  
 Adams, Terry  
  
 Ano: Freshman  
  
 Mortensen, Sven  
  
 Garcia, Cesar  
  
 A variação mostrada no código a seguir ordena os anos de classe e, em seguida, ordena os alunos em cada ano por sobrenome.  
  
 [!code-vb[VbLINQBasicOps#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#12)]  
  
 Para obter mais informações sobre `Group By`, consulte [por cláusula Group](../../../../visual-basic/language-reference/queries/group-by-clause.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Collections.Generic.IEnumerable%601>
- [Introdução ao LINQ no Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)
- [Consultas](../../../../visual-basic/language-reference/queries/index.md)
- [Visão geral de operadores de consulta padrão (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
