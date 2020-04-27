---
title: Anotar uma transação (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 87e33ff166f07c10ee8b0b32eac5590f486e70c1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483910"
---
# <a name="annotate-a-transaction-master-data-services"></a>Anotar uma transação (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], anote uma transação quando desejar fornecer detalhes de suporte sobre a transação para objetivos históricos.  
  
> [!NOTE]  
>  Não é possível excluir anotações.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Para anotar as transações criadas, você deve ter permissões para acessar a área funcional **Explorer** e ter, no mínimo, a permissão **Atualizar** no objeto do modelo que você deseja anotar.  
  
-   Para anotar transações para todos os usuários, você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** e ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-annotate-a-transaction-in-explorer"></a>Para anotar uma transação no Explorer  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista **Modelo** , selecione um modelo.  
  
2.  Na lista **Versão** , selecione uma versão.  
  
3.  Clique em **Gerenciador**.  
  
4.  Na barra de menus, aponte para **Entidades** e clique na entidade que contém o membro com a transação que você deseja anotar.  
  
5.  Na grade, clique na linha do membro.  
  
6.  Clique em **Exibir Transações**.  
  
7.  Na caixa de diálogo **Exibir Transações** , clique na transação que você deseja anotar.  
  
8.  Na caixa na parte inferior da caixa de diálogo, digite sua anotação.  
  
9. Clique em **Adicionar Anotação**. A anotação é exibida no painel **Anotações** .  
  
### <a name="to-annotate-a-transaction-in-version-management-administrators-only"></a>Para anotar uma transação no Gerenciamento de Versão (somente administradores)  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , clique em **Gerenciamento de Versões**.  
  
2.  Na barra de menus, clique em **Transações**.  
  
3.  No painel **Transações** , clique na linha da grade da transação que você deseja anotar.  
  
4.  No painel **Anotações da Transação** , na caixa **Anotação** , digite a anotação.  
  
5.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;de anotações Master Data Services&#41;](../../2014/master-data-services/annotations-master-data-services.md)   
 [Transações &#40;Master Data Services&#41;](../../2014/master-data-services/transactions-master-data-services.md)  
  
  
