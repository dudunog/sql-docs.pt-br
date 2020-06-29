---
title: Editor de transformação pesquisa (página conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.referencetable.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: e90d6b69-5a26-43c5-8433-5c3c9588e08c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 788075ce45ca09da585fd3675258062ef2e8a054
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440243"
---
# <a name="lookup-transformation-editor-connection-page"></a>Editor da Transformação Pesquisa (página Conexão)
  Use a página **Conexão** da caixa de diálogo **Editor da Transformação Pesquisa** para selecionar um gerenciador de conexões. Se você selecionar um gerenciador de conexões OLE DB, também poderá selecionar uma consulta, tabela ou exibição para gerar o conjunto de dados de referência.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 As opções a seguir estarão disponíveis quando você selecionar **Cache cheio** e **Gerenciador de conexões de cache** na página Geral da caixa de diálogo **Editor da Transformação Pesquisa** .  
  
 **Gerenciador de conexões de cache**  
 Selecione um gerenciador de conexões de cache existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Novo**  
 Crie uma nova conexão usando a caixa de diálogo **Editor de Gerenciador de Conexões de Cache** .  
  
 As opções a seguir estarão disponíveis quando você selecionar **Cache cheio**, **Cache parcial**ou **Sem cache**e **Gerenciador de conexões OLE DB**na página Geral da caixa de diálogo **Editor da Transformação Pesquisa** .  
  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Novo**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Use uma tabela ou exibição**  
 Selecione uma tabela ou exibição existente na lista ou crie uma nova tabela clicando em **novo**.  
  
> [!NOTE]  
>  Se você especificar uma instrução SQL na página **Avançado** do **Editor da Transformação Pesquisa**, essa instrução SQL vai sobrescrever e substituir o nome da tabela selecionada aqui. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;Página Avançado&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md).  
  
 **Novo**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
 **Usar resultados de uma consulta SQL**  
 Escolha esta opção para navegar até uma consulta preexistente, criar uma nova consulta, verificar a sintaxe da consulta e visualizar os resultados da consulta.  
  
 **Compilar consulta**  
 Crie a instrução Transact-SQL a ser executada usando o **Construtor de Consultas**, uma ferramenta gráfica que é usada para criar consultas navegando pelos dados.  
  
 **Procurar**  
 Use esta opção para navegar até uma consulta preexistente salva como um arquivo.  
  
 **Analisar consulta**  
 Verifique a sintaxe da consulta.  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . Esta opção exibe até 200 linhas.  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [Lookup cache modes](https://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de transformação pesquisa &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de transformação pesquisa &#40;página colunas&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Editor de transformação pesquisa &#40;página avançado&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [Editor de transformação pesquisa &#40;página saída de erro&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [transformação Pesquisa Difusa](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
