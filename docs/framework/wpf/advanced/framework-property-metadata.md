---
title: Metadados de propriedade de estrutura
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WPF], framework properties
- framework property metadata [WPF]
ms.assetid: 9962f380-b885-4b61-a62e-457397083fea
ms.openlocfilehash: 81c1941ffd95afb01dcb6ebda2634832a91cd876
ms.sourcegitcommit: 83ecdf731dc1920bca31f017b1556c917aafd7a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67859853"
---
# <a name="framework-property-metadata"></a>Metadados de propriedade de estrutura
Opções de metadados de propriedades de Framework são relatadas para as propriedades dos elementos de objeto consideradas a nível de estrutura do WPF na [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] arquitetura. Em geral a designação de nível de estrutura WPF implica que recursos, como renderização, associação de dados e refinamentos do sistema são tratados pelo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] APIs de apresentação e executáveis. Metadados de propriedade de estrutura é consultado por esses sistemas para determinar características específicas de recurso de propriedades de elemento específico.  

<a name="prerequisites"></a>   
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico pressupõe que você entende as propriedades de dependência da perspectiva de um consumidor de propriedades de dependência existentes nas classes [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] e que leu a [Visão geral das propriedades de dependência](dependency-properties-overview.md). Você também deve ter lido [metadados de propriedade de dependência](dependency-property-metadata.md).  
  
<a name="What_Is_Communicated_by_Framework_Property"></a>   
## <a name="what-is-communicated-by-framework-property-metadata"></a>O que é comunicado por metadados de propriedades de estrutura  
 Metadados de propriedade de estrutura podem ser divididos nas seguintes categorias:  
  
- Relatar propriedades de layout que afetam um elemento (<xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A>, <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>, <xref:System.Windows.FrameworkPropertyMetadata.AffectsRender%2A>). Você pode definir esses sinalizadores nos metadados se a propriedade afeta esses respectivos aspectos e você também estiver implementando o <xref:System.Windows.FrameworkElement.MeasureOverride%2A>  /  <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> métodos em sua classe para fornecer comportamento de renderização específico e informações para o layout sistema. Normalmente, tal implementação deve verificar para invalidações de propriedade nas propriedades de dependência em que qualquer uma dessas propriedades de layout eram "verdadeiras" nos metadados de propriedade e somente essas exigiriam uma solicitação de uma nova passagem de layout.  
  
- Propriedades de layout que afetam o elemento pai de um elemento de relatório (<xref:System.Windows.FrameworkPropertyMetadata.AffectsParentArrange%2A>, <xref:System.Windows.FrameworkPropertyMetadata.AffectsParentMeasure%2A>). Alguns exemplos onde esses sinalizadores são definidos por padrão são <xref:System.Windows.Documents.FixedPage.Left%2A?displayProperty=nameWithType> e <xref:System.Windows.Documents.Paragraph.KeepWithNext%2A?displayProperty=nameWithType>.  
  
- <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A>. Por padrão, as propriedades de dependência não herdam valores. <xref:System.Windows.FrameworkPropertyMetadata.OverridesInheritanceBehavior%2A> permite que o caminho de herança também viagem para uma árvore visual, que é necessária para alguns cenários de composição de controle.  
  
    > [!NOTE]
    >  O termo "herda" no contexto de valores de propriedade significa algo específico para propriedades de dependência; Isso significa que elementos filho podem herdar o valor da propriedade de dependência real de elementos pai por causa de uma funcionalidade de nível de estrutura WPF do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sistema de propriedade. Não tem nada a ver diretamente com herança de tipo e membros de código gerenciado por tipos derivados. Para obter detalhes, consulte [Herança do valor da propriedade](property-value-inheritance.md).  
  
- Relatar características de associação de dados (<xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A>, <xref:System.Windows.FrameworkPropertyMetadata.BindsTwoWayByDefault%2A>). Por padrão, as propriedades de dependência na estrutura dão suporte à vinculação de dados, com um comportamento de associação unidirecional. Você poderá desabilitar a vinculação de dados se não houvesse nenhum cenário para isso qualquer tipo (porque elas devem ser flexível e extensível, existem muitos exemplos de tais propriedades no padrão [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] APIs). Você pode configurar a associação para ter um padrão bidirecional para as propriedades que liga os comportamentos de um controle entre seus componentes (<xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> é um exemplo) ou onde a associação bidirecional é a situação comum e esperada pelos usuários (<xref:System.Windows.Controls.TextBox.Text%2A> é um exemplo). Alterar os metadados relacionados a vinculação de dados somente influencia o padrão; em uma base por associação esse padrão sempre pode ser alterado. Para obter detalhes sobre modos de associação e associação em geral, consulte [visão geral de vinculação de dados](../data/data-binding-overview.md).  
  
- Relatar se as propriedades devem ser registradas no diário por aplicativos ou serviços que dão suporte ao registro no diário (<xref:System.Windows.FrameworkPropertyMetadata.Journal%2A>). Para elementos gerais, o registro no diário não está habilitado por padrão, mas ele é habilitado seletivamente para certos controles de entrada do usuário. Esta propriedade destina-se a ser lida pelos serviços de diário incluindo a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] implementação do registro no diário e normalmente é definida em controles de usuário, como seleções pelo usuário em listas que devem ser persistentes entre etapas de navegação. Para obter informações sobre o diário, consulte [visão geral da navegação](../app-development/navigation-overview.md).  
  
