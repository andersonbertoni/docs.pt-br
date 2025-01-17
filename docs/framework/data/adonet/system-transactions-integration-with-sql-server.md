---
title: Integração de System.Transactions com o SQL Server
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b555544e-7abb-4814-859b-ab9cdd7d8716
ms.openlocfilehash: 09fcf3f1a7e58a4bd8c2c6b0d25c24f32ea5ec5e
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65880588"
---
# <a name="systemtransactions-integration-with-sql-server"></a>Integração de System.Transactions com o SQL Server
O .NET Framework versão 2.0 introduziu uma estrutura de transação que pode ser acessada por meio de <xref:System.Transactions> namespace. Essa estrutura expõe transações de forma que é totalmente integrado no .NET Framework, inclusive o ADO.NET.  
  
 Além dos aprimoramentos de programabilidade, <xref:System.Transactions> e ADO.NET podem trabalhar juntos para coordenar as otimizações, quando você trabalha com transações. Uma transação passível de promoção é uma transação leve (local) que pode ser elevada automaticamente a uma transação totalmente distribuída em uma base conforme necessário.  
  
 Começando com o ADO.NET 2.0 <xref:System.Data.SqlClient> dá suporte a transações passíveis de promoção ao trabalhar com o SQL Server. Uma transação passível de promoção não chama a sobrecarga adicional de uma transação distribuída a menos que a sobrecarga adicional seja necessária. Transações passíveis de promoção são automáticas e não exigem intervenção do desenvolvedor.  
  
 Transações passíveis de promoção só estão disponíveis quando você usa o .NET Framework Data Provider para SQL Server (`SqlClient`) com o SQL Server.  
  
## <a name="creating-promotable-transactions"></a>Criando transações passíveis de promoção  
 O provedor do .NET Framework para SQL Server fornece suporte para transações passíveis de promoção, que são tratadas por meio das classes no .NET Framework <xref:System.Transactions> namespace. Transações passíveis de promoção otimizam transações distribuídas, adiando a criação de uma transação distribuída até que ele seja necessário. Se houver apenas um Gerenciador de recursos necessário, nenhuma transação distribuída ocorre.  
  
> [!NOTE]
>  Em um cenário parcialmente confiável, o <xref:System.Transactions.DistributedTransactionPermission> é necessário quando uma transação é promovida a uma transação distribuída.  
  
## <a name="promotable-transaction-scenarios"></a>Cenários de transação passível de promoção  
 Transações distribuídas normalmente consomem recursos significativos do sistema, que está sendo gerenciados pelo Microsoft Distributed Transaction Coordinator (MS DTC), que integra todos os gerenciadores de recursos acessados na transação. Uma transação passível de promoção é uma forma especial de um <xref:System.Transactions> transação que delega efetivamente o trabalho para uma simple transação do SQL Server. <xref:System.Transactions>, <xref:System.Data.SqlClient>, e o SQL Server coordenam o trabalho envolvido no tratamento da transação, elevando-a para uma transação distribuída completa conforme necessário.  
  
 A vantagem de usar transações passíveis de promoção é que quando uma conexão é aberta por meio de um ativo <xref:System.Transactions.TransactionScope> transação e nenhuma outra conexão aberta, a transação é confirmada como uma transação superficial, em vez de incorrer adicional sobrecarga de uma transação distribuída completa.  
  
