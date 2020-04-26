---
title: Criar uma dimensão de tempo gerando uma tabela de tempo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- time periods [Analysis Services]
- range-based time dimensions [Analysis Services]
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- table-based time dimensions [Analysis Services]
ms.assetid: 58303326-1361-4c0e-9f3d-642ce69c4f6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b54bfbdb03f6f2220cf66cb988456b2e6e6a0070
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66076287"
---
# <a name="create-a-time-dimension-by-generating-a-time-table"></a>Criar uma dimensão de tempo ao gerar uma tabela de tempo
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode usar o assistente para dimensões [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no para criar uma dimensão de tempo quando nenhuma tabela de tempo estiver disponível no banco de dados de origem. Você faz isso selecionando uma das opções a seguir na página **Selecionar Método de Criação** :  
  
-   **Gerar uma tabela de tempo na fonte de dados** Selecione esta opção quando você tiver permissões para criar objetos na fonte de dados subjacente. O assistente gerará uma tabela de tempo e, em seguida, armazenará essa tabela na fonte de dados. O assistente cria a dimensão de tempo a partir dessa tabela de tempo.  
  
-   **Gerar uma tabela de tempo no servidor** Selecione esta opção quando você não tiver permissões para criar objetos na fonte de dados subjacente. O assistente gerará e armazenará uma tabela no servidor, em vez de na fonte de dados. (A dimensão criada por meio de uma tabela de tempo no servidor é chamada de *dimensão de tempo do servidor*.) O assistente cria a dimensão de tempo do servidor a partir dessa tabela.  
  
 Ao criar uma dimensão de tempo, você especifica os períodos de tempo e também as datas de início e término para as dimensões. O assistente usa os períodos de tempo especificados para criar os atributos de tempo. Ao processar a dimensão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gera e armazena os dados necessários para suportar as datas e períodos especificados. O assistente usa os atributos criados para uma dimensão de tempo para recomendar hierarquias para a dimensão. As hierarquias refletem as relações entre períodos de tempo diferentes e considera os diferentes calendários. Por exemplo, em uma hierarquia de calendário padrão, o nível Semanas aparece abaixo do nível Anos, mas não abaixo do nível Meses, porque as semanas se dividem uniformemente no ano, mas não em meses. Por outro lado, na hierarquia de calendário de fabricação ou relatório, as semanas se dividem uniformemente em meses, então o nível Semanas aparece abaixo do nível Meses.  
  
## <a name="define-time-periods"></a>Definir períodos de tempo  
 Você utilizará a página **Definir Períodos de Tempo** do assistente para especificar o intervalo de datas que deseja incluir na dimensão. Você pode, por exemplo, selecionar um intervalo que inicie em 1 de janeiro do ano mais recente nos seus dados e que termine um ou dois anos após o ano atual (para permitir transações futuras). As transações que estão fora do intervalo não aparecem ou aparecem como membros desconhecidos na dimensão, dependendo da configuração da propriedade `UnknownMemberVisible` da dimensão. Também é possível alterar o primeiro dia da semana usado por seus dados (o padrão é domingo).  
  
 Selecione os períodos de tempo para utilizar quando o assistente criar as hierarquias aplicadas aos seus dados, tais como Anos, Semestres, Trimestres, Meses, Dez Dias, Semanas ou Data. Você sempre deve selecionar pelo menos o período de tempo Data. O atributo Data é o principal atributo para a dimensão, que não pode funcionar sem ele.  
  
 Em seguida, em **Idioma dos nomes de membro de tempo**, selecione o idioma a ser usado para identificar os membros da dimensão.  
  
 Depois de criar uma dimensão de tempo com base em um intervalo de datas, você pode utilizar o Designer de Dimensão para adicionar ou remover atributos de tempo. Como o atributo Data é o principal atributo para a dimensão, você não pode removê-lo da dimensão. Para ocultar o atributo Data dos usuários, você pode alterar a propriedade `AttributeHierarchyVisible` no atributo para `False`.  
  
## <a name="select-calendars"></a>Selecione os calendários  
 O calendário padrão (Gregoriano) de 12 meses, começando em 1 de janeiro e terminando em 31 de dezembro, é sempre incluído quando você cria uma dimensão de tempo. Na página **Selecionar Calendários** do assistente, você pode especificar calendários adicionais nos quais as hierarquias na dimensão se baseiam. Para obter descrições dos tipos de calendário, consulte [Criar uma dimensão de tipo de data](database-dimensions-create-a-date-type-dimension.md).  
  
 Dependendo dos períodos de tempo selecionados na página **Definir Períodos de Tempo** do assistente, as seleções de calendário determinam os atributos criados na dimensão. Por exemplo, se você selecionar os períodos **Ano** e **Trimestre** na página **Definir Períodos de Tempo** do assistente e selecionar **Calendário fiscal** na página **Selecionar Calendários** , os atributos FiscalYear, FiscalQuarter e FiscalQuarterOfYear serão criados para o calendário fiscal.  
  
 O assistente também cria hierarquias específicas do calendário, compostas pelos atributos criados para o calendário. Para todo calendário, cada nível de cada hierarquia se acumula no nível acima dele. Por exemplo, no calendário padrão de 12 meses, o assistente cria uma hierarquia de Anos e Semanas ou Anos e Meses. Porém, as semanas de um calendário padrão não estão contidas uniformemente dentro dos meses, então não há hierarquia de Anos, Meses e Semanas. Por outro lado, as semanas de um calendário de relatório ou fabricação estão divididas uniformemente dentro dos meses, então nesses calendários as semanas se acumulam em meses.  
  
## <a name="completing-the-dimension-wizard"></a>Concluindo o Assistente para Dimensões  
 Na página **Concluindo o Assistente** , verifique os atributos e hierarquias criados pelo assistente e, em seguida, nomeie a dimensão de tempo. Clique em **Concluir** para concluir o assistente e criar a dimensão. Após a conclusão da dimensão, você pode alterá-la usando o Designer de Dimensão.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições da fonte de dados em modelos multidimensionais](data-source-views-in-multidimensional-models.md)   
 [Criar uma dimensão de tipo de data](database-dimensions-create-a-date-type-dimension.md)   
 [Propriedades da dimensão do banco de dados](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [Relações de dimensão](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Criar uma dimensão usando uma tabela existente](create-a-dimension-by-using-an-existing-table.md)   
 [Criar uma dimensão ao gerar uma tabela que não seja de tempo na fonte de dados](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
