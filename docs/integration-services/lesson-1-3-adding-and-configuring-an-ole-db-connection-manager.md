---
description: 'Lição 1-3: Adicionar e configurar um gerenciador de conexões OLE DB'
title: 'Etapa 3: Adicionar e configurar um gerenciador de conexões OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 33eeb6e462c096505fc4fbd1088e7f5b36b37618
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88449654"
---
# <a name="lesson-1-3-add-and-configure-an-ole-db-connection-manager"></a>Lição 1-3: Adicionar e configurar um gerenciador de conexões OLE DB

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Depois de adicionar um gerenciador de conexões de arquivo simples para conectar-se à fonte de dados, adicione um gerenciador de conexões OLE DB para conectar-se ao destino de dados. Um gerenciador de conexões OLE DB permite que um pacote extraia dados de qualquer fonte de dados compatível com OLE DB ou carregue dados nela. Usando um gerenciador de conexões OLE DB, você pode especificar o servidor, o método de autenticação e o banco de dados padrão para a conexão.  
  
Nesta tarefa, você criará um gerenciador de conexões OLE DB que usa a Autenticação do Windows para conectar-se à instância local do **AdventureWorksDW2012**. Esse gerenciador de conexões OLE DB também será referenciado por outros componentes criados posteriormente neste tutorial, como a transformação Pesquisa e o destino OLE DB.  
  
## <a name="add-and-configure-an-ole-db-connection-manager"></a>Adicionar e configurar um gerenciador de conexões OLE DB

1. No painel do **Gerenciador de Soluções**, clique com o botão direito do mouse em **Gerenciadores de Conexão** e selecione **Novo Gerenciador de Conexão**.

1. Na caixa de diálogo **Adicionar Gerenciador de Conexão do SSIS**, selecione **OLEDB** e, em seguida, **Adicionar**.
    
2. Na caixa de diálogo **Configurar Gerenciador de Conexões OLE DB**, clique em **Novo**.  
  
3. Em **Nome do servidor**, insira **localhost**.  
  
    Quando você especifica localhost como o nome do servidor, o gerenciador de conexões se conecta à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador local. Para usar uma instância remota do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], substitua localhost pelo nome do servidor ao qual você deseja se conectar.  
  
4. No grupo **Fazer logon no servidor** , verifique se a opção **Usar Autenticação do Windows** está selecionada.  
  
5. No grupo **Conectar-se a um banco de dados** , na caixa **Selecionar ou inserir um nome de banco de dados** , digite ou selecione **AdventureWorksDW2012**.  
  
6. Selecione **Testar Conexão** para verificar se as configurações de conexão especificadas são válidas.  
  
7. Selecione **OK**.  
  
8. Selecione **OK**.  
  
9. No painel **Gerenciador de Conexões**, verifique se **localhost. AdventureWorksDW2012** está selecionado.  
  

## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 4: Adicionar uma tarefa de Fluxo de Dados ao pacote](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>Confira também  
[Gerenciador de conexões OLE DB](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
