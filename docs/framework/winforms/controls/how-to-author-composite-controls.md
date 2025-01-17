---
title: 'Como: Criar controles compostos'
ms.date: 03/30/2017
helpviewer_keywords:
- UserControl class [Windows Forms], creating composite controls
- user controls [Windows Forms], creating
- user controls [Windows Forms], inheriting from
- composite controls [Windows Forms], creating
ms.assetid: 79c9cf05-5ab6-4a18-886d-88a64748b098
ms.openlocfilehash: 7b0ee8efa62175e2ced2a810ca6dd76e8adc103b
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69039889"
---
# <a name="how-to-author-composite-controls"></a>Como: Criar controles compostos

Os controles de composição podem ser usados de várias maneiras. É possível criá-los como parte de um projeto de aplicativo da área de trabalho do Windows e usá-los somente em formulários do projeto. Também é possível criá-los em um projeto da Biblioteca de Controles do Windows, compilar o projeto em um assembly e usar os controles em outros projetos. Você pode até mesmo herdar deles e usar a herança visual para personalizá-los rapidamente para fins especiais.

> [!NOTE]
> Caso queira criar um controle de composição para usar no Web Forms, consulte [Desenvolvendo Controles de Servidores ASP.NET Personalizados](https://docs.microsoft.com/previous-versions/aspnet/zt27tfhy(v=vs.100)).

## <a name="to-author-a-composite-control"></a>Criar um controle de composição

1. No Visual Studio, crie um novo projeto de **aplicativo** do `DemoControlHost`Windows chamado.

2. No menu **projeto** , clique em **Adicionar controle de usuário**.

3. Na caixa de diálogo **Adicionar Novo Item**, dê ao arquivo de classe (arquivo .vb ou .cs) o nome que você deseja que o controle de composição tenha.

4. Selecione o botão **Adicionar** para criar o arquivo de classe para o controle composto.

5. Adicione os controles da **Caixa de Ferramentas** à superfície do controle de composição.

6. Coloque o código em procedimentos de evento, a fim de manipular eventos gerados pelo controle de composição ou por seus controles constituintes.

7. Feche o designer do controle de composição e salve o arquivo quando solicitado.

8. No menu **Compilar**, clique em **Compilar Solução**.

     O projeto deve ser criado para que os controles personalizados apareçam na **Caixa de Ferramentas**.

9. Use a guia **DemoControlHost** da **Caixa de Ferramentas** para adicionar instâncias do controle ao `Form1`.

## <a name="to-author-a-control-class-library"></a>Criar uma biblioteca de classes de controle

1. Abra um novo projeto da **Biblioteca de Controles do Windows**.

     Por padrão, o projeto contém um controle de composição.

2. Adicione controles e código, conforme descrito no procedimento acima.

3. Escolha um controle que as classes de herança não alterarão e defina a propriedade **Modificadores** desse controle como **Privada**.

4. Compile a DLL.

## <a name="to-inherit-from-a-composite-control-in-a-control-class-library"></a>Herdar de um controle de composição em uma biblioteca de classes de controle

1. No menu **Arquivo**, aponte para **Adicionar** e selecione **Novo Projeto** para adicionar um novo projeto dos **Aplicativos do Windows** à solução.

2. No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Referências** do novo projeto e escolha **Adicionar Referência** para abrir a caixa de diálogo **Adicionar Referência**.

3. Selecione a guia **Projetos** e clique duas vezes no projete de biblioteca de controle.

4. No menu **Compilar**, clique em **Compilar Solução**.

5. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de biblioteca de controle e selecione **Adicionar Novo Item** no menu de atalho.

6. Selecione o modelo **Controle de Usuário Herdado** na caixa de diálogo **Adicionar Novo Item**.

7. Na caixa de diálogo **Selecionador de Herança**, clique duas vezes no controle do qual você deseja herdar.

     Um novo controle será adicionado ao projeto.

8. Abra o designer visual do novo controle e adicione outros controles constituintes.

     É possível ver os controles constituintes que foram herdados do controle composição na DLL e alterar as propriedades de controles cuja propriedade **Modificadores** for **Pública**. Não é possível alterar as propriedades do controle cuja propriedade **Modificadores** for **Privada**.

## <a name="see-also"></a>Consulte também

- [Passo a passo: Criando um controle composto com Visual Basic](walkthrough-authoring-a-composite-control-with-visual-basic.md)
- [Passo a passo: Criando um controle composto com VisualC#](walkthrough-authoring-a-composite-control-with-visual-csharp.md)
- [Passo a passo: Herdar de um controle de Windows Forms com Visual Basic](walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)
- [Passo a passo: Herdar de um controle de Windows Forms com o VisualC#](walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)
- [Recomendações do Tipo de Controle](control-type-recommendations.md)
- [Como: Controles de autor para Windows Forms](how-to-author-controls-for-windows-forms.md)
- [Variedades de controles personalizados](varieties-of-custom-controls.md)
