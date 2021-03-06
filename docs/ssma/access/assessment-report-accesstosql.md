---
description: Relatório de avaliação (AccessToSQL)
title: Relatório de avaliação (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6c747f50c9216626e710318175cf5e53a0624d7a
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987652"
---
# <a name="assessment-report-accesstosql"></a>Relatório de avaliação (AccessToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco de dados em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe e também pode ajudá-lo a estimar a complexidade e o custo de seus projetos de migração.  
  
Para criar um relatório de avaliação, selecione objetos a serem convertidos no Gerenciador de metadados de origem, clique com o botão direito do mouse em **bancos de dados**e selecione **criar relatório**. Você também pode exibir esse relatório automaticamente depois de converter esquemas. No entanto, o nome do relatório será relatório de conversão. Para obter mais informações, consulte [configurações do projeto (GUI) (SSMA Common)](../sybase/project-settings-gui-sybasetosql.md).  
  
## <a name="options"></a>Opções  
**Painel Explorer**  
Contém uma hierarquia de objetos no relatório de avaliação. Expanda pastas para exibir objetos individuais e subcomponentes. Quando você clica em uma categoria ou objeto, as estatísticas de conversão para essa categoria ou objeto aparecem no painel de detalhes.  
  
**Painel de detalhes**  
Mostra as estatísticas de conversão ou mensagens de erro e de aviso para o objeto selecionado. Por exemplo, se a pasta tabelas estiver selecionada, o painel detalhes mostrará os números de chaves estrangeiras, índices, chaves primárias e tabelas que foram convertidas.  
  
**painel Mensagens**  
Mostra os erros, avisos e mensagens de informações que foram gerados quando o relatório de avaliação foi criado. As mensagens são agrupadas por número.  
  
Para exibir os detalhes da mensagem, clique em **erros**, **avisos**ou **mensagens**e, em seguida, expanda uma mensagem. O SSMA exibirá a lista de objetos que têm esse erro. Clique em um objeto para exibir todos os detalhes de conversão do objeto.  
  
## <a name="see-also"></a>Consulte Também  
[Referência da interface do usuário (Access)](./user-interface-reference-accesstosql.md)  
