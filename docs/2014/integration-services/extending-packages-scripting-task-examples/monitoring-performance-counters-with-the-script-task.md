---
title: Monitorar contadores de desempenho com a tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- performance counters [Integration Services]
- SSIS Script task, performance counters
- custom performance counters [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], performance counters
- counters [Integration Services]
ms.assetid: 86609bf1-cae6-435e-a58d-41bdfc521e94
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1cd8b10fb17288806234db923e2ed087f2bd27c8
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968494"
---
# <a name="monitoring-performance-counters-with-the-script-task"></a>Monitorando contadores de desempenho com a tarefa Script
  Talvez administradores precisem monitorar o desempenho de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que executam transformações complexas em grandes volumes de dados. O namespace **System.Diagnostics** do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornece classes para usar contadores de desempenho existentes e para criar contadores de desempenho próprios.  
  
 Os contadores de desempenho armazenam informações de desempenho do aplicativo que podem ser usadas para analisar o desempenho do software com tempo. Contadores de desempenho podem ser monitorados local ou remotamente através da ferramenta **Monitor de Desempenho**. Você pode armazenar os valores de contadores de desempenho em variáveis para posteriormente criar ramificações do fluxo de controle no pacote.  
  
 Como alternativa ao uso de contadores de desempenho, você pode gerar o evento <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> através da propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> do objeto `Dts`. O evento <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> retorna o progresso incremental e informações completas sobre percentual ao runtime [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
> [!NOTE]  
>  Se desejar criar uma tarefa mais fácil de ser reutilizada em vários pacotes, procure utilizar o código desse exemplo de tarefa Script como o ponto inicial de uma tarefa personalizada. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>DESCRIÇÃO  
 O exemplo a seguir cria um contador de desempenho personalizado e incrementa o contador. Primeiro, o exemplo determina se o contador de desempenho já existe. Se o contador de desempenho não tiver sido criado, o script chamará o método `Create` do objeto `PerformanceCounterCategory` para criá-lo. Depois que o contador de desempenho for criado, o script irá incrementá-lo. Finalmente, o exemplo adota a prática ideal de chamar o método `Close` no contador de desempenho quando ele não é mais necessário.  
  
> [!NOTE]  
>  É necessário ter direitos administrativos para criar uma nova categoria de contador de desempenho e um contador de desempenho. Além disso, a nova categoria e o contador permanecem no computador depois da sua criação.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar esse exemplo de tarefa Script  
  
-   Use uma `Imports` instrução em seu código para importar o namespace **System. Diagnostics** .  
  
### <a name="example-code"></a>Código de exemplo  
  
```vb  
Public Sub Main()  
  
    Dim myCounter As PerformanceCounter  
  
    Try  
        'Create the performance counter if it does not already exist.  
        If Not _  
        PerformanceCounterCategory.Exists("TaskExample") Then  
            PerformanceCounterCategory.Create("TaskExample", _  
                "Task Performance Counter Example", "Iterations", _  
                "Number of times this task has been called.")  
        End If  
  
        'Initialize the performance counter.  
        myCounter = New PerformanceCounter("TaskExample", _  
            "Iterations", String.Empty, False)  
  
        'Increment the performance counter.  
        myCounter.Increment()  
  
         myCounter.Close()  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Task Performance Counter Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
  
public class ScriptMain  
{  
  
public void Main()  
        {  
  
            PerformanceCounter myCounter;  
  
            try  
            {  
                //Create the performance counter if it does not already exist.  
                if (!PerformanceCounterCategory.Exists("TaskExample"))  
                {  
                    PerformanceCounterCategory.Create("TaskExample", "Task Performance Counter Example", "Iterations", "Number of times this task has been called.");  
                }  
  
                //Initialize the performance counter.  
                myCounter = new PerformanceCounter("TaskExample", "Iterations", String.Empty, false);  
  
                //Increment the performance counter.  
                myCounter.Increment();  
  
                myCounter.Close();  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Task Performance Counter Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
```  
  
![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  
