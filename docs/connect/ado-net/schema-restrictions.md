---
title: Restrições de esquemas
description: Descreve as restrições de esquema que podem ser usadas com GetSchema ao usar o Provedor de Dados Microsoft SqlClient para SQL Server.
ms.date: 11/26/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 8d72e2dd020f1345ceb0b68249cb3d3acd1024dc
ms.sourcegitcommit: 2add15a99df7b85d271adb261523689984dfd134
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97051245"
---
# <a name="schema-restrictions"></a>Restrições de esquemas

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O segundo parâmetro opcional do método **GetSchema** são as restrições usadas para limitar a quantidade de informações de esquema retornadas, e é transmitido para o método **GetSchema** como uma matriz de cadeias de caracteres. A posição na matriz determina os valores que podem se transmitidos, e isso é equivalente ao número da restrição.  
  
Por exemplo, a tabela a seguir descreve as restrições compatíveis com a coleção de esquemas "Tables" usando o Provedor de Dados Microsoft SqlClient para SQL Server. As restrições adicionais para as coleções de esquemas do SQL Server são listadas ao final deste tópico.  

|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Name|TABLE_NAME|3|  
|TableType|@TableType|TABLE_TYPE|4|  
 
## <a name="specifying-restriction-values"></a>Como especificar valores de restrição  

Para usar uma das restrições da coleção de esquemas "Tables", basta criar uma matriz de cadeias de caracteres com quatro elementos e inserir um valor no elemento que corresponde ao número da restrição. Por exemplo, para restringir as tabelas retornadas pelo método **GetSchema** apenas às tabelas no esquema "Sales", defina o segundo elemento da matriz como "Sales" antes de transmiti-lo para o método **GetSchema**.  
  
> [!NOTE]
> - As coleções de restrições para `SqlClient` têm uma coluna `ParameterName` adicional. A coluna padrão de restrição ainda está disponível para compatibilidade com versões anteriores, mas é ignorada no momento. Consultas parametrizadas em vez da substituição de cadeia de caracteres devem ser usadas para minimizar o risco de um ataque de injeção de SQL ao especificar valores de restrição.  
> - O número de elementos na matriz precisa ser inferior ou igual ao número de restrições compatíveis com a coleção de esquemas especificada. Caso contrário, uma <xref:System.ArgumentException> será gerada. Pode haver menos do que o número máximo de restrições. As restrições ausentes são consideradas nulas (irrestrito).  
  
Você pode consultar o Provedor de Dados Microsoft SqlClient para SQL Server para determinar a lista de restrições compatíveis chamando o método **GetSchema** com o nome da coleção de esquemas de restrições, que é "Restrictions". Isso retornará uma <xref:System.Data.DataTable> com uma lista de nomes de coleção, os nomes de restrição, os valores de restrição padrão e os números de restrição.  
  
### <a name="example"></a>Exemplo  

Os seguintes exemplos demonstram como usar o método <xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A> da classe <xref:Microsoft.Data.SqlClient.SqlConnection> do Provedor de Dados Microsoft SqlClient para SQL Server para recuperar informações de esquema sobre todas as tabelas contidas no banco de dados de exemplo **AdventureWorks** e para restringir as informações retornadas apenas às tabelas no esquema "Sales":  

[!code-csharp[SqlClient GetSchema with restrictions#1](~/../sqlclient/doc/samples/SqlConnection_GetSchema_Restriction.cs#1)]  

## <a name="sql-server-schema-restrictions"></a>Restrições de esquema do SQL Server  

 As tabelas a seguir listam as restrições para coleções de esquemas do SQL Server.  
  
### <a name="users"></a>Usuários  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|User_Name|@Name|name|1|  
  
### <a name="databases"></a>Bancos de dados  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Nome|@Name|Nome|1|  
  
### <a name="tables"></a>Tabelas  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Name|TABLE_NAME|3|  
|TableType|@TableType|TABLE_TYPE|4|  
  
### <a name="columns"></a>Colunas  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
|Coluna|@Column|COLUMN_NAME|4|  
  
### <a name="structuredtypemembers"></a>StructuredTypeMembers  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
|Coluna|@Column|COLUMN_NAME|4|  
  
### <a name="views"></a>Exibições  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
  
### <a name="viewcolumns"></a>ViewColumns  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|VIEW_CATALOG|1|  
|Proprietário|@Owner|VIEW_SCHEMA|2|  
|Tabela|@Table|VIEW_NAME|3|  
|Coluna|@Column|COLUMN_NAME|4|  
  
### <a name="procedureparameters"></a>ProcedureParameters  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|SPECIFIC_CATALOG|1|  
|Proprietário|@Owner|SPECIFIC_SCHEMA|2|  
|Nome|@Name|SPECIFIC_NAME|3|  
|Parâmetro|@Parameter|PARAMETER_NAME|4|  
  
### <a name="procedures"></a>Procedimentos  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|SPECIFIC_CATALOG|1|  
|Proprietário|@Owner|SPECIFIC_SCHEMA|2|  
|Nome|@Name|SPECIFIC_NAME|3|  
|Tipo|@Type|ROUTINE_TYPE|4|  
  
### <a name="indexcolumns"></a>IndexColumns  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|db_name()|1|  
|Proprietário|@Owner|user_name()|2|  
|Tabela|@Table|o.name|3|  
|ConstraintName|@ConstraintName|x.name|4|  
|Coluna|@Column|c.name|5|  
  
### <a name="indexes"></a>Índices  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|db_name()|1|  
|Proprietário|@Owner|user_name()|2|  
|Tabela|@Table|o.name|3|  
  
### <a name="userdefinedtypes"></a>UserDefinedTypes  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|assembly_name|@AssemblyName|assemblies.name|1|  
|udt_name|@UDTName|types.assembly_class|2|  
  
### <a name="foreignkeys"></a>ForeignKeys  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|CONSTRAINT_CATALOG|1|  
|Proprietário|@Owner|CONSTRAINT_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
|Nome|@Name|CONSTRAINT_NAME|4|  
  
## <a name="see-also"></a>Confira também

- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
