---
title: Propriedades do banco de dados (página Arquivos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.files.f1
ms.assetid: 3c030e51-db82-4b43-b1e5-8547ddd3de87
author: stevestein
ms.author: sstein
ms.openlocfilehash: 955a17857ce0d847fb712473dddd581a072ab83d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970166"
---
# <a name="database-properties-files-page"></a>Propriedades do Banco de Dados (página Arquivos)
  Use esta página para criar um novo banco de dados ou para exibir ou modificar as propriedades do banco de dados selecionado. Este tópico se aplica às **Propriedades do Banco de Dados (página Arquivos)** de bancos de dados existentes e ao **Novo Banco de Dados (página Geral)** .  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Nome do banco de dados**  
 Adicione ou exiba o nome do banco de dados.  
  
 **Proprietário**  
 Especifique o proprietário do banco de dados selecionando na lista.  
  
 **Usar indexação de texto completo**  
 Essa caixa de seleção fica marcada e desabilitada porque a indexação de texto completo está sempre habilitada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Pesquisa de texto completo](../search/full-text-search.md).  
  
 **Arquivos do banco de dados**  
 Adicione, exiba, modifique ou remova arquivos do banco de dados associado. Arquivos de banco de dados têm as seguintes propriedades:  
  
 **Nome Lógico**  
 Digite ou modifique o nome do arquivo.  
  
 **Tipo de arquivo**  
 Selecione o tipo de arquivo na lista. O tipo de arquivo pode ser **Dados**, **Log**ou **Dados de Filestream**. Você não pode modificar o tipo de arquivo de um arquivo existente.  
  
 Selecione **Dados do Fluxo de Arquivos** se estiver adicionando arquivos (contêineres) a um grupo de arquivos com otimização de memória.  
  
 Para adicionar arquivos (contêineres) a um grupo de arquivos de dados de Filestream, o FILESTREAM deve estar habilitado. Você pode habilitar o FILESTREAM usando a caixa de diálogo [Propriedades do Servidor (página Avançado)](../../database-engine/configure-windows/server-properties-advanced-page.md) .  
  
 **Grupo de arquivos**  
 Selecione o grupo de arquivos do arquivo na lista. Por padrão, o grupo de arquivos é PRIMARY. Você pode criar um novo grupo de arquivos selecionando **\<new filegroup>** e inserindo informações sobre o grupo de arquivos na caixa de diálogo **novo grupo de arquivos** . Um novo grupo de arquivos também pode ser criado na página **Grupo de Arquivos** . Você não pode modificar o grupo de arquivos de um arquivo existente.  
  
 Ao adicionar arquivos (contêineres) a um grupo de arquivos com otimização de memória, o campo de **Grupo de Arquivos** será preenchido com o nome do grupo de arquivos com otimização de memória do banco de dados.  
  
 **Tamanho Inicial**  
 Digite ou modifique o tamanho inicial do arquivo em megabytes. Por padrão, esse é o valor do banco de dados **modelo** .  
  
 Esse campo não é válido para arquivos de FILESTREAM.  
  
 Para arquivos em grupos de arquivos com otimização de memória, este campo não pode ser alterado.  
  
 **Aumento Automático**  
 Selecione ou exiba as propriedades de aumento automático do arquivo. Essas propriedades controlam como o arquivo se expande quando seu tamanho máximo é alcançado. Para editar valores de aumento automático, clique no botão de edição ao lado das propriedades de aumento automático do arquivo desejado e altere os valores na caixa de diálogo **Alterar Aumento Automático** . Por padrão, esses são os valores do banco de dados **modelo** .  
  
 Esse campo não é válido para arquivos de FILESTREAM.  
  
 Para arquivos em grupos de arquivos com otimização de memória, este campo deve ser **Ilimitado**.  
  
 **Caminho**  
 Exibe o caminho do arquivo selecionado. Para especificar um caminho para um novo arquivo, clique no botão de edição próximo ao caminho do arquivo e navegue até a pasta de destino. Você não pode modificar o caminho de um arquivo existente.  
  
 Para arquivos de FILESTREAM, o caminho é uma pasta. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] criará os arquivos subjacentes nesta pasta.  
  
 **Nome do Arquivo**  
 Exibe o nome do arquivo.  
  
 Este campo não é válido para arquivos de FILESTREAM, incluindo arquivos em grupos de arquivos com otimização de memória.  
  
 **Adicionar**  
 Adicione um novo arquivo ao banco de dados.  
  
 **Remover**  
 Exclua o arquivo selecionado do banco de dados. Um arquivo não pode ser removido, a menos que esteja vazio. O arquivo de dados principal e o arquivo de log não podem ser removidos.  
  
 Para obter informações sobre arquivos, consulte [Database Files and Filegroups](database-files-and-filegroups.md).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
