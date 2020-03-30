---
title: Destino do SQL Server Compact Edition | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlservercompactdest.f1
helpviewer_keywords:
- destinations [Integration Services], SQL Server Compact
- SQL Server Compact, destination
- inserting data
ms.assetid: 697742ba-cc14-414d-8187-1845ad0dd99b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1a9192e96bb99082b63e4feac451a378eabd8093
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298053"
---
# <a name="sql-server-compact-edition-destination"></a>Destino do SQL Server Compact Edition

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact grava dados em bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  Em um computador de 64 bits, você deve executar pacotes que se conectam a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact no modo de 32 bits. O provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa para se conectar a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, só está disponível na versão de 32 bits.  
  
 Você configura o destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact especificando o nome da tabela na qual o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact deve inserir os dados. A propriedade personalizada TableName do destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact contém o nome da tabela.  
  
 Esse destino usa um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact para conectar-se a uma fonte de dados, e o gerenciador de conexões especifica o provedor OLE DB a ser usado. Para obter mais informações, consulte [Gerenciador de Conexões do SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md).  
  
 O destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact inclui a propriedade personalizada TableName, que pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Expressões](../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas de destino do SQL Server Compact Edition](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md).  
  
 O destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact tem uma entrada e não aceita uma saída de erro.  
  
## <a name="configuration-of-the-sql-server-compact-edition-destination"></a>Configuração do destino do SQL Server Compact Edition  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do destino SQL Server](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir as propriedades desse componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
