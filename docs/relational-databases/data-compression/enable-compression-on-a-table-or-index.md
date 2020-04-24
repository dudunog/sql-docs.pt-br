---
title: Habilitar a compactação em uma tabela ou índice | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.compwiz.compressiontype.f1
- sql13.swb.compwiz.outputoptions.f1
- sql13.swb.compwiz.summary.f1
- sql13.swb.compwiz.scriptfileoption.f1
- sql13.swb.compwiz.progress.f1
- sql13.swb.compwiz.welcome.f1
- sql13.swb.compwiz.createjob.f1
- sql13.swb.compwiz.selectaction.f1
helpviewer_keywords:
- data compression wizard
- compression [SQL Server], enable
ms.assetid: b7442cff-e616-475a-9c5a-5a765089e5f2
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ea7316580a1c9d3ce2f68e0d701cd5885c52bc80
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488005"
---
# <a name="enable-compression-on-a-table-or-index"></a>Permitir a compactação em uma tabela ou índice

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tópico descreve como habilitar a compactação em uma tabela ou índice no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para permitir a compactação em uma tabela ou índice, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Não é possível habilitar as tabelas do sistema para compactação.  
  
-   Se a tabela for um heap, a operação de reconstrução para o modo ONLINE será um thread único. Use o modo OFFLINE para uma operação de reconstrução de um heap multi-threaded. Para obter mais informações sobre compactação de dados, veja [Compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
-   Não será possível alterar a configuração de compactação de uma única partição se a tabela tiver índices não alinhados.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou índice.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-enable-compression-on-a-table-or-index"></a>Para permitir a compactação em uma tabela ou índice  
  
1.  No Pesquisador de Objetos, expanda o banco de dados que contém a tabela que você deseja compactar e expanda a pasta **Tabelas** .  
  
2.  Para compactar um índice, expanda a tabela que contém o índice que você deseja compactar e expanda a pasta **Índices** .  
  
3.  Clique com o botão direito do mouse na tabela ou no índice a ser compactado, aponte para **Armazenamento** e selecione **Gerenciar Compactação...** .  
  
4.  No Assistente de Compactação de Dados, na página **Bem-vindo ao Assistente de Compactação de Dados** , clique em **Avançar**.  
  
5.  Na página **Selecionar Tipo de Compactação** , selecione o tipo de compactação a ser aplicado a cada partição na tabela ou índice que você deseja compactar. Ao concluir, clique em **Avançar**.  
  
     As seguintes opções estão disponíveis na página **Selecionar Tipo de Compactação** :  
  
     Caixa de seleção**Usar o mesmo tipo de compactação para todas as partições**  
     Selecione para configurar a mesma configuração de compactação para todas as partições. Isso habilita a caixa de seleção e desabilita a coluna **Tipo de Compactação** na grade. Quando selecionadas, as opções na lista adjacente são **Nenhum**, **Linha**e **Página**.  
  
     **Número da partição**  
     Lista cada partição na tabela ou índice. Essa coluna é somente leitura.  
  
     **Tipo de Compactação**  
     Selecione a opção de compactação para cada partição. Ela não estará disponível quando a opção **Usar o mesmo tipo de compactação para todas as partições** estiver selecionada. As opções da lista são **Nenhum**, **Linha**e **Página**.  
  
     **Limite**  
     Exibe o limite da partição. Essa coluna é somente leitura.  
  
     **Contagem de Linhas**  
     Exibe o número de linhas nesta partição. Essa coluna é somente leitura.  
  
     **Espaço Atual**  
     Exibe o espaço atual ocupado por esta partição em megabytes (MB). Essa coluna é somente leitura.  
  
     **Espaço Compactado Solicitado**  
     Depois de clicar em **Calcular**, essa coluna exibe o tamanho estimado de cada partição após a compactação usando a configuração especificada na coluna **Tipo de Compactação** . Essa coluna é somente leitura.  
  
     **Calcular**  
     Clique para estimar o tamanho de cada partição após a compactação usando a configuração especificada na coluna **Tipo de Compactação** .  
  
6.  Na página **Selecione uma Opção de Saída** , especifique como você deseja preencher sua compactação. Selecione **Criar Script** para criar um script SQL baseado nas páginas anteriores no assistente. Selecione **Executar imediatamente** para criar a nova tabela particionada depois de concluir todas as páginas restantes no assistente. Selecione **Agenda** para criar uma nova tabela particionada em um momento predeterminado no futuro.  
  
     Se você selecionar **Criar script**, as opções a seguir estarão disponíveis em **Opções de script**:  
  
     **Script para arquivo**  
     Gera o script como um arquivo .sql. Digite um nome de arquivo e o local na caixa **Nome do arquivo** ou clique em **Procurar** para abrir a caixa de diálogo **Local do Arquivo de Script** . Em **Salvar Como**, selecione **Texto Unicode** ou **Texto ANSI**.  
  
     **Script para Área de Transferência**  
     Salva o script na área de transferência.  
  
     **Script para Nova Janela de Consulta**  
     Gera o script para uma nova janela do Editor de Consultas. Essa é a seleção padrão.  
  
     Se você selecionar **Agenda**, clique em **Alterar agenda**.  
  
    1.  Na caixa de diálogo **Nova Agenda de Trabalho**, na caixa **Nome**, digite o nome da agenda de trabalho.  
  
    2.  Na lista **Tipo de Agenda** , selecione o tipo de agenda:  
  
        -   **Iniciar automaticamente quando o SQL Server Agent for iniciado**  
  
        -   **Iniciar sempre que as CPUs estiverem ociosas**  
  
        -   **Recorrente**. Selecione essa opção se sua nova tabela particionada for atualizada com novas informações regularmente.  
  
        -   **Uma vez**. Essa é a seleção padrão.  
  
    3.  Marque ou desmarque a caixa de seleção **Habilitado** para habilitar ou desabilitar a agenda.  
  
    4.  Se você selecionar **Recorrente**:  
  
        1.  Em **Frequência**, na lista **Ocorre** , especifique a frequência de ocorrência:  
  
            -   Se você selecionar **Diário**, na caixa **Ocorre periodicamente a cada** , digite a frequência com que a agenda de trabalho se repete em dias.  
  
            -   Se você selecionar **Semanal**, na caixa **Ocorre periodicamente a cada** , digite a frequência com que a agenda de trabalho se repete em semanas. Selecione o dia ou os dias da semana em que a agenda de trabalho é executada.  
  
            -   Se você selecionar **Mensalmente**, selecione **Dia** ou **O**.  
  
                -   Se você selecionar **Dia**, digite o dia do mês que você deseja que a agenda de trabalho seja executada e a frequência com que a agenda de trabalho se repete em meses. Por exemplo, se desejar que a agenda de trabalho seja executada no 15º dia do mês a cada dois meses, selecione **Dia** e digite "15" na primeira caixa e "2" na segunda caixa. Observe que o maior número permitido na segunda caixa é "99".  
  
                -   Se você selecionar **O**, selecione o dia específico da semana no mês que você deseja que a agenda de trabalho seja executada e a frequência com que a agenda de trabalho se repete em meses. Por exemplo, se você desejar que a agenda de trabalho seja executada no último dia da semana do mês a cada dois meses, selecione **Dia**, selecione **último** na primeira lista e **dia da semana** na segunda lista e depois digite “2” na última caixa. Você também pode selecionar **primeiro**, **segundo**, **terceiro**ou **quarto**, bem como dias específicos da semana (por exemplo: domingo ou quarta-feira) nas primeiras duas listas. Observe que o maior número permitido na última caixa é "99".  
  
        2.  Em **Frequência diária**, especifique a frequência com que a agenda de trabalho se repete no dia da execução da agenda de trabalho:  
  
            -   Se você selecionar **Ocorre uma vez às**, digite a hora específica do dia em que a agenda de trabalho deve ser executada na caixa **Ocorre uma vez às** . Digite a hora, os minutos e os segundos do dia, bem como AM ou PM.  
  
            -   Se você selecionar **Ocorre a cada**, especifique a frequência com que a agenda de trabalho é executada durante o dia escolhido em **Frequência**. Por exemplo, se você desejar que o agendamento de trabalho se repita a cada 2 horas durante o dia em que é executado, selecione **Ocorre a cada**, digite "2" na primeira caixa e selecione **hora(s)** na lista. Nessa lista, você pode selecionar também **minuto(s)** e **segundo(s)** . Observe que o maior número permitido na primeira caixa é "100".  
  
                 Na caixa **Iniciando às** , digite a hora em que a agenda de trabalho deve começar a ser executada. Na caixa **Terminando às** , digite a hora em que a agenda de trabalho deve parar de se repetir. Digite a hora, os minutos e os segundos do dia, bem como AM ou PM.  
  
        3.  Em **Duração**, em **Data de início**, digite a data que você deseja que a agenda de trabalho inicie a execução. Selecione **Data de término** ou **Nenhuma data de término** para indicar quando a execução da agenda de trabalho deve parar. Se você selecionar **Data de término**, digite a data em que você deseja que a execução da agenda de trabalho pare.  
  
    5.  Se você selecionar **Uma Vez**, em **Ocorrência única**, na caixa **Data** , insira a data em que o agendamento de trabalho será executado. Na caixa **Hora** , digite a hora em que a agenda de trabalho será executada. Digite a hora, os minutos e os segundos do dia, bem como AM ou PM.  
  
    6.  Em **Resumo**, em **Descrição**, verifique se todas as configurações da agenda de trabalho estão corretas.  
  
    7.  Clique em **OK**.  
  
     Depois de concluir essa página, clique em **Avançar**.  
  
7.  Na página **Resumo da Revisão** , em **Examinar as seleções**, expanda todas as opções disponíveis para verificar se todas as configurações de compactação estão corretas. Se tudo estiver como esperado, clique em **Concluir**.  
  
8.  Na página **Progresso do Assistente de Compactação** , monitore as informações de status das ações do Assistente para Criar Partição. Dependendo das opções selecionadas no assistente, a página de progresso pode conter uma ou várias ações. A caixa superior exibe o status geral do assistente e o número de mensagens de status, erro e aviso que ele recebeu.  
  
     As opções a seguir estão disponíveis na página **Progresso do Assistente de Compactação** :  
  
     **Detalhes**  
     Fornece a ação, status e qualquer mensagem retornada pela ação executada pelo assistente.  
  
     **Ação**  
     Especifica o tipo e o nome de cada ação.  
  
     **Status**  
     Indica se a ação do assistente retornou como um todo o valor de **Êxito** ou de **Falha**.  
  
     **Mensagem**  
     Fornece qualquer mensagem de aviso ou erro retornada pelo processo.  
  
     **Report**  
     Cria um relatório contendo os resultados do Assistente para Criar Partição. As opções são **Exibir Relatório**, **Salvar Relatório no Arquivo**, **Copiar Relatório na Área de Transferência**e **Enviar Relatório como Email**.  
  
     **Exibir Relatório**  
     Abre a caixa de diálogo **Exibir Relatório** , que contém um relatório de texto do progresso do Assistente para Criar Partições.  
  
     **Salvar Relatório no Arquivo**  
     Abre a caixa de diálogo **Salvar Relatório Como** .  
  
     **Copiar Relatório na Área de Transferência**  
     Copia os resultados do relatório de progresso do assistente na Área de transferência.  
  
     **Enviar Relatório como Email**  
     Copia os resultados do relatório de progresso do assistente para uma mensagem de email.  
  
     Quando terminar, clique em **Fechar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-enable-compression-on-a-table"></a>Para permitir a compactação em uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo primeiro executa o procedimento armazenado `sp_estimate_data_compression_savings` para retornar o tamanho estimado do objeto se ele fosse usar a configuração de compactação ROW. Em seguida, o exemplo permite a compactação ROW em todas as partições na tabela especificada.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_estimate_data_compression_savings 'Production', 'TransactionHistory', NULL, NULL, 'ROW' ;  
  
    ALTER TABLE Production.TransactionHistory REBUILD PARTITION = ALL  
    WITH (DATA_COMPRESSION = ROW);   
    GO  
    ```  
  
#### <a name="to-enable-compression-on-an-index"></a>Para permitir a compactação em um índice  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Primeiro, o exemplo consulta a exibição de catálogo `sys.indexes` para retornar o nome e o `index_id` para cada índice na tabela `Production.TransactionHistory` . Em seguida, ele executaria o procedimento armazenado `sp_estimate_data_compression_savings` para retornar o tamanho estimado da ID de índice especificada como se a configuração de compactação PAGE fosse usada. Por fim, o exemplo recria o ID do índice 2 (`IX_TransactionHistory_ProductID`), especificando a compactação PAGE.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, index_id  
    FROM sys.indexes  
    WHERE OBJECT_NAME (object_id) = N'TransactionHistory';  
  
    EXEC sp_estimate_data_compression_savings   
        @schema_name = 'Production',   
        @object_name = 'TransactionHistory',  
        @index_id = 2,   
        @partition_number = NULL,   
        @data_compression = 'PAGE' ;   
  
    ALTER INDEX IX_TransactionHistory_ProductID ON Production.TransactionHistory REBUILD PARTITION = ALL WITH (DATA_COMPRESSION = PAGE);  
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) e [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Compactação de dados](../../relational-databases/data-compression/data-compression.md)   
 [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)  
  
  
