---
title: Extrair dados usando a origem ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 10f25703-49a2-4d45-abab-6b4da2a57ba5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ed7cdc549b3521d3efddc831455136775378cd52
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915666"
---
# <a name="extract-data-by-using-the-odbc-source"></a>Extrair dados por meio da origem ODBC
  Este procedimento descreve como extrair dados usando uma fonte ODBC. Para adicionar e configurar uma origem ODBC, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados.  
  
### <a name="to-extract-data-using-an-odbc-source"></a>Para extrair dados usando uma origem ODBC  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] desejado.  
  
2.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a origem ODBC para a superfície de design.  
  
3.  Clique duas vezes na origem ODBC.  
  
4.  Na caixa de diálogo **Editor de Origem de ODBC** , na página **Gerenciador de Conexões** , selecione um gerenciador de conexões ODBC existente ou clique em **Novo** para criar um gerenciador de conexões novo.  
  
5.  Selecione o método de acesso de dados.  
  
    -   **Nome da Tabela**: selecione uma tabela ou exibição no banco de dados ou digite uma expressão regular para identificar a tabela à qual o gerenciador de conexão ODBC se conecta.  
  
         Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1.000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.  
  
    -   **Comando SQL**: digite um Comando SQL ou clique em **Procurar** para carregar a consulta SQL de um arquivo de texto.  
  
6.  É possível clicar em **Visualizar** para exibir até 200 linhas dos dados extraídos pela origem ODBC.  
  
7.  Para atualizar o mapeamento entre colunas externas e de saída, clique em **Colunas** e selecione colunas diferentes na lista **Coluna Externa** .  
  
8.  Se necessário, atualize os nomes de colunas de saída editando valores na lista **Coluna de Saída** .  
  
9. Para configurar a saída de erro, clique em **Saída de Erro**.  
  
10. Clique em **OK**.  
  
11. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de Fonte ODBC &#40;Página Gerenciador de Conexões&#41;](../odbc-source-editor-connection-manager-page.md)   
 [Editor de Origem ODBC &#40;Página Colunas&#41;](../odbc-source-editor-columns-page.md)   
 [Editor de Fonte ODBC &#40;Página Saída de Erro&#41;](../odbc-source-editor-error-output-page.md)  
  
  
