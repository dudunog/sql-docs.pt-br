---
description: MSSQLSERVER_7936
title: MSSQLSERVER_7936 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7936 (Database Engine error)
ms.assetid: d78fc8a9-d173-4801-bb32-ed6a29257f08
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f7077b7947a7aaa5e856f8e47d0b2de468f77540
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88331643"
---
# <a name="mssqlserver_7936"></a>MSSQLSERVER_7936
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|7936|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_FS_ORPHANED_COLUMN_DIRECTORY|  
|Texto da mensagem|Erro de tabela: existe um diretório de Fluxo de arquivos para a ID de coluna C_ID da ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, mas essa coluna não é de Filestream.|  
  
## <a name="explanation"></a>Explicação  
Durante o DBCC CHECKDB, um diretório FILESTREAM foi encontrado para a coluna especificada, no entanto, essa não é uma coluna **FILESTREAM**.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
Não aplicável. Não é possível corrigir esse erro automaticamente. Se você não conseguir restaurar o banco de dados com base em um backup, contate o CSS (Suporte e Atendimento ao Cliente) [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
