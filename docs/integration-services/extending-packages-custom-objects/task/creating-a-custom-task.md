---
description: Criando uma tarefa personalizada
title: Criar uma tarefa personalizada | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom tasks [Integration Services], creating
ms.assetid: 42965c09-1782-4cdb-9ce1-216af4c23e0a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c7f6f2892210371837bb2940e56266582e729e99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477374"
---
# <a name="creating-a-custom-task"></a>Criando uma tarefa personalizada

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  As etapas envolvidas na criação de uma tarefa personalizada são semelhantes às etapas de criação de qualquer outro objeto personalizado do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Crie uma classe nova herdada da classe base. Para uma tarefa, a classe base é [Microsoft.SqlServer.Dts.Runtime.Task](/dotnet/api/microsoft.sqlserver.dts.runtime.task).  
  
-   Aplique o atributo que identifica o tipo de objeto para a classe. Para uma tarefa, o atributo é <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>.  
  
-   Substitua a implementação dos métodos e propriedades da classe base. Para uma tarefa, isso inclui os métodos <xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
-   Opcionalmente, desenvolva uma interface de usuário personalizada. Para uma tarefa, isso requer uma classe que implementa a interface <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>.  
  
## <a name="getting-started-with-a-custom-task"></a>Guia de introdução com uma tarefa personalizada  
  
### <a name="creating-projects-and-classes"></a>Criando projetos e classes  
 Como todas as tarefas gerenciadas derivam da classe base [Microsoft.SqlServer.Dts.Runtime.Task](/dotnet/api/microsoft.sqlserver.dts.runtime.task), a primeira etapa ao criar uma tarefa personalizada é criar um projeto de biblioteca de classes na linguagem de programação gerenciada de sua preferência e criar uma classe herdada da classe base. Nessa classe derivada, você substituirá os métodos e propriedades da classe base para implementar sua funcionalidade personalizada.  
  
 Na mesma solução, crie um segundo projeto de biblioteca de classe para a interface de usuário personalizada. Recomenda-se um assembly separado para a interface de usuário para facilitar a implantação pois ela permite que você atualize e reimplante o gerenciador de conexões ou sua interface de usuário de forma independente.  
  
 Configure ambos os projetos para atribuir os assemblies que serão gerados no momento de compilação usando um arquivo de chave de nome forte.  
  
### <a name="applying-the-dtstask-attribute"></a>Aplicando o atributo DtsTask  
 Aplique o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> à classe que você criou para identificar isso como uma tarefa. Esse atributo fornece informações de tempo de design como o nome, a descrição e o tipo da tarefa.  
  
 Use a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A> para vincular a tarefa à sua interface de usuário personalizada. Para obter o token de chave pública exigido para essa propriedade, você pode usar o **sn.exe -t** para exibir o token de chave pública por meio do arquivo de par de chaves (.snk) a ser usado para assinar o assembly da interface do usuário.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.SSIS.Samples  
{  
  [DtsTask  
  (  
   DisplayName = "MyTask",  
   IconResource = "MyTask.MyTaskIcon.ico",  
   UITypeName = "My Custom Task," +  
   "Version=1.0.0.0," +  
   "Culture = Neutral," +  
   "PublicKeyToken = 12345abc6789de01",  
   TaskType = "PackageMaintenance",  
   TaskContact = "MyTask; company name; any other information",  
   RequiredProductLevel = DTSProductLevel.None  
   )]  
  public class MyTask : Task  
  {  
    // Your code here.  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsTask(DisplayName:="MyTask", _  
 IconResource:="MyTask.MyTaskIcon.ico", _  
 UITypeName:="My Custom Task," & _  
 "Version=1.0.0.0,Culture=Neutral," & _  
 "PublicKeyToken=12345abc6789de01", _  
 TaskType:="PackageMaintenance", _  
 TaskContact:="MyTask; company name; any other information", _  
 RequiredProductLevel:=DTSProductLevel.None)> _  
Public Class MyTask  
  Inherits Task  
  
  ' Your code here.  
  
End Class 'MyTask  
```  
  
## <a name="building-deploying-and-debugging-a-custom-task"></a>Compilando, implantando e depurando uma tarefa personalizada  
 As etapas para compilar, implantar e depurar uma tarefa personalizada no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] são semelhantes às etapas necessárias para outros tipos de objetos personalizados. Para obter mais informações, consulte [Compilar, implantar e depurar objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)   
 [Codificar uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)   
 [Desenvolver uma interface do usuário para uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
  
  
