---
title: Tipos de dados básicos
ms.date: 03/30/2017
ms.assetid: eca2c472-9548-4800-bd31-5d8d9f11752b
ms.openlocfilehash: 6e1e48b3d390cf7c8ec81735b9637f706ad3a0ad
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67306257"
---
# <a name="basic-data-types"></a>Tipos de dados básicos
Porque as consultas LINQ to SQL traduzem a Transact-SQL antes que elas sejam executadas no Microsoft SQL Server. LINQ to SQL suporta grande parte da mesma funcionalidade interna que o SQL Server faz para tipos de dados básicos.  
  
## <a name="casting"></a>Conversão  
 Conversões implícitas ou explícitas estão ativados de um tipo de CLR de origem para um tipo de CLR de destino se há uma conversão válido semelhante em SQL Server. Para obter mais informações sobre conversão de CLR, consulte [função CType](~/docs/visual-basic/language-reference/functions/ctype-function.md) (Visual Basic) e [operadores de conversão e de teste de tipo](~/docs/csharp/language-reference/operators/type-testing-and-conversion-operators.md). Após a conversão, as conversões alteram o comportamento das operações executadas em uma expressão de CLR para corresponder ao comportamento de outras expressões de CLR que mapeiam naturalmente para o tipo de destino. Conversões são também translatable no contexto de mapeamento de herança. Objetos podem ser convertidos em um subtipos mais específicos entidade para que seus dados específicos subtipo- possam ser acessados.  
  
## <a name="equality-operators"></a>Operadores de igualdade  
 LINQ to SQL oferece suporte aos seguintes operadores de igualdade em tipos de dados básicos dentro das consultas LINQ to SQL:  
  
- Iguais e operador de desigualdade: Operadores de igualdade e desigualdade têm suporte para, numéricos <xref:System.Boolean>, <xref:System.DateTime>, e <xref:System.TimeSpan> tipos. Para obter mais informações sobre operadores do Visual Basic `=` e `<>`, consulte [operadores de comparação](~/docs/visual-basic/language-reference/operators/comparison-operators.md). Para obter mais informações sobre C# operadores de comparação `==` e `!=`, consulte [operadores de igualdade](~/docs/csharp/language-reference/operators/equality-operators.md).
  
- É o operador: O `IS` operador tem uma translação suportado quando está sendo usado o mapeamento de herança. Pode ser usado em vez de diretamente testar a coluna de discriminador para determinar se um objeto é de um tipo específico de entidade, e é convertido para uma verificação na coluna de discriminador. Para obter mais informações sobre o Visual Basic e C# for operators, consulte [operador Is](~/docs/visual-basic/language-reference/operators/is-operator.md) e [está](~/docs/csharp/language-reference/operators/type-testing-and-conversion-operators.md#is-operator).  
  
## <a name="see-also"></a>Consulte também

- [Mapeamento de tipo CLR do SQL](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)
- [Funções e tipos de dados](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)
