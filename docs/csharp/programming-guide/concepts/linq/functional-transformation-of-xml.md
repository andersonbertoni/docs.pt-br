---
title: Transformação funcional de XML (C#)
ms.date: 07/20/2015
ms.assetid: 0ccb9251-38d7-44e3-9b84-1b5fe25e4b59
ms.openlocfilehash: b1325644873db29b2c40901ded3eb254b3a31073
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66485962"
---
# <a name="functional-transformation-of-xml-c"></a>Transformação funcional de XML (C#)
Este tópico descreve a abordagem funcional pura de transformação aos documentos XML de alteração, e ele contrastes com uma abordagem procedural.  
  
## <a name="modifying-an-xml-document"></a>Alterando um documento XML  
 Uma das tarefas mais comuns para um programador XML está transformando XML de uma forma para outra. A forma de um documento XML é a estrutura do documento, que inclui o seguinte:  
  
- A hierarquia expressa pelo documento.  
  
- Nomes de elementos e atributos.  
  
- Os tipos de dados de elementos e atributos.  
  
 Em geral, a abordagem mais eficiente para transformar XML de uma forma para outra é a de transformação funcional pura. Nessa abordagem, a tarefa principal do programador é criar uma transformação que é aplicada ao documento XML inteiro (ou a um ou mais nós estritamente definido). A transformação funcional é teoricamente a mais fácil de código (após um programador estiver familiarizado com a abordagem), produz o código o mais sustentável, e é geralmente mais compacta de abordagens alternativas.  
  
### <a name="xml-functional-transformational-technologies"></a>Tecnologias transformacionais funcionais XML  
 A Microsoft oferece duas tecnologias funcionais de transformação para uso em documentos XML: XSLT e LINQ to XML. XSLT é suportado no namespace gerenciada <xref:System.Xml.Xsl> e na implementação nativo COM de MSXML. Embora XSLT é uma tecnologia robusta para documentos XML de tratamento, requer a experiência em um domínio especializado, como o idioma XSLT e seus APIs de suporte.  
  
 LINQ to XML fornece as ferramentas necessárias codificação transformações e puras de uma maneira poderosa completo expressive e, em C# ou de código Visual Basic. Por exemplo, muitos dos exemplos o uso da documentação LINQ to XML uma abordagem funcional pura. Além disso, no [Tutorial: Manipulando o conteúdo em um documento WordprocessingML (C#)](../../../../csharp/programming-guide/concepts/linq/shape-of-wordprocessingml-documents.md), usamos o LINQ to XML em uma abordagem funcional para manipular informações em um documento do Microsoft Word.  
  
 Para obter uma comparação mais completa entre LINQ to XML e outras tecnologias Microsoft XML, consulte [LINQ to XML versus Outras Tecnologias XML](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-vs-other-xml-technologies.md).  
  
 XSLT a ferramenta é recomendada para transformações um documento céntricas quando o documento de origem tem uma estrutura denteada. No entanto, LINQ to XML também pode executar um documento centralizado em transformações. Para obter mais informações, confira [Como: Usar anotações para transformar árvores LINQ to XML em um estilo XSLT (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-use-annotations-to-transform-linq-to-xml-trees-in-an-xslt-style.md).  
  
## <a name="see-also"></a>Consulte também

- [Introdução às transformações funcionais puras (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)
- [Tutorial: manipulando conteúdo em um documento WordprocessingML (C#)](../../../../csharp/programming-guide/concepts/linq/shape-of-wordprocessingml-documents.md)
- [LINQ to XML versus Outras Tecnologias XML](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-vs-other-xml-technologies.md)
