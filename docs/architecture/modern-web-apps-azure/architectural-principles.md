---
title: Princípios de arquitetura
description: Projetar aplicativos Web modernos com o ASP.NET Core e o Azure | Princípios de arquitetura
author: ardalis
ms.author: wiwagn
ms.date: 02/16/2019
ms.openlocfilehash: 74ff7196ce17807b98a975687a524041f15a7f5b
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68675573"
---
# <a name="architectural-principles"></a><span data-ttu-id="128ca-103">Princípios de arquitetura</span><span class="sxs-lookup"><span data-stu-id="128ca-103">Architectural principles</span></span>

> <span data-ttu-id="128ca-104">"Se os construtores construíssem edifícios da maneira como os programadores escrevem programas, o primeiro pica-pau que surgisse destruiria a civilização."</span><span class="sxs-lookup"><span data-stu-id="128ca-104">"If builders built buildings the way programmers wrote programs, then the first woodpecker that came along would destroy civilization."</span></span>  
> <span data-ttu-id="128ca-105">_\- Gerald Weinberg_</span><span class="sxs-lookup"><span data-stu-id="128ca-105">_\- Gerald Weinberg_</span></span>

<span data-ttu-id="128ca-106">Você deve projetar e criar soluções de software com a facilidade de manutenção em mente.</span><span class="sxs-lookup"><span data-stu-id="128ca-106">You should architect and design software solutions with maintainability in mind.</span></span> <span data-ttu-id="128ca-107">Os princípios descritos nesta seção podem ajudar a orientá-lo em direção à tomada de decisões de arquitetura que resultarão em aplicativos limpos e de fácil manutenção.</span><span class="sxs-lookup"><span data-stu-id="128ca-107">The principles outlined in this section can help guide you toward architectural decisions that will result in clean, maintainable applications.</span></span> <span data-ttu-id="128ca-108">Em geral, esses princípios orientarão você para a criação de aplicativos fora de componentes discretos que não têm um acoplamento rígido com outras partes do aplicativo, mas que, em vez disso, se comunicam por meio de interfaces explícitas ou sistemas de mensagens.</span><span class="sxs-lookup"><span data-stu-id="128ca-108">Generally, these principles will guide you toward building applications out of discrete components that are not tightly coupled to other parts of your application, but rather communicate through explicit interfaces or messaging systems.</span></span>

## <a name="common-design-principles"></a><span data-ttu-id="128ca-109">Princípios comuns de design</span><span class="sxs-lookup"><span data-stu-id="128ca-109">Common design principles</span></span>

### <a name="separation-of-concerns"></a><span data-ttu-id="128ca-110">Separação de interesses</span><span class="sxs-lookup"><span data-stu-id="128ca-110">Separation of concerns</span></span>

<span data-ttu-id="128ca-111">Um princípio norteador durante o desenvolvimento é o da **Separação de Interesses**.</span><span class="sxs-lookup"><span data-stu-id="128ca-111">A guiding principle when developing is **Separation of Concerns**.</span></span> <span data-ttu-id="128ca-112">Esse princípio declara que o software deve ser separado de acordo com os tipos de trabalho que ele executa.</span><span class="sxs-lookup"><span data-stu-id="128ca-112">This principle asserts that software should be separated based on the kinds of work it performs.</span></span> <span data-ttu-id="128ca-113">Por exemplo, considere um aplicativo que inclua uma lógica para identificar itens importantes a serem exibidos ao usuário, e que formata esses itens de uma maneira específica para torná-los mais perceptíveis.</span><span class="sxs-lookup"><span data-stu-id="128ca-113">For instance, consider an application that includes logic for identifying noteworthy items to display to the user, and which formats such items in a particular way to make them more noticeable.</span></span> <span data-ttu-id="128ca-114">O comportamento responsável por escolher quais itens devem ser formatados deve ser mantido separado do comportamento responsável por formatar os itens, pois esses são interesses separados que somente se relacionam coincidentemente um com o outro.</span><span class="sxs-lookup"><span data-stu-id="128ca-114">The behavior responsible for choosing which items to format should be kept separate from the behavior responsible for formatting the items, since these are separate concerns that are only coincidentally related to one another.</span></span>

