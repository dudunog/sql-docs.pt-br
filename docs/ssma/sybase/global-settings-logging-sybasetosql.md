---
description: Configurações globais (registro em log) (SybaseToSQL)
title: Configurações globais (log) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4cb4da20-3b99-4aae-8c80-329ee23e796e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: bc71ae0d44048d656bfba1a81ba19b9cb0ee0269
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492259"
---
# <a name="global-settings-logging-sybasetosql"></a>Configurações globais (registro em log) (SybaseToSQL)
Use a caixa de diálogo **configurações globais** para especificar as configurações de log para o SSMA. Normalmente, você alteraria essas configurações apenas ao trabalhar com o suporte ao produto.  
  
Para acessar essa caixa de diálogo, no menu **ferramentas** , selecione **configurações globais** e, em seguida, clique no botão **log** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Nível de mensagens**  
As seguintes opções estão disponíveis no **nível de mensagens**:  
  
|Opção|Descrição|  
|----------|---------------|  
|**[todas as categorias]**|Usado para definir o nível de log para todas as opções a seguir.|  
|**Coletor**|Coleta metadados sobre o esquema de origem e salva-os no projeto.|  
|**Conversor**|Converte estruturas de objetos de banco de dados de origem, como tabelas e procedimentos armazenados, em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estruturas correspondentes.|  
|**Data Migrator**|Migra dados do banco de dado de origem para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**Formatador**|Subcomponente do conversor que gera scripts para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema.|  
|**Interface gráfica do usuário**|Mensagens que aparecem quando você usa a ferramenta SSMA.|  
|**Vinculador**|Resolve os identificadores do SQL e fornece informações para outros componentes.|  
|**Outras**|Todas as mensagens que não estão em nenhuma outra categoria.|  
|**Analisador**|Analisa o esquema de origem.|  
|**Sincronizador**|Carrega objetos de banco de dados de origem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**Árvoreconverter**|Converte objetos nos metadados de origem em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados.|  
  
Para cada opção sob o **nível de mensagens**, configure um dos seguintes níveis de log para o SSMA:  
  
|||  
|-|-|  
|**Erro fatal**|Grave somente mensagens de erro fatal no log.|  
|**Erro**|Grave mensagens de erro e erro fatal no log.|  
|**Aviso**|Gravar mensagens de erro fatal, de erro e de aviso no log.|  
|**Informações**|Grave mensagens informativas, de aviso, de erro e de erro fatal no log.|  
|**Depurar**|Grave todas as mensagens, incluindo as mensagens de depuração, no log.|  
  
**Caminho do arquivo de log**  
O caminho do arquivo e o nome dos arquivos de log do SSMA. Para especificar um nome diferente, clique no caminho atual e, em seguida, clique no botão procurar (**...**).  
  
**Tamanho do arquivo de log**  
O tamanho máximo do arquivo de log em KB. O tamanho mínimo é 10 KB. O tamanho padrão é 10240 KB.  
  
**Número total de arquivos de log**  
Quando um log for preenchido, o SSMA renomeará o arquivo de log e iniciará um novo. Usando essa configuração, especifique o número máximo de arquivos de log a serem mantidos. O mínimo é 2.  
  
