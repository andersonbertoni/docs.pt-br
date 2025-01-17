---
title: 'Como: ler um arquivo de texto – Guia de Programação em C#'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- StreamReader.ReadToEnd
helpviewer_keywords:
- text files, writing to
- reading text files
- reading data, text files
- text files, reading
ms.assetid: 92246c5b-e819-4eea-9370-1a9460e12de3
ms.openlocfilehash: 236e730eaae0bc73c715e9b1c2c71d6c870d78e3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64608531"
---
# <a name="how-to-read-from-a-text-file-c-programming-guide"></a>Como: ler um arquivo de texto (Guia de Programação em C#)
Este exemplo lê o conteúdo de um arquivo de texto usando os métodos estáticos <xref:System.IO.File.ReadAllText%2A> e <xref:System.IO.File.ReadAllLines%2A> da classe <xref:System.IO.File?displayProperty=nameWithType>.  
  
 Para obter um exemplo que use <xref:System.IO.StreamReader>, confira [Como ler um arquivo de texto uma linha de cada vez](../../../csharp/programming-guide/file-system/how-to-read-a-text-file-one-line-at-a-time.md).  
  
> [!NOTE]
>  Os arquivos usados neste exemplo são criados no tópico [Como gravar em um arquivo de texto](../../../csharp/programming-guide/file-system/how-to-write-to-a-text-file.md)  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[csFilesandFolders#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#4)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Copie o código e cole-o em um aplicativo de console em C#.  
  
 Se você não estiver usando os arquivos de texto de [Como gravar em um arquivo de texto](../../../csharp/programming-guide/file-system/how-to-write-to-a-text-file.md), substitua o argumento de `ReadAllText` e `ReadAllLines` pelo nome de arquivo e pelo caminho adequado em seu computador.  
  
## <a name="robust-programming"></a>Programação robusta  
 As seguintes condições podem causar uma exceção:  
  
- O arquivo não existe ou não existe no local especificado. Verifique o caminho e a ortografia do nome do arquivo.  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Não confie no nome de um arquivo para determinar o conteúdo do arquivo. Por exemplo, o arquivo `myFile.cs` pode não ser um arquivo de origem do C#.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.IO?displayProperty=nameWithType>
- [Guia de Programação em C#](../../../csharp/programming-guide/index.md)
- [Sistema de arquivos e o Registro (Guia de Programação em C#)](../../../csharp/programming-guide/file-system/index.md)
