---
title: Gerenciar o controle de alterações (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- tracking data changes [SQL Server]
- change tracking [SQL Server], overhead
- change tracking [SQL Server]
- change tracking [SQL Server], managing
ms.assetid: 94a8d361-e897-4d6d-9a8f-1bb652e7a850
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c9d0deb3567daa64afb46c96a4e93c9da9c0972a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62670837"
---
# <a name="manage-change-tracking-sql-server"></a>Gerenciar o controle de alterações (SQL Server)
  Este tópico descreve como gerenciar o controle de alterações. Ele também descreve como configurar a segurança e determinar os efeitos sobre o armazenamento e o desempenho quando você usa o controle de alterações.  
  
## <a name="managing-change-tracking"></a>Gerenciando o controle de alterações  
 As próximas seções listam exibições de catálogo, permissões e configurações relevantes para o gerenciamento do controle de alterações.  
  
### <a name="catalog-views"></a>Exibições do catálogo  
 Para determinar quais as tabelas e bancos de dados que possuem o controle de alterações habilitado, você pode usar as seguintes exibições do catálogo:  
  
-   [sys.change_tracking_databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases)  
  
-   [sys.change_tracking_tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables)  
  
 Além disso, a exibição de catálogo [sys.internal_tables](/sql/relational-databases/system-catalog-views/sys-internal-tables-transact-sql) lista as tabelas internas criadas quando o controle de alterações está habilitado para um usuário da tabela.  
  
### <a name="security"></a>Segurança  
 Para acessar informações do controle de alterações usando as [funções de controle de alterações](/sql/relational-databases/system-functions/change-tracking-functions-transact-sql), o principal deve ter as seguintes permissões:  
  
-   Permissão SELECT em pelo menos as colunas de chave primária, em uma tabela com alterações controladas da tabela que está sendo consultada.  
  
-   Permissão VIEW CHANGE TRACKING na tabela na qual estão sendo obtidas as alterações. A permissão VIEW CHANGE TRACKING é necessária pelas seguintes razões:  
  
    -   Os registros do controle de alterações incluem informações sobre linhas excluídas, especificamente os valores de chave primária das linhas que foram excluídas. Um principal poderia ter recebido a permissão SELECT em uma tabela com controle de alterações após a exclusão de alguns dados confidenciais. Nesse caso, não convém que o principal tenha acesso às informações excluídas usando o controle de alterações.  
  
    -   As informações do controle de alterações podem armazenar informações sobre as colunas que foram alteradas por operações de atualização. Um principal poderia ter negada a permissão de acesso a uma coluna que contém informações confidenciais. Porém, como as informações de controle de alterações estão disponíveis, um principal pode determinar que um valor de coluna foi atualizado, mas não pode determinar o valor da coluna.  
  
## <a name="understanding-change-tracking-overhead"></a>Noções básicas de sobrecarga do controle de alterações  
 Quando o controle de alterações estiver habilitado em uma tabela, algumas operações de administração são afetadas. A tabela a seguir lista as operações e os efeitos que você deve considerar:  
  
|Operação|Quando o controle de alterações está habilitado|  
|---------------|-------------------------------------|  
|DROP TABLE|Todas as informações do controle de alterações da tabela descartada são removidas.|  
|ALTER TABLE DROP CONSTRAINT|Uma tentativa para cancelar a restrição PRIMARY KEY falhará. O controle de alterações deve ser desabilitado antes de uma restrição PRIMARY KEY ser cancelada.|  
|ALTER TABLE DROP COLUMN|Se a coluna que está sendo cancelada é parte de uma chave primária, não é permitido cancelar a coluna, independentemente do controle de alterações.<br /><br /> Se a coluna que está sendo cancelada não é parte de uma chave primária, cancelar a coluna terá êxito. Entretanto, o efeito em qualquer aplicativo que estiver sincronizando esses dados deve ser compreendido antes. Se o controle de alterações de coluna estiver habilitado na tabela, a coluna cancelada poderá retornar como parte das informações do controle de alterações. É responsabilidade do aplicativo controlar a coluna cancelada.|  
|ALTER TABLE ADD COLUMN|Se uma nova coluna for adicionada à tabela com controle de alterações, a inclusão da coluna não será controlada. Somente as atualizações e alterações feitas na nova coluna serão controladas.|  
|ALTER TABLE ALTER COLUMN|Alterações de tipos de dados de colunas de chave primária não são controladas.|  
|ALTER TABLE SWITCH|Trocar uma partição falhará se uma ou ambas as tabelas tiverem o controle de alterações habilitado.|  
|DROP INDEX ou ALTER INDEX DISABLE|O índice que aplica a chave primária não pode ser cancelado ou desabilitado.|  
|TRUNCATE TABLE|Truncando uma tabela pode ser executada em uma tabela que tenha o controle de alterações habilitado. No entanto, não são controladas as linhas que foram excluídas pela operação e a versão mínima válida é atualizada. Quando o aplicativo controla sua versão, o controle verifica se a versão é muito antiga e é necessário fazer uma atualização. Isso é o mesmo que desabilitar o controle de alterações da tabela e, depois, habilitá-lo novamente.|  
  
 O uso do controle de alterações adiciona uma certa sobrecarga às operações DML devido às informações de controle que são armazenadas como parte do procedimento.  
  
### <a name="effects-on-dml"></a>Efeitos na DML  
 O controle de alterações foi otimizado para minimizar a sobrecarga de desempenho nas operações DML. A sobrecarga de desempenho incremental associada com o uso do controle de alterações em uma tabela é semelhante à sobrecarga incorrida quando um índice é criado para uma tabela e precisa ser mantido  
  
 Para cada linha alterada por uma operação DML, uma linha é adicionada à tabela interna de controle de alterações. O efeito dessa relação com a operação DML depende de vários fatores, como os seguintes:  
  
-   O número de colunas de chave primária  
  
-   A quantidade de dados que estão sendo alterados na linha da tabela do usuário  
  
-   O número de operações executadas em uma transação  
  
 O isolamento do instantâneo, se utilizado, também afeta o desempenho de todas as operações DML, quer o controle de alterações esteja habilitado ou não.  
  
### <a name="effects-on-storage"></a>Efeitos no armazenamento  
 Os dados do controle de alterações são armazenados nos seguintes tipos de tabelas internas:  
  
-   Tabela de alteração interna  
  
     Há uma tabela de alteração interna para cada tabela de usuário para a qual o controle de alterações está habilitado.  
  
-   Tabela de transação interna  
  
     Há uma tabela de transação interna para o banco de dados.  
  
 Essas tabelas internas afetam os requisitos de armazenamento das seguintes maneiras:  
  
-   Para cada alteração, em cada linha na tabela do usuário, uma linha é adicionada à tabela de alteração interna. Essa linha tem uma pequena sobrecarga fixa, mais uma sobrecarga variável igual ao tamanho das colunas de chave primária. A linha pode conter informações de contexto opcionais definidas por um aplicativo. E, se o controle de alterações de coluna estiver habilitado, cada coluna alterada necessitará de 4 bytes na tabela de controle.  
  
-   Para cada transação confirmada, uma linha é adicionada a uma tabela de transação interna.  
  
 Assim como ocorre em outras tabelas internas, você pode determinar o espaço usado para as tabelas de controle de alterações usando o procedimento armazenado [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) . Os nomes das tabelas internas podem ser obtidos usando a exibição de catálogo [sys.internal_tables](/sql/relational-databases/system-catalog-views/sys-internal-tables-transact-sql) , conforme mostrado no exemplo a seguir.  
  
```sql  
sp_spaceused 'sys.change_tracking_309576141'  
sp_spaceused 'sys.syscommittab'  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Controle de alterações de dados &#40;SQL Server&#41;](track-data-changes-sql-server.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [Propriedades do Banco de Dados &#40;Página Controle de Alterações&#41;](../databases/database-properties-changetracking-page.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables)   
 [Controle de alterações de dados &#40;SQL Server&#41;](track-data-changes-sql-server.md)   
 [Sobre o controle de alterações &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md)   
 [Trabalhar com dados de alterações &#40;SQL Server&#41;](work-with-change-data-sql-server.md)  
  
  
