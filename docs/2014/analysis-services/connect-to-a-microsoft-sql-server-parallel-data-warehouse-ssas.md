---
title: Conectar-se a um Microsoft SQL Server Parallel Data Warehouse (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlparadatawh.f1
ms.assetid: 98c879ee-7257-40c9-bc85-6766bd3b4885
author: minewiskan
ms.author: owend
ms.openlocfilehash: f5f3c678968f8620414ceb4c7c2574be322674cd
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527142"
---
# <a name="connect-to-a-microsoft-sql-server-parallel-data-warehouse-ssas"></a>Conectar a um Microsoft SQL Server Parallel Data Warehouse (SSAS)
  Esta página do **Assistente de Importação de Tabela** permite especificar as configurações de conexão a um Microsoft SQL Server Parallel Data Warehouse (PDW). Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 SQL Server PDW é um aplicativo altamente escalonável que proporciona desempenho a baixo custo por meio do processamento paralelo em massa. Para obter mais informações sobre o SQL Server PDW, consulte o site [SQL Server 2008 R2 Parallel Data Warehouse](https://go.microsoft.com/fwlink/?LinkId=150895). A conexão com o data warehouse é feita usando a Autenticação do SQL Server. Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador.  
  
> [!NOTE]  
>  As credenciais do usuário atual são usadas na seleção de um banco de dados nesta página. Porém, a importação não terá êxito se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Nome de conexão amigável**  
 Digite um nome exclusivo para esta conexão de fonte de dados. Esse é um campo obrigatório.  
  
 **Nome do servidor**  
 Digite o nome ou o endereço IP do servidor com o qual se conectar.  
  
 **Nome de usuário**  
 Especifique um nome de usuário para a conexão de banco de dados.  
  
 Este nome de usuário é usado ao construir a cadeia de conexão para a fonte de dados. Essas credenciais também são usadas na visualização e filtragem de dados na janela Propriedades de Tabela e no Assistente de Importação. Essas credenciais não são usadas para importar ou atualizar dados; em vez disso, utiliza-se as credenciais do Windows especificadas na página Informações sobre Representação.  
  
 **Senha**  
 Especifique uma senha para a conexão de banco de dados.  
  
 **Salvar minha senha**  
 Especifique se a senha que você inseriu na caixa **Senha** deve ser armazenada.  
  
 **Nome do banco de dados**  
 Selecione um banco de dados da lista de bancos de dados.  
  
 **Avançado**  
 Defina as propriedades de conexão adicionais usando a caixa de diálogo **Definir Propriedades Avançadas** . Para obter mais informações, consulte [Definir propriedades avançadas &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Testar conexão**  
 Tente estabelecer uma conexão com a fonte de dados usando as configurações atuais. Uma mensagem é exibida e indica se a conexão foi bem-sucedida.  
  
  
