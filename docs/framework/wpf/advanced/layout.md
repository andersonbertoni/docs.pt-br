---
title: Layout
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF layout system [WPF]
- controls [WPF], layout system
- layout system [WPF]
ms.assetid: 3eecdced-3623-403a-a077-7595453a9221
ms.openlocfilehash: 1aa182ced462e5fc90b22019aaf424d400bb4fd5
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68629668"
---
# <a name="layout"></a>Layout
Este tópico descreve o sistema de layout do [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]. Entender como e quando ocorrem os cálculos de layout é essencial para a criação de interfaces do usuário no [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Esse tópico contém as seguintes seções:  
  
- [Caixas delimitadoras de elementos](#LayoutSystem_BoundingBox)  
  
- [O sistema de layout](#LayoutSystem_Overview)  
  
- [Medindo e organizando filhos](#LayoutSystem_Measure_Arrange)  
  
- [Elementos de painel e comportamentos de layout personalizados](#LayoutSystem_PanelsCustom)  
  
- [Considerações sobre desempenho de layout](#LayoutSystem_Performance)  
  
- [Renderização subpixel e arredondamento de layout](#LayoutSystem_LayoutRounding)  
  
- [Novidades](#LayoutSystem_whatsnext)  
  
<a name="LayoutSystem_BoundingBox"></a>   
## <a name="element-bounding-boxes"></a>Caixas delimitadoras de elementos  
 Ao pensar sobre layout no [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], é importante compreender a caixa delimitadora que circunda todos os elementos. Cada <xref:System.Windows.FrameworkElement> um consumido pelo sistema de layout pode ser considerado um retângulo que está encarado no layout. A <xref:System.Windows.Controls.Primitives.LayoutInformation> classe retorna os limites da alocação de layout de um elemento ou slot. O tamanho do retângulo é determinado pelo cálculo do espaço de tela disponível, pelo tamanho de quaisquer restrições, propriedades específicas de layout (como margem e preenchimento) e o comportamento individual do elemento pai <xref:System.Windows.Controls.Panel> . Processando esses dados, o sistema de layout é capaz de calcular a posição de todos os filhos de <xref:System.Windows.Controls.Panel>um específico. É importante lembrar que as características de dimensionamento definidas no elemento pai, como a <xref:System.Windows.Controls.Border>, afetam seus filhos.  
  
 A ilustração a seguir mostra um layout simples.  
  
 ![Captura de tela que mostra uma grade típica, sem a caixa delimitadora sobreposta.](./media/layout/grid-no-bounding-box-superimpose.png)  
  
 Este layout pode ser alcançado usando o seguinte [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-xaml[LayoutInformation#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml#1)]  
  
 Um único <xref:System.Windows.Controls.TextBlock> elemento é hospedado em um <xref:System.Windows.Controls.Grid>. Embora o texto preencha apenas o canto superior esquerdo da primeira coluna, o espaço alocado para o <xref:System.Windows.Controls.TextBlock> é realmente muito maior. A caixa delimitadora de <xref:System.Windows.FrameworkElement> qualquer pode ser recuperada usando <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> o método. A ilustração a seguir mostra a caixa delimitadora <xref:System.Windows.Controls.TextBlock> para o elemento.  
  
 ![Captura de tela que mostra que a caixa delimitadora de TextBlock agora está visível.](./media/layout/visible-textblock-bounding-box.png)  
  
 Conforme mostrado pelo retângulo amarelo, o espaço alocado para o <xref:System.Windows.Controls.TextBlock> elemento é realmente muito maior do que é exibido. À medida que elementos adicionais são adicionados <xref:System.Windows.Controls.Grid>ao, essa alocação pode ser reduzida ou expandida, dependendo do tipo e do tamanho dos elementos que são adicionados.  
  
 O slot de layout do <xref:System.Windows.Controls.TextBlock> é convertido em um <xref:System.Windows.Shapes.Path> usando o <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A> método. Essa técnica pode ser útil para exibir a caixa delimitadora de um elemento.  
  
 [!code-csharp[LayoutInformation#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml.cs#2)]
 [!code-vb[LayoutInformation#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/LayoutInformation/VisualBasic/Window1.xaml.vb#2)]  
  
<a name="LayoutSystem_Overview"></a>   
## <a name="the-layout-system"></a>O sistema de layout  
 Em sua forma mais simples, o layout é um sistema recursivo que leva um elemento a ser dimensionado, posicionado e desenhado. Mais especificamente, layout descreve o processo de medição e organização dos membros da <xref:System.Windows.Controls.Panel> <xref:System.Windows.Controls.Panel.Children%2A> coleção de um elemento. O layout é um processo intensivo. Quanto maior a <xref:System.Windows.Controls.Panel.Children%2A> coleção, maior será o número de cálculos que devem ser feitos. A complexidade também pode ser introduzida com base no comportamento de layout <xref:System.Windows.Controls.Panel> definido pelo elemento que possui a coleção. Uma relativamente simples <xref:System.Windows.Controls.Panel>, <xref:System.Windows.Controls.Canvas>como, pode ter um desempenho significativamente melhor do que um <xref:System.Windows.Controls.Grid>mais <xref:System.Windows.Controls.Panel>complexo, como o.  
  
 Cada vez que um filho <xref:System.Windows.UIElement> altera sua posição, ele tem o potencial de disparar uma nova passagem pelo sistema de layout. Portanto, é importante compreender os eventos que podem invocar o sistema de layout, pois invocações desnecessárias podem levar a desempenho ruim do aplicativo. O exemplo a seguir descreve o processo que ocorre quando o sistema de layout é invocado.  
  
1. Um filho <xref:System.Windows.UIElement> começa o processo de layout, primeiro tendo suas propriedades principais medidas.  
  
2. As propriedades de <xref:System.Windows.FrameworkElement> dimensionamento definidas em são avaliadas, <xref:System.Windows.FrameworkElement.Width%2A>como <xref:System.Windows.FrameworkElement.Margin%2A>, <xref:System.Windows.FrameworkElement.Height%2A>e.  
  
3. <xref:System.Windows.Controls.Panel>a lógica específica é aplicada, <xref:System.Windows.Controls.Dock> como direção ou <xref:System.Windows.Controls.StackPanel.Orientation%2A>empilhamento.  
  
4. O conteúdo é organizado depois que todos os filhos são medidos.  
  
5. A <xref:System.Windows.Controls.Panel.Children%2A> coleção é desenhada na tela.  
  
6. O processo é invocado novamente se <xref:System.Windows.Controls.Panel.Children%2A> forem adicionados adicionais à coleção, um <xref:System.Windows.FrameworkElement.LayoutTransform%2A> será aplicado ou o <xref:System.Windows.UIElement.UpdateLayout%2A> método será chamado.  
  
 Esse processo e como ele é invocado são definidos em mais detalhes nas seções a seguir.  
  
<a name="LayoutSystem_Measure_Arrange"></a>   
## <a name="measuring-and-arranging-children"></a>Medindo e organizando filhos  
 O sistema de layout conclui duas passagens para cada membro da <xref:System.Windows.Controls.Panel.Children%2A> coleção, uma passagem de medida e uma passagem de organização. Cada filho <xref:System.Windows.Controls.Panel> fornece seu próprio <xref:System.Windows.FrameworkElement.MeasureOverride%2A> e <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> seus métodos para obter seu próprio comportamento de layout específico.  
  
 Durante o passo de medida, cada membro da <xref:System.Windows.Controls.Panel.Children%2A> coleção é avaliado. O processo começa com uma chamada para o <xref:System.Windows.UIElement.Measure%2A> método. Esse método é chamado dentro da implementação do elemento pai <xref:System.Windows.Controls.Panel> e não precisa ser chamado explicitamente para que o layout ocorra.  
  
 Primeiro, as propriedades de tamanho nativo <xref:System.Windows.UIElement> de são avaliadas, <xref:System.Windows.UIElement.Clip%2A> como <xref:System.Windows.UIElement.Visibility%2A>e. Isso gera um valor chamado `constraintSize` que é passado para <xref:System.Windows.FrameworkElement.MeasureCore%2A>.  
  
 Em segundo lugar, as propriedades <xref:System.Windows.FrameworkElement> da estrutura definidas em são processadas, `constraintSize`o que afeta o valor de. Essas propriedades geralmente descrevem as características de dimensionamento do <xref:System.Windows.UIElement>subjacente, como <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.Width%2A> <xref:System.Windows.FrameworkElement.Margin%2A>, e <xref:System.Windows.FrameworkElement.Style%2A>. Cada uma dessas propriedades pode alterar o espaço necessário para exibir o elemento. <xref:System.Windows.FrameworkElement.MeasureOverride%2A>é chamado com `constraintSize` como um parâmetro.  
  
> [!NOTE]
>  Há uma diferença entre as <xref:System.Windows.FrameworkElement.Height%2A> Propriedades de <xref:System.Windows.FrameworkElement.ActualHeight%2A> e <xref:System.Windows.FrameworkElement.Width%2A> e e <xref:System.Windows.FrameworkElement.ActualWidth%2A>. Por exemplo, a <xref:System.Windows.FrameworkElement.ActualHeight%2A> propriedade é um valor calculado com base em outras entradas de altura e no sistema de layout. O valor é definido pelo próprio sistema de layout, com base em uma passagem de renderização real, e, portanto, pode atrasar um pouco atrás do valor definido <xref:System.Windows.FrameworkElement.Height%2A>das propriedades, como, que são a base da alteração de entrada.  
>   
>  Como <xref:System.Windows.FrameworkElement.ActualHeight%2A> é um valor calculado, você deve estar ciente de que pode haver várias alterações relatadas e incrementadas para ele como resultado de várias operações pelo sistema de layout. O sistema de layout pode estar calculando o espaço de medição necessário para elementos filhos, as restrições do elemento pai e assim por diante.  
  
 O objetivo final do passo de medida é que o filho Determine seu <xref:System.Windows.UIElement.DesiredSize%2A>, que ocorre durante a <xref:System.Windows.FrameworkElement.MeasureCore%2A> chamada. O <xref:System.Windows.UIElement.DesiredSize%2A> valor é armazenado pelo <xref:System.Windows.UIElement.Measure%2A> para uso durante a passagem de organização de conteúdo.  
  
 A passagem Arrange começa com uma chamada para o <xref:System.Windows.UIElement.Arrange%2A> método. Durante a passagem de Arrange, o <xref:System.Windows.Controls.Panel> elemento pai gera um retângulo que representa os limites do filho. Esse valor é passado para o <xref:System.Windows.FrameworkElement.ArrangeCore%2A> método para processamento.  
  
 O <xref:System.Windows.FrameworkElement.ArrangeCore%2A> método avalia o <xref:System.Windows.UIElement.DesiredSize%2A> do filho e avalia quaisquer margens adicionais que possam afetar o tamanho renderizado do elemento. <xref:System.Windows.FrameworkElement.ArrangeCore%2A>gera um `arrangeSize`, que é passado para o <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> método do <xref:System.Windows.Controls.Panel> como um parâmetro. <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>gera o `finalSize` do filho. Por fim, <xref:System.Windows.FrameworkElement.ArrangeCore%2A> o método faz uma avaliação final das propriedades de deslocamento, como margem e alinhamento, e coloca o filho em seu slot de layout. O filho não precisa preencher o espaço inteiro alocado (e geralmente não faz isso). Em seguida, o controle é retornado <xref:System.Windows.Controls.Panel> para o pai e o processo de layout é concluído.  
  
<a name="LayoutSystem_PanelsCustom"></a>   
## <a name="panel-elements-and-custom-layout-behaviors"></a>Elementos de painel e comportamentos de layout personalizados  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]inclui um grupo de elementos que derivam <xref:System.Windows.Controls.Panel>de. Esses <xref:System.Windows.Controls.Panel> elementos habilitam muitos layouts complexos. Por exemplo, os elementos de empilhamento podem ser facilmente obtidos <xref:System.Windows.Controls.StackPanel> usando o elemento, enquanto layouts de fluxo mais complexos e livres são possíveis <xref:System.Windows.Controls.Canvas>usando um.  
  
 A tabela a seguir resume os elementos de <xref:System.Windows.Controls.Panel> layout disponíveis.  
  
|Nome do painel|Descrição|  
|----------------|-----------------|  
|<xref:System.Windows.Controls.Canvas>|Define uma área na qual você pode posicionar explicitamente elementos filho por coordenadas em relação <xref:System.Windows.Controls.Canvas> à área.|  
|<xref:System.Windows.Controls.DockPanel>|Define uma área dentro da qual você pode organizar elementos filho horizontal ou verticalmente, uns em relação aos outros.|  
|<xref:System.Windows.Controls.Grid>|Define uma área de grade flexível que consiste em colunas e linhas.|  
|<xref:System.Windows.Controls.StackPanel>|Organiza elementos filho em uma única linha que pode ser orientada horizontal ou verticalmente.|  
|<xref:System.Windows.Controls.VirtualizingPanel>|Fornece uma estrutura para os elementos <xref:System.Windows.Controls.Panel> que virtualizam os respectivos dados filho. Esta é uma classe abstrata.|  
|<xref:System.Windows.Controls.WrapPanel>|Coloca os elementos filho na posição sequencial da esquerda para a direita, quebrando o conteúdo para a próxima linha na borda da caixa delimitadora. A ordenação subsequente ocorre sequencialmente de cima para baixo ou da direita para a esquerda, dependendo do valor <xref:System.Windows.Controls.WrapPanel.Orientation%2A> da propriedade.|  
  
 Para aplicativos que exigem um layout que não é possível usando qualquer <xref:System.Windows.Controls.Panel> um dos elementos predefinidos, os comportamentos de layout personalizados podem ser obtidos pela herança <xref:System.Windows.Controls.Panel> e substituição <xref:System.Windows.FrameworkElement.MeasureOverride%2A> dos <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> métodos e. Para obter um exemplo, consulte [Custom Radial Panel Sample](https://go.microsoft.com/fwlink/?LinkID=159982) (Amostra de painel radial personalizado).  
  
<a name="LayoutSystem_Performance"></a>   
## <a name="layout-performance-considerations"></a>Considerações sobre desempenho de layout  
 O layout é um processo recursivo. Cada elemento filho em uma <xref:System.Windows.Controls.Panel.Children%2A> coleção é processado durante cada invocação do sistema de layout. Como resultado, disparar o sistema de layout deve ser evitado quando não for necessário. As considerações a seguir podem ajudá-lo a melhorar o desempenho.  
  
- Esteja ciente de quais alterações de valor da propriedade forçarão uma atualização recursiva realizada pelo sistema de layout.  
  
     As propriedades de dependência cujos valores podem fazer com que o sistema de layout seja inicializado são marcadas com sinalizadores públicos. <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>e <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> fornecem pistas úteis sobre quais alterações de valor de propriedade forçarão uma atualização recursiva pelo sistema de layout. Em geral, qualquer propriedade que possa afetar o tamanho da caixa delimitadora de um elemento deve ter <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> um sinalizador definido como true. Para obter mais informações, consulte [Visão geral sobre propriedades de dependência](dependency-properties-overview.md).  
  
- Quando possível, use um <xref:System.Windows.UIElement.RenderTransform%2A> em vez de <xref:System.Windows.FrameworkElement.LayoutTransform%2A>um.  
  
     Um <xref:System.Windows.FrameworkElement.LayoutTransform%2A> pode ser uma maneira muito útil de afetar o conteúdo de um [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]. No entanto, se o efeito da transformação não tiver que afetar a posição de outros elementos, será melhor usar um <xref:System.Windows.UIElement.RenderTransform%2A> em vez disso, porque <xref:System.Windows.UIElement.RenderTransform%2A> o não invoca o sistema de layout. <xref:System.Windows.FrameworkElement.LayoutTransform%2A>aplica sua transformação e força uma atualização de layout recursivo para considerar a nova posição do elemento afetado.  
  
- Evite chamadas desnecessárias para <xref:System.Windows.UIElement.UpdateLayout%2A>.  
  
     O <xref:System.Windows.UIElement.UpdateLayout%2A> método força uma atualização de layout recursiva e frequentemente não é necessário. A menos que você tenha certeza de que uma atualização completa é necessária, confie no sistema de layout para chamar esse método para você.  
  
- Ao trabalhar com uma grande <xref:System.Windows.Controls.Panel.Children%2A> coleção, considere usar um <xref:System.Windows.Controls.VirtualizingStackPanel> em vez de um <xref:System.Windows.Controls.StackPanel>regular.  
  
     Ao virtualizar a coleção filho, <xref:System.Windows.Controls.VirtualizingStackPanel> o só mantém os objetos na memória que estão no visor do pai. Como resultado, o desempenho é significativamente melhorado na maioria dos cenários.  
  
<a name="LayoutSystem_LayoutRounding"></a>   
## <a name="sub-pixel-rendering-and-layout-rounding"></a>Renderização subpixel e arredondamento de layout  
 O sistema gráfico do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa unidades independentes de dispositivo para habilitar a independência entre resolução e dispositivo. Cada pixel independente de dispositivo é dimensionado automaticamente com a configuração de pontos por polegada (DPI) do sistema. Isso fornece [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aos aplicativos um dimensionamento adequado para diferentes configurações de dpi e torna o aplicativo ciente de DPI automaticamente.  
  
 No entanto, essa independência de DPI pode criar renderização de borda irregular devido à suavização de serrilhado. Esses artefatos, geralmente vistos como bordas desfocadas ou semitransparentes, podem ocorrer quando o local de uma borda está no meio de um pixel de dispositivo, em vez de entre os pixels de dispositivo. O sistema de layout fornece uma maneira de compensar isso com o arredondamento de layout. O arredondamento de layout ocorre quando o sistema de layout arredonda valores de pixel não integrais durante a passagem de layout.  
  
 O arredondamento de layout é desabilitado por padrão. Para habilitar o arredondamento de layout <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> , defina `true` a propriedade <xref:System.Windows.FrameworkElement>como on any. Como essa é uma propriedade de dependência, o valor será propagado para todos os filhos na árvore visual. Para habilitar o arredondamento de layout para a interface <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> do `true` usuário inteira, defina como no contêiner raiz. Para ver um exemplo, consulte <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A>.  
  
<a name="LayoutSystem_whatsnext"></a>   
## <a name="whats-next"></a>Novidades  
 Entender como os elementos são medidos e organizados é o primeiro passo para entender o layout. Para obter mais informações sobre os <xref:System.Windows.Controls.Panel> elementos disponíveis, consulte [visão geral dos painéis](../controls/panels-overview.md). Para compreender melhor as várias propriedades de posicionamento que podem afetar o layout, consulte [Visão geral de alinhamento, margens e preenchimento](alignment-margins-and-padding-overview.md). Para obter um exemplo de um <xref:System.Windows.Controls.Panel> elemento personalizado, consulte [exemplo de painel radial personalizado](https://go.microsoft.com/fwlink/?LinkID=159982). Quando estiver pronto para colocá-lo em um aplicativo leve, consulte [passo a passos: Meu primeiro aplicativo](../getting-started/walkthrough-my-first-wpf-desktop-application.md)de área de trabalho do WPF.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.UIElement>
- [Visão geral de painéis](../controls/panels-overview.md)
- [Visão geral de alinhamento, margens e preenchimento](alignment-margins-and-padding-overview.md)
- [Layout e design](optimizing-performance-layout-and-design.md)
