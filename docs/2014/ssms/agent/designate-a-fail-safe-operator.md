---
title: Designar um operador à prova de falhas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54ec71df8efab1f60bfb7a5b9af448705e349d28
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211421"
---
# <a name="designate-a-fail-safe-operator"></a>Designar um operador à prova de falhas
  Um operador à prova de falhas é um usuário que recebe o alerta caso o operador designado não possa ser localizado. Este tópico descreve como definir um operador à prova de falhas para receber [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] notificações de alerta do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]usando o.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para designar um operador à prova de falhas usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   As opções pager e **net send** serão removidas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Agent em uma versão futura [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente.  
  
-   Observe que o SQL Server Agent deve ser configurado para usar o Database Mail a fim de enviar notificações por pager ou email a operadores. Para obter mais informações, consulte [Atribuir alertas a um operador](assign-alerts-to-an-operator.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Somente membros da função de servidor fixa **sysadmin** podem designar operadores à prova de falhas.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-designate-a-fail-safe-operator"></a>Para designar um operador à prova de falhas  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor contém operador do SQL Server Agent que você deseja designar como à prova de falhas.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.  

3.  Na caixa de diálogo **Propriedades do SQL Server Agent –**_server_name_ , em **selecionar uma página**, selecione **sistema de alerta**.  
 
4.  Em **Operador à prova de falhas**, selecione **Habilitar operador à prova de falhas**.  
  
5.  Na lista **Operador** , selecione o operador que você deseja tornar à prova de falhas.  
  
6.  Marque qualquer uma ou todas as caixas de seleção a seguir para especificar como o operador será notificado: **Email**, **Pager**ou **Net send**.  
  
7.  Ao concluir, clique em **OK**.  
  
  
