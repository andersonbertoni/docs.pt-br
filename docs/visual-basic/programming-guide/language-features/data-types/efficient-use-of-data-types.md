---
title: Uso eficiente de tipos de dados (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- performance, data type efficiency
- data types [Visual Basic], weak typing
- AscW function [Visual Basic], preferred to Asc
- data types [Visual Basic], using efficiently
- optimization [Visual Basic], data types
- data types [Visual Basic], strong typing
- strong typing
- typing, strong
- data types [Visual Basic], optimizing
- ChrW function [Visual Basic], preferred to Chr
ms.assetid: 28f5e4ba-ec24-4f37-b90a-e8ee822f778a
ms.openlocfilehash: 68371a9f8d4dcc5d0a2b67955d5e88943a83b085
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68631112"
---
# <a name="efficient-use-of-data-types-visual-basic"></a>Uso eficiente de tipos de dados (Visual Basic)
Variáveis não declaradas e variáveis declaradas sem um tipo `Object` de dados recebem o tipo de dados. Isso facilita escrever programas rapidamente, mas pode fazer com que eles sejam executados mais lentamente.

## <a name="strong-typing"></a>Tipagem forte
 Especificar tipos de dados para todas as suas variáveis é conhecido como tipagem *forte*. O uso de rigidez de tipos tem várias vantagens:

- Ele habilita o suporte IntelliSense para suas variáveis. Isso permite que você veja suas propriedades e outros membros enquanto digita no código.

- Ele aproveita a verificação do tipo de compilador. Isso captura instruções que podem falhar em tempo de execução devido a erros como overflow. Ele também captura chamadas para métodos em objetos que não dão suporte a eles.

- Isso resulta em uma execução mais rápida do seu código.

## <a name="most-efficient-data-types"></a>Tipos de dados mais eficientes
 Para variáveis que nunca contêm frações, os tipos de dados integral são mais eficientes do que os tipos não integrais. No Visual Basic, `Integer` e `UInteger` são os tipos numéricos mais eficientes.

 Para números fracionários, `Double` é o tipo de dados mais eficiente, porque os processadores em plataformas atuais executam operações de ponto flutuante em precisão dupla. No entanto, `Double` as operações com não são tão rápidas quanto com os tipos `Integer`integrais, como.

## <a name="specifying-data-type"></a>Especificando o tipo de dados
 Use a [instrução Dim](../../../../visual-basic/language-reference/statements/dim-statement.md) para declarar uma variável de um tipo específico. Você pode especificar simultaneamente seu nível de acesso usando a palavra-chave [Public](../../../../visual-basic/language-reference/modifiers/public.md), [Protected](../../../../visual-basic/language-reference/modifiers/protected.md), [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)ou [Private](../../../../visual-basic/language-reference/modifiers/private.md) , como no exemplo a seguir.

```vb
Private x As Double
Protected s As String
```

## <a name="character-conversion"></a>Conversão de caracteres
 As `AscW` funções `ChrW` e operam em Unicode. Você deve usá-los em preferência `Asc` ao `Chr`e, que devem ser traduzidos para dentro e fora do Unicode.

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- [Tipos de Dados](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [Tipos de Dados Numéricos](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)
- [Declaração de Variável](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [Usando o IntelliSense](/visualstudio/ide/using-intellisense)