<span data-ttu-id="128ca-115">Em termos de arquitetura, os aplicativos podem ser criados logicamente para seguir esse princípio, separando o comportamento principal dos negócios da lógica de interface do usuário e de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="128ca-115">Architecturally, applications can be logically built to follow this principle by separating core business behavior from infrastructure and user interface logic.</span></span> <span data-ttu-id="128ca-116">O ideal é que a lógica e as regras de negócio residam em um projeto separado, que não deve depender de outros projetos no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="128ca-116">Ideally, business rules and logic should reside in a separate project, which should not depend on other projects in the application.</span></span> <span data-ttu-id="128ca-117">Isso ajuda a garantir que o modelo de negócios seja fácil de ser testado e possa evoluir sem ter um acoplamento rígido com detalhes de implementação de nível inferior.</span><span class="sxs-lookup"><span data-stu-id="128ca-117">This helps ensure that the business model is easy to test and can evolve without being tightly coupled to low-level implementation details.</span></span> <span data-ttu-id="128ca-118">A separação de interesses é uma consideração fundamental por trás do uso de camadas em arquiteturas de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="128ca-118">Separation of concerns is a key consideration behind the use of layers in application architectures.</span></span>

### <a name="encapsulation"></a><span data-ttu-id="128ca-119">Encapsulamento</span><span class="sxs-lookup"><span data-stu-id="128ca-119">Encapsulation</span></span>

<span data-ttu-id="128ca-120">Diferentes partes de um aplicativo devem usar o **encapsulamento** para isolá-las de outras partes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="128ca-120">Different parts of an application should use **encapsulation** to insulate them from other parts of the application.</span></span> <span data-ttu-id="128ca-121">As camadas e os componentes do aplicativo devem poder ajustar sua implementação interna sem dividir seus colaboradores, desde que contratos externos não sejam violados.</span><span class="sxs-lookup"><span data-stu-id="128ca-121">Application components and layers should be able to adjust their internal implementation without breaking their collaborators as long as external contracts are not violated.</span></span> <span data-ttu-id="128ca-122">O uso adequado do encapsulamento ajuda a obter um acoplamento flexível e uma modularidade nos designs do aplicativo, pois os objetos e os pacotes podem ser substituídos por implementações alternativas, desde que a mesma interface seja mantida.</span><span class="sxs-lookup"><span data-stu-id="128ca-122">Proper use of encapsulation helps achieve loose coupling and modularity in application designs, since objects and packages can be replaced with alternative implementations so long as the same interface is maintained.</span></span>

<span data-ttu-id="128ca-123">Nas classes, o encapsulamento é obtido por meio da limitação do acesso externo ao estado interno da classe.</span><span class="sxs-lookup"><span data-stu-id="128ca-123">In classes, encapsulation is achieved by limiting outside access to the class's internal state.</span></span> <span data-ttu-id="128ca-124">Se um ator externo desejar manipular o estado do objeto, ele deverá fazer isso por meio de uma função bem definida (ou um setter de propriedade), em vez de ter acesso direto ao estado particular do objeto.</span><span class="sxs-lookup"><span data-stu-id="128ca-124">If an outside actor wants to manipulate the state of the object, it should do so through a well-defined function (or property setter), rather than having direct access to the private state of the object.</span></span> <span data-ttu-id="128ca-125">Da mesma forma, os componentes do aplicativo e os próprios aplicativos devem expor interfaces bem definidas para uso de seus colaboradores, em vez de permitir que seu estado seja modificado diretamente.</span><span class="sxs-lookup"><span data-stu-id="128ca-125">Likewise, application components and applications themselves should expose well-defined interfaces for their collaborators to use, rather than allowing their state to be modified directly.</span></span> <span data-ttu-id="128ca-126">Isso libera o design interno do aplicativo para evoluir ao longo do tempo, sem a preocupação de que fazendo isso dividirá os colaboradores, desde que os contratos públicos sejam mantidos.</span><span class="sxs-lookup"><span data-stu-id="128ca-126">This frees the application's internal design to evolve over time without worrying that doing so will break collaborators, so long as the public contracts are maintained.</span></span>

### <a name="dependency-inversion"></a><span data-ttu-id="128ca-127">Inversão de dependência</span><span class="sxs-lookup"><span data-stu-id="128ca-127">Dependency inversion</span></span>

