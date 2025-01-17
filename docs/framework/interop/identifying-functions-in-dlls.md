---
title: Identificando funções em DLLs
ms.date: 03/30/2017
helpviewer_keywords:
- platform invoke, identifying functions
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- identifying DLL functions
- DLL functions
ms.assetid: 3e3f6780-6d90-4413-bad7-ba641220364d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c4c56712460d772426a2d8d6d328cba9bb03373d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648668"
---
# <a name="identifying-functions-in-dlls"></a>Identificando funções em DLLs
A identidade de uma função de DLL consiste dos seguintes elementos:  
  
- Ordinal ou nome da função  
  
- Nome do arquivo DLL em que a implementação pode ser encontrada  
  
 Por exemplo, especificar a função **MessageBox** na User32.dll identifica a função (**MessageBox**) e sua localização (User32.dll, User32 ou user32). A interface de programação de aplicativo (API do Windows) do Microsoft Windows pode conter duas versões de cada função que manipula caracteres e cadeias de caracteres: uma versão ANSI do caractere de 1 byte e uma versão Unicode do caractere de 2 bytes. Quando não especificado, o conjunto de caracteres, representado pelo campo <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet>, torna-se ANSI por padrão. Algumas funções podem ter mais de duas versões.  
  
 **MessageBoxA** é o ponto de entrada ANSI para a função **MessageBox**; **MessageBoxW** é a versão Unicode. Você pode listar os nomes de função para uma DLL específica, como user32.dll, por meio da execução de uma variedade de ferramentas de linha de comando. Por exemplo, você pode usar `dumpbin /exports user32.dll` ou `link /dump /exports user32.dll` para obter nomes de função.  
  
 Você pode renomear uma função não gerenciada para o que você quiser em seu código desde que você mapeie o novo nome para o ponto de entrada original na DLL. Para obter instruções sobre como renomear uma função de DLL não gerenciada no código-fonte gerenciado, consulte [Especificando um ponto de entrada](../../../docs/framework/interop/specifying-an-entry-point.md).  
  
 A invocação de plataforma permite que você controle uma parte significativa do sistema operacional chamando funções na API do Windows e outras DLLs. Além da API do Windows, há várias outras APIs e DLLs disponíveis para você por meio da invocação de plataforma.  
  
 A tabela a seguir descreve várias DLLs comumente usadas na API do Windows.  
  
|DLL|Descrição dos conteúdos|  
|---------|-----------------------------|  
|GDI32.dll|As funções de GDI (Graphics Device Interface) para o dispositivo de saída, tais como aquelas para desenho e para gerenciamento de fontes.|  
|Kernel32.dll|Funções do sistema de operacional de baixo nível para gerenciamento de memória e manipulação de recursos.|  
|User32.dll|Funções de gerenciamento do Windows para a manipulação de mensagens, temporizadores, menus e comunicações.|  
  
 Para obter a documentação completa sobre a API do Windows, confira o SDK da Plataforma. Para obter exemplos que demonstram como construir declarações baseadas no .NET a serem usadas com a invocação de plataforma, consulte [Realizando marshaling de dados com a invocação de plataforma](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md).  
  
## <a name="see-also"></a>Consulte também

- [Consumindo funções de DLL não gerenciadas](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)
- [Especificando um ponto de entrada](../../../docs/framework/interop/specifying-an-entry-point.md)
- [Criando uma classe para conter funções de DLL](../../../docs/framework/interop/creating-a-class-to-hold-dll-functions.md)
- [Criando protótipos em código gerenciado](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)
- [Chamando uma função de DLL](../../../docs/framework/interop/calling-a-dll-function.md)
