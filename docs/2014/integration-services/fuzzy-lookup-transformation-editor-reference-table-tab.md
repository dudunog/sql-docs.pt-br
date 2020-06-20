---
title: Editor de transformação pesquisa difusa (guia tabela de referência) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.referencetable.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 451f4e7d-1c8e-4784-b540-df0806509bf1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3efdb863b0a067d3d52405c5caa5a78e85555c62
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966265"
---
# <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>Editor de Transformação Pesquisa Difusa (guia Tabela de Referência)
  Use a guia **Tabela de Referência** da caixa de diálogo **Editor de Transformação Pesquisa Difusa** para especificar a tabela de origem e o índice a ser usado na pesquisa. A fonte de dados de referência deve ser uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  A transformação Pesquisa Difusa cria uma cópia de trabalho da tabela de referência. Os índices descritos abaixo são criados nesta tabela de trabalho usando uma tabela especial, não um índice do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] comum. A transformação não modifica as tabelas de origem existentes a menos que você selecione **Manter índice armazenado**. Nesse caso, ela cria um gatilho na tabela de referência que atualiza a tabela de trabalho e a tabela de índices de pesquisa baseada em alterações na tabela de referência.  
  
> [!NOTE]  
>  As `Exhaustive` Propriedades e `MaxMemoryUsage` da transformação pesquisa difusa não estão disponíveis no **Editor de transformação pesquisa difusa**, mas podem ser definidas usando o **Editor avançado**. Além disso, um valor maior que 100 para `MaxOutputMatchesPerInput` pode ser especificado somente no **Editor avançado**. Para obter mais informações sobre estas propriedades, consulte a seção Transformação de Pesquisa Difusa em [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md).  
  
 Para saber mais sobre a transformação Pesquisa Difusa, consulte [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Novo**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Gerar novo índice**  
 Especifique que a transformação deve criar um índice novo para ser utilizado na pesquisa.  
  
 **Nome da tabela de referência**  
 Selecione a tabela existente para usar como tabela de referência (pesquisa).  
  
 **Armazenar novo índice**  
 Selecione esta opção para salvar o novo índice de pesquisa.  
  
 **Novo nome de índice**  
 Se você optou por salvar o novo índice de pesquisa, digite um nome descritivo para o índice.  
  
 **Manter índice armazenado**  
 Se você optou por salvar o novo índice de pesquisa, especifique se deseja que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mantenha o índice.  
  
> [!NOTE]  
>  Quando você seleciona **Manter índice armazenado** na guia **Tabela de Referência** de **Editor de Transformação Pesquisa Difusa**, a transformação usa procedimentos armazenados gerenciados para manter o índice. Esses procedimentos armazenados gerenciados usam o recurso de integração de CLR (Common Language Runtime) no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por padrão, a integração de CLR no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não está habilitada. Para usar a funcionalidade **Manter índice armazenado** , você deve habilitar a integração de CLR. Para obter mais informações, consulte [Enabling CLR Integration](../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Como a opção **Manter índice armazenado** requer a integração CLR, esse recurso funciona apenas quando você seleciona uma tabela de referência em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em que a integração CLR está habilitada.  
  
 **Usar índice já existente**  
 Especifique que a transformação deve usar um índice existente na pesquisa.  
  
 **Nome de um índice já existente**  
 Selecione um índice de pesquisa criado anteriormente na lista.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformação pesquisa difusa &#40;guia colunas&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Editor de Transformação Pesquisa Difusa &#40;Guia Avançado&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
