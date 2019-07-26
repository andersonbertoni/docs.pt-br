---
ms.openlocfilehash: 6a99ed916e4e86e85d7ebc2d6ea36a6372c00206
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802585"
---
### <a name="aspnet-incorrect-multipart-handling-may-result-in-lost-form-data"></a><span data-ttu-id="18608-101">ASP.NET A manipulação incorreta com várias partes pode resultar na perda dos dados de formulário.</span><span class="sxs-lookup"><span data-stu-id="18608-101">ASP.NET Incorrect multipart handling may result in lost form data.</span></span>

|   |   |
|---|---|
|<span data-ttu-id="18608-102">Detalhes</span><span class="sxs-lookup"><span data-stu-id="18608-102">Details</span></span>|<span data-ttu-id="18608-103">Nos aplicativos que direcionam o .NET Framework 4.7.2 e versões anteriores, o ASP.Net pode analisar incorretamente valores de limite com várias partes, resultando na indisponibilidade dos dados de formulário durante a execução da solicitação.</span><span class="sxs-lookup"><span data-stu-id="18608-103">In applications that target .NET Framework 4.7.2 and earlier versions, ASP.Net might incorrectly parse multipart boundary values, resulting in form data being unavailable during request execution.</span></span> <span data-ttu-id="18608-104">Os aplicativos que direcionam o .NET Framework 4.8 ou versões posteriores analisam corretamente os dados com várias partes para que os valores de formulário estejam disponíveis durante a execução da solicitação.</span><span class="sxs-lookup"><span data-stu-id="18608-104">Applications that target .NET Framework 4.8 or later versions correctly parse multipart data, so form values are available during request execution.</span></span>|
|<span data-ttu-id="18608-105">Sugestão</span><span class="sxs-lookup"><span data-stu-id="18608-105">Suggestion</span></span>|<span data-ttu-id="18608-106">Começando com aplicativos em execução no .NET Framework 4.8, ao direcionar o .NET Framework 4.8 ou posterior usando o elemento <code>targetFrameworkVersion</code>, o comportamento padrão é alterado para retirar os delimitadores.</span><span class="sxs-lookup"><span data-stu-id="18608-106">Starting with applications running on .NET Framework 4.8, when targeting .NET Framework 4.8 or later by using the <code>targetFrameworkVersion</code> element, the default behavior changes to strip delimiters.</span></span> <span data-ttu-id="18608-107">Ao direcionar versões anteriores da estrutura ou não usar <code>targetFrameworkVersion</code>, ainda são retornados delimitadores à direita para alguns valores. Esse comportamento também pode ser explicitamente controlado com um <code>appSetting</code>:</span><span class="sxs-lookup"><span data-stu-id="18608-107">When targeting previous framework versions or not using <code>targetFrameworkVersion</code>, trailing delimiters for some values are still returned.This behavior can also be explicitly controlled with an <code>appSetting</code>:</span></span><pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;appSettings&gt;&#13;&#10;...&#13;&#10;&lt;add key=&quot;aspnet:UseLegacyMultiValueHeaderHandling&quot;  value=&quot;true&quot;/&gt;&#13;&#10;...&#13;&#10;&lt;/appSettings&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|<span data-ttu-id="18608-108">Escopo</span><span class="sxs-lookup"><span data-stu-id="18608-108">Scope</span></span>|<span data-ttu-id="18608-109">Unknown</span><span class="sxs-lookup"><span data-stu-id="18608-109">Unknown</span></span>|
|<span data-ttu-id="18608-110">Versão</span><span class="sxs-lookup"><span data-stu-id="18608-110">Version</span></span>|<span data-ttu-id="18608-111">4.8</span><span class="sxs-lookup"><span data-stu-id="18608-111">4.8</span></span>|
|<span data-ttu-id="18608-112">Tipo</span><span class="sxs-lookup"><span data-stu-id="18608-112">Type</span></span>|<span data-ttu-id="18608-113">Tempo de execução</span><span class="sxs-lookup"><span data-stu-id="18608-113">Runtime</span></span>|
|<span data-ttu-id="18608-114">APIs afetadas</span><span class="sxs-lookup"><span data-stu-id="18608-114">Affected APIs</span></span>|<ul><li><xref:System.Web.HttpRequest.Form?displayProperty=nameWithType></li><li><xref:System.Web.HttpRequest.Files?displayProperty=nameWithType></li><li><xref:System.Web.HttpRequest.ContentEncoding?displayProperty=nameWithType></li></ul>|
