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
ms.openlocfilehash: 66b066ac017cb999342bd9bee7dd605a841ee421
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596595"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>Desenvolvimento de banco de dados orientado a projetos usando ferramentas de linha de comando

O SQL Server Data Tools prova ferramentas de linha de comando que permitem vários cenários de desenvolvimento orientados a projeto.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage/sqlpackage.md)|Este tópico descreve o utilitário SQLPackage.exe, usado para as seguintes tarefas:<br /><br />-   Extrair um arquivo .dacpac de um banco de dados dinâmico do SQL Server.<br />-   Publicar um arquivo .dacpac em um banco de dados dinâmico do SQL Server para atualizar incrementalmente o esquema do banco de dados dinâmico para que corresponda ao .dacpac.<br />-   Comparar um arquivo .dacpac com um banco de dados dinâmico do SQL Server e gerar um script Transact\-SQL de atualização incremental sem atualizar o banco de dados dinâmico.<br />-   Comparar dois arquivos .dacpac para gerar um script Transact\-SQL de atualização incremental.<br />-   Gerar um relatório XML que resume as alterações da atualização incremental que ocorreriam se o banco de dados fosse atualizado incrementalmente.|  
|[Usar o MSDeploy com o provedor do dbSqlPackage](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|Este tópico descreve o provedor da [Ferramenta de Implantação da Web](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd568996(v=ws.10)), denominado dbSqlPackage, incluído no SSDT, que funciona com a Ferramenta de Desenvolvimento da Web da Microsoft (MSDeploy.exe) do IIS (Serviços de Informações da Internet), usada para as seguintes tarefas:<br /><br />–   Extrair um arquivo .dacpac de um banco de dados remoto/local do SQL Server ou do Banco de Dados SQL do Azure.<br />–   Publicar um .dacpac em um banco de dados remoto/local do SQL Server ou do Banco de Dados SQL do Azure para atualizá-lo incrementalmente.<br />–   Publicar a partir de um banco de dados local do SQL Server em um banco de dados remoto do SQL Server ou do Banco de Dados SQL do Azure para atualizá-lo incrementalmente.<br />–   Comparar um .dacpac com um banco de dados remoto/local do SQL Server ou do Banco de Dados SQL do Azure para gerar um script do Transact\-SQL de atualização incremental sem atualizar o banco de dados dinâmico.<br />-   Gerar um relatório XML que resume as alterações da atualização incremental que ocorreriam se o banco de dados fosse atualizado incrementalmente.|  
  
## <a name="related-sections"></a>Seções relacionadas  
[Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md)  
