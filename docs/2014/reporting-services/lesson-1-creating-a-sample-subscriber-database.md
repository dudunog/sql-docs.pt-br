---
title: 'Lição 1: Criando um banco de dados do assinante de exemplo | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9e68650b21ee8cddc6258ab64b874bcf51ec1a83
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108534"
---
# <a name="lesson-1-creating-a-sample-subscriber-database"></a>Lição 1: Criando um banco de dados do assinante de exemplo
  Antes de definir uma assinatura controlada por dados, você deve ter uma fonte de dados que fornece dados de assinatura. Nesta etapa, você criará um banco de dados pequeno para armazenar os dados de assinatura usados neste tutorial. Posteriormente, quando a assinatura for processada, o servidor de relatório recuperará esses dados e os utilizará para personalizar a saída de relatório, as opções de entrega e o formato de apresentação do relatório.  
  
 Esta lição pressupõe que você está [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] usando o para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] criar um banco de dados.  
  
### <a name="to-create-a-sample-subscriber-database"></a>Para criar um banco de dados de assinantes de exemplo  
  
1.  Inicie o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e abra uma conexão com um [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Clique com o botão direito do mouse em Bancos de Dados e selecione **Novo Banco de Dados...** .  
  
3.  Na caixa de diálogo novo banco de dados, em nome do banco de dados, digite *assinantes*. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  Clique no botão **Nova Consulta** na barra de ferramentas.  
  
5.  Copie as seguintes instruções [!INCLUDE[tsql](../includes/tsql-md.md)] na consulta vazia:  
  
    ```  
    Use Subscribers  
    CREATE TABLE [dbo].[OrderInfo] (  
        [SubscriptionID] [int] NOT NULL PRIMARY KEY ,  
        [Order] [nvarchar] (20) NOT NULL,  
        [FileType] [bit],  
        [Format] [nvarchar] (20) NOT NULL ,  
    ) ON [PRIMARY]  
    GO  
  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('1', 'so43659', '1', 'IMAGE')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('2', 'so43664', '1', 'MHTML')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('3', 'so43668', '1', 'PDF')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('4', 'so71949', '1', 'Excel')  
    GO  
    ```  
  
6.  Clique em **! Execute** na barra de ferramentas.  
  
7.  Use uma instrução SELECT para verificar se há três linhas de dados. Por exemplo: `select * from OrderInfo`  
  
## <a name="next-steps"></a>Próximas etapas  
 Você criou com êxito os dados de assinatura que controlarão a distribuição de relatórios e modificarão a saída de relatório para cada assinante. Em seguida, você modificará as propriedades de fonte de dados do relatório que será distribuído aos assinantes. A modificação das propriedades de fonte de dados é feita para preparar o relatório para a entrega da assinatura controlada por dados. Você também modificará o design do relatório para incluir um parâmetro que a assinatura usará com os dados do assinante. [Lição 2: modificando as propriedades da fonte de dados do relatório](lesson-2-modifying-the-report-data-source-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Criar um banco de dados](../relational-databases/databases/create-a-database.md)   
 [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
