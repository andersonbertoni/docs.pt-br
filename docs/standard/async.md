---
title: Visão geral da assincronia
description: Saiba como a programação assíncrona é uma técnica chave que torna fácil lidar com o bloqueio de E/S e operações simultâneas em vários núcleos.
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.technology: dotnet-standard
ms.assetid: 1e38e9d9-8284-46ee-a15f-199adc4f26f4
ms.openlocfilehash: aa08389d896fa81dbed8a63bb22a97e151016392
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64628800"
---
# <a name="async-overview"></a>Visão geral da assincronia

Não muito tempo atrás, os aplicativos ficavam mais rápidos simplesmente comprando um computador ou servidor mais novo e então essa tendência parou. Na verdade, ela foi invertida. Surgiram telefones celulares com chips ARM de núcleo único de 1 GHz e as cargas de trabalho do servidor passaram para VMs. Os usuários ainda querem uma interface do usuário responsiva e os proprietários de negócios querem servidores que ajustem a escala com seus negócios. A transição para celular e nuvem e uma população conectada à Internet de >3B usuários resultaram em um novo conjunto de padrões de software. 

* Os aplicativos cliente devem estar sempre ativos, sempre conectados e constantemente responsivos à interação do usuário (por exemplo, toque) com classificações altas na loja de aplicativos!
* Os serviços devem lidar com picos de tráfego escalando e reduzindo horizontalmente sem problemas. 

A programação assíncrona é uma técnica chave que torna fácil de lidar com o bloqueio de E/S e operações simultâneas em vários núcleos. O .NET fornece a capacidade para os aplicativos e serviços serem responsivos e elásticos com modelos de programação assíncrona fáceis de usar e em nível de linguagem em C#, VB e F#.

## <a name="why-write-async-code"></a>Por que escrever código assíncrono?

Os aplicativos modernos fazem amplo uso de E/S de arquivos e rede. As APIs de E/S tradicionalmente bloqueiam por padrão, resultando em experiências de usuário e utilização de hardware ruins, a menos que você deseje aprender e usar padrões desafiadores. O modelo de programação assíncrona em nível de linguagem e as APIs assíncronas baseadas em tarefa invertem esse modelo, tornando a execução assíncrona o padrão com poucos novos conceitos para aprender.

O código assíncrono tem as seguintes características:

* Lida com mais solicitações de servidor gerando threads para lidar com mais solicitações enquanto espera as solicitações de E/S retornarem.
* Permite que as interfaces do usuário sejam mais responsivas gerando threads para a interação da interface do usuário enquanto espera as solicitações de E/S e fazendo a transição do trabalho de longa execução para outros núcleos de CPU.
* Muitas das APIs do .NET mais novas são assíncronas.
* É fácil escrever código assíncrono no .NET!

## <a name="whats-next"></a>O que vem a seguir?

Para obter mais informações, consulte os comentários no tópico [Assincronia detalhada](async-in-depth.md).

O tópico [Padrões de programação assíncrona](asynchronous-programming-patterns/index.md) fornece uma visão geral dos três padrões de programação assíncronos com suporte no .NET Framework:  
  
- [APM (Modelo assíncrono de programação)](asynchronous-programming-patterns/asynchronous-programming-model-apm.md) (herdado)  
  
- [EAP (Padrão assíncrono baseado em evento)](asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md) (herdado)  
  
- [TAP (Padrão assíncrono baseado em tarefa)](asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) (recomendado para novos desenvolvimentos)  

Para obter mais informações sobre o modelo de programação baseado em tarefa recomendado, consulte o tópico [Programação assíncrona baseada em tarefas](parallel-programming/task-based-asynchronous-programming.md).