<span data-ttu-id="128ca-128">A direção da dependência dentro do aplicativo deve ser na direção de abstração, não os detalhes de implementação.</span><span class="sxs-lookup"><span data-stu-id="128ca-128">The direction of dependency within the application should be in the direction of abstraction, not implementation details.</span></span> <span data-ttu-id="128ca-129">A maioria dos aplicativos é escrita de modo que a dependência em tempo de compilação flua na direção da execução em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="128ca-129">Most applications are written such that compile-time dependency flows in the direction of runtime execution.</span></span> <span data-ttu-id="128ca-130">Isso produz um grafo de dependência direta.</span><span class="sxs-lookup"><span data-stu-id="128ca-130">This produces a direct dependency graph.</span></span> <span data-ttu-id="128ca-131">Ou seja, se o módulo A chamar uma função no módulo B, que chama uma função no módulo C, em tempo de compilação, A dependerá de B que dependerá de C, conforme mostrado na Figura 4-1.</span><span class="sxs-lookup"><span data-stu-id="128ca-131">That is, if module A calls a function in module B, which calls a function in module C, then at compile time A will depend on B which will depend on C, as shown in Figure 4-1.</span></span>

![](./media/image4-1.png)

<span data-ttu-id="128ca-132">**Figura 4-1.**</span><span class="sxs-lookup"><span data-stu-id="128ca-132">**Figure 4-1.**</span></span> <span data-ttu-id="128ca-133">Grafo de dependência direta.</span><span class="sxs-lookup"><span data-stu-id="128ca-133">Direct dependency graph.</span></span>

<span data-ttu-id="128ca-134">A aplicação do princípio da inversão de dependência permite que A chame métodos em uma abstração implementada por B, possibilitando que A chame B em tempo de execução, mas que B dependa de uma interface controlada por A em tempo de compilação (*invertendo*, portanto, a dependência típica em tempo de compilação).</span><span class="sxs-lookup"><span data-stu-id="128ca-134">Applying the dependency inversion principle allows A to call methods on an abstraction that B implements, making it possible for A to call B at runtime, but for B to depend on an interface controlled by A at compile time (thus, *inverting* the typical compile-time dependency).</span></span> <span data-ttu-id="128ca-135">Em tempo de execução, o fluxo da execução do programa permanece inalterado, mas a introdução de interfaces significa que diferentes implementações dessas interfaces podem ser conectadas com facilidade.</span><span class="sxs-lookup"><span data-stu-id="128ca-135">At run time, the flow of program execution remains unchanged, but the introduction of interfaces means that different implementations of these interfaces can easily be plugged in.</span></span>

![](./media/image4-2.png)

<span data-ttu-id="128ca-136">**Figura 4-2.**</span><span class="sxs-lookup"><span data-stu-id="128ca-136">**Figure 4-2.**</span></span> <span data-ttu-id="128ca-137">Grafo de dependência invertida.</span><span class="sxs-lookup"><span data-stu-id="128ca-137">Inverted dependency graph.</span></span>

<span data-ttu-id="128ca-138">A **inversão de dependência** é uma parte fundamental da criação de aplicativos com acoplamento flexível, pois os detalhes de implementação podem ser escritos para que eles dependam de abstrações de nível superior e implemente-as, em vez do inverso.</span><span class="sxs-lookup"><span data-stu-id="128ca-138">**Dependency inversion** is a key part of building loosely-coupled applications, since implementation details can be written to depend on and implement higher level abstractions, rather than the other way around.</span></span> <span data-ttu-id="128ca-139">Como resultado, os aplicativos resultantes são mais testáveis, modulares e de manutenção mais fácil.</span><span class="sxs-lookup"><span data-stu-id="128ca-139">The resulting applications are more testable, modular, and maintainable as a result.</span></span> <span data-ttu-id="128ca-140">A prática da *injeção de dependência* se tornou possível pela observância do princípio da inversão de dependência.</span><span class="sxs-lookup"><span data-stu-id="128ca-140">The practice of *dependency injection* is made possible by following the dependency inversion principle.</span></span>

### <a name="explicit-dependencies"></a><span data-ttu-id="128ca-141">Dependências explícitas</span><span class="sxs-lookup"><span data-stu-id="128ca-141">Explicit dependencies</span></span>

