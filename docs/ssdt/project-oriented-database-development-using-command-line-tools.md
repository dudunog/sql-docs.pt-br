---
title: Desenvolvimento de banco de dados orientado a projetos usando ferramentas de linha de comando
description: Veja os recursos disponíveis nas ferramentas de linha de comando que o SQL Server Data Tools fornece para trabalhar com arquivos .dacpac, como o SqlPackage.exe e o dbSqlPackage.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9a26def9-8fbd-43e4-9e57-414840b73ed8
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 04/26/2017
ms.openlocfilehash: dd2f9464bb9369337cd8ef4687e48d05fb0aa664
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246439"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>Desenvolvimento de banco de dados orientado a projetos usando ferramentas de linha de comando

O SQL Server Data Tools prova ferramentas de linha de comando que permitem vários cenários de desenvolvimento orientados a projeto.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage.md)|Este tópico descreve o utilitário SQLPackage.exe, usado para as seguintes tarefas:<br /><br />-   Extrair um arquivo .dacpac de um banco de dados dinâmico do SQL Server.<br />-   Publicar um arquivo .dacpac em um banco de dados dinâmico do SQL Server para atualizar incrementalmente o esquema do banco de dados dinâmico para que corresponda ao .dacpac.<br />-   Comparar um arquivo .dacpac com um banco de dados dinâmico do SQL Server e gerar um script Transact\-SQL de atualização incremental sem atualizar o banco de dados dinâmico.<br />-   Comparar dois arquivos .dacpac para gerar um script Transact\-SQL de atualização incremental.<br />-   Gerar um relatório XML que resume as alterações da atualização incremental que ocorreriam se o banco de dados fosse atualizado incrementalmente.|  
|[Usar o MSDeploy com o provedor do dbSqlPackage](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|Este tópico descreve o provedor da [Ferramenta de Implantação da Web](https://go.microsoft.com/fwlink/?LinkId=231798), denominado dbSqlPackage, incluído no SSDT, que funciona com a Ferramenta de Desenvolvimento da Web da Microsoft (MSDeploy.exe) do IIS (Serviços de Informações da Internet), usada para as seguintes tarefas:<br /><br />-   Extrair um arquivo .dacpac de um banco de dados remoto/local do SQL Server ou do SQL Azure.<br />-   Publicar um .dacpac em um banco de dados remoto/local do SQL Server ou do SQL Azure para atualizá-lo incrementalmente.<br />-   Publicar a partir de um banco de dados local do SQL Server em um banco de dados remoto do SQL Server ou do SQL Azure para atualizar o banco de dados remoto incrementalmente.<br />-   Comparar um .dacpac com um banco de dados remoto/local do SQL Server ou do SQL Azure para gerar um script Transact\-SQL de atualização incremental sem atualizar o banco de dados dinâmico.<br />-   Gerar um relatório XML que resume as alterações da atualização incremental que ocorreriam se o banco de dados fosse atualizado incrementalmente.|  
  
## <a name="related-sections"></a>Seções relacionadas  
[Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md)  
  
