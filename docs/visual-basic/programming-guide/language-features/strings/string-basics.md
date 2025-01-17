---
title: Noções básicas de cadeias de caracteres no Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], Like operator
- strings [Visual Basic], Visual Basic
- strings [Visual Basic], regular expressions
ms.assetid: 5674418d-f00d-4f72-9f98-d15897793350
ms.openlocfilehash: f1f6b98d7db510373f2729fab2a6e0ad993ea086
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591388"
---
# <a name="string-basics-in-visual-basic"></a>Noções básicas de cadeias de caracteres no Visual Basic
O `String` tipo de dados representa uma série de caracteres (cada uma instância de um por vez representando o `Char` tipo de dados). Este tópico apresenta os conceitos básicos de cadeias de caracteres no Visual Basic.  
  
## <a name="string-variables"></a>Variáveis de cadeia de caracteres  
 Um valor literal que representa uma série de caracteres pode ser atribuída a uma instância de uma cadeia de caracteres. Por exemplo:  
  
 [!code-vb[VbVbalrStrings#63](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#63)]  
  
 Um `String` variável também pode aceitar qualquer expressão que é avaliada como uma cadeia de caracteres. São mostrados exemplos abaixo:  
  
 [!code-vb[VbVbalrStrings#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#64)]  
  
 Qualquer literal que é atribuído a um `String` variável deve ser colocada entre aspas (""). Isso significa que aspas dentro de uma cadeia de caracteres não pode ser representada por uma marca de aspas. Por exemplo, o código a seguir causa um erro do compilador:  
  
 [!code-vb[VbVbalrStrings#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#65)]  
  
 Esse código causa um erro porque o compilador encerra a cadeia de caracteres após a segunda aspa, e o restante da cadeia de caracteres é interpretado como código. Para resolver esse problema, o Visual Basic interpreta duas aspas em uma cadeia de caracteres literal como uma aspa na cadeia de caracteres. O exemplo a seguir demonstra a maneira correta de incluir uma marca de aspas em uma cadeia de caracteres:  
  
 [!code-vb[VbVbalrStrings#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#66)]  
  
 No exemplo anterior, as duas aspas antes da palavra `Look` se tornam uma aspas na cadeia de caracteres. As três aspas no final da linha representam uma aspas na cadeia de caracteres e o caractere de terminação da cadeia de caracteres.  
  
 Literais de cadeia de caracteres podem conter várias linhas:  
  
```vb  
Dim x = "hello  
world"  
```  
  
 A cadeia de caracteres resultante contém sequências de nova linha que você usou em sua cadeia de caracteres literal (vbcr, vbcrlf, etc.).  Você não precisa usar a solução alternativa antiga:  
  
```vb  
Dim x = <xml><![CDATA[Hello  
World]]></xml>.Value  
```  
  
## <a name="characters-in-strings"></a>Caracteres em cadeias de caracteres  
 Uma cadeia de caracteres pode ser pensada como uma série de `Char` valores e o `String` tipo tem funções internas que permitem que você execute várias manipulações em uma cadeia de caracteres parecidas com as manipulações permitidas por arrays. Como todos os arrays no .NET Framework, essas são matrizes com base em zero. Você pode se referir a um caractere específico em uma cadeia de caracteres por meio de `Chars` propriedade, que fornece uma maneira de acessar um caractere pela posição em que aparece na cadeia de caracteres. Por exemplo:  
  
 [!code-vb[VbVbalrStrings#67](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#67)]  
  
 No exemplo acima, o `Chars` propriedade da cadeia de caracteres retorna o quarto caractere na cadeia de caracteres, que é `D`e a atribui `myChar`. Você também pode obter o comprimento de uma cadeia de caracteres específica por meio de `Length` propriedade. Se você precisar executar várias manipulações de tipo de matriz em uma cadeia de caracteres, você pode convertê-la para uma matriz de `Char` instâncias usando o `ToCharArray` função da cadeia de caracteres. Por exemplo:  
  
 [!code-vb[VbVbalrStrings#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#68)]  
  
 A variável `myArray` agora contém uma matriz de `Char` valores, cada um representando um caractere de `myString`.  
  
## <a name="the-immutability-of-strings"></a>A imutabilidade de cadeias de caracteres  
 É uma cadeia de caracteres *imutável*, que significa que seu valor não pode ser alterado quando ele foi criado. No entanto, isso não impede que você atribuir mais de um valor a uma variável de cadeia de caracteres. Considere o exemplo a seguir:  
  
 [!code-vb[VbVbalrStrings#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#69)]  
  
 Aqui, uma variável de cadeia de caracteres é criada, dado um valor, e, em seguida, seu valor é alterado.  
  
 Mais especificamente, na primeira linha, uma instância do tipo `String` é criado e receberá o valor `This string is immutable`. Na segunda linha do exemplo, uma nova instância é criada e recebe o valor `Or is it?`, e a variável de cadeia de caracteres descarta sua referência para a primeira instância e armazena uma referência para a nova instância.  
  
 Ao contrário de outros tipos de dados intrínsecos, `String` é um tipo de referência. Quando uma variável do tipo de referência é passada como um argumento para uma função ou sub-rotina, uma referência para o endereço de memória onde os dados são armazenados é passada em vez do valor real da cadeia de caracteres. Portanto, no exemplo anterior, o nome da variável permanece o mesmo, mas ele aponta para uma instância nova e diferente de `String` classe, que contém o novo valor.  
  
## <a name="see-also"></a>Consulte também

- [Introdução às cadeias de caracteres no Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
- [Tipo de Dados String](../../../../visual-basic/language-reference/data-types/string-data-type.md)
- [Tipo de Dados de Caractere](../../../../visual-basic/language-reference/data-types/char-data-type.md)
- [Operações básicas de cadeias de caracteres](../../../../standard/base-types/basic-string-operations.md)
