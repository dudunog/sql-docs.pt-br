---
title: Configurar notificações por email (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- e-mail [Master Data Services], configuring
- notifications [Master Data Services], configuring notifications
ms.assetid: 4241a6ab-7465-471b-9890-57c6b572037e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d0c76727e9d1550183a8697c2833ded0510c5624
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971936"
---
# <a name="configure-email-notifications-master-data-services"></a>Configurar notificações por email (Master Data Services)
  Configure emails de notificação quando desejar que o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] envie mensagens de email automaticamente.  
  
### <a name="to-configure-notifications"></a>Para configurar notificações  
  
1.  No [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], na página **Banco de Dados** , selecione seu banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Na seção **Configurações do Sistema** , clique em **Criar Perfil**.  
  
3.  Preencha todos os campos obrigatórios. Para obter mais informações, consulte [Caixa de diálogo Criar Perfil e Conta do Database Mail &#40;Gerenciador de Configuração do Master Data Services&#41;](../../2014/master-data-services/create-database-mail-profile-and-account-dialog-box.md).  
  
4.  Clique em **OK**.  
  
    > [!NOTE]  
    >  Depois de configurar notificações, você não poderá usar o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para fazer alterações. Você deve fazer alterações diretamente no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações, consulte [Database Mail Configuration Objects](../relational-databases/database-mail/database-mail-configuration-objects.md).  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Existem configurações no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que afetam as notificações. Essas configurações podem ser ajustadas no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ou diretamente na tabela de Configurações do Sistema do banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Master Data Services de notificações &#40;&#41;](../../2014/master-data-services/notifications-master-data-services.md)   
 [Solucionando problemas de notificações por email (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)   
 [Configurar regras de negócio para enviar notificações &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
