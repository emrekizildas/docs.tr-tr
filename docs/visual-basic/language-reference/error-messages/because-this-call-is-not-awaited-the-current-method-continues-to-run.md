---
title: Bu çağrı beklenmediğinden, çağrı tamamlanmadan geçerli yöntemin çalıştırılması devam eder
ms.date: 07/20/2015
f1_keywords:
- bc42358
- vbc42358
helpviewer_keywords:
- BC42358
ms.assetid: 43342515-c3c8-4155-9263-c302afabcbc2
ms.openlocfilehash: 6ceebc3af01c13474affa6e728c49d6d246eb331
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701194"
---
# <a name="because-this-call-is-not-awaited-the-current-method-continues-to-run-before-the-call-is-completed"></a>Bu çağrı beklenmediğinden, çağrı tamamlanmadan geçerli yöntemin çalıştırılması devam eder
Bu çağrı beklenmediğinden, çağrı tamamlanmadan önce geçerli yöntemin yürütülmesi devam eder. Çağrının sonucuna ' await ' işlecini uygulamayı düşünün.  
  
 Geçerli yöntem <xref:System.Threading.Tasks.Task> veya <xref:System.Threading.Tasks.Task%601> döndüren zaman uyumsuz bir yöntem çağırır ve sonuca [await](../../../visual-basic/language-reference/operators/await-operator.md) işlecini uygulamaz. Zaman uyumsuz metoda yapılan çağrı zaman uyumsuz bir görev başlatır. Ancak `Await` işleci uygulanmadığından, program görevin tamamlanmasını beklemeden devam eder. Çoğu durumda, bu davranış beklenmez. Genellikle çağıran yöntemin diğer yönleri çağrının sonuçlarına bağlıdır veya, çağrıyı içeren yöntemden döndürmeden önce çağrılan yöntemin tamamlanmasının beklenmez.  
  
 Eşit ölçüde önemli bir sorun, çağrılan zaman uyumsuz yöntemde oluşturulan özel durumlarla gerçekleşen şeydir. @No__t-0 veya <xref:System.Threading.Tasks.Task%601> döndüren bir yöntemde oluşturulan bir özel durum döndürülen görevde saklanır. Görevi beklemezseniz veya özel durumları açıkça denetmezseniz, özel durum kaybolur. Görevi beklekullanacaksanız, özel durumu yeniden oluşturulur.  
  
 En iyi uygulama olarak, her zaman çağrıyı beklemelisiniz.  
  
 Bu ileti, varsayılan olarak bir uyarıdır. Uyarıları gizleme veya uyarıları hata olarak değerlendirme hakkında daha fazla bilgi için bkz. [Visual Basic uyarıları yapılandırma](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Hata kimliği:** BC42358  
  
### <a name="to-address-this-warning"></a>Bu uyarıyı çözmek için  
  
- Yalnızca zaman uyumsuz çağrının tamamlanmasını beklemek istemediğiniz ve çağrılan yöntemin herhangi bir özel durum tetiklemediğinizden emin değilseniz, uyarının görüntülenmesini düşünmelisiniz. Bu durumda, çağrının görev sonucunu bir değişkene atayarak uyarıyı bastırın.  
  
     Aşağıdaki örnek, uyarıya nasıl neden olduğunu, nasıl bastırılacağını ve çağrının nasıl bekleleneceğini gösterir.  
  
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
  
     Örnekte, çağır #1 veya #2 çağır ' ı seçerseniz, hem çağıranı (`CallingMethodAsync`) hem de arayanın çağıranı (`StartButton_Click`) tamamlandıktan sonra geri beklenen zaman uyumsuz Yöntem (`CalledMethodAsync`) tamamlanır. Aşağıdaki çıktıda yer aldığı son satırda, çağrılan yöntemin ne zaman bittiği gösterilmektedir. Tam örnekte `CallingMethodAsync` ' ı çağıran olay işleyiciden giriş ve çıkış, çıkışta işaretlenir.  
  
    ```console  
    Entering the Click event handler.  
      Entering calling method.  
        Entering called method, starting and awaiting Task.Delay.  
      Returning from calling method.  
    Exiting the Click event handler.  
        Task.Delay is finished--returning from called method.  
    ```  
  
## <a name="example"></a>Örnek  
 Aşağıdaki Windows Presentation Foundation (WPF) uygulaması, önceki örnekteki yöntemleri içerir. Aşağıdaki adımlar uygulamayı ayarlar.  
  
1. Bir WPF uygulaması oluşturun ve `AsyncWarning` olarak adlandırın.  
  
2. Visual Studio Code düzenleyicisinde **MainWindow. xaml** sekmesini seçin.  
  
     Sekme görünür değilse, **Çözüm Gezgini**' de MainWindow. xaml için kısayol menüsünü açın ve **kodu görüntüle**' yi seçin.  
  
3. MainWindow. xaml **xaml** görünümündeki kodu aşağıdaki kodla değiştirin.  
  
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
  
     Bir düğme içeren basit bir pencere ve MainWindow. xaml **Tasarım** görünümünde bir metin kutusu görünür.  
  
     XAML Tasarımcısı hakkında daha fazla bilgi için, bkz. [XAML Tasarımcısı kullanarak Kullanıcı arabirimi oluşturma](/visualstudio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio). Kendi basit kullanıcı arabiriminizi derleme hakkında daha fazla bilgi için, bkz. "WPF uygulaması oluşturmak Için" ve [Izlenecek yol: Async ve await kullanarak Web 'e erişme](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
4. MainWindow. xaml. vb içindeki kodu aşağıdaki kodla değiştirin.  
  
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
  
5. Programı çalıştırmak için F5 tuşunu seçin ve sonra **Başlat** düğmesini seçin.  
  
     Beklenen çıkış kodun sonunda görünür.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Await İşleci](../../../visual-basic/language-reference/operators/await-operator.md)
- [Async ve Await ile Zaman Uyumsuz Programlama](../../../visual-basic/programming-guide/concepts/async/index.md)
