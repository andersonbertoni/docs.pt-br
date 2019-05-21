---
title: Aprendizado de máquina automatizado com o ML.NET
description: Visão geral do treinamento e seleção automáticos de modelos
author: natke
ms.date: 05/01/2019
ms.topic: overview
ms.custom: mvc
ms.author: nakersha
ms.openlocfilehash: e6654718f174c9d8b628b05d85d74952c222eb66
ms.sourcegitcommit: 4c10802ad003374641a2c2373b8a92e3c88babc8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65452738"
---
# <a name="automated-machine-learning-with-mlnet"></a><span data-ttu-id="0ee2e-103">Aprendizado de máquina automatizado com o ML.NET</span><span class="sxs-lookup"><span data-stu-id="0ee2e-103">Automated machine learning with ML.NET</span></span>

<span data-ttu-id="0ee2e-104">O aprendizado de máquina automatizado é um recurso do ML.NET que executa a seleção e treinamento automáticos de modelos.</span><span class="sxs-lookup"><span data-stu-id="0ee2e-104">Automated machine learning is a feature of ML.NET that performs automatic model selection and training.</span></span> <span data-ttu-id="0ee2e-105">Você especifica a tarefa de aprendizado de máquina e fornece um conjunto de dados. O ML automatizado escolhe o modelo com as melhores métricas.</span><span class="sxs-lookup"><span data-stu-id="0ee2e-105">You specify the machine learning task and supply a dataset, and automated ML chooses the model with the best metrics.</span></span> <span data-ttu-id="0ee2e-106">Ele produz:</span><span class="sxs-lookup"><span data-stu-id="0ee2e-106">It outputs:</span></span>
- <span data-ttu-id="0ee2e-107">um arquivo de modelo que pode ser carregado em seu aplicativo de previsão</span><span class="sxs-lookup"><span data-stu-id="0ee2e-107">a model file that can be loaded into your prediction application</span></span>
- <span data-ttu-id="0ee2e-108">código do aplicativo para fazer previsões</span><span class="sxs-lookup"><span data-stu-id="0ee2e-108">application code to make predictions</span></span>
- <span data-ttu-id="0ee2e-109">o código-fonte usado para seleção de recursos e o treinamento do modelo (para entender o modelo)</span><span class="sxs-lookup"><span data-stu-id="0ee2e-109">the source code used for feature selection and model training (to understand the model)</span></span>

> [!NOTE]
> <span data-ttu-id="0ee2e-110">Esse recurso está atualmente em versão prévia e o material pode estar sujeito a alterações.</span><span class="sxs-lookup"><span data-stu-id="0ee2e-110">This feature is currently in Preview, and material may be subject to change.</span></span> 

<span data-ttu-id="0ee2e-111">O ML automatizado é atualmente limitado a [tarefas](resources/tasks.md) de aprendizado de máquina de classificação binária, classificação multiclasse e regressão.</span><span class="sxs-lookup"><span data-stu-id="0ee2e-111">Automated ML is currently limited to the machine learning [tasks](resources/tasks.md) of binary classification, multiclass classification, and regression.</span></span> <span data-ttu-id="0ee2e-112">As outras tarefas de aprendizado de máquina terão suporte em versões futuras.</span><span class="sxs-lookup"><span data-stu-id="0ee2e-112">The other machine learning tasks will be supported in future releases.</span></span>

<span data-ttu-id="0ee2e-113">Há três maneiras de usar o ML automatizado:</span><span class="sxs-lookup"><span data-stu-id="0ee2e-113">There are three ways to use automated ML:</span></span>
1. <span data-ttu-id="0ee2e-114">Na linha de comando, com a [CLI do ML.NET](automate-training-with-cli.md)</span><span class="sxs-lookup"><span data-stu-id="0ee2e-114">On the command line, with the [ML.NET CLI](automate-training-with-cli.md)</span></span>
1. <span data-ttu-id="0ee2e-115">Por meio de um aplicativo com a [API de ML automatizada](how-to-guides/how-to-use-the-automl-api.md)</span><span class="sxs-lookup"><span data-stu-id="0ee2e-115">Via an application, with the [automated ML API](how-to-guides/how-to-use-the-automl-api.md)</span></span>
1. <span data-ttu-id="0ee2e-116">Com uma interface gráfica do usuário, com o construtor de modelo do ML.NET</span><span class="sxs-lookup"><span data-stu-id="0ee2e-116">With a graphical user interface, with the the ML.NET Model Builder</span></span>