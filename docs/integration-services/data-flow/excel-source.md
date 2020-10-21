---
description: Origem do Excel
title: Origem do Excel | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e00a786dfb9d9ffe55274822b276a2d2497efd82
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192737"
---
# <a name="excel-source"></a>Origem do Excel

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A origem do Excel extrai dados de planilhas ou intervalos em pastas de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  

> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).

## <a name="access-modes"></a>Modos de acesso
 A origem do Excel fornece quatro modos de acesso a dados diferentes para extrair dados:  
  
-   Uma tabela ou exibição.  
  
-   Uma tabela ou exibição especificada em uma variável.  
  
-   Os resultados de uma instrução SQL. A consulta pode ser uma consulta parametrizada.  
  
-   Os resultados de uma instrução SQL armazenados em uma variável.  
  
 A origem do Excel usa um gerenciador de conexões do Excel para se conectar a uma fonte de dados e o gerenciador de conexões especifica o arquivo da planilha de trabalho a ser usado. Para obter mais informações, consulte [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 A origem do Excel tem uma saída comum e uma saída de erro.  
  
## <a name="excel-source-configuration"></a>Configuração da origem do Excel  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete todas as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](./set-the-properties-of-a-data-flow-component.md)  
  
-   [Propriedades personalizadas do Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Para obter informações sobre loop através de um grupo de arquivos do Excel, consulte [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## <a name="excel-source-editor-connection-manager-page"></a>Editor de Origem do Excel (página Gerenciador de Conexões)
  Use o nó **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem do Excel** para selecionar a pasta de trabalho do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] para a origem que será usada. A origem do Excel lê os dados de uma planilha ou intervalo nomeado em uma pasta de trabalho existente.  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** da origem do Excel não está disponível no **Editor de Origem do Excel**, mas ela pode ser definida usando o **Editor Avançado**. Para obter mais informações sobre esta propriedade, consulte a seção Origem do Excel em [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões do Excel existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Novo**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Gerenciador de Conexões do Excel** .  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Tabela ou exibição|Recupere dados de uma planilha ou intervalo nomeado no arquivo do Excel.|  
|Nome da tabela ou variável do nome de exibição|Especifique a planilha ou o nome do intervalo em uma variável.<br /><br /> **Informações relacionadas:** [Usar variáveis em pacotes](../integration-services-ssis-variables.md)|  
|Comando SQL|Recupere os dados do arquivo do Excel usando uma consulta SQL. |  
|Comando SQL a partir da variável|Especifique o texto da consulta SQL em uma variável.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A visualização pode exibir até 200 linhas.  
  
### <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da planilha do Excel**  
 Selecione o nome da planilha ou o intervalo nomeado na lista disponível na pasta de trabalho do Excel.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da planilha ou do intervalo nomeado.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Insira o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou procure o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Parâmetros**  
 Se você inseriu uma consulta parametrizada usando ? como um espaço reservado para o parâmetro no texto da consulta, use a caixa de diálogo **Definir Parâmetros da Consulta** para mapear os parâmetros de entrada da consulta para as variáveis do pacote.  
  
 **Construir consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>Modo de acesso aos dados = Comando SQL a partir da variável  
 **Nome da variável**  
 Selecione a variável que contém o texto da consulta SQL.  
  
## <a name="excel-source-editor-columns-page"></a>Editor de Origem do Excel (página Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem do Excel** para mapear uma coluna de saída para cada coluna externa (origem).  
  
### <a name="options"></a>Opções  
 **Colunas Externas Disponíveis**  
 Exiba a lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas.  
  
 **Coluna Externa**  
 Exiba as colunas externas (fonte) na ordem em que serão lidas pela tarefa. Você pode alterar essa ordem desmarcando as colunas selecionadas na tabela discutida acima e selecionando colunas externas da lista em uma ordem diferente.  
  
 **Coluna de Saída**  
 Forneça um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="excel-source-editor-error-output-page"></a>Editor de Origem do Excel (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem do Excel** para selecionar opções de tratamento de erro e definir propriedades em colunas de saída de erros.  
  
### <a name="options"></a>Opções  
 **Entrada ou Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Veja as colunas externas (origem) que você selecionou na página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem do Excel**.  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos relacionados:** [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="related-content"></a>Conteúdo relacionado  
[Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)  
[Destino do Excel](excel-destination.md)  
[Gerenciador de Conexões do Excel](../connection-manager/excel-connection-manager.md)