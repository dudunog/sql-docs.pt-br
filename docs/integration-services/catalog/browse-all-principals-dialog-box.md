---
description: Caixa de diálogo Procurar Todas as Entidades de Segurança
title: Caixa de diálogo Procurar Todas as Entidades de Segurança | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f5ec280020b966a1d23b5ebb9dfb2c740692a6d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88394962"
---
# <a name="browse-all-principals-dialog-box"></a>Caixa de diálogo Procurar Todas as Entidades de Segurança

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a caixa de diálogo **Procurar Todas as Entidades de Segurança** para selecionar uma entidade de segurança de banco de dados para alterar as permissões da entidade de segurança no projeto selecionado ou em todos os projetos contidos em uma pasta selecionada.  
  
 **O que você deseja fazer?**  
  
-   [Caixa de diálogo Abrir Todas as Entidades de Segurança](#open_dialog)  
  
-   [Configurar as opções](#options)  
  
##  <a name="open-the-browse-all-principals-dialog-box"></a><a name="open_dialog"></a> Caixa de diálogo Abrir Todas as Entidades de Segurança  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o catálogo SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Para alteraras permissões da entidade de segurança em todos os projetos contidos em uma pasta selecionada, clique com o botão direito do mouse na pasta e clique em **Propriedades**.  
  
     Para alteraras permissões da entidade de segurança em um projeto selecionado, expanda a pasta que contém o projeto, clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
5.  Selecione a página **Permissões** e clique em **Procurar**.  
  
##  <a name="configure-the-options"></a><a name="options"></a> Configurar as opções  
 Esta página exibe as entidades de segurança da exibição do catálogo, sys.database_principals, do banco de dados do SSISDB.  
  
 Ao serem selecionadas, as entidades de segurança serão adicionadas à lista **Logons ou funções** na página **Permissões** da caixa de diálogo pai quando você clicar em **OK** e fechar a caixa de diálogo **Procurar Todas as Entidades de Segurança** . Depois de adicionar entidades de segurança à lista **Logons ou funções** , você poderá alterar as permissões no projeto selecionado.  
  
 **Seleção de coluna**  
 Selecione para adicionar a entidade de segurança à lista **Logons ou funções** na página **Permissões** da caixa de diálogo pai.  
  
 **Coluna de ícone**  
 Um ícone que corresponde ao **Tipo** da entidade de segurança.  
  
 **Nome**  
 O nome da entidade de segurança.  
  
 **Tipo**  
 O tipo da entidade de segurança. Os tipos comuns são:  
  
-   Usuário do SQL  
  
-   Usuário do Windows  
  
-   Função de banco de dados  
  
  
