---
title: Orquestrar microsserviços e aplicativos de vários contêineres para alta escalabilidade e disponibilidade
description: Descubra as opções para orquestrar microsserviços e aplicativos de vários contêineres para alta escalabilidade e disponibilidade e as possibilidades de Azure Dev Spaces durante o desenvolvimento do ciclo de vida de aplicativos Kubernetes.
ms.date: 09/20/2018
ms.openlocfilehash: 76fa68cee41f8d1f34ec399c346f457efae57151
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68675023"
---
# <a name="orchestrating-microservices-and-multi-container-applications-for-high-scalability-and-availability"></a><span data-ttu-id="0d7a5-103">Orquestrar microsserviços e aplicativos de vários contêineres para alta escalabilidade e disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0d7a5-103">Orchestrating microservices and multi-container applications for high scalability and availability</span></span>

<span data-ttu-id="0d7a5-104">O uso de orquestradores em aplicativos prontos para produção é essencial se o aplicativo for baseado em microsserviços ou simplesmente dividido em vários contêineres.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-104">Using orchestrators for production-ready applications is essential if your application is based on microservices or simply split across multiple containers.</span></span> <span data-ttu-id="0d7a5-105">Conforme apresentado anteriormente, em uma abordagem baseada em microsserviço, cada microsserviço tem seu próprio modelo e dados para que seja autônomo de um ponto de vista de desenvolvimento e implantação.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-105">As introduced previously, in a microservice-based approach, each microservice owns its model and data so that it will be autonomous from a development and deployment point of view.</span></span> <span data-ttu-id="0d7a5-106">No entanto, se o aplicativo for mais tradicional, composto por diversos serviços (como o SOA), também haverá vários contêineres ou serviços que abrangem um único aplicativo de negócios e precisam ser implantados como um sistema distribuído.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-106">But even if you have a more traditional application that's composed of multiple services (like SOA), you'll also have multiple containers or services comprising a single business application that need to be deployed as a distributed system.</span></span> <span data-ttu-id="0d7a5-107">Esses tipos de sistemas são difíceis de escalar horizontalmente e gerenciar; portanto, um orquestrador é absolutamente necessário para ter um aplicativo pronto para produção, escalonável e com vários contêineres.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-107">These kinds of systems are complex to scale out and manage; therefore, you absolutely need an orchestrator if you want to have a production-ready and scalable multi-container application.</span></span>

<span data-ttu-id="0d7a5-108">A Figura 4-23 ilustra a implantação de um aplicativo composto por vários microsserviços (contêineres) em um cluster.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-108">Figure 4-23 illustrates deployment into a cluster of an application composed of multiple microservices (containers).</span></span>

![Aplicativos do Docker compostos em um cluster: você pode usar um contêiner para cada instância de serviço.](./media/image23.png)

<span data-ttu-id="0d7a5-111">**Figura 4-23**.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-111">**Figure 4-23**.</span></span> <span data-ttu-id="0d7a5-112">Um cluster de contêineres</span><span class="sxs-lookup"><span data-stu-id="0d7a5-112">A cluster of containers</span></span>

<span data-ttu-id="0d7a5-113">Parece ser uma abordagem lógica.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-113">It looks like a logical approach.</span></span> <span data-ttu-id="0d7a5-114">Mas como você lida com o balanceamento de carga, roteamento e orquestração desses aplicativos compostos?</span><span class="sxs-lookup"><span data-stu-id="0d7a5-114">But how are you handling load-balancing, routing, and orchestrating these composed applications?</span></span>

