---
title: Exibir o log de aplicativos do Windows (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- application logs [SQL Server]
- logs [SQL Server], application
- monitoring Windows NT application log [SQL Server]
- Windows NT application logs [SQL Server]
- displaying logs
- monitoring [SQL Server], events
- logs [SQL Server], viewing
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2e6e721948c2e875a5f9d6e100cdb29f928b4042
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85655270"
---
# <a name="view-the-windows-application-log-windows-10"></a>Exibir o log de aplicativos do Windows (Windows 10)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é configurado para usar o log de aplicativos do Windows, cada sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grava novos eventos nesse log. Ao contrário do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não é criado um novo log de aplicativos cada vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]é iniciada.  
  
## <a name="view-the-windows-application-log"></a>Para exibir o log de aplicativos do Windows  
  
1. Na **barra de Pesquisa**, digite **Visualizador de Eventos**, depois selecione o aplicativo da área de trabalho do **Visualizador de Eventos**.
  
2. No **Visualizador de Eventos**, abra **Logs de aplicativos e serviços**.

3. Os eventos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são identificados pela entrada **MSSQLSERVER** (as instâncias nomeadas são identificadas com **MSSQL$** _<instance_name>_ ) na coluna **Origem**. Os eventos do SQL Server Agent são identificados pela entrada SQLSERVERAGENT (no caso de instâncias nomeadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent são identificados com **SQLAgent$** \<*instance_name*>). Os eventos do serviço do Microsoft Search são identificados pela entrada **Microsoft Search**.  
  
4. Para exibir o log de um computador diferente, clique com o botão direito do mouse em **Visualizador de Eventos (local)** . Selecione **Conectar a outro computador** e preencha os campos para completar a caixa de diálogo **Selecionar Computador**.  
  
5. Opcionalmente, para exibir apenas eventos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no menu **Exibir**, selecione **Filtro**. Na lista **Origem do evento**, selecione **MSSQLSERVER**. Para exibir apenas eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, selecione **SQLSERVERAGENT** na lista **Origem do evento** .  
  
6. Para exibir mais informações sobre um evento, clique duas vezes no evento.  
  
## <a name="see-also"></a>Confira também  
 [Exibir o log de erros do SQL Server &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  
