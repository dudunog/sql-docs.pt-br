---
title: Modificar dados com procedimentos armazenados
description: Descreve como usar parâmetros de entrada e de saída de procedimentos armazenados para inserir uma linha em um banco de dados, retornando um novo valor de identidade.
ms.date: 12/04/2020
dev_langs:
- csharp
ms.assetid: 7d8e9a46-1af6-4a02-bf61-969d77ae07e0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: f04884302bb1f13852097182d6ebc8e06570c66b
ms.sourcegitcommit: 4419e99d77ee2c73f9da1559c7944f7702f2de30
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97744333"
---
# <a name="modify-data-with-stored-procedures"></a>Modificar dados com procedimentos armazenados

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Os procedimentos armazenados podem aceitar dados como parâmetros de entrada e podem retornar dados como parâmetros de saída, conjuntos de resultados ou valores de retorno. O exemplo abaixo ilustra como o Provedor de Dados do Microsoft SqlClient para o SQL Server envia e recebe parâmetros de entrada, parâmetros de saída e valores retornados. O exemplo insere um novo registro em uma tabela, em que a coluna de chave primária é uma coluna de identidade.

> [!NOTE]
> Se você estiver usando procedimentos armazenados para editar ou excluir dados por meio de um <xref:Microsoft.Data.SqlClient.SqlDataAdapter>, não use **SET NOCOUNT ON** na definição do procedimento armazenado. Isso faz com que a contagem retornada de linhas afetadas seja zero, o que o `DataAdapter` interpreta como um conflito de simultaneidade. Nesse caso, será gerada uma <xref:System.Data.DBConcurrencyException>.

## <a name="example"></a>Exemplo

O exemplo usa o procedimento armazenado a seguir para inserir uma nova categoria na tabela **Northwind** **Categories**. O procedimento armazenado usa o valor da coluna **CategoryName** como um parâmetro de entrada e a função **SCOPE_IDENTITY()** para recuperar o novo valor do campo de identidade, **CategoryID**, e retorná-lo em um parâmetro de saída. A instrução RETURN usa a função **\@\@ROWCOUNT** para retornar o número de linhas inseridas.

```sql
CREATE PROCEDURE dbo.InsertCategory  
  @CategoryName nvarchar(15),  
  @Identity int OUT  
AS  
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)  
SET @Identity = SCOPE_IDENTITY()  
RETURN @@ROWCOUNT  
```  

O código de exemplo a seguir usa o procedimento armazenado `InsertCategory` mostrado acima como a origem de <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> de <xref:Microsoft.Data.SqlClient.SqlDataAdapter>. O parâmetro de saída `@Identity` será refletido em <xref:System.Data.DataSet> após a inserção do registro no banco de dados quando o método `Update` de <xref:Microsoft.Data.SqlClient.SqlDataAdapter> for chamado. O código também recupera o valor de retorno.

[!code-csharp[DataWorks SqlClient.SprocIdentityReturn#1](~/../sqlclient/doc/samples/SqlDataAdapter_SPIdentityReturn.cs#1)]

## <a name="see-also"></a>Confira também

- [Recuperar e modificar dados no ADO.NET](retrieving-modifying-data.md)
- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Executar um comando](execute-command.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
