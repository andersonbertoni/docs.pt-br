---
title: 'Passo a passo: habilitar arrastar e soltar em um controle de usuário'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- walkthrough [WPF], drag-and-drop
- drag-and-drop [WPF], walkthrough
ms.assetid: cc844419-1a77-4906-95d9-060d79107fc7
ms.openlocfilehash: 80fd55be9230729cb8336be91c1d8fb4f7f3f080
ms.sourcegitcommit: 30a83efb57c468da74e9e218de26cf88d3254597
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2019
ms.locfileid: "68364255"
---
# <a name="walkthrough-enabling-drag-and-drop-on-a-user-control"></a>Passo a passo: habilitar arrastar e soltar em um controle de usuário

Este passo a passo demonstra como criar um controle de usuário personalizado que pode participar na transferência de dados por arrastar e soltar no [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].

Neste tutorial, você criará um WPF <xref:System.Windows.Controls.UserControl> personalizado que representa uma forma de círculo. Você implementará a funcionalidade no controle para permitir a transferência de dados por meio de arrastar e soltar. Por exemplo, se você arrastar de um controle do círculo para outro, os dados de cor de preenchimento serão copiados do círculo de origem para o destino. Se você arrastar de um controle de círculo para <xref:System.Windows.Controls.TextBox>um, a representação de cadeia de caracteres da cor de preenchimento <xref:System.Windows.Controls.TextBox>será copiada para o. Você também criará um pequeno aplicativo que contém dois controles de painel e <xref:System.Windows.Controls.TextBox> um para testar a funcionalidade de arrastar e soltar. Será gravado um código que permite que os painéis processem os dados do círculo que foram soltos, o que permitirá mover ou copiar círculos da coleção de filhos de um painel para o outro.

Esta explicação passo a passo ilustra as seguintes tarefas:

- Crie um controle de usuário personalizado.

- Habilite o controle de usuário como uma fonte de arrastar.

- Habilite o controle de usuário como um destino de soltar.

- Habilite um painel para receber dados que foram soltos pelo controle de usuário.

## <a name="prerequisites"></a>Pré-requisitos

É necessário o Visual Studio para concluir este passo a passo.

## <a name="create-the-application-project"></a>Criar o projeto de aplicativo
 Nesta seção, você criará a infraestrutura do aplicativo, que inclui uma página principal com dois painéis e um <xref:System.Windows.Controls.TextBox>.

1. Crie um novo projeto de aplicativo do WPF no Visual Basic ou no Visual C#, chamado `DragDropExample`. Para obter mais informações, confira [Passo a passo: Meu primeiro aplicativo](../getting-started/walkthrough-my-first-wpf-desktop-application.md)de área de trabalho do WPF.

2. Abra MainWindow.xaml.

