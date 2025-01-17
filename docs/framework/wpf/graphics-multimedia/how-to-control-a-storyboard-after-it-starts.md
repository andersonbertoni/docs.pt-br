---
title: 'Como: Controlar um Storyboard depois de ter começado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboards [WPF], controlling after start
ms.assetid: 040f13f0-69f9-4ab5-be2b-079f4f80c7c0
ms.openlocfilehash: 680676921e14ad69d97f3ee1c39e3ec955e66dec
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662145"
---
# <a name="how-to-control-a-storyboard-after-it-starts"></a>Como: Controlar um Storyboard depois de ter começado
Este exemplo mostra como usar código para controlar um <xref:System.Windows.Media.Animation.Storyboard> depois que ele foi iniciado. Para controlar um storyboard no [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], use <xref:System.Windows.Trigger> e <xref:System.Windows.TriggerAction> objetos; por exemplo, consulte [usar gatilhos de evento para controlar um Storyboard depois de ter começado](how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md).  
  
 Para iniciar um storyboard, use seu <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> método, que distribui as animações do storyboard às propriedades que elas animam e inicia o storyboard.  
  
 Para tornar um storyboard controlável, você deve usar o <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> método e especifique **verdadeiro** como o segundo parâmetro. Em seguida, use os métodos interativos do storyboard para pausar, retomar, procurar, parar, acelerar ou retardar o storyboard ou avançar para seu período de preenchimento. A seguir temos uma lista de métodos interativos de storyboard:  
  
- <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>: Pausa o storyboard.  
  
- <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>: Retoma um storyboard em pausa.  
  
- <xref:System.Windows.Media.Animation.Storyboard.SetSpeedRatio%2A>: Define a velocidade interativa do storyboard.  
  
- <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>: Busca o storyboard no local especificado.  
  
- <xref:System.Windows.Media.Animation.Storyboard.SeekAlignedToLastTick%2A>: Busca o storyboard para o local especificado. Ao contrário de <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> método, essa operação é processado antes da próxima escala.  
  
- <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>: Avança o storyboard para seu período de preenchimento, se ele tiver um.  
  
- <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>: Interrompe o storyboard.  
  
 No exemplo a seguir, diversos métodos de storyboard são usados para controlar de forma interativa um storyboard.  
  
 **Observação:** Para ver um exemplo de como controlar um storyboard usando gatilhos com [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], consulte [usar gatilhos de evento para controlar um Storyboard depois de ter começado](how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md).  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ControlStoryboardExample.cs#controlstoryboardexampleusingwholepage)]
 [!code-vb[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/controlstoryboardexample.vb#controlstoryboardexampleusingwholepage)]  
  
## <a name="see-also"></a>Consulte também

- [Usar gatilhos de evento para controlar um storyboard depois de ter começado](how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)
