---
title: Habilitar a opção Bloquear Páginas na Memória (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0f6e938e3212e519ab51be1faf3f18e28957ef3e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62782274"
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>Habilitar a opção Bloquear Páginas na Memória (Windows)
  Essa política do Windows determina quais contas podem usar um processo para manter dados na memória física, impedindo o sistema de paginar os dados para a memória virtual em disco.  
  
> [!NOTE]  
>  O bloqueio de páginas na memória pode aumentar o desempenho quando se espera paginar a memória em disco.  
  
 Use a ferramenta Política de Grupo do Windows (gpedit.msc) para habilitar essa política para a conta usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você deve ser um administrador do sistema para alterar essa política.  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>Para habilitar a opção de bloqueio de páginas na memória  
  
1.  No menu **Iniciar** , clique em **Executar**. Na caixa **abrir** , digite `gpedit.msc`.  
  
2.  No console **Editor de Política de Grupo Local** , expanda **Configuração do Computador**e depois expanda **Configurações do Windows**.  
  
3.  Expanda **Configurações de Segurança**e então expanda **Políticas Locais**.  
  
4.  Selecione a pasta **Atribuição de direitos de usuários** .  
  
     As políticas serão exibidas no painel de detalhes.  
  
5.  No painel, clique duas vezes em **Bloquear páginas na memória**.  
  
6.  Na caixa de diálogo **Configuração de Segurança Local – Bloquear páginas na memória**, clique em **Adicionar Usuário ou Grupo**.  
  
7.  Na caixa de diálogo **Selecionar Usuários, Contas de Serviço ou Grupos** , adicione uma conta com privilégios para executar sqlservr.exe.  
  
8.  Faça logoff e depois faça logon para que essas alterações entrem em vigor.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções Server Memory de configuração do servidor](server-memory-server-configuration-options.md)  
  
  
