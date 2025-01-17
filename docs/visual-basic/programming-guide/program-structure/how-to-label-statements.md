---
title: 'Como: Rótulo de instruções (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- colons (:)
- statements [Visual Basic], labels
- ': separator character'
- Visual Basic code, labeling statements
ms.assetid: 38f1ff43-2054-42cb-963b-1998e60c6ed4
ms.openlocfilehash: cbb80d94dc8280aa67859c89daad1520ce4e9669
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648740"
---
# <a name="how-to-label-statements-visual-basic"></a>Como: Rótulo de instruções (Visual Basic)
Blocos de instrução são compostos de linhas de código delimitado por vírgulas. Linhas de código precedida por um inteiro ou cadeia de caracteres de identificação são consideradas *rotulado*. Rótulos de instrução são usados para marcar uma linha de código para identificá-lo para uso com instruções de como `On Error Goto`.  
  
 Rótulos podem ser qualquer um dos identificadores válidos do Visual Basic — como aquelas que identificam os elementos de programação — ou literais inteiros. Um rótulo deve aparecer no início de uma linha de código-fonte e deve ser seguido por dois-pontos, independentemente se ele é seguido por uma instrução na mesma linha.  
  
 O compilador identifica rótulos, verificando se o início da linha corresponde a qualquer identificador já definido. Se não existir, o compilador pressupõe que ele é um rótulo.  
  
 Rótulos tenham seu próprio espaço de declaração e não interfiram com outros identificadores. Escopo de um rótulo é o corpo do método. Declaração de rótulo tem precedência em qualquer situação ambígua.  
  
> [!NOTE]
>  Rótulos podem ser usados somente em declarações executáveis dentro de métodos.  
  
### <a name="to-label-a-line-of-code"></a>Para rotular uma linha de código  
  
- Coloque um identificador, seguido por dois-pontos, no início da linha de código-fonte.  
  
     Por exemplo, as seguintes linhas de código são rotuladas com `Jump` e `120`, respectivamente:  
  
     [!code-vb[VbVbalrStatements#708](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#708)]  
  
## <a name="see-also"></a>Consulte também

- [Instruções](../../../visual-basic/programming-guide/language-features/statements.md)
- [Nomes de Elementos Declarados](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [Estrutura do Programa e Convenções de Código](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
