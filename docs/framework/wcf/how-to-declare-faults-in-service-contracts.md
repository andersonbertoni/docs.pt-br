---
title: 'Como: declarar falhas em contratos de serviço'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e8da98e7-d22f-4f60-ac82-3fb0928a353f
ms.openlocfilehash: 6f08ef6eb62b31b0969779d51d0a068145a23fc0
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971964"
---
# <a name="how-to-declare-faults-in-service-contracts"></a>Como: declarar falhas em contratos de serviço

No código gerenciado, as exceções são geradas quando ocorrem condições de erro. Nos aplicativos Windows Communication Foundation (WCF), no entanto, os contratos de serviço especificam quais informações de erro são retornadas aos clientes declarando falhas de SOAP no contrato de serviço. Para obter uma visão geral da relação entre exceções e falhas, consulte [especificando e manipulando falhas em contratos e serviços](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md).

## <a name="create-a-service-contract-that-specifies-a-soap-fault"></a>Criar um contrato de serviço que especifica uma falha de SOAP

1. Crie um contrato de serviço que contenha pelo menos uma operação. Para obter um exemplo, consulte [ Defina um contrato](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)de serviço.

2. Selecione uma operação que possa especificar uma condição de erro sobre a qual os clientes podem esperar para serem notificados. Para decidir quais condições de erro justificam o retorno de falhas de SOAP aos clientes, consulte [especificando e manipulando falhas em contratos e serviços](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md).

3. Aplique um <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> à operação selecionada e passe um tipo de falha serializável para o construtor. Para obter detalhes sobre como criar e usar tipos serializáveis, consulte [especificando transferência de dados em contratos de serviço](../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md). O exemplo a seguir mostra como especificar que a `SampleMethod` operação pode resultar em um `GreetingFault`.

     [!code-csharp[FaultContractAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#4)]
     [!code-vb[FaultContractAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#4)]

4. Repita as etapas 2 e 3 para todas as operações no contrato que comunicam condições de erro aos clientes.

## <a name="implementing-an-operation-to-return-a-specified-soap-fault"></a>Implementando uma operação para retornar uma falha de SOAP especificada
 Depois que uma operação tiver especificado que uma falha SOAP específica pode ser retornada (como no procedimento anterior) para comunicar uma condição de erro a um aplicativo de chamada, a próxima etapa será implementar essa especificação.

### <a name="throw-the-specified-soap-fault-in-the-operation"></a>Lançar a falha SOAP especificada na operação

1. Quando uma <xref:System.ServiceModel.FaultContractAttribute>condição de erro especificada ocorre em uma operação, o lança um <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType> novo em que a falha SOAP especificada é o parâmetro de tipo. O exemplo a seguir mostra como lançar o `GreetingFault` `SampleMethod` no mostrado no procedimento anterior e na seção de código a seguir.

     [!code-csharp[FaultContractAttribute#5](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#5)]
     [!code-vb[FaultContractAttribute#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#5)]

## <a name="example"></a>Exemplo

O exemplo de código a seguir mostra uma implementação de uma única operação que `GreetingFault` especifica um `SampleMethod` para a operação.

[!code-csharp[FaultContractAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#1)]
[!code-vb[FaultContractAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#1)]

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>
