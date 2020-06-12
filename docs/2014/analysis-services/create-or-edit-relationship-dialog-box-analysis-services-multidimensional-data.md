---
title: Caixa de diálogo criar ou editar relação (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.createrelationship.f1
helpviewer_keywords:
- Create Relationship dialog box
ms.assetid: da3c7074-623e-4ddf-a707-d3276a47cf1c
author: minewiskan
ms.author: owend
ms.openlocfilehash: b18a0b6c79a3787af4a55a473e5203daf9c7308f
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526476"
---
# <a name="create-or-edit-relationship-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Criar ou Editar Relação (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Criar/Editar Relação** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir ou modificar uma relação em uma exibição da fonte de dados. É possível exibir a caixa de diálogo **Criar/Editar Relação** das seguintes maneiras:  
  
-   Clicando em **Nova Relação** no painel **Barra de Ferramentas** do **Designer de Exibição da Fonte de Dados**.  
  
-   Clicando com o botão direito do mouse em uma tabela no painel **Tabelas** ou **Diagrama** do **Designer de Exibição da Fonte de Dados** e selecionando **Nova Relação**.  
  
-   Clicando com o botão direito do mouse em uma relação no painel **Diagrama** do **Designer de Exibição da Fonte de Dados** e selecionando **Explorar Relação**.  
  
> [!NOTE]  
>  Você pode criar relações no **Designer de exibição da fonte de dados** que não existem na fonte de dados subjacente e remover relações criadas pelo **Designer de exibição da fonte de dados** de relações de chave estrangeira existentes na fonte de dados subjacente.  
  
## <a name="options"></a>Opções  
 **Tabela de origem (chave estrangeira)**  
 Selecione a tabela ou consulta nomeada que contém a referência a uma ou mais colunas na tabela de destino.  
  
 **Tabela de destino (chave primária)**  
 Selecione a tabela que contém uma ou mais colunas referenciadas pela tabela de origem. Para autojunções, selecione a mesma tabela selecionada em **Tabela de origem (chave estrangeira)**.  
  
 **Colunas de origem**  
 Selecione as colunas que referenciam colunas na tabela de dimensões.  
  
 **Colunas de destino**  
 Selecione as colunas que são referenciadas pelas colunas na tabela de origem.  
  
 **Ordem**  
 Clique para inverter a direção da relação.  
  
 **Descrição**  
 Digite uma descrição opcional para a relação.  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Designer de Exibição da Fonte de Dados &#40;Analysis Services – Dados multidimensionais&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
