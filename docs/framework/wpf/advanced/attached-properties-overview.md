---
title: Visão geral das propriedades anexadas
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- attached properties [WPF Designer]
ms.assetid: 75928354-dc01-47e8-a018-8409aec1f32d
ms.openlocfilehash: 2eacb0ff49b868f144bf35af4bb64b7d049b30cb
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401378"
---
# <a name="attached-properties-overview"></a>Visão geral das propriedades anexadas

Uma propriedade anexada é um conceito definido por XAML. Uma propriedade anexada deve ser utilizada como um tipo de propriedade global configurável em qualquer objeto. No [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], as propriedades anexadas normalmente são definidas como uma forma especializada de propriedade de dependência que não tem a propriedade “wrapper” convencional.

## Pré-requisitos<a name="prerequisites"></a>

Este tópico pressupõe que você entende as propriedades de dependência da perspectiva de um consumidor de propriedades de dependência existentes nas classes [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] e que leu a [Visão geral das propriedades de dependência](dependency-properties-overview.md). Para seguir os exemplos neste tópico, você também deve entender o XAML e saber como escrever aplicativos WPF.

## Por que usar propriedades anexadas<a name="attached_properties_usage"></a>

Uma das finalidades de uma propriedade anexada é permitir que diferentes elementos filho especifiquem valores exclusivos para uma propriedade que, na verdade, é definida em um elemento pai. Um aplicativo específico desse cenário é quando elementos filho informam ao elemento pai como devem ser apresentados no [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]. Um exemplo é a <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> propriedade. A <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> propriedade é criada como uma propriedade anexada porque foi projetada para ser definida em elementos que estão contidos em um <xref:System.Windows.Controls.DockPanel>, em vez de <xref:System.Windows.Controls.DockPanel> em si. A <xref:System.Windows.Controls.DockPanel> classe define o campo <xref:System.Windows.DependencyProperty> estático chamado <xref:System.Windows.Controls.DockPanel.DockProperty>e, em seguida, <xref:System.Windows.Controls.DockPanel.GetDock%2A> fornece <xref:System.Windows.Controls.DockPanel.SetDock%2A> os métodos e como acessadores públicos para a propriedade anexada.

## Propriedades anexadas em XAML<a name="attached_properties_xaml"></a>

Em XAML, as propriedades anexadas são definidas por meio do uso da sintaxe *AttachedPropertyProvider*.*PropertyName*

Veja a seguir um exemplo de como você pode definir <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> em XAML:

