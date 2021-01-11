---
title: Recuperar identidade ou valores de numeração automática
description: Saiba como recuperar valores de identidade e de numeração automática de chaves primárias no SQL Server e como mesclar novos valores de identidade no ADO.NET.
ms.date: 12/04/2020
dev_langs:
- csharp
ms.assetid: d6b7f9cb-81be-44e1-bb94-56137954876d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 4ca2199686359235ff1d2c834b0b19a88296030d
ms.sourcegitcommit: 4419e99d77ee2c73f9da1559c7944f7702f2de30
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97744329"
---
# <a name="retrieve-identity-or-autonumber-values"></a>Recuperar identidade ou valores de numeração automática

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Uma chave primária em um banco de dados relacional é uma coluna ou uma combinação de colunas que sempre contém valores exclusivos. Saber o valor da chave primária permite que você localize a linha que o contém. Os mecanismos de bancos de dados relacionais, como o SQL Server, o Oracle e o Microsoft Access/Jet dão suporte à criação de colunas de incremento automático, que podem ser designadas como chaves primárias. Esses valores gerados pelo servidor como linhas são adicionados a uma tabela. No SQL Server, você define a propriedade de identidade de uma coluna, no Oracle você cria uma Sequência e no Microsoft Access você cria uma coluna AutoNumber.

O <xref:System.Data.DataColumn> também pode ser usado para gerar valores incrementais automaticamente definindo a propriedade <xref:System.Data.DataColumn.AutoIncrement%2A> como true. No entanto, você pode terminar com valores duplicados em instâncias separadas de um <xref:System.Data.DataTable>, se vários aplicativos cliente estiverem criando valores incrementais automaticamente de forma independente. Fazer com que o servidor gere valores incrementais automaticamente elimina conflitos potenciais permitindo que cada usuário recupere o valor gerado para cada linha inserida.

Durante uma chamada para o método `Update` de um `DataAdapter`, o banco de dados pode enviar dados de volta para seu aplicativo ADO.NET como parâmetros de saída ou como o primeiro registro retornado do conjunto de resultados de uma instrução SELECT executada no mesmo lote que a instrução INSERT. O Provedor de Dados do Microsoft SqlClient para o SQL Server pode recuperar esses valores e atualizar as colunas correspondentes na <xref:System.Data.DataRow> que está sendo atualizada.

> [!NOTE]
> Uma alternativa ao uso de um valor incrementado automaticamente é usar o método <xref:System.Guid.NewGuid%2A> de um objeto <xref:System.Guid> para gerar um GUID, ou identificador exclusivo, no computador cliente que pode ser copiado para o servidor à medida que cada nova linha é inserida. O método `NewGuid` gera um valor binário de 16 bytes que é criado usando um algoritmo que fornece uma alta probabilidade de que nenhum valor será duplicado. Em um banco de dados SQL Server, um GUID é armazenado em uma coluna `uniqueidentifier`, que o SQL Server pode gerar automaticamente usando a função Transact-SQL `NEWID()`. Usar um GUID como uma chave primária pode afetar negativamente o desempenho. O SQL Server fornece suporte para a função `NEWSEQUENTIALID()`, que gera um GUID sequencial que não tem a garantia de ser global exclusivo, mas que pode ser indexado com mais eficiência.

## <a name="retrieve-sql-server-identity-column-values"></a>Recuperar valores da coluna de identidade do SQL Server

Ao trabalhar com o Microsoft SQL Server, você pode criar um procedimento armazenado com um parâmetro de saída para retornar o valor da identidade de uma linha inserida. A tabela a seguir descreve as três funções Transact-SQL no SQL Server que podem ser usadas para recuperar valores de colunas de identidade.

|Função|Descrição|
|--------------|-----------------|
|SCOPE_IDENTITY|Retorna o valor de identidade mais recente no escopo atual de execução. SCOPE_IDENTITY é recomendado para a maioria dos cenários.|
|@@IDENTITY|Contém o valor de identidade mais recente gerado em qualquer tabela da sessão atual. @@IDENTITY pode ser afetado por gatilhos e talvez não retorne o valor de identidade esperado.|
|IDENT_CURRENT|Retorna o valor de identidade mais recente gerado para uma tabela específica em qualquer sessão e em qualquer escopo.|

