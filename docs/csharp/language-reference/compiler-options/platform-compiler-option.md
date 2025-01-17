---
title: -platform (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /platform
helpviewer_keywords:
- platform compiler option [C#]
- -platform compiler option [C#]
- /platform compiler option [C#]
ms.assetid: c290ff5e-47f4-4a85-9bb3-9c2525b0be04
ms.openlocfilehash: 5a00820b01ee0ac78715efa0140e2a5aef28bef8
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592795"
---
# <a name="-platform-c-compiler-options"></a>-platform (opções do compilador C#)
Especifica qual versão do CLR (Common Language Runtime) pode executar o assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-platform:string  
```  
  
## <a name="parameters"></a>Parâmetros  
 `string`  
 anycpu (padrão), anycpu32bitpreferred, ARM, x64, x86 ou Itanium.  
  
## <a name="remarks"></a>Comentários  
  
- O **anycpu** (padrão) compila seu assembly para que ele seja executado em qualquer plataforma. Seu aplicativo será executado como um processo de 64 bits sempre que possível e realizará fallback para 32 bits quando apenas esse modo estiver disponível.  
  
- **anycpu32bitpreferred** compila seu assembly para que ele seja executado em qualquer plataforma. Seu aplicativo é executado no modo 32 bits em sistemas que dão suporte para aplicativos de 32 bits e 64 bits. É possível especificar essa opção apenas para projetos que definem como destino o .NET Framework 4.5.  
  
- O **ARM** compila seu assembly para que ele seja executado em um computador que tem um processador ARM (Advanced RISC Machine).  
  
- **ARM64** compila o assembly para execução pelo CLR de 64 bits em um computador que tem um processador ARM (Máquina RISC Avançada) que dá suporte ao conjunto de instruções A64.  

- **x64** compila o assembly para ser executado pelo CLR de 64 bits em um computador que dá suporte ao conjunto de instruções AMD64 ou EM64T.  
  
- **x86** compila o assembly para ser executado pelo CLR compatível com x86 de 32 bits.  
  
- **Itanium** compila o assembly para ser executado pelo CLR de 64 bits em um computador com um processador Itanium.  
  
 Em um sistema operacional do Windows de 64 bits:  
  
- Os assemblies compilados com **-platform:x86** são executados no CLR de 32 bits em execução no WOW64.  
  
- Uma DLL compilada com o **-platform:anycpu** é executada no mesmo CLR que o processo no qual ela é carregada.  
  
- Os executáveis compilados com **-platform:anycpu** são executados no CLR de 64 bits.  
  
- Os executáveis compilados com **-platform:anycpu32bitpreferred** são executados no CLR de 32 bits.  
  
 A configuração **anycpu32bitpreferred** é válida apenas para arquivos .EXE (executáveis) e requer o .NET Framework 4.5.  
  
 Para obter mais informações sobre o desenvolvimento de um aplicativo para ser executado em um sistema operacional Windows de 64 bits, consulte [Aplicativos de 64 bits](../../../framework/64-bit-apps.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a página **Propriedades** do projeto.  
  
2. Clique na página de propriedades **Compilar**.  
  
3. Modifique a propriedade **Destino da plataforma** e, para projetos que definem como destino o .NET Framework 4.5, marque ou desmarque a caixa de seleção **Preferir 32 bits**.  
  
 **Observe que -platform** não está disponível no ambiente de desenvolvimento no Visual C# Express.  
  
 Para saber mais sobre como definir essa opção do compilador programaticamente, veja <xref:VSLangProj80.CSharpProjectConfigurationProperties3.PlatformTarget%2A>.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar a opção **-platform** para especificar que o aplicativo deve ser executado pelo CLR de 64 bits em um sistema de operacional Windows de 64 bits.  
  
```console  
csc -platform:anycpu filename.cs  
```  
  
## <a name="see-also"></a>Consulte também

- [Opções do compilador de C#](index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