[!code-xaml[PropertiesOvwSupport#APBasicUsage](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml#apbasicusage)]

Observe que o uso é um pouco semelhante a uma propriedade estática; Você sempre referencia o tipo <xref:System.Windows.Controls.DockPanel> que possui e registra a propriedade anexada, em vez de se referir a qualquer instância especificada por nome.

Além disso, como uma propriedade anexada em XAML é um atributo definido na marcação, somente a operação de conjuntos tem alguma relevância. Não é possível obter uma propriedade diretamente em XAML, apesar de existirem alguns mecanismos indiretos para comparar valores, como gatilhos em estilos (para mais detalhes, consulte [Estilo e modelagem](../controls/styling-and-templating.md)).

### <a name="attached-property-implementation-in-wpf"></a>Implementação de propriedades anexadas no WPF

No [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], a maioria das propriedades anexadas que existem em tipos do WPF relacionados à apresentação da interface do usuário são implementadas como propriedades de dependência. As propriedades anexadas são um conceito XAML, enquanto as propriedades de dependência são um conceito do WPF. Como as propriedades anexadas do WPF são propriedades de dependência, elas dão suporte a conceitos de propriedade de dependência, como metadados de propriedade, e valores padrão dos metadados de propriedade.

## Como as propriedades anexadas são usadas pelo tipo proprietário<a name="howused"></a>

Embora as propriedades anexadas possam ser definidas em qualquer objeto, isso não significa, automaticamente, que a definição da propriedade produzirá um resultado tangível ou que o valor será usado por outro objeto. Em geral, as propriedades anexadas são criadas para que os objetos provenientes de uma grande variedade de hierarquias de classe possíveis ou relações lógicas possam reportar informações comuns para o tipo que define a propriedade anexada. O tipo que define a propriedade anexada normalmente segue um destes modelos:

- O tipo que define a propriedade anexada é concebido para que possa ser o elemento pai dos elementos que definirão valores para a propriedade anexada. Em seguida, o tipo itera os objetos filho por meio de lógica interna com relação a algumas estruturas de árvore de objeto, obtém os valores e age sobre eles de alguma maneira.

- O tipo que define a propriedade anexada será usado como elemento filho para vários elementos pai e modelos de conteúdo possíveis.

- O tipo que define a propriedade anexada representa um serviço. Outros tipos definem valores para a propriedade anexada. A seguir, quando o elemento que define a propriedade é avaliado no contexto do serviço, os valores da propriedade anexada são obtidos por meio da lógica interna da classe de serviço.

### <a name="an-example-of-a-parent-defined-attached-property"></a>Um exemplo de propriedade anexada definida pelo pai

O cenário mais comum em que o WPF define uma propriedade anexada é quando um elemento pai dá suporte a uma coleção de elementos filho e também implementa um comportamento em que as especificidades do comportamento são relatadas individualmente para cada elemento filho.

<xref:System.Windows.Controls.DockPanel>define a <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> Propriedade anexada e <xref:System.Windows.Controls.DockPanel> tem código de nível de classe como parte de sua lógica de renderização ( <xref:System.Windows.Controls.DockPanel.MeasureOverride%2A> especificamente <xref:System.Windows.Controls.DockPanel.ArrangeOverride%2A>, e). Uma <xref:System.Windows.Controls.DockPanel> instância sempre verificará se algum de seus elementos filho imediatos definiu um valor para <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>. Nesse caso, tais valores se tornam uma entrada para a lógica de renderização aplicada ao elemento filho em questão. As <xref:System.Windows.Controls.DockPanel> instâncias aninhadas tratam suas próprias coleções de elementos filho imediatos, mas esse comportamento é específico <xref:System.Windows.Controls.DockPanel> da <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> implementação para o modo como os valores de processos são processados. Teoricamente, é possível ter propriedades anexadas que influenciam elementos além do pai imediato. Se a <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> Propriedade anexada estiver definida em um elemento que não <xref:System.Windows.Controls.DockPanel> tem nenhum elemento pai para agir sobre ela, nenhum erro ou exceção será gerado. Isso simplesmente significa que um valor de propriedade global foi definido, mas ele não tem <xref:System.Windows.Controls.DockPanel> um pai atual que possa consumir as informações.

## Propriedades anexadas no código<a name="attached_properties_code"></a>

As propriedades anexadas no WPF não têm os métodos "wrapper" do CLR típicos para acesso de Get/Set fácil. Isso ocorre porque a propriedade anexada não é necessariamente parte do namespace CLR para instâncias em que a propriedade está definida. No entanto, um processador XAML deve ser capaz de definir esses valores quando o XAML for analisado. Para dar suporte a um uso de Propriedade anexado efetivo, o tipo de proprietário da propriedade anexada deve implementar métodos de acessadores dedicados no formato **Get_PropertyName_** e **Set_PropertyName_** . Esses métodos de acesso dedicados também são úteis para obter ou definir a propriedade anexada em código. De uma perspectiva de código, uma propriedade anexada é semelhante a um campo de suporte que tem métodos de acesso em vez de acessadores de propriedade; além disso, o campo de suporte pode existir em qualquer objeto, sem precisar ser definido especificamente.

O exemplo a seguir mostra como você pode definir uma propriedade anexada em código. Neste exemplo, `myCheckBox` é uma instância <xref:System.Windows.Controls.CheckBox> da classe.

[!code-csharp[PropertiesOvwSupport#APCode](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#apcode)]
[!code-vb[PropertiesOvwSupport#APCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#apcode)]

Semelhante ao caso XAML, se `myCheckBox` ainda não havia sido adicionado como um elemento filho de `myDockPanel` pela terceira linha de código, a quarta linha de código não geraria uma exceção, mas o valor da propriedade não interagiria com um <xref:System.Windows.Controls.DockPanel> pai e, portanto, Não faria nada. Somente um <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> valor definido em um elemento filho combinado com a presença de um <xref:System.Windows.Controls.DockPanel> elemento pai causará um comportamento efetivo no aplicativo renderizado. (Nesse caso, você poderia definir a propriedade anexada e anexar à árvore. Uma alternativa é anexar à árvore e, em seguida, definir a propriedade anexada. A ordem das ações gera o mesmo resultado.)

## Metadados de Propriedade anexado<a name="attached_properties_metadata"></a>

Ao registrar a propriedade, <xref:System.Windows.FrameworkPropertyMetadata> é definido para especificar as características da propriedade, como se a propriedade afeta a renderização, a medida e assim por diante. Em geral, os metadados de uma propriedade anexada não diferem dos metadados de uma propriedade de dependência. Se você especificar um valor padrão em uma substituição para metadados da propriedade anexada, esse valor vai se tornar o valor padrão da propriedade anexada implícita em instâncias da classe de substituição. Especificamente, o valor padrão será relatado se algum processo consultar o valor de uma propriedade anexada por meio do acessador do método `Get` para essa propriedade, especificando uma instância da classe em que os metadados foram especificados, e caso o valor dessa propriedade anexada não tenha sido definido de outra maneira.

Se você desejar habilitar a herança de valor da propriedade em uma propriedade, deverá usar propriedades anexadas em vez de propriedades de dependência não anexadas. Para obter detalhes, consulte [Herança do valor da propriedade](property-value-inheritance.md).

## Propriedades anexadas personalizadas<a name="custom"></a>

### Quando criar uma propriedade anexada<a name="create_attached_properties"></a>

É possível criar uma propriedade anexada quando há um motivo para ter um mecanismo de configuração de propriedade disponível para classes diferentes da classe de definição. O cenário mais comum para isso é o layout. Exemplos de propriedades de layout existentes <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>são <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType>, e <xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=nameWithType>. O cenário habilitado aqui é que os elementos que existem como elementos filho para elementos de controle do layout conseguem expressar os requisitos de layout para os elementos pai de layout individualmente, sendo que cada um configura um valor da propriedade que o pai definiu como propriedade anexada.

Outro cenário para usar uma propriedade anexada é quando a classe representa um serviço, e você deseja que classes possam integrar o serviço de forma mais transparente.

Outro cenário é receber suporte ao designer do WPF do Visual Studio, como a edição da janela **Propriedades** . Para obter mais informações, consulte [Visão geral da criação de controle](../controls/control-authoring-overview.md).

Como mencionado anteriormente, será necessário registrar como propriedade anexada se você quiser usar a herança de valor da propriedade.

### Como criar uma propriedade anexada<a name="how_do_i_create_attached_properties"></a>

Se sua classe estiver definindo a propriedade anexada estritamente para uso em outros tipos, a classe não precisará derivar de <xref:System.Windows.DependencyObject>. Mas você precisa derivar de <xref:System.Windows.DependencyObject> se você seguir o modelo do WPF geral de ter sua propriedade anexada também é uma propriedade de dependência.

Defina a propriedade anexada como uma propriedade de dependência declarando `public static readonly` um <xref:System.Windows.DependencyProperty>campo do tipo. Você define esse campo usando o valor de retorno do <xref:System.Windows.DependencyProperty.RegisterAttached%2A> método. O nome do campo deve corresponder ao nome da propriedade anexada, acrescentado com `Property`a cadeia de caracteres, para seguir o padrão WPF estabelecido de nomear os campos de identificação versus as propriedades que eles representam. O provedor de propriedades anexada também deve fornecer métodos **Get_PropertyName_** e **Set_PropertyName_** estáticos como acessadores para a propriedade anexada; a falha em fazer isso fará com que o sistema de propriedades não possa usar sua propriedade anexada.

> [!NOTE]
> Se você omitir o acessador get da propriedade anexada, a vinculação de dados na propriedade não funcionará em ferramentas de design, como o Visual Studio e o Expression Blend.

#### <a name="the-get-accessor"></a>O acessador get

A assinatura para o acessador **Get_PropertyName_** deve ser:

`public static object GetPropertyName(object target)`

- O objeto `target` pode ser especificado como um tipo mais específico na sua implementação. Por exemplo, o <xref:System.Windows.Controls.DockPanel.GetDock%2A?displayProperty=nameWithType> método digita o parâmetro como <xref:System.Windows.UIElement>, porque a propriedade anexada destina-se apenas a ser <xref:System.Windows.UIElement> definida em instâncias.

- O valor retornado pode ser especificado como um tipo mais específico na sua implementação. Por exemplo, o <xref:System.Windows.Controls.DockPanel.GetDock%2A> método o digita como <xref:System.Windows.Controls.Dock>, porque o valor só pode ser definido como essa enumeração.

#### <a name="the-set-accessor"></a>O acessador set

A assinatura para o acessador **Set_PropertyName_** deve ser:

`public static void SetPropertyName(object target, object value)`

- O objeto `target` pode ser especificado como um tipo mais específico na sua implementação. Por exemplo, o <xref:System.Windows.Controls.DockPanel.SetDock%2A> método o digita como <xref:System.Windows.UIElement>, porque a propriedade anexada destina-se apenas a ser <xref:System.Windows.UIElement> definida em instâncias.

- O objeto `value` pode ser especificado como um tipo mais específico na sua implementação. Por exemplo, o <xref:System.Windows.Controls.DockPanel.SetDock%2A> método o digita como <xref:System.Windows.Controls.Dock>, porque o valor só pode ser definido como essa enumeração. Lembre-se de que o valor para esse método é a entrada proveniente do carregador de XAML, quando ele encontra a propriedade anexada em um uso da propriedade anexada na marcação. Essa entrada é o valor especificado como um valor de atributo XAML na marcação. Portanto, deve haver conversão de tipo, serializador de valores ou suporte à extensão de marcação para o tipo que usar, de modo que o tipo adequado possa ser criado por meio do valor do atributo (que é, basicamente, apenas uma cadeia de caracteres).

O exemplo a seguir mostra o registro de propriedade de dependência <xref:System.Windows.DependencyProperty.RegisterAttached%2A> (usando o método), bem como os acessadores **Get_PropertyName_** e **Set_PropertyName_** . No exemplo, o nome da propriedade anexada é `IsBubbleSource`. Portanto, os acessadores devem ser nomeados como `GetIsBubbleSource` e `SetIsBubbleSource`.

[!code-csharp[WPFAquariumSln#RegisterAttachedBubbler](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerattachedbubbler)]
[!code-vb[WPFAquariumSln#RegisterAttachedBubbler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerattachedbubbler)]

#### <a name="attached-property-attributes"></a>Atributos de propriedade anexada

O WPF define [!INCLUDE[TLA2#tla_netframewkattr#plural](../../../../includes/tla2sharptla-netframewkattrsharpplural-md.md)] vários que se destinam a fornecer informações sobre propriedades anexadas a processos de reflexão e a usuários típicos de informações de reflexão e propriedade, como designers. Como as propriedades anexadas têm um tipo de escopo ilimitado, os designers precisam de uma maneira de evitar sobrecarregar os usuários com uma lista global de todas as propriedades anexadas que são definidas em uma implementação de tecnologia específica que usa XAML. O [!INCLUDE[TLA2#tla_netframewkattr#plural](../../../../includes/tla2sharptla-netframewkattrsharpplural-md.md)] WPF que define para propriedades anexadas pode ser usado para definir o escopo das situações em que uma determinada propriedade anexada deve ser mostrada em uma janela de propriedades. Você também pode considerar a possibilidade de aplicar esses atributos para suas próprias propriedades anexadas personalizadas. A finalidade e a sintaxe do [!INCLUDE[TLA2#tla_netframewkattr#plural](../../../../includes/tla2sharptla-netframewkattrsharpplural-md.md)] é descrita nas páginas de referência adequadas:

- <xref:System.Windows.AttachedPropertyBrowsableAttribute>

- <xref:System.Windows.AttachedPropertyBrowsableForChildrenAttribute>

- <xref:System.Windows.AttachedPropertyBrowsableForTypeAttribute>

- <xref:System.Windows.AttachedPropertyBrowsableWhenAttributePresentAttribute>

## Aprendendo mais sobre propriedades anexadas<a name="more"></a>

- Para obter mais informações sobre como criar uma propriedade anexada, consulte [Registrar uma propriedade anexada](how-to-register-an-attached-property.md).

- Para ver mais cenários de uso avançados para as propriedades de dependência e as propriedades anexadas, consulte [Propriedades de dependência personalizada](custom-dependency-properties.md).

- Também é possível registrar uma propriedade como propriedade anexada e como propriedade de dependência, mas ainda expor implementações de “wrapper”. Nesse caso, a propriedade pode ser definida nesse elemento ou em qualquer elemento por meio da sintaxe de propriedade anexada XAML. Um exemplo de uma propriedade com um cenário apropriado para os usos padrão e anexado é <xref:System.Windows.FrameworkElement.FlowDirection%2A?displayProperty=nameWithType>.

## <a name="see-also"></a>Consulte também

- <xref:System.Windows.DependencyProperty>
- [Visão geral das propriedades da dependência](dependency-properties-overview.md)
- [Propriedades de dependência personalizada](custom-dependency-properties.md)
- [Visão geral de XAML (WPF)](xaml-overview-wpf.md)
- [Registrar uma propriedade anexada](how-to-register-an-attached-property.md)
