---
title: Visão geral de storyboards
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboard syntax [WPF]
- syntax [WPF], Storyboard
- timelines [WPF]
ms.assetid: 1a698c3c-30f1-4b30-ae56-57e8a39811bd
ms.openlocfilehash: 41f8ec79eecf47e9caeb5bf1411e17211c32a410
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64663292"
---
# <a name="storyboards-overview"></a>Visão geral de storyboards
Este tópico mostra como usar <xref:System.Windows.Media.Animation.Storyboard> objetos para organizar e aplicar animações. Ele descreve como manipular interativamente <xref:System.Windows.Media.Animation.Storyboard> objetos e descreve a sintaxe de direcionamento indireto de propriedade.  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>Pré-requisitos  
 Para entender esse tópico, você deve estar familiarizado com os diferentes tipos de animação e seus recursos básicos. Para obter uma introdução à animação, consulte a [Visão geral da animação](animation-overview.md). Você também deve saber usar propriedades anexadas. Para obter mais informações sobre as propriedades anexadas, consulte [Visão geral das propriedades anexadas](../advanced/attached-properties-overview.md).  
  
<a name="whatisatimeline"></a>   
## <a name="what-is-a-storyboard"></a>O que é um storyboard?  
 Animações não são o único tipo útil de linha do tempo. Outras classes de linha do tempo são fornecidas para ajudá-lo a organizar conjuntos de linhas do tempo e aplicar linhas do tempo a propriedades. Cronogramas contêiner derivam de <xref:System.Windows.Media.Animation.TimelineGroup> de classe e inclua <xref:System.Windows.Media.Animation.ParallelTimeline> e <xref:System.Windows.Media.Animation.Storyboard>.  
  
 Um <xref:System.Windows.Media.Animation.Storyboard> é um tipo de linha de tempo de contêiner que fornece informações de direcionamento para as linhas do tempo que ele contém. Um Storyboard pode conter qualquer tipo de <xref:System.Windows.Media.Animation.Timeline>, incluindo outras linhas do tempo contêiner e animações. <xref:System.Windows.Media.Animation.Storyboard> objetos permitem que você combine cronogramas que afetam uma variedade de objetos e propriedades em uma árvore de única linha do tempo, tornando mais fácil organizar e controlar comportamentos complexos de tempo. Por exemplo, suponha que você deseje que um botão faça estas três coisas.  
  
- Aumenta e muda de cor quando o usuário o seleciona.  
  
- Diminui e, em seguida, aumenta novamente para seu tamanho original quando recebe um clique.  
  
- Diminui e esmaece até uma opacidade de 50% quando é desabilitado.  
  
 Nesse caso, você tem vários conjuntos de animações que se aplicam ao mesmo objeto e deseja que eles sejam reproduzidos em tempos diferentes, dependentes do estado do botão. <xref:System.Windows.Media.Animation.Storyboard> objetos permitem que você organize as animações e aplicá-las em grupos para um ou mais objetos.  
  
<a name="wherecanyouuseastoryboard"></a>   
## <a name="where-can-you-use-a-storyboard"></a>Onde você pode usar um storyboard?  
 Um <xref:System.Windows.Media.Animation.Storyboard> pode ser usado para animar propriedades de dependência de classes animáveis (para obter mais informações sobre o que torna uma classe animável, consulte a [visão geral da animação](animation-overview.md)). No entanto, como o storyboard é um recurso de nível de estrutura, o objeto deve pertencer à <xref:System.Windows.NameScope> de um <xref:System.Windows.FrameworkElement> ou um <xref:System.Windows.FrameworkContentElement>.  
  
 Por exemplo, você pode usar um <xref:System.Windows.Media.Animation.Storyboard> para fazer o seguinte:  
  
- Animar uma <xref:System.Windows.Media.SolidColorBrush> (elemento não estrutura) que pinta a tela de fundo de um botão (um tipo de <xref:System.Windows.FrameworkElement>),  
  
- Animar uma <xref:System.Windows.Media.SolidColorBrush> (elemento não estrutura) que pinta o preenchimento de uma <xref:System.Windows.Media.GeometryDrawing> (elemento não estrutura) exibido usando uma <xref:System.Windows.Controls.Image> (<xref:System.Windows.FrameworkElement>).  
  
