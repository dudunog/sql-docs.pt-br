---
title: sys.fn_all_changes_&lt;capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_all_changes
- sys.fn_all_changes
- fn_all_changes_TSQL
- sys.fn_all_changes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_all_changes_<capture_instance>
- sys.fn_all_changes_<capture_instance>
ms.assetid: 564fae96-b88c-4f22-9338-26ec168ba6f5
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b9b6e62d0f69c5182ad69e21cb46800d4ddcc86
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "72909395"
---
# <a name="sysfn_all_changes_ltcapture_instancegt-transact-sql"></a>sys.fn_all_changes_&lt;capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wrappers para as funções de consulta **todas as alterações** . Os scripts necessários para criar essas funções são gerados pelo procedimento armazenado sys.sp_cdc_generate_wrapper_function.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_all_changes_<capture_instance> ('start_time' ,'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all update old  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *start_time*  
 O valor **DateTime** que representa o ponto de extremidade inferior do intervalo de entradas da tabela de alteração a serem incluídas no conjunto de resultados.  
  
 Somente as linhas na capture_instance CDC. <>_CT alteração da tabela que têm uma hora de confirmação associada maior que *start_time* são incluídas no conjunto de resultados.  
  
 Se um valor NULL for fornecido para este argumento, o ponto de extremidade inferior do intervalo da consulta corresponderá ao ponto de extremidade inferior de um intervalo válido para a instância de captura.  
  
 *end_time*  
 O valor **DateTime** que representa o ponto de extremidade superior do intervalo de entradas da tabela de alteração a serem incluídas no conjunto de resultados.  
  
 Esse parâmetro pode assumir um dos dois significados possíveis, dependendo do valor escolhido para @closed_high_end_point quando sys. sp_cdc_generate_wrapper_function for chamado para gerar o script de criação para a função de wrapper:  
  
-   @closed_high_end_point = 1  
  
     Somente as linhas na capture_instance CDC. <>_CT alterar a tabela que têm uma hora de confirmação associada menor ou igual a end_time estão incluídas no conjunto de resultados.  
  
-   @closed_high_end_point = 0  
  
     Somente as linhas no CDC. capture_instance_CT alterar a tabela que tem uma hora de confirmação associada estritamente menor que end_time estão incluídas no conjunto de resultados.  
  
 Se um valor NULL for fornecido para este argumento, o ponto de extremidade superior do intervalo da consulta corresponderá ao ponto de extremidade superior de um intervalo válido para a instância de captura.  
  
 <row_filter_option>:: = {ALL | todas as atualizações antigas}  
 Um opção que rege o conteúdo das colunas de metadados e as linhas retornadas no conjunto de resultados.  
  
 Pode ser uma das seguintes opções:  
  
 all  
 Retorna todas as alterações do intervalo LSN especificado. Para alterações que ocorrem devido a uma operação de atualização, essa opção retorna apenas a linha que contém os novos valores após a aplicação da atualização.  
  
 all update old  
 Retorna todas as alterações do intervalo LSN especificado. Para alterações que ocorrem devido a uma operação de atualização, essa opção retorna duas linhas que contêm os valores de coluna de antes e depois da atualização.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de coluna|Descrição|  
