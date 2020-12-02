---
description: Caixa de diálogo Validar
title: Caixa de diálogo Validar | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isprojectvalidate.f1
- sql13.ssis.ssms.ispackagevalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a65f5d8114907472eb03aa06e428927aa1408b7b
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88484899"
---
# <a name="validate-dialog-box"></a>Caixa de diálogo Validar

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a caixa de diálogo **Validar** para verificar os problemas comuns de um projeto ou pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Se houver um problema, uma mensagem será exibida na parte superior da caixa de diálogo. Caso contrário, o termo Ready aparecerá na parte superior.  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Validar](#open_dialog)  
  
-   [Definir as opções na página Geral](#general)  
  
##  <a name="open-the-validate-dialog-box"></a><a name="open_dialog"></a> Abrir a caixa de diálogo Validar  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o projeto ou pacote que você deseja validar.  
  
5.  Clique com o botão direito do mouse no projeto ou pacote e clique em **Validar**.  
  
##  <a name="set-the-options-on-the-general-page"></a><a name="general"></a> Definir as opções na página Geral  
 **Ambiente**  
 Selecione o ambiente que você deseja usar para validar o projeto ou pacote.  
  
 **runtime de 32 bits**  
 Opte por usar um runtime de 32 bits para executar um pacote.  
  
 A guia **Parâmetros** lista os valores de parâmetros usados para validar o projeto ou pacote. As opções a seguir constam na guia Parâmetros.  
  
 **Contêiner**  
 Lista o objeto que contém o parâmetro.  
  
 **Parâmetro**  
 Lista o nome dos parâmetros  
  
 **Valor**  
 Lista o valor do parâmetro.  
  
 A guia **Gerenciadores de Conexões** lista os valores de propriedade dos gerenciadores de conexões usados para validar o projeto ou pacote.  
  
 As opções a seguir constam na guia **Gerenciadores de Conexões** .  
  
 **Contêiner**  
 Lista o objeto que contém o gerenciador de conexões.  
  
 **Nome**  
 Lista o nome do gerenciador de conexões.  
  
 **Nome da propriedade**  
 Lista o nome da propriedade do gerenciador de conexões.  
  
 **Valor**  
 Lista o valor atribuído à propriedade do gerenciador de conexões.  
  
  