- No código, animar uma <xref:System.Windows.Media.SolidColorBrush> declarado por uma classe que também contém um <xref:System.Windows.FrameworkElement>, se o <xref:System.Windows.Media.SolidColorBrush> registra seu nome com que <xref:System.Windows.FrameworkElement>.  
  
 No entanto, você não poderia usar um <xref:System.Windows.Media.Animation.Storyboard> animar uma <xref:System.Windows.Media.SolidColorBrush> que não registrou seu nome com um <xref:System.Windows.FrameworkElement> ou <xref:System.Windows.FrameworkContentElement>, ou não foi usado para definir uma propriedade de um <xref:System.Windows.FrameworkElement> ou <xref:System.Windows.FrameworkContentElement>.  
  
<a name="applyanimationswithastoryboard"></a>   
## <a name="how-to-apply-animations-with-a-storyboard"></a>Como aplicar animações com um storyboard  
 Para usar um <xref:System.Windows.Media.Animation.Storyboard> para organizar e aplicar animações, adicione as animações como linhas do tempo filho do <xref:System.Windows.Media.Animation.Storyboard>. O <xref:System.Windows.Media.Animation.Storyboard> classe fornece a <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> e <xref:System.Windows.Media.Animation.Storyboard.TargetProperty?displayProperty=nameWithType> propriedades anexadas. Você pode definir essas propriedades em uma animação para especificar seu objeto de destino e sua propriedade.  
  
 Para aplicar as animações aos seus destinos, começar a <xref:System.Windows.Media.Animation.Storyboard> usando um método ou uma ação de gatilho. Na [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], você usa um <xref:System.Windows.Media.Animation.BeginStoryboard> do objeto com um <xref:System.Windows.EventTrigger>, <xref:System.Windows.Trigger>, ou <xref:System.Windows.DataTrigger>. No código, você também pode usar o <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> método.  
  
 A tabela a seguir mostra os diferentes locais em que cada <xref:System.Windows.Media.Animation.Storyboard> começar técnica tem suporte: por instância, estilo, modelo de controle e modelo de dados. "Por instância" se refere à técnica de aplicar uma animação ou storyboard diretamente às instâncias de um objeto, em vez de um estilo, modelo de controle ou modelo de dados.  
  
