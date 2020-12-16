---
title: Como publicar a execução de procedimento armazenado (transacional)
description: Saiba como incluir procedimentos armazenados que são executados no Publicador e afetam as tabelas publicadas na publicação transacional como artigos de execução de procedimento armazenado.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], stored procedures and
- transactional replication, publishing stored procedure execution
ms.assetid: f4686f6f-c224-4f07-a7cb-92f4dd483158
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 0f339c2be8c7424134ba76fabbed1105d447a621
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479587"
---
# <a name="publishing-stored-procedure-execution-in-transactional-replication"></a>Publicando execução de procedimento armazenado em replicação transacional
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Caso haja um ou mais procedimentos armazenados executados no Publicador e que afetem as tabelas publicadas, considere excluir esses procedimentos armazenados na publicação como artigos de execução de procedimentos armazenados. A definição do procedimento (instrução CREATE PROCEDURE) será replicada para o Assinante quando a inscrição for inicializada. Quando o procedimento armazenado for executado no Publicador, a replicação executará o procedimento correspondente no Assinante. Isso pode fornecer um desempenho significativamente melhor nos casos em que são executadas grandes operações em lote, pois apenas a execução do procedimento é replicada, ignorando-se a necessidade de replicar as alterações individuais de cada linha. Por exemplo, supondo que o procedimento armazenado a seguir seja criado no banco de dados de publicação:  
  
```  
CREATE PROC give_raise AS  
UPDATE EMPLOYEES SET salary = salary * 1.10  
```  
  
 Esse procedimento dá a cada um dos 10.000 funcionários da empresa um aumento salarial de 10 por cento. Quando executado no Publicador, esse procedimento armazenado atualiza o salário de todos os funcionários. Sem a replicação de execução de procedimento armazenado, a atualização seria enviada aos Assinantes como uma transação extensa e de várias etapas:  
  
```  
BEGIN TRAN  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 1'  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 2'  
```  
  
 E isto se repetiria em 10.000 atualizações.  
  
 Com a execução de procedimento armazenado, a replicação envia apenas o comando para execução do procedimento armazenado do Assinante, em vez de gravar todas as atualizações no banco de dados de distribuição, enviando-as em seguida ao Assinante, pela rede:  
  
```  
EXEC give_raise  
```  
  
> [!IMPORTANT]  
>  A replicação de procedimento armazenado não é apropriada para todos os aplicativos. Se um artigo for filtrado horizontalmente, de modo que os conjuntos de linhas do Publicador sejam diferentes do Assinante, a execução do mesmo procedimento armazenado em ambos retornará diferentes resultados. De forma similar, quando uma atualização é baseada em uma subconsulta de outra tabela não replicada, a execução do mesmo procedimento armazenado no Publicador e no Assinante retornará diferentes resultados.  
  
 **Para publicar a execução de um procedimento armazenado**  
  
