---
description: Fazer alterações às tabelas selecionadas para capturar alterações
title: Fazer alterações nas tabelas selecionadas para capturar alterações | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- makChanToTab
ms.assetid: a309f82a-c6ef-464d-a6ef-df555bfb609a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b6caa3f5d6d1abe5a8d4a197391da18a74942f00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88394482"
---
# <a name="make-changes-to-the-tables-selected-for-capturing-changes"></a>Fazer alterações às tabelas selecionadas para capturar alterações

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Nesta caixa de diálogo, você pode selecionar colunas específicas da tabela selecionada da qual capturar alterações. Você também pode editar as informações de **Função de Segurança** e **Instância de Captura** .  
  
 Você pode fazer as seguintes alterações nas tabelas selecionadas para capturar alterações nessa caixa de diálogo.  
  
 **Faça alterações para quais colunas são incluídas na instância CDC:**  
  
 Siga um ou ambos destes procedimentos:  
  
-   Marque a caixa de seleção ao lado de qualquer coluna adicional que você quer incluir.  
  
-   Desmarque a caixa de seleção ao lado de qualquer coluna que você não quer mais incluir.  
  
 **Alterar o tipo de dados para uma coluna específica**:  
  
 Você pode selecionar um tipo de dados diferente para uma coluna específica. Você pode alterar somente o tipo de dados para um tipo de dados que seja compatível com o tipo de dados original.  
  
 Para alterar o tipo de dados, clique na coluna **Tipo de Dados** e selecione um tipo de dados diferente. Somente os tipos de dados que são compatível com o tipo de dados original estão disponíveis.  
  
> [!NOTE]  
>  Se nenhum tipo de dados adicional puder ser selecionado, a lista suspensa não estará disponível.  
  
 **Alterar a função de segurança**  
  
 Digite um novo nome ou edite o nome da função de associação de segurança no campo **Função de Segurança** .  
  
 **Altere ou adicione uma instância de captura**  
  
 No campo **Instância de Captura** , insira um nome para a instância de captura.  
  
## <a name="see-also"></a>Consulte Também  
 [Como criar a instância de banco de dados de alteração do SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Selecionar tabelas e colunas Oracle](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
