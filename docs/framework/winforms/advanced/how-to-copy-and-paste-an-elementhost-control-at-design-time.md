---
title: 'Como: copiar e colar um controle ElementHost em tempo de design'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, content copying and pasting
- interoperability [WPF]
- ElementHost control [Windows Forms], copying and pasting at design time
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: e570375d-2a68-44ba-b4f7-c781af2d20e8
ms.openlocfilehash: 0f3367deaaec04744a3f812d7f2d08047d7eb588
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211377"
---
# <a name="how-to-copy-and-paste-an-elementhost-control-at-design-time"></a>Como: copiar e colar um controle ElementHost em tempo de design

Este procedimento mostra como copiar um controle Windows Presentation Foundation (WPF) em um formulário do Windows no Visual Studio.

## <a name="copy-and-paste-an-elementhost-control-at-design-time"></a>Copiar e colar um controle ElementHost em tempo de design

1. Adicione um novo WPF <xref:System.Windows.Controls.UserControl> ao seu projeto de formulários do Windows. Use o nome padrão do tipo de controle, `UserControl1.xaml`. Para obter mais informações, confira [Passo a passo: Criando novo conteúdo WPF nos Windows Forms em tempo de Design](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md).

2. No **propriedades** janela, defina o valor da <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> propriedades do `UserControl1` para `200`.

3. Definir o valor de <xref:System.Windows.Controls.Control.Background%2A> propriedade para `Blue`.

4. Compile o projeto.

5. Abra `Form1` no Designer de Formulários do Windows.

6. Da **Caixa de Ferramentas**, arraste uma instância de `UserControl1` para o formulário.

   Uma instância do `UserControl1` é hospedado em uma nova <xref:System.Windows.Forms.Integration.ElementHost> controle chamado `elementHost1`.

7. Com `elementHost1` selecionado, pressione CTRL+C para copiá-lo para a área de transferência.

8. Pressione CTRL + V para colar o controle copiado para o formulário.

   Uma nova <xref:System.Windows.Forms.Integration.ElementHost> controle chamado `elementHost2` é criado no formulário.

## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Migração e interoperabilidade](../../wpf/advanced/migration-and-interoperability.md)
- [Usando Controles do WPF](using-wpf-controls.md)
- [Criar o XAML no Visual Studio](/visualstudio/designers/designing-xaml-in-visual-studio)
