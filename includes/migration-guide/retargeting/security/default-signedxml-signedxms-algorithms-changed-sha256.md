---
ms.openlocfilehash: 12ba683655319e42368f9f2a6cf7bf70e1dbd77d
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859016"
---
### <a name="default-signedxml-and-signedxms-algorithms-changed-to-sha256"></a>Algoritmos SignedXML e SignedXMS padrão alterados para SHA256

|   |   |
|---|---|
|Detalhes|No .NET Framework 4.7 e anteriores, SignedXML e SignedCMS usam SHA1 como padrão para algumas operações. A partir do .NET Framework 4.7.1, SHA256 é habilitado por padrão para essas operações. Essa alteração é necessária porque SHA1 não é mais considerado seguro.|
|Sugestão|Há dois novos valores de alternância de contexto para controlar se SHA1 (inseguro) ou SHA256 é usado por padrão:<ul><li>Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms</li><li>Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms</li></ul>Para aplicativos destinados ao .NET Framework 4.7.1 e a versões posteriores, se o uso de SHA256 for indesejável, você poderá restaurar o padrão para SHA1 adicionando a seguinte opção de configuração à seção do [tempo de execução](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) do arquivo de configuração de seu aplicativo:<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms=true;Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms=true&quot; /&gt;&#13;&#10;</code></pre>Para aplicativos destinados ao .NET Framework 4.7 e a versões anteriores, é possível aceitar essa alteração adicionando a seguinte opção de configuração à seção do [tempo de execução](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) do arquivo de configuração de seu aplicativo:<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms=false;Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms=false&quot; /&gt;&#13;&#10;</code></pre>|
|Escopo|Secundário|
|Versão|4.7.1|
|Tipo|Redirecionando|
|APIs afetadas|<ul><li><xref:System.Security.Cryptography.Pkcs.CmsSigner?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.Reference?displayProperty=nameWithType></li></ul>|

