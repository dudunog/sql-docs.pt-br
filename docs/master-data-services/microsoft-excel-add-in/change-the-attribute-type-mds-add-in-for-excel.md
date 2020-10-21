---
description: Alterar o tipo de atributo (suplemento MDS para Excel)
title: Alterar o tipo de atributo
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1fd0e7f0acbe6792a5d303d50ef66014ebc5c1cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257542"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>Alterar o tipo de atributo (suplemento MDS para Excel)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], os administradores podem alterar o tipo de atributo quando o tipo de dados ou número de caracteres permitido está incorreto.  
  
 Se você quiser alterar o tipo de atributo para criar uma lista restrita (atributo baseado em domínio), consulte [Criar um atributo baseado em domínio &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  Não é possível atualizar o tipo ou o tamanho da coluna **Nome** ou **Código**.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você precisa ter permissão para acessar as áreas funcionais **Administração do Sistema** e **Gerenciador** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md).  
  
-   Deve haver um modelo, entidade e atributo existente.  
  
### <a name="to-change-the-attribute-type"></a>Para alterar o tipo de atributo  
  
1.  No Excel, carregue a entidade que contém a coluna (atributo) a ser alterada. Para obter mais informações, consulte [Exportar dados para o Excel do Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
2.  Clique em qualquer célula da coluna que você deseja alterar.  
  
3.  No grupo **Compilar Modelo** , clique em **Propriedades do Atributo**.  
  
4.  Na caixa de diálogo **Propriedades do Atributo** , é necessário atualizar as configurações.  
  
5.  Clique em **OK**.  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>O que acontece quando você altera o tipo de atributo?  
 Se houver qualquer dependência no atributo, por exemplo, o atributo ser referenciado por qualquer regra de negócio do MDS ou hierarquia derivada, não será possível alterar o tipo de dados do atributo. Você obterá um erro informando que o tipo de atributo não pode ser modificado, pois é referenciado por um objeto.  
  
 Se houver algum erro durante a conversão do tipo de dados para os valores do atributo, o MDS fará o seguinte.  
  
-   Altera o tipo de dados do atributo.  
  
-   Gera uma cópia do atributo com o sufixo "_old" que contém os valores anteriores. Isso é chamado de atributo preterido.  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md)   
 [Criando um modelo &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
  
