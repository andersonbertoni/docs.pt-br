---
title: 'Como: definir o modo de segurança'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Mode property
- WCF, security mode
- WCF, security
ms.assetid: 6e01dd9f-b5dd-4474-b24c-06e124de4ff7
ms.openlocfilehash: 6bd81bd24d28f0a9e318d60a3b7fb4aa059f9a49
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971984"
---
# <a name="how-to-set-the-security-mode"></a>Como: definir o modo de segurança

A segurança do Windows Communication Foundation (WCF) tem três modos de segurança comuns encontrados na maioria das associações predefinidas: transporte, mensagem e "transporte com credencial de mensagem". Dois modos adicionais são específicos de duas associações: o modo "somente credencial de transporte" encontrado no <xref:System.ServiceModel.BasicHttpBinding>, e o modo "ambos", encontrado <xref:System.ServiceModel.NetMsmqBinding>no. No entanto, este tópico se concentra nos três modos de segurança <xref:System.ServiceModel.SecurityMode.Transport>comuns <xref:System.ServiceModel.SecurityMode.Message>:, <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>e.

Observe que nem toda Associação predefinida dá suporte a todos esses modos. Este tópico define o modo com as <xref:System.ServiceModel.WSHttpBinding> classes <xref:System.ServiceModel.NetTcpBinding> e e demonstra como definir o modo de forma programática e por meio da configuração.

Para obter mais informações, consulte segurança do WCF, consulte [visão geral de segurança](../../../docs/framework/wcf/feature-details/security-overview.md), [protegendo serviços](../../../docs/framework/wcf/securing-services.md)e [protegendo serviços e clientes](../../../docs/framework/wcf/feature-details/securing-services-and-clients.md). Para obter mais informações sobre o modo de transporte e a mensagem, consulte [segurança de transporte](../../../docs/framework/wcf/feature-details/transport-security.md) e [segurança de mensagem](../../../docs/framework/wcf/feature-details/message-security-in-wcf.md).

## <a name="to-set-the-security-mode-in-code"></a>Para definir o modo de segurança no código

1. Crie uma instância da classe de associação que você está usando. Para obter uma lista de associações predefinidas, consulte [associações fornecidas pelo sistema](../../../docs/framework/wcf/system-provided-bindings.md). Este exemplo cria uma instância da <xref:System.ServiceModel.WSHttpBinding> classe.