O procedimento armazenado a seguir demonstra como inserir uma linha na tabela **Categories** e usar um parâmetro de saída para retornar o novo valor de identidade gerado pela função SCOPE_IDENTITY() do Transact-SQL.

```sql
CREATE PROCEDURE dbo.InsertCategory
  @CategoryName nvarchar(15),
  @Identity int OUT
AS
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)
SET @Identity = SCOPE_IDENTITY()
```

O procedimento armazenado pode ser especificado como a origem do <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> de um objeto <xref:Microsoft.Data.SqlClient.SqlDataAdapter>. A propriedade <xref:Microsoft.Data.SqlClient.SqlCommand.CommandType%2A> do <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> deve ser definida como <xref:System.Data.CommandType.StoredProcedure>. A saída de identidade é recuperada criando um <xref:Microsoft.Data.SqlClient.SqlParameter> que tenha um <xref:System.Data.ParameterDirection> de <xref:System.Data.ParameterDirection.Output>. Quando o `InsertCommand` é processado, o valor de identidade incrementado automaticamente é retornado e colocado na coluna **CategoryID** da linha atual se você define a propriedade <xref:Microsoft.Data.SqlClient.SqlCommand.UpdatedRowSource%2A> do comando de inserção como `UpdateRowSource.OutputParameters` ou como `UpdateRowSource.Both`.

Se o comando de inserção executar um lote que inclua uma instrução INSERT e uma instrução SELECT, que retorne o novo valor de identidade, você poderá recuperar o novo valor definindo a propriedade `UpdatedRowSource` do comando de inserção como `UpdateRowSource.FirstReturnedRecord`.

