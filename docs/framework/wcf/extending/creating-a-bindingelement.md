---
title: Criando um BindingElement
ms.date: 03/30/2017
ms.assetid: 01a35307-a41f-4ef6-a3db-322af40afc99
ms.openlocfilehash: 0c08494315f43f35f60d70abf643f596a013c302
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64587331"
---
# <a name="creating-a-bindingelement"></a>Criando um BindingElement
Associações e elementos de associação (objetos que estendem <xref:System.ServiceModel.Channels.Binding?displayProperty=nameWithType> e <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType>, respectivamente) são o lugar onde o modelo de aplicativo do Windows Communication Foundation (WCF) é associado com as fábricas de canais e ouvintes de canais. Sem associações, usar canais personalizados requer programação no nível de canal como descrito em [programação de nível de serviço canal](../../../../docs/framework/wcf/extending/service-channel-level-programming.md) e [programação de nível de canal do cliente](../../../../docs/framework/wcf/extending/client-channel-level-programming.md). Este tópico discute o requisito mínimo para habilitar o uso do seu canal no WCF, o desenvolvimento de um <xref:System.ServiceModel.Channels.BindingElement> de canal e habilitar o uso do aplicativo conforme descrito na etapa 4 do [canais de desenvolvimento](../../../../docs/framework/wcf/extending/developing-channels.md).  
  
## <a name="overview"></a>Visão geral  
 Criando um <xref:System.ServiceModel.Channels.BindingElement> de seu canal permite que os desenvolvedores a usá-lo em um aplicativo WCF. <xref:System.ServiceModel.Channels.BindingElement> objetos podem ser usados pelo <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> classe para se conectar a um aplicativo do WCF em seu canal sem ter que as informações de tipo exato do seu canal.  
  
 Uma vez um <xref:System.ServiceModel.Channels.BindingElement> tiver sido criado, você pode habilitar mais funcionalidades, dependendo das suas necessidades, seguindo as etapas restantes de desenvolvimento de canal descritas em [canais de desenvolvimento](../../../../docs/framework/wcf/extending/developing-channels.md).  
  
## <a name="adding-a-binding-element"></a>Adicionando um elemento de associação  
 Para implementar um personalizado <xref:System.ServiceModel.Channels.BindingElement>, escrever uma classe que herda de <xref:System.ServiceModel.Channels.BindingElement>. Por exemplo, se você tiver desenvolvido uma `ChunkingChannel` que pode dividir mensagens grandes em partes e remontá-las na outra extremidade, você pode usar esse canal em qualquer associação com a implementação de um <xref:System.ServiceModel.Channels.BindingElement> e configurando a ligação para usá-lo. O restante deste tópico usa o `ChunkingChannel` como um exemplo para demonstrar os requisitos de implementação de um elemento de associação.  
  
 Um `ChunkingBindingElement` é responsável por criar o `ChunkingChannelFactory` e `ChunkingChannelListener`. Ela substitui <xref:System.ServiceModel.Channels.BindingElement.CanBuildChannelFactory%2A> e <xref:System.ServiceModel.Channels.BindingElement.CanBuildChannelListener%2A> implementações e verifica se o parâmetro de tipo está <xref:System.ServiceModel.Channels.IDuplexSessionChannel> (em nosso exemplo, isso é a única forma de canal com suporte pelo `ChunkingChannel`) e que os outros elementos de associação na associação de dar suporte a isso forma de canal.  
  
 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> primeiro verifica que a forma de canal solicitada pode ser criada e, em seguida, obtém uma lista de ações de mensagem a ser fragmentado. Em seguida, cria um novo `ChunkingChannelFactory`, passando-o a fábrica de canais interna. (Se você estiver criando um elemento de associação de transporte, esse elemento é a última na pilha de associação e, portanto, deve criar um ouvinte de canais ou fábrica de canais.)  
  
 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> tem uma implementação semelhante para a criação de `ChunkingChannelListener` e passando-o ouvinte de canais interna.  
  
 Como outro exemplo, usando um canal de transporte, o [transporte: UDP](../../../../docs/framework/wcf/samples/transport-udp.md) exemplo fornece a seguinte substituição.  
  
 No exemplo, é o elemento de associação `UdpTransportBindingElement`, que é derivada de <xref:System.ServiceModel.Channels.TransportBindingElement>. Ele substitui os seguintes métodos para compilar as fábricas associadas ao canal.  
  
```csharp  
public IChannelFactory<TChannel> BuildChannelFactory<TChannel>(BindingContext context)  
{  
    return (IChannelFactory<TChannel>)(object)new UdpChannelFactory(this, context);  
}  
  
public IChannelListener<TChannel> BuildChannelListener<TChannel>(BindingContext context)  
{  
    return (IChannelListener<TChannel>)(object)new UdpChannelListener(this, context);  
}  
```  
  
 Ele também contém membros para clonagem de `BindingElement` e retornando o nosso esquema (soap.udp).  
  
