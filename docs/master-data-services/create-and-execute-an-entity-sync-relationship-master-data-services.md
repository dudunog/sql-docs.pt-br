---
description: Criar e executar um relacionamento de sincronização de entidade (Master Data Services)
title: Criar e executar um relacionamento de sincronização de entidade
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 0ddceab4-d2b3-4bc1-bd9c-6b852200b414
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6e96975fbd7946c53f60af29a91cec938b0ffeb0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461788"
---
# <a name="create-and-execute-an-entity-sync-relationship-master-data-services"></a>Criar e executar um relacionamento de sincronização de entidade (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  A sincronização de entidade é uma sincronização unidirecional e repetível entre versões da entidade. Ela fornece uma maneira de compartilhar dados de entidade entre diferentes modelos.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Pré-requisitos para criar e executar um relacionamento de sincronização de entidade:  
  
-   Você deve ter permissão para acessar a área funcional Administração do Sistema. Para obter mais informações, consulte [permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ser um administrador de modelo do modelo de destino. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   É necessário ter, pelo menos, acesso de leitura à entidade de origem e a todos os seus atributos e membros.  
  
 Pré-requisitos para executar um relacionamento de sincronização de entidade:  
  
-   Você deve ter permissão para acessar a área funcional Administração do Sistema. Para obter mais informações, consulte [permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ser um administrador de modelo do modelo de destino. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 Durante a criação de um relacionamento de sincronização de entidade.  
  
-   As entidades de origem e de destino devem ser em modelos diferentes.  
  
-   Um status de versão da entidade de destino não deve ser confirmado.  
  
-   Depois que o relacionamento de sincronização é estabelecido, o destino é imediatamente sincronizado com a origem.  
  
-   A versão da entidade de destino não pode ser uma versão da entidade de origem de outro relacionamento de sincronização.  
  
 Durante a execução de um relacionamento de sincronização de entidade, considere o seguinte.  
  
-   Somente membros folha serão copiados  
  
-   Atributos baseados em domínio não serão copiados.  
  
-   Membros excluídos temporários não serão copiados.  
  
-   Sincronização não gera transações/históricos da entidade de destino.  
  
 **Para criar um relacionamento de sincronização de entidade**  
  
1.  No Master Data Manager, clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelos** , na barra de menus, aponte para **Gerenciar** e clique em **Sincronização de Entidades**.  
  
3.  Na página **Manutenção de Sincronização de Entidades** , clique em **Adicionar**. Um painel aparece no lado direito.  
  
4.  Na lista de origem **Modelo** , selecione um modelo.  
  
5.  Na lista de origem **Versão** , selecione uma versão.  
  
6.  Na lista de origem **Entidade** , selecione uma entidade.  
  
7.  Na lista de destino **Modelo** , selecione um modelo.  
  
8.  Na lista de destino **Versão** , selecione uma versão.  
  
9. Escolha **Entidade Existente** e selecione uma entidade na lista de entidades para sincronizar uma entidade existente ou escolha **Nova Entidade** e insira o nome da entidade de destino para sincronizar com uma nova entidade  
  
10. Selecione **Sincronização Sob Demanda**, ou selecione **Sincronização Automática** e configure uma frequência.  
  
11. Clique em **Save** (Salvar).  
  
 **Para executar um relacionamento de sincronização de entidade**  
  
1.  No Master Data Manager, clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelos** , na barra de menus, aponte para **Gerenciar** e clique em **Sincronização de Entidades**.  
  
3.  Na página **Manutenção de Sincronização da Entidade** selecione um relacionamento de sincronização na grade.  
  
4.  Clique em **Executar**.  
  
## <a name="sync-relationship-information"></a>Informações de relacionamento de sincronização  
 Para cada relacionamento de sincronização criado, uma linha com dez colunas é adicionada à grade. A tabela a seguir descreve as colunas.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Status|O status de relacionamento da sincronização.<br /><br /> Quando você clica em **salvar** ou executa uma relação de sincronização, o ![ícone para atualizar a imagem de status](../master-data-services/media/mds-statusicon-updating.png "Ícone para atualizar o status") é exibido, indicando que a relação de sincronização está sendo atualizada.<br /><br /> Se houver erros ao criar, editar ou executar uma relação de sincronização, a imagem ![ícone para o status de erro](../master-data-services/media/mds-statusicon-error.png "Ícone para status de erro") será exibida.<br /><br /> Caso contrário, o status é OK e o ![ícone para a imagem de status OK](../master-data-services/media/mds-statusicon-ok.png "Ícone para status OK") é exibido.|  
|Modelo de origem|O nome do modelo de origem.|  
|Versão de origem|O nome da versão de origem.|  
|Entidade de origem|O nome da entidade de origem.|  
|Modelo de destino|O nome do modelo de destino.|  
|Versão de destino|O nome da versão de destino.|  
|Entidade de destino|O nome da entidade de destino.|  
|Frequência|Especifica a frequência do relacionamento de sincronização.|  
|Hora da última tentativa|Mostra a hora em que ocorreu a última tentativa de sincronização.|  
|Última vez com êxito|A hora em que ocorreu a última tentativa de sincronização bem-sucedida.|  
  
 Quando você clica em um índice, as informações a seguir são exibidas.  
  
-   **Erro da Última Tentativa**: mostra as informações de erro sobre a última tentativa de sincronização.  
  
-   **Criado Por**: o nome do usuário que criou a sincronização.  
  
-   **Em**: a data e a hora em que a sincronização foi criada.  
  
-   **Atualizado Por**: o nome do usuário que atualizou a sincronização pela última vez.  
  
-   **Em**: a data e a hora em que a sincronização foi atualizada pela última vez.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Editar e excluir uma relação de sincronização de entidade &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