|O storyboard é iniciado usando…|Por instância|Estilo|Modelo de controle|Modelo de dados|Exemplo|  
|--------------------------------|-------------------|-----------|----------------------|-------------------|-------------|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> e um <xref:System.Windows.EventTrigger>|Sim|Sim|Sim|Sim|[Animar uma propriedade usando um storyboard](how-to-animate-a-property-by-using-a-storyboard.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> e uma propriedade <xref:System.Windows.Trigger>|Não|Sim|Sim|Sim|[Disparar uma animação quando o valor de uma propriedade é alterado](how-to-trigger-an-animation-when-a-property-value-changes.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> e um <xref:System.Windows.DataTrigger>|Não|Sim|Sim|Sim|[Como: Disparar uma animação quando dados forem alterados](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/aa970679(v=vs.90))|  
|Método <xref:System.Windows.Media.Animation.Storyboard.Begin%2A>|Sim|Não|Não|Não|[Animar uma propriedade usando um storyboard](how-to-animate-a-property-by-using-a-storyboard.md)|  
  
 O exemplo a seguir usa uma <xref:System.Windows.Media.Animation.Storyboard> animar o <xref:System.Windows.FrameworkElement.Width%2A> de uma <xref:System.Windows.Shapes.Rectangle> elemento e o <xref:System.Windows.Media.SolidColorBrush.Color%2A> de um <xref:System.Windows.Media.SolidColorBrush> usado para pintar que <xref:System.Windows.Shapes.Rectangle>.  
  
 [!code-xaml[storyboards_ovw_snip_XAML#1](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#1)]  
  
 [!code-csharp[storyboards_ovw_snip#100](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#100)]  
  
 As seções a seguir descrevem os <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> e <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> propriedades anexadas em mais detalhes.  
  
<a name="targetingelementsandfreezables"></a>   
## <a name="targeting-framework-elements-framework-content-elements-and-freezables"></a>Definindo como destino elementos de estrutura, elementos de conteúdo de estrutura e congeláveis  
 Na seção anterior, mencionamos que, para uma animação encontrar seu destino, ela deve saber o nome do destino e a propriedade a ser animada. Especificando a propriedade a ser animada é muito simples: basta definir <xref:System.Windows.Media.Animation.Storyboard.TargetProperty?displayProperty=nameWithType> com o nome da propriedade a animar.  Você especifica o nome do objeto cuja propriedade você deseja animar definindo a <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> propriedade na animação.  
  
 Para o <xref:System.Windows.Setter.TargetName%2A> propriedade funcione, o objeto de destino deve ter um nome. Atribuir um nome a um <xref:System.Windows.FrameworkElement> ou um <xref:System.Windows.FrameworkContentElement> na [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] é diferente de atribuir um nome para um <xref:System.Windows.Freezable> objeto.  
  
 Os elementos de estrutura são as classes que herdam a <xref:System.Windows.FrameworkElement> classe. Exemplos de elementos de estrutura <xref:System.Windows.Window>, <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Button>, e <xref:System.Windows.Shapes.Rectangle>. Basicamente, todas as janelas, todos os painéis e todos os controles são elementos. Elementos de conteúdo de estrutura são as classes que herdam a <xref:System.Windows.FrameworkContentElement> classe. Exemplos de elementos de conteúdo do framework <xref:System.Windows.Documents.FlowDocument> e <xref:System.Windows.Documents.Paragraph>. Se você não tiver certeza se um tipo é um elemento de estrutura ou um elemento de conteúdo de estrutura, verifique se ele tem uma propriedade Name. Se isso acontecer, provavelmente, ele será um elemento de estrutura ou um elemento de conteúdo de estrutura. Para ter certeza, confira a seção Hierarquia de herança da página de seu tipo.  
  
 Para habilitar o direcionamento de um elemento de estrutura ou um elemento de conteúdo de estrutura no [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], você define sua <xref:System.Windows.FrameworkElement.Name%2A> propriedade. No código, você também precisará usar o <xref:System.Windows.NameScope.RegisterName%2A> método para registrar o nome do elemento com o elemento para o qual você criou um <xref:System.Windows.NameScope>.  
  
 O exemplo a seguir, extraído do exemplo anterior, atribui o nome `MyRectangle` uma <xref:System.Windows.Shapes.Rectangle>, um tipo de <xref:System.Windows.FrameworkElement>.  
  
 [!code-xaml[storyboards_ovw_snip_XAML#2](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#2)]  
  
 [!code-csharp[storyboards_ovw_snip#102](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#102)]  
  
 Depois que ele tiver um nome, você poderá animar uma propriedade desse elemento.  
  
 [!code-xaml[storyboards_ovw_snip_XAML#5](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#5)]  
  
 [!code-csharp[storyboards_ovw_snip#105](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#105)]  
  
 <xref:System.Windows.Freezable> tipos são as classes que herdam a <xref:System.Windows.Freezable> classe. Exemplos de <xref:System.Windows.Freezable> incluem <xref:System.Windows.Media.SolidColorBrush>, <xref:System.Windows.Media.RotateTransform>, e <xref:System.Windows.Media.GradientStop>.  
  
 Para habilitar o direcionamento de uma <xref:System.Windows.Freezable> por uma animação no [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], você usa o [X:Name Directive](../../xaml-services/x-name-directive.md) para atribuir um nome. No código, você deve usar o <xref:System.Windows.NameScope.RegisterName%2A> método para registrar seu nome com o elemento para o qual você criou um <xref:System.Windows.NameScope>.  
  
 O exemplo a seguir atribui um nome para um <xref:System.Windows.Freezable> objeto.  
  
 [!code-xaml[storyboards_ovw_snip_XAML#3](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#3)]  
  
 [!code-csharp[storyboards_ovw_snip#103](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#103)]  
  
 Em seguida, o objeto pode ser o destino de uma animação.  
  
 [!code-xaml[storyboards_ovw_snip_XAML#7](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#7)]  
  
 [!code-csharp[storyboards_ovw_snip#107](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#107)]  
  
 <xref:System.Windows.Media.Animation.Storyboard> objetos usam escopos de nome para resolver o <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> propriedade. Para obter mais informações sobre escopos de nome no WPF, consulte [Escopos de nome XAML no WPF](../advanced/wpf-xaml-namescopes.md). Se o <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> propriedade for omitida, a animação atinge o elemento no qual ela está definida, ou, no caso de estilos, o elemento com estilo.  
  
 Às vezes, um nome não pode ser atribuído a um <xref:System.Windows.Freezable> objeto. Por exemplo, se um <xref:System.Windows.Freezable> é declarado como um recurso ou usado para definir um valor de propriedade em um estilo, ele não pode ser dado um nome. Como ele não tem um nome, ele não pode ser definido como destino diretamente – mas ele pode ser definido como destino indiretamente. As próximas seções descrevem como usar o direcionamento indireto.  
  
<a name="pathsyntaxforchangeable"></a>   
## <a name="indirect-targeting"></a>Direcionamento indireto  
 Há vezes uma <xref:System.Windows.Freezable> não pode ser alvo diretamente de uma animação, por exemplo, quando o <xref:System.Windows.Freezable> é declarado como um recurso ou usado para definir um valor de propriedade em um estilo. Nesses casos, mesmo que você não pode direcionar diretamente, você ainda pode animar o <xref:System.Windows.Freezable> objeto. Em vez de definir a <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> propriedade com o nome da <xref:System.Windows.Freezable>, você dê a ele o nome do elemento ao qual o <xref:System.Windows.Freezable> "pertence". Por exemplo, uma <xref:System.Windows.Media.SolidColorBrush> usado para definir o <xref:System.Windows.Shapes.Shape.Fill%2A> de um retângulo elemento pertence a esse retângulo. Para animar o pincel, você definiria a animação <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> com uma cadeia de propriedades que começa na propriedade do elemento de estrutura ou do elemento de conteúdo de <xref:System.Windows.Freezable> foi usado para definir e termina com o <xref:System.Windows.Freezable> propriedade a ser animada.  
  
 [!code-xaml[storyboards_ovw_snip_XAML#33](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#33)]  
  
 [!code-csharp[storyboards_ovw_snip#134](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#134)]  
  
 Observe que, se o <xref:System.Windows.Freezable> é congelado, um clone será feito e esse clone será animado. Quando isso acontece, o objeto original <xref:System.Windows.Media.Animation.Animatable.HasAnimatedProperties%2A> propriedade continua a retornar `false`, porque o objeto original não é realmente animado. Para obter mais informações sobre a clonagem, consulte o [visão geral de objetos congeláveis](../advanced/freezable-objects-overview.md).  
  
 Observe também que, ao usar o direcionamento indireto de propriedade, é possível definir como destino objetos inexistentes. Por exemplo, você pode pressupor que o <xref:System.Windows.Controls.Control.Background%2A> de um determinado botão foi definido com um <xref:System.Windows.Media.SolidColorBrush> e tentar animar sua Color, quando na verdade um <xref:System.Windows.Media.LinearGradientBrush> foi usado para definir o plano de fundo do botão. Nesses casos, nenhuma exceção é lançada; a animação não tem efeito visível porque <xref:System.Windows.Media.LinearGradientBrush> reage a alterações para o <xref:System.Windows.Media.SolidColorBrush.Color%2A> propriedade.  
  
 As próximas seções descrevem a sintaxe de direcionamento indireto de propriedade mais detalhadamente.  
  
<a name="xamlsyntaxchangeableproperty"></a>   
### <a name="indirectly-targeting-a-property-of-a-freezable-in-xaml"></a>Definindo indiretamente como destino uma propriedade de um congelável em XAML  
 Para selecionar uma propriedade de um congelável em [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], use a seguinte sintaxe.  
  
| |  
|-|  
|*ElementPropertyName* `.` *FreezablePropertyName*|  
  
 Where  
  
- *ElementPropertyName* é a propriedade do <xref:System.Windows.FrameworkElement> que o <xref:System.Windows.Freezable> é usado para definir, e  
  
- *FreezablePropertyName* é a propriedade do <xref:System.Windows.Freezable> animar.  
  
 O código a seguir mostra como animar a <xref:System.Windows.Media.SolidColorBrush.Color%2A> de um <xref:System.Windows.Media.SolidColorBrush> usado para definir o  
  
 <xref:System.Windows.Shapes.Shape.Fill%2A> de um elemento retângulo.  
  
 [!code-xaml[storyboards_ovw_snip_XAML#32](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#32)]  
  
 Às vezes, você precisa ter como destino um congelável contido em uma coleção ou matriz.  
  
 Para definir um congelável como destino contido em uma coleção, use a sintaxe de caminho a seguir.  
  
| |  
|-|  
|*ElementPropertyName* `.Children[` *CollectionIndex* `].` *FreezablePropertyName*|  
  
 Em que *CollectionIndex* é o índice do objeto em sua matriz ou coleção.  
  
 Por exemplo, suponha que um retângulo tem um <xref:System.Windows.Media.TransformGroup> recurso aplicado à sua <xref:System.Windows.UIElement.RenderTransform%2A> propriedade e você deseja animar uma das transformações que ele contém.  
  
 [!code-xaml[storyboards_ovw_snip_XAML#34](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#34)]  
  
 O código a seguir mostra como animar a <xref:System.Windows.Media.RotateTransform.Angle%2A> propriedade do <xref:System.Windows.Media.RotateTransform> mostrado no exemplo anterior.  
  
 [!code-xaml[storyboards_ovw_snip_XAML#35](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#35)]  
  
<a name="targetingpropertyofchangeableincode"></a>   
### <a name="indirectly-targeting-a-property-of-a-freezable-in-code"></a>Definindo indiretamente como destino uma propriedade de um congelável no código  
 No código, você cria um <xref:System.Windows.PropertyPath> objeto. Quando você cria o <xref:System.Windows.PropertyPath>, você especificar um <xref:System.Windows.PropertyPath.Path%2A> e <xref:System.Windows.PropertyPath.PathParameters%2A>.  
  
 Para criar <xref:System.Windows.PropertyPath.PathParameters%2A>, você cria uma matriz do tipo <xref:System.Windows.DependencyProperty> que contém uma lista de campos de identificador de propriedade de dependência. O primeiro campo identificador é para a propriedade do <xref:System.Windows.FrameworkElement> ou <xref:System.Windows.FrameworkContentElement> que o <xref:System.Windows.Freezable> é usado para definir. O próximo campo identificador representa a propriedade do <xref:System.Windows.Freezable> ao destino. Pense nela como uma cadeia de propriedades que se conecta a <xref:System.Windows.Freezable> para o <xref:System.Windows.FrameworkElement> objeto.  
  
 A seguir está um exemplo de uma cadeia de propriedade de dependência que tem como alvo o <xref:System.Windows.Media.SolidColorBrush.Color%2A> de um <xref:System.Windows.Media.SolidColorBrush> usado para definir o <xref:System.Windows.Shapes.Shape.Fill%2A> de um elemento retângulo.  
  
 [!code-csharp[storyboards_ovw_snip#135](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#135)]  
  
 Você também precisará especificar um <xref:System.Windows.PropertyPath.Path%2A>. Um <xref:System.Windows.PropertyPath.Path%2A> é um <xref:System.String> que informa o <xref:System.Windows.PropertyPath.Path%2A> como interpretar seus <xref:System.Windows.PropertyPath.PathParameters%2A>. Ele usa a sintaxe a seguir.  
  
| |  
|-|  
|`(` *OwnerPropertyArrayIndex* `).(` *FreezablePropertyArrayIndex* `)`|  
  
 Where  
  
- *OwnerPropertyArrayIndex* é o índice do <xref:System.Windows.DependencyProperty> matriz que contém o identificador do <xref:System.Windows.FrameworkElement> propriedade do objeto que o <xref:System.Windows.Freezable> é usado para definir, e  
  
- *FreezablePropertyArrayIndex* é o índice do <xref:System.Windows.DependencyProperty> matriz que contém o identificador de propriedade de destino.  
  
 A exemplo a seguir mostra a <xref:System.Windows.PropertyPath.Path%2A> que acompanharia os <xref:System.Windows.PropertyPath.PathParameters%2A> definido no exemplo anterior.
  
 [!code-csharp[storyboards_ovw_snip#PropertyChainAndPath](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#propertychainandpath)]  
  
 O exemplo a seguir combina o código nos exemplos anteriores para animar a <xref:System.Windows.Media.SolidColorBrush.Color%2A> de um <xref:System.Windows.Media.SolidColorBrush> usado para definir o <xref:System.Windows.Shapes.Shape.Fill%2A> de um elemento retângulo.  
  
 [!code-csharp[storyboards_ovw_snip#137](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#137)]  
  
 Às vezes, você precisa ter como destino um congelável contido em uma coleção ou matriz. Por exemplo, suponha que um retângulo tem um <xref:System.Windows.Media.TransformGroup> recurso aplicado à sua <xref:System.Windows.UIElement.RenderTransform%2A> propriedade e você deseja animar uma das transformações que ele contém.  
  
 [!code-xaml[storyboards_ovw_snip#142](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml#142)]  
  
 Para o destino um <xref:System.Windows.Freezable> contido em uma coleção, você use a seguinte sintaxe de caminho.  
  
| |  
|-|  
|`(` *OwnerPropertyArrayIndex* `).(` *CollectionChildrenPropertyArrayIndex* `)` `[` *CollectionIndex* `].(` *FreezablePropertyArrayIndex* `)`|  
  
 Em que *CollectionIndex* é o índice do objeto em sua matriz ou coleção.  
  
 Para o destino o <xref:System.Windows.Media.RotateTransform.Angle%2A> propriedade do <xref:System.Windows.Media.RotateTransform>, a segunda transformação a <xref:System.Windows.Media.TransformGroup>, você usaria o seguinte <xref:System.Windows.PropertyPath.Path%2A> e <xref:System.Windows.PropertyPath.PathParameters%2A>.  
  
 [!code-csharp[storyboards_ovw_snip#139](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#139)]  
  
 O exemplo a seguir mostra o código completo para animar a <xref:System.Windows.Media.RotateTransform.Angle%2A> de um <xref:System.Windows.Media.RotateTransform> contidas dentro de um <xref:System.Windows.Media.TransformGroup>.  
  
 [!code-csharp[storyboards_ovw_snip#138](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#138)]  
  
### <a name="indirectly-targeting-with-a-freezable-as-the-starting-point"></a>Definindo indiretamente como destino um congelável como o ponto de partida  
 As seções anteriores descreveram como definir indiretamente como destino uma <xref:System.Windows.Freezable> começando com um <xref:System.Windows.FrameworkElement> ou <xref:System.Windows.FrameworkContentElement> e a criação de uma cadeia de propriedade para um <xref:System.Windows.Freezable> subpropriedade. Você também pode usar um <xref:System.Windows.Freezable> como uma partida aponte e definir indiretamente como destino um dos seus <xref:System.Windows.Freezable> subpropriedades. Uma restrição adicional se aplica ao usar um <xref:System.Windows.Freezable> como ponto de partida para o direcionamento indireto: iniciais <xref:System.Windows.Freezable> e cada <xref:System.Windows.Freezable> entre ele e a subpropriedade definida indiretamente como destino não devem ser congelados.  
  
<a name="controllable_storyboards"></a>   
## <a name="interactively-controlling-a-storyboard-in-xaml"></a>Controlando um storyboard de forma interativa no XAML  
 Para iniciar um storyboard [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], você usa um <xref:System.Windows.Media.Animation.BeginStoryboard> disparar a ação. <xref:System.Windows.Media.Animation.BeginStoryboard> distribui as animações aos objetos e propriedades que elas animam e inicia o storyboard. (Para obter detalhes sobre esse processo, consulte o [animação e visão geral do sistema de temporização](animation-and-timing-system-overview.md).) Se você conceder a <xref:System.Windows.Media.Animation.BeginStoryboard> um nome especificando sua <xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> propriedade, você tornará um storyboard controlável. Você poderá então controlar o storyboard de forma interativa depois que ele for iniciado. Veja a seguir uma lista de ações de storyboard controlável usadas com gatilhos de evento para controlar um storyboard.  
  
- <xref:System.Windows.Media.Animation.PauseStoryboard>: Pausa o storyboard.  
  
- <xref:System.Windows.Media.Animation.ResumeStoryboard>: Retoma um storyboard em pausa.  
  
- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>: Altera a velocidade do storyboard.  
  
- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>: Avança um storyboard até o final do seu período de preenchimento, se ele tiver um.  
  
- <xref:System.Windows.Media.Animation.StopStoryboard>: Interrompe o storyboard.  
  
- <xref:System.Windows.Media.Animation.RemoveStoryboard>: Remove o storyboard.  
  
 No exemplo a seguir, as ações de storyboard controlável são usadas para controlar um storyboard de forma interativa.  
  
 [!code-xaml[animation_ovws_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snip/CS/ControllableStoryboardExample.xaml#controllablestoryboardexamplewholepage)]  
  
<a name="controllable_storyboards_procedural"></a>   
## <a name="interactively-controlling-a-storyboard-by-using-code"></a>Controlando um storyboard de forma interativa usando um código  
 Os exemplos anteriores mostraram como animar usando ações de gatilho. No código, você também pode controlar um storyboard usando métodos interativos do <xref:System.Windows.Media.Animation.Storyboard> classe. Para um <xref:System.Windows.Media.Animation.Storyboard> para se tornar interativas no código, você deve usar a sobrecarga apropriada do storyboard <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> método e especificar `true` para torná-lo controlável. Consulte o <xref:System.Windows.Media.Animation.Storyboard.Begin%28System.Windows.FrameworkElement%2CSystem.Boolean%29> página para obter mais informações.  
  
 A lista a seguir mostra os métodos que podem ser usados para manipular um <xref:System.Windows.Media.Animation.Storyboard> depois de iniciado:  
  
- <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>  
  
- <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>  
  
- <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>  
  
- <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>  
  
- <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>  
  
- <xref:System.Windows.Media.Animation.Storyboard.Remove%2A>  
  
 A vantagem de usar esses métodos é que você não precisa criar <xref:System.Windows.Trigger> ou <xref:System.Windows.TriggerAction> objetos; basta uma referência para o controlável <xref:System.Windows.Media.Animation.Storyboard> você deseja manipular.  
  
 **Observação:** Todas as ações interativas executadas em um <xref:System.Windows.Media.Animation.Clock>e, portanto, também em um <xref:System.Windows.Media.Animation.Storyboard> ocorrerá no próximo tique do mecanismo de tempo que ocorrerá logo antes da próxima renderização. Por exemplo, se você usar o <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> método para ir para outro ponto em uma animação, o valor da propriedade não é alterado imediatamente, em vez disso, o valor é alterado no próximo tique do mecanismo de temporização.  
  
 O exemplo a seguir mostra como aplicar e controlar as animações usando os métodos interativos do <xref:System.Windows.Media.Animation.Storyboard> classe.  
  
 [!code-csharp[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/ControllableStoryboardExample.cs#controllablestoryboardexamplewholepage)]
 [!code-vb[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/controllablestoryboardexample.vb#controllablestoryboardexamplewholepage)]  
  
<a name="usingstoryboardsinstyles"></a>   
## <a name="animate-in-a-style"></a>Animar em um estilo  
 Você pode usar <xref:System.Windows.Media.Animation.Storyboard> objetos para definir animações em um <xref:System.Windows.Style>. A animação com uma <xref:System.Windows.Media.Animation.Storyboard> em um <xref:System.Windows.Style> é semelhante a usar um <xref:System.Windows.Media.Animation.Storyboard> em outro lugar, com as seguintes três exceções:  
  
- Você não especificar uma <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>; o <xref:System.Windows.Media.Animation.Storyboard> sempre tem como alvo o elemento ao qual o <xref:System.Windows.Style> é aplicado. Destino <xref:System.Windows.Freezable> objetos, você deve usar o direcionamento indireto. Para obter mais informações sobre o direcionamento indireto, consulte o [direcionamento indireto](#pathsyntaxforchangeable) seção.  
  
- Não é possível especificar uma <xref:System.Windows.EventTrigger.SourceName%2A> para um <xref:System.Windows.EventTrigger> ou um <xref:System.Windows.Trigger>.  
  
- Você não pode usar expressões de associação de dados ou referências de recurso dinâmico para definir <xref:System.Windows.Media.Animation.Storyboard> ou valores de propriedade de animação. Isso ocorre porque tudo dentro de um <xref:System.Windows.Style> deve ser thread-safe, e o sistema de temporização deve <xref:System.Windows.Freezable.Freeze%2A> <xref:System.Windows.Media.Animation.Storyboard> objetos para torná-los thread-safe. Um <xref:System.Windows.Media.Animation.Storyboard> não pode ser congelado se ele ou suas linhas do tempo filho contiverem expressões de associação de dados ou referências de recurso dinâmico. Para obter mais informações sobre congelamento e outros <xref:System.Windows.Freezable> recursos, consulte a [visão geral de objetos congeláveis](../advanced/freezable-objects-overview.md).  
  
- Na [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], você não pode declarar manipuladores de eventos para <xref:System.Windows.Media.Animation.Storyboard> ou eventos de animação.  
  
 Para obter um exemplo que mostra como definir um storyboard em um estilo, consulte o [animar em um estilo](how-to-animate-in-a-style.md) exemplo.  
  
<a name="defineAStoryboardInAControlTemplateSection"></a>   
## <a name="animate-in-a-controltemplate"></a>Animar em um ControlTemplate  
 Você pode usar <xref:System.Windows.Media.Animation.Storyboard> objetos para definir animações em um <xref:System.Windows.Controls.ControlTemplate>. A animação com uma <xref:System.Windows.Media.Animation.Storyboard> em um <xref:System.Windows.Controls.ControlTemplate> é semelhante a usar um <xref:System.Windows.Media.Animation.Storyboard> em outro lugar, com as seguintes duas exceções:  
  
- O <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> só podem se referir a objetos filho do <xref:System.Windows.Controls.ControlTemplate>. Se <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> não for especificado, a animação atinge o elemento ao qual o <xref:System.Windows.Controls.ControlTemplate> é aplicado.  
  
- O <xref:System.Windows.EventTrigger.SourceName%2A> para um <xref:System.Windows.EventTrigger> ou um <xref:System.Windows.Trigger> só podem se referir a objetos filho do <xref:System.Windows.Controls.ControlTemplate>.  
  
- Você não pode usar expressões de associação de dados ou referências de recurso dinâmico para definir <xref:System.Windows.Media.Animation.Storyboard> ou valores de propriedade de animação. Isso ocorre porque tudo dentro de um <xref:System.Windows.Controls.ControlTemplate> deve ser thread-safe, e o sistema de temporização deve <xref:System.Windows.Freezable.Freeze%2A> <xref:System.Windows.Media.Animation.Storyboard> objetos para torná-los thread-safe. Um <xref:System.Windows.Media.Animation.Storyboard> não pode ser congelado se ele ou suas linhas do tempo filho contiverem expressões de associação de dados ou referências de recurso dinâmico. Para obter mais informações sobre congelamento e outros <xref:System.Windows.Freezable> recursos, consulte a [visão geral de objetos congeláveis](../advanced/freezable-objects-overview.md).  
  
- Na [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], você não pode declarar manipuladores de eventos para <xref:System.Windows.Media.Animation.Storyboard> ou eventos de animação.  
  
 Para obter um exemplo que mostra como definir um storyboard em um <xref:System.Windows.Controls.ControlTemplate>, consulte o [animar em um ControlTemplate](how-to-animate-in-a-controltemplate.md) exemplo.  
  
<a name="animateWhenAPropertyValueChanges"></a>   
## <a name="animate-when-a-property-value-changes"></a>Animar quando um valor da propriedade é alterado  
 Em estilos e modelos de controle, você pode usar objetos Trigger para iniciar um storyboard quando uma propriedade é alterada. Para obter exemplos, consulte [disparar uma animação quando um valor da propriedade muda](how-to-trigger-an-animation-when-a-property-value-changes.md) e [animar em um ControlTemplate](how-to-animate-in-a-controltemplate.md).  
  
 As animações aplicadas pela propriedade <xref:System.Windows.Trigger> objetos se comportam de maneira mais complexa que <xref:System.Windows.EventTrigger> animações ou animações iniciadas usando <xref:System.Windows.Media.Animation.Storyboard> métodos.  Eles "entrega" com animações definida por outros <xref:System.Windows.Trigger> objetos, mas se compõem com <xref:System.Windows.EventTrigger> e animações disparadas por método.  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da animação](animation-overview.md)
- [Visão geral das técnicas de animação da propriedade](property-animation-techniques-overview.md)
- [Visão geral de objetos congeláveis](../advanced/freezable-objects-overview.md)