[!code-csharp[DataWorks SqlClient.RetrieveIdentityStoredProcedure#1](~/../sqlclient/doc/samples/SqlDataAdapter_RetrieveIdentityStoredProcedure.cs#1)]

## <a name="merge-new-identity-values"></a>Mesclar novos valores de identidade

Um cenário comum é chamar o método `GetChanges` de um `DataTable` para criar uma cópia que contenha somente linhas alteradas e usar a nova cópia ao chamar o método `Update` de um `DataAdapter`. Isso é especialmente útil quando você precisar realizar marshaling das linhas alteradas para um componente separado que executa a atualização. Após a atualização, a cópia pode conter os novos valores de identidade que devem ser mesclados de volta para o `DataTable` original. Os novos valores de identidade provavelmente serão diferentes dos valores originais no `DataTable`. Para realizar a mesclagem, os valores originais das colunas **AutoIncrement** na cópia precisam ser mantidos, para localizar e atualizar as linhas existentes na `DataTable` original, em vez de acrescentar novas linhas contendo os novos valores de identidade. No entanto, por padrão, esses valores originais são perdidos depois de uma chamada para o método `Update` de um `DataAdapter`, porque `AcceptChanges` é chamado implicitamente para cada `DataRow` atualizado.

Há duas maneiras de preservar os valores originais de um `DataColumn` em um `DataRow` durante uma atualização do `DataAdapter`:

- O primeiro método de preservação dos valores originais é definir a propriedade `AcceptChangesDuringUpdate` do `DataAdapter` como `false`. Essa configuração afeta todas as `DataRow` na `DataTable` que estão sendo atualizadas. Para obter mais informações e um exemplo de código, consulte <xref:System.Data.Common.DataAdapter.AcceptChangesDuringUpdate%2A>.

- O segundo método é escrever o código no manipulador de eventos `RowUpdated` do `DataAdapter` para definir o <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> como <xref:System.Data.UpdateStatus.SkipCurrentRow>. O `DataRow` é atualizado, mas o valor original de cada `DataColumn` é preservado. Esse método permite que você preserve os valores originais de algumas linhas, mas não de outras. Por exemplo, seu código pode preservar os valores originais das linhas adicionadas e não das linhas excluídas ou editadas verificando primeiro o <xref:System.Data.Common.RowUpdatedEventArgs.StatementType%2A> e, em seguida, definindo <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> como <xref:System.Data.UpdateStatus.SkipCurrentRow> somente para linhas com um `StatementType` de `Insert`.

Quando um desses métodos é usado para preservar os valores originais em uma `DataRow` durante uma atualização do `DataAdapter`, o Adaptador de Dados do Microsoft SqlClient para o SQL Server executa uma série de ações para definir os valores atuais da `DataRow` para novos valores retornados pelos parâmetros de saída ou pela primeira linha retornada de um conjunto de resultados, preservando o valor original em cada `DataColumn`. Primeiro, o método `AcceptChanges` do `DataRow` é chamado para preservar os valores atuais como valores originais e, em seguida, os novos valores são atribuídos. Depois dessas ações, o `DataRows` que teve sua propriedade <xref:System.Data.DataRow.RowState%2A> definida como <xref:System.Data.DataRowState.Added> terá sua propriedade `RowState` definida como <xref:System.Data.DataRowState.Modified>, o que pode ser inesperado.

Como os resultados do comando serão aplicados a cada <xref:System.Data.DataRow> que está sendo atualizado é determinado pela propriedade <xref:System.Data.Common.DbCommand.UpdatedRowSource%2A> de cada <xref:System.Data.Common.DbCommand>. Essa propriedade é definida como um valor da enumeração `UpdateRowSource`.

A tabela a seguir descreve como os valores de enumeração `UpdateRowSource` afetam a propriedade <xref:System.Data.DataRow.RowState%2A> das linhas atualizadas.

|Nome do membro|Descrição|
|-----------------|-----------------|
|<xref:System.Data.UpdateRowSource.Both>|`AcceptChanges` é chamado e os valores do parâmetro de saída e/ou os valores na primeira linha de qualquer conjunto de resultados retornado são colocados no `DataRow` que está sendo atualizado. Se não houver nenhum valor a ser aplicado, o `RowState` será <xref:System.Data.DataRowState.Unchanged>.|
|<xref:System.Data.UpdateRowSource.FirstReturnedRecord>|Se uma linha for retornada, `AcceptChanges` será chamado e a linha será mapeada para as linhas alteradas no `DataTable`, definindo `RowState` como `Modified`. Se nenhuma linha for retornada, `AcceptChanges` não será chamado e o `RowState` permanecerá `Added`.|
|<xref:System.Data.UpdateRowSource.None>|Todos os parâmetros ou linhas retornados são ignorados. Não há nenhuma chamada para `AcceptChanges` e o `RowState` permanece `Added`.|
|<xref:System.Data.UpdateRowSource.OutputParameters>|`AcceptChanges` é chamado e todos os parâmetros de saída são mapeados para a linha alterada no `DataTable`, definindo o `RowState` como `Modified`. Se não houver nenhum parâmetro de saída, o `RowState` será `Unchanged`.|

### <a name="example"></a>Exemplo

Este exemplo demonstra como extrair linhas alteradas de um `DataTable` e como usar um <xref:Microsoft.Data.SqlClient.SqlDataAdapter> para atualizar a fonte de dados e recuperar um novo valor de coluna de identidade. O <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> executa duas instruções Transact-SQL, a primeira é a instrução INSERT, e a segunda é uma instrução SELECT, que usa a função SCOPE_IDENTITY para recuperar o valor de identidade.

```sql
INSERT INTO dbo.Shippers (CompanyName)
VALUES (@CompanyName);
SELECT ShipperID, CompanyName FROM dbo.Shippers
WHERE ShipperID = SCOPE_IDENTITY();
```

A propriedade `UpdatedRowSource` do comando de inserção é definida como `UpdateRowSource.FirstReturnedRow` e a propriedade <xref:System.Data.MissingSchemaAction> do `DataAdapter` é definida como `MissingSchemaAction.AddWithKey`. O `DataTable` é preenchido e o código adiciona uma nova linha ao `DataTable`. As linhas alteradas são extraídas em um novo `DataTable`, que é passado para o `DataAdapter`, que atualiza o servidor.

[!code-csharp[DataWorks SqlClient.MergeIdentity#1](~/../sqlclient/doc/samples/SqlDataAdapter_MergeIdentity.cs#1)]

O manipulador de eventos `OnRowUpdated` verifica o <xref:System.Data.Common.RowUpdatedEventArgs.StatementType%2A> do <xref:Microsoft.Data.SqlClient.SqlRowUpdatedEventArgs> para determinar se a linha é uma inserção. Se for, a propriedade <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> será definida como <xref:System.Data.UpdateStatus.SkipCurrentRow>. A linha é atualizada, mas os valores originais da linha são preservados. No corpo principal do procedimento, o método <xref:System.Data.DataSet.Merge%2A> é chamado para mesclar o novo valor de identidade com o `DataTable`original e, finalmente, `AcceptChanges` é chamado.

[!code-csharp[DataWorks SqlClient.MergeIdentity#2](~/../sqlclient/doc/samples/SqlDataAdapter_MergeIdentity.cs#2)]

### <a name="retrieve-identity-values"></a>Recuperar valores de identidade

Geralmente, definimos a coluna como identidade quando os valores da coluna devem ser exclusivos. E, às vezes, precisamos do valor de identidade de novos dados. Este exemplo demonstra como recuperar os valores de identidade:

- Cria um procedimento armazenado para inserir os dados e retornar um valor de identidade.

- Executa um comando para inserir os novos dados e exibir o resultado.

- Usa <xref:Microsoft.Data.SqlClient.SqlDataAdapter> para inserir novos dados e exibir o resultado.

Antes de você compilar e executar o exemplo, deverá criar o banco de dados de exemplo, usando o seguinte script:

```sql
USE [master]
GO

CREATE DATABASE [MySchool]
GO

USE [MySchool]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE procedure [dbo].[CourseExtInfo] @CourseId int
as
select c.CourseID,c.Title,c.Credits,d.Name as DepartmentName
from Course as c left outer join Department as d on c.DepartmentID=d.DepartmentID
where c.CourseID=@CourseId

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
create procedure [dbo].[DepartmentInfo] @DepartmentId int,@CourseCount int output
as
select @CourseCount=Count(c.CourseID)
from course as c
where c.DepartmentID=@DepartmentId

select d.DepartmentID,d.Name,d.Budget,d.StartDate,d.Administrator
from Department as d
where d.DepartmentID=@DepartmentId

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
Create PROCEDURE [dbo].[GetDepartmentsOfSpecifiedYear]
@Year int,@BudgetSum money output
AS
BEGIN
        SELECT @BudgetSum=SUM([Budget])
  FROM [MySchool].[dbo].[Department]
  Where YEAR([StartDate])=@Year

SELECT [DepartmentID]
      ,[Name]
      ,[Budget]
      ,[StartDate]
      ,[Administrator]
  FROM [MySchool].[dbo].[Department]
  Where YEAR([StartDate])=@Year

END
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[GradeOfStudent]
-- Add the parameters for the stored procedure here
@CourseTitle nvarchar(100),@FirstName nvarchar(50),
@LastName nvarchar(50),@Grade decimal(3,2) output
AS
BEGIN
select @Grade=Max(Grade)
from [dbo].[StudentGrade] as s join [dbo].[Course] as c on
s.CourseID=c.CourseID join [dbo].[Person] as p on s.StudentID=p.PersonID
where c.Title=@CourseTitle and p.FirstName=@FirstName
and p.LastName= @LastName
END
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE PROCEDURE [dbo].[InsertPerson]
-- Add the parameters for the stored procedure here
@FirstName nvarchar(50),@LastName nvarchar(50),
@PersonID int output
AS
BEGIN
    insert [dbo].[Person](LastName,FirstName) Values(@LastName,@FirstName)

    set @PersonID=SCOPE_IDENTITY()
END
Go

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Course]([CourseID] [nvarchar](10) NOT NULL,
[Year] [smallint] NOT NULL,
[Title] [nvarchar](100) NOT NULL,
[Credits] [int] NOT NULL,
[DepartmentID] [int] NOT NULL,
 CONSTRAINT [PK_Course] PRIMARY KEY CLUSTERED
(
[CourseID] ASC,
[Year] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Department]([DepartmentID] [int] IDENTITY(1,1) NOT NULL,
[Name] [nvarchar](50) NOT NULL,
[Budget] [money] NOT NULL,
[StartDate] [datetime] NOT NULL,
[Administrator] [int] NULL,
 CONSTRAINT [PK_Department] PRIMARY KEY CLUSTERED
(
[DepartmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[Person]([PersonID] [int] IDENTITY(1,1) NOT NULL,
[LastName] [nvarchar](50) NOT NULL,
[FirstName] [nvarchar](50) NOT NULL,
[HireDate] [datetime] NULL,
[EnrollmentDate] [datetime] NULL,
[Picture] [varbinary](max) NULL,
 CONSTRAINT [PK_School.Student] PRIMARY KEY CLUSTERED
(
[PersonID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[StudentGrade]([EnrollmentID] [int] IDENTITY(1,1) NOT NULL,
[CourseID] [nvarchar](10) NOT NULL,
[StudentID] [int] NOT NULL,
[Grade] [decimal](3, 2) NOT NULL,
 CONSTRAINT [PK_StudentGrade] PRIMARY KEY CLUSTERED
(
[EnrollmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
create view [dbo].[EnglishCourse]
as
select c.CourseID,c.Title,c.Credits,c.DepartmentID
from Course as c join Department as d on c.DepartmentID=d.DepartmentID
where d.Name=N'English'

GO
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1045', 2012, N'Calculus', 4, 7)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1061', 2012, N'Physics', 4, 1)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2021', 2012, N'Composition', 3, 2)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2042', 2012, N'Literature', 4, 2)
SET IDENTITY_INSERT [dbo].[Department] ON

INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (1, N'Engineering', 350000.0000, CAST(0x0000999C00000000 AS DateTime), 2)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (2, N'English', 120000.0000, CAST(0x0000999C00000000 AS DateTime), 6)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (4, N'Economics', 200000.0000, CAST(0x0000999C00000000 AS DateTime), 4)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (7, N'Mathematics', 250024.0000, CAST(0x0000999C00000000 AS DateTime), 3)
SET IDENTITY_INSERT [dbo].[Department] OFF
SET IDENTITY_INSERT [dbo].[Person] ON

INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (1, N'Hu', N'Nan', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (2, N'Norman', N'Laura', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (3, N'Olivotto', N'Nino', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (4, N'Anand', N'Arturo', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (5, N'Jai', N'Damien', NULL, CAST(0x0000A0BF00000000 AS DateTime))
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (6, N'Holt', N'Roger', CAST(0x000097F100000000 AS DateTime), NULL)
INSERT [dbo].[Person] ([PersonID], [LastName], [FirstName], [HireDate], [EnrollmentDate]) VALUES (7, N'Martin', N'Randall', CAST(0x00008B1A00000000 AS DateTime), NULL)
SET IDENTITY_INSERT [dbo].[Person] OFF
SET IDENTITY_INSERT [dbo].[StudentGrade] ON

INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (1, N'C1045', 1, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (2, N'C1045', 2, CAST(3.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (3, N'C1045', 3, CAST(2.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (4, N'C1045', 4, CAST(4.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (5, N'C1045', 5, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (6, N'C1061', 1, CAST(4.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (7, N'C1061', 3, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (8, N'C1061', 4, CAST(2.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (9, N'C1061', 5, CAST(1.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (10, N'C2021', 1, CAST(2.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (11, N'C2021', 2, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (12, N'C2021', 4, CAST(3.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (13, N'C2021', 5, CAST(3.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (14, N'C2042', 1, CAST(2.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (15, N'C2042', 2, CAST(3.50 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (16, N'C2042', 3, CAST(4.00 AS Decimal(3, 2)))
INSERT [dbo].[StudentGrade] ([EnrollmentID], [CourseID], [StudentID], [Grade]) VALUES (17, N'C2042', 5, CAST(3.00 AS Decimal(3, 2)))
SET IDENTITY_INSERT [dbo].[StudentGrade] OFF
ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])
REFERENCES [dbo].[Department] ([DepartmentID])
GO
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]
GO
ALTER TABLE [dbo].[StudentGrade]  WITH CHECK ADD  CONSTRAINT [FK_StudentGrade_Student] FOREIGN KEY([StudentID])
REFERENCES [dbo].[Person] ([PersonID])
GO
ALTER TABLE [dbo].[StudentGrade] CHECK CONSTRAINT [FK_StudentGrade_Student]
GO
```

A listagem de código a seguir:

[!code-csharp[SqlClient_RetrieveIdentity#1](~/../sqlclient/doc/samples/SqlClient_RetrieveIdentity.cs#1)]

## <a name="see-also"></a>Confira também

- [Recuperar e modificar dados no ADO.NET](retrieving-modifying-data.md)
- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Atualizar fontes de dados com DataAdapters](update-data-sources-with-dataadapters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