### <a name="connection-string-keywords"></a>Palavras-chave de cadeia de caracteres de Conexão  
 O <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> propriedade dá suporte a uma palavra-chave `Enlist`, que indica se <xref:System.Data.SqlClient> detecta contextos transacionais e inscrever-se automaticamente a conexão em uma transação distribuída. Se `Enlist=true`, a conexão será inscrita automaticamente no contexto de transação atual do thread de abertura. Se `Enlist=false`, o `SqlClient` conexão não interage com uma transação distribuída. O valor padrão para `Enlist` é verdadeiro. Se `Enlist` não for especificado na cadeia de conexão, a conexão será inscrita automaticamente em uma transação distribuída caso uma seja detectada quando a conexão é aberta.  
  
 O `Transaction Binding` palavras-chave em um <xref:System.Data.SqlClient.SqlConnection> cadeia de caracteres de conexão controlar a associação da conexão com um inscrito `System.Transactions` transação. Ele também está disponível por meio de <xref:System.Data.SqlClient.SqlConnectionStringBuilder.TransactionBinding%2A> propriedade de um <xref:System.Data.SqlClient.SqlConnectionStringBuilder>.  
  
 A tabela a seguir descreve os possíveis valores.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|Implícita desassociar|O padrão. A conexão se desconecta da transação quando ele termina, alternando de volta para o modo de confirmação automática.|  
|Explícito desassociar|A conexão permanece anexado à transação até que a transação seja fechada. A conexão falhará se a transação associada não está ativa ou não corresponde ao <xref:System.Transactions.Transaction.Current%2A>.|  
  
## <a name="using-transactionscope"></a>Usando o TransactionScope  
 O <xref:System.Transactions.TransactionScope> classe torna um bloco de código transacional inscrevendo implicitamente conexões em uma transação distribuída. Você deve chamar o <xref:System.Transactions.TransactionScope.Complete%2A> método no final o <xref:System.Transactions.TransactionScope> bloco antes de deixá-lo. Sair do bloco invoca o <xref:System.Transactions.TransactionScope.Dispose%2A> método. Se uma exceção foi lançada que faz com que o código deixar o escopo, a transação é considerado anulada.  
  
 É recomendável que você use uma `using` bloco para certificar-se de que <xref:System.Transactions.TransactionScope.Dispose%2A> é chamado no <xref:System.Transactions.TransactionScope> objeto que o uso do bloco é encerrado. Falha ao confirmar ou reverter transações pendentes significativamente pode danificar o desempenho porque o tempo limite padrão para o <xref:System.Transactions.TransactionScope> é um minuto. Se você não usar um `using` instrução, você deve executar todo o trabalho em um `Try` bloquear e chamar explicitamente o <xref:System.Transactions.TransactionScope.Dispose%2A> método no `Finally` bloco.  
  
 Se ocorrer uma exceção no <xref:System.Transactions.TransactionScope>, a transação será marcada como inconsistente e abandonada. Ela será revertida quando o <xref:System.Transactions.TransactionScope> é descartado. Se nenhuma exceção ocorrer, confirmar as transações participantes serão.  
  
> [!NOTE]
>  O `TransactionScope` classe cria uma transação com um <xref:System.Transactions.Transaction.IsolationLevel%2A> de `Serializable` por padrão. Dependendo do seu aplicativo, você talvez queira considerar abaixar o nível de isolamento para evitar uma contenção elevada em seu aplicativo.  
  
> [!NOTE]
>  É recomendável que você execute apenas atualizações, inserções e exclusões em transações distribuídas porque eles consomem recursos significativos do banco de dados. Instruções SELECT podem bloquear recursos do banco de dados desnecessariamente e, em alguns cenários, talvez você precise usar transações para seleções. Qualquer trabalho de banco de dados não deve ser feito fora do escopo da transação, a menos que ele envolve outros gerenciadores de recursos transacionados. Embora uma exceção no escopo da transação evitar que a transação seja confirmada, o <xref:System.Transactions.TransactionScope> classe não tem provisão para reverter alterações de seu código tenha feito fora do escopo da própria transação. Se você tiver que executar alguma ação quando a transação for revertida, você deve escrever sua própria implementação do <xref:System.Transactions.IEnlistmentNotification> de interface e inscrevê-la explicitamente na transação.  
  