|-----------------|-----------------|-----------------|  
|__CDC_STARTLSN|**binary(10)**|O LSN de confirmação da transação que é associado à alteração. Todas as alterações que são confirmadas na mesma transação compartilham o mesmo LSN de confirmação.|  
|__CDC_SEQVAL|**binary(10)**|Valor de sequência usado para organizar as alterações de linha em uma transação.|  
|\<colunas de @column_list>|**consoante**|As colunas identificadas no argumento *column_list* para sp_cdc_generate_wrapper_function quando ele é chamado para gerar o script que cria a função de wrapper.|  
|__CDC_OPERATION|**nvarchar(2)**|Um código de operação que indica qual operação é necessária para aplicar a linha ao ambiente de destino. Ele irá variar com base no valor do argumento *row_filter_option* fornecido na chamada:<br /><br /> *row_filter_option* = ' all'<br /><br /> 'D' – exclui a operação<br /><br /> 'I' – insere a operação<br /><br /> 'UN' – atualiza os novos valores da operação<br /><br /> *row_filter_option* = ' todas as atualizações antigas '<br /><br /> 'D' – exclui a operação<br /><br /> 'I' – insere a operação<br /><br /> 'UN' – atualiza os novos valores da operação<br /><br /> 'UO' – atualiza os valores antigos da operação|  
|\<colunas de @update_flag_list>|**bit**|Um sinalizador de bits é nomeado acrescentando _uflag ao nome da coluna. O sinalizador é sempre definido como nulo quando \__CDC_OPERATION é ', ' I ', de ' atualizadas '. Quando \__CDC_OPERATION for ' un ', ele será definido como 1 se a atualização tiver produzido uma alteração na coluna correspondente. Caso contrário, será 0.|  
  
## <a name="remarks"></a>Comentários  
 A função fn_all_changes_<capture_instance> serve como um wrapper para a função de consulta cdc. fn_cdc_get_all_changes_<capture_instance>. O procedimento armazenado sys.sp_cdc_generate_wrapper é usado para gerar o script para criar o wrapper.  
  
 As funções de wrapper não são criadas automaticamente. Há duas coisas que você precisa fazer para criar funções de wrapper:  
  
1.  Executar o procedimento armazenado para gerar o script para criar o wrapper.  
  
2.  Executar o script para realmente criar a função de wrapper.  

 As funções de wrapper permitem que os usuários consultem sistematicamente as alterações que ocorreram em um intervalo limitado por valores de **data e hora** em vez de valores LSN. As funções de wrapper executam todas as conversões necessárias entre os valores **DateTime** fornecidos e os valores LSN necessários internamente como argumentos para as funções de consulta. Quando as funções de wrapper são usadas em série para processar um fluxo de dados de alteração, elas garantem que nenhum dado seja perdido ou repetido desde que a seguinte convenção @end_time seja seguida: o valor do intervalo associado a uma chamada é @start_time fornecido como o valor para o intervalo associado à chamada subsequente.  
  
 Usando o parâmetro @closed_high_end_point ao criar o script, você pode gerar wrappers para oferecer suporte a um limite superior fechado ou a um limite superior em aberto na janela de consulta especificada. Ou seja, você pode decidir se as entradas que têm uma hora de confirmação igual ao limite superior do intervalo de extração devem ser incluídas no intervalo. Por padrão, o limite superior é incluído.  
  
 O conjunto de resultados retornado pela função wrapper **All Changes** retorna as colunas _ $ start_lsn e \_ \_$seqval da tabela de alteração como colunas \__CDC_STARTLSN e \__CDC_SEQVAL, respectivamente. Ele os segue apenas com as colunas rastreadas que apareciam no parâmetro * \@column_list* quando o wrapper foi gerado. Se * \@column_list* for NULL, todas as colunas de origem rastreadas serão retornadas. As colunas de origem são seguidas por uma coluna \_de operação, _CDC_OPERATION, que é uma coluna de um ou dois caracteres que identifica a operação.  
  
 Em seguida, os sinalizadores de bit são acrescentados ao conjunto de resultados para cada coluna identificada no parâmetro @update_flag_list. Para o wrapper **todas as alterações** , os sinalizadores de bit sempre serão nulos se __CDC_OPERATION for ', ' I ' ou ' atualizadas '. Se \__CDC_OPERATION for ' un ', o sinalizador será definido como 1 ou 0, dependendo se a operação de atualização causou uma alteração na coluna.  
  
 O modelo de configuração da captura de dados de alterações ' instanciar CDC wrapper TVFs for Schema ' mostra como usar o sp_cdc_generate_wrapper_function procedimento armazenado para obter scripts de criação para todas as funções de wrapper para funções de consulta definidas pelo esquema. Em seguida, o modelo cria esses scripts. Para obter mais informações sobre modelos, consulte [Gerenciador de modelos](../../ssms/template/template-explorer.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sys. sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
