---
title: Alta disponibilidade no SQL Server Reporting Services | Microsoft Docs
description: Saiba mais sobre a melhor maneira de garantir a disponibilidade da funcionalidade do Reporting Services no SQL Server.
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7cac05af8a930b6926ca1b643a9eaef6d198e86a
ms.sourcegitcommit: 66a0672e47415dbd5cfd8d19075102c8c3973e70
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83766989"
---
# <a name="high-availability-in-sql-server-reporting-services"></a>Alta disponibilidade no SQL Server Reporting Services

Um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é um servidor sem monitoração de estado que armazena dados de aplicativo, conteúdo, propriedades e informações de sessão em dois bancos de dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Como tal, o melhor modo para assegurar a disponibilidade da funcionalidade do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é fazer o seguinte:  
  
-   Use os recursos de alta disponibilidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] para maximizar o tempo de atividade dos bancos de dados do servidor de relatório. Se uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] for configurada para ser executada em um cluster de failover, selecione essa instância ao criar um banco de dados do servidor de relatório.  
  
-   Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] com os bancos de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e para fontes de dados, como for possível. Para obter mais informações, consulte [Reporting Services com Grupos de Disponibilidade AlwaysOn](../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md).  
  
-   Configure vários servidores de relatório para serem executados em uma implantação de expansão, onde todos os servidores compartilham um único banco de dados do servidor de relatório. A implantação de várias instâncias do servidor de relatório, de preferência em servidores diferentes, em uma implantação de expansão pode ajudar a fornecer serviço ininterrupto caso uma das instâncias deixe de funcionar.  
  
 Uma implantação de expansão fornece um meio de compartilhar um banco de dados. Se um servidor de relatório deixar de funcionar, outros servidores na mesma implantação continuarão funcionando.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não dá suporte a cluster. A implantação de expansão propriamente dita não fornece balanceamento de carga; ela não detecta as cargas de processamento em um servidor de relatório e roteia as novas solicitações de processamento para o servidor menos ocupado. As solicitações de processamento que falharam antes da conclusão não são roteadas novamente. Para obter os recursos de balanceamento, configure o balanceamento de carga para os servidores da Web que hospedam os servidores de relatório e, em seguida, configure os servidores de relatório em uma implantação de expansão para que compartilhem o mesmo banco de dados de servidor de relatório.  
  
 O serviço Web e o serviço Windows do servidor de relatório são integrados e executados juntos como uma única instância do servidor de relatório. Você não pode configurar a disponibilidade separadamente para cada serviço.  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
