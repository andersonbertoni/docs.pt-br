---
title: Características de aplicativos Web modernos
description: Arquitetar aplicativos Web modernos com o ASP.NET Core e o Azure | Características de aplicativos Web modernos
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: f4fe18d7361f7d67c29fb7dab53132237f709280
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68672903"
---
# <a name="characteristics-of-modern-web-applications"></a>Características de aplicativos Web modernos

> "… com o design correto, os recursos são obtidos sem esforços. Essa abordagem é árdua, mas continua a ter êxito."  
> _\- Dennis Ritchie_

Os aplicativos Web modernos têm maiores expectativas de usuário e maiores demandas do que nunca. Os aplicativos Web de hoje devem estar disponíveis 24/7 em qualquer lugar do mundo e ser utilizáveis praticamente em qualquer dispositivo ou tamanho de tela. Os aplicativos Web precisam ser seguros, flexíveis e escalonáveis para atender aos picos da demanda. Cada vez mais, os cenários complexos devem ser tratados por experiências avançadas do usuário criadas no cliente por meio de JavaScript e pela comunicação eficiente por meio de APIs Web.

O ASP.NET Core é otimizado para aplicativos Web modernos e cenários de hospedagem baseada em nuvem. Seu design modular permite que os aplicativos dependam somente dos recursos que realmente usarem, melhorando o desempenho e a segurança do aplicativo e, ao mesmo tempo, reduzindo os requisitos de recursos de hospedagem.

## <a name="reference-application-eshoponweb"></a>Referência de aplicativo: eShopOnWeb

Estas diretrizes incluem um aplicativo de referência, o _eShopOnWeb_, que demonstra alguns dos princípios e das recomendações. O aplicativo é uma loja online simples compatível com navegação em um catálogo de camisetas, canecas e outros itens de marketing. O aplicativo de referência é deliberadamente simples para facilitar o entendimento.

**Figura 2-1.** eShopOnWeb

![](./media/image2-1.png)

> ### <a name="reference-application"></a>Aplicativo de referência
>
> - **eShopOnWeb**  
>   <https://github.com/dotnet/eShopOnWeb>

## <a name="cloud-hosted-and-scalable"></a>Hospedado na nuvem e escalonável

O ASP.NET Core é otimizado para a nuvem (nuvem pública, nuvem privada, qualquer nuvem) porque tem baixa memória e alta taxa de transferência. Uma superfície menor dos aplicativos ASP.NET Core significa que você pode hospedar mais partes dele no mesmo hardware e pagar por menos recursos quando usar os serviços pré-pagos de hospedagem na nuvem. A taxa de transferência mais alta significa que você pode atender mais clientes por meio de um aplicativo considerando o mesmo hardware, reduzindo ainda mais a necessidade de investir em servidores e na infraestrutura de hospedagem.

## <a name="cross-platform"></a>Plataforma cruzada

O ASP.NET Core é multiplataforma e pode ser executado no Windows, no macOS e no Linux. Isso proporciona muitas novas opções para o desenvolvimento e a implantação de aplicativos criados com o ASP.NET Core. Os contêineres do Docker, tanto do Linux quanto do Windows, podem hospedar aplicativos ASP.NET Core, permitindo que eles aproveitem os benefícios de [contêineres e microsserviços](../microservices/index.md).

## <a name="modular-and-loosely-coupled"></a>Flexível e acoplado de forma flexível

Os pacotes NuGet são cidadãos de primeira classe no .NET Core, e os aplicativos ASP.NET Core são compostos por muitas bibliotecas por meio do NuGet. Essa granularidade da funcionalidade ajuda a garantir que os aplicativos dependam e implantem somente a funcionalidade de que realmente precisam, reduzindo sua área da superfície de vulnerabilidade de segurança.

