---
title: LINQ e o ADO.NET
ms.date: 03/30/2017
ms.assetid: bf0c8f93-3ff7-49f3-8aed-f2b7ac938dec
ms.openlocfilehash: 9c517b3efca8cd2b41782858ef1e18e3cba76c1b
ms.sourcegitcommit: b5c59eaaf8bf48ef3ec259f228cb328d6d4c0ceb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67539404"
---
# <a name="linq-and-adonet"></a>LINQ e o ADO.NET
Hoje, muitos desenvolvedores comerciais devem usar duas (ou mais) linguagens de programação: uma linguagem de alto nível para as camadas de apresentação e lógica de negócios (como o Visual C# ou Visual Basic) e uma linguagem de consulta para interagir com o banco de dados (como Transact-SQL) . Isso exige que o desenvolvedor seja proficiente em várias linguagens para ser eficaz e também provoca incompatibilidades de linguagens no ambiente de desenvolvimento. Por exemplo, um aplicativo que usa uma API de acesso a dados para executar uma consulta em um banco de dados especifica a consulta como um literal de cadeia de caracteres usando aspas. Essa cadeia de caracteres de consulta é ilegível para o compilador e os erros não são verificados, como sintaxe inválida ou se as colunas ou linhas referenciadas realmente existem. Não há nenhuma verificação do tipo dos parâmetros da consulta e também nenhum suporte do `IntelliSense`.  
  
 O [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] permite que os desenvolvedores formem consultas baseadas em conjuntos no código de seus aplicativos, sem precisar usar uma linguagem de consulta separada. Você pode escrever consultas de [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] com várias fontes de dados enumeráveis (ou seja, uma fonte de dados que implemente a interface <xref:System.Collections.IEnumerable>), como estruturas de dados na memória, documentos XML, bancos de dados SQL e objetos <xref:System.Data.DataSet>. Embora essas fontes de dados enumeráveis sejam implementadas de várias maneiras, todas elas expõem as mesmas sintaxe e constructos de linguagem. Como as consultas podem ser formadas na própria linguagem de programação, você não precisa usar outra linguagem de consulta que seja inserida como literais de cadeia de caracteres que não podem ser compreendidos ou verificados pelo compilador. Integração de consultas na linguagem de programação também permite que os programadores do Visual Studio ser mais produtivo, fornecendo o tipo de tempo de compilação e verificação de sintaxe, e `IntelliSense`. Esses recursos reduzem a necessidade de depuração da consulta e de correção de erros.  
  
 A transferência de dados de tabelas SQL para objetos na memória é geralmente tediosa e sujeita a erros. O [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] provedor implementado pelo LINQ to DataSet e [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] converte os dados de origem em <xref:System.Collections.IEnumerable>-com base em coleções de objetos. O programador sempre exibe os dados como uma coleção de <xref:System.Collections.IEnumerable>, quando você consulta e quando você atualiza. Suporte completo do `IntelliSense` é fornecido para escrever consultas nessas coleções.  
  
 Há três ADO.NET separado [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] tecnologias: LINQ to DataSet, [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)]e LINQ to Entities. LINQ to DataSet fornece mais rica e otimizadas sobre o <xref:System.Data.DataSet> e [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] permite que você consulte diretamente esquemas de banco de dados do SQL Server e o LINQ to Entities permite que você consulte um modelo de dados de entidade.  
  
 O diagrama a seguir fornece uma visão geral de como as tecnologias LINQ do ADO.NET estão relacionadas às linguagens de programação de alto nível e às fontes de dados habilitadas para LINQ.  
  
 ![LINQ to ADO.NET overview](../../../../docs/framework/data/adonet/media/dpue-linqtoadonetoverview-bpuedev11.gif "DPUE_LinqToAdoNetOverview_bpuedev11")  
  
 Para obter mais informações sobre o LINQ, consulte [Language Integrated Query (LINQ)](../../../csharp/programming-guide/concepts/linq/index.md).
  
 As seções a seguir fornecem mais informações sobre o LINQ to DataSet, [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)]e LINQ to Entities.  
  
## <a name="linq-to-dataset"></a>LINQ to DataSet  
 O <xref:System.Data.DataSet> é um elemento fundamental do modelo de programação desconectado que se baseia no ADO.NET e é amplamente usado. LINQ to DataSet permite que os desenvolvedores criem recursos sofisticados de consulta no <xref:System.Data.DataSet> usando o mesmo mecanismo de formulação de consulta que está disponível para muitas outras fontes de dados. Para obter mais informações, consulte [LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset.md).  
  
## <a name="linq-to-sql"></a>LINQ to SQL  
 O [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] é uma ferramenta útil para os desenvolvedores que não requerem mapeamento para um modelo conceitual. Usando o [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)], você pode usar o modelo de programação do [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] diretamente sobre o esquema do banco de dados existente. [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] permite aos desenvolvedores gerar classes do .NET Framework que representam os dados. Em vez do mapeamento para um modelo de dados conceitual, essas classes geradas mapeiam diretamente para tabelas do banco de dados, modos de exibição, procedimentos armazenados e funções definidas pelo usuário.  
  
 Com o [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)], os desenvolvedores podem escrever código diretamente no esquema de armazenamento usando o mesmo padrão de programação do [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] como coleções na memória e o <xref:System.Data.DataSet>, além de outras fontes de dados, como XML. Para obter mais informações, consulte [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md).  
  
## <a name="linq-to-entities"></a>LINQ to Entities  
 Atualmente, maioria dos aplicativos são escritos sobre bancos de dados relacionais. Em algum ponto, esses aplicativos precisarão interagir com os dados representados em um formulário relacional. Os esquemas de banco de dados não são sempre ideais para criar aplicativos, e os modelos conceituais do aplicativo não são os mesmos que os modelos lógicos de bancos de dados. O modelo de dados de entidade é um modelo de dados conceitual que pode ser usado para modelar os dados de um domínio específico, para que os aplicativos podem interagir com dados como objetos. Ver [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) para obter mais informações.  
  
 Por meio do modelo de dados de entidade, os dados relacionais são expostos como objetos no ambiente .NET. Isso torna a camada do objeto um destino ideal para o suporte do [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] permitindo que os desenvolvedores formulem consultas no banco de dados na linguagem usada para criar a lógica de negócios. Esse recurso é conhecido como LINQ to Entities. Consulte [LINQ to Entities](../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md) para obter mais informações.  
  
## <a name="see-also"></a>Consulte também

- [LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset.md)
- [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md)
- [LINQ to Entities](../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)
- [LINQ (Consulta Integrada à Linguagem)](../../../csharp/programming-guide/concepts/linq/index.md)
- [ADO.NET Overview](ado-net-overview.md) (Visão geral do ADO.NET)
