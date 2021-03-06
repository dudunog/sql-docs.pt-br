---
title: 'Etapa 3: como conectar ao SQL usando pyodbc'
description: A etapa 3 é uma prova de conceito, que mostra como você pode se conectar ao SQL Server usando Python e pyODBC. Os exemplos básicos demonstram a seleção e a inserção de dados.
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26cbdea53547f30a59dc6953d7bf68bddc712164
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807041"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Etapa 3: Prova de conceito da conexão ao SQL usando pyodbc

Este exemplo é uma prova de conceito. O código de exemplo está simplificado para fins de clareza e não necessariamente representa as melhores práticas recomendadas pela Microsoft.  

Para começar, execute o script de exemplo a seguir. Crie um arquivo chamado test.py e adicione cada snippet de código conforme prosseguir. 

```
> python test.py
```
  
## <a name="connect"></a>Conectar  
  
```python
import pyodbc 
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="run-query"></a>Executar consulta  
  
A função cursor.execute pode ser usada para recuperar um conjunto de resultados de uma consulta no Banco de Dados SQL. Essa função aceita uma consulta e retorna um conjunto de resultados que pode ser iterado com o uso de cursor.fetchone()
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="insert-a-row"></a>Inserir uma linha  
  
Neste exemplo, você verá como executar uma instrução [INSERT](../../../t-sql/statements/insert-transact-sql.md) com segurança e como passar parâmetros. Os parâmetros protegem seu aplicativo contra a [injeção de SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md).    
  
  
```python
#Sample insert query
cursor.execute("""
INSERT INTO SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) 
VALUES (?,?,?,?,?)""",
'SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP) 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print('Inserted Product key is ' + str(row[0]))
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-and-the-connection-string"></a>Azure Active Directory e a cadeia de conexão

O pyODBC usa o driver ODBC da Microsoft para SQL Server.
Se a versão do driver ODBC for 17.1 ou posterior, você poderá usar o modo interativo do Azure Active Directory do driver ODBC por meio de pyODBC.
Essa opção interativa funcionará se o Python e o pyODBC permitirem que o driver ODBC exiba a caixa de diálogo. Essa opção só está disponível nos sistemas operacionais Windows. 

### <a name="example-connection-string-for-azure-active-directory-interactive-authentication"></a>Exemplo de cadeia de conexão para autenticação interativa do Azure Active Directory

O exemplo a seguir fornece uma cadeia de conexão ODBC que especifica a autenticação interativa do Azure Active Directory:

`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

Para obter mais informações sobre as opções de autenticação do driver ODBC, confira [Usar o Azure Active Directory com o Driver ODBC](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords).

## <a name="next-steps"></a>Próximas etapas
  
Para saber mais, confira o [Centro de Desenvolvedores do Python](https://azure.microsoft.com/develop/python/).
