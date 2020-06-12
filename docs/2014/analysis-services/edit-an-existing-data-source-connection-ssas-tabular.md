---
title: Editar uma conexão de fonte de dados existente (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.selexistconn.f1
ms.assetid: 97e63f18-a01d-4c91-a411-e7e6d40a0647
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1dd8ac9a27d1bcf46ba14b5f49fee3cc9b3b3b4e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528452"
---
# <a name="edit-an-existing-data-source-connection-ssas-tabular"></a>Editar uma conexão de fonte de dados existente (SSAS tabular)
  Este tópico descreve como editar as propriedades de uma conexão de fonte de dados existentes em um modelo tabular.  
  
 Depois de criar uma conexão com uma fonte de dados externa, você poderá modificá-la destas maneiras:  
  
-   Você pode alterar as informações da conexão, inclusive o arquivo, o feed ou o banco de dados usado como fonte, suas propriedades ou outras opções de conexão específicas do provedor.  
  
-   Você pode alterar os mapeamentos de coluna e tabela, e remove referências a colunas que já não são mais usadas.  
  
-   Você pode alterar as tabelas, exibições ou colunas que obtém da fonte de dados externa.  
  
## <a name="modify-a-connection"></a>Modificar uma conexão  
 Este procedimento descreve como modificar uma conexão de fonte de dados de banco de dados. Algumas opções para trabalhar com fontes de dados diferem dependendo do tipo de fonte de dados; porém, você deve poder identificar essas diferenças facilmente.  
  
#### <a name="to-change-the-external-data-source-used-by-a-current-connection"></a>Para alterar a fonte de dados externa usada por uma conexão atual  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Conexões Existentes**.  
  
2.  Selecione a conexão de fonte de dados que você deseja modificar e clique em **Editar**.  
  
3.  Na caixa de diálogo **Editar Conexão** , clique em **Procurar** para localizar outro banco de dados do mesmo tipo, mas com um nome ou local diferente.  
  
     Assim que você alterar o arquivo de banco de dados, será exibida uma mensagem indicando que é necessário salvar e atualizar as tabelas para ver os novos dados.  
  
4.  Clique em **Salvar**e em **Fechar**.  
  
5.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no **Modelo**, em **Processar**e em **Processar Tudo**.  
  
     As tabelas são reprocessadas usando a nova fonte de dados, mas com as seleções de dados originais.  
  
    > [!NOTE]  
    >  Se a nova fonte de dados contiver tabelas adicionais que não estavam presentes na fonte de dados original, você deverá reabrir a conexão alterada e adicionar as tabelas.  
  
## <a name="edit-table-and-column-mappings-bindings"></a>Editar mapeamentos de coluna e tabela (associações)  
 Este procedimento descreve como editar os mapeamentos depois que você alterar uma fonte de dados.  
  
#### <a name="to-edit-column-mappings-when-a-data-source-changes"></a>Para editar mapeamentos de coluna quando uma fonte de dados é alterada  
  
1.  No Designer de Modelo, selecione uma tabela.  
  
2.  Clique no menu **Tabela** e clique em **Propriedades da Tabela**.  
  
     O nome da tabela selecionada é exibido na caixa **Nome da Tabela** . A caixa **Nome da Origem** contém o nome da tabela na fonte de dados externa. Se as colunas forem nomeadas diferentemente na origem e no modelo, você poderá alternar entre os dois conjuntos de nomes de colunas selecionando a opção **Origem** ou **Modelo**.  
  
3.  Para alterar a tabela usada como uma fonte de dados, em **Nome da Origem**, selecione uma tabela diferente da atual.  
  
4.  Altere os mapeamentos de coluna se necessário:  
  
    1.  Para adicionar colunas que estão presentes na origem mas não no modelo, marque a caixa de seleção ao lado do nome da coluna.  
  
         Os dados reais serão carregados no modelo na próxima vez que você atualizá-la.  
  
    2.  Se algumas colunas no modelo não estiverem mais disponíveis na fonte de dados atual, será exibida uma mensagem na área de notificação listando as colunas inválidas. Não é necessário fazer mais nada.  
  
5.  Clique em **Salvar** para aplicar as alterações ao modelo.  
  
     Quando você salvar o conjunto atual de propriedades de tabela, uma mensagem poderá aparecer indicando que você precisa processar as tabelas. Clique em **Processar** para carregar dados atualizados no modelo.  
  
## <a name="see-also"></a>Consulte Também  
 [Processar dados &#40;SSAS de tabela&#41;](process-data-ssas-tabular.md)   
 [Fontes de dados com suporte &#40;SSAS de Tabela&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
