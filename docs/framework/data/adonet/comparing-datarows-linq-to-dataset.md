---
title: Comparando DataRows (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8fe0eadf-297b-487c-8d4b-7816753c2883
ms.openlocfilehash: 7c8687e0e14458c944e2dec2b51b9f78bb2377c3
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504215"
---
# <a name="comparing-datarows-linq-to-dataset"></a>Comparando DataRows (LINQ to DataSet)
O [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] define vários operadores de conjunto para comparar elementos de origem e ver se são iguais. O [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] fornece os seguintes operadores de conjunto:  
  
- <xref:System.Linq.Enumerable.Distinct%2A>  
  
- <xref:System.Linq.Enumerable.Union%2A>  
  
- <xref:System.Linq.Enumerable.Intersect%2A>  
  
- <xref:System.Linq.Enumerable.Except%2A>  
  
 Esses operadores comparam os elementos de origem chamando os métodos <xref:System.Collections.Generic.IEqualityComparer%601.GetHashCode%2A> e <xref:System.Collections.Generic.IEqualityComparer%601.Equals%2A> em cada coleção de elementos. No caso de <xref:System.Data.DataRow>, esses operadores executam uma comparação de referência, que geralmente não é o comportamento ideal para operações de conjunto em dados de tabela. Para operações de conjunto, você geralmente quer determinar se os valores de elementos são iguais, e não as referências de elementos. Portanto, o <xref:System.Data.DataRowComparer> classe foi adicionado ao LINQ to DataSet. Essa classe pode ser usada para comparar os valores de linha.  
  
 A classe <xref:System.Data.DataRowComparer> contém uma implementação de comparação de valores para <xref:System.Data.DataRow>, portanto essa classe pode ser usada para operações de conjunto, como <xref:System.Linq.Enumerable.Distinct%2A>. Essa classe não pode ser instanciada diretamente; em vez disso, a propriedade <xref:System.Data.DataRowComparer.Default%2A> deve ser usada para retornar uma instância de <xref:System.Data.DataRowComparer%601>. O método <xref:System.Data.DataRowComparer%601.Equals%2A> é então chamado e os dois objetos <xref:System.Data.DataRow> a serem comparados são passados como parâmetros de entrada. O método <xref:System.Data.DataRowComparer%601.Equals%2A> retornará `true` se o conjunto ordenado de valores de coluna em ambos os objetos <xref:System.Data.DataRow> forem iguais; caso contrário, retornará `false`.  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa `Intersect` para retornar os contatos que aparecem em ambas as tabelas.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#intersect2)]
 [!code-vb[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#intersect2)]  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir compara duas linhas e obtém seus códigos hash.  
  
 [!code-vb[DP LINQ to DataSet Examples#CompareDifferentRows](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#comparedifferentrows)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataRowComparer>
- [Carregar dados para um conjunto de dados](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md)
- [Exemplos de LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)
