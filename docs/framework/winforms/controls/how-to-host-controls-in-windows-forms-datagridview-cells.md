---
title: 'Como: Hospedar controles em células DataGridView do Windows Forms'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [Windows Forms], hosting in cells
- DataGridView control [Windows Forms], hosting controls in cells
- cells [Windows Forms], hosting controls
ms.assetid: e79a9d4e-64ec-41f5-93ec-f5492633cbb2
ms.openlocfilehash: 20b9f33b31df9145205a13b8649153e51d840a6c
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592444"
---
# <a name="how-to-host-controls-in-windows-forms-datagridview-cells"></a>Como: Hospedar controles em células DataGridView do Windows Forms
O <xref:System.Windows.Forms.DataGridView> controle fornece vários tipos de coluna, permitindo que os usuários insiram e editem valores em uma variedade de formas. No entanto, se esses tipos de coluna não atenderem às suas necessidades de entrada de dados, será possível criar seus próprios tipos de coluna com células que hospedam controles de sua escolha. Para fazer isso, você deve definir classes que derivam de <xref:System.Windows.Forms.DataGridViewColumn> e <xref:System.Windows.Forms.DataGridViewCell>. Você também deve definir uma classe que deriva de <xref:System.Windows.Forms.Control> e implementa o <xref:System.Windows.Forms.IDataGridViewEditingControl> interface.  
  
 O exemplo de código a seguir mostra como criar uma coluna de calendário. As células desta coluna exibem datas nas células de caixa de texto comum, mas quando o usuário edita uma célula, um <xref:System.Windows.Forms.DateTimePicker> controle aparece. Para evitar a necessidade de implementar a funcionalidade de exibição da caixa de texto novamente, o `CalendarCell` classe deriva de <xref:System.Windows.Forms.DataGridViewTextBoxCell> classe em vez de herdar a <xref:System.Windows.Forms.DataGridViewCell> classe diretamente.  
  
> [!NOTE]
>  Quando você deriva <xref:System.Windows.Forms.DataGridViewCell> ou <xref:System.Windows.Forms.DataGridViewColumn> e adicionar novas propriedades à classe derivada, certifique-se de substituir o `Clone` método para copiar as novas propriedades durante operações de clonagem. Você também deve chamar o método `Clone` da classe base para que as propriedades da classe base sejam copiadas para a nova célula ou coluna.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[System.Windows.Forms.DataGridViewCalendarColumn#000](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCalendarColumn/CS/datagridviewcalendarcolumn.cs#000)]
 [!code-vb[System.Windows.Forms.DataGridViewCalendarColumn#000](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCalendarColumn/VB/datagridviewcalendarcolumn.vb#000)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 O exemplo a seguir requer:  
  
- Referências aos assemblies Sistema e System.Windows.Forms.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewColumn>
- <xref:System.Windows.Forms.DataGridViewCell>
- <xref:System.Windows.Forms.DataGridViewTextBoxCell>
- <xref:System.Windows.Forms.IDataGridViewEditingControl>
- <xref:System.Windows.Forms.DateTimePicker>
- [Personalizando o controle DataGridView dos Windows Forms](customizing-the-windows-forms-datagridview-control.md)
- [Arquitetura de controle DataGridView](datagridview-control-architecture-windows-forms.md)
- [Tipos de coluna no controle DataGridView dos Windows Forms](column-types-in-the-windows-forms-datagridview-control.md)
