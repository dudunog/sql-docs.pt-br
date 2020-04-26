---
title: Criar uma dimensão usando o assistente para dimensões | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], creating
ms.assetid: d84f66ae-7551-49bf-99d0-88368ca2dd0e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e23d4af96b5ce7c740f1b29893e6ee760104b871
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66076433"
---
# <a name="create-a-dimension-using-the-dimension-wizard"></a>Criar uma dimensão usando o Assistente para Dimensões
  Você pode criar uma nova dimensão usando o Assistente para Dimensões no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-create-a-new-dimension"></a>Para criar uma nova dimensão  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Dimensões**e clique em **Nova Dimensão**.  
  
2.  Na página **Selecionar Método de Criação** do Assistente para Dimensões, selecione **Usar uma tabela existente**e clique em **Avançar**.  
  
    > [!NOTE]  
    >  Ocasionalmente, você pode precisar criar uma dimensão sem usar uma tabela existente. Para obter mais informações, consulte [Criar uma dimensão gerando uma tabela que não seja de tempo na fonte de dados](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md) e [Criar uma dimensão de tempo gerando uma tabela de tempo](create-a-time-dimension-by-generating-a-time-table.md).  
  
3.  Na página **Especificar Informações sobre a Origem** , execute os seguintes procedimentos:  
  
    1.  Na lista **Exibição da fonte de dados** , selecione uma exibição da fonte de dados.  
  
    2.  Na lista **Tabela principal** , selecione a tabela principal de dimensão.  
  
    3.  Na lista **Colunas de Chaves** , examine as colunas de chave que o assistente selecionou automaticamente com base na chave primária definida na tabela principal de dimensão. Para alterar essa configuração padrão, especifique as colunas de chaves que vinculam a tabela de dimensões à tabela de fatos.  
  
    4.  Na lista suspensa **Coluna de Nome** , examine a coluna de nome que o assistente selecionou automaticamente.  
  
         Esse nome padrão é apropriado quando a coluna contém informações descritivas. Porém, convém especificar um nome que contenha valores mais significativos para o usuário final. Por exemplo, se um atributo de categoria de produto em uma dimensão de Produtos usar a coluna **ProductCategoryKey** como sua coluna de chaves, você poderá especificar a coluna **ProductCategoryName** como sua coluna de nome.  
  
         Se a lista **Colunas de Chaves** contiver várias colunas de chaves, você deverá especificar uma coluna de nome que forneça os valores de membro para o atributo de chave. Para fazer isso, você pode criar um cálculo nomeado na exibição da fonte de dados e usá-lo como a coluna de nome.  
  
    5.  Clique em **Avançar**.  
  
4.  Na página **Selecionar Tabelas Relacionadas** , selecione as tabelas relacionadas que você quer incluir em sua dimensão e clique em **Avançar**.  
  
    > [!NOTE]  
    >  A página **Selecionar Tabelas Relacionadas** será exibida se a tabela principal de dimensão especificada tiver relações com outras tabelas de dimensão.  
  
5.  Na página **Selecionar Atributos de Dimensão** , selecione os atributos que você quer incluir na dimensão e clique em **Avançar**.  
  
     Opcionalmente, você pode alterar os nomes de atributo, habilitar ou desabilitar a navegação, e especificar o tipo de atributo.  
  
    > [!NOTE]  
    >  Para ativar os campos **Habilitar Navegação** e **Tipo de Atributo** de um atributo, o atributo deve ser selecionado para inclusão na dimensão.  
  
6.  Na página **Definir Inteligência de Conta** , na coluna **Tipos de Conta Interna** , selecione o tipo de conta e clique em **Avançar**.  
  
     O tipo de conta deve corresponder ao tipo de conta da tabela de origem que está listada na coluna **Tipos de Conta de Tabela de Origem** .  
  
    > [!NOTE]  
    >  A página **Definir Inteligência de Conta** aparecerá se você definir um atributo de dimensão **Tipo de Conta** na página **Selecionar Atributos da Dimensão** do assistente.  
  
7.  Na página **Concluindo o Assistente** , digite um nome para a nova dimensão e examine a estrutura da dimensão. Se você quiser fazer mudanças, clique em **Voltar**; caso contrário, clique em **Concluir**.  
  
    > [!NOTE]  
    >  Você pode usar o Designer de Dimensão depois de concluir o Assistente para Dimensões para adicionar, remover, e configurar atributos e hierarquias na dimensão.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma dimensão usando uma tabela existente](create-a-dimension-by-using-an-existing-table.md)  
  
  
