---
title: Tarefa de limpeza de manutenção (plano de manutenção) | Microsoft Docs
description: Saiba como remover arquivos antigos para planos de manutenção, inclusive relatórios de texto criados por planos de manutenção e arquivos de backup de banco de dados, usando a Tarefa de Limpeza de Manutenção.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.cleanup.f1
helpviewer_keywords:
- Maintenance Cleanup Task dialog box
ms.assetid: 022b679c-6799-4c13-9185-814224a20412
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b7e01cbee4a518b7b2f6b9ef9dea783f1a6ce24d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85666962"
---
# <a name="maintenance-cleanup-task-maintenance-plan"></a>Tarefa de limpeza de manutenção (plano de manutenção)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use a **Tarefa de Limpeza de Manutenção** para remover arquivos antigos relacionados a planos de manutenção, inclusive relatórios de texto criados por planos de manutenção e arquivos de backup de banco de dados.  
  
> [!NOTE]  
>  A tarefa Limpeza de Manutenção não exclui automaticamente os arquivos nas subpastas do diretório especificado. Esse recurso reduz a possibilidade de um ataque mal-intencionado que use a tarefa de Limpeza de Manutenção para excluir arquivos. Se quiser excluir arquivos em subpastas de primeiro nível, você deverá selecionar **Incluir subpastas de primeiro nível**.  
  
## <a name="options"></a>Opções  
 **Conexão**  
 Exibe a conexão atual.  
  
 **Novo**  
 Crie uma nova conexão com o servidor para usar ao executar esta tarefa. A caixa de diálogo **Nova Conexão** é descrita abaixo.  
  
 **Arquivos de backup**  
 Exclua arquivos de backup.  
  
 **Relatórios de texto do Plano de Manutenção**  
 Exclua relatórios de texto de planos de manutenção executados anteriormente.  
  
 **Excluir arquivo específico**  
 Exclua o arquivo específico fornecido na caixa **Nome do arquivo** .  
  
 **Nome do arquivo**  
 Caminho e nome do arquivo a ser excluído.  
  
 **Pesquisar pasta e excluir arquivos com base em uma extensão**  
 Exclua todos os arquivos com a extensão especificada na pasta especificada. Use para excluir vários arquivos de uma vez, tais como todos os arquivos de backup com a extensão .bak, na pasta Terça-feira.  
  
 **Pasta**  
 Caminho e nome da pasta que contém os arquivos a serem excluídos.  
  
 **Extensão de arquivo**  
 Forneça a extensão dos arquivos a ser excluídos. Não inclua nenhum outro caractere antes ou depois da extensão (por exemplo, use BAK ou TRN). 
  
 **Incluir subpastas de primeiro nível**  
 Exclua arquivos com a extensão especificada para **Extensão de arquivo** de subpastas de primeiro-nível em **Pasta**.  
  
 **Excluir arquivos com base na idade do arquivo em tempo de execução da tarefa**  
 Especifique a idade mínima dos arquivos que você deseja excluir fornecendo um número e unidade de tempo na caixa **Excluir arquivos com idade acima de** .  
  
 **Excluir arquivos com idade acima de**  
 Especifique a idade mínima dos arquivos que você deseja excluir, fornecendo um número e unidade de tempo (Dia, Semana, Mês ou Ano). Arquivos com idade acima do período especificado serão excluídos.  
  
 **Exibir T-SQL**  
 Exiba as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas no servidor para esta tarefa, com base nas opções selecionadas.  
  
> [!NOTE]  
>  Quando o número de objetos afetados é grande, essa exibição pode ser demorada.  
  
## <a name="new-connection-dialog-box"></a>Caixa de diálogo Nova Conexão  
 **Nome da conexão**  
 Digite um nome para a nova conexão.  
  
 **Selecione ou digite um nome de servidor**  
 Selecione um servidor com o qual se conectar ao executar esta tarefa.  
  
 **...**  
 Selecione para exibir a lista de servidores disponíveis.  
  
 **Digite as informações para fazer logon no servidor**  
 Especifica como autenticar no servidor.  
  
 **Use a segurança integrada do Windows**  
 Conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com a Autenticação do Microsoft Windows.  
  
 **Usar nome de usuário e senha específicos**  
 Conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usando a Autenticação do SQL Server. Essa opção não está disponível.  
  
 **Nome de usuário**  
 Forneça um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado na autenticação. Essa opção não está disponível.  
  
 **Senha**  
 Forneça uma senha a ser usada na autenticação. Essa opção não está disponível.  
  
## <a name="see-also"></a>Consulte Também  
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
