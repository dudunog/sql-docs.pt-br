---
title: Propriedades do Analysis Server (guia Logon) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: a82e0c98-efaa-4b0b-9582-3c879ee42444
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 907840b051a4230a06525e8c3d6574aee4f40bcc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63035265"
---
# <a name="analysis-server-properties-log-on-tab"></a>Propriedades do Analysis Server (guia Fazer Logon)
  Use a guia **Fazer Logon** da caixa de diálogo **Propriedades do Analysis Server** para especificar a conta usada pelo serviço [!INCLUDE[ssAS](../../includes/ssas-md.md)] e para iniciar e parar o serviço.  
  
> [!NOTE]  
>  Quando ocorrer alteração no **Nome da Conta** usado por um serviço em uma instância clusterizada, a nova conta deverá ser membro do grupo de domínio especificado durante a instalação para o serviço que está sendo alterado, ou você deverá ter permissão para adicionar membros a esse grupo. Se você não tiver permissão para modificar a associação de grupo, contate o administrador de domínio.  
  
## <a name="options"></a>Opções  
 **Conta Sistema Local**  
 Especifique uma conta Sistema Local que não requeira uma senha. Porém, essa conta pode restringir a interação do serviço com outros servidores, dependendo dos privilégios concedidos a ela.  
  
 **Esta conta**  
 Especifique uma conta de usuário local ou de domínio que usa a Autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda usar uma conta de usuário do domínio com direitos mínimos para serviços. Para obter informações sobre como selecionar uma conta, pesquise o tópico "Configurando as contas de serviço do Windows" nos Manuais Online.  
  
 **Nome da Conta**  
 Especifique o nome da conta local ou de usuário de domínio.  
  
 **Senha**  
 Digite a senha da conta.  
  
 **Confirmar senha**  
 Digite a senha da conta novamente.  
  
 **Iniciar**  
 Inicie o serviço.  
  
 **Parar**  
 Parar o serviço.  
  
 **Pausar**  
 Pausar o serviço.  
  
 **Retomar**  
 Retomar um serviço pausado.  
  
  