<span data-ttu-id="128ca-142">**Métodos e classes devem exigir explicitamente os objetos de colaboração de que precisam para funcionarem corretamente.**</span><span class="sxs-lookup"><span data-stu-id="128ca-142">**Methods and classes should explicitly require any collaborating objects they need in order to function correctly.**</span></span> <span data-ttu-id="128ca-143">Os construtores de classe oferecem uma oportunidade para que as classes identifiquem os itens necessários para que estejam em um estado válido e funcionem corretamente.</span><span class="sxs-lookup"><span data-stu-id="128ca-143">Class constructors provide an opportunity for classes to identify the things they need in order to be in a valid state and to function properly.</span></span> <span data-ttu-id="128ca-144">Se você definir classes que podem ser construídas e chamadas, mas que só funcionarão corretamente se certos componentes globais ou da infraestrutura estiverem em vigor, essas classes estarão sendo *desonestas* com seus clientes.</span><span class="sxs-lookup"><span data-stu-id="128ca-144">If you define classes that can be constructed and called, but which will only function properly if certain global or infrastructure components are in place, these classes are being *dishonest* with their clients.</span></span> <span data-ttu-id="128ca-145">O contrato do construtor informa o cliente de que ele precisa apenas dos itens especificados (possivelmente nada se a classe estiver usando apenas um construtor sem parâmetros), mas, em seguida, em tempo de execução, acontece que o objeto realmente precisou de outra coisa.</span><span class="sxs-lookup"><span data-stu-id="128ca-145">The constructor contract is telling the client that it only needs the things specified (possibly nothing if the class is just using a parameterless constructor), but then at runtime it turns out the object really did need something else.</span></span>

<span data-ttu-id="128ca-146">Seguindo o princípio da dependência explícita, os métodos e as classes estão sendo honestos com seus clientes sobre o que precisam para funcionar.</span><span class="sxs-lookup"><span data-stu-id="128ca-146">By following the explicit dependencies principle, your classes and methods are being honest with their clients about what they need in order to function.</span></span> <span data-ttu-id="128ca-147">Isso torna o código mais autodocumentado e os contratos de codificação mais amigáveis, pois os usuários confiarão que, desde que eles forneçam o que é necessário na forma de método ou de parâmetros do construtor, os objetos com os quais eles estão trabalhando se comportarão corretamente em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="128ca-147">This makes your code more self-documenting and your coding contracts more user-friendly, since users will come to trust that as long as they provide what's required in the form of method or constructor parameters, the objects they're working with will behave correctly at runtime.</span></span>

### <a name="single-responsibility"></a><span data-ttu-id="128ca-148">Responsabilidade única</span><span class="sxs-lookup"><span data-stu-id="128ca-148">Single responsibility</span></span>

<span data-ttu-id="128ca-149">O princípio da responsabilidade única se aplica ao design orientado a objeto, mas também pode ser considerado um princípio de arquitetura semelhante à separação de interesses.</span><span class="sxs-lookup"><span data-stu-id="128ca-149">The single responsibility principle applies to object-oriented design, but can also be considered as an architectural principle similar to separation of concerns.</span></span> <span data-ttu-id="128ca-150">Ele informa que os objetos devem ter apenas uma responsabilidade e que devem ter apenas uma única razão para serem alterados.</span><span class="sxs-lookup"><span data-stu-id="128ca-150">It states that objects should have only one responsibility and that they should have only one reason to change.</span></span> <span data-ttu-id="128ca-151">Especificamente, a única situação na qual o objeto deve ser alterado é se a maneira na qual ele executa sua responsabilidade única precisa ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="128ca-151">Specifically, the only situation in which the object should change is if the manner in which it performs its one responsibility must be updated.</span></span> <span data-ttu-id="128ca-152">A observância desse princípio ajuda a produzir sistemas modulares e com acoplamento mais flexível, pois muitos tipos de novos comportamentos podem ser implementados como novas classes, em vez de pela adição de mais responsabilidades para as classes existentes.</span><span class="sxs-lookup"><span data-stu-id="128ca-152">Following this principle helps to produce more loosely-coupled and modular systems, since many kinds of new behavior can be implemented as new classes, rather than by adding additional responsibility to existing classes.</span></span> <span data-ttu-id="128ca-153">A adição de novas classes sempre é mais segura do que a alteração das classes existentes, pois nenhum código ainda depende das novas classes.</span><span class="sxs-lookup"><span data-stu-id="128ca-153">Adding new classes is always safer than changing existing classes, since no code yet depends on the new classes.</span></span>

