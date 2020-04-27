---
title: Propriedades do SQL Server Agent (página Sistema de Trabalho) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8dceeba78e639ecbe2fd81fbdb1021293e75cf8a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63246080"
---
# <a name="sql-server-agent-properties-job-system-page"></a>Propriedades do SQL Server Agent (página Sistema de Trabalho)
  Use esta página para exibir e modificar como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço Agent gerencia trabalhos.  
  
## <a name="options"></a>Opções  
 **Intervalo de tempo limite de desligamento (em segundos)**  
 Especifica o número de segundos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent espera os trabalhos serem concluídos antes de desligar. Se o trabalho ainda estiver em execução depois do intervalo especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para o trabalho à força.  
  
 **Usar uma conta proxy não administrador**  
 Define uma conta proxy não administrador para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores dão suporte a vários proxies, portanto, essa opção só [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é aplicável ao gerenciar [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]versões do Agent anteriores ao.  
  
 **Nome de usuário**  
 Digite o nome do usuário para a conta proxy não administrador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 **Senha**  
 Digite a senha do usuário para a conta proxy não administrador. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e as versões posteriores dão suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 **Controlador**  
 Digite o domínio do usuário para a conta proxy não administrador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar trabalhos](implement-jobs.md)  
  
  
