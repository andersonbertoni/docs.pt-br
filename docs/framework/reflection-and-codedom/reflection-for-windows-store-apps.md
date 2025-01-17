---
title: Reflexão no .NET Framework para aplicativos da Windows Store
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- reflection, Windows Store apps
- .NET for Windows Store apps, TypeInfo class
ms.assetid: 0d07090c-9b47-4ecc-81d1-29d539603c9b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b5503d8a474d7f19348b9342bc02e216bd987223
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66378603"
---
# <a name="reflection-in-the-net-framework-for-windows-store-apps"></a>Reflexão no .NET Framework para aplicativos da Windows Store
Desde sua versão 4.5, o .NET Framework inclui um conjunto de membros e tipos de reflexão para uso em aplicativos [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Esses tipos e membros estão disponíveis no .NET Framework completo, bem como no [.NET para aplicativos da Windows Store](https://go.microsoft.com/fwlink/?LinkID=225700). Este documento explica as principais diferenças entre eles e seus equivalentes no .NET Framework 4 e em versões anteriores.  
  
 Se você estiver criando um aplicativo [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], deverá usar os membros e tipos de reflexão no [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]. Esses membros e tipos também estão disponíveis, mas não são obrigatórios, para uso em aplicativos da área de trabalho, portanto você pode usar o mesmo código para os dois tipos de aplicativos.  
  
## <a name="typeinfo-and-assembly-loading"></a>TypeInfo e Carregamento do Assembly  
 No [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)], a classe <xref:System.Reflection.TypeInfo> contém algumas das funcionalidades da classe <xref:System.Type> do .NET Framework 4. Um objeto <xref:System.Type> representa uma referência a uma definição de tipo, enquanto um objeto <xref:System.Reflection.TypeInfo> representa a definição de tipo em si. Isso permite que você manipule objetos <xref:System.Type> sem necessariamente exigir que o tempo de execução carregue o assembly que eles referenciam. Obter o objeto <xref:System.Reflection.TypeInfo> associado força o assembly a ser carregado.  
  
 <xref:System.Reflection.TypeInfo> contém muitos dos membros disponíveis em <xref:System.Type> e muitas das propriedades de reflexão no [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] retornam coleções de objetos <xref:System.Reflection.TypeInfo>. Para obter um objeto <xref:System.Reflection.TypeInfo> de um objeto <xref:System.Type>, use o método <xref:System.Reflection.IReflectableType.GetTypeInfo%2A>.  
  
## <a name="query-methods"></a>Métodos de consulta  
 No [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)], use as propriedades de reflexão que retornam coleções <xref:System.Collections.Generic.IEnumerable%601> em vez de métodos que retornam matrizes. Os contextos de reflexão podem implementar passagens lentas dessas coleções para grandes tipos ou assemblies.  
  
 As propriedades de reflexão retornam apenas os métodos declarados em um objeto específico em vez de percorrer a árvore de herança. Além disso, elas não usam parâmetros <xref:System.Reflection.BindingFlags> para filtragem. Em vez disso, a filtragem ocorre no código do usuário, usando consultas LINQ nas coleções retornadas. Para objetos de reflexão que se originam com o tempo de execução (por exemplo, como resultado de `typeof(Object)`), a passagem pela árvore de herança é melhor realizada usando os métodos auxiliares da classe <xref:System.Reflection.RuntimeReflectionExtensions>. Os consumidores de objetos de contextos de reflexão personalizados não podem usar esses métodos e devem percorrer a árvore de herança sozinhos.  
  
## <a name="restrictions"></a>Restrições  
 Em um aplicativo [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], o acesso a alguns membros e tipos do .NET Framework é restrito. Por exemplo, você não pode chamar os métodos do .NET Framework que não estão incluídos no [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)], usando um objeto <xref:System.Reflection.MethodInfo>. Além disso, determinados tipos e membros que não são considerados seguros dentro do contexto de um aplicativo [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] são bloqueados, como são os membros <xref:System.Runtime.InteropServices.Marshal> e <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal>. Essa restrição afeta apenas os tipos e membros do .NET Framework. Você pode chamar seu código ou o código de terceiros como faria normalmente.  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa os tipos e membros de reflexão no [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] para recuperar os métodos e propriedades do tipo <xref:System.Globalization.Calendar>, incluindo os métodos e propriedades herdados. Para executar esse código, cole-o no arquivo de código para uma página [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] que contém um controle <xref:Windows.UI.Xaml.Controls.TextBlock?displayProperty=nameWithType> denominado `textblock1` em um projeto chamado Reflexão. Se você colar esse código dentro de um projeto com um nome diferente, certifique-se de alterar o nome do namespace para corresponder ao seu projeto.  
  
 [!code-csharp[System.ReflectionWinStoreApp#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.reflectionwinstoreapp/cs/mainpage.xaml.cs#1)]
 [!code-vb[System.ReflectionWinStoreApp#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.reflectionwinstoreapp/vb/mainpage.xaml.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Reflexão](../../../docs/framework/reflection-and-codedom/reflection.md)
- [.NET para aplicativos da Windows Store – APIs com suporte](https://go.microsoft.com/fwlink/?LinkID=225700)
