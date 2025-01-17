---
title: Design de Struct
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], structures
- deallocating structures
- allocating structures
- value types, structures
- structure design
- type design guidelines, structures
- structures [.NET Framework], design guidelines
ms.assetid: 1f48b2d8-608c-4be6-9ba4-d8f203ed9f9f
author: KrzysztofCwalina
ms.openlocfilehash: e787c5b34848a561b43c3457341673f11cc2bd00
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67775552"
---
# <a name="struct-design"></a>Design de Struct
O tipo de valor de uso geral é mais conhecido como um struct, sua palavra-chave c#. Esta seção fornece diretrizes para design de struct geral.  
  
 **X não** fornecer um construtor sem parâmetros para um struct.  
  
 Seguir essa diretriz permite matrizes de structs são criados sem necessidade de executar o construtor em cada item da matriz. Observe que C# não permite que structs ter construtores sem parâmetros.  
  
 **X DO NOT** definir tipos de valor mutável.  
  
 Tipos de valor mutável tem vários problemas. Por exemplo, quando um getter de propriedade retorna um tipo de valor, o chamador recebe uma cópia. Como a cópia é criada implicitamente, os desenvolvedores podem não estar cientes de que eles são mutação a cópia e não o valor original. Além disso, alguns idiomas (linguagens dinâmicas, em particular) tem problemas ao usar tipos de valor mutável porque mesmo variáveis locais, quando desreferenciado, fazer com que uma cópia a ser feita.  
  
 **✓ DO** Certifique-se de que um estado em que todos os dados da instância é definido como zero, false ou null (conforme apropriado) é válido.  
  
 Isso impede a criação acidental de instâncias inválidas quando uma matriz de estruturas de é criada.  
  
 **✓ DO** implementar <xref:System.IEquatable%601> em tipos de valor.  
  
 O <xref:System.Object.Equals%2A?displayProperty=nameWithType> método em tipos de valor faz com que a conversão boxing e sua implementação padrão não é muito eficiente, porque ele usa a reflexão. <xref:System.IEquatable%601.Equals%2A> pode ter um desempenho muito melhor e pode ser implementado para que ele não fará com que a conversão boxing.  
  
 **X DO NOT** estender explicitamente <xref:System.ValueType>. Na verdade, a maioria das linguagens de evitar isso.  
  
 Em geral, structs pode ser muito útil, mas só deve ser usados para valores pequenos, único e imutáveis que não serão ser boxed com frequência.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*  
  
 *Reimpresso com permissão da Pearson Education, Inc. de [as diretrizes de Design do Framework: As convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicados 22 de outubro de 2008 pela Addison-Wesley Professional, como parte da série de desenvolvimento do Microsoft Windows.*  
  
## <a name="see-also"></a>Consulte também

- [Diretrizes de Design de tipo](../../../docs/standard/design-guidelines/type.md)
- [Diretrizes de design do Framework](../../../docs/standard/design-guidelines/index.md)
- [Escolhendo entre a classe e Struct](../../../docs/standard/design-guidelines/choosing-between-class-and-struct.md)