<span data-ttu-id="0d7a5-115">O Docker Engine simples em hosts individuais do Docker atende às necessidades de gerenciamento de instâncias de imagem única em um host, mas fica aquém quando se trata de gerenciar vários contêineres implantados em diversos hosts de aplicativos distribuídos mais complexos.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-115">The plain Docker Engine in single Docker hosts meets the needs of managing single image instances on one host, but it falls short when it comes to managing multiple containers deployed on multiple hosts for more complex distributed applications.</span></span> <span data-ttu-id="0d7a5-116">Na maioria dos casos, é necessária uma plataforma de gerenciamento que inicie os contêineres automaticamente, escale horizontalmente os que têm várias instâncias por imagem, suspenda-os ou desligue-os quando preciso e também controlem como eles acessam recursos como a rede e o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-116">In most cases, you need a management platform that will automatically start containers, scale-out containers with multiple instances per image, suspend them or shut them down when needed, and ideally also control how they access resources like the network and data storage.</span></span>

<span data-ttu-id="0d7a5-117">Para ir além do gerenciamento de contêineres individuais ou aplicativos compostos muito simples e em direção a aplicativos empresariais com microsserviços, é necessário adotar a orquestração e as plataformas de clustering.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-117">To go beyond the management of individual containers or very simple composed apps and move toward larger enterprise applications with microservices, you must turn to orchestration and clustering platforms.</span></span>

<span data-ttu-id="0d7a5-118">De uma perspectiva de arquitetura e desenvolvimento, ao criar aplicativos empresariais grandes, compostos e baseados em microsserviços, é importante entender as seguintes plataformas e produtos que dão suporte a cenários avançados:</span><span class="sxs-lookup"><span data-stu-id="0d7a5-118">From an architecture and development point of view, if you're building large enterprise composed of microservices-based applications, it's important to understand the following platforms and products that support advanced scenarios:</span></span>

<span data-ttu-id="0d7a5-119">**Clusters e orquestradores.**</span><span class="sxs-lookup"><span data-stu-id="0d7a5-119">**Clusters and orchestrators.**</span></span> <span data-ttu-id="0d7a5-120">Quando é preciso expandir os aplicativos em vários hosts do Docker, como um aplicativo grande baseado em microsserviço, é essencial ter a capacidade de gerenciar todos esses hosts como um cluster único, abstraindo a complexidade da plataforma subjacente.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-120">When you need to scale out applications across many Docker hosts, as when a large microservice-based application, it's critical to be able to manage all those hosts as a single cluster by abstracting the complexity of the underlying platform.</span></span> <span data-ttu-id="0d7a5-121">É isso que os clusters e orquestradores de contêineres fazem.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-121">That's what the container clusters and orchestrators provide.</span></span> <span data-ttu-id="0d7a5-122">O Kubernetes é um exemplo de orquestrador e está disponível no Azure por meio do Serviço de Kubernetes do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-122">Kubernetes is an example of an orchestrator, and is available in Azure through Azure Kubernetes Service.</span></span>

<span data-ttu-id="0d7a5-123">**Agendadores.**</span><span class="sxs-lookup"><span data-stu-id="0d7a5-123">**Schedulers.**</span></span> <span data-ttu-id="0d7a5-124">*Agendamento* é a capacidade do administrador de iniciar contêineres em um cluster para que eles também forneçam uma interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-124">*Scheduling* means to have the capability for an administrator to launch containers in a cluster so they also provide a UI.</span></span> <span data-ttu-id="0d7a5-125">O agendador do cluster tem diversas responsabilidades: usar os recursos de cluster de forma eficiente, definir as restrições fornecidas pelo usuário, balancear a carga dos contêineres em nós ou hosts de maneira eficaz, ser robusto contra erros e, ao mesmo tempo, oferecer alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-125">A cluster scheduler has several responsibilities: to use the cluster's resources efficiently, to set the constraints provided by the user, to efficiently load-balance containers across nodes or hosts, and to be robust against errors while providing high availability.</span></span>

