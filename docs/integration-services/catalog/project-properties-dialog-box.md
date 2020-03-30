---
title: Caixa de diálogo Propriedades do Projeto | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isprojectprop.general.f1
- sql13.ssis.ssms.isprojectprop.permissions.f1
ms.assetid: d5cf52f5-1fe2-438a-98a3-fe117360acf8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f9aee0d7233b5f163a5f9c39f9053b9f0842aa7e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298950"
---
# <a name="project-properties-dialog-box"></a>Caixa de diálogo Propriedades do Projeto

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é uma unidade de implantação. Cada projeto pode conter pacotes, parâmetros e referências de ambiente. Um projeto é um objeto protegível e pode definir permissões para principais de banco de dados. Quando um projeto é reimplantado, a versão anterior dele pode ser armazenada no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Os parâmetros de projeto e de pacote podem ser usados para atribuir valores às propriedades nos pacotes em tempo de execução. Alguns parâmetros exigem valores antes da execução do pacote. Valores de parâmetros que referenciam variáveis de ambiente requerem que o projeto tenha a referência de ambiente correspondente antes da execução.  
  
 **O que você deseja fazer?**  
  
-   [Abra a caixa de diálogo Propriedades do Projeto](#open_dialog)  
  
-   [Definir as opções na página Geral](#general)  
  
-   [Defina as opções na página Permissões](#permissions)  
  
##  <a name="open-the-project-properties-dialog-box"></a><a name="open_dialog"></a> Abra a caixa de diálogo Propriedades do Projeto  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o projeto para o qual você deseja definir propriedades.  
  
5.  Clique com o botão direito do mouse no projeto e, em seguida, clique em **Propriedades**.  
  
##  <a name="set-the-options-on-the-general-page"></a><a name="general"></a> Definir as opções na página Geral  
 Use a página Geral para exibir as propriedades do projeto.  
  
 **Nome**  
 Lista o nome do projeto.  
  
 **Identificador**  
 Lista a ID do projeto.  
  
 **Descrição**  
 Exibe a descrição opcional do projeto.  
  
 **Versão do projeto**  
 Lista a versão do projeto.  
  
 **Data de implantação**  
 Lista a data e a hora em que o projeto foi implantado ou reimplantado.  
  
##  <a name="set-the-options-on-the-permissions-page"></a><a name="permissions"></a> Defina as opções na página Permissões  
 Use a página **Permissões** para exibir e definir as permissões explícitas para o projeto.  
  
 Procurar  
 Clique em **Procurar** para selecionar usuários e funções para os quais você quer definir permissões, usando a caixa de diálogo **Procurar Todas as Entidades de Segurança** .  
  
 **Nome**  
 Lista o nome do usuário ou função.  
  
 **Tipo**  
 Lista o tipo de usuário ou função.  
  
 **Permissão**  
 Lista as permissões.  
  
 **Concessor**  
 Lista o usuário ou função que concede a permissão.  
  
 **Conceder**  
 Quando **Conceder** está selecionado, a permissão é concedida para o usuário ou função selecionado.  
  
 **Deny**  
 Quando **Negar** está selecionado, a permissão é negada para o usuário ou função selecionado.  
  
  
