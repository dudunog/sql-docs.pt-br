---
description: Método Resync
title: Método de ressincronização | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6e64c2f297e4628f04f99a7e97a6b9df00f6efa1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777645"
---
# <a name="resync-method"></a>Método Resync
Atualiza os dados no objeto [Recordset](./recordset-object-ado.md) atual ou na coleção [Fields](./fields-collection-ado.md) de um objeto [Record](./record-object-ado.md) , do banco de dados subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Opcional. Um valor [AffectEnum](./affectenum.md) que determina quantos registros o método de **ressincronização** afetará. O valor padrão é **adAffectAll**. Esse valor não está disponível com o método **Ressync** da coleção **Fields** de um objeto **Record** .  
  
 *ResyncValues*  
 Opcional. Um valor [ResyncEnum](./resyncenum.md) que especifica se os valores subjacentes são substituídos. O valor padrão é **adResyncAllValues**.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="recordset"></a>Conjunto de registros  
 Use o método **Ressync** para ressincronizar os registros no **conjunto de registros** atual com o banco de dados subjacente. Isso será útil se você estiver usando um cursor estático ou somente de avanço, mas quiser ver as alterações no banco de dados subjacente.  
  
 Se você definir a propriedade [CursorLocation](./cursorlocation-property-ado.md) como **adUseClient**, a **ressincronização** só estará disponível para objetos **Recordset** não somente leitura.  
  
 Ao contrário do método [Requery](./requery-method.md) , o método **Ressync** não executa novamente o comando subjacente do objeto **Recordset** . Os novos registros no banco de dados subjacente não estarão visíveis.  
  
 Se a tentativa de ressincronização falhar devido a um conflito com os dados subjacentes (por exemplo, um registro foi excluído por outro usuário), o provedor retornará avisos à coleção de [erros](./errors-collection-ado.md) e ocorrerá um erro em tempo de execução. Use a propriedade [Filter](./filter-property.md) (**adFilterConflictingRecords**) e a propriedade [status](./status-property-ado-recordset.md) para localizar registros com conflitos.  
  
 Se as propriedades dinâmicas de comando de tabela e [ressincronização](./resync-command-property-dynamic-ado.md) [exclusivas](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) forem definidas e o **conjunto de registros** for o resultado da execução de uma operação de junção em várias tabelas, o método de **ressincronização** executará o comando fornecido na propriedade **comando de ressincronização** somente na tabela nomeada na propriedade de **tabela exclusiva** .  
  
## <a name="fields"></a>Campos  
 Use o método **Ressync** para ressincronizar os valores da coleção **Fields** de um objeto **Record** com a fonte de dados subjacente. A propriedade [Count](./count-property-ado.md) não é afetada por este método.  
  
 Se *ResyncValues* for definido como **adResyncAllValues** (o valor padrão), as propriedades [subdependentes](./underlyingvalue-property.md), [Value](./value-property-ado.md)e [OriginalValue](./originalvalue-property-ado.md) dos objetos de [campo](./field-object.md) na coleção serão sincronizadas. Se *ResyncValues* for definido como **adResyncUnderlyingValues**, somente a propriedade **subdependvalue** será sincronizada.  
  
 O valor da propriedade **status** para cada objeto de **campo** no momento da chamada também afeta o comportamento da **ressincronização**. Para objetos de **campo** que têm valores de **status** de **adFieldPendingUnknown** ou **adFieldPendingInsert**, a **ressincronização** não tem nenhum efeito. Para valores de **status** de **adFieldPendingChange** ou **adFieldPendingDelete**, **Ressync** sincroniza valores de dados para campos que ainda existem na fonte de dados.  
  
 A **ressincronização** não modificará os valores de **status** dos objetos de **campo** , a menos que ocorra um erro quando a **ressincronização** for chamada. Por exemplo, se o campo não existir mais, o provedor retornará um valor de **status** apropriado para o objeto de **campo** , como **adFieldDoesNotExist**. Valores de **status** retornados podem ser logicamente combinados dentro do valor da propriedade **status** .  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Coleção Fields (ADO)](./fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Recordset (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Resync (VB)](./resync-method-example-vb.md)   
 [Exemplo do método Resync (VC + +)](./resync-method-example-vc.md)   
 [Método Clear (ADO)](./clear-method-ado.md)   
 [Propriedade UnderlyingValue](./underlyingvalue-property.md)