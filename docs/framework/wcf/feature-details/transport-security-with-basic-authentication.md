---
title: Segurança de transporte com autenticação básica
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b54f491d-196b-4279-876c-76b83ec0442c
ms.openlocfilehash: 5cbe6ce6e8e36fc9460295c454014d6f3fbf3983
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64635125"
---
# <a name="transport-security-with-basic-authentication"></a>Segurança de transporte com autenticação básica
A ilustração a seguir mostra um serviço Windows Communication Foundation (WCF) e um cliente. O servidor precisa de um certificado X.509 válido que pode ser usado para Secure Sockets Layer (SSL) e os clientes devem confiar em certificado do servidor. Além disso, o serviço Web já tem uma implementação de SSL que pode ser usada. Para obter mais informações sobre como habilitar a autenticação básica no Internet Information Services (IIS), consulte <https://go.microsoft.com/fwlink/?LinkId=83822>.  
  
 ![Captura de tela que mostra a segurança de transporte com autenticação básica.](./media/transport-security-with-basic-authentication/transport-security-basic-authentication.gif)  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Modo de segurança|Transporte|  
|Interoperabilidade|Com os serviços e clientes de serviço Web existentes|  
|Autenticação (servidor)<br /><br /> Autenticação (cliente)|Sim (usando HTTPS)<br /><br /> Sim (por meio do nome de usuário/senha)|  
|Integridade|Sim|  
|Confidencialidade|Sim|  
|Transporte|HTTPS|  
|Associação|<xref:System.ServiceModel.WSHttpBinding>|  
  
## <a name="service"></a>Serviço  
 O código e a configuração a seguir destinam-se para executar de forma independente. Realize um dos seguintes procedimentos:  
  
- Crie um serviço autônomo usando o código sem nenhuma configuração.  
  
- Criar um serviço usando a configuração fornecida, mas não definir nenhum ponto de extremidade.  
  
### <a name="code"></a>Código  
 O código a seguir mostra como criar um ponto de extremidade de serviço que usa um nome de usuário de domínio do Windows e uma senha para segurança de transferência. Observe que o serviço requer um certificado x. 509 para autenticar o cliente. Para obter mais informações, consulte [trabalhando com certificados](../../../../docs/framework/wcf/feature-details/working-with-certificates.md) e [como: Configurar uma porta com um certificado SSL](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md).  
  
 [!code-csharp[C_SecurityScenarios#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#1)]
 [!code-vb[C_SecurityScenarios#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#1)]  
  
## <a name="configuration"></a>Configuração  
 O exemplo a seguir configura um serviço para usar a autenticação básica com segurança em nível de transporte:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <bindings>  
            <wsHttpBinding>  
                <binding name="UsernameWithTransport">  
                    <security mode="Transport">  
                        <transport clientCredentialType="Basic" />  
                    </security>  
                </binding>  
            </wsHttpBinding>  
        </bindings>  
        <services>  
            <service name="BasicAuthentication.Calculator">  
                <endpoint address="https://localhost/Calculator"  
                          binding="wsHttpBinding"   
                          bindingConfiguration="UsernameWithTransport"  
                          name="BasicEndpoint"   
                          contract="BasicAuthentication.ICalculator" />  
            </service>  
        </services>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>Cliente  
  
### <a name="code"></a>Código  
 O código a seguir mostra o código do cliente que inclui o nome de usuário e senha. Observe que o usuário deve fornecer um nome de usuário do Windows e uma senha válida. O código para retornar o nome de usuário e a senha não é mostrado aqui. Use uma caixa de diálogo ou outra interface para consultar as informações do usuário.  
  
> [!NOTE]
>  Nome de usuário e senha só podem ser definidos usando código.  
  
 [!code-csharp[C_SecurityScenarios#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#2)]
 [!code-vb[C_SecurityScenarios#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#2)]  
  
### <a name="configuration"></a>Configuração  
 O código a seguir mostra a configuração do cliente.  
  
> [!NOTE]
>  Você não pode usar a configuração para definir o nome de usuário e senha. A configuração mostrada aqui deve ser aumentada usando código para definir o nome de usuário e senha.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator" >  
          <security mode="Transport">  
            <transport clientCredentialType="Basic" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="https://machineName/Calculator"   
                binding="wsHttpBinding"  
                bindingConfiguration="WSHttpBinding_ICalculator"   
                contract="ICalculator"  
                name="WSHttpBinding_ICalculator" />  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>
- [Trabalhando com certificados](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [Como: Configurar uma porta com um certificado SSL](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)
- [Visão geral de segurança](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [\<clientCredentials>](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)
- [Modelo de segurança do Windows Server App Fabric](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