-   SQL Server Management Studio: [Publicar a execução de um procedimento armazenado em uma publicação transacional &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
-   Programação Transact-SQL de replicação: execute [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) e especifique um valor 'serializable proc exec' (recomendado) ou 'proc exec' para o parâmetro `@type`. Para obter mais informações sobre como definir artigos, consulte [Definir um artigo](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="modifying-the-procedure-at-the-subscriber"></a>Modificando o procedimento no Assinante  
 Por padrão, a definição de procedimento armazenado no Publicador é propagada para todos os Assinantes. Porém, é igualmente possível modificar o procedimento armazenado no Assinante. Isso será útil para executar lógicas diferentes no Publicador e no Assinante. Por exemplo, considere **sp_big_delete**, um procedimento armazenado do Publicador que tem duas funções: exclui 1.000.000 linhas da tabela replicada **big_table1** e atualiza a tabela não replicada **big_table2**. Para reduzir a demanda por recursos de rede, propague a exclusão de 1 milhão de linhas como procedimento armazenado publicando **sp_big_delete**. No Assinante, modifique **sp_big_delete** para excluir apenas o 1 milhão de linhas e não realizar a atualização subsequente em **big_table2**.  
  
> [!NOTE]  
>  Por padrão, todas as alterações feitas com ALTER PROCEDURE, no Publicador, são propagadas para o Assinante. Para impedir isso, desative a propagação de alterações de esquema antes de executar ALTER PROCEDURE. Para obter informações sobre alterações de esquema, consulte [Fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="types-of-stored-procedure-execution-articles"></a>Tipos de artigos de execução de procedimento armazenado  
 Há duas formas diferentes pelas quais a execução de um procedimento armazenado pode ser publicada: artigo de execução de procedimento serializável e artigo de execução de procedimento.  
  
-   A opção serializável é recomendada uma vez que ela replica a execução do procedimento apenas se o procedimento for executado no contexto de uma transação serializável. Se o procedimento armazenado for executado fora de uma transação serializável, as alterações dos dados nas tabelas publicadas serão replicadas como uma série de instruções DML. Esse comportamento contribui para tornar os dados do Assinante consistentes com os dados do Publicador. Isso é especialmente útil para operações em lote, como grandes operações de limpeza.  
  
-   Com a opção de execução de procedimento, é possível que a execução seja replicada para todos os Assinantes, quer as instruções individuais no procedimento armazenado tenham sido bem-sucedidas ou não. Acima de tudo, como é possível que as alterações feitas nos dados pelo procedimento armazenado ocorram em várias transações, talvez os dados dos Assinantes não estejam consistentes com os dados do Publicador. Para resolver esses problemas, é necessário que os Assinantes sejam somente leitura e que você use um nível de isolamento superior ao de leitura não confirmado. Se você usar a leitura não confirmada, as alterações aos dados em tabelas publicadas serão replicadas como uma série de instruções DML.  
  
 O exemplo a seguir ilustra por que é recomendado definir a replicação de procedimentos como artigos de procedimento serializáveis.  
  
```  
BEGIN TRANSACTION T1  
SELECT @var = max(col1) FROM tableA  
UPDATE tableA SET col2 = <value>   
   WHERE col1 = @var   
  
BEGIN TRANSACTION T2  
INSERT tableA VALUES <values>  
COMMIT TRANSACTION T2  
```  
  
 No exemplo anterior, supôs-se que SELECT na transação T1 ocorre antes de INSERT na transação T2.  
  
 Se o procedimento não for executado na transação serializável (com o nível de isolamento definido como SERIALIZABLE), a transação T2 não terá permissão para inserir uma nova linha no intervalo da instrução SELECT em T1 e será confirmada antes de T1. Isto também significa que ela será aplicada ao Assinante antes de T1. Quando T1 é aplicada ao Assinante, SELECT pode retornar potencialmente um valor diferente do valor do Publicador e poderá ser convertido em um resultado diferente de UPDATE.  
  
 Se o procedimento for executado em uma transação serializável, a transação T2 não terá permissão para ser inserida no intervalo coberto pela instrução SELECT em T2. Ele será bloqueado até que T1 seja confirmada, assegurando os mesmos resultados no Assinante.  
  
 Os bloqueios serão mantidos por mais tempo quando esse procedimento for executado em uma transação serializável e poderá resultar em redução de simultaneidade.  
  
## <a name="the-xact_abort-setting"></a>A configuração XACT_ABORT  
 Ao replicar a execução de procedimento armazenado, a configuração da sessão que executa o procedimento armazenado deve especificar XACT_ABORT ON. Se XACT_ABORT estiver definida como OFF e ocorrer um erro na execução do procedimento, no Publicador, o mesmo erro ocorrerá no Assinante, causando falha do Agente de Distribuição. Especificar XACT_ABORT ON assegura que nenhum erro encontrado durante a execução, no Publicador, cause a reversão total da execução, evitando falha do Agente de Distribuição. Para obter mais informações sobre como configurar XACT_ABORT, consulte [SET XACT_ABORT &#40;Transact-SQL&#41;](../../../t-sql/statements/set-xact-abort-transact-sql.md).  
  
 Se a configuração de XACT_ABORT OFF for necessária, especifique o parâmetro **-SkipErrors** do Agente de Distribuição. Isto permitirá que o agente continue a aplicar alterações no Assinante, ainda que um erro seja encontrado.  
  
## <a name="see-also"></a>Consulte Também  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
