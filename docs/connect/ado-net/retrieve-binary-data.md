---
title: Recuperar dados binários
description: Descreve como recuperar dados binários ou grandes estruturas de dados usando o `CommandBehavior`.`SequentialAccess` para modificar o comportamento padrão de um `DataReader`.
ms.date: 12/04/2020
dev_langs:
- csharp
ms.assetid: 56c5a9e3-31f1-482f-bce0-ff1c41a658d0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 1033a6b5394d92a45cd19d70f4dd6c250ec37b62
ms.sourcegitcommit: 4419e99d77ee2c73f9da1559c7944f7702f2de30
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97744338"
---
# <a name="retrieve-binary-data"></a>Recuperar dados binários

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Por padrão, o **DataReader** carrega dados de entrada como uma linha assim que uma linha inteira de dados está disponível. Os blobs precisam de tratamento diferente, no entanto, porque podem conter gigabytes de dados que não podem ser contidos em uma única linha. O método **Command.ExecuteReader** tem uma sobrecarga que receberá um argumento <xref:System.Data.CommandBehavior> para modificar o comportamento padrão do **DataReader**. Você pode passar <xref:System.Data.CommandBehavior.SequentialAccess> para o método **ExecuteReader** para modificar o comportamento padrão do **DataReader** para que, em vez de carregar linhas de dados, carregará dados em sequência à medida que são recebidos. Isso é ideal para carregar BLOBs ou outras estruturas grandes de dados.

> [!NOTE]
> Ao definir o **DataReader** para usar **SequentialAccess**, observe a sequência na qual você acessa os campos retornados. O comportamento padrão do **DataReader**, que carrega uma linha inteira assim que ela está disponível, permite que você acesse os campos retornados em qualquer ordem até que a próxima linha seja lida. No entanto, ao usar o **SequentialAccess**, você deverá acessar os campos retornados pelo **DataReader** na ordem. Por exemplo, se sua consulta retornar três colunas, a terceiro das quais é um BLOB, você deverá retornar os valores do primeiro campo e do segundo antes de acessar os dados de BLOB no terceiro campo. Se você acessar o terceiro campo antes do primeiro campo ou segundo, o primeiro e o segundo valores de campo não estarão mais disponíveis. Isso ocorre porque **SequentialAccess** alterou o **DataReader** para retornar dados na sequência e os dados não estarão disponíveis depois que o **DataReader** tiver lido depois deles.

Para acessar os dados no campo BLOB, use os acessadores tipados **GetBytes** ou **GetChars** do **DataReader**, que preenchem uma matriz com dados. Você também pode usar **GetString** para dados de caracteres. No entanto, para conservar os recursos do sistema, talvez seja melhor não carregar um valor inteiro de BLOB em uma única variável de cadeia de caracteres. Em vez disso, você pode especificar um tamanho do buffer específico de dados a serem retornados e um local inicial para que o primeiro byte ou caractere seja lido dos dados retornados. **GetBytes** e **GetChars** retornarão um valor `long`, que representa o número de bytes ou caracteres retornados. Se você passar um array nulo para **GetBytes** ou **GetChars**, o valor longo retornado será o número total de bytes ou caracteres no BLOB. Você pode opcionalmente especificar um índice na matriz como uma posição inicial para os dados que estão sendo lidos.

## <a name="example"></a>Exemplo

O exemplo a seguir retorna a ID do publicador e o logotipo do banco de dados de exemplo [**pubs**](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs). A ID do publicador (`pub_id`) é um campo de caracteres e o logotipo é uma imagem, que é um BLOB. Como o campo **logo** é um bitmap, o exemplo retorna os dados binários usando **GetBytes**. Observe que a ID do publicador é acessada para a linha atual de dados antes do logotipo, porque os campos devem ser acessados sequencialmente.

[!code-csharp[SqlCommand_ExecuteReader_SequentialAccess#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteReader_SequentialAccess.cs#1)]

## <a name="see-also"></a>Consulte também

- [Dados binários e de valor grande do SQL Server](./sql/sql-server-binary-large-value-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
