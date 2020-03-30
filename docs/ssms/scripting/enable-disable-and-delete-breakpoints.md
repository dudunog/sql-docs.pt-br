---
title: Habilitar, desabilitar e excluir pontos de interrupção
titleSuffix: T-SQL debugger
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 357b5874-273f-43a9-8e30-83872bdea5dc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 72acf04118e0b3b7f3f205a06d6e93e96bf13ecb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75253920"
---
# <a name="enable-disable-and-delete-breakpoints"></a>Habilitar, desabilitar e excluir pontos de interrupção

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Para exibir e gerenciar todos os pontos de interrupção abertos, você pode usar a janela **Pontos de Interrupção** . Use a janela para exibir informações de ponto de interrupção e executar ações como excluir, desabilitar ou habilitar pontos de interrupção.

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]
  
## <a name="the-breakpoints-window"></a>Janela Pontos de Interrupção  
 A janela **Pontos de Interrupção** lista informações como a linha de código em que o ponto de interrupção é localizado. Na janela **Pontos de Interrupção** , você também pode excluir, desabilitar e habilitar pontos de interrupção. Para obter mais informações sobre a janela **Pontos de Interrupção** , consulte [Pontos de Interrupção Window](../../relational-databases/scripting/transact-sql-debugger-breakpoints-window.md).  
  
 A desabilitação de um ponto de interrupção impede a pausa da execução, mas deixa a definição no local caso você deseje habilitar o ponto de interrupção mais tarde. A exclusão de um ponto de interrupção remove isso permanentemente. Você deve alternar um novo ponto de interrupção para pausar execução na instrução.  
  
## <a name="to-open-the-breakpoints-window"></a>Para abrir a janela Pontos de Interrupção  
 **To open the Breakpoints window**  
  
 Você pode abrir a janela **Pontos de Interrupção** de uma das seguintes maneiras:  
  
-   No menu **Depurar** , clique em **Janelas**e em **Pontos de Interrupção**.  
  
-   Na barra de ferramentas **Depurar** , clique no botão **Pontos de Interrupção** .  
  
-   Pressione CTRL+ALT+B.  
  
## <a name="to-disable-a-single-breakpoint"></a>Para desabilitar um único ponto de interrupção  
 **To disable a single breakpoint**  
  
 Você pode desabilitar um único ponto de interrupção de uma das seguintes maneiras:  
  
-   Na janela Editor de Consultas, clique com o botão direito do mouse no ponto de interrupção e clique em **Desabilitar Ponto de Interrupção**.  
  
-   Na janela Pontos de Interrupção, desmarque a caixa de seleção à esquerda do ponto de interrupção.  
  
## <a name="to-disable-all-breakpoints"></a>Para desabilitar todos os pontos de interrupção  
 **To disable all breakpoints**  
  
 Você pode desabilitar todos os pontos de interrupção de uma das seguintes maneiras:  
  
-   No menu **Depurar** , clique em **Desabilitar Todos os Pontos de Interrupção**.  
  
-   Na barra de ferramentas da janela **Pontos de Interrupção** , clique no botão **Desabilitar Todos os Pontos de Interrupção** .  
  
## <a name="to-enable-a-single-breakpoint"></a>Para habilitar um único ponto de interrupção  
 **To enable a single breakpoint**  
  
 Você pode habilitar um único ponto de interrupção de uma das seguintes maneiras:  
  
-   Na janela Editor de Consultas, clique com o botão direito do mouse no ponto de interrupção e clique em **Habilitar Ponto de Interrupção**.  
  
-   Na janela Pontos de Interrupção, clique na caixa à esquerda do ponto de interrupção.  
  
## <a name="to-enable-all-breakpoints"></a>Para habilitar todos os pontos de interrupção  
 **To enable all breakpoints**  
  
 Você pode habilitar todos os pontos de interrupção de uma das seguintes maneiras:  
  
-   No menu **Depurar** , clique em **Habilitar Todos os Pontos de Interrupção**.  
  
-   Na barra de ferramentas da janela **Pontos de Interrupção** , clique no botão **Habilitar Todos os Pontos de Interrupção** .  
  
## <a name="to-delete-a-single-breakpoint"></a>Para excluir um único ponto de interrupção  
 **To delete a single breakpoint**  
  
 Você pode excluir um único ponto de interrupção de uma das seguintes maneiras:  
  
-   Na janela Editor de Consultas, clique com o botão direito do mouse no ponto de interrupção e clique em **Excluir Ponto de Interrupção**.  
  
-   Na janela Pontos de Interrupção, clique com o botão direito do mouse no ponto de interrupção e em **Excluir** no menu de atalho.  
  
-   Na janela Pontos de Interrupção, selecione o ponto de interrupção e pressione DELETE.  
  
## <a name="to-delete-all-breakpoints"></a>Para excluir todos os pontos de interrupção  
 **To delete all breakpoints**  
  
 Você pode excluir todos os pontos de interrupção de uma das seguintes maneiras:  
  
-   No menu **Depurar** , clique em **Excluir Todos os Pontos de Interrupção**.  
  
-   Na barra de ferramentas da janela **Pontos de Interrupção** , clique no botão **Excluir Todos os Pontos de Interrupção** .  
  
## <a name="see-also"></a>Consulte Também  
 [Alternar um ponto de interrupção](../../relational-databases/scripting/toggle-a-breakpoint.md)  
  
  
