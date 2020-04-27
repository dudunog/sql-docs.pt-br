---
title: Editor de origem de OLE DB (página Gerenciador de conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsourceadapter.connection.f1
helpviewer_keywords:
- OLE DB Source Editor
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 22b7c9ea4012655043cac7eb7f3d432ef1e2e854
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057052"
---
# <a name="ole-db-source-editor-connection-manager-page"></a>Editor de Origem OLE DB (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem OLE DB** para selecionar o gerenciador de conexões OLE DB para a origem. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
> [!NOTE]  
>  Para carregar dados de uma fonte de dados que usa o [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2007, use uma origem OLE DB. Você não pode usar uma origem do Excel para carregar dados de uma fonte de dados do Excel 2007. Para obter mais informações, consulte [Configurar Gerenciador de Conexões OLE DB](configure-ole-db-connection-manager.md).  
>   
>  Para carregar dados de uma fonte de dados que usa o [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2003 ou uma versão anterior, use uma origem do Excel. Para obter mais informações, consulte [Editor de Fonte Excel &#40;Página Gerenciador de Conexões&#41;](../../2014/integration-services/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  A `CommandTimeout` propriedade da fonte de OLE DB não está disponível no **Editor de fonte de OLE DB**, mas pode ser definida usando o **Editor avançado**. Para obter mais informações sobre esta propriedade, consulte a seção Origem do Excel em [Propriedades personalizadas do OLE DB](data-flow/ole-db-custom-properties.md).  
  
 Para saber mais sobre a origem de OLE DB, consulte [OLE DB Source](data-flow/ole-db-source.md).  
  
## <a name="open-the-ole-db-source-editor-connection-manager-page"></a>Abrir a página do Gerenciador de Conexões do Editor de Origem OLE DB  
  
1.  Adicione a origem OLE DB ao pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no componente de origem e clique em **Editar**.  
  
3.  Clique em **Gerenciador de Conexões**.  
  
## <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Novo**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Modo de acesso a dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Descrição|  
|------------|-----------------|  
|Tabela ou exibição|Recupere os dados de uma tabela ou exibição na fonte de dados OLE DB.|  
|Nome da tabela ou variável do nome de exibição|Especifique a tabela ou nome de exibição em uma variável.<br /><br /> **Informações relacionadas:** [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md)|  
|Comando SQL|Recupere os dados da fonte de dados OLE DB usando uma consulta SQL.|  
|Comando SQL a partir da variável|Especifique o texto da consulta SQL em uma variável.|  
  
 **Visualizar**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A**visualização** pode exibir até 200 linhas.  
  
> [!NOTE]  
>  Quando você visualiza os dados, as colunas com um tipo de dado CLR definido pelo usuário não contêm dados. Em vez disso, o valor \<valor muito grande para ser exibido> ou System.Byte[] é exibido. O primeiro é exibido quando a fonte de dados é acessada usando o provedor SQL OLE DB e o segundo, usando o provedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da tabela ou da exibição**  
 Selecione o nome da tabela ou da exibição na lista de tabelas ou exibições disponíveis na fonte de dados.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da tabela ou da exibição.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Parameters**  
 Se você inseriu uma consulta parametrizada usando ? como um espaço reservado para o parâmetro no texto da consulta, use a caixa de diálogo **Definir Parâmetros da Consulta** para mapear os parâmetros de entrada da consulta para as variáveis do pacote.  
  
 **Compilar consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
### <a name="data-access-mode--sql-command-from-variable"></a>Modo de acesso aos dados = Comando SQL a partir da variável  
 **Nome da variável**  
 Selecione a variável que contém o texto da consulta SQL.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de fonte de OLE DB &#40;página colunas&#41;](../../2014/integration-services/ole-db-source-editor-columns-page.md)   
 [Editor de origem OLE DB &#40;página saída de erro&#41;](../../2014/integration-services/ole-db-source-editor-error-output-page.md)   
 [Extrair dados usando a fonte de OLE DB](data-flow/extract-data-by-using-the-ole-db-source.md)   
 [gerenciador de conexões OLE DB](connection-manager/ole-db-connection-manager.md)  
  
  
