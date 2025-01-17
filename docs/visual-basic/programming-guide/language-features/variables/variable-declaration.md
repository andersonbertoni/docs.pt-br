---
title: Declaração de variável no Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], declaring
- member variables [Visual Basic], declarations
- Dim statement [Visual Basic], variable declaration
- declaring variables [Visual Basic]
- variables [Visual Basic], scope
- variables [Visual Basic], data types
- data types [Visual Basic], variable declarations
- lifetime [Visual Basic], variables
- variables [Visual Basic], lifetime
- access levels [Visual Basic], variables
- scope [Visual Basic], declaration statements
- variables [Visual Basic], access level
- local variables [Visual Basic], declarations
- scope [Visual Basic], variables
ms.assetid: d8f10226-92b1-480f-9f53-df377b2d7e15
ms.openlocfilehash: 4706f306e8db252b35148f8e6a0f8c42122f5482
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65583383"
---
# <a name="variable-declaration-in-visual-basic"></a>Declaração de variável no Visual Basic
Você declara uma variável para especificar seu nome e características. A instrução de declaração para variáveis é a [instrução Dim](../../../../visual-basic/language-reference/statements/dim-statement.md). Sua localização e conteúdo determinam as características da variável.  
  
 Para regras de nomenclatura de variável e considerações, consulte [nomes de elemento declarado](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## <a name="declaration-levels"></a>Níveis de declaração  
  
### <a name="local-and-member-variables"></a>Local e variáveis de membro  
 Um *variável local* é aquele que é declarada dentro de um procedimento. Um *variável de membro* é um membro de um tipo de Visual Basic; ela é declarada no nível de módulo, dentro de uma classe, estrutura ou módulo, mas não em qualquer procedimento interno para essa classe, estrutura ou módulo.  
  
### <a name="shared-and-instance-variables"></a>Compartilhado e variáveis de instância  
 Em uma classe ou estrutura, a categoria de uma variável de membro depende se ela é compartilhada. Se ela for declarada com o [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) palavra-chave, ele é um *variável compartilhada*, e ela existe em uma única cópia compartilhada entre todas as instâncias da classe ou estrutura.  
  
 Caso contrário, ele é um *variável de instância*, e uma cópia separada do que ele é criada para cada instância da classe ou estrutura. Uma cópia determinada de uma variável de instância está disponível somente para a instância da classe ou estrutura na qual ele foi criado. Ele é independente de uma cópia da variável de instância em qualquer outra instância da classe ou estrutura.  
  
## <a name="declaring-data-type"></a>Declarando o tipo de dados  
 O [como](../../../../visual-basic/language-reference/statements/as-clause.md) cláusula na instrução de declaração permite que você defina o tipo de dados ou o tipo de objeto da variável que você está declarando. Você pode especificar qualquer um dos seguintes tipos para uma variável:  
  
- Tipo de dados um elementar, como `Boolean`, `Long`, ou `Decimal`  
  
- Um tipo de dados compostos, como uma matriz ou estrutura  
  
- Um tipo de objeto ou classe, definida em seu aplicativo ou em outro aplicativo  
  
- Classe de um .NET Framework, como <xref:System.Windows.Forms.Label> ou <xref:System.Windows.Forms.TextBox>  
  
- Tipo de uma interface, como <xref:System.IComparable> ou <xref:System.IDisposable>  
  
 Você pode declarar diversas variáveis em uma instrução sem ter que repetir o tipo de dados. Nas instruções a seguir, as variáveis `i`, `j`, e `k` são declaradas como tipo `Integer`, `l` e `m` como `Long`, e `x` e `y` como `Single`:  
  
```  
Dim i, j, k As Integer  
' All three variables in the preceding statement are declared as Integer.  
Dim l, m As Long, x, y As Single  
' In the preceding statement, l and m are Long, x and y are Single.  
```  
  
 Para obter mais informações sobre tipos de dados, consulte [tipos de dados](../../../../visual-basic/programming-guide/language-features/data-types/index.md). Para obter mais informações sobre objetos, consulte [objetos e Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md) e [Programando com componentes](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/0ffkdtkf(v=vs.120)).  
  
## <a name="local-type-inference"></a>Inferência de tipo local  
 *Inferência de tipos* é usado para determinar os tipos de dados de variáveis locais declaradas sem um `As` cláusula. O compilador infere o tipo da variável do tipo da expressão de inicialização. Isso permite que você declare variáveis sem especificar explicitamente um tipo. No exemplo a seguir, ambos `num1` e `num2` são fortemente tipadas como inteiros.  
  
 [!code-vb[VbVbalrTypeInference#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#1)]  
  
 Se você quiser usar inferência de tipo local, `Option Infer` deve ser definida como `On`. Para obter mais informações, consulte [Inferência de tipo de variável local](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md) e [Instrução Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md).  
  
## <a name="characteristics-of-declared-variables"></a>Características de variáveis declaradas  
 O *tempo de vida* de uma variável é o período de tempo durante o qual ele está disponível para uso. Em geral, uma variável existe desde que o elemento que o declara (por exemplo, um procedimento ou classe) continua existindo. Se a variável não precisa continuar existindo além do tempo de vida do elemento que contém, você não precisa fazer nada especial na declaração. Se a variável precisa continuar existindo mais que o elemento que contém, você pode incluir a `Static` ou `Shared` palavra-chave em seu `Dim` instrução. Para obter mais informações, consulte [tempo de vida no Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md).  
  
 O *escopo* de uma variável é o conjunto de todo o código que pode se referir a ele sem qualificar seu nome. Um escopo de variável é determinado pelo qual ele é declarado. Código localizado em uma determinada região pode usar as variáveis definidas naquela região sem ter que qualificar seus nomes. Para obter mais informações, consulte [escopo no Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md).  
  
 Uma variável *nível de acesso* é a extensão de código que tem permissão para acessá-lo. Isso é determinado pelo modificador de acesso (como [pública](../../../../visual-basic/language-reference/modifiers/public.md) ou [privada](../../../../visual-basic/language-reference/modifiers/private.md)) que você usa no `Dim` instrução. Para obter mais informações, consulte [acessar níveis no Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## <a name="see-also"></a>Consulte também

- [Como: Criar uma nova variável](../../../../visual-basic/programming-guide/language-features/variables/how-to-create-a-new-variable.md)
- [Como: Mover dados dentro e fora de uma variável](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)
- [Tipos de Dados](../../../../visual-basic/language-reference/data-types/index.md)
- [Protegido](../../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)
- [Estático](../../../../visual-basic/language-reference/modifiers/static.md)
- [Características do Elemento Declarado](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)
- [Inferência de Tipo de Variável Local](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Instrução Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md)
