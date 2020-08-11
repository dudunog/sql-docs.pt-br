---
title: Trabalhando com conjuntos de dados compartilhados (portal da Web) | Microsoft Docs
description: Veja e gerencie as propriedades de um conjunto de dados compartilhado no portal da Web. Use o portal da Web para criar ou editar conjuntos de dados compartilhados no Construtor de Relatórios.
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 2641ea84-9343-4e6f-aec1-25339031b163
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0d37e617ef7dcb4c63b7d2239881cc6cb96c7c2f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243593"
---
# <a name="work-with-shared-datasets---web-portal"></a>Trabalhar com conjuntos de dados compartilhados – portal da Web

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Com um conjunto de dados compartilhado, você pode gerenciar as configurações de um conjunto de dados separadamente dos relatórios e outros itens de catálogo que o usam. Os conjuntos de dados compartilhados podem ser usados com relatórios paginados e móveis, juntamente com os KPIs.

Você pode exibir e gerenciar as propriedades de um conjunto de dados compartilhado dentro do portal da Web. O portal da Web pode iniciar o Construtor de Relatórios para criar ou editar conjuntos de dados compartilhados.

## <a name="create-a-shared-dataset"></a>Criar um conjunto de dados compartilhado
  
Para criar um novo conjunto de dados compartilhado, você pode fazer o seguinte.  
  
1.  Selecione Novo na barra de menus.  
  
2.  Selecione **Conjunto de dados**.  
  
    ![ssRSDataset-NewDataset](../reporting-services/media/ssrsdataset-newdataset.png)  
  
3.  Isso iniciará o Construtor de Relatórios ou solicitará que você o baixe.  
  
4.  Na caixa de diálogo **Novo Relatório ou Conjunto de Dados** , selecione uma conexão de fonte de dados a ser usada para esse conjunto de dados. Talvez seja necessário navegar até o local da fonte de dados compartilhada.  
  
5.  Selecione **Criar**.  
  
6.  Crie seu conjunto de dados e selecione o ícone **Salvar** no canto superior esquerdo para salvar o conjunto de dados de volta no servidor de relatório.  
  
## <a name="manage-an-existing-shared-dataset"></a>Gerenciar um conjunto de dados compartilhado existente
  
Para gerenciar um conjunto de dados compartilhado existente, você pode fazer o seguinte.  
  
> [!NOTE]
> Se o conjunto de dados compartilhado não estiver na pasta, verifique se os conjuntos de dados estão sendo exibidos. Você pode selecionar **Modo de Exibição** na barra de menus na parte superior direita do portal da Web. Certifique-se de que **Conjuntos de dados** esteja marcado.  
  
1.  Selecione as **reticências (...)** do conjunto de dados que deseja gerenciar.  
  
    ![ssRSDataset-Ellipse](../reporting-services/media/ssrsdataset-ellipse.png)  
  
2.  Selecione **Gerenciar** , o que levará você até a tela de edição.  
  
    ![ssRSDataset-Manage](../reporting-services/media/ssrsdataset-manage.png)  
  
## <a name="properties"></a>Propriedades
  
Na tela de propriedades, você pode alterar o **nome** a e **descrição** do conjunto de dados. Você também pode **Excluir**, **Mover**, **Editar no Construtor de Relatórios**, **Baixar** ou **Substituir**.  
  
![ssRSdataset-Properties](../reporting-services/media/ssrsdataset-properties.png)  
  
## <a name="caching"></a>Cache
  
Quando o assunto é armazenar dados em cache para um conjunto de dados, há opções. Você começará com uma simples seleção.  
  
1.  **Sempre executar este relatório com os dados mais recentes** emitirá as consultas à fonte de dados quando for solicitado.  
  
2.  **Armazenar cópias deste relatório em cache e utilizá-las quando disponíveis** colocará uma cópia temporária dos dados em um cache para uso com os itens que usam esse conjunto de dados. O cache normalmente melhora o desempenho porque os dados são retornados do cache, em vez de haver uma nova execução da consulta de conjunto de dados.  
  
![ssRSDataset-Caching1](../reporting-services/media/ssrsdataset-caching1.png)  
  
A seleção de **Armazenar cópias deste relatório em cache e utilizá-las quando disponíveis** apresentará algumas opções adicionais.  
  
![ssRSDataset-Caching2](../reporting-services/media/ssrsdataset-caching2.png)  
  
### <a name="cache-expiration"></a>Validade do cache  
  
Você pode controlar se deseja expirar o cache do conjunto de dados compartilhados após um determinado período, ou se prefere fazer isso com base em uma agenda. Você pode usar uma agenda compartilhada  
  
![ssRSDataset-Caching3](../reporting-services/media/ssrsdataset-caching3.png)  
  
> [!NOTE]
> A configuração de uma expiração não atualiza o cache. Sem um plano de atualização de cache, os dados serão atualizados na próxima execução do conjunto de dados.  
  
### <a name="cache-refresh-plans"></a>Planos de atualização do cache  
  
Você pode usar os Planos de Atualização do Cache para criar agendas de pré-carregamento do cache com cópias temporárias de dados para um conjunto de dados compartilhado. Um plano de atualização inclui uma agenda e a opção para especificar ou substituir valores de parâmetros. Você não pode substituir valores de parâmetros que estão marcados como somente leitura. Você pode criar e usar mais de um plano de atualização.   
  
As atribuições padrão de função que permitem adicionar, excluir e alterar conjuntos de dados compartilhados para planos de atualização de cache são Gerenciador de Conteúdo, Meus Relatórios e Publicador.  
  
Depois de aplicar a opção de cache acima, você pode definir um plano de atualização do cache. Para fazer isso, escolha o link **Gerenciar Planos de Atualização** que aparece depois de aplicar as configurações de cache. Isso o levará até a página de plano de atualização do cache.   
  
Para criar um novo plano de atualização de cache, escolha **Novo Plano de Atualização do Cache**. Em seguida, você pode inserir um nome para o plano e especificar uma agenda. Se o conjunto de dados tiver parâmetros definidos, você verá os listados e será capaz de fornecer valores, a menos que estejam marcados como somente leitura.  
  
Quando terminar, selecione **Criar Plano de Atualização do Cache**.  
  
![ssRSDataset-Caching4](../reporting-services/media/ssrsdataset-caching4.png)  
  
> [!NOTE]
> O SQL Server Agent precisa estar em execução para criar um plano de atualização do cache.  
  
Em seguida, você pode **Editar** ou **Excluir** os planos listados. A opção **Novo Com Base Em Existente** é habilitada quando um, e apenas um, plano de atualização do cache for selecionado. Essa opção criará um novo plano de atualização que é copiado do plano original. A página Plano de Atualização do Cache é aberta pré-populada com detalhes do plano que foi selecionado. Você pode modificar as opções do plano de atualização e salvar o plano com uma nova descrição.  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