#### <a name="protocol-binding-elements"></a>Elementos de ligação de protocolo  
 Novos elementos de associação podem substituir ou aumentar a qualquer um dos elementos de associação incluído, adicionando novos transportes, codificações ou protocolos de nível mais altos. Para criar um novo elemento de associação de protocolo, iniciar, estendendo o <xref:System.ServiceModel.Channels.BindingElement> classe. No mínimo, em seguida, você deve implementar o <xref:System.ServiceModel.Channels.BindingElement.Clone%2A?displayProperty=nameWithType> e implementar o `ChannelProtectionRequirements` usando <xref:System.ServiceModel.Channels.IChannel.GetProperty%2A?displayProperty=nameWithType>. Isso retorna o <xref:System.ServiceModel.Security.ChannelProtectionRequirements> para este elemento de associação.  Para obter mais informações, consulte <xref:System.ServiceModel.Security.ChannelProtectionRequirements>.  
  
 <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> deve retornar uma nova cópia do elemento de associação. Como prática recomendada, é recomendável que esse elemento de ligação autores implementar <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> usando um construtor de cópia que chama o construtor de cópia base, em seguida, clona outros campos nessa classe.  
  
#### <a name="transport-binding-elements"></a>Elementos de associação de transporte  
 Para criar um novo elemento de associação de transporte, estender o <xref:System.ServiceModel.Channels.TransportBindingElement> interface. No mínimo, em seguida, você deve implementar o <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> método e o <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A?displayProperty=nameWithType> propriedade.  
  
 <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> – Deve retornar uma nova cópia desse elemento de associação.  Como prática recomendada, é recomendável que o autores do elemento de associação implementem Clone por meio de um construtor de cópia que chama o construtor de cópia base e, em seguida, clones de quaisquer campos adicionais nessa classe.  
  
 <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A> – A <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A> obter propriedade retorna o esquema de URI para o protocolo de transporte representado pelo elemento de associação. Por exemplo, o <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType> e o <xref:System.ServiceModel.Channels.TcpTransportBindingElement?displayProperty=nameWithType> retornar "http" e "NET. TCP" de suas respectivas <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A> propriedades.  
  
#### <a name="encoding-binding-elements"></a>Codificação de elementos de associação  
 Para criar a nova codificação elementos de associação, iniciar, estendendo a <xref:System.ServiceModel.Channels.BindingElement> classe e implementando o <xref:System.ServiceModel.Channels.MessageEncodingBindingElement?displayProperty=nameWithType> classe. No mínimo, em seguida, você deve implementar o <xref:System.ServiceModel.Channels.BindingElement.Clone%2A>, <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A?displayProperty=nameWithType> métodos e as <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.MessageVersion%2A?displayProperty=nameWithType> propriedade.  
  
- <xref:System.ServiceModel.Channels.BindingElement.Clone%2A>. Retorna uma nova cópia do elemento de associação. Como prática recomendada, é recomendável que esse elemento de ligação autores implementar <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> usando um construtor de cópia que chama o construtor de cópia base, em seguida, clona outros campos nessa classe.  
  
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A>. Retorna um <xref:System.ServiceModel.Channels.MessageEncoderFactory>, que fornece um identificador para a classe real que implementa o novo codificador e quais devem estender <xref:System.ServiceModel.Channels.MessageEncoder>. Para obter mais informações, consulte <xref:System.ServiceModel.Channels.MessageEncoderFactory> e <xref:System.ServiceModel.Channels.MessageEncoder>.  
  
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.MessageVersion%2A>. Retorna o <xref:System.ServiceModel.Channels.MessageVersion> usado essa codificação, que representa as versões de SOAP e WS-Addressing em uso.  
  
 Para obter uma lista completa de métodos opcionais e propriedades para elementos de ligação de codificação definidas pelo usuário, consulte <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>.  
  
 Para obter mais informações sobre como criar um novo elemento de associação, consulte [Criando associações](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md).  
  
 Depois de criar um elemento de associação para o seu canal, retornar para o [canais de desenvolvimento](../../../../docs/framework/wcf/extending/developing-channels.md) tópico para ver se você deseja adicionar suporte de arquivo de configuração para o elemento de associação, se e como adicionar suporte de publicação de metadados, e Se e como para construir uma associação definida pelo usuário que usa o elemento de associação.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Channels.BindingElement>
- [Desenvolvimento de canais](../../../../docs/framework/wcf/extending/developing-channels.md)
- [Transporte: UDP](../../../../docs/framework/wcf/samples/transport-udp.md)