## <a name="example"></a>Exemplo  
 Trabalhando com <xref:System.Transactions> exige que você tenha uma referência a Transactions.  
  
 A função a seguir demonstra como criar uma transação passível de promoção em duas instâncias do SQL Server diferentes, representado por dois diferentes <xref:System.Data.SqlClient.SqlConnection> objetos, que são encapsulados em um <xref:System.Transactions.TransactionScope> bloco. O código cria o <xref:System.Transactions.TransactionScope> bloco com um `using` instrução e abre a primeira conexão, que inscreve automaticamente no <xref:System.Transactions.TransactionScope>. A transação é inscrita inicialmente como uma transação superficial, não uma transação distribuída completa. A segunda conexão está inscrita no <xref:System.Transactions.TransactionScope> somente se o comando em que a primeira conexão não gerará uma exceção. Quando a segunda conexão for aberta, a transação é promovida automaticamente a uma transação distribuída completa. O <xref:System.Transactions.TransactionScope.Complete%2A> método é invocado, que confirma a transação apenas se nenhuma exceção tiver sido lançada. Se uma exceção tiver sido lançada em qualquer ponto a <xref:System.Transactions.TransactionScope> bloco, `Complete` será não ser chamado e a transação distribuída será revertida quando o <xref:System.Transactions.TransactionScope> é descartada no final do seu `using` bloco.  
  
```csharp  
// This function takes arguments for the 2 connection strings and commands in order  
// to create a transaction involving two SQL Servers. It returns a value > 0 if the  
// transaction committed, 0 if the transaction rolled back. To test this code, you can   
// connect to two different databases on the same server by altering the connection string,  
// or to another RDBMS such as Oracle by altering the code in the connection2 code block.  
static public int CreateTransactionScope(  
    string connectString1, string connectString2,  
    string commandText1, string commandText2)  
{  
    // Initialize the return value to zero and create a StringWriter to display results.  
    int returnValue = 0;  
    System.IO.StringWriter writer = new System.IO.StringWriter();  
  
    // Create the TransactionScope in which to execute the commands, guaranteeing  
    // that both commands will commit or roll back as a single unit of work.  
    using (TransactionScope scope = new TransactionScope())  
    {  
        using (SqlConnection connection1 = new SqlConnection(connectString1))  
        {  
            try  
            {  
                // Opening the connection automatically enlists it in the   
                // TransactionScope as a lightweight transaction.  
                connection1.Open();  
  
                // Create the SqlCommand object and execute the first command.  
                SqlCommand command1 = new SqlCommand(commandText1, connection1);  
                returnValue = command1.ExecuteNonQuery();  
                writer.WriteLine("Rows to be affected by command1: {0}", returnValue);  
  
                // if you get here, this means that command1 succeeded. By nesting  
                // the using block for connection2 inside that of connection1, you  
                // conserve server and network resources by opening connection2   
                // only when there is a chance that the transaction can commit.     
                using (SqlConnection connection2 = new SqlConnection(connectString2))  
                    try  
                    {  
                        // The transaction is promoted to a full distributed  
                        // transaction when connection2 is opened.  
                        connection2.Open();  
  
                        // Execute the second command in the second database.  
                        returnValue = 0;  
                        SqlCommand command2 = new SqlCommand(commandText2, connection2);  
                        returnValue = command2.ExecuteNonQuery();  
                        writer.WriteLine("Rows to be affected by command2: {0}", returnValue);  
                    }  
                    catch (Exception ex)  
                    {  
                        // Display information that command2 failed.  
                        writer.WriteLine("returnValue for command2: {0}", returnValue);  
                        writer.WriteLine("Exception Message2: {0}", ex.Message);  
                    }  
            }  
            catch (Exception ex)  
            {  
                // Display information that command1 failed.  
                writer.WriteLine("returnValue for command1: {0}", returnValue);  
                writer.WriteLine("Exception Message1: {0}", ex.Message);  
            }  
        }  
  
        // If an exception has been thrown, Complete will not   
        // be called and the transaction is rolled back.  
        scope.Complete();  
    }  
  
    // The returnValue is greater than 0 if the transaction committed.  
    if (returnValue > 0)  
    {  
        writer.WriteLine("Transaction was committed.");  
    }  
    else  
    {  
        // You could write additional business logic here, notify the caller by  
        // throwing a TransactionAbortedException, or log the failure.  
        writer.WriteLine("Transaction rolled back.");  
    }  
  
    // Display messages.  
    Console.WriteLine(writer.ToString());  
  
    return returnValue;  
}  
```  
  