2. Defina a `Mode` Propriedade do objeto retornado `Security` pela propriedade.

     [!code-csharp[c_SettingSecurityMode#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#1)]
     [!code-vb[c_SettingSecurityMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#1)]

     Como alternativa, defina o modo como mensagem, conforme mostrado no código a seguir.

     [!code-csharp[c_SettingSecurityMode#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#2)]
     [!code-vb[c_SettingSecurityMode#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#2)]

     Ou defina o modo como transporte com credenciais de mensagem, conforme mostrado no código a seguir.

     [!code-csharp[c_SettingSecurityMode#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#3)]
     [!code-vb[c_SettingSecurityMode#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#3)]

3. Você também pode definir o modo no construtor da associação, conforme mostrado no código a seguir.

     [!code-csharp[c_SettingSecurityMode#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#4)]
     [!code-vb[c_SettingSecurityMode#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#4)]

## <a name="setting-the-clientcredentialtype-property"></a>Definindo a propriedade ClientCredentialtype

Definir o modo como um dos três valores determina como você define a `ClientCredentialType` propriedade. Por exemplo, usando a <xref:System.ServiceModel.WSHttpBinding> classe, definir o modo como `Transport` significa que você deve <xref:System.ServiceModel.HttpTransportSecurity> definir <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> a propriedade da classe como um valor apropriado.

### <a name="to-set-the-clientcredentialtype-property-for-transport-mode"></a>Para definir a propriedade ClientCredentialtype para o modo de transporte

1. Crie uma instância da associação.

2. Defina a propriedade `Mode` como `Transport`.

3. Defina a propriedade `ClientCredential` com um valor apropriado. O código a seguir define a propriedade `Windows`como.

     [!code-csharp[c_SettingSecurityMode#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#5)]
     [!code-vb[c_SettingSecurityMode#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#5)]

### <a name="to-set-the-clientcredentialtype-property-for-message-mode"></a>Para definir a propriedade ClientCredentialtype para o modo de mensagem

1. Crie uma instância da associação.

2. Defina a propriedade `Mode` como `Message`.

3. Defina a propriedade `ClientCredential` com um valor apropriado. O código a seguir define a propriedade `Certificate`como.

     [!code-csharp[c_SettingSecurityMode#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#6)]
     [!code-vb[c_SettingSecurityMode#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#6)]

### <a name="to-set-the-mode-and-clientcredentialtype-property-in-configuration"></a>Para definir o modo e a propriedade ClientCredentialtype na configuração

1. Adicione um elemento Binding apropriado ao [ \<elemento bindings >](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) do arquivo de configuração. O exemplo a seguir adiciona um [ \<elemento WSHttpBinding >](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) .

2. Adicione um `<binding>` elemento e defina seu `name` atributo como um valor apropriado.

3. Adicione um `<security>` elemento e defina o `mode` atributo como `Message`, `Transport`ou `TransportWithMessageCredential`.

4. Se o modo for definido como `Transport`, adicione um `<transport>` elemento e defina o `clientCredential` atributo como um valor apropriado.

     O exemplo a seguir define o modo como`Transport"`"e, em seguida `clientCredentialType` , define o `<transport>` atributo do elemento`Windows"`como".

    ```xml
    <wsHttpBinding>
    <binding name="TransportSecurity">
        <security mode="Transport" >
           <transport clientCredentialType = "Windows" />
        </security>
    </binding>
    </wsHttpBinding >
    ```

     Como alternativa, defina `security mode` como "`Message"`, seguido por um `<"message">` elemento. Este exemplo define o `clientCredentialType` como "`Certificate"`.

    ```xml
    <wsHttpBinding>
    <binding name="MessageSecurity">
        <security mode="Message" >
           <message clientCredentialType = "Certificate" />
        </security>
    </binding>
    </wsHttpBinding >
    ```

     Usar o <xref:System.ServiceModel.BasicHttpSecurityMode.TransportWithMessageCredential> valor é um caso especial e é explicado abaixo.

### <a name="using-transportwithmessagecredential"></a>Usando TransportWithMessageCredential

Ao definir o modo de segurança `TransportWithMessageCredential`como, o transporte determina o mecanismo real que fornece a segurança em nível de transporte. Por exemplo, o protocolo HTTP usa protocolo SSL (SSL) via HTTP (HTTPS). Portanto, a definição `ClientCredentialType` da propriedade de qualquer objeto de segurança de transporte <xref:System.ServiceModel.HttpTransportSecurity>(como) é ignorada.  Em outras palavras, você só pode definir o `ClientCredentialType` do objeto de segurança da mensagem (para `WSHttpBinding` a associação, <xref:System.ServiceModel.NonDualMessageSecurityOverHttp> o objeto).

Para obter mais informações, confira [Como: Use segurança de transporte e credenciais](../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md)de mensagem.

## <a name="see-also"></a>Consulte também

- [Como: Configurar uma porta com um certificado SSL](../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)
- [Como: Usar segurança de transporte e credenciais de mensagem](../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md)
- [Segurança de transporte](../../../docs/framework/wcf/feature-details/transport-security.md)
- [Segurança de mensagem](../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)
- [Visão geral de segurança](../../../docs/framework/wcf/feature-details/security-overview.md)
- [Associações fornecidas pelo sistema](../../../docs/framework/wcf/system-provided-bindings.md)
- [\<security>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)
- [\<security>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md)
- [\<security>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)
