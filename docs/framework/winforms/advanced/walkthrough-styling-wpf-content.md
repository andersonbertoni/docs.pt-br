---
title: 'Passo a passo: definir o estilo do conteúdo do WPF'
ms.date: 03/30/2017
helpviewer_keywords:
- WPF Designer [Windows Forms], styling WPF content
- interoperability [WDF]
- styles [Windows Forms], WPF content
ms.assetid: e574aac7-7ea4-4cdb-8034-bab541f000df
ms.openlocfilehash: 32ca9658ddf4ab6e8690f29797b7ac7b09df2ca7
ms.sourcegitcommit: d98fdb087d9c8aba7d2cb93fe4b4ee35a2308cee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69012952"
---
# <a name="walkthrough-style-wpf-content"></a>Passo a passo: Conteúdo do WPF de estilo

Essa instrução passo a passo mostra como aplicar estilos a um controle WPF (Windows Presentation Foundation) hospedado em um Windows Form.

 Nesta instrução passo a passo, as seguintes tarefas serão executadas:

- Crie o projeto.

- Crie o tipo de controle WPF.

- Aplique um estilo ao controle do WPF.

## <a name="prerequisites"></a>Pré-requisitos

É necessário o Visual Studio para concluir este passo a passo.

## <a name="create-the-project"></a>Criar o projeto

Abra o Visual Studio e crie um novo projeto de aplicativo Windows Forms em Visual Basic C# ou `StylingWpfContent`Visual chamado.

> [!NOTE]
> Ao hospedar conteúdo do WPF, haverá suporte apenas para projetos em C# e Visual Basic.

## <a name="create-the-wpf-control-types"></a>Criar os tipos de controle do WPF

Depois de adicionar um tipo de controle do WPF ao projeto, você pode hospedá-lo <xref:System.Windows.Forms.Integration.ElementHost> em um controle.

1. Adicione um novo projeto <xref:System.Windows.Controls.UserControl> do WPF à solução. Use o nome padrão do tipo de controle, `UserControl1.xaml`. Para obter mais informações, confira [Passo a passo: Criando novo conteúdo do WPF em Windows Forms em tempo](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)de design.

2. No modo de exibição de Design, verifique se `UserControl1` está selecionado. Para obter mais informações, confira [Como: Selecione e mova elementos no Design Surface](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb514527(v=vs.100)).

3. Na janela **Propriedades** , defina o valor das <xref:System.Windows.FrameworkElement.Width%2A> Propriedades e <xref:System.Windows.FrameworkElement.Height%2A> como `200`.

4. Adicione um <xref:System.Windows.Controls.Button?displayProperty=nameWithType> <xref:System.Windows.Controls.UserControl> controle ao e <xref:System.Windows.Controls.ContentControl.Content%2A> defina o valor da propriedade como **Cancelar**.

5. Adicione um segundo <xref:System.Windows.Controls.Button?displayProperty=nameWithType> controle <xref:System.Windows.Controls.UserControl> ao e <xref:System.Windows.Controls.ContentControl.Content%2A> defina o valor da propriedade como **OK**.

6. Compile o projeto.

## <a name="apply-a-style-to-a-wpf-control"></a>Aplicar um estilo a um controle WPF

Você pode aplicar um estilo diferente a um controle WPF para alterar sua aparência e comportamento.

1. Abra `Form1` no Designer de Formulários do Windows.

1. Na **Caixa de ferramentas**, clique duas vezes em `UserControl1` para criar uma instância de `UserControl1` no formulário.

     Uma instância do `UserControl1` é hospedada em um <xref:System.Windows.Forms.Integration.ElementHost> novo controle `elementHost1`chamado.

1. No painel de smart tag para `elementHost1`, clique em **Editar conteúdo hospedado** na lista suspensa.

     `UserControl1` é aberto no [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].

1. Na exibição XAML, insira o seguinte XAML após a marca de abertura `<UserControl>`.

     Esse XAML cria um gradiente com uma borda gradiente de contraste. Ao clicar no controle, os gradientes são alterados para gerar uma aparência de botão pressionado. Para obter mais informações, consulte [Estilo e modelagem](../../wpf/controls/styling-and-templating.md).

   ```xaml
   <UserControl.Resources>
    <LinearGradientBrush x:Key="NormalBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#FFF" Offset="0.0"/>
        <GradientStop Color="#CCC" Offset="1.0"/>
    </LinearGradientBrush>
    <LinearGradientBrush x:Key="PressedBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#BBB" Offset="0.0"/>
        <GradientStop Color="#EEE" Offset="0.1"/>
        <GradientStop Color="#EEE" Offset="0.9"/>
        <GradientStop Color="#FFF" Offset="1.0"/>
    </LinearGradientBrush>
    <LinearGradientBrush x:Key="NormalBorderBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#CCC" Offset="0.0"/>
        <GradientStop Color="#444" Offset="1.0"/>
    </LinearGradientBrush>
    <LinearGradientBrush x:Key="BorderBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#CCC" Offset="0.0"/>
        <GradientStop Color="#444" Offset="1.0"/>
    </LinearGradientBrush>
    <LinearGradientBrush x:Key="PressedBorderBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#444" Offset="0.0"/>
        <GradientStop Color="#888" Offset="1.0"/>
    </LinearGradientBrush>

    <Style x:Key="SimpleButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="Background" Value="{StaticResource NormalBrush}"/>
        <Setter Property="BorderBrush" Value="{StaticResource NormalBorderBrush}"/>
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="{x:Type Button}">
                    <Grid x:Name="Grid">
                        <Border x:Name="Border" Background="{TemplateBinding Background}" BorderBrush="{TemplateBinding BorderBrush}" BorderThickness="{TemplateBinding BorderThickness}" Padding="{TemplateBinding Padding}"/>
                        <ContentPresenter HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}" Margin="{TemplateBinding Padding}" VerticalAlignment="{TemplateBinding VerticalContentAlignment}" RecognizesAccessKey="True"/>
                    </Grid>
                    <ControlTemplate.Triggers>
                        <Trigger Property="IsPressed" Value="true">
                            <Setter Property="Background" Value="{StaticResource PressedBrush}" TargetName="Border"/>
                            <Setter Property="BorderBrush" Value="{StaticResource PressedBorderBrush}" TargetName="Border"/>
                        </Trigger>
                    </ControlTemplate.Triggers>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
   </UserControl.Resources>
   ```

1. Aplique o estilo `SimpleButton` definido na etapa anterior para o botão Cancelar inserindo o seguinte XAML na marca `<Button>` do botão Cancelar.

   ```xaml
   Style="{StaticResource SimpleButton}
   ```

   A declaração do botão será semelhante ao seguinte XAML:

   ```xaml
   <Button Height="23" Margin="41,52,98,0" Name="button1" VerticalAlignment="Top"
                Style="{StaticResource SimpleButton}">Cancel</Button>
   ```

1. Compile o projeto.

1. Abra `Form1` no Designer de Formulários do Windows.

1. O novo estilo é aplicado ao controle de botão.

1. No menu **Depuração**, selecione **Iniciar Depuração** para executar o aplicativo.

1. Clique nos botões OK e Cancelar e exibir as diferenças.

## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Migração e interoperabilidade](../../wpf/advanced/migration-and-interoperability.md)
- [Usando Controles do WPF](using-wpf-controls.md)
- [Criar o XAML no Visual Studio](/visualstudio/designers/designing-xaml-in-visual-studio)
- [Visão geral de XAML (WPF)](../../wpf/advanced/xaml-overview-wpf.md)
- [Estilo e modelagem](../../wpf/controls/styling-and-templating.md)