O ASP.NET Core também é totalmente compatível com a [injeção de dependência](https://deviq.com/dependency-injection/), tanto internamente quanto no nível do aplicativo. As interfaces podem ter várias implementações que podem ser alternadas, conforme necessário. A injeção de dependência permite que os aplicativos sejam acoplados de modo flexível a essas interfaces, em vez de a implementações específicas, facilitando a extensão, a manutenção e o teste.

## <a name="easily-tested-with-automated-tests"></a>Testados facilmente com testes automatizados

Os aplicativos ASP.NET Core são compatíveis com teste de unidade, além disso, o acoplamento flexível e o suporte a injeções de dependência facilitam a alternância de interesses da infraestrutura com implementações fictícias para fins de teste. O ASP.NET Core também fornece um TestServer que pode ser usado para hospedar aplicativos em memória. Os testes funcionais podem então fazer solicitações para esse servidor em memória, exercitando a pilha completa do aplicativo (incluindo middleware, roteamento, model binding, filtros, etc.) e recebendo uma resposta, tudo isso em uma fração do tempo que levaria para hospedar o aplicativo em um servidor real e fazer solicitações por meio da camada de rede. Esses testes são especialmente fáceis de serem gravados e significativos para APIs, que são cada vez mais importantes em aplicativos Web modernos.

## <a name="traditional-and-spa-behaviors-supported"></a>Comportamentos tradicionais e de SPA com suporte

Os aplicativos Web tradicionais envolvem pouco comportamento do lado do cliente e, em vez disso, dependem do servidor para todas as consultas, atualizações e navegação que o aplicativo pode precisar fazer. Cada nova operação feita pelo usuário é convertida em uma nova solicitação da Web, com o resultado sendo um recarregamento de página inteira no navegador do usuário final. As estruturas MVC (Modelo-Exibição-Controlador) clássicas normalmente seguem essa abordagem, com cada nova solicitação correspondente a uma ação de controlador diferente, que, por sua vez, trabalham com um modelo e retornam uma exibição. Algumas operações individuais em determinada página podem ser aprimoradas com a funcionalidade AJAX (Asynchronous JavaScript And XML), mas a arquitetura geral do aplicativo usava muitas diferentes exibições do MVC e pontos de extremidade de URL. Além disso, o ASP.NET Core MVC também é compatível com Razor Pages, uma maneira mais simples para organizar as páginas de estilo MVC.

Por outro lado, os SPAs (aplicativos de página única) envolvem muito poucos carregamentos de página do lado do servidor gerados dinamicamente (se houver). Muitos SPAs são inicializados em um arquivo HTML estático que carrega as bibliotecas JavaScript necessárias para iniciar e executar o aplicativo. Esses aplicativos fazem uso intenso de APIs Web para suas necessidades de dados e podem fornecer experiências do usuário muito mais avançadas.

Muitos aplicativos Web envolvem uma combinação do comportamento do aplicativo Web tradicional (normalmente para o conteúdo) e SPAs (para a interatividade). O ASP.NET Core é compatível com o MVC (baseado em Exibições ou em Páginas) e com as APIs Web no mesmo aplicativo, usando o mesmo conjunto de ferramentas e de bibliotecas da estrutura subjacentes.

## <a name="simple-development-and-deployment"></a>Desenvolvimento e implantação simples

Os aplicativos ASP.NET Core podem ser escritos com editores de texto e interfaces de linha de comando simples ou com ambientes de desenvolvimento completo como o Visual Studio. Normalmente, os aplicativos monolíticos são implantados em um único ponto de extremidade. As implantações podem ser automatizadas com facilidade para ocorrerem como parte de um pipeline de CI (integração contínua) e CD (entrega contínua). Além das ferramentas de CI/CD tradicionais, o Microsoft Azure tem suporte integrado para repositórios Git e pode implantar automaticamente atualizações conforme elas são feitas em um GIT branch ou marcação especificado.

## <a name="traditional-aspnet-and-web-forms"></a>ASP.NET tradicional e Web Forms

Além do ASP.NET Core, o ASP.NET 4.x tradicional continua sendo uma plataforma robusta e confiável para a criação de aplicativos Web. O ASP.NET é compatível com modelos de desenvolvimento do MVC e da API Web, bem como ao Web Forms, que é adequado para o desenvolvimento de aplicativos avançados baseados em página e apresenta um ecossistema avançado de componentes de terceiros. O Microsoft Azure apresenta um excelente suporte de longa data para aplicativos ASP.NET 4.x e muitos desenvolvedores estão familiarizados com essa plataforma.

> ### <a name="references--modern-web-applications"></a>Referências – Aplicativos Web modernos
>
> - **Introdução ao ASP.NET Core**  
>   <https://docs.microsoft.com/aspnet/core/>
> - **Seis benefícios principais do ASP.NET Core que o tornam diferente e melhor**  
>   <https://blog.trigent.com/six-key-benefits-of-asp-net-core-1-0-which-make-it-different-better/>
> - **Teste no ASP.NET Core**  
>   <https://docs.microsoft.com/aspnet/core/testing/>

>[!div class="step-by-step"]
>[Anterior](index.md)
>[Próximo](choose-between-traditional-web-and-single-page-apps.md)
