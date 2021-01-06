---
title: uso do utilitário de prompt de comando dta
description: Saiba mais sobre as funcionalidades fornecidas pelo utilitário de prompt de comando dta além daquelas fornecidas pelo Orientador de Otimização do Mecanismo de Banco de Dados do SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 064d7fc2d47cbd4f688d113f60be6080ca90fee1
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97642578"
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>Lição 3: uso do utilitário de prompt de comando dta
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
O utilitário de prompt de comando **dta** oferece funcionalidade além da fornecida pelo Orientador de Otimização do Mecanismo de Banco de Dados.  
  
Você pode usar suas ferramentas XML favoritas para criar arquivos de entrada para o utilitário usando o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Esse esquema é instalado durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e pode ser encontrado em: C:\Arquivos de Programas (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd.  
  
O esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados também está disponível online no [Microsoft Web site](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
O esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados oferece mais flexibilidade para definir opções de ajuste. Ele permite, por exemplo, executar a análise hipotética. A análise hipotética compreende a especificação de um conjunto de estruturas de design físicas hipotéticas e existentes para o banco de dados a ser ajustado e a análise usando o Orientador de Otimização do Mecanismo de Banco de Dados para descobrir se esse design físico hipotético melhorará o desempenho do processamento de consulta. Esse tipo de análise oferece a vantagem de poder avaliar a nova configuração sem incorrer na sobrecarga da implementação de fato. Se seu design físico hipotético não oferecer a melhora de desempenho desejada, é fácil alterá-lo e fazer novas análises até que você alcance a configuração que produza os resultados necessários.  
  
Além disso, usando o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados e o utilitário de prompt de comando **dta** , você pode inserir a funcionalidade do Orientador de Otimização do Mecanismo de Banco de Dados em scripts e usá-la com outras ferramentas de design de banco de dados.  
  
A utilização da funcionalidade de entrada XML do Orientador de Otimização do Mecanismo de Banco de Dados ultrapassa o alcance desta lição.  
  
 Essa tarefa descreve a inicialização do utilitário **dta**, a exibição da Ajuda e o uso do utilitário para ajustar uma carga de trabalho usando o prompt de comando. Ela usa a carga de trabalho MyScript.sql, criada para a prática [Ajustando uma carga de trabalho](lesson-2-using-database-engine-tuning-advisor.md#tuning-a-workload) da GUI (interface gráfica do usuário) do Orientador de Otimização do Mecanismo de Banco de Dados  
  
O tutorial usa o banco de dados de exemplo AdventureWorks2017. Por motivos de segurança, os bancos de dados de exemplo não são instalados por padrão. Para instalar os bancos de dados de exemplo, consulte [Instalando amostras e bancos de dados de exemplo do SQL Server](../../samples/adventureworks-install-configure.md).  
  
As tarefas a seguir descrevem a abertura de um prompt de comando, a inicialização do utilitário de prompt de comando **dta** , a exibição da Ajuda sobre a sintaxe e o ajuste de uma carga de trabalho simples, MyScript.sql, que você criou em [Ajustando uma carga de trabalho](./lesson-2-using-database-engine-tuning-advisor.md).  

## <a name="prerequisites"></a>Pré-requisitos 

Para concluir este tutorial, você precisará do SQL Server Management Studio, bem como acesso a um servidor que executa o SQL Server e um banco de dados do AdventureWorks.

- Instalar o [SQL Server 2017 Developer Edition.](https://www.microsoft.com/sql-server/sql-server-downloads)
- Baixar o [Banco de dados de exemplo do AdventureWorks2017.](../../samples/adventureworks-install-configure.md)


Instruções para restaurar bancos de dados no SSMS são encontradas aqui: [Restaurar um banco de dados.](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)

  >[!NOTE]
  > Este tutorial destina-se a um usuário familiarizado com o uso de SQL Server Management Studio e com as tarefas básicas de administração de banco de dados. 

## <a name="access-dta-command-prompt-utility-help-menu"></a>Acessar o menu de ajuda do utilitário de prompt de comando do DTA
  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para **Acessórios** e clique em **Prompt de Comando**.  
  
2.  No prompt de comando, digite o seguinte e pressione ENTER:  
  
    ```  
    dta -? | more  
    ```  
  
    A parte `| more` desse comando é opcional. Porém, seu uso permite que você pesquise na sintaxe de ajuda do utilitário. Pressione ENTER para avançar o texto de ajuda pela linha ou pressione a SPACEBAR para avançar por página.  

  ![Como usar a ajuda com o utilitário cmd do DTA](media/dta-tutorials/dta-cmd-help.png)

## <a name="tune-simple-workload-using-the-dta-command-prompt-utility"></a>Ajustar uma carga de trabalho simples usando o utilitário de prompt de comando do DTA  


  
1.  No prompt de comando, navegue até o diretório em que você armazenou o arquivo MyScript.sql.  
  
2.  No prompt de comando, digite o seguinte e pressione ENTER para executar o comando e iniciar a sessão de ajuste (observe que o utilitário faz diferenciação de maiúsculas e minúsculas na análise de comandos):  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
    onde `-S` especifica o nome de seu servidor e a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] é instalado. A configuração `-E` especifica que você quer usar uma conexão confiável com a instância, o que é apropriado se você estiver se conectando com uma conta de domínio Windows. A configuração `-D` especifica o banco de dados que você quer ajustar, `-if` especifica o arquivo de carga de trabalho, `-s` especifica o nome de sessão, `-of` especifica o arquivo para o qual você deseja que a ferramenta escreva o script de recomendações [!INCLUDE[tsql](../../includes/tsql-md.md)] e `-ox` especifica o arquivo para o qual você deseja que a ferramenta escreva as recomendações no formato XML. As três últimas opções especificam opções de ajuste como segue: `-fa IDX_IV` especifica que o Orientador de Otimização do Mecanismo de Banco de Dados só deve considerar adicionar índices (clusterizado e não clusterizado) e exibições indexadas; `-fp NONE` especifica que nenhuma estratégia de partição deve ser considerada durante a análise; e `-fk NONE` especifica que nenhuma estrutura de design física existente no banco de dados deve ser mantida quando o Orientador de Otimização do Mecanismo de Banco de Dados faz suas recomendações.  

  ![como usar o CMD com o DTA](media/dta-tutorials/dta-cmd.png)
  
3.  Depois que o Orientador de Otimização do Mecanismo de Banco de Dados termina de ajustar a carga de trabalho, exibe uma mensagem que indica que a sessão de ajuste foi concluída com êxito. Você pode exibir os resultados do ajuste, usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para abrir os arquivos MySession2OutputScript.sql e MySession2Output.xml. Como alternativa, você também pode abrir a sessão de ajuste MySession2 na GUI do Orientador de Otimização do Mecanismo de Banco de Dados e exibir suas recomendações e relatórios da mesma forma que fez em [Exibindo recomendações de ajuste](./lesson-2-using-database-engine-tuning-advisor.md) e [Exibindo relatórios de ajuste](./lesson-2-using-database-engine-tuning-advisor.md).  
  
 
## <a name="after-you-finish-this-tutorial"></a>Depois de você concluir este tutorial  
Depois de você terminar as lições deste tutorial, recorra aos tópicos a seguir para obter mais informações sobre o Orientador de Otimização do Mecanismo de Banco de Dados:  
  
-   [Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md) para obter descrições sobre como executar tarefas com essa ferramenta. 
-   [dta Utility](../../tools/dta/dta-utility.md) para obter material de referência sobre o utilitário de prompt de comando e o arquivo XML opcional que você pode usar para controlar a operação do utilitário.  
  
Para retornar ao início do tutorial, confira [Tutorial: Orientador de Otimização do Mecanismo de Banco de Dados](../../tools/dta/tutorial-database-engine-tuning-advisor.md).  
  
## <a name="see-also"></a>Consulte Também  
[Tutoriais do Mecanismo de Banco de Dados](../../relational-databases/database-engine-tutorials.md)  