<a name="Reading_FrameworkPropertyMetadata"></a>   
## <a name="reading-frameworkpropertymetadata"></a>Leitura do FrameworkPropertyMetadata  
 Cada uma das propriedades citadas acima são as propriedades específicas que o <xref:System.Windows.FrameworkPropertyMetadata> adiciona à sua classe base imediata <xref:System.Windows.UIPropertyMetadata>. Cada uma dessas propriedades será `false`, por padrão. Uma solicitação de metadados para uma propriedade em que é importante saber o valor dessas propriedades deve tentar converter os metadados retornados para <xref:System.Windows.FrameworkPropertyMetadata>e, em seguida, verificar os valores das propriedades individuais conforme necessário.  
  
<a name="Specifying_Metadata"></a>   
## <a name="specifying-metadata"></a>Especificação dos metadados  
 Quando você cria uma nova instância de metadados para fins de aplicá-los para um novo registro de propriedade de dependência, você tem a opção de qual classe de metadados usar: a base <xref:System.Windows.PropertyMetadata> ou alguma classe derivada, como <xref:System.Windows.FrameworkPropertyMetadata>. Em geral, você deve usar <xref:System.Windows.FrameworkPropertyMetadata>, especialmente se sua propriedade tiver qualquer interação com o sistema de propriedades e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] funções como layout e associação de dados. Outra opção para situações mais sofisticadas é derivar de <xref:System.Windows.FrameworkPropertyMetadata> para criar seus próprios metadados reporting classe com informações extras carregadas em seus membros. Ou você pode usar <xref:System.Windows.PropertyMetadata> ou <xref:System.Windows.UIPropertyMetadata> para comunicar o grau de suporte para recursos da sua implementação.  
  
 Para propriedades existentes (<xref:System.Windows.DependencyProperty.AddOwner%2A> ou <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> chamar), você sempre deve substituir com o tipo de metadados usado pelo registro original.  
  
 Se você estiver criando um <xref:System.Windows.FrameworkPropertyMetadata> da instância, há duas maneiras de preencher os metadados com valores para as propriedades específicas que comunicam as características de propriedade do framework:  
  
1. Use o <xref:System.Windows.FrameworkPropertyMetadata> assinatura de construtor que permite que um `flags` parâmetro. Esse parâmetro deve ser preenchido com desejado de todos os valores combinados do <xref:System.Windows.FrameworkPropertyMetadataOptions> sinalizadores de enumeração.  
  
2. Use uma das assinaturas sem um `flags` parâmetro e, em seguida, defina cada propriedade booliana de relatório <xref:System.Windows.FrameworkPropertyMetadata> para `true` para cada alteração de característica desejada. Se você fizer isso, você deverá definir essas propriedades antes de quaisquer elementos com esta propriedade de dependência sejam construídos; as propriedades boolianas são leitura / gravação para permitir que esse comportamento de evitar o `flags` parâmetro e ainda preencher os metadados, mas os metadados devem ficar efetivamente selados antes de usar a propriedade. Assim, a tentativa de definir as propriedades, depois de solicitar os metadados, será uma operação inválida.  
  
<a name="Framework_Property_Metadata_Merge_Behavior"></a>   
## <a name="framework-property-metadata-merge-behavior"></a>Comportamento de mesclagem de metadados de propriedades de estrutura  
 Quando você substitui metadados de propriedade de estrutura, as diferentes características dos metadados são mescladas ou substituídas.  
  
- <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> é mesclada. Se você adicionar um novo <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>, retorno de chamada é armazenado nos metadados. Se você não especificar uma <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> em uma substituição, o valor de <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> é promovido como uma referência do ancestral mais próximo que o especificou nos metadados.  
  
- O comportamento do sistema de propriedade real para <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> é que as implementações para todos os proprietários de metadados na hierarquia são retidos e adicionados a uma tabela com ordem de execução pelo sistema de propriedades sendo que os retornos de chamada da classe mais profundamente derivada são chamado pela primeira vez. Retornos de chamada herdados são executados somente uma vez, contando como sendo pertencente a classe que colocou-os nos metadados.  
  
- <xref:System.Windows.PropertyMetadata.DefaultValue%2A> é substituído. Se você não especificar uma <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> em uma substituição, o valor de <xref:System.Windows.PropertyMetadata.DefaultValue%2A> virá do ancestral mais próximo que o especificou nos metadados.  
  
- <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> as implementações são substituídas. Se você adicionar um novo <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>, retorno de chamada é armazenado nos metadados. Se você não especificar uma <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> em uma substituição, o valor de <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> é promovido como uma referência do ancestral mais próximo que o especificou nos metadados.  
  
- O comportamento de sistema de propriedades é que apenas o <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> nos metadados imediatos é invocado. Não há referências a outras <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> implementações na hierarquia são retidas.  
  
- Os sinalizadores de <xref:System.Windows.FrameworkPropertyMetadataOptions> enumeração são combinados como uma operação OR bit a bit.  Se você especificar <xref:System.Windows.FrameworkPropertyMetadataOptions>, as opções originais não serão substituídas.  Para alterar uma opção, defina a propriedade correspondente no <xref:System.Windows.FrameworkPropertyMetadata>. Por exemplo, se o original <xref:System.Windows.FrameworkPropertyMetadata> conjuntos de objetos do <xref:System.Windows.FrameworkPropertyMetadataOptions.NotDataBindable?displayProperty=nameWithType> sinalizador, você pode alterar isso definindo <xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A?displayProperty=nameWithType> para `false`.  
  
 Esse comportamento é implementado por <xref:System.Windows.FrameworkPropertyMetadata.Merge%2A>e pode ser substituído em classes derivadas de metadados.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.DependencyProperty.GetMetadata%2A>
- [Metadados de propriedade da dependência](dependency-property-metadata.md)
- [Visão geral das propriedades da dependência](dependency-properties-overview.md)
- [Propriedades de dependência personalizada](custom-dependency-properties.md)