3. Adicione a marcação a seguir entre as marcas de <xref:System.Windows.Controls.Grid> abertura e de fechamento.

     Essa marcação cria a interface do usuário para o aplicativo de teste.

     [!code-xaml[DragDropWalkthrough#PanelsStep1XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep1xaml)]

## <a name="add-a-new-user-control-to-the-project"></a>Adicionar um novo controle de usuário ao projeto
 Nesta seção, você adicionará um novo controle de usuário ao projeto.

1. No menu Projeto, selecione **Adicionar controle de usuário**.

2. Na caixa de diálogo **Adicionar novo item** , altere o nome para `Circle.xaml`e clique em **Adicionar**.

     O Circle.xaml e seu code-behind são adicionados ao projeto.

3. Abra o Circle.xaml.

     Esse arquivo conterá os elementos de interface do usuário do controle de usuário.

4. Adicione a seguinte marcação à raiz <xref:System.Windows.Controls.Grid> para criar um controle de usuário simples que tenha um círculo azul como sua interface do usuário.

     [!code-xaml[DragDropWalkthrough#EllipseXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#ellipsexaml)]

5. Abra Circle.xaml.cs ou Circle.xaml.vb.

6. No C#, adicione o código a seguir após o construtor sem parâmetros para criar um construtor de cópia. Em Visual Basic, adicione o código a seguir para criar um construtor sem parâmetros e um construtor de cópia.

     Para permitir que o controle de usuário seja copiado, você pode adicionar um método de construtor de cópia no arquivo code-behind. No controle de usuário simplificado do círculo, será copiado apenas o preenchimento e o tamanho do controle de usuário.

     [!code-csharp[DragDropWalkthrough#CopyCtor](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#copyctor)]
     [!code-vb[DragDropWalkthrough#CopyCtor](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#copyctor)]

## <a name="add-the-user-control-to-the-main-window"></a>Adicionar o controle de usuário à janela principal

1. Abra MainWindow.xaml.

2. Adicione o XAML a seguir à marca <xref:System.Windows.Window> de abertura para criar uma referência de namespace XML para o aplicativo atual.

    ```
    xmlns:local="clr-namespace:DragDropExample"
    ```

3. Na primeira <xref:System.Windows.Controls.StackPanel>, adicione o XAML a seguir para criar duas instâncias do controle de usuário de círculo no primeiro painel.

     [!code-xaml[DragDropWalkthrough#CirclesXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#circlesxaml)]

     O XAML completo para o painel tem a aparência a seguir.

     [!code-xaml[DragDropWalkthrough#PanelsStep2XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep2xaml)]

## <a name="implement-drag-source-events-in-the-user-control"></a>Implementar eventos de arrastar origem no controle de usuário
 Nesta seção, você substituirá o <xref:System.Windows.UIElement.OnMouseMove%2A> método e iniciará a operação de arrastar e soltar.

 Se um arrastar for iniciado (um botão do mouse for pressionado e o mouse for movido), você empacotará os dados a serem transferidos para <xref:System.Windows.DataObject>um. Nesse caso, o controle do círculo empacotará três itens de dados; uma representação de cadeia de caracteres da cor de preenchimento, uma representação dupla da altura e uma cópia de si mesmo.

### <a name="to-initiate-a-drag-and-drop-operation"></a>Para iniciar uma operação do tipo “arrastar e soltar”

1. Abra Circle.xaml.cs ou Circle.xaml.vb.

2. Adicione a substituição <xref:System.Windows.UIElement.OnMouseMove%2A> a seguir para fornecer manipulação de classe <xref:System.Windows.UIElement.MouseMove> para o evento.

     [!code-csharp[DragDropWalkthrough#OnMouseMove](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#onmousemove)]
     [!code-vb[DragDropWalkthrough#OnMouseMove](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#onmousemove)]

     Essa <xref:System.Windows.UIElement.OnMouseMove%2A> substituição executa as seguintes tarefas:

    - Verifica se o botão esquerdo do mouse é pressionado enquanto o mouse se move.

    - Empacota os dados de círculo em <xref:System.Windows.DataObject>um. Nesse caso, o controle do círculo empacota três itens de dados; uma representação de cadeia de caracteres da cor de preenchimento, uma representação dupla da altura e uma cópia de si mesmo.

    - Chama o método <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=nameWithType> estático para iniciar a operação de arrastar e soltar. Você passa os três parâmetros a seguir para <xref:System.Windows.DragDrop.DoDragDrop%2A> o método:

        - `dragSource` – Uma referência para esse controle.

        - `data`– O <xref:System.Windows.DataObject> criado no código anterior.

        - `allowedEffects`– As operações de arrastar e soltar permitidas, que são <xref:System.Windows.DragDropEffects.Copy> ou <xref:System.Windows.DragDropEffects.Move>.

3. Pressione **F5** para compilar e executar o aplicativo.

4. Clique em um dos controles de círculo e arraste-o sobre os painéis, o outro círculo e <xref:System.Windows.Controls.TextBox>o. Ao arrastar sobre o <xref:System.Windows.Controls.TextBox>, o cursor é alterado para indicar uma movimentação.

5. Ao arrastar um círculo sobre o <xref:System.Windows.Controls.TextBox>, pressione a tecla **Ctrl** . Observe como o cursor muda para indicar uma cópia.

6. Arraste e solte um círculo no <xref:System.Windows.Controls.TextBox>. A representação de cadeia de caracteres da cor de preenchimento do círculo é anexada ao <xref:System.Windows.Controls.TextBox>.

     ![Representação de cadeia de caracteres da cor de preenchimento do círculo](./media/dragdrop-colorstring.png "DragDrop_ColorString")

Por padrão, o cursor será alterado durante uma operação do tipo “arrastar e soltar” para indicar qual será o efeito de soltar os dados. Você pode personalizar os comentários fornecidos ao usuário manipulando o <xref:System.Windows.UIElement.GiveFeedback> evento e definindo um cursor diferente.

## <a name="give-feedback-to-the-user"></a>Enviar comentários para o usuário

1. Abra Circle.xaml.cs ou Circle.xaml.vb.

2. Adicione a substituição <xref:System.Windows.UIElement.OnGiveFeedback%2A> a seguir para fornecer manipulação de classe <xref:System.Windows.UIElement.GiveFeedback> para o evento.

     [!code-csharp[DragDropWalkthrough#OnGiveFeedback](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ongivefeedback)]
     [!code-vb[DragDropWalkthrough#OnGiveFeedback](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ongivefeedback)]

     Essa <xref:System.Windows.UIElement.OnGiveFeedback%2A> substituição executa as seguintes tarefas:

    - Verifica os <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> valores que são definidos no manipulador de <xref:System.Windows.UIElement.DragOver> eventos de soltar destino.

    - Define um cursor personalizado com base no <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> valor. O cursor deve fornecer comentários visuais ao usuário a respeito de qual será o efeito de soltar os dados.

3. Pressione **F5** para compilar e executar o aplicativo.

4. Arraste um dos controles de círculo sobre os painéis, o outro círculo e o <xref:System.Windows.Controls.TextBox>. Observe que os cursores são agora os cursores personalizados que você especificou na <xref:System.Windows.UIElement.OnGiveFeedback%2A> substituição.

     ![Arraste e solte com os cursores personalizados](./media/dragdrop-customcursor.png "DragDrop_CustomCursor")

5. Selecione o texto `green` <xref:System.Windows.Controls.TextBox>do.

6. Arraste o texto `green` para um controle do círculo. Observe que os cursores padrão são mostrados para indicar os efeitos da operação do tipo “arrastar e soltar”. O cursor de comentários sempre é definido pela fonte de arrastar.

## <a name="implement-drop-target-events-in-the-user-control"></a>Implementar eventos de soltar destino no controle de usuário
 Nesta seção, você especificará que o controle de usuário é um destino de soltar, substituirá os métodos que permitem que o controle de usuário seja um destino de soltar e processará os dados soltos nele.

### <a name="to-enable-the-user-control-to-be-a-drop-target"></a>Para permitir que o controle de usuário seja um destino de soltar

1. Abra o Circle.xaml.

2. Na marca de <xref:System.Windows.Controls.UserControl> abertura, adicione a <xref:System.Windows.UIElement.AllowDrop%2A> Propriedade e defina-a `true`como.

     [!code-xaml[DragDropWalkthrough#UCTagXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#uctagxaml)]

O <xref:System.Windows.UIElement.OnDrop%2A> método é chamado quando a <xref:System.Windows.UIElement.AllowDrop%2A> propriedade é definida como `true` e os dados da fonte de arrastar são descartados no controle de usuário de círculo. Nesse método, você processará os dados que foram soltos e aplicará os dados ao círculo.

### <a name="to-process-the-dropped-data"></a>Para processar os dados soltos

1. Abra Circle.xaml.cs ou Circle.xaml.vb.

2. Adicione a substituição <xref:System.Windows.UIElement.OnDrop%2A> a seguir para fornecer manipulação de classe <xref:System.Windows.UIElement.Drop> para o evento.

     [!code-csharp[DragDropWalkthrough#OnDrop](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondrop)]
     [!code-vb[DragDropWalkthrough#OnDrop](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondrop)]

     Essa <xref:System.Windows.UIElement.OnDrop%2A> substituição executa as seguintes tarefas:

    - Usa o <xref:System.Windows.DataObject.GetDataPresent%2A> método para verificar se os dados arrastados contêm um objeto de cadeia de caracteres.

    - Usa o <xref:System.Windows.DataObject.GetData%2A> método para extrair os dados de cadeia de caracteres, se estiverem presentes.

    - Usa um <xref:System.Windows.Media.BrushConverter> para tentar converter a cadeia de caracteres em <xref:System.Windows.Media.Brush>um.

    - Se a conversão for bem-sucedida, o aplicará o pincel <xref:System.Windows.Shapes.Shape.Fill%2A> ao <xref:System.Windows.Shapes.Ellipse> do que fornece a interface do usuário do controle de círculo.

    - Marca o <xref:System.Windows.UIElement.Drop> evento como manipulado. O evento de soltar deve ser marcado como manipulado para que os outros elementos que o recebem saibam que foi manipulado pelo controle de usuário do círculo.

3. Pressione **F5** para compilar e executar o aplicativo.

4. Selecione o texto `green` <xref:System.Windows.Controls.TextBox>no.

5. Arraste o texto para um controle do círculo e solte-o. O círculo muda de azul para verde.

     ![Converta uma cadeia de caracteres em um pincel](./media/dragdrop-dropgreentext.png "DragDrop_DropGreenText")

6. Digite o texto `green` <xref:System.Windows.Controls.TextBox>no.

7. Selecione o texto `gre` <xref:System.Windows.Controls.TextBox>no.

8. Arraste-o para um controle do círculo e solte-o. Observe que o cursor muda para indicar que é permitido soltar; porém, a cor do círculo não muda, porque `gre` não é uma cor válida.

9. Arraste do controle do círculo verde e solte no controle do círculo azul. O círculo muda de azul para verde. Observe que o cursor mostrado depende de se o <xref:System.Windows.Controls.TextBox> círculo ou é a origem do arrasto.

Definir a <xref:System.Windows.UIElement.AllowDrop%2A> propriedade para `true` e processar os dados descartados é tudo o que é necessário para permitir que um elemento seja um destino de soltar. No entanto, para fornecer uma melhor experiência do usuário, você também <xref:System.Windows.UIElement.DragEnter>deve <xref:System.Windows.UIElement.DragLeave>manipular os <xref:System.Windows.UIElement.DragOver> eventos, e. Nesses eventos, é possível executar verificações e fornecer comentários adicionais ao usuário antes de soltar os dados.

Quando dados são arrastados sobre o controle de usuário do círculo, o controle deve notificar a fonte de arrasto se os dados arrastados podem ser processados. Se o controle não souber como processar os dados, deverá recusá-los quando forem soltos. Para fazer isso, você manipulará o <xref:System.Windows.UIElement.DragOver> evento e definirá <xref:System.Windows.DragEventArgs.Effects%2A> a propriedade.

### <a name="to-verify-that-the-data-drop-is-allowed"></a>Para verificar se é permitido soltar os dados

1. Abra Circle.xaml.cs ou Circle.xaml.vb.

2. Adicione a substituição <xref:System.Windows.UIElement.OnDragOver%2A> a seguir para fornecer manipulação de classe <xref:System.Windows.UIElement.DragOver> para o evento.

     [!code-csharp[DragDropWalkthrough#OnDragOver](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragover)]
     [!code-vb[DragDropWalkthrough#OnDragOver](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragover)]

     Essa <xref:System.Windows.UIElement.OnDragOver%2A> substituição executa as seguintes tarefas:

    - Define a propriedade <xref:System.Windows.DragEventArgs.Effects%2A> como <xref:System.Windows.DragDropEffects.None>.

    - Executa as mesmas verificações que são executadas no <xref:System.Windows.UIElement.OnDrop%2A> método para determinar se o controle de usuário de círculo pode processar os dados arrastados.

    - Se o controle de usuário puder processar os dados, o <xref:System.Windows.DragEventArgs.Effects%2A> definirá <xref:System.Windows.DragDropEffects.Copy> a <xref:System.Windows.DragDropEffects.Move>Propriedade como ou.

3. Pressione **F5** para compilar e executar o aplicativo.

4. Selecione o texto `gre` <xref:System.Windows.Controls.TextBox>no.

5. Arraste o texto para um controle do círculo. Observe que, agora, o cursor muda para indicar que não é permitido soltar, porque `gre` não é uma cor válida.

 É possível aprimorar ainda mais a experiência do usuário por meio da aplicação de uma visualização da operação do tipo “soltar”. Para o controle de usuário de círculo, você substituirá <xref:System.Windows.UIElement.OnDragLeave%2A> os <xref:System.Windows.UIElement.OnDragEnter%2A> métodos e. Quando os dados são arrastados sobre o controle, o plano <xref:System.Windows.Shapes.Shape.Fill%2A> de fundo atual é salvo em uma variável de espaço reservado. Em seguida, a cadeia de caracteres é convertida em um <xref:System.Windows.Shapes.Ellipse> pincel e aplicada ao que fornece a interface do usuário do círculo. Se os dados forem arrastados para fora do círculo sem serem descartados <xref:System.Windows.Shapes.Shape.Fill%2A> , o valor original será aplicado novamente ao círculo.

### <a name="to-preview-the-effects-of-the-drag-and-drop-operation"></a>Para visualizar os efeitos da operação do tipo “arrastar e soltar”

1. Abra Circle.xaml.cs ou Circle.xaml.vb.

2. Na classe Circle, declare uma variável privada <xref:System.Windows.Media.Brush> chamada `_previousFill` e a inicialize como `null`.

     [!code-csharp[DragDropWalkthrough#Brush](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#brush)]
     [!code-vb[DragDropWalkthrough#Brush](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#brush)]

3. Adicione a substituição <xref:System.Windows.UIElement.OnDragEnter%2A> a seguir para fornecer manipulação de classe <xref:System.Windows.UIElement.DragEnter> para o evento.

     [!code-csharp[DragDropWalkthrough#OnDragEnter](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragenter)]
     [!code-vb[DragDropWalkthrough#OnDragEnter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragenter)]

     Essa <xref:System.Windows.UIElement.OnDragEnter%2A> substituição executa as seguintes tarefas:

    - Salva a <xref:System.Windows.Shapes.Shape.Fill%2A> propriedade <xref:System.Windows.Shapes.Ellipse> do na `_previousFill` variável.

    - Executa as mesmas verificações que são executadas no <xref:System.Windows.UIElement.OnDrop%2A> método para determinar se os dados podem ser convertidos em um. <xref:System.Windows.Media.Brush>

    - Se os dados forem convertidos em um <xref:System.Windows.Media.Brush>válido, o o aplicará <xref:System.Windows.Shapes.Shape.Fill%2A> ao <xref:System.Windows.Shapes.Ellipse>do.

4. Adicione a substituição <xref:System.Windows.UIElement.OnDragLeave%2A> a seguir para fornecer manipulação de classe <xref:System.Windows.UIElement.DragLeave> para o evento.

     [!code-csharp[DragDropWalkthrough#OnDragLeave](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragleave)]
     [!code-vb[DragDropWalkthrough#OnDragLeave](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragleave)]

     Essa <xref:System.Windows.UIElement.OnDragLeave%2A> substituição executa as seguintes tarefas:

    - Aplica o <xref:System.Windows.Media.Brush> `_previousFill` salvo <xref:System.Windows.Shapes.Shape.Fill%2A> na<xref:System.Windows.Shapes.Ellipse> variável ao do que fornece a interface do usuário do controle de usuários de círculo.

5. Pressione **F5** para compilar e executar o aplicativo.

6. Selecione o texto `green` <xref:System.Windows.Controls.TextBox>no.

7. Arraste o texto sobre um controle do círculo sem soltá-lo. O círculo muda de azul para verde.

     ![Visualize os efeitos de uma operação do tipo “arrastar&#45;e&#45;soltar”](./media/dragdrop-previeweffects.png "DragDrop_PreviewEffects")

8. Arraste o texto para fora do controle do círculo. O círculo volta de verde para azul.

## <a name="enable-a-panel-to-receive-dropped-data"></a>Habilitar um painel para receber dados descartados

Nesta seção, você habilita os painéis que hospedam os controles de usuário de círculo para atuar como destinos de soltar para dados de círculo arrastados. Você implementará o código que permite mover um círculo de um painel para outro ou para fazer uma cópia de um controle de círculo mantendo pressionada a tecla **Ctrl** enquanto arrasta e solta um círculo.

1. Abra MainWindow.xaml.

2. Conforme mostrado no XAML a seguir, em cada um dos <xref:System.Windows.Controls.StackPanel> controles, adicione manipuladores para os <xref:System.Windows.UIElement.DragOver> eventos <xref:System.Windows.UIElement.Drop> e. Nomeie o <xref:System.Windows.UIElement.DragOver> manipulador de eventos `panel_DragOver`, e nomeie o <xref:System.Windows.UIElement.Drop> manipulador de eventos `panel_Drop`,.

     [!code-xaml[DragDropWalkthrough#PanelsXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml#panelsxaml)]

3. Abra MainWindows.xaml.cs ou MainWindow.xaml.vb.

4. Adicione o código a seguir para <xref:System.Windows.UIElement.DragOver> o manipulador de eventos.

     [!code-csharp[DragDropWalkthrough#PanelDragOver](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldragover)]
     [!code-vb[DragDropWalkthrough#PanelDragOver](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldragover)]

     Esse <xref:System.Windows.UIElement.DragOver> manipulador de eventos executa as seguintes tarefas:

    - Verifica se os dados arrastados contêm os dados de "objeto" que foram empacotados <xref:System.Windows.DataObject> no pelo controle de usuário de círculo e passados na chamada <xref:System.Windows.DragDrop.DoDragDrop%2A>para.

    - Se os dados de "objeto" estiverem presentes, o verificará se a tecla **Ctrl** foi pressionada.

    - Se a tecla **Ctrl** for pressionada, definirá a <xref:System.Windows.DragDropEffects.Copy> <xref:System.Windows.DragEventArgs.Effects%2A> Propriedade como. Caso contrário, defina <xref:System.Windows.DragEventArgs.Effects%2A> a propriedade <xref:System.Windows.DragDropEffects.Move>como.

5. Adicione o código a seguir para <xref:System.Windows.UIElement.Drop> o manipulador de eventos.

     [!code-csharp[DragDropWalkthrough#PanelDrop](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldrop)]
     [!code-vb[DragDropWalkthrough#PanelDrop](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldrop)]

     Esse <xref:System.Windows.UIElement.Drop> manipulador de eventos executa as seguintes tarefas:

    - Verifica se o <xref:System.Windows.UIElement.Drop> evento já foi tratado. Por exemplo, se um círculo for descartado em outro círculo que manipula o <xref:System.Windows.UIElement.Drop> evento, você não desejará que o painel que contém o círculo também o manipule.

    - Se o <xref:System.Windows.UIElement.Drop> evento não for tratado, o verificará se a tecla **Ctrl** foi pressionada.

    - Se a **tecla CTRL** for pressionada quando <xref:System.Windows.UIElement.Drop> acontecer, o fará uma cópia do controle de círculo e a <xref:System.Windows.Controls.Panel.Children%2A> adicionará à coleção do <xref:System.Windows.Controls.StackPanel>.

    - Se a tecla **Ctrl** não for pressionada, o moverá o <xref:System.Windows.Controls.Panel.Children%2A> círculo da coleção de seu painel pai <xref:System.Windows.Controls.Panel.Children%2A> para a coleção do painel em que foi Descartado.

    - Define a <xref:System.Windows.DragEventArgs.Effects%2A> propriedade para notificar <xref:System.Windows.DragDrop.DoDragDrop%2A> o método se uma operação de movimentação ou cópia foi executada.

6. Pressione **F5** para compilar e executar o aplicativo.

7. Selecione o texto `green` <xref:System.Windows.Controls.TextBox>do.

8. Arraste o texto sobre um controle do círculo e solte-o.

9. Arraste um controle do círculo do painel esquerdo para o painel direito e solte-o. O círculo é removido da <xref:System.Windows.Controls.Panel.Children%2A> coleção do painel esquerdo e adicionado à coleção Children do painel direito.

10. Arraste um controle de círculo do painel no qual ele está no outro painel e solte-o enquanto pressiona a tecla **Ctrl** . O círculo é copiado e a cópia é adicionada à <xref:System.Windows.Controls.Panel.Children%2A> coleção do painel de recebimento.

     ![Arrastando um círculo enquanto pressiona a tecla CTRL](./media/dragdrop-paneldrop.png "DragDrop_PanelDrop")

## <a name="see-also"></a>Consulte também

- [Visão geral de arrastar e soltar](drag-and-drop-overview.md)
