---
title: Arquitetura e gerenciamento do log de transações do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 4d1a4f97-3fe4-44af-9d4f-f884a6eaa457
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2495b9487a633fff6c5214a07e589f58fafa5e61
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62512706"
---
# <a name="sql-server-transaction-log-architecture-and-management"></a>Arquitetura e gerenciamento do log de transações do SQL Server

[!INCLUDE[appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Todo banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem um log de transações que registra todas as transações e modificações feitas no banco de dados a cada transação. O log de transações é um componente crítico do banco de dados e, se houver uma falha do sistema, será necessário que o log de transações retorne seu banco de dados a um estado consistente. Este guia fornece informações sobre a arquitetura física e lógica do log de transações. A compreensão da arquitetura pode melhorar sua efetividade na administração de logs de transações.  

  
##  <a name="transaction-log-logical-architecture"></a><a name="Logical_Arch"></a>Arquitetura lógica do log de transações  

 O log de transações do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] opera de forma lógica como se o log de transações fosse uma cadeia de caracteres de registros de log. Cada registro de log é identificado por um LSN (número de sequência de log). Cada registro de log novo é gravado no final lógico do log com um LSN maior que o do registro antes da gravação. Os registros de log são armazenados em sequência consecutiva conforme são criados. Cada registro de log contém a ID da transação a que pertence. Para cada transação, todos os registros de log associados com a transação são vinculados individualmente em uma cadeia usando ponteiros de retrocesso que aceleram a reversão da transação.  
  
 Os registros de log para modificações de dados registram a operação lógica executada ou as imagens anteriores e posteriores dos dados modificados. A imagem anterior é uma cópia dos dados antes da execução da operação; a imagem posterior é uma cópia dos dados após a execução da operação.  
  
 As etapas para recuperar uma operação dependem do tipo de registro de log:  
  
-   Log da operação lógica  
  
    -   Para avançar a operação lógica, é executada a operação novamente.  
  
    -   Para reverter a operação lógica, é executada a operação lógica inversa.  
  
-   Log da imagem anterior e posterior  
  
    -   Para avançar a operação lógica, é aplicada a imagem posterior.  
  
    -   Para reverter a operação lógica, é aplicada a imagem anterior.  
  
 São registrados muitos tipos de operações no log de transações. Essas operações incluem:  
  
-   O início e o término de cada transação.  
  
-   Toda modificação de dados (inserção, atualização ou exclusão). Isso inclui mudanças por procedimentos armazenados do sistema ou instruções DDL (linguagem de definição de dados) para qualquer tabela, inclusive tabelas do sistema.  
  
-   Toda extensão e alocação ou desalocação de página.  
  
-   Criando ou descartando uma tabela ou um índice.  
  
 Operações de reversão também são registradas. Cada transação reserva espaço no log de transações para verificar se há espaço de log suficiente para oferecer suporte a uma reversão causada por uma instrução de reversão explícita ou se um erro for encontrado. A quantidade de espaço reservada depende das operações executadas na transação, mas geralmente é igual à quantidade de espaço usada para registrar cada operação. Esse espaço reservado é liberado quando a transação é concluída.  
  
  A seção do arquivo de log do primeiro registro de log que deve estar presente para uma reversão bem-sucedida em todo o banco de dados para o registro de log da última gravação é chamada de parte ativa do log ou *log ativo*. Essa é a seção do log necessária para uma recuperação completa do banco de dados. Nenhuma parte do log ativo pode ter sido truncada. O LSN (número de sequência de log) desse primeiro registro de log é conhecido como LSN de recuperação mínima (*MinLSN*).  
  
##  <a name="transaction-log-physical-architecture"></a><a name="physical_arch"></a>Arquitetura física do log de transações  

 O log de transações em um banco de dados mapeia um ou mais arquivos físicos. Conceitualmente, o arquivo de log é uma cadeia de caracteres de registros de log. Fisicamente, a sequência de registros de log é armazenada com eficiência no conjunto de arquivos físicos que implementam o log de transações. Deve haver, no mínimo, um arquivo de log para cada banco de dados.  
  
 O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] divide cada arquivo de log físico interiormente em vários arquivos de log virtuais. Os arquivos de log virtuais não têm tamanho fixo e não há número fixo de arquivos de log virtuais para um arquivo de log físico. O [!INCLUDE[ssDE](../includes/ssde-md.md)] escolhe o tamanho dos arquivos de log virtuais dinamicamente enquanto está criando ou estendendo os arquivos de log. O [!INCLUDE[ssDE](../includes/ssde-md.md)] tenta manter um pequeno número de arquivos virtuais. O tamanho dos arquivos virtuais depois que um arquivo de log for estendido é a soma do tamanho do log existente com o tamanho do incremento do arquivo novo. O tamanho ou o número de arquivos de log virtuais não pode ser configurado nem definido por administradores.  
  
 O único momento em que arquivos de log virtuais afetam o desempenho do sistema é quando os arquivos de log físicos são definidos por valores baixos de *size* e *growth_increment* . O valor de *size* é o tamanho inicial do arquivo de log e o valor de *growth_increment* é a quantidade de espaço adicionada ao arquivo sempre que um novo espaço é necessário. Se os arquivos de log ficarem grandes por causa de diversos incrementos pequenos, eles terão muitos arquivos de log virtuais. Isso pode reduzir a velocidade de inicialização do banco de dados e também das operações de backup e restauração de log. Recomendamos que você atribua aos arquivos de log um valor de *size* próximo ao tamanho final necessário e também que tenha um valor de *growth_increment* relativamente grande. Para obter mais informações sobre esses parâmetros, consulte [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
 O log de transações é um arquivo embrulhado. Por exemplo, considere um banco de dados com um arquivo de log físico dividido em quatro arquivos de log virtuais. Quando o banco de dados é criado, o arquivo de log lógico começa no início do arquivo de log físico. Novos registros de log são adicionados no final do log lógico e expandem para o final do log físico. O truncamento de logs libera quaisquer logs virtuais cujos registros apareçam todos na frente do número mínimo de sequência de recuperação do log (MinLSN). O *MinLSN* é o número de sequência de log do registro de log mais antigo que deve estar presente para o êxito de uma reversão de todo o banco de dados. O log de transações no banco de dados de exemplo pareceria semelhante ao apresentado na ilustração a seguir.  
  
 ![Arquivo de log dividido em quatro arquivos de log virtuais](media/tranlog3.gif "Arquivo de log dividido em quatro arquivos de log virtuais")  
  
 Quando o final do log lógico alcança o final do arquivo de log físico, os novos registros de log são adicionados no início do arquivo de log físico.  
  
 ![Registros de log delimitados no início do arquivo de log](media/tranlog4.gif "Registros de log delimitados no início do arquivo de log")  
  
 Esse ciclo repete-se indefinidamente, desde que o final do log lógico nunca alcance o início do log lógico. Se os registros de log antigos forem truncados com frequência suficiente para sempre deixar espaço suficiente para todos os registros de log novos criados através do próximo ponto de verificação, o log nunca estará completo. Contudo, se o final do log lógico não alcançar o início do log lógico, ocorrerá uma das duas coisas:  
  
-   Se a configuração de FILEGROWTH estiver habilitada para o log e houver espaço disponível no disco, o arquivo será estendido na quantidade especificada no parâmetro *growth_increment* e os novos registros de log serão adicionados à extensão. Para obter mais informações sobre a configuração de FILEGROWTH, consulte [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
-   Se a configuração de FILEGROWTH não estiver habilitada ou se o disco que estiver mantendo o arquivo de log tiver menos espaço livre do que a quantidade especificada em *growth_increment*, será gerado um erro 9002.  
  
 Se o log contiver diversos arquivos de log físico, o log lógico percorrerá todos os arquivos de log físico antes de voltar ao início do primeiro arquivo de log físico.  
  
### <a name="log-truncation"></a>Truncamento do log  

 O truncamento de log é essencial para impedir o preenchimento do log. O truncamento de log exclui arquivos de log virtuais inativos do log de transações lógicas de um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , liberando espaço no log lógico para reutilização pelo log de transações físicas. Se um log de transações nunca foi truncado, eventualmente, ele preencherá todo o espaço em disco alocado para seus arquivos de log físicos. No entanto, para que o log possa ser truncado, deve ocorrer uma operação ponto de verificação. Um ponto de verificação grava as páginas modificadas na memória atualmente (conhecidas como páginas sujas) e as informações do log de transações de memória em disco. Quando o ponto de verificação é executado, a porção inativa do log de transações é marcada como reutilizável. Depois disso, a porção inativa pode ser liberada por meio do truncamento de log. Para obter mais informações sobre pontos de verificação, consulte [Pontos de verificação de bancos de dados &#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 As ilustrações seguintes mostram um log de transações antes e depois do truncamento. A primeira ilustração mostra um log de transações que nunca foi truncado. Atualmente, quatro arquivos de log virtuais estão em uso pelo log lógico. O log virtual inicia à frente do primeiro arquivo de log virtual e termina em log 4 virtual. O registro de MinLSN está em log 3 virtual. O log 1 virtual e o log 2 virtual contêm apenas registros de log inativos. Estes registros podem ser truncados. O log 5 virtual ainda está sem-uso e não é parte do log lógico atual.  
  
 ![Log de transação com quatro logs virtuais](media/tranlog2.gif "Log de transação com quatro logs virtuais")  
  
 A segunda ilustração mostra como o log aparece depois de ser truncado. Log 1 virtual e log 2 virtual foram liberados para reutilização. O log lógico agora inicia no começo do log 3 virtual. O log 5 virtual ainda está sem-uso e não é parte do log lógico atual.  
  
 ![Arquivo de log dividido em quatro arquivos de log virtuais](media/tranlog3.gif "Arquivo de log dividido em quatro arquivos de log virtuais")  
  
 O truncamento de log ocorre automaticamente após os seguintes eventos, exceto quando atrasado por alguma razão:  
  
-   No modelo de recuperação simples, depois de um ponto de verificação.  
  
-   No modelo de recuperação completa ou bulk-logged, depois de um backup de log, se um ponto de verificação tiver acontecido desde o backup prévio.  
  
 O truncamento de log pode ser atrasado por uma variedade de fatores. No caso de uma demora longa em truncamento de log, o log de transações pode ficar cheio. Para obter informações, consulte [Fatores que podem atrasar o truncamento de log](../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation) e [Solução de problemas de um log de transação completa &#40;Erro do SQL Server 9002&#41;](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
##  <a name="write-ahead-transaction-log"></a><a name="WAL"></a>Log de transações write-ahead  

 Esta seção descreve a função do log de transações write-ahead no registro de modificações de dados no disco. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa um WAL (log write-ahead), que garante que nenhuma modificação de dados seja gravada no disco antes de o registro de log associado ser gravado no disco. Isso mantém as propriedades ACID de uma transação.  
  
 Para entender como o log write-ahead funciona, é importante saber como os dados modificados são gravados em disco. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mantém um cache de buffer em que ele lê páginas de dados quando dados precisam ser recuperados. Quando uma página é modificada no cache do buffer, não é gravada imediatamente de volta no disco. Em vez disso, a página é marcada como *suja*. Uma página de dados pode ter mais de uma gravação lógica feita antes de ser gravada fisicamente no disco. Para cada gravação lógica, um registro de log de transações é inserido no cache de log que registra a modificação. Os registros de log devem ser gravados no disco antes de a página suja associada ser removida do cache do buffer e gravada no disco. O processo de ponto de verificação examina o cache do buffer periodicamente para buffers com páginas de um banco de dados especificado e grava todas as páginas sujas no disco. Os pontos de verificação economizam tempo durante uma recuperação posterior, pois criam um ponto em que todas as páginas sujas são gravadas no disco.  
  
 A gravação de uma página de dados modificada do cache do buffer no disco é chamada de liberação de página. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem uma lógica que impede que uma página suja seja removida antes do registro de log associado ser gravado. Os registros de log são gravados no disco quando as transações são confirmadas.  
  
##  <a name="transaction-log-backups"></a><a name="Backups"></a>Backups de log de transações  

 Esta seção apresenta conceitos sobre como fazer backup e restaurar (aplicar) logs de transações. Nos modelos de recuperação completa e de recuperação com log de operações em massa é necessário fazer backups de rotina de logs de transações (*backups de log*) para recuperar dados. É possível fazer backup do log enquanto qualquer backup completo está em execução. Para obter mais informações sobre os modelos de recuperação, consulte [Fazer backup e restaurar bancos de dados do SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Para poder criar o primeiro backup de log, você deve criar um backup completo, como um backup de banco de dados ou o primeiro de um conjunto de backups de arquivo. A restauração de um banco de dados usando apenas backups de arquivo pode tornar-se complexa. Portanto, recomendamos que, assim que possível, você inicie com um backup de banco de dados. Assim, é necessário fazer backup de log de transações regularmente. Isto não só minimiza a exposição à perda de trabalho, como também habilita o truncamento do log de transações. Normalmente, o log de transações é truncado após todos os backups de log convencionais.  
  
 É recomendável fazer backups de log com frequência suficiente para fornecer suporte aos seus requisitos empresariais, especificamente a tolerância à perda de trabalho que pode ser causada por um drive de log danificado. A frequência apropriada para fazer backups de log depende de tolerância à exposição à perda de trabalho, equilibrada por quantos backups de log é possível armazenar, administrar e, potencialmente, restaurar. Fazer um backup de log a cada 15 a 30 minutos deve ser o bastante. Se o seu negócio requer que você reduza ao mínimo a exposição à perda de trabalho, considere fazer backups de log com mais frequência. Backups de log mais frequentes têm a vantagem adicional de aumentar a frequência de truncamentos de log, resultando em arquivos de log menores.  
  
 Para limitar o número de backups de log que você precisa restaurar, é essencial fazer backup dos dados com frequência. Por exemplo, convém programar um backup de banco de dados completo por semana e backups de diferenciais de banco de dados diariamente.  
  
### <a name="the-log-chain"></a>A cadeia de logs  

 Uma sequência contínua de backups de log é chamada de *cadeia de logs*. Uma cadeia de logs começa com um backup completo do banco de dados. Normalmente, uma cadeia de logs nova será iniciada apenas quando for feito backup do banco de dados pela primeira vez ou, depois que o modelo de recuperação for trocado de recuperação simples para recuperação completa ou recuperação com log de operações bulk-logged. A menos que você decida substituir os conjuntos de backup existentes quando criar um backup de banco de dados completo, a cadeia de logs existente permanecerá intacta. Com a cadeia de logs intacta, é possível restaurar o banco de dados a partir de qualquer backup de banco de dados completo do conjunto de mídias, seguido por todos os backups de logs subsequentes até o ponto de recuperação. O ponto de recuperação pode estar no fim do último backup de log ou em um ponto de recuperação específico em qualquer dos backups de log. Para obter mais informações, veja [Backups de log do transações &#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 Para restaurar um banco de dados até o ponto de falha, a cadeia de logs deve estar intacta. Isto é, uma sequência ininterrupta de backups de log de transações deve se estender até o ponto de falha. Onde essa sequência de log deve começar depende do tipo de backup de dados que você está restaurando: banco de dados, parcial ou de arquivo. Para um backup de banco de dados ou backup parcial, a sequência de backups de log deve se estender do final de um banco de dados ou backup parcial. Para um conjunto de backups de arquivos, a sequência de backups de log deve se estender desde o início de um conjunto completo de backups de arquivos. Para obter mais informações, veja [Aplicar backups de log de transações &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
### <a name="restore-log-backups"></a>Restaurar backups de log  

 A restauração de um backup de log rola para frente as alterações que foram registradas no log de transações para recriar o estado exato do banco de dados no momento em que a operação do backup de log começou. Ao restaurar um banco de dados, é necessário, também, restaurar os backups de log que foram criados após o backup completo do banco de dados restaurado ou, desde o início do primeiro backup de arquivos que você restaura. Normalmente, depois de restaurar o backup de dados ou diferencial mais recente, será necessário restaurar uma série de backups de log até alcançar o seu ponto de recuperação. Em seguida, o banco de dados é recuperado. Isso rola para trás todas as transações que estavam incompletas quando a recuperação começou e coloca o banco de dados online. Depois que o banco de dados for recuperado, não será possível restaurar mais nenhum backup. Para obter mais informações, veja [Aplicar backups de log de transações &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
## <a name="additional-reading"></a>Leitura adicional  

 Recomendamos a leitura dos artigos e livros a seguir, que fornecem mais informações sobre o log de transações.  
  
 [Noções básicas sobre registro em log e recuperação no SQL Server, por Paul Randall](https://technet.microsoft.com/magazine/2009.02.logging.aspx)  
  
 [Gerenciamento de log de transações do SQL Server, por Tony Davis e Gail Shaw](http://www.simple-talk.com/books/sql-books/sql-server-transaction-log-management-by-tony-davis-and-gail-shaw/)  
  
  
