---
title: 'Como: desenhar texto com o GDI'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- GDI [Windows Forms], drawing text [Windows Forms]
- text [Windows Forms], drawing with TextRenderer
- drawing [Windows Forms], text
- Windows Forms, drawing text with GDI
ms.assetid: 2a19fe5d-2ace-451c-94db-01cb1118ef7b
ms.openlocfilehash: 3d5b79e82185c044314ff8807b86835ef6a87c45
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505912"
---
# <a name="how-to-draw-text-with-gdi"></a>Como: desenhar texto com o GDI
Com o <xref:System.Windows.Forms.TextRenderer.DrawText%2A> método no <xref:System.Windows.Forms.TextRenderer> classe, você pode acessar a funcionalidade GDI para desenhar texto em um formulário ou controle. Renderização de texto GDI normalmente oferece melhor desempenho e medição de GDI+ de texto mais preciso.  
  
> [!NOTE]
>  O <xref:System.Windows.Forms.TextRenderer.DrawText%2A> métodos do <xref:System.Windows.Forms.TextRenderer> classe não dá suporte para impressão. Ao imprimir, sempre use a <xref:System.Drawing.Graphics.DrawString%2A> métodos do <xref:System.Drawing.Graphics> classe.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como desenhar texto em várias linhas dentro de um retângulo usando o <xref:System.Windows.Forms.TextRenderer.DrawText%2A> método.  
  
 [!code-csharp[System.Windows.Forms.TextRendererExamples#7](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/CS/Form1.cs#7)]
 [!code-vb[System.Windows.Forms.TextRendererExamples#7](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/VB/Form1.vb#7)]  
  
 Para renderizar o texto com o <xref:System.Windows.Forms.TextRenderer> classe, é necessário um <xref:System.Drawing.IDeviceContext>, como um <xref:System.Drawing.Graphics> e um <xref:System.Drawing.Font>, um local para desenhar o texto e a cor em que ele deve ser desenhado. Opcionalmente, você pode especificar o texto de formatação usando a <xref:System.Windows.Forms.TextFormatFlags> enumeração.  
  
 Para obter mais informações sobre como obter um <xref:System.Drawing.Graphics>, consulte [como: Criar objetos gráficos para desenho](how-to-create-graphics-objects-for-drawing.md). Para obter mais informações sobre como construir uma <xref:System.Drawing.Font>, consulte [como: Construir fontes e famílias de fontes](how-to-construct-font-families-and-fonts.md).  
  
## <a name="compiling-the-code"></a>Compilando o código  
 O exemplo de código anterior foi projetado para uso com o Windows Forms e requer o <xref:System.Windows.Forms.PaintEventArgs> `e`, que é um parâmetro de <xref:System.Windows.Forms.PaintEventHandler>.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.TextRenderer>
- <xref:System.Drawing.Font>
- <xref:System.Drawing.Color>
- [Usando fontes e texto](using-fonts-and-text.md)
