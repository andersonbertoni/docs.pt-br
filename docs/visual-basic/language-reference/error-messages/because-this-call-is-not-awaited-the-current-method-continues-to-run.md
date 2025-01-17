---
title: Como esta chamada não é aguardada, o método atual continua sendo executado antes da chamada ser concluída
ms.date: 07/20/2015
f1_keywords:
- bc42358
- vbc42358
helpviewer_keywords:
- BC42358
ms.assetid: 43342515-c3c8-4155-9263-c302afabcbc2
ms.openlocfilehash: c4704fb09e9519c14f29365b2cf7f536bbbc5dca
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64619556"
---
# <a name="because-this-call-is-not-awaited-the-current-method-continues-to-run-before-the-call-is-completed"></a>Como esta chamada não é aguardada, o método atual continua sendo executado antes da chamada ser concluída
Como esta chamada não era esperada, a execução do método atual continua antes da chamada ser concluída. Considere aplicar o operador 'Await' ao resultado da chamada.  
  
 O método atual chama um método assíncrono que retorna um <xref:System.Threading.Tasks.Task> ou um <xref:System.Threading.Tasks.Task%601> e não se aplica a [Await](../../../visual-basic/language-reference/operators/await-operator.md) operador para o resultado. A chamada ao método assíncrono inicia uma tarefa assíncrona. No entanto, como nenhum operador `Await` é aplicado, o programa continua sem esperar que a tarefa seja concluída. Na maioria dos casos, esse comportamento não é esperado. Geralmente, os outros aspectos do método de chamada dependem dos resultados da chamada ou, no mínimo, é esperado que o método chamado seja concluído antes de retornar do método que contém a chamada.  
  
 Igualmente importante é o que acontece com as exceções que são geradas no método assíncrono chamado. Uma exceção que é acionada em um método que retorna um <xref:System.Threading.Tasks.Task> ou <xref:System.Threading.Tasks.Task%601> é armazenado na tarefa retornada. Se você não aguardar a tarefa ou verificar explicitamente se há exceções, a exceção será perdida. Se você aguardar a tarefa, a exceção será relançada.  
  
 Como uma melhor prática, você sempre deve aguardar a chamada.  
  
 Por padrão, esta mensagem é um aviso. Para obter mais informações sobre como ocultar avisos ou tratar avisos como erros, consulte [Configurando avisos no Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID do erro:** BC42358  
  
### <a name="to-address-this-warning"></a>Para resolver este aviso  
  
- Considere suprimir o aviso somente se você tiver certeza de que não deseja aguardar que a chamada assíncrona seja concluída e que o método chamado não gerará nenhuma exceção. Nesse caso, você pode suprimir o aviso atribuindo o resultado da tarefa da chamada a uma variável.  
  
     O exemplo a seguir mostra como causar o aviso, como suprimi-lo e como aguardar a chamada.  
  
    ```vb  
    Async Function CallingMethodAsync() As Task  
  
        ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
        ' Variable delay is used to slow down the called method so that you  
        ' can distinguish between awaiting and not awaiting in the program's output.   
        ' You can adjust the value to produce the output that this topic shows   
        ' after the code.  
        Dim delay = 5000  
  
        ' Call #1.  
        ' Call an async method. Because you don't await it, its completion isn't   
        ' coordinated with the current method, CallingMethodAsync.  
        ' The following line causes the warning.  
        CalledMethodAsync(delay)  
  
        ' Call #2.  
        ' To suppress the warning without awaiting, you can assign the   
        ' returned task to a variable. The assignment doesn't change how  
        ' the program runs. However, the recommended practice is always to  
        ' await a call to an async method.  
        ' Replace Call #1 with the following line.  
        'Task delayTask = CalledMethodAsync(delay)  
  
        ' Call #3  
        ' To contrast with an awaited call, replace the unawaited call   
        ' (Call #1 or Call #2) with the following awaited call. The best   
        ' practice is to await the call.  
  
        'Await CalledMethodAsync(delay)  
  
        ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
        ' continues to run and, in this example, finishes its work and returns  
        ' to its caller.  
        ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
    End Function  
  
    Async Function CalledMethodAsync(howLong As Integer) As Task  
  
        ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
        ' Slow the process down a little so you can distinguish between awaiting  
        ' and not awaiting. Adjust the value for howLong if necessary.  
        Await Task.Delay(howLong)  
        ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
    End Function  
    ```  
  
     No exemplo, se você escolher a Chamada nº 1 ou Chamada nº 2, o método assíncrono não aguardado (`CalledMethodAsync`) será concluído após o chamador (`CallingMethodAsync`) e o chamador do chamador (`StartButton_Click`) serem concluídos. A última linha na saída a seguir mostra quando o método chamado termina. A entrada e a saída do manipulador de eventos que chama `CallingMethodAsync` no exemplo completo estão marcadas na saída.  
  
    ```  
    Entering the Click event handler.  
      Entering calling method.  
        Entering called method, starting and awaiting Task.Delay.  
      Returning from calling method.  
    Exiting the Click event handler.  
        Task.Delay is finished--returning from called method.  
    ```  
  
## <a name="example"></a>Exemplo  
 O seguinte aplicativo do WPF (Windows Presentation Foundation) contém os métodos do exemplo anterior. As etapas a seguir configuram o aplicativo.  
  
1. Crie um aplicativo WPF e nomeie-o `AsyncWarning`.  
  
2. No Editor do Visual Studio Code, escolha a guia **MainWindow.xaml**.  
  
     Se a guia não estiver visível, abra o menu de atalho para MainWindow.xaml no **Gerenciador de Soluções** e, em seguida, escolha **Exibir Código**.  
  
3. Substitua o código na exibição **XAML** de MainWindow.xaml pelo código a seguir.  
  
    ```vb  
    <Window x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="StartButton_Click" />  
            <TextBox x:Name="ResultsTextBox" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
        </Grid>  
    </Window>  
    ```  
  
     Uma janela simples, contendo um botão e uma caixa de texto, aparecerá no modo de exibição de **Design** de MainWindow.xaml.  
  
     Para obter mais informações sobre o Designer XAML, consulte [Criando uma interface do usuário usando o Designer XAML](/visualstudio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio). Para obter informações sobre como criar sua própria interface do usuário simples, confira as seções "Para criar um aplicativo WPF" e "Para criar um MainWindow simples do WPF" do [Passo a passo: acessar a Web usando Async e Await](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
4. Substitua o código no XAML. vb pelo código a seguir.  
  
    ```vb  
    Class MainWindow   
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
  
            ResultsTextBox.Text &= vbCrLf & "Entering the Click event handler."  
            Await CallingMethodAsync()  
            ResultsTextBox.Text &= vbCrLf & "Exiting the Click event handler."  
        End Sub  
  
        Async Function CallingMethodAsync() As Task  
  
            ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
            ' Variable delay is used to slow down the called method so that you  
            ' can distinguish between awaiting and not awaiting in the program's output.   
            ' You can adjust the value to produce the output that this topic shows   
            ' after the code.  
            Dim delay = 5000  
  
            ' Call #1.  
            ' Call an async method. Because you don't await it, its completion isn't   
            ' coordinated with the current method, CallingMethodAsync.  
            ' The following line causes the warning.  
            CalledMethodAsync(delay)  
  
            ' Call #2.  
            ' To suppress the warning without awaiting, you can assign the   
            ' returned task to a variable. The assignment doesn't change how  
            ' the program runs. However, the recommended practice is always to  
            ' await a call to an async method.  
  
            ' Replace Call #1 with the following line.  
            'Task delayTask = CalledMethodAsync(delay)  
  
            ' Call #3  
            ' To contrast with an awaited call, replace the unawaited call   
            ' (Call #1 or Call #2) with the following awaited call. The best   
            ' practice is to await the call.  
  
            'Await CalledMethodAsync(delay)  
  
            ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
            ' continues to run and, in this example, finishes its work and returns  
            ' to its caller.  
            ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
        End Function  
  
        Async Function CalledMethodAsync(howLong As Integer) As Task  
  
            ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
            ' Slow the process down a little so you can distinguish between awaiting  
            ' and not awaiting. Adjust the value for howLong if necessary.  
            Await Task.Delay(howLong)  
            ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
        End Function  
  
    End Class  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    '     Task.Delay is finished--returning from called method.  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '     Task.Delay is finished--returning from called method.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    ```  
  
5. Escolha a tecla F5 para executar o programa e, em seguida, escolha o botão **Iniciar**.  
  
     A saída esperada será exibida no final do código.  
  
## <a name="see-also"></a>Consulte também

- [Operador Await](../../../visual-basic/language-reference/operators/await-operator.md)
- [Programação assíncrona com Async e Await](../../../visual-basic/programming-guide/concepts/async/index.md)
