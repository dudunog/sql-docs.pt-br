---
title: Conectar-se a um banco de dados Teradata (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connterradb.f1
ms.assetid: 875ad4a3-a2b3-4b68-8c1c-6507e9f25b4d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc6712598452b1957857509e6b3ff6f659a16c4b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087184"
---
# <a name="connect-to-a-teradata-database-ssas"></a>Conectar a um banco de dados Teradata (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a especificar as configurações de conexão a um banco de dados Teradata. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador.  
  
> [!NOTE]  
>  As credenciais do usuário atual são usadas na seleção de um banco de dados nesta página. Porém, a importação não terá êxito se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome de conexão amigável**  
 Digite um nome exclusivo para esta conexão de fonte de dados. Esse é um campo obrigatório.  
  
 **Nome do servidor**  
 Digite ou selecione o nome da instância do servidor com a qual se conectar.  
  
 **Nome de usuário**  
 Especifique um nome de usuário para a conexão de banco de dados.  
  
 Este nome de usuário é usado ao construir a cadeia de conexão para a fonte de dados. Essas credenciais também são usadas na visualização e filtragem de dados na janela Propriedades de Tabela e no Assistente de Importação. Essas credenciais não são usadas para importar ou atualizar dados; em vez disso, utiliza-se as credenciais do Windows especificadas na página Informações sobre Representação.  
  
 **Senha**  
 Especifique uma senha para a conexão de banco de dados.  
  
 **Salvar minha senha**  
 Especifique se a senha que você inseriu na caixa **Senha** deve ser armazenada.  
  
 **Avançado**  
 Defina as propriedades de conexão adicionais usando a caixa de diálogo **Definir Propriedades Avançadas** . Para obter mais informações, consulte [Definir propriedades avançadas &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Testar conexão**  
 Tente estabelecer uma conexão com a fonte de dados usando as configurações atuais. Uma mensagem que indica se a conexão foi bem-sucedida é exibida.  
  
  
