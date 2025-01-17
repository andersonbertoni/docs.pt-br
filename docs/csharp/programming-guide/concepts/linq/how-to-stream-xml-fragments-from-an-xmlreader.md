---
title: 'Como: Transmitir fragmentos XML de um XmlReader (C#)'
ms.date: 07/20/2015
ms.assetid: 4a8f0e45-768a-42e2-bc5f-68bdf0e0a726
ms.openlocfilehash: 6937a7160c83def3238c8d2fe3e2b83c996396fd
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66484915"
---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-c"></a>Como: Transmitir fragmentos XML de um XmlReader (C#)
Quando você tem que processa grandes arquivos XML, talvez não seja possível carregar a árvore inteira XML na memória. Este tópico mostra como passar informações usando <xref:System.Xml.XmlReader>.  
  
 Um dos modos de efetivas usar <xref:System.Xml.XmlReader> para ler objetos de <xref:System.Xml.Linq.XElement> é escrever seu próprio método personalizado do eixo. Um método do eixo normalmente retorna uma coleção como <xref:System.Collections.Generic.IEnumerable%601> de <xref:System.Xml.Linq.XElement>, conforme mostrado no exemplo neste tópico. No método personalizado do eixo, depois de criar o fragmento XML chamando o método <xref:System.Xml.Linq.XNode.ReadFrom%2A> , retornar a coleção usando `yield return`. Isso fornece a semântica de execução adiada ao método personalizado do eixo.  
  
 Quando você cria uma árvore XML de um objeto de <xref:System.Xml.XmlReader> , <xref:System.Xml.XmlReader> deve ser posicionado em um elemento. O método de <xref:System.Xml.Linq.XNode.ReadFrom%2A> não retorna até que lê a marca do elemento.  
  
 Se você desejar criar uma árvore parcial, você pode criar uma instância <xref:System.Xml.XmlReader>, posiciona o leitor no nó que você deseja converter a <xref:System.Xml.Linq.XElement> uma árvore e em seguida, cria o objeto de <xref:System.Xml.Linq.XElement> .  
  
 O tópico [Como: Transmitir fragmentos XML com acesso a informações de cabeçalho (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md) contém informações e um exemplo de como transmitir um documento mais complexo.  
  
 O tópico [Como: Executar a transformação de streaming de documentos XML grandes (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-perform-streaming-transform-of-large-xml-documents.md) contém um exemplo de como usar o LINQ to XML para transformar documentos XML muito grandes, mantendo um volume de memória pequeno.  
  
## <a name="example"></a>Exemplo  
 Este exemplo cria um método personalizado do eixo. Você pode consultá-lo usando uma consulta [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]. O método de eixo personalizado `StreamRootChildDoc` é um método que foi projetado especificamente para ler um documento que tenha um elemento `Child` de repetição.  
  
```csharp  
static IEnumerable<XElement> StreamRootChildDoc(StringReader stringReader)  
{  
    using (XmlReader reader = XmlReader.Create(stringReader))  
    {  
        reader.MoveToContent();  
        // Parse the file and display each of the nodes.  
        while (reader.Read())  
        {  
            switch (reader.NodeType)  
            {  
                case XmlNodeType.Element:  
                    if (reader.Name == "Child") {  
                        XElement el = XElement.ReadFrom(reader) as XElement;  
                        if (el != null)  
                            yield return el;  
                    }  
                    break;  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    string markup = @"<Root>  
      <Child Key=""01"">  
        <GrandChild>aaa</GrandChild>  
      </Child>  
      <Child Key=""02"">  
        <GrandChild>bbb</GrandChild>  
      </Child>  
      <Child Key=""03"">  
        <GrandChild>ccc</GrandChild>  
      </Child>  
    </Root>";  
  
    IEnumerable<string> grandChildData =  
        from el in StreamRootChildDoc(new StringReader(markup))  
        where (int)el.Attribute("Key") > 1  
        select (string)el.Element("GrandChild");  
  
    foreach (string str in grandChildData) {  
        Console.WriteLine(str);  
    }  
}  
```  
  
 Este exemplo gera a seguinte saída:  
  
```  
bbb  
ccc  
```  
  
 Nesse exemplo, o documento de origem é muito pequeno. No entanto, mesmo se houver milhões de elementos de `Child` , este exemplo ainda terá uma pegada pequena de memória.  
  