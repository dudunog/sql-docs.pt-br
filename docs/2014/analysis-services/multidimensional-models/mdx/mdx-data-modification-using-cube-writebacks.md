---
title: Usando o cubo write-backs (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- writeback [Analysis Services], cubes
- cubes [Analysis Services], modifying
- modifying cubes
- UPDATE CUBE statement
- cubes [Analysis Services], writeback
ms.assetid: ae2385fc-7fa0-4f8e-98d7-dcb0a5f0eeea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a79e98375c27c6a3570b2fafcf424965d7a97c8d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074215"
---
# <a name="using-cube-writebacks-mdx"></a>Usando Cube Writebacks (MDX)
  Você atualiza um cubo usando a instrução [UPDATE CUBE](/sql/mdx/mdx-data-manipulation-update-cube) . Essa instrução permite que você atualize uma tupla com um valor específico. Para usar a instrução UPDATE CUBE de forma eficiente para atualizar um cubo, você precisa entender a sintaxe da instrução, as condições de erro que podem acontecer, e como as atualizações podem afetar um cubo.  
  
## <a name="update-cube-statement-syntax"></a>Sintaxe da instrução UPDATE CUBE  
 A seguinte sintaxe descreve a instrução UPDATE CUBE:  
  
```  
UPDATE [CUBE] <Cube_Name> SET <tuple>.VALUE = <value> [,<tuple>.VALUE = <value>...]  
 [ USE_EQUAL_ALLOCATION | USE_EQUAL_INCREMENT |  
  USE_WEIGHTED_ALLOCATION [BY <weight value_expression>] |  
  USE_WEIGHTED_INCREMENT [BY <weight value_expression>] ]   
```  
  
 Se um conjunto completo de coordenadas não for especificado para a tupla, as coordenadas não especificadas usarão o membro padrão da hierarquia. A tupla identificada deve fazer referência a uma célula que seja agregada com a função [Sum](/sql/mdx/sum-mdx) , e não deve usar um membro calculado como uma das coordenadas da célula.  
  
 Você pode pensar na instrução UPDATE CUBE como uma sub-rotina que gera uma série de operações de write-back individuais a células atômicas. Todas essas operações de write-back individuais são acumuladas à soma especificada.  
  
> [!NOTE]  
>  Quando células atualizadas não se sobrepõem, a propriedade de cadeia de caracteres da conexão `Update Isolation Level` pode ser usada para aprimorar o desempenho de UPDATE CUBE. Para obter mais informações, consulte <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.  
  
## <a name="example"></a>Exemplo  
 Você pode testar o UPDATE CUBE usando o grupo de medidas Público-Alvo das Vendas no cubo do Adventure Works. Esse grupo de medidas consiste em medidas agregadas por SUM, que é uma exigência para UPDATE CUBE.  
  
1.  Habilite o write-back para o grupo de medidas Público-Alvo das Vendas no banco de dados do Adventure Works. No Management Studio, clique com o botão direito do mouse em um grupo de medidas, aponte para **Opções de Write-back**, escolha **Habilitar Write-back**.  
  
     Você deve ver uma nova tabela de write-back na pasta Write-back. O nome da tabela é WriteTable_Fact Sales Quota.  
  
2.  Abra uma janela de consulta MDX. Execute a seguinte instrução select para exibir o valor original:  
  
    ```  
    SELECT [Measures].[Sales Amount Quota] on 0 ,  
    [Employee].[Employee Department].[Title].&[Sales Representative].children on 1  
    FROM [Adventure Works]  
  
    ```  
  
     Você deve ver as contas do valor de vendas para cada representante.  
  
3.  Execute a instrução update cube para fazer write-back de um novo valor. Neste exemplo, estamos definindo a cota do valor de vendas como 0. Como o novo valor é 0, não especifique um método de alocação.  
  
    ```  
    UPDATE CUBE [Adventure Works]   
    SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 0  
  
    ```  
  
4.  Reexecute a instrução SELECT. Agora você deve ver zero para as cotas.  
  
 O valor de write-back é restrito à sessão atual. Para manter o valor em usuários e sessões, processe a tabela de write-back. No Management Studio, clique com o botão direito do mouse em Cota de Vendas de WriteTable_Fact e escolha **Processar**.  
  
 Para especificar um método de alocação, o novo valor deve ser maior que zero. Neste exemplo, o novo valor de Cota do Valor de Vendas é dois milhões e o método de alocação distribui o valor por todos os representantes de vendas.  
  
```  
UPDATE CUBE [Adventure Works]   
SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 2000000   
USE_EQUAL_ALLOCATION  
```  
  
## <a name="error-conditions"></a>Condições de erro  
 A tabela a seguir descreve a causa de falha dos write-backs e o resultado desses erros.  
  
|Condição de erro|Result|  
|---------------------|------------|  
|A atualização inclui membros da mesma dimensão que não existem um com o outro.|Haverá falha na atualização. O espaço do cubo não conterá a célula mencionada.|  
|A atualização inclui uma medida com origem em uma medida de um tipo não atribuído.|Haverá falha na atualização. Os incrementos requerem que a medida possa receber um valor negativo.|  
|A atualização inclui uma medida que agrega um item diferente da soma.|Foi gerado um erro.|  
|Foi tentada uma atualização em um subcubo.|Foi gerado um erro.|  
  
## <a name="affect-of-cube-changes"></a>Efeito das mudanças do cubo  
 As seguintes mudanças não vão afetar um write-back:  
  
-   Processamento de um cubo, dos grupos de medidas do cubo ou das dimensões do cubo.  
  
-   Adicionando atributos a qualquer dimensão.  
  
-   Adicionando uma nova dimensão.  
  
-   Excluindo uma dimensão que não inclui o write-back.  
  
-   Adicionando, modificando ou removendo uma hierarquia.  
  
-   Adicionando uma nova medida.  
  
 As seguintes mudanças não podem ser feitas sem remover os dados de write-back:  
  
-   Excluindo um atributo, ou sua hierarquia de atributo, se o atributo estiver incluído no write-back. Isso inclui explicitamente remover o atributo, ou sua hierarquia de atributo, ou remover a dimensão pai do atributo.  
  
-   Excluindo uma medida incluída no write-back.  
  
-   Adicionando um atributo sem um nível `(All)` a uma dimensão incluída no write-back.  
  
-   Alterando a granularidade da dimensão da dimensão incluída no write-back.  
  
## <a name="see-also"></a>Consulte Também  
 [Modificando dados &#40;MDX&#41;](mdx-data-modification-modifying-data.md)  
  
  
