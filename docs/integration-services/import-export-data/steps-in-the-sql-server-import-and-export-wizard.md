---
description: Etapas no Assistente de Importação e Exportação do SQL Server
title: Etapas no Assistente de Importação e Exportação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5799d85c7978505503fcbd56aa85eb693da6665e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88346432"
---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>Etapas no Assistente de Importação e Exportação do SQL Server

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Este tópico descreve a sequência de etapas para importar e exportar dados com o Assistente de Importação e Exportação do SQL Server. Ele também contém links para as páginas individuais da documentação que descrevem cada página ou caixa de diálogo exibida no assistente.

Este tópico descreve somente as **etapas** no assistente. Se você estiver procurando por alguma outra coisa, consulte [Tarefas e conteúdo relacionados](#related).

## <a name="steps-for-importing-and-exporting-data"></a>Etapas para importar e exportar dados  
 A tabela a seguir lista as etapas para importar e exportar dados e as páginas correspondentes do assistente. Dependendo das opções selecionadas no assistente, você normalmente não verá todas essas páginas.  

Para obter uma visão rápida das várias telas exibidas em uma sessão típica, dê uma olhada neste exemplo simples de ponta a ponta em uma única página – [Introdução a este exemplo simples do Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

|Etapa|Páginas do Assistente|  
|----------|------------------|  
|**Bem-vindo**<br />Você não precisa realizar nenhuma ação nesta página.|[Bem-vindo ao Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**Selecione a fonte** dos dados.|[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|**Selecione o destino** para os dados.|[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**Configure o destino**. (etapas opcionais)<br /><br /> -   Criar um novo banco de dados de destino.<br />-   Se você estiver copiando dados para um arquivo de texto, defina as configurações adicionais.|[Criar banco de dados](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[Configurar um destino de arquivo simples](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**Especifique o que você deseja copiar.**|[Especificar Cópia ou Consulta de Tabela](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[Selecionar Tabelas e Exibições de Origem](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[Fornecer uma consulta de origem](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**Configure a operação de cópia**. (etapas opcionais)<br /><br /> -   Criar uma nova tabela de destino.<br />– decida o que fazer se o assistente não sabe como mapear tipos de dados entre a origem e o destino que você selecionou.<br />-   Examine os mapeamentos de coluna entre a origem e o destino.<br />-   Lidar com problemas com a conversão de tipos de dados entre origem e destino.<br />-   Visualizar os dados a serem copiados.|[Criar a instrução Tabela SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[Converter Tipos sem Verificar a Conversão](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[Mapeamentos de Coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[Examinar o mapeamento de tipo de dados](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[Caixa de diálogo Detalhes da Conversão de Coluna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[Caixa de diálogo Visualizar Dados](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**Copie os dados.**<br /><br /> Opcionalmente, salve as configurações como um pacote do SSIS (SQL Server Integration Services).|[Salvar e executar o pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[Salvar Pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[Conclua o assistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[Executando operação](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> Pressione a tecla F1 em qualquer caixa de diálogo ou página do assistente para ver a documentação da página atual.

## <a name="related-tasks-and-content"></a><a name="related"></a> Tarefas e conteúdo relacionados  
Aqui estão algumas outras tarefas básicas.
-   **Veja um exemplo rápido de como o assistente funciona.**

    -   **Se você prefere ver capturas de tela.** Veja este exemplo de ponta a ponta simples em uma única página – [Introdução a este exemplo simples do Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Se você prefere assistir a um vídeo.** Assista a este vídeo de quatro minutos no YouTube que demonstra o assistente e explica, com instruções claras e simples, como exportar dados para o Excel – [Usando o Assistente de Importação e Exportação do SQL Server para exportar para o Excel](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Saiba mais sobre como o assistente funciona.**

    -   **Saiba mais sobre o assistente.** Se você estiver procurando uma visão geral sobre o assistente, consulte [Importar e Exportar Dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Saiba como se conectar a fontes de dados e destinos.** Se estiver procurando informações sobre como se conectar aos seus dados, selecione a página desejada na lista aqui – [Conectar-se a fontes de dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Há uma página separada da documentação para cada uma das várias fontes de dados usadas com frequência. 

-   **Inicie o assistente.** Se você está pronto para executar o assistente e apenas deseja saber como iniciá-lo, consulte [Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

-   **Obter o assistente.** Se você desejar executar o assistente, mas não tiver o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador, será possível instalar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalando o SSDT (SQL Server Data Tools). Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).


