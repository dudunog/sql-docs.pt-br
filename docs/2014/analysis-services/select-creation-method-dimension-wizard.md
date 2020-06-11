---
title: Selecionar método de criação (Assistente para dimensões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensiondefinition.f1
ms.assetid: 291b0b2d-a03a-4df6-82f7-90ad92d4d1cf
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6cc05e073bdb57033e4e618eb85a9c04fda76f5d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84538208"
---
# <a name="select-creation-method-dimension-wizard"></a>Selecionar Método de Criação (Assistente para Dimensões)
  Use a página **Selecionar Método de Criação** para selecionar como criar a dimensão.  
  
 **Para abrir o Assistente para Dimensões**  
  
-   No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Dimensões** de um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique em **Nova Dimensão**.  
  
## <a name="options"></a>Opções  
 **Usar uma tabela existente**  
 Crie uma dimensão a partir de uma ou mais tabelas em uma fonte de dados. Os atributos que estão disponíveis para a dimensão dependerão da estrutura dos dados na tabela.  
  
 Para obter mais informações, consulte [Criar uma dimensão usando uma tabela existente](multidimensional-models/create-a-dimension-by-using-an-existing-table.md).  
  
 **Gerar uma tabela de tempo na fonte de dados**  
 Crie uma tabela de tempo na fonte de dados subjacente e então use essa tabela para criar uma dimensão de tempo. Use esta opção quando nenhuma tabela dessas existir e você não quiser usar um script para criar uma. A nova tabela de tempo conterá dados para o intervalo de datas, atributos e calendários que você especificar no assistente.  
  
> [!NOTE]  
>  Para usar esta opção, você deve ter permissão para criar objetos na fonte de dados subjacente. Se você não tiver permissão para criar objetos na fonte de dados, tente em vez disso usar a opção **Gerar uma tabela de tempo no servidor** .  
  
 Para obter mais informações, consulte [Criar uma dimensão temporal gerando uma tabela de tempo](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md).  
  
 **Gerar uma tabela de tempo no servidor**  
 Crie uma tabela de tempo diretamente no servidor e então use essa tabela para criar uma dimensão de tempo. Use esta opção se você não tem permissão para criar objetos na fonte de dados subjacente. A nova dimensão de tempo conterá dados para o intervalo de datas, atributos e calendários que você especificar no assistente.  
  
 Para obter mais informações, consulte [Criar uma dimensão temporal gerando uma tabela de tempo](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md).  
  
 **Gerar uma tabela que não seja de tempo na fonte de dados**  
 Crie a dimensão sem uma fonte de dados relacional subjacente e então gere o esquema necessário para a fonte de dados. Esta abordagem é conhecida como modelagem de cima para baixo.  
  
> [!NOTE]  
>  Para usar esta opção, você deve ter permissão para criar objetos na fonte de dados subjacente.  
  
 Você pode construir a dimensão com ou sem um modelo. Para construir a dimensão com um modelo, selecione o modelo da lista **Modelo** .  
  
 Para obter mais informações, consulte [Criar uma dimensão gerando uma tabela que não seja de tempo na fonte de dados](multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md).  
  
 **Modelo**  
 Selecione o modelo que deseja usar para criar a dimensão. Os modelos oferecem um conjunto completo de atributos e definições de hierarquia orientado a um propósito empresarial específico.  
  
> [!NOTE]  
>  Esta opção só está disponível quando a opção **Gerar uma tabela que não seja de tempo na fonte de dados** tiver sido marcada.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente para dimensões](dimension-wizard-f1-help.md)   
 [Dimensões &#40;Analysis Services de dados multidimensionais&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensões em modelos multidimensionais](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