<span data-ttu-id="128ca-154">Em um aplicativo monolítico, podemos aplicar o princípio da responsabilidade única em um alto nível às camadas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="128ca-154">In a monolithic application, we can apply the single responsibility principle at a high level to the layers in the application.</span></span> <span data-ttu-id="128ca-155">A responsabilidade de apresentação deve permanecer no projeto de interface do usuário, enquanto a responsabilidade de acesso a dados deve ser mantida em um projeto de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="128ca-155">Presentation responsibility should remain in the UI project, while data access responsibility should be kept within an infrastructure project.</span></span> <span data-ttu-id="128ca-156">A lógica de negócios deve ser mantida no projeto de núcleo do aplicativo, no qual ela pode ser testada com facilidade e pode evoluir de maneira independente das outras responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="128ca-156">Business logic should be kept in the application core project, where it can be easily tested and can evolve independently from other responsibilities.</span></span>

<span data-ttu-id="128ca-157">Quando esse princípio é aplicado à arquitetura do aplicativo e levado para seu ponto de extremidade lógico, você obtém os microsserviços.</span><span class="sxs-lookup"><span data-stu-id="128ca-157">When this principle is applied to application architecture, and taken to its logical endpoint, you get microservices.</span></span> <span data-ttu-id="128ca-158">Um microsserviço específico deve ter uma única responsabilidade.</span><span class="sxs-lookup"><span data-stu-id="128ca-158">A given microservice should have a single responsibility.</span></span> <span data-ttu-id="128ca-159">Caso você precise estender o comportamento de um sistema, será melhor fazer isso adicionando outros microsserviços, em vez de pela adição de responsabilidade a um existente.</span><span class="sxs-lookup"><span data-stu-id="128ca-159">If you need to extend the behavior of a system, it's usually better to do it by adding additional microservices, rather than by adding responsibility to an existing one.</span></span>

