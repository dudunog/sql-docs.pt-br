---
title: Excluir um grupo de carga de trabalho | Microsoft Docs
description: Saiba como excluir um grupo de carga de trabalho ou um pool de recursos usando o SQL Server Management Studio ou o Transact-SQL. É necessário ter a permissão CONTROL SERVER.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], delete
- Resource Governor, workload group delete
ms.assetid: d5902c46-5c28-4ac1-8b56-cb4ca2b072d0
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 27708e9a4b5a6d0a2863595e7ee25dccf77e5d2f
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506591"
---
# <a name="delete-a-workload-group"></a>Excluir um grupo de carga de trabalho
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  É possível excluir um grupo de carga de trabalho ou um pool de recursos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou Transact-SQL.  
  
-   **Antes de começar:**  [Limitações e Restrições](#LimitationsRestrictions), [Permissões](#Permissions)  
  
-   **Para excluir um grupo de carga de trabalho usando:**  [Pesquisador de Objetos](#DelWGObjEx), [Propriedades do Resource Governor](#DelWGRGProp), [Transact-SQL](#DelWGTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
 Não é possível excluir um grupo de carga de trabalho se ele contiver sessões ativas.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitações e restrições  
 Se um grupo de cargas de trabalho contiver sessões ativas, a exclusão ou movimentação do grupo de cargas de trabalho para um pool de recursos diferente não terá êxito quando a instrução ALTER RESOURCE GOVERNOR RECONFIGURE for chamada para aplicar a alteração. Para evitar esse problema, é possível executar uma das seguintes ações:  
  
-   Aguardar até que todas as sessões do grupo afetado sejam desconectadas e depois executar novamente a instrução ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
-   Interromper explicitamente as sessões do grupo afetado usando o comando KILL e depois executar novamente a instrução ALTER RESOURCE GOVERNOR RECONFIGURE. Se você decidir que não deseja interromper explicitamente as sessões depois de usar **Excluir** , mas antes de interromper as sessões ativas, recrie o grupo usando o nome original e mova o grupo para o pool de recursos original.  
  
-   Reinicie o servidor. Depois que o processo de reinicialização estiver concluído, o grupo excluído não será criado e um grupo movido usará a atribuição do novo pool de recursos.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Excluir um grupo de cargas de trabalho exige permissão CONTROL SERVER.  
  
##  <a name="delete-a-workload-group-using-object-explorer"></a><a name="DelWGObjEx"></a> Excluir um grupo de cargas de trabalho usando o Pesquisador de Objetos  
 **Para excluir um grupo de cargas de trabalho usando o Pesquisador de Objetos**  
  
1.  No[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e expanda recursivamente o nó **Gerenciamento** para baixo e inclua o **Pools de Recursos**.  
  
2.  Expanda recursivamente o nó **Pools de Recursos** para baixo e incluindo o nó **Grupos de Cargas de Trabalho** no pool de recursos que contém o grupo de cargas de trabalho a ser excluído.  
  
3.  Clique com o botão direito do mouse em grupo de cargas de trabalho e clique em **Excluir**.  
  
4.  Na janela **Excluir Objeto** , o grupo de carga de trabalho é listado em **Objeto a ser excluído** . Para excluir o grupo de cargas de trabalho, clique em **OK**.  
  
##  <a name="delete-a-workload-group-using-resource-governor-properties"></a><a name="DelWGRGProp"></a> Excluir um grupo de cargas de trabalho usando propriedades do administrador de recursos  
 **Para excluir um grupo de cargas de trabalho usando a página de propriedades do administrador de recursos**  
  
1.  No Pesquisador de Objetos, expanda recursivamente o nó **Gerenciamento** para baixo e incluindo **Pools de Recursos**.  
  
2.  Clique com o botão direito do mouse no pool de recursos que contém o grupo de cargas de trabalho a ser excluído e clique em **Propriedades**. Isso abre a página **Propriedades do Administrador de Recursos** .  
  
3.  Na janela **Grupos de cargas de trabalho para o pool de recursos** , clique na linha do grupo de cargas de trabalho a ser excluído, clique com o botão direito do mouse na seta para a direita no lado esquerdo da linha e clique em **Excluir**.  
  
4.  Para excluir o grupo de cargas de trabalho, clique em **OK**.  
  
##  <a name="delete-a-workload-group-using-transact-sql"></a><a name="DelWGTSQL"></a> Excluir grupo de cargas de trabalho usando Transact-SQL  
 **Para mover um grupo de cargas de trabalho usando Transact-SQL**  
  
1.  Execute a instrução **DROP WORKLOAD GROUP** especificando o nome do grupo de cargas de trabalho a ser excluído.  
  
2.  Antes de emitir a instrução **ALTER RESOURCE GOVERNOR RECONFIGURE** , verifique se não há solicitações ativas no grupo de cargas de trabalho a ser excluído. Se houver solicitações ativas, **ALTER RESOURCE GOVERNOR** apresentará falha. Para evitar esse problema, é possível executar uma das seguintes ações:  
  
    -   Aguarde até que todas as sessões do grupo de carga de trabalho estejam desconectadas.  
  
    -   Explicitamente pare sessões no grupo de carga de trabalho usando o comando **KILL** .  
  
    -   Reinicie o servidor. O grupo de cargas de trabalho não será recriado.  
  
    -   Em um cenário no qual você emitiu a instrução **DROP WORKLOAD GROUP** , mas decide que não deseja interromper sessões explicitamente para aplicar a mudança, é possível recriar o grupo usando o mesmo nome que ele tinha antes de você emitir a instrução DROP e depois mover o grupo para o pool de recursos original.  
  
3.  Execute a instrução **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Exemplo (Transact-SQL)  
 O seguinte exemplo descarta um grupo de carga de trabalho denominado `groupAdhoc`.  
  
```  
DROP WORKLOAD GROUP groupAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Criar um pool de recursos](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Criar um grupo de carga de trabalho](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [Excluir um pool de recursos](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
