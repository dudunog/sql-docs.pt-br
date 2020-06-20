---
title: Requisitos para agregações CLR definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
author: rothja
ms.author: jroth
ms.openlocfilehash: 8123f8324d43212007857dbb596a4fc61872bd2e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970776"
---
# <a name="requirements-for-clr-user-defined-aggregates"></a>Requisitos para agregações CLR definidas pelo usuário
  Um tipo em um assembly do CLR pode ser registrado como uma função de agregação definida pelo usuário, desde que implemente o contrato de agregação necessário. Esse contrato consiste no atributo `SqlUserDefinedAggregate` e os métodos de contrato de agregação. O contrato de agregação inclui o mecanismo para salvar o estado intermediário da agregação e o mecanismo para acumular novos valores, o qual consiste em quatro métodos: `Init`, `Accumulate`, `Merge` e `Terminate`. Quando atender a esses requisitos, você poderá aproveitar ao máximo as agregações definidas pelo usuário no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As seguintes seções deste tópico fornecem detalhes adicionais sobre como criar e trabalhar com agregações definidas pelo usuário. Para obter um exemplo, consulte [invocando funções de agregação definidas pelo usuário CLR](clr-user-defined-aggregate-invoking-functions.md).  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 Para obter mais informações, consulte [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="aggregation-methods"></a>Métodos de agregação  
 A classe registrada como uma agregação definida pelo usuário deve dar suporte aos seguintes métodos de instância. Eles são os métodos que o processador de consultas usa para computar a agregação:  
  
|Método|Sintaxe|Descrição|  
|------------|------------|-----------------|  
|`Init`|public void init ();|O processador de consultas usa esse método para inicializar a computação da agregação. Ele é invocado uma vez para cada grupo que o processador de consultas está agregando. O processador de consultas pode optar por reutilizar a mesma instância da classe de agregação para computar agregações de grupos vários. O método `Init` deve executar qualquer limpeza, conforme necessário, de usos anteriores desta instância e habilitá-la para que uma nova computação de agregação seja reiniciada.|  
|`Accumulate`|public void Accumulate (valor de tipo de entrada [, valor de tipo de entrada,...]);|Um ou mais parâmetros que representam os parâmetros da função. *input_type* deve ser o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados gerenciado equivalente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados nativo especificado por *input_sqltype* na `CREATE AGGREGATE` instrução. Para obter mais informações, consulte [mapeando dados de parâmetro CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).<br /><br /> Para UDTs (tipos definidos pelo usuário), o tipo de entrada é o mesmo que o tipo do UDT. O processador de consultas usa esse método para acumular os valores de agregação. Ele é invocado uma vez para obter cada valor no grupo que está sendo agregado. O processador de consultas o chama somente depois de chamar o método `Init` na instância determinada da classe de agregação. A implementação desse método deve atualizar o estado da instância para refletir o acúmulo do valor do argumento que é passado.|  
|`Merge`|particular void Merge (valor de udagg_class);|Esse método pode ser usado para mesclar outra instância desta classe de agregação com a instância atual. O processador de consultas usa esse método para mesclar várias computações parciais de uma agregação.|  
|`Terminate`|return_type pública terminar ();|Esse método completa a computação de agregações e retorna o resultado da agregação. O *return_type* deve ser um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados gerenciado que seja o equivalente gerenciado de *return_sqltype* especificado na `CREATE AGGREGATE` instrução. O *return_type* também pode ser um tipo definido pelo usuário.|  
  
### <a name="table-valued-parameters"></a>Parâmetros com valor de tabela  
 Os TVPs (parâmetros com valor de tabela), ou seja, tipos de tabela definidos pelo usuário transmitidos para um procedimento ou uma função, oferecem uma maneira eficiente de passar várias linhas de dados para o servidor. Os TVPs proporcionam funcionalidade semelhante para matrizes de parâmetro, porém com maior flexibilidade e integração com [!INCLUDE[tsql](../../includes/tsql-md.md)]. Eles também fornecem o potencial para melhor desempenho. Os TVPs também ajudam a reduzir o número de viagens de ida e volta para o servidor. Em vez de enviar várias solicitações ao servidor, como com uma lista de parâmetros escalares, os dados podem ser enviados ao servidor como um TVP. Um tipo de tabela definido pelo usuário não pode ser passado como um parâmetro com valor de tabela para, ou ser retornado de, um procedimento armazenado ou uma função gerenciada(o) que é executada(o) no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Além disso, TVPs não podem ser usados dentro do escopo de uma conexão de contexto. Entretanto, um TVP pode ser usado com o SqlClient nos procedimentos armazenados gerenciados ou nas funções em execução no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se for usado em uma conexão que não seja de contexto. A conexão pode ser com o mesmo servidor que está executando o procedimento ou função gerenciada. Para obter mais informações sobre TVPs, consulte [usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Atualizada a descrição do método `Accumulate`; agora ele aceita mais de um parâmetro.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos CLR definidos pelo usuário](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Invocando funções de agregação CLR definidas pelo usuário](clr-user-defined-aggregate-invoking-functions.md)  
  
  