```vb  
' This function takes arguments for the 2 connection strings and commands in order  
' to create a transaction involving two SQL Servers. It returns a value > 0 if the  
' transaction committed, 0 if the transaction rolled back. To test this code, you can   
' connect to two different databases on the same server by altering the connection string,  
' or to another RDBMS such as Oracle by altering the code in the connection2 code block.  
Public Function CreateTransactionScope( _  
  ByVal connectString1 As String, ByVal connectString2 As String, _  
  ByVal commandText1 As String, ByVal commandText2 As String) As Integer  
  
    ' Initialize the return value to zero and create a StringWriter to display results.  
    Dim returnValue As Integer = 0  
    Dim writer As System.IO.StringWriter = New System.IO.StringWriter  
  
    ' Create the TransactionScope in which to execute the commands, guaranteeing  
    ' that both commands will commit or roll back as a single unit of work.  
    Using scope As New TransactionScope()  
        Using connection1 As New SqlConnection(connectString1)  
            Try  
                ' Opening the connection automatically enlists it in the   
                ' TransactionScope as a lightweight transaction.  
                connection1.Open()  
  
                ' Create the SqlCommand object and execute the first command.  
                Dim command1 As SqlCommand = New SqlCommand(commandText1, connection1)  
                returnValue = command1.ExecuteNonQuery()  
                writer.WriteLine("Rows to be affected by command1: {0}", returnValue)  
  
                ' If you get here, this means that command1 succeeded. By nesting  
                ' the Using block for connection2 inside that of connection1, you  
                ' conserve server and network resources by opening connection2   
                ' only when there is a chance that the transaction can commit.     
                Using connection2 As New SqlConnection(connectString2)  
                    Try  
                        ' The transaction is promoted to a full distributed  
                        ' transaction when connection2 is opened.  
                        connection2.Open()  
  
                        ' Execute the second command in the second database.  
                        returnValue = 0  
                        Dim command2 As SqlCommand = New SqlCommand(commandText2, connection2)  
                        returnValue = command2.ExecuteNonQuery()  
                        writer.WriteLine("Rows to be affected by command2: {0}", returnValue)  
  
                    Catch ex As Exception  
                        ' Display information that command2 failed.  
                        writer.WriteLine("returnValue for command2: {0}", returnValue)  
                        writer.WriteLine("Exception Message2: {0}", ex.Message)  
                    End Try  
                End Using  
  
            Catch ex As Exception  
                ' Display information that command1 failed.  
                writer.WriteLine("returnValue for command1: {0}", returnValue)  
                writer.WriteLine("Exception Message1: {0}", ex.Message)  
            End Try  
        End Using  
  
        ' If an exception has been thrown, Complete will   
        ' not be called and the transaction is rolled back.  
        scope.Complete()  
    End Using  
  
    ' The returnValue is greater than 0 if the transaction committed.  
    If returnValue > 0 Then  
        writer.WriteLine("Transaction was committed.")  
    Else  
        ' You could write additional business logic here, notify the caller by  
        ' throwing a TransactionAbortedException, or log the failure.  
       writer.WriteLine("Transaction rolled back.")  
     End If  
  
    ' Display messages.  
    Console.WriteLine(writer.ToString())  
  
    Return returnValue  
End Function  
```  
  
## <a name="see-also"></a>Consulte também

- [Transações e simultaneidade](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)
- [ADO.NET Managed Providers and DataSet Developer Center](https://go.microsoft.com/fwlink/?LinkId=217917) (Central de desenvolvedores do DataSet e de provedores gerenciados do ADO.NET)
