---
title: 'Como: Compartilhar dados associados entre formulários usando o componente BindingSource'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- examples [Windows Forms], BindingSource component
- data binding [Windows Forms], sharing data across forms
- BindingSource component [Windows Forms], examples
- BindingSource [Windows Forms], using with multiple forms
ms.assetid: a1a49630-db9c-4485-b888-1f62a373a4f7
ms.openlocfilehash: 28eceaec72053d70885d54bc09179cff743ff71c
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591442"
---
# <a name="how-to-share-bound-data-across-forms-using-the-bindingsource-component"></a>Como: Compartilhar dados associados entre formulários usando o componente BindingSource
Você pode compartilhar facilmente dados entre formulários usando o <xref:System.Windows.Forms.BindingSource> componente. Por exemplo, talvez você queira exibir um formulário de somente leitura que resume os dados de origem de dados e outro formulário editável que contém informações detalhadas sobre o item atualmente selecionado na fonte de dados. Este exemplo demonstra esse cenário.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como compartilhar um <xref:System.Windows.Forms.BindingSource> e seus dados associados entre formulários. Neste exemplo, o compartilhado <xref:System.Windows.Forms.BindingSource> é passado para o construtor do formulário filho. O formulário filho permite que o usuário edite os dados para o atualmente item selecionado no formulário principal.  
  
> [!NOTE]
>  O <xref:System.Windows.Forms.BindingSource.BindingComplete> evento para o <xref:System.Windows.Forms.BindingSource> componente é tratado no exemplo para garantir que os dois formulários permaneçam sincronizados. Para obter mais informações sobre por que isso é feito, consulte [como: Certifique-se de vários controles associados à mesma fonte de dados permaneçam sincronizados](../multiple-controls-bound-to-data-source-synchronized.md).  
  
 [!code-csharp[System.Windows.Forms.BindingSourceMultipleForms#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleForms/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingSourceMultipleForms#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleForms/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Este exemplo requer:  
  
- Referências aos assemblies System, System.Windows.Forms, System.Drawing, System.Data e System.Xml.  
  
## <a name="see-also"></a>Consulte também

- [Componente BindingSource](bindingsource-component.md)
- [Associação de dados do Windows Forms](../windows-forms-data-binding.md)
- [Como: Tratar erros e exceções que ocorrem na associação de dados](how-to-handle-errors-and-exceptions-that-occur-with-databinding.md)
