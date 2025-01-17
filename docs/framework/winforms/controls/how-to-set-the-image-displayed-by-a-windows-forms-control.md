---
title: 'Como: Definir a imagem exibida por um controle do Windows Forms'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Button control [Windows Forms], images
- Windows Forms controls, images
- controls [Windows Forms], images
- images [Windows Forms], Windows Forms controls
- examples [Windows Forms], controls
ms.assetid: 9445af8f-4f62-48b0-a3f6-068058964b9f
ms.openlocfilehash: 99bde4fac7b3057358c7e6a8550efdb4cc351eb0
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69037875"
---
# <a name="how-to-set-the-image-displayed-by-a-windows-forms-control"></a>Como: Definir a imagem exibida por um controle de Windows Forms

Vários controles de Windows Forms podem exibir imagens. Essas imagens podem ser ícones que esclarecem a finalidade do controle, como um ícone de disquete em um botão que indica o comando **salvar** . Como alternativa, os ícones podem ser imagens de plano de fundo para dar ao controle a aparência e o comportamento que você deseja.

## <a name="to-set-the-image-displayed-by-a-control"></a>Para definir a imagem exibida por um controle

1. Defina a propriedade `Image` ou `BackgroundImage` o controle como um objeto do tipo <xref:System.Drawing.Image>. Em geral, você carregará a imagem de um arquivo usando o <xref:System.Drawing.Image.FromFile%2A> método.

     No exemplo de código a seguir, o caminho definido para o local da imagem é a pasta **minhas imagens** . A maioria dos computadores que executam o sistema operacional Windows incluirá esse diretório. Isso também permite que os usuários com níveis mínimos de acesso do sistema executem o aplicativo com segurança. O exemplo de código a seguir requer que você já tenha um formulário <xref:System.Windows.Forms.PictureBox> com um controle adicionado.

    ```vb
    ' Replace the image named below
    ' with an icon of your own choosing.
    PictureBox1.Image = Image.FromFile _
       (System.Environment.GetFolderPath _
       (System.Environment.SpecialFolder.MyPictures) _
       & "\Image.gif")
    ```

    ```csharp
    // Replace the image named below
    // with an icon of your own choosing.
    // Note the escape character used (@) when specifying the path.
    pictureBox1.Image = Image.FromFile
       (System.Environment.GetFolderPath
       (System.Environment.SpecialFolder.MyPictures)
       + @"\Image.gif");
    ```

    ```cpp
    // Replace the image named below
    // with an icon of your own choosing.
    pictureBox1->Image = Image::FromFile(String::Concat
       (System::Environment::GetFolderPath
       (System::Environment::SpecialFolder::MyPictures),
       "\\Image.gif"));
    ```

## <a name="see-also"></a>Consulte também

- <xref:System.Drawing.Image.FromFile%2A>
- <xref:System.Drawing.Image>
- <xref:System.Windows.Forms.Control.BackgroundImage%2A>
