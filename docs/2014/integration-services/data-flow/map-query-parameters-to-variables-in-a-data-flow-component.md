---
title: Mapear parâmetros de consulta para variáveis em um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d2d9c9470364c13380751e3e7aca1fef13973a76
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432003"
---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>Mapear parâmetros de consulta para variáveis em um componente de fluxo de dados
  Quando você configura a fonte OLE DB para usar consultas parametrizadas, pode mapear os parâmetros para variáveis.  
  
 As fontes OLE DB usam consultas parametrizadas para filtrar dados quando a fonte conecta-se a uma fonte de dados.  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>Para mapear um parâmetro de consulta para uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a fonte OLE DB para a superfície de design.  
  
4.  Clique com o botão direito do mouse na fonte OLE DB e, depois, clique em **Editar**.  
  
5.  Em **Editor de Origem OLE DB**, selecione um gerenciador de conexões para usar para conectar-se à fonte de dados ou clique em **Novo** para criar um novo gerenciador de conexões OLE DB.  
  
6.  Selecione a opção de **Comando SQL** para o modo de acesso a dados e, então, digite uma consulta parametrizada no painel **Texto de comando SQL** .  
  
7.  Clique em **Parâmetros**.  
  
8.  Na caixa de diálogo **definir parâmetros de consulta** , mapeie cada parâmetro na lista de **parâmetros** para uma variável na lista de **variáveis** ou crie uma nova variável clicando em **\<New variable>** . Clique em **OK**.  
  
    > [!NOTE]  
    >  Apenas as variáveis do sistema e as variáveis definidas pelo usuário que estão no escopo do pacote, um contêiner pai como Loop Foreach ou a tarefa de Fluxo de Dados que contém o componente de fluxo de dados, estão disponíveis para mapeamento. A variável deve ter um tipo de dados que seja compatível com a coluna na cláusula WHERE, para a qual o parâmetro é designado.  
  
9. Você pode clicar em **Visualizar** para exibir até 200 linhas dos dados que a consulta retorna.  
  
10. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Origem de OLE DB](ole-db-source.md)   
 [Transformação Pesquisa](transformations/lookup-transformation.md)  
  
  
