---
title: Usando o protocolo SSL
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Networking
- SSL
- Secure Sockets Layer
- requesting data from Internet, Secure Sockets Layer
- sending data, Secure Sockets Layer
- Network Resources
- data requests, Secure Sockets Layer
- receiving data, Secure Sockets Layer
- Internet, Secure Sockets Layer
ms.assetid: 6e4289e6-d1b7-4e82-ab0d-e83e3b6063ed
ms.openlocfilehash: 9cfa8d6a71898a1d1ea91825ffc9a37f4654ebd5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64583529"
---
# <a name="using-secure-sockets-layer"></a>Usando o protocolo SSL
As classes <xref:System.Net> usam o protocolo SSL para criptografar a conexão para vários protocolos de rede.  
  
 Para conexões HTTP, as classes <xref:System.Net.WebRequest> e <xref:System.Net.WebResponse> usam o SSL para se comunicarem com hosts Web que dão suporte ao SSL. A decisão de usar o SSL é feita pela classe <xref:System.Net.WebRequest>, com base no URI fornecido. Se o URI começa com “https:”, o SSL é usado; se o URI começa com “http:”, uma conexão não criptografada é usada.  
  
 Para usar o SSL com o protocolo FTP, defina a propriedade <xref:System.Net.FtpWebRequest.EnableSsl> como verdadeiro antes de chamar <xref:System.Net.FtpWebRequest.GetResponse>. Da mesma forma, para usar o SSL com o protocolo SMTP, defina a propriedade <xref:System.Net.Mail.SmtpClient.EnableSsl> como verdadeira antes de enviar o email.  
  
 A classe <xref:System.Net.Security.SslStream> fornece uma abstração baseada em fluxo para o SSL e oferece muitas maneiras de configurar o handshake SSL.  
  
## <a name="example"></a>Exemplo  
  
### <a name="code"></a>Código  
  
```vb  
Dim MyURI As String = "https://www.contoso.com/"  
Dim Wreq As WebRequest = WebRequest.Create(MyURI)  
  
Dim serverUri As String = "ftp://ftp.contoso.com/file.txt"  
Dim request As FtpWebRequest = CType(WebRequest.Create(serverUri), FtpWebRequest)  
request.Method = WebRequestMethods.Ftp.DeleteFile  
request.EnableSsl = True  
Dim response As FtpWebResponse = CType(request.GetResponse(), FtpWebResponse)  
```  
  
```csharp  
String MyURI = "https://www.contoso.com/";  
WebRequest WReq = WebRequest.Create(MyURI);  
  
String serverUri = "ftp://ftp.contoso.com/file.txt"  
FtpWebRequest request = (FtpWebRequest)WebRequest.Create(serverUri);  
request.EnableSsl = true;  
request.Method = WebRequestMethods.Ftp.DeleteFile;  
FtpWebResponse response = (FtpWebResponse)request.GetResponse();  
```  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Este exemplo requer:  
  
- Referências ao namespace **System.Net**.  
  
## <a name="see-also"></a>Consulte também

- [Segurança na programação de rede](../../../docs/framework/network-programming/security-in-network-programming.md)
- [Programação de rede no .NET Framework](../../../docs/framework/network-programming/index.md)
- [Seleção e validação de certificado](../../../docs/framework/network-programming/certificate-selection-and-validation.md)
