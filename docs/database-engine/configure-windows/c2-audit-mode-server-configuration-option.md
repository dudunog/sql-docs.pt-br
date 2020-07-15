---
title: Opção de configuração de servidor c2 audit mode | Microsoft Docs
description: Familiarize-se com o modo de auditoria C2, uma opção de configuração do SQL Server que pode ajudá-lo a analisar a atividade do sistema e acompanhar possíveis violações da política de segurança.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], C2 Audit Mode option
- C2 auditing
- C2 Audit Mode option
- recording attempts
ms.assetid: 5a8d73a6-c4f6-4967-ba11-ecbcfc90b9cc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d92dcad571574310c1b64a9992a54b166fe8ad8e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759199"
---
# <a name="c2-audit-mode-server-configuration-option"></a>Opção c2 audit mode de configuração de servidor
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O modo de auditoria C2 pode ser configurado pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou com a opção **modo de auditoria c2** no **sp_configure**. Selecionar esta opção configurará o servidor para registrar tentativas com falha e com êxito ao acessar instruções e objetos. Essas informações podem ajudá-lo a determinar o perfil da atividade do sistema e rastrear possíveis violações na política de segurança.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] O padrão de segurança C2 foi substituído pela Certificação de Critérios Comuns. Consulte [Opção de configuração de servidor com conformidade de critérios comuns habilitada](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md).  
  
## <a name="audit-log-file"></a>Arquivo de auditoria de log  
 Os dados do modo de auditoria C2 são salvados no diretório de dados padrão da instância. Se o arquivo de log de auditoria atingir seu limite de tamanho de 200 MB, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criará um novo arquivo, fechará o arquivo antigo e gravará todos os novos registros de auditoria no novo arquivo. Esse processo continuará até que o diretório de dados de auditoria atinja seu limite ou a auditoria seja desativada. Para determinar o estado de um rastreamento de C2, consulte a exibição do catálogo sys.traces.  
  
> [!IMPORTANT]  
>  O modo de auditoria C2 salva uma grande quantidade de informações de eventos no arquivo de log, que pode aumentar rapidamente. Se o diretório de dados no qual os logs estão sendo salvos atingir seu limite de espaço, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será encerrado. Se a auditoria for definida para iniciar automaticamente, você deverá reiniciar a instância com o sinalizador **-f** (que passa pela auditoria) ou liberar espaço em disco adicional para o log de auditoria.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ativa o modo de auditoria C2.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
sp_configure 'c2 audit mode', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
