---
title: Classificando com DataView (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 885b3b7b-51c1-42b3-bb29-b925f4f69a6f
ms.openlocfilehash: 4d000fd392b653f294a1d749f769f4e3bde5110d
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504286"
---
# <a name="sorting-with-dataview-linq-to-dataset"></a>Classificando com DataView (LINQ to DataSet)
A capacidade de classificar dados com base em critérios específicos e apresentá-los para um cliente através de um controle da interface do usuário é um aspecto importante da vinculação de dados. O objeto <xref:System.Data.DataView> fornece várias maneiras de classificar dados e retornar linhas de dados ordenadas por critérios específicos. Além de sua cadeia de caracteres com base em recursos, de classificação <xref:System.Data.DataView> também permite que você use [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] expressões para os critérios de classificação. [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] expressões de permitem operações de classificação muito mais poderosas e complexas que a classificação baseada em cadeia de caracteres. Este tópico descreve as duas abordagens de classificação usando <xref:System.Data.DataView>.  
  
## <a name="creating-dataview-from-a-query-with-sorting-information"></a>Criando um DataView a partir de uma consulta com informações de classificação  
 Um <xref:System.Data.DataView> objeto pode ser criado de um LINQ para consulta de conjunto de dados. Se a consulta contiver uma <xref:System.Linq.Enumerable.OrderBy%2A>, <xref:System.Linq.Enumerable.OrderByDescending%2A>, <xref:System.Linq.Enumerable.ThenBy%2A>, ou <xref:System.Linq.Enumerable.ThenByDescending%2A> cláusula as expressões nessas cláusulas são usadas como base para classificar os dados no <xref:System.Data.DataView>. Por exemplo, se a consulta contém o `Order By…`e `Then By…` cláusulas, resultante <xref:System.Data.DataView> ordenaria os dados pelas duas colunas especificadas.  
  
 A classificação baseada em expressão oferece uma classificação mais avançada e complexa do que a classificação mais simples baseada em cadeia de caracteres. Observe que a classificação baseada em cadeia de caracteres e a classificação baseada em expressão são mutuamente excludentes. Se a <xref:System.Data.DataView.Sort%2A> baseada em cadeia de caracteres for definida após <xref:System.Data.DataView> ser criado a partir de uma consulta, o filtro baseado em expressão inferido da consulta será limpo e não poderá ser redefinido.  
  
 O índice de um <xref:System.Data.DataView> é compilado quando <xref:System.Data.DataView> é criado e quando qualquer informação de classificação ou de filtragem é modificada. Obter o melhor desempenho por meio do fornecimento de classificação critérios em LINQ to DataSet de consulta que o <xref:System.Data.DataView> é criado e não modificando informações de classificação mais tarde. Para obter mais informações, consulte [desempenho de DataView](../../../../docs/framework/data/adonet/dataview-performance.md).  
  
> [!NOTE]
>  Na maioria dos casos, as expressões usadas para classificação não devem ter efeitos colaterais e devem ser determinísticas. Além disso, as expressões não devem conter lógica que dependa de um número definido de execuções, pois as operações de classificação podem ser executadas qualquer número de vezes.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir consulta a tabela SalesOrderHeader e ordena as linhas retornadas pela ordem do pedido; cria <xref:System.Data.DataView> a partir da consulta e associa o objeto <xref:System.Data.DataView> a uma <xref:System.Windows.Forms.BindingSource>.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderby)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderby)]  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir consulta a tabela SalesOrderHeader e ordena as linhas retornadas pelo valor total devido; cria <xref:System.Data.DataView> a partir da consulta e associa o objeto <xref:System.Data.DataView> a uma <xref:System.Windows.Forms.BindingSource>.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderBy2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderby2)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderBy2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderby2)]  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir consulta a tabela SalesOrderDetail e ordena as linhas retornadas pela quantidade de pedidos e depois pela ID da ordem de venda; cria <xref:System.Data.DataView> a partir da consulta e associa o objeto <xref:System.Data.DataView> a uma <xref:System.Windows.Forms.BindingSource>.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryOrderByThenBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromqueryorderbythenby)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryOrderByThenBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromqueryorderbythenby)]  
  
## <a name="using-the-string-based-sort-property"></a>Usando a propriedade de classificação baseada em cadeia de caracteres  
 A funcionalidade de classificação baseada em cadeia de caracteres de <xref:System.Data.DataView> ainda funciona com o LINQ to DataSet. Depois de um <xref:System.Data.DataView> tiver sido criado a partir de uma consulta LINQ to DataSet, você pode usar o <xref:System.Data.DataView.Sort%2A> propriedade para definir a classificação no <xref:System.Data.DataView>.  
  
 As funcionalidades de classificação baseada em cadeia de caracteres e de classificação baseada em expressão são mutuamente excludentes. A definição da propriedade <xref:System.Data.DataView.Sort%2A> limpa a classificação baseada em expressão herdada da consulta a partir da qual o objeto <xref:System.Data.DataView> foi criado.  
  
 Para obter mais informações sobre a cadeia de caracteres-baseados <xref:System.Data.DataView.Sort%2A> filtragem, consulte [classificando e filtrando dados](../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md).  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir cria um <xref:System.Data.DataView> a partir da tabela de contatos e classifica as linhas por sobrenome em ordem decrescente e depois por nome em ordem crescente:  
  
 [!code-csharp[DP DataView Samples#LDVStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvstringsort)]
 [!code-vb[DP DataView Samples#LDVStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvstringsort)]  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir consulta na tabela de contatos os sobrenomes que começam com a letra "S".  Um <xref:System.Data.DataView> é criado a partir dessa consulta e associado a um objeto <xref:System.Windows.Forms.BindingSource>.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquerystringsort)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquerystringsort)]  
  
## <a name="clearing-the-sort"></a>Limpando a classificação  
 As informações de classificação em um objeto <xref:System.Data.DataView> podem ser limpas depois de definidas usando a propriedade <xref:System.Data.DataView.Sort%2A>. Existem duas maneiras de limpar informações de classificação no objeto <xref:System.Data.DataView>:  
  
- Defina a propriedade <xref:System.Data.DataView.Sort%2A> como `null`.  
  
- Defina a propriedade <xref:System.Data.DataView.Sort%2A> como uma cadeia de caracteres vazia.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir cria um objeto <xref:System.Data.DataView> a partir de uma consulta e limpa a classificação definindo a propriedade <xref:System.Data.DataView.Sort%2A> como uma cadeia de caracteres vazia:  
  
 [!code-csharp[DP DataView Samples#LDVClearSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearsort)]
 [!code-vb[DP DataView Samples#LDVClearSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearsort)]  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir cria um objeto <xref:System.Data.DataView> a partir da tabela de contatos e define a propriedade <xref:System.Data.DataView.Sort%2A> a ser classificada por sobrenome em ordem decrescente. As informações de classificação serão limpas definindo a propriedade <xref:System.Data.DataView.Sort%2A> como `null`:  
  
 [!code-csharp[DP DataView Samples#LDVClearSort2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearsort2)]
 [!code-vb[DP DataView Samples#LDVClearSort2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearsort2)]  
  
## <a name="see-also"></a>Consulte também

- [Associação de dados e LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)
- [Filtrando com DataView](../../../../docs/framework/data/adonet/filtering-with-dataview-linq-to-dataset.md)
- [Classificando Dados](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb546145(v=vs.120))
