---
title: Gerar Scripts
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
author: rothja
ms.author: jroth
ms.openlocfilehash: 8207e899c98d788ea0cbd618231597b22a6c0793
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063454"
---
# <a name="generate-scripts-sql-server-management-studio"></a>Gerar scripts (SQL Server Management Studio)
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece dois mecanismos para gerar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] . Você pode criar scripts para vários objetos usando o **Assistente para gerar e publicar scripts.** É possível gerar um script para objetos individuais ou para vários objetos usando o menu **Gerar script como** no **Pesquisador de Objetos**.  
  
1.  **Escolha um método:**  [Assistente para Gerar e Publicar Scripts](#GenPubScriptWiz), [Menu Script Como do Pesquisador de Objetos](#OEScriptAsMenu)  
  
2.  **Para usar o menu Script Como:**  [Gerar script de um único objeto](#ScriptSingleObject), [Gerar script de dois objetos usando o Pesquisador de Objetos](#ScriptTwoObjectsOE), [Gerar script de dois objetos usando detalhes do Pesquisador de Objetos](#ScriptTwoObjectsOED)  
  
## <a name="before-you-begin"></a>Antes de começar  
 Escolha o mecanismo que melhor satisfaz seus requisitos.  
  
###  <a name="generate-and-publish-scripts-wizard"></a><a name="GenPubScriptWiz"></a> Assistente para Gerar e Publicar Scripts  
 Use o **Assistente para Gerar e Publicar Scripts** para criar um script [!INCLUDE[tsql](../../includes/tsql-md.md)] para vários objetos. O assistente gera um script de todos os objetos de um banco de dados ou de um subconjunto dos objetos selecionado. O assistente tem muitas opções para seus scripts, por exemplo, se permissões, ordenações, restrições etc. devem ser incluídos. Para obter instruções sobre como usar o assistente, veja [Assistente para Gerar e Publicar Scripts](generate-and-publish-scripts-wizard.md).  
  
###  <a name="object-explorer-script-as-menu"></a><a name="OEScriptAsMenu"></a> Menu Script Como do Pesquisador de Objetos  
 Você pode usar o menu **Gerar Script como do Pesquisador de Objetos** para gerar script de um único objeto, de vários objetos ou de várias instruções para um único objeto. É possível escolher um de vários tipos de scripts. Por exemplo, para criar, alterar ou descartar o objeto. É possível salvar o script em uma janela do Editor de Consultas em um arquivo ou na Área de Transferência. O script é criado em formato Unicode.  
  
##  <a name="to-generate-a-script-of-a-single-object"></a><a name="ScriptSingleObject"></a> Para gerar um script de um único objeto  
 **Para gerar script de um único objeto**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados que contém o objeto do qual será gerado um script.  
  
3.  Expanda a categoria do objeto. Por exemplo, expanda o nó **Tabelas** ou **Exibições** .  
  
4.  Clique com o botão direito do mouse no objeto, aponte para **script \<object type> como**, por exemplo, apontar para **script de tabela como**.  
  
5.  Aponte para o tipo de script, como **Criar para** ou **Alterar para**.  
  
6.  Selecione o local para salvar o script, como **Nova janela do Editor de Consultas** ou **Área de Transferência**.  
  
##  <a name="to-generate-a-script-of-two-objects-using-object-explorer"></a><a name="ScriptTwoObjectsOE"></a> Para gerar um script de dois objetos usando o Pesquisador de Objetos  
 **Para gerar um script de dois objetos usando o Pesquisador de Objetos**  
  
 Talvez você queira um script que tenha várias opções, como descartar um procedimento e, em seguida, criar um procedimento ou criar uma tabela e alterá-la. Os processos a seguir para gerar scripts de vários objetos também funcionarão se você precisar criar um script que faça referência a tipos de objetos diferentes, como tabelas, exibições e procedimentos armazenados.  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados que contém os objetos dos quais será gerado um script.  
  
3.  Clique com o botão direito do mouse no primeiro objeto a ser inserido no script, aponte para **script \<object type> como**e, nas seleções **salvar como** , escolha **nova janela do editor de consultas** como o destino de saída.  
  
4.  Navegue até o segundo objeto do qual deseja gerar script.  
  
5.  Clique com o botão direito do mouse no objeto, aponte para **script \<object type> como**e, nas seleções **salvar como** , escolha **área de transferência** como o destino de saída.  
  
6.  Na janela Editor de Consultas aberta para o primeiro objeto, cole o script para o segundo objeto da área de transferência.  
  
##  <a name="to-generate-a-script-of-two-objects-using-object-explorer-details"></a><a name="ScriptTwoObjectsOED"></a> Para gerar um script de dois objetos usando Detalhes do Pesquisador de Objetos  
 **Para gerar um script de dois objetos usando Detalhes do Pesquisador de Objetos**  
  
 É possível usar o painel **Detalhes do Pesquisador de Objetos** para gerar um script para vários objetos da mesma categoria.  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados que contém os objetos dos quais será gerado um script.  
  
3.  Expanda o nó de categoria dos tipos de objeto dos quais você deseja gerar o script, como o nó **Tabelas** .  
  
4.  Abra o painel **Detalhes do Pesquisador de Objetos** selecionando **F7**ou abrindo o menu **Exibição** e selecionando **Detalhes do Pesquisador de Objetos**.  
  
5.  Clique com o botão esquerdo do mouse em um dos objetos dos quais você deseja gerar um script.  
  
6.  Clique em Ctrl + botão esquerdo do mouse no segundo objeto do qual você deseja gerar um script.  
  
7.  Clique com o botão direito do mouse em um dos objetos selecionados e selecione **script \<object type> como**.  
  
  