<span data-ttu-id="0d7a5-126">Os conceitos de "cluster" e "agendador" estão intimamente relacionados, então os produtos oferecidos por diferentes fornecedores geralmente têm as duas capacidades.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-126">The concepts of a cluster and a scheduler are closely related, so the products provided by different vendors often provide both sets of capabilities.</span></span> <span data-ttu-id="0d7a5-127">A lista a seguir mostra a plataforma mais importante e opções de software para clusters e agendadores.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-127">The following list shows the most important platform and software choices you have for clusters and schedulers.</span></span> <span data-ttu-id="0d7a5-128">Geralmente, esses orquestradores são oferecidos em nuvens públicas como o Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-128">These orchestrators are generally offered in public clouds like Azure.</span></span>

## <a name="software-platforms-for-container-clustering-orchestration-and-scheduling"></a><span data-ttu-id="0d7a5-129">Plataformas de software para clustering, orquestração e agendamento de contêineres</span><span class="sxs-lookup"><span data-stu-id="0d7a5-129">Software platforms for container clustering, orchestration, and scheduling</span></span>

### <a name="kubernetes"></a><span data-ttu-id="0d7a5-130">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0d7a5-130">Kubernetes</span></span>

![Logotipo do Kubernetes](./media/image24.png)

> <span data-ttu-id="0d7a5-132">O [*Kubernetes*](https://kubernetes.io/) é um produto de software livre que oferece funcionalidades que variam da infraestrutura do cluster e do agendamento de contêiner a capacidades de orquestração.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-132">[*Kubernetes*](https://kubernetes.io/) is an open-source product that provides functionality that ranges from cluster infrastructure and container scheduling to orchestrating capabilities.</span></span> <span data-ttu-id="0d7a5-133">Com ele, é possível automatizar a implantação, o escalonamento e as operações de contêineres de aplicativo em clusters de hosts.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-133">It lets you automate deployment, scaling, and operations of application containers across clusters of hosts.</span></span>
>
> <span data-ttu-id="0d7a5-134">O *Kubernetes* oferece uma infraestrutura centrada no contêiner que agrupa contêineres de aplicativo em unidades lógicas para facilitar o gerenciamento e a descoberta.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-134">*Kubernetes* provides a container-centric infrastructure that groups application containers into logical units for easy management and discovery.</span></span>
>
> <span data-ttu-id="0d7a5-135">O *Kubernetes* é maduro no Linux e menos maduro no Windows.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-135">*Kubernetes* is mature in Linux, less mature in Windows.</span></span>

### <a name="azure-kubernetes-service-aks"></a><span data-ttu-id="0d7a5-136">AKS (Serviço de Kubernetes do Azure)</span><span class="sxs-lookup"><span data-stu-id="0d7a5-136">Azure Kubernetes Service (AKS)</span></span>

![Logotipo do Serviço de Kubernetes do Azure](./media/image41.png)

> <span data-ttu-id="0d7a5-138">O [Serviço de Kubernetes do Azure (AKS)](https://azure.microsoft.com/services/kubernetes-service/) é um serviço de orquestração de contêiner de Kubernetes gerenciado no Azure que simplifica o gerenciamento, a implantação e as operações do cluster do Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-138">[Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service/) is a managed Kubernetes container orchestration service in Azure that simplifies Kubernetes cluster’s management, deployment, and operations.</span></span>

## <a name="using-container-based-orchestrators-in-microsoft-azure"></a><span data-ttu-id="0d7a5-139">Usar orquestradores baseados em contêiner no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0d7a5-139">Using container-based orchestrators in Microsoft Azure</span></span>

<span data-ttu-id="0d7a5-140">Diversos provedores de nuvem oferecem suporte a contêineres do Docker e seus clusters e orquestração, como o Microsoft Azure, o Amazon EC2 Container Service e o Google Container Engine.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-140">Several cloud vendors offer Docker containers support plus Docker clusters and orchestration support, including Microsoft Azure, Amazon EC2 Container Service, and Google Container Engine.</span></span> <span data-ttu-id="0d7a5-141">O Microsoft Azure fornece suporte ao orquestrador e ao cluster do Docker por meio do AKS (Serviço de Kubernetes do Azure).</span><span class="sxs-lookup"><span data-stu-id="0d7a5-141">Microsoft Azure provides Docker cluster and orchestrator support through Azure Kubernetes Service (AKS).</span></span>

## <a name="using-azure-kubernetes-service"></a><span data-ttu-id="0d7a5-142">Usando o Serviço de Kubernetes do Azure</span><span class="sxs-lookup"><span data-stu-id="0d7a5-142">Using Azure Kubernetes Service</span></span>

<span data-ttu-id="0d7a5-143">Um cluster do Kubernetes cria um pool de diversos hosts do Docker e os expõe como um host virtual único. Assim, é possível implantar vários contêineres no cluster e expandir com qualquer número de instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-143">A Kubernetes cluster pools multiple Docker hosts and exposes them as a single virtual Docker host, so you can deploy multiple containers into the cluster and scale-out with any number of container instances.</span></span> <span data-ttu-id="0d7a5-144">O cluster lidará com todos os detalhes complexos de gerenciamento, como escalabilidade, integridade e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-144">The cluster will handle all the complex management plumbing, like scalability, health, and so forth.</span></span>

<span data-ttu-id="0d7a5-145">O AKS é uma maneira de simplificar a criação, configuração e gerenciamento de um cluster de máquinas virtuais no Azure pré-configuradas para executar aplicativos em contêineres.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-145">AKS provides a way to simplify the creation, configuration, and management of a cluster of virtual machines in Azure that are preconfigured to run containerized applications.</span></span> <span data-ttu-id="0d7a5-146">Ao utilizar uma configuração otimizada de ferramentas de software livre conhecidas de agendamento e orquestração, o AKS permite o uso de habilidades existentes ou recorre ao grande e crescente conhecimento da comunidade para implantar e gerenciar aplicativos baseados em contêiner no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-146">Using an optimized configuration of popular open-source scheduling and orchestration tools, AKS enables you to use your existing skills or draw on a large and growing body of community expertise to deploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="0d7a5-147">O Serviço de Kubernetes do Azure otimiza a configuração de ferramentas de software livre e tecnologias conhecidas do Docker especificamente para o Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-147">Azure Kubernetes Service optimizes the configuration of popular Docker clustering open-source tools and technologies specifically for Azure.</span></span> <span data-ttu-id="0d7a5-148">É uma solução aberta que oferece portabilidade para contêineres e configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-148">You get an open solution that offers portability for both your containers and your application configuration.</span></span> <span data-ttu-id="0d7a5-149">Selecione o tamanho, a quantidade de hosts e as ferramentas de orquestrador e deixe o AKS cuidar de todo o resto.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-149">You select the size, the number of hosts, and the orchestrator tools, and AKS handles everything else.</span></span>

![Estrutura de cluster Kubernetes: há um nó mestre que manipula o DNS, o agendador, o proxy, entre outros e vários nós de trabalho que hospedam os contêineres.](media/image36.png)

<span data-ttu-id="0d7a5-151">**Figura 4-24**.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-151">**Figure 4-24**.</span></span> <span data-ttu-id="0d7a5-152">Topologia e estrutura simplificadas do cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0d7a5-152">Kubernetes cluster's simplified structure and topology</span></span>

<span data-ttu-id="0d7a5-153">Na figura 4-24 veja a estrutura de um cluster Kubernetes em que um nó mestre (VM) controla a maior parte da coordenação do cluster e você pode implantar contêineres no restante dos nós que são gerenciados como um único pool de um ponto de vista do aplicativo, permitindo dimensionar para milhares ou até mesmo dezenas de milhares de contêineres.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-153">In figure 4-24 you can see the structure of a Kubernetes cluster where a master node (VM) controls most of the coordination of the cluster and you can deploy containers to the rest of the nodes which are managed as a single pool from an application point of view and allows you to scale to thousands or even tens of thousands of containers.</span></span>

## <a name="development-environment-for-kubernetes"></a><span data-ttu-id="0d7a5-154">Ambiente de desenvolvimento para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0d7a5-154">Development environment for Kubernetes</span></span>

<span data-ttu-id="0d7a5-155">No ambiente de desenvolvimento, o [Docker anunciou em julho de 2018](https://blog.docker.com/2018/07/kubernetes-is-now-available-in-docker-desktop-stable-channel/) que o Kubernetes também pode ser executado em um único computador de desenvolvimento (Windows 10 ou macOS) simplesmente instalando o [Docker Desktop](https://docs.docker.com/install/).</span><span class="sxs-lookup"><span data-stu-id="0d7a5-155">In the development environment, [Docker announced in July 2018](https://blog.docker.com/2018/07/kubernetes-is-now-available-in-docker-desktop-stable-channel/) that Kubernetes can also run in a single development machine (Windows 10 or macOS) by simply installing [Docker Desktop](https://docs.docker.com/install/).</span></span> <span data-ttu-id="0d7a5-156">Posteriormente, você pode implantar para a nuvem (AKS) para testes de integração posteriores, conforme mostrado na figura 4-25.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-156">You can later deploy to the cloud (AKS) for further integration tests, as shown in figure 4-25.</span></span>

![O Docker anunciou o suporte a computador de desenvolvimento para clusters Kubernetes em julho de 2018 com o Docker Desktop.](media/image37.png) 

<span data-ttu-id="0d7a5-158">**Figura 4-25**.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-158">**Figure 4-25**.</span></span> <span data-ttu-id="0d7a5-159">Executando Kubernetes no computador de desenvolvimento e na nuvem</span><span class="sxs-lookup"><span data-stu-id="0d7a5-159">Running Kubernetes in dev machine and the cloud</span></span>

## <a name="getting-started-with-azure-kubernetes-service-aks"></a><span data-ttu-id="0d7a5-160">Introdução ao AKS (Serviço de Kubernetes do Azure)</span><span class="sxs-lookup"><span data-stu-id="0d7a5-160">Getting started with Azure Kubernetes Service (AKS)</span></span> 

<span data-ttu-id="0d7a5-161">Para começar a usar o AKS, implante um cluster do AKS do portal do Azure ou usando a CLI.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-161">To begin using AKS, you deploy an AKS cluster from the Azure portal or by using the CLI.</span></span> <span data-ttu-id="0d7a5-162">Para saber mais sobre como implantar um cluster do Kubernetes no Azure, veja [Implantar um cluster do AKS (Serviço de Kubernetes do Azure)](https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal).</span><span class="sxs-lookup"><span data-stu-id="0d7a5-162">For more information on deploying a Kubernetes cluster in Azure, see [Deploy an Azure Kubernetes Service (AKS) cluster](https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal).</span></span>

<span data-ttu-id="0d7a5-163">Nenhum valor é cobrado pelos softwares instalados por padrão como parte do AKS.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-163">There are no fees for any of the software installed by default as part of AKS.</span></span> <span data-ttu-id="0d7a5-164">Todas as opções padrão são implementadas com software livre.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-164">All default options are implemented with open-source software.</span></span> <span data-ttu-id="0d7a5-165">O AKS está disponível para várias máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-165">AKS is available for multiple virtual machines in Azure.</span></span> <span data-ttu-id="0d7a5-166">Somente as instâncias de computação escolhidas serão cobradas, bem como outros recursos adjacentes de infraestrutura consumidos, como armazenamento e rede.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-166">You're charged only for the compute instances you choose, as well as the other underlying infrastructure resources consumed, such as storage and networking.</span></span> <span data-ttu-id="0d7a5-167">Não há cobranças adicionais pelo AKS.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-167">There are no incremental charges for AKS itself.</span></span>

<span data-ttu-id="0d7a5-168">Para mais informações sobre a implementação na implantação para Kubernetes com base no kubectl e em arquivos .yaml originais, verifique a postagem [Configurando eShopOnContainers no AKS (Serviço de Kubernetes do Azure)](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.-Setting-the-solution-up-in-AKS-(Azure-Kubernetes-Service)).</span><span class="sxs-lookup"><span data-stu-id="0d7a5-168">For further implementation information on deployment to Kubernetes based on kubectl and original .yaml files, check the post on [Setting eShopOnContainers up in AKS (Azure Kubernetes Service)](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.-Setting-the-solution-up-in-AKS-(Azure-Kubernetes-Service)).</span></span>

## <a name="deploying-with-helm-charts-into-kubernetes-clusters"></a><span data-ttu-id="0d7a5-169">Implantando com gráficos do Helm em clusters Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0d7a5-169">Deploying with Helm charts into Kubernetes clusters</span></span>

<span data-ttu-id="0d7a5-170">Ao implantar um aplicativo em um cluster Kubernetes, você pode usar a ferramenta de CLI kubectl.exe original usando arquivos de implantação com base no formato nativo (arquivos .yaml), conforme já mencionado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-170">When deploying an application to a Kubernetes cluster, you can use the original kubectl.exe CLI tool using deployment files based on the native format (.yaml files), as already mentioned in the previous section.</span></span> <span data-ttu-id="0d7a5-171">No entanto, para aplicativos mais complexos do Kubernetes, como ao implantar aplicativos complexos baseados em microsserviços, é recomendável usar o [Helm](https://helm.sh/).</span><span class="sxs-lookup"><span data-stu-id="0d7a5-171">However, for more complex Kubernetes applications such as when deploying complex microservice-based applications, it's recommended to use [Helm](https://helm.sh/).</span></span>

<span data-ttu-id="0d7a5-172">Os Gráficos do Helm ajudam você a definir, realizar controle de versão, instalar, compartilhar, atualizar ou reverter até mesmo o aplicativo mais complexo do Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-172">Helm Charts helps you define, version, install, share, upgrade or rollback even the most complex Kubernetes application.</span></span>

<span data-ttu-id="0d7a5-173">Indo mais além, o uso do Helm também é recomendável porque ambientes adicionais do Kubernetes no Azure, tais como [Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces), também são baseados em gráficos do Helm.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-173">Going further, Helm usage is also recommended because additional Kubernetes environments in Azure, such as [Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces) are also based on Helm charts.</span></span>

<span data-ttu-id="0d7a5-174">O Helm é mantido pela [CNCF (Fundação de Computação Nativa na Nuvem)](https://www.cncf.io/), em colaboração com Microsoft, Google, Bitnami e a comunidade de colaboradores do Helm.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-174">Helm is maintained by the [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io/) - in collaboration with Microsoft, Google, Bitnami and the Helm contributor community.</span></span>

<span data-ttu-id="0d7a5-175">Para mais informações sobre a implementação sobre os gráficos do Helm e o Kubernetes, verifique a postagem [Usando gráficos do Helm para implantar o eShopOnContainers no AKS](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.1-Deploying-to-AKS-using-Helm-Charts).</span><span class="sxs-lookup"><span data-stu-id="0d7a5-175">For further implementation information on Helm charts and Kubernetes check the post on [Using Helm Charts to deploy eShopOnContainers to AKS](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.1-Deploying-to-AKS-using-Helm-Charts).</span></span>

## <a name="use-azure-dev-spaces-for-your-kubernetes-application-lifecycle"></a><span data-ttu-id="0d7a5-176">Usar o Azure Dev Spaces para o ciclo de vida do aplicativo do Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0d7a5-176">Use Azure Dev Spaces for your Kubernetes application lifecycle</span></span>

<span data-ttu-id="0d7a5-177">O [Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces) fornece uma experiência de desenvolvimento rápida e iterativa do Kubernetes para equipes.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-177">[Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces) provides a rapid, iterative Kubernetes development experience for teams.</span></span> <span data-ttu-id="0d7a5-178">Com uma configuração mínima de computador de desenvolvimento, você pode executar e depurar contêineres iterativamente diretamente no AKS (Serviço de Kubernetes do Azure).</span><span class="sxs-lookup"><span data-stu-id="0d7a5-178">With minimal dev machine setup, you can iteratively run and debug containers directly in Azure Kubernetes Service (AKS).</span></span> <span data-ttu-id="0d7a5-179">Desenvolva em Windows, Mac ou Linux usando ferramentas familiares como o Visual Studio, o Visual Studio Code ou a linha de comando.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-179">Develop on Windows, Mac, or Linux using familiar tools like Visual Studio, Visual Studio Code, or the command line.</span></span>

<span data-ttu-id="0d7a5-180">Conforme mencionado, o Azure Dev Spaces usa gráficos do Helm ao implantar os aplicativos baseados em contêiner.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-180">As mentioned, Azure Dev Spaces uses Helm charts when deploying the container-based applications.</span></span>

<span data-ttu-id="0d7a5-181">O Azure Dev Spaces ajuda as equipes de desenvolvimento a serem mais produtivas no Kubernetes, pois permite que você itere e depure rapidamente o código diretamente em um cluster Kubernetes global no Azure, simplesmente usando o Visual Studio 2017 ou Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-181">Azure Dev Spaces helps development teams be more productive on Kubernetes because it allows you to rapidly iterate and debug code directly in a global Kubernetes cluster in Azure by simply using Visual Studio 2017 or Visual Studio Code.</span></span> <span data-ttu-id="0d7a5-182">Esse cluster Kubernetes no Azure é um cluster Kubernetes gerenciado compartilhado, de modo que sua equipe pode trabalhar conjuntamente de forma colaborativa.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-182">That Kubernetes cluster in Azure is a shared managed Kubernetes cluster, so your team can collaboratively work together.</span></span> <span data-ttu-id="0d7a5-183">Você pode desenvolver o código de forma isolada, depois implantar no cluster global e realizar testes de ponta a ponta com outros componentes sem replicar ou criar dependências fictícias.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-183">You can develop your code in isolation, then deploy to the global cluster and do end-to-end testing with other components without replicating or mocking up dependencies.</span></span>

<span data-ttu-id="0d7a5-184">Conforme mostrado na Figura 4-26, o recurso mais diferencial no Azure Dev Spaces é a capacidade de criar "espaços" que podem ser executados integrados ao restante da implantação global no cluster.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-184">As shown in figure 4-26, the most differential feature in Azure Dev Spaces is capability of creating 'spaces' that can run integrated to the rest of the global deployment in the cluster.</span></span>

![O Azure Dev Spaces pode misturar e combinar microsserviços de produção transparentemente com a instância de contêiner de desenvolvimento, para facilitar o teste de novas versões.](media/image38.png)

<span data-ttu-id="0d7a5-186">**Figura 4-26**.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-186">**Figure 4-26**.</span></span> <span data-ttu-id="0d7a5-187">Usando vários espaços no Azure Dev Spaces</span><span class="sxs-lookup"><span data-stu-id="0d7a5-187">Using multiple spaces in Azure Dev Spaces</span></span>

<span data-ttu-id="0d7a5-188">Basicamente, você pode configurar um espaço de desenvolvimento compartilhado no Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-188">Basically you can set up a shared dev space in Azure.</span></span> <span data-ttu-id="0d7a5-189">Cada desenvolvedor pode se concentrar apenas em sua parte do aplicativo e pode desenvolver iterativamente um código de pré-confirmação em um espaço de desenvolvimento que já contém todos os outros serviços e recursos de nuvem dos quais seus cenários dependem.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-189">Each developer can focus on just their part of the application, and can iteratively develop pre-commit code in a dev space that already contains all the other services and cloud resources that their scenarios depend on.</span></span> <span data-ttu-id="0d7a5-190">As dependências estão sempre atualizadas e os desenvolvedores trabalham de uma forma que reflete a produção.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-190">Dependencies are always up-to-date, and developers are working in a way that mirrors production.</span></span>

<span data-ttu-id="0d7a5-191">O Azure Dev Spaces oferece o conceito de um espaço, que permite trabalhar em relativo isolamento e sem medo de interromper o trabalho da equipe.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-191">Azure Dev Spaces provides the concept of a space, which allows you to work in relative isolation, and without the fear of breaking your team's work.</span></span> <span data-ttu-id="0d7a5-192">Cada espaço de desenvolvimento faz parte de uma estrutura hierárquica que permite que você substitua um ou muitos microsserviços a partir do espaço de desenvolvimento mestre “top” com seu próprio microsserviço em andamento.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-192">Each dev space is part of a hierarchical structure that allows you to override one microservice (or many), from the "top" master dev space, with your own work-in-progress microservice.</span></span>

<span data-ttu-id="0d7a5-193">Esse recurso se baseia nos prefixos de URL, portanto, ao usar qualquer prefixo de espaço de desenvolvimento na URL, uma solicitação é enviada do microsserviço de destino caso ele exista no espaço de desenvolvimento; caso contrário, ela é encaminhada até a primeira instância do microsserviço de destino encontrado na hierarquia, chegando ao espaço de desenvolvimento mestre na parte superior em algum momento.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-193">This feature is based on URL prefixes, so when using any dev space prefix in the url, a request is served from the target microservice if it exists in the dev space, otherwise it's forwarded up to the first instance of the target microservice found in the hierarchy, eventually getting to the master dev space at the top.</span></span>

<span data-ttu-id="0d7a5-194">Você pode ver a [página de wiki de eShopOnContainers no Azure Dev Spaces](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.1-Using-Azure-Dev-Spaces-and-AKS) para obter uma visão prática em um exemplo concreto.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-194">You can see the [eShopOnContainers wiki page on Azure Dev Spaces](https://github.com/dotnet-architecture/eShopOnContainers/wiki/10.1-Using-Azure-Dev-Spaces-and-AKS), to get a practical view on a concrete example.</span></span>

<span data-ttu-id="0d7a5-195">Para obter mais informações, confira o artigo sobre [Desenvolvimento em equipe com o Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/team-development-netcore).</span><span class="sxs-lookup"><span data-stu-id="0d7a5-195">For further information check the article on [Team Development with Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/team-development-netcore).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d7a5-196">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0d7a5-196">Additional resources</span></span>

- <span data-ttu-id="0d7a5-197">**Introdução ao AKS (Serviço de Kubernetes do Azure)**  </span><span class="sxs-lookup"><span data-stu-id="0d7a5-197">**Getting started with Azure Kubernetes Service (AKS)** </span></span>\
  <https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal>

- <span data-ttu-id="0d7a5-198">**Azure Dev Spaces** </span><span class="sxs-lookup"><span data-stu-id="0d7a5-198">**Azure Dev Spaces** </span></span>\
  <https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces>

- <span data-ttu-id="0d7a5-199">**Kubernetes** O site oficial.</span><span class="sxs-lookup"><span data-stu-id="0d7a5-199">**Kubernetes** The official site.</span></span> \
  <https://kubernetes.io/>

>[!div class="step-by-step"]
><span data-ttu-id="0d7a5-200">[Anterior](resilient-high-availability-microservices.md)
>[Próximo](../docker-application-development-process/index.md)</span><span class="sxs-lookup"><span data-stu-id="0d7a5-200">[Previous](resilient-high-availability-microservices.md)
[Next](../docker-application-development-process/index.md)</span></span>