[<span data-ttu-id="128ca-160">Saiba mais sobre a arquitetura de microsserviços</span><span class="sxs-lookup"><span data-stu-id="128ca-160">Learn more about microservices architecture</span></span>](https://aka.ms/MicroservicesEbook)

### <a name="dont-repeat-yourself-dry"></a><span data-ttu-id="128ca-161">DRY (Don't Repeat Yourself)</span><span class="sxs-lookup"><span data-stu-id="128ca-161">Don't repeat yourself (DRY)</span></span>

<span data-ttu-id="128ca-162">O aplicativo deve evitar especificar o comportamento relacionado a determinado conceito em vários locais, pois essa é uma fonte frequente de erros.</span><span class="sxs-lookup"><span data-stu-id="128ca-162">The application should avoid specifying behavior related to a particular concept in multiple places as this is a frequent source of errors.</span></span> <span data-ttu-id="128ca-163">Em algum momento, uma alteração nos requisitos exigirá a alteração desse comportamento e a probabilidade de que, pelo menos, uma instância do comportamento não conseguirá ser atualizada resultará em um comportamento inconsistente do sistema.</span><span class="sxs-lookup"><span data-stu-id="128ca-163">At some point, a change in requirements will require changing this behavior and the likelihood that at least one instance of the behavior will fail to be updated will result in inconsistent behavior of the system.</span></span>

<span data-ttu-id="128ca-164">Em vez de duplicar a lógica, encapsule-a em um constructo de programação.</span><span class="sxs-lookup"><span data-stu-id="128ca-164">Rather than duplicating logic, encapsulate it in a programming construct.</span></span> <span data-ttu-id="128ca-165">Torne esse constructo a autoridade única sobre esse comportamento e imponha o uso desse novo constructo a qualquer outra parte do aplicativo que exija esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="128ca-165">Make this construct the single authority over this behavior, and have any other part of the application that requires this behavior use the new construct.</span></span>

> [!NOTE]
> <span data-ttu-id="128ca-166">Evite associar um comportamento que é apenas coincidentemente repetitivo.</span><span class="sxs-lookup"><span data-stu-id="128ca-166">Avoid binding together behavior that is only coincidentally repetitive.</span></span> <span data-ttu-id="128ca-167">Por exemplo, só porque duas constantes diferentes têm o mesmo valor, isso não significa que você deve ter apenas uma constante, caso elas estejam se referindo a coisas diferentes conceitualmente.</span><span class="sxs-lookup"><span data-stu-id="128ca-167">For example, just because two different constants both have the same value, that doesn't mean you should have only one constant, if conceptually they're referring to different things.</span></span>

### <a name="persistence-ignorance"></a><span data-ttu-id="128ca-168">Ignorância de persistência</span><span class="sxs-lookup"><span data-stu-id="128ca-168">Persistence ignorance</span></span>

<span data-ttu-id="128ca-169">A **PI** (ignorância de persistência) refere-se aos tipos que precisam ser persistidos, mas cujo código não é afetado pela opção de tecnologia de persistência.</span><span class="sxs-lookup"><span data-stu-id="128ca-169">**Persistence ignorance** (PI) refers to types that need to be persisted, but whose code is unaffected by the choice of persistence technology.</span></span> <span data-ttu-id="128ca-170">Esses tipos no .NET são, às vezes, chamados de POCOs (Objetos CRL Básicos), pois não precisam herdar de uma classe base específica nem implementar uma interface específica.</span><span class="sxs-lookup"><span data-stu-id="128ca-170">Such types in .NET are sometimes referred to as Plain Old CLR Objects (POCOs), because they do not need to inherit from a particular base class or implement a particular interface.</span></span> <span data-ttu-id="128ca-171">A ignorância de persistência é importante porque permite que o mesmo modelo de negócios seja persistente de várias maneiras, oferecendo flexibilidade adicional ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="128ca-171">Persistence ignorance is valuable because it allows the same business model to be persisted in multiple ways, offering additional flexibility to the application.</span></span> <span data-ttu-id="128ca-172">As opções de persistência podem ser alteradas ao longo do tempo, de uma tecnologia de banco de dados para outra ou outras formas de persistência podem ser necessárias, além daquela com a qual o aplicativo começou (por exemplo, o uso do Cache Redis ou do Azure DocumentDB, além um banco de dados relacional).</span><span class="sxs-lookup"><span data-stu-id="128ca-172">Persistence choices might change over time, from one database technology to another, or additional forms of persistence might be required in addition to whatever the application started with (for example, using a Redis cache or Azure DocumentDb in addition to a relational database).</span></span>

<span data-ttu-id="128ca-173">Alguns exemplos de violações desse princípio incluem:</span><span class="sxs-lookup"><span data-stu-id="128ca-173">Some examples of violations of this principle include:</span></span>

- <span data-ttu-id="128ca-174">Uma classe base necessária.</span><span class="sxs-lookup"><span data-stu-id="128ca-174">A required base class.</span></span>

- <span data-ttu-id="128ca-175">Uma implementação de interface necessária.</span><span class="sxs-lookup"><span data-stu-id="128ca-175">A required interface implementation.</span></span>

- <span data-ttu-id="128ca-176">Classes responsáveis por salvar a si mesmas (como o padrão de Registro Ativo).</span><span class="sxs-lookup"><span data-stu-id="128ca-176">Classes responsible for saving themselves (such as the Active Record pattern).</span></span>

- <span data-ttu-id="128ca-177">Construtor sem parâmetros necessário.</span><span class="sxs-lookup"><span data-stu-id="128ca-177">Required parameterless constructor.</span></span>

- <span data-ttu-id="128ca-178">Propriedades que exigem uma palavra-chave virtual.</span><span class="sxs-lookup"><span data-stu-id="128ca-178">Properties requiring virtual keyword.</span></span>

- <span data-ttu-id="128ca-179">Atributos necessário específicos da persistência.</span><span class="sxs-lookup"><span data-stu-id="128ca-179">Persistence-specific required attributes.</span></span>

<span data-ttu-id="128ca-180">O requisito de que as classes tenham um dos recursos ou comportamentos acima adiciona um acoplamento entre os tipos a serem persistidos e a opção de tecnologia de persistência, dificultando a adoção de novas estratégias de acesso a dados no futuro.</span><span class="sxs-lookup"><span data-stu-id="128ca-180">The requirement that classes have any of the above features or behaviors adds coupling between the types to be persisted and the choice of persistence technology, making it more difficult to adopt new data access strategies in the future.</span></span>

### <a name="bounded-contexts"></a><span data-ttu-id="128ca-181">Contextos limitados</span><span class="sxs-lookup"><span data-stu-id="128ca-181">Bounded contexts</span></span>

<span data-ttu-id="128ca-182">**Contextos limitados** são um padrão central no Design Controlado por Domínio.</span><span class="sxs-lookup"><span data-stu-id="128ca-182">**Bounded contexts** are a central pattern in Domain-Driven Design.</span></span> <span data-ttu-id="128ca-183">Eles fornecem uma maneira de lidar com a complexidade de aplicativos ou organizações grandes dividindo-os em módulos conceituais separados.</span><span class="sxs-lookup"><span data-stu-id="128ca-183">They provide a way of tackling complexity in large applications or organizations by breaking it up into separate conceptual modules.</span></span> <span data-ttu-id="128ca-184">Em seguida, cada módulo conceitual representa um contexto que é separado de outros contextos (portanto, limitado) e pode evoluir de maneira independente.</span><span class="sxs-lookup"><span data-stu-id="128ca-184">Each conceptual module then represents a context which is separated from other contexts (hence, bounded), and can evolve independently.</span></span> <span data-ttu-id="128ca-185">Cada contexto limitado deve ser, de preferência, livre para escolher seus próprios nomes para conceitos dentro dele e deve ter acesso exclusivo ao seu próprio repositório de persistência.</span><span class="sxs-lookup"><span data-stu-id="128ca-185">Each bounded context should ideally be free to choose its own names for concepts within it, and should have exclusive access to its own persistence store.</span></span>

<span data-ttu-id="128ca-186">No mínimo, os aplicativos Web individuais devem tentar ser seu próprio contexto limitado, com seu próprio repositório de persistência para seu modelo de negócios, em vez de compartilhar um banco de dados com outros aplicativos.</span><span class="sxs-lookup"><span data-stu-id="128ca-186">At a minimum, individual web applications should strive to be their own bounded context, with their own persistence store for their business model, rather than sharing a database with other applications.</span></span> <span data-ttu-id="128ca-187">A comunicação entre contextos limitados ocorre por meio de interfaces programáticas, em vez de por meio de um banco de dados compartilhado, o que permite que a lógica de negócios e os eventos ocorram em resposta às alterações feitas.</span><span class="sxs-lookup"><span data-stu-id="128ca-187">Communication between bounded contexts occurs through programmatic interfaces, rather than through a shared database, which allows for business logic and events to take place in response to changes that take place.</span></span> <span data-ttu-id="128ca-188">Os contextos limitados são mapeados estreitamente aos microsserviços, que também são idealmente implementados como seus próprios contextos limitados individuais.</span><span class="sxs-lookup"><span data-stu-id="128ca-188">Bounded contexts map closely to microservices, which also are ideally implemented as their own individual bounded contexts.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="128ca-189">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="128ca-189">Additional resources</span></span>

* <span data-ttu-id="128ca-190">[JAVA Design Patterns: Principles](https://java-design-patterns.com/principles/) (Padrões de design do JAVA: princípios)</span><span class="sxs-lookup"><span data-stu-id="128ca-190">[JAVA Design Patterns: Principles](https://java-design-patterns.com/principles/)</span></span>
* [<span data-ttu-id="128ca-191">Contexto limitado</span><span class="sxs-lookup"><span data-stu-id="128ca-191">Bounded Context</span></span>](https://martinfowler.com/bliki/BoundedContext.html)

>[!div class="step-by-step"]
><span data-ttu-id="128ca-192">[Anterior](choose-between-traditional-web-and-single-page-apps.md)
>[Próximo](common-web-application-architectures.md)</span><span class="sxs-lookup"><span data-stu-id="128ca-192">[Previous](choose-between-traditional-web-and-single-page-apps.md)
[Next](common-web-application-architectures.md)</span></span>