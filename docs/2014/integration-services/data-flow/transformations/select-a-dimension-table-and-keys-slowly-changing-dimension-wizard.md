---
title: Selecionar uma Tabela e Chaves de Dimensão (Assistente para Dimensões de Alteração Lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6207f01290b21c556ed16a836d12974d227e2d3c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939337"
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>Selecionar uma Tabela e Chaves de Dimensão (Assistente para Dimensões de Alteração Lenta)
  Use a página **Selecionar uma Tabela e Chaves de Dimensão** para selecionar uma tabela de dimensões a ser carregada. Mapeie colunas do fluxo de dados para as colunas que serão carregadas.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opções  
 **Connection manager**  
 Selecione um gerenciador de conexões OLE DB existente na lista ou clique em **Novo** para criar um novo gerenciador de conexões OLE DB.  
  
> [!NOTE]  
>  O Assistente para Dimensão de Alteração Lenta dá suporte apenas a gerenciadores de conexões OLE DB e a conexões ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Novo**  
 Use a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** para selecionar um gerenciador de conexões existente ou clique em **Nova** para criar uma nova conexão OLE DB.  
  
 **Tabela ou Exibição**  
 Selecione uma tabela ou exibição da lista.  
  
 **Colunas de Entrada**  
 Selecione na lista as colunas de entrada para as quais você pode especificar mapeamento.  
  
 **Colunas de Dimensão**  
 Exiba todas as colunas de dimensão disponíveis.  
  
 **Tipo de Chave**  
 Selecione uma das colunas de dimensão para servir de chave de negócio. É necessário possuir uma chave de negócio.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
