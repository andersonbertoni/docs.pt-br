---
title: LINQ para visão geral do DataSet
ms.date: 03/30/2017
ms.assetid: dc20a8fb-03f6-4b68-9c2b-7f7299e3070b
ms.openlocfilehash: f60308b122841421613d8e1f84aa5b9a23cc3315
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67504445"
---
# <a name="linq-to-dataset-overview"></a>LINQ para visão geral do DataSet
O <xref:System.Data.DataSet> é um dos componentes mais amplamente usados do ADO.NET. É um elemento fundamental do modelo de programação desconectado baseado no ADO.NET e ele permite que você explicitamente os dados em cache de fontes de dados diferentes. Para a camada de apresentação, o <xref:System.Data.DataSet> está totalmente integrado com controles de GUI para vinculação de dados. Para a camada intermediária, ele fornece um cache que preserva a forma dos dados relacional e inclui consulta rápida, simples e serviços de navegação da hierarquia. Uma técnica comum usada para reduzir o número de solicitações em um banco de dados é usar o <xref:System.Data.DataSet> para armazenar em cache na camada intermediária. Por exemplo, considere um aplicativo da Web ASP.NET controlado por dados. Geralmente, uma parte significativa de dados do aplicativo não muda com frequência e é comum em sessões ou usuários. Esses dados podem ser mantidos na memória no servidor Web, reduzindo o número de solicitações no banco de dados e acelerando as interações do usuário. Outro aspecto útil do <xref:System.Data.DataSet> é que ele permite que um aplicativo traga subconjuntos de dados da fonte de dados de um ou mais para o espaço de aplicativo. O aplicativo pode manipular os dados na memória, mantendo sua forma relacional.  
  
 Apesar de sua importância, o <xref:System.Data.DataSet> limitou os recursos de consulta. O método <xref:System.Data.DataTable.Select%2A> pode ser usado para filtrar e classificar, e os métodos <xref:System.Data.DataRow.GetChildRows%2A> e <xref:System.Data.DataRow.GetParentRow%2A> podem ser usados para navegação a hierarquia. Para algo mais complexo, no entanto, o desenvolvedor precisa escrever uma consulta personalizada. Isso pode resultar em aplicativos com baixo desempenho e de difícil manutenção.  
  
 LINQ to DataSet torna mais fácil e mais rápida para consultar sobre dados armazenados em cache em um <xref:System.Data.DataSet> objeto. Essas consultas são expressas na própria linguagem de programação, e não como os literais de cadeia de caracteres inseridos no código do aplicativo. Isso significa que os desenvolvedores não precisam aprender uma linguagem de consulta separada. Além disso, LINQ to DataSet permite que os desenvolvedores do Visual Studio trabalhar de maneira mais produtiva, porque o IDE do Visual Studio fornece verificação de sintaxe em tempo de compilação, digitação estática e suporte ao IntelliSense para [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]. LINQ to DataSet também pode ser usado para consultar sobre dados que foram consolidados de uma ou mais fontes de dados. Isso habilita vários cenários que exigem flexibilidade na maneira como dados são representados e tratados. Em particular, genéricos de relatório, análise e aplicativos de business intelligence requerem esse método de manipulação.  
  
## <a name="querying-datasets-using-linq-to-dataset"></a>Consultando DataSets usando o LINQ to DataSet  
 Antes de começar a consultar um <xref:System.Data.DataSet> do objeto usando LINQ to DataSet, você deve preencher o <xref:System.Data.DataSet>. Há várias maneiras de carregar dados em um <xref:System.Data.DataSet>, como o uso de <xref:System.Data.Common.DataAdapter> classe ou [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md). Depois que os dados foram carregados em um <xref:System.Data.DataSet> do objeto, você pode começar a consultá-lo. A formulação de consultas usando LINQ to DataSet é semelhante a usar [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] em relação a outros [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]-habilitado fontes de dados. [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] consultas podem ser executadas em únicas tabelas em uma <xref:System.Data.DataSet> ou em mais de uma tabela usando o <xref:System.Linq.Enumerable.Join%2A> e <xref:System.Linq.Enumerable.GroupJoin%2A> operadores de consulta padrão.  
  
 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] as consultas têm suporte em relação a tipados e sem tipo <xref:System.Data.DataSet> objetos. Se o esquema do <xref:System.Data.DataSet> é conhecido em tempo de design de aplicativo, com um tipo <xref:System.Data.DataSet> é recomendado. Em um tipo <xref:System.Data.DataSet>, as tabelas e linhas têm membros para cada uma das colunas, o que torna as consultas mais simples e mais legível tipados.  
  
 Além dos operadores de consulta padrão implementados no DLL, LINQ to DataSet adiciona várias <xref:System.Data.DataSet>-extensões específicas que facilitam a consulta em um conjunto de <xref:System.Data.DataRow> objetos. Essas extensões específicas de <xref:System.Data.DataSet> incluem operadores para comparar sequências de linhas, bem como métodos que fornecem acesso aos valores de coluna de <xref:System.Data.DataRow>.  
  
## <a name="n-tier-applications-and-linq-to-dataset"></a>Aplicativos de n camadas e LINQ to DataSet  
 Aplicativos de dados de n camadas são aplicativos centrados em dados que são separados em várias camadas lógicas (ou camadas). Um aplicativo de n camadas típico inclui uma camada de apresentação, uma camada intermediária e uma camada de dados. Dividir componentes do aplicativo em camadas separadas aumenta a facilidade de manutenção e a escalabilidade do aplicativo. Para obter mais informações sobre aplicativos de N camadas de dados, consulte [trabalhar com conjuntos de dados em aplicativos de n camadas](/visualstudio/data-tools/work-with-datasets-in-n-tier-applications).  
  
 Em aplicativos de n camadas, o <xref:System.Data.DataSet> costuma ser usado na camada intermediária para armazenar em cache informações para um aplicativo Web. O LINQ to DataSet, funcionalidade de consulta é implementado por meio de métodos de extensão e estende o ADO.NET 2.0 existente <xref:System.Data.DataSet>.  
  
## <a name="see-also"></a>Consulte também

- [Consultando DataSets](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)
- [LINQ (consulta integrada à linguagem) – C#](../../../csharp/programming-guide/concepts/linq/index.md)
- [LINQ (consulta integrada à linguagem) – Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md)
- [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md)
